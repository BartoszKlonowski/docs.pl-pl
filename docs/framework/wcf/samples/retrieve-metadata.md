---
title: Pobieranie metadanych
ms.date: 03/30/2017
ms.assetid: e8a6ef8c-a195-495a-a15e-7d92bdf0b28c
ms.openlocfilehash: a7a30fee36b14d0414f2f5bed513c21a694f3484
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96255406"
---
# <a name="retrieve-metadata"></a><span data-ttu-id="2ecd2-102">Pobieranie metadanych</span><span class="sxs-lookup"><span data-stu-id="2ecd2-102">Retrieve Metadata</span></span>

<span data-ttu-id="2ecd2-103">Ten przykład pokazuje, jak wdrożyć klienta, który dynamicznie pobiera metadane z usługi, aby wybrać punkt końcowy, z którym należy się komunikować.</span><span class="sxs-lookup"><span data-stu-id="2ecd2-103">This sample demonstrates how to implement a client that dynamically retrieves metadata from a service to choose an endpoint with which to communicate.</span></span> <span data-ttu-id="2ecd2-104">Ten przykład jest oparty na [wprowadzenie](getting-started-sample.md).</span><span class="sxs-lookup"><span data-stu-id="2ecd2-104">This sample is based on the [Getting Started](getting-started-sample.md).</span></span> <span data-ttu-id="2ecd2-105">Usługa została zmodyfikowana w celu uwidocznienia dwóch punktów końcowych — punktu końcowego na adresie podstawowym przy użyciu `basicHttpBinding` powiązania oraz bezpiecznego punktu końcowego w lokalizacji {*BaseAddress*}/Secure przy użyciu `wsHttpBinding` powiązania.</span><span class="sxs-lookup"><span data-stu-id="2ecd2-105">The service has been modified to expose two endpoints—an endpoint at the base address using the `basicHttpBinding` binding, and a secure endpoint at {*baseaddress*}/secure using the `wsHttpBinding` binding.</span></span> <span data-ttu-id="2ecd2-106">Zamiast konfigurować klienta z adresami punktów końcowych i powiązaniami, klient dynamicznie pobiera metadane dla usługi przy użyciu klasy, <xref:System.ServiceModel.Description.MetadataExchangeClient> a następnie Importuje metadane jako <xref:System.ServiceModel.Description.ServiceEndpointCollection> za pomocą <xref:System.ServiceModel.Description.WsdlImporter> klasy.</span><span class="sxs-lookup"><span data-stu-id="2ecd2-106">Instead of configuring the client with the endpoint addresses and bindings, the client dynamically retrieves the metadata for the service using the <xref:System.ServiceModel.Description.MetadataExchangeClient> class and then imports the metadata as a <xref:System.ServiceModel.Description.ServiceEndpointCollection> using the <xref:System.ServiceModel.Description.WsdlImporter> class.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="2ecd2-107">Procedura instalacji i instrukcje dotyczące kompilacji dla tego przykładu znajdują się na końcu tego tematu.</span><span class="sxs-lookup"><span data-stu-id="2ecd2-107">The setup procedure and build instructions for this sample are located at the end of this topic.</span></span>  
  
 <span data-ttu-id="2ecd2-108">Aplikacja kliencka używa zaimportowanego <xref:System.ServiceModel.Description.ServiceEndpointCollection> programu do tworzenia klientów do komunikowania się z usługą.</span><span class="sxs-lookup"><span data-stu-id="2ecd2-108">The client application uses the imported <xref:System.ServiceModel.Description.ServiceEndpointCollection> to create clients to communicate with the service.</span></span> <span data-ttu-id="2ecd2-109">Aplikacja kliencka wykonuje iterację przez każdy pobrany punkt końcowy i komunikuje się z każdym punktem końcowym, który implementuje `ICalculator` kontrakt.</span><span class="sxs-lookup"><span data-stu-id="2ecd2-109">The client application iterates through each retrieved endpoint and communicates with each endpoint that implements the `ICalculator` contract.</span></span> <span data-ttu-id="2ecd2-110">Odpowiednie adresy i powiązania są dostarczane ze pobranym punktem końcowym, aby klient został skonfigurowany do komunikacji z każdym punktem końcowym, jak pokazano w poniższym przykładowym kodzie.</span><span class="sxs-lookup"><span data-stu-id="2ecd2-110">The appropriate address and binding are provided with the retrieved endpoint, so that the client is configured to communicate with each endpoint, as shown in the following sample code.</span></span>  
  
