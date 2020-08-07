---
title: '! operator (null-łagodniejszej) — odwołanie w C#'
ms.date: 10/11/2019
f1_keywords:
- '!_CSharpKeyword'
helpviewer_keywords:
- null-forgiving operator [C#]
- '! operator [C#]'
ms.openlocfilehash: 5d8dcba5eb794d4d64f58e23a3ad952ef8055aeb
ms.sourcegitcommit: ef50c99928183a0bba75e07b9f22895cd4c480f8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/07/2020
ms.locfileid: "87916755"
---
# <a name="-null-forgiving-operator-c-reference"></a>! (null-łagodniejszej) — operator (odwołanie w C#)

Dostępne w języku C# 8,0 i nowszych, jednoargumentowy operator przyrostkowy `!` jest operatorem łagodniejszej o wartości null. W włączonym [kontekście dopuszczającym wartość null](../../nullable-references.md#nullable-annotation-context)należy użyć operatora null-łagodniejszej, aby zadeklarować wyrażenie `x` typu referencyjnego nie jest `null` : `x!` . Jednoargumentowy `!` operator prefiksu jest [logicznym operatorem negacji](boolean-logical-operators.md#logical-negation-operator-).

Operator null-łagodniejszej nie ma wpływu w czasie wykonywania. Ma wpływ tylko na analizę przepływu statycznego kompilatora przez zmianę stanu null wyrażenia. W czasie wykonywania wyrażenie `x!` oblicza wynik wyrażenia bazowego `x` .

> [!NOTE]
> W języku C# 8 operator łagodniejszej o wartości null kończy listę poprzednich operacji [warunkowych o wartości null](member-access-operators.md#null-conditional-operators--and-) . Na przykład wyrażenie `x?.y!.z` jest analizowane jako `(x?.y)!.z` . Ze względu na tę interpretację, `z` jest oceniane, nawet jeśli `x` jest `null` , co może skutkować <xref:System.NullReferenceException> .

Aby uzyskać więcej informacji na temat funkcji typów referencyjnych dopuszczających wartość null, zobacz [typy referencyjne dopuszczające wartość null](../builtin-types/nullable-reference-types.md).

## <a name="examples"></a>Przykłady

Jednym z przypadków użycia operatora null-łagodniejszej jest Testowanie logiki walidacji argumentów. Rozważmy na przykład następujące klasy:

[!code-csharp[Person class](snippets/shared/NullForgivingOperator.cs#PersonClass)]

Używając [platformy testów MSTest](../../../core/testing/unit-testing-with-mstest.md), można utworzyć następujący test dla logiki walidacji w konstruktorze:

[!code-csharp[Person test](snippets/shared/NullForgivingOperator.cs#TestPerson)]

Bez operatora null łagodniejszej kompilator generuje następujące ostrzeżenie dla poprzedniego kodu: `Warning CS8625: Cannot convert null literal to non-nullable reference type` . Za pomocą operatora null-łagodniejszej, należy poinformować kompilator, że `null` oczekiwano, i nie powinien być ostrzegany o.

Można również użyć operatora o wartości null-łagodniejszej, gdy wiadomo, że wyrażenie nie może być, `null` ale kompilator nie rozpoznaje tego elementu. W poniższym przykładzie, jeśli `IsValid` Metoda zwraca `true` , jego argument nie jest `null` i można bezpiecznie odwoływać się do niego:

[!code-csharp[Use null-forgiving operator](snippets/shared/NullForgivingOperator.cs#UseNullForgiving)]

Bez operatora null łagodniejszej kompilator generuje następujące ostrzeżenie dla `p.Name` kodu: `Warning CS8602: Dereference of a possibly null reference` .

Jeśli można zmodyfikować `IsValid` metodę, można użyć atrybutu [NotNullWhen](xref:System.Diagnostics.CodeAnalysis.NotNullWhenAttribute) do informowania kompilatora, że argument `IsValid` metody nie może być, `null` gdy metoda zwraca `true` :

[!code-csharp[Use an attribute](snippets/shared/NullForgivingOperator.cs#UseAttribute)]

W poprzednim przykładzie nie trzeba używać operatora o wartości null-łagodniejszej, ponieważ kompilator ma wystarczającą ilość informacji, aby dowiedzieć się, że `p` nie może znajdować się `null` wewnątrz `if` instrukcji. Aby uzyskać więcej informacji o atrybutach, które umożliwiają podanie dodatkowych informacji o stanie null zmiennej, zobacz [uaktualnianie interfejsów API z atrybutami w celu zdefiniowania oczekiwań o wartości null](../attributes/nullable-analysis.md).

## <a name="c-language-specification"></a>specyfikacja języka C#

Aby uzyskać więcej informacji, zobacz sekcję [operator null-łagodniejszej](~/_csharplang/proposals/csharp-8.0/nullable-reference-types-specification.md#the-null-forgiving-operator) w [wersji roboczej specyfikacji typów odwołań dopuszczających wartość null](~/_csharplang/proposals/csharp-8.0/nullable-reference-types-specification.md).

## <a name="see-also"></a>Zobacz także

- [Dokumentacja języka C#](../index.md)
- [Operatory i wyrażenia języka C#](index.md)
- [Samouczek: Projektowanie przy użyciu typów referencyjnych dopuszczających wartość null](../../tutorials/nullable-reference-types.md)
