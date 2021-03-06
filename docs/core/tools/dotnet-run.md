---
title: polecenie dotnet Run
description: Polecenie dotnet Run udostępnia wygodną opcję uruchamiania aplikacji z kodu źródłowego.
ms.date: 02/19/2020
ms.openlocfilehash: c80f290c75e3bac65ae73fe8edada53db4ce86f8
ms.sourcegitcommit: b201d177e01480a139622f3bf8facd367657a472
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/15/2020
ms.locfileid: "94634419"
---
# <a name="dotnet-run"></a>dotnet run

**Ten artykuł ma zastosowanie do:** ✔️ .NET Core 2. x SDK i nowszych wersji

## <a name="name"></a>Nazwa

`dotnet run` -Uruchamia kod źródłowy bez żadnych jawnych poleceń kompilacji lub uruchamiania.

## <a name="synopsis"></a>Streszczenie

```dotnetcli
dotnet run [-c|--configuration <CONFIGURATION>] [-f|--framework <FRAMEWORK>]
    [--force] [--interactive] [--launch-profile <NAME>] [--no-build]
    [--no-dependencies] [--no-launch-profile] [--no-restore]
    [-p|--project <PATH>] [-r|--runtime <RUNTIME_IDENTIFIER>]
    [-v|--verbosity <LEVEL>] [[--] [application arguments]]

dotnet run -h|--help
```

## <a name="description"></a>Opis

`dotnet run`Polecenie udostępnia wygodną opcję uruchamiania aplikacji z kodu źródłowego za pomocą jednego polecenia. Jest to przydatne w przypadku szybkiego iteracyjnego programowania z poziomu wiersza polecenia. Polecenie jest zależne od [`dotnet build`](dotnet-build.md) polecenia do kompilowania kodu. Wszelkie wymagania dotyczące kompilacji, takie jak najpierw należy przywrócić projekt, również zastosować do `dotnet run` .

Pliki wyjściowe są zapisywane w lokalizacji domyślnej, czyli `bin/<configuration>/<target>` . Na przykład jeśli masz `netcoreapp2.1` aplikację i uruchomisz `dotnet run` , dane wyjściowe są umieszczane w `bin/Debug/netcoreapp2.1` . Pliki są zastępowane w razie konieczności. Pliki tymczasowe są umieszczane w `obj` katalogu.

Jeśli projekt określa wiele struktur, wykonanie `dotnet run` powoduje błąd, chyba że `-f|--framework <FRAMEWORK>` opcja jest używana do określenia struktury.

`dotnet run`Polecenie jest używane w kontekście projektów, nieskompilowanych zestawów. Jeśli próbujesz uruchomić bibliotekę DLL aplikacji zależnej od platformy, musisz użyć [dotnet](dotnet.md) bez polecenia. Na przykład aby uruchomić `myapp.dll` polecenie, użyj:

```dotnetcli
dotnet myapp.dll
```

Aby uzyskać więcej informacji na temat `dotnet` sterownika, zobacz temat [narzędzia wiersza polecenia (CLI) platformy .NET](index.md) .

Aby uruchomić aplikację, `dotnet run` polecenie rozwiązuje zależności aplikacji, które są poza udostępnionym środowiskiem uruchomieniowym z pamięci podręcznej NuGet. Ponieważ używa on buforowanych zależności, nie jest zalecane do `dotnet run` uruchamiania aplikacji w środowisku produkcyjnym. Zamiast tego [Utwórz wdrożenie](../deploying/index.md) przy użyciu [`dotnet publish`](dotnet-publish.md) polecenia i Wdróż opublikowane dane wyjściowe.

### <a name="implicit-restore"></a>Przywracanie niejawne

[!INCLUDE[dotnet restore note + options](~/includes/dotnet-restore-note-options.md)]

## <a name="options"></a>Opcje

