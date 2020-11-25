---
title: ICorProfilerCallback::ClassUnloadFinished — Metoda
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.ClassUnloadFinished
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::ClassUnloadFinished
helpviewer_keywords:
- ICorProfilerCallback::ClassUnloadFinished method [.NET Framework profiling]
- ClassUnloadFinished method [.NET Framework profiling]
ms.assetid: 55674b68-678a-4747-ae06-4e91519c7305
topic_type:
- apiref
ms.openlocfilehash: 114d5d58d0d9098944299aefd0cb99a70c5da09d
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95700265"
---
# <a name="icorprofilercallbackclassunloadfinished-method"></a><span data-ttu-id="6b5a8-102">ICorProfilerCallback::ClassUnloadFinished — Metoda</span><span class="sxs-lookup"><span data-stu-id="6b5a8-102">ICorProfilerCallback::ClassUnloadFinished Method</span></span>

<span data-ttu-id="6b5a8-103">Powiadamia profiler o zakończeniu zwalniania klasy.</span><span class="sxs-lookup"><span data-stu-id="6b5a8-103">Notifies the profiler that a class has finished unloading.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="6b5a8-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="6b5a8-104">Syntax</span></span>  
  
```cpp  
HRESULT ClassUnloadFinished(  
    [in] ClassID classId,  
    [in] HRESULT hrStatus);  
```  
  
## <a name="parameters"></a><span data-ttu-id="6b5a8-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="6b5a8-105">Parameters</span></span>

- `classId`

  <span data-ttu-id="6b5a8-106">\[w] identyfikuje klasę, która została zwolniona.</span><span class="sxs-lookup"><span data-stu-id="6b5a8-106">\[in] Identifies the class that was unloaded.</span></span>

- `hrStatus`

  <span data-ttu-id="6b5a8-107">\[w] wynik HRESULT wskazujący, czy klasa została zwolniona pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="6b5a8-107">\[in] An HRESULT that indicates whether the class was unloaded successfully.</span></span>
  
## <a name="remarks"></a><span data-ttu-id="6b5a8-108">Uwagi</span><span class="sxs-lookup"><span data-stu-id="6b5a8-108">Remarks</span></span>  

 <span data-ttu-id="6b5a8-109">Niektóre części zwalniania klasy mogą być kontynuowane po `ClassUnloadFinished` wywołaniu wywołania zwrotnego.</span><span class="sxs-lookup"><span data-stu-id="6b5a8-109">Some parts of unloading the class might continue after the `ClassUnloadFinished` callback.</span></span> <span data-ttu-id="6b5a8-110">Błąd HRESULT w elemencie `hrStatus` wskazuje na błąd.</span><span class="sxs-lookup"><span data-stu-id="6b5a8-110">A failure HRESULT in `hrStatus` indicates a failure.</span></span> <span data-ttu-id="6b5a8-111">Jednak wynik HRESULT w programie `hrStatus` wskazuje tylko, że pierwsza część zwalniania klasy zakończyła się powodzeniem.</span><span class="sxs-lookup"><span data-stu-id="6b5a8-111">However, a success HRESULT in `hrStatus` indicates only that the first part of unloading the class has succeeded.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="6b5a8-112">Wymagania</span><span class="sxs-lookup"><span data-stu-id="6b5a8-112">Requirements</span></span>  

 <span data-ttu-id="6b5a8-113">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="6b5a8-113">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="6b5a8-114">**Nagłówek:** CorProf. idl, CorProf. h</span><span class="sxs-lookup"><span data-stu-id="6b5a8-114">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="6b5a8-115">**Biblioteka:** CorGuids. lib</span><span class="sxs-lookup"><span data-stu-id="6b5a8-115">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="6b5a8-116">**.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="6b5a8-116">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="6b5a8-117">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="6b5a8-117">See also</span></span>

- [<span data-ttu-id="6b5a8-118">ICorProfilerCallback — Interfejs</span><span class="sxs-lookup"><span data-stu-id="6b5a8-118">ICorProfilerCallback Interface</span></span>](icorprofilercallback-interface.md)
- [<span data-ttu-id="6b5a8-119">ClassUnloadStarted, metoda</span><span class="sxs-lookup"><span data-stu-id="6b5a8-119">ClassUnloadStarted Method</span></span>](icorprofilercallback-classunloadstarted-method.md)
