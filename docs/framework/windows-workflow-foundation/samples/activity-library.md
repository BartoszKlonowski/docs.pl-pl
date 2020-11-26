---
title: Biblioteka działań
ms.date: 03/30/2017
ms.assetid: 5323e9d4-71d6-47eb-bfa6-31feac62044d
ms.openlocfilehash: 1a0c289315d7181645573098916788f18493abb8
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96245711"
---
# <a name="activity-library"></a><span data-ttu-id="47635-102">Biblioteka działań</span><span class="sxs-lookup"><span data-stu-id="47635-102">Activity Library</span></span>

<span data-ttu-id="47635-103">Ta sekcja zawiera przykłady demonstrujące zaawansowane działania niestandardowe w Windows Workflow Foundation (WF).</span><span class="sxs-lookup"><span data-stu-id="47635-103">This section contains samples that demonstrate advanced custom activities in Windows Workflow Foundation (WF).</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="47635-104">W tej sekcji</span><span class="sxs-lookup"><span data-stu-id="47635-104">In This Section</span></span>

 [<span data-ttu-id="47635-105">Niestandardowe działanie SendMail</span><span class="sxs-lookup"><span data-stu-id="47635-105">SendMail Custom Activity</span></span>](sendmail-custom-activity.md)  
 <span data-ttu-id="47635-106">Pokazuje, jak utworzyć niestandardowe działanie, które wynika z programu <xref:System.Activities.AsyncCodeActivity> w celu wysłania wiadomości e-mail przy użyciu protokołu SMTP do użycia w aplikacji przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="47635-106">Demonstrates how to create a custom activity that derives from <xref:System.Activities.AsyncCodeActivity> to send mail using SMTP for use within a workflow application.</span></span>  
  
 [<span data-ttu-id="47635-107">Działanie ThrottledParallelForEach</span><span class="sxs-lookup"><span data-stu-id="47635-107">Throttled Parallel ForEach</span></span>](throttled-parallel-foreach.md)  
 <span data-ttu-id="47635-108">Pokazuje, w jaki sposób `ThrottleParallelForEach` działanie jest podobne do <xref:System.Activities.Statements.ParallelForEach%601> działania z jedynym wyjątkiem, że umożliwia ustawienie współczynnika współbieżności, aby ograniczyć liczbę równoczesnych gałęzi do wykonania.</span><span class="sxs-lookup"><span data-stu-id="47635-108">Demonstrates how the `ThrottleParallelForEach` activity is similar to the <xref:System.Activities.Statements.ParallelForEach%601> activity with the one exception that it allows setting a concurrency factor to restrict the number of simultaneous branches to execute.</span></span>
  
 [<span data-ttu-id="47635-109">Działania dostępu do bazy danych</span><span class="sxs-lookup"><span data-stu-id="47635-109">Database Access Activities</span></span>](database-access-activities.md)  
 <span data-ttu-id="47635-110">Pokazuje, jak tworzyć działania umożliwiające dostęp do baz danych w celu pobierania lub modyfikowania informacji oraz korzystania z [ADO.NET](../../data/adonet/index.md) w celu uzyskania dostępu do bazy danych.</span><span class="sxs-lookup"><span data-stu-id="47635-110">Demonstrates how to create activities that allow accessing databases to retrieve or modify information and use [ADO.NET](../../data/adonet/index.md) to access the database.</span></span>  
  
 [<span data-ttu-id="47635-111">Działanie zasad zewnętrznych w programie .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="47635-111">Externalized Policy Activity in .NET Framework 4.5</span></span>](externalized-policy-activity-in-net-framework-4-5.md)  
 <span data-ttu-id="47635-112">Pokazuje, jak działanie ExternalizedPolicy4 umożliwia wykonywanie istniejących Windows Workflow Foundation w .NET Framework 3,5 (WF 3,5) <xref:System.Workflow.Activities.Rules.RuleSet> obiektów w Windows Workflow Foundation [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] (WF 4,5) bezpośrednio przy użyciu aparatu reguł, który jest dostarczany w programie WF 3,5.</span><span class="sxs-lookup"><span data-stu-id="47635-112">Demonstrates how the ExternalizedPolicy4 activity allows executing existing Windows Workflow Foundation in .NET Framework 3.5 (WF 3.5) <xref:System.Workflow.Activities.Rules.RuleSet> objects in Windows Workflow Foundation in [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] (WF 4.5) directly by using the rules engine that is shipped in WF 3.5.</span></span>
  
 [<span data-ttu-id="47635-113">Nieogólne działanie ForEach</span><span class="sxs-lookup"><span data-stu-id="47635-113">Non-Generic ForEach</span></span>](non-generic-foreach.md)  
 <span data-ttu-id="47635-114">Pokazuje, jak utworzyć nieogólną wersję <xref:System.Activities.Statements.ForEach%601> działania.</span><span class="sxs-lookup"><span data-stu-id="47635-114">Demonstrates how to create a non-generic version of the <xref:System.Activities.Statements.ForEach%601> activity.</span></span>  
  
 [<span data-ttu-id="47635-115">Nieogólne działanie ParallelForEach</span><span class="sxs-lookup"><span data-stu-id="47635-115">Non-Generic ParallelForEach</span></span>](non-generic-parallelforeach.md)  
 <span data-ttu-id="47635-116">Pokazuje, jak utworzyć nieogólną wersję <xref:System.Activities.Statements.ParallelForEach%601> działania.</span><span class="sxs-lookup"><span data-stu-id="47635-116">Demonstrates how to create a non-generic version of the <xref:System.Activities.Statements.ParallelForEach%601> activity.</span></span>  
  
 [<span data-ttu-id="47635-117">Działanie GetWorkflowInstanceId</span><span class="sxs-lookup"><span data-stu-id="47635-117">Get WorkflowInstanceId</span></span>](get-workflowinstanceid.md)  
 <span data-ttu-id="47635-118">Demonstruje sposób używania działania niestandardowego w `GetWorkflowInstanceId` celu ZWRÓCENIA identyfikatora wystąpienia przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="47635-118">Demonstrates how to use the custom activity, `GetWorkflowInstanceId`, to return the workflow instance ID.</span></span>
