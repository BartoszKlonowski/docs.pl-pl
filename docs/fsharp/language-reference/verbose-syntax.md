---
title: Pełna składnia
description: Zapoznaj się z różnicą między pełną i uproszczoną F# składnią w języku programowania.
ms.date: 05/16/2016
ms.openlocfilehash: d2459da60bba5d88bd23615c8bf09ba64f7c22c4
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2019
ms.locfileid: "71214040"
---
# <a name="verbose-syntax"></a>Pełna składnia

Istnieją dwie formy składni dostępne dla wielu konstrukcji w F# języku: *Pełna składnia* i *składnia uproszczona*. Składnia verbose nie jest zgodna z powszechnie używanymi, ale ma zalety mniejszej czułości do wcięcia. Uproszczona składnia jest krótsza i używa wcięć do sygnalizowania początku i końca konstrukcji, zamiast dodatkowych słów kluczowych `begin` `in`, takich jak `end`,, i tak dalej. Domyślną składnią jest składnia uproszczona. W tym temacie opisano składnię F# dla konstrukcji, gdy nie jest włączona składnia uproszczona. Pełna składnia jest zawsze włączona, więc nawet w przypadku włączenia uproszczonej składni można nadal używać składni pełnej dla niektórych konstrukcji. Można wyłączyć składnię uproszczoną za pomocą `#light "off"` dyrektywy.

## <a name="table-of-constructs"></a>Tabela konstrukcji

W poniższej tabeli przedstawiono składnię uproszczoną i pełną dla F# konstrukcji języka w kontekstach, w których istnieje różnica między dwoma formularzami. W tej tabeli, nawiasy kątowe (&lt;&gt;) otaczają elementy składni dostarczone przez użytkownika. Zapoznaj się z dokumentacją dla każdej konstrukcji języka, aby uzyskać bardziej szczegółowe informacje na temat składni używanej w ramach tych konstrukcji.

<table>
<tr>
<th>Konstrukcja języka</th>
<th>Składnia uproszczona</th>
<th>Verbose — składnia</th>
</tr>
<tr>
<td>
wyrażenia złożone
</td>
<td>

```xml
<expression1>
<expression2>
```

</td><td>

```fsharp
<expression1>; <expression2>
```

</td>
</tr>
<tr><td>

powiązania `let` zagnieżdżone

</td><td>

```fsharp
let f x =
    let a = 1
    let b = 2
    x + a + b
```

</td><td>

```fsharp
let f x =
    let a = 1 in
    let b = 2 in
    x + a + b
```

</td>
</tr>
<tr><td>
blok kodu
</td><td>

```fsharp
(
    <expression1>
    <expression2>
)
```

</td><td>

```fsharp
begin
    <expression1>;
    <expression2>;
end
```

</td>
</tr>
<tr><td>
`for...do`
</td><td>

```fsharp
for counter = start to finish do
    ...
```

</td><td>

```fsharp
for counter = start to finish do
    ...
done
```

</td>
</tr>
<tr><td>
`while...do`
</td><td>

```fsharp
while <condition> do
    ...
```

</td><td>

```fsharp
while <condition> do
    ...
done
```

</td>
</tr>
<tr><td>
`for...in`
</td><td>

```fsharp
for var in start .. finish do
    ...
```

</td><td>

```fsharp
for var in start .. finish do
    ...
done
```

</td>
</tr>
<tr><td>
`do`
</td><td>

```fsharp
do
    ...
```

</td><td>

```fsharp
do
    ...
in
```

</td>
</tr>
<tr><td>record
</td><td>

```fsharp
type <record-name> =
    {
        <field-declarations>
    }
    <value-or-member-definitions>
```

</td><td>

```fsharp
type <record-name> =
    {
        <field-declarations>
    }
    with
        <value-or-member-definitions>
    end
```

</td>
</tr>
<tr><td>class
</td><td>

```fsharp
type <class-name>(<params>) =
    ...
```

</td><td>

```fsharp
type <class-name>(<params>) =
    class
        ...
    end
```

</td>
</tr>
<tr><td>— struktura</td><td>

```fsharp
[<StructAttribute>]
type <structure-name> =
    ...
```

</td><td>

```fsharp
type <structure-name> =
    struct
        ...
    end
```

</td>
</tr>
<tr><td>Unia rozłączna</td><td>

```fsharp
type <union-name> =
    | ...
    | ...
    ...
    <value-or-member definitions>
```

</td><td>

```fsharp
type <union-name> =
    | ...
    | ...
    ...
    with
        <value-or-member-definitions>
    end
```

</td>
</tr>
<tr><td>interface</td><td>

```fsharp
type <interface-name> =
    ...
```

</td><td>

```fsharp
type <interface-name> =
    interface
        ...
    end
```

</td>
</tr>
<tr><td>wyrażenie obiektu</td><td>

```fsharp
{ new <type-name>
    with
        <value-or-member-definitions>
        <interface-implementations>
}
```

</td><td>

```fsharp
{ new <type-name>
    with
        <value-or-member-definitions>
    end
    <interface-implementations>
}
```

</td>
</tr>
<tr><td>implementacja interfejsu</td><td>

```fsharp
interface <interface-name>
    with
        <value-or-member-definitions>
```

</td><td>

```fsharp
interface <interface-name>
    with
        <value-or-member-definitions>
    end
```

</td>
</tr>
<tr><td>rozszerzenie typu</td><td>

```fsharp
type <type-name>
    with
        <value-or-member-definitions>
```

</td><td>

```fsharp
type <type-name>
    with
        <value-or-member-definitions>
    end
```

</td>
</tr>
<tr><td>moduł</td><td>

```fsharp
module <module-name> =
    ...
```

</td><td>

```fsharp
module <module-name> =
    begin
        ...
    end
```

</td>
</tr>
</table>

## <a name="see-also"></a>Zobacz także

- [Dokumentacja języka F#](index.md)
- [Dyrektywy kompilatora](compiler-directives.md)
- [Wskazówki dotyczące formatowania kodu](code-formatting-guidelines.md)