- **`--`**

  Ogranicza argumenty `dotnet run` od argumentów dla uruchamianej aplikacji. Wszystkie argumenty po tym ograniczniku są przesyłane do uruchomienia aplikacji.

- **`-c|--configuration <CONFIGURATION>`**

  Definiuje konfigurację kompilacji. Wartością domyślną dla większości projektów jest `Debug` , ale można zastąpić ustawienia konfiguracji kompilacji w projekcie.

- **`-f|--framework <FRAMEWORK>`**

  Kompiluje i uruchamia aplikację przy użyciu określonej [struktury](../../standard/frameworks.md). Struktura musi być określona w pliku projektu.

- **`--force`**

  Wymusza rozpoznanie wszystkich zależności, nawet jeśli ostatnie przywracanie zakończyło się pomyślnie. Określenie tej flagi jest takie samo jak usuwanie *project.assets.jsw* pliku.

- **`-h|--help`**

  Drukuje krótką pomoc dla polecenia.

- **`--interactive`**

  Zezwala na zatrzymanie polecenia i oczekiwanie na dane wejściowe użytkownika lub akcję (na przykład w celu ukończenia uwierzytelniania). Dostępne od wersji .NET Core 3,0 SDK.

- **`--launch-profile <NAME>`**

  Nazwa profilu uruchamiania (jeśli istnieje) do użycia podczas uruchamiania aplikacji. Profile uruchamiania są zdefiniowane w *launchSettings.js* pliku i są zwykle nazywane `Development` , `Staging` i `Production` . Aby uzyskać więcej informacji, zobacz [Praca z wieloma środowiskami](/aspnet/core/fundamentals/environments).

- **`--no-build`**

  Nie kompiluje projektu przed uruchomieniem. Również niejawne ustawia `--no-restore` flagę.

- **`--no-dependencies`**

  W przypadku przywracania projektu z odwołaniami do projektu (P2P) program przywraca projekt główny, a nie odwołania.

- **`--no-launch-profile`**

  Nie próbuje użyć *launchSettings.jsw* celu skonfigurowania aplikacji.

- **`--no-restore`**

  Nie wykonuje przywracania niejawnego podczas wykonywania polecenia.

- **`-p|--project <PATH>`**

  Określa ścieżkę do pliku projektu do uruchomienia (nazwa folderu lub pełna ścieżka). Jeśli nie zostanie określony, domyślnie jest bieżącym katalogiem.

- **`-r|--runtime <RUNTIME_IDENTIFIER>`**

  Określa docelowy środowisko uruchomieniowe, dla którego mają zostać przywrócone pakiety. Aby uzyskać listę identyfikatorów środowiska uruchomieniowego (RID), zobacz [wykaz identyfikatorów RID](../rid-catalog.md). `-r` Krótka opcja dostępna od wersji .NET Core 3,0 SDK.

- **`-v|--verbosity <LEVEL>`**

  Ustawia poziom szczegółowości polecenia. Dozwolone wartości to `q[uiet]` , `m[inimal]` , `n[ormal]` , `d[etailed]` i `diag[nostic]` . Wartość domyślna to `m`. Dostępne od wersji .NET Core 2,1 SDK.

## <a name="examples"></a>Przykłady

- Uruchom projekt w bieżącym katalogu:

  ```dotnetcli
  dotnet run
  ```

- Uruchom określony projekt:

  ```dotnetcli
  dotnet run --project ./projects/proj1/proj1.csproj
  ```

- Uruchom projekt w bieżącym katalogu ( `--help` argument w tym przykładzie jest przesyłany do aplikacji, ponieważ `--` jest używana opcja pusta):

  ```dotnetcli
  dotnet run --configuration Release -- --help
  ```

- Przywróć zależności i narzędzia dla projektu w bieżącym katalogu, wyświetlając tylko minimalne dane wyjściowe, a następnie Uruchom projekt:

  ```dotnetcli
  dotnet run --verbosity m
  ```
