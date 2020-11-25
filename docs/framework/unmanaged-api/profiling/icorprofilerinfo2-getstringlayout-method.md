---
title: ICorProfilerInfo2::GetStringLayout — Metoda
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo2.GetStringLayout
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo2::GetStringLayout
helpviewer_keywords:
- GetStringLayout method [.NET Framework profiling]
- ICorProfilerInfo2::GetStringLayout method [.NET Framework profiling]
ms.assetid: 43189651-a535-4803-a1d1-f1c427ace2ca
topic_type:
- apiref
ms.openlocfilehash: d141a78a953d4e0ab922535ad2363c79f2e18ecd
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95727045"
---
# <a name="icorprofilerinfo2getstringlayout-method"></a><span data-ttu-id="37985-102">ICorProfilerInfo2::GetStringLayout — Metoda</span><span class="sxs-lookup"><span data-stu-id="37985-102">ICorProfilerInfo2::GetStringLayout Method</span></span>

<span data-ttu-id="37985-103">Pobiera informacje o układzie obiektu ciągu.</span><span class="sxs-lookup"><span data-stu-id="37985-103">Gets information about the layout of a string object.</span></span> <span data-ttu-id="37985-104">Ta metoda jest przestarzała w .NET Framework 4 i jest zastępowana przez metodę [ICorProfilerInfo3:: GetStringLayout2 —](icorprofilerinfo3-getstringlayout2-method.md) .</span><span class="sxs-lookup"><span data-stu-id="37985-104">This method is deprecated in the .NET Framework 4, and is superseded by the [ICorProfilerInfo3::GetStringLayout2](icorprofilerinfo3-getstringlayout2-method.md) method.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="37985-105">Składnia</span><span class="sxs-lookup"><span data-stu-id="37985-105">Syntax</span></span>  
  
```cpp  
HRESULT GetStringLayout(  
    [out] ULONG *pBufferLengthOffset,  
    [out] ULONG *pStringLengthOffset,  
    [out] ULONG *pBufferOffset);  
```  
  
## <a name="parameters"></a><span data-ttu-id="37985-106">Parametry</span><span class="sxs-lookup"><span data-stu-id="37985-106">Parameters</span></span>  

 `pBufferLengthOffset`  
 <span data-ttu-id="37985-107">określoną Wskaźnik do przesunięcia lokalizacji względem `ObjectID` wskaźnika, który przechowuje długość ciągu.</span><span class="sxs-lookup"><span data-stu-id="37985-107">[out] A pointer to the offset of the location, relative to the `ObjectID` pointer, that stores the length of the string.</span></span> <span data-ttu-id="37985-108">Długość jest przechowywana jako `DWORD` .</span><span class="sxs-lookup"><span data-stu-id="37985-108">The length is stored as a `DWORD`.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="37985-109">Ten parametr zwraca długość samego ciągu, a nie długość buforu.</span><span class="sxs-lookup"><span data-stu-id="37985-109">This parameter returns the length of the string itself, not the length of the buffer.</span></span> <span data-ttu-id="37985-110">Długość buforu nie jest już dostępna.</span><span class="sxs-lookup"><span data-stu-id="37985-110">The length of the buffer is no longer available.</span></span>  
  
 `PStringLengthOffset`  
 <span data-ttu-id="37985-111">określoną Wskaźnik do przesunięcia lokalizacji względem `ObjectID` wskaźnika, w którym jest przechowywana długość ciągu.</span><span class="sxs-lookup"><span data-stu-id="37985-111">[out] A pointer to the offset of the location, relative to the `ObjectID` pointer, that stores the length of the string itself.</span></span> <span data-ttu-id="37985-112">Długość jest przechowywana jako `DWORD` .</span><span class="sxs-lookup"><span data-stu-id="37985-112">The length is stored as a `DWORD`.</span></span>  
  
 `pBufferOffset`  
 <span data-ttu-id="37985-113">określoną Wskaźnik do przesunięcia buforu względem `ObjectID` wskaźnika, który przechowuje ciąg znaków dwubajtowych.</span><span class="sxs-lookup"><span data-stu-id="37985-113">[out] A pointer to the offset of the buffer, relative to the `ObjectID` pointer, that stores the string of wide characters.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="37985-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="37985-114">Remarks</span></span>  

 <span data-ttu-id="37985-115">`GetStringLayout`Metoda pobiera przesunięcia, względem `ObjectID` wskaźnika, lokalizacji, w których są przechowywane następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="37985-115">The `GetStringLayout` method gets the offsets, relative to the `ObjectID` pointer, of the locations in which the following are stored:</span></span>  
  
- <span data-ttu-id="37985-116">Długość buforu ciągu.</span><span class="sxs-lookup"><span data-stu-id="37985-116">The length of the string's buffer.</span></span>  
  
- <span data-ttu-id="37985-117">Długość samego ciągu.</span><span class="sxs-lookup"><span data-stu-id="37985-117">The length of the string itself.</span></span>  
  
- <span data-ttu-id="37985-118">Bufor, który zawiera rzeczywisty ciąg znaków dwubajtowych.</span><span class="sxs-lookup"><span data-stu-id="37985-118">The buffer that contains the actual string of wide characters.</span></span>  
  
 <span data-ttu-id="37985-119">Ciągi mogą być zakończone wartością null.</span><span class="sxs-lookup"><span data-stu-id="37985-119">Strings may be null-terminated.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="37985-120">Wymagania</span><span class="sxs-lookup"><span data-stu-id="37985-120">Requirements</span></span>  

 <span data-ttu-id="37985-121">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="37985-121">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="37985-122">**Nagłówek:** CorProf. idl, CorProf. h</span><span class="sxs-lookup"><span data-stu-id="37985-122">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="37985-123">**Biblioteka:** CorGuids. lib</span><span class="sxs-lookup"><span data-stu-id="37985-123">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="37985-124">**.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="37985-124">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="37985-125">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="37985-125">See also</span></span>

- [<span data-ttu-id="37985-126">ICorProfilerInfo — Interfejs</span><span class="sxs-lookup"><span data-stu-id="37985-126">ICorProfilerInfo Interface</span></span>](icorprofilerinfo-interface.md)
- [<span data-ttu-id="37985-127">ICorProfilerInfo2 — Interfejs</span><span class="sxs-lookup"><span data-stu-id="37985-127">ICorProfilerInfo2 Interface</span></span>](icorprofilerinfo2-interface.md)
