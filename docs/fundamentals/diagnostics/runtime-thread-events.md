---
title: Zdarzenia czasu wykonywania puli wątków
description: Zobacz zdarzenia puli wątków środowiska uruchomieniowego platformy .NET, które zbierają informacje diagnostyczne dotyczące puli wątków w programie .NET Core. Zdarzenia puli wątków to zdarzenia puli wątków roboczych lub zdarzenia puli wątków we/wy.
ms.date: 11/13/2020
ms.topic: reference
helpviewer_keywords:
- ThreadPool events (CoreCLR)
- ETW, thread pool events (CoreCLR)
ms.openlocfilehash: cdd6041c5842d4922c60e33daf6db366f7d35327
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96590044"
---
# <a name="net-runtime-thread-pool-events"></a><span data-ttu-id="4bc2e-104">Zdarzenia puli wątków środowiska uruchomieniowego .NET</span><span class="sxs-lookup"><span data-stu-id="4bc2e-104">.NET runtime thread pool events</span></span>

<span data-ttu-id="4bc2e-105">Te zdarzenia zbierają informacje o wątkach procesów roboczych i we/wy w puli wątków.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-105">These events collect information about worker and I/O threads in the threadpool.</span></span> <span data-ttu-id="4bc2e-106">Aby uzyskać więcej informacji na temat korzystania z tych zdarzeń w celach diagnostycznych, zobacz [Rejestrowanie i śledzenie aplikacji .NET](../../core/diagnostics/logging-tracing.md) .</span><span class="sxs-lookup"><span data-stu-id="4bc2e-106">For more information about how to use these events for diagnostic purposes, see [logging and tracing .NET applications](../../core/diagnostics/logging-tracing.md)</span></span>

## <a name="iothreadcreate_v1-event"></a><span data-ttu-id="4bc2e-107">Zdarzenie IOThreadCreate_V1</span><span class="sxs-lookup"><span data-stu-id="4bc2e-107">IOThreadCreate_V1 event</span></span>

 <span data-ttu-id="4bc2e-108">W poniższej tabeli przedstawiono słowo kluczowe i poziom.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-108">The following table shows the keyword and level.</span></span>

|<span data-ttu-id="4bc2e-109">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-109">Keyword for raising the event</span></span>|<span data-ttu-id="4bc2e-110">Poziom</span><span class="sxs-lookup"><span data-stu-id="4bc2e-110">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="4bc2e-111">`ThreadingKeyword` 0x10000</span><span class="sxs-lookup"><span data-stu-id="4bc2e-111">`ThreadingKeyword` (0x10000)</span></span>|<span data-ttu-id="4bc2e-112">Informacyjny (4)</span><span class="sxs-lookup"><span data-stu-id="4bc2e-112">Informational (4)</span></span>|

 <span data-ttu-id="4bc2e-113">W poniższej tabeli przedstawiono informacje o zdarzeniu.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-113">The following table shows the event information.</span></span>

|<span data-ttu-id="4bc2e-114">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="4bc2e-114">Event</span></span>|<span data-ttu-id="4bc2e-115">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-115">Event ID</span></span>|<span data-ttu-id="4bc2e-116">Wywoływane, gdy</span><span class="sxs-lookup"><span data-stu-id="4bc2e-116">Raised when</span></span>|
|-----------------------------------|-----------|
|`IOThreadCreate_V1`|<span data-ttu-id="4bc2e-117">44</span><span class="sxs-lookup"><span data-stu-id="4bc2e-117">44</span></span>|<span data-ttu-id="4bc2e-118">W puli wątków tworzony jest wątek we/wy.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-118">An I/O thread is created in the thread pool.</span></span>|

 <span data-ttu-id="4bc2e-119">W poniższej tabeli przedstawiono dane zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-119">The following table shows the event data.</span></span>

|<span data-ttu-id="4bc2e-120">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="4bc2e-120">Field name</span></span>|<span data-ttu-id="4bc2e-121">Typ danych</span><span class="sxs-lookup"><span data-stu-id="4bc2e-121">Data type</span></span>|<span data-ttu-id="4bc2e-122">Opis</span><span class="sxs-lookup"><span data-stu-id="4bc2e-122">Description</span></span>|
|----------------|---------------|-----------------|
|`Count`|`win:UInt64`|<span data-ttu-id="4bc2e-123">Liczba wątków we/wy, łącznie z nowo utworzonym wątkiem.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-123">Number of I/O threads, including the newly created thread.</span></span>|
|`NumRetired`|`win:UInt64`|<span data-ttu-id="4bc2e-124">Liczba wycofanych wątków roboczych.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-124">Number of retired worker threads.</span></span>|
|`ClrInstanceID`|`win:UInt16`|<span data-ttu-id="4bc2e-125">Unikatowy identyfikator wystąpienia CLR lub CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-125">Unique ID for the instance of CLR or CoreCLR.</span></span>|

## <a name="iothreadterminate_v1-event"></a><span data-ttu-id="4bc2e-126">Zdarzenie IOThreadTerminate_V1</span><span class="sxs-lookup"><span data-stu-id="4bc2e-126">IOThreadTerminate_V1 event</span></span>

 <span data-ttu-id="4bc2e-127">W poniższej tabeli przedstawiono słowo kluczowe i poziom</span><span class="sxs-lookup"><span data-stu-id="4bc2e-127">The following table shows the keyword and level</span></span>

|<span data-ttu-id="4bc2e-128">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-128">Keyword for raising the event</span></span>|<span data-ttu-id="4bc2e-129">Poziom</span><span class="sxs-lookup"><span data-stu-id="4bc2e-129">Level</span></span>
|-----------------------------------|-----------
|<span data-ttu-id="4bc2e-130">`ThreadingKeyword` 0x10000</span><span class="sxs-lookup"><span data-stu-id="4bc2e-130">`ThreadingKeyword` (0x10000)</span></span>|<span data-ttu-id="4bc2e-131">Informacyjny (4)</span><span class="sxs-lookup"><span data-stu-id="4bc2e-131">Informational (4)</span></span>

 <span data-ttu-id="4bc2e-132">W poniższej tabeli przedstawiono informacje o zdarzeniu.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-132">The following table shows the event information.</span></span>

|<span data-ttu-id="4bc2e-133">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="4bc2e-133">Event</span></span>|<span data-ttu-id="4bc2e-134">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-134">Event ID</span></span>|<span data-ttu-id="4bc2e-135">Wywoływane, gdy</span><span class="sxs-lookup"><span data-stu-id="4bc2e-135">Raised when</span></span>|
|-----------|--------------|-----------------|
|`IOThreadTerminate`|<span data-ttu-id="4bc2e-136">45</span><span class="sxs-lookup"><span data-stu-id="4bc2e-136">45</span></span>|<span data-ttu-id="4bc2e-137">Wątek we/wy zostanie przerwany w puli wątków.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-137">An I/O thread is terminated in the thread pool.</span></span>|

 <span data-ttu-id="4bc2e-138">W poniższej tabeli przedstawiono dane zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-138">The following table shows the event data.</span></span>

|<span data-ttu-id="4bc2e-139">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="4bc2e-139">Field name</span></span>|<span data-ttu-id="4bc2e-140">Typ danych</span><span class="sxs-lookup"><span data-stu-id="4bc2e-140">Data type</span></span>|<span data-ttu-id="4bc2e-141">Opis</span><span class="sxs-lookup"><span data-stu-id="4bc2e-141">Description</span></span>|
|----------------|---------------|-----------------|
|`Count`|`win:UInt64`|<span data-ttu-id="4bc2e-142">Liczba wątków we/wy pozostałych w puli wątków.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-142">Number of I/O threads remaining in the thread pool.</span></span>|
|`NumRetired`|`win:UInt64`|<span data-ttu-id="4bc2e-143">Liczba wycofanych wątków we/wy.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-143">Number of retired I/O threads.</span></span>|
|`ClrInstanceID`|`win:UInt16`|<span data-ttu-id="4bc2e-144">Unikatowy identyfikator wystąpienia CLR lub CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-144">Unique ID for the instance of CLR or CoreCLR.</span></span>|

