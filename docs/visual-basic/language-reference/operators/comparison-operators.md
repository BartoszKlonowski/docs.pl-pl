---
title: Operatory porównania
ms.date: 07/20/2015
f1_keywords:
- vb.<>
- vb.>=
- vb.<=
- vb.>
- vb.<
helpviewer_keywords:
- greater than or equal to operator [Visual Basic]
- '>= operator [Visual Basic]'
- = operator [Visual Basic]
- < operator [Visual Basic]
- less than operator [Visual Basic]
- relational operators [Visual Basic], syntax
- Like operator [Visual Basic]
- <> operator [Visual Basic]
- '> operator [Visual Basic]'
- equal operator [Visual Basic]
- less than or equal to operator [Visual Basic]
- symbols, operators
- greater than operator [Visual Basic]
- comparing values [Visual Basic]
- operators [Visual Basic], relational
- string comparison [Visual Basic]
- not equal to comparison operator [Visual Basic]
- <= operator [Visual Basic]
- operators [Visual Basic], comparison
- Is operator [Visual Basic]
- comparison operators [Visual Basic], Visual Basic
ms.assetid: d6cb12a8-e52e-46a7-8aaf-f804d634a825
ms.openlocfilehash: fcbb9052a79fa4b20b5a0f8fdc15de73d55a4281
ms.sourcegitcommit: d2db216e46323f73b32ae312c9e4135258e5d68e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "90873441"
---
# <a name="comparison-operators-visual-basic"></a><span data-ttu-id="34d25-102">Operatory porównania (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="34d25-102">Comparison Operators (Visual Basic)</span></span>

<span data-ttu-id="34d25-103">Poniżej przedstawiono operatory porównania zdefiniowane w Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="34d25-103">The following are the comparison operators defined in Visual Basic.</span></span>

 <span data-ttu-id="34d25-104">`<` zakład</span><span class="sxs-lookup"><span data-stu-id="34d25-104">`<` operator</span></span>

 <span data-ttu-id="34d25-105">`<=` zakład</span><span class="sxs-lookup"><span data-stu-id="34d25-105">`<=` operator</span></span>

 <span data-ttu-id="34d25-106">`>` zakład</span><span class="sxs-lookup"><span data-stu-id="34d25-106">`>` operator</span></span>

 <span data-ttu-id="34d25-107">`>=` zakład</span><span class="sxs-lookup"><span data-stu-id="34d25-107">`>=` operator</span></span>

 <span data-ttu-id="34d25-108">`=` zakład</span><span class="sxs-lookup"><span data-stu-id="34d25-108">`=` operator</span></span>

 <span data-ttu-id="34d25-109">`<>` zakład</span><span class="sxs-lookup"><span data-stu-id="34d25-109">`<>` operator</span></span>

 [<span data-ttu-id="34d25-110">Is, operator</span><span class="sxs-lookup"><span data-stu-id="34d25-110">Is Operator</span></span>](is-operator.md)

 [<span data-ttu-id="34d25-111">IsNot, operator</span><span class="sxs-lookup"><span data-stu-id="34d25-111">IsNot Operator</span></span>](isnot-operator.md)

 [<span data-ttu-id="34d25-112">Like — Operator</span><span class="sxs-lookup"><span data-stu-id="34d25-112">Like Operator</span></span>](like-operator.md)

 <span data-ttu-id="34d25-113">Te operatory porównują dwa wyrażenia, aby określić, czy są równe, i czy nie, jak się różnią.</span><span class="sxs-lookup"><span data-stu-id="34d25-113">These operators compare two expressions to determine whether or not they are equal, and if not, how they differ.</span></span> <span data-ttu-id="34d25-114">`Is`, `IsNot` i `Like` są szczegółowo omówione na oddzielnych stronach pomocy.</span><span class="sxs-lookup"><span data-stu-id="34d25-114">`Is`, `IsNot`, and `Like` are discussed in detail on separate Help pages.</span></span> <span data-ttu-id="34d25-115">Operatory porównujące relacyjne zostały szczegółowo omówione na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="34d25-115">The relational comparison operators are discussed in detail on this page.</span></span>

