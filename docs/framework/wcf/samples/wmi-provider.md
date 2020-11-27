---
title: Dostawca WMI
ms.date: 03/30/2017
ms.assetid: 462f0db3-f4a4-4a4b-ac26-41fc25c670a4
ms.openlocfilehash: 9d654527c6897e071f914d4015ba9a225974b0f1
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96263782"
---
# <a name="wmi-provider"></a><span data-ttu-id="53451-102">Dostawca WMI</span><span class="sxs-lookup"><span data-stu-id="53451-102">WMI Provider</span></span>

<span data-ttu-id="53451-103">Ten przykład pokazuje, jak zbierać dane z usług Windows Communication Foundation (WCF) w środowisku uruchomieniowym przy użyciu dostawcy Instrumentacja zarządzania Windows (WMI) wbudowanego w funkcję WCF.</span><span class="sxs-lookup"><span data-stu-id="53451-103">This sample demonstrates how to gather data from Windows Communication Foundation (WCF) services at runtime by using the Windows Management Instrumentation (WMI) provider that is built into WCF.</span></span> <span data-ttu-id="53451-104">Ponadto w tym przykładzie pokazano, jak dodać obiekt usługi WMI zdefiniowany przez użytkownika do usługi.</span><span class="sxs-lookup"><span data-stu-id="53451-104">Also, this sample demonstrates how to add a user-defined WMI object to a service.</span></span> <span data-ttu-id="53451-105">Przykład aktywuje dostawcę WMI dla [wprowadzenie](getting-started-sample.md) i pokazuje, jak zbierać dane z `ICalculator` usługi w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="53451-105">The sample activates the WMI provider for the [Getting Started](getting-started-sample.md) and demonstrates how to gather data from the `ICalculator` service at runtime.</span></span>  
  
 <span data-ttu-id="53451-106">Usługa WMI to implementacja standardu Web-Based Enterprise Management (WBEM).</span><span class="sxs-lookup"><span data-stu-id="53451-106">WMI is Microsoft's implementation of the Web-Based Enterprise Management (WBEM) standard.</span></span> <span data-ttu-id="53451-107">Aby uzyskać więcej informacji na temat zestawu WMI SDK, zobacz [Instrumentacja zarządzania Windows](/windows/desktop/WmiSdk/wmi-start-page).</span><span class="sxs-lookup"><span data-stu-id="53451-107">For more information about the WMI SDK, see [Windows Management Instrumentation](/windows/desktop/WmiSdk/wmi-start-page).</span></span> <span data-ttu-id="53451-108">WBEM to standardowy branża, w której aplikacje uwidaczniają Instrumentację zarządzania w zewnętrznych narzędziach do zarządzania.</span><span class="sxs-lookup"><span data-stu-id="53451-108">WBEM is an industry standard for how applications expose management instrumentation to external management tools.</span></span>  
  
 <span data-ttu-id="53451-109">Funkcja WCF implementuje dostawcę WMI, składnik, który udostępnia instrumentację w czasie wykonywania za pomocą interfejsu zgodnego z pakietem WBEM.</span><span class="sxs-lookup"><span data-stu-id="53451-109">WCF implements a WMI provider, a component that exposes instrumentation at runtime through a WBEM-compatible interface.</span></span> <span data-ttu-id="53451-110">Narzędzia do zarządzania programu mogą łączyć się z usługami za pomocą interfejsu w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="53451-110">Management tools can connect to the services through the interface at runtime.</span></span> <span data-ttu-id="53451-111">Funkcja WCF udostępnia atrybuty usług, takie jak adresy, powiązania, zachowania i odbiorniki.</span><span class="sxs-lookup"><span data-stu-id="53451-111">WCF exposes attributes of services such as addresses, bindings, behaviors, and listeners.</span></span>  
  
 <span data-ttu-id="53451-112">Wbudowany Dostawca usługi WMI jest aktywowany w pliku konfiguracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="53451-112">The built-in WMI provider is activated in the configuration file of the application.</span></span> <span data-ttu-id="53451-113">Jest to realizowane za pomocą `wmiProviderEnabled` atrybutu [\<diagnostics>](../../configure-apps/file-schema/wcf/diagnostics.md) w [\<system.serviceModel>](../../configure-apps/file-schema/wcf/system-servicemodel.md) sekcji, jak pokazano w poniższej konfiguracji przykładowej:</span><span class="sxs-lookup"><span data-stu-id="53451-113">This is done through the `wmiProviderEnabled` attribute of the [\<diagnostics>](../../configure-apps/file-schema/wcf/diagnostics.md) in the [\<system.serviceModel>](../../configure-apps/file-schema/wcf/system-servicemodel.md) section, as shown in the following sample configuration:</span></span>  
  
