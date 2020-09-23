---
title: Operacje agregacji
ms.date: 07/20/2015
ms.assetid: 0f47e92c-5dd2-4007-baf4-c5fe5dc3b4a8
ms.openlocfilehash: 1cf82d8acfdb1f8b0fc33c324064574b0dd01f4a
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/23/2020
ms.locfileid: "91078401"
---
# <a name="aggregation-operations-visual-basic"></a><span data-ttu-id="9a3eb-102">Operacje agregacji (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="9a3eb-102">Aggregation Operations (Visual Basic)</span></span>

<span data-ttu-id="9a3eb-103">Operacja agregacji oblicza pojedynczą wartość z kolekcji wartości.</span><span class="sxs-lookup"><span data-stu-id="9a3eb-103">An aggregation operation computes a single value from a collection of values.</span></span> <span data-ttu-id="9a3eb-104">Przykład operacji agregacji oblicza średnią dzienną temperaturę od miesięcznej wartości dziennej temperatury.</span><span class="sxs-lookup"><span data-stu-id="9a3eb-104">An example of an aggregation operation is calculating the average daily temperature from a month's worth of daily temperature values.</span></span>  
  
 <span data-ttu-id="9a3eb-105">Na poniższej ilustracji przedstawiono wyniki dwóch różnych operacji agregacji w sekwencji liczb.</span><span class="sxs-lookup"><span data-stu-id="9a3eb-105">The following illustration shows the results of two different aggregation operations on a sequence of numbers.</span></span> <span data-ttu-id="9a3eb-106">Pierwsza operacja sumuje liczby.</span><span class="sxs-lookup"><span data-stu-id="9a3eb-106">The first operation sums the numbers.</span></span> <span data-ttu-id="9a3eb-107">Druga operacja zwraca maksymalną wartość w sekwencji.</span><span class="sxs-lookup"><span data-stu-id="9a3eb-107">The second operation returns the maximum value in the sequence.</span></span>  
  
 ![Ilustracja przedstawiająca operacje agregacji LINQ.](./media/aggregation-operations/linq-aggregation-operations.png)  
  
 <span data-ttu-id="9a3eb-109">W poniższej sekcji przedstawiono standardowe metody operatorów zapytań, które wykonują operacje agregacji.</span><span class="sxs-lookup"><span data-stu-id="9a3eb-109">The standard query operator methods that perform aggregation operations are listed in the following section.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="9a3eb-110">Metody</span><span class="sxs-lookup"><span data-stu-id="9a3eb-110">Methods</span></span>  
  
