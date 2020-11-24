---
title: ICorProfilerFunctionEnum — Interfejs
ms.date: 03/30/2017
api_name:
- ICorProfilerFunctionEnum
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerFunctionEnum
helpviewer_keywords:
- ICorProfilerFunctionEnum interface [.NET Framework profiling]
ms.assetid: 0a1d4a38-cd0b-4231-91df-13646218ae72
topic_type:
- apiref
ms.openlocfilehash: 84c3b504dff8a04172dde903c1681c9f3fb2fcd2
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95669238"
---
# <a name="icorprofilerfunctionenum-interface"></a>ICorProfilerFunctionEnum — Interfejs

Zapewnia metody sekwencyjnej iteracji przez kolekcję funkcji w środowisku uruchomieniowym języka wspólnego.  
  
## <a name="methods"></a>Metody  
  
|Metoda|Opis|  
|------------|-----------------|  
|[Clone — Metoda](icorprofilerfunctionenum-clone-method.md)|Pobiera wskaźnik interfejsu do kopii tego `ICorProfilerFunctionEnum` interfejsu.|  
|[GetCount, metoda](icorprofilerfunctionenum-getcount-method.md)|Pobiera liczbę funkcji, które zostały załadowane przez aplikację lub wymuszanie załadowane przez profiler.|  
|[Next, metoda](icorprofilerfunctionenum-next-method.md)|Pobiera określoną liczbę funkcji ciągłych z sekwencyjnego zbioru funkcji, rozpoczynając od bieżącej pozycji modułu wyliczającego w sekwencji.|  
|[Reset — Metoda](icorprofilerfunctionenum-reset-method.md)|Przenosi kursor modułu wyliczającego do początkowego położenia sekwencji.|  
|[Skip — Metoda](icorprofilerfunctionenum-skip-method.md)|Przesuwa kursor modułu wyliczającego z jego bieżącej pozycji, tak aby określona liczba elementów została pominięta.|  
  
## <a name="remarks"></a>Uwagi  

 `ICorProfilerFunctionEnum`Interfejs jest modułem wyliczającym. Umożliwia odbiorcom tablicy ściąganie elementów od nadawcy według stawki, która jest odpowiednia dla odbiornika. Innymi słowy, odbiorca może jawnie kontrolować przepływ elementów tablicy, co pozwala uniknąć problemów związanych z przekazywaniem dużych tablic jako parametrów metody.  
  
 `ICorProfilerFunctionEnum` wylicza funkcje, które zostały już skompilowane JIT, ale nie zawierają funkcji ładowanych z obrazów natywnych generowanych za pomocą Ngen.exe.  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorProf. idl, CorProf. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [ICorProfilerInfo — Interfejs](icorprofilerinfo-interface.md)
- [Interfejsy profilowania](profiling-interfaces.md)
- [EnumJITedFunctions, metoda](icorprofilerinfo3-enumjitedfunctions-method.md)