## <a name="syntax"></a><span data-ttu-id="34d25-116">Składnia</span><span class="sxs-lookup"><span data-stu-id="34d25-116">Syntax</span></span>
  
```vb
result = expression1 comparisonoperator expression2  
result = object1 [Is | IsNot] object2  
result = string Like pattern  
```  
  
## <a name="parts"></a><span data-ttu-id="34d25-117">Części</span><span class="sxs-lookup"><span data-stu-id="34d25-117">Parts</span></span>

 `result`  
 <span data-ttu-id="34d25-118">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="34d25-118">Required.</span></span> <span data-ttu-id="34d25-119">`Boolean`Wartość reprezentująca wynik porównania.</span><span class="sxs-lookup"><span data-stu-id="34d25-119">A `Boolean` value representing the result of the comparison.</span></span>

 <span data-ttu-id="34d25-120">`expression1`, `expression2`</span><span class="sxs-lookup"><span data-stu-id="34d25-120">`expression1`, `expression2`</span></span>  
 <span data-ttu-id="34d25-121">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="34d25-121">Required.</span></span> <span data-ttu-id="34d25-122">Dowolne wyrażenie.</span><span class="sxs-lookup"><span data-stu-id="34d25-122">Any expression.</span></span>

 `comparisonoperator`  
 <span data-ttu-id="34d25-123">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="34d25-123">Required.</span></span> <span data-ttu-id="34d25-124">Dowolny operator porównania relacyjnego.</span><span class="sxs-lookup"><span data-stu-id="34d25-124">Any relational comparison operator.</span></span>

 <span data-ttu-id="34d25-125">`object1`, `object2`</span><span class="sxs-lookup"><span data-stu-id="34d25-125">`object1`, `object2`</span></span>  
 <span data-ttu-id="34d25-126">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="34d25-126">Required.</span></span> <span data-ttu-id="34d25-127">Wszystkie nazwy obiektów odniesienia.</span><span class="sxs-lookup"><span data-stu-id="34d25-127">Any reference object names.</span></span>

 `string`  
 <span data-ttu-id="34d25-128">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="34d25-128">Required.</span></span> <span data-ttu-id="34d25-129">Dowolne `String` wyrażenie.</span><span class="sxs-lookup"><span data-stu-id="34d25-129">Any `String` expression.</span></span>

 `pattern`  
 <span data-ttu-id="34d25-130">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="34d25-130">Required.</span></span> <span data-ttu-id="34d25-131">Dowolne `String` wyrażenie lub zakres znaków.</span><span class="sxs-lookup"><span data-stu-id="34d25-131">Any `String` expression or range of characters.</span></span>

## <a name="remarks"></a><span data-ttu-id="34d25-132">Uwagi</span><span class="sxs-lookup"><span data-stu-id="34d25-132">Remarks</span></span>

 <span data-ttu-id="34d25-133">Poniższa tabela zawiera listę operatorów relacyjnych porównania i warunki, które określają, czy `result` jest `True` lub `False` .</span><span class="sxs-lookup"><span data-stu-id="34d25-133">The following table contains a list of the relational comparison operators and the conditions that determine whether `result` is `True` or `False`.</span></span>

