---
title: failedQI MDA
description: Zapoznaj się z asystentem debugowania zarządzanego w programie failedQI (MDA) w programie .NET, który może zostać aktywowany w przypadku niepowodzenia rzutowania lub wywołania modelu COM z otoki wywołującej (RCW) środowiska uruchomieniowego.
ms.date: 03/30/2017
helpviewer_keywords:
- failed QueryInterface
- FailedQI MDA
- QueryInterface call failures
- MDAs (managed debugging assistants), failed QueryInterface
- managed debugging assistants (MDAs), failed QueryInterface
ms.assetid: 902dc863-34b3-477c-b433-b8a6bb6133c6
ms.openlocfilehash: bbd8d5644f8620444d80845b9920b925b6891176
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96244330"
---
# <a name="failedqi-mda"></a><span data-ttu-id="d62a8-103">failedQI MDA</span><span class="sxs-lookup"><span data-stu-id="d62a8-103">failedQI MDA</span></span>

<span data-ttu-id="d62a8-104">`failedQI`Asystent debugowania zarządzanego (MDA) jest uaktywniany, gdy środowisko uruchomieniowe wywołuje `QueryInterface` wskaźnik interfejsu com w imieniu otoki (RCW) środowiska uruchomieniowego, a `QueryInterface` wywołanie kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="d62a8-104">The `failedQI` managed debugging assistant (MDA) is activated when the runtime calls `QueryInterface` on a COM interface pointer on behalf of a runtime callable wrapper (RCW), and the `QueryInterface` call fails.</span></span>  
  
## <a name="symptoms"></a><span data-ttu-id="d62a8-105">Objawy</span><span class="sxs-lookup"><span data-stu-id="d62a8-105">Symptoms</span></span>  

 <span data-ttu-id="d62a8-106">Rzutowanie otoki RCW kończy się niepowodzeniem lub wywołanie modelu COM z otoki RCW nieoczekiwanie zakończyło się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="d62a8-106">A cast on an RCW fails, or a call to COM from an RCW fails unexpectedly.</span></span>  
  
## <a name="cause"></a><span data-ttu-id="d62a8-107">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="d62a8-107">Cause</span></span>  
  
- <span data-ttu-id="d62a8-108">Wywołanie zostało wykonane z niewłaściwego kontekstu.</span><span class="sxs-lookup"><span data-stu-id="d62a8-108">The call is made from the wrong context.</span></span>  
  
- <span data-ttu-id="d62a8-109">Zarejestrowanego serwera proxy nie powiodło się, `QueryInterface` ponieważ wywołanie było podejmowane w nieprawidłowym kontekście.</span><span class="sxs-lookup"><span data-stu-id="d62a8-109">The registered proxy is failing the `QueryInterface` call because the call was attempted in the wrong context.</span></span>  
  
- <span data-ttu-id="d62a8-110">Serwer proxy należący do OLE zwrócił błąd HRESULT.</span><span class="sxs-lookup"><span data-stu-id="d62a8-110">An OLE-owned proxy returned a failure HRESULT.</span></span>  
  
## <a name="resolution"></a><span data-ttu-id="d62a8-111">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="d62a8-111">Resolution</span></span>  

 <span data-ttu-id="d62a8-112">Zapoznaj się z dokumentacją MSDN dotyczącą reguł COM.</span><span class="sxs-lookup"><span data-stu-id="d62a8-112">See the MSDN documentation on COM rules.</span></span>  
  
## <a name="effect-on-the-runtime"></a><span data-ttu-id="d62a8-113">Wpływ na środowisko uruchomieniowe</span><span class="sxs-lookup"><span data-stu-id="d62a8-113">Effect on the Runtime</span></span>  

 <span data-ttu-id="d62a8-114">Jeśli `QueryInterface` wywołanie zakończy się niepowodzeniem, kontekst jest przełączany, a `QueryInterface` wywołanie zostanie ponowione, aby sprawdzić, czy wystąpił błąd w nieprawidłowym kontekście.</span><span class="sxs-lookup"><span data-stu-id="d62a8-114">If a `QueryInterface` call fails, the context is switched and the `QueryInterface` call is attempted again to see if an incorrect context was at fault.</span></span>  
  
## <a name="output"></a><span data-ttu-id="d62a8-115">Dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="d62a8-115">Output</span></span>  

 <span data-ttu-id="d62a8-116">Zarządzana nazwa interfejsu, identyfikator GUID interfejsu i HRESULT błędu.</span><span class="sxs-lookup"><span data-stu-id="d62a8-116">The managed name of the interface, the GUID of the interface, and the HRESULT of the failure.</span></span>  
  
## <a name="configuration"></a><span data-ttu-id="d62a8-117">Konfigurowanie</span><span class="sxs-lookup"><span data-stu-id="d62a8-117">Configuration</span></span>  
  
```xml  
<mdaConfig>  
  <assistants>  
    <failedQI/>  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a><span data-ttu-id="d62a8-118">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="d62a8-118">See also</span></span>

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [<span data-ttu-id="d62a8-119">Diagnozowanie błędów przy użyciu asystentów zarządzanego debugowania</span><span class="sxs-lookup"><span data-stu-id="d62a8-119">Diagnosing Errors with Managed Debugging Assistants</span></span>](diagnosing-errors-with-managed-debugging-assistants.md)
- [<span data-ttu-id="d62a8-120">Organizowanie międzyoperacyjne</span><span class="sxs-lookup"><span data-stu-id="d62a8-120">Interop Marshaling</span></span>](../interop/interop-marshaling.md)
