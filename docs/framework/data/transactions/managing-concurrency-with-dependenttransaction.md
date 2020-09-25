---
title: Zarządzanie współbieżnością za pomocą DependentTransaction
description: Zarządzanie współbieżnością transakcji, w tym zadaniami asynchronicznymi, przy użyciu klasy DependentTransaction w programie .NET.
ms.date: 03/30/2017
ms.assetid: b85a97d8-8e02-4555-95df-34c8af095148
ms.openlocfilehash: 1e99006c127d83892155bd81e683f5995ac517ef
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91186747"
---
# <a name="managing-concurrency-with-dependenttransaction"></a><span data-ttu-id="cd750-103">Zarządzanie współbieżnością za pomocą DependentTransaction</span><span class="sxs-lookup"><span data-stu-id="cd750-103">Managing Concurrency with DependentTransaction</span></span>

<span data-ttu-id="cd750-104"><xref:System.Transactions.Transaction> Obiekt zostanie utworzony przy użyciu <xref:System.Transactions.Transaction.DependentClone%2A> metody.</span><span class="sxs-lookup"><span data-stu-id="cd750-104">The <xref:System.Transactions.Transaction> object is created using the <xref:System.Transactions.Transaction.DependentClone%2A> method.</span></span> <span data-ttu-id="cd750-105">Jedynym celem jest zagwarantowanie, że transakcja nie może zostać zatwierdzona, a niektóre inne fragmenty kodu (na przykład wątek roboczy) nadal wykonują prace nad transakcją.</span><span class="sxs-lookup"><span data-stu-id="cd750-105">Its sole purpose is to guarantee that the transaction cannot commit while some other pieces of code (for example, a worker thread) are still performing work on the transaction.</span></span> <span data-ttu-id="cd750-106">Gdy działanie wykonane w ramach sklonowanej transakcji zostanie ukończone i gotowe do zatwierdzenia, może powiadomić twórcę transakcji przy użyciu <xref:System.Transactions.DependentTransaction.Complete%2A> metody.</span><span class="sxs-lookup"><span data-stu-id="cd750-106">When the work done within the cloned transaction is complete and ready to be committed, it can notify the creator of the transaction using the <xref:System.Transactions.DependentTransaction.Complete%2A> method.</span></span> <span data-ttu-id="cd750-107">W związku z tym można zachować spójności i poprawności danych.</span><span class="sxs-lookup"><span data-stu-id="cd750-107">Thus, you can preserve the consistency and correctness of data.</span></span>  
  
 <span data-ttu-id="cd750-108"><xref:System.Transactions.DependentTransaction> Klasy można również zarządzać współbieżności między zadania asynchronicznego.</span><span class="sxs-lookup"><span data-stu-id="cd750-108">The <xref:System.Transactions.DependentTransaction> class can also be used to manage concurrency between asynchronous tasks.</span></span> <span data-ttu-id="cd750-109">W tym scenariuszu nadrzędnego można kontynuować wykonywania żadnych kodu podczas klon zależny działa na własnych zadań.</span><span class="sxs-lookup"><span data-stu-id="cd750-109">In this scenario, the parent can continue to execute any code while the dependent clone works on its own tasks.</span></span> <span data-ttu-id="cd750-110">Innymi słowy, wykonanie elementu nadrzędnego nie jest blokowane do momentu zakończenia zależnego.</span><span class="sxs-lookup"><span data-stu-id="cd750-110">In other words, the parent's execution is not blocked until the dependent completes.</span></span>  
  
## <a name="creating-a-dependent-clone"></a><span data-ttu-id="cd750-111">Tworzenie klon zależny</span><span class="sxs-lookup"><span data-stu-id="cd750-111">Creating a Dependent Clone</span></span>  

 <span data-ttu-id="cd750-112">Aby utworzyć zależne transakcji, należy wywołać <xref:System.Transactions.Transaction.DependentClone%2A> metody i przekazać <xref:System.Transactions.DependentCloneOption> wyliczenia jako parametr.</span><span class="sxs-lookup"><span data-stu-id="cd750-112">To create a dependent transaction, call the <xref:System.Transactions.Transaction.DependentClone%2A> method and pass the <xref:System.Transactions.DependentCloneOption> enumeration as a parameter.</span></span> <span data-ttu-id="cd750-113">Ten parametr określa zachowanie transakcji, jeśli `Commit` jest wywoływana w transakcji nadrzędnej przed klon zależny wskazuje, że jest gotowa na zatwierdzenie transakcji (przez wywołanie metody <xref:System.Transactions.DependentTransaction.Complete%2A> metody).</span><span class="sxs-lookup"><span data-stu-id="cd750-113">This parameter defines the behavior of the transaction if `Commit` is called on the parent transaction before the dependent clone indicates that it is ready for the transaction to commit (by calling the <xref:System.Transactions.DependentTransaction.Complete%2A> method).</span></span> <span data-ttu-id="cd750-114">Następujące wartości są prawidłowe dla tego parametru:</span><span class="sxs-lookup"><span data-stu-id="cd750-114">The following values are valid for this parameter:</span></span>  
  
