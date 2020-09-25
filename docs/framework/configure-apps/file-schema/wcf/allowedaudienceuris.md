---
title: <allowedAudienceUris>
ms.date: 03/30/2017
ms.assetid: 0f4dc73d-d95d-4193-9755-7df4cf2b8e1c
ms.openlocfilehash: 602e25240ddbd337543efa8c4097d4da9e5c25e9
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91201632"
---
# \<allowedAudienceUris>

<span data-ttu-id="389d5-101">Reprezentuje kolekcję docelowych identyfikatorów URI, dla których <xref:System.IdentityModel.Tokens.SamlSecurityToken> może być przeznaczony token zabezpieczający, aby można je było traktować jako prawidłowe przez <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator> wystąpienie.</span><span class="sxs-lookup"><span data-stu-id="389d5-101">Represents a collection of target URIs for which the <xref:System.IdentityModel.Tokens.SamlSecurityToken> security token can be targeted for in order to be considered valid by a <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator> instance.</span></span>  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<serviceBehaviors>**](servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<behavior>**](behavior-of-servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<serviceCredentials>**](servicecredentials.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<issuedTokenAuthentication>**](issuedtokenauthentication-of-servicecredentials.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<allowedAudienceUris>**  
  
## <a name="syntax"></a><span data-ttu-id="389d5-102">Składnia</span><span class="sxs-lookup"><span data-stu-id="389d5-102">Syntax</span></span>  
  
```xml  
<allowedAudienceUris>
  <add allowedAudienceUri="String" />
</allowedAudienceUris>
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="389d5-103">Atrybuty i elementy</span><span class="sxs-lookup"><span data-stu-id="389d5-103">Attributes and Elements</span></span>  

 <span data-ttu-id="389d5-104">W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.</span><span class="sxs-lookup"><span data-stu-id="389d5-104">The following sections describe attributes, child elements, and parent elements</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="389d5-105">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="389d5-105">Attributes</span></span>  

 <span data-ttu-id="389d5-106">Brak.</span><span class="sxs-lookup"><span data-stu-id="389d5-106">None.</span></span>  
  
### <a name="child-elements"></a><span data-ttu-id="389d5-107">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="389d5-107">Child Elements</span></span>  
  
|<span data-ttu-id="389d5-108">Element</span><span class="sxs-lookup"><span data-stu-id="389d5-108">Element</span></span>|<span data-ttu-id="389d5-109">Opis</span><span class="sxs-lookup"><span data-stu-id="389d5-109">Description</span></span>|  
|-------------|-----------------|  
|[\<add>](add-of-allowedaudienceuris.md)|<span data-ttu-id="389d5-110">Dodaje docelowy identyfikator URI, dla którego <xref:System.IdentityModel.Tokens.SamlSecurityToken> może być przeznaczony token zabezpieczający, aby można go było traktować jako ważny przez <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator> wystąpienie.</span><span class="sxs-lookup"><span data-stu-id="389d5-110">Adds a target Uri for which the <xref:System.IdentityModel.Tokens.SamlSecurityToken> security token can be targeted for in order to be considered valid by a <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator> instance.</span></span>|  
  
### <a name="parent-elements"></a><span data-ttu-id="389d5-111">Elementy nadrzędne</span><span class="sxs-lookup"><span data-stu-id="389d5-111">Parent Elements</span></span>  
  
|<span data-ttu-id="389d5-112">Element</span><span class="sxs-lookup"><span data-stu-id="389d5-112">Element</span></span>|<span data-ttu-id="389d5-113">Opis</span><span class="sxs-lookup"><span data-stu-id="389d5-113">Description</span></span>|  
|-------------|-----------------|  
|[\<issuedTokenAuthentication>](issuedtokenauthentication-of-servicecredentials.md)|<span data-ttu-id="389d5-114">Określa token wystawiony jako poświadczenie usługi.</span><span class="sxs-lookup"><span data-stu-id="389d5-114">Specifies a token issued as a service credential.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="389d5-115">Uwagi</span><span class="sxs-lookup"><span data-stu-id="389d5-115">Remarks</span></span>  

 <span data-ttu-id="389d5-116">Tej kolekcji należy używać w aplikacji federacyjnej, która używa usługi tokenu zabezpieczającego (STS), która wystawia <xref:System.IdentityModel.Tokens.SamlSecurityToken> tokeny zabezpieczające.</span><span class="sxs-lookup"><span data-stu-id="389d5-116">You should use this collection in a federated application that utilizes a security token service (STS) that issues <xref:System.IdentityModel.Tokens.SamlSecurityToken> security tokens.</span></span> <span data-ttu-id="389d5-117">Gdy usługa STS wystawia token zabezpieczający, może określić identyfikator URI usług sieci Web, dla których jest przeznaczony token zabezpieczający poprzez dodanie <xref:System.IdentityModel.Tokens.SamlAudienceRestrictionCondition> do tokenu zabezpieczającego.</span><span class="sxs-lookup"><span data-stu-id="389d5-117">When the STS issues the security token, it can specify the URI of the Web services for which the security token is intended by adding a <xref:System.IdentityModel.Tokens.SamlAudienceRestrictionCondition> to the security token.</span></span> <span data-ttu-id="389d5-118">Dzięki temu <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator> Usługa sieci Web odbiorcy może sprawdzić, czy wystawiony token zabezpieczający jest przeznaczony dla tej usługi sieci Web, określając, że to sprawdzenie powinno nastąpić, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="389d5-118">That allows the <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator> for the recipient Web service to verify that the issued security token is intended for this Web service by specifying that this check should happen by doing the following:</span></span>  
  
- <span data-ttu-id="389d5-119">Ustaw `audienceUriMode` atrybut `<issuedTokenAuthentication>` na <xref:System.IdentityModel.Selectors.AudienceUriMode.Always> lub <xref:System.IdentityModel.Selectors.AudienceUriMode.BearerKeyOnly> .</span><span class="sxs-lookup"><span data-stu-id="389d5-119">Set the `audienceUriMode` attribute of `<issuedTokenAuthentication>` to <xref:System.IdentityModel.Selectors.AudienceUriMode.Always> or <xref:System.IdentityModel.Selectors.AudienceUriMode.BearerKeyOnly>.</span></span>  
  
- <span data-ttu-id="389d5-120">Określ zestaw prawidłowych identyfikatorów URI, dodając identyfikatory URI do tej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="389d5-120">Specify the set of valid URIs, by adding the URIs to this collection.</span></span>  
  
 <span data-ttu-id="389d5-121">Aby uzyskać więcej informacji, zobacz <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator>.</span><span class="sxs-lookup"><span data-stu-id="389d5-121">For more information, see <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator>.</span></span>  
  
 <span data-ttu-id="389d5-122">Aby uzyskać więcej informacji na temat używania tego elementu konfiguracji, zobacz [How to: Configure Credentials in a a usługa federacyjna](../../../wcf/feature-details/how-to-configure-credentials-on-a-federation-service.md).</span><span class="sxs-lookup"><span data-stu-id="389d5-122">For more information on using this configuration element, see [How to: Configure Credentials on a Federation Service](../../../wcf/feature-details/how-to-configure-credentials-on-a-federation-service.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="389d5-123">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="389d5-123">See also</span></span>

- <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator>
- <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator.AllowedAudienceUris%2A>
- <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator.AudienceUriMode%2A>
- <xref:System.ServiceModel.Configuration.IssuedTokenServiceElement.AllowedAudienceUris%2A>
- <xref:System.ServiceModel.Configuration.AllowedAudienceUriElementCollection>
- <xref:System.ServiceModel.Configuration.AllowedAudienceUriElement>
- <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.AllowedAudienceUris%2A>
- [\<issuedTokenAuthentication>](issuedtokenauthentication-of-servicecredentials.md)
- [\<add>](add-of-allowedaudienceuris.md)
- [<span data-ttu-id="389d5-124">Zachowania zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="389d5-124">Security Behaviors</span></span>](../../../wcf/feature-details/security-behaviors-in-wcf.md)
- [<span data-ttu-id="389d5-125">Zabezpieczanie usług i klientów</span><span class="sxs-lookup"><span data-stu-id="389d5-125">Securing Services and Clients</span></span>](../../../wcf/feature-details/securing-services-and-clients.md)
- [<span data-ttu-id="389d5-126">Instrukcje: konfigurowanie poświadczeń usługi federacyjnej</span><span class="sxs-lookup"><span data-stu-id="389d5-126">How to: Configure Credentials on a Federation Service</span></span>](../../../wcf/feature-details/how-to-configure-credentials-on-a-federation-service.md)
