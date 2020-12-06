---
title: Dopasowanie wzorca
description: 'Dowiedz się, w jaki sposób wzorce są używane w języku F # do porównywania danych ze strukturami logicznymi, rozkładania danych na części składowych lub wyodrębniania informacji z danych.'
ms.date: 11/12/2020
ms.openlocfilehash: 932f50b7947f6df728149437dd3ceb19c42e5c6a
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96740279"
---
# <a name="pattern-matching"></a>Dopasowanie wzorca

Wzorce są regułami do przekształcania danych wejściowych. Są one używane w całym języku F # do porównywania danych ze strukturą logiczną lub strukturami, rozkładania danych do części składowych lub wyodrębniania informacji z danych na różne sposoby.

## <a name="remarks"></a>Uwagi

Wzorce są używane w wielu konstrukcjach języka, takich jak `match` wyrażenie. Są one używane podczas przetwarzania argumentów dla funkcji w `let` powiązaniach, wyrażeniach lambda i w obsłudze wyjątków skojarzonych z `try...with` wyrażeniem. Aby uzyskać więcej informacji, zobacz [wyrażenia dopasowywania](match-expressions.md), [Zezwalanie na powiązania](./functions/let-bindings.md), [wyrażenia lambda: `fun` słowo kluczowe](./functions/lambda-expressions-the-fun-keyword.md)i [wyjątki: `try...with` wyrażenie](./exception-handling/the-try-with-expression.md).

Na przykład, w `match` wyrażeniu *wzorzec* jest zgodny z symbolem potoku.

```fsharp
match expression with
| pattern [ when condition ] -> result-expression
...
```

Każdy wzorzec działa jako reguła do przekształcania danych wejściowych w jakiś sposób. W `match` wyrażeniu każdy wzorzec jest sprawdzany z kolei, aby sprawdzić, czy dane wejściowe są zgodne ze wzorcem. W przypadku znalezienia dopasowania zostanie wykonane wyrażenie wynik. Jeśli dopasowanie nie zostanie znalezione, zostanie przetestowana następna reguła wzorca. Wartość opcjonalna, gdy część *warunku* jest objaśniona w [wyrażeniach dopasowania](match-expressions.md).

Obsługiwane wzorce przedstawiono w poniższej tabeli. W czasie wykonywania, dane wejściowe są testowane względem każdego z następujących wzorców w kolejności wymienionej w tabeli, a wzorce są stosowane cyklicznie, od pierwszego do ostatniego, jak pojawiają się w kodzie, i od lewej do prawej dla wzorców w każdym wierszu.

|Nazwa|Opis|Przykład|
|----|-----------|-------|
|Wzorzec stałej|Dowolny literał numeryczny, znak lub ciąg, stała wyliczenia lub zdefiniowany identyfikator literału|`1.0`, `"test"`, `30`, `Color.Red`|
|Wzorzec identyfikatora|Wartość przypadku Unii rozłącznej, etykieta wyjątku lub przypadek aktywnego wzorca|`Some(x)`<br /><br />`Failure(msg)`|
|Wzorzec zmiennej|*identyfikatora*|`a`|
|`as` znaczne|*wzorzec* jako *Identyfikator*|`(a, b) as tuple1`|
|LUB wzorzec|*pattern1* &#124; *pattern2*|<code>([h] &#124; [h; _])</code>|
|I wzorzec|*pattern1* &amp; *pattern2*|`(a, b) & (_, "test")`|
|Wzorzec wad|*Identyfikator* :: *list — identyfikator*|`h :: t`|
|Wzorzec listy|[ *pattern_1*;...; *pattern_n* ]|`[ a; b; c ]`|
|Wzorzec tablicy|[&#124; *pattern_1*;..; *pattern_n* &#124;]|<code>[&#124; a; b; c &#124;]</code>|
|Wzorzec w nawiasach|( *wzorzec* )|`( a )`|
|Wzorzec krotki|( *pattern_1*,..., *pattern_n* )|`( a, b )`|
|Wzorzec rekordu|{ *Identifier1*  =  *pattern_1*; ... ; *identifier_n*  =  *pattern_n* }|`{ Name = name; }`|
|Wzorzec wieloznaczny|_|`_`|
|Wzorzec wraz z adnotacją typu|*wzorzec* : *Typ*|`a : int`|
|Typ wzorca testu|:? *Typ* [ *Identyfikator* as]|`:? System.DateTime as dt`|
|Wzorzec o wartości null|wartość null|`null`|
|Wzorzec nameof|*wyrażenie nameof*|`nameof str`|

## <a name="constant-patterns"></a>Wzorce stałe

Wzorce stałe są literami, znakami i literałami ciągów, stałymi wyliczeniami (z uwzględnieniem nazwy typu wyliczenia). `match`Wyrażenie, które ma tylko stałe wzorce, można porównać do instrukcji case w innych językach. Dane wejściowe są porównywane z wartością literału, a wzorzec pasuje, jeśli wartości są równe. Typ literału musi być zgodny z typem danych wejściowych.

Poniższy przykład demonstruje użycie wzorców literałów, a także używa wzorca zmiennej i wzorca OR.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4801.fs)]

