---
title: ICLRTask2::EndPreventAsyncAbort — Metoda
ms.date: 03/30/2017
api_name:
- ICLRTask2.EndPreventAsyncAbort
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRTask2::EndPreventAsyncAbort
helpviewer_keywords:
- EndPreventAsyncAbort method [.NET Framework hosting]
- ICLRTask2::EndPreventAsyncAbort method [.NET Framework hosting]
ms.assetid: d8013659-e3df-44b3-814f-a6b534ce62f8
topic_type:
- apiref
ms.openlocfilehash: 7f8963403c60815bbf1cd3008ed7fec73d849fea
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95720259"
---
# <a name="iclrtask2endpreventasyncabort-method"></a><span data-ttu-id="b2a45-102">ICLRTask2::EndPreventAsyncAbort — Metoda</span><span class="sxs-lookup"><span data-stu-id="b2a45-102">ICLRTask2::EndPreventAsyncAbort Method</span></span>

<span data-ttu-id="b2a45-103">Zezwala na to, aby nowe lub oczekujące żądania przerwania wątku powodowały przerwania wątku w bieżącym wątku.</span><span class="sxs-lookup"><span data-stu-id="b2a45-103">Allows new or pending thread abort requests to result in thread aborts on the current thread.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="b2a45-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="b2a45-104">Syntax</span></span>  
  
```cpp  
HRESULT EndPreventAsyncAbort();  
```  
  
## <a name="return-value"></a><span data-ttu-id="b2a45-105">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="b2a45-105">Return Value</span></span>  

 <span data-ttu-id="b2a45-106">Ta metoda zwraca następujące określone wartości HRESULT oraz błędy HRESULT wskazujące niepowodzenie metody.</span><span class="sxs-lookup"><span data-stu-id="b2a45-106">This method returns the following specific HRESULTs as well as HRESULT errors that indicate method failure.</span></span>  
  
