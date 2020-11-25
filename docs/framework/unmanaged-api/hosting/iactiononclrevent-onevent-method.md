---
title: IActionOnCLREvent::OnEvent — Metoda
ms.date: 03/30/2017
api_name:
- IActionOnCLREvent.OnEvent
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IActionOnCLREvent::OnEvent
helpviewer_keywords:
- OnEvent method [.NET Framework hosting]
- IActionOnCLREvent::OnEvent method [.NET Framework hosting]
ms.assetid: 0970f10c-4304-4c12-91c0-83e51455afb4
topic_type:
- apiref
ms.openlocfilehash: 3bfcb01e30b4cb33ec9276f1d3c6ac2f3bde4b58
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95721767"
---
# <a name="iactiononclreventonevent-method"></a>IActionOnCLREvent::OnEvent — Metoda

Wykonuje wywołania zwrotne dla zdarzeń, które zostały zarejestrowane za pomocą wywołania metody [ICLROnEventManager:: RegisterActionOnEvent —](iclroneventmanager-registeractiononevent-method.md) .  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT OnEvent (  
    [in] EClrEvent event,  
    [in] PVOID     data  
);  
```  
  
## <a name="parameters"></a>Parametry  

 `event`  
 podczas Jedna z wartości [EClrEvent —](eclrevent-enumeration.md) , która wskazuje typ zdarzenia.  
  
 `data`  
 podczas Wskaźnik do obiektu, który zawiera szczegółowe informacje o `event` .  
  
## <a name="return-value"></a>Wartość zwracana  
  
|HRESULT|Opis|  
|-------------|-----------------|  
|S_OK|`OnEvent` pomyślnie zwrócono.|  
|HOST_E_CLRNOTAVAILABLE|Środowisko uruchomieniowe języka wspólnego (CLR) nie zostało załadowane do procesu lub środowisko CLR znajduje się w stanie, w którym nie można uruchomić kodu zarządzanego lub przetworzyć wywołania pomyślnie.|  
|HOST_E_TIMEOUT|Upłynął limit czasu połączenia.|  
|HOST_E_NOT_OWNER|Obiekt wywołujący nie jest właocicielem blokady.|  
|HOST_E_ABANDONED|Zdarzenie zostało anulowane podczas oczekiwania zablokowanego wątku lub włókna.|  
|E_FAIL|Wystąpił nieznany błąd krytyczny. Jeśli metoda zwraca E_FAIL, środowisko CLR nie będzie już można używać w procesie. Kolejne wywołania metody hostingu zwracają HOST_E_CLRNOTAVAILABLE.|  
  
## <a name="remarks"></a>Uwagi  

 `data`Parametr jest wskaźnikiem do obiektu nieokreślonego typu. Jeśli `event` parametr jest `Event_DomainUnload` , `data` jest identyfikatorem liczbowym <xref:System.AppDomain> , który został zwolniony. Host może wykonać odpowiednią akcję przy użyciu tego identyfikatora jako klucza.  
  
 Jeśli `event` jest `Event_MDAFired` , `data` jest wskaźnikiem do wystąpienia [MDAInfo —](mdainfo-structure.md) , które zawiera komunikat wyjściowy z zarządzanego asystenta debugowania (MDA). MDA to funkcja środowiska CLR, która pomaga deweloperom w debugowaniu, generując komunikaty XML o zdarzeniach, które w przeciwnym razie są trudne do pułapki. Takie komunikaty mogą być szczególnie przydatne w przypadku przejść debugowania między kodem zarządzanym i niezarządzanym. Aby uzyskać więcej informacji, zobacz [Diagnozowanie błędów przy użyciu asystentów debugowania zarządzanego](../../debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md).  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** MSCorEE. h  
  
 **Biblioteka:** Uwzględnione jako zasób w MSCorEE.dll  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [Diagnozowanie błędów przy użyciu asystentów zarządzanego debugowania](../../debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)
- [EClrEvent — Wyliczenie](eclrevent-enumeration.md)
- [IActionOnCLREvent — Interfejs](iactiononclrevent-interface.md)
- [ICLRControl — Interfejs](iclrcontrol-interface.md)
- [ICLROnEventManager — Interfejs](iclroneventmanager-interface.md)
- [MDAInfo — Struktura](mdainfo-structure.md)
