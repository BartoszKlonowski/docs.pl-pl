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
# <a name="namespaces-entity-sql"></a>Przestrzenie nazw (Entity SQL)

[!INCLUDE[esql](../../../../../../includes/esql-md.md)] wprowadza przestrzenie nazw, aby uniknąć konfliktów nazw dla identyfikatorów globalnych, takich jak nazwy typów, zestawy jednostek, funkcje i tak dalej. Obsługa przestrzeni nazw w programie [!INCLUDE[esql](../../../../../../includes/esql-md.md)] jest podobna do obsługi przestrzeni nazw w .NET Framework.  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] Program udostępnia dwie formy klauzuli USING: kwalifikowane przestrzenie nazw (gdzie dla przestrzeni nazw jest określony krótszy alias) i niekwalifikowane obszary nazw, jak pokazano w następującym przykładzie:  
  
 `USING System.Data;`  
  
 `USING tsql = System.Data;`  
  
## <a name="name-resolution-rules"></a>Reguły rozpoznawania nazw  

 Jeśli nie można rozpoznać identyfikatora w lokalnych zakresach, program [!INCLUDE[esql](../../../../../../includes/esql-md.md)] próbuje zlokalizować nazwę w globalnych zakresach (przestrzeni nazw). [!INCLUDE[esql](../../../../../../includes/esql-md.md)] najpierw próbuje dopasować identyfikator (prefiks) do jednego z kwalifikowanych przestrzeni nazw. Jeśli istnieje dopasowanie, program [!INCLUDE[esql](../../../../../../includes/esql-md.md)] podejmie próbę rozpoznania reszty identyfikatora w podanej przestrzeni nazw. Jeśli nie zostanie znalezione dopasowanie, zostanie zgłoszony wyjątek.  
  
 Następnie program [!INCLUDE[esql](../../../../../../includes/esql-md.md)] próbuje przeszukać wszystkie niekwalifikowane przestrzenie nazw (określone w prologu) dla identyfikatora. Jeśli identyfikator może znajdować się w dokładnie jednej przestrzeni nazw, Ta lokalizacja jest zwracana. Jeśli więcej niż jedna przestrzeń nazw ma dopasowanie dla tego identyfikatora, zgłaszany jest wyjątek. Jeśli dla identyfikatora nie można zidentyfikować żadnej przestrzeni nazw, [!INCLUDE[esql](../../../../../../includes/esql-md.md)] przekazuje nazwę do następnego zakresu ( <xref:System.Data.Common.DbCommand> lub <xref:System.Data.Common.DbConnection> obiektu), jak pokazano w następującym przykładzie:  
  
```sql  
SELECT TREAT(p AS NamespaceName.Employee)  
FROM ContainerName.Person AS p  
WHERE p IS OF (NamespaceName.Employee)  
```  
  
## <a name="differences-from-the-net-framework"></a>Różnice między .NET Framework  

 W .NET Framework można użyć częściowo kwalifikowanych przestrzeni nazw. [!INCLUDE[esql](../../../../../../includes/esql-md.md)] nie zezwala na to.  
  
## <a name="adonet-usage"></a>ADO.NET użycie  

 Zapytania są wyrażane za poorednictwem <xref:System.Data.Common.DbCommand> obiektów ADO.NET. <xref:System.Data.Common.DbCommand> obiekty mogą być kompilowane względem <xref:System.Data.Common.DbConnection> obiektów. Przestrzenie nazw można także określić jako część <xref:System.Data.Common.DbCommand> obiektów i <xref:System.Data.Common.DbConnection> . Jeśli [!INCLUDE[esql](../../../../../../includes/esql-md.md)] nie można rozpoznać identyfikatora wewnątrz zapytania, zewnętrzne przestrzenie nazw są badane (na podstawie podobnych reguł).  
  
## <a name="see-also"></a>Zobacz też

- [Odwołanie do jednostki SQL](entity-sql-reference.md)
- [Omówienie jednostki SQL](entity-sql-overview.md)
