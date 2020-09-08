---
title: Wydajność zapytań łańcuchowych — LINQ to XML
description: Zapoznaj się z kwerendami łańcuchowymi, a także z pojedynczym bardziej skomplikowanym zapytaniem.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: b2f1d715-8946-4dc0-8d56-fb3d1bba54a6
ms.openlocfilehash: c1dae1eaf008a1f17c6884ef6b8e67d042719ad9
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/08/2020
ms.locfileid: "89553092"
---
# <a name="performance-of-chained-queries-linq-to-xml"></a><span data-ttu-id="311a9-103">Wydajność zapytań łańcuchowych (LINQ to XML)</span><span class="sxs-lookup"><span data-stu-id="311a9-103">Performance of chained queries (LINQ to XML)</span></span>

<span data-ttu-id="311a9-104">Jedną z najważniejszych zalet LINQ (i LINQ to XML) jest to, że kwerendy łańcuchowe mogą wykonywać, a także pojedyncze zapytanie, które jest większe i bardziej skomplikowane niż zapytania łańcuchowe.</span><span class="sxs-lookup"><span data-stu-id="311a9-104">One of the most important benefits of LINQ (and LINQ to XML) is that chained queries can perform as well as a single query that is larger and more complicated than the chained queries.</span></span>

<span data-ttu-id="311a9-105">Zapytanie łańcuchowe jest kwerendą, która używa innego zapytania jako źródła.</span><span class="sxs-lookup"><span data-stu-id="311a9-105">A chained query is a query that uses another query as its source.</span></span> <span data-ttu-id="311a9-106">Na przykład, w poniższym prostym kodzie, `query2` ma `query1` jako Źródło:</span><span class="sxs-lookup"><span data-stu-id="311a9-106">For example, in the following simple code, `query2` has `query1` as its source:</span></span>

```csharp
XElement root = new XElement("Root",
    new XElement("Child", 1),
    new XElement("Child", 2),
    new XElement("Child", 3),
    new XElement("Child", 4)
);

var query1 = from x in root.Elements("Child")
             where (int)x >= 3
             select x;

var query2 = from e in query1
             where (int)e % 2 == 0
             select e;

foreach (var i in query2)
    Console.WriteLine("{0}", (int)i);
```

```vb
Dim root As New XElement("Root", New XElement("Child", 1), New XElement("Child", 2), New XElement("Child", 3), New XElement("Child", 4))

Dim query1 = From x In root.Elements("Child") Where CInt(x) >= 3x

Dim query2 = From e In query1 Where CInt(e) Mod 2 = 0e

For Each i As var In query2
    Console.WriteLine("{0}", CInt(i))
Next
```

<span data-ttu-id="311a9-107">Ten przykład generuje następujące wyniki:</span><span class="sxs-lookup"><span data-stu-id="311a9-107">This example produces the following output:</span></span>

```output
4
```

<span data-ttu-id="311a9-108">To zapytanie łańcuchowe zapewnia ten sam profil wydajności co iteracja w połączonej liście.</span><span class="sxs-lookup"><span data-stu-id="311a9-108">This chained query provides the same performance profile as iterating through a linked list.</span></span>

