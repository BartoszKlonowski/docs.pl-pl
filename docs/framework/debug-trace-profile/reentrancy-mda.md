---
title: wielobieżność MDA
description: Zapoznaj się z współużytkowania wątkowości MDA, który może zostać aktywowany, jeśli sterta obiektu jest uszkodzona lub występują inne poważne błędy podczas przechodzenia z kodu natywnego do zarządzanego.
ms.date: 03/30/2017
helpviewer_keywords:
- unmanaged code, debugging
- transitioning threads unmanaged to managed code
- reentrancy MDA
- reentrancy without an orderly transition
- managed debugging assistants (MDAs), reentrancy
- illegal reentrancy
- MDAs (managed debugging assistants), reentrancy
- threading [.NET Framework], managed debugging assistants
- managed code, debugging
- native debugging, MDAs
ms.assetid: 7240c3f3-7df8-4b03-bbf1-17cdce142d45
ms.openlocfilehash: 0480b1a5aafbc8c4f9645ba83383d3a222d1f1c5
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96264585"
---
# <a name="reentrancy-mda"></a>wielobieżność MDA

`reentrancy`Asystent debugowania zarządzanego (MDA) jest uaktywniany, gdy podejmowana jest próba przejścia z kodu natywnego na kod zarządzany w przypadkach, gdy wcześniejszy przełącznik z kodu zarządzanego na kod natywny nie został wykonany przy użyciu przejścia uporządkowanego.  
  
## <a name="symptoms"></a>Objawy  

 Sterta obiektu jest uszkodzona lub występują inne poważne błędy podczas przechodzenia z kodu natywnego do zarządzanego.  
  
 Wątki przełączające się między kodem natywnym i zarządzanym w obu kierunkach muszą wykonywać uporządkowane przejścia. Jednak niektóre punkty rozszerzenia niskiego poziomu w systemie operacyjnym, takie jak obsługa wyjątków wektorowych, zezwalają na przełączanie z kodu zarządzanego na natywny bez wykonywania uporządkowanego przejścia.  Te przełączniki są pod kontrolą systemu operacyjnego, a nie pod kontrolą środowiska uruchomieniowego języka wspólnego (CLR).  Każdy kod natywny, który jest wykonywany w tych punktach rozszerzalności, musi unikać wywoływania kodu zarządzanego.  
  
## <a name="cause"></a>Przyczyna  

 Punkt rozszerzalności systemu operacyjnego niskiego poziomu, taki jak program obsługi wyjątków wektorowych, został aktywowany podczas wykonywania kodu zarządzanego.  Kod aplikacji, który jest wywoływany przez ten punkt rozszerzalności, próbuje wywołać kod zarządzany.  
  
 Ten problem jest zawsze spowodowany przez kod aplikacji.  
  
## <a name="resolution"></a>Rozwiązanie  

 Przejrzyj ślad stosu dla wątku, który uaktywnił to MDA.  Wątek próbuje niedozwolone wywołanie w kodzie zarządzanym.  Ślad stosu powinien ujawnić kod aplikacji przy użyciu tego punktu rozszerzalności, kodu systemu operacyjnego, który zapewnia ten punkt rozszerzalności, oraz kodu zarządzanego, który został przerwany przez punkt rozszerzalności.  
  
 Na przykład zobaczysz, że element MDA został aktywowany w trakcie próby wywołania kodu zarządzanego z wewnątrz wektorowego programu obsługi wyjątków.  Na stosie zobaczysz kod obsługi wyjątków systemu operacyjnego i jakiś kod zarządzany wyzwalający wyjątek, taki jak <xref:System.DivideByZeroException> lub <xref:System.AccessViolationException> .  
  
 W tym przykładzie poprawne rozwiązanie polega na zaimplementowaniu w całości kodu niezarządzanego programu obsługi wyjątków.  
  
## <a name="effect-on-the-runtime"></a>Wpływ na środowisko uruchomieniowe  

 To zdarzenie MDA nie ma wpływu na środowisko CLR.  
  
## <a name="output"></a>Dane wyjściowe  

 Podjęto próbę wykonania niedozwolonych współużytkowania wątkowości w raportach MDA.  Sprawdź stos wątku, aby określić, dlaczego dzieje się tak i jak rozwiązać problem. Poniżej przedstawiono przykładowe dane wyjściowe.  
  
```output
Additional Information: Attempting to call into managed code without
transitioning out first.  Do not attempt to run managed code inside
low-level native extensibility points. Managed Debugging Assistant
'Reentrancy' has detected a problem in 'D:\ConsoleApplication1\  
ConsoleApplication1\bin\Debug\ConsoleApplication1.vshost.exe'.  
```  
  
## <a name="configuration"></a>Konfigurowanie  
  
```xml  
<mdaConfig>  
  <assistants>  
    <reentrancy />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="example"></a>Przykład  

 Poniższy przykład kodu powoduje, że może <xref:System.AccessViolationException> zostać zgłoszony.  W przypadku wersji systemu Windows, które obsługują obsługę wyjątków wektorowych, spowoduje to wywołanie zarządzanej procedury obsługi wyjątków zarządzanych.  Jeśli `reentrancy` zdarzenie MDA jest włączone, zostanie aktywowane podczas próby wywołania `MyHandler` z poziomu wektorowego obsługi wyjątków systemu operacyjnego.  
  
```csharp
using System;  
public delegate int ExceptionHandler(IntPtr ptrExceptionInfo);  
  
public class Reenter
{  
    public static ExceptionHandler keepAlive;  
  
    [System.Runtime.InteropServices.DllImport("kernel32", ExactSpelling=true,
        CharSet=System.Runtime.InteropServices.CharSet.Auto)]  
    public static extern IntPtr AddVectoredExceptionHandler(int bFirst,
        ExceptionHandler handler);  
  
    static int MyHandler(IntPtr ptrExceptionInfo)
    {  
        // EXCEPTION_CONTINUE_SEARCH  
        return 0;  
    }  
    void Run() {}  
  
    static void Main()
    {  
        keepAlive = new ExceptionHandler(Reenter.MyHandler);  
        IntPtr ret = AddVectoredExceptionHandler(1, keepAlive);  
        try
        {  
            // Dispatch on null should AV.  
            Reenter r = null;
            r.Run();  
        }
        catch { }  
    }  
}  
```  
  
## <a name="see-also"></a>Zobacz też

- [Diagnozowanie błędów przy użyciu asystentów zarządzanego debugowania](diagnosing-errors-with-managed-debugging-assistants.md)
