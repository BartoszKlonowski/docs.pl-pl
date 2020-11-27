---
title: raceOnRCWCleanup MDA
description: Zapoznaj się z asystentem debugowania zarządzanego raceOnRCWCleanup (MDA), który jest uaktywniany, gdy Otoka RCW jest używana w innym wątku lub na wolnym stosie wątków w programie .NET.
ms.date: 03/30/2017
helpviewer_keywords:
- RCW
- managed debugging assistants (MDAs), RCWs
- race on RCW cleanup
- MDAs (managed debugging assistants), RCWs
- RaceOnRCWCleanup MDA
- runtime callable wrappers
ms.assetid: bee1e9b1-50a8-4c89-9cd9-7dd6b2458187
ms.openlocfilehash: 393c5ea44108445a9a1a9d16e7d1d192eced5740
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96271450"
---
# <a name="raceonrcwcleanup-mda"></a>raceOnRCWCleanup MDA

`raceOnRCWCleanup`Asystent debugowania zarządzanego (MDA) jest uaktywniany, gdy środowisko uruchomieniowe języka wspólnego (CLR) wykryje, że w [środowisku uruchomieniowym](../../standard/native-interop/runtime-callable-wrapper.md) (otoka), gdy wywołanie do wydania jest używane, za pomocą polecenia, takiego jak <xref:System.Runtime.InteropServices.Marshal.ReleaseComObject%2A?displayProperty=nameWithType> Metoda.  
  
## <a name="symptoms"></a>Objawy  

 Naruszenia zasad dostępu lub uszkodzenia pamięci w trakcie lub po zwolnieniu otoki RCW przy użyciu <xref:System.Runtime.InteropServices.Marshal.ReleaseComObject%2A> metody lub podobnej.  
  
## <a name="cause"></a>Przyczyna  

 Otoka RCW jest używana w innym wątku lub na stosie wolnego wątku.  Nie można zwolnić otoki RCW, która jest używana.  
  
## <a name="resolution"></a>Rozwiązanie  

 Nie zwalniaj otoki RCW, która może być używana w bieżącym lub w innych wątkach.  
  
## <a name="effect-on-the-runtime"></a>Wpływ na środowisko uruchomieniowe  

 To zdarzenie MDA nie ma wpływu na środowisko CLR.  
  
## <a name="output"></a>Dane wyjściowe  

 Komunikat z opisem błędu.  
  
## <a name="configuration"></a>Konfigurowanie  
  
```xml  
<mdaConfig>  
  <assistants>  
    <raceOnRCWCleanup/>  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>Zobacz też

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [Diagnozowanie błędów przy użyciu asystentów zarządzanego debugowania](diagnosing-errors-with-managed-debugging-assistants.md)
- [Organizowanie międzyoperacyjne](../interop/interop-marshaling.md)
