---
title: Programowanie asynchroniczne
description: 'Dowiedz się, w jaki sposób język F # zapewnia czystą obsługę asynchroniczności w oparciu o model programowania na poziomie języka pochodzący z podstawowych koncepcji programowania funkcjonalnego.'
ms.date: 08/15/2020
ms.openlocfilehash: 04b397ddbfb468aa3bc4ee245175d3ec9bdedb50
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96739330"
---
# <a name="async-programming-in-f"></a>Programowanie asynchroniczne w F\#

Programowanie asynchroniczne jest mechanizmem, który jest niezbędny dla nowoczesnych aplikacji z różnych powodów. Istnieją dwa podstawowe przypadki użycia, które napotykają większość deweloperów:

- Przedstawienie procesu serwera, który może obsłużyć znaczną liczbę współbieżnych żądań przychodzących, jednocześnie minimalizując zasoby systemowe zajęte podczas przetwarzania żądań czeka na dane wejściowe z systemów lub usług zewnętrznych dla tego procesu
- Utrzymywanie odpowiedzi na interfejsie użytkownika lub głównego wątku podczas współbieżnego postępu pracy w tle

Mimo że prace w tle często obejmują wykorzystanie wielu wątków, ważne jest, aby rozważyć koncepcje asynchroniczności i wielowątkowości osobno. W rzeczywistości są one oddzielnymi problemami, a jeden z nich nie ma innych. W tym artykule opisano różne koncepcje bardziej szczegółowo.

## <a name="asynchrony-defined"></a>Asynchroniczności zdefiniowany

Poprzedni punkt — ten asynchroniczności jest niezależny od użycia wielu wątków — jest również bardziej opisowy. Istnieją trzy koncepcje, które są czasami powiązane, ale ściśle niezależne od siebie:

- Współbieżności gdy wiele obliczeń jest wykonywanych w nadchodzących okresach czasowych.
- Równoległości gdy wiele obliczeń lub kilka części jednego obliczenia jest wykonywanych w dokładnie tym samym czasie.
- Asynchroniczności gdy jedno lub więcej obliczeń można wykonać niezależnie od przepływu głównego programu.

Wszystkie trzy są koncepcjami prostopadłymi, ale można je łatwo rozliczać, szczególnie gdy są używane razem. Na przykład może być konieczne wykonanie wielu obliczeń asynchronicznych równolegle. Ta relacja nie oznacza, że równoległość lub asynchroniczności implikują sobie siebie nawzajem.

Jeśli rozważasz etymology słowa "asynchroniczne", istnieją dwa elementy:

- "a", znaczenie "nie".
- "synchroniczne", znaczenie "w tym samym czasie".

Po umieszczeniu tych dwóch terminów, zobaczysz, że "asynchroniczne" oznacza "nie w tym samym czasie". Gotowe. W tej definicji nie ma implikacji współbieżności ani równoległości. Ta metoda jest również prawdziwa.

W praktyce, asynchroniczne obliczenia w języku F # są zaplanowane do wykonania niezależnie od przepływu głównego programu. Niezależne wykonanie nie oznacza współbieżności ani równoległości, ani nie oznacza, że obliczenie zawsze odbywa się w tle. W rzeczywistości asynchroniczne obliczenia mogą nawet wykonywać synchronicznie, w zależności od rodzaju obliczenia i środowiska, w którym jest wykonywane obliczenie.

Głównym wnioskiemem jest to, że obliczenia asynchroniczne są niezależne od przepływu głównego programu. Chociaż istnieją pewne gwarancje dotyczące tego, kiedy lub jak są wykonywane asynchroniczne obliczenia, istnieją niektóre podejścia do organizowania i planowania. W pozostałej części tego artykułu przedstawiono podstawowe koncepcje dotyczące języka F # asynchroniczności oraz sposób używania typów, funkcji i wyrażeń wbudowanych w języku F #.

## <a name="core-concepts"></a>Podstawowe pojęcia

W języku F # programowanie asynchroniczne zawiera trzy podstawowe koncepcje:

- `Async<'T>`Typ, który reprezentuje szeregowe Obliczanie asynchroniczne.
- `Async`Funkcja module, która umożliwia planowanie pracy asynchronicznej, tworzenie obliczeń asynchronicznych i przekształcanie asynchronicznych wyników.
- `async { }` [Wyrażenie obliczeń](../../language-reference/computation-expressions.md), które zapewnia wygodną składnię do kompilowania i kontrolowania asynchronicznych obliczeń.

Te trzy koncepcje można zobaczyć w następującym przykładzie:

```fsharp
open System
open System.IO

let printTotalFileBytes path =
    async {
        let! bytes = File.ReadAllBytesAsync(path) |> Async.AwaitTask
        let fileName = Path.GetFileName(path)
        printfn $"File {fileName} has %d{bytes.Length} bytes"
    }

[<EntryPoint>]
let main argv =
    printTotalFileBytes "path-to-file.txt"
    |> Async.RunSynchronously

    Console.Read() |> ignore
    0
```

W przykładzie `printTotalFileBytes` Funkcja jest typu `string -> Async<unit>` . Wywołanie funkcji nie powoduje rzeczywistego wykonania obliczeń asynchronicznych. Zamiast tego zwraca obiekt `Async<unit>` , który działa jako *Specyfikacja* pracy, która jest wykonywana asynchronicznie. Wywołuje `Async.AwaitTask` w swojej treści, który konwertuje wynik <xref:System.IO.File.ReadAllBytesAsync%2A> do odpowiedniego typu.

Innym ważnym wierszem jest wywołanie metody `Async.RunSynchronously` . Jest to jeden z funkcji uruchamiania modułów asynchronicznych, które należy wywołać, jeśli chcesz rzeczywiście wykonać obliczenia asynchroniczne w języku F #.

Jest to podstawowa różnica w stylu programowania w języku C#/Visual Basic `async` . W języku F # asynchroniczne obliczenia można traktować jako **zimne zadania**. Muszą być jawnie uruchomione w celu rzeczywistego wykonania. Ma to pewne zalety, ponieważ umożliwia łączenie i sekwencję asynchronicznych zadań znacznie łatwiej niż w języku C# lub Visual Basic.

## <a name="combine-asynchronous-computations"></a>Łączenie asynchronicznych obliczeń

Oto przykład, który kompiluje się na poprzednim, przez połączenie obliczeń:

```fsharp
open System
open System.IO

let printTotalFileBytes path =
    async {
        let! bytes = File.ReadAllBytesAsync(path) |> Async.AwaitTask
        let fileName = Path.GetFileName(path)
        printfn $"File {fileName} has %d{bytes.Length} bytes"
    }

[<EntryPoint>]
let main argv =
    argv
    |> Array.map printTotalFileBytes
    |> Async.Parallel
    |> Async.Ignore
    |> Async.RunSynchronously

    0
```

Jak widać, `main` Funkcja ma wiele większej liczby wywołań. Koncepcyjnie wykonuje następujące czynności:

1. Przekształcanie argumentów wiersza polecenia w `Async<unit>` obliczenia za pomocą `Array.map` .
2. Utwórz `Async<'T[]>` harmonogramy i uruchamia `printTotalFileBytes` obliczenia równolegle, gdy zostanie uruchomione.
3. Utwórz `Async<unit>` , który będzie uruchamiać obliczenia równoległe i zignorować jego wynik.
4. Jawnie Uruchom ostatnie obliczenie z `Async.RunSynchronously` i blokuj do momentu jego zakończenia.

Po uruchomieniu tego programu Program `printTotalFileBytes` uruchamia się równolegle dla każdego argumentu wiersza polecenia. Ponieważ asynchroniczne obliczenia są wykonywane niezależnie od przepływu programu, nie ma kolejności, w której drukują informacje i kończą wykonywanie. Obliczenia będą wykonywane równolegle, ale ich kolejność wykonywania nie jest gwarantowana.

## <a name="sequence-asynchronous-computations"></a>Asynchroniczne obliczenia sekwencji