```csharp
// Create a MetadataExchangeClient for retrieving metadata.  
EndpointAddress mexAddress = new EndpointAddress(ConfigurationManager.AppSettings["mexAddress"]);  
MetadataExchangeClient mexClient = new MetadataExchangeClient(mexAddress);  
  
// Retrieve the metadata for all endpoints using metadata exchange protocol (mex).  
MetadataSet metadataSet = mexClient.GetMetadata();  
  
//Convert the metadata into endpoints.  
WsdlImporter importer = new WsdlImporter(metadataSet);  
ServiceEndpointCollection endpoints = importer.ImportAllEndpoints();  
  
CalculatorClient client = null;  
ContractDescription contract = ContractDescription.GetContract(typeof(ICalculator));  
// Communicate with each endpoint that supports the ICalculator contract.  
foreach (ServiceEndpoint ep in endpoints)  
{  
    if (ep.Contract.Namespace.Equals(contract.Namespace) && ep.Contract.Name.Equals(contract.Name))  
    {  
        // Create a client using the endpoint address and binding.  
        client = new CalculatorClient(ep.Binding, new EndpointAddress(ep.Address.Uri));  
        Console.WriteLine("Communicate with endpoint: ");  
        Console.WriteLine("   AddressPath={0}", ep.Address.Uri.PathAndQuery);  
        Console.WriteLine("   Binding={0}", ep.Binding.Name);  
        // Call operations.  
        DoCalculations(client);  
  
        //Closing the client gracefully closes the connection and cleans up resources.  
        client.Close();  
    }  
}  
```  
  
 <span data-ttu-id="2ecd2-111">W oknie konsoli klienta zostaną wyświetlone operacje wysyłane do każdego z punktów końcowych, w których wyświetlana jest ścieżka adresu i nazwa powiązania.</span><span class="sxs-lookup"><span data-stu-id="2ecd2-111">The client console window displays the operations sent to each of the endpoints, displaying the address path and binding name.</span></span>  
  
### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="2ecd2-112">Aby skonfigurować, skompilować i uruchomić przykład</span><span class="sxs-lookup"><span data-stu-id="2ecd2-112">To set up, build, and run the sample</span></span>  
  
1. <span data-ttu-id="2ecd2-113">Upewnij się, że została wykonana [Procedura konfiguracji jednorazowej dla przykładów Windows Communication Foundation](one-time-setup-procedure-for-the-wcf-samples.md).</span><span class="sxs-lookup"><span data-stu-id="2ecd2-113">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>  
  
2. <span data-ttu-id="2ecd2-114">Aby skompilować wersję rozwiązania dla języka C#, C++ lub Visual Basic .NET, postępuj zgodnie z instrukcjami w temacie [Tworzenie przykładów Windows Communication Foundation](building-the-samples.md).</span><span class="sxs-lookup"><span data-stu-id="2ecd2-114">To build the C#, C++, or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>  
  
3. <span data-ttu-id="2ecd2-115">Aby uruchomić przykład w konfiguracji na jednym lub wielu komputerach, postępuj zgodnie z instrukcjami w temacie [Uruchamianie przykładów Windows Communication Foundation](running-the-samples.md).</span><span class="sxs-lookup"><span data-stu-id="2ecd2-115">To run the sample in a single- or cross-machine configuration, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="2ecd2-116">Przykłady mogą być już zainstalowane na komputerze.</span><span class="sxs-lookup"><span data-stu-id="2ecd2-116">The samples may already be installed on your machine.</span></span> <span data-ttu-id="2ecd2-117">Przed kontynuowaniem Wyszukaj następujący katalog (domyślny).</span><span class="sxs-lookup"><span data-stu-id="2ecd2-117">Check for the following (default) directory before continuing.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> <span data-ttu-id="2ecd2-118">Jeśli ten katalog nie istnieje, przejdź do [przykładów Windows Communication Foundation (WCF) i Windows Workflow Foundation (WF) dla .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) , aby pobrać wszystkie Windows Communication Foundation (WCF) i [!INCLUDE[wf1](../../../../includes/wf1-md.md)] przykłady.</span><span class="sxs-lookup"><span data-stu-id="2ecd2-118">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="2ecd2-119">Ten przykład znajduje się w następującym katalogu.</span><span class="sxs-lookup"><span data-stu-id="2ecd2-119">This sample is located in the following directory.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Client\RetrieveMetadata`  
