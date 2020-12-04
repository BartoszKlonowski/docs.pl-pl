---
title: Zdarzenia środowiska uruchomieniowego odzyskiwania pamięci
description: Zobacz zdarzenia środowiska uruchomieniowego platformy .NET, które zbierają informacje diagnostyczne specyficzne dla modułu zbierającego elementy bezużyteczne platformy .NET.
ms.date: 11/13/2020
ms.topic: reference
helpviewer_keywords:
- GC events
- garbage collection events (CoreCLR)
- ETW, EventPipe, LTTng garbage collection events (CoreCLR)
ms.openlocfilehash: 2799a93f351baf23ec7a359b0b4b2be5c216dc4d
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "96590000"
---
# <a name="net-runtime-garbage-collection-events"></a><span data-ttu-id="dc28d-103">Zdarzenia odzyskiwania pamięci środowiska uruchomieniowego platformy .NET</span><span class="sxs-lookup"><span data-stu-id="dc28d-103">.NET runtime garbage collection events</span></span>

<span data-ttu-id="dc28d-104">Te zdarzenia zbierają informacje dotyczące wyrzucania elementów bezużytecznych.</span><span class="sxs-lookup"><span data-stu-id="dc28d-104">These events collect information pertaining to garbage collection.</span></span> <span data-ttu-id="dc28d-105">Ułatwiają one diagnostykę i debugowanie, w tym określanie, ile razy zostało wykonane wyrzucanie elementów bezużytecznych, ile pamięci zostało zwolnione podczas wyrzucania elementów bezużytecznych itp. Aby uzyskać więcej informacji na temat korzystania z tych zdarzeń w celach diagnostycznych, zobacz [Rejestrowanie i śledzenie aplikacji .NET](../../core/diagnostics/logging-tracing.md) .</span><span class="sxs-lookup"><span data-stu-id="dc28d-105">They help in diagnostics and debugging, including determining how many times garbage collection was performed, how much memory was freed during garbage collection, etc. For more information about how to use these events for diagnostic purposes, see [logging and tracing .NET applications](../../core/diagnostics/logging-tracing.md)</span></span>

## <a name="gcstart_v2-event"></a><span data-ttu-id="dc28d-106">Zdarzenie GCStart_V2</span><span class="sxs-lookup"><span data-stu-id="dc28d-106">GCStart_V2 Event</span></span>

<span data-ttu-id="dc28d-107">W poniższej tabeli przedstawiono słowo kluczowe i poziom:</span><span class="sxs-lookup"><span data-stu-id="dc28d-107">The following table shows the keyword and level:</span></span>

|<span data-ttu-id="dc28d-108">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-108">Keyword for raising the event</span></span>|<span data-ttu-id="dc28d-109">Poziom</span><span class="sxs-lookup"><span data-stu-id="dc28d-109">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="dc28d-110">`GCKeyword` 0x1</span><span class="sxs-lookup"><span data-stu-id="dc28d-110">`GCKeyword` (0x1)</span></span>|<span data-ttu-id="dc28d-111">Informacyjny (4)</span><span class="sxs-lookup"><span data-stu-id="dc28d-111">Informational (4)</span></span>|

<span data-ttu-id="dc28d-112">W poniższej tabeli przedstawiono informacje o zdarzeniu:</span><span class="sxs-lookup"><span data-stu-id="dc28d-112">The following table shows the event information:</span></span>

|<span data-ttu-id="dc28d-113">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="dc28d-113">Event</span></span>|<span data-ttu-id="dc28d-114">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-114">Event ID</span></span>|<span data-ttu-id="dc28d-115">Wywoływane, gdy</span><span class="sxs-lookup"><span data-stu-id="dc28d-115">Raised when</span></span>|
|-----------|--------------|-----------------|
|`GCStart_V1`|<span data-ttu-id="dc28d-116">1</span><span class="sxs-lookup"><span data-stu-id="dc28d-116">1</span></span>|<span data-ttu-id="dc28d-117">Rozpoczęto odzyskiwanie pamięci.</span><span class="sxs-lookup"><span data-stu-id="dc28d-117">A garbage collection has started.</span></span>|

<span data-ttu-id="dc28d-118">W poniższej tabeli przedstawiono dane zdarzenia:</span><span class="sxs-lookup"><span data-stu-id="dc28d-118">The following table shows the event data:</span></span>

|<span data-ttu-id="dc28d-119">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="dc28d-119">Field name</span></span>|<span data-ttu-id="dc28d-120">Typ danych</span><span class="sxs-lookup"><span data-stu-id="dc28d-120">Data type</span></span>|<span data-ttu-id="dc28d-121">Opis</span><span class="sxs-lookup"><span data-stu-id="dc28d-121">Description</span></span>|
|----------------|---------------|-----------------|
|`Count`|`win:UInt32`|<span data-ttu-id="dc28d-122">*N*-ta kolekcja elementów bezużytecznych.</span><span class="sxs-lookup"><span data-stu-id="dc28d-122">The *n* th garbage collection.</span></span>|
|`Depth`|`win:UInt32`|<span data-ttu-id="dc28d-123">Generacja, która jest zbierana.</span><span class="sxs-lookup"><span data-stu-id="dc28d-123">The generation that is being collected.</span></span>|
|`Reason`|`win:UInt32`|<span data-ttu-id="dc28d-124">Dlaczego wyzwolono wyrzucanie elementów bezużytecznych:</span><span class="sxs-lookup"><span data-stu-id="dc28d-124">Why the garbage collection was triggered:</span></span><br /><br /> <span data-ttu-id="dc28d-125">`0x0` -Alokacja sterty dla małego obiektu.</span><span class="sxs-lookup"><span data-stu-id="dc28d-125">`0x0` - Small object heap allocation.</span></span><br /><br /> <span data-ttu-id="dc28d-126">`0x1` Wywołano.</span><span class="sxs-lookup"><span data-stu-id="dc28d-126">`0x1` - Induced.</span></span><br /><br /> <span data-ttu-id="dc28d-127">`0x2` -Mało pamięci.</span><span class="sxs-lookup"><span data-stu-id="dc28d-127">`0x2` - Low memory.</span></span><br /><br /> <span data-ttu-id="dc28d-128">`0x3` Ciągiem.</span><span class="sxs-lookup"><span data-stu-id="dc28d-128">`0x3` - Empty.</span></span><br /><br /> <span data-ttu-id="dc28d-129">`0x4` -Alokacja sterty dla dużego obiektu.</span><span class="sxs-lookup"><span data-stu-id="dc28d-129">`0x4` - Large object heap allocation.</span></span><br /><br /> <span data-ttu-id="dc28d-130">`0x5` -Brak miejsca (dla sterty małego obiektu).</span><span class="sxs-lookup"><span data-stu-id="dc28d-130">`0x5` - Out of space (for small object heap).</span></span><br /><br /> <span data-ttu-id="dc28d-131">`0x6` -Brak miejsca (dla sterty dużego obiektu).</span><span class="sxs-lookup"><span data-stu-id="dc28d-131">`0x6` - Out of space (for large object heap).</span></span><br /><br /> <span data-ttu-id="dc28d-132">`0x7` -Wywołano, ale nie wymuszono blokowania.</span><span class="sxs-lookup"><span data-stu-id="dc28d-132">`0x7` - Induced but not forced as blocking.</span></span>|
|`Type`|`win:UInt32`|<span data-ttu-id="dc28d-133">`0x0` -Blokowanie odzyskiwania pamięci wystąpiło poza odzyskiwaniem pamięci w tle.</span><span class="sxs-lookup"><span data-stu-id="dc28d-133">`0x0` - Blocking garbage collection occurred outside background garbage collection.</span></span><br /><br /> <span data-ttu-id="dc28d-134">`0x1` -Wyrzucanie elementów bezużytecznych w tle.</span><span class="sxs-lookup"><span data-stu-id="dc28d-134">`0x1` - Background garbage collection.</span></span><br /><br /> <span data-ttu-id="dc28d-135">`0x2` -Blokowanie odzyskiwania pamięci wystąpiło podczas odzyskiwania pamięci w tle.</span><span class="sxs-lookup"><span data-stu-id="dc28d-135">`0x2` - Blocking garbage collection occurred during background garbage collection.</span></span>|
|`ClrInstanceID`|<span data-ttu-id="dc28d-136">win: UInt16</span><span class="sxs-lookup"><span data-stu-id="dc28d-136">win:UInt16</span></span>|<span data-ttu-id="dc28d-137">Unikatowy identyfikator wystąpienia elementu CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="dc28d-137">Unique ID for the instance of CoreCLR.</span></span>|

## <a name="gcend_v1-event"></a><span data-ttu-id="dc28d-138">Zdarzenie GCEnd_V1</span><span class="sxs-lookup"><span data-stu-id="dc28d-138">GCEnd_V1 Event</span></span>

<span data-ttu-id="dc28d-139">W poniższej tabeli przedstawiono słowo kluczowe i poziom:</span><span class="sxs-lookup"><span data-stu-id="dc28d-139">The following table shows the keyword and level:</span></span>

|<span data-ttu-id="dc28d-140">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-140">Keyword for raising the event</span></span>|<span data-ttu-id="dc28d-141">Poziom</span><span class="sxs-lookup"><span data-stu-id="dc28d-141">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="dc28d-142">`GCKeyword` 0x1</span><span class="sxs-lookup"><span data-stu-id="dc28d-142">`GCKeyword` (0x1)</span></span>|<span data-ttu-id="dc28d-143">Informacyjny (4)</span><span class="sxs-lookup"><span data-stu-id="dc28d-143">Informational (4)</span></span>|

<span data-ttu-id="dc28d-144">W poniższej tabeli przedstawiono informacje o zdarzeniu:</span><span class="sxs-lookup"><span data-stu-id="dc28d-144">The following table shows the event information:</span></span>

|<span data-ttu-id="dc28d-145">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="dc28d-145">Event</span></span>|<span data-ttu-id="dc28d-146">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-146">Event ID</span></span>|<span data-ttu-id="dc28d-147">Wywoływane, gdy</span><span class="sxs-lookup"><span data-stu-id="dc28d-147">Raised when</span></span>|
|-----------|--------------|-----------------|
|`GCEnd_V1`|<span data-ttu-id="dc28d-148">2</span><span class="sxs-lookup"><span data-stu-id="dc28d-148">2</span></span>|<span data-ttu-id="dc28d-149">Wyrzucanie elementów bezużytecznych zostało zakończone.</span><span class="sxs-lookup"><span data-stu-id="dc28d-149">The garbage collection has ended.</span></span>|

<span data-ttu-id="dc28d-150">W poniższej tabeli przedstawiono dane zdarzenia:</span><span class="sxs-lookup"><span data-stu-id="dc28d-150">The following table shows the event data:</span></span>

