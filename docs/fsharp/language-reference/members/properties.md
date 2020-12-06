---
title: Właściwości
description: 'Informacje o właściwościach języka F #, które są elementami członkowskimi reprezentującymi wartości skojarzone z obiektem.'
ms.date: 05/16/2016
ms.openlocfilehash: a2a4fbfc88831dcb5cad7a2da701969b2e98b2e3
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96740201"
---
# <a name="properties"></a>Właściwości

*Właściwości* są elementami, które reprezentują wartości skojarzone z obiektem.

## <a name="syntax"></a>Składnia

```fsharp
// Property that has both get and set defined.
[ attributes ]
[ static ] member [accessibility-modifier] [self-identifier.]PropertyName
with [accessibility-modifier] get() =
    get-function-body
and [accessibility-modifier] set parameter =
    set-function-body

// Alternative syntax for a property that has get and set.
[ attributes-for-get ]
[ static ] member [accessibility-modifier-for-get] [self-identifier.]PropertyName =
    get-function-body
[ attributes-for-set ]
[ static ] member [accessibility-modifier-for-set] [self-identifier.]PropertyName
with set parameter =
    set-function-body

// Property that has get only.
[ attributes ]
[ static ] member [accessibility-modifier] [self-identifier.]PropertyName =
    get-function-body

// Alternative syntax for property that has get only.
[ attributes ]
[ static ] member [accessibility-modifier] [self-identifier.]PropertyName
with get() =
    get-function-body

// Property that has set only.
[ attributes ]
[ static ] member [accessibility-modifier] [self-identifier.]PropertyName
with set parameter =
    set-function-body

// Automatically implemented properties.
[ attributes ]
[ static ] member val [accessibility-modifier] PropertyName = initialization-expression [ with get, set ]
```

## <a name="remarks"></a>Uwagi

Właściwości reprezentują relację "ma" w programowaniu zorientowanym obiektowo, reprezentującą dane, które są skojarzone z wystąpieniami obiektów lub, dla właściwości statycznych z typem.

Możesz zadeklarować właściwości na dwa sposoby, w zależności od tego, czy chcesz jawnie określić wartość podstawową (nazywaną również magazynem zapasowym) dla właściwości, lub jeśli chcesz zezwolić kompilatorowi na automatyczne generowanie magazynu zapasowego. Ogólnie rzecz biorąc, należy użyć bardziej jawnej metody, jeśli właściwość ma nieprostą implementację i gdy właściwość to tylko prosta otoka dla wartości lub zmiennej. Aby jawnie zadeklarować właściwość, użyj `member` słowa kluczowego. W tej składni deklaratywnej następuje składnia, która określa `get` metody i `set` , nazywane także metodami *dostępu*. Różne formy jawnej składni pokazanej w sekcji składnia są używane do odczytu/zapisu, właściwości tylko do odczytu i zapisu. W przypadku właściwości tylko do odczytu należy zdefiniować tylko `get` metodę; dla właściwości tylko do zapisu należy zdefiniować tylko `set` metodę. Należy pamiętać, że gdy właściwość ma zarówno metody `get` `set` dostępu, jak i Akcesory, Alternatywna składnia pozwala określić atrybuty i Modyfikatory dostępności, które są różne dla każdego akcesora, jak pokazano w poniższym kodzie.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3201.fs)]

Dla właściwości odczytu/zapisu, które mają zarówno `get` `set` metodę, jak i, kolejność `get` i `set` można wycofać. Alternatywnie można podać składnię wyświetlaną tylko dla `get` i składnię wyświetlaną `set` tylko zamiast używać połączonej składni. Dzięki temu można łatwiej dodać komentarz do osoby `get` lub `set` metody, jeśli jest to coś, co może być konieczne. Alternatywą dla używania połączonej składni przedstawiono w poniższym kodzie.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3203.fs)]

Prywatne wartości przechowujące dane dla właściwości są nazywane *magazynami zapasowymi*. Aby kompilator automatycznie utworzył magazyn zapasowy, należy użyć słów kluczowych `member val` , pominąć samoidentyfikator, a następnie podać wyrażenie w celu zainicjowania właściwości. Jeśli właściwość ma być modyfikowalna, Dołącz `with get, set` . Na przykład następujący typ klasy obejmuje dwie automatycznie zaimplementowane właściwości. `Property1` jest tylko do odczytu i jest inicjowana do argumentu dostarczonego przez konstruktora podstawowego i `Property2` jest właściwością settable zainicjowaną do pustego ciągu:

```fsharp
type MyClass(property1 : int) =
member val Property1 = property1
member val Property2 = "" with get, set
```

Automatycznie implementowane właściwości są częścią inicjalizacji typu, dlatego muszą być zawarte przed innymi definicjami elementów członkowskich, podobnie jak `let` powiązania i `do` powiązania w definicji typu. Należy zauważyć, że wyrażenie inicjujące automatycznie implementowaną właściwość jest oceniane tylko po inicjacji, a nie za każdym razem, gdy właściwość jest używana. To zachowanie jest w przeciwieństwie do zachowania jawnie zaimplementowanej właściwości. To efektywnie oznacza, że kod, który ma inicjować te właściwości, jest dodawany do konstruktora klasy. Rozważmy następujący kod, który pokazuje tę różnicę:

```fsharp
type MyClass() =
    let random  = new System.Random()
    member val AutoProperty = random.Next() with get, set
    member this.ExplicitProperty = random.Next()

let class1 = new MyClass()

printfn $"class1.AutoProperty = %d{class1.AutoProperty}"
printfn $"class1.ExplicitProperty = %d{class1.ExplicitProperty}"
```

**Dane wyjściowe**

```console
class1.AutoProperty = 1853799794
class1.AutoProperty = 1853799794
class1.ExplicitProperty = 978922705
class1.ExplicitProperty = 1131210765
```

Dane wyjściowe powyższego kodu pokazują, że wartość właściwości autoproperty jest niezmieniona, gdy jest wywoływana wielokrotnie, podczas gdy ExplicitProperty ulega zmianie przy każdym wywołaniu. Pokazuje to, że wyrażenie dla automatycznie zaimplementowanej właściwości nie jest oceniane każdorazowo, podobnie jak metoda pobierająca dla właściwości explicit.

>[!WARNING]
>Istnieją pewne biblioteki, takie jak Entity Framework ( `System.Data.Entity` ), które wykonują niestandardowe operacje w konstruktorach klas podstawowych, które nie działają poprawnie z inicjowaniem automatycznie zaimplementowanych właściwości. W takich przypadkach spróbuj użyć jawnych właściwości.

Właściwości mogą być elementami członkowskimi klas, struktur, Unii rozłącznych, rekordów, interfejsów i rozszerzeń typów i mogą być również zdefiniowane w wyrażeniach obiektu.

Atrybuty mogą być stosowane do właściwości. Aby zastosować atrybut do właściwości, należy zapisać atrybut w osobnym wierszu przed właściwością. Aby uzyskać więcej informacji, zobacz [atrybuty](../attributes.md).

Domyślnie właściwości są publiczne. Modyfikatory dostępności można również stosować do właściwości. Aby zastosować modyfikator dostępności, należy dodać go bezpośrednio przed nazwą właściwości, jeśli ma zastosowanie do obu `get` `set` metod i; dodać go przed `get` `set` słowami kluczowymi i, jeśli dla każdego akcesora jest wymagana inna dostępność. *Modyfikator dostępności* może mieć jedną z następujących wartości: `public` , `private` , `internal` . Aby uzyskać więcej informacji, zobacz [Kontrola dostępu](../access-control.md).

Implementacje właściwości są wykonywane za każdym razem, gdy uzyskuje się dostęp do właściwości.

## <a name="static-and-instance-properties"></a>Właściwości statyczne i wystąpienia

Właściwości mogą być właściwościami statycznymi lub wystąpieniami. Właściwości statyczne mogą być wywoływane bez wystąpienia i są używane w przypadku wartości skojarzonych z typem, a nie z poszczególnymi obiektami. W przypadku właściwości statycznych Pomiń autoidentyfikator. Do właściwości wystąpienia są wymagane samoobsługowe identyfikatory.

Następująca Definicja właściwości statycznej jest oparta na scenariuszu, w którym istnieje pole statyczne `myStaticValue` , które jest magazynem zapasowym dla właściwości.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3204.fs)]

Właściwości mogą również być podobne do tablic, w tym przypadku są nazywane *indeksowanymi właściwościami*. Aby uzyskać więcej informacji, zobacz [indeksowane właściwości](indexed-properties.md).

## <a name="type-annotation-for-properties"></a>Adnotacja typu dla właściwości

W wielu przypadkach kompilator ma wystarczającą ilość informacji do wywnioskowania typu właściwości z typu magazynu zapasowego, ale można ustawić typ jawnie poprzez dodanie adnotacji typu.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3205.fs)]

## <a name="using-property-set-accessors"></a>Korzystanie z metod dostępu do ustawiania właściwości

Można ustawić właściwości, które zapewniają `set` metody dostępu przy użyciu `<-` operatora.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3206.fs)]

Wynik wynosi **20**.

## <a name="abstract-properties"></a>Właściwości abstrakcyjne

Właściwości mogą być abstrakcyjne. Podobnie jak w przypadku metod, `abstract` oznacza to, że istnieje wirtualna wysyłka skojarzona z właściwością. Właściwości abstrakcyjne mogą być prawdziwie abstrakcyjne, czyli bez definicji w tej samej klasie. Klasa, która zawiera taką właściwość, jest w związku z tym klasą abstrakcyjną. Alternatywnie abstrakcyjny może oznaczać, że właściwość jest wirtualna, a w takim przypadku definicja musi być obecna w tej samej klasie. Należy zauważyć, że właściwości abstrakcyjne nie mogą być prywatne i jeśli jedna metoda dostępu jest abstrakcyjna, druga musi również być abstrakcyjna. Aby uzyskać więcej informacji na temat klas abstrakcyjnych, zobacz [klasy abstrakcyjne](../abstract-classes.md).

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3207.fs)]

## <a name="see-also"></a>Zobacz także

- [Elementy członkowskie](index.md)
- [Metody](methods.md)
