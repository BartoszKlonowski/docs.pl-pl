---
title: Klasa DiscoveryClient i DynamicEndpoint
ms.date: 03/30/2017
ms.assetid: 7cd418f0-0eab-48d1-a493-7eb907867ec3
ms.openlocfilehash: 72e5beb1306b679cc3b546d77846b5d1e9bb8bb4
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96275014"
---
# <a name="discoveryclient-and-dynamicendpoint"></a>Klasa DiscoveryClient i DynamicEndpoint

<xref:System.ServiceModel.Discovery.DiscoveryClient> i <xref:System.ServiceModel.Discovery.DynamicEndpoint> są dwie klasy używane po stronie klienta do wyszukiwania usług. <xref:System.ServiceModel.Discovery.DiscoveryClient> zapewnia listę usług, które pasują do określonego zestawu kryteriów i umożliwiają łączenie się z usługami. <xref:System.ServiceModel.Discovery.DynamicEndpoint> wykonuje tę samą operację, a ponadto automatycznie nawiązuje połączenie z jedną z znalezionych usług. Każdy punkt końcowy może zostać dodany do <xref:System.ServiceModel.Discovery.DynamicEndpoint> , kryteria wyszukiwania można również dodać w konfiguracji, co <xref:System.ServiceModel.Discovery.DynamicEndpoint> jest przydatne, gdy potrzebujesz odnajdywania w rozwiązaniu, ale nie chcesz modyfikować logiki klienta — wystarczy tylko zmodyfikować punkty końcowe. <xref:System.ServiceModel.Discovery.DiscoveryClient> z drugiej strony można użyć, aby uzyskać dokładniejszą kontrolę nad operacją wyszukiwania. Poniższe korzyści są opisane poniżej.  
  
## <a name="discoveryclient"></a>Obiekt DiscoveryClient  

 <xref:System.ServiceModel.Discovery.DiscoveryClient>Definiuje metody szukania synchronicznego i asynchronicznego <xref:System.ServiceModel.Discovery.DiscoveryClient.FindCompleted> oraz <xref:System.ServiceModel.Discovery.DiscoveryClient.FindProgressChanged> zdarzenia.  Definiuje również synchroniczną i asynchroniczną metodę rozpoznawania oraz <xref:System.ServiceModel.Discovery.DiscoveryClient.ResolveCompleted> zdarzenie. Użyj <xref:System.ServiceModel.Discovery.DiscoveryClient.Find%2A> metod lub, <xref:System.ServiceModel.Discovery.DiscoveryClient.FindAsync%2A> Aby wyszukać usługi. Obie te metody przyjmują <xref:System.ServiceModel.Discovery.FindCriteria> wystąpienie, które pozwala określić nazwy typu kontraktu, zakresy, liczbę żądanych wyników i reguły dopasowywania zakresu. <xref:System.ServiceModel.Discovery.DiscoveryClient.FindCompleted>Zdarzenia i <xref:System.ServiceModel.Discovery.DiscoveryClient.FindProgressChanged> mogą być używane podczas wywoływania <xref:System.ServiceModel.Discovery.DiscoveryClient.FindAsync%2A> metody. <xref:System.ServiceModel.Discovery.DiscoveryClient.FindProgressChanged> jest uruchamiany za każdym razem, gdy <xref:System.ServiceModel.Discovery.DiscoveryClient> odbierze odpowiedź z usługi. Może służyć do wyświetlania paska postępu pokazującego postęp operacji znajdowania. Może również służyć do działania podczas wyszukiwania odpowiedzi po ich odebraniu. <xref:System.ServiceModel.Discovery.DiscoveryClient.FindCompleted>Zdarzenie jest wywoływane po zakończeniu operacji wyszukiwania. Może się tak zdarzyć, ponieważ odebrano maksymalną liczbę odpowiedzi lub jeśli <xref:System.ServiceModel.Discovery.FindCriteria.Duration%2A> upłynął. Po zakończeniu operacji Find wyniki są zwracane w <xref:System.ServiceModel.Discovery.FindResponse> wystąpieniu. <xref:System.ServiceModel.Discovery.FindResponse>Zawiera kolekcję zawierającą <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata> adresy, nazwy typów kontraktów, rozszerzenia, identyfikatory URI nasłuchiwania i zakresy pasujących usług. Możesz następnie użyć tych informacji, aby nawiązać połączenie z jedną z zgodnych usług i wywołać ją. Poniższy przykład pokazuje, jak wywołać metodę System. ServiceModel. Discovery. obiekt DiscoveryClient. Find (System. ServiceModel. Discovery. kryteria znajdowania) i użyć zwróconych metadanych do wywołania znalezionej usługi. Korzyścią z używania <xref:System.ServiceModel.Discovery.DiscoveryClient.Find(System.ServiceModel.Discovery.FindCriteria)> jest to, że można buforować listę znalezionych punktów końcowych i używać ich w późniejszym czasie. Za pomocą tej pamięci podręcznej można utworzyć logikę niestandardową w celu obsługi różnych warunków awarii.  
  
