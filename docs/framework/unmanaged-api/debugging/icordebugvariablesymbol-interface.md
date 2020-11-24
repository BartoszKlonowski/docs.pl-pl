---
title: ICorDebugVariableSymbol, interfejs
ms.date: 03/30/2017
ms.assetid: 0e58b85e-69bd-41ff-bedb-8cdc8be6a7a2
ms.openlocfilehash: 3d808fd49eb7767f1f48ad4e07d8ba7e47c8f34b
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95679484"
---
# <a name="icordebugvariablesymbol-interface"></a>ICorDebugVariableSymbol, interfejs

Pobiera informacje o symbolach debugowania dla zmiennej.  
  
## <a name="methods"></a>Metody  
  
|Metoda|Opis|  
|------------|-----------------|  
|[GetName — Metoda](icordebugvariablesymbol-getname-method.md)|Pobiera nazwę zmiennej.|  
|[GetSize — Metoda](icordebugvariablesymbol-getsize-method.md)|Pobiera rozmiar zmiennej w bajtach.|  
|[GetSlotIndex, metoda](icordebugvariablesymbol-getslotindex-method.md)|Pobiera indeks gniazda zarządzanego zmiennej lokalnej.|  
|[GetValue — Metoda](icordebugvariablesymbol-getvalue-method.md)|Pobiera wartość zmiennej jako tablicę bajtów.|  
|[SetValue — Metoda](icordebugvariablesymbol-setvalue-method.md)|Przypisuje wartość tablicy bajtów do zmiennej.|  
  
## <a name="remarks"></a>Uwagi  
  
> [!NOTE]
> Ten interfejs jest dostępny tylko dla .NET Native. W przypadku zaimplementowania tego interfejsu dla scenariuszy ICorDebug poza .NET Native, środowisko uruchomieniowe języka wspólnego zignoruje ten interfejs.  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorDebug. idl, CorDebug. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **.NET Framework wersje:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [Debugowanie — Interfejsy](debugging-interfaces.md)
- [Debugowanie](index.md)