|<span data-ttu-id="34d25-134">Operator</span><span class="sxs-lookup"><span data-stu-id="34d25-134">Operator</span></span>|<span data-ttu-id="34d25-135">`True` przypadku</span><span class="sxs-lookup"><span data-stu-id="34d25-135">`True` if</span></span>|<span data-ttu-id="34d25-136">`False` przypadku</span><span class="sxs-lookup"><span data-stu-id="34d25-136">`False` if</span></span>|
|--------------|---------------|----------------|
|<span data-ttu-id="34d25-137">`<` (Mniejsze niż)</span><span class="sxs-lookup"><span data-stu-id="34d25-137">`<` (Less than)</span></span>|`expression1` < `expression2`|`expression1` >= `expression2`|
|<span data-ttu-id="34d25-138">`<=` (Mniejsze niż lub równe)</span><span class="sxs-lookup"><span data-stu-id="34d25-138">`<=` (Less than or equal to)</span></span>|`expression1` <= `expression2`|`expression1` > `expression2`|
|<span data-ttu-id="34d25-139">`>` (Większe niż)</span><span class="sxs-lookup"><span data-stu-id="34d25-139">`>` (Greater than)</span></span>|`expression1` > `expression2`|`expression1` <= `expression2`|
|<span data-ttu-id="34d25-140">`>=` (Większe niż lub równe)</span><span class="sxs-lookup"><span data-stu-id="34d25-140">`>=` (Greater than or equal to)</span></span>|`expression1` >= `expression2`|`expression1` < `expression2`|
|<span data-ttu-id="34d25-141">`=` (Równe)</span><span class="sxs-lookup"><span data-stu-id="34d25-141">`=` (Equal to)</span></span>|`expression1` = `expression2`|`expression1` <> `expression2`|
|<span data-ttu-id="34d25-142">`<>` (Nie równa się)</span><span class="sxs-lookup"><span data-stu-id="34d25-142">`<>` (Not equal to)</span></span>|`expression1` <> `expression2`|`expression1` = `expression2`|

> [!NOTE]
> <span data-ttu-id="34d25-143">[Operator =](assignment-operator.md) jest również używany jako operator przypisania.</span><span class="sxs-lookup"><span data-stu-id="34d25-143">The [= Operator](assignment-operator.md) is also used as an assignment operator.</span></span>

 <span data-ttu-id="34d25-144">`Is`Operator, `IsNot` operator i `Like` operator mają określone funkcje porównania, które różnią się od operatorów w powyższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="34d25-144">The `Is` operator, the `IsNot` operator, and the `Like` operator have specific comparison functionalities that differ from the operators in the preceding table.</span></span>

## <a name="comparing-numbers"></a><span data-ttu-id="34d25-145">Porównywanie liczb</span><span class="sxs-lookup"><span data-stu-id="34d25-145">Comparing Numbers</span></span>

 <span data-ttu-id="34d25-146">W przypadku porównania wyrażenia typu `Single` z jednym z typów `Double` `Single` wyrażenie jest konwertowane na `Double` .</span><span class="sxs-lookup"><span data-stu-id="34d25-146">When you compare an expression of type `Single` to one of type `Double`, the `Single` expression is converted to `Double`.</span></span> <span data-ttu-id="34d25-147">Takie zachowanie jest przeciwieństwem do zachowania znalezionego w Visual Basic 6.</span><span class="sxs-lookup"><span data-stu-id="34d25-147">This behavior is opposite to the behavior found in Visual Basic 6.</span></span>

 <span data-ttu-id="34d25-148">Podobnie, podczas porównywania wyrażenia typu `Decimal` z wyrażeniem typu `Single` lub wyrażenie `Double` `Decimal` jest konwertowane na `Single` lub `Double` .</span><span class="sxs-lookup"><span data-stu-id="34d25-148">Similarly, when you compare an expression of type `Decimal` to an expression of type `Single` or `Double`, the `Decimal` expression is converted to `Single` or `Double`.</span></span> <span data-ttu-id="34d25-149">W przypadku `Decimal` wyrażeń, każda wartość ułamkowa mniejsza od 1e-28 może zostać utracona.</span><span class="sxs-lookup"><span data-stu-id="34d25-149">For `Decimal` expressions, any fractional value less than 1E-28 might be lost.</span></span> <span data-ttu-id="34d25-150">Taka ułamkowa utrata wartości może spowodować, że dwie wartości będą porównywane jako równe, gdy nie są.</span><span class="sxs-lookup"><span data-stu-id="34d25-150">Such fractional value loss may cause two values to compare as equal when they are not.</span></span> <span data-ttu-id="34d25-151">Z tego powodu należy zadbać o to, aby przy użyciu równości ( `=` ) porównać dwie zmienne zmiennoprzecinkowe.</span><span class="sxs-lookup"><span data-stu-id="34d25-151">For this reason, you should take care when using equality (`=`) to compare two floating-point variables.</span></span> <span data-ttu-id="34d25-152">Jest bezpieczniejsze, aby sprawdzić, czy wartość bezwzględna różnicy między dwoma liczbami jest mniejsza niż mała akceptowalna tolerancja.</span><span class="sxs-lookup"><span data-stu-id="34d25-152">It is safer to test whether the absolute value of the difference between the two numbers is less than a small acceptable tolerance.</span></span>

