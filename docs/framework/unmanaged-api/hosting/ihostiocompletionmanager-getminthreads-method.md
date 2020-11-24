---
title: IHostIoCompletionManager::GetMinThreads — Metoda
ms.date: 03/30/2017
api_name:
- IHostIoCompletionManager.GetMinThreads
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostIoCompletionManager::GetMinThreads
helpviewer_keywords:
- GetMinThreads method, IHostIoCompletionManager interface [.NET Framework hosting]
- IHostIoCompletionManager::GetMinThreads method [.NET Framework hosting]
ms.assetid: d7a7f733-677d-481c-b3d5-444fcc502b8e
topic_type:
- apiref
ms.openlocfilehash: d321ce08edf4780fc5f26ac627849b9129c2f283
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95673231"
---
# <a name="ihostiocompletionmanagergetminthreads-method"></a><span data-ttu-id="79dd9-102">IHostIoCompletionManager::GetMinThreads — Metoda</span><span class="sxs-lookup"><span data-stu-id="79dd9-102">IHostIoCompletionManager::GetMinThreads Method</span></span>

<span data-ttu-id="79dd9-103">Pobiera minimalną liczbę wątków udostępnianych przez hosta na potrzeby przetwarzania żądań we/wy.</span><span class="sxs-lookup"><span data-stu-id="79dd9-103">Gets the minimum number of threads that the host provides for processing I/O requests.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="79dd9-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="79dd9-104">Syntax</span></span>  
  
