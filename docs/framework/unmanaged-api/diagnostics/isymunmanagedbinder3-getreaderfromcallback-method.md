---
title: ISymUnmanagedBinder3::GetReaderFromCallback — Metoda
ms.date: 03/30/2017
api_name:
- ISymUnmanagedBinder3.GetReaderFromCallback
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedBinder3::GetReaderFromCallback
helpviewer_keywords:
- GetReaderFromCallback method [.NET Framework debugging]
- ISymUnmanagedBinder3::GetReaderFromCallback method [.NET Framework debugging]
ms.assetid: 4ef83bd2-3d8e-499e-8a12-d9d6fd6ced30
topic_type:
- apiref
ms.openlocfilehash: d48c2bdd55e487038048f432c5586d49f393118c
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95706947"
---
# <a name="isymunmanagedbinder3getreaderfromcallback-method"></a>ISymUnmanagedBinder3::GetReaderFromCallback — Metoda

Zezwala użytkownikowi na implementowanie lub dostarczanie za pośrednictwem wywołania zwrotnego albo `IID_IDiaReadExeAtRVACallback` `IID_IDiaReadExeAtOffsetCallback` uzyskanie informacji o katalogu debugowania z pamięci.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT GetReaderFromCallback(  
    [in]  IUnknown     *importer,  
    [in]  const WCHAR  *fileName,  
    [in]  const WCHAR  *searchPath,  
    [in]  ULONG32      searchPolicy,  
    [in]  IUnknown     *callback,  
    [out,retval] ISymUnmanagedReader  **pRetVal);  
```  
  
## <a name="parameters"></a>Parametry  

 `importer`  
 podczas Wskaźnik do interfejsu importowania metadanych.  
  
 `fileName`  
 podczas Wskaźnik do nazwy pliku.  
  
 `searchPath`  
 podczas Wskaźnik do ścieżki wyszukiwania.  
  
 `searchPolicy`  
 podczas Wartość wyliczenia [CorSymSearchPolicyAttributes —](corsymsearchpolicyattributes-enumeration.md) , która określa zasady, które mają być używane podczas wyszukiwania czytnika symboli.  
  
 `callback`  
 podczas Wskaźnik do funkcji wywołania zwrotnego.  
  
 `pRetVal`  
 określoną Wskaźnik, który jest ustawiony na zwracany Interfejs [ISymUnmanagedReader](isymunmanagedreader-interface.md) .  
  
## <a name="return-value"></a>Wartość zwracana  

 S_OK, jeśli metoda się powiedzie; w przeciwnym razie E_FAIL lub inny kod błędu.  
  
## <a name="requirements"></a>Wymagania  

 **Nagłówek:** CorSym. idl  
  
## <a name="see-also"></a>Zobacz także

- [ISymUnmanagedBinder3 — Interfejs](isymunmanagedbinder3-interface.md)
