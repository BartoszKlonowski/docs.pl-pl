---
title: 'Instrukcje: hostowanie usługi WCF w usłudze WAS'
ms.date: 03/30/2017
ms.assetid: 9e3e213e-2dce-4f98-81a3-f62f44caeb54
ms.openlocfilehash: 8049b7961169c6ec7a8d80fb0e8747e99992247b
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90555975"
---
# <a name="how-to-host-a-wcf-service-in-was"></a><span data-ttu-id="a3ff5-102">Instrukcje: hostowanie usługi WCF w usłudze WAS</span><span class="sxs-lookup"><span data-stu-id="a3ff5-102">How to: Host a WCF Service in WAS</span></span>
<span data-ttu-id="a3ff5-103">W tym temacie przedstawiono podstawowe kroki wymagane do utworzenia usług aktywacji procesów systemu Windows (znanych także jako usługa Windows Communication Foundation hostowanej usługi WCF).</span><span class="sxs-lookup"><span data-stu-id="a3ff5-103">This topic outlines the basic steps required to create a Windows Process Activation Services (also known as WAS) hosted Windows Communication Foundation (WCF) service.</span></span> <span data-ttu-id="a3ff5-104">BYŁA to nowa usługa aktywacji procesów, która jest generalizacją funkcji Internet Information Services (IIS), które działają z protokołami transportu innym niż HTTP.</span><span class="sxs-lookup"><span data-stu-id="a3ff5-104">WAS is the new process activation service that is a generalization of Internet Information Services (IIS) features that work with non-HTTP transport protocols.</span></span> <span data-ttu-id="a3ff5-105">Funkcja WCF używa interfejsu adaptera odbiornika do przekazywania żądań aktywacji odbieranych za pośrednictwem protokołów innych niż HTTP obsługiwanych przez program WCF, takich jak TCP, nazwane potoki i kolejkowanie komunikatów.</span><span class="sxs-lookup"><span data-stu-id="a3ff5-105">WCF uses the listener adapter interface to communicate activation requests that are received over the non-HTTP protocols supported by WCF, such as TCP, named pipes, and Message Queuing.</span></span>  
  
 <span data-ttu-id="a3ff5-106">Ta opcja hostingu wymaga, aby składniki aktywacji zostały prawidłowo zainstalowane i skonfigurowane, ale nie wymagają zapisywania kodu hostingu jako części aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a3ff5-106">This hosting option requires that WAS activation components are properly installed and configured, but it does not require any hosting code to be written as part of the application.</span></span> <span data-ttu-id="a3ff5-107">Aby uzyskać więcej informacji na temat instalowania i konfigurowania programu, zobacz [jak: Instalowanie i Konfigurowanie składników aktywacji programu WCF](how-to-install-and-configure-wcf-activation-components.md).</span><span class="sxs-lookup"><span data-stu-id="a3ff5-107">For more information about installing and configuring WAS, see [How to: Install and Configure WCF Activation Components](how-to-install-and-configure-wcf-activation-components.md).</span></span>  
  
> [!WARNING]
> <span data-ttu-id="a3ff5-108">Aktywacja nie jest obsługiwana, jeśli potok przetwarzania żądań serwera sieci Web jest ustawiony na tryb klasyczny.</span><span class="sxs-lookup"><span data-stu-id="a3ff5-108">WAS activation is not supported if the web server’s request processing pipeline is set to Classic mode.</span></span> <span data-ttu-id="a3ff5-109">Jeśli aktywacja ma być używana, potok przetwarzania żądań serwera sieci Web musi być ustawiony na tryb zintegrowany.</span><span class="sxs-lookup"><span data-stu-id="a3ff5-109">The web server’s request processing pipeline must be set to Integrated mode if WAS activation is to be used.</span></span>  
  
 <span data-ttu-id="a3ff5-110">Gdy usługa WCF jest hostowana w programie, standardowe powiązania są używane w zwykły sposób.</span><span class="sxs-lookup"><span data-stu-id="a3ff5-110">When a WCF service is hosted in WAS, the standard bindings are used in the usual way.</span></span> <span data-ttu-id="a3ff5-111">Jednak w przypadku korzystania z <xref:System.ServiceModel.NetTcpBinding> i w <xref:System.ServiceModel.NetNamedPipeBinding> celu skonfigurowania usługi hostowanej należy spełnić ograniczenie.</span><span class="sxs-lookup"><span data-stu-id="a3ff5-111">However, when using the <xref:System.ServiceModel.NetTcpBinding> and the <xref:System.ServiceModel.NetNamedPipeBinding> to configure a WAS-hosted service, a constraint must be satisfied.</span></span> <span data-ttu-id="a3ff5-112">Gdy różne punkty końcowe używają tego samego transportu, ustawienia powiązania muszą być zgodne z następującymi siedem właściwości:</span><span class="sxs-lookup"><span data-stu-id="a3ff5-112">When different endpoints use the same transport, the binding settings have to match on the following seven properties:</span></span>  
  
