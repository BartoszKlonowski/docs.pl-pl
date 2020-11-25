---
title: EInitializeNewDomainFlags — Wyliczenie
ms.date: 03/30/2017
api_name:
- EInitializeNewDomainFlags
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- EInitializeNewDomainFlags
helpviewer_keywords:
- EInitializeNewDomainFlags enumeration [.NET Framework hosting]
ms.assetid: 3a120ab2-f5ef-4c9b-8595-d3ed7247c342
ms.openlocfilehash: 8350b507609e63c060cda08514200d386c37a6b3
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95724328"
---
# <a name="einitializenewdomainflags-enumeration"></a><span data-ttu-id="9847b-102">EInitializeNewDomainFlags — Wyliczenie</span><span class="sxs-lookup"><span data-stu-id="9847b-102">EInitializeNewDomainFlags Enumeration</span></span>

<span data-ttu-id="9847b-103">Umożliwia hostowi zapewnienie środowiska uruchomieniowego z informacjami o inicjalizacji domeny aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9847b-103">Enables the host to provide the runtime with information about the initialization of an application domain.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="9847b-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="9847b-104">Syntax</span></span>  
  
```cpp  
typedef enum {  
    eInitializeNewDomainFlags_None              = 0x0000,  
    eInitializeNewDomainFlags_NoSecurityChanges = 0x0002  
} EInitializeNewDomainFlags;  
```  
  
## <a name="members"></a><span data-ttu-id="9847b-105">Elementy członkowskie</span><span class="sxs-lookup"><span data-stu-id="9847b-105">Members</span></span>  
  
|<span data-ttu-id="9847b-106">Członek</span><span class="sxs-lookup"><span data-stu-id="9847b-106">Member</span></span>|<span data-ttu-id="9847b-107">Opis</span><span class="sxs-lookup"><span data-stu-id="9847b-107">Description</span></span>|  
|------------|-----------------|  
|`eInitializeNewDomainFlags_None`|<span data-ttu-id="9847b-108">Brak flag.</span><span class="sxs-lookup"><span data-stu-id="9847b-108">No flags.</span></span>|  
|`eInitializeNewDomainFlags_NoSecurityChanges`|<span data-ttu-id="9847b-109">Informuje środowisko uruchomieniowe języka wspólnego (CLR), że host nie wprowadzi zmian w stanie zabezpieczeń domeny aplikacji w <xref:System.AppDomainManager.InitializeNewDomain%2A> metodzie.</span><span class="sxs-lookup"><span data-stu-id="9847b-109">Informs the common language runtime (CLR) that the host will not make changes to the security state of the application domain in the <xref:System.AppDomainManager.InitializeNewDomain%2A> method.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="9847b-110">Uwagi</span><span class="sxs-lookup"><span data-stu-id="9847b-110">Remarks</span></span>  

 <span data-ttu-id="9847b-111">Metoda [ICLRDomainManager:: SetAppDomainManagerType —](iclrdomainmanager-setappdomainmanagertype-method.md) przyjmuje parametr typu `EInitializeNewDomainFlags` .</span><span class="sxs-lookup"><span data-stu-id="9847b-111">The [ICLRDomainManager::SetAppDomainManagerType](iclrdomainmanager-setappdomainmanagertype-method.md) method takes a parameter of type `EInitializeNewDomainFlags`.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="9847b-112">Wymagania</span><span class="sxs-lookup"><span data-stu-id="9847b-112">Requirements</span></span>  

 <span data-ttu-id="9847b-113">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="9847b-113">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="9847b-114">**Nagłówek:** MSCorEE. h</span><span class="sxs-lookup"><span data-stu-id="9847b-114">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="9847b-115">**Biblioteka:** MSCorEE.dll</span><span class="sxs-lookup"><span data-stu-id="9847b-115">**Library:** MSCorEE.dll</span></span>  
  
 <span data-ttu-id="9847b-116">**.NET Framework wersje:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="9847b-116">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="9847b-117">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="9847b-117">See also</span></span>

- [<span data-ttu-id="9847b-118">Hosting — Wyliczenia</span><span class="sxs-lookup"><span data-stu-id="9847b-118">Hosting Enumerations</span></span>](hosting-enumerations.md)
- [<span data-ttu-id="9847b-119">SetAppDomainManagerType — Metoda</span><span class="sxs-lookup"><span data-stu-id="9847b-119">SetAppDomainManagerType Method</span></span>](iclrdomainmanager-setappdomainmanagertype-method.md)
