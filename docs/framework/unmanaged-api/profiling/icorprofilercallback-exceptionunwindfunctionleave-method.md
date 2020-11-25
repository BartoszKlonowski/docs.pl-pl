---
title: ICorProfilerCallback::ExceptionUnwindFunctionLeave — Metoda
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.ExceptionUnwindFunctionLeave
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::ExceptionUnwindFunctionLeave
helpviewer_keywords:
- ICorProfilerCallback::ExceptionUnwindFunctionLeave method [.NET Framework profiling]
- ExceptionUnwindFunctionLeave method [.NET Framework profiling]
ms.assetid: ebaad1d5-ee0a-4cb0-96bc-8ba5d371b747
topic_type:
- apiref
ms.openlocfilehash: 9f88a3fde7d7cb5941e3a7f44a7d94056a959ab8
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95733922"
---
# <a name="icorprofilercallbackexceptionunwindfunctionleave-method"></a><span data-ttu-id="38b67-102">ICorProfilerCallback::ExceptionUnwindFunctionLeave — Metoda</span><span class="sxs-lookup"><span data-stu-id="38b67-102">ICorProfilerCallback::ExceptionUnwindFunctionLeave Method</span></span>

<span data-ttu-id="38b67-103">Powiadamia profiler, że faza unwind dla obsługi wyjątków zakończyła odwinięcie funkcji.</span><span class="sxs-lookup"><span data-stu-id="38b67-103">Notifies the profiler that the unwind phase of exception handling has finished unwinding a function.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="38b67-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="38b67-104">Syntax</span></span>  
  
```cpp  
HRESULT ExceptionUnwindFunctionLeave();  
```  
  
## <a name="remarks"></a><span data-ttu-id="38b67-105">Uwagi</span><span class="sxs-lookup"><span data-stu-id="38b67-105">Remarks</span></span>  

 <span data-ttu-id="38b67-106">Po `ExceptionUnwindFunctionLeave` wywołaniu metody wystąpienie funkcji i jego dane stosu są usuwane ze stosu.</span><span class="sxs-lookup"><span data-stu-id="38b67-106">When the `ExceptionUnwindFunctionLeave` method is called, the function instance and its stack data are removed from the stack.</span></span>  
  
 <span data-ttu-id="38b67-107">Profiler nie powinien blokować tego wywołania, ponieważ stos może nie znajdować się w stanie, który zezwala na wyrzucanie elementów bezużytecznych, a tym samym nie można włączyć przerzucania elementów bezużytecznych.</span><span class="sxs-lookup"><span data-stu-id="38b67-107">The profiler should not block during this call because the stack may not be in a state that allows garbage collection, and therefore preemptive garbage collection cannot be enabled.</span></span> <span data-ttu-id="38b67-108">Jeśli profiler blokuje się w tym miejscu i podjęto próbę wyrzucania elementów bezużytecznych, środowisko uruchomieniowe zostanie zablokowane do momentu wywołania zwrotnego.</span><span class="sxs-lookup"><span data-stu-id="38b67-108">If the profiler blocks here and a garbage collection is attempted, the runtime will block until this callback returns.</span></span>  
  
 <span data-ttu-id="38b67-109">Ponadto w trakcie tego wywołania Profiler nie może wywołać kodu zarządzanego lub w jakikolwiek sposób spowodować alokację pamięci zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="38b67-109">Also, during this call, the profiler must not call into managed code or in any way cause a managed-memory allocation.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="38b67-110">Wymagania</span><span class="sxs-lookup"><span data-stu-id="38b67-110">Requirements</span></span>  

 <span data-ttu-id="38b67-111">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="38b67-111">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="38b67-112">**Nagłówek:** CorProf. idl, CorProf. h</span><span class="sxs-lookup"><span data-stu-id="38b67-112">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="38b67-113">**Biblioteka:** CorGuids. lib</span><span class="sxs-lookup"><span data-stu-id="38b67-113">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="38b67-114">**.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="38b67-114">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="38b67-115">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="38b67-115">See also</span></span>

- [<span data-ttu-id="38b67-116">ICorProfilerCallback — Interfejs</span><span class="sxs-lookup"><span data-stu-id="38b67-116">ICorProfilerCallback Interface</span></span>](icorprofilercallback-interface.md)
- [<span data-ttu-id="38b67-117">ExceptionUnwindFunctionEnter, metoda</span><span class="sxs-lookup"><span data-stu-id="38b67-117">ExceptionUnwindFunctionEnter Method</span></span>](icorprofilercallback-exceptionunwindfunctionenter-method.md)
