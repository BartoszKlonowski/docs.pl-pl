---
title: Operatory równości — odwołanie w C#
description: Dowiedz się więcej na temat operatorów porównania równości języka C# i równości typów języka C#.
ms.date: 10/30/2020
author: pkulikov
f1_keywords:
- ==_CSharpKeyword
- '!=_CSharpKeyword'
helpviewer_keywords:
- comparison operators [C#]
- relational operators [C#]
- equality operator [C#]
- equals operator [C#]
- == operator [C#]
- inequality operator [C#]
- not equals operator [C#]
- '!= operator [C#]'
ms.openlocfilehash: 39461157c33fea0effb5c8808ded1c9981900e17
ms.sourcegitcommit: b1442669f1982d3a1cb18ea35b5acfb0fc7d93e4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2020
ms.locfileid: "93063218"
---
# <a name="equality-operators-c-reference"></a>Operatory równości (odwołanie w C#)

Operatory [ `==` (równość)](#equality-operator-) i [ `!=` (nierówność)](#inequality-operator-) sprawdzają, czy ich operandy są równe, czy nie.

## <a name="equality-operator-"></a>Operator równości = =

Operator równości `==` zwraca `true` , jeśli jego operandy są równe, `false` w przeciwnym razie.

### <a name="value-types-equality"></a>Równość typów wartości

Argumenty operacji [wbudowanych typów wartości](../builtin-types/value-types.md#built-in-value-types) są równe, jeśli ich wartości są równe:

[!code-csharp-interactive[value types equality](snippets/shared/EqualityOperators.cs#ValueTypesEquality)]

> [!NOTE]
> Dla `==` operatorów, [ `<` , `>` , `<=` i `>=` ](comparison-operators.md) , jeśli którykolwiek z operandów nie jest liczbą ( <xref:System.Double.NaN?displayProperty=nameWithType> lub <xref:System.Single.NaN?displayProperty=nameWithType> ), wynikiem operacji jest `false` . Oznacza to, że `NaN` wartość nie jest większa niż, mniejsza niż ani równa żadnej innej `double` wartości (lub `float` ), w tym `NaN` . Aby uzyskać więcej informacji i przykładów, zobacz <xref:System.Double.NaN?displayProperty=nameWithType> <xref:System.Single.NaN?displayProperty=nameWithType> artykuł lub dokumentacja.

Dwa operandy tego samego typu [wyliczeniowego](../builtin-types/enum.md) są równe, jeśli odpowiadające wartości bazowego typu całkowitego są równe.

Zdefiniowane przez użytkownika typy [struktur](../builtin-types/struct.md) nie obsługują `==` operatora domyślnie. Aby zapewnić obsługę `==` operatora, struktura zdefiniowana przez użytkownika musi [przeciążać](operator-overloading.md) ją.

Począwszy od języka C# 7,3 `==` Operatory i `!=` są obsługiwane przez [krotki](../builtin-types/value-tuples.md)języka c#. Aby uzyskać więcej informacji, zobacz sekcję [równość krotki](../builtin-types/value-tuples.md#tuple-equality) w artykule [typy krotek](../builtin-types/value-tuples.md) .

### <a name="reference-types-equality"></a>Równość typów referencyjnych

Domyślnie dwa operandy typu odwołania, które nie są rekordami, są równe, jeśli odwołują się do tego samego obiektu:

[!code-csharp[reference type equality](snippets/shared/EqualityOperators.cs#ReferenceTypesEquality)]

Jak pokazano na przykładzie, zdefiniowane przez użytkownika typy odwołań domyślnie obsługują `==` operatora. Jednak typ referencyjny może przeciążać `==` operator. Jeśli typ referencyjny przeciąża `==` operatora, użyj <xref:System.Object.ReferenceEquals%2A?displayProperty=nameWithType> metody, aby sprawdzić, czy dwa odwołania tego typu odwołują się do tego samego obiektu.

### <a name="record-types-equality"></a>Równość typów rekordów

W języku C# 9,0 i nowszych [typy rekordów](../../whats-new/csharp-9.md#record-types) obsługują `==` `!=` Operatory i, które domyślnie udostępniają semantykę równości wartości. Oznacza to, że dwa operandy rekordu są równe, gdy oba z nich są `null` lub odpowiadające wartości wszystkich pól i właściwości zaimplementowane domyślnie są równe.

:::code language="csharp" source="snippets/shared/EqualityOperators.cs" id="RecordTypesEquality":::

Jak pokazano w powyższym przykładzie, w przypadku odwołań nienależących do rekordów, ich wartości odniesienia są porównywane, a nie wystąpienia przywoływane.

### <a name="string-equality"></a>Równość ciągów

Dwa operandy [ciągu](../builtin-types/reference-types.md#the-string-type) są równe, gdy oba z nich są `null` lub oba wystąpienia ciągu mają taką samą długość i mają identyczne znaki w każdej pozycji znaku:

[!code-csharp-interactive[string equality](snippets/shared/EqualityOperators.cs#StringEquality)]

Jest to porównanie porządkowe z uwzględnieniem wielkości liter. Aby uzyskać więcej informacji na temat porównywania ciągów, zobacz [Jak porównać ciągi w języku C#](../../how-to/compare-strings.md).

### <a name="delegate-equality"></a>Równość delegowania

Dwa operandy [delegatów](../../programming-guide/delegates/index.md) tego samego typu środowiska uruchomieniowego są równe, gdy oba z nich są `null` lub ich listy wywołań mają taką samą długość i mają równe wpisy w każdej pozycji:

[!code-csharp-interactive[delegate equality](snippets/shared/EqualityOperators.cs#DelegateEquality)]

Aby uzyskać więcej informacji, zobacz sekcję [delegowanie operatorów równości](~/_csharplang/spec/expressions.md#delegate-equality-operators) w [specyfikacji języka C#](~/_csharplang/spec/introduction.md).

Delegaty wytwarzane z oceny semantycznie identycznych [wyrażeń lambda](lambda-expressions.md) nie są równe, jak pokazano w poniższym przykładzie:

[!code-csharp-interactive[from identical lambdas](snippets/shared/EqualityOperators.cs#IdenticalLambdas)]

## <a name="inequality-operator-"></a>Operator nierówności! =

Operator nierówności `!=` zwraca `true` , jeśli jego operandy nie są równe `false` . w przeciwnym razie. W przypadku operandów [typów wbudowanych](../builtin-types/built-in-types.md)wyrażenie `x != y` daje ten sam wynik co wyrażenie `!(x == y)` . Aby uzyskać więcej informacji na temat równości typów, zobacz sekcję [operator równości](#equality-operator-) .

Poniższy przykład ilustruje użycie `!=` operatora:

[!code-csharp-interactive[non-equality examples](snippets/shared/EqualityOperators.cs#NonEquality)]

## <a name="operator-overloadability"></a>Przeciążanie operatora

Typ zdefiniowany przez użytkownika może [przeciążać](operator-overloading.md) `==` `!=` Operatory i. Jeśli typ przeciąża jeden z dwóch operatorów, musi on również przeciążać pozostałe.

Typ rekordu nie może jawnie przeciążać `==` `!=` operatorów i. Jeśli musisz zmienić zachowanie `==` `!=` operatorów i dla typu rekordu `T` , zaimplementuj <xref:System.IEquatable%601.Equals%2A?displayProperty=nameWithType> metodę następującym podpisem:

```csharp
public virtual bool Equals(T? other);
```

## <a name="c-language-specification"></a>specyfikacja języka C#

Aby uzyskać więcej informacji, zobacz sekcję [Operatory relacyjne i testowe typu](~/_csharplang/spec/expressions.md#relational-and-type-testing-operators) w [specyfikacji języka C#](~/_csharplang/spec/introduction.md).

Aby uzyskać więcej informacji na temat równości typów rekordów, zobacz sekcję z [członkami równości](~/_csharplang/proposals/csharp-9.0/records.md#equality-members) w temacie [Records propozycja funkcji](~/_csharplang/proposals/csharp-9.0/records.md).

## <a name="see-also"></a>Zobacz też

- [Dokumentacja języka C#](../index.md)
- [Operatory i wyrażenia języka C#](index.md)
- <xref:System.IEquatable%601?displayProperty=nameWithType>
- <xref:System.Object.Equals%2A?displayProperty=nameWithType>
- <xref:System.Object.ReferenceEquals%2A?displayProperty=nameWithType>
- [Porównywanie równości](../../programming-guide/statements-expressions-operators/equality-comparisons.md)
- [Operatory porównania](comparison-operators.md)
