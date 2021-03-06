---
title: ICLRDataTarget2::AllocVirtual — Metoda
ms.date: 03/30/2017
api_name:
- ICLRDataTarget2.AllocVirtual
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICLRDataTarget2::AllocVirtual
helpviewer_keywords:
- ICLRDataTarget2::AllocVirtual method [.NET Framework debugging]
- AllocVirtual method [.NET Framework debugging]
ms.assetid: e3226230-964b-47fb-9f53-d6fdbeda1e9e
topic_type:
- apiref
ms.openlocfilehash: 6d3985919ea7e766db7d07e4ed81484851156ca5
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95723672"
---
# <a name="iclrdatatarget2allocvirtual-method"></a>ICLRDataTarget2::AllocVirtual — Metoda

Wywoływane przez usługi dostępu do danych środowiska uruchomieniowego języka wspólnego (CLR) do przydzielania pamięci w przestrzeni adresowej tego procesu docelowego.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT AllocVirtual(  
    [in] CLRDATA_ADDRESS addr,  
    [in] ULONG32 size,  
    [in] ULONG32 typeFlags,  
    [in] ULONG32 protectFlags,  
    [out] CLRDATA_ADDRESS* virt  
);  
```  
  
## <a name="parameters"></a>Parametry  

 `addr`  
 podczas Wartość określająca `CLRDATA_ADDRESS` żądany adres początkowy pamięci do przydzielenia.  
  
 `size`  
 podczas Rozmiar pamięci do przydzielenia w bajtach.  
  
 `typeFlags`  
 podczas Flagi kontrolujące przydział pamięci. Zobacz funkcję Win32 `VirtualAlloc` .  
  
 `protectFlags`  
 podczas Atrybuty ochrony przydzieloną pamięć. Zobacz funkcję Win32 `VirtualAlloc` .  
  
 `virt`  
 określoną Wskaźnik do `CLRDATA_ADDRESS` wartości, która określa rzeczywisty adres początkowy przydzieloną pamięć.  
  
## <a name="remarks"></a>Uwagi  

 `AllocVirtual`Metoda służy jako otoka logiczna dla `VirtualAlloc` funkcji Win32.  
  
 Ta metoda jest implementowana przez moduł zapisujący aplikacji debugowania.  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** ClrData. idl, ClrData. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [ICLRDataTarget2 — Interfejs](iclrdatatarget2-interface.md)
- [FreeVirtual, metoda](iclrdatatarget2-freevirtual-method.md)
