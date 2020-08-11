---
title: Operatory i wyrażenia języka c# — odwołanie w C#
description: Więcej informacji na temat operatorów i wyrażeń języka C#, pierwszeństwa operatorów i łączność operatora
ms.date: 08/04/2020
f1_keywords:
- cs.operators
helpviewer_keywords:
- operators [C#]
- operator precedence [C#]
- operator associativity [C#]
- expressions [C#]
ms.assetid: 0301e31f-22ad-49af-ac3c-d5eae7f0ac43
ms.openlocfilehash: 854d7c1278319869104e1758ba91eb3594741126
ms.sourcegitcommit: 7476c20d2f911a834a00b8a7f5e8926bae6804d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/11/2020
ms.locfileid: "88063188"
---
# <a name="c-operators-and-expressions-c-reference"></a>Operatory i wyrażenia języka c# (odwołanie w C#)

Język C# zawiera wiele operatorów. Wiele z nich jest obsługiwanych przez [typy wbudowane](../builtin-types/built-in-types.md) i umożliwiają wykonywanie podstawowych operacji przy użyciu wartości tych typów. Te operatory obejmują następujące grupy:

- [Operatory arytmetyczne](arithmetic-operators.md) , które wykonują operacje arytmetyczne przy użyciu liczbowych argumentów operacji
- [Operatory porównania](comparison-operators.md) , które porównują argumenty operacji numerycznych
- Logiczne [operatorów logicznych](boolean-logical-operators.md) , które wykonują operacje logiczne z [`bool`](../builtin-types/bool.md) operandami
- [Operatory bitowe i przesunięcia](bitwise-and-shift-operators.md) , które wykonują operacje bitowe lub przesunięcia przy użyciu operandów typów całkowitych
- [Operatory równości](equality-operators.md) , które sprawdzają, czy ich operandy są równe

Zazwyczaj można [przeciążać](operator-overloading.md) te operatory, czyli określić zachowanie operatora dla argumentów operacji typu zdefiniowanego przez użytkownika.

Najprostszymi wyrażeniami języka C# są literały (na przykład liczby [całkowite](../builtin-types/integral-numeric-types.md#integer-literals) i [rzeczywiste](../builtin-types/floating-point-numeric-types.md#real-literals) ) oraz nazwy zmiennych. Można połączyć je w wyrażenia złożone przy użyciu operatorów. [Pierwszeństwo](#operator-precedence) operatorów i [łączność](#operator-associativity) określają kolejność wykonywania operacji w wyrażeniu. Możesz użyć nawiasów, aby zmienić kolejność oceny nałożona przez pierwszeństwo operatorów i łączność.

W poniższym kodzie Przykłady wyrażeń znajdują się po prawej stronie przypisań:

[!code-csharp[expression examples](snippets/shared/Overview.cs#Expressions)]

Zwykle wyrażenie generuje wynik i może być zawarte w innym wyrażeniu. [`void`](../builtin-types/void.md)Wywołanie metody jest przykładem wyrażenia, które nie tworzy wyniku. Może być używana tylko jako [instrukcja](../../programming-guide/statements-expressions-operators/statements.md), jak pokazano w poniższym przykładzie:

```csharp
Console.WriteLine("Hello, world!");
```

Poniżej przedstawiono niektóre inne rodzaje wyrażeń, które zapewnia język C#:

- [Interpolowane wyrażenia ciągów](../tokens/interpolated.md) , które zapewniają wygodną składnię do tworzenia sformatowanych ciągów:

  [!code-csharp-interactive[interpolated string](snippets/shared/Overview.cs#InterpolatedString)]

- [Wyrażenia lambda](lambda-expressions.md) , które umożliwiają tworzenie funkcji anonimowych:

  [!code-csharp-interactive[lambda expression](snippets/shared/Overview.cs#Lambda)]

- [Wyrażenia zapytań](../keywords/query-keywords.md) , które umożliwiają korzystanie z funkcji zapytań bezpośrednio w języku C#:

  [!code-csharp-interactive[query expression](snippets/shared/Overview.cs#Query)]

Możesz użyć [definicji treści wyrażenia](../../programming-guide/statements-expressions-operators/expression-bodied-members.md) , aby podać zwięzłą definicję dla metody, konstruktora, właściwości, indeksatora lub finalizatora.

## <a name="operator-precedence"></a>Pierwszeństwo operatorów

W wyrażeniu zawierającym wiele operatorów operatory o wyższym priorytecie są oceniane przed operatorami o niższym priorytecie. W poniższym przykładzie mnożenie jest wykonywane jako pierwsze, ponieważ ma wyższy priorytet niż dodanie:

```csharp-interactive
var a = 2 + 2 * 2;
Console.WriteLine(a); //  output: 6
```

Użyj nawiasów, aby zmienić kolejność oceny nałożona przez pierwszeństwo operatorów:

```csharp-interactive
var a = (2 + 2) * 2;
Console.WriteLine(a); //  output: 8
```

W poniższej tabeli wymieniono operatory języka C# zaczynające się od najwyższego priorytetu do najniższego. Operatory w każdym wierszu mają takie samo pierwszeństwo.

| Operatory | Kategoria lub nazwa |
| --------- | ---------------- |
| [x. y](member-access-operators.md#member-access-expression-), [f (x)](member-access-operators.md#invocation-expression-), [&#91;i&#93;](member-access-operators.md#indexer-operator-), [`x?.y`](member-access-operators.md#null-conditional-operators--and-) , [`x?[y]`](member-access-operators.md#null-conditional-operators--and-) , [x + +](arithmetic-operators.md#increment-operator-), [x--](arithmetic-operators.md#decrement-operator---), [x!](null-forgiving.md), [New](new-operator.md), [typeof](type-testing-and-cast.md#typeof-operator), [Checked](../keywords/checked.md), [unchecked](../keywords/unchecked.md), [default](default.md), [nameof](nameof.md), [Delegate](delegate-operator.md), [sizeof](sizeof.md), [stackalloc](stackalloc.md), [x->y](pointer-related-operators.md#pointer-member-access-operator--) | Podstawowe |
| [+ x](arithmetic-operators.md#unary-plus-and-minus-operators), [-x](arithmetic-operators.md#unary-plus-and-minus-operators), [ \! x](boolean-logical-operators.md#logical-negation-operator-), [~ x](bitwise-and-shift-operators.md#bitwise-complement-operator-), [+ + x](arithmetic-operators.md#increment-operator-), [--x](arithmetic-operators.md#decrement-operator---), [^ x](member-access-operators.md#index-from-end-operator-), [(T) x](type-testing-and-cast.md#cast-expression), [await](await.md), [&x](pointer-related-operators.md#address-of-operator-), [* x](pointer-related-operators.md#pointer-indirection-operator-), [true i false](true-false-operators.md) | Jednoargumentowy |
| [x.. t](member-access-operators.md#range-operator-) | Zakres |
| [switch](switch-expression.md) | `switch`wyrażenia |
| [x * y](arithmetic-operators.md#multiplication-operator-), [x/y](arithmetic-operators.md#division-operator-), [x% y](arithmetic-operators.md#remainder-operator-) | Mnożenie|
| [x + y](arithmetic-operators.md#addition-operator-), [x – y](arithmetic-operators.md#subtraction-operator--) | Dodawanie |
| [x \<\<  y](bitwise-and-shift-operators.md#left-shift-operator-), [x >> y](bitwise-and-shift-operators.md#right-shift-operator-) | Przesunięcia |
| [x \< y](comparison-operators.md#less-than-operator-), [x > y](comparison-operators.md#greater-than-operator-), [x \<= y](comparison-operators.md#less-than-or-equal-operator-), [x > = y](comparison-operators.md#greater-than-or-equal-operator-), [is](type-testing-and-cast.md#is-operator), [as](type-testing-and-cast.md#as-operator) | Relacyjne i testy typu |
| [x = = y](equality-operators.md#equality-operator-), [x! = y](equality-operators.md#inequality-operator-) | Równość |
| `x & y` | Koniunkcja logiczna logicznej [i](boolean-logical-operators.md#logical-and-operator-) [koniunkcji logicznej](bitwise-and-shift-operators.md#logical-and-operator-) |
| `x ^ y` | Logiczna logiczna [XOR](boolean-logical-operators.md#logical-exclusive-or-operator-) lub [KONIUNKCJa logiczna XOR](bitwise-and-shift-operators.md#logical-exclusive-or-operator-) |
| <code>x &#124; y</code> | Logiczna [logiczne or](boolean-logical-operators.md#logical-or-operator-) lub [bitowe logiczne lub](bitwise-and-shift-operators.md#logical-or-operator-) |
| [x && y](boolean-logical-operators.md#conditional-logical-and-operator-) | AND warunkowe |
| [x &#124;&#124; y](boolean-logical-operators.md#conditional-logical-or-operator-) | OR warunkowe |
| [x? t](null-coalescing-operator.md) | Operator łączenia wartości null |
| [s? t: f](conditional-operator.md) | Operator warunkowy |
| [x = y](assignment-operator.md), [x + = y](arithmetic-operators.md#compound-assignment), [x-= y](arithmetic-operators.md#compound-assignment), [x * = y](arithmetic-operators.md#compound-assignment), [x/= y](arithmetic-operators.md#compound-assignment), [x% = y](arithmetic-operators.md#compound-assignment), [x &=](boolean-logical-operators.md#compound-assignment)y, x [&#124;= y](boolean-logical-operators.md#compound-assignment), [x ^ =](boolean-logical-operators.md#compound-assignment)y, x [ <<= y](bitwise-and-shift-operators.md#compound-assignment), [x >>=](bitwise-and-shift-operators.md#compound-assignment)y, [x?? = y](null-coalescing-operator.md),[=>](lambda-operator.md) | Przypisanie i Deklaracja lambda |

## <a name="operator-associativity"></a>Łączność operatora

Gdy operatory mają takie samo pierwszeństwo, łączność operatorów określa kolejność wykonywania operacji:

- Operatory *kojarzenia w lewo* są oceniane w kolejności od lewej do prawej. Oprócz operatorów [przypisania](assignment-operator.md) i [operatorów łączenia wartości null](null-coalescing-operator.md)wszystkie operatory binarne są z lewej strony skojarzenia. Na przykład, `a + b - c` jest oceniane jako `(a + b) - c` .
- Operatory *kojarzenia w prawo* są oceniane w kolejności od prawej do lewej. Operatory przypisania, operatory łączenia wartości null i [ `?:` operator warunkowy](conditional-operator.md) są z prawej strony skojarzenia. Na przykład, `x = y = z` jest oceniane jako `x = (y = z)` .

Użyj nawiasów, aby zmienić kolejność oceny nałożona przez operator łączność:

```csharp-interactive
int a = 13 / 5 / 2;
int b = 13 / (5 / 2);
Console.WriteLine($"a = {a}, b = {b}");  // output: a = 1, b = 6
```

## <a name="operand-evaluation"></a>Obliczanie operandu

Niepowiązane z pierwszeństwem operatora i łączność, operandy w wyrażeniu są oceniane od lewej do prawej. W poniższych przykładach pokazano kolejność, w której są oceniane operatory i operandy:

| Wyrażenie | Kolejność obliczeń |
| ---------- | ------------------- |
|`a + b`|a, b, +|
|`a + b * c`|a, b, c, *, +|
|`a / b + c * d`|a, b,/, c, d, *, +|
|`a / (b + c) * d`|a, b, c, +,/, d, *|

Zazwyczaj są oceniane wszystkie operandy operatora. Jednak niektóre operatory jednocześnie obliczają operandy. Oznacza to, że wartość operandu z lewej strony takiego operatora definiuje, czy należy ocenić inne operandy. [Operatory te `||` ](boolean-logical-operators.md#conditional-logical-or-operator-) są warunkowymi operatorami [logicznymi i ( `&&` ](boolean-logical-operators.md#conditional-logical-and-operator-) ), [operatorami łączenia wartości null `??` oraz `??=` ](null-coalescing-operator.md) [operatorym `?.` `?[]` warunkowym null ](member-access-operators.md#null-conditional-operators--and-)i [operatorem `?:` warunkowym ](conditional-operator.md). Aby uzyskać więcej informacji, zobacz opis każdego operatora.

## <a name="c-language-specification"></a>specyfikacja języka C#

Aby uzyskać więcej informacji, zobacz następujące sekcje [specyfikacji języka C#](~/_csharplang/spec/introduction.md):

- [Wyrażenia](~/_csharplang/spec/expressions.md)
- [Operatory](~/_csharplang/spec/expressions.md#operators)

## <a name="see-also"></a>Zobacz także

- [Dokumentacja języka C#](../index.md)
- [Przeładowanie operatora](operator-overloading.md)
- [Drzewa wyrażeń](../../programming-guide/concepts/expression-trees/index.md)
