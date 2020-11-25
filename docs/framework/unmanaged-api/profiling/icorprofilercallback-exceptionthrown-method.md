---
title: ICorProfilerCallback::ExceptionThrown — Metoda
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.ExceptionThrown
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::ExceptionThrown
helpviewer_keywords:
- ExceptionThrown method [.NET Framework profiling]
- ICorProfilerCallback::ExceptionThrown method [.NET Framework profiling]
ms.assetid: f1a23f3b-ac21-4905-8abf-8ea59f15af53
topic_type:
- apiref
ms.openlocfilehash: 049339f7aecd0ababb74539e60395eff67d1c837
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95723808"
---
# <a name="icorprofilercallbackexceptionthrown-method"></a><span data-ttu-id="674fc-102">ICorProfilerCallback::ExceptionThrown — Metoda</span><span class="sxs-lookup"><span data-stu-id="674fc-102">ICorProfilerCallback::ExceptionThrown Method</span></span>

<span data-ttu-id="674fc-103">Powiadamia profiler o zgłoszonym wyjątku.</span><span class="sxs-lookup"><span data-stu-id="674fc-103">Notifies the profiler that an exception has been thrown.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="674fc-104">Ta funkcja jest wywoływana tylko wtedy, gdy wyjątek osiągnie kod zarządzany.</span><span class="sxs-lookup"><span data-stu-id="674fc-104">This function is called only if the exception reaches managed code.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="674fc-105">Składnia</span><span class="sxs-lookup"><span data-stu-id="674fc-105">Syntax</span></span>  
  
```cpp  
HRESULT ExceptionThrown(  
    [in] ObjectID thrownObjectId);  
```  
  
## <a name="parameters"></a><span data-ttu-id="674fc-106">Parametry</span><span class="sxs-lookup"><span data-stu-id="674fc-106">Parameters</span></span>

- `thrownObjectId`

  <span data-ttu-id="674fc-107">\[in] identyfikator obiektu, który spowodował wyjątek.</span><span class="sxs-lookup"><span data-stu-id="674fc-107">\[in] The ID of the object that caused the exception to be thrown.</span></span>
  
## <a name="remarks"></a><span data-ttu-id="674fc-108">Uwagi</span><span class="sxs-lookup"><span data-stu-id="674fc-108">Remarks</span></span>  

 <span data-ttu-id="674fc-109">Profiler nie powinien blokować swojej implementacji tej metody, ponieważ stos może nie znajdować się w stanie, który zezwala na wyrzucanie elementów bezużytecznych i dlatego nie można włączyć zastępujący elementów bezużytecznych.</span><span class="sxs-lookup"><span data-stu-id="674fc-109">The profiler should not block in its implementation of this method because the stack may not be in a state that allows garbage collection, and therefore preemptive garbage collection cannot be enabled.</span></span> <span data-ttu-id="674fc-110">Jeśli profiler blokuje tutaj i zostanie podjęta próba wyrzucania elementów bezużytecznych, środowisko uruchomieniowe zostanie zablokowane do momentu wywołania zwrotnego.</span><span class="sxs-lookup"><span data-stu-id="674fc-110">If the profiler blocks here and garbage collection is attempted, the runtime will block until this callback returns.</span></span>  
  
 <span data-ttu-id="674fc-111">Implementacja profilera nie powinna być wywoływana w kodzie zarządzanym lub w jakikolwiek sposób spowodować alokację pamięci zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="674fc-111">The profiler's implementation of this method should not call into managed code or in any way cause a managed-memory allocation.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="674fc-112">Wymagania</span><span class="sxs-lookup"><span data-stu-id="674fc-112">Requirements</span></span>  

 <span data-ttu-id="674fc-113">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="674fc-113">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="674fc-114">**Nagłówek:** CorProf. idl, CorProf. h</span><span class="sxs-lookup"><span data-stu-id="674fc-114">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="674fc-115">**Biblioteka:** CorGuids. lib</span><span class="sxs-lookup"><span data-stu-id="674fc-115">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="674fc-116">**.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="674fc-116">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="674fc-117">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="674fc-117">See also</span></span>

- [<span data-ttu-id="674fc-118">ICorProfilerCallback — Interfejs</span><span class="sxs-lookup"><span data-stu-id="674fc-118">ICorProfilerCallback Interface</span></span>](icorprofilercallback-interface.md)
