---
title: ICorProfilerInfo2::GetObjectGeneration — Metoda
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo2.GetObjectGeneration
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo2::GetObjectGeneration
helpviewer_keywords:
- GetObjectGeneration method [.NET Framework profiling]
- ICorProfilerInfo2::GetObjectGeneration method [.NET Framework profiling]
ms.assetid: b0d25f76-0bd5-4aa6-96cf-bfec0e1de28b
topic_type:
- apiref
ms.openlocfilehash: 4ba404692bef84c0522a799c61f07eac341eaab4
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95703853"
---
# <a name="icorprofilerinfo2getobjectgeneration-method"></a>ICorProfilerInfo2::GetObjectGeneration — Metoda

Pobiera segment sterty, która zawiera określony obiekt.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT GetObjectGeneration(  
    [in] ObjectID objectId,  
    [out] COR_PRF_GC_GENERATION_RANGE *range);  
```  
  
## <a name="parameters"></a>Parametry  

 `objectId`  
 podczas Identyfikator obiektu.  
  
 `range`  
 określoną Wskaźnik do struktury [COR_PRF_GC_GENERATION_RANGE](cor-prf-gc-generation-range-structure.md) , który opisuje zakres (czyli blok) pamięci w ramach generacji, która nie powoduje wyrzucania elementów bezużytecznych. Ten zakres zawiera określony obiekt.  
  
## <a name="remarks"></a>Uwagi  

 `GetObjectGeneration`Metoda może być wywoływana z dowolnego wywołania zwrotnego profilera, pod warunkiem, że odzyskiwanie pamięci nie jest w toku. Oznacza to, że może być wywoływana z dowolnego wywołania zwrotnego, z wyjątkiem tych, które występują między [ICorProfilerCallback2:: GarbageCollectionStarted —](icorprofilercallback2-garbagecollectionstarted-method.md) i [ICorProfilerCallback2:: GarbageCollectionFinished —](icorprofilercallback2-garbagecollectionfinished-method.md).  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorProf. idl, CorProf. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [ICorProfilerInfo — Interfejs](icorprofilerinfo-interface.md)
- [ICorProfilerInfo2 — Interfejs](icorprofilerinfo2-interface.md)
