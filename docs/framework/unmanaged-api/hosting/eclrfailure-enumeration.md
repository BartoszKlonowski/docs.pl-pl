---
title: EClrFailure — Wyliczenie
ms.date: 03/30/2017
api_name:
- EClrFailure
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- EClrFailure
helpviewer_keywords:
- EClrFailure enumeration [.NET Framework hosting]
ms.assetid: 37b95cce-9bfb-4ecf-a00b-33dcba782c67
topic_type:
- apiref
ms.openlocfilehash: d2794b53ed17640413928b3af0d1ed3656e25f22
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95675766"
---
# <a name="eclrfailure-enumeration"></a>EClrFailure — Wyliczenie

Opisuje zestaw błędów, dla których host może ustawiać akcje zasad.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
typedef enum {  
    FAIL_NonCriticalResource,  
    FAIL_CriticalResource,  
    FAIL_FatalRuntime,  
    FAIL_OrphanedLock  
    FAIL_StackOverflow  
    FAIL_AccessViolation  
    FAIL_CodeContract  
} EClrFailure;  
```  
  
## <a name="members"></a>Elementy członkowskie  
  
|Członek|Opis|  
|------------|-----------------|  
|`FAIL_NonCriticalResource`|Wystąpił błąd podczas próby przydzielenia zasobu (takiego jak wątek, blok pamięci lub blokada) w niekrytycznym regionie kodu.|  
|`FAIL_CriticalResource`|Wystąpił błąd podczas próby przydzielenia zasobu (takiego jak wątek, blok pamięci lub blokada) w krytycznym regionie kodu.|  
|`FAIL_FatalRuntime`|Środowisko uruchomieniowe języka wspólnego (CLR) nie może już uruchamiać kodu zarządzanego w procesie. Odtąd wywołania funkcji hostingu zwracają wartość HRESULT HOST_E_CLRNOTAVAILABLE.|  
|`FAIL_OrphanedLock`|Wątek nie może zwolnić blokady po powrocie z <xref:System.AppDomain> obiektu. Host nie może ustawić tego błędu, aby powodował przerwanie wątku.|  
|`FAIL_StackOverflow`|Nastąpiło przepełnienie stosu.|  
|`FAIL_AccessViolation`|Podjęto próbę odczytu lub zapisu chronionej pamięci. Nieobsługiwane w .NET Framework 4.|  
|`FAIL_CodeContract`|Wystąpił błąd kontraktu kodu. Zobacz [kontrakty kodu](../../debug-trace-profile/code-contracts.md).|  
  
## <a name="remarks"></a>Uwagi  

 Zobacz metodę [ICLRPolicyManager:: SetActionOnFailure —](iclrpolicymanager-setactiononfailure-method.md) , aby uzyskać listę wartości [EPolicyAction —](epolicyaction-enumeration.md) , których host może użyć do określenia akcji zasad dla warunków niepowodzeń. Aby uzyskać więcej informacji na temat krytycznych i niekrytycznych regionów kodu, zobacz [EClrOperation —](eclroperation-enumeration.md).  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** MSCorEE. h  
  
 **Biblioteka:** MSCorEE.dll  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [ICLRPolicyManager — Interfejs](iclrpolicymanager-interface.md)
- [SetActionOnFailure, metoda](iclrpolicymanager-setactiononfailure-method.md)
- [IHostPolicyManager — Interfejs](ihostpolicymanager-interface.md)
- [Hosting — Wyliczenia](hosting-enumerations.md)
