---
title: Zwracanie właściwości od dostawcy automatyzacji interfejsu użytkownika
description: Zobacz, w jaki sposób dostawca automatyzacji interfejsu użytkownika może zwracać właściwości elementu do aplikacji klienckich w programie .NET.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- providers, UI Automation, returning properties
- properties, returned by UI Automation providers
- UI Automation, providers returning properties
ms.assetid: 5eba950e-b9e1-48eb-ab8e-b69db76bf589
ms.openlocfilehash: 8269d7d04a67c2a89a28160c0a8bc82bd627749f
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96250479"
---
# <a name="return-properties-from-a-ui-automation-provider"></a>Zwracanie właściwości od dostawcy automatyzacji interfejsu użytkownika

> [!NOTE]
> Ta dokumentacja jest przeznaczona dla .NET Framework deweloperów, którzy chcą korzystać z zarządzanych [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] klas zdefiniowanych w <xref:System.Windows.Automation> przestrzeni nazw. Aby uzyskać najnowsze informacje na temat [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] , zobacz [interfejs API usługi Windows Automation: Automatyzacja interfejsu użytkownika](/windows/win32/winauto/entry-uiauto-win32).  
  
 Ten temat zawiera przykładowy kod, który pokazuje, w jaki sposób dostawca automatyzacji interfejsu użytkownika może zwracać właściwości elementu do aplikacji klienckich.  
  
 Dla każdej właściwości, która nie jest jawnie obsługiwana, dostawca musi zwrócić `null` ( `Nothing` w Visual Basic). Zapewnia to, że program [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] próbuje uzyskać właściwość z innego źródła, takiego jak dostawca okna hosta.  
  
## <a name="example"></a>Przykład  

 [!code-csharp[UIAFragmentProvider_snip#117](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAFragmentProvider_snip/CSharp/ListFragment.cs#117)]
 [!code-vb[UIAFragmentProvider_snip#117](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAFragmentProvider_snip/VisualBasic/ListFragment.vb#117)]  
  
## <a name="see-also"></a>Zobacz także

- [Przegląd dostawców automatyzacji interfejsu użytkownika](ui-automation-providers-overview.md)
- [Implementacja dostawcy automatyzacji interfejsu użytkownika po stronie serwera](server-side-ui-automation-provider-implementation.md)
