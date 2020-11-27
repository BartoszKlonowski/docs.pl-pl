---
title: Niestandardowy host usługi
ms.date: 03/30/2017
ms.assetid: fe16ff50-7156-4499-9c32-13d8a79dc100
ms.openlocfilehash: 56846f4021b2a0be1801decedb02c4c637847d07
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96275596"
---
# <a name="custom-service-host"></a>Niestandardowy host usługi

Ten przykład pokazuje, jak używać niestandardowych pochodnych <xref:System.ServiceModel.ServiceHost> klasy w celu zmiany zachowania usługi w czasie wykonywania. Takie podejście umożliwia użycie alternatywnej alternatywy do konfigurowania dużej liczby usług w typowy sposób. W przykładzie pokazano również, jak użyć <xref:System.ServiceModel.Activation.ServiceHostFactory> klasy do użycia niestandardowego ServiceHost w środowisku usług Internet Information Services (IIS) lub Windows Process Activation Service (was).  
  
> [!IMPORTANT]
> Przykłady mogą być już zainstalowane na komputerze. Przed kontynuowaniem Wyszukaj następujący katalog (domyślny).  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> Jeśli ten katalog nie istnieje, przejdź do [przykładów Windows Communication Foundation (WCF) i Windows Workflow Foundation (WF) dla .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) , aby pobrać wszystkie Windows Communication Foundation (WCF) i [!INCLUDE[wf1](../../../../includes/wf1-md.md)] przykłady. Ten przykład znajduje się w następującym katalogu.  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Hosting\CustomServiceHost`  
  
## <a name="about-the-scenario"></a>Informacje o tym scenariuszu

 Aby zapobiec przypadkowemu ujawnieniu potencjalnie poufnych metadanych usługi, konfiguracja domyślna dla usług Windows Communication Foundation (WCF) wyłącza Publikowanie metadanych. To zachowanie jest zabezpieczone domyślnie, ale oznacza to, że nie można użyć narzędzia do importowania metadanych (takiego jak Svcutil.exe) do wygenerowania kodu klienta wymaganego do wywołania usługi, chyba że zachowanie publikowania metadanych usługi jest jawnie włączone w konfiguracji.  
  
 Włączenie publikowania metadanych dla dużej liczby usług obejmuje dodanie tych samych elementów konfiguracji do poszczególnych usług, co skutkuje znaczną ilością informacji o konfiguracji, które są zasadniczo takie same. Alternatywnie, aby skonfigurować poszczególne usługi indywidualnie, można napisać bezwzględny kod, który umożliwia Publikowanie metadanych jednokrotnie, a następnie ponownie wykorzystać ten kod dla kilku różnych usług. Jest to realizowane przez utworzenie nowej klasy, która pochodzi od <xref:System.ServiceModel.ServiceHost> i przesłania `ApplyConfiguration` metodę (), aby bezwzględnie dodać zachowanie publikowania metadanych.  
  
> [!IMPORTANT]
> Dla jasności ten przykład pokazuje, jak utworzyć niezabezpieczony punkt końcowy publikowania metadanych. Takie punkty końcowe są potencjalnie dostępne dla anonimowych użytkowników nieuwierzytelnionych i należy zachować ostrożność przed wdrożeniem takich punktów końcowych, aby upewnić się, że można publicznie odzamknąć metadane usługi.  
  
## <a name="implementing-a-custom-servicehost"></a>Implementowanie niestandardowego ServiceHost

 <xref:System.ServiceModel.ServiceHost>Klasa uwidacznia kilka przydatnych metod wirtualnych, które dziedziczą mogą przesłonić, aby zmienić zachowanie usługi w czasie wykonywania. Na przykład `ApplyConfiguration` Metoda () odczytuje informacje o konfiguracji usługi z magazynu konfiguracji i odpowiednio zmienia hosta <xref:System.ServiceModel.Description.ServiceDescription> . Domyślna implementacja odczytuje konfigurację z pliku konfiguracyjnego aplikacji. Implementacje niestandardowe mogą przesłonić `ApplyConfiguration` (), aby jeszcze bardziej zmienić <xref:System.ServiceModel.Description.ServiceDescription> używany kod, lub nawet całkowicie zastąpić domyślny magazyn konfiguracji. Na przykład, aby odczytać konfigurację punktu końcowego usługi z bazy danych zamiast pliku konfiguracji aplikacji.  
  
 W tym przykładzie chcemy utworzyć niestandardowy ServiceHost, który dodaje ServiceMetadataBehavior (co umożliwia Publikowanie metadanych), nawet jeśli to zachowanie nie zostanie jawnie dodane w pliku konfiguracji usługi. Aby to osiągnąć, Utwórz nową klasę, która dziedziczy z <xref:System.ServiceModel.ServiceHost> i przesłonięcia `ApplyConfiguration` ().  
  
```csharp
class SelfDescribingServiceHost : ServiceHost  
{  
    public SelfDescribingServiceHost(Type serviceType, params Uri[] baseAddresses)  
        : base(serviceType, baseAddresses) { }  
  
