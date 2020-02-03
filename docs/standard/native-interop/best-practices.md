---
title: Najlepsze praktyki dotyczące natywnego współdziałania — platforma .NET
description: Poznaj najlepsze rozwiązania dotyczące współkorzystania ze składnikami macierzystymi w programie .NET.
ms.date: 01/18/2019
ms.openlocfilehash: 9486256b815856c0c283f5fe231be3d35d6e8f00
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/24/2020
ms.locfileid: "76742752"
---
# <a name="native-interoperability-best-practices"></a><span data-ttu-id="d5775-103">Najlepsze rozwiązania w zakresie współdziałania natywnego</span><span class="sxs-lookup"><span data-stu-id="d5775-103">Native interoperability best practices</span></span>

<span data-ttu-id="d5775-104">Program .NET oferuje różne sposoby dostosowywania natywnego kodu współdziałania.</span><span class="sxs-lookup"><span data-stu-id="d5775-104">.NET gives you a variety of ways to customize your native interoperability code.</span></span> <span data-ttu-id="d5775-105">Ten artykuł zawiera wskazówki, które są zgodne z zespołem .NET firmy Microsoft dotyczącym natywnej współdziałania.</span><span class="sxs-lookup"><span data-stu-id="d5775-105">This article includes the guidance that Microsoft's .NET teams follow for native interoperability.</span></span>

## <a name="general-guidance"></a><span data-ttu-id="d5775-106">Wskazówki ogólne</span><span class="sxs-lookup"><span data-stu-id="d5775-106">General guidance</span></span>

<span data-ttu-id="d5775-107">Wskazówki zawarte w tej sekcji dotyczą wszystkich scenariuszy międzyoperacyjnych.</span><span class="sxs-lookup"><span data-stu-id="d5775-107">The guidance in this section applies to all interop scenarios.</span></span>

- <span data-ttu-id="d5775-108">✔️ Użyj tej samej nazwy i wielkości liter dla metod i parametrów jako metody natywnej, którą chcesz wywołać.</span><span class="sxs-lookup"><span data-stu-id="d5775-108">✔️ DO use the same naming and capitalization for your methods and parameters as the native method you want to call.</span></span>
- <span data-ttu-id="d5775-109">✔️ ROZWAŻYĆ użycie tego samego nazewnictwa i wielkich liter w przypadku wartości stałych.</span><span class="sxs-lookup"><span data-stu-id="d5775-109">✔️ CONSIDER using the same naming and capitalization for constant values.</span></span>
- <span data-ttu-id="d5775-110">✔️ Użyj typów .NET, które są mapowane bliżej typu natywnego.</span><span class="sxs-lookup"><span data-stu-id="d5775-110">✔️ DO use .NET types that map closest to the native type.</span></span> <span data-ttu-id="d5775-111">Na przykład, w C#, użyj `uint`, gdy typ natywny jest `unsigned int`.</span><span class="sxs-lookup"><span data-stu-id="d5775-111">For example, in C#, use `uint` when the native type is `unsigned int`.</span></span>
- <span data-ttu-id="d5775-112">✔️ należy używać atrybutów `[In]` i `[Out]` tylko wtedy, gdy zachowanie ma być różne od zachowania domyślnego.</span><span class="sxs-lookup"><span data-stu-id="d5775-112">✔️ DO only use `[In]` and `[Out]` attributes when the behavior you want differs from the default behavior.</span></span>
- <span data-ttu-id="d5775-113">✔️ ROZWAŻYĆ użycie <xref:System.Buffers.ArrayPool%601?displayProperty=nameWithType> do puli natywnych buforów tablicowych.</span><span class="sxs-lookup"><span data-stu-id="d5775-113">✔️ CONSIDER using <xref:System.Buffers.ArrayPool%601?displayProperty=nameWithType> to pool your native array buffers.</span></span>
- <span data-ttu-id="d5775-114">✔️ Rozważ zapakowanie deklaracji P/Invoke w klasie o tej samej nazwie i wielkości liter jako biblioteki natywnej.</span><span class="sxs-lookup"><span data-stu-id="d5775-114">✔️ CONSIDER wrapping your P/Invoke declarations in a class with the same name and capitalization as your native library.</span></span>
  - <span data-ttu-id="d5775-115">Dzięki temu atrybuty `[DllImport]` mogą używać funkcji języka C# `nameof` do przekazywania nazwy biblioteki natywnej i upewnienia się, że nie jest ona błędną nazwą biblioteki natywnej.</span><span class="sxs-lookup"><span data-stu-id="d5775-115">This allows your `[DllImport]` attributes to use the C# `nameof` language feature to pass in the name of the native library and ensure that you didn't misspell the name of the native library.</span></span>

## <a name="dllimport-attribute-settings"></a><span data-ttu-id="d5775-116">Ustawienia atrybutów DllImport</span><span class="sxs-lookup"><span data-stu-id="d5775-116">DllImport attribute settings</span></span>

