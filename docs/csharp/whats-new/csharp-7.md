---
title: Co nowego w języku C# 7,0 — przewodnik w języku C#
description: Zapoznaj się z omówieniem nowych funkcji w wersji 7,0 języka C#.
ms.date: 10/02/2020
ms.assetid: fd41596d-d0c2-4816-b94d-c4d00a5d0243
ms.openlocfilehash: c238439b0f435e579d932b3b1eb13e9b0061fa5f
ms.sourcegitcommit: 4b79862c5b41fbd86cf38f926f6a49516059f6f2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/18/2020
ms.locfileid: "97678227"
---
# <a name="whats-new-in-c-70-through-c-73"></a><span data-ttu-id="5df8f-103">Co nowego w języku C# 7,0 za poorednictwem języka C# 7,3</span><span class="sxs-lookup"><span data-stu-id="5df8f-103">What's new in C# 7.0 through C# 7.3</span></span>

<span data-ttu-id="5df8f-104">W języku c# 7,0 do języka C# 7,3 wprowadzono wiele funkcji i przyrostowe ulepszenia środowiska programistycznego w języku C#.</span><span class="sxs-lookup"><span data-stu-id="5df8f-104">C# 7.0 through C# 7.3 brought a number of features and incremental improvements to your development experience with C#.</span></span> <span data-ttu-id="5df8f-105">Ten artykuł zawiera omówienie nowych funkcji języka i opcji kompilatora.</span><span class="sxs-lookup"><span data-stu-id="5df8f-105">This article provides an overview of the new language features and compiler options.</span></span> <span data-ttu-id="5df8f-106">Opisy opisują zachowanie języka C# 7,3, który jest najnowszą wersją obsługiwaną dla aplikacji opartych na .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="5df8f-106">The descriptions describe the behavior for C# 7.3, which is the most recent version supported for .NET Framework-based applications.</span></span>

<span data-ttu-id="5df8f-107">Element konfiguracji [wyboru wersji języka](../language-reference/configure-language-version.md) został dodany przy użyciu języka C# 7,1, który umożliwia określenie wersji języka kompilatora w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="5df8f-107">The [language version selection](../language-reference/configure-language-version.md) configuration element was added with C# 7.1, which enables you to specify the compiler language version in your project file.</span></span>

<span data-ttu-id="5df8f-108">C# 7.0 — 7.3 dodaje te funkcje i motywy do języka C#:</span><span class="sxs-lookup"><span data-stu-id="5df8f-108">C# 7.0-7.3 adds these features and themes to the C# language:</span></span>

