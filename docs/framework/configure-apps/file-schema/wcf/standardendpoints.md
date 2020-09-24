---
title: <standardEndpoints>
ms.date: 03/30/2017
ms.assetid: d62153d7-a6e6-462a-a784-cca61e9c2ba1
ms.openlocfilehash: 5d0607b5c541fc5ae402a50a0f8c464355b6b246
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91157203"
---
# \<standardEndpoints>

Ta sekcja konfiguracji umożliwia zdefiniowanie kolekcji standardowych punktów końcowych, które są wstępnie skonfigurowanymi punktami końcowymi wielokrotnego użytku. Standardowy punkt końcowy będzie miał co najmniej jeden atrybut Address, Binding i Contract ustawiony na wartość stałą. Na przykład w punkcie końcowym odnajdywania kontrakt jest ustalony. Możesz również użyć standardowych punktów końcowych, aby zwiększyć punkt końcowy usługi z nowymi właściwościami podobnymi do definiowania powiązań niestandardowych.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<standardEndpoints>**  
  
## <a name="syntax"></a>Składnia  
  
```xml  
<system.serviceModel>
  <standardEndpoints>
  </standardEndpoints>
</system.serviceModel>
```  
  
## <a name="attributes-and-elements"></a>Atrybuty i elementy  

 W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.  
  
### <a name="attributes"></a>Atrybuty  

 Brak.  
  
### <a name="child-elements"></a>Elementy podrzędne  
  
|Element|Opis|  
|-------------|-----------------|  
|[\<announcementEndpoint>](announcementendpoint.md)|Definiuje standardowy punkt końcowy ze stałym kontraktem anonsu. Usługa może opcjonalnie ogłaszać swoją dostępność, wysyłając wiadomość w trybie online i w trybie offline, gdy zostanie ona otwarta lub ZAMKNIĘTA odpowiednio. Usługa Windows Communication Foundation (WCF) określa punkty końcowe anonsu w [\<serviceDiscovery>](servicediscovery.md) elemencie i używa AnnouncementClient do wykonywania anonsów. Klient, który chce nasłuchiwać anonsu z innej usługi, działa jako usługa WCF. w tym celu należy skonfigurować punkty końcowe anonsu dla tego klienta w [\<services>](services.md) sekcji.|  
|[\<discoveryEndpoint>](discoveryendpoint.md)|Definiuje standardowy punkt końcowy ze stałym kontraktem odnajdowania. Po dodaniu do konfiguracji usługi określa miejsce nasłuchiwania komunikatów odnajdowania. Po dodaniu do konfiguracji klienta określa, gdzie mają być wysyłane zapytania odnajdywania.|  
|[\<dynamicEndpoint>](dynamicendpoint.md)|Ten element konfiguracji definiuje standardowy punkt końcowy, który zawiera informacje umożliwiające aplikacji działanie jako program kliencki, który może znaleźć adres punktu końcowego dynamicznie w czasie wykonywania.|  
|[\<mexEndpoint>](mexendpoint.md)|Definiuje standardowy punkt końcowy ze stałym kontraktem kontraktem IMetadataExchange. Ponieważ wszystkie punkty końcowe wymiany metadanych określają kontraktem IMetadataExchange jako kontrakt, można użyć tego standardowego punktu zamiast definiować go dla siebie.|  
|[\<udpAnnouncementEndpoint>](udpannouncementendpoint.md)|Definiuje standardowy punkt końcowy, który jest używany przez usługi do wysyłania komunikatów anonsu za pośrednictwem powiązania UDP. Ma ona ustaloną umowę i obsługuje dwie wersje odnajdywania. Oprócz tego ma stałe powiązanie UDP i domyślną wartość adresu określoną w specyfikacjach WS-Discovery (WS-Discovery Kwiecień 2005 lub WS-Discovery w wersji 1,1). Można określić adres multiemisji, który będzie używany do wysyłania i otrzymywania komunikatów anonsu.|  
|[\<udpDiscoveryEndpoint>](udpdiscoveryendpoint.md)|Definiuje standardowy punkt końcowy, który jest wstępnie skonfigurowany dla operacji odnajdywania za pośrednictwem powiązania multiemisji UDP. Ten punkt końcowy ma stały kontrakt i obsługuje dwie wersje protokołu WS-Discovery. Ponadto ma stałe powiązanie UDP i domyślny adres określony w specyfikacjach WS-Discovery (WS-Discovery Kwiecień 2005 lub WS-Discovery V 1.1).|  
|[\<webHttpEndpoint>](webhttpendpoint.md)|Definiuje standardowy punkt końcowy ze stałym [\<webHttpBinding>](webhttpbinding.md) powiązaniem, które automatycznie dodaje [\<webHttp>](webhttp.md) zachowanie. Użyj tego punktu końcowego podczas pisania usługi REST.|  
|[\<webScriptEndpoint>](webscriptendpoint.md)|Definiuje standardowy punkt końcowy ze stałym [\<webHttpBinding>](webhttpbinding.md) powiązaniem, które automatycznie dodaje [\<enableWebScript>](enablewebscript.md) zachowanie. Użyj tego punktu końcowego podczas pisania usługi, która jest wywoływana z aplikacji ASP.NET AJAX.|  
|[\<workflowControlEndpoint>](workflowcontrolendpoint.md)|Definiuje standardowy punkt końcowy do kontroli wykonania wystąpień przepływu pracy (tworzenie, uruchamianie, wstrzymywanie, przerywanie itp.).|  
  
### <a name="parent-elements"></a>Elementy nadrzędne  
  
|Element|Opis|  
|-------------|-----------------|  
|\<system.ServiceModel>|Element główny wszystkich elementów konfiguracji WCF.|  
  
## <a name="see-also"></a>Zobacz też

- [Standardowe punkty końcowe](../../../wcf/feature-details/standard-endpoints.md)