Innym przykładem wzorca literału jest wzorzec oparty na stałych wyliczeniach. Należy określić nazwę typu wyliczeniowego w przypadku używania stałych wyliczania.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4802.fs)]

## <a name="identifier-patterns"></a>Wzorce identyfikatorów

Jeśli wzorzec jest ciągiem znaków, który tworzy prawidłowy identyfikator, formularz identyfikatora określa sposób dopasowania wzorca. Jeśli identyfikator jest dłuższy niż pojedynczy znak i zaczyna się od wielkiej litery, kompilator próbuje dopasować wzorzec identyfikatora. Identyfikatorem tego wzorca może być wartość oznaczona przy użyciu atrybutu literału, przypadku Unii rozłącznej, identyfikatora wyjątku lub aktywnego przypadku wzorca. Jeśli nie znaleziono zgodnego identyfikatora, dopasowanie nie powiedzie się, a następna reguła wzorca, wzorzec zmiennej, jest porównywana z danymi wejściowymi.

Wzorce Unii rozłącznych mogą być prostymi nazwanymi przypadkami lub mogą mieć wartość lub krotkę zawierającą wiele wartości. Jeśli istnieje wartość, należy określić identyfikator dla tej wartości. W przypadku krotki, należy podać wzorzec krotki z identyfikatorem dla każdego elementu krotki lub identyfikatora z nazwą pola dla jednego lub więcej nazwanych pól Union. Przykłady kodu można znaleźć w przykładach w tej sekcji.

Typ jest Unią rozłączną, `option` która ma dwa przypadki, `Some` i `None` . Jeden przypadek ( `Some` ) ma wartość, ale drugi ( `None` ) jest tylko nazwanym przypadkiem. W związku z tym, musi `Some` mieć zmienną dla wartości skojarzonej z `Some` przypadkiem, ale `None` musi być wyświetlana sama przez siebie. W poniższym kodzie zmienna `var1` otrzymuje wartość uzyskaną przez dopasowanie do `Some` wielkości liter.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4803.fs)]

W poniższym przykładzie `PersonName` związek rozłącznych zawiera kombinację ciągów i znaków, które reprezentują możliwe formy nazw. Przypadki rozłącznych zbiorów to `FirstOnly` , `LastOnly` i `FirstLast` .

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4804.fs)]

W przypadku Unii rozłącznych, które mają nazwane pola, należy użyć znaku równości (=) do wyodrębnienia wartości nazwanego pola. Rozważmy na przykład Unię rozłącznych z deklaracją podobną do następującej.

```fsharp
type Shape =
    | Rectangle of height : float * width : float
    | Circle of radius : float
```

Możesz użyć nazwanych pól w wyrażeniu dopasowania wzorca w następujący sposób.

```fsharp
let matchShape shape =
    match shape with
    | Rectangle(height = h) -> printfn $"Rectangle with length %f{h}"
    | Circle(r) -> printfn $"Circle with radius %f{r}"
```

