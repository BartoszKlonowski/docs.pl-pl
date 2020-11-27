---
title: WebContentTypeMapper — przykład
ms.date: 03/30/2017
ms.assetid: a4fe59e7-44d8-43c6-a1f8-40c45223adca
ms.openlocfilehash: 550e763d30a7fa503f6500dcaa8f9b77ea499bca
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96283266"
---
# <a name="webcontenttypemapper-sample"></a><span data-ttu-id="c8287-102">WebContentTypeMapper — przykład</span><span class="sxs-lookup"><span data-stu-id="c8287-102">WebContentTypeMapper Sample</span></span>

<span data-ttu-id="c8287-103">Ten przykład pokazuje, jak mapować nowe typy zawartości na formaty treści wiadomości Windows Communication Foundation (WCF).</span><span class="sxs-lookup"><span data-stu-id="c8287-103">This sample demonstrates how to map new content types to Windows Communication Foundation (WCF) message body formats.</span></span>  
  
 <span data-ttu-id="c8287-104"><xref:System.ServiceModel.Description.WebHttpEndpoint>Element jest elementem kodera komunikatów sieci Web, który umożliwia platformie WCF odbieranie komunikatów JSON, XML lub nieprzetworzonych danych binarnych w tym samym punkcie końcowym.</span><span class="sxs-lookup"><span data-stu-id="c8287-104">The <xref:System.ServiceModel.Description.WebHttpEndpoint> element plugs in the Web message encoder, which allows WCF to receive JSON, XML, or raw binary messages at the same endpoint.</span></span> <span data-ttu-id="c8287-105">Koder określa format treści wiadomości, sprawdzając zawartość HTTP-Type żądania.</span><span class="sxs-lookup"><span data-stu-id="c8287-105">The encoder determines the body format of the message by looking at the HTTP content-type of the request.</span></span> <span data-ttu-id="c8287-106">Ten przykład wprowadza <xref:System.ServiceModel.Channels.WebContentTypeMapper> klasę, która umożliwia użytkownikowi kontrolowanie mapowania między typem zawartości i formatem treści.</span><span class="sxs-lookup"><span data-stu-id="c8287-106">This sample introduces the <xref:System.ServiceModel.Channels.WebContentTypeMapper> class, which allows the user to control the mapping between content type and body format.</span></span>  
  
 <span data-ttu-id="c8287-107">Funkcja WCF udostępnia zestaw domyślnych mapowań dla typów zawartości.</span><span class="sxs-lookup"><span data-stu-id="c8287-107">WCF provides a set of default mappings for content types.</span></span> <span data-ttu-id="c8287-108">Na przykład `application/json` mapuje do formatu JSON i `text/xml` mapuje do formatu XML.</span><span class="sxs-lookup"><span data-stu-id="c8287-108">For example, `application/json` maps to JSON and `text/xml` maps to XML.</span></span> <span data-ttu-id="c8287-109">Wszystkie typy zawartości, które nie są zamapowane na notację JSON lub XML, są mapowane na format nieprzetworzonych danych binarnych.</span><span class="sxs-lookup"><span data-stu-id="c8287-109">Any content type that is not mapped to JSON or XML is mapped to raw binary format.</span></span>  
  
 <span data-ttu-id="c8287-110">W niektórych scenariuszach (na przykład interfejsów API wypychania) Deweloper usługi nie kontroluje typu zawartości zwracanej przez klienta.</span><span class="sxs-lookup"><span data-stu-id="c8287-110">In some scenarios (for example, push-style APIs), the service developer does not control the content type returned by the client.</span></span> <span data-ttu-id="c8287-111">Na przykład klienci mogą zwrócić kod JSON jako `text/javascript` zamiast `application/json` .</span><span class="sxs-lookup"><span data-stu-id="c8287-111">For example, clients might return JSON as `text/javascript` instead of `application/json`.</span></span> <span data-ttu-id="c8287-112">W takim przypadku deweloper usług musi dostarczyć typ, który pochodzi od, <xref:System.ServiceModel.Channels.WebContentTypeMapper> Aby prawidłowo obsłużyć dany typ zawartości, jak pokazano w poniższym przykładowym kodzie.</span><span class="sxs-lookup"><span data-stu-id="c8287-112">In this case, the service developer must provide a type that derives from <xref:System.ServiceModel.Channels.WebContentTypeMapper> to handle the given content type correctly, as shown in the following sample code.</span></span>  
  