Ze względu `Async<'T>` na to, że jest to specyfikacja pracy, a nie zadania już uruchomionego, można łatwo wykonywać bardziej intricatee przekształcenia. Oto przykład, który służy do sekwencjonowania zestawu asynchronicznych obliczeń, tak aby były wykonywane jeden po drugim.

```fsharp
let printTotalFileBytes path =
    async {
        let! bytes = File.ReadAllBytesAsync(path) |> Async.AwaitTask
        let fileName = Path.GetFileName(path)
        printfn $"File {fileName} has %d{bytes.Length} bytes"
    }

[<EntryPoint>]
let main argv =
    argv
    |> Array.map printTotalFileBytes
    |> Async.Sequential
    |> Async.Ignore
    |> Async.RunSynchronously
    |> ignore
```

Spowoduje to zaplanowanie `printTotalFileBytes` wykonywania w kolejności elementów `argv` zamiast planowania ich równolegle. Ponieważ następny element nie zostanie zaplanowany do momentu zakończenia ostatniego obliczenia, obliczenia zostaną uporządkowane w taki sposób, że ich wykonanie nie nakłada się na siebie.

## <a name="important-async-module-functions"></a>Ważne funkcje modułu asynchronicznego

Gdy piszesz kod asynchroniczny w języku F #, zazwyczaj będziesz współdziałać z platformą, która obsługuje planowanie obliczeń. Nie jest to jednak zawsze przypadek, dlatego warto poznać różne funkcje uruchamiania w celu zaplanowania pracy asynchronicznej.

Ponieważ obliczenia asynchroniczne języka F # są _specyfikacją_ pracy, a nie reprezentacją już wykonywanej pracy, muszą być jawnie uruchomione przy użyciu funkcji początkowej. Istnieje wiele [metod uruchamiania asynchronicznego](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-control-fsharpasync.html#section0) , które są przydatne w różnych kontekstach. W poniższej sekcji opisano niektóre typowe funkcje uruchamiania.

### <a name="asyncstartchild"></a>Async. StartChild —

Uruchamia obliczenie elementu podrzędnego w ramach obliczeń asynchronicznych. Umożliwia to współbieżne wykonywanie wielu asynchronicznych obliczeń. Podrzędne obliczenie udostępnia token anulowania z obliczeniami nadrzędnymi. Jeśli Obliczanie nadrzędne zostanie anulowane, obliczenia podrzędne również zostaną anulowane.

Podpis:

```fsharp
computation: Async<'T> * timeout: ?int -> Async<Async<'T>>
```

Kiedy używać:

- Jeśli chcesz wykonać wiele asynchronicznych obliczeń jednocześnie, a nie jeden na raz, ale nie zaplanowano ich równolegle.
- Gdy chcesz powiązać okres istnienia obliczeń podrzędnych z tym, że jest to obliczenie nadrzędne.

Co należy obserwować:

- Uruchamianie wielu obliczeń za pomocą `Async.StartChild` nie jest takie samo jak planowanie ich równolegle. Jeśli chcesz zaplanować obliczenia równolegle, użyj `Async.Parallel` .
- Anulowanie obliczenia nadrzędnego spowoduje anulowanie wszystkich rozpoczętych obliczeń podrzędnych.

### <a name="asyncstartimmediate"></a>Async. StartImmediate —

Uruchamia asynchroniczne obliczenie, rozpoczynając od razu od bieżącego wątku systemu operacyjnego. Jest to przydatne, jeśli trzeba zaktualizować coś w wątku wywołującym podczas obliczania. Na przykład jeśli asynchroniczne obliczenie musi zaktualizować interfejs użytkownika (na przykład zaktualizować pasek postępu), `Async.StartImmediate` należy go użyć.

Podpis:

```fsharp
computation: Async<unit> * cancellationToken: ?CancellationToken -> unit
```

Kiedy używać:

- Gdy trzeba zaktualizować coś w wątku wywołującym w środku obliczeń asynchronicznych.

Co należy obserwować:

- Kod w asynchronicznym obliczaniu zostanie uruchomiony niezależnie od wątku, w którym ma zostać zaplanowana. Może to być problematyczne, jeśli ten wątek jest w sposób niezależny, na przykład wątek interfejsu użytkownika. W takich przypadkach `Async.StartImmediate` prawdopodobnie jest nieodpowiedni do użycia.

