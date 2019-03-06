---
title: 'Instrukcje: Obsługa zdarzenia ScrollChanged'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ScrollViewer control [WPF], raising ScrollChanged events
- ScrollChanged events [WPF]
ms.assetid: 42c695d8-ee28-49d4-80fd-fc71e9be7f29
ms.openlocfilehash: 34a3c97453df334e8c12da1a31cfb029294da687
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/05/2019
ms.locfileid: "57352529"
---
# <a name="how-to-handle-the-scrollchanged-event"></a>Instrukcje: Obsługa zdarzenia ScrollChanged
## <a name="example"></a>Przykład  
 W tym przykładzie pokazano, jak obsługiwać <xref:System.Windows.Controls.ScrollViewer.ScrollChanged> zdarzenia <xref:System.Windows.Controls.ScrollViewer>.  
  
 A <xref:System.Windows.Documents.FlowDocument> element z <xref:System.Windows.Documents.Paragraph> części jest zdefiniowany w [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]. Gdy <xref:System.Windows.Controls.ScrollViewer.ScrollChanged> zdarzenie występuje z powodu interakcji z użytkownikiem, program obsługi jest wywoływany i tekst jest zapisany do <xref:System.Windows.Controls.TextBlock> wskazująca, że wystąpiło zdarzenie.  
  
 [!code-xaml[scrollchangedeventargsLayout#1](~/samples/snippets/csharp/VS_Snippets_Wpf/scrollchangedeventargsLayout/CSharp/Window1.xaml#1)]  
[!code-xaml[scrollchangedeventargsLayout#2](~/samples/snippets/csharp/VS_Snippets_Wpf/scrollchangedeventargsLayout/CSharp/Window1.xaml#2)]  
  
 [!code-csharp[scrollchangedeventargsLayout#3](~/samples/snippets/csharp/VS_Snippets_Wpf/scrollchangedeventargsLayout/CSharp/Window1.xaml.cs#3)]
 [!code-vb[scrollchangedeventargsLayout#3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/scrollchangedeventargsLayout/VisualBasic/Window1.xaml.vb#3)]  
  
## <a name="see-also"></a>Zobacz także
- <xref:System.Windows.Controls.ScrollViewer>
- <xref:System.Windows.Controls.ScrollViewer.ScrollChanged>
- <xref:System.Windows.Controls.ScrollChangedEventHandler>
- <xref:System.Windows.Controls.ScrollChangedEventArgs>