|<span data-ttu-id="dc28d-151">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="dc28d-151">Field name</span></span>|<span data-ttu-id="dc28d-152">Typ danych</span><span class="sxs-lookup"><span data-stu-id="dc28d-152">Data type</span></span>|<span data-ttu-id="dc28d-153">Opis</span><span class="sxs-lookup"><span data-stu-id="dc28d-153">Description</span></span>|
|----------------|---------------|-----------------|
|`Count`|`win:UInt32`|<span data-ttu-id="dc28d-154">*N*-ta kolekcja elementów bezużytecznych.</span><span class="sxs-lookup"><span data-stu-id="dc28d-154">The *n* th garbage collection.</span></span>|
|`Depth`|`win:UInt32`|<span data-ttu-id="dc28d-155">Generacja, która została zebrana.</span><span class="sxs-lookup"><span data-stu-id="dc28d-155">The generation that was collected.</span></span>|
|`ClrInstanceID`|<span data-ttu-id="dc28d-156">win: UInt16</span><span class="sxs-lookup"><span data-stu-id="dc28d-156">win:UInt16</span></span>|<span data-ttu-id="dc28d-157">Unikatowy identyfikator wystąpienia elementu CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="dc28d-157">Unique ID for the instance of CoreCLR.</span></span>|

## <a name="gcheapstats_v2-event"></a><span data-ttu-id="dc28d-158">Zdarzenie GCHeapStats_V2</span><span class="sxs-lookup"><span data-stu-id="dc28d-158">GCHeapStats_V2 Event</span></span>

<span data-ttu-id="dc28d-159">W poniższej tabeli przedstawiono słowo kluczowe i poziom:</span><span class="sxs-lookup"><span data-stu-id="dc28d-159">The following table shows the keyword and level:</span></span>

|<span data-ttu-id="dc28d-160">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-160">Keyword for raising the event</span></span>|<span data-ttu-id="dc28d-161">Poziom</span><span class="sxs-lookup"><span data-stu-id="dc28d-161">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="dc28d-162">`GCKeyword` 0x1</span><span class="sxs-lookup"><span data-stu-id="dc28d-162">`GCKeyword` (0x1)</span></span>|<span data-ttu-id="dc28d-163">Informacyjny (4)</span><span class="sxs-lookup"><span data-stu-id="dc28d-163">Informational (4)</span></span>|

<span data-ttu-id="dc28d-164">W poniższej tabeli przedstawiono informacje o zdarzeniu:</span><span class="sxs-lookup"><span data-stu-id="dc28d-164">The following table shows the event information:</span></span>

|<span data-ttu-id="dc28d-165">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="dc28d-165">Event</span></span>|<span data-ttu-id="dc28d-166">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-166">Event ID</span></span>|<span data-ttu-id="dc28d-167">Opis</span><span class="sxs-lookup"><span data-stu-id="dc28d-167">Description</span></span>|
|-----------|--------------|-----------------|
|`GCHeapStats_V2`|<span data-ttu-id="dc28d-168">4</span><span class="sxs-lookup"><span data-stu-id="dc28d-168">4</span></span>|<span data-ttu-id="dc28d-169">Pokazuje statystyki sterty na końcu każdego wyrzucania elementów bezużytecznych.</span><span class="sxs-lookup"><span data-stu-id="dc28d-169">Shows the heap statistics at the end of each garbage collection.</span></span>|

<span data-ttu-id="dc28d-170">W poniższej tabeli przedstawiono dane zdarzenia:</span><span class="sxs-lookup"><span data-stu-id="dc28d-170">The following table shows the event data:</span></span>

|<span data-ttu-id="dc28d-171">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="dc28d-171">Field name</span></span>|<span data-ttu-id="dc28d-172">Typ danych</span><span class="sxs-lookup"><span data-stu-id="dc28d-172">Data type</span></span>|<span data-ttu-id="dc28d-173">Opis</span><span class="sxs-lookup"><span data-stu-id="dc28d-173">Description</span></span>|
|----------------|---------------|-----------------|
|`GenerationSize0`|`win:UInt64`|<span data-ttu-id="dc28d-174">Rozmiar (w bajtach) pamięci generacji 0.</span><span class="sxs-lookup"><span data-stu-id="dc28d-174">The size, in bytes, of generation 0 memory.</span></span>|
|`TotalPromotedSize0`|`win:UInt64`|<span data-ttu-id="dc28d-175">Liczba bajtów, które są podwyższane z generacji 0 do generacji 1.</span><span class="sxs-lookup"><span data-stu-id="dc28d-175">The number of bytes that are promoted from generation 0 to generation 1.</span></span>|
|`GenerationSize1`|`win:UInt64`|<span data-ttu-id="dc28d-176">Rozmiar (w bajtach) pamięci pierwszej generacji 1.</span><span class="sxs-lookup"><span data-stu-id="dc28d-176">The size, in bytes, of generation 1 memory.</span></span>|
|`TotalPromotedSize1`|`win:UInt64`|<span data-ttu-id="dc28d-177">Liczba bajtów, które są podwyższane z generacji 1 do generacji 2.</span><span class="sxs-lookup"><span data-stu-id="dc28d-177">The number of bytes that are promoted from generation 1 to generation 2.</span></span>|
|`GenerationSize2`|`win:UInt64`|<span data-ttu-id="dc28d-178">Rozmiar (w bajtach) pamięci podnoszącej 2 generacji.</span><span class="sxs-lookup"><span data-stu-id="dc28d-178">The size, in bytes, of generation 2 memory.</span></span>|
|`TotalPromotedSize2`|`win:UInt64`|<span data-ttu-id="dc28d-179">Liczba bajtów, które przeżyły w generacji 2 po ostatniej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="dc28d-179">The number of bytes that survived in generation 2 after the last collection.</span></span>|
|`GenerationSize3`|`win:UInt64`|<span data-ttu-id="dc28d-180">Rozmiar sterty dużego obiektu w bajtach.</span><span class="sxs-lookup"><span data-stu-id="dc28d-180">The size, in bytes, of the large object heap.</span></span>|
|`TotalPromotedSize3`|`win:UInt64`|<span data-ttu-id="dc28d-181">Liczba bajtów przeczytanych z sterty dużego obiektu po ostatniej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="dc28d-181">The number of bytes that survived in the large object heap after the last collection.</span></span>|
|`FinalizationPromotedSize`|`win:UInt64`|<span data-ttu-id="dc28d-182">Łączny rozmiar (w bajtach) obiektów, które są gotowe do finalizacji.</span><span class="sxs-lookup"><span data-stu-id="dc28d-182">The total size, in bytes, of the objects that are ready for finalization.</span></span>|
|`FinalizationPromotedCount`|`win:UInt64`|<span data-ttu-id="dc28d-183">Liczba obiektów, które są gotowe do finalizacji.</span><span class="sxs-lookup"><span data-stu-id="dc28d-183">The number of objects that are ready for finalization.</span></span>|
|`PinnedObjectCount`|`win:UInt32`|<span data-ttu-id="dc28d-184">Liczba przypiętych (nieruchomych) obiektów.</span><span class="sxs-lookup"><span data-stu-id="dc28d-184">The number of pinned (unmovable) objects.</span></span>|
|`SinkBlockCount`|`win:UInt32`|<span data-ttu-id="dc28d-185">Liczba bloków synchronizacji w użyciu.</span><span class="sxs-lookup"><span data-stu-id="dc28d-185">The number of synchronization blocks in use.</span></span>|
|`GCHandleCount`|`win:UInt32`|<span data-ttu-id="dc28d-186">Liczba dojść do wyrzucania elementów bezużytecznych w użyciu.</span><span class="sxs-lookup"><span data-stu-id="dc28d-186">The number of garbage collection handles in use.</span></span>|
|`ClrInstanceID`|`win:UInt16`|<span data-ttu-id="dc28d-187">Unikatowy identyfikator wystąpienia elementu CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="dc28d-187">Unique ID for the instance of CoreCLR.</span></span>|
|`GenerationSize4`|`win:UInt64`|<span data-ttu-id="dc28d-188">Rozmiar, w bajtach, przypiętej sterty obiektu.</span><span class="sxs-lookup"><span data-stu-id="dc28d-188">The size, in bytes, of the pinned object heap.</span></span>|
|`TotalPromotedSize4`|`win:UInt64`|<span data-ttu-id="dc28d-189">Liczba bajtów, które przeżyły na stercie przypiętych obiektów po ostatniej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="dc28d-189">The number of bytes that survived in the pinned object heap after the last collection.</span></span>|

## <a name="gccreatesegment_v1-event"></a><span data-ttu-id="dc28d-190">Zdarzenie GCCreateSegment_V1</span><span class="sxs-lookup"><span data-stu-id="dc28d-190">GCCreateSegment_V1 event</span></span>

<span data-ttu-id="dc28d-191">W poniższej tabeli przedstawiono słowo kluczowe i poziom:</span><span class="sxs-lookup"><span data-stu-id="dc28d-191">The following table shows the keyword and level:</span></span>

|<span data-ttu-id="dc28d-192">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-192">Keyword for raising the event</span></span>|<span data-ttu-id="dc28d-193">Poziom</span><span class="sxs-lookup"><span data-stu-id="dc28d-193">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="dc28d-194">`GCKeyword` 0x1</span><span class="sxs-lookup"><span data-stu-id="dc28d-194">`GCKeyword` (0x1)</span></span>|<span data-ttu-id="dc28d-195">Informacyjny (4)</span><span class="sxs-lookup"><span data-stu-id="dc28d-195">Informational (4)</span></span>|

<span data-ttu-id="dc28d-196">W poniższej tabeli przedstawiono informacje o zdarzeniu:</span><span class="sxs-lookup"><span data-stu-id="dc28d-196">The following table shows the event information:</span></span>

|<span data-ttu-id="dc28d-197">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="dc28d-197">Event</span></span>|<span data-ttu-id="dc28d-198">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-198">Event ID</span></span>|<span data-ttu-id="dc28d-199">Wywoływane, gdy</span><span class="sxs-lookup"><span data-stu-id="dc28d-199">Raised when</span></span>|
|-----------|--------------|-----------------|
|`GCCreateSegment_V1`|<span data-ttu-id="dc28d-200">5</span><span class="sxs-lookup"><span data-stu-id="dc28d-200">5</span></span>|<span data-ttu-id="dc28d-201">Utworzono nowy segment wyrzucania elementów bezużytecznych.</span><span class="sxs-lookup"><span data-stu-id="dc28d-201">A new garbage collection segment has been created.</span></span> <span data-ttu-id="dc28d-202">Ponadto po włączeniu śledzenia dla procesu, który jest już uruchomiony, to zdarzenie jest zgłaszane dla każdego istniejącego segmentu.</span><span class="sxs-lookup"><span data-stu-id="dc28d-202">In addition, when tracing is enabled on a process that is already running, this event is raised for each existing segment.</span></span>|

<span data-ttu-id="dc28d-203">W poniższej tabeli przedstawiono dane zdarzenia:</span><span class="sxs-lookup"><span data-stu-id="dc28d-203">The following table shows the event data:</span></span>

|<span data-ttu-id="dc28d-204">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="dc28d-204">Field name</span></span>|<span data-ttu-id="dc28d-205">Typ danych</span><span class="sxs-lookup"><span data-stu-id="dc28d-205">Data type</span></span>|<span data-ttu-id="dc28d-206">Opis</span><span class="sxs-lookup"><span data-stu-id="dc28d-206">Description</span></span>|
|----------------|---------------|-----------------|
|`Address`|`win:UInt64`|<span data-ttu-id="dc28d-207">Adres segmentu.</span><span class="sxs-lookup"><span data-stu-id="dc28d-207">The address of the segment.</span></span>|
|`Size`|`win:UInt64`|<span data-ttu-id="dc28d-208">Rozmiar segmentu.</span><span class="sxs-lookup"><span data-stu-id="dc28d-208">The size of the segment.</span></span>|
|`Type`|`win:UInt32`|<span data-ttu-id="dc28d-209">0x0 — sterta małego obiektu.</span><span class="sxs-lookup"><span data-stu-id="dc28d-209">0x0 - Small object heap.</span></span><br /><br /> <span data-ttu-id="dc28d-210">0x1 — sterta dużego obiektu.</span><span class="sxs-lookup"><span data-stu-id="dc28d-210">0x1 - Large object heap.</span></span><br /><br /> <span data-ttu-id="dc28d-211">0x2 — sterta tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="dc28d-211">0x2 - Read-only heap.</span></span>|
|`ClrInstanceID`|`win:UInt16`|<span data-ttu-id="dc28d-212">Unikatowy identyfikator wystąpienia elementu CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="dc28d-212">Unique ID for the instance of CoreCLR.</span></span>|

