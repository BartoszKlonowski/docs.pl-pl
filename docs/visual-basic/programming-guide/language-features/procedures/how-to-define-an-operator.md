---
title: 'Porady: definiowanie operatora'
ms.date: 07/20/2015
helpviewer_keywords:
- procedures [Visual Basic], defining
- Visual Basic code, procedures
- operators [Visual Basic], defining
- procedures [Visual Basic], operator
- Visual Basic code, operators
- syntax [Visual Basic], Operator procedures
- operators [Visual Basic], overloading
- operator procedures [Visual Basic], about operator procedures
- return values [Visual Basic], Operator procedures
- operator overloading
ms.assetid: d4b0e253-092a-4e6e-9fe2-01f562140a29
ms.openlocfilehash: 5acbd0439ddbb956b80d56e23d11cd5e152f37ff
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/23/2020
ms.locfileid: "91087404"
---
# <a name="how-to-define-an-operator-visual-basic"></a><span data-ttu-id="77122-102">Porady: definiowanie operatora (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="77122-102">How to: Define an Operator (Visual Basic)</span></span>

<span data-ttu-id="77122-103">Jeśli zdefiniowano klasę lub strukturę, można zdefiniować zachowanie operatora standardowego (na przykład `*` , `<>` lub `And` ), gdy jeden lub oba operandy są typu klasy lub struktury.</span><span class="sxs-lookup"><span data-stu-id="77122-103">If you have defined a class or structure, you can define the behavior of a standard operator (such as `*`, `<>`, or `And`) when one or both of the operands is of the type of your class or structure.</span></span>  
  
 <span data-ttu-id="77122-104">Zdefiniuj operatora standardowego jako procedurę operatora w klasie lub strukturze.</span><span class="sxs-lookup"><span data-stu-id="77122-104">Define the standard operator as an operator procedure within the class or structure.</span></span> <span data-ttu-id="77122-105">Wszystkie procedury operatora muszą być `Public` `Shared` .</span><span class="sxs-lookup"><span data-stu-id="77122-105">All operator procedures must be `Public` `Shared`.</span></span>  
  
 <span data-ttu-id="77122-106">Definiowanie operatora w klasie lub strukturze jest również nazywane *przeciążeniem* operatora.</span><span class="sxs-lookup"><span data-stu-id="77122-106">Defining an operator on a class or structure is also called *overloading* the operator.</span></span>  
  
## <a name="example"></a><span data-ttu-id="77122-107">Przykład</span><span class="sxs-lookup"><span data-stu-id="77122-107">Example</span></span>  

 <span data-ttu-id="77122-108">W poniższym przykładzie zdefiniowano `+` operatora dla struktury o nazwie `height` .</span><span class="sxs-lookup"><span data-stu-id="77122-108">The following example defines the `+` operator for a structure called `height`.</span></span> <span data-ttu-id="77122-109">Struktura używa wysokości mierzona w metrach i calach.</span><span class="sxs-lookup"><span data-stu-id="77122-109">The structure uses heights measured in feet and inches.</span></span> <span data-ttu-id="77122-110">1 *cal* wynosi 2,54 centymetrów, *a jedna z* nich jest 12 cali.</span><span class="sxs-lookup"><span data-stu-id="77122-110">One *inch* is 2.54 centimeters, and one *foot* is 12 inches.</span></span> <span data-ttu-id="77122-111">Aby zapewnić znormalizowaną wartość (w calach < 12,0), Konstruktor wykonuje *modulo* 12.</span><span class="sxs-lookup"><span data-stu-id="77122-111">To ensure normalized values (inches < 12.0), the constructor performs *modulo* 12 arithmetic.</span></span> <span data-ttu-id="77122-112">`+`Operator używa konstruktora do generowania znormalizowanych wartości.</span><span class="sxs-lookup"><span data-stu-id="77122-112">The `+` operator uses the constructor to generate normalized values.</span></span>  
  
 [!code-vb[VbVbcnProcedures#25](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#25)]  
  
 <span data-ttu-id="77122-113">Możesz przetestować strukturę `height` przy użyciu następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="77122-113">You can test the structure `height` with the following code.</span></span>  
  
 [!code-vb[VbVbcnProcedures#26](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#26)]  

## <a name="see-also"></a><span data-ttu-id="77122-114">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="77122-114">See also</span></span>

- [<span data-ttu-id="77122-115">Procedury operatorów</span><span class="sxs-lookup"><span data-stu-id="77122-115">Operator Procedures</span></span>](./operator-procedures.md)
- [<span data-ttu-id="77122-116">Instrukcje: definiowanie operatora konwersji</span><span class="sxs-lookup"><span data-stu-id="77122-116">How to: Define a Conversion Operator</span></span>](./how-to-define-a-conversion-operator.md)
- [<span data-ttu-id="77122-117">Instrukcje: wywoływanie procedury operatora</span><span class="sxs-lookup"><span data-stu-id="77122-117">How to: Call an Operator Procedure</span></span>](./how-to-call-an-operator-procedure.md)
- [<span data-ttu-id="77122-118">Instrukcje: używanie klasy definiującej operatory</span><span class="sxs-lookup"><span data-stu-id="77122-118">How to: Use a Class that Defines Operators</span></span>](./how-to-use-a-class-that-defines-operators.md)
- [<span data-ttu-id="77122-119">Operator — Instrukcja</span><span class="sxs-lookup"><span data-stu-id="77122-119">Operator Statement</span></span>](../../../language-reference/statements/operator-statement.md)
- [<span data-ttu-id="77122-120">Structure — Instrukcja</span><span class="sxs-lookup"><span data-stu-id="77122-120">Structure Statement</span></span>](../../../language-reference/statements/structure-statement.md)
- [<span data-ttu-id="77122-121">Instrukcje: Deklarowanie struktury</span><span class="sxs-lookup"><span data-stu-id="77122-121">How to: Declare a Structure</span></span>](../data-types/how-to-declare-a-structure.md)
- [<span data-ttu-id="77122-122">Mod — Operator</span><span class="sxs-lookup"><span data-stu-id="77122-122">Mod Operator</span></span>](../../../language-reference/operators/mod-operator.md)
