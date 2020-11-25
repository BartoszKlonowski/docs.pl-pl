---
title: CorRefToDefCheck — Wyliczenie
ms.date: 03/30/2017
api_name:
- CorRefToDefCheck
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorRefToDefCheck
helpviewer_keywords:
- CorRefToDefCheck enumeration [.NET Framework metadata]
ms.assetid: f9a80f1a-55af-4459-b095-8441aae16119
topic_type:
- apiref
ms.openlocfilehash: e7ce604acddb88d5a15844cbce2622b21e364cc1
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95706115"
---
# <a name="correftodefcheck-enumeration"></a>CorRefToDefCheck — Wyliczenie

Określa flagi do kontrolowania, które elementy, do których istnieją odwołania, są konwertowane na ich definicje, aby zoptymalizować kod.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
typedef enum CorRefToDefCheck {  
    MDRefToDefDefault           = 0x00000003,  
    MDRefToDefAll               = 0xffffffff,  
    MDRefToDefNone              = 0x00000000,  
    MDTypeRefToDef              = 0x00000001,  
    MDMemberRefToDef            = 0x00000002  
} CorRefToDefCheck;  
```  
  
## <a name="members"></a>Elementy członkowskie  
  
|Członek|Opis|  
|------------|-----------------|  
|`MDRefToDefDefault`|Określa, że odwołania do typu i odwołania do elementów członkowskich powinny być konwertowane na definicje. Jest to wartość domyślna ( `MDTypeRefToDef` &#124; `MDMemberRefToDef` ).|  
|`MDRefToDefAll`|Określa, że wszystkie elementy, do których istnieją odwołania, powinny być konwertowane na definicje.|  
|`MDRefToDefNone`|Określa, że żadne elementy, do których istnieją odwołania, nie powinny być konwertowane na definicje.|  
|`MDTypeRefToDef`|Określa, że odwołania do typu mają być konwertowane do definicji typu.|  
|`MDMemberRefToDef`|Określa, że tylko odwołania składowe powinny być konwertowane na definicje. Oznacza to, że odwołania do elementów członkowskich powinny być konwertowane na definicje metod lub definicje pól.|  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorHdr. h  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [Wyliczenia metadanych](metadata-enumerations.md)
