---
title: Obsługa automatyzacji interfejsu użytkownika dla kontrolek typu miniatura
description: Uzyskaj informacje na temat obsługi automatyzacji interfejsu użytkownika dla kontrolek typu kciuk. Poznaj wymaganą strukturę drzewa, właściwości, wzorce formantów i zdarzenia.
ms.date: 03/30/2017
helpviewer_keywords:
- control types, Thumb
- UI Automation, Thumb control type
- Thumb control type
ms.assetid: 13636338-e320-4355-b071-ede20a3fb1de
ms.openlocfilehash: 4a5aca4786fea2f4f258b6dde998287ea123b940
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/24/2020
ms.locfileid: "87168392"
---
# <a name="ui-automation-support-for-the-thumb-control-type"></a>Obsługa automatyzacji interfejsu użytkownika dla kontrolek typu miniatura
> [!NOTE]
> Ta dokumentacja jest przeznaczona dla .NET Framework deweloperów, którzy chcą korzystać z zarządzanych [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] klas zdefiniowanych w <xref:System.Windows.Automation> przestrzeni nazw. Aby uzyskać najnowsze informacje na temat [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] , zobacz [interfejs API usługi Windows Automation: Automatyzacja interfejsu użytkownika](/windows/win32/winauto/entry-uiauto-win32).  
  
 Ten temat zawiera informacje [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] na temat obsługi typu formantu kciuk. W programie [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] Typ kontrolki jest zestawem warunków, które formant musi spełniać, aby można było użyć <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty> właściwości. Warunki obejmują określone wytyczne dotyczące [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] struktury drzewa, [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] wartości właściwości i wzorców formantów.  
  
 Kontrolki kciuka zapewniają funkcje, które umożliwiają przeniesienie (lub przeciągnięcie) kontrolki, takie jak przycisk paska przewijania lub zmiany rozmiaru, na przykład widżet Zmienianie rozmiaru okna. Kontrolki kciuka można również zaimplementować jako ruchome obramowania okienek. Należy pamiętać, że nie zapewnia funkcji przeciągania i upuszczania. Kontrolki kciuka mogą odbierać fokus myszy, ale zazwyczaj nie jest to fokus klawiatury. Deweloper kontroli musi zaimplementować kontrolkę tak, aby działała prawidłowo (można ją przeciągać lub zmieniać jej rozmiar).  
  
 W poniższych sekcjach opisano wymaganą [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] strukturę drzewa, właściwości, wzorce formantów i zdarzenia dla typu formantu kciuk. [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]Wymagania stosują się do wszystkich kontrolek kciuka, [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)] systemu Win32 lub Windows Forms.  
  
<a name="Required_UI_Automation_Tree_Structure"></a>
## <a name="required-ui-automation-tree-structure"></a>Wymagana struktura drzewa automatyzacji interfejsu użytkownika  
 W poniższej tabeli przedstawiono widok kontrolki i widok zawartości [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] drzewa, które odnoszą się do kontrolek kciuka i opisano, co może być zawarte w poszczególnych widokach. Aby uzyskać więcej informacji na temat [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] drzewa, zobacz [drzewo automatyzacji interfejsu użytkownika — omówienie](ui-automation-tree-overview.md).  
  
|Widok kontrolki|Widok zawartości|  
|------------------|------------------|  
|Thumb|-Nie dotyczy|  
  
 Kontrolki kciuka nigdy nie pojawiają się w widoku zawartości, ponieważ istnieją tylko na potrzeby manipulowania myszą. Ich funkcjonalność jest uwidaczniana, chociaż inny wzorzec kontrolki, taki jak wzorzec przewijania, wzór przekształcenia lub wzorzec RangeValue dla, jest obsługiwany przez kontener kciuka.  
  
<a name="Required_UI_Automation_Properties"></a>
## <a name="required-ui-automation-properties"></a>Wymagane właściwości automatyzacji interfejsu użytkownika  
 Poniższa tabela zawiera listę [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] właściwości, których wartość lub definicja jest szczególnie istotna dla kontrolek przycisku przewijania. Aby uzyskać więcej informacji na temat [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] właściwości, zobacz [właściwości automatyzacji interfejsu użytkownika dla klientów](ui-automation-properties-for-clients.md).  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]Wartość|Wartość|Uwagi|  
|------------------------------------------------------------------------------------|-----------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|Zobacz uwagi.|Wartość tej właściwości musi być unikatowa dla wszystkich kontrolek w aplikacji.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|Zobacz uwagi.|Najbardziej zewnętrzny prostokąt, który zawiera cały formant.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|Zobacz uwagi.|Dowolny punkt w obszarze widocznego klienta kontrolki kciuka.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|Zobacz uwagi.|Jeśli formant może odbierać fokus klawiatury, musi obsługiwać tę właściwość.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|`Null`|Kontrolka kciuka nie jest dostępna w widoku zawartości drzewa automatyzacji interfejsu użytkownika, więc nie wymaga nazwy.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|`Null`|Kontrolki kciuka nigdy nie mają etykiety.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|Thumb|Ta wartość jest taka sama dla wszystkich platform interfejsu użytkownika.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|odcisk|Zlokalizowany ciąg odpowiadający typowi formantu kciuka.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|Fałsz|Kontrolka kciuka nigdy nie jest zawartością.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|Prawda|Kontrolka kciuka musi być zawsze kontrolką.|  
  
<a name="Required_UI_Automation_Control_Patterns"></a>
## <a name="required-ui-automation-control-patterns"></a>Wymagane wzorce kontrolek automatyzacji interfejsu użytkownika  
 W poniższej tabeli wymieniono [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] wzorce kontrolki wymagane do obsługi przez kontrolki miniatur. Aby uzyskać więcej informacji na temat wzorców kontroli, zobacz [Wzorce formantów automatyzacji interfejsu użytkownika — omówienie](ui-automation-control-patterns-overview.md).  
  
|Wzorzec kontrolki/Właściwość wzorca|Obsługa/wartość|Uwagi|  
|---------------------------------------|--------------------|-----------|  
|<xref:System.Windows.Automation.Provider.ITransformProvider>|Wymagane|Umożliwia przeniesienie kontrolki kciuka na ekranie.|  
  
<a name="Required_UI_Automation_Events"></a>
## <a name="required-ui-automation-events"></a>Wymagane zdarzenia automatyzacji interfejsu użytkownika  
 Poniższa tabela zawiera listę [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] zdarzeń wymaganych do obsługi przez wszystkie kontrolki kciuka. Aby uzyskać więcej informacji na temat zdarzeń, zobacz [Omówienie zdarzeń automatyzacji interfejsu użytkownika](ui-automation-events-overview.md).  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]Wydarzen|Pomoc techniczna|Uwagi|  
|---------------------------------------------------------------------------------|-------------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>zdarzenie zmiany właściwości.|Wymagane|Brak|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty>zdarzenie zmiany właściwości.|Wymagane|Brak|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty>zdarzenie zmiany właściwości.|Wymagane|Brak|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|Wymagane|Brak|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|Wymagane|Brak|  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Windows.Automation.ControlType.Thumb>
- [Typy formantów automatyzacji interfejsu użytkownika — omówienie](ui-automation-control-types-overview.md)
- [Przegląd automatyzacji interfejsu użytkownika](ui-automation-overview.md)
