---
title: ICorDebugAppDomain3::GetCachedWinRTTypes — Metoda
ms.date: 03/30/2017
api_name:
- ICorDebugAppDomain3.GetCachedWinRTTypes
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugAppDomain3::GetCachedWinRTTypes
helpviewer_keywords:
- ICorDebugAppDomain3::GetCachedWinRTTypes method [.NET Framework debugging]
- GetCachedWinRTTypes method, ICorDebugAppDomain3 interface [.NET Framework debugging]
ms.assetid: 9afd0e04-a403-41e2-9528-a6dcbcdcbd4d
topic_type:
- apiref
ms.openlocfilehash: 5e0df443e691292817ff37900fbc87204a8325ab
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95684502"
---
# <a name="icordebugappdomain3getcachedwinrttypes-method"></a>ICorDebugAppDomain3::GetCachedWinRTTypes — Metoda

Pobiera moduł wyliczający dla wszystkich typów środowisko wykonawcze systemu Windows w pamięci podręcznej.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT GetCachedWinRTTypes (
    [out] ICorDebugGuidToTypeEnum **ppGuidToTypeEnum)  
;  
```  
  
## <a name="parameters"></a>Parametry  

 `ppGuidToTypeEnum`  
 określoną Wskaźnik do obiektu interfejsu [ICorDebugGuidToTypeEnum](icordebugguidtotypeenum-interface.md) , który może wyliczyć zarządzane reprezentacje typów środowisko wykonawcze systemu Windows aktualnie załadowanych w domenie aplikacji.  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** środowisko wykonawcze systemu Windows  
  
 **Nagłówek:** CorDebug. idl, CorDebug. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [ICorDebugAppDomain3 — Interfejs](icordebugappdomain3-interface.md)
