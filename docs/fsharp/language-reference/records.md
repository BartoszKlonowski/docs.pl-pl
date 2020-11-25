---
title: Rekordy
description: 'Dowiedz się, w jaki sposób rekordy F # reprezentują proste agregowanie nazwanych wartości, opcjonalnie z elementami członkowskimi.'
ms.date: 08/15/2020
ms.openlocfilehash: 03de96b9c53bc21e7a7723a15d2a8451d100ba76
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95682032"
---
# <a name="records"></a>Rekordy

Rekordy reprezentują proste Agregowanie wartości nazwanych, opcjonalnie z elementami członkowskimi. Mogą to być struktury lub typy referencyjne.  Domyślnie są to typy odwołań.

## <a name="syntax"></a>Składnia

```fsharp
[ attributes ]
type [accessibility-modifier] typename =
    { [ mutable ] label1 : type1;
      [ mutable ] label2 : type2;
      ... }
    [ member-list ]
```

## <a name="remarks"></a>Uwagi

W poprzedniej składni, *TypeName* jest nazwą typu rekordu, *Label1* i *etykiety 2* są nazwami wartości, zwanymi *etykietami*, a *Type1* i *Type2* są typami tych wartości. *Lista elementów członkowskich* jest opcjonalną listą elementów członkowskich typu.  Możesz użyć atrybutu, `[<Struct>]` Aby utworzyć rekord struktury, a nie rekord, który jest typem referencyjnym.

Poniżej przedstawiono kilka przykładów.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1901.fs)]

Gdy każda etykieta znajduje się w osobnym wierszu, średnik jest opcjonalny.

Można ustawić wartości w wyrażeniach nazywanych *wyrażeniami rekordów*. Kompilator wnioskuje typ z użytych etykiet (Jeśli etykiety są wystarczająco odrębne od tych z innych typów rekordów). Nawiasy klamrowe ({}) otaczają wyrażenie rekordu. Poniższy kod przedstawia wyrażenie rekordu, które inicjuje rekord z trzema elementami zmiennoprzecinkowymi z etykietami `x` `y` i `z` .

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1907.fs)]

Nie używaj skróconej formy, jeśli może istnieć inny typ, który ma również te same etykiety.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1903.fs)]

Etykiety ostatnio zadeklarowanego typu mają pierwszeństwo przed poprzednimi zadeklarowanymi typem, więc w poprzednim przykładzie `mypoint3D` jest wywnioskowane `Point3D` . Można jawnie określić typ rekordu, jak w poniższym kodzie.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1908.fs)]

Metody można definiować dla typów rekordów, tak jak w przypadku typów klas.

## <a name="creating-records-by-using-record-expressions"></a>Tworzenie rekordów przy użyciu wyrażeń rekordu

Rekordy można inicjować przy użyciu etykiet, które są zdefiniowane w rekordzie. Wyrażenie, które jest nazywane *wyrażeniem rekordu*. Użyj nawiasów klamrowych, aby ująć wyrażenie rekordu i użyć średnika jako ogranicznika.

Poniższy przykład pokazuje, jak utworzyć rekord.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1904.fs)]

Średniki po ostatnim polu w wyrażeniu rekordu i w definicji typu są opcjonalne, bez względu na to, czy wszystkie pola znajdują się w jednym wierszu.

Podczas tworzenia rekordu należy podać wartości dla każdego pola. Nie można odwołać się do wartości innych pól w wyrażeniu inicjalizacji dla każdego pola.

W poniższym kodzie typ `myRecord2` jest wywnioskowany na podstawie nazw pól. Opcjonalnie można jawnie określić nazwę typu.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1905.fs)]

Inna forma konstruowania rekordów może być przydatna, gdy trzeba skopiować istniejący rekord i ewentualnie zmienić niektóre wartości pól. Ilustruje to poniższy wiersz kodu.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1906.fs)]

Ta forma wyrażenia rekordu jest nazywana *wyrażeniem Copy i Update Record*.

Rekordy są domyślnie niezmienne; można jednak łatwo tworzyć zmodyfikowane rekordy przy użyciu wyrażenia Copy i Update. Można również jawnie określić pole modyfikowalne.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1909.fs)]

Nie używaj atrybutu DefaultValue z polami rekordów. Lepszym rozwiązaniem jest zdefiniowanie domyślnych wystąpień rekordów z polami, które są inicjowane do wartości domyślnych, a następnie użycie wyrażenia Kopiuj i Aktualizuj rekord, aby ustawić wszystkie pola, które różnią się od wartości domyślnych.

