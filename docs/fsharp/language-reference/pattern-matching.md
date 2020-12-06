---
title: Dopasowanie wzorca
description: 'Dowiedz się, w jaki sposób wzorce są używane w języku F # do porównywania danych ze strukturami logicznymi, rozkładania danych na części składowych lub wyodrębniania informacji z danych.'
ms.date: 11/12/2020
ms.openlocfilehash: 932f50b7947f6df728149437dd3ceb19c42e5c6a
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96740279"
---
# <a name="pattern-matching"></a><span data-ttu-id="479d1-103">Dopasowanie wzorca</span><span class="sxs-lookup"><span data-stu-id="479d1-103">Pattern Matching</span></span>

<span data-ttu-id="479d1-104">Wzorce są regułami do przekształcania danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="479d1-104">Patterns are rules for transforming input data.</span></span> <span data-ttu-id="479d1-105">Są one używane w całym języku F # do porównywania danych ze strukturą logiczną lub strukturami, rozkładania danych do części składowych lub wyodrębniania informacji z danych na różne sposoby.</span><span class="sxs-lookup"><span data-stu-id="479d1-105">They are used throughout the F# language to compare data with a logical structure or structures, decompose data into constituent parts, or extract information from data in various ways.</span></span>

## <a name="remarks"></a><span data-ttu-id="479d1-106">Uwagi</span><span class="sxs-lookup"><span data-stu-id="479d1-106">Remarks</span></span>

<span data-ttu-id="479d1-107">Wzorce są używane w wielu konstrukcjach języka, takich jak `match` wyrażenie.</span><span class="sxs-lookup"><span data-stu-id="479d1-107">Patterns are used in many language constructs, such as the `match` expression.</span></span> <span data-ttu-id="479d1-108">Są one używane podczas przetwarzania argumentów dla funkcji w `let` powiązaniach, wyrażeniach lambda i w obsłudze wyjątków skojarzonych z `try...with` wyrażeniem.</span><span class="sxs-lookup"><span data-stu-id="479d1-108">They are used when you are processing arguments for functions in `let` bindings, lambda expressions, and in the exception handlers associated with the `try...with` expression.</span></span> <span data-ttu-id="479d1-109">Aby uzyskać więcej informacji, zobacz [wyrażenia dopasowywania](match-expressions.md), [Zezwalanie na powiązania](./functions/let-bindings.md), [wyrażenia lambda: `fun` słowo kluczowe](./functions/lambda-expressions-the-fun-keyword.md)i [wyjątki: `try...with` wyrażenie](./exception-handling/the-try-with-expression.md).</span><span class="sxs-lookup"><span data-stu-id="479d1-109">For more information, see [Match Expressions](match-expressions.md), [let Bindings](./functions/let-bindings.md), [Lambda Expressions: The `fun` Keyword](./functions/lambda-expressions-the-fun-keyword.md), and [Exceptions: The `try...with` Expression](./exception-handling/the-try-with-expression.md).</span></span>

<span data-ttu-id="479d1-110">Na przykład, w `match` wyrażeniu *wzorzec* jest zgodny z symbolem potoku.</span><span class="sxs-lookup"><span data-stu-id="479d1-110">For example, in the `match` expression, the *pattern* is what follows the pipe symbol.</span></span>

```fsharp
match expression with
| pattern [ when condition ] -> result-expression
...
```

<span data-ttu-id="479d1-111">Każdy wzorzec działa jako reguła do przekształcania danych wejściowych w jakiś sposób.</span><span class="sxs-lookup"><span data-stu-id="479d1-111">Each pattern acts as a rule for transforming input in some way.</span></span> <span data-ttu-id="479d1-112">W `match` wyrażeniu każdy wzorzec jest sprawdzany z kolei, aby sprawdzić, czy dane wejściowe są zgodne ze wzorcem.</span><span class="sxs-lookup"><span data-stu-id="479d1-112">In the `match` expression, each pattern is examined in turn to see if the input data is compatible with the pattern.</span></span> <span data-ttu-id="479d1-113">W przypadku znalezienia dopasowania zostanie wykonane wyrażenie wynik.</span><span class="sxs-lookup"><span data-stu-id="479d1-113">If a match is found, the result expression is executed.</span></span> <span data-ttu-id="479d1-114">Jeśli dopasowanie nie zostanie znalezione, zostanie przetestowana następna reguła wzorca.</span><span class="sxs-lookup"><span data-stu-id="479d1-114">If a match is not found, the next pattern rule is tested.</span></span> <span data-ttu-id="479d1-115">Wartość opcjonalna, gdy część *warunku* jest objaśniona w [wyrażeniach dopasowania](match-expressions.md).</span><span class="sxs-lookup"><span data-stu-id="479d1-115">The optional when *condition* part is explained in [Match Expressions](match-expressions.md).</span></span>

<span data-ttu-id="479d1-116">Obsługiwane wzorce przedstawiono w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="479d1-116">Supported patterns are shown in the following table.</span></span> <span data-ttu-id="479d1-117">W czasie wykonywania, dane wejściowe są testowane względem każdego z następujących wzorców w kolejności wymienionej w tabeli, a wzorce są stosowane cyklicznie, od pierwszego do ostatniego, jak pojawiają się w kodzie, i od lewej do prawej dla wzorców w każdym wierszu.</span><span class="sxs-lookup"><span data-stu-id="479d1-117">At run time, the input is tested against each of the following patterns in the order listed in the table, and patterns are applied recursively, from first to last as they appear in your code, and from left to right for the patterns on each line.</span></span>

