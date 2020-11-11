---
title: dotnet-Trace Tool-.NET Core
description: Instalowanie i używanie narzędzia wiersza polecenia do śledzenia dotnet.
ms.date: 11/21/2019
ms.openlocfilehash: d4175ccad785b21f860044a4fd5d691624ec495e
ms.sourcegitcommit: bc9c63541c3dc756d48a7ce9d22b5583a18cf7fd
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/11/2020
ms.locfileid: "94507231"
---
# <a name="dotnet-trace-performance-analysis-utility"></a><span data-ttu-id="00cca-103">Narzędzie do analizy wydajności śledzenia dotnet</span><span class="sxs-lookup"><span data-stu-id="00cca-103">dotnet-trace performance analysis utility</span></span>

<span data-ttu-id="00cca-104">**Ten artykuł ma zastosowanie do:** ✔️ .net Core 3,0 SDK i nowszych wersjach</span><span class="sxs-lookup"><span data-stu-id="00cca-104">**This article applies to:** ✔️ .NET Core 3.0 SDK and later versions</span></span>

## <a name="install-dotnet-trace"></a><span data-ttu-id="00cca-105">Zainstaluj program dotnet-Trace</span><span class="sxs-lookup"><span data-stu-id="00cca-105">Install dotnet-trace</span></span>