<span data-ttu-id="dc28d-213">Należy zauważyć, że rozmiar segmentów przydzielone przez moduł wyrzucania elementów bezużytecznych jest specyficzny dla implementacji i może ulec zmianie w dowolnym momencie, łącznie z okresowymi aktualizacjami.</span><span class="sxs-lookup"><span data-stu-id="dc28d-213">Note that the size of segments allocated by the garbage collector is implementation-specific and is subject to change at any time, including in periodic updates.</span></span> <span data-ttu-id="dc28d-214">Aplikacja nigdy nie powinna mieć założeń lub zależeć od określonego rozmiaru segmentu ani nie powinna próbować skonfigurować ilości pamięci dostępnej dla alokacji segmentu.</span><span class="sxs-lookup"><span data-stu-id="dc28d-214">Your app should never make assumptions about or depend on a particular segment size, nor should it attempt to configure the amount of memory available for segment allocations.</span></span>

## <a name="gcfreesegment_v1-event"></a><span data-ttu-id="dc28d-215">Zdarzenie GCFreeSegment_V1</span><span class="sxs-lookup"><span data-stu-id="dc28d-215">GCFreeSegment_V1 event</span></span>

<span data-ttu-id="dc28d-216">W poniższej tabeli przedstawiono słowo kluczowe i poziom:</span><span class="sxs-lookup"><span data-stu-id="dc28d-216">The following table shows the keyword and level:</span></span>

|<span data-ttu-id="dc28d-217">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-217">Keyword for raising the event</span></span>|<span data-ttu-id="dc28d-218">Poziom</span><span class="sxs-lookup"><span data-stu-id="dc28d-218">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="dc28d-219">`GCKeyword` 0x1</span><span class="sxs-lookup"><span data-stu-id="dc28d-219">`GCKeyword` (0x1)</span></span>|<span data-ttu-id="dc28d-220">Informacyjny (4)</span><span class="sxs-lookup"><span data-stu-id="dc28d-220">Informational (4)</span></span>|

<span data-ttu-id="dc28d-221">W poniższej tabeli przedstawiono informacje o zdarzeniu:</span><span class="sxs-lookup"><span data-stu-id="dc28d-221">The following table shows the event information:</span></span>

|<span data-ttu-id="dc28d-222">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="dc28d-222">Event</span></span>|<span data-ttu-id="dc28d-223">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-223">Event ID</span></span>|<span data-ttu-id="dc28d-224">Wywoływane, gdy</span><span class="sxs-lookup"><span data-stu-id="dc28d-224">Raised when</span></span>|
|-----------|--------------|-----------------|
|`GCFreeSegment_V1`|<span data-ttu-id="dc28d-225">6</span><span class="sxs-lookup"><span data-stu-id="dc28d-225">6</span></span>|<span data-ttu-id="dc28d-226">Wydano segment wyrzucania elementów bezużytecznych.</span><span class="sxs-lookup"><span data-stu-id="dc28d-226">A garbage collection segment has been released.</span></span>|

<span data-ttu-id="dc28d-227">W poniższej tabeli przedstawiono dane zdarzenia:</span><span class="sxs-lookup"><span data-stu-id="dc28d-227">The following table shows the event data:</span></span>

|<span data-ttu-id="dc28d-228">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="dc28d-228">Field name</span></span>|<span data-ttu-id="dc28d-229">Typ danych</span><span class="sxs-lookup"><span data-stu-id="dc28d-229">Data type</span></span>|<span data-ttu-id="dc28d-230">Opis</span><span class="sxs-lookup"><span data-stu-id="dc28d-230">Description</span></span>|
|----------------|---------------|-----------------|
|`Address`|`win:UInt64`|<span data-ttu-id="dc28d-231">Adres segmentu.</span><span class="sxs-lookup"><span data-stu-id="dc28d-231">The address of the segment.</span></span>|
|`ClrInstanceID`|`win:UInt16`|<span data-ttu-id="dc28d-232">Unikatowy identyfikator wystąpienia elementu CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="dc28d-232">Unique ID for the instance of CoreCLR.</span></span>|

## <a name="gcrestarteebegin_v1-event"></a><span data-ttu-id="dc28d-233">Zdarzenie GCRestartEEBegin_V1</span><span class="sxs-lookup"><span data-stu-id="dc28d-233">GCRestartEEBegin_V1 event</span></span>

<span data-ttu-id="dc28d-234">W poniższej tabeli przedstawiono słowo kluczowe i poziom:</span><span class="sxs-lookup"><span data-stu-id="dc28d-234">The following table shows the keyword and level:</span></span>

|<span data-ttu-id="dc28d-235">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-235">Keyword for raising the event</span></span>|<span data-ttu-id="dc28d-236">Poziom</span><span class="sxs-lookup"><span data-stu-id="dc28d-236">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="dc28d-237">`GCKeyword` 0x1</span><span class="sxs-lookup"><span data-stu-id="dc28d-237">`GCKeyword` (0x1)</span></span>|<span data-ttu-id="dc28d-238">Informacyjny (4)</span><span class="sxs-lookup"><span data-stu-id="dc28d-238">Informational (4)</span></span>|

<span data-ttu-id="dc28d-239">W poniższej tabeli przedstawiono informacje o zdarzeniu:</span><span class="sxs-lookup"><span data-stu-id="dc28d-239">The following table shows the event information:</span></span>

|<span data-ttu-id="dc28d-240">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="dc28d-240">Event</span></span>|<span data-ttu-id="dc28d-241">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-241">Event ID</span></span>|<span data-ttu-id="dc28d-242">Wywoływane, gdy</span><span class="sxs-lookup"><span data-stu-id="dc28d-242">Raised when</span></span>|
|-----------|--------------|-----------------|
|`GCRestartEEBegin_V1`|<span data-ttu-id="dc28d-243">7</span><span class="sxs-lookup"><span data-stu-id="dc28d-243">7</span></span>|<span data-ttu-id="dc28d-244">Rozpoczęto wznawianie od zawieszenia środowiska uruchomieniowego języka wspólnego.</span><span class="sxs-lookup"><span data-stu-id="dc28d-244">Resumption from common language runtime suspension has begun.</span></span>|

<span data-ttu-id="dc28d-245">To zdarzenie nie zawiera żadnych danych zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="dc28d-245">This event does not have any event data.</span></span>

## <a name="gcrestarteeend_v1-event"></a><span data-ttu-id="dc28d-246">Zdarzenie GCRestartEEEnd_V1</span><span class="sxs-lookup"><span data-stu-id="dc28d-246">GCRestartEEEnd_V1 event</span></span>

<span data-ttu-id="dc28d-247">W poniższej tabeli przedstawiono słowo kluczowe i poziom:</span><span class="sxs-lookup"><span data-stu-id="dc28d-247">The following table shows the keyword and level:</span></span>

|<span data-ttu-id="dc28d-248">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-248">Keyword for raising the event</span></span>|<span data-ttu-id="dc28d-249">Poziom</span><span class="sxs-lookup"><span data-stu-id="dc28d-249">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="dc28d-250">`GCKeyword` 0x1</span><span class="sxs-lookup"><span data-stu-id="dc28d-250">`GCKeyword` (0x1)</span></span>|<span data-ttu-id="dc28d-251">Informacyjny (4)</span><span class="sxs-lookup"><span data-stu-id="dc28d-251">Informational (4)</span></span>|

<span data-ttu-id="dc28d-252">W poniższej tabeli przedstawiono informacje o zdarzeniu:</span><span class="sxs-lookup"><span data-stu-id="dc28d-252">The following table shows the event information:</span></span>

|<span data-ttu-id="dc28d-253">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="dc28d-253">Event</span></span>|<span data-ttu-id="dc28d-254">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-254">Event Id</span></span>|<span data-ttu-id="dc28d-255">Wywoływane, gdy</span><span class="sxs-lookup"><span data-stu-id="dc28d-255">Raised when</span></span>|
|-----------|--------------|-----------------|
|`GCRestartEEEnd_V1`|<span data-ttu-id="dc28d-256">3</span><span class="sxs-lookup"><span data-stu-id="dc28d-256">3</span></span>|<span data-ttu-id="dc28d-257">Zakończono wznawianie z zawieszenia środowiska uruchomieniowego języka wspólnego.</span><span class="sxs-lookup"><span data-stu-id="dc28d-257">Resumption from common language runtime suspension has ended.</span></span>|

<span data-ttu-id="dc28d-258">To zdarzenie nie zawiera żadnych danych zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="dc28d-258">This event does not have any event data.</span></span>

## <a name="gcsuspendeeend_v1-event"></a><span data-ttu-id="dc28d-259">Zdarzenie GCSuspendEEEnd_V1</span><span class="sxs-lookup"><span data-stu-id="dc28d-259">GCSuspendEEEnd_V1 event</span></span>

<span data-ttu-id="dc28d-260">W poniższej tabeli przedstawiono słowo kluczowe i poziom:</span><span class="sxs-lookup"><span data-stu-id="dc28d-260">The following table shows the keyword and level:</span></span>

|<span data-ttu-id="dc28d-261">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-261">Keyword for raising the event</span></span>|<span data-ttu-id="dc28d-262">Poziom</span><span class="sxs-lookup"><span data-stu-id="dc28d-262">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="dc28d-263">`GCKeyword` 0x1</span><span class="sxs-lookup"><span data-stu-id="dc28d-263">`GCKeyword` (0x1)</span></span>|<span data-ttu-id="dc28d-264">Informacyjny (4)</span><span class="sxs-lookup"><span data-stu-id="dc28d-264">Informational (4)</span></span>|

<span data-ttu-id="dc28d-265">W poniższej tabeli przedstawiono informacje o zdarzeniu:</span><span class="sxs-lookup"><span data-stu-id="dc28d-265">The following table shows the event information:</span></span>

|<span data-ttu-id="dc28d-266">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="dc28d-266">Event</span></span>|<span data-ttu-id="dc28d-267">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-267">Event ID</span></span>|<span data-ttu-id="dc28d-268">Wywoływane, gdy</span><span class="sxs-lookup"><span data-stu-id="dc28d-268">Raised when</span></span>|
|-----------|--------------|-----------------|
|`GCSuspendEEEnd_V1`|<span data-ttu-id="dc28d-269">8</span><span class="sxs-lookup"><span data-stu-id="dc28d-269">8</span></span>|<span data-ttu-id="dc28d-270">Koniec zawieszenia aparatu wykonywania na potrzeby wyrzucania elementów bezużytecznych.</span><span class="sxs-lookup"><span data-stu-id="dc28d-270">End of suspension of the execution engine for garbage collection.</span></span>|

