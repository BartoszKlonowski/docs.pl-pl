---
title: Wpisz zdarzenia środowiska uruchomieniowego systemu
description: Zobacz zdarzenia środowiska uruchomieniowego platformy .NET, które zbierają informacje diagnostyczne specyficzne dla systemu typu .NET, takie jak TypeLoadStart i TypeLoadStop.
ms.date: 11/13/2020
ms.topic: reference
helpviewer_keywords:
- type system events (CoreCLR)
- ETW, EventPipe, LTTng type system events (CoreCLR)
ms.openlocfilehash: 8eee89cddb0098da2cb449a4be21945adac725e3
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "96589988"
---
# <a name="net-runtime-type-events"></a><span data-ttu-id="7e249-103">Zdarzenia typu środowiska uruchomieniowego .NET</span><span class="sxs-lookup"><span data-stu-id="7e249-103">.NET runtime type events</span></span>

<span data-ttu-id="7e249-104">Te zdarzenia zbierają informacje dotyczące typów ładowania.</span><span class="sxs-lookup"><span data-stu-id="7e249-104">These events collect information relating to loading types.</span></span> <span data-ttu-id="7e249-105">Aby uzyskać więcej informacji na temat korzystania z tych zdarzeń w celach diagnostycznych, zobacz [Rejestrowanie i śledzenie aplikacji .NET](../../core/diagnostics/logging-tracing.md) .</span><span class="sxs-lookup"><span data-stu-id="7e249-105">For more information about how to use these events for diagnostic purposes, see [logging and tracing .NET applications](../../core/diagnostics/logging-tracing.md)</span></span>

## <a name="typeloadstart-event"></a><span data-ttu-id="7e249-106">Zdarzenie TypeLoadStart</span><span class="sxs-lookup"><span data-stu-id="7e249-106">TypeLoadStart Event</span></span>

|<span data-ttu-id="7e249-107">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="7e249-107">Keyword for raising the event</span></span>|<span data-ttu-id="7e249-108">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="7e249-108">Event</span></span>|<span data-ttu-id="7e249-109">Poziom</span><span class="sxs-lookup"><span data-stu-id="7e249-109">Level</span></span>|  
|-----------------------------------|-----------|-----------|  
|<span data-ttu-id="7e249-110">`TypeDiagnosticKeyword` (0x8000000000)</span><span class="sxs-lookup"><span data-stu-id="7e249-110">`TypeDiagnosticKeyword` (0x8000000000)</span></span>|<span data-ttu-id="7e249-111">Informacyjny (4)</span><span class="sxs-lookup"><span data-stu-id="7e249-111">Informational (4)</span></span>|  

|<span data-ttu-id="7e249-112">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="7e249-112">Event</span></span>|<span data-ttu-id="7e249-113">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="7e249-113">Event ID</span></span>|<span data-ttu-id="7e249-114">Opis</span><span class="sxs-lookup"><span data-stu-id="7e249-114">Description</span></span>|  
|-----------|--------------|-----------------|  
|`TypeLoadStart`|<span data-ttu-id="7e249-115">73</span><span class="sxs-lookup"><span data-stu-id="7e249-115">73</span></span>|<span data-ttu-id="7e249-116">Ładowanie typu zostało rozpoczęte.</span><span class="sxs-lookup"><span data-stu-id="7e249-116">A type load has started.</span></span>|

|<span data-ttu-id="7e249-117">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="7e249-117">Field name</span></span>|<span data-ttu-id="7e249-118">Typ danych</span><span class="sxs-lookup"><span data-stu-id="7e249-118">Data type</span></span>|<span data-ttu-id="7e249-119">Opis</span><span class="sxs-lookup"><span data-stu-id="7e249-119">Description</span></span>|  
|----------------|---------------|-----------------|  
|`TypeLoadStartID`|`win:UInt32`|<span data-ttu-id="7e249-120">Identyfikator operacji ładowania typu.</span><span class="sxs-lookup"><span data-stu-id="7e249-120">ID for the type load operation.</span></span>|
|`ClrInstanceID`|`win:UInt16`|<span data-ttu-id="7e249-121">Unikatowy identyfikator wystąpienia CLR lub CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="7e249-121">Unique ID for the instance of CLR or CoreCLR.</span></span>|  

