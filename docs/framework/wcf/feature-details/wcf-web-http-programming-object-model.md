---
title: Model obiektowy programowania protokołu HTTP sieci Web w programie WCF
ms.date: 03/30/2017
ms.assetid: ed96b5fc-ca2c-4b0d-bdba-d06b77c3cb2a
ms.openlocfilehash: 4cd23ccb1956a73e36d5c7d3e444c347247e338d
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96266886"
---
# <a name="wcf-web-http-programming-object-model"></a>Model obiektowy programowania protokołu HTTP sieci Web w programie WCF

Model programowania HTTP sieci WEB w programie WCF umożliwia deweloperom udostępnianie usług sieci Web Windows Communication Foundation (WCF) za pośrednictwem podstawowych żądań HTTP bez konieczności stosowania protokołu SOAP. Model programowania HTTP sieci WEB w programie WCF jest oparty na istniejącym modelu rozszerzalności WCF. Definiuje następujące klasy:  
  
 **Model programowania:**  
  
- <xref:System.ServiceModel.Web.AspNetCacheProfileAttribute>  
  
- <xref:System.ServiceModel.Web.WebGetAttribute>  
  
- <xref:System.ServiceModel.Web.WebInvokeAttribute>  
  
- <xref:System.ServiceModel.Web.WebServiceHost>  
  
 **Infrastruktura kanałów i dyspozytorów:**  
  
- <xref:System.ServiceModel.WebHttpBinding>  
  
- <xref:System.ServiceModel.Description.WebHttpBehavior>  
  
 **Klasy narzędzi i punkty rozszerzalności:**  
  
- <xref:System.UriTemplate>  
  
- <xref:System.UriTemplateTable>  
  
- <xref:System.ServiceModel.Dispatcher.QueryStringConverter>  
  
- <xref:System.ServiceModel.Dispatcher.WebHttpDispatchOperationSelector>  
  
## <a name="aspnetcacheprofileattribute"></a>AspNetCacheProfileAttribute  

 W <xref:System.ServiceModel.Web.AspNetCacheProfileAttribute> przypadku zastosowania do operacji usługi program wskazuje w pliku konfiguracji wyjściowy profil pamięci podręcznej ASP.NET, który powinien być używany przez program do buforowania odpowiedzi z operacji w wyjściowej pamięci podręcznej ASP .NET. Ta właściwość przyjmuje tylko jeden parametr, nazwa profilu pamięci podręcznej, która określa ustawienia pamięci podręcznej w pliku konfiguracji.  
  
## <a name="webgetattribute"></a>Obiektu  

 Ten <xref:System.ServiceModel.Web.WebGetAttribute> atrybut służy do oznaczania operacji usługi, która odpowiada na żądania HTTP GET. Jest to zachowanie operacji pasywnej ( <xref:System.ServiceModel.Description.IOperationBehavior> metody nic nie rób), które dodaje metadane do opisu operacji. Zastosowanie nie <xref:System.ServiceModel.Web.WebGetAttribute> ma żadnego efektu, chyba że zachowanie, które szuka tych metadanych w opisie operacji (w tym celu <xref:System.ServiceModel.Description.WebHttpBehavior> ) jest dodawane do kolekcji zachowań usługi. Ten <xref:System.ServiceModel.Web.WebGetAttribute> atrybut przyjmuje parametry opcjonalne pokazane w poniższej tabeli.  
  
|Parametr|Opis|  
|---------------|-----------------|  
|`BodyStyle`|Określa, czy należy zawijać żądania i odpowiedzi wysyłane do i odbierane z operacji usługi, do której ma zastosowanie atrybut.|  
|`RequestFormat`|Kontroluje sposób formatowania komunikatów żądania.|  
|`ResponseFormat`|Kontroluje sposób formatowania komunikatów odpowiedzi.|  
|`UriTemplate`|Określa szablon identyfikatora URI, który kontroluje, jakie żądania HTTP są mapowane do operacji usługi, do której jest stosowany atrybut.|  
  
