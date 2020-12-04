---
title: Zdarzenia środowiska uruchomieniowego
description: Przeglądanie zdarzeń diagnostycznych emitowanych przez środowisko uruchomieniowe platformy .NET (CoreCLR), które mogą być używane z funkcją ETW, LTTng lub EventPipe.
ms.date: 11/13/2020
ms.topic: reference
helpviewer_keywords:
- runtime events (CoreCLR)
- ETW, EventPipe runtime events (CoreCLR)
ms.openlocfilehash: 33fa7275ce40934ce043b4d0dba5749c37515755
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "96589996"
---
# <a name="net-runtime-events"></a><span data-ttu-id="e698d-103">Zdarzenia środowiska uruchomieniowego platformy .NET</span><span class="sxs-lookup"><span data-stu-id="e698d-103">.NET runtime events</span></span>

<span data-ttu-id="e698d-104">Środowisko uruchomieniowe .NET (CoreCLR) emituje różne zdarzenia, których można użyć do diagnozowania problemów z aplikacją .NET, które mogą być używane przez różne mechanizmy `ETW` , takie jak, `LTTng` i `EventPipe` .</span><span class="sxs-lookup"><span data-stu-id="e698d-104">The .NET runtime (CoreCLR) emits various events that can be used to diagnose issues with your .NET application that can be consumed via various mechanisms such as `ETW`, `LTTng`, and `EventPipe`.</span></span>

<span data-ttu-id="e698d-105">Ten dokument służy jako odwołanie do zdarzeń, które są wywoływane przez środowisko uruchomieniowe platformy .NET Core.</span><span class="sxs-lookup"><span data-stu-id="e698d-105">This document serves as a reference on the events that are fired by .NET Core runtime.</span></span>

<span data-ttu-id="e698d-106">Zdarzenia środowiska uruchomieniowego w .NET Framework można znaleźć w temacie [zdarzenia ETW środowiska CLR](../../framework/performance/clr-etw-events.md).</span><span class="sxs-lookup"><span data-stu-id="e698d-106">For runtime events in .NET Framework, see [CLR ETW Events](../../framework/performance/clr-etw-events.md).</span></span>

## <a name="in-this-section"></a><span data-ttu-id="e698d-107">W tej sekcji</span><span class="sxs-lookup"><span data-stu-id="e698d-107">In this section</span></span>

<span data-ttu-id="e698d-108">[Zdarzenia rywalizacji](runtime-contention-events.md)</span><span class="sxs-lookup"><span data-stu-id="e698d-108">[Contention Events](runtime-contention-events.md)</span></span>\
<span data-ttu-id="e698d-109">Te zdarzenia zbierają informacje o rywalizacjach o blokady monitora.</span><span class="sxs-lookup"><span data-stu-id="e698d-109">These events collect information about monitor lock contentions.</span></span>

<span data-ttu-id="e698d-110">[Zdarzenia wyrzucania elementów bezużytecznych](runtime-garbage-collection-events.md)</span><span class="sxs-lookup"><span data-stu-id="e698d-110">[Garbage Collection Events](runtime-garbage-collection-events.md)</span></span>\
<span data-ttu-id="e698d-111">Te zdarzenia zbierają informacje dotyczące wyrzucania elementów bezużytecznych.</span><span class="sxs-lookup"><span data-stu-id="e698d-111">These events collect information pertaining to garbage collection.</span></span> <span data-ttu-id="e698d-112">Ułatwiają one diagnostykę i debugowanie, w tym określanie, ile razy zostało wykonane wyrzucanie elementów bezużytecznych, ile pamięci zostało zwolnione podczas wyrzucania elementów bezużytecznych itp.</span><span class="sxs-lookup"><span data-stu-id="e698d-112">They help in diagnostics and debugging, including determining how many times garbage collection was performed, how much memory was freed during garbage collection, etc.</span></span>

<span data-ttu-id="e698d-113">[Zdarzenia wyjątków](runtime-exception-events.md)</span><span class="sxs-lookup"><span data-stu-id="e698d-113">[Exception Events](runtime-exception-events.md)</span></span>\
<span data-ttu-id="e698d-114">Te zdarzenia środowiska uruchomieniowego przechwytują informacje o zgłaszanych wyjątkach.</span><span class="sxs-lookup"><span data-stu-id="e698d-114">These runtime events capture information about exceptions that are thrown.</span></span>

<span data-ttu-id="e698d-115">[Zdarzenia międzyoperacyjności](runtime-interop-events.md)</span><span class="sxs-lookup"><span data-stu-id="e698d-115">[Interop Events](runtime-interop-events.md)</span></span>\
<span data-ttu-id="e698d-116">Te zdarzenia środowiska uruchomieniowego przechwytują informacje o generacji wygenerowanej w języku pośrednim (CIL).</span><span class="sxs-lookup"><span data-stu-id="e698d-116">These runtime events capture information about Common Intermediate Language (CIL) stub generation.</span></span>

<span data-ttu-id="e698d-117">[Zdarzenia modułu ładującego i spinacza](runtime-loader-binder-events.md)</span><span class="sxs-lookup"><span data-stu-id="e698d-117">[Loader and Binder Events](runtime-loader-binder-events.md)</span></span>\
<span data-ttu-id="e698d-118">Te zdarzenia zbierają informacje dotyczące ładowania i zwalniania zestawów i modułów.</span><span class="sxs-lookup"><span data-stu-id="e698d-118">These events collect information relating to loading and unloading assemblies and modules.</span></span>

<span data-ttu-id="e698d-119">[Zdarzenia metody](runtime-method-events.md)</span><span class="sxs-lookup"><span data-stu-id="e698d-119">[Method Events](runtime-method-events.md)</span></span>\
<span data-ttu-id="e698d-120">Te zdarzenia zbierają informacje, które są specyficzne dla metod.</span><span class="sxs-lookup"><span data-stu-id="e698d-120">These events collect information that is specific to methods.</span></span> <span data-ttu-id="e698d-121">Ładunek tych zdarzeń jest wymagany do rozpoznawania symboli.</span><span class="sxs-lookup"><span data-stu-id="e698d-121">The payload of these events is required for symbol resolution.</span></span> <span data-ttu-id="e698d-122">Ponadto te zdarzenia zapewniają przydatne informacje, takie jak liczba przypadków wywołania metody.</span><span class="sxs-lookup"><span data-stu-id="e698d-122">In addition, these events provide helpful information such as the number of times a method was called.</span></span>

<span data-ttu-id="e698d-123">[Zdarzenia wątku](runtime-thread-events.md)</span><span class="sxs-lookup"><span data-stu-id="e698d-123">[Thread Events](runtime-thread-events.md)</span></span>\
<span data-ttu-id="e698d-124">Te zdarzenia zbierają informacje o wątkach procesów roboczych i we/wy.</span><span class="sxs-lookup"><span data-stu-id="e698d-124">These events collect information about worker and I/O threads.</span></span>

<span data-ttu-id="e698d-125">[Zdarzenia typu](runtime-type-events.md)</span><span class="sxs-lookup"><span data-stu-id="e698d-125">[Type Events](runtime-type-events.md)</span></span>\
<span data-ttu-id="e698d-126">Te zdarzenia zbierają informacje o systemie typów.</span><span class="sxs-lookup"><span data-stu-id="e698d-126">These events collect information about the type system.</span></span>
