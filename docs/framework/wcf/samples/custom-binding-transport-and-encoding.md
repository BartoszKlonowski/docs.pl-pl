---
title: Transport i kodowanie powiązań niestandardowych
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 6c0b353d-79ee-4e61-b348-be49ad0e9a16
ms.openlocfilehash: 00af245f49994314ca29e1f5a2debe3af2364999
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96241870"
---
# <a name="custom-binding-transport-and-encoding"></a><span data-ttu-id="18a6f-102">Transport i kodowanie powiązań niestandardowych</span><span class="sxs-lookup"><span data-stu-id="18a6f-102">Custom Binding Transport and Encoding</span></span>

<span data-ttu-id="18a6f-103">Niestandardowe powiązanie jest definiowane przez uporządkowaną listę elementów powiązania dyskretnego.</span><span class="sxs-lookup"><span data-stu-id="18a6f-103">A custom binding is defined by an ordered list of discrete binding elements.</span></span> <span data-ttu-id="18a6f-104">W tym przykładzie pokazano, jak skonfigurować powiązanie niestandardowe z różnymi elementami transportu i przenoszenia komunikatów.</span><span class="sxs-lookup"><span data-stu-id="18a6f-104">This sample demonstrates how to configure a custom binding with various transport and message encoding elements.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="18a6f-105">Procedura instalacji i instrukcje dotyczące kompilacji dla tego przykładu znajdują się na końcu tego tematu.</span><span class="sxs-lookup"><span data-stu-id="18a6f-105">The setup procedure and build instructions for this sample are located at the end of this topic.</span></span>  
  
 <span data-ttu-id="18a6f-106">Ten przykład jest oparty na [samym hoście](self-host.md)i został zmodyfikowany w celu skonfigurowania trzech punktów końcowych do obsługi transportów http, TCP i nazwany potok z powiązaniami niestandardowymi.</span><span class="sxs-lookup"><span data-stu-id="18a6f-106">This sample is based on the [Self-Host](self-host.md), and has been modified to configure three endpoints to support HTTP, TCP, and NamedPipe transports with custom bindings.</span></span> <span data-ttu-id="18a6f-107">Konfiguracja klienta została zmodyfikowana w podobny sposób, a kod klienta został zmieniony, aby komunikować się z każdym z trzech punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="18a6f-107">The client configuration was similarly modified, and the client code changed to communicate with each of the three endpoints.</span></span>  
  
 <span data-ttu-id="18a6f-108">W przykładzie przedstawiono sposób konfigurowania niestandardowego powiązania, które obsługuje określony transport i kodowanie komunikatów.</span><span class="sxs-lookup"><span data-stu-id="18a6f-108">The sample demonstrates a how to configure a custom binding that supports a particular transport and message encoding.</span></span> <span data-ttu-id="18a6f-109">W tym celu należy skonfigurować Transport i kodowanie komunikatów dla `binding` elementu.</span><span class="sxs-lookup"><span data-stu-id="18a6f-109">This is accomplished by configuring a transport and a message encoding for the `binding` element.</span></span> <span data-ttu-id="18a6f-110">Kolejność elementów powiązania jest istotna dla definiowania niestandardowego powiązania, ponieważ każdy reprezentuje warstwę w stosie kanału (zobacz [powiązania niestandardowe](../extending/custom-bindings.md)).</span><span class="sxs-lookup"><span data-stu-id="18a6f-110">The ordering of binding elements is important in defining a custom binding, because each represents a layer in the channel stack (see [Custom Bindings](../extending/custom-bindings.md)).</span></span> <span data-ttu-id="18a6f-111">Ten przykład konfiguruje trzy powiązania niestandardowe: transport HTTP z kodowaniem tekstu, transport TCP z kodowaniem tekstu oraz transport nazwany potok z kodowaniem binarnym.</span><span class="sxs-lookup"><span data-stu-id="18a6f-111">This sample configures three custom bindings: an HTTP transport with text encoding, a TCP transport with text encoding, and a NamedPipe transport with a binary encoding.</span></span>  
  
 <span data-ttu-id="18a6f-112">Konfiguracja usługi definiuje niestandardowe powiązania w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="18a6f-112">The service configuration defines the custom bindings as follows:</span></span>  
  