| <span data-ttu-id="d5775-117">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="d5775-117">Setting</span></span> | <span data-ttu-id="d5775-118">Domyślny</span><span class="sxs-lookup"><span data-stu-id="d5775-118">Default</span></span> | <span data-ttu-id="d5775-119">Zalecenie</span><span class="sxs-lookup"><span data-stu-id="d5775-119">Recommendation</span></span> | <span data-ttu-id="d5775-120">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="d5775-120">Details</span></span> |
|---------|---------|----------------|---------|
| <xref:System.Runtime.InteropServices.DllImportAttribute.PreserveSig>   | `true` |  <span data-ttu-id="d5775-121">Zachowaj domyślne</span><span class="sxs-lookup"><span data-stu-id="d5775-121">keep default</span></span>  | <span data-ttu-id="d5775-122">Jeśli ta opcja jest jawnie ustawiona na false, Niepowodzenie zwracanych wartości HRESULT spowoduje włączenie wyjątków (a wartość zwracana w definicji zmieni się na wartość null).</span><span class="sxs-lookup"><span data-stu-id="d5775-122">When this is explicitly set to false, failed HRESULT return values will be turned into exceptions (and the return value in the definition becomes null as a result).</span></span>|
| <xref:System.Runtime.InteropServices.DllImportAttribute.SetLastError> | `false`  | <span data-ttu-id="d5775-123">zależy od interfejsu API</span><span class="sxs-lookup"><span data-stu-id="d5775-123">depends on the API</span></span>  | <span data-ttu-id="d5775-124">Ustaw tę wartość na true, jeśli interfejs API używa wartości GetLastError i użyj Marshal. metodę GetLastWin32Error, aby pobrać wartość.</span><span class="sxs-lookup"><span data-stu-id="d5775-124">Set this to true if the API uses GetLastError and use Marshal.GetLastWin32Error to get the value.</span></span> <span data-ttu-id="d5775-125">Jeśli interfejs API ustawi warunek informujący o błędzie, należy uzyskać błąd przed wywołaniem innych wywołań, aby uniknąć niezamierzonego nadpisania.</span><span class="sxs-lookup"><span data-stu-id="d5775-125">If the API sets a condition that says it has an error, get the error before making other calls to avoid inadvertently having it overwritten.</span></span>|
| <xref:System.Runtime.InteropServices.DllImportAttribute.CharSet> | <span data-ttu-id="d5775-126">`CharSet.None`, które powracają do zachowania `CharSet.Ansi`</span><span class="sxs-lookup"><span data-stu-id="d5775-126">`CharSet.None`, which falls back to `CharSet.Ansi` behavior</span></span>  | <span data-ttu-id="d5775-127">Jawnie używaj `CharSet.Unicode` lub `CharSet.Ansi`, gdy ciągi lub znaki są obecne w definicji</span><span class="sxs-lookup"><span data-stu-id="d5775-127">Explicitly  use `CharSet.Unicode` or `CharSet.Ansi` when strings or characters are present in the definition</span></span> | <span data-ttu-id="d5775-128">Pozwala to na kierowanie zachowaniem ciągów i jakie `ExactSpelling` w przypadku `false`.</span><span class="sxs-lookup"><span data-stu-id="d5775-128">This specifies marshaling behavior of strings and what `ExactSpelling` does when `false`.</span></span> <span data-ttu-id="d5775-129">Należy pamiętać, że `CharSet.Ansi` jest w rzeczywistości UTF8 w systemie UNIX.</span><span class="sxs-lookup"><span data-stu-id="d5775-129">Note that `CharSet.Ansi` is actually UTF8 on Unix.</span></span> <span data-ttu-id="d5775-130">_Większość_ czasu Windows używa standardu Unicode, podczas gdy w systemie UNIX używa kodowania UTF8.</span><span class="sxs-lookup"><span data-stu-id="d5775-130">_Most_ of the time Windows uses Unicode while Unix uses UTF8.</span></span> <span data-ttu-id="d5775-131">Więcej informacji na temat zestawów [znaków](./charset.md)można znaleźć w dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="d5775-131">See more information on the [documentation on charsets](./charset.md).</span></span> |
| <xref:System.Runtime.InteropServices.DllImportAttribute.ExactSpelling> | `false` | `true`             | <span data-ttu-id="d5775-132">Ustaw tę wartość na true i uzyskaj niewielką korzyść w zakresie wydajności, ponieważ środowisko uruchomieniowe nie będzie szukać alternatywnych nazw funkcji z sufiksem "A" lub "W" w zależności od wartości ustawienia `CharSet` ("A" dla `CharSet.Ansi` i "W" dla `CharSet.Unicode`).</span><span class="sxs-lookup"><span data-stu-id="d5775-132">Set this to true and gain a slight perf benefit as the runtime will not look for alternate function names with either an "A" or "W" suffix depending on the value of the `CharSet` setting ("A" for `CharSet.Ansi` and "W" for `CharSet.Unicode`).</span></span> |

## <a name="string-parameters"></a><span data-ttu-id="d5775-133">Parametry ciągu</span><span class="sxs-lookup"><span data-stu-id="d5775-133">String parameters</span></span>

<span data-ttu-id="d5775-134">Gdy zestaw znaków jest Unicode lub argument jest jawnie oznaczony jako `[MarshalAs(UnmanagedType.LPWSTR)]` _i_ ciąg jest przenoszona przez wartość (nie `ref` lub `out`), ciąg zostanie przypięty i użyty bezpośrednio przez kod natywny (a nie skopiowany).</span><span class="sxs-lookup"><span data-stu-id="d5775-134">When the CharSet is Unicode or the argument is explicitly marked as `[MarshalAs(UnmanagedType.LPWSTR)]` _and_ the string is passed by value (not `ref` or `out`), the string will be pinned and used directly by native code (rather than copied).</span></span>

<span data-ttu-id="d5775-135">Pamiętaj, aby oznaczyć `[DllImport]` jako `Charset.Unicode`, chyba że jawnie ma być to zgodne z ANSI.</span><span class="sxs-lookup"><span data-stu-id="d5775-135">Remember to mark the `[DllImport]` as `Charset.Unicode` unless you explicitly want ANSI treatment of your strings.</span></span>

<span data-ttu-id="d5775-136">❌ nie używać `[Out] string` parametrów.</span><span class="sxs-lookup"><span data-stu-id="d5775-136">❌ DO NOT use `[Out] string` parameters.</span></span> <span data-ttu-id="d5775-137">Parametry ciągu przesłane przez wartość z atrybutem `[Out]` mogą destabilizację środowiska uruchomieniowego, jeśli ciąg jest ciągiem z stażystami.</span><span class="sxs-lookup"><span data-stu-id="d5775-137">String parameters passed by value with the `[Out]` attribute can destabilize the runtime if the string is an interned string.</span></span> <span data-ttu-id="d5775-138">Zobacz więcej informacji na temat sposobu informowania o ciągach w dokumentacji dotyczącej <xref:System.String.Intern%2A?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="d5775-138">See more information about string interning in the documentation for <xref:System.String.Intern%2A?displayProperty=nameWithType>.</span></span>

<span data-ttu-id="d5775-139">❌ uniknąć `StringBuilder` parametrów.</span><span class="sxs-lookup"><span data-stu-id="d5775-139">❌ AVOID `StringBuilder` parameters.</span></span> <span data-ttu-id="d5775-140">kierowanie `StringBuilder` *zawsze* tworzy natywną kopię buforu.</span><span class="sxs-lookup"><span data-stu-id="d5775-140">`StringBuilder` marshaling *always* creates a native buffer copy.</span></span> <span data-ttu-id="d5775-141">W związku z tym może być wyjątkowo niewydajne.</span><span class="sxs-lookup"><span data-stu-id="d5775-141">As such, it can be extremely inefficient.</span></span> <span data-ttu-id="d5775-142">Zapoznaj się z typowym scenariuszem wywoływania interfejsu API systemu Windows, który pobiera ciąg:</span><span class="sxs-lookup"><span data-stu-id="d5775-142">Take the typical scenario of calling a Windows API that takes a string:</span></span>

