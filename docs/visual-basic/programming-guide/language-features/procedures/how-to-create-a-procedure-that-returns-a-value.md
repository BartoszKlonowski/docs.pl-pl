---
title: 'Porady: tworzenie procedury, która zwraca wartość'
ms.date: 07/20/2015
helpviewer_keywords:
- procedures [Visual Basic], defining
- Visual Basic code, procedures
- procedures [Visual Basic], returning a value
ms.assetid: 8ee19f95-a9ef-4033-963b-d224dca207c4
ms.openlocfilehash: 3d28162d2a2103477a20b08fc03c937de8b5a475
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/23/2020
ms.locfileid: "91071875"
---
# <a name="how-to-create-a-procedure-that-returns-a-value-visual-basic"></a><span data-ttu-id="12816-102">Porady: tworzenie procedury, która zwraca wartość (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="12816-102">How to: Create a Procedure that Returns a Value (Visual Basic)</span></span>

<span data-ttu-id="12816-103">Używasz `Function` procedury do zwrócenia wartości do kodu wywołującego.</span><span class="sxs-lookup"><span data-stu-id="12816-103">You use a `Function` procedure to return a value to the calling code.</span></span>  
  
### <a name="to-create-a-procedure-that-returns-a-value"></a><span data-ttu-id="12816-104">Aby utworzyć procedurę zwracającą wartość</span><span class="sxs-lookup"><span data-stu-id="12816-104">To create a procedure that returns a value</span></span>  
  
1. <span data-ttu-id="12816-105">Poza inną procedurą Użyj `Function` instrukcji, a po niej `End Function` instrukcji.</span><span class="sxs-lookup"><span data-stu-id="12816-105">Outside any other procedure, use a `Function` statement, followed by an `End Function` statement.</span></span>  
  
2. <span data-ttu-id="12816-106">W `Function` instrukcji wykonaj `Function` słowo kluczowe z nazwą procedury, a następnie listę parametrów w nawiasach.</span><span class="sxs-lookup"><span data-stu-id="12816-106">In the `Function` statement, follow the `Function` keyword with the name of the procedure, and then the parameter list in parentheses.</span></span>  
  
3. <span data-ttu-id="12816-107">Użyj nawiasów z `As` klauzulą, aby określić typ danych zwracanej wartości.</span><span class="sxs-lookup"><span data-stu-id="12816-107">Follow the parentheses with an `As` clause to specify the data type of the returned value.</span></span>  
  
4. <span data-ttu-id="12816-108">Umieść instrukcje kodu procedury między `Function` `End Function` instrukcjami i.</span><span class="sxs-lookup"><span data-stu-id="12816-108">Place the procedure's code statements between the `Function` and `End Function` statements.</span></span>  
  
5. <span data-ttu-id="12816-109">Użyj `Return` instrukcji, aby zwrócić wartość do kodu wywołującego.</span><span class="sxs-lookup"><span data-stu-id="12816-109">Use a `Return` statement to return the value to the calling code.</span></span>  
  
     <span data-ttu-id="12816-110">Poniższa `Function` procedura oblicza najdłuższy Trójkąt lub przeciwprostokątnej, z prawej strony, z uwzględnieniem wartości pozostałych dwóch stron.</span><span class="sxs-lookup"><span data-stu-id="12816-110">The following `Function` procedure calculates the longest side, or hypotenuse, of a right triangle, given the values for the other two sides.</span></span>  
  
     [!code-vb[VbVbcnProcedures#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#1)]  
  
     <span data-ttu-id="12816-111">Poniższy przykład przedstawia typowe wywołanie `hypotenuse` .</span><span class="sxs-lookup"><span data-stu-id="12816-111">The following example shows a typical call to `hypotenuse`.</span></span>  
  
     [!code-vb[VbVbcnProcedures#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#6)]  
  
## <a name="see-also"></a><span data-ttu-id="12816-112">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="12816-112">See also</span></span>

- [<span data-ttu-id="12816-113">Procedury</span><span class="sxs-lookup"><span data-stu-id="12816-113">Procedures</span></span>](./index.md)
- [<span data-ttu-id="12816-114">Sub, procedury</span><span class="sxs-lookup"><span data-stu-id="12816-114">Sub Procedures</span></span>](./sub-procedures.md)
- [<span data-ttu-id="12816-115">Procedury własności</span><span class="sxs-lookup"><span data-stu-id="12816-115">Property Procedures</span></span>](./property-procedures.md)
- [<span data-ttu-id="12816-116">Procedury operatorów</span><span class="sxs-lookup"><span data-stu-id="12816-116">Operator Procedures</span></span>](./operator-procedures.md)
- [<span data-ttu-id="12816-117">Parametry i argumenty procedur</span><span class="sxs-lookup"><span data-stu-id="12816-117">Procedure Parameters and Arguments</span></span>](./procedure-parameters-and-arguments.md)
- [<span data-ttu-id="12816-118">Function, instrukcja</span><span class="sxs-lookup"><span data-stu-id="12816-118">Function Statement</span></span>](../../../language-reference/statements/function-statement.md)
- [<span data-ttu-id="12816-119">Porady: zwracanie wartości z procedury</span><span class="sxs-lookup"><span data-stu-id="12816-119">How to: Return a Value from a Procedure</span></span>](./how-to-return-a-value-from-a-procedure.md)
- [<span data-ttu-id="12816-120">Instrukcje: wywoływanie procedury zwracającej wartość</span><span class="sxs-lookup"><span data-stu-id="12816-120">How to: Call a Procedure That Returns a Value</span></span>](./how-to-call-a-procedure-that-returns-a-value.md)
