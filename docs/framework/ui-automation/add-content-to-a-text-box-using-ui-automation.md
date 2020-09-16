---
title: Dodawanie zawartości do pola tekstowego przy użyciu automatyzacji interfejsu użytkownika
description: Zapoznaj się z przykładem, jak dodać zawartość do jednowierszowego pola tekstowego przy użyciu automatyzacji interfejsu użytkownika firmy Microsoft w ramach platformy .NET.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- adding content to text boxes
- text boxes, adding content
- UI Automation, adding content to text boxes
ms.assetid: 8bdd1a73-1ecb-4a05-a891-a7827ebb767f
ms.openlocfilehash: 5e7ab77f1dcc2198e69255013eeb30cc703a235f
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90543137"
---
# <a name="add-content-to-a-text-box-using-ui-automation"></a>Dodawanie zawartości do pola tekstowego przy użyciu automatyzacji interfejsu użytkownika
> [!NOTE]
> Ta dokumentacja jest przeznaczona dla .NET Framework deweloperów, którzy chcą korzystać z zarządzanych [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] klas zdefiniowanych w <xref:System.Windows.Automation> przestrzeni nazw. Aby uzyskać najnowsze informacje na temat [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] , zobacz [interfejs API usługi Windows Automation: Automatyzacja interfejsu użytkownika](/windows/win32/winauto/entry-uiauto-win32).  
  
 Ten temat zawiera przykładowy kod, który demonstruje sposób użycia [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] do wstawiania tekstu w jednowierszowym polu tekstowym. Podano alternatywną metodę dla formantów tekstu wielowierszowego i sformatowanego, gdzie [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] nie ma zastosowania. W celu porównania przykład ilustruje sposób użycia metod Win32 do osiągnięcia tych samych wyników.  
  
## <a name="example"></a>Przykład  
 Poniższy przykład przechodzi przez sekwencję formantów tekstowych w aplikacji docelowej. Każda kontrolka tekstowa jest testowana, aby sprawdzić, czy <xref:System.Windows.Automation.ValuePattern> obiekt można uzyskać z niego przy użyciu <xref:System.Windows.Automation.AutomationElement.TryGetCurrentPattern%2A> metody. Jeśli kontrolka tekstu obsługuje <xref:System.Windows.Automation.ValuePattern> , metoda służy <xref:System.Windows.Automation.ValuePattern.SetValue%2A> do wstawiania ciągu zdefiniowanego przez użytkownika do kontrolki tekstowej. W przeciwnym razie <xref:System.Windows.Forms.SendKeys.SendWait%2A?displayProperty=nameWithType> Metoda jest używana.  
  
 [!code-csharp[InsertText#InsertText](../../../samples/snippets/csharp/VS_Snippets_Wpf/InsertText/CSharp/Window1.xaml.cs#inserttext)]
 [!code-vb[InsertText#InsertText](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/InsertText/VisualBasic/Window1.xaml.vb#inserttext)]  
  
## <a name="see-also"></a>Zobacz także

- [Przykład wstawiania TextPattern tekstu](/previous-versions/dotnet/netframework-3.5/ms771478(v=vs.90))
