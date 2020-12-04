---
title: Monitoruj zdarzenia czasu wykonywania rywalizacji o blokadę
description: Zobacz zdarzenia ETW, które zbierają informacje specyficzne dla rywalizacji o blokadę monitora.
ms.date: 11/13/2020
ms.topic: reference
helpviewer_keywords:
- monitor lock contention events (CoreCLR)
- ETW, EventPipe, LTTng contention events (CoreCLR)
ms.openlocfilehash: 38e5f493d4b223b4839dbd6f814cf656722189b2
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "96589999"
---
# <a name="net-runtime-contention-events"></a><span data-ttu-id="055ad-103">Zdarzenia rywalizacji o środowisko uruchomieniowe platformy .NET</span><span class="sxs-lookup"><span data-stu-id="055ad-103">.NET runtime contention events</span></span>

<span data-ttu-id="055ad-104">Te zdarzenia środowiska uruchomieniowego przechwytują informacje o rywalizacjach o blokadę monitora, takich jak program `Monitor.Enter` lub słowo kluczowe lock języka C#.</span><span class="sxs-lookup"><span data-stu-id="055ad-104">These runtime events capture information about monitor lock contentions such as with `Monitor.Enter` or the C# lock keyword.</span></span> <span data-ttu-id="055ad-105">Aby uzyskać więcej informacji na temat korzystania z tych zdarzeń w celach diagnostycznych, zobacz [Rejestrowanie i śledzenie aplikacji .NET](../../core/diagnostics/logging-tracing.md) .</span><span class="sxs-lookup"><span data-stu-id="055ad-105">For more information about how to use these events for diagnostic purposes, see [logging and tracing .NET applications](../../core/diagnostics/logging-tracing.md)</span></span>

## <a name="contentionstart_v1-event"></a><span data-ttu-id="055ad-106">Zdarzenie ContentionStart_V1</span><span class="sxs-lookup"><span data-stu-id="055ad-106">ContentionStart_V1 event</span></span>

<span data-ttu-id="055ad-107">To zdarzenie jest emitowane na początku rywalizacji o blokadę monitora.</span><span class="sxs-lookup"><span data-stu-id="055ad-107">This event is emitted at the start of a monitor lock contention.</span></span>

|<span data-ttu-id="055ad-108">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="055ad-108">Keyword for raising the event</span></span>|<span data-ttu-id="055ad-109">Poziom</span><span class="sxs-lookup"><span data-stu-id="055ad-109">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="055ad-110">`ContentionKeyword` 0x4000</span><span class="sxs-lookup"><span data-stu-id="055ad-110">`ContentionKeyword` (0x4000)</span></span>|<span data-ttu-id="055ad-111">Informacyjny (4)</span><span class="sxs-lookup"><span data-stu-id="055ad-111">Informational (4)</span></span>|

 <span data-ttu-id="055ad-112">W poniższej tabeli przedstawiono informacje o zdarzeniach.</span><span class="sxs-lookup"><span data-stu-id="055ad-112">The following table shows event information.</span></span>

|<span data-ttu-id="055ad-113">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="055ad-113">Event</span></span>|<span data-ttu-id="055ad-114">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="055ad-114">Event ID</span></span>|<span data-ttu-id="055ad-115">Wywoływane, gdy</span><span class="sxs-lookup"><span data-stu-id="055ad-115">Raised when</span></span>|
|-----------|--------------|-----------------|
|`ContentionStart_V1`|<span data-ttu-id="055ad-116">81</span><span class="sxs-lookup"><span data-stu-id="055ad-116">81</span></span>|<span data-ttu-id="055ad-117">Rozpocznie się rywalizacja o blokady monitora.</span><span class="sxs-lookup"><span data-stu-id="055ad-117">A monitor lock contention starts.</span></span>|