### <a name="asyncstartastask"></a>Async. Startastask —

Wykonuje obliczenia w puli wątków. Zwraca wartość <xref:System.Threading.Tasks.Task%601> , która zostanie zakończona w odpowiadającym stanie po zakończeniu obliczeń (tworzy wynik, zgłasza wyjątek lub jest anulowany). Jeśli nie podano tokenu anulowania, zostanie użyty domyślny token anulowania.

Podpis:

```fsharp
computation: Async<'T> * taskCreationOptions: ?TaskCreationOptions * cancellationToken: ?CancellationToken -> Task<'T>
```

Kiedy używać:

- Gdy musisz wywołać interfejs API platformy .NET, który oczekuje na <xref:System.Threading.Tasks.Task%601> wynik obliczeń asynchronicznych.

Co należy obserwować:

- To wywołanie spowoduje przydzielenie dodatkowego `Task` obiektu, co może zwiększyć obciążenie, jeśli jest używane często.

### <a name="asyncparallel"></a>Async. Parallel

Planuje sekwencję asynchronicznych obliczeń, które mają być wykonywane równolegle. Stopień równoległości można opcjonalnie dostrajać/ograniczyć przez określenie `maxDegreesOfParallelism` parametru.

Podpis:

```fsharp
computations: seq<Async<'T>> * ?maxDegreesOfParallelism: int -> Async<'T[]>
```

Kiedy używać go:

- Jeśli konieczne jest uruchomienie zestawu obliczeń w tym samym czasie i nie ma on zależności od ich kolejności wykonywania.
- Jeśli nie są wymagane wyniki z obliczeń zaplanowanych równolegle, dopóki nie zostaną ukończone.

Co należy obserwować:

- Można uzyskać dostęp tylko do wyników tablicy wartości po zakończeniu wszystkich obliczeń.
- Obliczenia zostaną uruchomione po każdym zaplanowaniu. To zachowanie oznacza, że nie można polegać na ich kolejności wykonywania.

### <a name="asyncsequential"></a>Async. sekwencyjny

Planuje sekwencję asynchronicznych obliczeń do wykonania w kolejności, w jakiej zostały przesłane. Pierwsze obliczenie zostanie wykonane, następnie następne i tak dalej. Żadne obliczenia nie będą wykonywane równolegle.

Podpis:

```fsharp
computations: seq<Async<'T>> -> Async<'T[]>
```

Kiedy używać go:

- Jeśli konieczne jest wykonanie wielu obliczeń w kolejności.

Co należy obserwować:

- Można uzyskać dostęp tylko do wyników tablicy wartości po zakończeniu wszystkich obliczeń.
- Obliczenia będą wykonywane w kolejności, w jakiej są przesyłane do tej funkcji, co może oznaczać, że upłynie więcej czasu przed zwróceniem wyników.

### <a name="asyncawaittask"></a>Async. Awaittask —

Zwraca asynchroniczne obliczenie, które czeka na zakończenie danego elementu <xref:System.Threading.Tasks.Task%601> i zwraca jego wynik jako `Async<'T>`

Podpis:

```fsharp
task: Task<'T> -> Async<'T>
```

Kiedy używać:

- Gdy korzystasz z interfejsu API platformy .NET, który zwraca <xref:System.Threading.Tasks.Task%601> w ramach obliczeń asynchronicznych języka F #.

Co należy obserwować:

- Wyjątki są opakowane w <xref:System.AggregateException> ramach Konwencji równoległej biblioteki zadań, a to zachowanie różni się od tego, w jaki sposób asynchronicznie zawiera ogólne powierzchnie w języku F #.

### <a name="asynccatch"></a>Async. catch

Tworzy asynchroniczne obliczenie, które wykonuje daną `Async<'T>` , zwracając `Async<Choice<'T, exn>>` . Jeśli podano `Async<'T>` pomyślnie, `Choice1Of2` zostanie zwrócona wartość wynikowy. Jeśli przed zakończeniem zostanie zgłoszony wyjątek, a następnie `Choice2of2` zwracany jest wyjątek. Jeśli jest używany w przypadku obliczeń asynchronicznych, które są tworzone w wielu obliczeniach, a jedno z tych obliczeń zgłasza wyjątek, obliczenia obejmujące obejmie zostaną całkowicie zatrzymane.

