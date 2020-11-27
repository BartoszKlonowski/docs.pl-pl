---
title: Obsługa automatyzacji interfejsu użytkownika dla typu kontrolki TreeItem
description: Uzyskaj informacje na temat obsługi automatyzacji interfejsu użytkownika dla typu formantu TreeItem. Poznaj wymaganą strukturę drzewa, właściwości, wzorce formantów i zdarzenia.
ms.date: 03/30/2017
helpviewer_keywords:
- control types, Tree Item
- Tree Item control type
- UI Automation, Tree Item control type
ms.assetid: 229f341a-477f-434e-b877-4db9973068eb
ms.openlocfilehash: 4ad53ee63d5e3ebb2cdd845a1258d191fa9fb521
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96281274"
---
# <a name="ui-automation-support-for-the-treeitem-control-type"></a>Obsługa automatyzacji interfejsu użytkownika dla typu kontrolki TreeItem

> [!NOTE]
> Ta dokumentacja jest przeznaczona dla .NET Framework deweloperów, którzy chcą korzystać z zarządzanych [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] klas zdefiniowanych w <xref:System.Windows.Automation> przestrzeni nazw. Aby uzyskać najnowsze informacje na temat [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] , zobacz [interfejs API usługi Windows Automation: Automatyzacja interfejsu użytkownika](/windows/win32/winauto/entry-uiauto-win32).  
  
 Ten temat zawiera informacje [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] na temat obsługi typu formantu TreeItem. W programie [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] Typ kontrolki jest zestawem warunków, które formant musi spełniać, aby można było użyć <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty> właściwości. Warunki obejmują określone wytyczne dotyczące [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] struktury drzewa, [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] wartości właściwości i wzorców formantów.  
  
 Typ formantu TreeItem reprezentuje węzeł wewnątrz kontenera drzewa. Każdy węzeł może zawierać inne węzły, nazywane węzłami podrzędnymi. Węzły nadrzędne lub węzły, które zawierają węzły podrzędne, mogą być wyświetlane jako rozwinięte lub zwinięte.  
  
 W poniższych sekcjach opisano wymaganą [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] strukturę drzewa, właściwości, wzorce formantów i zdarzenia dla typu formantu TreeItem. [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]Wymagania stosują się do wszystkich kontrolek elementów drzewa, [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)] systemu Win32 lub Windows Forms.  
  
<a name="Required_UI_Automation_Tree_Structure"></a>

## <a name="required-ui-automation-tree-structure"></a>Wymagana struktura drzewa automatyzacji interfejsu użytkownika  

 W poniższej tabeli przedstawiono widok kontrolki i widok zawartości [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] drzewa, które odnoszą się do kontrolek elementów drzewa i opisano, co może być zawarte w poszczególnych widokach. Aby uzyskać więcej informacji na temat [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] drzewa, zobacz [drzewo automatyzacji interfejsu użytkownika — omówienie](ui-automation-tree-overview.md).  
  
|Widok kontrolki|Widok zawartości|  
|------------------|------------------|  
|TreeItem<br /><br /> -CheckBox (0 lub 1)<br />-Image (0 lub 1)<br />-Przycisk (0 lub 1)<br />-TreeItem (0 lub więcej)|TreeItem<br /><br /> -TreeItem (0 lub więcej)|  
  
 Kontrolki elementu drzewa mogą mieć zero lub więcej elementów podrzędnych elementu drzewa w widoku zawartości [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] drzewa. Jeśli formant elementu drzewa ma funkcje wykraczające poza to, co jest widoczne w wzorcach kontrolek wymienionych poniżej, formant powinien opierać się na typie formantu elementu danych.  
  
 Zwinięte elementy drzewa nie będą wyświetlane w widoku kontroli ani zawartości, dopóki nie staną się rozwinięte i widoczne (lub mogą być przewijane do widoku).  
  
 Widok kontrolki może zawierać dodatkowe szczegóły kontrolki, w tym skojarzony obraz lub przycisk. Na przykład element w widoku konspektu może zawierać obraz, a także przycisk umożliwiający rozwijanie lub zwijanie konspektu. Te obiekty szczegółów nie są wyświetlane w widoku zawartości, ponieważ informacje są już reprezentowane przez element drzewa nadrzędnego. Elementy drzewa, które są przewijane na ekranie, pojawią się zarówno w widoku kontrolki, jak i zawartości [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] drzewa i powinny mieć <xref:System.Windows.Automation.AutomationElement.IsOffscreenProperty> ustawioną wartość true.  
  
<a name="Required_UI_Automation_Properties"></a>

## <a name="required-ui-automation-properties"></a>Wymagane właściwości automatyzacji interfejsu użytkownika  

 Poniższa tabela zawiera listę [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] właściwości, których wartość lub definicja jest szczególnie istotna dla formantów listy. Aby uzyskać więcej informacji na temat [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] właściwości, zobacz [właściwości automatyzacji interfejsu użytkownika dla klientów](ui-automation-properties-for-clients.md).  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] Wartość|Wartość|Uwagi|  
