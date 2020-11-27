---
title: Zabezpieczenia komunikatów z klientem dysponującym certyfikatem
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 99770573-c815-4428-a38c-e4335c8bd7ce
ms.openlocfilehash: 4a1cb6d804d313f438fc8e7a92946d55f73b9ee5
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96288583"
---
# <a name="message-security-with-a-certificate-client"></a><span data-ttu-id="3f289-102">Zabezpieczenia komunikatów z klientem dysponującym certyfikatem</span><span class="sxs-lookup"><span data-stu-id="3f289-102">Message Security with a Certificate Client</span></span>

<span data-ttu-id="3f289-103">W poniższym scenariuszu przedstawiono klienta i usługę Windows Communication Foundation (WCF) zabezpieczony przy użyciu trybu zabezpieczeń wiadomości.</span><span class="sxs-lookup"><span data-stu-id="3f289-103">The following scenario shows a Windows Communication Foundation (WCF) client and service secured using message security mode.</span></span> <span data-ttu-id="3f289-104">Zarówno klient, jak i usługa są uwierzytelniani przy użyciu certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="3f289-104">Both the client and the service are authenticated with certificates.</span></span> <span data-ttu-id="3f289-105">Aby uzyskać więcej informacji, zobacz [rozproszone zabezpieczenia aplikacji](distributed-application-security.md).</span><span class="sxs-lookup"><span data-stu-id="3f289-105">For more information, see [Distributed Application Security](distributed-application-security.md).</span></span>

 ![Zrzut ekranu pokazujący klienta z certyfikatem.](./media/message-security-with-a-certificate-client/client-with-certificate.gif)  
  
 <span data-ttu-id="3f289-107">Aby zapoznać się z przykładową aplikacją, zobacz [certyfikat zabezpieczeń wiadomości](../samples/message-security-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="3f289-107">For a sample application, see [Message Security Certificate](../samples/message-security-certificate.md).</span></span>  

|<span data-ttu-id="3f289-108">Charakterystyka</span><span class="sxs-lookup"><span data-stu-id="3f289-108">Characteristic</span></span>|<span data-ttu-id="3f289-109">Opis</span><span class="sxs-lookup"><span data-stu-id="3f289-109">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="3f289-110">Tryb zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="3f289-110">Security Mode</span></span>|<span data-ttu-id="3f289-111">Wiadomość</span><span class="sxs-lookup"><span data-stu-id="3f289-111">Message</span></span>|  
|<span data-ttu-id="3f289-112">Współdziałanie</span><span class="sxs-lookup"><span data-stu-id="3f289-112">Interoperability</span></span>|<span data-ttu-id="3f289-113">Tylko WCF</span><span class="sxs-lookup"><span data-stu-id="3f289-113">WCF only</span></span>|  
|<span data-ttu-id="3f289-114">Uwierzytelnianie (serwer)</span><span class="sxs-lookup"><span data-stu-id="3f289-114">Authentication (Server)</span></span>|<span data-ttu-id="3f289-115">Korzystanie z certyfikatu usługi</span><span class="sxs-lookup"><span data-stu-id="3f289-115">Using service certificate</span></span>|  
|<span data-ttu-id="3f289-116">Uwierzytelnianie (klient)</span><span class="sxs-lookup"><span data-stu-id="3f289-116">Authentication (Client)</span></span>|<span data-ttu-id="3f289-117">Korzystanie z certyfikatu klienta</span><span class="sxs-lookup"><span data-stu-id="3f289-117">Using client certificate</span></span>|  
|<span data-ttu-id="3f289-118">Integralność</span><span class="sxs-lookup"><span data-stu-id="3f289-118">Integrity</span></span>|<span data-ttu-id="3f289-119">Tak</span><span class="sxs-lookup"><span data-stu-id="3f289-119">Yes</span></span>|  
|<span data-ttu-id="3f289-120">Poufność</span><span class="sxs-lookup"><span data-stu-id="3f289-120">Confidentiality</span></span>|<span data-ttu-id="3f289-121">Tak</span><span class="sxs-lookup"><span data-stu-id="3f289-121">Yes</span></span>|  
|<span data-ttu-id="3f289-122">Transport</span><span class="sxs-lookup"><span data-stu-id="3f289-122">Transport</span></span>|<span data-ttu-id="3f289-123">HTTP</span><span class="sxs-lookup"><span data-stu-id="3f289-123">HTTP</span></span>|  
|<span data-ttu-id="3f289-124">Wiązanie</span><span class="sxs-lookup"><span data-stu-id="3f289-124">Binding</span></span>|<xref:System.ServiceModel.WSHttpBinding>|  
  
## <a name="service"></a><span data-ttu-id="3f289-125">Usługa</span><span class="sxs-lookup"><span data-stu-id="3f289-125">Service</span></span>  

 <span data-ttu-id="3f289-126">Poniższy kod i konfiguracja są przeznaczone do niezależnego uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="3f289-126">The following code and configuration are meant to run independently.</span></span> <span data-ttu-id="3f289-127">Wykonaj jedną z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="3f289-127">Do one of the following:</span></span>  
  
- <span data-ttu-id="3f289-128">Tworzenie usługi autonomicznej przy użyciu kodu bez konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="3f289-128">Create a stand-alone service using the code with no configuration.</span></span>  
  
- <span data-ttu-id="3f289-129">Utwórz usługę przy użyciu podanej konfiguracji, ale nie Definiuj żadnych punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="3f289-129">Create a service using the supplied configuration, but do not define any endpoints.</span></span>  
  
### <a name="code"></a><span data-ttu-id="3f289-130">Kod</span><span class="sxs-lookup"><span data-stu-id="3f289-130">Code</span></span>  

 <span data-ttu-id="3f289-131">Poniższy kod przedstawia sposób tworzenia punktu końcowego usługi, który używa zabezpieczeń komunikatów do ustanowienia bezpiecznego kontekstu.</span><span class="sxs-lookup"><span data-stu-id="3f289-131">The following code shows how to create a service endpoint that uses message security to establish a secure context.</span></span>  
  
 [!code-csharp[C_SecurityScenarios#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#10)]
 [!code-vb[C_SecurityScenarios#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#10)]  
  
### <a name="configuration"></a><span data-ttu-id="3f289-132">Konfigurowanie</span><span class="sxs-lookup"><span data-stu-id="3f289-132">Configuration</span></span>  

 <span data-ttu-id="3f289-133">Można użyć poniższej konfiguracji zamiast kodu.</span><span class="sxs-lookup"><span data-stu-id="3f289-133">The following configuration can be used instead of the code.</span></span>  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="ServiceCredentialsBehavior">  
          <serviceCredentials>  
            <serviceCertificate findValue="Contoso.com"  
                                x509FindType="FindBySubjectName" />  
          </serviceCredentials>  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
    <services>  
      <service behaviorConfiguration="ServiceCredentialsBehavior"
               name="ServiceModel.Calculator">  
        <endpoint address="http://localhost/Calculator"
                  binding="wsHttpBinding"  
                  bindingConfiguration="MessageAndCertificateClient"
                  name="SecuredByClientCertificate"  
                  contract="ServiceModel.ICalculator" />  
      </service>  
    </services>  
    <bindings>  
      <wsHttpBinding>  
        <binding name="WSHttpBinding_ICalculator">  
          <security mode="Message">  
            <message clientCredentialType="Certificate" />  
          </security>  
        </binding>  
      </wsHttpBinding>  
    </bindings>  
    <client />  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="client"></a><span data-ttu-id="3f289-134">Klient</span><span class="sxs-lookup"><span data-stu-id="3f289-134">Client</span></span>  

 <span data-ttu-id="3f289-135">Poniższy kod i konfiguracja są przeznaczone do niezależnego uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="3f289-135">The following code and configuration are meant to run independently.</span></span> <span data-ttu-id="3f289-136">Wykonaj jedną z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="3f289-136">Do one of the following:</span></span>  
  
- <span data-ttu-id="3f289-137">Utwórz klienta autonomicznego przy użyciu kodu (i kodu klienta).</span><span class="sxs-lookup"><span data-stu-id="3f289-137">Create a stand-alone client using the code (and client code).</span></span>  
  
- <span data-ttu-id="3f289-138">Utwórz klienta, który nie definiuje żadnych adresów punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="3f289-138">Create a client that does not define any endpoint addresses.</span></span> <span data-ttu-id="3f289-139">Zamiast tego należy użyć konstruktora klienta, który przyjmuje nazwę konfiguracji jako argument.</span><span class="sxs-lookup"><span data-stu-id="3f289-139">Instead, use the client constructor that takes the configuration name as an argument.</span></span> <span data-ttu-id="3f289-140">Przykład:</span><span class="sxs-lookup"><span data-stu-id="3f289-140">For example:</span></span>  
  
     [!code-csharp[C_SecurityScenarios#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#0)]
     [!code-vb[C_SecurityScenarios#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#0)]  
  
### <a name="code"></a><span data-ttu-id="3f289-141">Kod</span><span class="sxs-lookup"><span data-stu-id="3f289-141">Code</span></span>  

 <span data-ttu-id="3f289-142">Poniższy kod tworzy klienta.</span><span class="sxs-lookup"><span data-stu-id="3f289-142">The following code creates the client.</span></span> <span data-ttu-id="3f289-143">Powiązanie jest zabezpieczeniami trybu komunikatów, a typ poświadczeń klienta jest ustawiony na `Certificate` .</span><span class="sxs-lookup"><span data-stu-id="3f289-143">The binding is to message mode security, and the client credential type is set to `Certificate`.</span></span>  
  
 [!code-csharp[C_SecurityScenarios#17](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#17)]
 [!code-vb[C_SecurityScenarios#17](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#17)]  
  
### <a name="configuration"></a><span data-ttu-id="3f289-144">Konfigurowanie</span><span class="sxs-lookup"><span data-stu-id="3f289-144">Configuration</span></span>  

 <span data-ttu-id="3f289-145">Poniższa konfiguracja określa certyfikat klienta przy użyciu zachowania punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="3f289-145">The following configuration specifies the client certificate using an endpoint behavior.</span></span> <span data-ttu-id="3f289-146">Aby uzyskać więcej informacji o certyfikatach, zobacz [Praca z certyfikatami](working-with-certificates.md).</span><span class="sxs-lookup"><span data-stu-id="3f289-146">For more information about certificates, see [Working with Certificates](working-with-certificates.md).</span></span> <span data-ttu-id="3f289-147">Kod używa również `identity` elementu> <, aby określić system nazw domen (DNS) oczekiwanej tożsamości serwera.</span><span class="sxs-lookup"><span data-stu-id="3f289-147">The code also uses an <`identity`> element to specify a Domain Name System (DNS) of the expected server identity.</span></span> <span data-ttu-id="3f289-148">Aby uzyskać więcej informacji na temat tożsamości, zobacz [tożsamość usługi i uwierzytelnianie](service-identity-and-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="3f289-148">For more information about identity, see [Service Identity and Authentication](service-identity-and-authentication.md).</span></span>  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <endpointBehaviors>  
        <behavior name="endpointCredentialsBehavior">  
          <clientCredentials>  
            <clientCertificate findValue="Cohowinery.com"
               storeLocation="LocalMachine"  
              x509FindType="FindBySubjectName" />  
          </clientCredentials>  
        </behavior>  
      </endpointBehaviors>  
    </behaviors>  
    <bindings>  
      <wsHttpBinding>  
        <binding name="WSHttpBinding_ICalculator" >  
          <security mode="Message">  
            <message clientCredentialType="Certificate" />  
          </security>  
        </binding>  
      </wsHttpBinding>  
    </bindings>  
    <client>  
      <endpoint address="http://machineName/Calculator"
                behaviorConfiguration="endpointCredentialsBehavior"  
                binding="wsHttpBinding"  
                bindingConfiguration="WSHttpBinding_ICalculator"  
                contract="ICalculator"  
                name="WSHttpBinding_ICalculator">  
        <identity>  
          <dns value="Contoso.com" />  
        </identity>  
      </endpoint>  
    </client>  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="see-also"></a><span data-ttu-id="3f289-149">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="3f289-149">See also</span></span>

- [<span data-ttu-id="3f289-150">Przegląd zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="3f289-150">Security Overview</span></span>](security-overview.md)
- [<span data-ttu-id="3f289-151">Uwierzytelnianie i tożsamość usług</span><span class="sxs-lookup"><span data-stu-id="3f289-151">Service Identity and Authentication</span></span>](service-identity-and-authentication.md)
- [<span data-ttu-id="3f289-152">Praca z certyfikatami</span><span class="sxs-lookup"><span data-stu-id="3f289-152">Working with Certificates</span></span>](working-with-certificates.md)
- <span data-ttu-id="3f289-153">[Model zabezpieczeń dla sieci szkieletowej aplikacji systemu Windows Server](/previous-versions/appfabric/ee677202(v=azure.10))</span><span class="sxs-lookup"><span data-stu-id="3f289-153">[Security Model for Windows Server App Fabric](/previous-versions/appfabric/ee677202(v=azure.10))</span></span>
