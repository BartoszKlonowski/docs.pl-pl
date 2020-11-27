---
title: dllMainReturnsFalse MDA
description: Przeczytaj o Asystencie debugowania zarządzanego przez program dllMainReturnsFalse w programie .NET. To zdarzenie MDA zostanie aktywowane w przypadku niepowodzenia inicjacji biblioteki DLL.
ms.date: 03/30/2017
helpviewer_keywords:
- managed debugging assistants (MDAs), DllMain returns false
- DllMainReturnsFalse MDA
- DllMain function
- MDAs (managed debugging assistants), DllMain returns false
ms.assetid: e2abdd04-f571-4b97-8c16-2221b8588429
ms.openlocfilehash: 83f38c4918c1354477627b70a62e60cbdc7de275
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96273519"
---
# <a name="dllmainreturnsfalse-mda"></a>dllMainReturnsFalse MDA

`dllMainReturnsFalse`Asystent debugowania zarządzanego (MDA) jest aktywowany, jeśli zarządzana `DllMain` Funkcja zestawu użytkownika wywołana z powodu DLL_PROCESS_ATTACH, zwraca wartość false.  
  
## <a name="symptoms"></a>Objawy  

 `DllMain`Funkcja zwróciła wartość false, co oznacza, że nie została wykonana prawidłowo. Może to spowodować nieokreślone problemy, ponieważ `DllMain` funkcje zwykle zawierają ważny kod inicjujący.  
  
## <a name="cause"></a>Przyczyna  

 `DllMain`Funkcja jest wywoływana z powodu DLL_PROCESS_ATTACH dla inicjalizacji biblioteki DLL po załadowaniu. Jeśli zwraca wartość FALSE, oznacza to, że inicjowanie biblioteki DLL nie powiodło się.  
  
## <a name="resolution"></a>Rozwiązanie  

 Analizuj kod `DllMain` funkcji nieudanej biblioteki DLL i zidentyfikuj przyczynę niepowodzenia inicjacji.  
  
## <a name="effect-on-the-runtime"></a>Wpływ na środowisko uruchomieniowe  

 To zdarzenie MDA nie ma wpływu na środowisko CLR. Raportuje tylko dane dotyczące wartości zwracanej dla `DllMain` .  
  
## <a name="output"></a>Dane wyjściowe  

 Komunikat informujący o tym `DllMain` , że funkcja wywołana dla przyczyny DLL_PROCESS_ATTACH zwraca wartość false. Należy zauważyć, że to MDA jest uaktywniane tylko wtedy, gdy `DllMain` jest zaimplementowany w kodzie zarządzanym.  
  
## <a name="configuration"></a>Konfigurowanie  
  
```xml  
<mdaConfig>  
  <assistants>  
    <dllMainReturnsFalse />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>Zobacz też

- [Diagnozowanie błędów przy użyciu asystentów zarządzanego debugowania](diagnosing-errors-with-managed-debugging-assistants.md)