## <a name="iothreadretire_v1-event"></a><span data-ttu-id="4bc2e-145">Zdarzenie IOThreadRetire_V1</span><span class="sxs-lookup"><span data-stu-id="4bc2e-145">IOThreadRetire_V1 event</span></span>

 <span data-ttu-id="4bc2e-146">W poniższej tabeli przedstawiono słowo kluczowe i poziom.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-146">The following table shows the keyword and level.</span></span>

|<span data-ttu-id="4bc2e-147">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-147">Keyword for raising the event</span></span>|<span data-ttu-id="4bc2e-148">Poziom</span><span class="sxs-lookup"><span data-stu-id="4bc2e-148">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="4bc2e-149">`ThreadingKeyword` 0x10000</span><span class="sxs-lookup"><span data-stu-id="4bc2e-149">`ThreadingKeyword` (0x10000)</span></span>|<span data-ttu-id="4bc2e-150">Informacyjny (4)</span><span class="sxs-lookup"><span data-stu-id="4bc2e-150">Informational (4)</span></span>|

 <span data-ttu-id="4bc2e-151">W poniższej tabeli przedstawiono informacje o zdarzeniu.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-151">The following table shows the event information.</span></span>

|<span data-ttu-id="4bc2e-152">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="4bc2e-152">Event</span></span>|<span data-ttu-id="4bc2e-153">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-153">Event ID</span></span>|<span data-ttu-id="4bc2e-154">Wywoływane, gdy</span><span class="sxs-lookup"><span data-stu-id="4bc2e-154">Raised when</span></span>|
|-----------|--------------|-----------------|
|`IOThreadRetire_V1`|<span data-ttu-id="4bc2e-155">46</span><span class="sxs-lookup"><span data-stu-id="4bc2e-155">46</span></span>|<span data-ttu-id="4bc2e-156">Wątek we/wy zostaje kandydatem do wycofania.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-156">An I/O thread becomes a retirement candidate.</span></span>|

 <span data-ttu-id="4bc2e-157">W poniższej tabeli przedstawiono dane zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-157">The following table shows the event data.</span></span>

|<span data-ttu-id="4bc2e-158">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="4bc2e-158">Field name</span></span>|<span data-ttu-id="4bc2e-159">Typ danych</span><span class="sxs-lookup"><span data-stu-id="4bc2e-159">Data type</span></span>|<span data-ttu-id="4bc2e-160">Opis</span><span class="sxs-lookup"><span data-stu-id="4bc2e-160">Description</span></span>|
|----------------|---------------|-----------------|
|`Count`|`win:UInt64`|<span data-ttu-id="4bc2e-161">Liczba wątków we/wy pozostałych w puli wątków.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-161">Number of I/O threads remaining in the thread pool.</span></span>|
|`NumRetired`|`win:UInt64`|<span data-ttu-id="4bc2e-162">Liczba wycofanych wątków we/wy.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-162">Number of retired I/O threads.</span></span>|
|`ClrInstanceID`|`win:UInt16`|<span data-ttu-id="4bc2e-163">Unikatowy identyfikator wystąpienia CLR lub CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-163">Unique ID for the instance of CLR or CoreCLR.</span></span>|

## <a name="iothreadunretire_v1-event"></a><span data-ttu-id="4bc2e-164">Zdarzenie IOThreadUnretire_V1</span><span class="sxs-lookup"><span data-stu-id="4bc2e-164">IOThreadUnretire_V1 event</span></span>

 <span data-ttu-id="4bc2e-165">W poniższej tabeli przedstawiono słowo kluczowe i poziom.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-165">The following table shows the keyword and level.</span></span>

|<span data-ttu-id="4bc2e-166">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-166">Keyword for raising the event</span></span>|<span data-ttu-id="4bc2e-167">Poziom</span><span class="sxs-lookup"><span data-stu-id="4bc2e-167">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="4bc2e-168">`ThreadingKeyword` 0x10000</span><span class="sxs-lookup"><span data-stu-id="4bc2e-168">`ThreadingKeyword` (0x10000)</span></span>|<span data-ttu-id="4bc2e-169">Informacyjny (4)</span><span class="sxs-lookup"><span data-stu-id="4bc2e-169">Informational (4)</span></span>|

 <span data-ttu-id="4bc2e-170">W poniższej tabeli przedstawiono informacje o zdarzeniu.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-170">The following table shows the event information.</span></span>

|<span data-ttu-id="4bc2e-171">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="4bc2e-171">Event</span></span>|<span data-ttu-id="4bc2e-172">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-172">Event ID</span></span>|<span data-ttu-id="4bc2e-173">Wywoływane, gdy</span><span class="sxs-lookup"><span data-stu-id="4bc2e-173">Raised when</span></span>|
|-----------|--------------|-----------------|
|`IOThreadUnretire_V1`|<span data-ttu-id="4bc2e-174">47</span><span class="sxs-lookup"><span data-stu-id="4bc2e-174">47</span></span>|<span data-ttu-id="4bc2e-175">Wątek we/wy jest wycofywany ze względu na liczbę operacji we/wy, która dotarła w czasie oczekiwania, gdy wątek stanie się kandydatem wycofania.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-175">An I/O thread is unretired because of I/O that arrives within a waiting period after the thread becomes a retirement candidate.</span></span>|

 <span data-ttu-id="4bc2e-176">W poniższej tabeli przedstawiono dane zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-176">The following table shows the event data.</span></span>

|<span data-ttu-id="4bc2e-177">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="4bc2e-177">Field name</span></span>|<span data-ttu-id="4bc2e-178">Typ danych</span><span class="sxs-lookup"><span data-stu-id="4bc2e-178">Data type</span></span>|<span data-ttu-id="4bc2e-179">Opis</span><span class="sxs-lookup"><span data-stu-id="4bc2e-179">Description</span></span>|
|----------------|---------------|-----------------|
|`Count`|`win:UInt64`|<span data-ttu-id="4bc2e-180">Liczba wątków we/wy w puli wątków, z uwzględnieniem tego.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-180">Number of I/O threads in the thread pool, including this one.</span></span>|
|`NumRetired`|`win:UInt64`|<span data-ttu-id="4bc2e-181">Liczba wycofanych wątków we/wy.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-181">Number of retired I/O threads.</span></span>|
|`ClrInstanceID`|`Win:UInt16`|<span data-ttu-id="4bc2e-182">Unikatowy identyfikator wystąpienia CLR lub CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-182">Unique ID for the instance of CLR or CoreCLR.</span></span>|

## <a name="threadpoolworkerthreadstart-event"></a><span data-ttu-id="4bc2e-183">Zdarzenie ThreadPoolWorkerThreadStart</span><span class="sxs-lookup"><span data-stu-id="4bc2e-183">ThreadPoolWorkerThreadStart event</span></span>

|<span data-ttu-id="4bc2e-184">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-184">Keyword for raising the event</span></span>|<span data-ttu-id="4bc2e-185">Poziom</span><span class="sxs-lookup"><span data-stu-id="4bc2e-185">Level</span></span>|
|-----------------------------------|-----------|-----------|
|<span data-ttu-id="4bc2e-186">`ThreadingKeyword` 0x10000</span><span class="sxs-lookup"><span data-stu-id="4bc2e-186">`ThreadingKeyword` (0x10000)</span></span>|<span data-ttu-id="4bc2e-187">Informacyjny (4)</span><span class="sxs-lookup"><span data-stu-id="4bc2e-187">Informational (4)</span></span>|

|<span data-ttu-id="4bc2e-188">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="4bc2e-188">Event</span></span>|<span data-ttu-id="4bc2e-189">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-189">Event ID</span></span>|<span data-ttu-id="4bc2e-190">Opis</span><span class="sxs-lookup"><span data-stu-id="4bc2e-190">Description</span></span>|
|-----------|--------------|-----------------|
|`ThreadPoolWorkerThreadStart`|<span data-ttu-id="4bc2e-191">50</span><span class="sxs-lookup"><span data-stu-id="4bc2e-191">50</span></span>|<span data-ttu-id="4bc2e-192">Tworzony jest wątek roboczy.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-192">A worker thread is created.</span></span>|

