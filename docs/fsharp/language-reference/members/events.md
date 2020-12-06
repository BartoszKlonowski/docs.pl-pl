---
title: Zdarzenia
description: 'Dowiedz się, jak zdarzenia języka F # umożliwiają kojarzenie wywołań funkcji z akcjami użytkownika, które są ważne w programowaniu graficznego interfejsu użytkownika.'
ms.date: 08/15/2020
ms.openlocfilehash: 17e0cc8840053bf24d5c69694fe94d544c44510d
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96740344"
---
# <a name="events"></a><span data-ttu-id="80e25-103">Zdarzenia</span><span class="sxs-lookup"><span data-stu-id="80e25-103">Events</span></span>

<span data-ttu-id="80e25-104">Zdarzenia umożliwiają kojarzenie wywołań funkcji z akcjami użytkownika i są ważne w programowaniu graficznych interfejsów użytkownika.</span><span class="sxs-lookup"><span data-stu-id="80e25-104">Events enable you to associate function calls with user actions and are important in GUI programming.</span></span> <span data-ttu-id="80e25-105">Zdarzenia mogą być też wywoływane przez aplikacje lub system operacyjny.</span><span class="sxs-lookup"><span data-stu-id="80e25-105">Events can also be triggered by your applications or by the operating system.</span></span>

## <a name="handling-events"></a><span data-ttu-id="80e25-106">Obsługa zdarzeń</span><span class="sxs-lookup"><span data-stu-id="80e25-106">Handling Events</span></span>

<span data-ttu-id="80e25-107">Gdy jest używana biblioteka graficznych interfejsów użytkownika, taka jak Windows Forms lub Windows Presentation Foundation (WPF), większość kodu aplikacji działa w odpowiedzi na zdarzenia, które są wstępnie zdefiniowane w tej bibliotece.</span><span class="sxs-lookup"><span data-stu-id="80e25-107">When you use a GUI library like Windows Forms or Windows Presentation Foundation (WPF), much of the code in your application runs in response to events that are predefined by the library.</span></span> <span data-ttu-id="80e25-108">Te wstępnie zdefiniowane zdarzenia są składowymi klas graficznego interfejsu użytkownika, takich jak formularze i formanty.</span><span class="sxs-lookup"><span data-stu-id="80e25-108">These predefined events are members of GUI classes such as forms and controls.</span></span> <span data-ttu-id="80e25-109">Niestandardowe zachowanie można dodać do istniejącego zdarzenia, takiego jak kliknięcie przycisku, odwołując się do konkretnej nazwanego zdarzenia zainteresowania (na przykład `Click` zdarzenia `Form` klasy) i wywołując `Add` metodę, jak pokazano w poniższym kodzie.</span><span class="sxs-lookup"><span data-stu-id="80e25-109">You can add custom behavior to a preexisting event, such as a button click, by referencing the specific named event of interest (for example, the `Click` event of the `Form` class) and invoking the `Add` method, as shown in the following code.</span></span> <span data-ttu-id="80e25-110">Jeśli uruchomisz ten program z F# Interactive, Pomiń wywołanie metody `System.Windows.Forms.Application.Run(System.Windows.Forms.Form)` .</span><span class="sxs-lookup"><span data-stu-id="80e25-110">If you run this from F# Interactive, omit the call to `System.Windows.Forms.Application.Run(System.Windows.Forms.Form)`.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet3601.fs)]

