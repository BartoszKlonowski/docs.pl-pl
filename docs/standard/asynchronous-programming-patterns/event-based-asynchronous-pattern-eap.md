---
title: Asynchroniczny wzorzec oparty na zdarzeniach (EAP)
description: Zobacz linki do artykułów na temat wzorca asynchronicznego opartego na zdarzeniach (EAP) w programie .NET, takich jak implementacja, najlepsze rozwiązania, implementacja klienta protokołu EAP i wiele innych.
ms.date: 07/23/2018
helpviewer_keywords:
- asynchronous calls
- asynchronous programming, design patterns
- asynchronous programming
ms.assetid: c6baed9f-2a25-4728-9a9a-53b7b14840cf
ms.openlocfilehash: c15bb6c9ec6ea737e6f240376e12bf8de3aa61bc
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "94830405"
---
# <a name="event-based-asynchronous-pattern-eap"></a><span data-ttu-id="6d80a-103">Asynchroniczny wzorzec oparty na zdarzeniach (EAP)</span><span class="sxs-lookup"><span data-stu-id="6d80a-103">Event-based Asynchronous Pattern (EAP)</span></span>

<span data-ttu-id="6d80a-104">Istnieje wiele sposobów udostępniania funkcji asynchronicznych kodowi klienta.</span><span class="sxs-lookup"><span data-stu-id="6d80a-104">There are a number of ways to expose asynchronous features to client code.</span></span> <span data-ttu-id="6d80a-105">Wzorzec asynchroniczny oparty na zdarzeniach umożliwia jednokierunkową metodę prezentowania zachowań asynchronicznych.</span><span class="sxs-lookup"><span data-stu-id="6d80a-105">The Event-based Asynchronous Pattern prescribes one way for classes to present asynchronous behavior.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="6d80a-106">Począwszy od .NET Framework 4, Biblioteka zadań równoległych udostępnia nowy model dla programowania asynchronicznego i równoległego.</span><span class="sxs-lookup"><span data-stu-id="6d80a-106">Starting with .NET Framework 4, the Task Parallel Library provides a new model for asynchronous and parallel programming.</span></span> <span data-ttu-id="6d80a-107">Aby uzyskać więcej informacji, zobacz [Biblioteka zadań równoległych (TPL)](../parallel-programming/task-parallel-library-tpl.md) i [wzorzec asynchroniczny oparty na zadaniach (TAP)](task-based-asynchronous-pattern-tap.md).</span><span class="sxs-lookup"><span data-stu-id="6d80a-107">For more information, see [Task Parallel Library (TPL)](../parallel-programming/task-parallel-library-tpl.md) and [Task-based Asynchronous Pattern (TAP)](task-based-asynchronous-pattern-tap.md).</span></span>
  
