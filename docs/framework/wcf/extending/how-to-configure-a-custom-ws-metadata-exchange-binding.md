---
title: 'Instrukcje: Konfigurowanie niestandardowego wiązania WS-Metadata Exchange'
ms.date: 03/30/2017
helpviewer_keywords:
- WS-Metadata Exchange [WCF]
- WS-Metadata Exchange [WCF], configuring a custom binding
ms.assetid: cdba4d73-da64-4805-bc56-9822becfd1e4
ms.openlocfilehash: 6459e3f0cf0ab72af8027bd6802a0e7aa574aece
ms.sourcegitcommit: 1c1a1f9ec0bd1efb3040d86a79f7ee94e207cca5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/03/2020
ms.locfileid: "80635781"
---
# <a name="how-to-configure-a-custom-ws-metadata-exchange-binding"></a>Instrukcje: Konfigurowanie niestandardowego wiązania WS-Metadata Exchange

W tym artykule wyjaśniono, jak skonfigurować niestandardowe powiązanie wymiany metadanych usługi WS. Windows Communication Foundation (WCF) zawiera cztery powiązania metadanych zdefiniowane przez system, ale można publikować metadane przy użyciu dowolnego powiązania, które chcesz. W tym artykule pokazano, jak `wsHttpBinding`publikować metadane przy użyciu pliku . To powiązanie umożliwia udostępnianie metadanych w bezpieczny sposób. Kod w tym artykule jest oparty na [wprowadzenie](../samples/getting-started-sample.md).  
  
### <a name="using-a-configuration-file"></a>Korzystanie z pliku konfiguracyjnego  
  
1. W pliku konfiguracyjnym usługi dodaj zachowanie `serviceMetadata` usługi zawierające znacznik:  
  
    ```xml  
    <behaviors>  
       <serviceBehaviors>  
         <behavior name="CalculatorServiceBehavior">  
           <serviceMetadata httpGetEnabled="True"/>  
         </behavior>  
       </serviceBehaviors>  
    </behaviors>  
    ```  
  
2. Dodaj `behaviorConfiguration` atrybut do tagu usługi, który odwołuje się do tego nowego zachowania:  
  
    ```xml  
    <service name="Microsoft.ServiceModel.Samples.CalculatorService"  
    behaviorConfiguration="CalculatorServiceBehavior" />
    ```  
  
3. Dodaj punkt końcowy metadanych określając mex `wsHttpBinding` jako adres, <xref:System.ServiceModel.Description.IMetadataExchange> jako powiązanie i jako kontrakt:  
  
    ```xml  
    <endpoint address="mex"  
              binding="wsHttpBinding"  
              contract="IMetadataExchange" />  
    ```  
  
4. Aby sprawdzić, czy punkt końcowy wymiany metadanych działa poprawnie, dodaj znacznik punktu końcowego w pliku konfiguracji klienta:  
  
    ```xml  
    <endpoint name="MyMexEndpoint"               address="http://localhost:8000/servicemodelsamples/service/mex"  
              binding="wsHttpBinding"  
              contract="IMetadataExchange"/>  
    ```  
  
5. W metodzie Main() klienta utwórz <xref:System.ServiceModel.Description.MetadataExchangeClient> nowe wystąpienie, ustaw jego <xref:System.ServiceModel.Description.MetadataExchangeClient.ResolveMetadataReferences%2A> właściwość na , wywołaj, `true` <xref:System.ServiceModel.Description.MetadataExchangeClient.GetMetadata%2A> a następnie iteruj za pomocą kolekcji zwróconych metadanych:  
  
    ```csharp
    string mexAddress = "http://localhost:8000/servicemodelsamples/service/mex";  
  
    MetadataExchangeClient mexClient = new MetadataExchangeClient("MyMexEndpoint");  
    mexClient.ResolveMetadataReferences = true;  
    MetadataSet mdSet = mexClient.GetMetadata(new EndpointAddress(mexAddress));  
    foreach (MetadataSection section in mdSet.MetadataSections)  
    Console.WriteLine("Metadata section: " + section.Dialect.ToString());  
    ```  
  
### <a name="configuring-by-code"></a>Konfigurowanie według kodu  
  
1. Tworzenie <xref:System.ServiceModel.WSHttpBinding> wystąpienia wiązania:  
  
    ```csharp  
    WSHttpBinding binding = new WSHttpBinding();  
    ```  
  
2. Tworzenie <xref:System.ServiceModel.ServiceHost> wystąpienia:  
  
    ```csharp  
    ServiceHost serviceHost = new ServiceHost(typeof(CalculatorService), baseAddress);  
    ```  
  
3. Dodaj punkt końcowy usługi <xref:System.ServiceModel.Description.ServiceMetadataBehavior> i dodaj wystąpienie:  
  
    ```csharp  
    serviceHost.AddServiceEndpoint(typeof(ICalculator), binding, baseAddress);  
    ServiceMetadataBehavior smb = new ServiceMetadataBehavior();  
    smb.HttpGetEnabled = true;  
    serviceHost.Description.Behaviors.Add(smb);  
    ```  
  
4. Dodaj punkt końcowy wymiany metadanych, określając <xref:System.ServiceModel.WSHttpBinding> utworzony wcześniej:  
  
    ```csharp  
    serviceHost.AddServiceEndpoint(typeof(IMetadataExchange), binding, mexAddress);  
    ```  
  
5. Aby sprawdzić, czy punkt końcowy wymiany metadanych działa poprawnie, dodaj znacznik punktu końcowego w pliku konfiguracji klienta:  
  
    ```xml  
    <endpoint name="MyMexEndpoint"               address="http://localhost:8000/servicemodelsamples/service/mex"  
              binding="wsHttpBinding"  
              contract="IMetadataExchange"/>  
    ```  
  
6. W metodzie Main() klienta utwórz <xref:System.ServiceModel.Description.MetadataExchangeClient> nowe wystąpienie, ustaw <xref:System.ServiceModel.Description.MetadataExchangeClient.ResolveMetadataReferences%2A> właściwość na , wywołaj, `true` <xref:System.ServiceModel.Description.MetadataExchangeClient.GetMetadata%2A> a następnie iteruj za pomocą kolekcji zwróconych metadanych:  
  
    ```csharp  
    string mexAddress = "http://localhost:8000/servicemodelsamples/service/mex";  
  
    MetadataExchangeClient mexClient = new MetadataExchangeClient("MyMexEndpoint");  
    mexClient.ResolveMetadataReferences = true;  
    MetadataSet mdSet = mexClient.GetMetadata(new EndpointAddress(mexAddress));  
    foreach (MetadataSection section in mdSet.MetadataSections)  
    Console.WriteLine("Metadata section: " + section.Dialect.ToString());  
    ```  
  
## <a name="see-also"></a>Zobacz też

- [Zachowanie publikowania metadanych](../samples/metadata-publishing-behavior.md)
- [Pobieranie metadanych](../samples/retrieve-metadata.md)
- [Metadane](../feature-details/metadata.md)
- [Publikowanie metadanych](../feature-details/publishing-metadata.md)
- [Publikowanie punktów końcowych metadanych](../publishing-metadata-endpoints.md)
