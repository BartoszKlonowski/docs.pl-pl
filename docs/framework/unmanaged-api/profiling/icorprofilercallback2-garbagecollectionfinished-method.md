---
title: ICorProfilerCallback2::GarbageCollectionFinished — Metoda
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback2.GarbageCollectionFinished
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback2::GarbageCollectionFinished
helpviewer_keywords:
- ICorProfilerCallback2::GarbageCollectionFinished method [.NET Framework profiling]
- GarbageCollectionFinished method [.NET Framework profiling]
ms.assetid: 1a5758ea-2354-43c0-92a3-32c9909d64e1
topic_type:
- apiref
ms.openlocfilehash: 84a71853ba2ccc8b95e4a8936005f2790d09a2c4
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95717317"
---
# <a name="icorprofilercallback2garbagecollectionfinished-method"></a>ICorProfilerCallback2::GarbageCollectionFinished — Metoda

Powiadamia profiler, że wyrzucanie elementów bezużytecznych zostało ukończone i wydano wszystkie wywołania zwrotne elementów bezużytecznych.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT GarbageCollectionFinished();  
```  
  
## <a name="remarks"></a>Uwagi  

 Program profilujący może bezpiecznie zbadać obiekty w ich końcowych lokalizacjach, gdy `GarbageCollectionFinished` wywoływana jest metoda.  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorProf. idl, CorProf. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [ICorProfilerCallback — Interfejs](icorprofilercallback-interface.md)
- [ICorProfilerCallback2 — Interfejs](icorprofilercallback2-interface.md)