1. <span data-ttu-id="d5775-143">Utwórz SB o żądanej pojemności (przydzieli zarządzaną pojemność) **{1}**</span><span class="sxs-lookup"><span data-stu-id="d5775-143">Create a SB of the desired capacity (allocates managed capacity) **{1}**</span></span>
2. <span data-ttu-id="d5775-144">wywoływanie</span><span class="sxs-lookup"><span data-stu-id="d5775-144">Invoke</span></span>
   1. <span data-ttu-id="d5775-145">Przypisuje natywny bufor **{2}**</span><span class="sxs-lookup"><span data-stu-id="d5775-145">Allocates a native buffer **{2}**</span></span>
   2. <span data-ttu-id="d5775-146">Kopiuje zawartość, jeśli `[In]` _(wartość domyślna dla parametru `StringBuilder`)_</span><span class="sxs-lookup"><span data-stu-id="d5775-146">Copies the contents if `[In]` _(the default for a `StringBuilder` parameter)_</span></span>
   3. <span data-ttu-id="d5775-147">Kopiuje bufor macierzysty do nowo przydzielonej tablicy zarządzanej, jeśli `[Out]` **{3}** _(domyślnie `StringBuilder`)_</span><span class="sxs-lookup"><span data-stu-id="d5775-147">Copies the native buffer into a newly allocated managed array if `[Out]` **{3}** _(also the default for `StringBuilder`)_</span></span>
3. <span data-ttu-id="d5775-148">`ToString()` alokuje jeszcze inną zarządzaną tablicę **{4}**</span><span class="sxs-lookup"><span data-stu-id="d5775-148">`ToString()` allocates yet another managed array **{4}**</span></span>

<span data-ttu-id="d5775-149">Jest to *{4}* alokacji, aby uzyskać ciąg z kodu natywnego.</span><span class="sxs-lookup"><span data-stu-id="d5775-149">That is *{4}* allocations to get a string out of native code.</span></span> <span data-ttu-id="d5775-150">Najlepszym rozwiązaniem jest to, aby ograniczyć to użycie `StringBuilder` w innym wywołaniu, ale nadal tylko *1* przydział.</span><span class="sxs-lookup"><span data-stu-id="d5775-150">The best you can do to limit this is to reuse the `StringBuilder` in another call but this still only saves *1* allocation.</span></span> <span data-ttu-id="d5775-151">Znacznie lepiej jest używać pamięci podręcznej i bufora znaków z `ArrayPool`— możesz następnie uzyskać dostęp do przydziału dla `ToString()` przy kolejnych wywołaniach.</span><span class="sxs-lookup"><span data-stu-id="d5775-151">It's much better to use and cache a character buffer from `ArrayPool`- you can then get down to just the allocation for the `ToString()` on subsequent calls.</span></span>

<span data-ttu-id="d5775-152">Innym problemem związanym z `StringBuilder` jest to, że zawsze kopiuje kopię zapasową buforu powrotu do pierwszej wartości null.</span><span class="sxs-lookup"><span data-stu-id="d5775-152">The other issue with `StringBuilder` is that it always copies the return buffer back up to the first null.</span></span> <span data-ttu-id="d5775-153">Jeśli przeszedł ciąg zakończony nieprzerwanie lub jest ciągiem o podwójnej wartości null, element P/Invoke jest niewłaściwy.</span><span class="sxs-lookup"><span data-stu-id="d5775-153">If the passed back string isn't terminated or is a double-null-terminated string, your P/Invoke is incorrect at best.</span></span>

<span data-ttu-id="d5775-154">Jeśli używasz *`StringBuilder`* , Gotcha, że pojemność nie obejmuje ukrytych wartości null, które zawsze **są uwzględniane w** przypadku współdziałania.</span><span class="sxs-lookup"><span data-stu-id="d5775-154">If you *do* use `StringBuilder`, one last gotcha is that the capacity does **not** include a hidden null, which is always accounted for in interop.</span></span> <span data-ttu-id="d5775-155">Jest to często używane w przypadku, gdy większość interfejsów API ma rozmiar buforu, *łącznie* z wartością null.</span><span class="sxs-lookup"><span data-stu-id="d5775-155">It's common for people to get this wrong as most APIs want the size of the buffer *including* the null.</span></span> <span data-ttu-id="d5775-156">Może to spowodować marnowanie/niepotrzebne alokacje.</span><span class="sxs-lookup"><span data-stu-id="d5775-156">This can result in wasted/unnecessary allocations.</span></span> <span data-ttu-id="d5775-157">Ponadto ta Gotcha uniemożliwia środowisko uruchomieniowe przed optymalizacją `StringBuilder` organizowania, aby zminimalizować kopie.</span><span class="sxs-lookup"><span data-stu-id="d5775-157">Additionally, this gotcha prevents the runtime from optimizing `StringBuilder` marshaling to minimize copies.</span></span>

<span data-ttu-id="d5775-158">✔️ ROZWAŻYĆ użycie `char[]`s z `ArrayPool`.</span><span class="sxs-lookup"><span data-stu-id="d5775-158">✔️ CONSIDER using `char[]`s from an `ArrayPool`.</span></span>

