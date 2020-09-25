---
title: Uwagi dotyczące LINQ (Usługi danych programu WCF)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, LINQ
- querying the data service [WCF Data Services]
- WCF Data Services, querying
ms.assetid: cc4ec9e9-348f-42a6-a78e-1cd40e370656
ms.openlocfilehash: 2523aac510516fdf19087425b10ab3f2296eb726
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91194348"
---
# <a name="linq-considerations-wcf-data-services"></a><span data-ttu-id="3d399-102">Uwagi dotyczące LINQ (Usługi danych programu WCF)</span><span class="sxs-lookup"><span data-stu-id="3d399-102">LINQ Considerations (WCF Data Services)</span></span>

<span data-ttu-id="3d399-103">Ten temat zawiera informacje na temat sposobu tworzenia i wykonywania zapytań LINQ, gdy używasz klienta Usługi danych programu WCF i ograniczenia przy użyciu LINQ do wysyłania zapytań do usługi danych implementującej protokół Open Data Protocol (OData).</span><span class="sxs-lookup"><span data-stu-id="3d399-103">This topic provides information about the way in which LINQ queries are composed and executed when you are using the WCF Data Services client and limitations of using LINQ to query a data service that implements the Open Data Protocol (OData).</span></span> <span data-ttu-id="3d399-104">Aby uzyskać więcej informacji o tworzeniu i wykonywaniu zapytań dotyczących usługi danych opartych na protokole OData, zobacz [wykonywanie zapytań do usługi danych](querying-the-data-service-wcf-data-services.md).</span><span class="sxs-lookup"><span data-stu-id="3d399-104">For more information about composing and executing queries against an OData-based data service, see [Querying the Data Service](querying-the-data-service-wcf-data-services.md).</span></span>  
  
