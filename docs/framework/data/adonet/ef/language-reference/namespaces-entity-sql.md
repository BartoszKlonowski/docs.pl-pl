---
title: Przestrzenie nazw (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 83991c21-60db-4af9-aca3-b416f6cae98e
ms.openlocfilehash: 7a53f8e7e70dbc9fa505f7f8619af10a0e44c331
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91197810"
---
# <a name="namespaces-entity-sql"></a><span data-ttu-id="cf06c-102">Przestrzenie nazw (Entity SQL)</span><span class="sxs-lookup"><span data-stu-id="cf06c-102">Namespaces (Entity SQL)</span></span>

[!INCLUDE[esql](../../../../../../includes/esql-md.md)] <span data-ttu-id="cf06c-103">wprowadza przestrzenie nazw, aby uniknąć konfliktów nazw dla identyfikatorów globalnych, takich jak nazwy typów, zestawy jednostek, funkcje i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="cf06c-103">introduces namespaces to avoid name conflicts for global identifiers such as type names, entity sets, functions, and so on.</span></span> <span data-ttu-id="cf06c-104">Obsługa przestrzeni nazw w programie [!INCLUDE[esql](../../../../../../includes/esql-md.md)] jest podobna do obsługi przestrzeni nazw w .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="cf06c-104">The namespace support in [!INCLUDE[esql](../../../../../../includes/esql-md.md)] is similar to the namespace support in the .NET Framework.</span></span>  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] <span data-ttu-id="cf06c-105">Program udostępnia dwie formy klauzuli USING: kwalifikowane przestrzenie nazw (gdzie dla przestrzeni nazw jest określony krótszy alias) i niekwalifikowane obszary nazw, jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="cf06c-105">provides two forms of the USING clause: qualified namespaces (where a shorter alias is provided for the namespace), and unqualified namespaces, as illustrated in the following example:</span></span>  
  
 `USING System.Data;`  
  
 `USING tsql = System.Data;`  
  
## <a name="name-resolution-rules"></a><span data-ttu-id="cf06c-106">Reguły rozpoznawania nazw</span><span class="sxs-lookup"><span data-stu-id="cf06c-106">Name Resolution Rules</span></span>  

 <span data-ttu-id="cf06c-107">Jeśli nie można rozpoznać identyfikatora w lokalnych zakresach, program [!INCLUDE[esql](../../../../../../includes/esql-md.md)] próbuje zlokalizować nazwę w globalnych zakresach (przestrzeni nazw).</span><span class="sxs-lookup"><span data-stu-id="cf06c-107">If an identifier cannot be resolved in the local scopes, [!INCLUDE[esql](../../../../../../includes/esql-md.md)] tries to locate the name in the global scopes (the namespaces).</span></span> [!INCLUDE[esql](../../../../../../includes/esql-md.md)] <span data-ttu-id="cf06c-108">najpierw próbuje dopasować identyfikator (prefiks) do jednego z kwalifikowanych przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="cf06c-108">first tries to match the identifier (prefix) with one of the qualified namespaces.</span></span> <span data-ttu-id="cf06c-109">Jeśli istnieje dopasowanie, program [!INCLUDE[esql](../../../../../../includes/esql-md.md)] podejmie próbę rozpoznania reszty identyfikatora w podanej przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="cf06c-109">If there is a match, [!INCLUDE[esql](../../../../../../includes/esql-md.md)] tries to resolve the rest of the identifier in the specified namespace.</span></span> <span data-ttu-id="cf06c-110">Jeśli nie zostanie znalezione dopasowanie, zostanie zgłoszony wyjątek.</span><span class="sxs-lookup"><span data-stu-id="cf06c-110">If no match is found, an exception is thrown.</span></span>  
  
 <span data-ttu-id="cf06c-111">Następnie program [!INCLUDE[esql](../../../../../../includes/esql-md.md)] próbuje przeszukać wszystkie niekwalifikowane przestrzenie nazw (określone w prologu) dla identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="cf06c-111">Next, [!INCLUDE[esql](../../../../../../includes/esql-md.md)] tries to search all unqualified namespaces (specified in the prolog) for the identifier.</span></span> <span data-ttu-id="cf06c-112">Jeśli identyfikator może znajdować się w dokładnie jednej przestrzeni nazw, Ta lokalizacja jest zwracana.</span><span class="sxs-lookup"><span data-stu-id="cf06c-112">If the identifier can be located in exactly one namespace, that location is returned.</span></span> <span data-ttu-id="cf06c-113">Jeśli więcej niż jedna przestrzeń nazw ma dopasowanie dla tego identyfikatora, zgłaszany jest wyjątek.</span><span class="sxs-lookup"><span data-stu-id="cf06c-113">If more than one namespace has a match for that identifier, an exception is thrown.</span></span> <span data-ttu-id="cf06c-114">Jeśli dla identyfikatora nie można zidentyfikować żadnej przestrzeni nazw, [!INCLUDE[esql](../../../../../../includes/esql-md.md)] przekazuje nazwę do następnego zakresu ( <xref:System.Data.Common.DbCommand> lub <xref:System.Data.Common.DbConnection> obiektu), jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="cf06c-114">If no namespace can be identified for the identifier, [!INCLUDE[esql](../../../../../../includes/esql-md.md)] passes the name onto the next outward scope (the <xref:System.Data.Common.DbCommand> or <xref:System.Data.Common.DbConnection> object), as illustrated in the following example:</span></span>  
  
