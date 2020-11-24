---
title: IHostTaskManager::LeaveRuntime — Metoda
ms.date: 03/30/2017
api_name:
- IHostTaskManager.LeaveRuntime
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostTaskManager::LeaveRuntime
helpviewer_keywords:
- IHostTaskManager::LeaveRuntime method [.NET Framework hosting]
- LeaveRuntime method [.NET Framework hosting]
ms.assetid: 43689cc4-e48e-46e5-a22d-bafd768b8759
topic_type:
- apiref
ms.openlocfilehash: 855f8a5d3582bbad59301a344d8a51198c40a051
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95673049"
---
# <a name="ihosttaskmanagerleaveruntime-method"></a>IHostTaskManager::LeaveRuntime — Metoda

Powiadamia hosta, że aktualnie wykonywane zadanie ma opuścić środowisko uruchomieniowe języka wspólnego (CLR) i wprowadzić kod niezarządzany.  
  
> [!IMPORTANT]
> Odpowiednie wywołanie [IHostTaskManager:: EnterRuntime —](ihosttaskmanager-enterruntime-method.md) powiadamia hosta, że aktualnie wykonywane zadanie ponownie wprowadza kod zarządzany.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT LeaveRuntime (  
    [in] SIZE_T target  
);  
```  
  
## <a name="parameters"></a>Parametry  

 `target`  
 podczas Adres w mapowanym przenośnym pliku wykonywalnym funkcji niezarządzanej, która ma zostać wywołana.  
  
## <a name="return-value"></a>Wartość zwracana  
  
|HRESULT|Opis|  
|-------------|-----------------|  
|S_OK|`LeaveRuntime` pomyślnie zwrócono.|  
|HOST_E_CLRNOTAVAILABLE|Środowisko CLR nie zostało załadowane do procesu lub środowisko CLR znajduje się w stanie, w którym nie można uruchomić kodu zarządzanego lub przetworzyć wywołania pomyślnie.|  
|HOST_E_TIMEOUT|Upłynął limit czasu połączenia.|  
|HOST_E_NOT_OWNER|Obiekt wywołujący nie jest właocicielem blokady.|  
|HOST_E_ABANDONED|Zdarzenie zostało anulowane podczas oczekiwania na niego zablokowanego wątku lub włókna.|  
|E_FAIL|Wystąpił nieznany błąd krytyczny. Gdy metoda zwraca E_FAIL, środowisko CLR nie będzie już można używać w procesie. Kolejne wywołania metod hostingu zwracają HOST_E_CLRNOTAVAILABLE.|  
|E_OUTOFMEMORY|Za mało dostępnej pamięci, aby zakończyć żądaną alokację.|  
  
## <a name="remarks"></a>Uwagi  

 Sekwencje wywołań do i z kodu niezarządzanego mogą być zagnieżdżane. Na przykład na poniższej liście opisano hipotetyczną sytuację, w której sekwencja wywołań do `LeaveRuntime` , [IHostTaskManager:: ReverseEnterRuntime —](ihosttaskmanager-reverseenterruntime-method.md), [IHostTaskManager:: ReverseLeaveRuntime —](ihosttaskmanager-reverseleaveruntime-method.md), i `IHostTaskManager::EnterRuntime` umożliwia hostowi zidentyfikowanie warstw zagnieżdżonych.  
  
|Akcja|Odpowiednie wywołanie metody|  
|------------|-------------------------------|  
|Zarządzany Visual Basic plik wykonywalny wywołuje niezarządzaną funkcję zapisaną w C przy użyciu wywołania platformy.|`IHostTaskManager::LeaveRuntime`|  
|Niezarządzana funkcja języka C wywołuje metodę w zarządzanej bibliotece DLL, która została zapisywana w języku C#.|`IHostTaskManager::ReverseEnterRuntime`|  
|Zarządzana funkcja języka C# wywołuje inną niezarządzaną funkcję zapisaną w języku C, również przy użyciu wywołania platformy.|`IHostTaskManager::LeaveRuntime`|  
|Druga niezarządzana funkcja zwraca wykonanie do funkcji języka C#.|`IHostTaskManager::EnterRuntime`|  
|Funkcja języka C# zwraca wykonanie do pierwszej niezarządzanej funkcji.|`IHostTaskManager::ReverseLeaveRuntime`|  
|Pierwsza niezarządzana funkcja zwraca wykonanie do programu Visual Basic.|`IHostTaskManager::EnterRuntime`|  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** MSCorEE. h  
  
 **Biblioteka:** Uwzględnione jako zasób w MSCorEE.dll  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [ICLRTask — Interfejs](iclrtask-interface.md)
- [ICLRTaskManager — Interfejs](iclrtaskmanager-interface.md)
- [IHostTask — Interfejs](ihosttask-interface.md)
- [IHostTaskManager — Interfejs](ihosttaskmanager-interface.md)
