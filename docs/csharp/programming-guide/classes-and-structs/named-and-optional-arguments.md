---
title: Argumenty nazwane i opcjonalne — Przewodnik programowania w języku C#
description: Nazwane argumenty w języku C# określają argumenty według nazwy, a nie do położenia. Opcjonalne argumenty można pominąć.
ms.date: 09/25/2020
ms.custom: contperf-fy21q1
f1_keywords:
- namedParameter_CSharpKeyword
- cs_namedParameter
helpviewer_keywords:
- parameters [C#], named
- named arguments [C#]
- arguments [C#], named
- optional arguments [C#]
- arguments [C#], optional
- parameters [C#], optional
- named and optional arguments [C#]
ms.assetid: 839c960c-c2dc-4d05-af4d-ca5428e54008
ms.openlocfilehash: bb79d956124a610bac0de6825c1f42655789e98d
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2020
ms.locfileid: "97513110"
---
# <a name="named-and-optional-arguments-c-programming-guide"></a><span data-ttu-id="a79f2-104">Argumenty nazwane i opcjonalne (Przewodnik programowania w języku C#)</span><span class="sxs-lookup"><span data-stu-id="a79f2-104">Named and Optional Arguments (C# Programming Guide)</span></span>

<span data-ttu-id="a79f2-105">W języku C# 4 wprowadzono argumenty nazwane i opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="a79f2-105">C# 4 introduces named and optional arguments.</span></span> <span data-ttu-id="a79f2-106">*Nazwane argumenty* umożliwiają określenie argumentu dla parametru przez dopasowanie argumentu do jego nazwy, a nie do pozycji na liście parametrów.</span><span class="sxs-lookup"><span data-stu-id="a79f2-106">*Named arguments* enable you to specify an argument for a parameter by matching the argument with its name rather than with its position in the parameter list.</span></span> <span data-ttu-id="a79f2-107">*Argumenty opcjonalne* umożliwiają pominięcie argumentów dla niektórych parametrów.</span><span class="sxs-lookup"><span data-stu-id="a79f2-107">*Optional arguments* enable you to omit arguments for some parameters.</span></span> <span data-ttu-id="a79f2-108">Obie techniki mogą być używane z metodami, indeksatorami, konstruktorami i delegatami.</span><span class="sxs-lookup"><span data-stu-id="a79f2-108">Both techniques can be used with methods, indexers, constructors, and delegates.</span></span>

<span data-ttu-id="a79f2-109">W przypadku używania argumentów nazwanych i opcjonalnych argumenty są oceniane w kolejności, w jakiej są wyświetlane na liście argumentów, a nie na liście parametrów.</span><span class="sxs-lookup"><span data-stu-id="a79f2-109">When you use named and optional arguments, the arguments are evaluated in the order in which they appear in the argument list, not the parameter list.</span></span>

<span data-ttu-id="a79f2-110">Parametry nazwane i opcjonalne umożliwiają podawanie argumentów dla wybranych parametrów.</span><span class="sxs-lookup"><span data-stu-id="a79f2-110">Named and optional parameters enable you to supply arguments for selected parameters.</span></span> <span data-ttu-id="a79f2-111">Ta funkcja znacznie upraszcza wywołania interfejsów COM, takich jak interfejsy API automatyzacji Microsoft Office.</span><span class="sxs-lookup"><span data-stu-id="a79f2-111">This capability greatly eases calls to COM interfaces such as the Microsoft Office Automation APIs.</span></span>

## <a name="named-arguments"></a><span data-ttu-id="a79f2-112">Nazwane argumenty</span><span class="sxs-lookup"><span data-stu-id="a79f2-112">Named Arguments</span></span>

<span data-ttu-id="a79f2-113">Nazwane argumenty są bezpłatne od dopasowania do kolejności parametrów na listach parametrów wywoływanych metod.</span><span class="sxs-lookup"><span data-stu-id="a79f2-113">Named arguments free you from matching the order of parameters in the parameter lists of called methods.</span></span> <span data-ttu-id="a79f2-114">Parametr dla każdego argumentu można określić za pomocą nazwy parametru.</span><span class="sxs-lookup"><span data-stu-id="a79f2-114">The parameter for each argument can be specified by parameter name.</span></span> <span data-ttu-id="a79f2-115">Na przykład funkcja, która drukuje szczegóły zamówienia (takie jak nazwa sprzedawcy, numer zamówienia & Nazwa produktu), może być wywoływana przez wysłanie argumentów według pozycji w kolejności zdefiniowanej przez funkcję.</span><span class="sxs-lookup"><span data-stu-id="a79f2-115">For example, a function that prints order details (such as, seller name, order number & product name) can be called by sending arguments by position, in the order defined by the function.</span></span>

```csharp
PrintOrderDetails("Gift Shop", 31, "Red Mug");
```

<span data-ttu-id="a79f2-116">Jeśli nie pamiętasz kolejności parametrów, ale znasz ich nazwy, możesz wysłać argumenty w dowolnej kolejności.</span><span class="sxs-lookup"><span data-stu-id="a79f2-116">If you don't remember the order of the parameters but know their names, you can send the arguments in any order.</span></span>

```csharp
PrintOrderDetails(orderNum: 31, productName: "Red Mug", sellerName: "Gift Shop");
PrintOrderDetails(productName: "Red Mug", sellerName: "Gift Shop", orderNum: 31);
```

<span data-ttu-id="a79f2-117">Argumenty nazwane również zwiększają czytelność kodu przez zidentyfikowanie, co reprezentuje każdy argument.</span><span class="sxs-lookup"><span data-stu-id="a79f2-117">Named arguments also improve the readability of your code by identifying what each argument represents.</span></span> <span data-ttu-id="a79f2-118">W poniższym przykładzie metoda `sellerName` nie może mieć wartości null ani być białym znakiem.</span><span class="sxs-lookup"><span data-stu-id="a79f2-118">In the example method below, the `sellerName` can't be null or white space.</span></span> <span data-ttu-id="a79f2-119">Zarówno, jak `sellerName` i `productName` są typami ciągów, zamiast wysyłać argumenty według położenia, warto użyć nazwanych argumentów, aby odróżnić dwa i zmniejszyć liczbę pomyłek dla każdego odczytu kodu.</span><span class="sxs-lookup"><span data-stu-id="a79f2-119">As both `sellerName` and `productName` are string types, instead of sending arguments by position, it makes sense to use named arguments to disambiguate the two and reduce confusion for anyone reading the code.</span></span>
  
<span data-ttu-id="a79f2-120">Argumenty nazwane, gdy są używane z argumentami pozycyjnymi, są prawidłowe tak długo, jak</span><span class="sxs-lookup"><span data-stu-id="a79f2-120">Named arguments, when used with positional arguments, are valid as long as</span></span>

- <span data-ttu-id="a79f2-121">nie są one następują żadnych argumentów pozycyjnych lub</span><span class="sxs-lookup"><span data-stu-id="a79f2-121">they're not followed by any positional arguments, or</span></span>

    ```csharp
    PrintOrderDetails("Gift Shop", 31, productName: "Red Mug");
    ```

- <span data-ttu-id="a79f2-122">_począwszy od języka C# 7,2_, są one używane w poprawnej pozycji.</span><span class="sxs-lookup"><span data-stu-id="a79f2-122">_starting with C# 7.2_, they're used in the correct position.</span></span> <span data-ttu-id="a79f2-123">W poniższym przykładzie parametr `orderNum` znajduje się w poprawnej pozycji, ale nie jest jawnie nazwany.</span><span class="sxs-lookup"><span data-stu-id="a79f2-123">In the example below, the parameter `orderNum` is in the correct position but isn't explicitly named.</span></span>

    ```csharp
    PrintOrderDetails(sellerName: "Gift Shop", 31, productName: "Red Mug");
    ```

<span data-ttu-id="a79f2-124">Argumenty pozycyjne, które są zgodne z argumentami nazwanymi poza kolejnością, są nieprawidłowe.</span><span class="sxs-lookup"><span data-stu-id="a79f2-124">Positional arguments that follow any out-of-order named arguments are invalid.</span></span>

```csharp
// This generates CS1738: Named argument specifications must appear after all fixed arguments have been specified.
PrintOrderDetails(productName: "Red Mug", 31, "Gift Shop");
```

## <a name="example"></a><span data-ttu-id="a79f2-125">Przykład</span><span class="sxs-lookup"><span data-stu-id="a79f2-125">Example</span></span>

<span data-ttu-id="a79f2-126">Poniższy kod implementuje przykłady z tej sekcji wraz z dodatkowymi.</span><span class="sxs-lookup"><span data-stu-id="a79f2-126">The following code implements the examples from this section along with some additional ones.</span></span>  

[!code-csharp[csProgGuideNamedAndOptional#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguidenamedandoptional/cs/program.cs#1)]

## <a name="optional-arguments"></a><span data-ttu-id="a79f2-127">Argumenty opcjonalne</span><span class="sxs-lookup"><span data-stu-id="a79f2-127">Optional Arguments</span></span>

<span data-ttu-id="a79f2-128">Definicja metody, konstruktora, indeksatora lub delegata może określać, że jej parametry są wymagane lub opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="a79f2-128">The definition of a method, constructor, indexer, or delegate can specify its parameters are required or optional.</span></span> <span data-ttu-id="a79f2-129">Każde wywołanie musi udostępniać argumenty dla wszystkich wymaganych parametrów, ale może pominąć argumenty dla parametrów opcjonalnych.</span><span class="sxs-lookup"><span data-stu-id="a79f2-129">Any call must provide arguments for all required parameters, but can omit arguments for optional parameters.</span></span>

<span data-ttu-id="a79f2-130">Każdy opcjonalny parametr ma wartość domyślną w ramach swojej definicji.</span><span class="sxs-lookup"><span data-stu-id="a79f2-130">Each optional parameter has a default value as part of its definition.</span></span> <span data-ttu-id="a79f2-131">Jeśli żaden argument nie jest wysyłany dla tego parametru, zostanie użyta wartość domyślna.</span><span class="sxs-lookup"><span data-stu-id="a79f2-131">If no argument is sent for that parameter, the default value is used.</span></span> <span data-ttu-id="a79f2-132">Wartość domyślna musi być jednym z następujących typów wyrażeń:</span><span class="sxs-lookup"><span data-stu-id="a79f2-132">A default value must be one of the following types of expressions:</span></span>
  
- <span data-ttu-id="a79f2-133">wyrażenie stałe;</span><span class="sxs-lookup"><span data-stu-id="a79f2-133">a constant expression;</span></span>  
- <span data-ttu-id="a79f2-134">wyrażenie formularza `new ValType()` , gdzie `ValType` jest typem wartości, na przykład [wyliczeniem](../../language-reference/builtin-types/enum.md) lub [strukturą](../../language-reference/builtin-types/struct.md);</span><span class="sxs-lookup"><span data-stu-id="a79f2-134">an expression of the form `new ValType()`, where `ValType` is a value type, such as an [enum](../../language-reference/builtin-types/enum.md) or a [struct](../../language-reference/builtin-types/struct.md);</span></span>
- <span data-ttu-id="a79f2-135">wyrażenie [domyślne (ValType)](../../language-reference/operators/default.md), gdzie `ValType` jest typem wartości.</span><span class="sxs-lookup"><span data-stu-id="a79f2-135">an expression of the form [default(ValType)](../../language-reference/operators/default.md),  where `ValType` is a value type.</span></span>

<span data-ttu-id="a79f2-136">Parametry opcjonalne są definiowane na końcu listy parametrów po dowolnych wymaganych parametrach.</span><span class="sxs-lookup"><span data-stu-id="a79f2-136">Optional parameters are defined at the end of the parameter list, after any required parameters.</span></span> <span data-ttu-id="a79f2-137">Jeśli obiekt wywołujący zawiera argument dla dowolnego z parametrów opcjonalnych, musi podać argumenty dla wszystkich poprzedzających parametry opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="a79f2-137">If the caller provides an argument for any one of a succession of optional parameters, it must provide arguments for all preceding optional parameters.</span></span> <span data-ttu-id="a79f2-138">Luki rozdzielane przecinkami na liście argumentów nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="a79f2-138">Comma-separated gaps in the argument list aren't supported.</span></span> <span data-ttu-id="a79f2-139">Na przykład, w poniższym kodzie metoda wystąpienia `ExampleMethod` jest zdefiniowana z jednym wymaganym i dwoma opcjonalnymi parametrami.</span><span class="sxs-lookup"><span data-stu-id="a79f2-139">For example, in the following code, instance method `ExampleMethod` is defined with one required and two optional parameters.</span></span>

[!code-csharp[csProgGuideNamedAndOptional#15](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguidenamedandoptional/cs/optional.cs#15)]

<span data-ttu-id="a79f2-140">Następujące wywołanie `ExampleMethod` powoduje wystąpienie błędu kompilatora, ponieważ argument jest dostarczany dla trzeciego parametru, ale nie w drugim.</span><span class="sxs-lookup"><span data-stu-id="a79f2-140">The following call to `ExampleMethod` causes a compiler error, because an argument is provided for the third parameter but not for the second.</span></span>

```csharp
//anExample.ExampleMethod(3, ,4);
```

<span data-ttu-id="a79f2-141">Jeśli jednak znasz nazwę trzeciego parametru, możesz użyć argumentu nazwanego do wykonania zadania.</span><span class="sxs-lookup"><span data-stu-id="a79f2-141">However, if you know the name of the third parameter, you can use a named argument to accomplish the task.</span></span>

```csharp
anExample.ExampleMethod(3, optionalint: 4);
```

<span data-ttu-id="a79f2-142">Funkcja IntelliSense używa nawiasów, aby wskazać parametry opcjonalne, jak pokazano na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="a79f2-142">IntelliSense uses brackets to indicate optional parameters, as shown in the following illustration:</span></span>

![Zrzut ekranu przedstawiający funkcję IntelliSense Quick info dla metody ExampleMethod.](./media/named-and-optional-arguments/optional-examplemethod-parameters.png)

> [!NOTE]
> <span data-ttu-id="a79f2-144">Można również zadeklarować parametry opcjonalne przy użyciu klasy .NET <xref:System.Runtime.InteropServices.OptionalAttribute> .</span><span class="sxs-lookup"><span data-stu-id="a79f2-144">You can also declare optional parameters by using the .NET <xref:System.Runtime.InteropServices.OptionalAttribute> class.</span></span> <span data-ttu-id="a79f2-145">`OptionalAttribute` parametry nie wymagają wartości domyślnej.</span><span class="sxs-lookup"><span data-stu-id="a79f2-145">`OptionalAttribute` parameters do not require a default value.</span></span>

## <a name="example"></a><span data-ttu-id="a79f2-146">Przykład</span><span class="sxs-lookup"><span data-stu-id="a79f2-146">Example</span></span>

<span data-ttu-id="a79f2-147">W poniższym przykładzie Konstruktor dla `ExampleClass` ma jeden parametr, który jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="a79f2-147">In the following example, the constructor for `ExampleClass` has one parameter, which is optional.</span></span> <span data-ttu-id="a79f2-148">Metoda wystąpienia `ExampleMethod` ma jeden wymagany parametr, `required` i dwa parametry opcjonalne `optionalstr` oraz `optionalint` .</span><span class="sxs-lookup"><span data-stu-id="a79f2-148">Instance method `ExampleMethod` has one required parameter, `required`, and two optional parameters, `optionalstr` and `optionalint`.</span></span> <span data-ttu-id="a79f2-149">Kod w `Main` pokazuje różne sposoby wywoływania konstruktora i metody.</span><span class="sxs-lookup"><span data-stu-id="a79f2-149">The code in `Main` shows the different ways in which the constructor and method can be invoked.</span></span>

[!code-csharp[csProgGuideNamedAndOptional#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguidenamedandoptional/cs/optional.cs#2)]

<span data-ttu-id="a79f2-150">Poprzedni kod pokazuje kilka przykładów, w których parametry opcjonalne nie są poprawnie stosowane.</span><span class="sxs-lookup"><span data-stu-id="a79f2-150">The preceding code shows a number of examples where optional parameters aren't applied correctly.</span></span> <span data-ttu-id="a79f2-151">Pierwszy ilustruje, że argument musi być podany dla pierwszego parametru, który jest wymagany.</span><span class="sxs-lookup"><span data-stu-id="a79f2-151">The first illustrates that an argument must be supplied for the first parameter, which is required.</span></span>
  
## <a name="com-interfaces"></a><span data-ttu-id="a79f2-152">Interfejsy COM</span><span class="sxs-lookup"><span data-stu-id="a79f2-152">COM Interfaces</span></span>

<span data-ttu-id="a79f2-153">Argumenty nazwane i opcjonalne wraz z obsługą obiektów dynamicznych znacznie zwiększają współdziałanie z interfejsami API modelu COM, takimi jak interfejsy API usługi Office Automation.</span><span class="sxs-lookup"><span data-stu-id="a79f2-153">Named and optional arguments, along with support for dynamic objects, greatly improve interoperability with COM APIs, such as Office Automation APIs.</span></span>

<span data-ttu-id="a79f2-154">Na przykład <xref:Microsoft.Office.Interop.Excel.Range.AutoFormat%2A> Metoda w interfejsie programu Excel Microsoft Office <xref:Microsoft.Office.Interop.Excel.Range> ma siedem parametrów, z których wszystkie są opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="a79f2-154">For example, the <xref:Microsoft.Office.Interop.Excel.Range.AutoFormat%2A> method in the Microsoft Office Excel <xref:Microsoft.Office.Interop.Excel.Range> interface has seven parameters, all of which are optional.</span></span> <span data-ttu-id="a79f2-155">Te parametry przedstawiono na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="a79f2-155">These parameters are shown in the following illustration:</span></span>

![Zrzut ekranu przedstawiający funkcję IntelliSense Quick info dla metody Autoformatowania.](./media/named-and-optional-arguments/autoformat-method-parameters.png)

<span data-ttu-id="a79f2-157">W języku C# 3,0 i wcześniejszych wersjach argument jest wymagany dla każdego parametru, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="a79f2-157">In C# 3.0 and earlier versions, an argument is required for each parameter, as shown in the following example.</span></span>

[!code-csharp[csProgGuideNamedAndOptional#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguidenamedandoptional/cs/namedandoptcom.cs#3)]

<span data-ttu-id="a79f2-158">Można jednak znacznie uprościć wywołanie do `AutoFormat` za pomocą argumentów nazwanych i opcjonalnych wprowadzonych w języku C# 4,0.</span><span class="sxs-lookup"><span data-stu-id="a79f2-158">However, you can greatly simplify the call to `AutoFormat` by using named and optional arguments, introduced in C# 4.0.</span></span> <span data-ttu-id="a79f2-159">Argumenty nazwane i opcjonalne umożliwiają pominięcie argumentu dla opcjonalnego parametru, jeśli nie chcesz zmieniać wartości domyślnej parametru.</span><span class="sxs-lookup"><span data-stu-id="a79f2-159">Named and optional arguments enable you to omit the argument for an optional parameter if you don't want to change the parameter's default value.</span></span> <span data-ttu-id="a79f2-160">W poniższym wywołaniu wartość jest określona tylko dla jednego z siedmiu parametrów.</span><span class="sxs-lookup"><span data-stu-id="a79f2-160">In the following call, a value is specified for only one of the seven parameters.</span></span>

[!code-csharp[csProgGuideNamedAndOptional#13](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguidenamedandoptional/cs/namedandoptcom.cs#13)]

<span data-ttu-id="a79f2-161">Aby uzyskać więcej informacji i przykładów, zobacz [jak używać argumentów nazwanych i opcjonalnych w programowaniu pakietu Office](./how-to-use-named-and-optional-arguments-in-office-programming.md) oraz [jak uzyskiwać dostęp do obiektów międzyoperacyjności pakietu Office za pomocą funkcji języka C#](../interop/how-to-access-office-onterop-objects.md).</span><span class="sxs-lookup"><span data-stu-id="a79f2-161">For more information and examples, see [How to use named and optional arguments in Office programming](./how-to-use-named-and-optional-arguments-in-office-programming.md) and [How to access Office interop objects by using C# features](../interop/how-to-access-office-onterop-objects.md).</span></span>
  
## <a name="overload-resolution"></a><span data-ttu-id="a79f2-162">Rozpoznanie przeciążenia</span><span class="sxs-lookup"><span data-stu-id="a79f2-162">Overload Resolution</span></span>

<span data-ttu-id="a79f2-163">Użycie argumentów nazwanych i opcjonalnych wpływa na rozpoznawanie przeciążenia w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a79f2-163">Use of named and optional arguments affects overload resolution in the following ways:</span></span>

- <span data-ttu-id="a79f2-164">Metoda, indeksator lub Konstruktor jest kandydatem do wykonania, jeśli każdy z jego parametrów jest opcjonalny lub odpowiada według nazwy lub według pozycji, do pojedynczego argumentu w instrukcji wywołującej i ten argument można przekonwertować na typ parametru.</span><span class="sxs-lookup"><span data-stu-id="a79f2-164">A method, indexer, or constructor is a candidate for execution if each of its parameters either is optional or corresponds, by name or by position, to a single argument in the calling statement, and that argument can be converted to the type of the parameter.</span></span>  
- <span data-ttu-id="a79f2-165">W przypadku znalezienia więcej niż jednego kandydata reguły rozpoznawania przeciążenia dla preferowanych konwersji są stosowane do argumentów, które są jawnie określone.</span><span class="sxs-lookup"><span data-stu-id="a79f2-165">If more than one candidate is found, overload resolution rules for preferred conversions are applied to the arguments that are explicitly specified.</span></span> <span data-ttu-id="a79f2-166">Pominięte argumenty dla parametrów opcjonalnych są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="a79f2-166">Omitted arguments for optional parameters are ignored.</span></span>
- <span data-ttu-id="a79f2-167">Jeśli dwie kandydaci są uznawane za równie dobre, preferencja przechodzi do kandydata, który nie ma parametrów opcjonalnych, dla których argumenty zostały pominięte w wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="a79f2-167">If two candidates are judged to be equally good, preference goes to a candidate that doesn't have optional parameters for which arguments were omitted in the call.</span></span> <span data-ttu-id="a79f2-168">Rozpoznanie przeciążenia zazwyczaj preferuje kandydatów, które mają mniej parametrów.</span><span class="sxs-lookup"><span data-stu-id="a79f2-168">Overload resolution generally prefers candidates that have fewer parameters.</span></span>
  
## <a name="c-language-specification"></a><span data-ttu-id="a79f2-169">Specyfikacja języka C#</span><span class="sxs-lookup"><span data-stu-id="a79f2-169">C# Language Specification</span></span>

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]
