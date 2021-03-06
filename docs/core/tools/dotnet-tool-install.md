---
title: polecenie instalacji narzędzia dotnet
description: Polecenie instalacji narzędzia dotnet służy do instalowania określonego narzędzia platformy .NET na komputerze.
ms.date: 02/14/2020
ms.openlocfilehash: 1dd870a8f91e557a2f59919682616aa8817fc070
ms.sourcegitcommit: b201d177e01480a139622f3bf8facd367657a472
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/15/2020
ms.locfileid: "94634327"
---
# <a name="dotnet-tool-install"></a>dotnet tool install

**Ten artykuł ma zastosowanie do:** ✔️ .net Core 2,1 SDK i nowszych wersjach

## <a name="name"></a>Nazwa

`dotnet tool install` -Instaluje określone [Narzędzie .NET](global-tools.md) na komputerze.

## <a name="synopsis"></a>Streszczenie

```dotnetcli
dotnet tool install <PACKAGE_NAME> -g|--global
    [--add-source <SOURCE>] [--configfile <FILE>]
    [--framework <FRAMEWORK>] [-v|--verbosity <LEVEL>]
    [--version <VERSION_NUMBER>]

dotnet tool install <PACKAGE_NAME> --tool-path <PATH>
    [--add-source <SOURCE>] [--configfile <FILE>]
    [--framework <FRAMEWORK>] [-v|--verbosity <LEVEL>]
    [--version <VERSION_NUMBER>]

dotnet tool install <PACKAGE_NAME>
    [--add-source <SOURCE>] [--configfile <FILE>]
    [--framework <FRAMEWORK>] [-v|--verbosity <LEVEL>]
    [--version <VERSION_NUMBER>]

dotnet tool install -h|--help
```

## <a name="description"></a>Opis

`dotnet tool install`Polecenie zapewnia sposób instalacji narzędzi .NET na komputerze. Aby użyć polecenia, należy określić jedną z następujących opcji instalacji:

* Aby zainstalować narzędzie globalne w lokalizacji domyślnej, użyj `--global` opcji.
* Aby zainstalować narzędzie globalne w niestandardowej lokalizacji, użyj `--tool-path` opcji.
* Aby zainstalować narzędzie lokalne, należy pominąć `--global` Opcje i `--tool-path` .

**Narzędzia lokalne są dostępne począwszy od zestaw .NET Core SDK 3,0.**

Narzędzia globalne są instalowane domyślnie w następujących katalogach po określeniu `-g` `--global` opcji lub:

| System operacyjny          | Ścieżka                          |
|-------------|-------------------------------|
| Linux/macOS | `$HOME/.dotnet/tools`         |
| Windows     | `%USERPROFILE%\.dotnet\tools` |

Narzędzia lokalne są dodawane do *dotnet-tools.jsw* pliku w katalogu *. config* w bieżącym katalogu. Jeśli plik manifestu jeszcze nie istnieje, utwórz go, uruchamiając następujące polecenie:

```dotnetcli
dotnet new tool-manifest
```

Aby uzyskać więcej informacji, zobacz [Instalowanie narzędzia lokalnego](global-tools.md#install-a-local-tool).

## <a name="arguments"></a>Argumenty

- **`PACKAGE_NAME`**

  Nazwa/identyfikator pakietu NuGet zawierającego narzędzie .NET do zainstalowania.

## <a name="options"></a>Opcje

- **`add-source <SOURCE>`**

  Dodaje dodatkowe źródło pakietów NuGet do użycia podczas instalacji.

- **`configfile <FILE>`**

  Plik konfiguracji NuGet ( *nuget.config* ) do użycia.

- **`framework <FRAMEWORK>`**

  Określa [platformę docelową](../../standard/frameworks.md) do zainstalowania narzędzia dla programu. Domyślnie zestaw .NET SDK próbuje wybrać najbardziej odpowiednią platformę docelową.

- **`-g|--global`**

  Określa, że instalacja jest szeroka. Nie można łączyć z `--tool-path` opcją. Pomijanie obu `--global` i `--tool-path` określa instalację narzędzia lokalnego.

- **`-h|--help`**

  Drukuje krótką pomoc dla polecenia.

- **`tool-path <PATH>`**

  Określa lokalizację, w której ma zostać zainstalowane narzędzie globalne. ŚCIEŻKA może być bezwzględna lub względna. Jeśli ścieżka nie istnieje, polecenie próbuje ją utworzyć. Pomijanie obu `--global` i `--tool-path` określa instalację narzędzia lokalnego.

- **`-v|--verbosity <LEVEL>`**

  Ustawia poziom szczegółowości polecenia. Dozwolone wartości to `q[uiet]` , `m[inimal]` , `n[ormal]` , `d[etailed]` i `diag[nostic]` .

- **`--version <VERSION_NUMBER>`**

  Wersja narzędzia do zainstalowania. Domyślnie jest zainstalowana najnowsza stabilna wersja pakietu. Użyj tej opcji, aby zainstalować Podgląd lub starsze wersje narzędzia.

## <a name="examples"></a>Przykłady

- **`dotnet tool install -g dotnetsay`**

  Instaluje [dotnetsay](https://www.nuget.org/packages/dotnetsay/) jako narzędzie globalne w domyślnej lokalizacji.

- **`dotnet tool install dotnetsay --tool-path c:\global-tools`**

  Instaluje [dotnetsay](https://www.nuget.org/packages/dotnetsay/) jako narzędzie globalne w określonym katalogu systemu Windows.

- **`dotnet tool install dotnetsay --tool-path ~/bin`**

  Instaluje [dotnetsay](https://www.nuget.org/packages/dotnetsay/) jako narzędzie globalne w określonym katalogu systemu Linux/macOS.

- **`dotnet tool install -g dotnetsay --version 2.0.0`**

  Instaluje wersję 2.0.0 programu [dotnetsay](https://www.nuget.org/packages/dotnetsay/) jako narzędzie globalne.

- **`dotnet tool install dotnetsay`**

  Instaluje [dotnetsay](https://www.nuget.org/packages/dotnetsay/) jako narzędzie lokalne dla bieżącego katalogu.

## <a name="see-also"></a>Zobacz też

- [Narzędzia .NET](global-tools.md)
- [Samouczek: Instalowanie i używanie narzędzia globalnego platformy .NET przy użyciu interfejsu wiersza polecenia platformy .NET](global-tools-how-to-use.md)
- [Samouczek: Instalowanie i używanie lokalnego narzędzia .NET przy użyciu interfejsu wiersza polecenia platformy .NET](local-tools-how-to-use.md)
