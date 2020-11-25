---
title: ISymUnmanagedMethod — Interfejs
ms.date: 03/30/2017
api_name:
- ISymUnmanagedMethod
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedMethod
helpviewer_keywords:
- ISymUnmanagedMethod interface [.NET Framework debugging]
ms.assetid: f204d74c-cc79-4092-83bb-60654be95649
topic_type:
- apiref
ms.openlocfilehash: b72a77fecd15a43efbddd9dfd4618897c3372f88
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95699277"
---
# <a name="isymunmanagedmethod-interface"></a>ISymUnmanagedMethod — Interfejs

Reprezentuje metodę w magazynie symboli. Ten interfejs zapewnia dostęp tylko do atrybutów związanych z symbolami metody, a nie atrybutów związanych z typem.  
  
## <a name="methods"></a>Metody  
  
|Metoda|Opis|  
|------------|-----------------|  
|[GetNamespace, metoda](isymunmanagedmethod-getnamespace-method.md)|Pobiera przestrzeń nazw, w której jest zdefiniowana ta metoda.|  
|[GetOffset — Metoda](isymunmanagedmethod-getoffset-method.md)|Zwraca przesunięcie w ramach tej metody, które odnosi się do danej pozycji w dokumencie.|  
|[GetParameters, metoda](isymunmanagedmethod-getparameters-method.md)|Pobiera parametry dla tej metody.|  
|[GetRanges, metoda](isymunmanagedmethod-getranges-method.md)|Nadana pozycja w dokumencie zwraca tablicę par przesunięć początkowych i końcowych odpowiadających zakresom języka pośredniego firmy Microsoft (MSIL), który znajduje się w tej metodzie.|  
|[GetRootScope, metoda](isymunmanagedmethod-getrootscope-method.md)|Pobiera zakres leksykalny głównej w ramach tej metody. Ten zakres obejmuje całą metodę.|  
|[GetScopeFromOffset, metoda](isymunmanagedmethod-getscopefromoffset-method.md)|Pobiera najbardziej otaczający zakres leksykalny w ramach tej metody, który obejmuje określone przesunięcie.|  
|[GetSequencePointCount, metoda](isymunmanagedmethod-getsequencepointcount-method.md)|Pobiera liczbę punktów sekwencji w tej metodzie.|  
|[GetSequencePoints, metoda](isymunmanagedmethod-getsequencepoints-method.md)|Pobiera wszystkie punkty sekwencji w tej metodzie.|  
|[GetSourceStartEnd, metoda](isymunmanagedmethod-getsourcestartend-method.md)|Pobiera położenie początku i końca dokumentu dla źródła tej metody.|  
|[GetToken — Metoda](isymunmanagedmethod-gettoken-method.md)|Zwraca token metadanych dla tej metody.|  
  
## <a name="requirements"></a>Wymagania  

 **Nagłówek:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Zobacz także

- [Interfejsy magazynu symboli diagnostycznych](diagnostics-symbol-store-interfaces.md)
