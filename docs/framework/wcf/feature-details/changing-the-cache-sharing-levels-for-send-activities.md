---
title: Zmienianie poziomów współużytkowania pamięci podręcznej dla działań wysyłania
ms.date: 03/30/2017
ms.assetid: 03926a64-753d-460e-ac06-2a4ff8e1bbf5
ms.openlocfilehash: cbb937ac47c93307db922b28e3df0ea694a77960
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96262051"
---
# <a name="changing-the-cache-sharing-levels-for-send-activities"></a><span data-ttu-id="ce36d-102">Zmienianie poziomów współużytkowania pamięci podręcznej dla działań wysyłania</span><span class="sxs-lookup"><span data-stu-id="ce36d-102">Changing the Cache Sharing Levels for Send Activities</span></span>

<span data-ttu-id="ce36d-103"><xref:System.ServiceModel.Activities.SendMessageChannelCache>Rozszerzenie umożliwia dostosowanie poziomów udostępniania pamięci podręcznej, ustawień pamięci podręcznej fabryki kanałów oraz ustawień pamięci podręcznej kanału dla przepływów pracy, które wysyłają komunikaty do punktów końcowych usługi przy użyciu <xref:System.ServiceModel.Activities.Send> działań związanych z obsługą komunikatów.</span><span class="sxs-lookup"><span data-stu-id="ce36d-103">The <xref:System.ServiceModel.Activities.SendMessageChannelCache> extension enables you to customize the cache sharing levels, the settings of the channel factory cache, and the settings of the channel cache for workflows that send messages to service endpoints using <xref:System.ServiceModel.Activities.Send> messaging activities.</span></span> <span data-ttu-id="ce36d-104">Te przepływy pracy są zwykle przepływy pracy klienta, ale mogą być również usługi przepływu pracy, które znajdują się w <xref:System.ServiceModel.WorkflowServiceHost>.</span><span class="sxs-lookup"><span data-stu-id="ce36d-104">These workflows are typically client workflows but could also be workflow services that are hosted in a <xref:System.ServiceModel.WorkflowServiceHost>.</span></span> <span data-ttu-id="ce36d-105">Pamięć podręczna fabryki kanałów zawiera buforowane <xref:System.ServiceModel.ChannelFactory%601> obiekty.</span><span class="sxs-lookup"><span data-stu-id="ce36d-105">The channel factory cache contains cached <xref:System.ServiceModel.ChannelFactory%601> objects.</span></span> <span data-ttu-id="ce36d-106">Pamięć podręczna kanału zawiera buforowane kanały.</span><span class="sxs-lookup"><span data-stu-id="ce36d-106">The channel cache contains cached channels.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="ce36d-107">Przepływy pracy mogą <xref:System.ServiceModel.Activities.Send> wysyłać komunikaty lub parametry za pomocą działań związanych z wiadomościami.</span><span class="sxs-lookup"><span data-stu-id="ce36d-107">Workflows can use <xref:System.ServiceModel.Activities.Send> messaging activities to send either messages or parameters.</span></span> <span data-ttu-id="ce36d-108">Środowisko uruchomieniowe przepływu pracy dodaje fabryki kanałów do pamięci podręcznej, która tworzy kanały typu w <xref:System.ServiceModel.Channels.IRequestChannel> przypadku używania <xref:System.ServiceModel.Activities.ReceiveReply> działania z <xref:System.ServiceModel.Activities.Send> działaniem, a <xref:System.ServiceModel.Channels.IOutputChannel> kiedy tylko używa <xref:System.ServiceModel.Activities.Send> działania (nie <xref:System.ServiceModel.Activities.ReceiveReply> ).</span><span class="sxs-lookup"><span data-stu-id="ce36d-108">The workflow runtime adds channel factories to the cache that create channels of type <xref:System.ServiceModel.Channels.IRequestChannel> when you use a <xref:System.ServiceModel.Activities.ReceiveReply> activity with a <xref:System.ServiceModel.Activities.Send> activity, and an <xref:System.ServiceModel.Channels.IOutputChannel> when just using a <xref:System.ServiceModel.Activities.Send> activity (no <xref:System.ServiceModel.Activities.ReceiveReply>).</span></span>  
  
