---
description: Informacje o instrukcji try-catch-C#
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
ms.openlocfilehash: e3154da2103029f704abd6873d16d372f1ae19ac
ms.sourcegitcommit: d579fb5e4b46745fd0f1f8874c94c6469ce58604
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/30/2020
ms.locfileid: "89142001"
---
# <a name="try-catch-c-reference"></a><span data-ttu-id="00ff4-103">try-catch (odwołanie w C#)</span><span class="sxs-lookup"><span data-stu-id="00ff4-103">try-catch (C# Reference)</span></span>

<span data-ttu-id="00ff4-104">Instrukcja try-catch składa się z `try` bloku, po którym następuje co najmniej jedna `catch` klauzula, która określa programy obsługi dla różnych wyjątków.</span><span class="sxs-lookup"><span data-stu-id="00ff4-104">The try-catch statement consists of a `try` block followed by one or more `catch` clauses, which specify handlers for different exceptions.</span></span>

<span data-ttu-id="00ff4-105">Gdy wyjątek jest zgłaszany, środowisko uruchomieniowe języka wspólnego (CLR) wyszukuje `catch` instrukcję, która obsługuje ten wyjątek.</span><span class="sxs-lookup"><span data-stu-id="00ff4-105">When an exception is thrown, the common language runtime (CLR) looks for the `catch` statement that handles this exception.</span></span> <span data-ttu-id="00ff4-106">Jeśli aktualnie wykonywana metoda nie zawiera takiego `catch` bloku, środowisko CLR przegląda metodę, która wywołała bieżącą metodę, i tak dalej na stosie wywołań.</span><span class="sxs-lookup"><span data-stu-id="00ff4-106">If the currently executing method does not contain such a `catch` block, the CLR looks at the method that called the current method, and so on up the call stack.</span></span> <span data-ttu-id="00ff4-107">Jeśli nie `catch` zostanie znaleziony żaden blok, środowisko CLR wyświetli komunikat o nieobsługiwanym wyjątku dla użytkownika i zakończy wykonywanie programu.</span><span class="sxs-lookup"><span data-stu-id="00ff4-107">If no `catch` block is found, then the CLR displays an unhandled exception message to the user and stops execution of the program.</span></span>

<span data-ttu-id="00ff4-108">`try`Blok zawiera chroniony kod, który może spowodować wyjątek.</span><span class="sxs-lookup"><span data-stu-id="00ff4-108">The `try` block contains the guarded code that may cause the exception.</span></span> <span data-ttu-id="00ff4-109">Blok jest wykonywany do momentu wyrzucania wyjątku lub zostanie ukończony pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="00ff4-109">The block is executed until an exception is thrown or it is completed successfully.</span></span> <span data-ttu-id="00ff4-110">Na przykład następująca próba rzutowania `null` obiektu zgłasza <xref:System.NullReferenceException> wyjątek:</span><span class="sxs-lookup"><span data-stu-id="00ff4-110">For example, the following attempt to cast a `null` object raises the <xref:System.NullReferenceException> exception:</span></span>

```csharp
object o2 = null;
try
{
    int i2 = (int)o2;   // Error
}
```

<span data-ttu-id="00ff4-111">Chociaż `catch` klauzula może być używana bez argumentów do przechwytywania dowolnego typu wyjątku, to użycie nie jest zalecane.</span><span class="sxs-lookup"><span data-stu-id="00ff4-111">Although the `catch` clause can be used without arguments to catch any type of exception, this usage is not recommended.</span></span> <span data-ttu-id="00ff4-112">Ogólnie rzecz biorąc, należy jedynie przechwycić te wyjątki, z których wiadomo, jak odzyskać.</span><span class="sxs-lookup"><span data-stu-id="00ff4-112">In general, you should only catch those exceptions that you know how to recover from.</span></span> <span data-ttu-id="00ff4-113">W związku z tym zawsze należy określić argument obiektu pochodny <xref:System.Exception?displayProperty=nameWithType> na przykład:</span><span class="sxs-lookup"><span data-stu-id="00ff4-113">Therefore, you should always specify an object argument derived from <xref:System.Exception?displayProperty=nameWithType> For example:</span></span>

