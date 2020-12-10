---
title: dotnet-liczniki narzędzia diagnostyczne — interfejs wiersza polecenia platformy .NET
description: Dowiedz się, jak zainstalować i używać narzędzia interfejsu wiersza polecenia dotnet-Counter do monitorowania kondycji ad hoc i badania wydajności pierwszego poziomu.
ms.date: 11/17/2020
ms.openlocfilehash: 48e3b038ddb5c9421367612a592c5ba6b9459791
ms.sourcegitcommit: 81f1bba2c97a67b5ca76bcc57b37333ffca60c7b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/10/2020
ms.locfileid: "97009550"
---
# <a name="investigate-performance-counters-dotnet-counters"></a>Badanie liczników wydajności (dotnet-Counters)

**Ten artykuł ma zastosowanie do:** ✔️ .net Core 3,0 SDK i nowszych wersjach

## <a name="install"></a>Instalowanie

Istnieją dwa sposoby na pobranie i zainstalowanie `dotnet-counters` :

- **Narzędzie globalne dotnet:**

  Aby zainstalować najnowszą wersję `dotnet-counters` [pakietu NuGet](https://www.nuget.org/packages/dotnet-counters), użyj polecenia [Narzędzia dotnet Install](../tools/dotnet-tool-install.md) :

  ```dotnetcli
  dotnet tool install --global dotnet-counters
  ```

- **Pobieranie bezpośrednie:**

  Pobierz plik wykonywalny narzędzia, który jest zgodny z platformą:

  | System operacyjny  | Platforma |
  | --- | -------- |
  | Windows | [x86](https://aka.ms/dotnet-counters/win-x86) \| [x64](https://aka.ms/dotnet-counters/win-x64) \| [ARM](https://aka.ms/dotnet-counters/win-arm) \| [ARM — x64](https://aka.ms/dotnet-counters/win-arm64) |
  | macOS   | [x64](https://aka.ms/dotnet-counters/osx-x64) |
  | Linux   | [x64](https://aka.ms/dotnet-counters/linux-x64) \| [ARM](https://aka.ms/dotnet-counters/linux-arm) \| [arm64](https://aka.ms/dotnet-counters/linux-arm64) \| [MUSL — x64](https://aka.ms/dotnet-counters/linux-musl-x64) \| [MUSL — arm64](https://aka.ms/dotnet-counters/linux-musl-arm64) |

## <a name="synopsis"></a>Streszczenie

```console
dotnet-counters [-h|--help] [--version] <command>
```

## <a name="description"></a>Opis

`dotnet-counters` jest narzędziem do monitorowania wydajności w przypadku monitorowania kondycji ad hoc i badania wydajności pierwszego poziomu. Może obserwować wartości liczników wydajności, które są publikowane za pośrednictwem <xref:System.Diagnostics.Tracing.EventCounter> interfejsu API. Można na przykład szybko monitorować elementy, takie jak użycie procesora CPU lub częstotliwość zgłaszania wyjątków w aplikacji .NET Core, aby sprawdzić, czy istnieją jakieś podejrzane informacje przed uzyskaniem bardziej poważnych badań wydajności przy użyciu `PerfView` lub `dotnet-trace` .

## <a name="options"></a>Opcje

- **`--version`**

  Wyświetla wersję narzędzia dotnet-Counters.

- **`-h|--help`**

  Wyświetla pomoc w wierszu polecenia.

## <a name="commands"></a>Polecenia

| Polecenie                                             |
|-----------------------------------------------------|
| [dotnet — Zbieranie liczników](#dotnet-counters-collect) |
| [dotnet-lista liczników](#dotnet-counters-list)       |
| [Monitor dotnet-Counters](#dotnet-counters-monitor) |
| [dotnet-liczniki PS](#dotnet-counters-ps)           |

## <a name="dotnet-counters-collect"></a>dotnet — Zbieranie liczników

Okresowo Zbieraj wybrane wartości licznika i Eksportuj je do określonego formatu pliku na potrzeby przetwarzania końcowego.

### <a name="synopsis"></a>Streszczenie

```console
dotnet-counters collect [-h|--help] [-p|--process-id] [-n|--name] [--diagnostic-port] [--refresh-interval] [--counters <COUNTERS>] [--format] [-o|--output] [-- <command>]
```

### <a name="options"></a>Opcje

- **`-p|--process-id <PID>`**

  Identyfikator procesu, z którego mają być zbierane dane licznika.

- **`-n|--name <name>`**

  Nazwa procesu, z którego mają być zbierane dane licznika.

- **`--diagnostic-port`**

  Nazwa portu diagnostycznego do utworzenia. Aby rozpocząć monitorowanie liczników z uruchamiania aplikacji, zobacz [using the Diagnostic port](#using-diagnostic-port) .

- **`--refresh-interval <SECONDS>`**

  Liczba sekund opóźnienia między aktualizacją wyświetlanych liczników

- **`--counters <COUNTERS>`**

  Rozdzielana przecinkami lista liczników. Można określić liczniki `provider_name[:counter_name]` . Jeśli `provider_name` jest używany bez listy kwalifikującej się liczników, zostaną wyświetlone wszystkie liczniki od dostawcy. Aby odnaleźć nazwy dostawcy i licznika, użyj polecenia [dotnet-Counters](#dotnet-counters-list) .

- **`--format <csv|json>`**

  Format do wyeksportowania. Obecnie dostępne: CSV, JSON.

- **`-o|--output <output>`**

  Nazwa pliku wyjściowego.

- **`-- <command>` (w przypadku aplikacji docelowych z uruchomionym programem .NET 5,0 lub nowszym)**

  Po określeniu parametrów konfiguracji kolekcji użytkownik może dołączyć `--` po nim polecenie, aby uruchomić aplikację .NET z co najmniej 5,0 środowiskiem uruchomieniowym. `dotnet-counters` uruchomi proces za pomocą podanego polecenia i zbierze żądane metryki. Jest to często przydatne do zbierania metryk dla ścieżki uruchamiania aplikacji i może służyć do diagnozowania lub monitorowania problemów, które występują wczesne przed lub wkrótce po głównym punkcie wejścia.

  > [!NOTE]
  > Użycie tej opcji monitoruje pierwszy proces programu .NET 5,0, który komunikuje się z powrotem z narzędziem, co oznacza, że polecenie uruchamia wiele aplikacji .NET będzie zbierać tylko pierwszą aplikację. W związku z tym zaleca się używanie tej opcji w aplikacjach samodzielnych lub przy użyciu `dotnet exec <app.dll>` opcji.

  > [!NOTE]
  > Uruchamianie pliku wykonywalnego platformy .NET za pośrednictwem dotnet-Counters spowoduje przekierowanie danych wejściowych/wyjściowych i uniemożliwienie współpracy z jego stdin/stdout. Zamknięcie narzędzia za pośrednictwem kombinacji klawiszy CTRL + C lub SIGTERM spowoduje bezpieczne zakończenie zarówno narzędzia, jak i procesu podrzędnego. Jeśli proces podrzędny zostanie zakończony przed narzędziem, narzędzie zostanie również zakończone, a śledzenie powinno być bezpiecznie widoczne. Jeśli musisz użyć stdin/stdout, możesz użyć `--diagnostic-port` opcji. Aby uzyskać więcej informacji, zobacz [Używanie portu diagnostycznego](#using-diagnostic-port) .

### <a name="examples"></a>Przykłady

- Zbieraj wszystkie liczniki z interwałem odświeżania równym 3 sekund i Generuj wolumin CSV jako dane wyjściowe:

  ```console
  > dotnet-counters collect --process-id 1902 --refresh-interval 3 --format csv

  counter_list is unspecified. Monitoring all counters by default.
  Starting a counter session. Press Q to quit.
  ```

- Uruchom `dotnet mvc.dll` jako proces podrzędny i Rozpocznij zbieranie liczników środowiska uruchomieniowego oraz ASP.NET Core hostowanie liczników z uruchamiania i Zapisz je jako dane wyjściowe JSON:

  ```console
  > dotnet-counters collect --format json --counters System.Runtime,Microsoft.AspNetCore.Hosting -- dotnet mvc.dll
  Starting a counter session. Press Q to quit.
  File saved to counter.json
  ```

## <a name="dotnet-counters-list"></a>dotnet-lista liczników

Wyświetla listę nazw liczników i opisów pogrupowanych według dostawcy.

### <a name="synopsis"></a>Streszczenie

```console
dotnet-counters list [-h|--help]
```

### <a name="example"></a>Przykład

```console
> dotnet-counters list
Showing well-known counters only. Specific processes may support additional counters.

System.Runtime
    cpu-usage                                    Amount of time the process has utilized the CPU (ms)
    working-set                                  Amount of working set used by the process (MB)
    gc-heap-size                                 Total heap size reported by the GC (MB)
    gen-0-gc-count                               Number of Gen 0 GCs / min
    gen-1-gc-count                               Number of Gen 1 GCs / min
    gen-2-gc-count                               Number of Gen 2 GCs / min
    time-in-gc                                   % time in GC since the last GC
    gen-0-size                                   Gen 0 Heap Size
    gen-1-size                                   Gen 1 Heap Size
    gen-2-size                                   Gen 2 Heap Size
    loh-size                                     LOH Heap Size
    alloc-rate                                   Allocation Rate
    assembly-count                               Number of Assemblies Loaded
    exception-count                              Number of Exceptions / sec
    threadpool-thread-count                      Number of ThreadPool Threads
    monitor-lock-contention-count                Monitor Lock Contention Count
    threadpool-queue-length                      ThreadPool Work Items Queue Length
    threadpool-completed-items-count             ThreadPool Completed Work Items Count
    active-timer-count                           Active Timers Count

Microsoft.AspNetCore.Hosting
    requests-per-second                  Request rate
    total-requests                       Total number of requests
    current-requests                     Current number of requests
    failed-requests                      Failed number of requests
```

> [!NOTE]
> `Microsoft.AspNetCore.Hosting`Liczniki są wyświetlane, jeśli są zidentyfikowane procesy obsługujące te liczniki, na przykład, gdy aplikacja ASP.NET Core jest uruchomiona na komputerze-hoście.

## <a name="dotnet-counters-monitor"></a>Monitor dotnet-Counters

Wyświetla okresowe odświeżanie wartości wybranych liczników.

### <a name="synopsis"></a>Streszczenie

```console
dotnet-counters monitor [-h|--help] [-p|--process-id] [-n|--name] [--diagnostic-port] [--refresh-interval] [--counters] [-- <command>]
```

### <a name="options"></a>Opcje

- **`-p|--process-id <PID>`**

  Identyfikator procesu, który ma być monitorowany.

- **`-n|--name <name>`**

  Nazwa procesu, który ma być monitorowany.

- **`--diagnostic-port`**

  Nazwa portu diagnostycznego do utworzenia. Aby rozpocząć monitorowanie liczników z uruchamiania aplikacji, zobacz [using the Diagnostic port](#using-diagnostic-port) .

- **`--refresh-interval <SECONDS>`**

  Liczba sekund opóźnienia między aktualizacją wyświetlanych liczników

- **`--counters <COUNTERS>`**

  Rozdzielana przecinkami lista liczników. Można określić liczniki `provider_name[:counter_name]` . Jeśli `provider_name` jest używany bez listy kwalifikującej się liczników, zostaną wyświetlone wszystkie liczniki od dostawcy. Aby odnaleźć nazwy dostawcy i licznika, użyj polecenia [dotnet-Counters](#dotnet-counters-list) .

 **`-- <command>` (w przypadku aplikacji docelowych z uruchomionym programem .NET 5,0 lub nowszym)**

  Po określeniu parametrów konfiguracji kolekcji użytkownik może dołączyć `--` po nim polecenie, aby uruchomić aplikację .NET z co najmniej 5,0 środowiskiem uruchomieniowym. `dotnet-counters` uruchomi proces za pomocą podanego polecenia i monitoruje żądane metryki. Jest to często przydatne do zbierania metryk dla ścieżki uruchamiania aplikacji i może służyć do diagnozowania lub monitorowania problemów, które występują wczesne przed lub wkrótce po głównym punkcie wejścia.

  > [!NOTE]
  > Użycie tej opcji monitoruje pierwszy proces programu .NET 5,0, który komunikuje się z powrotem z narzędziem, co oznacza, że polecenie uruchamia wiele aplikacji .NET będzie zbierać tylko pierwszą aplikację. W związku z tym zaleca się używanie tej opcji w aplikacjach samodzielnych lub przy użyciu `dotnet exec <app.dll>` opcji.

  > [!NOTE]
  > Uruchamianie pliku wykonywalnego platformy .NET za pośrednictwem dotnet-Counters spowoduje przekierowanie danych wejściowych/wyjściowych i uniemożliwienie współpracy z jego stdin/stdout. Zamknięcie narzędzia za pośrednictwem kombinacji klawiszy CTRL + C lub SIGTERM spowoduje bezpieczne zakończenie zarówno narzędzia, jak i procesu podrzędnego. Jeśli proces podrzędny zostanie zakończony przed narzędziem, narzędzie zostanie również zakończone, a śledzenie powinno być bezpiecznie widoczne. Jeśli musisz użyć stdin/stdout, możesz użyć `--diagnostic-port` opcji. Aby uzyskać więcej informacji, zobacz [Używanie portu diagnostycznego](#using-diagnostic-port) .

### <a name="examples"></a>Przykłady

- Monitoruj wszystkie liczniki z poziomu `System.Runtime` interwału odświeżania wynoszącego 3 sekundy:

  ```console
  > dotnet-counters monitor --process-id 1902  --refresh-interval 3 --counters System.Runtime
  Press p to pause, r to resume, q to quit.
      Status: Running

  [System.Runtime]
      % Time in GC since last GC (%)                                 0
      Allocation Rate (B / 1 sec)                                5,376
      CPU Usage (%)                                                  0
      Exception Count (Count / 1 sec)                                0
      GC Fragmentation (%)                                          48.467
      GC Heap Size (MB)                                              0
      Gen 0 GC Count (Count / 1 sec)                                 1
      Gen 0 Size (B)                                                24
      Gen 1 GC Count (Count / 1 sec)                                 1
      Gen 1 Size (B)                                                24
      Gen 2 GC Count (Count / 1 sec)                                 1
      Gen 2 Size (B)                                           272,000
      IL Bytes Jitted (B)                                       19,449
      LOH Size (B)                                              19,640
      Monitor Lock Contention Count (Count / 1 sec)                  0
      Number of Active Timers                                        0
      Number of Assemblies Loaded                                    7
      Number of Methods Jitted                                     166
      POH (Pinned Object Heap) Size (B)                             24
      ThreadPool Completed Work Item Count (Count / 1 sec)           0
      ThreadPool Queue Length                                        0
      ThreadPool Thread Count                                        2
      Working Set (MB)                                              19
  ```

- Monitoruj tylko użycie procesora CPU i rozmiar sterty GC z `System.Runtime` :

  ```console
  > dotnet-counters monitor --process-id 1902 --counters System.Runtime[cpu-usage,gc-heap-size]

  Press p to pause, r to resume, q to quit.
    Status: Running

  [System.Runtime]
      CPU Usage (%)                                 24
      GC Heap Size (MB)                            811
  ```

- Monitoruj `EventCounter` wartości ze zdefiniowanych przez użytkownika `EventSource` . Aby uzyskać więcej informacji, zobacz [Samouczek: pomiar wydajności za pomocą EventCounters w programie .NET Core](event-counter-perf.md).

  ```console
  > dotnet-counters monitor --process-id 1902 --counters Samples-EventCounterDemos-Minimal

  Press p to pause, r to resume, q to quit.
      request                                      100
  ```

- Uruchom `my-aspnet-server.exe` i monitoruj liczbę zestawów załadowanych z jego uruchamiania (tylko .net 5,0 lub nowszy):

  > [!IMPORTANT]
  > Działa to w przypadku aplikacji z uruchomionym programem .NET 5,0 lub nowszym.

  ```console
  > dotnet-counters monitor --counters System.Runtime[assembly-count] -- my-aspnet-server.exe

  Press p to pause, r to resume, q to quit.
    Status: Running

  [System.Runtime]
      Number of Assemblies Loaded                   24
  ```
  
- Uruchom `my-aspnet-server.exe` z `arg1` i `arg2` jako argumenty wiersza polecenia oraz Monitoruj swój zestaw roboczy i rozmiar sterty GC, korzystając z jego uruchamiania (tylko .NET 5,0 lub nowszy):

  > [!IMPORTANT]
  > Działa to w przypadku aplikacji z uruchomionym programem .NET 5,0 lub nowszym.

  ```console
  > dotnet-counters monitor --counters System.Runtime[working-set,gc-heap-size] -- my-aspnet-server.exe arg1 arg2
  ```

  ```console
  Press p to pause, r to resume, q to quit.
    Status: Running

  [System.Runtime]
      GC Heap Size (MB)                                 39
      Working Set (MB)                                  59
  ```

## <a name="dotnet-counters-ps"></a>dotnet-liczniki PS

Wyświetl listę procesów dotnet, które mogą być monitorowane.

### <a name="synopsis"></a>Streszczenie

```console
dotnet-counters ps [-h|--help]
```

### <a name="example"></a>Przykład

```console
> dotnet-counters ps
  
  15683 WebApi     /home/user/repos/WebApi/WebApi
  16324 dotnet     /usr/local/share/dotnet/dotnet
```

## <a name="using-diagnostic-port"></a>Korzystanie z portu diagnostycznego

  > [!IMPORTANT]
  > Działa to w przypadku aplikacji z uruchomionym programem .NET 5,0 lub nowszym.

Port diagnostyczny to nowa funkcja środowiska uruchomieniowego, która została dodana w programie .NET 5, która umożliwia rozpoczęcie monitorowania lub zbierania liczników z uruchamiania aplikacji. W tym celu `dotnet-counters` można użyć polecenia `dotnet-counters <collect|monitor> -- <command>` zgodnie z opisem w powyższych przykładach lub użyć `--diagnostic-port` opcji.

Używanie `dotnet-counters <collect|monitor> -- <command>` do uruchamiania aplikacji jako procesu podrzędnego jest najprostszym sposobem szybkiego monitorowania go od jego uruchomienia.

Jeśli jednak chcesz uzyskać dokładniejszą kontrolę nad okresem istnienia monitorowanej aplikacji (na przykład monitorować aplikację tylko przez pierwsze 10 minut i kontynuować) lub jeśli chcesz korzystać z aplikacji przy użyciu interfejsu wiersza polecenia, użycie `--diagnostic-port` opcji pozwala kontrolować zarówno monitorowaną aplikację docelową, jak i `dotnet-counters` .

1. Poniższe polecenie sprawia, że liczniki dotnet tworzą gniazdo diagnostyki o nazwie `myport.sock` i poczekaj na połączenie.

    > ```dotnet-cli
    > dotnet-counters collect --diagnostic-port myport.sock
    > ```

    Dane wyjściowe:

    > ```bash
    > Waiting for connection on myport.sock
    > Start an application with the following environment variable: DOTNET_DiagnosticPorts=/home/user/myport.sock
    > ```

2. W osobnej konsoli Uruchom aplikację docelową ze zmienną środowiskową `DOTNET_DiagnosticPorts` ustawioną na wartość w `dotnet-counters` danych wyjściowych.

    > ```bash
    > export DOTNET_DiagnosticPorts=/home/user/myport.sock
    > ./my-dotnet-app arg1 arg2
    > ```

    Powinno to następnie umożliwić `dotnet-counters` rozpoczęcie zbierania liczników w `my-dotnet-app` :

    > ```bash
    > Waiting for connection on myport.sock
    > Start an application with the following environment variable: DOTNET_DiagnosticPorts=myport.sock
    > Starting a counter session. Press Q to quit.
    > ```

    > [!IMPORTANT]
    > Uruchamianie aplikacji w programie `dotnet run` może być problematyczne, ponieważ interfejs wiersza polecenia dotnet może mieć wiele procesów podrzędnych, które nie są używane przez aplikację, i mogą nawiązywać połączenie `dotnet-counters` przed aplikacją, pozostawiając, że aplikacja zostanie zawieszona w czasie wykonywania. Zaleca się, aby bezpośrednio korzystać z samodzielnej wersji aplikacji lub użyć `dotnet exec` do uruchomienia aplikacji.
