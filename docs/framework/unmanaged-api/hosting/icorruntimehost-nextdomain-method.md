---
title: ICorRuntimeHost::NextDomain — Metoda
ms.date: 03/30/2017
api_name:
- ICorRuntimeHost.NextDomain
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICorRuntimeHost::NextDomain
helpviewer_keywords:
- ICorRuntimeHost::NextDomain method [.NET Framework hosting]
- NextDomain method [.NET Framework hosting]
ms.assetid: fe07a05b-f6d6-44b5-ab01-b9a6eb15c350
topic_type:
- apiref
ms.openlocfilehash: 598c46d50d7b4a67c1b2c0d844c9b12deb12a428
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95671372"
---
# <a name="icorruntimehostnextdomain-method"></a><span data-ttu-id="15b3e-102">ICorRuntimeHost::NextDomain — Metoda</span><span class="sxs-lookup"><span data-stu-id="15b3e-102">ICorRuntimeHost::NextDomain Method</span></span>

<span data-ttu-id="15b3e-103">Pobiera wskaźnik interfejsu do następnej domeny w wyliczeniu.</span><span class="sxs-lookup"><span data-stu-id="15b3e-103">Gets an interface pointer to the next domain in the enumeration.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="15b3e-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="15b3e-104">Syntax</span></span>  
  
```cpp  
HRESULT NextDomain (  
    [in] HCORENUM hEnum,  
    [out] void** pAppDomain  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="15b3e-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="15b3e-105">Parameters</span></span>  

 `hEnum`  
 <span data-ttu-id="15b3e-106">podczas Moduł wyliczający uzyskany za pomocą wywołania do [EnumDomains —](icorruntimehost-enumdomains-method.md).</span><span class="sxs-lookup"><span data-stu-id="15b3e-106">[in] The enumerator that was obtained through a call to [EnumDomains](icorruntimehost-enumdomains-method.md).</span></span>  
  
 `pAppDomain`  
 <span data-ttu-id="15b3e-107">określoną Wskaźnik interfejsu do <xref:System._AppDomain?displayProperty=nameWithType> typu, który reprezentuje następną domenę w wyliczeniu lub wartość null, jeśli nie ma więcej domen.</span><span class="sxs-lookup"><span data-stu-id="15b3e-107">[out] An interface pointer to the <xref:System._AppDomain?displayProperty=nameWithType> type that represents the next domain in the enumeration, or null, if no more domains exist.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="15b3e-108">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="15b3e-108">Return Value</span></span>  
  
|<span data-ttu-id="15b3e-109">HRESULT</span><span class="sxs-lookup"><span data-stu-id="15b3e-109">HRESULT</span></span>|<span data-ttu-id="15b3e-110">Opis</span><span class="sxs-lookup"><span data-stu-id="15b3e-110">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="15b3e-111">S_OK</span><span class="sxs-lookup"><span data-stu-id="15b3e-111">S_OK</span></span>|<span data-ttu-id="15b3e-112">Operacja zakończyła się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="15b3e-112">The operation was successful.</span></span>|  
|<span data-ttu-id="15b3e-113">S_FALSE</span><span class="sxs-lookup"><span data-stu-id="15b3e-113">S_FALSE</span></span>|<span data-ttu-id="15b3e-114">Nie można ukończyć operacji lub w wyliczeniu nie ma więcej domen.</span><span class="sxs-lookup"><span data-stu-id="15b3e-114">The operation failed to complete, or there are no more domains in the enumeration.</span></span>|  
|<span data-ttu-id="15b3e-115">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="15b3e-115">E_FAIL</span></span>|<span data-ttu-id="15b3e-116">Wystąpił nieznany, Katastrofalny błąd.</span><span class="sxs-lookup"><span data-stu-id="15b3e-116">An unknown, catastrophic failure occurred.</span></span> <span data-ttu-id="15b3e-117">Jeśli metoda zwraca E_FAIL, środowisko uruchomieniowe języka wspólnego (CLR) nie jest już możliwe do użycia w procesie.</span><span class="sxs-lookup"><span data-stu-id="15b3e-117">If a method returns E_FAIL, the common language runtime (CLR) is no longer usable in the process.</span></span> <span data-ttu-id="15b3e-118">Kolejne wywołania interfejsów API hostingu zwracają HOST_E_CLRNOTAVAILABLE.</span><span class="sxs-lookup"><span data-stu-id="15b3e-118">Subsequent calls to any hosting APIs return HOST_E_CLRNOTAVAILABLE.</span></span>|  
|<span data-ttu-id="15b3e-119">HOST_E_CLRNOTAVAILABLE</span><span class="sxs-lookup"><span data-stu-id="15b3e-119">HOST_E_CLRNOTAVAILABLE</span></span>|<span data-ttu-id="15b3e-120">Środowisko CLR nie zostało załadowane do procesu lub środowisko CLR znajduje się w stanie, w którym nie można uruchomić kodu zarządzanego lub przetworzyć wywołania pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="15b3e-120">The CLR has not been loaded into a process, or the CLR is in a state in which it cannot run managed code or process the call successfully.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="15b3e-121">Wymagania</span><span class="sxs-lookup"><span data-stu-id="15b3e-121">Requirements</span></span>  

 <span data-ttu-id="15b3e-122">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="15b3e-122">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="15b3e-123">**Nagłówek:** MSCorEE. h</span><span class="sxs-lookup"><span data-stu-id="15b3e-123">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="15b3e-124">**Biblioteka:** Uwzględnione jako zasób w MSCorEE.dll</span><span class="sxs-lookup"><span data-stu-id="15b3e-124">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="15b3e-125">**.NET Framework wersje:** 1,0, 1,1</span><span class="sxs-lookup"><span data-stu-id="15b3e-125">**.NET Framework Versions:** 1.0, 1.1</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="15b3e-126">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="15b3e-126">See also</span></span>

- <xref:System._AppDomain>
- <xref:System.AppDomain>
- [<span data-ttu-id="15b3e-127">ICorRuntimeHost — Interfejs</span><span class="sxs-lookup"><span data-stu-id="15b3e-127">ICorRuntimeHost Interface</span></span>](icorruntimehost-interface.md)
