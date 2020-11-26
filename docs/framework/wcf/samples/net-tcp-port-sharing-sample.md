---
title: Przykład współużytkowania portów Net.TCP
ms.date: 03/30/2017
ms.assetid: 03da5959-0574-4e91-8a53-05854b6c55dc
ms.openlocfilehash: fa62734ed6a4a016011c9f29b3665dae05a000c6
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96235380"
---
# <a name="nettcp-port-sharing-sample"></a><span data-ttu-id="6608e-102">Przykład współużytkowania portów Net.TCP</span><span class="sxs-lookup"><span data-stu-id="6608e-102">Net.TCP Port Sharing Sample</span></span>

<span data-ttu-id="6608e-103">Protokół TCP/IP używa liczby 16-bitowej zwanej portem do rozróżniania połączeń z wieloma aplikacjami sieciowymi uruchomionymi na tym samym komputerze.</span><span class="sxs-lookup"><span data-stu-id="6608e-103">The TCP/IP protocol uses a 16-bit number, called a port, to differentiate connections to multiple network applications running on the same machine.</span></span> <span data-ttu-id="6608e-104">Jeśli aplikacja nasłuchuje na porcie, cały ruch TCP dla tego portu przechodzi do tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6608e-104">If an application is listening on a port, then all TCP traffic for that port goes to that application.</span></span> <span data-ttu-id="6608e-105">Inne aplikacje nie mogą nasłuchiwać tego portu w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="6608e-105">Other applications cannot listen on that port at the same time.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="6608e-106">Przykłady mogą być już zainstalowane na komputerze.</span><span class="sxs-lookup"><span data-stu-id="6608e-106">The samples may already be installed on your machine.</span></span> <span data-ttu-id="6608e-107">Przed kontynuowaniem Wyszukaj następujący katalog (domyślny).</span><span class="sxs-lookup"><span data-stu-id="6608e-107">Check for the following (default) directory before continuing.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> <span data-ttu-id="6608e-108">Jeśli ten katalog nie istnieje, przejdź do [przykładów Windows Communication Foundation (WCF) i Windows Workflow Foundation (WF) dla .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) , aby pobrać wszystkie Windows Communication Foundation (WCF) i [!INCLUDE[wf1](../../../../includes/wf1-md.md)] przykłady.</span><span class="sxs-lookup"><span data-stu-id="6608e-108">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="6608e-109">Ten przykład znajduje się w następującym katalogu.</span><span class="sxs-lookup"><span data-stu-id="6608e-109">This sample is located in the following directory.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Binding\Net\TCP\PortSharing`  
  
 <span data-ttu-id="6608e-110">Wiele protokołów ma standardowy lub domyślny numer portu, którego używają.</span><span class="sxs-lookup"><span data-stu-id="6608e-110">Many protocols have a standard or default port number that they use.</span></span> <span data-ttu-id="6608e-111">Na przykład protokół HTTP zwykle używa portu TCP 80.</span><span class="sxs-lookup"><span data-stu-id="6608e-111">For example, the HTTP protocol typically uses TCP port 80.</span></span> <span data-ttu-id="6608e-112">Internet Information Services (IIS) ma odbiornik do udostępniania portu między wieloma aplikacjami HTTP.</span><span class="sxs-lookup"><span data-stu-id="6608e-112">Internet Information Services (IIS) has a listener to share a port between multiple HTTP applications.</span></span> <span data-ttu-id="6608e-113">Usługi IIS nasłuchują na porcie bezpośrednio i przesyłają komunikaty do odpowiedniej aplikacji w oparciu o informacje znajdujące się w strumieniu wiadomości.</span><span class="sxs-lookup"><span data-stu-id="6608e-113">IIS listens on the port directly and forwards messages to the appropriate application based on information inside the message stream.</span></span> <span data-ttu-id="6608e-114">Pozwala to wielu aplikacjom HTTP korzystać z tego samego numeru portu bez konieczności konkurowania, aby zarezerwować port do odbioru wiadomości.</span><span class="sxs-lookup"><span data-stu-id="6608e-114">This allows multiple HTTP applications to use the same port number without having to compete to reserve the port for receiving messages.</span></span>  
  
 <span data-ttu-id="6608e-115">Udostępnianie portów NetTcp to funkcja programu Windows Communication Foundation (WCF), która w podobny sposób pozwala wielu aplikacjom sieciowym współużytkować jeden port.</span><span class="sxs-lookup"><span data-stu-id="6608e-115">NetTcp Port Sharing is a Windows Communication Foundation (WCF)feature that similarly allows multiple network applications to share a single port.</span></span> <span data-ttu-id="6608e-116">Usługa udostępniania portów NetTcp akceptuje połączenia za pomocą protokołu net. TCP i przekazuje komunikaty na podstawie ich adresu docelowego.</span><span class="sxs-lookup"><span data-stu-id="6608e-116">The NetTcp Port Sharing Service accepts connections using the net.tcp protocol and forwards messages based on their destination address.</span></span>  
  
 <span data-ttu-id="6608e-117">Usługa udostępniania portów NetTcp nie jest domyślnie włączona.</span><span class="sxs-lookup"><span data-stu-id="6608e-117">The NetTcp Port Sharing Service is not enabled by default.</span></span> <span data-ttu-id="6608e-118">Przed uruchomieniem tego przykładu należy ręcznie włączyć usługę.</span><span class="sxs-lookup"><span data-stu-id="6608e-118">Before running this sample, you must manually enable the service.</span></span> <span data-ttu-id="6608e-119">Aby uzyskać więcej informacji, zobacz [jak: Włączanie usługi udostępniania portów Net. TCP](../feature-details/how-to-enable-the-net-tcp-port-sharing-service.md).</span><span class="sxs-lookup"><span data-stu-id="6608e-119">For more information, see [How to: Enable the Net.TCP Port Sharing Service](../feature-details/how-to-enable-the-net-tcp-port-sharing-service.md).</span></span> <span data-ttu-id="6608e-120">Jeśli usługa jest wyłączona, podczas uruchamiania aplikacji serwera zostanie zgłoszony wyjątek.</span><span class="sxs-lookup"><span data-stu-id="6608e-120">If the service is disabled, an exception is thrown when the server application is started.</span></span>  
  