|<span data-ttu-id="4bc2e-193">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="4bc2e-193">Field name</span></span>|<span data-ttu-id="4bc2e-194">Typ danych</span><span class="sxs-lookup"><span data-stu-id="4bc2e-194">Data type</span></span>|<span data-ttu-id="4bc2e-195">Opis</span><span class="sxs-lookup"><span data-stu-id="4bc2e-195">Description</span></span>|
|----------------|---------------|-----------------|
|`ActiveWorkerThreadCount`|`win:UInt32`|<span data-ttu-id="4bc2e-196">Liczba wątków roboczych dostępnych do przetwarzania pracy, w tym tych, które już przetwarzają prace.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-196">Number of worker threads available to process work, including those that are already processing work.</span></span>|
|`RetiredWorkerThreadCount`|`win:UInt32`|<span data-ttu-id="4bc2e-197">Liczba wątków roboczych, które nie są dostępne do przetwarzania pracy, ale które są przechowywane w rezerwie w przypadku późniejszej liczby wątków.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-197">Number of worker threads that are not available to process work, but that are being held in reserve in case more threads are needed later.</span></span>|
|`ClrInstanceID`|`win:UInt16`|<span data-ttu-id="4bc2e-198">Unikatowy identyfikator wystąpienia CLR lub CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-198">Unique ID for the instance of CLR or CoreCLR.</span></span>|

## <a name="threadpoolworkerthreadstop-event"></a><span data-ttu-id="4bc2e-199">Zdarzenie ThreadPoolWorkerThreadStop</span><span class="sxs-lookup"><span data-stu-id="4bc2e-199">ThreadPoolWorkerThreadStop event</span></span>

|<span data-ttu-id="4bc2e-200">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-200">Keyword for raising the event</span></span>|<span data-ttu-id="4bc2e-201">Poziom</span><span class="sxs-lookup"><span data-stu-id="4bc2e-201">Level</span></span>|
|-----------------------------------|-----------|-----------|
|<span data-ttu-id="4bc2e-202">`ThreadingKeyword` 0x10000</span><span class="sxs-lookup"><span data-stu-id="4bc2e-202">`ThreadingKeyword` (0x10000)</span></span>|<span data-ttu-id="4bc2e-203">Informacyjny (4)</span><span class="sxs-lookup"><span data-stu-id="4bc2e-203">Informational (4)</span></span>|

|<span data-ttu-id="4bc2e-204">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="4bc2e-204">Event</span></span>|<span data-ttu-id="4bc2e-205">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-205">Event ID</span></span>|<span data-ttu-id="4bc2e-206">Opis</span><span class="sxs-lookup"><span data-stu-id="4bc2e-206">Description</span></span>|
|-----------|--------------|-----------------|
|`ThreadPoolWorkerThreadStop`|<span data-ttu-id="4bc2e-207">51</span><span class="sxs-lookup"><span data-stu-id="4bc2e-207">51</span></span>|<span data-ttu-id="4bc2e-208">Wątek roboczy został zatrzymany.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-208">A worker thread is stopped.</span></span>|

|<span data-ttu-id="4bc2e-209">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="4bc2e-209">Field name</span></span>|<span data-ttu-id="4bc2e-210">Typ danych</span><span class="sxs-lookup"><span data-stu-id="4bc2e-210">Data type</span></span>|<span data-ttu-id="4bc2e-211">Opis</span><span class="sxs-lookup"><span data-stu-id="4bc2e-211">Description</span></span>|
|----------------|---------------|-----------------|
|`ActiveWorkerThreadCount`|`win:UInt32`|<span data-ttu-id="4bc2e-212">Liczba wątków roboczych dostępnych do przetwarzania pracy, w tym tych, które już przetwarzają prace.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-212">Number of worker threads available to process work, including those that are already processing work.</span></span>|
|`RetiredWorkerThreadCount`|`win:UInt32`|<span data-ttu-id="4bc2e-213">Liczba wątków roboczych, które nie są dostępne do przetwarzania pracy, ale które są przechowywane w rezerwie w przypadku późniejszej liczby wątków.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-213">Number of worker threads that are not available to process work, but that are being held in reserve in case more threads are needed later.</span></span>|
|`ClrInstanceID`|`win:UInt16`|<span data-ttu-id="4bc2e-214">Unikatowy identyfikator wystąpienia CLR lub CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-214">Unique ID for the instance of CLR or CoreCLR.</span></span>|

## <a name="threadpoolworkerthreadwait-event"></a><span data-ttu-id="4bc2e-215">Zdarzenie ThreadPoolWorkerThreadWait</span><span class="sxs-lookup"><span data-stu-id="4bc2e-215">ThreadPoolWorkerThreadWait event</span></span>

|<span data-ttu-id="4bc2e-216">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-216">Keyword for raising the event</span></span>|<span data-ttu-id="4bc2e-217">Poziom</span><span class="sxs-lookup"><span data-stu-id="4bc2e-217">Level</span></span>|
|-----------------------------------|-----------|-----------|
|<span data-ttu-id="4bc2e-218">`ThreadingKeyword` 0x10000</span><span class="sxs-lookup"><span data-stu-id="4bc2e-218">`ThreadingKeyword` (0x10000)</span></span>|<span data-ttu-id="4bc2e-219">Informacyjny (4)</span><span class="sxs-lookup"><span data-stu-id="4bc2e-219">Informational (4)</span></span>|

|<span data-ttu-id="4bc2e-220">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="4bc2e-220">Event</span></span>|<span data-ttu-id="4bc2e-221">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-221">Event ID</span></span>|<span data-ttu-id="4bc2e-222">Opis</span><span class="sxs-lookup"><span data-stu-id="4bc2e-222">Description</span></span>|
|-----------|--------------|-----------------|
|`ThreadPoolWorkerThreadWait`|<span data-ttu-id="4bc2e-223">57</span><span class="sxs-lookup"><span data-stu-id="4bc2e-223">57</span></span>|<span data-ttu-id="4bc2e-224">Wątek roboczy zaczyna czekać na pracę.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-224">A worker thread starts waiting for work.</span></span>|

|<span data-ttu-id="4bc2e-225">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="4bc2e-225">Field name</span></span>|<span data-ttu-id="4bc2e-226">Typ danych</span><span class="sxs-lookup"><span data-stu-id="4bc2e-226">Data type</span></span>|<span data-ttu-id="4bc2e-227">Opis</span><span class="sxs-lookup"><span data-stu-id="4bc2e-227">Description</span></span>|
|----------------|---------------|-----------------|
|`ActiveWorkerThreadCount`|`win:UInt32`|<span data-ttu-id="4bc2e-228">Liczba wątków roboczych dostępnych do przetwarzania pracy, w tym tych, które już przetwarzają prace.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-228">Number of worker threads available to process work, including those that are already processing work.</span></span>|
|`RetiredWorkerThreadCount`|`win:UInt32`|<span data-ttu-id="4bc2e-229">Liczba wątków roboczych, które nie są dostępne do przetwarzania pracy, ale które są przechowywane w rezerwie w przypadku późniejszej liczby wątków.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-229">Number of worker threads that are not available to process work, but that are being held in reserve in case more threads are needed later.</span></span>|
|`ClrInstanceID`|`win:UInt16`|<span data-ttu-id="4bc2e-230">Unikatowy identyfikator wystąpienia CLR lub CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-230">Unique ID for the instance of CLR or CoreCLR.</span></span>|

## <a name="threadpoolworkerthreadretirementstart-event"></a><span data-ttu-id="4bc2e-231">Zdarzenie ThreadPoolWorkerThreadRetirementStart</span><span class="sxs-lookup"><span data-stu-id="4bc2e-231">ThreadPoolWorkerThreadRetirementStart event</span></span>