<span data-ttu-id="d5775-159">Aby uzyskać więcej informacji na temat organizowania ciągów, zobacz [domyślne kierowanie dla ciągów](../../framework/interop/default-marshaling-for-strings.md) i [Dostosowywanie organizowania ciągów](customize-parameter-marshaling.md#customizing-string-parameters).</span><span class="sxs-lookup"><span data-stu-id="d5775-159">For more information on string marshaling, see [Default Marshaling for Strings](../../framework/interop/default-marshaling-for-strings.md) and [Customizing string marshaling](customize-parameter-marshaling.md#customizing-string-parameters).</span></span>

> <span data-ttu-id="d5775-160">__Specyficzne dla systemu Windows__ W przypadku ciągów `[Out]` CLR będzie używać `CoTaskMemFree` domyślnie do zwalniania ciągów lub `SysStringFree` dla ciągów, które są oznaczone jako `UnmanagedType.BSTR`.</span><span class="sxs-lookup"><span data-stu-id="d5775-160">__Windows Specific__ For `[Out]` strings the CLR will use `CoTaskMemFree` by default to free strings or `SysStringFree` for strings that are marked as `UnmanagedType.BSTR`.</span></span>
> <span data-ttu-id="d5775-161">**W przypadku większości interfejsów API z buforem ciągu wyjściowego:** Liczba przesłanych znaków musi zawierać wartość null.</span><span class="sxs-lookup"><span data-stu-id="d5775-161">**For most APIs with an output string buffer:** The passed in character count must include the null.</span></span> <span data-ttu-id="d5775-162">Jeśli zwracana wartość jest mniejsza niż przekazana liczba znaków, wywołanie zakończyło się pomyślnie, a wartość jest liczbą znaków *bez* końcowej wartości null.</span><span class="sxs-lookup"><span data-stu-id="d5775-162">If the returned value is less than the passed in character count the call has succeeded and the value is the number of characters *without* the trailing null.</span></span> <span data-ttu-id="d5775-163">W przeciwnym razie liczba jest wymaganym rozmiarem bufora, w *tym* znakiem null.</span><span class="sxs-lookup"><span data-stu-id="d5775-163">Otherwise the count is the required size of the buffer *including* the null character.</span></span>
>
> - <span data-ttu-id="d5775-164">Przekaż 5, Pobierz 4: ciąg zawiera 4 znaki o długości końcowej null.</span><span class="sxs-lookup"><span data-stu-id="d5775-164">Pass in 5, get 4: The string is 4 characters long with a trailing null.</span></span>
> - <span data-ttu-id="d5775-165">Przekaż 5, get 6: ciąg ma długość 5 znaków, do przechowywania wartości null potrzebny jest rozmiar buforu znaków.</span><span class="sxs-lookup"><span data-stu-id="d5775-165">Pass in 5, get 6: The string is 5 characters long, need a 6 character buffer to hold the null.</span></span>
> [<span data-ttu-id="d5775-166">Typy danych systemu Windows dla ciągów</span><span class="sxs-lookup"><span data-stu-id="d5775-166">Windows Data Types for Strings</span></span>](/windows/desktop/Intl/windows-data-types-for-strings)

## <a name="boolean-parameters-and-fields"></a><span data-ttu-id="d5775-167">Parametry i pola logiczne</span><span class="sxs-lookup"><span data-stu-id="d5775-167">Boolean parameters and fields</span></span>

<span data-ttu-id="d5775-168">Wartości logiczne są łatwe w obsłudze.</span><span class="sxs-lookup"><span data-stu-id="d5775-168">Booleans are easy to mess up.</span></span> <span data-ttu-id="d5775-169">Domyślnie program .NET `bool` jest kierowany do `BOOL`systemu Windows, gdzie jest wartością 4-bajtową.</span><span class="sxs-lookup"><span data-stu-id="d5775-169">By default, a .NET `bool` is marshaled to a Windows `BOOL`, where it's a 4-byte value.</span></span> <span data-ttu-id="d5775-170">Jednak `_Bool`i typy `bool` w C i C++ są *pojedynczym* bajtem.</span><span class="sxs-lookup"><span data-stu-id="d5775-170">However, the `_Bool`, and `bool` types in C and C++ are a *single* byte.</span></span> <span data-ttu-id="d5775-171">Może to prowadzić do trudnej śledzenia błędów w postaci połowy wartości zwracanej zostanie odrzucone, co *spowoduje jedynie zmianę* wyniku.</span><span class="sxs-lookup"><span data-stu-id="d5775-171">This can lead to hard to track down bugs as half the return value will be discarded, which will only *potentially* change the result.</span></span> <span data-ttu-id="d5775-172">Aby uzyskać więcej informacji o kierowaniu wartości `bool` .NET do typów C C++ lub `bool`, zobacz dokumentację dotyczącą [dostosowywania kierowania pól logicznych](customize-struct-marshaling.md#customizing-boolean-field-marshaling).</span><span class="sxs-lookup"><span data-stu-id="d5775-172">For more for information on marshaling .NET `bool` values to C or C++ `bool` types, see the documentation on [customizing boolean field marshaling](customize-struct-marshaling.md#customizing-boolean-field-marshaling).</span></span>

## <a name="guids"></a><span data-ttu-id="d5775-173">Identyfikatory GUID</span><span class="sxs-lookup"><span data-stu-id="d5775-173">GUIDs</span></span>

<span data-ttu-id="d5775-174">Identyfikatory GUID można używać bezpośrednio w sygnaturach.</span><span class="sxs-lookup"><span data-stu-id="d5775-174">GUIDs are usable directly in signatures.</span></span> <span data-ttu-id="d5775-175">Wiele interfejsów API systemu Windows przyjmuje aliasy typu `GUID&`, takie jak `REFIID`.</span><span class="sxs-lookup"><span data-stu-id="d5775-175">Many Windows APIs take `GUID&` type aliases like `REFIID`.</span></span> <span data-ttu-id="d5775-176">Gdy są przesyłane przez odwołanie, mogą być przesyłane przez `ref` lub z atrybutem `[MarshalAs(UnmanagedType.LPStruct)]`.</span><span class="sxs-lookup"><span data-stu-id="d5775-176">When passed by ref, they can either be passed by `ref` or with the `[MarshalAs(UnmanagedType.LPStruct)]` attribute.</span></span>

| <span data-ttu-id="d5775-177">Identyfikator GUID</span><span class="sxs-lookup"><span data-stu-id="d5775-177">GUID</span></span> | <span data-ttu-id="d5775-178">Według-ref — identyfikator GUID</span><span class="sxs-lookup"><span data-stu-id="d5775-178">By-ref GUID</span></span> |
|------|-------------|
| `KNOWNFOLDERID` | `REFKNOWNFOLDERID` |

<span data-ttu-id="d5775-179">❌ nie należy używać `[MarshalAs(UnmanagedType.LPStruct)]` dla elementów innych niż `ref` parametrów GUID.</span><span class="sxs-lookup"><span data-stu-id="d5775-179">❌ DO NOT Use `[MarshalAs(UnmanagedType.LPStruct)]` for anything other than `ref` GUID parameters.</span></span>

## <a name="blittable-types"></a><span data-ttu-id="d5775-180">Typy danych kopiowalnych</span><span class="sxs-lookup"><span data-stu-id="d5775-180">Blittable types</span></span>

<span data-ttu-id="d5775-181">Typy danych kopiowalnych są typami, które mają taką samą reprezentację na poziomie bitowym w kodzie zarządzanym i natywnym.</span><span class="sxs-lookup"><span data-stu-id="d5775-181">Blittable types are types that have the same bit-level representation in managed and native code.</span></span> <span data-ttu-id="d5775-182">W związku z tym nie trzeba przekonwertowane do innego formatu, który ma być zorganizowany do i z kodu natywnego, a w miarę zwiększania wydajności powinny one być preferowane.</span><span class="sxs-lookup"><span data-stu-id="d5775-182">As such they do not need to be converted to another format to be marshaled to and from native code, and as this improves performance they should be preferred.</span></span>

<span data-ttu-id="d5775-183">**Typy danych kopiowalnych:**</span><span class="sxs-lookup"><span data-stu-id="d5775-183">**Blittable types:**</span></span>

- <span data-ttu-id="d5775-184">`byte`, `sbyte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `single`, `double`</span><span class="sxs-lookup"><span data-stu-id="d5775-184">`byte`, `sbyte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `single`, `double`</span></span>
- <span data-ttu-id="d5775-185">niezagnieżdżone tablice jednowymiarowe typów danych kopiowalnych (na przykład `int[]`)</span><span class="sxs-lookup"><span data-stu-id="d5775-185">non-nested one-dimensional arrays of blittable types (for example, `int[]`)</span></span>
- <span data-ttu-id="d5775-186">struktury i klasy ze stałym układem, które mają tylko typy wartości danych kopiowalnych dla pól wystąpień</span><span class="sxs-lookup"><span data-stu-id="d5775-186">structs and classes with fixed layout that only have blittable value types for instance fields</span></span>
  - <span data-ttu-id="d5775-187">stały układ wymaga `[StructLayout(LayoutKind.Sequential)]` lub `[StructLayout(LayoutKind.Explicit)]`</span><span class="sxs-lookup"><span data-stu-id="d5775-187">fixed layout requires `[StructLayout(LayoutKind.Sequential)]` or `[StructLayout(LayoutKind.Explicit)]`</span></span>
  - <span data-ttu-id="d5775-188">struktury są domyślnie `LayoutKind.Sequential`, klasy są `LayoutKind.Auto`</span><span class="sxs-lookup"><span data-stu-id="d5775-188">structs are `LayoutKind.Sequential` by default, classes are `LayoutKind.Auto`</span></span>

<span data-ttu-id="d5775-189">**NIE danych kopiowalnych:**</span><span class="sxs-lookup"><span data-stu-id="d5775-189">**NOT blittable:**</span></span>

- `bool`

<span data-ttu-id="d5775-190">**Czasami danych kopiowalnych:**</span><span class="sxs-lookup"><span data-stu-id="d5775-190">**SOMETIMES blittable:**</span></span>

- <span data-ttu-id="d5775-191">`char`, `string`</span><span class="sxs-lookup"><span data-stu-id="d5775-191">`char`, `string`</span></span>

<span data-ttu-id="d5775-192">Gdy typy danych kopiowalnych są przesyłane przez odwołanie, są one po prostu przypięte przez organizatora, zamiast kopiować do buforu pośredniego.</span><span class="sxs-lookup"><span data-stu-id="d5775-192">When blittable types are passed by reference, they're simply pinned by the marshaller instead of being copied to an intermediate buffer.</span></span> <span data-ttu-id="d5775-193">(Klasy są z założenia przesyłane przez odwołanie, struktury są przesyłane przez odwołanie, gdy są używane z `ref` lub `out`.)</span><span class="sxs-lookup"><span data-stu-id="d5775-193">(Classes are inherently passed by reference, structs are passed by reference when used with `ref` or `out`.)</span></span>

<span data-ttu-id="d5775-194">`char` jest danych kopiowalnych w tablicy jednowymiarowej **lub** , jeśli jest częścią typu, który zawiera go jawnie oznaczone `[StructLayout]` z `CharSet = CharSet.Unicode`.</span><span class="sxs-lookup"><span data-stu-id="d5775-194">`char` is blittable in a one-dimensional array **or** if it's part of a type that contains it's explicitly marked with `[StructLayout]` with `CharSet = CharSet.Unicode`.</span></span>

```csharp
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Unicode)]
public struct UnicodeCharStruct
{
    public char c;
}
```

<span data-ttu-id="d5775-195">`string` jest danych kopiowalnych, jeśli nie jest zawarty w innym typie i jest przenoszona jako argument, który jest oznaczony za pomocą `[MarshalAs(UnmanagedType.LPWStr)]` lub `[DllImport]` ma `CharSet = CharSet.Unicode` ustawiony.</span><span class="sxs-lookup"><span data-stu-id="d5775-195">`string` is blittable if it isn't contained in another type and it's being passed as an argument that is marked with `[MarshalAs(UnmanagedType.LPWStr)]` or the `[DllImport]` has `CharSet = CharSet.Unicode` set.</span></span>

<span data-ttu-id="d5775-196">Możesz sprawdzić, czy typ to danych kopiowalnych, próbując utworzyć przypiętą `GCHandle`.</span><span class="sxs-lookup"><span data-stu-id="d5775-196">You can see if a type is blittable by attempting to create a pinned `GCHandle`.</span></span> <span data-ttu-id="d5775-197">Jeśli typ nie jest ciągiem lub jest traktowany jako danych kopiowalnych, `GCHandle.Alloc` generuje `ArgumentException`.</span><span class="sxs-lookup"><span data-stu-id="d5775-197">If the type isn't a string or considered blittable, `GCHandle.Alloc` will throw an `ArgumentException`.</span></span>

<span data-ttu-id="d5775-198">✔️, gdy to możliwe, danych kopiowalnych struktury.</span><span class="sxs-lookup"><span data-stu-id="d5775-198">✔️ DO make your structures blittable when possible.</span></span>

<span data-ttu-id="d5775-199">Aby uzyskać więcej informacji, zobacz:</span><span class="sxs-lookup"><span data-stu-id="d5775-199">For more information, see:</span></span>

- [<span data-ttu-id="d5775-200">Typy kopiowalne i niekopiowalne</span><span class="sxs-lookup"><span data-stu-id="d5775-200">Blittable and Non-Blittable Types</span></span>](../../framework/interop/blittable-and-non-blittable-types.md)
- [<span data-ttu-id="d5775-201">Kierowanie typów</span><span class="sxs-lookup"><span data-stu-id="d5775-201">Type Marshaling</span></span>](type-marshaling.md)

## <a name="keeping-managed-objects-alive"></a><span data-ttu-id="d5775-202">Utrzymywanie aktywności obiektów zarządzanych</span><span class="sxs-lookup"><span data-stu-id="d5775-202">Keeping managed objects alive</span></span>

<span data-ttu-id="d5775-203">`GC.KeepAlive()` sprawdzi, czy obiekt pozostaje w zakresie, dopóki nie zostanie osiągnięta Metoda utrzymywania aktywności.</span><span class="sxs-lookup"><span data-stu-id="d5775-203">`GC.KeepAlive()` will ensure an object stays in scope until the KeepAlive method is hit.</span></span>

<span data-ttu-id="d5775-204">[`HandleRef`](xref:System.Runtime.InteropServices.HandleRef) umożliwia Organizatorowi utrzymywanie obiektu na czas trwania elementu P/Invoke.</span><span class="sxs-lookup"><span data-stu-id="d5775-204">[`HandleRef`](xref:System.Runtime.InteropServices.HandleRef) allows the marshaller to keep an object alive for the duration of a P/Invoke.</span></span> <span data-ttu-id="d5775-205">Można go użyć zamiast `IntPtr` w sygnaturach metod.</span><span class="sxs-lookup"><span data-stu-id="d5775-205">It can be used instead of `IntPtr` in method signatures.</span></span> <span data-ttu-id="d5775-206">`SafeHandle` efektywnie zamienia tę klasę i powinna być używana zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="d5775-206">`SafeHandle` effectively replaces this class and should be used instead.</span></span>

<span data-ttu-id="d5775-207">[`GCHandle`](xref:System.Runtime.InteropServices.GCHandle) umożliwia Przypinanie obiektu zarządzanego i uzyskanie wskaźnika natywnego do niego.</span><span class="sxs-lookup"><span data-stu-id="d5775-207">[`GCHandle`](xref:System.Runtime.InteropServices.GCHandle) allows pinning a managed object and getting the native pointer to it.</span></span> <span data-ttu-id="d5775-208">Wzorzec podstawowy to:</span><span class="sxs-lookup"><span data-stu-id="d5775-208">The basic pattern is:</span></span>

```csharp
GCHandle handle = GCHandle.Alloc(obj, GCHandleType.Pinned);
IntPtr ptr = handle.AddrOfPinnedObject();
handle.Free();
```

<span data-ttu-id="d5775-209">Przypinanie nie jest domyślne dla `GCHandle`.</span><span class="sxs-lookup"><span data-stu-id="d5775-209">Pinning isn't the default for `GCHandle`.</span></span> <span data-ttu-id="d5775-210">Inny wzorzec główny polega na przekazaniu odwołania do zarządzanego obiektu za pomocą kodu natywnego i z powrotem do kodu zarządzanego, zazwyczaj przy użyciu wywołania zwrotnego.</span><span class="sxs-lookup"><span data-stu-id="d5775-210">The other major pattern is for passing a reference to a managed object through native code and back to managed code, usually with a callback.</span></span> <span data-ttu-id="d5775-211">Oto wzorzec:</span><span class="sxs-lookup"><span data-stu-id="d5775-211">Here is the pattern:</span></span>

```csharp
GCHandle handle = GCHandle.Alloc(obj);
SomeNativeEnumerator(callbackDelegate, GCHandle.ToIntPtr(handle));

// In the callback
GCHandle handle = GCHandle.FromIntPtr(param);
object managedObject = handle.Target;

// After the last callback
handle.Free();
```

<span data-ttu-id="d5775-212">Nie zapomnij, że `GCHandle` muszą być jawnie zwolnione, aby uniknąć przecieków pamięci.</span><span class="sxs-lookup"><span data-stu-id="d5775-212">Don't forget that `GCHandle` needs to be explicitly freed to avoid memory leaks.</span></span>

## <a name="common-windows-data-types"></a><span data-ttu-id="d5775-213">Typowe typy danych systemu Windows</span><span class="sxs-lookup"><span data-stu-id="d5775-213">Common Windows data types</span></span>

<span data-ttu-id="d5775-214">Poniżej znajduje się lista typów danych używanych w interfejsach API systemu Windows, C# które mają być używane podczas wywoływania kodu systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="d5775-214">Here is a list of data types commonly used in Windows APIs and which C# types to use when calling into the Windows code.</span></span>

<span data-ttu-id="d5775-215">Następujące typy są takie same, jak w przypadku systemu Windows 32-bitowego i 64-bitowego, niezależnie od ich nazw.</span><span class="sxs-lookup"><span data-stu-id="d5775-215">The following types are the same size on 32-bit and 64-bit Windows, despite their names.</span></span>

| <span data-ttu-id="d5775-216">Szerokość</span><span class="sxs-lookup"><span data-stu-id="d5775-216">Width</span></span> | <span data-ttu-id="d5775-217">Windows</span><span class="sxs-lookup"><span data-stu-id="d5775-217">Windows</span></span>          | <span data-ttu-id="d5775-218">C (Windows)</span><span class="sxs-lookup"><span data-stu-id="d5775-218">C (Windows)</span></span>          | <span data-ttu-id="d5775-219">C#</span><span class="sxs-lookup"><span data-stu-id="d5775-219">C#</span></span>       | <span data-ttu-id="d5775-220">Różne</span><span class="sxs-lookup"><span data-stu-id="d5775-220">Alternative</span></span>                          |
|:------|:-----------------|:---------------------|:---------|:-------------------------------------|
| <span data-ttu-id="d5775-221">32</span><span class="sxs-lookup"><span data-stu-id="d5775-221">32</span></span>    | `BOOL`           | `int`                | `int`    | `bool`                               |
| <span data-ttu-id="d5775-222">8</span><span class="sxs-lookup"><span data-stu-id="d5775-222">8</span></span>     | `BOOLEAN`        | `unsigned char`      | `byte`   | `[MarshalAs(UnmanagedType.U1)] bool` |
| <span data-ttu-id="d5775-223">8</span><span class="sxs-lookup"><span data-stu-id="d5775-223">8</span></span>     | `BYTE`           | `unsigned char`      | `byte`   |                                      |
| <span data-ttu-id="d5775-224">8</span><span class="sxs-lookup"><span data-stu-id="d5775-224">8</span></span>     | `CHAR`           | `char`               | `sbyte`  |                                      |
| <span data-ttu-id="d5775-225">8</span><span class="sxs-lookup"><span data-stu-id="d5775-225">8</span></span>     | `UCHAR`          | `unsigned char`      | `byte`   |                                      |
| <span data-ttu-id="d5775-226">16</span><span class="sxs-lookup"><span data-stu-id="d5775-226">16</span></span>    | `SHORT`          | `short`              | `short`  |                                      |
| <span data-ttu-id="d5775-227">16</span><span class="sxs-lookup"><span data-stu-id="d5775-227">16</span></span>    | `CSHORT`         | `short`              | `short`  |                                      |
| <span data-ttu-id="d5775-228">16</span><span class="sxs-lookup"><span data-stu-id="d5775-228">16</span></span>    | `USHORT`         | `unsigned short`     | `ushort` |                                      |
| <span data-ttu-id="d5775-229">16</span><span class="sxs-lookup"><span data-stu-id="d5775-229">16</span></span>    | `WORD`           | `unsigned short`     | `ushort` |                                      |
| <span data-ttu-id="d5775-230">16</span><span class="sxs-lookup"><span data-stu-id="d5775-230">16</span></span>    | `ATOM`           | `unsigned short`     | `ushort` |                                      |
| <span data-ttu-id="d5775-231">32</span><span class="sxs-lookup"><span data-stu-id="d5775-231">32</span></span>    | `INT`            | `int`                | `int`    |                                      |
| <span data-ttu-id="d5775-232">32</span><span class="sxs-lookup"><span data-stu-id="d5775-232">32</span></span>    | `LONG`           | `long`               | `int`    |                                      |
| <span data-ttu-id="d5775-233">32</span><span class="sxs-lookup"><span data-stu-id="d5775-233">32</span></span>    | `ULONG`          | `unsigned long`      | `uint`   |                                      |
| <span data-ttu-id="d5775-234">32</span><span class="sxs-lookup"><span data-stu-id="d5775-234">32</span></span>    | `DWORD`          | `unsigned long`      | `uint`   |                                      |
| <span data-ttu-id="d5775-235">64</span><span class="sxs-lookup"><span data-stu-id="d5775-235">64</span></span>    | `QWORD`          | `long long`          | `long`   |                                      |
| <span data-ttu-id="d5775-236">64</span><span class="sxs-lookup"><span data-stu-id="d5775-236">64</span></span>    | `LARGE_INTEGER`  | `long long`          | `long`   |                                      |
| <span data-ttu-id="d5775-237">64</span><span class="sxs-lookup"><span data-stu-id="d5775-237">64</span></span>    | `LONGLONG`       | `long long`          | `long`   |                                      |
| <span data-ttu-id="d5775-238">64</span><span class="sxs-lookup"><span data-stu-id="d5775-238">64</span></span>    | `ULONGLONG`      | `unsigned long long` | `ulong`  |                                      |
| <span data-ttu-id="d5775-239">64</span><span class="sxs-lookup"><span data-stu-id="d5775-239">64</span></span>    | `ULARGE_INTEGER` | `unsigned long long` | `ulong`  |                                      |
| <span data-ttu-id="d5775-240">32</span><span class="sxs-lookup"><span data-stu-id="d5775-240">32</span></span>    | `HRESULT`        | `long`               | `int`    |                                      |
| <span data-ttu-id="d5775-241">32</span><span class="sxs-lookup"><span data-stu-id="d5775-241">32</span></span>    | `NTSTATUS`       | `long`               | `int`    |                                      |

<span data-ttu-id="d5775-242">Następujące typy, które są wskaźnikami, są zgodne z szerokością platformy.</span><span class="sxs-lookup"><span data-stu-id="d5775-242">The following types, being pointers, do follow the width of the platform.</span></span> <span data-ttu-id="d5775-243">Użyj `IntPtr`/`UIntPtr`.</span><span class="sxs-lookup"><span data-stu-id="d5775-243">Use `IntPtr`/`UIntPtr` for these.</span></span>

| <span data-ttu-id="d5775-244">Typy wskaźników ze znakiem (Użyj `IntPtr`)</span><span class="sxs-lookup"><span data-stu-id="d5775-244">Signed Pointer Types (use `IntPtr`)</span></span> | <span data-ttu-id="d5775-245">Niepodpisane typy wskaźnika (Użyj `UIntPtr`)</span><span class="sxs-lookup"><span data-stu-id="d5775-245">Unsigned Pointer Types (use `UIntPtr`)</span></span> |
|:------------------------------------|:---------------------------------------|
| `HANDLE`                            | `WPARAM`                               |
| `HWND`                              | `UINT_PTR`                             |
| `HINSTANCE`                         | `ULONG_PTR`                            |
| `LPARAM`                            | `SIZE_T`                               |
| `LRESULT`                           |                                        |
| `LONG_PTR`                          |                                        |
| `INT_PTR`                           |                                        |

<span data-ttu-id="d5775-246">`PVOID` systemu Windows, który jest `void*` C może być zorganizowany jako `IntPtr` lub `UIntPtr`, ale preferowany `void*`, gdy jest to możliwe.</span><span class="sxs-lookup"><span data-stu-id="d5775-246">A Windows `PVOID` which is a C `void*` can be marshaled as either `IntPtr` or `UIntPtr`, but prefer `void*` when possible.</span></span>

[<span data-ttu-id="d5775-247">Typy danych systemu Windows</span><span class="sxs-lookup"><span data-stu-id="d5775-247">Windows Data Types</span></span>](/windows/desktop/WinProg/windows-data-types)

[<span data-ttu-id="d5775-248">Zakresy typu danych</span><span class="sxs-lookup"><span data-stu-id="d5775-248">Data Type Ranges</span></span>](/cpp/cpp/data-type-ranges)

## <a name="structs"></a><span data-ttu-id="d5775-249">Struktury</span><span class="sxs-lookup"><span data-stu-id="d5775-249">Structs</span></span>

<span data-ttu-id="d5775-250">Zarządzane struktury są tworzone na stosie i nie są usuwane, dopóki metoda nie zwróci metody.</span><span class="sxs-lookup"><span data-stu-id="d5775-250">Managed structs are created on the stack and aren't removed until the method returns.</span></span> <span data-ttu-id="d5775-251">Według definicji są one "przypięte" (nie są przenoszone przez wykaz globalny).</span><span class="sxs-lookup"><span data-stu-id="d5775-251">By definition then, they are "pinned" (it won't get moved by the GC).</span></span> <span data-ttu-id="d5775-252">Można również po prostu przełączyć adres w niebezpieczny blok kodu, jeśli kod natywny nie będzie używać wskaźnika poza końcem bieżącej metody.</span><span class="sxs-lookup"><span data-stu-id="d5775-252">You can also simply take the address in unsafe code blocks if native code won't use the pointer past the end of the current method.</span></span>