```xml  
<system.serviceModel>  
    ...  
    <diagnostics wmiProviderEnabled="true" />  
    ...  
</system.serviceModel>  
```  
  
 <span data-ttu-id="53451-114">Ten wpis konfiguracji uwidacznia interfejs WMI.</span><span class="sxs-lookup"><span data-stu-id="53451-114">This configuration entry exposes a WMI interface.</span></span> <span data-ttu-id="53451-115">Aplikacje zarządzania mogą teraz łączyć się za pomocą tego interfejsu i uzyskiwać dostęp do Instrumentacji zarządzania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="53451-115">Management applications can now connect through this interface and access the management instrumentation of the application.</span></span>  
  
## <a name="custom-wmi-object"></a><span data-ttu-id="53451-116">Niestandardowy obiekt WMI</span><span class="sxs-lookup"><span data-stu-id="53451-116">Custom WMI Object</span></span>  

 <span data-ttu-id="53451-117">Dodanie obiektów usługi WMI do usługi umożliwia ujawnienie informacji zdefiniowanych przez użytkownika oraz wbudowanych informacji o dostawcach WMI.</span><span class="sxs-lookup"><span data-stu-id="53451-117">Adding WMI objects to a service makes it possible to reveal user-defined information along with the built-in WMI provider information.</span></span> <span data-ttu-id="53451-118">Jest to realizowane przez opublikowanie schematu usługi w usłudze WMI przy użyciu aplikacji Installutil.exe.</span><span class="sxs-lookup"><span data-stu-id="53451-118">This is accomplished by publishing the schema of the service to WMI by using the Installutil.exe application.</span></span> <span data-ttu-id="53451-119">Instrukcje do osiągnięcia tego, a także więcej szczegółów można znaleźć w instrukcjach instalacji na końcu tematu.</span><span class="sxs-lookup"><span data-stu-id="53451-119">Instructions to accomplish this, along with more details can be found in the setup instructions at the end of the topic.</span></span>  
  
## <a name="accessing-wmi-information"></a><span data-ttu-id="53451-120">Uzyskiwanie dostępu do informacji WMI</span><span class="sxs-lookup"><span data-stu-id="53451-120">Accessing WMI Information</span></span>  