```cpp  
HRESULT GetMinThreads (  
    [out] DWORD *pdwMinIOCompletionThreads  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="79dd9-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="79dd9-105">Parameters</span></span>  

 `pdwMinIOCompletionThreads`  
 <span data-ttu-id="79dd9-106">określoną Wskaźnik do minimalnej liczby wątków dostarczanych przez hosta w celu przetwarzania żądań we/wy.</span><span class="sxs-lookup"><span data-stu-id="79dd9-106">[out] A pointer to the minimum number of threads that the host provides to process I/O requests.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="79dd9-107">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="79dd9-107">Return Value</span></span>  
  
|<span data-ttu-id="79dd9-108">HRESULT</span><span class="sxs-lookup"><span data-stu-id="79dd9-108">HRESULT</span></span>|<span data-ttu-id="79dd9-109">Opis</span><span class="sxs-lookup"><span data-stu-id="79dd9-109">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="79dd9-110">S_OK</span><span class="sxs-lookup"><span data-stu-id="79dd9-110">S_OK</span></span>|<span data-ttu-id="79dd9-111">`GetMinThreads` pomyślnie zwrócono.</span><span class="sxs-lookup"><span data-stu-id="79dd9-111">`GetMinThreads` returned successfully.</span></span>|  
|<span data-ttu-id="79dd9-112">HOST_E_CLRNOTAVAILABLE</span><span class="sxs-lookup"><span data-stu-id="79dd9-112">HOST_E_CLRNOTAVAILABLE</span></span>|<span data-ttu-id="79dd9-113">Środowisko uruchomieniowe języka wspólnego (CLR) nie zostało załadowane do procesu lub środowisko CLR znajduje się w stanie, w którym nie można uruchomić kodu zarządzanego lub przetworzyć wywołania pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="79dd9-113">The common language runtime (CLR) has not been loaded into a process, or the CLR is in a state in which it cannot run managed code or process the call successfully.</span></span>|  
|<span data-ttu-id="79dd9-114">HOST_E_TIMEOUT</span><span class="sxs-lookup"><span data-stu-id="79dd9-114">HOST_E_TIMEOUT</span></span>|<span data-ttu-id="79dd9-115">Upłynął limit czasu połączenia.</span><span class="sxs-lookup"><span data-stu-id="79dd9-115">The call timed out.</span></span>|  
|<span data-ttu-id="79dd9-116">HOST_E_NOT_OWNER</span><span class="sxs-lookup"><span data-stu-id="79dd9-116">HOST_E_NOT_OWNER</span></span>|<span data-ttu-id="79dd9-117">Obiekt wywołujący nie jest właocicielem blokady.</span><span class="sxs-lookup"><span data-stu-id="79dd9-117">The caller does not own the lock.</span></span>|  
|<span data-ttu-id="79dd9-118">HOST_E_ABANDONED</span><span class="sxs-lookup"><span data-stu-id="79dd9-118">HOST_E_ABANDONED</span></span>|<span data-ttu-id="79dd9-119">Zdarzenie zostało anulowane podczas oczekiwania na niego zablokowanego wątku lub włókna.</span><span class="sxs-lookup"><span data-stu-id="79dd9-119">An event was canceled while a blocked thread or fiber was waiting on it.</span></span>|  
|<span data-ttu-id="79dd9-120">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="79dd9-120">E_FAIL</span></span>|<span data-ttu-id="79dd9-121">Wystąpił nieznany błąd krytyczny.</span><span class="sxs-lookup"><span data-stu-id="79dd9-121">An unknown catastrophic failure occurred.</span></span> <span data-ttu-id="79dd9-122">Gdy metoda zwraca E_FAIL, środowisko CLR nie będzie już można używać w procesie.</span><span class="sxs-lookup"><span data-stu-id="79dd9-122">When a method returns E_FAIL, the CLR is no longer usable within the process.</span></span> <span data-ttu-id="79dd9-123">Kolejne wywołania metod hostingu zwracają HOST_E_CLRNOTAVAILABLE.</span><span class="sxs-lookup"><span data-stu-id="79dd9-123">Subsequent calls to hosting methods return HOST_E_CLRNOTAVAILABLE.</span></span>|  
|<span data-ttu-id="79dd9-124">E_NOTIMPL</span><span class="sxs-lookup"><span data-stu-id="79dd9-124">E_NOTIMPL</span></span>|<span data-ttu-id="79dd9-125">Host nie oferuje implementacji programu `GetMinThreads` .</span><span class="sxs-lookup"><span data-stu-id="79dd9-125">The host does not provide an implementation of `GetMinThreads`.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="79dd9-126">Uwagi</span><span class="sxs-lookup"><span data-stu-id="79dd9-126">Remarks</span></span>  

 <span data-ttu-id="79dd9-127">Host może potrzebować wyłącznej kontroli nad liczbą wątków przydzielonych do żądań we/wy usługi, z przyczyn takich jak implementacja, wydajność lub skalowalność.</span><span class="sxs-lookup"><span data-stu-id="79dd9-127">A host might want exclusive control over the number of threads allotted to service I/O requests, for reasons such as implementation, performance, or scalability.</span></span> <span data-ttu-id="79dd9-128">Z tego powodu host nie musi być zaimplementowany `GetMinThreads` .</span><span class="sxs-lookup"><span data-stu-id="79dd9-128">For this reason, the host is not required to implement `GetMinThreads`.</span></span> <span data-ttu-id="79dd9-129">W takim przypadku host powinien zwrócić E_NOTIMPL z tej metody.</span><span class="sxs-lookup"><span data-stu-id="79dd9-129">In this case, the host should return E_NOTIMPL from this method.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="79dd9-130">Wymagania</span><span class="sxs-lookup"><span data-stu-id="79dd9-130">Requirements</span></span>  

 <span data-ttu-id="79dd9-131">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="79dd9-131">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="79dd9-132">**Nagłówek:** MSCorEE. h</span><span class="sxs-lookup"><span data-stu-id="79dd9-132">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="79dd9-133">**Biblioteka:** Uwzględnione jako zasób w MSCorEE.dll</span><span class="sxs-lookup"><span data-stu-id="79dd9-133">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="79dd9-134">**.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="79dd9-134">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="79dd9-135">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="79dd9-135">See also</span></span>

- [<span data-ttu-id="79dd9-136">ICLRIoCompletionManager — Interfejs</span><span class="sxs-lookup"><span data-stu-id="79dd9-136">ICLRIoCompletionManager Interface</span></span>](iclriocompletionmanager-interface.md)
- [<span data-ttu-id="79dd9-137">IHostIoCompletionManager — Interfejs</span><span class="sxs-lookup"><span data-stu-id="79dd9-137">IHostIoCompletionManager Interface</span></span>](ihostiocompletionmanager-interface.md)
