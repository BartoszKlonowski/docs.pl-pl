---
title: ICorProfilerCallback::ThreadAssignedToOSThread — Metoda
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.ThreadAssignedToOSThread
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::ThreadAssignedToOSThread
helpviewer_keywords:
- ThreadAssignedToOSThread method [.NET Framework profiling]
- ICorProfilerCallback::ThreadAssignedToOSThread method [.NET Framework profiling]
ms.assetid: f9671e5a-7b14-4f5b-8404-58136422c8b2
topic_type:
- apiref
ms.openlocfilehash: 2d6f34d88dd79fe350f1c018e3afa55e5b180c46
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95732011"
---
# <a name="icorprofilercallbackthreadassignedtoosthread-method"></a>ICorProfilerCallback::ThreadAssignedToOSThread — Metoda

Powiadamia program profilujący o implementacji wątku zarządzanego przy użyciu określonego wątku systemu operacyjnego.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT ThreadAssignedToOSThread(  
    [in] ThreadID managedThreadId,  
    [in] DWORD    osThreadId);  
```  
  
## <a name="parameters"></a>Parametry  

 `managedThreadId`  
 podczas Identyfikator zarządzanego wątku.  
  
 `osThreadId`  
 podczas Identyfikator wątku systemu operacyjnego.  
  
## <a name="remarks"></a>Uwagi  

 `ThreadAssignedToOSThread`Wywołanie zwrotne istnieje, aby Profiler mógł zachować dokładne mapowanie w włókien wątków systemu operacyjnego do zarządzanych wątków.  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorProf. idl, CorProf. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [ICorProfilerCallback — Interfejs](icorprofilercallback-interface.md)
