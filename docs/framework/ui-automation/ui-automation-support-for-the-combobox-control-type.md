---
title: Obsługa automatyzacji interfejsu użytkownika dla typu formantu ComboBox
description: Uzyskaj informacje na temat obsługi automatyzacji interfejsu użytkownika dla kontrolek typu ComboBox. Poznaj wymaganą strukturę drzewa, właściwości, wzorce formantów i zdarzenia.
ms.date: 03/30/2017
helpviewer_keywords:
- control types, Combo Box
- UI Automation, Combo Box control type
- ComboBox controls
ms.assetid: bb321126-4770-41da-983a-67b7b89d45dd
ms.openlocfilehash: 11cc12dc78c74a294472ec7831548c50960147d0
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96260997"
---
# <a name="ui-automation-support-for-the-combobox-control-type"></a>Obsługa automatyzacji interfejsu użytkownika dla typu formantu ComboBox

> [!NOTE]
> Ta dokumentacja jest przeznaczona dla .NET Framework deweloperów, którzy chcą korzystać z zarządzanych [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] klas zdefiniowanych w <xref:System.Windows.Automation> przestrzeni nazw. Aby uzyskać najnowsze informacje na temat [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] , zobacz [interfejs API usługi Windows Automation: Automatyzacja interfejsu użytkownika](/windows/win32/winauto/entry-uiauto-win32).  
  
 Ten temat zawiera informacje [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] na temat obsługi typu formantu ComboBox. W programie [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] Typ kontrolki jest zestawem warunków, które formant musi spełniać, aby można było użyć <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty> właściwości. Warunki obejmują określone wytyczne dotyczące [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] struktury drzewa, [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] wartości właściwości, wzorców formantów i [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] zdarzeń.  
  
 Pole kombi to pole listy połączone z kontrolką statyczną lub kontrolka edycji, która wyświetla aktualnie zaznaczony element w części pola kombi. Część pola listy kontrolki jest wyświetlana przez cały czas lub pojawia się tylko wtedy, gdy użytkownik wybierze strzałkę listy rozwijanej (która jest przyciskiem push) obok formantu. Jeśli pole wyboru jest kontrolką edycji, użytkownik może wprowadzić informacje, których nie ma na liście. w przeciwnym razie użytkownik może wybrać tylko elementy z listy.  
  
 W poniższych sekcjach opisano wymaganą [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] strukturę drzewa, właściwości, wzorce formantów i zdarzenia dla typu formantu ComboBox. [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]Wymagania stosują się do wszystkich kontrolek pola kombi, [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)] systemu Win32 lub Windows Forms.  
  
<a name="Required_UI_Automation_Tree_Structure"></a>

## <a name="required-ui-automation-tree-structure"></a>Wymagana struktura drzewa automatyzacji interfejsu użytkownika  

 W poniższej tabeli przedstawiono widok kontrolki i widok zawartości [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] drzewa, które odnoszą się do kontrolek pola kombi i opisano, co może być zawarte w poszczególnych widokach. Aby uzyskać więcej informacji na temat [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] drzewa, zobacz [Omówienie drzewa automatyzacji interfejsu użytkownika](ui-automation-tree-overview.md).  
  
|Widok kontrolki|Widok zawartości|  
|------------------|------------------|  
|ComboBox<br /><br /> -Edit (0 lub 1)<br />-List (1)<br />-Element listy (element podrzędny z listy; 0 do wielu)<br />-Przycisk (1)|ComboBox<br /><br /> -Element listy (od 0 do wielu)|  
  
 Kontrolka edycji w formancie kontrolki pola kombi jest niezbędna tylko wtedy, gdy pole kombi można edytować, aby wykonać dowolne dane wejściowe, podobnie jak w przypadku pola kombi w oknie dialogowym Uruchamianie.  
  
<a name="Required_UI_Automation_Properties"></a>

## <a name="required-ui-automation-properties"></a>Wymagane właściwości automatyzacji interfejsu użytkownika  

 Poniższa tabela zawiera listę [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] właściwości, których wartość lub definicja jest szczególnie istotna dla kontrolek pola kombi. Aby uzyskać więcej informacji na temat [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] właściwości, zobacz [właściwości automatyzacji interfejsu użytkownika dla klientów](ui-automation-properties-for-clients.md).  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] Wartość|Wartość|Uwagi|  
