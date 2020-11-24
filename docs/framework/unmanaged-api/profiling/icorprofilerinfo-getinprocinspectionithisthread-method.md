---
title: ICorProfilerInfo::GetInprocInspectionIThisThread — Metoda
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.GetInprocInspectionIThisThread
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::GetInprocInspectionIThisThread
helpviewer_keywords:
- ICorProfilerInfo::GetInprocInspectionIThisThread method [.NET Framework profiling]
- GetInprocInspectionIThisThread method [.NET Framework profiling]
ms.assetid: badddccd-f85c-416e-9f0f-419eab2c9d42
topic_type:
- apiref
ms.openlocfilehash: 8daa84e3abbbc64c9a48d8957b4ad9c6756d0d8b
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95682084"
---
# <a name="icorprofilerinfogetinprocinspectionithisthread-method"></a><span data-ttu-id="8830c-102">ICorProfilerInfo::GetInprocInspectionIThisThread — Metoda</span><span class="sxs-lookup"><span data-stu-id="8830c-102">ICorProfilerInfo::GetInprocInspectionIThisThread Method</span></span>

<span data-ttu-id="8830c-103">Pobiera obiekt, który może być badany dla interfejsu ICorDebugThread.</span><span class="sxs-lookup"><span data-stu-id="8830c-103">Gets an object that can be queried for the ICorDebugThread interface.</span></span> <span data-ttu-id="8830c-104">Ta metoda jest przestarzała w .NET Framework w wersji 2,0.</span><span class="sxs-lookup"><span data-stu-id="8830c-104">This method is obsolete in the .NET Framework version 2.0.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="8830c-105">Składnia</span><span class="sxs-lookup"><span data-stu-id="8830c-105">Syntax</span></span>  
  
```cpp  
HRESULT GetInprocInspectionIThisThread(  
    [out] IUnknown **ppicd);  
```  
  
## <a name="parameters"></a><span data-ttu-id="8830c-106">Parametry</span><span class="sxs-lookup"><span data-stu-id="8830c-106">Parameters</span></span>  

 `ppicd`  
 <span data-ttu-id="8830c-107">Obiekt [out](/cpp/atl/iunknown) , który może być badany dla `ICorDebugThread` interfejsu.</span><span class="sxs-lookup"><span data-stu-id="8830c-107">[out](/cpp/atl/iunknown) object that can be queried for the `ICorDebugThread` interface.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="8830c-108">Uwagi</span><span class="sxs-lookup"><span data-stu-id="8830c-108">Remarks</span></span>  

 <span data-ttu-id="8830c-109">Usługi debugowania środowiska uruchomieniowego języka wspólnego (CLR) obsługują ograniczone debugowanie w procesie w .NET Framework w wersji 1,0.</span><span class="sxs-lookup"><span data-stu-id="8830c-109">The common language runtime (CLR) debugging services supported limited in-process debugging in the .NET Framework version 1.0.</span></span> <span data-ttu-id="8830c-110">Debugowanie w procesie umożliwia profilerowi użycie części inspekcji interfejsu API debugowania.</span><span class="sxs-lookup"><span data-stu-id="8830c-110">In-process debugging enabled a profiler to use the inspection portions of the debugging API.</span></span> <span data-ttu-id="8830c-111">W wyniku opinii klientów, debugowanie w procesie zostało usunięte z .NET Framework w wersji 2,0 i zastąpione zestawem funkcji, który jest bardziej aktualny z profilem API profilowania.</span><span class="sxs-lookup"><span data-stu-id="8830c-111">As a result of customer feedback, in-process debugging has been removed from the .NET Framework in version 2.0, and replaced with a set of functionality that is more in line with the profiling API.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="8830c-112">Wymagania</span><span class="sxs-lookup"><span data-stu-id="8830c-112">Requirements</span></span>  

 <span data-ttu-id="8830c-113">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="8830c-113">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="8830c-114">**Nagłówek:** CorProf. idl, CorProf. h</span><span class="sxs-lookup"><span data-stu-id="8830c-114">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="8830c-115">**Biblioteka:** CorGuids. lib</span><span class="sxs-lookup"><span data-stu-id="8830c-115">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="8830c-116">**Wersja .NET Framework:** 1,0</span><span class="sxs-lookup"><span data-stu-id="8830c-116">**.NET Framework Version:** 1.0</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="8830c-117">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="8830c-117">See also</span></span>

- [<span data-ttu-id="8830c-118">ICorProfilerInfo — Interfejs</span><span class="sxs-lookup"><span data-stu-id="8830c-118">ICorProfilerInfo Interface</span></span>](icorprofilerinfo-interface.md)
