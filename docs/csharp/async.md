---
title: 'Programowanie asynchroniczne — C #'
description: Dowiedz się więcej o modelu programowania asynchronicznego na poziomie języka C# udostępnianym przez platformę .NET Core.
author: cartermp
ms.date: 05/20/2020
ms.technology: csharp-async
ms.assetid: b878c34c-a78f-419e-a594-a2b44fa521a4
ms.openlocfilehash: 58f650e7932d4f5862d545429376b3e417bb433c
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2020
ms.locfileid: "97512245"
---
# <a name="asynchronous-programming"></a><span data-ttu-id="263fb-103">Programowanie asynchroniczne</span><span class="sxs-lookup"><span data-stu-id="263fb-103">Asynchronous programming</span></span>

<span data-ttu-id="263fb-104">Jeśli istnieją jakieś wymagania dotyczące operacji we/wy (takie jak żądanie danych z sieci, uzyskiwanie dostępu do bazy danych lub odczytywanie i zapisywanie w systemie plików), należy wykorzystać programowanie asynchroniczne.</span><span class="sxs-lookup"><span data-stu-id="263fb-104">If you have any I/O-bound needs (such as requesting data from a network, accessing a database, or reading and writing to a file system), you'll want to utilize asynchronous programming.</span></span> <span data-ttu-id="263fb-105">Można również mieć kod powiązany z PROCESORem, taki jak wykonywanie kosztownych obliczeń, co jest również dobrym scenariuszem do pisania kodu asynchronicznego.</span><span class="sxs-lookup"><span data-stu-id="263fb-105">You could also have CPU-bound code, such as performing an expensive calculation, which is also a good scenario for writing async code.</span></span>

<span data-ttu-id="263fb-106">Język C# ma model programowania asynchronicznego na poziomie języka, który umożliwia łatwe pisanie kodu asynchronicznego bez konieczności Juggle wywołań zwrotnych lub zgodności z biblioteką obsługującą asynchroniczności.</span><span class="sxs-lookup"><span data-stu-id="263fb-106">C# has a language-level asynchronous programming model, which allows for easily writing asynchronous code without having to juggle callbacks or conform to a library that supports asynchrony.</span></span> <span data-ttu-id="263fb-107">Następuje to, co jest znane jako [wzorzec asynchroniczny oparty na zadaniach (TAP)](../standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap.md).</span><span class="sxs-lookup"><span data-stu-id="263fb-107">It follows what is known as the [Task-based Asynchronous Pattern (TAP)](../standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap.md).</span></span>

## <a name="overview-of-the-asynchronous-model"></a><span data-ttu-id="263fb-108">Przegląd modelu asynchronicznego</span><span class="sxs-lookup"><span data-stu-id="263fb-108">Overview of the asynchronous model</span></span>

<span data-ttu-id="263fb-109">Podstawowym programowaniem asynchronicznym są `Task` obiekty i `Task<T>` , które modelują operacje asynchroniczne.</span><span class="sxs-lookup"><span data-stu-id="263fb-109">The core of async programming is the `Task` and `Task<T>` objects, which model asynchronous operations.</span></span> <span data-ttu-id="263fb-110">Są one obsługiwane przez `async` `await` słowa kluczowe i.</span><span class="sxs-lookup"><span data-stu-id="263fb-110">They are supported by the `async` and `await` keywords.</span></span> <span data-ttu-id="263fb-111">Model jest dość prosty w większości przypadków:</span><span class="sxs-lookup"><span data-stu-id="263fb-111">The model is fairly simple in most cases:</span></span>

- <span data-ttu-id="263fb-112">W przypadku kodu powiązanego we/wy oczekujemy operacji, która zwraca `Task` lub `Task<T>` wewnątrz `async` metody.</span><span class="sxs-lookup"><span data-stu-id="263fb-112">For I/O-bound code, you await an operation that returns a `Task` or `Task<T>` inside of an `async` method.</span></span>
- <span data-ttu-id="263fb-113">W przypadku kodu powiązanego z PROCESORem czekasz na operację uruchomioną w wątku w tle za pomocą <xref:System.Threading.Tasks.Task.Run%2A?displayProperty=nameWithType> metody.</span><span class="sxs-lookup"><span data-stu-id="263fb-113">For CPU-bound code, you await an operation that is started on a background thread with the <xref:System.Threading.Tasks.Task.Run%2A?displayProperty=nameWithType> method.</span></span>

<span data-ttu-id="263fb-114">`await`Słowo kluczowe to miejsce, w którym występuje magiczna.</span><span class="sxs-lookup"><span data-stu-id="263fb-114">The `await` keyword is where the magic happens.</span></span> <span data-ttu-id="263fb-115">Zwraca kontrolę do obiektu wywołującego metody, która została wykonana `await` , i ostatecznie umożliwia interfejsowi użytkownika reagowanie lub na elastyczność usługi.</span><span class="sxs-lookup"><span data-stu-id="263fb-115">It yields control to the caller of the method that performed `await`, and it ultimately allows a UI to be responsive or a service to be elastic.</span></span> <span data-ttu-id="263fb-116">Chociaż istnieją [sposoby](../standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap.md) podejścia do kodu asynchronicznego innego niż `async` i `await` , ten artykuł koncentruje się na konstrukcjach poziomu języka.</span><span class="sxs-lookup"><span data-stu-id="263fb-116">While [there are ways](../standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap.md) to approach async code other than `async` and `await`, this article focuses on the language-level constructs.</span></span>

