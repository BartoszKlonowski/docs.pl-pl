---
title: LoggingLevelEnum — Wyliczenie
ms.date: 03/30/2017
api_name:
- LoggingLevelEnum
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- LoggingLevelEnum
helpviewer_keywords:
- LoggingLevelEnum enumeration [.NET Framework debugging]
ms.assetid: 09daac08-005a-46b2-beab-408d0820c5e5
topic_type:
- apiref
ms.openlocfilehash: 389edbeb746fbeaf60d88bf9ee2a3a0731822e55
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95672022"
---
# <a name="logginglevelenum-enumeration"></a>LoggingLevelEnum — Wyliczenie

Wskazuje poziom ważności komunikatu opisowego, który jest zapisywana w dzienniku zdarzeń, gdy zarządzany wątek rejestruje zdarzenie.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
typedef enum LoggingLevelEnum {  
    LTraceLevel0 = 0,  
    LTraceLevel1,  
    LTraceLevel2,  
    LTraceLevel3,  
    LTraceLevel4,  
    LStatusLevel0 = 20,  
    LStatusLevel1,  
    LStatusLevel2,  
    LStatusLevel3,  
    LStatusLevel4,  
    LWarningLevel = 40,  
    LErrorLevel = 50,  
    LPanicLevel = 100  
} LoggingLevelEnum;  
```  
  
## <a name="members"></a>Elementy członkowskie  
  
|Członek|Opis|  
|------------|-----------------|  
|`LTraceLevel0`|Komunikat jest poziomem śledzenia równym 0.|  
|`LTraceLevel1`|Komunikat jest poziomem śledzenia 1.|  
|`LTraceLevel2`|Komunikat jest poziomem śledzenia 2.|  
|`LTraceLevel3`|Komunikat jest poziomem śledzenia 3.|  
|`LTraceLevel4`|Komunikat jest poziomem śledzenia 4.|  
|`LStatusLevel0`|Komunikat jest poziomem stanu 0.|  
|`LStatusLevel1`|Komunikat jest poziomem stanu 1.|  
|`LStatusLevel2`|Komunikat jest poziomem stanu 2.|  
|`LStatusLevel3`|Komunikat jest poziomem stanu 3.|  
|`LStatusLevel4`|Komunikat jest poziomem stanu 4.|  
|`LWarningLevel`|Komunikat jest poziomem ostrzegawczym.|  
|`LErrorLevel`|Komunikat jest poziomem błędu.|  
|`LPanicLevel`|Komunikat jest poziomem awaryjnego.|  
  
## <a name="remarks"></a>Uwagi  

 Środowisko uruchomieniowe języka wspólnego (CLR) wywołuje metodę [ICorDebugManagedCallback:: LogMessage](icordebugmanagedcallback-logmessage-method.md) w celu powiadomienia debugera o zarejestrowaniu zdarzenia przez wątek zarządzany. Środowisko CLR przekazuje wartość `LoggingLevelEnum` wyliczenia, aby wskazać poziom ważności komunikatu, który został zapisany przez wątek zarządzany w dzienniku zdarzeń.  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorDebug. idl, CorDebug. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Diagnostics.EventLog>
- [Debugowanie — wyliczenia](debugging-enumerations.md)
