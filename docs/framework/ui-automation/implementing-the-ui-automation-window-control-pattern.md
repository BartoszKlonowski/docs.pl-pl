---
title: Implementacja wzorca kontrolki okna automatyzacji interfejsu użytkownika
description: Zapoznaj się z wytycznymi i konwencjami, aby zaimplementować wzorzec kontrolki okna w automatyzacji interfejsu użytkownika. Znajomość wymaganych członków interfejsu IWindowProvider.
ms.date: 03/30/2017
helpviewer_keywords:
- control patterns, Window
- UI Automation, Window control pattern
- Window control pattern
ms.assetid: a28cb286-296e-4a62-b4cb-55ad636ebccc
ms.openlocfilehash: b43884393974e6f2863da6a4a5ca8f305e5a160c
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96286100"
---
# <a name="implementing-the-ui-automation-window-control-pattern"></a><span data-ttu-id="cd203-104">Implementacja wzorca kontrolki okna automatyzacji interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="cd203-104">Implementing the UI Automation Window Control Pattern</span></span>

> [!NOTE]
> <span data-ttu-id="cd203-105">Ta dokumentacja jest przeznaczona dla .NET Framework deweloperów, którzy chcą korzystać z zarządzanych [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] klas zdefiniowanych w <xref:System.Windows.Automation> przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="cd203-105">This documentation is intended for .NET Framework developers who want to use the managed [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] classes defined in the <xref:System.Windows.Automation> namespace.</span></span> <span data-ttu-id="cd203-106">Aby uzyskać najnowsze informacje na temat [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] , zobacz [interfejs API usługi Windows Automation: Automatyzacja interfejsu użytkownika](/windows/win32/winauto/entry-uiauto-win32).</span><span class="sxs-lookup"><span data-stu-id="cd203-106">For the latest information about [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], see [Windows Automation API: UI Automation](/windows/win32/winauto/entry-uiauto-win32).</span></span>  
  
 <span data-ttu-id="cd203-107">W tym temacie przedstawiono wskazówki i konwencje dotyczące wdrażania <xref:System.Windows.Automation.Provider.IWindowProvider> , w tym informacje o <xref:System.Windows.Automation.WindowPattern> właściwościach, metodach i zdarzeniach.</span><span class="sxs-lookup"><span data-stu-id="cd203-107">This topic introduces guidelines and conventions for implementing <xref:System.Windows.Automation.Provider.IWindowProvider>, including information about <xref:System.Windows.Automation.WindowPattern> properties, methods, and events.</span></span> <span data-ttu-id="cd203-108">Linki do dodatkowych odwołań znajdują się na końcu tematu.</span><span class="sxs-lookup"><span data-stu-id="cd203-108">Links to additional references are listed at the end of the topic.</span></span>  
  
 <span data-ttu-id="cd203-109"><xref:System.Windows.Automation.WindowPattern>Wzorzec kontrolki służy do obsługi kontrolek, które zapewniają podstawowe funkcje oparte na oknach w tradycyjnym graficznym interfejsie użytkownika (GUI).</span><span class="sxs-lookup"><span data-stu-id="cd203-109">The <xref:System.Windows.Automation.WindowPattern> control pattern is used to support controls that provide fundamental window-based functionality within a traditional graphical user interface (GUI).</span></span> <span data-ttu-id="cd203-110">Przykłady kontrolek, które muszą implementować ten wzorzec kontrolki obejmują okna aplikacji najwyższego poziomu, okna podrzędne interfejsu wielu dokumentów (MDI), okna dialogowe podziału o zmiennym rozmiarze, modalnych okien dialogowych i okien pomocy dymków.</span><span class="sxs-lookup"><span data-stu-id="cd203-110">Examples of controls that must implement this control pattern include top-level application windows, multiple-document interface (MDI) child windows, resizable split pane controls, modal dialogs and balloon help windows.</span></span>  
  
<a name="Implementation_Guidelines_and_Conventions"></a>