- <span data-ttu-id="a3ff5-113">ConnectionBufferSize</span><span class="sxs-lookup"><span data-stu-id="a3ff5-113">ConnectionBufferSize</span></span>  
  
- <span data-ttu-id="a3ff5-114">ChannelInitializationTimeout</span><span class="sxs-lookup"><span data-stu-id="a3ff5-114">ChannelInitializationTimeout</span></span>  
  
- <span data-ttu-id="a3ff5-115">MaxPendingConnections</span><span class="sxs-lookup"><span data-stu-id="a3ff5-115">MaxPendingConnections</span></span>  
  
- <span data-ttu-id="a3ff5-116">MaxOutputDelay</span><span class="sxs-lookup"><span data-stu-id="a3ff5-116">MaxOutputDelay</span></span>  
  
- <span data-ttu-id="a3ff5-117">MaxPendingAccepts</span><span class="sxs-lookup"><span data-stu-id="a3ff5-117">MaxPendingAccepts</span></span>  
  
- <span data-ttu-id="a3ff5-118">ConnectionPoolSettings. IdleTimeout</span><span class="sxs-lookup"><span data-stu-id="a3ff5-118">ConnectionPoolSettings.IdleTimeout</span></span>  
  
- <span data-ttu-id="a3ff5-119">ConnectionPoolSettings. MaxOutboundConnectionsPerEndpoint</span><span class="sxs-lookup"><span data-stu-id="a3ff5-119">ConnectionPoolSettings.MaxOutboundConnectionsPerEndpoint</span></span>  
  
 <span data-ttu-id="a3ff5-120">W przeciwnym razie punkt końcowy, który jest inicjowany najpierw zawsze określa wartości tych właściwości, i punkty końcowe dodane później throw, <xref:System.ServiceModel.ServiceActivationException> Jeśli nie są zgodne z tymi ustawieniami.</span><span class="sxs-lookup"><span data-stu-id="a3ff5-120">Otherwise, the endpoint that is initialized first always determines the values of these properties, and endpoints added later throw a <xref:System.ServiceModel.ServiceActivationException> if they do not match those settings.</span></span>  
  
 <span data-ttu-id="a3ff5-121">Aby uzyskać kopię źródła tego przykładu, zobacz [Aktywacja protokołu TCP](../samples/tcp-activation.md).</span><span class="sxs-lookup"><span data-stu-id="a3ff5-121">For the source copy of this example, see [TCP Activation](../samples/tcp-activation.md).</span></span>  
  
### <a name="to-create-a-basic-service-hosted-by-was"></a><span data-ttu-id="a3ff5-122">Aby utworzyć podstawową usługę hostowaną przez program:</span><span class="sxs-lookup"><span data-stu-id="a3ff5-122">To create a basic service hosted by WAS</span></span>  
  
