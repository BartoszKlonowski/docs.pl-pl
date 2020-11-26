---
title: Niestandardowe powiązanie niezawodnej sesji przez protokół HTTPS
ms.date: 03/30/2017
ms.assetid: 16aaa80d-3ffe-47c4-8b16-ec65c4d25f8d
ms.openlocfilehash: aec9bc11fab71a8e3adfe60e0c19b0ac4a9e3699
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96241892"
---
# <a name="custom-binding-reliable-session-over-https"></a><span data-ttu-id="203b6-102">Niestandardowe powiązanie niezawodnej sesji przez protokół HTTPS</span><span class="sxs-lookup"><span data-stu-id="203b6-102">Custom Binding Reliable Session over HTTPS</span></span>

<span data-ttu-id="203b6-103">W tym przykładzie przedstawiono sposób korzystania z zabezpieczeń transportu SSL z niezawodnymi sesjami.</span><span class="sxs-lookup"><span data-stu-id="203b6-103">This sample demonstrates the use of SSL transport security with Reliable Sessions.</span></span> <span data-ttu-id="203b6-104">Niezawodne sesje programu implementują protokół obsługi komunikatów WS-Reliable.</span><span class="sxs-lookup"><span data-stu-id="203b6-104">Reliable Sessions implements the WS-Reliable Messaging protocol.</span></span> <span data-ttu-id="203b6-105">Można korzystać z bezpiecznej niezawodnej sesji, tworząc WS-Security za pośrednictwem niezawodnych sesji.</span><span class="sxs-lookup"><span data-stu-id="203b6-105">You can have a secure reliable session by composing WS-Security over Reliable Sessions.</span></span> <span data-ttu-id="203b6-106">Czasami jednak zamiast tego można użyć zabezpieczeń transportu HTTP z protokołem SSL.</span><span class="sxs-lookup"><span data-stu-id="203b6-106">But sometimes, you may choose to instead use HTTP transport security with SSL.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="203b6-107">Przykłady mogą być już zainstalowane na komputerze.</span><span class="sxs-lookup"><span data-stu-id="203b6-107">The samples may already be installed on your machine.</span></span> <span data-ttu-id="203b6-108">Przed kontynuowaniem Wyszukaj następujący katalog (domyślny).</span><span class="sxs-lookup"><span data-stu-id="203b6-108">Check for the following (default) directory before continuing.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> <span data-ttu-id="203b6-109">Jeśli ten katalog nie istnieje, przejdź do [przykładów Windows Communication Foundation (WCF) i Windows Workflow Foundation (WF) dla .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) , aby pobrać wszystkie Windows Communication Foundation (WCF) i [!INCLUDE[wf1](../../../../includes/wf1-md.md)] przykłady.</span><span class="sxs-lookup"><span data-stu-id="203b6-109">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="203b6-110">Ten przykład znajduje się w następującym katalogu.</span><span class="sxs-lookup"><span data-stu-id="203b6-110">This sample is located in the following directory.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Binding\Custom\ReliableSessionOverHttps`  
  
## <a name="sample-details"></a><span data-ttu-id="203b6-111">Przykładowe szczegóły</span><span class="sxs-lookup"><span data-stu-id="203b6-111">Sample Details</span></span>  

 <span data-ttu-id="203b6-112">Protokół SSL gwarantuje, że pakiety są zabezpieczone.</span><span class="sxs-lookup"><span data-stu-id="203b6-112">SSL ensures that the packets themselves are secured.</span></span> <span data-ttu-id="203b6-113">Należy pamiętać, że różni się to od zabezpieczania niezawodnej sesji przy użyciu WS-Secure konwersacji.</span><span class="sxs-lookup"><span data-stu-id="203b6-113">It is important to note that this is different from securing the reliable session using WS-Secure Conversation.</span></span>  
  
 <span data-ttu-id="203b6-114">Aby korzystać z niezawodnej sesji za pośrednictwem protokołu HTTPS, należy utworzyć niestandardowe powiązanie.</span><span class="sxs-lookup"><span data-stu-id="203b6-114">To use reliable session over HTTPS, you must create a custom binding.</span></span> <span data-ttu-id="203b6-115">Ten przykład jest oparty na [wprowadzenie](getting-started-sample.md) , który implementuje usługę kalkulatora.</span><span class="sxs-lookup"><span data-stu-id="203b6-115">This sample is based on the [Getting Started](getting-started-sample.md) that implements a calculator service.</span></span> <span data-ttu-id="203b6-116">Niestandardowe powiązanie jest tworzone przy użyciu elementu powiązania niezawodnej sesji i [\<httpsTransport>](../../configure-apps/file-schema/wcf/httpstransport.md) .</span><span class="sxs-lookup"><span data-stu-id="203b6-116">A custom binding is created using the reliable session binding element and the [\<httpsTransport>](../../configure-apps/file-schema/wcf/httpstransport.md).</span></span> <span data-ttu-id="203b6-117">Następująca konfiguracja jest powiązaniem niestandardowym.</span><span class="sxs-lookup"><span data-stu-id="203b6-117">The following configuration is of the custom binding.</span></span>  
  
```xml  
<?xml version="1.0" encoding="utf-8" ?>  
<configuration>  
  <system.serviceModel>  
    <services>  
      <service
          name="Microsoft.ServiceModel.Samples.CalculatorService"  
          behaviorConfiguration="CalculatorServiceBehavior">  
        <!-- use base address provided by host -->  
        <endpoint address=""  
                  binding="customBinding"  
                  bindingConfiguration="reliableSessionOverHttps"
                  contract="Microsoft.ServiceModel.Samples.ICalculator" />  
        <!-- the mex endpoint is exposed as http://localhost/servicemodelsamples/service.svc/mex-->  
        <endpoint address="mex"  
                  binding="mexHttpBinding"  
                  contract="IMetadataExchange"/>  
      </service>  
    </services>  
  
    <bindings>  
      <customBinding>  
        <binding name="reliableSessionOverHttps">  
          <reliableSession />  
          <httpsTransport />  
        </binding>  
      </customBinding>  
    </bindings>  
  
    <!--For debugging purposes set the includeExceptionDetailInFaults attribute to true-->  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="CalculatorServiceBehavior">  
          <serviceMetadata httpGetEnabled="true" />  
          <serviceDebug includeExceptionDetailInFaults="False" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  
  </system.serviceModel>  
  
