---
title: Obsługa automatyzacji interfejsu użytkownika dla kontrolek typu StatusBar
description: Uzyskaj informacje na temat obsługi automatyzacji interfejsu użytkownika dla typu formantu StatusBar. Poznaj wymaganą strukturę drzewa, właściwości, wzorce formantów i zdarzenia.
ms.date: 03/30/2017
helpviewer_keywords:
- StatusBar control type
- UI Automation, Status Bar control type
- control types, Status Bar
ms.assetid: 48dee94a-5119-4939-a4c7-ffeaf794c732
ms.openlocfilehash: 04ef1e531a33486ad93d8f0540d8564ea8e9d222
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96267003"
---
# <a name="ui-automation-support-for-the-statusbar-control-type"></a>Obsługa automatyzacji interfejsu użytkownika dla kontrolek typu StatusBar

> [!NOTE]
> Ta dokumentacja jest przeznaczona dla .NET Framework deweloperów, którzy chcą korzystać z zarządzanych [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] klas zdefiniowanych w <xref:System.Windows.Automation> przestrzeni nazw. Aby uzyskać najnowsze informacje na temat [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] , zobacz [interfejs API usługi Windows Automation: Automatyzacja interfejsu użytkownika](/windows/win32/winauto/entry-uiauto-win32).  
  
 Ten temat zawiera informacje [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] na temat obsługi typu formantu StatusBar. W programie [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] Typ kontrolki jest zestawem warunków, które formant musi spełniać, aby można było użyć <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty> właściwości. Warunki obejmują określone wytyczne dotyczące [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] struktury drzewa, [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] wartości właściwości i wzorców formantów.  
  
 Kontrolka pasek stanu wyświetla informacje o obiekcie, który jest wyświetlany w oknie aplikacji, składniku obiektu lub informacji kontekstowych odnoszących się do operacji tego obiektu w aplikacji.  
  
 W poniższych sekcjach opisano wymaganą [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] strukturę drzewa, właściwości, wzorce formantów i zdarzenia dla typu formantu StatusBar. [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]Wymagania stosują się do wszystkich kontrolek paska stanu, czy [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)] Win32 lub Windows Forms.  
  
<a name="Required_UI_Automation_Tree_Structure"></a>

## <a name="required-ui-automation-tree-structure"></a>Wymagana struktura drzewa automatyzacji interfejsu użytkownika  

 W poniższej tabeli przedstawiono widok kontrolki i widok zawartości [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] drzewa, które odnoszą się do kontrolek paska stanu i opisano, co może być zawarte w poszczególnych widokach. Aby uzyskać więcej informacji na temat [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] drzewa, zobacz [drzewo automatyzacji interfejsu użytkownika — omówienie](ui-automation-tree-overview.md).  
  
|Widok kontrolki|Widok zawartości|  
|------------------|------------------|  
|StatusBar<br /><br /> -Edytuj (0 lub więcej)<br />-Pasek postępu (0 lub wiele)<br />-Image (0 lub wiele)<br />-Przycisk (0 lub wiele)|StatusBar<br /><br /> -Edytuj (0 lub więcej)<br />-ProgressBar (0 lub wiele)<br />-Image (0 lub wiele)<br />-Przycisk (0 lub wiele)|  
  
<a name="Required_UI_Automation_Properties"></a>

## <a name="required-ui-automation-properties"></a>Wymagane właściwości automatyzacji interfejsu użytkownika  

 Poniższa tabela zawiera listę [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] właściwości, których wartość lub definicja jest szczególnie istotna dla kontrolek paska postępu. Aby uzyskać więcej informacji na temat [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] właściwości, zobacz [właściwości automatyzacji interfejsu użytkownika dla klientów](ui-automation-properties-for-clients.md).  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] Wartość|Wartość|Uwagi|  