|<span data-ttu-id="4bc2e-232">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-232">Keyword for raising the event</span></span>|<span data-ttu-id="4bc2e-233">Poziom</span><span class="sxs-lookup"><span data-stu-id="4bc2e-233">Level</span></span>|
|-----------------------------------|-----------|-----------|
|<span data-ttu-id="4bc2e-234">`ThreadingKeyword` 0x10000</span><span class="sxs-lookup"><span data-stu-id="4bc2e-234">`ThreadingKeyword` (0x10000)</span></span>|<span data-ttu-id="4bc2e-235">Informacyjny (4)</span><span class="sxs-lookup"><span data-stu-id="4bc2e-235">Informational (4)</span></span>|

|<span data-ttu-id="4bc2e-236">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="4bc2e-236">Event</span></span>|<span data-ttu-id="4bc2e-237">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-237">Event ID</span></span>|<span data-ttu-id="4bc2e-238">Opis</span><span class="sxs-lookup"><span data-stu-id="4bc2e-238">Description</span></span>|
|-----------|--------------|-----------------|
|`ThreadPoolWorkerThreadRetirementStart`|<span data-ttu-id="4bc2e-239">52</span><span class="sxs-lookup"><span data-stu-id="4bc2e-239">52</span></span>|<span data-ttu-id="4bc2e-240">Wątek roboczy jest przeoponą.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-240">A worker thread retires.</span></span>|

|<span data-ttu-id="4bc2e-241">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="4bc2e-241">Field name</span></span>|<span data-ttu-id="4bc2e-242">Typ danych</span><span class="sxs-lookup"><span data-stu-id="4bc2e-242">Data type</span></span>|<span data-ttu-id="4bc2e-243">Opis</span><span class="sxs-lookup"><span data-stu-id="4bc2e-243">Description</span></span>|
|----------------|---------------|-----------------|
|`ActiveWorkerThreadCount`|`win:UInt32`|<span data-ttu-id="4bc2e-244">Liczba wątków roboczych dostępnych do przetwarzania pracy, w tym tych, które już przetwarzają prace.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-244">Number of worker threads available to process work, including those that are already processing work.</span></span>|
|`RetiredWorkerThreadCount`|`win:UInt32`|<span data-ttu-id="4bc2e-245">Liczba wątków roboczych, które nie są dostępne do przetwarzania pracy, ale które są przechowywane w rezerwie w przypadku późniejszej liczby wątków.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-245">Number of worker threads that are not available to process work, but that are being held in reserve in case more threads are needed later.</span></span>|
|`ClrInstanceID`|`win:UInt16`|<span data-ttu-id="4bc2e-246">Unikatowy identyfikator wystąpienia CLR lub CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-246">Unique ID for the instance of CLR or CoreCLR.</span></span>|

## <a name="threadpoolworkerthreadretirementstop-event"></a><span data-ttu-id="4bc2e-247">Zdarzenie ThreadPoolWorkerThreadRetirementStop</span><span class="sxs-lookup"><span data-stu-id="4bc2e-247">ThreadPoolWorkerThreadRetirementStop event</span></span>

|<span data-ttu-id="4bc2e-248">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-248">Keyword for raising the event</span></span>|<span data-ttu-id="4bc2e-249">Poziom</span><span class="sxs-lookup"><span data-stu-id="4bc2e-249">Level</span></span>|
|-----------------------------------|-----------|-----------|
|<span data-ttu-id="4bc2e-250">`ThreadingKeyword` 0x10000</span><span class="sxs-lookup"><span data-stu-id="4bc2e-250">`ThreadingKeyword` (0x10000)</span></span>|<span data-ttu-id="4bc2e-251">Informacyjny (4)</span><span class="sxs-lookup"><span data-stu-id="4bc2e-251">Informational (4)</span></span>|

|<span data-ttu-id="4bc2e-252">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="4bc2e-252">Event</span></span>|<span data-ttu-id="4bc2e-253">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-253">Event ID</span></span>|<span data-ttu-id="4bc2e-254">Opis</span><span class="sxs-lookup"><span data-stu-id="4bc2e-254">Description</span></span>|
|-----------|--------------|-----------------|
|`ThreadPoolWorkerThreadRetirementStop`|<span data-ttu-id="4bc2e-255">53</span><span class="sxs-lookup"><span data-stu-id="4bc2e-255">53</span></span>|<span data-ttu-id="4bc2e-256">Wycofywany wątek roboczy zostanie ponownie uaktywniony.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-256">A retired worker thread becomes active again.</span></span>|

|<span data-ttu-id="4bc2e-257">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="4bc2e-257">Field name</span></span>|<span data-ttu-id="4bc2e-258">Typ danych</span><span class="sxs-lookup"><span data-stu-id="4bc2e-258">Data type</span></span>|<span data-ttu-id="4bc2e-259">Opis</span><span class="sxs-lookup"><span data-stu-id="4bc2e-259">Description</span></span>|
|----------------|---------------|-----------------|
|`ActiveWorkerThreadCount`|`win:UInt32`|<span data-ttu-id="4bc2e-260">Liczba wątków roboczych dostępnych do przetwarzania pracy, w tym tych, które już przetwarzają prace.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-260">Number of worker threads available to process work, including those that are already processing work.</span></span>|
|`RetiredWorkerThreadCount`|`win:UInt32`|<span data-ttu-id="4bc2e-261">Liczba wątków roboczych, które nie są dostępne do przetwarzania pracy, ale które są przechowywane w rezerwie w przypadku późniejszej liczby wątków.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-261">Number of worker threads that are not available to process work, but that are being held in reserve in case more threads are needed later.</span></span>|
|`ClrInstanceID`|`win:UInt16`|<span data-ttu-id="4bc2e-262">Unikatowy identyfikator wystąpienia CLR lub CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-262">Unique ID for the instance of CLR or CoreCLR.</span></span>|

## <a name="threadpoolworkerthreadadjustmentsample-event"></a><span data-ttu-id="4bc2e-263">Zdarzenie ThreadPoolWorkerThreadAdjustmentSample</span><span class="sxs-lookup"><span data-stu-id="4bc2e-263">ThreadPoolWorkerThreadAdjustmentSample event</span></span>

 <span data-ttu-id="4bc2e-264">W poniższej tabeli przedstawiono słowo kluczowe i poziom.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-264">The following table shows the keyword and level.</span></span>

|<span data-ttu-id="4bc2e-265">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-265">Keyword for raising the event</span></span>|<span data-ttu-id="4bc2e-266">Poziom</span><span class="sxs-lookup"><span data-stu-id="4bc2e-266">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="4bc2e-267">`ThreadingKeyword` 0x10000</span><span class="sxs-lookup"><span data-stu-id="4bc2e-267">`ThreadingKeyword` (0x10000)</span></span>|<span data-ttu-id="4bc2e-268">Informacyjny (4)</span><span class="sxs-lookup"><span data-stu-id="4bc2e-268">Informational (4)</span></span>|

 <span data-ttu-id="4bc2e-269">W poniższej tabeli przedstawiono informacje o zdarzeniu.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-269">The following table shows the event information.</span></span>

|<span data-ttu-id="4bc2e-270">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="4bc2e-270">Event</span></span>|<span data-ttu-id="4bc2e-271">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-271">Event ID</span></span>|<span data-ttu-id="4bc2e-272">Opis</span><span class="sxs-lookup"><span data-stu-id="4bc2e-272">Description</span></span>|
|-----------|--------------|-----------------|
|`ThreadPoolWorkerThreadAdjustmentSample`|<span data-ttu-id="4bc2e-273">54</span><span class="sxs-lookup"><span data-stu-id="4bc2e-273">54</span></span>|<span data-ttu-id="4bc2e-274">Odnosi się do kolekcji informacji dla jednej próbki; oznacza to, że pomiar przepływności z pewnym poziomem współbieżności w czasie.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-274">Refers to the collection of information for one sample; that is, a measurement of throughput with a certain concurrency level, in an instant of time.</span></span>|

 <span data-ttu-id="4bc2e-275">W poniższej tabeli przedstawiono dane zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-275">The following table shows the event data.</span></span>