## <a name="the-cache-sharing-levels"></a><span data-ttu-id="ce36d-109">Poziomy udostępniania pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="ce36d-109">The Cache Sharing Levels</span></span>  

 <span data-ttu-id="ce36d-110">Domyślnie, w przepływie pracy hostowanym przez <xref:System.ServiceModel.WorkflowServiceHost> pamięć podręczną używaną przez <xref:System.ServiceModel.Activities.Send> działania obsługi komunikatów jest współużytkowany przez wszystkie wystąpienia przepływu pracy w <xref:System.ServiceModel.WorkflowServiceHost> (buforowanie na poziomie hosta).</span><span class="sxs-lookup"><span data-stu-id="ce36d-110">By default, in a workflow hosted by a <xref:System.ServiceModel.WorkflowServiceHost> the cache used by <xref:System.ServiceModel.Activities.Send> messaging activities is shared across all workflow instances in the <xref:System.ServiceModel.WorkflowServiceHost> (host-level caching).</span></span> <span data-ttu-id="ce36d-111">Klient przepływu pracy, który nie jest obsługiwany przez <xref:System.ServiceModel.WorkflowServiceHost>, pamięci podręcznej jest dostępna tylko dla wystąpienia przepływu pracy (buforowanie poziomie wystąpienia).</span><span class="sxs-lookup"><span data-stu-id="ce36d-111">For a client workflow that is not hosted by a <xref:System.ServiceModel.WorkflowServiceHost>, the cache is available only to the workflow instance (instance-level caching).</span></span> <span data-ttu-id="ce36d-112">Pamięć podręczna jest dostępna tylko dla <xref:System.ServiceModel.Activities.Send> działań, które nie korzystają z punktów końcowych zdefiniowanych w konfiguracji, chyba że jest włączone bezpieczne buforowanie.</span><span class="sxs-lookup"><span data-stu-id="ce36d-112">The cache is only available for <xref:System.ServiceModel.Activities.Send> activities that do not use endpoints defined in configuration unless unsafe caching is enabled.</span></span>  
  
 <span data-ttu-id="ce36d-113">Poniżej przedstawiono różne poziomy udostępniania pamięci podręcznej dostępne dla <xref:System.ServiceModel.Activities.Send> działań w przepływie pracy i ich zalecane użycie:</span><span class="sxs-lookup"><span data-stu-id="ce36d-113">The following are the different cache sharing levels available for <xref:System.ServiceModel.Activities.Send> activities in a workflow and their recommended use:</span></span>  
  
- <span data-ttu-id="ce36d-114">**Poziom hosta**: na poziomie udostępniania hosta pamięć podręczna jest dostępna tylko dla wystąpień przepływu pracy hostowanych na hoście usługi przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="ce36d-114">**Host Level**: In the host sharing level, the cache is available only to the workflow instances hosted in the workflow service host.</span></span> <span data-ttu-id="ce36d-115">Pamięć podręczna może być również współużytkowana przez hosty usługi przepływu pracy w pamięci podręcznej dla całego procesu.</span><span class="sxs-lookup"><span data-stu-id="ce36d-115">A cache can also be shared between workflow service hosts in a process-wide cache.</span></span>  
  
- <span data-ttu-id="ce36d-116">**Poziom wystąpienia**: na poziomie udostępniania wystąpienia pamięć podręczna jest dostępna dla określonego wystąpienia przepływu pracy w całym okresie istnienia, ale pamięć podręczna nie jest dostępna dla innych wystąpień przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="ce36d-116">**Instance Level**: In the instance sharing level, the cache is available to a particular workflow instance throughout its lifetime but the cache is not available to other workflow instances.</span></span>  
  
- <span data-ttu-id="ce36d-117">**Brak pamięci podręcznej**: pamięć podręczna jest domyślnie wyłączona, jeśli istnieje przepływ pracy korzystający z punktów końcowych zdefiniowanych w konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="ce36d-117">**No Cache**: The cache is turned off by default if you have a workflow that uses endpoints defined in configuration.</span></span> <span data-ttu-id="ce36d-118">Zalecane jest również, aby pamięć podręczna była wyłączona w tym przypadku, ponieważ jej włączenie może być niezabezpieczone.</span><span class="sxs-lookup"><span data-stu-id="ce36d-118">It is also recommended to keep the cache turned off in this case because turning it on could be unsecure.</span></span> <span data-ttu-id="ce36d-119">Na przykład, jeśli dla każdego wysłania jest wymagana inna tożsamość (różne poświadczenia lub personifikacja).</span><span class="sxs-lookup"><span data-stu-id="ce36d-119">For example, if a different identity (different credentials or using impersonation) is required for each send.</span></span>  
  