## <a name="implementation-guidelines-and-conventions"></a><span data-ttu-id="cd203-111">Wytyczne i konwencje dotyczące implementacji</span><span class="sxs-lookup"><span data-stu-id="cd203-111">Implementation Guidelines and Conventions</span></span>  

 <span data-ttu-id="cd203-112">Podczas implementowania wzorca kontroli okna należy zwrócić uwagę na następujące wytyczne i konwencje:</span><span class="sxs-lookup"><span data-stu-id="cd203-112">When implementing the Window control pattern, note the following guidelines and conventions:</span></span>  
  
- <span data-ttu-id="cd203-113">Aby zapewnić możliwość modyfikowania rozmiaru okna i położenia ekranu przy użyciu automatyzacji interfejsu użytkownika, formant musi <xref:System.Windows.Automation.Provider.ITransformProvider> być zaimplementowany dodatkowo do <xref:System.Windows.Automation.Provider.IWindowProvider> .</span><span class="sxs-lookup"><span data-stu-id="cd203-113">To support the ability to modify both window size and screen position using UI Automation, a control must implement <xref:System.Windows.Automation.Provider.ITransformProvider> in addition to <xref:System.Windows.Automation.Provider.IWindowProvider>.</span></span>  
  
- <span data-ttu-id="cd203-114">Formanty, które zawierają paski tytułu i elementy paska tytułu, które umożliwiają przenoszenie formantu, jego rozmiar, zmaksymalizowany, zminimalizowany lub zamknięty są zwykle wymagane do wdrożenia <xref:System.Windows.Automation.Provider.IWindowProvider> .</span><span class="sxs-lookup"><span data-stu-id="cd203-114">Controls that contain title bars and title bar elements that enable the control to be moved, resized, maximized, minimized, or closed are typically required to implement <xref:System.Windows.Automation.Provider.IWindowProvider>.</span></span>  
  
- <span data-ttu-id="cd203-115">Kontrolki, takie jak okienka wyskakujące etykietki narzędzi i pola kombi lub menu rozwijane, zazwyczaj nie są implementowane <xref:System.Windows.Automation.Provider.IWindowProvider> .</span><span class="sxs-lookup"><span data-stu-id="cd203-115">Controls such as tooltip pop-ups and combo box or menu drop-downs do not typically implement <xref:System.Windows.Automation.Provider.IWindowProvider>.</span></span>  
  
- <span data-ttu-id="cd203-116">Okna pomocy w dymkach są odróżniane od podstawowych wyskakujących etykietek narzędzi przez udostępnienie przycisku Zamknij podobne do okna.</span><span class="sxs-lookup"><span data-stu-id="cd203-116">Balloon help windows are differentiated from basic tooltip pop-ups by the provision of a window-like Close button.</span></span>  
  
- <span data-ttu-id="cd203-117">Tryb pełnoekranowy nie jest obsługiwany przez program IWindowProvider, ponieważ jest on specyficzny dla aplikacji i nie jest typowym zachowaniem okna.</span><span class="sxs-lookup"><span data-stu-id="cd203-117">Full-screen mode is not supported by IWindowProvider as it is feature-specific to an application and is not typical window behavior.</span></span>  
  
<a name="Required_Members_for_IWindowProvider"></a>

## <a name="required-members-for-iwindowprovider"></a><span data-ttu-id="cd203-118">Wymagane elementy członkowskie dla IWindowProvider</span><span class="sxs-lookup"><span data-stu-id="cd203-118">Required Members for IWindowProvider</span></span>  

 <span data-ttu-id="cd203-119">Dla interfejsu IWindowProvider są wymagane następujące właściwości, metody i zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="cd203-119">The following properties, methods, and events are required for the IWindowProvider interface.</span></span>  
  
