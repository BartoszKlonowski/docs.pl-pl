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
# <a name="is-c-reference"></a><span data-ttu-id="71bba-103">is (odwołanie w C#)</span><span class="sxs-lookup"><span data-stu-id="71bba-103">is (C# Reference)</span></span>

<span data-ttu-id="71bba-104">`is`Operator sprawdza, czy wynik wyrażenia jest zgodny z danym typem, lub (począwszy od języka C# 7,0) testuje wyrażenie względem wzorca.</span><span class="sxs-lookup"><span data-stu-id="71bba-104">The `is` operator checks if the result of an expression is compatible with a given type, or (starting with C# 7.0) tests an expression against a pattern.</span></span> <span data-ttu-id="71bba-105">Aby uzyskać informacje na temat operatora testowania typu `is` , zobacz sekcję [is operatora](../operators/type-testing-and-cast.md#is-operator) w artykule operatorion [-Test and Cast](../operators/type-testing-and-cast.md) .</span><span class="sxs-lookup"><span data-stu-id="71bba-105">For information about the type-testing `is` operator, see the [is operator](../operators/type-testing-and-cast.md#is-operator) section of the [Type-testing and cast operators](../operators/type-testing-and-cast.md) article.</span></span>

## <a name="pattern-matching-with-is"></a><span data-ttu-id="71bba-106">Dopasowanie wzorca z `is`</span><span class="sxs-lookup"><span data-stu-id="71bba-106">Pattern matching with `is`</span></span>

<span data-ttu-id="71bba-107">Począwszy od języka C# 7,0 `is` instrukcje i [przełącznik](switch.md) obsługują Dopasowywanie wzorców.</span><span class="sxs-lookup"><span data-stu-id="71bba-107">Starting with C# 7.0, the `is` and [switch](switch.md) statements support pattern matching.</span></span> <span data-ttu-id="71bba-108">`is`Słowo kluczowe obsługuje następujące wzorce:</span><span class="sxs-lookup"><span data-stu-id="71bba-108">The `is` keyword supports the following patterns:</span></span>

- <span data-ttu-id="71bba-109">[Wzorzec typu](#type-pattern), który sprawdza, czy wyrażenie może być konwertowane na określony typ i, jeśli to możliwe, rzutuje zmienną do zmiennej tego typu.</span><span class="sxs-lookup"><span data-stu-id="71bba-109">[Type pattern](#type-pattern), which tests whether an expression can be converted to a specified type and, if it can be, casts the variable to a variable of that type.</span></span>
- <span data-ttu-id="71bba-110">[Wzorzec stałej](#constant-pattern), który sprawdza, czy wyrażenie daje w wyniku określoną wartość stałą.</span><span class="sxs-lookup"><span data-stu-id="71bba-110">[Constant pattern](#constant-pattern), which tests whether an expression evaluates to a specified constant value.</span></span>
- <span data-ttu-id="71bba-111">[wzorzec var](#var-pattern), dopasowanie, które zawsze powiedzie się i wiąże wartość wyrażenia z nową zmienną lokalną.</span><span class="sxs-lookup"><span data-stu-id="71bba-111">[var pattern](#var-pattern), a match that always succeeds and binds the value of an expression to a new local variable.</span></span>

### <a name="type-pattern"></a><span data-ttu-id="71bba-112">Wzorzec typu</span><span class="sxs-lookup"><span data-stu-id="71bba-112">Type pattern</span></span>

<span data-ttu-id="71bba-113">W przypadku używania wzorca typu do dopasowania do wzorca, `is` sprawdza, czy wyrażenie może być konwertowane do określonego typu i, jeśli może, rzutowania go na zmienną tego typu.</span><span class="sxs-lookup"><span data-stu-id="71bba-113">When using the type pattern to perform pattern matching, `is` tests whether an expression can be converted to a specified type and, if it can be, casts it to a variable of that type.</span></span> <span data-ttu-id="71bba-114">Jest to proste rozszerzenie `is` instrukcji, która umożliwia obliczanie i konwersję typu zwięzłego.</span><span class="sxs-lookup"><span data-stu-id="71bba-114">It's a straightforward extension of the `is` statement that enables concise type evaluation and conversion.</span></span> <span data-ttu-id="71bba-115">Ogólna forma `is` wzorca typu jest:</span><span class="sxs-lookup"><span data-stu-id="71bba-115">The general form of the `is` type pattern is:</span></span>

```csharp
expr is type varname
```

<span data-ttu-id="71bba-116">Gdzie *Expr* jest wyrażeniem, którego wynikiem jest wystąpienie pewnego typu, *Type* jest nazwą typu, do którego zostanie przekonwertowany wynik *wyrażenia* , a *nazwa_zmiennej* jest obiektem, do którego wynik *wyrażenia* jest konwertowany, jeśli `is` test jest `true` .</span><span class="sxs-lookup"><span data-stu-id="71bba-116">Where *expr* is an expression that evaluates to an instance of some type, *type* is the name of the type to which the result of *expr* is to be converted, and *varname* is the object to which the result of *expr* is converted if the `is` test is `true`.</span></span>

<span data-ttu-id="71bba-117">`is`Wyrażenie jest `true` , jeśli *wyrażenie* nie jest `null` , i spełniony jest dowolny z następujących warunków:</span><span class="sxs-lookup"><span data-stu-id="71bba-117">The `is` expression is `true` if *expr* isn't `null`, and any of the following conditions is true:</span></span>

- <span data-ttu-id="71bba-118">*wyrażenie* jest wystąpieniem tego samego typu co *Typ*.</span><span class="sxs-lookup"><span data-stu-id="71bba-118">*expr* is an instance of the same type as *type*.</span></span>
- <span data-ttu-id="71bba-119">*wyrażenie* jest wystąpieniem typu, który pochodzi od *typu*.</span><span class="sxs-lookup"><span data-stu-id="71bba-119">*expr* is an instance of a type that derives from *type*.</span></span> <span data-ttu-id="71bba-120">Innymi słowy, wynik *wyrażenia* może być rzutowany na wystąpienie *typu*.</span><span class="sxs-lookup"><span data-stu-id="71bba-120">In other words, the result of *expr* can be upcast to an instance of *type*.</span></span>
- <span data-ttu-id="71bba-121">*wyrażenie* ma typ czasu kompilacji, który jest klasą bazową *typu*, a *wyrażenie* ma typ środowiska uruchomieniowego, który jest *typem* lub pochodzi od *typu*.</span><span class="sxs-lookup"><span data-stu-id="71bba-121">*expr* has a compile-time type that is a base class of *type*, and *expr* has a runtime type that is *type* or is derived from *type*.</span></span> <span data-ttu-id="71bba-122">*Typ czasu kompilacji* zmiennej to typ zmiennej, zgodnie z definicją w swojej deklaracji.</span><span class="sxs-lookup"><span data-stu-id="71bba-122">The *compile-time type* of a variable is the variable's type as defined in its declaration.</span></span> <span data-ttu-id="71bba-123">*Typ środowiska uruchomieniowego* zmiennej to typ wystąpienia, które jest przypisane do tej zmiennej.</span><span class="sxs-lookup"><span data-stu-id="71bba-123">The *runtime type* of a variable is the type of the instance that is assigned to that variable.</span></span>
- <span data-ttu-id="71bba-124">*wyrażenie* jest wystąpieniem typu, który implementuje interfejs *typu* .</span><span class="sxs-lookup"><span data-stu-id="71bba-124">*expr* is an instance of a type that implements the *type* interface.</span></span>

<span data-ttu-id="71bba-125">Począwszy od języka C# 7,1, *wyrażenie* może mieć typ czasu kompilacji zdefiniowany przez parametr typu ogólnego i jego ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="71bba-125">Beginning with C# 7.1, *expr* may have a compile-time type defined by a generic type parameter and its constraints.</span></span>

<span data-ttu-id="71bba-126">Jeśli *wyrażenie* jest `true` i `is` jest używane z `if` instrukcją, *nazwa_zmiennej* jest przypisywana `if` tylko wewnątrz instrukcji.</span><span class="sxs-lookup"><span data-stu-id="71bba-126">If *expr* is `true` and `is` is used with an `if` statement, *varname* is assigned within the `if` statement only.</span></span> <span data-ttu-id="71bba-127">Zakres elementu *nazwa_zmiennej* pochodzi z `is` wyrażenia na końcu bloku otaczającego `if` instrukcję.</span><span class="sxs-lookup"><span data-stu-id="71bba-127">The scope of *varname* is from the `is` expression to the end of the block enclosing the `if` statement.</span></span> <span data-ttu-id="71bba-128">Użycie elementu *nazwa_zmiennej* w innej lokalizacji powoduje wygenerowanie błędu czasu kompilacji w celu użycia zmiennej, która nie została przypisana.</span><span class="sxs-lookup"><span data-stu-id="71bba-128">Using *varname* in any other location generates a compile-time error for use of a variable that hasn't been assigned.</span></span>

<span data-ttu-id="71bba-129">Poniższy przykład używa `is` wzorca typu, aby zapewnić implementację <xref:System.IComparable.CompareTo(System.Object)?displayProperty=nameWithType> metody typu.</span><span class="sxs-lookup"><span data-stu-id="71bba-129">The following example uses the `is` type pattern to provide the implementation of a type's <xref:System.IComparable.CompareTo(System.Object)?displayProperty=nameWithType> method.</span></span>

[!code-csharp[is#5](../../../../samples/snippets/csharp/language-reference/keywords/is/is-type-pattern5.cs#5)]

<span data-ttu-id="71bba-130">Bez dopasowania do wzorca ten kod może być zapisany w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="71bba-130">Without pattern matching, this code might be written as follows.</span></span> <span data-ttu-id="71bba-131">Użycie dopasowania wzorca typu daje bardziej zwarty, czytelny kod, eliminując konieczność sprawdzenia, czy wynik konwersji to `null` .</span><span class="sxs-lookup"><span data-stu-id="71bba-131">The use of type pattern matching produces more compact, readable code by eliminating the need to test whether the result of a conversion is a `null`.</span></span>  

[!code-csharp[is#6](../../../../samples/snippets/csharp/language-reference/keywords/is/is-type-pattern6.cs#6)]

<span data-ttu-id="71bba-132">`is`Wzorzec typu generuje również bardziej zwarty kod podczas określania typu wartości.</span><span class="sxs-lookup"><span data-stu-id="71bba-132">The `is` type pattern also produces more compact code when determining the type of a value type.</span></span> <span data-ttu-id="71bba-133">W poniższym przykładzie używa się `is` wzorca typu, aby określić, czy obiekt jest `Person` `Dog` wystąpieniem, czy przed wyświetleniem wartości odpowiedniej właściwości.</span><span class="sxs-lookup"><span data-stu-id="71bba-133">The following example uses the `is` type pattern to determine whether an object is a `Person` or a `Dog` instance before displaying the value of an appropriate property.</span></span>

[!code-csharp[is#9](../../../../samples/snippets/csharp/language-reference/keywords/is/is-type-pattern9.cs#9)]

<span data-ttu-id="71bba-134">Odpowiedni kod bez dopasowania do wzorca wymaga oddzielnego przypisania zawierającego jawne rzutowanie.</span><span class="sxs-lookup"><span data-stu-id="71bba-134">The equivalent code without pattern matching requires a separate assignment that includes an explicit cast.</span></span>

[!code-csharp[is#10](../../../../samples/snippets/csharp/language-reference/keywords/is/is-type-pattern10.cs#10)]

### <a name="constant-pattern"></a><span data-ttu-id="71bba-135">Wzorzec stałej</span><span class="sxs-lookup"><span data-stu-id="71bba-135">Constant pattern</span></span>

<span data-ttu-id="71bba-136">Podczas wykonywania dopasowania wzorca ze wzorcem stałej, `is` sprawdza, czy wyrażenie jest równe określonej stałej.</span><span class="sxs-lookup"><span data-stu-id="71bba-136">When performing pattern matching with the constant pattern, `is` tests whether an expression equals a specified constant.</span></span> <span data-ttu-id="71bba-137">W języku C# 6 i wcześniejszych wersjach wzorzec stałej jest obsługiwany przez instrukcję [Switch](switch.md) .</span><span class="sxs-lookup"><span data-stu-id="71bba-137">In C# 6 and earlier versions, the constant pattern is supported by the [switch](switch.md) statement.</span></span> <span data-ttu-id="71bba-138">Począwszy od języka C# 7,0, jest to również obsługiwane przez `is` instrukcję.</span><span class="sxs-lookup"><span data-stu-id="71bba-138">Starting with C# 7.0, it's supported by the `is` statement as well.</span></span> <span data-ttu-id="71bba-139">Jego składnia to:</span><span class="sxs-lookup"><span data-stu-id="71bba-139">Its syntax is:</span></span>

```csharp
   expr is constant
```

<span data-ttu-id="71bba-140">gdzie *Expr* jest wyrażeniem, które ma zostać obliczone, a *stała* jest wartością do przetestowania.</span><span class="sxs-lookup"><span data-stu-id="71bba-140">where *expr* is the expression to evaluate, and *constant* is the value to test for.</span></span> <span data-ttu-id="71bba-141">*stała* może być dowolnym z następujących wyrażeń stałych:</span><span class="sxs-lookup"><span data-stu-id="71bba-141">*constant* can be any of the following constant expressions:</span></span>

- <span data-ttu-id="71bba-142">Wartość literału.</span><span class="sxs-lookup"><span data-stu-id="71bba-142">A literal value.</span></span>

- <span data-ttu-id="71bba-143">Nazwa zadeklarowanej `const` zmiennej.</span><span class="sxs-lookup"><span data-stu-id="71bba-143">The name of a declared `const` variable.</span></span>

- <span data-ttu-id="71bba-144">Stała wyliczenia.</span><span class="sxs-lookup"><span data-stu-id="71bba-144">An enumeration constant.</span></span>

<span data-ttu-id="71bba-145">Wyrażenie stałe jest oceniane w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="71bba-145">The constant expression is evaluated as follows:</span></span>

- <span data-ttu-id="71bba-146">Jeśli *wyrażenie* i *stała* są typami całkowitymi, operator równości języka C# określa, czy wyrażenie zwróci wartość `true` (to znaczy czy `expr == constant` ).</span><span class="sxs-lookup"><span data-stu-id="71bba-146">If *expr* and *constant* are integral types, the C# equality operator determines whether the expression returns `true` (that is, whether `expr == constant`).</span></span>

- <span data-ttu-id="71bba-147">W przeciwnym razie wartość wyrażenia jest określana przez wywołanie metody static [obiektu. Equals (wyrażenie, stała)](xref:System.Object.Equals(System.Object,System.Object)) .</span><span class="sxs-lookup"><span data-stu-id="71bba-147">Otherwise, the value of the expression is determined by a call to the static [Object.Equals(expr, constant)](xref:System.Object.Equals(System.Object,System.Object)) method.</span></span>  

<span data-ttu-id="71bba-148">Poniższy przykład łączy typ i wzorce stałe, aby sprawdzić, czy obiekt jest `Dice` wystąpieniem i, jeśli to jest, aby określić, czy wartość rzutowania indeksu to 6.</span><span class="sxs-lookup"><span data-stu-id="71bba-148">The following example combines the type and constant patterns to test whether an object is a `Dice` instance and, if it is, to determine whether the value of a dice roll is 6.</span></span>

[!code-csharp[is#7](../../../../samples/snippets/csharp/language-reference/keywords/is/is-const-pattern7.cs#7)]

<span data-ttu-id="71bba-149">Sprawdzanie dla `null` można wykonać przy użyciu wzorca stałego.</span><span class="sxs-lookup"><span data-stu-id="71bba-149">Checking for `null` can be performed using the constant pattern.</span></span> <span data-ttu-id="71bba-150">`null`Słowo kluczowe jest obsługiwane przez `is` instrukcję.</span><span class="sxs-lookup"><span data-stu-id="71bba-150">The `null` keyword is supported by the `is` statement.</span></span> <span data-ttu-id="71bba-151">Jego składnia to:</span><span class="sxs-lookup"><span data-stu-id="71bba-151">Its syntax is:</span></span>

```csharp
   expr is null
```

<span data-ttu-id="71bba-152">W poniższym przykładzie przedstawiono porównanie `null` kontroli:</span><span class="sxs-lookup"><span data-stu-id="71bba-152">The following example shows a comparison of `null` checks:</span></span>

[!code-csharp[is#11](../../../../samples/snippets/csharp/language-reference/keywords/is/is-const-pattern11.cs#11)]

<span data-ttu-id="71bba-153">Wyrażenie `x is null` jest obliczane inaczej dla typów referencyjnych i wartości null.</span><span class="sxs-lookup"><span data-stu-id="71bba-153">The expression `x is null` is computed differently for reference types and nullable value types.</span></span> <span data-ttu-id="71bba-154">W przypadku typów wartości null, używa <xref:System.Nullable%601.HasValue?displayProperty=nameWithType> .</span><span class="sxs-lookup"><span data-stu-id="71bba-154">For nullable value types, it uses <xref:System.Nullable%601.HasValue?displayProperty=nameWithType>.</span></span> <span data-ttu-id="71bba-155">W przypadku typów referencyjnych używa `(object)x == null` .</span><span class="sxs-lookup"><span data-stu-id="71bba-155">For reference types, it uses `(object)x == null`.</span></span>

### <a name="var-pattern"></a><span data-ttu-id="71bba-156">wzorzec wariancji</span><span class="sxs-lookup"><span data-stu-id="71bba-156">var pattern</span></span>

<span data-ttu-id="71bba-157">Dopasowanie wzorca do `var` wzorca zawsze powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="71bba-157">A pattern match with the `var` pattern always succeeds.</span></span> <span data-ttu-id="71bba-158">Jego składnia to:</span><span class="sxs-lookup"><span data-stu-id="71bba-158">Its syntax is:</span></span>

```csharp
   expr is var varname
```

<span data-ttu-id="71bba-159">Gdzie wartość *wyrażenia* jest zawsze przypisana do zmiennej lokalnej o nazwie *nazwa_zmiennej*.</span><span class="sxs-lookup"><span data-stu-id="71bba-159">Where the value of *expr* is always assigned to a local variable named *varname*.</span></span> <span data-ttu-id="71bba-160">*nazwa_zmiennej* jest zmienną tego samego typu co typ *wyrażenia* w czasie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="71bba-160">*varname* is a variable of the same type as the compile-time type of *expr*.</span></span>

<span data-ttu-id="71bba-161">Jeśli *wyrażenie* zwróci wartość `null` , `is` wyrażenie generuje `true` i przypisuje `null` do wartości *nazwa_zmiennej*.</span><span class="sxs-lookup"><span data-stu-id="71bba-161">If *expr* evaluates to `null`, the `is` expression produces `true` and assigns `null` to *varname*.</span></span> <span data-ttu-id="71bba-162">Wzorzec var jest jednym z kilku zastosowania `is` , które tworzy `true` dla `null` wartości.</span><span class="sxs-lookup"><span data-stu-id="71bba-162">The var pattern is one of the few uses of `is` that produces `true` for a `null` value.</span></span>

<span data-ttu-id="71bba-163">Możesz użyć `var` wzorca, aby utworzyć zmienną tymczasową w ramach wyrażenia logicznego, jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="71bba-163">You can use the `var` pattern to create a temporary variable within a Boolean expression, as the following example shows:</span></span>

[!code-csharp[is#8](../../../../samples/snippets/csharp/language-reference/keywords/is/is-var-pattern8.cs#8)]

<span data-ttu-id="71bba-164">W poprzednim przykładzie zmienna tymczasowa jest używana do przechowywania wyniku kosztownej operacji.</span><span class="sxs-lookup"><span data-stu-id="71bba-164">In the preceding example, the temporary variable is used to store the result of an expensive operation.</span></span> <span data-ttu-id="71bba-165">Zmienna może być używana wiele razy.</span><span class="sxs-lookup"><span data-stu-id="71bba-165">The variable can then be used multiple times.</span></span>

## <a name="c-language-specification"></a><span data-ttu-id="71bba-166">specyfikacja języka C#</span><span class="sxs-lookup"><span data-stu-id="71bba-166">C# language specification</span></span>
  
<span data-ttu-id="71bba-167">Aby uzyskać więcej informacji, zobacz sekcję [operator is](~/_csharplang/spec/expressions.md#the-is-operator) w [specyfikacji języka c#](~/_csharplang/spec/introduction.md) oraz następujące propozycje dotyczące języka c#:</span><span class="sxs-lookup"><span data-stu-id="71bba-167">For more information, see [The is operator](~/_csharplang/spec/expressions.md#the-is-operator) section of the [C# language specification](~/_csharplang/spec/introduction.md) and the following C# language proposals:</span></span>

- [<span data-ttu-id="71bba-168">Dopasowanie do wzorca</span><span class="sxs-lookup"><span data-stu-id="71bba-168">Pattern matching</span></span>](~/_csharplang/proposals/csharp-7.0/pattern-matching.md)
- [<span data-ttu-id="71bba-169">Dopasowywanie wzorca do typów ogólnych</span><span class="sxs-lookup"><span data-stu-id="71bba-169">Pattern matching with generics</span></span>](~/_csharplang/proposals/csharp-7.1/generics-pattern-match.md)
  
## <a name="see-also"></a><span data-ttu-id="71bba-170">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="71bba-170">See also</span></span>

- [<span data-ttu-id="71bba-171">Dokumentacja języka C#</span><span class="sxs-lookup"><span data-stu-id="71bba-171">C# reference</span></span>](../index.md)
- [<span data-ttu-id="71bba-172">Słowa kluczowe języka C#</span><span class="sxs-lookup"><span data-stu-id="71bba-172">C# keywords</span></span>](index.md)
- [<span data-ttu-id="71bba-173">Operatory testowania typu i rzutowania</span><span class="sxs-lookup"><span data-stu-id="71bba-173">Type-testing and cast operators</span></span>](../operators/type-testing-and-cast.md)
