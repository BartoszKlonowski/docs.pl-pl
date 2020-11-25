---
title: ICorProfilerCallback::Initialize — Metoda
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.Initialize
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::Initialize
helpviewer_keywords:
- Initialize method, ICorProfilerCallback interface [.NET Framework profiling]
- ICorProfilerCallback::Initialize method [.NET Framework profiling]
ms.assetid: dc5fab2a-4b45-4b12-8727-b89c9915f23e
topic_type:
- apiref
ms.openlocfilehash: 26df1599af247bd08d3702d4ef3c5aa2f648620c
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95720376"
---
# <a name="icorprofilercallbackinitialize-method"></a><span data-ttu-id="83c6f-102">ICorProfilerCallback::Initialize — Metoda</span><span class="sxs-lookup"><span data-stu-id="83c6f-102">ICorProfilerCallback::Initialize Method</span></span>

<span data-ttu-id="83c6f-103">Wywołuje się, by zainicjować profiler kodu za każdym razem, gdy jest uruchomiona nowa aplikacja środowiska uruchomieniowego języka wspólnego (CLR).</span><span class="sxs-lookup"><span data-stu-id="83c6f-103">Called to initialize the code profiler whenever a new common language runtime (CLR) application is started.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="83c6f-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="83c6f-104">Syntax</span></span>  
  
```cpp  
HRESULT Initialize(  
    [in] IUnknown     *pICorProfilerInfoUnk);  
```  
  
## <a name="parameters"></a><span data-ttu-id="83c6f-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="83c6f-105">Parameters</span></span>

- `pICorProfilerInfoUnk`

  <span data-ttu-id="83c6f-106">\[in) wskaźnik do interfejsu [IUnknown](/cpp/atl/iunknown) , który profiler musi wykonać zapytanie o wskaźnik interfejsu [ICorProfilerInfo](icorprofilerinfo-interface.md) .</span><span class="sxs-lookup"><span data-stu-id="83c6f-106">\[in] Pointer to an [IUnknown](/cpp/atl/iunknown) interface that the profiler must query for an [ICorProfilerInfo](icorprofilerinfo-interface.md) interface pointer.</span></span>  

## <a name="remarks"></a><span data-ttu-id="83c6f-107">Uwagi</span><span class="sxs-lookup"><span data-stu-id="83c6f-107">Remarks</span></span>  

 <span data-ttu-id="83c6f-108">`Initialize`Wywołanie jest jedyną możliwością, aby włączyć (lub wyłączyć) wywołania zwrotne, które są niezmienne.</span><span class="sxs-lookup"><span data-stu-id="83c6f-108">The `Initialize` call is the only opportunity to enable (or disable) callbacks that are immutable.</span></span> <span data-ttu-id="83c6f-109">Po włączeniu wywołania zwrotnego przez `Initialize` wywołanie nie można go wyłączyć później za pomocą [ICorProfilerInfo:: SetEventMask](icorprofilerinfo-seteventmask-method.md).</span><span class="sxs-lookup"><span data-stu-id="83c6f-109">Once a callback is enabled by the `Initialize` call, it cannot be disabled later using [ICorProfilerInfo::SetEventMask](icorprofilerinfo-seteventmask-method.md).</span></span> <span data-ttu-id="83c6f-110">COR_PRF_MONITOR_IMMUTABLE wartość wyliczenia [COR_PRF_MONITOR](cor-prf-monitor-enumeration.md) wskazuje, które zdarzenia są niezmienne.</span><span class="sxs-lookup"><span data-stu-id="83c6f-110">The COR_PRF_MONITOR_IMMUTABLE value of the [COR_PRF_MONITOR](cor-prf-monitor-enumeration.md) enumeration indicates which events are immutable.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="83c6f-111">Wymagania</span><span class="sxs-lookup"><span data-stu-id="83c6f-111">Requirements</span></span>  

 <span data-ttu-id="83c6f-112">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="83c6f-112">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="83c6f-113">**Nagłówek:** CorProf. idl, CorProf. h</span><span class="sxs-lookup"><span data-stu-id="83c6f-113">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="83c6f-114">**Biblioteka:** CorGuids. lib</span><span class="sxs-lookup"><span data-stu-id="83c6f-114">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="83c6f-115">**.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="83c6f-115">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="83c6f-116">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="83c6f-116">See also</span></span>

- [<span data-ttu-id="83c6f-117">ICorProfilerCallback — Interfejs</span><span class="sxs-lookup"><span data-stu-id="83c6f-117">ICorProfilerCallback Interface</span></span>](icorprofilercallback-interface.md)
- [<span data-ttu-id="83c6f-118">Shutdown, metoda</span><span class="sxs-lookup"><span data-stu-id="83c6f-118">Shutdown Method</span></span>](icorprofilercallback-shutdown-method.md)
