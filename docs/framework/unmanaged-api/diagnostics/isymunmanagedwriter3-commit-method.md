---
title: ISymUnmanagedWriter3::Commit — Metoda
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter3.Commit
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter3::Commit
helpviewer_keywords:
- Commit method, ISymUnmanagedWriter3 interface [.NET Framework debugging]
- ISymUnmanagedWriter3::Commit method [.NET Framework debugging]
ms.assetid: f6961922-46ec-4d2c-8369-85f880731f37
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: bcfa0c01dc36a68711c42a7e8318cea023b1772f
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/10/2019
ms.locfileid: "67752433"
---
# <a name="isymunmanagedwriter3commit-method"></a>ISymUnmanagedWriter3::Commit — Metoda
Zatwierdza zmiany do tej pory zapisywane do strumienia.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT Commit();  
```  
  
## <a name="return-value"></a>Wartość zwracana  
 S_OK, jeśli metoda się powiedzie; w przeciwnym razie E_FAIL lub innego kodu błędu.  
  
## <a name="requirements"></a>Wymagania  
 **Nagłówek:** CorSym.idl, CorSym.h  
  
## <a name="see-also"></a>Zobacz także

- [ISymUnmanagedWriter3, interfejs](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter3-interface.md)
