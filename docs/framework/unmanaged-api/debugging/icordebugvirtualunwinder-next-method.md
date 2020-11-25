---
title: 'ICorDebugVirtualUnwinder:: Next — Metoda'
ms.date: 03/30/2017
ms.assetid: 790e0426-e5cd-49fd-a792-f8c8635d72fe
ms.openlocfilehash: bfc827a1503b0367a442e3f3ca0915bd2aaeb01e
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95725953"
---
# <a name="icordebugvirtualunwindernext-method"></a>ICorDebugVirtualUnwinder:: Next — Metoda

Przechodzi do kontekstu obiektu wywołującego.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT Next();  
```  
  
## <a name="parameters"></a>Parametry  

 Brak.  
  
## <a name="return-value"></a>Wartość zwracana  

 `S_OK` Jeśli operacja unwind zakończyła się pomyślnie lub `CORDBG_S_AT_END_OF_STACK` nie można ukończyć operacji unwindy, ponieważ nie ma więcej ramek.  
  
 Jeśli zwracana jest niepowodzenie HRESULT, ICorDebug interfejsy API zostaną zwrócone `CORDBG_E_DATA_TARGET_ERROR` .  
  
## <a name="remarks"></a>Uwagi  

 Analizator stosu powinien zapewnić, że postępuje postęp, tak że ostatecznie wywołanie `Next` zwróci błąd HRESULT lub `CORDBG_S_AT_END_OF_STACK` . Zwracanie `S_OK` nieokreślonych wartości może spowodować nieskończoną pętlę.  
  
> [!NOTE]
> Ta metoda jest dostępna tylko z .NET Native.  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorDebug. idl, CorDebug. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **.NET Framework wersje:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [ICorDebugMemoryBuffer, interfejs](icordebugmemorybuffer-interface.md)
- [Debugowanie — Interfejsy](debugging-interfaces.md)
