---
title: ICorProfilerInfo3::EnumJITedFunctions — Metoda
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo3.EnumJITedFunctions Method
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo3::EnumJITedFunctions
helpviewer_keywords:
- ICorProfilerInfo3::EnumJITedFunctions method [.NET Framework profiling]
- EnumJITedFunctions method [.NET Framework profiling]
ms.assetid: e2847a36-f460-45e2-9b6c-b33b008f40d9
topic_type:
- apiref
ms.openlocfilehash: 6227baaead518eae2de5913369b72de1072ac052
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95681499"
---
# <a name="icorprofilerinfo3enumjitedfunctions-method"></a><span data-ttu-id="1698e-102">ICorProfilerInfo3::EnumJITedFunctions — Metoda</span><span class="sxs-lookup"><span data-stu-id="1698e-102">ICorProfilerInfo3::EnumJITedFunctions Method</span></span>

<span data-ttu-id="1698e-103">Zwraca moduł wyliczający dla wszystkich funkcji, które zostały poprzednio skompilowane JIT.</span><span class="sxs-lookup"><span data-stu-id="1698e-103">Returns an enumerator for all functions that were previously JIT-compiled.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="1698e-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="1698e-104">Syntax</span></span>  
  
```cpp  
HRESULT EnumJITedFunctions([out] ICorProfilerFunctionEnum** ppEnum);  
```  
  
## <a name="parameters"></a><span data-ttu-id="1698e-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="1698e-105">Parameters</span></span>  

 `ppEnum`  
 <span data-ttu-id="1698e-106">określoną Wskaźnik do modułu wyliczającego [ICorProfilerFunctionEnum](icorprofilerfunctionenum-interface.md) .</span><span class="sxs-lookup"><span data-stu-id="1698e-106">[out] A pointer to the [ICorProfilerFunctionEnum](icorprofilerfunctionenum-interface.md) enumerator.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="1698e-107">Uwagi</span><span class="sxs-lookup"><span data-stu-id="1698e-107">Remarks</span></span>  

 <span data-ttu-id="1698e-108">Ta metoda może nakładać się na `JITCompilation` wywołania zwrotne, takie jak Metoda [ICorProfilerCallback:: JITCompilationStarted](icorprofilercallback-jitcompilationstarted-method.md) .</span><span class="sxs-lookup"><span data-stu-id="1698e-108">This method may overlap with `JITCompilation` callbacks such as the [ICorProfilerCallback::JITCompilationStarted](icorprofilercallback-jitcompilationstarted-method.md) method.</span></span> <span data-ttu-id="1698e-109">Moduł wyliczający zwrócony przez tę metodę nie zawiera funkcji ładowanych z obrazów natywnych generowanych z Ngen.exe.</span><span class="sxs-lookup"><span data-stu-id="1698e-109">The enumerator returned by this method does not include functions that are loaded from native images generated with Ngen.exe.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="1698e-110">Zwrócone Wyliczenie zawiera tylko wartość "0" dla wartości `COR_PRF_FUNCTION::reJitId` pola.</span><span class="sxs-lookup"><span data-stu-id="1698e-110">The returned enumeration includes only "0" for the value of the `COR_PRF_FUNCTION::reJitId` field.</span></span>  <span data-ttu-id="1698e-111">Jeśli wymagane są prawidłowe `COR_PRF_FUNCTION::reJitId` wartości, należy użyć metody [ICorProfilerInfo4:: EnumJITedFunctions2 —](icorprofilerinfo4-enumjitedfunctions2-method.md) .</span><span class="sxs-lookup"><span data-stu-id="1698e-111">If you require valid `COR_PRF_FUNCTION::reJitId` values, use the [ICorProfilerInfo4::EnumJITedFunctions2](icorprofilerinfo4-enumjitedfunctions2-method.md) method.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="1698e-112">Wymagania</span><span class="sxs-lookup"><span data-stu-id="1698e-112">Requirements</span></span>  

 <span data-ttu-id="1698e-113">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="1698e-113">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="1698e-114">**Nagłówek:** CorProf. idl, CorProf. h</span><span class="sxs-lookup"><span data-stu-id="1698e-114">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="1698e-115">**Biblioteka:** CorGuids. lib</span><span class="sxs-lookup"><span data-stu-id="1698e-115">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="1698e-116">**.NET Framework wersje:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="1698e-116">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="1698e-117">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="1698e-117">See also</span></span>

- [<span data-ttu-id="1698e-118">ICorProfilerInfo3 — Interfejs</span><span class="sxs-lookup"><span data-stu-id="1698e-118">ICorProfilerInfo3 Interface</span></span>](icorprofilerinfo3-interface.md)
- [<span data-ttu-id="1698e-119">Interfejsy profilowania</span><span class="sxs-lookup"><span data-stu-id="1698e-119">Profiling Interfaces</span></span>](profiling-interfaces.md)
- [<span data-ttu-id="1698e-120">Profilowanie</span><span class="sxs-lookup"><span data-stu-id="1698e-120">Profiling</span></span>](index.md)
