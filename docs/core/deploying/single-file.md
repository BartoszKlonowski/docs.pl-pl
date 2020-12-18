---
title: Aplikacja pojedynczego pliku
description: Dowiedz się, co to jest aplikacja z pojedynczym plikiem i dlaczego należy rozważyć użycie tego modelu wdrażania aplikacji.
author: lakshanf
ms.author: lakshanf
ms.date: 12/17/2020
ms.openlocfilehash: e2d2c9ed4c28d11a77e4f840602982a36cf1c80c
ms.sourcegitcommit: 4b79862c5b41fbd86cf38f926f6a49516059f6f2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/18/2020
ms.locfileid: "97678146"
---
# <a name="single-file-deployment-and-executable"></a>Wdrażanie i wykonywanie przy użyciu jednego pliku

Zgrupowanie wszystkich plików zależnych od aplikacji do jednego pliku binarnego zapewnia deweloperowi aplikacji z opcją atrakcyjną w celu wdrożenia i dystrybucji aplikacji jako pojedynczy plik. Ten model wdrażania został udostępniony od platformy .NET Core 3,0 i został ulepszony w programie .NET 5,0. Wcześniej w programie .NET Core 3,0, gdy użytkownik uruchamia aplikację z jednym plikiem, host .NET Core najpierw wyodrębnia wszystkie pliki do katalogu tymczasowego przed uruchomieniem aplikacji. Program .NET 5,0 podnosi to środowisko, bezpośrednio uruchamiając kod bez konieczności wyodrębniania plików z aplikacji.

