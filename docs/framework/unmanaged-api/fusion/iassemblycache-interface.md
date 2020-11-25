---
title: IAssemblyCache — Interfejs
ms.date: 03/30/2017
api_name:
- IAssemblyCache
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- IAssemblyCache
helpviewer_keywords:
- IAssemblyCache interface [.NET Framework fusion]
ms.assetid: 71ea170f-872d-4fc5-81b6-27da1dec9b19
topic_type:
- apiref
ms.openlocfilehash: df4f0ba018b55202c22cb90b22b927a9c426c4ed
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95696859"
---
# <a name="iassemblycache-interface"></a>IAssemblyCache — Interfejs

Reprezentuje globalną pamięć podręczną zestawów do użycia przez technologię Fusion.  
  
## <a name="methods"></a>Metody  
  
|Metoda|Opis|  
|------------|-----------------|  
|[CreateAssemblyCacheItem, metoda](iassemblycache-createassemblycacheitem-method.md)|Pobiera odwołanie do nowego [IAssemblyCacheItem](iassemblycacheitem-interface.md).|  
|[CreateAssemblyScavenger, metoda](iassemblycache-createassemblyscavenger-method.md)|Zarezerwowane do użytku wewnętrznego przez technologię Fusion.|  
|[InstallAssembly, metoda](iassemblycache-installassembly-method.md)|Instaluje określony zestaw w globalnej pamięci podręcznej zestawów.|  
|[QueryAssemblyInfo, metoda](iassemblycache-queryassemblyinfo-method.md)|Pobiera żądane dane dotyczące określonego zestawu.|  
|[UninstallAssembly, metoda](iassemblycache-uninstallassembly-method.md)|Odinstalowuje określony zestaw z globalnej pamięci podręcznej zestawów.|  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** Fusion. h  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [Interfejsy łączenia](fusion-interfaces.md)
- [Global Assembly Cache](../../app-domains/gac.md)
