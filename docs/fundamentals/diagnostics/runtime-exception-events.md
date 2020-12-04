---
title: Zdarzenia środowiska uruchomieniowego wyjątku
description: Zobacz zdarzenia środowiska uruchomieniowego platformy .NET, które zbierają informacje diagnostyczne specyficzne dla wyjątków i obsługi wyjątków.
ms.date: 11/13/2020
ms.topic: reference
helpviewer_keywords:
- exception events (CoreCLR)
- exception handling events (CoreCLR)
- ETW, EventPipe, LTTng exception events (CoreCLR)
ms.openlocfilehash: f4f63c8469f9c734b872ddaec8d1d7f7f0427576
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96590032"
---
# <a name="net-runtime-exception-events"></a><span data-ttu-id="2942a-103">Zdarzenia wyjątków środowiska uruchomieniowego .NET</span><span class="sxs-lookup"><span data-stu-id="2942a-103">.NET runtime exception events</span></span>

<span data-ttu-id="2942a-104">Te zdarzenia środowiska uruchomieniowego przechwytują informacje o zgłaszanych wyjątkach.</span><span class="sxs-lookup"><span data-stu-id="2942a-104">These runtime events capture information about exceptions that are thrown.</span></span> <span data-ttu-id="2942a-105">Aby uzyskać więcej informacji na temat korzystania z tych zdarzeń w celach diagnostycznych, zobacz [Rejestrowanie i śledzenie aplikacji .NET](../../core/diagnostics/logging-tracing.md) .</span><span class="sxs-lookup"><span data-stu-id="2942a-105">For more information about how to use these events for diagnostic purposes, see [logging and tracing .NET applications](../../core/diagnostics/logging-tracing.md)</span></span>

## <a name="exceptionthrown_v1-event"></a><span data-ttu-id="2942a-106">Zdarzenie ExceptionThrown_V1</span><span class="sxs-lookup"><span data-stu-id="2942a-106">ExceptionThrown_V1 event</span></span>

|<span data-ttu-id="2942a-107">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="2942a-107">Keyword for raising the event</span></span>|<span data-ttu-id="2942a-108">Poziom</span><span class="sxs-lookup"><span data-stu-id="2942a-108">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="2942a-109">`ExceptionKeyword` 0x8000</span><span class="sxs-lookup"><span data-stu-id="2942a-109">`ExceptionKeyword` (0x8000)</span></span>|<span data-ttu-id="2942a-110">Błąd (1)</span><span class="sxs-lookup"><span data-stu-id="2942a-110">Error (1)</span></span>|

 <span data-ttu-id="2942a-111">W poniższej tabeli przedstawiono informacje o zdarzeniach.</span><span class="sxs-lookup"><span data-stu-id="2942a-111">The following table shows event information.</span></span>

|<span data-ttu-id="2942a-112">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="2942a-112">Event</span></span>|<span data-ttu-id="2942a-113">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="2942a-113">Event ID</span></span>|<span data-ttu-id="2942a-114">Wywoływane, gdy</span><span class="sxs-lookup"><span data-stu-id="2942a-114">Raised when</span></span>|
|-----------|--------------|-----------------|
|`ExceptionThrown_V1`|<span data-ttu-id="2942a-115">80</span><span class="sxs-lookup"><span data-stu-id="2942a-115">80</span></span>|<span data-ttu-id="2942a-116">Generowany jest wyjątek zarządzany.</span><span class="sxs-lookup"><span data-stu-id="2942a-116">A managed exception is thrown.</span></span>|

