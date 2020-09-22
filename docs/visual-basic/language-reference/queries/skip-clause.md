---
title: Skip, klauzula
ms.date: 07/20/2015
f1_keywords:
- vb.QuerySkip
helpviewer_keywords:
- queries [Visual Basic], Skip
- Skip statement [Visual Basic]
- Skip clause [Visual Basic]
ms.assetid: f00eb172-3907-4c43-9745-d8546ab86234
ms.openlocfilehash: 40e89160baf663f7d6785e5d3e09ad6cc4eefbde
ms.sourcegitcommit: d2db216e46323f73b32ae312c9e4135258e5d68e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "90866308"
---
# <a name="skip-clause-visual-basic"></a><span data-ttu-id="9ec61-102">Skip — Klauzula (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="9ec61-102">Skip Clause (Visual Basic)</span></span>

<span data-ttu-id="9ec61-103">Pomija określoną liczbę elementów w kolekcji, a następnie zwraca pozostałe elementy.</span><span class="sxs-lookup"><span data-stu-id="9ec61-103">Bypasses a specified number of elements in a collection and then returns the remaining elements.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="9ec61-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="9ec61-104">Syntax</span></span>  
  
```vb  
Skip count  
```  
  
## <a name="parts"></a><span data-ttu-id="9ec61-105">Części</span><span class="sxs-lookup"><span data-stu-id="9ec61-105">Parts</span></span>  

 `count`  
 <span data-ttu-id="9ec61-106">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="9ec61-106">Required.</span></span> <span data-ttu-id="9ec61-107">Wartość lub wyrażenie, które oblicza liczbę elementów sekwencji do pominięcia.</span><span class="sxs-lookup"><span data-stu-id="9ec61-107">A value or an expression that evaluates to the number of elements of the sequence to skip.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="9ec61-108">Uwagi</span><span class="sxs-lookup"><span data-stu-id="9ec61-108">Remarks</span></span>  

 <span data-ttu-id="9ec61-109">`Skip`Klauzula powoduje, że zapytanie pomija elementy na początku listy wyników i zwróci pozostałe elementy.</span><span class="sxs-lookup"><span data-stu-id="9ec61-109">The `Skip` clause causes a query to bypass elements at the beginning of a results list and return the remaining elements.</span></span> <span data-ttu-id="9ec61-110">Liczba elementów do pominięcia jest identyfikowana przez `count` parametr.</span><span class="sxs-lookup"><span data-stu-id="9ec61-110">The number of elements to skip is identified by the `count` parameter.</span></span>  
  
 <span data-ttu-id="9ec61-111">Można użyć `Skip` klauzuli z `Take` klauzulą, aby zwrócić zakres danych z dowolnego segmentu zapytania.</span><span class="sxs-lookup"><span data-stu-id="9ec61-111">You can use the `Skip` clause with the `Take` clause to return a range of data from any segment of a query.</span></span> <span data-ttu-id="9ec61-112">Aby to zrobić, Przekaż indeks pierwszego elementu zakresu do `Skip` klauzuli i rozmiar zakresu do `Take` klauzuli.</span><span class="sxs-lookup"><span data-stu-id="9ec61-112">To do this, pass the index of the first element of the range to the `Skip` clause and the size of the range to the `Take` clause.</span></span>  
  
 <span data-ttu-id="9ec61-113">Gdy używasz `Skip` klauzuli w zapytaniu, możesz również upewnić się, że wyniki są zwracane w kolejności, która spowoduje `Skip` pominięcie zamierzonych wyników.</span><span class="sxs-lookup"><span data-stu-id="9ec61-113">When you use the `Skip` clause in a query, you may also need to ensure that the results are returned in an order that will enable the `Skip` clause to bypass the intended results.</span></span> <span data-ttu-id="9ec61-114">Aby uzyskać więcej informacji na temat porządkowania wyników zapytania, zobacz [klauzula Order by](order-by-clause.md).</span><span class="sxs-lookup"><span data-stu-id="9ec61-114">For more information about ordering query results, see [Order By Clause](order-by-clause.md).</span></span>  
  
 <span data-ttu-id="9ec61-115">Można użyć `SkipWhile` klauzuli, aby określić, że tylko niektóre elementy są ignorowane, w zależności od podanego warunku.</span><span class="sxs-lookup"><span data-stu-id="9ec61-115">You can use the `SkipWhile` clause to specify that only certain elements are ignored, depending on a supplied condition.</span></span>  
  
## <a name="example"></a><span data-ttu-id="9ec61-116">Przykład</span><span class="sxs-lookup"><span data-stu-id="9ec61-116">Example</span></span>  

 <span data-ttu-id="9ec61-117">Poniższy przykład kodu używa `Skip` klauzuli razem z `Take` klauzulą, aby zwrócić dane ze zapytania na stronach.</span><span class="sxs-lookup"><span data-stu-id="9ec61-117">The following code example uses the `Skip` clause together with the `Take` clause to return data from a query in pages.</span></span> <span data-ttu-id="9ec61-118">`GetCustomers`Funkcja używa `Skip` klauzuli do pomijania klientów na liście do momentu podanej wartości indeksu początkowego i używa `Take` klauzuli do zwrócenia strony klientów zaczynających się od tej wartości indeksu.</span><span class="sxs-lookup"><span data-stu-id="9ec61-118">The `GetCustomers` function uses the `Skip` clause to bypass the customers in the list until the supplied starting index value, and uses the `Take` clause to return a page of customers starting from that index value.</span></span>  
  
 [!code-vb[VbSimpleQuerySamples#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#1)]  
  
## <a name="see-also"></a><span data-ttu-id="9ec61-119">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="9ec61-119">See also</span></span>

- [<span data-ttu-id="9ec61-120">Wprowadzenie do LINQ w Visual Basic</span><span class="sxs-lookup"><span data-stu-id="9ec61-120">Introduction to LINQ in Visual Basic</span></span>](../../programming-guide/language-features/linq/introduction-to-linq.md)
- [<span data-ttu-id="9ec61-121">Zapytania</span><span class="sxs-lookup"><span data-stu-id="9ec61-121">Queries</span></span>](index.md)
- [<span data-ttu-id="9ec61-122">SELECT — klauzula</span><span class="sxs-lookup"><span data-stu-id="9ec61-122">Select Clause</span></span>](select-clause.md)
- [<span data-ttu-id="9ec61-123">Klauzula from</span><span class="sxs-lookup"><span data-stu-id="9ec61-123">From Clause</span></span>](from-clause.md)
- [<span data-ttu-id="9ec61-124">Klauzula Order by</span><span class="sxs-lookup"><span data-stu-id="9ec61-124">Order By Clause</span></span>](order-by-clause.md)
- [<span data-ttu-id="9ec61-125">Skip While, klauzula</span><span class="sxs-lookup"><span data-stu-id="9ec61-125">Skip While Clause</span></span>](skip-while-clause.md)
- [<span data-ttu-id="9ec61-126">Take, klauzula</span><span class="sxs-lookup"><span data-stu-id="9ec61-126">Take Clause</span></span>](take-clause.md)