<span data-ttu-id="dc28d-271">To zdarzenie nie zawiera żadnych danych zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="dc28d-271">This event does not have any event data.</span></span>

## <a name="gcsuspendeebegin_v1-event"></a><span data-ttu-id="dc28d-272">Zdarzenie GCSuspendEEBegin_V1</span><span class="sxs-lookup"><span data-stu-id="dc28d-272">GCSuspendEEBegin_V1 event</span></span>

<span data-ttu-id="dc28d-273">W poniższej tabeli przedstawiono słowo kluczowe i poziom:</span><span class="sxs-lookup"><span data-stu-id="dc28d-273">The following table shows the keyword and level:</span></span>

|<span data-ttu-id="dc28d-274">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-274">Keyword for raising the event</span></span>|<span data-ttu-id="dc28d-275">Poziom</span><span class="sxs-lookup"><span data-stu-id="dc28d-275">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="dc28d-276">`GCKeyword` 0x1</span><span class="sxs-lookup"><span data-stu-id="dc28d-276">`GCKeyword` (0x1)</span></span>|<span data-ttu-id="dc28d-277">Informacyjny (4)</span><span class="sxs-lookup"><span data-stu-id="dc28d-277">Informational (4)</span></span>|

<span data-ttu-id="dc28d-278">W poniższej tabeli przedstawiono informacje o zdarzeniu:</span><span class="sxs-lookup"><span data-stu-id="dc28d-278">The following table shows the event information:</span></span>

|<span data-ttu-id="dc28d-279">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="dc28d-279">Event</span></span>|<span data-ttu-id="dc28d-280">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-280">Event ID</span></span>|<span data-ttu-id="dc28d-281">Wywoływane, gdy</span><span class="sxs-lookup"><span data-stu-id="dc28d-281">Raised when</span></span>|
|-----------|--------------|-----------------|
|`GCSuspendEEBegin_V1`|<span data-ttu-id="dc28d-282">8</span><span class="sxs-lookup"><span data-stu-id="dc28d-282">8</span></span>|<span data-ttu-id="dc28d-283">Początek zawieszenia aparatu wykonywania na potrzeby wyrzucania elementów bezużytecznych.</span><span class="sxs-lookup"><span data-stu-id="dc28d-283">Start of suspension of the execution engine for garbage collection.</span></span>|

|<span data-ttu-id="dc28d-284">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="dc28d-284">Field name</span></span>|<span data-ttu-id="dc28d-285">Typ danych</span><span class="sxs-lookup"><span data-stu-id="dc28d-285">Data type</span></span>|<span data-ttu-id="dc28d-286">Opis</span><span class="sxs-lookup"><span data-stu-id="dc28d-286">Description</span></span>|
|----------------|---------------|-----------------|
|`Count`|`win:UInt32`|<span data-ttu-id="dc28d-287">*N*-ta kolekcja elementów bezużytecznych.</span><span class="sxs-lookup"><span data-stu-id="dc28d-287">The *n* th garbage collection.</span></span>|
|`Reason`|`win:UInt32`|<span data-ttu-id="dc28d-288">Przyczyna zawieszenia usługi EE.</span><span class="sxs-lookup"><span data-stu-id="dc28d-288">Reason for EE suspension.</span></span><br/><br/><span data-ttu-id="dc28d-289">`0x0`: Wstrzymywanie dla innych</span><span class="sxs-lookup"><span data-stu-id="dc28d-289">`0x0`: Suspend for Other</span></span><br/><br/><span data-ttu-id="dc28d-290">`0x1`: Suspend dla GC.</span><span class="sxs-lookup"><span data-stu-id="dc28d-290">`0x1`: Suspend for GC.</span></span><br/><br/><span data-ttu-id="dc28d-291">`0x2`: Wstrzymanie do zamknięcia domeny aplikacji.</span><span class="sxs-lookup"><span data-stu-id="dc28d-291">`0x2`: Suspend for AppDomain shutdown.</span></span><br/><br/><span data-ttu-id="dc28d-292">`0x3`: Wstrzymywanie do pochylenia kodu.</span><span class="sxs-lookup"><span data-stu-id="dc28d-292">`0x3`: Suspend for code pitching.</span></span><br/><br/><span data-ttu-id="dc28d-293">`0x4`: Wstrzymaj do zamknięcia.</span><span class="sxs-lookup"><span data-stu-id="dc28d-293">`0x4`: Suspend for shutdown.</span></span><br/><br/><span data-ttu-id="dc28d-294">`0x5`: Suspend for Debugger.</span><span class="sxs-lookup"><span data-stu-id="dc28d-294">`0x5`: Suspend for debugger.</span></span><br/><br/><span data-ttu-id="dc28d-295">`0x6`: Wstrzymaj przygotowanie do przygotowania do odzyskiwania pamięci.</span><span class="sxs-lookup"><span data-stu-id="dc28d-295">`0x6`: Suspend for GC Prep.</span></span><br/><br/><span data-ttu-id="dc28d-296">`0x7`: Wstrzymanie do odchylenia debugera</span><span class="sxs-lookup"><span data-stu-id="dc28d-296">`0x7`: Suspend for debugger sweep</span></span>|

## <a name="gcallocationtick_v3-event"></a><span data-ttu-id="dc28d-297">Zdarzenie GCAllocationTick_V3</span><span class="sxs-lookup"><span data-stu-id="dc28d-297">GCAllocationTick_V3 event</span></span>

<span data-ttu-id="dc28d-298">W poniższej tabeli przedstawiono słowo kluczowe i poziom:</span><span class="sxs-lookup"><span data-stu-id="dc28d-298">The following table shows the keyword and level:</span></span>

|<span data-ttu-id="dc28d-299">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-299">Keyword for raising the event</span></span>|<span data-ttu-id="dc28d-300">Poziom</span><span class="sxs-lookup"><span data-stu-id="dc28d-300">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="dc28d-301">`GCKeyword` 0x1</span><span class="sxs-lookup"><span data-stu-id="dc28d-301">`GCKeyword` (0x1)</span></span>|<span data-ttu-id="dc28d-302">Verbose (4)</span><span class="sxs-lookup"><span data-stu-id="dc28d-302">Verbose (4)</span></span>|

<span data-ttu-id="dc28d-303">W poniższej tabeli przedstawiono informacje o zdarzeniu:</span><span class="sxs-lookup"><span data-stu-id="dc28d-303">The following table shows the event information:</span></span>

|<span data-ttu-id="dc28d-304">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="dc28d-304">Event</span></span>|<span data-ttu-id="dc28d-305">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-305">Event ID</span></span>|<span data-ttu-id="dc28d-306">Wywoływane, gdy</span><span class="sxs-lookup"><span data-stu-id="dc28d-306">Raised when</span></span>|
|-----------|--------------|-----------------|
|`GCAllocationTick_V3`|<span data-ttu-id="dc28d-307">10</span><span class="sxs-lookup"><span data-stu-id="dc28d-307">10</span></span>|<span data-ttu-id="dc28d-308">Za każdym razem przydzielono około 100 KB.</span><span class="sxs-lookup"><span data-stu-id="dc28d-308">Each time approximately 100 KB is allocated.</span></span>|

<span data-ttu-id="dc28d-309">W poniższej tabeli przedstawiono dane zdarzenia:</span><span class="sxs-lookup"><span data-stu-id="dc28d-309">The following table shows the event data:</span></span>

|<span data-ttu-id="dc28d-310">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="dc28d-310">Field name</span></span>|<span data-ttu-id="dc28d-311">Typ danych</span><span class="sxs-lookup"><span data-stu-id="dc28d-311">Data type</span></span>|<span data-ttu-id="dc28d-312">Opis</span><span class="sxs-lookup"><span data-stu-id="dc28d-312">Description</span></span>|
|----------------|---------------|-----------------|
|`AllocationAmount`|`win:UInt32`|<span data-ttu-id="dc28d-313">Rozmiar alokacji w bajtach.</span><span class="sxs-lookup"><span data-stu-id="dc28d-313">The allocation size, in bytes.</span></span> <span data-ttu-id="dc28d-314">Ta wartość jest dokładna dla przydziałów, które są mniejsze niż długość ULONG (4 294 967 295 bajtów).</span><span class="sxs-lookup"><span data-stu-id="dc28d-314">This value is accurate for allocations that are less than the length of a ULONG (4,294,967,295 bytes).</span></span> <span data-ttu-id="dc28d-315">Jeśli alokacja jest większa, to pole zawiera obciętą wartość.</span><span class="sxs-lookup"><span data-stu-id="dc28d-315">If the allocation is greater, this field contains a truncated value.</span></span> <span data-ttu-id="dc28d-316">Używane `AllocationAmount64` dla bardzo dużych alokacji.</span><span class="sxs-lookup"><span data-stu-id="dc28d-316">Use `AllocationAmount64` for very large allocations.</span></span>|
|`AllocationKind`|`win:UInt32`|<span data-ttu-id="dc28d-317">`0x0` — Alokacja małego obiektu (alokacja jest w ramach sterty małego obiektu).</span><span class="sxs-lookup"><span data-stu-id="dc28d-317">`0x0` - Small object allocation (allocation is in small object heap).</span></span><br /><br /> <span data-ttu-id="dc28d-318">`0x1` -Alokacja dużego obiektu (alokacja jest w stosie dużego obiektu).</span><span class="sxs-lookup"><span data-stu-id="dc28d-318">`0x1` - Large object allocation (allocation is in large object heap).</span></span>|
|`AllocationAmount64`|`win:UInt64`|<span data-ttu-id="dc28d-319">Rozmiar alokacji w bajtach.</span><span class="sxs-lookup"><span data-stu-id="dc28d-319">The allocation size, in bytes.</span></span> <span data-ttu-id="dc28d-320">Ta wartość jest dokładna dla bardzo dużych alokacji.</span><span class="sxs-lookup"><span data-stu-id="dc28d-320">This value is accurate for very large allocations.</span></span>|
|`TypeId`|`win:Pointer`|<span data-ttu-id="dc28d-321">Adres metody.</span><span class="sxs-lookup"><span data-stu-id="dc28d-321">The address of the MethodTable.</span></span> <span data-ttu-id="dc28d-322">Jeśli istnieje kilka typów obiektów, które zostały przydzieloną w trakcie tego zdarzenia, jest to adres metody, która odnosi się do ostatniego przydzielony obiekt (obiekt, który spowodował przekroczenie 100 KB progu).</span><span class="sxs-lookup"><span data-stu-id="dc28d-322">When there are several types of objects that were allocated during this event, this is the address of the MethodTable that corresponds to the last object allocated (the object that caused the 100 KB threshold to be exceeded).</span></span>|
|`TypeName`|`win:UnicodeString`|<span data-ttu-id="dc28d-323">Nazwa przydzieloną typ.</span><span class="sxs-lookup"><span data-stu-id="dc28d-323">The name of the type that was allocated.</span></span> <span data-ttu-id="dc28d-324">Jeśli istnieje kilka typów obiektów, które zostały przydzieloną w trakcie tego zdarzenia, jest to typ ostatniego przydzielono obiektu (obiektu, który spowodował przekroczenie 100 KB).</span><span class="sxs-lookup"><span data-stu-id="dc28d-324">When there are several types of objects that were allocated during this event, this is the type of the last object allocated (the object that caused the 100 KB threshold to be exceeded).</span></span>|
|`HeapIndex`|`win:UInt32`|<span data-ttu-id="dc28d-325">Sterta, do której został przydzielony obiekt.</span><span class="sxs-lookup"><span data-stu-id="dc28d-325">The heap where the object was allocated.</span></span> <span data-ttu-id="dc28d-326">Ta wartość jest równa 0 (zero) podczas uruchamiania z odzyskiwaniem pamięci stacji roboczej.</span><span class="sxs-lookup"><span data-stu-id="dc28d-326">This value is 0 (zero) when running with workstation garbage collection.</span></span>|
|`Address`|`win:Pointer`|<span data-ttu-id="dc28d-327">Adres ostatniego przyznanego obiektu.</span><span class="sxs-lookup"><span data-stu-id="dc28d-327">The address of the last allocated object.</span></span>|
|`ClrInstanceID`|`win:UInt16`|<span data-ttu-id="dc28d-328">Unikatowy identyfikator wystąpienia elementu CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="dc28d-328">Unique ID for the instance of CoreCLR.</span></span>|