## <a name="composing-linq-queries"></a><span data-ttu-id="3d399-105">Redagowanie zapytań LINQ</span><span class="sxs-lookup"><span data-stu-id="3d399-105">Composing LINQ Queries</span></span>  

 <span data-ttu-id="3d399-106">LINQ umożliwia tworzenie zapytań względem kolekcji obiektów, które implementują <xref:System.Collections.Generic.IEnumerable%601> .</span><span class="sxs-lookup"><span data-stu-id="3d399-106">LINQ enables you to compose queries against a collection of objects that implements <xref:System.Collections.Generic.IEnumerable%601>.</span></span> <span data-ttu-id="3d399-107">Zarówno okno dialogowe **Dodaj odwołanie do usługi** w programie Visual Studio, jak i narzędzie DataSvcUtil.exe są używane do generowania reprezentacji usługi OData jako klasy kontenera jednostek, która dziedziczy z <xref:System.Data.Services.Client.DataServiceContext> , a także obiektów, które reprezentują jednostki zwracane w źródłach danych.</span><span class="sxs-lookup"><span data-stu-id="3d399-107">Both the **Add Service Reference** dialog box in Visual Studio and the DataSvcUtil.exe tool are used to generate a representation of an OData service as an entity container class that inherits from <xref:System.Data.Services.Client.DataServiceContext>, as well as objects that represent the entities returned in feeds.</span></span> <span data-ttu-id="3d399-108">Narzędzia te generują również właściwości klasy kontenera jednostek dla kolekcji, które są udostępniane jako źródła danych przez usługę.</span><span class="sxs-lookup"><span data-stu-id="3d399-108">These tools also generate properties on the entity container class for the collections that are exposed as feeds by the service.</span></span> <span data-ttu-id="3d399-109">Każda z tych właściwości klasy, która hermetyzuje usługę danych, zwraca <xref:System.Data.Services.Client.DataServiceQuery%601> .</span><span class="sxs-lookup"><span data-stu-id="3d399-109">Each of these properties of the class that encapsulates the data service return a <xref:System.Data.Services.Client.DataServiceQuery%601>.</span></span> <span data-ttu-id="3d399-110">Ponieważ <xref:System.Data.Services.Client.DataServiceQuery%601> Klasa implementuje <xref:System.Linq.IQueryable%601> interfejs zdefiniowany przez LINQ, można utworzyć zapytanie LINQ względem kanałów ujawnianych przez usługę danych, które są tłumaczone przez bibliotekę kliencką na identyfikator URI żądania zapytania, który jest wysyłany do usługi danych podczas wykonywania.</span><span class="sxs-lookup"><span data-stu-id="3d399-110">Because the <xref:System.Data.Services.Client.DataServiceQuery%601> class implements the <xref:System.Linq.IQueryable%601> interface defined by LINQ, you can compose a LINQ query against feeds exposed by the data service, which are translated by the client library into a query request URI that is sent to the data service on execution.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="3d399-111">Zestaw zapytań można wyrazić elementu w składni LINQ jest szerszy niż te włączone w składni identyfikatora URI, który jest używany przez usługi danych OData.</span><span class="sxs-lookup"><span data-stu-id="3d399-111">The set of queries expressible in the LINQ syntax is broader than those enabled in the URI syntax that is used by OData data services.</span></span> <span data-ttu-id="3d399-112"><xref:System.NotSupportedException>Występuje, gdy nie można zamapować zapytania na identyfikator URI w docelowej usłudze danych.</span><span class="sxs-lookup"><span data-stu-id="3d399-112">A <xref:System.NotSupportedException> is raised when the query cannot be mapped to a URI in the target data service.</span></span> <span data-ttu-id="3d399-113">Aby uzyskać więcej informacji, zobacz [nieobsługiwane metody LINQ](linq-considerations-wcf-data-services.md#unsupportedMethods) w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="3d399-113">For more information, see the [Unsupported LINQ Methods](linq-considerations-wcf-data-services.md#unsupportedMethods) in this topic.</span></span>  
  
 <span data-ttu-id="3d399-114">Poniższy przykład to zapytanie LINQ zwracające wartość `Orders` kosztu frachtu o wartości większej niż $30 i sortuje wyniki według daty wysyłki, rozpoczynając od ostatniego dnia wysyłki:</span><span class="sxs-lookup"><span data-stu-id="3d399-114">The following example is a LINQ query that returns `Orders` that have a freight cost of more than $30 and sorts the results by the shipping date, starting with the latest ship date:</span></span>  
  
[!code-csharp[Astoria Northwind Client#AddQueryOptionsLinqSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#addqueryoptionslinqspecific)]
[!code-vb[Astoria Northwind Client#AddQueryOptionsLinqSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#addqueryoptionslinqspecific)]
  
 <span data-ttu-id="3d399-115">To zapytanie LINQ jest tłumaczone na następujący identyfikator URI zapytania, który jest wykonywany względem usługi danych [szybkiego startu](quickstart-wcf-data-services.md) opartego na bazie Northwind:</span><span class="sxs-lookup"><span data-stu-id="3d399-115">This LINQ query is translated into the following query URI that is executed against the Northwind-based [quickstart](quickstart-wcf-data-services.md) data service:</span></span>  
  
```http
http://localhost:12345/Northwind.svc/Orders?Orderby=ShippedDate&?filter=Freight gt 30  
```  
  
 <span data-ttu-id="3d399-116">Aby uzyskać więcej ogólnych informacji na temat LINQ, zobacz [Language-Integrated Query (LINQ) — C#](../../../csharp/programming-guide/concepts/linq/index.md) lub [Language-Integrated Query (linq) — Visual Basic](../../../visual-basic/programming-guide/concepts/linq/index.md).</span><span class="sxs-lookup"><span data-stu-id="3d399-116">For more general information about LINQ, see [Language-Integrated Query (LINQ) - C#](../../../csharp/programming-guide/concepts/linq/index.md) or [Language-Integrated Query (LINQ) - Visual Basic](../../../visual-basic/programming-guide/concepts/linq/index.md).</span></span>  
  
 <span data-ttu-id="3d399-117">LINQ umożliwia tworzenie zapytań przy użyciu instrukcji zapytania deklaracyjnego specyficznego dla języka, pokazanego w poprzednim przykładzie, jak również zestawu metod zapytania znanych jako standardowe operatory zapytań.</span><span class="sxs-lookup"><span data-stu-id="3d399-117">LINQ enables you to compose queries by using both the language-specific declarative query syntax, shown in the previous example, as well as a set of query methods known as standard query operators.</span></span> <span data-ttu-id="3d399-118">Równoważne zapytanie do poprzedniego przykładu może być złożone przy użyciu tylko składni opartej na metodzie, jak pokazano na poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="3d399-118">An equivalent query to the previous example can be composed by using only the method-based syntax, as shown the following example:</span></span>  
  
[!code-csharp[Astoria Northwind Client#AddQueryOptionsLinqExpressionSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#addqueryoptionslinqexpressionspecific)]
[!code-vb[Astoria Northwind Client#AddQueryOptionsLinqExpressionSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#addqueryoptionslinqexpressionspecific)]
  
 <span data-ttu-id="3d399-119">Klient Usługi danych programu WCF może przetłumaczyć oba rodzaje złożonych zapytań na identyfikator URI zapytania i można ją rozłożyć, dołączając metody zapytania do wyrażenia zapytania.</span><span class="sxs-lookup"><span data-stu-id="3d399-119">The WCF Data Services client is able to translate both kinds of composed queries into a query URI, and you can extend a LINQ query by appending query methods to a query expression.</span></span> <span data-ttu-id="3d399-120">Podczas redagowania zapytań LINQ przez dołączenie składni metody do wyrażenia zapytania lub <xref:System.Data.Services.Client.DataServiceQuery%601> , operacje są dodawane do identyfikatora URI zapytania w kolejności, w której metody są wywoływane.</span><span class="sxs-lookup"><span data-stu-id="3d399-120">When you compose LINQ queries by appending method syntax to a query expression or a <xref:System.Data.Services.Client.DataServiceQuery%601>, the operations are added to the query URI in the order in which methods are called.</span></span> <span data-ttu-id="3d399-121">Jest to równoznaczne z wywołaniem <xref:System.Data.Services.Client.DataServiceQuery%601.AddQueryOption%2A> metody w celu dodania każdej opcji zapytania do identyfikatora URI zapytania.</span><span class="sxs-lookup"><span data-stu-id="3d399-121">This is equivalent to calling the <xref:System.Data.Services.Client.DataServiceQuery%601.AddQueryOption%2A> method to add each query option to the query URI.</span></span>  
  
## <a name="executing-linq-queries"></a><span data-ttu-id="3d399-122">Wykonywanie zapytań LINQ</span><span class="sxs-lookup"><span data-stu-id="3d399-122">Executing LINQ Queries</span></span>  

 <span data-ttu-id="3d399-123">Niektóre metody zapytania LINQ, takie jak <xref:System.Linq.Enumerable.First%60%601%28System.Collections.Generic.IEnumerable%7B%60%600%7D%29> lub <xref:System.Linq.Enumerable.Single%60%601%28System.Collections.Generic.IEnumerable%7B%60%600%7D%29> , po dołączeniu do zapytania, powodują wykonanie zapytania.</span><span class="sxs-lookup"><span data-stu-id="3d399-123">Certain LINQ query methods, such as <xref:System.Linq.Enumerable.First%60%601%28System.Collections.Generic.IEnumerable%7B%60%600%7D%29> or <xref:System.Linq.Enumerable.Single%60%601%28System.Collections.Generic.IEnumerable%7B%60%600%7D%29>, when appended to the query, cause the query to be executed.</span></span> <span data-ttu-id="3d399-124">Zapytanie jest również wykonywane, gdy wyniki są wyliczane niejawnie, na przykład w `foreach` pętli lub po przypisaniu zapytania do `List` kolekcji.</span><span class="sxs-lookup"><span data-stu-id="3d399-124">A query is also executed when results are enumerated implicitly, such as during a `foreach` loop or when the query is assigned to a `List` collection.</span></span> <span data-ttu-id="3d399-125">Aby uzyskać więcej informacji, zobacz [wykonywanie zapytań dotyczących usługi danych](querying-the-data-service-wcf-data-services.md).</span><span class="sxs-lookup"><span data-stu-id="3d399-125">For more information, see [Querying the Data Service](querying-the-data-service-wcf-data-services.md).</span></span>  
  
 <span data-ttu-id="3d399-126">Klient wykonuje zapytanie LINQ w dwóch częściach.</span><span class="sxs-lookup"><span data-stu-id="3d399-126">The client executes a LINQ query in two parts.</span></span> <span data-ttu-id="3d399-127">Zawsze, gdy to możliwe, wyrażenia LINQ w zapytaniu są najpierw oceniane na kliencie, a następnie generowane jest zapytanie oparte na identyfikatorze URI i wysyłane do usługi danych w celu oceny danych w usłudze.</span><span class="sxs-lookup"><span data-stu-id="3d399-127">Whenever possible, LINQ expressions in a query are first evaluated on the client, and then a URI-based query is generated and sent to the data service for evaluation against data in the service.</span></span> <span data-ttu-id="3d399-128">Aby uzyskać więcej informacji, zapoznaj się z sekcją [klient i wykonanie serwera](querying-the-data-service-wcf-data-services.md#executingQueries) w temacie wykonywanie [zapytań do usługi danych](querying-the-data-service-wcf-data-services.md).</span><span class="sxs-lookup"><span data-stu-id="3d399-128">For more information, see the section [Client versus Server Execution](querying-the-data-service-wcf-data-services.md#executingQueries) in [Querying the Data Service](querying-the-data-service-wcf-data-services.md).</span></span>  
  
 <span data-ttu-id="3d399-129">Gdy zapytania LINQ nie można przetłumaczyć na identyfikator URI zapytania zgodnego z protokołem OData, wyjątek jest zgłaszany w przypadku próby wykonania.</span><span class="sxs-lookup"><span data-stu-id="3d399-129">When a LINQ query cannot be translated in an OData-compliant query URI, an exception is raised when execution is attempted.</span></span> <span data-ttu-id="3d399-130">Aby uzyskać więcej informacji, zobacz [wykonywanie zapytań dotyczących usługi danych](querying-the-data-service-wcf-data-services.md).</span><span class="sxs-lookup"><span data-stu-id="3d399-130">For more information, see [Querying the Data Service](querying-the-data-service-wcf-data-services.md).</span></span>  
  
## <a name="linq-query-examples"></a><span data-ttu-id="3d399-131">Przykłady zapytań LINQ</span><span class="sxs-lookup"><span data-stu-id="3d399-131">LINQ Query Examples</span></span>  

 <span data-ttu-id="3d399-132">Przykłady w poniższych sekcjach przedstawiają rodzaje zapytań LINQ, które mogą być wykonywane względem usługi OData.</span><span class="sxs-lookup"><span data-stu-id="3d399-132">The examples in the following sections demonstrate the kinds of LINQ queries that can be executed against an OData service.</span></span>  
  
<a name="filtering"></a>

### <a name="filtering"></a><span data-ttu-id="3d399-133">Filtrowanie</span><span class="sxs-lookup"><span data-stu-id="3d399-133">Filtering</span></span>  

 <span data-ttu-id="3d399-134">Przykłady zapytań LINQ w tej sekcji filtrują dane w kanale informacyjnym zwracanym przez usługę.</span><span class="sxs-lookup"><span data-stu-id="3d399-134">The LINQ query examples in this section filter data in the feed returned by the service.</span></span>  
  
 <span data-ttu-id="3d399-135">Poniższe przykłady są równoważnymi zapytaniami, które filtrują zwrócone `Orders` jednostki, dzięki czemu zwracane są tylko zamówienia o kosztach frachtu większym niż $30:</span><span class="sxs-lookup"><span data-stu-id="3d399-135">The following examples are equivalent queries that filter the returned `Orders` entities so that only orders with a freight cost greater than $30 are returned:</span></span>  
  
- <span data-ttu-id="3d399-136">Przy użyciu składni zapytania LINQ:</span><span class="sxs-lookup"><span data-stu-id="3d399-136">Using LINQ query syntax:</span></span>  
  
[!code-csharp[Astoria Northwind Client#LinqWhereClauseSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#linqwhereclausespecific)]
[!code-vb[Astoria Northwind Client#LinqWhereClauseSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#linqwhereclausespecific)]
  
- <span data-ttu-id="3d399-137">Korzystanie z metod zapytań LINQ:</span><span class="sxs-lookup"><span data-stu-id="3d399-137">Using LINQ query methods:</span></span>  
  
[!code-csharp[Astoria Northwind Client#LinqWhereMethodSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#linqwheremethodspecific)]
[!code-vb[Astoria Northwind Client#LinqWhereMethodSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#linqwheremethodspecific)]
  
- <span data-ttu-id="3d399-138">Opcja ciągu zapytania identyfikatora URI `$filter` :</span><span class="sxs-lookup"><span data-stu-id="3d399-138">The URI query string `$filter` option:</span></span>  
  
[!code-csharp[Astoria Northwind Client#ExplicitQueryWhereMethodSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#explicitquerywheremethodspecific)]
[!code-vb[Astoria Northwind Client#ExplicitQueryWhereMethodSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#explicitquerywheremethodspecific)]
  
 <span data-ttu-id="3d399-139">Wszystkie poprzednie przykłady są tłumaczone na identyfikator URI zapytania: `http://localhost:12345/northwind.svc/Orders()?$filter=Freight gt 30M` .</span><span class="sxs-lookup"><span data-stu-id="3d399-139">All of the previous examples are translated to the query URI: `http://localhost:12345/northwind.svc/Orders()?$filter=Freight gt 30M`.</span></span>  
  
<a name="sorting"></a>

### <a name="sorting"></a><span data-ttu-id="3d399-140">Sortowanie</span><span class="sxs-lookup"><span data-stu-id="3d399-140">Sorting</span></span>  

 <span data-ttu-id="3d399-141">W poniższych przykładach pokazano równoważne zapytania, które sortują zwracane dane zarówno przez nazwę firmy, jak i kod pocztowy, malejąco:</span><span class="sxs-lookup"><span data-stu-id="3d399-141">The following examples show equivalent queries that sort returned data both by the company name and by postal code, descending:</span></span>  
  
- <span data-ttu-id="3d399-142">Przy użyciu składni zapytania LINQ:</span><span class="sxs-lookup"><span data-stu-id="3d399-142">Using LINQ query syntax:</span></span>  
  
[!code-csharp[Astoria Northwind Client#LinqOrderByClauseSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#linqorderbyclausespecific)]
[!code-vb[Astoria Northwind Client#LinqOrderByClauseSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#linqorderbyclausespecific)]
  
- <span data-ttu-id="3d399-143">Korzystanie z metod zapytań LINQ:</span><span class="sxs-lookup"><span data-stu-id="3d399-143">Using LINQ query methods:</span></span>  
  
[!code-csharp[Astoria Northwind Client#LinqOrderByMethodSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#linqorderbymethodspecific)]
[!code-vb[Astoria Northwind Client#LinqOrderByMethodSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#linqorderbymethodspecific)]
  
- <span data-ttu-id="3d399-144">Opcja ciągu zapytania URI `$orderby` ):</span><span class="sxs-lookup"><span data-stu-id="3d399-144">URI query string `$orderby` option):</span></span>  
  
[!code-csharp[Astoria Northwind Client#ExplicitQueryOrderByMethodSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#explicitqueryorderbymethodspecific)]
[!code-vb[Astoria Northwind Client#ExplicitQueryOrderByMethodSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#explicitqueryorderbymethodspecific)]
  
 <span data-ttu-id="3d399-145">Wszystkie poprzednie przykłady są tłumaczone na identyfikator URI zapytania: `http://localhost:12345/northwind.svc/Customers()?$orderby=CompanyName,PostalCode desc` .</span><span class="sxs-lookup"><span data-stu-id="3d399-145">All of the previous examples are translated to the query URI: `http://localhost:12345/northwind.svc/Customers()?$orderby=CompanyName,PostalCode desc`.</span></span>  
  
<a name="projection"></a>

### <a name="projection"></a><span data-ttu-id="3d399-146">Rzut</span><span class="sxs-lookup"><span data-stu-id="3d399-146">Projection</span></span>  

 <span data-ttu-id="3d399-147">W poniższych przykładach pokazano równoważne zapytania, które program Project zwraca dane do `CustomerAddress` typu węższego:</span><span class="sxs-lookup"><span data-stu-id="3d399-147">The following examples show equivalent queries that project returned data into the narrower `CustomerAddress` type:</span></span>  
  
- <span data-ttu-id="3d399-148">Przy użyciu składni zapytania LINQ:</span><span class="sxs-lookup"><span data-stu-id="3d399-148">Using LINQ query syntax:</span></span>  
  
[!code-csharp[Astoria Northwind Client#LinqSelectClauseSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#linqselectclausespecific)]
[!code-vb[Astoria Northwind Client#LinqSelectClauseSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#linqselectclausespecific)]
  
- <span data-ttu-id="3d399-149">Korzystanie z metod zapytań LINQ:</span><span class="sxs-lookup"><span data-stu-id="3d399-149">Using LINQ query methods:</span></span>  
  
[!code-csharp[Astoria Northwind Client#LinqSelectMethodSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#linqselectmethodspecific)]
[!code-vb[Astoria Northwind Client#LinqSelectMethodSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#linqselectmethodspecific)]

> [!NOTE]
> <span data-ttu-id="3d399-150">`$select`Nie można dodać opcji zapytania do identyfikatora URI zapytania przy użyciu <xref:System.Data.Services.Client.DataServiceQuery%601.AddQueryOption%2A> metody.</span><span class="sxs-lookup"><span data-stu-id="3d399-150">The `$select` query option cannot be added to a query URI by using the <xref:System.Data.Services.Client.DataServiceQuery%601.AddQueryOption%2A> method.</span></span> <span data-ttu-id="3d399-151">Zalecamy użycie metody LINQ, <xref:System.Linq.Enumerable.Select%2A> aby klient generował `$select` opcję zapytania w identyfikatorze URI żądania.</span><span class="sxs-lookup"><span data-stu-id="3d399-151">We recommend that you use the LINQ <xref:System.Linq.Enumerable.Select%2A> method to have the client generate the `$select` query option in the request URI.</span></span>  
  
 <span data-ttu-id="3d399-152">Oba poprzednie przykłady są tłumaczone na identyfikator URI zapytania: `"http://localhost:12345/northwind.svc/Customers()?$filter=Country eq 'GerGerm'&$select=CustomerID,Address,City,Region,PostalCode,Country"` .</span><span class="sxs-lookup"><span data-stu-id="3d399-152">Both of the previous examples are translated to the query URI: `"http://localhost:12345/northwind.svc/Customers()?$filter=Country eq 'GerGerm'&$select=CustomerID,Address,City,Region,PostalCode,Country"`.</span></span>  
  
<a name="paging"></a>

### <a name="client-paging"></a><span data-ttu-id="3d399-153">Stronicowanie klienta</span><span class="sxs-lookup"><span data-stu-id="3d399-153">Client Paging</span></span>  

 <span data-ttu-id="3d399-154">W poniższych przykładach pokazano równoważne zapytania, które żądają strony posortowanych obiektów Order, które zawierają 25 zamówień, pomijając pierwsze 50 zamówień:</span><span class="sxs-lookup"><span data-stu-id="3d399-154">The following examples show equivalent queries that request a page of sorted order entities that includes 25 orders, skipping the first 50 orders:</span></span>  
  
- <span data-ttu-id="3d399-155">Stosowanie metod zapytania do zapytania LINQ:</span><span class="sxs-lookup"><span data-stu-id="3d399-155">Applying query methods to a LINQ query:</span></span>  
  
[!code-csharp[Astoria Northwind Client#LinqSkipTakeMethodSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#linqskiptakemethodspecific)]
[!code-vb[Astoria Northwind Client#LinqSkipTakeMethodSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#linqskiptakemethodspecific)]
  
- <span data-ttu-id="3d399-156">Ciąg i opcje zapytania identyfikatora URI `$skip` `$top` :</span><span class="sxs-lookup"><span data-stu-id="3d399-156">URI query string `$skip` and `$top` options):</span></span>  
  
[!code-csharp[Astoria Northwind Client#ExplicitQuerySkipTakeMethodSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#explicitqueryskiptakemethodspecific)]
[!code-vb[Astoria Northwind Client#ExplicitQuerySkipTakeMethodSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#explicitqueryskiptakemethodspecific)]
  
 <span data-ttu-id="3d399-157">Oba poprzednie przykłady są tłumaczone na identyfikator URI zapytania: `http://localhost:12345/northwind.svc/Orders()?$orderby=OrderDate desc&$skip=50&$top=25` .</span><span class="sxs-lookup"><span data-stu-id="3d399-157">Both of the previous examples are translated to the query URI: `http://localhost:12345/northwind.svc/Orders()?$orderby=OrderDate desc&$skip=50&$top=25`.</span></span>  
  
<a name="expand"></a>

### <a name="expand"></a><span data-ttu-id="3d399-158">Rozwiń</span><span class="sxs-lookup"><span data-stu-id="3d399-158">Expand</span></span>  

 <span data-ttu-id="3d399-159">Podczas wykonywania zapytania dotyczącego usługi danych OData można zażądać, aby jednostki powiązane z jednostką dodaną przez zapytanie były dołączone do zwróconego źródła danych.</span><span class="sxs-lookup"><span data-stu-id="3d399-159">When you query an OData data service, you can request that entities related to the entity targeted by the query be included the returned feed.</span></span> <span data-ttu-id="3d399-160"><xref:System.Data.Services.Client.DataServiceQuery%601.Expand%2A>Metoda jest wywoływana <xref:System.Data.Services.Client.DataServiceQuery%601> dla elementu dla zestawu jednostek przeznaczonego dla zapytania LINQ, z pokrewną nazwą zestawu jednostek podaną jako `path` parametr.</span><span class="sxs-lookup"><span data-stu-id="3d399-160">The <xref:System.Data.Services.Client.DataServiceQuery%601.Expand%2A> method is called on the <xref:System.Data.Services.Client.DataServiceQuery%601> for the entity set targeted by the LINQ query, with the related entity set name supplied as the `path` parameter.</span></span> <span data-ttu-id="3d399-161">Aby uzyskać więcej informacji, zobacz [ładowanie odroczonej zawartości](loading-deferred-content-wcf-data-services.md).</span><span class="sxs-lookup"><span data-stu-id="3d399-161">For more information, see [Loading Deferred Content](loading-deferred-content-wcf-data-services.md).</span></span>  
  
 <span data-ttu-id="3d399-162">W poniższych przykładach pokazano równoważne sposoby używania <xref:System.Data.Services.Client.DataServiceQuery%601.Expand%2A> metody w kwerendzie:</span><span class="sxs-lookup"><span data-stu-id="3d399-162">The following examples show equivalent ways to use the <xref:System.Data.Services.Client.DataServiceQuery%601.Expand%2A> method in a query:</span></span>  
  
- <span data-ttu-id="3d399-163">W składni zapytania LINQ:</span><span class="sxs-lookup"><span data-stu-id="3d399-163">In LINQ query syntax:</span></span>  
  
[!code-csharp[Astoria Northwind Client#LinqQueryExpandSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#linqqueryexpandspecific)]
[!code-vb[Astoria Northwind Client#LinqQueryExpandSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#linqqueryexpandspecific)]  
  
- <span data-ttu-id="3d399-164">Z metodami zapytań LINQ:</span><span class="sxs-lookup"><span data-stu-id="3d399-164">With LINQ query methods:</span></span>  

[!code-csharp[Astoria Northwind Client#LinqQueryExpandMethodSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#linqqueryexpandmethodspecific)]
[!code-vb[Astoria Northwind Client#LinqQueryExpandMethodSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#linqqueryexpandmethodspecific)]

 <span data-ttu-id="3d399-165">Oba poprzednie przykłady są tłumaczone na identyfikator URI zapytania: `http://localhost:12345/northwind.svc/Orders()?$filter=CustomerID eq 'ALFKI'&$expand=Order_Details` .</span><span class="sxs-lookup"><span data-stu-id="3d399-165">Both of the previous examples are translated to the query URI: `http://localhost:12345/northwind.svc/Orders()?$filter=CustomerID eq 'ALFKI'&$expand=Order_Details`.</span></span>  
  
<a name="unsupportedMethods"></a>

## <a name="unsupported-linq-methods"></a><span data-ttu-id="3d399-166">Nieobsługiwane metody LINQ</span><span class="sxs-lookup"><span data-stu-id="3d399-166">Unsupported LINQ Methods</span></span>  

 <span data-ttu-id="3d399-167">Poniższa tabela zawiera klasy metod LINQ, które nie są obsługiwane i nie mogą być uwzględniane w zapytaniach wykonywanych względem usługi OData:</span><span class="sxs-lookup"><span data-stu-id="3d399-167">The following table contains the classes of LINQ methods are not supported and cannot be included in a query executed against an OData service:</span></span>  
  
|<span data-ttu-id="3d399-168">Typ operacji</span><span class="sxs-lookup"><span data-stu-id="3d399-168">Operation Type</span></span>|<span data-ttu-id="3d399-169">Nieobsługiwana Metoda</span><span class="sxs-lookup"><span data-stu-id="3d399-169">Unsupported Method</span></span>|  
|--------------------|------------------------|  
|<span data-ttu-id="3d399-170">Ustaw operatory</span><span class="sxs-lookup"><span data-stu-id="3d399-170">Set operators</span></span>|<span data-ttu-id="3d399-171">Wszystkie operatory zestawów są nieobsługiwane w odniesieniu do elementu <xref:System.Data.Services.Client.DataServiceQuery%601> , który obejmuje następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="3d399-171">All set operators are unsupported against a <xref:System.Data.Services.Client.DataServiceQuery%601>, which included the following:</span></span><br /><br /> -   <xref:System.Linq.Enumerable.All%2A><br />-   <xref:System.Linq.Enumerable.Any%2A><br />-   <xref:System.Linq.Enumerable.Concat%2A><br />-   <xref:System.Linq.Enumerable.DefaultIfEmpty%2A><br />-   <xref:System.Linq.Enumerable.Distinct%2A><br />-   <xref:System.Linq.Enumerable.Except%2A><br />-   <xref:System.Linq.Enumerable.Intersect%2A><br />-   <xref:System.Linq.Enumerable.Union%2A><br />-   <xref:System.Linq.Enumerable.Zip%2A>|  
|<span data-ttu-id="3d399-172">Operatory porządkowania</span><span class="sxs-lookup"><span data-stu-id="3d399-172">Ordering operators</span></span>|<span data-ttu-id="3d399-173">Następujące operatory porządkowania, które wymagają, nie <xref:System.Collections.Generic.IComparer%601> są obsługiwane w przypadku <xref:System.Data.Services.Client.DataServiceQuery%601> :</span><span class="sxs-lookup"><span data-stu-id="3d399-173">The following ordering operators that require <xref:System.Collections.Generic.IComparer%601> are unsupported against a <xref:System.Data.Services.Client.DataServiceQuery%601>:</span></span><br /><br /> -   <xref:System.Linq.Enumerable.OrderBy%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%2CSystem.Collections.Generic.IComparer%7B%60%601%7D%29><br />-   <xref:System.Linq.Enumerable.OrderByDescending%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%2CSystem.Collections.Generic.IComparer%7B%60%601%7D%29><br />-   <xref:System.Linq.Enumerable.ThenBy%60%602%28System.Linq.IOrderedEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%2CSystem.Collections.Generic.IComparer%7B%60%601%7D%29><br />-   <xref:System.Linq.Enumerable.ThenByDescending%60%602%28System.Linq.IOrderedEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%2CSystem.Collections.Generic.IComparer%7B%60%601%7D%29>|  
|<span data-ttu-id="3d399-174">Operatory projekcji i filtrowania</span><span class="sxs-lookup"><span data-stu-id="3d399-174">Projection and filtering operators</span></span>|<span data-ttu-id="3d399-175">Następujące operatory rzutowania i filtrowania, które akceptują argument pozycyjny, nie są obsługiwane dla <xref:System.Data.Services.Client.DataServiceQuery%601> :</span><span class="sxs-lookup"><span data-stu-id="3d399-175">The following projection and filtering operators that accept a positional argument are unsupported against a <xref:System.Data.Services.Client.DataServiceQuery%601>:</span></span><br /><br /> -   <xref:System.Linq.Enumerable.Join%60%604%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%2CSystem.Func%7B%60%600%2C%60%602%7D%2CSystem.Func%7B%60%601%2C%60%602%7D%2CSystem.Func%7B%60%600%2C%60%601%2C%60%603%7D%2CSystem.Collections.Generic.IEqualityComparer%7B%60%602%7D%29><br />-   <xref:System.Linq.Enumerable.Select%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2CSystem.Int32%2C%60%601%7D%29><br />-   <xref:System.Linq.Enumerable.SelectMany%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%7D%29><br />-   <xref:System.Linq.Enumerable.SelectMany%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2CSystem.Int32%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%7D%29><br />-   <xref:System.Linq.Enumerable.SelectMany%60%603%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%7D%2CSystem.Func%7B%60%600%2C%60%601%2C%60%602%7D%29><br />-   <xref:System.Linq.Enumerable.SelectMany%60%603%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2CSystem.Int32%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%7D%2CSystem.Func%7B%60%600%2C%60%601%2C%60%602%7D%29><br />-   <xref:System.Linq.Enumerable.Where%60%601%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2CSystem.Int32%2CSystem.Boolean%7D%29>|  
|<span data-ttu-id="3d399-176">Operatory grupowania</span><span class="sxs-lookup"><span data-stu-id="3d399-176">Grouping operators</span></span>|<span data-ttu-id="3d399-177">Wszystkie operatory grupowania są nieobsługiwane w programie <xref:System.Data.Services.Client.DataServiceQuery%601> , w tym:</span><span class="sxs-lookup"><span data-stu-id="3d399-177">All grouping operators are unsupported against a <xref:System.Data.Services.Client.DataServiceQuery%601>, including the following:</span></span><br /><br /> -   <xref:System.Linq.Enumerable.GroupBy%2A><br />-   <xref:System.Linq.Enumerable.GroupJoin%2A><br /><br /> <span data-ttu-id="3d399-178">Na kliencie należy wykonać operacje grupowania.</span><span class="sxs-lookup"><span data-stu-id="3d399-178">Grouping operations must be performed on the client.</span></span>|  
|<span data-ttu-id="3d399-179">Operatory agregujące</span><span class="sxs-lookup"><span data-stu-id="3d399-179">Aggregate operators</span></span>|<span data-ttu-id="3d399-180">Wszystkie operacje agregacji są nieobsługiwane w odniesieniu do programu <xref:System.Data.Services.Client.DataServiceQuery%601> , w tym:</span><span class="sxs-lookup"><span data-stu-id="3d399-180">All aggregate operations are unsupported against a <xref:System.Data.Services.Client.DataServiceQuery%601>, including the following:</span></span><br /><br /> -   <xref:System.Linq.Enumerable.Aggregate%2A><br />-   <xref:System.Linq.Enumerable.Average%2A><br />-   <xref:System.Linq.Enumerable.Count%2A><br />-   <xref:System.Linq.Enumerable.LongCount%2A><br />-   <xref:System.Linq.Enumerable.Max%2A><br />-   <xref:System.Linq.Enumerable.Min%2A><br />-   <xref:System.Linq.Enumerable.Sum%2A><br /><br /> <span data-ttu-id="3d399-181">Operacje agregujące muszą być wykonywane na kliencie lub być hermetyzowane przez operację usługi.</span><span class="sxs-lookup"><span data-stu-id="3d399-181">Aggregate operations must either be performed on the client or be encapsulated by a service operation.</span></span>|  
|<span data-ttu-id="3d399-182">Operatory stronicowania</span><span class="sxs-lookup"><span data-stu-id="3d399-182">Paging operators</span></span>|<span data-ttu-id="3d399-183">Następujące operatory stronicowania nie są obsługiwane w przypadku <xref:System.Data.Services.Client.DataServiceQuery%601> :</span><span class="sxs-lookup"><span data-stu-id="3d399-183">The following paging operators are not supported against a <xref:System.Data.Services.Client.DataServiceQuery%601>:</span></span><br /><br /> -   <xref:System.Linq.Enumerable.ElementAt%2A><br />-   <xref:System.Linq.Enumerable.Last%2A><br />-   <xref:System.Linq.Enumerable.LastOrDefault%2A><br />-   <xref:System.Linq.Enumerable.SkipWhile%2A><br />-   <xref:System.Linq.Enumerable.TakeWhile%2A><br/><br/><span data-ttu-id="3d399-184">**Uwaga:**  Operatory stronicowania wykonywane na pustej sekwencji zwracają wartość null.</span><span class="sxs-lookup"><span data-stu-id="3d399-184">**Note:**  Paging operators that are executed on an empty sequence return null.</span></span>|  
|<span data-ttu-id="3d399-185">Inne operatory</span><span class="sxs-lookup"><span data-stu-id="3d399-185">Other operators</span></span>|<span data-ttu-id="3d399-186">Następujące operatory nie są również obsługiwane w przypadku <xref:System.Data.Services.Client.DataServiceQuery%601> :</span><span class="sxs-lookup"><span data-stu-id="3d399-186">The following operators are also not supported against a <xref:System.Data.Services.Client.DataServiceQuery%601>:</span></span><br /><br /> - <xref:System.Linq.Enumerable.Empty%2A><br />- <xref:System.Linq.Enumerable.Range%2A><br />- <xref:System.Linq.Enumerable.Repeat%2A><br />- <xref:System.Linq.Enumerable.ToDictionary%2A><br />- <xref:System.Linq.Enumerable.ToLookup%2A>|  
  
<a name="supportedExpressions"></a>

## <a name="supported-expression-functions"></a><span data-ttu-id="3d399-187">Obsługiwane funkcje wyrażeń</span><span class="sxs-lookup"><span data-stu-id="3d399-187">Supported Expression Functions</span></span>  

 <span data-ttu-id="3d399-188">Obsługiwane są następujące metody i właściwości środowiska uruchomieniowego języka wspólnego (CLR), ponieważ mogą one być tłumaczone w wyrażeniu zapytania w celu uwzględnienia w identyfikatorze URI żądania do usługi OData:</span><span class="sxs-lookup"><span data-stu-id="3d399-188">The following common-language runtime (CLR) methods and properties are supported because they can be translated in a query expression for inclusion in the request URI to an OData service:</span></span>  
  
|<span data-ttu-id="3d399-189"><xref:System.String> Członkiem</span><span class="sxs-lookup"><span data-stu-id="3d399-189"><xref:System.String> Member</span></span>|<span data-ttu-id="3d399-190">Obsługiwana funkcja OData</span><span class="sxs-lookup"><span data-stu-id="3d399-190">Supported OData Function</span></span>|  
|-----------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|  
|<xref:System.String.Concat%28System.String%2CSystem.String%29>|`string concat(string p0, string p1)`|  
|<xref:System.String.Contains%28System.String%29>|`bool substringof(string p0, string p1)`|  
|<xref:System.String.EndsWith%28System.String%29>|`bool endswith(string p0, string p1)`|  
|<xref:System.String.IndexOf%28System.String%2CSystem.Int32%29>|`int indexof(string p0, string p1)`|  
|<xref:System.String.Length>|`int length(string p0)`|  
|<xref:System.String.Replace%28System.String%2CSystem.String%29>|`string replace(string p0, string find, string replace)`|  
|<xref:System.String.Substring%28System.Int32%29>|`string substring(string p0, int pos)`|  
|<xref:System.String.Substring%28System.Int32%2CSystem.Int32%29>|`string substring(string p0, int pos, int length)`|  
|<xref:System.String.ToLower>|`string tolower(string p0)`|  
|<xref:System.String.ToUpper>|`string toupper(string p0)`|  
|<xref:System.String.Trim>|`string trim(string p0)`|  
  
|<span data-ttu-id="3d399-191"><xref:System.DateTime> Członek<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="3d399-191"><xref:System.DateTime> Member<sup>1</sup></span></span>|<span data-ttu-id="3d399-192">Obsługiwana funkcja OData</span><span class="sxs-lookup"><span data-stu-id="3d399-192">Supported OData Function</span></span>|  
|-------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|  
|<xref:System.DateTime.Day>|`int day(DateTime p0)`|  
|<xref:System.DateTime.Hour>|`int hour(DateTime p0)`|  
|<xref:System.DateTime.Minute>|`int minute(DateTime p0)`|  
|<xref:System.DateTime.Month>|`int month(DateTime p0)`|  
|<xref:System.DateTime.Second>|`int second(DateTime p0)`|  
|<xref:System.DateTime.Year>|`int year(DateTime p0)`|  
  
 <span data-ttu-id="3d399-193"><sup>1</sup> Obsługiwane są również równoważne właściwości daty i godziny <xref:Microsoft.VisualBasic.DateAndTime?displayProperty=nameWithType> oraz <xref:Microsoft.VisualBasic.DateAndTime.DatePart%2A> metoda w Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="3d399-193"><sup>1</sup>The equivalent date and time properties of <xref:Microsoft.VisualBasic.DateAndTime?displayProperty=nameWithType> and the <xref:Microsoft.VisualBasic.DateAndTime.DatePart%2A> method in Visual Basic are also supported.</span></span>  
  
|<span data-ttu-id="3d399-194"><xref:System.Math> Członkiem</span><span class="sxs-lookup"><span data-stu-id="3d399-194"><xref:System.Math> Member</span></span>|<span data-ttu-id="3d399-195">Obsługiwana funkcja OData</span><span class="sxs-lookup"><span data-stu-id="3d399-195">Supported OData Function</span></span>|  
|---------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|  
|<xref:System.Math.Ceiling%28System.Decimal%29>|`decimal ceiling(decimal p0)`|  
|<xref:System.Math.Ceiling%28System.Double%29>|`double ceiling(double p0)`|  
|<xref:System.Math.Floor%28System.Decimal%29>|`decimal floor(decimal p0)`|  
|<xref:System.Math.Floor%28System.Double%29>|`double floor(double p0)`|  
|<xref:System.Math.Round%28System.Decimal%29>|`decimal round(decimal p0)`|  
|<xref:System.Math.Round%28System.Double%29>|`double round(double p0)`|  
  
|<span data-ttu-id="3d399-196"><xref:System.Linq.Expressions.Expression> Członkiem</span><span class="sxs-lookup"><span data-stu-id="3d399-196"><xref:System.Linq.Expressions.Expression> Member</span></span>|<span data-ttu-id="3d399-197">Obsługiwana funkcja OData</span><span class="sxs-lookup"><span data-stu-id="3d399-197">Supported OData Function</span></span>|  
|---------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|  
|<xref:System.Linq.Expressions.Expression.TypeIs%28System.Linq.Expressions.Expression%2CSystem.Type%29>|`bool isof(type p0)`|  
  
 <span data-ttu-id="3d399-198">Klient może również mieć możliwość oszacowania dodatkowych funkcji CLR na kliencie.</span><span class="sxs-lookup"><span data-stu-id="3d399-198">The client may also be able to evaluate additional CLR functions on the client.</span></span> <span data-ttu-id="3d399-199">Element <xref:System.NotSupportedException> jest wywoływany dla dowolnego wyrażenia, które nie może zostać obliczone na kliencie i nie może zostać przetłumaczone na prawidłowy identyfikator URI żądania na potrzeby oceny na serwerze.</span><span class="sxs-lookup"><span data-stu-id="3d399-199">A <xref:System.NotSupportedException> is raised for any expression that cannot be evaluated on the client and cannot be translated into a valid request URI for evaluation on the server.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="3d399-200">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="3d399-200">See also</span></span>

- [<span data-ttu-id="3d399-201">Wykonywanie zapytań do usługi danych</span><span class="sxs-lookup"><span data-stu-id="3d399-201">Querying the Data Service</span></span>](querying-the-data-service-wcf-data-services.md)
- [<span data-ttu-id="3d399-202">Projekcje zapytania</span><span class="sxs-lookup"><span data-stu-id="3d399-202">Query Projections</span></span>](query-projections-wcf-data-services.md)
- [<span data-ttu-id="3d399-203">Materializacja obiektu</span><span class="sxs-lookup"><span data-stu-id="3d399-203">Object Materialization</span></span>](object-materialization-wcf-data-services.md)
- [<span data-ttu-id="3d399-204">OData: konwencje URI</span><span class="sxs-lookup"><span data-stu-id="3d399-204">OData: URI Conventions</span></span>](https://www.odata.org/documentation/odata-version-2-0/uri-conventions/)
