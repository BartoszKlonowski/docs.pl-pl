---
title: Zdarzenia wyjątku ETW Thrown_V1
description: Wyświetl szczegółowe informacje o zdarzeniu ETW ExceptionThrown_V1. Dane zdarzenia, takie jak nazwy pól, typy danych i opisy, są przyznawane dla zgłaszanych wyjątków.
ms.date: 03/30/2017
helpviewer_keywords:
- ExceptionThrown_V1 event [.NET Framework]
- ETW, ExceptionThrown_V1 event (CLR)
ms.assetid: 0d3da389-6b7b-40f6-a877-fac546d6019c
ms.openlocfilehash: c1ba994b291bd278a95e34beb0b02ed6581786e8
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96263480"
---
# <a name="exception-thrown_v1-etw-event"></a><span data-ttu-id="118ef-104">Zdarzenia wyjątku ETW Thrown_V1</span><span class="sxs-lookup"><span data-stu-id="118ef-104">Exception Thrown_V1 ETW Event</span></span>

<span data-ttu-id="118ef-105">To zdarzenie przechwytuje informacje o wygenerowanych wyjątkach.</span><span class="sxs-lookup"><span data-stu-id="118ef-105">This event captures information about the exceptions that are thrown.</span></span>  
  
 <span data-ttu-id="118ef-106">W poniższej tabeli przedstawiono słowo kluczowe, pod którym zdarzenie jest zgłaszane, oraz poziom zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="118ef-106">The following table shows the keyword under which the event is raised, and the level of the event.</span></span> <span data-ttu-id="118ef-107">(Aby uzyskać więcej informacji, zobacz [słowa kluczowe i poziomy ETW CLR](clr-etw-keywords-and-levels.md)).</span><span class="sxs-lookup"><span data-stu-id="118ef-107">(For more information, see [CLR ETW Keywords and Levels](clr-etw-keywords-and-levels.md).)</span></span>  
  
|<span data-ttu-id="118ef-108">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="118ef-108">Keyword for raising the event</span></span>|<span data-ttu-id="118ef-109">Poziom</span><span class="sxs-lookup"><span data-stu-id="118ef-109">Level</span></span>|  
|-----------------------------------|-----------|  
|<span data-ttu-id="118ef-110">`ExceptionKeyword` 0x8000</span><span class="sxs-lookup"><span data-stu-id="118ef-110">`ExceptionKeyword` (0x8000)</span></span>|<span data-ttu-id="118ef-111">Ostrzeżenie (2)</span><span class="sxs-lookup"><span data-stu-id="118ef-111">Warning (2)</span></span>|  
  
 <span data-ttu-id="118ef-112">W poniższej tabeli przedstawiono informacje o zdarzeniach.</span><span class="sxs-lookup"><span data-stu-id="118ef-112">The following table shows event information.</span></span>  
  
|<span data-ttu-id="118ef-113">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="118ef-113">Event</span></span>|<span data-ttu-id="118ef-114">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="118ef-114">Event ID</span></span>|<span data-ttu-id="118ef-115">Wywoływane, gdy</span><span class="sxs-lookup"><span data-stu-id="118ef-115">Raised when</span></span>|  
|-----------|--------------|-----------------|  
|`ExceptionThrown_V1`|<span data-ttu-id="118ef-116">80</span><span class="sxs-lookup"><span data-stu-id="118ef-116">80</span></span>|<span data-ttu-id="118ef-117">Generowany jest wyjątek zarządzany.</span><span class="sxs-lookup"><span data-stu-id="118ef-117">A managed exception is thrown.</span></span>|  
  
 <span data-ttu-id="118ef-118">W poniższej tabeli przedstawiono dane zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="118ef-118">The following table shows event data.</span></span>  
  