```xml  
<bindings>  
    <customBinding>  
        <binding name="HttpBinding" >  
            <textMessageEncoding
                messageVersion="Soap12Addressing10"/>  
            <httpTransport />  
        </binding>  
        <binding name="TcpBinding" >  
            <textMessageEncoding />  
            <tcpTransport />  
        </binding>  
        <binding name="NamedPipeBinding" >  
            <binaryMessageEncoding />  
            <namedPipeTransport />  
        </binding>  
    </customBinding>  
</bindings>  
```  
  
 <span data-ttu-id="18a6f-113">Po uruchomieniu przykładu żądania operacji i odpowiedzi są wyświetlane zarówno w oknie usługi, jak i w konsoli klienta.</span><span class="sxs-lookup"><span data-stu-id="18a6f-113">When you run the sample, the operation requests and responses are displayed in both the service and client console window.</span></span> <span data-ttu-id="18a6f-114">Klient komunikuje się z każdym z trzech punktów końcowych, uzyskując dostęp do pierwszego protokołu HTTP, a następnie TCP i finally nazwany potok.</span><span class="sxs-lookup"><span data-stu-id="18a6f-114">The client communicates with each of the three endpoints, accessing first HTTP, then TCP, and finally NamedPipe.</span></span> <span data-ttu-id="18a6f-115">Naciśnij klawisz ENTER w każdym oknie konsoli, aby zamknąć usługę i klienta.</span><span class="sxs-lookup"><span data-stu-id="18a6f-115">Press ENTER in each console window to shut down the service and client.</span></span>  
  
 <span data-ttu-id="18a6f-116">`namedPipeTransport`Powiązanie nie obsługuje operacji na komputerze.</span><span class="sxs-lookup"><span data-stu-id="18a6f-116">The `namedPipeTransport` binding does not support machine-to-machine operations.</span></span> <span data-ttu-id="18a6f-117">Jest on używany tylko do komunikacji na tym samym komputerze.</span><span class="sxs-lookup"><span data-stu-id="18a6f-117">It is used only for communication on the same machine.</span></span> <span data-ttu-id="18a6f-118">W związku z tym podczas uruchamiania przykładu w scenariuszu między maszynami należy dodać komentarz do następujących wierszy w pliku kodu klienta:</span><span class="sxs-lookup"><span data-stu-id="18a6f-118">Therefore, when running the sample in a cross-machine scenario, comment out the following lines in the client code file:</span></span>  
  
```csharp  
CalculatorClient client = new CalculatorClient("default");  
Console.WriteLine("Communicate with named pipe endpoint.");  
// Call operations.  
DoCalculations(client);  
//Closing the client gracefully closes the connection and cleans up resources  
client.Close();  
```  
  
```vb  
Dim client As New CalculatorClient("default")  
Console.WriteLine("Communicate with named pipe endpoint.")  
' call operations  
DoCalculations(client)  
'Closing the client gracefully closes the connection and cleans up resources  
client.Close()  
```  
  
> [!NOTE]
> <span data-ttu-id="18a6f-119">W przypadku użycia Svcutil.exe do ponownego wygenerowania konfiguracji dla tego przykładu należy zmodyfikować nazwę punktu końcowego w konfiguracji klienta, aby odpowiadała kodowi klienta.</span><span class="sxs-lookup"><span data-stu-id="18a6f-119">If you use Svcutil.exe to regenerate the configuration for this sample, be sure to modify the endpoint name in the client configuration to match the client code.</span></span>  
  
### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="18a6f-120">Aby skonfigurować, skompilować i uruchomić przykład</span><span class="sxs-lookup"><span data-stu-id="18a6f-120">To set up, build, and run the sample</span></span>  
  
1. <span data-ttu-id="18a6f-121">Upewnij się, że została wykonana [Procedura konfiguracji jednorazowej dla przykładów Windows Communication Foundation](one-time-setup-procedure-for-the-wcf-samples.md).</span><span class="sxs-lookup"><span data-stu-id="18a6f-121">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>  
  
2. <span data-ttu-id="18a6f-122">Aby skompilować wersję rozwiązania dla języka C#, C++ lub Visual Basic .NET, postępuj zgodnie z instrukcjami w temacie [Tworzenie przykładów Windows Communication Foundation](building-the-samples.md).</span><span class="sxs-lookup"><span data-stu-id="18a6f-122">To build the C#, C++, or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>  
  
3. <span data-ttu-id="18a6f-123">Aby uruchomić przykład w konfiguracji na jednym lub wielu komputerach, postępuj zgodnie z instrukcjami w temacie [Uruchamianie przykładów Windows Communication Foundation](running-the-samples.md).</span><span class="sxs-lookup"><span data-stu-id="18a6f-123">To run the sample in a single- or cross-machine configuration, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="18a6f-124">Przykłady mogą być już zainstalowane na komputerze.</span><span class="sxs-lookup"><span data-stu-id="18a6f-124">The samples may already be installed on your machine.</span></span> <span data-ttu-id="18a6f-125">Przed kontynuowaniem Wyszukaj następujący katalog (domyślny).</span><span class="sxs-lookup"><span data-stu-id="18a6f-125">Check for the following (default) directory before continuing.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> <span data-ttu-id="18a6f-126">Jeśli ten katalog nie istnieje, przejdź do [przykładów Windows Communication Foundation (WCF) i Windows Workflow Foundation (WF) dla .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) , aby pobrać wszystkie Windows Communication Foundation (WCF) i [!INCLUDE[wf1](../../../../includes/wf1-md.md)] przykłady.</span><span class="sxs-lookup"><span data-stu-id="18a6f-126">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="18a6f-127">Ten przykład znajduje się w następującym katalogu.</span><span class="sxs-lookup"><span data-stu-id="18a6f-127">This sample is located in the following directory.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Binding\Custom\Transport`  
