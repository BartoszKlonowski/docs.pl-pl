---
title: CorDebugStepReason — Wyliczenie
ms.date: 03/30/2017
api_name:
- CorDebugStepReason
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorDebugStepReason
helpviewer_keywords:
- CorDebugStepReason enumeration [.NET Framework debugging]
ms.assetid: fe248069-b33c-48e1-a777-06ac9b239c54
topic_type:
- apiref
ms.openlocfilehash: 50903b3737c0fc63eda2b1190e4c3d961ce3ae7b
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95726044"
---
# <a name="cordebugstepreason-enumeration"></a>CorDebugStepReason — Wyliczenie

Wskazuje wynik pojedynczego kroku.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
typedef enum CorDebugStepReason {  
    STEP_NORMAL,  
    STEP_RETURN,  
    STEP_CALL,  
    STEP_EXCEPTION_FILTER,  
    STEP_EXCEPTION_HANDLER,  
    STEP_INTERCEPT,  
    STEP_EXIT  
} CorDebugStepReason;  
```  
  
## <a name="members"></a>Elementy członkowskie  
  
|Członek|Opis|  
|------------|-----------------|  
|`STEP_NORMAL`|Przechodzenie do normalnego działania w ramach tej samej funkcji.|  
|`STEP_RETURN`|Dalsze dalsze przechodzenie po zwróceniu funkcji.|  
|`STEP_CALL`|Dalsze przechodzenie dalej na początku nowo wywołanej funkcji.|  
|`STEP_EXCEPTION_FILTER`|Wygenerowano wyjątek i kontrola została przeniesiona do filtru wyjątków.|  
|`STEP_EXCEPTION_HANDLER`|Wygenerowano wyjątek i kontrola została przeniesiona do procedury obsługi wyjątków.|  
|`STEP_INTERCEPT`|Kontrolka została przeniesiona do interceptora.|  
|`STEP_EXIT`|Wątek zakończył działanie przed ukończeniem kroku.|  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorDebug. idl, CorDebug. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [StepComplete, metoda](icordebugmanagedcallback-stepcomplete-method.md)
- [Debugowanie — wyliczenia](debugging-enumerations.md)