<span data-ttu-id="00cca-106">Zainstaluj `dotnet-trace` [pakiet NuGet](https://www.nuget.org/packages/dotnet-trace) za pomocą polecenia [instalacji narzędzia dotnet](../tools/dotnet-tool-install.md) :</span><span class="sxs-lookup"><span data-stu-id="00cca-106">Install `dotnet-trace` [NuGet package](https://www.nuget.org/packages/dotnet-trace) with the [dotnet tool install](../tools/dotnet-tool-install.md) command:</span></span>

```dotnetcli
dotnet tool install --global dotnet-trace
```

## <a name="synopsis"></a><span data-ttu-id="00cca-107">Streszczenie</span><span class="sxs-lookup"><span data-stu-id="00cca-107">Synopsis</span></span>

```console
dotnet-trace [-h, --help] [--version] <command>
```

## <a name="description"></a><span data-ttu-id="00cca-108">Opis</span><span class="sxs-lookup"><span data-stu-id="00cca-108">Description</span></span>

<span data-ttu-id="00cca-109">`dotnet-trace`Narzędzie:</span><span class="sxs-lookup"><span data-stu-id="00cca-109">The `dotnet-trace` tool:</span></span>

* <span data-ttu-id="00cca-110">Program to międzyplatformowe narzędzie .NET Core.</span><span class="sxs-lookup"><span data-stu-id="00cca-110">Is a cross-platform .NET Core tool.</span></span>
* <span data-ttu-id="00cca-111">Włącza zbieranie śladów .NET Core działającego procesu bez natywnego profilera.</span><span class="sxs-lookup"><span data-stu-id="00cca-111">Enables the collection of .NET Core traces of a running process without a native profiler.</span></span>
* <span data-ttu-id="00cca-112">Program jest oparty na technologii międzyplatformowej `EventPipe` środowiska uruchomieniowego platformy .NET Core.</span><span class="sxs-lookup"><span data-stu-id="00cca-112">Is built around the cross-platform `EventPipe` technology of the .NET Core runtime.</span></span>
* <span data-ttu-id="00cca-113">Zapewnia takie samo środowisko w systemach Windows, Linux lub macOS.</span><span class="sxs-lookup"><span data-stu-id="00cca-113">Delivers the same experience on Windows, Linux, or macOS.</span></span>

## <a name="options"></a><span data-ttu-id="00cca-114">Opcje</span><span class="sxs-lookup"><span data-stu-id="00cca-114">Options</span></span>

- **`-h|--help`**

  <span data-ttu-id="00cca-115">Wyświetla pomoc w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="00cca-115">Shows command-line help.</span></span>

- **`--version`**

  <span data-ttu-id="00cca-116">Wyświetla wersję narzędzia do śledzenia dotnet.</span><span class="sxs-lookup"><span data-stu-id="00cca-116">Displays the version of the dotnet-trace utility.</span></span>

## <a name="commands"></a><span data-ttu-id="00cca-117">Polecenia</span><span class="sxs-lookup"><span data-stu-id="00cca-117">Commands</span></span>

| <span data-ttu-id="00cca-118">Polecenie</span><span class="sxs-lookup"><span data-stu-id="00cca-118">Command</span></span>                                                   |
|-----------------------------------------------------------|
| [<span data-ttu-id="00cca-119">zbieranie danych śledzenia dotnet</span><span class="sxs-lookup"><span data-stu-id="00cca-119">dotnet-trace collect</span></span>](#dotnet-trace-collect)             |
| [<span data-ttu-id="00cca-120">Konwersja dotnet-Trace</span><span class="sxs-lookup"><span data-stu-id="00cca-120">dotnet-trace convert</span></span>](#dotnet-trace-convert)             |
| [<span data-ttu-id="00cca-121">dotnet-Trace — śledzenie</span><span class="sxs-lookup"><span data-stu-id="00cca-121">dotnet-trace ps</span></span>](#dotnet-trace-ps)                       |
| [<span data-ttu-id="00cca-122">dotnet-lista śledzenia — profile</span><span class="sxs-lookup"><span data-stu-id="00cca-122">dotnet-trace list-profiles</span></span>](#dotnet-trace-list-profiles) |

## <a name="dotnet-trace-collect"></a><span data-ttu-id="00cca-123">zbieranie danych śledzenia dotnet</span><span class="sxs-lookup"><span data-stu-id="00cca-123">dotnet-trace collect</span></span>

<span data-ttu-id="00cca-124">Zbiera dane śledzenia diagnostycznego z uruchomionego procesu.</span><span class="sxs-lookup"><span data-stu-id="00cca-124">Collects a diagnostic trace from a running process.</span></span>

### <a name="synopsis"></a><span data-ttu-id="00cca-125">Streszczenie</span><span class="sxs-lookup"><span data-stu-id="00cca-125">Synopsis</span></span>

```console
dotnet-trace collect [--buffersize <size>] [--clreventlevel <clreventlevel>] [--clrevents <clrevents>]
    [--format <Chromium|NetTrace|Speedscope>] [-h|--help]
    [-n, --name <name>]  [-o|--output <trace-file-path>] [-p|--process-id <pid>]
    [--profile <profile-name>] [--providers <list-of-comma-separated-providers>]
    [-- <command>] (for target applications running .NET 5.0 or later)
```

### <a name="options"></a><span data-ttu-id="00cca-126">Opcje</span><span class="sxs-lookup"><span data-stu-id="00cca-126">Options</span></span>

- **`--buffersize <size>`**

  <span data-ttu-id="00cca-127">Ustawia rozmiar buforu cyklicznego w pamięci (w megabajtach).</span><span class="sxs-lookup"><span data-stu-id="00cca-127">Sets the size of the in-memory circular buffer, in megabytes.</span></span> <span data-ttu-id="00cca-128">Wartość domyślna to 256 MB.</span><span class="sxs-lookup"><span data-stu-id="00cca-128">Default 256 MB.</span></span>

- **`--clreventlevel <clreventlevel>`**

  <span data-ttu-id="00cca-129">Poziom szczegółowości zdarzeń CLR do wyemitowania.</span><span class="sxs-lookup"><span data-stu-id="00cca-129">Verbosity of CLR events to be emitted.</span></span>

- **`--clrevents <clrevents>`**

  <span data-ttu-id="00cca-130">Lista zdarzeń środowiska uruchomieniowego CLR do emisji.</span><span class="sxs-lookup"><span data-stu-id="00cca-130">List of CLR runtime events to emit.</span></span>

- **`--format {Chromium|NetTrace|Speedscope}`**

  <span data-ttu-id="00cca-131">Ustawia format danych wyjściowych dla konwersji pliku śledzenia.</span><span class="sxs-lookup"><span data-stu-id="00cca-131">Sets the output format for the trace file conversion.</span></span> <span data-ttu-id="00cca-132">Wartość domyślna to `NetTrace`.</span><span class="sxs-lookup"><span data-stu-id="00cca-132">The default is `NetTrace`.</span></span>

- **`-n, --name <name>`**

  <span data-ttu-id="00cca-133">Nazwa procesu, z którego ma zostać zebrane śledzenie.</span><span class="sxs-lookup"><span data-stu-id="00cca-133">The name of the process to collect the trace from.</span></span>

- **`-o|--output <trace-file-path>`**

  <span data-ttu-id="00cca-134">Ścieżka wyjściowa zebranych danych śledzenia.</span><span class="sxs-lookup"><span data-stu-id="00cca-134">The output path for the collected trace data.</span></span> <span data-ttu-id="00cca-135">Jeśli nie zostanie określony, jego wartość domyślna to `trace.nettrace` .</span><span class="sxs-lookup"><span data-stu-id="00cca-135">If not specified, it defaults to `trace.nettrace`.</span></span>

- **`-p|--process-id <PID>`**

  <span data-ttu-id="00cca-136">Identyfikator procesu, z którego ma zostać zebrane śledzenie.</span><span class="sxs-lookup"><span data-stu-id="00cca-136">The process id to collect the trace from.</span></span>

- **`--profile <profile-name>`**

  <span data-ttu-id="00cca-137">Nazwany wstępnie zdefiniowany zestaw konfiguracji dostawcy, który umożliwia zwięzłe Określanie typowych scenariuszy śledzenia.</span><span class="sxs-lookup"><span data-stu-id="00cca-137">A named pre-defined set of provider configurations that allows common tracing scenarios to be specified succinctly.</span></span>

- **`--providers <list-of-comma-separated-providers>`**

  <span data-ttu-id="00cca-138">Rozdzielana przecinkami lista `EventPipe` dostawców do włączenia.</span><span class="sxs-lookup"><span data-stu-id="00cca-138">A comma-separated list of `EventPipe` providers to be enabled.</span></span> <span data-ttu-id="00cca-139">Tacy dostawcy uzupełniają dostawców implikowaną przez `--profile <profile-name>` .</span><span class="sxs-lookup"><span data-stu-id="00cca-139">These providers supplement any providers implied by `--profile <profile-name>`.</span></span> <span data-ttu-id="00cca-140">W przypadku niespójności określonego dostawcy ta konfiguracja ma pierwszeństwo przed niejawną konfiguracją w profilu.</span><span class="sxs-lookup"><span data-stu-id="00cca-140">If there's any inconsistency for a particular provider, this configuration takes precedence over the implicit configuration from the profile.</span></span>

  <span data-ttu-id="00cca-141">Ta lista dostawców ma postać:</span><span class="sxs-lookup"><span data-stu-id="00cca-141">This list of providers is in the form:</span></span>

  - `Provider[,Provider]`
  - <span data-ttu-id="00cca-142">`Provider` ma postać: `KnownProviderName[:Flags[:Level][:KeyValueArgs]]` .</span><span class="sxs-lookup"><span data-stu-id="00cca-142">`Provider` is in the form: `KnownProviderName[:Flags[:Level][:KeyValueArgs]]`.</span></span>
  - <span data-ttu-id="00cca-143">`KeyValueArgs` ma postać: `[key1=value1][;key2=value2]` .</span><span class="sxs-lookup"><span data-stu-id="00cca-143">`KeyValueArgs` is in the form: `[key1=value1][;key2=value2]`.</span></span>

- <span data-ttu-id="00cca-144">**`-- <command>` (tylko w przypadku aplikacji docelowych z programem .NET 5,0)**</span><span class="sxs-lookup"><span data-stu-id="00cca-144">**`-- <command>` (for target applications running .NET 5.0 only)**</span></span>

  <span data-ttu-id="00cca-145">Po określeniu parametrów konfiguracji kolekcji użytkownik może dołączyć `--` po nim polecenie, aby uruchomić aplikację .NET z co najmniej 5,0 środowiskiem uruchomieniowym.</span><span class="sxs-lookup"><span data-stu-id="00cca-145">After the collection configuration parameters, the user can append `--` followed by a command to start a .NET application with at least a 5.0 runtime.</span></span> <span data-ttu-id="00cca-146">Może to być przydatne podczas diagnozowania problemów, które występują na wczesnym etapie procesu, takich jak problemy z wydajnością uruchamiania lub moduł ładujący zestawu i błędy spinacza.</span><span class="sxs-lookup"><span data-stu-id="00cca-146">This may be helpful when diagnosing issues that happen early in the process, such as startup performance issue or assembly loader and binder errors.</span></span>

  > [!NOTE]
  > <span data-ttu-id="00cca-147">Użycie tej opcji monitoruje pierwszy proces programu .NET 5,0, który komunikuje się z powrotem z narzędziem, co oznacza, że polecenie uruchamia wiele aplikacji .NET będzie zbierać tylko pierwszą aplikację.</span><span class="sxs-lookup"><span data-stu-id="00cca-147">Using this option monitors the first .NET 5.0 process that communicates back to the tool, which means if your command launches multiple .NET applications, it will only collect the first app.</span></span> <span data-ttu-id="00cca-148">W związku z tym zaleca się używanie tej opcji w aplikacjach samodzielnych lub przy użyciu `dotnet exec <app.dll>` opcji.</span><span class="sxs-lookup"><span data-stu-id="00cca-148">Therefore, it is recommended you use this option on self-contained applications, or using the `dotnet exec <app.dll>` option.</span></span>

## <a name="dotnet-trace-convert"></a><span data-ttu-id="00cca-149">Konwersja dotnet-Trace</span><span class="sxs-lookup"><span data-stu-id="00cca-149">dotnet-trace convert</span></span>

<span data-ttu-id="00cca-150">Konwertuje `nettrace` ślady na formaty alternatywne do użycia z alternatywnymi narzędziami do analizy śledzenia.</span><span class="sxs-lookup"><span data-stu-id="00cca-150">Converts `nettrace` traces to alternate formats for use with alternate trace analysis tools.</span></span>

### <a name="synopsis"></a><span data-ttu-id="00cca-151">Streszczenie</span><span class="sxs-lookup"><span data-stu-id="00cca-151">Synopsis</span></span>

```console
dotnet-trace convert [<input-filename>] [--format <Chromium|NetTrace|Speedscope>] [-h|--help] [-o|--output <output-filename>]
```

### <a name="arguments"></a><span data-ttu-id="00cca-152">Argumenty</span><span class="sxs-lookup"><span data-stu-id="00cca-152">Arguments</span></span>

- **`<input-filename>`**

  <span data-ttu-id="00cca-153">Wejściowy plik śledzenia do przekonwertowania.</span><span class="sxs-lookup"><span data-stu-id="00cca-153">Input trace file to be converted.</span></span> <span data-ttu-id="00cca-154">Wartość domyślna to *Trace. Trace*.</span><span class="sxs-lookup"><span data-stu-id="00cca-154">Defaults to *trace.nettrace*.</span></span>

### <a name="options"></a><span data-ttu-id="00cca-155">Opcje</span><span class="sxs-lookup"><span data-stu-id="00cca-155">Options</span></span>

- **`--format <Chromium|NetTrace|Speedscope>`**

  <span data-ttu-id="00cca-156">Ustawia format danych wyjściowych dla konwersji pliku śledzenia.</span><span class="sxs-lookup"><span data-stu-id="00cca-156">Sets the output format for the trace file conversion.</span></span>

- **`-o|--output <output-filename>`**

  <span data-ttu-id="00cca-157">Nazwa pliku wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="00cca-157">Output filename.</span></span> <span data-ttu-id="00cca-158">Rozszerzenie formatu docelowego zostanie dodane.</span><span class="sxs-lookup"><span data-stu-id="00cca-158">Extension of target format will be added.</span></span>

## <a name="dotnet-trace-ps"></a><span data-ttu-id="00cca-159">dotnet-Trace — śledzenie</span><span class="sxs-lookup"><span data-stu-id="00cca-159">dotnet-trace ps</span></span>

 <span data-ttu-id="00cca-160">Wyświetla listę procesów dotnet, z których można zbierać dane śledzenia.</span><span class="sxs-lookup"><span data-stu-id="00cca-160">Lists the dotnet processes that traces can be collected from.</span></span>

### <a name="synopsis"></a><span data-ttu-id="00cca-161">Streszczenie</span><span class="sxs-lookup"><span data-stu-id="00cca-161">Synopsis</span></span>

```console
dotnet-trace ps [-h|--help]
```

## <a name="dotnet-trace-list-profiles"></a><span data-ttu-id="00cca-162">dotnet-lista śledzenia — profile</span><span class="sxs-lookup"><span data-stu-id="00cca-162">dotnet-trace list-profiles</span></span>

<span data-ttu-id="00cca-163">Wyświetla wstępnie skompilowane profile śledzenia z opisem dostawców i filtrów w poszczególnych profilach.</span><span class="sxs-lookup"><span data-stu-id="00cca-163">Lists pre-built tracing profiles with a description of what providers and filters are in each profile.</span></span>

### <a name="synopsis"></a><span data-ttu-id="00cca-164">Streszczenie</span><span class="sxs-lookup"><span data-stu-id="00cca-164">Synopsis</span></span>

```console
dotnet-trace list-profiles [-h|--help]
```

## <a name="collect-a-trace-with-dotnet-trace"></a><span data-ttu-id="00cca-165">Zbieranie śledzenia przy użyciu funkcji monitorowania dotnet</span><span class="sxs-lookup"><span data-stu-id="00cca-165">Collect a trace with dotnet-trace</span></span>

<span data-ttu-id="00cca-166">Aby zebrać ślady przy użyciu `dotnet-trace` :</span><span class="sxs-lookup"><span data-stu-id="00cca-166">To collect traces using `dotnet-trace`:</span></span>

- <span data-ttu-id="00cca-167">Pobierz identyfikator procesu (PID) aplikacji .NET Core, aby zebrać ślady z programu.</span><span class="sxs-lookup"><span data-stu-id="00cca-167">Get the process identifier (PID) of the .NET Core application to collect traces from.</span></span>

  - <span data-ttu-id="00cca-168">W systemie Windows można użyć Menedżera zadań lub `tasklist` polecenia, na przykład.</span><span class="sxs-lookup"><span data-stu-id="00cca-168">On Windows, you can use Task Manager or the `tasklist` command, for example.</span></span>
  - <span data-ttu-id="00cca-169">Na przykład w systemie Linux `ps` polecenie.</span><span class="sxs-lookup"><span data-stu-id="00cca-169">On Linux, for example, the `ps` command.</span></span>
  - [<span data-ttu-id="00cca-170">dotnet-Trace — śledzenie</span><span class="sxs-lookup"><span data-stu-id="00cca-170">dotnet-trace ps</span></span>](#dotnet-trace-ps)

- <span data-ttu-id="00cca-171">Uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="00cca-171">Run the following command:</span></span>

  ```console
  dotnet-trace collect --process-id <PID>
  ```

  <span data-ttu-id="00cca-172">Poprzednie polecenie generuje dane wyjściowe podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="00cca-172">The preceding command generates output similar to the following:</span></span>

  ```console
  Press <Enter> to exit...
  Connecting to process: <Full-Path-To-Process-Being-Profiled>/dotnet.exe
  Collecting to file: <Full-Path-To-Trace>/trace.nettrace
  Session Id: <SessionId>
  Recording trace 721.025 (KB)
  ```

- <span data-ttu-id="00cca-173">Zatrzymaj zbieranie przez naciśnięcie `<Enter>` klawisza.</span><span class="sxs-lookup"><span data-stu-id="00cca-173">Stop collection by pressing the `<Enter>` key.</span></span> <span data-ttu-id="00cca-174">`dotnet-trace`spowoduje zakończenie rejestrowania zdarzeń w pliku *śledzenia.*</span><span class="sxs-lookup"><span data-stu-id="00cca-174">`dotnet-trace` will finish logging events to the *trace.nettrace* file.</span></span>

## <a name="launch-a-child-application-and-collect-a-trace-from-its-startup-using-dotnet-trace"></a><span data-ttu-id="00cca-175">Uruchamianie aplikacji podrzędnej i zbieranie śladów z uruchamiania przy użyciu programu dotnet-Trace</span><span class="sxs-lookup"><span data-stu-id="00cca-175">Launch a child application and collect a trace from its startup using dotnet-trace</span></span>

<span data-ttu-id="00cca-176">Uwaga: działa to w przypadku aplikacji z uruchomionym programem .NET 5,0 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="00cca-176">NOTE: This works for apps running .NET 5.0 or later only.</span></span>

<span data-ttu-id="00cca-177">Czasami przydatne może być zebranie śladu procesu od jego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="00cca-177">Sometimes it may be useful to collect a trace of a process from its startup.</span></span> <span data-ttu-id="00cca-178">W przypadku aplikacji, na których działa program .NET 5,0 lub nowszy, można to zrobić za pomocą funkcji śledzenia dotnet.</span><span class="sxs-lookup"><span data-stu-id="00cca-178">For apps running .NET 5.0 or later, it is possible to do this by using dotnet-trace.</span></span>

<span data-ttu-id="00cca-179">Spowoduje to uruchomienie `hello.exe` z `arg1` i `arg2` jako argumentów wiersza polecenia i zebranie śladu w czasie jego uruchamiania:</span><span class="sxs-lookup"><span data-stu-id="00cca-179">This will launch `hello.exe` with `arg1` and `arg2` as its command line arguments and collect a trace from its runtime startup:</span></span>

```console
dotnet-trace collect -- hello.exe arg1 arg2
```

<span data-ttu-id="00cca-180">Poprzednie polecenie generuje dane wyjściowe podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="00cca-180">The preceding command generates output similar to the following:</span></span>

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

<span data-ttu-id="00cca-181">Można zatrzymać zbieranie śladów przez naciśnięcie klawisza `<Enter>` lub `<Ctrl + C>` klawisza.</span><span class="sxs-lookup"><span data-stu-id="00cca-181">You can stop collecting the trace by pressing `<Enter>` or `<Ctrl + C>` key.</span></span> <span data-ttu-id="00cca-182">To spowoduje również wyjście `hello.exe` .</span><span class="sxs-lookup"><span data-stu-id="00cca-182">Doing this will also exit `hello.exe`.</span></span>

> [!NOTE]
> <span data-ttu-id="00cca-183">Uruchamianie `hello.exe` za pomocą programu dotnet-Trace spowoduje przekierowanie danych wejściowych/wyjściowych i nie będzie możliwe interakcje z jego stdin/stdout.</span><span class="sxs-lookup"><span data-stu-id="00cca-183">Launching `hello.exe` via dotnet-trace will make its input/output to be redirected and you won't be able to interact with its stdin/stdout.</span></span>
> <span data-ttu-id="00cca-184">Zamknięcie narzędzia za pośrednictwem kombinacji klawiszy CTRL + C lub SIGTERM spowoduje bezpieczne zakończenie zarówno narzędzia, jak i procesu podrzędnego.</span><span class="sxs-lookup"><span data-stu-id="00cca-184">Exiting the tool via CTRL+C or SIGTERM will safely end both the tool and the child process.</span></span>
> <span data-ttu-id="00cca-185">Jeśli proces podrzędny zostanie zakończony przed narzędziem, narzędzie zostanie również zakończone, a śledzenie powinno być bezpiecznie widoczne.</span><span class="sxs-lookup"><span data-stu-id="00cca-185">If the child process exits before the tool, the tool will exit as well and the trace should be safely viewable.</span></span>

## <a name="view-the-trace-captured-from-dotnet-trace"></a><span data-ttu-id="00cca-186">Wyświetl śledzenie przechwycone przez śledzenie dotnet</span><span class="sxs-lookup"><span data-stu-id="00cca-186">View the trace captured from dotnet-trace</span></span>

<span data-ttu-id="00cca-187">W systemie Windows można przeglądać pliki *śledzenia* w usłudze [Narzędzia PerfView](https://github.com/microsoft/perfview) for Analysis: w przypadku śladów zebranych na innych platformach plik śledzenia można przenieść na komputer z systemem Windows, który ma być wyświetlany na narzędzia PerfView.</span><span class="sxs-lookup"><span data-stu-id="00cca-187">On Windows, *.nettrace* files can be viewed on [PerfView](https://github.com/microsoft/perfview) for analysis: For traces collected on other platforms, the trace file can be moved to a Windows machine to be viewed on PerfView.</span></span>

<span data-ttu-id="00cca-188">W systemie Linux śledzenie można wyświetlić, zmieniając format danych wyjściowych `dotnet-trace` na `speedscope` .</span><span class="sxs-lookup"><span data-stu-id="00cca-188">On Linux, the trace can be viewed by changing the output format of `dotnet-trace` to `speedscope`.</span></span> <span data-ttu-id="00cca-189">Format pliku wyjściowego można zmienić przy użyciu `-f|--format` opcji — `-f speedscope` spowoduje `dotnet-trace` to utworzenie `speedscope` pliku.</span><span class="sxs-lookup"><span data-stu-id="00cca-189">The output file format can be changed using the `-f|--format` option - `-f speedscope` will make `dotnet-trace` produce a `speedscope` file.</span></span> <span data-ttu-id="00cca-190">Można wybrać opcję `nettrace` (opcja domyślna) i `speedscope` .</span><span class="sxs-lookup"><span data-stu-id="00cca-190">You can choose between `nettrace` (the default option) and `speedscope`.</span></span> <span data-ttu-id="00cca-191">`Speedscope` Pliki można otwierać w lokalizacji <https://www.speedscope.app> .</span><span class="sxs-lookup"><span data-stu-id="00cca-191">`Speedscope` files can be opened at <https://www.speedscope.app>.</span></span>

> [!NOTE]
> <span data-ttu-id="00cca-192">Środowisko uruchomieniowe programu .NET Core generuje ślady w `nettrace` formacie.</span><span class="sxs-lookup"><span data-stu-id="00cca-192">The .NET Core runtime generates traces in the `nettrace` format.</span></span> <span data-ttu-id="00cca-193">Ślady są konwertowane na speedscope (jeśli zostaną określone) po zakończeniu śledzenia.</span><span class="sxs-lookup"><span data-stu-id="00cca-193">The traces are converted to speedscope (if specified) after the trace is completed.</span></span> <span data-ttu-id="00cca-194">Ponieważ niektóre Konwersje mogą spowodować utratę danych, oryginalny `nettrace` plik zostanie zachowany obok skonwertowanego pliku.</span><span class="sxs-lookup"><span data-stu-id="00cca-194">Since some conversions may result in loss of data, the original `nettrace` file is preserved next to the converted file.</span></span>

## <a name="use-dotnet-trace-to-collect-counter-values-over-time"></a><span data-ttu-id="00cca-195">Używanie funkcji monitorowania dotnet do zbierania wartości licznika w czasie</span><span class="sxs-lookup"><span data-stu-id="00cca-195">Use dotnet-trace to collect counter values over time</span></span>

<span data-ttu-id="00cca-196">`dotnet-trace` może</span><span class="sxs-lookup"><span data-stu-id="00cca-196">`dotnet-trace` can:</span></span>

* <span data-ttu-id="00cca-197">Służy `EventCounter` do podstawowego monitorowania kondycji w środowiskach z uwzględnieniem wydajności.</span><span class="sxs-lookup"><span data-stu-id="00cca-197">Use `EventCounter` for basic health monitoring in performance-sensitive environments.</span></span> <span data-ttu-id="00cca-198">Na przykład w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="00cca-198">For example, in production.</span></span>
* <span data-ttu-id="00cca-199">Zbieraj ślady, aby nie trzeba było ich wyświetlać w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="00cca-199">Collect traces so they don't need to be viewed in real time.</span></span>

<span data-ttu-id="00cca-200">Na przykład, aby zbierać wartości liczników wydajności środowiska uruchomieniowego, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="00cca-200">For example, to collect runtime performance counter values, use the following command:</span></span>

```console
dotnet-trace collect --process-id <PID> --providers System.Runtime:0:1:EventCounterIntervalSec=1
```

<span data-ttu-id="00cca-201">Poprzednie polecenie instruuje liczniki środowiska uruchomieniowego do raportowania co sekundę w przypadku uproszczonego monitorowania kondycji.</span><span class="sxs-lookup"><span data-stu-id="00cca-201">The preceding command tells the runtime counters to report once every second for lightweight health monitoring.</span></span> <span data-ttu-id="00cca-202">Zastąpienie `EventCounterIntervalSec=1` o wyższej wartości (na przykład 60) umożliwia zbieranie mniejszych śladów o mniejszej szczegółowości danych licznika.</span><span class="sxs-lookup"><span data-stu-id="00cca-202">Replacing `EventCounterIntervalSec=1` with a higher value (for example, 60) allows collection of a smaller trace with less granularity in the counter data.</span></span>

<span data-ttu-id="00cca-203">Następujące polecenie zmniejsza obciążenie i rozmiar śladu więcej niż poprzedni:</span><span class="sxs-lookup"><span data-stu-id="00cca-203">The following command reduces overhead and trace size more than the preceding one:</span></span>

```console
dotnet-trace collect --process-id <PID> --providers System.Runtime:0:1:EventCounterIntervalSec=1,Microsoft-Windows-DotNETRuntime:0:1,Microsoft-DotNETCore-SampleProfiler:0:1
```

<span data-ttu-id="00cca-204">Poprzednie polecenie powoduje wyłączenie zdarzeń środowiska uruchomieniowego i zarządzanego profilera stosu.</span><span class="sxs-lookup"><span data-stu-id="00cca-204">The preceding command disables runtime events and the managed stack profiler.</span></span>

## <a name="net-providers"></a><span data-ttu-id="00cca-205">Dostawcy .NET</span><span class="sxs-lookup"><span data-stu-id="00cca-205">.NET Providers</span></span>

<span data-ttu-id="00cca-206">Środowisko uruchomieniowe platformy .NET Core obsługuje następujących dostawców platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="00cca-206">The .NET Core runtime supports the following .NET providers.</span></span> <span data-ttu-id="00cca-207">.NET Core używa tych samych słów kluczowych do włączenia obu `Event Tracing for Windows (ETW)` i `EventPipe` śladów.</span><span class="sxs-lookup"><span data-stu-id="00cca-207">.NET Core uses the same keywords to enable both `Event Tracing for Windows (ETW)` and `EventPipe` traces.</span></span>

| <span data-ttu-id="00cca-208">Nazwa dostawcy</span><span class="sxs-lookup"><span data-stu-id="00cca-208">Provider name</span></span>                            | <span data-ttu-id="00cca-209">Informacje</span><span class="sxs-lookup"><span data-stu-id="00cca-209">Information</span></span> |
|------------------------------------------|-------------|
| `Microsoft-Windows-DotNETRuntime`        | [<span data-ttu-id="00cca-210">Dostawca środowiska uruchomieniowego</span><span class="sxs-lookup"><span data-stu-id="00cca-210">The Runtime Provider</span></span>](../../framework/performance/clr-etw-providers.md#the-runtime-provider)<br>[<span data-ttu-id="00cca-211">Słowa kluczowe środowiska uruchomieniowego CLR</span><span class="sxs-lookup"><span data-stu-id="00cca-211">CLR Runtime Keywords</span></span>](../../framework/performance/clr-etw-keywords-and-levels.md#runtime) |
| `Microsoft-Windows-DotNETRuntimeRundown` | [<span data-ttu-id="00cca-212">Dostawca uwalniania</span><span class="sxs-lookup"><span data-stu-id="00cca-212">The Rundown Provider</span></span>](../../framework/performance/clr-etw-providers.md#the-rundown-provider)<br>[<span data-ttu-id="00cca-213">Słowa kluczowe uwalniania CLR</span><span class="sxs-lookup"><span data-stu-id="00cca-213">CLR Rundown Keywords</span></span>](../../framework/performance/clr-etw-keywords-and-levels.md#rundown) |
| `Microsoft-DotNETCore-SampleProfiler`    | <span data-ttu-id="00cca-214">Włącza przykładowy Profiler.</span><span class="sxs-lookup"><span data-stu-id="00cca-214">Enables the sample profiler.</span></span> |