<span data-ttu-id="53451-121">Dostęp do danych usługi WMI można uzyskać na wiele różnych sposobów.</span><span class="sxs-lookup"><span data-stu-id="53451-121">WMI data can be accessed in many different ways.</span></span> <span data-ttu-id="53451-122">Firma Microsoft udostępnia interfejsy API usługi WMI dla skryptów, aplikacji Visual Basic, aplikacji C++ i .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="53451-122">Microsoft provides WMI APIs for scripts, Visual Basic applications, C++ applications, and the .NET Framework.</span></span> <span data-ttu-id="53451-123">Aby uzyskać więcej informacji, zobacz [Korzystanie z usługi WMI](/windows/desktop/wmisdk/using-wmi).</span><span class="sxs-lookup"><span data-stu-id="53451-123">For more information, see [Using WMI](/windows/desktop/wmisdk/using-wmi).</span></span>
  
 <span data-ttu-id="53451-124">W tym przykładzie zastosowano dwa skrypty Java: jeden do wyliczania usług działających na komputerze wraz z niektórymi właściwościami, a drugą, aby wyświetlić dane usługi WMI zdefiniowane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="53451-124">This sample uses two Java scripts: one to enumerate services running on the computer along with some of their properties and the second to view user-defined WMI data.</span></span> <span data-ttu-id="53451-125">Skrypt otwiera połączenie z dostawcą WMI, analizuje dane i wyświetla zebrane dane.</span><span class="sxs-lookup"><span data-stu-id="53451-125">The script opens a connection to the WMI provider, parses data, and displays the data gathered.</span></span>  
  
 <span data-ttu-id="53451-126">Rozpocznij przykład, aby utworzyć uruchomione wystąpienie usługi WCF.</span><span class="sxs-lookup"><span data-stu-id="53451-126">Start the sample to create a running instance of a WCF service.</span></span> <span data-ttu-id="53451-127">Gdy usługa jest uruchomiona, uruchom każdy skrypt Java za pomocą następującego polecenia w wierszu polecenia:</span><span class="sxs-lookup"><span data-stu-id="53451-127">While the service is running, run each Java script by using the following command at the command prompt:</span></span>  
  
```console  
cscript EnumerateServices.js  
```  
  
 <span data-ttu-id="53451-128">Skrypt uzyskuje dostęp do Instrumentacji zawartej w usłudze i tworzy następujące dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="53451-128">The script accesses the instrumentation contained in the service and produces the following output:</span></span>  
  
```console  
Microsoft (R) Windows Script Host Version 5.6  
Copyright © Microsoft Corporation 1996-2001. All rights reserved.  
  
1 service(s) found.  
|-PID:           5776  
|-DistinguishedName:  CalculatorService@http://localhost/ServiceModelSamples/service.svc  
|-Endpoints:     1 endpoints  
  |-CalculatorService.ICalculator@http://localhost/ServiceModelSamples/service.svc  
    |-Address:                        http://localhost/ServiceModelSamples/service.svc  
    |-CounterInstanceName:  
    |-AddressHeaders:                 0  
    |-ContractType:                   Contract.Name='ICalculator'  
    |-BindingElements:                4 bindings  
      |-BindingElements[0]  
        |-Type:                       TransactionFlowBindingElement  
      |-BindingElements[1]  
        |-Type:                       SymmetricSecurityBindingElement  
      |-BindingElements[2]  
        |-Type:                       TextMessageEncodingBindingElement  
        |-MaxReadPoolSize:            64  
        |-MaxWritePoolSize:           16  
      |-BindingElements[3]  
        |-Type:                       HttpTransportBindingElement  
        |-ManualAddressing:           false  
        |-MaxBufferSize:              65536  
        |-AllowCookies:               false  
        |-AuthenticationScheme:       Anonymous  
        |-BypassProxyOnLocal:         false  
        |-HostNameComparisonMode:     StrongWildcard  
        |-ProxyAddress:               null  
        |-ProxyAuthenticationScheme:  Anonymous  
        |-Realm:  
        |-TransferMode:               Buffered  
        |-UseDefaultWebProxy:         true  
|-Behaviors:     5 behaviors  
      |-Behavior[0]  
      |-Type:                       ServiceBehaviorAttribute  
        |-AddressFilterMode:               Exact  
        |-AutomaticSessionShutdown:        true  
        |-ConcurrencyMode:                 Single  
        |-IncludeExceptionDetailInFaults:  false  
        |-InstanceContextMode:             PerSession  
        |-TransactionIsolationLevel:       Unspecified  
        |-TransactionTimeout:              null  
        |-ValidateMustUnderstand:          true  
      |-Behavior[1]  
      |-Type:                       AspNetCompatibilityRequirementsAttribute  
      |-Behavior[2]  
      |-Type:                       ServiceDebugBehavior  
      |-Behavior[3]  
      |-Type:                       ServiceAuthorizationBehavior  
      |-Behavior[4]  
      |-Type:                       Behavior  
```  
  
 <span data-ttu-id="53451-129">Następnie Uruchom drugi skrypt języka Java, aby wyświetlić dane zdefiniowane przez użytkownika usługi WMI:</span><span class="sxs-lookup"><span data-stu-id="53451-129">Next, run the second Java Script to display the user-defined WMI data:</span></span>  
  