|<span data-ttu-id="2942a-117">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="2942a-117">Field name</span></span>|<span data-ttu-id="2942a-118">Typ danych</span><span class="sxs-lookup"><span data-stu-id="2942a-118">Data type</span></span>|<span data-ttu-id="2942a-119">Opis</span><span class="sxs-lookup"><span data-stu-id="2942a-119">Description</span></span>|
|----------------|---------------|-----------------|
|`ExceptionType`|`win:UnicodeString`|<span data-ttu-id="2942a-120">Typ wyjątku; na przykład `System.NullReferenceException` .</span><span class="sxs-lookup"><span data-stu-id="2942a-120">Type of the exception; for example, `System.NullReferenceException`.</span></span>|
|`ExceptionMessage`|`win:UnicodeString`|<span data-ttu-id="2942a-121">Rzeczywisty komunikat o wyjątku.</span><span class="sxs-lookup"><span data-stu-id="2942a-121">Actual exception message.</span></span>|
|`EIPCodeThrow`|`win:Pointer`|<span data-ttu-id="2942a-122">Wskaźnik instrukcji, w którym wystąpił wyjątek.</span><span class="sxs-lookup"><span data-stu-id="2942a-122">Instruction pointer where exception occurred.</span></span>|
|`ExceptionHR`|`win:UInt32`|<span data-ttu-id="2942a-123">Wyjątek [HRESULT](/openspecs/windows_protocols/ms-erref/0642cb2f-2075-4469-918c-4441e69c548a).</span><span class="sxs-lookup"><span data-stu-id="2942a-123">Exception [HRESULT](/openspecs/windows_protocols/ms-erref/0642cb2f-2075-4469-918c-4441e69c548a).</span></span>|
|`ExceptionFlags`|`win:UInt16`|<span data-ttu-id="2942a-124">`0x01`: HasInnerException.</span><span class="sxs-lookup"><span data-stu-id="2942a-124">`0x01`: HasInnerException.</span></span><br /><br /> <span data-ttu-id="2942a-125">`0x02`: Isnestexception.</span><span class="sxs-lookup"><span data-stu-id="2942a-125">`0x02`: IsNestedException.</span></span><br /><br /> <span data-ttu-id="2942a-126">`0x04`: IsRethrownException.</span><span class="sxs-lookup"><span data-stu-id="2942a-126">`0x04`: IsRethrownException.</span></span><br /><br /> <span data-ttu-id="2942a-127">`0x08`: IsCorruptedStateException (wskazuje, że stan procesu jest uszkodzony; zobacz [Obsługa wyjątków uszkodzonego stanu](/archive/msdn-magazine/2009/february/clr-inside-out-handling-corrupted-state-exceptions)).</span><span class="sxs-lookup"><span data-stu-id="2942a-127">`0x08`: IsCorruptedStateException (indicates that the process state is corrupt; see [Handling Corrupted State Exceptions](/archive/msdn-magazine/2009/february/clr-inside-out-handling-corrupted-state-exceptions)).</span></span><br /><br /> <span data-ttu-id="2942a-128">`0x10`: IsCLSCompliant (wyjątek pochodzący z <xref:System.Exception> jest zgodny ze specyfikacją CLS; w przeciwnym razie nie jest zgodny ze specyfikacją CLS).</span><span class="sxs-lookup"><span data-stu-id="2942a-128">`0x10`: IsCLSCompliant (an exception that derives from <xref:System.Exception> is CLS-compliant; otherwise, it is not CLS-compliant).</span></span>|
|`ClrInstanceID`|`win:UInt16`|<span data-ttu-id="2942a-129">Unikatowy identyfikator wystąpienia CLR lub CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="2942a-129">Unique ID for the instance of CLR or CoreCLR.</span></span>|

## <a name="exceptioncatchstart-event"></a><span data-ttu-id="2942a-130">Zdarzenie ExceptionCatchStart</span><span class="sxs-lookup"><span data-stu-id="2942a-130">ExceptionCatchStart event</span></span>

<span data-ttu-id="2942a-131">To zdarzenie jest emitowane po rozpoczęciu procedury obsługi catch o wyjątku zarządzanym.</span><span class="sxs-lookup"><span data-stu-id="2942a-131">This event is emitted when a managed exception catch handler begins.</span></span>

|<span data-ttu-id="2942a-132">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="2942a-132">Keyword for raising the event</span></span>|<span data-ttu-id="2942a-133">Poziom</span><span class="sxs-lookup"><span data-stu-id="2942a-133">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="2942a-134">`ExceptionKeyword` 0x8000</span><span class="sxs-lookup"><span data-stu-id="2942a-134">`ExceptionKeyword` (0x8000)</span></span>|<span data-ttu-id="2942a-135">Informacyjny (4)</span><span class="sxs-lookup"><span data-stu-id="2942a-135">Informational (4)</span></span>|

 <span data-ttu-id="2942a-136">W poniższej tabeli przedstawiono informacje o zdarzeniach.</span><span class="sxs-lookup"><span data-stu-id="2942a-136">The following table shows event information.</span></span>