## <a name="webhttpbinding"></a>WebHttpBinding  

 <xref:System.ServiceModel.WebHttpBinding>Klasa obejmuje obsługę danych XML, JSON i nieprzetworzone dane binarne przy użyciu <xref:System.ServiceModel.Channels.WebMessageEncodingBindingElement> . Składa się z <xref:System.ServiceModel.Channels.HttpsTransportBindingElement> , <xref:System.ServiceModel.Channels.HttpTransportBindingElement> i <xref:System.ServiceModel.WebHttpSecurity> obiektu. <xref:System.ServiceModel.WebHttpBinding>Program jest przeznaczony do użycia w połączeniu z <xref:System.ServiceModel.Description.WebHttpBehavior> .  
  
## <a name="webinvokeattribute"></a>WebInvokeAttribute  

 Ten <xref:System.ServiceModel.Web.WebInvokeAttribute> atrybut jest podobny do <xref:System.ServiceModel.Web.WebGetAttribute> , ale jest używany do oznaczania operacji usługi, która odpowiada na żądania HTTP inne niż get. Jest to zachowanie operacji pasywnej ( <xref:System.ServiceModel.Description.IOperationBehavior> metody nic nie rób), które dodaje metadane do opisu operacji. Zastosowanie nie <xref:System.ServiceModel.Web.WebInvokeAttribute> ma żadnego efektu, chyba że zachowanie, które szuka tych metadanych w opisie operacji (w tym celu <xref:System.ServiceModel.Description.WebHttpBehavior> ) jest dodawane do kolekcji zachowań usługi.  
  
 Ten <xref:System.ServiceModel.Web.WebInvokeAttribute> atrybut przyjmuje parametry opcjonalne pokazane w poniższej tabeli.  
  
|Parametr|Opis|  
|---------------|-----------------|  
|`BodyStyle`|Określa, czy należy zawijać żądania i odpowiedzi wysyłane do i odbierane z operacji usługi, do której ma zastosowanie atrybut.|  
|`Method`|Określa metodę HTTP, do której jest zamapowana operacja usługi.|  
|`RequestFormat`|Kontroluje sposób formatowania komunikatów żądania.|  
|`ResponseFormat`|Kontroluje sposób formatowania komunikatów odpowiedzi.|  
|`UriTemplate`|Określa szablon identyfikatora URI, który kontroluje, jakie żądania GET są mapowane do operacji usługi, do której jest stosowany atrybut.|  
  
## <a name="uritemplate"></a>UriTemplate  

 <xref:System.UriTemplate>Klasa umożliwia zdefiniowanie zestawu podobnych identyfikatorów URI. Szablony składają się z dwóch części, ścieżki i zapytania. Ścieżka składa się z serii segmentów rozdzielonych ukośnikiem (/). Każdy segment może mieć wartość literału, wartość zmiennej (zapisaną w nawiasach klamrowych [{}], ograniczona do zawartości dokładnie jednego segmentu) lub symbol wieloznaczny (zapisany jako gwiazdka [ \* ], który pasuje do "reszty ścieżki"), który musi występować na końcu ścieżki. Wyrażenie zapytania można całkowicie pominąć. Jeśli jest obecny, określa nieuporządkowaną serię par nazwa/wartość. Elementy wyrażenia zapytania mogą być parami literałów (? x = 2) lub par zmiennych (? x = {*Value*}). Niesparowane wartości są niedozwolone. <xref:System.UriTemplate> jest używany wewnętrznie przez model programowania HTTP sieci WEB w programie WCF do mapowania określonych identyfikatorów URI lub grup identyfikatorów URI na operacje usługi.  
  