### <a name="floating-point-imprecision"></a><span data-ttu-id="34d25-153">Niedokładność zmiennoprzecinkowa</span><span class="sxs-lookup"><span data-stu-id="34d25-153">Floating-point Imprecision</span></span>

 <span data-ttu-id="34d25-154">Podczas pracy z liczbami zmiennoprzecinkowymi należy pamiętać, że nie zawsze mają dokładną reprezentację w pamięci.</span><span class="sxs-lookup"><span data-stu-id="34d25-154">When you work with floating-point numbers, keep in mind that they do not always have a precise representation in memory.</span></span> <span data-ttu-id="34d25-155">Może to prowadzić do nieoczekiwanych wyników niektórych operacji, takich jak porównanie wartości i [operator mod](mod-operator.md).</span><span class="sxs-lookup"><span data-stu-id="34d25-155">This could lead to unexpected results from certain operations, such as value comparison and the [Mod Operator](mod-operator.md).</span></span> <span data-ttu-id="34d25-156">Aby uzyskać więcej informacji, zobacz [Rozwiązywanie problemów z typami danych](../../programming-guide/language-features/data-types/troubleshooting-data-types.md).</span><span class="sxs-lookup"><span data-stu-id="34d25-156">For more information, see [Troubleshooting Data Types](../../programming-guide/language-features/data-types/troubleshooting-data-types.md).</span></span>

## <a name="comparing-strings"></a><span data-ttu-id="34d25-157">Porównywanie ciągów</span><span class="sxs-lookup"><span data-stu-id="34d25-157">Comparing Strings</span></span>

 <span data-ttu-id="34d25-158">Podczas porównywania ciągów wyrażenia ciągów są oceniane na podstawie alfabetycznej kolejności sortowania, która zależy od `Option Compare` Ustawienia.</span><span class="sxs-lookup"><span data-stu-id="34d25-158">When you compare strings, the string expressions are evaluated based on their alphabetical sort order, which depends on the `Option Compare` setting.</span></span>

 <span data-ttu-id="34d25-159">`Option Compare Binary` podstaw porównania ciągów w kolejności sortowania pochodzącej od wewnętrznych reprezentacji binarnych znaków.</span><span class="sxs-lookup"><span data-stu-id="34d25-159">`Option Compare Binary` bases string comparisons on a sort order derived from the internal binary representations of the characters.</span></span> <span data-ttu-id="34d25-160">Kolejność sortowania jest określana na podstawie strony kodowej.</span><span class="sxs-lookup"><span data-stu-id="34d25-160">The sort order is determined by the code page.</span></span> <span data-ttu-id="34d25-161">W poniższym przykładzie przedstawiono typowy binarny porządek sortowania.</span><span class="sxs-lookup"><span data-stu-id="34d25-161">The following example shows a typical binary sort order.</span></span>

 `A < B < E < Z < a < b < e < z < À < Ê < Ø < à < ê < ø`

 <span data-ttu-id="34d25-162">`Option Compare Text` podstawowe porównania ciągów w przypadku, w którym rozróżniana jest wielkość liter, porządek sortowania w postaci tekstu określony przez ustawienia regionalne Twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="34d25-162">`Option Compare Text` bases string comparisons on a case-insensitive, textual sort order determined by your application's locale.</span></span> <span data-ttu-id="34d25-163">Po ustawieniu `Option Compare Text` i posortowaniu znaków w poprzednim przykładzie stosuje się następujący porządek sortowania tekstu:</span><span class="sxs-lookup"><span data-stu-id="34d25-163">When you set `Option Compare Text` and sort the characters in the preceding example, the following text sort order applies:</span></span>

 `(A=a) < (À= à) < (B=b) < (E=e) < (Ê= ê) < (Ø = ø) < (Z=z)`