## <a name="in-this-section"></a><span data-ttu-id="6d80a-108">W tej sekcji</span><span class="sxs-lookup"><span data-stu-id="6d80a-108">In This Section</span></span>

 [<span data-ttu-id="6d80a-109">Asynchroniczny wzorzec oparty na zdarzeniach — przegląd</span><span class="sxs-lookup"><span data-stu-id="6d80a-109">Event-based Asynchronous Pattern Overview</span></span>](event-based-asynchronous-pattern-overview.md)  
 <span data-ttu-id="6d80a-110">Opisuje sposób, w jaki wzorzec asynchroniczny oparty na zdarzeniach udostępnia zalety aplikacji wielowątkowych, jednocześnie ukrywając wiele złożonych problemów niezależnych od projektów wielowątkowych.</span><span class="sxs-lookup"><span data-stu-id="6d80a-110">Describes how the Event-based Asynchronous Pattern makes available the advantages of multithreaded applications while hiding many of the complex issues inherent in multithreaded design.</span></span>  
  
 [<span data-ttu-id="6d80a-111">Implementacja wzorca asynchronicznego opartego na zdarzeniach</span><span class="sxs-lookup"><span data-stu-id="6d80a-111">Implementing the Event-based Asynchronous Pattern</span></span>](implementing-the-event-based-asynchronous-pattern.md)  
 <span data-ttu-id="6d80a-112">Opisuje ustandaryzowany sposób spakowania klasy, która ma funkcje asynchroniczne.</span><span class="sxs-lookup"><span data-stu-id="6d80a-112">Describes the standardized way to package a class that has asynchronous features.</span></span>  
  
 [<span data-ttu-id="6d80a-113">Najlepsze rozwiązania w zakresie implementacji wzorca asynchronicznego opartego na zdarzeniach</span><span class="sxs-lookup"><span data-stu-id="6d80a-113">Best Practices for Implementing the Event-based Asynchronous Pattern</span></span>](best-practices-for-implementing-the-event-based-asynchronous-pattern.md)  
 <span data-ttu-id="6d80a-114">Opisuje wymagania dotyczące uwidaczniania funkcji asynchronicznych zgodnie ze wzorcem asynchronicznym opartym na zdarzeniach.</span><span class="sxs-lookup"><span data-stu-id="6d80a-114">Describes the requirements for exposing asynchronous features according to the Event-based Asynchronous Pattern.</span></span>  
  
 [<span data-ttu-id="6d80a-115">Decydowanie o czasie implementacji klienta wzorca asynchronicznego opartego na zdarzeniach</span><span class="sxs-lookup"><span data-stu-id="6d80a-115">Deciding When to Implement the Event-based Asynchronous Pattern</span></span>](deciding-when-to-implement-the-event-based-asynchronous-pattern.md)  
 <span data-ttu-id="6d80a-116">Opisuje, jak określić, kiedy należy wybrać implementację wzorca asynchronicznego opartego na zdarzeniach zamiast <xref:System.IAsyncResult> wzorca reprezentowanego przez [model programowania ASYNCHRONICZNEGO (APM)](asynchronous-programming-model-apm.md)</span><span class="sxs-lookup"><span data-stu-id="6d80a-116">Describes how to determine when you should choose to implement the Event-based Asynchronous Pattern instead of the <xref:System.IAsyncResult> pattern represented by the [Asynchronous Programming Model (APM)](asynchronous-programming-model-apm.md)</span></span>
  
 [<span data-ttu-id="6d80a-117">Instrukcje: Implementacja składnika obsługującego wzorzec asynchroniczny oparty na zdarzeniach</span><span class="sxs-lookup"><span data-stu-id="6d80a-117">How to: Implement a Component That Supports the Event-based Asynchronous Pattern</span></span>](component-that-supports-the-event-based-asynchronous-pattern.md)  
 <span data-ttu-id="6d80a-118">Opisuje sposób tworzenia składnika implementującego wzorzec asynchroniczny oparty na zdarzeniach.</span><span class="sxs-lookup"><span data-stu-id="6d80a-118">Describes how to create a component that implements the Event-based Asynchronous Pattern.</span></span> <span data-ttu-id="6d80a-119">Jest implementowana przy użyciu klas pomocników z <xref:System.ComponentModel?displayProperty=nameWithType> przestrzeni nazw, co gwarantuje, że składnik działa prawidłowo w ramach dowolnego modelu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6d80a-119">It is implemented using helper classes from the <xref:System.ComponentModel?displayProperty=nameWithType> namespace, which ensures that the component works correctly under any application model.</span></span>  

 [<span data-ttu-id="6d80a-120">Instrukcje: Implementacja klienta wzorca asynchronicznego opartego na zdarzeniach</span><span class="sxs-lookup"><span data-stu-id="6d80a-120">How to: Implement a Client of the Event-based Asynchronous Pattern</span></span>](how-to-implement-a-client-of-the-event-based-asynchronous-pattern.md)  
 <span data-ttu-id="6d80a-121">Opisuje sposób tworzenia klienta korzystającego ze składnika implementującego wzorzec asynchroniczny oparty na zdarzeniach.</span><span class="sxs-lookup"><span data-stu-id="6d80a-121">Describes how to create a client that uses a component that implements the Event-based Asynchronous Pattern.</span></span>
  
 [<span data-ttu-id="6d80a-122">Instrukcje: Używanie składników obsługujących wzorzec asynchroniczny oparty na zdarzeniach</span><span class="sxs-lookup"><span data-stu-id="6d80a-122">How to: Use Components That Support the Event-based Asynchronous Pattern</span></span>](how-to-use-components-that-support-the-event-based-asynchronous-pattern.md)  
 <span data-ttu-id="6d80a-123">Opisuje sposób użycia składnika obsługującego wzorzec asynchroniczny oparty na zdarzeniach.</span><span class="sxs-lookup"><span data-stu-id="6d80a-123">Describes how to use a component that supports the Event-based Asynchronous Pattern.</span></span>  
  
