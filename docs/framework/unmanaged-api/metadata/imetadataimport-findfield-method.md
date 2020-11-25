---
title: IMetaDataImport::FindField — Metoda
ms.date: 03/30/2017
api_name:
- IMetaDataImport.FindField
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::FindField
helpviewer_keywords:
- IMetaDataImport::FindField method [.NET Framework metadata]
- FindField method [.NET Framework metadata]
ms.assetid: 38cd4e16-fbb2-471c-aa73-ac51a1931ad2
topic_type:
- apiref
ms.openlocfilehash: 9b42f0f7c8e2878ee3ec140344f51517a24247c4
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95729866"
---
# <a name="imetadataimportfindfield-method"></a>IMetaDataImport::FindField — Metoda

Pobiera wskaźnik do tokenu FieldDef dla pola, które jest ujęte w określonym <xref:System.Type> i który ma określoną nazwę i sygnaturę metadanych.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT FindField (  
   [in]  mdTypeDef         td,  
   [in]  LPCWSTR           szName,  
   [in]  PCCOR_SIGNATURE   pvSigBlob,  
   [in]  ULONG             cbSigBlob,  
   [out] mdFieldDef        *pmb  
);  
```  
  
## <a name="parameters"></a>Parametry  

 `td`  
 podczas Token TypeDef dla klasy lub interfejsu, który obejmuje pole, które ma zostać wyszukane. Jeśli ta wartość jest `mdTokenNil` , wyszukiwanie jest wykonywane dla zmiennej globalnej.  
  
 `szName`  
 podczas Nazwa pola, które ma zostać wyszukane.  
  
 `pvSigBlob`  
 podczas Wskaźnik do binarnego podpisu metadanych pola.  
  
 `cbSigBlob`  
 podczas Rozmiar w bajtach `pvSigBlob` .  
  
 `pmb`  
 określoną Wskaźnik do zgodnego tokenu FieldDef.  
  
## <a name="remarks"></a>Uwagi  

 Należy określić pole przy użyciu jego klasy lub interfejsu ( `td` ), jego nazwy ( `szName` ) i opcjonalnie jego sygnatury ( `pvSigBlob` ).  
  
 Sygnatura przekazano do `FindField` musi być wygenerowana w bieżącym zakresie, ponieważ sygnatury są powiązane z konkretnym zakresem. Podpis może osadzić token, który identyfikuje otaczającą klasę lub typ wartości. (Token jest indeksem w lokalnej tabeli TypeDef). Nie można utworzyć podpisu w czasie wykonywania poza kontekstem bieżącego zakresu i użyć tej sygnatury jako danych wejściowych `FindField` .  
  
 `FindField` znajduje tylko pola, które zostały zdefiniowane bezpośrednio w klasie lub interfejsie; nie znajdują się w nim dziedziczone pola.  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** Cor. h  
  
 **Biblioteka:** Uwzględnione jako zasób w MsCorEE.dll  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [IMetaDataImport — Interfejs](imetadataimport-interface.md)
- [IMetaDataImport2 — Interfejs](imetadataimport2-interface.md)