- <span data-ttu-id="cd750-115"><xref:System.Transactions.DependentCloneOption.BlockCommitUntilComplete> tworzy transakcję zależną, która blokuje proces zatwierdzania transakcji nadrzędnej, aż do upływu limitu czasu transakcji nadrzędnej lub do momentu <xref:System.Transactions.DependentTransaction.Complete%2A> wywołania wszystkich elementów zależnych wskazujących ich zakończenie.</span><span class="sxs-lookup"><span data-stu-id="cd750-115"><xref:System.Transactions.DependentCloneOption.BlockCommitUntilComplete> creates a dependent transaction that blocks the commit process of the parent transaction until the parent transaction times out, or until <xref:System.Transactions.DependentTransaction.Complete%2A> is called on all dependents indicating their completion.</span></span> <span data-ttu-id="cd750-116">Jest to przydatne, gdy klient nie chce, aby transakcja nadrzędna została zatwierdzona do momentu zakończenia transakcji zależnych.</span><span class="sxs-lookup"><span data-stu-id="cd750-116">This is useful when the client does not want the parent transaction to commit until the dependent transactions have completed.</span></span> <span data-ttu-id="cd750-117">Jeśli element nadrzędny zakończy pracę starszych niż zależne transakcji i wywołuje <xref:System.Transactions.CommittableTransaction.Commit%2A> dla transakcji, proces zatwierdzania jest zablokowany w stanie, w którym dodatkowe pracy można wykonać na transakcji i można było utworzyć nowe rejestracji, aż wszystkie wywołania zależności <xref:System.Transactions.DependentTransaction.Complete%2A>.</span><span class="sxs-lookup"><span data-stu-id="cd750-117">If the parent finishes its work earlier than the dependent transaction and calls <xref:System.Transactions.CommittableTransaction.Commit%2A> on the transaction, the commit process is blocked in a state where additional work can be done on the transaction and new enlistments can be created, until all of the dependents call <xref:System.Transactions.DependentTransaction.Complete%2A>.</span></span> <span data-ttu-id="cd750-118">Jako ukończony je wszystkie jego pracę, a następnie wywołać <xref:System.Transactions.DependentTransaction.Complete%2A>, rozpocznie się proces zatwierdzania dla transakcji.</span><span class="sxs-lookup"><span data-stu-id="cd750-118">As soon as all of them have finished their work and call <xref:System.Transactions.DependentTransaction.Complete%2A>, the commit process for the transaction begins.</span></span>  
  
