---
title: ICorProfilerInfo::GetHandleFromThread — Metoda
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.GetHandleFromThread
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::GetHandleFromThread
helpviewer_keywords:
- GetHandleFromThread method [.NET Framework profiling]
- ICorProfilerInfo::GetHandleFromThread method [.NET Framework profiling]
ms.assetid: 36cdc9f5-7579-4cd2-aa36-fc05c741584c
topic_type:
- apiref
ms.openlocfilehash: 94c2c6e01e4188f1fa13c3b6a9f638d4b79a502f
ms.sourcegitcommit: 4b79862c5b41fbd86cf38f926f6a49516059f6f2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/18/2020
ms.locfileid: "97678189"
---
# <a name="icorprofilerinfogethandlefromthread-method"></a><span data-ttu-id="54ac9-102">ICorProfilerInfo::GetHandleFromThread — Metoda</span><span class="sxs-lookup"><span data-stu-id="54ac9-102">ICorProfilerInfo::GetHandleFromThread Method</span></span>

<span data-ttu-id="54ac9-103">Mapuje identyfikator wątku na dojście wątku Win32.</span><span class="sxs-lookup"><span data-stu-id="54ac9-103">Maps the ID of a thread to a Win32 thread handle.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="54ac9-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="54ac9-104">Syntax</span></span>  
  
```cpp  
HRESULT GetHandleFromThread(  
    [in]  ThreadID threadId,  
    [out] HANDLE  *phThread);  
```  
  
## <a name="parameters"></a><span data-ttu-id="54ac9-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="54ac9-105">Parameters</span></span>  

 `threadId`  
 <span data-ttu-id="54ac9-106">podczas Identyfikator wątku, który ma zostać zamapowany.</span><span class="sxs-lookup"><span data-stu-id="54ac9-106">[in] The thread ID to be mapped.</span></span>  
  
 `phThread`  
 <span data-ttu-id="54ac9-107">określoną Wskaźnik do dojścia do wątku Win32.</span><span class="sxs-lookup"><span data-stu-id="54ac9-107">[out] A pointer to a Win32 thread handle.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="54ac9-108">Uwagi</span><span class="sxs-lookup"><span data-stu-id="54ac9-108">Remarks</span></span>  

 <span data-ttu-id="54ac9-109">Profiler musi wywołać `DuplicateHandle` funkcję Win32 w uchwycie przed użyciem go.</span><span class="sxs-lookup"><span data-stu-id="54ac9-109">The profiler must call the Win32 `DuplicateHandle` function on the handle before using it.</span></span>  

 <span data-ttu-id="54ac9-110">Dojście zwrócone przez tę metodę jest własnością środowiska uruchomieniowego, a Profiler nie powinien go zamknąć.</span><span class="sxs-lookup"><span data-stu-id="54ac9-110">The handle returned from this method is owned by the runtime and the profiler should never close it.</span></span>
  
## <a name="requirements"></a><span data-ttu-id="54ac9-111">Wymagania</span><span class="sxs-lookup"><span data-stu-id="54ac9-111">Requirements</span></span>  

 <span data-ttu-id="54ac9-112">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="54ac9-112">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="54ac9-113">**Nagłówek:** CorProf. idl, CorProf. h</span><span class="sxs-lookup"><span data-stu-id="54ac9-113">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="54ac9-114">**Biblioteka:** CorGuids. lib</span><span class="sxs-lookup"><span data-stu-id="54ac9-114">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="54ac9-115">**.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="54ac9-115">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="54ac9-116">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="54ac9-116">See also</span></span>

- [<span data-ttu-id="54ac9-117">ICorProfilerInfo — Interfejs</span><span class="sxs-lookup"><span data-stu-id="54ac9-117">ICorProfilerInfo Interface</span></span>](icorprofilerinfo-interface.md)