```csharp
catch (InvalidCastException e)
{
}
```

<span data-ttu-id="00ff4-114">Istnieje możliwość użycia więcej niż jednej `catch` klauzuli określonej w tej samej instrukcji try-catch.</span><span class="sxs-lookup"><span data-stu-id="00ff4-114">It is possible to use more than one specific `catch` clause in the same try-catch statement.</span></span> <span data-ttu-id="00ff4-115">W tym przypadku kolejność `catch` klauzul jest ważna, ponieważ `catch` klauzule są badane w kolejności.</span><span class="sxs-lookup"><span data-stu-id="00ff4-115">In this case, the order of the `catch` clauses is important because the `catch` clauses are examined in order.</span></span> <span data-ttu-id="00ff4-116">Przechwyć bardziej szczegółowe wyjątki przed bardziej szczegółowymi.</span><span class="sxs-lookup"><span data-stu-id="00ff4-116">Catch the more specific exceptions before the less specific ones.</span></span> <span data-ttu-id="00ff4-117">Kompilator generuje błąd w przypadku uporządkowania bloków catch w taki sposób, aby można było nigdy nie dotrzeć do późniejszego bloku.</span><span class="sxs-lookup"><span data-stu-id="00ff4-117">The compiler produces an error if you order your catch blocks so that a later block can never be reached.</span></span>

<span data-ttu-id="00ff4-118">Używanie `catch` argumentów jest jednym ze sposobów filtrowania wyjątków, które mają być obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="00ff4-118">Using `catch` arguments is one way to filter for the exceptions you want to handle.</span></span>  <span data-ttu-id="00ff4-119">Można również użyć filtru wyjątków, który dodatkowo bada wyjątek, aby zdecydować, czy go obsłużyć.</span><span class="sxs-lookup"><span data-stu-id="00ff4-119">You can also use an exception filter that further examines the exception to decide whether to handle it.</span></span>  <span data-ttu-id="00ff4-120">Jeśli filtr wyjątku zwraca wartość false, wyszukiwanie programu obsługi jest kontynuowane.</span><span class="sxs-lookup"><span data-stu-id="00ff4-120">If the exception filter returns false, then the search for a handler continues.</span></span>

```csharp
catch (ArgumentException e) when (e.ParamName == "…")
{
}
```

<span data-ttu-id="00ff4-121">Filtry wyjątków są preferowane do przechwytywania i ponownego zgłaszania (wyjaśniono poniżej), ponieważ filtry pozostawiają nienaruszony stos.</span><span class="sxs-lookup"><span data-stu-id="00ff4-121">Exception filters are preferable to catching and rethrowing (explained below) because filters leave the stack unharmed.</span></span>  <span data-ttu-id="00ff4-122">Jeśli w późniejszym czasie program obsługi będzie zrzucał stos, zobaczysz miejsce, z którego pochodzi wyjątek, a nie tylko ostatnie miejsce, które zostało ponownie zgłoszone.</span><span class="sxs-lookup"><span data-stu-id="00ff4-122">If a later handler dumps the stack, you can see where the exception originally came from, rather than just the last place it was rethrown.</span></span>  <span data-ttu-id="00ff4-123">Typowym zastosowaniem wyrażeń filtrów wyjątków jest rejestrowanie.</span><span class="sxs-lookup"><span data-stu-id="00ff4-123">A common use of exception filter expressions is logging.</span></span>  <span data-ttu-id="00ff4-124">Można utworzyć filtr, który zawsze zwraca wartość false, która również prowadzi do dziennika, można rejestrować wyjątki w miarę ich wykonywania, bez konieczności ich obsługi i ponownego zgłaszania.</span><span class="sxs-lookup"><span data-stu-id="00ff4-124">You can create a filter that always returns false that also outputs to a log, you can log exceptions as they go by without having to handle them and rethrow.</span></span>

