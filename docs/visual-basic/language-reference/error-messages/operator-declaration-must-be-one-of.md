---
title: 'Deklaracja operatora musi być jednym z: +,-, *,-,-, ^, &amp; , like, mod, and, or, XOR, not,  <<,  >>, =,  <>, <, <=, >, >=, CType, IsTrue, IsFalse'
ms.date: 07/20/2015
f1_keywords:
- bc33000
- vbc33000
helpviewer_keywords:
- BC33000
ms.assetid: 15c5d8eb-3a8c-4141-8f41-33151afabf97
ms.openlocfilehash: c388b1b0762dd7475ca365a8a62228d0b5d59414
ms.sourcegitcommit: d2db216e46323f73b32ae312c9e4135258e5d68e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "90873615"
---
# <a name="operator-declaration-must-be-one-of----amp-like-mod-and-or-xor-not--"></a><span data-ttu-id="285fe-102">Deklaracja operatora musi być jedną z: +,-, \*, \, /, ^, &amp; , like, mod, and, or, XOR, not, \<\<, >>...</span><span class="sxs-lookup"><span data-stu-id="285fe-102">Operator declaration must be one of:  +,-,\*,\,/,^, &amp;, Like, Mod, And, Or, Xor, Not, \<\<, >>...</span></span>

<span data-ttu-id="285fe-103">Można zadeklarować tylko operatora, który kwalifikuje się do przeciążenia.</span><span class="sxs-lookup"><span data-stu-id="285fe-103">You can declare only an operator that is eligible for overloading.</span></span> <span data-ttu-id="285fe-104">W poniższej tabeli wymieniono operatory, które można zadeklarować.</span><span class="sxs-lookup"><span data-stu-id="285fe-104">The following table lists the operators you can declare.</span></span>  
  
|<span data-ttu-id="285fe-105">Typ</span><span class="sxs-lookup"><span data-stu-id="285fe-105">Type</span></span>|<span data-ttu-id="285fe-106">Operatory</span><span class="sxs-lookup"><span data-stu-id="285fe-106">Operators</span></span>|  
|----------|---------------|  
|<span data-ttu-id="285fe-107">Jednoargumentowy</span><span class="sxs-lookup"><span data-stu-id="285fe-107">Unary</span></span>|<span data-ttu-id="285fe-108">`+`, `-`, `IsFalse`, `IsTrue`, `Not`</span><span class="sxs-lookup"><span data-stu-id="285fe-108">`+`, `-`, `IsFalse`, `IsTrue`, `Not`</span></span>|  
|<span data-ttu-id="285fe-109">Binarne</span><span class="sxs-lookup"><span data-stu-id="285fe-109">Binary</span></span>|<span data-ttu-id="285fe-110">`+`, `-`, `*`, `/`, `\`, `&`, `^`, `>>`, `<<`, `=`, `<>`, `>`, `>=`, `<`, `<=`, `And`, `Like`, `Mod`, `Or`, `Xor`</span><span class="sxs-lookup"><span data-stu-id="285fe-110">`+`, `-`, `*`, `/`, `\`, `&`, `^`, `>>`, `<<`, `=`, `<>`, `>`, `>=`, `<`, `<=`, `And`, `Like`, `Mod`, `Or`, `Xor`</span></span>|  
|<span data-ttu-id="285fe-111">Konwersja (Jednoargumentowa)</span><span class="sxs-lookup"><span data-stu-id="285fe-111">Conversion (unary)</span></span>|`CType`|  
  
 <span data-ttu-id="285fe-112">Należy zauważyć, że `=` operator na liście Binary jest operatorem porównania, a nie operatorem przypisania.</span><span class="sxs-lookup"><span data-stu-id="285fe-112">Note that the `=` operator in the binary list is the comparison operator, not the assignment operator.</span></span>  
  
 <span data-ttu-id="285fe-113">**Identyfikator błędu:** BC33000</span><span class="sxs-lookup"><span data-stu-id="285fe-113">**Error ID:** BC33000</span></span>  
  
## <a name="to-correct-this-error"></a><span data-ttu-id="285fe-114">Aby poprawić ten błąd</span><span class="sxs-lookup"><span data-stu-id="285fe-114">To correct this error</span></span>  
  
1. <span data-ttu-id="285fe-115">Wybierz operator z zestawu operatorów z możliwością przeciążenia.</span><span class="sxs-lookup"><span data-stu-id="285fe-115">Select an operator from the set of overloadable operators.</span></span>  
  
2. <span data-ttu-id="285fe-116">Jeśli potrzebujesz funkcji przeciążania operatora, którego nie można przeciążyć bezpośrednio, Utwórz `Function` procedurę, która przyjmuje odpowiednie parametry i zwraca odpowiednią wartość.</span><span class="sxs-lookup"><span data-stu-id="285fe-116">If you need the functionality of overloading an operator that you cannot overload directly, create a `Function` procedure that takes the appropriate parameters and returns the appropriate value.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="285fe-117">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="285fe-117">See also</span></span>

- [<span data-ttu-id="285fe-118">Operator — Instrukcja</span><span class="sxs-lookup"><span data-stu-id="285fe-118">Operator Statement</span></span>](../statements/operator-statement.md)
- [<span data-ttu-id="285fe-119">Procedury operatorów</span><span class="sxs-lookup"><span data-stu-id="285fe-119">Operator Procedures</span></span>](../../programming-guide/language-features/procedures/operator-procedures.md)
- [<span data-ttu-id="285fe-120">Instrukcje: definiowanie operatora</span><span class="sxs-lookup"><span data-stu-id="285fe-120">How to: Define an Operator</span></span>](../../programming-guide/language-features/procedures/how-to-define-an-operator.md)
- [<span data-ttu-id="285fe-121">Instrukcje: definiowanie operatora konwersji</span><span class="sxs-lookup"><span data-stu-id="285fe-121">How to: Define a Conversion Operator</span></span>](../../programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)
- [<span data-ttu-id="285fe-122">Function, instrukcja</span><span class="sxs-lookup"><span data-stu-id="285fe-122">Function Statement</span></span>](../statements/function-statement.md)