|<span data-ttu-id="479d1-118">Nazwa</span><span class="sxs-lookup"><span data-stu-id="479d1-118">Name</span></span>|<span data-ttu-id="479d1-119">Opis</span><span class="sxs-lookup"><span data-stu-id="479d1-119">Description</span></span>|<span data-ttu-id="479d1-120">Przykład</span><span class="sxs-lookup"><span data-stu-id="479d1-120">Example</span></span>|
|----|-----------|-------|
|<span data-ttu-id="479d1-121">Wzorzec stałej</span><span class="sxs-lookup"><span data-stu-id="479d1-121">Constant pattern</span></span>|<span data-ttu-id="479d1-122">Dowolny literał numeryczny, znak lub ciąg, stała wyliczenia lub zdefiniowany identyfikator literału</span><span class="sxs-lookup"><span data-stu-id="479d1-122">Any numeric, character, or string literal, an enumeration constant, or a defined literal identifier</span></span>|<span data-ttu-id="479d1-123">`1.0`, `"test"`, `30`, `Color.Red`</span><span class="sxs-lookup"><span data-stu-id="479d1-123">`1.0`, `"test"`, `30`, `Color.Red`</span></span>|
|<span data-ttu-id="479d1-124">Wzorzec identyfikatora</span><span class="sxs-lookup"><span data-stu-id="479d1-124">Identifier pattern</span></span>|<span data-ttu-id="479d1-125">Wartość przypadku Unii rozłącznej, etykieta wyjątku lub przypadek aktywnego wzorca</span><span class="sxs-lookup"><span data-stu-id="479d1-125">A case value of a discriminated union, an exception label, or an active pattern case</span></span>|`Some(x)`<br /><br />`Failure(msg)`|
|<span data-ttu-id="479d1-126">Wzorzec zmiennej</span><span class="sxs-lookup"><span data-stu-id="479d1-126">Variable pattern</span></span>|<span data-ttu-id="479d1-127">*identyfikatora*</span><span class="sxs-lookup"><span data-stu-id="479d1-127">*identifier*</span></span>|`a`|
|<span data-ttu-id="479d1-128">`as` znaczne</span><span class="sxs-lookup"><span data-stu-id="479d1-128">`as` pattern</span></span>|<span data-ttu-id="479d1-129">*wzorzec* jako *Identyfikator*</span><span class="sxs-lookup"><span data-stu-id="479d1-129">*pattern* as *identifier*</span></span>|`(a, b) as tuple1`|
|<span data-ttu-id="479d1-130">LUB wzorzec</span><span class="sxs-lookup"><span data-stu-id="479d1-130">OR pattern</span></span>|<span data-ttu-id="479d1-131">*pattern1* &#124; *pattern2*</span><span class="sxs-lookup"><span data-stu-id="479d1-131">*pattern1* &#124; *pattern2*</span></span>|<code>([h] &#124; [h; _])</code>|
|<span data-ttu-id="479d1-132">I wzorzec</span><span class="sxs-lookup"><span data-stu-id="479d1-132">AND pattern</span></span>|<span data-ttu-id="479d1-133">*pattern1* &amp; *pattern2*</span><span class="sxs-lookup"><span data-stu-id="479d1-133">*pattern1* &amp; *pattern2*</span></span>|`(a, b) & (_, "test")`|
|<span data-ttu-id="479d1-134">Wzorzec wad</span><span class="sxs-lookup"><span data-stu-id="479d1-134">Cons pattern</span></span>|<span data-ttu-id="479d1-135">*Identyfikator* :: *list — identyfikator*</span><span class="sxs-lookup"><span data-stu-id="479d1-135">*identifier* :: *list-identifier*</span></span>|`h :: t`|
|<span data-ttu-id="479d1-136">Wzorzec listy</span><span class="sxs-lookup"><span data-stu-id="479d1-136">List pattern</span></span>|<span data-ttu-id="479d1-137">[ *pattern_1*;...; *pattern_n* ]</span><span class="sxs-lookup"><span data-stu-id="479d1-137">[ *pattern_1*; ... ; *pattern_n* ]</span></span>|`[ a; b; c ]`|
|<span data-ttu-id="479d1-138">Wzorzec tablicy</span><span class="sxs-lookup"><span data-stu-id="479d1-138">Array pattern</span></span>|<span data-ttu-id="479d1-139">[&#124; *pattern_1*;..; *pattern_n* &#124;]</span><span class="sxs-lookup"><span data-stu-id="479d1-139">[&#124; *pattern_1*; ..; *pattern_n* &#124;]</span></span>|<code>[&#124; a; b; c &#124;]</code>|
|<span data-ttu-id="479d1-140">Wzorzec w nawiasach</span><span class="sxs-lookup"><span data-stu-id="479d1-140">Parenthesized pattern</span></span>|<span data-ttu-id="479d1-141">( *wzorzec* )</span><span class="sxs-lookup"><span data-stu-id="479d1-141">( *pattern* )</span></span>|`( a )`|
|<span data-ttu-id="479d1-142">Wzorzec krotki</span><span class="sxs-lookup"><span data-stu-id="479d1-142">Tuple pattern</span></span>|<span data-ttu-id="479d1-143">( *pattern_1*,..., *pattern_n* )</span><span class="sxs-lookup"><span data-stu-id="479d1-143">( *pattern_1*, ... , *pattern_n* )</span></span>|`( a, b )`|
|<span data-ttu-id="479d1-144">Wzorzec rekordu</span><span class="sxs-lookup"><span data-stu-id="479d1-144">Record pattern</span></span>|<span data-ttu-id="479d1-145">{ *Identifier1*  =  *pattern_1*; ... ; *identifier_n*  =  *pattern_n* }</span><span class="sxs-lookup"><span data-stu-id="479d1-145">{ *identifier1* = *pattern_1*; ... ; *identifier_n* = *pattern_n* }</span></span>|`{ Name = name; }`|
|<span data-ttu-id="479d1-146">Wzorzec wieloznaczny</span><span class="sxs-lookup"><span data-stu-id="479d1-146">Wildcard pattern</span></span>|<span data-ttu-id="479d1-147">_</span><span class="sxs-lookup"><span data-stu-id="479d1-147">_</span></span>|`_`|
|<span data-ttu-id="479d1-148">Wzorzec wraz z adnotacją typu</span><span class="sxs-lookup"><span data-stu-id="479d1-148">Pattern together with type annotation</span></span>|<span data-ttu-id="479d1-149">*wzorzec* : *Typ*</span><span class="sxs-lookup"><span data-stu-id="479d1-149">*pattern* : *type*</span></span>|`a : int`|
|<span data-ttu-id="479d1-150">Typ wzorca testu</span><span class="sxs-lookup"><span data-stu-id="479d1-150">Type test pattern</span></span>|<span data-ttu-id="479d1-151">:?</span><span class="sxs-lookup"><span data-stu-id="479d1-151">:?</span></span> <span data-ttu-id="479d1-152">*Typ* [ *Identyfikator* as]</span><span class="sxs-lookup"><span data-stu-id="479d1-152">*type* [ as *identifier* ]</span></span>|`:? System.DateTime as dt`|
|<span data-ttu-id="479d1-153">Wzorzec o wartości null</span><span class="sxs-lookup"><span data-stu-id="479d1-153">Null pattern</span></span>|<span data-ttu-id="479d1-154">wartość null</span><span class="sxs-lookup"><span data-stu-id="479d1-154">null</span></span>|`null`|
|<span data-ttu-id="479d1-155">Wzorzec nameof</span><span class="sxs-lookup"><span data-stu-id="479d1-155">Nameof pattern</span></span>|<span data-ttu-id="479d1-156">*wyrażenie nameof*</span><span class="sxs-lookup"><span data-stu-id="479d1-156">*nameof expr*</span></span>|`nameof str`|

## <a name="constant-patterns"></a><span data-ttu-id="479d1-157">Wzorce stałe</span><span class="sxs-lookup"><span data-stu-id="479d1-157">Constant Patterns</span></span>

<span data-ttu-id="479d1-158">Wzorce stałe są literami, znakami i literałami ciągów, stałymi wyliczeniami (z uwzględnieniem nazwy typu wyliczenia).</span><span class="sxs-lookup"><span data-stu-id="479d1-158">Constant patterns are numeric, character, and string literals, enumeration constants (with the enumeration type name included).</span></span> <span data-ttu-id="479d1-159">`match`Wyrażenie, które ma tylko stałe wzorce, można porównać do instrukcji case w innych językach.</span><span class="sxs-lookup"><span data-stu-id="479d1-159">A `match` expression that has only constant patterns can be compared to a case statement in other languages.</span></span> <span data-ttu-id="479d1-160">Dane wejściowe są porównywane z wartością literału, a wzorzec pasuje, jeśli wartości są równe.</span><span class="sxs-lookup"><span data-stu-id="479d1-160">The input is compared with the literal value and the pattern matches if the values are equal.</span></span> <span data-ttu-id="479d1-161">Typ literału musi być zgodny z typem danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="479d1-161">The type of the literal must be compatible with the type of the input.</span></span>

<span data-ttu-id="479d1-162">Poniższy przykład demonstruje użycie wzorców literałów, a także używa wzorca zmiennej i wzorca OR.</span><span class="sxs-lookup"><span data-stu-id="479d1-162">The following example demonstrates the use of literal patterns, and also uses a variable pattern and an OR pattern.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4801.fs)]

