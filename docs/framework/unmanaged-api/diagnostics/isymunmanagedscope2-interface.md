---
title: ISymUnmanagedScope2 — Interfejs
ms.date: 03/30/2017
api_name:
- ISymUnmanagedScope2
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedScope2
helpviewer_keywords:
- ISymUnmanagedScope2 interface [.NET Framework debugging]
ms.assetid: 2ed6a387-ba45-483e-9a1e-b0c69f67998b
topic_type:
- apiref
ms.openlocfilehash: 40c437e109eaa4352a83c5566185593cbc6b0eba
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95725836"
---
# <a name="isymunmanagedscope2-interface"></a>ISymUnmanagedScope2 — Interfejs

Reprezentuje zakres leksykalny w ramach metody. Ten interfejs rozszerza interfejs [ISymUnmanagedScope](isymunmanagedscope-interface.md) z metodami, które pobierają informacje o stałych zdefiniowanych w zakresie.  
  
## <a name="methods"></a>Metody  
  
|Metoda|Opis|  
|------------|-----------------|  
|[GetConstantCount, metoda](isymunmanagedscope2-getconstantcount-method.md)|Pobiera liczbę stałych zdefiniowanych w tym zakresie.|  
|[GetConstants, metoda](isymunmanagedscope2-getconstants-method.md)|Pobiera stałe lokalne zdefiniowane w tym zakresie.|  
  
## <a name="requirements"></a>Wymagania  

 **Nagłówek:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Zobacz także

- [Interfejsy magazynu symboli diagnostycznych](diagnostics-symbol-store-interfaces.md)
- [ISymUnmanagedScope — Interfejs](isymunmanagedscope-interface.md)