## <a name="changing-the-cache-sharing-level-for-a-client-workflow"></a><span data-ttu-id="ce36d-120">Zmiana poziomu udostępniania pamięci podręcznej dla przepływu pracy klienta</span><span class="sxs-lookup"><span data-stu-id="ce36d-120">Changing the Cache Sharing Level for a Client Workflow</span></span>  

 <span data-ttu-id="ce36d-121">Aby ustawić udostępnianie pamięci podręcznej w przepływie pracy klienta, Dodaj wystąpienie <xref:System.ServiceModel.Activities.SendMessageChannelCache> klasy jako rozszerzenie do żądanego zestawu wystąpień przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="ce36d-121">To set the cache sharing in a client workflow, add an instance of the <xref:System.ServiceModel.Activities.SendMessageChannelCache> class as an extension to the desired set of workflow instances.</span></span> <span data-ttu-id="ce36d-122">Powoduje to udostępnienie pamięci podręcznej we wszystkich wystąpieniach przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="ce36d-122">This results in sharing the cache across all the workflow instances.</span></span> <span data-ttu-id="ce36d-123">Poniższy przykład kodu pokazuje, jak wykonać te kroki.</span><span class="sxs-lookup"><span data-stu-id="ce36d-123">The following code examples show how to perform these steps.</span></span>  
  
 <span data-ttu-id="ce36d-124">Najpierw Zadeklaruj wystąpienie typu <xref:System.ServiceModel.Activities.SendMessageChannelCache> .</span><span class="sxs-lookup"><span data-stu-id="ce36d-124">First, declare an instance of type <xref:System.ServiceModel.Activities.SendMessageChannelCache>.</span></span>  
  
```csharp  
// Create an instance of SendMessageChannelCache with default cache settings.  
static SendMessageChannelCache sharedChannelCacheExtension =  
    new SendMessageChannelCache();  
```  
  
 <span data-ttu-id="ce36d-125">Następnie Dodaj rozszerzenie pamięci podręcznej do każdego wystąpienia przepływu pracy klienta.</span><span class="sxs-lookup"><span data-stu-id="ce36d-125">Next, add the cache extension to each client workflow instance.</span></span>  
  
```csharp
WorkflowApplication clientInstance1 = new WorkflowApplication(new clientWorkflow1());  
WorkflowApplication clientInstance2 = new WorkflowApplication(new clientWorkflow2());  
  
// Share the cache extension object
  
clientInstance1.Extensions.Add(sharedChannelCacheExtension);  
clientInstance2.Extensions.Add(sharedChannelCacheExtension);  
```  
  
## <a name="changing-the-cache-sharing-level-for-a-hosted-workflow-service"></a><span data-ttu-id="ce36d-126">Zmiana poziomu udostępniania pamięci podręcznej dla hostowanej usługi przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="ce36d-126">Changing the Cache Sharing Level for a Hosted Workflow Service</span></span>  

 <span data-ttu-id="ce36d-127">Aby ustawić udostępnianie pamięci podręcznej w hostowanej usłudze przepływu pracy, Dodaj wystąpienie <xref:System.ServiceModel.Activities.SendMessageChannelCache> klasy jako rozszerzenie do wszystkich hostów usługi przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="ce36d-127">To set the cache sharing in a hosted workflow service, add an instance of the <xref:System.ServiceModel.Activities.SendMessageChannelCache> class as an extension to all the workflow service hosts.</span></span> <span data-ttu-id="ce36d-128">Powoduje to udostępnienie pamięci podręcznej na wszystkich hostach usługi przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="ce36d-128">This results in sharing the cache across all the workflow service hosts.</span></span> <span data-ttu-id="ce36d-129">Poniższy przykład kodu pokazuje, aby wykonać te kroki.</span><span class="sxs-lookup"><span data-stu-id="ce36d-129">The following code examples show to perform these steps.</span></span>  
  
 <span data-ttu-id="ce36d-130">Najpierw Zadeklaruj wystąpienie typu <xref:System.ServiceModel.Activities.SendMessageChannelCache> na poziomie klasy.</span><span class="sxs-lookup"><span data-stu-id="ce36d-130">First, declare an instance  of type <xref:System.ServiceModel.Activities.SendMessageChannelCache> at the class level.</span></span>  
  
