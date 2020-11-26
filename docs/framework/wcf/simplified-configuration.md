---
title: Uproszczona konfiguracja
description: Zapoznaj się z uproszczoną konfiguracją usług WCF. .NET Framework 4.6.1 zapewnia sposób zmniejszenia rozmiaru i złożoności konfiguracji usługi.
ms.date: 03/30/2017
ms.assetid: dcbe1f84-437c-495f-9324-2bc09fd79ea9
ms.openlocfilehash: 248fe05e5854dbbec1a66b046c4def3d11d30327
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96235951"
---
# <a name="simplified-configuration"></a><span data-ttu-id="082dc-104">Uproszczona konfiguracja</span><span class="sxs-lookup"><span data-stu-id="082dc-104">Simplified Configuration</span></span>

<span data-ttu-id="082dc-105">Konfigurowanie usług Windows Communication Foundation (WCF) może być złożonym zadaniem.</span><span class="sxs-lookup"><span data-stu-id="082dc-105">Configuring Windows Communication Foundation (WCF) services can be a complex task.</span></span> <span data-ttu-id="082dc-106">Istnieje wiele różnych opcji i nie zawsze można łatwo określić, które ustawienia są wymagane.</span><span class="sxs-lookup"><span data-stu-id="082dc-106">There are many different options and it is not always easy to determine what settings are required.</span></span> <span data-ttu-id="082dc-107">Pliki konfiguracji zwiększają elastyczność usług WCF, ale również są źródłem wielu trudno znaleźć problemy.</span><span class="sxs-lookup"><span data-stu-id="082dc-107">While configuration files increase the flexibility of WCF services, they also are the source for many hard to find problems.</span></span> [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] <span data-ttu-id="082dc-108">rozwiązuje te problemy i zapewnia sposób zmniejszenia rozmiaru i złożoności konfiguracji usługi.</span><span class="sxs-lookup"><span data-stu-id="082dc-108">addresses these problems and provides a way to reduce the size and complexity of service configuration.</span></span>  
  
## <a name="simplified-configuration"></a><span data-ttu-id="082dc-109">Uproszczona konfiguracja</span><span class="sxs-lookup"><span data-stu-id="082dc-109">Simplified Configuration</span></span>  

 <span data-ttu-id="082dc-110">W obszarze pliki konfiguracji usługi WCF sekcja <`system.serviceModel`> zawiera `service` element> <dla każdej hostowanej usługi.</span><span class="sxs-lookup"><span data-stu-id="082dc-110">In WCF service configuration files, the <`system.serviceModel`> section contains a <`service`> element for each service hosted.</span></span> <span data-ttu-id="082dc-111">Element <`service`> zawiera kolekcję <`endpoint` elementów>, które określają punkty końcowe uwidocznione dla każdej usługi i opcjonalnie zestaw zachowań usługi.</span><span class="sxs-lookup"><span data-stu-id="082dc-111">The <`service`> element contains a collection of <`endpoint`> elements that specify the endpoints exposed for each service and optionally a set of service behaviors.</span></span> <span data-ttu-id="082dc-112"><`endpoint` elementy> określają adres, powiązanie i kontrakt udostępniane przez punkt końcowy oraz opcjonalnie powiązania konfiguracji i punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="082dc-112">The <`endpoint`> elements specify the address, binding, and contract exposed by the endpoint, and optionally binding configuration and endpoint behaviors.</span></span> <span data-ttu-id="082dc-113">Sekcja <`system.serviceModel`> zawiera również `behaviors` element> <, który umożliwia określenie zachowań usługi lub punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="082dc-113">The <`system.serviceModel`> section also contains a <`behaviors`> element that allows you to specify service or endpoint behaviors.</span></span> <span data-ttu-id="082dc-114">W poniższym przykładzie przedstawiono `system.serviceModel` sekcję> <w pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="082dc-114">The following example shows the <`system.serviceModel`> section of a configuration file.</span></span>  
  