```console
Unhandled Exception: System.ServiceModel.CommunicationException: The TransportManager failed to listen on the supplied URI using the NetTcpPortSharing service: failed to start the service because it is disabled. An administrator can enable it by running 'sc.exe config NetTcpPortSharing start= demand'.. ---> System.InvalidOperationException: Cannot start service NetTcpPortSharing on computer '.'. ---> System.ComponentModel.Win32Exception: The service cannot be started, either because it is disabled or because it has no enabled devices associated with it  
```  
  
 <span data-ttu-id="6608e-121">Udostępnianie portów jest włączone na serwerze przez ustawienie <xref:System.ServiceModel.NetTcpBinding.PortSharingEnabled%2A> właściwości <xref:System.ServiceModel.NetTcpBinding> powiązania lub <xref:System.ServiceModel.Channels.TcpTransportBindingElement> elementu powiązania.</span><span class="sxs-lookup"><span data-stu-id="6608e-121">Port sharing is enabled on the server by setting the <xref:System.ServiceModel.NetTcpBinding.PortSharingEnabled%2A> property of the <xref:System.ServiceModel.NetTcpBinding> binding or the <xref:System.ServiceModel.Channels.TcpTransportBindingElement> binding element.</span></span> <span data-ttu-id="6608e-122">Klient nie musi wiedzieć, jak Udostępnianie portów zostało skonfigurowane do korzystania z niego na serwerze.</span><span class="sxs-lookup"><span data-stu-id="6608e-122">The client does not have to know how port sharing has been configured to use it on the server.</span></span>  
  
## <a name="enabling-port-sharing"></a><span data-ttu-id="6608e-123">Włączanie udostępniania portów</span><span class="sxs-lookup"><span data-stu-id="6608e-123">Enabling Port Sharing</span></span>  

 <span data-ttu-id="6608e-124">Poniższy kod demonstruje włączenie udostępniania portów na serwerze.</span><span class="sxs-lookup"><span data-stu-id="6608e-124">The following code demonstrates enabling port sharing on the server.</span></span> <span data-ttu-id="6608e-125">Uruchamia wystąpienie `ICalculator` usługi na stałym porcie ze losową ścieżką URI.</span><span class="sxs-lookup"><span data-stu-id="6608e-125">It starts an instance of the `ICalculator` service on a fixed port with a random URI path.</span></span> <span data-ttu-id="6608e-126">Mimo że dwie usługi mogą współużytkować ten sam port, ich ogólne adresy punktów końcowych nadal muszą być unikatowe, aby usługa udostępniania portów NetTcp mogła kierować komunikaty do odpowiedniej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6608e-126">Even though two services can share the same port, their overall endpoint addresses still must be unique so that the NetTcp Port Sharing Service can route messages to the correct application.</span></span>  

