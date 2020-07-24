---
title: Grupowanie danych (C#)
description: Grupowanie umieszcza dane w grupach elementów, które współużytkują atrybut. Zapoznaj się ze standardowymi metodami operatorów zapytań w LINQ w języku C#, które grupują elementy danych.
ms.date: 07/20/2015
ms.assetid: e414e9e4-343a-4e6e-858f-4a30c5e64492
ms.openlocfilehash: 5e1bca1d360b0f44a081cf2770118a0551629b5b
ms.sourcegitcommit: 04022ca5d00b2074e1b1ffdbd76bec4950697c4c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/23/2020
ms.locfileid: "87103675"
---
# <a name="grouping-data-c"></a><span data-ttu-id="e7d40-104">Grupowanie danych (C#)</span><span class="sxs-lookup"><span data-stu-id="e7d40-104">Grouping Data (C#)</span></span>
<span data-ttu-id="e7d40-105">Grupowanie odwołuje się do operacji umieszczania danych w grupach, tak aby elementy w każdej grupie miały wspólny atrybut.</span><span class="sxs-lookup"><span data-stu-id="e7d40-105">Grouping refers to the operation of putting data into groups so that the elements in each group share a common attribute.</span></span>  
  
 <span data-ttu-id="e7d40-106">Na poniższej ilustracji przedstawiono wyniki grupowania sekwencji znaków.</span><span class="sxs-lookup"><span data-stu-id="e7d40-106">The following illustration shows the results of grouping a sequence of characters.</span></span> <span data-ttu-id="e7d40-107">Klucz dla każdej grupy jest znakiem.</span><span class="sxs-lookup"><span data-stu-id="e7d40-107">The key for each group is the character.</span></span>  
  
 ![Diagram przedstawiający operację grupowania LINQ.](./media/grouping-data/linq-group-operation.png)  
  
 <span data-ttu-id="e7d40-109">Standardowe metody operatorów zapytań, które grupują elementy danych, są wymienione w poniższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="e7d40-109">The standard query operator methods that group data elements are listed in the following section.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="e7d40-110">Metody</span><span class="sxs-lookup"><span data-stu-id="e7d40-110">Methods</span></span>  
  
|<span data-ttu-id="e7d40-111">Nazwa metody</span><span class="sxs-lookup"><span data-stu-id="e7d40-111">Method Name</span></span>|<span data-ttu-id="e7d40-112">Opis</span><span class="sxs-lookup"><span data-stu-id="e7d40-112">Description</span></span>|<span data-ttu-id="e7d40-113">Składnia wyrażenia zapytania C#</span><span class="sxs-lookup"><span data-stu-id="e7d40-113">C# Query Expression Syntax</span></span>|<span data-ttu-id="e7d40-114">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="e7d40-114">More Information</span></span>|  
|-----------------|-----------------|---------------------------------|----------------------|  
|<span data-ttu-id="e7d40-115">GroupBy</span><span class="sxs-lookup"><span data-stu-id="e7d40-115">GroupBy</span></span>|<span data-ttu-id="e7d40-116">Grupuje elementy, które mają wspólny atrybut.</span><span class="sxs-lookup"><span data-stu-id="e7d40-116">Groups elements that share a common attribute.</span></span> <span data-ttu-id="e7d40-117">Każda grupa jest reprezentowana przez <xref:System.Linq.IGrouping%602> obiekt.</span><span class="sxs-lookup"><span data-stu-id="e7d40-117">Each group is represented by an <xref:System.Linq.IGrouping%602> object.</span></span>|`group … by`<br /><br /> <span data-ttu-id="e7d40-118">-lub-</span><span class="sxs-lookup"><span data-stu-id="e7d40-118">-or-</span></span><br /><br /> `group … by … into …`|<xref:System.Linq.Enumerable.GroupBy%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.GroupBy%2A?displayProperty=nameWithType>|  
|<span data-ttu-id="e7d40-119">ToLookup</span><span class="sxs-lookup"><span data-stu-id="e7d40-119">ToLookup</span></span>|<span data-ttu-id="e7d40-120">Wstawia elementy do <xref:System.Linq.Lookup%602> (słownik jeden-do-wielu) w oparciu o funkcję selektora kluczy.</span><span class="sxs-lookup"><span data-stu-id="e7d40-120">Inserts elements into a <xref:System.Linq.Lookup%602> (a one-to-many dictionary) based on a key selector function.</span></span>|<span data-ttu-id="e7d40-121">Nie dotyczy.</span><span class="sxs-lookup"><span data-stu-id="e7d40-121">Not applicable.</span></span>|<xref:System.Linq.Enumerable.ToLookup%2A?displayProperty=nameWithType>|  
  
## <a name="query-expression-syntax-example"></a><span data-ttu-id="e7d40-122">Przykład składni wyrażenia zapytania</span><span class="sxs-lookup"><span data-stu-id="e7d40-122">Query Expression Syntax Example</span></span>  
 <span data-ttu-id="e7d40-123">Poniższy przykład kodu używa `group by` klauzuli do grupowania liczb całkowitych na liście zgodnie z tym, czy są one parzyste czy nieparzyste.</span><span class="sxs-lookup"><span data-stu-id="e7d40-123">The following code example uses the `group by` clause to group integers in a list according to whether they are even or odd.</span></span>  
  
```csharp  
List<int> numbers = new List<int>() { 35, 44, 200, 84, 3987, 4, 199, 329, 446, 208 };  
  
IEnumerable<IGrouping<int, int>> query = from number in numbers  
                                         group number by number % 2;  
  
foreach (var group in query)  
{  
    Console.WriteLine(group.Key == 0 ? "\nEven numbers:" : "\nOdd numbers:");  
    foreach (int i in group)  
        Console.WriteLine(i);  
}  
  
/* This code produces the following output:  
  
    Odd numbers:  
    35  
    3987  
    199  
    329  
  
    Even numbers:  
    44  
    200  
    84  
    4  
    446  
    208  
*/  
```  
  
## <a name="see-also"></a><span data-ttu-id="e7d40-124">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="e7d40-124">See also</span></span>

- <xref:System.Linq>
- [<span data-ttu-id="e7d40-125">Standardowe operatory zapytań — Omówienie (C#)</span><span class="sxs-lookup"><span data-stu-id="e7d40-125">Standard Query Operators Overview (C#)</span></span>](./standard-query-operators-overview.md)
- [<span data-ttu-id="e7d40-126">group — Klauzula</span><span class="sxs-lookup"><span data-stu-id="e7d40-126">group clause</span></span>](../../../language-reference/keywords/group-clause.md)
- [<span data-ttu-id="e7d40-127">Tworzenie grupy zagnieżdżonej</span><span class="sxs-lookup"><span data-stu-id="e7d40-127">Create a nested group</span></span>](../../../linq/create-a-nested-group.md)
- [<span data-ttu-id="e7d40-128">Jak grupować pliki według rozszerzenia (LINQ) (C#)</span><span class="sxs-lookup"><span data-stu-id="e7d40-128">How to group files by extension (LINQ) (C#)</span></span>](./how-to-group-files-by-extension-linq.md)
- [<span data-ttu-id="e7d40-129">Grupowanie wyników zapytania</span><span class="sxs-lookup"><span data-stu-id="e7d40-129">Group query results</span></span>](../../../linq/group-query-results.md)
- [<span data-ttu-id="e7d40-130">Wykonywanie podzapytania w operacji grupowania</span><span class="sxs-lookup"><span data-stu-id="e7d40-130">Perform a subquery on a grouping operation</span></span>](../../../linq/perform-a-subquery-on-a-grouping-operation.md)
- [<span data-ttu-id="e7d40-131">Jak podzielić plik na wiele plików przy użyciu grup (LINQ) (C#)</span><span class="sxs-lookup"><span data-stu-id="e7d40-131">How to split a file into many files by using groups (LINQ) (C#)</span></span>](./how-to-split-a-file-into-many-files-by-using-groups-linq.md)
