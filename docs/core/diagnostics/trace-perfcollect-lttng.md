---
title: Śledzenie aplikacji .NET za pomocą PerfCollect.
description: Samouczek, który przeprowadzi Cię przez zbieranie śladów z perfcollect na platformie .NET.
ms.topic: tutorial
ms.date: 10/23/2020
ms.openlocfilehash: 53e4584953d2af4e766daadfa757cca752ae7329
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/16/2020
ms.locfileid: "97593223"
---
# <a name="trace-net-applications-with-perfcollect"></a><span data-ttu-id="5cd12-103">Śledzenie aplikacji .NET za pomocą PerfCollect</span><span class="sxs-lookup"><span data-stu-id="5cd12-103">Trace .NET applications with PerfCollect</span></span>

<span data-ttu-id="5cd12-104">**Ten artykuł ma zastosowanie do: ✔️** .net Core 2,1 SDK i nowszych wersjach</span><span class="sxs-lookup"><span data-stu-id="5cd12-104">**This article applies to: ✔️** .NET Core 2.1 SDK and later versions</span></span>

<span data-ttu-id="5cd12-105">W przypadku wystąpienia problemów z wydajnością w systemie Linux zbieranie danych śledzenia za pomocą `perfcollect` może służyć do zbierania szczegółowych informacji na temat tego, co się dzieje na komputerze w momencie problemu z wydajnością.</span><span class="sxs-lookup"><span data-stu-id="5cd12-105">When performance problems are encountered on Linux, collecting a trace with `perfcollect` can be used to gather detailed information about what was happening on the machine at the time of the performance problem.</span></span>