<span data-ttu-id="d5775-253">Struktury danych kopiowalnych są znacznie bardziej wydajne, ponieważ mogą być używane bezpośrednio przez warstwę kierującą.</span><span class="sxs-lookup"><span data-stu-id="d5775-253">Blittable structs are much more performant as they can simply be used directly by the marshaling layer.</span></span> <span data-ttu-id="d5775-254">Spróbuj utworzyć struktury danych kopiowalnych (na przykład unikać `bool`).</span><span class="sxs-lookup"><span data-stu-id="d5775-254">Try to make structs blittable (for example, avoid `bool`).</span></span> <span data-ttu-id="d5775-255">Aby uzyskać więcej informacji, zobacz sekcję [typy danych kopiowalnych](#blittable-types) .</span><span class="sxs-lookup"><span data-stu-id="d5775-255">For more information, see the [Blittable Types](#blittable-types) section.</span></span>

<span data-ttu-id="d5775-256">*Jeśli* struktura jest danych kopiowalnych, użyj `sizeof()` zamiast `Marshal.SizeOf<MyStruct>()` w celu uzyskania lepszej wydajności.</span><span class="sxs-lookup"><span data-stu-id="d5775-256">*If* the struct is blittable, use `sizeof()` instead of `Marshal.SizeOf<MyStruct>()` for better performance.</span></span> <span data-ttu-id="d5775-257">Jak wspomniano powyżej, można sprawdzić, czy typ to danych kopiowalnych, próbując utworzyć przypiętą `GCHandle`.</span><span class="sxs-lookup"><span data-stu-id="d5775-257">As mentioned above, you can validate that the type is blittable by attempting to create a pinned `GCHandle`.</span></span> <span data-ttu-id="d5775-258">Jeśli typ nie jest ciągiem lub uznano za danych kopiowalnych, `GCHandle.Alloc` generuje `ArgumentException`.</span><span class="sxs-lookup"><span data-stu-id="d5775-258">If the type is not a string or considered blittable, `GCHandle.Alloc` will throw an `ArgumentException`.</span></span>

<span data-ttu-id="d5775-259">Wskaźniki do struktur w definicjach muszą być przesyłane przez `ref` lub używać `unsafe` i `*`.</span><span class="sxs-lookup"><span data-stu-id="d5775-259">Pointers to structs in definitions must either be passed by `ref` or use `unsafe` and `*`.</span></span>

<span data-ttu-id="d5775-260">✔️ być zgodna z zarządzaną strukturą jak najbliżej kształtu i nazw, które są używane w oficjalnej dokumentacji lub nagłówku platformy.</span><span class="sxs-lookup"><span data-stu-id="d5775-260">✔️ DO match the managed struct as closely as possible to the shape and names that are used in the official platform documentation or header.</span></span>

<span data-ttu-id="d5775-261">Aby zwiększyć wydajność, C# ✔️ używać `sizeof()` zamiast `Marshal.SizeOf<MyStruct>()` dla struktur danych kopiowalnych.</span><span class="sxs-lookup"><span data-stu-id="d5775-261">✔️ DO use the C# `sizeof()` instead of `Marshal.SizeOf<MyStruct>()` for blittable structures to improve performance.</span></span>

<span data-ttu-id="d5775-262">Tablica, taka jak `INT_PTR Reserved1[2]`, musi być organizowana do dwóch `IntPtr` pól, `Reserved1a` i `Reserved1b`.</span><span class="sxs-lookup"><span data-stu-id="d5775-262">An array like `INT_PTR Reserved1[2]` has to be marshaled to two `IntPtr` fields, `Reserved1a` and `Reserved1b`.</span></span> <span data-ttu-id="d5775-263">Gdy natywna tablica jest typem pierwotnym, możemy użyć słowa kluczowego `fixed`, aby napisać je nieco bardziej czysty.</span><span class="sxs-lookup"><span data-stu-id="d5775-263">When the native array is a primitive type, we can use the `fixed` keyword to write it a little more cleanly.</span></span> <span data-ttu-id="d5775-264">Na przykład `SYSTEM_PROCESS_INFORMATION` wygląda następująco w nagłówku natywnym:</span><span class="sxs-lookup"><span data-stu-id="d5775-264">For example, `SYSTEM_PROCESS_INFORMATION` looks like this in the native header:</span></span>

```c
typedef struct _SYSTEM_PROCESS_INFORMATION {
    ULONG NextEntryOffset;
    ULONG NumberOfThreads;
    BYTE Reserved1[48];
    UNICODE_STRING ImageName;
...
} SYSTEM_PROCESS_INFORMATION
```

<span data-ttu-id="d5775-265">W C#programie możemy napisać następujący element:</span><span class="sxs-lookup"><span data-stu-id="d5775-265">In C#, we can write it like this:</span></span>

```csharp
internal unsafe struct SYSTEM_PROCESS_INFORMATION
{
    internal uint NextEntryOffset;
    internal uint NumberOfThreads;
    private fixed byte Reserved1[48];
    internal Interop.UNICODE_STRING ImageName;
    ...
}
```

<span data-ttu-id="d5775-266">Istnieje jednak kilka pytania dotyczące usługi z stałymi buforami.</span><span class="sxs-lookup"><span data-stu-id="d5775-266">However, there are some gotchas with fixed buffers.</span></span> <span data-ttu-id="d5775-267">Stałe bufory typów innych niż danych kopiowalnych nie będą poprawnie organizowane, więc tablica w miejscu musi być rozwijana do wielu pojedynczych pól.</span><span class="sxs-lookup"><span data-stu-id="d5775-267">Fixed buffers of non-blittable types won't be correctly marshaled, so the in-place array needs to be expanded out to multiple individual fields.</span></span> <span data-ttu-id="d5775-268">Ponadto w .NET Framework i .NET Core przed 3,0, jeśli struktura zawierająca pole stałego buforu jest zagnieżdżona w strukturze innej niż danych kopiowalnych, stałe pole buforu nie będzie poprawnie organizowane w kodzie natywnym.</span><span class="sxs-lookup"><span data-stu-id="d5775-268">Additionally, in .NET Framework and .NET Core before 3.0, if a struct containing a fixed buffer field is nested within a non-blittable struct, the fixed buffer field won't be correctly marshaled to native code.</span></span>
