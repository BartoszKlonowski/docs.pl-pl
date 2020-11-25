---
title: StrongNameSignatureVerificationFromImage — Funkcja
ms.date: 03/30/2017
api_name:
- StrongNameSignatureVerificationFromImage
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- StrongNameSignatureVerificationFromImage
helpviewer_keywords:
- StrongnameSignatureVerificationFromImage function [.NET Framework strong naming]
ms.assetid: 9fb144d2-07e0-4a0e-8e05-907bbb6c9e03
topic_type:
- apiref
ms.openlocfilehash: b90cc6fe99cf592f1b3fd117888462a957e4ce35
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95708429"
---
# <a name="strongnamesignatureverificationfromimage-function"></a>StrongNameSignatureVerificationFromImage — Funkcja

Sprawdza, czy zestaw, który został już zamapowany na pamięć, jest prawidłowy dla skojarzonego klucza publicznego.  
  
 Ta funkcja jest przestarzała. Zamiast tego użyj metody [ICLRStrongName:: StrongNameVerificationFromImage](../hosting/iclrstrongname-strongnamesignatureverificationfromimage-method.md) .  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
BOOLEAN StrongNameSignatureVerificationFromImage (  
    [in]  BYTE    *pbBase,  
    [in]  DWORD   dwLength,  
    [in]  DWORD   dwInFlags,  
    [out] DWORD   *pdwOutFlags  
);  
```  
  
## <a name="parameters"></a>Parametry  

 `pbBase`  
 podczas Względny adres wirtualny zamapowanego manifestu zestawu.  
  
 `dwLength`  
 podczas Rozmiar zamapowanego obrazu w bajtach.  
  
 `dwInFlags`  
 podczas Flagi wpływające na zachowanie weryfikacji. Obsługiwane są następujące wartości:  
  
- `SN_INFLAG_FORCE_VER` (0x00000001) — wymusza weryfikację, nawet jeśli konieczne jest przesłonięcie ustawień rejestru.  
  
- `SN_INFLAG_INSTALL` (0x00000002) — określa, że jest to pierwsza weryfikacja wykonywana na tym obrazie.  
  
- `SN_INFLAG_ADMIN_ACCESS` (0x00000004) — określa, że pamięć podręczna będzie zezwalać na dostęp tylko użytkownikom z uprawnieniami administracyjnymi.  
  
- `SN_INFLAG_USER_ACCESS` (0x00000008) — określa, że zestaw będzie dostępny tylko dla bieżącego użytkownika.  
  
- `SN_INFLAG_ALL_ACCESS` (0x00000010) — określa, że pamięć podręczna nie będzie zapewniać żadnych gwarancji ograniczenia dostępu.  
  
- `SN_INFLAG_RUNTIME` (0x80000000) — zarezerwowane do debugowania wewnętrznego.  
  
 `pdwOutFlags`  
 określoną Flaga dodatkowych informacji wyjściowych. Obsługiwana jest następująca wartość:  
  
- `SN_OUTFLAG_WAS_VERIFIED` (0x00000001) — ta wartość jest ustawiona na `false` , aby określić, że weryfikacja powiodła się z powodu ustawień rejestru.  
  
## <a name="return-value"></a>Wartość zwracana  

 `true` Po pomyślnym zakończeniu; w przeciwnym razie `false` .  
  
## <a name="remarks"></a>Uwagi  

 Jeśli `StrongNameSignatureVerificationFromImage` Funkcja nie zakończy się pomyślnie, wywołaj funkcję [StrongNameErrorInfo —](strongnameerrorinfo-function.md) w celu pobrania ostatniego wygenerowanego błędu.  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** StrongName. h  
  
 **Biblioteka:** Uwzględnione jako zasób w mscoree.dll  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [StrongNameSignatureVerificationFromImage, metoda](../hosting/iclrstrongname-strongnamesignatureverificationfromimage-method.md)
- [ICLRStrongName — Interfejs](../hosting/iclrstrongname-interface.md)
