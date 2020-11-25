---
title: ISymUnmanagedWriter::CloseScope — Metoda
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter.CloseScope
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter::CloseScope
helpviewer_keywords:
- CloseScope method [.NET Framework debugging]
- ISymUnmanagedWriter::CloseScope method [.NET Framework debugging]
ms.assetid: 6dade525-7770-4cb4-bafd-4bb995ad0d87
topic_type:
- apiref
ms.openlocfilehash: 561a6348b9976789b02961fadb37d9127f5a6a13
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95713044"
---
# <a name="isymunmanagedwriterclosescope-method"></a>ISymUnmanagedWriter::CloseScope — Metoda

Zamyka bieżący zakres leksykalny.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT CloseScope(  
    [in] ULONG32 endOffset);  
```  
  
## <a name="parameters"></a>Parametry  

 `endOffset`  
 podczas Przesunięcie od początku metody punktu na końcu ostatniej instrukcji w zakresie leksykalnym w bajtach.  
  
## <a name="return-value"></a>Wartość zwracana  

 S_OK, jeśli metoda się powiedzie; w przeciwnym razie E_FAIL lub inny kod błędu.  
  
## <a name="remarks"></a>Uwagi  

 Po zamknięciu zakresu nie można w nim definiować więcej zmiennych.  
  
 [ISymUnmanagedWriter:: OpenScope —](isymunmanagedwriter-openscope-method.md) zwraca nieprzezroczysty identyfikator zakresu, który może być używany z [ISymUnmanagedWriter:: SetScopeRange —](isymunmanagedwriter-setscoperange-method.md) w celu późniejszego zdefiniowania początkowego i końcowego przesunięcia zakresu. W takim przypadku przesunięcia przechodzą do `ISymUnmanagedWriter::OpenScope` i `ISymUnmanagedWriter::CloseScope` są ignorowane. Identyfikatory zakresów są prawidłowe tylko w bieżącej metodzie.  
  
## <a name="requirements"></a>Wymagania  

 **Nagłówek:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Zobacz także

- [ISymUnmanagedWriter — Interfejs](isymunmanagedwriter-interface.md)
