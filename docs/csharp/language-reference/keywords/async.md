---
title: Dokumentacja Async-C#
ms.date: 05/22/2017
f1_keywords:
- async_CSharpKeyword
helpviewer_keywords:
- async keyword [C#]
- async method [C#]
- async [C#]
ms.assetid: 16f14f09-b2ce-42c7-a875-e4eca5d50674
ms.openlocfilehash: 279ea2f9875681401c9c7acab922d9e4424e6827
ms.sourcegitcommit: 7476c20d2f911a834a00b8a7f5e8926bae6804d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/11/2020
ms.locfileid: "88062538"
---
# <a name="async-c-reference"></a><span data-ttu-id="7b56f-102">async (odwołanie w C#)</span><span class="sxs-lookup"><span data-stu-id="7b56f-102">async (C# Reference)</span></span>

<span data-ttu-id="7b56f-103">Użyj `async` modyfikatora, aby określić, że metoda, [wyrażenie lambda](../operators/lambda-expressions.md)lub [Metoda anonimowa](../operators/delegate-operator.md) jest asynchroniczna.</span><span class="sxs-lookup"><span data-stu-id="7b56f-103">Use the `async` modifier to specify that a method, [lambda expression](../operators/lambda-expressions.md), or [anonymous method](../operators/delegate-operator.md) is asynchronous.</span></span> <span data-ttu-id="7b56f-104">Jeśli używasz tego modyfikatora w metodzie lub wyrażeniu, jest on nazywany *metodą Async*.</span><span class="sxs-lookup"><span data-stu-id="7b56f-104">If you use this modifier on a method or expression, it's referred to as an *async method*.</span></span> <span data-ttu-id="7b56f-105">W poniższym przykładzie zdefiniowano metodę asynchroniczną o nazwie `ExampleMethodAsync` :</span><span class="sxs-lookup"><span data-stu-id="7b56f-105">The following example defines an async method named `ExampleMethodAsync`:</span></span>
  
```csharp  
public async Task<int> ExampleMethodAsync()  
{  
    // . . . .  
}  
```  

<span data-ttu-id="7b56f-106">Jeśli dopiero zaczynasz programowanie asynchroniczne lub nie wiesz, w jaki sposób Metoda async używa [ `await` operatora](../operators/await.md) , aby potencjalnie długo pracować bez blokowania wątku wywołującego, zapoznaj się z tematem wprowadzenie do [programowania asynchronicznego przy użyciu Async i await](../../programming-guide/concepts/async/index.md).</span><span class="sxs-lookup"><span data-stu-id="7b56f-106">If you're new to asynchronous programming or do not understand how an async method uses the [`await` operator](../operators/await.md) to do potentially long-running work without blocking the caller's thread, read the introduction in [Asynchronous Programming with async and await](../../programming-guide/concepts/async/index.md).</span></span> <span data-ttu-id="7b56f-107">Poniższy kod znajduje się w metodzie asynchronicznej i wywołuje <xref:System.Net.Http.HttpClient.GetStringAsync%2a?displayProperty=nameWithType> metodę:</span><span class="sxs-lookup"><span data-stu-id="7b56f-107">The following code is found inside an async method and calls the <xref:System.Net.Http.HttpClient.GetStringAsync%2a?displayProperty=nameWithType> method:</span></span>
  
```csharp  
string contents = await httpClient.GetStringAsync(requestUrl);  
```  
  
<span data-ttu-id="7b56f-108">Metoda async jest uruchamiana synchronicznie do momentu, aż osiągnie swoje pierwsze `await` wyrażenie, w którym momencie Metoda jest wstrzymana do momentu ukończenia zadania.</span><span class="sxs-lookup"><span data-stu-id="7b56f-108">An async method runs synchronously until it reaches its first `await` expression, at which point the method is suspended until the awaited task is complete.</span></span> <span data-ttu-id="7b56f-109">W międzyczasie sterowanie jest przekazywane do obiektu wywołującego metody, tak jak pokazano w przykładzie w następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="7b56f-109">In the meantime, control returns to the caller of the method, as the example in the next section shows.</span></span>  
  
<span data-ttu-id="7b56f-110">Jeśli metoda `async` modyfikowana przez słowo kluczowe nie zawiera `await` wyrażenia lub instrukcji, metoda jest wykonywana synchronicznie.</span><span class="sxs-lookup"><span data-stu-id="7b56f-110">If the method that the `async` keyword modifies doesn't contain an `await` expression or statement, the method executes synchronously.</span></span> <span data-ttu-id="7b56f-111">Ostrzeżenie kompilatora ostrzega użytkownika o wszelkich metodach asynchronicznych, które nie zawierają `await` instrukcji, ponieważ taka sytuacja może wskazywać na błąd.</span><span class="sxs-lookup"><span data-stu-id="7b56f-111">A compiler warning alerts you to any async methods that don't contain `await` statements, because that situation might indicate an error.</span></span> <span data-ttu-id="7b56f-112">Zobacz [Ostrzeżenie kompilatora (poziom 1) CS4014](../compiler-messages/cs4014.md).</span><span class="sxs-lookup"><span data-stu-id="7b56f-112">See [Compiler Warning (level 1) CS4014](../compiler-messages/cs4014.md).</span></span>  
  
 <span data-ttu-id="7b56f-113">`async`Słowo kluczowe jest kontekstowe, ponieważ jest słowem kluczowym tylko wtedy, gdy modyfikuje metodę, wyrażenie lambda lub metodę anonimową.</span><span class="sxs-lookup"><span data-stu-id="7b56f-113">The `async` keyword is contextual in that it's a keyword only when it modifies a method, a lambda expression, or an anonymous method.</span></span> <span data-ttu-id="7b56f-114">W innych kontekstach jest interpretowane jako identyfikator.</span><span class="sxs-lookup"><span data-stu-id="7b56f-114">In all other contexts, it's interpreted as an identifier.</span></span>  
  
## <a name="example"></a><span data-ttu-id="7b56f-115">Przykład</span><span class="sxs-lookup"><span data-stu-id="7b56f-115">Example</span></span>  
<span data-ttu-id="7b56f-116">Poniższy przykład pokazuje strukturę i przepływ kontroli między obsługą zdarzeń asynchronicznych, `StartButton_Click` i metodę asynchroniczną `ExampleMethodAsync` .</span><span class="sxs-lookup"><span data-stu-id="7b56f-116">The following example shows the structure and flow of control between an async event handler, `StartButton_Click`, and an async method, `ExampleMethodAsync`.</span></span> <span data-ttu-id="7b56f-117">Wynikiem metody asynchronicznej jest liczba znaków strony sieci Web.</span><span class="sxs-lookup"><span data-stu-id="7b56f-117">The result from the async method is the number of characters of a web page.</span></span> <span data-ttu-id="7b56f-118">Kod jest odpowiedni dla aplikacji Windows Presentation Foundation (WPF) lub aplikacji ze sklepu Windows, którą tworzysz w programie Visual Studio; Zobacz komentarze do kodu dotyczące konfigurowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7b56f-118">The code is suitable for a Windows Presentation Foundation (WPF) app or Windows Store app that you create in Visual Studio; see the code comments for setting up the app.</span></span>  

<span data-ttu-id="7b56f-119">Ten kod można uruchomić w programie Visual Studio jako aplikacja Windows Presentation Foundation (WPF) lub aplikacja ze sklepu Windows.</span><span class="sxs-lookup"><span data-stu-id="7b56f-119">You can run this code in Visual Studio as a Windows Presentation Foundation (WPF) app or a Windows Store app.</span></span> <span data-ttu-id="7b56f-120">Potrzebujesz formantu Button o nazwie `StartButton` i kontrolki TextBox o nazwie `ResultsTextBox` .</span><span class="sxs-lookup"><span data-stu-id="7b56f-120">You need a Button control named `StartButton` and a Textbox control named `ResultsTextBox`.</span></span> <span data-ttu-id="7b56f-121">Pamiętaj, aby ustawić nazwy i obsługę, tak aby wyglądały następująco:</span><span class="sxs-lookup"><span data-stu-id="7b56f-121">Remember to set the names and handler so that you have something like this:</span></span>  

```xaml
<Button Content="Button" HorizontalAlignment="Left" Margin="88,77,0,0" VerticalAlignment="Top" Width="75"  
        Click="StartButton_Click" Name="StartButton"/>  
<TextBox HorizontalAlignment="Left" Height="137" Margin="88,140,0,0" TextWrapping="Wrap"
         Text="&lt;Enter a URL&gt;" VerticalAlignment="Top" Width="310" Name="ResultsTextBox"/>  
```
  
<span data-ttu-id="7b56f-122">Aby uruchomić kod jako aplikację WPF:</span><span class="sxs-lookup"><span data-stu-id="7b56f-122">To run the code as a WPF app:</span></span>  

- <span data-ttu-id="7b56f-123">Wklej ten kod do `MainWindow` klasy w MainWindow.XAML.cs.</span><span class="sxs-lookup"><span data-stu-id="7b56f-123">Paste this code into the `MainWindow` class in MainWindow.xaml.cs.</span></span>  
- <span data-ttu-id="7b56f-124">Dodaj odwołanie do systemu .NET. http.</span><span class="sxs-lookup"><span data-stu-id="7b56f-124">Add a reference to System.Net.Http.</span></span>  
- <span data-ttu-id="7b56f-125">Dodaj `using` dyrektywę dla systemu .NET. http.</span><span class="sxs-lookup"><span data-stu-id="7b56f-125">Add a `using` directive for System.Net.Http.</span></span>  
  
<span data-ttu-id="7b56f-126">Aby uruchomić kod jako aplikację ze sklepu Windows:</span><span class="sxs-lookup"><span data-stu-id="7b56f-126">To run the code as a Windows Store app:</span></span>  

- <span data-ttu-id="7b56f-127">Wklej ten kod do `MainPage` klasy w MainPage.XAML.cs.</span><span class="sxs-lookup"><span data-stu-id="7b56f-127">Paste this code into the `MainPage` class in MainPage.xaml.cs.</span></span>  
- <span data-ttu-id="7b56f-128">Dodaj dyrektywy using dla systemu .NET. http i system. Threading. Tasks.</span><span class="sxs-lookup"><span data-stu-id="7b56f-128">Add using directives for System.Net.Http and System.Threading.Tasks.</span></span>  
  
[!code-csharp[wpf-async](../../../../samples/snippets/csharp/language-reference/keywords/async/wpf/mainwindow.xaml.cs#1)]
  
> [!IMPORTANT]
> <span data-ttu-id="7b56f-129">Aby uzyskać więcej informacji o zadaniach i kodzie, który jest wykonywany podczas oczekiwania na zadanie, zobacz [programowanie asynchroniczne z Async i await](../../programming-guide/concepts/async/index.md).</span><span class="sxs-lookup"><span data-stu-id="7b56f-129">For more information about tasks and the code that executes while waiting for a task, see [Asynchronous Programming with async and await](../../programming-guide/concepts/async/index.md).</span></span> <span data-ttu-id="7b56f-130">Aby zapoznać się z pełnym przykładem WPF, który używa podobnych elementów, zobacz [Przewodnik: uzyskiwanie dostępu do sieci Web za pomocą Async i await](../../programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md).</span><span class="sxs-lookup"><span data-stu-id="7b56f-130">For a full WPF example that uses similar elements, see [Walkthrough: Accessing the Web by Using Async and Await](../../programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md).</span></span>  
  
## <a name="return-types"></a><span data-ttu-id="7b56f-131">Typy zwracane</span><span class="sxs-lookup"><span data-stu-id="7b56f-131">Return Types</span></span>  
<span data-ttu-id="7b56f-132">Metoda asynchroniczna może mieć następujące zwracane typy:</span><span class="sxs-lookup"><span data-stu-id="7b56f-132">An async method can have the following return types:</span></span>

- <xref:System.Threading.Tasks.Task>
- <xref:System.Threading.Tasks.Task%601>
- <span data-ttu-id="7b56f-133">[typ void](../builtin-types/void.md).</span><span class="sxs-lookup"><span data-stu-id="7b56f-133">[void](../builtin-types/void.md).</span></span> <span data-ttu-id="7b56f-134">`async void`metody są generalnie odradzane dla kodu innego niż programy obsługi zdarzeń, ponieważ obiekty wywołujące nie mogą `await` być tymi metodami i muszą implementować inny mechanizm, aby zgłosić pomyślne zakończenie lub błędy.</span><span class="sxs-lookup"><span data-stu-id="7b56f-134">`async void` methods are generally discouraged for code other than event handlers because callers cannot `await` those methods and must implement a different mechanism to report successful completion or error conditions.</span></span>
- <span data-ttu-id="7b56f-135">Począwszy od języka C# 7,0, dowolnego typu, który ma dostępną `GetAwaiter` metodę.</span><span class="sxs-lookup"><span data-stu-id="7b56f-135">Starting with C# 7.0, any type that has an accessible `GetAwaiter` method.</span></span> <span data-ttu-id="7b56f-136">`System.Threading.Tasks.ValueTask<TResult>`Typ to taka implementacja.</span><span class="sxs-lookup"><span data-stu-id="7b56f-136">The `System.Threading.Tasks.ValueTask<TResult>` type is one such implementation.</span></span> <span data-ttu-id="7b56f-137">Jest on dostępny przez dodanie pakietu NuGet `System.Threading.Tasks.Extensions` .</span><span class="sxs-lookup"><span data-stu-id="7b56f-137">It is available by adding the NuGet package `System.Threading.Tasks.Extensions`.</span></span>

<span data-ttu-id="7b56f-138">Metoda async nie może deklarować żadnych parametrów [in](./in-parameter-modifier.md), [ref](./ref.md) ani [out](./out-parameter-modifier.md) ani nie może mieć [wartości zwracanej przez odwołanie](../../programming-guide/classes-and-structs/ref-returns.md), ale może wywoływać metody, które mają takie parametry.</span><span class="sxs-lookup"><span data-stu-id="7b56f-138">The async method can't declare any [in](./in-parameter-modifier.md), [ref](./ref.md) or [out](./out-parameter-modifier.md) parameters, nor can it have a [reference return value](../../programming-guide/classes-and-structs/ref-returns.md), but it can call methods that have such parameters.</span></span>  
  
<span data-ttu-id="7b56f-139">Należy określić `Task<TResult>` jako zwracany typ metody asynchronicznej, jeśli instrukcja [Return](./return.md) metody określa argument operacji typu `TResult` .</span><span class="sxs-lookup"><span data-stu-id="7b56f-139">You specify `Task<TResult>` as the return type of an async method if the [return](./return.md) statement of the method specifies an operand of type `TResult`.</span></span> <span data-ttu-id="7b56f-140">Należy użyć, `Task` Jeśli podczas kończenia metody nie zostanie zwrócona wartość znacząca.</span><span class="sxs-lookup"><span data-stu-id="7b56f-140">You use `Task` if no meaningful value is returned when the method is completed.</span></span> <span data-ttu-id="7b56f-141">Oznacza to, że wywołanie metody zwraca `Task` , ale po `Task` zakończeniu, dowolne `await` wyrażenie, które oczekuje na `Task` wartości `void` .</span><span class="sxs-lookup"><span data-stu-id="7b56f-141">That is, a call to the method returns a `Task`, but when the `Task` is completed, any `await` expression that's awaiting the `Task` evaluates to `void`.</span></span>  
  
<span data-ttu-id="7b56f-142">`void`Typ zwracany jest używany głównie do definiowania programów obsługi zdarzeń, które wymagają tego typu zwracanego.</span><span class="sxs-lookup"><span data-stu-id="7b56f-142">You use the `void` return type primarily to define event handlers, which require that return type.</span></span> <span data-ttu-id="7b56f-143">Obiekt wywołujący `void` metodę asynchroniczną zwracającą wartość, której nie może oczekiwać i nie może przechwytywać wyjątków zgłaszanych przez metodę.</span><span class="sxs-lookup"><span data-stu-id="7b56f-143">The caller of a `void`-returning async method can't await it and can't catch exceptions that the method throws.</span></span>  

<span data-ttu-id="7b56f-144">Począwszy od języka C# 7,0, zwracany jest inny typ, zazwyczaj typ wartości, który ma `GetAwaiter` metodę, aby zminimalizować alokacje pamięci w sekcjach o kluczowym znaczeniu dla wydajności.</span><span class="sxs-lookup"><span data-stu-id="7b56f-144">Starting with C# 7.0, you return another type, typically a value type, that has a `GetAwaiter` method to minimize memory allocations in performance-critical sections of code.</span></span>

<span data-ttu-id="7b56f-145">Aby uzyskać więcej informacji i przykładów, zobacz [asynchroniczne typy zwracane](../../programming-guide/concepts/async/async-return-types.md).</span><span class="sxs-lookup"><span data-stu-id="7b56f-145">For more information and examples, see [Async Return Types](../../programming-guide/concepts/async/async-return-types.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="7b56f-146">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="7b56f-146">See also</span></span>

- <xref:System.Runtime.CompilerServices.AsyncStateMachineAttribute>
- [<span data-ttu-id="7b56f-147">await</span><span class="sxs-lookup"><span data-stu-id="7b56f-147">await</span></span>](../operators/await.md)
- [<span data-ttu-id="7b56f-148">Przewodnik: uzyskiwanie dostępu do sieci Web za pomocą Async i await</span><span class="sxs-lookup"><span data-stu-id="7b56f-148">Walkthrough: Accessing the Web by Using Async and Await</span></span>](../../programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)
- [<span data-ttu-id="7b56f-149">Programowanie asynchroniczne z Async i await</span><span class="sxs-lookup"><span data-stu-id="7b56f-149">Asynchronous Programming with async and await</span></span>](../../programming-guide/concepts/async/index.md)