<span data-ttu-id="479d1-163">Innym przykładem wzorca literału jest wzorzec oparty na stałych wyliczeniach.</span><span class="sxs-lookup"><span data-stu-id="479d1-163">Another example of a literal pattern is a pattern based on enumeration constants.</span></span> <span data-ttu-id="479d1-164">Należy określić nazwę typu wyliczeniowego w przypadku używania stałych wyliczania.</span><span class="sxs-lookup"><span data-stu-id="479d1-164">You must specify the enumeration type name when you use enumeration constants.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4802.fs)]

## <a name="identifier-patterns"></a><span data-ttu-id="479d1-165">Wzorce identyfikatorów</span><span class="sxs-lookup"><span data-stu-id="479d1-165">Identifier Patterns</span></span>

<span data-ttu-id="479d1-166">Jeśli wzorzec jest ciągiem znaków, który tworzy prawidłowy identyfikator, formularz identyfikatora określa sposób dopasowania wzorca.</span><span class="sxs-lookup"><span data-stu-id="479d1-166">If the pattern is a string of characters that forms a valid identifier, the form of the identifier determines how the pattern is matched.</span></span> <span data-ttu-id="479d1-167">Jeśli identyfikator jest dłuższy niż pojedynczy znak i zaczyna się od wielkiej litery, kompilator próbuje dopasować wzorzec identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="479d1-167">If the identifier is longer than a single character and starts with an uppercase character, the compiler tries to make a match to the identifier pattern.</span></span> <span data-ttu-id="479d1-168">Identyfikatorem tego wzorca może być wartość oznaczona przy użyciu atrybutu literału, przypadku Unii rozłącznej, identyfikatora wyjątku lub aktywnego przypadku wzorca.</span><span class="sxs-lookup"><span data-stu-id="479d1-168">The identifier for this pattern could be a value marked with the Literal attribute, a discriminated union case, an exception identifier, or an active pattern case.</span></span> <span data-ttu-id="479d1-169">Jeśli nie znaleziono zgodnego identyfikatora, dopasowanie nie powiedzie się, a następna reguła wzorca, wzorzec zmiennej, jest porównywana z danymi wejściowymi.</span><span class="sxs-lookup"><span data-stu-id="479d1-169">If no matching identifier is found, the match fails and the next pattern rule, the variable pattern, is compared to the input.</span></span>

