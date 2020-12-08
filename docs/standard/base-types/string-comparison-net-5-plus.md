---
title: Zachowanie zmian w przypadku porównywania ciągów w programie .NET 5 +
description: Informacje o zmianach zachowania porównania ciągów w programie .NET 5 i nowszych wersjach w systemie Windows.
ms.date: 12/07/2020
ms.openlocfilehash: a53c36b31785fb43c0aa5f5040042abb6d40031a
ms.sourcegitcommit: 45c7148f2483db2501c1aa696ab6ed2ed8cb71b2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/08/2020
ms.locfileid: "96851754"
---
# <a name="behavior-changes-when-comparing-strings-on-net-5"></a><span data-ttu-id="fdae6-103">Zachowanie zmian w przypadku porównywania ciągów w programie .NET 5 +</span><span class="sxs-lookup"><span data-stu-id="fdae6-103">Behavior changes when comparing strings on .NET 5+</span></span>

<span data-ttu-id="fdae6-104">W programie .NET 5,0 wprowadzono zmianę behawioralną środowiska uruchomieniowego, w której interfejsy API globalizacji [teraz domyślnie używają ICU](../../core/compatibility/globalization/5.0/icu-globalization-api.md) na wszystkich obsługiwanych platformach.</span><span class="sxs-lookup"><span data-stu-id="fdae6-104">.NET 5.0 introduces a runtime behavioral change where globalization APIs [now use ICU by default](../../core/compatibility/globalization/5.0/icu-globalization-api.md) across all supported platforms.</span></span> <span data-ttu-id="fdae6-105">Jest to wyjście z wcześniejszych wersji programu .NET Core i z .NET Framework, które korzystają z funkcji obsługi języka narodowego (NLS) systemu operacyjnego w przypadku uruchamiania w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="fdae6-105">This is a departure from earlier versions of .NET Core and from .NET Framework, which utilize the operating system's national language support (NLS) functionality when running on Windows.</span></span> <span data-ttu-id="fdae6-106">Aby uzyskać więcej informacji na temat tych zmian, w tym przełączników zgodności, które mogą przywrócić zmianę zachowania, zobacz [globalizacja platformy .NET i ICU](../globalization-localization/globalization-icu.md).</span><span class="sxs-lookup"><span data-stu-id="fdae6-106">For more information on these changes, including compatibility switches that can revert the behavior change, see [.NET globalization and ICU](../globalization-localization/globalization-icu.md).</span></span>

## <a name="reason-for-change"></a><span data-ttu-id="fdae6-107">Przyczyna zmiany</span><span class="sxs-lookup"><span data-stu-id="fdae6-107">Reason for change</span></span>

<span data-ttu-id="fdae6-108">Ta zmiana została wprowadzona w celu ujednolicenia. Zachowanie globalizacji sieci we wszystkich obsługiwanych systemach operacyjnych.</span><span class="sxs-lookup"><span data-stu-id="fdae6-108">This change was introduced to unify .NET's globalization behavior across all supported operating systems.</span></span> <span data-ttu-id="fdae6-109">Zapewnia również możliwość tworzenia przez aplikacje własnych bibliotek globalizacji, a nie zależą od wbudowanych bibliotek systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="fdae6-109">It also provides the ability for applications to bundle their own globalization libraries rather than depend on the OS's built-in libraries.</span></span> <span data-ttu-id="fdae6-110">Aby uzyskać więcej informacji, zobacz [powiadomienie o zmianie](../../core/compatibility/globalization/5.0/icu-globalization-api.md).</span><span class="sxs-lookup"><span data-stu-id="fdae6-110">For more information, see [the breaking change notification](../../core/compatibility/globalization/5.0/icu-globalization-api.md).</span></span>

## <a name="behavioral-differences"></a><span data-ttu-id="fdae6-111">Różnice w zachowaniu</span><span class="sxs-lookup"><span data-stu-id="fdae6-111">Behavioral differences</span></span>

<span data-ttu-id="fdae6-112">Jeśli używasz funkcji, takich jak `string.IndexOf(string)` bez wywoływania przeciążenia, które przyjmuje <xref:System.StringComparison> argument, możesz zamierzyć wyszukiwanie *porządkowe* , ale zamiast tego przypadkowo wykonujesz zależność od zachowania specyficznego dla kultury.</span><span class="sxs-lookup"><span data-stu-id="fdae6-112">If you use functions like `string.IndexOf(string)` without calling the overload that takes a <xref:System.StringComparison> argument, you might intend to perform an *ordinal* search, but instead you inadvertently take a dependency on culture-specific behavior.</span></span> <span data-ttu-id="fdae6-113">Ponieważ funkcje NLS i ICU implementują inną logikę w ich porównania językowe, wyniki metod takich jak `string.IndexOf(string)` mogą zwracać nieoczekiwane wartości.</span><span class="sxs-lookup"><span data-stu-id="fdae6-113">Since NLS and ICU implement different logic in their linguistic comparers, the results of methods like `string.IndexOf(string)` can return unexpected values.</span></span>

<span data-ttu-id="fdae6-114">Może to spowodować, że jest to możliwe nawet w miejscach, w których nie zawsze oczekuje się, że funkcje globalizacji są aktywne.</span><span class="sxs-lookup"><span data-stu-id="fdae6-114">This can manifest itself even in places where you aren't always expecting globalization facilities to be active.</span></span> <span data-ttu-id="fdae6-115">Na przykład poniższy kod może utworzyć inną odpowiedź w zależności od bieżącego środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="fdae6-115">For example, the following code can produce a different answer depending on the current runtime.</span></span>

```cs
string s = "Hello\r\nworld!";
int idx = s.IndexOf("\n");
Console.WriteLine(idx);

// The snippet prints:
//
// '6' when running on .NET Framework (Windows)
// '6' when running on .NET Core 2.x - 3.x (Windows)
// '-1' when running on .NET 5 (Windows)
// '-1' when running on .NET Core 2.x - 3.x or .NET 5 (non-Windows)
// '6' when running on .NET Core 2.x or .NET 5 (in invariant mode)
```

## <a name="guard-against-unexpected-behavior"></a><span data-ttu-id="fdae6-116">Ochrona przed nieoczekiwanym zachowaniem</span><span class="sxs-lookup"><span data-stu-id="fdae6-116">Guard against unexpected behavior</span></span>

<span data-ttu-id="fdae6-117">Ta sekcja zawiera dwie opcje dotyczące postępowania z nieoczekiwanymi zmianami zachowania w programie .NET 5,0.</span><span class="sxs-lookup"><span data-stu-id="fdae6-117">This section provides two options for dealing with unexpected behavior changes in .NET 5.0.</span></span>

### <a name="enable-code-analyzers"></a><span data-ttu-id="fdae6-118">Włącz analizatory kodu</span><span class="sxs-lookup"><span data-stu-id="fdae6-118">Enable code analyzers</span></span>

<span data-ttu-id="fdae6-119">[Analizatory kodu](../../fundamentals/code-analysis/overview.md) mogą wykrywać możliwe wywołania debugowania.</span><span class="sxs-lookup"><span data-stu-id="fdae6-119">[Code analyzers](../../fundamentals/code-analysis/overview.md) can detect possibly buggy call sites.</span></span> <span data-ttu-id="fdae6-120">Aby pomóc w ochronie przed wszelkimi zachowaniami zaskakujące, zalecamy włączenie analizatorów platformy .NET kompilators (Roslyn) w projekcie.</span><span class="sxs-lookup"><span data-stu-id="fdae6-120">To help guard against any surprising behaviors, we recommend enabling .NET compiler platform (Roslyn) analyzers in your project.</span></span> <span data-ttu-id="fdae6-121">Analizatory ułatwiają flagę kodu, który może przypadkowo używać funkcji porównującej język, gdy wartośćowa wartość porównująca była prawdopodobnie zamierzona.</span><span class="sxs-lookup"><span data-stu-id="fdae6-121">The analyzers help flag code that might inadvertently be using a linguistic comparer when an ordinal comparer was likely intended.</span></span> <span data-ttu-id="fdae6-122">Następujące reguły powinny pomóc w oznaczeniu tych problemów:</span><span class="sxs-lookup"><span data-stu-id="fdae6-122">The following rules should help flag these issues:</span></span>

