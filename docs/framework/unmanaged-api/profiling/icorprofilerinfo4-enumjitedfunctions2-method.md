---
title: ICorProfilerInfo4::EnumJITedFunctions2 — Metoda
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo4.EnumJITedFunctions2
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo4::EnumJITedFunctions2
helpviewer_keywords:
- EnumJITedFunctions2 method, ICorProfilerInfo4 interface [.NET Framework profiling]
- ICorProfilerInfo4::EnumJITedFunctions2 method [.NET Framework profiling]
ms.assetid: 40e9a1be-9bd2-4fad-9921-34a84b61c1e3
topic_type:
- apiref
ms.openlocfilehash: 2a6ddaef7b64427f8349abedbbd85b4d82a0b88c
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95697795"
---
# <a name="icorprofilerinfo4enumjitedfunctions2-method"></a><span data-ttu-id="97fd2-102">ICorProfilerInfo4::EnumJITedFunctions2 — Metoda</span><span class="sxs-lookup"><span data-stu-id="97fd2-102">ICorProfilerInfo4::EnumJITedFunctions2 Method</span></span>

<span data-ttu-id="97fd2-103">Zwraca moduł wyliczający dla wszystkich funkcji, które były poprzednio skompilowane JIT i ponownie skompilowane w trybie JIT.</span><span class="sxs-lookup"><span data-stu-id="97fd2-103">Returns an enumerator for all functions that were previously JIT-compiled and JIT-recompiled.</span></span> <span data-ttu-id="97fd2-104">Ta metoda zastępuje metodę [ICorProfilerInfo3:: EnumJITedFunctions —](icorprofilerinfo3-enumjitedfunctions-method.md) , która nie WYLICZA identyfikatorów JIT-ponownie kompilowanych.</span><span class="sxs-lookup"><span data-stu-id="97fd2-104">This method replaces the [ICorProfilerInfo3::EnumJITedFunctions](icorprofilerinfo3-enumjitedfunctions-method.md) method, which does not enumerate JIT-recompiled IDs.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="97fd2-105">Składnia</span><span class="sxs-lookup"><span data-stu-id="97fd2-105">Syntax</span></span>  
  
```cpp  
HRESULT EnumJITedFunctions([out] ICorProfilerFunctionEnum** ppEnum);  
```  
  