<span data-ttu-id="479d1-170">Wzorce Unii rozłącznych mogą być prostymi nazwanymi przypadkami lub mogą mieć wartość lub krotkę zawierającą wiele wartości.</span><span class="sxs-lookup"><span data-stu-id="479d1-170">Discriminated union patterns can be simple named cases or they can have a value, or a tuple containing multiple values.</span></span> <span data-ttu-id="479d1-171">Jeśli istnieje wartość, należy określić identyfikator dla tej wartości.</span><span class="sxs-lookup"><span data-stu-id="479d1-171">If there is a value, you must specify an identifier for the value.</span></span> <span data-ttu-id="479d1-172">W przypadku krotki, należy podać wzorzec krotki z identyfikatorem dla każdego elementu krotki lub identyfikatora z nazwą pola dla jednego lub więcej nazwanych pól Union.</span><span class="sxs-lookup"><span data-stu-id="479d1-172">In the case of a tuple, you must supply a tuple pattern with an identifier for each element of the tuple or an identifier with a field name for one or more named union fields.</span></span> <span data-ttu-id="479d1-173">Przykłady kodu można znaleźć w przykładach w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="479d1-173">See the code examples in this section for examples.</span></span>

<span data-ttu-id="479d1-174">Typ jest Unią rozłączną, `option` która ma dwa przypadki, `Some` i `None` .</span><span class="sxs-lookup"><span data-stu-id="479d1-174">The `option` type is a discriminated union that has two cases, `Some` and `None`.</span></span> <span data-ttu-id="479d1-175">Jeden przypadek ( `Some` ) ma wartość, ale drugi ( `None` ) jest tylko nazwanym przypadkiem.</span><span class="sxs-lookup"><span data-stu-id="479d1-175">One case (`Some`) has a value, but the other (`None`) is just a named case.</span></span> <span data-ttu-id="479d1-176">W związku z tym, musi `Some` mieć zmienną dla wartości skojarzonej z `Some` przypadkiem, ale `None` musi być wyświetlana sama przez siebie.</span><span class="sxs-lookup"><span data-stu-id="479d1-176">Therefore, `Some` needs to have a variable for the value associated with the `Some` case, but `None` must appear by itself.</span></span> <span data-ttu-id="479d1-177">W poniższym kodzie zmienna `var1` otrzymuje wartość uzyskaną przez dopasowanie do `Some` wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="479d1-177">In the following code, the variable `var1` is given the value that is obtained by matching to the `Some` case.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4803.fs)]

<span data-ttu-id="479d1-178">W poniższym przykładzie `PersonName` związek rozłącznych zawiera kombinację ciągów i znaków, które reprezentują możliwe formy nazw.</span><span class="sxs-lookup"><span data-stu-id="479d1-178">In the following example, the `PersonName` discriminated union contains a mixture of strings and characters that represent possible forms of names.</span></span> <span data-ttu-id="479d1-179">Przypadki rozłącznych zbiorów to `FirstOnly` , `LastOnly` i `FirstLast` .</span><span class="sxs-lookup"><span data-stu-id="479d1-179">The cases of the discriminated union are `FirstOnly`, `LastOnly`, and `FirstLast`.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4804.fs)]

<span data-ttu-id="479d1-180">W przypadku Unii rozłącznych, które mają nazwane pola, należy użyć znaku równości (=) do wyodrębnienia wartości nazwanego pola.</span><span class="sxs-lookup"><span data-stu-id="479d1-180">For discriminated unions that have named fields, you use the equals sign (=) to extract the value of a named field.</span></span> <span data-ttu-id="479d1-181">Rozważmy na przykład Unię rozłącznych z deklaracją podobną do następującej.</span><span class="sxs-lookup"><span data-stu-id="479d1-181">For example, consider a discriminated union with a declaration like the following.</span></span>

