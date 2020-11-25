---
title: ICorProfilerInfo4::GetObjectSize2 — Metoda
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo4.GetObjectSize2
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo4::GetObjectSize2
helpviewer_keywords:
- GetObjectSize2 method, ICorProfilerInfo4 interface [.NET Framework profiling]
- ICorProfilerInfo4::GetObjectSize2 method [.NET Framework profiling]
ms.assetid: 4a3e43ed-3ee3-4395-ab14-f78b903be13e
topic_type:
- apiref
ms.openlocfilehash: 960f8f1fe2315e068d599aa5a31e03f521b235a8
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95733870"
---
# <a name="icorprofilerinfo4getobjectsize2-method"></a>ICorProfilerInfo4::GetObjectSize2 — Metoda

Zwraca rozmiar określonego obiektu. Zastępuje metodę [ICorProfilerInfo:: GetObjectSize —](icorprofilerinfo-getobjectsize-method.md) przez raportowanie rozmiarów obiektów, które są większe niż to, co może być wyrażone w `ULONG` .  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT GetObjectSize2(  
    [in]  ObjectID objectId,  
    [out] SIZE_T *pcSize);  
```  
  
## <a name="parameters"></a>Parametry  

 `objectId`  
 podczas Identyfikator obiektu.  
  
 `pcSize`  
 określoną Wskaźnik do rozmiaru obiektu, w bajtach.  
  
## <a name="remarks"></a>Uwagi  

 Różne obiekty tego samego typu często mają ten sam rozmiar. Jednak niektóre typy, takie jak tablice lub ciągi, mogą mieć różne rozmiary dla każdego obiektu.  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorProf. idl, CorProf. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [ICorProfilerInfo4 — Interfejs](icorprofilerinfo4-interface.md)
