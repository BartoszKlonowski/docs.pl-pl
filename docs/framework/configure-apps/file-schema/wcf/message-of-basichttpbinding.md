---
title: <message> dla <basicHttpBinding>
ms.date: 03/30/2017
ms.assetid: 51cdd329-6461-471a-8747-56c2299b61e5
ms.openlocfilehash: 8b1e889efc53d0132368111037399ea8872008b1
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91204869"
---
# <a name="message-of-basichttpbinding"></a>\<message> dla \<basicHttpBinding>

Definiuje ustawienia zabezpieczeń na poziomie wiadomości [\<basicHttpBinding>](basichttpbinding.md) .  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<bindings>**](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<basicHttpBinding>**](basichttpbinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<binding>**\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<security>**](security-of-basichttpbinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<message>**  
  
## <a name="syntax"></a>Składnia  
  
```xml  
<message algorithmSuite="Basic128/Basic192/Basic256/Basic128Rsa15/Basic256Rsa15/TripleDes/TripleDesRsa15/Basic128Sha256/Basic192Sha256/TripleDesSha256/Basic128Sha256Rsa15/Basic192Sha256Rsa15/Basic256Sha256Rsa15/TripleDesSha256Rsa15"
         clientCredentialType="UserName/Certificate" />
```  
  
## <a name="attributes-and-elements"></a>Atrybuty i elementy  

 W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.  
  
### <a name="attributes"></a>Atrybuty  
  
|Atrybut|Opis|  
|---------------|-----------------|  
|algorithmSuite|Ustawia szyfrowanie komunikatów i algorytmy zawijania kluczy. Ten atrybut jest typu <xref:System.ServiceModel.Security.SecurityAlgorithmSuite> , który określa algorytmy i rozmiary kluczy. Te algorytmy są mapowane na te określone w specyfikacji języka zasad zabezpieczeń (WS-SecurityPolicy).<br /><br /> Wartość domyślna to `Basic256`.|  
|Powiązania ClientCredentialType|Określa typ poświadczeń, które mają być używane podczas uwierzytelniania klienta przy użyciu zabezpieczeń opartych na komunikatach. Wartość domyślna to `UserName`.|  
  
## <a name="clientcredentialtype-attribute"></a>clientCredentialtype — atrybut  
  
|Wartość|Opis|  
|-----------|-----------------|  
|Nazwa użytkownika|-Wymaga uwierzytelnienia klienta na serwerze przy użyciu poświadczeń nazwy użytkownika. To poświadczenie należy określić przy użyciu [\<clientCredentials>](clientcredentials.md) .<br />— Usługa WCF nie obsługuje wysyłania skrótu hasła ani wyprowadzania kluczy przy użyciu haseł i używania tych kluczy do zabezpieczenia komunikatów. W związku z tym WCF wymusza, aby transport był zabezpieczony przy użyciu poświadczeń nazwy użytkownika. W przypadku programu `basicHttpBinding` wymagane jest skonfigurowanie kanału SSL.|  
|Certyfikat|Wymaga uwierzytelnienia klienta na serwerze przy użyciu certyfikatu. Poświadczenia klienta w tym przypadku należy określić przy użyciu [\<clientCredentials>](clientcredentials.md) i [\<clientCertificate>](clientcertificate-of-servicecredentials.md) . Ponadto w przypadku korzystania z trybu zabezpieczeń wiadomości klient musi być zainicjowany przy użyciu certyfikatu usługi. Poświadczenia usługi w tym przypadku należy określić przy użyciu <xref:System.ServiceModel.Description.ClientCredentials> klasy lub `ClientCredentials` zachowania elementu, a także określić certyfikat usługi przy użyciu [\<serviceCertificate>](servicecertificate-of-servicecredentials.md) .|  
  
### <a name="child-elements"></a>Elementy podrzędne  

 Brak  
  
### <a name="parent-elements"></a>Elementy nadrzędne  
  
|Element|Opis|  
|-------------|-----------------|  
|[\<security>](security-of-basichttpbinding.md)|Definiuje funkcje zabezpieczeń dla programu [\<basicHttpBinding>](basichttpbinding.md) .|  
  
## <a name="example"></a>Przykład  

 Ten przykład ilustruje sposób implementacji aplikacji, która korzysta z basicHttpBinding i zabezpieczenia komunikatów. W poniższym przykładzie konfiguracji dla usługi definicja punktu końcowego określa basicHttpBinding i odwołuje się do konfiguracji powiązania o nazwie `Binding1` . Certyfikat, którego używa Usługa do samodzielnego uwierzytelnienia klienta, jest ustawiany w `behaviors` sekcji pliku konfiguracji w obszarze `serviceCredentials` elementu. Tryb walidacji, który ma zastosowanie do certyfikatu używanego przez klienta do samodzielnego uwierzytelnienia w usłudze, jest również ustawiany w `behaviors` sekcji w obszarze `clientCertificate` elementu.  
  
 W pliku konfiguracji klienta określono te same informacje o powiązaniu i zabezpieczeniach.  
  
```xml  
<system.serviceModel>
  <services>
    <service name="Microsoft.ServiceModel.Samples.CalculatorService"
             behaviorConfiguration="CalculatorServiceBehavior">
      <host>
        <baseAddresses>
          <add baseAddress="http://localhost:8000/ServiceModelSamples/service" />
        </baseAddresses>
      </host>
      <!-- this endpoint is exposed at the base address provided by host: http://localhost:8000/ServiceModelSamples/service -->
      <endpoint address=""
                binding="basicHttpBinding"
                bindingConfiguration="Binding1"
                contract="Microsoft.ServiceModel.Samples.ICalculator" />
      <!-- the mex endpoint is exposed at http://localhost:8000/ServiceModelSamples/service/mex -->
      <endpoint address="mex"
                binding="mexHttpBinding"
                contract="IMetadataExchange" />
    </service>
  </services>
  <bindings>
    <basicHttpBinding>
    <!-- This configuration defines the SecurityMode as Message and
         the clientCredentialType as Certificate. -->
      <binding name="Binding1">
        <security mode = "Message">
          <message clientCredentialType="Certificate" />
        </security>
      </binding>
    </basicHttpBinding>
  </bindings>
  <!--For debugging purposes set the includeExceptionDetailInFaults attribute to true-->
  <behaviors>
    <serviceBehaviors>
      <behavior name="CalculatorServiceBehavior">
        <serviceMetadata httpGetEnabled="True" />
        <serviceDebug includeExceptionDetailInFaults="False" />
        <!-- The serviceCredentials behavior allows one to define a service certificate.
             A service certificate is used by a client to authenticate the service and provide message protection.
             This configuration references the "localhost" certificate installed during the setup instructions. -->
        <serviceCredentials>
          <serviceCertificate findValue="localhost"
                              storeLocation="LocalMachine"
                              storeName="My"
                              x509FindType="FindBySubjectName" />
          <clientCertificate>
            <!-- Setting the certificateValidationMode to PeerOrChainTrust means that if the certificate
               is in the user's Trusted People store, then it will be trusted without performing a
               validation of the certificate's issuer chain. This setting is used here for convenience so that the
               sample can be run without having to have certificates issued by a certification authority (CA).
               This setting is less secure than the default, ChainTrust. The security implications of this
               setting should be carefully considered before using PeerOrChainTrust in production code. -->
            <authentication certificateValidationMode="PeerOrChainTrust" />
          </clientCertificate>
        </serviceCredentials>
      </behavior>
    </serviceBehaviors>
  </behaviors>
</system.serviceModel>
```  
  
## <a name="see-also"></a>Zobacz też

- <xref:System.ServiceModel.BasicHttpMessageSecurity>
- <xref:System.ServiceModel.Configuration.BasicHttpSecurityElement.Message%2A>
- <xref:System.ServiceModel.BasicHttpSecurity.Message%2A>
- <xref:System.ServiceModel.Configuration.BasicHttpMessageSecurityElement>
- [Zabezpieczanie usług i klientów](../../../wcf/feature-details/securing-services-and-clients.md)
- [Powiązania](../../../wcf/bindings.md)
- [Konfigurowanie powiązań dostarczanych przez system](../../../wcf/feature-details/configuring-system-provided-bindings.md)
- [Konfigurowanie usług i klientów za pomocą wiązań](../../../wcf/using-bindings-to-configure-services-and-clients.md)
- [\<binding>](bindings.md)
