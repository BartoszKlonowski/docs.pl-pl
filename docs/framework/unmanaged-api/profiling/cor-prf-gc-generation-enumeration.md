---
title: COR_PRF_GC_GENERATION — Wyliczenie
ms.date: 03/30/2017
api_name:
- COR_PRF_GC_GENERATION
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- COR_PRF_GC_GENERATION
helpviewer_keywords:
- COR_GC_GENERATION_FLAGS enumeration [.NET Framework profiling]
ms.assetid: d6ece160-26ad-4d39-abd7-05acd6f78c48
topic_type:
- apiref
ms.openlocfilehash: 1d7489e997868a9486f77d176580cee18213a99d
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95718566"
---
# <a name="cor_prf_gc_generation-enumeration"></a><span data-ttu-id="e5552-102">COR_PRF_GC_GENERATION — Wyliczenie</span><span class="sxs-lookup"><span data-stu-id="e5552-102">COR_PRF_GC_GENERATION Enumeration</span></span>

<span data-ttu-id="e5552-103">Identyfikuje Generowanie elementów bezużytecznych.</span><span class="sxs-lookup"><span data-stu-id="e5552-103">Identifies a garbage-collection generation.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="e5552-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="e5552-104">Syntax</span></span>  
  
```cpp  
typedef enum {  
    COR_PRF_GC_GEN_0 = 0,  
    COR_PRF_GC_GEN_1 = 1,  
    COR_PRF_GC_GEN_2 = 2,  
    COR_PRF_GC_LARGE_OBJECT_HEAP = 3,
    COR_PRF_GC_PINNED_OBJECT_HEAP= 4
} COR_PRF_GC_GENERATION;  
```  
  
## <a name="members"></a><span data-ttu-id="e5552-105">Elementy członkowskie</span><span class="sxs-lookup"><span data-stu-id="e5552-105">Members</span></span>  
  
|<span data-ttu-id="e5552-106">Członek</span><span class="sxs-lookup"><span data-stu-id="e5552-106">Member</span></span>|<span data-ttu-id="e5552-107">Opis</span><span class="sxs-lookup"><span data-stu-id="e5552-107">Description</span></span>|  
|------------|-----------------|  
|`COR_PRF_GC_GEN_0`|<span data-ttu-id="e5552-108">Obiekt jest przechowywany jako generacja 0.</span><span class="sxs-lookup"><span data-stu-id="e5552-108">The object is stored as generation 0.</span></span>|  
|`COR_PRF_GC_GEN_1`|<span data-ttu-id="e5552-109">Obiekt jest przechowywany jako generacja 1.</span><span class="sxs-lookup"><span data-stu-id="e5552-109">The object is stored as generation 1.</span></span>|  
|`COR_PRF_GC_GEN_2`|<span data-ttu-id="e5552-110">Obiekt jest przechowywany jako generacja 2.</span><span class="sxs-lookup"><span data-stu-id="e5552-110">The object is stored as generation 2.</span></span>|  
|`COR_PRF_GC_LARGE_OBJECT_HEAP`|<span data-ttu-id="e5552-111">Obiekt jest przechowywany w stercie dużego obiektu.</span><span class="sxs-lookup"><span data-stu-id="e5552-111">The object is stored in the large-object heap.</span></span>|  
|`COR_PRF_GC_PINNED_OBJECT_HEAP`|<span data-ttu-id="e5552-112">Obiekt jest przechowywany w stercie przypiętych obiektów.</span><span class="sxs-lookup"><span data-stu-id="e5552-112">The object is stored in the pinned-object heap.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="e5552-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="e5552-113">Remarks</span></span>  

 <span data-ttu-id="e5552-114">Moduł wyrzucania elementów bezużytecznych zwiększa wydajność zarządzania pamięcią, dzieląc obiekty na generacji na podstawie wieku.</span><span class="sxs-lookup"><span data-stu-id="e5552-114">The garbage collector improves memory management performance by dividing objects into generations based on age.</span></span> <span data-ttu-id="e5552-115">Moduł wyrzucania elementów bezużytecznych obecnie używa trzech generacji, numerowanych 0, 1 i 2 oraz dwóch specjalnych segmentów sterty, jeden dla dużych obiektów i jeden dla przypiętych obiektów.</span><span class="sxs-lookup"><span data-stu-id="e5552-115">The garbage collector currently uses three generations, numbered 0, 1, and 2, and two special heap segments, one for large objects and one for pinned objects.</span></span>
  
 <span data-ttu-id="e5552-116">Obiekty, których rozmiar przekracza wartość progową, są przechowywane w stercie dużego obiektu.</span><span class="sxs-lookup"><span data-stu-id="e5552-116">Objects whose size is larger than a threshold value are stored in the large-object heap.</span></span> <span data-ttu-id="e5552-117">Przypięte obiekty można przydzielić do sterty przypiętych obiektów, aby uniknąć kosztu związanego z przydzieleniem ich do normalnych stert.</span><span class="sxs-lookup"><span data-stu-id="e5552-117">Pinned objects can be allocated to the pinned-object heap to avoid the performance cost of allocating them on the normal heaps.</span></span> <span data-ttu-id="e5552-118">Inne przydziały, które zaczynają się od wygenerowania 0.</span><span class="sxs-lookup"><span data-stu-id="e5552-118">Other allocated objects start out belonging to generation 0.</span></span> <span data-ttu-id="e5552-119">Wszystkie obiekty istniejące po wyrzucaniu elementów bezużytecznych w generacji 0 są podwyższane do generacji 1.</span><span class="sxs-lookup"><span data-stu-id="e5552-119">All objects that exist after garbage collection occurs in generation 0 are promoted to generation 1.</span></span> <span data-ttu-id="e5552-120">Obiekty istniejące po wyrzucaniu elementów bezużytecznych odbywają się w generacji 1.</span><span class="sxs-lookup"><span data-stu-id="e5552-120">Objects that exist after garbage collection occurs in generation 1 move into generation 2.</span></span>  
  
 <span data-ttu-id="e5552-121">Użycie generacji oznacza, że moduł zbierający elementy bezużyteczne musi współpracować z tylko podzbiorem przyznanych obiektów w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="e5552-121">The use of generations means that the garbage collector has to work with only a subset of the allocated objects at any one time.</span></span>  
  
 <span data-ttu-id="e5552-122">`COR_PRF_GC_GENERATION`Wyliczenie jest używane przez strukturę [COR_PRF_GC_GENERATION_RANGE](cor-prf-gc-generation-range-structure.md) .</span><span class="sxs-lookup"><span data-stu-id="e5552-122">The `COR_PRF_GC_GENERATION` enumeration is used by the [COR_PRF_GC_GENERATION_RANGE](cor-prf-gc-generation-range-structure.md) structure.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="e5552-123">Wymagania</span><span class="sxs-lookup"><span data-stu-id="e5552-123">Requirements</span></span>  

 <span data-ttu-id="e5552-124">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="e5552-124">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="e5552-125">**Nagłówek:** CorProf. idl, CorProf. h</span><span class="sxs-lookup"><span data-stu-id="e5552-125">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="e5552-126">**Biblioteka:** CorGuids. lib</span><span class="sxs-lookup"><span data-stu-id="e5552-126">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="e5552-127">**.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="e5552-127">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="e5552-128">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="e5552-128">See also</span></span>

- [<span data-ttu-id="e5552-129">Profilowanie — Wyliczenia</span><span class="sxs-lookup"><span data-stu-id="e5552-129">Profiling Enumerations</span></span>](profiling-enumerations.md)