```csharp  
// Create static instance of SendMessageChannelCache with default cache settings.  
static SendMessageChannelCache sharedChannelCacheExtension = new  
    SendMessageChannelCache();  
```  
  
 <span data-ttu-id="ce36d-131">Następnie Dodaj rozszerzenie statycznej pamięci podręcznej do każdego hosta usługi przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="ce36d-131">Next, add the static cache extension to each workflow service host.</span></span>  
  
```csharp  
WorkflowServiceHost host1 = new WorkflowServiceHost(new serviceWorkflow1(), new Uri(baseAddress1));  
WorkflowServiceHost host2 = new WorkflowServiceHost(new serviceWorkflow2(), new Uri(baseAddress2));  
  
// Share the static cache to get an AppDomain level cache.  
host1.WorkflowExtensions.Add(sharedChannelCacheExtension);  
host2.WorkflowExtensions.Add(sharedChannelCacheExtension);  
```  
  
 <span data-ttu-id="ce36d-132">Aby skonfigurować udostępnianie pamięci podręcznej w hostowanej usłudze przepływu pracy na poziomie wystąpienia, Dodaj `Func<SendMessageChannelCache>` delegata jako rozszerzenie hosta usługi przepływu pracy i przypisz tego delegata do kodu, który tworzy wystąpienie nowego wystąpienia <xref:System.ServiceModel.Activities.SendMessageChannelCache> klasy.</span><span class="sxs-lookup"><span data-stu-id="ce36d-132">To set the cache sharing in a hosted workflow service to the instance level, add a `Func<SendMessageChannelCache>` delegate as an extension to the workflow service host and assign this delegate to the code that instantiates a new instance of the <xref:System.ServiceModel.Activities.SendMessageChannelCache> class.</span></span> <span data-ttu-id="ce36d-133">Powoduje to inną pamięć podręczną dla każdego pojedynczego wystąpienia przepływu pracy, a nie pojedynczej pamięci podręcznej udostępnionej przez wszystkie wystąpienia przepływu pracy na hoście usługi przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="ce36d-133">This results in a different cache for each individual workflow instance, instead of a single cache shared by all workflow instances in the workflow service host.</span></span> <span data-ttu-id="ce36d-134">Poniższy przykład kodu pokazuje, jak to osiągnąć za pomocą wyrażenia lambda do bezpośredniego definiowania <xref:System.ServiceModel.Activities.SendMessageChannelCache> rozszerzenia, do którego odwołuje się delegat.</span><span class="sxs-lookup"><span data-stu-id="ce36d-134">The following code example shows how to achieve this by using a lambda expression to directly define the <xref:System.ServiceModel.Activities.SendMessageChannelCache> extension that the delegate points to.</span></span>  
  
```csharp
serviceHost.WorkflowExtensions.Add(() => new SendMessageChannelCache  
{  
    // Use FactorySettings property to add custom factory cache settings.  
    FactorySettings = new ChannelCacheSettings
    { MaxItemsInCache = 5, },  
    // Use ChannelSettings property to add custom channel cache settings.  
    ChannelSettings = new ChannelCacheSettings
    { MaxItemsInCache = 10 },  
});  
```  
  
## <a name="customizing-cache-settings"></a><span data-ttu-id="ce36d-135">Dostosowywanie ustawień pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="ce36d-135">Customizing Cache Settings</span></span>  

 <span data-ttu-id="ce36d-136">Można dostosować ustawienia pamięci podręcznej dla pamięci podręcznej fabryki kanału i pamięci podręcznej kanału.</span><span class="sxs-lookup"><span data-stu-id="ce36d-136">You can customize the cache settings for the channel factory cache and the channel cache.</span></span> <span data-ttu-id="ce36d-137">Ustawienia pamięci podręcznej są zdefiniowane w <xref:System.ServiceModel.Activities.ChannelCacheSettings> klasie.</span><span class="sxs-lookup"><span data-stu-id="ce36d-137">The cache settings are defined in the <xref:System.ServiceModel.Activities.ChannelCacheSettings> class.</span></span> <span data-ttu-id="ce36d-138"><xref:System.ServiceModel.Activities.SendMessageChannelCache>Klasa definiuje domyślne ustawienia pamięci podręcznej dla fabryki kanałów i pamięć podręczną kanału w konstruktorze bez parametrów.</span><span class="sxs-lookup"><span data-stu-id="ce36d-138">The <xref:System.ServiceModel.Activities.SendMessageChannelCache> class defines default cache settings for the channel factory cache and the channel cache in its parameterless constructor.</span></span> <span data-ttu-id="ce36d-139">W poniższej tabeli wymieniono wartości domyślne tych ustawień pamięci podręcznej dla każdego typu pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="ce36d-139">The following table lists the default values of these cache settings for each type of cache.</span></span>  
  
