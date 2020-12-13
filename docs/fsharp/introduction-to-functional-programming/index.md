---
title: Wprowadzenie do programowania funkcyjnego w F#
description: 'Poznaj podstawy programowania funkcjonalnego w języku F #.'
ms.date: 10/29/2018
ms.openlocfilehash: 44242a4319a331312a003a555d1483f2a3f1a90d
ms.sourcegitcommit: 9b877e160c326577e8aa5ead22a937110d80fa44
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2020
ms.locfileid: "97110588"
---
# <a name="introduction-to-functional-programming-in-f"></a><span data-ttu-id="7a9ec-103">Wprowadzenie do programowania funkcjonalnego w języku F\#</span><span class="sxs-lookup"><span data-stu-id="7a9ec-103">Introduction to Functional Programming in F\#</span></span>

<span data-ttu-id="7a9ec-104">Programowanie funkcjonalne to styl programowania, który kładzie nacisk na korzystanie z funkcji i niezmienne dane.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-104">Functional programming is a style of programming that emphasizes the use of functions and immutable data.</span></span> <span data-ttu-id="7a9ec-105">Programistyczne programowanie funkcjonalne jest połączone z typami statycznymi, na przykład w języku F #.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-105">Typed functional programming is when functional programming is combined with static types, such as with F#.</span></span> <span data-ttu-id="7a9ec-106">Ogólnie rzecz biorąc, następujące koncepcje zostały wyróżnione w programowaniu funkcjonalnym:</span><span class="sxs-lookup"><span data-stu-id="7a9ec-106">In general, the following concepts are emphasized in functional programming:</span></span>

* <span data-ttu-id="7a9ec-107">Działa jako konstrukcje podstawowe, z których korzystasz</span><span class="sxs-lookup"><span data-stu-id="7a9ec-107">Functions as the primary constructs you use</span></span>
* <span data-ttu-id="7a9ec-108">Wyrażenia zamiast instrukcji</span><span class="sxs-lookup"><span data-stu-id="7a9ec-108">Expressions instead of statements</span></span>
* <span data-ttu-id="7a9ec-109">Niezmienne wartości w zmiennych</span><span class="sxs-lookup"><span data-stu-id="7a9ec-109">Immutable values over variables</span></span>
* <span data-ttu-id="7a9ec-110">Programowanie deklaratywne nad bezwzględnym programowaniem</span><span class="sxs-lookup"><span data-stu-id="7a9ec-110">Declarative programming over imperative programming</span></span>

<span data-ttu-id="7a9ec-111">W tej serii zapoznajesz koncepcje i wzorce w programowaniu funkcjonalnym przy użyciu języka F #.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-111">Throughout this series, you'll explore concepts and patterns in functional programming using F#.</span></span> <span data-ttu-id="7a9ec-112">W ten sposób dowiesz się, że tylko niektóre F #.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-112">Along the way, you'll learn some F# too.</span></span>

## <a name="terminology"></a><span data-ttu-id="7a9ec-113">Terminologia</span><span class="sxs-lookup"><span data-stu-id="7a9ec-113">Terminology</span></span>

<span data-ttu-id="7a9ec-114">Programowanie funkcjonalne, takie jak inne odmiany programistyczne, zawiera słownictwo, które trzeba poznać.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-114">Functional programming, like other programming paradigms, comes with a vocabulary that you will eventually need to learn.</span></span> <span data-ttu-id="7a9ec-115">Poniżej przedstawiono niektóre typowe terminy, w których zobaczysz cały czas:</span><span class="sxs-lookup"><span data-stu-id="7a9ec-115">Here are some common terms you'll see all of the time:</span></span>

