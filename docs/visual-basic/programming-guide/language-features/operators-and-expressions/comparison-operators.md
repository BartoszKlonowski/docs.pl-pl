---
title: Operatory porównania
ms.date: 07/20/2015
helpviewer_keywords:
- comparison operators [Visual Basic], comparing strings
- comparison operators [Visual Basic], comparing objects
- strings [Visual Basic], comparing
- comparison operators [Visual Basic]
- string comparison [Visual Basic], operators
- objects [Visual Basic], comparing
- numbers [Visual Basic], comparing
- Visual Basic code, operators
- string comparison [Visual Basic]
- numeric values [Visual Basic], comparing
- comparison operators [Visual Basic], comparing numeric values
- operators [Visual Basic], comparison
ms.assetid: 0b570339-5407-474f-8421-e183a8b303ee
ms.openlocfilehash: fbe81532bb435e54e694f9b5fe9dd497392f31e1
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/23/2020
ms.locfileid: "91071771"
---
# <a name="comparison-operators-in-visual-basic"></a><span data-ttu-id="4cca3-102">Operatory porównania w Visual Basic</span><span class="sxs-lookup"><span data-stu-id="4cca3-102">Comparison Operators in Visual Basic</span></span>

<span data-ttu-id="4cca3-103">Operatory porównania porównują dwa wyrażenia i zwracają `Boolean` wartość, która reprezentuje relację ich wartości.</span><span class="sxs-lookup"><span data-stu-id="4cca3-103">Comparison operators compare two expressions and return a `Boolean` value that represents the relationship of their values.</span></span> <span data-ttu-id="4cca3-104">Istnieją operatory do porównywania wartości liczbowych, operatorów do porównywania ciągów i operatorów do porównywania obiektów.</span><span class="sxs-lookup"><span data-stu-id="4cca3-104">There are operators for comparing numeric values, operators for comparing strings, and operators for comparing objects.</span></span> <span data-ttu-id="4cca3-105">Wszystkie trzy typy operatorów zostały omówione w tym dokumencie.</span><span class="sxs-lookup"><span data-stu-id="4cca3-105">All three types of operators are discussed herein.</span></span>  
  
## <a name="comparing-numeric-values"></a><span data-ttu-id="4cca3-106">Porównywanie wartości liczbowych</span><span class="sxs-lookup"><span data-stu-id="4cca3-106">Comparing Numeric Values</span></span>  

 <span data-ttu-id="4cca3-107">Visual Basic porównuje wartości liczbowe przy użyciu sześciu liczbowych operatorów porównywania.</span><span class="sxs-lookup"><span data-stu-id="4cca3-107">Visual Basic compares numeric values using six numeric comparison operators.</span></span> <span data-ttu-id="4cca3-108">Każdy operator przyjmuje jako operandy dwa wyrażenia, które obliczają wartości numeryczne.</span><span class="sxs-lookup"><span data-stu-id="4cca3-108">Each operator takes as operands two expressions that evaluate to numeric values.</span></span> <span data-ttu-id="4cca3-109">W poniższej tabeli przedstawiono operatory i przedstawiono przykłady poszczególnych elementów.</span><span class="sxs-lookup"><span data-stu-id="4cca3-109">The following table lists the operators and shows examples of each.</span></span>  
  