## <a name="gccreateconcurrentthread_v1-event"></a><span data-ttu-id="dc28d-329">Zdarzenie GCCreateConcurrentThread_V1</span><span class="sxs-lookup"><span data-stu-id="dc28d-329">GCCreateConcurrentThread_V1 event</span></span>

<span data-ttu-id="dc28d-330">W poniższej tabeli przedstawiono słowo kluczowe i poziom:</span><span class="sxs-lookup"><span data-stu-id="dc28d-330">The following table shows the keyword and level:</span></span>

|<span data-ttu-id="dc28d-331">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-331">Keyword for raising the event</span></span>|<span data-ttu-id="dc28d-332">Poziom</span><span class="sxs-lookup"><span data-stu-id="dc28d-332">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="dc28d-333">`GCKeyword` 0x1</span><span class="sxs-lookup"><span data-stu-id="dc28d-333">`GCKeyword` (0x1)</span></span>|<span data-ttu-id="dc28d-334">Informacyjny (4)</span><span class="sxs-lookup"><span data-stu-id="dc28d-334">Informational (4)</span></span>|
|<span data-ttu-id="dc28d-335">`ThreadingKeyword` 0x10000</span><span class="sxs-lookup"><span data-stu-id="dc28d-335">`ThreadingKeyword` (0x10000)</span></span>|<span data-ttu-id="dc28d-336">Informacyjny (4)</span><span class="sxs-lookup"><span data-stu-id="dc28d-336">Informational (4)</span></span>|

<span data-ttu-id="dc28d-337">W poniższej tabeli przedstawiono informacje o zdarzeniu:</span><span class="sxs-lookup"><span data-stu-id="dc28d-337">The following table shows the event information:</span></span>

|<span data-ttu-id="dc28d-338">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="dc28d-338">Event</span></span>|<span data-ttu-id="dc28d-339">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-339">Event ID</span></span>|<span data-ttu-id="dc28d-340">Wywoływane, gdy</span><span class="sxs-lookup"><span data-stu-id="dc28d-340">Raised when</span></span>|
|-----------|--------------|-----------------|
|`GCCreateConcurrentThread_V1`|<span data-ttu-id="dc28d-341">11</span><span class="sxs-lookup"><span data-stu-id="dc28d-341">11</span></span>|<span data-ttu-id="dc28d-342">Utworzono wątek współbieżnego wyrzucania elementów bezużytecznych.</span><span class="sxs-lookup"><span data-stu-id="dc28d-342">Concurrent garbage collection thread was created.</span></span>|

<span data-ttu-id="dc28d-343">To zdarzenie nie zawiera żadnych danych zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="dc28d-343">This event does not have any event data.</span></span>

## <a name="gcterminateconcurrentthread_v1-event"></a><span data-ttu-id="dc28d-344">Zdarzenie GCTerminateConcurrentThread_V1</span><span class="sxs-lookup"><span data-stu-id="dc28d-344">GCTerminateConcurrentThread_V1 event</span></span>

<span data-ttu-id="dc28d-345">W poniższej tabeli przedstawiono słowo kluczowe i poziom:</span><span class="sxs-lookup"><span data-stu-id="dc28d-345">The following table shows the keyword and level:</span></span>

|<span data-ttu-id="dc28d-346">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-346">Keyword for raising the event</span></span>|<span data-ttu-id="dc28d-347">Poziom</span><span class="sxs-lookup"><span data-stu-id="dc28d-347">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="dc28d-348">`GCKeyword` 0x1</span><span class="sxs-lookup"><span data-stu-id="dc28d-348">`GCKeyword` (0x1)</span></span>|<span data-ttu-id="dc28d-349">Informacyjny (4)</span><span class="sxs-lookup"><span data-stu-id="dc28d-349">Informational (4)</span></span>|
|<span data-ttu-id="dc28d-350">`ThreadingKeyword` 0x10000</span><span class="sxs-lookup"><span data-stu-id="dc28d-350">`ThreadingKeyword` (0x10000)</span></span>|<span data-ttu-id="dc28d-351">Informacyjny (4)</span><span class="sxs-lookup"><span data-stu-id="dc28d-351">Informational (4)</span></span>|

<span data-ttu-id="dc28d-352">W poniższej tabeli przedstawiono informacje o zdarzeniu:</span><span class="sxs-lookup"><span data-stu-id="dc28d-352">The following table shows the event information:</span></span>

|<span data-ttu-id="dc28d-353">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="dc28d-353">Event</span></span>|<span data-ttu-id="dc28d-354">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-354">Event ID</span></span>|<span data-ttu-id="dc28d-355">Wywoływane, gdy</span><span class="sxs-lookup"><span data-stu-id="dc28d-355">Raised when</span></span>|
|-----------|--------------|-----------------|
|`GCTerminateConcurrentThread_V1`|<span data-ttu-id="dc28d-356">12</span><span class="sxs-lookup"><span data-stu-id="dc28d-356">12</span></span>|<span data-ttu-id="dc28d-357">Wątek współbieżnego wyrzucania elementów bezużytecznych został zakończony.</span><span class="sxs-lookup"><span data-stu-id="dc28d-357">Concurrent garbage collection thread was terminated.</span></span>|

<span data-ttu-id="dc28d-358">To zdarzenie nie zawiera żadnych danych zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="dc28d-358">This event does not have any event data.</span></span>

## <a name="gcfinalizersbegin_v1-event"></a><span data-ttu-id="dc28d-359">Zdarzenie GCFinalizersBegin_V1</span><span class="sxs-lookup"><span data-stu-id="dc28d-359">GCFinalizersBegin_V1 event</span></span>

<span data-ttu-id="dc28d-360">W poniższej tabeli przedstawiono słowo kluczowe i poziom:</span><span class="sxs-lookup"><span data-stu-id="dc28d-360">The following table shows the keyword and level:</span></span>

|<span data-ttu-id="dc28d-361">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-361">Keyword for raising the event</span></span>|<span data-ttu-id="dc28d-362">Poziom</span><span class="sxs-lookup"><span data-stu-id="dc28d-362">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="dc28d-363">`GCKeyword` 0x1</span><span class="sxs-lookup"><span data-stu-id="dc28d-363">`GCKeyword` (0x1)</span></span>|<span data-ttu-id="dc28d-364">Informacyjny (4)</span><span class="sxs-lookup"><span data-stu-id="dc28d-364">Informational (4)</span></span>|

<span data-ttu-id="dc28d-365">W poniższej tabeli przedstawiono informacje o zdarzeniu:</span><span class="sxs-lookup"><span data-stu-id="dc28d-365">The following table shows the event information:</span></span>

|<span data-ttu-id="dc28d-366">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="dc28d-366">Event</span></span>|<span data-ttu-id="dc28d-367">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-367">Event ID</span></span>|<span data-ttu-id="dc28d-368">Wywoływane, gdy</span><span class="sxs-lookup"><span data-stu-id="dc28d-368">Raised when</span></span>|
|-----------|--------------|-----------------|
|`GCFinalizersBegin_V1`|<span data-ttu-id="dc28d-369">14</span><span class="sxs-lookup"><span data-stu-id="dc28d-369">14</span></span>|<span data-ttu-id="dc28d-370">Początek uruchamiania finalizatorów.</span><span class="sxs-lookup"><span data-stu-id="dc28d-370">The start of running finalizers.</span></span>|

<span data-ttu-id="dc28d-371">To zdarzenie nie zawiera żadnych danych zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="dc28d-371">This event does not have any event data.</span></span>

## <a name="gcfinalizersend_v1-event"></a><span data-ttu-id="dc28d-372">Zdarzenie GCFinalizersEnd_V1</span><span class="sxs-lookup"><span data-stu-id="dc28d-372">GCFinalizersEnd_V1 event</span></span>

<span data-ttu-id="dc28d-373">W poniższej tabeli przedstawiono słowo kluczowe i poziom:</span><span class="sxs-lookup"><span data-stu-id="dc28d-373">The following table shows the keyword and level:</span></span>

|<span data-ttu-id="dc28d-374">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-374">Keyword for raising the event</span></span>|<span data-ttu-id="dc28d-375">Poziom</span><span class="sxs-lookup"><span data-stu-id="dc28d-375">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="dc28d-376">`GCKeyword` 0x1</span><span class="sxs-lookup"><span data-stu-id="dc28d-376">`GCKeyword` (0x1)</span></span>|<span data-ttu-id="dc28d-377">Informacyjny (4)</span><span class="sxs-lookup"><span data-stu-id="dc28d-377">Informational (4)</span></span>|

<span data-ttu-id="dc28d-378">W poniższej tabeli przedstawiono informacje o zdarzeniu:</span><span class="sxs-lookup"><span data-stu-id="dc28d-378">The following table shows the event information:</span></span>

|<span data-ttu-id="dc28d-379">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="dc28d-379">Event</span></span>|<span data-ttu-id="dc28d-380">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-380">Event ID</span></span>|<span data-ttu-id="dc28d-381">Wywoływane, gdy</span><span class="sxs-lookup"><span data-stu-id="dc28d-381">Raised when</span></span>|
|-----------|--------------|-----------------|
|`GCFinalizersEnd_V1`|<span data-ttu-id="dc28d-382">13</span><span class="sxs-lookup"><span data-stu-id="dc28d-382">13</span></span>|<span data-ttu-id="dc28d-383">Koniec uruchomionych finalizatorów.</span><span class="sxs-lookup"><span data-stu-id="dc28d-383">The end of running finalizers.</span></span>|

<span data-ttu-id="dc28d-384">W poniższej tabeli przedstawiono dane zdarzenia:</span><span class="sxs-lookup"><span data-stu-id="dc28d-384">The following table shows the event data:</span></span>

|<span data-ttu-id="dc28d-385">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="dc28d-385">Field name</span></span>|<span data-ttu-id="dc28d-386">Typ danych</span><span class="sxs-lookup"><span data-stu-id="dc28d-386">Data type</span></span>|<span data-ttu-id="dc28d-387">Opis</span><span class="sxs-lookup"><span data-stu-id="dc28d-387">Description</span></span>|
|----------------|---------------|-----------------|
|`Count`|`win:UInt32`|<span data-ttu-id="dc28d-388">Liczba uruchomionych finalizatorów.</span><span class="sxs-lookup"><span data-stu-id="dc28d-388">The number of finalizers that were run.</span></span>|
|`ClrInstanceID`|<span data-ttu-id="dc28d-389">win: UInt16</span><span class="sxs-lookup"><span data-stu-id="dc28d-389">win:UInt16</span></span>|<span data-ttu-id="dc28d-390">Unikatowy identyfikator wystąpienia CLR lub CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="dc28d-390">Unique ID for the instance of CLR or CoreCLR.</span></span>|

