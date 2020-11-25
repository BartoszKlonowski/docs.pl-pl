---
title: ICorDebugStepper::IsActive — Metoda
ms.date: 03/30/2017
api_name:
- ICorDebugStepper.IsActive
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugStepper::IsActive
helpviewer_keywords:
- IsActive method, ICorDebugStepper interface [.NET Framework debugging]
- ICorDebugStepper::IsActive method [.NET Framework debugging]
ms.assetid: 8b35e7a9-b40e-40a9-8d8e-b82e823fc575
topic_type:
- apiref
ms.openlocfilehash: 0a57dfe5bb4dfdc08a5e3f2238da6794e62bd958
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95718283"
---
# <a name="icordebugstepperisactive-method"></a>ICorDebugStepper::IsActive — Metoda

Pobiera wartość wskazującą, czy ten ICorDebugStepper aktualnie wykonuje krok.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT IsActive (  
    [out] BOOL   *pbActive  
);  
```  
  
## <a name="parameters"></a>Parametry  

 `pbActive`  
 określoną Zwraca `true` czy stepper jest aktualnie wykonywany krok; w przeciwnym razie zwraca `false` .  
  
## <a name="remarks"></a>Uwagi  

 Każda akcja krok pozostaje aktywna, dopóki debuger nie otrzyma wywołania [ICorDebugManagedCallback:: StepComplete —](icordebugmanagedcallback-stepcomplete-method.md) , które automatycznie dezaktywuje stepper. Stepper może również zostać zdezaktywowany przedwcześnie przez wywołanie [ICorDebugStepper::D eactivate](icordebugstepper-deactivate-method.md) przed osiągnięciem warunku wywołania zwrotnego.  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorDebug. idl, CorDebug. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