<span data-ttu-id="80e25-111">Typ `Add` metody to `('a -> unit) -> unit` .</span><span class="sxs-lookup"><span data-stu-id="80e25-111">The type of the `Add` method is `('a -> unit) -> unit`.</span></span> <span data-ttu-id="80e25-112">W związku z tym metoda obsługi zdarzeń przyjmuje jeden parametr, zazwyczaj argumenty zdarzenia i zwraca `unit` .</span><span class="sxs-lookup"><span data-stu-id="80e25-112">Therefore, the event handler method takes one parameter, typically the event arguments, and returns `unit`.</span></span> <span data-ttu-id="80e25-113">W poprzednim przykładzie pokazano program obsługi zdarzeń w postaci wyrażenia lambda.</span><span class="sxs-lookup"><span data-stu-id="80e25-113">The previous example shows the event handler as a lambda expression.</span></span> <span data-ttu-id="80e25-114">Program obsługi zdarzeń może być także wartością funkcji, tak jak w poniższym przykładzie kodu.</span><span class="sxs-lookup"><span data-stu-id="80e25-114">The event handler can also be a function value, as in the following code example.</span></span> <span data-ttu-id="80e25-115">W poniższym przykładzie kodu pokazano także użycie parametrów programu obsługi zdarzeń, które dostarczają informacje charakterystyczne dla typu zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="80e25-115">The following code example also shows the use of the event handler parameters, which provide information specific to the type of event.</span></span> <span data-ttu-id="80e25-116">Dla `MouseMove` zdarzenia system przekazuje `System.Windows.Forms.MouseEventArgs` obiekt, który zawiera `X` `Y` położenie wskaźnika i.</span><span class="sxs-lookup"><span data-stu-id="80e25-116">For a `MouseMove` event, the system passes a `System.Windows.Forms.MouseEventArgs` object, which contains the `X` and `Y` position of the pointer.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet3602.fs)]

## <a name="creating-custom-events"></a><span data-ttu-id="80e25-117">Tworzenie zdarzeń niestandardowych</span><span class="sxs-lookup"><span data-stu-id="80e25-117">Creating Custom Events</span></span>

<span data-ttu-id="80e25-118">Zdarzenia języka f # są reprezentowane przez typ [zdarzenia](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-control-fsharpevent-1.html) języka f #, który implementuje interfejs [IEvent](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-control-ievent-1.html) .</span><span class="sxs-lookup"><span data-stu-id="80e25-118">F# events are represented by the F# [Event](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-control-fsharpevent-1.html) type, which implements the [IEvent](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-control-ievent-1.html) interface.</span></span> <span data-ttu-id="80e25-119">`IEvent` jest samym interfejsem, który łączy funkcje dwóch innych interfejsów `System.IObservable<'T>` i [IDelegateEvent](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-control-idelegateevent-1.html).</span><span class="sxs-lookup"><span data-stu-id="80e25-119">`IEvent` is itself an interface that combines the functionality of two other interfaces, `System.IObservable<'T>` and [IDelegateEvent](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-control-idelegateevent-1.html).</span></span> <span data-ttu-id="80e25-120">W związku z tym program `Event` s ma równoważne funkcje delegatów w innych językach oraz dodatkowe funkcje od `IObservable` , co oznacza, że zdarzenia języka f # obsługują filtrowanie zdarzeń oraz funkcje pierwszej klasy języka f # i wyrażenia lambda jako programy obsługi zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="80e25-120">Therefore, `Event`s have the equivalent functionality of delegates in other languages, plus the additional functionality from `IObservable`, which means that F# events support event filtering and using F# first-class functions and lambda expressions as event handlers.</span></span> <span data-ttu-id="80e25-121">Ta funkcja jest dostępna w [module Event](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-control-eventmodule.html).</span><span class="sxs-lookup"><span data-stu-id="80e25-121">This functionality is provided in the [Event module](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-control-eventmodule.html).</span></span>