    //Overriding ApplyConfiguration() allows us to
    //alter the ServiceDescription prior to opening  
    //the service host.
    protected override void ApplyConfiguration()  
    {  
        //First, we call base.ApplyConfiguration()  
        //to read any configuration that was provided for  
        //the service we're hosting. After this call,  
        //this.Description describes the service  
        //as it was configured.  
        base.ApplyConfiguration();
  
        //(rest of implementation elided for clarity)  
    }  
}  
```  
  
 Ponieważ nie chcemy ignorować żadnej konfiguracji, która została dostarczona w pliku konfiguracyjnym aplikacji, w pierwszej kolejności zastępowanie `ApplyConfiguration` () jest wywołaniem podstawowej implementacji. Po zakończeniu tej metody możemy bezwzględnie dodać <xref:System.ServiceModel.Description.ServiceMetadataBehavior> do opisu przy użyciu następującego kodu.  
  
```csharp
ServiceMetadataBehavior mexBehavior = this.Description.Behaviors.Find<ServiceMetadataBehavior>();  
if (mexBehavior == null)  
{  
    mexBehavior = new ServiceMetadataBehavior();  
    this.Description.Behaviors.Add(mexBehavior);  
}  
else  
{  
    //Metadata behavior has already been configured,
    //so we do not have any work to do.  
    return;  
}  
```  
  
 Ostatnim `ApplyConfiguration` zastępowaniem () musi być dodanie domyślnego punktu końcowego metadanych. Zgodnie z Konwencją jeden punkt końcowy metadanych jest tworzony dla każdego identyfikatora URI w kolekcji BaseAddresses hosta usługi.  
  
```csharp
//Add a metadata endpoint at each base address  
//using the "/mex" addressing convention  
foreach (Uri baseAddress in this.BaseAddresses)  
{  
    if (baseAddress.Scheme == Uri.UriSchemeHttp)  
    {  
        mexBehavior.HttpGetEnabled = true;  
        this.AddServiceEndpoint(ServiceMetadataBehavior.MexContractName,  
                                MetadataExchangeBindings.CreateMexHttpBinding(),  
                                "mex");  
    }  
    else if (baseAddress.Scheme == Uri.UriSchemeHttps)  
    {  
        mexBehavior.HttpsGetEnabled = true;  
        this.AddServiceEndpoint(ServiceMetadataBehavior.MexContractName,  
                                MetadataExchangeBindings.CreateMexHttpsBinding(),  
                                "mex");  
    }  
    else if (baseAddress.Scheme == Uri.UriSchemeNetPipe)  
    {  
        this.AddServiceEndpoint(ServiceMetadataBehavior.MexContractName,  
                                MetadataExchangeBindings.CreateMexNamedPipeBinding(),  
                                "mex");  
    }  
    else if (baseAddress.Scheme == Uri.UriSchemeNetTcp)  
    {  
        this.AddServiceEndpoint(ServiceMetadataBehavior.MexContractName,  
                                MetadataExchangeBindings.CreateMexTcpBinding(),  
                                "mex");  
    }  
}  
```  
  
## <a name="using-a-custom-servicehost-in-self-host"></a>Używanie niestandardowego ServiceHost na własnym hoście  

 Teraz, gdy zakończymy implementację niestandardowej ServiceHost, możemy użyć jej do dodania zachowania publikowania metadanych do dowolnej usługi przez hostowanie tej usługi w ramach naszego wystąpienia `SelfDescribingServiceHost` . Poniższy kod przedstawia sposób korzystania z niego w scenariuszu z własnym hostem.  
  
```csharp
SelfDescribingServiceHost host =
         new SelfDescribingServiceHost( typeof( Calculator ) );  
