---
title: Obsługa automatyzacji interfejsu użytkownika dla typu formantu ToolTip
description: Uzyskaj informacje na temat obsługi automatyzacji interfejsu użytkownika dla kontrolek typu etykietka narzędzia. Poznaj wymaganą strukturę drzewa, właściwości, wzorce formantów i zdarzenia.
ms.date: 03/30/2017
helpviewer_keywords:
- UI Automation, ToolTip control type
- ToolTip control type
- control types, ToolTip
ms.assetid: c3779d78-3164-43ae-8dae-bfaeafffdd65
ms.openlocfilehash: 8c4f66de95acd3f18148887b4eb18713cb30fa87
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96240189"
---
# <a name="ui-automation-support-for-the-tooltip-control-type"></a>Obsługa automatyzacji interfejsu użytkownika dla typu formantu ToolTip

> [!NOTE]
> Ta dokumentacja jest przeznaczona dla .NET Framework deweloperów, którzy chcą korzystać z zarządzanych [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] klas zdefiniowanych w <xref:System.Windows.Automation> przestrzeni nazw. Aby uzyskać najnowsze informacje na temat [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] , zobacz [interfejs API usługi Windows Automation: Automatyzacja interfejsu użytkownika](/windows/win32/winauto/entry-uiauto-win32).  
  
 Ten temat zawiera informacje [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] na temat obsługi typu formantu tooltip. W programie [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] Typ kontrolki jest zestawem warunków, które formant musi spełniać, aby można było użyć <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty> właściwości. Warunki obejmują określone wytyczne dotyczące [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] struktury drzewa, [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] wartości właściwości i wzorców formantów.  
  
 Kontrolki etykietki narzędzi to okna podręczne, które zawierają tekst.  
  
 W poniższych sekcjach opisano wymaganą [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] strukturę drzewa, właściwości, wzorce formantów i zdarzenia dla typu formantu tooltip. [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]Wymagania stosują się do wszystkich kontrolek etykietki narzędzi, zarówno [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)] systemu Win32, jak i Windows Forms.  
  
<a name="Required_UI_Automation_Tree_Structure"></a>

## <a name="required-ui-automation-tree-structure"></a>Wymagana struktura drzewa automatyzacji interfejsu użytkownika  

 W poniższej tabeli przedstawiono widok kontrolki i widok zawartości [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] drzewa, które odnoszą się do kontrolek etykietek narzędzi i opisano, co może być zawarte w poszczególnych widokach. Aby uzyskać więcej informacji na temat [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] drzewa, zobacz [drzewo automatyzacji interfejsu użytkownika — omówienie](ui-automation-tree-overview.md).  
  
|Widok kontrolki|Widok zawartości|  
|------------------|------------------|  
|ToolTip<br /><br /> -Tekst (0 lub więcej)<br />-Image (0 lub więcej)|ToolTip|  
  
 Kontrolki etykietki narzędzi są wyświetlane tylko w widoku zawartości [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] drzewa, jeśli mogą odbierać fokus klawiatury. W przeciwnym razie wszystkie informacje etykietki narzędzi są dostępne z poziomu `HelpTextProperty` [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] elementu, do którego odwołuje się etykietka narzędzia.  
  
 Etykietki narzędzi powinny znajdować się poniżej kontrolki, do której odwołują się te informacje. Klienci muszą nasłuchiwać, `ToolTipOpenedEvent` Aby zapewnić spójność uzyskiwania informacji zawartych w etykietach narzędzi.  
  
<a name="Required_UI_Automation_Properties"></a>

## <a name="required-ui-automation-properties"></a>Wymagane właściwości automatyzacji interfejsu użytkownika  

 Poniższa tabela zawiera listę [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] właściwości, których wartość lub definicja jest szczególnie istotna dla kontrolek etykietki narzędzi. Aby uzyskać więcej informacji na temat [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] właściwości, zobacz [właściwości automatyzacji interfejsu użytkownika dla klientów](ui-automation-properties-for-clients.md).  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] Wartość|Wartość|Uwagi|  