```xml  
<system.serviceModel>  
  <behaviors>  
    <serviceBehaviors>  
      <behavior name="MyServiceBehavior">  
        <serviceMetadata httpGetEnabled="true" />  
        <serviceDebug includeExceptionDetailInFaults="false" />  
      </behavior>  
    </serviceBehaviors>  
  </behaviors>  
  <bindings>  
   <basicHttpBinding>  
      <binding name=MyBindingConfig"  
               maxBufferSize="100"  
               maxReceiveBufferSize="100" />  
   </basicHttpBinding>  
   </bindings>   <services>  
    <service behaviorConfiguration="MyServiceBehavior"  
             name="MyService">  
      <endpoint address=""  
                binding="basicHttpBinding"  
                contract="ICalculator"  
                bindingConfiguration="MyBindingConfig" />  
      <endpoint address="mex"  
                binding="mexHttpBinding"  
                contract="IMetadataExchange"/>  
    </service>  
  </services>  
</system.serviceModel>  
```  
  
 [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] <span data-ttu-id="082dc-115">ułatwia skonfigurowanie usługi WCF poprzez usunięcie wymagania dotyczącego `service` elementu> <.</span><span class="sxs-lookup"><span data-stu-id="082dc-115">makes configuring a WCF service easier by removing the requirement for the <`service`> element.</span></span> <span data-ttu-id="082dc-116">Jeśli nie dodasz `service` sekcji> <ani nie dodasz żadnych punktów końcowych w `service` sekcji <> i Twoja usługa nie będzie programowo definiować żadnych punktów końcowych, zestaw domyślnych punktów końcowych zostanie automatycznie dodany do usługi, po jednej dla każdego adresu podstawowego usługi i dla każdego kontraktu zaimplementowanego przez usługę.</span><span class="sxs-lookup"><span data-stu-id="082dc-116">If you do not add a <`service`>  section or add any endpoints in a <`service`> section and your service does not programmatically define any endpoints, then a set of default endpoints are automatically added to your service, one for each service base address and for each contract implemented by your service.</span></span> <span data-ttu-id="082dc-117">W każdym z tych punktów końcowych adres punktu końcowego odpowiada adresowi bazowemu, powiązanie jest określane przez schemat adresów bazowych, a kontrakt jest zaimplementowany przez usługę.</span><span class="sxs-lookup"><span data-stu-id="082dc-117">In each of these endpoints, the endpoint address corresponds to the base address, the binding is determined by the base address scheme and the contract is the one implemented by your service.</span></span> <span data-ttu-id="082dc-118">Jeśli nie musisz określać żadnych punktów końcowych lub zachowań usług lub wprowadzić żadnych zmian w ustawieniach powiązania, nie musisz określać w ogóle pliku konfiguracji usługi.</span><span class="sxs-lookup"><span data-stu-id="082dc-118">If you do not need to specify any endpoints or service behaviors or make any binding setting changes, you do not need to specify a service configuration file at all.</span></span> <span data-ttu-id="082dc-119">Jeśli usługa implementuje dwie kontrakty, a host włącza transporty HTTP i TCP hosta usługi, program tworzy cztery domyślne punkty końcowe, po jednym dla każdego kontraktu przy użyciu poszczególnych transportów.</span><span class="sxs-lookup"><span data-stu-id="082dc-119">If a service implements two contracts and the host enables both HTTP and TCP transports the service host creates four default endpoints, one for each contract using each transport.</span></span> <span data-ttu-id="082dc-120">Aby utworzyć domyślne punkty końcowe, Host usługi musi wiedzieć, jakie powiązania mają być używane.</span><span class="sxs-lookup"><span data-stu-id="082dc-120">To create default endpoints the service host must know what bindings to use.</span></span> <span data-ttu-id="082dc-121">Te ustawienia są określone w sekcji <`protocolMappings`> w `system.serviceModel` sekcji <>.</span><span class="sxs-lookup"><span data-stu-id="082dc-121">These settings are specified in a <`protocolMappings`> section within the <`system.serviceModel`> section.</span></span> <span data-ttu-id="082dc-122">`protocolMappings`Sekcja> <zawiera listę schematów protokołu transportowego mapowanych na typy powiązań.</span><span class="sxs-lookup"><span data-stu-id="082dc-122">The <`protocolMappings`> section contains a list of transport protocol schemes mapped to binding types.</span></span> <span data-ttu-id="082dc-123">Host usługi korzysta z adresów bazowych, które są do niego przesyłane, aby określić, które powiązanie ma być używane.</span><span class="sxs-lookup"><span data-stu-id="082dc-123">The service host uses the base addresses passed to it to determine which binding to use.</span></span> <span data-ttu-id="082dc-124">Poniższy przykład używa `protocolMappings` elementu> <.</span><span class="sxs-lookup"><span data-stu-id="082dc-124">The following example uses the <`protocolMappings`> element.</span></span>  
  