- [<span data-ttu-id="fdae6-123">CA1307: Określ parametr StringComparison w celu zapewnienia jednoznaczności</span><span class="sxs-lookup"><span data-stu-id="fdae6-123">CA1307: Specify StringComparison for clarity</span></span>](../../fundamentals/code-analysis/quality-rules/ca1307.md)
- [<span data-ttu-id="fdae6-124">CA1309: Użyj porządkowego ustawienia właściwości StringComparison</span><span class="sxs-lookup"><span data-stu-id="fdae6-124">CA1309: Use ordinal StringComparison</span></span>](../../fundamentals/code-analysis/quality-rules/ca1309.md)
- [<span data-ttu-id="fdae6-125">CA1310: Określ parametr StringComparison w celu zapewnienia poprawności</span><span class="sxs-lookup"><span data-stu-id="fdae6-125">CA1310: Specify StringComparison for correctness</span></span>](../../fundamentals/code-analysis/quality-rules/ca1310.md)

<span data-ttu-id="fdae6-126">Te określone reguły nie są domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="fdae6-126">These specific rules aren't enabled by default.</span></span> <span data-ttu-id="fdae6-127">Aby je włączyć i pokazać wszystkie naruszenia jako błędy kompilacji, ustaw następujące właściwości w pliku projektu:</span><span class="sxs-lookup"><span data-stu-id="fdae6-127">To enable them and show any violations as build errors, set the following properties in your project file:</span></span>

```xml
<PropertyGroup>
  <AnalysisMode>AllEnabledByDefault</AnalysisMode>
  <WarningsAsErrors>$(WarningsAsErrors);CA1307;CA1309;CA1310</WarningsAsErrors>
</PropertyGroup>
```

<span data-ttu-id="fdae6-128">Poniższy fragment kodu przedstawia przykłady kodów, które tworzą odpowiednie ostrzeżenia analizatora kodu lub błędy.</span><span class="sxs-lookup"><span data-stu-id="fdae6-128">The following snippet shows examples of code that produces the relevant code analyzer warnings or errors.</span></span>

```cs
//
// Potentially incorrect code - answer might vary based on locale.
//
string s = GetString();
// Produces analyzer warning CA1310 for string; CA1307 matches on char ','
int idx = s.IndexOf(",");
Console.WriteLine(idx);

//
// Corrected code - matches the literal substring ",".
//
string s = GetString();
int idx = s.IndexOf(",", StringComparison.Ordinal);
Console.WriteLine(idx);

//
// Corrected code (alternative) - searches for the literal ',' character.
//
string s = GetString();
int idx = s.IndexOf(',');
Console.WriteLine(idx);
```

<span data-ttu-id="fdae6-129">Podobnie podczas tworzenia wystąpienia posortowanej kolekcji ciągów lub sortowania istniejącej kolekcji opartej na ciągach należy określić jawną funkcję porównującą.</span><span class="sxs-lookup"><span data-stu-id="fdae6-129">Similarly, when instantiating a sorted collection of strings or sorting an existing string-based collection, specify an explicit comparer.</span></span>

```cs
//
// Potentially incorrect code - behavior might vary based on locale.
//
SortedSet<string> mySet = new SortedSet<string>();
List<string> list = GetListOfStrings();
list.Sort();

//
// Corrected code - uses ordinal sorting; doesn't vary by locale.
//
SortedSet<string> mySet = new SortedSet<string>(StringComparer.Ordinal);
List<string> list = GetListOfStrings();
list.Sort(StringComparer.Ordinal);
```

### <a name="revert-back-to-nls-behaviors"></a><span data-ttu-id="fdae6-130">Przywracanie zachowań NLS</span><span class="sxs-lookup"><span data-stu-id="fdae6-130">Revert back to NLS behaviors</span></span>

<span data-ttu-id="fdae6-131">Aby przywrócić aplikacje .NET 5 z powrotem do starszych zachowań funkcji NLS podczas działania w systemie Windows, wykonaj kroki opisane w temacie [globalizacja i ICU platformy .NET](../globalization-localization/globalization-icu.md).</span><span class="sxs-lookup"><span data-stu-id="fdae6-131">To revert .NET 5 applications back to older NLS behaviors when running on Windows, follow the steps in [.NET Globalization and ICU](../globalization-localization/globalization-icu.md).</span></span> <span data-ttu-id="fdae6-132">Ten przełącznik zgodności dla całej aplikacji musi być ustawiony na poziomie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fdae6-132">This application-wide compatibility switch must be set at the application level.</span></span> <span data-ttu-id="fdae6-133">Poszczególne biblioteki nie mogą korzystać z tego zachowania ani go wycofać.</span><span class="sxs-lookup"><span data-stu-id="fdae6-133">Individual libraries cannot opt-in or opt-out of this behavior.</span></span>