|<span data-ttu-id="9a3eb-111">Nazwa metody</span><span class="sxs-lookup"><span data-stu-id="9a3eb-111">Method Name</span></span>|<span data-ttu-id="9a3eb-112">Opis</span><span class="sxs-lookup"><span data-stu-id="9a3eb-112">Description</span></span>|<span data-ttu-id="9a3eb-113">Składnia wyrażenia zapytania Visual Basic</span><span class="sxs-lookup"><span data-stu-id="9a3eb-113">Visual Basic Query Expression Syntax</span></span>|<span data-ttu-id="9a3eb-114">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="9a3eb-114">More Information</span></span>|  
|-----------------|-----------------|------------------------------------------|----------------------|  
|<span data-ttu-id="9a3eb-115">Agregacja</span><span class="sxs-lookup"><span data-stu-id="9a3eb-115">Aggregate</span></span>|<span data-ttu-id="9a3eb-116">Wykonuje niestandardową operację agregacji na wartościach kolekcji.</span><span class="sxs-lookup"><span data-stu-id="9a3eb-116">Performs a custom aggregation operation on the values of a collection.</span></span>|<span data-ttu-id="9a3eb-117">Nie dotyczy.</span><span class="sxs-lookup"><span data-stu-id="9a3eb-117">Not applicable.</span></span>|<xref:System.Linq.Enumerable.Aggregate%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.Aggregate%2A?displayProperty=nameWithType>|  
|<span data-ttu-id="9a3eb-118">Średnia</span><span class="sxs-lookup"><span data-stu-id="9a3eb-118">Average</span></span>|<span data-ttu-id="9a3eb-119">Oblicza średnią wartość kolekcji wartości.</span><span class="sxs-lookup"><span data-stu-id="9a3eb-119">Calculates the average value of a collection of values.</span></span>|`Aggregate … In … Into Average()`|<xref:System.Linq.Enumerable.Average%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.Average%2A?displayProperty=nameWithType>|  
|<span data-ttu-id="9a3eb-120">Liczba</span><span class="sxs-lookup"><span data-stu-id="9a3eb-120">Count</span></span>|<span data-ttu-id="9a3eb-121">Zlicza elementy w kolekcji, opcjonalnie tylko te elementy, które spełniają funkcję predykatu.</span><span class="sxs-lookup"><span data-stu-id="9a3eb-121">Counts the elements in a collection, optionally only those elements that satisfy a predicate function.</span></span>|`Aggregate … In … Into Count()`|<xref:System.Linq.Enumerable.Count%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.Count%2A?displayProperty=nameWithType>|  
|<span data-ttu-id="9a3eb-122">LongCount</span><span class="sxs-lookup"><span data-stu-id="9a3eb-122">LongCount</span></span>|<span data-ttu-id="9a3eb-123">Zlicza elementy w dużej kolekcji, opcjonalnie tylko te elementy, które spełniają funkcję predykatu.</span><span class="sxs-lookup"><span data-stu-id="9a3eb-123">Counts the elements in a large collection, optionally only those elements that satisfy a predicate function.</span></span>|`Aggregate … In … Into LongCount()`|<xref:System.Linq.Enumerable.LongCount%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.LongCount%2A?displayProperty=nameWithType>|  
|<span data-ttu-id="9a3eb-124">Maks.</span><span class="sxs-lookup"><span data-stu-id="9a3eb-124">Max</span></span>|<span data-ttu-id="9a3eb-125">Określa maksymalną wartość w kolekcji.</span><span class="sxs-lookup"><span data-stu-id="9a3eb-125">Determines the maximum value in a collection.</span></span>|`Aggregate … In … Into Max()`|<xref:System.Linq.Enumerable.Max%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.Max%2A?displayProperty=nameWithType>|  
|<span data-ttu-id="9a3eb-126">Min.</span><span class="sxs-lookup"><span data-stu-id="9a3eb-126">Min</span></span>|<span data-ttu-id="9a3eb-127">Określa minimalną wartość w kolekcji.</span><span class="sxs-lookup"><span data-stu-id="9a3eb-127">Determines the minimum value in a collection.</span></span>|`Aggregate … In … Into Min()`|<xref:System.Linq.Enumerable.Min%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.Min%2A?displayProperty=nameWithType>|  
|<span data-ttu-id="9a3eb-128">Suma</span><span class="sxs-lookup"><span data-stu-id="9a3eb-128">Sum</span></span>|<span data-ttu-id="9a3eb-129">Oblicza sumę wartości w kolekcji.</span><span class="sxs-lookup"><span data-stu-id="9a3eb-129">Calculates the sum of the values in a collection.</span></span>|`Aggregate … In … Into Sum()`|<xref:System.Linq.Enumerable.Sum%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.Sum%2A?displayProperty=nameWithType>|  
  
## <a name="query-expression-syntax-examples"></a><span data-ttu-id="9a3eb-130">Przykłady składni wyrażeń zapytania</span><span class="sxs-lookup"><span data-stu-id="9a3eb-130">Query Expression Syntax Examples</span></span>  
  
