---
title: Kompensacja
ms.date: 03/30/2017
ms.assetid: 722e9766-48d7-456c-9496-d7c5c8f0fa76
ms.openlocfilehash: 60e2789c4bbd29185af50eaf6555307b894d3902
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96289194"
---
# <a name="compensation"></a><span data-ttu-id="3dc9b-102">Kompensacja</span><span class="sxs-lookup"><span data-stu-id="3dc9b-102">Compensation</span></span>

<span data-ttu-id="3dc9b-103">Kompensacja w Windows Workflow Foundation (WF) to mechanizm, za pomocą którego poprzednio ukończona czynność może zostać cofnięta lub wynagradzana (zgodnie z logiką zdefiniowaną przez aplikację) w przypadku wystąpienia kolejnego błędu.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-103">Compensation in Windows Workflow Foundation (WF) is the mechanism by which previously completed work can be undone or compensated (following the logic defined by the application) when a subsequent failure occurs.</span></span> <span data-ttu-id="3dc9b-104">W tej sekcji opisano sposób korzystania z kompensacji w przepływach pracy.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-104">This section describes how to use compensation in workflows.</span></span>  
  
## <a name="compensation-vs-transactions"></a><span data-ttu-id="3dc9b-105">Kompensacja a transakcje</span><span class="sxs-lookup"><span data-stu-id="3dc9b-105">Compensation vs. Transactions</span></span>  

 <span data-ttu-id="3dc9b-106">Transakcja umożliwia łączenie wielu operacji w pojedynczą jednostkę pracy.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-106">A transaction allows you to combine multiple operations into a single unit of work.</span></span> <span data-ttu-id="3dc9b-107">Użycie transakcji umożliwia aplikacji przerwanie (Przywracanie) wszystkich zmian wykonywanych w ramach transakcji w przypadku wystąpienia błędów występujących w ramach procesu transakcji.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-107">Using a transaction gives your application the ability to abort (roll back) all changes executed from within the transaction if any errors occur during any part of the transaction process.</span></span> <span data-ttu-id="3dc9b-108">Jednak użycie transakcji może być nieodpowiednie, jeśli prace są długotrwałe.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-108">However, using transactions may not be appropriate if the work is long running.</span></span> <span data-ttu-id="3dc9b-109">Na przykład aplikacja do planowania podróży jest zaimplementowana jako przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-109">For example, a travel planning application is implemented as a workflow.</span></span> <span data-ttu-id="3dc9b-110">Kroki przepływu pracy mogą obejmować zarezerwowanie lotu, oczekiwanie na zatwierdzenie przez kierownika, a następnie zapłacenie za lot.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-110">The steps of the workflow may consist of booking a flight, waiting for manager approval, and then paying for the flight.</span></span> <span data-ttu-id="3dc9b-111">Ten proces może potrwać wiele dni i nie jest praktyczny w przypadku czynności związanych z rezerwacją i uiszczeniem opłat za uczestnictwo w tej samej transakcji.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-111">This process could take many days and it is not practical for the steps of booking and paying for the flight to participate in the same transaction.</span></span> <span data-ttu-id="3dc9b-112">W takim scenariuszu można użyć kompensacji w celu cofnięcia etapu rezerwacji przepływu pracy w przypadku wystąpienia błędu w dalszej części przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-112">In a scenario such as this, compensation could be used to undo the booking step of the workflow if there is a failure later in the processing.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="3dc9b-113">W tym temacie omówiono odszkodowanie w przepływach pracy.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-113">This topic covers compensation in workflows.</span></span> <span data-ttu-id="3dc9b-114">Aby uzyskać więcej informacji o transakcjach w przepływach pracy, zobacz [transakcje](workflow-transactions.md) i <xref:System.Activities.Statements.TransactionScope> .</span><span class="sxs-lookup"><span data-stu-id="3dc9b-114">For more information about transactions in workflows, see [Transactions](workflow-transactions.md) and <xref:System.Activities.Statements.TransactionScope>.</span></span> <span data-ttu-id="3dc9b-115">Aby uzyskać więcej informacji na temat transakcji, zobacz <xref:System.Transactions?displayProperty=nameWithType> i <xref:System.Transactions.Transaction?displayProperty=nameWithType> .</span><span class="sxs-lookup"><span data-stu-id="3dc9b-115">For more information about transactions, see <xref:System.Transactions?displayProperty=nameWithType> and <xref:System.Transactions.Transaction?displayProperty=nameWithType>.</span></span>  
  
