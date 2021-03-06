---
title: ICorDebugProcess::IsTransitionStub — Metoda
ms.date: 03/30/2017
api_name:
- ICorDebugProcess.IsTransitionStub
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess::IsTransitionStub
helpviewer_keywords:
- ICorDebugProcess::IsTransitionStub method [.NET Framework debugging]
- IsTransitionStub method [.NET Framework debugging]
ms.assetid: f7653317-7e48-4163-be03-f50f1a4b0f70
topic_type:
- apiref
ms.openlocfilehash: 2996c219ccf4e975c45fb531807abc4a608bae73
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95694779"
---
# <a name="icordebugprocessistransitionstub-method"></a>ICorDebugProcess::IsTransitionStub — Metoda

Pobiera wartość wskazującą, czy adres znajduje się wewnątrz klasy zastępczej, która spowoduje przejście do kodu zarządzanego.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT IsTransitionStub(  
    [in]  CORDB_ADDRESS address,  
    [out] BOOL *pbTransitionStub);  
```  
  
## <a name="parameters"></a>Parametry  

 `address`  
 podczas `CORDB_ADDRESS` Wartość, która określa dany adres.  
  
 `pbTransitionStub`  
 określoną Wskaźnik do wartości logicznej, która jest, `true` Jeśli określony adres znajduje się wewnątrz klasy zastępczej, która spowoduje przejście do kodu zarządzanego; w przeciwnym razie * `pbTransitionStub` jest `false` .  
  
## <a name="remarks"></a>Uwagi  

 `IsTransitionStub`Metoda może być używana przez niezarządzany kod wykonujący, aby zdecydować, kiedy należy zwrócić kontrolę krokową do zarządzanego stepper.  
  
 Można również posłużyć do przechodzenia między zmianami, sprawdzając informacje w przenośnym pliku wykonywalnym (PE).  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorDebug. idl, CorDebug. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