<span data-ttu-id="80e25-122">Aby utworzyć zdarzenie na klasie, która działa podobnie jak wszystkie inne zdarzenia .NET Framework, Dodaj do klasy `let` powiązanie, które definiuje `Event` jako pole w klasie.</span><span class="sxs-lookup"><span data-stu-id="80e25-122">To create an event on a class that acts just like any other .NET Framework event, add to the class a `let` binding that defines an `Event` as a field in a class.</span></span> <span data-ttu-id="80e25-123">Odpowiedni typ argumentu zdarzenia można określić jako argument typu, ale można też pozostawić ten typu pusty, co spowoduje, że kompilator wywnioskuje odpowiedni typ.</span><span class="sxs-lookup"><span data-stu-id="80e25-123">You can specify the desired event argument type as the type argument, or leave it blank and have the compiler infer the appropriate type.</span></span> <span data-ttu-id="80e25-124">Należy także zdefiniować element członkowski zdarzenia, który będzie uwidaczniał zdarzenie jako zdarzenie CLI.</span><span class="sxs-lookup"><span data-stu-id="80e25-124">You also must define an event member that exposes the event as a CLI event.</span></span> <span data-ttu-id="80e25-125">Ten element członkowski powinien mieć atrybut [CLIEvent](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-clieventattribute.html) .</span><span class="sxs-lookup"><span data-stu-id="80e25-125">This member should have the [CLIEvent](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-clieventattribute.html) attribute.</span></span> <span data-ttu-id="80e25-126">Jest on zadeklarowany jako właściwość, a jego implementacja jest tylko wywołaniem właściwości [Publish](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-control-fsharpevent-1.html#Publish) zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="80e25-126">It is declared like a property and its implementation is just a call to the [Publish](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-control-fsharpevent-1.html#Publish) property of the event.</span></span> <span data-ttu-id="80e25-127">Użytkownicy klasy mogą korzystać z `Add` metody opublikowanego zdarzenia w celu dodania procedury obsługi.</span><span class="sxs-lookup"><span data-stu-id="80e25-127">Users of your class can use the `Add` method of the published event to add a handler.</span></span> <span data-ttu-id="80e25-128">Argument `Add` metody może być wyrażeniem lambda.</span><span class="sxs-lookup"><span data-stu-id="80e25-128">The argument for the `Add` method can be a lambda expression.</span></span> <span data-ttu-id="80e25-129">Możesz użyć `Trigger` właściwości zdarzenia, aby zgłosić zdarzenie, przekazując argumenty do funkcji obsługi.</span><span class="sxs-lookup"><span data-stu-id="80e25-129">You can use the `Trigger` property of the event to raise the event, passing the arguments to the handler function.</span></span> <span data-ttu-id="80e25-130">Pokazano to w poniższym przykładzie kodu.</span><span class="sxs-lookup"><span data-stu-id="80e25-130">The following code example illustrates this.</span></span> <span data-ttu-id="80e25-131">W tym przykładzie wywnioskowany argument typu dla zdarzenia to spójna kolekcja, która reprezentuje argumenty wyrażenia lambda.</span><span class="sxs-lookup"><span data-stu-id="80e25-131">In this example, the inferred type argument for the event is a tuple, which represents the arguments for the lambda expression.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet3605.fs)]

<span data-ttu-id="80e25-132">Dane wyjściowe są następujące:</span><span class="sxs-lookup"><span data-stu-id="80e25-132">The output is as follows.</span></span>

```console
Event1 occurred! Object data: Hello World!
```

<span data-ttu-id="80e25-133">Dodatkowe funkcje zapewniane przez moduł przedstawiono w `Event` tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="80e25-133">The additional functionality provided by the `Event` module is illustrated here.</span></span> <span data-ttu-id="80e25-134">Poniższy przykład kodu ilustruje podstawowe użycie programu `Event.create` , aby utworzyć zdarzenie i metodę wyzwalacza, dodać dwa programy obsługi zdarzeń w postaci wyrażeń lambda, a następnie wyzwoli zdarzenie, aby wykonać oba wyrażenia lambda.</span><span class="sxs-lookup"><span data-stu-id="80e25-134">The following code example illustrates the basic use of `Event.create` to create an event and a trigger method, add two event handlers in the form of lambda expressions, and then trigger the event to execute both lambda expressions.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet3603.fs)]

<span data-ttu-id="80e25-135">Dane wyjściowe poprzedniego kodu wyglądają następująco:</span><span class="sxs-lookup"><span data-stu-id="80e25-135">The output of the previous code is as follows.</span></span>

```console
Event occurred.
Given a value: Event occurred.
```

## <a name="processing-event-streams"></a><span data-ttu-id="80e25-136">Przetwarzanie strumieni zdarzeń</span><span class="sxs-lookup"><span data-stu-id="80e25-136">Processing Event Streams</span></span>

