---
title: ISymUnmanagedReader2 — Interfejs
ms.date: 03/30/2017
api_name:
- ISymUnmanagedReader2
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedReader2
helpviewer_keywords:
- ISymUnmanagedReader2 interface [.NET Framework debugging]
ms.assetid: a01a881b-82a3-4b3e-a3a9-9dc305c2e5f7
topic_type:
- apiref
ms.openlocfilehash: 3f34be833d3ccb5c636d2c5f18ccb6e216ef2c49
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95709079"
---
# <a name="isymunmanagedreader2-interface"></a>ISymUnmanagedReader2 — Interfejs

Reprezentuje czytnik symboli, który zapewnia dostęp do dokumentów, metod i zmiennych w magazynie symboli. Ten interfejs rozszerza interfejs [ISymUnmanagedReader](isymunmanagedreader-interface.md) .  
  
## <a name="methods"></a>Metody  
  
|Metoda|Opis|  
|------------|-----------------|  
|[GetMethodByVersionPreRemap, metoda](isymunmanagedreader2-getmethodbyversionpreremap-method.md)|Pobierz metodę czytnika symboli, używając tokenu metody oraz numeru wersji Edit-and-Continue.|  
|[GetMethodsInDocument, metoda](isymunmanagedreader2-getmethodsindocument-method.md)|Pobiera każdą metodę, która zawiera informacje o wierszu w podanym dokumencie.|  
|[GetSymAttributePreRemap, metoda](isymunmanagedreader2-getsymattributepreremap-method.md)|Pobiera atrybut niestandardowy na podstawie jego nazwy.|  
  
## <a name="requirements"></a>Wymagania  

 **Nagłówek:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Zobacz także

- [Interfejsy magazynu symboli diagnostycznych](diagnostics-symbol-store-interfaces.md)
- [ISymUnmanagedReader — Interfejs](isymunmanagedreader-interface.md)