|<span data-ttu-id="4bc2e-276">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="4bc2e-276">Field name</span></span>|<span data-ttu-id="4bc2e-277">Typ danych</span><span class="sxs-lookup"><span data-stu-id="4bc2e-277">Data type</span></span>|<span data-ttu-id="4bc2e-278">Opis</span><span class="sxs-lookup"><span data-stu-id="4bc2e-278">Description</span></span>|
|----------------|---------------|-----------------|
|`Throughput`|`win:Double`|<span data-ttu-id="4bc2e-279">Liczba zaawansowania na jednostkę czasu.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-279">Number of completions per unit of time.</span></span>|
|`ClrInstanceID`|`win:UInt16`|<span data-ttu-id="4bc2e-280">Unikatowy identyfikator wystąpienia CLR lub CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-280">Unique ID for the instance of CLR or CoreCLR.</span></span>|

## <a name="threadpoolworkerthreadadjustmentadjustment-event"></a><span data-ttu-id="4bc2e-281">Zdarzenie ThreadPoolWorkerThreadAdjustmentAdjustment</span><span class="sxs-lookup"><span data-stu-id="4bc2e-281">ThreadPoolWorkerThreadAdjustmentAdjustment event</span></span>

 <span data-ttu-id="4bc2e-282">W poniższej tabeli przedstawiono słowo kluczowe i poziom.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-282">The following table shows the keyword and level.</span></span>

|<span data-ttu-id="4bc2e-283">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-283">Keyword for raising the event</span></span>|<span data-ttu-id="4bc2e-284">Poziom</span><span class="sxs-lookup"><span data-stu-id="4bc2e-284">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="4bc2e-285">`ThreadingKeyword` 0x10000</span><span class="sxs-lookup"><span data-stu-id="4bc2e-285">`ThreadingKeyword` (0x10000)</span></span>|<span data-ttu-id="4bc2e-286">Informacyjny (4)</span><span class="sxs-lookup"><span data-stu-id="4bc2e-286">Informational (4)</span></span>|

 <span data-ttu-id="4bc2e-287">W poniższej tabeli przedstawiono informacje o zdarzeniu.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-287">The following table shows the event information.</span></span>

|<span data-ttu-id="4bc2e-288">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="4bc2e-288">Event</span></span>|<span data-ttu-id="4bc2e-289">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-289">Event ID</span></span>|<span data-ttu-id="4bc2e-290">Opis</span><span class="sxs-lookup"><span data-stu-id="4bc2e-290">Description</span></span>|
|-----------|--------------|-----------------|
|`ThreadPoolWorkerThreadAdjustmentAdjustment`|<span data-ttu-id="4bc2e-291">55</span><span class="sxs-lookup"><span data-stu-id="4bc2e-291">55</span></span>|<span data-ttu-id="4bc2e-292">Rejestruje zmianę w kontrolce, gdy algorytm iniekcji wątku (Hill-wspinanie się) określa, że zmiana na poziomie współbieżności jest na miejscu.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-292">Records a change in control, when the thread injection (hill-climbing) algorithm determines that a change in concurrency level is in place.</span></span>|

 <span data-ttu-id="4bc2e-293">W poniższej tabeli przedstawiono dane zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-293">The following table shows the event data.</span></span>

|<span data-ttu-id="4bc2e-294">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="4bc2e-294">Field name</span></span>|<span data-ttu-id="4bc2e-295">Typ danych</span><span class="sxs-lookup"><span data-stu-id="4bc2e-295">Data type</span></span>|<span data-ttu-id="4bc2e-296">Opis</span><span class="sxs-lookup"><span data-stu-id="4bc2e-296">Description</span></span>|
|----------------|---------------|-----------------|
|`AverageThroughput`|`win:Double`|<span data-ttu-id="4bc2e-297">Średnia przepływność próbki pomiarów.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-297">Average throughput of a sample of measurements.</span></span>|
|`NewWorkerThreadCount`|`win:UInt32`|<span data-ttu-id="4bc2e-298">Nowa liczba aktywnych wątków roboczych.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-298">New number of active worker threads.</span></span>|
|`Reason`|`win:UInt32`|<span data-ttu-id="4bc2e-299">Przyczyna korekty.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-299">Reason for the adjustment.</span></span><br /><br /> <span data-ttu-id="4bc2e-300">`0x0` Rozgrzewania.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-300">`0x0` - Warmup.</span></span><br /><br /> <span data-ttu-id="4bc2e-301">`0x1` Inicjacj.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-301">`0x1` - Initializing.</span></span><br /><br /> <span data-ttu-id="4bc2e-302">`0x2` -Losowe przechodzenie.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-302">`0x2` - Random move.</span></span><br /><br /> <span data-ttu-id="4bc2e-303">`0x3` -Wspinanie się Przenieś.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-303">`0x3` - Climbing move.</span></span><br /><br /> <span data-ttu-id="4bc2e-304">`0x4` — Zmień punkt.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-304">`0x4` - Change point.</span></span><br /><br /> <span data-ttu-id="4bc2e-305">`0x5` Utrwala.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-305">`0x5` - Stabilizing.</span></span><br /><br /> <span data-ttu-id="4bc2e-306">`0x6` Deficyt.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-306">`0x6` - Starvation.</span></span><br /><br /> <span data-ttu-id="4bc2e-307">`0x7` — Przekroczono limit czasu wątku.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-307">`0x7` - Thread timed out.</span></span>|
|`ClrInstanceID`|`win:UInt16`|<span data-ttu-id="4bc2e-308">Unikatowy identyfikator wystąpienia CLR lub CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-308">Unique ID for the instance of CLR or CoreCLR.</span></span>|

## <a name="threadpoolworkerthreadadjustmentstats-event"></a><span data-ttu-id="4bc2e-309">Zdarzenie ThreadPoolWorkerThreadAdjustmentStats</span><span class="sxs-lookup"><span data-stu-id="4bc2e-309">ThreadPoolWorkerThreadAdjustmentStats event</span></span>

 <span data-ttu-id="4bc2e-310">W poniższej tabeli przedstawiono słowo kluczowe i poziom.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-310">The following table shows the keyword and level.</span></span>

|<span data-ttu-id="4bc2e-311">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-311">Keyword for raising the event</span></span>|<span data-ttu-id="4bc2e-312">Poziom</span><span class="sxs-lookup"><span data-stu-id="4bc2e-312">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="4bc2e-313">`ThreadingKeyword` 0x10000</span><span class="sxs-lookup"><span data-stu-id="4bc2e-313">`ThreadingKeyword` (0x10000)</span></span>|<span data-ttu-id="4bc2e-314">Verbose (5)</span><span class="sxs-lookup"><span data-stu-id="4bc2e-314">Verbose (5)</span></span>

 <span data-ttu-id="4bc2e-315">W poniższej tabeli przedstawiono informacje o zdarzeniu.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-315">The following table shows the event information.</span></span>

|<span data-ttu-id="4bc2e-316">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="4bc2e-316">Event</span></span>|<span data-ttu-id="4bc2e-317">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-317">Event ID</span></span>|<span data-ttu-id="4bc2e-318">Opis</span><span class="sxs-lookup"><span data-stu-id="4bc2e-318">Description</span></span>|
|-----------|--------------|-----------------|
|`ThreadPoolWorkerThreadAdjustmentStats`|<span data-ttu-id="4bc2e-319">56</span><span class="sxs-lookup"><span data-stu-id="4bc2e-319">56</span></span>|<span data-ttu-id="4bc2e-320">Zbiera dane w puli wątków.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-320">Gathers data on the thread pool.</span></span>|

 <span data-ttu-id="4bc2e-321">W poniższej tabeli przedstawiono dane zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-321">The following table shows the event data</span></span>

