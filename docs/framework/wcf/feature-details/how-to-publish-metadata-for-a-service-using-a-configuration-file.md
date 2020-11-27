---
title: 'Instrukcje: publikowanie metadanych dla usługi za pomocą pliku konfiguracji'
description: Dowiedz się, jak publikować metadane dla usługi WCF przy użyciu pliku konfiguracji. Publikowanie umożliwia klientom pobieranie tych metadanych przy użyciu żądania GET lub HTTP/GET.
ms.date: 03/30/2017
ms.assetid: f061443f-92df-4824-b36a-609c4cd14a17
ms.openlocfilehash: eb7aeb4275e367bfc4463a7289d4bc3ff77ff9f4
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96295551"
---
# <a name="how-to-publish-metadata-for-a-service-using-a-configuration-file"></a><span data-ttu-id="618ec-104">Instrukcje: publikowanie metadanych dla usługi za pomocą pliku konfiguracji</span><span class="sxs-lookup"><span data-stu-id="618ec-104">How to: Publish Metadata for a Service Using a Configuration File</span></span>

<span data-ttu-id="618ec-105">Jest to jeden z dwóch tematów, które przedstawiają Publikowanie metadanych dla usługi Windows Communication Foundation (WCF).</span><span class="sxs-lookup"><span data-stu-id="618ec-105">This is one of two how-to topics that demonstrate publishing metadata for a Windows Communication Foundation (WCF) service.</span></span> <span data-ttu-id="618ec-106">Istnieją dwa sposoby, aby określić, w jaki sposób usługa powinna publikować metadane przy użyciu pliku konfiguracji i przy użyciu kodu.</span><span class="sxs-lookup"><span data-stu-id="618ec-106">There are two ways to specify how a service should publish metadata, using a configuration file and using code.</span></span> <span data-ttu-id="618ec-107">W tym temacie przedstawiono sposób publikowania metadanych dla usługi za pomocą pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="618ec-107">This topic shows how to publish metadata for a service using a configuration file.</span></span>  
  