```fsharp
type Shape =
    | Rectangle of height : float * width : float
    | Circle of radius : float
```

<span data-ttu-id="479d1-182">Możesz użyć nazwanych pól w wyrażeniu dopasowania wzorca w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="479d1-182">You can use the named fields in a pattern matching expression as follows.</span></span>

```fsharp
let matchShape shape =
    match shape with
    | Rectangle(height = h) -> printfn $"Rectangle with length %f{h}"
    | Circle(r) -> printfn $"Circle with radius %f{r}"
```

<span data-ttu-id="479d1-183">Użycie nazwanego pola jest opcjonalne, dlatego w poprzednim przykładzie oba `Circle(r)` i `Circle(radius = r)` mają ten sam efekt.</span><span class="sxs-lookup"><span data-stu-id="479d1-183">The use of the named field is optional, so in the previous example, both `Circle(r)` and `Circle(radius = r)` have the same effect.</span></span>

<span data-ttu-id="479d1-184">Po określeniu wielu pól Użyj średnika (;) jako separator.</span><span class="sxs-lookup"><span data-stu-id="479d1-184">When you specify multiple fields, use the semicolon (;) as a separator.</span></span>

```fsharp
match shape with
| Rectangle(height = h; width = w) -> printfn $"Rectangle with height %f{h} and width %f{w}"
| _ -> ()
```

<span data-ttu-id="479d1-185">Aktywne wzorce umożliwiają zdefiniowanie bardziej złożonej niestandardowej dopasowywania do wzorca.</span><span class="sxs-lookup"><span data-stu-id="479d1-185">Active patterns enable you to define more complex custom pattern matching.</span></span> <span data-ttu-id="479d1-186">Aby uzyskać więcej informacji na temat aktywnych wzorców, zobacz [aktywne wzorce](active-patterns.md).</span><span class="sxs-lookup"><span data-stu-id="479d1-186">For more information about active patterns, see [Active Patterns](active-patterns.md).</span></span>

<span data-ttu-id="479d1-187">Przypadek, w którym identyfikator jest wyjątek jest używany w dopasowywaniu wzorców w kontekście obsługi wyjątków.</span><span class="sxs-lookup"><span data-stu-id="479d1-187">The case in which the identifier is an exception is used in pattern matching in the context of exception handlers.</span></span> <span data-ttu-id="479d1-188">Aby uzyskać informacje na temat dopasowywania wzorców w obsłudze wyjątków, zobacz [wyjątki: `try...with` wyrażenie](./exception-handling/the-try-with-expression.md).</span><span class="sxs-lookup"><span data-stu-id="479d1-188">For information about pattern matching in exception handling, see [Exceptions: The `try...with` Expression](./exception-handling/the-try-with-expression.md).</span></span>

## <a name="variable-patterns"></a><span data-ttu-id="479d1-189">Wzorce zmiennych</span><span class="sxs-lookup"><span data-stu-id="479d1-189">Variable Patterns</span></span>

<span data-ttu-id="479d1-190">Wzór zmiennej przypisuje wartość dopasowaną do nazwy zmiennej, która jest następnie dostępna do użycia w wyrażeniu wykonywania na prawo od `->` symbolu.</span><span class="sxs-lookup"><span data-stu-id="479d1-190">The variable pattern assigns the value being matched to a variable name, which is then available for use in the execution expression to the right of the `->` symbol.</span></span> <span data-ttu-id="479d1-191">Sam wzorzec zmiennej pasuje do dowolnych danych wejściowych, ale wzorce zmiennych często pojawiają się w innych wzorcach, co pozwala na bardziej złożone struktury, takie jak krotki i tablice, do rozdzielania na zmienne.</span><span class="sxs-lookup"><span data-stu-id="479d1-191">A variable pattern alone matches any input, but variable patterns often appear within other patterns, therefore enabling more complex structures such as tuples and arrays to be decomposed into variables.</span></span>

<span data-ttu-id="479d1-192">Poniższy przykład ilustruje wzór zmiennej w obrębie wzorca krotki.</span><span class="sxs-lookup"><span data-stu-id="479d1-192">The following example demonstrates a variable pattern within a tuple pattern.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4805.fs)]

## <a name="as-pattern"></a><span data-ttu-id="479d1-193">jako wzorzec</span><span class="sxs-lookup"><span data-stu-id="479d1-193">as Pattern</span></span>

<span data-ttu-id="479d1-194">`as`Wzorzec jest wzorcem z `as` dołączoną do niej klauzulą.</span><span class="sxs-lookup"><span data-stu-id="479d1-194">The `as` pattern is a pattern that has an `as` clause appended to it.</span></span> <span data-ttu-id="479d1-195">`as`Klauzula wiąże dopasowaną wartość do nazwy, która może być używana w wyrażeniu wykonywania `match` wyrażenia lub, w przypadku, gdy ten wzorzec jest używany w `let` powiązaniu, nazwa jest dodawana jako powiązanie do zakresu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="479d1-195">The `as` clause binds the matched value to a name that can be used in the execution expression of a `match` expression, or, in the case where this pattern is used in a `let` binding, the name is added as a binding to the local scope.</span></span>

