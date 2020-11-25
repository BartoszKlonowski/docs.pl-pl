---
title: ETaskType — Wyliczenie
ms.date: 03/30/2017
api_name:
- ETaskType
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ETaskType
helpviewer_keywords:
- ETaskType enumeration [.NET Framework hosting]
ms.assetid: aa527b31-89d4-41f2-ad6f-63b76950b7df
topic_type:
- apiref
ms.openlocfilehash: 332488fee4c982fdbaecceeaa2a6a3876f1602a5
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95733701"
---
# <a name="etasktype-enumeration"></a>ETaskType — Wyliczenie

Zawiera wartości wskazujące typ zadania reprezentowanego przez interfejs [ICLRTask](iclrtask-interface.md) lub [IHostTask](ihosttask-interface.md) .  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
typedef enum ETaskType {  
    TT_DEBUGGERHELPER           = 0x1,  
    TT_GC                       = 0x2,  
    TT_FINALIZER                = 0x4,  
    TT_THREADPOOL_TIMER         = 0x8,  
    TT_THREADPOOL_GATE          = 0x10,  
    TT_THREADPOOL_WORKER        = 0x20,  
    TT_THREADPOOL_IOCOMPLETION  = 0x40,  
    TT_ADUNLOAD                 = 0x80,  
    TT_USER                     = 0x100,  
    TT_THREADPOOL_WAIT          = 0x200,  
    TT_UNKNOWN                  = 0x80000000  
} ETaskType;  
```  
  
## <a name="members"></a>Elementy członkowskie  
  
|Członek|Opis|  
|------------|-----------------|  
|`TT_ADUNLOAD`|Interfejs reprezentuje zadanie wyładowywania domeny aplikacji.|  
|`TT_DEBUGGERHELPER`|Interfejs reprezentuje zadanie pomocnika debugera.|  
|`TT_FINALIZER`|Interfejs reprezentuje zadanie finalizatora.|  
|`TT_GC`|Interfejs reprezentuje zadanie wyrzucania elementów bezużytecznych.|  
|`TT_THREADPOOL_GATE`|Interfejs reprezentuje zadanie wątku bramy.|  
|`TT_THREADPOOL_IOCOMPLETION`|Interfejs reprezentuje zadanie wątku we/wy lub zadanie wątku zakończenia.|  
|`TT_THREADPOOL_TIMER`|Interfejs reprezentuje zadanie wątku czasomierza.|  
|`TT_THREADPOOL_WAIT`|Interfejs reprezentuje zadanie wątku oczekiwania.|  
|`TT_THREADPOOL_WORKER`|Interfejs reprezentuje zadanie wątku roboczego.|  
|`TT_UNKNOWN`|Zadanie jest nieznane.|  
|`TT_USER`|Interfejs reprezentuje zadanie użytkownika.|  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** MSCorEE. h  
  
 **Biblioteka:** MSCorEE.dll  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [Hosting — Wyliczenia](hosting-enumerations.md)
