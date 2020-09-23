---
title: 'Porady: deklarowanie zdarzeń niestandardowych w celu unikania blokowania'
ms.date: 07/20/2015
helpviewer_keywords:
- declaring events [Visual Basic], custom
- events [Visual Basic], custom
- custom events [Visual Basic]
ms.assetid: 998b6a90-67c5-4d2c-8b11-366d3e355505
ms.openlocfilehash: a9350470836652f65532068402c78375b4c5495c
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/23/2020
ms.locfileid: "91077101"
---
# <a name="how-to-declare-custom-events-to-avoid-blocking-visual-basic"></a><span data-ttu-id="9d1a8-102">Porady: deklarowanie zdarzeń niestandardowych w celu unikania blokowania (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="9d1a8-102">How to: Declare Custom Events To Avoid Blocking (Visual Basic)</span></span>

<span data-ttu-id="9d1a8-103">Istnieją pewne sytuacje, w których należy pamiętać, że jedna procedura obsługi zdarzeń nie blokuje kolejnych programów obsługi zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="9d1a8-103">There are several circumstances when it is important that one event handler not block subsequent event handlers.</span></span> <span data-ttu-id="9d1a8-104">Zdarzenia niestandardowe umożliwiają zdarzeniom Asynchroniczne wywoływanie obsługi zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="9d1a8-104">Custom events allow the event to call its event handlers asynchronously.</span></span>  
  
 <span data-ttu-id="9d1a8-105">Domyślnie pole zapasowe magazynu dla deklaracji zdarzenia jest delegatem multiemisji, który szeregowo łączy wszystkie programy obsługi zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="9d1a8-105">By default, the backing-store field for an event declaration is a multicast delegate that serially combines all the event handlers.</span></span> <span data-ttu-id="9d1a8-106">Oznacza to, że jeśli jedna procedura obsługi zajmuje dużo czasu, program blokuje inne programy obsługi do momentu jego zakończenia.</span><span class="sxs-lookup"><span data-stu-id="9d1a8-106">This means that if one handler takes a long time to complete, it blocks the other handlers until it completes.</span></span> <span data-ttu-id="9d1a8-107">(Dobrze działające programy obsługi zdarzeń nigdy nie wykonują długotrwałych ani potencjalnie blokujących operacji).</span><span class="sxs-lookup"><span data-stu-id="9d1a8-107">(Well-behaved event handlers should never perform lengthy or potentially blocking operations.)</span></span>  
  
 <span data-ttu-id="9d1a8-108">Zamiast korzystać z domyślnej implementacji zdarzeń, które Visual Basic zapewnia, można użyć niestandardowego zdarzenia do wykonywania obsługi zdarzeń asynchronicznie.</span><span class="sxs-lookup"><span data-stu-id="9d1a8-108">Instead of using the default implementation of events that Visual Basic provides, you can use a custom event to execute the event handlers asynchronously.</span></span>  
  
## <a name="example"></a><span data-ttu-id="9d1a8-109">Przykład</span><span class="sxs-lookup"><span data-stu-id="9d1a8-109">Example</span></span>  

 <span data-ttu-id="9d1a8-110">W tym przykładzie `AddHandler` metoda dostępu dodaje delegata dla każdego procedury obsługi `Click` zdarzenia do wartości <xref:System.Collections.ArrayList> przechowywanej w `EventHandlerList` polu.</span><span class="sxs-lookup"><span data-stu-id="9d1a8-110">In this example, the `AddHandler` accessor adds the delegate for each handler of the `Click` event to an <xref:System.Collections.ArrayList> stored in the `EventHandlerList` field.</span></span>  
  
 <span data-ttu-id="9d1a8-111">Gdy kod wywołuje `Click` zdarzenie, `RaiseEvent` metoda dostępu wywołuje wszystkie delegatów obsługi zdarzeń asynchronicznie za pomocą <xref:System.Web.Services.Protocols.LogicalMethodInfo.BeginInvoke%2A> metody.</span><span class="sxs-lookup"><span data-stu-id="9d1a8-111">When code raises the `Click` event, the `RaiseEvent` accessor invokes all the event handler delegates asynchronously using the <xref:System.Web.Services.Protocols.LogicalMethodInfo.BeginInvoke%2A> method.</span></span> <span data-ttu-id="9d1a8-112">Ta metoda wywołuje każdy program obsługi w wątku roboczym i zwraca natychmiast, dlatego programy obsługi nie mogą blokować siebie nawzajem.</span><span class="sxs-lookup"><span data-stu-id="9d1a8-112">That method invokes each handler on a worker thread and returns immediately, so handlers cannot block one another.</span></span>  
  
 [!code-vb[VbVbalrEvents#27](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/Class1.vb#27)]  
  
## <a name="see-also"></a><span data-ttu-id="9d1a8-113">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="9d1a8-113">See also</span></span>

- <xref:System.Collections.ArrayList>
- <xref:System.Web.Services.Protocols.LogicalMethodInfo.BeginInvoke%2A>
- [<span data-ttu-id="9d1a8-114">Zdarzenia</span><span class="sxs-lookup"><span data-stu-id="9d1a8-114">Events</span></span>](index.md)
- [<span data-ttu-id="9d1a8-115">Instrukcje: deklarowanie zdarzeń niestandardowych w celu zachowywania pamięci</span><span class="sxs-lookup"><span data-stu-id="9d1a8-115">How to: Declare Custom Events To Conserve Memory</span></span>](how-to-declare-custom-events-to-conserve-memory.md)
