---
title: Używanie kontraktów w przepływie pracy
ms.date: 03/30/2017
ms.assetid: 939c64e9-e7cc-4abc-b41e-27cfce1d7e50
ms.openlocfilehash: e32130395e05a56de081620f82e0e6f72ae0db38
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96289623"
---
# <a name="using-contracts-in-workflow"></a><span data-ttu-id="e825a-102">Używanie kontraktów w przepływie pracy</span><span class="sxs-lookup"><span data-stu-id="e825a-102">Using Contracts in Workflow</span></span>

<span data-ttu-id="e825a-103">Podczas implementowania usługi należy zdefiniować kilka kontraktów, które opisują usługę i dane wysyłane i odbierane.</span><span class="sxs-lookup"><span data-stu-id="e825a-103">When implementing a service, you define a number of contracts that describe the service and the data that it sends and receives.</span></span> <span data-ttu-id="e825a-104">Dane są reprezentowane jako Kontrakty danych i umowy dotyczące komunikatów; usługi WCF i Workflow Services korzystają z kontraktów danych i definicji kontraktu komunikatów w ramach opisów usług.</span><span class="sxs-lookup"><span data-stu-id="e825a-104">The data is represented as data contracts and message contracts; both WCF and workflow services use data contract and message contract definitions as part of service descriptions.</span></span> <span data-ttu-id="e825a-105">Sama usługa ujawnia metadane (w formie WSDL) w celu opisania operacji usługi.</span><span class="sxs-lookup"><span data-stu-id="e825a-105">The service itself exposes metadata (in the form of WSDL) in order to describe the operations of the service.</span></span> <span data-ttu-id="e825a-106">W programie WCF kontrakty usług i kontrakty operacji definiują usługę i obsługiwane przez nią operacje.</span><span class="sxs-lookup"><span data-stu-id="e825a-106">In WCF, service contracts and operation contracts define the service and the operations it supports.</span></span> <span data-ttu-id="e825a-107">Jednak w usłudze przepływu pracy te kontrakty są częścią procesu biznesowego. są one ujawniane w metadanych przez proces o nazwie wnioskowanie kontraktu.</span><span class="sxs-lookup"><span data-stu-id="e825a-107">However, in a workflow service, these contracts are part of the business process itself; they are exposed in metadata by a process called contract inference.</span></span>  
  
## <a name="contract-inference"></a><span data-ttu-id="e825a-108">Wnioskowanie o kontrakcie</span><span class="sxs-lookup"><span data-stu-id="e825a-108">Contract Inference</span></span>  

 <span data-ttu-id="e825a-109">Gdy usługa przepływu pracy jest hostowana przy użyciu <xref:System.ServiceModel.Activities.WorkflowServiceHost> , sprawdzana jest definicja przepływu pracy i jest generowana umowa oparta na zestawie działań obsługi komunikatów znalezionych w przepływie pracy.</span><span class="sxs-lookup"><span data-stu-id="e825a-109">When a workflow service is hosted using <xref:System.ServiceModel.Activities.WorkflowServiceHost>, the workflow definition is examined and a contract is generated based on the set of messaging activities found in the workflow.</span></span> <span data-ttu-id="e825a-110">W szczególności następujące działania i właściwości są używane do generowania kontraktu:</span><span class="sxs-lookup"><span data-stu-id="e825a-110">In particular the following activities and properties are used to generate the contract:</span></span>  
  
 <span data-ttu-id="e825a-111"><xref:System.ServiceModel.Activities.Receive> Interakcyjn</span><span class="sxs-lookup"><span data-stu-id="e825a-111"><xref:System.ServiceModel.Activities.Receive> Activity</span></span>  
  
- <xref:System.ServiceModel.Activities.Receive.ServiceContractName%2A>  
  
- <xref:System.ServiceModel.Activities.Receive.OperationName%2A>
  
- <xref:System.ServiceModel.Activities.Receive.Action%2A>

 <span data-ttu-id="e825a-112"><xref:System.ServiceModel.Activities.SendReply> Interakcyjn</span><span class="sxs-lookup"><span data-stu-id="e825a-112"><xref:System.ServiceModel.Activities.SendReply> Activity</span></span>  
  
- <xref:System.ServiceModel.Activities.SendReply.Action%2A>  
  
 <span data-ttu-id="e825a-113"><xref:System.ServiceModel.Activities.TransactedReceiveScope> Interakcyjn</span><span class="sxs-lookup"><span data-stu-id="e825a-113"><xref:System.ServiceModel.Activities.TransactedReceiveScope> Activity</span></span>  
  
 <span data-ttu-id="e825a-114">Końcowy wynik wnioskowania o umowę to opis usługi przy użyciu tych samych struktur danych co usługa WCF i kontrakty operacji.</span><span class="sxs-lookup"><span data-stu-id="e825a-114">The end result of contract inference is a description of the service using the same data structures as WCF service and operation contracts.</span></span> <span data-ttu-id="e825a-115">Te informacje są następnie używane w celu udostępnienia WSDL dla usługi przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="e825a-115">This information is then used to expose WSDL for the workflow service.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="e825a-116">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="e825a-116">See also</span></span>

- [<span data-ttu-id="e825a-117">Usługi przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="e825a-117">Workflow Services</span></span>](workflow-services.md)
- [<span data-ttu-id="e825a-118">Działania dotyczące komunikatów</span><span class="sxs-lookup"><span data-stu-id="e825a-118">Messaging Activities</span></span>](messaging-activities.md)
- [<span data-ttu-id="e825a-119">Instrukcje: Tworzenie usługi przepływu pracy przy użyciu działań dotyczących komunikatów</span><span class="sxs-lookup"><span data-stu-id="e825a-119">How to: Create a Workflow Service with Messaging Activities</span></span>](how-to-create-a-workflow-service-with-messaging-activities.md)
- [<span data-ttu-id="e825a-120">Instrukcje: Tworzenie usługi przepływu pracy wykorzystującej istniejący kontrakt usługi</span><span class="sxs-lookup"><span data-stu-id="e825a-120">How to: Create a workflow service that consumes an existing service contract</span></span>](../../windows-workflow-foundation/how-to-create-a-workflow-service-that-consumes-an-existing-service-contract.md)
