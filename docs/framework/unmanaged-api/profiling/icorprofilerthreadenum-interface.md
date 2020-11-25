---
title: ICorProfilerThreadEnum — Interfejs
ms.date: 03/30/2017
api_name:
- ICorProfilerThreadEnum
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerThreadEnum
helpviewer_keywords:
- ICorProfilerThreadEnum interface [.NET Framework profiling]
ms.assetid: 1e35031b-e095-4c14-9644-8deeb3081e0b
topic_type:
- apiref
ms.openlocfilehash: 147694431d2c378b856577ef5a60e8a8b4e9a7a7
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95721221"
---
# <a name="icorprofilerthreadenum-interface"></a>ICorProfilerThreadEnum — Interfejs

Zapewnia metody sekwencyjnej iteracji przez kolekcję wątków w środowisku uruchomieniowym języka wspólnego.  
  
## <a name="methods"></a>Metody  
  
|Metoda|Opis|  
|------------|-----------------|  
|[Clone — Metoda](icorprofilerthreadenum-clone-method.md)|Pobiera wskaźnik interfejsu do kopii tego `ICorProfilerThreadEnum` interfejsu.|  
|[GetCount, metoda](icorprofilerthreadenum-getcount-method.md)|Pobiera liczbę wątków, które są używane przez aplikację.|  
|[Next, metoda](icorprofilerthreadenum-next-method.md)|Pobiera określoną liczbę sąsiadujących wątków z kolejnej kolekcji wątków, rozpoczynając od bieżącej pozycji modułu wyliczającego w sekwencji.|  
|[Reset — Metoda](icorprofilerthreadenum-reset-method.md)|Przenosi kursor modułu wyliczającego do początkowego położenia sekwencji.|  
|[Skip — Metoda](icorprofilerthreadenum-skip-method.md)|Przesuwa kursor modułu wyliczającego z jego bieżącej pozycji, aby pominąć określoną liczbę elementów.|  
  
## <a name="remarks"></a>Uwagi  

 `ICorProfilerThreadEnum`Interfejs jest modułem wyliczającym. Umożliwia odbiorcom tablicy ściąganie elementów od nadawcy według stawki, która jest odpowiednia dla odbiornika. Innymi słowy, odbiorca może jawnie kontrolować przepływ elementów tablicy, co pozwala uniknąć problemów związanych z przekazywaniem dużych tablic jako parametrów metody.  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorProf. idl, CorProf. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [ICorProfilerInfo — Interfejs](icorprofilerinfo-interface.md)
- [Interfejsy profilowania](profiling-interfaces.md)
