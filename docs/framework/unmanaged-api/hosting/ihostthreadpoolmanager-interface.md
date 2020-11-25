---
title: IHostThreadPoolManager — Interfejs
ms.date: 03/30/2017
api_name:
- IHostThreadPoolManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostThreadPoolManager
helpviewer_keywords:
- IHostThreadPoolManager interface [.NET Framework hosting]
ms.assetid: c3a2cd90-7c4e-4374-bb87-b41befb8344f
topic_type:
- apiref
ms.openlocfilehash: b6625b0ef4dc3de4067514a0b39849c7a958d5c4
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95730763"
---
# <a name="ihostthreadpoolmanager-interface"></a><span data-ttu-id="40ff5-102">IHostThreadPoolManager — Interfejs</span><span class="sxs-lookup"><span data-stu-id="40ff5-102">IHostThreadPoolManager Interface</span></span>

<span data-ttu-id="40ff5-103">Dostarcza metody, które umożliwiają środowisko uruchomieniowe języka wspólnego (CLR) do konfigurowania puli wątków i umieszczania elementów roboczych w kolejce w puli wątków.</span><span class="sxs-lookup"><span data-stu-id="40ff5-103">Provides methods that enable the common language runtime (CLR) to configure the thread pool and to queue work items to the thread pool.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="40ff5-104">Metody</span><span class="sxs-lookup"><span data-stu-id="40ff5-104">Methods</span></span>  
  
|<span data-ttu-id="40ff5-105">Metoda</span><span class="sxs-lookup"><span data-stu-id="40ff5-105">Method</span></span>|<span data-ttu-id="40ff5-106">Opis</span><span class="sxs-lookup"><span data-stu-id="40ff5-106">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="40ff5-107">GetAvailableThreads, metoda</span><span class="sxs-lookup"><span data-stu-id="40ff5-107">GetAvailableThreads Method</span></span>](ihostthreadpoolmanager-getavailablethreads-method.md)|<span data-ttu-id="40ff5-108">Pobiera liczbę wątków w puli wątków, które nie przetwarzają obecnie elementów roboczych.</span><span class="sxs-lookup"><span data-stu-id="40ff5-108">Gets the number of threads in the thread pool that are not currently processing work items.</span></span>|  
|[<span data-ttu-id="40ff5-109">GetMaxThreads, metoda</span><span class="sxs-lookup"><span data-stu-id="40ff5-109">GetMaxThreads Method</span></span>](ihostthreadpoolmanager-getmaxthreads-method.md)|<span data-ttu-id="40ff5-110">Pobiera maksymalną liczbę wątków, które Host przechowuje współbieżnie w puli wątków.</span><span class="sxs-lookup"><span data-stu-id="40ff5-110">Gets the maximum number of threads that the host maintains concurrently in the thread pool.</span></span>|  
|[<span data-ttu-id="40ff5-111">GetMinThreads, metoda</span><span class="sxs-lookup"><span data-stu-id="40ff5-111">GetMinThreads Method</span></span>](ihostthreadpoolmanager-getminthreads-method.md)|<span data-ttu-id="40ff5-112">Pobiera minimalną liczbę bezczynnych wątków hostowanych przez hosta w oczekiwaniu na żądania.</span><span class="sxs-lookup"><span data-stu-id="40ff5-112">Gets the minimum number of idle threads that the host maintains in anticipation of requests.</span></span>|  
|[<span data-ttu-id="40ff5-113">QueueUserWorkItem, metoda</span><span class="sxs-lookup"><span data-stu-id="40ff5-113">QueueUserWorkItem Method</span></span>](ihostthreadpoolmanager-queueuserworkitem-method.md)|<span data-ttu-id="40ff5-114">Kolejkuje funkcję do wykonania i dostarcza obiekt zawierający dane, które mają być używane przez funkcję.</span><span class="sxs-lookup"><span data-stu-id="40ff5-114">Queues a function for execution, and provides an object containing data to be used by the function.</span></span>|  
|[<span data-ttu-id="40ff5-115">SetMaxThreads, metoda</span><span class="sxs-lookup"><span data-stu-id="40ff5-115">SetMaxThreads Method</span></span>](ihostthreadpoolmanager-setmaxthreads-method.md)|<span data-ttu-id="40ff5-116">Ustawia maksymalną liczbę wątków, które host może przechowywać w puli wątków.</span><span class="sxs-lookup"><span data-stu-id="40ff5-116">Sets the maximum number of threads that the host can maintain in the thread pool.</span></span>|  
|[<span data-ttu-id="40ff5-117">SetMinThreads, metoda</span><span class="sxs-lookup"><span data-stu-id="40ff5-117">SetMinThreads Method</span></span>](ihostthreadpoolmanager-setminthreads-method.md)|<span data-ttu-id="40ff5-118">Określa minimalną liczbę bezczynnych wątków, które host musi zachować w oczekiwaniu na żądania.</span><span class="sxs-lookup"><span data-stu-id="40ff5-118">Sets the minimum number of idle threads that the host must maintain in anticipation of requests.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="40ff5-119">Uwagi</span><span class="sxs-lookup"><span data-stu-id="40ff5-119">Remarks</span></span>  

 <span data-ttu-id="40ff5-120">Host nie jest wymagany do skonfigurowania puli wątków przy użyciu wartości określonych w wywołaniach `SetMaxThreads` `SetMinThreads` metod i.</span><span class="sxs-lookup"><span data-stu-id="40ff5-120">The host is not required to configure the thread pool by using the values specified in calls to the `SetMaxThreads` and `SetMinThreads` methods.</span></span> <span data-ttu-id="40ff5-121">W takim przypadku host powinien zwrócić wartość HRESULT E_NOTIMPL z tych metod.</span><span class="sxs-lookup"><span data-stu-id="40ff5-121">In this case, the host should return an HRESULT value of E_NOTIMPL from these methods.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="40ff5-122">Wymagania</span><span class="sxs-lookup"><span data-stu-id="40ff5-122">Requirements</span></span>  

 <span data-ttu-id="40ff5-123">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="40ff5-123">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="40ff5-124">**Nagłówek:** MSCorEE. h</span><span class="sxs-lookup"><span data-stu-id="40ff5-124">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="40ff5-125">**Biblioteka:** Uwzględnione jako zasób w MSCorEE.dll</span><span class="sxs-lookup"><span data-stu-id="40ff5-125">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="40ff5-126">**.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="40ff5-126">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="40ff5-127">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="40ff5-127">See also</span></span>

- <xref:System.Threading>
- <xref:System.Threading.ThreadPool>
- [<span data-ttu-id="40ff5-128">Hosting — Interfejsy</span><span class="sxs-lookup"><span data-stu-id="40ff5-128">Hosting Interfaces</span></span>](hosting-interfaces.md)
