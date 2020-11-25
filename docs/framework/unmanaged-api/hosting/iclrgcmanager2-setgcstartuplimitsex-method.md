---
title: ICLRGCManager2::SetGCStartupLimitsEx — Metoda
ms.date: 03/30/2017
api_name:
- ICLRGCManager2.SetGCStartupLimitsEx
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRGCManager2::SetCLRGCStartupLimitsEx
helpviewer_keywords:
- ICLRGCManager2::SetGCStartupLimitsEx method [.NET Framework hosting]
- SetGCStartupLimitsEx method, ICLRGCManager2 interface [.NET Framework hosting]
ms.assetid: 6c3a08a9-5d65-48d4-8bbf-2a86ed7d356a
topic_type:
- apiref
ms.openlocfilehash: 27d1ce06800075d2690bc508554b70f8d10168af
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95715020"
---
# <a name="iclrgcmanager2setgcstartuplimitsex-method"></a><span data-ttu-id="9f730-102">ICLRGCManager2::SetGCStartupLimitsEx — Metoda</span><span class="sxs-lookup"><span data-stu-id="9f730-102">ICLRGCManager2::SetGCStartupLimitsEx Method</span></span>

<span data-ttu-id="9f730-103">Ustawia rozmiar segmentu wyrzucania elementów bezużytecznych i maksymalny rozmiar generacji 0 systemu odzyskiwania pamięci.</span><span class="sxs-lookup"><span data-stu-id="9f730-103">Sets the size of a garbage collection segment and the maximum size of the garbage collection system's generation 0.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="9f730-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="9f730-104">Syntax</span></span>  
  
