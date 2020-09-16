---
title: Ngen.exe (Generator obrazu natywnego)
description: Przejrzyj Ngen.exe, Generator obrazu natywnego. Zwiększ wydajność zarządzanej aplikacji, tworząc obrazy natywne i instalując je w lokalnej pamięci podręcznej obrazów natywnych.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- Native Image Generator
- images [.NET Framework], native
- side-by-side execution, native images
- assemblies [.NET Framework], native image
- Ngen.exe
- native image generation
- native image cache
- publisher policy applied for native images
- invalid images
- BypassNGenAttribute
- System.Runtime.BypassNGenAttribute
ms.assetid: 44bf97aa-a9a4-4eba-9a0d-cfaa6fc53a66
ms.openlocfilehash: 12ef6724a76ec59bd412427a0a353565b1be2c8e
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90558420"
---
# <a name="ngenexe-native-image-generator"></a><span data-ttu-id="25e80-104">Ngen.exe (Generator obrazu natywnego)</span><span class="sxs-lookup"><span data-stu-id="25e80-104">Ngen.exe (Native Image Generator)</span></span>

<span data-ttu-id="25e80-105">Generator obrazów natywnych (Ngen.exe) jest narzędziem, które poprawia wydajność zarządzanych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25e80-105">The Native Image Generator (Ngen.exe) is a tool that improves the performance of managed applications.</span></span> <span data-ttu-id="25e80-106">Program Ngen.exe tworzy obrazy natywne, które są plikami zawierającymi skompilowany kod maszynowy specyficzny dla procesora, i instaluje je w pamięci podręcznej obrazów natywnych na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="25e80-106">Ngen.exe creates native images, which are files containing compiled processor-specific machine code, and installs them into the native image cache on the local computer.</span></span> <span data-ttu-id="25e80-107">Środowisko uruchomieniowe może używać obrazów natywnych z tej pamięci podręcznej, zamiast używać kompilatora JIT (Just-In-Time) w celu skompilowania oryginalnego zestawu.</span><span class="sxs-lookup"><span data-stu-id="25e80-107">The runtime can use native images from the cache instead of using the just-in-time (JIT) compiler to compile the original assembly.</span></span>