|<span data-ttu-id="2942a-137">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="2942a-137">Event</span></span>|<span data-ttu-id="2942a-138">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="2942a-138">Event ID</span></span>|<span data-ttu-id="2942a-139">Wywoływane, gdy</span><span class="sxs-lookup"><span data-stu-id="2942a-139">Raised when</span></span>|
|-----------|--------------|-----------------|
|`ExceptionCatchStart`|<span data-ttu-id="2942a-140">250</span><span class="sxs-lookup"><span data-stu-id="2942a-140">250</span></span>|<span data-ttu-id="2942a-141">Wyjątek zarządzany jest obsługiwany przez środowisko uruchomieniowe.</span><span class="sxs-lookup"><span data-stu-id="2942a-141">A managed exception is handled by the runtime.</span></span>|

|<span data-ttu-id="2942a-142">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="2942a-142">Field name</span></span>|<span data-ttu-id="2942a-143">Typ danych</span><span class="sxs-lookup"><span data-stu-id="2942a-143">Data type</span></span>|<span data-ttu-id="2942a-144">Opis</span><span class="sxs-lookup"><span data-stu-id="2942a-144">Description</span></span>|
|----------------|---------------|-----------------|
|`EIPCodeThrow`|`win:Pointer`|<span data-ttu-id="2942a-145">Wskaźnik instrukcji, w którym wystąpił wyjątek.</span><span class="sxs-lookup"><span data-stu-id="2942a-145">Instruction pointer where exception occurred.</span></span>|
|`MethodID`|`win:Pointer`|<span data-ttu-id="2942a-146">Wskaźnik do deskryptora metody na metodzie, w której wystąpił wyjątek.</span><span class="sxs-lookup"><span data-stu-id="2942a-146">Pointer to the method descriptor on the method where exception occurred.</span></span>|
|`MethodName`|`win:UnicodeString`|<span data-ttu-id="2942a-147">Nazwa metody, w której wystąpił wyjątek.</span><span class="sxs-lookup"><span data-stu-id="2942a-147">Name of the method where exception occurred.</span></span>|
|`ClrInstanceID`|`win:UInt16`|<span data-ttu-id="2942a-148">Unikatowy identyfikator wystąpienia CLR lub CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="2942a-148">Unique ID for the instance of CLR or CoreCLR.</span></span>|

## <a name="exceptioncatchstop-event"></a><span data-ttu-id="2942a-149">Zdarzenie ExceptionCatchStop</span><span class="sxs-lookup"><span data-stu-id="2942a-149">ExceptionCatchStop event</span></span>

<span data-ttu-id="2942a-150">To zdarzenie jest emitowane po zakończeniu obsługi catch o wyjątku zarządzanym.</span><span class="sxs-lookup"><span data-stu-id="2942a-150">This event is emitted when a managed exception catch handler ends.</span></span>

|<span data-ttu-id="2942a-151">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="2942a-151">Keyword for raising the event</span></span>|<span data-ttu-id="2942a-152">Poziom</span><span class="sxs-lookup"><span data-stu-id="2942a-152">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="2942a-153">`ExceptionKeyword` 0x8000</span><span class="sxs-lookup"><span data-stu-id="2942a-153">`ExceptionKeyword` (0x8000)</span></span>|<span data-ttu-id="2942a-154">Informacyjny (4)</span><span class="sxs-lookup"><span data-stu-id="2942a-154">Informational (4)</span></span>|

 <span data-ttu-id="2942a-155">W poniższej tabeli przedstawiono informacje o zdarzeniach.</span><span class="sxs-lookup"><span data-stu-id="2942a-155">The following table shows event information.</span></span>

|<span data-ttu-id="2942a-156">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="2942a-156">Event</span></span>|<span data-ttu-id="2942a-157">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="2942a-157">Event ID</span></span>|<span data-ttu-id="2942a-158">Wywoływane, gdy</span><span class="sxs-lookup"><span data-stu-id="2942a-158">Raised when</span></span>|
|-----------|--------------|-----------------|
|`ExceptionCatchStop`|<span data-ttu-id="2942a-159">251</span><span class="sxs-lookup"><span data-stu-id="2942a-159">251</span></span>|<span data-ttu-id="2942a-160">Wykonano procedurę obsługi catch o wyjątku zarządzanym.</span><span class="sxs-lookup"><span data-stu-id="2942a-160">A managed exception catch handler is done.</span></span>|

## <a name="exceptionfinallystart-event"></a><span data-ttu-id="2942a-161">Zdarzenie ExceptionFinallyStart</span><span class="sxs-lookup"><span data-stu-id="2942a-161">ExceptionFinallyStart event</span></span>

