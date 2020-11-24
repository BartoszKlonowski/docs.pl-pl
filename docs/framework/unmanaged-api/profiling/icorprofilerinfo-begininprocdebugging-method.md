---
title: ICorProfilerInfo::BeginInprocDebugging — Metoda
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.BeginInprocDebugging
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::BeginInprocDebugging
helpviewer_keywords:
- BeginInprocDebugging method [.NET Framework profiling]
- ICorProfilerInfo::BeginInprocDebugging method [.NET Framework profiling]
ms.assetid: c5c82c69-99f8-4447-aee0-42cca0a5eb5c
topic_type:
- apiref
ms.openlocfilehash: 3f56c3faa10eb05896936a37b0094797b0b6e2b9
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95669175"
---
# <a name="icorprofilerinfobegininprocdebugging-method"></a><span data-ttu-id="fe38b-102">ICorProfilerInfo::BeginInprocDebugging — Metoda</span><span class="sxs-lookup"><span data-stu-id="fe38b-102">ICorProfilerInfo::BeginInprocDebugging Method</span></span>

<span data-ttu-id="fe38b-103">Inicjuje obsługę debugowania w procesie.</span><span class="sxs-lookup"><span data-stu-id="fe38b-103">Initializes in-process debugging support.</span></span> <span data-ttu-id="fe38b-104">Ta metoda jest przestarzała w .NET Framework w wersji 2,0.</span><span class="sxs-lookup"><span data-stu-id="fe38b-104">This method is obsolete in the .NET Framework version 2.0.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="fe38b-105">Składnia</span><span class="sxs-lookup"><span data-stu-id="fe38b-105">Syntax</span></span>  
  
```cpp  
HRESULT BeginInprocDebugging(  
    [in]  BOOL   fThisThreadOnly,  
    [out] DWORD *pdwProfilerContext);  
```  
  
## <a name="parameters"></a><span data-ttu-id="fe38b-106">Parametry</span><span class="sxs-lookup"><span data-stu-id="fe38b-106">Parameters</span></span>  

 `fThisThreadOnly`  
 <span data-ttu-id="fe38b-107">podczas Ustaw tę wartość na `true` , aby zainicjować obsługę debugowania tylko dla bieżącego wątku; ustaw ją na `false` w celu zainicjowania obsługi debugowania dla wszystkich wątków.</span><span class="sxs-lookup"><span data-stu-id="fe38b-107">[in] Set this value to `true` to initialize debugging support for only the current thread; set it to `false` to initialize debugging support for all threads.</span></span>  
  
 `pdwProfilerContext`  
 <span data-ttu-id="fe38b-108">określoną Wskaźnik do zwracanej wartości, która identyfikuje sesję debugowania.</span><span class="sxs-lookup"><span data-stu-id="fe38b-108">[out] The pointer to a returned value that identifies the debugging session.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="fe38b-109">Uwagi</span><span class="sxs-lookup"><span data-stu-id="fe38b-109">Remarks</span></span>  

 <span data-ttu-id="fe38b-110">Usługi debugowania CLR obsługiwały ograniczone debugowanie w procesie w .NET Framework wersje 1,0 i 1,1.</span><span class="sxs-lookup"><span data-stu-id="fe38b-110">The CLR debugging services supported limited in-process debugging in the .NET Framework versions 1.0 and 1.1.</span></span> <span data-ttu-id="fe38b-111">Debugowanie w procesie umożliwia profilerowi użycie części inspekcji interfejsu API debugowania.</span><span class="sxs-lookup"><span data-stu-id="fe38b-111">In-process debugging enabled a profiler to use the inspection portions of the debugging API.</span></span> <span data-ttu-id="fe38b-112">Jednak ze względu na Opinie klientów, debugowanie w procesie zostało usunięte z .NET Framework w wersji 2,0 i zastąpione zestawem funkcji, który jest bardziej aktualny z profilem API profilowania.</span><span class="sxs-lookup"><span data-stu-id="fe38b-112">However, due to customer feedback, in-process debugging has been removed from the .NET Framework in version 2.0, and replaced with a set of functionality that is more in line with the profiling API.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="fe38b-113">Wymagania</span><span class="sxs-lookup"><span data-stu-id="fe38b-113">Requirements</span></span>  

 <span data-ttu-id="fe38b-114">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="fe38b-114">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="fe38b-115">**Nagłówek:** CorProf. idl, CorProf. h</span><span class="sxs-lookup"><span data-stu-id="fe38b-115">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="fe38b-116">**Biblioteka:** CorGuids. lib</span><span class="sxs-lookup"><span data-stu-id="fe38b-116">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="fe38b-117">**Wersja .NET Framework:** 1,0</span><span class="sxs-lookup"><span data-stu-id="fe38b-117">**.NET Framework Version:** 1.0</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="fe38b-118">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="fe38b-118">See also</span></span>

- [<span data-ttu-id="fe38b-119">ICorProfilerInfo — Interfejs</span><span class="sxs-lookup"><span data-stu-id="fe38b-119">ICorProfilerInfo Interface</span></span>](icorprofilerinfo-interface.md)