> [!CAUTION]
> <span data-ttu-id="618ec-108">W tym temacie przedstawiono sposób publikowania metadanych w niezabezpieczony sposób.</span><span class="sxs-lookup"><span data-stu-id="618ec-108">This topic shows how to publish metadata in an unsecure manner.</span></span> <span data-ttu-id="618ec-109">Dowolny klient może pobrać metadane z usługi.</span><span class="sxs-lookup"><span data-stu-id="618ec-109">Any client can retrieve the metadata from the service.</span></span> <span data-ttu-id="618ec-110">Jeśli wymagasz, aby usługa opublikowała metadane w bezpieczny sposób, zobacz [Niestandardowy bezpieczny metadanych punkt końcowy](../samples/custom-secure-metadata-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="618ec-110">If you require your service to publish metadata in a secure manner, see [Custom Secure Metadata Endpoint](../samples/custom-secure-metadata-endpoint.md).</span></span>  
  
 <span data-ttu-id="618ec-111">Aby uzyskać więcej informacji na temat publikowania metadanych w kodzie, zobacz [How to: Publikowanie metadanych dla usługi przy użyciu kodu](how-to-publish-metadata-for-a-service-using-code.md).</span><span class="sxs-lookup"><span data-stu-id="618ec-111">For more information about publishing metadata in code, see [How to: Publish Metadata for a Service Using Code](how-to-publish-metadata-for-a-service-using-code.md).</span></span> <span data-ttu-id="618ec-112">Publikowanie metadanych umożliwia klientom Pobieranie metadanych przy użyciu żądania GET WS-Transfer lub żądania HTTP/GET przy użyciu `?wsdl` ciągu zapytania.</span><span class="sxs-lookup"><span data-stu-id="618ec-112">Publishing metadata allows clients to retrieve the metadata using a WS-Transfer GET request or an HTTP/GET request using the `?wsdl` query string.</span></span> <span data-ttu-id="618ec-113">Aby upewnić się, że kod działa, Utwórz podstawową usługę WCF.</span><span class="sxs-lookup"><span data-stu-id="618ec-113">To be sure that the code is working, create a basic WCF service.</span></span> <span data-ttu-id="618ec-114">Dla uproszczenia podstawowa usługa samoobsługowa jest udostępniana w poniższym kodzie.</span><span class="sxs-lookup"><span data-stu-id="618ec-114">For simplicity, a basic self-hosted service is provided in the following code.</span></span>  
  
```csharp  
using System;  
using System.Runtime.Serialization;  
using System.ServiceModel;  
using System.ServiceModel.Description;  
  
namespace Metadata.Samples  
{  
    [ServiceContract]  
    public interface ISimpleService  
    {  
        [OperationContract]  
        string SimpleMethod(string msg);  
    }  
  
    class SimpleService : ISimpleService  
    {  
        public string SimpleMethod(string msg)  
        {  
            Console.WriteLine("The caller passed in " + msg);  
            return "Hello " + msg;  
        }  
    }  
  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            ServiceHost host = new ServiceHost(typeof(SimpleService),  
                new Uri("http://localhost:8001/MetadataSample"));
            try  
            {  
                // Open the service host to accept incoming calls  
                host.Open();  
  
                // The service can now be accessed.  
                Console.WriteLine("The service is ready.");  
                Console.WriteLine("Press <ENTER> to terminate service.");  
                Console.WriteLine();  
                Console.ReadLine();  
  
                // Close the ServiceHostBase to shutdown the service.  
                host.Close();  
            }  
            catch (CommunicationException commProblem)  
            {  
                Console.WriteLine("There was a communication problem. " + commProblem.Message);  
                Console.Read();  
            }  
        }  
    }  
}  
```  
  
 <span data-ttu-id="618ec-115">Ta usługa to usługa samodzielna, która jest konfigurowana przy użyciu pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="618ec-115">This service is a self-hosted service, which is configured using a configuration file.</span></span> <span data-ttu-id="618ec-116">Następujący plik konfiguracyjny służy jako punkt wyjścia.</span><span class="sxs-lookup"><span data-stu-id="618ec-116">The following configuration file serves as a starting point.</span></span>  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <services>  
      <service name="Metadata.Example.SimpleService">  
        <endpoint address=""  
                  binding="basicHttpBinding"  
                  contract="Metadata.Example.ISimpleService" />  
      </service>  
    </services>  
    <behaviors>  
  
    </behaviors>  
  </system.serviceModel>  
</configuration>  
```  
  
### <a name="to-publish-metadata-for-a-wcf-service-using-an-application-configuration-file"></a><span data-ttu-id="618ec-117">Aby opublikować metadane usługi WCF przy użyciu pliku konfiguracji aplikacji</span><span class="sxs-lookup"><span data-stu-id="618ec-117">To publish metadata for a WCF service using an application configuration file</span></span>  
  
1. <span data-ttu-id="618ec-118">W pliku App.config po elemencie zamykającym `</services>` Utwórz `<behaviors>` element.</span><span class="sxs-lookup"><span data-stu-id="618ec-118">Within the App.config file, after the closing `</services>` element, create a `<behaviors>` element.</span></span>  

2. <span data-ttu-id="618ec-119">W `<behaviors>` elemencie Dodaj `<serviceBehaviors>` element.</span><span class="sxs-lookup"><span data-stu-id="618ec-119">Within the `<behaviors>` element, add a `<serviceBehaviors>` element.</span></span>  

3. <span data-ttu-id="618ec-120">Dodaj `<behavior>` element do `<serviceBehaviors>` elementu i określ wartość `name` atrybutu `<behavior>` elementu.</span><span class="sxs-lookup"><span data-stu-id="618ec-120">Add a `<behavior>` element to the `<serviceBehaviors>` element and specify a value for the `name` attribute of the `<behavior>` element.</span></span>  

4. <span data-ttu-id="618ec-121">Dodaj `<serviceMetadata>` element do `<behavior>` elementu.</span><span class="sxs-lookup"><span data-stu-id="618ec-121">Add a `<serviceMetadata>` element to the `<behavior>` element.</span></span> <span data-ttu-id="618ec-122">Ustaw `httpGetEnabled` atrybut na `true` i `policyVersion` atrybut na Policy15.</span><span class="sxs-lookup"><span data-stu-id="618ec-122">Set the `httpGetEnabled` attribute to `true` and the `policyVersion` attribute to Policy15.</span></span> <span data-ttu-id="618ec-123">`httpGetEnabled` umożliwia usłudze reagowanie na żądania metadanych wykonywane przez żądanie HTTP GET.</span><span class="sxs-lookup"><span data-stu-id="618ec-123">`httpGetEnabled` allows the service to respond to metadata requests made by an HTTP GET request.</span></span> <span data-ttu-id="618ec-124">`policyVersion` instruuje usługę, aby była zgodna z WS-Policy 1,5 podczas generowania metadanych.</span><span class="sxs-lookup"><span data-stu-id="618ec-124">`policyVersion` tells the service to conform to WS-Policy 1.5 when generating metadata.</span></span>  

5. <span data-ttu-id="618ec-125">Dodaj `behaviorConfiguration` atrybut do `<service>` elementu i określ `name` atrybut `<behavior>` elementu dodanego w kroku 1, jak pokazano w poniższym przykładzie kodu.</span><span class="sxs-lookup"><span data-stu-id="618ec-125">Add a `behaviorConfiguration` attribute to the `<service>` element and specify the `name` attribute of the `<behavior>` element added in step 1, as shown in the following code example.</span></span>  
  
    ```xml  
    <services>  
      <service  
          name="Metadata.Example.SimpleService"  
          behaviorConfiguration="SimpleServiceBehavior">  
        ...  
      </service>  
    </services>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="SimpleServiceBehavior">  
          <serviceMetadata httpGetEnabled="True" policyVersion="Policy15" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
    ```  
  
6. <span data-ttu-id="618ec-126">Dodaj jeden lub więcej `<endpoint>` elementów z ustawioną umową do `IMetadataExchange` , jak pokazano w poniższym przykładzie kodu.</span><span class="sxs-lookup"><span data-stu-id="618ec-126">Add one or more `<endpoint>` elements with the contract set to `IMetadataExchange`, as shown in the following code example.</span></span>  
  
    ```xml  
    <services>  
      <service  
          name="Metadata.Example.SimpleService"  
          behaviorConfiguration="SimpleServiceBehavior">  
  
        <endpoint address=""  
                  binding="wsHttpBinding"  
                  contract="Metadata.Example.ISimpleService" />  
  
        <endpoint address="mex"  
                  binding="mexHttpBinding"  
                  contract="IMetadataExchange" />  
      </service>  
    </services>  
    ```  
  
7. <span data-ttu-id="618ec-127">Dla punktów końcowych metadanych dodanych w poprzednim kroku Ustaw `binding` atrybut na jeden z następujących:</span><span class="sxs-lookup"><span data-stu-id="618ec-127">For the metadata endpoints added in the previous step, set the `binding` attribute to one of the following:</span></span>  
  
    - <span data-ttu-id="618ec-128">`mexHttpBinding` dla publikacji HTTP.</span><span class="sxs-lookup"><span data-stu-id="618ec-128">`mexHttpBinding` for HTTP publication.</span></span>  
  
    - <span data-ttu-id="618ec-129">`mexHttpsBinding` dla publikacji HTTPS.</span><span class="sxs-lookup"><span data-stu-id="618ec-129">`mexHttpsBinding` for HTTPS publication.</span></span>  
  
    - <span data-ttu-id="618ec-130">`mexNamedPipeBinding` dla publikacji nazwanego potoku.</span><span class="sxs-lookup"><span data-stu-id="618ec-130">`mexNamedPipeBinding` for named pipe publication.</span></span>  
  
    - <span data-ttu-id="618ec-131">`mexTcpBinding` dla publikacji TCP.</span><span class="sxs-lookup"><span data-stu-id="618ec-131">`mexTcpBinding` for TCP publication.</span></span>  
  
8. <span data-ttu-id="618ec-132">Dla punktów końcowych metadanych dodanych w poprzednim kroku Ustaw adres równy:</span><span class="sxs-lookup"><span data-stu-id="618ec-132">For the metadata endpoints added in a previous step, set the address equal to:</span></span>  
  
    - <span data-ttu-id="618ec-133">Pusty ciąg, który będzie używać adresu podstawowego aplikacji hosta jako punktu publikacji, jeśli adres podstawowy jest taki sam jak powiązanie metadanych.</span><span class="sxs-lookup"><span data-stu-id="618ec-133">An empty string to use the host application's base address as the publication point if the base address is the same as the metadata binding.</span></span>  
  
    - <span data-ttu-id="618ec-134">Adres względny, jeśli aplikacja hosta ma adres podstawowy.</span><span class="sxs-lookup"><span data-stu-id="618ec-134">A relative address if the host application has a base address.</span></span>  
  
    - <span data-ttu-id="618ec-135">Adres bezwzględny.</span><span class="sxs-lookup"><span data-stu-id="618ec-135">An absolute address.</span></span>  
  
9. <span data-ttu-id="618ec-136">Skompiluj i uruchom aplikację konsolową.</span><span class="sxs-lookup"><span data-stu-id="618ec-136">Build and run the console application.</span></span>  
  
10. <span data-ttu-id="618ec-137">Użyj programu Internet Explorer, aby przejść do adresu podstawowego usługi ( `http://localhost:8001/MetadataSample` w tym przykładzie) i sprawdzić, czy Publikowanie metadanych jest włączone.</span><span class="sxs-lookup"><span data-stu-id="618ec-137">Use Internet Explorer to browse to the base address of the service (`http://localhost:8001/MetadataSample` in this sample) and verify that the metadata publishing is turned on.</span></span> <span data-ttu-id="618ec-138">Jeśli nie, zostanie wyświetlony komunikat w górnej części strony wyników: "Publikowanie metadanych dla tej usługi jest obecnie wyłączone".</span><span class="sxs-lookup"><span data-stu-id="618ec-138">If not, a message at the top of the resulting page displays: "Metadata publishing for this service is currently disabled."</span></span>  
  
### <a name="to-use-default-endpoints"></a><span data-ttu-id="618ec-139">Aby użyć domyślnych punktów końcowych</span><span class="sxs-lookup"><span data-stu-id="618ec-139">To use default endpoints</span></span>  
  
1. <span data-ttu-id="618ec-140">Aby skonfigurować metadane w usłudze korzystającej z domyślnych punktów końcowych, określ <xref:System.ServiceModel.Description.ServiceMetadataBehavior> w pliku konfiguracji, jak w poprzednim przykładzie, ale nie określaj żadnych punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="618ec-140">To configure metadata on a service that uses default endpoints, specify the <xref:System.ServiceModel.Description.ServiceMetadataBehavior> in the configuration file as in the previous example, but do not specify any endpoints.</span></span> <span data-ttu-id="618ec-141">Plik konfiguracji będzie wyglądał następująco.</span><span class="sxs-lookup"><span data-stu-id="618ec-141">The configuration file would then look like this.</span></span>  
  
    ```xml  
    <configuration>  
      <system.serviceModel>  
        <behaviors>  
          <serviceBehaviors>  
            <behavior name="SimpleServiceBehavior">  
              <serviceMetadata httpGetEnabled="True" policyVersion="Policy12" />  
            </behavior>  
          </serviceBehaviors>  
        </behaviors>  
  
      </system.serviceModel>  
    </configuration>  
    ```  
  
     <span data-ttu-id="618ec-142">Ponieważ usługa ma <xref:System.ServiceModel.Description.ServiceMetadataBehavior> `httpGetEnabled` ustawioną wartość `true` , usługa ma włączone metadane publikowania i ponieważ żadne punkty końcowe nie zostały jawnie dodane, środowisko uruchomieniowe dodaje domyślne punkty końcowe.</span><span class="sxs-lookup"><span data-stu-id="618ec-142">Because the service has a <xref:System.ServiceModel.Description.ServiceMetadataBehavior> with the `httpGetEnabled` set to `true`, the service has publishing metadata enabled, and because no endpoints were explicitly added, the runtime adds the default endpoints.</span></span> <span data-ttu-id="618ec-143">Aby uzyskać więcej informacji na temat domyślnych punktów końcowych, powiązań i zachowań, zobacz [Uproszczona konfiguracja](../simplified-configuration.md) i [Uproszczona konfiguracja dla usług WCF](../samples/simplified-configuration-for-wcf-services.md).</span><span class="sxs-lookup"><span data-stu-id="618ec-143">For more information about default endpoints, bindings, and behaviors, see [Simplified Configuration](../simplified-configuration.md) and [Simplified Configuration for WCF Services](../samples/simplified-configuration-for-wcf-services.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="618ec-144">Przykład</span><span class="sxs-lookup"><span data-stu-id="618ec-144">Example</span></span>  

 <span data-ttu-id="618ec-145">Poniższy przykład kodu pokazuje implementację podstawowej usługi WCF i plik konfiguracji, który publikuje metadane dla usługi.</span><span class="sxs-lookup"><span data-stu-id="618ec-145">The following code example shows the implementation of a basic WCF service and the configuration file that publishes metadata for the service.</span></span>  
  
```csharp  
using System;  
using System.Runtime.Serialization;  
using System.ServiceModel;  
using System.ServiceModel.Description;  
  
namespace Metadata.Samples  
{  
    [ServiceContract]  
    public interface ISimpleService  
    {  
        [OperationContract]  
        string SimpleMethod(string msg);  
    }  
  
    class SimpleService : ISimpleService  
    {  
        public string SimpleMethod(string msg)  
        {  
            Console.WriteLine("The caller passed in " + msg);  
            return "Hello " + msg;  
        }  
    }  
  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            ServiceHost host = new ServiceHost(typeof(SimpleService),  
                new Uri("http://localhost:8001/MetadataSample"));
            try  
            {  
                // Open the service host to accept incoming calls  
                host.Open();  
  
                // The service can now be accessed.  
                Console.WriteLine("The service is ready.");  
                Console.WriteLine("Press <ENTER> to terminate service.");  
                Console.WriteLine();  
                Console.ReadLine();  
  
                // Close the ServiceHostBase to shutdown the service.  
                host.Close();  
            }  
            catch (CommunicationException commProblem)  
            {  
                Console.WriteLine("There was a communication problem. " + commProblem.Message);  
                Console.Read();  
            }  
        }  
    }  
}  
```  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="SimpleServiceBehavior">  
          <serviceMetadata httpGetEnabled="True" policyVersion="Policy12" />  
          <serviceDebug includeExceptionDetailInFaults="False" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="see-also"></a><span data-ttu-id="618ec-146">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="618ec-146">See also</span></span>

- <xref:System.ServiceModel.Description.ServiceMetadataBehavior>
- [<span data-ttu-id="618ec-147">Instrukcje: Hostowanie usługi WCF w zarządzanej aplikacji</span><span class="sxs-lookup"><span data-stu-id="618ec-147">How to: Host a WCF Service in a Managed Application</span></span>](../how-to-host-a-wcf-service-in-a-managed-application.md)
- [<span data-ttu-id="618ec-148">Host samodzielny</span><span class="sxs-lookup"><span data-stu-id="618ec-148">Self-Host</span></span>](../samples/self-host.md)
- [<span data-ttu-id="618ec-149">Przegląd architektury metadanych</span><span class="sxs-lookup"><span data-stu-id="618ec-149">Metadata Architecture Overview</span></span>](metadata-architecture-overview.md)
- [<span data-ttu-id="618ec-150">Używanie metadanych</span><span class="sxs-lookup"><span data-stu-id="618ec-150">Using Metadata</span></span>](using-metadata.md)
- [<span data-ttu-id="618ec-151">Instrukcje: publikowanie metadanych dla usługi przy użyciu kodu</span><span class="sxs-lookup"><span data-stu-id="618ec-151">How to: Publish Metadata for a Service Using Code</span></span>](how-to-publish-metadata-for-a-service-using-code.md)
