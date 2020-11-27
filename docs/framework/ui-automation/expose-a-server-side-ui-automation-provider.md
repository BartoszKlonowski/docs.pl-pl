---
title: Udostępnianie dostawcy automatyzacji interfejsu użytkownika po stronie serwera
description: Wyświetl przykład pokazujący, jak uwidocznić dostawcę automatyzacji interfejsu użytkownika po stronie serwera, który jest hostowany w oknie System. Windows. Forms. Control.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- expose a server-side UI Automation provider
- UI Automation, server-side provider, exposing
- server-side UI Automation provider, exposing
ms.assetid: 55d419c0-2201-4101-90c9-2888df4dbb47
ms.openlocfilehash: be39130c7a91fc081256bf14a87f503d27f45129
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96276532"
---
# <a name="expose-a-server-side-ui-automation-provider"></a><span data-ttu-id="45146-103">Udostępnianie dostawcy automatyzacji interfejsu użytkownika po stronie serwera</span><span class="sxs-lookup"><span data-stu-id="45146-103">Expose a Server-side UI Automation Provider</span></span>

> [!NOTE]
> <span data-ttu-id="45146-104">Ta dokumentacja jest przeznaczona dla .NET Framework deweloperów, którzy chcą korzystać z zarządzanych [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] klas zdefiniowanych w <xref:System.Windows.Automation> przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="45146-104">This documentation is intended for .NET Framework developers who want to use the managed [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] classes defined in the <xref:System.Windows.Automation> namespace.</span></span> <span data-ttu-id="45146-105">Aby uzyskać najnowsze informacje na temat [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] , zobacz [interfejs API usługi Windows Automation: Automatyzacja interfejsu użytkownika](/windows/win32/winauto/entry-uiauto-win32).</span><span class="sxs-lookup"><span data-stu-id="45146-105">For the latest information about [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], see [Windows Automation API: UI Automation](/windows/win32/winauto/entry-uiauto-win32).</span></span>  
  
 <span data-ttu-id="45146-106">Ten temat zawiera przykładowy kod, który pokazuje, jak uwidocznić dostawcę automatyzacji interfejsu użytkownika po stronie serwera, który jest hostowany w <xref:System.Windows.Forms.Control?displayProperty=nameWithType> oknie.</span><span class="sxs-lookup"><span data-stu-id="45146-106">This topic contains example code that shows how to expose a server-side UI Automation provider that is hosted in a <xref:System.Windows.Forms.Control?displayProperty=nameWithType> window.</span></span>  
  
 <span data-ttu-id="45146-107">Przykład zastępuje procedurę okna WM_GETOBJECT, czyli komunikat wysyłany przez [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] usługę podstawową, gdy aplikacja kliencka zażąda informacji o oknie.</span><span class="sxs-lookup"><span data-stu-id="45146-107">The example overrides the window procedure to trap WM_GETOBJECT, which is the message sent by the [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] core service when a client application requests information about the window.</span></span>  
  
## <a name="example"></a><span data-ttu-id="45146-108">Przykład</span><span class="sxs-lookup"><span data-stu-id="45146-108">Example</span></span>  

 [!code-csharp[UIAFragmentProvider_snip#116](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAFragmentProvider_snip/CSharp/ListFragment.cs#116)]
 [!code-vb[UIAFragmentProvider_snip#116](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAFragmentProvider_snip/VisualBasic/ListFragment.vb#116)]  
  
## <a name="see-also"></a><span data-ttu-id="45146-109">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="45146-109">See also</span></span>

- [<span data-ttu-id="45146-110">Przegląd dostawców automatyzacji interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="45146-110">UI Automation Providers Overview</span></span>](ui-automation-providers-overview.md)
- [<span data-ttu-id="45146-111">Implementacja dostawcy automatyzacji interfejsu użytkownika po stronie serwera</span><span class="sxs-lookup"><span data-stu-id="45146-111">Server-Side UI Automation Provider Implementation</span></span>](server-side-ui-automation-provider-implementation.md)
