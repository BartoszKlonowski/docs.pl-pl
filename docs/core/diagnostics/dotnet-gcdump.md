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
# <a name="heap-analysis-tool-dotnet-gcdump"></a><span data-ttu-id="6edf0-103">Narzędzie do analizy sterty (dotnet-gcdump)</span><span class="sxs-lookup"><span data-stu-id="6edf0-103">Heap analysis tool (dotnet-gcdump)</span></span>

<span data-ttu-id="6edf0-104">**Ten artykuł ma zastosowanie do:** ✔️ .net Core 3,1 SDK i nowszych wersjach</span><span class="sxs-lookup"><span data-stu-id="6edf0-104">**This article applies to:** ✔️ .NET Core 3.1 SDK and later versions</span></span>

## <a name="install"></a><span data-ttu-id="6edf0-105">Instalowanie</span><span class="sxs-lookup"><span data-stu-id="6edf0-105">Install</span></span>

<span data-ttu-id="6edf0-106">Istnieją dwa sposoby na pobranie i zainstalowanie `dotnet-gcdump` :</span><span class="sxs-lookup"><span data-stu-id="6edf0-106">There are two ways to download and install `dotnet-gcdump`:</span></span>

- <span data-ttu-id="6edf0-107">**Narzędzie globalne dotnet:**</span><span class="sxs-lookup"><span data-stu-id="6edf0-107">**dotnet global tool:**</span></span>

  <span data-ttu-id="6edf0-108">Aby zainstalować najnowszą wersję `dotnet-gcdump` [pakietu NuGet](https://www.nuget.org/packages/dotnet-gcdump), użyj polecenia [Narzędzia dotnet Install](../tools/dotnet-tool-install.md) :</span><span class="sxs-lookup"><span data-stu-id="6edf0-108">To install the latest release version of the `dotnet-gcdump` [NuGet package](https://www.nuget.org/packages/dotnet-gcdump), use the [dotnet tool install](../tools/dotnet-tool-install.md) command:</span></span>

  ```dotnetcli
  dotnet tool install --global dotnet-gcdump
  ```

- <span data-ttu-id="6edf0-109">**Pobieranie bezpośrednie:**</span><span class="sxs-lookup"><span data-stu-id="6edf0-109">**Direct download:**</span></span>

  <span data-ttu-id="6edf0-110">Pobierz plik wykonywalny narzędzia, który jest zgodny z platformą:</span><span class="sxs-lookup"><span data-stu-id="6edf0-110">Download the tool executable that matches your platform:</span></span>

  | <span data-ttu-id="6edf0-111">System operacyjny</span><span class="sxs-lookup"><span data-stu-id="6edf0-111">OS</span></span>  | <span data-ttu-id="6edf0-112">Platforma</span><span class="sxs-lookup"><span data-stu-id="6edf0-112">Platform</span></span> |
  | --- | -------- |
  | <span data-ttu-id="6edf0-113">Windows</span><span class="sxs-lookup"><span data-stu-id="6edf0-113">Windows</span></span> | <span data-ttu-id="6edf0-114">[x86](https://aka.ms/dotnet-gcdump/win-x86) \| [x64](https://aka.ms/dotnet-gcdump/win-x64) \| [ARM](https://aka.ms/dotnet-gcdump/win-arm) \| [ARM — x64](https://aka.ms/dotnet-gcdump/win-arm64)</span><span class="sxs-lookup"><span data-stu-id="6edf0-114">[x86](https://aka.ms/dotnet-gcdump/win-x86) \| [x64](https://aka.ms/dotnet-gcdump/win-x64) \| [arm](https://aka.ms/dotnet-gcdump/win-arm) \| [arm-x64](https://aka.ms/dotnet-gcdump/win-arm64)</span></span> |
  | <span data-ttu-id="6edf0-115">macOS</span><span class="sxs-lookup"><span data-stu-id="6edf0-115">macOS</span></span>   | [<span data-ttu-id="6edf0-116">x64</span><span class="sxs-lookup"><span data-stu-id="6edf0-116">x64</span></span>](https://aka.ms/dotnet-gcdump/osx-x64) |
  | <span data-ttu-id="6edf0-117">Linux</span><span class="sxs-lookup"><span data-stu-id="6edf0-117">Linux</span></span>   | <span data-ttu-id="6edf0-118">[x64](https://aka.ms/dotnet-gcdump/linux-x64) \| [ARM](https://aka.ms/dotnet-gcdump/linux-arm) \| [arm64](https://aka.ms/dotnet-gcdump/linux-arm64) \| [MUSL — x64](https://aka.ms/dotnet-gcdump/linux-musl-x64) \| [MUSL — arm64](https://aka.ms/dotnet-gcdump/linux-musl-arm64)</span><span class="sxs-lookup"><span data-stu-id="6edf0-118">[x64](https://aka.ms/dotnet-gcdump/linux-x64) \| [arm](https://aka.ms/dotnet-gcdump/linux-arm) \| [arm64](https://aka.ms/dotnet-gcdump/linux-arm64) \| [musl-x64](https://aka.ms/dotnet-gcdump/linux-musl-x64) \| [musl-arm64](https://aka.ms/dotnet-gcdump/linux-musl-arm64)</span></span> |

## <a name="synopsis"></a><span data-ttu-id="6edf0-119">Streszczenie</span><span class="sxs-lookup"><span data-stu-id="6edf0-119">Synopsis</span></span>

```console
dotnet-gcdump [-h|--help] [--version] <command>
```

## <a name="description"></a><span data-ttu-id="6edf0-120">Opis</span><span class="sxs-lookup"><span data-stu-id="6edf0-120">Description</span></span>

<span data-ttu-id="6edf0-121">`dotnet-gcdump`Narzędzie globalne zbiera zrzuty procesów .NET na żywo (Moduł wyrzucania elementów bezużytecznych) za pomocą [EventPipe](./eventpipe.md).</span><span class="sxs-lookup"><span data-stu-id="6edf0-121">The `dotnet-gcdump` global tool collects GC (Garbage Collector) dumps of live .NET processes using [EventPipe](./eventpipe.md).</span></span> <span data-ttu-id="6edf0-122">Zrzuty GC są tworzone przez wyzwolenie GC w procesie docelowym, włączenie zdarzeń specjalnych i ponowne wygenerowanie grafu obiektów głównych obiektu ze strumienia zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="6edf0-122">GC dumps are created by triggering a GC in the target process, turning on special events, and regenerating the graph of object roots from the event stream.</span></span> <span data-ttu-id="6edf0-123">Ten proces umożliwia zbieranie zrzutów GC, gdy proces jest uruchomiony i z minimalnymi kosztami.</span><span class="sxs-lookup"><span data-stu-id="6edf0-123">This process allows for GC dumps to be collected while the process is running and with minimal overhead.</span></span> <span data-ttu-id="6edf0-124">Te zrzuty są przydatne w kilku scenariuszach:</span><span class="sxs-lookup"><span data-stu-id="6edf0-124">These dumps are useful for several scenarios:</span></span>

- <span data-ttu-id="6edf0-125">Porównanie liczby obiektów w stercie w kilku punktach w czasie.</span><span class="sxs-lookup"><span data-stu-id="6edf0-125">Comparing the number of objects on the heap at several points in time.</span></span>
- <span data-ttu-id="6edf0-126">Analizowanie katalogów głównych obiektów (odpowiedzi na pytania, takie jak nadal ma odwołanie do tego typu?).</span><span class="sxs-lookup"><span data-stu-id="6edf0-126">Analyzing roots of objects (answering questions like, "what still has a reference to this type?").</span></span>
- <span data-ttu-id="6edf0-127">Zbieranie ogólnych statystyk o liczbie obiektów na stercie.</span><span class="sxs-lookup"><span data-stu-id="6edf0-127">Collecting general statistics about the counts of objects on the heap.</span></span>

### <a name="view-the-gc-dump-captured-from-dotnet-gcdump"></a><span data-ttu-id="6edf0-128">Wyświetlanie zrzutu pamięci podręcznej przechwycone z programu dotnet-gcdump</span><span class="sxs-lookup"><span data-stu-id="6edf0-128">View the GC dump captured from dotnet-gcdump</span></span>

<span data-ttu-id="6edf0-129">W systemie Windows `.gcdump` pliki można wyświetlać w [Narzędzia PerfView](https://github.com/microsoft/perfview) na potrzeby analizy lub w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6edf0-129">On Windows, `.gcdump` files can be viewed in [PerfView](https://github.com/microsoft/perfview) for analysis or in Visual Studio.</span></span> <span data-ttu-id="6edf0-130">Obecnie nie ma możliwości otwierania `.gcdump` na platformach innych niż Windows.</span><span class="sxs-lookup"><span data-stu-id="6edf0-130">Currently, There is no way of opening a `.gcdump` on non-Windows platforms.</span></span>

<span data-ttu-id="6edf0-131">Można zbierać wiele `.gcdump` i otwierać je jednocześnie w programie Visual Studio w celu uzyskania porównania.</span><span class="sxs-lookup"><span data-stu-id="6edf0-131">You can collect multiple `.gcdump`s and open them simultaneously in Visual Studio to get a comparison experience.</span></span>

## <a name="options"></a><span data-ttu-id="6edf0-132">Opcje</span><span class="sxs-lookup"><span data-stu-id="6edf0-132">Options</span></span>

- **`--version`**

  <span data-ttu-id="6edf0-133">Wyświetla wersję `dotnet-gcdump` Narzędzia.</span><span class="sxs-lookup"><span data-stu-id="6edf0-133">Displays the version of the `dotnet-gcdump` utility.</span></span>

- **`-h|--help`**

  <span data-ttu-id="6edf0-134">Wyświetla pomoc w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="6edf0-134">Shows command-line help.</span></span>

## `dotnet-gcdump collect`

<span data-ttu-id="6edf0-135">Zbiera zrzut GC z aktualnie uruchomionego procesu.</span><span class="sxs-lookup"><span data-stu-id="6edf0-135">Collects a GC dump from a currently running process.</span></span>

> [!WARNING]
> <span data-ttu-id="6edf0-136">W celu przeanalizowania sterty GC to polecenie wyzwala wyrzucanie elementów bezużytecznych generacji 2 (pełne), które mogą wstrzymywać środowisko uruchomieniowe przez długi czas, szczególnie gdy sterta GC jest duża.</span><span class="sxs-lookup"><span data-stu-id="6edf0-136">To walk the GC heap, this command triggers a generation 2 (full) garbage collection, which can suspend the runtime for a long time, especially when the GC heap is large.</span></span> <span data-ttu-id="6edf0-137">Nie używaj tego polecenia w środowiskach z uwzględnieniem wydajności, gdy sterta GC jest duża.</span><span class="sxs-lookup"><span data-stu-id="6edf0-137">Don't use this command in performance-sensitive environments when the GC heap is large.</span></span>

### <a name="synopsis"></a><span data-ttu-id="6edf0-138">Streszczenie</span><span class="sxs-lookup"><span data-stu-id="6edf0-138">Synopsis</span></span>

```console
dotnet-gcdump collect [-h|--help] [-p|--process-id <pid>] [-o|--output <gcdump-file-path>] [-v|--verbose] [-t|--timeout <timeout>] [-n|--name <name>]
```

### <a name="options"></a><span data-ttu-id="6edf0-139">Opcje</span><span class="sxs-lookup"><span data-stu-id="6edf0-139">Options</span></span>

- **`-h|--help`**

  <span data-ttu-id="6edf0-140">Wyświetla pomoc w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="6edf0-140">Shows command-line help.</span></span>

- **`-p|--process-id <pid>`**

  <span data-ttu-id="6edf0-141">Identyfikator procesu, z którego ma zostać zebrany zrzut GC.</span><span class="sxs-lookup"><span data-stu-id="6edf0-141">The process ID to collect the GC dump from.</span></span>

- **`-o|--output <gcdump-file-path>`**

  <span data-ttu-id="6edf0-142">Ścieżka, w której powinny być zapisywane zebrane zrzuty GC.</span><span class="sxs-lookup"><span data-stu-id="6edf0-142">The path where collected GC dumps should be written.</span></span> <span data-ttu-id="6edf0-143">Wartość domyślna to *. \\ RRRRMMDD \_ HHMMSS \_ \<pid> . gcdump*.</span><span class="sxs-lookup"><span data-stu-id="6edf0-143">Defaults to *.\\YYYYMMDD\_HHMMSS\_\<pid>.gcdump*.</span></span>

- **`-v|--verbose`**

  <span data-ttu-id="6edf0-144">Wyprowadza dziennik podczas zbierania zrzutu GC.</span><span class="sxs-lookup"><span data-stu-id="6edf0-144">Output the log while collecting the GC dump.</span></span>

- **`-t|--timeout <timeout>`**

  <span data-ttu-id="6edf0-145">Zastanów się nad zbieraniem zrzutu pamięci podręcznej, jeśli trwa dłużej niż wynosi to wiele sekund.</span><span class="sxs-lookup"><span data-stu-id="6edf0-145">Give up on collecting the GC dump if it takes longer than this many seconds.</span></span> <span data-ttu-id="6edf0-146">Wartość domyślna to 30.</span><span class="sxs-lookup"><span data-stu-id="6edf0-146">The default value is 30.</span></span>

- **`-n|--name <name>`**

  <span data-ttu-id="6edf0-147">Nazwa procesu, z którego ma zostać zebrany zrzut GC.</span><span class="sxs-lookup"><span data-stu-id="6edf0-147">The name of the process to collect the GC dump from.</span></span>

## `dotnet-gcdump ps`

<span data-ttu-id="6edf0-148">Wyświetla listę procesów dotnet, dla których można zbierać zrzuty GC.</span><span class="sxs-lookup"><span data-stu-id="6edf0-148">Lists the dotnet processes that GC dumps can be collected for.</span></span>

### <a name="synopsis"></a><span data-ttu-id="6edf0-149">Streszczenie</span><span class="sxs-lookup"><span data-stu-id="6edf0-149">Synopsis</span></span>

```console
dotnet-gcdump ps
```

## `dotnet-gcdump report <gcdump_filename>`

<span data-ttu-id="6edf0-150">Wygeneruj Raport z wcześniej wygenerowanego zrzutu GC lub z uruchomionego procesu, a następnie wpisz polecenie `stdout` .</span><span class="sxs-lookup"><span data-stu-id="6edf0-150">Generate a report from a previously generated GC dump or from a running process, and write to `stdout`.</span></span>

### <a name="synopsis"></a><span data-ttu-id="6edf0-151">Streszczenie</span><span class="sxs-lookup"><span data-stu-id="6edf0-151">Synopsis</span></span>

```console
dotnet-gcdump report [-h|--help] [-p|--process-id <pid>] [-t|--report-type <HeapStat>]
```

### <a name="options"></a><span data-ttu-id="6edf0-152">Opcje</span><span class="sxs-lookup"><span data-stu-id="6edf0-152">Options</span></span>

- **`-h|--help`**

  <span data-ttu-id="6edf0-153">Wyświetla pomoc w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="6edf0-153">Shows command-line help.</span></span>

- **`-p|--process-id <pid>`**

  <span data-ttu-id="6edf0-154">Identyfikator procesu, z którego ma zostać zebrany zrzut GC.</span><span class="sxs-lookup"><span data-stu-id="6edf0-154">The process ID to collect the GC dump from.</span></span>

- **`-t|--report-type <HeapStat>`**

  <span data-ttu-id="6edf0-155">Typ raportu do wygenerowania.</span><span class="sxs-lookup"><span data-stu-id="6edf0-155">The type of report to generate.</span></span> <span data-ttu-id="6edf0-156">Dostępne opcje: heapstat (domyślnie).</span><span class="sxs-lookup"><span data-stu-id="6edf0-156">Available options: heapstat (default).</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="6edf0-157">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="6edf0-157">Troubleshoot</span></span>

- <span data-ttu-id="6edf0-158">Brak informacji o typie w gcdump.</span><span class="sxs-lookup"><span data-stu-id="6edf0-158">There is no type information in the gcdump.</span></span>

   <span data-ttu-id="6edf0-159">Przed platformą .NET Core 3,1 wystąpił problem polegający na tym, że pamięć podręczna typu nie została wyczyszczona między gcdumps, gdy zostały wywołane z EventPipe.</span><span class="sxs-lookup"><span data-stu-id="6edf0-159">Prior to .NET Core 3.1, there was an issue where a type cache was not cleared between gcdumps when they were invoked with EventPipe.</span></span> <span data-ttu-id="6edf0-160">Spowodowało to zdarzenia, które trzeba wykonać, aby określić informacje o typie, które nie są wysyłane dla drugiego i kolejnego gcdumps.</span><span class="sxs-lookup"><span data-stu-id="6edf0-160">This resulted in the events needed for determining type information not being sent for the second and subsequent gcdumps.</span></span> <span data-ttu-id="6edf0-161">Ten problem został rozwiązany w programie .NET Core 3,1-preview2.</span><span class="sxs-lookup"><span data-stu-id="6edf0-161">This was fixed in .NET Core 3.1-preview2.</span></span>

- <span data-ttu-id="6edf0-162">COM i typy statyczne nie znajdują się w zrzucie odzyskiwania pamięci.</span><span class="sxs-lookup"><span data-stu-id="6edf0-162">COM and static types aren't in the GC dump.</span></span>

   <span data-ttu-id="6edf0-163">Przed uruchomieniem programu .NET Core 3,1-preview2 wystąpił problem polegający na tym, że typy statyczne i COM nie zostały wysłane, gdy zrzut GC został wywołany za pośrednictwem EventPipe.</span><span class="sxs-lookup"><span data-stu-id="6edf0-163">Prior to .NET Core 3.1-preview2, there was an issue where static and COM types weren't sent when the GC dump was invoked via EventPipe.</span></span> <span data-ttu-id="6edf0-164">Ten problem został rozwiązany w programie .NET Core 3,1-preview2.</span><span class="sxs-lookup"><span data-stu-id="6edf0-164">This has been fixed in .NET Core 3.1-preview2.</span></span>
