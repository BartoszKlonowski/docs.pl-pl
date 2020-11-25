---
title: ICorDebugChain, interfejs
ms.date: 03/30/2017
api_name:
- ICorDebugChain
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugChain
helpviewer_keywords:
- ICorDebugChain interface [.NET Framework debugging]
ms.assetid: f671f519-1cb3-4ae5-b9f1-abc5e783459f
topic_type:
- apiref
ms.openlocfilehash: a0285970a8a42c078aa663579e1d5998d0d1c037
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95724458"
---
# <a name="icordebugchain-interface"></a>ICorDebugChain, interfejs

Reprezentuje segment stosu wywołań fizycznych lub logicznych.  
  
## <a name="methods"></a>Metody  
  
|Metoda|Opis|  
|------------|-----------------|  
|[EnumerateFrames, metoda](icordebugchain-enumerateframes-method.md)|Pobiera moduł wyliczający, który zawiera wszystkie zarządzane ramki stosu w łańcuchu, rozpoczynając od ostatniej ramki.|  
|[GetActiveFrame — Metoda](icordebugchain-getactiveframe-method.md)|Pobiera aktywną (czyli ostatnią) ramkę w łańcuchu.|  
|[GetCallee, metoda](icordebugchain-getcallee-method.md)|Pobiera łańcuch, który został wywołany przez ten łańcuch.|  
|[GetCaller, metoda](icordebugchain-getcaller-method.md)|Pobiera łańcuch, który wywołał ten łańcuch.|  
|[GetContext — Metoda](icordebugchain-getcontext-method.md)|Nie zaimplementowano.|  
|[GetNext, metoda](icordebugchain-getnext-method.md)|Pobiera następny łańcuch ramek dla wątku.|  
|[GetPrevious, metoda](icordebugchain-getprevious-method.md)|Pobiera poprzedni łańcuch ramek dla wątku.|  
|[GetReason, metoda](icordebugchain-getreason-method.md)|Pobiera przyczynę Genesis tego łańcucha wywołującego.|  
|[GetRegisterSet — Metoda](icordebugchain-getregisterset-method.md)|Pobiera zestaw rejestru dla aktywnej części tego łańcucha.|  
|[GetStackRange — Metoda](icordebugchain-getstackrange-method.md)|Pobiera zakres adresów segmentu stosu dla tego łańcucha.|  
|[GetThread, metoda](icordebugchain-getthread-method.md)|Pobiera wątek fizyczny, do którego należy ten łańcuch wywołań.|  
|[IsManaged, metoda](icordebugchain-ismanaged-method.md)|Pobiera wartość wskazującą, czy w tym łańcuchu działa kod zarządzany.|  
  
## <a name="remarks"></a>Uwagi  

 Ramki stosu w łańcuchu zajmują ciągły obszar stosu i korzystają z tego samego wątku i kontekstu. Łańcuch może reprezentować zarządzane lub niezarządzane łańcuchy kodu. Puste `ICorDebugChain` wystąpienie reprezentuje łańcuch kodu niezarządzanego.  
  
> [!NOTE]
> Ten interfejs nie obsługuje wywoływania zdalnego na wielu maszynach ani wielu procesów.  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorDebug. idl, CorDebug. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [Debugowanie — Interfejsy](debugging-interfaces.md)
