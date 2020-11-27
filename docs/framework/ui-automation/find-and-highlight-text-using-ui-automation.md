---
title: Znajdowanie i wyróżnianie tekstu przy użyciu automatyzacji interfejsu użytkownika
description: Znajdowanie i wyróżnianie tekstu przy użyciu automatyzacji interfejsu użytkownika. Przykład sekwencyjny wyszukuje i wyróżnia każde wystąpienie ciągu w zawartości kontrolki Text.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- text, highlighting
- finding text
- text, finding
- UI automation, highlighting text
- UI automation, finding text
- highlighting text
ms.assetid: b77693f5-87bb-4b29-a297-05ff882e2044
ms.openlocfilehash: 7ae933bdf12c81e48371fa89ba5fc5cf5dd4731e
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96276467"
---
# <a name="find-and-highlight-text-using-ui-automation"></a><span data-ttu-id="9d7a2-104">Znajdowanie i wyróżnianie tekstu przy użyciu automatyzacji interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="9d7a2-104">Find and Highlight Text Using UI Automation</span></span>

> [!NOTE]
> <span data-ttu-id="9d7a2-105">Ta dokumentacja jest przeznaczona dla .NET Framework deweloperów, którzy chcą korzystać z zarządzanych [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] klas zdefiniowanych w <xref:System.Windows.Automation> przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="9d7a2-105">This documentation is intended for .NET Framework developers who want to use the managed [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] classes defined in the <xref:System.Windows.Automation> namespace.</span></span> <span data-ttu-id="9d7a2-106">Aby uzyskać najnowsze informacje na temat [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] , zobacz [interfejs API usługi Windows Automation: Automatyzacja interfejsu użytkownika](/windows/win32/winauto/entry-uiauto-win32).</span><span class="sxs-lookup"><span data-stu-id="9d7a2-106">For the latest information about [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], see [Windows Automation API: UI Automation](/windows/win32/winauto/entry-uiauto-win32).</span></span>  
  
 <span data-ttu-id="9d7a2-107">W tym temacie pokazano, jak w sposób sekwencyjny wyszukiwać i wyróżniać każde wystąpienie ciągu w zawartości kontrolki tekstu przy użyciu [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] .</span><span class="sxs-lookup"><span data-stu-id="9d7a2-107">This topic demonstrates how to sequentially search for and highlight each occurrence of a string within the content of a text control using [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)].</span></span>  
  
## <a name="example"></a><span data-ttu-id="9d7a2-108">Przykład</span><span class="sxs-lookup"><span data-stu-id="9d7a2-108">Example</span></span>  

 <span data-ttu-id="9d7a2-109">Poniższy przykład pobiera <xref:System.Windows.Automation.TextPattern> obiekt z kontrolki tekstowej.</span><span class="sxs-lookup"><span data-stu-id="9d7a2-109">The following example obtains a <xref:System.Windows.Automation.TextPattern> object from a text control.</span></span> <span data-ttu-id="9d7a2-110"><xref:System.Windows.Automation.Text.TextPatternRange>Obiekt reprezentujący zawartość tekstową całego dokumentu jest następnie tworzony przy użyciu <xref:System.Windows.Automation.TextPattern.DocumentRange%2A> właściwości tego elementu <xref:System.Windows.Automation.TextPattern> .</span><span class="sxs-lookup"><span data-stu-id="9d7a2-110">A <xref:System.Windows.Automation.Text.TextPatternRange> object, representing the textual content of the entire document, is then created using the <xref:System.Windows.Automation.TextPattern.DocumentRange%2A> property of this <xref:System.Windows.Automation.TextPattern>.</span></span> <span data-ttu-id="9d7a2-111">Dwa dodatkowe <xref:System.Windows.Automation.Text.TextPatternRange> obiekty są następnie tworzone dla funkcji wyszukiwania sekwencyjnego i wyróżniania.</span><span class="sxs-lookup"><span data-stu-id="9d7a2-111">Two additional <xref:System.Windows.Automation.Text.TextPatternRange> objects are then created for the sequential search and highlight functionality.</span></span>  
  
[!code-csharp[FindText#StartApp](../../../samples/snippets/csharp/VS_Snippets_Wpf/FindText/CSharp/SearchWindow.cs#startapp)]
[!code-vb[FindText#StartApp](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FindText/VisualBasic/SearchWindow.vb#startapp)]  
[!code-csharp[FindText#FindTextProvider](../../../samples/snippets/csharp/VS_Snippets_Wpf/FindText/CSharp/SearchWindow.cs#findtextprovider)]
[!code-vb[FindText#FindTextProvider](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FindText/VisualBasic/SearchWindow.vb#findtextprovider)]  
[!code-csharp[FindText#SearchTarget](../../../samples/snippets/csharp/VS_Snippets_Wpf/FindText/CSharp/SearchWindow.cs#searchtarget)]
[!code-vb[FindText#SearchTarget](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FindText/VisualBasic/SearchWindow.vb#searchtarget)]  
  
## <a name="see-also"></a><span data-ttu-id="9d7a2-112">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="9d7a2-112">See also</span></span>

- [<span data-ttu-id="9d7a2-113">Znajdowanie i wyróżnianie tekstu przy użyciu automatyzacji interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="9d7a2-113">Find and Highlight Text Using UI Automation</span></span>](find-and-highlight-text-using-ui-automation.md)
