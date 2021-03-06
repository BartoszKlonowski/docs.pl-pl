---
title: Składnia wyrażeń dla standardowych operatorów zapytań
ms.date: 07/20/2015
ms.assetid: eb978d86-d3b5-497b-95ce-a054bea8f510
ms.openlocfilehash: 57a08f6540cbf3e091ee1b2e202e0e181487e3be
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/23/2020
ms.locfileid: "91090251"
---
# <a name="query-expression-syntax-for-standard-query-operators-visual-basic"></a>Składnia wyrażenia zapytania dla standardowych operatorów zapytań (Visual Basic)

Niektóre często używane standardowe operatory zapytań mają dedykowaną składnię słowa kluczowego Visual Basic języka, która umożliwia ich wywoływanie jako część *wyrażenia zapytania*. Wyrażenie zapytania jest inną, bardziej czytelną formą wyrażenia zapytania niż jego odpowiednik *oparty na metodzie*  . Klauzule wyrażenia zapytania są tłumaczone na wywołania metod zapytania w czasie kompilacji.  
  
## <a name="query-expression-syntax-table"></a>Tabela składni wyrażeń zapytania  

 W poniższej tabeli wymieniono standardowe operatory zapytań, które mają równoważne klauzule wyrażenia zapytania.  
  
|Metoda|Składnia wyrażenia zapytania Visual Basic|  
|------------|------------------------------------------|  
|<xref:System.Linq.Enumerable.All%2A>|`Aggregate … In … Into All(…)`<br /><br /> (Aby uzyskać więcej informacji, zobacz [klauzula agregująca](../../../language-reference/queries/aggregate-clause.md)).|  
|<xref:System.Linq.Enumerable.Any%2A>|`Aggregate … In … Into Any()`<br /><br /> (Aby uzyskać więcej informacji, zobacz [klauzula agregująca](../../../language-reference/queries/aggregate-clause.md)).|  
|<xref:System.Linq.Enumerable.Average%2A>|`Aggregate … In … Into Average()`<br /><br /> (Aby uzyskać więcej informacji, zobacz [klauzula agregująca](../../../language-reference/queries/aggregate-clause.md)).|  
|<xref:System.Linq.Enumerable.Cast%2A>|`From … As …`<br /><br /> (Aby uzyskać więcej informacji, zobacz [klauzula FROM](../../../language-reference/queries/from-clause.md)).|  
|<xref:System.Linq.Enumerable.Count%2A>|`Aggregate … In … Into Count()`<br /><br /> (Aby uzyskać więcej informacji, zobacz [klauzula agregująca](../../../language-reference/queries/aggregate-clause.md)).|  
|<xref:System.Linq.Enumerable.Distinct%60%601%28System.Collections.Generic.IEnumerable%7B%60%600%7D%29>|`Distinct`<br /><br /> (Aby uzyskać więcej informacji, zobacz [klauzula DISTINCT](../../../language-reference/queries/distinct-clause.md)).|  
|<xref:System.Linq.Enumerable.GroupBy%2A>|`Group … By … Into …`<br /><br /> (Aby uzyskać więcej informacji, zobacz [klauzula GROUP by](../../../language-reference/queries/group-by-clause.md).)|  
|<xref:System.Linq.Enumerable.GroupJoin%60%604%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%2CSystem.Func%7B%60%600%2C%60%602%7D%2CSystem.Func%7B%60%601%2C%60%602%7D%2CSystem.Func%7B%60%600%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%2C%60%603%7D%29>|`Group Join … In … On …`<br /><br /> (Aby uzyskać więcej informacji, zobacz [Klauzula join Group](../../../language-reference/queries/group-join-clause.md).)|  
|<xref:System.Linq.Enumerable.Join%60%604%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%2CSystem.Func%7B%60%600%2C%60%602%7D%2CSystem.Func%7B%60%601%2C%60%602%7D%2CSystem.Func%7B%60%600%2C%60%601%2C%60%603%7D%29>|`From x In …, y In … Where x.a = b.a`<br /><br /> -lub-<br /><br /> `Join … [As …]In … On …`<br /><br /> (Aby uzyskać więcej informacji, zobacz [Klauzula join](../../../language-reference/queries/join-clause.md)).|  
|<xref:System.Linq.Enumerable.LongCount%2A>|`Aggregate … In … Into LongCount()`<br /><br /> (Aby uzyskać więcej informacji, zobacz [klauzula agregująca](../../../language-reference/queries/aggregate-clause.md)).|  
|<xref:System.Linq.Enumerable.Max%2A>|`Aggregate … In … Into Max()`<br /><br /> (Aby uzyskać więcej informacji, zobacz [klauzula agregująca](../../../language-reference/queries/aggregate-clause.md)).|  
|<xref:System.Linq.Enumerable.Min%2A>|`Aggregate … In … Into Min()`<br /><br /> (Aby uzyskać więcej informacji, zobacz [klauzula agregująca](../../../language-reference/queries/aggregate-clause.md)).|  
|<xref:System.Linq.Enumerable.OrderBy%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%29>|`Order By`<br /><br /> (Aby uzyskać więcej informacji, zobacz [klauzula Order by](../../../language-reference/queries/order-by-clause.md).)|  
|<xref:System.Linq.Enumerable.OrderByDescending%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%29>|`Order By … Descending`<br /><br /> (Aby uzyskać więcej informacji, zobacz [klauzula Order by](../../../language-reference/queries/order-by-clause.md).)|  
|<xref:System.Linq.Enumerable.Select%2A>|`Select`<br /><br /> (Aby uzyskać więcej informacji, zobacz [klauzula SELECT](../../../language-reference/queries/select-clause.md).).|  
|<xref:System.Linq.Enumerable.SelectMany%2A>|Wiele `From` klauzul<br /><br /> (Aby uzyskać więcej informacji, zobacz [klauzula FROM](../../../language-reference/queries/from-clause.md)).|  
|<xref:System.Linq.Enumerable.Skip%2A>|`Skip`<br /><br /> (Aby uzyskać więcej informacji, zobacz [klauzula Skip](../../../language-reference/queries/skip-clause.md)).|  
|<xref:System.Linq.Enumerable.SkipWhile%2A>|`Skip While`<br /><br /> (Aby uzyskać więcej informacji, zobacz [klauzula Skip While](../../../language-reference/queries/skip-while-clause.md).)|  
|<xref:System.Linq.Enumerable.Sum%2A>|`Aggregate … In … Into Sum()`<br /><br /> (Aby uzyskać więcej informacji, zobacz [klauzula agregująca](../../../language-reference/queries/aggregate-clause.md)).|  
|<xref:System.Linq.Enumerable.Take%2A>|`Take`<br /><br /> (Aby uzyskać więcej informacji, zobacz [klauzula Take](../../../language-reference/queries/take-clause.md).).|  
|<xref:System.Linq.Enumerable.TakeWhile%2A>|`Take While`<br /><br /> (Aby uzyskać więcej informacji, zobacz [klauzula Take While](../../../language-reference/queries/take-while-clause.md).)|  
|<xref:System.Linq.Enumerable.ThenBy%60%602%28System.Linq.IOrderedEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%29>|`Order By …, …`<br /><br /> (Aby uzyskać więcej informacji, zobacz [klauzula Order by](../../../language-reference/queries/order-by-clause.md).)|  
|<xref:System.Linq.Enumerable.ThenByDescending%60%602%28System.Linq.IOrderedEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%29>|`Order By …, … Descending`<br /><br /> (Aby uzyskać więcej informacji, zobacz [klauzula Order by](../../../language-reference/queries/order-by-clause.md).)|  
|<xref:System.Linq.Enumerable.Where%2A>|`Where`<br /><br /> (Aby uzyskać więcej informacji, zobacz [klauzula WHERE](../../../language-reference/queries/where-clause.md)).|  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Linq.Enumerable>
- <xref:System.Linq.Queryable>
- [Standardowe operatory zapytań — Omówienie (Visual Basic)](standard-query-operators-overview.md)
- [Klasyfikacja standardowych operatorów zapytań według sposobu wykonywania (Visual Basic)](classification-of-standard-query-operators-by-manner-of-execution.md)
