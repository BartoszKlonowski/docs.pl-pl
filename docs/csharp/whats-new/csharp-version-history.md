---
title: Historia języka C# — Przewodnik c#
description: Jak wygląda ten język we wcześniejszych wersjach i jak został on rozwijający od?
author: erikdietrich
ms.date: 04/08/2020
ms.openlocfilehash: 7258dc8b8fcfbd6354b5ceee4183429bfee14038
ms.sourcegitcommit: 9b877e160c326577e8aa5ead22a937110d80fa44
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2020
ms.locfileid: "97110731"
---
# <a name="the-history-of-c"></a>Historia języka C\#

Ten artykuł zawiera historię poszczególnych głównych wersji języka C#. Zespół C# kontynuuje wprowadzanie innowacji i dodawanie nowych funkcji. Szczegółowy stan funkcji języka, w tym funkcje uwzględniane w przypadku przyszłych wersji, można znaleźć [w repozytorium dotnet/Roslyn](https://github.com/dotnet/roslyn/blob/master/docs/Language%20Feature%20Status.md) w witrynie GitHub.

> [!IMPORTANT]
> Język C# opiera się na typach i metodach, które Specyfikacja języka C# definiuje jako *bibliotekę standardową* dla niektórych funkcji. Platforma .NET dostarcza te typy i metody w wielu pakietach. Przykładem jest przetwarzanie wyjątków. Każda `throw` instrukcja lub wyrażenie jest zaznaczone, aby upewnić się, że zgłaszany obiekt jest pochodną <xref:System.Exception> . Podobnie każde `catch` jest sprawdzane w celu upewnienia się, że typ, który jest przechwytywany, pochodzi od <xref:System.Exception> . Każda wersja może dodawać nowe wymagania. Aby korzystać z najnowszych funkcji języka w starszych środowiskach, może być konieczne zainstalowanie określonych bibliotek. Te zależności są udokumentowane na stronie dla każdej konkretnej wersji. Aby uzyskać więcej informacji na temat [relacji między językiem i biblioteką](relationships-between-language-and-library.md) w tle, należy zapoznać się z tematem dotyczącym tej zależności.

Narzędzia kompilacji w języku C# uwzględniają najnowszą wersję językową domyślnej wersji językowej. Między wersjami głównymi mogą występować wersje punktów, które opisano w innych artykułach w tej sekcji. Aby użyć najnowszych funkcji w wersji próbnej, należy [skonfigurować wersję języka kompilatora](../language-reference/configure-language-version.md) i wybrać wersję. Istnieją trzy punkty wersji od języka C# 7,0:

- C# 7,3:
  - Język C# 7,3 jest dostępny w programie [Visual Studio 2017 w wersji 15,7](https://visualstudio.microsoft.com/vs/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link) i [.NET Core 2,1 SDK](../../core/whats-new/dotnet-core-2-1.md).
- C# 7,2:
  - Język C# 7,2 jest dostępny w programie [Visual Studio 2017 w wersji 15,5](https://visualstudio.microsoft.com/vs/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link) i [.NET Core 2,0 SDK](../../core/whats-new/dotnet-core-2-0.md).
- C# 7,1:
  - Język C# 7,1 jest dostępny w programie [Visual Studio 2017 w wersji 15,3](https://visualstudio.microsoft.com/vs/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link) i [.NET Core 2,0 SDK](../../core/whats-new/dotnet-core-2-0.md).

## <a name="c-version-10"></a>C#, wersja 1,0

Po przejściu do tyłu i wyglądu w języku C# wersja 1,0 wydanej w programie Visual Studio .NET 2002 sprawdzono wiele takich elementów jak Java. Zgodnie [z ustalonymi celami projektu dla języka ECMA](https://feeldotneteasy.blogspot.com/2011/01/c-design-goals.html), powinien to być "prosty, nowoczesny, zorientowany na obiekty ogólnego przeznaczenia".  W tym czasie wygląda na to, że środowisko Java osiągnęło te wczesne cele projektowania.

Ale jeśli teraz powrócisz do języka C# 1,0, znajdziesz nieco Dizzy. Brakuje wbudowanych funkcji asynchronicznych i niektórych funkcji sprawny wokół typów ogólnych, które należy podjąć. Z tego względu nie wszystkie ogólne.  I [LINQ](../linq/index.md)? Jeszcze niedostępne. Te dodatki będą trwać kilka lat.

