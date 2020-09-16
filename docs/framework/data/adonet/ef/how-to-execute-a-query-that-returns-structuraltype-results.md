---
title: 'Instrukcje: Wykonywanie zapytania, które zwraca wyniki StructuralType'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 2314f2a2-b1c3-40c4-95bb-cdf9b21a7b53
ms.openlocfilehash: e9b9c806dd77ea90399aaefdaa751cbd0ab938e9
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90546747"
---
# <a name="how-to-execute-a-query-that-returns-structuraltype-results"></a>Instrukcje: Wykonywanie zapytania, które zwraca wyniki StructuralType
W tym temacie pokazano, jak wykonać polecenie względem modelu koncepcyjnego za pomocą <xref:System.Data.EntityClient.EntityCommand> obiektu i jak pobrać <xref:System.Data.Metadata.Edm.StructuralType> wyniki przy użyciu <xref:System.Data.EntityClient.EntityDataReader> . <xref:System.Data.Metadata.Edm.EntityType> <xref:System.Data.Metadata.Edm.RowType> Klasy i są <xref:System.Data.Metadata.Edm.ComplexType> pochodne od <xref:System.Data.Metadata.Edm.StructuralType> klasy.  
  
### <a name="to-run-the-code-in-this-example"></a>Aby uruchomić kod w tym przykładzie  
  
1. Dodaj [model sprzedaży AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) do projektu i skonfiguruj projekt tak, aby korzystał z Entity Framework. Aby uzyskać więcej informacji, zobacz [How to: Use the Entity Data Model Wizard](/previous-versions/dotnet/netframework-4.0/bb738677(v=vs.100)).  
  
2. Na stronie kodowej aplikacji Dodaj następujące `using` instrukcje ( `Imports` w Visual Basic):  
  
     [!code-csharp[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#namespaces)]
     [!code-vb[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#namespaces)]  
  
## <a name="example"></a>Przykład  
 Ten przykład wykonuje zapytanie zwracające <xref:System.Data.Metadata.Edm.EntityType> wyniki. W przypadku przekazania następującego zapytania jako argumentu do `ExecuteStructuralTypeQuery` funkcji, funkcja wyświetla szczegółowe informacje o `Products` :  
  
 [!code-csharp[DP EntityServices Concepts 2#SelectProduct](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#selectproduct)]  
  
 W przypadku przekazania sparametryzowanych zapytań, takich jak następujące, Dodaj <xref:System.Data.EntityClient.EntityParameter> obiekty do <xref:System.Data.EntityClient.EntityCommand.Parameters%2A> właściwości <xref:System.Data.EntityClient.EntityCommand> obiektu.  
  
 [!code-csharp[DP EntityServices Concepts 2#GREATER_OR_EQUALS](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#greater_or_equals)]  
  
 [!code-csharp[DP EntityServices Concepts#eSQLStructuralTypes](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#esqlstructuraltypes)]
 [!code-vb[DP EntityServices Concepts#eSQLStructuralTypes](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#esqlstructuraltypes)]  
  
## <a name="see-also"></a>Zobacz także

- [Odwołanie do jednostki SQL](./language-reference/entity-sql-reference.md)
- [Dostawca EntityClient dla programu Entity Framework](entityclient-provider-for-the-entity-framework.md)