* <span data-ttu-id="7a9ec-116">**Function** -a funkcja jest konstrukcja, która spowoduje wygenerowanie danych wyjściowych po otrzymaniu danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-116">**Function** - A function is a construct that will produce an output when given an input.</span></span> <span data-ttu-id="7a9ec-117">Bardziej formalnie _mapuje_ element z jednego zestawu na inny.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-117">More formally, it _maps_ an item from one set to another set.</span></span> <span data-ttu-id="7a9ec-118">Ta formalność jest przekształcana w konkretną na wiele sposobów, szczególnie w przypadku korzystania z funkcji, które działają na kolekcjach danych.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-118">This formalism is lifted into the concrete in many ways, especially when using functions that operate on collections of data.</span></span> <span data-ttu-id="7a9ec-119">Jest to najbardziej podstawowe (i ważne) koncepcje programowania funkcjonalnego.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-119">It is the most basic (and important) concept in functional programming.</span></span>
* <span data-ttu-id="7a9ec-120">**Wyrażenie** -wyrażenie jest konstrukcja w kodzie, która tworzy wartość.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-120">**Expression** - An expression is a construct in code that produces a value.</span></span> <span data-ttu-id="7a9ec-121">W języku F # ta wartość musi być powiązana lub jawnie ignorowana.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-121">In F#, this value must be bound or explicitly ignored.</span></span> <span data-ttu-id="7a9ec-122">Wyrażenie może być nieuproszczone zamieniane przez wywołanie funkcji.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-122">An expression can be trivially replaced by a function call.</span></span>
* <span data-ttu-id="7a9ec-123">**Czystość** — czystość jest właściwością funkcji, w taki sposób, że jej wartość zwracana jest zawsze taka sama dla tych samych argumentów i że jej Ocena nie ma żadnych efektów ubocznych.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-123">**Purity** - Purity is a property of a function such that its return value is always the same for the same arguments, and that its evaluation has no side effects.</span></span> <span data-ttu-id="7a9ec-124">Czysta funkcja zależy wyłącznie od jej argumentów.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-124">A pure function depends entirely on its arguments.</span></span>
* <span data-ttu-id="7a9ec-125">**Przezroczystość referencyjna** — przezroczystość referencyjna jest właściwością wyrażeń, które mogą zostać zastąpione danymi wyjściowymi bez wpływania na zachowanie programu.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-125">**Referential Transparency** - Referential Transparency is a property of expressions such that they can be replaced with their output without affecting a program's behavior.</span></span>
* <span data-ttu-id="7a9ec-126">**Niezmienności** -niezmienności oznacza, że wartości nie można zmienić w miejscu.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-126">**Immutability** - Immutability means that a value cannot be changed in-place.</span></span> <span data-ttu-id="7a9ec-127">Jest to w przeciwieństwie do zmiennych, które mogą ulec zmianie w miejscu.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-127">This is in contrast with variables, which can change in place.</span></span>

## <a name="examples"></a><span data-ttu-id="7a9ec-128">Przykłady</span><span class="sxs-lookup"><span data-stu-id="7a9ec-128">Examples</span></span>

<span data-ttu-id="7a9ec-129">W poniższych przykładach przedstawiono podstawowe pojęcia.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-129">The following examples demonstrate these core concepts.</span></span>

### <a name="functions"></a><span data-ttu-id="7a9ec-130">Funkcje</span><span class="sxs-lookup"><span data-stu-id="7a9ec-130">Functions</span></span>

<span data-ttu-id="7a9ec-131">Najbardziej typową i podstawową konstrukcją w programowaniu funkcjonalnym jest funkcja.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-131">The most common and fundamental construct in functional programming is the function.</span></span> <span data-ttu-id="7a9ec-132">Oto prosta funkcja, która dodaje 1 do liczby całkowitej:</span><span class="sxs-lookup"><span data-stu-id="7a9ec-132">Here's a simple function that adds 1 to an integer:</span></span>

```fsharp
let addOne x = x + 1
```

<span data-ttu-id="7a9ec-133">Podpis typu jest następujący:</span><span class="sxs-lookup"><span data-stu-id="7a9ec-133">Its type signature is as follows:</span></span>

```fsharp
val addOne: x:int -> int
```

