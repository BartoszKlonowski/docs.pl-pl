---
title: ICorDebugHeapValue::IsValid — Metoda
ms.date: 03/30/2017
api_name:
- ICorDebugHeapValue.IsValid
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugHeapValue::IsValid
helpviewer_keywords:
- IsValid method [.NET Framework debugging]
- ICorDebugHeapValue::IsValid method [.NET Framework debugging]
ms.assetid: 68e20e62-203d-46d8-bb91-8d3c61cfacc3
topic_type:
- apiref
ms.openlocfilehash: d9150d15ac183b65b87448424f265693ed7b7ab7
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95726577"
---
# <a name="icordebugheapvalueisvalid-method"></a>ICorDebugHeapValue::IsValid — Metoda

Pobiera wartość wskazującą, czy obiekt reprezentowany przez ten ICorDebugHeapValue jest prawidłowy.  
  
 Ta metoda jest przestarzała w .NET Framework w wersji 2,0.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT IsValid (  
    [out] BOOL    *pbValid  
);  
```  
  
## <a name="parameters"></a>Parametry  

 `pbValid`  
 określoną Wskaźnik do wartości logicznej wskazującej, czy ta wartość w stercie jest prawidłowa.  
  
## <a name="remarks"></a>Uwagi  

 Wartość jest nieprawidłowa, jeśli została odinicjowana przez moduł wyrzucania elementów bezużytecznych.  
  
 Ta metoda jest przestarzała. W .NET Framework 2,0 wszystkie wartości są ważne do momentu wywołania metody [ICorDebugController:: Continue](icordebugcontroller-continue-method.md) , podczas gdy wartości są unieważnione.  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorDebug. idl, CorDebug. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
