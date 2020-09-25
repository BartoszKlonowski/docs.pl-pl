---
title: Zwracanie pierwszego elementu w sekwencji
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: ccdc3777-b2c2-44e3-a627-abef8d79a555
ms.openlocfilehash: 4506ef1a79c8f7e77160df4d55d0f93ee79f5a41
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91200345"
---
# <a name="return-the-first-element-in-a-sequence"></a><span data-ttu-id="18bb5-102">Zwracanie pierwszego elementu w sekwencji</span><span class="sxs-lookup"><span data-stu-id="18bb5-102">Return the First Element in a Sequence</span></span>

<span data-ttu-id="18bb5-103">Użyj <xref:System.Linq.Enumerable.First%2A> operatora, aby zwrócić pierwszy element w sekwencji.</span><span class="sxs-lookup"><span data-stu-id="18bb5-103">Use the <xref:System.Linq.Enumerable.First%2A> operator to return the first element in a sequence.</span></span> <span data-ttu-id="18bb5-104">Zapytania, które używają <xref:System.Linq.Enumerable.First%2A> są wykonywane od razu.</span><span class="sxs-lookup"><span data-stu-id="18bb5-104">Queries that use <xref:System.Linq.Enumerable.First%2A> are executed immediately.</span></span>  
  
> [!NOTE]
> [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <span data-ttu-id="18bb5-105">nie obsługuje <xref:System.Linq.Enumerable.Last%2A> operatora.</span><span class="sxs-lookup"><span data-stu-id="18bb5-105">does not support the <xref:System.Linq.Enumerable.Last%2A> operator.</span></span>  
  
## <a name="example"></a><span data-ttu-id="18bb5-106">Przykład</span><span class="sxs-lookup"><span data-stu-id="18bb5-106">Example</span></span>  

 <span data-ttu-id="18bb5-107">Poniższy kod umożliwia znalezienie pierwszego `Shipper` w tabeli:</span><span class="sxs-lookup"><span data-stu-id="18bb5-107">The following code finds the first `Shipper` in a table:</span></span>  
  
 <span data-ttu-id="18bb5-108">W przypadku uruchomienia tego zapytania względem przykładowej bazy danych Northwind wyniki są</span><span class="sxs-lookup"><span data-stu-id="18bb5-108">If you run this query against the Northwind sample database, the results are</span></span>  
  
 <span data-ttu-id="18bb5-109">`ID = 1, Company = Speedy Express`.</span><span class="sxs-lookup"><span data-stu-id="18bb5-109">`ID = 1, Company = Speedy Express`.</span></span>  
  
 [!code-csharp[DLinqQueryExamples#14](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#14)]
 [!code-vb[DLinqQueryExamples#14](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#14)]  
  
## <a name="example"></a><span data-ttu-id="18bb5-110">Przykład</span><span class="sxs-lookup"><span data-stu-id="18bb5-110">Example</span></span>  

 <span data-ttu-id="18bb5-111">Poniższy kod umożliwia znalezienie pojedynczego `Customer` , który ma `CustomerID` BONAP.</span><span class="sxs-lookup"><span data-stu-id="18bb5-111">The following code finds the single `Customer` that has the `CustomerID` BONAP.</span></span>  
  
 <span data-ttu-id="18bb5-112">W przypadku uruchomienia tego zapytania względem przykładowej bazy danych Northwind wyniki są następujące `ID = BONAP, Contact = Laurence Lebihan` .</span><span class="sxs-lookup"><span data-stu-id="18bb5-112">If you run this query against the Northwind sample database, the results are `ID = BONAP, Contact = Laurence Lebihan`.</span></span>  
  
 [!code-csharp[DLinqQueryExamples#15](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#15)]
 [!code-vb[DLinqQueryExamples#15](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#15)]  
  
## <a name="see-also"></a><span data-ttu-id="18bb5-113">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="18bb5-113">See also</span></span>

- [<span data-ttu-id="18bb5-114">Przykłady zapytań</span><span class="sxs-lookup"><span data-stu-id="18bb5-114">Query Examples</span></span>](query-examples.md)
- [<span data-ttu-id="18bb5-115">Pobieranie przykładowych baz danych</span><span class="sxs-lookup"><span data-stu-id="18bb5-115">Downloading Sample Databases</span></span>](downloading-sample-databases.md)