W języku C# w wersji 1,0 wywyglądało funkcje, w porównaniu do dzisiaj. Znajdziesz kod pełny. Jednak musisz zacząć korzystać z dowolnego miejsca. Język C# w wersji 1,0 był żywotną alternatywą dla języka Java na platformie Windows.

Główne funkcje języka C# 1,0:

- [Klasy](../programming-guide/classes-and-structs/classes.md)
- [Struktury](../language-reference/builtin-types/struct.md)
- [Interfejsy](../programming-guide/interfaces/index.md)
- [Zdarzenia](../events-overview.md)
- [Właściwości](../properties.md)
- [Delegaci](../delegates-overview.md)
- [Operatory i wyrażenia](../language-reference/operators/index.md)
- [Instrukcje](../programming-guide/statements-expressions-operators/statements.md)
- [Atrybuty](../programming-guide/concepts/attributes/index.md)

## <a name="c-version-12"></a>C#, wersja 1,2

C# w wersji 1,2 dostarczonej z programem Visual Studio .NET 2003. Zawiera kilka małych ulepszeń w języku. Najbardziej istotny jest to, że począwszy od tej wersji, kod wygenerowany w `foreach` pętli wywoływana <xref:System.IDisposable.Dispose%2A> w <xref:System.Collections.IEnumerator> przypadku, gdy jest <xref:System.Collections.IEnumerator> zaimplementowany <xref:System.IDisposable> .

## <a name="c-version-20"></a>C#, wersja 2,0

Teraz można zacząć korzystać z interesujących rzeczy. Przyjrzyjmy się najważniejszym funkcjom języka C# 2,0, które zostały wydane w 2005, wraz z programem Visual Studio 2005:

- [Typy ogólne](../programming-guide/generics/index.md)
- [Typy częściowe](../programming-guide/classes-and-structs/partial-classes-and-methods.md#partial-classes)
- [Metody anonimowe](../language-reference/operators/delegate-operator.md)
- [Typy wartości dopuszczające wartość null](../language-reference/builtin-types/nullable-value-types.md)
- [Iteratory](../programming-guide/concepts/iterators.md)
- [Kowariancja i kontrawariancja](../programming-guide/concepts/covariance-contravariance/index.md)

Inne funkcje języka C# 2,0 dodaliśmy możliwości do istniejących funkcji:

- Metoda pobierająca/setter oddzielna dostępność
- Konwersje grup metod (delegatów)
- Klasy statyczne
- Delegowanie wnioskowania

Podczas gdy język C# mógł rozpocząć pracę jako generyczny Object-Oriented (OO), w języku C# wersja 2,0 zmieniła się w pospiesz. Gdy miały swoje stopy w nich, zakończyły się po kilku poważnych punktach bólu deweloperów. I zostały one w znaczący sposób.

W przypadku typów ogólnych typy i metody mogą działać na dowolnym typie przy zachowaniu bezpieczeństwa typu. Na przykład, jeśli istnieje, <xref:System.Collections.Generic.List%601> a umożliwia `List<string>` `List<int>` wykonywanie operacji bezpiecznych typu na tych ciągach lub liczbach całkowitych w trakcie iteracji. Używanie typów ogólnych jest lepszym rozwiązaniem niż tworzenie `ListInt` , które wynika z `ArrayList`  lub rzutowanie z `Object` dla każdej operacji.

W języku C# w wersji 2,0 zostały wprowadzone Iteratory. Aby umieścić je w sposób zwięzły, Iteratory umożliwiają badanie wszystkich elementów w `List` (lub innych wyliczalnych typach) za pomocą `foreach` pętli. Posiadanie iteratorów jako pierwszej klasy języka znacznie zwiększa czytelność języka i zdolności osób do uzyskania informacji o kodzie.

A jeszcze w języku C# pozostała potrzeba odtworzenia nieprzerwanego przechwytywania w języku Java. Java wydano już wersje, które zawierały typy ogólne i Iteratory. Ale to wkrótce zmieni się, ponieważ Języki będą nadal rozliczane od siebie.

## <a name="c-version-30"></a>C#, wersja 3,0

Język C# w wersji 3,0 znajduje się w późnej 2007, wraz z programem Visual Studio 2008, chociaż pełna łódź funkcji języka rzeczywiście będzie miała .NET Framework wersja 3,5. Ta wersja oznacza istotną zmianę w zakresie wzrostu języka C#. Język C# został ustalony jako prawdziwie Formidable programowanie. Spójrzmy na kilka najważniejszych funkcji w tej wersji:

- [Właściwości zaimplementowane wstępnie](../programming-guide/classes-and-structs/auto-implemented-properties.md)
- [Typy anonimowe](../programming-guide/classes-and-structs/anonymous-types.md)
- [Wyrażenia zapytań](../linq/query-expression-basics.md)
- [Wyrażenia lambda](../language-reference/operators/lambda-expressions.md)
- [Drzewa wyrażeń](../expression-trees.md)
- [Metody rozszerzające](../programming-guide/classes-and-structs/extension-methods.md)
- [Niejawnie wpisane zmienne lokalne](../language-reference/keywords/var.md)
- [Metody częściowe](../language-reference/keywords/partial-method.md)
- [Inicjatory obiektów i kolekcji](../programming-guide/classes-and-structs/object-and-collection-initializers.md)

W programie Spoglądając wstecz wiele z tych funkcji sprawia, że są one nieuniknione i nierozdzielne. Wszystkie te same pasują do siebie strategicznie. Ogólnie uważa się, że funkcja Killer wersji C# była wyrażeniem zapytania, znanym również jako zapytanie Language-Integrated (LINQ).

Dokładniejszy widok złożonych bada drzewa wyrażeń, wyrażenia lambda i typy anonimowe jako podstawę, na której jest konstruowany składnik LINQ. Jednak w obu przypadkach w języku C# 3,0 przedstawiono koncepcję Rewolucyjne. W języku c# 3,0 rozpoczęto tworzenie podstawę w celu przetworzenia języka C# w hybrydowej Object-Oriented/języku funkcjonalnym.

W tym celu można teraz napisać w stylu SQL zapytania deklaracyjne, aby wykonywać operacje na kolekcjach, między innymi. Zamiast pisać `for` pętlę, aby obliczyć średnią z listy liczb całkowitych, można to zrobić tak samo jak w przypadku `list.Average()` . Kombinacja wyrażeń zapytania i metod rozszerzających wygląda tak, jakby ta lista liczb całkowitych uzyskała całą dużą liczbę.

Zajęło ci dużo czasu na opanujesz i integrację koncepcji, ale stopniowo. A teraz lata później, kod jest znacznie bardziej zwięzły, prosty i funkcjonalny.

## <a name="c-version-40"></a>C#, wersja 4,0

W języku C# w wersji 4,0 wydanej w programie Visual Studio 2010 wystąpił trudny czas utrzymania stanu przełomowe w wersji 3,0. W wersji 3,0, C# przeniósł język od w tle środowiska Java i do wyeksponowanie. Język mógł szybko stać się elegancki.

Następna wersja wprowadziła interesujące nowe funkcje:

- [Wiązanie dynamiczne](../language-reference/builtin-types/reference-types.md)
- [Argumenty nazwane/opcjonalne](../programming-guide/classes-and-structs/named-and-optional-arguments.md)
- [Ogólna współvariant i kontrawariantne](../../standard/generics/covariance-and-contravariance.md)
- [Osadzone typy międzyoperacyjnych](../../framework/interop/type-equivalence-and-embedded-interop-types.md)

Wbudowane typy międzyoperacyjności zmniejszają możliwości wdrożenia. Ogólna Kowariancja i kontrawariancja zapewniają większą moc do korzystania z typów ogólnych, ale są one nieco akademickie i prawdopodobnie najbardziej doceniane przez autorów struktury i biblioteki. Parametry nazwane i opcjonalne pozwalają wyeliminować wiele przeciążeń metod i zapewnić wygodę. Jednak żadna z tych funkcji nie ma dokładnej zmiany modelu.

Funkcja główna była wprowadzeniem `dynamic` słowa kluczowego. `dynamic`Słowo kluczowe wprowadzone do języka C# w wersji 4,0 możliwość zastąpienia kompilatora podczas pisania w czasie kompilacji. Za pomocą słowa kluczowego Dynamic można tworzyć konstrukcje podobne do dynamicznie wpisanych języków, takich jak JavaScript. Możesz utworzyć `dynamic x = "a string"` a następnie dodać do niej sześć, pozostawiając ją w środowisku uruchomieniowym, aby określić, co powinno się stać dalej.

Dynamiczne powiązanie zapewnia potencjalne błędy, ale również doskonale moc w języku.

## <a name="c-version-50"></a>C#, wersja 5,0

Język C# w wersji 5,0 wydanej w programie Visual Studio 2012 był skoncentrowaną wersją języka. Niemal cały nakład pracy związany z tą wersją osiągnął inną koncepcję języka przełomowe: `async` `await` model i programowanie asynchroniczne.  Oto lista głównych funkcji:

- [Asynchroniczne elementy członkowskie](../async.md)
- [Atrybuty informacji o wywołującym](../language-reference/attributes/caller-information.md)

### <a name="see-also"></a>Zobacz też

- [Projekt kodu: atrybuty informacji o obiekcie wywołującym w języku C# 5,0](https://www.codeproject.com/Tips/606379/Caller-Info-Attributes-in-Csharp)

Atrybut informacje o wywołującym pozwala łatwo pobrać informacje dotyczące kontekstu, w którym jest wykonywane, bez konieczności przeliczania się na tonę standardowego kodu odbicia. Ma wiele użycia w zadaniach diagnostycznych i dzienników.

Ale `async` i `await` są rzeczywiste gwiazdki tej wersji. Gdy te funkcje zostały dostarczone w 2012, w języku C# zmieniono grę ponownie przez asynchroniczności jako uczestnika pierwszej klasy. Jeśli kiedykolwiek zdarzyło Ci się zająć długotrwałymi operacjami i implementacją sieci Web wywołania zwrotnego, prawdopodobnie uwielbiane tej funkcji językowej.

## <a name="c-version-60"></a>C#, wersja 6,0

W wersjach 3,0 i 5,0 język C# dodał nowe funkcje w języku zorientowanym obiektowo. W wersji 6,0 wydanej w programie Visual Studio 2015 nie można przeprowadzić dominującej funkcji Killer i zamiast tego wydać wiele mniejszych funkcji, które zwiększają produktywność programowania w języku C#. Oto niektóre z nich:

- [Importy statyczne](../language-reference/keywords/using-static.md)
- [Filtry wyjątków](../language-reference/keywords/when.md)
- [Inicjatory właściwości autoproperty](../properties.md)
- [Wyrażenie składowych składowanych](../language-reference/operators/lambda-operator.md#expression-body-definition)
- [Propagator o wartości null](../language-reference/operators/member-access-operators.md#null-conditional-operators--and-)
- [Interpolacja ciągów](../language-reference/tokens/interpolated.md)
- [operator nameof](../language-reference/operators/nameof.md)

Inne nowe funkcje obejmują:

- Inicjatory indeksów
- Await w blokach catch/finally
- Wartości domyślne właściwości metody pobierającej

Każda z tych funkcji jest interesująca po prawej stronie. Ale jeśli zobaczysz je całkowicie, zobaczysz interesujący wzór. W tej wersji język C# nie eliminuje języka standardowego, aby kod był bardziej zwięzła i możliwy do odczytania. Tak więc dla wentylatorów czysty, prosty kod, ta wersja językowa była ogromnym wygraniem.

Te osoby były jednym innym elementem wraz z tą wersją, chociaż nie jest tradycyjną funkcją języka. Zostały one wydane [Roslyn kompilator jako usługi](https://github.com/dotnet/roslyn). Kompilator języka C# jest teraz pisany w języku C# i można użyć kompilatora w ramach wysiłków programistycznych.

## <a name="c-version-70"></a>C#, wersja 7,0

Język C# w wersji 7,0 został opublikowany z Visual Studio 2017. Ta wersja ma pewne ewolucje i chłodnie w przerostach języka C# 6,0, ale bez kompilatora jako usługi. Oto niektóre z nowych funkcji:

- [Zmienne out](./csharp-7.md#out-variables)
- [Krotki i dekonstrukcja](./csharp-7.md#tuples-and-discards)
- [Dopasowanie do wzorca](./csharp-7.md#pattern-matching)
- [Funkcje lokalne](./csharp-7.md#local-functions)
- [Rozwinięte składowe wyrażeń](./csharp-7.md#more-expression-bodied-members)
- [Ref locales i Returns](./csharp-7.md#ref-locals-and-returns)

Dostępne są inne funkcje:

- [Odrzucenia](./csharp-7.md#tuples-and-discards)
- [Literały binarne i separatory cyfr](./csharp-7.md#numeric-literal-syntax-improvements)
- [Wyrażenia throw](./csharp-7.md#throw-expressions)

Wszystkie te funkcje oferują chłodne nowe możliwości dla deweloperów i możliwość pisania jeszcze bardziej estetycznego kodu. Podświetlanie zbliża się do deklaracji zmiennych, które mają być używane ze `out` słowem kluczowym, i zezwalając na wiele wartości zwracanych za pośrednictwem krotki.

Ale język C# jest wprowadzany do coraz szerszego użycia. Platforma .NET Core jest teraz przeznaczona dla dowolnego systemu operacyjnego i ma swoje oczy w chmurze i na przenośności.  Te nowe funkcje mają na celu zajmowanie pomysłów i czasu projektanta języka, a także nowe funkcje.

## <a name="c-version-71"></a>C#, wersja 7,1

W języku c# rozpoczęto zwalnianie *wydań punktów* w języku c# 7,1. Ta wersja dodała element konfiguracji [wyboru wersji języka](../language-reference/configure-language-version.md) , trzy nowe funkcje językowe oraz nowe zachowanie kompilatora.

Nowe funkcje języka w tej wersji są następujące:

- [`async``Main`Metoda](./csharp-7.md#async-main)
  - Punkt wejścia dla aplikacji może mieć `async` modyfikator.
- [`default` wyrażenia literału](./csharp-7.md#default-literal-expressions)
  - Można użyć domyślnych wyrażeń literałów w wyrażeniach wartości domyślnych, gdy można wywnioskować typ docelowy.
- [Wywnioskowane nazwy elementów krotki](./csharp-7.md#tuples-and-discards)
  - Nazwy elementów krotki można wywnioskować na podstawie inicjalizacji krotki w wielu przypadkach.
- [Dopasowanie wzorca dla parametrów typu ogólnego](./csharp-7.md#pattern-matching)
  - Wyrażeń dopasowania wzorców można używać w zmiennych, których typem jest parametr typu ogólnego.

Na koniec kompilator ma dwie opcje `-refout` i `-refonly` umożliwia [wygenerowanie zestawu odwołań](./csharp-7.md#reference-assembly-generation).

## <a name="c-version-72"></a>C#, wersja 7,2

W języku C# 7,2 dodano kilka małych funkcji języka:

- [Techniki pisania bezpiecznego wydajnego kodu](./csharp-7.md#enabling-more-efficient-safe-code)
  - Kombinacja ulepszeń składni, które umożliwiają pracę z typami wartości przy użyciu semantyki referencyjnej.
- [Argumenty nazwane inne niż końcowe](./csharp-7.md#non-trailing-named-arguments)
  - Po nazwanych argumentach mogą występować argumenty pozycyjne.
- [Wiodące znaki podkreślenia w literałach numerycznych](./csharp-7.md#numeric-literal-syntax-improvements)
  - Literały numeryczne mogą teraz zawierać podkreślenia wiodące przed wszelkimi drukowanymi cyframi.
- [`private protected` Modyfikator dostępu](./csharp-7.md#private-protected-access-modifier)
  - `private protected`Modyfikator dostępu umożliwia dostęp do klas pochodnych w tym samym zestawie.
- [Wyrażenia warunkowe `ref`](./csharp-7.md#conditional-ref-expressions)
  - Wynik wyrażenia warunkowego ( `?:` ) może teraz być odwołaniem.

## <a name="c-version-73"></a>C#, wersja 7,3

Istnieją dwa główne motywy w wersji C# 7,3. Jeden motyw udostępnia funkcje, które umożliwiają bezpieczny kod, tak jak kod niebezpieczny. Drugi motyw zawiera ulepszenia przyrostowe istniejących funkcji. Ponadto w tej wersji dodano nowe opcje kompilatora.

Poniższe nowe funkcje obsługują motyw lepszej wydajności dla bezpiecznego kodu:

- [Można uzyskać dostęp do stałych pól bez przypinania.](csharp-7.md#indexing-fixed-fields-does-not-require-pinning)
- [Zmienne lokalne można przypisywać ponownie `ref` .](csharp-7.md#enabling-more-efficient-safe-code)
- [Inicjatorów można używać w `stackalloc` tablicach.](csharp-7.md#stackalloc-arrays-support-initializers)
- [Można używać `fixed` instrukcji z dowolnym typem, który obsługuje wzorzec.](csharp-7.md#more-types-support-the-fixed-statement)
- [Można użyć dodatkowych ograniczeń ogólnych.](csharp-7.md#enhanced-generic-constraints)

W istniejących funkcjach wprowadzono następujące ulepszenia:

- Można testować `==` i `!=` z typami krotek.
- Zmiennych wyrażeń można używać w większej liczbie lokalizacji.
- Możesz dołączyć atrybuty do pola zapasowego właściwości, które są implementowane automatycznie.
- Ulepszono metodę rozdzielczości, gdy argumenty różnią się od `in` .
- Rozwiązanie przeciążenia ma teraz mniej niejednoznaczne przypadki.

Nowe opcje kompilatora są następujące:

- `-publicsign` Aby włączyć podpisywanie zestawów przez oprogramowanie typu Open Source (OSS).
- `-pathmap` w celu zapewnienia mapowania dla katalogów źródłowych.

## <a name="c-version-80"></a>C#, wersja 8,0

C# 8,0 to pierwsza główna wersja języka C#, która jest przeznaczona dla platformy .NET Core. Niektóre funkcje są zależne od nowych możliwości środowiska CLR, inne w przypadku typów bibliotek dodanych tylko w programie .NET Core. W języku c# 8,0 dodano następujące funkcje i ulepszenia języka C#:

- [Elementy członkowskie tylko do odczytu](./csharp-8.md#readonly-members)
- [Domyślne metody interfejsu](./csharp-8.md#default-interface-methods)
- [Ulepszenia dopasowania wzorców](./csharp-8.md#more-patterns-in-more-places):
  - [Przełącz wyrażenia](./csharp-8.md#switch-expressions)
  - [Wzorce właściwości](./csharp-8.md#property-patterns)
  - [Wzorce krotek](./csharp-8.md#tuple-patterns)
  - [Wzorce pozycyjne](./csharp-8.md#positional-patterns)
- [Korzystanie z deklaracji](./csharp-8.md#using-declarations)
- [Statyczne funkcje lokalne](./csharp-8.md#static-local-functions)
- [Nierozporządzalne struktury ref](./csharp-8.md#disposable-ref-structs)
- [Typy referencyjne dopuszczające wartość null](../language-reference/builtin-types/nullable-reference-types.md)
- [Strumienie asynchroniczne](./csharp-8.md#asynchronous-streams)
- [Indeksy i zakresy](./csharp-8.md#indices-and-ranges)
- [Przypisanie do łączenia o wartości null](./csharp-8.md#null-coalescing-assignment)
- [Niezarządzane typy skonstruowane](./csharp-8.md#unmanaged-constructed-types)
- [Stackalloc w wyrażeniach zagnieżdżonych](./csharp-8.md#stackalloc-in-nested-expressions)
- [Ulepszenie interpolowanych ciągów Verbatim](./csharp-8.md#enhancement-of-interpolated-verbatim-strings)

Domyślne elementy członkowskie interfejsu wymagają ulepszeń w środowisku CLR. Te funkcje zostały dodane w środowisku CLR dla platformy .NET Core 3,0. Zakresy i indeksy oraz strumienie asynchroniczne wymagają nowych typów w bibliotekach programu .NET Core 3,0. Typy referencyjne dopuszczające wartość null, ale zaimplementowane w kompilatorze, są znacznie bardziej przydatne, gdy biblioteki są opatrzone adnotacjami, aby zapewnić informacje semantyczne dotyczące stanu null argumentów i zwracanych wartości. Adnotacje są dodawane w bibliotekach programu .NET Core.

_Artykuł_ [_pierwotnie opublikowany w blogu NDepend_](https://blog.ndepend.com/c-versions-look-language-history/)_, grzecznościowa Erik Dietrich i Patryk Smacchia._
