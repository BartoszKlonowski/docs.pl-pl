---
title: Odwołanie do słowa kluczowego
description: 'Znajdź linki do informacji o wszystkich słowach kluczowych języka F #.'
f1_keywords:
- new_FS
- use_FS
- end_FS
- lsl_FS
- exception_FS
- asr_FS
- if_FS
- internal_FS
- default_FS
- in_FS
- lsr_FS
- open_FS
- static_FS
- assert_FS
- match_FS
- land_FS
- with_FS
- inherit_FS
- mutable_FS
- downto_FS
- false_FS
- sig_FS
- and_FS
- true_FS
- namespace_FS
- public_FS
- lxor_FS
- val_FS
- void_FS
- downcast_FS
- function_FS
- while_FS
- for_FS
- class_FS
- done_FS
- to_FS
- module_FS
- let_FS
- delegate_FS
- abstract_FS
- then_FS
- when_FS
- lazy_FS
- try_FS
- inline_FS
- do_FS
- upcast_FS
- begin_FS
- base_FS
- fun_FS
- struct_FS
- as_FS
- extern_FS
- null_FS
- lor_FS
- return_FS
- mod_FS
- private_FS
- of_FS
- or_FS
- member_FS
- type_FS
- rec_FS
- elif_FS
- override_FS
- interface_FS
- yield_FS
- else_FS
- finally_FS
- global_FS
- select_FS
- use!_FS
- const_FS
dev_langs:
- FSharp
ms.date: 08/15/2020
ms.openlocfilehash: 15505c123dd0d6497fbc80c8fc9f0910018911ea
ms.sourcegitcommit: 8bfeb5930ca48b2ee6053f16082dcaf24d46d221
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2020
ms.locfileid: "88558104"
---
# <a name="keyword-reference"></a>Odwołanie do słowa kluczowego

Ten temat zawiera linki do informacji o wszystkich słowach kluczowych języka F #.

## <a name="f-keyword-table"></a>Tabela słów kluczowych języka F #

W poniższej tabeli przedstawiono wszystkie słowa kluczowe języka F # w kolejności alfabetycznej wraz z krótkimi opisami i łączami do odpowiednich tematów, które zawierają więcej informacji.

