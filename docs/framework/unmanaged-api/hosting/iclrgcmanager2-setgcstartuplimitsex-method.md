---
title: ICLRGCManager2::SetGCStartupLimitsEx — Metoda
ms.date: 03/30/2017
api_name:
- ICLRGCManager2.SetGCStartupLimitsEx
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRGCManager2::SetCLRGCStartupLimitsEx
helpviewer_keywords:
- ICLRGCManager2::SetGCStartupLimitsEx method [.NET Framework hosting]
- SetGCStartupLimitsEx method, ICLRGCManager2 interface [.NET Framework hosting]
ms.assetid: 6c3a08a9-5d65-48d4-8bbf-2a86ed7d356a
topic_type:
- apiref
ms.openlocfilehash: 27d1ce06800075d2690bc508554b70f8d10168af
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95715020"
---
# <a name="iclrgcmanager2setgcstartuplimitsex-method"></a>ICLRGCManager2::SetGCStartupLimitsEx — Metoda

Ustawia rozmiar segmentu wyrzucania elementów bezużytecznych i maksymalny rozmiar generacji 0 systemu odzyskiwania pamięci.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT SetGCStartupLimitsEx (  
    [in] SIZE_T SegmentSize,
    [in] SIZE_T MaxGen0Size  
);  
```  
  
## <a name="parameters"></a>Parametry  

 `SegmentSize`  
 podczas Określony rozmiar segmentu odzyskiwania pamięci.  
  
 Minimalny rozmiar segmentu to 4 MB. Segmenty można zwiększyć z przyrostem wynoszącym 1 MB lub większą.  
  
 `MaxGen0Size`  
 podczas Określony maksymalny rozmiar dla generacji 0.  
  
 Minimalna wielkość generacji 0 to 64 KB.  
  
## <a name="return-value"></a>Wartość zwracana  
  
|HRESULT|Opis|  
|-------------|-----------------|  
|S_OK|`SetGCStartupLimitsEx` pomyślnie zwrócono.|  
|HOST_E_CLRNOTAVAILABLE|Środowisko uruchomieniowe języka wspólnego (CLR) nie zostało załadowane do procesu lub środowisko CLR znajduje się w stanie, w którym nie można uruchomić kodu zarządzanego lub przetworzyć wywołania pomyślnie.|  
|HOST_E_TIMEOUT|Upłynął limit czasu połączenia.|  
|HOST_E_NOT_OWNER|Obiekt wywołujący nie jest właocicielem blokady.|  
|HOST_E_ABANDONED|Zdarzenie zostało anulowane podczas oczekiwania na niego zablokowanego wątku lub włókna.|  
|E_FAIL|Wystąpił nieznany błąd krytyczny. Po powrocie metody E_FAIL nie będzie można używać środowiska CLR w procesie. Kolejne wywołania metod hostingu zwracają HOST_E_CLRNOTAVAILABLE.|  
  
## <a name="remarks"></a>Uwagi  

 Wartości, które `SetGCStartupLimitsEx` ustawia się, można określić tylko przed uruchomieniem hosta. Późniejsze wywołania `SetGCStartupLimitsEx` są ignorowane.  
  
 Aby ustawić jeden z parametrów bez wpływu na pozostałe, określ wartość 0 (zero) dla parametru, którego nie chcesz zmienić.  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** MSCorEE. h  
  
 **Biblioteka:** Uwzględnione jako zasób w MSCorEE.dll  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [Automatyczne zarządzanie pamięcią](../../../standard/automatic-memory-management.md)
- [Odzyskiwanie pamięci](../../../standard/garbage-collection/index.md)
- [ICLRControl — Interfejs](iclrcontrol-interface.md)
- [ICLRGCManager2 — Interfejs](iclrgcmanager2-interface.md)