```cpp  
HRESULT SetGCStartupLimitsEx (  
    [in] SIZE_T SegmentSize,
    [in] SIZE_T MaxGen0Size  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="9f730-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="9f730-105">Parameters</span></span>  

 `SegmentSize`  
 <span data-ttu-id="9f730-106">podczas Określony rozmiar segmentu odzyskiwania pamięci.</span><span class="sxs-lookup"><span data-stu-id="9f730-106">[in] The specified size of a garbage collection segment.</span></span>  
  
 <span data-ttu-id="9f730-107">Minimalny rozmiar segmentu to 4 MB.</span><span class="sxs-lookup"><span data-stu-id="9f730-107">The minimum segment size is 4 MB.</span></span> <span data-ttu-id="9f730-108">Segmenty można zwiększyć z przyrostem wynoszącym 1 MB lub większą.</span><span class="sxs-lookup"><span data-stu-id="9f730-108">Segments can be increased in increments of 1 MB or larger.</span></span>  
  
 `MaxGen0Size`  
 <span data-ttu-id="9f730-109">podczas Określony maksymalny rozmiar dla generacji 0.</span><span class="sxs-lookup"><span data-stu-id="9f730-109">[in] The specified maximum size for generation 0.</span></span>  
  
 <span data-ttu-id="9f730-110">Minimalna wielkość generacji 0 to 64 KB.</span><span class="sxs-lookup"><span data-stu-id="9f730-110">The minimum generation 0 size is 64 KB.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="9f730-111">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="9f730-111">Return Value</span></span>  
  
|<span data-ttu-id="9f730-112">HRESULT</span><span class="sxs-lookup"><span data-stu-id="9f730-112">HRESULT</span></span>|<span data-ttu-id="9f730-113">Opis</span><span class="sxs-lookup"><span data-stu-id="9f730-113">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="9f730-114">S_OK</span><span class="sxs-lookup"><span data-stu-id="9f730-114">S_OK</span></span>|<span data-ttu-id="9f730-115">`SetGCStartupLimitsEx` pomyślnie zwrócono.</span><span class="sxs-lookup"><span data-stu-id="9f730-115">`SetGCStartupLimitsEx` returned successfully.</span></span>|  
|<span data-ttu-id="9f730-116">HOST_E_CLRNOTAVAILABLE</span><span class="sxs-lookup"><span data-stu-id="9f730-116">HOST_E_CLRNOTAVAILABLE</span></span>|<span data-ttu-id="9f730-117">Środowisko uruchomieniowe języka wspólnego (CLR) nie zostało załadowane do procesu lub środowisko CLR znajduje się w stanie, w którym nie można uruchomić kodu zarządzanego lub przetworzyć wywołania pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="9f730-117">The common language runtime (CLR) has not been loaded into a process, or the CLR is in a state in which it cannot run managed code or process the call successfully.</span></span>|  
|<span data-ttu-id="9f730-118">HOST_E_TIMEOUT</span><span class="sxs-lookup"><span data-stu-id="9f730-118">HOST_E_TIMEOUT</span></span>|<span data-ttu-id="9f730-119">Upłynął limit czasu połączenia.</span><span class="sxs-lookup"><span data-stu-id="9f730-119">The call timed out.</span></span>|  
|<span data-ttu-id="9f730-120">HOST_E_NOT_OWNER</span><span class="sxs-lookup"><span data-stu-id="9f730-120">HOST_E_NOT_OWNER</span></span>|<span data-ttu-id="9f730-121">Obiekt wywołujący nie jest właocicielem blokady.</span><span class="sxs-lookup"><span data-stu-id="9f730-121">The caller does not own the lock.</span></span>|  
|<span data-ttu-id="9f730-122">HOST_E_ABANDONED</span><span class="sxs-lookup"><span data-stu-id="9f730-122">HOST_E_ABANDONED</span></span>|<span data-ttu-id="9f730-123">Zdarzenie zostało anulowane podczas oczekiwania na niego zablokowanego wątku lub włókna.</span><span class="sxs-lookup"><span data-stu-id="9f730-123">An event was canceled while a blocked thread or fiber was waiting on it.</span></span>|  
|<span data-ttu-id="9f730-124">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="9f730-124">E_FAIL</span></span>|<span data-ttu-id="9f730-125">Wystąpił nieznany błąd krytyczny.</span><span class="sxs-lookup"><span data-stu-id="9f730-125">An unknown catastrophic failure occurred.</span></span> <span data-ttu-id="9f730-126">Po powrocie metody E_FAIL nie będzie można używać środowiska CLR w procesie.</span><span class="sxs-lookup"><span data-stu-id="9f730-126">After a method returns E_FAIL, the CLR is no longer usable within the process.</span></span> <span data-ttu-id="9f730-127">Kolejne wywołania metod hostingu zwracają HOST_E_CLRNOTAVAILABLE.</span><span class="sxs-lookup"><span data-stu-id="9f730-127">Subsequent calls to hosting methods return HOST_E_CLRNOTAVAILABLE.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="9f730-128">Uwagi</span><span class="sxs-lookup"><span data-stu-id="9f730-128">Remarks</span></span>  

 <span data-ttu-id="9f730-129">Wartości, które `SetGCStartupLimitsEx` ustawia się, można określić tylko przed uruchomieniem hosta.</span><span class="sxs-lookup"><span data-stu-id="9f730-129">The values that `SetGCStartupLimitsEx` sets can be specified only before the host is started.</span></span> <span data-ttu-id="9f730-130">Późniejsze wywołania `SetGCStartupLimitsEx` są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="9f730-130">Later calls to `SetGCStartupLimitsEx` are ignored.</span></span>  
  
 <span data-ttu-id="9f730-131">Aby ustawić jeden z parametrów bez wpływu na pozostałe, określ wartość 0 (zero) dla parametru, którego nie chcesz zmienić.</span><span class="sxs-lookup"><span data-stu-id="9f730-131">To set either parameter without affecting the other, specify 0 (zero) for the parameter you don't want to change.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="9f730-132">Wymagania</span><span class="sxs-lookup"><span data-stu-id="9f730-132">Requirements</span></span>  

 <span data-ttu-id="9f730-133">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="9f730-133">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="9f730-134">**Nagłówek:** MSCorEE. h</span><span class="sxs-lookup"><span data-stu-id="9f730-134">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="9f730-135">**Biblioteka:** Uwzględnione jako zasób w MSCorEE.dll</span><span class="sxs-lookup"><span data-stu-id="9f730-135">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="9f730-136">**.NET Framework wersje:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="9f730-136">**.NET Framework Versions:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="9f730-137">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="9f730-137">See also</span></span>

- [<span data-ttu-id="9f730-138">Automatyczne zarządzanie pamięcią</span><span class="sxs-lookup"><span data-stu-id="9f730-138">Automatic Memory Management</span></span>](../../../standard/automatic-memory-management.md)
- [<span data-ttu-id="9f730-139">Odzyskiwanie pamięci</span><span class="sxs-lookup"><span data-stu-id="9f730-139">Garbage Collection</span></span>](../../../standard/garbage-collection/index.md)
- [<span data-ttu-id="9f730-140">ICLRControl — Interfejs</span><span class="sxs-lookup"><span data-stu-id="9f730-140">ICLRControl Interface</span></span>](iclrcontrol-interface.md)
- [<span data-ttu-id="9f730-141">ICLRGCManager2 — Interfejs</span><span class="sxs-lookup"><span data-stu-id="9f730-141">ICLRGCManager2 Interface</span></span>](iclrgcmanager2-interface.md)
