---
title: EMemoryAvailable — Wyliczenie
ms.date: 03/30/2017
api_name:
- EMemoryAvailable
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- EMemoryAvailable
helpviewer_keywords:
- EMemoryAvailable enumeration [.NET Framework hosting]
ms.assetid: 38e72a06-dbed-473b-a59b-7e0b3ea4f2af
topic_type:
- apiref
ms.openlocfilehash: 6a8765bfd62a2e6543661804ab8d009ce19f8813
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95724315"
---
# <a name="ememoryavailable-enumeration"></a>EMemoryAvailable — Wyliczenie

Zawiera wartości wskazujące ilość wolnej pamięci fizycznej na komputerze. Te wartości logicznie mapują do zdarzeń związanych z wysoką i niską ilością pamięci zwracaną z `CreateMemoryResourceNotification` funkcji w interfejsie API systemu Windows.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
typedef enum {  
    eMemoryAvailableLow     = 1,  
    eMemoryAvailableNeutral = 2,  
    eMemoryAvailableHigh    = 3
} EMemoryAvailable;  
```  
  
## <a name="members"></a>Elementy członkowskie  
  
|Członek|Opis|  
|------------|-----------------|  
|`eMemoryAvailableHigh`|Dostępna jest duża ilość pamięci fizycznej.|  
|`eMemoryAvailableLow`|Dostępna jest bardzo mała ilość pamięci fizycznej.|  
|`eMemoryAvailableNeutral`|Dostępna pamięć fizyczna jest neutralna.|  
  
## <a name="remarks"></a>Uwagi  

 Ta wartość jest przesyłana przez hosta do środowiska uruchomieniowego języka wspólnego (CLR) za pomocą wywołania metody [ICLRMemoryNotificationCallback:: OnMemoryNotification —](iclrmemorynotificationcallback-onmemorynotification-method.md) .  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** MSCorEE. h  
  
 **Biblioteka:** MSCorEE.dll  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [Hosting — Wyliczenia](hosting-enumerations.md)
