---
title: ICorDebugInternalFrame::GetFrameType — Metoda
ms.date: 03/30/2017
api_name:
- ICorDebugInternalFrame.GetFrameType
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugInternalFrame::GetFrameType
helpviewer_keywords:
- GetFrameType method [.NET Framework debugging]
- ICorDebugInternalFrame::GetFrameType method [.NET Framework debugging]
ms.assetid: da278a29-dc2e-4bf7-96ce-801bdc4d7025
topic_type:
- apiref
ms.openlocfilehash: c675ba4b56cecd1990184cd2f0e805250c3dfeb7
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95724887"
---
# <a name="icordebuginternalframegetframetype-method"></a>ICorDebugInternalFrame::GetFrameType — Metoda

Pobiera typ tej wewnętrznej ramki.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT GetFrameType (  
    [out] CorDebugInternalFrameType  *pType  
);  
```  
  
## <a name="parameters"></a>Parametry  

 `pType`  
 określoną Wskaźnik do wartości wyliczenia CorDebugInternalFrameType —, który wskazuje typ wewnętrznej ramki reprezentowanej przez ten `ICorDebugInternalFrame` obiekt.  
  
## <a name="remarks"></a>Uwagi  

 Wewnętrzny typ ramki nigdy nie będzie STUBFRAME_NONE. Debugery powinny bezpiecznie ignorować nierozpoznane typy ramek wewnętrznych.  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorDebug. idl, CorDebug. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