<span data-ttu-id="00ff4-125">Instrukcji [throw](throw.md) można użyć w `catch` bloku, aby ponownie zgłosić wyjątek, który jest przechwytywany przez `catch` instrukcję.</span><span class="sxs-lookup"><span data-stu-id="00ff4-125">A [throw](throw.md) statement can be used in a `catch` block to re-throw the exception that is caught by the `catch` statement.</span></span> <span data-ttu-id="00ff4-126">Poniższy przykład wyodrębnia informacje źródłowe z <xref:System.IO.IOException> wyjątku, a następnie zgłasza wyjątek do metody nadrzędnej.</span><span class="sxs-lookup"><span data-stu-id="00ff4-126">The following example extracts source information from an <xref:System.IO.IOException> exception, and then throws the exception to the parent method.</span></span>

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

<span data-ttu-id="00ff4-127">Możesz przechwytywać jeden wyjątek i zgłosić inny wyjątek.</span><span class="sxs-lookup"><span data-stu-id="00ff4-127">You can catch one exception and throw a different exception.</span></span> <span data-ttu-id="00ff4-128">Gdy to zrobisz, określ wyjątek, który został przechwycony jako wyjątek wewnętrzny, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="00ff4-128">When you do this, specify the exception that you caught as the inner exception, as shown in the following example.</span></span>

```csharp
catch (InvalidCastException e)
{
    // Perform some action here, and then throw a new exception.
    throw new YourCustomException("Put your error message here.", e);
}
```

<span data-ttu-id="00ff4-129">Możesz również ponownie zgłosić wyjątek, gdy określony warunek ma wartość true, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="00ff4-129">You can also re-throw an exception when a specified condition is true, as shown in the following example.</span></span>

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
> <span data-ttu-id="00ff4-130">Istnieje również możliwość użycia filtru wyjątków, aby uzyskać podobny wynik w sposób, który jest w sposób bardziej przejrzysty (a także bez modyfikowania stosu, jak wyjaśniono wcześniej w tym dokumencie).</span><span class="sxs-lookup"><span data-stu-id="00ff4-130">It is also possible to use an exception filter to get a similar result in an often cleaner fashion (as well as not modifying the stack, as explained earlier in this document).</span></span> <span data-ttu-id="00ff4-131">Poniższy przykład ma podobne zachowanie w przypadku wywołujących w poprzednim przykładzie.</span><span class="sxs-lookup"><span data-stu-id="00ff4-131">The following example has a similar behavior for callers as the previous example.</span></span> <span data-ttu-id="00ff4-132">Funkcja zwraca z `InvalidCastException` powrotem do obiektu wywołującego, gdy `e.Data` ma wartość `null` .</span><span class="sxs-lookup"><span data-stu-id="00ff4-132">The function throws the `InvalidCastException` back to the caller when `e.Data` is `null`.</span></span>
>
> ```csharp
> catch (InvalidCastException e) when (e.Data != null)
> {
>     // Take some action.
> }
> ```

<span data-ttu-id="00ff4-133">Z wewnątrz `try` bloku należy inicjować tylko zmienne, które są w nim zadeklarowane.</span><span class="sxs-lookup"><span data-stu-id="00ff4-133">From inside a `try` block, initialize only variables that are declared therein.</span></span> <span data-ttu-id="00ff4-134">W przeciwnym razie może wystąpić wyjątek przed ukończeniem wykonywania bloku.</span><span class="sxs-lookup"><span data-stu-id="00ff4-134">Otherwise, an exception can occur before the execution of the block is completed.</span></span> <span data-ttu-id="00ff4-135">Na przykład, w poniższym przykładzie kodu zmienna `n` jest inicjowana wewnątrz `try` bloku.</span><span class="sxs-lookup"><span data-stu-id="00ff4-135">For example, in the following code example, the variable `n` is initialized inside the `try` block.</span></span> <span data-ttu-id="00ff4-136">Próba użycia tej zmiennej poza `try` blokiem w `Write(n)` instrukcji spowoduje wygenerowanie błędu kompilatora.</span><span class="sxs-lookup"><span data-stu-id="00ff4-136">An attempt to use this variable outside the `try` block in the `Write(n)` statement will generate a compiler error.</span></span>

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