```csharp
// Configure a binding with TCP port sharing enabled  
NetTcpBinding binding = new NetTcpBinding();  
binding.PortSharingEnabled = true;  
  
// Start a service on a fixed TCP port  
ServiceHost host = new ServiceHost(typeof(CalculatorService));  
ushort salt = (ushort)new Random().Next();  
string address = $"net.tcp://localhost:9000/calculator/{salt}";
host.AddServiceEndpoint(typeof(ICalculator), binding, address);  
host.Open();  
```

 <span data-ttu-id="6608e-127">Włączenie udostępniania portów umożliwia uruchomienie usługi wiele razy bez konfliktu przez numer portu.</span><span class="sxs-lookup"><span data-stu-id="6608e-127">With port sharing enabled, you can run the service multiple times without having a conflict over the port number.</span></span> <span data-ttu-id="6608e-128">Jeśli zmienisz kod w celu wyłączenia udostępniania portów, uruchomienie dwóch kopii usługi powoduje, że w drugim kończy się niepowodzeniem z <xref:System.ServiceModel.AddressAlreadyInUseException> .</span><span class="sxs-lookup"><span data-stu-id="6608e-128">If you change the code to disable port sharing, starting up two copies of the service results in the second failing with an <xref:System.ServiceModel.AddressAlreadyInUseException>.</span></span>  
  
```console  
Unhandled Exception: System.ServiceModel.AddressAlreadyInUseException: There is already a listener on IP endpoint 0.0.0.0:9000.  Make sure that you are not trying to use this endpoint multiple times in your application and that there are no other applications listening on this endpoint. ---> System.Net.Sockets.SocketException: Only one usage of each socket address (protocol/network address/port) is normally permitted  
```  
  
## <a name="running-the-sample"></a><span data-ttu-id="6608e-129">Uruchamianie przykładu</span><span class="sxs-lookup"><span data-stu-id="6608e-129">Running the Sample</span></span>  

 <span data-ttu-id="6608e-130">Możesz użyć klienta testowego, aby sprawdzić, czy komunikaty są prawidłowo kierowane do usług udostępniających port.</span><span class="sxs-lookup"><span data-stu-id="6608e-130">You can use the test client to check that messages are correctly routed to services sharing the port.</span></span>  

```csharp
class client  
{  
   static void Main(string[] args)  
   {  
      Console.Write("Enter the service number to test: ");  
      ushort salt = ushort.Parse(Console.ReadLine());  
      string address = $"net.tcp://localhost:9000/calculator/{salt}";
      ChannelFactory<ICalculator> factory = new ChannelFactory<ICalculator>(new NetTcpBinding());  
      ICalculator proxy = factory.CreateChannel(new EndpointAddress(address));  
  
      // Call the Add service operation.  
      double value1 = 100.00D;  
      double value2 = 15.99D;  
      double result = proxy.Add(value1, value2);  
      Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);  
  
      // Call the Subtract service operation.  
      value1 = 145.00D;  
      value2 = 76.54D;  
      result = proxy.Subtract(value1, value2);  
      Console.WriteLine("Subtract({0},{1}) = {2}", value1, value2, result);  
  
      // Call the Multiply service operation.  
      value1 = 9.00D;  
      value2 = 81.25D;  
      result = proxy.Multiply(value1, value2);  
      Console.WriteLine("Multiply({0},{1}) = {2}", value1, value2, result);  
  
      // Call the Divide service operation.  
      value1 = 22.00D;  
      value2 = 7.00D;  
      result = proxy.Divide(value1, value2);  
      Console.WriteLine("Divide({0},{1}) = {2}", value1, value2, result);  
  
      Console.WriteLine();  
      Console.WriteLine("Press <ENTER> to terminate client.");  
      Console.ReadLine();  
  
      factory.Close();  
   }  
}  
```

 <span data-ttu-id="6608e-131">Każde wystąpienie usługi drukuje swój unikatowy numer i adres.</span><span class="sxs-lookup"><span data-stu-id="6608e-131">Each instance of the service prints out its unique number and address.</span></span> <span data-ttu-id="6608e-132">Na przykład po uruchomieniu service.exe może zostać wyświetlony następujący tekst.</span><span class="sxs-lookup"><span data-stu-id="6608e-132">For instance, you may see the following text when you run service.exe.</span></span>  
  
