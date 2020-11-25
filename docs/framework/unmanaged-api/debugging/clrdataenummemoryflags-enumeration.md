---
title: CLRDataEnumMemoryFlags — Wyliczenie
ms.date: 03/30/2017
api_name:
- CLRDataEnumMemoryFlags
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CLRDataEnumMemoryFlags
helpviewer_keywords:
- CLRDataEnumMemoryFlags enumeration [.NET Framework debugging]
ms.assetid: e249f9fc-e24a-4506-903c-92781f6eab7c
topic_type:
- apiref
ms.openlocfilehash: 9a82162023fa05e85fc9bbeb16961f2aafd9a4ec
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95729801"
---
# <a name="clrdataenummemoryflags-enumeration"></a><span data-ttu-id="abbd6-102">CLRDataEnumMemoryFlags — Wyliczenie</span><span class="sxs-lookup"><span data-stu-id="abbd6-102">CLRDataEnumMemoryFlags Enumeration</span></span>

<span data-ttu-id="abbd6-103">Wskazuje, które regiony pamięci są wywoływane przez wywołanie metody [ICLRDataEnumMemoryRegions:: EnumMemoryRegions —](iclrdataenummemoryregions-enummemoryregions-method.md) .</span><span class="sxs-lookup"><span data-stu-id="abbd6-103">Indicates which memory regions a call to the [ICLRDataEnumMemoryRegions::EnumMemoryRegions](iclrdataenummemoryregions-enummemoryregions-method.md) method should include.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="abbd6-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="abbd6-104">Syntax</span></span>  
  
```cpp  
typedef enum CLRDataEnumMemoryFlags {  
    CLRDATA_ENUM_MEM_DEFAULT  = 0x0,  
    CLRDATA_ENUM_MEM_MINI     = CLRDATA_ENUM_MEM_DEFAULT,  
    CLRDATA_ENUM_MEM_HEAP     = 0x1  
} CLRDataEnumMemoryFlags;  
```  
  
## <a name="members"></a><span data-ttu-id="abbd6-105">Elementy członkowskie</span><span class="sxs-lookup"><span data-stu-id="abbd6-105">Members</span></span>  
  
|<span data-ttu-id="abbd6-106">Członek</span><span class="sxs-lookup"><span data-stu-id="abbd6-106">Member</span></span>|<span data-ttu-id="abbd6-107">Opis</span><span class="sxs-lookup"><span data-stu-id="abbd6-107">Description</span></span>|  
|------------|-----------------|  
|`CLRDATA_ENUM_MEM_DEFAULT`|<span data-ttu-id="abbd6-108">Minizrzutu, czyli zrzut pamięci rozrzedzonej.</span><span class="sxs-lookup"><span data-stu-id="abbd6-108">A minidump, that is, a sparse memory dump.</span></span>|  
|`CLRDATA_ENUM_MEM_HEAP`|<span data-ttu-id="abbd6-109">Pełny zrzut sterty.</span><span class="sxs-lookup"><span data-stu-id="abbd6-109">A full heap dump.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="abbd6-110">Wymagania</span><span class="sxs-lookup"><span data-stu-id="abbd6-110">Requirements</span></span>  

 <span data-ttu-id="abbd6-111">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="abbd6-111">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="abbd6-112">**Nagłówek:** ClrData. idl, ClrData. h</span><span class="sxs-lookup"><span data-stu-id="abbd6-112">**Header:** ClrData.idl, ClrData.h</span></span>  
  
 <span data-ttu-id="abbd6-113">**Biblioteka:** CorGuids. lib</span><span class="sxs-lookup"><span data-stu-id="abbd6-113">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="abbd6-114">**.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="abbd6-114">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="abbd6-115">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="abbd6-115">See also</span></span>

- [<span data-ttu-id="abbd6-116">Debugowanie — wyliczenia</span><span class="sxs-lookup"><span data-stu-id="abbd6-116">Debugging Enumerations</span></span>](debugging-enumerations.md)
