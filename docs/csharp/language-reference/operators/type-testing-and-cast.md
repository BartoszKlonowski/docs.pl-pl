---
title: Operatory testowania typu i wyrażenie rzutowania — odwołanie w C#
description: Dowiedz się więcej na temat operatorów języka C#, których można użyć do sprawdzenia typu wyniku wyrażenia i przekonwertowania go na inny typ w razie potrzeby.
ms.date: 06/21/2019
author: pkulikov
f1_keywords:
- is_CSharpKeyword
- as_CSharpKeyword
- ()_CSharpKeyword
- typeof_CSharpKeyword
- as
- typeof
helpviewer_keywords:
- type-testing operators [C#]
- conversion operators [C#]
- type conversion [C#]
- is operator [C#]
- as operator [C#]
- cast operator [C#]
- cast expression [C#]
- () operator [C#]
- typeof operator [C#]
ms.openlocfilehash: 328a40f0213cbb55f86e16625507c1a5a5d775fb
ms.sourcegitcommit: c37e8d4642fef647ebab0e1c618ecc29ddfe2a0f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2020
ms.locfileid: "87855832"
---
# <a name="type-testing-operators-and-cast-expression-c-reference"></a>Operatory testowania typu i wyrażenie rzutowania (odwołanie w C#)

Można użyć następujących operatorów i wyrażeń do przeprowadzenia sprawdzania typu lub konwersji typu:

- [is — operator](#is-operator): Aby sprawdzić, czy typ środowiska uruchomieniowego wyrażenia jest zgodny z danym typem
- [operator as](#as-operator): Aby jawnie przekonwertować wyrażenie na dany typ, jeśli jego typ środowiska uruchomieniowego jest zgodny z tym typem
- [wyrażenie rzutowania](#cast-expression): Aby wykonać konwersję jawną
- [operator typeof](#typeof-operator): Aby uzyskać <xref:System.Type?displayProperty=nameWithType> wystąpienie dla typu

## <a name="is-operator"></a>IS — operator

`is`Operator sprawdza, czy typ środowiska uruchomieniowego wyniku wyrażenia jest zgodny z danym typem. Począwszy od języka C# 7,0, `is` operator sprawdza także wynik wyrażenia względem wzorca.

Wyrażenie z `is` operatorem testowania typu ma następującą postać

```csharp
E is T
```

gdzie `E` jest wyrażeniem zwracającym wartość i `T` jest nazwą typu lub parametrem typu. `E`nie może być metodą anonimową ani wyrażeniem lambda.

`E is T`Wyrażenie zwraca wartość, `true` Jeśli wynik `E` ma wartość inną niż null i można go przekonwertować na typ `T` za pomocą konwersji odwołania, konwersji pakującej lub konwersji rozpakowywania; w przeciwnym razie zwraca wartość `false` . `is`Operator nie uwzględnia konwersji zdefiniowanych przez użytkownika.

Poniższy przykład pokazuje, że `is` operator zwraca, `true` Jeśli typ środowiska uruchomieniowego wyniku wyrażenia pochodzi z danego typu, to oznacza, że istnieje konwersja odwołania między typami:

[!code-csharp[is with reference conversion](snippets/TypeTestingAndConversionOperators.cs#IsWithReferenceConversion)]

W następnym przykładzie pokazano, że `is` operator bierze pod uwagę opakowanie i konwersje rozpakowywanie, ale nie uwzględnia [konwersji liczbowych](../builtin-types/numeric-conversions.md):

[!code-csharp-interactive[is with int](snippets/TypeTestingAndConversionOperators.cs#IsWithInt)]

Aby uzyskać informacje na temat konwersji C#, zobacz rozdział dotyczący [konwersji](~/_csharplang/spec/conversions.md) [specyfikacji języka c#](~/_csharplang/spec/introduction.md).

### <a name="type-testing-with-pattern-matching"></a>Testowanie typu z dopasowaniem do wzorca

Począwszy od języka C# 7,0, `is` operator sprawdza także wynik wyrażenia względem wzorca. W szczególności obsługuje wzorzec typu w następującej postaci:

```csharp
E is T v
```

gdzie `E` jest wyrażeniem zwracającym wartość, `T` jest nazwą typu lub parametrem typu, a `v` to Nowa zmienna lokalna typu `T` . Jeśli wynik `E` jest inny niż null i można go przekonwertować na `T` za pomocą konwersji referencyjnej, pakującej lub rozpakowywania, `E is T v` wyrażenie zwraca `true` i przekonwertowaną wartość wyniku `E` jest przypisana do zmiennej `v` .

Poniższy przykład ilustruje użycie `is` operatora z wzorcem typu:

[!code-csharp-interactive[is with type pattern](snippets/TypeTestingAndConversionOperators.cs#IsTypePattern)]

Aby uzyskać więcej informacji na temat wzorca typu i innych obsługiwanych wzorców, zobacz [Dopasowanie wzorców do](../keywords/is.md#pattern-matching-with-is).

## <a name="as-operator"></a>operator as

`as`Operator jawnie konwertuje wynik wyrażenia na daną odwołanie lub typ wartości null. Jeśli konwersja nie jest możliwa, `as` operator zwraca `null` . W przeciwieństwie do [wyrażenia Cast](#cast-expression) `as` operator nigdy nie zgłasza wyjątku.

Wyrażenie formularza

```csharp
E as T
```

gdzie `E` jest wyrażeniem zwracającym wartość i `T` jest nazwą typu lub parametrem typu, daje ten sam wynik jako

```csharp
E is T ? (T)(E) : (T)null
```

z tą różnicą, że `E` jest obliczana tylko raz.

`as`Operator traktuje wyłącznie konwersje odwołania, dopuszczające wartość null, opakowanie i rozpakowywanie. Nie można użyć `as` operatora do wykonania konwersji zdefiniowanej przez użytkownika. W tym celu należy użyć [wyrażenia Cast](#cast-expression).

Poniższy przykład ilustruje użycie `as` operatora:

[!code-csharp-interactive[as operator](snippets/TypeTestingAndConversionOperators.cs#AsOperator)]

> [!NOTE]
> Jak pokazano na powyższym przykładzie, należy porównać wynik `as` wyrażenia z, `null` Aby sprawdzić, czy konwersja zakończyła się pomyślnie. Począwszy od języka C# 7,0, można użyć [operatora is](#type-testing-with-pattern-matching) , aby sprawdzić, czy konwersja się powiedzie i, jeśli zakończy się pomyślnie, przypisz wynik do nowej zmiennej.

## <a name="cast-expression"></a>Wyrażenie rzutowania

Wyrażenie rzutowania formularza `(T)E` wykonuje jawną konwersję wyniku wyrażenia `E` na typ `T` . Jeśli nie istnieje jawna konwersja z typu `E` do typu `T` , wystąpi błąd czasu kompilacji. W czasie wykonywania jawna konwersja może się nie powieść, a wyrażenie rzutowania może zgłosić wyjątek.

W poniższym przykładzie zademonstrowano jawne konwersje liczbowe i odwołania:

[!code-csharp-interactive[cast expression](snippets/TypeTestingAndConversionOperators.cs#Cast)]

Aby uzyskać informacje na temat obsługiwanych konwersji jawnych, zobacz sekcję [Konwersje jawne](~/_csharplang/spec/conversions.md#explicit-conversions) w [specyfikacji języka C#](~/_csharplang/spec/introduction.md). Aby uzyskać informacje dotyczące sposobu definiowania niestandardowej jawnej lub niejawnej konwersji typu, zobacz [Operatory konwersji zdefiniowane przez użytkownika](user-defined-conversion-operators.md).

### <a name="other-usages-of-"></a>Inne użycie ()

Należy również użyć nawiasów do [wywołania metody lub wywołania delegata](member-access-operators.md#invocation-expression-).

Innym zastosowaniem nawiasów jest dostosowanie kolejności, w której mają być oceniane operacje w wyrażeniu. Aby uzyskać więcej informacji, zobacz [operatory języka C#](index.md).

## <a name="typeof-operator"></a>typeof — Operator

`typeof`Operator uzyskuje <xref:System.Type?displayProperty=nameWithType> wystąpienie dla typu. Argument `typeof` operatora musi być nazwą typu lub parametrem typu, jak pokazano w poniższym przykładzie:

[!code-csharp-interactive[typeof operator](snippets/TypeTestingAndConversionOperators.cs#TypeOf)]

Można również użyć `typeof` operatora z niepowiązane typy ogólne. Nazwa niepowiązanego typu ogólnego musi zawierać odpowiednią liczbę przecinków, która jest mniejsza niż liczba parametrów typu. W poniższym przykładzie pokazano użycie `typeof` operatora z niezwiązanym typem ogólnym:

[!code-csharp-interactive[typeof unbound generic](snippets/TypeTestingAndConversionOperators.cs#TypeOfUnboundGeneric)]

Wyrażenie nie może być argumentem `typeof` operatora. Aby uzyskać <xref:System.Type?displayProperty=nameWithType> wystąpienie dla typu środowiska uruchomieniowego wyniku wyrażenia, użyj <xref:System.Object.GetType%2A?displayProperty=nameWithType> metody.

### <a name="type-testing-with-the-typeof-operator"></a>Testowanie typu za pomocą `typeof` operatora

Użyj `typeof` operatora, aby sprawdzić, czy typ środowiska uruchomieniowego wyniku wyrażenia dokładnie pasuje do danego typu. Poniższy przykład ilustruje różnicę między sprawdzaniem typu wykonane z `typeof` operatorem i [operatorem is](#is-operator):

[!code-csharp[typeof vs is](snippets/TypeTestingAndConversionOperators.cs#TypeCheckWithTypeOf)]

## <a name="operator-overloadability"></a>Przeciążanie operatora

`is`Operatory, `as` i `typeof` nie mogą być przeciążone.

Typ zdefiniowany przez użytkownika nie może przeciążać `()` operatora, ale może definiować konwersje typów niestandardowych, które mogą być wykonywane przez wyrażenie rzutowania. Aby uzyskać więcej informacji, zobacz [Operatory konwersji zdefiniowane przez użytkownika](user-defined-conversion-operators.md).

## <a name="c-language-specification"></a>specyfikacja języka C#

Aby uzyskać więcej informacji, zobacz następujące sekcje [specyfikacji języka C#](~/_csharplang/spec/introduction.md):

- [Operator is](~/_csharplang/spec/expressions.md#the-is-operator)
- [Operator as](~/_csharplang/spec/expressions.md#the-as-operator)
- [Wyrażenia rzutowania](~/_csharplang/spec/expressions.md#cast-expressions)
- [Operator typeof](~/_csharplang/spec/expressions.md#the-typeof-operator)

## <a name="see-also"></a>Zobacz także

- [Dokumentacja języka C#](../index.md)
- [Operatory i wyrażenia języka C#](index.md)
- [Jak bezpiecznie rzutować przy użyciu dopasowania wzorca i operatorów is i AS](../../how-to/safely-cast-using-pattern-matching-is-and-as-operators.md)
- [Typy ogólne w .NET](../../../standard/generics/index.md)
