---
title: 'Instrukcje: Włączanie sprawdzania pisowni w kontrolce edycji tekstu'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- spellchecking [WPF]
- real-time spellchecking
- TextBox control [WPF], real-time spellchecking
- spelling checker [WPF]
- checking spelling [WPF]
ms.assetid: 6f953d2b-67e8-4012-84ce-53c0e958da47
ms.openlocfilehash: 7381bafc349506d89058581e9ed62a4348a72865
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/08/2019
ms.locfileid: "59076851"
---
# <a name="how-to-enable-spell-checking-in-a-text-editing-control"></a>Instrukcje: Włączanie sprawdzania pisowni w kontrolce edycji tekstu
Poniższy przykład pokazuje, jak włączyć w czasie rzeczywistym sprawdzanie pisowni w <xref:System.Windows.Controls.TextBox> przy użyciu <xref:System.Windows.Controls.SpellCheck.IsEnabled%2A> właściwość <xref:System.Windows.Controls.SpellCheck> klasy.  
  
## <a name="example"></a>Przykład  
 [!code-xaml[TextBoxMiscSnippets_snip#SpellCheckExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBoxMiscSnippets_snip/csharp/spellcheckexample.xaml#spellcheckexamplewholepage)]  
  
 [!code-csharp[TextBoxMiscSnippets_procedural_snip#SpellCheckCodeExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBoxMiscSnippets_procedural_snip/CSharp/SpellCheckExample.cs#spellcheckcodeexamplewholepage)]
 [!code-vb[TextBoxMiscSnippets_procedural_snip#SpellCheckCodeExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TextBoxMiscSnippets_procedural_snip/visualbasic/spellcheckexample.vb#spellcheckcodeexamplewholepage)]  
  
## <a name="see-also"></a>Zobacz także

- [Używanie sprawdzania pisowni z menu kontekstowym](how-to-use-spell-checking-with-a-context-menu.md)
- [TextBox — Przegląd](textbox-overview.md)
- [RichTextBox — Przegląd](richtextbox-overview.md)