<span data-ttu-id="00ff4-137">Aby uzyskać więcej informacji na temat catch, zobacz [try-catch-finally](try-catch-finally.md).</span><span class="sxs-lookup"><span data-stu-id="00ff4-137">For more information about catch, see [try-catch-finally](try-catch-finally.md).</span></span>

## <a name="exceptions-in-async-methods"></a><span data-ttu-id="00ff4-138">Wyjątki w metodach asynchronicznych</span><span class="sxs-lookup"><span data-stu-id="00ff4-138">Exceptions in async methods</span></span>

<span data-ttu-id="00ff4-139">Metoda asynchroniczna jest oznaczona przez modyfikator  [Async](async.md) i zwykle zawiera co najmniej jedno wyrażenie lub instrukcje await.</span><span class="sxs-lookup"><span data-stu-id="00ff4-139">An async method is marked  by an  [async](async.md) modifier and usually contains one or more await expressions or statements.</span></span> <span data-ttu-id="00ff4-140">Wyrażenie await stosuje operator [await](../operators/await.md) do <xref:System.Threading.Tasks.Task> lub <xref:System.Threading.Tasks.Task%601> .</span><span class="sxs-lookup"><span data-stu-id="00ff4-140">An await expression applies the [await](../operators/await.md) operator to a <xref:System.Threading.Tasks.Task> or <xref:System.Threading.Tasks.Task%601>.</span></span>

<span data-ttu-id="00ff4-141">Gdy kontrolka osiągnie `await` wartość w metodzie asynchronicznej, postęp w metodzie jest zawieszony do momentu zakończenia zadania oczekiwania.</span><span class="sxs-lookup"><span data-stu-id="00ff4-141">When control reaches an `await` in the async method, progress in the method is suspended until the awaited task completes.</span></span> <span data-ttu-id="00ff4-142">Po zakończeniu zadania wykonywanie może zostać wznowione w metodzie.</span><span class="sxs-lookup"><span data-stu-id="00ff4-142">When the task  is complete, execution can resume in the method.</span></span> <span data-ttu-id="00ff4-143">Aby uzyskać więcej informacji, zobacz [programowanie asynchroniczne z Async i await](../../programming-guide/concepts/async/index.md).</span><span class="sxs-lookup"><span data-stu-id="00ff4-143">For more information, see [Asynchronous programming with async and await](../../programming-guide/concepts/async/index.md).</span></span>

<span data-ttu-id="00ff4-144">Ukończone zadanie, do którego `await` zastosowano, może być w stanie awarii z powodu nieobsłużonego wyjątku w metodzie, która zwraca zadanie.</span><span class="sxs-lookup"><span data-stu-id="00ff4-144">The completed task to which `await` is applied might be in a faulted state because of an unhandled exception in the method that returns the task.</span></span> <span data-ttu-id="00ff4-145">Oczekiwanie na zadanie zgłosi wyjątek.</span><span class="sxs-lookup"><span data-stu-id="00ff4-145">Awaiting the task throws an exception.</span></span> <span data-ttu-id="00ff4-146">Zadanie można także zakończyć w stanie anulowanym, jeśli asynchroniczny proces zwraca go.</span><span class="sxs-lookup"><span data-stu-id="00ff4-146">A task can also end up in a canceled state if the asynchronous process that returns it is canceled.</span></span> <span data-ttu-id="00ff4-147">Oczekiwanie na anulowane zadanie wyrzuca `OperationCanceledException` .</span><span class="sxs-lookup"><span data-stu-id="00ff4-147">Awaiting a canceled task throws an `OperationCanceledException`.</span></span>

