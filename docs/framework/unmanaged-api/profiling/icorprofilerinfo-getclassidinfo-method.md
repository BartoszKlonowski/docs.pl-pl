---
title: ICorProfilerInfo::GetClassIDInfo — Metoda
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.GetClassIDInfo
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::GetClassIDInfo
helpviewer_keywords:
- GetClassIDInfo method [.NET Framework profiling]
- ICorProfilerInfo::GetClassIDInfo method [.NET Framework profiling]
ms.assetid: 9e93b99e-5aca-415c-8e37-7f33753b612d
topic_type:
- apiref
ms.openlocfilehash: 7d19a43048da742e702636faaa46ecf1458556f5
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95722594"
---
# <a name="icorprofilerinfogetclassidinfo-method"></a>ICorProfilerInfo::GetClassIDInfo — Metoda

Pobiera moduł nadrzędny i token metadanych dla określonej klasy.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT GetClassIDInfo(  
    [in]  ClassID   classId,  
    [out] ModuleID  *pModuleId,  
    [out] mdTypeDef *pTypeDefToken);  
```  
  
## <a name="parameters"></a>Parametry  

 `classId`  
 podczas Identyfikator klasy, dla której mają zostać pobrane informacje.  
  
 `pModuleId`  
 określoną Wskaźnik do identyfikatora modułu nadrzędnego klasy.  
  
 `pTypeDefToken`  
 określoną Wskaźnik do tokenu metadanych dla klasy.  
  
## <a name="remarks"></a>Uwagi  

 Kod profilera może wywołać [ICorProfilerInfo:: GetModuleMetaData —](icorprofilerinfo-getmodulemetadata-method.md) w celu uzyskania interfejsu metadanych dla danego modułu. Token metadanych, który jest zwracany do lokalizacji, do której się odwołuje się, `pTypeDefToken` może następnie zostać użyty w celu uzyskania dostępu do metadanych dla klasy.  
  
 Aby uzyskać więcej informacji na temat typów ogólnych, użyj [ICorProfilerInfo2:: GetClassIDInfo2 —](icorprofilerinfo2-getclassidinfo2-method.md).  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorProf. idl, CorProf. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [ICorProfilerInfo — Interfejs](icorprofilerinfo-interface.md)