## <a name="parameters"></a><span data-ttu-id="97fd2-106">Parametry</span><span class="sxs-lookup"><span data-stu-id="97fd2-106">Parameters</span></span>  

 `ppEnum`  
 <span data-ttu-id="97fd2-107">określoną Wskaźnik do modułu wyliczającego [ICorProfilerFunctionEnum](icorprofilerfunctionenum-interface.md) .</span><span class="sxs-lookup"><span data-stu-id="97fd2-107">[out] A pointer to the [ICorProfilerFunctionEnum](icorprofilerfunctionenum-interface.md) enumerator.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="97fd2-108">Uwagi</span><span class="sxs-lookup"><span data-stu-id="97fd2-108">Remarks</span></span>  

 <span data-ttu-id="97fd2-109">Ta metoda może nakładać się na `JITCompilation` wywołania zwrotne, takie jak Metoda [ICorProfilerCallback:: JITCompilationStarted](icorprofilercallback-jitcompilationstarted-method.md) .</span><span class="sxs-lookup"><span data-stu-id="97fd2-109">This method may overlap with `JITCompilation` callbacks such as the [ICorProfilerCallback::JITCompilationStarted](icorprofilercallback-jitcompilationstarted-method.md) method.</span></span> <span data-ttu-id="97fd2-110">Zwrócone Wyliczenie zawiera wartości dla `COR_PRF_FUNCTION::reJitId` pola.</span><span class="sxs-lookup"><span data-stu-id="97fd2-110">The returned enumeration includes values for the `COR_PRF_FUNCTION::reJitId` field.</span></span> <span data-ttu-id="97fd2-111">Metoda [ICorProfilerInfo3:: EnumJITedFunctions —](icorprofilerinfo3-enumjitedfunctions-method.md) , która zastępuje tę metodę, nie wylicza identyfikatorów, które ponownie skompilowano JIT, ponieważ `COR_PRF_FUNCTION::reJitId` pole jest zawsze ustawione na 0.</span><span class="sxs-lookup"><span data-stu-id="97fd2-111">The [ICorProfilerInfo3::EnumJITedFunctions](icorprofilerinfo3-enumjitedfunctions-method.md) method, which this method replaces, does not enumerate JIT-recompiled IDs, because the `COR_PRF_FUNCTION::reJitId` field is always set to 0.</span></span> <span data-ttu-id="97fd2-112">`ICorProfilerInfo4::EnumJITedFunctions`Metoda wylicza identyfikatory ponownie skompilowane JIT, ponieważ `COR_PRF_FUNCTION::reJitId` pole jest ustawione prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="97fd2-112">The `ICorProfilerInfo4::EnumJITedFunctions` method does enumerate JIT-recompiled IDs, because the `COR_PRF_FUNCTION::reJitId` field is set properly.</span></span> <span data-ttu-id="97fd2-113">Należy pamiętać, że metoda [ICorProfilerInfo4:: EnumJITedFunctions2 —](icorprofilerinfo4-enumjitedfunctions2-method.md) może wyzwolić wyrzucanie elementów bezużytecznych, natomiast [Metoda ICorProfilerInfo3:: EnumJITedFunctions —](icorprofilerinfo3-enumjitedfunctions-method.md) nie będzie.</span><span class="sxs-lookup"><span data-stu-id="97fd2-113">Note that the [ICorProfilerInfo4::EnumJITedFunctions2](icorprofilerinfo4-enumjitedfunctions2-method.md) method can trigger a garbage collection, whereas [ICorProfilerInfo3::EnumJITedFunctions method](icorprofilerinfo3-enumjitedfunctions-method.md) will not.</span></span>  <span data-ttu-id="97fd2-114">Aby uzyskać więcej informacji, zobacz [CORPROF_E_UNSUPPORTED_CALL_SEQUENCE HRESULT](corprof-e-unsupported-call-sequence-hresult.md).</span><span class="sxs-lookup"><span data-stu-id="97fd2-114">For more information, see [CORPROF_E_UNSUPPORTED_CALL_SEQUENCE HRESULT](corprof-e-unsupported-call-sequence-hresult.md).</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="97fd2-115">Wymagania</span><span class="sxs-lookup"><span data-stu-id="97fd2-115">Requirements</span></span>  

 <span data-ttu-id="97fd2-116">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="97fd2-116">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="97fd2-117">**Nagłówek:** CorProf. idl, CorProf. h</span><span class="sxs-lookup"><span data-stu-id="97fd2-117">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="97fd2-118">**Biblioteka:** CorGuids. lib</span><span class="sxs-lookup"><span data-stu-id="97fd2-118">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="97fd2-119">**.NET Framework wersje:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="97fd2-119">**.NET Framework Versions:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="97fd2-120">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="97fd2-120">See also</span></span>

- [<span data-ttu-id="97fd2-121">EnumJITedFunctions, metoda</span><span class="sxs-lookup"><span data-stu-id="97fd2-121">EnumJITedFunctions Method</span></span>](icorprofilerinfo3-enumjitedfunctions-method.md)
- [<span data-ttu-id="97fd2-122">ICorProfilerInfo4 — Interfejs</span><span class="sxs-lookup"><span data-stu-id="97fd2-122">ICorProfilerInfo4 Interface</span></span>](icorprofilerinfo4-interface.md)
- [<span data-ttu-id="97fd2-123">Interfejsy profilowania</span><span class="sxs-lookup"><span data-stu-id="97fd2-123">Profiling Interfaces</span></span>](profiling-interfaces.md)
- [<span data-ttu-id="97fd2-124">Profilowanie</span><span class="sxs-lookup"><span data-stu-id="97fd2-124">Profiling</span></span>](index.md)