<span data-ttu-id="80e25-137">Zamiast tylko dodać procedurę obsługi zdarzeń dla zdarzenia przy użyciu funkcji [Event. Add](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-control-eventmodule.html#add) , można użyć funkcji w `Event` module do przetwarzania strumieni zdarzeń w sposób wysoce dostosowany.</span><span class="sxs-lookup"><span data-stu-id="80e25-137">Instead of just adding an event handler for an event by using the [Event.add](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-control-eventmodule.html#add) function, you can use the functions in the `Event` module to process streams of events in highly customized ways.</span></span> <span data-ttu-id="80e25-138">W tym celu należy użyć potoku do przodu ( `|>` ) wraz ze zdarzeniem jako pierwszą wartością w szeregu wywołań funkcji, a `Event` moduł działa jako kolejne wywołania funkcji.</span><span class="sxs-lookup"><span data-stu-id="80e25-138">To do this, you use the forward pipe (`|>`) together with the event as the first value in a series of function calls, and the `Event` module functions as subsequent function calls.</span></span>

<span data-ttu-id="80e25-139">W poniższym przykładzie kodu pokazano, jak skonfigurować zdarzenie, dla którego program obsługi jest wywoływany tylko w określonych warunkach.</span><span class="sxs-lookup"><span data-stu-id="80e25-139">The following code example shows how to set up an event for which the handler is only called under certain conditions.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet3604.fs)]

<span data-ttu-id="80e25-140">[Moduł zauważalny](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-control-observablemodule.html) zawiera podobne funkcje, które działają na obiektach zauważalnych.</span><span class="sxs-lookup"><span data-stu-id="80e25-140">The [Observable module](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-control-observablemodule.html) contains similar functions that operate on observable objects.</span></span> <span data-ttu-id="80e25-141">Widoczne obiekty są podobne do zdarzeń, ale aktywnie subskrybują zdarzenia tylko wtedy, gdy same są subskrybowane.</span><span class="sxs-lookup"><span data-stu-id="80e25-141">Observable objects are similar to events but only actively subscribe to events if they themselves are being subscribed to.</span></span>

## <a name="implementing-an-interface-event"></a><span data-ttu-id="80e25-142">Implementowanie zdarzenia interfejsu</span><span class="sxs-lookup"><span data-stu-id="80e25-142">Implementing an Interface Event</span></span>

<span data-ttu-id="80e25-143">Projektowanie składników interfejsu użytkownika często rozpoczyna się od utworzenia nowego formularza lub nowego formantu, który dziedziczy z istniejącego formularza lub formantu.</span><span class="sxs-lookup"><span data-stu-id="80e25-143">As you develop UI components, you often start by creating a new form or a new control that inherits from an existing form or control.</span></span> <span data-ttu-id="80e25-144">Zdarzenia są często definiowane w interfejsie, a w takim przypadku trzeba zaimplementować interfejs służący do implementacji zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="80e25-144">Events are frequently defined on an interface, and, in that case, you must implement the interface to implement the event.</span></span> <span data-ttu-id="80e25-145">`System.ComponentModel.INotifyPropertyChanged`Interfejs definiuje pojedyncze `System.ComponentModel.INotifyPropertyChanged.PropertyChanged` zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="80e25-145">The `System.ComponentModel.INotifyPropertyChanged` interface defines a single `System.ComponentModel.INotifyPropertyChanged.PropertyChanged` event.</span></span> <span data-ttu-id="80e25-146">Poniższy kod ilustruje sposób implementacji zdarzenia definiowanego przez ten dziedziczony interfejs:</span><span class="sxs-lookup"><span data-stu-id="80e25-146">The following code illustrates how to implement the event that this inherited interface defined:</span></span>

