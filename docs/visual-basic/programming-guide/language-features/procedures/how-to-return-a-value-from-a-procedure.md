---
title: 'Porady: zwracanie wartości z procedury'
ms.date: 07/20/2015
helpviewer_keywords:
- Visual Basic code, procedures
- procedures [Visual Basic], returning from
- procedures [Visual Basic], returning a value
ms.assetid: 4bcc4724-2b4e-4df8-9b4b-16054607f87d
ms.openlocfilehash: cbc785a07aa8a7b299508a093e08d5d0510b838a
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/23/2020
ms.locfileid: "91071381"
---
# <a name="how-to-return-a-value-from-a-procedure-visual-basic"></a><span data-ttu-id="3eeb0-102">Porady: zwracanie wartości z procedury (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="3eeb0-102">How to: Return a Value from a Procedure (Visual Basic)</span></span>

<span data-ttu-id="3eeb0-103">`Function`Procedura zwraca wartość do wywołującego kodu przez wykonanie `Return` instrukcji lub przez napotkanie `Exit Function` `End Function` instrukcji or.</span><span class="sxs-lookup"><span data-stu-id="3eeb0-103">A `Function` procedure returns a value to the calling code either by executing a `Return` statement or by encountering an `Exit Function` or `End Function` statement.</span></span>  
  
### <a name="to-return-a-value-using-the-return-statement"></a><span data-ttu-id="3eeb0-104">Aby zwrócić wartość przy użyciu instrukcji return</span><span class="sxs-lookup"><span data-stu-id="3eeb0-104">To return a value using the Return statement</span></span>  
  
1. <span data-ttu-id="3eeb0-105">Umieść `Return` instrukcję w punkcie, w którym wykonano zadanie procedury.</span><span class="sxs-lookup"><span data-stu-id="3eeb0-105">Put a `Return` statement at the point where the procedure's task is completed.</span></span>  
  
2. <span data-ttu-id="3eeb0-106">Użyj `Return` słowa kluczowego z wyrażeniem, które zwraca wartość, która ma zostać zwrócona do kodu wywołującego.</span><span class="sxs-lookup"><span data-stu-id="3eeb0-106">Follow the `Return` keyword with an expression that yields the value you want to return to the calling code.</span></span>  
  
