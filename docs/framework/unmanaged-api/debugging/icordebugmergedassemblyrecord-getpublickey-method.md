---
title: 'ICorDebugMergedAssemblyRecord:: GetPublicKey, Metoda'
ms.date: 03/30/2017
ms.assetid: 6f4e78ba-082b-489d-8b58-4c35fbcc7a5b
ms.openlocfilehash: e89ecca25edb0d7eae3a7e65f9585d71ad4ace4d
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95710600"
---
# <a name="icordebugmergedassemblyrecordgetpublickey-method"></a>ICorDebugMergedAssemblyRecord:: GetPublicKey, Metoda

Pobiera klucz publiczny zestawu.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT GetPublicKey(  
   [in] ULONG32 cbPublicKey,
   [out] ULONG32 *pcbPublicKey,
   [out, size_is(cbPublicKey), length_is(*pcbPublicKey)] BYTE pbPublicKey[]);  
```  
  
## <a name="parameters"></a>Parametry  

 `cbPublicKey`  
 podczas Maksymalna liczba bajtów w `pbPublicKey` tablicy.  
  
 `pcbPublicKey`  
 określoną Wskaźnik do rzeczywistej liczby bajtów zapisanych do `pbPublicKey` tablicy.  
  
 `pbPublicKey`  
 określoną Wskaźnik do tablicy bajtów zawierającej klucz publiczny zestawu.  
  
## <a name="remarks"></a>Uwagi  
  
> [!NOTE]
> Ta metoda jest dostępna tylko z .NET Native.  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorDebug. idl, CorDebug. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **.NET Framework wersje:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [ICorDebugMergedAssemblyRecord, interfejs](icordebugmergedassemblyrecord-interface.md)
- [Debugowanie — Interfejsy](debugging-interfaces.md)