<span data-ttu-id="2942a-162">To zdarzenie jest emitowane po rozpoczęciu obsługi wyjątku zarządzanego finally.</span><span class="sxs-lookup"><span data-stu-id="2942a-162">This event is emitted when a managed exception finally handler begins.</span></span>

|<span data-ttu-id="2942a-163">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="2942a-163">Keyword for raising the event</span></span>|<span data-ttu-id="2942a-164">Poziom</span><span class="sxs-lookup"><span data-stu-id="2942a-164">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="2942a-165">`ExceptionKeyword` 0x8000</span><span class="sxs-lookup"><span data-stu-id="2942a-165">`ExceptionKeyword` (0x8000)</span></span>|<span data-ttu-id="2942a-166">Informacyjny (4)</span><span class="sxs-lookup"><span data-stu-id="2942a-166">Informational (4)</span></span>|

 <span data-ttu-id="2942a-167">W poniższej tabeli przedstawiono informacje o zdarzeniach.</span><span class="sxs-lookup"><span data-stu-id="2942a-167">The following table shows event information.</span></span>

|<span data-ttu-id="2942a-168">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="2942a-168">Event</span></span>|<span data-ttu-id="2942a-169">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="2942a-169">Event ID</span></span>|<span data-ttu-id="2942a-170">Wywoływane, gdy</span><span class="sxs-lookup"><span data-stu-id="2942a-170">Raised when</span></span>|
|-----------|--------------|-----------------|
|`ExceptionFinallyStart`|<span data-ttu-id="2942a-171">252</span><span class="sxs-lookup"><span data-stu-id="2942a-171">252</span></span>|<span data-ttu-id="2942a-172">Wyjątek zarządzany jest obsługiwany przez środowisko uruchomieniowe.</span><span class="sxs-lookup"><span data-stu-id="2942a-172">A managed exception is handled by the runtime.</span></span>|

|<span data-ttu-id="2942a-173">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="2942a-173">Field name</span></span>|<span data-ttu-id="2942a-174">Typ danych</span><span class="sxs-lookup"><span data-stu-id="2942a-174">Data type</span></span>|<span data-ttu-id="2942a-175">Opis</span><span class="sxs-lookup"><span data-stu-id="2942a-175">Description</span></span>|
|----------------|---------------|-----------------|
|`EIPCodeThrow`|`win:Pointer`|<span data-ttu-id="2942a-176">Wskaźnik instrukcji, w którym wystąpił wyjątek.</span><span class="sxs-lookup"><span data-stu-id="2942a-176">Instruction pointer where exception occurred.</span></span>|
|`MethodID`|`win:Pointer`|<span data-ttu-id="2942a-177">Wskaźnik do deskryptora metody na metodzie, w której wystąpił wyjątek.</span><span class="sxs-lookup"><span data-stu-id="2942a-177">Pointer to the method descriptor on the method where exception occurred.</span></span>|
|`MethodName`|`win:UnicodeString`|<span data-ttu-id="2942a-178">Nazwa metody, w której wystąpił wyjątek.</span><span class="sxs-lookup"><span data-stu-id="2942a-178">Name of the method where exception occurred.</span></span>|
|`ClrInstanceID`|`win:UInt16`|<span data-ttu-id="2942a-179">Unikatowy identyfikator wystąpienia CLR lub CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="2942a-179">Unique ID for the instance of CLR or CoreCLR.</span></span>|

## <a name="exceptionfinallystop-event"></a><span data-ttu-id="2942a-180">Zdarzenie ExceptionFinallyStop</span><span class="sxs-lookup"><span data-stu-id="2942a-180">ExceptionFinallyStop event</span></span>

<span data-ttu-id="2942a-181">To zdarzenie jest emitowane po zakończeniu obsługi catch o wyjątku zarządzanym.</span><span class="sxs-lookup"><span data-stu-id="2942a-181">This event is emitted when a managed exception catch handler ends.</span></span>

|<span data-ttu-id="2942a-182">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="2942a-182">Keyword for raising the event</span></span>|<span data-ttu-id="2942a-183">Poziom</span><span class="sxs-lookup"><span data-stu-id="2942a-183">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="2942a-184">`ExceptionKeyword` 0x8000</span><span class="sxs-lookup"><span data-stu-id="2942a-184">`ExceptionKeyword` (0x8000)</span></span>|<span data-ttu-id="2942a-185">Informacyjny (4)</span><span class="sxs-lookup"><span data-stu-id="2942a-185">Informational (4)</span></span>|

 <span data-ttu-id="2942a-186">W poniższej tabeli przedstawiono informacje o zdarzeniach.</span><span class="sxs-lookup"><span data-stu-id="2942a-186">The following table shows event information.</span></span>