## <a name="setgchandle-event"></a><span data-ttu-id="dc28d-391">Zdarzenie SetGCHandle</span><span class="sxs-lookup"><span data-stu-id="dc28d-391">SetGCHandle event</span></span>

<span data-ttu-id="dc28d-392">W poniższej tabeli przedstawiono słowo kluczowe i poziom:</span><span class="sxs-lookup"><span data-stu-id="dc28d-392">The following table shows the keyword and level:</span></span>

|<span data-ttu-id="dc28d-393">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-393">Keyword for raising the event</span></span>|<span data-ttu-id="dc28d-394">Poziom</span><span class="sxs-lookup"><span data-stu-id="dc28d-394">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="dc28d-395">`GCHandleKeyword` 0x2</span><span class="sxs-lookup"><span data-stu-id="dc28d-395">`GCHandleKeyword` (0x2)</span></span>|<span data-ttu-id="dc28d-396">Informacyjny (4)</span><span class="sxs-lookup"><span data-stu-id="dc28d-396">Informational (4)</span></span>|

<span data-ttu-id="dc28d-397">W poniższej tabeli przedstawiono informacje o zdarzeniu:</span><span class="sxs-lookup"><span data-stu-id="dc28d-397">The following table shows the event information:</span></span>

|<span data-ttu-id="dc28d-398">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="dc28d-398">Event</span></span>|<span data-ttu-id="dc28d-399">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-399">Event ID</span></span>|<span data-ttu-id="dc28d-400">Wywoływane, gdy</span><span class="sxs-lookup"><span data-stu-id="dc28d-400">Raised when</span></span>|
|-----------|--------------|-----------------|
|`SetGCHandle`|<span data-ttu-id="dc28d-401">30</span><span class="sxs-lookup"><span data-stu-id="dc28d-401">30</span></span>|<span data-ttu-id="dc28d-402">Dojście GC zostało ustawione.</span><span class="sxs-lookup"><span data-stu-id="dc28d-402">A GC Handle has been set.</span></span>|

<span data-ttu-id="dc28d-403">W poniższej tabeli przedstawiono dane zdarzenia:</span><span class="sxs-lookup"><span data-stu-id="dc28d-403">The following table shows the event data:</span></span>

|<span data-ttu-id="dc28d-404">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="dc28d-404">Field name</span></span>|<span data-ttu-id="dc28d-405">Typ danych</span><span class="sxs-lookup"><span data-stu-id="dc28d-405">Data type</span></span>|<span data-ttu-id="dc28d-406">Opis</span><span class="sxs-lookup"><span data-stu-id="dc28d-406">Description</span></span>|
|----------------|---------------|-----------------|
|`HandleID`|`win:Pointer`|<span data-ttu-id="dc28d-407">Adres przydzielnego dojścia.</span><span class="sxs-lookup"><span data-stu-id="dc28d-407">The address of the allocated handle.</span></span>|
|`ObjectID`|`win:Pointer`|<span data-ttu-id="dc28d-408">Adres obiektu, którego dojście zostało utworzone.</span><span class="sxs-lookup"><span data-stu-id="dc28d-408">The address of the object whose handle was created.</span></span>|
|`Kind`|`win:UInt32`|<span data-ttu-id="dc28d-409">Typ dojścia GC, który został ustawiony.</span><span class="sxs-lookup"><span data-stu-id="dc28d-409">The type of GC handle that was set.</span></span> <br /><br /><span data-ttu-id="dc28d-410">`0x0`: WeakShort</span><span class="sxs-lookup"><span data-stu-id="dc28d-410">`0x0`: WeakShort</span></span> <br/><br/><span data-ttu-id="dc28d-411">`0x1`: WeakLong</span><span class="sxs-lookup"><span data-stu-id="dc28d-411">`0x1`: WeakLong</span></span> <br /><br /><span data-ttu-id="dc28d-412">`0x2`: Strong</span><span class="sxs-lookup"><span data-stu-id="dc28d-412">`0x2`: Strong</span></span> <br /><br /><span data-ttu-id="dc28d-413">`0x3`: Przypięty</span><span class="sxs-lookup"><span data-stu-id="dc28d-413">`0x3`: Pinned</span></span> <br /><br /><span data-ttu-id="dc28d-414">`0x4`: Zmienna</span><span class="sxs-lookup"><span data-stu-id="dc28d-414">`0x4`: Variable</span></span><br /><br /><span data-ttu-id="dc28d-415">`0x5`: RefCounted</span><span class="sxs-lookup"><span data-stu-id="dc28d-415">`0x5`: RefCounted</span></span> <br /><br /><span data-ttu-id="dc28d-416">`0x6`: Zależne</span><span class="sxs-lookup"><span data-stu-id="dc28d-416">`0x6`: Dependent</span></span><br /><br /><span data-ttu-id="dc28d-417">`0x7`: AsyncPinned</span><span class="sxs-lookup"><span data-stu-id="dc28d-417">`0x7`: AsyncPinned</span></span><br /><br /><span data-ttu-id="dc28d-418">`0x8`: Dojście SizedRef</span><span class="sxs-lookup"><span data-stu-id="dc28d-418">`0x8`: SizedRef</span></span>|
|`Generation`|`win:UInt32`|<span data-ttu-id="dc28d-419">Generacja obiektu, którego dojście zostało utworzone.</span><span class="sxs-lookup"><span data-stu-id="dc28d-419">The generation of the object whose handle was created.</span></span>|
|`AppDomainID`|`win:UInt64`|<span data-ttu-id="dc28d-420">Identyfikator domeny aplikacji.</span><span class="sxs-lookup"><span data-stu-id="dc28d-420">The AppDomain ID.</span></span>|
|`ClrInstanceID`|`win:UInt16`|<span data-ttu-id="dc28d-421">Unikatowy identyfikator wystąpienia elementu CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="dc28d-421">Unique ID for the instance of CoreCLR.</span></span>|

## <a name="destroygchandle-event"></a><span data-ttu-id="dc28d-422">Zdarzenie DestroyGCHandle</span><span class="sxs-lookup"><span data-stu-id="dc28d-422">DestroyGCHandle event</span></span>

<span data-ttu-id="dc28d-423">W poniższej tabeli przedstawiono słowo kluczowe i poziom:</span><span class="sxs-lookup"><span data-stu-id="dc28d-423">The following table shows the keyword and level:</span></span>

|<span data-ttu-id="dc28d-424">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-424">Keyword for raising the event</span></span>|<span data-ttu-id="dc28d-425">Poziom</span><span class="sxs-lookup"><span data-stu-id="dc28d-425">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="dc28d-426">`GCHandleKeyword` 0x2</span><span class="sxs-lookup"><span data-stu-id="dc28d-426">`GCHandleKeyword` (0x2)</span></span>|<span data-ttu-id="dc28d-427">Informacyjny (4)</span><span class="sxs-lookup"><span data-stu-id="dc28d-427">Informational (4)</span></span>|

<span data-ttu-id="dc28d-428">W poniższej tabeli przedstawiono informacje o zdarzeniu:</span><span class="sxs-lookup"><span data-stu-id="dc28d-428">The following table shows the event information:</span></span>

|<span data-ttu-id="dc28d-429">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="dc28d-429">Event</span></span>|<span data-ttu-id="dc28d-430">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-430">Event ID</span></span>|<span data-ttu-id="dc28d-431">Wywoływane, gdy</span><span class="sxs-lookup"><span data-stu-id="dc28d-431">Raised when</span></span>|
|-----------|--------------|-----------------|
|`DestroyGCHandle`|<span data-ttu-id="dc28d-432">31</span><span class="sxs-lookup"><span data-stu-id="dc28d-432">31</span></span>|<span data-ttu-id="dc28d-433">Dojście GC zostało zniszczone.</span><span class="sxs-lookup"><span data-stu-id="dc28d-433">A GC Handle is destroyed.</span></span>|

<span data-ttu-id="dc28d-434">W poniższej tabeli przedstawiono dane zdarzenia:</span><span class="sxs-lookup"><span data-stu-id="dc28d-434">The following table shows the event data:</span></span>

|<span data-ttu-id="dc28d-435">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="dc28d-435">Field name</span></span>|<span data-ttu-id="dc28d-436">Typ danych</span><span class="sxs-lookup"><span data-stu-id="dc28d-436">Data type</span></span>|<span data-ttu-id="dc28d-437">Opis</span><span class="sxs-lookup"><span data-stu-id="dc28d-437">Description</span></span>|
|----------------|---------------|-----------------|
|`HandleID`|`win:Pointer`|<span data-ttu-id="dc28d-438">Adres zniszczonego dojścia.</span><span class="sxs-lookup"><span data-stu-id="dc28d-438">The address of the destroyed handle.</span></span>|
|`ClrInstanceID`|<span data-ttu-id="dc28d-439">win: UInt16</span><span class="sxs-lookup"><span data-stu-id="dc28d-439">win:UInt16</span></span>|<span data-ttu-id="dc28d-440">Unikatowy identyfikator wystąpienia elementu CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="dc28d-440">Unique ID for the instance of CoreCLR.</span></span>|

## <a name="pinobjectatgctime-event"></a><span data-ttu-id="dc28d-441">Zdarzenie PinObjectAtGCTime</span><span class="sxs-lookup"><span data-stu-id="dc28d-441">PinObjectAtGCTime event</span></span>

<span data-ttu-id="dc28d-442">W poniższej tabeli przedstawiono słowo kluczowe i poziom:</span><span class="sxs-lookup"><span data-stu-id="dc28d-442">The following table shows the keyword and level:</span></span>

|<span data-ttu-id="dc28d-443">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-443">Keyword for raising the event</span></span>|<span data-ttu-id="dc28d-444">Poziom</span><span class="sxs-lookup"><span data-stu-id="dc28d-444">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="dc28d-445">`GCKeyword` 0x1</span><span class="sxs-lookup"><span data-stu-id="dc28d-445">`GCKeyword` (0x1)</span></span>|<span data-ttu-id="dc28d-446">Verbose (5)</span><span class="sxs-lookup"><span data-stu-id="dc28d-446">Verbose (5)</span></span>|

<span data-ttu-id="dc28d-447">W poniższej tabeli przedstawiono informacje o zdarzeniu:</span><span class="sxs-lookup"><span data-stu-id="dc28d-447">The following table shows the event information:</span></span>

|<span data-ttu-id="dc28d-448">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="dc28d-448">Event</span></span>|<span data-ttu-id="dc28d-449">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-449">Event ID</span></span>|<span data-ttu-id="dc28d-450">Wywoływane, gdy</span><span class="sxs-lookup"><span data-stu-id="dc28d-450">Raised when</span></span>|
|-----------|--------------|-----------------|
|`PinObjectAtGCTime`|<span data-ttu-id="dc28d-451">33</span><span class="sxs-lookup"><span data-stu-id="dc28d-451">33</span></span>|<span data-ttu-id="dc28d-452">Obiekt został przypięty podczas operacji GC.</span><span class="sxs-lookup"><span data-stu-id="dc28d-452">An object was pinned during a GC.</span></span>|