```console  
cscript EnumerateCustomObjects.js  
```  
  
 <span data-ttu-id="53451-130">Skrypt uzyskuje dostęp do zdefiniowanej przez użytkownika Instrumentacji zawartej w usługach i tworzy następujące dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="53451-130">The script accesses the user-defined instrumentation contained in the services and produces the following output:</span></span>  
  
```console
1 WMIObject(s) found.  
|-PID:           30285bfd-9d66-4c4e-9be2-310499c5cef5  
|-InstanceId:    3839  
|-WMIInfo:       User Defined WMI Information.  
```  
  
 <span data-ttu-id="53451-131">Dane wyjściowe pokazują, że na komputerze jest uruchomiona jedna usługa.</span><span class="sxs-lookup"><span data-stu-id="53451-131">The output shows that there is a single service running on the computer.</span></span> <span data-ttu-id="53451-132">Usługa ujawnia jeden punkt końcowy, który implementuje `ICalculator` kontrakt.</span><span class="sxs-lookup"><span data-stu-id="53451-132">The service exposes one endpoint that implements the `ICalculator` contract.</span></span> <span data-ttu-id="53451-133">Ustawienia zachowania i powiązania, które są implementowane przez punkt końcowy, są wyświetlane jako suma poszczególnych elementów stosu komunikatów.</span><span class="sxs-lookup"><span data-stu-id="53451-133">The settings of the behavior and binding that are implemented by the endpoint are listed as the sum of individual elements of the messaging stack.</span></span>  
  
 <span data-ttu-id="53451-134">Usługa WMI nie jest ograniczona do uwidaczniania Instrumentacji zarządzania infrastruktury WCF.</span><span class="sxs-lookup"><span data-stu-id="53451-134">WMI is not limited to exposing the management instrumentation of the WCF infrastructure.</span></span> <span data-ttu-id="53451-135">Aplikacja może uwidaczniać własne specyficzne dla domeny elementy danych za pomocą tego samego mechanizmu.</span><span class="sxs-lookup"><span data-stu-id="53451-135">The application can expose its own domain-specific data items through the same mechanism.</span></span> <span data-ttu-id="53451-136">Usługa WMI to ujednolicony mechanizm kontroli i kontroli nad usługą sieci Web.</span><span class="sxs-lookup"><span data-stu-id="53451-136">WMI is a unified mechanism for inspection and control of a Web service.</span></span>  
  
#### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="53451-137">Aby skonfigurować, skompilować i uruchomić przykład</span><span class="sxs-lookup"><span data-stu-id="53451-137">To set up, build, and run the sample</span></span>  
  
1. <span data-ttu-id="53451-138">Upewnij się, że została wykonana [Procedura konfiguracji jednorazowej dla przykładów Windows Communication Foundation](one-time-setup-procedure-for-the-wcf-samples.md).</span><span class="sxs-lookup"><span data-stu-id="53451-138">Ensure you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>  
  
2. <span data-ttu-id="53451-139">Aby skompilować wersję rozwiązania w języku C# lub Visual Basic .NET, postępuj zgodnie z instrukcjami w temacie [Tworzenie przykładów Windows Communication Foundation](building-the-samples.md).</span><span class="sxs-lookup"><span data-stu-id="53451-139">To build the C# or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>  
  