|<span data-ttu-id="cd203-120">Wymagany element członkowski</span><span class="sxs-lookup"><span data-stu-id="cd203-120">Required member</span></span>|<span data-ttu-id="cd203-121">Typ elementu członkowskiego</span><span class="sxs-lookup"><span data-stu-id="cd203-121">Member type</span></span>|<span data-ttu-id="cd203-122">Uwagi</span><span class="sxs-lookup"><span data-stu-id="cd203-122">Notes</span></span>|  
|---------------------|-----------------|-----------|  
|<xref:System.Windows.Automation.Provider.IWindowProvider.InteractionState%2A>|<span data-ttu-id="cd203-123">Właściwość</span><span class="sxs-lookup"><span data-stu-id="cd203-123">Property</span></span>|<span data-ttu-id="cd203-124">Brak</span><span class="sxs-lookup"><span data-stu-id="cd203-124">None</span></span>|  
|<xref:System.Windows.Automation.Provider.IWindowProvider.IsModal%2A>|<span data-ttu-id="cd203-125">Właściwość</span><span class="sxs-lookup"><span data-stu-id="cd203-125">Property</span></span>|<span data-ttu-id="cd203-126">Brak</span><span class="sxs-lookup"><span data-stu-id="cd203-126">None</span></span>|  
|<xref:System.Windows.Automation.Provider.IWindowProvider.IsTopmost%2A>|<span data-ttu-id="cd203-127">Właściwość</span><span class="sxs-lookup"><span data-stu-id="cd203-127">Property</span></span>|<span data-ttu-id="cd203-128">Brak</span><span class="sxs-lookup"><span data-stu-id="cd203-128">None</span></span>|  
|<xref:System.Windows.Automation.Provider.IWindowProvider.Maximizable%2A>|<span data-ttu-id="cd203-129">Właściwość</span><span class="sxs-lookup"><span data-stu-id="cd203-129">Property</span></span>|<span data-ttu-id="cd203-130">Brak</span><span class="sxs-lookup"><span data-stu-id="cd203-130">None</span></span>|  
|<xref:System.Windows.Automation.Provider.IWindowProvider.Minimizable%2A>|<span data-ttu-id="cd203-131">Właściwość</span><span class="sxs-lookup"><span data-stu-id="cd203-131">Property</span></span>|<span data-ttu-id="cd203-132">Brak</span><span class="sxs-lookup"><span data-stu-id="cd203-132">None</span></span>|  
|<xref:System.Windows.Automation.Provider.IWindowProvider.VisualState%2A>|<span data-ttu-id="cd203-133">Właściwość</span><span class="sxs-lookup"><span data-stu-id="cd203-133">Property</span></span>|<span data-ttu-id="cd203-134">Brak</span><span class="sxs-lookup"><span data-stu-id="cd203-134">None</span></span>|  
|<xref:System.Windows.Automation.Provider.IWindowProvider.Close%2A>|<span data-ttu-id="cd203-135">Metoda</span><span class="sxs-lookup"><span data-stu-id="cd203-135">Method</span></span>|<span data-ttu-id="cd203-136">Brak</span><span class="sxs-lookup"><span data-stu-id="cd203-136">None</span></span>|  
|<xref:System.Windows.Automation.Provider.IWindowProvider.SetVisualState%2A>|<span data-ttu-id="cd203-137">Metoda</span><span class="sxs-lookup"><span data-stu-id="cd203-137">Method</span></span>|<span data-ttu-id="cd203-138">Brak</span><span class="sxs-lookup"><span data-stu-id="cd203-138">None</span></span>|  
|<xref:System.Windows.Automation.Provider.IWindowProvider.WaitForInputIdle%2A>|<span data-ttu-id="cd203-139">Metoda</span><span class="sxs-lookup"><span data-stu-id="cd203-139">Method</span></span>|<span data-ttu-id="cd203-140">Brak</span><span class="sxs-lookup"><span data-stu-id="cd203-140">None</span></span>|  
|<xref:System.Windows.Automation.WindowPattern.WindowClosedEvent>|<span data-ttu-id="cd203-141">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="cd203-141">Event</span></span>|<span data-ttu-id="cd203-142">Brak</span><span class="sxs-lookup"><span data-stu-id="cd203-142">None</span></span>|  
|<xref:System.Windows.Automation.WindowPattern.WindowOpenedEvent>|<span data-ttu-id="cd203-143">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="cd203-143">Event</span></span>|<span data-ttu-id="cd203-144">Brak</span><span class="sxs-lookup"><span data-stu-id="cd203-144">None</span></span>|  
|<xref:System.Windows.Automation.WindowInteractionState>|<span data-ttu-id="cd203-145">Zdarzenie</span><span class="sxs-lookup"><span data-stu-id="cd203-145">Event</span></span>|<span data-ttu-id="cd203-146">Nie ma gwarancji <xref:System.Windows.Automation.WindowInteractionState.ReadyForUserInteraction></span><span class="sxs-lookup"><span data-stu-id="cd203-146">Is not guaranteed to be <xref:System.Windows.Automation.WindowInteractionState.ReadyForUserInteraction></span></span>|  
  
