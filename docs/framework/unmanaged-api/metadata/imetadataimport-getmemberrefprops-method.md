---
title: IMetaDataImport::GetMemberRefProps — Metoda
ms.date: 03/30/2017
api_name:
- IMetaDataImport.GetMemberRefProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetMemberRefProps
helpviewer_keywords:
- GetMemberRefProps method [.NET Framework metadata]
- IMetaDataImport::GetMemberRefProps method [.NET Framework metadata]
ms.assetid: 0ea73055-ece0-4151-a094-414c88ef8941
topic_type:
- apiref
ms.openlocfilehash: 3237b67f8f711e9ef213d6fc66f1513c534fbdeb
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95733207"
---
# <a name="imetadataimportgetmemberrefprops-method"></a>IMetaDataImport::GetMemberRefProps — Metoda

Pobiera metadane skojarzone z elementem członkowskim, do którego odwołuje się określony token.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT GetMemberRefProps (  
   [in]  mdMemberRef       mr,
   [out] mdToken           *ptk,
   [out] LPWSTR            szMember,
   [in]  ULONG             cchMember,
   [out] ULONG             *pchMember,
   [out] PCCOR_SIGNATURE   *ppvSigBlob,
   [out] ULONG             *pbSig
);  
```  
  
## <a name="parameters"></a>Parametry  

 `mr`  
 podczas Token elementu MemberRef do zwrócenia skojarzonych metadanych.  
  
 `ptk`  
 określoną Element TypeDef lub TypeRef albo token elementu TypeSpec reprezentujący klasę, która deklaruje element członkowski lub token elementu ModuleRef reprezentujący klasę modułu, która deklaruje element członkowski, lub element MethodDef reprezentujący element członkowski.  
  
 `szMember`  
 określoną Bufor ciągu dla nazwy elementu członkowskiego.  
  
 `cchMember`  
 podczas Żądany rozmiar w postaci znaków dwubajtowych `szMember` .  
  
 `pchMember`  
 określoną Zwrócony rozmiar w postaci znaków dwubajtowych `szMember` .  
  
 `ppvSibBlob`  
 określoną Wskaźnik do binarnego podpisu metadanych dla elementu członkowskiego.  
  
 `pbSig`  
 określoną Rozmiar w bajtach `ppvSigBlob` .  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** Cor. h  
  
 **Biblioteka:** Uwzględnione jako zasób w MsCorEE.dll  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [IMetaDataImport — Interfejs](imetadataimport-interface.md)
- [IMetaDataImport2 — Interfejs](imetadataimport2-interface.md)
