---
title: ICorProfilerCallback4::ReJITCompilationStarted — Metoda
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback4.ReJITCompilationStarted
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback4::ReJITCompilationStarted
helpviewer_keywords:
- ReJITCompilationStarted method, ICorProfilerCallback4 interface [.NET Framework profiling]
- ICorProfilerCallback4::ReJITCompilationStarted method [.NET Framework profiling]
ms.assetid: 512fdd00-262a-4456-a075-365ef4133c4d
topic_type:
- apiref
ms.openlocfilehash: 43db4ce0ba7a95a029e6c4928f55a99df9085164
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95730256"
---
# <a name="icorprofilercallback4rejitcompilationstarted-method"></a><span data-ttu-id="6e0c0-102">ICorProfilerCallback4::ReJITCompilationStarted — Metoda</span><span class="sxs-lookup"><span data-stu-id="6e0c0-102">ICorProfilerCallback4::ReJITCompilationStarted Method</span></span>

<span data-ttu-id="6e0c0-103">Powiadamia profiler, że został uruchomiony kompilator just-in-Time (JIT), aby ponownie skompilować funkcję.</span><span class="sxs-lookup"><span data-stu-id="6e0c0-103">Notifies the profiler that the just-in-time (JIT) compiler has started to recompile a function.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="6e0c0-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="6e0c0-104">Syntax</span></span>  
  
```cpp  
HRESULT ReJITCompilationStarted(
    [in] FunctionID functionId,  
    [in] ReJITID    rejitId,  
    [in] BOOL       fIsSafeToBlock);  
```  
  