### <a name="io-bound-example-download-data-from-a-web-service"></a><span data-ttu-id="263fb-117">Przykład powiązania we/wy: pobieranie danych z usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="263fb-117">I/O-bound example: Download data from a web service</span></span>

<span data-ttu-id="263fb-118">Może być konieczne pobranie niektórych danych z usługi sieci Web po naciśnięciu przycisku, ale nie chcesz blokować wątku interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="263fb-118">You may need to download some data from a web service when a button is pressed but don't want to block the UI thread.</span></span> <span data-ttu-id="263fb-119">Można to zrobić w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="263fb-119">It can be accomplished like this:</span></span>

```csharp
private readonly HttpClient _httpClient = new HttpClient();

downloadButton.Clicked += async (o, e) =>
{
    // This line will yield control to the UI as the request
    // from the web service is happening.
    //
    // The UI thread is now free to perform other work.
    var stringData = await _httpClient.GetStringAsync(URL);
    DoSomethingWithData(stringData);
};
```

<span data-ttu-id="263fb-120">Kod wyraża zamiar (pobieranie danych asynchronicznie) bez ugrzęźnięcia w pracy z `Task` obiektami.</span><span class="sxs-lookup"><span data-stu-id="263fb-120">The code expresses the intent (downloading data asynchronously) without getting bogged down in interacting with `Task` objects.</span></span>

### <a name="cpu-bound-example-perform-a-calculation-for-a-game"></a><span data-ttu-id="263fb-121">Przykład związany z PROCESORem: wykonywanie obliczeń dla gry</span><span class="sxs-lookup"><span data-stu-id="263fb-121">CPU-bound example: Perform a calculation for a game</span></span>

<span data-ttu-id="263fb-122">Załóżmy, że nastąpi napisanie gry mobilnej, gdzie naciśnięcie przycisku może spowodować uszkodzenie wielu Enemies na ekranie.</span><span class="sxs-lookup"><span data-stu-id="263fb-122">Say you're writing a mobile game where pressing a button can inflict damage on many enemies on the screen.</span></span> <span data-ttu-id="263fb-123">Wykonywanie obliczeń uszkodzeń może być kosztowne, a wykonanie tej operacji w wątku interfejsu użytkownika spowoduje, że gra zostanie wstrzymana w miarę wykonywania obliczeń.</span><span class="sxs-lookup"><span data-stu-id="263fb-123">Performing the damage calculation can be expensive, and doing it on the UI thread would make the game appear to pause as the calculation is performed!</span></span>

<span data-ttu-id="263fb-124">Najlepszym sposobem obsługi tego jest uruchomienie wątku w tle, który wykonuje pracę przy użyciu programu `Task.Run` i czeka na jego wynik `await` .</span><span class="sxs-lookup"><span data-stu-id="263fb-124">The best way to handle this is to start a background thread, which does the work using `Task.Run`, and await its result using `await`.</span></span> <span data-ttu-id="263fb-125">Dzięki temu interfejs użytkownika może być niezakłócony podczas wykonywania pracy.</span><span class="sxs-lookup"><span data-stu-id="263fb-125">This allows the UI to feel smooth as the work is being done.</span></span>

```csharp
private DamageResult CalculateDamageDone()
{
    // Code omitted:
    //
    // Does an expensive calculation and returns
    // the result of that calculation.
}

calculateButton.Clicked += async (o, e) =>
{
    // This line will yield control to the UI while CalculateDamageDone()
    // performs its work. The UI thread is free to perform other work.
    var damageResult = await Task.Run(() => CalculateDamageDone());
    DisplayDamage(damageResult);
};
```

<span data-ttu-id="263fb-126">Ten kod jasno oznacza intencję zdarzenia kliknięcia przycisku, nie wymaga ręcznego zarządzania wątkiem w tle i robi to w sposób nieblokowany.</span><span class="sxs-lookup"><span data-stu-id="263fb-126">This code clearly expresses the intent of the button's click event, it doesn't require managing a background thread manually, and it does so in a non-blocking way.</span></span>

### <a name="what-happens-under-the-covers"></a><span data-ttu-id="263fb-127">Co się dzieje w obszarze okładek</span><span class="sxs-lookup"><span data-stu-id="263fb-127">What happens under the covers</span></span>

<span data-ttu-id="263fb-128">Istnieje wiele elementów, w których dane są wykonywane asynchronicznie.</span><span class="sxs-lookup"><span data-stu-id="263fb-128">There are many moving pieces where asynchronous operations are concerned.</span></span> <span data-ttu-id="263fb-129">`Task` `Task<T>` Aby uzyskać więcej informacji, zapoznaj się z informacjami o tym, co się dzieje [w](../standard/async-in-depth.md) artykule dotyczącym usługi i.</span><span class="sxs-lookup"><span data-stu-id="263fb-129">If you're curious about what's happening underneath the covers of `Task` and `Task<T>`, see the [Async in-depth](../standard/async-in-depth.md) article for more information.</span></span>

<span data-ttu-id="263fb-130">W języku C# po stronie elementów kompilator przekształca swój kod na maszynę stanu, która śledzi elementy, takie jak wykonywanie operacji, gdy `await` zostanie osiągnięty i wznowiono wykonywanie po zakończeniu zadania w tle.</span><span class="sxs-lookup"><span data-stu-id="263fb-130">On the C# side of things, the compiler transforms your code into a state machine that keeps track of things like yielding execution when an `await` is reached and resuming execution when a background job has finished.</span></span>

