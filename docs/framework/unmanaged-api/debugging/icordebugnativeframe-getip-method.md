---
title: ICorDebugNativeFrame::GetIP — Metoda
ms.date: 03/30/2017
api_name:
- ICorDebugNativeFrame.GetIP
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugNativeFrame::GetIP
helpviewer_keywords:
- GetIP method, ICorDebugNativeFrame interface [.NET Framework debugging]
- ICorDebugNativeFrame::GetIP method [.NET Framework debugging]
ms.assetid: 99f693f3-d3b9-4fd8-9d09-b8efd03f7b67
topic_type:
- apiref
ms.openlocfilehash: c9c0598f8e7b3e8654124f50663c912f3cd61659
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95709309"
---
# <a name="icordebugnativeframegetip-method"></a>ICorDebugNativeFrame::GetIP — Metoda

Pobiera lokalizację natywnego przesunięcia kodu, w której wskaźnik instrukcji jest obecnie ustawiony.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT GetIP (  
    [out] ULONG32           *pnOffset  
);  
```  
  
## <a name="parameters"></a>Parametry  

 `pnOffset`  
 określoną Wskaźnik do lokalizacji przesunięcia w kodzie natywnym.  
  
## <a name="remarks"></a>Uwagi  

 Jeśli ramka stosu reprezentowana przez ten "ICorDebugNativeFrame" jest aktywna, przesunięcie jest adresem następnej instrukcji do wykonania. Jeśli ta ramka stosu nie jest aktywna, przesunięcie jest adresem następnej instrukcji, która ma zostać wykonana po ponownym uaktywnieniu ramki stosu.  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorDebug. idl, CorDebug. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także