<span data-ttu-id="479d1-196">Poniższy przykład używa `as` wzorca.</span><span class="sxs-lookup"><span data-stu-id="479d1-196">The following example uses an `as` pattern.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4806.fs)]

## <a name="or-pattern"></a><span data-ttu-id="479d1-197">LUB wzorzec</span><span class="sxs-lookup"><span data-stu-id="479d1-197">OR Pattern</span></span>

<span data-ttu-id="479d1-198">Wzorzec OR jest używany, gdy dane wejściowe mogą odpowiadać wielu wzorcem i chcesz wykonać ten sam kod w wyniku.</span><span class="sxs-lookup"><span data-stu-id="479d1-198">The OR pattern is used when input data can match multiple patterns, and you want to execute the same code as a result.</span></span> <span data-ttu-id="479d1-199">Typy obu stron wzorca OR muszą być zgodne.</span><span class="sxs-lookup"><span data-stu-id="479d1-199">The types of both sides of the OR pattern must be compatible.</span></span>

<span data-ttu-id="479d1-200">Poniższy przykład demonstruje wzorzec OR.</span><span class="sxs-lookup"><span data-stu-id="479d1-200">The following example demonstrates the OR pattern.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4807.fs)]

## <a name="and-pattern"></a><span data-ttu-id="479d1-201">I wzorzec</span><span class="sxs-lookup"><span data-stu-id="479d1-201">AND Pattern</span></span>

<span data-ttu-id="479d1-202">Wzorzec i wymaga, aby dane wejściowe były zgodne z dwoma wzorcami.</span><span class="sxs-lookup"><span data-stu-id="479d1-202">The AND pattern requires that the input match two patterns.</span></span> <span data-ttu-id="479d1-203">Typy obu stron wzorca i muszą być zgodne.</span><span class="sxs-lookup"><span data-stu-id="479d1-203">The types of both sides of the AND pattern must be compatible.</span></span>

<span data-ttu-id="479d1-204">Poniższy przykład jest podobny do `detectZeroTuple` przedstawionego w sekcji wzorzec krotki w dalszej części tego tematu, ale w tym miejscu `var1` i `var2` są uzyskiwane jako wartości przy użyciu wzorca i.</span><span class="sxs-lookup"><span data-stu-id="479d1-204">The following example is like `detectZeroTuple` shown in the Tuple Pattern section later in this topic, but here both `var1` and `var2` are obtained as values by using the AND pattern.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4808.fs)]

## <a name="cons-pattern"></a><span data-ttu-id="479d1-205">Wzorzec wad</span><span class="sxs-lookup"><span data-stu-id="479d1-205">Cons Pattern</span></span>

<span data-ttu-id="479d1-206">Wzorzec wad służy do rozdzielania listy na pierwszy element, *nagłówek* i listę zawierającą pozostałe elementy, *ogon*.</span><span class="sxs-lookup"><span data-stu-id="479d1-206">The cons pattern is used to decompose a list into the first element, the *head*, and a list that contains the remaining elements, the *tail*.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4809.fs)]

## <a name="list-pattern"></a><span data-ttu-id="479d1-207">Wzorzec listy</span><span class="sxs-lookup"><span data-stu-id="479d1-207">List Pattern</span></span>

<span data-ttu-id="479d1-208">Wzorzec listy umożliwia rozdzielanie list na wiele elementów.</span><span class="sxs-lookup"><span data-stu-id="479d1-208">The list pattern enables lists to be decomposed into a number of elements.</span></span> <span data-ttu-id="479d1-209">Sam wzorzec listy może pasować tylko do list o określonej liczbie elementów.</span><span class="sxs-lookup"><span data-stu-id="479d1-209">The list pattern itself can match only lists of a specific number of elements.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4810.fs)]

## <a name="array-pattern"></a><span data-ttu-id="479d1-210">Wzorzec tablicy</span><span class="sxs-lookup"><span data-stu-id="479d1-210">Array Pattern</span></span>

<span data-ttu-id="479d1-211">Wzór tablicy przypomina wzorzec listy i może służyć do rozdzielania tablic o określonej długości.</span><span class="sxs-lookup"><span data-stu-id="479d1-211">The array pattern resembles the list pattern and can be used to decompose arrays of a specific length.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4811.fs)]

## <a name="parenthesized-pattern"></a><span data-ttu-id="479d1-212">Wzorzec w nawiasach</span><span class="sxs-lookup"><span data-stu-id="479d1-212">Parenthesized Pattern</span></span>

<span data-ttu-id="479d1-213">Nawiasy można grupować wokół wzorców w celu osiągnięcia żądanych łączność.</span><span class="sxs-lookup"><span data-stu-id="479d1-213">Parentheses can be grouped around patterns to achieve the desired associativity.</span></span> <span data-ttu-id="479d1-214">W poniższym przykładzie nawiasy są używane do kontrolowania łączność między wzorcem a i wzorcem wad.</span><span class="sxs-lookup"><span data-stu-id="479d1-214">In the following example, parentheses are used to control associativity between an AND pattern and a cons pattern.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4812.fs)]