Podpis:

```fsharp
computation: Async<'T> -> Async<Choice<'T, exn>>
```

Kiedy używać:

- Gdy wykonujesz asynchroniczne zadanie, które może zakończyć się niepowodzeniem z wyjątkiem i chcesz obsłużyć ten wyjątek w obiekcie wywołującym.

Co należy obserwować:

- W przypadku korzystania z połączonych lub sekwencyjnych obliczeń asynchronicznych Obliczanie obejmujące obliczenia zostanie całkowicie zatrzymane, jeśli jedno z jego "wewnętrznego" obliczeń zgłosi wyjątek.

### <a name="asyncignore"></a>Async. Ignore

Tworzy asynchroniczne obliczenie, które uruchamia danego obliczenia i ignoruje jego wynik.

Podpis:

```fsharp
computation: Async<'T> -> Async<unit>
```

Kiedy używać:

- W przypadku obliczeń asynchronicznych, których wynik nie jest wymagany. Jest to analogiczny `ignore` kod nieasynchroniczny.

Co należy obserwować:

- Jeśli musisz użyć `Async.Ignore` programu, ponieważ chcesz użyć `Async.Start` lub innej funkcji, która jest wymagana `Async<unit>` , weź pod uwagę, czy odrzucanie wyniku jest dobry. Unikaj odrzucania wyników tylko w celu dopasowania do podpisu typu.

### <a name="asyncrunsynchronously"></a>Async. metody RunSynchronously

Uruchamia asynchroniczne obliczenie i czeka na wynik wątku wywołującego. To wywołanie blokuje.

Podpis:

```fsharp
computation: Async<'T> * timeout: ?int * cancellationToken: ?CancellationToken -> 'T
```

Kiedy używać go:

- Jeśli potrzebujesz tego, użyj go tylko raz w aplikacji — w punkcie wejścia dla pliku wykonywalnego.
- Gdy nie masz opieki nad wydajnością i chcesz wykonać zestaw innych operacji asynchronicznych jednocześnie.

Co należy obserwować:

- Wywoływanie `Async.RunSynchronously` blokuje wątek wywołujący do momentu zakończenia wykonywania.

### <a name="asyncstart"></a>Async. Start

Uruchamia asynchroniczne obliczenie w puli wątków, która zwraca `unit` . Nie czeka na jego wynik. Zagnieżdżone obliczenia rozpoczęte przy użyciu `Async.Start` są uruchamiane niezależnie od obliczeń nadrzędnych, które je wywołały. Ich okres istnienia nie jest powiązany z żadnym z obliczeń nadrzędnych. Jeśli Obliczanie nadrzędne zostało anulowane, nie są anulowane żadne obliczenia podrzędne.

Podpis:

```fsharp
computation: Async<unit> * cancellationToken: ?CancellationToken -> unit
```

Używaj tylko wtedy, gdy:

- Istnieje asynchroniczne obliczenie, które nie zwraca wyniku i/lub wymaga przetwarzania jednego.
- Nie musisz wiedzieć, kiedy kończy się Obliczanie asynchroniczne.
- Nie musisz określać wątku, w którym jest wykonywane asynchroniczne obliczenie.
- Nie trzeba znać ani zgłosić wyjątków wynikających z zadania.

Co należy obserwować:

- Wyjątki wywoływane przez obliczenia rozpoczęte z `Async.Start` nie są propagowane do obiektu wywołującego. Stos wywołań zostanie całkowicie odłożony.
- Każda z zadań (takich jak wywoływanie `printfn` ) rozpoczyna się od `Async.Start` nie spowoduje wystąpienia efektu w głównym wątku wykonywania programu.

## <a name="interoperate-with-net"></a>Współdziałanie z platformą .NET

