---
title: Obsługa automatyzacji interfejsu użytkownika dla kontrolek typu lista
description: Uzyskaj informacje na temat obsługi automatyzacji interfejsu użytkownika dla typu formantu listy. Poznaj wymaganą strukturę drzewa, właściwości, wzorce formantów i zdarzenia.
ms.date: 03/30/2017
helpviewer_keywords:
- control types, List
- List control type
- UI Automation, List control type
ms.assetid: 0e959fcb-50f2-413b-948d-7167d279bc11
ms.openlocfilehash: b56856e3157ad4b770173cf0b34c7e092ffff075
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96247242"
---
# <a name="ui-automation-support-for-the-list-control-type"></a>Obsługa automatyzacji interfejsu użytkownika dla kontrolek typu lista

> [!NOTE]
> Ta dokumentacja jest przeznaczona dla .NET Framework deweloperów, którzy chcą korzystać z zarządzanych [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] klas zdefiniowanych w <xref:System.Windows.Automation> przestrzeni nazw. Aby uzyskać najnowsze informacje na temat [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] , zobacz [interfejs API usługi Windows Automation: Automatyzacja interfejsu użytkownika](/windows/win32/winauto/entry-uiauto-win32).  
  
 Ten temat zawiera informacje [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] na temat obsługi typu formantu listy. W programie [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] Typ kontrolki jest zestawem warunków, które formant musi spełniać, aby można było użyć <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty> właściwości. Warunki obejmują określone wytyczne dotyczące [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] struktury drzewa, [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] wartości właściwości i wzorców formantów.  
  
 Typ kontrolki listy umożliwia organizowanie płaskiej grupy lub grup elementów i umożliwia użytkownikowi wybranie co najmniej jednego z tych elementów. Typ formantu listy ma swobodne ograniczenie dotyczące typów elementów podrzędnych, które może zawierać. Dzięki temu dostawcy automatyzacji interfejsu użytkownika mogą obsługiwać dobrze znany element dla kontenerów wyboru.  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]Wymagania zawarte w poniższych sekcjach mają zastosowanie do wszystkich kontrolek, które implementują typ kontrolki list, niezależnie od tego [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)] , czy Win32 czy Windows Forms. Lista formantów kontenera jest przykładem formantów, które implementują typ kontrolki listy.  
  
<a name="Required_UI_Automation_Tree_Structure"></a>

## <a name="required-ui-automation-tree-structure"></a>Wymagana struktura drzewa automatyzacji interfejsu użytkownika  

 W poniższej tabeli przedstawiono dwa widoki [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] drzewa, które odnoszą się do kontrolek listy, i opisano, co może być zawarte w poszczególnych widokach. Widok kontrolki zawiera tylko elementy, które są kontrolkami, a widok zawartości usuwa nadmiarowe informacje z drzewa. Na przykład kontrolka tekstowa użyta do etykietowania pola kombi zostanie uwidoczniona jako `ComboBox NameProperty` . Ponieważ kontrolka tekst jest już uwidoczniona w ten sposób, za pomocą widoku kontroli nie ma potrzeby uwidocznić go dwukrotnie. w związku z tym zostanie on usunięty z widoku zawartości. Aby uzyskać więcej informacji na temat [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] drzewa, zobacz [drzewo automatyzacji interfejsu użytkownika — omówienie](ui-automation-tree-overview.md).  
  
|Widok kontrolki|Widok zawartości|  
|------------------|------------------|  
|Zawiera elementy, które odpowiadają kontrolkom.|Usuwa nadmiarowe informacje z drzewa, dzięki czemu technologie pomocnicze pracują z najmniejszym zestawem istotnych informacji dla użytkownika końcowego.|  
|Lista<br /><br /> -Element (0 lub więcej)<br />-ListItem (0 lub więcej)<br />-Grupa (0 lub więcej)<br />-ScrollBar (0, 1 lub 2)|Lista<br /><br /> -Element (0 lub więcej)<br />-ListItem (0 lub więcej)<br />-Grupa (0 lub więcej)|  
  
 Widok kontroli dla kontrolki implementującej typ kontrolki listy (na przykład kontrolka listy) składa się z:  
  
- Zero lub więcej elementów w kontrolce listy (elementy mogą opierać się na elemencie listy lub typach formantów elementu danych).
  
