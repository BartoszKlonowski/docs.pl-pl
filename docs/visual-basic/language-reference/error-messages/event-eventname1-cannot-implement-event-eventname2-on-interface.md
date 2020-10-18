---
title: Zdarzenie „<eventname1>” nie może implementować zdarzenia „<eventname2>” w interfejsie „<interface>”, ponieważ ich typy delegowane „<delegate1>” i „<delegate2>” są niezgodne
ms.date: 07/20/2015
f1_keywords:
- vbc31423
- bc31423
helpviewer_keywords:
- BC31423
ms.assetid: 2e754b66-5836-48ff-9697-b9c0d7085f18
ms.openlocfilehash: d0b2b095ed355b420b28e87ed0b9d6a31f049ebf
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2020
ms.locfileid: "92162027"
---
# <a name="bc31423-event-eventname1-cannot-implement-event-eventname2-on-interface-interface-because-their-delegate-types-delegate1-and-delegate2-do-not-match"></a><span data-ttu-id="9f6bf-102">BC31423: zdarzenie " \<eventname1> " nie może implementować zdarzenia " \<eventname2> " w interfejsie " \<interface> ", ponieważ ich typy delegatów " \<delegate1> " i " \<delegate2> " nie pasują do siebie</span><span class="sxs-lookup"><span data-stu-id="9f6bf-102">BC31423: Event '\<eventname1>' cannot implement event '\<eventname2>' on interface '\<interface>' because their delegate types '\<delegate1>' and '\<delegate2>' do not match</span></span>

<span data-ttu-id="9f6bf-103">Visual Basic nie może zaimplementować zdarzenia, ponieważ typ delegata zdarzenia nie jest zgodny z typem delegata zdarzenia w interfejsie.</span><span class="sxs-lookup"><span data-stu-id="9f6bf-103">Visual Basic cannot implement an event because the delegate type of the event does not match the delegate type of the event in the interface.</span></span> <span data-ttu-id="9f6bf-104">Ten błąd może wystąpić, gdy zdefiniujesz wiele zdarzeń w interfejsie, a następnie spróbujesz zaimplementować je razem z tym samym zdarzeniem.</span><span class="sxs-lookup"><span data-stu-id="9f6bf-104">This error can occur when you define multiple events in an interface and then attempt to implement them together with the same event.</span></span> <span data-ttu-id="9f6bf-105">Zdarzenie może zaimplementować dwa lub więcej zdarzeń tylko wtedy, gdy wszystkie zaimplementowane zdarzenia są deklarowane przy użyciu `As` składni i określają ten sam typ delegata.</span><span class="sxs-lookup"><span data-stu-id="9f6bf-105">An event can implement two or more events only if all implemented events are declared using the `As` syntax and specify the same delegate type.</span></span>

 <span data-ttu-id="9f6bf-106">**Identyfikator błędu:** BC31423</span><span class="sxs-lookup"><span data-stu-id="9f6bf-106">**Error ID:** BC31423</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="9f6bf-107">Aby poprawić ten błąd</span><span class="sxs-lookup"><span data-stu-id="9f6bf-107">To correct this error</span></span>

- <span data-ttu-id="9f6bf-108">Zaimplementuj zdarzenia oddzielnie.</span><span class="sxs-lookup"><span data-stu-id="9f6bf-108">Implement the events separately.</span></span>

     <span data-ttu-id="9f6bf-109">—lub—</span><span class="sxs-lookup"><span data-stu-id="9f6bf-109">—or—</span></span>

- <span data-ttu-id="9f6bf-110">Zdefiniuj zdarzenia w interfejsie przy użyciu `As` składni i określ ten sam typ delegata.</span><span class="sxs-lookup"><span data-stu-id="9f6bf-110">Define the events in the interface using the `As` syntax and specify the same delegate type.</span></span>

## <a name="see-also"></a><span data-ttu-id="9f6bf-111">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="9f6bf-111">See also</span></span>

- [<span data-ttu-id="9f6bf-112">Event — Instrukcja</span><span class="sxs-lookup"><span data-stu-id="9f6bf-112">Event Statement</span></span>](../statements/event-statement.md)
- [<span data-ttu-id="9f6bf-113">Delegate — Instrukcja</span><span class="sxs-lookup"><span data-stu-id="9f6bf-113">Delegate Statement</span></span>](../statements/delegate-statement.md)
- [<span data-ttu-id="9f6bf-114">Zdarzenia</span><span class="sxs-lookup"><span data-stu-id="9f6bf-114">Events</span></span>](../../programming-guide/language-features/events/index.md)
