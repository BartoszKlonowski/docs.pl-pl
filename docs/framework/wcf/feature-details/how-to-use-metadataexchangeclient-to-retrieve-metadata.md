---
title: 'Instrukcje: używanie elementu MetadataExchangeClient do pobierania metadanych'
ms.date: 03/30/2017
ms.assetid: 0754e9dc-13c5-45c2-81b5-f3da466e5a87
ms.openlocfilehash: 412e695036f29886310099cc5a55b940247b0c72
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96280835"
---
# <a name="how-to-use-metadataexchangeclient-to-retrieve-metadata"></a>Instrukcje: używanie elementu MetadataExchangeClient do pobierania metadanych

Użyj <xref:System.ServiceModel.Description.MetadataExchangeClient> klasy, aby pobrać metadane przy użyciu protokołu WS-MetadataExchange (Mex). Pobrane pliki metadanych są zwracane jako <xref:System.ServiceModel.Description.MetadataSet> obiekt. Zwrócony <xref:System.ServiceModel.Description.MetadataSet> obiekt zawiera kolekcję <xref:System.ServiceModel.Description.MetadataSection> obiektów, z których każdy zawiera określony dialekt metadanych i identyfikator. Można napisać zwrócone metadane do plików lub, jeśli zwrócone metadane zawierają dokumenty Web Services Description Language (WSDL), można zaimportować metadane przy użyciu <xref:System.ServiceModel.Description.WsdlImporter> .  
  
 <xref:System.ServiceModel.Description.MetadataExchangeClient>Konstruktory, które pobierają adres, używają powiązania w <xref:System.ServiceModel.Description.MetadataExchangeBindings> klasie statycznej zgodnej ze schematem Uniform Resource Identifier (URI) adresu. Możesz Alternatywnie użyć <xref:System.ServiceModel.Description.MetadataExchangeClient> konstruktora, który umożliwia jawne określanie powiązania do użycia. Określone powiązanie służy do rozpoznawania wszystkich odwołań do metadanych.  
  
 Podobnie jak każdy inny klient Windows Communication Foundation (WCF), <xref:System.ServiceModel.Description.MetadataExchangeClient> Typ udostępnia Konstruktor do ładowania konfiguracji punktów końcowych klienta przy użyciu nazwy konfiguracji punktu końcowego. Określona konfiguracja punktu końcowego musi określać <xref:System.ServiceModel.Description.IMetadataExchange> kontrakt. Adres w konfiguracji punktu końcowego nie został załadowany, dlatego należy użyć jednego z <xref:System.ServiceModel.Description.MetadataExchangeClient.GetMetadata%2A> przeciążeń, które pobiera adres. Po określeniu adresu metadanych przy użyciu <xref:System.ServiceModel.EndpointAddress> wystąpienia <xref:System.ServiceModel.Description.MetadataExchangeClient> przyjmuje się, że adres wskazuje punkt końcowy MEX. W przypadku określania adresu metadanych jako adresu URL należy również określić, który z nich ma być <xref:System.ServiceModel.Description.MetadataExchangeClientMode> używany, MEX lub HTTP GET.  
  
> [!IMPORTANT]
> Domyślnie program <xref:System.ServiceModel.Description.MetadataExchangeClient> rozwiązuje wszystkie odwołania dla Ciebie, włącznie z importami schematu WSDL i XML. Tę funkcję można wyłączyć, ustawiając <xref:System.ServiceModel.Description.MetadataExchangeClient.ResolveMetadataReferences%2A> Właściwość na `false` . Można kontrolować maksymalną liczbę odwołań do rozpoznawania przy użyciu <xref:System.ServiceModel.Description.MetadataExchangeClient.MaximumResolvedReferences%2A> właściwości. Tej właściwości można użyć w połączeniu z `MaxReceivedMessageSize` właściwością w powiązaniu w celu kontrolowania ilości pobieranych metadanych.  
  
### <a name="to-use-metadataexchangeclient-to-obtain-metadata"></a>Aby używać klasy MetadataExchangeClient do uzyskiwania metadanych  
  
1. Utwórz nowy <xref:System.ServiceModel.Description.MetadataExchangeClient> obiekt przez jawne określenie powiązania, nazwy konfiguracji punktu końcowego lub adresu metadanych.  
  
2. Skonfiguruj odpowiednie <xref:System.ServiceModel.Description.MetadataExchangeClient> wymagania. Na przykład można określić poświadczenia, które będą używane podczas żądania metadanych, kontrolować sposób rozwiązywania odwołań do metadanych i ustawiać <xref:System.ServiceModel.Description.MetadataExchangeClient.OperationTimeout%2A> Właściwość w celu kontrolowania, jak długo żądanie metadanych musi zostać zwrócone przed upływem limitu czasu.  
  
3. Uzyskaj <xref:System.ServiceModel.Description.MetadataSet> obiekt zawierający pobrane metadane, wywołując jedną z <xref:System.ServiceModel.Description.MetadataExchangeClient.GetMetadata%2A> metod. Należy pamiętać, że można użyć tylko <xref:System.ServiceModel.Description.MetadataExchangeClient.GetMetadata%2A> przeciążenia, które nie przyjmuje argumentów, jeśli jawnie określono adres podczas konstruowania <xref:System.ServiceModel.Description.MetadataExchangeClient> .  
  
## <a name="example"></a>Przykład  

 Poniższy przykład kodu pokazuje, jak używać <xref:System.ServiceModel.Description.MetadataExchangeClient> do pobierania i wyliczania plików metadanych.  

 [!code-csharp[MetadataResolver#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/metadataresolver/cs/client.cs#3)]  

## <a name="compiling-the-code"></a>Kompilowanie kodu  

 Aby skompilować ten przykład kodu, należy odwołać się do zestawu System.ServiceModel.dll i zaimportować <xref:System.ServiceModel.Description> przestrzeń nazw.  
  
## <a name="see-also"></a>Zobacz też

- <xref:System.ServiceModel.Description.MetadataResolver>
- <xref:System.ServiceModel.Description.MetadataExchangeClient>
- <xref:System.ServiceModel.Description.WsdlImporter>