## <a name="reference"></a><span data-ttu-id="6d80a-124">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="6d80a-124">Reference</span></span>

 <xref:System.ComponentModel.AsyncOperation>  
 <span data-ttu-id="6d80a-125">Opisuje <xref:System.ComponentModel.AsyncOperation> klasę i zawiera linki do wszystkich jej elementów członkowskich.</span><span class="sxs-lookup"><span data-stu-id="6d80a-125">Describes the <xref:System.ComponentModel.AsyncOperation> class and has links to all its members.</span></span>  
  
 <xref:System.ComponentModel.AsyncOperationManager>  
 <span data-ttu-id="6d80a-126">Opisuje <xref:System.ComponentModel.AsyncOperationManager> klasę i zawiera linki do wszystkich jej elementów członkowskich.</span><span class="sxs-lookup"><span data-stu-id="6d80a-126">Describes the <xref:System.ComponentModel.AsyncOperationManager> class and has links to all its members.</span></span>  
  
 <xref:System.ComponentModel.BackgroundWorker>  
 <span data-ttu-id="6d80a-127">Opisuje <xref:System.ComponentModel.BackgroundWorker> składnik i zawiera linki do wszystkich jego członków.</span><span class="sxs-lookup"><span data-stu-id="6d80a-127">Describes the <xref:System.ComponentModel.BackgroundWorker> component and has links to all its members.</span></span>  
  
## <a name="related-sections"></a><span data-ttu-id="6d80a-128">Sekcje pokrewne</span><span class="sxs-lookup"><span data-stu-id="6d80a-128">Related Sections</span></span>

 [<span data-ttu-id="6d80a-129">Biblioteka zadań równoległych (TPL)</span><span class="sxs-lookup"><span data-stu-id="6d80a-129">Task Parallel Library (TPL)</span></span>](../parallel-programming/task-parallel-library-tpl.md)  
 <span data-ttu-id="6d80a-130">Opisuje model programowania dla operacji asynchronicznych i równoległych.</span><span class="sxs-lookup"><span data-stu-id="6d80a-130">Describes a programming model for asynchronous and parallel operations.</span></span>  
  
 [<span data-ttu-id="6d80a-131">Wątkowość</span><span class="sxs-lookup"><span data-stu-id="6d80a-131">Threading</span></span>](../threading/index.md)  
 <span data-ttu-id="6d80a-132">Opisuje funkcje wielowątkowości w programie .NET.</span><span class="sxs-lookup"><span data-stu-id="6d80a-132">Describes multithreading features in .NET.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="6d80a-133">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="6d80a-133">See also</span></span>

- [<span data-ttu-id="6d80a-134">Zarządzana wątkowość — najlepsze rozwiązania</span><span class="sxs-lookup"><span data-stu-id="6d80a-134">Managed Threading Best Practices</span></span>](../threading/managed-threading-best-practices.md)
- [<span data-ttu-id="6d80a-135">Zdarzenia</span><span class="sxs-lookup"><span data-stu-id="6d80a-135">Events</span></span>](../events/index.md)
- [<span data-ttu-id="6d80a-136">Wzorce projektowania programowania asynchronicznego</span><span class="sxs-lookup"><span data-stu-id="6d80a-136">Asynchronous Programming Design Patterns</span></span>](index.md)
