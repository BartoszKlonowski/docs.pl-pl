---
title: INotifySink2::OnSyncCallEnter — Metoda
ms.date: 03/30/2017
api_name:
- INotifySink2.OnSyncCallEnter
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- INotifySink2::OnSyncCallEnter
helpviewer_keywords:
- INotifySink2::OnSyncCallEnter method [.NET Framework debugging]
- OnSyncCallEnter method [.NET Framework debugging]
ms.assetid: e33265be-c25d-4145-ad02-c3e89d6f26c1
topic_type:
- apiref
ms.openlocfilehash: 57d12a463bc0904e1a5c873d24f843e004b95101
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95720012"
---
# <a name="inotifysink2onsynccallenter-method"></a>INotifySink2::OnSyncCallEnter — Metoda

Wywoływana podczas wprowadzania wywołania.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT OnSyncCallEnter  
(  
    [in]  CALL_ID   in_CallID,  
    [in, size_is(in_BufferSize)] BYTE*  in_pBuffer,  
    [in]  DWORD     in_BufferSize  
);  
```  
  
## <a name="parameters"></a>Parametry  

 `in_CallID`  
 podczas Identyfikator wprowadzonego wywołania. Zobacz [strukturę CALL_ID](call-id-structure.md).  
  
 `in_pBuffer`  
 podczas Bufor wywołań.  
  
 `in_BufferSize`  
 podczas Rozmiar buforu wywołań w bajtach.  
  
## <a name="return-value"></a>Wartość zwracana  

 S_OK, jeśli metoda zakończy się pomyślnie.  
  
## <a name="requirements"></a>Wymagania  

 **Nagłówek:** ProtocolNotify2. idl  
  
## <a name="see-also"></a>Zobacz także

- [INotifySink2 — Interfejs](inotifysink2-interface.md)
- [INotifySource2 — Interfejs](inotifysource2-interface.md)
- [INotifyConnection2 — Interfejs](inotifyconnection2-interface.md)
