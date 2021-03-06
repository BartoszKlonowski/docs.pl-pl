---
title: CorDebugThreadState — Wyliczenie
ms.date: 03/30/2017
api_name:
- CorDebugThreadState
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorDebugThreadState
helpviewer_keywords:
- CorDebugThreadState enumeration [.NET Framework debugging]
ms.assetid: a3ccdf18-4ec6-494d-9024-48e5c8c724f5
topic_type:
- apiref
ms.openlocfilehash: 5eee2aee5873fe512136bc5407e395acdc31af29
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95722612"
---
# <a name="cordebugthreadstate-enumeration"></a>CorDebugThreadState — Wyliczenie

Określa stan wątku do debugowania.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
typedef enum CorDebugThreadState {  
    THREAD_RUN,  
    THREAD_SUSPEND  
} CorDebugThreadState;  
```  
  
## <a name="members"></a>Elementy członkowskie  
  
|Członek|Opis|  
|------------|-----------------|  
|`THREAD_RUN`|Wątek działa swobodnie, chyba że wystąpi zdarzenie debugowania.|  
|`THREAD_SUSPEND`|Nie można uruchomić wątku.|  
  
## <a name="remarks"></a>Uwagi  

 Debuger używa wyliczenia, `CorDebugThreadState` Aby kontrolować wykonywanie wątku. Stan wątku można ustawić za pomocą metody [ICorDebugThread:: SetDebugState —](icordebugthread-setdebugstate-method.md) lub [ICorDebugController:: SetAllThreadsDebugState —](icordebugcontroller-setallthreadsdebugstate-method.md) .  
  
 Wywołanie zwrotne obsługiwane w [interfejsie API hostingu](../hosting/index.md) umożliwia pompowanie komunikatów, dlatego nie jest wymagany stan przerwania.  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorDebug. idl, CorDebug. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [Debugowanie — wyliczenia](debugging-enumerations.md)
