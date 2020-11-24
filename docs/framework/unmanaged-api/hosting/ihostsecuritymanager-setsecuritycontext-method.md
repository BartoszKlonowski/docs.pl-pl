---
title: IHostSecurityManager::SetSecurityContext — Metoda
ms.date: 03/30/2017
api_name:
- IHostSecurityManager.SetSecurityContext
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostSecurityManager::SetSecurityContext
helpviewer_keywords:
- SetSecurityContext method [.NET Framework hosting]
- IHostSecurityManager::SetSecurityContext method [.NET Framework hosting]
ms.assetid: e4372384-ee69-48d7-97e0-8fab7866597a
topic_type:
- apiref
ms.openlocfilehash: dadacaea2b8741afc7b8c51404e2604dc759a629
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95680381"
---
# <a name="ihostsecuritymanagersetsecuritycontext-method"></a><span data-ttu-id="2e5c5-102">IHostSecurityManager::SetSecurityContext — Metoda</span><span class="sxs-lookup"><span data-stu-id="2e5c5-102">IHostSecurityManager::SetSecurityContext Method</span></span>

<span data-ttu-id="2e5c5-103">Ustawia kontekst zabezpieczeń aktualnie wykonywanego wątku.</span><span class="sxs-lookup"><span data-stu-id="2e5c5-103">Sets the security context of the currently executing thread.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="2e5c5-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="2e5c5-104">Syntax</span></span>  
  
