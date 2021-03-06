---
title: Konwertowanie typu na ogólny interfejs IEnumerable
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 64774fb5-7447-4296-ad3b-8a94346f99a1
ms.openlocfilehash: c2d34ae708f79d9f920679b3714a100fe8943c38
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91164418"
---
# <a name="convert-a-type-to-a-generic-ienumerable"></a>Konwertowanie typu na ogólny interfejs IEnumerable

Użyj, <xref:System.Linq.Enumerable.AsEnumerable%2A> Aby zwrócić argument, który jest typem ogólnym `IEnumerable` .  
  
## <a name="example"></a>Przykład  

 W tym przykładzie [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] (przy użyciu domyślnego generycznego `Query` ) próba konwersji zapytania na SQL i wykonania go na serwerze. Natomiast `where` klauzula odwołuje się do zdefiniowanej przez użytkownika metody po stronie klienta ( `isValidProduct` ), której nie można przekonwertować na SQL.  
  
 Rozwiązaniem jest określenie, że implementacja ogólna po stronie klienta <xref:System.Collections.Generic.IEnumerable%601> `where` zastąpi ogólny <xref:System.Linq.IQueryable%601> . W tym celu należy wycofać <xref:System.Linq.Enumerable.AsEnumerable%2A> operatora.  
  
 [!code-csharp[DLinqQueryExamples#46](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#46)]
 [!code-vb[DLinqQueryExamples#46](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#46)]  
  
## <a name="see-also"></a>Zobacz też

- [Przykłady zapytań](query-examples.md)