Wdrożenie pojedynczego pliku jest dostępne zarówno dla [modelu wdrażania zależnego od platformy](index.md#publish-framework-dependent) , jak i [aplikacji samodzielnych](index.md#publish-self-contained). Rozmiar pojedynczego pliku w aplikacji samodzielnej jest duży, ponieważ będzie obejmował środowisko uruchomieniowe i biblioteki struktury. Opcja wdrożenia pojedynczego pliku może być łączona z [ReadyToRun](ready-to-run.md) i [Trim (funkcja eksperymentalna w programie .NET 5,0)](trim-self-contained.md) opcje publikowania.

## <a name="api-incompatibility"></a>Niezgodność interfejsu API

Niektóre interfejsy API nie są zgodne z wdrożeniem pojedynczego pliku, a aplikacje mogą wymagać modyfikacji, jeśli korzystają z tych interfejsów API. Jeśli używasz struktury lub pakietu innej firmy, istnieje możliwość, że mogą one również korzystać z jednego z tych interfejsów API i wymagać modyfikacji. Najczęstsze przyczyny problemów są zależne od ścieżek plików plików lub bibliotek DLL dostarczanych z aplikacją.

W poniższej tabeli znajdują się odpowiednie szczegóły interfejsu API biblioteki środowiska uruchomieniowego dotyczące użycia pojedynczego pliku.

| Interfejs API                            | Uwaga                                                                   |
|--------------------------------|------------------------------------------------------------------------|
| `Assembly.Location`            | Zwraca pusty ciąg.                                               |
| `Module.FullyQualifiedName`    | Zwraca ciąg z wartością `<Unknown>` lub zgłasza wyjątek. |
| `Module.Name`                  | Zwraca ciąg o wartości `<Unknown>` .                        |
| `Assembly.GetFile`             | Zgłasza <xref:System.IO.IOException> .                                   |
| `Assembly.GetFiles`            | Zgłasza <xref:System.IO.IOException> .                                   |
| `Assembly.CodeBase`            | Zgłasza <xref:System.PlatformNotSupportedException> .                    |
| `Assembly.EscapedCodeBase`     | Zgłasza <xref:System.PlatformNotSupportedException> .                    |
| `AssemblyName.CodeBase`        | Zwraca wartość `null`.                                                        |
| `AssemblyName.EscapedCodeBase` | Zwraca wartość `null`.                                                        |

Mamy pewne zalecenia dotyczące rozwiązywania typowych scenariuszy:

* Aby uzyskać dostęp do plików obok pliku wykonywalnego, użyj programu <xref:System.AppContext.BaseDirectory?displayProperty=nameWithType> .

* Aby znaleźć nazwę pliku wykonywalnego, użyj pierwszego elementu <xref:System.Environment.GetCommandLineArgs?displayProperty=nameWithType> .

* Aby uniknąć całkowitego wysyłania luźnych plików, należy rozważyć użycie [zasobów osadzonych](../../framework/resources/creating-resource-files-for-desktop-apps.md).

## <a name="attaching-a-debugger"></a>Dołączanie debugera

W systemie Linux jedynym debugerem, który może dołączyć do samodzielnego procesu pojedynczego pliku lub Zrzuty awaryjne debugowania, jest [sos z LLDB](../diagnostics/dotnet-sos.md).

W systemach Windows i Mac program Visual Studio i VS Code mogą służyć do debugowania zrzutów awaryjnych. Dołączanie do uruchomionego samodzielnego pliku wykonywalnego wymaga dodatkowego pliku: _mscordbi. { DLL, dlatego}_.

Bez tego pliku program Visual Studio może generować błąd "nie można dołączyć do procesu. Składnik debugowania nie jest zainstalowany. i VS Code mogą generować błąd "nie można dołączyć do procesu: nieznany błąd: 0x80131c3c".

Aby naprawić te błędy, _mscordbi_ musi zostać skopiowana obok pliku wykonywalnego. _mscordbi_ jest `publish` Domyślnie ED w PODkatalogu z identyfikatorem środowiska uruchomieniowego aplikacji. Na przykład jeśli jedna z nich była opublikowana samodzielny plik wykonywalny przy użyciu `dotnet` interfejsu wiersza polecenia dla systemu Windows za pomocą parametrów `-r win-x64` , plik wykonywalny zostanie umieszczony w pliku _bin/debug/NET 5.0/win-x64/Publish_. Kopia _mscordbi.dll_ byłaby obecna w _bin/debug/NET 5.0/win-x64_.

## <a name="other-considerations"></a>Inne zagadnienia

Pojedynczy plik domyślnie nie obsługuje bibliotek natywnych. W systemie Linux wstępnie łączymy środowisko uruchomieniowe z pakietem i tylko biblioteki natywne aplikacji są wdrażane w tym samym katalogu, w którym znajduje się aplikacja Jednoplikowa. W systemie Windows połączymy tylko kod hostingu, a biblioteki natywne środowiska uruchomieniowego i aplikacji są wdrażane w tym samym katalogu, w którym znajduje się aplikacja pojedynczego pliku. Jest to konieczne w celu zapewnienia dobrego środowiska debugowania, które wymaga wykluczenia plików natywnych z pojedynczego pliku. Istnieje możliwość ustawienia flagi, `IncludeNativeLibrariesForSelfExtract` Aby uwzględnić biblioteki natywne w pojedynczym zbiorze plików, ale te pliki zostaną wyodrębnione do katalogu tymczasowego na komputerze klienckim po uruchomieniu aplikacji pojedynczego pliku.

Aplikacja Jednoplikowa będzie zawierała wszystkie powiązane pliki PDB obok niej i nie zostanie domyślnie zawiązana. Jeśli chcesz uwzględnić plików pdb wewnątrz zestawu dla projektów, które tworzysz, ustaw polecenie `DebugType` na zgodnie z `embedded` [poniższym](#include-pdb-files-inside-the-bundle) opisem.

Zarządzane składniki języka C++ nie są dobrze dopasowane do wdrożenia jednoplikowego i zalecamy zapisanie aplikacji w języku C# lub innym niezarządzanym języku C++ w celu zapewnienia zgodności z pojedynczym plikiem.

## <a name="exclude-files-from-being-embedded"></a>Wykluczanie plików z osadzania

Niektóre pliki można jawnie wykluczyć z osadzania w pojedynczym pliku przez ustawienie następujących metadanych:

```xml
<ExcludeFromSingleFile>true</ExcludeFromSingleFile>
```

Na przykład w celu umieszczenia niektórych plików w katalogu publikowania, ale nie są one powiązane z pojedynczym plikiem:

```xml
<ItemGroup>
  <Content Update="Plugin.dll">
    <CopyToPublishDirectory>PreserveNewest</CopyToPublishDirectory>
    <ExcludeFromSingleFile>true</ExcludeFromSingleFile>
  </Content>
</ItemGroup>
```

## <a name="include-pdb-files-inside-the-bundle"></a>Uwzględnij pliki PDB wewnątrz pakietu

Plik PDB zestawu może być osadzony w samym zestawie ( `.dll` ) przy użyciu poniższego ustawienia. Ponieważ symbole są częścią zestawu, będą również częścią aplikacji jednoplikowej:

```xml
<DebugType>embedded</DebugType>
```

Na przykład Dodaj następującą właściwość do pliku projektu zestawu, aby osadzić plik PDB w tym zestawie:

```xml
<PropertyGroup>
  <DebugType>embedded</DebugType>
</PropertyGroup>
```

## <a name="publish-a-single-file-app---sample-project-file"></a>Publikowanie pojedynczego pliku aplikacji — przykładowego pliku projektu

Oto przykładowy plik projektu, który określa publikację pojedynczego pliku:

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net5.0</TargetFramework>
    <PublishSingleFile>true</PublishSingleFile>
    <SelfContained>true</SelfContained>
    <RuntimeIdentifier>win-x64</RuntimeIdentifier>
    <PublishTrimmed>true</PublishTrimmed>
    <PublishReadyToRun>true</PublishReadyToRun>
  </PropertyGroup>

</Project>
```

Te właściwości mają następujące funkcje:

* `PublishSingleFile` -Włącza publikowanie Jednoplikowe.
* `SelfContained` -Określa, czy aplikacja będzie samodzielna lub zależna od struktury.
* `RuntimeIdentifier` -Określa docelowy [Typ systemu operacyjnego i procesora CPU](../rid-catalog.md) .
* `PublishTrimmed` -Umożliwia użycie [przycinania zestawu](trim-self-contained.md), który jest obsługiwany tylko w przypadku aplikacji samodzielnych.
* `PublishReadyToRun` -Włącza [kompilację w czasie (AOT)](ready-to-run.md).

**Uwagi:**

* Aplikacje są zależne od systemu operacyjnego i architektury. Należy opublikować dla każdej konfiguracji, na przykład Linux x64, Linux ARM64, Windows x64 i tak dalej.
* Pliki konfiguracji, takie jak *\*.runtimeconfig.json*, są zawarte w pojedynczym pliku. Jeśli jest wymagany dodatkowy plik konfiguracji, możesz go umieścić obok pojedynczego pliku.

## <a name="publish-a-single-file-app---cli"></a>Publikowanie pojedynczego pliku aplikacji — interfejs wiersza polecenia

Opublikuj aplikację pojedynczego pliku przy użyciu polecenia [dotnet Publish](../tools/dotnet-publish.md) . Po opublikowaniu aplikacji ustaw następujące właściwości:

- Publikuj dla określonego środowiska uruchomieniowego: `-r win-x64`
- Publikuj jako pojedynczy plik: `-p:PublishSingleFile=true`

W poniższym przykładzie jest publikowana aplikacja dla systemu Windows jako samodzielna aplikacja pojedynczego pliku.

```dotnetcli
dotnet publish -r win-x64 -p:PublishSingleFile=true --self-contained true
```

Poniższy przykład umożliwia opublikowanie aplikacji dla systemu Linux jako zależnej od struktury aplikacji pojedynczego pliku.

```dotnetcli
dotnet publish -r linux-x64 -p:PublishSingleFile=true --self-contained false
```

Aby uzyskać więcej informacji, zobacz [publikowanie aplikacji .NET Core za pomocą interfejs wiersza polecenia platformy .NET Core](deploy-with-cli.md).

## <a name="publish-a-single-file-app---visual-studio"></a>Publikowanie aplikacji pojedynczego pliku — Visual Studio

Program Visual Studio tworzy Profile publikowania wielokrotnego użytku, które kontrolują sposób publikowania aplikacji.

01. W okienku **Eksplorator rozwiązań** kliknij prawym przyciskiem myszy projekt, który chcesz opublikować. Kliknij opcję **Opublikuj**.

    :::image type="content" source="media/single-file/visual-studio-solution-explorer.png" alt-text="Eksplorator rozwiązań z menu po kliknięciu prawym przyciskiem myszy wyróżnianie opcji Publikuj.":::

    Jeśli nie masz jeszcze profilu publikowania, postępuj zgodnie z instrukcjami, aby utworzyć jeden, i wybierz typ docelowy **folderu** .

01. Wybierz pozycję **Edytuj**.

    :::image type="content" source="media/single-file/visual-studio-publish-edit-settings.png" alt-text="Profil publikacji programu Visual Studio za pomocą przycisku Edytuj.":::

01. W oknie dialogowym **Ustawienia profilu** ustaw następujące opcje:

    - Ustaw **Tryb wdrożenia** na **własny**.
    - Ustaw **docelowy środowisko uruchomieniowe** na platformę, w której chcesz publikować.
    - Wybierz pozycję **Wygeneruj pojedynczy plik**.

    Wybierz pozycję **Zapisz** , aby zapisać ustawienia i powrócić do okna dialogowego **Publikowanie** .

    :::image type="content" source="media/single-file/visual-studio-publish-single-file-properties.png" alt-text="Okno dialogowe ustawień profilu z trybem wdrożenia, docelowym środowiskiem uruchomieniowym i opcją pojedynczego pliku.":::

01. Wybierz pozycję **Publikuj** , aby opublikować aplikację jako pojedynczy plik.

Aby uzyskać więcej informacji, zobacz [publikowanie aplikacji .NET Core za pomocą programu Visual Studio](deploy-with-vs.md).

## <a name="publish-a-single-file-app---visual-studio-for-mac"></a>Publikowanie aplikacji pojedynczego pliku — Visual Studio dla komputerów Mac

Visual Studio dla komputerów Mac nie udostępnia opcji publikowania aplikacji jako pojedynczego pliku. Należy opublikować ręcznie, postępując zgodnie z instrukcjami zawartymi w sekcji [Publikowanie pojedynczego pliku App-CLI](#publish-a-single-file-app---cli) . Aby uzyskać więcej informacji, zobacz [publikowanie aplikacji .NET Core za pomocą interfejs wiersza polecenia platformy .NET Core](deploy-with-cli.md).

## <a name="see-also"></a>Zobacz także

- [Wdrażanie aplikacji .NET Core](index.md).
- [Publikowanie aplikacji platformy .NET Core za pomocą interfejs wiersza polecenia platformy .NET Core](deploy-with-cli.md).
- [Publikowanie aplikacji platformy .NET Core w programie Visual Studio](deploy-with-vs.md).
- [ `dotnet publish` polecenie](../tools/dotnet-publish.md).
