---
title: ICLRTask2 — Interfejs
ms.date: 03/30/2017
api_name:
- ICLRTask2
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRTask2
helpviewer_keywords:
- ICLRTask2 interface [.NET Framework hosting]
ms.assetid: b5a22ebc-0582-49de-91f9-97a3d9789290
topic_type:
- apiref
ms.openlocfilehash: 9332b3462ba389783a113d173e32850d40427ce2
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95720233"
---
# <a name="iclrtask2-interface"></a><span data-ttu-id="5584b-102">ICLRTask2 — Interfejs</span><span class="sxs-lookup"><span data-stu-id="5584b-102">ICLRTask2 Interface</span></span>

<span data-ttu-id="5584b-103">Oferuje wszystkie funkcje interfejsu [ICLRTask](iclrtask-interface.md) ; Ponadto udostępnia metody zezwalające na opóźnione przerywanie wątków w bieżącym wątku.</span><span class="sxs-lookup"><span data-stu-id="5584b-103">Provides all the functionality of the [ICLRTask](iclrtask-interface.md) interface; in addition, provides methods that allow thread aborts to be delayed on the current thread.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="5584b-104">Metody</span><span class="sxs-lookup"><span data-stu-id="5584b-104">Methods</span></span>  
  
|<span data-ttu-id="5584b-105">Metoda</span><span class="sxs-lookup"><span data-stu-id="5584b-105">Method</span></span>|<span data-ttu-id="5584b-106">Opis</span><span class="sxs-lookup"><span data-stu-id="5584b-106">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="5584b-107">BeginPreventAsyncAbort, metoda</span><span class="sxs-lookup"><span data-stu-id="5584b-107">BeginPreventAsyncAbort Method</span></span>](iclrtask2-beginpreventasyncabort-method.md)|<span data-ttu-id="5584b-108">Opóźnia nowe żądania przerwania wątku w bieżącym wątku.</span><span class="sxs-lookup"><span data-stu-id="5584b-108">Delays new thread abort requests on the current thread.</span></span>|  
|[<span data-ttu-id="5584b-109">EndPreventAsyncAbort, metoda</span><span class="sxs-lookup"><span data-stu-id="5584b-109">EndPreventAsyncAbort Method</span></span>](iclrtask2-endpreventasyncabort-method.md)|<span data-ttu-id="5584b-110">Zezwala na to, aby nowe lub oczekujące żądania przerwania wątku powodowały przerwania wątku w bieżącym wątku.</span><span class="sxs-lookup"><span data-stu-id="5584b-110">Allows new or pending thread abort requests to result in thread aborts on the current thread.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="5584b-111">Uwagi</span><span class="sxs-lookup"><span data-stu-id="5584b-111">Remarks</span></span>  

 <span data-ttu-id="5584b-112">`ICLRTask2`Interfejs dziedziczy `ICLRTask` interfejs i dodaje metody, które pozwalają hostowi opóźnić przerwania wątku, aby chronić region kodu, który nie może kończyć się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="5584b-112">The `ICLRTask2` interface inherits the `ICLRTask` interface and adds methods that allow the host to delay thread aborts, to protect a region of code that must not fail.</span></span> <span data-ttu-id="5584b-113">Wywołanie `BeginPreventAsyncAbort` zwiększa wartość licznika Opóźnij wątek i Przerwij dla bieżącego wątku i wywołuje `EndPreventAsyncAbort` jego zmniejszenie.</span><span class="sxs-lookup"><span data-stu-id="5584b-113">Calling `BeginPreventAsyncAbort` increments the delay-thread-abort counter for the current thread, and calling `EndPreventAsyncAbort` decrements it.</span></span> <span data-ttu-id="5584b-114">Wywołania `BeginPreventAsyncAbort` i `EndPreventAsyncAbort` mogą być zagnieżdżane.</span><span class="sxs-lookup"><span data-stu-id="5584b-114">Calls to `BeginPreventAsyncAbort` and `EndPreventAsyncAbort` can be nested.</span></span> <span data-ttu-id="5584b-115">Tak długo, jak licznik jest większy od zera, przerwania wątku dla bieżącego wątku są opóźnione.</span><span class="sxs-lookup"><span data-stu-id="5584b-115">As long as the counter is greater than zero, thread aborts for the current thread are delayed.</span></span>  
  
 <span data-ttu-id="5584b-116">Jeśli wywołania do `BeginPreventAsyncAbort` i `EndPreventAsyncAbort` nie są sparowane, możliwe jest osiągnięcie stanu, w którym przerwania wątku nie można dostarczyć do bieżącego wątku.</span><span class="sxs-lookup"><span data-stu-id="5584b-116">If calls to `BeginPreventAsyncAbort` and `EndPreventAsyncAbort` are not paired, it is possible to reach a state in which thread aborts cannot be delivered to the current thread.</span></span>  
  
 <span data-ttu-id="5584b-117">Opóźnienie nie jest uznawane za wątek, który przerywa siebie.</span><span class="sxs-lookup"><span data-stu-id="5584b-117">The delay is not honored for a thread that aborts itself.</span></span>  
  
 <span data-ttu-id="5584b-118">Funkcja, która jest udostępniona przez tę funkcję, jest używana wewnętrznie przez maszynę wirtualną (VM).</span><span class="sxs-lookup"><span data-stu-id="5584b-118">The functionality that is exposed by this feature is used internally by the virtual machine (VM).</span></span> <span data-ttu-id="5584b-119">Użycie tych metod może spowodować nieokreślone zachowanie maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5584b-119">Misuse of these methods may cause unspecified behavior in the VM.</span></span> <span data-ttu-id="5584b-120">Na przykład wywołanie `EndPreventAsyncAbort` bez pierwszego wywołania `BeginPreventAsyncAbort` może spowodować ustawienie wartości zero dla licznika, gdy maszyna wirtualna została wcześniej zwiększona.</span><span class="sxs-lookup"><span data-stu-id="5584b-120">For example, calling `EndPreventAsyncAbort` without first calling `BeginPreventAsyncAbort` could set the counter to zero when the VM has previously incremented it.</span></span> <span data-ttu-id="5584b-121">Podobnie licznik wewnętrzny nie jest sprawdzany pod kątem przepełnienia.</span><span class="sxs-lookup"><span data-stu-id="5584b-121">Similarly, the internal counter is not checked for overflow.</span></span> <span data-ttu-id="5584b-122">W przypadku przekroczenia limitu całkowitego, ponieważ jest zwiększana przez zarówno hosta, jak i maszynę wirtualną, zachowanie nie zostanie określone.</span><span class="sxs-lookup"><span data-stu-id="5584b-122">If it exceeds its integral limit because it is incremented by both the host and the VM, the resulting behavior is unspecified.</span></span>  
  
 <span data-ttu-id="5584b-123">Aby uzyskać informacje na temat członków dziedziczonych z `ICLRTask` i innych sposobów korzystania z tego interfejsu, zobacz Interfejs [ICLRTask](iclrtask-interface.md) .</span><span class="sxs-lookup"><span data-stu-id="5584b-123">For information about members inherited from `ICLRTask` and about the other uses of this interface, see the [ICLRTask](iclrtask-interface.md) interface.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="5584b-124">Wymagania</span><span class="sxs-lookup"><span data-stu-id="5584b-124">Requirements</span></span>  

 <span data-ttu-id="5584b-125">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="5584b-125">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="5584b-126">**Nagłówek:** MSCorEE. h</span><span class="sxs-lookup"><span data-stu-id="5584b-126">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="5584b-127">**Biblioteka:** Uwzględnione jako zasób w MSCorEE.dll</span><span class="sxs-lookup"><span data-stu-id="5584b-127">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="5584b-128">**.NET Framework wersje:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="5584b-128">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="5584b-129">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="5584b-129">See also</span></span>

- [<span data-ttu-id="5584b-130">ICLRTask — Interfejs</span><span class="sxs-lookup"><span data-stu-id="5584b-130">ICLRTask Interface</span></span>](iclrtask-interface.md)
- [<span data-ttu-id="5584b-131">ICLRTaskManager — Interfejs</span><span class="sxs-lookup"><span data-stu-id="5584b-131">ICLRTaskManager Interface</span></span>](iclrtaskmanager-interface.md)
- [<span data-ttu-id="5584b-132">IHostTask — Interfejs</span><span class="sxs-lookup"><span data-stu-id="5584b-132">IHostTask Interface</span></span>](ihosttask-interface.md)
- [<span data-ttu-id="5584b-133">IHostTaskManager — Interfejs</span><span class="sxs-lookup"><span data-stu-id="5584b-133">IHostTaskManager Interface</span></span>](ihosttaskmanager-interface.md)
- [<span data-ttu-id="5584b-134">Hosting — Interfejsy</span><span class="sxs-lookup"><span data-stu-id="5584b-134">Hosting Interfaces</span></span>](hosting-interfaces.md)