- <span data-ttu-id="cd750-119"><xref:System.Transactions.DependentCloneOption.RollbackIfNotComplete>z drugiej strony program tworzy zależną transakcję, która zostanie automatycznie przerwana, jeśli <xref:System.Transactions.CommittableTransaction.Commit%2A> jest wywoływana w transakcji nadrzędnej przed <xref:System.Transactions.DependentTransaction.Complete%2A> wywołaniem.</span><span class="sxs-lookup"><span data-stu-id="cd750-119"><xref:System.Transactions.DependentCloneOption.RollbackIfNotComplete>, on the other hand, creates a dependent transaction that automatically aborts if <xref:System.Transactions.CommittableTransaction.Commit%2A> is called on the parent transaction before <xref:System.Transactions.DependentTransaction.Complete%2A> is called.</span></span> <span data-ttu-id="cd750-120">W takim przypadku wszystkie prace wykonane w transakcji zależne jest prawidłowa w ramach jednej transakcji okres istnienia i nie jest Państwo przekazać tylko jego części.</span><span class="sxs-lookup"><span data-stu-id="cd750-120">In this case, all the work done in the dependent transaction is intact within one transaction lifetime, and no one has a chance to commit just a portion of it.</span></span>  
  
 <span data-ttu-id="cd750-121"><xref:System.Transactions.DependentTransaction.Complete%2A>Metoda musi być wywoływana tylko raz, gdy aplikacja zakończy pracę w transakcji zależnej; w przeciwnym razie <xref:System.InvalidOperationException> jest zgłaszany.</span><span class="sxs-lookup"><span data-stu-id="cd750-121">The <xref:System.Transactions.DependentTransaction.Complete%2A> method must be called only once when your application finishes its work on the dependent transaction; otherwise, a <xref:System.InvalidOperationException> is thrown.</span></span> <span data-ttu-id="cd750-122">Po wywołaniu to wywołanie, nie należy spróbować żadnych dodatkowych działań w transakcji lub wyjątku.</span><span class="sxs-lookup"><span data-stu-id="cd750-122">After this call is invoked, you must not attempt any additional work on the transaction, or an exception is thrown.</span></span>  
  
 <span data-ttu-id="cd750-123">Poniższy przykład kodu pokazuje, jak utworzyć transakcję zależną, aby zarządzać dwoma współbieżnymi zadaniami przez klonowanie transakcji zależnej i przekazanie jej do wątku roboczego.</span><span class="sxs-lookup"><span data-stu-id="cd750-123">The following code example shows how to create a dependent transaction to manage two concurrent tasks by cloning a dependent transaction and passing it to a worker thread.</span></span>  
  
```csharp  
public class WorkerThread  
{  
    public void DoWork(DependentTransaction dependentTransaction)  
    {  
        Thread thread = new Thread(ThreadMethod);  
        thread.Start(dependentTransaction);
    }  
  
    public void ThreadMethod(object transaction)
    {
        DependentTransaction dependentTransaction = transaction as DependentTransaction;  
        Debug.Assert(dependentTransaction != null);
        try  
        {  
            using(TransactionScope ts = new TransactionScope(dependentTransaction))  
            {  
                /* Perform transactional work here */
                ts.Complete();  
            }  
        }  
        finally  
        {  
            dependentTransaction.Complete();
             dependentTransaction.Dispose();
        }  
    }  
  
//Client code
using(TransactionScope scope = new TransactionScope())  
{  
    Transaction currentTransaction = Transaction.Current;  
    DependentTransaction dependentTransaction;
    dependentTransaction = currentTransaction.DependentClone(DependentCloneOption.BlockCommitUntilComplete);  
    WorkerThread workerThread = new WorkerThread();  
    workerThread.DoWork(dependentTransaction);  
    /* Do some transactional work here, then: */  
    scope.Complete();  
}  
```  
  
 <span data-ttu-id="cd750-124">Kod klienta tworzy zakres transakcji, który ustawia również otoczenia transakcji.</span><span class="sxs-lookup"><span data-stu-id="cd750-124">The client code creates a transactional scope that also sets the ambient transaction.</span></span> <span data-ttu-id="cd750-125">Transakcja otoczenia nie mają być przekazywane do wątku roboczego.</span><span class="sxs-lookup"><span data-stu-id="cd750-125">You should not pass the ambient transaction to the worker thread.</span></span> <span data-ttu-id="cd750-126">Zamiast tego należy sklonować bieżącej transakcji (otoczenia) przez wywołanie metody <xref:System.Transactions.Transaction.DependentClone%2A> metody w bieżącej transakcji i przekazać zależne od do wątku roboczego.</span><span class="sxs-lookup"><span data-stu-id="cd750-126">Instead, you should clone the current (ambient) transaction by calling the <xref:System.Transactions.Transaction.DependentClone%2A> method on the current transaction, and pass the dependent to the worker thread.</span></span>  
  
 <span data-ttu-id="cd750-127">`ThreadMethod` Metoda wykonuje na nowy wątek.</span><span class="sxs-lookup"><span data-stu-id="cd750-127">The `ThreadMethod` method executes on the new thread.</span></span> <span data-ttu-id="cd750-128">Klient uruchamia nowy wątek, przekazywania zależne transakcji jako `ThreadMethod` parametru.</span><span class="sxs-lookup"><span data-stu-id="cd750-128">The client starts a new thread, passing the dependent transaction as the `ThreadMethod` parameter.</span></span>  
  
 <span data-ttu-id="cd750-129">Ponieważ zależne transakcji jest tworzone z <xref:System.Transactions.DependentCloneOption.BlockCommitUntilComplete>, ma gwarancji, że nie można zatwierdzić transakcji, aż wszystkie transakcyjnych zadań wykonywanych na sekundę wątek został zakończony i <xref:System.Transactions.DependentTransaction.Complete%2A> jest wywoływana w transakcji zależnych.</span><span class="sxs-lookup"><span data-stu-id="cd750-129">Because the dependent transaction is created with <xref:System.Transactions.DependentCloneOption.BlockCommitUntilComplete>, you are guaranteed that the transaction cannot be committed until all of the transactional work done on the second thread is finished and <xref:System.Transactions.DependentTransaction.Complete%2A> is called on the dependent transaction.</span></span> <span data-ttu-id="cd750-130">Oznacza to, że jeśli zakres klienta zakończy się (gdy próbuje usunąć obiekt transakcji na końcu `using` instrukcji) przed wywołaniem nowego wątku <xref:System.Transactions.DependentTransaction.Complete%2A> w transakcji zależnej, kod klienta zostaje zablokować do momentu wywołania elementu <xref:System.Transactions.DependentTransaction.Complete%2A> zależnego.</span><span class="sxs-lookup"><span data-stu-id="cd750-130">This means that if the client's scope ends (when it tries to dispose of the transaction object at the end of the `using` statement) before the new thread calls <xref:System.Transactions.DependentTransaction.Complete%2A> on the dependent transaction, the client code blocks until <xref:System.Transactions.DependentTransaction.Complete%2A> is called on the dependent.</span></span> <span data-ttu-id="cd750-131">Następnie transakcji może zakończyć przekazywanie lub przerywanie.</span><span class="sxs-lookup"><span data-stu-id="cd750-131">Then the transaction can finish committing or aborting.</span></span>  
  
