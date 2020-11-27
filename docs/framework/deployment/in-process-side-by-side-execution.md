---
title: Wykonywanie równoczesne i wewnątrzprocesowe
description: Obsługa w procesie równoczesnego wykonywania wielu wersji środowiska uruchomieniowego języka wspólnego (CLR) w pojedynczym procesie platformy .NET.
ms.date: 03/30/2017
helpviewer_keywords:
- in-process side-by-side execution
- side-by-side execution, in-process
ms.assetid: 18019342-a810-4986-8ec2-b933a17c2267
ms.openlocfilehash: 85d0ec90a8877384517e9de3b56258d294e0c612
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96283487"
---
# <a name="in-process-side-by-side-execution"></a>Wykonywanie równoczesne i wewnątrzprocesowe

Począwszy od .NET Framework 4, można użyć w procesie równoczesnego hostowania do uruchamiania wielu wersji środowiska uruchomieniowego języka wspólnego (CLR) w ramach jednego procesu. Domyślnie zarządzane składniki COM są uruchamiane z .NET Framework wersją, z którą zostały skompilowane, niezależnie od wersji .NET Framework, która jest ładowana dla tego procesu.  
  
## <a name="background"></a>Tło  

 .NET Framework zawsze udostępnia hosting równoczesny dla aplikacji z kodem zarządzanym, ale przed .NET Framework 4, nie zapewniał on funkcji zarządzanych składników COM. W przeszłości zarządzane składniki COM, które zostały załadowane do procesu, działały z wersją środowiska uruchomieniowego, które zostało już załadowane lub z najnowszą zainstalowaną wersją .NET Framework. Jeśli ta wersja nie jest zgodna ze składnikiem COM, składnik ten nie powiedzie się.  
  
 .NET Framework 4 zawiera nowe podejście do hostingu równoczesnego, które zapewnia następujące działania:  
  
- Zainstalowanie nowej wersji .NET Framework nie ma wpływu na istniejące aplikacje.  
  
- Aplikacje działają w porównaniu z wersją .NET Framework, z którą zostały skompilowane. Nie używają nowej wersji .NET Framework, chyba że jest to wyraźnie ukierunkowane. Jest to jednak łatwiejsze w aplikacjach do przechodzenia do korzystania z nowej wersji .NET Framework.  
  
## <a name="effects-on-users-and-developers"></a>Efekty dla użytkowników i deweloperów  
  
- **Użytkownicy końcowi i Administratorzy systemu**. Ci użytkownicy mogą teraz mieć większą pewność, że podczas instalowania nowej wersji środowiska uruchomieniowego niezależnie lub z aplikacją nie będą mieć wpływu na komputery. Istniejące aplikacje będą nadal działać tak jak wcześniej.  
  