1. <span data-ttu-id="a3ff5-123">Zdefiniuj kontrakt usługi dla typu usługi.</span><span class="sxs-lookup"><span data-stu-id="a3ff5-123">Define a service contract for the type of service.</span></span>  
  
     [!code-csharp[C_HowTo_HostInWAS#1121](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostinwas/cs/service.cs#1121)]  
  
2. <span data-ttu-id="a3ff5-124">Zaimplementuj kontrakt usługi w klasie usługi.</span><span class="sxs-lookup"><span data-stu-id="a3ff5-124">Implement the service contract in a service class.</span></span> <span data-ttu-id="a3ff5-125">Należy zauważyć, że informacje o adresie lub powiązaniu nie są określone w implementacji usługi.</span><span class="sxs-lookup"><span data-stu-id="a3ff5-125">Note that address or binding information is not specified inside the implementation of the service.</span></span> <span data-ttu-id="a3ff5-126">Ponadto kod nie musi być zapisany, aby można było pobrać te informacje z pliku konfiguracyjnego.</span><span class="sxs-lookup"><span data-stu-id="a3ff5-126">Also, code does not have to be written to retrieve that information from the configuration file.</span></span>  
  
     [!code-csharp[C_HowTo_HostInWAS#1122](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostinwas/cs/service.cs#1122)]  
  
3. <span data-ttu-id="a3ff5-127">Utwórz plik Web.config, aby zdefiniować <xref:System.ServiceModel.NetTcpBinding> powiązanie, które ma być używane przez `CalculatorService` punkty końcowe.</span><span class="sxs-lookup"><span data-stu-id="a3ff5-127">Create a Web.config file to define the <xref:System.ServiceModel.NetTcpBinding> binding to be used by the `CalculatorService` endpoints.</span></span>  
  
    ```xml  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
      <system.serviceModel>  
        <bindings>  
          <netTcpBinding>  
            <binding portSharingEnabled="true">  
              <security mode="None" />  
            </binding>  
          </netTcpBinding>  
        </bindings>  
      </system.serviceModel>  
    </configuration>  
    ```  
  
4. <span data-ttu-id="a3ff5-128">Utwórz plik Service. svc zawierający poniższy kod.</span><span class="sxs-lookup"><span data-stu-id="a3ff5-128">Create a Service.svc file that contains the following code.</span></span>  
  
   ```aspx-csharp
   <%@ServiceHost language=c# Service="CalculatorService" %>
   ```
  
5. <span data-ttu-id="a3ff5-129">Umieść plik Service. svc w katalogu wirtualnym usług IIS.</span><span class="sxs-lookup"><span data-stu-id="a3ff5-129">Place the Service.svc file in your IIS virtual directory.</span></span>  
  
### <a name="to-create-a-client-to-use-the-service"></a><span data-ttu-id="a3ff5-130">Aby utworzyć klienta do korzystania z usługi</span><span class="sxs-lookup"><span data-stu-id="a3ff5-130">To create a client to use the service</span></span>  
  
1. <span data-ttu-id="a3ff5-131">Użyj [Narzędzia Narzędzia metadanych ServiceModel (Svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md) z wiersza polecenia, aby wygenerować kod na podstawie metadanych usługi.</span><span class="sxs-lookup"><span data-stu-id="a3ff5-131">Use [ServiceModel Metadata Utility Tool (Svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md) from the command line to generate code from service metadata.</span></span>  
  
    ```console
    Svcutil.exe <service's Metadata Exchange (MEX) address or HTTP GET address>
    ```  
  
2. <span data-ttu-id="a3ff5-132">Wygenerowany klient zawiera `ICalculator` interfejs, który definiuje kontrakt usługi, który musi spełniać implementacja klienta.</span><span class="sxs-lookup"><span data-stu-id="a3ff5-132">The client that is generated contains the `ICalculator` interface that defines the service contract that the client implementation must satisfy.</span></span>  
  
     [!code-csharp[C_HowTo_HostInWAS#1221](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostinwas/cs/client.cs#1221)]  
  
3. <span data-ttu-id="a3ff5-133">Wygenerowana aplikacja kliencka zawiera również implementację programu `ClientCalculator` .</span><span class="sxs-lookup"><span data-stu-id="a3ff5-133">The generated client application also contains the implementation of the `ClientCalculator`.</span></span> <span data-ttu-id="a3ff5-134">Należy zauważyć, że informacje o adresie i powiązaniu nie są określone w dowolnym miejscu w implementacji usługi.</span><span class="sxs-lookup"><span data-stu-id="a3ff5-134">Note that the address and binding information is not specified anywhere inside the implementation of the service.</span></span> <span data-ttu-id="a3ff5-135">Ponadto kod nie musi być zapisany, aby można było pobrać te informacje z pliku konfiguracyjnego.</span><span class="sxs-lookup"><span data-stu-id="a3ff5-135">Also, code does not have to be written to retrieve that information from the configuration file.</span></span>  
  
     [!code-csharp[C_HowTo_HostInWAS#1222](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostinwas/cs/client.cs#1222)]  
  
4. <span data-ttu-id="a3ff5-136">Konfiguracja klienta korzystającego z programu <xref:System.ServiceModel.NetTcpBinding> jest również generowana przez Svcutil.exe.</span><span class="sxs-lookup"><span data-stu-id="a3ff5-136">The configuration for the client that uses the <xref:System.ServiceModel.NetTcpBinding> is also generated by Svcutil.exe.</span></span> <span data-ttu-id="a3ff5-137">Ten plik powinien być nazwany w pliku App.config podczas korzystania z programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a3ff5-137">This file should be named in the App.config file when using Visual Studio.</span></span>  
  
     [!code-xml[C_HowTo_HostInWAS#2211](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostinwas/common/app.config#2211)]
  
5. <span data-ttu-id="a3ff5-138">Utwórz wystąpienie elementu `ClientCalculator` w aplikacji, a następnie Wywołaj operacje usługi.</span><span class="sxs-lookup"><span data-stu-id="a3ff5-138">Create an instance of the `ClientCalculator` in an application and then call the service operations.</span></span>  
  
     [!code-csharp[C_HowTo_HostInWAS#1223](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostinwas/cs/client.cs#1223)]  
  
6. <span data-ttu-id="a3ff5-139">Kompiluj i uruchom klienta.</span><span class="sxs-lookup"><span data-stu-id="a3ff5-139">Compile and run the client.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="a3ff5-140">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="a3ff5-140">See also</span></span>

- [<span data-ttu-id="a3ff5-141">Aktywacja TCP</span><span class="sxs-lookup"><span data-stu-id="a3ff5-141">TCP Activation</span></span>](../samples/tcp-activation.md)
- <span data-ttu-id="a3ff5-142">[Funkcje hostingu sieci szkieletowej aplikacji systemu Windows Server](/previous-versions/appfabric/ee677189(v=azure.10))</span><span class="sxs-lookup"><span data-stu-id="a3ff5-142">[Windows Server App Fabric Hosting Features](/previous-versions/appfabric/ee677189(v=azure.10))</span></span>
