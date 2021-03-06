---
title: 'ICorDebugMutableDataTarget:: SetThreadContext —, Metoda'
ms.date: 03/30/2017
ms.assetid: 8c0d01d5-67e5-4522-9ccf-c8f3a78cb4fd
ms.openlocfilehash: 558a1ee2eb0ac06213c2ebcebbd5595b69ecc43e
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95695713"
---
# <a name="icordebugmutabledatatargetsetthreadcontext-method"></a>ICorDebugMutableDataTarget:: SetThreadContext —, Metoda

Ustawia kontekst (wartości rejestru) dla wątku.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT SetThreadContext(  
   [in] DWORD dwThreadID,  
   [in] ULONG32 contextSize,   [in, size_is(contextSize)] const BYTE * pContext);  
```  
  
## <a name="parameters"></a>Parametry  

 `dwThreadID`  
 podczas Identyfikator wątku zdefiniowanego przez system operacyjny.  
  
 `contextSize`  
 podczas Rozmiar `pContext` buforu, który ma zostać zapisany.  
  
 `pContext`  
 podczas Wskaźnik do bajtów do zapisania.  
  
## <a name="remarks"></a>Uwagi  

 `SetThreadContext`Metoda aktualizuje bieżący kontekst dla wątku określonego przez argument zdefiniowany przez system operacyjny `dwThreadID` . Format rekordu kontekstu jest określany przez platformę wskazywaną przez metodę [ICorDebugDataTarget:: GetPlatform](icordebugdatatarget-getplatform-method.md) . W systemie Windows jest to struktura [kontekstu](/windows/win32/api/winnt/ns-winnt-arm64_nt_context) .  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorDebug. idl, CorDebug. h  
  
 **Biblioteka:** CorGuids. lib  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v46plus](../../../../includes/net-current-v46plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [ICorDebugMutableDataTarget, interfejs](icordebugmutabledatatarget-interface.md)
- [Debugowanie — Interfejsy](debugging-interfaces.md)
