---
title: Struktury
description: 'Dowiedz się więcej o strukturze języka F #, typ obiektu kompaktowego jest często bardziej wydajny niż Klasa dla typów z małą ilością danych i prostym zachowaniem.'
ms.date: 05/16/2016
ms.openlocfilehash: 1e9652cc4776e4d1d52eb20e41b6dd87a6c5ba05
ms.sourcegitcommit: 67ebdb695fd017d79d9f1f7f35d145042d5a37f7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/20/2020
ms.locfileid: "92223825"
---
# <a name="structures"></a>Struktury

*Struktura* jest typem obiektu kompaktowego, który może być bardziej wydajny niż Klasa dla typów, które mają niewielką ilość danych i proste zachowanie.

## <a name="syntax"></a>Składnia

```fsharp
[ attributes ]
type [accessibility-modifier] type-name =
    struct
        type-definition-elements-and-members
    end
// or
[ attributes ]
[<StructAttribute>]
type [accessibility-modifier] type-name =
    type-definition-elements-and-members
```

## <a name="remarks"></a>Uwagi

Struktury są *typami wartości*, co oznacza, że są przechowywane bezpośrednio na stosie lub, gdy są używane jako pola lub elementy tablicy, wbudowane w typie nadrzędnym. W przeciwieństwie do klas i rekordów struktury mają semantykę typu pass-by-Value. Oznacza to, że są one przydatne głównie w przypadku małych zagregowanych danych, do których często uzyskuje się dostęp i które są kopiowane.

W poprzedniej składni są wyświetlane dwa formularze. Pierwsza nie jest prostą składnią, ale jest Niemniej często używana, ponieważ przy użyciu `struct` `end` słów kluczowych i można pominąć ten `StructAttribute` atrybut, który pojawia się w drugim formularzu. Można skrócić `StructAttribute` do samego `Struct` .

*Definicja typu-elementy-i-Members* w poprzedniej składni reprezentuje deklaracje i definicje składowych. Struktury mogą mieć konstruktory i modyfikowalne i niezmienne pola oraz mogą deklarować elementy członkowskie i implementacje interfejsów. Aby uzyskać więcej informacji, zobacz [Członkowie](./members/index.md).

Struktury nie mogą uczestniczyć w dziedziczeniu, nie mogą zawierać `let` ani `do` powiązań ani rekursywnie zawierać pól własnego typu (chociaż mogą zawierać komórki odniesienia odwołujące się do własnego typu).

Ponieważ struktury nie zezwalają na `let` powiązania, należy zadeklarować pola w strukturach za pomocą `val` słowa kluczowego. `val`Słowo kluczowe definiuje pole i jego typ, ale nie zezwala na inicjalizację. Zamiast tego `val` deklaracje są inicjowane do zera lub wartości null. Z tego powodu struktury, które mają niejawny Konstruktor (czyli parametry, które są nadawane bezpośrednio po nazwie struktury w deklaracji), wymagają, aby `val` deklaracje miały adnotację z `DefaultValue` atrybutem. Struktury, które mają zdefiniowany Konstruktor nadal obsługują inicjowanie zerowe. W związku z tym `DefaultValue` atrybut jest deklaracją, że ta wartość zerowa jest prawidłowa dla pola. Niejawne konstruktory struktur nie wykonują żadnych akcji, ponieważ nie `let` `do` są dozwolone powiązania z typem, ale niejawne wartości parametrów konstruktora są dostępne jako pola prywatne.

Jawne konstruktory mogą polegać na inicjacji wartości pól. Jeśli masz strukturę, która ma jawny Konstruktor, nadal obsługuje inicjowanie zerujące; nie należy jednak używać `DefaultValue` atrybutu w `val` deklaracjach, ponieważ powoduje on konflikt z konstruktorem jawnym. Aby uzyskać więcej informacji na temat `val` deklaracji, zobacz [jawne pola: `val` słowo kluczowe](./members/explicit-fields-the-val-keyword.md).

Atrybuty i Modyfikatory dostępności są dozwolone w strukturach i są zgodne z tymi samymi regułami dla innych typów. Aby uzyskać więcej informacji, zobacz [atrybuty](attributes.md) i [Access Control](access-control.md).

Poniższe przykłady kodu ilustrują definicje struktury.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2501.fs)]

## <a name="byreflike-structs"></a>Struktury ByRefLike

Można definiować własne struktury, które mogą przestrzegać `byref` podobnej semantyki: Aby uzyskać więcej informacji, zobacz [ByRef](byrefs.md) . Jest to realizowane z <xref:System.Runtime.CompilerServices.IsByRefLikeAttribute> atrybutem:

```fsharp
open System
open System.Runtime.CompilerServices

[<IsByRefLike; Struct>]
type S(count1: Span<int>, count2: Span<int>) =
    member x.Count1 = count1
    member x.Count2 = count2
```

`IsByRefLike` nie oznacza `Struct` . Oba muszą być obecne w typie.

Struktura " `byref` like" w języku F # jest typem wartości powiązanej ze stosem. Nigdy nie jest przydzielany na zarządzanym stosie. `byref`Struktura przypominająca podobne rozwiązanie jest przydatna w programowaniu o wysokiej wydajności, ponieważ jest wymuszana z zestawem silnych sprawdzeń i bez przechwycenia. Reguły są następujące:

- Mogą one być używane jako parametry funkcji, parametry metody, zmienne lokalne, Metoda Return.
- Nie mogą być statyczne ani składowe wystąpień klasy ani normalnej struktury.
- Nie mogą być przechwytywane przez żadną konstrukcję zamknięcia ( `async` metody lub wyrażenia lambda).
- Nie mogą być używane jako parametr generyczny.

Chociaż te reguły bardzo zdecydowanie ograniczają użycie, robią to w celu zapewnienia bezpieczeństwa obliczeń o wysokiej wydajności w bezpieczny sposób.

## <a name="readonly-structs"></a>Struktury tylko do odczytu

Można dodawać adnotacje do struktur przy użyciu <xref:System.Runtime.CompilerServices.IsReadOnlyAttribute> atrybutu. Na przykład:

```fsharp
[<IsReadOnly; Struct>]
type S(count1: int, count2: int) =
    member x.Count1 = count1
    member x.Count2 = count2
```

`IsReadOnly` nie oznacza `Struct` . Musisz dodać oba, aby mieć `IsReadOnly` strukturę.

Użycie tego atrybutu emituje metadane, dzięki czemu F # i C# wiedzą, że odpowiednio traktuje ją jako `inref<'T>` i `in ref` .

Zdefiniowanie wartości modyfikowalnej wewnątrz struktury tylko do odczytu powoduje wystąpienie błędu.

## <a name="struct-records-and-discriminated-unions"></a>Rekordy struktury i związki rozłącznych

[Rekordy](records.md) i [związki rozłącznych](discriminated-unions.md) można reprezentować jako struktury z `[<Struct>]` atrybutem.  Aby dowiedzieć się więcej, zobacz każdy artykuł.

## <a name="see-also"></a>Zobacz też

- [Dokumentacja języka F #](index.md)
- [Klasy](classes.md)
- [Rekordy](records.md)
- [Elementy członkowskie](./members/index.md)