3. <span data-ttu-id="53451-140">Opublikuj schemat usług w usłudze WMI, uruchamiając InstallUtil.exe (domyślne lokalizacje InstallUtil.exe to "%WINDIR%\Microsoft.NET\Framework\v4.0.30319") w pliku service.dll w katalogu hostingu.</span><span class="sxs-lookup"><span data-stu-id="53451-140">Publish the services schema to WMI by running the InstallUtil.exe (the default locations for InstallUtil.exe is "%WINDIR%\Microsoft.NET\Framework\v4.0.30319") on the service.dll file in the hosting directory.</span></span> <span data-ttu-id="53451-141">Ten krok należy wykonać tylko wtedy, gdy wprowadzono zmiany w pliku service.dll.</span><span class="sxs-lookup"><span data-stu-id="53451-141">This step only needs to be executed when changes have been made to the service.dll file.</span></span>
  
4. <span data-ttu-id="53451-142">Aby uruchomić przykład w konfiguracji na jednym lub wielu komputerach, postępuj zgodnie z instrukcjami w temacie [Uruchamianie przykładów Windows Communication Foundation](running-the-samples.md).</span><span class="sxs-lookup"><span data-stu-id="53451-142">To run the sample in a single- or cross-computer configuration, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span>  
  
    > [!NOTE]
    > <span data-ttu-id="53451-143">W przypadku zainstalowania programu WCF po zainstalowaniu ASP.NET może być konieczne uruchomienie "% WINDIR% \ Foundation\servicemodelreg.exe komunikacji Microsoft. Net\Framework\v3.0\Windows "-r-x, aby nadać kontu ASPNET uprawnienie do publikowania obiektów usługi WMI.</span><span class="sxs-lookup"><span data-stu-id="53451-143">If you installed WCF after installing ASP.NET, you may need to run "%WINDIR%\ Microsoft.Net\Framework\v3.0\Windows Communication Foundation\servicemodelreg.exe " -r -x to give the ASPNET account permission to publish WMI objects.</span></span>  
  
5. <span data-ttu-id="53451-144">Wyświetl dane z przykładu, korzystając z poleceń: `cscript EnumerateServices.js` lub `cscript EnumerateCustomObjects.js` .</span><span class="sxs-lookup"><span data-stu-id="53451-144">View data from the sample surfaced through WMI by using the commands: `cscript EnumerateServices.js` or `cscript EnumerateCustomObjects.js`.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="53451-145">Przykłady mogą być już zainstalowane na komputerze.</span><span class="sxs-lookup"><span data-stu-id="53451-145">The samples may already be installed on your computer.</span></span> <span data-ttu-id="53451-146">Przed kontynuowaniem Wyszukaj następujący katalog (domyślny).</span><span class="sxs-lookup"><span data-stu-id="53451-146">Check for the following (default) directory before continuing.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> <span data-ttu-id="53451-147">Jeśli ten katalog nie istnieje, przejdź do [przykładów Windows Communication Foundation (WCF) i Windows Workflow Foundation (WF) dla .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) , aby pobrać wszystkie Windows Communication Foundation (WCF) i [!INCLUDE[wf1](../../../../includes/wf1-md.md)] przykłady.</span><span class="sxs-lookup"><span data-stu-id="53451-147">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="53451-148">Ten przykład znajduje się w następującym katalogu.</span><span class="sxs-lookup"><span data-stu-id="53451-148">This sample is located in the following directory.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Management\WMIProvider`  
  
## <a name="see-also"></a><span data-ttu-id="53451-149">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="53451-149">See also</span></span>

- <span data-ttu-id="53451-150">[Przykłady monitorowania oprogramowania AppFabric](/previous-versions/appfabric/ff383407(v=azure.10))</span><span class="sxs-lookup"><span data-stu-id="53451-150">[AppFabric Monitoring Samples](/previous-versions/appfabric/ff383407(v=azure.10))</span></span>