## <a name="typeloadstop-event"></a><span data-ttu-id="7e249-122">Zdarzenie TypeLoadStop</span><span class="sxs-lookup"><span data-stu-id="7e249-122">TypeLoadStop Event</span></span>

|<span data-ttu-id="7e249-123">Słowo kluczowe do podniesienia zdarzenia</span><span class="sxs-lookup"><span data-stu-id="7e249-123">Keyword for raising the event</span></span>|<span data-ttu-id="7e249-124">Poziom</span><span class="sxs-lookup"><span data-stu-id="7e249-124">Level</span></span>|  
|-----------------------------------|-----------|-----------|  
|<span data-ttu-id="7e249-125">`TypeDiagnosticKeyword` (0x8000000000)</span><span class="sxs-lookup"><span data-stu-id="7e249-125">`TypeDiagnosticKeyword` (0x8000000000)</span></span>|<span data-ttu-id="7e249-126">Informacyjny (4)</span><span class="sxs-lookup"><span data-stu-id="7e249-126">Informational (4)</span></span>|  

|<span data-ttu-id="7e249-127">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="7e249-127">Event</span></span>|<span data-ttu-id="7e249-128">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="7e249-128">Event ID</span></span>|<span data-ttu-id="7e249-129">Opis</span><span class="sxs-lookup"><span data-stu-id="7e249-129">Description</span></span>|  
|-----------|--------------|-----------------|  
|`TypeLoadStop`|<span data-ttu-id="7e249-130">74</span><span class="sxs-lookup"><span data-stu-id="7e249-130">74</span></span>|<span data-ttu-id="7e249-131">Ładowanie typu zostało zakończone.</span><span class="sxs-lookup"><span data-stu-id="7e249-131">A type load is finished.</span></span>|

|<span data-ttu-id="7e249-132">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="7e249-132">Field name</span></span>|<span data-ttu-id="7e249-133">Typ danych</span><span class="sxs-lookup"><span data-stu-id="7e249-133">Data type</span></span>|<span data-ttu-id="7e249-134">Opis</span><span class="sxs-lookup"><span data-stu-id="7e249-134">Description</span></span>|  
|----------------|---------------|-----------------|  
|`TypeLoadStartID`|`win:UInt32`|<span data-ttu-id="7e249-135">Identyfikator operacji ładowania typu (pasuje do odpowiadającego TypeLoadStartID zdarzenia TypeLoadStart).</span><span class="sxs-lookup"><span data-stu-id="7e249-135">ID for the type load operation (matches the corresponding TypeLoadStart event's TypeLoadStartID).</span></span>|
|`LoadLevel`|`win:UInt16`|<span data-ttu-id="7e249-136">Wpisz poziom ładowania.</span><span class="sxs-lookup"><span data-stu-id="7e249-136">Type load level.</span></span>|
|`TypeID`|`win:UInt64`|<span data-ttu-id="7e249-137">Wskaźnik do dojścia do typu.</span><span class="sxs-lookup"><span data-stu-id="7e249-137">Pointer to the type handle.</span></span>|
|`TypeName`|`win:UnicodeString`|<span data-ttu-id="7e249-138">Nazwa typu.</span><span class="sxs-lookup"><span data-stu-id="7e249-138">Name of the type.</span></span>|
|`ClrInstanceID`|`win:UInt16`|<span data-ttu-id="7e249-139">Unikatowy identyfikator wystąpienia CLR lub CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="7e249-139">Unique ID for the instance of CLR or CoreCLR.</span></span>|  
