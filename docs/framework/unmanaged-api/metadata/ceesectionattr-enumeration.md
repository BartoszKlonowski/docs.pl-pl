---
title: CeeSectionAttr — Wyliczenie
ms.date: 03/30/2017
api_name:
- CeeSectionAttr
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CeeSectionAttr
helpviewer_keywords:
- CeeSectionAttr enumeration [.NET Framework metadata]
ms.assetid: 0db51881-b869-4677-a715-1726a9216489
topic_type:
- apiref
ms.openlocfilehash: 4b2fb80298f6eef331b5b7ae4a46222ce97ede6f
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95732739"
---
# <a name="ceesectionattr-enumeration"></a><span data-ttu-id="cd1d6-102">CeeSectionAttr — Wyliczenie</span><span class="sxs-lookup"><span data-stu-id="cd1d6-102">CeeSectionAttr Enumeration</span></span>

<span data-ttu-id="cd1d6-103">Zawiera wartości określające atrybuty sekcji, która ma być używana przez interfejs [ICeeGen](iceegen-interface.md) .</span><span class="sxs-lookup"><span data-stu-id="cd1d6-103">Provides values that specify attributes of a section for use by the [ICeeGen](iceegen-interface.md) interface.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="cd1d6-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="cd1d6-104">Syntax</span></span>  
  
```cpp  
typedef enum  {  
    sdNone      = 0,  
    sdReadOnly  = IMAGE_SCN_CNT_INITIALIZED_DATA |  
                  IMAGE_SCN_MEM_READ,  
    sdReadWrite = sdReadOnly | IMAGE_SCN_MEM_WRITE,  
    sdExecute   = IMAGE_SCN_MEM_READ | IMAGE_SCN_CNT_CODE |  
                  IMAGE_SCN_MEM_EXECUTE  
} CeeSectionAttr;  
```  
  
## <a name="members"></a><span data-ttu-id="cd1d6-105">Elementy członkowskie</span><span class="sxs-lookup"><span data-stu-id="cd1d6-105">Members</span></span>  
  
|<span data-ttu-id="cd1d6-106">Członek</span><span class="sxs-lookup"><span data-stu-id="cd1d6-106">Member</span></span>|<span data-ttu-id="cd1d6-107">Opis</span><span class="sxs-lookup"><span data-stu-id="cd1d6-107">Description</span></span>|  
|------------|-----------------|  
|`sdNone`|<span data-ttu-id="cd1d6-108">Sekcja nie ma żadnych atrybutów.</span><span class="sxs-lookup"><span data-stu-id="cd1d6-108">Section has no attributes.</span></span>|  
|`sdReadOnly`|<span data-ttu-id="cd1d6-109">Sekcja zawiera zainicjowane dane, które mogą być tylko do odczytu, a nie zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="cd1d6-109">Section contains initialized data that can be only read, not updated.</span></span>|  
|`sdReadWrite`|<span data-ttu-id="cd1d6-110">Sekcja zawiera zainicjowane dane, które można odczytać lub zaktualizować.</span><span class="sxs-lookup"><span data-stu-id="cd1d6-110">Section contains initialized data that can be read or updated.</span></span>|  
|`sdExecute`|<span data-ttu-id="cd1d6-111">Sekcja zawiera kod wykonywalny, który może być odczytywany i wykonywany.</span><span class="sxs-lookup"><span data-stu-id="cd1d6-111">Section contains executable code that is allowed to be read and executed.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="cd1d6-112">Wymagania</span><span class="sxs-lookup"><span data-stu-id="cd1d6-112">Requirements</span></span>  

 <span data-ttu-id="cd1d6-113">**Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="cd1d6-113">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="cd1d6-114">**Nagłówek:** Cor. h</span><span class="sxs-lookup"><span data-stu-id="cd1d6-114">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="cd1d6-115">**Biblioteka:** Uwzględnione jako zasób w MsCorEE.dll</span><span class="sxs-lookup"><span data-stu-id="cd1d6-115">**Library:** Included as a resource in MsCorEE.dll</span></span>  
  
 <span data-ttu-id="cd1d6-116">**.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="cd1d6-116">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="cd1d6-117">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="cd1d6-117">See also</span></span>

- [<span data-ttu-id="cd1d6-118">Wyliczenia metadanych</span><span class="sxs-lookup"><span data-stu-id="cd1d6-118">Metadata Enumerations</span></span>](metadata-enumerations.md)
