---
title: ICorDebugProcess5::EnableNGENPolicy — Metoda
ms.date: 03/30/2017
api_name:
- ICorDebugProcess5::EnableNGenPolicy
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess5::EnableNGENPolicy
helpviewer_keywords:
- ICorDebugProcess5::EnableNGENPolicy method [.NET Framework debugging]
- EnableNGENPolicy method, ICorDebugProcess5 interface [.NET Framework debugging]
ms.assetid: 3b8e15ca-3c72-4685-a937-da4c739cb9e9
topic_type:
- apiref
ms.openlocfilehash: e3dfd3cae83c7891d246ff3a81427c161cc0e2d1
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95731392"
---
# <a name="icordebugprocess5enablengenpolicy-method"></a>ICorDebugProcess5::EnableNGENPolicy — Metoda

Ustawia wartość określającą sposób ładowania obrazów natywnych przez aplikację podczas działania w ramach zarządzanego debugera.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT EnableNGENPolicy(  
    [in] CorDebugNGENPolicy ePolicy  
);  
```  
  
## <a name="parameters"></a>Parametry  

 `ePolicy`  
 podczas Stała [CorDebugNGenPolicy —](cordebugngenpolicy-enumeration.md) , która określa, w jaki sposób aplikacja ładuje obrazy natywne podczas działania w zarządzanym debugerze.  
  
## <a name="remarks"></a>Uwagi  

 Jeśli zasady zostały ustawione pomyślnie, metoda zwraca `S_OK` . Jeśli `ePolicy` znajduje się poza zakresem wartości wyliczanych zdefiniowanych przez [CorDebugNGenPolicy —](cordebugngenpolicy-enumeration.md), metoda zwraca `E_INVALIDARG` i wywołanie metody nie ma żadnego wpływu. Jeśli nie można zaktualizować zasad generatora obrazów natywnych (Ngen.exe), metoda zwraca `E_FAIL` .  
  
 `ICorDebugProcess5::EnableNGenPolicy`Metodę można wywołać w dowolnym momencie w okresie istnienia procesu. Zasady obowiązują dla wszystkich modułów, które są ładowane po ustawieniu zasad.  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorDebug. idl, CorDebug. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [ICorDebugProcess5 — Interfejs](icordebugprocess5-interface.md)
- [Debugowanie — Interfejsy](debugging-interfaces.md)
- [Debugowanie](index.md)