Być może pracujesz z biblioteką .NET lub bazą kodu C#, która używa programowania asynchronicznego [/await](../../../standard/async.md)w stylu. Ze względu na to, że język C# i większość bibliotek .NET używają <xref:System.Threading.Tasks.Task%601> <xref:System.Threading.Tasks.Task> typów i jako ich podstawowych streszczeń, a nie, należy przeprowadzić `Async<'T>` granicę między tymi dwoma podejściami do asynchroniczności.

### <a name="how-to-work-with-net-async-and-taskt"></a>Jak korzystać z komunikacji asynchronicznej .NET i `Task<T>`

Praca z bibliotekami asynchronicznymi platformy .NET i bazami kodu, które używają <xref:System.Threading.Tasks.Task%601> (czyli obliczeń asynchronicznych, które mają zwracane wartości) jest prosta i wbudowana obsługa języka F #.

Można użyć funkcji, `Async.AwaitTask` aby oczekiwać na asynchroniczne Obliczanie na platformie .NET:

```fsharp
let getValueFromLibrary param =
    async {
        let! value = DotNetLibrary.GetValueAsync param |> Async.AwaitTask
        return value
    }
```

Można użyć funkcji, `Async.StartAsTask` Aby przekazać asynchroniczne obliczenie do obiektu wywołującego platformy .NET:

```fsharp
let computationForCaller param =
    async {
        let! result = getAsyncResult param
        return result
    } |> Async.StartAsTask
```

### <a name="how-to-work-with-net-async-and-task"></a>Jak korzystać z komunikacji asynchronicznej .NET i `Task`

Aby można było korzystać z interfejsów API, które używają <xref:System.Threading.Tasks.Task> (czyli obliczeń asynchronicznych platformy .NET, które nie zwracają wartości), może być konieczne dodanie dodatkowej funkcji, która spowoduje przekonwertowanie `Async<'T>` na <xref:System.Threading.Tasks.Task> :

```fsharp
module Async =
    // Async<unit> -> Task
    let startTaskFromAsyncUnit (comp: Async<unit>) =
        Async.StartAsTask comp :> Task
```

Istnieje już element `Async.AwaitTask` , który akceptuje <xref:System.Threading.Tasks.Task> jako dane wejściowe. Za pomocą tej i wcześniej zdefiniowanej `startTaskFromAsyncUnit` funkcji można rozpocząć i oczekiwać <xref:System.Threading.Tasks.Task> typów z obliczeń asynchronicznych języka F #.

## <a name="relationship-to-multi-threading"></a>Relacja do wielowątkowości

Chociaż wątki są wymienione w tym artykule, istnieją dwie ważne kwestie, które należy zapamiętać:

1. Nie ma koligacji między asynchronicznym obliczaniem a wątkiem, chyba że jest on jawnie uruchamiany w bieżącym wątku.
1. Programowanie asynchroniczne w języku F # nie jest abstrakcją dla wielowątkowości.

Na przykład obliczenia mogą być uruchamiane w wątku wywołującego, w zależności od rodzaju pracy. Obliczenia mogą również "przeskoczyć" między wątkami, co pociąga za sobą niewielką ilość czasu, aby wykonywać przydatne działania w okresie "oczekiwanie" (na przykład podczas przesyłania połączenia sieciowego).

Chociaż język F # zapewnia pewne możliwości uruchamiania obliczeń asynchronicznych w bieżącym wątku (lub jawnie nie w bieżącym wątku), asynchroniczności zazwyczaj nie jest skojarzony z określoną strategią wątkowości.

## <a name="see-also"></a>Zobacz także

- [Asynchroniczny model programowania F #](https://www.microsoft.com/research/publication/the-f-asynchronous-programming-model)
- [Przewodnik asynchroniczny języka F # dla aparatu Jet. com](https://medium.com/jettech/f-async-guide-eb3c8a2d180a)
- [Przewodnik po programowaniu asynchronicznym w języku F # dla zabawy i zysków](https://fsharpforfunandprofit.com/posts/concurrency-async-and-parallel/)
- [Asynchroniczne w językach C# i F #: asynchroniczna pytania dotyczące usługi w języku C #](http://tomasp.net/blog/csharp-async-gotchas.aspx/)