```csharp
DiscoveryClient dc = new DiscoveryClient(new UdpDiscoveryEndpoint());  
  
FindCriteria criteria = new FindCriteria(typeof(ICalculatorService));  
FindResponse fr = dc.Find(criteria);  
  
if (fr.Endpoints.Count > 0)  
{  
   EndpointAddress ep = fr.Endpoints[0].Address;  
   CalculatorServiceClient client = new CalculatorServiceClient();  
  
    // Connect to the discovered service endpoint  
   client.Endpoint.Address = endpointAddress;  
   Console.WriteLine("Invoking CalculatorService at {0}", endpointAddress);  
  
   double value1 = 100.00D;  
   double value2 = 15.99D;  
  
   // Call the Add service operation.  
   double result = client.Add(value1, value2);  
   Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);  
}  
else  
   Console.WriteLine("No matching endpoints found");  
```  
  
 Poniższy przykład pokazuje, jak wykonać operację znajdowania asynchronicznie.  
  
```csharp
static void FindServiceAsync()  
{  
   DiscoveryClient dc = new DiscoveryClient(new UdpDiscoveryEndpoint());
   dc.FindCompleted += new EventHandler<FindCompletedEventArgs>( discoveryClient_FindCompleted);  
   dc.FindProgressChanged += new EventHandler<FindProgressChangedEventArgs>(discoveryClient_FindProgressChanged);  
   dc.FindAsync(new FindCriteria(typeof(ICalculatorService)));
}
static void discoveryClient_FindProgressChanged(object sender, FindProgressChangedEventArgs e)  
{  
   Console.WriteLine("Found service at: " + e.EndpointDiscoveryMetadata.Address  
}
  
static void discoveryClient_FindCompleted(object sender, FindCompletedEventArgs e)  
{
      if (e.Result.Endpoints.Count > 0)  
            {  
                EndpointAddress ep = e.Result.Endpoints[0].Address;  
                CalculatorServiceClient client = new CalculatorServiceClient();  
  
                // Connect to the discovered service endpoint  
                client.Endpoint.Address = ep;  
                Console.WriteLine("Invoking CalculatorService at {0}", ep);  
  
                double value1 = 100.00D;  
                double value2 = 15.99D;  
  
                double result = client.Add(value1, value2);  
                Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);  
            }  
            else  
                Console.WriteLine("No matching endpoints found");  
  
        }  
```
  
 Użyj <xref:System.ServiceModel.Discovery.DiscoveryClient.Resolve%2A> metod i, <xref:System.ServiceModel.Discovery.DiscoveryClient.ResolveAsync%28System.ServiceModel.Discovery.ResolveCriteria%29> Aby zlokalizować usługę na podstawie adresu punktu końcowego. Jest to przydatne, gdy adres punktu końcowego nie jest adresami sieciowymi. Metody rozwiązywania to wystąpienie, z <xref:System.ServiceModel.Discovery.ResolveCriteria> którego można określić adres punktu końcowego rozwiązywanej usługi, maksymalny czas trwania operacji rozpoznawania oraz zestaw rozszerzeń. Poniższy przykład pokazuje, jak używać <xref:System.ServiceModel.Discovery.DiscoveryClient.Resolve%2A> metody do rozwiązywania usługi.  
  
```csharp  
DiscoveryClient dc = new DiscoveryClient(new UdpDiscoveryEndpoint());  
ResolveCriteria criteria = new ResolveCriteria(endpointAddress);  
ResolveResponse response = dc.Resolve(criteria);  
EndpointAddress newEp = response.EndpointDiscoveryMetadata.Address;  
```  
  
## <a name="dynamicendpoint"></a>DynamicEndpoint  

 <xref:System.ServiceModel.Discovery.DynamicEndpoint> jest standardowym punktem końcowym (Aby uzyskać więcej informacji, zobacz [standardowe punkty końcowe](standard-endpoints.md)), które wykonuje odnajdywanie i automatycznie wybiera zgodną usługę. Po prostu Utwórz <xref:System.ServiceModel.Discovery.DynamicEndpoint> przekazywanie kontraktu w celu wyszukania i powiązania, aby użyć i przekazać <xref:System.ServiceModel.Discovery.DynamicEndpoint> wystąpienie do klienta WCF. Poniższy przykład pokazuje, jak utworzyć i użyć wywołania, <xref:System.ServiceModel.Discovery.DynamicEndpoint> Aby wywołać usługę Kalkulator. Odnajdywanie jest wykonywane za każdym razem, gdy klient zostanie otwarty. Każdy punkt końcowy zdefiniowany w konfiguracji może również zostać włączony <xref:System.ServiceModel.Discovery.DynamicEndpoint> przez dodanie `kind ="dynamicEndpoint"` atrybutu do elementu konfiguracji punktu końcowego.  
  
```csharp  
DynamicEndpoint dynamicEndpoint = new DynamicEndpoint(ContractDescription.GetContract(typeof(ICalculatorService)), new WSHttpBinding());  
CalculatorServiceClient client = new CalculatorServiceClient(dynamicEndpoint);  
  
Console.WriteLine("Invoking CalculatorService");  
Console.WriteLine();  
  
double value1 = 100.00D;  
double value2 = 15.99D;  
  
double result = client.Add(value1, value2);  
Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);  
```  
  
## <a name="see-also"></a>Zobacz też

- [Odnajdywanie z zakresami](../samples/discovery-with-scopes-sample.md)
- [Podstawowe](../samples/basic-sample.md)
