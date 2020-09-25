---
title: <add> dla <allowedAudienceUris>
ms.date: 03/30/2017
ms.assetid: 4e7b7637-e0ea-4a91-988f-6b6ef28d9fc3
ms.openlocfilehash: bcbc9c7dbc5b57da2de2685fff8eee4aca64f7cc
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91181690"
---
# <a name="add-of-allowedaudienceuris"></a><span data-ttu-id="c1c92-102">\<add> dla \<allowedAudienceUris></span><span class="sxs-lookup"><span data-stu-id="c1c92-102">\<add> of \<allowedAudienceUris></span></span>

<span data-ttu-id="c1c92-103">Dodaje docelowy identyfikator URI, dla którego <xref:System.IdentityModel.Tokens.SamlSecurityToken> może być przeznaczony token zabezpieczający, aby można go było traktować jako ważny przez <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator> wystąpienie.</span><span class="sxs-lookup"><span data-stu-id="c1c92-103">Adds a target Uri for which the <xref:System.IdentityModel.Tokens.SamlSecurityToken> security token can be targeted for in order to be considered valid by a <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator> instance.</span></span>  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<serviceBehaviors>**](servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<behavior>**](behavior-of-servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<serviceCredentials>**](servicecredentials.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<issuedTokenAuthentication>**](issuedtokenauthentication-of-servicecredentials.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<allowedAudienceUris>**](allowedaudienceuris.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<add>**  
  
## <a name="syntax"></a><span data-ttu-id="c1c92-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="c1c92-104">Syntax</span></span>  
  
```xml  
<allowedAudienceUris>
  <add allowedAudienceUri="String" />
</allowedAudienceUris>
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="c1c92-105">Atrybuty i elementy</span><span class="sxs-lookup"><span data-stu-id="c1c92-105">Attributes and Elements</span></span>  

 <span data-ttu-id="c1c92-106">W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.</span><span class="sxs-lookup"><span data-stu-id="c1c92-106">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="c1c92-107">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="c1c92-107">Attributes</span></span>  
  
|<span data-ttu-id="c1c92-108">Atrybut</span><span class="sxs-lookup"><span data-stu-id="c1c92-108">Attribute</span></span>|<span data-ttu-id="c1c92-109">Opis</span><span class="sxs-lookup"><span data-stu-id="c1c92-109">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="c1c92-110">allowedAudienceUri</span><span class="sxs-lookup"><span data-stu-id="c1c92-110">allowedAudienceUri</span></span>|<span data-ttu-id="c1c92-111">Ciąg zawierający docelowy identyfikator URI, dla którego <xref:System.IdentityModel.Tokens.SamlSecurityToken> może być przeznaczony token zabezpieczający, aby można go było traktować jako ważny przez <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator> wystąpienie.</span><span class="sxs-lookup"><span data-stu-id="c1c92-111">A string that contains a target Uri for which the <xref:System.IdentityModel.Tokens.SamlSecurityToken> security token can be targeted for in order to be considered valid by a <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator> instance.</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="c1c92-112">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="c1c92-112">Child Elements</span></span>  

 <span data-ttu-id="c1c92-113">Brak.</span><span class="sxs-lookup"><span data-stu-id="c1c92-113">None.</span></span>  
  
### <a name="parent-elements"></a><span data-ttu-id="c1c92-114">Elementy nadrzędne</span><span class="sxs-lookup"><span data-stu-id="c1c92-114">Parent Elements</span></span>  
  
|<span data-ttu-id="c1c92-115">Element</span><span class="sxs-lookup"><span data-stu-id="c1c92-115">Element</span></span>|<span data-ttu-id="c1c92-116">Opis</span><span class="sxs-lookup"><span data-stu-id="c1c92-116">Description</span></span>|  
|-------------|-----------------|  
|[\<allowedAudienceUris>](allowedaudienceuris.md)|<span data-ttu-id="c1c92-117">Reprezentuje kolekcję docelowych identyfikatorów URI, dla których <xref:System.IdentityModel.Tokens.SamlSecurityToken> może być przeznaczony token zabezpieczający, aby można je było traktować jako prawidłowe przez <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator> wystąpienie.</span><span class="sxs-lookup"><span data-stu-id="c1c92-117">Represents a collection of target URIs for which the <xref:System.IdentityModel.Tokens.SamlSecurityToken> security token can be targeted for in order to be considered valid by a <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator> instance.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="c1c92-118">Uwagi</span><span class="sxs-lookup"><span data-stu-id="c1c92-118">Remarks</span></span>  

 <span data-ttu-id="c1c92-119">Tej kolekcji należy używać w aplikacji federacyjnej, która używa usługi tokenu zabezpieczającego (STS), która wystawia <xref:System.IdentityModel.Tokens.SamlSecurityToken> tokeny zabezpieczające.</span><span class="sxs-lookup"><span data-stu-id="c1c92-119">You should use this collection in a federated application that utilizes a security token service (STS) that issues <xref:System.IdentityModel.Tokens.SamlSecurityToken> security tokens.</span></span> <span data-ttu-id="c1c92-120">Gdy usługa STS wystawia token zabezpieczający, może określić identyfikator URI usług sieci Web, dla których jest przeznaczony token zabezpieczający poprzez dodanie <xref:System.IdentityModel.Tokens.SamlAudienceRestrictionCondition> do tokenu zabezpieczającego.</span><span class="sxs-lookup"><span data-stu-id="c1c92-120">When the STS issues the security token, it can specify the URI of the Web services for which the security token is intended by adding a <xref:System.IdentityModel.Tokens.SamlAudienceRestrictionCondition> to the security token.</span></span> <span data-ttu-id="c1c92-121">Dzięki temu <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator> Usługa sieci Web odbiorcy może sprawdzić, czy wystawiony token zabezpieczający jest przeznaczony dla tej usługi sieci Web, określając, że to sprawdzenie powinno nastąpić, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c1c92-121">That allows the <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator> for the recipient Web service to verify that the issued security token is intended for this Web service by specifying that this check should happen by doing the following:</span></span>  
  
- <span data-ttu-id="c1c92-122">Ustaw `audienceUriMode` atrybut `<issuedTokenAuthentication>` na <xref:System.IdentityModel.Selectors.AudienceUriMode.Always> lub <xref:System.IdentityModel.Selectors.AudienceUriMode.BearerKeyOnly> .</span><span class="sxs-lookup"><span data-stu-id="c1c92-122">Set the `audienceUriMode` attribute of `<issuedTokenAuthentication>` to <xref:System.IdentityModel.Selectors.AudienceUriMode.Always> or <xref:System.IdentityModel.Selectors.AudienceUriMode.BearerKeyOnly>.</span></span>  
  
- <span data-ttu-id="c1c92-123">Określ zestaw prawidłowych identyfikatorów URI, dodając identyfikatory URI do tej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="c1c92-123">Specify the set of valid URIs, by adding the URIs to this collection.</span></span>  
  
 <span data-ttu-id="c1c92-124">Aby uzyskać więcej informacji, zobacz <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator>.</span><span class="sxs-lookup"><span data-stu-id="c1c92-124">For more information, see <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator>.</span></span>  
  
 <span data-ttu-id="c1c92-125">Aby uzyskać więcej informacji na temat używania tego elementu konfiguracji, zobacz [How to: Configure Credentials in a a usługa federacyjna](../../../wcf/feature-details/how-to-configure-credentials-on-a-federation-service.md).</span><span class="sxs-lookup"><span data-stu-id="c1c92-125">For more information on using this configuration element, see [How to: Configure Credentials on a Federation Service](../../../wcf/feature-details/how-to-configure-credentials-on-a-federation-service.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="c1c92-126">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="c1c92-126">See also</span></span>

- <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator>
- <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator.AllowedAudienceUris%2A>
- <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator.AudienceUriMode%2A>
- <xref:System.ServiceModel.Configuration.IssuedTokenServiceElement.AllowedAudienceUris%2A>
- <xref:System.ServiceModel.Configuration.AllowedAudienceUriElementCollection>
- <xref:System.ServiceModel.Configuration.AllowedAudienceUriElement>
- <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.AllowedAudienceUris%2A>
- [\<allowedAudienceUris>](allowedaudienceuris.md)
- [\<issuedTokenAuthentication>](issuedtokenauthentication-of-servicecredentials.md)
- [<span data-ttu-id="c1c92-127">Zachowania zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="c1c92-127">Security Behaviors</span></span>](../../../wcf/feature-details/security-behaviors-in-wcf.md)
- [<span data-ttu-id="c1c92-128">Zabezpieczanie usług i klientów</span><span class="sxs-lookup"><span data-stu-id="c1c92-128">Securing Services and Clients</span></span>](../../../wcf/feature-details/securing-services-and-clients.md)
- [<span data-ttu-id="c1c92-129">Instrukcje: konfigurowanie poświadczeń usługi federacyjnej</span><span class="sxs-lookup"><span data-stu-id="c1c92-129">How to: Configure Credentials on a Federation Service</span></span>](../../../wcf/feature-details/how-to-configure-credentials-on-a-federation-service.md)