<span data-ttu-id="7a9ec-134">Podpis może być odczytywany jako, " `addOne` akceptuje `int` nazwane `x` i spowoduje utworzenie `int` ".</span><span class="sxs-lookup"><span data-stu-id="7a9ec-134">The signature can be read as, "`addOne` accepts an `int` named `x` and will produce an `int`".</span></span> <span data-ttu-id="7a9ec-135">Bardziej formalnie `addOne` _mapuje_ wartość z zestawu liczb całkowitych na zestaw liczb całkowitych.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-135">More formally, `addOne` is _mapping_ a value from the set of integers to the set of integers.</span></span> <span data-ttu-id="7a9ec-136">`->`Token oznacza to mapowanie.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-136">The `->` token signifies this mapping.</span></span> <span data-ttu-id="7a9ec-137">W języku F # zwykle można przyjrzeć się sygnatury funkcji w celu uzyskania sensu, co robi.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-137">In F#, you can usually look at the function signature to get a sense for what it does.</span></span>

<span data-ttu-id="7a9ec-138">Dlatego dlaczego sygnatura jest ważna?</span><span class="sxs-lookup"><span data-stu-id="7a9ec-138">So, why is the signature important?</span></span> <span data-ttu-id="7a9ec-139">W przypadku programowania w określonym zakresie implementacja funkcji jest często mniej ważna niż faktyczny podpis typu!</span><span class="sxs-lookup"><span data-stu-id="7a9ec-139">In typed functional programming, the implementation of a function is often less important than the actual type signature!</span></span> <span data-ttu-id="7a9ec-140">Fakt, że `addOne` wartość 1 jest dodawana do liczby całkowitej, jest interesujący w czasie wykonywania, ale podczas konstruowania programu, fakt, że akceptuje, i zwraca wartość, co informuje, `int` jak faktycznie będzie używać tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-140">The fact that `addOne` adds the value 1 to an integer is interesting at runtime, but when you are constructing a program, the fact that it accepts and returns an `int` is what informs how you will actually use this function.</span></span> <span data-ttu-id="7a9ec-141">Ponadto po poprawnym użyciu tej funkcji (w odniesieniu do podpisu typu) diagnozowanie wszelkich problemów może odbywać się tylko w treści `addOne` funkcji.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-141">Furthermore, once you use this function correctly (with respect to its type signature), diagnosing any problems can be done only within the body of the `addOne` function.</span></span> <span data-ttu-id="7a9ec-142">Jest to tempo związane z programowaniem funkcjonalności w określonym typie.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-142">This is the impetus behind typed functional programming.</span></span>

### <a name="expressions"></a><span data-ttu-id="7a9ec-143">Wyrażenia</span><span class="sxs-lookup"><span data-stu-id="7a9ec-143">Expressions</span></span>

<span data-ttu-id="7a9ec-144">Wyrażenia są konstrukcjami, które są szacowane do wartości.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-144">Expressions are constructs that evaluate to a value.</span></span> <span data-ttu-id="7a9ec-145">W przeciwieństwie do instrukcji, które wykonują akcję, wyrażenia mogą być uważane za wykonywanie akcji, która zwraca wartość.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-145">In contrast to statements, which perform an action, expressions can be thought of performing an action that gives back a value.</span></span> <span data-ttu-id="7a9ec-146">Wyrażenia są prawie zawsze używane w programowaniu funkcjonalnym zamiast instrukcji.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-146">Expressions are almost always used in functional programming instead of statements.</span></span>

<span data-ttu-id="7a9ec-147">Weź pod uwagę poprzednią funkcję, `addOne` .</span><span class="sxs-lookup"><span data-stu-id="7a9ec-147">Consider the previous function, `addOne`.</span></span> <span data-ttu-id="7a9ec-148">Treść `addOne` jest wyrażeniem:</span><span class="sxs-lookup"><span data-stu-id="7a9ec-148">The body of `addOne` is an expression:</span></span>

```fsharp
// 'x + 1' is an expression!
let addOne x = x + 1
```

<span data-ttu-id="7a9ec-149">Jest to wynik tego wyrażenia, który definiuje typ wyniku `addOne` funkcji.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-149">It is the result of this expression that defines the result type of the `addOne` function.</span></span> <span data-ttu-id="7a9ec-150">Na przykład, wyrażenie, które powoduje, że ta funkcja może zostać zmieniony na inny typ, taki jak `string` :</span><span class="sxs-lookup"><span data-stu-id="7a9ec-150">For example, the expression that makes up this function could be changed to be a different type, such as a `string`:</span></span>

```fsharp
let addOne x = x.ToString() + "1"
```

