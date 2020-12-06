---
title: Sumy rozłączne
description: 'Dowiedz się, jak używać związków rozłącznych w języku F #.'
ms.date: 08/15/2020
ms.openlocfilehash: f90ac2c2ea21182cf5fd3657d2ada00a763139fe
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96740240"
---
# <a name="discriminated-unions"></a>Sumy rozłączne

Związki rozłączne zapewniają obsługę wartości, które mogą być jedną z wielu nazwanych przypadków, prawdopodobnie z różnymi wartościami i typami. Związki rozłącznych są przydatne w przypadku danych heterogenicznych; dane, które mogą mieć specjalne przypadki, w tym prawidłowe i błędne przypadki; dane, które różnią się w typie z jednego wystąpienia na inne; i jako alternatywę dla małych hierarchii obiektów. Ponadto cykliczne związki rozłącznych są używane do reprezentowania struktur danych drzewa.

## <a name="syntax"></a>Składnia

```fsharp
[ attributes ]
type [accessibility-modifier] type-name =
    | case-identifier1 [of [ fieldname1 : ] type1 [ * [ fieldname2 : ] type2 ...]
    | case-identifier2 [of [fieldname3 : ]type3 [ * [ fieldname4 : ]type4 ...]

    [ member-list ]
```

## <a name="remarks"></a>Uwagi

Związki rozłączne są podobne do typów Unii w innych językach, ale istnieją różnice. Podobnie jak w przypadku typu Unii w języku C++ lub typu wariantowego w Visual Basic, dane przechowywane w wartości nie są naprawione; może to być jedna z kilku odrębnych opcji. Jednak w przeciwieństwie do Unii w tych innych językach, każda z możliwych opcji ma *Identyfikator przypadku*. Identyfikatory przypadków są nazwami różnych możliwych typów wartości, które obiekty tego typu mogą być; wartości są opcjonalne. Jeśli wartości nie są obecne, sprawa jest równoważna z wielkością liter wyliczenia. Jeśli wartości są obecne, każda wartość może być pojedynczą wartością określonego typu lub krotką agregującą wiele pól tego samego lub różnych typów. Można nadać pojedynczemu polu nazwę, ale nazwa jest opcjonalna, nawet jeśli inne pola w tym samym przypadku mają nazwę.

Dostępność dla Unii rozłącznych jest domyślnie ustawiona na `public` .

Rozważmy na przykład następującą deklarację typu kształtu.

```fsharp
type Shape =
    | Rectangle of width : float * length : float
    | Circle of radius : float
    | Prism of width : float * float * height : float
```

Poprzedni kod deklaruje kształt Unii rozłącznej, który może mieć wartości z trzech przypadków: prostokąt, okrąg i biblioteki Prism. Każdy przypadek ma inny zestaw pól. Przypadek prostokąta ma dwa nazwane pola, oba typy `float` , które mają szerokość i długość. Przypadek okręgu ma tylko jedno nazwane pole, promień. Przypadek biblioteki Prism ma trzy pola, dwa z których (szerokość i wysokość) są nazwanymi polami. Pola nienazwane są określane jako pola anonimowe.

Obiekty są konstruowane przez podanie wartości pól nazwanych i anonimowych zgodnie z poniższymi przykładami.

```fsharp
let rect = Rectangle(length = 1.3, width = 10.0)
let circ = Circle (1.0)
let prism = Prism(5., 2.0, height = 3.0)
```

Ten kod pokazuje, że można użyć nazwanych pól w inicjalizacji lub można polegać na kolejności pól w deklaracji i po prostu podać wartości dla każdego pola. Wywołanie konstruktora dla `rect` w poprzednim kodzie używa nazwanych pól, ale wywołanie konstruktora `circ` używa kolejności. Można mieszać pola uporządkowane i nazwane pola, jak w konstrukcji `prism` .

`option`Typ to prosty związek rozłącznych w podstawowej bibliotece języka F #. `option`Typ jest zadeklarowany w następujący sposób.

```fsharp
// The option type is a discriminated union.
type Option<'a> =
    | Some of 'a
    | None
```

