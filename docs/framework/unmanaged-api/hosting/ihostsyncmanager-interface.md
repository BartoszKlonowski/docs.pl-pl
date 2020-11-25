---
title: IHostSyncManager — Interfejs
ms.date: 03/30/2017
api_name:
- IHostSyncManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostSyncManager
helpviewer_keywords:
- IHostSyncManager interface [.NET Framework hosting]
ms.assetid: 2e081a37-6a28-4c93-b7ab-1c96a464637c
topic_type:
- apiref
ms.openlocfilehash: 8a5fc42191634a2e5a441baecc4b78212ffad687
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95720499"
---
# <a name="ihostsyncmanager-interface"></a>IHostSyncManager — Interfejs

Dostarcza metody, które umożliwiają środowisko uruchomieniowe języka wspólnego (CLR) do tworzenia pierwotnych synchronizacji przez wywołanie hosta zamiast korzystania z funkcji synchronizacji Win32.  
  
## <a name="methods"></a>Metody  
  
|Metoda|Opis|  
|------------|-----------------|  
|[CreateAutoEvent, metoda](ihostsyncmanager-createautoevent-method.md)|Tworzy obiekt zdarzenia autoresetowania.|  
|[CreateCrst, metoda](ihostsyncmanager-createcrst-method.md)|Tworzy obiekt sekcji krytycznej do synchronizacji.|  
|[CreateCrstWithSpinCount, metoda](ihostsyncmanager-createcrstwithspincount-method.md)|Tworzy obiekt sekcji krytycznej z liczbą wirowania do synchronizacji.|  
|[CreateManualEvent, metoda](ihostsyncmanager-createmanualevent-method.md)|Tworzy obiekt zdarzenia resetowania ręcznego.|  
|[CreateMonitorEvent, metoda](ihostsyncmanager-createmonitorevent-method.md)|Tworzy monitorowany obiekt zdarzenia autoresetowania.|  
|[CreateRWLockReaderEvent, metoda](ihostsyncmanager-createrwlockreaderevent-method.md)|Tworzy obiekt zdarzenia resetowania ręcznego dla implementacji blokady czytnika.|  
|[CreateRWLockWriterEvent, metoda](ihostsyncmanager-createrwlockwriterevent-method.md)|Tworzy obiekt zdarzenia autoresetowania dla implementacji blokady składnika zapisywania.|  
|[CreateSemaphore, metoda](ihostsyncmanager-createsemaphore-method.md)|Tworzy obiekt [IHostSemaphore](ihostsemaphore-interface.md) dla środowiska CLR do użycia jako semafor dla zdarzeń oczekiwania.|  
|[SetCLRSyncManager, metoda](ihostsyncmanager-setclrsyncmanager-method.md)|Ustawia wystąpienie [ICLRSyncManager](iclrsyncmanager-interface.md) do skojarzenia z bieżącym `IHostSyncManager` wystąpieniem.|  
  
## <a name="remarks"></a>Uwagi  

 Środowisko CLR wykrywa implementację hosta `IHostSyncManager` przez wywołanie metody [IHostControl:: GetHostManager](ihostcontrol-gethostmanager-method.md) z `IID` IID_IHostSyncManager.  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** MSCorEE. h  
  
 **Biblioteka:** Uwzględnione jako zasób w MSCorEE.dll  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [ICLRSyncManager — Interfejs](iclrsyncmanager-interface.md)
- [Hosting — Interfejsy](hosting-interfaces.md)
