---
title: Trwałość przepływu pracy
description: .NET Framework 4.6.1 zawiera klasę obiekt SqlWorkflowInstanceStore, która umożliwia trwałość danych przepływu pracy i metadanych w SQL Server bazie danych.
ms.date: 03/30/2017
helpviewer_keywords:
- programming [WF], persistence
ms.assetid: 39e69d1f-b771-4c16-9e18-696fa43b65b2
ms.openlocfilehash: 2184a159423a611a8936e900591a480ce7ef6ec8
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96293809"
---
# <a name="workflow-persistence"></a><span data-ttu-id="c03c8-103">Trwałość przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="c03c8-103">Workflow Persistence</span></span>

<span data-ttu-id="c03c8-104">Trwałość przepływu pracy to trwałe Przechwytywanie stanu wystąpienia przepływu pracy niezależnie od informacji o procesie lub komputerze.</span><span class="sxs-lookup"><span data-stu-id="c03c8-104">Workflow persistence is the durable capture of a workflow instance's state, independent of process or computer information.</span></span> <span data-ttu-id="c03c8-105">W tym celu należy zapewnić dobrze znany punkt odzyskiwania wystąpienia przepływu pracy w przypadku awarii systemu lub zachować pamięć, zwalniając wystąpienia przepływu pracy, które nie działają aktywnie, lub przenieść stan wystąpienia przepływu pracy z jednego węzła do innego w węźle farmy serwerów.</span><span class="sxs-lookup"><span data-stu-id="c03c8-105">This is done to provide a well-known point of recovery for the workflow instance in the event of system failure, or to preserve memory by unloading workflow instances that are not actively doing work, or to move the state of the workflow instance from one node to another node in a server farm.</span></span>  
  
 <span data-ttu-id="c03c8-106">Trwałość umożliwia elastyczność procesów, skalowalność, odzyskiwanie w miarę awarii oraz możliwość bardziej wydajnego zarządzania pamięcią.</span><span class="sxs-lookup"><span data-stu-id="c03c8-106">Persistence enables process agility, scalability, recovery in the face of failure, and the ability to manage memory more efficiently.</span></span> <span data-ttu-id="c03c8-107">Proces trwałości obejmuje identyfikację punktu trwałości, zbieranie danych do zapisania, a wreszcie delegowanie rzeczywistego magazynu danych do dostawcy trwałości.</span><span class="sxs-lookup"><span data-stu-id="c03c8-107">The persistence process includes the identification of a persistence point, the gathering of the data to be saved, and finally the delegation of the actual storage of the data to a persistence provider.</span></span>  
  
 <span data-ttu-id="c03c8-108">Aby włączyć trwałość dla przepływu pracy, należy skojarzyć magazyn wystąpień z obiektem **WorkflowApplication** lub **WorkflowServiceHost** , jak wspomniano w [instrukcje: Włączanie trwałości dla przepływów pracy i usług przepływu pracy](how-to-enable-persistence-for-workflows-and-workflow-services.md).</span><span class="sxs-lookup"><span data-stu-id="c03c8-108">To enable persistence for a workflow, you need to associate an instance store with the **WorkflowApplication** or **WorkflowServiceHost** as mentioned in [How to: Enable Persistence for Workflows and Workflow Services](how-to-enable-persistence-for-workflows-and-workflow-services.md).</span></span> <span data-ttu-id="c03c8-109">Obiekty **WorkflowApplication** i **WorkflowServiceHost** używają magazynu wystąpień skojarzonego z nimi w celu włączenia utrwalania wystąpień przepływu pracy do magazynu trwałości i ładowania wystąpień przepływu pracy do pamięci na podstawie danych wystąpienia przepływu pracy przechowywanych w magazynie trwałości.</span><span class="sxs-lookup"><span data-stu-id="c03c8-109">The **WorkflowApplication** and **WorkflowServiceHost** use the instance store associated with them to enable persisting workflow instances into a persistence store and loading workflow instances into memory based on the workflow instance data stored in the persistence store.</span></span>  
  
 <span data-ttu-id="c03c8-110">[!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)]Dostarcza z klasą **obiekt SqlWorkflowInstanceStore** , która umożliwia trwałość danych i metadanych o wystąpieniach przepływu pracy w bazie danych SQL Server 2005 lub SQL Server 2008.</span><span class="sxs-lookup"><span data-stu-id="c03c8-110">The [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] ships with the **SqlWorkflowInstanceStore** class, which allows persistence of data and metadata about workflow instances into a SQL Server 2005 or SQL Server 2008 database.</span></span> <span data-ttu-id="c03c8-111">Aby uzyskać więcej informacji, zobacz [Magazyn wystąpień przepływu pracy SQL](sql-workflow-instance-store.md) .</span><span class="sxs-lookup"><span data-stu-id="c03c8-111">See [SQL Workflow Instance Store](sql-workflow-instance-store.md) for more details.</span></span>  
  
 <span data-ttu-id="c03c8-112">Aby przechowywać i ładować dane specyficzne dla aplikacji wraz z informacjami związanymi z wystąpieniem przepływu pracy, można utworzyć uczestników trwałości rozszerzających <xref:System.Activities.Persistence.PersistenceParticipant> klasę.</span><span class="sxs-lookup"><span data-stu-id="c03c8-112">To store and load your application-specific data along with the workflow instance-related information, you can create persistence participants that extend the <xref:System.Activities.Persistence.PersistenceParticipant> class.</span></span> <span data-ttu-id="c03c8-113">Uczestnik trwałości uczestniczy w procesie trwałości w celu zapisania niestandardowych danych, które można serializować do magazynu trwałości, do załadowania danych z magazynu wystąpień do pamięci oraz do wykonania dodatkowej logiki w ramach transakcji trwałości.</span><span class="sxs-lookup"><span data-stu-id="c03c8-113">A persistence participant participates in the persistence process to save custom serializable data into the persistence store, to load the data from the instance store into memory, and to perform any additional logic under a persistence transaction.</span></span> <span data-ttu-id="c03c8-114">Aby uzyskać więcej informacji, zobacz temat [trwałość uczestników](persistence-participants.md).</span><span class="sxs-lookup"><span data-stu-id="c03c8-114">For more information, see [Persistence Participants](persistence-participants.md).</span></span>  
  
 <span data-ttu-id="c03c8-115">Sieć szkieletowa aplikacji systemu Windows Server upraszcza proces konfigurowania trwałości.</span><span class="sxs-lookup"><span data-stu-id="c03c8-115">Windows Server App Fabric simplifies the process of configuring persistence.</span></span> <span data-ttu-id="c03c8-116">Aby uzyskać więcej informacji, zobacz [pojęcia dotyczące trwałości przy użyciu sieci szkieletowej aplikacji systemu Windows Server](/previous-versions/appfabric/ee677272(v=azure.10))</span><span class="sxs-lookup"><span data-stu-id="c03c8-116">For more information, see [Persistence Concepts with Windows Server App Fabric](/previous-versions/appfabric/ee677272(v=azure.10))</span></span>  
  