> [!WARNING]
> <span data-ttu-id="082dc-125">Zmiana domyślnych elementów konfiguracji, takich jak powiązania lub zachowania, może mieć wpływ na usługi zdefiniowane na niższych poziomach w hierarchii konfiguracji, ponieważ mogą one korzystać z tych domyślnych powiązań i zachowań.</span><span class="sxs-lookup"><span data-stu-id="082dc-125">Changing default configuration elements, such as bindings or behaviors, might affect services defined in lower levels of the configuration hierarchy, since they might be using these default bindings and behaviors.</span></span> <span data-ttu-id="082dc-126">Z tego względu, inne zmiany powiązań domyślnych i zachowań muszą mieć świadomość, że te zmiany mogą wpływać na inne usługi w hierarchii.</span><span class="sxs-lookup"><span data-stu-id="082dc-126">Thus, whoever changes default bindings and behaviors needs to be aware that these changes might affect other services in the hierarchy.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="082dc-127">Usługi hostowane w usłudze Internet Information Services (IIS) lub Windows Process Activation Service (WAS) używają katalogu wirtualnego jako adresu podstawowego.</span><span class="sxs-lookup"><span data-stu-id="082dc-127">Services hosted under Internet Information Services (IIS) or Windows Process Activation Service (WAS) use the virtual directory as their base address.</span></span>  
  
```xml  
<protocolMapping>  
  <add scheme="http"     binding="basicHttpBinding" bindingConfiguration="MyBindingConfiguration"/>  
  <add scheme="net.tcp"  binding="netTcpBinding"/>  
  <add scheme="net.pipe" binding="netNamedPipeBinding"/>  
  <add scheme="net.msmq" binding="netMSMQBinding"/>  
</protocolMapping>  
```  
  
 <span data-ttu-id="082dc-128">W poprzednim przykładzie punkt końcowy o adresie podstawowym rozpoczynającym się od schematu "http" używa <xref:System.ServiceModel.BasicHttpBinding> .</span><span class="sxs-lookup"><span data-stu-id="082dc-128">In the previous example, an endpoint with a base address that starts with the "http" scheme uses the <xref:System.ServiceModel.BasicHttpBinding>.</span></span> <span data-ttu-id="082dc-129">Punkt końcowy o adresie podstawowym rozpoczynającym się od schematu "net. TCP" używa <xref:System.ServiceModel.NetTcpBinding> .</span><span class="sxs-lookup"><span data-stu-id="082dc-129">An endpoint with a base address that starts with the "net.tcp" scheme uses the <xref:System.ServiceModel.NetTcpBinding>.</span></span> <span data-ttu-id="082dc-130">Możesz przesłonić ustawienia w lokalnym pliku App.config lub Web.config.</span><span class="sxs-lookup"><span data-stu-id="082dc-130">You can override settings in a local App.config or Web.config file.</span></span>  
  
 <span data-ttu-id="082dc-131">Każdy element w `protocolMappings` sekcji> <musi określać schemat i powiązanie.</span><span class="sxs-lookup"><span data-stu-id="082dc-131">Each element within the <`protocolMappings`> section must specify a scheme and a binding.</span></span> <span data-ttu-id="082dc-132">Opcjonalnie można określić `bindingConfiguration` atrybut określający konfigurację powiązania w `bindings` sekcji <> pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="082dc-132">Optionally it can specify a `bindingConfiguration` attribute that specifies a binding configuration within the <`bindings`> section of the configuration file.</span></span> <span data-ttu-id="082dc-133">Jeśli nie `bindingConfiguration` zostanie określona, zostanie użyta Konfiguracja powiązania anonimowego dla odpowiedniego typu powiązania.</span><span class="sxs-lookup"><span data-stu-id="082dc-133">If no `bindingConfiguration` is specified, the anonymous binding configuration of the appropriate binding type is used.</span></span>  
  
 <span data-ttu-id="082dc-134">Zachowania usługi są skonfigurowane dla domyślnych punktów końcowych przy użyciu <anonimowe `behavior`> sekcje w `serviceBehaviors` sekcji <>.</span><span class="sxs-lookup"><span data-stu-id="082dc-134">Service behaviors are configured for the default endpoints by using anonymous <`behavior`> sections within <`serviceBehaviors`> sections.</span></span> <span data-ttu-id="082dc-135">Wszystkie nienazwane <`behavior` elementy> w <`serviceBehaviors`> są używane do konfigurowania zachowań usługi.</span><span class="sxs-lookup"><span data-stu-id="082dc-135">Any unnamed <`behavior`> elements within <`serviceBehaviors`> are used to configure service behaviors.</span></span> <span data-ttu-id="082dc-136">Na przykład następujący plik konfiguracji umożliwia Publikowanie metadanych usługi dla wszystkich usług na hoście.</span><span class="sxs-lookup"><span data-stu-id="082dc-136">For example, the following configuration file enables service metadata publishing for all services within the host.</span></span>  
  
