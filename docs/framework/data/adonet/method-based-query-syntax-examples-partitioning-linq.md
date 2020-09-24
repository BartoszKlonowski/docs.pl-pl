---
title: 'Przykłady składni zapytania oparte na metodzie: partycjonowanie (LINQ'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: a582c53f-f203-44ae-a797-d7f169a4fbb5
ms.openlocfilehash: 0ef7176ccffb7037a7d4496cc7d4da7991741d38
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91147934"
---
# <a name="method-based-query-syntax-examples-partitioning-linq"></a><span data-ttu-id="3ab1f-102">Przykłady składni zapytania oparte na metodzie: partycjonowanie (LINQ</span><span class="sxs-lookup"><span data-stu-id="3ab1f-102">Method-Based Query Syntax Examples: Partitioning (LINQ</span></span>

<span data-ttu-id="3ab1f-103">W przykładach w tym temacie pokazano, jak używać <xref:System.Linq.Enumerable.Skip%2A> <xref:System.Linq.Enumerable.SkipWhile%2A> metod,, <xref:System.Linq.Enumerable.Take%2A> i <xref:System.Linq.Enumerable.TakeWhile%2A> do wykonywania zapytań <xref:System.Data.DataSet> przy użyciu składni wyrażenia zapytania.</span><span class="sxs-lookup"><span data-stu-id="3ab1f-103">The examples in this topic demonstrate how to use the <xref:System.Linq.Enumerable.Skip%2A>, <xref:System.Linq.Enumerable.SkipWhile%2A>, <xref:System.Linq.Enumerable.Take%2A>, and <xref:System.Linq.Enumerable.TakeWhile%2A> methods to query a <xref:System.Data.DataSet> using the query expression syntax.</span></span>  
  
 <span data-ttu-id="3ab1f-104">`FillDataSet`Metoda użyta w tych przykładach jest określona w temacie [ładowanie danych do zestawu danych](loading-data-into-a-dataset.md).</span><span class="sxs-lookup"><span data-stu-id="3ab1f-104">The `FillDataSet` method used in these examples is specified in [Loading Data Into a DataSet](loading-data-into-a-dataset.md).</span></span>  
  
 <span data-ttu-id="3ab1f-105">W przykładach w tym temacie użyto tabel Contact, Address, Product, SalesOrderHeader i SalesOrderDetail w przykładowej bazie danych AdventureWorks.</span><span class="sxs-lookup"><span data-stu-id="3ab1f-105">The examples in this topic use the Contact, Address, Product, SalesOrderHeader, and SalesOrderDetail tables in the AdventureWorks sample database.</span></span>  
  
 <span data-ttu-id="3ab1f-106">Przykłady w tym temacie wykorzystują następujące `using` / `Imports` instrukcje:</span><span class="sxs-lookup"><span data-stu-id="3ab1f-106">The examples in this topic use the following `using`/`Imports` statements:</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#ImportsUsing](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#importsusing)]
 [!code-vb[DP LINQ to DataSet Examples#ImportsUsing](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#importsusing)]  
  
 <span data-ttu-id="3ab1f-107">Aby uzyskać więcej informacji, zobacz [How to: Create a LINQ to DataSet Project in Visual Studio](how-to-create-a-linq-to-dataset-project-in-vs.md).</span><span class="sxs-lookup"><span data-stu-id="3ab1f-107">For more information, see [How to: Create a LINQ to DataSet Project In Visual Studio](how-to-create-a-linq-to-dataset-project-in-vs.md).</span></span>  
  
## <a name="skip"></a><span data-ttu-id="3ab1f-108">Pomiń</span><span class="sxs-lookup"><span data-stu-id="3ab1f-108">Skip</span></span>  
  
### <a name="example"></a><span data-ttu-id="3ab1f-109">Przykład</span><span class="sxs-lookup"><span data-stu-id="3ab1f-109">Example</span></span>  

 <span data-ttu-id="3ab1f-110">W tym przykładzie zastosowano <xref:System.Linq.Enumerable.Skip%2A> metodę, aby pobrać wszystkie pierwsze kontakty z `Contact` tabeli.</span><span class="sxs-lookup"><span data-stu-id="3ab1f-110">This example uses the <xref:System.Linq.Enumerable.Skip%2A> method to get all but the first five contacts of the `Contact` table.</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#SkipSimple](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#skipsimple)]
 [!code-vb[DP LINQ to DataSet Examples#SkipSimple](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#skipsimple)]  
  
### <a name="example"></a><span data-ttu-id="3ab1f-111">Przykład</span><span class="sxs-lookup"><span data-stu-id="3ab1f-111">Example</span></span>  

 <span data-ttu-id="3ab1f-112">W tym przykładzie zastosowano <xref:System.Linq.Enumerable.Skip%2A> metodę, aby pobrać wszystkie pierwsze dwa adresy z Seattle.</span><span class="sxs-lookup"><span data-stu-id="3ab1f-112">This example uses the <xref:System.Linq.Enumerable.Skip%2A> method to get all but the first two addresses in Seattle.</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#SkipNested](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#skipnested)]
 [!code-vb[DP LINQ to DataSet Examples#SkipNested](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#skipnested)]  
  
## <a name="skipwhile"></a><span data-ttu-id="3ab1f-113">SkipWhile —</span><span class="sxs-lookup"><span data-stu-id="3ab1f-113">SkipWhile</span></span>  
  
### <a name="example"></a><span data-ttu-id="3ab1f-114">Przykład</span><span class="sxs-lookup"><span data-stu-id="3ab1f-114">Example</span></span>  

 <span data-ttu-id="3ab1f-115">Ten przykład używa <xref:System.Linq.Enumerable.OrderBy%2A> <xref:System.Linq.Enumerable.SkipWhile%2A> metod i zwraca produkty z `Product` tabeli z cennikiem większym niż 300,00.</span><span class="sxs-lookup"><span data-stu-id="3ab1f-115">This example uses <xref:System.Linq.Enumerable.OrderBy%2A> and <xref:System.Linq.Enumerable.SkipWhile%2A> methods to return products from the `Product` table with a list price greater than 300.00.</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#SkipWhileSimple_MQ](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#skipwhilesimple_mq)]
 [!code-vb[DP LINQ to DataSet Examples#SkipWhileSimple_MQ](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#skipwhilesimple_mq)]  
  
## <a name="take"></a><span data-ttu-id="3ab1f-116">Take</span><span class="sxs-lookup"><span data-stu-id="3ab1f-116">Take</span></span>  
  
### <a name="example"></a><span data-ttu-id="3ab1f-117">Przykład</span><span class="sxs-lookup"><span data-stu-id="3ab1f-117">Example</span></span>  

 <span data-ttu-id="3ab1f-118">Ten przykład używa <xref:System.Linq.Enumerable.Take%2A> metody, aby uzyskać tylko pięć pierwszych kontaktów z `Contact` tabeli.</span><span class="sxs-lookup"><span data-stu-id="3ab1f-118">This example uses the <xref:System.Linq.Enumerable.Take%2A> method to get only the first five contacts from the `Contact` table.</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#TakeSimple](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#takesimple)]
 [!code-vb[DP LINQ to DataSet Examples#TakeSimple](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#takesimple)]  
  
### <a name="example"></a><span data-ttu-id="3ab1f-119">Przykład</span><span class="sxs-lookup"><span data-stu-id="3ab1f-119">Example</span></span>  

 <span data-ttu-id="3ab1f-120">W tym przykładzie zastosowano <xref:System.Linq.Enumerable.Take%2A> metodę, aby pobrać pierwsze trzy adresy w Seattle.</span><span class="sxs-lookup"><span data-stu-id="3ab1f-120">This example uses the <xref:System.Linq.Enumerable.Take%2A> method to get the first three addresses in Seattle.</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#TakeNested](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#takenested)]
 [!code-vb[DP LINQ to DataSet Examples#TakeNested](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#takenested)]  
  
## <a name="takewhile"></a><span data-ttu-id="3ab1f-121">TakeWhile —</span><span class="sxs-lookup"><span data-stu-id="3ab1f-121">TakeWhile</span></span>  
  
### <a name="example"></a><span data-ttu-id="3ab1f-122">Przykład</span><span class="sxs-lookup"><span data-stu-id="3ab1f-122">Example</span></span>  

 <span data-ttu-id="3ab1f-123">Ten przykład używa <xref:System.Linq.Enumerable.OrderBy%2A> i <xref:System.Linq.Enumerable.TakeWhile%2A> zwraca produkty z `Product` tabeli z cennikiem mniejszym niż 300,00.</span><span class="sxs-lookup"><span data-stu-id="3ab1f-123">This example uses <xref:System.Linq.Enumerable.OrderBy%2A> and <xref:System.Linq.Enumerable.TakeWhile%2A> to return products from the `Product` table with a list price less than 300.00.</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#TakeWhileSimple_MQ](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#takewhilesimple_mq)]
 [!code-vb[DP LINQ to DataSet Examples#TakeWhileSimple_MQ](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#takewhilesimple_mq)]  
  
## <a name="see-also"></a><span data-ttu-id="3ab1f-124">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="3ab1f-124">See also</span></span>

- [<span data-ttu-id="3ab1f-125">Ładowanie danych do zestawu danych</span><span class="sxs-lookup"><span data-stu-id="3ab1f-125">Loading Data Into a DataSet</span></span>](loading-data-into-a-dataset.md)
- [<span data-ttu-id="3ab1f-126">Przykłady LINQ to DataSet</span><span class="sxs-lookup"><span data-stu-id="3ab1f-126">LINQ to DataSet Examples</span></span>](linq-to-dataset-examples.md)
- [<span data-ttu-id="3ab1f-127">Standardowe operatory zapytań — Omówienie (C#)</span><span class="sxs-lookup"><span data-stu-id="3ab1f-127">Standard Query Operators Overview (C#)</span></span>](../../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md)
- [<span data-ttu-id="3ab1f-128">Standardowe operatory zapytań — Omówienie (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="3ab1f-128">Standard Query Operators Overview (Visual Basic)</span></span>](../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)
