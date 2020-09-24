---
title: <serviceThrottling>
ms.date: 03/30/2017
ms.assetid: a337d064-1e64-4209-b4a9-db7fdb7e3eaf
ms.openlocfilehash: 0c6d844ac287037b7a546d3a48e7cd924e8a63d1
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91153615"
---
# \<serviceThrottling>

<span data-ttu-id="b2676-101">Określa mechanizm ograniczania przepustowości usługi Windows Communication Foundation (WCF).</span><span class="sxs-lookup"><span data-stu-id="b2676-101">Specifies the throttling mechanism of a Windows Communication Foundation (WCF) service.</span></span>  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<serviceBehaviors>**](servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<behavior>**](behavior-of-servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<serviceThrottling>**  
  
## <a name="syntax"></a><span data-ttu-id="b2676-102">Składnia</span><span class="sxs-lookup"><span data-stu-id="b2676-102">Syntax</span></span>  
  
```xml  
<serviceThrottling maxConcurrentCalls="Integer"
                   maxConcurrentInstances="Integer"
                   maxConcurrentSessions="Integer" />
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="b2676-103">Atrybuty i elementy</span><span class="sxs-lookup"><span data-stu-id="b2676-103">Attributes and Elements</span></span>  

 <span data-ttu-id="b2676-104">W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.</span><span class="sxs-lookup"><span data-stu-id="b2676-104">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="b2676-105">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="b2676-105">Attributes</span></span>  
  
|<span data-ttu-id="b2676-106">Atrybut</span><span class="sxs-lookup"><span data-stu-id="b2676-106">Attribute</span></span>|<span data-ttu-id="b2676-107">Opis</span><span class="sxs-lookup"><span data-stu-id="b2676-107">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="b2676-108">maxConcurrentCalls</span><span class="sxs-lookup"><span data-stu-id="b2676-108">maxConcurrentCalls</span></span>|<span data-ttu-id="b2676-109">Dodatnia liczba całkowita, która ogranicza liczbę komunikatów przetwarzanych obecnie w ramach <xref:System.ServiceModel.ServiceHost> .</span><span class="sxs-lookup"><span data-stu-id="b2676-109">A positive integer that limits the number of messages that currently process across a <xref:System.ServiceModel.ServiceHost>.</span></span> <span data-ttu-id="b2676-110">Wywołania przekraczające limit są umieszczane w kolejce.</span><span class="sxs-lookup"><span data-stu-id="b2676-110">Calls in excess of the limit are queued.</span></span> <span data-ttu-id="b2676-111">Ustawienie tej wartości na 0 jest równoznaczne z ustawieniem wartość Int32. MaxValue.</span><span class="sxs-lookup"><span data-stu-id="b2676-111">Setting this value to 0 is equivalent to setting it to Int32.MaxValue.</span></span> <span data-ttu-id="b2676-112">Wartość domyślna to 16 \* liczba procesorów.</span><span class="sxs-lookup"><span data-stu-id="b2676-112">The default is 16 \* processor count.</span></span>|  
|<span data-ttu-id="b2676-113">maxConcurrentInstances</span><span class="sxs-lookup"><span data-stu-id="b2676-113">maxConcurrentInstances</span></span>|<span data-ttu-id="b2676-114">Dodatnia liczba całkowita, która ogranicza liczbę <xref:System.ServiceModel.InstanceContext> obiektów, które są wykonywane jednocześnie w czasie <xref:System.ServiceModel.ServiceHost> .</span><span class="sxs-lookup"><span data-stu-id="b2676-114">A positive integer that limits the number of <xref:System.ServiceModel.InstanceContext> objects that execute at one time across a <xref:System.ServiceModel.ServiceHost>.</span></span> <span data-ttu-id="b2676-115">Żądania utworzenia dodatkowych wystąpień są umieszczane w kolejce i uzupełniane, gdy zostanie udostępnione miejsce poniżej limitu.</span><span class="sxs-lookup"><span data-stu-id="b2676-115">Requests to create additional instances are queued and complete when a slot below the limit becomes available.</span></span> <span data-ttu-id="b2676-116">Wartość domyślna to suma wartości maxConcurrentSessions i MaxConcurrentCalls</span><span class="sxs-lookup"><span data-stu-id="b2676-116">The default is the sum of maxConcurrentSessions and MaxConcurrentCalls</span></span>|  
|<span data-ttu-id="b2676-117">maxConcurrentSessions</span><span class="sxs-lookup"><span data-stu-id="b2676-117">maxConcurrentSessions</span></span>|<span data-ttu-id="b2676-118">Dodatnia liczba całkowita, która ogranicza liczbę sesji <xref:System.ServiceModel.ServiceHost> akceptowanych przez obiekt.</span><span class="sxs-lookup"><span data-stu-id="b2676-118">A positive integer that limits the number of sessions a <xref:System.ServiceModel.ServiceHost> object can accept.</span></span><br /><br /> <span data-ttu-id="b2676-119">Usługa będzie akceptować połączenia o przekroczeniu limitu, ale tylko kanały poniżej limitu są aktywne (komunikaty są odczytywane z kanału).</span><span class="sxs-lookup"><span data-stu-id="b2676-119">The service will accept connections in excess of the limit, but only the channels below the limit are active (messages are read from the channel).</span></span> <span data-ttu-id="b2676-120">Ustawienie tej wartości na 0 jest równoznaczne z ustawieniem wartość Int32. MaxValue.</span><span class="sxs-lookup"><span data-stu-id="b2676-120">Setting this value to 0 is equivalent to setting it to Int32.MaxValue.</span></span> <span data-ttu-id="b2676-121">Wartość domyślna to 100 \* liczba procesorów.</span><span class="sxs-lookup"><span data-stu-id="b2676-121">The default is 100 \* processor count.</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="b2676-122">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="b2676-122">Child Elements</span></span>  

 <span data-ttu-id="b2676-123">Brak.</span><span class="sxs-lookup"><span data-stu-id="b2676-123">None.</span></span>  
  
### <a name="parent-elements"></a><span data-ttu-id="b2676-124">Elementy nadrzędne</span><span class="sxs-lookup"><span data-stu-id="b2676-124">Parent Elements</span></span>  
  
|<span data-ttu-id="b2676-125">Element</span><span class="sxs-lookup"><span data-stu-id="b2676-125">Element</span></span>|<span data-ttu-id="b2676-126">Opis</span><span class="sxs-lookup"><span data-stu-id="b2676-126">Description</span></span>|  
|-------------|-----------------|  
|[\<behavior>](behavior-of-endpointbehaviors.md)|<span data-ttu-id="b2676-127">Określa zachowanie elementu.</span><span class="sxs-lookup"><span data-stu-id="b2676-127">Specifies a behavior element.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="b2676-128">Uwagi</span><span class="sxs-lookup"><span data-stu-id="b2676-128">Remarks</span></span>  

 <span data-ttu-id="b2676-129">Kontrolki ograniczania nakładają limity liczby współbieżnych wywołań, wystąpień lub sesji, aby zapobiec nadmiernemu zużyciu zasobów.</span><span class="sxs-lookup"><span data-stu-id="b2676-129">Throttling controls place limits on the number of concurrent calls, instances, or sessions to prevent over-consumption of resources.</span></span>  
  
 <span data-ttu-id="b2676-130">Ślad jest zapisywana za każdym razem, gdy wartość atrybutu zostanie osiągnięta.</span><span class="sxs-lookup"><span data-stu-id="b2676-130">A trace is written every time the value of attributes is reached.</span></span> <span data-ttu-id="b2676-131">Pierwszy ślad jest zapisywana jako ostrzeżenie.</span><span class="sxs-lookup"><span data-stu-id="b2676-131">The first trace is written as a warning.</span></span>  
  
## <a name="example"></a><span data-ttu-id="b2676-132">Przykład</span><span class="sxs-lookup"><span data-stu-id="b2676-132">Example</span></span>  

 <span data-ttu-id="b2676-133">Poniższy przykład konfiguracji określa, że usługa ogranicza maksymalną liczbę współbieżnych wywołań do 2, a maksymalna liczba równoczesnych wystąpień do 10.</span><span class="sxs-lookup"><span data-stu-id="b2676-133">The following configuration example specifies that the service limits the maximum concurrent calls to 2, and the maximum number of concurrent instances to 10.</span></span> <span data-ttu-id="b2676-134">Aby zapoznać się z szczegółowym przykładem uruchamiania tego przykładu, zobacz [ograniczanie przepustowości](../../../wcf/samples/throttling.md).</span><span class="sxs-lookup"><span data-stu-id="b2676-134">For a detailed example of running this example, see [Throttling](../../../wcf/samples/throttling.md).</span></span>  
  
```xml  
<behaviors>
  <serviceBehaviors>
    <behavior name="CalculatorServiceBehavior">
      <serviceDebug includeExceptionDetailInFaults="False" />
      <serviceMetadata httpGetEnabled="True" />
      <!-- Specify throttling behavior -->
      <serviceThrottling maxConcurrentCalls="2"
                         maxConcurrentInstances="10" />
    </behavior>
  </serviceBehaviors>
</behaviors>
```  
  
## <a name="see-also"></a><span data-ttu-id="b2676-135">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="b2676-135">See also</span></span>

- <xref:System.ServiceModel.Description.ServiceThrottlingBehavior>
- <xref:System.ServiceModel.Configuration.ServiceThrottlingElement>
- [<span data-ttu-id="b2676-136">Używanie elementu ServiceThrottlingBehavior do kontrolowania wydajności programu WCF</span><span class="sxs-lookup"><span data-stu-id="b2676-136">Using ServiceThrottlingBehavior to Control WCF Service Performance</span></span>](../../../wcf/feature-details/using-servicethrottlingbehavior-to-control-wcf-service-performance.md)