## <a name="tuple-pattern"></a><span data-ttu-id="479d1-215">Wzorzec krotki</span><span class="sxs-lookup"><span data-stu-id="479d1-215">Tuple Pattern</span></span>

<span data-ttu-id="479d1-216">Wzorzec krotki dopasowuje dane wejściowe w postaci spójnej kolekcji i umożliwia rozłożenie krotki na elementy składowe za pomocą zmiennych dopasowywania wzorców dla każdej pozycji w spójnej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="479d1-216">The tuple pattern matches input in tuple form and enables the tuple to be decomposed into its constituent elements by using pattern matching variables for each position in the tuple.</span></span>

<span data-ttu-id="479d1-217">Poniższy przykład demonstruje wzorzec krotki i używa także wzorców literałów, wzorów zmiennych i wzorca symboli wieloznacznych.</span><span class="sxs-lookup"><span data-stu-id="479d1-217">The following example demonstrates the tuple pattern and also uses literal patterns, variable patterns, and the wildcard pattern.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4813.fs)]

## <a name="record-pattern"></a><span data-ttu-id="479d1-218">Wzorzec rekordu</span><span class="sxs-lookup"><span data-stu-id="479d1-218">Record Pattern</span></span>

<span data-ttu-id="479d1-219">Wzorzec rekordu służy do rozkładania rekordów w celu wyodrębnienia wartości pól.</span><span class="sxs-lookup"><span data-stu-id="479d1-219">The record pattern is used to decompose records to extract the values of fields.</span></span> <span data-ttu-id="479d1-220">Wzorzec nie musi odwoływać się do wszystkich pól rekordu; wszystkie pominięte pola tylko nie uczestniczą w dopasowaniu i nie są wyodrębniane.</span><span class="sxs-lookup"><span data-stu-id="479d1-220">The pattern does not have to reference all fields of the record; any omitted fields just do not participate in matching and are not extracted.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4814.fs)]

## <a name="wildcard-pattern"></a><span data-ttu-id="479d1-221">Wzorzec wieloznaczny</span><span class="sxs-lookup"><span data-stu-id="479d1-221">Wildcard Pattern</span></span>

<span data-ttu-id="479d1-222">Wzorzec symbol wieloznaczny jest reprezentowany przez znak podkreślenia ( `_` ) i dopasowuje wszelkie dane wejściowe, podobnie jak wzór zmiennej, z tą różnicą, że dane wejściowe są odrzucane zamiast przypisywania do zmiennej.</span><span class="sxs-lookup"><span data-stu-id="479d1-222">The wildcard pattern is represented by the underscore (`_`) character and matches any input, just like the variable pattern, except that the input is discarded instead of assigned to a variable.</span></span> <span data-ttu-id="479d1-223">Wzorzec symbol wieloznaczny jest często używany w innych wzorcach jako symbol zastępczy dla wartości, które nie są konieczne w wyrażeniu z prawej strony `->` symbolu.</span><span class="sxs-lookup"><span data-stu-id="479d1-223">The wildcard pattern is often used within other patterns as a placeholder for values that are not needed in the expression to the right of the `->` symbol.</span></span> <span data-ttu-id="479d1-224">Wzorzec symboli wieloznacznych jest również często używany na końcu listy wzorców w celu dopasowania do niedopasowanych danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="479d1-224">The wildcard pattern is also frequently used at the end of a list of patterns to match any unmatched input.</span></span> <span data-ttu-id="479d1-225">Wzorzec symboli wieloznacznych jest prezentowany w wielu przykładach kodu w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="479d1-225">The wildcard pattern is demonstrated in many code examples in this topic.</span></span> <span data-ttu-id="479d1-226">Zobacz poprzedni kod na jeden przykład.</span><span class="sxs-lookup"><span data-stu-id="479d1-226">See the preceding code for one example.</span></span>

## <a name="patterns-that-have-type-annotations"></a><span data-ttu-id="479d1-227">Wzorce, które mają adnotacje typu</span><span class="sxs-lookup"><span data-stu-id="479d1-227">Patterns That Have Type Annotations</span></span>

<span data-ttu-id="479d1-228">Wzorce mogą mieć adnotacje typu.</span><span class="sxs-lookup"><span data-stu-id="479d1-228">Patterns can have type annotations.</span></span> <span data-ttu-id="479d1-229">Zachowują się one tak jak inne adnotacje typu i w odróżnieniu od innych typów.</span><span class="sxs-lookup"><span data-stu-id="479d1-229">These behave like other type annotations and guide inference like other type annotations.</span></span> <span data-ttu-id="479d1-230">Nawiasy są wymagane wokół adnotacji typu w wzorcach.</span><span class="sxs-lookup"><span data-stu-id="479d1-230">Parentheses are required around type annotations in patterns.</span></span> <span data-ttu-id="479d1-231">Poniższy kod przedstawia wzorzec, który ma adnotację typu.</span><span class="sxs-lookup"><span data-stu-id="479d1-231">The following code shows a pattern that has a type annotation.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4815.fs)]

## <a name="type-test-pattern"></a><span data-ttu-id="479d1-232">Typ wzorca testu</span><span class="sxs-lookup"><span data-stu-id="479d1-232">Type Test Pattern</span></span>