### <a name="locale-dependence"></a><span data-ttu-id="34d25-164">Zależność ustawień regionalnych</span><span class="sxs-lookup"><span data-stu-id="34d25-164">Locale Dependence</span></span>

 <span data-ttu-id="34d25-165">Po ustawieniu `Option Compare Text` wynik porównania ciągów może zależeć od ustawień regionalnych, w których działa aplikacja.</span><span class="sxs-lookup"><span data-stu-id="34d25-165">When you set `Option Compare Text`, the result of a string comparison can depend on the locale in which the application is running.</span></span> <span data-ttu-id="34d25-166">Dwa znaki mogą być porównywane jako równe w jednej lokalizacji, ale nie w innym.</span><span class="sxs-lookup"><span data-stu-id="34d25-166">Two characters might compare as equal in one locale but not in another.</span></span> <span data-ttu-id="34d25-167">Jeśli używasz porównania ciągów, aby podejmować ważne decyzje, na przykład czy należy zaakceptować próbę zalogowania, należy ostrzec o czułości ustawień regionalnych.</span><span class="sxs-lookup"><span data-stu-id="34d25-167">If you are using a string comparison to make important decisions, such as whether to accept an attempt to log on, you should be alert to locale sensitivity.</span></span> <span data-ttu-id="34d25-168">Rozważ ustawienie `Option Compare Binary` lub wywołanie metody <xref:Microsoft.VisualBasic.Strings.StrComp%2A> , która przyjmuje ustawienia regionalne.</span><span class="sxs-lookup"><span data-stu-id="34d25-168">Consider either setting `Option Compare Binary` or calling the <xref:Microsoft.VisualBasic.Strings.StrComp%2A>, which takes the locale into account.</span></span>

## <a name="typeless-programming-with-relational-comparison-operators"></a><span data-ttu-id="34d25-169">Programowanie bez typu z relacyjnymi operatorami porównania</span><span class="sxs-lookup"><span data-stu-id="34d25-169">Typeless Programming with Relational Comparison Operators</span></span>

 <span data-ttu-id="34d25-170">Użycie operatorów porównania relacyjnego z `Object` wyrażeniami jest niedozwolone w `Option Strict On` .</span><span class="sxs-lookup"><span data-stu-id="34d25-170">The use of relational comparison operators with `Object` expressions is not allowed under `Option Strict On`.</span></span> <span data-ttu-id="34d25-171">Gdy `Option Strict` jest `Off` , i albo `expression1` `expression2` jest `Object` wyrażeniem, typy czasu wykonywania określają, jak są porównywane.</span><span class="sxs-lookup"><span data-stu-id="34d25-171">When `Option Strict` is `Off`, and either `expression1` or `expression2` is an `Object` expression, the run-time types determine how they are compared.</span></span> <span data-ttu-id="34d25-172">W poniższej tabeli przedstawiono, w jaki sposób wyrażenia są porównywane i wynik porównania, w zależności od typu czasu wykonywania argumentów operacji.</span><span class="sxs-lookup"><span data-stu-id="34d25-172">The following table shows how the expressions are compared and the result from the comparison, depending on the runtime type of the operands.</span></span>