<span data-ttu-id="00ff4-148">Aby wychwycić wyjątek, oczekiwanie na zadanie w `try` bloku i Przechwyć wyjątek w skojarzonym `catch` bloku.</span><span class="sxs-lookup"><span data-stu-id="00ff4-148">To catch the exception, await the task in a `try` block, and catch the exception in the associated `catch` block.</span></span> <span data-ttu-id="00ff4-149">Aby zapoznać się z przykładem, zobacz sekcję dotyczącą [przykładu metody asynchronicznej](#async-method-example) .</span><span class="sxs-lookup"><span data-stu-id="00ff4-149">For an example, see the [Async method example](#async-method-example) section.</span></span>

<span data-ttu-id="00ff4-150">Zadanie może być w stanie nieprawidłowym, ponieważ wystąpiły wiele wyjątków w metodzie asynchronicznej oczekiwania.</span><span class="sxs-lookup"><span data-stu-id="00ff4-150">A task can be in a faulted state because multiple exceptions occurred in the awaited async method.</span></span> <span data-ttu-id="00ff4-151">Na przykład zadanie może być wynikiem wywołania metody <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType> .</span><span class="sxs-lookup"><span data-stu-id="00ff4-151">For example, the task might be the result of a call to <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType>.</span></span> <span data-ttu-id="00ff4-152">Podczas oczekiwania na takie zadanie zostanie przechwycony tylko jeden z wyjątków i nie będzie można przewidzieć, który wyjątek zostanie przechwycony.</span><span class="sxs-lookup"><span data-stu-id="00ff4-152">When you await such a task, only one of the exceptions is caught, and you can't predict which exception will be caught.</span></span> <span data-ttu-id="00ff4-153">Aby zapoznać się z przykładem, zapoznaj się z sekcją [przykład Task. WhenAll](#taskwhenall-example) .</span><span class="sxs-lookup"><span data-stu-id="00ff4-153">For an example, see the [Task.WhenAll example](#taskwhenall-example) section.</span></span>

## <a name="example"></a><span data-ttu-id="00ff4-154">Przykład</span><span class="sxs-lookup"><span data-stu-id="00ff4-154">Example</span></span>

<span data-ttu-id="00ff4-155">W poniższym przykładzie `try` blok zawiera wywołanie `ProcessString` metody, która może spowodować wyjątek.</span><span class="sxs-lookup"><span data-stu-id="00ff4-155">In the following example, the `try` block contains a call to the `ProcessString` method that may cause an exception.</span></span> <span data-ttu-id="00ff4-156">`catch`Klauzula zawiera procedurę obsługi wyjątków, która po prostu wyświetla komunikat na ekranie.</span><span class="sxs-lookup"><span data-stu-id="00ff4-156">The `catch` clause contains the exception handler that just displays a message on the screen.</span></span> <span data-ttu-id="00ff4-157">Gdy `throw` instrukcja jest wywoływana z wewnątrz `ProcessString` , system szuka `catch` instrukcji i wyświetla komunikat `Exception caught` .</span><span class="sxs-lookup"><span data-stu-id="00ff4-157">When the `throw` statement is called from inside `ProcessString`, the system looks for the `catch` statement and displays the message `Exception caught`.</span></span>

[!code-csharp[csrefKeywordsExceptions#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsExceptions/CS/csrefKeywordsExceptions.cs#2)]

## <a name="two-catch-blocks-example"></a><span data-ttu-id="00ff4-158">Przykład dwóch bloków catch</span><span class="sxs-lookup"><span data-stu-id="00ff4-158">Two catch blocks example</span></span>

<span data-ttu-id="00ff4-159">W poniższym przykładzie są używane dwa bloki catch, a najbardziej konkretny wyjątek, który jest pierwszy, jest przechwytywany.</span><span class="sxs-lookup"><span data-stu-id="00ff4-159">In the following example, two catch blocks are used, and the most specific exception, which comes first, is caught.</span></span>

<span data-ttu-id="00ff4-160">Aby przechwycić najmniejszy konkretny wyjątek, można zastąpić instrukcję throw przy `ProcessString` użyciu następującej instrukcji: `throw new Exception()` .</span><span class="sxs-lookup"><span data-stu-id="00ff4-160">To catch the least specific exception, you can replace the throw statement in `ProcessString` with the following statement: `throw new Exception()`.</span></span>

<span data-ttu-id="00ff4-161">W przypadku umieszczenia bloku catch o najniższym poziomie najpierw w tym przykładzie zostanie wyświetlony następujący komunikat o błędzie: `A previous catch clause already catches all exceptions of this or a super type ('System.Exception')` .</span><span class="sxs-lookup"><span data-stu-id="00ff4-161">If you place the least-specific catch block first in the example, the following  error message appears: `A previous catch clause already catches all exceptions of this or a super type ('System.Exception')`.</span></span>

[!code-csharp[csrefKeywordsExceptions#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsExceptions/CS/csrefKeywordsExceptions.cs#3)]

## <a name="async-method-example"></a><span data-ttu-id="00ff4-162">Przykład metody asynchronicznej</span><span class="sxs-lookup"><span data-stu-id="00ff4-162">Async method example</span></span>

<span data-ttu-id="00ff4-163">Poniższy przykład ilustruje obsługę wyjątków dla metod asynchronicznych.</span><span class="sxs-lookup"><span data-stu-id="00ff4-163">The following example illustrates exception handling for async methods.</span></span> <span data-ttu-id="00ff4-164">Aby przechwytywać wyjątek, który generuje zadanie asynchroniczne, umieść `await` wyrażenie w `try` bloku i Przechwyć wyjątek w `catch` bloku.</span><span class="sxs-lookup"><span data-stu-id="00ff4-164">To catch an exception that an async task throws, place the `await` expression in a `try` block, and catch the exception in a `catch` block.</span></span>

<span data-ttu-id="00ff4-165">Usuń komentarz `throw new Exception` wiersza z przykładu, aby zademonstrować obsługę wyjątków.</span><span class="sxs-lookup"><span data-stu-id="00ff4-165">Uncomment the `throw new Exception` line in the example to demonstrate exception handling.</span></span> <span data-ttu-id="00ff4-166">`IsFaulted`Właściwość zadania jest ustawiona na `True` , `Exception.InnerException` Właściwość zadania jest ustawiana na wyjątek, a wyjątek jest przechwytywany w `catch` bloku.</span><span class="sxs-lookup"><span data-stu-id="00ff4-166">The task's `IsFaulted` property is set to `True`, the task's `Exception.InnerException` property is set to the exception, and the exception is caught in the `catch` block.</span></span>

<span data-ttu-id="00ff4-167">Usuń komentarz z `throw new OperationCanceledException` wiersza, aby zademonstrować, co się dzieje po anulowaniu procesu asynchronicznego.</span><span class="sxs-lookup"><span data-stu-id="00ff4-167">Uncomment the `throw new OperationCanceledException` line to demonstrate what happens when you cancel an asynchronous process.</span></span> <span data-ttu-id="00ff4-168">`IsCanceled`Właściwość zadania jest ustawiona na `true` , a wyjątek jest przechwytywany w `catch` bloku.</span><span class="sxs-lookup"><span data-stu-id="00ff4-168">The task's `IsCanceled` property is set to `true`, and the exception is caught in the `catch` block.</span></span> <span data-ttu-id="00ff4-169">W przypadku niektórych warunków, które nie dotyczą tego przykładu, `IsFaulted` Właściwość zadania jest ustawiona na `true` i `IsCanceled` jest ustawiona na `false` .</span><span class="sxs-lookup"><span data-stu-id="00ff4-169">Under some conditions that don't apply to this example, the task's `IsFaulted` property is set to `true` and `IsCanceled` is set to `false`.</span></span>

[!code-csharp[csAsyncExceptions#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csasyncexceptions/cs/class1.cs#2)]  

## <a name="taskwhenall-example"></a><span data-ttu-id="00ff4-170">Task. WhenAll — przykład</span><span class="sxs-lookup"><span data-stu-id="00ff4-170">Task.WhenAll example</span></span>

<span data-ttu-id="00ff4-171">Poniższy przykład ilustruje obsługę wyjątków, gdy wiele zadań może skutkować wieloma wyjątkami.</span><span class="sxs-lookup"><span data-stu-id="00ff4-171">The following example illustrates exception handling where multiple tasks can result in multiple exceptions.</span></span> <span data-ttu-id="00ff4-172">`try`Blok oczekuje zadania, które jest zwracane przez wywołanie metody <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType> .</span><span class="sxs-lookup"><span data-stu-id="00ff4-172">The `try` block awaits the task that's returned by a call to <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType>.</span></span> <span data-ttu-id="00ff4-173">Zadanie zostanie ukończone, gdy zostaną wykonane trzy zadania, do których zastosowano WhenAll.</span><span class="sxs-lookup"><span data-stu-id="00ff4-173">The task is complete when the three tasks to which WhenAll is applied are complete.</span></span>

<span data-ttu-id="00ff4-174">Każdy z tych trzech zadań powoduje wyjątek.</span><span class="sxs-lookup"><span data-stu-id="00ff4-174">Each of the three tasks causes an exception.</span></span> <span data-ttu-id="00ff4-175">`catch`Blok wykonuje iterację w wyjątkach, które są dostępne we `Exception.InnerExceptions` właściwości zadania, które zostało zwrócone przez <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType> .</span><span class="sxs-lookup"><span data-stu-id="00ff4-175">The `catch` block iterates through the exceptions, which are found in the `Exception.InnerExceptions` property of the task that was returned by <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType>.</span></span>

[!code-csharp[csAsyncExceptions#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csasyncexceptions/cs/class1.cs#4)]

## <a name="c-language-specification"></a><span data-ttu-id="00ff4-176">specyfikacja języka C#</span><span class="sxs-lookup"><span data-stu-id="00ff4-176">C# language specification</span></span>

<span data-ttu-id="00ff4-177">Aby uzyskać więcej informacji, zobacz sekcję [try instrukcji](~/_csharplang/spec/statements.md#the-try-statement) w [specyfikacji języka C#](~/_csharplang/spec/introduction.md).</span><span class="sxs-lookup"><span data-stu-id="00ff4-177">For more information, see [The try statement](~/_csharplang/spec/statements.md#the-try-statement) section of the [C# language specification](~/_csharplang/spec/introduction.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="00ff4-178">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="00ff4-178">See also</span></span>

- [<span data-ttu-id="00ff4-179">Odwołanie w C#</span><span class="sxs-lookup"><span data-stu-id="00ff4-179">C# Reference</span></span>](../index.md)
- [<span data-ttu-id="00ff4-180">Przewodnik programowania w języku C#</span><span class="sxs-lookup"><span data-stu-id="00ff4-180">C# Programming Guide</span></span>](../../programming-guide/index.md)
- [<span data-ttu-id="00ff4-181">Słowa kluczowe języka C#</span><span class="sxs-lookup"><span data-stu-id="00ff4-181">C# Keywords</span></span>](index.md)
- [<span data-ttu-id="00ff4-182">Instrukcje try, throw i catch (C++)</span><span class="sxs-lookup"><span data-stu-id="00ff4-182">try, throw, and catch Statements (C++)</span></span>](/cpp/cpp/try-throw-and-catch-statements-cpp)
- [<span data-ttu-id="00ff4-183">throw</span><span class="sxs-lookup"><span data-stu-id="00ff4-183">throw</span></span>](throw.md)
- [<span data-ttu-id="00ff4-184">try-finally</span><span class="sxs-lookup"><span data-stu-id="00ff4-184">try-finally</span></span>](try-finally.md)
- [<span data-ttu-id="00ff4-185">Instrukcje: Jawne zgłaszanie wyjątków</span><span class="sxs-lookup"><span data-stu-id="00ff4-185">How to: Explicitly Throw Exceptions</span></span>](../../../standard/exceptions/how-to-explicitly-throw-exceptions.md)
