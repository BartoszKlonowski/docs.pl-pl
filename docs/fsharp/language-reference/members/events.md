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
# <a name="events"></a>Zdarzenia

Zdarzenia umożliwiają kojarzenie wywołań funkcji z akcjami użytkownika i są ważne w programowaniu graficznych interfejsów użytkownika. Zdarzenia mogą być też wywoływane przez aplikacje lub system operacyjny.

## <a name="handling-events"></a>Obsługa zdarzeń

Gdy jest używana biblioteka graficznych interfejsów użytkownika, taka jak Windows Forms lub Windows Presentation Foundation (WPF), większość kodu aplikacji działa w odpowiedzi na zdarzenia, które są wstępnie zdefiniowane w tej bibliotece. Te wstępnie zdefiniowane zdarzenia są składowymi klas graficznego interfejsu użytkownika, takich jak formularze i formanty. Niestandardowe zachowanie można dodać do istniejącego zdarzenia, takiego jak kliknięcie przycisku, odwołując się do konkretnej nazwanego zdarzenia zainteresowania (na przykład `Click` zdarzenia `Form` klasy) i wywołując `Add` metodę, jak pokazano w poniższym kodzie. Jeśli uruchomisz ten program z F# Interactive, Pomiń wywołanie metody `System.Windows.Forms.Application.Run(System.Windows.Forms.Form)` .

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet3601.fs)]

Typ `Add` metody to `('a -> unit) -> unit` . W związku z tym metoda obsługi zdarzeń przyjmuje jeden parametr, zazwyczaj argumenty zdarzenia i zwraca `unit` . W poprzednim przykładzie pokazano program obsługi zdarzeń w postaci wyrażenia lambda. Program obsługi zdarzeń może być także wartością funkcji, tak jak w poniższym przykładzie kodu. W poniższym przykładzie kodu pokazano także użycie parametrów programu obsługi zdarzeń, które dostarczają informacje charakterystyczne dla typu zdarzenia. Dla `MouseMove` zdarzenia system przekazuje `System.Windows.Forms.MouseEventArgs` obiekt, który zawiera `X` `Y` położenie wskaźnika i.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet3602.fs)]

## <a name="creating-custom-events"></a>Tworzenie zdarzeń niestandardowych

Zdarzenia języka f # są reprezentowane przez typ [zdarzenia](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-control-fsharpevent-1.html) języka f #, który implementuje interfejs [IEvent](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-control-ievent-1.html) . `IEvent` jest samym interfejsem, który łączy funkcje dwóch innych interfejsów `System.IObservable<'T>` i [IDelegateEvent](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-control-idelegateevent-1.html). W związku z tym program `Event` s ma równoważne funkcje delegatów w innych językach oraz dodatkowe funkcje od `IObservable` , co oznacza, że zdarzenia języka f # obsługują filtrowanie zdarzeń oraz funkcje pierwszej klasy języka f # i wyrażenia lambda jako programy obsługi zdarzeń. Ta funkcja jest dostępna w [module Event](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-control-eventmodule.html).

Aby utworzyć zdarzenie na klasie, która działa podobnie jak wszystkie inne zdarzenia .NET Framework, Dodaj do klasy `let` powiązanie, które definiuje `Event` jako pole w klasie. Odpowiedni typ argumentu zdarzenia można określić jako argument typu, ale można też pozostawić ten typu pusty, co spowoduje, że kompilator wywnioskuje odpowiedni typ. Należy także zdefiniować element członkowski zdarzenia, który będzie uwidaczniał zdarzenie jako zdarzenie CLI. Ten element członkowski powinien mieć atrybut [CLIEvent](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-clieventattribute.html) . Jest on zadeklarowany jako właściwość, a jego implementacja jest tylko wywołaniem właściwości [Publish](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-control-fsharpevent-1.html#Publish) zdarzenia. Użytkownicy klasy mogą korzystać z `Add` metody opublikowanego zdarzenia w celu dodania procedury obsługi. Argument `Add` metody może być wyrażeniem lambda. Możesz użyć `Trigger` właściwości zdarzenia, aby zgłosić zdarzenie, przekazując argumenty do funkcji obsługi. Pokazano to w poniższym przykładzie kodu. W tym przykładzie wywnioskowany argument typu dla zdarzenia to spójna kolekcja, która reprezentuje argumenty wyrażenia lambda.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet3605.fs)]

Dane wyjściowe są następujące:

```console
Event1 occurred! Object data: Hello World!
```

Dodatkowe funkcje zapewniane przez moduł przedstawiono w `Event` tym miejscu. Poniższy przykład kodu ilustruje podstawowe użycie programu `Event.create` , aby utworzyć zdarzenie i metodę wyzwalacza, dodać dwa programy obsługi zdarzeń w postaci wyrażeń lambda, a następnie wyzwoli zdarzenie, aby wykonać oba wyrażenia lambda.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet3603.fs)]

Dane wyjściowe poprzedniego kodu wyglądają następująco:

```console
Event occurred.
Given a value: Event occurred.
```

## <a name="processing-event-streams"></a>Przetwarzanie strumieni zdarzeń

Zamiast tylko dodać procedurę obsługi zdarzeń dla zdarzenia przy użyciu funkcji [Event. Add](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-control-eventmodule.html#add) , można użyć funkcji w `Event` module do przetwarzania strumieni zdarzeń w sposób wysoce dostosowany. W tym celu należy użyć potoku do przodu ( `|>` ) wraz ze zdarzeniem jako pierwszą wartością w szeregu wywołań funkcji, a `Event` moduł działa jako kolejne wywołania funkcji.

W poniższym przykładzie kodu pokazano, jak skonfigurować zdarzenie, dla którego program obsługi jest wywoływany tylko w określonych warunkach.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet3604.fs)]

[Moduł zauważalny](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-control-observablemodule.html) zawiera podobne funkcje, które działają na obiektach zauważalnych. Widoczne obiekty są podobne do zdarzeń, ale aktywnie subskrybują zdarzenia tylko wtedy, gdy same są subskrybowane.

## <a name="implementing-an-interface-event"></a>Implementowanie zdarzenia interfejsu

Projektowanie składników interfejsu użytkownika często rozpoczyna się od utworzenia nowego formularza lub nowego formantu, który dziedziczy z istniejącego formularza lub formantu. Zdarzenia są często definiowane w interfejsie, a w takim przypadku trzeba zaimplementować interfejs służący do implementacji zdarzeń. `System.ComponentModel.INotifyPropertyChanged`Interfejs definiuje pojedyncze `System.ComponentModel.INotifyPropertyChanged.PropertyChanged` zdarzenie. Poniższy kod ilustruje sposób implementacji zdarzenia definiowanego przez ten dziedziczony interfejs:

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

Jeśli chcesz podłączyć zdarzenie w konstruktorze, kod jest nieco bardziej skomplikowany, ponieważ usługa Event podłączenie musi znajdować się w `then` bloku w dodatkowym konstruktorze, jak w poniższym przykładzie:

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

## <a name="see-also"></a>Zobacz także

- [Elementy członkowskie](index.md)
- [Obsługa i wywoływanie zdarzeń](../../../standard/events/index.md)
- [Wyrażenia lambda: `fun` słowo kluczowe](../functions/lambda-expressions-the-fun-keyword.md)
