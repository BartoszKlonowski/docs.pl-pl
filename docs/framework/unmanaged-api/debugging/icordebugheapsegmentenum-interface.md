---
title: ICorDebugHeapSegmentEnum — Interfejs
ms.date: 03/30/2017
api_name:
- ICorDebugHealRegionEnum
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugHeapSegmentEnum
helpviewer_keywords:
- ICorDebugHeapSegmentEnum interface [.NET Framework debugging]
ms.assetid: 20fc1b9d-e228-4107-bd76-53934c1724b9
topic_type:
- apiref
ms.openlocfilehash: 42126d15c64175f35bba89a1ab6abacc64128012
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95704633"
---
# <a name="icordebugheapsegmentenum-interface"></a><span data-ttu-id="e497e-102">ICorDebugHeapSegmentEnum — Interfejs</span><span class="sxs-lookup"><span data-stu-id="e497e-102">ICorDebugHeapSegmentEnum Interface</span></span>

<span data-ttu-id="e497e-103">Zawiera moduł wyliczający dla obszarów pamięci zarządzanej sterty.</span><span class="sxs-lookup"><span data-stu-id="e497e-103">Provides an enumerator for the memory regions of the managed heap.</span></span> <span data-ttu-id="e497e-104">Ten interfejs jest podklasą interfejsu ICorDebugEnum.</span><span class="sxs-lookup"><span data-stu-id="e497e-104">This interface is a subclass of the ICorDebugEnum interface.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="e497e-105">Metody</span><span class="sxs-lookup"><span data-stu-id="e497e-105">Methods</span></span>  
  
|<span data-ttu-id="e497e-106">Metoda</span><span class="sxs-lookup"><span data-stu-id="e497e-106">Method</span></span>|<span data-ttu-id="e497e-107">Opis</span><span class="sxs-lookup"><span data-stu-id="e497e-107">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="e497e-108">Next, metoda</span><span class="sxs-lookup"><span data-stu-id="e497e-108">Next Method</span></span>](icordebugheapsegmentenum-next-method.md)|<span data-ttu-id="e497e-109">Pobiera określoną liczbę wystąpień [COR_SEGMENT](cor-segment-structure.md) , które zawierają informacje o regionach zarządzanej sterty.</span><span class="sxs-lookup"><span data-stu-id="e497e-109">Gets the specified number of [COR_SEGMENT](cor-segment-structure.md) instances that contain information about regions of the managed heap.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="e497e-110">Uwagi</span><span class="sxs-lookup"><span data-stu-id="e497e-110">Remarks</span></span>  

 <span data-ttu-id="e497e-111">`ICorDebugHeapSegmentEnum`Interfejs implementuje interfejs ICorDebugEnum.</span><span class="sxs-lookup"><span data-stu-id="e497e-111">The `ICorDebugHeapSegmentEnum` interface implements the ICorDebugEnum interface.</span></span>  
  
 <span data-ttu-id="e497e-112">`ICorDebugHeapSegmentEnum`Wystąpienie jest wypełniane wystąpieniami [COR_SEGMENT](cor-segment-structure.md) , wywołując metodę [ICorDebugProcess5:: EnumerateHeapRegions —](icordebugprocess5-enumerateheapregions-method.md) .</span><span class="sxs-lookup"><span data-stu-id="e497e-112">An `ICorDebugHeapSegmentEnum` instance is populated with [COR_SEGMENT](cor-segment-structure.md) instances by calling the [ICorDebugProcess5::EnumerateHeapRegions](icordebugprocess5-enumerateheapregions-method.md) method.</span></span> <span data-ttu-id="e497e-113">[COR_SEGMENT](cor-segment-structure.md) obiektów w kolekcji można wyliczyć, wywołując metodę [ICorDebugHeapSegmentEnum:: Next](icordebugheapsegmentenum-next-method.md) .</span><span class="sxs-lookup"><span data-stu-id="e497e-113">The [COR_SEGMENT](cor-segment-structure.md) objects in the collection can be enumerated by calling the [ICorDebugHeapSegmentEnum::Next](icordebugheapsegmentenum-next-method.md) method.</span></span>  
  
 <span data-ttu-id="e497e-114">`ICorDebugHeapSegmentEnum`Obiekt kolekcji wylicza wszystkie obszary pamięci, które mogą zawierać obiekty zarządzane, ale nie gwarantuje, że obiekty zarządzane rzeczywiście znajdują się w tych regionach.</span><span class="sxs-lookup"><span data-stu-id="e497e-114">An `ICorDebugHeapSegmentEnum` collection object enumerates all memory regions that may contain managed objects, but it does not guarantee that managed objects actually reside in those regions.</span></span> <span data-ttu-id="e497e-115">Może zawierać informacje dotyczące pustych lub zarezerwowanych regionów pamięci.</span><span class="sxs-lookup"><span data-stu-id="e497e-115">It may include information about empty or reserved memory regions.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="e497e-116">Wymagania</span><span class="sxs-lookup"><span data-stu-id="e497e-116">Requirements</span></span>  

 <span data-ttu-id="e497e-117">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="e497e-117">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="e497e-118">**Nagłówek:** CorDebug. idl, CorDebug. h</span><span class="sxs-lookup"><span data-stu-id="e497e-118">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="e497e-119">**Biblioteka:** CorGuids. lib</span><span class="sxs-lookup"><span data-stu-id="e497e-119">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="e497e-120">**.NET Framework wersje:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="e497e-120">**.NET Framework Versions:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="e497e-121">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="e497e-121">See also</span></span>

- [<span data-ttu-id="e497e-122">Debugowanie — Interfejsy</span><span class="sxs-lookup"><span data-stu-id="e497e-122">Debugging Interfaces</span></span>](debugging-interfaces.md)
