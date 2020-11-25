---
title: ICorDebugNativeFrame::SetIP — Metoda
ms.date: 03/30/2017
api_name:
- ICorDebugNativeFrame.SetIP
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugNativeFrame::SetIP
helpviewer_keywords:
- ICorDebugNativeFrame::SetIP method [.NET Framework debugging]
- SetIP method, ICorDebugNativeFrame interface [.NET Framework debugging]
ms.assetid: 57784a51-c76d-48f8-9392-584d0e1946d9
topic_type:
- apiref
ms.openlocfilehash: 65de42a0b86e4b4593b7880e9dc290ce00007a40
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95709261"
---
# <a name="icordebugnativeframesetip-method"></a>ICorDebugNativeFrame::SetIP — Metoda

Ustawia wskaźnik instrukcji na określoną lokalizację przesunięcia w kodzie natywnym.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT SetIP (  
    [in] ULONG32 nOffset  
);  
```  
  
## <a name="parameters"></a>Parametry  

 `nOffset`  
 podczas Lokalizacja przesunięcia w kodzie natywnym.  
  
## <a name="remarks"></a>Uwagi  

 Wywołuje `SetIP` natychmiastowe unieważnienie wszystkich ramek i łańcuchów dla bieżącego wątku. Jeśli debuger wymaga informacji o klatce po wywołaniu `SetIP` , musi wykonać nowy ślad stosu.  
  
 [ICorDebug](icordebug-interface.md) spróbuje zachować prawidłowy stan ramki stosu. Jednak nawet jeśli ramka jest w prawidłowym stanie, o ile jest to związane ze środowiskiem uruchomieniowym, nadal mogą wystąpić problemy, takie jak Niezainicjowane zmienne lokalne itd. Obiekt wywołujący jest odpowiedzialny za ubezpieczenie spójność uruchomionego programu.  
  
 Na platformach 64-bitowych wskaźnik instrukcji nie może zostać przeniesiony z `catch` `finally` bloku lub. Jeśli `SetIP` jest wywoływana w celu przechodzenia na platformę 64-bitową, zwróci wynik HRESULT wskazujący błąd.  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorDebug. idl, CorDebug. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także