```fsharp
// Rather than use [<DefaultValue>], define a default record.
type MyRecord =
    { Field1 : int
      Field2 : int }

let defaultRecord1 = { Field1 = 0; Field2 = 0 }
let defaultRecord2 = { Field1 = 1; Field2 = 25 }

// Use the with keyword to populate only a few chosen fields
// and leave the rest with default values.
let rr3 = { defaultRecord1 with Field2 = 42 }
```

## <a name="creating-mutually-recursive-records"></a>Tworzenie wzajemnie rekurencyjnych rekordów

Czasami podczas tworzenia rekordu można zależeć od innego typu, który ma zostać zdefiniowany później. Jest to błąd kompilacji, chyba że zostanie zdefiniowany typ rekordu, który ma być wzajemnie cykliczne.

Definiowanie wzajemnie cyklicznych rekordów odbywa się za pomocą `and` słowa kluczowego. Dzięki temu można połączyć 2 lub więcej typów rekordów jednocześnie.

Na przykład poniższy kod definiuje a `Person` i `Address` Typ jako wzajemnie cyklicznie:

```fsharp
// Create a Person type and use the Address type that is not defined
type Person =
  { Name: string
    Age: int
    Address: Address }
// Define the Address type which is used in the Person record
and Address =
  { Line1: string
    Line2: string
    PostCode: string
    Occupant: Person }
```

Jeśli zdefiniowano poprzedni przykład bez `and` słowa kluczowego, nie zostanie on skompilowany. `and`Słowo kluczowe jest wymagane dla wzajemnie cyklicznych definicji.

## <a name="pattern-matching-with-records"></a>Dopasowanie wzorca z rekordami

Rekordy mogą być używane z dopasowywaniem do wzorca. Niektóre pola można określić jawnie i podać zmienne dla innych pól, które będą przypisywane w przypadku wystąpienia dopasowania. Pokazano to w poniższym przykładzie kodu.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1910.fs)]

Dane wyjściowe tego kodu są następujące.

```console
Point is at the origin.
Point is on the x-axis. Value is 100.000000.
Point is at (10.000000, 0.000000, -1.000000).
```

## <a name="records-and-members"></a>Rekordy i elementy członkowskie

Możesz określić elementy członkowskie dla rekordów, tak jak w przypadku klas. Nie ma obsługi dla pól. Typowym podejściem jest zdefiniowanie `Default` statycznej składowej w celu łatwego konstruowania rekordów:

```fsharp
type Person =
  { Name: string
    Age: int
    Address: string }

    static member Default =
        { Name = "Phillip"
          Age = 12
          Address = "123 happy fun street" }

let defaultPerson = Person.Default
```

Jeśli używasz samego identyfikatora, identyfikator ten odnosi się do wystąpienia rekordu, którego Członek jest wywoływany:

```fsharp
type Person =
  { Name: string
    Age: int
    Address: string }

    member this.WeirdToString() =
        this.Name + this.Address + string this.Age

let p = { Name = "a"; Age = 12; Address = "abc123" }
let weirdString = p.WeirdToString()
```

## <a name="differences-between-records-and-classes"></a>Różnice między rekordami i klasami

Pola rekordów różnią się od klas, które są automatycznie uwidaczniane jako właściwości i są używane podczas tworzenia i kopiowania rekordów. Konstrukcja rekordu różni się także od konstrukcji klasy. W typie rekordu nie można zdefiniować konstruktora. Zamiast tego stosuje się składnię konstrukcyjną opisaną w tym temacie. Klasy nie mają bezpośredniej relacji między parametrami konstruktora, polami i właściwościami.

Podobnie jak w przypadku typów Unii i struktury, rekordy mają semantykę równości strukturalnej. Klasy mają semantykę równości odwołań. Poniższy przykład kodu demonstruje ten sposób.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1911.fs)]

Dane wyjściowe tego kodu są następujące:

```console
The records are equal.
```

Jeśli piszesz ten sam kod z klasami, obiekty obu klas byłyby nierówne, ponieważ dwie wartości przedstawiają dwa obiekty na stercie i porównywane są tylko te adresy (chyba że typ klasy zastępuje `System.Object.Equals` metodę).

Jeśli potrzebujesz równości odwołań dla rekordów, Dodaj atrybut `[<ReferenceEquality>]` powyżej rekordu.

## <a name="see-also"></a>Zobacz też

- [Typy F#](fsharp-types.md)
- [Klasy](classes.md)
- [Dokumentacja języka F #](index.md)
- [Odwołanie — równość](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-referenceequalityattribute.html)
- [Dopasowanie wzorca](pattern-matching.md)