|<span data-ttu-id="4cca3-110">Operator</span><span class="sxs-lookup"><span data-stu-id="4cca3-110">Operator</span></span>|<span data-ttu-id="4cca3-111">Testowany warunek</span><span class="sxs-lookup"><span data-stu-id="4cca3-111">Condition tested</span></span>|<span data-ttu-id="4cca3-112">Przykłady</span><span class="sxs-lookup"><span data-stu-id="4cca3-112">Examples</span></span>|  
|--------------|----------------------|--------------|  
|<span data-ttu-id="4cca3-113">`=` Kryteri</span><span class="sxs-lookup"><span data-stu-id="4cca3-113">`=` (Equality)</span></span>|<span data-ttu-id="4cca3-114">Czy wartość pierwszego wyrażenia jest równa wartości sekundy?</span><span class="sxs-lookup"><span data-stu-id="4cca3-114">Is the value of the first expression equal to the value of the second?</span></span>|<span data-ttu-id="4cca3-115">`23`   `=`   `33    ' False`</span><span class="sxs-lookup"><span data-stu-id="4cca3-115">`23`   `=`   `33    ' False`</span></span><br /><br /> <span data-ttu-id="4cca3-116">`23`   `=`   `23    ' True`</span><span class="sxs-lookup"><span data-stu-id="4cca3-116">`23`   `=`   `23    ' True`</span></span><br /><br /> <span data-ttu-id="4cca3-117">`23`   `=`   `12    ' False`</span><span class="sxs-lookup"><span data-stu-id="4cca3-117">`23`   `=`   `12    ' False`</span></span>|  
|<span data-ttu-id="4cca3-118">`<>` Nierówności</span><span class="sxs-lookup"><span data-stu-id="4cca3-118">`<>` (Inequality)</span></span>|<span data-ttu-id="4cca3-119">Czy wartość pierwszego wyrażenia jest nierówna wartości sekundy?</span><span class="sxs-lookup"><span data-stu-id="4cca3-119">Is the value of the first expression unequal to the value of the second?</span></span>|<span data-ttu-id="4cca3-120">`23`   `<>`   `33    ' True`</span><span class="sxs-lookup"><span data-stu-id="4cca3-120">`23`   `<>`   `33    ' True`</span></span><br /><br /> <span data-ttu-id="4cca3-121">`23`   `<>`   `23    ' False`</span><span class="sxs-lookup"><span data-stu-id="4cca3-121">`23`   `<>`   `23    ' False`</span></span><br /><br /> <span data-ttu-id="4cca3-122">`23`   `<>`   `12    ' True`</span><span class="sxs-lookup"><span data-stu-id="4cca3-122">`23`   `<>`   `12    ' True`</span></span>|  
|<span data-ttu-id="4cca3-123">`<` (Mniejsze niż)</span><span class="sxs-lookup"><span data-stu-id="4cca3-123">`<` (Less than)</span></span>|<span data-ttu-id="4cca3-124">Czy wartość pierwszego wyrażenia jest mniejsza niż wartość drugiego?</span><span class="sxs-lookup"><span data-stu-id="4cca3-124">Is the value of the first expression less than the value of the second?</span></span>|<span data-ttu-id="4cca3-125">`23`   `<`   `33    ' True`</span><span class="sxs-lookup"><span data-stu-id="4cca3-125">`23`   `<`   `33    ' True`</span></span><br /><br /> <span data-ttu-id="4cca3-126">`23`   `<`   `23    ' False`</span><span class="sxs-lookup"><span data-stu-id="4cca3-126">`23`   `<`   `23    ' False`</span></span><br /><br /> <span data-ttu-id="4cca3-127">`23`   `<`   `12    ' False`</span><span class="sxs-lookup"><span data-stu-id="4cca3-127">`23`   `<`   `12    ' False`</span></span>|  
|<span data-ttu-id="4cca3-128">`>` (Większe niż)</span><span class="sxs-lookup"><span data-stu-id="4cca3-128">`>` (Greater than)</span></span>|<span data-ttu-id="4cca3-129">Czy wartość pierwszego wyrażenia jest większa niż wartość drugiego?</span><span class="sxs-lookup"><span data-stu-id="4cca3-129">Is the value of the first expression greater than the value of the second?</span></span>|<span data-ttu-id="4cca3-130">`23`   `>`   `33    ' False`</span><span class="sxs-lookup"><span data-stu-id="4cca3-130">`23`   `>`   `33    ' False`</span></span><br /><br /> <span data-ttu-id="4cca3-131">`23`   `>`   `23    ' False`</span><span class="sxs-lookup"><span data-stu-id="4cca3-131">`23`   `>`   `23    ' False`</span></span><br /><br /> <span data-ttu-id="4cca3-132">`23`   `>`   `12    ' True`</span><span class="sxs-lookup"><span data-stu-id="4cca3-132">`23`   `>`   `12    ' True`</span></span>|  
|<span data-ttu-id="4cca3-133">`<=` (Mniejsze niż lub równe)</span><span class="sxs-lookup"><span data-stu-id="4cca3-133">`<=` (Less than or equal to)</span></span>|<span data-ttu-id="4cca3-134">Czy wartość pierwszego wyrażenia jest mniejsza lub równa wartości sekundy?</span><span class="sxs-lookup"><span data-stu-id="4cca3-134">Is the value of the first expression less than or equal to the value of the second?</span></span>|<span data-ttu-id="4cca3-135">`23`   `<=`   `33    ' True`</span><span class="sxs-lookup"><span data-stu-id="4cca3-135">`23`   `<=`   `33    ' True`</span></span><br /><br /> <span data-ttu-id="4cca3-136">`23`   `<=`   `23    ' True`</span><span class="sxs-lookup"><span data-stu-id="4cca3-136">`23`   `<=`   `23    ' True`</span></span><br /><br /> <span data-ttu-id="4cca3-137">`23`   `<=`   `12    ' False`</span><span class="sxs-lookup"><span data-stu-id="4cca3-137">`23`   `<=`   `12    ' False`</span></span>|  
|<span data-ttu-id="4cca3-138">`>=` (Większe niż lub równe)</span><span class="sxs-lookup"><span data-stu-id="4cca3-138">`>=` (Greater than or equal to)</span></span>|<span data-ttu-id="4cca3-139">Czy wartość pierwszego wyrażenia jest większa niż lub równa wartości sekundy?</span><span class="sxs-lookup"><span data-stu-id="4cca3-139">Is the value of the first expression greater than or equal to the value of the second?</span></span>|<span data-ttu-id="4cca3-140">`23`   `>=`   `33    ' False`</span><span class="sxs-lookup"><span data-stu-id="4cca3-140">`23`   `>=`   `33    ' False`</span></span><br /><br /> <span data-ttu-id="4cca3-141">`23`   `>=`   `23    ' True`</span><span class="sxs-lookup"><span data-stu-id="4cca3-141">`23`   `>=`   `23    ' True`</span></span><br /><br /> <span data-ttu-id="4cca3-142">`23`   `>=`   `12    ' True`</span><span class="sxs-lookup"><span data-stu-id="4cca3-142">`23`   `>=`   `12    ' True`</span></span>|  
  
