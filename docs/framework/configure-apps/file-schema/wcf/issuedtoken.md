---
title: <issuedToken>
ms.date: 03/30/2017
ms.assetid: b6eae4b7-a6cd-4e1a-b0f6-f407022550b0
ms.openlocfilehash: 9f3feb11fbe45cbb4b952c70feaa99f9c481dd2b
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91157372"
---
# \<issuedToken>

Określa niestandardowy token używany do uwierzytelniania klienta w usłudze.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<endpointBehaviors>**](endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<behavior>**](behavior-of-endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<clientCredentials>**](clientcredentials.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<issuedToken>**  
  
## <a name="syntax"></a>Składnia  
  
```xml  
<issuedToken cacheIssuedTokens="Boolean"
             defaultKeyEntropyMode="ClientEntropy/ServerEntropy/CombinedEntropy"
             issuedTokenRenewalThresholdPercentage = "0 to 100"
             issuerChannelBehaviors="String"
             localIssuerChannelBehaviors="String"
             maxIssuedTokenCachingTime="TimeSpan">
</issuedToken>
```  
  
## <a name="attributes-and-elements"></a>Atrybuty i elementy  

 W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.  
  
### <a name="attributes"></a>Atrybuty  
  
|Atrybut|Opis|  
|---------------|-----------------|  
|`cacheIssuedTokens`|Opcjonalny atrybut logiczny, który określa, czy tokeny są buforowane. Wartość domyślna to `true`.|  
|`defaultKeyEntropyMode`|Opcjonalny atrybut ciągu, który określa, które losowe wartości (entropie) są używane dla operacji uzgadniania. Wartości to `ClientEntropy` , `ServerEntropy` i `CombinedEntropy` , wartość domyślna to `CombinedEntropy` . Ten atrybut jest typu <xref:System.ServiceModel.Security.SecurityKeyEntropyMode> .|  
|`issuedTokenRenewalThresholdPercentage`|Opcjonalny atrybut Integer, który określa wartość procentową prawidłowego przedziału czasowego (dostarczonych przez wystawcę tokenu), która może upłynąć przed odnowieniem tokenu. Wartości to od 0 do 100. Wartość domyślna to 60, co oznacza, że 60% czasu kończy się przed próbą odnowienia.|  
|`issuerChannelBehaviors`|Opcjonalny atrybut, który określa zachowania kanału do użycia podczas komunikacji z wystawcą.|  
|`localIssuerChannelBehaviors`|Opcjonalny atrybut, który określa zachowania kanału do użycia podczas komunikowania się z lokalnym wystawcą.|  
|`maxIssuedTokenCachingTime`|Opcjonalny atrybut TimeSpan, który określa czas, przez jaki wystawione tokeny są buforowane, gdy Wystawca tokenu (STS) nie określa czasu. Wartość domyślna to "10675199.02:48:05.4775807".|  
  
### <a name="child-elements"></a>Elementy podrzędne  
  
|Element|Opis|  
|-------------|-----------------|  
|[\<localIssuer>](localissuer.md)|Określa adres lokalnego wystawcy tokenu i powiązania używanego do komunikacji z punktem końcowym.|  
|[\<issuerChannelBehaviors>](issuerchannelbehaviors-element.md)|Określa zachowania punktu końcowego, który ma być używany podczas kontaktowania się z lokalnym wystawcą.|  
  
### <a name="parent-elements"></a>Elementy nadrzędne  
  
|Element|Opis|  
|-------------|-----------------|  
|[\<clientCredentials>](clientcredentials.md)|Określa poświadczenia używane do uwierzytelniania klienta w usłudze.|  
  
## <a name="remarks"></a>Uwagi  

 Wystawiony token jest niestandardowym typem poświadczeń używanym na przykład podczas uwierzytelniania przy użyciu usługi bezpiecznego tokenu (STS) w scenariuszu federacyjnym. Domyślnie token jest tokenem SAML. Aby uzyskać więcej informacji, zobacz [federacyjne i wystawione tokeny](../../../wcf/feature-details/federation-and-issued-tokens.md)oraz [federacyjnego i wystawione tokeny](../../../wcf/feature-details/federation-and-issued-tokens.md).  
  
 Ta sekcja zawiera elementy używane do konfigurowania lokalnego wystawcy tokenów lub zachowań używanych z usługą tokenu zabezpieczającego. Aby uzyskać instrukcje dotyczące konfigurowania klienta do korzystania z wystawcy lokalnego, zobacz [How to: Configure a Local wystawca](../../../wcf/feature-details/how-to-configure-a-local-issuer.md).  
  
## <a name="see-also"></a>Zobacz też

- <xref:System.ServiceModel.Configuration.IssuedTokenClientElement>
- <xref:System.ServiceModel.Configuration.ClientCredentialsElement>
- <xref:System.ServiceModel.Description.ClientCredentials>
- <xref:System.ServiceModel.Configuration.ClientCredentialsElement.IssuedToken%2A>
- <xref:System.ServiceModel.Description.ClientCredentials.IssuedToken%2A>
- <xref:System.ServiceModel.Security.IssuedTokenClientCredential>
- [Zachowania zabezpieczeń](../../../wcf/feature-details/security-behaviors-in-wcf.md)
- [Zabezpieczanie usług i klientów](../../../wcf/feature-details/securing-services-and-clients.md)
- [Federacja i wystawione tokeny](../../../wcf/feature-details/federation-and-issued-tokens.md)
- [Zabezpieczanie klientów [WCF]](../../../wcf/securing-clients.md)
- [Instrukcje: tworzenie klienta federacyjnego](../../../wcf/feature-details/how-to-create-a-federated-client.md)
- [Instrukcje: konfigurowanie lokalnego wystawcy](../../../wcf/feature-details/how-to-configure-a-local-issuer.md)
- [Federacja i wystawione tokeny](../../../wcf/feature-details/federation-and-issued-tokens.md)