- Zero lub więcej kontrolek grupy w kontrolce listy.
  
- Zero, jeden lub dwie kontrolki paska przewijania.
  
Widok zawartości kontrolki implementującej typ kontrolki listy (na przykład kontrolka listy) składa się z:  
  
- Zero lub więcej elementów w kontrolce listy (elementy mogą opierać się na elemencie listy lub typach formantów elementu danych).
  
- Zero lub więcej grup w kontrolce listy.

Kontrolka listy nie może mieć elementów, które mają relację hierarchiczną inną niż zgrupowana. Jeśli elementy znajdują się w [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] drzewie, kontener listy powinien opierać się na typie formantu drzewa.  
  
 Elementy możliwe do wyboru w kontrolce listy będą dostępne z elementów podrzędnych w [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] drzewie kontrolki listy. Wszystkie elementy w kontrolce listy muszą należeć do tej samej grupy wyboru. Elementy możliwe do wyboru na liście powinny być uwidocznione jako typy kontrolne (zamiast elementu dane).  
  
<a name="Required_UI_Automation_Properties"></a>

## <a name="required-ui-automation-properties"></a>Wymagane właściwości automatyzacji interfejsu użytkownika  

 Poniższa tabela zawiera listę [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] właściwości, których wartość lub definicja jest szczególnie istotna dla formantów listy. Aby uzyskać więcej informacji na temat [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] właściwości, zobacz [właściwości automatyzacji interfejsu użytkownika dla klientów](ui-automation-properties-for-clients.md).  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] Wartość|Wartość|Uwagi|  
|------------------------------------------------------------------------------------|-----------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|Zobacz uwagi.|Wartość tej właściwości musi być unikatowa dla wszystkich kontrolek w aplikacji.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|Zobacz uwagi.|Najbardziej zewnętrzny prostokąt, który zawiera cały formant.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|Zobacz uwagi.|Jeśli kontrolka listy ma punkt kliknięcia (punkt, który może być kliknięty, aby spowodować, że lista zostanie skoncentrowana), ten punkt musi być narażony za pomocą tej właściwości.<br /><br /> Jeśli wartość `IsOffScreen` właściwości ma wartość true, <xref:System.Windows.Automation.NoClickablePointException> zostanie wyniesiona.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|Zobacz uwagi.|Jeśli formant może odbierać fokus klawiatury, musi obsługiwać tę właściwość.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|Zobacz uwagi.|Wartość właściwości Nazwa kontrolki listy powinna przekazać kategorię opcji, z których użytkownik jest proszony o wybranie. Ta właściwość zwykle Pobiera nazwę z statycznej etykiety tekstowej. Jeśli nie istnieje etykieta tekstu statycznego, Deweloper aplikacji musi uwidocznić wartość właściwości Nazwa.<br /><br /> Jedynym czasem, gdy ta właściwość nie jest wymagana dla formantów list, jest używana w ramach poddrzewa innej kontrolki.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|Zobacz uwagi.|Jeśli istnieje statyczna etykieta tekstowa, ta właściwość musi ujawniać odwołanie do tej kontrolki.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|Lista|Ta wartość jest taka sama dla wszystkich platform interfejsu użytkownika.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|staw|Zlokalizowany ciąg odpowiadający typowi formantu listy.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|Prawda|Kontrolka listy jest zawsze uwzględniona w widoku zawartości [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] drzewa.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|Prawda|Kontrolka listy jest zawsze uwzględniona w widoku kontrolki [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] drzewa.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|Prawda|Jeśli kontener może przyjmować dane wejściowe z klawiatury, ta wartość właściwości powinna mieć wartość true.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.HelpTextProperty>|Zobacz uwagi.|Tekst pomocy dla kontrolek listy powinien wyjaśnić, dlaczego użytkownik jest proszony o dokonanie wyboru z listy opcji. Na przykład "zaznaczenie elementu z tej listy ustawi rozdzielczość ekranu dla monitora".|  
  
<a name="Required_UI_Automation_Control_Patterns"></a>