- **Deweloperzy aplikacji**. Hosting równoległy nie ma prawie żadnego wpływu na deweloperów aplikacji. Domyślnie aplikacje są zawsze uruchamiane w porównaniu z wersją .NET Framework, w których zostały skompilowane; Ta zmiana nie została zmieniona. Deweloperzy mogą jednak zastąpić to zachowanie i skierować aplikację do uruchamiania w nowszej wersji .NET Framework (patrz [Scenariusz 2](#scenarios)).  
  
- **Deweloperzy biblioteki i konsumenci**. Hosting równoległy nie rozwiązuje problemów ze zgodnością, które są używane przez deweloperów biblioteki. Biblioteka, która jest bezpośrednio ładowana przez aplikację — albo za pośrednictwem bezpośredniego odwołania lub <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> wywołania — kontynuuje używanie środowiska uruchomieniowego, który <xref:System.AppDomain> jest ładowany do. Należy przetestować biblioteki dla wszystkich wersji .NET Framework, które mają być obsługiwane. Jeśli aplikacja jest kompilowana przy użyciu środowiska uruchomieniowego .NET Framework 4, ale zawiera bibliotekę, która została skompilowana przy użyciu wcześniejszego środowiska uruchomieniowego, biblioteka będzie używać środowiska uruchomieniowego .NET Framework 4. Jeśli jednak masz aplikację, która została skompilowana przy użyciu wcześniejszego środowiska uruchomieniowego i biblioteki, która została skompilowana przy użyciu .NET Framework 4, musisz wymusić, aby aplikacja korzystała również z .NET Framework 4 (patrz [Scenariusz 3](#scenarios)).  
  
- **Zarządzani Deweloperzy składników modelu COM**. W przeszłości zarządzane składniki COM zostały automatycznie uruchomione przy użyciu najnowszej wersji środowiska uruchomieniowego zainstalowanej na komputerze. Teraz można wykonywać składniki COM względem wersji środowiska uruchomieniowego, które zostały skompilowane przy użyciu programu.  
  
     Zgodnie z poniższą tabelą składniki, które zostały skompilowane przy użyciu .NET Framework w wersji 1,1 mogą działać obok składników w wersji 4, ale nie mogą być uruchamiane z wersjami 2,0, 3,0 lub 3,5, ponieważ nie są dostępne dla tych wersji.  
  
    |Wersja programu .NET Framework|1,1|2,0 – 3,5|4|  
    |----------------------------|---------|----------------|-------|  
    |1,1|Nie dotyczy|Nie|Tak|  
    |2,0 – 3,5|Nie|Nie dotyczy|Tak|  
    |4|Tak|Tak|Nie dotyczy|  
  
> [!NOTE]
> .NET Framework wersje 3,0 i 3,5 są kompilowane przyrostowo w wersji 2,0 i nie muszą być uruchamiane obok siebie. Są one w tej samej wersji.  
  
<a name="scenarios"></a>

## <a name="common-side-by-side-hosting-scenarios"></a>Typowe scenariusze hostingu równoczesnego  
  
- **Scenariusz 1:** Aplikacja natywna, która korzysta ze składników COM utworzonych przy użyciu wcześniejszych wersji .NET Framework.  
  
     Zainstalowane wersje .NET Framework: .NET Framework 4 i wszystkie pozostałe wersje .NET Framework używane przez składniki COM.  
  
     Co należy zrobić: w tym scenariuszu nic nie rób. Składniki COM będą działać z wersją .NET Framework, w których zostały zarejestrowane.  
  
- **Scenariusz 2**: zarządzana aplikacja skompilowana z .NET Framework 2,0 SP1, którą wolisz uruchomić przy użyciu .NET Framework 2,0, ale chcemy działać na .NET Framework 4, jeśli wersja 2,0 nie jest obecna.  
  
     Zainstalowane wersje .NET Framework: wcześniejsza wersja .NET Framework i .NET Framework 4.  
  
     Co należy zrobić: w [pliku konfiguracji aplikacji](../configure-apps/index.md) w katalogu aplikacji użyj [ \<startup> elementu](../configure-apps/file-schema/startup/startup-element.md) i zestawu [ \<supportedRuntime> elementów](../configure-apps/file-schema/startup/supportedruntime-element.md) w następujący sposób:  
  
    ```xml  
    <configuration>  
      <startup >  
        <supportedRuntime version="v2.0.50727" />  
        <supportedRuntime version="v4.0" />  
      </startup>  
    </configuration>  
    ```  
  
- **Scenariusz 3:** Aplikacja natywna korzystająca ze składników COM utworzonych przy użyciu wcześniejszych wersji .NET Framework, które mają być uruchamiane z .NET Framework 4.  
  
     Zainstalowane wersje .NET Framework: .NET Framework 4.  
  
     Co należy zrobić: w pliku konfiguracji aplikacji w katalogu aplikacji użyj `<startup>` elementu z `useLegacyV2RuntimeActivationPolicy` atrybutem ustawionym na `true` i `<supportedRuntime>` zestaw elementów w następujący sposób:  
  
    ```xml  
    <configuration>  
      <startup useLegacyV2RuntimeActivationPolicy="true">  
        <supportedRuntime version="v4.0" />  
      </startup>  
    </configuration>  
    ```  
  
## <a name="example"></a>Przykład  

 Poniższy przykład ilustruje niezarządzany host COM, na którym działa zarządzany składnik COM przy użyciu wersji .NET Framework, do której składnik został skompilowany.  
  
 Aby uruchomić Poniższy przykład, skompiluj i zarejestruj następujący zarządzany składnik COM przy użyciu .NET Framework 3,5. Aby zarejestrować składnik, w menu **projekt** kliknij polecenie **Właściwości**, kliknij kartę **kompilacja** , a następnie zaznacz pole wyboru **Zarejestruj dla międzyoperacyjności modelu COM** .  
  
```csharp
using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.Text;  
using System.Runtime.InteropServices;  
  
namespace BasicComObject  
{  
    [ComVisible(true), Guid("9C99C4B5-CA54-4c58-8988-49B6811BA53B")]  
    public class MyObject : SimpleObjectModel.IPrintInfo  
    {  
        public MyObject()  
        {  
        }  
        public void PrintInfo()  
        {  
            Console.WriteLine("MyObject was activated in {0} runtime in:\n\tAppDomain {1}:{2}", System.Runtime.InteropServices.RuntimeEnvironment.GetSystemVersion(), AppDomain.CurrentDomain.Id, AppDomain.CurrentDomain.FriendlyName);  
        }  
    }  
}  
```  
  
 Skompiluj następującą niezarządzaną aplikację C++, która aktywuje obiekt COM, który został utworzony w poprzednim przykładzie.  
  
```cpp
#include "stdafx.h"  
#include <string>  
#include <iostream>  
#include <objbase.h>  
#include <string.h>  
#include <process.h>  
  
using namespace std;  
  
int _tmain(int argc, _TCHAR* argv[])  
{  
    char input;  
    CoInitialize(NULL) ;  
    CLSID clsid;  
    HRESULT hr;  
    HRESULT clsidhr = CLSIDFromString(L"{9C99C4B5-CA54-4c58-8988-49B6811BA53B}",&clsid);  
    hr = -1;  
    if (FAILED(clsidhr))  
    {  
        printf("Failed to construct CLSID from String\n");  
    }  
    UUID id = __uuidof(IUnknown);  
    IUnknown * pUnk = NULL;  
    hr = ::CoCreateInstance(clsid,NULL,CLSCTX_INPROC_SERVER,id,(void **) &pUnk);  
    if (FAILED(hr))  
    {  
        printf("Failed CoCreateInstance\n");  
    }else  
    {  
        pUnk->AddRef();  
        printf("Succeeded\n");  
    }  
  
    DISPID dispid;  
    IDispatch* pPrintInfo;  
    pUnk->QueryInterface(IID_IDispatch, (void**)&pPrintInfo);  
    OLECHAR FAR* szMethod[1];  
    szMethod[0]=OLESTR("PrintInfo");
    hr = pPrintInfo->GetIDsOfNames(IID_NULL,szMethod, 1, LOCALE_SYSTEM_DEFAULT, &dispid);  
    DISPPARAMS dispparams;  
    dispparams.cNamedArgs = 0;  
    dispparams.cArgs = 0;  
    VARIANTARG* pvarg = NULL;  
    EXCEPINFO * pexcepinfo = NULL;  
    WORD wFlags = DISPATCH_METHOD ;  
;  
    LPVARIANT pvRet = NULL;  
    UINT * pnArgErr = NULL;  
    hr = pPrintInfo->Invoke(dispid,IID_NULL, LOCALE_USER_DEFAULT, wFlags,  
        &dispparams, pvRet, pexcepinfo, pnArgErr);  
    printf("Press Enter to exit");  
    scanf_s("%c",&input);  
    CoUninitialize();  
    return 0;  
}  
```  
  
## <a name="see-also"></a>Zobacz też

- [\<startup> Postaci](../configure-apps/file-schema/startup/startup-element.md)
- [\<supportedRuntime> Postaci](../configure-apps/file-schema/startup/supportedruntime-element.md)