Użycie nazwanego pola jest opcjonalne, dlatego w poprzednim przykładzie oba `Circle(r)` i `Circle(radius = r)` mają ten sam efekt.

Po określeniu wielu pól Użyj średnika (;) jako separator.

```fsharp
match shape with
| Rectangle(height = h; width = w) -> printfn $"Rectangle with height %f{h} and width %f{w}"
| _ -> ()
```

Aktywne wzorce umożliwiają zdefiniowanie bardziej złożonej niestandardowej dopasowywania do wzorca. Aby uzyskać więcej informacji na temat aktywnych wzorców, zobacz [aktywne wzorce](active-patterns.md).

Przypadek, w którym identyfikator jest wyjątek jest używany w dopasowywaniu wzorców w kontekście obsługi wyjątków. Aby uzyskać informacje na temat dopasowywania wzorców w obsłudze wyjątków, zobacz [wyjątki: `try...with` wyrażenie](./exception-handling/the-try-with-expression.md).

## <a name="variable-patterns"></a>Wzorce zmiennych

Wzór zmiennej przypisuje wartość dopasowaną do nazwy zmiennej, która jest następnie dostępna do użycia w wyrażeniu wykonywania na prawo od `->` symbolu. Sam wzorzec zmiennej pasuje do dowolnych danych wejściowych, ale wzorce zmiennych często pojawiają się w innych wzorcach, co pozwala na bardziej złożone struktury, takie jak krotki i tablice, do rozdzielania na zmienne.

Poniższy przykład ilustruje wzór zmiennej w obrębie wzorca krotki.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4805.fs)]

## <a name="as-pattern"></a>jako wzorzec

`as`Wzorzec jest wzorcem z `as` dołączoną do niej klauzulą. `as`Klauzula wiąże dopasowaną wartość do nazwy, która może być używana w wyrażeniu wykonywania `match` wyrażenia lub, w przypadku, gdy ten wzorzec jest używany w `let` powiązaniu, nazwa jest dodawana jako powiązanie do zakresu lokalnego.

Poniższy przykład używa `as` wzorca.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4806.fs)]

## <a name="or-pattern"></a>LUB wzorzec

Wzorzec OR jest używany, gdy dane wejściowe mogą odpowiadać wielu wzorcem i chcesz wykonać ten sam kod w wyniku. Typy obu stron wzorca OR muszą być zgodne.

Poniższy przykład demonstruje wzorzec OR.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4807.fs)]

## <a name="and-pattern"></a>I wzorzec

Wzorzec i wymaga, aby dane wejściowe były zgodne z dwoma wzorcami. Typy obu stron wzorca i muszą być zgodne.

Poniższy przykład jest podobny do `detectZeroTuple` przedstawionego w sekcji wzorzec krotki w dalszej części tego tematu, ale w tym miejscu `var1` i `var2` są uzyskiwane jako wartości przy użyciu wzorca i.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4808.fs)]

## <a name="cons-pattern"></a>Wzorzec wad

Wzorzec wad służy do rozdzielania listy na pierwszy element, *nagłówek* i listę zawierającą pozostałe elementy, *ogon*.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4809.fs)]

## <a name="list-pattern"></a>Wzorzec listy

Wzorzec listy umożliwia rozdzielanie list na wiele elementów. Sam wzorzec listy może pasować tylko do list o określonej liczbie elementów.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4810.fs)]

## <a name="array-pattern"></a>Wzorzec tablicy

Wzór tablicy przypomina wzorzec listy i może służyć do rozdzielania tablic o określonej długości.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4811.fs)]

## <a name="parenthesized-pattern"></a>Wzorzec w nawiasach

Nawiasy można grupować wokół wzorców w celu osiągnięcia żądanych łączność. W poniższym przykładzie nawiasy są używane do kontrolowania łączność między wzorcem a i wzorcem wad.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4812.fs)]

## <a name="tuple-pattern"></a>Wzorzec krotki

Wzorzec krotki dopasowuje dane wejściowe w postaci spójnej kolekcji i umożliwia rozłożenie krotki na elementy składowe za pomocą zmiennych dopasowywania wzorców dla każdej pozycji w spójnej kolekcji.