Poprzedni kod określa, że typ `Option` jest Unią rozłącznych, która ma dwa przypadki `Some` i `None` . `Some`Przypadek ma skojarzoną wartość, która składa się z jednego pola anonimowego, którego typ jest reprezentowany przez parametr typu `'a` . `None`Przypadek nie ma skojarzonej wartości. W tym celu `option` Typ określa typ ogólny, który ma wartość pewnego typu lub nie ma wartości. Typ `Option` ma również alias typu małe litery, `option` który jest częściej często używany.

Identyfikatory przypadków mogą służyć jako konstruktory dla typu Unii rozłącznej. Na przykład poniższy kod służy do tworzenia wartości `option` typu.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2001.fs)]

Identyfikatory przypadków są również używane w wyrażeniach dopasowania wzorców. W wyrażeniu dopasowania do wzorca identyfikatory są udostępniane dla wartości skojarzonych z indywidualnymi przypadkami. Na przykład, w poniższym kodzie, `x` jest identyfikatorem, który ma wartość, która jest skojarzona z `Some` wielkością liter `option` typu.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2002.fs)]

W wyrażeniach dopasowania do wzorca można użyć nazwanych pól do określenia dopasowania złożenia rozłącznych. Dla typu kształtu, który został zadeklarowany wcześniej, można użyć nazwanych pól, jak pokazano w poniższym kodzie, aby wyodrębnić wartości pól.

```fsharp
let getShapeWidth shape =
    match shape with
    | Rectangle(width = w) -> w
    | Circle(radius = r) -> 2. * r
    | Prism(width = w) -> w
```

Zwykle identyfikatory przypadków mogą być używane bez kwalifikowania ich do nazwy związku. Jeśli chcesz, aby nazwa była zawsze kwalifikowana nazwą Unii, możesz zastosować atrybut [RequireQualifiedAccess](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-requirequalifiedaccessattribute.html) do definicji typu Unii.

### <a name="unwrapping-discriminated-unions"></a>Odpakowanie związków rozłącznych

W przypadku Unii rozłącznych w języku F # często są używane do modelowania domen do zawijania jednego typu. Można łatwo wyodrębnić podstawową wartość poprzez dopasowanie do wzorca. Nie musisz używać wyrażenia dopasowania dla pojedynczego przypadku:

```fsharp
let ([UnionCaseIdentifier] [values]) = [UnionValue]
```

Poniższy przykład ilustruje:

```fsharp
type ShaderProgram = | ShaderProgram of id:int

let someFunctionUsingShaderProgram shaderProgram =
    let (ShaderProgram id) = shaderProgram
    // Use the unwrapped value
    ...
```

Dopasowywanie do wzorca jest również dozwolone bezpośrednio w parametrach funkcji, więc można odwinąć pojedynczy przypadek:

```fsharp
let someFunctionUsingShaderProgram (ShaderProgram id) =
    // Use the unwrapped value
    ...
```

## <a name="struct-discriminated-unions"></a>Związki rozłącznych struktur

Można również reprezentować związki rozłączne jako struktury.  Jest to realizowane przy użyciu `[<Struct>]` atrybutu.

```fsharp
[<Struct>]
type SingleCase = Case of string

[<Struct>]
type Multicase =
    | Case1 of Case1 : string
    | Case2 of Case2 : int
    | Case3 of Case3 : double
```

Ponieważ są to typy wartości i nie są typami odwołań, istnieją dodatkowe zagadnienia w porównaniu z odniesiemi się do związków rozłącznych:

1. Są one kopiowane jako typy wartości i mają semantykę typu wartości.
2. Nie można użyć definicji typu cyklicznego z wieloliterowym związkiem rozłącznych struktury.
3. Należy podać unikatowe nazwy przypadków dla wieloliterowego związku wieloskładnikowego.

## <a name="using-discriminated-unions-instead-of-object-hierarchies"></a>Używanie Unii rozłącznych zamiast hierarchii obiektów

