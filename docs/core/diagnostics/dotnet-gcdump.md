---
title: Narzędzie diagnostyczne dotnet-gcdump — interfejs wiersza polecenia platformy .NET
description: Dowiedz się, jak zainstalować i użyć narzędzia interfejsu wiersza polecenia dotnet-gcdump w celu zebrania zrzutów pamięci podręcznej na żywo procesów .NET przy użyciu programu .NET EventPipe.
ms.date: 11/17/2020
ms.openlocfilehash: 02e1a7c5d86b582289672a027464aefd67a6f490
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/16/2020
ms.locfileid: "97593373"
---
# <a name="heap-analysis-tool-dotnet-gcdump"></a>Narzędzie do analizy sterty (dotnet-gcdump)

**Ten artykuł ma zastosowanie do:** ✔️ .net Core 3,1 SDK i nowszych wersjach

## <a name="install"></a>Instalowanie

Istnieją dwa sposoby na pobranie i zainstalowanie `dotnet-gcdump` :

- **Narzędzie globalne dotnet:**

  Aby zainstalować najnowszą wersję `dotnet-gcdump` [pakietu NuGet](https://www.nuget.org/packages/dotnet-gcdump), użyj polecenia [Narzędzia dotnet Install](../tools/dotnet-tool-install.md) :

  ```dotnetcli
  dotnet tool install --global dotnet-gcdump
  ```

- **Pobieranie bezpośrednie:**

  Pobierz plik wykonywalny narzędzia, który jest zgodny z platformą:

  | System operacyjny  | Platforma |
  | --- | -------- |
  | Windows | [x86](https://aka.ms/dotnet-gcdump/win-x86) \| [x64](https://aka.ms/dotnet-gcdump/win-x64) \| [ARM](https://aka.ms/dotnet-gcdump/win-arm) \| [ARM — x64](https://aka.ms/dotnet-gcdump/win-arm64) |
  | macOS   | [x64](https://aka.ms/dotnet-gcdump/osx-x64) |
  | Linux   | [x64](https://aka.ms/dotnet-gcdump/linux-x64) \| [ARM](https://aka.ms/dotnet-gcdump/linux-arm) \| [arm64](https://aka.ms/dotnet-gcdump/linux-arm64) \| [MUSL — x64](https://aka.ms/dotnet-gcdump/linux-musl-x64) \| [MUSL — arm64](https://aka.ms/dotnet-gcdump/linux-musl-arm64) |

## <a name="synopsis"></a>Streszczenie

```console
dotnet-gcdump [-h|--help] [--version] <command>
```

## <a name="description"></a>Opis

`dotnet-gcdump`Narzędzie globalne zbiera zrzuty procesów .NET na żywo (Moduł wyrzucania elementów bezużytecznych) za pomocą [EventPipe](./eventpipe.md). Zrzuty GC są tworzone przez wyzwolenie GC w procesie docelowym, włączenie zdarzeń specjalnych i ponowne wygenerowanie grafu obiektów głównych obiektu ze strumienia zdarzeń. Ten proces umożliwia zbieranie zrzutów GC, gdy proces jest uruchomiony i z minimalnymi kosztami. Te zrzuty są przydatne w kilku scenariuszach:

- Porównanie liczby obiektów w stercie w kilku punktach w czasie.
- Analizowanie katalogów głównych obiektów (odpowiedzi na pytania, takie jak nadal ma odwołanie do tego typu?).
- Zbieranie ogólnych statystyk o liczbie obiektów na stercie.

### <a name="view-the-gc-dump-captured-from-dotnet-gcdump"></a>Wyświetlanie zrzutu pamięci podręcznej przechwycone z programu dotnet-gcdump

W systemie Windows `.gcdump` pliki można wyświetlać w [Narzędzia PerfView](https://github.com/microsoft/perfview) na potrzeby analizy lub w programie Visual Studio. Obecnie nie ma możliwości otwierania `.gcdump` na platformach innych niż Windows.

Można zbierać wiele `.gcdump` i otwierać je jednocześnie w programie Visual Studio w celu uzyskania porównania.

## <a name="options"></a>Opcje

- **`--version`**

  Wyświetla wersję `dotnet-gcdump` Narzędzia.

- **`-h|--help`**

  Wyświetla pomoc w wierszu polecenia.

## `dotnet-gcdump collect`

Zbiera zrzut GC z aktualnie uruchomionego procesu.

> [!WARNING]
> W celu przeanalizowania sterty GC to polecenie wyzwala wyrzucanie elementów bezużytecznych generacji 2 (pełne), które mogą wstrzymywać środowisko uruchomieniowe przez długi czas, szczególnie gdy sterta GC jest duża. Nie używaj tego polecenia w środowiskach z uwzględnieniem wydajności, gdy sterta GC jest duża.

### <a name="synopsis"></a>Streszczenie

```console
dotnet-gcdump collect [-h|--help] [-p|--process-id <pid>] [-o|--output <gcdump-file-path>] [-v|--verbose] [-t|--timeout <timeout>] [-n|--name <name>]
```

### <a name="options"></a>Opcje

- **`-h|--help`**

  Wyświetla pomoc w wierszu polecenia.

- **`-p|--process-id <pid>`**

  Identyfikator procesu, z którego ma zostać zebrany zrzut GC.

- **`-o|--output <gcdump-file-path>`**

  Ścieżka, w której powinny być zapisywane zebrane zrzuty GC. Wartość domyślna to *. \\ RRRRMMDD \_ HHMMSS \_ \<pid> . gcdump*.

- **`-v|--verbose`**

  Wyprowadza dziennik podczas zbierania zrzutu GC.

- **`-t|--timeout <timeout>`**

  Zastanów się nad zbieraniem zrzutu pamięci podręcznej, jeśli trwa dłużej niż wynosi to wiele sekund. Wartość domyślna to 30.

- **`-n|--name <name>`**

  Nazwa procesu, z którego ma zostać zebrany zrzut GC.

## `dotnet-gcdump ps`

Wyświetla listę procesów dotnet, dla których można zbierać zrzuty GC.

### <a name="synopsis"></a>Streszczenie

```console
dotnet-gcdump ps
```

## `dotnet-gcdump report <gcdump_filename>`

Wygeneruj Raport z wcześniej wygenerowanego zrzutu GC lub z uruchomionego procesu, a następnie wpisz polecenie `stdout` .

### <a name="synopsis"></a>Streszczenie

```console
dotnet-gcdump report [-h|--help] [-p|--process-id <pid>] [-t|--report-type <HeapStat>]
```

### <a name="options"></a>Opcje

- **`-h|--help`**

  Wyświetla pomoc w wierszu polecenia.

- **`-p|--process-id <pid>`**

  Identyfikator procesu, z którego ma zostać zebrany zrzut GC.

- **`-t|--report-type <HeapStat>`**

  Typ raportu do wygenerowania. Dostępne opcje: heapstat (domyślnie).

## <a name="troubleshoot"></a>Rozwiązywanie problemów

- Brak informacji o typie w gcdump.

   Przed platformą .NET Core 3,1 wystąpił problem polegający na tym, że pamięć podręczna typu nie została wyczyszczona między gcdumps, gdy zostały wywołane z EventPipe. Spowodowało to zdarzenia, które trzeba wykonać, aby określić informacje o typie, które nie są wysyłane dla drugiego i kolejnego gcdumps. Ten problem został rozwiązany w programie .NET Core 3,1-preview2.

- COM i typy statyczne nie znajdują się w zrzucie odzyskiwania pamięci.

   Przed uruchomieniem programu .NET Core 3,1-preview2 wystąpił problem polegający na tym, że typy statyczne i COM nie zostały wysłane, gdy zrzut GC został wywołany za pośrednictwem EventPipe. Ten problem został rozwiązany w programie .NET Core 3,1-preview2.