> [!TIP]
> <span data-ttu-id="fdae6-134">Zdecydowanie zalecamy włączenie reguł analizy kodu [CA1307](../../fundamentals/code-analysis/quality-rules/ca1307.md), [CA1309](../../fundamentals/code-analysis/quality-rules/ca1309.md)i [CA1310](../../fundamentals/code-analysis/quality-rules/ca1310.md) , aby pomóc w ulepszaniu higieny kodu i wykryciu wszelkich istniejących błędów.</span><span class="sxs-lookup"><span data-stu-id="fdae6-134">We strongly recommend you enable the [CA1307](../../fundamentals/code-analysis/quality-rules/ca1307.md), [CA1309](../../fundamentals/code-analysis/quality-rules/ca1309.md), and [CA1310](../../fundamentals/code-analysis/quality-rules/ca1310.md) code analysis rules to help improve code hygiene and discover any existing latent bugs.</span></span> <span data-ttu-id="fdae6-135">Aby uzyskać więcej informacji, zobacz [Włączanie analizatorów kodu](#enable-code-analyzers).</span><span class="sxs-lookup"><span data-stu-id="fdae6-135">For more information, see [Enable code analyzers](#enable-code-analyzers).</span></span>

## <a name="affected-apis"></a><span data-ttu-id="fdae6-136">Dotyczy interfejsów API</span><span class="sxs-lookup"><span data-stu-id="fdae6-136">Affected APIs</span></span>

<span data-ttu-id="fdae6-137">Większość aplikacji .NET nie napotka nieoczekiwanych zachowań spowodowanych zmianami w programie .NET 5,0.</span><span class="sxs-lookup"><span data-stu-id="fdae6-137">Most .NET applications won't encounter any unexpected behaviors due to the changes in .NET 5.0.</span></span> <span data-ttu-id="fdae6-138">Jednak ze względu na liczbę uszkodzonych interfejsów API i podstaw tych interfejsów API do szerszego ekosystemu .NET, należy pamiętać o potencjale dla programu .NET 5,0, aby wprowadzić niepożądane zachowania lub ujawnić ukryte usterki, które już istnieją w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fdae6-138">However, due to the number of affected APIs and how foundational these APIs are to the wider .NET ecosystem, you should be aware of the potential for .NET 5.0 to introduce unwanted behaviors or to expose latent bugs that already exist in your application.</span></span>

<span data-ttu-id="fdae6-139">Narażone interfejsy API obejmują:</span><span class="sxs-lookup"><span data-stu-id="fdae6-139">The affected APIs include:</span></span>

- <xref:System.String.Compare%2A?displayProperty=fullName>
- <xref:System.String.EndsWith%2A?displayProperty=fullName>
- <xref:System.String.IndexOf%2A?displayProperty=fullName>
- <xref:System.String.StartsWith%2A?displayProperty=fullName>
- <xref:System.String.ToLower%2A?displayProperty=fullName>
- <xref:System.String.ToLowerInvariant%2A?displayProperty=fullName>
- <xref:System.String.ToUpper%2A?displayProperty=fullName>
- <xref:System.String.ToUpperInvariant%2A?displayProperty=fullName>
- <span data-ttu-id="fdae6-140"><xref:System.Globalization.TextInfo?displayProperty=fullName> (większość elementów członkowskich)</span><span class="sxs-lookup"><span data-stu-id="fdae6-140"><xref:System.Globalization.TextInfo?displayProperty=fullName> (most members)</span></span>
- <span data-ttu-id="fdae6-141"><xref:System.Globalization.CompareInfo?displayProperty=fullName> (większość elementów członkowskich)</span><span class="sxs-lookup"><span data-stu-id="fdae6-141"><xref:System.Globalization.CompareInfo?displayProperty=fullName> (most members)</span></span>
- <span data-ttu-id="fdae6-142"><xref:System.Array.Sort%2A?displayProperty=fullName> (podczas sortowania tablic ciągów)</span><span class="sxs-lookup"><span data-stu-id="fdae6-142"><xref:System.Array.Sort%2A?displayProperty=fullName> (when sorting arrays of strings)</span></span>
- <span data-ttu-id="fdae6-143"><xref:System.Collections.Generic.List%601.Sort?displayProperty=fullName> (gdy elementy listy są ciągami)</span><span class="sxs-lookup"><span data-stu-id="fdae6-143"><xref:System.Collections.Generic.List%601.Sort?displayProperty=fullName> (when the list elements are strings)</span></span>
- <span data-ttu-id="fdae6-144"><xref:System.Collections.Generic.SortedDictionary%602?displayProperty=fullName> (gdy klucze są ciągami)</span><span class="sxs-lookup"><span data-stu-id="fdae6-144"><xref:System.Collections.Generic.SortedDictionary%602?displayProperty=fullName> (when the keys are strings)</span></span>
- <span data-ttu-id="fdae6-145"><xref:System.Collections.Generic.SortedList%602?displayProperty=fullName> (gdy klucze są ciągami)</span><span class="sxs-lookup"><span data-stu-id="fdae6-145"><xref:System.Collections.Generic.SortedList%602?displayProperty=fullName> (when the keys are strings)</span></span>
- <span data-ttu-id="fdae6-146"><xref:System.Collections.Generic.SortedSet%601?displayProperty=fullName> (gdy zestaw zawiera ciągi)</span><span class="sxs-lookup"><span data-stu-id="fdae6-146"><xref:System.Collections.Generic.SortedSet%601?displayProperty=fullName> (when the set contains strings)</span></span>

> [!NOTE]
> <span data-ttu-id="fdae6-147">Nie jest to pełna lista interfejsów API, których to dotyczy.</span><span class="sxs-lookup"><span data-stu-id="fdae6-147">This is not an exhaustive list of affected APIs.</span></span>

<span data-ttu-id="fdae6-148">Wszystkie powyższe interfejsy API używają domyślnie wyszukiwania ciągów *językowych* i porównywania przy użyciu [bieżącej kultury](xref:System.Threading.Thread.CurrentCulture)wątku.</span><span class="sxs-lookup"><span data-stu-id="fdae6-148">All of the above APIs use *linguistic* string searching and comparison using the thread's [current culture](xref:System.Threading.Thread.CurrentCulture), by default.</span></span> <span data-ttu-id="fdae6-149">Różnice między *językiem* a przeszukiwaniem i porównaniem *porządkowym* są określane w [liczbie porządkowej a przeszukiwaniu i porównaniu językowej](#ordinal-vs-linguistic-search-and-comparison).</span><span class="sxs-lookup"><span data-stu-id="fdae6-149">The differences between *linguistic* and *ordinal* search and comparison are called out in the [Ordinal vs. linguistic search and comparison](#ordinal-vs-linguistic-search-and-comparison).</span></span>

<span data-ttu-id="fdae6-150">Ponieważ ICU implementują porównania ciągów językowych inaczej niż w przypadku aplikacji NLS, opartych na systemie Windows, które uaktualniają do programu .NET 5,0 ze starszej wersji programu .NET Core lub .NET Framework, a wywołanie jednego z tych interfejsów API może zauważyć, że interfejsy API zaczynają się od innych zachowań.</span><span class="sxs-lookup"><span data-stu-id="fdae6-150">Because ICU implements linguistic string comparisons differently from NLS, Windows-based applications that upgrade to .NET 5.0 from an earlier version of .NET Core or .NET Framework and that call one of the affected APIs may notice that the APIs begin exhibiting different behaviors.</span></span>

### <a name="exceptions"></a><span data-ttu-id="fdae6-151">Wyjątki</span><span class="sxs-lookup"><span data-stu-id="fdae6-151">Exceptions</span></span>

* <span data-ttu-id="fdae6-152">Jeśli interfejs API akceptuje jawnie `StringComparison` lub `CultureInfo` parametr, ten parametr zastępuje zachowanie domyślne interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="fdae6-152">If an API accepts an explicit `StringComparison` or `CultureInfo` parameter, that parameter overrides the API's default behavior.</span></span>
* <span data-ttu-id="fdae6-153">`System.String` elementy członkowskie, w których pierwszy parametr jest typu `char` (na przykład <xref:System.String.IndexOf(System.Char)?displayProperty=nameWithType> ) używają wyszukiwania porządkowego, chyba że obiekt wywołujący przekazuje jawny `StringComparison` argument, który określa `CurrentCulture[IgnoreCase]` lub `InvariantCulture[IgnoreCase]` .</span><span class="sxs-lookup"><span data-stu-id="fdae6-153">`System.String` members where the first parameter is of type `char` (for example, <xref:System.String.IndexOf(System.Char)?displayProperty=nameWithType>) use ordinal searching, unless the caller passes an explicit `StringComparison` argument that specifies `CurrentCulture[IgnoreCase]` or `InvariantCulture[IgnoreCase]`.</span></span>

<span data-ttu-id="fdae6-154">Aby zapoznać się z bardziej szczegółową analizą zachowania poszczególnych <xref:System.String> interfejsów API, zobacz sekcję [domyślne typy wyszukiwania i porównywania](#default-search-and-comparison-types) .</span><span class="sxs-lookup"><span data-stu-id="fdae6-154">For a more detailed analysis of the default behavior of each <xref:System.String> API, see the [Default search and comparison types](#default-search-and-comparison-types) section.</span></span>

## <a name="ordinal-vs-linguistic-search-and-comparison"></a><span data-ttu-id="fdae6-155">Liczba porządkowa a wyszukiwanie lingwistyczne i porównanie</span><span class="sxs-lookup"><span data-stu-id="fdae6-155">Ordinal vs. linguistic search and comparison</span></span>

<span data-ttu-id="fdae6-156">*Liczba porządkowa* (znana także jako *niejęzykowa*) Wyszukiwanie i porównywanie składa ciąg w poszczególnych `char` elementach i wykonuje wyszukiwanie typu char-by-char.</span><span class="sxs-lookup"><span data-stu-id="fdae6-156">*Ordinal* (also known as *non-linguistic*) search and comparison decomposes a string into its individual `char` elements and performs a char-by-char search or comparison.</span></span> <span data-ttu-id="fdae6-157">Na przykład ciągi `"dog"` i `"dog"` porównywanie jako *takie* same, jak w przypadku opcji `Ordinal` porównującej, ponieważ dwa ciągi składają się z dokładnie tej samej sekwencji znaków.</span><span class="sxs-lookup"><span data-stu-id="fdae6-157">For example, the strings `"dog"` and `"dog"` compare as *equal* under an `Ordinal` comparer, since the two strings consist of the exact same sequence of chars.</span></span> <span data-ttu-id="fdae6-158">Jednakże `"dog"` i `"Dog"` porównać *nie równa* się w ramach opcji `Ordinal` porównującej, ponieważ nie zawierają dokładnie tej samej sekwencji znaków.</span><span class="sxs-lookup"><span data-stu-id="fdae6-158">However, `"dog"` and `"Dog"` compare as *not equal* under an `Ordinal` comparer, because they don't consist of the exact same sequence of chars.</span></span> <span data-ttu-id="fdae6-159">Oznacza to, że wielkie litery `'D'` `U+0044` występuje przed punktem kodu małymi literami `'d'` `U+0064` , co spowoduje `"dog"` sortowanie przed `"Dog"` .</span><span class="sxs-lookup"><span data-stu-id="fdae6-159">That is, uppercase `'D'`'s code point `U+0044` occurs before lowercase `'d'`'s code point `U+0064`, resulting in `"dog"` sorting before `"Dog"`.</span></span>

<span data-ttu-id="fdae6-160">`OrdinalIgnoreCase`Funkcja porównująca nadal działa na zasadzie typu char-by-char, ale eliminuje różnice wielkości liter podczas wykonywania operacji.</span><span class="sxs-lookup"><span data-stu-id="fdae6-160">An `OrdinalIgnoreCase` comparer still operates on a char-by-char basis, but it eliminates case differences while performing the operation.</span></span> <span data-ttu-id="fdae6-161">W obszarze `OrdinalIgnoreCase` porównującym pary znaków `'d'` i są `'D'` porównywane jako *równe*, tak jak pary char `'á'` i `'Á'` .</span><span class="sxs-lookup"><span data-stu-id="fdae6-161">Under an `OrdinalIgnoreCase` comparer, the char pairs `'d'` and `'D'` compare as *equal*, as do the char pairs `'á'` and `'Á'`.</span></span> <span data-ttu-id="fdae6-162">Ale nieakcentowane znak jest `'a'` porównywany z *nierównym* znakiem akcentu `'á'` .</span><span class="sxs-lookup"><span data-stu-id="fdae6-162">But the unaccented char `'a'` compares as *not equal* to the accented char `'á'`.</span></span>

<span data-ttu-id="fdae6-163">Kilka przykładów tego typu przedstawiono w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="fdae6-163">Some examples of this are provided in the following table:</span></span>

| <span data-ttu-id="fdae6-164">Ciąg 1</span><span class="sxs-lookup"><span data-stu-id="fdae6-164">String 1</span></span> | <span data-ttu-id="fdae6-165">Ciąg 2</span><span class="sxs-lookup"><span data-stu-id="fdae6-165">String 2</span></span> | <span data-ttu-id="fdae6-166">`Ordinal` prowadzone</span><span class="sxs-lookup"><span data-stu-id="fdae6-166">`Ordinal` comparison</span></span> | <span data-ttu-id="fdae6-167">`OrdinalIgnoreCase` prowadzone</span><span class="sxs-lookup"><span data-stu-id="fdae6-167">`OrdinalIgnoreCase` comparison</span></span> |
|---|---|---|---|
| `"dog"` | `"dog"` | <span data-ttu-id="fdae6-168">equal</span><span class="sxs-lookup"><span data-stu-id="fdae6-168">equal</span></span> | <span data-ttu-id="fdae6-169">equal</span><span class="sxs-lookup"><span data-stu-id="fdae6-169">equal</span></span> |
| `"dog"` | `"Dog"` | <span data-ttu-id="fdae6-170">nie równa się</span><span class="sxs-lookup"><span data-stu-id="fdae6-170">not equal</span></span> | <span data-ttu-id="fdae6-171">equal</span><span class="sxs-lookup"><span data-stu-id="fdae6-171">equal</span></span> |
| `"resume"` | `"Resume"` | <span data-ttu-id="fdae6-172">nie równa się</span><span class="sxs-lookup"><span data-stu-id="fdae6-172">not equal</span></span> | <span data-ttu-id="fdae6-173">equal</span><span class="sxs-lookup"><span data-stu-id="fdae6-173">equal</span></span> |
| `"resume"` | `"résumé"` | <span data-ttu-id="fdae6-174">nie równa się</span><span class="sxs-lookup"><span data-stu-id="fdae6-174">not equal</span></span> | <span data-ttu-id="fdae6-175">nie równa się</span><span class="sxs-lookup"><span data-stu-id="fdae6-175">not equal</span></span> |

<span data-ttu-id="fdae6-176">Unicode umożliwia również ciągów, które mają kilka różnych reprezentacji w pamięci.</span><span class="sxs-lookup"><span data-stu-id="fdae6-176">Unicode also allows strings to have several different in-memory representations.</span></span> <span data-ttu-id="fdae6-177">Na przykład e-ostra (é) może być reprezentowana na dwa możliwe sposoby:</span><span class="sxs-lookup"><span data-stu-id="fdae6-177">For example, an e-acute (é) can be represented in two possible ways:</span></span>

* <span data-ttu-id="fdae6-178">Pojedynczy znak literału `'é'` (również zapisany jako `'\u00E9'` ).</span><span class="sxs-lookup"><span data-stu-id="fdae6-178">A single literal `'é'` character (also written as `'\u00E9'`).</span></span>
* <span data-ttu-id="fdae6-179">Znak nieakcentowane literału `'e'` , po którym następuje łączenie znaku modyfikatora akcentu `'\u0301'` .</span><span class="sxs-lookup"><span data-stu-id="fdae6-179">A literal unaccented `'e'` character, followed by a combining accent modifier character `'\u0301'`.</span></span>

<span data-ttu-id="fdae6-180">Oznacza to, że _four_ `"résumé"` podczas wyświetlania są wyświetlane następujące cztery ciągi, nawet jeśli ich elementy składowe różnią się.</span><span class="sxs-lookup"><span data-stu-id="fdae6-180">This means that the following _four_ strings all result in `"résumé"` when displayed, even though their constituent pieces are different.</span></span> <span data-ttu-id="fdae6-181">Ciągi używają kombinacji znaków literału `'é'` lub literałów nieakcentowanech `'e'` znaków oraz łączenia modyfikatora akcentu `'\u0301'` .</span><span class="sxs-lookup"><span data-stu-id="fdae6-181">The strings use a combination of literal `'é'` characters or literal unaccented `'e'` characters plus the combining accent modifier `'\u0301'`.</span></span>

* `"r\u00E9sum\u00E9"`
* `"r\u00E9sume\u0301"`
* `"re\u0301sum\u00E9"`
* `"re\u0301sume\u0301"`

<span data-ttu-id="fdae6-182">W obszarze porównującej wartości porządkowej żaden z tych ciągów nie jest porównywany ze sobą.</span><span class="sxs-lookup"><span data-stu-id="fdae6-182">Under an ordinal comparer, none of these strings compare as equal to each other.</span></span> <span data-ttu-id="fdae6-183">Wynika to z faktu, że wszystkie one zawierają różne sekwencje znaków, nawet jeśli są renderowane na ekranie, wszystkie wyglądają tak samo.</span><span class="sxs-lookup"><span data-stu-id="fdae6-183">This is because they all contain different underlying char sequences, even though when they're rendered to the screen, they all look the same.</span></span>

<span data-ttu-id="fdae6-184">Podczas wykonywania `string.IndexOf(..., StringComparison.Ordinal)` operacji środowisko uruchomieniowe szuka dokładnego dopasowania podciągu.</span><span class="sxs-lookup"><span data-stu-id="fdae6-184">When performing a `string.IndexOf(..., StringComparison.Ordinal)` operation, the runtime looks for an exact substring match.</span></span> <span data-ttu-id="fdae6-185">Wyniki są następujące.</span><span class="sxs-lookup"><span data-stu-id="fdae6-185">The results are as follows.</span></span>

```cs
Console.WriteLine("resume".IndexOf("e", StringComparison.Ordinal)); // prints '1'
Console.WriteLine("r\u00E9sum\u00E9".IndexOf("e", StringComparison.Ordinal)); // prints '-1'
Console.WriteLine("r\u00E9sume\u0301".IndexOf("e", StringComparison.Ordinal)); // prints '5'
Console.WriteLine("re\u0301sum\u00E9".IndexOf("e", StringComparison.Ordinal)); // prints '1'
Console.WriteLine("re\u0301sume\u0301".IndexOf("e", StringComparison.Ordinal)); // prints '1'
Console.WriteLine("resume".IndexOf("E", StringComparison.OrdinalIgnoreCase)); // prints '1'
Console.WriteLine("r\u00E9sum\u00E9".IndexOf("E", StringComparison.OrdinalIgnoreCase)); // prints '-1'
Console.WriteLine("r\u00E9sume\u0301".IndexOf("E", StringComparison.OrdinalIgnoreCase)); // prints '5'
Console.WriteLine("re\u0301sum\u00E9".IndexOf("E", StringComparison.OrdinalIgnoreCase)); // prints '1'
Console.WriteLine("re\u0301sume\u0301".IndexOf("E", StringComparison.OrdinalIgnoreCase)); // prints '1'
```

<span data-ttu-id="fdae6-186">Ustawienie kultury bieżącego wątku nie ma żadnego wpływania na liczby porządkowe wyszukiwania i procedury porównania.</span><span class="sxs-lookup"><span data-stu-id="fdae6-186">Ordinal search and comparison routines are never affected by the current thread's culture setting.</span></span>

<span data-ttu-id="fdae6-187">Procedury wyszukiwania i porównywania *lingwistycznego* służą do rozdzielania ciągu na *elementy sortowania* i wykonywania wyszukiwania lub porównywania tych elementów.</span><span class="sxs-lookup"><span data-stu-id="fdae6-187">*Linguistic* search and comparison routines decompose a string into *collation elements* and perform searches or comparisons on these elements.</span></span> <span data-ttu-id="fdae6-188">Nie jest konieczne mapowanie 1:1 między znakami ciągu a jego elementami sortowania elementów.</span><span class="sxs-lookup"><span data-stu-id="fdae6-188">There's not necessarily a 1:1 mapping between a string's characters and its constituent collation elements.</span></span> <span data-ttu-id="fdae6-189">Na przykład ciąg o długości 2 może składać się tylko z pojedynczego elementu sortowania.</span><span class="sxs-lookup"><span data-stu-id="fdae6-189">For example, a string of length 2 may consist of only a single collation element.</span></span> <span data-ttu-id="fdae6-190">Gdy dwa ciągi są porównywane w sposób obsługujący język, funkcja porównująca sprawdza, czy elementy sortowania dwóch ciągów mają takie same semantykę, nawet jeśli znaki literału ciągu są różne.</span><span class="sxs-lookup"><span data-stu-id="fdae6-190">When two strings are compared in a linguistic-aware fashion, the comparer checks whether the two strings' collation elements have the same semantic meaning, even if the string's literal characters are different.</span></span>

<span data-ttu-id="fdae6-191">Rozważ ponownie ciąg `"résumé"` i cztery różne reprezentacje.</span><span class="sxs-lookup"><span data-stu-id="fdae6-191">Consider again the string `"résumé"` and its four different representations.</span></span> <span data-ttu-id="fdae6-192">W poniższej tabeli przedstawiono każdą reprezentację rozdzielona na elementy sortowania.</span><span class="sxs-lookup"><span data-stu-id="fdae6-192">The following table shows each representation broken down into its collation elements.</span></span>

| <span data-ttu-id="fdae6-193">Ciąg</span><span class="sxs-lookup"><span data-stu-id="fdae6-193">String</span></span> | <span data-ttu-id="fdae6-194">Jako elementy sortowania</span><span class="sxs-lookup"><span data-stu-id="fdae6-194">As collation elements</span></span> |
|---|---|
| `"r\u00E9sum\u00E9"` | `"r" + "\u00E9" + "s" + "u" + "m" + "\u00E9"` |
| `"r\u00E9sume\u0301"` | `"r" + "\u00E9" + "s" + "u" + "m" + "e\u0301"` |
| `"re\u0301sum\u00E9"` | `"r" + "e\u0301" + "s" + "u" + "m" + "\u00E9"` |
| `"re\u0301sume\u0301"` | `"r" + "e\u00E9" + "s" + "u" + "m" + "e\u0301"` |

<span data-ttu-id="fdae6-195">Element sortowania ponosi swobodne informacje o tym, co czytelnicy mogą traktować jako pojedynczy znak lub klaster znaków.</span><span class="sxs-lookup"><span data-stu-id="fdae6-195">A collation element corresponds loosely to what readers would think of as a single character or cluster of characters.</span></span> <span data-ttu-id="fdae6-196">Jest on koncepcyjnie podobny do [klastra Grapheme](character-encoding-introduction.md#grapheme-clusters) , ale obejmuje nieco większy parasol.</span><span class="sxs-lookup"><span data-stu-id="fdae6-196">It's conceptually similar to a [grapheme cluster](character-encoding-introduction.md#grapheme-clusters) but encompasses a somewhat larger umbrella.</span></span>

<span data-ttu-id="fdae6-197">W przypadku opcji porównującej język dokładne dopasowania nie są konieczne.</span><span class="sxs-lookup"><span data-stu-id="fdae6-197">Under a linguistic comparer, exact matches aren't necessary.</span></span> <span data-ttu-id="fdae6-198">W przeciwieństwie do ich semantyki są porównywane elementy sortowania.</span><span class="sxs-lookup"><span data-stu-id="fdae6-198">Collation elements are instead compared based on their semantic meaning.</span></span> <span data-ttu-id="fdae6-199">Na przykład, funkcja porównująca język traktuje podciągi `"\u00E9"` i jest `"e\u0301"` równe, ponieważ obie semantyką oznaczają "małą literę e z ostrym modyfikatorem akcentu".</span><span class="sxs-lookup"><span data-stu-id="fdae6-199">For example, a linguistic comparer treats the substrings `"\u00E9"` and `"e\u0301"` as equal since they both semantically mean "a lowercase e with an acute accent modifier."</span></span> <span data-ttu-id="fdae6-200">Dzięki temu `IndexOf` Metoda pasuje do podciągu `"e\u0301"` w większym ciągu zawierającym semantycznie równoważny podciąg `"\u00E9"` , jak pokazano w poniższym przykładzie kodu.</span><span class="sxs-lookup"><span data-stu-id="fdae6-200">This allows the `IndexOf` method to match the substring `"e\u0301"` within a larger string that contains the semantically equivalent substring `"\u00E9"`, as shown in the following code sample.</span></span>

```cs
Console.WriteLine("r\u00E9sum\u00E9".IndexOf("e")); // prints '-1' (not found)
Console.WriteLine("r\u00E9sum\u00E9".IndexOf("e\u00E9")); // prints '1'
Console.WriteLine("\u00E9".IndexOf("e\u00E9")); // prints '0'
```

<span data-ttu-id="fdae6-201">W związku z tym dwa ciągi o różnych długości mogą być porównywane tak samo, jak w przypadku użycia porównania językowe.</span><span class="sxs-lookup"><span data-stu-id="fdae6-201">As a consequence of this, two strings of different lengths may compare as equal if a linguistic comparison is used.</span></span> <span data-ttu-id="fdae6-202">Obiekty wywołujące powinny zadbać o to, aby nie występowały specyficzne dla logiki wielkości liter, która zajmuje się długością ciągu w takich scenariuszach.</span><span class="sxs-lookup"><span data-stu-id="fdae6-202">Callers should take care not to special-case logic that deals with string length in such scenarios.</span></span>

<span data-ttu-id="fdae6-203">Procedury wyszukiwania i porównywania *z obsługą kultur* są specjalną formą procedur wyszukiwania i porównywania języków.</span><span class="sxs-lookup"><span data-stu-id="fdae6-203">*Culture-aware* search and comparison routines are a special form of linguistic search and comparison routines.</span></span> <span data-ttu-id="fdae6-204">W obszarze porównującym z kulturą pojęcie elementu sortowania jest rozszerzane w celu uwzględnienia informacji specyficznych dla określonej kultury.</span><span class="sxs-lookup"><span data-stu-id="fdae6-204">Under a culture-aware comparer, the concept of a collation element is extended to include information specific to the specified culture.</span></span>

<span data-ttu-id="fdae6-205">Na przykład [w alfabecie węgierskim](https://en.wikipedia.org/wiki/Hungarian_alphabet), gdy dwa znaki \<dz\> są wyświetlane z powrotem do tyłu, są uznawane za ich własną unikatową literę inną niż \<d\> lub \<z\> .</span><span class="sxs-lookup"><span data-stu-id="fdae6-205">For example, [in the Hungarian alphabet](https://en.wikipedia.org/wiki/Hungarian_alphabet), when the two characters \<dz\> appear back-to-back, they are considered their own unique letter distinct from either \<d\> or \<z\>.</span></span> <span data-ttu-id="fdae6-206">Oznacza to, że kiedy \<dz\> występuje w ciągu, węgierskia funkcja porównująca z obsługą kultur traktuje ją jako pojedynczy element sortowania.</span><span class="sxs-lookup"><span data-stu-id="fdae6-206">This means that when \<dz\> is seen in a string, a Hungarian culture-aware comparer treats it as a single collation element.</span></span>

| <span data-ttu-id="fdae6-207">Ciąg</span><span class="sxs-lookup"><span data-stu-id="fdae6-207">String</span></span> | <span data-ttu-id="fdae6-208">Jako elementy sortowania</span><span class="sxs-lookup"><span data-stu-id="fdae6-208">As collation elements</span></span> | <span data-ttu-id="fdae6-209">Uwagi</span><span class="sxs-lookup"><span data-stu-id="fdae6-209">Remarks</span></span> |
|---|---|---|
| `"endz"` | `"e" + "n" + "d" + "z"` | <span data-ttu-id="fdae6-210">(przy użyciu standardowej funkcji porównującej język)</span><span class="sxs-lookup"><span data-stu-id="fdae6-210">(using a standard linguistic comparer)</span></span> |
| `"endz"` | `"e" + "n" + "dz"` | <span data-ttu-id="fdae6-211">(przy użyciu węgierskiej funkcji porównującej z kulturą)</span><span class="sxs-lookup"><span data-stu-id="fdae6-211">(using a Hungarian culture-aware comparer)</span></span> |

<span data-ttu-id="fdae6-212">W przypadku korzystania z funkcji porównującej opartej na kulturze węgierskiej, oznacza to, że ciąg nie `"endz"` *does not* kończy się podciągiem `"z"` , ponieważ < \dz \> i < \z \> są uważane za elementy sortowania o różnym znaczeniu semantycznym.</span><span class="sxs-lookup"><span data-stu-id="fdae6-212">When using a Hungarian culture-aware comparer, this means that the string `"endz"` *does not* end with the substring `"z"`, as <\dz\> and <\z\> are considered collation elements with different semantic meaning.</span></span>

```cs
// Set thread culture to Hungarian
CultureInfo.CurrentCulture = CultureInfo.GetCultureInfo("hu-HU");
Console.WriteLine("endz".EndsWith("z")); // Prints 'False'

// Set thread culture to invariant culture
CultureInfo.CurrentCulture = CultureInfo.InvariantCulture;
Console.WriteLine("endz".EndsWith("z")); // Prints 'True'
```

> [!NOTE]
>
> - <span data-ttu-id="fdae6-213">Zachowanie: w przypadku języków i funkcji porównujących z obsługą kultur mogą być poddawane korekty zachowań od czasu do czasu.</span><span class="sxs-lookup"><span data-stu-id="fdae6-213">Behavior: Linguistic and culture-aware comparers can undergo behavioral adjustments from time to time.</span></span> <span data-ttu-id="fdae6-214">Zarówno ICU, jak i Starsza funkcja funkcji NLS systemu Windows są aktualizowane w celu uwzględnienia zmian w językach świata.</span><span class="sxs-lookup"><span data-stu-id="fdae6-214">Both ICU and the older Windows NLS facility are updated to account for how world languages change.</span></span> <span data-ttu-id="fdae6-215">Aby uzyskać więcej informacji, zobacz zmiany danych regionalnych wpisów w blogu [(kulturę)](/archive/blogs/shawnste/locale-culture-data-churn).</span><span class="sxs-lookup"><span data-stu-id="fdae6-215">For more information, see the blog post [Locale (culture) data churn](/archive/blogs/shawnste/locale-culture-data-churn).</span></span> <span data-ttu-id="fdae6-216">Zachowanie funkcji porównującej *liczby porządkowej* nigdy nie ulegnie zmianie, ponieważ wykonuje dokładne wyszukiwanie bitowe i porównanie.</span><span class="sxs-lookup"><span data-stu-id="fdae6-216">The *Ordinal* comparer's behavior will never change since it performs exact bitwise searching and comparison.</span></span> <span data-ttu-id="fdae6-217">Jednak zachowanie funkcji porównującej *OrdinalIgnoreCase* może ulec zmianie w miarę zwiększania rozmiaru Unicode, aby obejmowało więcej zestawów znaków i poprawiał pominięcia w istniejących danych o wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="fdae6-217">However, the *OrdinalIgnoreCase* comparer's behavior may change as Unicode grows to encompass more character sets and corrects omissions in existing casing data.</span></span>
> - <span data-ttu-id="fdae6-218">Użycie: funkcje porównujące `StringComparison.InvariantCulture` i `StringComparison.InvariantCultureIgnoreCase` są to porównania językowe, które nie obsługują kultury.</span><span class="sxs-lookup"><span data-stu-id="fdae6-218">Usage: The comparers `StringComparison.InvariantCulture` and `StringComparison.InvariantCultureIgnoreCase` are linguistic comparers that are not culture-aware.</span></span> <span data-ttu-id="fdae6-219">Oznacza to, że te porównania są zrozumiałe dla pojęć, takich jak znak wyróżniony é, z wieloma możliwymi reprezentacjami, i że wszystkie takie reprezentacje powinny być traktowane jako równe.</span><span class="sxs-lookup"><span data-stu-id="fdae6-219">That is, these comparers understand concepts such as the accented character é having multiple possible underlying representations, and that all such representations should be treated equal.</span></span> <span data-ttu-id="fdae6-220">Ale nieoparte na kulturze funkcje porównujące nie będą zawierały specjalnej obsługi dla elementu \<dz\> DISTINCT z \<d\> lub \<z\> , jak pokazano powyżej.</span><span class="sxs-lookup"><span data-stu-id="fdae6-220">But non-culture-aware linguistic comparers won't contain special handling for \<dz\> as distinct from \<d\> or \<z\>, as shown above.</span></span> <span data-ttu-id="fdae6-221">Nie mogą również zawierać specjalnych liter, takich jak niemiecki Eszett (ß).</span><span class="sxs-lookup"><span data-stu-id="fdae6-221">They also won't special-case characters like the German Eszett (ß).</span></span>

<span data-ttu-id="fdae6-222">Platforma .NET oferuje również *niezmienną tryb globalizacji*.</span><span class="sxs-lookup"><span data-stu-id="fdae6-222">.NET also offers the *invariant globalization mode*.</span></span> <span data-ttu-id="fdae6-223">Ten tryb rezygnacji wyłącza ścieżki kodu, które zajmują się przeszukiwaniem językowym i procedurami porównania.</span><span class="sxs-lookup"><span data-stu-id="fdae6-223">This opt-in mode disables code paths that deal with linguistic search and comparison routines.</span></span> <span data-ttu-id="fdae6-224">W tym trybie wszystkie operacje używają wartości *porządkowych* lub *OrdinalIgnoreCase* , niezależnie od tego, `CultureInfo` co `StringComparison` lub argument obiektu wywołującego.</span><span class="sxs-lookup"><span data-stu-id="fdae6-224">In this mode, all operations use *Ordinal* or *OrdinalIgnoreCase* behaviors, regardless of what `CultureInfo` or `StringComparison` argument the caller provides.</span></span> <span data-ttu-id="fdae6-225">Aby uzyskać więcej informacji, zobacz [Opcje konfiguracji czasu wykonywania dla globalizacji](../../core/run-time-config/globalization.md) i [tryb niezmienny globalizacji platformy .NET Core](https://github.com/dotnet/runtime/blob/master/docs/design/features/globalization-invariant-mode.md).</span><span class="sxs-lookup"><span data-stu-id="fdae6-225">For more information, see [Run-time configuration options for globalization](../../core/run-time-config/globalization.md) and [.NET Core Globalization Invariant Mode](https://github.com/dotnet/runtime/blob/master/docs/design/features/globalization-invariant-mode.md).</span></span>

<span data-ttu-id="fdae6-226">Aby uzyskać więcej informacji, zobacz [najlepsze rozwiązania dotyczące porównywania ciągów w programie .NET](best-practices-strings.md).</span><span class="sxs-lookup"><span data-stu-id="fdae6-226">For more information, see [Best practices for comparing strings in .NET](best-practices-strings.md).</span></span>

## <a name="security-implications"></a><span data-ttu-id="fdae6-227">Implikacje dotyczące bezpieczeństwa</span><span class="sxs-lookup"><span data-stu-id="fdae6-227">Security implications</span></span>

<span data-ttu-id="fdae6-228">Jeśli aplikacja korzysta z dostosowanego do filtrowania interfejsu API, zalecamy włączenie reguł analizy kodu CA1307 i CA1309, aby pomóc w znalezieniu miejsc, w których wyszukiwanie lingwistyczne mogło przypadkowo zostać użyte zamiast wyszukiwania porządkowego.</span><span class="sxs-lookup"><span data-stu-id="fdae6-228">If your app uses an affected API for filtering, we recommend enabling the CA1307 and CA1309 code analysis rules to help locate places where a linguistic search may have inadvertently been used instead of an ordinal search.</span></span> <span data-ttu-id="fdae6-229">Wzorce kodu podobne do poniższych mogą być podatne na luki w zabezpieczeniach.</span><span class="sxs-lookup"><span data-stu-id="fdae6-229">Code patterns like the following may be susceptible to security exploits.</span></span>

```cs
//
// THIS SAMPLE CODE IS INCORRECT.
// DO NOT USE IT IN PRODUCTION.
//
public bool ContainsHtmlSensitiveCharacters(string input)
{
    if (input.IndexOf("<") >= 0) { return true; }
    if (input.IndexOf("&") >= 0) { return true; }
    return false;
}
```

<span data-ttu-id="fdae6-230">Ponieważ `string.IndexOf(string)` Metoda domyślnie używa wyszukiwania w języku językowym, możliwe jest, aby ciąg zawierał literał `'<'` lub `'&'` znak i dla `string.IndexOf(string)` procedury zwracanej `-1` , wskazujący, że nie znaleziono podciągu wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="fdae6-230">Because the `string.IndexOf(string)` method uses a linguistic search by default, it's possible for a string to contain a literal `'<'` or `'&'` character and for the `string.IndexOf(string)` routine to return `-1`, indicating that the search substring was not found.</span></span> <span data-ttu-id="fdae6-231">Reguły analizy kodu CA1307 i CA1309 flag takich, które wywołują Lokacje i ostrzegają dewelopera o potencjalnym problemie.</span><span class="sxs-lookup"><span data-stu-id="fdae6-231">Code analysis rules CA1307 and CA1309 flag such call sites and alert the developer that there's a potential problem.</span></span>

## <a name="default-search-and-comparison-types"></a><span data-ttu-id="fdae6-232">Domyślne typy wyszukiwania i porównywania</span><span class="sxs-lookup"><span data-stu-id="fdae6-232">Default search and comparison types</span></span>

<span data-ttu-id="fdae6-233">W poniższej tabeli wymieniono domyślne typy wyszukiwania i porównywania dla różnych interfejsów API w postaci ciągów i ciągów.</span><span class="sxs-lookup"><span data-stu-id="fdae6-233">The following table lists the default search and comparison types for various string and string-like APIs.</span></span> <span data-ttu-id="fdae6-234">Jeśli obiekt wywołujący dostarcza jawny `CultureInfo` lub `StringComparison` parametr, ten parametr będzie honorować domyślnie.</span><span class="sxs-lookup"><span data-stu-id="fdae6-234">If the caller provides an explicit `CultureInfo` or `StringComparison` parameter, that parameter will be honored over any default.</span></span>

| <span data-ttu-id="fdae6-235">interfejs API</span><span class="sxs-lookup"><span data-stu-id="fdae6-235">API</span></span> | <span data-ttu-id="fdae6-236">Zachowanie domyślne</span><span class="sxs-lookup"><span data-stu-id="fdae6-236">Default behavior</span></span> | <span data-ttu-id="fdae6-237">Uwagi</span><span class="sxs-lookup"><span data-stu-id="fdae6-237">Remarks</span></span> |
|---|---|---|
| `string.Compare` | <span data-ttu-id="fdae6-238">CurrentCulture</span><span class="sxs-lookup"><span data-stu-id="fdae6-238">CurrentCulture</span></span> | |
| `string.CompareTo` | <span data-ttu-id="fdae6-239">CurrentCulture</span><span class="sxs-lookup"><span data-stu-id="fdae6-239">CurrentCulture</span></span> | |
| `string.Contains` | <span data-ttu-id="fdae6-240">Liczba porządkowa</span><span class="sxs-lookup"><span data-stu-id="fdae6-240">Ordinal</span></span> | |
| `string.EndsWith` | <span data-ttu-id="fdae6-241">Liczba porządkowa</span><span class="sxs-lookup"><span data-stu-id="fdae6-241">Ordinal</span></span> | <span data-ttu-id="fdae6-242">(gdy pierwszy parametr to a `char` )</span><span class="sxs-lookup"><span data-stu-id="fdae6-242">(when the first parameter is a `char`)</span></span> |
| `string.EndsWith` | <span data-ttu-id="fdae6-243">CurrentCulture</span><span class="sxs-lookup"><span data-stu-id="fdae6-243">CurrentCulture</span></span> | <span data-ttu-id="fdae6-244">(gdy pierwszy parametr to a `string` )</span><span class="sxs-lookup"><span data-stu-id="fdae6-244">(when the first parameter is a `string`)</span></span> |
| `string.Equals` | <span data-ttu-id="fdae6-245">Liczba porządkowa</span><span class="sxs-lookup"><span data-stu-id="fdae6-245">Ordinal</span></span> | |
| `string.GetHashCode` | <span data-ttu-id="fdae6-246">Liczba porządkowa</span><span class="sxs-lookup"><span data-stu-id="fdae6-246">Ordinal</span></span> | |
| `string.IndexOf` | <span data-ttu-id="fdae6-247">Liczba porządkowa</span><span class="sxs-lookup"><span data-stu-id="fdae6-247">Ordinal</span></span> | <span data-ttu-id="fdae6-248">(gdy pierwszy parametr to a `char` )</span><span class="sxs-lookup"><span data-stu-id="fdae6-248">(when the first parameter is a `char`)</span></span> |
| `string.IndexOf` | <span data-ttu-id="fdae6-249">CurrentCulture</span><span class="sxs-lookup"><span data-stu-id="fdae6-249">CurrentCulture</span></span> | <span data-ttu-id="fdae6-250">(gdy pierwszy parametr to a `string` )</span><span class="sxs-lookup"><span data-stu-id="fdae6-250">(when the first parameter is a `string`)</span></span> |
| `string.IndexOfAny` | <span data-ttu-id="fdae6-251">Liczba porządkowa</span><span class="sxs-lookup"><span data-stu-id="fdae6-251">Ordinal</span></span> | |
| `string.LastIndexOf` | <span data-ttu-id="fdae6-252">Liczba porządkowa</span><span class="sxs-lookup"><span data-stu-id="fdae6-252">Ordinal</span></span> | <span data-ttu-id="fdae6-253">(gdy pierwszy parametr to a `char` )</span><span class="sxs-lookup"><span data-stu-id="fdae6-253">(when the first parameter is a `char`)</span></span> |
| `string.LastIndexOf` | <span data-ttu-id="fdae6-254">CurrentCulture</span><span class="sxs-lookup"><span data-stu-id="fdae6-254">CurrentCulture</span></span> | <span data-ttu-id="fdae6-255">(gdy pierwszy parametr to a `string` )</span><span class="sxs-lookup"><span data-stu-id="fdae6-255">(when the first parameter is a `string`)</span></span> |
| `string.LastIndexOfAny` | <span data-ttu-id="fdae6-256">Liczba porządkowa</span><span class="sxs-lookup"><span data-stu-id="fdae6-256">Ordinal</span></span> | |
| `string.Replace` | <span data-ttu-id="fdae6-257">Liczba porządkowa</span><span class="sxs-lookup"><span data-stu-id="fdae6-257">Ordinal</span></span> | |
| `string.Split` | <span data-ttu-id="fdae6-258">Liczba porządkowa</span><span class="sxs-lookup"><span data-stu-id="fdae6-258">Ordinal</span></span> | |
| `string.StartsWith` | <span data-ttu-id="fdae6-259">Liczba porządkowa</span><span class="sxs-lookup"><span data-stu-id="fdae6-259">Ordinal</span></span> | <span data-ttu-id="fdae6-260">(gdy pierwszy parametr to a `char` )</span><span class="sxs-lookup"><span data-stu-id="fdae6-260">(when the first parameter is a `char`)</span></span> |
| `string.StartsWith` | <span data-ttu-id="fdae6-261">CurrentCulture</span><span class="sxs-lookup"><span data-stu-id="fdae6-261">CurrentCulture</span></span> | <span data-ttu-id="fdae6-262">(gdy pierwszy parametr to a `string` )</span><span class="sxs-lookup"><span data-stu-id="fdae6-262">(when the first parameter is a `string`)</span></span> |
| `string.ToLower` | <span data-ttu-id="fdae6-263">CurrentCulture</span><span class="sxs-lookup"><span data-stu-id="fdae6-263">CurrentCulture</span></span> | |
| `string.ToLowerInvariant` | <span data-ttu-id="fdae6-264">InvariantCulture</span><span class="sxs-lookup"><span data-stu-id="fdae6-264">InvariantCulture</span></span> | |
| `string.ToUpper` | <span data-ttu-id="fdae6-265">CurrentCulture</span><span class="sxs-lookup"><span data-stu-id="fdae6-265">CurrentCulture</span></span> | |
| `string.ToUpperInvariant` | <span data-ttu-id="fdae6-266">InvariantCulture</span><span class="sxs-lookup"><span data-stu-id="fdae6-266">InvariantCulture</span></span> | |
| `string.Trim` | <span data-ttu-id="fdae6-267">Liczba porządkowa</span><span class="sxs-lookup"><span data-stu-id="fdae6-267">Ordinal</span></span> | |
| `string.TrimEnd` | <span data-ttu-id="fdae6-268">Liczba porządkowa</span><span class="sxs-lookup"><span data-stu-id="fdae6-268">Ordinal</span></span> | |
| `string.TrimStart` | <span data-ttu-id="fdae6-269">Liczba porządkowa</span><span class="sxs-lookup"><span data-stu-id="fdae6-269">Ordinal</span></span> | |
| `string == string` | <span data-ttu-id="fdae6-270">Liczba porządkowa</span><span class="sxs-lookup"><span data-stu-id="fdae6-270">Ordinal</span></span> | |
| `string != string` | <span data-ttu-id="fdae6-271">Liczba porządkowa</span><span class="sxs-lookup"><span data-stu-id="fdae6-271">Ordinal</span></span> | |

<span data-ttu-id="fdae6-272">W przeciwieństwie do `string` interfejsów API, wszystkie `MemoryExtensions` interfejsy API domyślnie wykonują wyszukiwanie *porządkowe* i porównania z następującymi wyjątkami.</span><span class="sxs-lookup"><span data-stu-id="fdae6-272">Unlike `string` APIs, all `MemoryExtensions` APIs perform *Ordinal* searches and comparisons by default, with the following exceptions.</span></span>

| <span data-ttu-id="fdae6-273">interfejs API</span><span class="sxs-lookup"><span data-stu-id="fdae6-273">API</span></span> | <span data-ttu-id="fdae6-274">Zachowanie domyślne</span><span class="sxs-lookup"><span data-stu-id="fdae6-274">Default behavior</span></span> | <span data-ttu-id="fdae6-275">Uwagi</span><span class="sxs-lookup"><span data-stu-id="fdae6-275">Remarks</span></span> |
|---|---|---|
| `MemoryExtensions.ToLower` | <span data-ttu-id="fdae6-276">CurrentCulture</span><span class="sxs-lookup"><span data-stu-id="fdae6-276">CurrentCulture</span></span> | <span data-ttu-id="fdae6-277">(gdy przeszedł argument o wartości null `CultureInfo` )</span><span class="sxs-lookup"><span data-stu-id="fdae6-277">(when passed a null `CultureInfo` argument)</span></span> |
| `MemoryExtensions.ToLowerInvariant` | <span data-ttu-id="fdae6-278">InvariantCulture</span><span class="sxs-lookup"><span data-stu-id="fdae6-278">InvariantCulture</span></span> | |
| `MemoryExtensions.ToUpper` | <span data-ttu-id="fdae6-279">CurrentCulture</span><span class="sxs-lookup"><span data-stu-id="fdae6-279">CurrentCulture</span></span> | <span data-ttu-id="fdae6-280">(gdy przeszedł argument o wartości null `CultureInfo` )</span><span class="sxs-lookup"><span data-stu-id="fdae6-280">(when passed a null `CultureInfo` argument)</span></span> |
| `MemoryExtensions.ToUpperInvariant` | <span data-ttu-id="fdae6-281">InvariantCulture</span><span class="sxs-lookup"><span data-stu-id="fdae6-281">InvariantCulture</span></span> | |

<span data-ttu-id="fdae6-282">Jest to, że podczas konwertowania kodu z konsumowania `string` do konsumowania `ReadOnlySpan<char>` zmiany behawioralne mogą być wprowadzane przypadkowo.</span><span class="sxs-lookup"><span data-stu-id="fdae6-282">A consequence is that when converting code from consuming `string` to consuming `ReadOnlySpan<char>`, behavioral changes may be introduced inadvertently.</span></span> <span data-ttu-id="fdae6-283">Przykład poniżej.</span><span class="sxs-lookup"><span data-stu-id="fdae6-283">An example of this follows.</span></span>

```cs
string str = GetString();
if (str.StartsWith("Hello")) { /* do something */ } // this is a CULTURE-AWARE (linguistic) comparison

ReadOnlySpan<char> span = s.AsSpan();
if (span.StartsWith("Hello")) { /* do something */ } // this is an ORDINAL (non-linguistic) comparison
```

<span data-ttu-id="fdae6-284">Zalecanym sposobem na rozwiązanie tego jest przekazanie jawnego `StringComparison` parametru do tych interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="fdae6-284">The recommended way to address this is to pass an explicit `StringComparison` parameter to these APIs.</span></span> <span data-ttu-id="fdae6-285">Reguły analizy kodu CA1307 i CA1309 mogą pomóc w tym.</span><span class="sxs-lookup"><span data-stu-id="fdae6-285">The code analysis rules CA1307 and CA1309 can assist with this.</span></span>

```cs
string str = GetString();
if (str.StartsWith("Hello", StringComparison.Ordinal)) { /* do something */ } // ordinal comparison

ReadOnlySpan<char> span = s.AsSpan();
if (span.StartsWith("Hello", StringComparison.Ordinal)) { /* do something */ } // ordinal comparison
```

## <a name="see-also"></a><span data-ttu-id="fdae6-286">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="fdae6-286">See also</span></span>

- [<span data-ttu-id="fdae6-287">Zmiany dotyczące podziału globalizacji</span><span class="sxs-lookup"><span data-stu-id="fdae6-287">Globalization breaking changes</span></span>](../../core/compatibility/globalization.md)
- [<span data-ttu-id="fdae6-288">Najlepsze rozwiązania dotyczące porównywania ciągów w programie .NET</span><span class="sxs-lookup"><span data-stu-id="fdae6-288">Best practices for comparing strings in .NET</span></span>](best-practices-strings.md)
- [<span data-ttu-id="fdae6-289">Jak porównać ciągi w języku C #</span><span class="sxs-lookup"><span data-stu-id="fdae6-289">How to compare strings in C#</span></span>](../../csharp/how-to/compare-strings.md)
- [<span data-ttu-id="fdae6-290">Globalizacja i ICU platformy .NET</span><span class="sxs-lookup"><span data-stu-id="fdae6-290">.NET globalization and ICU</span></span>](../globalization-localization/globalization-icu.md)
- [<span data-ttu-id="fdae6-291">Liczba porządkowa a operacje na ciągach zależnych od kultury</span><span class="sxs-lookup"><span data-stu-id="fdae6-291">Ordinal vs. culture-sensitive string operations</span></span>](/dotnet/api/system.string#ordinal-vs-culture-sensitive-operations)
- [<span data-ttu-id="fdae6-292">Przegląd analizy kodu źródłowego platformy .NET</span><span class="sxs-lookup"><span data-stu-id="fdae6-292">Overview of .NET source code analysis</span></span>](../../fundamentals/code-analysis/overview.md)
