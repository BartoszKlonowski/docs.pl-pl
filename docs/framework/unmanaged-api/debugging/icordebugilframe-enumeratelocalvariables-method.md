---
title: ICorDebugILFrame::EnumerateLocalVariables — Metoda
ms.date: 03/30/2017
api_name:
- ICorDebugILFrame.EnumerateLocalVariables
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugILFrame::EnumerateLocalVariables
helpviewer_keywords:
- EnumerateLocalVariables method [.NET Framework debugging]
- ICorDebugILFrame::EnumerateLocalVariables method [.NET Framework debugging]
ms.assetid: 1a67fa1b-2419-4cd0-aad4-6f46a0719b4b
topic_type:
- apiref
ms.openlocfilehash: 968ceec53aade3d04c500c8247d397ffb71382c1
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95703203"
---
# <a name="icordebugilframeenumeratelocalvariables-method"></a>ICorDebugILFrame::EnumerateLocalVariables — Metoda

Pobiera moduł wyliczający dla zmiennych lokalnych w tej ramce.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT EnumerateLocalVariables(
    [out] ICorDebugValueEnum    **ppValueEnum  
);  
```  
  
## <a name="parameters"></a>Parametry  

 `ppValueEnum`  
 określoną Wskaźnik do adresu obiektu ICorDebugValueEnum, który jest modułem wyliczającym dla zmiennych lokalnych w tej ramce.  
  
## <a name="remarks"></a>Uwagi  

 `EnumerateLocalVariables` Pobiera moduł wyliczający, który może wyświetlać listę zmiennych lokalnych dostępnych w ramce wywołania, która jest reprezentowana przez ten obiekt ICorDebugILFrame. Lista nie może zawierać wszystkich zmiennych lokalnych w uruchomionej funkcji, ponieważ niektóre z nich mogą nie być aktywne.  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorDebug. idl, CorDebug. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
