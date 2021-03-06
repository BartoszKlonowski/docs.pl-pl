---
title: Zwracanie lub pomijanie elementów w sekwencji
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 81a31acd-e0f1-4bca-9a12-fa1ad5752374
ms.openlocfilehash: 1a36d3c8457374183148599bf8160d14847cbf3e
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91200423"
---
# <a name="return-or-skip-elements-in-a-sequence"></a>Zwracanie lub pomijanie elementów w sekwencji

Użyj <xref:System.Linq.Queryable.Take%2A> operatora, aby zwrócić daną liczbę elementów w sekwencji, a następnie pominąć resztę.  
  
 Użyj <xref:System.Linq.Queryable.Skip%2A> operatora, aby pominąć daną liczbę elementów w sekwencji, a następnie zwrócić resztę.  
  
> [!NOTE]
> <xref:System.Linq.Enumerable.Take%2A> i <xref:System.Linq.Enumerable.Skip%2A> mają pewne ograniczenia, gdy są używane w zapytaniach do SQL Server 2000. Aby uzyskać więcej informacji, zobacz wpis "Pomiń i przejmowanie wyjątków w SQL Server 2000" w [temacie Rozwiązywanie problemów](troubleshooting.md).  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] tłumaczy przy <xref:System.Linq.Queryable.Skip%2A> użyciu podzapytania z `NOT EXISTS` klauzulą SQL. To tłumaczenie ma następujące ograniczenia:  
  
- Argument musi być zestawem. Zestawy wielozbiorowe nie są obsługiwane, nawet jeśli są uporządkowane.  
  
- Wygenerowane zapytanie może być znacznie bardziej złożone niż zapytanie wygenerowane dla zapytania bazowego, na którym <xref:System.Linq.Queryable.Skip%2A> jest stosowane. Taka złożoność może spowodować spadek wydajności lub nawet przekroczenie limitu czasu.  
  
## <a name="example"></a>Przykład  

 Poniższy przykład używa `Take` do wybierania pierwszych pięciu `Employees` zatrudnianych. Należy pamiętać, że kolekcja jest najpierw sortowana według `HireDate` .  
  
 [!code-csharp[DLinqQueryExamples#16](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#16)]
 [!code-vb[DLinqQueryExamples#16](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#16)]  
  
## <a name="example"></a>Przykład  

 Poniższy przykład używa <xref:System.Linq.Queryable.Skip%2A> do zaznaczania wszystkiego z wyjątkiem 10 `Products` .  
  
 [!code-csharp[DLinqQueryExamples#17](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#17)]
 [!code-vb[DLinqQueryExamples#17](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#17)]  
  
## <a name="example"></a>Przykład  

 Poniższy przykład łączy <xref:System.Linq.Queryable.Skip%2A> metody i, <xref:System.Linq.Queryable.Take%2A> Aby pominąć pierwsze 50 rekordów, a następnie zwrócić następny 10.  
  
 [!code-csharp[DLinqQueryExamples#18](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#18)]
 [!code-vb[DLinqQueryExamples#18](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#18)]  
  
 <xref:System.Linq.Queryable.Take%2A><xref:System.Linq.Queryable.Skip%2A>operacje i są dobrze zdefiniowane tylko względem uporządkowanych zestawów. Semantyka nieuporządkowanych zestawów lub zestawów wielozbiorówowych jest niezdefiniowana.  
  
 Ze względu na ograniczenia związane z kolejnością w programie SQL, program [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] próbuje przenieść argument <xref:System.Linq.Queryable.Take%2A> operatora or <xref:System.Linq.Queryable.Skip%2A> do wyniku operatora.  
  
> [!NOTE]
> Tłumaczenie jest różne dla SQL Server 2000 i SQL Server 2005. Jeśli planujesz używać <xref:System.Linq.Queryable.Skip%2A> zapytania o dowolnej złożoności, użyj SQL Server 2005.  
  
 Rozważ następujące [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] zapytanie dla SQL Server 2000:  
  
 [!code-csharp[DLinqQueryExamples#19](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#19)]
 [!code-vb[DLinqQueryExamples#19](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#19)]  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] przenosi porządkowanie do końca kodu SQL w następujący sposób:  
  
```sql
SELECT TOP 1 [t0].[CustomerID], [t0].[CompanyName],  
FROM [Customers] AS [t0]  
WHERE (NOT (EXISTS(  
    SELECT NULL AS [EMPTY]  
    FROM (  
        SELECT TOP 1 [t1].[CustomerID]  
        FROM [Customers] AS [t1]  
        WHERE [t1].[City] = @p0  
        ORDER BY [t1].[CustomerID]  
        ) AS [t2]  
    WHERE [t0].[CustomerID] = [t2].[CustomerID]  
    ))) AND ([t0].[City] = @p1)  
ORDER BY [t0].[CustomerID]  
```  
  
 Gdy <xref:System.Linq.Queryable.Take%2A> i <xref:System.Linq.Queryable.Skip%2A> są połączone łańcuchowo, cała określona kolejność musi być spójna. W przeciwnym razie wyniki są niezdefiniowane.  
  
 W przypadku nieujemnych, stałych argumentów całkowitych opartych na specyfikacji SQL, obie <xref:System.Linq.Queryable.Take%2A> i <xref:System.Linq.Queryable.Skip%2A> są dobrze zdefiniowane.  
  
## <a name="see-also"></a>Zobacz też

- [Przykłady zapytań](query-examples.md)
- [Translacja standardowego operatora zapytania](standard-query-operator-translation.md)
