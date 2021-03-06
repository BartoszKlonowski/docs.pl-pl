---
title: _EFN_GetManagedObjectName — Funkcja
ms.date: 03/30/2017
api_name:
- _EFN_GetManagedObjectName
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- _EFN_GetManagedObjectName
helpviewer_keywords:
- _EFN_GetManagedObjectName function [.NET Framework debugging]
ms.assetid: 6e7c6bee-7ced-495f-bf6c-2a5f0c716f7e
topic_type:
- apiref
ms.openlocfilehash: 0fb694cf85256c0f3ac5ae179e53ff504ab707e9
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95676208"
---
# <a name="_efn_getmanagedobjectname-function"></a>\_\_Funkcja EFN GetManagedObjectName

Pobiera nazwę typu za pomocą podanego wskaźnika obiektu zarządzanego.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT _EFN_GetManagedObjectName(  
    [in]  PDEBUG_CLIENT  Client,  
    [in]  ULONG64        objAddr,  
    [out] __out_ecount(cbName) PSTR szName,  
    [out] ULONG          cbName  
);  
```  
  
## <a name="parameters"></a>Parametry  

 `Client`  
 podczas Wskaźnik do klienta debugowania.  
  
 `objAddr`  
 podczas Wskaźnik obiektu zarządzanego.  
  
 szName  
 określoną Nazwa typu.  
  
 `cbName`  
 określoną Liczba znaków dostępnych w buforze ciągów.  
  
## <a name="remarks"></a>Uwagi  

 W przypadku braku kodu zarządzanego w wątku, który jest obecnie w kontekście, funkcja zwraca wartość HRESULT SOS_E_NOMANAGEDCODE z wartością instrumentu 0xa0 i kodem błędu 0x1000.  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** SOS_Stacktrace. h  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [Debugowanie statycznych funkcji globalnych](debugging-global-static-functions.md)
