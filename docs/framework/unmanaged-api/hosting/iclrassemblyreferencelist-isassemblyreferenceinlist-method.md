---
title: ICLRAssemblyReferenceList::IsAssemblyReferenceInList — Metoda
ms.date: 03/30/2017
api_name:
- ICLRAssemblyReferenceList.IsAssemblyReferenceInList
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRAssemblyReferenceList::IsAssemblyReferenceInList
helpviewer_keywords:
- ICLRAssemblyReferenceList::IsAssemblyReferenceInList method [.NET Framework hosting]
- IsAssemblyReferenceInList method [.NET Framework hosting]
ms.assetid: 8a570813-21be-407e-92a6-7ae8de3bc728
topic_type:
- apiref
ms.openlocfilehash: f74e0f111ff7869d0bfed61d420f3788f65876dc
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95679159"
---
# <a name="iclrassemblyreferencelistisassemblyreferenceinlist-method"></a>ICLRAssemblyReferenceList::IsAssemblyReferenceInList — Metoda

Pobiera wartość wskazującą, czy dostarczony wskaźnik odwołuje się do zestawu na liście.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT IsAssemblyReferenceInList (  
    [in] IUnknown *pName  
);  
```  
  
## <a name="parameters"></a>Parametry  

 `pName`  
 podczas Wskaźnik interfejsu do zestawu, który ma zostać wyszukany. Prawidłowe wartości to typu `IAssemblyName` lub `IReferenceIdentity` .  
  
## <a name="return-value"></a>Wartość zwracana  
  
|HRESULT|Opis|  
|-------------|-----------------|  
|S_OK|Ciąg zostanie wyświetlony na liście.|  
|S_FALSE|Ciąg nie pojawia się na liście.|  
|E_FAIL|Wystąpił nieznany błąd krytyczny. Po powrocie metody E_FAIL, środowisko uruchomieniowe języka wspólnego nie będzie już można używać w procesie. Kolejne wywołania metod hostingu zwracają HOST_E_CLRNOTAVAILABLE.|  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** MSCorEE. h  
  
 **Biblioteka:** Uwzględnione jako zasób w MSCorEE.dll  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [ICLRAssemblyIdentityManager — Interfejs](iclrassemblyidentitymanager-interface.md)
- [ICLRAssemblyReferenceList — Interfejs](iclrassemblyreferencelist-interface.md)
- [IHostAssemblyManager — Interfejs](ihostassemblymanager-interface.md)
- [IHostAssemblyStore — Interfejs](ihostassemblystore-interface.md)
