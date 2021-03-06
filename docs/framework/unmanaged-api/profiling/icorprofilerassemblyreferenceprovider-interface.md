---
title: Interfejs ICorProfilerAssemblyReferenceProvider
ms.date: 03/30/2017
api_name:
- ICorProfilerAssemblyReferenceProvider
api_location:
- mscorwks.dll
api_type:
- COM
ms.assetid: 17205116-66e1-4acc-8f01-532fb3867028
topic_type:
- apiref
ms.openlocfilehash: 2cee012be2665f5a7212600ec11e401b18160d8b
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95691399"
---
# <a name="icorprofilerassemblyreferenceprovider-interface"></a>Interfejs ICorProfilerAssemblyReferenceProvider

[Obsługiwane w .NET Framework 4.5.2 i nowszych wersjach]  
  
 Umożliwia programowi Profiler poinformowanie środowiska uruchomieniowego języka wspólnego (CLR) o odwołaniach do zestawu, które Profiler doda do wywołania zwrotnego [ICorProfilerCallback:: ModuleLoadFinished —](icorprofilercallback-moduleloadfinished-method.md) .  
  
## <a name="methods"></a>Metody  
  
|Metoda|Opis|  
|------------|-----------------|  
|[AddAssemblyReference, metoda](icorprofilerassemblyreferenceprovider-addassemblyreference-method.md)|Informuje środowisko CLR odwołania do zestawu, które program Profiler ma dodać do wywołania zwrotnego [ModuleLoadFinished —](icorprofilercallback-moduleloadfinished-method.md) .|  
  
## <a name="remarks"></a>Uwagi  

 Środowisko CLR przekazuje `ICorProfilerAssemblyReferenceProvider` obiekt interfejsu profilera do wywołania zwrotnego [ICorProfilerCallback6:: GetAssemblyReferences](icorprofilercallback6-getassemblyreferences-method.md) . Dzięki temu Profiler będzie informować CLR o odwołaniach do zestawów, które Profiler ma dodać później w [ICorProfilerCallback:: ModuleLoadFinished —](icorprofilercallback-moduleloadfinished-method.md). wywołania zwrotnego. Poprawia to dokładność analizatora zamknięcia odwołań do zestawu środowiska CLR i jego algorytmy umożliwiające określenie, czy zestawy mogą być udostępniane.  
  
 Tego interfejsu można używać tylko w wywołaniu zwrotnym [ICorProfilerCallback6:: GetAssemblyReferences](icorprofilercallback6-getassemblyreferences-method.md) , które przekazuje ten obiekt interfejsu do profilera.  
  
## <a name="requirements"></a>Wymagania  

 **Platformy:** Zobacz [wymagania systemowe](../../get-started/system-requirements.md).  
  
 **Nagłówek:** CorProf. idl, CorProf. h  
  
 **.NET Framework wersje:**[!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]  
  
## <a name="see-also"></a>Zobacz także

- [Interfejsy profilowania](profiling-interfaces.md)
