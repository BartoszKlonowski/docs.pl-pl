---
title: ICLRTask2 — Interfejs
ms.date: 03/30/2017
api_name:
- ICLRTask2
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRTask2
helpviewer_keywords:
- ICLRTask2 interface [.NET Framework hosting]
ms.assetid: b5a22ebc-0582-49de-91f9-97a3d9789290
topic_type:
- apiref
ms.openlocfilehash: 9332b3462ba389783a113d173e32850d40427ce2
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95720233"
---
# <a name="iclrtask2-interface"></a>ICLRTask2 — Interfejs

Oferuje wszystkie funkcje interfejsu [ICLRTask](iclrtask-interface.md) ; Ponadto udostępnia metody zezwalające na opóźnione przerywanie wątków w bieżącym wątku.  
  
## <a name="methods"></a>Metody  
  
|Metoda|Opis|  
|------------|-----------------|  
|[BeginPreventAsyncAbort, metoda](iclrtask2-beginpreventasyncabort-method.md)|Opóźnia nowe żądania przerwania wątku w bieżącym wątku.|  
|[EndPreventAsyncAbort, metoda](iclrtask2-endpreventasyncabort-method.md)|Zezwala na to, aby nowe lub oczekujące żądania przerwania wątku powodowały przerwania wątku w bieżącym wątku.|  
  
## <a name="remarks"></a>Uwagi  

 `ICLRTask2`Interfejs dziedziczy `ICLRTask` interfejs i dodaje metody, które pozwalają hostowi opóźnić przerwania wątku, aby chronić region kodu, który nie może kończyć się niepowodzeniem. Wywołanie `BeginPreventAsyncAbort` zwiększa wartość licznika Opóźnij wątek i Przerwij dla bieżącego wątku i wywołuje `EndPreventAsyncAbort` jego zmniejszenie. Wywołania `BeginPreventAsyncAbort` i `EndPreventAsyncAbort` mogą być zagnieżdżane. Tak długo, jak licznik jest większy od zera, przerwania wątku dla bieżącego wątku są opóźnione.  
  
 Jeśli wywołania do `BeginPreventAsyncAbort` i `EndPreventAsyncAbort` nie są sparowane, możliwe jest osiągnięcie stanu, w którym przerwania wątku nie można dostarczyć do bieżącego wątku.  
  
 Opóźnienie nie jest uznawane za wątek, który przerywa siebie.  
  
 Funkcja, która jest udostępniona przez tę funkcję, jest używana wewnętrznie przez maszynę wirtualną (VM). Użycie tych metod może spowodować nieokreślone zachowanie maszyny wirtualnej. Na przykład wywołanie `EndPreventAsyncAbort` bez pierwszego wywołania `BeginPreventAsyncAbort` może spowodować ustawienie wartości zero dla licznika, gdy maszyna wirtualna została wcześniej zwiększona. Podobnie licznik wewnętrzny nie jest sprawdzany pod kątem przepełnienia. W przypadku przekroczenia limitu całkowitego, ponieważ jest zwiększana przez zarówno hosta, jak i maszynę wirtualną, zachowanie nie zostanie określone.  
  
 Aby uzyskać informacje na temat członków dziedziczonych z `ICLRTask` i innych sposobów korzystania z tego interfejsu, zobacz Interfejs [ICLRTask](iclrtask-interface.md) .  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** MSCorEE. h  
  
 **Biblioteka:** Uwzględnione jako zasób w MSCorEE.dll  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [ICLRTask — Interfejs](iclrtask-interface.md)
- [ICLRTaskManager — Interfejs](iclrtaskmanager-interface.md)
- [IHostTask — Interfejs](ihosttask-interface.md)
- [IHostTaskManager — Interfejs](ihosttaskmanager-interface.md)
- [Hosting — Interfejsy](hosting-interfaces.md)