## <a name="comparing-strings"></a><span data-ttu-id="4cca3-143">Porównywanie ciągów</span><span class="sxs-lookup"><span data-stu-id="4cca3-143">Comparing Strings</span></span>  

 <span data-ttu-id="4cca3-144">Visual Basic porównuje ciągi przy użyciu [operatora like](../../../language-reference/operators/like-operator.md) oraz liczbowych operatorów porównania.</span><span class="sxs-lookup"><span data-stu-id="4cca3-144">Visual Basic compares strings using the [Like Operator](../../../language-reference/operators/like-operator.md) as well as the numeric comparison operators.</span></span> <span data-ttu-id="4cca3-145">`Like`Operator pozwala określić wzorzec.</span><span class="sxs-lookup"><span data-stu-id="4cca3-145">The `Like` operator allows you to specify a pattern.</span></span> <span data-ttu-id="4cca3-146">Ciąg jest porównywany z wzorcem i jeśli jest zgodny, wynik jest `True` .</span><span class="sxs-lookup"><span data-stu-id="4cca3-146">The string is then compared against the pattern, and if it matches, the result is `True`.</span></span> <span data-ttu-id="4cca3-147">W przeciwnym razie wynik jest `False` .</span><span class="sxs-lookup"><span data-stu-id="4cca3-147">Otherwise, the result is `False`.</span></span> <span data-ttu-id="4cca3-148">Operatory liczbowe umożliwiają porównywanie `String` wartości na podstawie ich kolejności sortowania, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="4cca3-148">The numeric operators allow you to compare `String` values based on their sort order, as the following example shows.</span></span>  
  
 `"73" < "9"`  
  
 `' The result of the preceding comparison is True.`  
  
 <span data-ttu-id="4cca3-149">Wynikiem powyższego przykładu jest to `True` , że pierwszy znak w pierwszym ciągu sortuje przed pierwszym znakiem w drugim ciągu.</span><span class="sxs-lookup"><span data-stu-id="4cca3-149">The result in the preceding example is `True` because the first character in the first string sorts before the first character in the second string.</span></span> <span data-ttu-id="4cca3-150">Jeśli pierwsze znaki były równe, porównywanie będzie kontynuowane do następnego znaku w obu ciągach i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="4cca3-150">If the first characters were equal, the comparison would continue to the next character in both strings, and so on.</span></span> <span data-ttu-id="4cca3-151">Można również testować równość ciągów przy użyciu operatora równości, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="4cca3-151">You can also test equality of strings using the equality operator, as the following example shows.</span></span>  
  
 `"734" = "734"`  
  
 `' The result of the preceding comparison is True.`  
  
 <span data-ttu-id="4cca3-152">Jeśli jeden ciąg jest prefiksem innego, na przykład "AA" i "aaa", dłuższy ciąg jest traktowany jako większy niż krótszy ciąg.</span><span class="sxs-lookup"><span data-stu-id="4cca3-152">If one string is a prefix of another, such as "aa" and "aaa", the longer string is considered to be greater than the shorter string.</span></span> <span data-ttu-id="4cca3-153">Ilustruje to poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="4cca3-153">The following example illustrates this.</span></span>  
  
 `"aaa" > "aa"`  
  
 `' The result of the preceding comparison is True.`  
  
 <span data-ttu-id="4cca3-154">Kolejność sortowania jest oparta na porównaniu binarnej lub porównującej tekst w zależności od ustawienia `Option Compare` .</span><span class="sxs-lookup"><span data-stu-id="4cca3-154">The sort order is based on either a binary comparison or a textual comparison depending on the setting of `Option Compare`.</span></span> <span data-ttu-id="4cca3-155">Aby uzyskać więcej informacji, zobacz [opcja porównania instrukcji](../../../language-reference/statements/option-compare-statement.md).</span><span class="sxs-lookup"><span data-stu-id="4cca3-155">For more information see [Option Compare Statement](../../../language-reference/statements/option-compare-statement.md).</span></span>  
  
