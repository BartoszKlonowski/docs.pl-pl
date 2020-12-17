---
title: Narzędzia platformy .NET
description: Jak instalować, używać, aktualizować i usuwać narzędzia platformy .NET. Obejmuje narzędzia globalne, narzędzia ścieżki narzędzi i narzędzia lokalne.
author: KathleenDollard
ms.topic: how-to
ms.date: 02/12/2020
ms.openlocfilehash: 8839fd4fba72c9f973d906eabb72919306a847dd
ms.sourcegitcommit: 635a0ff775d2447a81ef7233a599b8f88b162e5d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/17/2020
ms.locfileid: "97633887"
---
# <a name="how-to-manage-net-tools"></a>Jak zarządzać narzędziami .NET

**Ten artykuł ma zastosowanie do:** ✔️ .net Core 2,1 SDK i nowszych wersjach

Narzędzie .NET jest specjalnym pakietem NuGet, który zawiera aplikację konsolową. Narzędzie można zainstalować na maszynie w następujący sposób:

* Jako narzędzie globalne.

  Pliki binarne narzędzia są instalowane w katalogu domyślnym, który jest dodawany do zmiennej środowiskowej PATH. Można wywołać narzędzie z dowolnego katalogu na maszynie bez określania jego lokalizacji. Jedna wersja narzędzia jest używana dla wszystkich katalogów na komputerze.

* Jako narzędzie globalne w niestandardowej lokalizacji (nazywanej również narzędziem ścieżki narzędzia).

  Pliki binarne narzędzia są instalowane w określonej lokalizacji. Możesz wywołać narzędzie z katalogu instalacyjnego lub podając katalog z nazwą polecenia lub dodając katalog do zmiennej środowiskowej PATH. Jedna wersja narzędzia jest używana dla wszystkich katalogów na komputerze.

* Jako narzędzie lokalne (dotyczy zestaw .NET Core SDK 3,0 i nowszych).

  Pliki binarne narzędzia są instalowane w katalogu domyślnym. Należy wywołać narzędzie z katalogu instalacyjnego lub któregokolwiek z jego podkatalogów. Różne katalogi mogą korzystać z różnych wersji tego samego narzędzia.
  
  Interfejs wiersza polecenia platformy .NET używa plików manifestu do śledzenia, które narzędzia są instalowane jako lokalne w katalogu. Gdy plik manifestu jest zapisywany w katalogu głównym repozytorium kodu źródłowego, współautor może sklonować repozytorium i wywoływać pojedyncze polecenie interfejsu wiersza polecenia platformy .NET, które instaluje wszystkie narzędzia wymienione w plikach manifestu.

> [!IMPORTANT]
> Narzędzia platformy .NET działają w trybie pełnego zaufania. Nie instaluj narzędzia platformy .NET, chyba że ufasz autorowi.

## <a name="find-a-tool"></a>Znajdź narzędzie

Oto kilka sposobów znajdowania narzędzi:

* Użyj polecenia [Search narzędzia dotnet](dotnet-tool-search.md) , aby znaleźć narzędzie, które jest publikowane w usłudze NuGet.org.
* Przeszukaj witrynę sieci Web [NuGet](https://www.nuget.org) przy użyciu filtru typu pakietu "narzędzie .NET". Aby uzyskać więcej informacji, zobacz [Znajdowanie i wybieranie pakietów](/nuget/consume-packages/finding-and-choosing-packages).
* Zobacz kod źródłowy narzędzi utworzonych przez zespół ASP.NET Core w [katalogu Tools w repozytorium GitHub/aspnetcore](https://github.com/dotnet/aspnetcore/tree/master/src/Tools).
* Informacje o narzędziach diagnostycznych w [narzędziach diagnostycznych platformy .NET](../diagnostics/index.md#net-core-diagnostic-global-tools).

## <a name="check-the-author-and-statistics"></a>Sprawdź autora i statystyki

Ponieważ narzędzia platformy .NET działają w trybie pełnego zaufania, a narzędzia globalne są dodawane do zmiennej środowiskowej PATH, mogą być bardzo wydajne. Nie pobieraj narzędzi z osób, które nie są zaufane.

Jeśli narzędzie jest hostowane w usłudze NuGet, można sprawdzić autora i statystyk, wyszukując narzędzie.

## <a name="install-a-global-tool"></a>Instalowanie narzędzia globalnego

Aby zainstalować narzędzie jako narzędzie globalne, użyj `-g` lub `--global` opcji [instalacji narzędzia dotnet](dotnet-tool-install.md), jak pokazano w następującym przykładzie:

```dotnetcli
dotnet tool install -g dotnetsay
```

Dane wyjściowe przedstawiają polecenie używane do wywołania narzędzia i zainstalowanej wersji, podobnie jak w poniższym przykładzie:

```output
You can invoke the tool using the following command: dotnetsay
Tool 'dotnetsay' (version '2.1.4') was successfully installed.
```

Domyślna lokalizacja plików binarnych narzędzia zależy od systemu operacyjnego:

| System operacyjny          | Ścieżka                          |
|-------------|-------------------------------|
| Linux/macOS | `$HOME/.dotnet/tools`         |
| Windows     | `%USERPROFILE%\.dotnet\tools` |

Ta lokalizacja jest dodawana do ścieżki użytkownika podczas pierwszego uruchomienia zestawu SDK, dzięki czemu narzędzia globalne mogą być wywoływane z dowolnego katalogu bez określania lokalizacji narzędzia.

Dostęp do narzędzi to specyficzne dla użytkownika, a nie globalne maszyny. Narzędzie globalne jest dostępne tylko dla użytkownika, który zainstalował narzędzie.

### <a name="install-a-global-tool-in-a-custom-location"></a>Instalowanie narzędzia globalnego w niestandardowej lokalizacji

Aby zainstalować narzędzie jako narzędzie globalne w niestandardowej lokalizacji, użyj `--tool-path` opcji [Instalacja narzędzia dotnet](dotnet-tool-install.md), jak pokazano w poniższych przykładach.

W systemie Windows:

```dotnetcli
dotnet tool install dotnetsay --tool-path c:\dotnet-tools
```

W systemie Linux lub macOS:

```dotnetcli
dotnet tool install dotnetsay --tool-path ~/bin
```

Zestaw SDK platformy .NET nie dodaje automatycznie tej lokalizacji do zmiennej środowiskowej PATH. Aby [wywołać narzędzie ścieżki narzędzi](#invoke-a-tool-path-tool), należy upewnić się, że polecenie jest dostępne za pomocą jednej z następujących metod:

* Dodaj katalog instalacyjny do zmiennej środowiskowej PATH.
* Określ pełną ścieżkę do narzędzia podczas jego wywoływania.
* Wywołaj narzędzie z katalogu instalacyjnego.

## <a name="install-a-local-tool"></a>Instalowanie narzędzia lokalnego

**Dotyczy zestawu .NET Core 3,0 SDK i nowszych wersji.**

Aby zainstalować narzędzie tylko do dostępu lokalnego (dla bieżącego katalogu i podkatalogów), należy dodać je do pliku manifestu narzędzia. Aby utworzyć plik manifestu narzędzia, uruchom `dotnet new tool-manifest` polecenie:

```dotnetcli
dotnet new tool-manifest
```

To polecenie tworzy plik manifestu o nazwie *dotnet-tools.jsw* katalogu *. config* . Aby dodać narzędzie lokalne do pliku manifestu, należy użyć polecenia [Zainstaluj narzędzie dotnet](dotnet-tool-install.md) i **pominąć** `--global` `--tool-path` Opcje i, jak pokazano w następującym przykładzie:

```dotnetcli
dotnet tool install dotnetsay
```

Dane wyjściowe polecenia pokazują plik manifestu, w którym znajduje się nowo zainstalowane narzędzie, podobnie jak w poniższym przykładzie:

```console
You can invoke the tool from this directory using the following command:
dotnet tool run dotnetsay
Tool 'dotnetsay' (version '2.1.4') was successfully installed.
Entry is added to the manifest file /home/name/botsay/.config/dotnet-tools.json.
```

W poniższym przykładzie przedstawiono plik manifestu z zainstalowanymi dwoma lokalnymi narzędziami:

```json
{
  "version": 1,
  "isRoot": true,
  "tools": {
    "botsay": {
      "version": "1.0.0",
      "commands": [
        "botsay"
      ]
    },
    "dotnetsay": {
      "version": "2.1.3",
      "commands": [
        "dotnetsay"
      ]
    }
  }
}
```

Zazwyczaj można dodać lokalne narzędzie do katalogu głównego repozytorium. Po zaewidencjonowaniu pliku manifestu do repozytorium, deweloperzy, którzy ewidencjonują kod z repozytorium, pobierają najnowszy plik manifestu. Aby zainstalować wszystkie narzędzia wymienione w pliku manifestu, uruchom `dotnet tool restore` polecenie:

```dotnetcli
dotnet tool restore
```

Dane wyjściowe wskazują, które narzędzia zostały przywrócone:

```console
Tool 'botsay' (version '1.0.0') was restored. Available commands: botsay
Tool 'dotnetsay' (version '2.1.3') was restored. Available commands: dotnetsay
Restore was successful.
```

## <a name="install-a-specific-tool-version"></a>Zainstaluj określoną wersję narzędzia

Aby zainstalować wersję wstępną lub określoną wersję narzędzia, należy określić numer wersji przy użyciu `--version` opcji, jak pokazano w następującym przykładzie:

```dotnetcli
dotnet tool install dotnetsay --version 2.1.3
```

## <a name="use-a-tool"></a>Korzystanie z narzędzia

Polecenie używane do wywoływania narzędzia może różnić się od nazwy instalowanego pakietu. Aby wyświetlić wszystkie narzędzia aktualnie zainstalowane na komputerze dla bieżącego użytkownika, użyj polecenia z [listy narzędzi dotnet](dotnet-tool-list.md) :

```dotnetcli
dotnet tool list
```

Dane wyjściowe wyświetlają wersję i polecenie każdego narzędzia, podobnie jak w poniższym przykładzie:

```console
Package Id      Version      Commands       Manifest
-------------------------------------------------------------------------------------------
botsay          1.0.0        botsay         /home/name/repository/.config/dotnet-tools.json
dotnetsay       2.1.3        dotnetsay      /home/name/repository/.config/dotnet-tools.json
```

Jak pokazano w tym przykładzie, lista zawiera narzędzia lokalne. Aby wyświetlić narzędzia globalne, użyj `--global` opcji i, aby zobaczyć narzędzia ścieżki narzędzi, użyj `--tool-path` opcji.

### <a name="invoke-a-global-tool"></a>Wywołaj narzędzie globalne

W przypadku narzędzi globalnych Użyj narzędzia. Na przykład jeśli polecenie jest `dotnetsay` lub, to jest `dotnet-doc` używane do wywołania polecenia:

```console
dotnetsay
dotnet-doc
```

Jeśli polecenie zaczyna się od prefiksu `dotnet-` , alternatywnym sposobem wywołania narzędzia jest użycie `dotnet` polecenia i pominięcie prefiksu polecenia narzędzia. Na przykład, jeśli polecenie ma wartość `dotnet-doc` , następujące polecenie wywołuje narzędzie:

```dotnetcli
dotnet doc
```

Jednak w poniższym scenariuszu nie można użyć `dotnet` polecenia do wywołania narzędzia globalnego:

* Narzędzie globalne i narzędzie lokalne mają to samo polecenie poprzedzone przez program `dotnet-` .
* Chcesz wywołać narzędzie globalne z katalogu, który znajduje się w zakresie dla narzędzia lokalnego.

W tym scenariuszu `dotnet doc` i `dotnet dotnet-doc` Wywołaj narzędzie lokalne. Aby wywołać narzędzie globalne, użyj polecenia przez samego siebie:

```dotnetcli
dotnet-doc
```

### <a name="invoke-a-tool-path-tool"></a>Wywołaj narzędzie ścieżki narzędziowej

Aby wywołać narzędzie globalne, które jest instalowane przy użyciu `tool-path` opcji, upewnij się, że polecenie jest dostępne, zgodnie z opisem [we wcześniejszej części tego artykułu](#install-a-global-tool-in-a-custom-location).

### <a name="invoke-a-local-tool"></a>Wywoływanie narzędzia lokalnego

Aby wywołać narzędzie lokalne, należy użyć `dotnet` polecenia z katalogu instalacyjnego. Możesz użyć długiej formy ( `dotnet tool run <COMMAND_NAME>` ) lub krótkiej formy ( `dotnet <COMMAND_NAME>` ), jak pokazano w następujących przykładach:

```dotnetcli
dotnet tool run dotnetsay
dotnet dotnetsay
```

Jeśli polecenie jest poprzedzone przez `dotnet-` , można dołączyć lub pominąć prefiks po wywołaniu narzędzia. Na przykład, jeśli polecenie jest `dotnet-doc` , każdy z poniższych przykładów wywoła narzędzie lokalne:

```dotnetcli
dotnet tool run dotnet-doc
dotnet dotnet-doc
dotnet doc
```

## <a name="update-a-tool"></a>Aktualizowanie narzędzia

Aktualizacja narzędzia polega na odinstalowaniu i ponownym zainstalowaniu go z najnowszą stabilną wersją. Aby zaktualizować narzędzie, należy użyć polecenia " [Update" narzędzia dotnet](dotnet-tool-update.md) z tą samą opcją, która została użyta do zainstalowania narzędzia:

```dotnetcli
dotnet tool update --global <packagename>
dotnet tool update --tool-path <packagename>
dotnet tool update <packagename>
```

W przypadku narzędzia lokalnego zestaw SDK znajduje pierwszy plik manifestu zawierający identyfikator pakietu, przeszukując bieżący katalog i katalogi nadrzędne. Jeśli w pliku manifestu nie ma takiego identyfikatora pakietu, zestaw SDK dodaje nowy wpis do najbliższego pliku manifestu.

## <a name="uninstall-a-tool"></a>Odinstalowywanie narzędzia

Usuń narzędzie za pomocą [Narzędzia dotnet Command Uninstall](dotnet-tool-uninstall.md) polecenie z tą samą opcją, która została użyta do zainstalowania narzędzia:

```dotnetcli
dotnet tool uninstall --global <packagename>
dotnet tool uninstall --tool-path <packagename>
dotnet tool uninstall <packagename>
```

W przypadku narzędzia lokalnego zestaw SDK znajduje pierwszy plik manifestu zawierający identyfikator pakietu, przeszukując bieżący katalog i katalogi nadrzędne.

## <a name="get-help-and-troubleshoot"></a>Uzyskiwanie pomocy i rozwiązywanie problemów

Aby uzyskać listę dostępnych `dotnet tool` poleceń, wprowadź następujące polecenie:

```dotnetcli
dotnet tool --help
```

Aby uzyskać instrukcje dotyczące użycia narzędzia, wprowadź jedno z następujących poleceń lub zapoznaj się z witryną sieci Web narzędzia:

```dotnetcli
<command> --help
dotnet <command> --help
```

Jeśli instalacja lub uruchomienie narzędzia nie powiedzie się, zobacz [Rozwiązywanie problemów z użyciem narzędzia platformy .NET](troubleshoot-usage-issues.md).

## <a name="see-also"></a>Zobacz także

- [Samouczek: Tworzenie narzędzia platformy .NET przy użyciu interfejsu wiersza polecenia platformy .NET](global-tools-how-to-create.md)
- [Samouczek: Instalowanie i używanie narzędzia globalnego platformy .NET przy użyciu interfejsu wiersza polecenia platformy .NET](global-tools-how-to-use.md)
- [Samouczek: Instalowanie i używanie lokalnego narzędzia .NET przy użyciu interfejsu wiersza polecenia platformy .NET](local-tools-how-to-use.md)
