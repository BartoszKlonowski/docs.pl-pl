---
title: 'Instrukcje: sprawdzanie lub modyfikowanie parametrów'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: ab6c0ac7-aac4-45ba-93d6-a0e9afd1756f
ms.openlocfilehash: e8b2674d8efc0ef3ac2f1dd6ab0df559195c274c
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96249036"
---
# <a name="how-to-inspect-or-modify-parameters"></a><span data-ttu-id="bc297-102">Instrukcje: sprawdzanie lub modyfikowanie parametrów</span><span class="sxs-lookup"><span data-stu-id="bc297-102">How to: Inspect or Modify Parameters</span></span>

<span data-ttu-id="bc297-103">Możesz sprawdzić lub zmodyfikować przychodzące lub wychodzące komunikaty dla pojedynczej operacji na obiekcie klienta Windows Communication Foundation (WCF) lub w usłudze WCF, implementując <xref:System.ServiceModel.Dispatcher.IParameterInspector?displayProperty=nameWithType> interfejs i wstawiając go do środowiska uruchomieniowego klienta lub usługi.</span><span class="sxs-lookup"><span data-stu-id="bc297-103">You can inspect or modify the incoming or outgoing messages for a single operation on a Windows Communication Foundation (WCF) client object or a WCF service by implementing the <xref:System.ServiceModel.Dispatcher.IParameterInspector?displayProperty=nameWithType> interface and inserting it into the client or service runtime.</span></span> <span data-ttu-id="bc297-104">Zwykle zachowanie operacji służy do dodawania inspektorów parametrów dla jednej operacji; Inne zachowania mogą służyć do zapewnienia łatwego dostępu do środowiska uruchomieniowego w większym zakresie.</span><span class="sxs-lookup"><span data-stu-id="bc297-104">Typically an operation behavior is used to add parameter inspectors for a single operation; other behaviors can be used to provide easy access to the runtime at a greater scope.</span></span> <span data-ttu-id="bc297-105">Aby uzyskać więcej informacji, zobacz [Rozszerzanie klientów](extending-clients.md) i [rozszerzanie dyspozytorów](extending-dispatchers.md).</span><span class="sxs-lookup"><span data-stu-id="bc297-105">For more information, see [Extending Clients](extending-clients.md) and [Extending Dispatchers](extending-dispatchers.md).</span></span>  
  
### <a name="inspecting-or-modifying-parameters"></a><span data-ttu-id="bc297-106">Inspekcja lub modyfikowanie parametrów</span><span class="sxs-lookup"><span data-stu-id="bc297-106">Inspecting or Modifying Parameters</span></span>  
  
1. <span data-ttu-id="bc297-107">Zaimplementuj interfejs <xref:System.ServiceModel.Dispatcher.IParameterInspector?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="bc297-107">Implement the <xref:System.ServiceModel.Dispatcher.IParameterInspector?displayProperty=nameWithType> interface.</span></span>  
  
2. <span data-ttu-id="bc297-108">Zaimplementuj <xref:System.ServiceModel.Description.IOperationBehavior?displayProperty=nameWithType> , <xref:System.ServiceModel.Description.IEndpointBehavior?displayProperty=nameWithType> , <xref:System.ServiceModel.Description.IServiceBehavior?displayProperty=nameWithType> lub <xref:System.ServiceModel.Description.IContractBehavior?displayProperty=nameWithType> (w zależności od wymaganego zakresu), aby dodać Inspektor parametrów do <xref:System.ServiceModel.Dispatcher.ClientOperation.ParameterInspectors%2A?displayProperty=nameWithType> <xref:System.ServiceModel.Dispatcher.DispatchOperation.ParameterInspectors%2A?displayProperty=nameWithType> właściwości lub.</span><span class="sxs-lookup"><span data-stu-id="bc297-108">Implement a <xref:System.ServiceModel.Description.IOperationBehavior?displayProperty=nameWithType>, <xref:System.ServiceModel.Description.IEndpointBehavior?displayProperty=nameWithType>, <xref:System.ServiceModel.Description.IServiceBehavior?displayProperty=nameWithType> or <xref:System.ServiceModel.Description.IContractBehavior?displayProperty=nameWithType> (depending upon the required scope) to add your parameter inspector to either the <xref:System.ServiceModel.Dispatcher.ClientOperation.ParameterInspectors%2A?displayProperty=nameWithType> or <xref:System.ServiceModel.Dispatcher.DispatchOperation.ParameterInspectors%2A?displayProperty=nameWithType> properties.</span></span>  
  
