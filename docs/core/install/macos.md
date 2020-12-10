---
title: Zainstaluj platformę .NET na macOS
description: Dowiedz się więcej na temat wersji programu macOS, na których można zainstalować platformę .NET.
author: adegeo
ms.author: adegeo
ms.date: 11/10/2020
ms.openlocfilehash: b1434938a8e8e81da81e495a6b99e6c99467aae1
ms.sourcegitcommit: 81f1bba2c97a67b5ca76bcc57b37333ffca60c7b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/10/2020
ms.locfileid: "97009361"
---
# <a name="install-net-on-macos"></a>Zainstaluj platformę .NET na macOS

> [!div class="op_single_selector"]
>
> - [Instalowanie w systemie Windows](windows.md)
> - [Instalowanie w systemie macOS](macos.md)
> - [Instalowanie w systemie Linux](linux.md)

W tym artykule dowiesz się, jak zainstalować platformę .NET na macOS. Platforma .NET składa się z środowiska uruchomieniowego i zestawu SDK. Środowisko uruchomieniowe służy do uruchamiania aplikacji .NET i może nie być dołączone do aplikacji. Zestaw SDK służy do tworzenia aplikacji i bibliotek platformy .NET. Środowisko uruchomieniowe .NET jest zawsze instalowane z zestawem SDK.

Najnowsza wersja platformy .NET to 5,0.