<span data-ttu-id="7a9ec-151">Sygnatura funkcji jest teraz:</span><span class="sxs-lookup"><span data-stu-id="7a9ec-151">The signature of the function is now:</span></span>

```fsharp
val addOne: x:'a -> string
```

<span data-ttu-id="7a9ec-152">Ponieważ dowolny typ w języku F # może zostać `ToString()` wywołany, typ elementu `x` został utworzony jako generyczny (nazywany [automatycznym generalizacją](../language-reference/generics/automatic-generalization.md)), a wynikowy typ to `string` .</span><span class="sxs-lookup"><span data-stu-id="7a9ec-152">Since any type in F# can have `ToString()` called on it, the type of `x` has been made generic (called [Automatic Generalization](../language-reference/generics/automatic-generalization.md)), and the resultant type is a `string`.</span></span>

<span data-ttu-id="7a9ec-153">Wyrażenia nie są tylko treścią funkcji.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-153">Expressions are not just the bodies of functions.</span></span> <span data-ttu-id="7a9ec-154">Można utworzyć wyrażenia, które tworzą wartość używaną w innym miejscu.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-154">You can have expressions that produce a value you use elsewhere.</span></span> <span data-ttu-id="7a9ec-155">Typowy `if` :</span><span class="sxs-lookup"><span data-stu-id="7a9ec-155">A common one is `if`:</span></span>

```fsharp
// Checks if 'x' is odd by using the mod operator
let isOdd x = x % 2 <> 0

let addOneIfOdd input =
    let result =
        if isOdd input then
            input + 1
        else
            input

    result
```

<span data-ttu-id="7a9ec-156">`if`Wyrażenie generuje wartość o nazwie `result` .</span><span class="sxs-lookup"><span data-stu-id="7a9ec-156">The `if` expression produces a value called `result`.</span></span> <span data-ttu-id="7a9ec-157">Należy zauważyć, że można `result` całkowicie pominąć, wprowadzając `if` wyrażenie do treści `addOneIfOdd` funkcji.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-157">Note that you could omit `result` entirely, making the `if` expression the body of the `addOneIfOdd` function.</span></span> <span data-ttu-id="7a9ec-158">Kluczem do zapamiętania w przypadku wyrażeń jest utworzenie wartości.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-158">The key thing to remember about expressions is that they produce a value.</span></span>

<span data-ttu-id="7a9ec-159">Istnieje typ specjalny, `unit` który jest używany, gdy nie ma niczego do zwrócenia.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-159">There is a special type, `unit`, that is used when there is nothing to return.</span></span> <span data-ttu-id="7a9ec-160">Rozważmy na przykład tę prostą funkcję:</span><span class="sxs-lookup"><span data-stu-id="7a9ec-160">For example, consider this simple function:</span></span>

```fsharp
let printString (str: string) =
    printfn $"String is: {str}"
```

<span data-ttu-id="7a9ec-161">Podpis wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="7a9ec-161">The signature looks like this:</span></span>

```fsharp
val printString: str:string -> unit
```

<span data-ttu-id="7a9ec-162">`unit`Typ wskazuje, że nie jest zwracana wartość rzeczywista.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-162">The `unit` type indicates that there is no actual value being returned.</span></span> <span data-ttu-id="7a9ec-163">Jest to przydatne, gdy masz procedurę, która musi "do pracy" mimo braku wartości do zwrócenia w wyniku tej pracy.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-163">This is useful when you have a routine that must "do work" despite having no value to return as a result of that work.</span></span>

<span data-ttu-id="7a9ec-164">Jest to bardzo zróżnicowane dla bezwzględnego programowania, gdzie równoważna `if` konstrukcja jest instrukcją, a Tworzenie wartości jest często wykonywane z mutacją zmiennych.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-164">This is in sharp contrast to imperative programming, where the equivalent `if` construct is a statement, and producing values is often done with mutating variables.</span></span> <span data-ttu-id="7a9ec-165">Na przykład w języku C# kod może być zapisany w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="7a9ec-165">For example, in C#, the code might be written like this:</span></span>

