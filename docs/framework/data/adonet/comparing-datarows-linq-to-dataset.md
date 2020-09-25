---
title: Porównywanie wierszy DataRows (LINQ to DataSet)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 8fe0eadf-297b-487c-8d4b-7816753c2883
ms.openlocfilehash: 8cce52734c83e42312d71806d4151ef21e4df0ba
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91203803"
---
# <a name="comparing-datarows-linq-to-dataset"></a><span data-ttu-id="c9ffa-102">Porównywanie wierszy DataRows (LINQ to DataSet)</span><span class="sxs-lookup"><span data-stu-id="c9ffa-102">Comparing DataRows (LINQ to DataSet)</span></span>

<span data-ttu-id="c9ffa-103">Załączone w języku zapytanie (LINQ) definiuje różne operatory zestawów do porównywania elementów źródłowych, aby sprawdzić, czy są równe.</span><span class="sxs-lookup"><span data-stu-id="c9ffa-103">Language-Integrated Query (LINQ) defines various set operators to compare source elements to see if they are equal.</span></span> <span data-ttu-id="c9ffa-104">LINQ udostępnia następujące operatory zestawu:</span><span class="sxs-lookup"><span data-stu-id="c9ffa-104">LINQ provides the following set operators:</span></span>  
  
- <xref:System.Linq.Enumerable.Distinct%2A>  
  
- <xref:System.Linq.Enumerable.Union%2A>  
  
- <xref:System.Linq.Enumerable.Intersect%2A>  
  
- <xref:System.Linq.Enumerable.Except%2A>  
  
 <span data-ttu-id="c9ffa-105">Te operatory porównują elementy źródłowe, <xref:System.Collections.Generic.IEqualityComparer%601.GetHashCode%2A> wywołując <xref:System.Collections.Generic.IEqualityComparer%601.Equals%2A> metody i dla każdej kolekcji elementów.</span><span class="sxs-lookup"><span data-stu-id="c9ffa-105">These operators compare source elements by calling the <xref:System.Collections.Generic.IEqualityComparer%601.GetHashCode%2A> and <xref:System.Collections.Generic.IEqualityComparer%601.Equals%2A> methods on each collection of elements.</span></span> <span data-ttu-id="c9ffa-106">W przypadku <xref:System.Data.DataRow> , te operatory wykonują porównanie odwołań, które zwykle nie jest idealnym zachowaniem dla operacji ustawiania w danych tabelarycznych.</span><span class="sxs-lookup"><span data-stu-id="c9ffa-106">In the case of a <xref:System.Data.DataRow>, these operators perform a reference comparison, which is generally not the ideal behavior for set operations over tabular data.</span></span> <span data-ttu-id="c9ffa-107">W przypadku operacji ustawiania zazwyczaj należy określić, czy wartości elementów są równe, a nie odwołania do elementów.</span><span class="sxs-lookup"><span data-stu-id="c9ffa-107">For set operations, you usually want to determine whether the element values are equal and not the element references.</span></span> <span data-ttu-id="c9ffa-108">W związku z tym <xref:System.Data.DataRowComparer> Klasa została dodana do LINQ to DataSet.</span><span class="sxs-lookup"><span data-stu-id="c9ffa-108">Therefore, the <xref:System.Data.DataRowComparer> class has been added to LINQ to DataSet.</span></span> <span data-ttu-id="c9ffa-109">Ta klasa może służyć do porównywania wartości wierszy.</span><span class="sxs-lookup"><span data-stu-id="c9ffa-109">This class can be used to compare row values.</span></span>  
  
 <span data-ttu-id="c9ffa-110"><xref:System.Data.DataRowComparer>Klasa zawiera implementację porównania wartości dla <xref:System.Data.DataRow> , więc ta klasa może być używana do ustawiania operacji, takich jak <xref:System.Linq.Enumerable.Distinct%2A> .</span><span class="sxs-lookup"><span data-stu-id="c9ffa-110">The <xref:System.Data.DataRowComparer> class contains a value comparison implementation for <xref:System.Data.DataRow>, so this class can be used for set operations such as <xref:System.Linq.Enumerable.Distinct%2A>.</span></span> <span data-ttu-id="c9ffa-111">Nie można bezpośrednio utworzyć wystąpienia tej klasy; Zamiast tego <xref:System.Data.DataRowComparer.Default%2A> Właściwość musi być używana do zwracania wystąpienia <xref:System.Data.DataRowComparer%601> .</span><span class="sxs-lookup"><span data-stu-id="c9ffa-111">This class cannot be directly instantiated; instead, the <xref:System.Data.DataRowComparer.Default%2A> property must be used to return an instance of the <xref:System.Data.DataRowComparer%601>.</span></span> <span data-ttu-id="c9ffa-112"><xref:System.Data.DataRowComparer%601.Equals%2A>Metoda jest następnie wywoływana, a dwa <xref:System.Data.DataRow> obiekty, które mają być porównane, są przenoszone jako parametry wejściowe.</span><span class="sxs-lookup"><span data-stu-id="c9ffa-112">The <xref:System.Data.DataRowComparer%601.Equals%2A> method is then called and the two <xref:System.Data.DataRow> objects to be compared are passed in as input parameters.</span></span> <span data-ttu-id="c9ffa-113"><xref:System.Data.DataRowComparer%601.Equals%2A>Metoda zwraca `true` , czy uporządkowany zestaw wartości kolumn w obu <xref:System.Data.DataRow> obiektach jest równy; w przeciwnym razie `false` .</span><span class="sxs-lookup"><span data-stu-id="c9ffa-113">The <xref:System.Data.DataRowComparer%601.Equals%2A> method returns `true` if the ordered set of column values in both <xref:System.Data.DataRow> objects are equal; otherwise, `false`.</span></span>  
  
## <a name="example"></a><span data-ttu-id="c9ffa-114">Przykład</span><span class="sxs-lookup"><span data-stu-id="c9ffa-114">Example</span></span>  

 <span data-ttu-id="c9ffa-115">Ten przykład używa `Intersect` do zwracania kontaktów, które pojawiają się w obu tabelach.</span><span class="sxs-lookup"><span data-stu-id="c9ffa-115">This example uses `Intersect` to return contacts that appear in both tables.</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#Intersect2](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#intersect2)]
 [!code-vb[DP LINQ to DataSet Examples#Intersect2](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#intersect2)]  
  
### <a name="example"></a><span data-ttu-id="c9ffa-116">Przykład</span><span class="sxs-lookup"><span data-stu-id="c9ffa-116">Example</span></span>  

 <span data-ttu-id="c9ffa-117">Poniższy przykład porównuje dwa wiersze i pobiera ich kody skrótów.</span><span class="sxs-lookup"><span data-stu-id="c9ffa-117">The following example compares two rows and gets their hash codes.</span></span>  
  
 [!code-vb[DP LINQ to DataSet Examples#CompareDifferentRows](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#comparedifferentrows)]  
  
## <a name="see-also"></a><span data-ttu-id="c9ffa-118">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="c9ffa-118">See also</span></span>

- <xref:System.Data.DataRowComparer>
- [<span data-ttu-id="c9ffa-119">Ładowanie danych do zestawu danych</span><span class="sxs-lookup"><span data-stu-id="c9ffa-119">Loading Data Into a DataSet</span></span>](loading-data-into-a-dataset.md)
- [<span data-ttu-id="c9ffa-120">Przykłady LINQ to DataSet</span><span class="sxs-lookup"><span data-stu-id="c9ffa-120">LINQ to DataSet Examples</span></span>](linq-to-dataset-examples.md)
