---
title: ICorDebugProcess8::EnableExceptionCallbacksOutsideOfMyCode — metoda
ms.date: 03/30/2017
dev_langs:
- cpp
ms.assetid: b3af44ec-7d41-425b-aed9-0c4379e5cbe9
ms.openlocfilehash: 750d2a2d69c74e147c34c9c496079ee48ac04b42
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95732544"
---
# <a name="icordebugprocess8enableexceptioncallbacksoutsideofmycode-method"></a>ICorDebugProcess8::EnableExceptionCallbacksOutsideOfMyCode — metoda

[Obsługiwane w .NET Framework 4,6 i nowszych wersjach]  
  
 Włącza lub wyłącza określone typy wywołań zwrotnych wyjątków [ICorDebugManagedCallback2](icordebugmanagedcallback2-interface.md) .  
  
## <a name="syntax"></a>Składnia  
  
```cpp
HRESULT EnableExceptionCallbacksOutsideOfMyCode(  
   [in] BOOL enableExceptionsOutsideOfJMC  
);  
```  
  
## <a name="parameters"></a>Parametry  

 `enableExceptionsOutsideOfJMC`  
 podczas  
  
## <a name="remarks"></a>Uwagi  

 Jeśli wartość `enableExceptionsOutsideOfJMC` jest `false` :  
  
- Wyjątek DEBUG_EXCEPTION_FIRST_CHANCE nie powoduje wywołania zwrotnego debugera.  
  
- Wyjątek DEBUG_EXCEPTION_CATCH_HANDLER_FOUND nie powoduje wywołania zwrotnego debugera, jeśli wyjątek nigdy nie wyjdzie do kodu użytkownika (oznacza to, że ścieżka ze źródła wyjątku do procedury obsługi wyjątku nie ma metod oznaczonych jako JustMyCode lub JMC).  
  
 Wartość domyślna `enableExceptionsOutsideOfJMC` to `true` .  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorDebug. idl, CorDebug. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v46plus](../../../../includes/net-current-v46plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [ICorDebugProcess8 — interfejs](icordebugprocess8-interface.md)
- [Debugowanie — Interfejsy](debugging-interfaces.md)
