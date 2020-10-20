---
title: Co nowego w programie .NET Core 2.0
description: Dowiedz się więcej o nowych funkcjach dostępnych w programie .NET Core.
ms.date: 08/13/2017
ms.openlocfilehash: bdca38d1584107727fe8e20b80ab2337f4cb05f1
ms.sourcegitcommit: 67ebdb695fd017d79d9f1f7f35d145042d5a37f7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/20/2020
ms.locfileid: "92223717"
---
# <a name="whats-new-in-net-core-20"></a>Co nowego w programie .NET Core 2.0

Program .NET Core 2,0 zawiera ulepszenia i nowe funkcje w następujących obszarach:

- [Narzędzia](#tooling)
- [Obsługa języków](#language-support)
- [Ulepszenia platformy](#platform-improvements)
- [Zmiany interfejsu API](#api-changes-and-library-support)
- [integracja z programem Visual Studio](#visual-studio-integration)
- [Udoskonalenia dokumentacji](#documentation-improvements)

## <a name="tooling"></a>Narzędzia

### <a name="dotnet-restore-runs-implicitly"></a>niejawnie uruchamiane dotnet restore

W poprzednich wersjach programu .NET Core należy uruchomić polecenie [dotnet Restore](../tools/dotnet-restore.md) , aby pobrać zależności natychmiast po utworzeniu nowego projektu za pomocą polecenia [dotnet New](../tools/dotnet-new.md) , a także za każdym razem, gdy dodano nową zależność do projektu.

[!INCLUDE[DotNet Restore Note](~/includes/dotnet-restore-note.md)]

Możesz również wyłączyć automatyczne wywoływanie `dotnet restore` przez przekazanie `--no-restore` przełącznika do `new` `run` poleceń,, `build` ,, `publish` `pack` i `test` .

### <a name="retargeting-to-net-core-20"></a>Przekierowywanie do programu .NET Core 2,0

Jeśli jest zainstalowany zestaw SDK programu .NET Core 2,0, projekty przeznaczone dla platformy .NET Core 1. x można przekierować do programu .NET Core 2,0.

Aby przekierować do programu .NET Core 2,0, edytuj plik projektu, zmieniając wartość `<TargetFramework>` elementu (lub `<TargetFrameworks>` elementu, jeśli masz więcej niż jeden obiekt docelowy w pliku projektu) od 1. x do 2,0:

```xml
<PropertyGroup>
    <TargetFramework>netcoreapp2.0</TargetFramework>
 </PropertyGroup>
```

Można również przekierować .NET Standard biblioteki do .NET Standard 2,0 w ten sam sposób:

```xml
<PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
 </PropertyGroup>
```

Aby uzyskać więcej informacji na temat migrowania projektu do programu .NET Core 2,0, zobacz [Migrowanie z ASP.NET Core 1. x do ASP.NET Core 2,0](/aspnet/core/migration/1x-to-2x/index).

## <a name="language-support"></a>Obsługa języków

Oprócz obsługi języków C# i F #, .NET Core 2,0 obsługuje również Visual Basic.

### <a name="visual-basic"></a>Visual Basic

W wersji 2,0 program .NET Core obsługuje teraz Visual Basic 2017. Za pomocą Visual Basic można utworzyć następujące typy projektów:

- Aplikacje konsolowe platformy .NET Core
- Biblioteki klas platformy .NET Core
- .NET Standard biblioteki klas
- Projekty testów jednostkowych .NET Core
- Projekty testowe programu .NET Core xUnit

Na przykład aby utworzyć Visual Basic aplikację "Hello world", wykonaj następujące kroki w wierszu polecenia:

1. Otwórz okno konsoli, Utwórz katalog dla projektu i ustaw go jako bieżący katalog.

1. Wprowadź polecenie `dotnet new console -lang vb` .

   Polecenie tworzy plik projektu z `.vbproj` rozszerzeniem pliku wraz z Visual Basic plikiem kodu źródłowego o nazwie *program. vb*. Ten plik zawiera kod źródłowy do zapisu ciągu "Hello world!" do okna konsoli.

1. Wprowadź polecenie `dotnet run` . [Interfejs wiersza polecenia platformy .NET Core](../tools/index.md) automatycznie kompiluje i wykonuje aplikację, która wyświetla komunikat "Hello World!" w oknie konsoli.

### <a name="support-for-c-71"></a>Obsługa języka C# 7,1

Program .NET Core 2,0 obsługuje język C# 7,1, który dodaje wiele nowych funkcji, takich jak:

- `Main`Metoda, punkt wejścia aplikacji, może być oznaczona za pomocą słowa kluczowego [Async](../../csharp/language-reference/keywords/async.md) .
- Wywnioskowane nazwy krotek.
- Wyrażenia domyślne.

<!-- For more information see [link to C# what's new](url). -->

## <a name="platform-improvements"></a>Ulepszenia platformy

Program .NET Core 2,0 zawiera szereg funkcji, które ułatwiają instalowanie programu .NET Core i korzystanie z nich w obsługiwanych systemach operacyjnych.

### <a name="net-core-for-linux-is-a-single-implementation"></a>.NET Core dla systemu Linux to jedna implementacja

Platforma .NET Core 2,0 oferuje jedną implementację systemu Linux, która działa w przypadku wielu dystrybucji systemu Linux. Program .NET Core 1. x wymaga pobrania implementacji systemu Linux dotyczącej dystrybucji.

Możesz również opracowywać aplikacje przeznaczone dla systemu Linux jako pojedynczy system operacyjny. W przypadku programu .NET Core 1. x wymagana jest Każda dystrybucja systemu Linux osobno.

### <a name="support-for-the-apple-cryptographic-libraries"></a>Obsługa bibliotek kryptograficznych firmy Apple

Platforma .NET Core 1. x w systemie macOS wymagała biblioteki kryptograficznej zestawu narzędzi OpenSSL. Platforma .NET Core 2,0 korzysta z bibliotek kryptograficznych firmy Apple i nie wymaga OpenSSL, więc nie trzeba już jej instalować.

## <a name="api-changes-and-library-support"></a>Obsługa zmian i bibliotek interfejsu API

### <a name="support-for-net-standard-20"></a>Obsługa .NET Standard 2,0

.NET Standard definiuje zestaw interfejsów API, które muszą być dostępne w implementacjach platformy .NET, które są zgodne z tą wersją Standard. .NET Standard jest przeznaczona dla deweloperów biblioteki. Ma ona na celu zagwarantowanie funkcjonalności dostępnej dla biblioteki, która jest przeznaczona dla wersji .NET Standard w każdej implementacji platformy .NET. Platforma .NET Core 1. x obsługuje .NET Standard w wersji 1,6; program .NET Core 2,0 obsługuje najnowszą wersję .NET Standard 2,0. Aby uzyskać więcej informacji, zobacz [.NET Standard](../../standard/net-standard.md).

.NET Standard 2,0 obejmuje ponad 20 000 więcej interfejsów API, niż jest dostępne w .NET Standard 1,6. Większość tego rozwiniętego obszaru powierzchni polega na dołączaniu interfejsów API, które są wspólne dla .NET Framework i platformy Xamarin w .NET Standard.

Biblioteki klas .NET Standard 2,0 mogą również odwoływać się do bibliotek klas .NET Framework, pod warunkiem, że wywoła interfejsy API, które znajdują się w .NET Standard 2,0. Nie jest wymagana ponowna kompilacja bibliotek .NET Framework.

Aby zapoznać się z listą interfejsów API, które zostały dodane do .NET Standard od momentu jego ostatniej wersji, .NET Standard 1,6, zobacz [.NET Standard 2,0 a 1,6](https://raw.githubusercontent.com/dotnet/standard/master/docs/versions/netstandard2.0_diff.md).

### <a name="expanded-surface-area"></a>Rozwinięty obszar powierzchni

Łączna liczba interfejsów API dostępnych w środowisku .NET Core 2,0 jest większa niż dwukrotnie w porównaniu z platformą .NET Core 1,1.

Natomiast [pakiet zgodności systemu Windows](../porting/windows-compat-pack.md) z .NET Framework został również znacznie łatwiejszy.

### <a name="support-for-net-framework-libraries"></a>Obsługa bibliotek .NET Framework

Kod .NET Core może odwoływać się do istniejących bibliotek .NET Framework, w tym istniejących pakietów NuGet. Należy pamiętać, że biblioteki muszą używać interfejsów API, które znajdują się w .NET Standard.

## <a name="visual-studio-integration"></a>integracja z programem Visual Studio

Program Visual Studio 2017 w wersji 15,3 i w niektórych przypadkach Visual Studio dla komputerów Mac oferować szereg znaczących ulepszeń dla deweloperów platformy .NET Core.

### <a name="retargeting-net-core-apps-and-net-standard-libraries"></a>Przekierowywanie aplikacji .NET Core i bibliotek .NET Standard

Jeśli jest zainstalowany zestaw SDK programu .NET Core 2,0, można przekierować projekty platformy .NET Core 1. x do bibliotek .NET Core 2,0 i .NET Standard 1. x do .NET Standard 2,0.

Aby przekierować projekt w programie Visual Studio, Otwórz kartę **aplikacji** okna dialogowego właściwości projektu i zmień wartość **platformy docelowej** na **.net Core 2,0** lub **.NET Standard 2,0**. Możesz również ją zmienić, klikając prawym przyciskiem myszy projekt i wybierając opcję **Edytuj \* plik CSPROJ** . Aby uzyskać więcej informacji, zobacz sekcję dotyczącą [narzędzi](#tooling) wcześniej w tym temacie.

### <a name="live-unit-testing-support-for-net-core"></a>Obsługa funkcji Live Unit Testing dla platformy .NET Core

Za każdym razem, gdy modyfikujesz swój kod, Live Unit Testing automatycznie uruchamia wszystkie objęte testy jednostkowe w tle i wyświetla wyniki i pokrycie kodu na żywo w środowisku programu Visual Studio. Platforma .NET Core 2,0 obsługuje teraz Live Unit Testing. Wcześniej Live Unit Testing był dostępny tylko dla aplikacji .NET Framework.

Aby uzyskać więcej informacji, zobacz [Live Unit Testing z programem Visual Studio](/visualstudio/test/live-unit-testing) i [Live Unit Testing często zadawanych pytań](/visualstudio/test/live-unit-testing-faq).

### <a name="better-support-for-multiple-target-frameworks"></a>Lepsza obsługa wielu platform docelowych

Jeśli tworzysz projekt dla wielu struktur docelowych, możesz teraz wybrać platformę docelową z menu najwyższego poziomu. Na poniższej ilustracji projekt o nazwie SCD1 targets 64-bit macOS X 10,11 ( `osx.10.11-x64` ) i 64-bit Windows 10/Windows Server 2016 ( `win10-x64` ). Możesz wybrać platformę docelową przed wybraniem przycisku projektu, w tym przypadku, aby uruchomić kompilację debugowania.

![Zrzut ekranu przedstawiający wybór platformy docelowej podczas kompilowania projektu.](./media/dotnet-core-2-0/target-framework-selection.png)

### <a name="side-by-side-support-for-net-core-sdks"></a>Obsługa równoczesna dla zestawów SDK platformy .NET Core

Teraz można zainstalować zestaw .NET Core SDK niezależnie od programu Visual Studio. Dzięki temu pojedynczej wersji programu Visual Studio można tworzyć projekty przeznaczone dla różnych wersji platformy .NET Core. Wcześniej program Visual Studio i zestaw .NET Core SDK były ściśle sprzężone; określona wersja zestawu SDK dołączona do określonej wersji programu Visual Studio.

## <a name="documentation-improvements"></a>Udoskonalenia dokumentacji

### <a name="net-application-architecture"></a>Architektura aplikacji .NET

[Architektura aplikacji .NET](https://dotnet.microsoft.com/learn/dotnet/architecture-guides) zapewnia dostęp do zestawu książek elektronicznych, które udostępniają wskazówki, najlepsze rozwiązania i przykładowe aplikacje w przypadku korzystania z platformy .NET do kompilowania:

- [Mikrousługi i kontenery platformy Docker](../../architecture/microservices/index.md)
- [Aplikacje sieci Web z ASP.NET](../../architecture/modern-web-apps-azure/index.md)
- [Aplikacje mobilne przy użyciu platformy Xamarin](/xamarin/xamarin-forms/enterprise-application-patterns/index)
- [Aplikacje wdrożone w chmurze na platformie Azure](/azure/architecture/reference-architectures/index)

## <a name="see-also"></a>Zobacz też

- [Co nowego w ASP.NET Core 2,0](/aspnet/core/aspnetcore-2.0)
