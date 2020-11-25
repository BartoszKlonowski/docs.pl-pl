---
title: ISymUnmanagedReader2::GetMethodByVersionPreRemap — Metoda
ms.date: 03/30/2017
api_name:
- ISymUnmanagedReader2.GetMethodByVersionPreRemap
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedReader2::GetMethodByVersionPreRemap
helpviewer_keywords:
- GetMethodByVersionPreRemap method [.NET Framework debugging]
- ISymUnmanagedReader2::GetMethodByVersionPreRemap method [.NET Framework debugging]
ms.assetid: 0d144ed4-bdb0-4cac-960c-cb90f4dca173
topic_type:
- apiref
ms.openlocfilehash: 5484242562deaf463b7435ad4e54735a7abee45e
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95730490"
---
# <a name="isymunmanagedreader2getmethodbyversionpreremap-method"></a>ISymUnmanagedReader2::GetMethodByVersionPreRemap — Metoda

Pobiera metodę czytnika symboli, używając tokenu metody oraz numeru wersji Edit-and-Continue. Numery wersji zaczynają się od 1 i zwiększają się za każdym razem, gdy metoda zostanie zmieniona w wyniku operacji Edit-and-Continue.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT GetMethodByVersionPreRemap(  
    [in]  mdMethodDef token,  
    [in]  int version,  
    [out, retval] ISymUnmanagedMethod** pRetVal);  
```  
  
## <a name="parameters"></a>Parametry  

 `token`  
 podczas Token metadanych metody.  
  
 `version`  
 podczas Wersja metody.  
  
 `pRetVal`  
 określoną Wskaźnik do zwracanego interfejsu [ISymUnmanagedMethod](isymunmanagedmethod-interface.md) .  
  
## <a name="return-value"></a>Wartość zwracana  

 S_OK, jeśli metoda się powiedzie; w przeciwnym razie E_FAIL lub inny kod błędu.  
  
## <a name="requirements"></a>Wymagania  

 **Nagłówek:** CorSym. idl. CorSym. h  
  
## <a name="see-also"></a>Zobacz także

- [ISymUnmanagedReader2 — Interfejs](isymunmanagedreader2-interface.md)
