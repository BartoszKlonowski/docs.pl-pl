---
title: IMetaDataEmit2::DefineGenericParam — Metoda
ms.date: 03/30/2017
api_name:
- IMetaDataEmit2.DefineGenericParam
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit2::DefineGenericParam
helpviewer_keywords:
- IMetaDataEmit2::DefineGenericParam method [.NET Framework metadata]
- DefineGenericParam method [.NET Framework metadata]
ms.assetid: 47b2a3b6-907d-43dc-858d-1ae7dca1316a
topic_type:
- apiref
ms.openlocfilehash: c9ff918121e7bb4ee972e674207810358b3f36f2
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95712914"
---
# <a name="imetadataemit2definegenericparam-method"></a>IMetaDataEmit2::DefineGenericParam — Metoda

Tworzy definicję parametru typu ogólnego i pobiera token do tego parametru typu ogólnego.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
HRESULT DefineGenericParam (
    [in]  mdToken         tk,
    [in]  ULONG           ulParamSeq,
    [in]  DWORD           dwParamFlags,
    [in]  LPCWSTR         szname,
    [in]  DWORD           reserved,
    [in]  mdToken         rtkConstraints[],
    [out] mdGenericParam  *pgp  
);  
```  
  
## <a name="parameters"></a>Parametry  

 `tk`  
 podczas `mdTypeDef` Token lub `mdMethodDef` reprezentujący metodę lub konstruktora, dla którego ma zostać zdefiniowany parametr generyczny.  
  
 `ulParamSeq`  
 podczas Indeks parametru generycznego.  
  
 `dwParamFlags`  
 podczas Wartość wyliczenia [CorGenericParamAttr —](corgenericparamattr-enumeration.md) opisująca typ parametru generycznego.  
  
 `szname`  
 podczas Nazwa parametru.  
  
 `reserved`  
 podczas Ten parametr jest zarezerwowany do użytku w przyszłości.  
  
 `rtkConstraints`  
 podczas Tablica zakończona zerem z ograniczeniami typu. Elementy członkowskie tablicy muszą być `mdTypeDef` `mdTypeRef` `mdTypeSpec` tokenami, lub.  
  
 `pgp`  
 określoną Token, który reprezentuje parametr generyczny.  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** Cor. h  
  
 **Biblioteka:** Używane jako zasób w MsCorEE.dll  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [IMetaDataEmit2 — Interfejs](imetadataemit2-interface.md)
- [IMetaDataEmit — Interfejs](imetadataemit-interface.md)