host.Open();  
```  
  
 Nasz Host niestandardowy nadal odczytuje konfigurację punktu końcowego usługi z pliku konfiguracyjnego aplikacji, tak jakby używała domyślnej <xref:System.ServiceModel.ServiceHost> klasy do hostowania usługi. Jednak ze względu na to, że dodaliśmy logikę umożliwiającą opublikowanie metadanych w ramach naszego hosta niestandardowego, nie należy jawnie włączać zachowania publikowania metadanych w konfiguracji. Takie podejście ma różne zalety podczas kompilowania aplikacji, która zawiera kilka usług i chcesz włączyć Publikowanie metadanych na każdym z nich bez konieczności pisania tych samych elementów konfiguracji w porównaniu do i więcej.  
  
## <a name="using-a-custom-servicehost-in-iis-or-was"></a>Używanie niestandardowego ServiceHost w usługach IIS lub  

 Używanie niestandardowego hosta usługi w scenariuszach z własnym hostem jest proste, ponieważ jest to kod aplikacji, który jest ostatecznie odpowiedzialny za tworzenie i otwieranie wystąpienia hosta usługi. Jednak w usługach IIS lub w środowisku macierzystym Infrastruktura WCF tworzy dynamicznie wystąpienie hosta usługi w odpowiedzi na komunikaty przychodzące. Niestandardowe hosty usługi mogą być również używane w tym środowisku hostingu, ale wymagają one dodatkowego kodu w formie obiektu ServiceHostFactory. Poniższy kod przedstawia pochodne <xref:System.ServiceModel.Activation.ServiceHostFactory> zwracające wystąpienia naszych niestandardowych `SelfDescribingServiceHost` .  
  
```csharp
public class SelfDescribingServiceHostFactory : ServiceHostFactory  
{  
    protected override ServiceHost CreateServiceHost(Type serviceType,
     Uri[] baseAddresses)  
    {  
        //All the custom factory does is return a new instance  
        //of our custom host class. The bulk of the custom logic should  
        //live in the custom host (as opposed to the factory)
        //for maximum  
        //reuse value outside of the IIS/WAS hosting environment.  
        return new SelfDescribingServiceHost(serviceType,
                                             baseAddresses);  
    }  
}  
```  
  
 Jak widać, implementacja niestandardowego obiektu ServiceHostFactory jest prosta. Cała logika niestandardowa znajduje się wewnątrz implementacji ServiceHost; Fabryka zwraca wystąpienie klasy pochodnej.  
  
 Aby użyć fabryki niestandardowej z implementacją usługi, należy dodać dodatkowe metadane do pliku SVC usługi.  
  
```aspx-csharp
<% @ServiceHost Service="Microsoft.ServiceModel.Samples.CalculatorService"
               Factory="Microsoft.ServiceModel.Samples.SelfDescribingServiceHostFactory"
               language=c# Debug="true" %>
```
  
 W tym miejscu dodaliśmy dodatkowy `Factory` atrybut do `@ServiceHost` dyrektywy i przeszedł nazwę typu CLR fabryki niestandardowej jako wartość atrybutu. Gdy usługi IIS lub otrzymali komunikat dla tej usługi, infrastruktura hostingu WCF najpierw tworzy wystąpienie obiektu ServiceHostFactory, a następnie uruchamia wystąpienie samego hosta usługi przez wywołanie `ServiceHostFactory.CreateServiceHost()` .  
  
## <a name="running-the-sample"></a>Uruchamianie przykładowej aplikacji  

 Mimo że ten przykład zapewnia w pełni funkcjonalną implementację klienta i usługi, punkt przykładu ilustruje sposób zmiany zachowania w czasie wykonywania usługi za pomocą niestandardowego hosta. wykonaj następujące czynności:  
  
### <a name="observe-the-effect-of-the-custom-host"></a>Obserwuj efekt hosta niestandardowego
  
1. Otwórz plik Web.config usługi i sprawdź, czy nie ma konfiguracji jawnie włączającej metadane dla usługi.  
  
2. Otwórz plik SVC usługi i sprawdź, czy jego @ServiceHost dyrektywa zawiera atrybut fabryki, który określa nazwę niestandardowego obiektu ServiceHostFactory.  
  
### <a name="set-up-build-and-run-the-sample"></a>Konfigurowanie, kompilowanie i uruchamianie przykładu
  
1. Upewnij się, że została wykonana [Procedura konfiguracji jednorazowej dla przykładów Windows Communication Foundation](one-time-setup-procedure-for-the-wcf-samples.md).

2. Aby skompilować rozwiązanie, postępuj zgodnie z instrukcjami w temacie [Tworzenie przykładów Windows Communication Foundation](building-the-samples.md).

3. Po skompilowaniu rozwiązania Uruchom Setup.bat, aby skonfigurować aplikację ServiceModelSamples w usługach IIS 7,0. Katalog ServiceModelSamples powinien teraz pojawić się jako aplikacja usług IIS 7,0.

4. Aby uruchomić przykład w konfiguracji na jednym lub wielu komputerach, postępuj zgodnie z instrukcjami w temacie [Uruchamianie przykładów Windows Communication Foundation](running-the-samples.md).

5. Aby usunąć aplikację IIS 7,0, uruchom *Cleanup.bat*.

## <a name="see-also"></a>Zobacz też

- [Instrukcje: hostowanie usługi WCF w usługach IIS](../feature-details/how-to-host-a-wcf-service-in-iis.md)
