---
title: ICorProfilerCallback::ModuleAttachedToAssembly — Metoda
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.ModuleAttachedToAssembly
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::ModuleAttachedToAssembly
helpviewer_keywords:
- ICorProfilerCallback::ModuleAttachedToAssembly method [.NET Framework profiling]
- ModuleAttachedToAssembly method [.NET Framework profiling]
ms.assetid: b595798a-5d40-4cac-ab4f-911c61d2c5d2
topic_type:
- apiref
ms.openlocfilehash: bcf5c5c9044a30fc8259dbc54bad8f3141f0f926
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95733116"
---
# <a name="icorprofilercallbackmoduleattachedtoassembly-method"></a>ICorProfilerCallback::ModuleAttachedToAssembly — Metoda

Powiadamia program profilujący, że moduł jest dołączony do jego zestawu nadrzędnego.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT ModuleAttachedToAssembly(  
    [in] ModuleID   moduleId,  
    [in] AssemblyID AssemblyId);  
```  
  
## <a name="parameters"></a>Parametry  

 `moduleId`  
 podczas Identyfikator dołączanego modułu.  
  
 `AssemblyId`  
 podczas Identyfikator zestawu nadrzędnego, do którego jest dołączony moduł.  
  
## <a name="remarks"></a>Uwagi  

 Moduł może zostać załadowany za pomocą tabeli adresów importu (IAT), przez wywołanie do `LoadLibrary` lub przez odwołanie do metadanych. W związku z tym moduł ładujący środowisko uruchomieniowe języka wspólnego (CLR) ma wiele ścieżek kodu do określenia zestawu, w którym przebywa moduł. W związku z tym jest możliwe, że po wywołaniu [ICorProfilerCallback:: ModuleLoadFinished —](icorprofilercallback-moduleloadfinished-method.md) moduł nie wie, w jakim zestawie znajduje się i nie jest możliwe uzyskanie identyfikatora zestawu nadrzędnego. `ModuleAttachedToAssembly`Metoda jest wywoływana, gdy moduł jest dołączony do jego zestawu nadrzędnego i można uzyskać jego identyfikator zestawu nadrzędnego.  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorProf. idl, CorProf. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [ICorProfilerCallback — Interfejs](icorprofilercallback-interface.md)
