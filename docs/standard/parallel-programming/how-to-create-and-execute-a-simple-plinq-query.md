---
title: 'Instrukcje: Tworzenie i wykonywanie prostego zapytania PLINQ'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- PLINQ queries, how to create
ms.assetid: 983b4213-bddd-4a44-9262-cbe59186df4c
ms.openlocfilehash: 228a94323c42d7c7a5ecbd295a0db5d73f4f1f49
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95703697"
---
# <a name="how-to-create-and-execute-a-simple-plinq-query"></a>Instrukcje: Tworzenie i wykonywanie prostego zapytania PLINQ

W przykładzie w tym artykule przedstawiono sposób tworzenia prostego zapytania programu Parallel Language Integrated Query (LINQ) przy użyciu <xref:System.Linq.ParallelEnumerable.AsParallel%2A?displayProperty=nameWithType> metody rozszerzenia w sekwencji źródłowej i wykonywania zapytania przy użyciu <xref:System.Linq.ParallelEnumerable.ForAll%2A?displayProperty=nameWithType> metody.  
  
> [!NOTE]
> Ta dokumentacja używa wyrażeń lambda do definiowania delegatów w PLINQ. Jeśli nie znasz wyrażeń lambda w języku C# lub Visual Basic, zobacz [lambda Expressions in PLINQ and TPL](lambda-expressions-in-plinq-and-tpl.md).  
  
## <a name="example"></a>Przykład  

 [!code-csharp[PLINQ#11](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/create1.cs#11)]
 [!code-vb[PLINQ#11](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/create1.vb#11)]  
  
 W tym przykładzie przedstawiono podstawowy wzorzec tworzenia i wykonywania wszelkich równoległych zapytań LINQ, gdy kolejność sekwencji wyników nie jest ważna. Zapytania nieuporządkowane są zwykle szybsze niż uporządkowane zapytania. Zapytanie dzieli źródło na zadania, które są wykonywane asynchronicznie na wielu wątkach. Kolejność, w której każde zadanie jest wykonywane, zależy nie tylko od ilości pracy związanej z przetwarzaniem elementów w partycji, ale również na zewnętrznych czynnikach, takich jak system operacyjny planuje każdy wątek. Ten przykład jest przeznaczony do zademonstrowania użycia i może nie działać szybciej niż równoważne LINQ to Objects sekwencyjne zapytanie. Aby uzyskać więcej informacji na temat przyspieszenie, zobacz [Opis przyspieszenie w PLINQ](understanding-speedup-in-plinq.md). Aby uzyskać więcej informacji na temat zachowania kolejności elementów w zapytaniu, zobacz [How to: Control Order in a PLINQ Query](how-to-control-ordering-in-a-plinq-query.md).  
  
## <a name="see-also"></a>Zobacz także

- [Równoległe LINQ (PLINQ)](introduction-to-plinq.md)