## <a name="comparing-objects"></a><span data-ttu-id="4cca3-156">Porównywanie obiektów</span><span class="sxs-lookup"><span data-stu-id="4cca3-156">Comparing Objects</span></span>  

 <span data-ttu-id="4cca3-157">Visual Basic porównuje dwie zmienne odwołań do obiektów z [operatorem is](../../../language-reference/operators/is-operator.md) i [operatorem IsNot](../../../language-reference/operators/isnot-operator.md).</span><span class="sxs-lookup"><span data-stu-id="4cca3-157">Visual Basic compares two object reference variables with the [Is Operator](../../../language-reference/operators/is-operator.md) and the [IsNot Operator](../../../language-reference/operators/isnot-operator.md).</span></span> <span data-ttu-id="4cca3-158">Można użyć dowolnego z tych operatorów, aby określić, czy dwie zmienne referencyjne odwołują się do tego samego wystąpienia obiektu.</span><span class="sxs-lookup"><span data-stu-id="4cca3-158">You can use either of these operators to determine if two reference variables refer to the same object instance.</span></span> <span data-ttu-id="4cca3-159">Ilustruje to poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="4cca3-159">The following example illustrates this.</span></span>  
  
 [!code-vb[VbVbalrOperators#65](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#65)]  
  
 <span data-ttu-id="4cca3-160">W poprzednim przykładzie `x Is y` jest to wynikiem `True` , ponieważ obie zmienne odwołują się do tego samego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="4cca3-160">In the preceding example, `x Is y` evaluates to `True`, because both variables refer to the same instance.</span></span> <span data-ttu-id="4cca3-161">Ten wynik należy do poniższego przykładu.</span><span class="sxs-lookup"><span data-stu-id="4cca3-161">Contrast this result with the following example.</span></span>  
  
 [!code-vb[VbVbalrOperators#66](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#66)]  
  
 <span data-ttu-id="4cca3-162">W poprzednim przykładzie `x Is y` jest to wynikiem `False` , ponieważ chociaż zmienne odwołują się do obiektów tego samego typu, odwołują się do różnych wystąpień tego typu.</span><span class="sxs-lookup"><span data-stu-id="4cca3-162">In the preceding example, `x Is y` evaluates to `False`, because although the variables refer to objects of the same type, they refer to different instances of that type.</span></span>  
  
 <span data-ttu-id="4cca3-163">Jeśli chcesz przeprowadzić test dla dwóch obiektów, które nie wskazują tego samego wystąpienia, `IsNot` operator pozwala uniknąć Clumsy z `Not` i `Is` .</span><span class="sxs-lookup"><span data-stu-id="4cca3-163">When you want to test for two objects not pointing to the same instance, the `IsNot` operator lets you avoid a grammatically clumsy combination of `Not` and `Is`.</span></span> <span data-ttu-id="4cca3-164">Ilustruje to poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="4cca3-164">The following example illustrates this.</span></span>  
  
 [!code-vb[VbVbalrOperators#67](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#67)]  
  
 <span data-ttu-id="4cca3-165">W poprzednim przykładzie `If a IsNot b` jest równoważne `If Not a Is b` .</span><span class="sxs-lookup"><span data-stu-id="4cca3-165">In the preceding example, `If a IsNot b` is equivalent to `If Not a Is b`.</span></span>  
  
### <a name="comparing-object-type"></a><span data-ttu-id="4cca3-166">Porównywanie typu obiektu</span><span class="sxs-lookup"><span data-stu-id="4cca3-166">Comparing Object Type</span></span>  

 <span data-ttu-id="4cca3-167">Można sprawdzić, czy obiekt jest określonego typu z `TypeOf` wyrażeniem.... `Is`</span><span class="sxs-lookup"><span data-stu-id="4cca3-167">You can test whether an object is of a particular type with the `TypeOf`...`Is` expression.</span></span> <span data-ttu-id="4cca3-168">Składnia wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="4cca3-168">The syntax is as follows:</span></span>  
  
 `TypeOf <objectexpression> Is <typename>`  
  
 <span data-ttu-id="4cca3-169">Gdy `typename` określa typ interfejsu, `TypeOf` wyrażenie... `Is` zwraca wartość, `True` Jeśli obiekt implementuje typ interfejsu.</span><span class="sxs-lookup"><span data-stu-id="4cca3-169">When `typename` specifies an interface type, then the `TypeOf`...`Is` expression returns `True` if the object implements the interface type.</span></span> <span data-ttu-id="4cca3-170">Gdy `typename` jest typem klasy, wyrażenie zwraca, `True` Jeśli obiekt jest wystąpieniem określonej klasy lub klasy, która pochodzi od określonej klasy.</span><span class="sxs-lookup"><span data-stu-id="4cca3-170">When `typename` is a class type, then the expression returns `True` if the object is an instance of the specified class or of a class that derives from the specified class.</span></span> <span data-ttu-id="4cca3-171">Ilustruje to poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="4cca3-171">The following example illustrates this.</span></span>  
  
 [!code-vb[VbVbalrOperators#68](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#68)]  
  
 <span data-ttu-id="4cca3-172">W poprzednim przykładzie `TypeOf x Is Control` wyrażenie szacuje się `True` `x` , że jest typem `Button` , który dziedziczy z `Control` .</span><span class="sxs-lookup"><span data-stu-id="4cca3-172">In the preceding example, the `TypeOf x Is Control` expression evaluates to `True` because the type of `x` is `Button`, which inherits from `Control`.</span></span>  
  
 <span data-ttu-id="4cca3-173">Aby uzyskać więcej informacji, zobacz [operator typeof](../../../language-reference/operators/typeof-operator.md).</span><span class="sxs-lookup"><span data-stu-id="4cca3-173">For more information, see [TypeOf Operator](../../../language-reference/operators/typeof-operator.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="4cca3-174">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="4cca3-174">See also</span></span>

- [<span data-ttu-id="4cca3-175">Porównania wartości</span><span class="sxs-lookup"><span data-stu-id="4cca3-175">Value Comparisons</span></span>](value-comparisons.md)
- [<span data-ttu-id="4cca3-176">Operatory porównania</span><span class="sxs-lookup"><span data-stu-id="4cca3-176">Comparison Operators</span></span>](../../../language-reference/operators/comparison-operators.md)
- [<span data-ttu-id="4cca3-177">Operatory</span><span class="sxs-lookup"><span data-stu-id="4cca3-177">Operators</span></span>](../../../language-reference/operators/index.md)
- [<span data-ttu-id="4cca3-178">Operatory arytmetyczne w Visual Basic</span><span class="sxs-lookup"><span data-stu-id="4cca3-178">Arithmetic Operators in Visual Basic</span></span>](arithmetic-operators.md)
- [<span data-ttu-id="4cca3-179">Operatory łączenia w Visual Basic</span><span class="sxs-lookup"><span data-stu-id="4cca3-179">Concatenation Operators in Visual Basic</span></span>](concatenation-operators.md)
- [<span data-ttu-id="4cca3-180">Operatory logiczne i bitowe w Visual Basic</span><span class="sxs-lookup"><span data-stu-id="4cca3-180">Logical and Bitwise Operators in Visual Basic</span></span>](logical-and-bitwise-operators.md)
