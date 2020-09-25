---
title: <security> dla <webHttpBinding>
ms.date: 03/30/2017
ms.assetid: 727cf3d2-6f56-48ad-a59f-ba423edb9c83
ms.openlocfilehash: 60b863a0a2a846a60dde2e4b323a305b5096b1cc
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91169898"
---
# <a name="security-of-webhttpbinding"></a><span data-ttu-id="aaae7-102">\<security> dla \<webHttpBinding></span><span class="sxs-lookup"><span data-stu-id="aaae7-102">\<security> of \<webHttpBinding></span></span>

<span data-ttu-id="aaae7-103">Określa wymagania dotyczące zabezpieczeń dla punktu końcowego skonfigurowanego za pomocą [\<webHttpBinding>](webhttpbinding.md) .</span><span class="sxs-lookup"><span data-stu-id="aaae7-103">Specifies the security requirements for an endpoint configured with a [\<webHttpBinding>](webhttpbinding.md).</span></span>  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<bindings>**](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<webHttpBinding>**](webhttpbinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<binding>**\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<security>**  
  
## <a name="syntax"></a><span data-ttu-id="aaae7-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="aaae7-104">Syntax</span></span>  
  
```xml  
<system.ServiceModel>
  <bindings>
    <webHttpBinding>
      <binding name = "String">
        <security mode="None/Transport/TransportCredentialOnly">
          <transport clientCredentialType="Basic/Certificate/Digest/None/Ntlm/Windows"
                     proxyCredentialType="Basic/Digest/None/Ntlm/Windows"
                     realm="String" />
        </security>
      </binding>
    </webHttpBinding>
  </bindings>
</system.ServiceModel>
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="aaae7-105">Atrybuty i elementy</span><span class="sxs-lookup"><span data-stu-id="aaae7-105">Attributes and Elements</span></span>  

 <span data-ttu-id="aaae7-106">W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.</span><span class="sxs-lookup"><span data-stu-id="aaae7-106">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="aaae7-107">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="aaae7-107">Attributes</span></span>  
  
|<span data-ttu-id="aaae7-108">Atrybut</span><span class="sxs-lookup"><span data-stu-id="aaae7-108">Attribute</span></span>|<span data-ttu-id="aaae7-109">Opis</span><span class="sxs-lookup"><span data-stu-id="aaae7-109">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="aaae7-110">tryb</span><span class="sxs-lookup"><span data-stu-id="aaae7-110">mode</span></span>|<span data-ttu-id="aaae7-111">Określa, czy w punkcie końcowym nie są używane zabezpieczenia na poziomie transportu, czy żadne zabezpieczenia.</span><span class="sxs-lookup"><span data-stu-id="aaae7-111">Specifies whether transport-level security or no security is used by an endpoint.</span></span> <span data-ttu-id="aaae7-112">Wartość domyślna to `None`.</span><span class="sxs-lookup"><span data-stu-id="aaae7-112">The default is `None`.</span></span> <span data-ttu-id="aaae7-113">Ten atrybut jest typu <xref:System.ServiceModel.WebHttpSecurityMode> .</span><span class="sxs-lookup"><span data-stu-id="aaae7-113">This attribute is of type <xref:System.ServiceModel.WebHttpSecurityMode>.</span></span>|  
  
## <a name="mode-attribute"></a><span data-ttu-id="aaae7-114">Atrybut Mode</span><span class="sxs-lookup"><span data-stu-id="aaae7-114">Mode Attribute</span></span>  
  
|<span data-ttu-id="aaae7-115">Wartość</span><span class="sxs-lookup"><span data-stu-id="aaae7-115">Value</span></span>|<span data-ttu-id="aaae7-116">Opis</span><span class="sxs-lookup"><span data-stu-id="aaae7-116">Description</span></span>|  
|-----------|-----------------|  
|<span data-ttu-id="aaae7-117">Brak</span><span class="sxs-lookup"><span data-stu-id="aaae7-117">None</span></span>|<span data-ttu-id="aaae7-118">Zabezpieczenia są wyłączone.</span><span class="sxs-lookup"><span data-stu-id="aaae7-118">Security is disabled.</span></span>|  
|<span data-ttu-id="aaae7-119">Transport</span><span class="sxs-lookup"><span data-stu-id="aaae7-119">Transport</span></span>|<span data-ttu-id="aaae7-120">Zabezpieczenia są udostępniane przy użyciu protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="aaae7-120">Security is provided using HTTPS.</span></span> <span data-ttu-id="aaae7-121">Usługa musi być skonfigurowana przy użyciu certyfikatów SSL.</span><span class="sxs-lookup"><span data-stu-id="aaae7-121">The service needs to be configured with SSL certificates.</span></span> <span data-ttu-id="aaae7-122">Wiadomość jest całkowicie zabezpieczona przy użyciu protokołu HTTPS, a usługa jest uwierzytelniana przez klienta przy użyciu certyfikatu SSL usługi.</span><span class="sxs-lookup"><span data-stu-id="aaae7-122">The message is entirely secured using HTTPS and the service is authenticated by the client using the service’s SSL certificate.</span></span> <span data-ttu-id="aaae7-123">Uwierzytelnianie klienta jest kontrolowane przez `ClientCredentialType` atrybut [\<transport>](transport-of-webhttpbinding.md) .</span><span class="sxs-lookup"><span data-stu-id="aaae7-123">The client authentication is controlled through the `ClientCredentialType` attribute of the [\<transport>](transport-of-webhttpbinding.md).</span></span>|  
|<span data-ttu-id="aaae7-124">TransportCredentialOnly</span><span class="sxs-lookup"><span data-stu-id="aaae7-124">TransportCredentialOnly</span></span>|<span data-ttu-id="aaae7-125">Ten tryb nie zapewnia integralności i poufności komunikatów.</span><span class="sxs-lookup"><span data-stu-id="aaae7-125">This mode does not provide message integrity and confidentiality.</span></span> <span data-ttu-id="aaae7-126">Zapewnia uwierzytelnianie klienta oparte na protokole HTTP.</span><span class="sxs-lookup"><span data-stu-id="aaae7-126">It provides HTTP-based client authentication.</span></span> <span data-ttu-id="aaae7-127">Ten tryb powinien być używany z zachowaniem ostrożności.</span><span class="sxs-lookup"><span data-stu-id="aaae7-127">This mode should be used with caution.</span></span> <span data-ttu-id="aaae7-128">Powinna być używana w środowiskach, w których zabezpieczenia transportu są dostarczane przy użyciu innych metod (takich jak IPSec) i tylko uwierzytelnianie klienta jest udostępniane przez infrastrukturę WCF.</span><span class="sxs-lookup"><span data-stu-id="aaae7-128">It should be used in environments where the transport security is being provided by other means (such as IPSec) and only client authentication is provided by the WCF infrastructure.</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="aaae7-129">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="aaae7-129">Child Elements</span></span>  
  
|<span data-ttu-id="aaae7-130">Element</span><span class="sxs-lookup"><span data-stu-id="aaae7-130">Element</span></span>|<span data-ttu-id="aaae7-131">Opis</span><span class="sxs-lookup"><span data-stu-id="aaae7-131">Description</span></span>|  
|-------------|-----------------|  
|[\<transport>](transport-of-webhttpbinding.md)|<span data-ttu-id="aaae7-132">Definiuje ustawienia zabezpieczeń transportu.</span><span class="sxs-lookup"><span data-stu-id="aaae7-132">Defines the transport security settings.</span></span> <span data-ttu-id="aaae7-133">Ten element odnosi się do <xref:System.ServiceModel.Configuration.HttpTransportSecurityElement> typu.</span><span class="sxs-lookup"><span data-stu-id="aaae7-133">This element corresponds to the <xref:System.ServiceModel.Configuration.HttpTransportSecurityElement> type.</span></span>|  
  
### <a name="parent-elements"></a><span data-ttu-id="aaae7-134">Elementy nadrzędne</span><span class="sxs-lookup"><span data-stu-id="aaae7-134">Parent Elements</span></span>  
  
|<span data-ttu-id="aaae7-135">Element</span><span class="sxs-lookup"><span data-stu-id="aaae7-135">Element</span></span>|<span data-ttu-id="aaae7-136">Opis</span><span class="sxs-lookup"><span data-stu-id="aaae7-136">Description</span></span>|  
|-------------|-----------------|  
|[\<webHttpBinding>](webhttpbinding.md)|<span data-ttu-id="aaae7-137">Element powiązania, który jest używany do konfigurowania punktów końcowych dla usług sieci Web Windows Communication Foundation (WCF), które odpowiadają na żądania HTTP zamiast komunikatów protokołu SOAP.</span><span class="sxs-lookup"><span data-stu-id="aaae7-137">A binding element that is used to configure endpoints for Windows Communication Foundation (WCF) Web services that respond to HTTP requests instead of SOAP messages.</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="aaae7-138">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="aaae7-138">See also</span></span>

- <xref:System.ServiceModel.Configuration.WebHttpBindingElement>
- <xref:System.ServiceModel.Configuration.WSHttpSecurityElement>
- <xref:System.ServiceModel.WebHttpBinding.Security%2A>
- <xref:System.ServiceModel.Configuration.WebHttpBindingElement.Security%2A>
- <xref:System.ServiceModel.WebHttpSecurity>
- [<span data-ttu-id="aaae7-139">Zabezpieczanie usług i klientów</span><span class="sxs-lookup"><span data-stu-id="aaae7-139">Securing Services and Clients</span></span>](../../../wcf/feature-details/securing-services-and-clients.md)
- [<span data-ttu-id="aaae7-140">Wybieranie typu poświadczeń</span><span class="sxs-lookup"><span data-stu-id="aaae7-140">Selecting a Credential Type</span></span>](../../../wcf/feature-details/selecting-a-credential-type.md)
- [<span data-ttu-id="aaae7-141">Powiązania</span><span class="sxs-lookup"><span data-stu-id="aaae7-141">Bindings</span></span>](../../../wcf/bindings.md)
- [<span data-ttu-id="aaae7-142">Konfigurowanie powiązań dostarczanych przez system</span><span class="sxs-lookup"><span data-stu-id="aaae7-142">Configuring System-Provided Bindings</span></span>](../../../wcf/feature-details/configuring-system-provided-bindings.md)
- [<span data-ttu-id="aaae7-143">Konfigurowanie usług i klientów za pomocą wiązań</span><span class="sxs-lookup"><span data-stu-id="aaae7-143">Using Bindings to Configure Services and Clients</span></span>](../../../wcf/using-bindings-to-configure-services-and-clients.md)
- [\<binding>](bindings.md)
- [<span data-ttu-id="aaae7-144">Model programowania protokołu HTTP sieci Web w programie WCF</span><span class="sxs-lookup"><span data-stu-id="aaae7-144">WCF Web HTTP Programming Model</span></span>](../../../wcf/feature-details/wcf-web-http-programming-model.md)
