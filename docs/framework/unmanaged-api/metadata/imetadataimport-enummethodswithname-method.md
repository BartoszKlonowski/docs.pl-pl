---
title: IMetaDataImport::EnumMethodsWithName — Metoda
ms.date: 03/30/2017
api_name:
- IMetaDataImport.EnumMethodsWithName
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::EnumMethodsWithName
helpviewer_keywords:
- IMetaDataImport::EnumMethodsWithName method [.NET Framework metadata]
- EnumMethodsWithName method [.NET Framework metadata]
ms.assetid: a8624913-2e23-46ad-a0c1-bb8eccbbf20f
topic_type:
- apiref
ms.openlocfilehash: 5b5345fc4819716dc6c2a00323f94546cfc67f32
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95720935"
---
# <a name="imetadataimportenummethodswithname-method"></a>IMetaDataImport::EnumMethodsWithName — Metoda

Wylicza metody, które mają określoną nazwę i które są definiowane przez typ, do którego odwołuje się określony token TypeDef.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT EnumMethodsWithName (  
   [in, out] HCORENUM    *phEnum,  
   [in]  mdTypeDef       cl,  
   [in]  LPCWSTR         szName,  
   [out] mdMethodDef     rMethods[],  
   [in]  ULONG           cMax,  
   [out] ULONG           *pcTokens  
);  
```  
  
## <a name="parameters"></a>Parametry  

 `phEnum`  
 [in. out] Wskaźnik do modułu wyliczającego. Musi ona mieć wartość NULL dla pierwszego wywołania tej metody.  
  
 `cl`  
 podczas Token TypeDef reprezentujący typ, którego metody mają zostać wyliczone.  
  
 `szName`  
 podczas Nazwa, która ogranicza zakres wyliczania.  
  
 `rMethods`  
 określoną Tablica służąca do przechowywania tokenów MethodDef.  
  
 `cMax`  
 podczas Maksymalny rozmiar `rMethods` tablicy.  
  
 `pcTokens`  
 określoną Liczba tokenów MethodDef zwróconych w `rMethods` .  
  
## <a name="remarks"></a>Uwagi  

 Ta metoda wylicza pola i metody, ale nie właściwości ani zdarzenia. W przeciwieństwie do [IMetaDataImport:: EnumMethods —](imetadataimport-enummethods-method.md), `EnumMethodsWithName` odrzuca wszystkie tokeny metody, które nie mają określonej nazwy.  
  
## <a name="return-value"></a>Wartość zwracana  
  
|HRESULT|Opis|  
|-------------|-----------------|  
|`S_OK`|`EnumMethodsWithName` pomyślnie zwrócono.|  
|`S_FALSE`|Brak tokenów do wyliczenia. W takim przypadku `pcTokens` jest równa zero.|  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** Cor. h  
  
 **Biblioteka:** Uwzględnione jako zasób w MsCorEE.dll  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [IMetaDataImport — Interfejs](imetadataimport-interface.md)
- [IMetaDataImport2 — Interfejs](imetadataimport2-interface.md)
