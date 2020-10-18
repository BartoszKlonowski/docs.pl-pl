---
title: „<methodname>” ma wiele definicji o identycznych podpisach
ms.date: 07/20/2015
f1_keywords:
- vbc30269
- bc30269
helpviewer_keywords:
- BC30269
ms.assetid: 39489621-6617-4e5c-9b24-c2faf8273891
ms.openlocfilehash: 663b22421d1a0e401cfb3c135c99bd097163a78b
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2020
ms.locfileid: "92160369"
---
# <a name="bc30269-methodname-has-multiple-definitions-with-identical-signatures"></a><span data-ttu-id="34552-102">BC30269: " \<methodname> " ma wiele definicji z identycznymi sygnaturami</span><span class="sxs-lookup"><span data-stu-id="34552-102">BC30269: '\<methodname>' has multiple definitions with identical signatures</span></span>

<span data-ttu-id="34552-103">`Function` `Sub` Deklaracja procedury lub używa identycznej nazwy procedury i listy argumentów jako poprzedniej deklaracji.</span><span class="sxs-lookup"><span data-stu-id="34552-103">A `Function` or `Sub` procedure declaration uses the identical procedure name and argument list as a previous declaration.</span></span> <span data-ttu-id="34552-104">Jedną z możliwych przyczyn jest próba przeciążenia oryginalnej procedury.</span><span class="sxs-lookup"><span data-stu-id="34552-104">One possible cause is an attempt to overload the original procedure.</span></span> <span data-ttu-id="34552-105">Przeciążone procedury muszą mieć różne listy argumentów.</span><span class="sxs-lookup"><span data-stu-id="34552-105">Overloaded procedures must have different argument lists.</span></span>

 <span data-ttu-id="34552-106">**Identyfikator błędu:** BC30269</span><span class="sxs-lookup"><span data-stu-id="34552-106">**Error ID:** BC30269</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="34552-107">Aby poprawić ten błąd</span><span class="sxs-lookup"><span data-stu-id="34552-107">To correct this error</span></span>

- <span data-ttu-id="34552-108">Zmień nazwę procedury lub listę argumentów lub Usuń zduplikowaną deklarację.</span><span class="sxs-lookup"><span data-stu-id="34552-108">Change the procedure name or the argument list, or remove the duplicate declaration.</span></span>

## <a name="see-also"></a><span data-ttu-id="34552-109">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="34552-109">See also</span></span>

- [<span data-ttu-id="34552-110">Odwołania do elementów zadeklarowanych</span><span class="sxs-lookup"><span data-stu-id="34552-110">References to Declared Elements</span></span>](../../programming-guide/language-features/declared-elements/references-to-declared-elements.md)
- [<span data-ttu-id="34552-111">Zagadnienia dotyczące przeciążania procedur</span><span class="sxs-lookup"><span data-stu-id="34552-111">Considerations in Overloading Procedures</span></span>](../../programming-guide/language-features/procedures/considerations-in-overloading-procedures.md)