<span data-ttu-id="dc28d-453">W poniższej tabeli przedstawiono dane zdarzenia:</span><span class="sxs-lookup"><span data-stu-id="dc28d-453">The following table shows the event data:</span></span>

|<span data-ttu-id="dc28d-454">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="dc28d-454">Field name</span></span>|<span data-ttu-id="dc28d-455">Typ danych</span><span class="sxs-lookup"><span data-stu-id="dc28d-455">Data type</span></span>|<span data-ttu-id="dc28d-456">Opis</span><span class="sxs-lookup"><span data-stu-id="dc28d-456">Description</span></span>|
|----------------|---------------|-----------------|
|`HandleID`|`win:Pointer`|<span data-ttu-id="dc28d-457">Adres dojścia.</span><span class="sxs-lookup"><span data-stu-id="dc28d-457">The address of the handle.</span></span>|
|`ObjectID`|`win:Pointer`|<span data-ttu-id="dc28d-458">Adres przypiętego obiektu.</span><span class="sxs-lookup"><span data-stu-id="dc28d-458">The address of the pinned object.</span></span>|
|`ObjectSize`|`win:UInt64`|<span data-ttu-id="dc28d-459">Rozmiar przypiętego obiektu.</span><span class="sxs-lookup"><span data-stu-id="dc28d-459">The size of the pinned object.</span></span>|
|`TypeName`|`win:UnicodeString`|<span data-ttu-id="dc28d-460">Nazwa typu przypiętego obiektu.</span><span class="sxs-lookup"><span data-stu-id="dc28d-460">The name of the type of the pinned object.</span></span>|
|`ClrInstanceID`|`win:UInt16`|<span data-ttu-id="dc28d-461">Unikatowy identyfikator wystąpienia elementu CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="dc28d-461">Unique ID for the instance of CoreCLR.</span></span>|

## <a name="gctriggered-event"></a><span data-ttu-id="dc28d-462">Zdarzenie GCTriggered</span><span class="sxs-lookup"><span data-stu-id="dc28d-462">GCTriggered event</span></span>

<span data-ttu-id="dc28d-463">W poniższej tabeli przedstawiono słowo kluczowe i poziom:</span><span class="sxs-lookup"><span data-stu-id="dc28d-463">The following table shows the keyword and level:</span></span>

|<span data-ttu-id="dc28d-464">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-464">Keyword for raising the event</span></span>|<span data-ttu-id="dc28d-465">Poziom</span><span class="sxs-lookup"><span data-stu-id="dc28d-465">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="dc28d-466">`GCKeyword` 0x1</span><span class="sxs-lookup"><span data-stu-id="dc28d-466">`GCKeyword` (0x1)</span></span>|<span data-ttu-id="dc28d-467">Verbose (5)</span><span class="sxs-lookup"><span data-stu-id="dc28d-467">Verbose (5)</span></span>|

<span data-ttu-id="dc28d-468">W poniższej tabeli przedstawiono informacje o zdarzeniu:</span><span class="sxs-lookup"><span data-stu-id="dc28d-468">The following table shows the event information:</span></span>

|<span data-ttu-id="dc28d-469">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="dc28d-469">Event</span></span>|<span data-ttu-id="dc28d-470">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-470">Event ID</span></span>|<span data-ttu-id="dc28d-471">Wywoływane, gdy</span><span class="sxs-lookup"><span data-stu-id="dc28d-471">Raised when</span></span>|
|-----------|--------------|-----------------|
|`GCTriggered`|<span data-ttu-id="dc28d-472">33</span><span class="sxs-lookup"><span data-stu-id="dc28d-472">33</span></span>|<span data-ttu-id="dc28d-473">Wyzwolono wykaz globalny.</span><span class="sxs-lookup"><span data-stu-id="dc28d-473">A GC has been triggered.</span></span>|

<span data-ttu-id="dc28d-474">W poniższej tabeli przedstawiono dane zdarzenia:</span><span class="sxs-lookup"><span data-stu-id="dc28d-474">The following table shows the event data:</span></span>

|<span data-ttu-id="dc28d-475">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="dc28d-475">Field name</span></span>|<span data-ttu-id="dc28d-476">Typ danych</span><span class="sxs-lookup"><span data-stu-id="dc28d-476">Data type</span></span>|<span data-ttu-id="dc28d-477">Opis</span><span class="sxs-lookup"><span data-stu-id="dc28d-477">Description</span></span>|
|----------------|---------------|-----------------|
|`Reason`|`win:UInt32`|<span data-ttu-id="dc28d-478">Przyczyna wyzwolenia GC.</span><span class="sxs-lookup"><span data-stu-id="dc28d-478">The reason a GC was triggered.</span></span><br/><br/><span data-ttu-id="dc28d-479">`0x0`: AllocSmall</span><span class="sxs-lookup"><span data-stu-id="dc28d-479">`0x0`: AllocSmall</span></span><br/><br/><span data-ttu-id="dc28d-480">`0x1`: Wywołane</span><span class="sxs-lookup"><span data-stu-id="dc28d-480">`0x1`: Induced</span></span> <br/><br/><span data-ttu-id="dc28d-481">`0x2`: LowMemory</span><span class="sxs-lookup"><span data-stu-id="dc28d-481">`0x2`: LowMemory</span></span> <br/><br/><span data-ttu-id="dc28d-482">`0x3`: Puste</span><span class="sxs-lookup"><span data-stu-id="dc28d-482">`0x3`: Empty</span></span> <br/><br/><span data-ttu-id="dc28d-483">`0x4`: AllocLarge</span><span class="sxs-lookup"><span data-stu-id="dc28d-483">`0x4`: AllocLarge</span></span> <br/><br/><span data-ttu-id="dc28d-484">`0x5`: OutOfSpaceSmallObjectHeap</span><span class="sxs-lookup"><span data-stu-id="dc28d-484">`0x5`: OutOfSpaceSmallObjectHeap</span></span> <br/><br/><span data-ttu-id="dc28d-485">`0x6`: OutOfSpaceLargeObjectHeap</span><span class="sxs-lookup"><span data-stu-id="dc28d-485">`0x6`: OutOfSpaceLargeObjectHeap</span></span> <br/><br/><span data-ttu-id="dc28d-486">`0x7`:InducedNoForce</span><span class="sxs-lookup"><span data-stu-id="dc28d-486">`0x7`:InducedNoForce</span></span> <br/><br/><span data-ttu-id="dc28d-487">`0x8`: Naprężenie</span><span class="sxs-lookup"><span data-stu-id="dc28d-487">`0x8`: Stress</span></span> <br/><br/><span data-ttu-id="dc28d-488">`0x9`: InducedLowMemory</span><span class="sxs-lookup"><span data-stu-id="dc28d-488">`0x9`: InducedLowMemory</span></span>|
|`ClrInstanceID`|`win:UInt16`|<span data-ttu-id="dc28d-489">Unikatowy identyfikator wystąpienia elementu CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="dc28d-489">Unique ID for the instance of CoreCLR.</span></span>|

## <a name="increasememorypressure-event"></a><span data-ttu-id="dc28d-490">Zdarzenie IncreaseMemoryPressure</span><span class="sxs-lookup"><span data-stu-id="dc28d-490">IncreaseMemoryPressure event</span></span>

<span data-ttu-id="dc28d-491">W poniższej tabeli przedstawiono słowo kluczowe i poziom:</span><span class="sxs-lookup"><span data-stu-id="dc28d-491">The following table shows the keyword and level:</span></span>

|<span data-ttu-id="dc28d-492">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-492">Keyword for raising the event</span></span>|<span data-ttu-id="dc28d-493">Poziom</span><span class="sxs-lookup"><span data-stu-id="dc28d-493">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="dc28d-494">`GCKeyword` 0x1</span><span class="sxs-lookup"><span data-stu-id="dc28d-494">`GCKeyword` (0x1)</span></span>|<span data-ttu-id="dc28d-495">Informacje (4)</span><span class="sxs-lookup"><span data-stu-id="dc28d-495">Information (4)</span></span>|

<span data-ttu-id="dc28d-496">W poniższej tabeli przedstawiono informacje o zdarzeniu:</span><span class="sxs-lookup"><span data-stu-id="dc28d-496">The following table shows the event information:</span></span>

|<span data-ttu-id="dc28d-497">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="dc28d-497">Event</span></span>|<span data-ttu-id="dc28d-498">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-498">Event ID</span></span>|<span data-ttu-id="dc28d-499">Wywoływane, gdy</span><span class="sxs-lookup"><span data-stu-id="dc28d-499">Raised when</span></span>|
|----------------|---------------|-----------------|
|`IncreaseMemoryPressure`|<span data-ttu-id="dc28d-500">200</span><span class="sxs-lookup"><span data-stu-id="dc28d-500">200</span></span>|<span data-ttu-id="dc28d-501">Zwiększono wykorzystanie pamięci.</span><span class="sxs-lookup"><span data-stu-id="dc28d-501">Memory pressure was increased.</span></span>|

<span data-ttu-id="dc28d-502">W poniższej tabeli przedstawiono dane zdarzenia:</span><span class="sxs-lookup"><span data-stu-id="dc28d-502">The following table shows the event data:</span></span>

|<span data-ttu-id="dc28d-503">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="dc28d-503">Field Name</span></span>|<span data-ttu-id="dc28d-504">Typ danych</span><span class="sxs-lookup"><span data-stu-id="dc28d-504">Data type</span></span>|<span data-ttu-id="dc28d-505">Opis</span><span class="sxs-lookup"><span data-stu-id="dc28d-505">Description</span></span>|
|----------------|---------------|-----------------|
|`ClrInstanceID`|<span data-ttu-id="dc28d-506">win: UInt16</span><span class="sxs-lookup"><span data-stu-id="dc28d-506">win:UInt16</span></span>|<span data-ttu-id="dc28d-507">Unikatowy identyfikator wystąpienia elementu CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="dc28d-507">Unique ID for the instance of CoreCLR.</span></span>|

## <a name="decreasememorypressure-event"></a><span data-ttu-id="dc28d-508">Zdarzenie DecreaseMemoryPressure</span><span class="sxs-lookup"><span data-stu-id="dc28d-508">DecreaseMemoryPressure event</span></span>

<span data-ttu-id="dc28d-509">W poniższej tabeli przedstawiono słowo kluczowe i poziom:</span><span class="sxs-lookup"><span data-stu-id="dc28d-509">The following table shows the keyword and level:</span></span>

|<span data-ttu-id="dc28d-510">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-510">Keyword for raising the event</span></span>|<span data-ttu-id="dc28d-511">Poziom</span><span class="sxs-lookup"><span data-stu-id="dc28d-511">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="dc28d-512">`GCKeyword` 0x1</span><span class="sxs-lookup"><span data-stu-id="dc28d-512">`GCKeyword` (0x1)</span></span>|<span data-ttu-id="dc28d-513">Informacje (4)</span><span class="sxs-lookup"><span data-stu-id="dc28d-513">Information (4)</span></span>|

<span data-ttu-id="dc28d-514">W poniższej tabeli przedstawiono informacje o zdarzeniu:</span><span class="sxs-lookup"><span data-stu-id="dc28d-514">The following table shows the event information:</span></span>