|<span data-ttu-id="34d25-173">Jeśli operandy są</span><span class="sxs-lookup"><span data-stu-id="34d25-173">If operands are</span></span>|<span data-ttu-id="34d25-174">Porównanie jest</span><span class="sxs-lookup"><span data-stu-id="34d25-174">Comparison is</span></span>|
|---------------------|-------------------|
|<span data-ttu-id="34d25-175">Jedn `String`</span><span class="sxs-lookup"><span data-stu-id="34d25-175">Both `String`</span></span>|<span data-ttu-id="34d25-176">Porównanie sortowania na podstawie charakterystyki sortowania ciągów.</span><span class="sxs-lookup"><span data-stu-id="34d25-176">Sort comparison based on string sorting characteristics.</span></span>|
|<span data-ttu-id="34d25-177">Zarówno liczbowe</span><span class="sxs-lookup"><span data-stu-id="34d25-177">Both numeric</span></span>|<span data-ttu-id="34d25-178">Obiekty konwertowane na `Double` , porównywanie numeryczne.</span><span class="sxs-lookup"><span data-stu-id="34d25-178">Objects converted to `Double`, numeric comparison.</span></span>|
|<span data-ttu-id="34d25-179">Jeden i jeden `String`</span><span class="sxs-lookup"><span data-stu-id="34d25-179">One numeric and one `String`</span></span>|<span data-ttu-id="34d25-180">`String`Jest konwertowany na `Double` i jest wykonywane porównywanie numeryczne.</span><span class="sxs-lookup"><span data-stu-id="34d25-180">The `String` is converted to a `Double` and numeric comparison is performed.</span></span> <span data-ttu-id="34d25-181">Jeśli `String` nie można przekonwertować na `Double` , <xref:System.InvalidCastException> zostanie zgłoszony.</span><span class="sxs-lookup"><span data-stu-id="34d25-181">If the `String` cannot be converted to `Double`, an <xref:System.InvalidCastException> is thrown.</span></span>|
|<span data-ttu-id="34d25-182">Oba lub oba są typami odwołań innym niż `String`</span><span class="sxs-lookup"><span data-stu-id="34d25-182">Either or both are reference types other than `String`</span></span>|<span data-ttu-id="34d25-183"><xref:System.InvalidCastException>Jest zgłaszany.</span><span class="sxs-lookup"><span data-stu-id="34d25-183">An <xref:System.InvalidCastException> is thrown.</span></span>|

 <span data-ttu-id="34d25-184">Porównania liczbowe traktują się `Nothing` jako 0.</span><span class="sxs-lookup"><span data-stu-id="34d25-184">Numeric comparisons treat `Nothing` as 0.</span></span> <span data-ttu-id="34d25-185">Porównania ciągów traktują `Nothing` jako `""` (pusty ciąg).</span><span class="sxs-lookup"><span data-stu-id="34d25-185">String comparisons treat `Nothing` as `""` (an empty string).</span></span>

## <a name="overloading"></a><span data-ttu-id="34d25-186">Przeciążenie</span><span class="sxs-lookup"><span data-stu-id="34d25-186">Overloading</span></span>

 <span data-ttu-id="34d25-187">Operatory porównania relacyjnego ( `<` .</span><span class="sxs-lookup"><span data-stu-id="34d25-187">The relational comparison operators (`<`.</span></span> <span data-ttu-id="34d25-188">`<=`, `>` ,,, `>=` `=` `<>` ) może być *przeciążona*, co oznacza, że Klasa lub struktura mogą definiować ich zachowanie, gdy operand ma typ tej klasy lub struktury.</span><span class="sxs-lookup"><span data-stu-id="34d25-188">`<=`, `>`, `>=`, `=`, `<>`) can be *overloaded*, which means that a class or structure can redefine their behavior when an operand has the type of that class or structure.</span></span> <span data-ttu-id="34d25-189">Jeśli kod używa dowolnego z tych operatorów w takiej klasie lub strukturze, pamiętaj o tym, aby zrozumieć zachowanie, które zostało ponownie zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="34d25-189">If your code uses any of these operators on such a class or structure, be sure you understand the redefined behavior.</span></span> <span data-ttu-id="34d25-190">Aby uzyskać więcej informacji, zobacz [procedury operatorów](../../programming-guide/language-features/procedures/operator-procedures.md).</span><span class="sxs-lookup"><span data-stu-id="34d25-190">For more information, see [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md).</span></span>

 <span data-ttu-id="34d25-191">Należy zauważyć, że [operator =](assignment-operator.md) może być przeciążony tylko jako operator porównania relacyjnego, a nie jako operator przypisania.</span><span class="sxs-lookup"><span data-stu-id="34d25-191">Notice that the [= Operator](assignment-operator.md) can be overloaded only as a relational comparison operator, not as an assignment operator.</span></span>

