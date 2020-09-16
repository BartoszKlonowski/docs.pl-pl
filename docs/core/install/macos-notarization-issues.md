---
title: Praca z macOS Catalina Notarization
description: Jak obsłużyć problemy z notarization i certyfikatami w programie macOS po zainstalowaniu środowiska uruchomieniowego platformy .NET Core, zestawu SDK i aplikacji utworzonych za pomocą platformy .NET Core.
author: adegeo
ms.author: adegeo
ms.date: 02/14/2020
ms.openlocfilehash: 616f163856cca48ccc6d1a14e0c6e68d56379c0c
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90538305"
---
# <a name="macos-catalina-notarization-and-the-impact-on-net-core-downloads-and-projects"></a>macOS Catalina Notarization i wpływ na pobieranie i projekty platformy .NET Core

Począwszy od programu macOS Catalina (wersja 10,15), całe oprogramowanie skompilowane po 1 czerwca 2019 i dystrybuowane z IDENTYFIKATORem dewelopera musi być notarialne. To wymaganie dotyczy środowiska uruchomieniowego .NET Core, zestaw .NET Core SDK i oprogramowania utworzonego za pomocą platformy .NET Core. W tym artykule opisano typowe scenariusze, które mogą być używane przez platformę .NET Core i macOS notarization.

## <a name="installing-net-core"></a>Instalowanie programu .NET Core