|<span data-ttu-id="2942a-187">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="2942a-187">Event</span></span>|<span data-ttu-id="2942a-188">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="2942a-188">Event ID</span></span>|<span data-ttu-id="2942a-189">Wywoływane, gdy</span><span class="sxs-lookup"><span data-stu-id="2942a-189">Raised when</span></span>|
|-----------|--------------|-----------------|
|`ExceptionFinallyStop`|<span data-ttu-id="2942a-190">253</span><span class="sxs-lookup"><span data-stu-id="2942a-190">253</span></span>|<span data-ttu-id="2942a-191">Zakończono procedurę obsługi finally wyjątku zarządzanego.</span><span class="sxs-lookup"><span data-stu-id="2942a-191">A managed exception finally handler is done.</span></span>|

## <a name="exceptionfilterstart-event"></a><span data-ttu-id="2942a-192">Zdarzenie ExceptionFilterStart</span><span class="sxs-lookup"><span data-stu-id="2942a-192">ExceptionFilterStart event</span></span>

<span data-ttu-id="2942a-193">To zdarzenie jest emitowane po rozpoczęciu filtrowania zarządzanego wyjątku.</span><span class="sxs-lookup"><span data-stu-id="2942a-193">This event is emitted when a managed exception filtering begins.</span></span>

|<span data-ttu-id="2942a-194">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="2942a-194">Keyword for raising the event</span></span>|<span data-ttu-id="2942a-195">Poziom</span><span class="sxs-lookup"><span data-stu-id="2942a-195">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="2942a-196">`ExceptionKeyword` 0x8000</span><span class="sxs-lookup"><span data-stu-id="2942a-196">`ExceptionKeyword` (0x8000)</span></span>|<span data-ttu-id="2942a-197">Informacyjny (4)</span><span class="sxs-lookup"><span data-stu-id="2942a-197">Informational (4)</span></span>|

 <span data-ttu-id="2942a-198">W poniższej tabeli przedstawiono informacje o zdarzeniach.</span><span class="sxs-lookup"><span data-stu-id="2942a-198">The following table shows event information.</span></span>

|<span data-ttu-id="2942a-199">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="2942a-199">Event</span></span>|<span data-ttu-id="2942a-200">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="2942a-200">Event ID</span></span>|<span data-ttu-id="2942a-201">Wywoływane, gdy</span><span class="sxs-lookup"><span data-stu-id="2942a-201">Raised when</span></span>|
|-----------|--------------|-----------------|
|`ExceptionFilterStart`|<span data-ttu-id="2942a-202">254</span><span class="sxs-lookup"><span data-stu-id="2942a-202">254</span></span>|<span data-ttu-id="2942a-203">Rozpocznie się filtrowanie zarządzanych wyjątków.</span><span class="sxs-lookup"><span data-stu-id="2942a-203">A managed exception filtering begins.</span></span>|

|<span data-ttu-id="2942a-204">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="2942a-204">Field name</span></span>|<span data-ttu-id="2942a-205">Typ danych</span><span class="sxs-lookup"><span data-stu-id="2942a-205">Data type</span></span>|<span data-ttu-id="2942a-206">Opis</span><span class="sxs-lookup"><span data-stu-id="2942a-206">Description</span></span>|
|----------------|---------------|-----------------|
|`EIPCodeThrow`|`win:Pointer`|<span data-ttu-id="2942a-207">Wskaźnik instrukcji, w którym wystąpił wyjątek.</span><span class="sxs-lookup"><span data-stu-id="2942a-207">Instruction pointer where exception occurred.</span></span>|
|`MethodID`|`win:Pointer`|<span data-ttu-id="2942a-208">Wskaźnik do deskryptora metody na metodzie, w której wystąpił wyjątek.</span><span class="sxs-lookup"><span data-stu-id="2942a-208">Pointer to the method descriptor on the method where exception occurred.</span></span>|
|`MethodName`|`win:UnicodeString`|<span data-ttu-id="2942a-209">Nazwa metody, w której wystąpił wyjątek.</span><span class="sxs-lookup"><span data-stu-id="2942a-209">Name of the method where exception occurred.</span></span>|
|`ClrInstanceID`|`win:UInt16`|<span data-ttu-id="2942a-210">Unikatowy identyfikator wystąpienia elementu CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="2942a-210">Unique ID for the instance of CoreCLR.</span></span>|