```cpp  
HRESULT SetSecurityContext (  
    [in]  EContextType eContextType,  
    [out] IHostSecurityContext** ppSecurityContext  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="2e5c5-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="2e5c5-105">Parameters</span></span>  

 `eContextType`  
 <span data-ttu-id="2e5c5-106">podczas Jedna z wartości [EContextType —](econtexttype-enumeration.md) , wskazująca, jakiego typu kontekstu środowisko uruchomieniowe języka wspólnego (CLR) umieszcza na hoście.</span><span class="sxs-lookup"><span data-stu-id="2e5c5-106">[in] One of the [EContextType](econtexttype-enumeration.md) values, indicating what type of context the common language runtime (CLR) is placing on the host.</span></span>  
  
 `ppSecurityContext`  
 <span data-ttu-id="2e5c5-107">określoną Wskaźnik do adresu nowego obiektu [IHostSecurityContext](ihostsecuritycontext-interface.md) .</span><span class="sxs-lookup"><span data-stu-id="2e5c5-107">[out] A pointer to the address of a new [IHostSecurityContext](ihostsecuritycontext-interface.md) object.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="2e5c5-108">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="2e5c5-108">Return Value</span></span>  
  
|<span data-ttu-id="2e5c5-109">HRESULT</span><span class="sxs-lookup"><span data-stu-id="2e5c5-109">HRESULT</span></span>|<span data-ttu-id="2e5c5-110">Opis</span><span class="sxs-lookup"><span data-stu-id="2e5c5-110">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="2e5c5-111">S_OK</span><span class="sxs-lookup"><span data-stu-id="2e5c5-111">S_OK</span></span>|<span data-ttu-id="2e5c5-112">`SetSecurityContext` pomyślnie zwrócono.</span><span class="sxs-lookup"><span data-stu-id="2e5c5-112">`SetSecurityContext` returned successfully.</span></span>|  
|<span data-ttu-id="2e5c5-113">HOST_E_CLRNOTAVAILABLE</span><span class="sxs-lookup"><span data-stu-id="2e5c5-113">HOST_E_CLRNOTAVAILABLE</span></span>|<span data-ttu-id="2e5c5-114">Środowisko CLR nie zostało załadowane do procesu lub środowisko CLR znajduje się w stanie, w którym nie można uruchomić kodu zarządzanego lub przetworzyć wywołania pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="2e5c5-114">The CLR has not been loaded into a process, or the CLR is in a state in which it cannot run managed code or process the call successfully.</span></span>|  
|<span data-ttu-id="2e5c5-115">HOST_E_TIMEOUT</span><span class="sxs-lookup"><span data-stu-id="2e5c5-115">HOST_E_TIMEOUT</span></span>|<span data-ttu-id="2e5c5-116">Upłynął limit czasu połączenia.</span><span class="sxs-lookup"><span data-stu-id="2e5c5-116">The call timed out.</span></span>|  
|<span data-ttu-id="2e5c5-117">HOST_E_NOT_OWNER</span><span class="sxs-lookup"><span data-stu-id="2e5c5-117">HOST_E_NOT_OWNER</span></span>|<span data-ttu-id="2e5c5-118">Obiekt wywołujący nie jest właocicielem blokady.</span><span class="sxs-lookup"><span data-stu-id="2e5c5-118">The caller does not own the lock.</span></span>|  
|<span data-ttu-id="2e5c5-119">HOST_E_ABANDONED</span><span class="sxs-lookup"><span data-stu-id="2e5c5-119">HOST_E_ABANDONED</span></span>|<span data-ttu-id="2e5c5-120">Zdarzenie zostało anulowane podczas oczekiwania na niego zablokowanego wątku lub włókna.</span><span class="sxs-lookup"><span data-stu-id="2e5c5-120">An event was canceled while a blocked thread or fiber was waiting on it.</span></span>|  
|<span data-ttu-id="2e5c5-121">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="2e5c5-121">E_FAIL</span></span>|<span data-ttu-id="2e5c5-122">Wystąpił nieznany błąd krytyczny.</span><span class="sxs-lookup"><span data-stu-id="2e5c5-122">An unknown catastrophic failure occurred.</span></span> <span data-ttu-id="2e5c5-123">Gdy metoda zwraca E_FAIL, środowisko CLR nie będzie już można używać w procesie.</span><span class="sxs-lookup"><span data-stu-id="2e5c5-123">When a method returns E_FAIL, the CLR is no longer usable within the process.</span></span> <span data-ttu-id="2e5c5-124">Kolejne wywołania metod hostingu zwracają HOST_E_CLRNOTAVAILABLE.</span><span class="sxs-lookup"><span data-stu-id="2e5c5-124">Subsequent calls to hosting methods return HOST_E_CLRNOTAVAILABLE.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="2e5c5-125">Uwagi</span><span class="sxs-lookup"><span data-stu-id="2e5c5-125">Remarks</span></span>  

 <span data-ttu-id="2e5c5-126">Środowisko CLR wywołuje `SetSecurityContext` kilka scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="2e5c5-126">The CLR calls `SetSecurityContext` in several scenarios.</span></span> <span data-ttu-id="2e5c5-127">Przed wykonaniem konstruktorów klas i modułów oraz finalizatorów, środowisko CLR wywołuje `SetSecurityContext` w celu ochrony hosta przed błędami wykonania.</span><span class="sxs-lookup"><span data-stu-id="2e5c5-127">Before it executes class and module constructors and finalizers, the CLR calls `SetSecurityContext` to protect the host from execution failures.</span></span> <span data-ttu-id="2e5c5-128">Następnie resetuje kontekst zabezpieczeń do oryginalnego stanu po wykonaniu konstruktora lub finalizatora przy użyciu innego wywołania do `SetSecurityContext` .</span><span class="sxs-lookup"><span data-stu-id="2e5c5-128">It then resets the security context to its original state after execution of the constructor or finalizer, by using another call to `SetSecurityContext`.</span></span> <span data-ttu-id="2e5c5-129">Podobny wzorzec występuje po zakończeniu operacji we/wy.</span><span class="sxs-lookup"><span data-stu-id="2e5c5-129">A similar pattern occurs with I/O completion.</span></span> <span data-ttu-id="2e5c5-130">Jeśli Host implementuje [IHostIoCompletionManager](ihostiocompletionmanager-interface.md), środowisko CLR wywołuje się `SetSecurityContext` po wywołaniach hosta [ICLRIoCompletionManager:: OnComplete](iclriocompletionmanager-oncomplete-method.md).</span><span class="sxs-lookup"><span data-stu-id="2e5c5-130">If the host implements [IHostIoCompletionManager](ihostiocompletionmanager-interface.md), the CLR calls `SetSecurityContext` after the host calls [ICLRIoCompletionManager::OnComplete](iclriocompletionmanager-oncomplete-method.md).</span></span>  
  
 <span data-ttu-id="2e5c5-131">W przypadku asynchronicznych punktów w wątkach roboczych, środowisko CLR wywołuje `SetSecurityContext` wewnątrz <xref:System.Threading.ThreadPool.QueueUserWorkItem%2A?displayProperty=nameWithType> lub w [IHostThreadPoolManager:: QueueUserWorkItem](ihostthreadpoolmanager-queueuserworkitem-method.md), w zależności od tego, czy host lub środowisko CLR implementuje pulę wątków.</span><span class="sxs-lookup"><span data-stu-id="2e5c5-131">At asynchronous points in worker threads, the CLR calls `SetSecurityContext` within <xref:System.Threading.ThreadPool.QueueUserWorkItem%2A?displayProperty=nameWithType> or within [IHostThreadPoolManager::QueueUserWorkItem](ihostthreadpoolmanager-queueuserworkitem-method.md), depending on whether the host or the CLR is implementing the thread pool.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="2e5c5-132">Wymagania</span><span class="sxs-lookup"><span data-stu-id="2e5c5-132">Requirements</span></span>  

 <span data-ttu-id="2e5c5-133">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="2e5c5-133">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="2e5c5-134">**Nagłówek:** MSCorEE. h</span><span class="sxs-lookup"><span data-stu-id="2e5c5-134">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="2e5c5-135">**Biblioteka:** Uwzględnione jako zasób w MSCorEE.dll</span><span class="sxs-lookup"><span data-stu-id="2e5c5-135">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="2e5c5-136">**.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="2e5c5-136">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="2e5c5-137">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="2e5c5-137">See also</span></span>

- <xref:System.Threading.ThreadPool?displayProperty=nameWithType>
- [<span data-ttu-id="2e5c5-138">EContextType — Wyliczenie</span><span class="sxs-lookup"><span data-stu-id="2e5c5-138">EContextType Enumeration</span></span>](econtexttype-enumeration.md)
- [<span data-ttu-id="2e5c5-139">ICLRIoCompletionManager — Interfejs</span><span class="sxs-lookup"><span data-stu-id="2e5c5-139">ICLRIoCompletionManager Interface</span></span>](iclriocompletionmanager-interface.md)
- [<span data-ttu-id="2e5c5-140">IHostIoCompletionManager — Interfejs</span><span class="sxs-lookup"><span data-stu-id="2e5c5-140">IHostIoCompletionManager Interface</span></span>](ihostiocompletionmanager-interface.md)
- [<span data-ttu-id="2e5c5-141">IHostSecurityContext — Interfejs</span><span class="sxs-lookup"><span data-stu-id="2e5c5-141">IHostSecurityContext Interface</span></span>](ihostsecuritycontext-interface.md)
- [<span data-ttu-id="2e5c5-142">IHostSecurityManager — Interfejs</span><span class="sxs-lookup"><span data-stu-id="2e5c5-142">IHostSecurityManager Interface</span></span>](ihostsecuritymanager-interface.md)
- [<span data-ttu-id="2e5c5-143">IHostThreadPoolManager — Interfejs</span><span class="sxs-lookup"><span data-stu-id="2e5c5-143">IHostThreadPoolManager Interface</span></span>](ihostthreadpoolmanager-interface.md)
