---
title: NetNamedPipeBinding
ms.date: 03/30/2017
helpviewer_keywords:
- Net Profile Named Pipe
ms.assetid: e78e845f-c325-46e2-927d-81616f97f7d5
ms.openlocfilehash: 46365c8dbfee66d719b114947f6b04069e0f8870
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96235302"
---
# <a name="netnamedpipebinding"></a><span data-ttu-id="fd7bb-102">NetNamedPipeBinding</span><span class="sxs-lookup"><span data-stu-id="fd7bb-102">NetNamedPipeBinding</span></span>

<span data-ttu-id="fd7bb-103">Ten przykład pokazuje `netNamedPipeBinding` powiązanie, które zapewnia komunikację między procesami na tym samym komputerze.</span><span class="sxs-lookup"><span data-stu-id="fd7bb-103">This sample demonstrates the `netNamedPipeBinding` binding, which provides cross-process communication on the same machine.</span></span> <span data-ttu-id="fd7bb-104">Nazwane potoki nie działają między maszynami.</span><span class="sxs-lookup"><span data-stu-id="fd7bb-104">Named pipes do not work across machines.</span></span> <span data-ttu-id="fd7bb-105">Ten przykład jest oparty na usłudze kalkulatora [wprowadzenie](getting-started-sample.md) .</span><span class="sxs-lookup"><span data-stu-id="fd7bb-105">This sample is based on The [Getting Started](getting-started-sample.md) calculator service.</span></span>  
  
 <span data-ttu-id="fd7bb-106">W tym przykładzie usługa jest samodzielna.</span><span class="sxs-lookup"><span data-stu-id="fd7bb-106">In this sample, the service is self-hosted.</span></span> <span data-ttu-id="fd7bb-107">Klientem i usługą są aplikacje konsolowe.</span><span class="sxs-lookup"><span data-stu-id="fd7bb-107">Both the client and the service are console applications.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="fd7bb-108">Procedura instalacji i instrukcje dotyczące kompilacji dla tego przykładu znajdują się na końcu tego tematu.</span><span class="sxs-lookup"><span data-stu-id="fd7bb-108">The setup procedure and build instructions for this sample are located at the end of this topic.</span></span>  
  
 <span data-ttu-id="fd7bb-109">Powiązanie jest określone w plikach konfiguracji klienta i usługi.</span><span class="sxs-lookup"><span data-stu-id="fd7bb-109">The binding is specified in the configuration files for the client and service.</span></span> <span data-ttu-id="fd7bb-110">Typ powiązania jest określony w `binding` atrybucie [\<endpoint>](../../configure-apps/file-schema/wcf/endpoint-element.md) [ \<endpoint> \<client> ](../../configure-apps/file-schema/wcf/endpoint-of-client.md) lub elementu, jak pokazano w poniższej konfiguracji przykładowej:</span><span class="sxs-lookup"><span data-stu-id="fd7bb-110">The binding type is specified in the `binding` attribute of the [\<endpoint>](../../configure-apps/file-schema/wcf/endpoint-element.md) or [\<endpoint> of \<client>](../../configure-apps/file-schema/wcf/endpoint-of-client.md) element, as shown in the following sample configuration:</span></span>  
  
```xml  
<endpoint address="net.pipe://localhost/ServiceModelSamples/service"  
          binding="netNamedPipeBinding"  
          contract="Microsoft.ServiceModel.Samples.ICalculator" />  
```  
  
 <span data-ttu-id="fd7bb-111">Poprzedni przykład pokazuje, jak skonfigurować punkt końcowy do używania `netNamedPipeBinding` powiązania z ustawieniami domyślnymi.</span><span class="sxs-lookup"><span data-stu-id="fd7bb-111">The previous sample shows how to configure an endpoint to use the `netNamedPipeBinding` binding with the default settings.</span></span> <span data-ttu-id="fd7bb-112">Jeśli chcesz skonfigurować `netNamedPipeBinding` powiązanie i zmienić niektóre z jego ustawień, musisz zdefiniować konfigurację powiązania.</span><span class="sxs-lookup"><span data-stu-id="fd7bb-112">If you want to configure the `netNamedPipeBinding` binding and change some of its settings, you must define a binding configuration.</span></span> <span data-ttu-id="fd7bb-113">Punkt końcowy musi odwoływać się do konfiguracji powiązania za pomocą nazwy z `bindingConfiguration` atrybutem.</span><span class="sxs-lookup"><span data-stu-id="fd7bb-113">The endpoint must reference the binding configuration by name with a `bindingConfiguration` attribute.</span></span>  
  
