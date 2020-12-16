---
title: dotnet-Trace — narzędzie diagnostyczne — interfejs wiersza polecenia platformy .NET
description: Dowiedz się, jak zainstalować i użyć narzędzia interfejsu wiersza polecenia śledzenia dotnet, aby zebrać ślady środowiska .NET działającego procesu bez natywnego profilera przy użyciu programu .NET EventPipe.
ms.date: 11/17/2020
ms.openlocfilehash: a2925ac0a0815fe48ca9b36b643ff896aa3c0ff6
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/16/2020
ms.locfileid: "97593210"
---
# <a name="dotnet-trace-performance-analysis-utility"></a>Narzędzie do analizy wydajności śledzenia dotnet

**Ten artykuł ma zastosowanie do:** ✔️ .net Core 3,0 SDK i nowszych wersjach

## <a name="install"></a>Instalowanie

Istnieją dwa sposoby na pobranie i zainstalowanie `dotnet-trace` :

- **Narzędzie globalne dotnet:**

  Aby zainstalować najnowszą wersję `dotnet-trace` [pakietu NuGet](https://www.nuget.org/packages/dotnet-trace), użyj polecenia [Narzędzia dotnet Install](../tools/dotnet-tool-install.md) :

  ```dotnetcli
  dotnet tool install --global dotnet-trace
  ```

- **Pobieranie bezpośrednie:**

  Pobierz plik wykonywalny narzędzia, który jest zgodny z platformą:

  | System operacyjny  | Platforma |
  | --- | -------- |
  | Windows | [x86](https://aka.ms/dotnet-trace/win-x86) \| [x64](https://aka.ms/dotnet-trace/win-x64) \| [ARM](https://aka.ms/dotnet-trace/win-arm) \| [ARM — x64](https://aka.ms/dotnet-trace/win-arm64) |
  | macOS   | [x64](https://aka.ms/dotnet-trace/osx-x64) |
  | Linux   | [x64](https://aka.ms/dotnet-trace/linux-x64) \| [ARM](https://aka.ms/dotnet-trace/linux-arm) \| [arm64](https://aka.ms/dotnet-trace/linux-arm64) \| [MUSL — x64](https://aka.ms/dotnet-trace/linux-musl-x64) \| [MUSL — arm64](https://aka.ms/dotnet-trace/linux-musl-arm64) |

## <a name="synopsis"></a>Streszczenie

```console
dotnet-trace [-h, --help] [--version] <command>
```

## <a name="description"></a>Opis

`dotnet-trace`Narzędzie:

* Program to międzyplatformowe narzędzie .NET Core.
* Włącza zbieranie śladów .NET Core działającego procesu bez natywnego profilera.
* Jest wbudowana w [`EventPipe`](./eventpipe.md) środowisko uruchomieniowe platformy .NET Core.
* Zapewnia takie samo środowisko w systemach Windows, Linux lub macOS.

## <a name="options"></a>Opcje

- **`-h|--help`**

  Wyświetla pomoc w wierszu polecenia.

- **`--version`**

  Wyświetla wersję narzędzia do śledzenia dotnet.

## <a name="commands"></a>Polecenia

| Polecenie                                                   |
|-----------------------------------------------------------|
| [zbieranie danych śledzenia dotnet](#dotnet-trace-collect)             |
| [Konwersja dotnet-Trace](#dotnet-trace-convert)             |
| [dotnet-Trace — śledzenie](#dotnet-trace-ps)                       |
| [dotnet-lista śledzenia — profile](#dotnet-trace-list-profiles) |

## <a name="dotnet-trace-collect"></a>zbieranie danych śledzenia dotnet

Zbiera dane śledzenia diagnostycznego z uruchomionego procesu.

### <a name="synopsis"></a>Streszczenie

```console
dotnet-trace collect [--buffersize <size>] [--clreventlevel <clreventlevel>] [--clrevents <clrevents>]
    [--format <Chromium|NetTrace|Speedscope>] [-h|--help]
    [-n, --name <name>] [--diagnostic-port] [-o|--output <trace-file-path>] [-p|--process-id <pid>]
    [--profile <profile-name>] [--providers <list-of-comma-separated-providers>]
    [-- <command>] (for target applications running .NET 5.0 or later)
```

### <a name="options"></a>Opcje

- **`--buffersize <size>`**

  Ustawia rozmiar buforu cyklicznego w pamięci (w megabajtach). Wartość domyślna to 256 MB.

- **`--clreventlevel <clreventlevel>`**

  Poziom szczegółowości zdarzeń CLR do wyemitowania.

- **`--clrevents <clrevents>`**

  Lista zdarzeń środowiska uruchomieniowego CLR do emisji.

- **`--format {Chromium|NetTrace|Speedscope}`**

  Ustawia format danych wyjściowych dla konwersji pliku śledzenia. Wartość domyślna to `NetTrace`.

- **`-n, --name <name>`**

  Nazwa procesu, z którego ma zostać zebrane śledzenie.

- **`--diagnostic-port <path-to-port>`**

  Nazwa portu diagnostycznego do utworzenia. Zobacz [Używanie portu diagnostycznego, aby zebrać ślad z uruchamiania aplikacji](#use-diagnostic-port-to-collect-a-trace-from-app-startup) , aby dowiedzieć się, jak za pomocą tej opcji zbierać dane śledzenia z uruchamiania aplikacji.

- **`-o|--output <trace-file-path>`**

  Ścieżka wyjściowa zebranych danych śledzenia. Jeśli nie zostanie określony, jego wartość domyślna to `trace.nettrace` .

- **`-p|--process-id <PID>`**

  Identyfikator procesu, z którego ma zostać zebrane śledzenie.

- **`--profile <profile-name>`**

  Nazwany wstępnie zdefiniowany zestaw konfiguracji dostawcy, który umożliwia zwięzłe Określanie typowych scenariuszy śledzenia. Dostępne są następujące profile:

 | Profil | Opis |
 |---------|-------------|
 |`cpu-sampling`|Przydatne do śledzenia użycia procesora i ogólnych informacji środowiska uruchomieniowego platformy .NET. Jest to opcja domyślna, jeśli nie określono żadnego profilu ani dostawcy.|
 |`gc-verbose`|Śledzi kolekcje GC i przykłady alokacji obiektów.|
 |`gc-collect`|Śledzi kolekcje GC tylko przy niskim obciążeniu.|

- **`--providers <list-of-comma-separated-providers>`**

  Rozdzielana przecinkami lista `EventPipe` dostawców do włączenia. Tacy dostawcy uzupełniają dostawców implikowaną przez `--profile <profile-name>` . W przypadku niespójności określonego dostawcy ta konfiguracja ma pierwszeństwo przed niejawną konfiguracją w profilu.

  Ta lista dostawców ma postać:

  - `Provider[,Provider]`
  - `Provider` ma postać: `KnownProviderName[:Flags[:Level][:KeyValueArgs]]` .
  - `KeyValueArgs` ma postać: `[key1=value1][;key2=value2]` .

- **`-- <command>` (tylko w przypadku aplikacji docelowych z programem .NET 5,0)**

  Po określeniu parametrów konfiguracji kolekcji użytkownik może dołączyć `--` po nim polecenie, aby uruchomić aplikację .NET z co najmniej 5,0 środowiskiem uruchomieniowym. Może to być przydatne podczas diagnozowania problemów, które występują na wczesnym etapie procesu, takich jak problemy z wydajnością uruchamiania lub moduł ładujący zestawu i błędy spinacza.

  > [!NOTE]
  > Użycie tej opcji monitoruje pierwszy proces programu .NET 5,0, który komunikuje się z powrotem z narzędziem, co oznacza, że polecenie uruchamia wiele aplikacji .NET będzie zbierać tylko pierwszą aplikację. W związku z tym zaleca się używanie tej opcji w aplikacjach samodzielnych lub przy użyciu `dotnet exec <app.dll>` opcji.

> [!NOTE]
> Zatrzymanie śledzenia może zająć dużo czasu (do minut) w przypadku dużych aplikacji. Środowisko uruchomieniowe musi wysyłać za pośrednictwem pamięci podręcznej typów dla całego kodu zarządzanego, który został przechwycony w śladzie.

## <a name="dotnet-trace-convert"></a>Konwersja dotnet-Trace

Konwertuje `nettrace` ślady na formaty alternatywne do użycia z alternatywnymi narzędziami do analizy śledzenia.

### <a name="synopsis"></a>Streszczenie

```console
dotnet-trace convert [<input-filename>] [--format <Chromium|NetTrace|Speedscope>] [-h|--help] [-o|--output <output-filename>]
```

### <a name="arguments"></a>Argumenty

- **`<input-filename>`**

  Wejściowy plik śledzenia do przekonwertowania. Wartość domyślna to *Trace. Trace*.

### <a name="options"></a>Opcje

- **`--format <Chromium|NetTrace|Speedscope>`**

  Ustawia format danych wyjściowych dla konwersji pliku śledzenia.

- **`-o|--output <output-filename>`**

  Nazwa pliku wyjściowego. Rozszerzenie formatu docelowego zostanie dodane.

> [!NOTE]
> Konwertowanie `nettrace` plików na `chromium` `speedscope` pliki lub plików jest nieodwracalne. `speedscope``chromium`pliki i nie zawierają wszystkich informacji niezbędnych do odtworzenia `nettrace` plików. Jednak `convert` polecenie zachowuje oryginalny `nettrace` plik, dlatego nie należy go usuwać, jeśli planujesz otworzyć go w przyszłości.

## <a name="dotnet-trace-ps"></a>dotnet-Trace — śledzenie

 Wyświetla listę procesów dotnet, z których można zbierać dane śledzenia.

### <a name="synopsis"></a>Streszczenie

```console
dotnet-trace ps [-h|--help]
```

## <a name="dotnet-trace-list-profiles"></a>dotnet-lista śledzenia — profile

Wyświetla wstępnie skompilowane profile śledzenia z opisem dostawców i filtrów w poszczególnych profilach.

### <a name="synopsis"></a>Streszczenie

```console
dotnet-trace list-profiles [-h|--help]
```

## <a name="collect-a-trace-with-dotnet-trace"></a>Zbieranie śledzenia przy użyciu funkcji monitorowania dotnet

Aby zebrać ślady przy użyciu `dotnet-trace` :

- Pobierz identyfikator procesu (PID) aplikacji .NET Core, aby zebrać ślady z programu.

  - W systemie Windows można użyć Menedżera zadań lub `tasklist` polecenia, na przykład.
  - Na przykład w systemie Linux `ps` polecenie.
  - [dotnet-Trace — śledzenie](#dotnet-trace-ps)

- Uruchom następujące polecenie:

  ```console
  dotnet-trace collect --process-id <PID>
  ```

  Poprzednie polecenie generuje dane wyjściowe podobne do następujących:

  ```console
  Press <Enter> to exit...
  Connecting to process: <Full-Path-To-Process-Being-Profiled>/dotnet.exe
  Collecting to file: <Full-Path-To-Trace>/trace.nettrace
  Session Id: <SessionId>
  Recording trace 721.025 (KB)
  ```

- Zatrzymaj zbieranie przez naciśnięcie `<Enter>` klawisza. `dotnet-trace`spowoduje zakończenie rejestrowania zdarzeń w pliku *śledzenia.*

## <a name="launch-a-child-application-and-collect-a-trace-from-its-startup-using-dotnet-trace"></a>Uruchamianie aplikacji podrzędnej i zbieranie śladów z uruchamiania przy użyciu programu dotnet-Trace

> [!IMPORTANT]
> Działa to w przypadku aplikacji z uruchomionym programem .NET 5,0 lub nowszym.

Czasami przydatne może być zebranie śladu procesu od jego uruchomienia. W przypadku aplikacji, na których działa program .NET 5,0 lub nowszy, można to zrobić za pomocą funkcji śledzenia dotnet.

Spowoduje to uruchomienie `hello.exe` z `arg1` i `arg2` jako argumentów wiersza polecenia i zebranie śladu w czasie jego uruchamiania:

```console
dotnet-trace collect -- hello.exe arg1 arg2
```

Poprzednie polecenie generuje dane wyjściowe podobne do następujących:

```console
No profile or providers specified, defaulting to trace profile 'cpu-sampling'

Provider Name                           Keywords            Level               Enabled By
Microsoft-DotNETCore-SampleProfiler     0x0000F00000000000  Informational(4)    --profile
Microsoft-Windows-DotNETRuntime         0x00000014C14FCCBD  Informational(4)    --profile

Process        : E:\temp\gcperfsim\bin\Debug\net5.0\gcperfsim.exe
Output File    : E:\temp\gcperfsim\trace.nettrace


[00:00:00:05]   Recording trace 122.244  (KB)
Press <Enter> or <Ctrl+C> to exit...
```

Można zatrzymać zbieranie śladów przez naciśnięcie klawisza `<Enter>` lub `<Ctrl + C>` klawisza. To spowoduje również wyjście `hello.exe` .

> [!NOTE]
> Uruchamianie `hello.exe` za pomocą programu dotnet-Trace spowoduje przekierowanie danych wejściowych/wyjściowych i nie będzie możliwe interakcje z jego stdin/stdout.
> Zamknięcie narzędzia za pośrednictwem kombinacji klawiszy CTRL + C lub SIGTERM spowoduje bezpieczne zakończenie zarówno narzędzia, jak i procesu podrzędnego.
> Jeśli proces podrzędny zostanie zakończony przed narzędziem, narzędzie zostanie również zakończone, a śledzenie powinno być bezpiecznie widoczne.

## <a name="use-diagnostic-port-to-collect-a-trace-from-app-startup"></a>Użyj portu diagnostycznego, aby zebrać ślad z uruchamiania aplikacji

  > [!IMPORTANT]
  > Działa to w przypadku aplikacji z uruchomionym programem .NET 5,0 lub nowszym.

Port diagnostyczny to nowa funkcja środowiska uruchomieniowego, która została dodana w programie .NET 5, która umożliwia uruchamianie śledzenia przy uruchamianiu aplikacji. W tym celu `dotnet-trace` można użyć polecenia `dotnet-trace collect -- <command>` zgodnie z opisem w powyższych przykładach lub użyć `--diagnostic-port` opcji.

Używanie `dotnet-trace <collect|monitor> -- <command>` do uruchamiania aplikacji jako procesu podrzędnego jest najprostszym sposobem na szybkie śledzenie go od jego uruchomienia.

Jeśli jednak chcesz uzyskać dokładniejszą kontrolę nad okresem istnienia śledzonej aplikacji (na przykład monitorować aplikację tylko przez pierwsze 10 minut i kontynuować) lub jeśli chcesz korzystać z aplikacji przy użyciu interfejsu wiersza polecenia, użycie `--diagnostic-port` opcji pozwala kontrolować zarówno monitorowaną aplikację docelową, jak i `dotnet-trace` .

1. Poniższe polecenie tworzy `dotnet-trace` gniazdo diagnostyczne o nazwie `myport.sock` i poczekaj na połączenie.

    > ```dotnet-cli
    > dotnet-trace collect --diagnostic-port myport.sock
    > ```

    Dane wyjściowe:

    > ```bash
    > Waiting for connection on myport.sock
    > Start an application with the following environment variable: DOTNET_DiagnosticPorts=/home/user/myport.sock
    > ```

2. W osobnej konsoli Uruchom aplikację docelową ze zmienną środowiskową `DOTNET_DiagnosticPorts` ustawioną na wartość w `dotnet-trace` danych wyjściowych.

    > ```bash
    > export DOTNET_DiagnosticPorts=/home/user/myport.sock
    > ./my-dotnet-app arg1 arg2
    > ```

    Powinno to następnie umożliwić `dotnet-trace` rozpoczęcie śledzenia `my-dotnet-app` :

    > ```bash
    > Waiting for connection on myport.sock
    > Start an application with the following environment variable: DOTNET_DiagnosticPorts=myport.sock
    > Starting a counter session. Press Q to quit.
    > ```

    > [!IMPORTANT]
    > Uruchamianie aplikacji w programie `dotnet run` może być problematyczne, ponieważ interfejs wiersza polecenia dotnet może mieć wiele procesów podrzędnych, które nie są używane przez aplikację, i mogą nawiązywać połączenie `dotnet-trace` przed aplikacją, pozostawiając, że aplikacja zostanie zawieszona w czasie wykonywania. Zaleca się, aby bezpośrednio korzystać z samodzielnej wersji aplikacji lub użyć `dotnet exec` do uruchomienia aplikacji.

## <a name="view-the-trace-captured-from-dotnet-trace"></a>Wyświetl śledzenie przechwycone przez śledzenie dotnet

W systemie Windows można przeglądać pliki *śledzenia* w usłudze [Narzędzia PerfView](https://github.com/microsoft/perfview) for Analysis: w przypadku śladów zebranych na innych platformach plik śledzenia można przenieść na komputer z systemem Windows, który ma być wyświetlany na narzędzia PerfView.

W systemie Linux śledzenie można wyświetlić, zmieniając format danych wyjściowych `dotnet-trace` na `speedscope` . Format pliku wyjściowego można zmienić przy użyciu `-f|--format` opcji — `-f speedscope` spowoduje `dotnet-trace` to utworzenie `speedscope` pliku. Można wybrać opcję `nettrace` (opcja domyślna) i `speedscope` . `Speedscope` Pliki można otwierać w lokalizacji <https://www.speedscope.app> .

> [!NOTE]
> Środowisko uruchomieniowe programu .NET Core generuje ślady w `nettrace` formacie. Ślady są konwertowane na speedscope (jeśli zostaną określone) po zakończeniu śledzenia. Ponieważ niektóre Konwersje mogą spowodować utratę danych, oryginalny `nettrace` plik zostanie zachowany obok skonwertowanego pliku.

## <a name="use-dotnet-trace-to-collect-counter-values-over-time"></a>Używanie funkcji monitorowania dotnet do zbierania wartości licznika w czasie

`dotnet-trace` może

* Służy `EventCounter` do podstawowego monitorowania kondycji w środowiskach z uwzględnieniem wydajności. Na przykład w środowisku produkcyjnym.
* Zbieraj ślady, aby nie trzeba było ich wyświetlać w czasie rzeczywistym.

Na przykład, aby zbierać wartości liczników wydajności środowiska uruchomieniowego, użyj następującego polecenia:

```console
dotnet-trace collect --process-id <PID> --providers System.Runtime:0:1:EventCounterIntervalSec=1
```

Poprzednie polecenie instruuje liczniki środowiska uruchomieniowego do raportowania co sekundę w przypadku uproszczonego monitorowania kondycji. Zastąpienie `EventCounterIntervalSec=1` o wyższej wartości (na przykład 60) umożliwia zbieranie mniejszych śladów o mniejszej szczegółowości danych licznika.

Następujące polecenie zmniejsza obciążenie i rozmiar śladu więcej niż poprzedni:

```console
dotnet-trace collect --process-id <PID> --providers System.Runtime:0:1:EventCounterIntervalSec=1,Microsoft-Windows-DotNETRuntime:0:1,Microsoft-DotNETCore-SampleProfiler:0:1
```

Poprzednie polecenie powoduje wyłączenie zdarzeń środowiska uruchomieniowego i zarządzanego profilera stosu.

## <a name="net-providers"></a>Dostawcy .NET

Środowisko uruchomieniowe platformy .NET Core obsługuje następujących dostawców platformy .NET. .NET Core używa tych samych słów kluczowych do włączenia obu `Event Tracing for Windows (ETW)` i `EventPipe` śladów.

| Nazwa dostawcy                            | Informacje |
|------------------------------------------|-------------|
| `Microsoft-Windows-DotNETRuntime`        | [Dostawca środowiska uruchomieniowego](../../framework/performance/clr-etw-providers.md#the-runtime-provider)<br>[Słowa kluczowe środowiska uruchomieniowego CLR](../../framework/performance/clr-etw-keywords-and-levels.md#runtime) |
| `Microsoft-Windows-DotNETRuntimeRundown` | [Dostawca uwalniania](../../framework/performance/clr-etw-providers.md#the-rundown-provider)<br>[Słowa kluczowe uwalniania CLR](../../framework/performance/clr-etw-keywords-and-levels.md#rundown) |
| `Microsoft-DotNETCore-SampleProfiler`    | Włącza przykładowy Profiler. |