```csharp
bool IsOdd(int x) => x % 2 != 0;

int AddOneIfOdd(int input)
{
    var result = input;

    if (IsOdd(input))
    {
        result = input + 1;
    }

    return result;
}
```

<span data-ttu-id="7a9ec-166">Warto zauważyć, że język C# i inne języki w stylu C obsługują [wyrażenie Trzyelementowy](../../csharp/language-reference/operators/conditional-operator.md), które umożliwia programowanie warunkowe oparte na wyrażeniach.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-166">It's worth noting that C# and other C-style languages do support the [ternary expression](../../csharp/language-reference/operators/conditional-operator.md), which allows for expression-based conditional programming.</span></span>

<span data-ttu-id="7a9ec-167">W programowaniu funkcjonalnym rzadko można przystąpić do wartości instrukcji.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-167">In functional programming, it is rare to mutate values with statements.</span></span> <span data-ttu-id="7a9ec-168">Chociaż niektóre języki funkcjonalne obsługują instrukcje i mutacje, nie jest powszechna możliwość używania tych koncepcji w programowaniu funkcjonalnym.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-168">Although some functional languages support statements and mutation, it is not common to use these concepts in functional programming.</span></span>

### <a name="pure-functions"></a><span data-ttu-id="7a9ec-169">Czyste funkcje</span><span class="sxs-lookup"><span data-stu-id="7a9ec-169">Pure functions</span></span>

<span data-ttu-id="7a9ec-170">Jak wspomniano wcześniej, czyste funkcje to funkcje, które:</span><span class="sxs-lookup"><span data-stu-id="7a9ec-170">As previously mentioned, pure functions are functions that:</span></span>

* <span data-ttu-id="7a9ec-171">Należy zawsze oszacować tę samą wartość dla tych samych danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-171">Always evaluate to the same value for the same input.</span></span>
* <span data-ttu-id="7a9ec-172">Nie ma żadnych efektów ubocznych.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-172">Have no side effects.</span></span>

<span data-ttu-id="7a9ec-173">Warto traktować funkcje matematyczne w tym kontekście.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-173">It is helpful to think of mathematical functions in this context.</span></span> <span data-ttu-id="7a9ec-174">W przypadku matematyki funkcje są zależne od ich argumentów i nie mają żadnych efektów ubocznych.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-174">In mathematics, functions depend only on their arguments and do not have any side effects.</span></span> <span data-ttu-id="7a9ec-175">W funkcji matematycznej `f(x) = x + 1` wartość jest `f(x)` zależna od wartości `x` .</span><span class="sxs-lookup"><span data-stu-id="7a9ec-175">In the mathematical function `f(x) = x + 1`, the value of `f(x)` depends only on the value of `x`.</span></span> <span data-ttu-id="7a9ec-176">Czyste funkcje w programowaniu funkcjonalnym są takie same.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-176">Pure functions in functional programming are the same way.</span></span>

<span data-ttu-id="7a9ec-177">Podczas pisania czystej funkcji, funkcja musi zależeć tylko od jej argumentów i nie wykonuje żadnej akcji, która skutkuje efektem ubocznym.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-177">When writing a pure function, the function must depend only on its arguments and not perform any action that results in a side effect.</span></span>

<span data-ttu-id="7a9ec-178">Oto przykład funkcji nieczystych, ponieważ zależy ona od globalnego, modyfikowalnego stanu:</span><span class="sxs-lookup"><span data-stu-id="7a9ec-178">Here is an example of a non-pure function because it depends on global, mutable state:</span></span>

```fsharp
let mutable value = 1

let addOneToValue x = x + value
```

<span data-ttu-id="7a9ec-179">`addOneToValue`Funkcja jest jasno nieczytelna, ponieważ `value` można ją zmienić w dowolnym momencie, aby miała inną wartość niż 1.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-179">The `addOneToValue` function is clearly impure, because `value` could be changed at any time to have a different value than 1.</span></span> <span data-ttu-id="7a9ec-180">Ten wzorzec w zależności od wartości globalnej należy unikać w programowaniu funkcjonalnym.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-180">This pattern of depending on a global value is to be avoided in functional programming.</span></span>