## <a name="required-ui-automation-control-patterns-and-properties"></a>Wymagane wzorce i właściwości formantów automatyzacji interfejsu użytkownika  

 W poniższej tabeli wymieniono [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] wzorce kontrolki wymagane do obsługi przez kontrolki listy. Aby uzyskać więcej informacji na temat wzorców kontroli, zobacz [Wzorce formantów automatyzacji interfejsu użytkownika — omówienie](ui-automation-control-patterns-overview.md).  
  
|Wzorzec kontrolki/Właściwość wzorca|Obsługa/wartość|Uwagi|  
|---------------------------------------|--------------------|-----------|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider>|Wymagany|Wszystkie kontrolki, które obsługują typ kontrolki listy, muszą implementować, `ISelectionProvider` gdy stan zaznaczenia jest obsługiwany między elementami zawartymi w kontrolce. Jeśli elementy w kontenerze nie są możliwe do wyboru, należy użyć typu kontrolki Grupa.|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider.IsSelectionRequired%2A>|Zależy od|Kontrolki listy nie zawsze wymagają wybrania elementu.|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider.CanSelectMultiple%2A>|Zależy od|Formanty listy mogą być kontenerami jednego lub wielokrotnego wyboru.|  
|<xref:System.Windows.Automation.Provider.IScrollProvider>|Zależy od|Zaimplementuj ten wzorzec kontrolki, jeśli elementy w kontenerze są przewijane.|  
|<xref:System.Windows.Automation.Provider.IGridProvider>|Zależy od|Zaimplementuj ten wzorzec, gdy Nawigacja siatki musi być dostępna dla elementu na podstawie elementu.|  
|<xref:System.Windows.Automation.Provider.IMultipleViewProvider>|Zależy od|Zaimplementuj ten wzorzec kontrolki, jeśli formant może obsługiwać wiele widoków elementów w kontenerze.|  
|<xref:System.Windows.Automation.Provider.ITableProvider>|Nigdy|`ITableProvider` nie jest nigdy obsługiwane dla typu formantu listy. Jeśli formant powinien obsługiwać ten wzorzec kontrolki, formant powinien opierać się na typie formantu siatki danych.|  
  
<a name="Required_UI_Automation_Events"></a>

## <a name="required-ui-automation-events"></a>Wymagane zdarzenia automatyzacji interfejsu użytkownika  

 Poniższa tabela zawiera listę [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] zdarzeń wymaganych do obsługi przez wszystkie kontrolki listy. Aby uzyskać więcej informacji na temat zdarzeń, zobacz [Omówienie zdarzeń automatyzacji interfejsu użytkownika](ui-automation-events-overview.md).  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] Wydarzen|Obsługa/wartość|Uwagi|  
|---------------------------------------------------------------------------------|--------------------|-----------|  
|<xref:System.Windows.Automation.SelectionPatternIdentifiers.InvalidatedEvent>|Zależy od|Brak|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LayoutInvalidatedEvent>|Zależy od|Brak|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty> zdarzenie zmiany właściwości.|Wymagany|Brak|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty> zdarzenie zmiany właściwości.|Wymagany|Brak|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> zdarzenie zmiany właściwości.|Wymagany|Brak|  
|<xref:System.Windows.Automation.MultipleViewPatternIdentifiers.CurrentViewProperty> zdarzenie zmiany właściwości.|Zależy od|Brak|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontallyScrollableProperty> zdarzenie zmiany właściwości.|Zależy od|Brak|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontalScrollPercentProperty> zdarzenie zmiany właściwości.|Zależy od|Brak|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.HorizontalViewSizeProperty> zdarzenie zmiany właściwości.|Zależy od|Brak|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticalScrollPercentProperty> zdarzenie zmiany właściwości.|Zależy od|Brak|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticallyScrollableProperty> zdarzenie zmiany właściwości.|Zależy od|Brak|  
|<xref:System.Windows.Automation.ScrollPatternIdentifiers.VerticalViewSizeProperty> zdarzenie zmiany właściwości.|Zależy od|Brak|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|Wymagany|Brak|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|Wymagany|Brak|  
  
## <a name="see-also"></a>Zobacz też

- <xref:System.Windows.Automation.ControlType.List>
- [Typy formantów automatyzacji interfejsu użytkownika — omówienie](ui-automation-control-types-overview.md)
- [Przegląd automatyzacji interfejsu użytkownika](ui-automation-overview.md)