|------------------------------------------------------------------------------------|-----------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|Zobacz uwagi.|Wartość tej właściwości musi być unikatowa dla wszystkich kontrolek w aplikacji.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|Zobacz uwagi.|Najbardziej zewnętrzny prostokąt, który zawiera cały formant.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|Zobacz uwagi.|Punkt kliknięcia powinien być częścią etykietki narzędzia, która spowoduje odłączenie formantu. Niektóre porady narzędziowe nie mają tej możliwości i nie będą miały punktu kliknięcia.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|Zobacz uwagi.|Jeśli formant może odbierać fokus klawiatury, musi obsługiwać tę właściwość.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|Zobacz uwagi.|Nazwa kontrolki etykietki narzędzia jest tekstem wyświetlanym w etykietce narzędzia.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|`Null`|Kontrolki etykietki narzędzi są zawsze z własnym oznaczeniem przez ich zawartość.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|ToolTip|Ta wartość jest taka sama dla wszystkich platform interfejsu użytkownika.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|"etykietka narzędzia"|Zlokalizowany ciąg odpowiadający typowi kontrolki ToolTip.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|Zależy od|Jeśli formant etykietki narzędzia może odbierać fokus klawiatury, musi on znajdować się w widoku zawartości drzewa. Jeśli jest to tylko tekst, jest on dostępny jako HelpTextProperty z formantu, który go wywołał.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|Prawda|Kontrolka etykietki narzędzia musi być zawsze kontrolką.|  
  
<a name="Required_UI_Automation_Control_Patterns"></a>

## <a name="required-ui-automation-control-patterns"></a>Wymagane wzorce kontrolek automatyzacji interfejsu użytkownika  

 Poniższa tabela zawiera listę [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] wzorców formantów wymaganych do obsługi przez kontrolki etykietki narzędzi. Aby uzyskać więcej informacji na temat wzorców kontroli, zobacz [Wzorce formantów automatyzacji interfejsu użytkownika — omówienie](ui-automation-control-patterns-overview.md).  
  
|Wzorzec kontrolki|Pomoc techniczna|Uwagi|  
|---------------------|-------------|-----------|  
|<xref:System.Windows.Automation.Provider.IWindowProvider>|Zależy od|Porady dotyczące narzędzi, które można zamknąć przez kliknięcie elementu interfejsu użytkownika, muszą obsługiwać WindowPattern, aby mogły zostać zamknięte automatycznie.|  
|<xref:System.Windows.Automation.Provider.ITextProvider>|Zależy od|Aby zapewnić lepszą dostępność, formant etykietki narzędzia może obsługiwać wzorzec kontrolki tekstu, chociaż nie jest to wymagane. Wzorzec kontrolki tekstu jest przydatny, gdy tekst ma bogaty styl i atrybuty (na przykład kolor, pogrubienie i kursywa).|  
  
<a name="Required_UI_Automation_Events"></a>

## <a name="required-ui-automation-events"></a>Wymagane zdarzenia automatyzacji interfejsu użytkownika  

 Kontrolki etykietki narzędzi muszą podnieść, `ToolTipOpenedEvent` kiedy pojawiają się na ekranie. Zdarzenie będzie zawierać odwołanie do [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] elementu etykietki narzędzia.  
  
 Poniższa tabela zawiera listę [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] zdarzeń wymaganych do obsługi przez wszystkie kontrolki etykietki narzędzi. Aby uzyskać więcej informacji na temat zdarzeń, zobacz [Omówienie zdarzeń automatyzacji interfejsu użytkownika](ui-automation-events-overview.md).  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] Wydarzen|Pomoc techniczna|Uwagi|  
|---------------------------------------------------------------------------------|-------------|-----------|  
|<xref:System.Windows.Automation.TextPatternIdentifiers.TextSelectionChangedEvent>|Zależy od|Brak|  
|<xref:System.Windows.Automation.TextPatternIdentifiers.TextChangedEvent>|Zależy od|Brak|  
|<xref:System.Windows.Automation.WindowPatternIdentifiers.WindowClosedEvent>|Zależy od|Brak|  
|<xref:System.Windows.Automation.WindowPatternIdentifiers.WindowOpenedEvent>|Zależy od|Brak|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ToolTipOpenedEvent>|Wymagany|Brak|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ToolTipClosedEvent>|Wymagany|Brak|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty> zdarzenie zmiany właściwości.|Wymagany|Brak|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty> zdarzenie zmiany właściwości.|Wymagany|Brak|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> zdarzenie zmiany właściwości.|Wymagany|Brak|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty> zdarzenie zmiany właściwości.|Wymagany|Brak|  
|<xref:System.Windows.Automation.WindowPatternIdentifiers.WindowVisualStateProperty> zdarzenie zmiany właściwości.|Zależy od|Brak|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|Wymagany|Brak|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|Wymagany|Brak|  
  
## <a name="see-also"></a>Zobacz też

- <xref:System.Windows.Automation.ControlType.ToolTip>
- [Typy formantów automatyzacji interfejsu użytkownika — omówienie](ui-automation-control-types-overview.md)
- [Przegląd automatyzacji interfejsu użytkownika](ui-automation-overview.md)
