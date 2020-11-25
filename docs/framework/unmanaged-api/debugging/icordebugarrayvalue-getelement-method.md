---
title: ICorDebugArrayValue::GetElement — Metoda
ms.date: 03/30/2017
api_name:
- ICorDebugArrayValue.GetElement
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugArrayValue::GetElement
helpviewer_keywords:
- GetElement method [.NET Framework debugging]
- ICorDebugArrayValue::GetElement method [.NET Framework debugging]
ms.assetid: 7ac3cba5-c282-402e-b7ef-b46634f5176b
topic_type:
- apiref
ms.openlocfilehash: 0b6b6f46c7fff8f1d4c2ad555c93423f9ca8ac09
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95698152"
---
# <a name="icordebugarrayvaluegetelement-method"></a>ICorDebugArrayValue::GetElement — Metoda

Pobiera wartość danego elementu tablicy.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT GetElement (  
    [in]  ULONG32          cdim,  
    [in, size_is(cdim), length_is(cdim)]
         ULONG32           indices[],  
    [out] ICorDebugValue   **ppValue  
);  
```  
  
## <a name="parameters"></a>Parametry  

 `cdim`  
 podczas Liczba wymiarów tego `ICorDebugArrayValue` obiektu.  
  
 Ta wartość jest również rozmiarem tablicy, `indices` ponieważ jej rozmiar jest równy liczbie wymiarów `ICorDebugArrayValue` obiektu.  
  
 `indices`  
 podczas Tablica wartości indeksu, z których każdy określa pozycję w wymiarze `ICorDebugArrayValue` obiektu.  
  
 Ta wartość nie może być równa null.  
  
 `ppValue`  
 określoną Wskaźnik do adresu obiektu ICorDebugValue, który reprezentuje wartość określonego elementu.  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorDebug. idl, CorDebug. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
