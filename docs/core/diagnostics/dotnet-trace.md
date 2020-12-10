---
title: dotnet-Trace — narzędzie diagnostyczne — interfejs wiersza polecenia platformy .NET
description: Dowiedz się, jak zainstalować i użyć narzędzia interfejsu wiersza polecenia śledzenia dotnet, aby zebrać ślady środowiska .NET działającego procesu bez natywnego profilera przy użyciu programu .NET EventPipe.
ms.date: 11/17/2020
ms.openlocfilehash: 868ce7828eee6bd7f2101d5d6a65c7f7bf87fe24
ms.sourcegitcommit: 81f1bba2c97a67b5ca76bcc57b37333ffca60c7b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/10/2020
ms.locfileid: "97009537"
---
# <a name="dotnet-trace-performance-analysis-utility"></a><span data-ttu-id="a189d-103">Narzędzie do analizy wydajności śledzenia dotnet</span><span class="sxs-lookup"><span data-stu-id="a189d-103">dotnet-trace performance analysis utility</span></span>

<span data-ttu-id="a189d-104">**Ten artykuł ma zastosowanie do:** ✔️ .net Core 3,0 SDK i nowszych wersjach</span><span class="sxs-lookup"><span data-stu-id="a189d-104">**This article applies to:** ✔️ .NET Core 3.0 SDK and later versions</span></span>

## <a name="install"></a><span data-ttu-id="a189d-105">Instalowanie</span><span class="sxs-lookup"><span data-stu-id="a189d-105">Install</span></span>

<span data-ttu-id="a189d-106">Istnieją dwa sposoby na pobranie i zainstalowanie `dotnet-trace` :</span><span class="sxs-lookup"><span data-stu-id="a189d-106">There are two ways to download and install `dotnet-trace`:</span></span>