|------------------------------------------------------------------------------------|-----------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|Zobacz uwagi.|Wartość tej właściwości musi być unikatowa dla wszystkich kontrolek w aplikacji.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|Zobacz uwagi.|Prostokąt ograniczający pasek stanu musi obejmować wszystkie kontrolki znajdujące się w nim.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|Zobacz uwagi.|Obsługiwane, jeśli istnieje prostokąt ograniczający. Jeśli nie każdy punkt wewnątrz prostokąta ograniczenia jest klikany, a będziesz wykonywał wyspecjalizowane Testy trafień, a następnie przesłonić i udostępnić punkt kliknięcia.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|Zobacz uwagi.|Jeśli formant może odbierać fokus klawiatury, musi obsługiwać tę właściwość.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|Zobacz uwagi.|Kontrolka pasek stanu nie wymaga nazwy, chyba że w aplikacji jest używana więcej niż jedna. W takim przypadku należy odróżnić każdy pasek nazwami, takimi jak "status internetowy" lub "stan aplikacji".|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|`Null`|Kontrolka pasek stanu zwykle nie ma etykiety.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|StatusBar|Ta wartość jest taka sama dla wszystkich platform interfejsu użytkownika.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|"pasek stanu"|Zlokalizowany ciąg odpowiadający typowi kontrolce StatusBar.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|Prawda|Kontrolka pasek stanu zawsze zawiera zawartość.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|Prawda|Kontrolka pasek stanu jest zawsze kontrolką.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty>|Zależy od|Kontrolka pasek stanu zwróci wartość true dla tej właściwości, jeśli nie jest ona aktualnie widoczna na ekranie.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.OrientationProperty>|Zależy od|Wartość orientacji formantu: pozioma lub pionowa.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|Fałsz|Nie dotyczy|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AcceleratorKeyProperty>|`Null`|Paski stanu nie mają kluczy akceleratora.|  
  
<a name="Required_UI_Automation_Control_Patterns"></a>

## <a name="required-ui-automation-control-patterns"></a>Wymagane wzorce kontrolek automatyzacji interfejsu użytkownika  

 Poniższa tabela zawiera listę [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] wzorców formantów wymaganych do obsługi przez kontrolki paska stanu. Aby uzyskać więcej informacji na temat wzorców kontrolek, zobacz [Omówienie wzorców kontrolek automatyzacji interfejsu użytkownika](ui-automation-control-patterns-overview.md).  
  
|Wzorzec kontrolki|Pomoc techniczna|Uwagi|  
|---------------------|-------------|-----------|  
|<xref:System.Windows.Automation.Provider.IGridProvider>|Opcjonalne|Formanty paska stanu powinny obsługiwać wzorzec kontrolki siatki, dzięki czemu pojedyncze elementy mogą być monitorowane i łatwe do odwołuje się do informacji.|  
  
<a name="Required_UI_Automation_Events"></a>

## <a name="required-ui-automation-events"></a>Wymagane zdarzenia automatyzacji interfejsu użytkownika  

 Poniższa tabela zawiera listę [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] zdarzeń wymaganych do obsługi przez wszystkie kontrolki paska stanu. Aby uzyskać więcej informacji na temat zdarzeń, zobacz [Omówienie zdarzeń automatyzacji interfejsu użytkownika](ui-automation-events-overview.md).  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] Wydarzen|Pomoc techniczna|Uwagi|  
|---------------------------------------------------------------------------------|-------------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty> zdarzenie zmiany właściwości.|Wymagany|Brak|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty> zdarzenie zmiany właściwości.|Wymagany|Brak|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> zdarzenie zmiany właściwości.|Wymagany|Brak|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|Wymagany|Brak|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|Wymagany|Brak|  
  
## <a name="see-also"></a>Zobacz też

- <xref:System.Windows.Automation.ControlType.StatusBar>
- [Typy formantów automatyzacji interfejsu użytkownika — omówienie](ui-automation-control-types-overview.md)
- [Przegląd automatyzacji interfejsu użytkownika](ui-automation-overview.md)
