---
title: CoEEShutDownCOM — Funkcja
ms.date: 03/30/2017
api_name:
- CoEEShutDownCOM
api_location:
- mscoree.dll
- clr.dll
- mscorwks.dll
- mscoreei.dll
- mscorsvr.dll
api_type:
- DLLExport
f1_keywords:
- CoEEShutDownCOM
helpviewer_keywords:
- CoEEShutDownCOM function [.NET Framework hosting]
ms.assetid: b634cae2-632f-4737-9be4-92d0652844d7
topic_type:
- apiref
ms.openlocfilehash: 774704698f92d546d6bafa61c65d18d083c65f89
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95716762"
---
# <a name="coeeshutdowncom-function"></a><span data-ttu-id="9659b-102">CoEEShutDownCOM — Funkcja</span><span class="sxs-lookup"><span data-stu-id="9659b-102">CoEEShutDownCOM Function</span></span>

<span data-ttu-id="9659b-103">Wymusza, aby środowisko uruchomieniowe języka wspólnego (CLR) zwolnił wszystkie wskaźniki interfejsu, które znajdują się wewnątrz wywoływanych otok (RCW) środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="9659b-103">Forces the common language runtime (CLR) to release all interface pointers it holds inside runtime callable wrappers (RCW).</span></span> <span data-ttu-id="9659b-104">Ma to wpływ na zwalnianie wszystkich pamięci podręcznych OTOKi.</span><span class="sxs-lookup"><span data-stu-id="9659b-104">This has the effect of releasing all RCW caches.</span></span> <span data-ttu-id="9659b-105">Ta funkcja globalna jest przestarzała w .NET Framework 4.</span><span class="sxs-lookup"><span data-stu-id="9659b-105">This global function is deprecated in the .NET Framework 4.</span></span> <span data-ttu-id="9659b-106">Zamiast tego należy użyć punktu wejścia dla określonego środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="9659b-106">Instead, use the entry point for a specific runtime.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="9659b-107">Składnia</span><span class="sxs-lookup"><span data-stu-id="9659b-107">Syntax</span></span>  
  
```cpp  
void CoEEShutDownCOM ();  
```  
  
## <a name="remarks"></a><span data-ttu-id="9659b-108">Uwagi</span><span class="sxs-lookup"><span data-stu-id="9659b-108">Remarks</span></span>  

 <span data-ttu-id="9659b-109">`CoEEShutDownCOM`Funkcja najpierw zwalnia wszystkie RCW we wszystkich kontekstach i we wszystkich pamięciach podręcznych, a następnie usuwa wszelkie powiadomienia o rozrywaniu istniejące w instalatorze.</span><span class="sxs-lookup"><span data-stu-id="9659b-109">The `CoEEShutDownCOM` function first releases all the RCWs in all contexts and in all caches, and then removes any tear-down notification existing in setup.</span></span> <span data-ttu-id="9659b-110">Brak wyładowywania biblioteki DLL.</span><span class="sxs-lookup"><span data-stu-id="9659b-110">No DLL unloading occurs.</span></span>  
  
> [!CAUTION]
> <span data-ttu-id="9659b-111">Ta funkcja ma wpływ na wszystkie środowiska uruchomieniowe, które są ładowane do procesu.</span><span class="sxs-lookup"><span data-stu-id="9659b-111">This function affects all runtimes that are loaded into the process.</span></span>  
  
 <span data-ttu-id="9659b-112">Począwszy od .NET Framework 4, wywołaj punkt wejścia dla tej funkcji w konkretnym środowisku uruchomieniowym, którego chcesz dotyczyć.</span><span class="sxs-lookup"><span data-stu-id="9659b-112">Beginning with the .NET Framework 4, call the entry point for this function on the specific runtime you want to affect.</span></span> <span data-ttu-id="9659b-113">Aby uzyskać punkt wejścia, wywołaj metodę [ICLRRuntimeInfo:: GetProcAddress](iclrruntimeinfo-getprocaddress-method.md) i określ wartość "CoEEShutDownCOM —".</span><span class="sxs-lookup"><span data-stu-id="9659b-113">To get the entry point, call the [ICLRRuntimeInfo::GetProcAddress](iclrruntimeinfo-getprocaddress-method.md) method and specify "CoEEShutDownCOM".</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="9659b-114">Wymagania</span><span class="sxs-lookup"><span data-stu-id="9659b-114">Requirements</span></span>  

 <span data-ttu-id="9659b-115">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="9659b-115">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="9659b-116">**Nagłówek:** Cor. h</span><span class="sxs-lookup"><span data-stu-id="9659b-116">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="9659b-117">**Biblioteka:** Uwzględnione jako zasób w MsCorEE.dll</span><span class="sxs-lookup"><span data-stu-id="9659b-117">**Library:** Included as a resource in MsCorEE.dll</span></span>  
  
 <span data-ttu-id="9659b-118">**.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="9659b-118">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="9659b-119">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="9659b-119">See also</span></span>

- [<span data-ttu-id="9659b-120">Statyczne funkcje globalne metadanych</span><span class="sxs-lookup"><span data-stu-id="9659b-120">Metadata Global Static Functions</span></span>](../metadata/metadata-global-static-functions.md)