<span data-ttu-id="5cd12-106">`perfcollect` to skrypt bash, który wykorzystuje [generowanie śledzenia Tookit-Next systemu Linux (LTTng)](https://lttng.org) do zbierania zdarzeń utworzonych na podstawie środowiska uruchomieniowego lub dowolnego elementu [EventSource](xref:System.Diagnostics.Tracing.EventListener), a także [wydajności](https://perf.wiki.kernel.org/) do zbierania próbek procesora CPU procesu docelowego.</span><span class="sxs-lookup"><span data-stu-id="5cd12-106">`perfcollect` is a bash script that leverages [Linux Tracing Tookit-Next Generation (LTTng)](https://lttng.org) to collect events written from the runtime or any [EventSource](xref:System.Diagnostics.Tracing.EventListener), as well as [perf](https://perf.wiki.kernel.org/) to collect CPU samples of the target process.</span></span>

## <a name="prepare-your-machine"></a><span data-ttu-id="5cd12-107">Przygotuj maszynę</span><span class="sxs-lookup"><span data-stu-id="5cd12-107">Prepare your machine</span></span>

<span data-ttu-id="5cd12-108">Wykonaj następujące kroki, aby przygotować komputer do zbierania danych śledzenia wydajności za pomocą programu `perfcollect` .</span><span class="sxs-lookup"><span data-stu-id="5cd12-108">Follow these steps to prepare your machine to collect a performance trace with `perfcollect`.</span></span>

> [!NOTE]
> <span data-ttu-id="5cd12-109">Jeśli jesteś w środowisku kontenera, kontener musi mieć `SYS_ADMIN` możliwość.</span><span class="sxs-lookup"><span data-stu-id="5cd12-109">If you are in a container environment, your container needs to have `SYS_ADMIN` capability.</span></span> <span data-ttu-id="5cd12-110">Aby uzyskać więcej informacji na temat śledzenia aplikacji wewnątrz kontenerów za pomocą PerfCollect, zobacz [zbieranie danych diagnostycznych w kontenerach](./diagnostics-in-containers.md).</span><span class="sxs-lookup"><span data-stu-id="5cd12-110">For more information on tracing applications inside containers using PerfCollect, see [Collect diagnostics in containers](./diagnostics-in-containers.md).</span></span>

1. <span data-ttu-id="5cd12-111">Pobierz `perfcollect` .</span><span class="sxs-lookup"><span data-stu-id="5cd12-111">Download `perfcollect`.</span></span>

    > ```bash
    > curl -OL https://aka.ms/perfcollect
    > ```

2. <span data-ttu-id="5cd12-112">Utwórz plik wykonywalny skryptu.</span><span class="sxs-lookup"><span data-stu-id="5cd12-112">Make the script executable.</span></span>

    > ```bash
    > chmod +x perfcollect
    > ```

3. <span data-ttu-id="5cd12-113">Wymagania wstępne dotyczące śledzenia instalacji — są to rzeczywiste biblioteki śledzenia.</span><span class="sxs-lookup"><span data-stu-id="5cd12-113">Install tracing prerequisites - these are the actual tracing libraries.</span></span>

    > ```bash
    > sudo ./perfcollect install
    > ```

    <span data-ttu-id="5cd12-114">Spowoduje to zainstalowanie następujących warunków wstępnych na maszynie:</span><span class="sxs-lookup"><span data-stu-id="5cd12-114">This will install the following prerequisites on your machine:</span></span>

    1. <span data-ttu-id="5cd12-115">`perf`: podsystem zdarzeń wydajności systemu Linux oraz aplikacja do zbierania/przeglądania w trybie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5cd12-115">`perf`: the Linux Performance Events subsystem and companion user-mode collection/viewer application.</span></span> <span data-ttu-id="5cd12-116">`perf` jest częścią źródła jądra systemu Linux, ale zazwyczaj nie jest instalowany domyślnie.</span><span class="sxs-lookup"><span data-stu-id="5cd12-116">`perf` is part of the Linux kernel source, but is not usually installed by default.</span></span>

    2. <span data-ttu-id="5cd12-117">`LTTng`: Służy do przechwytywania danych zdarzeń emitowanych w czasie wykonywania przez CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="5cd12-117">`LTTng`: Used to capture event data emitted at runtime by CoreCLR.</span></span> <span data-ttu-id="5cd12-118">Te dane są następnie używane do analizowania zachowania różnych składników środowiska uruchomieniowego, takich jak GC, JIT i Pula wątków.</span><span class="sxs-lookup"><span data-stu-id="5cd12-118">This data is then used to analyze the behavior of various runtime components such as the GC, JIT, and thread pool.</span></span>

<span data-ttu-id="5cd12-119">Najnowsze wersje programu .NET Core i narzędzie wydajności systemu Linux obsługują automatyczne rozpoznawanie nazw metod dla kodu struktury.</span><span class="sxs-lookup"><span data-stu-id="5cd12-119">Recent versions of .NET Core and the Linux perf tool support automatic resolution of method names for framework code.</span></span> <span data-ttu-id="5cd12-120">Jeśli pracujesz z platformą .NET Core w wersji 3,1 lub mniejszej, konieczny jest dodatkowy krok.</span><span class="sxs-lookup"><span data-stu-id="5cd12-120">If you are working with .NET Core version 3.1 or less, an extra step is necessary.</span></span> <span data-ttu-id="5cd12-121">Aby uzyskać szczegółowe informacje, zobacz [Rozpoznawanie symboli struktury](#resolve-framework-symbols) .</span><span class="sxs-lookup"><span data-stu-id="5cd12-121">See [Resolving Framework Symbols](#resolve-framework-symbols) for details.</span></span>

<span data-ttu-id="5cd12-122">W przypadku rozpoznawania nazw metod natywnych bibliotek DLL środowiska uruchomieniowego (takich jak libcoreclr.so) program `perfcollect` rozpozna symbole dla nich podczas konwertowania danych, ale tylko wtedy, gdy są obecne symbole dla tych plików binarnych.</span><span class="sxs-lookup"><span data-stu-id="5cd12-122">For resolving method names of native runtime DLLs (such as libcoreclr.so), `perfcollect` will resolve symbols for them when it converts the data, but only if the symbols for these binaries are present.</span></span> <span data-ttu-id="5cd12-123">Aby uzyskać szczegółowe informacje, zobacz sekcję [pobieranie symboli dla natywnego środowiska uruchomieniowego](#get-symbols-for-the-native-runtime) .</span><span class="sxs-lookup"><span data-stu-id="5cd12-123">See [Getting Symbols for the Native Runtime](#get-symbols-for-the-native-runtime) section for details.</span></span>

## <a name="collect-a-trace"></a><span data-ttu-id="5cd12-124">Zbieranie śladu</span><span class="sxs-lookup"><span data-stu-id="5cd12-124">Collect a trace</span></span>

1. <span data-ttu-id="5cd12-125">Dostępne są dwie powłoki — jeden do sterowania śledzeniem, zwany jako **[Trace]**, i jeden do uruchamiania aplikacji, zwany jako **[app]**.</span><span class="sxs-lookup"><span data-stu-id="5cd12-125">Have two shells available - one for controlling tracing, referred to as **[Trace]**, and one for running the application, referred to as **[App]**.</span></span>

2. <span data-ttu-id="5cd12-126">**[Trace]** Rozpocznij zbieranie danych.</span><span class="sxs-lookup"><span data-stu-id="5cd12-126">**[Trace]** Start collection.</span></span>

    > ```bash
    > sudo ./perfcollect collect sampleTrace
    > ```

    <span data-ttu-id="5cd12-127">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="5cd12-127">Expected Output:</span></span>

    > ```bash
    > Collection started.  Press CTRL+C to stop.
    > ```

3. <span data-ttu-id="5cd12-128">**[Aplikacja]** Skonfiguruj powłokę aplikacji z następującymi zmiennymi środowiskowymi — umożliwia to konfigurację śledzenia CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="5cd12-128">**[App]** Set up the application shell with the following environment variables - this enables tracing configuration of CoreCLR.</span></span>

    > ```bash
    > export COMPlus_PerfMapEnabled=1
    > export COMPlus_EnableEventLog=1
    > ```

4. <span data-ttu-id="5cd12-129">**[Aplikacja]** Uruchom aplikację — niech działa tak długo, jak w celu przechwycenia problemu z wydajnością.</span><span class="sxs-lookup"><span data-stu-id="5cd12-129">**[App]** Run the app - let it run as long as you need to in order to capture the performance problem.</span></span> <span data-ttu-id="5cd12-130">Dokładna długość może być tak mała, jak jest to konieczne, tak długo, jak przechwytuje okno czasu, w którym występuje problem z wydajnością.</span><span class="sxs-lookup"><span data-stu-id="5cd12-130">The exact length can be as short as you need as long as it sufficiently captures the window of time where the performance problem you want to investigate occurs.</span></span>

    > ```bash
    > dotnet run
    > ```

5. <span data-ttu-id="5cd12-131">**[Trace]** Zatrzymaj zbieranie — naciśnij klawisze CTRL + C.</span><span class="sxs-lookup"><span data-stu-id="5cd12-131">**[Trace]** Stop collection - hit CTRL+C.</span></span>

    > ```bash
    > ^C
    > ...STOPPED.
    >
    > Starting post-processing. This may take some time.
    >
    > Generating native image symbol files
    > ...SKIPPED
    > Saving native symbols
    > ...FINISHED
    > Exporting perf.data file
    > ...FINISHED
    > Compressing trace files
    > ...FINISHED
    > Cleaning up artifacts
    > ...FINISHED
    >
    > Trace saved to sampleTrace.trace.zip
    > ```

    <span data-ttu-id="5cd12-132">Skompresowany plik śledzenia jest teraz przechowywany w bieżącym katalogu roboczym.</span><span class="sxs-lookup"><span data-stu-id="5cd12-132">The compressed trace file is now stored in the current working directory.</span></span>

## <a name="view-a-trace"></a><span data-ttu-id="5cd12-133">Wyświetlanie śladu</span><span class="sxs-lookup"><span data-stu-id="5cd12-133">View a trace</span></span>

<span data-ttu-id="5cd12-134">Istnieje kilka opcji wyświetlania śladu, który został zebrany.</span><span class="sxs-lookup"><span data-stu-id="5cd12-134">There are a number of options for viewing the trace that was collected.</span></span> <span data-ttu-id="5cd12-135">Ślady są najlepiej oglądane przy użyciu [Narzędzia PerfView](https://aka.ms/perfview) w systemie Windows, ale mogą być wyświetlane bezpośrednio w systemie Linux przy użyciu `PerfCollect` samego siebie lub `TraceCompass` .</span><span class="sxs-lookup"><span data-stu-id="5cd12-135">Traces are best viewed using [PerfView](https://aka.ms/perfview) on Windows, but they can be viewed directly on Linux using `PerfCollect` itself or `TraceCompass`.</span></span>

### <a name="use-perfcollect-to-view-the-trace-file"></a><span data-ttu-id="5cd12-136">Użyj PerfCollect, aby wyświetlić plik śledzenia</span><span class="sxs-lookup"><span data-stu-id="5cd12-136">Use PerfCollect to view the trace file</span></span>

<span data-ttu-id="5cd12-137">Możesz użyć perfcollect, aby wyświetlić zebrany ślad.</span><span class="sxs-lookup"><span data-stu-id="5cd12-137">You can use perfcollect itself to view the trace that you collected.</span></span> <span data-ttu-id="5cd12-138">Aby to zrobić, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="5cd12-138">To do this, use the following command:</span></span>

```bash
./perfcollect view sampleTrace.trace.zip
```

<span data-ttu-id="5cd12-139">Domyślnie zostanie wyświetlone śledzenie procesora CPU aplikacji przy użyciu programu `perf` .</span><span class="sxs-lookup"><span data-stu-id="5cd12-139">By default, this will show the CPU trace of the application using `perf`.</span></span>

<span data-ttu-id="5cd12-140">Aby sprawdzić zdarzenia, które zostały zebrane za pośrednictwem `LTTng` , można przekazać flagę w `-viewer lttng` celu wyświetlenia poszczególnych zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="5cd12-140">To look at the events that were collected via `LTTng`, you can pass in the flag `-viewer lttng` to see the individual events:</span></span>

```bash
./perfcollect view sampleTrace.trace.zip -viewer lttng
```

<span data-ttu-id="5cd12-141">Spowoduje to `babeltrace` wydrukowanie ładunku zdarzeń przy użyciu przeglądarki:</span><span class="sxs-lookup"><span data-stu-id="5cd12-141">This will use `babeltrace` viewer to print the events payload:</span></span>

```bash
# [01:02:18.189217659] (+0.020132603) ubuntu-xenial DotNETRuntime:ExceptionThrown_V1: { cpu_id = 0 }, { ExceptionType = "System.Exception", ExceptionMessage = "An exception happened", ExceptionEIP = 139875671834775, ExceptionHRESULT = 2148734208, ExceptionFlags = 16, ClrInstanceID = 0 }
# [01:02:18.189250227] (+0.020165171) ubuntu-xenial DotNETRuntime:ExceptionCatchStart: { cpu_id = 0 }, { EntryEIP = 139873639728404, MethodID = 139873626968120, MethodName = "void [helloworld] helloworld.Program::Main(string[])", ClrInstanceID = 0 }
```

### <a name="use-perfview-to-open-the-trace-file"></a><span data-ttu-id="5cd12-142">Użyj narzędzia PerfView, aby otworzyć plik śledzenia</span><span class="sxs-lookup"><span data-stu-id="5cd12-142">Use PerfView to open the trace file</span></span>

<span data-ttu-id="5cd12-143">Aby wyświetlić Zagregowany widok zarówno przykładowego procesora, jak i zdarzeń, można użyć `PerfView` na komputerze z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="5cd12-143">To see an aggregate view of both the CPU sample and the events, you can use `PerfView` on a Windows machine.</span></span>

1. <span data-ttu-id="5cd12-144">Skopiuj plik trace.zip z systemu Linux na komputer z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="5cd12-144">Copy the trace.zip file from Linux to a Windows machine.</span></span>

2. <span data-ttu-id="5cd12-145">Pobierz narzędzia PerfView z <https://aka.ms/perfview> .</span><span class="sxs-lookup"><span data-stu-id="5cd12-145">Download PerfView from <https://aka.ms/perfview>.</span></span>

3. <span data-ttu-id="5cd12-146">Uruchom PerfView.exe</span><span class="sxs-lookup"><span data-stu-id="5cd12-146">Run PerfView.exe</span></span>

    > ```cmd
    > PerfView.exe <path to trace.zip file>
    > ```

<span data-ttu-id="5cd12-147">Narzędzia PerfView wyświetli listę widoków, które są obsługiwane w oparciu o dane zawarte w pliku śledzenia.</span><span class="sxs-lookup"><span data-stu-id="5cd12-147">PerfView will display the list of views that are supported based on the data contained in the trace file.</span></span>

- <span data-ttu-id="5cd12-148">W obszarze badania procesora wybierz **stosy procesora**.</span><span class="sxs-lookup"><span data-stu-id="5cd12-148">For CPU investigations, choose **CPU stacks**.</span></span>

- <span data-ttu-id="5cd12-149">Aby uzyskać szczegółowe informacje dotyczące GC, wybierz **GCStats**.</span><span class="sxs-lookup"><span data-stu-id="5cd12-149">For detailed GC information, choose **GCStats**.</span></span>

- <span data-ttu-id="5cd12-150">Dla informacji JIT dla poszczególnych procesów/modułów/metod, wybierz **JITStats**.</span><span class="sxs-lookup"><span data-stu-id="5cd12-150">For per-process/module/method JIT information, choose **JITStats**.</span></span>

- <span data-ttu-id="5cd12-151">Jeśli nie ma widoku dla potrzebnych informacji, możesz spróbować wyszukać zdarzenia w widoku nieprzetworzone zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="5cd12-151">If there is not a view for the information you need, you can try looking for the events in the raw events view.</span></span>  <span data-ttu-id="5cd12-152">Wybierz pozycję **zdarzenia**.</span><span class="sxs-lookup"><span data-stu-id="5cd12-152">Choose **Events**.</span></span>

<span data-ttu-id="5cd12-153">Aby uzyskać więcej informacji na temat interpretowania widoków w programie narzędzia PerfView, zobacz linki pomocy w samym widoku lub w oknie głównym w narzędzia PerfView, wybierz opcję **Pomoc->użytkownicy przewodnika**.</span><span class="sxs-lookup"><span data-stu-id="5cd12-153">For more information on how to interpret views in PerfView, see help links in the view itself, or from the main window in PerfView, choose **Help->Users Guide**.</span></span>

### <a name="use-tracecompass-to-open-the-trace-file"></a><span data-ttu-id="5cd12-154">Użyj TraceCompass, aby otworzyć plik śledzenia</span><span class="sxs-lookup"><span data-stu-id="5cd12-154">Use TraceCompass to open the trace file</span></span>

<span data-ttu-id="5cd12-155">Aby wyświetlić dane śledzenia, można użyć opcji [zaćmienie TraceCompass](https://www.eclipse.org/tracecompass/) .</span><span class="sxs-lookup"><span data-stu-id="5cd12-155">[Eclipse TraceCompass](https://www.eclipse.org/tracecompass/) is another option you can use to view the traces.</span></span> <span data-ttu-id="5cd12-156">`TraceCompass` działa również na maszynach z systemem Linux, dzięki czemu nie musisz przenosić śladu do komputera z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="5cd12-156">`TraceCompass` works on Linux machines as well, so you don't need to move your trace over to a Windows machine.</span></span> <span data-ttu-id="5cd12-157">Aby można było `TraceCompass` otworzyć plik śledzenia przy użyciu programu, należy rozpakować plik.</span><span class="sxs-lookup"><span data-stu-id="5cd12-157">To use `TraceCompass` to open your trace file, you will need to unzip the file.</span></span>

```bash
unzip myTrace.trace.zip
```

<span data-ttu-id="5cd12-158">`perfcollect` program zapisze ślad LTTng zebrany w formacie pliku COLLABORATIVE w podkatalogu w `lttngTrace` .</span><span class="sxs-lookup"><span data-stu-id="5cd12-158">`perfcollect` will save the LTTng trace it collected into a CTF file format in a subdirectory in the `lttngTrace`.</span></span> <span data-ttu-id="5cd12-159">Plik COLLABORATIVE zostanie umieszczony w katalogu, który wygląda jak `lttngTrace/auto-20201025-101230\ust\uid\1000\64-bit\` .</span><span class="sxs-lookup"><span data-stu-id="5cd12-159">Specifically, the CTF file will be located in a directory that looks like `lttngTrace/auto-20201025-101230\ust\uid\1000\64-bit\`.</span></span>

<span data-ttu-id="5cd12-160">Plik śledzenia COLLABORATIVE można otworzyć w programie `TraceCompass` , zaznaczając `File -> Open Trace` i wybierając `metadata` plik.</span><span class="sxs-lookup"><span data-stu-id="5cd12-160">You can open the CTF trace file in `TraceCompass` by selecting `File -> Open Trace` and select the `metadata` file.</span></span>

<span data-ttu-id="5cd12-161">Aby uzyskać więcej informacji, zapoznaj się z [ `TraceCompass` dokumentacją](https://www.eclipse.org/tracecompass/).</span><span class="sxs-lookup"><span data-stu-id="5cd12-161">For more details, please refer to [`TraceCompass` documentation](https://www.eclipse.org/tracecompass/).</span></span>

## <a name="resolve-framework-symbols"></a><span data-ttu-id="5cd12-162">Rozpoznawanie symboli struktury</span><span class="sxs-lookup"><span data-stu-id="5cd12-162">Resolve framework symbols</span></span>

<span data-ttu-id="5cd12-163">Symbole struktury muszą być generowane ręcznie podczas zbierania śladu.</span><span class="sxs-lookup"><span data-stu-id="5cd12-163">Framework symbols need to be manually generated at the time the trace is collected.</span></span> <span data-ttu-id="5cd12-164">Różnią się one od symboli poziomu aplikacji, ponieważ struktura jest wstępnie skompilowana, podczas gdy kod aplikacji jest kompilowany dokładnie na czas.</span><span class="sxs-lookup"><span data-stu-id="5cd12-164">They are different than app-level symbols because the framework is pre-compiled while app code is just-in-time-compiled.</span></span> <span data-ttu-id="5cd12-165">W przypadku kodu struktury, który został wstępnie skompilowany do kodu natywnego, należy wywołać `crossgen` , który wie, jak generować mapowanie z kodu natywnego do nazwy metod.</span><span class="sxs-lookup"><span data-stu-id="5cd12-165">For framework code that was precompiled to native code, you need to call `crossgen` that knows how to generate the mapping from the native code to the name of the methods.</span></span>

<span data-ttu-id="5cd12-166">`perfcollect` może obsłużyć większość szczegółowych informacji, ale muszą być `crossgen` dostępne.</span><span class="sxs-lookup"><span data-stu-id="5cd12-166">`perfcollect` can handle most of the details for you, but it needs to have `crossgen` available.</span></span> <span data-ttu-id="5cd12-167">Domyślnie nie jest on instalowany z dystrybucją programu .NET.</span><span class="sxs-lookup"><span data-stu-id="5cd12-167">By default it is not installed with .NET distribution.</span></span> <span data-ttu-id="5cd12-168">Jeśli `crossgen` go nie ma, `perfcollect` ostrzega użytkownika i odwołuje się do tych instrukcji.</span><span class="sxs-lookup"><span data-stu-id="5cd12-168">If `crossgen` is not there, `perfcollect` warns you and refers you to these instructions.</span></span> <span data-ttu-id="5cd12-169">Aby rozwiązać problemy, musisz pobrać dokładnie odpowiednią wersję crossgen dla używanego środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="5cd12-169">To fix things you need to fetch exactly the right version of crossgen for the runtime you are using.</span></span> <span data-ttu-id="5cd12-170">Jeśli umieścisz narzędzie crossgen w tym samym katalogu, co biblioteki DLL środowiska uruchomieniowego .NET (na przykład libcoreclr.so), `perfcollect` można je znaleźć i dodać do pliku śledzenia symbole struktury.</span><span class="sxs-lookup"><span data-stu-id="5cd12-170">If you place the crossgen tool in the same directory as the .NET Runtime DLLs (for example, libcoreclr.so), then `perfcollect` can find it and add the framework symbols to the trace file for you.</span></span>

<span data-ttu-id="5cd12-171">Zwykle podczas tworzenia aplikacji platformy .NET po prostu jest generowana Biblioteka DLL dla napisanego kodu, przy użyciu udostępnionej kopii środowiska uruchomieniowego dla pozostałych.</span><span class="sxs-lookup"><span data-stu-id="5cd12-171">Normally when you create a .NET application, it just generates the DLL for the code you wrote, using a shared copy of the runtime for the rest.</span></span>   <span data-ttu-id="5cd12-172">Można jednak również generować informacje o nazwie "samodzielne" aplikacji i zawiera wszystkie biblioteki DLL środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="5cd12-172">However you can also generate what is called a 'self-contained' version of an application and this contains all runtime DLLs.</span></span> <span data-ttu-id="5cd12-173">`crossgen` jest częścią pakietu NuGet, który jest używany do tworzenia samodzielnych aplikacji, więc jednym ze sposobów uzyskania odpowiedniej wersji programu `crossgen` jest utworzenie samodzielnego pakietu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5cd12-173">`crossgen` is part of the NuGet package that is used to create self-contained apps, so one way of getting the right version of `crossgen` is to create a self-contained package of your application.</span></span>

<span data-ttu-id="5cd12-174">Przykład:</span><span class="sxs-lookup"><span data-stu-id="5cd12-174">For example:</span></span>

   >```bash
   > mkdir helloWorld
   > cd helloWorld
   > dotnet new console
   > dotnet publish --self-contained -r linux-x64
   >```

<span data-ttu-id="5cd12-175">Spowoduje to utworzenie nowej aplikacji Hello world i utworzenie jej jako aplikacji samodzielnej.</span><span class="sxs-lookup"><span data-stu-id="5cd12-175">This creates a new Hello World application and builds it as a self-contained app.</span></span>

<span data-ttu-id="5cd12-176">Jako efekt po stronie tworzenia samodzielnej aplikacji Narzędzie dotnet pobierze pakiet NuGet o nazwie Runtime. linux-x64. Microsoft. WebCore. app i umieści go w katalogu ~/.nuget/packages/runtime.linux-x64.microsoft.netcore.app/VERSION, gdzie wersja jest numerem wersji środowiska uruchomieniowego platformy .NET Core (na przykład 2.1.0).</span><span class="sxs-lookup"><span data-stu-id="5cd12-176">As a side effect of creating the self-contained application the dotnet tool will download a NuGet package called runtime.linux-x64.microsoft.netcore.app and place it in the directory ~/.nuget/packages/runtime.linux-x64.microsoft.netcore.app/VERSION, where VERSION is the version number of your .NET Core runtime (for example, 2.1.0).</span></span> <span data-ttu-id="5cd12-177">W obszarze, który jest katalogiem narzędzi i w tym miejscu jest potrzebne narzędzie crossgen.</span><span class="sxs-lookup"><span data-stu-id="5cd12-177">Under that is a tools directory and inside there is the crossgen tool you need.</span></span> <span data-ttu-id="5cd12-178">Począwszy od platformy .NET Core 3,0, lokalizacja pakietu to ~/.nuget/packages/microsoft.netcore.app.runtime.linux-x64/VERSION.</span><span class="sxs-lookup"><span data-stu-id="5cd12-178">Starting with .NET Core 3.0, the package location is ~/.nuget/packages/microsoft.netcore.app.runtime.linux-x64/VERSION.</span></span>

<span data-ttu-id="5cd12-179">`crossgen`Narzędzie należy umieścić obok środowiska uruchomieniowego, które jest aktualnie używane przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="5cd12-179">The `crossgen` tool needs to be put next to the runtime that is actually used by your application.</span></span> <span data-ttu-id="5cd12-180">Zazwyczaj aplikacja używa udostępnionej wersji platformy .NET Core, która jest zainstalowana w/usr/share/dotnet/shared/Microsoft.NETCore.App/VERSION, gdzie wersja jest numerem wersji środowiska uruchomieniowego .NET.</span><span class="sxs-lookup"><span data-stu-id="5cd12-180">Typically your app uses the shared version of .NET Core that is installed at /usr/share/dotnet/shared/Microsoft.NETCore.App/VERSION where VERSION is the version number of the .NET Runtime.</span></span> <span data-ttu-id="5cd12-181">Jest to lokalizacja udostępniona, dlatego musisz być administratorem.</span><span class="sxs-lookup"><span data-stu-id="5cd12-181">This is a shared location, so you need to be super-user to modify it.</span></span> <span data-ttu-id="5cd12-182">Jeśli wersja jest 2.1.0, polecenia do zaktualizowania `crossgen` byłyby następujące:</span><span class="sxs-lookup"><span data-stu-id="5cd12-182">If the VERSION is 2.1.0 the commands to update `crossgen` would be:</span></span>

   >```bash
   > sudo bash
   > cp ~/.nuget/packages/runtime.linux-x64.microsoft.netcore.app/2.1.0/tools/crossgen /usr/share/dotnet/shared/Microsoft.NETCore.App/2.1.0
   >```

<span data-ttu-id="5cd12-183">Po wykonaniu tej czynności program `perfcollect` użyje crossgen w celu uwzględnienia symboli struktury.</span><span class="sxs-lookup"><span data-stu-id="5cd12-183">Once you have done this, `perfcollect` will use crossgen to include framework symbols.</span></span> <span data-ttu-id="5cd12-184">Ostrzeżenie, które `perfcollect` ma zostać użyte do wystawienia, powinno odejść.</span><span class="sxs-lookup"><span data-stu-id="5cd12-184">The warning that `perfcollect` used to issue should go away.</span></span> <span data-ttu-id="5cd12-185">Musi to być jeden raz dla każdego komputera (do momentu zaktualizowania środowiska uruchomieniowego).</span><span class="sxs-lookup"><span data-stu-id="5cd12-185">This only has to be one once per machine (until you update your runtime).</span></span>

### <a name="alternative-turn-off-use-of-precompiled-code"></a><span data-ttu-id="5cd12-186">Alternatywa: wyłącz użycie wstępnie skompilowanego kodu</span><span class="sxs-lookup"><span data-stu-id="5cd12-186">Alternative: Turn off use of precompiled code</span></span>

<span data-ttu-id="5cd12-187">Jeśli nie masz możliwości zaktualizowania środowiska uruchomieniowego .NET (do dodania `crossgen` ) lub jeśli powyższa procedura nie zadziałała z jakiegoś powodu, istnieje inne podejście do uzyskiwania symboli struktury.</span><span class="sxs-lookup"><span data-stu-id="5cd12-187">If you don't have the ability to update the .NET Runtime (to add `crossgen`), or if the above procedure did not work for some reason, there is another approach to getting framework symbols.</span></span> <span data-ttu-id="5cd12-188">Możesz powiedzieć środowisko uruchomieniowe, aby po prostu nie używać wstępnie skompilowanego kodu struktury.</span><span class="sxs-lookup"><span data-stu-id="5cd12-188">You can tell the runtime to simply not use the precompiled framework code.</span></span> <span data-ttu-id="5cd12-189">Kod zostanie skompilowany dokładnie i `crossgen` nie jest wymagany.</span><span class="sxs-lookup"><span data-stu-id="5cd12-189">The code will be Just-In-Time compiled and `crossgen` is not needed.</span></span>

> [!NOTE]
> <span data-ttu-id="5cd12-190">Wybranie tej metody może wydłużyć czas uruchamiania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5cd12-190">Choosing this approach may increase the startup time for your application.</span></span>

<span data-ttu-id="5cd12-191">W tym celu można dodać następującą zmienną środowiskową:</span><span class="sxs-lookup"><span data-stu-id="5cd12-191">To do this, you can add the following environment variable:</span></span>

```bash
export COMPlus_ZapDisable=1
```

<span data-ttu-id="5cd12-192">Po wprowadzeniu tej zmiany należy uzyskać symbole dla całego kodu platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="5cd12-192">With this change, you should get the symbols for all .NET code.</span></span>

## <a name="get-symbols-for-the-native-runtime"></a><span data-ttu-id="5cd12-193">Pobierz symbole dla natywnego środowiska uruchomieniowego</span><span class="sxs-lookup"><span data-stu-id="5cd12-193">Get symbols for the native runtime</span></span>

<span data-ttu-id="5cd12-194">Większość czasu interesujący Twój własny kod, który jest `perfcollect` rozpoznawany domyślnie.</span><span class="sxs-lookup"><span data-stu-id="5cd12-194">Most of the time you are interested in your own code, which `perfcollect` resolves by default.</span></span> <span data-ttu-id="5cd12-195">Czasami warto zobaczyć, co się dzieje w bibliotekach DLL platformy .NET (co to jest Ostatnia sekcja), ale czasami co się dzieje w natywnych bibliotekach DLL środowiska uruchomieniowego (zazwyczaj libcoreclr.so).</span><span class="sxs-lookup"><span data-stu-id="5cd12-195">Sometimes it is useful to see what is going on inside the .NET DLLs (which is what the last section was about), but sometimes what is going on in the native runtime dlls (typically libcoreclr.so), is interesting.</span></span>  <span data-ttu-id="5cd12-196">`perfcollect` program rozpozna symbole dla tych, gdy konwertuje swoje dane, ale tylko wtedy, gdy są obecne symbole dla tych natywnych bibliotek DLL (i znajdują się obok biblioteki, do której się odnoszą).</span><span class="sxs-lookup"><span data-stu-id="5cd12-196">`perfcollect` will resolve the symbols for these when it converts its data, but only if the symbols for these native DLLs are present (and are beside the library they are for).</span></span>

<span data-ttu-id="5cd12-197">Istnieje polecenie globalne zwane [symbolem dotnet](https://github.com/dotnet/symstore/blob/master/src/dotnet-symbol/README.md#symbol-downloader-dotnet-cli-extension) .</span><span class="sxs-lookup"><span data-stu-id="5cd12-197">There is a global command called [dotnet-symbol](https://github.com/dotnet/symstore/blob/master/src/dotnet-symbol/README.md#symbol-downloader-dotnet-cli-extension) that does this.</span></span> <span data-ttu-id="5cd12-198">Aby użyć symbolu dotnet-symbol w celu uzyskania natywnych symboli środowiska uruchomieniowego:</span><span class="sxs-lookup"><span data-stu-id="5cd12-198">To use dotnet-symbol to get native runtime symbols:</span></span>

1. <span data-ttu-id="5cd12-199">Zainstaluj program `dotnet-symbol`:</span><span class="sxs-lookup"><span data-stu-id="5cd12-199">Install `dotnet-symbol`:</span></span>

    ```bash
    dotnet tool install -g dotnet-symbol
    ```

2. <span data-ttu-id="5cd12-200">Pobierz symbole.</span><span class="sxs-lookup"><span data-stu-id="5cd12-200">Download the symbols.</span></span> <span data-ttu-id="5cd12-201">Jeśli zainstalowana wersja środowiska uruchomieniowego .NET Core to 2.1.0, polecenie to jest następujące:</span><span class="sxs-lookup"><span data-stu-id="5cd12-201">If your installed version of the .NET Core runtime is 2.1.0, the command to do this is:</span></span>

    ```bash
    mkdir mySymbols
    dotnet symbol --symbols --output mySymbols  /usr/share/dotnet/shared/Microsoft.NETCore.App/2.1.0/lib*.so
    ```

3. <span data-ttu-id="5cd12-202">Skopiuj symbole do poprawnego miejsca.</span><span class="sxs-lookup"><span data-stu-id="5cd12-202">Copy the symbols to the correct place.</span></span>

    ```bash
    sudo cp mySymbols/* /usr/share/dotnet/shared/Microsoft.NETCore.App/2.1.0
    ```

    <span data-ttu-id="5cd12-203">Jeśli nie można tego zrobić, ponieważ nie masz dostępu do zapisu do odpowiedniego katalogu, możesz użyć, `perf buildid-cache` Aby dodać symbole.</span><span class="sxs-lookup"><span data-stu-id="5cd12-203">If this cannot be done because you do not have write access to the appropriate directory, you can use `perf buildid-cache` to add the symbols.</span></span>

<span data-ttu-id="5cd12-204">Następnie należy uzyskać nazwy symboliczne natywnych bibliotek DLL podczas uruchamiania `perfcollect` .</span><span class="sxs-lookup"><span data-stu-id="5cd12-204">After this, you should get symbolic names for the native dlls when you run `perfcollect`.</span></span>

## <a name="collect-in-a-docker-container"></a><span data-ttu-id="5cd12-205">Zbieranie danych w kontenerze platformy Docker</span><span class="sxs-lookup"><span data-stu-id="5cd12-205">Collect in a Docker container</span></span>

<span data-ttu-id="5cd12-206">Aby uzyskać więcej informacji na temat używania `perfcollect` w środowiskach kontenerów, zobacz [zbieranie danych diagnostycznych w kontenerach](./diagnostics-in-containers.md).</span><span class="sxs-lookup"><span data-stu-id="5cd12-206">For more information on how to use `perfcollect` in container environments, see [Collect diagnostics in containers](./diagnostics-in-containers.md).</span></span>

## <a name="learn-more-about-collection-options"></a><span data-ttu-id="5cd12-207">Dowiedz się więcej na temat opcji kolekcji</span><span class="sxs-lookup"><span data-stu-id="5cd12-207">Learn more about collection options</span></span>

<span data-ttu-id="5cd12-208">Możesz określić następujące opcjonalne flagi, `perfcollect` Aby lepiej odpowiadały potrzebom diagnostycznym.</span><span class="sxs-lookup"><span data-stu-id="5cd12-208">You can specify the following optional flags with `perfcollect` to better suit your diagnostic needs.</span></span>

### <a name="collect-for-a-specific-duration"></a><span data-ttu-id="5cd12-209">Zbieraj przez określony czas trwania</span><span class="sxs-lookup"><span data-stu-id="5cd12-209">Collect for a specific duration</span></span>

<span data-ttu-id="5cd12-210">Gdy chcesz zbierać ślady dla określonego czasu trwania, możesz użyć `-collectsec` opcji, a po niej liczby określającej łączną liczbę sekund do zebrania śladu.</span><span class="sxs-lookup"><span data-stu-id="5cd12-210">When you want to collect a trace for a specific duration, you can use `-collectsec` option followed by a number specifying the total seconds to collect a trace for.</span></span>

### <a name="collect-threadtime-traces"></a><span data-ttu-id="5cd12-211">Zbierz ślady threadtime</span><span class="sxs-lookup"><span data-stu-id="5cd12-211">Collect threadtime traces</span></span>

<span data-ttu-id="5cd12-212">Określenie `-threadtime` `perfcollect` opcji with umożliwia zbieranie danych użycia procesora CPU dla wątków.</span><span class="sxs-lookup"><span data-stu-id="5cd12-212">Specifying `-threadtime` with `perfcollect` lets you collect per-thread CPU usage data.</span></span> <span data-ttu-id="5cd12-213">Dzięki temu można analizować, gdzie każdy wątek spędza czas procesora CPU.</span><span class="sxs-lookup"><span data-stu-id="5cd12-213">This lets you analyze where every thread was spending its CPU time.</span></span>

### <a name="collect-traces-for-managed-memory-and-garbage-collector-performance"></a><span data-ttu-id="5cd12-214">Zbieranie śladów wydajności pamięci zarządzanej i modułu wyrzucania elementów bezużytecznych</span><span class="sxs-lookup"><span data-stu-id="5cd12-214">Collect traces for managed memory and garbage collector performance</span></span>

<span data-ttu-id="5cd12-215">Poniższe opcje pozwalają na zbieranie zdarzeń GC z środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="5cd12-215">The following options let you specifically collect the GC events from the runtime.</span></span>

* `perfcollect collect -gccollectonly`

<span data-ttu-id="5cd12-216">Zbiera tylko minimalny zestaw zdarzeń zbierania danych GC.</span><span class="sxs-lookup"><span data-stu-id="5cd12-216">Collect only a minimal set of GC Collection events.</span></span> <span data-ttu-id="5cd12-217">Jest to najmniej pełny profil kolekcji zdarzeń GC o najniższym wpływie na wydajność aplikacji docelowej.</span><span class="sxs-lookup"><span data-stu-id="5cd12-217">This is the least verbose GC eventing collection profile with the lowest impact on the target app's performance.</span></span> <span data-ttu-id="5cd12-218">To polecenie jest analogiczne do `PerfView.exe /GCCollectOnly collect` polecenia w narzędzia PerfView.</span><span class="sxs-lookup"><span data-stu-id="5cd12-218">This command is analogous to `PerfView.exe /GCCollectOnly collect` command in PerfView.</span></span>

* `perfcollect collect -gconly`

<span data-ttu-id="5cd12-219">Zbieraj więcej szczegółowych zdarzeń zbierania danych GC z zdarzeniami JIT, Loader i Exception.</span><span class="sxs-lookup"><span data-stu-id="5cd12-219">Collect more verbose GC collection events with JIT, Loader, and Exception events.</span></span> <span data-ttu-id="5cd12-220">Powoduje to zażądanie więcej zdarzeń pełnych (takich jak informacje o alokacji i informacje o przyłączeniu GC) i ma większy wpływ na wydajność aplikacji docelowej niż `-gccollectonly` opcja.</span><span class="sxs-lookup"><span data-stu-id="5cd12-220">This requests more verbose events (such as the allocation information and GC join information) and will have more impact to the target app's performance than `-gccollectonly` option.</span></span> <span data-ttu-id="5cd12-221">To polecenie jest analogiczne do `PerfView.exe /GCOnly collect` polecenia w narzędzia PerfView.</span><span class="sxs-lookup"><span data-stu-id="5cd12-221">This command is analogous to `PerfView.exe /GCOnly collect` command in PerfView.</span></span>

* `perfcollect collect -gcwithheap`

<span data-ttu-id="5cd12-222">Zbierz najbardziej szczegółowe zdarzenia zbierania danych GC, które śledzą przeżycie sterty i przesunięcia.</span><span class="sxs-lookup"><span data-stu-id="5cd12-222">Collect the most verbose GC collection events which tracks the heap survival and movements as well.</span></span> <span data-ttu-id="5cd12-223">Zapewnia to szczegółową analizę zachowania GC, ale powiąże się z dużym kosztem wydajności, ponieważ każda GLOBALna wydajność może trwać dłużej niż dwa razy.</span><span class="sxs-lookup"><span data-stu-id="5cd12-223">This gives in-depth analysis of the GC behavior but will incur high performance cost as each GC can take more than two times longer.</span></span> <span data-ttu-id="5cd12-224">Zaleca się zrozumienie implikacji wydajności korzystania z tej opcji śledzenia podczas śledzenia w środowiskach produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="5cd12-224">It is recommended you understand the performance implication of using this trace option when tracing in production environments.</span></span>