## <a name="concurrency-issues"></a><span data-ttu-id="cd750-132">Problemy z współbieżności</span><span class="sxs-lookup"><span data-stu-id="cd750-132">Concurrency Issues</span></span>  

 <span data-ttu-id="cd750-133">Istnieje kilka problemów współbieżności dodatkowe, które należy zwrócić uwagę podczas korzystania z <xref:System.Transactions.DependentTransaction> klasy:</span><span class="sxs-lookup"><span data-stu-id="cd750-133">There are a few additional concurrency issues that you need to be aware of when using the <xref:System.Transactions.DependentTransaction> class:</span></span>  
  
- <span data-ttu-id="cd750-134">Jeśli wątku roboczego powoduje wycofanie transakcji, ale nadrzędnego próbuje zatwierdzić, <xref:System.Transactions.TransactionAbortedException> zgłaszany.</span><span class="sxs-lookup"><span data-stu-id="cd750-134">If the worker thread rolls back the transaction but the parent tries to commit it, a <xref:System.Transactions.TransactionAbortedException> is thrown.</span></span>  
  
- <span data-ttu-id="cd750-135">Należy utworzyć nowy klon zależny dla każdego wątku roboczego w transakcji.</span><span class="sxs-lookup"><span data-stu-id="cd750-135">You should create a new dependent clone for each worker thread in the transaction.</span></span> <span data-ttu-id="cd750-136">Nie przekazuj tego samego klonu zależnego do wielu wątków, ponieważ tylko jeden z nich może wywoływać <xref:System.Transactions.DependentTransaction.Complete%2A> .</span><span class="sxs-lookup"><span data-stu-id="cd750-136">Do not pass the same dependent clone to multiple threads, because only one of them can call <xref:System.Transactions.DependentTransaction.Complete%2A> on it.</span></span>  
  
- <span data-ttu-id="cd750-137">Jeśli wątku roboczego spawns nowego wątku roboczego, upewnij się, że tworzenie klon zależny od klon zależny i przekazywanie ich do nowego wątku.</span><span class="sxs-lookup"><span data-stu-id="cd750-137">If the worker thread spawns a new worker thread, make sure to create a dependent clone from the dependent clone and pass it to the new thread.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="cd750-138">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="cd750-138">See also</span></span>

- <xref:System.Transactions.DependentTransaction>