<span data-ttu-id="479d1-233">Wzorzec testu typu jest używany do dopasowania danych wejściowych do typu.</span><span class="sxs-lookup"><span data-stu-id="479d1-233">The type test pattern is used to match the input against a type.</span></span> <span data-ttu-id="479d1-234">Jeśli typ danych wejściowych jest zgodny z (lub typem pochodnym) typu określonego we wzorcu, dopasowanie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="479d1-234">If the input type is a match to (or a derived type of) the type specified in the pattern, the match succeeds.</span></span>

<span data-ttu-id="479d1-235">Poniższy przykład demonstruje wzorzec testu typu.</span><span class="sxs-lookup"><span data-stu-id="479d1-235">The following example demonstrates the type test pattern.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4816.fs)]

<span data-ttu-id="479d1-236">Jeśli sprawdzasz tylko, czy identyfikator jest określonego typu pochodnego, nie potrzebujesz `as identifier` części wzorca, jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="479d1-236">If you're only checking if an identifier is of a particular derived type, you don't need the `as identifier` part of the pattern, as shown in the following example:</span></span>

```fsharp
type A() = class end
type B() = inherit A()
type C() = inherit A()

let m (a: A) =
    match a with
    | :? B -> printfn "It's a B"
    | :? C -> printfn "It's a C"
    | _ -> ()
```

## <a name="null-pattern"></a><span data-ttu-id="479d1-237">Wzorzec o wartości null</span><span class="sxs-lookup"><span data-stu-id="479d1-237">Null Pattern</span></span>

<span data-ttu-id="479d1-238">Wzorzec o wartości null jest zgodny z wartością null, która może pojawić się podczas pracy z typami, które zezwalają na wartość null.</span><span class="sxs-lookup"><span data-stu-id="479d1-238">The null pattern matches the null value that can appear when you are working with types that allow a null value.</span></span> <span data-ttu-id="479d1-239">Wzorce o wartości null są często używane podczas współdziałania z kodem .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="479d1-239">Null patterns are frequently used when interoperating with .NET Framework code.</span></span> <span data-ttu-id="479d1-240">Na przykład wartość zwracana przez interfejs API platformy .NET może być danymi wejściowymi do `match` wyrażenia.</span><span class="sxs-lookup"><span data-stu-id="479d1-240">For example, the return value of a .NET API might be the input to a `match` expression.</span></span> <span data-ttu-id="479d1-241">Można kontrolować przepływ programu w zależności od tego, czy zwracana wartość jest równa null, a także od innych cech zwracanej wartości.</span><span class="sxs-lookup"><span data-stu-id="479d1-241">You can control program flow based on whether the return value is null, and also on other characteristics of the returned value.</span></span> <span data-ttu-id="479d1-242">Możesz użyć wzorca o wartości null, aby zapobiec propagowaniu wartości null do reszty programu.</span><span class="sxs-lookup"><span data-stu-id="479d1-242">You can use the null pattern to prevent null values from propagating to the rest of your program.</span></span>

<span data-ttu-id="479d1-243">Poniższy przykład używa wzorca o wartości null i wzorca zmiennej.</span><span class="sxs-lookup"><span data-stu-id="479d1-243">The following example uses the null pattern and the variable pattern.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4817.fs)]

## <a name="nameof-pattern"></a><span data-ttu-id="479d1-244">Wzorzec nameof</span><span class="sxs-lookup"><span data-stu-id="479d1-244">Nameof pattern</span></span>

<span data-ttu-id="479d1-245">`nameof`Wzorzec jest zgodny z ciągiem, gdy jego wartość jest równa wyrażeniu, które następuje po `nameof` słowie kluczowym.</span><span class="sxs-lookup"><span data-stu-id="479d1-245">The `nameof` pattern matches against a string when its value is equal to the expression that follows the `nameof` keyword.</span></span> <span data-ttu-id="479d1-246">na przykład:</span><span class="sxs-lookup"><span data-stu-id="479d1-246">for example:</span></span>

```fsharp
let f (str: string) =
    match str with
    | nameof str -> "It's 'str'!"
    | _ -> "It is not 'str'!"

f "str" // matches
f "asdf" // does not match
```

<span data-ttu-id="479d1-247">Zapoznaj się z [`nameof`](nameof.md) operatorem, aby uzyskać informacje o tym, co można zrobić z nazwą.</span><span class="sxs-lookup"><span data-stu-id="479d1-247">See the [`nameof`](nameof.md) operator for information on what you can take a name of.</span></span>

## <a name="see-also"></a><span data-ttu-id="479d1-248">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="479d1-248">See also</span></span>

- [<span data-ttu-id="479d1-249">Wyrażenia dopasowania</span><span class="sxs-lookup"><span data-stu-id="479d1-249">Match Expressions</span></span>](match-expressions.md)
- [<span data-ttu-id="479d1-250">Wzorce aktywne</span><span class="sxs-lookup"><span data-stu-id="479d1-250">Active Patterns</span></span>](active-patterns.md)
- [<span data-ttu-id="479d1-251">Dokumentacja języka F #</span><span class="sxs-lookup"><span data-stu-id="479d1-251">F# Language Reference</span></span>](index.md)