## <a name="example"></a><span data-ttu-id="34d25-192">Przykład</span><span class="sxs-lookup"><span data-stu-id="34d25-192">Example</span></span>

 <span data-ttu-id="34d25-193">W poniższym przykładzie pokazano różne zastosowania relacyjnych operatorów porównania, które służą do porównywania wyrażeń.</span><span class="sxs-lookup"><span data-stu-id="34d25-193">The following example shows various uses of relational comparison operators, which you use to compare expressions.</span></span> <span data-ttu-id="34d25-194">Relacyjne operatory porównujące zwracają `Boolean` wynik, który reprezentuje, czy wyrażenie podane ma wartość `True` .</span><span class="sxs-lookup"><span data-stu-id="34d25-194">Relational comparison operators return a `Boolean` result that represents whether or not the stated expression evaluates to `True`.</span></span> <span data-ttu-id="34d25-195">Gdy `>` Operatory i są stosowane `<` do ciągów, porównanie jest wykonywane przy użyciu zwykłej alfabetycznej kolejności sortowania ciągów.</span><span class="sxs-lookup"><span data-stu-id="34d25-195">When you apply the `>` and `<` operators to strings, the comparison is made using the normal alphabetical sorting order of the strings.</span></span> <span data-ttu-id="34d25-196">Ta kolejność może być zależna od ustawień regionalnych.</span><span class="sxs-lookup"><span data-stu-id="34d25-196">This order can be dependent on your locale setting.</span></span> <span data-ttu-id="34d25-197">Czy sortowanie jest rozróżniana wielkość liter, czy nie jest zależne od [opcji Porównaj](../statements/option-compare-statement.md) ustawienia.</span><span class="sxs-lookup"><span data-stu-id="34d25-197">Whether the sort is case-sensitive or not depends on the [Option Compare](../statements/option-compare-statement.md) setting.</span></span>

 [!code-vb[VbVbalrOperators#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#1)]

 <span data-ttu-id="34d25-198">W poprzednim przykładzie pierwsze porównanie zwraca, `False` a pozostałe porównania zwracają `True` .</span><span class="sxs-lookup"><span data-stu-id="34d25-198">In the preceding example, the first comparison returns `False` and the remaining comparisons return `True`.</span></span>

## <a name="see-also"></a><span data-ttu-id="34d25-199">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="34d25-199">See also</span></span>

- <xref:System.InvalidCastException>
- [<span data-ttu-id="34d25-200">= — Operator</span><span class="sxs-lookup"><span data-stu-id="34d25-200">= Operator</span></span>](assignment-operator.md)
- [<span data-ttu-id="34d25-201">Kolejność wykonywania działań (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="34d25-201">Operator Precedence in Visual Basic</span></span>](operator-precedence.md)
- [<span data-ttu-id="34d25-202">Operatory według funkcji</span><span class="sxs-lookup"><span data-stu-id="34d25-202">Operators Listed by Functionality</span></span>](operators-listed-by-functionality.md)
- [<span data-ttu-id="34d25-203">Rozwiązywanie problemów związanych z typami danych</span><span class="sxs-lookup"><span data-stu-id="34d25-203">Troubleshooting Data Types</span></span>](../../programming-guide/language-features/data-types/troubleshooting-data-types.md)
- [<span data-ttu-id="34d25-204">Operatory porównania w Visual Basic</span><span class="sxs-lookup"><span data-stu-id="34d25-204">Comparison Operators in Visual Basic</span></span>](../../programming-guide/language-features/operators-and-expressions/comparison-operators.md)