```sql  
SELECT TREAT(p AS NamespaceName.Employee)  
FROM ContainerName.Person AS p  
WHERE p IS OF (NamespaceName.Employee)  
```  
  
## <a name="differences-from-the-net-framework"></a><span data-ttu-id="cf06c-115">Różnice między .NET Framework</span><span class="sxs-lookup"><span data-stu-id="cf06c-115">Differences from the .NET Framework</span></span>  

 <span data-ttu-id="cf06c-116">W .NET Framework można użyć częściowo kwalifikowanych przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="cf06c-116">In the .NET Framework, you can use partially qualified namespaces.</span></span> [!INCLUDE[esql](../../../../../../includes/esql-md.md)] <span data-ttu-id="cf06c-117">nie zezwala na to.</span><span class="sxs-lookup"><span data-stu-id="cf06c-117">does not allow this.</span></span>  
  
## <a name="adonet-usage"></a><span data-ttu-id="cf06c-118">ADO.NET użycie</span><span class="sxs-lookup"><span data-stu-id="cf06c-118">ADO.NET Usage</span></span>  

 <span data-ttu-id="cf06c-119">Zapytania są wyrażane za poorednictwem <xref:System.Data.Common.DbCommand> obiektów ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="cf06c-119">Queries are expressed through ADO.NET <xref:System.Data.Common.DbCommand> objects.</span></span> <span data-ttu-id="cf06c-120"><xref:System.Data.Common.DbCommand> obiekty mogą być kompilowane względem <xref:System.Data.Common.DbConnection> obiektów.</span><span class="sxs-lookup"><span data-stu-id="cf06c-120"><xref:System.Data.Common.DbCommand> objects can be built over <xref:System.Data.Common.DbConnection> objects.</span></span> <span data-ttu-id="cf06c-121">Przestrzenie nazw można także określić jako część <xref:System.Data.Common.DbCommand> obiektów i <xref:System.Data.Common.DbConnection> .</span><span class="sxs-lookup"><span data-stu-id="cf06c-121">Namespaces can also be specified as part of the <xref:System.Data.Common.DbCommand> and <xref:System.Data.Common.DbConnection> objects.</span></span> <span data-ttu-id="cf06c-122">Jeśli [!INCLUDE[esql](../../../../../../includes/esql-md.md)] nie można rozpoznać identyfikatora wewnątrz zapytania, zewnętrzne przestrzenie nazw są badane (na podstawie podobnych reguł).</span><span class="sxs-lookup"><span data-stu-id="cf06c-122">If [!INCLUDE[esql](../../../../../../includes/esql-md.md)] cannot resolve an identifier within the query itself, the external namespaces are probed (based on similar rules).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="cf06c-123">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="cf06c-123">See also</span></span>

- [<span data-ttu-id="cf06c-124">Odwołanie do jednostki SQL</span><span class="sxs-lookup"><span data-stu-id="cf06c-124">Entity SQL Reference</span></span>](entity-sql-reference.md)
- [<span data-ttu-id="cf06c-125">Omówienie jednostki SQL</span><span class="sxs-lookup"><span data-stu-id="cf06c-125">Entity SQL Overview</span></span>](entity-sql-overview.md)