|<span data-ttu-id="4bc2e-322">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="4bc2e-322">Field name</span></span>|<span data-ttu-id="4bc2e-323">Typ danych</span><span class="sxs-lookup"><span data-stu-id="4bc2e-323">Data type</span></span>|<span data-ttu-id="4bc2e-324">Opis</span><span class="sxs-lookup"><span data-stu-id="4bc2e-324">Description</span></span>|
|----------------|---------------|-----------------|
|`Duration`|`win:Double`|<span data-ttu-id="4bc2e-325">Czas (w sekundach), w którym te statystyki zostały zebrane.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-325">Amount of time, in seconds, during which these statistics were collected.</span></span>|
|`Throughput`|`win:Double`|<span data-ttu-id="4bc2e-326">Średnia liczba zaawansowanych na sekundę w tym interwale.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-326">Average number of completions per second during this interval.</span></span>|
|`ThreadWave`|`win:Double`|<span data-ttu-id="4bc2e-327">Zarezerwowane do użytku wewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-327">Reserved for internal use.</span></span>|
|`ThroughputWave`|`win:Double`|<span data-ttu-id="4bc2e-328">Zarezerwowane do użytku wewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-328">Reserved for internal use.</span></span>|
|`ThroughputErrorEstimate`|`win:Double`|<span data-ttu-id="4bc2e-329">Zarezerwowane do użytku wewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-329">Reserved for internal use.</span></span>|
|`AverageThroughputErrorEstimate`|`win:Double`|<span data-ttu-id="4bc2e-330">Zarezerwowane do użytku wewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-330">Reserved for internal use.</span></span>|
|`ThroughputRatio`|`win:Double`|<span data-ttu-id="4bc2e-331">Względne ulepszenie przepływności spowodowane przez różnice w liczbie wątków roboczych w tym interwale.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-331">The relative improvement in throughput caused by variations in active worker thread count during this interval.</span></span>|
|`Confidence`|`win:Double`|<span data-ttu-id="4bc2e-332">Miara ważności pola ThroughputRatio.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-332">A measure of the validity of the ThroughputRatio field.</span></span>|
|`NewcontrolSetting`|`win:Double`|<span data-ttu-id="4bc2e-333">Liczba aktywnych wątków roboczych, które będą stanowić podstawę dla przyszłych różnic w aktywnej liczbie wątków.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-333">The number of active worker threads that will serve as the baseline for future variations in active thread count.</span></span>|
|`NewThreadWaveMagnitude`|`win:UInt16`|<span data-ttu-id="4bc2e-334">Wielkość przyszłych wariantów w aktywnej liczbie wątków.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-334">The magnitude of future variations in active thread count.</span></span>|
|`ClrInstanceID`|`win:UInt16`|<span data-ttu-id="4bc2e-335">Unikatowy identyfikator wystąpienia CLR lub CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-335">Unique ID for the instance of CLR or CoreCLR.</span></span>|

## <a name="threadpoolenqueue-event"></a><span data-ttu-id="4bc2e-336">Zdarzenie ThreadPoolEnqueue</span><span class="sxs-lookup"><span data-stu-id="4bc2e-336">ThreadPoolEnqueue event</span></span>

 <span data-ttu-id="4bc2e-337">W poniższej tabeli przedstawiono słowo kluczowe i poziom.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-337">The following table shows the keyword and level.</span></span>

|<span data-ttu-id="4bc2e-338">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-338">Keyword for raising the event</span></span>|<span data-ttu-id="4bc2e-339">Poziom</span><span class="sxs-lookup"><span data-stu-id="4bc2e-339">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="4bc2e-340">`ThreadingKeyword` 0x10000</span><span class="sxs-lookup"><span data-stu-id="4bc2e-340">`ThreadingKeyword` (0x10000)</span></span>|<span data-ttu-id="4bc2e-341">Verbose (5)</span><span class="sxs-lookup"><span data-stu-id="4bc2e-341">Verbose (5)</span></span>

 <span data-ttu-id="4bc2e-342">W poniższej tabeli przedstawiono informacje o zdarzeniu.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-342">The following table shows the event information.</span></span>

|<span data-ttu-id="4bc2e-343">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="4bc2e-343">Event</span></span>|<span data-ttu-id="4bc2e-344">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-344">Event ID</span></span>|<span data-ttu-id="4bc2e-345">Opis</span><span class="sxs-lookup"><span data-stu-id="4bc2e-345">Description</span></span>|
|-----------|--------------|-----------------|
|`ThreadPoolEnqueue`|<span data-ttu-id="4bc2e-346">61</span><span class="sxs-lookup"><span data-stu-id="4bc2e-346">61</span></span>|<span data-ttu-id="4bc2e-347">Element roboczy został poddany do kolejki w kolejce puli wątków.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-347">A work item was enqueued in the thread pool queue.</span></span>|

 <span data-ttu-id="4bc2e-348">W poniższej tabeli przedstawiono dane zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-348">The following table shows the event data</span></span>

|<span data-ttu-id="4bc2e-349">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="4bc2e-349">Field name</span></span>|<span data-ttu-id="4bc2e-350">Typ danych</span><span class="sxs-lookup"><span data-stu-id="4bc2e-350">Data type</span></span>|<span data-ttu-id="4bc2e-351">Opis</span><span class="sxs-lookup"><span data-stu-id="4bc2e-351">Description</span></span>|
|----------------|---------------|-----------------|
|`WorkID`|`win:Pointer`|<span data-ttu-id="4bc2e-352">Wskaźnik na żądanie służbowe.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-352">Pointer to the work request.</span></span>|
|`ClrInstanceID`|`win:UInt16`|<span data-ttu-id="4bc2e-353">Unikatowy identyfikator wystąpienia elementu CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-353">Unique ID for the instance of CoreCLR.</span></span>|

## <a name="threadpooldequeue-event"></a><span data-ttu-id="4bc2e-354">Zdarzenie ThreadPoolDequeue</span><span class="sxs-lookup"><span data-stu-id="4bc2e-354">ThreadPoolDequeue event</span></span>

 <span data-ttu-id="4bc2e-355">W poniższej tabeli przedstawiono słowo kluczowe i poziom.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-355">The following table shows the keyword and level.</span></span>

|<span data-ttu-id="4bc2e-356">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-356">Keyword for raising the event</span></span>|<span data-ttu-id="4bc2e-357">Poziom</span><span class="sxs-lookup"><span data-stu-id="4bc2e-357">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="4bc2e-358">`ThreadingKeyword` 0x10000</span><span class="sxs-lookup"><span data-stu-id="4bc2e-358">`ThreadingKeyword` (0x10000)</span></span>|<span data-ttu-id="4bc2e-359">Verbose (5)</span><span class="sxs-lookup"><span data-stu-id="4bc2e-359">Verbose (5)</span></span>

 <span data-ttu-id="4bc2e-360">W poniższej tabeli przedstawiono informacje o zdarzeniu.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-360">The following table shows the event information.</span></span>

|<span data-ttu-id="4bc2e-361">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="4bc2e-361">Event</span></span>|<span data-ttu-id="4bc2e-362">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-362">Event ID</span></span>|<span data-ttu-id="4bc2e-363">Opis</span><span class="sxs-lookup"><span data-stu-id="4bc2e-363">Description</span></span>|
|-----------|--------------|-----------------|
|`ThreadPoolDequeue`|<span data-ttu-id="4bc2e-364">62</span><span class="sxs-lookup"><span data-stu-id="4bc2e-364">62</span></span>|<span data-ttu-id="4bc2e-365">Element roboczy został usunięty z kolejki puli wątków.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-365">A work item was dequeued from the thread pool queue.</span></span>|

 <span data-ttu-id="4bc2e-366">W poniższej tabeli przedstawiono dane zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-366">The following table shows the event data</span></span>