## <a name="parameters"></a><span data-ttu-id="6e0c0-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="6e0c0-105">Parameters</span></span>  

 `functionId`  
 <span data-ttu-id="6e0c0-106">podczas Identyfikator funkcji, którą rozpoczęło ponowne kompilowanie kompilatora JIT.</span><span class="sxs-lookup"><span data-stu-id="6e0c0-106">[in] The ID of the function that the JIT compiler has started to recompile.</span></span>  
  
 `rejitId`  
 <span data-ttu-id="6e0c0-107">podczas Identyfikator ponownej kompilacji nowej wersji funkcji.</span><span class="sxs-lookup"><span data-stu-id="6e0c0-107">[in] The recompilation ID of the new version of the function.</span></span>  
  
 `fIsSafeToBlock`  
 <span data-ttu-id="6e0c0-108">[w] `true` Aby wskazać, że blokowanie może spowodować, że środowisko uruchomieniowe będzie oczekiwać na zwrócenie przez wątek wywołujący z tego wywołania zwrotnego; `false` , aby wskazać, że blokowanie nie wpłynie na działanie środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="6e0c0-108">[in] `true` to indicate that blocking may cause the runtime to wait for the calling thread to return from this callback; `false` to indicate that blocking will not affect the operation of the runtime.</span></span> <span data-ttu-id="6e0c0-109">Wartość nie jest `true` szkodliwe dla środowiska uruchomieniowego, ale może mieć wpływ na wyniki profilowania.</span><span class="sxs-lookup"><span data-stu-id="6e0c0-109">A value of `true` does not harm the runtime, but can affect the profiling results.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="6e0c0-110">Uwagi</span><span class="sxs-lookup"><span data-stu-id="6e0c0-110">Remarks</span></span>  

 <span data-ttu-id="6e0c0-111">Istnieje możliwość otrzymywania więcej niż jednej pary `ReJITCompilationStarted` i wywołań metod [ReJITCompilationFinished —](icorprofilercallback4-rejitcompilationfinished-method.md) dla każdej funkcji ze względu na sposób, w jaki środowisko uruchomieniowe obsługuje konstruktory klas.</span><span class="sxs-lookup"><span data-stu-id="6e0c0-111">It is possible to receive more than one pair of `ReJITCompilationStarted` and [ReJITCompilationFinished](icorprofilercallback4-rejitcompilationfinished-method.md) method calls for each function because of the way the runtime handles class constructors.</span></span> <span data-ttu-id="6e0c0-112">Na przykład środowisko uruchomieniowe zaczyna ponownie kompilować metodę A, ale Konstruktor klasy dla klasy B musi być uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="6e0c0-112">For example, the runtime starts to recompile method A, but the class constructor for class B needs to be run.</span></span> <span data-ttu-id="6e0c0-113">W związku z tym środowisko uruchomieniowe ponownie kompiluje Konstruktor dla klasy B i uruchamia go.</span><span class="sxs-lookup"><span data-stu-id="6e0c0-113">Therefore, the runtime recompiles the constructor for class B and runs it.</span></span> <span data-ttu-id="6e0c0-114">Gdy Konstruktor jest uruchomiony, wywołuje metodę A, która powoduje ponowne skompilowanie metody A.</span><span class="sxs-lookup"><span data-stu-id="6e0c0-114">While the constructor is running, it makes a call to method A, which causes method A to be recompiled again.</span></span> <span data-ttu-id="6e0c0-115">W tym scenariuszu pierwsza ponowna kompilacja metody A jest zatrzymywana.</span><span class="sxs-lookup"><span data-stu-id="6e0c0-115">In this scenario, the first recompilation of method A is halted.</span></span> <span data-ttu-id="6e0c0-116">Jednak obie próby rekompilacji metody A są raportowane przy użyciu zdarzeń ponownej kompilacji JIT.</span><span class="sxs-lookup"><span data-stu-id="6e0c0-116">However, both attempts to recompile method A are reported with JIT recompilation events.</span></span>  
  
 <span data-ttu-id="6e0c0-117">Profilowani muszą obsługiwać sekwencję wywołań zwrotnych ponownej kompilacji JIT w przypadkach, gdy dwa wątki jednocześnie wydają wywołania zwrotne.</span><span class="sxs-lookup"><span data-stu-id="6e0c0-117">Profilers must support the sequence of JIT recompilation callbacks in cases where two threads are simultaneously making callbacks.</span></span> <span data-ttu-id="6e0c0-118">Na przykład wywołanie Thread A, `ReJITCompilationStarted` jednak przed wywołaniem wątku [ReJITCompilationFinished —](icorprofilercallback4-rejitcompilationfinished-method.md), wątek B wywołuje [ICorProfilerCallback:: ExceptionSearchFunctionEnter —](icorprofilercallback-exceptionsearchfunctionenter-method.md) z identyfikatorem funkcji z `ReJITCompilationStarted` wywołania zwrotnego wątku A. Może się wydawać, że identyfikator funkcji nie powinien jeszcze być prawidłowy, ponieważ wywołanie [ReJITCompilationFinished —](icorprofilercallback4-rejitcompilationfinished-method.md) nie zostało jeszcze odebrane przez profiler.</span><span class="sxs-lookup"><span data-stu-id="6e0c0-118">For example, thread A calls `ReJITCompilationStarted`; however, before thread A calls [ReJITCompilationFinished](icorprofilercallback4-rejitcompilationfinished-method.md), thread B calls [ICorProfilerCallback::ExceptionSearchFunctionEnter](icorprofilercallback-exceptionsearchfunctionenter-method.md) with the function ID from the `ReJITCompilationStarted` callback for thread A. It might appear that the function ID should not yet be valid because a call to [ReJITCompilationFinished](icorprofilercallback4-rejitcompilationfinished-method.md) had not yet been received by the profiler.</span></span> <span data-ttu-id="6e0c0-119">Jednak w tym przypadku identyfikator funkcji jest prawidłowy.</span><span class="sxs-lookup"><span data-stu-id="6e0c0-119">However, in this case, the function ID is valid.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="6e0c0-120">Wymagania</span><span class="sxs-lookup"><span data-stu-id="6e0c0-120">Requirements</span></span>  

 <span data-ttu-id="6e0c0-121">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="6e0c0-121">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="6e0c0-122">**Nagłówek:** CorProf. idl, CorProf. h</span><span class="sxs-lookup"><span data-stu-id="6e0c0-122">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="6e0c0-123">**Biblioteka:** CorGuids. lib</span><span class="sxs-lookup"><span data-stu-id="6e0c0-123">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="6e0c0-124">**.NET Framework wersje:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="6e0c0-124">**.NET Framework Versions:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="6e0c0-125">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="6e0c0-125">See also</span></span>

- [<span data-ttu-id="6e0c0-126">ICorProfilerCallback — Interfejs</span><span class="sxs-lookup"><span data-stu-id="6e0c0-126">ICorProfilerCallback Interface</span></span>](icorprofilercallback-interface.md)
- [<span data-ttu-id="6e0c0-127">ICorProfilerCallback4 — Interfejs</span><span class="sxs-lookup"><span data-stu-id="6e0c0-127">ICorProfilerCallback4 Interface</span></span>](icorprofilercallback4-interface.md)
- [<span data-ttu-id="6e0c0-128">JITCompilationFinished, metoda</span><span class="sxs-lookup"><span data-stu-id="6e0c0-128">JITCompilationFinished Method</span></span>](icorprofilercallback-jitcompilationfinished-method.md)
- [<span data-ttu-id="6e0c0-129">ReJITCompilationFinished, metoda</span><span class="sxs-lookup"><span data-stu-id="6e0c0-129">ReJITCompilationFinished Method</span></span>](icorprofilercallback4-rejitcompilationfinished-method.md)
