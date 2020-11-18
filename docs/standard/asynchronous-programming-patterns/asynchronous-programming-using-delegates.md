---
title: Programowanie asynchroniczne przy użyciu delegatów
ms.date: 03/30/2017
helpviewer_keywords:
- BeginInvoke method
- asynchronous programming, delegates
- asynchronous delegates
- calling synchronous methods in asynchronous manner
- EndInvoke method
- calling asynchronous methods
- delegates [.NET], asynchronous
- synchronous calling in asynchronous manner
ms.assetid: 38a345ca-6963-4436-9608-5c9defef9c64
ms.openlocfilehash: da468d3b16ee504317c7de2e216a9be2073d1cf3
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "94830509"
---
# <a name="asynchronous-programming-using-delegates"></a><span data-ttu-id="ca3bd-102">Programowanie asynchroniczne przy użyciu delegatów</span><span class="sxs-lookup"><span data-stu-id="ca3bd-102">Asynchronous Programming Using Delegates</span></span>

<span data-ttu-id="ca3bd-103">Delegaty umożliwiają wywoływanie metody synchronicznej w sposób asynchroniczny.</span><span class="sxs-lookup"><span data-stu-id="ca3bd-103">Delegates enable you to call a synchronous method in an asynchronous manner.</span></span> <span data-ttu-id="ca3bd-104">W przypadku wywołania delegata synchronicznie `Invoke` Metoda wywołuje metodę docelową bezpośrednio w bieżącym wątku.</span><span class="sxs-lookup"><span data-stu-id="ca3bd-104">When you call a delegate synchronously, the `Invoke` method calls the target method directly on the current thread.</span></span> <span data-ttu-id="ca3bd-105">Jeśli `BeginInvoke` Metoda jest wywoływana, środowisko uruchomieniowe języka wspólnego (CLR) kolejkuje żądanie i natychmiast wraca do obiektu wywołującego.</span><span class="sxs-lookup"><span data-stu-id="ca3bd-105">If the `BeginInvoke` method is called, the common language runtime (CLR) queues the request and returns immediately to the caller.</span></span> <span data-ttu-id="ca3bd-106">Metoda docelowa jest wywoływana asynchronicznie w wątku z puli wątków.</span><span class="sxs-lookup"><span data-stu-id="ca3bd-106">The target method is called asynchronously on a thread from the thread pool.</span></span> <span data-ttu-id="ca3bd-107">Oryginalny wątek, który przesłał żądanie, jest bezpłatny, aby kontynuować wykonywanie równolegle z metodą docelową.</span><span class="sxs-lookup"><span data-stu-id="ca3bd-107">The original thread, which submitted the request, is free to continue executing in parallel with the target method.</span></span> <span data-ttu-id="ca3bd-108">Jeśli metoda wywołania zwrotnego została określona w wywołaniu `BeginInvoke` metody, metoda wywołania zwrotnego jest wywoływana, gdy metoda docelowa zostanie zakończona.</span><span class="sxs-lookup"><span data-stu-id="ca3bd-108">If a callback method has been specified in the call to the `BeginInvoke` method, the callback method is called when the target method ends.</span></span> <span data-ttu-id="ca3bd-109">W metodzie wywołania zwrotnego `EndInvoke` metoda uzyskuje wartość zwracaną oraz wszystkie parametry wejściowe/wyjściowe lub wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="ca3bd-109">In the callback method, the `EndInvoke` method obtains the return value and any input/output or output-only parameters.</span></span> <span data-ttu-id="ca3bd-110">Jeśli metoda wywołania zwrotnego nie zostanie określona podczas wywoływania `BeginInvoke` , `EndInvoke` można wywołać z wątku, który wywołał `BeginInvoke` .</span><span class="sxs-lookup"><span data-stu-id="ca3bd-110">If no callback method is specified when calling `BeginInvoke`, `EndInvoke` can be called from the thread that called `BeginInvoke`.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="ca3bd-111">Kompilatory powinny emitować klasy delegatów `Invoke` z `BeginInvoke` `EndInvoke` metodami, i przy użyciu podpisu delegata określonego przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ca3bd-111">Compilers should emit delegate classes with `Invoke`, `BeginInvoke`, and `EndInvoke` methods using the delegate signature specified by the user.</span></span> <span data-ttu-id="ca3bd-112">`BeginInvoke`Metody i `EndInvoke` powinny być dekoracyjne.</span><span class="sxs-lookup"><span data-stu-id="ca3bd-112">The `BeginInvoke` and `EndInvoke` methods should be decorated as native.</span></span> <span data-ttu-id="ca3bd-113">Ponieważ te metody są oznaczone jako natywne, środowisko CLR automatycznie udostępnia implementację w czasie ładowania klasy.</span><span class="sxs-lookup"><span data-stu-id="ca3bd-113">Because these methods are marked as native, the CLR automatically provides the implementation at class load time.</span></span> <span data-ttu-id="ca3bd-114">Moduł ładujący gwarantuje, że nie są one zastępowane.</span><span class="sxs-lookup"><span data-stu-id="ca3bd-114">The loader ensures that they are not overridden.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="ca3bd-115">W tej sekcji</span><span class="sxs-lookup"><span data-stu-id="ca3bd-115">In This Section</span></span>  
 [<span data-ttu-id="ca3bd-116">Wywołanie metod synchronicznych w sposób asynchroniczny</span><span class="sxs-lookup"><span data-stu-id="ca3bd-116">Calling Synchronous Methods Asynchronously</span></span>](calling-synchronous-methods-asynchronously.md)  
 <span data-ttu-id="ca3bd-117">W tym artykule omówiono użycie delegatów do wykonywania wywołań asynchronicznych metod zwykłych i przedstawiono proste przykłady kodu, które pokazują cztery sposoby oczekiwania na zwrócenie wywołania asynchronicznego.</span><span class="sxs-lookup"><span data-stu-id="ca3bd-117">Discusses the use of delegates to make asynchronous calls to ordinary methods, and provides simple code examples that show the four ways to wait for an asynchronous call to return.</span></span>  
  
## <a name="related-sections"></a><span data-ttu-id="ca3bd-118">Sekcje pokrewne</span><span class="sxs-lookup"><span data-stu-id="ca3bd-118">Related Sections</span></span>  
 [<span data-ttu-id="ca3bd-119">Asynchroniczny wzorzec oparty na zdarzeniach (EAP)</span><span class="sxs-lookup"><span data-stu-id="ca3bd-119">Event-based Asynchronous Pattern (EAP)</span></span>](event-based-asynchronous-pattern-eap.md)  
 <span data-ttu-id="ca3bd-120">Opisuje programowanie asynchroniczne w programie .NET.</span><span class="sxs-lookup"><span data-stu-id="ca3bd-120">Describes asynchronous programming in .NET.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="ca3bd-121">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="ca3bd-121">See also</span></span>

- <xref:System.Delegate>