|<span data-ttu-id="dc28d-515">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="dc28d-515">Event</span></span>|<span data-ttu-id="dc28d-516">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-516">Event ID</span></span>|<span data-ttu-id="dc28d-517">Wywoływane, gdy</span><span class="sxs-lookup"><span data-stu-id="dc28d-517">Raised when</span></span>|
|----------------|---------------|-----------------|
|`DecreaseMemoryPressure`|<span data-ttu-id="dc28d-518">201</span><span class="sxs-lookup"><span data-stu-id="dc28d-518">201</span></span>|<span data-ttu-id="dc28d-519">Obniżono wykorzystanie pamięci.</span><span class="sxs-lookup"><span data-stu-id="dc28d-519">Memory pressure was decreased.</span></span>|

<span data-ttu-id="dc28d-520">W poniższej tabeli przedstawiono dane zdarzenia:</span><span class="sxs-lookup"><span data-stu-id="dc28d-520">The following table shows the event data:</span></span>

|<span data-ttu-id="dc28d-521">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="dc28d-521">Field Name</span></span>|<span data-ttu-id="dc28d-522">Typ danych</span><span class="sxs-lookup"><span data-stu-id="dc28d-522">Data type</span></span>|<span data-ttu-id="dc28d-523">Opis</span><span class="sxs-lookup"><span data-stu-id="dc28d-523">Description</span></span>|
|----------------|---------------|-----------------|
|`BytesFreed`|`win:UInt32`|<span data-ttu-id="dc28d-524">Bajty zwolnione.</span><span class="sxs-lookup"><span data-stu-id="dc28d-524">Bytes freed.</span></span>|
|`ClrInstanceID`|`win:UInt16`|<span data-ttu-id="dc28d-525">Unikatowy identyfikator wystąpienia elementu CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="dc28d-525">Unique ID for the instance of CoreCLR.</span></span>|

## <a name="gcmarkwithtype-event"></a><span data-ttu-id="dc28d-526">Zdarzenie GCMarkWithType</span><span class="sxs-lookup"><span data-stu-id="dc28d-526">GCMarkWithType event</span></span>

<span data-ttu-id="dc28d-527">W poniższej tabeli przedstawiono słowo kluczowe i poziom:</span><span class="sxs-lookup"><span data-stu-id="dc28d-527">The following table shows the keyword and level:</span></span>

|<span data-ttu-id="dc28d-528">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-528">Keyword for raising the event</span></span>|<span data-ttu-id="dc28d-529">Poziom</span><span class="sxs-lookup"><span data-stu-id="dc28d-529">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="dc28d-530">`GCKeyword` 0x1</span><span class="sxs-lookup"><span data-stu-id="dc28d-530">`GCKeyword` (0x1)</span></span>|<span data-ttu-id="dc28d-531">Informacje (4)</span><span class="sxs-lookup"><span data-stu-id="dc28d-531">Information (4)</span></span>|

<span data-ttu-id="dc28d-532">W poniższej tabeli przedstawiono informacje o zdarzeniu:</span><span class="sxs-lookup"><span data-stu-id="dc28d-532">The following table shows the event information:</span></span>

|<span data-ttu-id="dc28d-533">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="dc28d-533">Event</span></span>|<span data-ttu-id="dc28d-534">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-534">Event ID</span></span>|<span data-ttu-id="dc28d-535">Wywoływane, gdy</span><span class="sxs-lookup"><span data-stu-id="dc28d-535">Raised when</span></span>|
|----------------|---------------|-----------------|
|`GCMarkWithType`|<span data-ttu-id="dc28d-536">202</span><span class="sxs-lookup"><span data-stu-id="dc28d-536">202</span></span>|<span data-ttu-id="dc28d-537">Element główny GC został oznaczony podczas fazy znacznika GC.</span><span class="sxs-lookup"><span data-stu-id="dc28d-537">A GC root has been marked during GC mark phase.</span></span>|

<span data-ttu-id="dc28d-538">W poniższej tabeli przedstawiono dane zdarzenia:</span><span class="sxs-lookup"><span data-stu-id="dc28d-538">The following table shows the event data:</span></span>

|<span data-ttu-id="dc28d-539">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="dc28d-539">Field Name</span></span>|<span data-ttu-id="dc28d-540">Typ danych</span><span class="sxs-lookup"><span data-stu-id="dc28d-540">Data type</span></span>|<span data-ttu-id="dc28d-541">Opis</span><span class="sxs-lookup"><span data-stu-id="dc28d-541">Description</span></span>|
|----------------|---------------|-----------------|
|`HeapNum`|`win:UInt32`|<span data-ttu-id="dc28d-542">Numer sterty.</span><span class="sxs-lookup"><span data-stu-id="dc28d-542">The heap number.</span></span>|
|`ClrInstanceID`|<span data-ttu-id="dc28d-543">win: UInt16</span><span class="sxs-lookup"><span data-stu-id="dc28d-543">win:UInt16</span></span>|<span data-ttu-id="dc28d-544">Unikatowy identyfikator wystąpienia elementu CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="dc28d-544">Unique ID for the instance of CoreCLR.</span></span>|
|`Type`|`win:UInt32`|<span data-ttu-id="dc28d-545">Typ główny GC.</span><span class="sxs-lookup"><span data-stu-id="dc28d-545">The GC root type.</span></span><br/><br/><span data-ttu-id="dc28d-546">`0x0`: Stos</span><span class="sxs-lookup"><span data-stu-id="dc28d-546">`0x0`: Stack</span></span><br/><br/><span data-ttu-id="dc28d-547">`0x1`: Finalizator</span><span class="sxs-lookup"><span data-stu-id="dc28d-547">`0x1`: Finalizer</span></span><br/><br/><span data-ttu-id="dc28d-548">`0x2`: Uchwyt</span><span class="sxs-lookup"><span data-stu-id="dc28d-548">`0x2`: Handle</span></span><br/><br/><span data-ttu-id="dc28d-549">`0x3`: Starsze</span><span class="sxs-lookup"><span data-stu-id="dc28d-549">`0x3`: Older</span></span><br/><br/><span data-ttu-id="dc28d-550">`0x4`: Dojście SizedRef</span><span class="sxs-lookup"><span data-stu-id="dc28d-550">`0x4`: SizedRef</span></span><br/><br/><span data-ttu-id="dc28d-551">`0x5`: Przepełnienie</span><span class="sxs-lookup"><span data-stu-id="dc28d-551">`0x5`: Overflow</span></span><br/><br/>|
|`Bytes`|`win:UInt64`|<span data-ttu-id="dc28d-552">Liczba bajtów oznaczonych.</span><span class="sxs-lookup"><span data-stu-id="dc28d-552">The number of bytes marked.</span></span>|

## <a name="gcjoin_v2-event"></a><span data-ttu-id="dc28d-553">Zdarzenie GCJoin_V2</span><span class="sxs-lookup"><span data-stu-id="dc28d-553">GCJoin_V2 event</span></span>

<span data-ttu-id="dc28d-554">W poniższej tabeli przedstawiono słowo kluczowe i poziom:</span><span class="sxs-lookup"><span data-stu-id="dc28d-554">The following table shows the keyword and level:</span></span>

|<span data-ttu-id="dc28d-555">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-555">Keyword for raising the event</span></span>|<span data-ttu-id="dc28d-556">Poziom</span><span class="sxs-lookup"><span data-stu-id="dc28d-556">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="dc28d-557">`GCKeyword` 0x1</span><span class="sxs-lookup"><span data-stu-id="dc28d-557">`GCKeyword` (0x1)</span></span>|<span data-ttu-id="dc28d-558">Verbose (5)</span><span class="sxs-lookup"><span data-stu-id="dc28d-558">Verbose (5)</span></span>|

<span data-ttu-id="dc28d-559">W poniższej tabeli przedstawiono informacje o zdarzeniu:</span><span class="sxs-lookup"><span data-stu-id="dc28d-559">The following table shows the event information:</span></span>

|<span data-ttu-id="dc28d-560">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="dc28d-560">Event</span></span>|<span data-ttu-id="dc28d-561">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc28d-561">Event ID</span></span>|<span data-ttu-id="dc28d-562">Wywoływane, gdy</span><span class="sxs-lookup"><span data-stu-id="dc28d-562">Raised when</span></span>|
|-----------|--------------|-----------------|
|`GCJoin_V2`|<span data-ttu-id="dc28d-563">203</span><span class="sxs-lookup"><span data-stu-id="dc28d-563">203</span></span>|<span data-ttu-id="dc28d-564">Przyłączony wątek GC.</span><span class="sxs-lookup"><span data-stu-id="dc28d-564">A GC thread joined.</span></span>|

<span data-ttu-id="dc28d-565">W poniższej tabeli przedstawiono dane zdarzenia:</span><span class="sxs-lookup"><span data-stu-id="dc28d-565">The following table shows the event data:</span></span>

|<span data-ttu-id="dc28d-566">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="dc28d-566">Field name</span></span>|<span data-ttu-id="dc28d-567">Typ danych</span><span class="sxs-lookup"><span data-stu-id="dc28d-567">Data type</span></span>|<span data-ttu-id="dc28d-568">Opis</span><span class="sxs-lookup"><span data-stu-id="dc28d-568">Description</span></span>|
|----------------|---------------|-----------------|
|`Heap`|`win:UInt32`|<span data-ttu-id="dc28d-569">Numer sterty</span><span class="sxs-lookup"><span data-stu-id="dc28d-569">The heap number</span></span>|
|`JoinTime`|`win:UInt32`|<span data-ttu-id="dc28d-570">Wskazuje, czy to zdarzenie jest wyzwalane na początku sprzężenia, czy na końcu sprzężenia (w celu rozpoczęcia dołączania `0x0` `0x1` w celu dołączenia)</span><span class="sxs-lookup"><span data-stu-id="dc28d-570">Indicates whether this event is fired at the start of a join or end of a join (`0x0` for join start, `0x1` for join end)</span></span>|
|`JoinType`|`win:UInt32`|<span data-ttu-id="dc28d-571">Typ sprzężenia.</span><span class="sxs-lookup"><span data-stu-id="dc28d-571">The join type.</span></span> <br/><br/><span data-ttu-id="dc28d-572">`0x0`: Ostatnie połączenie</span><span class="sxs-lookup"><span data-stu-id="dc28d-572">`0x0`: Last Join</span></span><br/><br/><span data-ttu-id="dc28d-573">`0x1`: Dołącz</span><span class="sxs-lookup"><span data-stu-id="dc28d-573">`0x1`: Join</span></span> <br/><br/><span data-ttu-id="dc28d-574">`0x2`: Uruchom ponownie</span><span class="sxs-lookup"><span data-stu-id="dc28d-574">`0x2`: Restart</span></span> <br/><br/><span data-ttu-id="dc28d-575">`0x3`: Pierwsze odwrotne sprzężenie</span><span class="sxs-lookup"><span data-stu-id="dc28d-575">`0x3`: First Reverse Join</span></span><br/><br/><span data-ttu-id="dc28d-576">`0x4`: Odwrotne sprzężenie</span><span class="sxs-lookup"><span data-stu-id="dc28d-576">`0x4`: Reverse Join</span></span><br/><br/>|
|`ClrInstanceID`|`win:UInt16`|<span data-ttu-id="dc28d-577">Unikatowy identyfikator wystąpienia elementu CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="dc28d-577">Unique ID for the instance of CoreCLR.</span></span>|
