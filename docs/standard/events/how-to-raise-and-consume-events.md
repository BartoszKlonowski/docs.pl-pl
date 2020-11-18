---
title: 'Porady: wywoływanie zdarzeń i korzystanie z nich'
description: Zgłoś & zużywać zdarzenia w programie .NET. Zobacz przykłady, które używają delegata EventHandler, <TEventArgs> delegata EventHandler, & delegata niestandardowego.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- events [.NET], raising
- raising events
- events [.NET], samples
ms.assetid: 42afade7-3a02-4f2e-868b-95845f302f8f
ms.openlocfilehash: 9d068981694c212c5cb29a67ccd2fcb19dcc907b
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "94828299"
---
# <a name="how-to-raise-and-consume-events"></a>Porady: wywoływanie zdarzeń i korzystanie z nich
Przykłady w tym temacie przedstawiają sposób pracy ze zdarzeniami. Obejmują one przykłady <xref:System.EventHandler> delegata, <xref:System.EventHandler%601> delegata i delegata niestandardowego, które ilustrują zdarzenia z i bez danych.  
  
 Przykłady wykorzystują Koncepcje opisane w artykule [zdarzenia](index.md) .  
  
## <a name="example"></a>Przykład  
 Pierwszy przykład pokazuje, jak podnieść i zużyć zdarzenie, które nie ma danych. Zawiera klasę o nazwie `Counter` , która ma zdarzenie o nazwie `ThresholdReached` . To zdarzenie jest zgłaszane, gdy wartość licznika jest równa lub przekracza wartość progową. <xref:System.EventHandler>Delegat jest skojarzony ze zdarzeniem, ponieważ nie podano danych zdarzenia.  
  
 [!code-csharp[EventsOverview#5](../../../samples/snippets/csharp/VS_Snippets_CLR/eventsoverview/cs/programnodata.cs#5)]
 [!code-vb[EventsOverview#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/eventsoverview/vb/module1nodata.vb#5)]  
  
## <a name="example"></a>Przykład  
 W następnym przykładzie pokazano, jak podnieść i zużyć zdarzenie, które dostarcza dane. <xref:System.EventHandler%601>Delegat jest skojarzony ze zdarzeniem, a wystąpienie obiektu danych zdarzenia niestandardowego jest dostarczone.  
  
 [!code-cpp[EventsOverview#6](../../../samples/snippets/cpp/VS_Snippets_CLR/eventsoverview/cpp/programwithdata.cpp#6)]
 [!code-csharp[EventsOverview#6](../../../samples/snippets/csharp/VS_Snippets_CLR/eventsoverview/cs/programwithdata.cs#6)]
 [!code-vb[EventsOverview#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/eventsoverview/vb/module1withdata.vb#6)]  
  
## <a name="example"></a>Przykład  
 W następnym przykładzie pokazano, jak zadeklarować delegata dla zdarzenia. Delegat ma nazwę `ThresholdReachedEventHandler` . Jest to tylko ilustracja. Zazwyczaj nie trzeba deklarować delegatów dla zdarzenia, ponieważ można użyć albo <xref:System.EventHandler> <xref:System.EventHandler%601> delegata. Delegata należy zadeklarować tylko w rzadkich scenariuszach, takich jak udostępnienie klasy dla starszego kodu, który nie może używać typów ogólnych.  
  
 [!code-csharp[EventsOverview#7](../../../samples/snippets/csharp/VS_Snippets_CLR/eventsoverview/cs/programwithdelegate.cs#7)]
 [!code-vb[EventsOverview#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/eventsoverview/vb/module1withdelegate.vb#7)]  
  
## <a name="see-also"></a>Zobacz także

- [Zdarzenia](index.md)