## <a name="exceptionfilterstop-event"></a><span data-ttu-id="2942a-211">Zdarzenie ExceptionFilterStop</span><span class="sxs-lookup"><span data-stu-id="2942a-211">ExceptionFilterStop event</span></span>

<span data-ttu-id="2942a-212">To zdarzenie jest emitowane po zakończeniu filtrowania zarządzanego wyjątku.</span><span class="sxs-lookup"><span data-stu-id="2942a-212">This event is emitted when a managed exception filtering ends.</span></span>

|<span data-ttu-id="2942a-213">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="2942a-213">Keyword for raising the event</span></span>|<span data-ttu-id="2942a-214">Poziom</span><span class="sxs-lookup"><span data-stu-id="2942a-214">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="2942a-215">`ExceptionKeyword` 0x8000</span><span class="sxs-lookup"><span data-stu-id="2942a-215">`ExceptionKeyword` (0x8000)</span></span>|<span data-ttu-id="2942a-216">Informacyjny (4)</span><span class="sxs-lookup"><span data-stu-id="2942a-216">Informational (4)</span></span>|

 <span data-ttu-id="2942a-217">W poniższej tabeli przedstawiono informacje o zdarzeniach.</span><span class="sxs-lookup"><span data-stu-id="2942a-217">The following table shows event information.</span></span>

|<span data-ttu-id="2942a-218">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="2942a-218">Event</span></span>|<span data-ttu-id="2942a-219">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="2942a-219">Event ID</span></span>|<span data-ttu-id="2942a-220">Wywoływane, gdy</span><span class="sxs-lookup"><span data-stu-id="2942a-220">Raised when</span></span>|
|-----------|--------------|-----------------|
|`ExceptionFilteringStart`|<span data-ttu-id="2942a-221">255</span><span class="sxs-lookup"><span data-stu-id="2942a-221">255</span></span>|<span data-ttu-id="2942a-222">Zostanie zakończone filtrowanie wyjątków zarządzanych.</span><span class="sxs-lookup"><span data-stu-id="2942a-222">A managed exception filtering ends.</span></span>|

## <a name="exceptionthrownstop-event"></a><span data-ttu-id="2942a-223">Zdarzenie ExceptionThrownStop</span><span class="sxs-lookup"><span data-stu-id="2942a-223">ExceptionThrownStop event</span></span>

<span data-ttu-id="2942a-224">To zdarzenie jest emitowane, gdy środowisko uruchomieniowe zakończy obsługę zgłoszonego wyjątku.</span><span class="sxs-lookup"><span data-stu-id="2942a-224">This event is emitted when the runtime is done handling a managed exception that was thrown.</span></span>

|<span data-ttu-id="2942a-225">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="2942a-225">Keyword for raising the event</span></span>|<span data-ttu-id="2942a-226">Poziom</span><span class="sxs-lookup"><span data-stu-id="2942a-226">Level</span></span>|
|-----------------------------------|-----------|
|<span data-ttu-id="2942a-227">`ExceptionKeyword` 0x8000</span><span class="sxs-lookup"><span data-stu-id="2942a-227">`ExceptionKeyword` (0x8000)</span></span>|<span data-ttu-id="2942a-228">Informacyjny (4)</span><span class="sxs-lookup"><span data-stu-id="2942a-228">Informational (4)</span></span>|
  
 <span data-ttu-id="2942a-229">W poniższej tabeli przedstawiono informacje o zdarzeniach.</span><span class="sxs-lookup"><span data-stu-id="2942a-229">The following table shows event information.</span></span>

|<span data-ttu-id="2942a-230">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="2942a-230">Event</span></span>|<span data-ttu-id="2942a-231">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="2942a-231">Event ID</span></span>|<span data-ttu-id="2942a-232">Wywoływane, gdy</span><span class="sxs-lookup"><span data-stu-id="2942a-232">Raised when</span></span>|
|-----------|--------------|-----------------|
|`ExceptionThrownStop`|<span data-ttu-id="2942a-233">256</span><span class="sxs-lookup"><span data-stu-id="2942a-233">256</span></span>|<span data-ttu-id="2942a-234">Zostanie zakończone filtrowanie wyjątków zarządzanych.</span><span class="sxs-lookup"><span data-stu-id="2942a-234">A managed exception filtering ends.</span></span>|