|<span data-ttu-id="4bc2e-367">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="4bc2e-367">Field name</span></span>|<span data-ttu-id="4bc2e-368">Typ danych</span><span class="sxs-lookup"><span data-stu-id="4bc2e-368">Data type</span></span>|<span data-ttu-id="4bc2e-369">Opis</span><span class="sxs-lookup"><span data-stu-id="4bc2e-369">Description</span></span>|
|----------------|---------------|-----------------|
|`WorkID`|`win:Pointer`|<span data-ttu-id="4bc2e-370">Wskaźnik na żądanie służbowe.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-370">Pointer to the work request.</span></span>|
|`ClrInstanceID`|`win:UInt16`|<span data-ttu-id="4bc2e-371">Unikatowy identyfikator wystąpienia elementu CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-371">Unique ID for the instance of CoreCLR.</span></span>|

## <a name="threadpoolioenqueue-event"></a><span data-ttu-id="4bc2e-372">Zdarzenie ThreadPoolIOEnqueue</span><span class="sxs-lookup"><span data-stu-id="4bc2e-372">ThreadPoolIOEnqueue event</span></span>

 <span data-ttu-id="4bc2e-373">W poniższej tabeli przedstawiono słowo kluczowe i poziom.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-373">The following table shows the keyword and level.</span></span>

|<span data-ttu-id="4bc2e-374">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-374">Keyword for raising the event</span></span>|<span data-ttu-id="4bc2e-375">Poziom</span><span class="sxs-lookup"><span data-stu-id="4bc2e-375">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="4bc2e-376">`ThreadingKeyword` 0x10000</span><span class="sxs-lookup"><span data-stu-id="4bc2e-376">`ThreadingKeyword` (0x10000)</span></span>|<span data-ttu-id="4bc2e-377">Verbose (5)</span><span class="sxs-lookup"><span data-stu-id="4bc2e-377">Verbose (5)</span></span>

 <span data-ttu-id="4bc2e-378">W poniższej tabeli przedstawiono informacje o zdarzeniu.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-378">The following table shows the event information.</span></span>

|<span data-ttu-id="4bc2e-379">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="4bc2e-379">Event</span></span>|<span data-ttu-id="4bc2e-380">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-380">Event ID</span></span>|<span data-ttu-id="4bc2e-381">Opis</span><span class="sxs-lookup"><span data-stu-id="4bc2e-381">Description</span></span>|
|-----------|--------------|-----------------|
|`ThreadPoolIOEnqueue`|<span data-ttu-id="4bc2e-382">63</span><span class="sxs-lookup"><span data-stu-id="4bc2e-382">63</span></span>|<span data-ttu-id="4bc2e-383">Wątek enqueues powiadomienie o ukończeniu operacji we/wy po wystąpieniu asynchronicznej operacji we/wy.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-383">A thread enqueues an IO completion notification after an async IO completion occurs.</span></span>|

 <span data-ttu-id="4bc2e-384">W poniższej tabeli przedstawiono dane zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-384">The following table shows the event data</span></span>

|<span data-ttu-id="4bc2e-385">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="4bc2e-385">Field name</span></span>|<span data-ttu-id="4bc2e-386">Typ danych</span><span class="sxs-lookup"><span data-stu-id="4bc2e-386">Data type</span></span>|<span data-ttu-id="4bc2e-387">Opis</span><span class="sxs-lookup"><span data-stu-id="4bc2e-387">Description</span></span>|
|----------------|---------------|-----------------|
|`NativeOverlapped`|`win:Pointer`|<span data-ttu-id="4bc2e-388">Zarezerwowane do użytku wewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-388">Reserved for internal use.</span></span>|
|`Overlapped`|`win:Pointer`|<span data-ttu-id="4bc2e-389">Zarezerwowane do użytku wewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-389">Reserved for internal use.</span></span>|
|`MultiDequeues`|`win:Boolean`|<span data-ttu-id="4bc2e-390">Zarezerwowane do użytku wewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-390">Reserved for internal use.</span></span>|
|`ClrInstanceID`|`win:UInt16`|<span data-ttu-id="4bc2e-391">Unikatowy identyfikator wystąpienia elementu CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-391">Unique ID for the instance of CoreCLR.</span></span>|

## <a name="threadpooliodequeue-event"></a><span data-ttu-id="4bc2e-392">Zdarzenie ThreadPoolIODequeue</span><span class="sxs-lookup"><span data-stu-id="4bc2e-392">ThreadPoolIODequeue event</span></span>

 <span data-ttu-id="4bc2e-393">W poniższej tabeli przedstawiono słowo kluczowe i poziom.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-393">The following table shows the keyword and level.</span></span>

|<span data-ttu-id="4bc2e-394">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-394">Keyword for raising the event</span></span>|<span data-ttu-id="4bc2e-395">Poziom</span><span class="sxs-lookup"><span data-stu-id="4bc2e-395">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="4bc2e-396">`ThreadingKeyword` 0x10000</span><span class="sxs-lookup"><span data-stu-id="4bc2e-396">`ThreadingKeyword` (0x10000)</span></span>|<span data-ttu-id="4bc2e-397">Verbose (5)</span><span class="sxs-lookup"><span data-stu-id="4bc2e-397">Verbose (5)</span></span>

 <span data-ttu-id="4bc2e-398">W poniższej tabeli przedstawiono informacje o zdarzeniu.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-398">The following table shows the event information.</span></span>

|<span data-ttu-id="4bc2e-399">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="4bc2e-399">Event</span></span>|<span data-ttu-id="4bc2e-400">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-400">Event ID</span></span>|<span data-ttu-id="4bc2e-401">Opis</span><span class="sxs-lookup"><span data-stu-id="4bc2e-401">Description</span></span>|
|-----------|--------------|-----------------|
|`ThreadPoolIODequeue`|<span data-ttu-id="4bc2e-402">64</span><span class="sxs-lookup"><span data-stu-id="4bc2e-402">64</span></span>|<span data-ttu-id="4bc2e-403">Wątek usuwa powiadomienie o ukończeniu operacji we/wy.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-403">A thread dequeues the IO completion notification.</span></span>|

 <span data-ttu-id="4bc2e-404">W poniższej tabeli przedstawiono dane zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-404">The following table shows the event data</span></span>

|<span data-ttu-id="4bc2e-405">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="4bc2e-405">Field name</span></span>|<span data-ttu-id="4bc2e-406">Typ danych</span><span class="sxs-lookup"><span data-stu-id="4bc2e-406">Data type</span></span>|<span data-ttu-id="4bc2e-407">Opis</span><span class="sxs-lookup"><span data-stu-id="4bc2e-407">Description</span></span>|
|----------------|---------------|-----------------|
|`NativeOverlapped`|`win:Pointer`|<span data-ttu-id="4bc2e-408">Zarezerwowane do użytku wewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-408">Reserved for internal use.</span></span>|
|`Overlapped`|`win:Pointer`|<span data-ttu-id="4bc2e-409">Zarezerwowane do użytku wewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-409">Reserved for internal use.</span></span>|
|`MultiDequeues`|`win:Boolean`|<span data-ttu-id="4bc2e-410">Zarezerwowane do użytku wewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-410">Reserved for internal use.</span></span>|
|`ClrInstanceID`|`win:UInt16`|<span data-ttu-id="4bc2e-411">Unikatowy identyfikator wystąpienia elementu CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-411">Unique ID for the instance of CoreCLR.</span></span>|

## <a name="threadpooliopack-event"></a><span data-ttu-id="4bc2e-412">Zdarzenie ThreadPoolIOPack</span><span class="sxs-lookup"><span data-stu-id="4bc2e-412">ThreadPoolIOPack event</span></span>

 <span data-ttu-id="4bc2e-413">W poniższej tabeli przedstawiono słowo kluczowe i poziom.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-413">The following table shows the keyword and level.</span></span>

