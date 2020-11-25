---
title: ICorProfilerCallback::JITFunctionPitched — Metoda
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.JITFunctionPitched
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::JITFunctionPitched
helpviewer_keywords:
- JITFunctionPitched method [.NET Framework profiling]
- ICorProfilerCallback::JITFunctionPitched method [.NET Framework profiling]
ms.assetid: 116085df-7a77-404a-afac-d0557a12b986
topic_type:
- apiref
ms.openlocfilehash: 51fec26837b3c7f0a0328a7b64ff4a02148283da
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95725517"
---
# <a name="icorprofilercallbackjitfunctionpitched-method"></a>ICorProfilerCallback::JITFunctionPitched — Metoda

Powiadamia program profilujący, że funkcja, która została skompilowana just-in-Time (JIT), została usunięta z pamięci.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT JITFunctionPitched(  
    [in] FunctionID functionId);  
```  
  
## <a name="parameters"></a>Parametry  

 `functionId`  
 podczas Identyfikator funkcji, która została usunięta.  
  
## <a name="remarks"></a>Uwagi  

 Jeśli usunięta funkcja zostanie wywołana, profiler otrzyma nowe zdarzenia JIT-kompilacja po ponownym skompilowaniu funkcji. Obecnie kompilator JIT środowiska uruchomieniowego języka wspólnego (CLR) nie usuwa funkcji z pamięci, więc to wywołanie zwrotne nie jest obecnie używane i nie zostanie odebrane przez profiler.  
  
 Wartość `functionId` jest nieprawidłowa, dopóki funkcja nie zostanie ponownie skompilowana. Po ponownym skompilowaniu funkcji `functionId` zostanie użyta ta sama wartość.  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorProf. idl, CorProf. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [ICorProfilerCallback — Interfejs](icorprofilercallback-interface.md)
