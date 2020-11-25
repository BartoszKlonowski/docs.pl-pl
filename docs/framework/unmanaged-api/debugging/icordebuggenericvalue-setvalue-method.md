---
title: ICorDebugGenericValue::SetValue — Metoda
ms.date: 03/30/2017
api_name:
- ICorDebugGenericValue.SetValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugGenericValue::SetValue
helpviewer_keywords:
- ICorDebugGenericValue::SetValue method [.NET Framework debugging]
- SetValue method, ICorDebugGenericValue interface [.NET Framework debugging]
ms.assetid: ed4c6458-0435-44fc-8e78-8ba00be362f2
topic_type:
- apiref
ms.openlocfilehash: 493793c45e7d13511e4c36fe76e472a856b50d72
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95705751"
---
# <a name="icordebuggenericvaluesetvalue-method"></a>ICorDebugGenericValue::SetValue — Metoda

Kopiuje nową wartość z określonego buforu.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT SetValue (  
    [in] void      *pFrom  
);  
```  
  
## <a name="parameters"></a>Parametry  

 `pFrom`  
 podczas Wskaźnik do buforu, z którego ma zostać skopiowana wartość.  
  
## <a name="remarks"></a>Uwagi  

 W przypadku typów referencyjnych wartością jest odwołanie, a nie zawartość.  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorDebug. idl, CorDebug. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