<span data-ttu-id="7a9ec-181">Oto inny przykład nieczystej funkcji, ponieważ wykonuje efekt uboczny:</span><span class="sxs-lookup"><span data-stu-id="7a9ec-181">Here is another example of a non-pure function, because it performs a side effect:</span></span>

```fsharp
let addOneToValue x =
    printfn $"x is %d{x}"
    x + 1
```

<span data-ttu-id="7a9ec-182">Chociaż ta funkcja nie jest zależna od wartości globalnej, zapisuje wartość `x` do danych wyjściowych programu.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-182">Although this function does not depend on a global value, it writes the value of `x` to the output of the program.</span></span> <span data-ttu-id="7a9ec-183">Chociaż nie ma żadnego niewłaściwego w tym celu, oznacza to, że funkcja nie jest czysta.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-183">Although there is nothing inherently wrong with doing this, it does mean that the function is not pure.</span></span> <span data-ttu-id="7a9ec-184">Jeśli inna część programu zależy od elementu zewnętrznego do programu, takiego jak bufor wyjściowy, wywołanie tej funkcji może mieć wpływ na tę inną część programu.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-184">If another part of your program depends on something external to the program, such as the output buffer, then calling this function can affect that other part of your program.</span></span>

<span data-ttu-id="7a9ec-185">Usunięcie `printfn` instrukcji powoduje, że funkcja ma charakter czysty:</span><span class="sxs-lookup"><span data-stu-id="7a9ec-185">Removing the `printfn` statement makes the function pure:</span></span>

```fsharp
let addOneToValue x = x + 1
```

<span data-ttu-id="7a9ec-186">Mimo że ta funkcja nie jest jeszcze _lepsza_ niż poprzednia wersja z `printfn` instrukcją, gwarantuje, że cała ta funkcja zwraca wartość.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-186">Although this function is not inherently _better_ than the previous version with the `printfn` statement, it does guarantee that all this function does is return a value.</span></span> <span data-ttu-id="7a9ec-187">Wywołanie tej funkcji dowolna liczba razy daje ten sam wynik: po prostu tworzy wartość.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-187">Calling this function any number of times produces the same result: it just produces a value.</span></span> <span data-ttu-id="7a9ec-188">Przewidywalność podaną przez czystość to coś wielu programistów.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-188">The predictability given by purity is something many functional programmers strive for.</span></span>

### <a name="immutability"></a><span data-ttu-id="7a9ec-189">Niezmienność</span><span class="sxs-lookup"><span data-stu-id="7a9ec-189">Immutability</span></span>

<span data-ttu-id="7a9ec-190">Na koniec jednym z najważniejszych koncepcji programowania funkcjonalnego z typem jest niezmienności.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-190">Finally, one of the most fundamental concepts of typed functional programming is immutability.</span></span> <span data-ttu-id="7a9ec-191">W języku F # wszystkie wartości są domyślnie niezmienne.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-191">In F#, all values are immutable by default.</span></span> <span data-ttu-id="7a9ec-192">Oznacza to, że nie można ich zmodyfikować w miejscu, chyba że jawnie Oznacz je jako modyfikowalne.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-192">That means they cannot be mutated in-place unless you explicitly mark them as mutable.</span></span>

<span data-ttu-id="7a9ec-193">W tym przypadku praca z niezmiennymi wartościami oznacza zmianę podejścia do programowania z, "muszę zmienić coś" na "chcę utworzyć nową wartość".</span><span class="sxs-lookup"><span data-stu-id="7a9ec-193">In practice, working with immutable values means that you change your approach to programming from, "I need to change something", to "I need to produce a new value".</span></span>

<span data-ttu-id="7a9ec-194">Na przykład dodanie 1 do wartości oznacza wygenerowanie nowej wartości, a nie mutację istniejącej:</span><span class="sxs-lookup"><span data-stu-id="7a9ec-194">For example, adding 1 to a value means producing a new value, not mutating the existing one:</span></span>

```fsharp
let value = 1
let secondValue = value + 1
```

<span data-ttu-id="7a9ec-195">W języku F # następujący **kod nie ma mutacji** `value` funkcji; zamiast tego wykonuje kontrolę równości:</span><span class="sxs-lookup"><span data-stu-id="7a9ec-195">In F#, the following code does **not** mutate the `value` function; instead, it performs an equality check:</span></span>