|------------------------------------------------------------------------------------|-----------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|Zobacz uwagi.|Wartość tej właściwości musi być unikatowa dla wszystkich kontrolek w aplikacji.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|Zobacz uwagi.|Najbardziej zewnętrzny prostokąt, który zawiera cały formant.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|Zobacz uwagi.|Obsługiwane, jeśli istnieje prostokąt ograniczający. Jeśli nie każdy punkt wewnątrz prostokąta ograniczenia jest klikany, a będziesz wykonywał wyspecjalizowane Testy trafień, a następnie przesłonić i udostępnić punkt kliknięcia.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|ComboBox|Ta wartość jest taka sama dla wszystkich [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] platform.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.HelpTextProperty>|Zobacz uwagi.|Tekst pomocy dla kontrolek pola kombi powinien wyjaśnić, dlaczego użytkownik jest proszony o wybranie opcji z pola kombi. Tekst jest podobny do informacji przedstawionych za pomocą etykietki narzędzia. Na przykład "Wybierz element, aby ustawić rozdzielczość ekranu monitora".|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|Prawda|Kontrolki pola kombi zawsze znajdują się w widoku zawartości [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] drzewa.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|Prawda|Kontrolki pola kombi są zawsze dołączane do widoku kontrolki [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] drzewa.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|Prawda|Kontrolki pola kombi uwidaczniają zestaw elementów z kontenera zaznaczania. Kontrolka pola kombi może odbierać fokus klawiatury, chociaż gdy klient automatyzacji interfejsu użytkownika ustawi fokus w polu kombi, wszystkie elementy w poddrzewie pola kombi mogą mieć fokus.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|Zobacz uwagi.|Kontrolki pola kombi zwykle mają statyczną etykietę tekstową, do której odwołuje się ta właściwość.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|"pole kombi"|Zlokalizowany ciąg odpowiadający typowi kontrolki ComboBox.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|Zobacz uwagi.|Kontrolka pola kombi zazwyczaj pobiera swoją nazwę z statycznej kontrolki tekstowej.|  
  
<a name="Required_UI_Automation_Control_Patterns"></a>

## <a name="required-ui-automation-control-patterns"></a>Wymagane wzorce kontrolek automatyzacji interfejsu użytkownika  

 W poniższej tabeli wymieniono [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] wzorce kontrolki wymagane do obsługi przez wszystkie kontrolki pola kombi. Aby uzyskać więcej informacji na temat wzorców kontroli, zobacz [Wzorce formantów automatyzacji interfejsu użytkownika — omówienie](ui-automation-control-patterns-overview.md).  
  
|Wzorzec kontrolki|Pomoc techniczna|Uwagi|  
|---------------------|-------------|-----------|  
|<xref:System.Windows.Automation.Provider.IExpandCollapseProvider>|Tak|Kontrolka pola kombi musi zawsze zawierać przycisk listy rozwijanej, aby być polem kombi.|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider>|Tak|Wyświetla bieżące zaznaczenie w polu kombi. Ta obsługa jest delegowana do pola listy poniżej pola kombi.|  
|<xref:System.Windows.Automation.Provider.IValueProvider>|Zależy od|Jeśli pole kombi ma możliwość wykonania dowolnych wartości tekstowych, wzorzec wartości musi być obsługiwany. Ten wzorzec pozwala programistycznie ustawiać zawartość ciągu pola kombi. Jeśli wzorzec wartości nie jest obsługiwany, oznacza to, że użytkownik musi dokonać wyboru z listy elementów w poddrzewie pola kombi.|  
|<xref:System.Windows.Automation.Provider.IScrollProvider>|Nigdy|Wzorzec przewijania nigdy nie jest obsługiwany w polu kombi. Jest obsługiwana, jeśli pole listy zawarte w polu kombi można przewijać. Może być obsługiwane tylko wtedy, gdy pole listy jest widoczne na ekranie.|  
  
<a name="Required_Events"></a>

## <a name="required-events"></a>Wymagane zdarzenia  

 Poniższa tabela zawiera listę [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] zdarzeń wymaganych do obsługi przez wszystkie kontrolki pola kombi. Aby uzyskać więcej informacji na temat zdarzeń, zobacz [Omówienie zdarzeń automatyzacji interfejsu użytkownika](ui-automation-events-overview.md).  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] Wydarzen|Pomoc techniczna|Uwagi|  
|---------------------------------------------------------------------------------|-------------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|Wymagany|Brak|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty> zdarzenie zmiany właściwości.|Wymagany|Brak|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty> zdarzenie zmiany właściwości.|Wymagany|Brak|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> zdarzenie zmiany właściwości.|Wymagany|Brak|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|Wymagany|Brak|  
|<xref:System.Windows.Automation.ExpandCollapsePatternIdentifiers.ExpandCollapseStateProperty> zdarzenie zmiany właściwości.|Wymagany|Brak|  
|<xref:System.Windows.Automation.ValuePatternIdentifiers.ValueProperty> zdarzenie zmiany właściwości.|Zależy od|Jeśli formant obsługuje wzorzec wartości, musi obsługiwać to zdarzenie.|  
  
## <a name="see-also"></a>Zobacz też

- <xref:System.Windows.Automation.ControlType.ComboBox>
- [Typy formantów automatyzacji interfejsu użytkownika — omówienie](ui-automation-control-types-overview.md)
- [Przegląd automatyzacji interfejsu użytkownika](ui-automation-overview.md)