```xml  
<system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <serviceMetadata httpGetEnabled="True"/>  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>    <!-- No <service> tag is necessary. Default endpoints are added to the service -->  
    <!-- The service behavior with name="" is picked up by the service -->  
 </system.serviceModel>  
```  
  
 <span data-ttu-id="082dc-137">Zachowania punktów końcowych konfiguruje się za pomocą <anonimowe> sekcjach `behavior` w `serviceBehaviors` sekcji <>.</span><span class="sxs-lookup"><span data-stu-id="082dc-137">Endpoint behaviors are configured by using anonymous <`behavior`> sections within <`serviceBehaviors`> sections.</span></span>  
  
 <span data-ttu-id="082dc-138">Poniższy przykład to plik konfiguracji odpowiadający pierwszemu na początku tego tematu, który korzysta z uproszczonego modelu konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="082dc-138">The following example is a configuration file equivalent to the one at the beginning of this topic that uses the simplified configuration model.</span></span>  
  
```xml  
<system.serviceModel>
    <behaviors>
      <serviceBehaviors>
        <behavior>
          <serviceMetadata httpGetEnabled="true" />
          <serviceDebug includeExceptionDetailInFaults="false" />
        </behavior>
      </serviceBehaviors>
    </behaviors>
    <bindings>
       <basicHttpBinding>
          <binding maxBufferSize="100"
                   maxReceiveBufferSize="100" />
       </basicHttpBinding>
    </bindings>
    <!-- No <service> tag is necessary. Default endpoints will be added to the service -->
    <!-- The service behavior with name="" will be picked up by the service -->
    <protocolMapping>
      <add scheme="http" binding="basicHttpBinding" />
  </protocolMapping>
  </system.serviceModel>
```  
  
> [!IMPORTANT]
> <span data-ttu-id="082dc-139">Ta funkcja odnosi się tylko do konfiguracji usługi WCF, a nie konfiguracji klienta.</span><span class="sxs-lookup"><span data-stu-id="082dc-139">This feature relates only to WCF service configuration, not client configuration.</span></span> <span data-ttu-id="082dc-140">W większości przypadków konfiguracja klienta WCF zostanie wygenerowana przez narzędzie, takie jak svcutil.exe lub dodanie odwołania do usługi z programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="082dc-140">Most times, WCF client configuration will be generated by a tool such as svcutil.exe or adding a service reference from Visual Studio.</span></span> <span data-ttu-id="082dc-141">W przypadku ręcznego konfigurowania klienta WCF należy dodać \<client> element do konfiguracji i określić wszystkie punkty końcowe, które chcesz wywołać.</span><span class="sxs-lookup"><span data-stu-id="082dc-141">If you are manually configuring a WCF client you will need to add a \<client> element to the configuration and specify any endpoints you wish to call.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="082dc-142">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="082dc-142">See also</span></span>

- [<span data-ttu-id="082dc-143">Konfigurowanie usług za pomocą plików konfiguracji</span><span class="sxs-lookup"><span data-stu-id="082dc-143">Configuring Services Using Configuration Files</span></span>](configuring-services-using-configuration-files.md)
- [<span data-ttu-id="082dc-144">Konfigurowanie powiązań dla usług</span><span class="sxs-lookup"><span data-stu-id="082dc-144">Configuring Bindings for Services</span></span>](configuring-bindings-for-wcf-services.md)
- [<span data-ttu-id="082dc-145">Konfigurowanie powiązań dostarczanych przez system</span><span class="sxs-lookup"><span data-stu-id="082dc-145">Configuring System-Provided Bindings</span></span>](./feature-details/configuring-system-provided-bindings.md)
- [<span data-ttu-id="082dc-146">Konfigurowanie usług</span><span class="sxs-lookup"><span data-stu-id="082dc-146">Configuring Services</span></span>](configuring-services.md)
- [<span data-ttu-id="082dc-147">Konfigurowanie usług WCF</span><span class="sxs-lookup"><span data-stu-id="082dc-147">Configuring WCF services</span></span>](configuring-services.md)
- [<span data-ttu-id="082dc-148">Konfigurowanie usług WCF w kodzie</span><span class="sxs-lookup"><span data-stu-id="082dc-148">Configuring WCF Services in Code</span></span>](configuring-wcf-services-in-code.md)