## <a name="uritemplatetable"></a>UriTemplateTable  

 <xref:System.UriTemplateTable>Klasa reprezentuje zestaw asocjacyjny <xref:System.UriTemplate> obiektów powiązanych z obiektem wyboru dewelopera. Pozwala dopasować identyfikatory URI (Uniform Resource Identifier) kandydatów do szablonów w zestawie i pobrać dane skojarzone z pasującymi szablonami. <xref:System.UriTemplateTable> jest używany wewnętrznie przez model programowania HTTP sieci WEB w programie WCF do mapowania określonych identyfikatorów URI lub grup identyfikatorów URI na operacje usługi.  
  
## <a name="webservicehost"></a>WebServiceHost  

 <xref:System.ServiceModel.Web.WebServiceHost> rozszerza, <xref:System.ServiceModel.ServiceHost> Aby ułatwić Hostowanie usługi w stylu sieci Web bez protokołu SOAP. Jeśli <xref:System.ServiceModel.Web.WebServiceHost> w opisie usługi nie znaleziono żadnych punktów końcowych, program automatycznie utworzy domyślny punkt końcowy na adresie podstawowym usługi. Podczas tworzenia domyślnego punktu końcowego HTTP program <xref:System.ServiceModel.Web.WebServiceHost> wyłącza również stronę pomocy http i funkcję pobierania Web Services Description Language (WSDL), dzięki czemu punkt końcowy metadanych nie zakłóca domyślnego punktu końcowego http. <xref:System.ServiceModel.Web.WebServiceHost> zapewnia również, że wszystkie punkty końcowe, które używają, <xref:System.ServiceModel.WebHttpBinding> mają wymagany <xref:System.ServiceModel.Description.WebHttpBehavior> dołączony. Na koniec program <xref:System.ServiceModel.Web.WebServiceHost> automatycznie konfiguruje powiązanie punktu końcowego, aby działał przy użyciu skojarzonych ustawień zabezpieczeń Internet Information Services (IIS), gdy są używane w bezpiecznym katalogu wirtualnym.  
  
## <a name="webservicehostfactory"></a>WebServiceHostFactory  

 <xref:System.ServiceModel.Activation.WebServiceHostFactory>Klasa jest używana do dynamicznego tworzenia, <xref:System.ServiceModel.Web.WebServiceHost> gdy usługa jest hostowana w Internet Information Services (IIS) lub usługa aktywacji procesów systemu Windows (was). W przeciwieństwie do usługi samodzielnej, w której aplikacja hostingu tworzy wystąpienia <xref:System.ServiceModel.Web.WebServiceHost> , usługi hostowane w usługach IIS lub używała tej klasy do utworzenia <xref:System.ServiceModel.Web.WebServiceHost> dla usługi. <xref:System.ServiceModel.Activation.WebServiceHostFactory.CreateServiceHost%28System.Type%2CSystem.Uri%5B%5D%29>Metoda jest wywoływana w przypadku otrzymania żądania przychodzącego dla usługi.  
  
## <a name="webhttpbehavior"></a>WebHttpBehavior  

 <xref:System.ServiceModel.Description.WebHttpBehavior>Klasa dostarcza niezbędne elementy formatujące, selektory operacji i tak dalej, które są wymagane do obsługi usługi w stylu sieci Web w warstwie modelu usług. Jest to implementowane jako zachowanie punktu końcowego (używane w połączeniu z <xref:System.ServiceModel.WebHttpBinding> ) i pozwala na określenie programów formatującego i selektorów operacji dla każdego punktu końcowego, co umożliwia tej samej implementacji usługi Uwidacznianie punktów końcowych protokołu SOAP i POX.  
  