## <a name="implicit-persistence-points"></a><span data-ttu-id="c03c8-117">Niejawne punkty trwałości</span><span class="sxs-lookup"><span data-stu-id="c03c8-117">Implicit Persistence Points</span></span>  

 <span data-ttu-id="c03c8-118">Poniższa lista zawiera przykłady warunków, na których przepływ pracy jest utrwalany, gdy magazyn wystąpień jest skojarzony z przepływem pracy.</span><span class="sxs-lookup"><span data-stu-id="c03c8-118">The following list contains examples of the conditions upon which a workflow is persisted when an instance store is associated with a workflow.</span></span>  
  
- <span data-ttu-id="c03c8-119">Po zakończeniu działania elementu **TransactionScope** lub zakończeniu działania **TransactedReceiveScope** .</span><span class="sxs-lookup"><span data-stu-id="c03c8-119">When a **TransactionScope** activity completes or a **TransactedReceiveScope** activity completes.</span></span>  
  
- <span data-ttu-id="c03c8-120">Gdy wystąpienie przepływu pracy stanie się bezczynna, a **WorkflowIdleBehavior** jest ustawiony na hoście przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="c03c8-120">When a workflow instance becomes idle and the **WorkflowIdleBehavior** is set on workflow host.</span></span> <span data-ttu-id="c03c8-121">Dzieje się tak na przykład wtedy, gdy używane są działania dotyczące komunikatów lub **opóźnienia** .</span><span class="sxs-lookup"><span data-stu-id="c03c8-121">This occurs, for example, when you use messaging activities or a **Delay** activity.</span></span>  
  
