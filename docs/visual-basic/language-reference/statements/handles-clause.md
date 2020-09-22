---
title: Handles, klauzula
ms.date: 07/20/2015
f1_keywords:
- Handles
- vb.Handles
helpviewer_keywords:
- Handles keyword [Visual Basic]
ms.assetid: 1b051c0e-f499-42f6-acb5-6f4f27824b40
ms.openlocfilehash: 347f521267d4fd954ac359ab25ed5810cfd71d34
ms.sourcegitcommit: d2db216e46323f73b32ae312c9e4135258e5d68e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "90873248"
---
# <a name="handles-clause-visual-basic"></a><span data-ttu-id="b7967-102">Handles — Klauzula (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="b7967-102">Handles Clause (Visual Basic)</span></span>

<span data-ttu-id="b7967-103">Deklaruje, że procedura obsługuje określone zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="b7967-103">Declares that a procedure handles a specified event.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="b7967-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="b7967-104">Syntax</span></span>  
  
```vb  
proceduredeclaration Handles eventlist  
```  
  
## <a name="parts"></a><span data-ttu-id="b7967-105">Części</span><span class="sxs-lookup"><span data-stu-id="b7967-105">Parts</span></span>  

 `proceduredeclaration`  
 <span data-ttu-id="b7967-106">`Sub`Deklaracja procedury dla procedury, która będzie obsługiwać zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="b7967-106">The `Sub` procedure declaration for the procedure that will handle the event.</span></span>  
  
 `eventlist`  
 <span data-ttu-id="b7967-107">Lista zdarzeń `proceduredeclaration` do obsługi, rozdzielonych przecinkami.</span><span class="sxs-lookup"><span data-stu-id="b7967-107">List of the events for `proceduredeclaration` to handle, separated by commas.</span></span> <span data-ttu-id="b7967-108">Zdarzenia muszą być wywoływane przez klasę bazową dla bieżącej klasy lub przez obiekt zadeklarowany za pomocą `WithEvents` słowa kluczowego.</span><span class="sxs-lookup"><span data-stu-id="b7967-108">The events must be raised by either the base class for the current class, or by an object declared using the `WithEvents` keyword.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="b7967-109">Uwagi</span><span class="sxs-lookup"><span data-stu-id="b7967-109">Remarks</span></span>  

 <span data-ttu-id="b7967-110">Użyj `Handles` słowa kluczowego na końcu deklaracji procedury, aby spowodować obsługę zdarzeń wywoływanych przez zmienną obiektu zadeklarowaną za pomocą `WithEvents` słowa kluczowego.</span><span class="sxs-lookup"><span data-stu-id="b7967-110">Use the `Handles` keyword at the end of a procedure declaration to cause it to handle events raised by an object variable declared using the `WithEvents` keyword.</span></span> <span data-ttu-id="b7967-111">`Handles`Słowo kluczowe może być również używane w klasie pochodnej do obsługi zdarzeń z klasy bazowej.</span><span class="sxs-lookup"><span data-stu-id="b7967-111">The `Handles` keyword can also be used in a derived class to handle events from a base class.</span></span>  
  
 <span data-ttu-id="b7967-112">`Handles`Słowo kluczowe i `AddHandler` instrukcja umożliwiają określenie, że konkretne procedury obsługują określone zdarzenia, ale istnieją różnice.</span><span class="sxs-lookup"><span data-stu-id="b7967-112">The `Handles` keyword and the `AddHandler` statement both allow you to specify that particular procedures handle particular events, but there are differences.</span></span> <span data-ttu-id="b7967-113">Użyj `Handles` słowa kluczowego podczas definiowania procedury, aby określić, że obsługuje określone zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="b7967-113">Use the `Handles` keyword when defining a procedure to specify that it handles a particular event.</span></span> <span data-ttu-id="b7967-114">`AddHandler`Instrukcja łączy procedury ze zdarzeniami w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="b7967-114">The `AddHandler` statement connects procedures to events at run time.</span></span> <span data-ttu-id="b7967-115">Aby uzyskać więcej informacji, zobacz [AddHandler instrukcji](addhandler-statement.md).</span><span class="sxs-lookup"><span data-stu-id="b7967-115">For more information, see [AddHandler Statement](addhandler-statement.md).</span></span>  
  
 <span data-ttu-id="b7967-116">W przypadku zdarzeń niestandardowych aplikacja wywołuje metodę dostępu do zdarzenia, `AddHandler` gdy dodaje procedurę jako program obsługi zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="b7967-116">For custom events, the application invokes the event's `AddHandler` accessor when it adds the procedure as an event handler.</span></span> <span data-ttu-id="b7967-117">Aby uzyskać więcej informacji na temat zdarzeń niestandardowych, zobacz [instrukcja zdarzenia](event-statement.md).</span><span class="sxs-lookup"><span data-stu-id="b7967-117">For more information on custom events, see [Event Statement](event-statement.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="b7967-118">Przykład</span><span class="sxs-lookup"><span data-stu-id="b7967-118">Example</span></span>  

 [!code-vb[VbVbalrEvents#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/Class1.vb#2)]  
  
 <span data-ttu-id="b7967-119">W poniższym przykładzie pokazano, jak Klasa pochodna może używać `Handles` instrukcji do obsługi zdarzenia z klasy bazowej.</span><span class="sxs-lookup"><span data-stu-id="b7967-119">The following example demonstrates how a derived class can use the `Handles` statement to handle an event from a base class.</span></span>  
  
 [!code-vb[VbVbalrEvents#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/Class1.vb#3)]  
  
## <a name="example"></a><span data-ttu-id="b7967-120">Przykład</span><span class="sxs-lookup"><span data-stu-id="b7967-120">Example</span></span>  

 <span data-ttu-id="b7967-121">Poniższy przykład zawiera dwa programy obsługi zdarzeń przycisków dla projektu **aplikacji WPF** .</span><span class="sxs-lookup"><span data-stu-id="b7967-121">The following example contains two button event handlers for a **WPF Application** project.</span></span>  
  
 [!code-vb[VbVbalrEvents#41](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/class3.vb#41)]  
  
## <a name="example"></a><span data-ttu-id="b7967-122">Przykład</span><span class="sxs-lookup"><span data-stu-id="b7967-122">Example</span></span>  

 <span data-ttu-id="b7967-123">Poniższy przykład jest równoważny z poprzednim przykładem.</span><span class="sxs-lookup"><span data-stu-id="b7967-123">The following example is equivalent to the previous example.</span></span> <span data-ttu-id="b7967-124">`eventlist` `Handles` Klauzula in zawiera zdarzenia dla obu przycisków.</span><span class="sxs-lookup"><span data-stu-id="b7967-124">The `eventlist` in the `Handles` clause contains the events for both buttons.</span></span>  
  
 [!code-vb[VbVbalrEvents#42](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/class3.vb#42)]  
  
## <a name="see-also"></a><span data-ttu-id="b7967-125">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="b7967-125">See also</span></span>

- [<span data-ttu-id="b7967-126">WithEvents</span><span class="sxs-lookup"><span data-stu-id="b7967-126">WithEvents</span></span>](../modifiers/withevents.md)
- [<span data-ttu-id="b7967-127">AddHandler — Instrukcja</span><span class="sxs-lookup"><span data-stu-id="b7967-127">AddHandler Statement</span></span>](addhandler-statement.md)
- [<span data-ttu-id="b7967-128">RemoveHandler — Instrukcja</span><span class="sxs-lookup"><span data-stu-id="b7967-128">RemoveHandler Statement</span></span>](removehandler-statement.md)
- [<span data-ttu-id="b7967-129">Event — Instrukcja</span><span class="sxs-lookup"><span data-stu-id="b7967-129">Event Statement</span></span>](event-statement.md)
- [<span data-ttu-id="b7967-130">RaiseEvent — Instrukcja</span><span class="sxs-lookup"><span data-stu-id="b7967-130">RaiseEvent Statement</span></span>](raiseevent-statement.md)
- [<span data-ttu-id="b7967-131">Zdarzenia</span><span class="sxs-lookup"><span data-stu-id="b7967-131">Events</span></span>](../../programming-guide/language-features/events/index.md)
