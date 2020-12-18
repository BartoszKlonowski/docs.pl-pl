---
title: Co nowego w języku C# 7,0 — przewodnik w języku C#
description: Zapoznaj się z omówieniem nowych funkcji w wersji 7,0 języka C#.
ms.date: 10/02/2020
ms.assetid: fd41596d-d0c2-4816-b94d-c4d00a5d0243
ms.openlocfilehash: c238439b0f435e579d932b3b1eb13e9b0061fa5f
ms.sourcegitcommit: 4b79862c5b41fbd86cf38f926f6a49516059f6f2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/18/2020
ms.locfileid: "97678227"
---
# <a name="whats-new-in-c-70-through-c-73"></a>Co nowego w języku C# 7,0 za poorednictwem języka C# 7,3

W języku c# 7,0 do języka C# 7,3 wprowadzono wiele funkcji i przyrostowe ulepszenia środowiska programistycznego w języku C#. Ten artykuł zawiera omówienie nowych funkcji języka i opcji kompilatora. Opisy opisują zachowanie języka C# 7,3, który jest najnowszą wersją obsługiwaną dla aplikacji opartych na .NET Framework.

Element konfiguracji [wyboru wersji języka](../language-reference/configure-language-version.md) został dodany przy użyciu języka C# 7,1, który umożliwia określenie wersji języka kompilatora w pliku projektu.

C# 7.0 — 7.3 dodaje te funkcje i motywy do języka C#:

- [Krotki i odrzuty](#tuples-and-discards)
  - Można tworzyć lekkie, nienazwane typy, które zawierają wiele pól publicznych. Narzędzia kompilatora i IDE rozumieją semantykę tych typów.
  - Odrzucenia są tymczasowymi zmiennymi tylko do zapisu, które są używane w przypisaniach, gdy nie ma opieki nad przypisaną wartością. Są one najbardziej przydatne podczas dekonstrukcji krotek i typów zdefiniowanych przez użytkownika, a także podczas wywoływania metod z `out` parametrami.
- [Dopasowanie wzorca](#pattern-matching)
  - Można utworzyć logikę rozgałęziania na podstawie dowolnego typu i wartości elementów członkowskich tych typów.
- [`async``Main`Metoda](#async-main)
  - Punkt wejścia dla aplikacji może mieć `async` modyfikator.
- [Funkcje lokalne](#local-functions)
  - Funkcje w innych funkcjach można zagnieżdżać w celu ograniczenia ich zakresu i widoczności.
- [Więcej składowych wyrażeń](#more-expression-bodied-members)
  - Lista elementów członkowskich, które mogą zostać utworzone przy użyciu wyrażeń.
- [`throw` Wyrażeń](#throw-expressions)
  - Można zgłosić wyjątki w konstrukcjach kodu, które wcześniej nie były dozwolone, ponieważ `throw` była instrukcją.
- [`default` wyrażenia literału](#default-literal-expressions)
  - Można użyć domyślnych wyrażeń literałów w wyrażeniach wartości domyślnych, gdy można wywnioskować typ docelowy.
- [Udoskonalenia składni literału liczbowego](#numeric-literal-syntax-improvements)
  - Nowe tokeny zwiększają czytelność dla stałych numerycznych.
- [`out` modyfikacj](#out-variables)
  - Można zadeklarować `out` wartości jako argumenty metody, gdzie są używane.
- [Argumenty nazwane inne niż końcowe](#non-trailing-named-arguments)
  - Po nazwanych argumentach mogą występować argumenty pozycyjne.
- [`private protected` Modyfikator dostępu](#private-protected-access-modifier)
  - `private protected`Modyfikator dostępu umożliwia dostęp do klas pochodnych w tym samym zestawie.
- [Ulepszone rozwiązanie przeciążania](#improved-overload-candidates)
  - Nowe reguły do rozwiązywania niejednoznaczności rozpoznawania przeciążenia.
- [Techniki pisania bezpiecznego wydajnego kodu](#enabling-more-efficient-safe-code)
  - Kombinacja ulepszeń składni, które umożliwiają pracę z typami wartości przy użyciu semantyki referencyjnej.

Na koniec kompilator ma nowe opcje:

- `-refout` i `-refonly` tej kontrolki [generacji zestawu odwołania](#reference-assembly-generation).
- `-publicsign` Aby włączyć podpisywanie zestawów przez oprogramowanie typu Open Source (OSS).
- `-pathmap` w celu zapewnienia mapowania dla katalogów źródłowych.

Pozostała część tego artykułu zawiera omówienie każdej funkcji. Dla każdej funkcji należy zapoznać się z jej uzasadnieniem i składnią. Te funkcje można eksplorować w środowisku za pomocą `dotnet try` Narzędzia globalnego:

1. Zainstaluj narzędzie [dotnet-try](https://github.com/dotnet/try/blob/master/README.md#setup) Global.
1. Sklonuj repozytorium [dotnet/try-Samples](https://github.com/dotnet/try-samples) .
1. Ustaw bieżący katalog na podkatalog *csharp7* dla repozytorium *try-Samples* .
1. Uruchom polecenie `dotnet try`.

## <a name="tuples-and-discards"></a>Krotki i odrzuty

Język C# zawiera rozbudowaną składnię dla klas i struktur, które są używane do wyjaśnienia zamiaru projektowania. Jednak czasami rozbudowana Składnia wymaga dodatkowej pracy z minimalną korzyścią. Często możesz pisać metody, które potrzebują prostej struktury zawierającej więcej niż jeden element danych. Aby obsługiwać te scenariusze, *krotki* zostały dodane do języka C#. Krotki są lekkimi strukturami danych, które zawierają wiele pól do reprezentowania elementów członkowskich danych. Pola nie są weryfikowane i nie można definiować własnych metod. Typy krotek języka C# obsługują `==` i `!=` . Więcej informacji.

> [!NOTE]
> Krotki były dostępne przed C# 7,0, ale były niewydajne i nie obsługiwały języka. Oznacza to, że elementy krotki mogą być przywoływane tylko jako `Item1` `Item2` i tak dalej. W języku C# 7,0 wprowadzono obsługę języka dla krotek, która umożliwia używanie nazw semantycznych dla pól krotki przy użyciu nowych, wydajniejszych typów krotek.

Można utworzyć krotkę, przypisując wartość do każdego elementu członkowskiego, a opcjonalnie dostarczając nazwy semantyczne dla każdego z elementów członkowskich krotki:

[!code-csharp[NamedTuple](~/samples/snippets/csharp/new-in-7/program.cs#NamedTuple "Named tuple")]

`namedLetters`Krotka zawiera pola, które są określane jako `Alpha` i `Beta` . Te nazwy istnieją tylko w czasie kompilacji i nie są zachowywane, na przykład podczas sprawdzania krotki przy użyciu odbicia w czasie wykonywania.

W przypisaniu spójnej kolekcji można także określić nazwy pól po prawej stronie przypisania:

[!code-csharp[ImplicitNamedTuple](~/samples/snippets/csharp/new-in-7/program.cs#ImplicitNamedTuple "Implicitly named tuple")]

Mogą wystąpić sytuacje, w których chcesz rozpakować elementy członkowskie spójnej kolekcji, która została zwrócona z metody.  Można to zrobić przez zadeklarowanie oddzielnych zmiennych dla każdej wartości w spójnej kolekcji. To rozpakowanie nosi nazwę *dekonstrukcja* krotki:

[!code-csharp[CallingWithDeconstructor](~/samples/snippets/csharp/new-in-7/program.cs#CallingWithDeconstructor "Deconstructing a tuple")]

Można także zapewnić podobną dekonstrukcję dla dowolnego typu w programie .NET. Należy napisać `Deconstruct` metodę jako element członkowski klasy. Ta `Deconstruct` Metoda zapewnia zestaw `out` argumentów dla każdej właściwości, które mają zostać wyodrębnione. Rozważmy tę `Point` klasę, która zapewnia metodę dekonstruktora, która `X` wyodrębnia `Y` współrzędne i:

[!code-csharp[PointWithDeconstruction](~/samples/snippets/csharp/new-in-7/point.cs#PointWithDeconstruction "Point with deconstruction method")]

Poszczególne pola można wyodrębnić, przypisując `Point` do krotki:

[!code-csharp[DeconstructPoint](~/samples/snippets/csharp/new-in-7/program.cs#DeconstructPoint "Deconstruct a point")]

Wiele razy podczas inicjowania krotki zmienne używane po prawej stronie przypisania są takie same jak nazwy dla elementów krotki: nazwy elementów krotki mogą być wywnioskowane na podstawie zmiennych używanych do inicjowania krotki:

```csharp
int count = 5;
string label = "Colors used in the map";
var pair = (count, label); // element names are "count" and "label"
```

Więcej informacji na temat tej funkcji można znaleźć w artykule [typy krotek](../language-reference/builtin-types/value-tuples.md) .

Często podczas dekonstruowania krotki lub wywoływania metody z `out` parametrami należy wymusić zdefiniowanie zmiennej, której wartość nie ma znaczenia, i nie zamierza się jej używać. Język C# dodaje obsługę *odrzutów* , aby obsłużyć ten scenariusz. Odrzucanie to zmienna tylko do zapisu, której nazwa to `_` (znak podkreślenia); można przypisać wszystkie wartości, które mają zostać odrzucone do pojedynczej zmiennej. Odrzucenie przypomina przypisaną zmienną; poza instrukcją przypisania nie można używać odrzucania w kodzie.

Odrzucenia są obsługiwane w następujących scenariuszach:

- Podczas dekonstrukcji krotek lub typów zdefiniowanych przez użytkownika.
- Podczas wywoływania metod z parametrami [out](../language-reference/keywords/out-parameter-modifier.md) .
- W operacji dopasowania wzorca z instrukcjami with [i](../language-reference/keywords/is.md) [Switch](../language-reference/keywords/switch.md) .
- Jako identyfikator autonomiczny, gdy chcesz jawnie określić wartość przypisania jako odrzucenie.

W poniższym przykładzie zdefiniowano `QueryCityDataForYears` metodę, która zwraca 6-krotkę zawierającą dane dla miasta na dwa różne lata. Wywołanie metody w przykładzie jest rozważane tylko z dwiema wartościami populacji zwracanymi przez metodę i dlatego traktują pozostałe wartości w spójnej kolekcji jako odrzucane podczas dekonstruowania krotki.

[!code-csharp[Tuple-discard](~/samples/snippets/csharp/programming-guide/deconstructing-tuples/discard-tuple1.cs)]

Aby uzyskać więcej informacji, zobacz [odrzucanie](../discards.md).

## <a name="pattern-matching"></a>Dopasowanie do wzorca

*Dopasowanie wzorca* to zestaw funkcji umożliwiających nowe sposoby wyrażania przepływu sterowania w kodzie. Można testować zmienne dla ich typów, wartości lub wartości właściwości. Techniki te tworzą bardziej czytelny przepływ kodu.

Dopasowywanie wzorców obsługuje `is` wyrażenia i `switch` wyrażenia. Każdy umożliwia inspekcję obiektu i jego właściwości w celu ustalenia, czy ten obiekt spełnia oczekiwany wzorzec. Użyj `when` słowa kluczowego, aby określić dodatkowe reguły do wzorca.

`is`Wyrażenie wzorca rozszerza znanego [ `is` operatora](../language-reference/keywords/is.md#pattern-matching-with-is) w celu zbadania obiektu o jego typie i przypisuje wynik w jednej instrukcji. Poniższy kod sprawdza, czy zmienna jest `int` , i jeśli tak, dodaje ją do bieżącej sumy:

```csharp
if (input is int count)
    sum += count;
```

Powyższy mały przykład ilustruje ulepszenia `is` wyrażenia. Można testować względem typów wartości, a także typów referencyjnych, a następnie można przypisać prawidłowy wynik do nowej zmiennej poprawnego typu.

Wyrażenie dopasowania przełącznika ma znaną składnię opartą na instrukcji, która jest `switch` już częścią języka C#. Zaktualizowana instrukcja SWITCH zawiera kilka nowych konstrukcji:

- Typ decydujący `switch` wyrażenia nie jest już ograniczony do typów całkowitych, `Enum` typów, `string` lub typu dopuszczającego wartość null odpowiadającego jednemu z tych typów. Można użyć dowolnego typu.
- Możesz przetestować typ `switch` wyrażenia w każdej `case` etykiecie. Podobnie jak w przypadku `is` wyrażenia, można przypisać nową zmienną do tego typu.
- Można dodać `when` klauzulę do dalszych warunków testowania dla tej zmiennej.
- Kolejność `case` etykiet jest teraz ważna. Pierwsza gałąź do dopasowania jest wykonywana; pozostałe są pomijane.

Poniższy kod ilustruje następujące nowe funkcje:

```csharp
public static int SumPositiveNumbers(IEnumerable<object> sequence)
{
    int sum = 0;
    foreach (var i in sequence)
    {
        switch (i)
        {
            case 0:
                break;
            case IEnumerable<int> childSequence:
            {
                foreach(var item in childSequence)
                    sum += (item > 0) ? item : 0;
                break;
            }
            case int n when n > 0:
                sum += n;
                break;
            case null:
                throw new NullReferenceException("Null found in sequence");
            default:
                throw new InvalidOperationException("Unrecognized type");
        }
    }
    return sum;
}
```

- `case 0:` jest znanym wzorcem stałej.
- `case IEnumerable<int> childSequence:` jest wzorcem typu.
- `case int n when n > 0:` jest wzorcem typu z dodatkowym `when` warunkiem.
- `case null:` jest wzorcem o wartości null.
- `default:` jest znanym domyślnym przypadkiem.

Począwszy od języka C# 7,1 wyrażenie wzorca dla `is` i `switch` wzorzec typu może mieć typ parametru typu ogólnego. Może to być najbardziej przydatne podczas sprawdzania typów, które mogą być `struct` albo `class` typu, i chcesz uniknąć pakowania.

Dowiedz się więcej na temat dopasowywania wzorców we [wzorcu w języku C#](../pattern-matching.md).

## <a name="async-main"></a>Asynchroniczny, główny

Metoda *Async Main* umożliwia korzystanie `await` z `Main` metody. Wcześniej należy napisać:

```csharp
static int Main()
{
    return DoAsyncWork().GetAwaiter().GetResult();
}
```

Teraz możesz napisać:

```csharp
static async Task<int> Main()
{
    // This could also be replaced with the body
    // DoAsyncWork, including its await expressions:
    return await DoAsyncWork();
}
```

Jeśli program nie zwraca kodu zakończenia, można zadeklarować `Main` metodę, która zwraca <xref:System.Threading.Tasks.Task> :

```csharp
static async Task Main()
{
    await SomeAsyncMethod();
}
```

Więcej informacji na temat szczegółowych informacji można znaleźć w artykule dotyczącym [asynchronicznego](../programming-guide/main-and-command-args/index.md) artykułu w przewodniku programowania.

## <a name="local-functions"></a>Funkcje lokalne

Wiele projektów klas obejmuje metody, które są wywoływane tylko z jednej lokalizacji. Te dodatkowe metody prywatne przechowują każdą metodę na małe i skoncentrowane. *Funkcje lokalne* umożliwiają deklarowanie metod wewnątrz kontekstu innej metody. Funkcje lokalne ułatwiają czytelnikom klasy sprawdzenie, czy metoda lokalna jest wywoływana tylko z kontekstu, w którym jest zadeklarowana.

Istnieją dwa typowe przypadki użycia funkcji lokalnych: metody iteratora publicznego i publiczne metody async. Oba typy metod generują kod, który zgłasza błędy później niż programiści mogą oczekiwać. W metodach iteratora wszystkie wyjątki są obserwowane tylko podczas wywoływania kodu, który wylicza zwracaną sekwencję. W metodach asynchronicznych wszelkie wyjątki są przestrzegane tylko wtedy, gdy zwracane `Task` jest oczekiwane. Poniższy przykład ilustruje oddzielanie walidacji parametrów od implementacji iteratora przy użyciu funkcji lokalnej:

[!code-csharp[22_IteratorMethodLocal](~/samples/snippets/csharp/new-in-7/Iterator.cs#IteratorMethodLocal "Iterator method with local function")]

Ta sama technika może być stosowana z `async` metodami, aby zapewnić, że wyjątki wynikające z walidacji argumentów są zgłaszane przed rozpoczęciem pracy asynchronicznej:

[!code-csharp[TaskExample](~/samples/snippets/csharp/new-in-7/AsyncWork.cs#TaskExample "Task returning method with local function")]

Ta składnia jest teraz obsługiwana:

```csharp
[field: SomeThingAboutFieldAttribute]
public int SomeProperty { get; set; }
```

Ten atrybut `SomeThingAboutFieldAttribute` jest stosowany do pola zapasowego wygenerowanego przez kompilator dla `SomeProperty` . Aby uzyskać więcej informacji, zobacz [atrybuty](../programming-guide/concepts/attributes/index.md) w Przewodnik programowania w języku C#.

> [!NOTE]
> Niektóre projekty, które są obsługiwane przez funkcje lokalne, można również zrealizować przy użyciu *wyrażeń lambda*. Aby uzyskać więcej informacji, zobacz temat [funkcje lokalne a wyrażenia lambda](../programming-guide/classes-and-structs/local-functions.md#local-functions-vs-lambda-expressions).

## <a name="more-expression-bodied-members"></a>Więcej składowych wyrażeń

W języku C# 6 wprowadzono składowe z wyrażeniami dla funkcji Członkowskich i właściwości tylko do odczytu. C# 7,0 rozwija dozwolone elementy członkowskie, które mogą być zaimplementowane jako wyrażenia. W języku C# 7,0 można zaimplementować *konstruktory*, *finalizatory* i metody `get` `set` dostępu do *Właściwości* i *indeksatorów*. Poniższy kod przedstawia przykłady każdego z nich:

[!code-csharp[ExpressionBodiedMembers](~/samples/snippets/csharp/new-in-7/expressionmembers.cs#ExpressionBodiedEverything "new expression-bodied members")]

> [!NOTE]
> Ten przykład nie wymaga finalizatora, ale jest pokazywany do zademonstrowania składni. Nie należy implementować finalizatora w klasie, chyba że konieczne jest zwolnienie niezarządzanych zasobów. Należy również rozważyć użycie <xref:System.Runtime.InteropServices.SafeHandle> klasy zamiast bezpośrednio zarządzać niezarządzanymi zasobami.

Te nowe lokalizacje dla elementów członkowskich zabudowanych w wyrażeniach reprezentują ważne punkty kontrolne języka C#: te funkcje zostały zaimplementowane przez członków społeczności pracujących w projekcie [Roslyn](https://github.com/dotnet/Roslyn) typu open source.

Zmiana metody na wyrażenie składowane składowej jest [zgodną z binarną zmianą](version-update-considerations.md#binary-compatible-changes).

## <a name="throw-expressions"></a>Wyrażenia throw

W języku C# `throw` zawsze była instrukcją. Ponieważ `throw` jest instrukcją, a nie wyrażeniem, istnieją konstrukcje języka C#, w których nie można było ich użyć. Uwzględnione wyrażenia warunkowe, wyrażenia łączenia o wartości null i niektóre wyrażenia lambda. Dodanie elementów członkowskich będących członkami wyrażeń dodaje więcej lokalizacji, w których `throw` wyrażenia byłyby przydatne. Aby można było napisać dowolne z tych konstrukcji, w języku C# 7,0 wprowadzono [*wyrażenia throw*](../language-reference/keywords/throw.md#the-throw-expression).

To dodanie ułatwia zapisanie więcej kodu opartego na wyrażeniach. Nie potrzebujesz dodatkowych instrukcji do sprawdzania błędów.

## <a name="default-literal-expressions"></a>Domyślne wyrażenia literału

Domyślne wyrażenia literałów to ulepszenie wyrażeń wartości domyślnych. Te wyrażenia inicjują zmienną do wartości domyślnej. Gdzie wcześniej warto napisać:

```csharp
Func<string, bool> whereClause = default(Func<string, bool>);
```

Możesz teraz pominąć typ po prawej stronie inicjalizacji:

```csharp
Func<string, bool> whereClause = default;
```

Aby uzyskać więcej informacji, zobacz sekcję [domyślny literał](../language-reference/operators/default.md#default-literal) w artykule [domyślny operator](../language-reference/operators/default.md) .

## <a name="numeric-literal-syntax-improvements"></a>Udoskonalenia składni literału liczbowego

Nieodczytanie stałych numerycznych może utrudnić zrozumienie kodu podczas odczytywania go po raz pierwszy. Maski bitowe lub inne wartości symboliczne są podatne na nieporozumienia. Język C# 7,0 zawiera dwie nowe funkcje do zapisu liczb w najbardziej czytelny sposób dla zamierzonego użycia: *literały binarne* oraz *separatory cyfr*.

Dla tych czasów podczas tworzenia masek bitowych lub za każdym razem, gdy binarna reprezentacja liczby sprawia, że jest to najbardziej czytelny kod, Zapisz ten numer w postaci binarnej:

[!code-csharp[ThousandSeparators](~/samples/snippets/csharp/new-in-7/Program.cs#ThousandSeparators "Thousands separators")]

`0b`Na początku stała wskazuje, że liczba jest zapisywana jako liczba binarna. Liczby binarne mogą być długie, więc często łatwiej jest zobaczyć wzorce bitowe, wprowadzając `_` jako separator cyfr, jak pokazano w powyższym przykładzie w postaci binarnej. Separator cyfr może pojawić się w dowolnym miejscu w stałej. W przypadku numerów podstawowych 10 często należy używać jej jako separatora tysięcy. Szesnastkowe i binarne literały numeryczne mogą zaczynać się od `_` :

[!code-csharp[LargeIntegers](~/samples/snippets/csharp/new-in-7/Program.cs#LargeIntegers "Large integer")]

Separator cyfr może być używany z `decimal` , `float` i `double` również typy:

[!code-csharp[OtherConstants](~/samples/snippets/csharp/new-in-7/Program.cs#OtherConstants "non-integral constants")]

Ze sobą można zadeklarować stałe liczbowe o znacznie większej czytelności.

## <a name="out-variables"></a>`out` modyfikacj

Istniejąca składnia, która obsługuje parametry, została `out` ulepszona w języku C# 7. Można teraz zadeklarować `out` zmienne na liście argumentów wywołania metody, zamiast pisać oddzielne oświadczenie deklaracji:

[!code-csharp[OutVariableDeclarations](~/samples/snippets/csharp/new-in-7/program.cs#OutVariableDeclarations "Out variable declarations")]

Możesz chcieć określić typ `out` zmiennej dla przejrzystości, jak pokazano w poprzednim przykładzie. Język obsługuje jednak użycie niejawnie wpisanej zmiennej lokalnej:

[!code-csharp[OutVarVariableDeclarations](~/samples/snippets/csharp/new-in-7/program.cs#OutVarVariableDeclarations "Implicitly typed Out variable")]

- Kod jest łatwiejszy do odczytania.
  - Można zadeklarować zmienną out tam, gdzie jest używana, a nie w poprzednim wierszu kodu.
- Nie trzeba przypisywać wartości początkowej.
  - Deklarując `out` zmienną, w której jest używana w wywołaniu metody, nie można go przypadkowo użyć przed przypisaniem.

Składnia dodana w języku C# 7,0 do zezwalania na `out` deklaracje zmiennych w celu uwzględnienia inicjatorów pól, inicjatorów właściwości, inicjatorów konstruktora i klauzul zapytania. Umożliwia to wykonywanie kodu, takiego jak Poniższy przykład:

```csharp
public class B
{
   public B(int i, out int j)
   {
      j = i;
   }
}

public class D : B
{
   public D(int i) : base(i, out var j)
   {
      Console.WriteLine($"The value of 'j' is {j}");
   }
}
```

## <a name="non-trailing-named-arguments"></a>Argumenty nazwane inne niż końcowe

Wywołania metod mogą teraz używać nazwanych argumentów, które poprzedzają argumenty pozycyjne, gdy te nazwane argumenty znajdują się w poprawnych pozycjach. Aby uzyskać więcej informacji, zobacz [argumenty nazwane i opcjonalne](../programming-guide/classes-and-structs/named-and-optional-arguments.md).

## <a name="private-protected-access-modifier"></a>modyfikator *prywatnego dostępu chronionego*

Nowy modyfikator dostępu złożonego: `private protected` wskazuje, że element członkowski może być dostępny przez zawiera klasy lub klasy pochodne, które są zadeklarowane w tym samym zestawie. `protected internal`Zezwala na dostęp przez klasy pochodne lub klasy, które znajdują się w tym samym zestawie, `private protected` ogranicza dostęp do typów pochodnych zadeklarowanych w tym samym zestawie.

Aby uzyskać więcej informacji, zobacz [Modyfikatory dostępu](../language-reference/keywords/access-modifiers.md) w dokumentacji języka.

## <a name="improved-overload-candidates"></a>Ulepszone kandydujące metody rozwiązywania przeciążenia

W każdej wersji reguły rozpoznawania przeciążenia zostały zaktualizowane w celu rozwiązania sytuacji, w których niejednoznaczne wywołania metod mają oczywisty wybór. W tej wersji dodano trzy nowe reguły, które ułatwiają wybór oczywisty przez kompilator:

1. Gdy grupa metod zawiera zarówno wystąpienie, jak i statyczne elementy członkowskie, kompilator odrzuca elementy członkowskie wystąpienia, jeśli metoda została wywołana bez odbiorcy wystąpienia lub kontekstu. Kompilator odrzuca statyczne elementy członkowskie, jeśli metoda została wywołana z odbiornikiem wystąpienia. Gdy nie ma odbiornika, kompilator zawiera tylko statyczne elementy członkowskie w kontekście statycznym, w przeciwnym razie elementy członkowskie statyczne i wystąpienia. Gdy odbiorca jest niejednoznacznie wystąpieniem lub typem, kompilator zawiera oba te elementy. Statyczny kontekst, w którym niejawny `this` odbiornik wystąpienia nie może być używany, zawiera treść elementów członkowskich, gdzie nie `this` jest zdefiniowana, takich jak statyczne elementy członkowskie, a także miejsca, w których `this` nie można ich używać, takich jak inicjatory pól i konstruktory.
1. Gdy grupa metod zawiera kilka metod ogólnych, których argumenty typu nie spełniają ograniczeń, te elementy członkowskie są usuwane z zestawu kandydatów.
1. Dla konwersji grup metod, metody kandydujące, których typ zwracany nie jest zgodny z typem zwracanym delegata, są usuwane z zestawu.

Ta zmiana zostanie wykorzystana tylko dlatego, że w przypadku niejednoznacznych przeciążeń metod znajdziesz mniej błędów kompilatora, gdy masz pewność, która metoda jest lepsza.

## <a name="enabling-more-efficient-safe-code"></a>Włączanie bardziej wydajnego bezpiecznego kodu

Należy mieć możliwość bezpiecznego pisania kodu w języku C#, który wykonuje, a także kod niebezpieczny. Bezpieczny kod unika klas błędów, takich jak przekroczenia buforu, nieużywane wskaźniki i inne błędy dostępu do pamięci. Te nowe funkcje rozszerzają możliwości zweryfikowania bezpiecznego kodu. Staraj się pisać więcej kodu przy użyciu bezpiecznych konstrukcji. Te funkcje ułatwiają to.

Poniższe nowe funkcje obsługują motyw lepszej wydajności dla bezpiecznego kodu:

- Można uzyskać dostęp do stałych pól bez przypinania.
- Zmienne lokalne można przypisywać ponownie `ref` .
- Inicjatorów można używać w `stackalloc` tablicach.
- Można używać `fixed` instrukcji z dowolnym typem, który obsługuje wzorzec.
- Można użyć dodatkowych ograniczeń ogólnych.
- `in`Modyfikator parametrów, aby określić, że argument jest przesyłany przez odwołanie, ale nie modyfikowane przez wywołaną metodę. Dodanie `in` modyfikatora do argumentu jest [zgodną zmianą źródłową](version-update-considerations.md#source-compatible-changes).
- `ref readonly`Modyfikator metody zwraca, aby wskazać, że metoda zwraca swoją wartość przez odwołanie, ale nie zezwala na zapis w tym obiekcie. Dodanie `ref readonly` modyfikatora jest [zgodną ze źródłem zmian](version-update-considerations.md#source-compatible-changes), jeśli powrót jest przypisany do wartości. Dodanie `readonly` modyfikatora do istniejącej `ref` instrukcji return jest [niezgodną zmianą](version-update-considerations.md#incompatible-changes). Wymaga, aby wywołujący zaktualizował deklarację `ref` zmiennych lokalnych w celu uwzględnienia `readonly` modyfikatora.
- `readonly struct`Deklaracja wskazująca, że struktura jest niezmienna i powinna zostać przeniesiona jako `in` parametr do metod składowych. Dodanie `readonly` modyfikatora do istniejącej deklaracji struktury jest [zgodną binarną zmianą](version-update-considerations.md#binary-compatible-changes).
- `ref struct`Deklaracja wskazująca, że typ struktury bezpośrednio uzyskuje dostęp do pamięci zarządzanej i zawsze musi mieć przydzieloną stos. Dodanie `ref` modyfikatora do istniejącej `struct` deklaracji jest [niezgodną zmianą](version-update-considerations.md#incompatible-changes). Element a `ref struct` nie może być składową klasy ani używać w innych lokalizacjach, w których może być przydzielony na stercie.

Więcej informacji na temat tych zmian można znaleźć w artykule [pisanie bezpiecznego wydajnego kodu](../write-safe-efficient-code.md).

### <a name="ref-locals-and-returns"></a>Ref locales i Returns

Ta funkcja włącza algorytmy, które używają i zwracają odwołania do zmiennych zdefiniowanych w innym miejscu. Jeden przykład pracuje z dużymi macierzami i odnajduje jedną lokalizację z określonymi cechami. Poniższa metoda zwraca **odwołanie** do tego magazynu w macierzy:

[!code-csharp[FindReturningRef](~/samples/snippets/csharp/new-in-7/MatrixSearch.cs#FindReturningRef "Find returning by reference")]

Można zadeklarować wartość zwracaną jako `ref` i zmodyfikować tę wartość w macierzy, jak pokazano w poniższym kodzie:

[!code-csharp[AssignRefReturn](~/samples/snippets/csharp/new-in-7/Program.cs#AssignRefReturn "Assign ref return")]

Język C# ma kilka reguł, które chronią przed niepożądanym użyciem `ref` zmiennych lokalnych i zwraca:

- Należy dodać `ref` słowo kluczowe do sygnatury metody i do wszystkich `return` instrukcji w metodzie.
  - Dzięki temu czyszczenie metody następuje przez odwołanie w całej metodzie.
- A `ref return` może być przypisana do zmiennej wartości lub `ref` zmiennej.
  - Obiekt wywołujący kontroluje, czy wartość zwracana jest kopiowana, czy nie. Pominięcie `ref` modyfikatora podczas przypisywania wartości zwracanej wskazuje, że obiekt wywołujący chce mieć kopię wartości, a nie odwołanie do magazynu.
- Nie można przypisać wartości zwracanej metody standardowej do `ref` zmiennej lokalnej.
  - Nie zezwala na instrukcje, takie jak `ref int i = sequence.Count();`
- Nie można zwrócić `ref` do zmiennej, której okres istnienia nie przekracza wykonywania metody.
  - Oznacza to, że nie można zwrócić odwołania do zmiennej lokalnej lub zmiennej o podobnym zakresie.
- `ref` elementy locale i Returns nie mogą być używane z metodami asynchronicznymi.
  - Kompilator nie może wiedzieć, czy przywoływana zmienna została ustawiona na jej końcową wartość, gdy Metoda asynchroniczna zwraca.

Dodanie elementów lokalnych ref i Return ref umożliwia stosowanie algorytmów, które są bardziej wydajne przez uniknięcie kopiowania wartości lub wielokrotne wykonywanie operacji usuwania odwołań.

Dodanie `ref` do wartości zwracanej jest [zmianą zgodną ze źródłem](version-update-considerations.md#source-compatible-changes). Istniejący kod kompiluje, ale zwracana wartość Ref jest kopiowana po przypisaniu. Obiekty wywołujące muszą zaktualizować magazyn dla wartości zwracanej do `ref` zmiennej lokalnej, aby można było przechowywać zwrot jako odwołanie.

Teraz elementy `ref` lokalne mogą zostać ponownie przypisane, aby odwoływać się do różnych wystąpień po zainicjowaniu. Poniższy kod jest teraz kompilowany:

```csharp
ref VeryLargeStruct refLocal = ref veryLargeStruct; // initialization
refLocal = ref anotherVeryLargeStruct; // reassigned, refLocal refers to different storage.
```

Aby uzyskać więcej informacji, zobacz artykuł dotyczący [ `ref` zwrotów i elementów `ref` lokalnych](../programming-guide/classes-and-structs/ref-returns.md)oraz artykuł w artykule [`foreach`](../language-reference/keywords/foreach-in.md) .

Aby uzyskać więcej informacji, zobacz artykuł [słowo kluczowe ref](../language-reference/keywords/ref.md) .

### <a name="conditional-ref-expressions"></a>Wyrażenia warunkowe `ref`

Na koniec wyrażenie warunkowe może generować wynik ref zamiast wyniku wartości. Na przykład Napisz następujące polecenie, aby pobrać odwołanie do pierwszego elementu w jednej z dwóch tablic:

```csharp
ref var r = ref (arr != null ? ref arr[0] : ref otherArr[0]);
```

Zmienna `r` jest odwołaniem do pierwszej wartości z `arr` lub `otherArr` .

Aby uzyskać więcej informacji, zobacz [operator warunkowy (?:)](../language-reference/operators/conditional-operator.md) w dokumentacji języka.

### <a name="in-parameter-modifier"></a>`in` modyfikator parametru

`in`Słowo kluczowe uzupełnia istniejące słowa kluczowe ref i out do przekazywania argumentów przez odwołanie. `in`Słowo kluczowe Określa przekazywanie argumentu przez odwołanie, ale wywołana metoda nie modyfikuje wartości.

Można zadeklarować przeciążenia, które przechodzą przez wartość lub przez odwołanie tylko do odczytu, jak pokazano w poniższym kodzie:

```csharp
static void M(S arg);
static void M(in S arg);
```

Wartość przez (najpierw w poprzednim przykładzie) przeciążenie jest lepsza niż wersja odwołania do tylko do odczytu. Aby wywołać wersję z argumentem odwołania tylko do odczytu, należy dołączyć `in` modyfikator podczas wywoływania metody.

Aby uzyskać więcej informacji, zobacz artykuł dotyczący [ `in` modyfikatora parametru](../language-reference/keywords/in-parameter-modifier.md).

### <a name="more-types-support-the-fixed-statement"></a>Więcej typów obsługuje `fixed` instrukcja

`fixed`Instrukcja obsługuje ograniczony zestaw typów. Począwszy od języka C# 7,3, dowolnego typu, który zawiera `GetPinnableReference()` metodę zwracającą `ref T` lub `ref readonly T` może być `fixed` . Dodanie tej funkcji oznacza, że `fixed` mogą być używane z <xref:System.Span%601?displayProperty=nameWithType> i powiązane typy.

Aby uzyskać więcej informacji, zobacz artykuł [ `fixed` instrukcji](../language-reference/keywords/fixed-statement.md) w dokumentacji języka.

### <a name="indexing-fixed-fields-does-not-require-pinning"></a>Pola indeksowania nie `fixed` wymagają przypinania

Rozważmy tę strukturę:

```csharp
unsafe struct S
{
    public fixed int myFixedField[10];
}
```

We wcześniejszych wersjach języka C# wymagało przypinania zmiennej w celu uzyskania dostępu do jednej z liczb całkowitych, które są częścią `myFixedField` . Teraz Poniższy kod kompiluje bez przypinania zmiennej `p` wewnątrz oddzielnej `fixed` instrukcji:

```csharp
class C
{
    static S s = new S();

    unsafe public void M()
    {
        int p = s.myFixedField[5];
    }
}
```

Zmienna `p` uzyskuje dostęp do jednego elementu w `myFixedField` . Nie musisz deklarować odrębnej `int*` zmiennej. Nadal potrzebujesz `unsafe` kontekstu. We wcześniejszych wersjach języka C# należy zadeklarować drugi stały wskaźnik:

```csharp
class C
{
    static S s = new S();

    unsafe public void M()
    {
        fixed (int* ptr = s.myFixedField)
        {
            int p = ptr[5];
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz artykuł na temat [ `fixed` instrukcji](../language-reference/keywords/fixed-statement.md).

### <a name="stackalloc-arrays-support-initializers"></a>`stackalloc` Tablice obsługują inicjatory

Po zainicjowaniu można określić wartości dla elementów w tablicy:

```csharp
var arr = new int[3] {1, 2, 3};
var arr2 = new int[] {1, 2, 3};
```

Teraz tę samą składnię można zastosować do tablic, które są zadeklarowane za pomocą `stackalloc` :

```csharp
int* pArr = stackalloc int[3] {1, 2, 3};
int* pArr2 = stackalloc int[] {1, 2, 3};
Span<int> arr = stackalloc [] {1, 2, 3};
```

Aby uzyskać więcej informacji, zobacz artykuł dotyczący [ `stackalloc` operatorów](../language-reference/operators/stackalloc.md) .

### <a name="enhanced-generic-constraints"></a>Ulepszone ograniczenia ogólne

Teraz można określić typ <xref:System.Enum?displayProperty=nameWithType> lub <xref:System.Delegate?displayProperty=nameWithType> jako ograniczenia klasy bazowej dla parametru typu.

Można również użyć nowego `unmanaged` ograniczenia, aby określić, że parametr typu musi być [typem niezarządzanym](../language-reference/builtin-types/unmanaged-types.md)null.

Aby uzyskać więcej informacji, zobacz artykuły dotyczące [ `where` ograniczeń ogólnych](../language-reference/keywords/where-generic-type-constraint.md) i [ograniczeń dla parametrów typu](../programming-guide/generics/constraints-on-type-parameters.md).

Dodanie tych ograniczeń do istniejących typów jest [niezgodną zmianą](version-update-considerations.md#incompatible-changes). Zamknięte typy ogólne nie mogą już odpowiadać tym nowym ograniczeniom.

### <a name="generalized-async-return-types"></a>Uogólnione asynchroniczne typy zwracane

Zwrócenie `Task` obiektu z metod asynchronicznych może spowodować wąskie gardła wydajności w określonych ścieżkach. `Task` to typ referencyjny, dlatego użycie go oznacza przydzielenie obiektu. W przypadkach, gdy metoda zadeklarowana za pomocą `async` modyfikatora zwraca zbuforowany wynik lub wykonuje synchronicznie, dodatkowe alokacje mogą stać się ważnym kosztem w przypadku krytycznych sekcji kodu. Może być kosztowna, jeśli te przydziały występują w ścisłych pętlach.

Nowa funkcja języka oznacza, że zwracane typy metod asynchronicznych nie są ograniczone do `Task` , `Task<T>` , i `void` . Zwracany typ musi nadal spełniać wzorzec asynchroniczny, co oznacza, że `GetAwaiter` Metoda musi być dostępna. Jak określono w konkretnym przykładzie, `ValueTask` Typ został dodany do platformy .NET, aby można było korzystać z tej nowej funkcji języka:

[!code-csharp[UsingValueTask](~/samples/snippets/csharp/new-in-7/AsyncWork.cs#UsingValueTask "Using ValueTask")]

> [!NOTE]
> Należy dodać pakiet NuGet [`System.Threading.Tasks.Extensions`](https://www.nuget.org/packages/System.Threading.Tasks.Extensions/) >, aby można było użyć <xref:System.Threading.Tasks.ValueTask%601> typu.

To ulepszenie jest najbardziej przydatne w przypadku autorów bibliotek, aby uniknąć alokowania `Task` w kodzie krytycznym wydajności.

## <a name="new-compiler-options"></a>Nowe opcje kompilatora

Nowe opcje kompilatora obsługują nowe scenariusze kompilacji i DevOps dla programów w języku C#.

### <a name="reference-assembly-generation"></a>Generowanie zestawu odwołań

Istnieją dwie nowe opcje kompilatora, które generują *zestawy tylko do odwołania*: [-opcji refout](../language-reference/compiler-options/refout-compiler-option.md) i [-refonly](../language-reference/compiler-options/refonly-compiler-option.md).
Połączone artykuły wyjaśniają te opcje i zestawy referencyjne bardziej szczegółowo.

### <a name="public-or-open-source-signing"></a>Podpisywanie publiczne lub Open Source

`-publicsign`Opcja kompilatora instruuje kompilator do podpisania zestawu przy użyciu klucza publicznego. Zestaw jest oznaczony jako podpisany, ale podpis jest pobierany z klucza publicznego. Ta opcja umożliwia tworzenie podpisanych zestawów z projektów typu "open source" przy użyciu klucza publicznego.

Aby uzyskać więcej informacji, zobacz [publicsign opcji kompilatora](../language-reference/compiler-options/publicsign-compiler-option.md) .

### <a name="pathmap"></a>elemencie pathmap

`-pathmap`Opcja kompilatora instruuje kompilator, aby zamieniać ścieżki źródłowe ze środowiska kompilacji z zamapowanymi ścieżkami źródłowymi. `-pathmap`Opcja steruje ścieżką źródłową zapisaną przez kompilator do plików PDB lub dla <xref:System.Runtime.CompilerServices.CallerFilePathAttribute> .

Aby uzyskać więcej informacji, zobacz [elemencie pathmap opcji kompilatora](../language-reference/compiler-options/pathmap-compiler-option.md) .