|<span data-ttu-id="ce36d-140">Ustawienia</span><span class="sxs-lookup"><span data-stu-id="ce36d-140">Settings</span></span>|<span data-ttu-id="ce36d-141">LeaseTimeout (min.)</span><span class="sxs-lookup"><span data-stu-id="ce36d-141">LeaseTimeout (min)</span></span>|<span data-ttu-id="ce36d-142">IdleTimeout (minimum)</span><span class="sxs-lookup"><span data-stu-id="ce36d-142">IdleTimeout (min)</span></span>|<span data-ttu-id="ce36d-143">MaxItemsInCache</span><span class="sxs-lookup"><span data-stu-id="ce36d-143">MaxItemsInCache</span></span>|  
|-|-|-|-|  
|<span data-ttu-id="ce36d-144">Domyślna pamięć podręczna fabryki</span><span class="sxs-lookup"><span data-stu-id="ce36d-144">Factory Cache Default</span></span>|<span data-ttu-id="ce36d-145">TimeSpan. MaxValue</span><span class="sxs-lookup"><span data-stu-id="ce36d-145">TimeSpan.MaxValue</span></span>|<span data-ttu-id="ce36d-146">2</span><span class="sxs-lookup"><span data-stu-id="ce36d-146">2</span></span>|<span data-ttu-id="ce36d-147">16</span><span class="sxs-lookup"><span data-stu-id="ce36d-147">16</span></span>|  
|<span data-ttu-id="ce36d-148">Wartość domyślna pamięci podręcznej kanału</span><span class="sxs-lookup"><span data-stu-id="ce36d-148">Channel Cache Default</span></span>|<span data-ttu-id="ce36d-149">5</span><span class="sxs-lookup"><span data-stu-id="ce36d-149">5</span></span>|<span data-ttu-id="ce36d-150">2</span><span class="sxs-lookup"><span data-stu-id="ce36d-150">2</span></span>|<span data-ttu-id="ce36d-151">16</span><span class="sxs-lookup"><span data-stu-id="ce36d-151">16</span></span>|  
  
 <span data-ttu-id="ce36d-152">Aby dostosować ustawienia pamięci podręcznej fabryki i pamięci podręcznej kanałów, Utwórz wystąpienie <xref:System.ServiceModel.Activities.SendMessageChannelCache> klasy przy użyciu konstruktora sparametryzowanego <xref:System.ServiceModel.Activities.SendMessageChannelCache.%23ctor%2A> i przekaż nowe wystąpienie <xref:System.ServiceModel.Activities.ChannelCacheSettings> z wartościami niestandardowymi do każdego z `factorySettings` `channelSettings` parametrów i.</span><span class="sxs-lookup"><span data-stu-id="ce36d-152">To customize the factory cache and channel cache settings, instantiate the <xref:System.ServiceModel.Activities.SendMessageChannelCache> class using the parameterized constructor <xref:System.ServiceModel.Activities.SendMessageChannelCache.%23ctor%2A> and pass a new instance of the <xref:System.ServiceModel.Activities.ChannelCacheSettings> with custom values to each of the `factorySettings` and `channelSettings` parameters.</span></span> <span data-ttu-id="ce36d-153">Następnie Dodaj nowe wystąpienie tej klasy jako rozszerzenie do hosta usługi przepływu pracy lub wystąpienia przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="ce36d-153">Next, add the new instance of this class as an extension to a workflow service host or a workflow instance.</span></span> <span data-ttu-id="ce36d-154">Poniższy przykład kodu pokazuje, jak wykonać te kroki dla wystąpienia przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="ce36d-154">The following code example shows how to perform these steps for a workflow instance.</span></span>  
  
