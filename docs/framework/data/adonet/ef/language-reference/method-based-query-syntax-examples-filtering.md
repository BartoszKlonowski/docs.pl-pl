---
title: Przykłady składni zapytania oparte na metodzie, filtrowanie
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: e40e314c-eb30-4f44-a054-41e511e35832
ms.openlocfilehash: 392181f201c7b18b1b38f62f5f35c5657cbbe601
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91191999"
---
# <a name="method-based-query-syntax-examples-filtering"></a>Przykłady składni zapytania oparte na metodzie, filtrowanie

W przykładach w tym temacie pokazano, jak za `Where` pomocą `Where…Contains` metod i zbadać [model sprzedaży AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) przy użyciu składni zapytania opartego na metodzie. Uwaga, gdzie...`Contains` nie można użyć jako części [skompilowanego zapytania](compiled-queries-linq-to-entities.md).  
  
 Model sprzedaży AdventureWorks używany w tych przykładach jest tworzony na podstawie tabel Contact, Address, Product, SalesOrderHeader i SalesOrderDetail w przykładowej bazie danych AdventureWorks.  
  
 Przykłady w tym temacie wykorzystują następujące `using` / `Imports` instrukcje:  
  
 [!code-csharp[DP L2E Examples#ImportsUsing](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#importsusing)]
 [!code-vb[DP L2E Examples#ImportsUsing](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#importsusing)]  
  
## <a name="where"></a>Lokalizacja  
  
### <a name="example"></a>Przykład  

 Poniższy przykład zwraca wszystkie zamówienia online.  
  
 [!code-csharp[DP L2E Examples#Where1_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#where1_mq)]
 [!code-vb[DP L2E Examples#Where1_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#where1_mq)]  
  
### <a name="example"></a>Przykład  

 Poniższy przykład zwraca zamówienia, w których ilość zamówienia jest większa niż 2 i mniejsza niż 6.  
  
 [!code-csharp[DP L2E Examples#Where2_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#where2_mq)]
 [!code-vb[DP L2E Examples#Where2_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#where2_mq)]  
  
### <a name="example"></a>Przykład  

 Poniższy przykład zwraca wszystkie kolorowe produkty.  
  
 [!code-csharp[DP L2E Examples#Where3_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#where3_mq)]
 [!code-vb[DP L2E Examples#Where3_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#where3_mq)]  
  
### <a name="example"></a>Przykład  

 W poniższym przykładzie użyto `Where` metody, aby znaleźć zamówienia, które zostały wprowadzone po 1 grudnia 2003, a następnie użyć `order.SalesOrderDetail` właściwości nawigacji, aby uzyskać szczegółowe informacje dotyczące poszczególnych zamówień.  
  
 [!code-csharp[DP L2E Examples#WhereNavProperty_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#wherenavproperty_mq)]
 [!code-vb[DP L2E Examples#WhereNavProperty_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#wherenavproperty_mq)]  
  
## <a name="wherecontains"></a>Gdzie... Wyświetlana  
  
### <a name="example"></a>Przykład  

 Poniższy przykład używa tablicy jako części `Where…Contains` klauzuli, aby znaleźć wszystkie produkty, które są `ProductModelID` zgodne z wartością w tablicy.  
  
 [!code-csharp[DP L2E ArraysAndListsInQueries#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e arraysandlistsinqueries/cs/program.cs#3)]
 [!code-vb[DP L2E ArraysAndListsInQueries#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e arraysandlistsinqueries/vb/module1.vb#3)]  
  
> [!NOTE]
> Jako część predykatu w `Where…Contains` klauzuli, można użyć <xref:System.Array> , a <xref:System.Collections.Generic.List%601> lub kolekcji dowolnego typu, który implementuje <xref:System.Collections.Generic.IEnumerable%601> interfejs. Można również zadeklarować i zainicjować kolekcję w ramach zapytania LINQ to Entities. Aby uzyskać więcej informacji, zobacz następny przykład.  
  
### <a name="example"></a>Przykład  

 Poniższy przykład deklaruje i inicjuje tablice w `Where…Contains` klauzuli, aby znaleźć wszystkie produkty, które mają `ProductModelID` lub `Size` , które pasują do wartości w tablicach.  
  
 [!code-csharp[DP L2E ArraysAndListsInQueries#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e arraysandlistsinqueries/cs/program.cs#4)]
 [!code-vb[DP L2E ArraysAndListsInQueries#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e arraysandlistsinqueries/vb/module1.vb#4)]  
  
## <a name="see-also"></a>Zobacz też

- [Zapytania w składniku LINQ to Entities](queries-in-linq-to-entities.md)
