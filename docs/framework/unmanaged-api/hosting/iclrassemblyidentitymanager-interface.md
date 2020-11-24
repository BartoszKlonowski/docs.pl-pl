---
title: ICLRAssemblyIdentityManager — Interfejs
ms.date: 03/30/2017
api_name:
- ICLRAssemblyIdentityManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRAssemblyIdentityManager
helpviewer_keywords:
- ICLRAssemblyIdentityManager interface [.NET Framework hosting]
ms.assetid: 6a81c6fe-cc22-4062-ae27-d6eeee03a7b9
topic_type:
- apiref
ms.openlocfilehash: 41d049c931091d2cc0b41bd1e9d74b3c15d7878d
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95679263"
---
# <a name="iclrassemblyidentitymanager-interface"></a>ICLRAssemblyIdentityManager — Interfejs

Zapewnia metody obsługujące komunikację między hostem i środowiskiem uruchomieniowym języka wspólnego (CLR) dotyczące zestawów.  
  
## <a name="methods"></a>Metody  
  
|Metoda|Opis|  
|------------|-----------------|  
|[GetBindingIdentityFromFile, metoda](iclrassemblyidentitymanager-getbindingidentityfromfile-method.md)|Pobiera dane powiązania tożsamości zestawu z określoną ścieżką do pliku.|  
|[GetBindingIdentityFromStream, metoda](iclrassemblyidentitymanager-getbindingidentityfromstream-method.md)|Pobiera dane tożsamości zestawu kanonicznego dla zestawu w określonym strumieniu.|  
|[GetCLRAssemblyReferenceList, metoda](iclrassemblyidentitymanager-getclrassemblyreferencelist-method.md)|Pobiera wystąpienie [ICLRAssemblyReferenceList](iclrassemblyreferencelist-interface.md) z podanej listy tożsamości zestawów częściowych.|  
|[GetProbingAssembliesFromReference, metoda](iclrassemblyidentitymanager-getprobingassembliesfromreference-method.md)|Pobiera moduł wyliczający [ICLRProbingAssemblyEnum](iclrprobingassemblyenum-interface.md) dla tożsamości zestawu, do których odwołuje się zestaw z określoną tożsamością.|  
|[GetReferencedAssembliesFromFile, metoda](iclrassemblyidentitymanager-getreferencedassembliesfromfile-method.md)|Pobiera wystąpienie [ICLRReferenceAssemblyEnum](iclrreferenceassemblyenum-interface.md) , które zawiera listę zestawów, do których odwołuje się zestaw w określonej ścieżce pliku.|  
|[GetReferencedAssembliesFromStream, metoda](iclrassemblyidentitymanager-getreferencedassembliesfromstream-method.md)|Pobiera wskaźnik do `ICLRReferenceAssemblyEnum` obiektu, który zawiera dane tożsamości zestawu dla zestawów, do których odwołuje się zestaw w określonym strumieniu.|  
|[IsStronglyNamed, metoda](iclrassemblyidentitymanager-isstronglynamed-method.md)|Pobiera wartość wskazującą, czy określony zestaw ma silną nazwę.|  
  
## <a name="remarks"></a>Uwagi  

 Służy `ICLRAssemblyIdentityManager` do pobierania wystąpień `ICLRAssemblyReferenceList` i wyliczania tożsamości zestawu.  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** MSCorEE. h  
  
 **Biblioteka:** Uwzględnione jako zasób w MSCorEE.dll  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [ICLRAssemblyReferenceList — Interfejs](iclrassemblyreferencelist-interface.md)
- [ICLRProbingAssemblyEnum — Interfejs](iclrprobingassemblyenum-interface.md)
- [Hosting — Interfejsy](hosting-interfaces.md)