### <a name="extending-webhttpbehavior"></a>Rozszerzanie WebHttpBehavior  

 <xref:System.ServiceModel.Description.WebHttpBehavior> jest rozszerzalny przy użyciu wielu metod wirtualnych: <xref:System.ServiceModel.Description.WebHttpBehavior.GetOperationSelector%28System.ServiceModel.Description.ServiceEndpoint%29> , <xref:System.ServiceModel.Description.WebHttpBehavior.GetReplyClientFormatter%28System.ServiceModel.Description.OperationDescription%2CSystem.ServiceModel.Description.ServiceEndpoint%29> ,, <xref:System.ServiceModel.Description.WebHttpBehavior.GetRequestClientFormatter%28System.ServiceModel.Description.OperationDescription%2CSystem.ServiceModel.Description.ServiceEndpoint%29> <xref:System.ServiceModel.Description.WebHttpBehavior.GetReplyDispatchFormatter%28System.ServiceModel.Description.OperationDescription%2CSystem.ServiceModel.Description.ServiceEndpoint%29> i <xref:System.ServiceModel.Description.WebHttpBehavior.GetRequestDispatchFormatter%28System.ServiceModel.Description.OperationDescription%2CSystem.ServiceModel.Description.ServiceEndpoint%29> . Deweloperzy mogą dziedziczyć klasy z <xref:System.ServiceModel.Description.WebHttpBehavior> i przesłonić te metody, aby dostosować zachowanie domyślne.  
  
 <xref:System.ServiceModel.Description.WebScriptEnablingBehavior>Jest to przykład rozszerzania <xref:System.ServiceModel.Description.WebHttpBehavior> . <xref:System.ServiceModel.Description.WebScriptEnablingBehavior> umożliwia punktom końcowym Windows Communication Foundation (WCF) odbieranie żądań HTTP z klienta ASP.NET AJAX opartego na przeglądarce. Przykładem użycia tego punktu rozszerzalności jest [Usługa AJAX korzystająca z protokołu HTTP Post](../samples/ajax-service-using-http-post.md) .  
  
> [!WARNING]
> W przypadku korzystania z <xref:System.ServiceModel.Description.WebScriptEnablingBehavior> , <xref:System.UriTemplate> nie są obsługiwane w <xref:System.ServiceModel.Web.WebGetAttribute> ani <xref:System.ServiceModel.Web.WebInvokeAttribute> atrybuty.  
  
## <a name="webhttpdispatchoperationselector"></a>WebHttpDispatchOperationSelector  

 <xref:System.ServiceModel.Dispatcher.WebHttpDispatchOperationSelector>Klasa używa <xref:System.UriTemplate> klas i <xref:System.UriTemplateTable> do wysyłania wywołań do operacji usługi.  
  
## <a name="compatibility"></a>Zgodność  

 Model programowania HTTP sieci WEB w programie WCF nie korzysta z komunikatów opartych na protokole SOAP, dlatego nie obsługuje protokołów WS-*. Można jednak uwidocznić ten sam kontrakt przez dwa różne punkty końcowe: jeden przy użyciu protokołu SOAP, a drugi nie używa protokołu SOAP. Zapoznaj się z tematem [jak to zrobić: uwidocznienie kontraktu dla klientów protokołu SOAP i sieci Web](how-to-expose-a-contract-to-soap-and-web-clients.md) na przykład.  
  
## <a name="security"></a>Zabezpieczenia  

Ponieważ model programowania HTTP sieci WEB w programie WCF nie obsługuje protokołów WS-*, jedynym sposobem zabezpieczenia usługi sieci Web opartej na modelu programowania HTTP sieci WEB w programie WCF jest udostępnienie usługi przy użyciu protokołu SSL. Aby uzyskać więcej informacji na temat konfigurowania protokołu SSL w usługach IIS 7,0, zobacz [jak zaimplementować protokół SSL w usługach IIS](https://support.microsoft.com/help/299875/how-to-implement-ssl-in-iis).
  
## <a name="see-also"></a>Zobacz też

- <xref:System.ServiceModel.WebHttpBinding>
- <xref:System.ServiceModel.Web.WebGetAttribute>
- <xref:System.ServiceModel.Web.WebInvokeAttribute>
- <xref:System.ServiceModel.Description.WebHttpBehavior>
- <xref:System.ServiceModel.Dispatcher.WebHttpDispatchOperationSelector>
- [Omówienie modelu programowania usług HTTP w sieci Web przy użyciu programu WCF](wcf-web-http-programming-model-overview.md)
