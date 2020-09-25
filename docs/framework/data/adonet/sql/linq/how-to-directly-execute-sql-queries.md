---
title: 'Instrukcje: Bezpośrednie wykonywanie zapytań SQL'
description: Dowiedz się, w jaki sposób używać ExecuteQuery do uruchamiania zapytania, a następnie konwertować wyniki bezpośrednio do obiektów w przypadkach, gdy zapytanie LINQ to SQL jest niewystarczające.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: e491b9bf-741a-4296-9f51-76c25ddf6a82
ms.openlocfilehash: 7ebd02581d789266396b58296bbd6ad312dd468e
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91200579"
---
# <a name="how-to-directly-execute-sql-queries"></a><span data-ttu-id="8d7dc-103">Instrukcje: Bezpośrednie wykonywanie zapytań SQL</span><span class="sxs-lookup"><span data-stu-id="8d7dc-103">How to: Directly Execute SQL Queries</span></span>

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <span data-ttu-id="8d7dc-104">tłumaczy zapytania zapisywane w sparametryzowanych zapytaniach SQL (w formie tekstowej) i wysyła je do programu SQL Server w celu przetworzenia.</span><span class="sxs-lookup"><span data-stu-id="8d7dc-104">translates the queries you write into parameterized SQL queries (in text form) and sends them to the SQL server for processing.</span></span>  
  
 <span data-ttu-id="8d7dc-105">W programie SQL Server nie można wykonywać różnych metod, które mogą być lokalnie dostępne dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8d7dc-105">SQL cannot execute the variety of methods that might be locally available to your application.</span></span> [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <span data-ttu-id="8d7dc-106">próbuje przekonwertować te metody lokalne na równoważne operacje i funkcje, które są dostępne wewnątrz środowiska SQL.</span><span class="sxs-lookup"><span data-stu-id="8d7dc-106">tries to convert these local methods to equivalent operations and functions that are available inside the SQL environment.</span></span> <span data-ttu-id="8d7dc-107">Większość metod i operatorów na .NET Framework typów wbudowanych ma bezpośrednie tłumaczenia na polecenia SQL.</span><span class="sxs-lookup"><span data-stu-id="8d7dc-107">Most methods and operators on .NET Framework built-in types have direct translations to SQL commands.</span></span> <span data-ttu-id="8d7dc-108">Niektóre z dostępnych funkcji można wytwarzać.</span><span class="sxs-lookup"><span data-stu-id="8d7dc-108">Some can be produced from the functions that are available.</span></span> <span data-ttu-id="8d7dc-109">Te, które nie mogą zostać wygenerowane, generują wyjątki w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="8d7dc-109">Those that cannot be produced generate run-time exceptions.</span></span> <span data-ttu-id="8d7dc-110">Aby uzyskać więcej informacji, zobacz [Mapowanie typu SQL-CLR](sql-clr-type-mapping.md).</span><span class="sxs-lookup"><span data-stu-id="8d7dc-110">For more information, see [SQL-CLR Type Mapping](sql-clr-type-mapping.md).</span></span>  
  
 <span data-ttu-id="8d7dc-111">W przypadkach, gdy [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] zapytanie jest niewystarczające dla wyspecjalizowanego zadania, można użyć <xref:System.Data.Linq.DataContext.ExecuteQuery%2A> metody do wykonania zapytania SQL, a następnie przekonwertować wynik zapytania bezpośrednio do obiektów.</span><span class="sxs-lookup"><span data-stu-id="8d7dc-111">In cases where a [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] query is insufficient for a specialized task, you can use the <xref:System.Data.Linq.DataContext.ExecuteQuery%2A> method to execute a SQL query, and then convert the result of your query directly into objects.</span></span>  
  
## <a name="example"></a><span data-ttu-id="8d7dc-112">Przykład</span><span class="sxs-lookup"><span data-stu-id="8d7dc-112">Example</span></span>  

 <span data-ttu-id="8d7dc-113">W poniższym przykładzie Załóżmy, że dane dla `Customer` klasy są rozłożone na dwie tabele (customer1 i Customer2).</span><span class="sxs-lookup"><span data-stu-id="8d7dc-113">In the following example, assume that the data for the `Customer` class is spread over two tables (customer1 and customer2).</span></span> <span data-ttu-id="8d7dc-114">Zapytanie zwraca sekwencję `Customer` obiektów.</span><span class="sxs-lookup"><span data-stu-id="8d7dc-114">The query returns a sequence of `Customer` objects.</span></span>  
  
 [!code-csharp[DLinqQuerying#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQuerying/cs/Program.cs#4)]
 [!code-vb[DLinqQuerying#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQuerying/vb/Module1.vb#4)]  
  
 <span data-ttu-id="8d7dc-115">Tak długo, jak nazwy kolumn w wynikach tabelarycznych są zgodne z właściwościami kolumny klasy Entity, program [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] tworzy obiekty z dowolnego zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="8d7dc-115">As long as the column names in the tabular results match column properties of your entity class, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] creates your objects out of any SQL query.</span></span>  
  
## <a name="example"></a><span data-ttu-id="8d7dc-116">Przykład</span><span class="sxs-lookup"><span data-stu-id="8d7dc-116">Example</span></span>  

 <span data-ttu-id="8d7dc-117"><xref:System.Data.Linq.DataContext.ExecuteQuery%2A>Metoda umożliwia również parametry.</span><span class="sxs-lookup"><span data-stu-id="8d7dc-117">The <xref:System.Data.Linq.DataContext.ExecuteQuery%2A> method also allows for parameters.</span></span> <span data-ttu-id="8d7dc-118">Użyj poniższego kodu, aby wykonać zapytanie parametryczne.</span><span class="sxs-lookup"><span data-stu-id="8d7dc-118">Use code such as the following to execute a parameterized query.</span></span>  
  
 [!code-csharp[DLinqQuerying#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQuerying/cs/Program.cs#5)]
 [!code-vb[DLinqQuerying#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQuerying/vb/Module1.vb#5)]  
  
 <span data-ttu-id="8d7dc-119">Parametry są wyrażane w tekście zapytania przy użyciu tej samej notacji klamrowej używanej przez `Console.WriteLine()` i `String.Format()` .</span><span class="sxs-lookup"><span data-stu-id="8d7dc-119">The parameters are expressed in the query text by using the same curly notation used by `Console.WriteLine()` and `String.Format()`.</span></span> <span data-ttu-id="8d7dc-120">W rzeczywistości `String.Format()` jest faktycznie wywoływana w podanym ciągu zapytania, podstawiając parametry klamrowe z wygenerowanymi nazwami parametrów, takimi jak @p0 , @p1 ..., @p (n).</span><span class="sxs-lookup"><span data-stu-id="8d7dc-120">In fact, `String.Format()` is actually called on the query string you provide, substituting the curly braced parameters with generated parameter names such as @p0, @p1 …, @p(n).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="8d7dc-121">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="8d7dc-121">See also</span></span>

- [<span data-ttu-id="8d7dc-122">Informacje uzupełniające</span><span class="sxs-lookup"><span data-stu-id="8d7dc-122">Background Information</span></span>](background-information.md)
- [<span data-ttu-id="8d7dc-123">wykonywanie zapytania w bazie danych</span><span class="sxs-lookup"><span data-stu-id="8d7dc-123">Querying the Database</span></span>](querying-the-database.md)
