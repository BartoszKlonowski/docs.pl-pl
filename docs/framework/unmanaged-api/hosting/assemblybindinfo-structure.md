---
title: AssemblyBindInfo — Struktura
ms.date: 03/30/2017
api_name:
- AssemblyBindInfo
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- AssemblyBindInfo
helpviewer_keywords:
- AssemblyBindInfo structure [.NET Framework hosting]
ms.assetid: 6fc01e98-c2e7-49de-ab9f-95937cc89017
topic_type:
- apiref
ms.openlocfilehash: d2ba7d8e66472f771a932a2dfb05bb9e1ee96290
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95685880"
---
# <a name="assemblybindinfo-structure"></a>AssemblyBindInfo — Struktura

Zawiera szczegółowe informacje o przywoływanym zestawie.  
  
## <a name="syntax"></a>Składnia  
  
```cpp  
typedef struct _AssemblyBindInfo {  
    DWORD       dwAppDomainId;  
    LPCWSTR     lpReferencedIdentity;  
    LPCWSTR     lpPostPolicyIdentity;  
    DWORD       ePolicyLevel;  
} AssemblyBindInfo;  
```  
  
## <a name="members"></a>Elementy członkowskie  
  
|Członek|Opis|  
|------------|-----------------|  
|`dwAppDomainId`|Unikatowy identyfikator `IStream` zwracanego przez wywołanie [IHostAssemblyStore::P rovideassembly](ihostassemblystore-provideassembly-method.md), z którego ma zostać załadowany przywoływany zestaw.|  
|`lpReferencedIdentity`|Unikatowy identyfikator dla przywoływanego zestawu.|  
|`lpPostPolicyIdentity`|Identyfikator zestawu, którego dotyczy odwołanie, po zastosowaniu wszystkich wartości zasad powiązań.|  
|`ePolicyLevel`|Jedna z wartości [EPolicyAction —](epolicyaction-enumeration.md) wskazujących, które zasady przechowywania wersji (jeśli istnieją), należy zastosować do przywoływanego zestawu.|  
  
## <a name="remarks"></a>Uwagi  

 Host dostarcza unikatowy identyfikator `dwAppDomainId` do środowiska uruchomieniowego języka wspólnego (CLR). Po wywołaniu `IHostAssemblyStore::ProvideAssembly` zwraca, środowisko uruchomieniowe używa identyfikatora, aby określić, czy zawartość `IStream` została zamapowana. Jeśli tak, środowisko uruchomieniowe ładuje istniejącą kopię zamiast ponownego mapowania strumienia. Środowisko uruchomieniowe używa również tego identyfikatora jako klucza wyszukiwania dla strumieni zwróconych z wywołań do [IHostAssemblyStore::P rovidemodule](ihostassemblystore-providemodule-method.md). W związku z tym identyfikator musi być unikatowy dla żądań modułów i dla żądań zestawu.  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** MSCorEE. idl  
  
 **Biblioteka:** Uwzględnione jako zasób w MSCorEE.dll  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [Hosting — Struktury](hosting-structures.md)
- [ICLRAssemblyIdentityManager — Interfejs](iclrassemblyidentitymanager-interface.md)
- [ICLRAssemblyReferenceList — Interfejs](iclrassemblyreferencelist-interface.md)
- [IHostAssemblyManager — Interfejs](ihostassemblymanager-interface.md)
- [IHostAssemblyStore — Interfejs](ihostassemblystore-interface.md)
- [ModuleBindInfo — Struktura](modulebindinfo-structure.md)