```xml  
<endpoint address="net.pipe://localhost/ServiceModelSamples/service"  
          binding="netNamedPipeBinding"  
          bindingConfiguration="Binding1"
          contract="Microsoft.ServiceModel.Samples.ICalculator" />  
```  
  
 <span data-ttu-id="fd7bb-114">W tym przykładzie Konfiguracja powiązania ma nazwę `Binding1` i ma następującą definicję:</span><span class="sxs-lookup"><span data-stu-id="fd7bb-114">In this sample, the binding configuration is named `Binding1` and has the following definition:</span></span>  
  
```xml  
<bindings>  
  <!--   
        Following is the expanded configuration section for a NetNamedPipeBinding.  
        Each property is configured with the default value.  
     -->  
  <netNamedPipeBinding>  
    <binding name="Binding1"
             closeTimeout="00:01:00"  
             openTimeout="00:01:00"
             receiveTimeout="00:10:00"
             sendTimeout="00:01:00"  
             transactionFlow="false"
             transferMode="Buffered"
             transactionProtocol="OleTransactions"  
             hostNameComparisonMode="StrongWildcard"
             maxBufferPoolSize="524288"  
             maxBufferSize="65536"
             maxConnections="10"
             maxReceivedMessageSize="65536">  
      <security mode="Transport">  
        <transport protectionLevel="EncryptAndSign" />  
      </security>  
    </binding>  
  </netNamedPipeBinding>  
</bindings>  
```  
  
 <span data-ttu-id="fd7bb-115">Po uruchomieniu przykładu żądania operacji i odpowiedzi są wyświetlane w oknie konsoli klienta.</span><span class="sxs-lookup"><span data-stu-id="fd7bb-115">When you run the sample, the operation requests and responses are displayed in the client console window.</span></span> <span data-ttu-id="fd7bb-116">Naciśnij klawisz ENTER w oknie klienta, aby zamknąć klienta programu.</span><span class="sxs-lookup"><span data-stu-id="fd7bb-116">Press ENTER in the client window to shut down the client.</span></span>  
  
```console  
Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
  
Press <ENTER> to terminate client.  
```  
  
### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="fd7bb-117">Aby skonfigurować, skompilować i uruchomić przykład</span><span class="sxs-lookup"><span data-stu-id="fd7bb-117">To set up, build, and run the sample</span></span>  
  
1. <span data-ttu-id="fd7bb-118">Upewnij się, że została wykonana [Procedura konfiguracji jednorazowej dla przykładów Windows Communication Foundation](one-time-setup-procedure-for-the-wcf-samples.md).</span><span class="sxs-lookup"><span data-stu-id="fd7bb-118">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>  
  
2. <span data-ttu-id="fd7bb-119">Aby skompilować wersję rozwiązania w języku C# lub Visual Basic .NET, postępuj zgodnie z instrukcjami w temacie [Tworzenie przykładów Windows Communication Foundation](building-the-samples.md).</span><span class="sxs-lookup"><span data-stu-id="fd7bb-119">To build the C# or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>  
  
3. <span data-ttu-id="fd7bb-120">Aby uruchomić przykład w konfiguracji pojedynczej maszyny, postępuj zgodnie z instrukcjami w temacie [Uruchamianie przykładów Windows Communication Foundation](running-the-samples.md).</span><span class="sxs-lookup"><span data-stu-id="fd7bb-120">To run the sample in a single machine configuration, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="fd7bb-121">Przykłady mogą być już zainstalowane na komputerze.</span><span class="sxs-lookup"><span data-stu-id="fd7bb-121">The samples may already be installed on your machine.</span></span> <span data-ttu-id="fd7bb-122">Przed kontynuowaniem Wyszukaj następujący katalog (domyślny).</span><span class="sxs-lookup"><span data-stu-id="fd7bb-122">Check for the following (default) directory before continuing.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> <span data-ttu-id="fd7bb-123">Jeśli ten katalog nie istnieje, przejdź do [przykładów Windows Communication Foundation (WCF) i Windows Workflow Foundation (WF) dla .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) , aby pobrać wszystkie Windows Communication Foundation (WCF) i [!INCLUDE[wf1](../../../../includes/wf1-md.md)] przykłady.</span><span class="sxs-lookup"><span data-stu-id="fd7bb-123">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="fd7bb-124">Ten przykład znajduje się w następującym katalogu.</span><span class="sxs-lookup"><span data-stu-id="fd7bb-124">This sample is located in the following directory.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Binding\Net\NamedPipe`  