```fsharp
let value = 1
value = value + 1 // Produces a 'bool' value!
```

<span data-ttu-id="7a9ec-196">Niektóre funkcjonalne Języki programowania nie obsługują mutacji.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-196">Some functional programming languages do not support mutation at all.</span></span> <span data-ttu-id="7a9ec-197">W języku F # jest obsługiwane, ale nie jest to domyślne zachowanie dla wartości.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-197">In F#, it is supported, but it is not the default behavior for values.</span></span>

<span data-ttu-id="7a9ec-198">Koncepcja ta rozszerza jeszcze więcej do struktur danych.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-198">This concept extends even further to data structures.</span></span> <span data-ttu-id="7a9ec-199">W programowaniu funkcjonalnym niezmienne struktury danych, takie jak zestawy (i wiele innych), mają inną implementację niż oczekiwano.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-199">In functional programming, immutable data structures such as sets (and many more) have a different implementation than you might initially expect.</span></span> <span data-ttu-id="7a9ec-200">Ze względu na to, że dodanie elementu do zestawu nie powoduje zmiany zestawu, tworzy _Nowy_ zestaw z dodaną wartością.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-200">Conceptually, something like adding an item to a set does not change the set, it produces a _new_ set with the added value.</span></span> <span data-ttu-id="7a9ec-201">W obszarze okładek jest to często realizowane przez inną strukturę danych, która umożliwia efektywne śledzenie wartości, dzięki czemu w wyniku tego można otrzymać odpowiednią reprezentację danych.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-201">Under the covers, this is often accomplished by a different data structure that allows for efficiently tracking a value so that the appropriate representation of the data can be given as a result.</span></span>

<span data-ttu-id="7a9ec-202">Ten styl pracy z wartościami i strukturami danych jest krytyczny, ponieważ Wymusza traktowanie dowolnej operacji, która modyfikuje coś, tak jakby tworzy nową wersję tego elementu.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-202">This style of working with values and data structures is critical, as it forces you to treat any operation that modifies something as if it creates a new version of that thing.</span></span> <span data-ttu-id="7a9ec-203">Pozwala to na takie jak równość i porównywalność w programach.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-203">This allows for things like equality and comparability to be consistent in your programs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a9ec-204">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7a9ec-204">Next steps</span></span>

<span data-ttu-id="7a9ec-205">W następnej sekcji znajdują się dokładne funkcje, eksplorowanie różnych sposobów korzystania z nich w programowaniu funkcjonalnym.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-205">The next section will thoroughly cover functions, exploring different ways you can use them in functional programming.</span></span>

<span data-ttu-id="7a9ec-206">[Funkcje pierwszej klasy](first-class-functions.md) eksplorują funkcje głęboko i pokazują, jak można ich używać w różnych kontekstach.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-206">[First-class functions](first-class-functions.md) explores functions deeply, showing how you can use them in various contexts.</span></span>

## <a name="further-reading"></a><span data-ttu-id="7a9ec-207">Dalsze informacje</span><span class="sxs-lookup"><span data-stu-id="7a9ec-207">Further reading</span></span>

<span data-ttu-id="7a9ec-208">Warto zastanowić [się, że szereg funkcjonalny](https://fsharpforfunandprofit.com/posts/thinking-functionally-intro/) jest innym doskonałym zasobem, aby uzyskać informacje na temat programowania funkcjonalnego w języku F #</span><span class="sxs-lookup"><span data-stu-id="7a9ec-208">The [Thinking Functionally](https://fsharpforfunandprofit.com/posts/thinking-functionally-intro/) series is another great resource to learn about functional programming with F#.</span></span> <span data-ttu-id="7a9ec-209">Obejmuje ona podstawowe programowanie funkcjonalne w sposób pragmatyczny i łatwy do odczytu, przy użyciu funkcji języka F # do zilustrowania koncepcji.</span><span class="sxs-lookup"><span data-stu-id="7a9ec-209">It covers fundamentals of functional programming in a pragmatic and easy-to-read way, using F# features to illustrate the concepts.</span></span>
