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
# <a name="investigate-performance-counters-dotnet-counters"></a><span data-ttu-id="885ce-103">Badanie liczników wydajności (dotnet-Counters)</span><span class="sxs-lookup"><span data-stu-id="885ce-103">Investigate performance counters (dotnet-counters)</span></span>

<span data-ttu-id="885ce-104">**Ten artykuł ma zastosowanie do:** ✔️ .net Core 3,0 SDK i nowszych wersjach</span><span class="sxs-lookup"><span data-stu-id="885ce-104">**This article applies to:** ✔️ .NET Core 3.0 SDK and later versions</span></span>

## <a name="install"></a><span data-ttu-id="885ce-105">Instalowanie</span><span class="sxs-lookup"><span data-stu-id="885ce-105">Install</span></span>

<span data-ttu-id="885ce-106">Istnieją dwa sposoby na pobranie i zainstalowanie `dotnet-counters` :</span><span class="sxs-lookup"><span data-stu-id="885ce-106">There are two ways to download and install `dotnet-counters`:</span></span>

- <span data-ttu-id="885ce-107">**Narzędzie globalne dotnet:**</span><span class="sxs-lookup"><span data-stu-id="885ce-107">**dotnet global tool:**</span></span>

  <span data-ttu-id="885ce-108">Aby zainstalować najnowszą wersję `dotnet-counters` [pakietu NuGet](https://www.nuget.org/packages/dotnet-counters), użyj polecenia [Narzędzia dotnet Install](../tools/dotnet-tool-install.md) :</span><span class="sxs-lookup"><span data-stu-id="885ce-108">To install the latest release version of the `dotnet-counters` [NuGet package](https://www.nuget.org/packages/dotnet-counters), use the [dotnet tool install](../tools/dotnet-tool-install.md) command:</span></span>

  ```dotnetcli
  dotnet tool install --global dotnet-counters
  ```

- <span data-ttu-id="885ce-109">**Pobieranie bezpośrednie:**</span><span class="sxs-lookup"><span data-stu-id="885ce-109">**Direct download:**</span></span>

  <span data-ttu-id="885ce-110">Pobierz plik wykonywalny narzędzia, który jest zgodny z platformą:</span><span class="sxs-lookup"><span data-stu-id="885ce-110">Download the tool executable that matches your platform:</span></span>

  | <span data-ttu-id="885ce-111">System operacyjny</span><span class="sxs-lookup"><span data-stu-id="885ce-111">OS</span></span>  | <span data-ttu-id="885ce-112">Platforma</span><span class="sxs-lookup"><span data-stu-id="885ce-112">Platform</span></span> |
  | --- | -------- |
  | <span data-ttu-id="885ce-113">Windows</span><span class="sxs-lookup"><span data-stu-id="885ce-113">Windows</span></span> | <span data-ttu-id="885ce-114">[x86](https://aka.ms/dotnet-counters/win-x86) \| [x64](https://aka.ms/dotnet-counters/win-x64) \| [ARM](https://aka.ms/dotnet-counters/win-arm) \| [ARM — x64](https://aka.ms/dotnet-counters/win-arm64)</span><span class="sxs-lookup"><span data-stu-id="885ce-114">[x86](https://aka.ms/dotnet-counters/win-x86) \| [x64](https://aka.ms/dotnet-counters/win-x64) \| [arm](https://aka.ms/dotnet-counters/win-arm) \| [arm-x64](https://aka.ms/dotnet-counters/win-arm64)</span></span> |
  | <span data-ttu-id="885ce-115">macOS</span><span class="sxs-lookup"><span data-stu-id="885ce-115">macOS</span></span>   | [<span data-ttu-id="885ce-116">x64</span><span class="sxs-lookup"><span data-stu-id="885ce-116">x64</span></span>](https://aka.ms/dotnet-counters/osx-x64) |
  | <span data-ttu-id="885ce-117">Linux</span><span class="sxs-lookup"><span data-stu-id="885ce-117">Linux</span></span>   | <span data-ttu-id="885ce-118">[x64](https://aka.ms/dotnet-counters/linux-x64) \| [ARM](https://aka.ms/dotnet-counters/linux-arm) \| [arm64](https://aka.ms/dotnet-counters/linux-arm64) \| [MUSL — x64](https://aka.ms/dotnet-counters/linux-musl-x64) \| [MUSL — arm64](https://aka.ms/dotnet-counters/linux-musl-arm64)</span><span class="sxs-lookup"><span data-stu-id="885ce-118">[x64](https://aka.ms/dotnet-counters/linux-x64) \| [arm](https://aka.ms/dotnet-counters/linux-arm) \| [arm64](https://aka.ms/dotnet-counters/linux-arm64) \| [musl-x64](https://aka.ms/dotnet-counters/linux-musl-x64) \| [musl-arm64](https://aka.ms/dotnet-counters/linux-musl-arm64)</span></span> |

## <a name="synopsis"></a><span data-ttu-id="885ce-119">Streszczenie</span><span class="sxs-lookup"><span data-stu-id="885ce-119">Synopsis</span></span>

```console
dotnet-counters [-h|--help] [--version] <command>
```

## <a name="description"></a><span data-ttu-id="885ce-120">Opis</span><span class="sxs-lookup"><span data-stu-id="885ce-120">Description</span></span>

<span data-ttu-id="885ce-121">`dotnet-counters` jest narzędziem do monitorowania wydajności w przypadku monitorowania kondycji ad hoc i badania wydajności pierwszego poziomu.</span><span class="sxs-lookup"><span data-stu-id="885ce-121">`dotnet-counters` is a performance monitoring tool for ad-hoc health monitoring and first-level performance investigation.</span></span> <span data-ttu-id="885ce-122">Może obserwować wartości liczników wydajności, które są publikowane za pośrednictwem <xref:System.Diagnostics.Tracing.EventCounter> interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="885ce-122">It can observe performance counter values that are published via the <xref:System.Diagnostics.Tracing.EventCounter> API.</span></span> <span data-ttu-id="885ce-123">Można na przykład szybko monitorować elementy, takie jak użycie procesora CPU lub częstotliwość zgłaszania wyjątków w aplikacji .NET Core, aby sprawdzić, czy istnieją jakieś podejrzane informacje przed uzyskaniem bardziej poważnych badań wydajności przy użyciu `PerfView` lub `dotnet-trace` .</span><span class="sxs-lookup"><span data-stu-id="885ce-123">For example, you can quickly monitor things like the CPU usage or the rate of exceptions being thrown in your .NET Core application to see if there's anything suspicious before diving into more serious performance investigation using `PerfView` or `dotnet-trace`.</span></span>

## <a name="options"></a><span data-ttu-id="885ce-124">Opcje</span><span class="sxs-lookup"><span data-stu-id="885ce-124">Options</span></span>

- **`--version`**

  <span data-ttu-id="885ce-125">Wyświetla wersję narzędzia dotnet-Counters.</span><span class="sxs-lookup"><span data-stu-id="885ce-125">Displays the version of the dotnet-counters utility.</span></span>

- **`-h|--help`**

  <span data-ttu-id="885ce-126">Wyświetla pomoc w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="885ce-126">Shows command-line help.</span></span>

## <a name="commands"></a><span data-ttu-id="885ce-127">Polecenia</span><span class="sxs-lookup"><span data-stu-id="885ce-127">Commands</span></span>

| <span data-ttu-id="885ce-128">Polecenie</span><span class="sxs-lookup"><span data-stu-id="885ce-128">Command</span></span>                                             |
|-----------------------------------------------------|
| [<span data-ttu-id="885ce-129">dotnet — Zbieranie liczników</span><span class="sxs-lookup"><span data-stu-id="885ce-129">dotnet-counters collect</span></span>](#dotnet-counters-collect) |
| [<span data-ttu-id="885ce-130">dotnet-lista liczników</span><span class="sxs-lookup"><span data-stu-id="885ce-130">dotnet-counters list</span></span>](#dotnet-counters-list)       |
| [<span data-ttu-id="885ce-131">Monitor dotnet-Counters</span><span class="sxs-lookup"><span data-stu-id="885ce-131">dotnet-counters monitor</span></span>](#dotnet-counters-monitor) |
| [<span data-ttu-id="885ce-132">dotnet-liczniki PS</span><span class="sxs-lookup"><span data-stu-id="885ce-132">dotnet-counters ps</span></span>](#dotnet-counters-ps)           |

## <a name="dotnet-counters-collect"></a><span data-ttu-id="885ce-133">dotnet — Zbieranie liczników</span><span class="sxs-lookup"><span data-stu-id="885ce-133">dotnet-counters collect</span></span>

<span data-ttu-id="885ce-134">Okresowo Zbieraj wybrane wartości licznika i Eksportuj je do określonego formatu pliku na potrzeby przetwarzania końcowego.</span><span class="sxs-lookup"><span data-stu-id="885ce-134">Periodically collect selected counter values and export them into a specified file format for post-processing.</span></span>

### <a name="synopsis"></a><span data-ttu-id="885ce-135">Streszczenie</span><span class="sxs-lookup"><span data-stu-id="885ce-135">Synopsis</span></span>

```console
dotnet-counters collect [-h|--help] [-p|--process-id] [-n|--name] [--diagnostic-port] [--refresh-interval] [--counters <COUNTERS>] [--format] [-o|--output] [-- <command>]
```

### <a name="options"></a><span data-ttu-id="885ce-136">Opcje</span><span class="sxs-lookup"><span data-stu-id="885ce-136">Options</span></span>

- **`-p|--process-id <PID>`**

  <span data-ttu-id="885ce-137">Identyfikator procesu, z którego mają być zbierane dane licznika.</span><span class="sxs-lookup"><span data-stu-id="885ce-137">The ID of the process to be collect counter data from.</span></span>

- **`-n|--name <name>`**

  <span data-ttu-id="885ce-138">Nazwa procesu, z którego mają być zbierane dane licznika.</span><span class="sxs-lookup"><span data-stu-id="885ce-138">The name of the process to be collect counter data from.</span></span>

- **`--diagnostic-port`**

  <span data-ttu-id="885ce-139">Nazwa portu diagnostycznego do utworzenia.</span><span class="sxs-lookup"><span data-stu-id="885ce-139">The name of the diagnostic port to create.</span></span> <span data-ttu-id="885ce-140">Aby rozpocząć monitorowanie liczników z uruchamiania aplikacji, zobacz [using the Diagnostic port](#using-diagnostic-port) .</span><span class="sxs-lookup"><span data-stu-id="885ce-140">See [using diagnostic port](#using-diagnostic-port) for how to use this option to start monitoring counters from app startup.</span></span>

- **`--refresh-interval <SECONDS>`**

  <span data-ttu-id="885ce-141">Liczba sekund opóźnienia między aktualizacją wyświetlanych liczników</span><span class="sxs-lookup"><span data-stu-id="885ce-141">The number of seconds to delay between updating the displayed counters</span></span>

- **`--counters <COUNTERS>`**

  <span data-ttu-id="885ce-142">Rozdzielana przecinkami lista liczników.</span><span class="sxs-lookup"><span data-stu-id="885ce-142">A comma-separated list of counters.</span></span> <span data-ttu-id="885ce-143">Można określić liczniki `provider_name[:counter_name]` .</span><span class="sxs-lookup"><span data-stu-id="885ce-143">Counters can be specified `provider_name[:counter_name]`.</span></span> <span data-ttu-id="885ce-144">Jeśli `provider_name` jest używany bez listy kwalifikującej się liczników, zostaną wyświetlone wszystkie liczniki od dostawcy.</span><span class="sxs-lookup"><span data-stu-id="885ce-144">If the `provider_name` is used without a qualifying list of counters, then all counters from the provider are shown.</span></span> <span data-ttu-id="885ce-145">Aby odnaleźć nazwy dostawcy i licznika, użyj polecenia [dotnet-Counters](#dotnet-counters-list) .</span><span class="sxs-lookup"><span data-stu-id="885ce-145">To discover provider and counter names, use the [dotnet-counters list](#dotnet-counters-list) command.</span></span>

- **`--format <csv|json>`**

  <span data-ttu-id="885ce-146">Format do wyeksportowania.</span><span class="sxs-lookup"><span data-stu-id="885ce-146">The format to be exported.</span></span> <span data-ttu-id="885ce-147">Obecnie dostępne: CSV, JSON.</span><span class="sxs-lookup"><span data-stu-id="885ce-147">Currently available: csv, json.</span></span>

- **`-o|--output <output>`**

  <span data-ttu-id="885ce-148">Nazwa pliku wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="885ce-148">The name of the output file.</span></span>

- <span data-ttu-id="885ce-149">**`-- <command>` (w przypadku aplikacji docelowych z uruchomionym programem .NET 5,0 lub nowszym)**</span><span class="sxs-lookup"><span data-stu-id="885ce-149">**`-- <command>` (for target applications running .NET 5.0 or later only)**</span></span>

  <span data-ttu-id="885ce-150">Po określeniu parametrów konfiguracji kolekcji użytkownik może dołączyć `--` po nim polecenie, aby uruchomić aplikację .NET z co najmniej 5,0 środowiskiem uruchomieniowym.</span><span class="sxs-lookup"><span data-stu-id="885ce-150">After the collection configuration parameters, the user can append `--` followed by a command to start a .NET application with at least a 5.0 runtime.</span></span> <span data-ttu-id="885ce-151">`dotnet-counters` uruchomi proces za pomocą podanego polecenia i zbierze żądane metryki.</span><span class="sxs-lookup"><span data-stu-id="885ce-151">`dotnet-counters` will launch a process with the provided command and collect the requested metrics.</span></span> <span data-ttu-id="885ce-152">Jest to często przydatne do zbierania metryk dla ścieżki uruchamiania aplikacji i może służyć do diagnozowania lub monitorowania problemów, które występują wczesne przed lub wkrótce po głównym punkcie wejścia.</span><span class="sxs-lookup"><span data-stu-id="885ce-152">This is often useful to collect metrics for the application's startup path and can be used to diagnose or monitor issues that happen early before or shortly after the main entrypoint.</span></span>

  > [!NOTE]
  > <span data-ttu-id="885ce-153">Użycie tej opcji monitoruje pierwszy proces programu .NET 5,0, który komunikuje się z powrotem z narzędziem, co oznacza, że polecenie uruchamia wiele aplikacji .NET będzie zbierać tylko pierwszą aplikację.</span><span class="sxs-lookup"><span data-stu-id="885ce-153">Using this option monitors the first .NET 5.0 process that communicates back to the tool, which means if your command launches multiple .NET applications, it will only collect the first app.</span></span> <span data-ttu-id="885ce-154">W związku z tym zaleca się używanie tej opcji w aplikacjach samodzielnych lub przy użyciu `dotnet exec <app.dll>` opcji.</span><span class="sxs-lookup"><span data-stu-id="885ce-154">Therefore, it is recommended you use this option on self-contained applications, or using the `dotnet exec <app.dll>` option.</span></span>

  > [!NOTE]
  > <span data-ttu-id="885ce-155">Uruchamianie pliku wykonywalnego platformy .NET za pośrednictwem dotnet-Counters spowoduje przekierowanie danych wejściowych/wyjściowych i uniemożliwienie współpracy z jego stdin/stdout.</span><span class="sxs-lookup"><span data-stu-id="885ce-155">Launching a .NET executable via dotnet-counters will make its input/output to be redirected and you won't be able to interact with its stdin/stdout.</span></span> <span data-ttu-id="885ce-156">Zamknięcie narzędzia za pośrednictwem kombinacji klawiszy CTRL + C lub SIGTERM spowoduje bezpieczne zakończenie zarówno narzędzia, jak i procesu podrzędnego.</span><span class="sxs-lookup"><span data-stu-id="885ce-156">Exiting the tool via CTRL+C or SIGTERM will safely end both the tool and the child process.</span></span> <span data-ttu-id="885ce-157">Jeśli proces podrzędny zostanie zakończony przed narzędziem, narzędzie zostanie również zakończone, a śledzenie powinno być bezpiecznie widoczne.</span><span class="sxs-lookup"><span data-stu-id="885ce-157">If the child process exits before the tool, the tool will exit as well and the trace should be safely viewable.</span></span> <span data-ttu-id="885ce-158">Jeśli musisz użyć stdin/stdout, możesz użyć `--diagnostic-port` opcji.</span><span class="sxs-lookup"><span data-stu-id="885ce-158">If you need to use stdin/stdout, you can use the `--diagnostic-port` option.</span></span> <span data-ttu-id="885ce-159">Aby uzyskać więcej informacji, zobacz [Używanie portu diagnostycznego](#using-diagnostic-port) .</span><span class="sxs-lookup"><span data-stu-id="885ce-159">See [Using diagnostic port](#using-diagnostic-port) for more information.</span></span>

### <a name="examples"></a><span data-ttu-id="885ce-160">Przykłady</span><span class="sxs-lookup"><span data-stu-id="885ce-160">Examples</span></span>

- <span data-ttu-id="885ce-161">Zbieraj wszystkie liczniki z interwałem odświeżania równym 3 sekund i Generuj wolumin CSV jako dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="885ce-161">Collect all counters at a refresh interval of 3 seconds and generate a csv as output:</span></span>

  ```console
  > dotnet-counters collect --process-id 1902 --refresh-interval 3 --format csv

  counter_list is unspecified. Monitoring all counters by default.
  Starting a counter session. Press Q to quit.
  ```

- <span data-ttu-id="885ce-162">Uruchom `dotnet mvc.dll` jako proces podrzędny i Rozpocznij zbieranie liczników środowiska uruchomieniowego oraz ASP.NET Core hostowanie liczników z uruchamiania i Zapisz je jako dane wyjściowe JSON:</span><span class="sxs-lookup"><span data-stu-id="885ce-162">Start `dotnet mvc.dll` as a child process and start collecting runtime counters and ASP.NET Core Hosting counters from startup and save it as a JSON output:</span></span>

  ```console
  > dotnet-counters collect --format json --counters System.Runtime,Microsoft.AspNetCore.Hosting -- dotnet mvc.dll
  Starting a counter session. Press Q to quit.
  File saved to counter.json
  ```

## <a name="dotnet-counters-list"></a><span data-ttu-id="885ce-163">dotnet-lista liczników</span><span class="sxs-lookup"><span data-stu-id="885ce-163">dotnet-counters list</span></span>

<span data-ttu-id="885ce-164">Wyświetla listę nazw liczników i opisów pogrupowanych według dostawcy.</span><span class="sxs-lookup"><span data-stu-id="885ce-164">Displays a list of counter names and descriptions, grouped by provider.</span></span>

### <a name="synopsis"></a><span data-ttu-id="885ce-165">Streszczenie</span><span class="sxs-lookup"><span data-stu-id="885ce-165">Synopsis</span></span>

```console
dotnet-counters list [-h|--help]
```

### <a name="example"></a><span data-ttu-id="885ce-166">Przykład</span><span class="sxs-lookup"><span data-stu-id="885ce-166">Example</span></span>

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
> <span data-ttu-id="885ce-167">`Microsoft.AspNetCore.Hosting`Liczniki są wyświetlane, jeśli są zidentyfikowane procesy obsługujące te liczniki, na przykład, gdy aplikacja ASP.NET Core jest uruchomiona na komputerze-hoście.</span><span class="sxs-lookup"><span data-stu-id="885ce-167">The `Microsoft.AspNetCore.Hosting` counters are displayed when there are processes identified that support these counters, for example; when an ASP.NET Core application is running on the host machine.</span></span>

## <a name="dotnet-counters-monitor"></a><span data-ttu-id="885ce-168">Monitor dotnet-Counters</span><span class="sxs-lookup"><span data-stu-id="885ce-168">dotnet-counters monitor</span></span>

<span data-ttu-id="885ce-169">Wyświetla okresowe odświeżanie wartości wybranych liczników.</span><span class="sxs-lookup"><span data-stu-id="885ce-169">Displays periodically refreshing values of selected counters.</span></span>

### <a name="synopsis"></a><span data-ttu-id="885ce-170">Streszczenie</span><span class="sxs-lookup"><span data-stu-id="885ce-170">Synopsis</span></span>

```console
dotnet-counters monitor [-h|--help] [-p|--process-id] [-n|--name] [--diagnostic-port] [--refresh-interval] [--counters] [-- <command>]
```

### <a name="options"></a><span data-ttu-id="885ce-171">Opcje</span><span class="sxs-lookup"><span data-stu-id="885ce-171">Options</span></span>

- **`-p|--process-id <PID>`**

  <span data-ttu-id="885ce-172">Identyfikator procesu, który ma być monitorowany.</span><span class="sxs-lookup"><span data-stu-id="885ce-172">The ID of the process to be monitored.</span></span>

- **`-n|--name <name>`**

  <span data-ttu-id="885ce-173">Nazwa procesu, który ma być monitorowany.</span><span class="sxs-lookup"><span data-stu-id="885ce-173">The name of the process to be monitored.</span></span>

- **`--diagnostic-port`**

  <span data-ttu-id="885ce-174">Nazwa portu diagnostycznego do utworzenia.</span><span class="sxs-lookup"><span data-stu-id="885ce-174">The name of the diagnostic port to create.</span></span> <span data-ttu-id="885ce-175">Aby rozpocząć monitorowanie liczników z uruchamiania aplikacji, zobacz [using the Diagnostic port](#using-diagnostic-port) .</span><span class="sxs-lookup"><span data-stu-id="885ce-175">See [using diagnostic port](#using-diagnostic-port) for how to use this option to start monitoring counters from app startup.</span></span>

- **`--refresh-interval <SECONDS>`**

  <span data-ttu-id="885ce-176">Liczba sekund opóźnienia między aktualizacją wyświetlanych liczników</span><span class="sxs-lookup"><span data-stu-id="885ce-176">The number of seconds to delay between updating the displayed counters</span></span>

- **`--counters <COUNTERS>`**

  <span data-ttu-id="885ce-177">Rozdzielana przecinkami lista liczników.</span><span class="sxs-lookup"><span data-stu-id="885ce-177">A comma-separated list of counters.</span></span> <span data-ttu-id="885ce-178">Można określić liczniki `provider_name[:counter_name]` .</span><span class="sxs-lookup"><span data-stu-id="885ce-178">Counters can be specified `provider_name[:counter_name]`.</span></span> <span data-ttu-id="885ce-179">Jeśli `provider_name` jest używany bez listy kwalifikującej się liczników, zostaną wyświetlone wszystkie liczniki od dostawcy.</span><span class="sxs-lookup"><span data-stu-id="885ce-179">If the `provider_name` is used without a qualifying list of counters, then all counters from the provider are shown.</span></span> <span data-ttu-id="885ce-180">Aby odnaleźć nazwy dostawcy i licznika, użyj polecenia [dotnet-Counters](#dotnet-counters-list) .</span><span class="sxs-lookup"><span data-stu-id="885ce-180">To discover provider and counter names, use the [dotnet-counters list](#dotnet-counters-list) command.</span></span>

 <span data-ttu-id="885ce-181">**`-- <command>` (w przypadku aplikacji docelowych z uruchomionym programem .NET 5,0 lub nowszym)**</span><span class="sxs-lookup"><span data-stu-id="885ce-181">**`-- <command>` (for target applications running .NET 5.0 or later only)**</span></span>

  <span data-ttu-id="885ce-182">Po określeniu parametrów konfiguracji kolekcji użytkownik może dołączyć `--` po nim polecenie, aby uruchomić aplikację .NET z co najmniej 5,0 środowiskiem uruchomieniowym.</span><span class="sxs-lookup"><span data-stu-id="885ce-182">After the collection configuration parameters, the user can append `--` followed by a command to start a .NET application with at least a 5.0 runtime.</span></span> <span data-ttu-id="885ce-183">`dotnet-counters` uruchomi proces za pomocą podanego polecenia i monitoruje żądane metryki.</span><span class="sxs-lookup"><span data-stu-id="885ce-183">`dotnet-counters` will launch a process with the provided command and monitor the requested metrics.</span></span> <span data-ttu-id="885ce-184">Jest to często przydatne do zbierania metryk dla ścieżki uruchamiania aplikacji i może służyć do diagnozowania lub monitorowania problemów, które występują wczesne przed lub wkrótce po głównym punkcie wejścia.</span><span class="sxs-lookup"><span data-stu-id="885ce-184">This is often useful to collect metrics for the application's startup path and can be used to diagnose or monitor issues that happen early before or shortly after the main entrypoint.</span></span>

  > [!NOTE]
  > <span data-ttu-id="885ce-185">Użycie tej opcji monitoruje pierwszy proces programu .NET 5,0, który komunikuje się z powrotem z narzędziem, co oznacza, że polecenie uruchamia wiele aplikacji .NET będzie zbierać tylko pierwszą aplikację.</span><span class="sxs-lookup"><span data-stu-id="885ce-185">Using this option monitors the first .NET 5.0 process that communicates back to the tool, which means if your command launches multiple .NET applications, it will only collect the first app.</span></span> <span data-ttu-id="885ce-186">W związku z tym zaleca się używanie tej opcji w aplikacjach samodzielnych lub przy użyciu `dotnet exec <app.dll>` opcji.</span><span class="sxs-lookup"><span data-stu-id="885ce-186">Therefore, it is recommended you use this option on self-contained applications, or using the `dotnet exec <app.dll>` option.</span></span>

  > [!NOTE]
  > <span data-ttu-id="885ce-187">Uruchamianie pliku wykonywalnego platformy .NET za pośrednictwem dotnet-Counters spowoduje przekierowanie danych wejściowych/wyjściowych i uniemożliwienie współpracy z jego stdin/stdout.</span><span class="sxs-lookup"><span data-stu-id="885ce-187">Launching a .NET executable via dotnet-counters will make its input/output to be redirected and you won't be able to interact with its stdin/stdout.</span></span> <span data-ttu-id="885ce-188">Zamknięcie narzędzia za pośrednictwem kombinacji klawiszy CTRL + C lub SIGTERM spowoduje bezpieczne zakończenie zarówno narzędzia, jak i procesu podrzędnego.</span><span class="sxs-lookup"><span data-stu-id="885ce-188">Exiting the tool via CTRL+C or SIGTERM will safely end both the tool and the child process.</span></span> <span data-ttu-id="885ce-189">Jeśli proces podrzędny zostanie zakończony przed narzędziem, narzędzie zostanie również zakończone, a śledzenie powinno być bezpiecznie widoczne.</span><span class="sxs-lookup"><span data-stu-id="885ce-189">If the child process exits before the tool, the tool will exit as well and the trace should be safely viewable.</span></span> <span data-ttu-id="885ce-190">Jeśli musisz użyć stdin/stdout, możesz użyć `--diagnostic-port` opcji.</span><span class="sxs-lookup"><span data-stu-id="885ce-190">If you need to use stdin/stdout, you can use the `--diagnostic-port` option.</span></span> <span data-ttu-id="885ce-191">Aby uzyskać więcej informacji, zobacz [Używanie portu diagnostycznego](#using-diagnostic-port) .</span><span class="sxs-lookup"><span data-stu-id="885ce-191">See [Using diagnostic port](#using-diagnostic-port) for more information.</span></span>

### <a name="examples"></a><span data-ttu-id="885ce-192">Przykłady</span><span class="sxs-lookup"><span data-stu-id="885ce-192">Examples</span></span>

- <span data-ttu-id="885ce-193">Monitoruj wszystkie liczniki z poziomu `System.Runtime` interwału odświeżania wynoszącego 3 sekundy:</span><span class="sxs-lookup"><span data-stu-id="885ce-193">Monitor all counters from `System.Runtime` at a refresh interval of 3 seconds:</span></span>

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

- <span data-ttu-id="885ce-194">Monitoruj tylko użycie procesora CPU i rozmiar sterty GC z `System.Runtime` :</span><span class="sxs-lookup"><span data-stu-id="885ce-194">Monitor just CPU usage and GC heap size from `System.Runtime`:</span></span>

  ```console
  > dotnet-counters monitor --process-id 1902 --counters System.Runtime[cpu-usage,gc-heap-size]

  Press p to pause, r to resume, q to quit.
    Status: Running

  [System.Runtime]
      CPU Usage (%)                                 24
      GC Heap Size (MB)                            811
  ```

- <span data-ttu-id="885ce-195">Monitoruj `EventCounter` wartości ze zdefiniowanych przez użytkownika `EventSource` .</span><span class="sxs-lookup"><span data-stu-id="885ce-195">Monitor `EventCounter` values from user-defined `EventSource`.</span></span> <span data-ttu-id="885ce-196">Aby uzyskać więcej informacji, zobacz [Samouczek: pomiar wydajności za pomocą EventCounters w programie .NET Core](event-counter-perf.md).</span><span class="sxs-lookup"><span data-stu-id="885ce-196">For more information, see [Tutorial: Measure performance using EventCounters in .NET Core](event-counter-perf.md).</span></span>

  ```console
  > dotnet-counters monitor --process-id 1902 --counters Samples-EventCounterDemos-Minimal

  Press p to pause, r to resume, q to quit.
      request                                      100
  ```

- <span data-ttu-id="885ce-197">Uruchom `my-aspnet-server.exe` i monitoruj liczbę zestawów załadowanych z jego uruchamiania (tylko .net 5,0 lub nowszy):</span><span class="sxs-lookup"><span data-stu-id="885ce-197">Launch `my-aspnet-server.exe` and monitor the # of assemblies loaded from its startup (.NET 5.0 or later only):</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="885ce-198">Działa to w przypadku aplikacji z uruchomionym programem .NET 5,0 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="885ce-198">This works for apps running .NET 5.0 or later only.</span></span>

  ```console
  > dotnet-counters monitor --counters System.Runtime[assembly-count] -- my-aspnet-server.exe

  Press p to pause, r to resume, q to quit.
    Status: Running

  [System.Runtime]
      Number of Assemblies Loaded                   24
  ```
  
- <span data-ttu-id="885ce-199">Uruchom `my-aspnet-server.exe` z `arg1` i `arg2` jako argumenty wiersza polecenia oraz Monitoruj swój zestaw roboczy i rozmiar sterty GC, korzystając z jego uruchamiania (tylko .NET 5,0 lub nowszy):</span><span class="sxs-lookup"><span data-stu-id="885ce-199">Launch `my-aspnet-server.exe` with `arg1` and `arg2` as command-line arguments and monitor its working set and GC heap size from its startup (.NET 5.0 or later only):</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="885ce-200">Działa to w przypadku aplikacji z uruchomionym programem .NET 5,0 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="885ce-200">This works for apps running .NET 5.0 or later only.</span></span>

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

## <a name="dotnet-counters-ps"></a><span data-ttu-id="885ce-201">dotnet-liczniki PS</span><span class="sxs-lookup"><span data-stu-id="885ce-201">dotnet-counters ps</span></span>

<span data-ttu-id="885ce-202">Wyświetl listę procesów dotnet, które mogą być monitorowane.</span><span class="sxs-lookup"><span data-stu-id="885ce-202">Display a list of dotnet processes that can be monitored.</span></span>

### <a name="synopsis"></a><span data-ttu-id="885ce-203">Streszczenie</span><span class="sxs-lookup"><span data-stu-id="885ce-203">Synopsis</span></span>

```console
dotnet-counters ps [-h|--help]
```

### <a name="example"></a><span data-ttu-id="885ce-204">Przykład</span><span class="sxs-lookup"><span data-stu-id="885ce-204">Example</span></span>

```console
> dotnet-counters ps
  
  15683 WebApi     /home/user/repos/WebApi/WebApi
  16324 dotnet     /usr/local/share/dotnet/dotnet
```

## <a name="using-diagnostic-port"></a><span data-ttu-id="885ce-205">Korzystanie z portu diagnostycznego</span><span class="sxs-lookup"><span data-stu-id="885ce-205">Using diagnostic port</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="885ce-206">Działa to w przypadku aplikacji z uruchomionym programem .NET 5,0 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="885ce-206">This works for apps running .NET 5.0 or later only.</span></span>

<span data-ttu-id="885ce-207">Port diagnostyczny to nowa funkcja środowiska uruchomieniowego, która została dodana w programie .NET 5, która umożliwia rozpoczęcie monitorowania lub zbierania liczników z uruchamiania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="885ce-207">Diagnostic port is a new runtime feature that was added in .NET 5 that allows you to start monitoring or collecting counters from app startup.</span></span> <span data-ttu-id="885ce-208">W tym celu `dotnet-counters` można użyć polecenia `dotnet-counters <collect|monitor> -- <command>` zgodnie z opisem w powyższych przykładach lub użyć `--diagnostic-port` opcji.</span><span class="sxs-lookup"><span data-stu-id="885ce-208">To do this using `dotnet-counters`, you can either use `dotnet-counters <collect|monitor> -- <command>` as described in the examples above, or use the `--diagnostic-port` option.</span></span>

<span data-ttu-id="885ce-209">Używanie `dotnet-counters <collect|monitor> -- <command>` do uruchamiania aplikacji jako procesu podrzędnego jest najprostszym sposobem szybkiego monitorowania go od jego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="885ce-209">Using `dotnet-counters <collect|monitor> -- <command>` to launch the application as a child process is the simplest way to quickly monitor it from its startup.</span></span>

<span data-ttu-id="885ce-210">Jeśli jednak chcesz uzyskać dokładniejszą kontrolę nad okresem istnienia monitorowanej aplikacji (na przykład monitorować aplikację tylko przez pierwsze 10 minut i kontynuować) lub jeśli chcesz korzystać z aplikacji przy użyciu interfejsu wiersza polecenia, użycie `--diagnostic-port` opcji pozwala kontrolować zarówno monitorowaną aplikację docelową, jak i `dotnet-counters` .</span><span class="sxs-lookup"><span data-stu-id="885ce-210">However, when you want to gain a finer control over the lifetime of the app being monitored (for example, monitor the app for the first 10 minutes only and continue executing) or if you need to interact with the app using the CLI, using `--diagnostic-port` option allows you to control both the target app being monitored and `dotnet-counters`.</span></span>

1. <span data-ttu-id="885ce-211">Poniższe polecenie sprawia, że liczniki dotnet tworzą gniazdo diagnostyki o nazwie `myport.sock` i poczekaj na połączenie.</span><span class="sxs-lookup"><span data-stu-id="885ce-211">The command below makes dotnet-counters create a diagnostics socket named `myport.sock` and wait for a connection.</span></span>

    > ```dotnet-cli
    > dotnet-counters collect --diagnostic-port myport.sock
    > ```

    <span data-ttu-id="885ce-212">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="885ce-212">Output:</span></span>

    > ```bash
    > Waiting for connection on myport.sock
    > Start an application with the following environment variable: DOTNET_DiagnosticPorts=/home/user/myport.sock
    > ```

2. <span data-ttu-id="885ce-213">W osobnej konsoli Uruchom aplikację docelową ze zmienną środowiskową `DOTNET_DiagnosticPorts` ustawioną na wartość w `dotnet-counters` danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="885ce-213">In a separate console, launch the target application with the environment variable `DOTNET_DiagnosticPorts` set to the value in the `dotnet-counters` output.</span></span>

    > ```bash
    > export DOTNET_DiagnosticPorts=/home/user/myport.sock
    > ./my-dotnet-app arg1 arg2
    > ```

    <span data-ttu-id="885ce-214">Powinno to następnie umożliwić `dotnet-counters` rozpoczęcie zbierania liczników w `my-dotnet-app` :</span><span class="sxs-lookup"><span data-stu-id="885ce-214">This should then enable `dotnet-counters` to start collecting counters on `my-dotnet-app`:</span></span>

    > ```bash
    > Waiting for connection on myport.sock
    > Start an application with the following environment variable: DOTNET_DiagnosticPorts=myport.sock
    > Starting a counter session. Press Q to quit.
    > ```

    > [!IMPORTANT]
    > <span data-ttu-id="885ce-215">Uruchamianie aplikacji w programie `dotnet run` może być problematyczne, ponieważ interfejs wiersza polecenia dotnet może mieć wiele procesów podrzędnych, które nie są używane przez aplikację, i mogą nawiązywać połączenie `dotnet-counters` przed aplikacją, pozostawiając, że aplikacja zostanie zawieszona w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="885ce-215">Launching your app with `dotnet run` can be problematic because the dotnet CLI may spawn many child processes that are not your app and they can connect to `dotnet-counters` before your app, leaving your app to be suspended at runtime.</span></span> <span data-ttu-id="885ce-216">Zaleca się, aby bezpośrednio korzystać z samodzielnej wersji aplikacji lub użyć `dotnet exec` do uruchomienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="885ce-216">It is recommended you directly use a self-contained version of the app or use `dotnet exec` to launch the application.</span></span>