```csharp  
ChannelCacheSettings factorySettings = new ChannelCacheSettings{  
                        MaxItemsInCache = 5,
                        IdleTimeout = TimeSpan.FromMinutes(5),
                        LeaseTimeout = TimeSpan.FromMinutes(20)};  
  
ChannelCacheSettings channelSettings = new ChannelCacheSettings{  
                        MaxItemsInCache = 5,
                        IdleTimeout = TimeSpan.FromMinutes(2),  
                        LeaseTimeout = TimeSpan.FromMinutes(10) };  
  
SendMessageChannelCache customChannelCacheExtension =
    new SendMessageChannelCache(factorySettings, channelSettings);  
  
clientInstance.Extensions.Add(customChannelCacheExtension);  
```  
  
 <span data-ttu-id="ce36d-155">Aby włączyć buforowanie, gdy usługa przepływu pracy ma punkty końcowe zdefiniowane w konfiguracji, Utwórz wystąpienie <xref:System.ServiceModel.Activities.SendMessageChannelCache> klasy przy użyciu konstruktora sparametryzowanego <xref:System.ServiceModel.Activities.SendMessageChannelCache.%23ctor%2A> z `allowUnsafeCaching` parametrem ustawionym na `true` .</span><span class="sxs-lookup"><span data-stu-id="ce36d-155">To enable caching when your workflow service has endpoints defined in configuration, instantiate the <xref:System.ServiceModel.Activities.SendMessageChannelCache> class using the parameterized constructor <xref:System.ServiceModel.Activities.SendMessageChannelCache.%23ctor%2A> with the `allowUnsafeCaching` parameter set to `true`.</span></span> <span data-ttu-id="ce36d-156">Następnie Dodaj nowe wystąpienie tej klasy jako rozszerzenie do hosta usługi przepływu pracy lub wystąpienia przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="ce36d-156">Next, add the new instance of this class as an extension to a workflow service host or a workflow instance.</span></span> <span data-ttu-id="ce36d-157">Poniższy przykład kodu pokazuje, jak włączyć buforowanie dla wystąpienia przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="ce36d-157">The following code example shows how to enable caching for a workflow instance.</span></span>  
  
```csharp  
SendMessageChannelCache customChannelCacheExtension =
    new SendMessageChannelCache{ AllowUnsafeCaching = true };  
  
clientInstance.Extensions.Add(customChannelCacheExtension);  
```  
  
 <span data-ttu-id="ce36d-158">Aby całkowicie wyłączyć pamięć podręczną dla fabryk kanałów i kanałów, Wyłącz pamięć podręczną fabryki kanałów.</span><span class="sxs-lookup"><span data-stu-id="ce36d-158">To disable the cache completely for the channel factories and the channels, disable the channel factory cache.</span></span> <span data-ttu-id="ce36d-159">Spowoduje to również wyłączenie pamięci podręcznej kanału, ponieważ kanały są własnością odpowiednich fabryk kanałów.</span><span class="sxs-lookup"><span data-stu-id="ce36d-159">Doing so also turns off the channel cache as the channels are owned by their corresponding channel factories.</span></span> <span data-ttu-id="ce36d-160">Aby wyłączyć pamięć podręczną fabryki kanałów, Przekaż `factorySettings` parametr do konstruktora, który <xref:System.ServiceModel.Activities.SendMessageChannelCache.%23ctor%2A> został zainicjowany do <xref:System.ServiceModel.Activities.ChannelCacheSettings> wystąpienia o <xref:System.ServiceModel.Activities.ChannelCacheSettings.MaxItemsInCache%2A> wartości 0.</span><span class="sxs-lookup"><span data-stu-id="ce36d-160">To disable the channel factory cache, pass the `factorySettings` parameter to the <xref:System.ServiceModel.Activities.SendMessageChannelCache.%23ctor%2A> constructor initialized to a <xref:System.ServiceModel.Activities.ChannelCacheSettings> instance with a <xref:System.ServiceModel.Activities.ChannelCacheSettings.MaxItemsInCache%2A> value of 0.</span></span> <span data-ttu-id="ce36d-161">Poniższy przykład kodu pokazuje to.</span><span class="sxs-lookup"><span data-stu-id="ce36d-161">The following code example shows this.</span></span>  
  
