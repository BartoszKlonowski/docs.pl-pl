---
title: Używanie buforowania w automatyzacji interfejsu użytkownika
description: Zobacz jak używać buforowania w automatyzacji interfejsu użytkownika. Zapoznaj się z instrukcjami dotyczącymi aktywacji żądania pamięci podręcznej, buforowania właściwości AutomationElement i uzyskiwania buforowanych wzorców.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- caching, UI Automation
- UI Automation, caching
ms.assetid: ec722dff-6009-4279-b86a-e18d3fa94ebf
ms.openlocfilehash: f99fb724130c359a77c72db66dd9f837ef1a2219
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96258611"
---
# <a name="use-caching-in-ui-automation"></a>Używanie buforowania w automatyzacji interfejsu użytkownika

> [!NOTE]
> Ta dokumentacja jest przeznaczona dla .NET Framework deweloperów, którzy chcą korzystać z zarządzanych [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] klas zdefiniowanych w <xref:System.Windows.Automation> przestrzeni nazw. Aby uzyskać najnowsze informacje na temat [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] , zobacz [interfejs API usługi Windows Automation: Automatyzacja interfejsu użytkownika](/windows/win32/winauto/entry-uiauto-win32).  
  
 W tej sekcji pokazano, jak zaimplementować buforowanie <xref:System.Windows.Automation.AutomationElement> właściwości i wzorców kontrolek.  
  
### <a name="activate-a-cache-request"></a>Aktywuj żądanie pamięci podręcznej  
  
1. Utwórz <xref:System.Windows.Automation.CacheRequest> .  
  
2. Określ właściwości i wzorce do buforowania przy użyciu programu <xref:System.Windows.Automation.CacheRequest.Add%2A> .  
  
3. Określ zakres buforowania przez ustawienie <xref:System.Windows.Automation.CacheRequest.TreeScope%2A> właściwości.  
  
4. Określ widok poddrzewa przez ustawienie <xref:System.Windows.Automation.CacheRequest.TreeFilter%2A> właściwości.  
  
5. Ustaw <xref:System.Windows.Automation.CacheRequest.AutomationElementMode%2A> Właściwość na, <xref:System.Windows.Automation.AutomationElementMode.None> Jeśli chcesz zwiększyć wydajność, nie pobierając pełnych odwołań do obiektów. (Spowoduje to niemożliwe pobranie bieżących wartości z tych obiektów).  
  
6. Aktywuj żądanie przy użyciu <xref:System.Windows.Automation.CacheRequest.Activate%2A> `using` bloku ( `Using` w programie Microsoft Visual Basic .NET).  
  
 Po uzyskaniu <xref:System.Windows.Automation.AutomationElement> obiektów lub zasubskrybowaniu zdarzeń, Dezaktywuj żądanie przy użyciu <xref:System.Windows.Automation.CacheRequest.Pop%2A> (Jeśli <xref:System.Windows.Automation.CacheRequest.Push%2A> zostało użyte) lub przez odtworzenie obiektu utworzonego przez <xref:System.Windows.Automation.CacheRequest.Activate%2A> . (Użyj <xref:System.Windows.Automation.CacheRequest.Activate%2A> w `using` bloku ( `Using` w programie Microsoft Visual Basic .NET).  
  
### <a name="cache-automationelement-properties"></a>Właściwości automatyzacji  
  
1. Gdy <xref:System.Windows.Automation.CacheRequest> jest aktywny, należy uzyskać <xref:System.Windows.Automation.AutomationElement> obiekty za pomocą <xref:System.Windows.Automation.AutomationElement.FindFirst%2A> lub <xref:System.Windows.Automation.AutomationElement.FindAll%2A> ; albo uzyskać <xref:System.Windows.Automation.AutomationElement> jako źródło zdarzenia, które zostało zarejestrowane, gdy <xref:System.Windows.Automation.CacheRequest> był aktywny. (Możesz również utworzyć pamięć podręczną, przechodząc <xref:System.Windows.Automation.CacheRequest> do GetUpdatedCache lub jednej z <xref:System.Windows.Automation.TreeWalker> metod).  
  
2. Użyj <xref:System.Windows.Automation.AutomationElement.GetCachedPropertyValue%2A> lub Pobierz właściwość z <xref:System.Windows.Automation.AutomationElement.Cached%2A> właściwości <xref:System.Windows.Automation.AutomationElement> .  
  
### <a name="obtain-cached-patterns-and-their-properties"></a>Uzyskiwanie buforowanych wzorców i ich właściwości  
  
1. Gdy <xref:System.Windows.Automation.CacheRequest> jest aktywny, należy uzyskać <xref:System.Windows.Automation.AutomationElement> obiekty za pomocą <xref:System.Windows.Automation.AutomationElement.FindFirst%2A> lub <xref:System.Windows.Automation.AutomationElement.FindAll%2A> ; albo uzyskać <xref:System.Windows.Automation.AutomationElement> jako źródło zdarzenia, które zostało zarejestrowane, gdy <xref:System.Windows.Automation.CacheRequest> był aktywny. (Możesz również utworzyć pamięć podręczną, przechodząc <xref:System.Windows.Automation.CacheRequest> do GetUpdatedCache lub jednej z <xref:System.Windows.Automation.TreeWalker> metod).  
  
2. Użyj <xref:System.Windows.Automation.AutomationElement.GetCachedPattern%2A> lub, <xref:System.Windows.Automation.AutomationElement.TryGetCachedPattern%2A> Aby pobrać buforowany wzorzec.  
  
3. Pobiera wartości właściwości z `Cached` właściwości wzorca kontrolki.  
  
## <a name="example"></a>Przykład  

 Poniższy przykład kodu przedstawia różne aspekty buforowania przy użyciu narzędzia <xref:System.Windows.Automation.CacheRequest.Activate%2A> do aktywacji <xref:System.Windows.Automation.CacheRequest> .  
  
 [!code-csharp[UIAClient_snip#107](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAClient_snip/CSharp/ClientForm.cs#107)]
 [!code-vb[UIAClient_snip#107](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAClient_snip/VisualBasic/ClientForm.vb#107)]  
  
## <a name="example"></a>Przykład  

 Poniższy przykład kodu przedstawia różne aspekty buforowania przy użyciu narzędzia <xref:System.Windows.Automation.CacheRequest.Push%2A> do aktywacji <xref:System.Windows.Automation.CacheRequest> . W przypadku zamiaru zagnieżdżenia żądań pamięci podręcznej najlepiej jest używać <xref:System.Windows.Automation.CacheRequest.Activate%2A> .  
  
 [!code-csharp[UIAClient_snip#108](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAClient_snip/CSharp/ClientForm.cs#108)]
 [!code-vb[UIAClient_snip#108](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAClient_snip/VisualBasic/ClientForm.vb#108)]  
  
## <a name="see-also"></a>Zobacz też

- [Buforowanie w klientach automatyzacji interfejsu użytkownika](caching-in-ui-automation-clients.md)