Instalatory dla programu .NET Core (zarówno środowisko uruchomieniowe, jak i zestaw SDK) w wersji 3,1, 3,0 i 2,1 zostały zgłoszone od 18 lutego 2020. Wcześniejsze wersje nie zostały ujawnione. Możesz ręcznie zainstalować nieświadomą wersję programu .NET Core, pobierając najpierw Instalatora, a następnie używając `sudo installer` polecenia. Aby uzyskać więcej informacji, zobacz [Pobierz i ręcznie zainstaluj program macOS](./macos.md#download-and-manually-install).

Począwszy od następujących wersji, instalatorzy programu .NET Core są notariusz:

- Środowisko uruchomieniowe platformy .NET Core
  - 2.1.16
  - 3.0.3
  - 3.1.2

- Zestaw .NET Core SDK
  - 2.1.512
  - 3.0.103
  - 3.1.102

## <a name="apphost-is-disabled-by-default"></a>appHost jest domyślnie wyłączona

Domyślnie nienotarialne wersje zestaw .NET Core SDK 3,0 i powyżej tworzą natywny plik wykonywalny (znany jako **appHost**), gdy projekt kompiluje, publikuje lub jest uruchomiony. Ten plik wykonywalny jest wygodnym sposobem uruchomienia aplikacji. W przeciwnym razie aplikacja musi być uruchomiona, uruchamiając polecenie `dotnet <filename.dll>` . Po włączeniu appHost `dotnet run` polecenie jest wywoływane w kontekście appHost. Aby uzyskać więcej informacji, zobacz [kontekst appHost](#context-of-the-apphost).

Począwszy od wersji zestaw .NET Core SDK 3,0 i nowszych, plik wykonywalny appHost nie jest generowany domyślnie. Generowanie appHost można włączyć przy użyciu [`UseAppHost`](../project-sdk/msbuild-props.md#useapphost) Ustawienia Boolean w pliku projektu. Możesz również przełączać appHost z `-p:UseAppHost` parametrem w wierszu polecenia dla określonego polecenia, `dotnet` które uruchamiasz:

- Plik projektu

  ```xml
  <PropertyGroup>
    <UseAppHost>true</UseAppHost>
  </PropertyGroup>
  ```

- Parametr wiersza polecenia

  ```dotnetcli
  dotnet run -p:UseAppHost=true
  ```

AppHost jest zawsze tworzona przy publikowaniu [własnej aplikacji.](../deploying/index.md#publish-self-contained)

Aby uzyskać więcej informacji na temat tego `UseAppHost` Ustawienia, zobacz [Właściwości programu MSBuild dla Microsoft. NET. SDK](../project-sdk/msbuild-props.md#useapphost).

### <a name="context-of-the-apphost"></a>Kontekst appHost

Gdy appHost jest włączona w projekcie i używasz `dotnet run` polecenia, aby uruchomić aplikację, aplikacja jest wywoływana w kontekście appHost, a nie domyślnym hostem (domyślnym hostem jest `dotnet` polecenie). Jeśli appHost jest wyłączona w projekcie, `dotnet run` polecenie uruchamia aplikację w kontekście domyślnego hosta. Nawet jeśli appHost jest wyłączona, opublikowanie aplikacji jako samodzielnego spowoduje wygenerowanie pliku wykonywalnego appHost, a użytkownicy używają tego pliku wykonywalnego do uruchomienia aplikacji. Uruchomienie aplikacji przy użyciu `dotnet <filename.dll>` wywoła aplikację z domyślnym hostem, udostępnionym środowisku uruchomieniowym.

Po wywołaniu aplikacji używającej appHost partycja certyfikatu, do której uzyskuje dostęp aplikacja, różni się od notarialnego hosta domyślnego. Jeśli aplikacja musi uzyskać dostęp do certyfikatów zainstalowanych za pośrednictwem domyślnego hosta, użyj `dotnet run` polecenia, aby uruchomić aplikację z pliku projektu, lub użyj polecenia, `dotnet <filename.dll>` Aby uruchomić aplikację bezpośrednio.

Więcej informacji na temat tego scenariusza znajduje się w sekcji [ASP.NET Core i macOS oraz certyfikaty](#aspnet-core-and-macos-and-certificates) .

## <a name="aspnet-core-and-macos-and-certificates"></a>ASP.NET Core i macOS oraz certyfikaty

Platforma .NET Core zapewnia możliwość zarządzania certyfikatami w łańcuchu macOS z <xref:System.Security.Cryptography.X509Certificates> klasą. Dostęp do pęku kluczy macOS używa tożsamości aplikacji jako klucza podstawowego podczas wybierania partycji do uwzględnienia. Na przykład niepodpisane aplikacje przechowują wpisy tajne w partycji bez znaku, ale podpisane aplikacje przechowują wpisy tajne w partycjach, które mają dostęp do nich. Źródło wykonania, które wywołuje aplikację, decyduje o tym, której partycji użyć.

Platforma .NET Core udostępnia trzy źródła wykonywania: [appHost](#apphost-is-disabled-by-default), host domyślny ( `dotnet` polecenie) i hosta niestandardowego. Każdy model wykonywania może mieć różne tożsamości, podpisane lub niepodpisane i ma dostęp do różnych partycji w łańcuchu kluczy. Certyfikaty zaimportowane przez jeden tryb mogą nie być dostępne z innego. Na przykład, notarialne wersje platformy .NET Core mają domyślnie podpisanym hostem. Certyfikaty są importowane do bezpiecznej partycji na podstawie jej tożsamości. Te certyfikaty nie są dostępne z wygenerowanego appHost, ponieważ appHost jest niepodpisany.

Inny przykład domyślnie ASP.NET Core importuje domyślny certyfikat SSL za pośrednictwem domyślnego hosta. ASP.NET Core aplikacji korzystających z appHost nie będzie mieć dostępu do tego certyfikatu i wystąpi błąd podczas wykrywania przez program .NET Core certyfikatu jest niedostępny. Komunikat o błędzie zawiera instrukcje dotyczące sposobu rozwiązania tego problemu.

Jeśli jest wymagane Udostępnianie certyfikatów, macOS udostępnia opcje konfiguracji za pomocą `security` Narzędzia.

Aby uzyskać więcej informacji na temat rozwiązywania problemów z certyfikatem ASP.NET Core, zobacz [Wymuszanie protokołu HTTPS w programie ASP.NET Core](/aspnet/core/security/enforcing-ssl?view=aspnetcore-3.1&tabs=visual-studio#troubleshoot-certificate-problems).

## <a name="default-entitlements"></a>Uprawnienia domyślne

Domyślny Host platformy .NET Core ( `dotnet` polecenie) ma zestaw domyślnych uprawnień. Te uprawnienia są wymagane do prawidłowego działania platformy .NET Core. Istnieje możliwość, że aplikacja może potrzebować dodatkowych uprawnień. w takim przypadku należy wygenerować i użyć [appHost](#apphost-is-disabled-by-default) , a następnie dodać wymagane uprawnienia lokalnie.

Domyślny zestaw uprawnień dla platformy .NET Core:

- `com.apple.security.cs.allow-jit`
- `com.apple.security.cs.allow-unsigned-executable-memory`
- `com.apple.security.cs.allow-dyld-environment-variables`
- `com.apple.security.cs.disable-library-validation`

## <a name="notarize-a-net-core-app"></a>Notarize aplikacji .NET Core

Jeśli aplikacja ma być uruchamiana w witrynie macOS Catalina (wersja 10,15) lub nowsza, należy notarize aplikację. AppHost przesyłana z aplikacją dla notarization powinna być używana z co najmniej tymi samymi [domyślnymi uprawnieniami](#default-entitlements) dla platformy .NET Core.

## <a name="next-steps"></a>Następne kroki

- [Zależności i wymagania dotyczące platformy .NET Core](macos.md#dependencies).
- [Zainstaluj środowisko uruchomieniowe programu .NET Core i zestaw SDK](macos.md).