```csharp  
// Disable the factory cache. This results in the channel cache to be turned off as well.  
ChannelCacheSettings factorySettings = new ChannelCacheSettings  
    { MaxItemsInCache = 0 };  
  
ChannelCacheSettings channelSettings = new ChannelCacheSettings();  
  
SendMessageChannelCache customChannelCacheExtension =
    new SendMessageChannelCache(factorySettings, channelSettings);
  
clientInstance.Extensions.Add(customChannelCacheExtension);  
```  
  
 <span data-ttu-id="ce36d-162">Można wybrać opcję użycia tylko pamięci podręcznej fabryki kanału i wyłączyć pamięć podręczną kanału przez przekazanie `channelSettings` parametru do konstruktora, który <xref:System.ServiceModel.Activities.SendMessageChannelCache.%23ctor%2A> został zainicjowany do <xref:System.ServiceModel.Activities.ChannelCacheSettings> wystąpienia o <xref:System.ServiceModel.Activities.ChannelCacheSettings.MaxItemsInCache%2A> wartości 0.</span><span class="sxs-lookup"><span data-stu-id="ce36d-162">You can choose to use only the channel factory cache and disable the channel cache by passing the `channelSettings` parameter to the <xref:System.ServiceModel.Activities.SendMessageChannelCache.%23ctor%2A> constructor initialized to a <xref:System.ServiceModel.Activities.ChannelCacheSettings> instance with a <xref:System.ServiceModel.Activities.ChannelCacheSettings.MaxItemsInCache%2A> value of 0.</span></span> <span data-ttu-id="ce36d-163">Poniższy przykład kodu pokazuje to.</span><span class="sxs-lookup"><span data-stu-id="ce36d-163">The following code example shows this.</span></span>  
  
```csharp  
ChannelCacheSettings factorySettings = new ChannelCacheSettings();  
// Disable only the channel cache.  
ChannelCacheSettings channelSettings = new ChannelCacheSettings  
    { MaxItemsInCache = 0};  
  
SendMessageChannelCache customChannelCacheExtension =
    new SendMessageChannelCache(factorySettings, channelSettings);
  
clientInstance.Extensions.Add(customChannelCacheExtension);  
```  
  
 <span data-ttu-id="ce36d-164">W hostowanej usłudze przepływu pracy można określić ustawienia pamięci podręcznej i ustawień pamięci podręcznej kanału w pliku konfiguracyjnym aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ce36d-164">In a hosted workflow service, you can specify the factory cache and channel cache settings in the application configuration file.</span></span> <span data-ttu-id="ce36d-165">W tym celu należy dodać zachowanie usługi, które zawiera ustawienia pamięci podręcznej pamięci podręcznej fabryki i kanał i dodać to zachowanie usługi z usługą.</span><span class="sxs-lookup"><span data-stu-id="ce36d-165">To do so, add a service behavior that contains the cache settings for the factory and channel cache and add this service behavior to your service.</span></span> <span data-ttu-id="ce36d-166">Poniższy przykład pokazuje zawartość pliku konfiguracji, który zawiera `MyChannelCacheBehavior` zachowanie usługi z niestandardową pamięcią podręczną i ustawieniami pamięci podręcznej kanału.</span><span class="sxs-lookup"><span data-stu-id="ce36d-166">The following example shows the contents of a configuration file that contains the `MyChannelCacheBehavior` service behavior with the custom factory cache and channel cache settings.</span></span> <span data-ttu-id="ce36d-167">To zachowanie usługi jest dodawane do usługi za pomocą `behaviorConfiguration` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="ce36d-167">This service behavior is added to the service through the `behaviorConfiguration` attribute.</span></span>  
  
```xml  
<configuration>
  <system.serviceModel>  
    <!-- List of other config sections here -->
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="MyChannelCacheBehavior">  
          <sendMessageChannelCache allowUnsafeCaching ="false" >  
            <!-- Control only the host level settings -->
            <factorySettings maxItemsInCache = "8" idleTimeout = "00:05:00" leaseTimeout="10:00:00" />  
            <channelSettings maxItemsInCache = "32" idleTimeout = "00:05:00" leaseTimeout="00:06:00" />  
          </sendMessageChannelCache>  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
    <services>  
      <service name="MyService" behaviorConfiguration="MyChannelCacheBehavior" />  
    </services>  
  </system.serviceModel>  
</configuration>  
```
