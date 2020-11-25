---
title: ISymUnmanagedBinder::GetReaderForFile — Metoda
ms.date: 03/30/2017
api_name:
- ISymUnmanagedBinder.GetReaderForFile
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedBinder::GetReaderForFile
helpviewer_keywords:
- ISymUnmanagedBinder::GetReaderForFile method [.NET Framework debugging]
- GetReaderForFile method [.NET Framework debugging]
ms.assetid: 46c06258-831e-47c8-a50a-8650af6b637e
topic_type:
- apiref
ms.openlocfilehash: ac895032e70cf31532ab4c73409d6d750eae65df
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95706999"
---
# <a name="isymunmanagedbindergetreaderforfile-method"></a>ISymUnmanagedBinder::GetReaderForFile — Metoda

Podanym interfejsem metadanych i nazwą pliku zwraca poprawny interfejs [ISymUnmanagedReader](isymunmanagedreader-interface.md) , który odczytuje symbole debugowania skojarzone z modułem.  
  
 Ta metoda spowoduje otwarcie pliku bazy danych programu (PDB) tylko wtedy, gdy znajduje się obok pliku wykonywalnego. Ta zmiana została wprowadzona ze względów bezpieczeństwa. Jeśli potrzebujesz bardziej szczegółowego wyszukiwania pliku PDB, użyj metody [ISymUnmanagedBinder2:: GetReaderForFile2 —](isymunmanagedbinder2-getreaderforfile2-method.md) .  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT GetReaderForFile(  
    [in]  IUnknown     *importer,  
    [in]  const WCHAR  *fileName,  
    [in]  const WCHAR  *searchPath,  
    [out, retval] ISymUnmanagedReader  **pRetVal);  
```  
  
## <a name="parameters"></a>Parametry  

 `importer`  
 podczas Wskaźnik do interfejsu importowania metadanych.  
  
 `fileName`  
 podczas Wskaźnik do nazwy pliku.  
  
 `searchPath`  
 podczas Wskaźnik do ścieżki wyszukiwania.  
  
 `pRetVal`  
 określoną Wskaźnik, który jest ustawiony na zwracany Interfejs [ISymUnmanagedReader](isymunmanagedreader-interface.md) .  
  
## <a name="return-value"></a>Wartość zwracana  

 S_OK, jeśli metoda się powiedzie; w przeciwnym razie E_FAIL lub inny kod błędu.  
  
## <a name="requirements"></a>Wymagania  

 **Nagłówek:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Zobacz także

- [ISymUnmanagedBinder — Interfejs](isymunmanagedbinder-interface.md)
- [GetReaderForFile2, metoda](isymunmanagedbinder2-getreaderforfile2-method.md)
