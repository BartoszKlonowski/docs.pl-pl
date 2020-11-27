---
title: Wiele kontraktów
ms.date: 03/30/2017
ms.assetid: 2bef319b-fe9c-4d49-ac6c-dfb23eb35099
ms.openlocfilehash: 516867a2fd7d6ba0ca1eb6cc3b51c68769b46aba
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96260209"
---
# <a name="multiple-contracts"></a><span data-ttu-id="1a7f4-102">Wiele kontraktów</span><span class="sxs-lookup"><span data-stu-id="1a7f4-102">Multiple Contracts</span></span>

<span data-ttu-id="1a7f4-103">Przykład wielu kontraktów pokazuje, jak zaimplementować więcej niż jeden kontrakt w usłudze i jak skonfigurować punkty końcowe do komunikowania się z każdą z zaimplementowanych kontraktów.</span><span class="sxs-lookup"><span data-stu-id="1a7f4-103">The Multiple Contracts sample demonstrates how to implement more than one contract on a service and how to configure endpoints for communicating with each of the implemented contracts.</span></span> <span data-ttu-id="1a7f4-104">Ten przykład jest oparty na [wprowadzenie](getting-started-sample.md).</span><span class="sxs-lookup"><span data-stu-id="1a7f4-104">This sample is based on the [Getting Started](getting-started-sample.md).</span></span> <span data-ttu-id="1a7f4-105">Usługa została zmodyfikowana w celu zdefiniowania dwóch kontraktów, `ICalculator` kontraktu i `ICalculatorSession` kontraktu.</span><span class="sxs-lookup"><span data-stu-id="1a7f4-105">The service has been modified to define two contracts, the `ICalculator` contract and the `ICalculatorSession` contract.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="1a7f4-106">Procedura instalacji i instrukcje dotyczące kompilacji dla tego przykładu znajdują się na końcu tego tematu.</span><span class="sxs-lookup"><span data-stu-id="1a7f4-106">The setup procedure and build instructions for this sample are located at the end of this topic.</span></span>  
  
 <span data-ttu-id="1a7f4-107">Klasa usługi implementuje zarówno `ICalculator` kontrakt, jak i `ICalculatorSession` .</span><span class="sxs-lookup"><span data-stu-id="1a7f4-107">The service class implements both the `ICalculator` and `ICalculatorSession` contracts.</span></span> <span data-ttu-id="1a7f4-108">Ponieważ jeden z kontraktów wymaga sesji, usługa używa <xref:System.ServiceModel.InstanceContextMode.PerSession> trybu wystąpienia, aby zachować stan w okresie istnienia sesji.</span><span class="sxs-lookup"><span data-stu-id="1a7f4-108">Because one of the contracts requires a session, the service uses the <xref:System.ServiceModel.InstanceContextMode.PerSession> instance mode to maintain the state over the lifetime of the session.</span></span>  
  
 <span data-ttu-id="1a7f4-109">Konfiguracja usługi została zmodyfikowana w celu zdefiniowania dwóch punktów końcowych, aby uwidocznić każdy kontrakt.</span><span class="sxs-lookup"><span data-stu-id="1a7f4-109">The service configuration has been modified to define two endpoints to expose each contract.</span></span> <span data-ttu-id="1a7f4-110">`ICalculator`Punkt końcowy jest uwidoczniony pod adresem podstawowym przy użyciu `basicHttpBinding` .</span><span class="sxs-lookup"><span data-stu-id="1a7f4-110">The `ICalculator` endpoint is exposed at the base address using a `basicHttpBinding`.</span></span> <span data-ttu-id="1a7f4-111">`ICalculatorSession`Punkt końcowy jest uwidaczniany w BaseAddress/sesji przy użyciu `wsHttpBinding` atrybutu z `bindingConfiguration` ustawionym na `BindingWithSession` , jak pokazano w poniższej konfiguracji przykładowej.</span><span class="sxs-lookup"><span data-stu-id="1a7f4-111">The `ICalculatorSession` endpoint is exposed at the baseaddress/session using a `wsHttpBinding` with the `bindingConfiguration` attribute set to `BindingWithSession`, as shown in the following sample configuration.</span></span>  
  
