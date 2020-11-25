---
title: ICorDebugHeapSegmentEnum — Interfejs
ms.date: 03/30/2017
api_name:
- ICorDebugHealRegionEnum
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugHeapSegmentEnum
helpviewer_keywords:
- ICorDebugHeapSegmentEnum interface [.NET Framework debugging]
ms.assetid: 20fc1b9d-e228-4107-bd76-53934c1724b9
topic_type:
- apiref
ms.openlocfilehash: 42126d15c64175f35bba89a1ab6abacc64128012
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95704633"
---
# <a name="icordebugheapsegmentenum-interface"></a>ICorDebugHeapSegmentEnum — Interfejs

Zawiera moduł wyliczający dla obszarów pamięci zarządzanej sterty. Ten interfejs jest podklasą interfejsu ICorDebugEnum.  
  
## <a name="methods"></a>Metody  
  
|Metoda|Opis|  
|------------|-----------------|  
|[Next, metoda](icordebugheapsegmentenum-next-method.md)|Pobiera określoną liczbę wystąpień [COR_SEGMENT](cor-segment-structure.md) , które zawierają informacje o regionach zarządzanej sterty.|  
  
## <a name="remarks"></a>Uwagi  

 `ICorDebugHeapSegmentEnum`Interfejs implementuje interfejs ICorDebugEnum.  
  
 `ICorDebugHeapSegmentEnum`Wystąpienie jest wypełniane wystąpieniami [COR_SEGMENT](cor-segment-structure.md) , wywołując metodę [ICorDebugProcess5:: EnumerateHeapRegions —](icordebugprocess5-enumerateheapregions-method.md) . [COR_SEGMENT](cor-segment-structure.md) obiektów w kolekcji można wyliczyć, wywołując metodę [ICorDebugHeapSegmentEnum:: Next](icordebugheapsegmentenum-next-method.md) .  
  
 `ICorDebugHeapSegmentEnum`Obiekt kolekcji wylicza wszystkie obszary pamięci, które mogą zawierać obiekty zarządzane, ale nie gwarantuje, że obiekty zarządzane rzeczywiście znajdują się w tych regionach. Może zawierać informacje dotyczące pustych lub zarezerwowanych regionów pamięci.  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorDebug. idl, CorDebug. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [Debugowanie — Interfejsy](debugging-interfaces.md)