> [!NOTE]
> <span data-ttu-id="25e80-108">Ngen.exe kompiluje obrazy natywne dla zestawów, które są przeznaczone tylko dla .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="25e80-108">Ngen.exe compiles native images for assemblies that target the .NET Framework only.</span></span> <span data-ttu-id="25e80-109">Równoważny Generator obrazu natywnego dla platformy .NET Core to [CrossGen](https://github.com/dotnet/runtime/blob/master/docs/workflow/building/coreclr/crossgen.md).</span><span class="sxs-lookup"><span data-stu-id="25e80-109">The equivalent native image generator for .NET Core is [CrossGen](https://github.com/dotnet/runtime/blob/master/docs/workflow/building/coreclr/crossgen.md).</span></span>

<span data-ttu-id="25e80-110">Zmiany Ngen.exe w .NET Framework 4:</span><span class="sxs-lookup"><span data-stu-id="25e80-110">Changes to Ngen.exe in the .NET Framework 4:</span></span>

- <span data-ttu-id="25e80-111">Program Ngen.exe obecnie kompiluje zestawy w trybie pełnego zaufania, a zasady zabezpieczeń dostępu kodu (CAS) nie są już uwzględniane.</span><span class="sxs-lookup"><span data-stu-id="25e80-111">Ngen.exe now compiles assemblies with full trust, and code access security (CAS) policy is no longer evaluated.</span></span>

- <span data-ttu-id="25e80-112">Obrazy natywne generowane przez program Ngen.exe nie mogą już być ładowane do aplikacji, które działają w trybie częściowego zaufania.</span><span class="sxs-lookup"><span data-stu-id="25e80-112">Native images that are generated with Ngen.exe can no longer be loaded into applications that are running in partial trust.</span></span>

<span data-ttu-id="25e80-113">Zmiany w programie Ngen.exe wprowadzone w programie .NET Framework w wersji 2.0:</span><span class="sxs-lookup"><span data-stu-id="25e80-113">Changes to Ngen.exe in the .NET Framework version 2.0:</span></span>

- <span data-ttu-id="25e80-114">Instalacja zestawu powoduje także instalację jego zależności, co upraszcza składnię programu Ngen.exe.</span><span class="sxs-lookup"><span data-stu-id="25e80-114">Installing an assembly also installs its dependencies, simplifying the syntax of Ngen.exe.</span></span>

- <span data-ttu-id="25e80-115">Obrazy natywne mogą być współużytkowane w różnych domenach aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25e80-115">Native images can now be shared across application domains.</span></span>

- <span data-ttu-id="25e80-116">Nowa akcja, `update` program ponownie tworzy obrazy, które zostały unieważnione.</span><span class="sxs-lookup"><span data-stu-id="25e80-116">A new action, `update`, re-creates images that have been invalidated.</span></span>

- <span data-ttu-id="25e80-117">Akcje mogą być odraczane w celu wykonania przez usługę, która korzysta z czasu bezczynności komputera, aby generować i instalować obrazy.</span><span class="sxs-lookup"><span data-stu-id="25e80-117">Actions can be deferred for execution by a service that uses idle time on the computer to generate and install images.</span></span>

- <span data-ttu-id="25e80-118">Niektóre przyczyny unieważnienia obrazu zostały wyeliminowane.</span><span class="sxs-lookup"><span data-stu-id="25e80-118">Some causes of image invalidation have been eliminated.</span></span>

<span data-ttu-id="25e80-119">W systemie Windows 8 zobacz [zadania obrazu natywnego](#native-image-task).</span><span class="sxs-lookup"><span data-stu-id="25e80-119">On Windows 8, see [Native Image Task](#native-image-task).</span></span>

<span data-ttu-id="25e80-120">Aby uzyskać dodatkowe informacje na temat używania Ngen.exe i usługi obrazów natywnych, zobacz [Native Image Service](#native-image-service).</span><span class="sxs-lookup"><span data-stu-id="25e80-120">For additional information on using Ngen.exe and the native image service, see [Native Image Service](#native-image-service).</span></span>

> [!NOTE]
> <span data-ttu-id="25e80-121">Ngen.exe składni dla wersji 1,0 i 1,1 .NET Framework można znaleźć w [starszej składni generatora obrazów natywnych (Ngen.exe)](/previous-versions/dotnet/netframework-4.0/ms165073(v=vs.100)).</span><span class="sxs-lookup"><span data-stu-id="25e80-121">Ngen.exe syntax for versions 1.0 and 1.1 of the .NET Framework can be found in [Native Image Generator (Ngen.exe) Legacy Syntax](/previous-versions/dotnet/netframework-4.0/ms165073(v=vs.100)).</span></span>

<span data-ttu-id="25e80-122">To narzędzie jest instalowane automatycznie z programem Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="25e80-122">This tool is automatically installed with Visual Studio.</span></span> <span data-ttu-id="25e80-123">Aby uruchomić narzędzie, użyj wiersz polecenia dla deweloperów dla programu Visual Studio (lub wiersza polecenia programu Visual Studio w systemie Windows 7).</span><span class="sxs-lookup"><span data-stu-id="25e80-123">To run the tool, use the Developer Command Prompt for Visual Studio (or the Visual Studio Command Prompt in Windows 7).</span></span> <span data-ttu-id="25e80-124">Aby uzyskać więcej informacji, zobacz [wiersza polecenia](developer-command-prompt-for-vs.md).</span><span class="sxs-lookup"><span data-stu-id="25e80-124">For more information, see [Command Prompts](developer-command-prompt-for-vs.md).</span></span>

<span data-ttu-id="25e80-125">W wierszu polecenia wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="25e80-125">At the command prompt, type the following:</span></span>

## <a name="syntax"></a><span data-ttu-id="25e80-126">Składnia</span><span class="sxs-lookup"><span data-stu-id="25e80-126">Syntax</span></span>

```console
ngen action [options]
```

```console
ngen /? | /help
```

## <a name="actions"></a><span data-ttu-id="25e80-127">Akcje</span><span class="sxs-lookup"><span data-stu-id="25e80-127">Actions</span></span>

<span data-ttu-id="25e80-128">W poniższej tabeli przedstawiono składnię każdego z nich `action` .</span><span class="sxs-lookup"><span data-stu-id="25e80-128">The following table shows the syntax of each `action`.</span></span> <span data-ttu-id="25e80-129">Aby zapoznać się z opisami poszczególnych części elementu `action` , zobacz [argumenty](#ArgumentTable), [poziomy priorytetów](#PriorityTable), [scenariusze](#ScenarioTable)i tabele [konfiguracyjne](#ConfigTable) .</span><span class="sxs-lookup"><span data-stu-id="25e80-129">For descriptions of the individual parts of an `action`, see the [Arguments](#ArgumentTable), [Priority Levels](#PriorityTable), [Scenarios](#ScenarioTable), and [Config](#ConfigTable) tables.</span></span> <span data-ttu-id="25e80-130">W tabeli [Options](#OptionTable) opisano `options` przełączniki i.</span><span class="sxs-lookup"><span data-stu-id="25e80-130">The [Options](#OptionTable) table describes the `options` and the help switches.</span></span>

|<span data-ttu-id="25e80-131">Akcja</span><span class="sxs-lookup"><span data-stu-id="25e80-131">Action</span></span>|<span data-ttu-id="25e80-132">Opis</span><span class="sxs-lookup"><span data-stu-id="25e80-132">Description</span></span>|
|------------|-----------------|
|<span data-ttu-id="25e80-133">`install` [ `assemblyName` &#124; `assemblyPath` ] [ `scenarios` ] [] [ `config` `/queue` [ `:` { `1`&#124;`2`&#124;`3` }]]</span><span class="sxs-lookup"><span data-stu-id="25e80-133">`install` [`assemblyName` &#124; `assemblyPath`] [`scenarios`] [`config`] [`/queue`[`:`{`1`&#124;`2`&#124;`3`}]]</span></span>|<span data-ttu-id="25e80-134">Generuje obrazy natywne dla zestawu i jego zależności, a także instaluje obrazy w pamięci podręcznej obrazów natywnych.</span><span class="sxs-lookup"><span data-stu-id="25e80-134">Generate native images for an assembly and its dependencies and install the images in the native image cache.</span></span><br /><br /> <span data-ttu-id="25e80-135">Jeśli `/queue` jest określona, akcja jest umieszczana w kolejce dla usługi obrazów natywnych.</span><span class="sxs-lookup"><span data-stu-id="25e80-135">If `/queue` is specified, the action is queued for the native image service.</span></span> <span data-ttu-id="25e80-136">Domyślnym priorytetem jest 3.</span><span class="sxs-lookup"><span data-stu-id="25e80-136">The default priority is 3.</span></span> <span data-ttu-id="25e80-137">Zobacz tabelę [poziomów priorytetów](#PriorityTable) .</span><span class="sxs-lookup"><span data-stu-id="25e80-137">See the [Priority Levels](#PriorityTable) table.</span></span>|
|<span data-ttu-id="25e80-138">`uninstall` [ `assemblyName` &#124; `assemblyPath` ] [ `scenarios` ] [ `config` ]</span><span class="sxs-lookup"><span data-stu-id="25e80-138">`uninstall` [`assemblyName` &#124; `assemblyPath`] [`scenarios`] [`config`]</span></span>|<span data-ttu-id="25e80-139">Usuwa obrazy natywne zestawu i jego zależności z pamięci podręcznej obrazów natywnych.</span><span class="sxs-lookup"><span data-stu-id="25e80-139">Delete the native images of an assembly and its dependencies from the native image cache.</span></span><br /><br /> <span data-ttu-id="25e80-140">Aby odinstalować pojedynczy obraz i jego zależności, należy użyć tych samych argumentów wiersza polecenia, które zostały użyte podczas instalacji obrazu.</span><span class="sxs-lookup"><span data-stu-id="25e80-140">To uninstall a single image and its dependencies, use the same command-line arguments that were used to install the image.</span></span> <span data-ttu-id="25e80-141">**Uwaga:**  Począwszy od .NET Framework 4, Akcja `uninstall` \* nie jest już obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="25e80-141">**Note:**  Starting with the .NET Framework 4, the action `uninstall` \* is no longer supported.</span></span>|
|<span data-ttu-id="25e80-142">`update` [`/queue`]</span><span class="sxs-lookup"><span data-stu-id="25e80-142">`update` [`/queue`]</span></span>|<span data-ttu-id="25e80-143">Aktualizuje obrazy natywne, które stały się nieprawidłowe.</span><span class="sxs-lookup"><span data-stu-id="25e80-143">Update native images that have become invalid.</span></span><br /><br /> <span data-ttu-id="25e80-144">Jeśli `/queue` jest określony, aktualizacje są umieszczane w kolejce dla usługi obrazów natywnych.</span><span class="sxs-lookup"><span data-stu-id="25e80-144">If `/queue` is specified, the updates are queued for the native image service.</span></span> <span data-ttu-id="25e80-145">Aktualizacje są zawsze planowane z priorytetem 3, więc są uruchamiane, gdy komputer znajduje się w stanie bezczynności.</span><span class="sxs-lookup"><span data-stu-id="25e80-145">Updates are always scheduled at priority 3, so they run when the computer is idle.</span></span>|
|<span data-ttu-id="25e80-146">`display` [ `assemblyName` &#124; `assemblyPath` ]</span><span class="sxs-lookup"><span data-stu-id="25e80-146">`display` [`assemblyName` &#124; `assemblyPath`]</span></span>|<span data-ttu-id="25e80-147">Wyświetla stan obrazów natywnych dla zestawu i jego zależności.</span><span class="sxs-lookup"><span data-stu-id="25e80-147">Display the state of the native images for an assembly and its dependencies.</span></span><br /><br /> <span data-ttu-id="25e80-148">Jeśli nie zostaną dostarczone argumenty, będą wyświetlane wszystkie dane z pamięci podręcznej obrazów natywnych.</span><span class="sxs-lookup"><span data-stu-id="25e80-148">If no argument is supplied, everything in the native image cache is displayed.</span></span>|
|<span data-ttu-id="25e80-149">`executeQueuedItems` [<code>1&#124;2&#124;3</code>]</span><span class="sxs-lookup"><span data-stu-id="25e80-149">`executeQueuedItems` [<code>1&#124;2&#124;3</code>]</span></span><br /><br /> <span data-ttu-id="25e80-150">-lub-</span><span class="sxs-lookup"><span data-stu-id="25e80-150">-or-</span></span><br /><br /> <span data-ttu-id="25e80-151">`eqi` [1&#124;2&#124;3]</span><span class="sxs-lookup"><span data-stu-id="25e80-151">`eqi` [1&#124;2&#124;3]</span></span>|<span data-ttu-id="25e80-152">Wykonuje umieszczone w kolejce zadania kompilacji.</span><span class="sxs-lookup"><span data-stu-id="25e80-152">Execute queued compilation jobs.</span></span><br /><br /> <span data-ttu-id="25e80-153">Jeśli określono priorytet, wykonywane są zadania kompilacji z większym lub równym priorytetem.</span><span class="sxs-lookup"><span data-stu-id="25e80-153">If a priority is specified, compilation jobs with greater or equal priority are executed.</span></span> <span data-ttu-id="25e80-154">Jeśli nie określono priorytetu, wykonywane są wszystkie skolejkowane zadania kompilacji.</span><span class="sxs-lookup"><span data-stu-id="25e80-154">If no priority is specified, all queued compilation jobs are executed.</span></span>|
|<span data-ttu-id="25e80-155">`queue` { `pause` &#124; `continue` &#124; `status` }</span><span class="sxs-lookup"><span data-stu-id="25e80-155">`queue` {`pause` &#124; `continue` &#124; `status`}</span></span>|<span data-ttu-id="25e80-156">Wstrzymuje usługę obrazów natywnych, zezwala wstrzymanej usłudze na kontynuowanie działania lub bada stan usługi.</span><span class="sxs-lookup"><span data-stu-id="25e80-156">Pause the native image service, allow the paused service to continue, or query the status of the service.</span></span>|

<a name="ArgumentTable"></a>

## <a name="arguments"></a><span data-ttu-id="25e80-157">Argumenty</span><span class="sxs-lookup"><span data-stu-id="25e80-157">Arguments</span></span>

|<span data-ttu-id="25e80-158">Argument</span><span class="sxs-lookup"><span data-stu-id="25e80-158">Argument</span></span>|<span data-ttu-id="25e80-159">Opis</span><span class="sxs-lookup"><span data-stu-id="25e80-159">Description</span></span>|
|--------------|-----------------|
|`assemblyName`|<span data-ttu-id="25e80-160">Pełna nazwa wyświetlana zestawu.</span><span class="sxs-lookup"><span data-stu-id="25e80-160">The full display name of the assembly.</span></span> <span data-ttu-id="25e80-161">Na przykład `"myAssembly, Version=2.0.0.0, Culture=neutral, PublicKeyToken=0038abc9deabfle5"`.</span><span class="sxs-lookup"><span data-stu-id="25e80-161">For example, `"myAssembly, Version=2.0.0.0, Culture=neutral, PublicKeyToken=0038abc9deabfle5"`.</span></span> <span data-ttu-id="25e80-162">**Uwaga:**  `myAssembly`Dla akcji i można podać częściową nazwę zestawu, taką jak `display` `uninstall` .</span><span class="sxs-lookup"><span data-stu-id="25e80-162">**Note:**  You can supply a partial assembly name, such as `myAssembly`, for the `display` and `uninstall` actions.</span></span> <br /><br /> <span data-ttu-id="25e80-163">W jednym wierszu polecenia programu Ngen.exe można określić tylko jeden zestaw.</span><span class="sxs-lookup"><span data-stu-id="25e80-163">Only one assembly can be specified per Ngen.exe command line.</span></span>|
|`assemblyPath`|<span data-ttu-id="25e80-164">Jawna ścieżka zestawu.</span><span class="sxs-lookup"><span data-stu-id="25e80-164">The explicit path of the assembly.</span></span> <span data-ttu-id="25e80-165">Można określić pełną lub względną ścieżkę.</span><span class="sxs-lookup"><span data-stu-id="25e80-165">You can specify a full or relative path.</span></span><br /><br /> <span data-ttu-id="25e80-166">Jeśli użytkownik określi nazwę pliku bez ścieżki, zestaw musi znajdować się w bieżącym katalogu.</span><span class="sxs-lookup"><span data-stu-id="25e80-166">If you specify a file name without a path, the assembly must be located in the current directory.</span></span><br /><br /> <span data-ttu-id="25e80-167">W jednym wierszu polecenia programu Ngen.exe można określić tylko jeden zestaw.</span><span class="sxs-lookup"><span data-stu-id="25e80-167">Only one assembly can be specified per Ngen.exe command line.</span></span>|

<a name="PriorityTable"></a>

## <a name="priority-levels"></a><span data-ttu-id="25e80-168">Poziomy priorytetów</span><span class="sxs-lookup"><span data-stu-id="25e80-168">Priority Levels</span></span>

|<span data-ttu-id="25e80-169">Priorytet</span><span class="sxs-lookup"><span data-stu-id="25e80-169">Priority</span></span>|<span data-ttu-id="25e80-170">Opis</span><span class="sxs-lookup"><span data-stu-id="25e80-170">Description</span></span>|
|--------------|-----------------|
|`1`|<span data-ttu-id="25e80-171">Obrazy natywne są generowane i instalowane natychmiast, bez czekania na okres bezczynności.</span><span class="sxs-lookup"><span data-stu-id="25e80-171">Native images are generated and installed immediately, without waiting for idle time.</span></span>|
|`2`|<span data-ttu-id="25e80-172">Obrazy natywne są generowane i instalowane bez czekania na okres bezczynności, ale po zakończeniu wszystkich akcji z priorytetem 1 (i ich zależności).</span><span class="sxs-lookup"><span data-stu-id="25e80-172">Native images are generated and installed without waiting for idle time, but after all priority 1 actions (and their dependencies) have completed.</span></span>|
|`3`|<span data-ttu-id="25e80-173">Obrazy natywne są instalowane, gdy usługa obrazów natywnych wykryje, że komputer jest w stanie bezczynności.</span><span class="sxs-lookup"><span data-stu-id="25e80-173">Native images are installed when the native image service detects that the computer is idle.</span></span> <span data-ttu-id="25e80-174">Zobacz [Native Image Service](#native-image-service).</span><span class="sxs-lookup"><span data-stu-id="25e80-174">See [Native Image Service](#native-image-service).</span></span>|

<a name="ScenarioTable"></a>

## <a name="scenarios"></a><span data-ttu-id="25e80-175">Scenariusze</span><span class="sxs-lookup"><span data-stu-id="25e80-175">Scenarios</span></span>

|<span data-ttu-id="25e80-176">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="25e80-176">Scenario</span></span>|<span data-ttu-id="25e80-177">Opis</span><span class="sxs-lookup"><span data-stu-id="25e80-177">Description</span></span>|
|--------------|-----------------|
|`/Debug`|<span data-ttu-id="25e80-178">Generuje obrazy natywne, których można używać w debugerze.</span><span class="sxs-lookup"><span data-stu-id="25e80-178">Generate native images that can be used under a debugger.</span></span>|
|`/Profile`|<span data-ttu-id="25e80-179">Generuje obrazy natywne, które mogą być używane w profilerze.</span><span class="sxs-lookup"><span data-stu-id="25e80-179">Generate native images that can be used under a profiler.</span></span>|
|`/NoDependencies`|<span data-ttu-id="25e80-180">Generuje minimalną liczbę obrazów natywnych wymaganą przez opcje określonego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="25e80-180">Generate the minimum number of native images required by the specified scenario options.</span></span>|

<a name="ConfigTable"></a>

## <a name="config"></a><span data-ttu-id="25e80-181">Config</span><span class="sxs-lookup"><span data-stu-id="25e80-181">Config</span></span>

|<span data-ttu-id="25e80-182">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="25e80-182">Configuration</span></span>|<span data-ttu-id="25e80-183">Opis</span><span class="sxs-lookup"><span data-stu-id="25e80-183">Description</span></span>|
|-------------------|-----------------|
|<span data-ttu-id="25e80-184">`/ExeConfig:` `exePath`</span><span class="sxs-lookup"><span data-stu-id="25e80-184">`/ExeConfig:` `exePath`</span></span>|<span data-ttu-id="25e80-185">Używa konfiguracji określonego zestawu wykonywalnego.</span><span class="sxs-lookup"><span data-stu-id="25e80-185">Use the configuration of the specified executable assembly.</span></span><br /><br /> <span data-ttu-id="25e80-186">Program Ngen.exe musi podjąć te same decyzje, co moduł ładowania podczas tworzenia powiązania z zależnościami.</span><span class="sxs-lookup"><span data-stu-id="25e80-186">Ngen.exe needs to make the same decisions as the loader when binding to dependencies.</span></span> <span data-ttu-id="25e80-187">Gdy składnik współużytkowany jest ładowany w czasie wykonywania, przy użyciu <xref:System.Reflection.Assembly.Load%2A> metody, plik konfiguracyjny aplikacji określa zależności, które są ładowane dla składnika współużytkowanego — na przykład wersję załadowanej zależności.</span><span class="sxs-lookup"><span data-stu-id="25e80-187">When a shared component is loaded at run time, using the <xref:System.Reflection.Assembly.Load%2A> method, the application's configuration file determines the dependencies that are loaded for the shared component — for example, the version of a dependency that is loaded.</span></span> <span data-ttu-id="25e80-188">`/ExeConfig`Przełącznik zawiera Ngen.exe wskazówki dotyczące tego, które zależności zostaną załadowane w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="25e80-188">The `/ExeConfig` switch gives Ngen.exe guidance on which dependencies would be loaded at run time.</span></span>|
|<span data-ttu-id="25e80-189">`/AppBase:` `directoryPath`</span><span class="sxs-lookup"><span data-stu-id="25e80-189">`/AppBase:` `directoryPath`</span></span>|<span data-ttu-id="25e80-190">Podczas lokalizowania zależności należy użyć określonego katalogu jako podstawy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25e80-190">When locating dependencies, use the specified directory as the application base.</span></span>|

<a name="OptionTable"></a>

## <a name="options"></a><span data-ttu-id="25e80-191">Opcje</span><span class="sxs-lookup"><span data-stu-id="25e80-191">Options</span></span>

|<span data-ttu-id="25e80-192">Opcja</span><span class="sxs-lookup"><span data-stu-id="25e80-192">Option</span></span>|<span data-ttu-id="25e80-193">Opis</span><span class="sxs-lookup"><span data-stu-id="25e80-193">Description</span></span>|
|------------|-----------------|
|`/nologo`|<span data-ttu-id="25e80-194">Pomija wyświetlanie transparentu startowego firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="25e80-194">Suppress the Microsoft startup banner display.</span></span>|
|`/silent`|<span data-ttu-id="25e80-195">Pomija wyświetlanie komunikatów o sukcesie.</span><span class="sxs-lookup"><span data-stu-id="25e80-195">Suppress the display of success messages.</span></span>|
|`/verbose`|<span data-ttu-id="25e80-196">Wyświetla szczegółowe informacje na potrzeby debugowania.</span><span class="sxs-lookup"><span data-stu-id="25e80-196">Display detailed information for debugging.</span></span> <span data-ttu-id="25e80-197">**Uwaga:**  Ze względu na ograniczenia systemu operacyjnego ta opcja nie wyświetla więcej informacji o systemach Windows 98 i Windows Millennium Edition.</span><span class="sxs-lookup"><span data-stu-id="25e80-197">**Note:**  Due to operating system limitations, this option does not display as much additional information on Windows 98 and Windows Millennium Edition.</span></span>|
|<span data-ttu-id="25e80-198">`/help`, `/?`</span><span class="sxs-lookup"><span data-stu-id="25e80-198">`/help`, `/?`</span></span>|<span data-ttu-id="25e80-199">Wyświetla składnię polecenia i opcje dla aktualnego wydania.</span><span class="sxs-lookup"><span data-stu-id="25e80-199">Display command syntax and options for the current release.</span></span>|

## <a name="remarks"></a><span data-ttu-id="25e80-200">Uwagi</span><span class="sxs-lookup"><span data-stu-id="25e80-200">Remarks</span></span>

<span data-ttu-id="25e80-201">Użytkownik musi mieć uprawnienia administracyjne, aby uruchomić program Ngen.exe.</span><span class="sxs-lookup"><span data-stu-id="25e80-201">To run Ngen.exe, you must have administrative privileges.</span></span>

> [!CAUTION]
> <span data-ttu-id="25e80-202">Nie należy uruchamiać programu Ngen.exe dla zestawów, które nie są w pełni zaufane.</span><span class="sxs-lookup"><span data-stu-id="25e80-202">Do not run Ngen.exe on assemblies that are not fully trusted.</span></span> <span data-ttu-id="25e80-203">Począwszy od .NET Framework 4, Ngen.exe kompiluje zestawy z pełnym zaufaniem, a zasady zabezpieczeń dostępu kodu (CAS) nie są już oceniane.</span><span class="sxs-lookup"><span data-stu-id="25e80-203">Starting with the .NET Framework 4, Ngen.exe compiles assemblies with full trust, and code access security (CAS) policy is no longer evaluated.</span></span>

<span data-ttu-id="25e80-204">Począwszy od .NET Framework 4, obrazy natywne generowane z Ngen.exe nie mogą być już ładowane do aplikacji, które działają w częściowej relacji zaufania.</span><span class="sxs-lookup"><span data-stu-id="25e80-204">Starting with the .NET Framework 4, the native images that are generated with Ngen.exe can no longer be loaded into applications that are running in partial trust.</span></span> <span data-ttu-id="25e80-205">Zamiast tego wywoływany jest kompilator JIT (Just-In-Time).</span><span class="sxs-lookup"><span data-stu-id="25e80-205">Instead, the just-in-time (JIT) compiler is invoked.</span></span>

<span data-ttu-id="25e80-206">Ngen.exe generuje obrazy natywne dla zestawu określonego przez `assemblyname` argument dla `install` akcji i wszystkich jej zależności.</span><span class="sxs-lookup"><span data-stu-id="25e80-206">Ngen.exe generates native images for the assembly specified by the `assemblyname` argument to the `install` action and all its dependencies.</span></span> <span data-ttu-id="25e80-207">Zależności są ustalane na podstawie odwołań w manifeście zestawu.</span><span class="sxs-lookup"><span data-stu-id="25e80-207">Dependencies are determined from references in the assembly manifest.</span></span> <span data-ttu-id="25e80-208">Jedyny scenariusz, w którym należy oddzielnie zainstalować zależność, to, gdy aplikacja ładuje ją przy użyciu odbicia, na przykład przez wywołanie <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> metody.</span><span class="sxs-lookup"><span data-stu-id="25e80-208">The only scenario in which you need to install a dependency separately is when the application loads it using reflection, for example by calling the <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> method.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="25e80-209">Nie należy używać <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType> metody z obrazami natywnymi.</span><span class="sxs-lookup"><span data-stu-id="25e80-209">Do not use the <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType> method with native images.</span></span> <span data-ttu-id="25e80-210">Obraz załadowany za pomocą tej metody nie może być używany przez inne zestawy w kontekście wykonywania.</span><span class="sxs-lookup"><span data-stu-id="25e80-210">An image loaded with this method cannot be used by other assemblies in the execution context.</span></span>

<span data-ttu-id="25e80-211">Program Ngen.exe utrzymuje licznik zależności.</span><span class="sxs-lookup"><span data-stu-id="25e80-211">Ngen.exe maintains a count on dependencies.</span></span> <span data-ttu-id="25e80-212">Załóżmy na przykład, że `MyAssembly.exe` `YourAssembly.exe` są one zainstalowane w pamięci podręcznej obrazów natywnych, i oba zawierają odwołania do `OurDependency.dll` .</span><span class="sxs-lookup"><span data-stu-id="25e80-212">For example, suppose `MyAssembly.exe` and `YourAssembly.exe` are both installed in the native image cache, and both have references to `OurDependency.dll`.</span></span> <span data-ttu-id="25e80-213">Jeśli `MyAssembly.exe` program zostanie odinstalowany, `OurDependency.dll` nie zostanie odinstalowany.</span><span class="sxs-lookup"><span data-stu-id="25e80-213">If `MyAssembly.exe` is uninstalled, `OurDependency.dll` is not uninstalled.</span></span> <span data-ttu-id="25e80-214">Jest on usuwany tylko wtedy, gdy `YourAssembly.exe` jest również odinstalowywany.</span><span class="sxs-lookup"><span data-stu-id="25e80-214">It is only removed when `YourAssembly.exe` is also uninstalled.</span></span>

<span data-ttu-id="25e80-215">Jeśli jest generowany obraz natywny dla zestawu przechowywanego w globalnej pamięci podręcznej zestawów, należy określić jego nazwę wyświetlaną.</span><span class="sxs-lookup"><span data-stu-id="25e80-215">If you are generating a native image for an assembly in the global assembly cache, specify its display name.</span></span> <span data-ttu-id="25e80-216">Zobacz: <xref:System.Reflection.Assembly.FullName%2A?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="25e80-216">See <xref:System.Reflection.Assembly.FullName%2A?displayProperty=nameWithType>.</span></span>

<span data-ttu-id="25e80-217">Obrazy natywne, które generuje program Ngen.exe, mogą być współużytkowane w różnych domenach aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25e80-217">The native images that Ngen.exe generates can be shared across application domains.</span></span> <span data-ttu-id="25e80-218">Oznacza to, że można używać programu Ngen.exe w scenariuszach aplikacji, które wymagają współużytkowania zestawów w różnych domenach aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25e80-218">This means you can use Ngen.exe in application scenarios that require assemblies to be shared across application domains.</span></span> <span data-ttu-id="25e80-219">Aby określić neutralność domeny:</span><span class="sxs-lookup"><span data-stu-id="25e80-219">To specify domain neutrality:</span></span>

- <span data-ttu-id="25e80-220">Zastosuj <xref:System.LoaderOptimizationAttribute> atrybut do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25e80-220">Apply the <xref:System.LoaderOptimizationAttribute> attribute to your application.</span></span>

- <span data-ttu-id="25e80-221">Ustaw <xref:System.AppDomainSetup.LoaderOptimization%2A?displayProperty=nameWithType> Właściwość podczas tworzenia informacji o konfiguracji dla nowej domeny aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25e80-221">Set the <xref:System.AppDomainSetup.LoaderOptimization%2A?displayProperty=nameWithType> property when you create setup information for a new application domain.</span></span>

<span data-ttu-id="25e80-222">Zawsze należy używać kodu neutralnego względem domeny podczas ładowania jego zestawu do wielu domen aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25e80-222">Always use domain-neutral code when loading the same assembly into multiple application domains.</span></span> <span data-ttu-id="25e80-223">Jeśli obraz natywny zostanie załadowany do niewspółużytkowanej domeny aplikacji po załadowaniu do domeny współużytkowanej, nie będzie można go użyć.</span><span class="sxs-lookup"><span data-stu-id="25e80-223">If a native image is loaded into a nonshared application domain after having been loaded into a shared domain, it cannot be used.</span></span>

> [!NOTE]
> <span data-ttu-id="25e80-224">Kod neutralny względem domeny nie może zostać zwolniony i wydajność może być nieco niższa, szczególnie w przypadku uzyskiwania dostępu do statycznych elementów członkowskich.</span><span class="sxs-lookup"><span data-stu-id="25e80-224">Domain-neutral code cannot be unloaded, and performance may be slightly slower, particularly when accessing static members.</span></span>

<span data-ttu-id="25e80-225">W tej sekcji uwag:</span><span class="sxs-lookup"><span data-stu-id="25e80-225">In this Remarks section:</span></span>

- [<span data-ttu-id="25e80-226">Generowanie obrazów dla różnych scenariuszy</span><span class="sxs-lookup"><span data-stu-id="25e80-226">Generating images for different scenarios</span></span>](#Scenarios)

- [<span data-ttu-id="25e80-227">Ustalanie, kiedy należy używać obrazów natywnych</span><span class="sxs-lookup"><span data-stu-id="25e80-227">Determining when to Use native images</span></span>](#WhenToUse)

  - [<span data-ttu-id="25e80-228">Ulepszone użycie pamięci</span><span class="sxs-lookup"><span data-stu-id="25e80-228">Improved memory use</span></span>](#Memory)

  - [<span data-ttu-id="25e80-229">Szybsze uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="25e80-229">Faster application startup</span></span>](#Startup)

  - [<span data-ttu-id="25e80-230">Podsumowanie zagadnień dotyczących użycia</span><span class="sxs-lookup"><span data-stu-id="25e80-230">Summary of usage considerations</span></span>](#UsageSummary)

- [<span data-ttu-id="25e80-231">Ważność adresów podstawowych zestawu</span><span class="sxs-lookup"><span data-stu-id="25e80-231">Importance of assembly base addresses</span></span>](#BaseAddresses)

- [<span data-ttu-id="25e80-232">Twarde powiązanie</span><span class="sxs-lookup"><span data-stu-id="25e80-232">Hard binding</span></span>](#HardBinding)

  - [<span data-ttu-id="25e80-233">Określanie wskazówki dotyczącej powiązań dla zależności</span><span class="sxs-lookup"><span data-stu-id="25e80-233">Specifying a binding hint for a dependency</span></span>](#DependencyHint)

  - [<span data-ttu-id="25e80-234">Określanie domyślnej wskazówki dotyczącej powiązań dla zestawu</span><span class="sxs-lookup"><span data-stu-id="25e80-234">Specifying a default binding hint for an assembly</span></span>](#AssemblyHint)

- [<span data-ttu-id="25e80-235">Przetwarzanie Odroczone</span><span class="sxs-lookup"><span data-stu-id="25e80-235">Deferred processing</span></span>](#Deferred)

- [<span data-ttu-id="25e80-236">Obrazy natywne i kompilacja JIT</span><span class="sxs-lookup"><span data-stu-id="25e80-236">Native images and JIT compilation</span></span>](#JITCompilation)

  - [<span data-ttu-id="25e80-237">Nieprawidłowe obrazy</span><span class="sxs-lookup"><span data-stu-id="25e80-237">Invalid images</span></span>](#InvalidImages)

- [<span data-ttu-id="25e80-238">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="25e80-238">Troubleshooting</span></span>](#Troubleshooting)

  - [<span data-ttu-id="25e80-239">podgląd dziennika powiązań zestawów</span><span class="sxs-lookup"><span data-stu-id="25e80-239">Assembly Binding Log Viewer</span></span>](#Fusion)

  - [<span data-ttu-id="25e80-240">Asystent debugowania zarządzanego JITCompilationStart</span><span class="sxs-lookup"><span data-stu-id="25e80-240">The JITCompilationStart managed debugging assistant</span></span>](#MDA)

  - [<span data-ttu-id="25e80-241">Rezygnacja z generowania obrazu natywnego</span><span class="sxs-lookup"><span data-stu-id="25e80-241">Opting out of native image generation</span></span>](#OptOut)

<a name="Scenarios"></a>

## <a name="generating-images-for-----different-scenarios"></a><span data-ttu-id="25e80-242">Generowanie obrazów dla różnych scenariuszy</span><span class="sxs-lookup"><span data-stu-id="25e80-242">Generating images for     different scenarios</span></span>

<span data-ttu-id="25e80-243">Po wygenerowaniu obrazu natywnego zestawu środowisko uruchomieniowe automatycznie próbuje zlokalizować i używać tego obrazu natywnego przy każdym uruchomieniu zestawu.</span><span class="sxs-lookup"><span data-stu-id="25e80-243">After you have generated a native image for an assembly, the runtime automatically attempts to locate and use this native   image each time it runs the assembly.</span></span> <span data-ttu-id="25e80-244">W zależności od scenariuszy użycia można generować wiele obrazów.</span><span class="sxs-lookup"><span data-stu-id="25e80-244">Multiple images can be generated, depending on usage scenarios.</span></span>

<span data-ttu-id="25e80-245">Na przykład w przypadku uruchomienia zestawu w scenariuszu debugowania lub profilowania środowisko uruchomieniowe szuka obrazu natywnego, który został wygenerowany przy użyciu `/Debug` `/Profile` opcji lub.</span><span class="sxs-lookup"><span data-stu-id="25e80-245">For example, if you run an assembly in a debugging or profiling scenario, the runtime looks for a native image that was generated with the `/Debug` or `/Profile` options.</span></span> <span data-ttu-id="25e80-246">Jeśli nie można odnaleźć pasującego obrazu natywnego, środowisko uruchomieniowe przywraca standardową kompilację JIT.</span><span class="sxs-lookup"><span data-stu-id="25e80-246">If it is unable to find a matching native image, the runtime reverts to standard JIT compilation.</span></span> <span data-ttu-id="25e80-247">Jedynym sposobem debugowania obrazów natywnych jest utworzenie obrazu natywnego z `/Debug` opcją.</span><span class="sxs-lookup"><span data-stu-id="25e80-247">The only way to debug native images is to create a native image with the `/Debug` option.</span></span>

<span data-ttu-id="25e80-248">`uninstall`Akcja rozpoznaje również scenariusze, dzięki czemu można odinstalować wszystkie scenariusze lub tylko wybrane scenariusze.</span><span class="sxs-lookup"><span data-stu-id="25e80-248">The `uninstall` action also recognize scenarios, so you can uninstall all scenarios or only selected scenarios.</span></span>

<a name="WhenToUse"></a>

## <a name="determining-when-to-use-native-images"></a><span data-ttu-id="25e80-249">Ustalanie, kiedy należy używać obrazów natywnych</span><span class="sxs-lookup"><span data-stu-id="25e80-249">Determining when to Use native images</span></span>

<span data-ttu-id="25e80-250">Obrazy natywne zapewniają poprawę wydajności w dwóch obszarach: ulepszone wykorzystanie pamięci i skrócenie czasu uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="25e80-250">Native images can provide performance improvements in two areas: improved memory use and reduced startup time.</span></span>

> [!NOTE]
> <span data-ttu-id="25e80-251">Wydajność obrazów natywnych zależy od kilku czynników, które utrudniają analizę, takich jak wzorce dostępu kodu i danych, liczba wywołań, jakie miały miejsce między granicami modułów, a także liczba zależności, które zostały już załadowane przez inne aplikacje.</span><span class="sxs-lookup"><span data-stu-id="25e80-251">Performance of native images depends on a number of factors that make analysis difficult, such as code and data access patterns, how many calls are made across module boundaries, and how many dependencies have already been loaded by other applications.</span></span> <span data-ttu-id="25e80-252">Jedynym sposobem ustalenia, czy obrazy natywne przynoszą korzyść aplikacji, są dokładne pomiary wydajności w kluczowych scenariuszach wdrażania.</span><span class="sxs-lookup"><span data-stu-id="25e80-252">The only way to determine whether native images benefit your application is by careful performance measurements in your key deployment scenarios.</span></span>

<a name="Memory"></a>

### <a name="improved-memory-use"></a><span data-ttu-id="25e80-253">Ulepszone użycie pamięci</span><span class="sxs-lookup"><span data-stu-id="25e80-253">Improved memory use</span></span>

<span data-ttu-id="25e80-254">Obrazy natywne mogą znacznie poprawić wykorzystanie pamięci, gdy kod jest współużytkowany w różnych procesach.</span><span class="sxs-lookup"><span data-stu-id="25e80-254">Native images can significantly improve memory use when code is shared between processes.</span></span> <span data-ttu-id="25e80-255">Obrazy natywne są plikami środowiska Windows PE, więc pojedyncza kopia pliku dll może być współużytkowana przez wiele procesów, natomiast kod natywny wytworzony przez kompilator JIT jest przechowywany w pamięci prywatnej i nie może być współużytkowany.</span><span class="sxs-lookup"><span data-stu-id="25e80-255">Native images are Windows PE files, so a single copy of a .dll file can be shared by multiple processes; by contrast, native code produced by the JIT compiler is stored in private memory and cannot be shared.</span></span>

<span data-ttu-id="25e80-256">Aplikacje uruchamiane w ramach usług terminalowych również mogą korzystać z udostępnionych stron kodowych.</span><span class="sxs-lookup"><span data-stu-id="25e80-256">Applications that are run under terminal services can also benefit from shared code pages.</span></span>

<span data-ttu-id="25e80-257">Ponadto rezygnacja z ładowania kompilatora JIT umożliwia oszczędzenie określonej ilości pamięci dla każdego wystąpienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25e80-257">In addition, not loading the JIT compiler saves a fixed amount of memory for each application instance.</span></span>

<a name="Startup"></a>

### <a name="faster-application-startup"></a><span data-ttu-id="25e80-258">Szybsze uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="25e80-258">Faster application startup</span></span>

<span data-ttu-id="25e80-259">Wstępna kompilacja zestawów przy użyciu programu Ngen.exe może poprawić czas uruchamiania niektórych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25e80-259">Precompiling assemblies with Ngen.exe can improve the startup time for some applications.</span></span> <span data-ttu-id="25e80-260">Ogólnie rzecz biorąc, współużytkowanie zestawów składnika przez aplikacje przynosi zyski, ponieważ po uruchomieniu pierwszej aplikacji składniki współużytkowane są już załadowane dla kolejnych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25e80-260">In general, gains can be made when applications share component assemblies because after the first application has been started the shared components are already loaded for subsequent applications.</span></span> <span data-ttu-id="25e80-261">Podczas zimnego uruchamiania nie występują takie zyski z wykorzystania obrazów natywnych, ponieważ każdy zestaw aplikacji musi zostać załadowany z dysku twardego, przez co czas dostępu do dysku twardego przeważa zyski ze współużytkowania.</span><span class="sxs-lookup"><span data-stu-id="25e80-261">Cold startup, in which all the assemblies in an application must be loaded from the hard disk, does not benefit as much from native images because the hard disk access time predominates.</span></span>

<span data-ttu-id="25e80-262">Trwałe powiązania mogą wpływać na czas uruchamiania, ponieważ wszystkie obrazy trwale powiązane z głównym zestawem aplikacji muszą zostać załadowane w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="25e80-262">Hard binding can affect startup time, because all images that are hard bound to the main application assembly must be loaded at the same time.</span></span>

> [!NOTE]
> <span data-ttu-id="25e80-263">Przed .NET Framework 3,5 z dodatkiem Service Pack 1 należy umieścić udostępnione, silnie nazwane składniki w globalnej pamięci podręcznej zestawów, ponieważ moduł ładujący wykonuje dodatkową weryfikację w przypadku zestawów o silnych nazwach, które nie znajdują się w globalnej pamięci podręcznej zestawów, co skutecznie eliminuje wszelką poprawę czasu uruchamiania uzyskaną za pomocą obrazów natywnych.</span><span class="sxs-lookup"><span data-stu-id="25e80-263">Before the .NET Framework 3.5 Service Pack 1, you should put shared, strong-named components in the global assembly cache, because the loader performs extra validation on strong-named assemblies that are not in the global assembly cache, effectively eliminating any improvement in startup time gained by using native images.</span></span> <span data-ttu-id="25e80-264">Optymalizacje wprowadzone w .NET Framework 3,5 z dodatkiem SP1 spowodowały usunięcie dodatkowej weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="25e80-264">Optimizations that were introduced in the .NET Framework 3.5 SP1 removed the extra validation.</span></span>

<a name="UsageSummary"></a>

### <a name="summary-of-usage-considerations"></a><span data-ttu-id="25e80-265">Podsumowanie zagadnień dotyczących użycia</span><span class="sxs-lookup"><span data-stu-id="25e80-265">Summary of usage considerations</span></span>

<span data-ttu-id="25e80-266">Następujące zagadnienia ogólne i dotyczące aplikacji mogą pomóc zadecydować, czy warto używać obrazów natywnych dla swojej aplikacji:</span><span class="sxs-lookup"><span data-stu-id="25e80-266">The following general considerations and application considerations may assist you in deciding whether to undertake the effort of evaluating native images for your application:</span></span>

- <span data-ttu-id="25e80-267">Obrazy natywne są ładowane szybciej niż pliki MSIL, ponieważ eliminują potrzebę wykonywania wielu działań podczas uruchamiania, takich jak kompilacja JIT i weryfikacja bezpieczeństwa typów.</span><span class="sxs-lookup"><span data-stu-id="25e80-267">Native images load faster than MSIL because they eliminate the need for many startup activities, such as JIT compilation and type-safety verification.</span></span>

- <span data-ttu-id="25e80-268">Obrazy natywne wymagają mniejszego początkowego zestawu roboczego, ponieważ nie ma potrzeby wczytywania kompilatora JIT.</span><span class="sxs-lookup"><span data-stu-id="25e80-268">Native images require a smaller initial working set because there is no need for the JIT compiler.</span></span>

- <span data-ttu-id="25e80-269">Obrazy natywne umożliwiają współużytkowanie kodu przez różne procesy.</span><span class="sxs-lookup"><span data-stu-id="25e80-269">Native images enable code sharing between processes.</span></span>

- <span data-ttu-id="25e80-270">Obrazy natywne wymagają więcej miejsca na dysku twardym niż zestawy MSIL, a ich generowanie może długo trwać.</span><span class="sxs-lookup"><span data-stu-id="25e80-270">Native images require more hard disk space than MSIL assemblies and may require considerable time to generate.</span></span>

- <span data-ttu-id="25e80-271">Obrazy natywne muszą być obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="25e80-271">Native images must be maintained.</span></span>

  - <span data-ttu-id="25e80-272">Obrazy muszą być generowane ponownie, gdy oryginalny zestaw lub jedna z jego zależności jest zmieniana.</span><span class="sxs-lookup"><span data-stu-id="25e80-272">Images need to be regenerated when the original assembly or one of its dependencies is serviced.</span></span>

  - <span data-ttu-id="25e80-273">Pojedynczy zestaw może wymagać wielu obrazów natywnych, aby można było używać go w różnych aplikacjach lub scenariuszach.</span><span class="sxs-lookup"><span data-stu-id="25e80-273">A single assembly may need multiple native images for use in different applications or different scenarios.</span></span> <span data-ttu-id="25e80-274">Na przykład informacje o konfiguracji w dwóch aplikacjach mogą powodować różne decyzje dotyczące powiązań dla tego samego zestawu zależnego.</span><span class="sxs-lookup"><span data-stu-id="25e80-274">For example, the configuration information in two applications might result in different binding decisions for the same dependent assembly.</span></span>

  - <span data-ttu-id="25e80-275">Obrazy natywne muszą być generowane przez administratora, czyli za pomocą konta systemu Windows z grupy Administratorzy.</span><span class="sxs-lookup"><span data-stu-id="25e80-275">Native images must be generated by an administrator; that is, from a Windows account in the Administrators group.</span></span>

<span data-ttu-id="25e80-276">Podczas określania, czy obrazy natywne mogą spowodować poprawę wydajności, oprócz tych ogólnych zagadnień, należy też rozważyć naturę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25e80-276">In addition to these general considerations, the nature of your application must be considered when determining whether native images might provide a performance benefit:</span></span>

- <span data-ttu-id="25e80-277">Jeśli aplikacja działa w środowisku, w którym jest używanych wiele współużytkowanych składników, obrazy natywne umożliwią współużytkowanie składników przez wiele procesów.</span><span class="sxs-lookup"><span data-stu-id="25e80-277">If your application runs in an environment that uses many shared components, native images allow the components to be shared by multiple processes.</span></span>

- <span data-ttu-id="25e80-278">Jeśli aplikacja używa wielu domen aplikacji, obrazy natywne umożliwią współużytkowanie stron kodu w różnych domenach.</span><span class="sxs-lookup"><span data-stu-id="25e80-278">If your application uses multiple application domains, native images allow code pages to be shared across domains.</span></span>

    > [!NOTE]
    > <span data-ttu-id="25e80-279">W wersjach 1.0 i 1.1 programu .NET Framework obrazów natywnych nie można współużytkować w różnych domenach aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25e80-279">In the .NET Framework versions 1.0 and 1.1, native images cannot be shared across application domains.</span></span> <span data-ttu-id="25e80-280">Inaczej jest w wersji 2.0 i późniejszych.</span><span class="sxs-lookup"><span data-stu-id="25e80-280">This is not the case in version 2.0 or later.</span></span>

- <span data-ttu-id="25e80-281">Jeśli aplikacja będzie uruchamiana na serwerze terminali, obrazy natywne umożliwią współużytkowanie stron kodu.</span><span class="sxs-lookup"><span data-stu-id="25e80-281">If your application will be run under Terminal Server, native images allow sharing of code pages.</span></span>

- <span data-ttu-id="25e80-282">Zazwyczaj korzystne jest kompilowanie do obrazów natywnych dużych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25e80-282">Large applications generally benefit from compilation to native images.</span></span> <span data-ttu-id="25e80-283">Taka kompilacja małych aplikacje zazwyczaj nie przynosi korzyści.</span><span class="sxs-lookup"><span data-stu-id="25e80-283">Small applications generally do not benefit.</span></span>

- <span data-ttu-id="25e80-284">W przypadku aplikacji działających przez długi czas kompilacja JIT w czasie wykonywania sprawdza się nieco lepiej niż obrazy natywne.</span><span class="sxs-lookup"><span data-stu-id="25e80-284">For long-running applications, run-time JIT compilation performs slightly better than native images.</span></span> <span data-ttu-id="25e80-285">(Trwałe powiązania mogą do pewnego stopnia złagodzić różnicę w wydajności).</span><span class="sxs-lookup"><span data-stu-id="25e80-285">(Hard binding can mitigate this performance difference to some degree.)</span></span>

<a name="BaseAddresses"></a>

## <a name="importance-of-assembly-base-addresses"></a><span data-ttu-id="25e80-286">Ważność adresów podstawowych zestawu</span><span class="sxs-lookup"><span data-stu-id="25e80-286">Importance of assembly base addresses</span></span>

<span data-ttu-id="25e80-287">Obrazy natywne są plikami środowiska Windows PE, więc dotyczą ich te same problemy zmiany podstawy, co innych plików wykonywalnych.</span><span class="sxs-lookup"><span data-stu-id="25e80-287">Because native images are Windows PE files, they are subject to the same rebasing issues as other executable files.</span></span> <span data-ttu-id="25e80-288">Spadek wydajności przy relokacji jest jeszcze bardziej widoczny, jeśli są stosowane powiązania trwałe.</span><span class="sxs-lookup"><span data-stu-id="25e80-288">The performance cost of relocation is even more pronounced if hard binding is employed.</span></span>

<span data-ttu-id="25e80-289">Aby ustawić adres podstawowy dla obrazu natywnego, należy użyć odpowiedniej opcji kompilatora, aby ustawić adres podstawowy dla zestawu.</span><span class="sxs-lookup"><span data-stu-id="25e80-289">To set the base address for a native image, use the appropriate option of your compiler to set the base address for the assembly.</span></span> <span data-ttu-id="25e80-290">Program Ngen.exe używa tego adresu podstawowego dla obrazu natywnego.</span><span class="sxs-lookup"><span data-stu-id="25e80-290">Ngen.exe uses this base address for the native image.</span></span>

> [!NOTE]
> <span data-ttu-id="25e80-291">Obrazy natywne są większe niż zestawy zarządzane, na podstawie których zostały utworzone.</span><span class="sxs-lookup"><span data-stu-id="25e80-291">Native images are larger than the managed assemblies from which they were created.</span></span> <span data-ttu-id="25e80-292">Adresy podstawowe muszą być obliczane tak, aby zezwalały na te większe rozmiary.</span><span class="sxs-lookup"><span data-stu-id="25e80-292">Base addresses must be calculated to allow for these larger sizes.</span></span>

<span data-ttu-id="25e80-293">Można użyć narzędzia, takiego jak dumpbin.exe, aby wyświetlić preferowany adres podstawowy obrazu natywnego.</span><span class="sxs-lookup"><span data-stu-id="25e80-293">You can use a tool such as dumpbin.exe to view the preferred base address of a native image.</span></span>

<a name="HardBinding"></a>

## <a name="hard-binding"></a><span data-ttu-id="25e80-294">Twarde powiązanie</span><span class="sxs-lookup"><span data-stu-id="25e80-294">Hard binding</span></span>

<span data-ttu-id="25e80-295">Trwałe powiązania zwiększają przepustowość i zmniejszają rozmiar zestawu roboczego dla obrazów natywnych.</span><span class="sxs-lookup"><span data-stu-id="25e80-295">Hard binding increases throughput and reduces working set size for native images.</span></span> <span data-ttu-id="25e80-296">Wadą trwałych powiązań jest fakt, że wszystkie obrazy, które są trwale powiązane z zestawem, muszą być ładowane razem z zestawem.</span><span class="sxs-lookup"><span data-stu-id="25e80-296">The disadvantage of hard binding is that all the images that are hard bound to an assembly must be loaded when the assembly is loaded.</span></span> <span data-ttu-id="25e80-297">Może to znacznie zwiększyć czas uruchamiania dużych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25e80-297">This can significantly increase startup time for a large application.</span></span>

<span data-ttu-id="25e80-298">Trwałe powiązanie jest odpowiednie dla zależności, które są ładowane we wszystkich krytycznych pod względem wydajności scenariuszach aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25e80-298">Hard binding is appropriate for dependencies that are loaded in all your application's performance-critical scenarios.</span></span> <span data-ttu-id="25e80-299">Podobnie jak w przypadku każdego aspektu wykorzystania obrazu natywnego, staranne wykonywanie pomiarów wydajności jest jedynym sposobem ustalenia, czy trwałe powiązanie zwiększa wydajność aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25e80-299">As with any aspect of native image use, careful performance measurements are the only way to determine whether hard binding improves your application's performance.</span></span>

<span data-ttu-id="25e80-300"><xref:System.Runtime.CompilerServices.DependencyAttribute>Atrybuty i <xref:System.Runtime.CompilerServices.DefaultDependencyAttribute> umożliwiają udostępnianie twardych wskazówek do Ngen.exe.</span><span class="sxs-lookup"><span data-stu-id="25e80-300">The <xref:System.Runtime.CompilerServices.DependencyAttribute> and <xref:System.Runtime.CompilerServices.DefaultDependencyAttribute> attributes allow you to provide hard binding hints to Ngen.exe.</span></span>

> [!NOTE]
> <span data-ttu-id="25e80-301">Te atrybuty są wskazówkami dla programu Ngen.exe, a nie poleceniami.</span><span class="sxs-lookup"><span data-stu-id="25e80-301">These attributes are hints to Ngen.exe, not commands.</span></span> <span data-ttu-id="25e80-302">Użycie ich nie gwarantuje uzyskania trwałego powiązania.</span><span class="sxs-lookup"><span data-stu-id="25e80-302">Using them does not guarantee hard binding.</span></span> <span data-ttu-id="25e80-303">Znaczenie tych atrybutów może się zmieniać w przyszłych wersjach.</span><span class="sxs-lookup"><span data-stu-id="25e80-303">The meaning of these attributes may change in future releases.</span></span>

<a name="DependencyHint"></a>

### <a name="specifying-a-binding-hint-for-a-dependency"></a><span data-ttu-id="25e80-304">Określanie wskazówki dotyczącej powiązań dla zależności</span><span class="sxs-lookup"><span data-stu-id="25e80-304">Specifying a binding hint for a dependency</span></span>

<span data-ttu-id="25e80-305">Zastosuj <xref:System.Runtime.CompilerServices.DependencyAttribute> do zestawu, aby wskazać prawdopodobieństwo, że zostanie załadowana określona zależność.</span><span class="sxs-lookup"><span data-stu-id="25e80-305">Apply the <xref:System.Runtime.CompilerServices.DependencyAttribute> to an assembly to indicate the likelihood that a specified dependency will be loaded.</span></span> <span data-ttu-id="25e80-306"><xref:System.Runtime.CompilerServices.LoadHint.Always?displayProperty=nameWithType> wskazuje, że stałe powiązanie jest odpowiednie, <xref:System.Runtime.CompilerServices.LoadHint.Default> wskazuje, że wartość domyślna dla zależności powinna być używana i <xref:System.Runtime.CompilerServices.LoadHint.Sometimes> wskazuje, że twarde powiązanie nie jest odpowiednie.</span><span class="sxs-lookup"><span data-stu-id="25e80-306"><xref:System.Runtime.CompilerServices.LoadHint.Always?displayProperty=nameWithType> indicates that hard binding is appropriate, <xref:System.Runtime.CompilerServices.LoadHint.Default> indicates that the default for the dependency should be used, and <xref:System.Runtime.CompilerServices.LoadHint.Sometimes> indicates that hard binding is not appropriate.</span></span>

<span data-ttu-id="25e80-307">Poniższy kod pokazuje atrybuty dla zestawu mającego dwie zależności.</span><span class="sxs-lookup"><span data-stu-id="25e80-307">The following code shows the attributes for an assembly that has two dependencies.</span></span> <span data-ttu-id="25e80-308">Pierwsza zależność (Assembly1) jest odpowiednim kandydatem dla trwałego powiązania, ale druga zależność (Assembly2) nie jest.</span><span class="sxs-lookup"><span data-stu-id="25e80-308">The first dependency (Assembly1) is an appropriate candidate for hard binding, and the second (Assembly2) is not.</span></span>

```vb
Imports System.Runtime.CompilerServices
<Assembly:DependencyAttribute("Assembly1", LoadHint.Always)>
<Assembly:DependencyAttribute("Assembly2", LoadHint.Sometimes)>
```

```csharp
using System.Runtime.CompilerServices;
[assembly:DependencyAttribute("Assembly1", LoadHint.Always)]
[assembly:DependencyAttribute("Assembly2", LoadHint.Sometimes)]
```

```cpp
using namespace System::Runtime::CompilerServices;
[assembly:DependencyAttribute("Assembly1", LoadHint.Always)];
[assembly:DependencyAttribute("Assembly2", LoadHint.Sometimes)];
```

<span data-ttu-id="25e80-309">Nazwa zestawu nie zawiera rozszerzenia nazwy pliku.</span><span class="sxs-lookup"><span data-stu-id="25e80-309">The assembly name does not include the file name extension.</span></span> <span data-ttu-id="25e80-310">Można używać nazw wyświetlanych.</span><span class="sxs-lookup"><span data-stu-id="25e80-310">Display names can be used.</span></span>

<a name="AssemblyHint"></a>

### <a name="specifying-a-default-binding-hint-for-an-assembly"></a><span data-ttu-id="25e80-311">Określanie domyślnej wskazówki dotyczącej powiązań dla zestawu</span><span class="sxs-lookup"><span data-stu-id="25e80-311">Specifying a default binding hint for an assembly</span></span>

<span data-ttu-id="25e80-312">Domyślne wskazówki powiązania potrzebne są tylko zestawom, które będą stosowane natychmiastowo i często przez dowolną aplikację, która jest od nich zależna.</span><span class="sxs-lookup"><span data-stu-id="25e80-312">Default binding hints are only needed for assemblies that will be used immediately and frequently by any application that has a dependency on them.</span></span> <span data-ttu-id="25e80-313">Zastosuj <xref:System.Runtime.CompilerServices.DefaultDependencyAttribute> <xref:System.Runtime.CompilerServices.LoadHint.Always?displayProperty=nameWithType> do takich zestawów, aby określić, że twarde powiązanie ma być używane.</span><span class="sxs-lookup"><span data-stu-id="25e80-313">Apply the <xref:System.Runtime.CompilerServices.DefaultDependencyAttribute> with <xref:System.Runtime.CompilerServices.LoadHint.Always?displayProperty=nameWithType> to such assemblies to specify that hard binding should be used.</span></span>

> [!NOTE]
> <span data-ttu-id="25e80-314">Nie ma powodów zastosowania <xref:System.Runtime.CompilerServices.DefaultDependencyAttribute> do zestawów dll, które nie należą do tej kategorii, ponieważ stosowanie atrybutu z jakąkolwiek wartością inną niż <xref:System.Runtime.CompilerServices.LoadHint.Always?displayProperty=nameWithType> ma ten sam efekt, co nie ma zastosowania atrybutu.</span><span class="sxs-lookup"><span data-stu-id="25e80-314">There is no reason to apply <xref:System.Runtime.CompilerServices.DefaultDependencyAttribute> to .dll assemblies that do not fall into this category, because applying the attribute with any value other than <xref:System.Runtime.CompilerServices.LoadHint.Always?displayProperty=nameWithType> has the same effect as not applying the attribute at all.</span></span>

<span data-ttu-id="25e80-315">Firma Microsoft korzysta z programu, <xref:System.Runtime.CompilerServices.DefaultDependencyAttribute> Aby określić, że stałe powiązanie jest wartością domyślną dla bardzo niewielkiej liczby zestawów w .NET Framework, takich jak mscorlib.dll.</span><span class="sxs-lookup"><span data-stu-id="25e80-315">Microsoft uses the <xref:System.Runtime.CompilerServices.DefaultDependencyAttribute> to specify that hard binding is the default for a very small number of assemblies in the .NET Framework, such as mscorlib.dll.</span></span>

<a name="Deferred"></a>

## <a name="deferred-processing"></a><span data-ttu-id="25e80-316">Przetwarzanie Odroczone</span><span class="sxs-lookup"><span data-stu-id="25e80-316">Deferred processing</span></span>

<span data-ttu-id="25e80-317">Generowanie obrazów natywnych dla bardzo dużych aplikacji może zająć znaczną ilość czasu.</span><span class="sxs-lookup"><span data-stu-id="25e80-317">Generation of native images for a very large application can take considerable time.</span></span> <span data-ttu-id="25e80-318">Podobnie zmiany składnika współużytkowanego lub zmiany w ustawieniach komputera mogą wymagać aktualizacji wielu obrazów natywnych.</span><span class="sxs-lookup"><span data-stu-id="25e80-318">Similarly, changes to a shared component or changes to computer settings might require many native images to be updated.</span></span> <span data-ttu-id="25e80-319">`install`Akcje i `update` mają `/queue` opcję, która kolejkuje operację dla odroczonego wykonania przez usługę obrazu natywnego.</span><span class="sxs-lookup"><span data-stu-id="25e80-319">The `install` and `update` actions have a `/queue` option that queues the operation for deferred execution by the native image service.</span></span> <span data-ttu-id="25e80-320">Ponadto Ngen.exe ma `queue` i `executeQueuedItems` działania, które zapewniają kontrolę nad usługą.</span><span class="sxs-lookup"><span data-stu-id="25e80-320">In addition, Ngen.exe has `queue` and `executeQueuedItems` actions that provide some control over the service.</span></span> <span data-ttu-id="25e80-321">Aby uzyskać więcej informacji, zobacz [Native Image Service](#native-image-service).</span><span class="sxs-lookup"><span data-stu-id="25e80-321">For more information, see [Native Image Service](#native-image-service).</span></span>

<a name="JITCompilation"></a>

## <a name="native-images-and-jit-compilation"></a><span data-ttu-id="25e80-322">Obrazy natywne i kompilacja JIT</span><span class="sxs-lookup"><span data-stu-id="25e80-322">Native images and JIT compilation</span></span>

<span data-ttu-id="25e80-323">Jeśli program Ngen.exe napotka w zestawie jakiekolwiek metody, których nie może wygenerować, wyklucza je z obrazu natywnego.</span><span class="sxs-lookup"><span data-stu-id="25e80-323">If Ngen.exe encounters any methods in an assembly that it cannot generate, it excludes them from the native image.</span></span> <span data-ttu-id="25e80-324">Gdy środowisko uruchomieniowe wykonuje zestaw, przywraca kompilację JIT dla metod, które nie zostały uwzględnione w obrazie natywnym.</span><span class="sxs-lookup"><span data-stu-id="25e80-324">When the runtime executes this assembly, it reverts to JIT compilation for the methods that were not included in the native image.</span></span>

<span data-ttu-id="25e80-325">Ponadto obrazy natywne nie są używane, jeśli zestaw został uaktualniony lub jeśli obraz został unieważniony z jakiegokolwiek powodu.</span><span class="sxs-lookup"><span data-stu-id="25e80-325">In addition, native images are not used if the assembly has been upgraded, or if the image has been invalidated for any reason.</span></span>

<a name="InvalidImages"></a>

### <a name="invalid-images"></a><span data-ttu-id="25e80-326">Nieprawidłowe obrazy</span><span class="sxs-lookup"><span data-stu-id="25e80-326">Invalid images</span></span>

<span data-ttu-id="25e80-327">Użycie programu Ngen.exe w celu utworzenia obrazu natywnego zestawu powoduje, że dane wyjściowe zależą od opcji wiersza polecenia, które można określić, i niektórych ustawień na komputerze.</span><span class="sxs-lookup"><span data-stu-id="25e80-327">When you use Ngen.exe to create a native image of an assembly, the output depends upon the command-line options that you specify and certain settings on your computer.</span></span> <span data-ttu-id="25e80-328">Są to m.in. następujące ustawienia:</span><span class="sxs-lookup"><span data-stu-id="25e80-328">These settings include the following:</span></span>

- <span data-ttu-id="25e80-329">Wersja programu .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="25e80-329">The version of the .NET Framework.</span></span>

- <span data-ttu-id="25e80-330">Wersja systemu operacyjnego, jeśli zmiana pochodzi z rodziny Windows 9X do rodziny systemu Windows NT.</span><span class="sxs-lookup"><span data-stu-id="25e80-330">The version of the operating system, if the change is from the Windows 9x family to the Windows NT family.</span></span>

- <span data-ttu-id="25e80-331">Dokładna tożsamość zestawu (ponowna kompilacja zmienia tożsamość).</span><span class="sxs-lookup"><span data-stu-id="25e80-331">The exact identity of the assembly (recompilation changes identity).</span></span>

- <span data-ttu-id="25e80-332">Dokładna tożsamość wszystkich zestawów, do których odwołuje się zestaw (ponowna kompilacja zmienia tożsamość).</span><span class="sxs-lookup"><span data-stu-id="25e80-332">The exact identity of all assemblies that the assembly references (recompilation changes identity).</span></span>

- <span data-ttu-id="25e80-333">Czynniki związane z zabezpieczeniami.</span><span class="sxs-lookup"><span data-stu-id="25e80-333">Security factors.</span></span>

<span data-ttu-id="25e80-334">Program Ngen.exe rejestruje te informacje podczas generowania obrazu natywnego.</span><span class="sxs-lookup"><span data-stu-id="25e80-334">Ngen.exe records this information when it generates a native image.</span></span> <span data-ttu-id="25e80-335">Podczas wykonywania zestawu środowisko uruchomieniowe poszukuje obrazu natywnego wygenerowanego z użyciem opcji i ustawień, które odpowiadają bieżącemu środowisku komputera.</span><span class="sxs-lookup"><span data-stu-id="25e80-335">When you execute an assembly, the runtime looks for the native image generated with options and settings that match the computer's current environment.</span></span> <span data-ttu-id="25e80-336">Jeśli nie można odnaleźć pasującego obrazu natywnego, środowisko uruchomieniowe przywraca kompilację JIT zestawu.</span><span class="sxs-lookup"><span data-stu-id="25e80-336">The runtime reverts to JIT compilation of an assembly if it cannot find a matching native image.</span></span> <span data-ttu-id="25e80-337">Następujące zmiany w ustawieniach komputera i środowiska powodują, że obrazy natywne stają się nieprawidłowe:</span><span class="sxs-lookup"><span data-stu-id="25e80-337">The following changes to a computer's settings and environment cause native images to become invalid:</span></span>

- <span data-ttu-id="25e80-338">Wersja programu .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="25e80-338">The version of the .NET Framework.</span></span>

     <span data-ttu-id="25e80-339">Jeśli zastosowano aktualizację programu .NET Framework, wszystkie obrazy natywne utworzone przy użyciu programu Ngen.exe stają się nieprawidłowe.</span><span class="sxs-lookup"><span data-stu-id="25e80-339">If you apply an update to the .NET Framework, all native images that you have created using Ngen.exe become invalid.</span></span> <span data-ttu-id="25e80-340">Z tego powodu wszystkie aktualizacje .NET Framework wykonać `Ngen Update` polecenie, aby upewnić się, że wszystkie obrazy natywne zostaną ponownie wygenerowane.</span><span class="sxs-lookup"><span data-stu-id="25e80-340">For this reason, all updates of the .NET Framework execute the `Ngen Update` command, to ensure that all native images are regenerated.</span></span> <span data-ttu-id="25e80-341">Program .NET Framework automatycznie tworzy nowe obrazy natywne dla bibliotek programu .NET Framework, które instaluje.</span><span class="sxs-lookup"><span data-stu-id="25e80-341">The .NET Framework automatically creates new native images for the .NET Framework libraries that it installs.</span></span>

- <span data-ttu-id="25e80-342">Wersja systemu operacyjnego, jeśli zmiana pochodzi z rodziny Windows 9X do rodziny systemu Windows NT.</span><span class="sxs-lookup"><span data-stu-id="25e80-342">The version of the operating system, if the change is from the Windows 9x family to the Windows NT family.</span></span>

     <span data-ttu-id="25e80-343">Na przykład jeśli wersja systemu operacyjnego działającego na komputerze zmienia się z systemu Windows 98 na system Windows XP, wszystkie obrazy natywne przechowywane w pamięci podręcznej obrazów natywnych staną się nieprawidłowe.</span><span class="sxs-lookup"><span data-stu-id="25e80-343">For example, if the version of the operating system running on a computer changes from Windows 98 to Windows XP, all native images stored in the native image cache become invalid.</span></span> <span data-ttu-id="25e80-344">Jeśli jednak system operacyjny ulegnie zmianie z systemu Windows 2000 do systemu Windows XP, obrazy nie zostaną unieważnione.</span><span class="sxs-lookup"><span data-stu-id="25e80-344">However, if the operating system changes from Windows 2000 to Windows XP, the images are not invalidated.</span></span>

- <span data-ttu-id="25e80-345">Dokładna tożsamość zestawu.</span><span class="sxs-lookup"><span data-stu-id="25e80-345">The exact identity of the assembly.</span></span>

     <span data-ttu-id="25e80-346">Jeśli zestaw zostanie ponownie skompilowany, obraz natywny odpowiadający zestawowi staje się nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="25e80-346">If you recompile an assembly, the assembly's corresponding native image becomes invalid.</span></span>

- <span data-ttu-id="25e80-347">Dokładna tożsamość jakichkolwiek zestawów, do których odwołuje się zestaw.</span><span class="sxs-lookup"><span data-stu-id="25e80-347">The exact identity of any assemblies the assembly references.</span></span>

     <span data-ttu-id="25e80-348">Jeżeli zestaw zarządzany zostanie zaktualizowany, wszystkie obrazy natywne zależne bezpośrednio lub pośrednio od tego zestawu stają się nieprawidłowe i muszą zostać wygenerowane ponownie.</span><span class="sxs-lookup"><span data-stu-id="25e80-348">If you update a managed assembly, all native images that directly or indirectly depend on that assembly become invalid and need to be regenerated.</span></span> <span data-ttu-id="25e80-349">Obejmuje to zarówno zwykłe odwołania, jak i trwale powiązane zależności.</span><span class="sxs-lookup"><span data-stu-id="25e80-349">This includes both ordinary references and hard-bound dependencies.</span></span> <span data-ttu-id="25e80-350">Za każdym razem, gdy aktualizacja oprogramowania zostanie zastosowana, program instalacyjny powinien wykonać `Ngen Update` polecenie, aby upewnić się, że wszystkie zależne obrazy natywne zostaną ponownie wygenerowane.</span><span class="sxs-lookup"><span data-stu-id="25e80-350">Whenever a software update is applied, the installation program should execute an `Ngen Update` command to ensure that all dependent native images are regenerated.</span></span>

- <span data-ttu-id="25e80-351">Czynniki związane z zabezpieczeniami.</span><span class="sxs-lookup"><span data-stu-id="25e80-351">Security factors.</span></span>

     <span data-ttu-id="25e80-352">Zmiana zasad zabezpieczeń komputera ograniczająca uprawnienia udzielone uprzednio zestawowi może spowodować, że poprzednio skompilowane obrazy natywne dla tego zestawu staną się nieprawidłowe.</span><span class="sxs-lookup"><span data-stu-id="25e80-352">Changing machine security policy to restrict permissions previously granted to an assembly can cause a previously compiled native image for that assembly to become invalid.</span></span>

     <span data-ttu-id="25e80-353">Aby uzyskać szczegółowe informacje na temat sposobu, w jaki środowisko uruchomieniowe języka wspólnego administruje zabezpieczeniami dostępu kodu i jak korzystać z uprawnień, zobacz [zabezpieczenia dostępu kodu](../misc/code-access-security.md).</span><span class="sxs-lookup"><span data-stu-id="25e80-353">For detailed information about how the common language runtime administers code access security and how to use permissions, see [Code Access Security](../misc/code-access-security.md).</span></span>

<a name="Troubleshooting"></a>

## <a name="troubleshooting"></a><span data-ttu-id="25e80-354">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="25e80-354">Troubleshooting</span></span>

<span data-ttu-id="25e80-355">Poniższe tematy dotyczące rozwiązywania problemów umożliwiają sprawdzenie, które obrazy natywne są używane i które nie mogą być używane przez aplikację, aby określić, kiedy kompilator JIT zaczyna kompilować metodę, i pokazuje, jak zrezygnować z kompilacji obrazu natywnego określonych metod.</span><span class="sxs-lookup"><span data-stu-id="25e80-355">The following troubleshooting topics allow you to see which native images are being used and which cannot be used by your application, to determine when the JIT compiler starts to compile a method, and shows how to opt out of native image compilation of specified methods.</span></span>

<a name="Fusion"></a>

### <a name="assembly-binding-log-viewer"></a><span data-ttu-id="25e80-356">podgląd dziennika powiązań zestawów</span><span class="sxs-lookup"><span data-stu-id="25e80-356">Assembly Binding Log Viewer</span></span>

<span data-ttu-id="25e80-357">Aby upewnić się, że obrazy natywne są używane przez aplikację, można użyć [Fuslogvw.exe (Podgląd dziennika powiązań zestawów)](fuslogvw-exe-assembly-binding-log-viewer.md).</span><span class="sxs-lookup"><span data-stu-id="25e80-357">To confirm that native images are being used by your application, you can use the [Fuslogvw.exe (Assembly Binding Log Viewer)](fuslogvw-exe-assembly-binding-log-viewer.md).</span></span> <span data-ttu-id="25e80-358">Wybierz opcję **obrazy natywne** w polu **kategorie dzienników** w oknie Przeglądarka dzienników powiązań.</span><span class="sxs-lookup"><span data-stu-id="25e80-358">Select **Native Images** in the **Log Categories** box on the binding log viewer window.</span></span> <span data-ttu-id="25e80-359">Program Fuslogvw.exe dostarcza informacje o tym, dlaczego obraz natywny został odrzucony.</span><span class="sxs-lookup"><span data-stu-id="25e80-359">Fuslogvw.exe provides information about why a native image was rejected.</span></span>

<a name="MDA"></a>

### <a name="the-jitcompilationstart-managed-debugging-assistant"></a><span data-ttu-id="25e80-360">Asystent debugowania zarządzanego JITCompilationStart</span><span class="sxs-lookup"><span data-stu-id="25e80-360">The JITCompilationStart managed debugging assistant</span></span>

<span data-ttu-id="25e80-361">Za pomocą asystenta debugowania zarządzanego [jitCompilationStart](../debug-trace-profile/jitcompilationstart-mda.md) (MDA) można określić, kiedy kompilator JIT zacznie kompilować funkcję.</span><span class="sxs-lookup"><span data-stu-id="25e80-361">You can use the [jitCompilationStart](../debug-trace-profile/jitcompilationstart-mda.md) managed debugging assistant (MDA) to determine when the JIT compiler starts to compile a function.</span></span>

<a name="OptOut"></a>

### <a name="opting-out-of-native-image-generation"></a><span data-ttu-id="25e80-362">Rezygnacja z generowania obrazu natywnego</span><span class="sxs-lookup"><span data-stu-id="25e80-362">Opting out of native image generation</span></span>

<span data-ttu-id="25e80-363">W niektórych przypadkach NGen.exe mogą mieć problemy z generowaniem obrazu natywnego dla konkretnej metody lub można preferować, aby Metoda była skompilowana JIT, a następnie skompilowana do obrazu natywnego.</span><span class="sxs-lookup"><span data-stu-id="25e80-363">In some cases, NGen.exe may have difficulty generating a native image for a specific method, or you may prefer that the method be JIT compiled rather then compiled to a native image.</span></span> <span data-ttu-id="25e80-364">W takim przypadku można użyć `System.Runtime.BypassNGenAttribute` atrybutu, aby uniemożliwić NGen.exe generowania obrazu natywnego dla określonej metody.</span><span class="sxs-lookup"><span data-stu-id="25e80-364">In this case, you can use the `System.Runtime.BypassNGenAttribute` attribute to prevent NGen.exe from generating a native image for a particular method.</span></span> <span data-ttu-id="25e80-365">Ten atrybut musi być zastosowany indywidualnie dla każdej metody, której kod nie ma być dołączony do obrazu natywnego.</span><span class="sxs-lookup"><span data-stu-id="25e80-365">The attribute must be applied individually to each method whose code you do not want to include in the native image.</span></span> <span data-ttu-id="25e80-366">NGen.exe rozpoznaje atrybut i nie generuje kodu w obrazie natywnym dla odpowiadającej metody.</span><span class="sxs-lookup"><span data-stu-id="25e80-366">NGen.exe recognizes the attribute and does not generate code in the native image for the corresponding method.</span></span>

<span data-ttu-id="25e80-367">Należy jednak pamiętać, że `BypassNGenAttribute` nie jest on zdefiniowany jako typ w bibliotece klas .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="25e80-367">Note, however, that `BypassNGenAttribute` is not defined as a type in the .NET Framework Class Library.</span></span> <span data-ttu-id="25e80-368">Aby można było użyć atrybutu w kodzie, należy najpierw zdefiniować go w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="25e80-368">In order to consume the attribute in your code, you must first define it as follows:</span></span>

[!code-csharp[System.Runtime.BypassNGenAttribute#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/System.Runtime.BypassNGenAttribute/cs/Optout1.cs#1)]
[!code-vb[System.Runtime.BypassNGenAttribute#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/System.Runtime.BypassNGenAttribute/vb/Optout1.vb#1)]

<span data-ttu-id="25e80-369">Następnie można zastosować atrybut dla poszczególnych metod.</span><span class="sxs-lookup"><span data-stu-id="25e80-369">You can then apply the attribute on a per-method basis.</span></span> <span data-ttu-id="25e80-370">Poniższy przykład instruuje Generator obrazu natywnego, że nie powinien generować obrazu natywnego dla `ExampleClass.ToJITCompile` metody.</span><span class="sxs-lookup"><span data-stu-id="25e80-370">The following example instructs the Native Image Generator that it should not generate a native image for the `ExampleClass.ToJITCompile` method.</span></span>

[!code-csharp[System.Runtime.BypassNGenAttribute#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/System.Runtime.BypassNGenAttribute/cs/Optout1.cs#2)]
[!code-vb[System.Runtime.BypassNGenAttribute#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/System.Runtime.BypassNGenAttribute/vb/Optout1.vb#2)]

## <a name="examples"></a><span data-ttu-id="25e80-371">Przykłady</span><span class="sxs-lookup"><span data-stu-id="25e80-371">Examples</span></span>

<span data-ttu-id="25e80-372">Następujące polecenie generuje obraz natywny dla `ClientApp.exe` , znajdujący się w bieżącym katalogu i instaluje obraz w pamięci podręcznej obrazów natywnych.</span><span class="sxs-lookup"><span data-stu-id="25e80-372">The following command generates a native image for `ClientApp.exe`, located in the current directory, and installs the image in the native image cache.</span></span> <span data-ttu-id="25e80-373">Jeśli istnieje plik konfiguracji zestawu, program Ngen.exe go użyje.</span><span class="sxs-lookup"><span data-stu-id="25e80-373">If a configuration file exists for the assembly, Ngen.exe uses it.</span></span> <span data-ttu-id="25e80-374">Ponadto obrazy natywne są generowane dla dowolnych plików DLL, `ClientApp.exe` do których odwołuje się.</span><span class="sxs-lookup"><span data-stu-id="25e80-374">In addition, native images are generated for any .dll files that `ClientApp.exe` references.</span></span>

```console
ngen install ClientApp.exe
```

<span data-ttu-id="25e80-375">Obraz instalowany za pomocą programu Ngen.exe jest również nazywany elementem głównym.</span><span class="sxs-lookup"><span data-stu-id="25e80-375">An image installed with Ngen.exe is also called a root.</span></span> <span data-ttu-id="25e80-376">Elementem głównym może być aplikacja albo składnik współużytkowany.</span><span class="sxs-lookup"><span data-stu-id="25e80-376">A root can be an application or a shared component.</span></span>

<span data-ttu-id="25e80-377">Następujące polecenie generuje obraz natywny dla `MyAssembly.exe` określonej ścieżki.</span><span class="sxs-lookup"><span data-stu-id="25e80-377">The following command generates a native image for `MyAssembly.exe` with the specified path.</span></span>

```console
ngen install c:\myfiles\MyAssembly.exe
```

<span data-ttu-id="25e80-378">Podczas lokalizowania zestawów i ich zależności program Ngen.exe używa tej samej logiki badania, co środowisko uruchomieniowe języka wspólnego (CLR).</span><span class="sxs-lookup"><span data-stu-id="25e80-378">When locating assemblies and their dependencies, Ngen.exe uses the same probing logic used by the common language runtime.</span></span> <span data-ttu-id="25e80-379">Domyślnie katalog, który zawiera, `ClientApp.exe` jest używany jako katalog podstawowy aplikacji, a wszystkie sondy zestawu zaczynają się w tym katalogu.</span><span class="sxs-lookup"><span data-stu-id="25e80-379">By default, the directory that contains `ClientApp.exe` is used as the application base directory, and all assembly probing begins in this directory.</span></span> <span data-ttu-id="25e80-380">To zachowanie można zastąpić przy użyciu `/AppBase` opcji.</span><span class="sxs-lookup"><span data-stu-id="25e80-380">You can override this behavior by using the `/AppBase` option.</span></span>

> [!NOTE]
> <span data-ttu-id="25e80-381">Zachowanie to różni się od zachowania programu Ngen.exe w wersjach 1.0 i 1.1 programu .NET Framework, gdzie podstawa aplikacji znajduje się w bieżącym katalogu.</span><span class="sxs-lookup"><span data-stu-id="25e80-381">This is a change from Ngen.exe behavior in the .NET Framework versions 1.0 and 1.1, where the application base is set to the current directory.</span></span>

<span data-ttu-id="25e80-382">Zestaw może mieć zależność bez odwołania, na przykład jeśli ładuje plik DLL za pomocą <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> metody.</span><span class="sxs-lookup"><span data-stu-id="25e80-382">An assembly can have a dependency without a reference, for example if it loads a .dll file by using the <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="25e80-383">Można utworzyć obraz natywny dla takiego pliku dll przy użyciu informacji konfiguracyjnych dla zestawu aplikacji z `/ExeConfig` opcją.</span><span class="sxs-lookup"><span data-stu-id="25e80-383">You can create a native image for such a .dll file by using configuration information for the application assembly, with the `/ExeConfig` option.</span></span> <span data-ttu-id="25e80-384">Następujące polecenie generuje obraz natywny do `MyLib.dll,` użycia informacji o konfiguracji z programu `MyApp.exe` .</span><span class="sxs-lookup"><span data-stu-id="25e80-384">The following command generates a native image for `MyLib.dll,` using the configuration information from `MyApp.exe`.</span></span>

```console
ngen install c:\myfiles\MyLib.dll /ExeConfig:c:\myapps\MyApp.exe
```

<span data-ttu-id="25e80-385">Zestawy instalowane w ten sposób nie są usuwane, gdy jest usuwana aplikacja.</span><span class="sxs-lookup"><span data-stu-id="25e80-385">Assemblies installed in this way are not removed when the application is removed.</span></span>

<span data-ttu-id="25e80-386">Aby odinstalować zależność, należy użyć tych samych opcji wiersza polecenia, które zostały użyte podczas jej instalowania.</span><span class="sxs-lookup"><span data-stu-id="25e80-386">To uninstall a dependency, use the same command-line options that were used to install it.</span></span> <span data-ttu-id="25e80-387">Poniższe polecenie Odinstalowuje `MyLib.dll` z poprzedniego przykładu.</span><span class="sxs-lookup"><span data-stu-id="25e80-387">The following command uninstalls the `MyLib.dll` from the previous example.</span></span>

```console
ngen uninstall c:\myfiles\MyLib.dll /ExeConfig:c:\myapps\MyApp.exe
```

<span data-ttu-id="25e80-388">Aby utworzyć obraz natywny dla zestawu w globalnej pamięci podręcznej zestawów, należy użyć nazwy wyświetlanej zestawu.</span><span class="sxs-lookup"><span data-stu-id="25e80-388">To create a native image for an assembly in the global assembly cache, use the display name of the assembly.</span></span> <span data-ttu-id="25e80-389">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="25e80-389">For example:</span></span>

```console
ngen install "ClientApp, Version=1.0.0.0, Culture=neutral,
  PublicKeyToken=3c7ba247adcd2081, processorArchitecture=MSIL"
```

<span data-ttu-id="25e80-390">Program NGen.exe generuje oddzielny zestaw obrazów dla każdego instalowanego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="25e80-390">NGen.exe generates a separate set of images for each scenario you install.</span></span> <span data-ttu-id="25e80-391">Na przykład poniższe polecenia instalują kompletny zestaw obrazów natywnych dla normalnych operacji, drugi kompletny zestaw na potrzeby debugowania i trzeci na potrzeby profilowania:</span><span class="sxs-lookup"><span data-stu-id="25e80-391">For example, the following commands install a complete set of native images for normal operation, another complete set for debugging, and a third for profiling:</span></span>

```console
ngen install MyApp.exe
ngen install MyApp.exe /debug
ngen install MyApp.exe /profile
```

### <a name="displaying-the-native-image-cache"></a><span data-ttu-id="25e80-392">Wyświetlanie pamięci podręcznej obrazów natywnych</span><span class="sxs-lookup"><span data-stu-id="25e80-392">Displaying the Native Image Cache</span></span>

<span data-ttu-id="25e80-393">Obrazy natywne zainstalowane w pamięci podręcznej można wyświetlić przy użyciu programu Ngen.exe.</span><span class="sxs-lookup"><span data-stu-id="25e80-393">Once native images are installed in the cache, they can be displayed using Ngen.exe.</span></span> <span data-ttu-id="25e80-394">Poniższe polecenie wyświetla wszystkie obrazy natywne znajdujące się w pamięci podręcznej obrazów natywnych.</span><span class="sxs-lookup"><span data-stu-id="25e80-394">The following command displays all native images in the native image cache.</span></span>

```console
ngen display
```

<span data-ttu-id="25e80-395">`display`Akcja najpierw wyświetla listę wszystkich zestawów głównych, a następnie listę wszystkich obrazów natywnych na komputerze.</span><span class="sxs-lookup"><span data-stu-id="25e80-395">The `display` action lists all the root assemblies first, followed by a list of all the native images on the computer.</span></span>

<span data-ttu-id="25e80-396">Prosta nazwa zestawu służy do wyświetlania informacji dotyczących tylko tego zestawu.</span><span class="sxs-lookup"><span data-stu-id="25e80-396">Use the simple name of an assembly to display information only for that assembly.</span></span> <span data-ttu-id="25e80-397">Następujące polecenie wyświetla wszystkie obrazy natywne w pamięci podręcznej obrazów natywnych, które pasują do nazwy częściowej `MyAssembly` , ich zależności i wszystkich elementów głównych, które mają zależność od `MyAssembly` :</span><span class="sxs-lookup"><span data-stu-id="25e80-397">The following command displays all native images in the native image cache that match the partial name `MyAssembly`, their dependencies, and all roots that have a dependency on `MyAssembly`:</span></span>

```console
ngen display MyAssembly
```

<span data-ttu-id="25e80-398">Znajomość tego, jakie elementy główne są zależne od zestawu współużytkowanego składnika, jest przydatna w oceny wpływu `update` akcji po uaktualnieniu składnika współużytkowanego.</span><span class="sxs-lookup"><span data-stu-id="25e80-398">Knowing what roots depend on a shared component assembly is useful in gauging the impact of an `update` action after the shared component is upgraded.</span></span>

<span data-ttu-id="25e80-399">Aby określić rozszerzenie pliku zestawu, należy określić ścieżkę lub wykonać program Ngen.exe z katalogu zawierającego zestaw:</span><span class="sxs-lookup"><span data-stu-id="25e80-399">If you specify an assembly's file extension, you must either specify the path or execute Ngen.exe from the directory containing the assembly:</span></span>

```console
ngen display c:\myApps\MyAssembly.exe
```

<span data-ttu-id="25e80-400">Następujące polecenie wyświetla wszystkie obrazy natywne w pamięci podręcznej obrazów natywnych o nazwie `MyAssembly` i wersji 1.0.0.0.</span><span class="sxs-lookup"><span data-stu-id="25e80-400">The following command displays all native images in the native image cache with the name `MyAssembly` and the version 1.0.0.0.</span></span>

```console
ngen display "myAssembly, version=1.0.0.0"
```

### <a name="updating-images"></a><span data-ttu-id="25e80-401">Aktualizacja obrazów</span><span class="sxs-lookup"><span data-stu-id="25e80-401">Updating Images</span></span>

<span data-ttu-id="25e80-402">Obrazy są zazwyczaj aktualizowane po uaktualnieniu składnika współużytkowanego.</span><span class="sxs-lookup"><span data-stu-id="25e80-402">Images are typically updated after a shared component has been upgraded.</span></span> <span data-ttu-id="25e80-403">Aby zaktualizować wszystkie obrazy natywne, które uległy zmianie lub których zależności uległy zmianie, użyj `update` akcji bez argumentów.</span><span class="sxs-lookup"><span data-stu-id="25e80-403">To update all native images that have changed, or whose dependencies have changed, use the `update` action with no arguments.</span></span>

```console
ngen update
```

<span data-ttu-id="25e80-404">Aktualizacja wszystkich obrazów może być długotrwałym procesem.</span><span class="sxs-lookup"><span data-stu-id="25e80-404">Updating all images can be a lengthy process.</span></span> <span data-ttu-id="25e80-405">Można kolejkować aktualizacje do wykonania przez usługę obrazu macierzystego przy użyciu `/queue` opcji.</span><span class="sxs-lookup"><span data-stu-id="25e80-405">You can queue the updates for execution by the native image service by using the `/queue` option.</span></span> <span data-ttu-id="25e80-406">Aby uzyskać więcej informacji na temat `/queue` opcji i priorytetów instalacji, zobacz [Native Image Service](#native-image-service).</span><span class="sxs-lookup"><span data-stu-id="25e80-406">For more information on the `/queue` option and installation priorities, see [Native Image Service](#native-image-service).</span></span>

```console
ngen update /queue
```

### <a name="uninstalling-images"></a><span data-ttu-id="25e80-407">Odinstalowywanie obrazów</span><span class="sxs-lookup"><span data-stu-id="25e80-407">Uninstalling Images</span></span>

<span data-ttu-id="25e80-408">Program Ngen.exe utrzymuje listę zależności, aby składniki współużytkowane były usuwane tylko wtedy, gdy wszystkie zestawy, które od nich zależą, zostały usunięte.</span><span class="sxs-lookup"><span data-stu-id="25e80-408">Ngen.exe maintains a list of dependencies, so that shared components are removed only when all assemblies that depend on them have been removed.</span></span> <span data-ttu-id="25e80-409">Ponadto współużytkowany składnik nie zostanie usunięty, jeśli został zainstalowany jako element główny.</span><span class="sxs-lookup"><span data-stu-id="25e80-409">In addition, a shared component is not removed if it has been installed as a root.</span></span>

<span data-ttu-id="25e80-410">Następujące polecenie Odinstalowuje wszystkie scenariusze dla katalogu głównego `ClientApp.exe` :</span><span class="sxs-lookup"><span data-stu-id="25e80-410">The following command uninstalls all scenarios for the root `ClientApp.exe`:</span></span>

```console
ngen uninstall ClientApp
```

<span data-ttu-id="25e80-411">`uninstall`Akcja może służyć do usuwania konkretnych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="25e80-411">The `uninstall` action can be used to remove specific scenarios.</span></span> <span data-ttu-id="25e80-412">Następujące polecenie Odinstalowuje wszystkie scenariusze debugowania dla `ClientApp.exe` :</span><span class="sxs-lookup"><span data-stu-id="25e80-412">The following command uninstalls all debug scenarios for `ClientApp.exe`:</span></span>

```console
ngen uninstall ClientApp /debug
```

> [!NOTE]
> <span data-ttu-id="25e80-413">Odinstalowywanie `/debug` scenariuszy nie powoduje odinstalowania scenariusza, który obejmuje zarówno `/profile` , jak i `/debug.`</span><span class="sxs-lookup"><span data-stu-id="25e80-413">Uninstalling `/debug` scenarios does not uninstall a scenario that includes both `/profile` and `/debug.`</span></span>

<span data-ttu-id="25e80-414">Następujące polecenie Odinstalowuje wszystkie scenariusze dla określonej wersji programu `ClientApp.exe` :</span><span class="sxs-lookup"><span data-stu-id="25e80-414">The following command uninstalls all scenarios for a specific version of `ClientApp.exe`:</span></span>

```console
ngen uninstall "ClientApp, Version=1.0.0.0"
```

<span data-ttu-id="25e80-415">Następujące polecenia Odinstalowuje wszystkie scenariusze dla `"ClientApp, Version=1.0.0.0, Culture=neutral, PublicKeyToken=3c7ba247adcd2081, processorArchitecture=MSIL",` lub tylko scenariusz debugowania dla tego zestawu:</span><span class="sxs-lookup"><span data-stu-id="25e80-415">The following commands uninstall all scenarios for `"ClientApp, Version=1.0.0.0, Culture=neutral, PublicKeyToken=3c7ba247adcd2081, processorArchitecture=MSIL",` or just the debug scenario for that assembly:</span></span>

```console
ngen uninstall "ClientApp, Version=1.0.0.0, Culture=neutral,
  PublicKeyToken=3c7ba247adcd2081, processorArchitecture=MSIL"
ngen uninstall "ClientApp, Version=1.0.0.0, Culture=neutral,
  PublicKeyToken=3c7ba247adcd2081, processorArchitecture=MSIL" /debug
```

<span data-ttu-id="25e80-416">Podobnie jak w przypadku `install` akcji, dostarczenie rozszerzenia wymaga wykonania Ngen.exe z katalogu zawierającego zestaw lub określenia pełnej ścieżki.</span><span class="sxs-lookup"><span data-stu-id="25e80-416">As with the `install` action, supplying an extension requires either executing Ngen.exe from the directory containing the assembly or specifying a full path.</span></span>

<span data-ttu-id="25e80-417">Aby zapoznać się z przykładami dotyczącymi usługi obrazów natywnych, zobacz [Native Image Service](#native-image-service).</span><span class="sxs-lookup"><span data-stu-id="25e80-417">For examples relating to the native image service, see [Native Image Service](#native-image-service).</span></span>

## <a name="native-image-task"></a><span data-ttu-id="25e80-418">Obraz macierzysty — zadanie</span><span class="sxs-lookup"><span data-stu-id="25e80-418">Native Image Task</span></span>

<span data-ttu-id="25e80-419">Zadanie obrazu natywnego to zadanie systemu Windows, które generuje i utrzymuje obrazy natywne.</span><span class="sxs-lookup"><span data-stu-id="25e80-419">The native image task is a Windows task that generates and maintains native images.</span></span> <span data-ttu-id="25e80-420">Zadanie obrazu natywnego generuje i automatycznie przejmuje obrazy natywne dla obsługiwanych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="25e80-420">The native image task generates and reclaims native images automatically for supported scenarios.</span></span> <span data-ttu-id="25e80-421">Umożliwia także instalatorom używanie [Ngen.exe (Generator obrazu natywnego)](ngen-exe-native-image-generator.md) do tworzenia i aktualizowania obrazów natywnych w odłożonym czasie.</span><span class="sxs-lookup"><span data-stu-id="25e80-421">It also enables installers to use [Ngen.exe (Native Image Generator)](ngen-exe-native-image-generator.md) to create and update native images at a deferred time.</span></span>

<span data-ttu-id="25e80-422">Zadanie obrazu natywnego jest rejestrowane raz dla każdej architektury procesora obsługiwanej na komputerze, aby umożliwić kompilację dla aplikacji przeznaczonych dla każdej architektury:</span><span class="sxs-lookup"><span data-stu-id="25e80-422">The native image task is registered once for each CPU architecture supported on a computer, to allow compilation for applications that target each architecture:</span></span>

|<span data-ttu-id="25e80-423">Nazwa zadania</span><span class="sxs-lookup"><span data-stu-id="25e80-423">Task name</span></span>|<span data-ttu-id="25e80-424">32-bitowy komputer</span><span class="sxs-lookup"><span data-stu-id="25e80-424">32-bit computer</span></span>|<span data-ttu-id="25e80-425">64-bitowy komputer</span><span class="sxs-lookup"><span data-stu-id="25e80-425">64-bit computer</span></span>|
|---------------|----------------------|----------------------|
|<span data-ttu-id="25e80-426">.NET Framework NGEN v 4.0.30319</span><span class="sxs-lookup"><span data-stu-id="25e80-426">NET Framework NGEN v4.0.30319</span></span>|<span data-ttu-id="25e80-427">Yes</span><span class="sxs-lookup"><span data-stu-id="25e80-427">Yes</span></span>|<span data-ttu-id="25e80-428">Yes</span><span class="sxs-lookup"><span data-stu-id="25e80-428">Yes</span></span>|
|<span data-ttu-id="25e80-429">.NET Framework NGEN v 4.0.30319 64</span><span class="sxs-lookup"><span data-stu-id="25e80-429">NET Framework NGEN v4.0.30319 64</span></span>|<span data-ttu-id="25e80-430">Nie</span><span class="sxs-lookup"><span data-stu-id="25e80-430">No</span></span>|<span data-ttu-id="25e80-431">Yes</span><span class="sxs-lookup"><span data-stu-id="25e80-431">Yes</span></span>|

<span data-ttu-id="25e80-432">Zadanie obrazu natywnego jest dostępne w .NET Framework 4,5 i nowszych wersjach, gdy działa w systemie Windows 8 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="25e80-432">The native image task is available in the .NET Framework 4.5 and later versions, when running on Windows 8 or later.</span></span> <span data-ttu-id="25e80-433">We wcześniejszych wersjach systemu Windows .NET Framework używa [usługi obrazów natywnych](#native-image-service).</span><span class="sxs-lookup"><span data-stu-id="25e80-433">On earlier versions of Windows, the .NET Framework uses the [Native Image Service](#native-image-service).</span></span>

### <a name="task-lifetime"></a><span data-ttu-id="25e80-434">Okres istnienia zadania</span><span class="sxs-lookup"><span data-stu-id="25e80-434">Task Lifetime</span></span>

<span data-ttu-id="25e80-435">Ogólnie rzecz biorąc, Harmonogram zadań systemu Windows uruchamia zadanie obrazu natywnego co noc, gdy komputer jest w stanie bezczynności.</span><span class="sxs-lookup"><span data-stu-id="25e80-435">In general, the Windows Task Scheduler starts the native image task every night when the computer is idle.</span></span> <span data-ttu-id="25e80-436">Zadanie sprawdza wszystkie odroczone zadania, które są umieszczane w kolejce przez instalatorów aplikacji, wszystkie odroczone żądania aktualizacji obrazów natywnych i wszelkie automatyczne tworzenie obrazu.</span><span class="sxs-lookup"><span data-stu-id="25e80-436">The task checks for any deferred work that is queued by application installers, any deferred native image update requests, and any automatic image creation.</span></span> <span data-ttu-id="25e80-437">Zadanie kończy zaległe elementy robocze, a następnie zamyka.</span><span class="sxs-lookup"><span data-stu-id="25e80-437">The task completes outstanding work items and then shuts down.</span></span> <span data-ttu-id="25e80-438">Jeśli komputer przestanie być bezczynny, gdy zadanie jest uruchomione, zadanie zostanie zatrzymane.</span><span class="sxs-lookup"><span data-stu-id="25e80-438">If the computer stops being idle while the task is running, the task stops.</span></span>

<span data-ttu-id="25e80-439">Możesz również ręcznie uruchomić zadanie natywnego obrazu za pomocą interfejsu użytkownika Harmonogram zadań lub ręcznie, aby NGen.exe.</span><span class="sxs-lookup"><span data-stu-id="25e80-439">You can also start the native image task manually through the Task Scheduler UI or through manual calls to NGen.exe.</span></span> <span data-ttu-id="25e80-440">Jeśli zadanie zostało rozpoczęte za pomocą jednej z tych metod, będzie ono nadal działać, gdy komputer nie będzie już w stanie bezczynności.</span><span class="sxs-lookup"><span data-stu-id="25e80-440">If the task is started through either of these methods, it will continue running when the computer is no longer idle.</span></span> <span data-ttu-id="25e80-441">Obrazy tworzone ręcznie przy użyciu NGen.exe są ustalane według priorytetów, aby umożliwić przewidywalne zachowanie dla instalatorów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25e80-441">Images created manually by using NGen.exe are prioritized to enable predictable behavior for application installers.</span></span>

## <a name="native-image-service"></a><span data-ttu-id="25e80-442">Usługa obrazu macierzystego</span><span class="sxs-lookup"><span data-stu-id="25e80-442">Native Image Service</span></span>

<span data-ttu-id="25e80-443">Natywna usługa obrazów to usługa systemu Windows, która generuje i utrzymuje obrazy natywne.</span><span class="sxs-lookup"><span data-stu-id="25e80-443">The native image service is a Windows service that generates and maintains native images.</span></span> <span data-ttu-id="25e80-444">Usługa obrazów natywnych umożliwia deweloperom odroczenie instalacji i aktualizacji obrazów natywnych na okresy, gdy komputer jest w stanie bezczynności.</span><span class="sxs-lookup"><span data-stu-id="25e80-444">The native image service allows the developer to defer the installation and update of native images to periods when the computer is idle.</span></span>

<span data-ttu-id="25e80-445">Zwykle usługa obrazów natywnych jest inicjowana przez program instalacyjny (Instalator) dla aplikacji lub aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="25e80-445">Normally, the native image service is initiated by the installation program (installer) for an application or update.</span></span> <span data-ttu-id="25e80-446">W przypadku akcji o priorytecie 3 usługa jest wykonywana w czasie bezczynności na komputerze.</span><span class="sxs-lookup"><span data-stu-id="25e80-446">For priority 3 actions, the service executes during idle time on the computer.</span></span> <span data-ttu-id="25e80-447">Usługa zapisuje swój stan i umożliwia kontynuowanie wielu ponownych uruchomień, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="25e80-447">The service saves its state and is capable of continuing through multiple reboots if necessary.</span></span> <span data-ttu-id="25e80-448">Kompilacja wielu obrazów może być umieszczona w kolejce.</span><span class="sxs-lookup"><span data-stu-id="25e80-448">Multiple image compilations can be queued.</span></span>

<span data-ttu-id="25e80-449">Usługa współdziała również z ręcznym Ngen.exe poleceniem.</span><span class="sxs-lookup"><span data-stu-id="25e80-449">The service also interacts with the manual Ngen.exe command.</span></span> <span data-ttu-id="25e80-450">Polecenia ręczne mają pierwszeństwo przed działaniami w tle.</span><span class="sxs-lookup"><span data-stu-id="25e80-450">Manual commands take precedence over background activity.</span></span>

> [!NOTE]
> <span data-ttu-id="25e80-451">W systemie Windows Vista Nazwa wyświetlana dla usługi obrazów natywnych to "Microsoft.NET Framework NGEN v 2.0.50727_X86" lub "Microsoft.NET Framework NGEN v 2.0.50727_X64".</span><span class="sxs-lookup"><span data-stu-id="25e80-451">On Windows Vista, the name displayed for the native image service is "Microsoft.NET Framework NGEN v2.0.50727_X86" or "Microsoft.NET Framework NGEN v2.0.50727_X64".</span></span> <span data-ttu-id="25e80-452">We wszystkich wcześniejszych wersjach systemu Microsoft Windows nazwa to "Usługa optymalizacji środowiska uruchomieniowego .NET w wersji 2.0.50727_X86" lub "Optymalizacja środowiska uruchomieniowego .NET w wersji 2.0.50727_X64".</span><span class="sxs-lookup"><span data-stu-id="25e80-452">On all earlier versions of Microsoft Windows, the name is ".NET Runtime Optimization Service v2.0.50727_X86" or ".NET Runtime Optimization Service v2.0.50727_X64".</span></span>

### <a name="launching-deferred-operations"></a><span data-ttu-id="25e80-453">Uruchamianie odroczonych operacji</span><span class="sxs-lookup"><span data-stu-id="25e80-453">Launching Deferred Operations</span></span>

<span data-ttu-id="25e80-454">Przed rozpoczęciem instalacji lub uaktualnienia zaleca się wstrzymywanie usługi.</span><span class="sxs-lookup"><span data-stu-id="25e80-454">Before beginning an installation or upgrade, pausing the service is recommended.</span></span> <span data-ttu-id="25e80-455">Gwarantuje to, że usługa nie zostanie wykonana, podczas gdy Instalator kopiuje pliki lub umieszcza zestawy w globalnej pamięci podręcznej zestawów.</span><span class="sxs-lookup"><span data-stu-id="25e80-455">This ensures that the service does not execute while the installer is copying files or putting assemblies in the global assembly cache.</span></span> <span data-ttu-id="25e80-456">Następujący Ngen.exe wiersz polecenia wstrzymuje usługę:</span><span class="sxs-lookup"><span data-stu-id="25e80-456">The following Ngen.exe command line pauses the service:</span></span>

```console
ngen queue pause
```

<span data-ttu-id="25e80-457">Po dodaniu wszystkich odroczonych operacji do kolejki następujące polecenie umożliwia wznowienie działania usługi:</span><span class="sxs-lookup"><span data-stu-id="25e80-457">When all deferred operations have been queued, the following command allows the service to resume:</span></span>

```console
ngen queue continue
```

<span data-ttu-id="25e80-458">Aby odroczyć generowanie obrazu natywnego podczas instalowania nowej aplikacji lub podczas aktualizowania składnika współużytkowanego, należy użyć `/queue` opcji `install` z `update` akcjami lub.</span><span class="sxs-lookup"><span data-stu-id="25e80-458">To defer native image generation when installing a new application or when updating a shared component, use the `/queue` option with the `install` or `update` actions.</span></span> <span data-ttu-id="25e80-459">Następujące Ngen.exe linie poleceń instalują obraz macierzysty dla składnika współużytkowanego i przeprowadzają aktualizację wszystkich katalogów głównych, które mogły mieć to oddziaływać:</span><span class="sxs-lookup"><span data-stu-id="25e80-459">The following Ngen.exe command lines install a native image for a shared component and perform an update of all roots that may have been affected:</span></span>

```console
ngen install MyComponent /queue
ngen update /queue
```

<span data-ttu-id="25e80-460">`update`Akcja generuje ponownie wszystkie obrazy natywne, które zostały unieważnione, a nie tylko te, które używają `MyComponent` .</span><span class="sxs-lookup"><span data-stu-id="25e80-460">The `update` action regenerates all native images that have been invalidated, not just those that use `MyComponent`.</span></span>

<span data-ttu-id="25e80-461">Jeśli aplikacja składa się z wielu katalogów głównych, można kontrolować priorytet akcji odroczonych.</span><span class="sxs-lookup"><span data-stu-id="25e80-461">If your application consists of many roots, you can control the priority of the deferred actions.</span></span> <span data-ttu-id="25e80-462">Następujące polecenia kolejką instalację trzech katalogów głównych.</span><span class="sxs-lookup"><span data-stu-id="25e80-462">The following commands queue the installation of three roots.</span></span> <span data-ttu-id="25e80-463">`Assembly1` Program jest instalowany jako pierwszy, bez czekania na czas bezczynności.</span><span class="sxs-lookup"><span data-stu-id="25e80-463">`Assembly1` is installed first, without waiting for idle time.</span></span> <span data-ttu-id="25e80-464">`Assembly2` Program jest również instalowany bez oczekiwania na czas bezczynności, ale po zakończeniu wszystkich akcji o priorytecie 1.</span><span class="sxs-lookup"><span data-stu-id="25e80-464">`Assembly2` is also installed without waiting for idle time, but after all priority 1 actions have completed.</span></span> <span data-ttu-id="25e80-465">`Assembly3` Program jest instalowany, gdy usługa wykryje, że komputer jest w stanie bezczynności.</span><span class="sxs-lookup"><span data-stu-id="25e80-465">`Assembly3` is installed when the service detects that the computer is idle.</span></span>

```console
ngen install Assembly1 /queue:1
ngen install Assembly2 /queue:2
ngen install Assembly3 /queue:3
```

<span data-ttu-id="25e80-466">Można wymusić, aby kolejkowane akcje były wykonywane synchronicznie za pomocą `executeQueuedItems` akcji.</span><span class="sxs-lookup"><span data-stu-id="25e80-466">You can force queued actions to occur synchronously by using the `executeQueuedItems` action.</span></span> <span data-ttu-id="25e80-467">W przypadku podania opcjonalnego priorytetu ta akcja ma wpływ tylko na akcje znajdujące się w kolejce, które mają równy lub niższy priorytet.</span><span class="sxs-lookup"><span data-stu-id="25e80-467">If you supply the optional priority, this action affects only the queued actions that have equal or lower priority.</span></span> <span data-ttu-id="25e80-468">Domyślnym priorytetem jest 3, dlatego następujące Ngen.exe polecenie przetwarza natychmiast wszystkie akcje w kolejce i nie zwraca do momentu zakończenia:</span><span class="sxs-lookup"><span data-stu-id="25e80-468">The default priority is 3, so the following Ngen.exe command processes all queued actions immediately, and does not return until they are finished:</span></span>

```console
ngen executeQueuedItems
```

<span data-ttu-id="25e80-469">Polecenia synchroniczne są wykonywane przez Ngen.exe i nie używają natywnej usługi obrazu.</span><span class="sxs-lookup"><span data-stu-id="25e80-469">Synchronous commands are executed by Ngen.exe and do not use the native image service.</span></span> <span data-ttu-id="25e80-470">Akcje można wykonywać przy użyciu Ngen.exe, gdy jest uruchomiona usługa obrazów natywnych.</span><span class="sxs-lookup"><span data-stu-id="25e80-470">You can execute actions using Ngen.exe while the native image service is running.</span></span>

### <a name="service-shutdown"></a><span data-ttu-id="25e80-471">Zamykanie usługi</span><span class="sxs-lookup"><span data-stu-id="25e80-471">Service Shutdown</span></span>

<span data-ttu-id="25e80-472">Po zainicjowaniu przez wykonanie polecenia Ngen.exe, które zawiera `/queue` opcję, usługa jest uruchamiana w tle do momentu zakończenia wszystkich akcji.</span><span class="sxs-lookup"><span data-stu-id="25e80-472">After being initiated by the execution of an Ngen.exe command that includes the `/queue` option, the service runs in the background until all actions have been completed.</span></span> <span data-ttu-id="25e80-473">Usługa zapisuje swój stan, aby umożliwić kontynuowanie wielu ponownych uruchomień, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="25e80-473">The service saves its state so that it can continue through multiple reboots if necessary.</span></span> <span data-ttu-id="25e80-474">Gdy usługa wykryje, że nie ma więcej akcji w kolejce, resetuje jej stan tak, aby nie był uruchamiany ponownie przy następnym uruchomieniu komputera, a następnie zostanie zamknięty.</span><span class="sxs-lookup"><span data-stu-id="25e80-474">When the service detects that there are no more actions queued, it resets its status so that it will not restart the next time the computer is booted, and then it shuts itself down.</span></span>

### <a name="service-interaction-with-clients"></a><span data-ttu-id="25e80-475">Interakcja z klientami usługi</span><span class="sxs-lookup"><span data-stu-id="25e80-475">Service Interaction with Clients</span></span>

<span data-ttu-id="25e80-476">W .NET Framework w wersji 2,0 jedyną interakcją z usługą obrazu natywnego jest za pomocą narzędzia wiersza polecenia Ngen.exe.</span><span class="sxs-lookup"><span data-stu-id="25e80-476">In the .NET Framework version 2.0, the only interaction with the native image service is through the command-line tool Ngen.exe.</span></span> <span data-ttu-id="25e80-477">Użyj narzędzia wiersza polecenia w skryptach instalacyjnych, aby kolejkować akcje dla usługi obrazów natywnych i współdziałać z usługą.</span><span class="sxs-lookup"><span data-stu-id="25e80-477">Use the command-line tool in installation scripts to queue actions for the native image service and to interact with the service.</span></span>

## <a name="see-also"></a><span data-ttu-id="25e80-478">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="25e80-478">See also</span></span>

- [<span data-ttu-id="25e80-479">Narzędzia</span><span class="sxs-lookup"><span data-stu-id="25e80-479">Tools</span></span>](index.md)
- [<span data-ttu-id="25e80-480">Zarządzany proces wykonywania</span><span class="sxs-lookup"><span data-stu-id="25e80-480">Managed Execution Process</span></span>](../../standard/managed-execution-process.md)
- [<span data-ttu-id="25e80-481">Sposoby lokalizowania zestawów przez środowisko uruchomieniowe</span><span class="sxs-lookup"><span data-stu-id="25e80-481">How the Runtime Locates Assemblies</span></span>](../deployment/how-the-runtime-locates-assemblies.md)
- [<span data-ttu-id="25e80-482">Wiersze poleceń</span><span class="sxs-lookup"><span data-stu-id="25e80-482">Command Prompts</span></span>](developer-command-prompt-for-vs.md)
