---
title: Zmienne
ms.date: 07/20/2015
helpviewer_keywords:
- variables [Visual Basic]
- values [Visual Basic], storing
ms.assetid: 4cfaa06d-4ae3-4307-897b-cf599dc24caa
ms.openlocfilehash: bd6417033a6c2626d17ad003de6c637dd1e8adaa
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/23/2020
ms.locfileid: "91080221"
---
# <a name="variables-in-visual-basic"></a><span data-ttu-id="6cd7e-102">Zmienne w Visual Basic</span><span class="sxs-lookup"><span data-stu-id="6cd7e-102">Variables in Visual Basic</span></span>

<span data-ttu-id="6cd7e-103">Często należy przechowywać wartości podczas wykonywania obliczeń z Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="6cd7e-103">You often have to store values when you perform calculations with Visual Basic.</span></span> <span data-ttu-id="6cd7e-104">Na przykład możesz chcieć obliczyć kilka wartości, porównać je i wykonywać na nich różne operacje, w zależności od wyniku porównania.</span><span class="sxs-lookup"><span data-stu-id="6cd7e-104">For example, you might want to calculate several values, compare them, and perform different operations on them, depending on the result of the comparison.</span></span> <span data-ttu-id="6cd7e-105">Należy zachować wartości, jeśli chcesz je porównać.</span><span class="sxs-lookup"><span data-stu-id="6cd7e-105">You have to retain the values if you want to compare them.</span></span>  
  
## <a name="usage"></a><span data-ttu-id="6cd7e-106">Użycie</span><span class="sxs-lookup"><span data-stu-id="6cd7e-106">Usage</span></span>  

 <span data-ttu-id="6cd7e-107">Visual Basic, podobnie jak większość języków programowania, używa zmiennych do przechowywania wartości.</span><span class="sxs-lookup"><span data-stu-id="6cd7e-107">Visual Basic, just like most programming languages, uses variables for storing values.</span></span> <span data-ttu-id="6cd7e-108">*Zmienna* ma nazwę (wyraz używany do odwoływania się do wartości, która zawiera zmienna).</span><span class="sxs-lookup"><span data-stu-id="6cd7e-108">A *variable* has a name (the word that you use to refer to the value that the variable contains).</span></span> <span data-ttu-id="6cd7e-109">Zmienna ma również typ danych (który określa rodzaj danych, które mogą być przechowywane w zmiennej).</span><span class="sxs-lookup"><span data-stu-id="6cd7e-109">A variable also has a data type (which determines the kind of data that the variable can store).</span></span> <span data-ttu-id="6cd7e-110">Zmienna może reprezentować tablicę, jeśli musi przechowywać indeksowany zestaw ściśle powiązanych elementów danych.</span><span class="sxs-lookup"><span data-stu-id="6cd7e-110">A variable can represent an array if it has to store an indexed set of closely related data items.</span></span>  
  
 <span data-ttu-id="6cd7e-111">Wnioskowanie o typie lokalnym umożliwia deklarowanie zmiennych bez jawnego określenia typu danych.</span><span class="sxs-lookup"><span data-stu-id="6cd7e-111">Local type inference enables you to declare variables without explicitly stating a data type.</span></span> <span data-ttu-id="6cd7e-112">Zamiast tego, kompilator wnioskuje typ zmiennej z typu wyrażenia inicjowania.</span><span class="sxs-lookup"><span data-stu-id="6cd7e-112">Instead, the compiler infers the type of the variable from the type of the initialization expression.</span></span> <span data-ttu-id="6cd7e-113">Aby uzyskać więcej informacji, zobacz [lokalne wnioskowanie o typie](local-type-inference.md) i [zestawienie opcji](../../../language-reference/statements/option-infer-statement.md).</span><span class="sxs-lookup"><span data-stu-id="6cd7e-113">For more information, see [Local Type Inference](local-type-inference.md) and [Option Infer Statement](../../../language-reference/statements/option-infer-statement.md).</span></span>  
  
