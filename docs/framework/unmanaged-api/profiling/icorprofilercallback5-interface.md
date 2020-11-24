---
title: ICorProfilerCallback5 — Interfejs
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback5
api_location:
- Mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback5
helpviewer_keywords:
- ICorProfilerCallback5 interface [.NET Framework profiling]
ms.assetid: 61d2e9ef-5f1f-4771-8847-239616e35d84
topic_type:
- apiref
ms.openlocfilehash: 8e94aebc489fff1c81593e54b17c471e7228d810
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95689293"
---
# <a name="icorprofilercallback5-interface"></a><span data-ttu-id="836f5-102">ICorProfilerCallback5 — Interfejs</span><span class="sxs-lookup"><span data-stu-id="836f5-102">ICorProfilerCallback5 Interface</span></span>

<span data-ttu-id="836f5-103">Uzupełnia informacje ułatwiające profilerowi zidentyfikowanie pełnego zamknięcia obiektów na żywo, gdy jest używana z [ICorProfilerCallback:: RootReferences —](icorprofilercallback-rootreferences-method.md) lub [ICorProfilerCallback2:: RootReferences2 —](icorprofilercallback2-rootreferences2-method.md) oraz metodami [ICorProfilerCallback:: ObjectReferences —](icorprofilercallback-objectreferences-method.md) i [ConditionalWeakTableElementReferences —](icorprofilercallback5-conditionalweaktableelementreferences-method.md) .</span><span class="sxs-lookup"><span data-stu-id="836f5-103">Supplements information to help a profiler identify the full closure of live objects, when used with either the [ICorProfilerCallback::RootReferences](icorprofilercallback-rootreferences-method.md) or [ICorProfilerCallback2::RootReferences2](icorprofilercallback2-rootreferences2-method.md) method together with the [ICorProfilerCallback::ObjectReferences](icorprofilercallback-objectreferences-method.md) and [ConditionalWeakTableElementReferences](icorprofilercallback5-conditionalweaktableelementreferences-method.md) methods.</span></span>  
  
 <span data-ttu-id="836f5-104">`ICorProfilerCallback5` musi być zaimplementowany przez profiler pamięci zarządzanej, aby subskrybować powiadomienia związane z dojściami zależnymi.</span><span class="sxs-lookup"><span data-stu-id="836f5-104">`ICorProfilerCallback5` must be implemented by a managed memory profiler to subscribe to notifications related to dependent handles.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="836f5-105">Uwagi</span><span class="sxs-lookup"><span data-stu-id="836f5-105">Remarks</span></span>  
  
## <a name="methods"></a><span data-ttu-id="836f5-106">Metody</span><span class="sxs-lookup"><span data-stu-id="836f5-106">Methods</span></span>  
  
|<span data-ttu-id="836f5-107">Metoda</span><span class="sxs-lookup"><span data-stu-id="836f5-107">Method</span></span>|<span data-ttu-id="836f5-108">Opis</span><span class="sxs-lookup"><span data-stu-id="836f5-108">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="836f5-109">ConditionalWeakTableElementReferences, metoda</span><span class="sxs-lookup"><span data-stu-id="836f5-109">ConditionalWeakTableElementReferences Method</span></span>](icorprofilercallback5-conditionalweaktableelementreferences-method.md)|<span data-ttu-id="836f5-110">Identyfikuje przechodnie zamknięcie obiektów, do których odwołują się te elementy główne za pośrednictwem bezpośrednich odwołań do pól składowych i za pośrednictwem `ConditionalWeakTable` zależności.</span><span class="sxs-lookup"><span data-stu-id="836f5-110">Identifies the transitive closure of objects referenced by those roots through both direct member field references and through `ConditionalWeakTable` dependencies.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="836f5-111">Wymagania</span><span class="sxs-lookup"><span data-stu-id="836f5-111">Requirements</span></span>  

 <span data-ttu-id="836f5-112">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="836f5-112">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="836f5-113">**Nagłówek:** CorProf. idl, CorProf. h</span><span class="sxs-lookup"><span data-stu-id="836f5-113">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="836f5-114">**.NET Framework wersje:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="836f5-114">**.NET Framework Versions:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="836f5-115">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="836f5-115">See also</span></span>

- [<span data-ttu-id="836f5-116">Interfejsy profilowania</span><span class="sxs-lookup"><span data-stu-id="836f5-116">Profiling Interfaces</span></span>](profiling-interfaces.md)
- [<span data-ttu-id="836f5-117">ICorProfilerCallback2 — Interfejs</span><span class="sxs-lookup"><span data-stu-id="836f5-117">ICorProfilerCallback2 Interface</span></span>](icorprofilercallback2-interface.md)
