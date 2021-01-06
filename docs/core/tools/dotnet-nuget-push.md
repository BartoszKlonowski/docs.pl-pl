---
title: polecenia wypychania NuGet dotnet
description: Polecenie polecenia push NuGet narzędzia dotnet wypycha pakiet do serwera i opublikuje go.
author: karann-msft
ms.date: 02/14/2020
ms.openlocfilehash: 50a4a542c2d192bfbd927845489d04fd1b6c6cf3
ms.sourcegitcommit: b7a8b09828bab4e90f66af8d495ecd7024c45042
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/04/2020
ms.locfileid: "87555126"
---
# <a name="dotnet-nuget-push"></a>dotnet nuget push

**Ten artykuł ma zastosowanie do:** ✔️ .NET Core 2. x SDK i nowszych wersji

## <a name="name"></a>Nazwa

`dotnet nuget push`— Wypchnij pakiet do serwera i opublikuje go.

## <a name="synopsis"></a>Streszczenie

```dotnetcli
dotnet nuget push [<ROOT>] [-d|--disable-buffering] [--force-english-output]
    [--interactive] [-k|--api-key <API_KEY>] [-n|--no-symbols true]
    [--no-service-endpoint] [-s|--source <SOURCE>] [--skip-duplicate]
    [-sk|--symbol-api-key <API_KEY>] [-ss|--symbol-source <SOURCE>]
    [-t|--timeout <TIMEOUT>]

dotnet nuget push -h|--help
```

## <a name="description"></a>Opis

`dotnet nuget push`Polecenie wypycha pakiet do serwera i opublikuje go. Polecenie push używa informacji o serwerze i poświadczeniach znajdujących się w pliku konfiguracyjnym NuGet systemu lub w łańcuchu plików konfiguracji. Aby uzyskać więcej informacji na temat plików konfiguracji, zobacz [Konfigurowanie zachowania NuGet](/nuget/consume-packages/configuring-nuget-behavior). Domyślna konfiguracja narzędzia NuGet jest uzyskiwana przez załadowanie pliku *% AppData% \NuGet\NuGet.config* (Windows) lub *$Home/.local/share* (Linux/macOS), a następnie załadowanie dowolnych *nuget.config* lub *.nuget\nuget.config* począwszy od katalogu głównego dysku i kończącego się w bieżącym katalogu.

Polecenie wypycha istniejący pakiet. Nie tworzy pakietu. Aby utworzyć pakiet, użyj [`dotnet pack`](dotnet-pack.md) .

## <a name="arguments"></a>Argumenty

- **`ROOT`**

  Określa ścieżkę pliku do pakietu do wypchnięcia.

## <a name="options"></a>Opcje

- **`-d|--disable-buffering`**

  Wyłącza buforowanie podczas wypychania do serwera HTTP (S) w celu zmniejszenia użycia pamięci.

- **`--force-english-output`**

  Wymusza uruchomienie aplikacji przy użyciu niezmiennej, opartej na języku angielskim kultury.

- **`-h|--help`**

  Drukuje krótką pomoc dla polecenia.

- **`--interactive`**

  Umożliwia zablokowanie polecenia i wymaga ręcznej akcji dla operacji takich jak uwierzytelnianie. Opcja dostępna od wersji .NET Core 2,2 SDK.

- **`-k|--api-key <API_KEY>`**

  Klucz interfejsu API dla serwera programu.

- **`-n|--no-symbols true`**

  Nie Wypychaj symboli (nawet jeśli istnieją).

- **`--no-service-endpoint`**

  Nie dołącza "API/v2/Package" do źródłowego adresu URL. Opcja dostępna od wersji .NET Core 2,1 SDK.

- **`-s|--source <SOURCE>`**

  Określa adres URL serwera. Ta opcja jest wymagana, chyba że `DefaultPushSource` wartość konfiguracji jest ustawiona w pliku konfiguracyjnym NuGet.

- **`--skip-duplicate`**

  Podczas wypychania wielu pakietów do serwera HTTP (S) program traktuje wszystkie 409 odpowiedzi w konflikcie jako ostrzeżenie, aby można było kontynuować wypychanie. Dostępne od wersji .NET Core 3,1 SDK.

- **`-sk|--symbol-api-key <API_KEY>`**

  Klucz interfejsu API dla serwera symboli.

- **`-ss|--symbol-source <SOURCE>`**

  Określa adres URL serwera symboli.

- **`-t|--timeout <TIMEOUT>`**

  Określa limit czasu wypychania do serwera w sekundach. Wartość domyślna to 300 sekund (5 minut). Podanie wartości 0 (zero sekund) powoduje ustawienie wartości domyślnej.

## <a name="examples"></a>Przykłady

- Wypychanie *foo. nupkg* do domyślnego źródła push, określając klucz interfejsu API:

  ```dotnetcli
  dotnet nuget push foo.nupkg -k 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a
  ```

- Wypychanie *foo. nupkg* do oficjalnego serwera NuGet, określając klucz interfejsu API:

  ```dotnetcli
  dotnet nuget push foo.nupkg -k 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s https://api.nuget.org/v3/index.json
  ```
  
  * Wypychanie *foo. nupkg* do niestandardowego źródła wypychania `https://customsource` , określając klucz interfejsu API:

  ```dotnetcli
  dotnet nuget push foo.nupkg -k 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s https://customsource/
  ```

- Wypychanie *foo. nupkg* do domyślnego źródła push:

  ```dotnetcli
  dotnet nuget push foo.nupkg
  ```

- Wypchnij *foo. Symbols. nupkg* do domyślnego źródła symboli:

  ```dotnetcli
  dotnet nuget push foo.symbols.nupkg
  ```

- Wypchnij *foo. nupkg* do domyślnego źródła push, określając 360-sekundowy limit czasu:

  ```dotnetcli
  dotnet nuget push foo.nupkg --timeout 360
  ```

- Wypchnij wszystkie pliki *. nupkg* w bieżącym katalogu do domyślnego źródła push:

  ```dotnetcli
  dotnet nuget push "*.nupkg"
  ```

  > [!NOTE]
  > Jeśli to polecenie nie działa, może to być spowodowane usterką, która istniała we wcześniejszych wersjach zestawu SDK (zestaw SDK programu .NET Core 2,1 i wcześniejsze wersje).
  > Aby rozwiązać ten problem, Uaktualnij wersję zestawu SDK lub zamiast tego Uruchom następujące polecenie:`dotnet nuget push "**/*.nupkg"`
  
  > [!NOTE]
  > Otaczające cudzysłowy są wymagane dla powłok, takich jak bash, które wykonują obsługi symboli wieloznacznych pliku. Aby uzyskać więcej informacji, zobacz [NuGet/Home # 4393](https://github.com/NuGet/Home/issues/4393#issuecomment-667618120).

- Wypchnij wszystkie pliki *NUPKG* , nawet jeśli odpowiedź na 409 jest zwracana przez serwer http (S):

  ```dotnetcli
  dotnet nuget push "*.nupkg" --skip-duplicate
  ```

- Wypchnij wszystkie pliki *. nupkg* w bieżącym katalogu do katalogu lokalnego źródła danych:

  ```dotnetcli
  dotnet nuget push "*.nupkg" -s c:\mydir
  ```

  To polecenie nie przechowuje pakietów w hierarchicznej strukturze folderów, co jest zalecane w celu zoptymalizowania wydajności. Aby uzyskać więcej informacji, zobacz [lokalne źródła danych](/nuget/hosting-packages/local-feeds).  
