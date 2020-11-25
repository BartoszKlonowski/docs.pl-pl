---
title: GetDemultiplexedStub — funkcja (niezarządzana dokumentacja interfejsu API)
description: Funkcja GetDemultiplexedStub tworzy ujścia usługi przesyłania dalej obiektów, aby pomóc klientowi w odbieraniu asynchronicznych wywołań z usługi zarządzania systemem Windows.
ms.date: 11/06/2017
api_name:
- GetDemultiplexedStub
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- GetDemultiplexedStub
helpviewer_keywords:
- GetDemultiplexedStub function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: f8f9b56268168bb16c476a9366facd17e8ac44e5
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95730633"
---
# <a name="getdemultiplexedstub-function"></a>GetDemultiplexedStub, funkcja

Tworzy obiekt sink usługi przesyłania dalej obiektów, który pomaga klientowi odbierać asynchroniczne wywołania z usługi Windows Management.
  
[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT GetDemultiplexedStub (
   [in] IUnknown*    pObject,
   [in] boolean      isLocal,
   [out] IUnknown**  ppObject
);
```  

## <a name="parameters"></a>Parametry

`pObject`  
podczas Wskaźnik do implementacji w procesie klienta [IWbemObjectSink](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemobjectsink).

`isLocal`  
podczas Flaga wskazująca, czy zdarzenie jest lokalne ( `true` ); w przeciwnym razie `false` .

`ppObject`  
określoną Obiekt sink usługi przesyłania dalej obiektów, który ułatwia Klientowi otrzymywanie wywołań asynchronicznych z usługi Windows Management.

## <a name="return-value"></a>Wartość zwracana

Jeśli funkcja się powiedzie, zwracaną wartością jest `S_OK` (0).

Jeśli funkcja się nie powiedzie, wartość zwracana jest kodem błędu o wartości innej niż zero. Aby uzyskać rozszerzone informacje o błędzie, wywołaj funkcję [GetErrorInfo](geterrorinfo.md) .

## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** WMINet_Utils. idl  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>Zobacz także

- [WMI i liczniki wydajności (niezarządzana dokumentacja interfejsu API)](index.md)