3. <span data-ttu-id="bc297-109">Wstaw zachowanie przed wywołaniem <xref:System.ServiceModel.ClientBase%601.Open%2A?displayProperty=nameWithType> lub <xref:System.ServiceModel.ICommunicationObject.Open%2A?displayProperty=nameWithType> metodą w <xref:System.ServiceModel.ChannelFactory%601?displayProperty=nameWithType> .</span><span class="sxs-lookup"><span data-stu-id="bc297-109">Insert your behavior prior to calling <xref:System.ServiceModel.ClientBase%601.Open%2A?displayProperty=nameWithType> or the <xref:System.ServiceModel.ICommunicationObject.Open%2A?displayProperty=nameWithType> method on the <xref:System.ServiceModel.ChannelFactory%601?displayProperty=nameWithType>.</span></span> <span data-ttu-id="bc297-110">Aby uzyskać szczegółowe informacje, zobacz [Konfigurowanie i rozszerzanie środowiska uruchomieniowego za pomocą zachowań](configuring-and-extending-the-runtime-with-behaviors.md).</span><span class="sxs-lookup"><span data-stu-id="bc297-110">For details, see [Configuring and Extending the Runtime with Behaviors](configuring-and-extending-the-runtime-with-behaviors.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="bc297-111">Przykład</span><span class="sxs-lookup"><span data-stu-id="bc297-111">Example</span></span>  

 <span data-ttu-id="bc297-112">Poniższy przykład kodu pokazuje, w kolejności:</span><span class="sxs-lookup"><span data-stu-id="bc297-112">The following code examples show, in order:</span></span>  
  
- <span data-ttu-id="bc297-113">Implementacja inspektora parametrów.</span><span class="sxs-lookup"><span data-stu-id="bc297-113">A parameter inspector implementation.</span></span>  
  
- <span data-ttu-id="bc297-114">Implementacja zachowania, która wstawia Inspektor parametrów przy użyciu <xref:System.ServiceModel.Description.IOperationBehavior?displayProperty=nameWithType> , <xref:System.ServiceModel.Description.IEndpointBehavior?displayProperty=nameWithType> i <xref:System.ServiceModel.Description.IServiceBehavior?displayProperty=nameWithType> .</span><span class="sxs-lookup"><span data-stu-id="bc297-114">The behavior implementation that inserts the parameter inspector using a <xref:System.ServiceModel.Description.IOperationBehavior?displayProperty=nameWithType>, <xref:System.ServiceModel.Description.IEndpointBehavior?displayProperty=nameWithType>, and an <xref:System.ServiceModel.Description.IServiceBehavior?displayProperty=nameWithType>.</span></span>  
  
- <span data-ttu-id="bc297-115">Plik konfiguracji, który ładuje i uruchamia zachowanie punktu końcowego w aplikacji klienckiej w celu wstawienia inspektora parametrów na kliencie.</span><span class="sxs-lookup"><span data-stu-id="bc297-115">A configuration file that loads and runs the endpoint behavior in a client application to insert the parameter inspector on the client.</span></span>  
  
 [!code-csharp[Interceptors#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/interceptors/cs/interceptors.cs#4)]
 [!code-vb[Interceptors#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/interceptors/vb/interceptors.vb#4)]  
  
 [!code-csharp[Interceptors#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/interceptors/cs/insertingbehaviors.cs#5)]
 [!code-vb[Interceptors#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/interceptors/vb/insertingbehaviors.vb#5)]  
  
 [!code-xml[Interceptors#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/interceptors/cs/client.exe.config#3)]  
  
## <a name="see-also"></a><span data-ttu-id="bc297-116">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="bc297-116">See also</span></span>

- [<span data-ttu-id="bc297-117">Konfigurowanie i rozszerzanie środowiska uruchomieniowego za pomocą zachowań</span><span class="sxs-lookup"><span data-stu-id="bc297-117">Configuring and Extending the Runtime with Behaviors</span></span>](configuring-and-extending-the-runtime-with-behaviors.md)