```xml  
<service
    name="Microsoft.ServiceModel.Samples.CalculatorService"  
    behaviorConfiguration="CalculatorServiceBehavior">  
  <!-- ICalculator endpoint is exposed using BasicBinding at the base  
       address provided by host:   
       http://localhost/servicemodelsamples/service.svc  -->  
  <endpoint address=""  
            binding="basicHttpBinding"  
            contract="Microsoft.ServiceModel.Samples.ICalculator" />  
  <!-- ICalculatorSession endpoint is exposed using BindingWithSession  
       at {baseaddress}/session:  
       http://localhost/servicemodelsamples/service.svc/session -->  
  <endpoint address="session"  
            binding="wsHttpBinding"  
            bindingConfiguration="BindingWithSession"
           contract="Microsoft.ServiceModel.Samples.ICalculatorSession" />  
  ...  
</service>  
```  
  
 <span data-ttu-id="1a7f4-112">Wygenerowany kod klienta zawiera teraz klasę klienta zarówno dla oryginalnego `ICalculator` kontraktu, jak i nowego `ICalculatorSession` kontraktu.</span><span class="sxs-lookup"><span data-stu-id="1a7f4-112">The generated client code now includes a client class for both the original `ICalculator` contract and the new `ICalculatorSession` contract.</span></span> <span data-ttu-id="1a7f4-113">Konfiguracja i kod klienta zostały zmodyfikowane w celu komunikowania się z każdą umową w odpowiednim punkcie końcowym usługi.</span><span class="sxs-lookup"><span data-stu-id="1a7f4-113">The client configuration and code have been modified to communicate with each contract at the appropriate service endpoint.</span></span>  
  
 <span data-ttu-id="1a7f4-114">Klient jest aplikacją dla systemu Windows (exe).</span><span class="sxs-lookup"><span data-stu-id="1a7f4-114">The client is a console windows application (.exe).</span></span> <span data-ttu-id="1a7f4-115">Usługa jest hostowana przez Internet Information Services (IIS).</span><span class="sxs-lookup"><span data-stu-id="1a7f4-115">The service is hosted by Internet Information Services (IIS).</span></span>  
  
 <span data-ttu-id="1a7f4-116">W oknie konsoli klienta są wyświetlane operacje wysyłane do poszczególnych punktów końcowych, pierwszy punkt końcowy podstawowego, a następnie bezpieczny punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="1a7f4-116">The client console window displays the operations sent to each of the endpoints, first the basic endpoint, followed by the secure endpoint.</span></span>  
  
### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="1a7f4-117">Aby skonfigurować, skompilować i uruchomić przykład</span><span class="sxs-lookup"><span data-stu-id="1a7f4-117">To set up, build, and run the sample</span></span>  
  
1. <span data-ttu-id="1a7f4-118">Upewnij się, że została wykonana [Procedura konfiguracji jednorazowej dla przykładów Windows Communication Foundation](one-time-setup-procedure-for-the-wcf-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1a7f4-118">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>  
  
2. <span data-ttu-id="1a7f4-119">Aby skompilować wersję rozwiązania w języku C# lub Visual Basic .NET, postępuj zgodnie z instrukcjami w temacie [Tworzenie przykładów Windows Communication Foundation](building-the-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1a7f4-119">To build the C# or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>  
  
3. <span data-ttu-id="1a7f4-120">Aby uruchomić przykład w konfiguracji na jednym lub wielu komputerach, postępuj zgodnie z instrukcjami w temacie [Uruchamianie przykładów Windows Communication Foundation](running-the-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1a7f4-120">To run the sample in a single- or cross-machine configuration, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="1a7f4-121">Przykłady mogą być już zainstalowane na komputerze.</span><span class="sxs-lookup"><span data-stu-id="1a7f4-121">The samples may already be installed on your machine.</span></span> <span data-ttu-id="1a7f4-122">Przed kontynuowaniem Wyszukaj następujący katalog (domyślny).</span><span class="sxs-lookup"><span data-stu-id="1a7f4-122">Check for the following (default) directory before continuing.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> <span data-ttu-id="1a7f4-123">Jeśli ten katalog nie istnieje, przejdź do [przykładów Windows Communication Foundation (WCF) i Windows Workflow Foundation (WF) dla .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) , aby pobrać wszystkie Windows Communication Foundation (WCF) i [!INCLUDE[wf1](../../../../includes/wf1-md.md)] przykłady.</span><span class="sxs-lookup"><span data-stu-id="1a7f4-123">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="1a7f4-124">Ten przykład znajduje się w następującym katalogu.</span><span class="sxs-lookup"><span data-stu-id="1a7f4-124">This sample is located in the following directory.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\MultipleContracts`  