```console  
Service #4381 listening on net.tcp://localhost:9000/calculator/4381.  
Press <ENTER> to terminate service.  
```  
  
 <span data-ttu-id="6608e-133">Wprowadź numer usługi widoczny w tym miejscu podczas uruchamiania client.exe.</span><span class="sxs-lookup"><span data-stu-id="6608e-133">Enter the service number you see here when you run client.exe.</span></span>  
  
```console  
Enter the service number to test: 4381  
Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
  
Press <ENTER> to terminate client.  
```  
  
 <span data-ttu-id="6608e-134">Ten przykład można uruchomić w konfiguracji między maszynami, zmieniając wygenerowany adres wykorzystywany przez klienta.</span><span class="sxs-lookup"><span data-stu-id="6608e-134">This sample can be run in a cross-machine configuration by changing the generated address that the client uses.</span></span> <span data-ttu-id="6608e-135">W Client.cs Zmień ciąg formatu adresu punktu końcowego, aby odpowiadał nowemu adresowi usługi.</span><span class="sxs-lookup"><span data-stu-id="6608e-135">In the Client.cs, change the endpoint address format string to match the new address of your service.</span></span> <span data-ttu-id="6608e-136">Zastąp wszystkie odwołania do "localhost" adresem IP komputera serwera.</span><span class="sxs-lookup"><span data-stu-id="6608e-136">Replace any references to "localhost" with the IP address of the server machine.</span></span> <span data-ttu-id="6608e-137">Po wprowadzeniu tej zmiany należy ponownie skompilować przykład.</span><span class="sxs-lookup"><span data-stu-id="6608e-137">You must recompile the sample after making this change.</span></span>  
  
#### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="6608e-138">Aby skonfigurować, skompilować i uruchomić przykład</span><span class="sxs-lookup"><span data-stu-id="6608e-138">To set up, build, and run the sample</span></span>  
  
1. <span data-ttu-id="6608e-139">Zainstaluj ASP.NET 4,0 przy użyciu następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="6608e-139">Install ASP.NET 4.0 using the following command.</span></span>  
  
    ```console  
    %windir%\Microsoft.NET\Framework\v4.0.XXXXX\aspnet_regiis.exe /i /enable  
    ```  
  
2. <span data-ttu-id="6608e-140">Upewnij się, że została wykonana [Procedura konfiguracji jednorazowej dla przykładów Windows Communication Foundation](one-time-setup-procedure-for-the-wcf-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6608e-140">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>  
  
3. <span data-ttu-id="6608e-141">Włącz usługę udostępniania portów NetTcp, jak opisano wcześniej w sekcji wprowadzenie.</span><span class="sxs-lookup"><span data-stu-id="6608e-141">Enable the NetTcp Port Sharing Service as previously described in the introduction section.</span></span>  
  
4. <span data-ttu-id="6608e-142">Aby skompilować wersję rozwiązania w języku C# lub Visual Basic .NET, postępuj zgodnie z instrukcjami w temacie [Tworzenie przykładów Windows Communication Foundation](building-the-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6608e-142">To build the C# or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>  
  
5. <span data-ttu-id="6608e-143">Aby uruchomić przykład w konfiguracji na jednym lub wielu komputerach, postępuj zgodnie z instrukcjami w temacie [Uruchamianie przykładów Windows Communication Foundation](running-the-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6608e-143">To run the sample in a single- or cross-machine configuration, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span> <span data-ttu-id="6608e-144">Szczegółowe informacje na temat uruchamiania tego przykładu są zawarte wcześniej w sekcji Uruchamianie przykładu.</span><span class="sxs-lookup"><span data-stu-id="6608e-144">Specific details for running this sample are included previously in the Running the Sample section.</span></span>  
