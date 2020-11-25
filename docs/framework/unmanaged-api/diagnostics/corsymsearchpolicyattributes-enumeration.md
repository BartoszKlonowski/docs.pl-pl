---
title: CorSymSearchPolicyAttributes — Wyliczenie
ms.date: 03/30/2017
api_name:
- CorSymSearchPolicyAttributes
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorSymSearchPolicyAttributes
helpviewer_keywords:
- CorSymSearchPolicyAttributes enumeration [.NET Framework debugging]
ms.assetid: 03abde84-930a-49d3-bac3-23abb34a0184
topic_type:
- apiref
ms.openlocfilehash: 2d5d19fb3fb7c727227827dacbaac2c910ac8b3c
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95725225"
---
# <a name="corsymsearchpolicyattributes-enumeration"></a>CorSymSearchPolicyAttributes — Wyliczenie

Określa zasady, które mają być używane podczas wyszukiwania czytnika symboli. Te stałe są używane przez metody [ISymUnmanagedBinder2:: GetReaderForFile2 —](isymunmanagedbinder2-getreaderforfile2-method.md) i [ISymUnmanagedBinder3:: GetReaderFromCallback —](isymunmanagedbinder3-getreaderfromcallback-method.md) .  
  
> [!IMPORTANT]
> Jest to zagrożenie bezpieczeństwa, aby otworzyć plik bazy danych programu (PDB) z niezaufanego źródła.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
typedef enum CorSymSearchPolicyAttributes  
{  
    AllowRegistryAccess      = 0x1,
    AllowSymbolServerAccess  = 0x2,  
    AllowOriginalPathAccess  = 0x4,     //
    AllowReferencePathAccess = 0x8  
} CorSymSearchPolicyAttributes;  
```  
  
## <a name="members"></a>Elementy członkowskie  
  
|Członek|Opis|  
|------------|-----------------|  
|`AllowRegistryAccess`|Wysyła zapytanie do rejestru pod kątem ścieżek wyszukiwania symboli.|  
|`AllowSymbolServerAccess`|Uzyskuje dostęp do serwera symboli.|  
|`AllowOriginalPathAccess`|Przeszukuje ścieżkę określoną w katalogu debugowania.|  
|`AllowReferencePathAccess`|Wyszukuje PDB w miejscu, gdzie plik. exe jest.|  
  
## <a name="requirements"></a>Wymagania  

 **Nagłówek:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Zobacz także

- [Wyliczenia magazynu symboli diagnostycznych](diagnostics-symbol-store-enumerations.md)