3. <span data-ttu-id="3eeb0-107">W tej samej procedurze można mieć więcej niż jedną `Return` instrukcję.</span><span class="sxs-lookup"><span data-stu-id="3eeb0-107">You can have more than one `Return` statement in the same procedure.</span></span>  
  
     <span data-ttu-id="3eeb0-108">Poniższa `Function` procedura oblicza dłuższy Trójkąt lub przeciwprostokątnej, z prawej strony i zwraca go do kodu wywołującego.</span><span class="sxs-lookup"><span data-stu-id="3eeb0-108">The following `Function` procedure calculates the longest side, or hypotenuse, of a right triangle, and returns it to the calling code.</span></span>  
  
     [!code-vb[VbVbcnProcedures#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#1)]  
  
     <span data-ttu-id="3eeb0-109">Poniższy przykład przedstawia typowe wywołanie do `hypotenuse` , które przechowuje zwracaną wartość.</span><span class="sxs-lookup"><span data-stu-id="3eeb0-109">The following example shows a typical call to `hypotenuse`, which stores the returned value.</span></span>  
  
     [!code-vb[VbVbcnProcedures#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#6)]  
  
### <a name="to-return-a-value-using-exit-function-or-end-function"></a><span data-ttu-id="3eeb0-110">Aby zwrócić wartość przy użyciu funkcji Exit lub End Function</span><span class="sxs-lookup"><span data-stu-id="3eeb0-110">To return a value using Exit Function or End Function</span></span>  
  
1. <span data-ttu-id="3eeb0-111">W co najmniej jednym miejscu w `Function` procedurze Przypisz wartość do nazwy procedury.</span><span class="sxs-lookup"><span data-stu-id="3eeb0-111">In at least one place in the `Function` procedure, assign a value to the procedure's name.</span></span>  
  
2. <span data-ttu-id="3eeb0-112">Podczas wykonywania `Exit Function` `End Function` instrukcji lub Visual Basic zwraca wartość ostatnio przypisaną do nazwy procedury.</span><span class="sxs-lookup"><span data-stu-id="3eeb0-112">When you execute an `Exit Function` or `End Function` statement, Visual Basic returns the value most recently assigned to the procedure's name.</span></span>  
  
3. <span data-ttu-id="3eeb0-113">Można mieć więcej niż jedną `Exit Function` instrukcję w tej samej procedurze i można mieszać `Return` i `Exit Function` wypełniać instrukcje w tej samej procedurze.</span><span class="sxs-lookup"><span data-stu-id="3eeb0-113">You can have more than one `Exit Function` statement in the same procedure, and you can mix `Return` and `Exit Function` statements in the same procedure.</span></span>  
  
4. <span data-ttu-id="3eeb0-114">W procedurze można mieć tylko jedną `End Function` instrukcję `Function` .</span><span class="sxs-lookup"><span data-stu-id="3eeb0-114">You can have only one `End Function` statement in a `Function` procedure.</span></span>  
  
     <span data-ttu-id="3eeb0-115">Aby uzyskać więcej informacji i zapoznać się z przykładem, zobacz "wartość zwracana" w [instrukcji funkcji](../../../language-reference/statements/function-statement.md).</span><span class="sxs-lookup"><span data-stu-id="3eeb0-115">For more information and an example, see "Return Value" in [Function Statement](../../../language-reference/statements/function-statement.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="3eeb0-116">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="3eeb0-116">See also</span></span>

- [<span data-ttu-id="3eeb0-117">Procedury</span><span class="sxs-lookup"><span data-stu-id="3eeb0-117">Procedures</span></span>](./index.md)
- [<span data-ttu-id="3eeb0-118">Sub, procedury</span><span class="sxs-lookup"><span data-stu-id="3eeb0-118">Sub Procedures</span></span>](./sub-procedures.md)
- [<span data-ttu-id="3eeb0-119">Procedury własności</span><span class="sxs-lookup"><span data-stu-id="3eeb0-119">Property Procedures</span></span>](./property-procedures.md)
- [<span data-ttu-id="3eeb0-120">Procedury operatorów</span><span class="sxs-lookup"><span data-stu-id="3eeb0-120">Operator Procedures</span></span>](./operator-procedures.md)
- [<span data-ttu-id="3eeb0-121">Parametry i argumenty procedur</span><span class="sxs-lookup"><span data-stu-id="3eeb0-121">Procedure Parameters and Arguments</span></span>](./procedure-parameters-and-arguments.md)
- [<span data-ttu-id="3eeb0-122">Function, instrukcja</span><span class="sxs-lookup"><span data-stu-id="3eeb0-122">Function Statement</span></span>](../../../language-reference/statements/function-statement.md)
- [<span data-ttu-id="3eeb0-123">Return, instrukcja</span><span class="sxs-lookup"><span data-stu-id="3eeb0-123">Return Statement</span></span>](../../../language-reference/statements/return-statement.md)
- [<span data-ttu-id="3eeb0-124">Instrukcje: tworzenie procedury, która zwraca wartość</span><span class="sxs-lookup"><span data-stu-id="3eeb0-124">How to: Create a Procedure that Returns a Value</span></span>](./how-to-create-a-procedure-that-returns-a-value.md)
- [<span data-ttu-id="3eeb0-125">Instrukcje: wywoływanie procedury zwracającej wartość</span><span class="sxs-lookup"><span data-stu-id="3eeb0-125">How to: Call a Procedure That Returns a Value</span></span>](./how-to-call-a-procedure-that-returns-a-value.md)
