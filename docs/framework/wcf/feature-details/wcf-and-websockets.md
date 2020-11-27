---
title: Program WCF i technologia WebSockets
ms.date: 03/30/2017
ms.assetid: 1e53b49e-022c-49c7-8984-4b21b53c05b3
ms.openlocfilehash: 2ee27eef015ee8c2fbee8360b444343a1c757097
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96281589"
---
# <a name="wcf-and-websockets"></a><span data-ttu-id="3ba42-102">Program WCF i technologia WebSockets</span><span class="sxs-lookup"><span data-stu-id="3ba42-102">WCF and WebSockets</span></span>

<span data-ttu-id="3ba42-103">.NET Framework 4,5 wprowadza obsługę obiektów WebSockets w Windows Communication Foundation.</span><span class="sxs-lookup"><span data-stu-id="3ba42-103">The .NET Framework 4.5 introduces support for WebSockets in Windows Communication Foundation.</span></span>  <span data-ttu-id="3ba42-104">Obiekty WebSockets to wydajna technologia oparta na standardach, która umożliwia komunikację dwukierunkową za pośrednictwem standardowych portów HTTP 80 i 443.</span><span class="sxs-lookup"><span data-stu-id="3ba42-104">WebSockets is an efficient, standards-based technology that enables bidirectional communication over the standard HTTP ports 80 and 443.</span></span> <span data-ttu-id="3ba42-105">Użycie standardowych portów HTTP umożliwia komunikację między składnikami sieci Web za pośrednictwem pośredników.</span><span class="sxs-lookup"><span data-stu-id="3ba42-105">The use of the standard HTTP ports allow WebSockets to communicate across the web through intermediaries.</span></span>  <span data-ttu-id="3ba42-106">Dodano dwa nowe powiązania standardowe do obsługi komunikacji przy użyciu protokołu WebSocket.</span><span class="sxs-lookup"><span data-stu-id="3ba42-106">Two new standard bindings have been added to support communication over a WebSocket transport.</span></span> <span data-ttu-id="3ba42-107"><xref:System.ServiceModel.NetHttpBinding> i <xref:System.ServiceModel.NetHttpsBinding> .</span><span class="sxs-lookup"><span data-stu-id="3ba42-107"><xref:System.ServiceModel.NetHttpBinding> and <xref:System.ServiceModel.NetHttpsBinding>.</span></span> <span data-ttu-id="3ba42-108">Ustawienia specyficzne dla obiektów WebSockets można skonfigurować w <xref:System.ServiceModel.Channels.HttpTransportBindingElement> programie, uzyskując dostęp do <xref:System.ServiceModel.Channels.HttpTransportBindingElement.WebSocketSettings%2A> właściwości.</span><span class="sxs-lookup"><span data-stu-id="3ba42-108">WebSockets-specific settings can be configured on the <xref:System.ServiceModel.Channels.HttpTransportBindingElement> by accessing the <xref:System.ServiceModel.Channels.HttpTransportBindingElement.WebSocketSettings%2A> property.</span></span>
  
## <a name="in-this-section"></a><span data-ttu-id="3ba42-109">W tej sekcji</span><span class="sxs-lookup"><span data-stu-id="3ba42-109">In This Section</span></span>  

 [<span data-ttu-id="3ba42-110">Używanie elementu NetHttpBinding</span><span class="sxs-lookup"><span data-stu-id="3ba42-110">Using the NetHttpBinding</span></span>](using-the-nethttpbinding.md)  
 <span data-ttu-id="3ba42-111">W tym artykule omówiono <xref:System.ServiceModel.NetHttpBinding> i sposób konfigurowania tego programu.</span><span class="sxs-lookup"><span data-stu-id="3ba42-111">Discusses the <xref:System.ServiceModel.NetHttpBinding> and how to configure it.</span></span>  
  
 [<span data-ttu-id="3ba42-112">Instrukcje: tworzenie usługi WCF komunikującej się przez protokół WebSockets</span><span class="sxs-lookup"><span data-stu-id="3ba42-112">How to: Create a WCF Service that Communicates over WebSockets</span></span>](how-to-create-a-wcf-service-that-communicates-over-websockets.md)  
 <span data-ttu-id="3ba42-113">Opisuje sposób tworzenia usługi WCF, która komunikuje się za pośrednictwem obiektów WebSockets.</span><span class="sxs-lookup"><span data-stu-id="3ba42-113">Describes how to create a WCF service that communicates over Websockets.</span></span>  
  
## <a name="reference"></a><span data-ttu-id="3ba42-114">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="3ba42-114">Reference</span></span>  
  
## <a name="related-sections"></a><span data-ttu-id="3ba42-115">Sekcje pokrewne</span><span class="sxs-lookup"><span data-stu-id="3ba42-115">Related Sections</span></span>
