---
title: Implements, klauzula
ms.date: 07/20/2015
f1_keywords:
- vb.ImplementsClause
helpviewer_keywords:
- interface implementation [Visual Basic], reimplementation
- interface members [Visual Basic], reimplementation
- interface members [Visual Basic], Implements keyword
- interface members
- members [Visual Basic], reimplementation
- interface implementation [Visual Basic], Implements keyword
- interface members [Visual Basic], implementing
- Implements keyword [Visual Basic]
- Implements statement [Visual Basic], about Implements
- members [Visual Basic], implementing
- members [Visual Basic], Implements keyword
- reimplementation
ms.assetid: 5252cdf9-964d-4fc6-af0f-0449b7126b5a
ms.openlocfilehash: 7c95cf76b1bac24e2a0f20857b8984d54ebbea85
ms.sourcegitcommit: d2db216e46323f73b32ae312c9e4135258e5d68e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "90866163"
---
# <a name="implements-clause-visual-basic"></a><span data-ttu-id="57110-102">Implements — Klauzula (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="57110-102">Implements Clause (Visual Basic)</span></span>

<span data-ttu-id="57110-103">Wskazuje, że składowa klasy lub struktury dostarcza implementację dla składowej zdefiniowanej w interfejsie.</span><span class="sxs-lookup"><span data-stu-id="57110-103">Indicates that a class or structure member is providing the implementation for a member defined in an interface.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="57110-104">Uwagi</span><span class="sxs-lookup"><span data-stu-id="57110-104">Remarks</span></span>  

<span data-ttu-id="57110-105">`Implements`Słowo kluczowe nie jest takie samo jak [instrukcja Implements](implements-statement.md).</span><span class="sxs-lookup"><span data-stu-id="57110-105">The `Implements` keyword is not the same as the [Implements Statement](implements-statement.md).</span></span> <span data-ttu-id="57110-106">Możesz użyć `Implements` instrukcji, aby określić, że Klasa lub struktura implementuje jeden lub więcej interfejsów, a następnie dla każdego elementu członkowskiego używa `Implements` słowa kluczowego, aby określić, który interfejs i który element członkowski implementuje.</span><span class="sxs-lookup"><span data-stu-id="57110-106">You use the `Implements` statement to specify that a class or structure implements one or more interfaces, and then for each member you use the `Implements` keyword to specify which interface and which member it implements.</span></span>

<span data-ttu-id="57110-107">Jeśli klasa lub struktura implementuje interfejs, musi zawierać `Implements` instrukcję bezpośrednio po [instrukcji klasy](class-statement.md) lub [instrukcji struktury](structure-statement.md)i musi zaimplementować wszystkie elementy członkowskie zdefiniowane przez interfejs.</span><span class="sxs-lookup"><span data-stu-id="57110-107">If a class or structure implements an interface, it must include the `Implements` statement immediately after the [Class Statement](class-statement.md) or [Structure Statement](structure-statement.md), and it must implement all the members defined by the interface.</span></span>

## <a name="reimplementation"></a><span data-ttu-id="57110-108">Reimplementacja</span><span class="sxs-lookup"><span data-stu-id="57110-108">Reimplementation</span></span>  

<span data-ttu-id="57110-109">W klasie pochodnej można wykonać ponowną implementację elementu członkowskiego interfejsu, który został już zaimplementowany przez klasę bazową.</span><span class="sxs-lookup"><span data-stu-id="57110-109">In a derived class, you can reimplement an interface member that the base class has already implemented.</span></span> <span data-ttu-id="57110-110">Różni się to od przesłaniania składowej klasy bazowej w następujących aspektach:</span><span class="sxs-lookup"><span data-stu-id="57110-110">This is different from overriding the base class member in the following respects:</span></span>

- <span data-ttu-id="57110-111">Składowa klasy bazowej nie musi być zaimplementowana [, aby](../modifiers/overridable.md) można ją było ponownie zaimplementować.</span><span class="sxs-lookup"><span data-stu-id="57110-111">The base class member does not need to be [Overridable](../modifiers/overridable.md) to be reimplemented.</span></span>
- <span data-ttu-id="57110-112">Można wykonać ponowną implementację elementu członkowskiego z inną nazwą.</span><span class="sxs-lookup"><span data-stu-id="57110-112">You can reimplement the member with a different name.</span></span>

<span data-ttu-id="57110-113">`Implements`Słowo kluczowe może być używane w następujących kontekstach:</span><span class="sxs-lookup"><span data-stu-id="57110-113">The `Implements` keyword can be used in the following contexts:</span></span>

- [<span data-ttu-id="57110-114">Event — Instrukcja</span><span class="sxs-lookup"><span data-stu-id="57110-114">Event Statement</span></span>](event-statement.md)
- [<span data-ttu-id="57110-115">Function, instrukcja</span><span class="sxs-lookup"><span data-stu-id="57110-115">Function Statement</span></span>](function-statement.md)
- [<span data-ttu-id="57110-116">Property — Instrukcja</span><span class="sxs-lookup"><span data-stu-id="57110-116">Property Statement</span></span>](property-statement.md)
- [<span data-ttu-id="57110-117">Sub, instrukcja</span><span class="sxs-lookup"><span data-stu-id="57110-117">Sub Statement</span></span>](sub-statement.md)  
  
## <a name="see-also"></a><span data-ttu-id="57110-118">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="57110-118">See also</span></span>

- [<span data-ttu-id="57110-119">Implements — Instrukcja</span><span class="sxs-lookup"><span data-stu-id="57110-119">Implements Statement</span></span>](implements-statement.md)
- [<span data-ttu-id="57110-120">Interface, instrukcja</span><span class="sxs-lookup"><span data-stu-id="57110-120">Interface Statement</span></span>](interface-statement.md)
- [<span data-ttu-id="57110-121">Class, instrukcja</span><span class="sxs-lookup"><span data-stu-id="57110-121">Class Statement</span></span>](class-statement.md)
- [<span data-ttu-id="57110-122">Structure — Instrukcja</span><span class="sxs-lookup"><span data-stu-id="57110-122">Structure Statement</span></span>](structure-statement.md)
