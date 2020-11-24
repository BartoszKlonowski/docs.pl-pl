---
title: Przestarzałe klasy coclass i interfejsy hostingu środowiska CLR
ms.date: 03/30/2017
helpviewer_keywords:
- interfaces [.NET Framework hosting], version 1
- .NET Framework 1.1, hosting interfaces
- hosting interfaces [.NET Framework], version 1
- .NET Framework 1.0, hosting interfaces
ms.assetid: 7b3d2755-cbab-4160-bc69-eb85791e38c7
ms.openlocfilehash: 8b90a33e2a0e6780a2ce908ff7ab251e94fbce90
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95673101"
---
# <a name="deprecated-clr-hosting-interfaces-and-coclasses"></a><span data-ttu-id="822ed-102">Przestarzałe klasy coclass i interfejsy hostingu środowiska CLR</span><span class="sxs-lookup"><span data-stu-id="822ed-102">Deprecated CLR Hosting Interfaces and Coclasses</span></span>

<span data-ttu-id="822ed-103">W tej sekcji opisano interfejsy, które mogą być używane przez niezarządzane hosty do integrowania środowiska uruchomieniowego języka wspólnego (CLR) w .NET Framework wersje 1,0 i 1,1 w aplikacjach.</span><span class="sxs-lookup"><span data-stu-id="822ed-103">This section describes the interfaces that unmanaged hosts can use to integrate the common language runtime (CLR) in the .NET Framework versions 1.0 and 1.1 into their applications.</span></span> <span data-ttu-id="822ed-104">Te interfejsy zapewniają metody hosta do konfigurowania i ładowania środowiska uruchomieniowego do procesu.</span><span class="sxs-lookup"><span data-stu-id="822ed-104">These interfaces provide methods for a host to configure and load the runtime into a process.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="822ed-105">W tej sekcji</span><span class="sxs-lookup"><span data-stu-id="822ed-105">In This Section</span></span>  

 <span data-ttu-id="822ed-106">IAppDomainSetup —</span><span class="sxs-lookup"><span data-stu-id="822ed-106">IAppDomainSetup</span></span>  
 <span data-ttu-id="822ed-107">Dostarcza metody dla hosta do konfigurowania <xref:System.AppDomain> .</span><span class="sxs-lookup"><span data-stu-id="822ed-107">Provides methods for the host to configure an <xref:System.AppDomain>.</span></span>  
  
 [<span data-ttu-id="822ed-108">ICeeFileGen — Klasa</span><span class="sxs-lookup"><span data-stu-id="822ed-108">ICeeFileGen Class</span></span>](iceefilegen-class.md)  
 <span data-ttu-id="822ed-109">Przestarzałe Oferuje funkcje tworzenia natywnego przenośnego pliku wykonywalnego (PE).</span><span class="sxs-lookup"><span data-stu-id="822ed-109">(Deprecated) Provides functionality for creating a native portable executable (PE) file.</span></span>  
  
 [<span data-ttu-id="822ed-110">ICorRuntimeHost — Interfejs</span><span class="sxs-lookup"><span data-stu-id="822ed-110">ICorRuntimeHost Interface</span></span>](icorruntimehost-interface.md)  
 <span data-ttu-id="822ed-111">Zapewnia metody dla hosta do konfigurowania ustawień środowiska CLR.</span><span class="sxs-lookup"><span data-stu-id="822ed-111">Provides methods for the host to configure CLR settings.</span></span>  
  
## <a name="related-sections"></a><span data-ttu-id="822ed-112">Sekcje pokrewne</span><span class="sxs-lookup"><span data-stu-id="822ed-112">Related Sections</span></span>  

 [<span data-ttu-id="822ed-113">Interfejsy hostingu środowiska CLR</span><span class="sxs-lookup"><span data-stu-id="822ed-113">CLR Hosting Interfaces</span></span>](clr-hosting-interfaces.md)  
 <span data-ttu-id="822ed-114">Zawiera tematy opisujące Interfejsy hostingu udostępniane w .NET Framework w wersji 2,0 i nowszych.</span><span class="sxs-lookup"><span data-stu-id="822ed-114">Contains topics that describe the hosting interfaces provided with the .NET Framework version 2.0 and later versions.</span></span>