<a name="Exceptions"></a>

## <a name="exceptions"></a><span data-ttu-id="cd203-147">Wyjątki</span><span class="sxs-lookup"><span data-stu-id="cd203-147">Exceptions</span></span>  

 <span data-ttu-id="cd203-148">Dostawcy muszą zgłosić następujące wyjątki.</span><span class="sxs-lookup"><span data-stu-id="cd203-148">Providers must throw the following exceptions.</span></span>  
  
|<span data-ttu-id="cd203-149">Typ wyjątku</span><span class="sxs-lookup"><span data-stu-id="cd203-149">Exception type</span></span>|<span data-ttu-id="cd203-150">Warunek</span><span class="sxs-lookup"><span data-stu-id="cd203-150">Condition</span></span>|  
|--------------------|---------------|  
|<xref:System.InvalidOperationException>|<xref:System.Windows.Automation.Provider.IWindowProvider.SetVisualState%2A><br /><br /> <span data-ttu-id="cd203-151">— Gdy kontrolka nie obsługuje żądanego zachowania.</span><span class="sxs-lookup"><span data-stu-id="cd203-151">-   When a control does not support a requested behavior.</span></span>|  
|<xref:System.ArgumentOutOfRangeException>|<xref:System.Windows.Automation.Provider.IWindowProvider.WaitForInputIdle%2A><br /><br /> <span data-ttu-id="cd203-152">-Jeśli parametr nie jest prawidłową liczbą.</span><span class="sxs-lookup"><span data-stu-id="cd203-152">-   When the parameter is not a valid number.</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="cd203-153">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="cd203-153">See also</span></span>

- [<span data-ttu-id="cd203-154">Wzorce formantów automatyzacji interfejsu użytkownika — omówienie</span><span class="sxs-lookup"><span data-stu-id="cd203-154">UI Automation Control Patterns Overview</span></span>](ui-automation-control-patterns-overview.md)
- [<span data-ttu-id="cd203-155">Obsługa wzorców formantów dostawcy automatyzacji interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="cd203-155">Support Control Patterns in a UI Automation Provider</span></span>](support-control-patterns-in-a-ui-automation-provider.md)
- [<span data-ttu-id="cd203-156">Wzorce kontrolek automatyzacji interfejsu użytkownika dla klientów</span><span class="sxs-lookup"><span data-stu-id="cd203-156">UI Automation Control Patterns for Clients</span></span>](ui-automation-control-patterns-for-clients.md)
- [<span data-ttu-id="cd203-157">Przegląd drzewa automatyzacji interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="cd203-157">UI Automation Tree Overview</span></span>](ui-automation-tree-overview.md)
- [<span data-ttu-id="cd203-158">Używanie buforowania w automatyzacji interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="cd203-158">Use Caching in UI Automation</span></span>](use-caching-in-ui-automation.md)
