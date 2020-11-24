---
title: ICorProfilerCallback::AppDomainCreationStarted — Metoda
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.AppDomainCreationStarted
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::AppDomainCreationStarted
helpviewer_keywords:
- AppDomainCreationStarted method [.NET Framework profiling]
- ICorProfilerCallback::AppDomainCreationStarted method [.NET Framework profiling]
ms.assetid: b2a8240b-07fe-4859-bb2b-7d3adbfa0a9f
topic_type:
- apiref
ms.openlocfilehash: 901546c80c3bee32afddfa8e8cffbd2b679bc43b
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95685399"
---
# <a name="icorprofilercallbackappdomaincreationstarted-method"></a><span data-ttu-id="f4cf5-102">ICorProfilerCallback::AppDomainCreationStarted — Metoda</span><span class="sxs-lookup"><span data-stu-id="f4cf5-102">ICorProfilerCallback::AppDomainCreationStarted Method</span></span>

<span data-ttu-id="f4cf5-103">Powiadamia profiler o tworzeniu domeny aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-103">Notifies the profiler that an application domain is being created.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="f4cf5-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="f4cf5-104">Syntax</span></span>  
  
```cpp  
HRESULT AppDomainCreationStarted(  
    [in] AppDomainID appDomainId);  
```  
  
## <a name="parameters"></a><span data-ttu-id="f4cf5-105">Parametry</span><span class="sxs-lookup"><span data-stu-id="f4cf5-105">Parameters</span></span>

- `appDomainId`

  <span data-ttu-id="f4cf5-106">\[w programie] identyfikuje domenę, która jest tworzona.</span><span class="sxs-lookup"><span data-stu-id="f4cf5-106">\[in] Identifies the domain which is being created.</span></span>
  
## <a name="remarks"></a><span data-ttu-id="f4cf5-107">Uwagi</span><span class="sxs-lookup"><span data-stu-id="f4cf5-107">Remarks</span></span>  

 <span data-ttu-id="f4cf5-108">Identyfikator nie jest prawidłowy dla żadnego żądania informacji, dopóki nie zostanie wywołana metoda [ICorProfilerCallback:: AppDomainCreationFinished —](icorprofilercallback-appdomaincreationfinished-method.md) .</span><span class="sxs-lookup"><span data-stu-id="f4cf5-108">The ID is not valid for any information request until the [ICorProfilerCallback::AppDomainCreationFinished](icorprofilercallback-appdomaincreationfinished-method.md) method is called.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="f4cf5-109">Wymagania</span><span class="sxs-lookup"><span data-stu-id="f4cf5-109">Requirements</span></span>  

 <span data-ttu-id="f4cf5-110">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="f4cf5-110">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="f4cf5-111">**Nagłówek:** CorProf. idl, CorProf. h</span><span class="sxs-lookup"><span data-stu-id="f4cf5-111">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="f4cf5-112">**Biblioteka:** CorGuids. lib</span><span class="sxs-lookup"><span data-stu-id="f4cf5-112">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="f4cf5-113">**.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="f4cf5-113">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="f4cf5-114">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="f4cf5-114">See also</span></span>

- [<span data-ttu-id="f4cf5-115">ICorProfilerCallback — Interfejs</span><span class="sxs-lookup"><span data-stu-id="f4cf5-115">ICorProfilerCallback Interface</span></span>](icorprofilercallback-interface.md)