> [!div class="button"]
> [Pobierz program .NET Core](https://dotnet.microsoft.com/download/dotnet-core)

## <a name="supported-releases"></a>Obsługiwane wersje

Poniższa tabela zawiera listę obecnie obsługiwanych wersji platformy .NET i wersje macOS, w których są obsługiwane. Te wersje pozostają obsługiwane albo wersja [platformy .NET osiągnie koniec obsługi](https://dotnet.microsoft.com/platform/support/policy/dotnet-core).

- ✔️ wskazuje, że wersja platformy .NET Core jest nadal obsługiwana.
- ❌Wskazuje, że wersja programu .NET Core nie jest obsługiwana.

| System operacyjny          | .NET Core 2.1 | .NET Core 3.1 | .NET 5.0 |
|---------------------------|---------------|---------------|----------------|
| macOS 11,0 "Big Sur"        | ✔️ 2,1 ([Informacje o wersji][release-notes-21]) | ✔️ 3,1 ([Informacje o wersji][release-notes-31]) | ✔️ 5,0 ([Informacje o wersji][release-notes-50]) |
| macOS 10,15 "Catalina"    | ✔️ 2,1 ([Informacje o wersji][release-notes-21]) | ✔️ 3,1 ([Informacje o wersji][release-notes-31]) | ✔️ 5,0 ([Informacje o wersji][release-notes-50]) |
| macOS 10,14 "Mojave"      | ✔️ 2,1 ([Informacje o wersji][release-notes-21]) | ✔️ 3,1 ([Informacje o wersji][release-notes-31]) | ✔️ 5,0 ([Informacje o wersji][release-notes-50]) |
| macOS 10,13 "wysoka firma Sierra" | ✔️ 2,1 ([Informacje o wersji][release-notes-21]) | ✔️ 3,1 ([Informacje o wersji][release-notes-31]) | ✔️ 5,0 ([Informacje o wersji][release-notes-50]) |
| macOS 10,12 "Sierra"      | ✔️ 2,1 ([Informacje o wersji][release-notes-21]) | ❌ 3,1 ([Informacje o wersji][release-notes-31]) | ❌ 5,0 ([Informacje o wersji][release-notes-50]) |

## <a name="unsupported-releases"></a>Nieobsługiwane wersje

Następujące wersje platformy .NET nie są ❌ już obsługiwane. Pliki do pobrania dla tych nadal są publikowane:

- 3,0 ([Informacje o wersji][release-notes-30])
- 2,2 ([Informacje o wersji][release-notes-22])
- 2,0 ([Informacje o wersji][release-notes-20])

## <a name="runtime-information"></a>Informacje o środowisku uruchomieniowym

Środowisko uruchomieniowe służy do uruchamiania aplikacji utworzonych przy użyciu platformy .NET. Gdy autor aplikacji publikuje aplikację, może ona obejmować środowisko uruchomieniowe wraz z ich aplikacjami. Jeśli nie obejmują środowiska uruchomieniowego, można zainstalować środowisko uruchomieniowe.

Istnieją trzy różne środowiska uruchomieniowe, które można zainstalować w systemie macOS:

*Środowisko uruchomieniowe ASP.NET Core*\
Uruchamia ASP.NET Core aplikacje. Obejmuje środowisko uruchomieniowe platformy .NET.

*Środowisko uruchomieniowe platformy .NET*\
To środowisko uruchomieniowe jest najprostszym środowiskiem uruchomieniowym i nie zawiera żadnego innego środowiska uruchomieniowego. Zdecydowanie zaleca się zainstalowanie *ASP.NET Core środowiska uruchomieniowego* w celu uzyskania najlepszej zgodności z aplikacjami .NET.

> [!div class="button"]
> [Pobierz środowisko uruchomieniowe platformy .NET](https://dotnet.microsoft.com/download/dotnet-core)

## <a name="sdk-information"></a>Informacje o zestawie SDK

Zestaw SDK służy do kompilowania i publikowania aplikacji i bibliotek platformy .NET. Instalowanie zestawu SDK obejmuje zarówno [środowisko uruchomieniowe](#runtime-information): ASP.NET Core, jak i .NET.

## <a name="dependencies"></a>Zależności

Platforma .NET jest obsługiwana w następujących wersjach macOS:

> [!NOTE]
> `+`Symbol reprezentuje wersję minimalną.

| Wersja platformy .NET Core | macOS                 | Architektury | Więcej informacji    |
| ----------------- | --------------------- | --------------| --- |
| 5,0               | Wysoka firma Sierra (10.13 +)  | x64 | [Więcej informacji](https://github.com/dotnet/core/blob/master/release-notes/5.0/5.0-supported-os.md) |
| 3,1               | Wysoka firma Sierra (10.13 +)  | x64 | [Więcej informacji](https://github.com/dotnet/core/blob/master/release-notes/3.1/3.1-supported-os.md) |
| 3.0               | Wysoka firma Sierra (10.13 +)  | x64 | [Więcej informacji](https://github.com/dotnet/core/blob/master/release-notes/3.0/3.0-supported-os.md) |
| 2.2               | Sierra (10.12 +)       | x64 | [Więcej informacji](https://github.com/dotnet/core/blob/master/release-notes/2.2/2.2-supported-os.md) |
| 2.1               | Sierra (10.12 +)       | x64 | [Więcej informacji](https://github.com/dotnet/core/blob/master/release-notes/2.1/2.1-supported-os.md) |

Począwszy od programu macOS Catalina (wersja 10,15), całe oprogramowanie skompilowane po 1 czerwca 2019, które jest dystrybuowane z IDENTYFIKATORem dewelopera, musi być notarialne. To wymaganie dotyczy środowiska uruchomieniowego .NET, zestawu .NET SDK i oprogramowania utworzonego przy użyciu platformy .NET.

Programy instalacyjne środowiska uruchomieniowego i zestawu SDK dla programów .NET 5,0 i .NET Core 3,1, 3,0 i 2,1 zostały zgłoszone od 18 lutego 2020. Wcześniejsze wersje nie zostały ujawnione. Jeśli uruchomisz zanotarialną aplikację, zobaczysz komunikat o błędzie podobny do następującego:

![Alert notarization macOS Catalina](media/dependencies/macos-notarized-pkg-warning.png)

Aby uzyskać więcej informacji na temat sposobu, w jaki wymuszone — notarization wpływa na platformę .NET (i aplikacje .NET), zobacz [Praca z MacOS Catalina notarization](macos-notarization-issues.md).

## <a name="libgdiplus"></a>libgdiplus

Aplikacje .NET, które używają zestawu *System. Drawing. Common* , wymagają zainstalowania libgdiplus.

Łatwym sposobem uzyskania libgdiplus jest użycie Menedżera pakietów [oprogramowania homebrew ("rozwiązania brew")](https://brew.sh/) dla macOS. Po zainstalowaniu *rozwiązania brew* Zainstaluj libgdiplus, wykonując następujące polecenia w wierszu terminalu (polecenie):

```console
brew update
brew install mono-libgdiplus
```

## <a name="install-with-an-installer"></a>Instalowanie za pomocą Instalatora

macOS ma autonomiczne Instalatory, których można użyć do zainstalowania zestawu .NET 5,0 SDK:

- [Procesory x64 (64-bitowe)](https://dotnet.microsoft.com/download/dotnet-core/5.0)

## <a name="download-and-manually-install"></a>Pobierz i ręcznie zainstaluj

<!-- Note, this content is taken from includes/linux-install-manual.md but changed for macOS. Any fixes should be applied there too, though content may be different -->

Jako alternatywę dla instalatorów macOS dla platformy .NET można pobrać i ręcznie zainstalować zestaw SDK i środowisko uruchomieniowe. Instalacja ręczna jest zwykle wykonywana w ramach testowania ciągłej integracji. Dla deweloperów lub użytkowników zazwyczaj lepiej jest użyć [Instalatora](https://dotnet.microsoft.com/download/dotnet-core).

W przypadku instalowania zestawu .NET SDK nie trzeba instalować odpowiedniego środowiska uruchomieniowego. Najpierw pobierz wydanie **binarne** dla zestawu SDK lub środowiska uruchomieniowego z jednej z następujących lokacji:

- ✔️ [pliki do pobrania w programie .net 5,0](https://dotnet.microsoft.com/download/dotnet/5.0)
- [pliki do pobrania ✔️ .NET Core 3,1](https://dotnet.microsoft.com/download/dotnet-core/3.1)
- [pliki do pobrania ✔️ .NET Core 2,1](https://dotnet.microsoft.com/download/dotnet-core/2.1)
- [Wszystkie pliki do pobrania z platformy .NET Core](https://dotnet.microsoft.com/download/dotnet-core)

Następnie wyodrębnij pobrany plik i użyj polecenia, `export` Aby ustawić zmienne używane przez platformę .NET, a następnie upewnij się, że platforma .NET znajduje się w ścieżce.

Aby wyodrębnić środowisko uruchomieniowe i udostępnić polecenie interfejsu wiersza polecenia platformy .NET w terminalu, najpierw Pobierz wydanie binarne platformy .NET. Następnie otwórz Terminal i uruchom następujące polecenia z katalogu, w którym zapisano plik. Nazwa pliku archiwum może się różnić w zależności od pobranych informacji.

**Aby wyodrębnić środowisko uruchomieniowe, użyj następującego polecenia**:

```bash
mkdir -p "$HOME/dotnet" && tar zxf aspnetcore-runtime-5.0.0-osx-x64.tar.gz -C "$HOME/dotnet"
export DOTNET_ROOT=$HOME/dotnet
export PATH=$PATH:$HOME/dotnet
```

**Użyj następującego polecenia, aby wyodrębnić zestaw SDK**:

```bash
mkdir -p "$HOME/dotnet" && tar zxf dotnet-sdk-5.0.100-osx-x64.tar.gz -C "$HOME/dotnet"
export DOTNET_ROOT=$HOME/dotnet
export PATH=$PATH:$HOME/dotnet
```

> [!TIP]
> Powyższe `export` polecenia sprawiają, że dla sesji terminala, w której został uruchomiony, są dostępne tylko polecenia interfejsu CLI platformy .NET.
>
> Możesz edytować profil powłoki, aby trwale dodać polecenia. Istnieje wiele różnych powłok dostępnych dla systemu Linux, a każdy z nich ma inny profil. Przykład:
>
> - **Bash Shell**: *~/.bash_profile*, *~/.bashrc.*
> - **Powłoka Korn**: *~/.KSHRC* lub *. profile*
> - **Powłoka Z**: *~/.zshrc* lub *. zprofile*
>
> Edytuj odpowiedni plik źródłowy dla powłoki i Dodaj `:$HOME/dotnet` na końcu istniejącej `PATH` instrukcji. Jeśli `PATH` instrukcja nie jest uwzględniona, Dodaj nowy wiersz za pomocą `export PATH=$PATH:$HOME/dotnet` .
>
> Ponadto Dodaj `export DOTNET_ROOT=$HOME/dotnet` na końcu pliku.

Takie podejście umożliwia zainstalowanie różnych wersji w oddzielnych lokalizacjach i wybór jawny, który ma być używany przez aplikację.

## <a name="install-with-visual-studio-for-mac"></a>Zainstaluj przy użyciu Visual Studio dla komputerów Mac

Visual Studio dla komputerów Mac instaluje zestaw .NET SDK przy wybranym obciążeniu **.NET** . Aby rozpocząć programowanie na platformie .NET w systemie macOS, zobacz [Instalowanie programu Visual Studio 2019 for Mac](/visualstudio/mac/installation).

| Wersja zestawu SDK platformy .NET      | Wersja programu Visual Studio                      |
| --------------------- | ------------------------------------------ |
| 5,0                   | Program Visual Studio 2019 dla komputerów Mac w wersji 8,8 lub nowszej. |
| 3,1                   | Program Visual Studio 2019 dla komputerów Mac w wersji 8,4 lub nowszej. |
| 2.1                   | Program Visual Studio 2019 dla komputerów Mac w wersji 8,0 lub nowszej. |

[![macOS programu Visual Studio 2019 for Mac z funkcją obciążenia .NET](media/install-sdk/mac-install-selection.png)](media/install-sdk/mac-install-selection.png#lightbox)

## <a name="install-alongside-visual-studio-code"></a>Zainstaluj obok Visual Studio Code

Visual Studio Code to zaawansowany i lekki Edytor kodu źródłowego, który jest uruchamiany na pulpicie. Visual Studio Code jest dostępny dla systemów Windows, macOS i Linux.

Mimo że Visual Studio Code nie jest dołączony do zautomatyzowanego Instalatora platformy .NET, takiego jak Visual Studio, Dodawanie obsługi platformy .NET jest proste.

01. [Pobierz i zainstaluj Visual Studio Code](https://code.visualstudio.com/Download).
01. [Pobierz i Zainstaluj zestaw SDK platformy .NET](https://dotnet.microsoft.com/download/dotnet-core).
01. [Zainstaluj rozszerzenie C# z witryny Visual Studio Code Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp).

## <a name="install-with-bash-automation"></a>Instalowanie przy użyciu usługi Bash Automation

[Skrypty programu dotnet-Install](../tools/dotnet-install-script.md) są używane na potrzeby automatyzacji i instalacji niebędących administratorami środowiska uruchomieniowego. Skrypt można pobrać ze [strony odniesienia do skryptu dotnet-Install](../tools/dotnet-install-script.md).

Skrypt domyślnie instaluje najnowszą [LTS](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) wersję, która jest platformą .net Core 3,1. Możesz wybrać określoną wersję, określając `current` przełącznik. Dołącz `runtime` przełącznik, aby zainstalować środowisko uruchomieniowe. W przeciwnym razie skrypt instaluje [zestaw SDK](./windows.md).

```bash
./dotnet-install.sh --channel 5.0 --runtime aspnetcore
```

> [!NOTE]
> Poprzednie polecenie instaluje środowisko uruchomieniowe ASP.NET Core, aby uzyskać maksymalną zgodność. Środowisko uruchomieniowe ASP.NET Core obejmuje również standardowe środowisko uruchomieniowe platformy .NET.

## <a name="docker"></a>Docker

Kontenery zapewniają lekki sposób izolowania aplikacji od pozostałej części systemu hosta. Kontenery na tym samym komputerze udostępniają tylko jądro i używają zasobów przyznanych aplikacji.

Środowisko .NET można uruchomić w kontenerze platformy Docker. Oficjalne obrazy platformy .NET Docker są publikowane w Container Registry firmy Microsoft (MCR) i można je odnajdywać w [repozytorium Microsoft .NET Core Docker Hub](https://hub.docker.com/_/microsoft-dotnet/). Każde repozytorium zawiera obrazy różnych kombinacji platformy .NET (zestawu SDK lub środowiska uruchomieniowego) i systemu operacyjnego, których można użyć.

Firma Microsoft udostępnia obrazy dostosowane do konkretnych scenariuszy. Na przykład [repozytorium ASP.NET Core](https://hub.docker.com/_/microsoft-dotnet-aspnet) zawiera obrazy skompilowane do uruchamiania aplikacji ASP.NET Core w środowisku produkcyjnym.

Aby uzyskać więcej informacji na temat korzystania z platformy .NET Core w kontenerze platformy Docker, zobacz [wprowadzenie do oprogramowania .NET i platformy Docker](../docker/introduction.md) i [przykładów](https://github.com/dotnet/dotnet-docker/blob/master/samples/README.md).

## <a name="next-steps"></a>Następne kroki

- [Jak sprawdzić, czy program .NET Core jest już zainstalowany](how-to-detect-installed-versions.md?pivots=os-macos).
- [Praca z MacOS Catalina notarization](macos-notarization-issues.md).
- [Samouczek: Rozpoczynanie pracy w witrynie macOS](../tutorials/with-visual-studio-mac.md).
- [Samouczek: Tworzenie nowej aplikacji przy użyciu Visual Studio Code](../tutorials/with-visual-studio-code.md).
- [Samouczek: konteneryzowanie aplikacji .NET Core](../docker/build-container.md).

[release-notes-21]: https://github.com/dotnet/core/blob/master/release-notes/2.1/2.1-supported-os.md
[release-notes-31]: https://github.com/dotnet/core/blob/master/release-notes/3.1/3.1-supported-os.md
[release-notes-50]: https://github.com/dotnet/core/blob/master/release-notes/5.0/5.0-supported-os.md
[release-notes-20]: https://github.com/dotnet/core/blob/master/release-notes/2.0/2.0-supported-os.md
[release-notes-22]: https://github.com/dotnet/core/blob/master/release-notes/2.2/2.2-supported-os.md
[release-notes-30]: https://github.com/dotnet/core/blob/master/release-notes/3.0/3.0-supported-os.md
