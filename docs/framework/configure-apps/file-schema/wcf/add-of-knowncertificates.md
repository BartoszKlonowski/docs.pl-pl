---
title: <add> dla <knownCertificates>
ms.date: 03/30/2017
ms.assetid: 128aaabe-3f1a-4c3b-b59f-898d0f02910f
ms.openlocfilehash: 453593918de15613edb801cca8a16c9dbf71aa90
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91176087"
---
# <a name="add-of-knowncertificates"></a>\<add> dla \<knownCertificates>

Dodaje certyfikat X. 509 do kolekcji znanych certyfikatów.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<serviceBehaviors>**](servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<behavior>**](behavior-of-servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<serviceCredentials>**](servicecredentials.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<issuedTokenAuthentication>**](issuedtokenauthentication-of-servicecredentials.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<knownCertificates>**](knowncertificates.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<add>**  
  
## <a name="syntax"></a>Składnia  
  
```xml  
<knownCertificates>
   <add findValue="String"
      storeLocation="CurrentUser/LocalMachine"
      storeName="AddressBook/AuthRoot/CertificateAuthority/Disallowed/My/Root/TrustedPeople/TrustedPublisher"
      x509FindType="FindByThumbprint/FindBySubjectName/FindBySubjectDistinguishedName/FindByIssuerName/FindByIssuerDistinguishedName/FindBySerialNumber/FindByTimeValid/FindByTimeNotYetValid/FindBySerialNumber/FindByTimeExpired/FindByTemplateName/FindByApplicationPolicy/FindByCertificatePolicy/FindByExtension/FindByKeyUsage/FindBySubjectKeyIdentifier"/>
</knownCertificates>
```  
  
## <a name="attributes-and-elements"></a>Atrybuty i elementy  

 W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.  
  
### <a name="attributes"></a>Atrybuty  
  
|Atrybut|Opis|  
|---------------|-----------------|  
|findValue|Ciąg. Wartość do wyszukania.|  
|storeLocation|Licznik. Jedna z dwóch lokalizacji przechowywania do przeszukania.|  
|storeName|Licznik. Jeden z magazynów systemu do przeszukania.|  
|x509FindType|Licznik. Jedno z pól certyfikatów do przeszukania.|  
  
## <a name="findvalue-attribute"></a>findValue — atrybut  
  
|Wartość|Opis|  
|-----------|-----------------|  
|String|Wartość jest zależna od pola (określonego przez atrybut X509FindType), który jest przeszukiwany. Na przykład, jeśli szukasz odcisku palca, wartość musi być ciągiem liczb szesnastkowych.|  
  
## <a name="x509findtype-attribute"></a>x509FindType — atrybut  
  
|Wartość|Opis|  
|-----------|-----------------|  
|Wyliczenie|Dostępne są następujące wartości: FindByThumbprint, FindBySubjectName, FindBySubjectDistinguishedName, FindByIssuerName, FindByIssuerDistinguishedName, FindBySerialNumber, FindByTimeValid, FindByTimeNotYetValid, FindBySerialNumber, FindByTimeExpired, FindByTemplateName, FindByApplicationPolicy, FindByCertificatePolicy, FindByExtension, FindByKeyUsage, FindBySubjectKeyIdentifier.|  
  
## <a name="storelocation-attribute"></a>storeLocation — atrybut  
  
|Wartość|Opis|  
|-----------|-----------------|  
|Wyliczenie|CurrentUser lub LocalMachine.|  
  
## <a name="storename-attribute"></a>storeName — atrybut  
  
|Wartość|Opis|  
|-----------|-----------------|  
|Wyliczenie|Dostępne są następujące wartości: AddressBook, AuthRoot, urząd certyfikacji, niedozwolone, my, root, TrustedPeople i TrustedPublisher.|  
  
### <a name="child-elements"></a>Elementy podrzędne  

 Brak.  
  
### <a name="parent-elements"></a>Elementy nadrzędne  
  
|Element|Opis|  
|-------------|-----------------|  
|[\<knownCertificates>](knowncertificates.md)|Reprezentuje kolekcję certyfikatów X. 509, które są dostarczane przez usługę tokenu zabezpieczającego (STS) do sprawdzania poprawności tokenów zabezpieczających.|  
  
## <a name="remarks"></a>Uwagi  

 Scenariusz wystawionego tokenu ma trzy etapy. Na pierwszym etapie klient próbujący uzyskać dostęp do usługi jest nazywany *usługą bezpiecznego tokenu*. Usługa Secure Tokens następnie uwierzytelnia klienta, a następnie wystawia klientowi token, zwykle tokena "Security Assertions Markup Language" (SAML). Klient następnie wraca do usługi przy użyciu tokenu. Usługa bada token dla danych, które umożliwiają usłudze uwierzytelnianie tokenu i w związku z tym klienta. Aby uwierzytelnić token, certyfikat, którego używa usługa bezpiecznego tokenu, musi być znany usłudze.  
  
 [\<issuedTokenAuthentication>](issuedtokenauthentication-of-servicecredentials.md)Element jest repozytorium dla wszystkich takich certyfikatów usługi Secure Token Service. Aby dodać certyfikaty, użyj [\<knownCertificates>](knowncertificates.md) . Wstaw [ \<add> \<knownCertificates> element](add-of-knowncertificates.md) elementu dla każdego certyfikatu, jak pokazano w poniższym przykładzie.  
  
```xml  
<issuedTokenAuthentication>
  <knownCertificates>
    <add findValue="www.contoso.com"
         storeLocation="LocalMachine"
         storeName="My"
         X509FindType="FindBySubjectName" />
  </knownCertificates>
</issuedTokenAuthentication>
```  
  
 Domyślnie certyfikaty muszą być uzyskiwane z usługi bezpiecznego tokenu. Te "znane" certyfikaty zapewniają dostęp do usługi tylko uprawnionym klientom.  
  
 Aby sprawdzić warunki wymagane przez klienta do uwierzytelniania za pomocą usługi federacyjnej, a także więcej informacji na temat korzystania z tego elementu konfiguracji, zobacz [How to: Configure Credentials in a usługa federacyjna](../../../wcf/feature-details/how-to-configure-credentials-on-a-federation-service.md). Aby uzyskać więcej informacji na temat scenariuszy federacyjnych, zobacz [federacyjnego i wystawione tokeny](../../../wcf/feature-details/federation-and-issued-tokens.md).  
  
## <a name="example"></a>Przykład  

 Poniższy przykład dodaje certyfikat do repozytorium dla wszystkich certyfikatów usługi STS.  
  
```xml  
<serviceBehaviors>
  <behavior name="myServiceBehavior">
    <serviceCredentials>
      <issuedTokenAuthentication>
        <knownCertificates>
          <add findValue="www.contoso.com"
               storeLocation="LocalMachine"
               storeName="CertificateAuthority"
               x509FindType="FindByIssuerName" />
        </knownCertificates>
      </issuedTokenAuthentication>
    </serviceCredentials>
  </behavior>
</serviceBehaviors>
```  
  
## <a name="see-also"></a>Zobacz też

- <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator>
- <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator.AllowedAudienceUris%2A>
- <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator.AudienceUriMode%2A>
- <xref:System.ServiceModel.Configuration.IssuedTokenServiceElement.KnownCertificates%2A>
- <xref:System.ServiceModel.Configuration.X509CertificateTrustedIssuerElementCollection>
- <xref:System.ServiceModel.Configuration.X509CertificateTrustedIssuerElement>
- <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.KnownCertificates%2A>
- [\<knownCertificates>](knowncertificates.md)
- [Praca z certyfikatami](../../../wcf/feature-details/working-with-certificates.md)
- [Federacja i wystawione tokeny](../../../wcf/feature-details/federation-and-issued-tokens.md)
- [Instrukcje: konfigurowanie poświadczeń usługi federacyjnej](../../../wcf/feature-details/how-to-configure-credentials-on-a-federation-service.md)
- [Zabezpieczanie usług i klientów](../../../wcf/feature-details/securing-services-and-clients.md)