|<span data-ttu-id="118ef-119">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="118ef-119">Field name</span></span>|<span data-ttu-id="118ef-120">Typ danych</span><span class="sxs-lookup"><span data-stu-id="118ef-120">Data type</span></span>|<span data-ttu-id="118ef-121">Opis</span><span class="sxs-lookup"><span data-stu-id="118ef-121">Description</span></span>|  
|----------------|---------------|-----------------|  
|<span data-ttu-id="118ef-122">Typ wyjątku</span><span class="sxs-lookup"><span data-stu-id="118ef-122">Exception Type</span></span>|<span data-ttu-id="118ef-123">win: UnicodeString</span><span class="sxs-lookup"><span data-stu-id="118ef-123">win:UnicodeString</span></span>|<span data-ttu-id="118ef-124">Typ wyjątku; na przykład `System.NullReferenceException` .</span><span class="sxs-lookup"><span data-stu-id="118ef-124">Type of the exception; for example, `System.NullReferenceException`.</span></span>|  
|<span data-ttu-id="118ef-125">Komunikat o wyjątku</span><span class="sxs-lookup"><span data-stu-id="118ef-125">Exception Message</span></span>|<span data-ttu-id="118ef-126">win: UnicodeString</span><span class="sxs-lookup"><span data-stu-id="118ef-126">win:UnicodeString</span></span>|<span data-ttu-id="118ef-127">Rzeczywisty komunikat o wyjątku.</span><span class="sxs-lookup"><span data-stu-id="118ef-127">Actual exception message.</span></span>|  
|<span data-ttu-id="118ef-128">EIPCodeThrow</span><span class="sxs-lookup"><span data-stu-id="118ef-128">EIPCodeThrow</span></span>|<span data-ttu-id="118ef-129">win: wskaźnik</span><span class="sxs-lookup"><span data-stu-id="118ef-129">win:Pointer</span></span>|<span data-ttu-id="118ef-130">Wskaźnik instrukcji, w którym wystąpił wyjątek.</span><span class="sxs-lookup"><span data-stu-id="118ef-130">Instruction pointer where exception occurred.</span></span>|  
|<span data-ttu-id="118ef-131">ExceptionHR</span><span class="sxs-lookup"><span data-stu-id="118ef-131">ExceptionHR</span></span>|<span data-ttu-id="118ef-132">win: UInt32</span><span class="sxs-lookup"><span data-stu-id="118ef-132">win:UInt32</span></span>|<span data-ttu-id="118ef-133">Wyjątek [HRESULT](/openspecs/windows_protocols/ms-erref/0642cb2f-2075-4469-918c-4441e69c548a).</span><span class="sxs-lookup"><span data-stu-id="118ef-133">Exception [HRESULT](/openspecs/windows_protocols/ms-erref/0642cb2f-2075-4469-918c-4441e69c548a).</span></span>|  
|<span data-ttu-id="118ef-134">ExceptionFlags</span><span class="sxs-lookup"><span data-stu-id="118ef-134">ExceptionFlags</span></span>|<span data-ttu-id="118ef-135">win: UInt16</span><span class="sxs-lookup"><span data-stu-id="118ef-135">win:UInt16</span></span>|<span data-ttu-id="118ef-136">0x01: HasInnerException (zobacz [zdarzenia ETW CLR](clr-etw-events.md) w dokumentacji Visual Basic).</span><span class="sxs-lookup"><span data-stu-id="118ef-136">0x01: HasInnerException (see [CLR ETW Events](clr-etw-events.md) in the Visual Basic documentation).</span></span><br /><br /> <span data-ttu-id="118ef-137">0x02: isnestexception.</span><span class="sxs-lookup"><span data-stu-id="118ef-137">0x02: IsNestedException.</span></span><br /><br /> <span data-ttu-id="118ef-138">0x04: IsRethrownException.</span><span class="sxs-lookup"><span data-stu-id="118ef-138">0x04: IsRethrownException.</span></span><br /><br /> <span data-ttu-id="118ef-139">0x08: IsCorruptedStateException (wskazuje, że stan procesu jest uszkodzony; zobacz [Obsługa wyjątków uszkodzonego stanu](/archive/msdn-magazine/2009/february/clr-inside-out-handling-corrupted-state-exceptions)).</span><span class="sxs-lookup"><span data-stu-id="118ef-139">0x08: IsCorruptedStateException (indicates that the process state is corrupt; see [Handling Corrupted State Exceptions](/archive/msdn-magazine/2009/february/clr-inside-out-handling-corrupted-state-exceptions)).</span></span><br /><br /> <span data-ttu-id="118ef-140">0x10: IsCLSCompliant (wyjątek pochodzący z <xref:System.Exception> jest zgodny ze specyfikacją CLS; w przeciwnym razie jest to niezgodne ze specyfikacją CLS).</span><span class="sxs-lookup"><span data-stu-id="118ef-140">0x10: IsCLSCompliant (an exception that derives from <xref:System.Exception> is CLS-compliant; otherwise, it is not CLS-compliant).</span></span>|  
|<span data-ttu-id="118ef-141">ClrInstanceID</span><span class="sxs-lookup"><span data-stu-id="118ef-141">ClrInstanceID</span></span>|<span data-ttu-id="118ef-142">win: UInt16</span><span class="sxs-lookup"><span data-stu-id="118ef-142">win:UInt16</span></span>|<span data-ttu-id="118ef-143">Unikatowy identyfikator wystąpienia CLR lub CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="118ef-143">Unique ID for the instance of CLR or CoreCLR.</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="118ef-144">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="118ef-144">See also</span></span>

- [<span data-ttu-id="118ef-145">Zdarzenia ETW CLR</span><span class="sxs-lookup"><span data-stu-id="118ef-145">CLR ETW Events</span></span>](clr-etw-events.md)