### <a name="average"></a><span data-ttu-id="9a3eb-131">Średnia</span><span class="sxs-lookup"><span data-stu-id="9a3eb-131">Average</span></span>  

 <span data-ttu-id="9a3eb-132">Poniższy przykład kodu używa `Aggregate Into Average` klauzuli w Visual Basic, aby obliczyć średnią temperaturę w tablicy liczb reprezentujących temperatury.</span><span class="sxs-lookup"><span data-stu-id="9a3eb-132">The following code example uses the `Aggregate Into Average` clause in Visual Basic to calculate the average temperature in an array of numbers that represent temperatures.</span></span>  
  
 [!code-vb[CsLINQAggregating#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/CsLINQAggregating/VB/Aggregating.vb#1)]  
  
### <a name="count"></a><span data-ttu-id="9a3eb-133">Liczba</span><span class="sxs-lookup"><span data-stu-id="9a3eb-133">Count</span></span>  

 <span data-ttu-id="9a3eb-134">Poniższy przykład kodu używa `Aggregate Into Count` klauzuli w Visual Basic, aby policzyć liczbę wartości w tablicy, która jest większa lub równa 80.</span><span class="sxs-lookup"><span data-stu-id="9a3eb-134">The following code example uses the `Aggregate Into Count` clause in Visual Basic to count the number of values in an array that are greater than or equal to 80.</span></span>  
  
 [!code-vb[CsLINQAggregating#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/CsLINQAggregating/VB/Aggregating.vb#2)]  
  
### <a name="longcount"></a><span data-ttu-id="9a3eb-135">LongCount</span><span class="sxs-lookup"><span data-stu-id="9a3eb-135">LongCount</span></span>  

 <span data-ttu-id="9a3eb-136">Poniższy przykład kodu używa klauzuli, `Aggregate Into LongCount` aby policzyć liczbę wartości w tablicy.</span><span class="sxs-lookup"><span data-stu-id="9a3eb-136">The following code example uses the `Aggregate Into LongCount` clause to count the number of values in an array.</span></span>  
  
 [!code-vb[CsLINQAggregating#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/CsLINQAggregating/VB/Aggregating.vb#3)]  
  
### <a name="max"></a><span data-ttu-id="9a3eb-137">Maks.</span><span class="sxs-lookup"><span data-stu-id="9a3eb-137">Max</span></span>  

 <span data-ttu-id="9a3eb-138">Poniższy przykład kodu używa klauzuli, `Aggregate Into Max` Aby obliczyć maksymalną temperaturę w tablicy liczb reprezentujących temperatury.</span><span class="sxs-lookup"><span data-stu-id="9a3eb-138">The following code example uses the `Aggregate Into Max` clause  to calculate the maximum temperature in an array of numbers that represent temperatures.</span></span>  
  
 [!code-vb[CsLINQAggregating#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/CsLINQAggregating/VB/Aggregating.vb#4)]  
  
### <a name="min"></a><span data-ttu-id="9a3eb-139">Min.</span><span class="sxs-lookup"><span data-stu-id="9a3eb-139">Min</span></span>  

 <span data-ttu-id="9a3eb-140">Poniższy przykład kodu używa klauzuli, `Aggregate Into Min` Aby obliczyć minimalną temperaturę w tablicy liczb reprezentujących temperatury.</span><span class="sxs-lookup"><span data-stu-id="9a3eb-140">The following code example uses the `Aggregate Into Min` clause  to calculate the minimum temperature in an array of numbers that represent temperatures.</span></span>  
  
 [!code-vb[CsLINQAggregating#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/CsLINQAggregating/VB/Aggregating.vb#5)]  
  
### <a name="sum"></a><span data-ttu-id="9a3eb-141">Suma</span><span class="sxs-lookup"><span data-stu-id="9a3eb-141">Sum</span></span>  

 <span data-ttu-id="9a3eb-142">Poniższy przykład kodu używa klauzuli, `Aggregate Into Sum` Aby obliczyć łączną kwotę wydatków z tablicy wartości, która reprezentuje wydatki.</span><span class="sxs-lookup"><span data-stu-id="9a3eb-142">The following code example uses the `Aggregate Into Sum` clause  to calculate the total expense amount from an array of values that represent expenses.</span></span>  
  
 [!code-vb[CsLINQAggregating#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/CsLINQAggregating/VB/Aggregating.vb#6)]  
  
## <a name="see-also"></a><span data-ttu-id="9a3eb-143">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="9a3eb-143">See also</span></span>

- <xref:System.Linq>
- [<span data-ttu-id="9a3eb-144">Standardowe operatory zapytań — Omówienie (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="9a3eb-144">Standard Query Operators Overview (Visual Basic)</span></span>](standard-query-operators-overview.md)
- [<span data-ttu-id="9a3eb-145">Aggregate, klauzula</span><span class="sxs-lookup"><span data-stu-id="9a3eb-145">Aggregate Clause</span></span>](../../../language-reference/queries/aggregate-clause.md)
- [<span data-ttu-id="9a3eb-146">Instrukcje: Obliczanie wartości kolumn w pliku tekstowym CSV (LINQ) (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="9a3eb-146">How to: Compute Column Values in a CSV Text File (LINQ) (Visual Basic)</span></span>](how-to-compute-column-values-in-a-csv-text-file-linq.md)
- [<span data-ttu-id="9a3eb-147">Instrukcje: zliczanie, sumowanie lub średnie dane</span><span class="sxs-lookup"><span data-stu-id="9a3eb-147">How to: Count, Sum, or Average Data</span></span>](../../language-features/linq/how-to-count-sum-or-average-data-by-using-linq.md)
- [<span data-ttu-id="9a3eb-148">Instrukcje: Znajdowanie wartości minimalnej lub maksymalnej w wyniku zapytania</span><span class="sxs-lookup"><span data-stu-id="9a3eb-148">How to: Find the Minimum or Maximum Value in a Query Result</span></span>](../../language-features/linq/how-to-find-the-minimum-or-maximum-value-in-a-query-result.md)
- [<span data-ttu-id="9a3eb-149">Instrukcje: zapytanie o największy plik lub pliki w drzewie katalogów (LINQ) (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="9a3eb-149">How to: Query for the Largest File or Files in a Directory Tree (LINQ) (Visual Basic)</span></span>](how-to-query-for-the-largest-file-or-files-in-a-directory-tree.md)
- [<span data-ttu-id="9a3eb-150">Instrukcje: zapytanie o całkowitą liczbę bajtów w zestawie folderów (LINQ) (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="9a3eb-150">How to: Query for the Total Number of Bytes in a Set of Folders (LINQ) (Visual Basic)</span></span>](how-to-query-for-the-total-number-of-bytes-in-a-set-of-folders.md)
