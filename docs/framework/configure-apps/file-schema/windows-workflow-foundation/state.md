---
title: <state>
ms.date: 03/30/2017
ms.topic: reference
ms.assetid: 619414f2-61c2-4427-9977-d05009e343db
ms.openlocfilehash: 169fa900b5be9a9577818b68b540184afd4a6681
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91169729"
---
# \<state>

<span data-ttu-id="921b0-101">Reprezentuje kolekcję subskrybowanego stanów z wystąpienia śledzonych przepływu pracy podczas tworzenia rekordów śledzenia.</span><span class="sxs-lookup"><span data-stu-id="921b0-101">Represents a collection of subscribed states from the tracked workflow instance when the tracking records are created.</span></span>  
  
 <span data-ttu-id="921b0-102">Aby uzyskać więcej informacji o śledzeniu zapytań profilowych, zobacz [śledzenie profilów](../../../windows-workflow-foundation/tracking-profiles.md)</span><span class="sxs-lookup"><span data-stu-id="921b0-102">For more information on tracking profile queries, see [Tracking Profiles](../../../windows-workflow-foundation/tracking-profiles.md)</span></span>  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.ServiceModel>**](system-servicemodel-of-workflow.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<tracking>**](tracking.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<trackingProfile>**](trackingprofile.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<workflow>**](workflow.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<workflowInstanceQueries>**](workflowinstancequeries.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<workflowInstanceQuery>**](workflowinstancequery.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<states>**](states.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<state>**  
  
## <a name="syntax"></a><span data-ttu-id="921b0-103">Składnia</span><span class="sxs-lookup"><span data-stu-id="921b0-103">Syntax</span></span>  
  
```xml  
<tracking>
  <trackingProfile name="Name">
    <workflow>
      <workflowInstanceQueries>
        <workflowInstanceQuery>
          <states>
            <state name="Name" />
          </states>
        </workflowInstanceQuery>
      </workflowInstanceQueries>
    </workflow>
  </trackingProfile>
</tracking>  
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="921b0-104">Atrybuty i elementy</span><span class="sxs-lookup"><span data-stu-id="921b0-104">Attributes and Elements</span></span>  

 <span data-ttu-id="921b0-105">W poniższych sekcjach opisano atrybuty, elementy podrzędne i elementy nadrzędne.</span><span class="sxs-lookup"><span data-stu-id="921b0-105">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="921b0-106">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="921b0-106">Attributes</span></span>  
  
|<span data-ttu-id="921b0-107">Atrybut</span><span class="sxs-lookup"><span data-stu-id="921b0-107">Attribute</span></span>|<span data-ttu-id="921b0-108">Opis</span><span class="sxs-lookup"><span data-stu-id="921b0-108">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="921b0-109">name</span><span class="sxs-lookup"><span data-stu-id="921b0-109">name</span></span>|<span data-ttu-id="921b0-110">Ciąg, który określa subskrybowanego stanu z wystąpienia śledzonych przepływu pracy podczas rekordem śledzenia.</span><span class="sxs-lookup"><span data-stu-id="921b0-110">A string that specifies a subscribed state from the tracked workflow instance when the tracking record is created.</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="921b0-111">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="921b0-111">Child Elements</span></span>  

 <span data-ttu-id="921b0-112">Brak.</span><span class="sxs-lookup"><span data-stu-id="921b0-112">None.</span></span>  
  
### <a name="parent-elements"></a><span data-ttu-id="921b0-113">Elementy nadrzędne</span><span class="sxs-lookup"><span data-stu-id="921b0-113">Parent Elements</span></span>  
  
|<span data-ttu-id="921b0-114">Element</span><span class="sxs-lookup"><span data-stu-id="921b0-114">Element</span></span>|<span data-ttu-id="921b0-115">Opis</span><span class="sxs-lookup"><span data-stu-id="921b0-115">Description</span></span>|  
|-------------|-----------------|  
|[\<states>](states.md)|<span data-ttu-id="921b0-116">Kolekcja subskrybowanego stanów z wystąpienia elementu śledzonych przepływu pracy podczas tworzenia rekordów śledzenia.</span><span class="sxs-lookup"><span data-stu-id="921b0-116">A collection of subscribed states from the tracked workflow instance when the tracking records are created.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="921b0-117">Uwagi</span><span class="sxs-lookup"><span data-stu-id="921b0-117">Remarks</span></span>  

 <span data-ttu-id="921b0-118">Zwracane rekordy są filtrowane według stanów w tej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="921b0-118">The returned records are filtered by the states in this collection.</span></span>  
  
 <span data-ttu-id="921b0-119">Stan możliwe wartości są opisane w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="921b0-119">Possible state values are described in the following table.</span></span>  
  
|<span data-ttu-id="921b0-120">Stan</span><span class="sxs-lookup"><span data-stu-id="921b0-120">State</span></span>|<span data-ttu-id="921b0-121">Opis</span><span class="sxs-lookup"><span data-stu-id="921b0-121">Description</span></span>|  
|-----------|-----------------|  
|<span data-ttu-id="921b0-122">Zostało przerwane</span><span class="sxs-lookup"><span data-stu-id="921b0-122">Aborted</span></span>|<span data-ttu-id="921b0-123">Wystąpienie przepływu pracy zostało przerwane.</span><span class="sxs-lookup"><span data-stu-id="921b0-123">The workflow instance is aborted.</span></span>|  
|<span data-ttu-id="921b0-124">Ukończone</span><span class="sxs-lookup"><span data-stu-id="921b0-124">Completed</span></span>|<span data-ttu-id="921b0-125">Wystąpienie przepływu pracy zostało zakończone.</span><span class="sxs-lookup"><span data-stu-id="921b0-125">The workflow instance is completed.</span></span>|  
|<span data-ttu-id="921b0-126">Usunięte</span><span class="sxs-lookup"><span data-stu-id="921b0-126">Deleted</span></span>|<span data-ttu-id="921b0-127">Wystąpienie przepływu pracy, został usunięty.</span><span class="sxs-lookup"><span data-stu-id="921b0-127">The workflow instance is deleted.</span></span>|  
|<span data-ttu-id="921b0-128">Okresy</span><span class="sxs-lookup"><span data-stu-id="921b0-128">Idle</span></span>|<span data-ttu-id="921b0-129">Wystąpienie przepływu pracy jest bezczynny.</span><span class="sxs-lookup"><span data-stu-id="921b0-129">The workflow instance is idle.</span></span>|  
|<span data-ttu-id="921b0-130">Trwały</span><span class="sxs-lookup"><span data-stu-id="921b0-130">Persisted</span></span>|<span data-ttu-id="921b0-131">Wystąpienie przepływu pracy jest trwały.</span><span class="sxs-lookup"><span data-stu-id="921b0-131">The workflow instance is persisted.</span></span>|  
|<span data-ttu-id="921b0-132">Wznowione</span><span class="sxs-lookup"><span data-stu-id="921b0-132">Resumed</span></span>|<span data-ttu-id="921b0-133">Wystąpienie przepływu pracy zostanie wznowione.</span><span class="sxs-lookup"><span data-stu-id="921b0-133">The workflow instance is resumed.</span></span>|  
|<span data-ttu-id="921b0-134">Rozpoczęto</span><span class="sxs-lookup"><span data-stu-id="921b0-134">Started</span></span>|<span data-ttu-id="921b0-135">Wystąpienie przepływu pracy zostało rozpoczęte.</span><span class="sxs-lookup"><span data-stu-id="921b0-135">The workflow instance is started.</span></span>|  
|<span data-ttu-id="921b0-136">UnhandledException</span><span class="sxs-lookup"><span data-stu-id="921b0-136">UnhandledException</span></span>|<span data-ttu-id="921b0-137">Wystąpienie przepływu pracy napotkał nieobsługiwany wyjątek.</span><span class="sxs-lookup"><span data-stu-id="921b0-137">The workflow instance encountered an unhandled exception.</span></span>|  
|<span data-ttu-id="921b0-138">Zwolniono</span><span class="sxs-lookup"><span data-stu-id="921b0-138">Unloaded</span></span>|<span data-ttu-id="921b0-139">Wystąpienie przepływu pracy nie jest załadowany.</span><span class="sxs-lookup"><span data-stu-id="921b0-139">The workflow instance is unloaded.</span></span>|  
|<span data-ttu-id="921b0-140">Anulowane</span><span class="sxs-lookup"><span data-stu-id="921b0-140">Canceled</span></span>|<span data-ttu-id="921b0-141">Wystąpienie przepływu pracy zostało anulowane.</span><span class="sxs-lookup"><span data-stu-id="921b0-141">The workflow instance is canceled.</span></span>|  
|<span data-ttu-id="921b0-142">Suspended</span><span class="sxs-lookup"><span data-stu-id="921b0-142">Suspended</span></span>|<span data-ttu-id="921b0-143">Wystąpienie przepływu pracy jest zawieszone.</span><span class="sxs-lookup"><span data-stu-id="921b0-143">The workflow instance is suspended.</span></span>|  
|<span data-ttu-id="921b0-144">Zakończony</span><span class="sxs-lookup"><span data-stu-id="921b0-144">Terminated</span></span>|<span data-ttu-id="921b0-145">Wystąpienie przepływu pracy jest zakończone.</span><span class="sxs-lookup"><span data-stu-id="921b0-145">The workflow instance is terminated.</span></span>|  
|<span data-ttu-id="921b0-146">Anulowano</span><span class="sxs-lookup"><span data-stu-id="921b0-146">Unsuspended</span></span>|<span data-ttu-id="921b0-147">Anulowano to wystąpienie przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="921b0-147">The workflow instance is unsuspended.</span></span>|  
  
## <a name="example"></a><span data-ttu-id="921b0-148">Przykład</span><span class="sxs-lookup"><span data-stu-id="921b0-148">Example</span></span>  

 <span data-ttu-id="921b0-149">Następująca konfiguracja subskrybuje przepływu rekordów dla śledzenia na poziomie wystąpienia `Started` stan wystąpienia przy użyciu tego zapytania.</span><span class="sxs-lookup"><span data-stu-id="921b0-149">The following configuration subscribes to workflow instance-level tracking records for the `Started` instance state using this query.</span></span>  
  
```xml  
<workflowInstanceQueries>  
    <workflowInstanceQuery>  
      <states>  
        <state name="Started"/>  
      </states>  
    </workflowInstanceQuery>  
</workflowInstanceQueries>  
```  
  
## <a name="see-also"></a><span data-ttu-id="921b0-150">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="921b0-150">See also</span></span>

- <xref:System.ServiceModel.Activities.Tracking.Configuration.WorkflowInstanceQueryElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Activities.Tracking.Configuration.StateElement?displayProperty=nameWithType>
- <xref:System.Activities.Tracking.WorkflowInstanceQuery?displayProperty=nameWithType>
- [<span data-ttu-id="921b0-151">Kontrola i śledzenie przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="921b0-151">Workflow Tracking and Tracing</span></span>](../../../windows-workflow-foundation/workflow-tracking-and-tracing.md)
- [<span data-ttu-id="921b0-152">Profile śledzenia</span><span class="sxs-lookup"><span data-stu-id="921b0-152">Tracking Profiles</span></span>](../../../windows-workflow-foundation/tracking-profiles.md)