```csharp  
public class JsonContentTypeMapper : WebContentTypeMapper  
{  
    public override WebContentFormat  
               GetMessageFormatForContentType(string contentType)  
    {  
        if (contentType == "text/javascript")  
        {  
            return WebContentFormat.Json;  
        }  
        else  
        {  
            return WebContentFormat.Default;  
        }  
    }  
}  
```  
  
 <span data-ttu-id="c8287-113">Typ musi przesłaniać <xref:System.ServiceModel.Channels.WebContentTypeMapper.GetMessageFormatForContentType%28System.String%29> metodę.</span><span class="sxs-lookup"><span data-stu-id="c8287-113">The type must override the <xref:System.ServiceModel.Channels.WebContentTypeMapper.GetMessageFormatForContentType%28System.String%29> method.</span></span> <span data-ttu-id="c8287-114">Metoda musi oszacować `contentType` argument i zwracać jedną z następujących wartości: <xref:System.ServiceModel.Channels.WebContentFormat.Json> , <xref:System.ServiceModel.Channels.WebContentFormat.Xml> , <xref:System.ServiceModel.Channels.WebContentFormat.Raw> , lub <xref:System.ServiceModel.Channels.WebContentFormat.Default> .</span><span class="sxs-lookup"><span data-stu-id="c8287-114">The method must evaluate the `contentType` argument and return one of the following values: <xref:System.ServiceModel.Channels.WebContentFormat.Json>, <xref:System.ServiceModel.Channels.WebContentFormat.Xml>, <xref:System.ServiceModel.Channels.WebContentFormat.Raw>, or <xref:System.ServiceModel.Channels.WebContentFormat.Default>.</span></span> <span data-ttu-id="c8287-115">Zwracanie <xref:System.ServiceModel.Channels.WebContentFormat.Default> wartości do domyślnych mapowań kodera komunikatów sieci Web.</span><span class="sxs-lookup"><span data-stu-id="c8287-115">Returning <xref:System.ServiceModel.Channels.WebContentFormat.Default> defers to the default Web message encoder mappings.</span></span> <span data-ttu-id="c8287-116">W poprzednim przykładowym kodzie `text/javascript` Typ zawartości jest mapowany na format JSON, a wszystkie inne mapowania pozostają bez zmian.</span><span class="sxs-lookup"><span data-stu-id="c8287-116">In the previous sample code, the `text/javascript` content type is mapped to JSON, and all other mappings remain unchanged.</span></span>  
  
 <span data-ttu-id="c8287-117">Aby użyć `JsonContentTypeMapper` klasy, należy użyć następujących danych w Web.config:</span><span class="sxs-lookup"><span data-stu-id="c8287-117">To use the `JsonContentTypeMapper` class, use the following in your Web.config:</span></span>  
  
```xml  
<system.serviceModel>  
  <standardEndpoints>  
    <webHttpEndpoint>  
      <standardEndpoint name="" contentTypeMapper="Microsoft.Samples.WebContentTypeMapper.JsonContentTypeMapper, JsonContentTypeMapper, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />  
    </webHttpEndpoint>  
  </standardEndpoints>  
</system.serviceModel>  
```  
  
 <span data-ttu-id="c8287-118">Aby sprawdzić wymagania dotyczące używania JsonContentTypeMapper, Usuń atrybut contentTypeMapper z powyższego pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="c8287-118">To verify the requirement for using the JsonContentTypeMapper, remove the contentTypeMapper attribute from the above configuration file.</span></span> <span data-ttu-id="c8287-119">Nie można załadować strony klienta podczas próby `text/javascript` wysłania zawartości JSON przy użyciu programu.</span><span class="sxs-lookup"><span data-stu-id="c8287-119">The client page fails to load when attempting to use `text/javascript` to send JSON content.</span></span>  
  
### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="c8287-120">Aby skonfigurować, skompilować i uruchomić przykład</span><span class="sxs-lookup"><span data-stu-id="c8287-120">To set up, build, and run the sample</span></span>  
  
1. <span data-ttu-id="c8287-121">Upewnij się, że została wykonana [Procedura konfiguracji jednorazowej dla przykładów Windows Communication Foundation](one-time-setup-procedure-for-the-wcf-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c8287-121">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>  
  
2. <span data-ttu-id="c8287-122">Skompiluj rozwiązanie WebContentTypeMapperSample. sln zgodnie z opisem w temacie [Tworzenie przykładów Windows Communication Foundation](building-the-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c8287-122">Build the solution WebContentTypeMapperSample.sln as described in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>  
  
3. <span data-ttu-id="c8287-123">Przejdź do `http://localhost/ServiceModelSamples/JCTMClientPage.htm` (nie otwieraj JCTMClientPage.htm w przeglądarce z katalogu projektu).</span><span class="sxs-lookup"><span data-stu-id="c8287-123">Navigate to `http://localhost/ServiceModelSamples/JCTMClientPage.htm` (do not open JCTMClientPage.htm in the browser from within the project directory).</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="c8287-124">Przykłady mogą być już zainstalowane na komputerze.</span><span class="sxs-lookup"><span data-stu-id="c8287-124">The samples may already be installed on your machine.</span></span> <span data-ttu-id="c8287-125">Przed kontynuowaniem Wyszukaj następujący katalog (domyślny).</span><span class="sxs-lookup"><span data-stu-id="c8287-125">Check for the following (default) directory before continuing.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> <span data-ttu-id="c8287-126">Jeśli ten katalog nie istnieje, przejdź do [przykładów Windows Communication Foundation (WCF) i Windows Workflow Foundation (WF) dla .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) , aby pobrać wszystkie Windows Communication Foundation (WCF) i [!INCLUDE[wf1](../../../../includes/wf1-md.md)] przykłady.</span><span class="sxs-lookup"><span data-stu-id="c8287-126">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="c8287-127">Ten przykład znajduje się w następującym katalogu.</span><span class="sxs-lookup"><span data-stu-id="c8287-127">This sample is located in the following directory.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Ajax\WebContentTypeMapper`  