|Słowo kluczowe|Łącze|Opis|
|-------|----|-----------|
|`abstract`|[Elementy członkowskie](./members/index.md)<br /><br />[Klasy abstrakcyjne](abstract-classes.md)|Wskazuje metodę, która nie ma implementacji w typie, w którym jest zadeklarowana lub jest wirtualna i ma implementację domyślną.|
|`and`|[`let` Powiązań](./functions/let-bindings.md)<br /><br />[Rekordy](records.md)<br /><br />[Elementy członkowskie](./members/index.md)<br /><br />[Ograniczenia](./generics/constraints.md)|Używane w wzajemnie rekurencyjnych powiązaniach i rekordach, w deklaracjach właściwości i z wieloma ograniczeniami parametrów ogólnych.|
|`as`|[Klasy](classes.md)<br /><br />[Dopasowanie wzorca](Pattern-Matching.md)|Służy do nadawania obiektowi Current klasy nazwy obiektu. Służy również do przyciągania nazwy do całego wzorca w ramach dopasowania do wzorca.|
|`assert`|[Potwierdzenia](assertions.md)|Służy do weryfikowania kodu podczas debugowania.|
|`base`|[Klasy](classes.md)<br /><br />[Dziedziczenie](inheritance.md)|Używane jako nazwa obiektu klasy bazowej.|
|`begin`|[Pełna składnia](verbose-syntax.md)|W instrukcji verbose wskazuje początek bloku kodu.|
|`class`|[Klasy](classes.md)|W instrukcji verbose wskazuje początek definicji klasy.|
|`default`|[Elementy członkowskie](./members/index.md)|Wskazuje implementację metody abstrakcyjnej; używane razem z deklaracją metody abstrakcyjnej do utworzenia metody wirtualnej.|
|`delegate`|[Delegaci](delegates.md)|Używane do deklarowania delegata.|
|`do`|[do — Powiązania](./functions/do-bindings.md)<br /><br />[Pętle: `for...to` wyrażenie](loops-for-to-expression.md)<br /><br />[Pętle: `for...in` wyrażenie](loops-for-in-expression.md)<br /><br />[Pętle: `while...do` wyrażenie](loops-while-do-expression.md)|Używane w konstrukcjach pętli lub do wykonywania bezwzględnie kodu.|
|`done`|[Pełna składnia](verbose-syntax.md)|W instrukcji verbose wskazuje koniec bloku kodu w wyrażeniu zapętlenia.|
|`downcast`|[Rzutowanie i konwersje](casting-and-conversions.md)|Używane do konwertowania na typ, który jest niższy w łańcuchu dziedziczenia.|
|`downto`|[Pętle: `for...to` wyrażenie](loops-for-to-expression.md)|W `for` wyrażeniu używanym podczas zliczania w odwrotnej postaci.|
|`elif`|[Wyrażenia warunkowe: `if...then...else`](conditional-expressions-if-then-else.md)|Używane w rozgałęzieniu warunkowym. Krótka forma `else if` .|
|`else`|[Wyrażenia warunkowe: `if...then...else`](conditional-expressions-if-then-else.md)|Używane w rozgałęzieniu warunkowym.|
|`end`|[Struktury](structures.md)<br /><br />[Sumy rozłączne](discriminated-unions.md)<br /><br />[Rekordy](records.md)<br /><br />[Rozszerzenia typu](type-extensions.md)<br /><br />[Pełna składnia](verbose-syntax.md)|W definicjach typów i rozszerzeniach typów wskazuje koniec sekcji definicji elementu członkowskiego.<br /><br />W pełnej składni, używany do określenia końca bloku kodu, który rozpoczyna się od `begin` słowa kluczowego.|
|`exception`|[Obsługa wyjątków](./exception-handling/index.md)<br /><br />[Typy wyjątków](./exception-handling/exception-types.md)|Używane do deklarowania typu wyjątku.|
|`extern`|[Funkcje zewnętrzne](./functions/external-functions.md)|Wskazuje, że zadeklarowany element programu jest zdefiniowany w innym pliku binarnym lub zestawie.|
|`false`|[Typy pierwotne](basic-types.md)|Używany jako literał wartości logicznej.|
|`finally`|[Wyjątki: `try...finally` wyrażenie](./exception-handling/the-try-finally-expression.md)|Używane razem z `try` , aby wprowadzić blok kodu, który jest wykonywany bez względu na to, czy wystąpił wyjątek.|
|`fixed`|[FIXED](fixed.md)|Służy do "przypinania" wskaźnika na stosie, aby zapobiec występowaniu elementów bezużytecznych.|
|`for`|[Pętle: `for...to` wyrażenie](loops-for-to-expression.md)<br /><br />[Pętle: for...in — Wyrażenie](loops-for-in-expression.md)|Używane w konstrukcjach zapętlenia.|
|`fun`|[Wyrażenia lambda: `fun` słowo kluczowe](./functions/lambda-expressions-the-fun-keyword.md)|Używane w wyrażeniach lambda, znane także jako funkcje anonimowe.|
|`function`|[Wyrażenia dopasowania](match-expressions.md)<br /><br />[Wyrażenia lambda: słowo kluczowe "zabawny"](./functions/lambda-expressions-the-fun-keyword.md)|Używane jako krótsza alternatywa dla `fun` słowa kluczowego i `match` wyrażenia w wyrażeniu lambda, które ma dopasowanie wzorca dla jednego argumentu.|
|`global`|[Przestrzenie nazw](namespaces.md)|Służy do odwoływania się do przestrzeni nazw najwyższego poziomu platformy .NET.|
|`if`|[Wyrażenia warunkowe: `if...then...else`](conditional-expressions-if-then-else.md)|Używane w konstrukcjach rozgałęzień warunkowych.|
|`in`|[Pętle: for...in — Wyrażenie](loops-for-in-expression.md)<br /><br />[Pełna składnia](verbose-syntax.md)|Używane dla wyrażeń sekwencji i, w składni pełnej, do oddzielania wyrażeń od powiązań.|
|`inherit`|[Dziedziczenie](inheritance.md)|Służy do określania klasy bazowej lub interfejsu bazowego.|
|`inline`|[Funkcje](./functions/index.md)<br /><br />[Funkcje śródwierszowe](./functions/inline-functions.md)|Służy do wskazywania funkcji, która powinna być zintegrowana bezpośrednio z kodem wywołującym.|
|`interface`|[Interfejsy](interfaces.md)|Używane do deklarowania i implementowania interfejsów.|
|`internal`|[Access Control](access-control.md)|Służy do określenia, że element członkowski jest widoczny wewnątrz zestawu, ale nie poza nim.|
|`lazy`|[Wyrażenia z opóźnionym obliczaniem](lazy-expressions.md)|Służy do określania wyrażenia, które ma zostać wykonane tylko wtedy, gdy jest wymagany wynik.|
|`let`|[`let` Powiązań](./functions/let-bindings.md)|Służy do kojarzenia nazwy z wartością lub funkcją.|
|`let!`|[Asynchroniczne przepływy pracy](asynchronous-workflows.md)<br /><br />[Wyrażenia obliczeń](computation-expressions.md)|Używany w asynchronicznych przepływach pracy w celu powiązania nazwy z wynikiem obliczeń asynchronicznych lub w innych wyrażeniach obliczeniowych, użytych do powiązania nazwy z wynikiem, który jest typem obliczenia.|
|`match`|[Wyrażenia dopasowania](match-expressions.md)|Używane do rozgałęziania przez porównanie wartości ze wzorcem.|
|`match!`|[Wyrażenia obliczeń](computation-expressions.md#match)|Służy do wbudowania wywołania wyrażenia obliczeń i dopasowania do wzorca w wyniku.|
|`member`|[Elementy członkowskie](./members/index.md)|Używane do deklarowania właściwości lub metody w typie obiektu.|
|`module`|[Moduły](modules.md)|Służy do kojarzenia nazwy z grupą powiązanych typów, wartości i funkcji, aby logicznie oddzielić ją od innego kodu.|
|`mutable`|[let — Powiązania](./functions/let-bindings.md)|Używane do deklarowania zmiennej, czyli wartości, którą można zmienić.|
|`namespace`|[Przestrzenie nazw](namespaces.md)|Służy do kojarzenia nazwy z grupą powiązanych typów i modułów, aby logicznie oddzielić ją od innego kodu.|
|`new`|[Konstruktory](./members/constructors.md)<br /><br />[Ograniczenia](./generics/constraints.md)|Służy do deklarowania, definiowania lub wywoływania konstruktora, który tworzy lub który może utworzyć obiekt.<br /><br />Używane również w ograniczeniach parametru generycznego, aby wskazać, że typ musi mieć określony Konstruktor.|
|`not`|[Odwołanie do symbolu i operatora](./symbol-and-operator-reference/index.md)<br /><br />[Ograniczenia](./generics/constraints.md)|W rzeczywistości nie jest słowem kluczowym. Jednak `not struct` w kombinacji jest używana jako ograniczenie parametru ogólnego.|
|`null`|[Wartości null](./values/null-values.md)<br /><br />[Ograniczenia](./generics/constraints.md)|Wskazuje brak obiektu.<br /><br />Używane również w ograniczeniach parametru generycznego.|
|`of`|[Sumy rozłączne](discriminated-unions.md)<br /><br />[Delegaci](delegates.md)<br /><br />[Typy wyjątków](./exception-handling/exception-types.md)|Używane w Unii rozłącznych, aby wskazać typ kategorii wartości, a w deklaracjach delegatów i wyjątków.|
|`open`|[Deklaracje importu: `open` słowo kluczowe](import-declarations-the-open-keyword.md)|Służy do udostępnienia zawartości przestrzeni nazw lub modułu bez kwalifikacji.|
|`or`|[Odwołanie do symbolu i operatora](./symbol-and-operator-reference/index.md)<br /><br />[Ograniczenia](./generics/constraints.md)|Używany z warunkami logicznymi jako `or` operator logiczny. Odpowiednik `||` .<br /><br />Używane również w ograniczeniach elementu członkowskiego.|
|`override`|[Elementy członkowskie](./members/index.md)|Służy do implementowania wersji metody abstrakcyjnej lub wirtualnej, która różni się od wersji podstawowej.|
|`private`|[Access Control](access-control.md)|Ogranicza dostęp do elementu członkowskiego do kodu w tym samym typie lub module.|
|`public`|[Access Control](access-control.md)|Zezwala na dostęp do elementu członkowskiego spoza typu.|
|`rec`|[Funkcje](./functions/index.md)|Używane do wskazywania, że funkcja jest cykliczna.|
|`return`|[Asynchroniczne przepływy pracy](Asynchronous-Workflows.md)<br /><br />[Wyrażenia obliczeń](computation-expressions.md)|Służy do wskazania wartości, która ma być używana jako wynik wyrażenia obliczeń.|
|`return!`|[Wyrażenia obliczeń](computation-expressions.md)<br /><br />[Asynchroniczne przepływy pracy](asynchronous-workflows.md)|Służy do wskazania wyrażenia obliczeń, które, gdy jest oceniane, zawiera wynik wyrażenia zawierającego wyrażenie obliczeniowe.|
|`select`|[Wyrażenia kwerend](query-expressions.md)|Używane w wyrażeniach zapytań w celu określenia pól lub kolumn do wyodrębnienia. Należy zauważyć, że jest to kontekstowe słowo kluczowe, co oznacza, że nie jest w rzeczywistości słowem zastrzeżonym i działa tylko jako słowo kluczowe w odpowiednim kontekście.|
|`static`|[Elementy członkowskie](./members/index.md)|Służy do wskazywania metody lub właściwości, które można wywołać bez wystąpienia typu, lub elementu członkowskiego wartości, który jest współużytkowany przez wszystkie wystąpienia typu.|
|`struct`|[Struktury](structures.md)<br /><br /> [Krotki](tuples.md)<br/><br/>[Ograniczenia](./generics/constraints.md)|Używane do deklarowania typu struktury.<br /><br/>Służy do określania krotki struktury.<br/><br />Używane również w ograniczeniach parametru generycznego.<br /><br />Używane na potrzeby zgodności OCaml w definicjach modułów.|
|`then`|[Wyrażenia warunkowe: `if...then...else`](conditional-expressions-if-then-else.md)<br /><br />[Konstruktory](./members/constructors.md)|Używane w wyrażeniach warunkowych.<br /><br />Używane również do wykonywania efektów ubocznych po konstrukcji obiektu.|
|`to`|[Pętle: `for...to` wyrażenie](loops-for-to-expression.md)|Używane w `for` pętlach, aby wskazać zakres.|
|`true`|[Typy pierwotne](basic-types.md)|Używany jako literał wartości logicznej.|
|`try`|[Wyjątki: try...with — Wyrażenie](./exception-handling/the-try-with-expression.md)<br /><br />[Wyjątki: try...finally — Wyrażenie](./exception-handling/the-try-finally-expression.md)|Służy do wprowadzenia bloku kodu, który może generować wyjątek. Używane razem z `with` lub `finally` .|
|`type`|[Typy F#](fsharp-types.md)<br /><br />[Klasy](classes.md)<br /><br />[Rekordy](records.md)<br /><br />[Struktury](structures.md)<br /><br />[Wyliczenia](enumerations.md)<br /><br />[Sumy rozłączne](discriminated-unions.md)<br /><br />[Skróty typów](type-abbreviations.md)<br /><br />[Jednostki miary](units-of-measure.md)|Służy do deklarowania klasy, rekordu, struktury, Unii rozłącznej, typu wyliczeniowego, jednostki miary lub skrótu typu.|
|`upcast`|[Rzutowanie i konwersje](casting-and-conversions.md)|Używane do konwertowania na typ, który jest wyższy w łańcuchu dziedziczenia.|
|`use`|[Zarządzanie zasobami: `use` słowo kluczowe](resource-management-the-use-keyword.md)|Używane zamiast `let` wartości, które wymagają `Dispose` wywołania w celu zwolnienia zasobów.|
|`use!`|[Wyrażenia obliczeń](computation-expressions.md)<br /><br />[Asynchroniczne przepływy pracy](asynchronous-workflows.md)|Używane zamiast `let!` w asynchronicznych przepływach pracy i innych wyrażeniach obliczeń dla wartości, które wymagają `Dispose` wywołania w celu zwolnienia zasobów.|
|`val`|[Pola jawne: `val` słowo kluczowe](./members/explicit-fields-the-val-keyword.md)<br /><br />[Podpisy](signature-files.md)<br /><br />[Elementy członkowskie](./members/index.md)|Używane w podpisie do wskazywania wartości lub w typie do deklarowania elementu członkowskiego w ograniczonych sytuacjach.|
|`void`|[Typy pierwotne](basic-types.md)|Wskazuje typ .NET `void` . Używane podczas współdziałania z innymi językami .NET.|
|`when`|[Ograniczenia](./generics/constraints.md)|Używane dla warunków logicznych (w*przypadku funkcji Guard*) w dopasowaniach wzorca i w celu wprowadzenia klauzuli ograniczenia dla parametru typu ogólnego.|
|`while`|[Pętle: `while...do` wyrażenie](loops-while-do-expression.md)|Wprowadza konstrukcję pętli.|
|`with`|[Wyrażenia dopasowania](match-expressions.md)<br /><br />[Wyrażenia obiektów](object-expressions.md)<br /><br />[Kopiowanie i aktualizacja wyrażeń rekordów](copy-and-update-record-expressions.md)<br /><br />[Rozszerzenia typu](type-extensions.md)<br /><br />[Wyjątki: `try...with` wyrażenie](./exception-handling/the-try-with-expression.md)|Używane razem ze `match` słowem kluczowym w wyrażeniach dopasowania wzorców. Używane również w wyrażeniach obiektów, rekordach kopiowania i rozszerzeniach w celu wprowadzenia definicji elementów członkowskich i wprowadzenia obsługi wyjątków.|
|`yield`|[Listy](lists.md), [tablice](arrays.md), [sekwencje](sequences.md)|Używany w wyrażeniu list, tablicy lub sekwencji do tworzenia wartości dla sekwencji. Zazwyczaj można pominąć, ponieważ w większości przypadków jest to niejawne.|
|`yield!`|[Wyrażenia obliczeń](computation-expressions.md)<br /><br />[Asynchroniczne przepływy pracy](asynchronous-workflows.md)|Używany w wyrażeniu obliczeniowym do dołączania wyniku danego wyrażenia obliczenia do kolekcji wyników dla zawierającego wyrażenie obliczenia.|
|`const`|[Dostawcy typów](../tutorials/type-providers/index.md)| Dostawcy typów umożliwiają użycie `const` słowa kluczowego AS do określenia stałego literału jako argumentu parametru typu.|

Następujące tokeny są zastrzeżone w języku F #, ponieważ są słowami kluczowymi w OCaml:

- `asr`
- `land`
- `lor`
- `lsl`
- `lsr`
- `lxor`
- `mod`
- `sig`

Jeśli używasz `--mlcompatibility` opcji kompilatora, powyższe słowa kluczowe są dostępne do użycia jako identyfikatory.

Następujące tokeny są zastrzeżone jako słowa kluczowe do przyszłego rozwinięcia języka F #:

- `atomic`
- `break`
- `checked`
- `component`
- `const`
- `constraint`
- `constructor`
- `continue`
- `eager`
- `event`
- `external`
- `functor`
- `include`
- `method`
- `mixin`
- `object`
- `parallel`
- `process`
- `protected`
- `pure`
- `sealed`
- `tailcall`
- `trait`
- `virtual`
- `volatile`

## <a name="see-also"></a>Zobacz też

- [Dokumentacja języka F #](index.md)
- [Odwołanie do symbolu i operatora](./symbol-and-operator-reference/index.md)
- [Opcje kompilatora](compiler-options.md)
