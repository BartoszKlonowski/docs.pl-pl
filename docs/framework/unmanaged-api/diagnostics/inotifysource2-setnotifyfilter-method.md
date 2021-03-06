---
title: INotifySource2::SetNotifyFilter — Metoda
ms.date: 03/30/2017
api_name:
- INotifySource2.SetNotifyFilter
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- INotifySource2::SetNotifyFilter
helpviewer_keywords:
- INotifySource2::SetNotifyFilter method [.NET Framework debugging]
- SetNotifyFilter method [.NET Framework debugging]
ms.assetid: 6351fc92-b126-4af6-9bf3-0a8ce92845fc
topic_type:
- apiref
ms.openlocfilehash: 99bce831405d722f1f1ca0ae56e60f95f2d905e8
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95719934"
---
# <a name="inotifysource2setnotifyfilter-method"></a>INotifySource2::SetNotifyFilter — Metoda

Przypisuje filtr powiadomień do użycia z tym źródłem.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT SetNotifyFilter  
(  
    [in]  NOTIFY_FILTER   in_NotifyFilter,  
    [in]  USER_THREAD*    in_pUserThreadFilter  
);  
```  
  
## <a name="parameters"></a>Parametry  

 `in_NotifyFilter`  
 podczas Bitowa kombinacja [NOTIFY_FILTER](notify-filter-enumeration.md) wartości wyliczenia, które identyfikują wywołania zwrotne dla interfejsu API debugera.  
  
 `in_pUserThreadFilter`  
 podczas Wskaźnik do struktury [USER_THREAD](user-thread-structure.md) , który identyfikuje wątki dla interfejsu API debugera.  
  
## <a name="return-value"></a>Wartość zwracana  

 S_OK, jeśli metoda zakończy się pomyślnie.  
  
## <a name="requirements"></a>Wymagania  

 **Nagłówek:** ProtocolNotify2. idl  
  
## <a name="see-also"></a>Zobacz także

- [INotifySource2 — Interfejs](inotifysource2-interface.md)
- [INotifyConnection2 — Interfejs](inotifyconnection2-interface.md)
- [INotifySink2 — Interfejs](inotifysink2-interface.md)