## <a name="assigning-values"></a><span data-ttu-id="6cd7e-114">Przypisywanie wartości</span><span class="sxs-lookup"><span data-stu-id="6cd7e-114">Assigning Values</span></span>  

 <span data-ttu-id="6cd7e-115">Instrukcje przypisania służą do wykonywania obliczeń i przypisywania wyniku do zmiennej, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="6cd7e-115">You use assignment statements to perform calculations and assign the result to a variable, as the following example shows.</span></span>  
  
 [!code-vb[VbVbalrVariables#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrVariables/VB/Class1.vb#1)]  
  
> [!NOTE]
> <span data-ttu-id="6cd7e-116">Znak równości ( `=` ) w tym przykładzie jest operatorem przypisania, a nie operatorem równości.</span><span class="sxs-lookup"><span data-stu-id="6cd7e-116">The equal sign (`=`) in this example is an assignment operator, not an equality operator.</span></span> <span data-ttu-id="6cd7e-117">Wartość jest przypisana do zmiennej `applesSold` .</span><span class="sxs-lookup"><span data-stu-id="6cd7e-117">The value is being assigned to the variable `applesSold`.</span></span>  
  
 <span data-ttu-id="6cd7e-118">Aby uzyskać więcej informacji, zobacz [How to: przenoszenie danych do zmiennej i z niej](how-to-move-data-into-and-out-of-a-variable.md).</span><span class="sxs-lookup"><span data-stu-id="6cd7e-118">For more information, see [How to: Move Data Into and Out of a Variable](how-to-move-data-into-and-out-of-a-variable.md).</span></span>  
  
## <a name="variables-and-properties"></a><span data-ttu-id="6cd7e-119">Zmienne i właściwości</span><span class="sxs-lookup"><span data-stu-id="6cd7e-119">Variables and Properties</span></span>  

 <span data-ttu-id="6cd7e-120">Podobnie jak zmienna, *Właściwość* reprezentuje wartość, do której można uzyskać dostęp.</span><span class="sxs-lookup"><span data-stu-id="6cd7e-120">Like a variable, a *property* represents a value that you can access.</span></span> <span data-ttu-id="6cd7e-121">Jest to jednak bardziej złożone niż zmienna.</span><span class="sxs-lookup"><span data-stu-id="6cd7e-121">However, it is more complex than a variable.</span></span> <span data-ttu-id="6cd7e-122">Właściwość używa bloków kodu, które kontrolują sposób ustawiania i pobierania jego wartości.</span><span class="sxs-lookup"><span data-stu-id="6cd7e-122">A property uses code blocks that control how to set and retrieve its value.</span></span> <span data-ttu-id="6cd7e-123">Aby uzyskać więcej informacji, zobacz [różnice między właściwościami i zmiennymi w Visual Basic](../procedures/differences-between-properties-and-variables.md).</span><span class="sxs-lookup"><span data-stu-id="6cd7e-123">For more information, see [Differences Between Properties and Variables in Visual Basic](../procedures/differences-between-properties-and-variables.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="6cd7e-124">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="6cd7e-124">See also</span></span>

- [<span data-ttu-id="6cd7e-125">Deklaracja zmiennej</span><span class="sxs-lookup"><span data-stu-id="6cd7e-125">Variable Declaration</span></span>](variable-declaration.md)
- [<span data-ttu-id="6cd7e-126">Zmienne obiektów</span><span class="sxs-lookup"><span data-stu-id="6cd7e-126">Object Variables</span></span>](object-variables.md)
- [<span data-ttu-id="6cd7e-127">Rozwiązywanie problemów związanych ze zmiennymi</span><span class="sxs-lookup"><span data-stu-id="6cd7e-127">Troubleshooting Variables</span></span>](troubleshooting-variables.md)
- [<span data-ttu-id="6cd7e-128">Porady: przenoszenie danych do zmiennej i z niej</span><span class="sxs-lookup"><span data-stu-id="6cd7e-128">How to: Move Data Into and Out of a Variable</span></span>](how-to-move-data-into-and-out-of-a-variable.md)
- [<span data-ttu-id="6cd7e-129">Różnice pomiędzy właściwościami i zmiennymi w Visual Basic</span><span class="sxs-lookup"><span data-stu-id="6cd7e-129">Differences Between Properties and Variables in Visual Basic</span></span>](../procedures/differences-between-properties-and-variables.md)
- [<span data-ttu-id="6cd7e-130">Wnioskowanie o typie lokalnym</span><span class="sxs-lookup"><span data-stu-id="6cd7e-130">Local Type Inference</span></span>](local-type-inference.md)
