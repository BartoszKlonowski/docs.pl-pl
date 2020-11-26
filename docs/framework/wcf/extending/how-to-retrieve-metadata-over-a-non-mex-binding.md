---
title: 'Instrukcje: pobieranie metadanych przez wiązanie inne niż wymiany metadanych'
ms.date: 03/30/2017
ms.assetid: 2292e124-81b2-4317-b881-ce9c1ec66ecb
ms.openlocfilehash: db4bad81241295e168685c8b80546f2305021066
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96249023"
---
# <a name="how-to-retrieve-metadata-over-a-non-mex-binding"></a>Instrukcje: pobieranie metadanych przez wiązanie inne niż wymiany metadanych

W tym temacie opisano sposób pobierania metadanych z punktu końcowego MEX względem powiązania niezwiązanego z MEX. Kod w tym przykładzie jest oparty na przykładowej [niestandardowej bezpiecznego punktu końcowego metadanych](../samples/custom-secure-metadata-endpoint.md) .  
  
### <a name="to-retrieve-metadata-over-a-non-mex-binding"></a>Aby pobrać metadane przez powiązanie inne niż MEX  
  
1. Określ powiązanie używane przez punkt końcowy MEX. W przypadku usług Windows Communication Foundation (WCF) można określić powiązanie MEX, uzyskując dostęp do pliku konfiguracji usługi. W takim przypadku powiązanie MEX jest zdefiniowane w następującej konfiguracji usługi.  
  
    ```xml  
    <services>  
        <service name="Microsoft.ServiceModel.Samples.CalculatorService"  
                behaviorConfiguration="CalculatorServiceBehavior">  
         <!-- Use the base address provided by the host. -->  
         <endpoint address=""  
           binding="wsHttpBinding"  
           bindingConfiguration="Binding2"  
           contract="Microsoft.ServiceModel.Samples.ICalculator" />  
         <endpoint address="mex"  
           binding="wsHttpBinding"  
           bindingConfiguration="Binding1"  
           contract="IMetadataExchange" />  
         </service>  
     </services>  
     <bindings>  
       <wsHttpBinding>  
         <binding name="Binding1">  
           <security mode="Message">  
             <message clientCredentialType="Certificate" />  
           </security>  
         </binding>  
         <binding name="Binding2">  
           <reliableSession inactivityTimeout="00:01:00" enabled="true" />  
           <security mode="Message">  
             <message clientCredentialType="Certificate" />  
           </security>  
         </binding>  
       </wsHttpBinding>  
     </bindings>  
    ```  
  
2. W pliku konfiguracji klienta skonfiguruj to samo powiązanie niestandardowe. W tym miejscu Klient definiuje również `clientCredentials` zachowanie, aby zapewnić certyfikat używany do uwierzytelniania w usłudze podczas żądania metadanych z punktu końcowego MEX. Podczas używania Svcutil.exe do żądania metadanych za pośrednictwem niestandardowego powiązania należy dodać konfigurację punktu końcowego MEX do pliku konfiguracji dla Svcutil.exe (Svcutil.exe.config), a nazwa konfiguracji punktu końcowego powinna być zgodna ze schematem identyfikatora URI adresu punktu końcowego MEX, jak pokazano w poniższym kodzie.  
  
    ```xml  
    <system.serviceModel>  
      <client>  
        <endpoint name="http"  
                  binding="wsHttpBinding"  
                  bindingConfiguration="Binding1"  
                  behaviorConfiguration="ClientCertificateBehavior"  
                  contract="IMetadataExchange" />  
      </client>  
      <bindings>  
        <wsHttpBinding>  
          <binding name="Binding1">  
            <security mode="Message">  
              <message clientCredentialType="Certificate"/>  
            </security>  
          </binding>  
        </wsHttpBinding>  
      </bindings>  
      <behaviors>  
        <endpointBehaviors>  
          <behavior name="ClientCertificateBehavior">  
            <clientCredentials>  
              <clientCertificate findValue="client.com" storeLocation="CurrentUser" storeName="My" x509FindType="FindBySubjectName" />  
              <serviceCertificate>  
                <authentication certificateValidationMode="PeerOrChainTrust" />  
              </serviceCertificate>  
            </clientCredentials>  
          </behavior>  
        </endpointBehaviors>  
      </behaviors>
    </system.serviceModel>  
    ```  
  
3. Utwórz `MetadataExchangeClient` wywołanie i `GetMetadata` . Istnieją dwa sposoby, aby to zrobić: można określić niestandardowe powiązanie w konfiguracji lub można określić niestandardowe powiązanie w kodzie, jak pokazano w poniższym przykładzie.  
  
    ```csharp
    // The custom binding is specified in configuration.  
    EndpointAddress mexAddress = new EndpointAddress("http://localhost:8000/ServiceModelSamples/Service/mex");  
  
    MetadataExchangeClient mexClient = new MetadataExchangeClient("http");  
    mexClient.ResolveMetadataReferences = true;  
    MetadataSet mexSet = mexClient.GetMetadata(mexAddress);  
  
    // The custom binding is specified in code.  
    // Specify the Metadata Exchange binding and its security mode.  
    WSHttpBinding mexBinding = new WSHttpBinding(SecurityMode.Message);  
    mexBinding.Security.Message.ClientCredentialType = MessageCredentialType.Certificate;  
  
    // Create a MetadataExchangeClient and set the certificate details.  
    MetadataExchangeClient mexClient = new MetadataExchangeClient(mexBinding);  
    mexClient.SoapCredentials.ClientCertificate.SetCertificate(  
        StoreLocation.CurrentUser, StoreName.My,  
        X509FindType.FindBySubjectName, "client.com");  
    mexClient.SoapCredentials.ServiceCertificate.Authentication.  
        CertificateValidationMode =  
        X509CertificateValidationMode.PeerOrChainTrust;  
    mexClient.SoapCredentials.ServiceCertificate.SetDefaultCertificate(  
        StoreLocation.CurrentUser, StoreName.TrustedPeople,  
        X509FindType.FindBySubjectName, "localhost");  
    MetadataExchangeClient mexClient2 = new MetadataExchangeClient(customBinding);  
    mexClient2.ResolveMetadataReferences = true;  
    MetadataSet mexSet2 = mexClient2.GetMetadata(mexAddress);  
    ```  
  
4. Utwórz `WsdlImporter` wywołanie i `ImportAllEndpoints` , jak pokazano w poniższym kodzie.  
  
    ```csharp
    WsdlImporter importer = new WsdlImporter(mexSet);  
    ServiceEndpointCollection endpoints = importer.ImportAllEndpoints();  
    ```  
  
5. W tym momencie masz kolekcję punktów końcowych usługi. Aby uzyskać więcej informacji na temat importowania metadanych, zobacz [How to: import Metadata into do punktów końcowych usługi](../feature-details/how-to-import-metadata-into-service-endpoints.md).  
  
## <a name="see-also"></a>Zobacz też

- [Metadane](../feature-details/metadata.md)