|<span data-ttu-id="b2a45-107">HRESULT</span><span class="sxs-lookup"><span data-stu-id="b2a45-107">HRESULT</span></span>|<span data-ttu-id="b2a45-108">Opis</span><span class="sxs-lookup"><span data-stu-id="b2a45-108">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="b2a45-109">S_OK</span><span class="sxs-lookup"><span data-stu-id="b2a45-109">S_OK</span></span>|<span data-ttu-id="b2a45-110">Metoda została ukończona pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="b2a45-110">The method completed successfully.</span></span>|  
|<span data-ttu-id="b2a45-111">HOST_E_INVALIDOPERATION</span><span class="sxs-lookup"><span data-stu-id="b2a45-111">HOST_E_INVALIDOPERATION</span></span>|<span data-ttu-id="b2a45-112">Metoda została wywołana w wątku, który nie jest bieżącym wątkiem.</span><span class="sxs-lookup"><span data-stu-id="b2a45-112">The method was called on a thread which is not the current thread.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="b2a45-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="b2a45-113">Remarks</span></span>  

 <span data-ttu-id="b2a45-114">Wywołanie tej metody zmniejsza licznik Opóźnij wątek-Abort dla bieżącego wątku o jeden.</span><span class="sxs-lookup"><span data-stu-id="b2a45-114">Calling this method decrements the delay-thread-abort counter for the current thread by one.</span></span>  
  
 <span data-ttu-id="b2a45-115">Wywołania [ICLRTask2:: BeginPreventAsyncAbort —](iclrtask2-beginpreventasyncabort-method.md) i `EndPreventAsyncAbort` mogą być zagnieżdżane.</span><span class="sxs-lookup"><span data-stu-id="b2a45-115">Calls to [ICLRTask2::BeginPreventAsyncAbort](iclrtask2-beginpreventasyncabort-method.md) and `EndPreventAsyncAbort` can be nested.</span></span> <span data-ttu-id="b2a45-116">Tak długo, jak licznik jest większy od zera, przerwania wątku dla bieżącego wątku są opóźnione.</span><span class="sxs-lookup"><span data-stu-id="b2a45-116">As long as the counter is greater than zero, thread aborts for the current thread are delayed.</span></span>  
  
 <span data-ttu-id="b2a45-117">Funkcja, która jest udostępniona przez tę funkcję, jest używana wewnętrznie przez maszynę wirtualną (VM).</span><span class="sxs-lookup"><span data-stu-id="b2a45-117">The functionality that is exposed by this feature is used internally by the virtual machine (VM).</span></span> <span data-ttu-id="b2a45-118">Użycie tych metod może spowodować nieokreślone zachowanie maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b2a45-118">Misuse of these methods may cause unspecified behavior in the VM.</span></span> <span data-ttu-id="b2a45-119">Na przykład wywołanie `EndPreventAsyncAbort` bez pierwszego wywołania `BeginPreventAsyncAbort` może spowodować ustawienie wartości zero dla licznika, gdy maszyna wirtualna została wcześniej zwiększona.</span><span class="sxs-lookup"><span data-stu-id="b2a45-119">For example, calling `EndPreventAsyncAbort` without first calling `BeginPreventAsyncAbort` could set the counter to zero when the VM has previously incremented it.</span></span> <span data-ttu-id="b2a45-120">Podobnie licznik wewnętrzny nie jest sprawdzany pod kątem przepełnienia.</span><span class="sxs-lookup"><span data-stu-id="b2a45-120">Similarly, the internal counter is not checked for overflow.</span></span> <span data-ttu-id="b2a45-121">W przypadku przekroczenia limitu całkowitego, ponieważ jest zwiększana przez zarówno hosta, jak i maszynę wirtualną, zachowanie nie zostanie określone.</span><span class="sxs-lookup"><span data-stu-id="b2a45-121">If it exceeds its integral limit because it is incremented by both the host and the VM, the resulting behavior is unspecified.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="b2a45-122">Wymagania</span><span class="sxs-lookup"><span data-stu-id="b2a45-122">Requirements</span></span>  

 <span data-ttu-id="b2a45-123">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="b2a45-123">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="b2a45-124">**Nagłówek:** MSCorEE. h</span><span class="sxs-lookup"><span data-stu-id="b2a45-124">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="b2a45-125">**Biblioteka:** Uwzględnione jako zasób w MSCorEE.dll</span><span class="sxs-lookup"><span data-stu-id="b2a45-125">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="b2a45-126">**.NET Framework wersje:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="b2a45-126">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="b2a45-127">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="b2a45-127">See also</span></span>

- [<span data-ttu-id="b2a45-128">BeginPreventAsyncAbort, metoda</span><span class="sxs-lookup"><span data-stu-id="b2a45-128">BeginPreventAsyncAbort Method</span></span>](iclrtask2-beginpreventasyncabort-method.md)
- [<span data-ttu-id="b2a45-129">ICLRTask2 — Interfejs</span><span class="sxs-lookup"><span data-stu-id="b2a45-129">ICLRTask2 Interface</span></span>](iclrtask2-interface.md)
- [<span data-ttu-id="b2a45-130">ICLRTaskManager — Interfejs</span><span class="sxs-lookup"><span data-stu-id="b2a45-130">ICLRTaskManager Interface</span></span>](iclrtaskmanager-interface.md)
- [<span data-ttu-id="b2a45-131">IHostTask — Interfejs</span><span class="sxs-lookup"><span data-stu-id="b2a45-131">IHostTask Interface</span></span>](ihosttask-interface.md)
- [<span data-ttu-id="b2a45-132">IHostTaskManager — Interfejs</span><span class="sxs-lookup"><span data-stu-id="b2a45-132">IHostTaskManager Interface</span></span>](ihosttaskmanager-interface.md)
- [<span data-ttu-id="b2a45-133">Hosting — Interfejsy</span><span class="sxs-lookup"><span data-stu-id="b2a45-133">Hosting Interfaces</span></span>](hosting-interfaces.md)
