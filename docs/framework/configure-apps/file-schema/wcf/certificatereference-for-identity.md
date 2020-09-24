---
title: <certificateReference> dla <identity>
ms.date: 03/30/2017
ms.assetid: ac359c65-c22d-42d2-97de-db53b77cebdb
ms.openlocfilehash: f3daa2dcdf9b464b51cfb9c883cbb828bccb42df
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91149000"
---
# <a name="certificatereference-for-identity"></a>\<certificateReference> dla \<identity>

Określa ustawienia dla walidacji certyfikatu X. 509. Bezpieczny Windows Communication Foundation (WCF), który nawiązuje połączenie z punktem końcowym z tą tożsamością, sprawdza, czy oświadczenia przedstawione przez serwer zawierają oświadczenie tożsamości użyte do skonstruowania tej tożsamości.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<client>**](client.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<endpoint>**](endpoint-of-client.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<identity>**](identity.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<certificateReference>**  
  
## <a name="syntax"></a>Składnia  
  
```xml  
<certificateReference findValue="String"
                      isChainIncluded="Boolean"
                      storeName="AddressBook/AuthRoot/CertificateAuthority/Disallowed/My/Root/TrustedPeople/TrustedPublisher"
                      storeLocation="LocalMachine/CurrentUser"
                      X509FindType="FindByThumbPrint/FindBySubjectName/FindBySubjectDistinguishedName/FindByIssuerName/FindByIssuerDistinguishedName/FindBySerialNumber/FindByTimeValid/FindByTimeNotYetValid/FindByTemplateName/FindByApplicationPolicy/FindByCertificatePolicy/FindByExtension/FindByKeyUsage/FindBySubjectKeyIdentifier">
</certificateReference>
```  
  
## <a name="attributes-and-elements"></a>Atrybuty i elementy  

 W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.  
  
### <a name="attributes"></a>Atrybuty  
  
|Atrybut|Opis|  
|---------------|-----------------|  
|findValue|Określa wartość do wyszukania w magazynie certyfikatów X. 509. Typ zawarty w tym atrybucie musi spełniać wymagania określonej `X509FindType` wartości. Wartość domyślna to pusty ciąg.|  
|isChainIncluded|Wartość logiczna określająca, czy Walidacja jest wykonana przy użyciu łańcucha certyfikatów.|  
|storeLocation|Określa lokalizację magazynu certyfikatów, którego może użyć klient do zweryfikowania certyfikatu serwera.<br /><br /> Prawidłowe wartości to:<br /><br /> -LocalMachine: Magazyn certyfikatów przypisany do komputera lokalnego.<br />-CurrentUser: Magazyn certyfikatów przypisany do bieżącego użytkownika.<br /><br /> Wartość domyślna to LocalMachine.<br /><br /> Ten atrybut jest typu <xref:System.Security.Cryptography.X509Certificates.StoreLocation> .|  
|storeName|Określa nazwę magazynu certyfikatu X. 509 do otwarcia.<br /><br /> Prawidłowe wartości to:<br /><br /> -AddressBook: Magazyn certyfikatów dla innych użytkowników.<br />-AuthRoot: Magazyn certyfikatów dla urzędów certyfikacji innych firm.<br />-Urząd certyfikacji: Magazyn certyfikatów dla pośrednich urzędów certyfikacji.<br />-Niedozwolone: Magazyn certyfikatów dla odwołanych certyfikatów.<br />-My: Magazyn certyfikatów dla certyfikatów osobistych.<br />-Root: Magazyn certyfikatów dla zaufanych głównych urzędów certyfikacji.<br />-TrustedPeople: Magazyn certyfikatów dla bezpośrednio zaufanych osób i zasobów.<br />-TrustedPublisher: Magazyn certyfikatów dla bezpośrednio zaufanych wydawców.<br /><br /> Wartość domyślna to my.<br /><br /> Ten atrybut jest typu <xref:System.Security.Cryptography.X509Certificates.StoreName> .|  
|X509FindType|Określa typ wyszukiwania X. 509, który ma zostać wykonany. Typ zawarty w `findValue` atrybucie musi spełniać wymagania określone X509FindType.<br /><br /> Prawidłowe wartości to:<br /><br /> - FindByThumbPrint<br />- FindBySubjectName<br />- FindBySubjectDistinguishedName<br />- FindByIssuerName<br />- FindByIssuerDistinguishedName<br />- FindBySerialNumber<br />- FindByTimeValid<br />- FindByTimeNotYetValid<br />- FindByTemplateName<br />- FindByApplicationPolicy<br />- FindByCertificatePolicy<br />- FindByExtension<br />- FindByKeyUsage<br />- FindBySubjectKeyIdentifier<br /><br /> Wartość domyślna to FindBySubjectDistinguishedName.<br /><br /> Ten atrybut jest typu <xref:System.Security.Cryptography.X509Certificates.X509FindType> .|  
  
### <a name="child-elements"></a>Elementy podrzędne  

 Brak.  
  
### <a name="parent-elements"></a>Elementy nadrzędne  
  
|Element|Opis|  
|-------------|-----------------|  
|[\<identity>](identity.md)|Określa ustawienia, które umożliwiają uwierzytelnianie punktu końcowego przez inne punkty końcowe wymieniające z nim komunikaty.|  
  
## <a name="see-also"></a>Zobacz też

- <xref:System.ServiceModel.Configuration.CertificateReferenceElement>
- <xref:System.ServiceModel.Configuration.IdentityElement>
- <xref:System.ServiceModel.EndpointAddress>
- <xref:System.ServiceModel.EndpointAddress.Identity%2A>