- <span data-ttu-id="311a9-109"><xref:System.Xml.Linq.XContainer.Elements%2A>Oś ma zasadniczo taką samą wydajność jak iteracja w połączonej liście.</span><span class="sxs-lookup"><span data-stu-id="311a9-109">The <xref:System.Xml.Linq.XContainer.Elements%2A> axis has essentially the same performance as iterating through a linked list.</span></span> <span data-ttu-id="311a9-110"><xref:System.Xml.Linq.XContainer.Elements%2A> jest zaimplementowany jako iterator z odroczonym wykonaniem.</span><span class="sxs-lookup"><span data-stu-id="311a9-110"><xref:System.Xml.Linq.XContainer.Elements%2A> is implemented as an iterator with deferred execution.</span></span> <span data-ttu-id="311a9-111">Oznacza to, że wykonuje kilka zadań oprócz iteracji przez połączoną listę, na przykład przydzielanie obiektu iteratora i śledzenie stanu wykonywania.</span><span class="sxs-lookup"><span data-stu-id="311a9-111">This means that it does some work in addition to iterating through the linked list, such as allocating the iterator object and keeping track of execution state.</span></span> <span data-ttu-id="311a9-112">Ta czynność może zostać podzielona na dwie kategorie: pracy, która jest wykonywana w chwili, gdy iterator jest skonfigurowany, i pracy, która jest wykonywana podczas każdej iteracji.</span><span class="sxs-lookup"><span data-stu-id="311a9-112">This work can be divided into two categories: the work that is done at the time the iterator is set up, and the work that is done during each iteration.</span></span> <span data-ttu-id="311a9-113">Konfiguracja pracy jest małą, stałą ilością pracy i pracy wykonywanej podczas każdej iteracji jest proporcjonalna do liczby elementów w kolekcji źródłowej.</span><span class="sxs-lookup"><span data-stu-id="311a9-113">The setup work is a small, fixed amount of work and the work done during each iteration is proportional to the number of items in the source collection.</span></span>
- <span data-ttu-id="311a9-114">W programie `query1` `where` klauzula ( `Where` w Visual Basic) powoduje, że zapytanie wywołuje <xref:System.Linq.Enumerable.Where%2A> metodę.</span><span class="sxs-lookup"><span data-stu-id="311a9-114">In `query1`, the `where` clause (`Where` in Visual Basic) causes the query to call the <xref:System.Linq.Enumerable.Where%2A> method.</span></span> <span data-ttu-id="311a9-115">Ta metoda jest również zaimplementowana jako iterator.</span><span class="sxs-lookup"><span data-stu-id="311a9-115">This method is also implemented as an iterator.</span></span> <span data-ttu-id="311a9-116">Konfiguracja zadań składa się z tworzenia wystąpienia delegata, który będzie odwoływać się do wyrażenia lambda oraz normalnej konfiguracji iteratora.</span><span class="sxs-lookup"><span data-stu-id="311a9-116">The setup work consists of instantiating the delegate that will reference the lambda expression, plus the normal setup for an iterator.</span></span> <span data-ttu-id="311a9-117">Dla każdej iteracji delegat jest wywoływany, aby wykonać predykat.</span><span class="sxs-lookup"><span data-stu-id="311a9-117">With each iteration, the delegate is called to execute the predicate.</span></span> <span data-ttu-id="311a9-118">Konfiguracja pracy i pracy wykonanej podczas każdej iteracji jest podobna do wykonanej pracy podczas iteracji na osi.</span><span class="sxs-lookup"><span data-stu-id="311a9-118">The setup work and the work done during each iteration is similar to the work done while iterating through the axis.</span></span>
- <span data-ttu-id="311a9-119">W programie `query1` klauzula SELECT powoduje, że zapytanie wywołuje <xref:System.Linq.Enumerable.Select%2A> metodę.</span><span class="sxs-lookup"><span data-stu-id="311a9-119">In `query1`, the select clause causes the query to call the <xref:System.Linq.Enumerable.Select%2A> method.</span></span> <span data-ttu-id="311a9-120">Ta metoda ma ten sam profil wydajności co <xref:System.Linq.Enumerable.Where%2A> Metoda.</span><span class="sxs-lookup"><span data-stu-id="311a9-120">This method has the same performance profile as the <xref:System.Linq.Enumerable.Where%2A> method.</span></span>
- <span data-ttu-id="311a9-121">W programie `query2` obie `where` klauzule ( `Where` w Visual Basic) i `select` klauzula mają taki sam profil wydajności jak w przypadku programu `query1` .</span><span class="sxs-lookup"><span data-stu-id="311a9-121">In `query2`, both the `where` clause (`Where` in Visual Basic) and the `select` clause have the same performance profile as in `query1`.</span></span>

<span data-ttu-id="311a9-122">Iteracja w programie `query2` jest w związku z tym bezpośrednio proporcjonalna do liczby elementów w źródle pierwszego zapytania, czyli czasu liniowego.</span><span class="sxs-lookup"><span data-stu-id="311a9-122">The iteration through `query2` is therefore directly proportional to the number of items in the source of the first query, in other words, linear time.</span></span>

<span data-ttu-id="311a9-123">Aby uzyskać więcej informacji na temat iteratorów, zobacz [Yield](../../csharp/language-reference/keywords/yield.md).</span><span class="sxs-lookup"><span data-stu-id="311a9-123">For more information on iterators, see [yield](../../csharp/language-reference/keywords/yield.md).</span></span>

<span data-ttu-id="311a9-124">Aby zapoznać się z bardziej szczegółowym samouczkiem dotyczącym łączenia zapytań, zobacz [Samouczek: zapytania łańcuchowe razem (C#)](chain-queries-example.md).</span><span class="sxs-lookup"><span data-stu-id="311a9-124">For a more detailed tutorial on chaining queries together, see [Tutorial: Chain queries together (C#)](chain-queries-example.md).</span></span>
