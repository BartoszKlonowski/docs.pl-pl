---
title: CorTokenType — Wyliczenie
ms.date: 03/30/2017
api_name:
- CorTokenType
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorTokenType
helpviewer_keywords:
- CorTokenType enumeration [.NET Framework metadata]
ms.assetid: 93c9a369-225f-4eff-9b78-3fbee4902cf1
topic_type:
- apiref
ms.openlocfilehash: 70b28ab0ca73988093eadb9628142fecd9442948
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95705478"
---
# <a name="cortokentype-enumeration"></a>CorTokenType — Wyliczenie

Wskazuje typ tokenu metadanych.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
typedef enum CorTokenType {  
  
    mdtModule                       = 0x00000000,  
    mdtTypeRef                      = 0x01000000,  
    mdtTypeDef                      = 0x02000000,  
    mdtFieldDef                     = 0x04000000,  
    mdtMethodDef                    = 0x06000000,  
    mdtParamDef                     = 0x08000000,  
    mdtInterfaceImpl                = 0x09000000,  
    mdtMemberRef                    = 0x0a000000,  
    mdtCustomAttribute              = 0x0c000000,  
    mdtPermission                   = 0x0e000000,  
    mdtSignature                    = 0x11000000,  
    mdtEvent                        = 0x14000000,  
    mdtProperty                     = 0x17000000,  
    mdtModuleRef                    = 0x1a000000,  
    mdtTypeSpec                     = 0x1b000000,  
    mdtAssembly                     = 0x20000000,  
    mdtAssemblyRef                  = 0x23000000,  
    mdtFile                         = 0x26000000,  
    mdtExportedType                 = 0x27000000,  
    mdtManifestResource             = 0x28000000,  
    mdtGenericParam                 = 0x2a000000,  
    mdtMethodSpec                   = 0x2b000000,  
    mdtGenericParamConstraint       = 0x2c000000,  
    mdtString                       = 0x70000000,  
    mdtName                         = 0x71000000,  
    mdtBaseType                     = 0x72000000  
  
} CorTokenType;  
```  
  
## <a name="members"></a>Elementy członkowskie  
  
|Członek|Opis|  
|------------|-----------------|  
|`mdtModule`|`mdModule`Token.|  
|`mdtTypeRef`|`mdTypeRef`Token.|  
|`mdtTypeDef`|`mdTypeDef`Token.|  
|`mdtFieldDef`|`mdFieldDef`Token.|  
|`mdtMethodDef`|`mdMethodDef`Token.|  
|`mdtParamDef`|`mdParamDef`Token.|  
|`mdtInterfaceImpl`|`mdInterfaceImpl`Token.|  
|`mdtMemberRef`|`mdMemberRef`Token.|  
|`mdtCustomAttribute`|`mdCustomAttribute`Token.|  
|`mdtPermission`|`mdPermission`Token.|  
|`mdtSignature`|`mdSignature`Token.|  
|`mdtEvent`|`mdEvent`Token.|  
|`mdtProperty`|`mdProperty`Token.|  
|`mdtModuleRef`|`mdModuleRef`Token.|  
|`mdtTypeSpec`|`mdTypeSpec`Token.|  
|`mdtAssembly`|`mdAssembly`Token.|  
|`mdtAssemblyRef`|`mdAssemblyRef`Token.|  
|`mdtFile`|`mdFile`Token.|  
|`mdtExportedType`|`mdExportedType`Token.|  
|`mdtManifestResource`|`mdManifestResource`Token.|  
|`mdtGenericParam`|`mdGenericParam`Token.|  
|`mdtMethodSpec`|`mdMethodSpec`Token.|  
|`mdtGenericParamConstraint`|`mdGenericParamConstraint`Token.|  
|`mdtString`|`mdString`Token.|  
|`mdtName`|`mdName`Token.|  
|`mdtBaseType`|Nie używany.|  
  
## <a name="remarks"></a>Uwagi  

 Każda wartość jest równa wartości górnego bajtu w odpowiednim tokenie metadanych.  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorHdr. h  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [Wyliczenia metadanych](metadata-enumerations.md)
