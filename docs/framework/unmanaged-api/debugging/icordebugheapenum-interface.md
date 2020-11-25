---
title: ICorDebugHeapEnum — Interfejs
ms.date: 03/30/2017
api_name:
- ICorDebugHeapEnum
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugHeapEnum
helpviewer_keywords:
- ICorDebugHeapEnum interface [.NET Framework debugging]
ms.assetid: 99cbc1eb-d539-4f76-a0d8-b93348112f14
topic_type:
- apiref
ms.openlocfilehash: 312052fcd683acbccb9ca616992bd635490aa2a5
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95724367"
---
# <a name="icordebugheapenum-interface"></a>ICorDebugHeapEnum — Interfejs

Dostarcza moduł wyliczający dla obiektów na zarządzanej stercie. Ten interfejs jest podklasą interfejsu ICorDebugEnum.  
  
## <a name="methods"></a>Metody  
  
|Metoda|Opis|  
|------------|-----------------|  
|[Next, metoda](icordebugheapenum-next-method.md)|Pobiera określoną liczbę wystąpień [COR_HEAPOBJECT](cor-heapobject-structure.md) , które zawierają informacje o obiektach na zarządzanym stosie.|  
  
## <a name="remarks"></a>Uwagi  

 `ICorDebugHeapEnum`Interfejs implementuje interfejs ICorDebugEnum.  
  
 `ICorDebugHeapEnum`Wystąpienie jest wypełniane wystąpieniami [COR_HEAPOBJECT](cor-heapobject-structure.md) , wywołując metodę [ICorDebugProcess5:: EnumerateHeap —](icordebugprocess5-enumerateheap-method.md) . Każde wystąpienie [COR_HEAPOBJECT](cor-heapobject-structure.md) w kolekcji reprezentuje obiekt na żywo na stercie lub obiekt, który nie jest odblokowany przez żaden obiekt, ale nie został jeszcze zebrany przez moduł wyrzucania elementów bezużytecznych. [COR_HEAPOBJECT](cor-heapobject-structure.md) obiektów w kolekcji można wyliczyć, wywołując metodę [ICorDebugHeapEnum:: Next](icordebugheapenum-next-method.md) .  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorDebug. idl, CorDebug. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [Debugowanie — Interfejsy](debugging-interfaces.md)