W przypadku niewielkiej alternatywy dla hierarchii obiektów często można użyć Unii rozłącznej. Na przykład, można użyć poniższego związku rozłącznych zamiast `Shape` klasy bazowej, która ma typy pochodne dla okręgu, kwadratu itd.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2003.fs)]

Zamiast metody wirtualnej do obliczenia obszaru lub obwodu, jak w przypadku implementacji zorientowanej obiektowo, można użyć dopasowania wzorców do gałęzi do odpowiednich formuł, aby obliczyć te ilości. W poniższym przykładzie różne formuły są używane do obliczania obszaru, w zależności od kształtu.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2004.fs)]

Wynik jest następujący:

```console
Area of circle that has radius 15.000000: 706.858347
Area of square that has side 10.000000: 100.000000
Area of rectangle that has height 5.000000 and width 10.000000 is 50.000000
```

## <a name="using-discriminated-unions-for-tree-data-structures"></a>Używanie związków rozłącznych dla struktur danych drzewa

Związki rozłączne mogą być cykliczne, co oznacza, że sama Unia może być uwzględniona w typie jednego lub więcej przypadków. Cykliczne związki rozłącznych mogą służyć do tworzenia struktur drzewa, które są używane do modelowania wyrażeń w językach programowania. W poniższym kodzie rekursywny związek rozłącznych służy do tworzenia struktury danych drzewa binarnego. Unia składa się z dwóch przypadków, `Node` , który jest węzłem z wartością całkowitą oraz poddrzewami z lewej i prawej strony, i `Tip` , który kończy drzewo.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2005.fs)]

W poprzednim kodzie `resultSumTree` ma wartość 10. Na poniższej ilustracji przedstawiono strukturę drzewa dla programu `myTree` .

![Diagram przedstawiający strukturę drzewa dla drzewa.](../media/discriminated-unions/tree-structure-mytree.png)

Związki rozłączne działają prawidłowo, jeśli węzły w drzewie są heterogeniczne. W poniższym kodzie typ `Expression` reprezentuje drzewo abstrakcyjnej składni wyrażenia w prostym języku programowania, który obsługuje dodawanie i mnożenie liczb i zmiennych. Niektóre przypadki Unii nie są cykliczne i reprezentują liczby ( `Number` ) lub zmienne ( `Variable` ). Inne przypadki są cykliczne i reprezentują operacje ( `Add` i `Multiply` ), gdzie operandy są również wyrażeniami. `Evaluate`Funkcja używa wyrażenia dopasowania, aby rekursywnie przetworzyć drzewo składni.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2006.fs)]

Gdy ten kod jest wykonywany, wartość jest równa `result` 5.

## <a name="members"></a>Elementy członkowskie

Istnieje możliwość zdefiniowania elementów członkowskich w Unii rozłącznych. Poniższy przykład pokazuje, jak zdefiniować Właściwość i zaimplementować interfejs:

```fsharp
open System

type IPrintable =
    abstract Print: unit -> unit

type Shape =
    | Circle of float
    | EquilateralTriangle of float
    | Square of float
    | Rectangle of float * float

    member this.Area =
        match this with
        | Circle r -> 2.0 * Math.PI * r
        | EquilateralTriangle s -> s * s * sqrt 3.0 / 4.0
        | Square s -> s * s
        | Rectangle(l, w) -> l * w

    interface IPrintable with
        member this.Print () =
            match this with
            | Circle r -> printfn $"Circle with radius %f{r}"
            | EquilateralTriangle s -> printfn $"Equilateral Triangle of side %f{s}"
            | Square s -> printfn $"Square with side %f{s}"
            | Rectangle(l, w) -> printfn $"Rectangle with length %f{l} and width %f{w}"
```

## <a name="common-attributes"></a>Atrybuty wspólne

Następujące atrybuty są często obserwowane w Unii rozłącznych:

- `[<RequireQualifiedAccess>]`
- `[<NoEquality>]`
- `[<NoComparison>]`
- `[<Struct>]`

## <a name="see-also"></a>Zobacz także

- [Dokumentacja języka F #](index.md)
