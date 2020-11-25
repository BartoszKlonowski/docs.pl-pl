---
title: PublicKeyBlob — Struktura
ms.date: 03/30/2017
api_name:
- PublicKeyBlob
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- PublicKeyBlob
helpviewer_keywords:
- PublicKeyBlob structure [.NET Framework strong naming]
ms.assetid: b9240712-829c-4c8d-9a09-a6e7aa63f63a
topic_type:
- apiref
ms.openlocfilehash: 42cd3cc22fbbb8eb3d5ac44544fce36650b6461f
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95705933"
---
# <a name="publickeyblob-structure"></a>PublicKeyBlob — Struktura

Reprezentuje w formacie binarnym klucz publiczny pary kluczy publiczny/prywatny.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
typedef struct {  
    unsigned int SigAlgId;  
    unsigned int HashAlgId;  
    ULONG cbPublicKey;  
    BYTE PublicKey[1]  
} PublicKeyBlob;
```  
  
## <a name="members"></a>Elementy członkowskie  
  
|Członek|Opis|  
|------------|-----------------|  
|`SigAlgId`|Identyfikator algorytmu podpisu (typu `ALG_ID` , zgodnie z definicją w WinCrypt. h) klucza publicznego.|  
|`HashAlgId`|Identyfikator algorytmu wyznaczania wartości skrótu (typu `ALG_ID` , zgodnie z definicją w WinCrypt. h) klucza publicznego.|  
|`cbPublicKey`|Długość klucza w bajtach.|  
|`PublicKey`|Tablica bajtów o zmiennej długości, która zawiera wartość klucza w formacie zwracanym przez interfejs CryptoAPI.|  
  
## <a name="remarks"></a>Uwagi  

 `PublicKeyBlob`Struktura jest używana przez [StrongNameGetPublicKey —](strongnamegetpublickey-function.md), [StrongNameSignatureGeneration —](strongnamesignaturegeneration-function.md)i inne funkcje silnej nazwy do reprezentowania klucza publicznego pary kluczy publicznych/prywatnych.  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** StrongName. h  
  
 **Biblioteka:** Uwzględnione jako zasób w MsCorEE.dll  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [StrongNameGetPublicKey — Funkcja](strongnamegetpublickey-function.md)
- [StrongNameSignatureGeneration — Funkcja](strongnamesignaturegeneration-function.md)
