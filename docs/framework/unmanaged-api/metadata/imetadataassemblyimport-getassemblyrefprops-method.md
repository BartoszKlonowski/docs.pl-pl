---
title: IMetaDataAssemblyImport::GetAssemblyRefProps — Metoda
ms.date: 03/30/2017
api_name:
- IMetaDataAssemblyImport.GetAssemblyRefProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataAssemblyImport::GetAssemblyRefProps
helpviewer_keywords:
- IMetaDataAssemblyImport::GetAssemblyRefProps method [.NET Framework metadata]
- GetAssemblyRefProps method [.NET Framework metadata]
ms.assetid: 5c6b7fb4-cbca-4479-b650-ab9a99732ea0
topic_type:
- apiref
ms.openlocfilehash: 25aefff46f7557f89f27d1eccab58c9c70d2d13e
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95722118"
---
# <a name="imetadataassemblyimportgetassemblyrefprops-method"></a>IMetaDataAssemblyImport::GetAssemblyRefProps — Metoda

Pobiera zestaw właściwości dla odwołania do zestawu z określonym podpisem metadanych.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT GetAssemblyRefProps (  
    [in]  mdAssemblyRef        mdar,
    [out] const void          **ppbPublicKeyOrToken,
    [out] ULONG                *pcbPublicKeyOrToken,
    [out] LPWSTR               szName,
    [in]  ULONG                cchName,
    [out] ULONG                *pchName,
    [out] ASSEMBLYMETADATA     *pMetaData,
    [out] const void           **ppbHashValue,
    [out] ULONG                *pcbHashValue,
    [out] DWORD                *pdwAssemblyRefFlags  
);  
```  
  
## <a name="parameters"></a>Parametry  

 `mdar`  
 podczas `mdAssemblyRef` Token metadanych reprezentujący odwołanie do zestawu, dla którego mają zostać pobrane właściwości.  
  
 `ppbPublicKeyOrToken`  
 określoną Wskaźnik do klucza publicznego lub tokenu metadanych.  
  
 `pcbPublicKeyOrToken`  
 określoną Liczba bajtów w zwracanym kluczu publicznym lub tokenie.  
  
 `szName`  
 określoną Prosta nazwa zestawu.  
  
 `cchName`  
 podczas Rozmiar, w postaci szerokich znaków, z `szName` .  
  
 `pchName`  
 określoną Wskaźnik do liczby znaków dwubajtowych faktycznie zwróconych w `szName` .  
  
 `pMetaData`  
 określoną Wskaźnik do struktury ASSEMBLYMETADATA, która zawiera metadane zestawu.  
  
 `ppbHashValue`  
 określoną Wskaźnik do wartości skrótu. Jest to skrót, przy użyciu algorytmu SHA-1 `PublicKey` Właściwości zestawu, którego dotyczy odwołanie, chyba że ustawiona jest flaga arfFullOriginator wyliczenia [AssemblyRefFlags —](assemblyrefflags-enumeration.md) .  
  
 `pcbHashValue`  
 określoną Liczba znaków dwubajtowych w zwracanej wartości skrótu.  
  
 `pdwAssemblyRefFlags`  
 określoną Wskaźnik do flag, które opisują metadane zastosowane do zestawu. Wartość flags jest kombinacją co najmniej jednej wartości [CorAssemblyFlags —](corassemblyflags-enumeration.md) .  
  
## <a name="return-value"></a>Wartość zwracana  

 Ta metoda zwraca S_OK, jeśli zakończy się pomyślnie; w przeciwnym razie zwraca jeden z kodów błędów zdefiniowanych w pliku nagłówkowym Winerror. h.  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** Cor. h  
  
 **Biblioteka:** Używane jako zasób w MsCorEE.dll  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [IMetaDataAssemblyImport — Interfejs](imetadataassemblyimport-interface.md)