|<span data-ttu-id="055ad-118">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="055ad-118">Field name</span></span>|<span data-ttu-id="055ad-119">Typ danych</span><span class="sxs-lookup"><span data-stu-id="055ad-119">Data type</span></span>|<span data-ttu-id="055ad-120">Opis</span><span class="sxs-lookup"><span data-stu-id="055ad-120">Description</span></span>|
|----------------|---------------|-----------------|
|`Flags`|`win:UInt8`|<span data-ttu-id="055ad-121">`0` dla zarządzanych; `1` dla natywnego.</span><span class="sxs-lookup"><span data-stu-id="055ad-121">`0` for managed; `1` for native.</span></span>|
|`ClrInstanceID`|`win:UInt16`|<span data-ttu-id="055ad-122">Unikatowy identyfikator wystąpienia elementu CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="055ad-122">Unique ID for the instance of CoreCLR.</span></span>|

## <a name="contentionstop_v1-event"></a><span data-ttu-id="055ad-123">Zdarzenie ContentionStop_V1</span><span class="sxs-lookup"><span data-stu-id="055ad-123">ContentionStop_V1 event</span></span>

<span data-ttu-id="055ad-124">To zdarzenie jest emitowane po zakończeniu rywalizacji o blokadę monitora.</span><span class="sxs-lookup"><span data-stu-id="055ad-124">This event is emitted at the end of a monitor lock contention.</span></span>

|<span data-ttu-id="055ad-125">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="055ad-125">Keyword for raising the event</span></span>|<span data-ttu-id="055ad-126">Poziom</span><span class="sxs-lookup"><span data-stu-id="055ad-126">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="055ad-127">`ContentionKeyword` 0x4000</span><span class="sxs-lookup"><span data-stu-id="055ad-127">`ContentionKeyword` (0x4000)</span></span>|<span data-ttu-id="055ad-128">Informacyjny (4)</span><span class="sxs-lookup"><span data-stu-id="055ad-128">Informational (4)</span></span>|

 <span data-ttu-id="055ad-129">W poniższej tabeli przedstawiono informacje o zdarzeniach.</span><span class="sxs-lookup"><span data-stu-id="055ad-129">The following table shows event information.</span></span>

|<span data-ttu-id="055ad-130">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="055ad-130">Event</span></span>|<span data-ttu-id="055ad-131">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="055ad-131">Event ID</span></span>|<span data-ttu-id="055ad-132">Wywoływane, gdy</span><span class="sxs-lookup"><span data-stu-id="055ad-132">Raised when</span></span>|
|-----------|--------------|-----------------|
|`ContentionStop_V1`|<span data-ttu-id="055ad-133">91</span><span class="sxs-lookup"><span data-stu-id="055ad-133">91</span></span>|<span data-ttu-id="055ad-134">Zakończyło się rywalizacja blokady monitora.</span><span class="sxs-lookup"><span data-stu-id="055ad-134">A monitor lock contention ends.</span></span>|

|<span data-ttu-id="055ad-135">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="055ad-135">Field name</span></span>|<span data-ttu-id="055ad-136">Typ danych</span><span class="sxs-lookup"><span data-stu-id="055ad-136">Data type</span></span>|<span data-ttu-id="055ad-137">Opis</span><span class="sxs-lookup"><span data-stu-id="055ad-137">Description</span></span>|
|----------------|---------------|-----------------|
|`Flags`|`win:UInt8`|<span data-ttu-id="055ad-138">`0` dla zarządzanych; `1` dla natywnego.</span><span class="sxs-lookup"><span data-stu-id="055ad-138">`0` for managed; `1` for native.</span></span>|
|`ClrInstanceID`|`win:UInt16`|<span data-ttu-id="055ad-139">Unikatowy identyfikator wystąpienia elementu CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="055ad-139">Unique ID for the instance of CoreCLR.</span></span>|
|`DurationNs`|`win:Double`|<span data-ttu-id="055ad-140">Czas trwania rywalizacji w nanosekundach.</span><span class="sxs-lookup"><span data-stu-id="055ad-140">Duration of the contention in nanoseconds.</span></span>|