- <span data-ttu-id="c03c8-122">Gdy obiekt WorkflowApplication stanie się bezczynny, a właściwość **PersistableIdle** aplikacji jest ustawiona na **PersistableIdleAction. utrwalanie**.</span><span class="sxs-lookup"><span data-stu-id="c03c8-122">When a WorkflowApplication becomes idle and the **PersistableIdle** property of the application is set to **PersistableIdleAction.Persist**.</span></span>  
  
- <span data-ttu-id="c03c8-123">Gdy aplikacja hosta nakazuje utrwalenie lub zwolnienie wystąpienia przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="c03c8-123">When a host application is instructed to persist or unload a workflow instance.</span></span>  
  
- <span data-ttu-id="c03c8-124">Po przerwaniu lub zakończeniu wystąpienia przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="c03c8-124">When a workflow instance is terminated or finishes.</span></span>  
  
- <span data-ttu-id="c03c8-125">Gdy działanie **utrwalania** jest wykonywane.</span><span class="sxs-lookup"><span data-stu-id="c03c8-125">When a **Persist** activity executes.</span></span>  
  
- <span data-ttu-id="c03c8-126">Gdy wystąpienie przepływu pracy utworzone przy użyciu poprzedniej wersji Windows Workflow Foundation napotka punkt trwałości podczas wykonywania międzyoperacyjnego.</span><span class="sxs-lookup"><span data-stu-id="c03c8-126">When an instance of a workflow developed using a previous version of Windows Workflow Foundation encounters a persistence point during interoperable execution.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="c03c8-127">W tej sekcji</span><span class="sxs-lookup"><span data-stu-id="c03c8-127">In This Section</span></span>  
  
- [<span data-ttu-id="c03c8-128">Magazyn wystąpień przepływu pracy SQL</span><span class="sxs-lookup"><span data-stu-id="c03c8-128">SQL Workflow Instance Store</span></span>](sql-workflow-instance-store.md)  
  
- [<span data-ttu-id="c03c8-129">Magazyny wystąpień</span><span class="sxs-lookup"><span data-stu-id="c03c8-129">Instance Stores</span></span>](instance-stores.md)  
  
- [<span data-ttu-id="c03c8-130">Uczestnicy stanów trwałych</span><span class="sxs-lookup"><span data-stu-id="c03c8-130">Persistence Participants</span></span>](persistence-participants.md)  
  
- [<span data-ttu-id="c03c8-131">Najlepsze rozwiązania w zakresie stanów trwałych</span><span class="sxs-lookup"><span data-stu-id="c03c8-131">Persistence Best Practices</span></span>](persistence-best-practices.md)  
  
- [<span data-ttu-id="c03c8-132">Nietrwałe wystąpienia przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="c03c8-132">Non-Persisted Workflow Instances</span></span>](non-persisted-workflow-instances.md)  
  
- [<span data-ttu-id="c03c8-133">Wstrzymywanie i wznawianie przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="c03c8-133">Pausing and Resuming a Workflow</span></span>](pausing-and-resuming-a-workflow.md)