- <span data-ttu-id="a189d-107">**Narzędzie globalne dotnet:**</span><span class="sxs-lookup"><span data-stu-id="a189d-107">**dotnet global tool:**</span></span>

  <span data-ttu-id="a189d-108">Aby zainstalować najnowszą wersję `dotnet-trace` [pakietu NuGet](https://www.nuget.org/packages/dotnet-trace), użyj polecenia [Narzędzia dotnet Install](../tools/dotnet-tool-install.md) :</span><span class="sxs-lookup"><span data-stu-id="a189d-108">To install the latest release version of the `dotnet-trace` [NuGet package](https://www.nuget.org/packages/dotnet-trace), use the [dotnet tool install](../tools/dotnet-tool-install.md) command:</span></span>

  ```dotnetcli
  dotnet tool install --global dotnet-trace
  ```

- <span data-ttu-id="a189d-109">**Pobieranie bezpośrednie:**</span><span class="sxs-lookup"><span data-stu-id="a189d-109">**Direct download:**</span></span>

  <span data-ttu-id="a189d-110">Pobierz plik wykonywalny narzędzia, który jest zgodny z platformą:</span><span class="sxs-lookup"><span data-stu-id="a189d-110">Download the tool executable that matches your platform:</span></span>

  | <span data-ttu-id="a189d-111">System operacyjny</span><span class="sxs-lookup"><span data-stu-id="a189d-111">OS</span></span>  | <span data-ttu-id="a189d-112">Platforma</span><span class="sxs-lookup"><span data-stu-id="a189d-112">Platform</span></span> |
  | --- | -------- |
  | <span data-ttu-id="a189d-113">Windows</span><span class="sxs-lookup"><span data-stu-id="a189d-113">Windows</span></span> | <span data-ttu-id="a189d-114">[x86](https://aka.ms/dotnet-trace/win-x86) \| [x64](https://aka.ms/dotnet-trace/win-x64) \| [ARM](https://aka.ms/dotnet-trace/win-arm) \| [ARM — x64](https://aka.ms/dotnet-trace/win-arm64)</span><span class="sxs-lookup"><span data-stu-id="a189d-114">[x86](https://aka.ms/dotnet-trace/win-x86) \| [x64](https://aka.ms/dotnet-trace/win-x64) \| [arm](https://aka.ms/dotnet-trace/win-arm) \| [arm-x64](https://aka.ms/dotnet-trace/win-arm64)</span></span> |
  | <span data-ttu-id="a189d-115">macOS</span><span class="sxs-lookup"><span data-stu-id="a189d-115">macOS</span></span>   | [<span data-ttu-id="a189d-116">x64</span><span class="sxs-lookup"><span data-stu-id="a189d-116">x64</span></span>](https://aka.ms/dotnet-trace/osx-x64) |
  | <span data-ttu-id="a189d-117">Linux</span><span class="sxs-lookup"><span data-stu-id="a189d-117">Linux</span></span>   | <span data-ttu-id="a189d-118">[x64](https://aka.ms/dotnet-trace/linux-x64) \| [ARM](https://aka.ms/dotnet-trace/linux-arm) \| [arm64](https://aka.ms/dotnet-trace/linux-arm64) \| [MUSL — x64](https://aka.ms/dotnet-trace/linux-musl-x64) \| [MUSL — arm64](https://aka.ms/dotnet-trace/linux-musl-arm64)</span><span class="sxs-lookup"><span data-stu-id="a189d-118">[x64](https://aka.ms/dotnet-trace/linux-x64) \| [arm](https://aka.ms/dotnet-trace/linux-arm) \| [arm64](https://aka.ms/dotnet-trace/linux-arm64) \| [musl-x64](https://aka.ms/dotnet-trace/linux-musl-x64) \| [musl-arm64](https://aka.ms/dotnet-trace/linux-musl-arm64)</span></span> |

## <a name="synopsis"></a><span data-ttu-id="a189d-119">Streszczenie</span><span class="sxs-lookup"><span data-stu-id="a189d-119">Synopsis</span></span>

```console
dotnet-trace [-h, --help] [--version] <command>
```

## <a name="description"></a><span data-ttu-id="a189d-120">Opis</span><span class="sxs-lookup"><span data-stu-id="a189d-120">Description</span></span>

<span data-ttu-id="a189d-121">`dotnet-trace`Narzędzie:</span><span class="sxs-lookup"><span data-stu-id="a189d-121">The `dotnet-trace` tool:</span></span>

* <span data-ttu-id="a189d-122">Program to międzyplatformowe narzędzie .NET Core.</span><span class="sxs-lookup"><span data-stu-id="a189d-122">Is a cross-platform .NET Core tool.</span></span>
* <span data-ttu-id="a189d-123">Włącza zbieranie śladów .NET Core działającego procesu bez natywnego profilera.</span><span class="sxs-lookup"><span data-stu-id="a189d-123">Enables the collection of .NET Core traces of a running process without a native profiler.</span></span>
* <span data-ttu-id="a189d-124">Jest wbudowana w [`EventPipe`](./eventpipe.md) środowisko uruchomieniowe platformy .NET Core.</span><span class="sxs-lookup"><span data-stu-id="a189d-124">Is built on [`EventPipe`](./eventpipe.md) of the .NET Core runtime.</span></span>
* <span data-ttu-id="a189d-125">Zapewnia takie samo środowisko w systemach Windows, Linux lub macOS.</span><span class="sxs-lookup"><span data-stu-id="a189d-125">Delivers the same experience on Windows, Linux, or macOS.</span></span>

## <a name="options"></a><span data-ttu-id="a189d-126">Opcje</span><span class="sxs-lookup"><span data-stu-id="a189d-126">Options</span></span>

- **`-h|--help`**

  <span data-ttu-id="a189d-127">Wyświetla pomoc w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="a189d-127">Shows command-line help.</span></span>

- **`--version`**

  <span data-ttu-id="a189d-128">Wyświetla wersję narzędzia do śledzenia dotnet.</span><span class="sxs-lookup"><span data-stu-id="a189d-128">Displays the version of the dotnet-trace utility.</span></span>

## <a name="commands"></a><span data-ttu-id="a189d-129">Polecenia</span><span class="sxs-lookup"><span data-stu-id="a189d-129">Commands</span></span>

| <span data-ttu-id="a189d-130">Polecenie</span><span class="sxs-lookup"><span data-stu-id="a189d-130">Command</span></span>                                                   |
|-----------------------------------------------------------|
| [<span data-ttu-id="a189d-131">zbieranie danych śledzenia dotnet</span><span class="sxs-lookup"><span data-stu-id="a189d-131">dotnet-trace collect</span></span>](#dotnet-trace-collect)             |
| [<span data-ttu-id="a189d-132">Konwersja dotnet-Trace</span><span class="sxs-lookup"><span data-stu-id="a189d-132">dotnet-trace convert</span></span>](#dotnet-trace-convert)             |
| [<span data-ttu-id="a189d-133">dotnet-Trace — śledzenie</span><span class="sxs-lookup"><span data-stu-id="a189d-133">dotnet-trace ps</span></span>](#dotnet-trace-ps)                       |
| [<span data-ttu-id="a189d-134">dotnet-lista śledzenia — profile</span><span class="sxs-lookup"><span data-stu-id="a189d-134">dotnet-trace list-profiles</span></span>](#dotnet-trace-list-profiles) |

## <a name="dotnet-trace-collect"></a><span data-ttu-id="a189d-135">zbieranie danych śledzenia dotnet</span><span class="sxs-lookup"><span data-stu-id="a189d-135">dotnet-trace collect</span></span>

<span data-ttu-id="a189d-136">Zbiera dane śledzenia diagnostycznego z uruchomionego procesu.</span><span class="sxs-lookup"><span data-stu-id="a189d-136">Collects a diagnostic trace from a running process.</span></span>

### <a name="synopsis"></a><span data-ttu-id="a189d-137">Streszczenie</span><span class="sxs-lookup"><span data-stu-id="a189d-137">Synopsis</span></span>

```console
dotnet-trace collect [--buffersize <size>] [--clreventlevel <clreventlevel>] [--clrevents <clrevents>]
    [--format <Chromium|NetTrace|Speedscope>] [-h|--help]
    [-n, --name <name>] [--diagnostic-port] [-o|--output <trace-file-path>] [-p|--process-id <pid>]
    [--profile <profile-name>] [--providers <list-of-comma-separated-providers>]
    [-- <command>] (for target applications running .NET 5.0 or later)
```

### <a name="options"></a><span data-ttu-id="a189d-138">Opcje</span><span class="sxs-lookup"><span data-stu-id="a189d-138">Options</span></span>

- **`--buffersize <size>`**

  <span data-ttu-id="a189d-139">Ustawia rozmiar buforu cyklicznego w pamięci (w megabajtach).</span><span class="sxs-lookup"><span data-stu-id="a189d-139">Sets the size of the in-memory circular buffer, in megabytes.</span></span> <span data-ttu-id="a189d-140">Wartość domyślna to 256 MB.</span><span class="sxs-lookup"><span data-stu-id="a189d-140">Default 256 MB.</span></span>

- **`--clreventlevel <clreventlevel>`**

  <span data-ttu-id="a189d-141">Poziom szczegółowości zdarzeń CLR do wyemitowania.</span><span class="sxs-lookup"><span data-stu-id="a189d-141">Verbosity of CLR events to be emitted.</span></span>

- **`--clrevents <clrevents>`**

  <span data-ttu-id="a189d-142">Lista zdarzeń środowiska uruchomieniowego CLR do emisji.</span><span class="sxs-lookup"><span data-stu-id="a189d-142">List of CLR runtime events to emit.</span></span>

- **`--format {Chromium|NetTrace|Speedscope}`**

  <span data-ttu-id="a189d-143">Ustawia format danych wyjściowych dla konwersji pliku śledzenia.</span><span class="sxs-lookup"><span data-stu-id="a189d-143">Sets the output format for the trace file conversion.</span></span> <span data-ttu-id="a189d-144">Wartość domyślna to `NetTrace`.</span><span class="sxs-lookup"><span data-stu-id="a189d-144">The default is `NetTrace`.</span></span>

- **`-n, --name <name>`**

  <span data-ttu-id="a189d-145">Nazwa procesu, z którego ma zostać zebrane śledzenie.</span><span class="sxs-lookup"><span data-stu-id="a189d-145">The name of the process to collect the trace from.</span></span>

- **`--diagnostic-port <path-to-port>`**

  <span data-ttu-id="a189d-146">Nazwa portu diagnostycznego do utworzenia.</span><span class="sxs-lookup"><span data-stu-id="a189d-146">The name of the diagnostic port to create.</span></span> <span data-ttu-id="a189d-147">Zobacz [Używanie portu diagnostycznego, aby zebrać ślad z uruchamiania aplikacji](#use-diagnostic-port-to-collect-a-trace-from-app-startup) , aby dowiedzieć się, jak za pomocą tej opcji zbierać dane śledzenia z uruchamiania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a189d-147">See [Use diagnostic port to collect a trace from app startup](#use-diagnostic-port-to-collect-a-trace-from-app-startup) to learn how to use this option to collect a trace from app startup.</span></span>

- **`-o|--output <trace-file-path>`**

  <span data-ttu-id="a189d-148">Ścieżka wyjściowa zebranych danych śledzenia.</span><span class="sxs-lookup"><span data-stu-id="a189d-148">The output path for the collected trace data.</span></span> <span data-ttu-id="a189d-149">Jeśli nie zostanie określony, jego wartość domyślna to `trace.nettrace` .</span><span class="sxs-lookup"><span data-stu-id="a189d-149">If not specified, it defaults to `trace.nettrace`.</span></span>

- **`-p|--process-id <PID>`**

  <span data-ttu-id="a189d-150">Identyfikator procesu, z którego ma zostać zebrane śledzenie.</span><span class="sxs-lookup"><span data-stu-id="a189d-150">The process ID to collect the trace from.</span></span>

- **`--profile <profile-name>`**

  <span data-ttu-id="a189d-151">Nazwany wstępnie zdefiniowany zestaw konfiguracji dostawcy, który umożliwia zwięzłe Określanie typowych scenariuszy śledzenia.</span><span class="sxs-lookup"><span data-stu-id="a189d-151">A named pre-defined set of provider configurations that allows common tracing scenarios to be specified succinctly.</span></span> <span data-ttu-id="a189d-152">Dostępne są następujące profile:</span><span class="sxs-lookup"><span data-stu-id="a189d-152">The following profiles are available:</span></span>

 | <span data-ttu-id="a189d-153">Profil</span><span class="sxs-lookup"><span data-stu-id="a189d-153">Profile</span></span> | <span data-ttu-id="a189d-154">Opis</span><span class="sxs-lookup"><span data-stu-id="a189d-154">Description</span></span> |
 |---------|-------------|
 |`cpu-sampling`|<span data-ttu-id="a189d-155">Przydatne do śledzenia użycia procesora i ogólnych informacji środowiska uruchomieniowego platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="a189d-155">Useful for tracking CPU usage and general .NET runtime information.</span></span> <span data-ttu-id="a189d-156">Jest to opcja domyślna, jeśli nie określono żadnego profilu ani dostawcy.</span><span class="sxs-lookup"><span data-stu-id="a189d-156">This is the default option if no profile or providers are specified.</span></span>|
 |`gc-verbose`|<span data-ttu-id="a189d-157">Śledzi kolekcje GC i przykłady alokacji obiektów.</span><span class="sxs-lookup"><span data-stu-id="a189d-157">Tracks GC collections and samples object allocations.</span></span>|
 |`gc-collect`|<span data-ttu-id="a189d-158">Śledzi kolekcje GC tylko przy niskim obciążeniu.</span><span class="sxs-lookup"><span data-stu-id="a189d-158">Tracks GC collections only at very low overhead.</span></span>|

- **`--providers <list-of-comma-separated-providers>`**

  <span data-ttu-id="a189d-159">Rozdzielana przecinkami lista `EventPipe` dostawców do włączenia.</span><span class="sxs-lookup"><span data-stu-id="a189d-159">A comma-separated list of `EventPipe` providers to be enabled.</span></span> <span data-ttu-id="a189d-160">Tacy dostawcy uzupełniają dostawców implikowaną przez `--profile <profile-name>` .</span><span class="sxs-lookup"><span data-stu-id="a189d-160">These providers supplement any providers implied by `--profile <profile-name>`.</span></span> <span data-ttu-id="a189d-161">W przypadku niespójności określonego dostawcy ta konfiguracja ma pierwszeństwo przed niejawną konfiguracją w profilu.</span><span class="sxs-lookup"><span data-stu-id="a189d-161">If there's any inconsistency for a particular provider, this configuration takes precedence over the implicit configuration from the profile.</span></span>

  <span data-ttu-id="a189d-162">Ta lista dostawców ma postać:</span><span class="sxs-lookup"><span data-stu-id="a189d-162">This list of providers is in the form:</span></span>

  - `Provider[,Provider]`
  - <span data-ttu-id="a189d-163">`Provider` ma postać: `KnownProviderName[:Flags[:Level][:KeyValueArgs]]` .</span><span class="sxs-lookup"><span data-stu-id="a189d-163">`Provider` is in the form: `KnownProviderName[:Flags[:Level][:KeyValueArgs]]`.</span></span>
  - <span data-ttu-id="a189d-164">`KeyValueArgs` ma postać: `[key1=value1][;key2=value2]` .</span><span class="sxs-lookup"><span data-stu-id="a189d-164">`KeyValueArgs` is in the form: `[key1=value1][;key2=value2]`.</span></span>

- <span data-ttu-id="a189d-165">**`-- <command>` (tylko w przypadku aplikacji docelowych z programem .NET 5,0)**</span><span class="sxs-lookup"><span data-stu-id="a189d-165">**`-- <command>` (for target applications running .NET 5.0 only)**</span></span>

  <span data-ttu-id="a189d-166">Po określeniu parametrów konfiguracji kolekcji użytkownik może dołączyć `--` po nim polecenie, aby uruchomić aplikację .NET z co najmniej 5,0 środowiskiem uruchomieniowym.</span><span class="sxs-lookup"><span data-stu-id="a189d-166">After the collection configuration parameters, the user can append `--` followed by a command to start a .NET application with at least a 5.0 runtime.</span></span> <span data-ttu-id="a189d-167">Może to być przydatne podczas diagnozowania problemów, które występują na wczesnym etapie procesu, takich jak problemy z wydajnością uruchamiania lub moduł ładujący zestawu i błędy spinacza.</span><span class="sxs-lookup"><span data-stu-id="a189d-167">This may be helpful when diagnosing issues that happen early in the process, such as startup performance issue or assembly loader and binder errors.</span></span>

  > [!NOTE]
  > <span data-ttu-id="a189d-168">Użycie tej opcji monitoruje pierwszy proces programu .NET 5,0, który komunikuje się z powrotem z narzędziem, co oznacza, że polecenie uruchamia wiele aplikacji .NET będzie zbierać tylko pierwszą aplikację.</span><span class="sxs-lookup"><span data-stu-id="a189d-168">Using this option monitors the first .NET 5.0 process that communicates back to the tool, which means if your command launches multiple .NET applications, it will only collect the first app.</span></span> <span data-ttu-id="a189d-169">W związku z tym zaleca się używanie tej opcji w aplikacjach samodzielnych lub przy użyciu `dotnet exec <app.dll>` opcji.</span><span class="sxs-lookup"><span data-stu-id="a189d-169">Therefore, it is recommended you use this option on self-contained applications, or using the `dotnet exec <app.dll>` option.</span></span>

## <a name="dotnet-trace-convert"></a><span data-ttu-id="a189d-170">Konwersja dotnet-Trace</span><span class="sxs-lookup"><span data-stu-id="a189d-170">dotnet-trace convert</span></span>

<span data-ttu-id="a189d-171">Konwertuje `nettrace` ślady na formaty alternatywne do użycia z alternatywnymi narzędziami do analizy śledzenia.</span><span class="sxs-lookup"><span data-stu-id="a189d-171">Converts `nettrace` traces to alternate formats for use with alternate trace analysis tools.</span></span>

### <a name="synopsis"></a><span data-ttu-id="a189d-172">Streszczenie</span><span class="sxs-lookup"><span data-stu-id="a189d-172">Synopsis</span></span>

```console
dotnet-trace convert [<input-filename>] [--format <Chromium|NetTrace|Speedscope>] [-h|--help] [-o|--output <output-filename>]
```

### <a name="arguments"></a><span data-ttu-id="a189d-173">Argumenty</span><span class="sxs-lookup"><span data-stu-id="a189d-173">Arguments</span></span>

- **`<input-filename>`**

  <span data-ttu-id="a189d-174">Wejściowy plik śledzenia do przekonwertowania.</span><span class="sxs-lookup"><span data-stu-id="a189d-174">Input trace file to be converted.</span></span> <span data-ttu-id="a189d-175">Wartość domyślna to *Trace. Trace*.</span><span class="sxs-lookup"><span data-stu-id="a189d-175">Defaults to *trace.nettrace*.</span></span>

### <a name="options"></a><span data-ttu-id="a189d-176">Opcje</span><span class="sxs-lookup"><span data-stu-id="a189d-176">Options</span></span>

- **`--format <Chromium|NetTrace|Speedscope>`**

  <span data-ttu-id="a189d-177">Ustawia format danych wyjściowych dla konwersji pliku śledzenia.</span><span class="sxs-lookup"><span data-stu-id="a189d-177">Sets the output format for the trace file conversion.</span></span>

- **`-o|--output <output-filename>`**

  <span data-ttu-id="a189d-178">Nazwa pliku wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="a189d-178">Output filename.</span></span> <span data-ttu-id="a189d-179">Rozszerzenie formatu docelowego zostanie dodane.</span><span class="sxs-lookup"><span data-stu-id="a189d-179">Extension of target format will be added.</span></span>

## <a name="dotnet-trace-ps"></a><span data-ttu-id="a189d-180">dotnet-Trace — śledzenie</span><span class="sxs-lookup"><span data-stu-id="a189d-180">dotnet-trace ps</span></span>

 <span data-ttu-id="a189d-181">Wyświetla listę procesów dotnet, z których można zbierać dane śledzenia.</span><span class="sxs-lookup"><span data-stu-id="a189d-181">Lists the dotnet processes that traces can be collected from.</span></span>

### <a name="synopsis"></a><span data-ttu-id="a189d-182">Streszczenie</span><span class="sxs-lookup"><span data-stu-id="a189d-182">Synopsis</span></span>

```console
dotnet-trace ps [-h|--help]
```

## <a name="dotnet-trace-list-profiles"></a><span data-ttu-id="a189d-183">dotnet-lista śledzenia — profile</span><span class="sxs-lookup"><span data-stu-id="a189d-183">dotnet-trace list-profiles</span></span>

<span data-ttu-id="a189d-184">Wyświetla wstępnie skompilowane profile śledzenia z opisem dostawców i filtrów w poszczególnych profilach.</span><span class="sxs-lookup"><span data-stu-id="a189d-184">Lists pre-built tracing profiles with a description of what providers and filters are in each profile.</span></span>

### <a name="synopsis"></a><span data-ttu-id="a189d-185">Streszczenie</span><span class="sxs-lookup"><span data-stu-id="a189d-185">Synopsis</span></span>

```console
dotnet-trace list-profiles [-h|--help]
```

## <a name="collect-a-trace-with-dotnet-trace"></a><span data-ttu-id="a189d-186">Zbieranie śledzenia przy użyciu funkcji monitorowania dotnet</span><span class="sxs-lookup"><span data-stu-id="a189d-186">Collect a trace with dotnet-trace</span></span>

<span data-ttu-id="a189d-187">Aby zebrać ślady przy użyciu `dotnet-trace` :</span><span class="sxs-lookup"><span data-stu-id="a189d-187">To collect traces using `dotnet-trace`:</span></span>

- <span data-ttu-id="a189d-188">Pobierz identyfikator procesu (PID) aplikacji .NET Core, aby zebrać ślady z programu.</span><span class="sxs-lookup"><span data-stu-id="a189d-188">Get the process identifier (PID) of the .NET Core application to collect traces from.</span></span>

  - <span data-ttu-id="a189d-189">W systemie Windows można użyć Menedżera zadań lub `tasklist` polecenia, na przykład.</span><span class="sxs-lookup"><span data-stu-id="a189d-189">On Windows, you can use Task Manager or the `tasklist` command, for example.</span></span>
  - <span data-ttu-id="a189d-190">Na przykład w systemie Linux `ps` polecenie.</span><span class="sxs-lookup"><span data-stu-id="a189d-190">On Linux, for example, the `ps` command.</span></span>
  - [<span data-ttu-id="a189d-191">dotnet-Trace — śledzenie</span><span class="sxs-lookup"><span data-stu-id="a189d-191">dotnet-trace ps</span></span>](#dotnet-trace-ps)

- <span data-ttu-id="a189d-192">Uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="a189d-192">Run the following command:</span></span>

  ```console
  dotnet-trace collect --process-id <PID>
  ```

  <span data-ttu-id="a189d-193">Poprzednie polecenie generuje dane wyjściowe podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="a189d-193">The preceding command generates output similar to the following:</span></span>

  ```console
  Press <Enter> to exit...
  Connecting to process: <Full-Path-To-Process-Being-Profiled>/dotnet.exe
  Collecting to file: <Full-Path-To-Trace>/trace.nettrace
  Session Id: <SessionId>
  Recording trace 721.025 (KB)
  ```

- <span data-ttu-id="a189d-194">Zatrzymaj zbieranie przez naciśnięcie `<Enter>` klawisza.</span><span class="sxs-lookup"><span data-stu-id="a189d-194">Stop collection by pressing the `<Enter>` key.</span></span> <span data-ttu-id="a189d-195">`dotnet-trace`spowoduje zakończenie rejestrowania zdarzeń w pliku *śledzenia.*</span><span class="sxs-lookup"><span data-stu-id="a189d-195">`dotnet-trace` will finish logging events to the *trace.nettrace* file.</span></span>

## <a name="launch-a-child-application-and-collect-a-trace-from-its-startup-using-dotnet-trace"></a><span data-ttu-id="a189d-196">Uruchamianie aplikacji podrzędnej i zbieranie śladów z uruchamiania przy użyciu programu dotnet-Trace</span><span class="sxs-lookup"><span data-stu-id="a189d-196">Launch a child application and collect a trace from its startup using dotnet-trace</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a189d-197">Działa to w przypadku aplikacji z uruchomionym programem .NET 5,0 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="a189d-197">This works for apps running .NET 5.0 or later only.</span></span>

<span data-ttu-id="a189d-198">Czasami przydatne może być zebranie śladu procesu od jego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="a189d-198">Sometimes it may be useful to collect a trace of a process from its startup.</span></span> <span data-ttu-id="a189d-199">W przypadku aplikacji, na których działa program .NET 5,0 lub nowszy, można to zrobić za pomocą funkcji śledzenia dotnet.</span><span class="sxs-lookup"><span data-stu-id="a189d-199">For apps running .NET 5.0 or later, it is possible to do this by using dotnet-trace.</span></span>

<span data-ttu-id="a189d-200">Spowoduje to uruchomienie `hello.exe` z `arg1` i `arg2` jako argumentów wiersza polecenia i zebranie śladu w czasie jego uruchamiania:</span><span class="sxs-lookup"><span data-stu-id="a189d-200">This will launch `hello.exe` with `arg1` and `arg2` as its command-line arguments and collect a trace from its runtime startup:</span></span>

```console
dotnet-trace collect -- hello.exe arg1 arg2
```

<span data-ttu-id="a189d-201">Poprzednie polecenie generuje dane wyjściowe podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="a189d-201">The preceding command generates output similar to the following:</span></span>

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

<span data-ttu-id="a189d-202">Można zatrzymać zbieranie śladów przez naciśnięcie klawisza `<Enter>` lub `<Ctrl + C>` klawisza.</span><span class="sxs-lookup"><span data-stu-id="a189d-202">You can stop collecting the trace by pressing `<Enter>` or `<Ctrl + C>` key.</span></span> <span data-ttu-id="a189d-203">To spowoduje również wyjście `hello.exe` .</span><span class="sxs-lookup"><span data-stu-id="a189d-203">Doing this will also exit `hello.exe`.</span></span>

> [!NOTE]
> <span data-ttu-id="a189d-204">Uruchamianie `hello.exe` za pomocą programu dotnet-Trace spowoduje przekierowanie danych wejściowych/wyjściowych i nie będzie możliwe interakcje z jego stdin/stdout.</span><span class="sxs-lookup"><span data-stu-id="a189d-204">Launching `hello.exe` via dotnet-trace will make its input/output to be redirected and you won't be able to interact with its stdin/stdout.</span></span>
> <span data-ttu-id="a189d-205">Zamknięcie narzędzia za pośrednictwem kombinacji klawiszy CTRL + C lub SIGTERM spowoduje bezpieczne zakończenie zarówno narzędzia, jak i procesu podrzędnego.</span><span class="sxs-lookup"><span data-stu-id="a189d-205">Exiting the tool via CTRL+C or SIGTERM will safely end both the tool and the child process.</span></span>
> <span data-ttu-id="a189d-206">Jeśli proces podrzędny zostanie zakończony przed narzędziem, narzędzie zostanie również zakończone, a śledzenie powinno być bezpiecznie widoczne.</span><span class="sxs-lookup"><span data-stu-id="a189d-206">If the child process exits before the tool, the tool will exit as well and the trace should be safely viewable.</span></span>

## <a name="use-diagnostic-port-to-collect-a-trace-from-app-startup"></a><span data-ttu-id="a189d-207">Użyj portu diagnostycznego, aby zebrać ślad z uruchamiania aplikacji</span><span class="sxs-lookup"><span data-stu-id="a189d-207">Use diagnostic port to collect a trace from app startup</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="a189d-208">Działa to w przypadku aplikacji z uruchomionym programem .NET 5,0 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="a189d-208">This works for apps running .NET 5.0 or later only.</span></span>

<span data-ttu-id="a189d-209">Port diagnostyczny to nowa funkcja środowiska uruchomieniowego, która została dodana w programie .NET 5, która umożliwia uruchamianie śledzenia przy uruchamianiu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a189d-209">Diagnostic port is a new runtime feature that was added in .NET 5 that allows you to start tracing from app startup.</span></span> <span data-ttu-id="a189d-210">W tym celu `dotnet-trace` można użyć polecenia `dotnet-trace collect -- <command>` zgodnie z opisem w powyższych przykładach lub użyć `--diagnostic-port` opcji.</span><span class="sxs-lookup"><span data-stu-id="a189d-210">To do this using `dotnet-trace`, you can either use `dotnet-trace collect -- <command>` as described in the examples above, or use the `--diagnostic-port` option.</span></span>

<span data-ttu-id="a189d-211">Używanie `dotnet-trace <collect|monitor> -- <command>` do uruchamiania aplikacji jako procesu podrzędnego jest najprostszym sposobem na szybkie śledzenie go od jego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="a189d-211">Using `dotnet-trace <collect|monitor> -- <command>` to launch the application as a child process is the simplest way to quickly trace it from its startup.</span></span>

<span data-ttu-id="a189d-212">Jeśli jednak chcesz uzyskać dokładniejszą kontrolę nad okresem istnienia śledzonej aplikacji (na przykład monitorować aplikację tylko przez pierwsze 10 minut i kontynuować) lub jeśli chcesz korzystać z aplikacji przy użyciu interfejsu wiersza polecenia, użycie `--diagnostic-port` opcji pozwala kontrolować zarówno monitorowaną aplikację docelową, jak i `dotnet-trace` .</span><span class="sxs-lookup"><span data-stu-id="a189d-212">However, when you want to gain a finer control over the lifetime of the app being traced (for example, monitor the app for the first 10 minutes only and continue executing) or if you need to interact with the app using the CLI, using `--diagnostic-port` option allows you to control both the target app being monitored and `dotnet-trace`.</span></span>

1. <span data-ttu-id="a189d-213">Poniższe polecenie tworzy `dotnet-trace` gniazdo diagnostyczne o nazwie `myport.sock` i poczekaj na połączenie.</span><span class="sxs-lookup"><span data-stu-id="a189d-213">The command below makes `dotnet-trace` create a diagnostics socket named `myport.sock` and wait for a connection.</span></span>

    > ```dotnet-cli
    > dotnet-trace collect --diagnostic-port myport.sock
    > ```

    <span data-ttu-id="a189d-214">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="a189d-214">Output:</span></span>

    > ```bash
    > Waiting for connection on myport.sock
    > Start an application with the following environment variable: DOTNET_DiagnosticPorts=/home/user/myport.sock
    > ```

2. <span data-ttu-id="a189d-215">W osobnej konsoli Uruchom aplikację docelową ze zmienną środowiskową `DOTNET_DiagnosticPorts` ustawioną na wartość w `dotnet-trace` danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="a189d-215">In a separate console, launch the target application with the environment variable `DOTNET_DiagnosticPorts` set to the value in the `dotnet-trace` output.</span></span>

    > ```bash
    > export DOTNET_DiagnosticPorts=/home/user/myport.sock
    > ./my-dotnet-app arg1 arg2
    > ```

    <span data-ttu-id="a189d-216">Powinno to następnie umożliwić `dotnet-trace` rozpoczęcie śledzenia `my-dotnet-app` :</span><span class="sxs-lookup"><span data-stu-id="a189d-216">This should then enable `dotnet-trace` to start tracing `my-dotnet-app`:</span></span>

    > ```bash
    > Waiting for connection on myport.sock
    > Start an application with the following environment variable: DOTNET_DiagnosticPorts=myport.sock
    > Starting a counter session. Press Q to quit.
    > ```

    > [!IMPORTANT]
    > <span data-ttu-id="a189d-217">Uruchamianie aplikacji w programie `dotnet run` może być problematyczne, ponieważ interfejs wiersza polecenia dotnet może mieć wiele procesów podrzędnych, które nie są używane przez aplikację, i mogą nawiązywać połączenie `dotnet-trace` przed aplikacją, pozostawiając, że aplikacja zostanie zawieszona w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="a189d-217">Launching your app with `dotnet run` can be problematic because the dotnet CLI may spawn many child processes that are not your app and they can connect to `dotnet-trace` before your app, leaving your app to be suspended at runtime.</span></span> <span data-ttu-id="a189d-218">Zaleca się, aby bezpośrednio korzystać z samodzielnej wersji aplikacji lub użyć `dotnet exec` do uruchomienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a189d-218">It is recommended you directly use a self-contained version of the app or use `dotnet exec` to launch the application.</span></span>

## <a name="view-the-trace-captured-from-dotnet-trace"></a><span data-ttu-id="a189d-219">Wyświetl śledzenie przechwycone przez śledzenie dotnet</span><span class="sxs-lookup"><span data-stu-id="a189d-219">View the trace captured from dotnet-trace</span></span>

<span data-ttu-id="a189d-220">W systemie Windows można przeglądać pliki *śledzenia* w usłudze [Narzędzia PerfView](https://github.com/microsoft/perfview) for Analysis: w przypadku śladów zebranych na innych platformach plik śledzenia można przenieść na komputer z systemem Windows, który ma być wyświetlany na narzędzia PerfView.</span><span class="sxs-lookup"><span data-stu-id="a189d-220">On Windows, *.nettrace* files can be viewed on [PerfView](https://github.com/microsoft/perfview) for analysis: For traces collected on other platforms, the trace file can be moved to a Windows machine to be viewed on PerfView.</span></span>

<span data-ttu-id="a189d-221">W systemie Linux śledzenie można wyświetlić, zmieniając format danych wyjściowych `dotnet-trace` na `speedscope` .</span><span class="sxs-lookup"><span data-stu-id="a189d-221">On Linux, the trace can be viewed by changing the output format of `dotnet-trace` to `speedscope`.</span></span> <span data-ttu-id="a189d-222">Format pliku wyjściowego można zmienić przy użyciu `-f|--format` opcji — `-f speedscope` spowoduje `dotnet-trace` to utworzenie `speedscope` pliku.</span><span class="sxs-lookup"><span data-stu-id="a189d-222">The output file format can be changed using the `-f|--format` option - `-f speedscope` will make `dotnet-trace` produce a `speedscope` file.</span></span> <span data-ttu-id="a189d-223">Można wybrać opcję `nettrace` (opcja domyślna) i `speedscope` .</span><span class="sxs-lookup"><span data-stu-id="a189d-223">You can choose between `nettrace` (the default option) and `speedscope`.</span></span> <span data-ttu-id="a189d-224">`Speedscope` Pliki można otwierać w lokalizacji <https://www.speedscope.app> .</span><span class="sxs-lookup"><span data-stu-id="a189d-224">`Speedscope` files can be opened at <https://www.speedscope.app>.</span></span>

> [!NOTE]
> <span data-ttu-id="a189d-225">Środowisko uruchomieniowe programu .NET Core generuje ślady w `nettrace` formacie.</span><span class="sxs-lookup"><span data-stu-id="a189d-225">The .NET Core runtime generates traces in the `nettrace` format.</span></span> <span data-ttu-id="a189d-226">Ślady są konwertowane na speedscope (jeśli zostaną określone) po zakończeniu śledzenia.</span><span class="sxs-lookup"><span data-stu-id="a189d-226">The traces are converted to speedscope (if specified) after the trace is completed.</span></span> <span data-ttu-id="a189d-227">Ponieważ niektóre Konwersje mogą spowodować utratę danych, oryginalny `nettrace` plik zostanie zachowany obok skonwertowanego pliku.</span><span class="sxs-lookup"><span data-stu-id="a189d-227">Since some conversions may result in loss of data, the original `nettrace` file is preserved next to the converted file.</span></span>

## <a name="use-dotnet-trace-to-collect-counter-values-over-time"></a><span data-ttu-id="a189d-228">Używanie funkcji monitorowania dotnet do zbierania wartości licznika w czasie</span><span class="sxs-lookup"><span data-stu-id="a189d-228">Use dotnet-trace to collect counter values over time</span></span>

<span data-ttu-id="a189d-229">`dotnet-trace` może</span><span class="sxs-lookup"><span data-stu-id="a189d-229">`dotnet-trace` can:</span></span>

* <span data-ttu-id="a189d-230">Służy `EventCounter` do podstawowego monitorowania kondycji w środowiskach z uwzględnieniem wydajności.</span><span class="sxs-lookup"><span data-stu-id="a189d-230">Use `EventCounter` for basic health monitoring in performance-sensitive environments.</span></span> <span data-ttu-id="a189d-231">Na przykład w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="a189d-231">For example, in production.</span></span>
* <span data-ttu-id="a189d-232">Zbieraj ślady, aby nie trzeba było ich wyświetlać w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="a189d-232">Collect traces so they don't need to be viewed in real time.</span></span>

<span data-ttu-id="a189d-233">Na przykład, aby zbierać wartości liczników wydajności środowiska uruchomieniowego, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="a189d-233">For example, to collect runtime performance counter values, use the following command:</span></span>

```console
dotnet-trace collect --process-id <PID> --providers System.Runtime:0:1:EventCounterIntervalSec=1
```

<span data-ttu-id="a189d-234">Poprzednie polecenie instruuje liczniki środowiska uruchomieniowego do raportowania co sekundę w przypadku uproszczonego monitorowania kondycji.</span><span class="sxs-lookup"><span data-stu-id="a189d-234">The preceding command tells the runtime counters to report once every second for lightweight health monitoring.</span></span> <span data-ttu-id="a189d-235">Zastąpienie `EventCounterIntervalSec=1` o wyższej wartości (na przykład 60) umożliwia zbieranie mniejszych śladów o mniejszej szczegółowości danych licznika.</span><span class="sxs-lookup"><span data-stu-id="a189d-235">Replacing `EventCounterIntervalSec=1` with a higher value (for example, 60) allows collection of a smaller trace with less granularity in the counter data.</span></span>

<span data-ttu-id="a189d-236">Następujące polecenie zmniejsza obciążenie i rozmiar śladu więcej niż poprzedni:</span><span class="sxs-lookup"><span data-stu-id="a189d-236">The following command reduces overhead and trace size more than the preceding one:</span></span>

```console
dotnet-trace collect --process-id <PID> --providers System.Runtime:0:1:EventCounterIntervalSec=1,Microsoft-Windows-DotNETRuntime:0:1,Microsoft-DotNETCore-SampleProfiler:0:1
```

<span data-ttu-id="a189d-237">Poprzednie polecenie powoduje wyłączenie zdarzeń środowiska uruchomieniowego i zarządzanego profilera stosu.</span><span class="sxs-lookup"><span data-stu-id="a189d-237">The preceding command disables runtime events and the managed stack profiler.</span></span>

## <a name="net-providers"></a><span data-ttu-id="a189d-238">Dostawcy .NET</span><span class="sxs-lookup"><span data-stu-id="a189d-238">.NET Providers</span></span>

<span data-ttu-id="a189d-239">Środowisko uruchomieniowe platformy .NET Core obsługuje następujących dostawców platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="a189d-239">The .NET Core runtime supports the following .NET providers.</span></span> <span data-ttu-id="a189d-240">.NET Core używa tych samych słów kluczowych do włączenia obu `Event Tracing for Windows (ETW)` i `EventPipe` śladów.</span><span class="sxs-lookup"><span data-stu-id="a189d-240">.NET Core uses the same keywords to enable both `Event Tracing for Windows (ETW)` and `EventPipe` traces.</span></span>

| <span data-ttu-id="a189d-241">Nazwa dostawcy</span><span class="sxs-lookup"><span data-stu-id="a189d-241">Provider name</span></span>                            | <span data-ttu-id="a189d-242">Informacje</span><span class="sxs-lookup"><span data-stu-id="a189d-242">Information</span></span> |
|------------------------------------------|-------------|
| `Microsoft-Windows-DotNETRuntime`        | [<span data-ttu-id="a189d-243">Dostawca środowiska uruchomieniowego</span><span class="sxs-lookup"><span data-stu-id="a189d-243">The Runtime Provider</span></span>](../../framework/performance/clr-etw-providers.md#the-runtime-provider)<br>[<span data-ttu-id="a189d-244">Słowa kluczowe środowiska uruchomieniowego CLR</span><span class="sxs-lookup"><span data-stu-id="a189d-244">CLR Runtime Keywords</span></span>](../../framework/performance/clr-etw-keywords-and-levels.md#runtime) |
| `Microsoft-Windows-DotNETRuntimeRundown` | [<span data-ttu-id="a189d-245">Dostawca uwalniania</span><span class="sxs-lookup"><span data-stu-id="a189d-245">The Rundown Provider</span></span>](../../framework/performance/clr-etw-providers.md#the-rundown-provider)<br>[<span data-ttu-id="a189d-246">Słowa kluczowe uwalniania CLR</span><span class="sxs-lookup"><span data-stu-id="a189d-246">CLR Rundown Keywords</span></span>](../../framework/performance/clr-etw-keywords-and-levels.md#rundown) |
| `Microsoft-DotNETCore-SampleProfiler`    | <span data-ttu-id="a189d-247">Włącza przykładowy Profiler.</span><span class="sxs-lookup"><span data-stu-id="a189d-247">Enables the sample profiler.</span></span> |
