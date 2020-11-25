---
title: NextMethod — funkcja (niezarządzana dokumentacja interfejsu API)
description: Funkcja NextMethod pobiera następną metodę w wyliczeniu.
ms.date: 11/06/2017
api_name:
- NextMethod
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- NextMethod
helpviewer_keywords:
- NextMethod function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: a0466aee47b0a6142870640c78b43f49e221ac2b
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95726772"
---
# <a name="nextmethod-function"></a>NextMethod, funkcja

Pobiera następną metodę w wyliczeniu, która rozpoczyna się od wywołania do [BeginMethodEnumeration](beginmethodenumeration.md).  

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT NextMethod (
   [in] int                 vFunc,
   [in] IWbemClassObject*   ptr,
   [in] LONG                lFlags,
   [out] BSTR*              pName,
   [out] IWbemClassObject** ppInSignature,
   [out] IWbemClassObject** ppOutSignature
);
```  

## <a name="parameters"></a>Parametry

`vFunc`  
podczas Ten parametr jest nieużywany.

`ptr`  
podczas Wskaźnik do wystąpienia [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) .

`lFlags`  
podczas Rezerwacj. Ten parametr musi być równy 0.

`pName`  
określoną Wskaźnik wskazujący `null` przed wywołaniem. Gdy funkcja zwraca, adres nowej `BSTR` , która zawiera nazwę metody.

`ppSignatureIn`  
określoną Wskaźnik, który odbiera wskaźnik do elementu [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) , który zawiera `in` parametry dla metody.

`ppSignatureOut`  
określoną Wskaźnik, który odbiera wskaźnik do elementu [IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject) , który zawiera `out` parametry dla metody.

## <a name="return-value"></a>Wartość zwracana

Następujące wartości zwracane przez tę funkcję są zdefiniowane w pliku nagłówkowym *WbemCli. h* lub można je definiować jako stałe w kodzie:

|Stała  |Wartość  |Opis  |
|---------|---------|---------|
| `WBEM_E_UNEXPECTED` | 0x8004101d | Brak wywołania [`BeginEnumeration`](beginenumeration.md) funkcji. |
| `WBEM_S_NO_ERROR` | 0 | Wywołanie funkcji zakończyło się pomyślnie.  |
| `WBEM_S_NO_MORE_DATA` | 0x40005 | Nie ma więcej właściwości w wyliczeniu. |
  
## <a name="remarks"></a>Uwagi

Ta funkcja otacza wywołanie metody [IWbemClassObject:: NextMethod](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-nextmethod) .

Obiekt wywołujący rozpoczyna sekwencję wyliczenia, wywołując funkcję [BeginMethodEnumeration](beginmethodenumeration.md) , a następnie wywołuje funkcję [NextMethod] do momentu, gdy funkcja zwróci wartość `WBEM_S_NO_MORE_DATA` . Opcjonalnie obiekt wywołujący kończy sekwencję przez wywołanie [EndMethodEnumeration](endmethodenumeration.md). Obiekt wywołujący może zakończyć Wyliczenie wczesne przez wywołanie [EndMethodEnumeration](endmethodenumeration.md) w dowolnym momencie.

## <a name="example"></a>Przykład

Aby zapoznać się z przykładem w języku C++, zobacz [IWbemClassObject:: NextMethod](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-nextmethod) .

## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** WMINet_Utils. idl  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>Zobacz także

- [WMI i liczniki wydajności (niezarządzana dokumentacja interfejsu API)](index.md)