<span data-ttu-id="263fb-131">Dla teoretycznie nachylonego elementu jest to implementacja [modelu Promise asynchroniczności](https://en.wikipedia.org/wiki/Futures_and_promises).</span><span class="sxs-lookup"><span data-stu-id="263fb-131">For the theoretically-inclined, this is an implementation of the [Promise Model of asynchrony](https://en.wikipedia.org/wiki/Futures_and_promises).</span></span>

## <a name="key-pieces-to-understand"></a><span data-ttu-id="263fb-132">Najważniejsze elementy do zrozumienia</span><span class="sxs-lookup"><span data-stu-id="263fb-132">Key pieces to understand</span></span>

* <span data-ttu-id="263fb-133">Kod asynchroniczny może być używany zarówno dla kodu powiązanego we/wy, jak i związanego z PROCESORem, ale różnią się w zależności od każdego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="263fb-133">Async code can be used for both I/O-bound and CPU-bound code, but differently for each scenario.</span></span>
* <span data-ttu-id="263fb-134">Kod asynchroniczny używa `Task<T>` i `Task` , które są konstrukcjami używanymi do modelowania pracy wykonywanej w tle.</span><span class="sxs-lookup"><span data-stu-id="263fb-134">Async code uses `Task<T>` and `Task`, which are constructs used to model work being done in the background.</span></span>
* <span data-ttu-id="263fb-135">`async`Słowo kluczowe zamienia metodę na metodę asynchroniczną, która umożliwia użycie `await` słowa kluczowego w treści.</span><span class="sxs-lookup"><span data-stu-id="263fb-135">The `async` keyword turns a method into an async method, which allows you to use the `await` keyword in its body.</span></span>
* <span data-ttu-id="263fb-136">Gdy `await` słowo kluczowe jest stosowane, wstrzymuje metodę wywołującą i zwraca kontrolę do jej obiektu wywołującego do momentu ukończenia zadania.</span><span class="sxs-lookup"><span data-stu-id="263fb-136">When the `await` keyword is applied, it suspends the calling method and yields control back to its caller until the awaited task is complete.</span></span>
* <span data-ttu-id="263fb-137">`await` można go używać tylko wewnątrz metody asynchronicznej.</span><span class="sxs-lookup"><span data-stu-id="263fb-137">`await` can only be used inside an async method.</span></span>

## <a name="recognize-cpu-bound-and-io-bound-work"></a><span data-ttu-id="263fb-138">Rozpoznawanie pracy powiązanej z PROCESORem i operacji we/wy</span><span class="sxs-lookup"><span data-stu-id="263fb-138">Recognize CPU-bound and I/O-bound work</span></span>

<span data-ttu-id="263fb-139">Pierwsze dwa przykłady tego przewodnika pokazują, jak można korzystać z `async` i `await` dla pracy związanej z obsługą procesora i przez nią.</span><span class="sxs-lookup"><span data-stu-id="263fb-139">The first two examples of this guide showed how you could use `async` and `await` for I/O-bound and CPU-bound work.</span></span> <span data-ttu-id="263fb-140">Jest to klucz, który można określić, gdy zadanie, które należy wykonać, jest powiązane z elementem we/wy lub przez procesor, ponieważ może znacznie wpływać na wydajność kodu i potencjalnie spowodować błędne użycie niektórych konstrukcji.</span><span class="sxs-lookup"><span data-stu-id="263fb-140">It's key that you can identify when a job you need to do is I/O-bound or CPU-bound because it can greatly affect the performance of your code and could potentially lead to misusing certain constructs.</span></span>

<span data-ttu-id="263fb-141">Poniżej przedstawiono dwa pytania, które należy zadać przed pisaniem dowolnego kodu:</span><span class="sxs-lookup"><span data-stu-id="263fb-141">Here are two questions you should ask before you write any code:</span></span>

1. <span data-ttu-id="263fb-142">Czy kod będzie oczekiwał na coś, takiego jak dane z bazy danych?</span><span class="sxs-lookup"><span data-stu-id="263fb-142">Will your code be "waiting" for something, such as data from a database?</span></span>

   <span data-ttu-id="263fb-143">Jeśli odpowiedź brzmi "tak", Twoja służba jest **powiązana z elementem we/wy**.</span><span class="sxs-lookup"><span data-stu-id="263fb-143">If your answer is "yes", then your work is **I/O-bound**.</span></span>

1. <span data-ttu-id="263fb-144">Czy kod będzie wykonywał kosztowne Obliczanie?</span><span class="sxs-lookup"><span data-stu-id="263fb-144">Will your code be performing an expensive computation?</span></span>

   <span data-ttu-id="263fb-145">Jeśli otrzymasz odpowiedź "tak", Twoja służba jest **powiązana z procesorem**.</span><span class="sxs-lookup"><span data-stu-id="263fb-145">If you answered "yes", then your work is **CPU-bound**.</span></span>

<span data-ttu-id="263fb-146">Jeśli posiadana pracy jest **związana z we/wy**, użyj `async` i `await` *bez* `Task.Run` .</span><span class="sxs-lookup"><span data-stu-id="263fb-146">If the work you have is **I/O-bound**, use `async` and `await` *without* `Task.Run`.</span></span> <span data-ttu-id="263fb-147">*Nie należy* używać biblioteki zadań równoległych.</span><span class="sxs-lookup"><span data-stu-id="263fb-147">You *should not* use the Task Parallel Library.</span></span> <span data-ttu-id="263fb-148">Przyczyną tego problemu jest opis [asynchroniczny](../standard/async-in-depth.md).</span><span class="sxs-lookup"><span data-stu-id="263fb-148">The reason for this is outlined in [Async in Depth](../standard/async-in-depth.md).</span></span>

<span data-ttu-id="263fb-149">Jeśli praca, którą dysponujesz, jest **zależna od procesora** i masz informacje o czasie reakcji, użyj `async` i `await` , ale nie należy wykonać duplikowania pracy w innym wątku *za pomocą* `Task.Run` .</span><span class="sxs-lookup"><span data-stu-id="263fb-149">If the work you have is **CPU-bound** and you care about responsiveness, use `async` and `await`, but spawn off the work on another thread *with* `Task.Run`.</span></span> <span data-ttu-id="263fb-150">Jeśli prace są odpowiednie dla współbieżności i równoległości, należy również rozważyć użycie [biblioteki zadań równoległych](../standard/parallel-programming/task-parallel-library-tpl.md).</span><span class="sxs-lookup"><span data-stu-id="263fb-150">If the work is appropriate for concurrency and parallelism, also consider using the [Task Parallel Library](../standard/parallel-programming/task-parallel-library-tpl.md).</span></span>

<span data-ttu-id="263fb-151">Dodatkowo należy zawsze mierzyć wykonywanie kodu.</span><span class="sxs-lookup"><span data-stu-id="263fb-151">Additionally, you should always measure the execution of your code.</span></span> <span data-ttu-id="263fb-152">Można na przykład wyszukać siebie w sytuacji, w której ilość pracy związanej z PROCESORem jest zbyt mała w porównaniu z kosztami przełączeń kontekstu w przypadku wielowątkowości.</span><span class="sxs-lookup"><span data-stu-id="263fb-152">For example, you may find yourself in a situation where your CPU-bound work is not costly enough compared with the overhead of context switches when multithreading.</span></span> <span data-ttu-id="263fb-153">Każdy wybór ma swoje wady i należy wybrać odpowiednią kompromis dla danej sytuacji.</span><span class="sxs-lookup"><span data-stu-id="263fb-153">Every choice has its tradeoff, and you should pick the correct tradeoff for your situation.</span></span>

## <a name="more-examples"></a><span data-ttu-id="263fb-154">Więcej przykładów</span><span class="sxs-lookup"><span data-stu-id="263fb-154">More examples</span></span>

<span data-ttu-id="263fb-155">W poniższych przykładach pokazano różne sposoby pisania kodu asynchronicznego w języku C#.</span><span class="sxs-lookup"><span data-stu-id="263fb-155">The following examples demonstrate various ways you can write async code in C#.</span></span> <span data-ttu-id="263fb-156">Obejmują one kilka różnych scenariuszy, które mogą się pojawić.</span><span class="sxs-lookup"><span data-stu-id="263fb-156">They cover a few different scenarios you may come across.</span></span>

### <a name="extract-data-from-a-network"></a><span data-ttu-id="263fb-157">Wyodrębnij dane z sieci</span><span class="sxs-lookup"><span data-stu-id="263fb-157">Extract data from a network</span></span>

<span data-ttu-id="263fb-158">Ten fragment kodu pobiera kod HTML z strony głównej pod adresem <https://dotnetfoundation.org> i zlicza liczbę wystąpień ciągu ".NET" w kodzie HTML.</span><span class="sxs-lookup"><span data-stu-id="263fb-158">This snippet downloads the HTML from the homepage at <https://dotnetfoundation.org> and counts the number of times the string ".NET" occurs in the HTML.</span></span> <span data-ttu-id="263fb-159">Używa ASP.NET do definiowania metody kontrolera interfejsu API sieci Web, która wykonuje to zadanie i zwraca liczbę.</span><span class="sxs-lookup"><span data-stu-id="263fb-159">It uses ASP.NET to define a Web API controller method, which performs this task and returns the number.</span></span>

> [!NOTE]
> <span data-ttu-id="263fb-160">Jeśli planujesz wykonywanie analizy HTML w kodzie produkcyjnym, nie używaj wyrażeń regularnych.</span><span class="sxs-lookup"><span data-stu-id="263fb-160">If you plan on doing HTML parsing in production code, don't use regular expressions.</span></span> <span data-ttu-id="263fb-161">Zamiast tego użyj biblioteki analizy.</span><span class="sxs-lookup"><span data-stu-id="263fb-161">Use a parsing library instead.</span></span>

```csharp
private readonly HttpClient _httpClient = new HttpClient();

[HttpGet, Route("DotNetCount")]
public async Task<int> GetDotNetCount()
{
    // Suspends GetDotNetCount() to allow the caller (the web server)
    // to accept another request, rather than blocking on this one.
    var html = await _httpClient.GetStringAsync("https://dotnetfoundation.org");

    return Regex.Matches(html, @"\.NET").Count;
}
```

<span data-ttu-id="263fb-162">Jest to ten sam scenariusz Zapisano dla aplikacji uniwersalnej systemu Windows, która wykonuje to samo zadanie po naciśnięciu przycisku:</span><span class="sxs-lookup"><span data-stu-id="263fb-162">Here's the same scenario written for a Universal Windows App, which performs the same task when a Button is pressed:</span></span>

```csharp
private readonly HttpClient _httpClient = new HttpClient();

private async void OnSeeTheDotNetsButtonClick(object sender, RoutedEventArgs e)
{
    // Capture the task handle here so we can await the background task later.
    var getDotNetFoundationHtmlTask = _httpClient.GetStringAsync("https://dotnetfoundation.org");

    // Any other work on the UI thread can be done here, such as enabling a Progress Bar.
    // This is important to do here, before the "await" call, so that the user
    // sees the progress bar before execution of this method is yielded.
    NetworkProgressBar.IsEnabled = true;
    NetworkProgressBar.Visibility = Visibility.Visible;

    // The await operator suspends OnSeeTheDotNetsButtonClick(), returning control to its caller.
    // This is what allows the app to be responsive and not block the UI thread.
    var html = await getDotNetFoundationHtmlTask;
    int count = Regex.Matches(html, @"\.NET").Count;

    DotNetCountLabel.Text = $"Number of .NETs on dotnetfoundation.org: {count}";

    NetworkProgressBar.IsEnabled = false;
    NetworkProgressBar.Visibility = Visibility.Collapsed;
}
```

### <a name="wait-for-multiple-tasks-to-complete"></a><span data-ttu-id="263fb-163">Poczekaj na zakończenie wielu zadań</span><span class="sxs-lookup"><span data-stu-id="263fb-163">Wait for multiple tasks to complete</span></span>

<span data-ttu-id="263fb-164">Możesz się zastanowić w sytuacji, w której konieczne jest pobranie wielu danych jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="263fb-164">You may find yourself in a situation where you need to retrieve multiple pieces of data concurrently.</span></span> <span data-ttu-id="263fb-165">`Task`Interfejs API zawiera dwie metody <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType> i <xref:System.Threading.Tasks.Task.WhenAny%2A?displayProperty=nameWithType> , które umożliwiają pisanie kodu asynchronicznego, który wykonuje operację nieblokującą w przypadku wielu zadań w tle.</span><span class="sxs-lookup"><span data-stu-id="263fb-165">The `Task` API contains two methods, <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType> and <xref:System.Threading.Tasks.Task.WhenAny%2A?displayProperty=nameWithType>, that allow you to write asynchronous code that performs a non-blocking wait on multiple background jobs.</span></span>

<span data-ttu-id="263fb-166">Ten przykład pokazuje, jak można pobrać `User` dane dla zestawu `userId` s.</span><span class="sxs-lookup"><span data-stu-id="263fb-166">This example shows how you might grab `User` data for a set of `userId`s.</span></span>

```csharp
public async Task<User> GetUserAsync(int userId)
{
    // Code omitted:
    //
    // Given a user Id {userId}, retrieves a User object corresponding
    // to the entry in the database with {userId} as its Id.
}

public static async Task<IEnumerable<User>> GetUsersAsync(IEnumerable<int> userIds)
{
    var getUserTasks = new List<Task<User>>();
    foreach (int userId in userIds)
    {
        getUserTasks.Add(GetUserAsync(userId));
    }

    return await Task.WhenAll(getUserTasks);
}
```

<span data-ttu-id="263fb-167">Oto inny sposób, aby napisać ten bardziej zwięzłie przy użyciu LINQ:</span><span class="sxs-lookup"><span data-stu-id="263fb-167">Here's another way to write this more succinctly, using LINQ:</span></span>

```csharp
public async Task<User> GetUserAsync(int userId)
{
    // Code omitted:
    //
    // Given a user Id {userId}, retrieves a User object corresponding
    // to the entry in the database with {userId} as its Id.
}

public static async Task<User[]> GetUsersAsync(IEnumerable<int> userIds)
{
    var getUserTasks = userIds.Select(id => GetUserAsync(id));
    return await Task.WhenAll(getUserTasks);
}
```

<span data-ttu-id="263fb-168">Chociaż nie jest to mniejsze, należy zachować ostrożność podczas mieszania LINQ z kodem asynchronicznym.</span><span class="sxs-lookup"><span data-stu-id="263fb-168">Although it's less code, use caution when mixing LINQ with asynchronous code.</span></span> <span data-ttu-id="263fb-169">Ponieważ LINQ korzysta z odroczonego (opóźnionego) wykonywania, wywołania asynchroniczne nie będą wykonywane natychmiast, dopóki nie `foreach` wymusisz wygenerowania sekwencji iteracji z wywołaniem `.ToList()` lub `.ToArray()` .</span><span class="sxs-lookup"><span data-stu-id="263fb-169">Because LINQ uses deferred (lazy) execution, async calls won't happen immediately as they do in a `foreach` loop unless you force the generated sequence to iterate with a call to `.ToList()` or `.ToArray()`.</span></span>

## <a name="important-info-and-advice"></a><span data-ttu-id="263fb-170">Ważne informacje i porady</span><span class="sxs-lookup"><span data-stu-id="263fb-170">Important info and advice</span></span>

<span data-ttu-id="263fb-171">W przypadku programowania asynchronicznego istnieje kilka szczegółów, które należy wziąć pod uwagę, co może uniemożliwić nieoczekiwane zachowanie.</span><span class="sxs-lookup"><span data-stu-id="263fb-171">With async programming, there are some details to keep in mind which can prevent unexpected behavior.</span></span>

* <span data-ttu-id="263fb-172">`async`**metody muszą mieć** `await` **słowo kluczowe w swojej treści lub nigdy nie da!**</span><span class="sxs-lookup"><span data-stu-id="263fb-172">`async` **methods need to have an** `await` **keyword in their body or they will never yield!**</span></span>

  <span data-ttu-id="263fb-173">Jest to ważne, aby mieć świadomość.</span><span class="sxs-lookup"><span data-stu-id="263fb-173">This is important to keep in mind.</span></span> <span data-ttu-id="263fb-174">Jeśli `await` nie jest używany w treści `async` metody, kompilator języka C# generuje ostrzeżenie, ale kod kompiluje i działa tak, jakby była normalną metodą.</span><span class="sxs-lookup"><span data-stu-id="263fb-174">If `await` is not used in the body of an `async` method, the C# compiler generates a warning, but the code compiles and runs as if it were a normal method.</span></span> <span data-ttu-id="263fb-175">Jest to niezwykle niewydajne, ponieważ komputer stanu wygenerowany przez kompilator C# dla metody asynchronicznej nie wykonuje żadnych operacji.</span><span class="sxs-lookup"><span data-stu-id="263fb-175">This is incredibly inefficient, as the state machine generated by the C# compiler for the async method is not accomplishing anything.</span></span>

* <span data-ttu-id="263fb-176">**Należy dodać "Async" jako sufiks każdej zapisywanych nazw metod asynchronicznych.**</span><span class="sxs-lookup"><span data-stu-id="263fb-176">**You should add "Async" as the suffix of every async method name you write.**</span></span>

<span data-ttu-id="263fb-177">Jest to Konwencja używana w programie .NET do łatwiejszego odróżnienia metod synchronicznych i asynchronicznych.</span><span class="sxs-lookup"><span data-stu-id="263fb-177">This is the convention used in .NET to more easily differentiate synchronous and asynchronous methods.</span></span> <span data-ttu-id="263fb-178">Niektóre metody, które nie są jawnie wywoływane przez kod (takie jak procedury obsługi zdarzeń lub metody kontrolera sieci Web), nie muszą być stosowane.</span><span class="sxs-lookup"><span data-stu-id="263fb-178">Certain methods that aren't explicitly called by your code (such as event handlers or web controller methods) don't necessarily apply.</span></span> <span data-ttu-id="263fb-179">Ponieważ nie są one jawnie wywoływane przez kod, jawny opis ich nazewnictwa nie jest ważny.</span><span class="sxs-lookup"><span data-stu-id="263fb-179">Because they are not explicitly called by your code, being explicit about their naming isn't as important.</span></span>

* <span data-ttu-id="263fb-180">`async void`**powinien być używany tylko dla programów obsługi zdarzeń.**</span><span class="sxs-lookup"><span data-stu-id="263fb-180">`async void` **should only be used for event handlers.**</span></span>

<span data-ttu-id="263fb-181">`async void` jest jedynym sposobem zezwalania na działanie programów obsługi zdarzeń asynchronicznych, ponieważ zdarzenia nie mają zwracanych typów (w związku z czym nie mogą korzystać z `Task` i `Task<T>` ).</span><span class="sxs-lookup"><span data-stu-id="263fb-181">`async void` is the only way to allow asynchronous event handlers to work because events do not have return types (thus cannot make use of `Task` and `Task<T>`).</span></span> <span data-ttu-id="263fb-182">Inne użycie nie jest `async void` zgodne z modelem TAP i może być trudne do użycia, takie jak:</span><span class="sxs-lookup"><span data-stu-id="263fb-182">Any other use of `async void` does not follow the TAP model and can be challenging to use, such as:</span></span>

* <span data-ttu-id="263fb-183">Wyjątki zgłoszone w `async void` metodzie nie mogą być przechwytywane poza tą metodą.</span><span class="sxs-lookup"><span data-stu-id="263fb-183">Exceptions thrown in an `async void` method can't be caught outside of that method.</span></span>
* <span data-ttu-id="263fb-184">`async void` metody są trudne do przetestowania.</span><span class="sxs-lookup"><span data-stu-id="263fb-184">`async void` methods are difficult to test.</span></span>
* <span data-ttu-id="263fb-185">`async void` metody mogą spowodować złe skutki uboczne, jeśli obiekt wywołujący nie oczekuje, że będzie on asynchroniczny.</span><span class="sxs-lookup"><span data-stu-id="263fb-185">`async void` methods can cause bad side effects if the caller isn't expecting them to be async.</span></span>

* <span data-ttu-id="263fb-186">**Dokładne użycie asynchronicznych wyrażeń lambda w wyrażeniach LINQ**</span><span class="sxs-lookup"><span data-stu-id="263fb-186">**Tread carefully when using async lambdas in LINQ expressions**</span></span>

<span data-ttu-id="263fb-187">Wyrażenia lambda w składniku LINQ wykorzystują odroczone wykonywanie, co oznacza, że kod może zakończyć wykonywanie w czasie, gdy nie jest oczekiwany.</span><span class="sxs-lookup"><span data-stu-id="263fb-187">Lambda expressions in LINQ use deferred execution, meaning code could end up executing at a time when you're not expecting it to.</span></span> <span data-ttu-id="263fb-188">Wprowadzenie zadań blokowania w tym celu może w prosty sposób spowodować zakleszczenie, jeśli nie zapisano prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="263fb-188">The introduction of blocking tasks into this can easily result in a deadlock if not written correctly.</span></span> <span data-ttu-id="263fb-189">Ponadto zagnieżdżanie kodu asynchronicznego, takiego jak ten, może być również trudniejsze do powodowania wykonywania kodu.</span><span class="sxs-lookup"><span data-stu-id="263fb-189">Additionally, the nesting of asynchronous code like this can also make it more difficult to reason about the execution of the code.</span></span> <span data-ttu-id="263fb-190">Asynchroniczne i LINQ są zaawansowane, ale powinny być używane razem, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="263fb-190">Async and LINQ are powerful but should be used together as carefully and clearly as possible.</span></span>

* <span data-ttu-id="263fb-191">**Napisz kod, który czeka na zadania w sposób nieblokowany**</span><span class="sxs-lookup"><span data-stu-id="263fb-191">**Write code that awaits Tasks in a non-blocking manner**</span></span>

<span data-ttu-id="263fb-192">Zablokowanie bieżącego wątku jako środka do oczekiwania na `Task` zakończenie może spowodować zakleszczenie i zablokowane wątki kontekstu i może wymagać bardziej złożonej obsługi błędów.</span><span class="sxs-lookup"><span data-stu-id="263fb-192">Blocking the current thread as a means to wait for a `Task` to complete can result in deadlocks and blocked context threads and can require more complex error-handling.</span></span> <span data-ttu-id="263fb-193">Poniższa tabela zawiera wskazówki dotyczące sposobu postępowania z oczekiwaniami w przypadku zadań w sposób nieblokowany:</span><span class="sxs-lookup"><span data-stu-id="263fb-193">The following table provides guidance on how to deal with waiting for tasks in a non-blocking way:</span></span>

| <span data-ttu-id="263fb-194">Użyj polecenia...</span><span class="sxs-lookup"><span data-stu-id="263fb-194">Use this...</span></span>          | <span data-ttu-id="263fb-195">Zamiast tego...</span><span class="sxs-lookup"><span data-stu-id="263fb-195">Instead of this...</span></span>           | <span data-ttu-id="263fb-196">Jeśli chcesz to zrobić...</span><span class="sxs-lookup"><span data-stu-id="263fb-196">When wishing to do this...</span></span>                 |
|----------------------|------------------------------|--------------------------------------------|
| `await`              | <span data-ttu-id="263fb-197">`Task.Wait` lub `Task.Result`</span><span class="sxs-lookup"><span data-stu-id="263fb-197">`Task.Wait` or `Task.Result`</span></span> | <span data-ttu-id="263fb-198">Pobieranie wyniku zadania w tle</span><span class="sxs-lookup"><span data-stu-id="263fb-198">Retrieving the result of a background task</span></span> |
| `await Task.WhenAny` | `Task.WaitAny`               | <span data-ttu-id="263fb-199">Oczekiwanie na zakończenie dowolnego zadania</span><span class="sxs-lookup"><span data-stu-id="263fb-199">Waiting for any task to complete</span></span>           |
| `await Task.WhenAll` | `Task.WaitAll`               | <span data-ttu-id="263fb-200">Oczekiwanie na zakończenie wszystkich zadań</span><span class="sxs-lookup"><span data-stu-id="263fb-200">Waiting for all tasks to complete</span></span>          |
| `await Task.Delay`   | `Thread.Sleep`               | <span data-ttu-id="263fb-201">Oczekiwanie przez pewien czas</span><span class="sxs-lookup"><span data-stu-id="263fb-201">Waiting for a period of time</span></span>               |

* <span data-ttu-id="263fb-202">**Rozważ użycie** `ValueTask` **tam, gdzie to możliwe**</span><span class="sxs-lookup"><span data-stu-id="263fb-202">**Consider using** `ValueTask` **where possible**</span></span>

<span data-ttu-id="263fb-203">Zwrócenie `Task` obiektu z metod asynchronicznych może spowodować wąskie gardła wydajności w określonych ścieżkach.</span><span class="sxs-lookup"><span data-stu-id="263fb-203">Returning a `Task` object from async methods can introduce performance bottlenecks in certain paths.</span></span> <span data-ttu-id="263fb-204">`Task` to typ referencyjny, dlatego użycie go oznacza przydzielenie obiektu.</span><span class="sxs-lookup"><span data-stu-id="263fb-204">`Task` is a reference type, so using it means allocating an object.</span></span> <span data-ttu-id="263fb-205">W przypadkach, gdy metoda zadeklarowana za pomocą `async` modyfikatora zwraca zbuforowany wynik lub wykonuje synchronicznie, dodatkowe alokacje mogą stać się znaczącym kosztem w przypadku krytycznych sekcji kodu.</span><span class="sxs-lookup"><span data-stu-id="263fb-205">In cases where a method declared with the `async` modifier returns a cached result or completes synchronously, the extra allocations can become a significant time cost in performance critical sections of code.</span></span> <span data-ttu-id="263fb-206">Może być kosztowna, jeśli te przydziały występują w ścisłych pętlach.</span><span class="sxs-lookup"><span data-stu-id="263fb-206">It can become costly if those allocations occur in tight loops.</span></span> <span data-ttu-id="263fb-207">Aby uzyskać więcej informacji, zobacz [uogólnione asynchroniczne typy zwracane](whats-new/csharp-7.md#generalized-async-return-types).</span><span class="sxs-lookup"><span data-stu-id="263fb-207">For more information, see [generalized async return types](whats-new/csharp-7.md#generalized-async-return-types).</span></span>

* <span data-ttu-id="263fb-208">**Rozważ użycie**`ConfigureAwait(false)`</span><span class="sxs-lookup"><span data-stu-id="263fb-208">**Consider using** `ConfigureAwait(false)`</span></span>

<span data-ttu-id="263fb-209">Typowym pytaniem jest "Kiedy należy używać <xref:System.Threading.Tasks.Task.ConfigureAwait(System.Boolean)?displayProperty=nameWithType> metody?".</span><span class="sxs-lookup"><span data-stu-id="263fb-209">A common question is, "when should I use the <xref:System.Threading.Tasks.Task.ConfigureAwait(System.Boolean)?displayProperty=nameWithType> method?".</span></span> <span data-ttu-id="263fb-210">Metoda pozwala na `Task` wystąpienie w celu skonfigurowania jego oczekiwania.</span><span class="sxs-lookup"><span data-stu-id="263fb-210">The method allows for a `Task` instance to configure its awaiter.</span></span> <span data-ttu-id="263fb-211">Jest to ważne zagadnienie, ale nieprawidłowe ustawienie może potencjalnie mieć wpływ na wydajność i nawet zakleszczenia.</span><span class="sxs-lookup"><span data-stu-id="263fb-211">This is an important consideration and setting it incorrectly could potentially have performance implications and even deadlocks.</span></span> <span data-ttu-id="263fb-212">Aby uzyskać więcej informacji na temat `ConfigureAwait` , zobacz [często zadawane pytania](https://devblogs.microsoft.com/dotnet/configureawait-faq)dotyczące usługi ConfigureAwait.</span><span class="sxs-lookup"><span data-stu-id="263fb-212">For more information on `ConfigureAwait`, see the [ConfigureAwait FAQ](https://devblogs.microsoft.com/dotnet/configureawait-faq).</span></span>

* <span data-ttu-id="263fb-213">**Zapisz mniej stanowy kod**</span><span class="sxs-lookup"><span data-stu-id="263fb-213">**Write less stateful code**</span></span>

<span data-ttu-id="263fb-214">Nie zależą od stanu obiektów globalnych lub wykonywania niektórych metod.</span><span class="sxs-lookup"><span data-stu-id="263fb-214">Don't depend on the state of global objects or the execution of certain methods.</span></span> <span data-ttu-id="263fb-215">Zamiast tego zależą tylko od wartości zwracanych z metod.</span><span class="sxs-lookup"><span data-stu-id="263fb-215">Instead, depend only on the return values of methods.</span></span> <span data-ttu-id="263fb-216">Dlaczego?</span><span class="sxs-lookup"><span data-stu-id="263fb-216">Why?</span></span>

* <span data-ttu-id="263fb-217">Kod będzie łatwiejszy z przyczyn.</span><span class="sxs-lookup"><span data-stu-id="263fb-217">Code will be easier to reason about.</span></span>
* <span data-ttu-id="263fb-218">Kod będzie łatwiejszy do przetestowania.</span><span class="sxs-lookup"><span data-stu-id="263fb-218">Code will be easier to test.</span></span>
* <span data-ttu-id="263fb-219">Mieszanie kodu asynchronicznego i synchronicznego jest bardzo prostsze.</span><span class="sxs-lookup"><span data-stu-id="263fb-219">Mixing async and synchronous code is far simpler.</span></span>
* <span data-ttu-id="263fb-220">Warunki wyścigu można zwykle uniknąć w ogóle.</span><span class="sxs-lookup"><span data-stu-id="263fb-220">Race conditions can typically be avoided altogether.</span></span>
* <span data-ttu-id="263fb-221">W zależności od zwracanych wartości upraszczamy prosty kod asynchroniczny.</span><span class="sxs-lookup"><span data-stu-id="263fb-221">Depending on return values makes coordinating async code simple.</span></span>
* <span data-ttu-id="263fb-222">(Premia) dobrze sprawdza się w przypadku iniekcji zależności.</span><span class="sxs-lookup"><span data-stu-id="263fb-222">(Bonus) it works really well with dependency injection.</span></span>

<span data-ttu-id="263fb-223">Zalecanym celem jest osiągnięcie pełnej lub niemal kompletnej [przejrzystości referencyjnej](https://en.wikipedia.org/wiki/Referential_transparency_%28computer_science%29) w kodzie.</span><span class="sxs-lookup"><span data-stu-id="263fb-223">A recommended goal is to achieve complete or near-complete [Referential Transparency](https://en.wikipedia.org/wiki/Referential_transparency_%28computer_science%29) in your code.</span></span> <span data-ttu-id="263fb-224">Wykonanie tej czynności spowoduje powstanie niezwykle przewidywalnej, weryfikowalneej i obsługiwanej bazy kodu.</span><span class="sxs-lookup"><span data-stu-id="263fb-224">Doing so will result in an extremely predictable, testable, and maintainable codebase.</span></span>

## <a name="other-resources"></a><span data-ttu-id="263fb-225">Inne zasoby</span><span class="sxs-lookup"><span data-stu-id="263fb-225">Other resources</span></span>

* <span data-ttu-id="263fb-226">[Asynchroniczne](../standard/async-in-depth.md) Szczegóły zawiera więcej informacji na temat działania zadań.</span><span class="sxs-lookup"><span data-stu-id="263fb-226">[Async in-depth](../standard/async-in-depth.md) provides more information about how Tasks work.</span></span>
* [<span data-ttu-id="263fb-227">Programowanie asynchroniczne z Async i Await (C#)</span><span class="sxs-lookup"><span data-stu-id="263fb-227">Asynchronous programming with async and await (C#)</span></span>](./programming-guide/concepts/async/index.md)
* <span data-ttu-id="263fb-228">Lucian Wischike [sześć najważniejszych porad dotyczących Async](https://channel9.msdn.com/Series/Three-Essential-Tips-for-Async) to wspaniałe zasoby dla programowania asynchronicznego</span><span class="sxs-lookup"><span data-stu-id="263fb-228">Lucian Wischik's [Six Essential Tips for Async](https://channel9.msdn.com/Series/Three-Essential-Tips-for-Async) are a wonderful resource for async programming</span></span>