## <a name="using-compensableactivity"></a><span data-ttu-id="3dc9b-116">Korzystanie z działanie CompensableActivity</span><span class="sxs-lookup"><span data-stu-id="3dc9b-116">Using CompensableActivity</span></span>  

 <span data-ttu-id="3dc9b-117"><xref:System.Activities.Statements.CompensableActivity> to podstawowe działanie związane z kompensacją w programie [!INCLUDE[wf1](../../../includes/wf1-md.md)] .</span><span class="sxs-lookup"><span data-stu-id="3dc9b-117"><xref:System.Activities.Statements.CompensableActivity> is the core compensation activity in [!INCLUDE[wf1](../../../includes/wf1-md.md)].</span></span> <span data-ttu-id="3dc9b-118">Wszelkie działania wykonujące zadania, które mogą być wymagane do uzyskania wynagrodzenia, są umieszczane w <xref:System.Activities.Statements.CompensableActivity.Body%2A> <xref:System.Activities.Statements.CompensableActivity> .</span><span class="sxs-lookup"><span data-stu-id="3dc9b-118">Any activities that perform work that may need to be compensated are placed into the <xref:System.Activities.Statements.CompensableActivity.Body%2A> of a <xref:System.Activities.Statements.CompensableActivity>.</span></span> <span data-ttu-id="3dc9b-119">W tym przykładzie etap rezerwacji zakupu lotu jest umieszczany w <xref:System.Activities.Statements.CompensableActivity.Body%2A> <xref:System.Activities.Statements.CompensableActivity> a, a anulowanie rezerwacji jest umieszczane w <xref:System.Activities.Statements.CompensableActivity.CompensationHandler%2A> .</span><span class="sxs-lookup"><span data-stu-id="3dc9b-119">In this example, the reservation step of purchasing a flight is placed into the <xref:System.Activities.Statements.CompensableActivity.Body%2A> of a <xref:System.Activities.Statements.CompensableActivity> and the cancellation of the reservation is placed into the <xref:System.Activities.Statements.CompensableActivity.CompensationHandler%2A>.</span></span> <span data-ttu-id="3dc9b-120">Natychmiast po <xref:System.Activities.Statements.CompensableActivity> przeniesieniu do przepływu pracy są dwa działania, które oczekują na zatwierdzenie przez Menedżera, a następnie ukończą krok zakupu lotu.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-120">Immediately following the <xref:System.Activities.Statements.CompensableActivity> in the workflow are two activities that wait for manager approval and then complete the purchasing step of the flight.</span></span> <span data-ttu-id="3dc9b-121">Jeśli warunek błędu powoduje, że przepływ pracy zostanie anulowany po <xref:System.Activities.Statements.CompensableActivity> pomyślnym zakończeniu, wówczas działania w ramach <xref:System.Activities.Statements.CompensableActivity.CompensationHandler%2A> programu obsługi są zaplanowane, a lot zostanie anulowany.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-121">If an error condition causes the workflow to be canceled after the <xref:System.Activities.Statements.CompensableActivity> has successfully completed, then the activities in the <xref:System.Activities.Statements.CompensableActivity.CompensationHandler%2A> handler are scheduled and the flight is canceled.</span></span>  
  
 [!code-csharp[CFX_CompensationExample#1](~/samples/snippets/csharp/VS_Snippets_CFX/CFX_CompensationExample/cs/Program.cs#1)]  
  
 <span data-ttu-id="3dc9b-122">Poniższy przykład to przepływ pracy w języku XAML.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-122">The following example is the workflow in XAML.</span></span>  
  
```xaml  
<Sequence  
   xmlns="http://schemas.microsoft.com/netfx/2009/xaml/activities"  
   xmlns:c="clr-namespace:CompensationExample;assembly=CompensationExample"  
   xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">  
  <CompensableActivity>  
    <CompensableActivity.Result>  
      <OutArgument  
         x:TypeArguments="CompensationToken" />  
    </CompensableActivity.Result>  
    <CompensableActivity.CompensationHandler>  
      <c:CancelFlight />  
    </CompensableActivity.CompensationHandler>  
    <c:ReserveFlight />  
  </CompensableActivity>  
  <c:ManagerApproval />  
  <c:PurchaseFlight />  
</Sequence>  
```  
  
 <span data-ttu-id="3dc9b-123">Po wywołaniu przepływu pracy następujące dane wyjściowe są wyświetlane w konsoli programu.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-123">When the workflow is invoked, the following output is displayed to the console.</span></span>  
  
 <span data-ttu-id="3dc9b-124">**ReserveFlight: bilet jest zarezerwowany.**</span><span class="sxs-lookup"><span data-stu-id="3dc9b-124">**ReserveFlight: Ticket is reserved.**</span></span>  
<span data-ttu-id="3dc9b-125">**ManagerApproval: Odebrano zatwierdzenie przez Menedżera.** 
 **PurchaseFlight: bilet jest kupowany.** 
 **Przepływ pracy został pomyślnie ukończony ze stanem: zamknięte.**</span><span class="sxs-lookup"><span data-stu-id="3dc9b-125">**ManagerApproval: Manager approval received.**
**PurchaseFlight: Ticket is purchased.**
**Workflow completed successfully with status: Closed.**</span></span>
> [!NOTE]
> <span data-ttu-id="3dc9b-126">Przykładowe działania w tym temacie, takie jak `ReserveFlight` wyświetlanie ich nazwy i przeznaczenia do konsoli programu, aby ułatwić zilustrowanie kolejności, w której działania są wykonywane, gdy nastąpi kompensacja.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-126">The sample activities in this topic such as `ReserveFlight` display their name and purpose to the console to help illustrate the order in which the activities are executed when compensation occurs.</span></span>  
  
### <a name="default-workflow-compensation"></a><span data-ttu-id="3dc9b-127">Domyślna kompensacja przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="3dc9b-127">Default Workflow Compensation</span></span>  

 <span data-ttu-id="3dc9b-128">Domyślnie, jeśli przepływ pracy zostanie anulowany, logika kompensacji jest uruchamiana dla wszystkich działań kompensacyjne, które zostały pomyślnie kompletne i nie zostały jeszcze potwierdzone lub wynagradzane.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-128">By default, if the workflow is canceled, the compensation logic is run for any compensable activity that has successfully completely and has not already been confirmed or compensated.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="3dc9b-129">Po <xref:System.Activities.Statements.CompensableActivity> *potwierdzeniu*, nie można już wywołać kompensaty dla działania.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-129">When a <xref:System.Activities.Statements.CompensableActivity> is *confirmed*, compensation for the activity can no longer be invoked.</span></span> <span data-ttu-id="3dc9b-130">Proces potwierdzania został opisany w dalszej części tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-130">The confirmation process is described later in this section.</span></span>  
  
 <span data-ttu-id="3dc9b-131">W tym przykładzie wyjątek jest zgłaszany po zarezerwacji lotu, ale przed etapem zatwierdzania przez Menedżera.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-131">In this example, an exception is thrown after the flight is reserved but before the manager approval step.</span></span>  
  
 [!code-csharp[CFX_CompensationExample#2](~/samples/snippets/csharp/VS_Snippets_CFX/CFX_CompensationExample/cs/Program.cs#2)]  
  
 <span data-ttu-id="3dc9b-132">Ten przykład to przepływ pracy w języku XAML.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-132">This example is the workflow in XAML.</span></span>  
  
```xaml  
<Sequence  
   xmlns="http://schemas.microsoft.com/netfx/2009/xaml/activities"  
   xmlns:c="clr-namespace:CompensationExample;assembly=CompensationExample"  
   xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">  
  <CompensableActivity>  
    <CompensableActivity.Result>  
      <OutArgument  
         x:TypeArguments="CompensationToken" />  
    </CompensableActivity.Result>  
    <CompensableActivity.CompensationHandler>  
      <c:CancelFlight />  
    </CompensableActivity.CompensationHandler>  
    <c:ReserveFlight />  
  </CompensableActivity>  
  <c:SimulatedErrorCondition />  
  <c:ManagerApproval />  
  <c:PurchaseFlight />  
</Sequence>  
```  
  
 [!code-csharp[CFX_CompensationExample#100](~/samples/snippets/csharp/VS_Snippets_CFX/CFX_CompensationExample/cs/Program.cs#100)]  
  
 <span data-ttu-id="3dc9b-133">Gdy przepływ pracy jest wywoływany, wyjątek symulowanego warunku błędu jest obsługiwany przez aplikację hosta w <xref:System.Activities.WorkflowApplication.OnUnhandledException%2A> , przepływ pracy zostanie anulowany, a logika kompensacji jest wywoływana.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-133">When the workflow is invoked, the simulated error condition exception is handled by the host application in <xref:System.Activities.WorkflowApplication.OnUnhandledException%2A>, the workflow is canceled, and the compensation logic is invoked.</span></span>  
  
 <span data-ttu-id="3dc9b-134">**ReserveFlight: bilet jest zarezerwowany.**</span><span class="sxs-lookup"><span data-stu-id="3dc9b-134">**ReserveFlight: Ticket is reserved.**</span></span>  
<span data-ttu-id="3dc9b-135">**SimulatedErrorCondition: Zgłaszanie elementu ApplicationException.** 
 **Nieobsługiwany wyjątek przepływu pracy:** 
 **System. ApplicationException: symulowany warunek błędu w przepływie pracy.** 
 **CancelFlight: bilet został anulowany.** 
 **Przepływ pracy został pomyślnie ukończony ze stanem: anulowane.**</span><span class="sxs-lookup"><span data-stu-id="3dc9b-135">**SimulatedErrorCondition: Throwing an ApplicationException.**
**Workflow Unhandled Exception:**
**System.ApplicationException: Simulated error condition in the workflow.**
**CancelFlight: Ticket is canceled.**
**Workflow completed successfully with status: Canceled.**</span></span>

### <a name="cancellation-and-compensableactivity"></a><span data-ttu-id="3dc9b-136">Anulowanie i działanie CompensableActivity</span><span class="sxs-lookup"><span data-stu-id="3dc9b-136">Cancellation and CompensableActivity</span></span>  

 <span data-ttu-id="3dc9b-137">Jeśli działania w ramach programu <xref:System.Activities.Statements.CompensableActivity.Body%2A> <xref:System.Activities.Statements.CompensableActivity> nie zostały ukończone i działanie zostało anulowane, działania w programie <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A> są wykonywane.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-137">If the activities in the <xref:System.Activities.Statements.CompensableActivity.Body%2A> of a <xref:System.Activities.Statements.CompensableActivity> have not completed and the activity is canceled, the activities in the <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A> are executed.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="3dc9b-138"><xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A>Jest wywoływana tylko w przypadku, gdy działania z <xref:System.Activities.Statements.CompensableActivity.Body%2A> programu <xref:System.Activities.Statements.CompensableActivity> nie zostały ukończone i działanie zostało anulowane.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-138">The <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A> is only invoked if the activities in the <xref:System.Activities.Statements.CompensableActivity.Body%2A> of the <xref:System.Activities.Statements.CompensableActivity> have not completed and the activity is canceled.</span></span> <span data-ttu-id="3dc9b-139"><xref:System.Activities.Statements.CompensableActivity.CompensationHandler%2A>Jest wykonywane tylko wtedy, gdy działania z <xref:System.Activities.Statements.CompensableActivity.Body%2A> programu <xref:System.Activities.Statements.CompensableActivity> zostały pomyślnie wykonane i wynagrodzenie jest następnie wywoływane dla działania.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-139">The <xref:System.Activities.Statements.CompensableActivity.CompensationHandler%2A> is only executed if the activities in the <xref:System.Activities.Statements.CompensableActivity.Body%2A> of the <xref:System.Activities.Statements.CompensableActivity> have successfully completed and compensation is subsequently invoked on the activity.</span></span>  
  
 <span data-ttu-id="3dc9b-140"><xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A>Daje autorom przepływu pracy możliwość zapewnienia odpowiedniej logiki anulowania.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-140">The <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A> gives workflow authors the opportunity to provide any appropriate cancellation logic.</span></span> <span data-ttu-id="3dc9b-141">W poniższym przykładzie wyjątek jest zgłaszany podczas wykonywania <xref:System.Activities.Statements.CompensableActivity.Body%2A> , a następnie <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A> wywoływany.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-141">In the following example, an exception is thrown during the execution of the <xref:System.Activities.Statements.CompensableActivity.Body%2A>, and then the <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A> is invoked.</span></span>  
  
```csharp  
Activity wf = new Sequence()  
{  
    Activities =  
    {  
        new CompensableActivity  
        {  
            Body = new Sequence  
            {  
                Activities =
                {  
                    new ChargeCreditCard(),  
                    new SimulatedErrorCondition(),  
                    new ReserveFlight()  
                }  
            },  
            CompensationHandler = new CancelFlight(),  
            CancellationHandler = new CancelCreditCard()  
        },  
        new ManagerApproval(),  
        new PurchaseFlight()  
    }  
};  
```  
  
 <span data-ttu-id="3dc9b-142">Ten przykład to przepływ pracy w języku XAML</span><span class="sxs-lookup"><span data-stu-id="3dc9b-142">This example is the workflow in XAML</span></span>  
  
```xaml  
<Sequence  
   xmlns="http://schemas.microsoft.com/netfx/2009/xaml/activities"  
   xmlns:c="clr-namespace:CompensationExample;assembly=CompensationExample"  
   xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">  
  <CompensableActivity>  
    <CompensableActivity.Result>  
      <OutArgument  
         x:TypeArguments="CompensationToken" />  
    </CompensableActivity.Result>  
    <Sequence>  
      <c:ChargeCreditCard />  
      <c:SimulatedErrorCondition />  
      <c:ReserveFlight />  
    </Sequence>  
    <CompensableActivity.CancellationHandler>  
      <c:CancelCreditCard />  
    </CompensableActivity.CancellationHandler>  
    <CompensableActivity.CompensationHandler>  
      <c:CancelFlight />  
    </CompensableActivity.CompensationHandler>  
  </CompensableActivity>  
  <c:ManagerApproval />  
  <c:PurchaseFlight />  
</Sequence>  
```  
  
 <span data-ttu-id="3dc9b-143">Gdy przepływ pracy jest wywoływany, wyjątek symulowanego warunku błędu jest obsługiwany przez aplikację hosta w <xref:System.Activities.WorkflowApplication.OnUnhandledException%2A> , przepływ pracy zostanie anulowany, a logika anulowania <xref:System.Activities.Statements.CompensableActivity> jest wywoływana.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-143">When the workflow is invoked, the simulated error condition exception is handled by the host application in <xref:System.Activities.WorkflowApplication.OnUnhandledException%2A>, the workflow is canceled, and the cancellation logic of the <xref:System.Activities.Statements.CompensableActivity> is invoked.</span></span> <span data-ttu-id="3dc9b-144">W tym przykładzie logika kompensacji i logika anulowania mają różne cele.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-144">In this example, the compensation logic and the cancellation logic have different goals.</span></span> <span data-ttu-id="3dc9b-145">Jeśli <xref:System.Activities.Statements.CompensableActivity.Body%2A> zakończyło się pomyślnie, oznacza to, że opłata za kartę kredytową została naliczona i jest ona księgowana zgodnie z zapisem, dlatego należy cofnąć obie czynności.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-145">If the <xref:System.Activities.Statements.CompensableActivity.Body%2A> completed successfully, then this means the credit card was charged and the flight booked, so the compensation should undo both steps.</span></span> <span data-ttu-id="3dc9b-146">(W tym przykładzie anulowanie lotu automatycznie anuluje opłaty za kartę kredytową). Jeśli jednak <xref:System.Activities.Statements.CompensableActivity> zostanie anulowana, oznacza to, że <xref:System.Activities.Statements.CompensableActivity.Body%2A> nie została ukończona, a więc logika <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A> musi być w stanie określić, jak najlepiej obsłużyć anulowanie.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-146">(In this example, canceling the flight automatically cancels the credit card charges.) However, if the <xref:System.Activities.Statements.CompensableActivity> is canceled, this means the <xref:System.Activities.Statements.CompensableActivity.Body%2A> did not complete and so the logic of the <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A> needs to be able to determine how to best handle the cancellation.</span></span> <span data-ttu-id="3dc9b-147">W tym przykładzie <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A> anuluje opłaty za kartę kredytową, ale od czasu `ReserveFlight` ostatniego działania w programie nie jest <xref:System.Activities.Statements.CompensableActivity.Body%2A> podejmowana próba anulowania lotu.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-147">In this example, the <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A> cancels the credit card charge, but since `ReserveFlight` was the last activity in the <xref:System.Activities.Statements.CompensableActivity.Body%2A>, it does not attempt to cancel the flight.</span></span> <span data-ttu-id="3dc9b-148">Ponieważ `ReserveFlight` była ostatnią aktywnością w programie <xref:System.Activities.Statements.CompensableActivity.Body%2A> , w przypadku pomyślnego wykonania operacji <xref:System.Activities.Statements.CompensableActivity.Body%2A> zostałaby ukończona i nie będzie możliwe jej anulowanie.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-148">Since `ReserveFlight` was the last activity in the <xref:System.Activities.Statements.CompensableActivity.Body%2A>, if it had successfully completed then the <xref:System.Activities.Statements.CompensableActivity.Body%2A> would have completed and no cancellation would be possible.</span></span>  
  
 <span data-ttu-id="3dc9b-149">**ChargeCreditCard: opłata za kartę kredytową dla lotu.**</span><span class="sxs-lookup"><span data-stu-id="3dc9b-149">**ChargeCreditCard: Charge credit card for flight.**</span></span>  
<span data-ttu-id="3dc9b-150">**SimulatedErrorCondition: Zgłaszanie elementu ApplicationException.** 
 **Nieobsługiwany wyjątek przepływu pracy:** 
 **System. ApplicationException: symulowany warunek błędu w przepływie pracy.** 
 **CancelCreditCard: Anuluj opłaty za karty kredytowe.** 
 **Przepływ pracy został pomyślnie ukończony ze stanem: anulowane.**</span><span class="sxs-lookup"><span data-stu-id="3dc9b-150">**SimulatedErrorCondition: Throwing an ApplicationException.**
**Workflow Unhandled Exception:**
**System.ApplicationException: Simulated error condition in the workflow.**
**CancelCreditCard: Cancel credit card charges.**
**Workflow completed successfully with status: Canceled.**</span></span>  <span data-ttu-id="3dc9b-151">Aby uzyskać więcej informacji na temat anulowania, zobacz [anulowania](modeling-cancellation-behavior-in-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="3dc9b-151">For more information about cancellation, see [Cancellation](modeling-cancellation-behavior-in-workflows.md).</span></span>  
  
### <a name="explicit-compensation-using-the-compensate-activity"></a><span data-ttu-id="3dc9b-152">Jawne wynagrodzenie przy użyciu działania kompensacja</span><span class="sxs-lookup"><span data-stu-id="3dc9b-152">Explicit Compensation Using the Compensate Activity</span></span>  

 <span data-ttu-id="3dc9b-153">W poprzedniej sekcji podano niejawną kompensację.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-153">In the previous section, implicit compensation was covered.</span></span> <span data-ttu-id="3dc9b-154">Niejawne kompensacje mogą być odpowiednie w przypadku prostych scenariuszy, ale jeśli jest wymagana bardziej jawna kontrola nad planowaniem obsługi kompensacji, <xref:System.Activities.Statements.Compensate> działanie może być używane.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-154">Implicit compensation can be appropriate for simple scenarios, but if more explicit control is required over the scheduling of compensation handling then the <xref:System.Activities.Statements.Compensate> activity can be used.</span></span> <span data-ttu-id="3dc9b-155">W celu zainicjowania procesu kompensacji <xref:System.Activities.Statements.Compensate> działania należy <xref:System.Activities.Statements.CompensationToken> użyć elementu, <xref:System.Activities.Statements.CompensableActivity> dla którego jest wymagana kompensacja.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-155">To initiate the compensation process with the <xref:System.Activities.Statements.Compensate> activity, the <xref:System.Activities.Statements.CompensationToken> of the <xref:System.Activities.Statements.CompensableActivity> for which compensation is desired is used.</span></span> <span data-ttu-id="3dc9b-156"><xref:System.Activities.Statements.Compensate>Działanie może służyć do inicjowania kompensaty dla wszystkich ukończonych <xref:System.Activities.Statements.CompensableActivity> , które nie zostały potwierdzone lub wynagradzane.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-156">The <xref:System.Activities.Statements.Compensate> activity can be used to initiate compensation on any completed <xref:System.Activities.Statements.CompensableActivity> that has not been confirmed or compensated.</span></span> <span data-ttu-id="3dc9b-157">Na przykład <xref:System.Activities.Statements.Compensate> działanie może być używane w <xref:System.Activities.Statements.TryCatch.Catches%2A> sekcji <xref:System.Activities.Statements.TryCatch> działania lub w dowolnym momencie po <xref:System.Activities.Statements.CompensableActivity> zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-157">For example, a <xref:System.Activities.Statements.Compensate> activity could be used in the <xref:System.Activities.Statements.TryCatch.Catches%2A> section of a <xref:System.Activities.Statements.TryCatch> activity, or any time after the <xref:System.Activities.Statements.CompensableActivity> has completed.</span></span> <span data-ttu-id="3dc9b-158">W tym przykładzie <xref:System.Activities.Statements.Compensate> działanie jest używane w <xref:System.Activities.Statements.TryCatch.Catches%2A> sekcji <xref:System.Activities.Statements.TryCatch> działania w celu odwrócenia akcji <xref:System.Activities.Statements.CompensableActivity> .</span><span class="sxs-lookup"><span data-stu-id="3dc9b-158">In this example, the <xref:System.Activities.Statements.Compensate> activity is used in the <xref:System.Activities.Statements.TryCatch.Catches%2A> section of a <xref:System.Activities.Statements.TryCatch> activity to reverse the action of the <xref:System.Activities.Statements.CompensableActivity>.</span></span>  
  
 [!code-csharp[CFX_CompensationExample#3](~/samples/snippets/csharp/VS_Snippets_CFX/CFX_CompensationExample/cs/Program.cs#3)]  
  
 <span data-ttu-id="3dc9b-159">Ten przykład to przepływ pracy w języku XAML.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-159">This example is the workflow in XAML.</span></span>  
  
```xaml  
<TryCatch  
   xmlns="http://schemas.microsoft.com/netfx/2009/xaml/activities"  
   xmlns:c="clr-namespace:CompensationExample;assembly=CompensationExample"  
   xmlns:s="clr-namespace:System;assembly=mscorlib"  
   xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">  
  <TryCatch.Variables>  
    <Variable  
       x:TypeArguments="CompensationToken"  
       x:Name="__ReferenceID0"  
       Name="token1" />  
  </TryCatch.Variables>  
  <TryCatch.Try>  
    <Sequence>  
      <CompensableActivity>  
        <CompensableActivity.Result>  
          <OutArgument  
             x:TypeArguments="CompensationToken">  
            <VariableReference  
               x:TypeArguments="CompensationToken"  
               Variable="{x:Reference __ReferenceID0}">  
              <VariableReference.Result>  
                <OutArgument  
                   x:TypeArguments="Location(CompensationToken)" />  
              </VariableReference.Result>  
            </VariableReference>  
          </OutArgument>  
        </CompensableActivity.Result>  
        <CompensableActivity.CompensationHandler>  
          <c:CancelFlight />  
        </CompensableActivity.CompensationHandler>  
        <CompensableActivity.ConfirmationHandler>  
          <c:ConfirmFlight />  
        </CompensableActivity.ConfirmationHandler>  
        <c:ReserveFlight />  
      </CompensableActivity>  
      <c:SimulatedErrorCondition />  
      <c:ManagerApproval />  
      <c:PurchaseFlight />  
    </Sequence>  
  </TryCatch.Try>  
  <TryCatch.Catches>  
    <Catch  
       x:TypeArguments="s:ApplicationException">  
      <ActivityAction  
         x:TypeArguments="s:ApplicationException">  
        <Compensate>  
          <Compensate.Target>  
            <InArgument  
               x:TypeArguments="CompensationToken">  
              <VariableValue  
                 x:TypeArguments="CompensationToken"  
                 Variable="{x:Reference __ReferenceID0}">  
                <VariableValue.Result>  
                  <OutArgument  
                     x:TypeArguments="CompensationToken" />  
                </VariableValue.Result>  
              </VariableValue>  
            </InArgument>  
          </Compensate.Target>  
        </Compensate>  
      </ActivityAction>  
    </Catch>  
  </TryCatch.Catches>  
</TryCatch>  
```  
  
 <span data-ttu-id="3dc9b-160">Po wywołaniu przepływu pracy następujące dane wyjściowe są wyświetlane w konsoli programu.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-160">When the workflow is invoked, the following output is displayed to the console.</span></span>  
  
 <span data-ttu-id="3dc9b-161">**ReserveFlight: bilet jest zarezerwowany.**</span><span class="sxs-lookup"><span data-stu-id="3dc9b-161">**ReserveFlight: Ticket is reserved.**</span></span>  
<span data-ttu-id="3dc9b-162">**SimulatedErrorCondition: Zgłaszanie elementu ApplicationException.** 
 **CancelFlight: bilet został anulowany.** 
 **Przepływ pracy został pomyślnie ukończony ze stanem: zamknięte.**</span><span class="sxs-lookup"><span data-stu-id="3dc9b-162">**SimulatedErrorCondition: Throwing an ApplicationException.**
**CancelFlight: Ticket is canceled.**
**Workflow completed successfully with status: Closed.**</span></span>

### <a name="confirming-compensation"></a><span data-ttu-id="3dc9b-163">Potwierdzanie kompensaty</span><span class="sxs-lookup"><span data-stu-id="3dc9b-163">Confirming Compensation</span></span>  

 <span data-ttu-id="3dc9b-164">Domyślnie działania kompensacyjne mogą być kompensowane w dowolnym momencie po zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-164">By default, compensable activities can be compensated any time after they have completed.</span></span> <span data-ttu-id="3dc9b-165">W niektórych scenariuszach może to nie być odpowiednie.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-165">In some scenarios this may not be appropriate.</span></span> <span data-ttu-id="3dc9b-166">W poprzednim przykładzie wynagrodzenie związane z odświadczeniem biletu zostało anulowane.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-166">In the previous example the compensation to reserving the ticket was to cancel the reservation.</span></span> <span data-ttu-id="3dc9b-167">Jednak po ukończeniu lotu ten krok kompensaty nie jest już ważny.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-167">However, after the flight has been completed this compensation step is no longer valid.</span></span> <span data-ttu-id="3dc9b-168">Potwierdzenie działania kompensacyjne wywołuje działanie określone przez <xref:System.Activities.Statements.CompensableActivity.ConfirmationHandler%2A> .</span><span class="sxs-lookup"><span data-stu-id="3dc9b-168">Confirming the compensable activity invokes the activity specified by the <xref:System.Activities.Statements.CompensableActivity.ConfirmationHandler%2A>.</span></span> <span data-ttu-id="3dc9b-169">Jednym z tych możliwości jest umożliwienie wszelkim zasobom, które są niezbędne do zwolnienia wyrównania.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-169">One possible use for this is to allow any resources that are necessary to perform the compensation to be released.</span></span> <span data-ttu-id="3dc9b-170">Po potwierdzeniu działania kompensacyjne nie jest możliwe jego kompensowanie, a jeśli zostanie podjęta próba, <xref:System.InvalidOperationException> zostanie zgłoszony wyjątek.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-170">After a compensable activity is confirmed it is not possible for it to be compensated, and if this is attempted an <xref:System.InvalidOperationException> exception is thrown.</span></span> <span data-ttu-id="3dc9b-171">Gdy przepływ pracy zakończy się pomyślnie, wszystkie niepotwierdzone i niekompensowane działania kompensacyjne, które zostały zakończone pomyślnie, są potwierdzone w odwrotnej kolejności uzupełniania.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-171">When a workflow completes successfully, all non-confirmed and non-compensated compensable activities that completed successfully are confirmed in reverse order of completion.</span></span> <span data-ttu-id="3dc9b-172">W tym przykładzie lot jest zastrzeżony, zakupiony i zakończony, a następnie działanie kompensacyjne zostało potwierdzone.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-172">In this example the flight is reserved, purchased, and completed, and then the compensable activity is confirmed.</span></span> <span data-ttu-id="3dc9b-173">Aby potwierdzić <xref:System.Activities.Statements.CompensableActivity> , użyj <xref:System.Activities.Statements.Confirm> działania i określ, <xref:System.Activities.Statements.CompensationToken> <xref:System.Activities.Statements.CompensableActivity> Aby potwierdzić.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-173">To confirm a <xref:System.Activities.Statements.CompensableActivity>, use the <xref:System.Activities.Statements.Confirm> activity and specify the <xref:System.Activities.Statements.CompensationToken> of the <xref:System.Activities.Statements.CompensableActivity> to confirm.</span></span>  
  
 [!code-csharp[CFX_CompensationExample#4](~/samples/snippets/csharp/VS_Snippets_CFX/CFX_CompensationExample/cs/Program.cs#4)]  
  
 <span data-ttu-id="3dc9b-174">Ten przykład to przepływ pracy w języku XAML.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-174">This example is the workflow in XAML.</span></span>  
  
```xaml  
<Sequence  
   xmlns="http://schemas.microsoft.com/netfx/2009/xaml/activities"  
   xmlns:c="clr-namespace:CompensationExample;assembly=CompensationExample"  
   xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">  
  <Sequence.Variables>  
    <x:Reference>__ReferenceID0</x:Reference>  
  </Sequence.Variables>  
  <CompensableActivity>  
    <CompensableActivity.Result>  
      <OutArgument  
         x:TypeArguments="CompensationToken">  
        <VariableReference  
           x:TypeArguments="CompensationToken">  
          <VariableReference.Result>  
            <OutArgument  
               x:TypeArguments="Location(CompensationToken)" />  
          </VariableReference.Result>  
          <VariableReference.Variable>  
            <Variable  
               x:TypeArguments="CompensationToken"  
               x:Name="__ReferenceID0"  
               Name="token1" />  
          </VariableReference.Variable>  
        </VariableReference>  
      </OutArgument>  
    </CompensableActivity.Result>  
    <CompensableActivity.CompensationHandler>  
      <c:CancelFlight />  
    </CompensableActivity.CompensationHandler>  
    <CompensableActivity.ConfirmationHandler>  
      <c:ConfirmFlight />  
    </CompensableActivity.ConfirmationHandler>  
    <c:ReserveFlight />  
  </CompensableActivity>  
  <c:ManagerApproval />  
  <c:PurchaseFlight />  
  <c:TakeFlight />  
  <Confirm>  
    <Confirm.Target>  
      <InArgument  
         x:TypeArguments="CompensationToken">  
        <VariableValue  
           x:TypeArguments="CompensationToken"  
           Variable="{x:Reference __ReferenceID0}">  
          <VariableValue.Result>  
            <OutArgument  
               x:TypeArguments="CompensationToken" />  
          </VariableValue.Result>  
        </VariableValue>  
      </InArgument>  
    </Confirm.Target>  
  </Confirm>  
</Sequence>  
```  
  
<span data-ttu-id="3dc9b-175">Po wywołaniu przepływu pracy następujące dane wyjściowe są wyświetlane w konsoli programu.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-175">When the workflow is invoked, the following output is displayed to the console.</span></span>  
  
<span data-ttu-id="3dc9b-176">**ReserveFlight: bilet jest zarezerwowany.**</span><span class="sxs-lookup"><span data-stu-id="3dc9b-176">**ReserveFlight: Ticket is reserved.**</span></span>  
<span data-ttu-id="3dc9b-177">**ManagerApproval: Odebrano zatwierdzenie przez Menedżera.** 
 **PurchaseFlight: bilet jest kupowany.** 
 **TakeFlight: samolot został ukończony.** 
 ConfirmFlight: nastąpiło przeprowadzenie **lotu. nie można uzyskać wynagrodzenia.** 
 **Przepływ pracy został pomyślnie ukończony ze stanem: zamknięte.**</span><span class="sxs-lookup"><span data-stu-id="3dc9b-177">**ManagerApproval: Manager approval received.**
**PurchaseFlight: Ticket is purchased.**
**TakeFlight: Flight is completed.**
**ConfirmFlight: Flight has been taken, no compensation possible.**
**Workflow completed successfully with status: Closed.**</span></span>

## <a name="nesting-compensation-activities"></a><span data-ttu-id="3dc9b-178">Zagnieżdżanie działań związanych z kompensacją</span><span class="sxs-lookup"><span data-stu-id="3dc9b-178">Nesting Compensation Activities</span></span>  

<span data-ttu-id="3dc9b-179"><xref:System.Activities.Statements.CompensableActivity>Można umieścić w <xref:System.Activities.Statements.CompensableActivity.Body%2A> sekcji innej <xref:System.Activities.Statements.CompensableActivity> .</span><span class="sxs-lookup"><span data-stu-id="3dc9b-179">A <xref:System.Activities.Statements.CompensableActivity> can be placed into the <xref:System.Activities.Statements.CompensableActivity.Body%2A> section of another <xref:System.Activities.Statements.CompensableActivity>.</span></span> <span data-ttu-id="3dc9b-180"><xref:System.Activities.Statements.CompensableActivity>Nie może być umieszczony w procedurze obsługi innej <xref:System.Activities.Statements.CompensableActivity> .</span><span class="sxs-lookup"><span data-stu-id="3dc9b-180">A <xref:System.Activities.Statements.CompensableActivity> may not be placed into a handler of another <xref:System.Activities.Statements.CompensableActivity>.</span></span> <span data-ttu-id="3dc9b-181">Zadaniem nadrzędnym jest <xref:System.Activities.Statements.CompensableActivity> upewnienie się, że gdy zostanie on anulowany, potwierdzony lub wynagradzany, wszystkie podrzędne działania kompensacyjne, które zostały zakończone pomyślnie i nie zostały jeszcze potwierdzone lub kompensowane, muszą zostać potwierdzone lub skompensowane przed zakończeniem anulowania, potwierdzenia lub kompensaty.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-181">It is the responsibility of a parent <xref:System.Activities.Statements.CompensableActivity> to ensure that when it is canceled, confirmed, or compensated, all child compensable activities that have completed successfully and have not already been confirmed or compensated must be confirmed or compensated before the parent completes cancellation, confirmation, or compensation.</span></span> <span data-ttu-id="3dc9b-182">Jeśli nie jest to jawnie modelowane, obiekt nadrzędny <xref:System.Activities.Statements.CompensableActivity> będzie niejawnie kompensować podrzędne działania kompensacyjne, jeśli element nadrzędny otrzymał sygnał Cancel lub kompensacja.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-182">If this is not modeled explicitly the parent <xref:System.Activities.Statements.CompensableActivity> will implicitly compensate child compensable activities if the parent received the cancel or compensate signal.</span></span> <span data-ttu-id="3dc9b-183">Jeśli element nadrzędny otrzymał sygnał Confirm, element nadrzędny będzie niejawnie potwierdzał podrzędne działania kompensacyjne.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-183">If the parent received the confirm signal the parent will implicitly confirm child compensable activities.</span></span> <span data-ttu-id="3dc9b-184">Jeśli logika do obsługi anulowania, potwierdzenia lub kompensacji jest jawnie modelowana w procedurze obsługi elementu nadrzędnego <xref:System.Activities.Statements.CompensableActivity> , wszelkie elementy podrzędne, które nie zostały jawnie obsłużone, zostaną niejawnie potwierdzone.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-184">If the logic to handle cancellation, confirmation, or compensation is explicitly modeled in the handler of the parent <xref:System.Activities.Statements.CompensableActivity>, any child not explicitly handled will be implicitly confirmed.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="3dc9b-185">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="3dc9b-185">See also</span></span>

- <xref:System.Activities.Statements.CompensableActivity>
- <xref:System.Activities.Statements.Compensate>
- <xref:System.Activities.Statements.Confirm>
- <xref:System.Activities.Statements.CompensationToken>
