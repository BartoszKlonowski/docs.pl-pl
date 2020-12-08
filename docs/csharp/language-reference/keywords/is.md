---
description: jest odwołaniem do języka C#
title: jest odwołaniem do języka C#
ms.date: 06/21/2019
f1_keywords:
- is_CSharpKeyword
- is
helpviewer_keywords:
- is keyword [C#]
ms.assetid: bc62316a-d41f-4f90-8300-c6f4f0556e43
ms.openlocfilehash: c38649a9e3b3f75ec35fb8711324302a682b504e
ms.sourcegitcommit: 45c7148f2483db2501c1aa696ab6ed2ed8cb71b2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/08/2020
ms.locfileid: "96851337"
---
# <a name="is-c-reference"></a>is (odwołanie w C#)

`is`Operator sprawdza, czy wynik wyrażenia jest zgodny z danym typem, lub (począwszy od języka C# 7,0) testuje wyrażenie względem wzorca. Aby uzyskać informacje na temat operatora testowania typu `is` , zobacz sekcję [is operatora](../operators/type-testing-and-cast.md#is-operator) w artykule operatorion [-Test and Cast](../operators/type-testing-and-cast.md) .

## <a name="pattern-matching-with-is"></a>Dopasowanie wzorca z `is`

Począwszy od języka C# 7,0 `is` instrukcje i [przełącznik](switch.md) obsługują Dopasowywanie wzorców. `is`Słowo kluczowe obsługuje następujące wzorce:

- [Wzorzec typu](#type-pattern), który sprawdza, czy wyrażenie może być konwertowane na określony typ i, jeśli to możliwe, rzutuje zmienną do zmiennej tego typu.
- [Wzorzec stałej](#constant-pattern), który sprawdza, czy wyrażenie daje w wyniku określoną wartość stałą.
- [wzorzec var](#var-pattern), dopasowanie, które zawsze powiedzie się i wiąże wartość wyrażenia z nową zmienną lokalną.

### <a name="type-pattern"></a>Wzorzec typu

W przypadku używania wzorca typu do dopasowania do wzorca, `is` sprawdza, czy wyrażenie może być konwertowane do określonego typu i, jeśli może, rzutowania go na zmienną tego typu. Jest to proste rozszerzenie `is` instrukcji, która umożliwia obliczanie i konwersję typu zwięzłego. Ogólna forma `is` wzorca typu jest:

```csharp
expr is type varname
```

Gdzie *Expr* jest wyrażeniem, którego wynikiem jest wystąpienie pewnego typu, *Type* jest nazwą typu, do którego zostanie przekonwertowany wynik *wyrażenia* , a *nazwa_zmiennej* jest obiektem, do którego wynik *wyrażenia* jest konwertowany, jeśli `is` test jest `true` .

`is`Wyrażenie jest `true` , jeśli *wyrażenie* nie jest `null` , i spełniony jest dowolny z następujących warunków:

- *wyrażenie* jest wystąpieniem tego samego typu co *Typ*.
- *wyrażenie* jest wystąpieniem typu, który pochodzi od *typu*. Innymi słowy, wynik *wyrażenia* może być rzutowany na wystąpienie *typu*.
- *wyrażenie* ma typ czasu kompilacji, który jest klasą bazową *typu*, a *wyrażenie* ma typ środowiska uruchomieniowego, który jest *typem* lub pochodzi od *typu*. *Typ czasu kompilacji* zmiennej to typ zmiennej, zgodnie z definicją w swojej deklaracji. *Typ środowiska uruchomieniowego* zmiennej to typ wystąpienia, które jest przypisane do tej zmiennej.
- *wyrażenie* jest wystąpieniem typu, który implementuje interfejs *typu* .

Począwszy od języka C# 7,1, *wyrażenie* może mieć typ czasu kompilacji zdefiniowany przez parametr typu ogólnego i jego ograniczenia.

Jeśli *wyrażenie* jest `true` i `is` jest używane z `if` instrukcją, *nazwa_zmiennej* jest przypisywana `if` tylko wewnątrz instrukcji. Zakres elementu *nazwa_zmiennej* pochodzi z `is` wyrażenia na końcu bloku otaczającego `if` instrukcję. Użycie elementu *nazwa_zmiennej* w innej lokalizacji powoduje wygenerowanie błędu czasu kompilacji w celu użycia zmiennej, która nie została przypisana.

Poniższy przykład używa `is` wzorca typu, aby zapewnić implementację <xref:System.IComparable.CompareTo(System.Object)?displayProperty=nameWithType> metody typu.

[!code-csharp[is#5](../../../../samples/snippets/csharp/language-reference/keywords/is/is-type-pattern5.cs#5)]

Bez dopasowania do wzorca ten kod może być zapisany w następujący sposób. Użycie dopasowania wzorca typu daje bardziej zwarty, czytelny kod, eliminując konieczność sprawdzenia, czy wynik konwersji to `null` .  

[!code-csharp[is#6](../../../../samples/snippets/csharp/language-reference/keywords/is/is-type-pattern6.cs#6)]

`is`Wzorzec typu generuje również bardziej zwarty kod podczas określania typu wartości. W poniższym przykładzie używa się `is` wzorca typu, aby określić, czy obiekt jest `Person` `Dog` wystąpieniem, czy przed wyświetleniem wartości odpowiedniej właściwości.

[!code-csharp[is#9](../../../../samples/snippets/csharp/language-reference/keywords/is/is-type-pattern9.cs#9)]

Odpowiedni kod bez dopasowania do wzorca wymaga oddzielnego przypisania zawierającego jawne rzutowanie.

[!code-csharp[is#10](../../../../samples/snippets/csharp/language-reference/keywords/is/is-type-pattern10.cs#10)]

### <a name="constant-pattern"></a>Wzorzec stałej

Podczas wykonywania dopasowania wzorca ze wzorcem stałej, `is` sprawdza, czy wyrażenie jest równe określonej stałej. W języku C# 6 i wcześniejszych wersjach wzorzec stałej jest obsługiwany przez instrukcję [Switch](switch.md) . Począwszy od języka C# 7,0, jest to również obsługiwane przez `is` instrukcję. Jego składnia to:

```csharp
   expr is constant
```

gdzie *Expr* jest wyrażeniem, które ma zostać obliczone, a *stała* jest wartością do przetestowania. *stała* może być dowolnym z następujących wyrażeń stałych:

- Wartość literału.

- Nazwa zadeklarowanej `const` zmiennej.

- Stała wyliczenia.

Wyrażenie stałe jest oceniane w następujący sposób:

- Jeśli *wyrażenie* i *stała* są typami całkowitymi, operator równości języka C# określa, czy wyrażenie zwróci wartość `true` (to znaczy czy `expr == constant` ).

- W przeciwnym razie wartość wyrażenia jest określana przez wywołanie metody static [obiektu. Equals (wyrażenie, stała)](xref:System.Object.Equals(System.Object,System.Object)) .  

Poniższy przykład łączy typ i wzorce stałe, aby sprawdzić, czy obiekt jest `Dice` wystąpieniem i, jeśli to jest, aby określić, czy wartość rzutowania indeksu to 6.

[!code-csharp[is#7](../../../../samples/snippets/csharp/language-reference/keywords/is/is-const-pattern7.cs#7)]

Sprawdzanie dla `null` można wykonać przy użyciu wzorca stałego. `null`Słowo kluczowe jest obsługiwane przez `is` instrukcję. Jego składnia to:

```csharp
   expr is null
```

W poniższym przykładzie przedstawiono porównanie `null` kontroli:

[!code-csharp[is#11](../../../../samples/snippets/csharp/language-reference/keywords/is/is-const-pattern11.cs#11)]

Wyrażenie `x is null` jest obliczane inaczej dla typów referencyjnych i wartości null. W przypadku typów wartości null, używa <xref:System.Nullable%601.HasValue?displayProperty=nameWithType> . W przypadku typów referencyjnych używa `(object)x == null` .

### <a name="var-pattern"></a>wzorzec wariancji

Dopasowanie wzorca do `var` wzorca zawsze powiedzie się. Jego składnia to:

```csharp
   expr is var varname
```

Gdzie wartość *wyrażenia* jest zawsze przypisana do zmiennej lokalnej o nazwie *nazwa_zmiennej*. *nazwa_zmiennej* jest zmienną tego samego typu co typ *wyrażenia* w czasie kompilacji.

Jeśli *wyrażenie* zwróci wartość `null` , `is` wyrażenie generuje `true` i przypisuje `null` do wartości *nazwa_zmiennej*. Wzorzec var jest jednym z kilku zastosowania `is` , które tworzy `true` dla `null` wartości.

Możesz użyć `var` wzorca, aby utworzyć zmienną tymczasową w ramach wyrażenia logicznego, jak pokazano w poniższym przykładzie:

[!code-csharp[is#8](../../../../samples/snippets/csharp/language-reference/keywords/is/is-var-pattern8.cs#8)]

W poprzednim przykładzie zmienna tymczasowa jest używana do przechowywania wyniku kosztownej operacji. Zmienna może być używana wiele razy.

## <a name="c-language-specification"></a>specyfikacja języka C#
  
Aby uzyskać więcej informacji, zobacz sekcję [operator is](~/_csharplang/spec/expressions.md#the-is-operator) w [specyfikacji języka c#](~/_csharplang/spec/introduction.md) oraz następujące propozycje dotyczące języka c#:

- [Dopasowanie do wzorca](~/_csharplang/proposals/csharp-7.0/pattern-matching.md)
- [Dopasowywanie wzorca do typów ogólnych](~/_csharplang/proposals/csharp-7.1/generics-pattern-match.md)
  
## <a name="see-also"></a>Zobacz też

- [Dokumentacja języka C#](../index.md)
- [Słowa kluczowe języka C#](index.md)
- [Operatory testowania typu i rzutowania](../operators/type-testing-and-cast.md)