|<span data-ttu-id="4bc2e-414">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-414">Keyword for raising the event</span></span>|<span data-ttu-id="4bc2e-415">Poziom</span><span class="sxs-lookup"><span data-stu-id="4bc2e-415">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="4bc2e-416">`ThreadingKeyword` 0x10000</span><span class="sxs-lookup"><span data-stu-id="4bc2e-416">`ThreadingKeyword` (0x10000)</span></span>|<span data-ttu-id="4bc2e-417">Verbose (5)</span><span class="sxs-lookup"><span data-stu-id="4bc2e-417">Verbose (5)</span></span>|

 <span data-ttu-id="4bc2e-418">W poniższej tabeli przedstawiono informacje o zdarzeniu.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-418">The following table shows the event information.</span></span>

|<span data-ttu-id="4bc2e-419">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="4bc2e-419">Event</span></span>|<span data-ttu-id="4bc2e-420">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-420">Event ID</span></span>|<span data-ttu-id="4bc2e-421">Opis</span><span class="sxs-lookup"><span data-stu-id="4bc2e-421">Description</span></span>|
|-----------|--------------|-----------------|
|`ThreadPoolIOPack`|<span data-ttu-id="4bc2e-422">65</span><span class="sxs-lookup"><span data-stu-id="4bc2e-422">65</span></span>|<span data-ttu-id="4bc2e-423">Jest wywoływany pakiet operacji we/wy nakładający się na siebie.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-423">ThreadPool overlapped IO pack is called.</span></span>|

 <span data-ttu-id="4bc2e-424">W poniższej tabeli przedstawiono dane zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-424">The following table shows the event data</span></span>

|<span data-ttu-id="4bc2e-425">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="4bc2e-425">Field name</span></span>|<span data-ttu-id="4bc2e-426">Typ danych</span><span class="sxs-lookup"><span data-stu-id="4bc2e-426">Data type</span></span>|<span data-ttu-id="4bc2e-427">Opis</span><span class="sxs-lookup"><span data-stu-id="4bc2e-427">Description</span></span>|
|----------------|---------------|-----------------|
|`NativeOverlapped`|`win:Pointer`|<span data-ttu-id="4bc2e-428">Zarezerwowane do użytku wewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-428">Reserved for internal use.</span></span>|
|`Overlapped`|`win:Pointer`|<span data-ttu-id="4bc2e-429">Zarezerwowane do użytku wewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-429">Reserved for internal use.</span></span>|
|`ClrInstanceID`|`win:UInt16`|<span data-ttu-id="4bc2e-430">Unikatowy identyfikator wystąpienia elementu CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-430">Unique ID for the instance of CoreCLR.</span></span>|

## <a name="threadcreating-event"></a><span data-ttu-id="4bc2e-431">Zdarzenie ThreadCreating</span><span class="sxs-lookup"><span data-stu-id="4bc2e-431">ThreadCreating event</span></span>

 <span data-ttu-id="4bc2e-432">W poniższej tabeli przedstawiono słowa kluczowe i poziom.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-432">The following table shows the keywords and level.</span></span>

|<span data-ttu-id="4bc2e-433">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-433">Keyword for raising the event</span></span>|<span data-ttu-id="4bc2e-434">Poziom</span><span class="sxs-lookup"><span data-stu-id="4bc2e-434">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="4bc2e-435">`ThreadingKeyword` 0x10000</span><span class="sxs-lookup"><span data-stu-id="4bc2e-435">`ThreadingKeyword` (0x10000)</span></span>|<span data-ttu-id="4bc2e-436">Informacyjny (4)</span><span class="sxs-lookup"><span data-stu-id="4bc2e-436">Informational (4)</span></span>|

 <span data-ttu-id="4bc2e-437">W poniższej tabeli przedstawiono informacje o zdarzeniu.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-437">The following table shows the event information.</span></span>

|<span data-ttu-id="4bc2e-438">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="4bc2e-438">Event</span></span>|<span data-ttu-id="4bc2e-439">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-439">Event ID</span></span>|<span data-ttu-id="4bc2e-440">Opis</span><span class="sxs-lookup"><span data-stu-id="4bc2e-440">Description</span></span>|
|----------------|---------------|-----------------|
|`ThreadCreating`|<span data-ttu-id="4bc2e-441">70</span><span class="sxs-lookup"><span data-stu-id="4bc2e-441">70</span></span>|<span data-ttu-id="4bc2e-442">Utworzono wątek.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-442">Thread has been created.</span></span>|

 <span data-ttu-id="4bc2e-443">W poniższej tabeli przedstawiono dane zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-443">The following table shows the event data.</span></span>

|<span data-ttu-id="4bc2e-444">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="4bc2e-444">Field name</span></span>|<span data-ttu-id="4bc2e-445">Typ danych</span><span class="sxs-lookup"><span data-stu-id="4bc2e-445">Data type</span></span>|<span data-ttu-id="4bc2e-446">Opis</span><span class="sxs-lookup"><span data-stu-id="4bc2e-446">Description</span></span>|
|----------------|---------------|-----------------|
|`ID`|`win:Pointer`|<span data-ttu-id="4bc2e-447">Identyfikator wątku</span><span class="sxs-lookup"><span data-stu-id="4bc2e-447">Thread ID</span></span>|
|`ClrInstanceID`|`win:UInt16`|<span data-ttu-id="4bc2e-448">Unikatowy identyfikator wystąpienia elementu CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-448">Unique ID for the instance of CoreCLR.</span></span>|

## <a name="threadrunning-event"></a><span data-ttu-id="4bc2e-449">Zdarzenie ThreadRunning</span><span class="sxs-lookup"><span data-stu-id="4bc2e-449">ThreadRunning event</span></span>

 <span data-ttu-id="4bc2e-450">W poniższej tabeli przedstawiono słowa kluczowe i poziom.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-450">The following table shows the keywords and level.</span></span>

|<span data-ttu-id="4bc2e-451">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-451">Keyword for raising the event</span></span>|<span data-ttu-id="4bc2e-452">Poziom</span><span class="sxs-lookup"><span data-stu-id="4bc2e-452">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="4bc2e-453">`ThreadingKeyword` 0x10000</span><span class="sxs-lookup"><span data-stu-id="4bc2e-453">`ThreadingKeyword` (0x10000)</span></span>|<span data-ttu-id="4bc2e-454">Informacyjny (4)</span><span class="sxs-lookup"><span data-stu-id="4bc2e-454">Informational (4)</span></span>|

 <span data-ttu-id="4bc2e-455">W poniższej tabeli przedstawiono informacje o zdarzeniu.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-455">The following table shows the event information.</span></span>

|<span data-ttu-id="4bc2e-456">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="4bc2e-456">Event</span></span>|<span data-ttu-id="4bc2e-457">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4bc2e-457">Event ID</span></span>|<span data-ttu-id="4bc2e-458">Opis</span><span class="sxs-lookup"><span data-stu-id="4bc2e-458">Description</span></span>|
|----------------|---------------|-----------------|
|`ThreadRunning`|<span data-ttu-id="4bc2e-459">71</span><span class="sxs-lookup"><span data-stu-id="4bc2e-459">71</span></span>|<span data-ttu-id="4bc2e-460">Wątek został uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-460">Thread has started running.</span></span>|

 <span data-ttu-id="4bc2e-461">W poniższej tabeli przedstawiono dane zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-461">The following table shows the event data.</span></span>

|<span data-ttu-id="4bc2e-462">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="4bc2e-462">Field name</span></span>|<span data-ttu-id="4bc2e-463">Typ danych</span><span class="sxs-lookup"><span data-stu-id="4bc2e-463">Data type</span></span>|<span data-ttu-id="4bc2e-464">Opis</span><span class="sxs-lookup"><span data-stu-id="4bc2e-464">Description</span></span>|
|----------------|---------------|-----------------|
|`ID`|`win:Pointer`|<span data-ttu-id="4bc2e-465">Identyfikator wątku</span><span class="sxs-lookup"><span data-stu-id="4bc2e-465">Thread ID</span></span>|
|`ClrInstanceID`|`win:UInt16`|<span data-ttu-id="4bc2e-466">Unikatowy identyfikator wystąpienia elementu CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="4bc2e-466">Unique ID for the instance of CoreCLR.</span></span>|