|------------------------------------------------------------------------------------|-----------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|Zobacz uwagi.|Wartość tej właściwości musi być unikatowa dla wszystkich kontrolek w aplikacji.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|Zobacz uwagi.|Najbardziej zewnętrzny prostokąt, który zawiera cały formant.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|Zobacz uwagi.|Ta właściwość musi zwracać lokalizację elementu, który spowoduje zmianę stanu zaznaczenia lub ustawienie fokusu.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|TreeItem|Ta wartość jest taka sama dla wszystkich platform interfejsu użytkownika.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|Prawda|Kontrolka listy jest zawsze uwzględniona w widoku zawartości [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] drzewa.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|Prawda|Kontrolka listy jest zawsze uwzględniona w widoku kontrolki [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] drzewa.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty>|Zobacz uwagi.|Ta właściwość jest ustawiona, aby wskazać, kiedy kontrolka elementu drzewa jest przewijana na ekranie.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|Zobacz uwagi.|Jeśli formant może odbierać fokus klawiatury, musi obsługiwać tę właściwość.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ItemTypeProperty>|Zobacz uwagi.|Jeśli formant elementu drzewa używa ikony wizualizacji, aby wskazać, że jest określony typ obiektu, ta właściwość musi być obsługiwana i wskazuje, co to jest obiekt.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|`Null`|Kontrolki elementów drzewa są niezależne.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|"element drzewa"|Zlokalizowany ciąg odpowiadający typowi kontrolce TreeItem.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|Zobacz uwagi.|Ta właściwość uwidacznia tekst wyświetlany dla każdej kontrolki elementu drzewa.|  
  
<a name="Required_UI_Automation_Control_Patterns"></a>

## <a name="required-ui-automation-control-patterns"></a>Wymagane wzorce kontrolek automatyzacji interfejsu użytkownika  

 W poniższej tabeli wymieniono [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] wzorce kontrolki wymagane do obsługi przez kontrolki listy. Aby uzyskać więcej informacji na temat wzorców kontroli, zobacz [Wzorce formantów automatyzacji interfejsu użytkownika — omówienie](ui-automation-control-patterns-overview.md).  
  
|Wzorzec kontrolki/Właściwość wzorca|Obsługa/wartość|Uwagi|  
|---------------------------------------|--------------------|-----------|  
|<xref:System.Windows.Automation.Provider.IInvokeProvider>|Zależy od|Zaimplementuj ten wzorzec kontrolki, jeśli element drzewa ma oddzielne polecenie z możliwością wykonania akcji.|  
|<xref:System.Windows.Automation.Provider.IExpandCollapseProvider>|Tak|Wszystkie elementy drzewa mogą być rozwinięte lub zwinięte.|  
|<xref:System.Windows.Automation.Provider.IExpandCollapseProvider.ExpandCollapseState%2A>|Rozwinięty, zwinięty lub węzeł liścia|Elementy drzewa będą węzłami liścia, gdy nie są rozwinięte lub zwinięte.|  
|<xref:System.Windows.Automation.Provider.IScrollItemProvider>|Zależy od|Zaimplementuj ten wzorzec kontrolki, jeśli kontener drzewa obsługuje wzorzec kontrolki Scroll.|  
|<xref:System.Windows.Automation.Provider.ISelectionItemProvider>|Zależy od|Zaimplementuj ten wzorzec kontrolki, jeśli istnieje możliwość wybrania aktywnego zaznaczenia, które jest utrzymywane, gdy użytkownik powróci do kontenera drzewa.|  
|<xref:System.Windows.Automation.Provider.ISelectionItemProvider.SelectionContainer%2A>|Tak|Ta właściwość będzie uwidaczniać ten sam kontener dla wszystkich elementów w kontenerze.|  
|<xref:System.Windows.Automation.Provider.IToggleProvider>|Zależy od|Zaimplementuj ten wzorzec kontrolki, jeśli element drzewa ma skojarzone pole wyboru.|  
  
<a name="Required_UI_Automation_Events"></a>

## <a name="required-ui-automation-events"></a>Wymagane zdarzenia automatyzacji interfejsu użytkownika  

 Poniższa tabela zawiera listę [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] zdarzeń wymaganych do obsługi przez wszystkie kontrolki elementów drzewa. Aby uzyskać więcej informacji na temat zdarzeń, zobacz [Omówienie zdarzeń automatyzacji interfejsu użytkownika](ui-automation-events-overview.md).  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] Wydarzen|Pomoc techniczna|Uwagi|  
|---------------------------------------------------------------------------------|-------------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|Wymagany|Brak|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty> zdarzenie zmiany właściwości.|Wymagany|Brak|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> zdarzenie zmiany właściwości.|Wymagany|Brak|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty> zdarzenie zmiany właściwości.|Wymagany|Brak|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ItemStatusProperty> zdarzenie zmiany właściwości.|Zależy od|Brak|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty> zdarzenie zmiany właściwości.|Wymagany|Brak|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|Wymagany|Brak|  
|<xref:System.Windows.Automation.ExpandCollapsePatternIdentifiers.ExpandCollapseStateProperty> zdarzenie zmiany właściwości.|Wymagany|Brak|  
|<xref:System.Windows.Automation.InvokePatternIdentifiers.InvokedEvent>|Zależy od|Brak|  
|<xref:System.Windows.Automation.MultipleViewPatternIdentifiers.CurrentViewProperty> zdarzenie zmiany właściwości.|Zależy od|Brak|  
|<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementAddedToSelectionEvent>|Zależy od|Brak|  
|<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementRemovedFromSelectionEvent>|Zależy od|Brak|  
|<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementSelectedEvent>|Zależy od|Brak|  
|<xref:System.Windows.Automation.TogglePatternIdentifiers.ToggleStateProperty> zdarzenie zmiany właściwości.|Zależy od|Brak|  
|<xref:System.Windows.Automation.ValuePatternIdentifiers.ValueProperty> zdarzenie zmiany właściwości.|Zależy od|Brak|  
  
## <a name="see-also"></a>Zobacz też

- <xref:System.Windows.Automation.ControlType.TreeItem>
- [Typy formantów automatyzacji interfejsu użytkownika — omówienie](ui-automation-control-types-overview.md)
- [Przegląd automatyzacji interfejsu użytkownika](ui-automation-overview.md)