Poniższy przykład demonstruje wzorzec krotki i używa także wzorców literałów, wzorów zmiennych i wzorca symboli wieloznacznych.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4813.fs)]

## <a name="record-pattern"></a>Wzorzec rekordu

Wzorzec rekordu służy do rozkładania rekordów w celu wyodrębnienia wartości pól. Wzorzec nie musi odwoływać się do wszystkich pól rekordu; wszystkie pominięte pola tylko nie uczestniczą w dopasowaniu i nie są wyodrębniane.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4814.fs)]

## <a name="wildcard-pattern"></a>Wzorzec wieloznaczny

Wzorzec symbol wieloznaczny jest reprezentowany przez znak podkreślenia ( `_` ) i dopasowuje wszelkie dane wejściowe, podobnie jak wzór zmiennej, z tą różnicą, że dane wejściowe są odrzucane zamiast przypisywania do zmiennej. Wzorzec symbol wieloznaczny jest często używany w innych wzorcach jako symbol zastępczy dla wartości, które nie są konieczne w wyrażeniu z prawej strony `->` symbolu. Wzorzec symboli wieloznacznych jest również często używany na końcu listy wzorców w celu dopasowania do niedopasowanych danych wejściowych. Wzorzec symboli wieloznacznych jest prezentowany w wielu przykładach kodu w tym temacie. Zobacz poprzedni kod na jeden przykład.

## <a name="patterns-that-have-type-annotations"></a>Wzorce, które mają adnotacje typu

Wzorce mogą mieć adnotacje typu. Zachowują się one tak jak inne adnotacje typu i w odróżnieniu od innych typów. Nawiasy są wymagane wokół adnotacji typu w wzorcach. Poniższy kod przedstawia wzorzec, który ma adnotację typu.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4815.fs)]

## <a name="type-test-pattern"></a>Typ wzorca testu

Wzorzec testu typu jest używany do dopasowania danych wejściowych do typu. Jeśli typ danych wejściowych jest zgodny z (lub typem pochodnym) typu określonego we wzorcu, dopasowanie powiedzie się.

Poniższy przykład demonstruje wzorzec testu typu.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4816.fs)]

Jeśli sprawdzasz tylko, czy identyfikator jest określonego typu pochodnego, nie potrzebujesz `as identifier` części wzorca, jak pokazano w następującym przykładzie:

```fsharp
type A() = class end
type B() = inherit A()
type C() = inherit A()

let m (a: A) =
    match a with
    | :? B -> printfn "It's a B"
    | :? C -> printfn "It's a C"
    | _ -> ()
```

## <a name="null-pattern"></a>Wzorzec o wartości null

Wzorzec o wartości null jest zgodny z wartością null, która może pojawić się podczas pracy z typami, które zezwalają na wartość null. Wzorce o wartości null są często używane podczas współdziałania z kodem .NET Framework. Na przykład wartość zwracana przez interfejs API platformy .NET może być danymi wejściowymi do `match` wyrażenia. Można kontrolować przepływ programu w zależności od tego, czy zwracana wartość jest równa null, a także od innych cech zwracanej wartości. Możesz użyć wzorca o wartości null, aby zapobiec propagowaniu wartości null do reszty programu.

Poniższy przykład używa wzorca o wartości null i wzorca zmiennej.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4817.fs)]

## <a name="nameof-pattern"></a>Wzorzec nameof

`nameof`Wzorzec jest zgodny z ciągiem, gdy jego wartość jest równa wyrażeniu, które następuje po `nameof` słowie kluczowym. na przykład:

```fsharp
let f (str: string) =
    match str with
    | nameof str -> "It's 'str'!"
    | _ -> "It is not 'str'!"

f "str" // matches
f "asdf" // does not match
```

Zapoznaj się z [`nameof`](nameof.md) operatorem, aby uzyskać informacje o tym, co można zrobić z nazwą.

## <a name="see-also"></a>Zobacz także

- [Wyrażenia dopasowania](match-expressions.md)
- [Wzorce aktywne](active-patterns.md)
- [Dokumentacja języka F #](index.md)
