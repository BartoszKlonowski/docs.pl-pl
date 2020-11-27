---
title: 'Instrukcje: konfigurowanie zachowania dotyczącego nieobsługiwanego wyjątku przepływu pracy przy użyciu klasy WorkflowServiceHost'
ms.date: 03/30/2017
ms.assetid: 51b25c86-292c-43e4-8d13-273d2badc8ad
ms.openlocfilehash: 93eb2f4493b70f54336a5d47957c6913239088e5
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96264858"
---
# <a name="how-to-configure-workflow-unhandled-exception-behavior-with-workflowservicehost"></a><span data-ttu-id="b95f9-102">Instrukcje: konfigurowanie zachowania dotyczącego nieobsługiwanego wyjątku przepływu pracy przy użyciu klasy WorkflowServiceHost</span><span class="sxs-lookup"><span data-stu-id="b95f9-102">How to: Configure Workflow Unhandled Exception Behavior with WorkflowServiceHost</span></span>

<span data-ttu-id="b95f9-103"><xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior>Jest zachowanie, które pozwala określić akcję do wykonania, jeśli wystąpi nieobsługiwany wyjątek w przepływie pracy hostowanym w <xref:System.ServiceModel.Activities.WorkflowServiceHost> .</span><span class="sxs-lookup"><span data-stu-id="b95f9-103">The <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior> is a behavior that enables you to specify the action to take if an unhandled exception occurs within a workflow hosted in <xref:System.ServiceModel.Activities.WorkflowServiceHost>.</span></span> <span data-ttu-id="b95f9-104">W tym temacie opisano sposób konfigurowania tego zachowania w pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="b95f9-104">This topic shows how to configure this behavior in a configuration file.</span></span>  
  
### <a name="to-configure-workflowunhandledexceptionbehavior"></a><span data-ttu-id="b95f9-105">Aby skonfigurować WorkflowUnhandledExceptionBehavior</span><span class="sxs-lookup"><span data-stu-id="b95f9-105">To configure WorkflowUnhandledExceptionBehavior</span></span>  
  
1. <span data-ttu-id="b95f9-106">Dodaj element <`workflowUnhandledException`> w elemencie <> w elemencie `behavior` <`serviceBehaviors`>, używając `action` atrybutu, aby określić akcję wykonywaną po wystąpieniu nieobsługiwanego wyjątku, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="b95f9-106">Add a <`workflowUnhandledException`> element in a <`behavior`> element within a <`serviceBehaviors`> element, using the `action` attribute to specify the action to take when an unhandled exception occurs as shown in the following example.</span></span>  
  
    ```xml  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="">  
          <workflowUnhandledException action="abandonAndSuspend"/>
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
    ```  
  
    > [!NOTE]
    > <span data-ttu-id="b95f9-107">Poprzedni przykład konfiguracji używa uproszczonej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="b95f9-107">The preceding configuration sample is using simplified configuration.</span></span> <span data-ttu-id="b95f9-108">Aby uzyskać więcej informacji, zobacz [Uproszczona konfiguracja](../simplified-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="b95f9-108">For more information, see [Simplified Configuration](../simplified-configuration.md).</span></span>  
  
     <span data-ttu-id="b95f9-109">Takie zachowanie można skonfigurować w kodzie, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="b95f9-109">This behavior can be configured in code as shown in the following example.</span></span>  
  
    ```csharp  
    host.Description.Behaviors.Add(new WorkflowUnhandledExceptionBehavior { Action = WorkflowUnhandledExceptionAction.AbandonAndSuspend });  
    ```  
  
     <span data-ttu-id="b95f9-110">`action`Atrybut <`workflowUnhandledException` elementu> można ustawić na jedną z następujących wartości:</span><span class="sxs-lookup"><span data-stu-id="b95f9-110">The `action` attribute of the <`workflowUnhandledException`> element can be set to one of the following values:</span></span>  
  
     <span data-ttu-id="b95f9-111">**rzucić**</span><span class="sxs-lookup"><span data-stu-id="b95f9-111">**abandon**</span></span>  
     <span data-ttu-id="b95f9-112">Przerywa wystąpienie w pamięci bez dotykania utrwalonego stanu wystąpienia (oznacza to, że wraca do ostatniego punktu utrwalania).</span><span class="sxs-lookup"><span data-stu-id="b95f9-112">Aborts the instance in memory without touching the persisted instance state (that is, roll back to the last persist point).</span></span>  
  
     <span data-ttu-id="b95f9-113">**abandonAndSuspend**</span><span class="sxs-lookup"><span data-stu-id="b95f9-113">**abandonAndSuspend**</span></span>  
     <span data-ttu-id="b95f9-114">Przerywa wystąpienie w pamięci i aktualizuje wystąpienie trwałe, które zostanie zawieszone.</span><span class="sxs-lookup"><span data-stu-id="b95f9-114">Aborts the instance in memory and updates the persisted instance to be suspended.</span></span>  
  
     <span data-ttu-id="b95f9-115">**Anuluj**</span><span class="sxs-lookup"><span data-stu-id="b95f9-115">**cancel**</span></span>  
     <span data-ttu-id="b95f9-116">Wywołuje programy obsługi anulowania dla wystąpienia, a następnie kończy wystąpienie w pamięci, co może również usunąć je z magazynu wystąpień</span><span class="sxs-lookup"><span data-stu-id="b95f9-116">Calls cancellation handlers for the instance and then completes the instance in memory, which may also remove it from the instance store</span></span>  
  
     <span data-ttu-id="b95f9-117">**kończyć**</span><span class="sxs-lookup"><span data-stu-id="b95f9-117">**terminate**</span></span>  
     <span data-ttu-id="b95f9-118">Kończy wystąpienie w pamięci i usuwa je z magazynu wystąpień.</span><span class="sxs-lookup"><span data-stu-id="b95f9-118">Completes the instance in memory and removes it from the instance store.</span></span>  
  
     <span data-ttu-id="b95f9-119">Aby uzyskać więcej informacji na temat <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior> , zobacz [Rozszerzalność hosta usługi przepływu pracy](workflow-service-host-extensibility.md).</span><span class="sxs-lookup"><span data-stu-id="b95f9-119">For more information about <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior>, see [Workflow Service Host Extensibility](workflow-service-host-extensibility.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="b95f9-120">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="b95f9-120">See also</span></span>

- [<span data-ttu-id="b95f9-121">Rozszerzalność hosta usługi przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="b95f9-121">Workflow Service Host Extensibility</span></span>](workflow-service-host-extensibility.md)
- [<span data-ttu-id="b95f9-122">Usługi przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="b95f9-122">Workflow Services</span></span>](workflow-services.md)