</configuration>  
```  
  
 <span data-ttu-id="203b6-118">Kod programu w przykładzie jest taki sam jak w przypadku usługi [wprowadzenie](getting-started-sample.md) .</span><span class="sxs-lookup"><span data-stu-id="203b6-118">The program code in the sample is identical to that of the [Getting Started](getting-started-sample.md) service.</span></span> <span data-ttu-id="203b6-119">Przed skompilowaniem i uruchomieniem przykładu należy utworzyć certyfikat i przypisać go przy użyciu kreatora certyfikatu serwera sieci Web.</span><span class="sxs-lookup"><span data-stu-id="203b6-119">You must create a certificate and assign it by using the Web Server Certificate Wizard before building and running the sample.</span></span> <span data-ttu-id="203b6-120">Definicja punktu końcowego i definicja powiązania w ustawieniach pliku konfiguracji umożliwiają korzystanie z niestandardowego powiązania, jak pokazano w poniższej konfiguracji przykładowej dla klienta.</span><span class="sxs-lookup"><span data-stu-id="203b6-120">The endpoint definition and binding definition in the configuration file settings enable the use of custom binding as shown in the following sample configuration for the client.</span></span>  
  
```xml  
<?xml version="1.0" encoding="utf-8" ?>  
<configuration>  
  <system.serviceModel>  
  
    <client>  
      <!-- this endpoint has an https: address -->  
      <endpoint name=""  
                address="https://localhost/servicemodelsamples/service.svc"
                binding="customBinding"
                bindingConfiguration="reliableSessionOverHttps"
                contract="Microsoft.ServiceModel.Samples.ICalculator" />  
    </client>  
  
      <bindings>  
        <customBinding>  
          <binding name="reliableSessionOverHttps">  
            <reliableSession />  
            <httpsTransport />  
          </binding>  
        </customBinding>
    </bindings>  
  
  </system.serviceModel>  
  
