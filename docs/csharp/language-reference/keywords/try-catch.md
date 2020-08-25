---
title: Informacje o instrukcji try-catch-C#
ms.date: 07/20/2015
f1_keywords:
- try
- try_CSharpKeyword
- catch
- catch_CSharpKeyword
helpviewer_keywords:
- catch keyword [C#]
- try-catch statement [C#]
ms.assetid: cb5503c7-bfa1-4610-8fc2-ddcd2e84c438
ms.openlocfilehash: bb81ddbe631fedfcfe247c6e62580de679ad972f
ms.sourcegitcommit: 9c45035b781caebc63ec8ecf912dc83fb6723b1f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/25/2020
ms.locfileid: "88812305"
---
# <a name="try-catch-c-reference"></a><span data-ttu-id="e33b4-102">try-catch (odwołanie w C#)</span><span class="sxs-lookup"><span data-stu-id="e33b4-102">try-catch (C# Reference)</span></span>

<span data-ttu-id="e33b4-103">Instrukcja try-catch składa się z `try` bloku, po którym następuje co najmniej jedna `catch` klauzula, która określa programy obsługi dla różnych wyjątków.</span><span class="sxs-lookup"><span data-stu-id="e33b4-103">The try-catch statement consists of a `try` block followed by one or more `catch` clauses, which specify handlers for different exceptions.</span></span>

<span data-ttu-id="e33b4-104">Gdy wyjątek jest zgłaszany, środowisko uruchomieniowe języka wspólnego (CLR) wyszukuje `catch` instrukcję, która obsługuje ten wyjątek.</span><span class="sxs-lookup"><span data-stu-id="e33b4-104">When an exception is thrown, the common language runtime (CLR) looks for the `catch` statement that handles this exception.</span></span> <span data-ttu-id="e33b4-105">Jeśli aktualnie wykonywana metoda nie zawiera takiego `catch` bloku, środowisko CLR przegląda metodę, która wywołała bieżącą metodę, i tak dalej na stosie wywołań.</span><span class="sxs-lookup"><span data-stu-id="e33b4-105">If the currently executing method does not contain such a `catch` block, the CLR looks at the method that called the current method, and so on up the call stack.</span></span> <span data-ttu-id="e33b4-106">Jeśli nie `catch` zostanie znaleziony żaden blok, środowisko CLR wyświetli komunikat o nieobsługiwanym wyjątku dla użytkownika i zakończy wykonywanie programu.</span><span class="sxs-lookup"><span data-stu-id="e33b4-106">If no `catch` block is found, then the CLR displays an unhandled exception message to the user and stops execution of the program.</span></span>

<span data-ttu-id="e33b4-107">`try`Blok zawiera chroniony kod, który może spowodować wyjątek.</span><span class="sxs-lookup"><span data-stu-id="e33b4-107">The `try` block contains the guarded code that may cause the exception.</span></span> <span data-ttu-id="e33b4-108">Blok jest wykonywany do momentu wyrzucania wyjątku lub zostanie ukończony pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="e33b4-108">The block is executed until an exception is thrown or it is completed successfully.</span></span> <span data-ttu-id="e33b4-109">Na przykład następująca próba rzutowania `null` obiektu zgłasza <xref:System.NullReferenceException> wyjątek:</span><span class="sxs-lookup"><span data-stu-id="e33b4-109">For example, the following attempt to cast a `null` object raises the <xref:System.NullReferenceException> exception:</span></span>

```csharp
object o2 = null;
try
{
    int i2 = (int)o2;   // Error
}
```

<span data-ttu-id="e33b4-110">Chociaż `catch` klauzula może być używana bez argumentów do przechwytywania dowolnego typu wyjątku, to użycie nie jest zalecane.</span><span class="sxs-lookup"><span data-stu-id="e33b4-110">Although the `catch` clause can be used without arguments to catch any type of exception, this usage is not recommended.</span></span> <span data-ttu-id="e33b4-111">Ogólnie rzecz biorąc, należy jedynie przechwycić te wyjątki, z których wiadomo, jak odzyskać.</span><span class="sxs-lookup"><span data-stu-id="e33b4-111">In general, you should only catch those exceptions that you know how to recover from.</span></span> <span data-ttu-id="e33b4-112">W związku z tym zawsze należy określić argument obiektu pochodny <xref:System.Exception?displayProperty=nameWithType> na przykład:</span><span class="sxs-lookup"><span data-stu-id="e33b4-112">Therefore, you should always specify an object argument derived from <xref:System.Exception?displayProperty=nameWithType> For example:</span></span>

```csharp
catch (InvalidCastException e)
{
}
```

<span data-ttu-id="e33b4-113">Istnieje możliwość użycia więcej niż jednej `catch` klauzuli określonej w tej samej instrukcji try-catch.</span><span class="sxs-lookup"><span data-stu-id="e33b4-113">It is possible to use more than one specific `catch` clause in the same try-catch statement.</span></span> <span data-ttu-id="e33b4-114">W tym przypadku kolejność `catch` klauzul jest ważna, ponieważ `catch` klauzule są badane w kolejności.</span><span class="sxs-lookup"><span data-stu-id="e33b4-114">In this case, the order of the `catch` clauses is important because the `catch` clauses are examined in order.</span></span> <span data-ttu-id="e33b4-115">Przechwyć bardziej szczegółowe wyjątki przed bardziej szczegółowymi.</span><span class="sxs-lookup"><span data-stu-id="e33b4-115">Catch the more specific exceptions before the less specific ones.</span></span> <span data-ttu-id="e33b4-116">Kompilator generuje błąd w przypadku uporządkowania bloków catch w taki sposób, aby można było nigdy nie dotrzeć do późniejszego bloku.</span><span class="sxs-lookup"><span data-stu-id="e33b4-116">The compiler produces an error if you order your catch blocks so that a later block can never be reached.</span></span>

<span data-ttu-id="e33b4-117">Używanie `catch` argumentów jest jednym ze sposobów filtrowania wyjątków, które mają być obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="e33b4-117">Using `catch` arguments is one way to filter for the exceptions you want to handle.</span></span>  <span data-ttu-id="e33b4-118">Można również użyć filtru wyjątków, który dodatkowo bada wyjątek, aby zdecydować, czy go obsłużyć.</span><span class="sxs-lookup"><span data-stu-id="e33b4-118">You can also use an exception filter that further examines the exception to decide whether to handle it.</span></span>  <span data-ttu-id="e33b4-119">Jeśli filtr wyjątku zwraca wartość false, wyszukiwanie programu obsługi jest kontynuowane.</span><span class="sxs-lookup"><span data-stu-id="e33b4-119">If the exception filter returns false, then the search for a handler continues.</span></span>

```csharp
catch (ArgumentException e) when (e.ParamName == "…")
{
}
```

<span data-ttu-id="e33b4-120">Filtry wyjątków są preferowane do przechwytywania i ponownego zgłaszania (wyjaśniono poniżej), ponieważ filtry pozostawiają nienaruszony stos.</span><span class="sxs-lookup"><span data-stu-id="e33b4-120">Exception filters are preferable to catching and rethrowing (explained below) because filters leave the stack unharmed.</span></span>  <span data-ttu-id="e33b4-121">Jeśli w późniejszym czasie program obsługi będzie zrzucał stos, zobaczysz miejsce, z którego pochodzi wyjątek, a nie tylko ostatnie miejsce, które zostało ponownie zgłoszone.</span><span class="sxs-lookup"><span data-stu-id="e33b4-121">If a later handler dumps the stack, you can see where the exception originally came from, rather than just the last place it was rethrown.</span></span>  <span data-ttu-id="e33b4-122">Typowym zastosowaniem wyrażeń filtrów wyjątków jest rejestrowanie.</span><span class="sxs-lookup"><span data-stu-id="e33b4-122">A common use of exception filter expressions is logging.</span></span>  <span data-ttu-id="e33b4-123">Można utworzyć filtr, który zawsze zwraca wartość false, która również prowadzi do dziennika, można rejestrować wyjątki w miarę ich wykonywania, bez konieczności ich obsługi i ponownego zgłaszania.</span><span class="sxs-lookup"><span data-stu-id="e33b4-123">You can create a filter that always returns false that also outputs to a log, you can log exceptions as they go by without having to handle them and rethrow.</span></span>

<span data-ttu-id="e33b4-124">Instrukcji [throw](throw.md) można użyć w `catch` bloku, aby ponownie zgłosić wyjątek, który jest przechwytywany przez `catch` instrukcję.</span><span class="sxs-lookup"><span data-stu-id="e33b4-124">A [throw](throw.md) statement can be used in a `catch` block to re-throw the exception that is caught by the `catch` statement.</span></span> <span data-ttu-id="e33b4-125">Poniższy przykład wyodrębnia informacje źródłowe z <xref:System.IO.IOException> wyjątku, a następnie zgłasza wyjątek do metody nadrzędnej.</span><span class="sxs-lookup"><span data-stu-id="e33b4-125">The following example extracts source information from an <xref:System.IO.IOException> exception, and then throws the exception to the parent method.</span></span>

```csharp
catch (FileNotFoundException e)
{
    // FileNotFoundExceptions are handled here.
}
catch (IOException e)
{
    // Extract some information from this exception, and then
    // throw it to the parent method.
    if (e.Source != null)
        Console.WriteLine("IOException source: {0}", e.Source);
    throw;
}
```

<span data-ttu-id="e33b4-126">Możesz przechwytywać jeden wyjątek i zgłosić inny wyjątek.</span><span class="sxs-lookup"><span data-stu-id="e33b4-126">You can catch one exception and throw a different exception.</span></span> <span data-ttu-id="e33b4-127">Gdy to zrobisz, określ wyjątek, który został przechwycony jako wyjątek wewnętrzny, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="e33b4-127">When you do this, specify the exception that you caught as the inner exception, as shown in the following example.</span></span>

```csharp
catch (InvalidCastException e)
{
    // Perform some action here, and then throw a new exception.
    throw new YourCustomException("Put your error message here.", e);
}
```

<span data-ttu-id="e33b4-128">Możesz również ponownie zgłosić wyjątek, gdy określony warunek ma wartość true, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="e33b4-128">You can also re-throw an exception when a specified condition is true, as shown in the following example.</span></span>

```csharp
catch (InvalidCastException e)
{
    if (e.Data == null)
    {
        throw;
    }
    else
    {
        // Take some action.
    }
}
```

> [!NOTE]
> <span data-ttu-id="e33b4-129">Istnieje również możliwość użycia filtru wyjątków, aby uzyskać podobny wynik w sposób, który jest w sposób bardziej przejrzysty (a także bez modyfikowania stosu, jak wyjaśniono wcześniej w tym dokumencie).</span><span class="sxs-lookup"><span data-stu-id="e33b4-129">It is also possible to use an exception filter to get a similar result in an often cleaner fashion (as well as not modifying the stack, as explained earlier in this document).</span></span> <span data-ttu-id="e33b4-130">Poniższy przykład ma podobne zachowanie w przypadku wywołujących w poprzednim przykładzie.</span><span class="sxs-lookup"><span data-stu-id="e33b4-130">The following example has a similar behavior for callers as the previous example.</span></span> <span data-ttu-id="e33b4-131">Funkcja zwraca z `InvalidCastException` powrotem do obiektu wywołującego, gdy `e.Data` ma wartość `null` .</span><span class="sxs-lookup"><span data-stu-id="e33b4-131">The function throws the `InvalidCastException` back to the caller when `e.Data` is `null`.</span></span>
>
> ```csharp
> catch (InvalidCastException e) when (e.Data != null)
> {
>     // Take some action.
> }
> ```

<span data-ttu-id="e33b4-132">Z wewnątrz `try` bloku należy inicjować tylko zmienne, które są w nim zadeklarowane.</span><span class="sxs-lookup"><span data-stu-id="e33b4-132">From inside a `try` block, initialize only variables that are declared therein.</span></span> <span data-ttu-id="e33b4-133">W przeciwnym razie może wystąpić wyjątek przed ukończeniem wykonywania bloku.</span><span class="sxs-lookup"><span data-stu-id="e33b4-133">Otherwise, an exception can occur before the execution of the block is completed.</span></span> <span data-ttu-id="e33b4-134">Na przykład, w poniższym przykładzie kodu zmienna `n` jest inicjowana wewnątrz `try` bloku.</span><span class="sxs-lookup"><span data-stu-id="e33b4-134">For example, in the following code example, the variable `n` is initialized inside the `try` block.</span></span> <span data-ttu-id="e33b4-135">Próba użycia tej zmiennej poza `try` blokiem w `Write(n)` instrukcji spowoduje wygenerowanie błędu kompilatora.</span><span class="sxs-lookup"><span data-stu-id="e33b4-135">An attempt to use this variable outside the `try` block in the `Write(n)` statement will generate a compiler error.</span></span>

```csharp
static void Main()
{
    int n;
    try
    {
        // Do not initialize this variable here.
        n = 123;
    }
    catch
    {
    }
    // Error: Use of unassigned local variable 'n'.
    Console.Write(n);
}
```

<span data-ttu-id="e33b4-136">Aby uzyskać więcej informacji na temat catch, zobacz [try-catch-finally](try-catch-finally.md).</span><span class="sxs-lookup"><span data-stu-id="e33b4-136">For more information about catch, see [try-catch-finally](try-catch-finally.md).</span></span>

## <a name="exceptions-in-async-methods"></a><span data-ttu-id="e33b4-137">Wyjątki w metodach asynchronicznych</span><span class="sxs-lookup"><span data-stu-id="e33b4-137">Exceptions in async methods</span></span>

<span data-ttu-id="e33b4-138">Metoda asynchroniczna jest oznaczona przez modyfikator  [Async](async.md) i zwykle zawiera co najmniej jedno wyrażenie lub instrukcje await.</span><span class="sxs-lookup"><span data-stu-id="e33b4-138">An async method is marked  by an  [async](async.md) modifier and usually contains one or more await expressions or statements.</span></span> <span data-ttu-id="e33b4-139">Wyrażenie await stosuje operator [await](../operators/await.md) do <xref:System.Threading.Tasks.Task> lub <xref:System.Threading.Tasks.Task%601> .</span><span class="sxs-lookup"><span data-stu-id="e33b4-139">An await expression applies the [await](../operators/await.md) operator to a <xref:System.Threading.Tasks.Task> or <xref:System.Threading.Tasks.Task%601>.</span></span>

<span data-ttu-id="e33b4-140">Gdy kontrolka osiągnie `await` wartość w metodzie asynchronicznej, postęp w metodzie jest zawieszony do momentu zakończenia zadania oczekiwania.</span><span class="sxs-lookup"><span data-stu-id="e33b4-140">When control reaches an `await` in the async method, progress in the method is suspended until the awaited task completes.</span></span> <span data-ttu-id="e33b4-141">Po zakończeniu zadania wykonywanie może zostać wznowione w metodzie.</span><span class="sxs-lookup"><span data-stu-id="e33b4-141">When the task  is complete, execution can resume in the method.</span></span> <span data-ttu-id="e33b4-142">Aby uzyskać więcej informacji, zobacz [programowanie asynchroniczne z Async i await](../../programming-guide/concepts/async/index.md).</span><span class="sxs-lookup"><span data-stu-id="e33b4-142">For more information, see [Asynchronous programming with async and await](../../programming-guide/concepts/async/index.md).</span></span>

<span data-ttu-id="e33b4-143">Ukończone zadanie, do którego `await` zastosowano, może być w stanie awarii z powodu nieobsłużonego wyjątku w metodzie, która zwraca zadanie.</span><span class="sxs-lookup"><span data-stu-id="e33b4-143">The completed task to which `await` is applied might be in a faulted state because of an unhandled exception in the method that returns the task.</span></span> <span data-ttu-id="e33b4-144">Oczekiwanie na zadanie zgłosi wyjątek.</span><span class="sxs-lookup"><span data-stu-id="e33b4-144">Awaiting the task throws an exception.</span></span> <span data-ttu-id="e33b4-145">Zadanie można także zakończyć w stanie anulowanym, jeśli asynchroniczny proces zwraca go.</span><span class="sxs-lookup"><span data-stu-id="e33b4-145">A task can also end up in a canceled state if the asynchronous process that returns it is canceled.</span></span> <span data-ttu-id="e33b4-146">Oczekiwanie na anulowane zadanie wyrzuca `OperationCanceledException` .</span><span class="sxs-lookup"><span data-stu-id="e33b4-146">Awaiting a canceled task throws an `OperationCanceledException`.</span></span>

<span data-ttu-id="e33b4-147">Aby wychwycić wyjątek, oczekiwanie na zadanie w `try` bloku i Przechwyć wyjątek w skojarzonym `catch` bloku.</span><span class="sxs-lookup"><span data-stu-id="e33b4-147">To catch the exception, await the task in a `try` block, and catch the exception in the associated `catch` block.</span></span> <span data-ttu-id="e33b4-148">Aby zapoznać się z przykładem, zobacz sekcję dotyczącą [przykładu metody asynchronicznej](#async-method-example) .</span><span class="sxs-lookup"><span data-stu-id="e33b4-148">For an example, see the [Async method example](#async-method-example) section.</span></span>

<span data-ttu-id="e33b4-149">Zadanie może być w stanie nieprawidłowym, ponieważ wystąpiły wiele wyjątków w metodzie asynchronicznej oczekiwania.</span><span class="sxs-lookup"><span data-stu-id="e33b4-149">A task can be in a faulted state because multiple exceptions occurred in the awaited async method.</span></span> <span data-ttu-id="e33b4-150">Na przykład zadanie może być wynikiem wywołania metody <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType> .</span><span class="sxs-lookup"><span data-stu-id="e33b4-150">For example, the task might be the result of a call to <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType>.</span></span> <span data-ttu-id="e33b4-151">Podczas oczekiwania na takie zadanie zostanie przechwycony tylko jeden z wyjątków i nie będzie można przewidzieć, który wyjątek zostanie przechwycony.</span><span class="sxs-lookup"><span data-stu-id="e33b4-151">When you await such a task, only one of the exceptions is caught, and you can't predict which exception will be caught.</span></span> <span data-ttu-id="e33b4-152">Aby zapoznać się z przykładem, zapoznaj się z sekcją [przykład Task. WhenAll](#taskwhenall-example) .</span><span class="sxs-lookup"><span data-stu-id="e33b4-152">For an example, see the [Task.WhenAll example](#taskwhenall-example) section.</span></span>

## <a name="example"></a><span data-ttu-id="e33b4-153">Przykład</span><span class="sxs-lookup"><span data-stu-id="e33b4-153">Example</span></span>

<span data-ttu-id="e33b4-154">W poniższym przykładzie `try` blok zawiera wywołanie `ProcessString` metody, która może spowodować wyjątek.</span><span class="sxs-lookup"><span data-stu-id="e33b4-154">In the following example, the `try` block contains a call to the `ProcessString` method that may cause an exception.</span></span> <span data-ttu-id="e33b4-155">`catch`Klauzula zawiera procedurę obsługi wyjątków, która po prostu wyświetla komunikat na ekranie.</span><span class="sxs-lookup"><span data-stu-id="e33b4-155">The `catch` clause contains the exception handler that just displays a message on the screen.</span></span> <span data-ttu-id="e33b4-156">Gdy `throw` instrukcja jest wywoływana z wewnątrz `ProcessString` , system szuka `catch` instrukcji i wyświetla komunikat `Exception caught` .</span><span class="sxs-lookup"><span data-stu-id="e33b4-156">When the `throw` statement is called from inside `ProcessString`, the system looks for the `catch` statement and displays the message `Exception caught`.</span></span>

[!code-csharp[csrefKeywordsExceptions#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsExceptions/CS/csrefKeywordsExceptions.cs#2)]

## <a name="two-catch-blocks-example"></a><span data-ttu-id="e33b4-157">Przykład dwóch bloków catch</span><span class="sxs-lookup"><span data-stu-id="e33b4-157">Two catch blocks example</span></span>

<span data-ttu-id="e33b4-158">W poniższym przykładzie są używane dwa bloki catch, a najbardziej konkretny wyjątek, który jest pierwszy, jest przechwytywany.</span><span class="sxs-lookup"><span data-stu-id="e33b4-158">In the following example, two catch blocks are used, and the most specific exception, which comes first, is caught.</span></span>

<span data-ttu-id="e33b4-159">Aby przechwycić najmniejszy konkretny wyjątek, można zastąpić instrukcję throw przy `ProcessString` użyciu następującej instrukcji: `throw new Exception()` .</span><span class="sxs-lookup"><span data-stu-id="e33b4-159">To catch the least specific exception, you can replace the throw statement in `ProcessString` with the following statement: `throw new Exception()`.</span></span>

<span data-ttu-id="e33b4-160">W przypadku umieszczenia bloku catch o najniższym poziomie najpierw w tym przykładzie zostanie wyświetlony następujący komunikat o błędzie: `A previous catch clause already catches all exceptions of this or a super type ('System.Exception')` .</span><span class="sxs-lookup"><span data-stu-id="e33b4-160">If you place the least-specific catch block first in the example, the following  error message appears: `A previous catch clause already catches all exceptions of this or a super type ('System.Exception')`.</span></span>

[!code-csharp[csrefKeywordsExceptions#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsExceptions/CS/csrefKeywordsExceptions.cs#3)]

## <a name="async-method-example"></a><span data-ttu-id="e33b4-161">Przykład metody asynchronicznej</span><span class="sxs-lookup"><span data-stu-id="e33b4-161">Async method example</span></span>

<span data-ttu-id="e33b4-162">Poniższy przykład ilustruje obsługę wyjątków dla metod asynchronicznych.</span><span class="sxs-lookup"><span data-stu-id="e33b4-162">The following example illustrates exception handling for async methods.</span></span> <span data-ttu-id="e33b4-163">Aby przechwytywać wyjątek, który generuje zadanie asynchroniczne, umieść `await` wyrażenie w `try` bloku i Przechwyć wyjątek w `catch` bloku.</span><span class="sxs-lookup"><span data-stu-id="e33b4-163">To catch an exception that an async task throws, place the `await` expression in a `try` block, and catch the exception in a `catch` block.</span></span>

<span data-ttu-id="e33b4-164">Usuń komentarz `throw new Exception` wiersza z przykładu, aby zademonstrować obsługę wyjątków.</span><span class="sxs-lookup"><span data-stu-id="e33b4-164">Uncomment the `throw new Exception` line in the example to demonstrate exception handling.</span></span> <span data-ttu-id="e33b4-165">`IsFaulted`Właściwość zadania jest ustawiona na `True` , `Exception.InnerException` Właściwość zadania jest ustawiana na wyjątek, a wyjątek jest przechwytywany w `catch` bloku.</span><span class="sxs-lookup"><span data-stu-id="e33b4-165">The task's `IsFaulted` property is set to `True`, the task's `Exception.InnerException` property is set to the exception, and the exception is caught in the `catch` block.</span></span>

<span data-ttu-id="e33b4-166">Usuń komentarz z `throw new OperationCanceledException` wiersza, aby zademonstrować, co się dzieje po anulowaniu procesu asynchronicznego.</span><span class="sxs-lookup"><span data-stu-id="e33b4-166">Uncomment the `throw new OperationCanceledException` line to demonstrate what happens when you cancel an asynchronous process.</span></span> <span data-ttu-id="e33b4-167">`IsCanceled`Właściwość zadania jest ustawiona na `true` , a wyjątek jest przechwytywany w `catch` bloku.</span><span class="sxs-lookup"><span data-stu-id="e33b4-167">The task's `IsCanceled` property is set to `true`, and the exception is caught in the `catch` block.</span></span> <span data-ttu-id="e33b4-168">W przypadku niektórych warunków, które nie dotyczą tego przykładu, `IsFaulted` Właściwość zadania jest ustawiona na `true` i `IsCanceled` jest ustawiona na `false` .</span><span class="sxs-lookup"><span data-stu-id="e33b4-168">Under some conditions that don't apply to this example, the task's `IsFaulted` property is set to `true` and `IsCanceled` is set to `false`.</span></span>

[!code-csharp[csAsyncExceptions#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csasyncexceptions/cs/class1.cs#2)]  

## <a name="taskwhenall-example"></a><span data-ttu-id="e33b4-169">Task. WhenAll — przykład</span><span class="sxs-lookup"><span data-stu-id="e33b4-169">Task.WhenAll example</span></span>

<span data-ttu-id="e33b4-170">Poniższy przykład ilustruje obsługę wyjątków, gdy wiele zadań może skutkować wieloma wyjątkami.</span><span class="sxs-lookup"><span data-stu-id="e33b4-170">The following example illustrates exception handling where multiple tasks can result in multiple exceptions.</span></span> <span data-ttu-id="e33b4-171">`try`Blok oczekuje zadania, które jest zwracane przez wywołanie metody <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType> .</span><span class="sxs-lookup"><span data-stu-id="e33b4-171">The `try` block awaits the task that's returned by a call to <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType>.</span></span> <span data-ttu-id="e33b4-172">Zadanie zostanie ukończone, gdy zostaną wykonane trzy zadania, do których zastosowano WhenAll.</span><span class="sxs-lookup"><span data-stu-id="e33b4-172">The task is complete when the three tasks to which WhenAll is applied are complete.</span></span>

<span data-ttu-id="e33b4-173">Każdy z tych trzech zadań powoduje wyjątek.</span><span class="sxs-lookup"><span data-stu-id="e33b4-173">Each of the three tasks causes an exception.</span></span> <span data-ttu-id="e33b4-174">`catch`Blok wykonuje iterację w wyjątkach, które są dostępne we `Exception.InnerExceptions` właściwości zadania, które zostało zwrócone przez <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType> .</span><span class="sxs-lookup"><span data-stu-id="e33b4-174">The `catch` block iterates through the exceptions, which are found in the `Exception.InnerExceptions` property of the task that was returned by <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType>.</span></span>

[!code-csharp[csAsyncExceptions#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csasyncexceptions/cs/class1.cs#4)]

## <a name="c-language-specification"></a><span data-ttu-id="e33b4-175">specyfikacja języka C#</span><span class="sxs-lookup"><span data-stu-id="e33b4-175">C# language specification</span></span>

<span data-ttu-id="e33b4-176">Aby uzyskać więcej informacji, zobacz sekcję [try instrukcji](~/_csharplang/spec/statements.md#the-try-statement) w [specyfikacji języka C#](~/_csharplang/spec/introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e33b4-176">For more information, see [The try statement](~/_csharplang/spec/statements.md#the-try-statement) section of the [C# language specification](~/_csharplang/spec/introduction.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="e33b4-177">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="e33b4-177">See also</span></span>

- [<span data-ttu-id="e33b4-178">Odwołanie w C#</span><span class="sxs-lookup"><span data-stu-id="e33b4-178">C# Reference</span></span>](../index.md)
- [<span data-ttu-id="e33b4-179">Przewodnik programowania w języku C#</span><span class="sxs-lookup"><span data-stu-id="e33b4-179">C# Programming Guide</span></span>](../../programming-guide/index.md)
- [<span data-ttu-id="e33b4-180">Słowa kluczowe języka C#</span><span class="sxs-lookup"><span data-stu-id="e33b4-180">C# Keywords</span></span>](index.md)
- [<span data-ttu-id="e33b4-181">Instrukcje try, throw i catch (C++)</span><span class="sxs-lookup"><span data-stu-id="e33b4-181">try, throw, and catch Statements (C++)</span></span>](/cpp/cpp/try-throw-and-catch-statements-cpp)
- [<span data-ttu-id="e33b4-182">throw</span><span class="sxs-lookup"><span data-stu-id="e33b4-182">throw</span></span>](throw.md)
- [<span data-ttu-id="e33b4-183">try-finally</span><span class="sxs-lookup"><span data-stu-id="e33b4-183">try-finally</span></span>](try-finally.md)
- [<span data-ttu-id="e33b4-184">Instrukcje: Jawne zgłaszanie wyjątków</span><span class="sxs-lookup"><span data-stu-id="e33b4-184">How to: Explicitly Throw Exceptions</span></span>](../../../standard/exceptions/how-to-explicitly-throw-exceptions.md)
