---
title: fatalExecutionEngineError MDA
description: Zapoznaj się z asystentem debugowania zarządzanego fatalExecutionEngineError (MDA) w programie .NET, który może zostać aktywowany z powodu nieoczekiwanego zakończenia procesu.
ms.date: 03/30/2017
helpviewer_keywords:
- corrupted CLR
- fatal execution error
- terminated processes
- unexpected terminations
- fatal errors
- MDAs (managed debugging assistants), fatal errors
- process termination
- FatalExecutionEngineError MDA
- managed debugging assistants (MDAs), fatal errors
ms.assetid: 8b559e44-2393-4e4e-8160-7558d37a4a89
ms.openlocfilehash: a9347338d53755b74b3ff291f75cb6b221134130
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96244278"
---
# <a name="fatalexecutionengineerror-mda"></a>fatalExecutionEngineError MDA

`fatalExecutionEngineError`Asystent debugowania zarządzanego (MDA) jest uaktywniany w przypadku wykrycia błędu krytycznego w środowisku uruchomieniowym języka wspólnego (CLR). Proces zostanie zakończony.  
  
## <a name="symptoms"></a>Objawy  

 Nieoczekiwane zakończenie procesu. Nie można ustalić innych objawów, ponieważ awaria środowiska CLR może wystąpić z różnych powodów.  
  
## <a name="cause"></a>Przyczyna  

 Środowisko CLR zostało uszkodzone w sposób krytyczny. Jest to najczęściej spowodowane uszkodzeniem danych, które może być spowodowane przez wiele problemów, takich jak wywołania źle sformułowanej platformy wywołania funkcji i przekazywanie nieprawidłowych danych do środowiska CLR.  
  
## <a name="resolution"></a>Rozwiązanie  

 Włączenie dodatkowych MDA może pomóc w zidentyfikowaniu problemu. Następujący MDA może być szczególnie przydatny w diagnozowaniu problemu:  
  
- [invalidOverlappedToPinvoke](invalidoverlappedtopinvoke-mda.md)  
  
- [overlappedFreeError](overlappedfreeerror-mda.md)  
  
- [pInvokeStackImbalance](pinvokestackimbalance-mda.md)  
  
- [gcUnmanagedToManaged](gcunmanagedtomanaged-mda.md)  
  
- [gcManagedToUnmanaged](gcmanagedtounmanaged-mda.md)  
  
- [callbackOnCollectedDelegate](callbackoncollecteddelegate-mda.md)  
  
- [reportAvOnComRelease](reportavoncomrelease-mda.md)  
  
- [invalidVariant](invalidvariant-mda.md)  
  
- [invalidIUnknown](invalidiunknown-mda.md)  
  
- [raceOnRCWCleanup](raceonrcwcleanup-mda.md)  
  
- [invalidFunctionPointerInDelegate](invalidfunctionpointerindelegate-mda.md)  
  
- [invalidGCHandleCookie](invalidgchandlecookie-mda.md)  
  
## <a name="effect-on-the-runtime"></a>Wpływ na środowisko uruchomieniowe  

 To zdarzenie MDA nie ma wpływu na zachowanie środowiska uruchomieniowego.  
  
## <a name="output"></a>Dane wyjściowe  

 Adres funkcji CLR, która spowodowała błąd krytyczny, identyfikator wątku, w którym wystąpił błąd, oraz kod błędu.  
  
## <a name="configuration"></a>Konfigurowanie  
  
```xml  
<mdaConfig>  
  <assistants>  
    <fatalExecutionEngineError />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>Zobacz też

- <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareMethod%2A>
- <xref:System.Runtime.ConstrainedExecution.Cer>
- [Diagnozowanie błędów przy użyciu asystentów zarządzanego debugowania](diagnosing-errors-with-managed-debugging-assistants.md)
