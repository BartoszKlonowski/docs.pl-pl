---
title: ICorProfilerCallback::ModuleUnloadFinished — Metoda
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.ModuleUnloadFinished
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::ModuleUnloadFinished
helpviewer_keywords:
- ModuleUnloadFinished method [.NET Framework profiling]
- ICorProfilerCallback::ModuleUnloadFinished method [.NET Framework profiling]
ms.assetid: 185e3327-9f9c-44bc-8a5c-febea9a6bb5b
topic_type:
- apiref
ms.openlocfilehash: 514c20455b95ecf74ffaecd349982fd8f8f49816
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95723236"
---
# <a name="icorprofilercallbackmoduleunloadfinished-method"></a>ICorProfilerCallback::ModuleUnloadFinished — Metoda

Powiadamia program profilujący o zakończeniu ładowania modułu.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT ModuleUnloadFinished(  
    [in] ModuleID moduleId,  
    [in] HRESULT  hrStatus);  
```  
  
## <a name="parameters"></a>Parametry  

 `moduleId`  
 podczas Identyfikator modułu, który został zwolniony.  
  
 `hrStatus`  
 podczas WYNIK HRESULT wskazujący, czy moduł został zwolniony pomyślnie.  
  
## <a name="remarks"></a>Uwagi  

 Wartość `moduleId` nie jest prawidłowa dla żądania informacji po powrocie metody [ICorProfilerCallback:: ModuleUnloadStarted —](icorprofilercallback-moduleunloadstarted-method.md) .  
  
 Niektóre części zwalniania klasy mogą być kontynuowane po `ModuleUnloadFinished` wywołaniu wywołania zwrotnego. Błąd HRESULT w elemencie `hrStatus` wskazuje na błąd. Jednak powodzenie HRESULT w programie `hrStatus` wskazuje tylko, że pierwsza część zwalniania modułu zakończyła się powodzeniem.  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorProf. idl, CorProf. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [ICorProfilerCallback — Interfejs](icorprofilercallback-interface.md)