- [<span data-ttu-id="5df8f-109">Krotki i odrzuty</span><span class="sxs-lookup"><span data-stu-id="5df8f-109">Tuples and discards</span></span>](#tuples-and-discards)
  - <span data-ttu-id="5df8f-110">Można tworzyć lekkie, nienazwane typy, które zawierają wiele pól publicznych.</span><span class="sxs-lookup"><span data-stu-id="5df8f-110">You can create lightweight, unnamed types that contain multiple public fields.</span></span> <span data-ttu-id="5df8f-111">Narzędzia kompilatora i IDE rozumieją semantykę tych typów.</span><span class="sxs-lookup"><span data-stu-id="5df8f-111">Compilers and IDE tools understand the semantics of these types.</span></span>
  - <span data-ttu-id="5df8f-112">Odrzucenia są tymczasowymi zmiennymi tylko do zapisu, które są używane w przypisaniach, gdy nie ma opieki nad przypisaną wartością.</span><span class="sxs-lookup"><span data-stu-id="5df8f-112">Discards are temporary, write-only variables used in assignments when you don't care about the value assigned.</span></span> <span data-ttu-id="5df8f-113">Są one najbardziej przydatne podczas dekonstrukcji krotek i typów zdefiniowanych przez użytkownika, a także podczas wywoływania metod z `out` parametrami.</span><span class="sxs-lookup"><span data-stu-id="5df8f-113">They're most useful when deconstructing tuples and user-defined types, as well as when calling methods with `out` parameters.</span></span>
- [<span data-ttu-id="5df8f-114">Dopasowanie wzorca</span><span class="sxs-lookup"><span data-stu-id="5df8f-114">Pattern Matching</span></span>](#pattern-matching)
  - <span data-ttu-id="5df8f-115">Można utworzyć logikę rozgałęziania na podstawie dowolnego typu i wartości elementów członkowskich tych typów.</span><span class="sxs-lookup"><span data-stu-id="5df8f-115">You can create branching logic based on arbitrary types and values of the members of those types.</span></span>
- [<span data-ttu-id="5df8f-116">`async``Main`Metoda</span><span class="sxs-lookup"><span data-stu-id="5df8f-116">`async` `Main` method</span></span>](#async-main)
  - <span data-ttu-id="5df8f-117">Punkt wejścia dla aplikacji może mieć `async` modyfikator.</span><span class="sxs-lookup"><span data-stu-id="5df8f-117">The entry point for an application can have the `async` modifier.</span></span>
- [<span data-ttu-id="5df8f-118">Funkcje lokalne</span><span class="sxs-lookup"><span data-stu-id="5df8f-118">Local Functions</span></span>](#local-functions)
  - <span data-ttu-id="5df8f-119">Funkcje w innych funkcjach można zagnieżdżać w celu ograniczenia ich zakresu i widoczności.</span><span class="sxs-lookup"><span data-stu-id="5df8f-119">You can nest functions inside other functions to limit their scope and visibility.</span></span>
- [<span data-ttu-id="5df8f-120">Więcej składowych wyrażeń</span><span class="sxs-lookup"><span data-stu-id="5df8f-120">More expression-bodied members</span></span>](#more-expression-bodied-members)
  - <span data-ttu-id="5df8f-121">Lista elementów członkowskich, które mogą zostać utworzone przy użyciu wyrażeń.</span><span class="sxs-lookup"><span data-stu-id="5df8f-121">The list of members that can be authored using expressions has grown.</span></span>
- [<span data-ttu-id="5df8f-122">`throw` Wyrażeń</span><span class="sxs-lookup"><span data-stu-id="5df8f-122">`throw` Expressions</span></span>](#throw-expressions)
  - <span data-ttu-id="5df8f-123">Można zgłosić wyjątki w konstrukcjach kodu, które wcześniej nie były dozwolone, ponieważ `throw` była instrukcją.</span><span class="sxs-lookup"><span data-stu-id="5df8f-123">You can throw exceptions in code constructs that previously weren't allowed because `throw` was a statement.</span></span>
- [<span data-ttu-id="5df8f-124">`default` wyrażenia literału</span><span class="sxs-lookup"><span data-stu-id="5df8f-124">`default` literal expressions</span></span>](#default-literal-expressions)
  - <span data-ttu-id="5df8f-125">Można użyć domyślnych wyrażeń literałów w wyrażeniach wartości domyślnych, gdy można wywnioskować typ docelowy.</span><span class="sxs-lookup"><span data-stu-id="5df8f-125">You can use default literal expressions in default value expressions when the target type can be inferred.</span></span>
- [<span data-ttu-id="5df8f-126">Udoskonalenia składni literału liczbowego</span><span class="sxs-lookup"><span data-stu-id="5df8f-126">Numeric literal syntax improvements</span></span>](#numeric-literal-syntax-improvements)
  - <span data-ttu-id="5df8f-127">Nowe tokeny zwiększają czytelność dla stałych numerycznych.</span><span class="sxs-lookup"><span data-stu-id="5df8f-127">New tokens improve readability for numeric constants.</span></span>
- [<span data-ttu-id="5df8f-128">`out` modyfikacj</span><span class="sxs-lookup"><span data-stu-id="5df8f-128">`out` variables</span></span>](#out-variables)
  - <span data-ttu-id="5df8f-129">Można zadeklarować `out` wartości jako argumenty metody, gdzie są używane.</span><span class="sxs-lookup"><span data-stu-id="5df8f-129">You can declare `out` values inline as arguments to the method where they're used.</span></span>
- [<span data-ttu-id="5df8f-130">Argumenty nazwane inne niż końcowe</span><span class="sxs-lookup"><span data-stu-id="5df8f-130">Non-trailing named arguments</span></span>](#non-trailing-named-arguments)
  - <span data-ttu-id="5df8f-131">Po nazwanych argumentach mogą występować argumenty pozycyjne.</span><span class="sxs-lookup"><span data-stu-id="5df8f-131">Named arguments can be followed by positional arguments.</span></span>
- [<span data-ttu-id="5df8f-132">`private protected` Modyfikator dostępu</span><span class="sxs-lookup"><span data-stu-id="5df8f-132">`private protected` access modifier</span></span>](#private-protected-access-modifier)
  - <span data-ttu-id="5df8f-133">`private protected`Modyfikator dostępu umożliwia dostęp do klas pochodnych w tym samym zestawie.</span><span class="sxs-lookup"><span data-stu-id="5df8f-133">The `private protected` access modifier enables access for derived classes in the same assembly.</span></span>
- [<span data-ttu-id="5df8f-134">Ulepszone rozwiązanie przeciążania</span><span class="sxs-lookup"><span data-stu-id="5df8f-134">Improved overload resolution</span></span>](#improved-overload-candidates)
  - <span data-ttu-id="5df8f-135">Nowe reguły do rozwiązywania niejednoznaczności rozpoznawania przeciążenia.</span><span class="sxs-lookup"><span data-stu-id="5df8f-135">New rules to resolve overload resolution ambiguity.</span></span>
- [<span data-ttu-id="5df8f-136">Techniki pisania bezpiecznego wydajnego kodu</span><span class="sxs-lookup"><span data-stu-id="5df8f-136">Techniques for writing safe efficient code</span></span>](#enabling-more-efficient-safe-code)
  - <span data-ttu-id="5df8f-137">Kombinacja ulepszeń składni, które umożliwiają pracę z typami wartości przy użyciu semantyki referencyjnej.</span><span class="sxs-lookup"><span data-stu-id="5df8f-137">A combination of syntax improvements that enable working with value types using reference semantics.</span></span>

<span data-ttu-id="5df8f-138">Na koniec kompilator ma nowe opcje:</span><span class="sxs-lookup"><span data-stu-id="5df8f-138">Finally, the compiler has new options:</span></span>

- <span data-ttu-id="5df8f-139">`-refout` i `-refonly` tej kontrolki [generacji zestawu odwołania](#reference-assembly-generation).</span><span class="sxs-lookup"><span data-stu-id="5df8f-139">`-refout` and `-refonly` that control [reference assembly generation](#reference-assembly-generation).</span></span>
- <span data-ttu-id="5df8f-140">`-publicsign` Aby włączyć podpisywanie zestawów przez oprogramowanie typu Open Source (OSS).</span><span class="sxs-lookup"><span data-stu-id="5df8f-140">`-publicsign` to enable Open Source Software (OSS) signing of assemblies.</span></span>
- <span data-ttu-id="5df8f-141">`-pathmap` w celu zapewnienia mapowania dla katalogów źródłowych.</span><span class="sxs-lookup"><span data-stu-id="5df8f-141">`-pathmap` to provide a mapping for source directories.</span></span>

<span data-ttu-id="5df8f-142">Pozostała część tego artykułu zawiera omówienie każdej funkcji.</span><span class="sxs-lookup"><span data-stu-id="5df8f-142">The remainder of this article provides an overview of each feature.</span></span> <span data-ttu-id="5df8f-143">Dla każdej funkcji należy zapoznać się z jej uzasadnieniem i składnią.</span><span class="sxs-lookup"><span data-stu-id="5df8f-143">For each feature, you'll learn the reasoning behind it and the syntax.</span></span> <span data-ttu-id="5df8f-144">Te funkcje można eksplorować w środowisku za pomocą `dotnet try` Narzędzia globalnego:</span><span class="sxs-lookup"><span data-stu-id="5df8f-144">You can explore these features in your environment using the `dotnet try` global tool:</span></span>

1. <span data-ttu-id="5df8f-145">Zainstaluj narzędzie [dotnet-try](https://github.com/dotnet/try/blob/master/README.md#setup) Global.</span><span class="sxs-lookup"><span data-stu-id="5df8f-145">Install the [dotnet-try](https://github.com/dotnet/try/blob/master/README.md#setup) global tool.</span></span>
1. <span data-ttu-id="5df8f-146">Sklonuj repozytorium [dotnet/try-Samples](https://github.com/dotnet/try-samples) .</span><span class="sxs-lookup"><span data-stu-id="5df8f-146">Clone the [dotnet/try-samples](https://github.com/dotnet/try-samples) repository.</span></span>
1. <span data-ttu-id="5df8f-147">Ustaw bieżący katalog na podkatalog *csharp7* dla repozytorium *try-Samples* .</span><span class="sxs-lookup"><span data-stu-id="5df8f-147">Set the current directory to the *csharp7* subdirectory for the *try-samples* repository.</span></span>
1. <span data-ttu-id="5df8f-148">Uruchom polecenie `dotnet try`.</span><span class="sxs-lookup"><span data-stu-id="5df8f-148">Run `dotnet try`.</span></span>

## <a name="tuples-and-discards"></a><span data-ttu-id="5df8f-149">Krotki i odrzuty</span><span class="sxs-lookup"><span data-stu-id="5df8f-149">Tuples and discards</span></span>

<span data-ttu-id="5df8f-150">Język C# zawiera rozbudowaną składnię dla klas i struktur, które są używane do wyjaśnienia zamiaru projektowania.</span><span class="sxs-lookup"><span data-stu-id="5df8f-150">C# provides a rich syntax for classes and structs that is used to explain your design intent.</span></span> <span data-ttu-id="5df8f-151">Jednak czasami rozbudowana Składnia wymaga dodatkowej pracy z minimalną korzyścią.</span><span class="sxs-lookup"><span data-stu-id="5df8f-151">But sometimes that rich syntax requires extra work with minimal benefit.</span></span> <span data-ttu-id="5df8f-152">Często możesz pisać metody, które potrzebują prostej struktury zawierającej więcej niż jeden element danych.</span><span class="sxs-lookup"><span data-stu-id="5df8f-152">You may often write methods that need a simple structure containing more than one data element.</span></span> <span data-ttu-id="5df8f-153">Aby obsługiwać te scenariusze, *krotki* zostały dodane do języka C#.</span><span class="sxs-lookup"><span data-stu-id="5df8f-153">To support these scenarios *tuples* were added to C#.</span></span> <span data-ttu-id="5df8f-154">Krotki są lekkimi strukturami danych, które zawierają wiele pól do reprezentowania elementów członkowskich danych.</span><span class="sxs-lookup"><span data-stu-id="5df8f-154">Tuples are lightweight data structures that contain multiple fields to represent the data members.</span></span> <span data-ttu-id="5df8f-155">Pola nie są weryfikowane i nie można definiować własnych metod.</span><span class="sxs-lookup"><span data-stu-id="5df8f-155">The fields aren't validated, and you can't define your own methods.</span></span> <span data-ttu-id="5df8f-156">Typy krotek języka C# obsługują `==` i `!=` .</span><span class="sxs-lookup"><span data-stu-id="5df8f-156">C# tuple types support `==` and `!=`.</span></span> <span data-ttu-id="5df8f-157">Więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="5df8f-157">For more information.</span></span>

> [!NOTE]
> <span data-ttu-id="5df8f-158">Krotki były dostępne przed C# 7,0, ale były niewydajne i nie obsługiwały języka.</span><span class="sxs-lookup"><span data-stu-id="5df8f-158">Tuples were available before C# 7.0, but they were inefficient and had no language support.</span></span> <span data-ttu-id="5df8f-159">Oznacza to, że elementy krotki mogą być przywoływane tylko jako `Item1` `Item2` i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="5df8f-159">This meant that tuple elements could only be referenced as `Item1`, `Item2` and so on.</span></span> <span data-ttu-id="5df8f-160">W języku C# 7,0 wprowadzono obsługę języka dla krotek, która umożliwia używanie nazw semantycznych dla pól krotki przy użyciu nowych, wydajniejszych typów krotek.</span><span class="sxs-lookup"><span data-stu-id="5df8f-160">C# 7.0 introduces language support for tuples, which enables semantic names for the fields of a tuple using new, more efficient tuple types.</span></span>

<span data-ttu-id="5df8f-161">Można utworzyć krotkę, przypisując wartość do każdego elementu członkowskiego, a opcjonalnie dostarczając nazwy semantyczne dla każdego z elementów członkowskich krotki:</span><span class="sxs-lookup"><span data-stu-id="5df8f-161">You can create a tuple by assigning a value to each member, and optionally providing semantic names to each of the members of the tuple:</span></span>

[!code-csharp[NamedTuple](~/samples/snippets/csharp/new-in-7/program.cs#NamedTuple "Named tuple")]

<span data-ttu-id="5df8f-162">`namedLetters`Krotka zawiera pola, które są określane jako `Alpha` i `Beta` .</span><span class="sxs-lookup"><span data-stu-id="5df8f-162">The `namedLetters` tuple contains fields referred to as `Alpha` and `Beta`.</span></span> <span data-ttu-id="5df8f-163">Te nazwy istnieją tylko w czasie kompilacji i nie są zachowywane, na przykład podczas sprawdzania krotki przy użyciu odbicia w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="5df8f-163">Those names exist only at compile time and aren't preserved, for example when inspecting the tuple using reflection at run time.</span></span>

<span data-ttu-id="5df8f-164">W przypisaniu spójnej kolekcji można także określić nazwy pól po prawej stronie przypisania:</span><span class="sxs-lookup"><span data-stu-id="5df8f-164">In a tuple assignment, you can also specify the names of the fields on the right-hand side of the assignment:</span></span>

[!code-csharp[ImplicitNamedTuple](~/samples/snippets/csharp/new-in-7/program.cs#ImplicitNamedTuple "Implicitly named tuple")]

<span data-ttu-id="5df8f-165">Mogą wystąpić sytuacje, w których chcesz rozpakować elementy członkowskie spójnej kolekcji, która została zwrócona z metody.</span><span class="sxs-lookup"><span data-stu-id="5df8f-165">There may be times when you want to unpackage the members of a tuple that were returned from a method.</span></span>  <span data-ttu-id="5df8f-166">Można to zrobić przez zadeklarowanie oddzielnych zmiennych dla każdej wartości w spójnej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="5df8f-166">You can do that by declaring separate variables for each of the values in the tuple.</span></span> <span data-ttu-id="5df8f-167">To rozpakowanie nosi nazwę *dekonstrukcja* krotki:</span><span class="sxs-lookup"><span data-stu-id="5df8f-167">This unpackaging is called *deconstructing* the tuple:</span></span>

[!code-csharp[CallingWithDeconstructor](~/samples/snippets/csharp/new-in-7/program.cs#CallingWithDeconstructor "Deconstructing a tuple")]

<span data-ttu-id="5df8f-168">Można także zapewnić podobną dekonstrukcję dla dowolnego typu w programie .NET.</span><span class="sxs-lookup"><span data-stu-id="5df8f-168">You can also provide a similar deconstruction for any type in .NET.</span></span> <span data-ttu-id="5df8f-169">Należy napisać `Deconstruct` metodę jako element członkowski klasy.</span><span class="sxs-lookup"><span data-stu-id="5df8f-169">You write a `Deconstruct` method as a member of the class.</span></span> <span data-ttu-id="5df8f-170">Ta `Deconstruct` Metoda zapewnia zestaw `out` argumentów dla każdej właściwości, które mają zostać wyodrębnione.</span><span class="sxs-lookup"><span data-stu-id="5df8f-170">That `Deconstruct` method provides a set of `out` arguments for each of the properties you want to extract.</span></span> <span data-ttu-id="5df8f-171">Rozważmy tę `Point` klasę, która zapewnia metodę dekonstruktora, która `X` wyodrębnia `Y` współrzędne i:</span><span class="sxs-lookup"><span data-stu-id="5df8f-171">Consider this `Point` class that provides a deconstructor method that extracts the `X` and `Y` coordinates:</span></span>

[!code-csharp[PointWithDeconstruction](~/samples/snippets/csharp/new-in-7/point.cs#PointWithDeconstruction "Point with deconstruction method")]

<span data-ttu-id="5df8f-172">Poszczególne pola można wyodrębnić, przypisując `Point` do krotki:</span><span class="sxs-lookup"><span data-stu-id="5df8f-172">You can extract the individual fields by assigning a `Point` to a tuple:</span></span>

[!code-csharp[DeconstructPoint](~/samples/snippets/csharp/new-in-7/program.cs#DeconstructPoint "Deconstruct a point")]

<span data-ttu-id="5df8f-173">Wiele razy podczas inicjowania krotki zmienne używane po prawej stronie przypisania są takie same jak nazwy dla elementów krotki: nazwy elementów krotki mogą być wywnioskowane na podstawie zmiennych używanych do inicjowania krotki:</span><span class="sxs-lookup"><span data-stu-id="5df8f-173">Many times when you initialize a tuple, the variables used for the right side of the assignment are the same as the names you'd like for the tuple elements: The names of tuple elements can be inferred from the variables used to initialize the tuple:</span></span>

```csharp
int count = 5;
string label = "Colors used in the map";
var pair = (count, label); // element names are "count" and "label"
```

<span data-ttu-id="5df8f-174">Więcej informacji na temat tej funkcji można znaleźć w artykule [typy krotek](../language-reference/builtin-types/value-tuples.md) .</span><span class="sxs-lookup"><span data-stu-id="5df8f-174">You can learn more about this feature in the [Tuple types](../language-reference/builtin-types/value-tuples.md) article.</span></span>

<span data-ttu-id="5df8f-175">Często podczas dekonstruowania krotki lub wywoływania metody z `out` parametrami należy wymusić zdefiniowanie zmiennej, której wartość nie ma znaczenia, i nie zamierza się jej używać.</span><span class="sxs-lookup"><span data-stu-id="5df8f-175">Often when deconstructing a tuple or calling a method with `out` parameters, you're forced to define a variable whose value you don't care about and don't intend to use.</span></span> <span data-ttu-id="5df8f-176">Język C# dodaje obsługę *odrzutów* , aby obsłużyć ten scenariusz.</span><span class="sxs-lookup"><span data-stu-id="5df8f-176">C# adds support for *discards* to handle this scenario.</span></span> <span data-ttu-id="5df8f-177">Odrzucanie to zmienna tylko do zapisu, której nazwa to `_` (znak podkreślenia); można przypisać wszystkie wartości, które mają zostać odrzucone do pojedynczej zmiennej.</span><span class="sxs-lookup"><span data-stu-id="5df8f-177">A discard is a write-only variable whose name is `_` (the underscore character); you can assign all of the values that you intend to discard to the single variable.</span></span> <span data-ttu-id="5df8f-178">Odrzucenie przypomina przypisaną zmienną; poza instrukcją przypisania nie można używać odrzucania w kodzie.</span><span class="sxs-lookup"><span data-stu-id="5df8f-178">A discard is like an unassigned variable; apart from the assignment statement, the discard can't be used in code.</span></span>

<span data-ttu-id="5df8f-179">Odrzucenia są obsługiwane w następujących scenariuszach:</span><span class="sxs-lookup"><span data-stu-id="5df8f-179">Discards are supported in the following scenarios:</span></span>

- <span data-ttu-id="5df8f-180">Podczas dekonstrukcji krotek lub typów zdefiniowanych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5df8f-180">When deconstructing tuples or user-defined types.</span></span>
- <span data-ttu-id="5df8f-181">Podczas wywoływania metod z parametrami [out](../language-reference/keywords/out-parameter-modifier.md) .</span><span class="sxs-lookup"><span data-stu-id="5df8f-181">When calling methods with [out](../language-reference/keywords/out-parameter-modifier.md) parameters.</span></span>
- <span data-ttu-id="5df8f-182">W operacji dopasowania wzorca z instrukcjami with [i](../language-reference/keywords/is.md) [Switch](../language-reference/keywords/switch.md) .</span><span class="sxs-lookup"><span data-stu-id="5df8f-182">In a pattern matching operation with the [is](../language-reference/keywords/is.md) and [switch](../language-reference/keywords/switch.md) statements.</span></span>
- <span data-ttu-id="5df8f-183">Jako identyfikator autonomiczny, gdy chcesz jawnie określić wartość przypisania jako odrzucenie.</span><span class="sxs-lookup"><span data-stu-id="5df8f-183">As a standalone identifier when you want to explicitly identify the value of an assignment as a discard.</span></span>

<span data-ttu-id="5df8f-184">W poniższym przykładzie zdefiniowano `QueryCityDataForYears` metodę, która zwraca 6-krotkę zawierającą dane dla miasta na dwa różne lata.</span><span class="sxs-lookup"><span data-stu-id="5df8f-184">The following example defines a `QueryCityDataForYears` method that returns a 6-tuple that contains data for a city for two different years.</span></span> <span data-ttu-id="5df8f-185">Wywołanie metody w przykładzie jest rozważane tylko z dwiema wartościami populacji zwracanymi przez metodę i dlatego traktują pozostałe wartości w spójnej kolekcji jako odrzucane podczas dekonstruowania krotki.</span><span class="sxs-lookup"><span data-stu-id="5df8f-185">The method call in the example is concerned only with the two population values returned by the method and so treats the remaining values in the tuple as discards when it deconstructs the tuple.</span></span>

[!code-csharp[Tuple-discard](~/samples/snippets/csharp/programming-guide/deconstructing-tuples/discard-tuple1.cs)]

<span data-ttu-id="5df8f-186">Aby uzyskać więcej informacji, zobacz [odrzucanie](../discards.md).</span><span class="sxs-lookup"><span data-stu-id="5df8f-186">For more information, see [Discards](../discards.md).</span></span>

## <a name="pattern-matching"></a><span data-ttu-id="5df8f-187">Dopasowanie do wzorca</span><span class="sxs-lookup"><span data-stu-id="5df8f-187">Pattern matching</span></span>

<span data-ttu-id="5df8f-188">*Dopasowanie wzorca* to zestaw funkcji umożliwiających nowe sposoby wyrażania przepływu sterowania w kodzie.</span><span class="sxs-lookup"><span data-stu-id="5df8f-188">*Pattern matching* is a set of features that enable new ways to express control flow in your code.</span></span> <span data-ttu-id="5df8f-189">Można testować zmienne dla ich typów, wartości lub wartości właściwości.</span><span class="sxs-lookup"><span data-stu-id="5df8f-189">You can test variables for their type, values or the values of their properties.</span></span> <span data-ttu-id="5df8f-190">Techniki te tworzą bardziej czytelny przepływ kodu.</span><span class="sxs-lookup"><span data-stu-id="5df8f-190">These techniques create more readable code flow.</span></span>

<span data-ttu-id="5df8f-191">Dopasowywanie wzorców obsługuje `is` wyrażenia i `switch` wyrażenia.</span><span class="sxs-lookup"><span data-stu-id="5df8f-191">Pattern matching supports `is` expressions and `switch` expressions.</span></span> <span data-ttu-id="5df8f-192">Każdy umożliwia inspekcję obiektu i jego właściwości w celu ustalenia, czy ten obiekt spełnia oczekiwany wzorzec.</span><span class="sxs-lookup"><span data-stu-id="5df8f-192">Each enables inspecting an object and its properties to determine if that object satisfies the sought pattern.</span></span> <span data-ttu-id="5df8f-193">Użyj `when` słowa kluczowego, aby określić dodatkowe reguły do wzorca.</span><span class="sxs-lookup"><span data-stu-id="5df8f-193">You use the `when` keyword to specify additional rules to the pattern.</span></span>

<span data-ttu-id="5df8f-194">`is`Wyrażenie wzorca rozszerza znanego [ `is` operatora](../language-reference/keywords/is.md#pattern-matching-with-is) w celu zbadania obiektu o jego typie i przypisuje wynik w jednej instrukcji.</span><span class="sxs-lookup"><span data-stu-id="5df8f-194">The `is` pattern expression extends the familiar [`is` operator](../language-reference/keywords/is.md#pattern-matching-with-is) to query an object about its type and assign the result in one instruction.</span></span> <span data-ttu-id="5df8f-195">Poniższy kod sprawdza, czy zmienna jest `int` , i jeśli tak, dodaje ją do bieżącej sumy:</span><span class="sxs-lookup"><span data-stu-id="5df8f-195">The following code checks if a variable is an `int`, and if so, adds it to the current sum:</span></span>

```csharp
if (input is int count)
    sum += count;
```

<span data-ttu-id="5df8f-196">Powyższy mały przykład ilustruje ulepszenia `is` wyrażenia.</span><span class="sxs-lookup"><span data-stu-id="5df8f-196">The preceding small example demonstrates the enhancements to the `is` expression.</span></span> <span data-ttu-id="5df8f-197">Można testować względem typów wartości, a także typów referencyjnych, a następnie można przypisać prawidłowy wynik do nowej zmiennej poprawnego typu.</span><span class="sxs-lookup"><span data-stu-id="5df8f-197">You can test against value types as well as reference types, and you can assign the successful result to a new variable of the correct type.</span></span>

<span data-ttu-id="5df8f-198">Wyrażenie dopasowania przełącznika ma znaną składnię opartą na instrukcji, która jest `switch` już częścią języka C#.</span><span class="sxs-lookup"><span data-stu-id="5df8f-198">The switch match expression has a familiar syntax, based on the `switch` statement already part of the C# language.</span></span> <span data-ttu-id="5df8f-199">Zaktualizowana instrukcja SWITCH zawiera kilka nowych konstrukcji:</span><span class="sxs-lookup"><span data-stu-id="5df8f-199">The updated switch statement has several new constructs:</span></span>

- <span data-ttu-id="5df8f-200">Typ decydujący `switch` wyrażenia nie jest już ograniczony do typów całkowitych, `Enum` typów, `string` lub typu dopuszczającego wartość null odpowiadającego jednemu z tych typów.</span><span class="sxs-lookup"><span data-stu-id="5df8f-200">The governing type of a `switch` expression is no longer restricted to integral types, `Enum` types, `string`, or a nullable type corresponding to one of those types.</span></span> <span data-ttu-id="5df8f-201">Można użyć dowolnego typu.</span><span class="sxs-lookup"><span data-stu-id="5df8f-201">Any type may be used.</span></span>
- <span data-ttu-id="5df8f-202">Możesz przetestować typ `switch` wyrażenia w każdej `case` etykiecie.</span><span class="sxs-lookup"><span data-stu-id="5df8f-202">You can test the type of the `switch` expression in each `case` label.</span></span> <span data-ttu-id="5df8f-203">Podobnie jak w przypadku `is` wyrażenia, można przypisać nową zmienną do tego typu.</span><span class="sxs-lookup"><span data-stu-id="5df8f-203">As with the `is` expression, you may assign a new variable to that type.</span></span>
- <span data-ttu-id="5df8f-204">Można dodać `when` klauzulę do dalszych warunków testowania dla tej zmiennej.</span><span class="sxs-lookup"><span data-stu-id="5df8f-204">You may add a `when` clause to further test conditions on that variable.</span></span>
- <span data-ttu-id="5df8f-205">Kolejność `case` etykiet jest teraz ważna.</span><span class="sxs-lookup"><span data-stu-id="5df8f-205">The order of `case` labels is now important.</span></span> <span data-ttu-id="5df8f-206">Pierwsza gałąź do dopasowania jest wykonywana; pozostałe są pomijane.</span><span class="sxs-lookup"><span data-stu-id="5df8f-206">The first branch to match is executed; others are skipped.</span></span>

<span data-ttu-id="5df8f-207">Poniższy kod ilustruje następujące nowe funkcje:</span><span class="sxs-lookup"><span data-stu-id="5df8f-207">The following code demonstrates these new features:</span></span>

```csharp
public static int SumPositiveNumbers(IEnumerable<object> sequence)
{
    int sum = 0;
    foreach (var i in sequence)
    {
        switch (i)
        {
            case 0:
                break;
            case IEnumerable<int> childSequence:
            {
                foreach(var item in childSequence)
                    sum += (item > 0) ? item : 0;
                break;
            }
            case int n when n > 0:
                sum += n;
                break;
            case null:
                throw new NullReferenceException("Null found in sequence");
            default:
                throw new InvalidOperationException("Unrecognized type");
        }
    }
    return sum;
}
```

- <span data-ttu-id="5df8f-208">`case 0:` jest znanym wzorcem stałej.</span><span class="sxs-lookup"><span data-stu-id="5df8f-208">`case 0:` is the familiar constant pattern.</span></span>
- <span data-ttu-id="5df8f-209">`case IEnumerable<int> childSequence:` jest wzorcem typu.</span><span class="sxs-lookup"><span data-stu-id="5df8f-209">`case IEnumerable<int> childSequence:` is a type pattern.</span></span>
- <span data-ttu-id="5df8f-210">`case int n when n > 0:` jest wzorcem typu z dodatkowym `when` warunkiem.</span><span class="sxs-lookup"><span data-stu-id="5df8f-210">`case int n when n > 0:` is a type pattern with an additional `when` condition.</span></span>
- <span data-ttu-id="5df8f-211">`case null:` jest wzorcem o wartości null.</span><span class="sxs-lookup"><span data-stu-id="5df8f-211">`case null:` is the null pattern.</span></span>
- <span data-ttu-id="5df8f-212">`default:` jest znanym domyślnym przypadkiem.</span><span class="sxs-lookup"><span data-stu-id="5df8f-212">`default:` is the familiar default case.</span></span>

<span data-ttu-id="5df8f-213">Począwszy od języka C# 7,1 wyrażenie wzorca dla `is` i `switch` wzorzec typu może mieć typ parametru typu ogólnego.</span><span class="sxs-lookup"><span data-stu-id="5df8f-213">Beginning with C# 7.1, the pattern expression for `is` and the `switch` type pattern may have the type of a generic type parameter.</span></span> <span data-ttu-id="5df8f-214">Może to być najbardziej przydatne podczas sprawdzania typów, które mogą być `struct` albo `class` typu, i chcesz uniknąć pakowania.</span><span class="sxs-lookup"><span data-stu-id="5df8f-214">This can be most useful when checking types that may be either `struct` or `class` types, and you want to avoid boxing.</span></span>

<span data-ttu-id="5df8f-215">Dowiedz się więcej na temat dopasowywania wzorców we [wzorcu w języku C#](../pattern-matching.md).</span><span class="sxs-lookup"><span data-stu-id="5df8f-215">You can learn more about pattern matching in [Pattern Matching in C#](../pattern-matching.md).</span></span>

## <a name="async-main"></a><span data-ttu-id="5df8f-216">Asynchroniczny, główny</span><span class="sxs-lookup"><span data-stu-id="5df8f-216">Async main</span></span>

<span data-ttu-id="5df8f-217">Metoda *Async Main* umożliwia korzystanie `await` z `Main` metody.</span><span class="sxs-lookup"><span data-stu-id="5df8f-217">An *async main* method enables you to use `await` in your `Main` method.</span></span> <span data-ttu-id="5df8f-218">Wcześniej należy napisać:</span><span class="sxs-lookup"><span data-stu-id="5df8f-218">Previously you would need to write:</span></span>

```csharp
static int Main()
{
    return DoAsyncWork().GetAwaiter().GetResult();
}
```

<span data-ttu-id="5df8f-219">Teraz możesz napisać:</span><span class="sxs-lookup"><span data-stu-id="5df8f-219">You can now write:</span></span>

```csharp
static async Task<int> Main()
{
    // This could also be replaced with the body
    // DoAsyncWork, including its await expressions:
    return await DoAsyncWork();
}
```

<span data-ttu-id="5df8f-220">Jeśli program nie zwraca kodu zakończenia, można zadeklarować `Main` metodę, która zwraca <xref:System.Threading.Tasks.Task> :</span><span class="sxs-lookup"><span data-stu-id="5df8f-220">If your program doesn't return an exit code, you can declare a `Main` method that returns a <xref:System.Threading.Tasks.Task>:</span></span>

```csharp
static async Task Main()
{
    await SomeAsyncMethod();
}
```

<span data-ttu-id="5df8f-221">Więcej informacji na temat szczegółowych informacji można znaleźć w artykule dotyczącym [asynchronicznego](../programming-guide/main-and-command-args/index.md) artykułu w przewodniku programowania.</span><span class="sxs-lookup"><span data-stu-id="5df8f-221">You can read more about the details in the [async main](../programming-guide/main-and-command-args/index.md) article in the programming guide.</span></span>

## <a name="local-functions"></a><span data-ttu-id="5df8f-222">Funkcje lokalne</span><span class="sxs-lookup"><span data-stu-id="5df8f-222">Local functions</span></span>

<span data-ttu-id="5df8f-223">Wiele projektów klas obejmuje metody, które są wywoływane tylko z jednej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="5df8f-223">Many designs for classes include methods that are called from only one location.</span></span> <span data-ttu-id="5df8f-224">Te dodatkowe metody prywatne przechowują każdą metodę na małe i skoncentrowane.</span><span class="sxs-lookup"><span data-stu-id="5df8f-224">These additional private methods keep each method small and focused.</span></span> <span data-ttu-id="5df8f-225">*Funkcje lokalne* umożliwiają deklarowanie metod wewnątrz kontekstu innej metody.</span><span class="sxs-lookup"><span data-stu-id="5df8f-225">*Local functions* enable you to declare methods inside the context of another method.</span></span> <span data-ttu-id="5df8f-226">Funkcje lokalne ułatwiają czytelnikom klasy sprawdzenie, czy metoda lokalna jest wywoływana tylko z kontekstu, w którym jest zadeklarowana.</span><span class="sxs-lookup"><span data-stu-id="5df8f-226">Local functions make it easier for readers of the class to see that the local method is only called from the context in which it is declared.</span></span>

<span data-ttu-id="5df8f-227">Istnieją dwa typowe przypadki użycia funkcji lokalnych: metody iteratora publicznego i publiczne metody async.</span><span class="sxs-lookup"><span data-stu-id="5df8f-227">There are two common use cases for local functions: public iterator methods and public async methods.</span></span> <span data-ttu-id="5df8f-228">Oba typy metod generują kod, który zgłasza błędy później niż programiści mogą oczekiwać.</span><span class="sxs-lookup"><span data-stu-id="5df8f-228">Both types of methods generate code that reports errors later than programmers might expect.</span></span> <span data-ttu-id="5df8f-229">W metodach iteratora wszystkie wyjątki są obserwowane tylko podczas wywoływania kodu, który wylicza zwracaną sekwencję.</span><span class="sxs-lookup"><span data-stu-id="5df8f-229">In iterator methods, any exceptions are observed only when calling code that enumerates the returned sequence.</span></span> <span data-ttu-id="5df8f-230">W metodach asynchronicznych wszelkie wyjątki są przestrzegane tylko wtedy, gdy zwracane `Task` jest oczekiwane.</span><span class="sxs-lookup"><span data-stu-id="5df8f-230">In async methods, any exceptions are only observed when the returned `Task` is awaited.</span></span> <span data-ttu-id="5df8f-231">Poniższy przykład ilustruje oddzielanie walidacji parametrów od implementacji iteratora przy użyciu funkcji lokalnej:</span><span class="sxs-lookup"><span data-stu-id="5df8f-231">The following example demonstrates separating parameter validation from the iterator implementation using a local function:</span></span>

[!code-csharp[22_IteratorMethodLocal](~/samples/snippets/csharp/new-in-7/Iterator.cs#IteratorMethodLocal "Iterator method with local function")]

<span data-ttu-id="5df8f-232">Ta sama technika może być stosowana z `async` metodami, aby zapewnić, że wyjątki wynikające z walidacji argumentów są zgłaszane przed rozpoczęciem pracy asynchronicznej:</span><span class="sxs-lookup"><span data-stu-id="5df8f-232">The same technique can be employed with `async` methods to ensure that exceptions arising from argument validation are thrown before the asynchronous work begins:</span></span>

[!code-csharp[TaskExample](~/samples/snippets/csharp/new-in-7/AsyncWork.cs#TaskExample "Task returning method with local function")]

<span data-ttu-id="5df8f-233">Ta składnia jest teraz obsługiwana:</span><span class="sxs-lookup"><span data-stu-id="5df8f-233">This syntax is now supported:</span></span>

```csharp
[field: SomeThingAboutFieldAttribute]
public int SomeProperty { get; set; }
```

<span data-ttu-id="5df8f-234">Ten atrybut `SomeThingAboutFieldAttribute` jest stosowany do pola zapasowego wygenerowanego przez kompilator dla `SomeProperty` .</span><span class="sxs-lookup"><span data-stu-id="5df8f-234">The attribute `SomeThingAboutFieldAttribute` is applied to the compiler generated backing field for `SomeProperty`.</span></span> <span data-ttu-id="5df8f-235">Aby uzyskać więcej informacji, zobacz [atrybuty](../programming-guide/concepts/attributes/index.md) w Przewodnik programowania w języku C#.</span><span class="sxs-lookup"><span data-stu-id="5df8f-235">For more information, see [attributes](../programming-guide/concepts/attributes/index.md) in the C# programming guide.</span></span>

> [!NOTE]
> <span data-ttu-id="5df8f-236">Niektóre projekty, które są obsługiwane przez funkcje lokalne, można również zrealizować przy użyciu *wyrażeń lambda*.</span><span class="sxs-lookup"><span data-stu-id="5df8f-236">Some of the designs that are supported by local functions can also be accomplished using *lambda expressions*.</span></span> <span data-ttu-id="5df8f-237">Aby uzyskać więcej informacji, zobacz temat [funkcje lokalne a wyrażenia lambda](../programming-guide/classes-and-structs/local-functions.md#local-functions-vs-lambda-expressions).</span><span class="sxs-lookup"><span data-stu-id="5df8f-237">For more information, see [Local functions vs. lambda expressions](../programming-guide/classes-and-structs/local-functions.md#local-functions-vs-lambda-expressions).</span></span>

## <a name="more-expression-bodied-members"></a><span data-ttu-id="5df8f-238">Więcej składowych wyrażeń</span><span class="sxs-lookup"><span data-stu-id="5df8f-238">More expression-bodied members</span></span>

<span data-ttu-id="5df8f-239">W języku C# 6 wprowadzono składowe z wyrażeniami dla funkcji Członkowskich i właściwości tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="5df8f-239">C# 6 introduced expression-bodied members for member functions and read-only properties.</span></span> <span data-ttu-id="5df8f-240">C# 7,0 rozwija dozwolone elementy członkowskie, które mogą być zaimplementowane jako wyrażenia.</span><span class="sxs-lookup"><span data-stu-id="5df8f-240">C# 7.0 expands the allowed members that can be implemented as expressions.</span></span> <span data-ttu-id="5df8f-241">W języku C# 7,0 można zaimplementować *konstruktory*, *finalizatory* i metody `get` `set` dostępu do *Właściwości* i *indeksatorów*.</span><span class="sxs-lookup"><span data-stu-id="5df8f-241">In C# 7.0, you can implement *constructors*, *finalizers*, and `get` and `set` accessors on *properties* and *indexers*.</span></span> <span data-ttu-id="5df8f-242">Poniższy kod przedstawia przykłady każdego z nich:</span><span class="sxs-lookup"><span data-stu-id="5df8f-242">The following code shows examples of each:</span></span>

[!code-csharp[ExpressionBodiedMembers](~/samples/snippets/csharp/new-in-7/expressionmembers.cs#ExpressionBodiedEverything "new expression-bodied members")]

> [!NOTE]
> <span data-ttu-id="5df8f-243">Ten przykład nie wymaga finalizatora, ale jest pokazywany do zademonstrowania składni.</span><span class="sxs-lookup"><span data-stu-id="5df8f-243">This example does not need a finalizer, but it is shown to demonstrate the syntax.</span></span> <span data-ttu-id="5df8f-244">Nie należy implementować finalizatora w klasie, chyba że konieczne jest zwolnienie niezarządzanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="5df8f-244">You should not implement a finalizer in your class unless it is necessary to  release unmanaged resources.</span></span> <span data-ttu-id="5df8f-245">Należy również rozważyć użycie <xref:System.Runtime.InteropServices.SafeHandle> klasy zamiast bezpośrednio zarządzać niezarządzanymi zasobami.</span><span class="sxs-lookup"><span data-stu-id="5df8f-245">You should also consider using the <xref:System.Runtime.InteropServices.SafeHandle> class instead of managing unmanaged resources directly.</span></span>

<span data-ttu-id="5df8f-246">Te nowe lokalizacje dla elementów członkowskich zabudowanych w wyrażeniach reprezentują ważne punkty kontrolne języka C#: te funkcje zostały zaimplementowane przez członków społeczności pracujących w projekcie [Roslyn](https://github.com/dotnet/Roslyn) typu open source.</span><span class="sxs-lookup"><span data-stu-id="5df8f-246">These new locations for expression-bodied members represent an important milestone for the C# language: These features were implemented by community members working on the open-source [Roslyn](https://github.com/dotnet/Roslyn) project.</span></span>

<span data-ttu-id="5df8f-247">Zmiana metody na wyrażenie składowane składowej jest [zgodną z binarną zmianą](version-update-considerations.md#binary-compatible-changes).</span><span class="sxs-lookup"><span data-stu-id="5df8f-247">Changing a method to an expression bodied member is a [binary compatible change](version-update-considerations.md#binary-compatible-changes).</span></span>

## <a name="throw-expressions"></a><span data-ttu-id="5df8f-248">Wyrażenia throw</span><span class="sxs-lookup"><span data-stu-id="5df8f-248">Throw expressions</span></span>

<span data-ttu-id="5df8f-249">W języku C# `throw` zawsze była instrukcją.</span><span class="sxs-lookup"><span data-stu-id="5df8f-249">In C#, `throw` has always been a statement.</span></span> <span data-ttu-id="5df8f-250">Ponieważ `throw` jest instrukcją, a nie wyrażeniem, istnieją konstrukcje języka C#, w których nie można było ich użyć.</span><span class="sxs-lookup"><span data-stu-id="5df8f-250">Because `throw` is a statement, not an expression, there were C# constructs where you couldn't use it.</span></span> <span data-ttu-id="5df8f-251">Uwzględnione wyrażenia warunkowe, wyrażenia łączenia o wartości null i niektóre wyrażenia lambda.</span><span class="sxs-lookup"><span data-stu-id="5df8f-251">These included conditional expressions, null coalescing expressions, and some lambda expressions.</span></span> <span data-ttu-id="5df8f-252">Dodanie elementów członkowskich będących członkami wyrażeń dodaje więcej lokalizacji, w których `throw` wyrażenia byłyby przydatne.</span><span class="sxs-lookup"><span data-stu-id="5df8f-252">The addition of expression-bodied members adds more locations where `throw` expressions would be useful.</span></span> <span data-ttu-id="5df8f-253">Aby można było napisać dowolne z tych konstrukcji, w języku C# 7,0 wprowadzono [*wyrażenia throw*](../language-reference/keywords/throw.md#the-throw-expression).</span><span class="sxs-lookup"><span data-stu-id="5df8f-253">So that you can write any of these constructs, C# 7.0 introduces [*throw expressions*](../language-reference/keywords/throw.md#the-throw-expression).</span></span>

<span data-ttu-id="5df8f-254">To dodanie ułatwia zapisanie więcej kodu opartego na wyrażeniach.</span><span class="sxs-lookup"><span data-stu-id="5df8f-254">This addition makes it easier to write more expression-based code.</span></span> <span data-ttu-id="5df8f-255">Nie potrzebujesz dodatkowych instrukcji do sprawdzania błędów.</span><span class="sxs-lookup"><span data-stu-id="5df8f-255">You don't need additional statements for error checking.</span></span>

## <a name="default-literal-expressions"></a><span data-ttu-id="5df8f-256">Domyślne wyrażenia literału</span><span class="sxs-lookup"><span data-stu-id="5df8f-256">Default literal expressions</span></span>

<span data-ttu-id="5df8f-257">Domyślne wyrażenia literałów to ulepszenie wyrażeń wartości domyślnych.</span><span class="sxs-lookup"><span data-stu-id="5df8f-257">Default literal expressions are an enhancement to default value expressions.</span></span> <span data-ttu-id="5df8f-258">Te wyrażenia inicjują zmienną do wartości domyślnej.</span><span class="sxs-lookup"><span data-stu-id="5df8f-258">These expressions initialize a variable to the default value.</span></span> <span data-ttu-id="5df8f-259">Gdzie wcześniej warto napisać:</span><span class="sxs-lookup"><span data-stu-id="5df8f-259">Where you previously would write:</span></span>

```csharp
Func<string, bool> whereClause = default(Func<string, bool>);
```

<span data-ttu-id="5df8f-260">Możesz teraz pominąć typ po prawej stronie inicjalizacji:</span><span class="sxs-lookup"><span data-stu-id="5df8f-260">You can now omit the type on the right-hand side of the initialization:</span></span>

```csharp
Func<string, bool> whereClause = default;
```

<span data-ttu-id="5df8f-261">Aby uzyskać więcej informacji, zobacz sekcję [domyślny literał](../language-reference/operators/default.md#default-literal) w artykule [domyślny operator](../language-reference/operators/default.md) .</span><span class="sxs-lookup"><span data-stu-id="5df8f-261">For more information, see the [default literal](../language-reference/operators/default.md#default-literal) section of the [default operator](../language-reference/operators/default.md) article.</span></span>

## <a name="numeric-literal-syntax-improvements"></a><span data-ttu-id="5df8f-262">Udoskonalenia składni literału liczbowego</span><span class="sxs-lookup"><span data-stu-id="5df8f-262">Numeric literal syntax improvements</span></span>

<span data-ttu-id="5df8f-263">Nieodczytanie stałych numerycznych może utrudnić zrozumienie kodu podczas odczytywania go po raz pierwszy.</span><span class="sxs-lookup"><span data-stu-id="5df8f-263">Misreading numeric constants can make it harder to understand code when reading it for the first time.</span></span> <span data-ttu-id="5df8f-264">Maski bitowe lub inne wartości symboliczne są podatne na nieporozumienia.</span><span class="sxs-lookup"><span data-stu-id="5df8f-264">Bit masks or other symbolic values are prone to misunderstanding.</span></span> <span data-ttu-id="5df8f-265">Język C# 7,0 zawiera dwie nowe funkcje do zapisu liczb w najbardziej czytelny sposób dla zamierzonego użycia: *literały binarne* oraz *separatory cyfr*.</span><span class="sxs-lookup"><span data-stu-id="5df8f-265">C# 7.0 includes two new features to write numbers in the most readable fashion for the intended use: *binary literals*, and *digit separators*.</span></span>

<span data-ttu-id="5df8f-266">Dla tych czasów podczas tworzenia masek bitowych lub za każdym razem, gdy binarna reprezentacja liczby sprawia, że jest to najbardziej czytelny kod, Zapisz ten numer w postaci binarnej:</span><span class="sxs-lookup"><span data-stu-id="5df8f-266">For those times when you're creating bit masks, or whenever a binary representation of a number makes the most readable code, write that number in binary:</span></span>

[!code-csharp[ThousandSeparators](~/samples/snippets/csharp/new-in-7/Program.cs#ThousandSeparators "Thousands separators")]

<span data-ttu-id="5df8f-267">`0b`Na początku stała wskazuje, że liczba jest zapisywana jako liczba binarna.</span><span class="sxs-lookup"><span data-stu-id="5df8f-267">The `0b` at the beginning of the constant indicates that the number is written as a binary number.</span></span> <span data-ttu-id="5df8f-268">Liczby binarne mogą być długie, więc często łatwiej jest zobaczyć wzorce bitowe, wprowadzając `_` jako separator cyfr, jak pokazano w powyższym przykładzie w postaci binarnej.</span><span class="sxs-lookup"><span data-stu-id="5df8f-268">Binary numbers can get long, so it's often easier to see the bit patterns by introducing the `_` as a digit separator, as shown in the binary constant in the preceding example.</span></span> <span data-ttu-id="5df8f-269">Separator cyfr może pojawić się w dowolnym miejscu w stałej.</span><span class="sxs-lookup"><span data-stu-id="5df8f-269">The digit separator can appear anywhere in the constant.</span></span> <span data-ttu-id="5df8f-270">W przypadku numerów podstawowych 10 często należy używać jej jako separatora tysięcy.</span><span class="sxs-lookup"><span data-stu-id="5df8f-270">For base 10 numbers, it is common to use it as a thousands separator.</span></span> <span data-ttu-id="5df8f-271">Szesnastkowe i binarne literały numeryczne mogą zaczynać się od `_` :</span><span class="sxs-lookup"><span data-stu-id="5df8f-271">Hex and binary numeric literals may begin with an `_`:</span></span>

[!code-csharp[LargeIntegers](~/samples/snippets/csharp/new-in-7/Program.cs#LargeIntegers "Large integer")]

<span data-ttu-id="5df8f-272">Separator cyfr może być używany z `decimal` , `float` i `double` również typy:</span><span class="sxs-lookup"><span data-stu-id="5df8f-272">The digit separator can be used with `decimal`, `float`, and `double` types as well:</span></span>

[!code-csharp[OtherConstants](~/samples/snippets/csharp/new-in-7/Program.cs#OtherConstants "non-integral constants")]

<span data-ttu-id="5df8f-273">Ze sobą można zadeklarować stałe liczbowe o znacznie większej czytelności.</span><span class="sxs-lookup"><span data-stu-id="5df8f-273">Taken together, you can declare numeric constants with much more readability.</span></span>

## <a name="out-variables"></a><span data-ttu-id="5df8f-274">`out` modyfikacj</span><span class="sxs-lookup"><span data-stu-id="5df8f-274">`out` variables</span></span>

<span data-ttu-id="5df8f-275">Istniejąca składnia, która obsługuje parametry, została `out` ulepszona w języku C# 7.</span><span class="sxs-lookup"><span data-stu-id="5df8f-275">The existing syntax that supports `out` parameters has been improved in C# 7.</span></span> <span data-ttu-id="5df8f-276">Można teraz zadeklarować `out` zmienne na liście argumentów wywołania metody, zamiast pisać oddzielne oświadczenie deklaracji:</span><span class="sxs-lookup"><span data-stu-id="5df8f-276">You can now declare `out` variables in the argument list of a method call, rather than writing a separate declaration statement:</span></span>

[!code-csharp[OutVariableDeclarations](~/samples/snippets/csharp/new-in-7/program.cs#OutVariableDeclarations "Out variable declarations")]

<span data-ttu-id="5df8f-277">Możesz chcieć określić typ `out` zmiennej dla przejrzystości, jak pokazano w poprzednim przykładzie.</span><span class="sxs-lookup"><span data-stu-id="5df8f-277">You may want to specify the type of the `out` variable for clarity, as shown in the preceding example.</span></span> <span data-ttu-id="5df8f-278">Język obsługuje jednak użycie niejawnie wpisanej zmiennej lokalnej:</span><span class="sxs-lookup"><span data-stu-id="5df8f-278">However, the language does support using an implicitly typed local variable:</span></span>

[!code-csharp[OutVarVariableDeclarations](~/samples/snippets/csharp/new-in-7/program.cs#OutVarVariableDeclarations "Implicitly typed Out variable")]

- <span data-ttu-id="5df8f-279">Kod jest łatwiejszy do odczytania.</span><span class="sxs-lookup"><span data-stu-id="5df8f-279">The code is easier to read.</span></span>
  - <span data-ttu-id="5df8f-280">Można zadeklarować zmienną out tam, gdzie jest używana, a nie w poprzednim wierszu kodu.</span><span class="sxs-lookup"><span data-stu-id="5df8f-280">You declare the out variable where you use it, not on a preceding line of code.</span></span>
- <span data-ttu-id="5df8f-281">Nie trzeba przypisywać wartości początkowej.</span><span class="sxs-lookup"><span data-stu-id="5df8f-281">No need to assign an initial value.</span></span>
  - <span data-ttu-id="5df8f-282">Deklarując `out` zmienną, w której jest używana w wywołaniu metody, nie można go przypadkowo użyć przed przypisaniem.</span><span class="sxs-lookup"><span data-stu-id="5df8f-282">By declaring the `out` variable where it's used in a method call, you can't accidentally use it before it is assigned.</span></span>

<span data-ttu-id="5df8f-283">Składnia dodana w języku C# 7,0 do zezwalania na `out` deklaracje zmiennych w celu uwzględnienia inicjatorów pól, inicjatorów właściwości, inicjatorów konstruktora i klauzul zapytania.</span><span class="sxs-lookup"><span data-stu-id="5df8f-283">The syntax added in C# 7.0 to allow `out` variable declarations has been extended to include field initializers, property initializers, constructor initializers, and query clauses.</span></span> <span data-ttu-id="5df8f-284">Umożliwia to wykonywanie kodu, takiego jak Poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="5df8f-284">It enables code such as the following example:</span></span>

```csharp
public class B
{
   public B(int i, out int j)
   {
      j = i;
   }
}

public class D : B
{
   public D(int i) : base(i, out var j)
   {
      Console.WriteLine($"The value of 'j' is {j}");
   }
}
```

## <a name="non-trailing-named-arguments"></a><span data-ttu-id="5df8f-285">Argumenty nazwane inne niż końcowe</span><span class="sxs-lookup"><span data-stu-id="5df8f-285">Non-trailing named arguments</span></span>

<span data-ttu-id="5df8f-286">Wywołania metod mogą teraz używać nazwanych argumentów, które poprzedzają argumenty pozycyjne, gdy te nazwane argumenty znajdują się w poprawnych pozycjach.</span><span class="sxs-lookup"><span data-stu-id="5df8f-286">Method calls may now use named arguments that precede positional arguments when those named arguments are in the correct positions.</span></span> <span data-ttu-id="5df8f-287">Aby uzyskać więcej informacji, zobacz [argumenty nazwane i opcjonalne](../programming-guide/classes-and-structs/named-and-optional-arguments.md).</span><span class="sxs-lookup"><span data-stu-id="5df8f-287">For more information, see [Named and optional arguments](../programming-guide/classes-and-structs/named-and-optional-arguments.md).</span></span>

## <a name="private-protected-access-modifier"></a><span data-ttu-id="5df8f-288">modyfikator *prywatnego dostępu chronionego*</span><span class="sxs-lookup"><span data-stu-id="5df8f-288">*private protected* access modifier</span></span>

<span data-ttu-id="5df8f-289">Nowy modyfikator dostępu złożonego: `private protected` wskazuje, że element członkowski może być dostępny przez zawiera klasy lub klasy pochodne, które są zadeklarowane w tym samym zestawie.</span><span class="sxs-lookup"><span data-stu-id="5df8f-289">A new compound access modifier: `private protected` indicates that a member may be accessed by containing class or derived classes that are declared in the same assembly.</span></span> <span data-ttu-id="5df8f-290">`protected internal`Zezwala na dostęp przez klasy pochodne lub klasy, które znajdują się w tym samym zestawie, `private protected` ogranicza dostęp do typów pochodnych zadeklarowanych w tym samym zestawie.</span><span class="sxs-lookup"><span data-stu-id="5df8f-290">While `protected internal` allows access by derived classes or classes that are in the same assembly, `private protected` limits access to derived types declared in the same assembly.</span></span>

<span data-ttu-id="5df8f-291">Aby uzyskać więcej informacji, zobacz [Modyfikatory dostępu](../language-reference/keywords/access-modifiers.md) w dokumentacji języka.</span><span class="sxs-lookup"><span data-stu-id="5df8f-291">For more information, see [access modifiers](../language-reference/keywords/access-modifiers.md) in the language reference.</span></span>

## <a name="improved-overload-candidates"></a><span data-ttu-id="5df8f-292">Ulepszone kandydujące metody rozwiązywania przeciążenia</span><span class="sxs-lookup"><span data-stu-id="5df8f-292">Improved overload candidates</span></span>

<span data-ttu-id="5df8f-293">W każdej wersji reguły rozpoznawania przeciążenia zostały zaktualizowane w celu rozwiązania sytuacji, w których niejednoznaczne wywołania metod mają oczywisty wybór.</span><span class="sxs-lookup"><span data-stu-id="5df8f-293">In every release, the overload resolution rules get updated to address situations where ambiguous method invocations have an "obvious" choice.</span></span> <span data-ttu-id="5df8f-294">W tej wersji dodano trzy nowe reguły, które ułatwiają wybór oczywisty przez kompilator:</span><span class="sxs-lookup"><span data-stu-id="5df8f-294">This release adds three new rules to help the compiler pick the obvious choice:</span></span>

1. <span data-ttu-id="5df8f-295">Gdy grupa metod zawiera zarówno wystąpienie, jak i statyczne elementy członkowskie, kompilator odrzuca elementy członkowskie wystąpienia, jeśli metoda została wywołana bez odbiorcy wystąpienia lub kontekstu.</span><span class="sxs-lookup"><span data-stu-id="5df8f-295">When a method group contains both instance and static members, the compiler discards the instance members if the method was invoked without an instance receiver or context.</span></span> <span data-ttu-id="5df8f-296">Kompilator odrzuca statyczne elementy członkowskie, jeśli metoda została wywołana z odbiornikiem wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="5df8f-296">The compiler discards the static members if the method was invoked with an instance receiver.</span></span> <span data-ttu-id="5df8f-297">Gdy nie ma odbiornika, kompilator zawiera tylko statyczne elementy członkowskie w kontekście statycznym, w przeciwnym razie elementy członkowskie statyczne i wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="5df8f-297">When there is no receiver, the compiler includes only static members in a static context, otherwise both static and instance members.</span></span> <span data-ttu-id="5df8f-298">Gdy odbiorca jest niejednoznacznie wystąpieniem lub typem, kompilator zawiera oba te elementy.</span><span class="sxs-lookup"><span data-stu-id="5df8f-298">When the receiver is ambiguously an instance or type, the compiler includes both.</span></span> <span data-ttu-id="5df8f-299">Statyczny kontekst, w którym niejawny `this` odbiornik wystąpienia nie może być używany, zawiera treść elementów członkowskich, gdzie nie `this` jest zdefiniowana, takich jak statyczne elementy członkowskie, a także miejsca, w których `this` nie można ich używać, takich jak inicjatory pól i konstruktory.</span><span class="sxs-lookup"><span data-stu-id="5df8f-299">A static context, where an implicit `this` instance receiver cannot be used, includes the body of members where no `this` is defined, such as static members, as well as places where `this` cannot be used, such as field initializers and constructor-initializers.</span></span>
1. <span data-ttu-id="5df8f-300">Gdy grupa metod zawiera kilka metod ogólnych, których argumenty typu nie spełniają ograniczeń, te elementy członkowskie są usuwane z zestawu kandydatów.</span><span class="sxs-lookup"><span data-stu-id="5df8f-300">When a method group contains some generic methods whose type arguments do not satisfy their constraints, these members are removed from the candidate set.</span></span>
1. <span data-ttu-id="5df8f-301">Dla konwersji grup metod, metody kandydujące, których typ zwracany nie jest zgodny z typem zwracanym delegata, są usuwane z zestawu.</span><span class="sxs-lookup"><span data-stu-id="5df8f-301">For a method group conversion, candidate methods whose return type doesn't match up with the delegate's return type are removed from the set.</span></span>

<span data-ttu-id="5df8f-302">Ta zmiana zostanie wykorzystana tylko dlatego, że w przypadku niejednoznacznych przeciążeń metod znajdziesz mniej błędów kompilatora, gdy masz pewność, która metoda jest lepsza.</span><span class="sxs-lookup"><span data-stu-id="5df8f-302">You'll only notice this change because you'll find fewer compiler errors for ambiguous method overloads when you are sure which method is better.</span></span>

## <a name="enabling-more-efficient-safe-code"></a><span data-ttu-id="5df8f-303">Włączanie bardziej wydajnego bezpiecznego kodu</span><span class="sxs-lookup"><span data-stu-id="5df8f-303">Enabling more efficient safe code</span></span>

<span data-ttu-id="5df8f-304">Należy mieć możliwość bezpiecznego pisania kodu w języku C#, który wykonuje, a także kod niebezpieczny.</span><span class="sxs-lookup"><span data-stu-id="5df8f-304">You should be able to write C# code safely that performs as well as unsafe code.</span></span> <span data-ttu-id="5df8f-305">Bezpieczny kod unika klas błędów, takich jak przekroczenia buforu, nieużywane wskaźniki i inne błędy dostępu do pamięci.</span><span class="sxs-lookup"><span data-stu-id="5df8f-305">Safe code avoids classes of errors, such as buffer overruns, stray pointers, and other memory access errors.</span></span> <span data-ttu-id="5df8f-306">Te nowe funkcje rozszerzają możliwości zweryfikowania bezpiecznego kodu.</span><span class="sxs-lookup"><span data-stu-id="5df8f-306">These new features expand the capabilities of verifiable safe code.</span></span> <span data-ttu-id="5df8f-307">Staraj się pisać więcej kodu przy użyciu bezpiecznych konstrukcji.</span><span class="sxs-lookup"><span data-stu-id="5df8f-307">Strive to write more of your code using safe constructs.</span></span> <span data-ttu-id="5df8f-308">Te funkcje ułatwiają to.</span><span class="sxs-lookup"><span data-stu-id="5df8f-308">These features make that easier.</span></span>

<span data-ttu-id="5df8f-309">Poniższe nowe funkcje obsługują motyw lepszej wydajności dla bezpiecznego kodu:</span><span class="sxs-lookup"><span data-stu-id="5df8f-309">The following new features support the theme of better performance for safe code:</span></span>

- <span data-ttu-id="5df8f-310">Można uzyskać dostęp do stałych pól bez przypinania.</span><span class="sxs-lookup"><span data-stu-id="5df8f-310">You can access fixed fields without pinning.</span></span>
- <span data-ttu-id="5df8f-311">Zmienne lokalne można przypisywać ponownie `ref` .</span><span class="sxs-lookup"><span data-stu-id="5df8f-311">You can reassign `ref` local variables.</span></span>
- <span data-ttu-id="5df8f-312">Inicjatorów można używać w `stackalloc` tablicach.</span><span class="sxs-lookup"><span data-stu-id="5df8f-312">You can use initializers on `stackalloc` arrays.</span></span>
- <span data-ttu-id="5df8f-313">Można używać `fixed` instrukcji z dowolnym typem, który obsługuje wzorzec.</span><span class="sxs-lookup"><span data-stu-id="5df8f-313">You can use `fixed` statements with any type that supports a pattern.</span></span>
- <span data-ttu-id="5df8f-314">Można użyć dodatkowych ograniczeń ogólnych.</span><span class="sxs-lookup"><span data-stu-id="5df8f-314">You can use additional generic constraints.</span></span>
- <span data-ttu-id="5df8f-315">`in`Modyfikator parametrów, aby określić, że argument jest przesyłany przez odwołanie, ale nie modyfikowane przez wywołaną metodę.</span><span class="sxs-lookup"><span data-stu-id="5df8f-315">The `in` modifier on parameters, to specify that an argument is passed by reference but not modified by the called method.</span></span> <span data-ttu-id="5df8f-316">Dodanie `in` modyfikatora do argumentu jest [zgodną zmianą źródłową](version-update-considerations.md#source-compatible-changes).</span><span class="sxs-lookup"><span data-stu-id="5df8f-316">Adding the `in` modifier to an argument is a [source compatible change](version-update-considerations.md#source-compatible-changes).</span></span>
- <span data-ttu-id="5df8f-317">`ref readonly`Modyfikator metody zwraca, aby wskazać, że metoda zwraca swoją wartość przez odwołanie, ale nie zezwala na zapis w tym obiekcie.</span><span class="sxs-lookup"><span data-stu-id="5df8f-317">The `ref readonly` modifier on method returns, to indicate that a method returns its value by reference but doesn't allow writes to that object.</span></span> <span data-ttu-id="5df8f-318">Dodanie `ref readonly` modyfikatora jest [zgodną ze źródłem zmian](version-update-considerations.md#source-compatible-changes), jeśli powrót jest przypisany do wartości.</span><span class="sxs-lookup"><span data-stu-id="5df8f-318">Adding the `ref readonly` modifier is a [source compatible change](version-update-considerations.md#source-compatible-changes), if the return is assigned to a value.</span></span> <span data-ttu-id="5df8f-319">Dodanie `readonly` modyfikatora do istniejącej `ref` instrukcji return jest [niezgodną zmianą](version-update-considerations.md#incompatible-changes).</span><span class="sxs-lookup"><span data-stu-id="5df8f-319">Adding the `readonly` modifier to an existing `ref` return statement is an [incompatible change](version-update-considerations.md#incompatible-changes).</span></span> <span data-ttu-id="5df8f-320">Wymaga, aby wywołujący zaktualizował deklarację `ref` zmiennych lokalnych w celu uwzględnienia `readonly` modyfikatora.</span><span class="sxs-lookup"><span data-stu-id="5df8f-320">It requires callers to update the declaration of `ref` local variables to include the `readonly` modifier.</span></span>
- <span data-ttu-id="5df8f-321">`readonly struct`Deklaracja wskazująca, że struktura jest niezmienna i powinna zostać przeniesiona jako `in` parametr do metod składowych.</span><span class="sxs-lookup"><span data-stu-id="5df8f-321">The `readonly struct` declaration, to indicate that a struct is immutable and should be passed as an `in` parameter to its member methods.</span></span> <span data-ttu-id="5df8f-322">Dodanie `readonly` modyfikatora do istniejącej deklaracji struktury jest [zgodną binarną zmianą](version-update-considerations.md#binary-compatible-changes).</span><span class="sxs-lookup"><span data-stu-id="5df8f-322">Adding the `readonly` modifier to an existing struct declaration is a [binary compatible change](version-update-considerations.md#binary-compatible-changes).</span></span>
- <span data-ttu-id="5df8f-323">`ref struct`Deklaracja wskazująca, że typ struktury bezpośrednio uzyskuje dostęp do pamięci zarządzanej i zawsze musi mieć przydzieloną stos.</span><span class="sxs-lookup"><span data-stu-id="5df8f-323">The `ref struct` declaration, to indicate that a struct type accesses managed memory directly and must always be stack allocated.</span></span> <span data-ttu-id="5df8f-324">Dodanie `ref` modyfikatora do istniejącej `struct` deklaracji jest [niezgodną zmianą](version-update-considerations.md#incompatible-changes).</span><span class="sxs-lookup"><span data-stu-id="5df8f-324">Adding the `ref` modifier to an existing `struct` declaration is an [incompatible change](version-update-considerations.md#incompatible-changes).</span></span> <span data-ttu-id="5df8f-325">Element a `ref struct` nie może być składową klasy ani używać w innych lokalizacjach, w których może być przydzielony na stercie.</span><span class="sxs-lookup"><span data-stu-id="5df8f-325">A `ref struct` cannot be a member of a class or used in other locations where it may be allocated on the heap.</span></span>

<span data-ttu-id="5df8f-326">Więcej informacji na temat tych zmian można znaleźć w artykule [pisanie bezpiecznego wydajnego kodu](../write-safe-efficient-code.md).</span><span class="sxs-lookup"><span data-stu-id="5df8f-326">You can read more about all these changes in [Write safe efficient code](../write-safe-efficient-code.md).</span></span>

### <a name="ref-locals-and-returns"></a><span data-ttu-id="5df8f-327">Ref locales i Returns</span><span class="sxs-lookup"><span data-stu-id="5df8f-327">Ref locals and returns</span></span>

<span data-ttu-id="5df8f-328">Ta funkcja włącza algorytmy, które używają i zwracają odwołania do zmiennych zdefiniowanych w innym miejscu.</span><span class="sxs-lookup"><span data-stu-id="5df8f-328">This feature enables algorithms that use and return references to variables defined elsewhere.</span></span> <span data-ttu-id="5df8f-329">Jeden przykład pracuje z dużymi macierzami i odnajduje jedną lokalizację z określonymi cechami.</span><span class="sxs-lookup"><span data-stu-id="5df8f-329">One example is working with large matrices, and finding a single location with certain characteristics.</span></span> <span data-ttu-id="5df8f-330">Poniższa metoda zwraca **odwołanie** do tego magazynu w macierzy:</span><span class="sxs-lookup"><span data-stu-id="5df8f-330">The following method returns a **reference** to that storage in the matrix:</span></span>

[!code-csharp[FindReturningRef](~/samples/snippets/csharp/new-in-7/MatrixSearch.cs#FindReturningRef "Find returning by reference")]

<span data-ttu-id="5df8f-331">Można zadeklarować wartość zwracaną jako `ref` i zmodyfikować tę wartość w macierzy, jak pokazano w poniższym kodzie:</span><span class="sxs-lookup"><span data-stu-id="5df8f-331">You can declare the return value as a `ref` and modify that value in the matrix, as shown in the following code:</span></span>

[!code-csharp[AssignRefReturn](~/samples/snippets/csharp/new-in-7/Program.cs#AssignRefReturn "Assign ref return")]

<span data-ttu-id="5df8f-332">Język C# ma kilka reguł, które chronią przed niepożądanym użyciem `ref` zmiennych lokalnych i zwraca:</span><span class="sxs-lookup"><span data-stu-id="5df8f-332">The C# language has several rules that protect you from misusing the `ref` locals and returns:</span></span>

- <span data-ttu-id="5df8f-333">Należy dodać `ref` słowo kluczowe do sygnatury metody i do wszystkich `return` instrukcji w metodzie.</span><span class="sxs-lookup"><span data-stu-id="5df8f-333">You must add the `ref` keyword to the method signature and to all `return` statements in a method.</span></span>
  - <span data-ttu-id="5df8f-334">Dzięki temu czyszczenie metody następuje przez odwołanie w całej metodzie.</span><span class="sxs-lookup"><span data-stu-id="5df8f-334">That makes it clear the method returns by reference throughout the method.</span></span>
- <span data-ttu-id="5df8f-335">A `ref return` może być przypisana do zmiennej wartości lub `ref` zmiennej.</span><span class="sxs-lookup"><span data-stu-id="5df8f-335">A `ref return` may be assigned to a value variable, or a `ref` variable.</span></span>
  - <span data-ttu-id="5df8f-336">Obiekt wywołujący kontroluje, czy wartość zwracana jest kopiowana, czy nie.</span><span class="sxs-lookup"><span data-stu-id="5df8f-336">The caller controls whether the return value is copied or not.</span></span> <span data-ttu-id="5df8f-337">Pominięcie `ref` modyfikatora podczas przypisywania wartości zwracanej wskazuje, że obiekt wywołujący chce mieć kopię wartości, a nie odwołanie do magazynu.</span><span class="sxs-lookup"><span data-stu-id="5df8f-337">Omitting the `ref` modifier when assigning the return value indicates that the caller wants a copy of the value, not a reference to the storage.</span></span>
- <span data-ttu-id="5df8f-338">Nie można przypisać wartości zwracanej metody standardowej do `ref` zmiennej lokalnej.</span><span class="sxs-lookup"><span data-stu-id="5df8f-338">You can't assign a standard method return value to a `ref` local variable.</span></span>
  - <span data-ttu-id="5df8f-339">Nie zezwala na instrukcje, takie jak `ref int i = sequence.Count();`</span><span class="sxs-lookup"><span data-stu-id="5df8f-339">That disallows statements like `ref int i = sequence.Count();`</span></span>
- <span data-ttu-id="5df8f-340">Nie można zwrócić `ref` do zmiennej, której okres istnienia nie przekracza wykonywania metody.</span><span class="sxs-lookup"><span data-stu-id="5df8f-340">You can't return a `ref` to a variable whose lifetime doesn't extend beyond the execution of the method.</span></span>
  - <span data-ttu-id="5df8f-341">Oznacza to, że nie można zwrócić odwołania do zmiennej lokalnej lub zmiennej o podobnym zakresie.</span><span class="sxs-lookup"><span data-stu-id="5df8f-341">That means you can't return a reference to a local variable or a variable with a similar scope.</span></span>
- <span data-ttu-id="5df8f-342">`ref` elementy locale i Returns nie mogą być używane z metodami asynchronicznymi.</span><span class="sxs-lookup"><span data-stu-id="5df8f-342">`ref` locals and returns can't be used with async methods.</span></span>
  - <span data-ttu-id="5df8f-343">Kompilator nie może wiedzieć, czy przywoływana zmienna została ustawiona na jej końcową wartość, gdy Metoda asynchroniczna zwraca.</span><span class="sxs-lookup"><span data-stu-id="5df8f-343">The compiler can't know if the referenced variable has been set to its final value when the async method returns.</span></span>

<span data-ttu-id="5df8f-344">Dodanie elementów lokalnych ref i Return ref umożliwia stosowanie algorytmów, które są bardziej wydajne przez uniknięcie kopiowania wartości lub wielokrotne wykonywanie operacji usuwania odwołań.</span><span class="sxs-lookup"><span data-stu-id="5df8f-344">The addition of ref locals and ref returns enables algorithms that are more efficient by avoiding copying values, or performing dereferencing operations multiple times.</span></span>

<span data-ttu-id="5df8f-345">Dodanie `ref` do wartości zwracanej jest [zmianą zgodną ze źródłem](version-update-considerations.md#source-compatible-changes).</span><span class="sxs-lookup"><span data-stu-id="5df8f-345">Adding `ref` to the return value is a [source compatible change](version-update-considerations.md#source-compatible-changes).</span></span> <span data-ttu-id="5df8f-346">Istniejący kod kompiluje, ale zwracana wartość Ref jest kopiowana po przypisaniu.</span><span class="sxs-lookup"><span data-stu-id="5df8f-346">Existing code compiles, but the ref return value is copied when assigned.</span></span> <span data-ttu-id="5df8f-347">Obiekty wywołujące muszą zaktualizować magazyn dla wartości zwracanej do `ref` zmiennej lokalnej, aby można było przechowywać zwrot jako odwołanie.</span><span class="sxs-lookup"><span data-stu-id="5df8f-347">Callers must update the storage for the return value to a `ref` local variable to store the return as a reference.</span></span>

<span data-ttu-id="5df8f-348">Teraz elementy `ref` lokalne mogą zostać ponownie przypisane, aby odwoływać się do różnych wystąpień po zainicjowaniu.</span><span class="sxs-lookup"><span data-stu-id="5df8f-348">Now, `ref` locals may be reassigned to refer to different instances after being initialized.</span></span> <span data-ttu-id="5df8f-349">Poniższy kod jest teraz kompilowany:</span><span class="sxs-lookup"><span data-stu-id="5df8f-349">The following code now compiles:</span></span>

```csharp
ref VeryLargeStruct refLocal = ref veryLargeStruct; // initialization
refLocal = ref anotherVeryLargeStruct; // reassigned, refLocal refers to different storage.
```

<span data-ttu-id="5df8f-350">Aby uzyskać więcej informacji, zobacz artykuł dotyczący [ `ref` zwrotów i elementów `ref` lokalnych](../programming-guide/classes-and-structs/ref-returns.md)oraz artykuł w artykule [`foreach`](../language-reference/keywords/foreach-in.md) .</span><span class="sxs-lookup"><span data-stu-id="5df8f-350">For more information, see the article on [`ref` returns and `ref` locals](../programming-guide/classes-and-structs/ref-returns.md), and the article on [`foreach`](../language-reference/keywords/foreach-in.md).</span></span>

<span data-ttu-id="5df8f-351">Aby uzyskać więcej informacji, zobacz artykuł [słowo kluczowe ref](../language-reference/keywords/ref.md) .</span><span class="sxs-lookup"><span data-stu-id="5df8f-351">For more information, see the [ref keyword](../language-reference/keywords/ref.md) article.</span></span>

### <a name="conditional-ref-expressions"></a><span data-ttu-id="5df8f-352">Wyrażenia warunkowe `ref`</span><span class="sxs-lookup"><span data-stu-id="5df8f-352">Conditional `ref` expressions</span></span>

<span data-ttu-id="5df8f-353">Na koniec wyrażenie warunkowe może generować wynik ref zamiast wyniku wartości.</span><span class="sxs-lookup"><span data-stu-id="5df8f-353">Finally, the conditional expression may produce a ref result instead of a value result.</span></span> <span data-ttu-id="5df8f-354">Na przykład Napisz następujące polecenie, aby pobrać odwołanie do pierwszego elementu w jednej z dwóch tablic:</span><span class="sxs-lookup"><span data-stu-id="5df8f-354">For example, you would write the following to retrieve a reference to the first element in one of two arrays:</span></span>

```csharp
ref var r = ref (arr != null ? ref arr[0] : ref otherArr[0]);
```

<span data-ttu-id="5df8f-355">Zmienna `r` jest odwołaniem do pierwszej wartości z `arr` lub `otherArr` .</span><span class="sxs-lookup"><span data-stu-id="5df8f-355">The variable `r` is a reference to the first value in either `arr` or `otherArr`.</span></span>

<span data-ttu-id="5df8f-356">Aby uzyskać więcej informacji, zobacz [operator warunkowy (?:)](../language-reference/operators/conditional-operator.md) w dokumentacji języka.</span><span class="sxs-lookup"><span data-stu-id="5df8f-356">For more information, see [conditional operator (?:)](../language-reference/operators/conditional-operator.md) in the language reference.</span></span>

### <a name="in-parameter-modifier"></a><span data-ttu-id="5df8f-357">`in` modyfikator parametru</span><span class="sxs-lookup"><span data-stu-id="5df8f-357">`in` parameter modifier</span></span>

<span data-ttu-id="5df8f-358">`in`Słowo kluczowe uzupełnia istniejące słowa kluczowe ref i out do przekazywania argumentów przez odwołanie.</span><span class="sxs-lookup"><span data-stu-id="5df8f-358">The `in` keyword complements the existing ref and out keywords to pass arguments by reference.</span></span> <span data-ttu-id="5df8f-359">`in`Słowo kluczowe Określa przekazywanie argumentu przez odwołanie, ale wywołana metoda nie modyfikuje wartości.</span><span class="sxs-lookup"><span data-stu-id="5df8f-359">The `in` keyword specifies passing the argument by reference, but the called method doesn't modify the value.</span></span>

<span data-ttu-id="5df8f-360">Można zadeklarować przeciążenia, które przechodzą przez wartość lub przez odwołanie tylko do odczytu, jak pokazano w poniższym kodzie:</span><span class="sxs-lookup"><span data-stu-id="5df8f-360">You may declare overloads that pass by value or by readonly reference, as shown in the following code:</span></span>

```csharp
static void M(S arg);
static void M(in S arg);
```

<span data-ttu-id="5df8f-361">Wartość przez (najpierw w poprzednim przykładzie) przeciążenie jest lepsza niż wersja odwołania do tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="5df8f-361">The by value (first in the preceding example) overload is better than the by readonly reference version.</span></span> <span data-ttu-id="5df8f-362">Aby wywołać wersję z argumentem odwołania tylko do odczytu, należy dołączyć `in` modyfikator podczas wywoływania metody.</span><span class="sxs-lookup"><span data-stu-id="5df8f-362">To call the version with the readonly reference argument, you must include the `in` modifier when calling the method.</span></span>

<span data-ttu-id="5df8f-363">Aby uzyskać więcej informacji, zobacz artykuł dotyczący [ `in` modyfikatora parametru](../language-reference/keywords/in-parameter-modifier.md).</span><span class="sxs-lookup"><span data-stu-id="5df8f-363">For more information, see the article on the [`in` parameter modifier](../language-reference/keywords/in-parameter-modifier.md).</span></span>

### <a name="more-types-support-the-fixed-statement"></a><span data-ttu-id="5df8f-364">Więcej typów obsługuje `fixed` instrukcja</span><span class="sxs-lookup"><span data-stu-id="5df8f-364">More types support the `fixed` statement</span></span>

<span data-ttu-id="5df8f-365">`fixed`Instrukcja obsługuje ograniczony zestaw typów.</span><span class="sxs-lookup"><span data-stu-id="5df8f-365">The `fixed` statement supported a limited set of types.</span></span> <span data-ttu-id="5df8f-366">Począwszy od języka C# 7,3, dowolnego typu, który zawiera `GetPinnableReference()` metodę zwracającą `ref T` lub `ref readonly T` może być `fixed` .</span><span class="sxs-lookup"><span data-stu-id="5df8f-366">Starting with C# 7.3, any type that contains a `GetPinnableReference()` method that returns a `ref T` or `ref readonly T` may be `fixed`.</span></span> <span data-ttu-id="5df8f-367">Dodanie tej funkcji oznacza, że `fixed` mogą być używane z <xref:System.Span%601?displayProperty=nameWithType> i powiązane typy.</span><span class="sxs-lookup"><span data-stu-id="5df8f-367">Adding this feature means that `fixed` can be used with <xref:System.Span%601?displayProperty=nameWithType> and related types.</span></span>

<span data-ttu-id="5df8f-368">Aby uzyskać więcej informacji, zobacz artykuł [ `fixed` instrukcji](../language-reference/keywords/fixed-statement.md) w dokumentacji języka.</span><span class="sxs-lookup"><span data-stu-id="5df8f-368">For more information, see the [`fixed` statement](../language-reference/keywords/fixed-statement.md) article in the language reference.</span></span>

### <a name="indexing-fixed-fields-does-not-require-pinning"></a><span data-ttu-id="5df8f-369">Pola indeksowania nie `fixed` wymagają przypinania</span><span class="sxs-lookup"><span data-stu-id="5df8f-369">Indexing `fixed` fields does not require pinning</span></span>

<span data-ttu-id="5df8f-370">Rozważmy tę strukturę:</span><span class="sxs-lookup"><span data-stu-id="5df8f-370">Consider this struct:</span></span>

```csharp
unsafe struct S
{
    public fixed int myFixedField[10];
}
```

<span data-ttu-id="5df8f-371">We wcześniejszych wersjach języka C# wymagało przypinania zmiennej w celu uzyskania dostępu do jednej z liczb całkowitych, które są częścią `myFixedField` .</span><span class="sxs-lookup"><span data-stu-id="5df8f-371">In earlier versions of C#, you needed to pin a variable to access one of the integers that are part of `myFixedField`.</span></span> <span data-ttu-id="5df8f-372">Teraz Poniższy kod kompiluje bez przypinania zmiennej `p` wewnątrz oddzielnej `fixed` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="5df8f-372">Now, the following code compiles without pinning the variable `p` inside a separate `fixed` statement:</span></span>

```csharp
class C
{
    static S s = new S();

    unsafe public void M()
    {
        int p = s.myFixedField[5];
    }
}
```

<span data-ttu-id="5df8f-373">Zmienna `p` uzyskuje dostęp do jednego elementu w `myFixedField` .</span><span class="sxs-lookup"><span data-stu-id="5df8f-373">The variable `p` accesses one element in `myFixedField`.</span></span> <span data-ttu-id="5df8f-374">Nie musisz deklarować odrębnej `int*` zmiennej.</span><span class="sxs-lookup"><span data-stu-id="5df8f-374">You don't need to declare a separate `int*` variable.</span></span> <span data-ttu-id="5df8f-375">Nadal potrzebujesz `unsafe` kontekstu.</span><span class="sxs-lookup"><span data-stu-id="5df8f-375">You still need an `unsafe` context.</span></span> <span data-ttu-id="5df8f-376">We wcześniejszych wersjach języka C# należy zadeklarować drugi stały wskaźnik:</span><span class="sxs-lookup"><span data-stu-id="5df8f-376">In earlier versions of C#, you need to declare a second fixed pointer:</span></span>

```csharp
class C
{
    static S s = new S();

    unsafe public void M()
    {
        fixed (int* ptr = s.myFixedField)
        {
            int p = ptr[5];
        }
    }
}
```

<span data-ttu-id="5df8f-377">Aby uzyskać więcej informacji, zobacz artykuł na temat [ `fixed` instrukcji](../language-reference/keywords/fixed-statement.md).</span><span class="sxs-lookup"><span data-stu-id="5df8f-377">For more information, see the article on the [`fixed` statement](../language-reference/keywords/fixed-statement.md).</span></span>

### <a name="stackalloc-arrays-support-initializers"></a><span data-ttu-id="5df8f-378">`stackalloc` Tablice obsługują inicjatory</span><span class="sxs-lookup"><span data-stu-id="5df8f-378">`stackalloc` arrays support initializers</span></span>

<span data-ttu-id="5df8f-379">Po zainicjowaniu można określić wartości dla elementów w tablicy:</span><span class="sxs-lookup"><span data-stu-id="5df8f-379">You've been able to specify the values for elements in an array when you initialize it:</span></span>

```csharp
var arr = new int[3] {1, 2, 3};
var arr2 = new int[] {1, 2, 3};
```

<span data-ttu-id="5df8f-380">Teraz tę samą składnię można zastosować do tablic, które są zadeklarowane za pomocą `stackalloc` :</span><span class="sxs-lookup"><span data-stu-id="5df8f-380">Now, that same syntax can be applied to arrays that are declared with `stackalloc`:</span></span>

```csharp
int* pArr = stackalloc int[3] {1, 2, 3};
int* pArr2 = stackalloc int[] {1, 2, 3};
Span<int> arr = stackalloc [] {1, 2, 3};
```

<span data-ttu-id="5df8f-381">Aby uzyskać więcej informacji, zobacz artykuł dotyczący [ `stackalloc` operatorów](../language-reference/operators/stackalloc.md) .</span><span class="sxs-lookup"><span data-stu-id="5df8f-381">For more information, see the [`stackalloc` operator](../language-reference/operators/stackalloc.md) article.</span></span>

### <a name="enhanced-generic-constraints"></a><span data-ttu-id="5df8f-382">Ulepszone ograniczenia ogólne</span><span class="sxs-lookup"><span data-stu-id="5df8f-382">Enhanced generic constraints</span></span>

<span data-ttu-id="5df8f-383">Teraz można określić typ <xref:System.Enum?displayProperty=nameWithType> lub <xref:System.Delegate?displayProperty=nameWithType> jako ograniczenia klasy bazowej dla parametru typu.</span><span class="sxs-lookup"><span data-stu-id="5df8f-383">You can now specify the type <xref:System.Enum?displayProperty=nameWithType> or <xref:System.Delegate?displayProperty=nameWithType> as base class constraints for a type parameter.</span></span>

<span data-ttu-id="5df8f-384">Można również użyć nowego `unmanaged` ograniczenia, aby określić, że parametr typu musi być [typem niezarządzanym](../language-reference/builtin-types/unmanaged-types.md)null.</span><span class="sxs-lookup"><span data-stu-id="5df8f-384">You can also use the new `unmanaged` constraint, to specify that a type parameter must be a non-nullable [unmanaged type](../language-reference/builtin-types/unmanaged-types.md).</span></span>

<span data-ttu-id="5df8f-385">Aby uzyskać więcej informacji, zobacz artykuły dotyczące [ `where` ograniczeń ogólnych](../language-reference/keywords/where-generic-type-constraint.md) i [ograniczeń dla parametrów typu](../programming-guide/generics/constraints-on-type-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="5df8f-385">For more information, see the articles on [`where` generic constraints](../language-reference/keywords/where-generic-type-constraint.md) and [constraints on type parameters](../programming-guide/generics/constraints-on-type-parameters.md).</span></span>

<span data-ttu-id="5df8f-386">Dodanie tych ograniczeń do istniejących typów jest [niezgodną zmianą](version-update-considerations.md#incompatible-changes).</span><span class="sxs-lookup"><span data-stu-id="5df8f-386">Adding these constraints to existing types is an [incompatible change](version-update-considerations.md#incompatible-changes).</span></span> <span data-ttu-id="5df8f-387">Zamknięte typy ogólne nie mogą już odpowiadać tym nowym ograniczeniom.</span><span class="sxs-lookup"><span data-stu-id="5df8f-387">Closed generic types may no longer meet these new constraints.</span></span>

### <a name="generalized-async-return-types"></a><span data-ttu-id="5df8f-388">Uogólnione asynchroniczne typy zwracane</span><span class="sxs-lookup"><span data-stu-id="5df8f-388">Generalized async return types</span></span>

<span data-ttu-id="5df8f-389">Zwrócenie `Task` obiektu z metod asynchronicznych może spowodować wąskie gardła wydajności w określonych ścieżkach.</span><span class="sxs-lookup"><span data-stu-id="5df8f-389">Returning a `Task` object from async methods can introduce performance bottlenecks in certain paths.</span></span> <span data-ttu-id="5df8f-390">`Task` to typ referencyjny, dlatego użycie go oznacza przydzielenie obiektu.</span><span class="sxs-lookup"><span data-stu-id="5df8f-390">`Task` is a reference type, so using it means allocating an object.</span></span> <span data-ttu-id="5df8f-391">W przypadkach, gdy metoda zadeklarowana za pomocą `async` modyfikatora zwraca zbuforowany wynik lub wykonuje synchronicznie, dodatkowe alokacje mogą stać się ważnym kosztem w przypadku krytycznych sekcji kodu.</span><span class="sxs-lookup"><span data-stu-id="5df8f-391">In cases where a method declared with the `async` modifier returns a cached result, or completes synchronously, the extra allocations can become a significant time cost in performance critical sections of code.</span></span> <span data-ttu-id="5df8f-392">Może być kosztowna, jeśli te przydziały występują w ścisłych pętlach.</span><span class="sxs-lookup"><span data-stu-id="5df8f-392">It can become costly if those allocations occur in tight loops.</span></span>

<span data-ttu-id="5df8f-393">Nowa funkcja języka oznacza, że zwracane typy metod asynchronicznych nie są ograniczone do `Task` , `Task<T>` , i `void` .</span><span class="sxs-lookup"><span data-stu-id="5df8f-393">The new language feature means that async method return types aren't limited to `Task`, `Task<T>`, and `void`.</span></span> <span data-ttu-id="5df8f-394">Zwracany typ musi nadal spełniać wzorzec asynchroniczny, co oznacza, że `GetAwaiter` Metoda musi być dostępna.</span><span class="sxs-lookup"><span data-stu-id="5df8f-394">The returned type must still satisfy the async pattern, meaning a `GetAwaiter` method must be accessible.</span></span> <span data-ttu-id="5df8f-395">Jak określono w konkretnym przykładzie, `ValueTask` Typ został dodany do platformy .NET, aby można było korzystać z tej nowej funkcji języka:</span><span class="sxs-lookup"><span data-stu-id="5df8f-395">As one concrete example, the `ValueTask` type has been added to .NET to make use of this new language feature:</span></span>

[!code-csharp[UsingValueTask](~/samples/snippets/csharp/new-in-7/AsyncWork.cs#UsingValueTask "Using ValueTask")]

> [!NOTE]
> <span data-ttu-id="5df8f-396">Należy dodać pakiet NuGet [`System.Threading.Tasks.Extensions`](https://www.nuget.org/packages/System.Threading.Tasks.Extensions/) >, aby można było użyć <xref:System.Threading.Tasks.ValueTask%601> typu.</span><span class="sxs-lookup"><span data-stu-id="5df8f-396">You need to add the NuGet package [`System.Threading.Tasks.Extensions`](https://www.nuget.org/packages/System.Threading.Tasks.Extensions/) > in order to use the <xref:System.Threading.Tasks.ValueTask%601> type.</span></span>

<span data-ttu-id="5df8f-397">To ulepszenie jest najbardziej przydatne w przypadku autorów bibliotek, aby uniknąć alokowania `Task` w kodzie krytycznym wydajności.</span><span class="sxs-lookup"><span data-stu-id="5df8f-397">This enhancement is most useful for library authors to avoid allocating a `Task` in performance critical code.</span></span>

## <a name="new-compiler-options"></a><span data-ttu-id="5df8f-398">Nowe opcje kompilatora</span><span class="sxs-lookup"><span data-stu-id="5df8f-398">New compiler options</span></span>

<span data-ttu-id="5df8f-399">Nowe opcje kompilatora obsługują nowe scenariusze kompilacji i DevOps dla programów w języku C#.</span><span class="sxs-lookup"><span data-stu-id="5df8f-399">New compiler options support new build and DevOps scenarios for C# programs.</span></span>

### <a name="reference-assembly-generation"></a><span data-ttu-id="5df8f-400">Generowanie zestawu odwołań</span><span class="sxs-lookup"><span data-stu-id="5df8f-400">Reference assembly generation</span></span>

<span data-ttu-id="5df8f-401">Istnieją dwie nowe opcje kompilatora, które generują *zestawy tylko do odwołania*: [-opcji refout](../language-reference/compiler-options/refout-compiler-option.md) i [-refonly](../language-reference/compiler-options/refonly-compiler-option.md).</span><span class="sxs-lookup"><span data-stu-id="5df8f-401">There are two new compiler options that generate *reference-only assemblies*: [-refout](../language-reference/compiler-options/refout-compiler-option.md) and [-refonly](../language-reference/compiler-options/refonly-compiler-option.md).</span></span>
<span data-ttu-id="5df8f-402">Połączone artykuły wyjaśniają te opcje i zestawy referencyjne bardziej szczegółowo.</span><span class="sxs-lookup"><span data-stu-id="5df8f-402">The linked articles explain these options and reference assemblies in more detail.</span></span>

### <a name="public-or-open-source-signing"></a><span data-ttu-id="5df8f-403">Podpisywanie publiczne lub Open Source</span><span class="sxs-lookup"><span data-stu-id="5df8f-403">Public or Open Source signing</span></span>

<span data-ttu-id="5df8f-404">`-publicsign`Opcja kompilatora instruuje kompilator do podpisania zestawu przy użyciu klucza publicznego.</span><span class="sxs-lookup"><span data-stu-id="5df8f-404">The `-publicsign` compiler option instructs the compiler to sign the assembly using a public key.</span></span> <span data-ttu-id="5df8f-405">Zestaw jest oznaczony jako podpisany, ale podpis jest pobierany z klucza publicznego.</span><span class="sxs-lookup"><span data-stu-id="5df8f-405">The assembly is marked as signed, but the signature is taken from the public key.</span></span> <span data-ttu-id="5df8f-406">Ta opcja umożliwia tworzenie podpisanych zestawów z projektów typu "open source" przy użyciu klucza publicznego.</span><span class="sxs-lookup"><span data-stu-id="5df8f-406">This option enables you to build signed assemblies from open-source projects using a public key.</span></span>

<span data-ttu-id="5df8f-407">Aby uzyskać więcej informacji, zobacz [publicsign opcji kompilatora](../language-reference/compiler-options/publicsign-compiler-option.md) .</span><span class="sxs-lookup"><span data-stu-id="5df8f-407">For more information, see the [-publicsign compiler option](../language-reference/compiler-options/publicsign-compiler-option.md) article.</span></span>

### <a name="pathmap"></a><span data-ttu-id="5df8f-408">elemencie pathmap</span><span class="sxs-lookup"><span data-stu-id="5df8f-408">pathmap</span></span>

<span data-ttu-id="5df8f-409">`-pathmap`Opcja kompilatora instruuje kompilator, aby zamieniać ścieżki źródłowe ze środowiska kompilacji z zamapowanymi ścieżkami źródłowymi.</span><span class="sxs-lookup"><span data-stu-id="5df8f-409">The `-pathmap` compiler option instructs the compiler to replace source paths from the build environment with mapped source paths.</span></span> <span data-ttu-id="5df8f-410">`-pathmap`Opcja steruje ścieżką źródłową zapisaną przez kompilator do plików PDB lub dla <xref:System.Runtime.CompilerServices.CallerFilePathAttribute> .</span><span class="sxs-lookup"><span data-stu-id="5df8f-410">The `-pathmap` option controls the source path written by the compiler to PDB files or for the <xref:System.Runtime.CompilerServices.CallerFilePathAttribute>.</span></span>

<span data-ttu-id="5df8f-411">Aby uzyskać więcej informacji, zobacz [elemencie pathmap opcji kompilatora](../language-reference/compiler-options/pathmap-compiler-option.md) .</span><span class="sxs-lookup"><span data-stu-id="5df8f-411">For more information, see the [-pathmap compiler option](../language-reference/compiler-options/pathmap-compiler-option.md) article.</span></span>