```fsharp
module CustomForm

open System.Windows.Forms
open System.ComponentModel

type AppForm() as this =
    inherit Form()

    // Define the propertyChanged event.
    let propertyChanged = Event<PropertyChangedEventHandler, PropertyChangedEventArgs>()
    let mutable underlyingValue = "text0"

    // Set up a click event to change the properties.
    do
        this.Click |> Event.add(fun evArgs ->
            this.Property1 <- "text2"
            this.Property2 <- "text3")

    // This property does not have the property-changed event set.
    member val Property1 : string = "text" with get, set

    // This property has the property-changed event set.
    member this.Property2
        with get() = underlyingValue
        and set(newValue) =
            underlyingValue <- newValue
            propertyChanged.Trigger(this, new PropertyChangedEventArgs("Property2"))

    // Expose the PropertyChanged event as a first class .NET event.
    [<CLIEvent>]
    member this.PropertyChanged = propertyChanged.Publish

    // Define the add and remove methods to implement this interface.
    interface INotifyPropertyChanged with
        member this.add_PropertyChanged(handler) = propertyChanged.Publish.AddHandler(handler)
        member this.remove_PropertyChanged(handler) = propertyChanged.Publish.RemoveHandler(handler)

    // This is the event-handler method.
    member this.OnPropertyChanged(args : PropertyChangedEventArgs) =
        let newProperty = this.GetType().GetProperty(args.PropertyName)
        let newValue = newProperty.GetValue(this :> obj) :?> string
        printfn "Property {args.PropertyName} changed its value to {newValue}"

// Create a form, hook up the event handler, and start the application.
let appForm = new AppForm()
let inpc = appForm :> INotifyPropertyChanged
inpc.PropertyChanged.Add(appForm.OnPropertyChanged)
Application.Run(appForm)
```

<span data-ttu-id="80e25-147">Jeśli chcesz podłączyć zdarzenie w konstruktorze, kod jest nieco bardziej skomplikowany, ponieważ usługa Event podłączenie musi znajdować się w `then` bloku w dodatkowym konstruktorze, jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="80e25-147">If you want to hook up the event in the constructor, the code is a bit more complicated because the event hookup must be in a `then` block in an additional constructor, as in the following example:</span></span>

```fsharp
module CustomForm

open System.Windows.Forms
open System.ComponentModel

// Create a private constructor with a dummy argument so that the public
// constructor can have no arguments.
type AppForm private (dummy) as this =
    inherit Form()

    // Define the propertyChanged event.
    let propertyChanged = Event<PropertyChangedEventHandler, PropertyChangedEventArgs>()
    let mutable underlyingValue = "text0"

    // Set up a click event to change the properties.
    do
        this.Click |> Event.add(fun evArgs ->
            this.Property1 <- "text2"
            this.Property2 <- "text3")

    // This property does not have the property changed event set.
    member val Property1 : string = "text" with get, set

    // This property has the property changed event set.
    member this.Property2
        with get() = underlyingValue
        and set(newValue) =
            underlyingValue <- newValue
            propertyChanged.Trigger(this, new PropertyChangedEventArgs("Property2"))

    [<CLIEvent>]
    member this.PropertyChanged = propertyChanged.Publish

    // Define the add and remove methods to implement this interface.
    interface INotifyPropertyChanged with
        member this.add_PropertyChanged(handler) = this.PropertyChanged.AddHandler(handler)
        member this.remove_PropertyChanged(handler) = this.PropertyChanged.RemoveHandler(handler)

    // This is the event handler method.
    member this.OnPropertyChanged(args : PropertyChangedEventArgs) =
        let newProperty = this.GetType().GetProperty(args.PropertyName)
        let newValue = newProperty.GetValue(this :> obj) :?> string
        printfn "Property {args.PropertyName} changed its value to {newValue}"

    new() as this =
        new AppForm(0)
        then
            let inpc = this :> INotifyPropertyChanged
            inpc.PropertyChanged.Add(this.OnPropertyChanged)

// Create a form, hook up the event handler, and start the application.
let appForm = new AppForm()
Application.Run(appForm)
```

## <a name="see-also"></a><span data-ttu-id="80e25-148">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="80e25-148">See also</span></span>

- [<span data-ttu-id="80e25-149">Elementy członkowskie</span><span class="sxs-lookup"><span data-stu-id="80e25-149">Members</span></span>](index.md)
- [<span data-ttu-id="80e25-150">Obsługa i wywoływanie zdarzeń</span><span class="sxs-lookup"><span data-stu-id="80e25-150">Handling and Raising Events</span></span>](../../../standard/events/index.md)
- [<span data-ttu-id="80e25-151">Wyrażenia lambda: `fun` słowo kluczowe</span><span class="sxs-lookup"><span data-stu-id="80e25-151">Lambda Expressions: The `fun` Keyword</span></span>](../functions/lambda-expressions-the-fun-keyword.md)