</configuration>  
```  
  
 <span data-ttu-id="203b6-121">Określony adres używa `https://` schematu.</span><span class="sxs-lookup"><span data-stu-id="203b6-121">The address specified uses the `https://` scheme.</span></span>  
  
 <span data-ttu-id="203b6-122">Ponieważ certyfikat używany w tym przykładzie jest certyfikatem testowym utworzonym przy użyciu Makecert.exe, po próbie uzyskania dostępu do adresu https:, takiego jak, z przeglądarki jest wyświetlany alert zabezpieczeń `https://localhost/servicemodelsamples/service.svc` .</span><span class="sxs-lookup"><span data-stu-id="203b6-122">Because the certificate used in this sample is a test certificate created with Makecert.exe, a security alert appears when you try to access an https: address, such as `https://localhost/servicemodelsamples/service.svc`, from your browser.</span></span> <span data-ttu-id="203b6-123">Aby umożliwić klientowi Windows Communication Foundation (WCF) współpracujący z certyfikatem testowym, do klienta został dodany dodatkowy kod, aby pominąć alert zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="203b6-123">To allow the Windows Communication Foundation (WCF) client to work with a test certificate in place, some additional code has been added to the client to suppress the security alert.</span></span> <span data-ttu-id="203b6-124">Ten kod i Klasa towarzysząca nie są wymagane w przypadku korzystania z certyfikatów produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="203b6-124">This code, and the accompanying class, is not required when using production certificates.</span></span>  

```csharp
// This code is required only for test certificates like those created by Makecert.exe.  
PermissiveCertificatePolicy.Enact("CN=ServiceModelSamples-HTTPS-Server");  
```

 <span data-ttu-id="203b6-125">Po uruchomieniu przykładu żądania operacji i odpowiedzi są wyświetlane w oknie konsoli klienta.</span><span class="sxs-lookup"><span data-stu-id="203b6-125">When you run the sample, the operation requests and responses are displayed in the client console window.</span></span> <span data-ttu-id="203b6-126">Naciśnij klawisz ENTER w oknie klienta, aby zamknąć klienta programu.</span><span class="sxs-lookup"><span data-stu-id="203b6-126">Press ENTER in the client window to shut down the client.</span></span>  
  
```console  
Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
  
Press <ENTER> to terminate client.  
```  
  
#### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="203b6-127">Aby skonfigurować, skompilować i uruchomić przykład</span><span class="sxs-lookup"><span data-stu-id="203b6-127">To set up, build, and run the sample</span></span>  
  
1. <span data-ttu-id="203b6-128">Zainstaluj ASP.NET 4,0 przy użyciu następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="203b6-128">Install  ASP.NET 4.0 using the following command.</span></span>  
  
    ```console  
    %windir%\Microsoft.NET\Framework\v4.0.XXXXX\aspnet_regiis.exe /i /enable  
    ```  
  
2. <span data-ttu-id="203b6-129">Upewnij się, że została wykonana [Procedura konfiguracji jednorazowej dla przykładów Windows Communication Foundation](one-time-setup-procedure-for-the-wcf-samples.md).</span><span class="sxs-lookup"><span data-stu-id="203b6-129">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>  
  
3. <span data-ttu-id="203b6-130">Upewnij się, że wykonano [instrukcje instalacji certyfikatu serwera Internet Information Services (IIS)](iis-server-certificate-installation-instructions.md).</span><span class="sxs-lookup"><span data-stu-id="203b6-130">Ensure that you have performed the [Internet Information Services (IIS) Server Certificate Installation Instructions](iis-server-certificate-installation-instructions.md).</span></span>  
  
4. <span data-ttu-id="203b6-131">Aby skompilować wersję rozwiązania w języku C# lub Visual Basic .NET, postępuj zgodnie z instrukcjami w temacie [Tworzenie przykładów Windows Communication Foundation](building-the-samples.md).</span><span class="sxs-lookup"><span data-stu-id="203b6-131">To build the C# or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>  
  
5. <span data-ttu-id="203b6-132">Aby uruchomić przykład w konfiguracji na jednym lub wielu komputerach, postępuj zgodnie z instrukcjami w temacie [Uruchamianie przykładów Windows Communication Foundation](running-the-samples.md).</span><span class="sxs-lookup"><span data-stu-id="203b6-132">To run the sample in a single- or cross-machine configuration, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span>  
