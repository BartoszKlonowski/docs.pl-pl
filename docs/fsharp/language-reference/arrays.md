---
title: Tablice
description: 'Dowiedz się, jak tworzyć i używać tablic w języku programowania F #.'
ms.date: 08/13/2020
ms.openlocfilehash: 96b0d7eaf10d5afcd9a647681d5c2ef2d2fba335
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96739754"
---
# <a name="arrays"></a><span data-ttu-id="726f7-103">Tablice</span><span class="sxs-lookup"><span data-stu-id="726f7-103">Arrays</span></span>

<span data-ttu-id="726f7-104">Tablice są stałymi, niemodyfikowalnymi kolekcjami kolejnych elementów danych, które są tego samego typu.</span><span class="sxs-lookup"><span data-stu-id="726f7-104">Arrays are fixed-size, zero-based, mutable collections of consecutive data elements that are all of the same type.</span></span>

## <a name="create-arrays"></a><span data-ttu-id="726f7-105">Tworzenie tablic</span><span class="sxs-lookup"><span data-stu-id="726f7-105">Create arrays</span></span>

<span data-ttu-id="726f7-106">Tablice można tworzyć na kilka sposobów.</span><span class="sxs-lookup"><span data-stu-id="726f7-106">You can create arrays in several ways.</span></span> <span data-ttu-id="726f7-107">Możesz utworzyć małą tablicę, określając kolejne wartości między `[|` i `|]` i rozdzielone średnikami, jak pokazano w poniższych przykładach.</span><span class="sxs-lookup"><span data-stu-id="726f7-107">You can create a small array by listing consecutive values between `[|` and `|]` and separated by semicolons, as shown in the following examples.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet1.fs)]

<span data-ttu-id="726f7-108">Można również umieścić każdy element w osobnym wierszu, w którym przypadku separator średników jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="726f7-108">You can also put each element on a separate line, in which case the semicolon separator is optional.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet2.fs)]

<span data-ttu-id="726f7-109">Typ elementów tablicy jest wywnioskowany na podstawie używanych literałów i musi być spójny.</span><span class="sxs-lookup"><span data-stu-id="726f7-109">The type of the array elements is inferred from the literals used and must be consistent.</span></span> <span data-ttu-id="726f7-110">Poniższy kod powoduje błąd, ponieważ 1,0 jest zmiennoprzecinkowa i 2 i 3 są liczbami całkowitymi.</span><span class="sxs-lookup"><span data-stu-id="726f7-110">The following code causes an error because 1.0 is a float and 2 and 3 are integers.</span></span>

```fsharp
// Causes an error.
// let array2 = [| 1.0; 2; 3 |]
```

<span data-ttu-id="726f7-111">Można również użyć wyrażeń sekwencji do tworzenia tablic.</span><span class="sxs-lookup"><span data-stu-id="726f7-111">You can also use sequence expressions to create arrays.</span></span> <span data-ttu-id="726f7-112">Poniżej znajduje się przykład, który tworzy tablicę kwadratów liczb całkowitych z zakresu od 1 do 10.</span><span class="sxs-lookup"><span data-stu-id="726f7-112">Following is an example that creates an array of squares of integers from 1 to 10.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet3.fs)]

<span data-ttu-id="726f7-113">Aby utworzyć tablicę, w której wszystkie elementy są zainicjowane do zera, użyj `Array.zeroCreate` .</span><span class="sxs-lookup"><span data-stu-id="726f7-113">To create an array in which all the elements are initialized to zero, use `Array.zeroCreate`.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet4.fs)]

## <a name="access-elements"></a><span data-ttu-id="726f7-114">Elementy dostępu</span><span class="sxs-lookup"><span data-stu-id="726f7-114">Access elements</span></span>

<span data-ttu-id="726f7-115">Możesz uzyskać dostęp do elementów tablicy przy użyciu operatora kropki ( `.` ) i nawiasów kwadratowych ( `[` i `]` ).</span><span class="sxs-lookup"><span data-stu-id="726f7-115">You can access array elements by using a dot operator (`.`) and brackets (`[` and `]`).</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet5.fs)]

<span data-ttu-id="726f7-116">Indeksy tablicy zaczynają się od 0.</span><span class="sxs-lookup"><span data-stu-id="726f7-116">Array indexes start at 0.</span></span>

<span data-ttu-id="726f7-117">Możesz również uzyskać dostęp do elementów tablicy przy użyciu notacji wycinka, która umożliwia określenie podzakresu tablicy.</span><span class="sxs-lookup"><span data-stu-id="726f7-117">You can also access array elements by using slice notation, which enables you to specify a subrange of the array.</span></span> <span data-ttu-id="726f7-118">Przykłady zapisu wycinka są następujące.</span><span class="sxs-lookup"><span data-stu-id="726f7-118">Examples of slice notation follow.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet51.fs)]

<span data-ttu-id="726f7-119">Gdy jest używana notacja wycinka, tworzona jest nowa kopia tablicy.</span><span class="sxs-lookup"><span data-stu-id="726f7-119">When slice notation is used, a new copy of the array is created.</span></span>

## <a name="array-types-and-modules"></a><span data-ttu-id="726f7-120">Typy tablic i moduły</span><span class="sxs-lookup"><span data-stu-id="726f7-120">Array types and modules</span></span>

<span data-ttu-id="726f7-121">Typ wszystkich tablic F # to typ .NET Framework <xref:System.Array?displayProperty=nameWithType> .</span><span class="sxs-lookup"><span data-stu-id="726f7-121">The type of all F# arrays is the .NET Framework type <xref:System.Array?displayProperty=nameWithType>.</span></span> <span data-ttu-id="726f7-122">W związku z tym tablice języka F # obsługują wszystkie funkcje dostępne w programie <xref:System.Array?displayProperty=nameWithType> .</span><span class="sxs-lookup"><span data-stu-id="726f7-122">Therefore, F# arrays support all the functionality available in <xref:System.Array?displayProperty=nameWithType>.</span></span>

<span data-ttu-id="726f7-123">[ `Array` Moduł](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html) obsługuje operacje w tablicach jednowymiarowych.</span><span class="sxs-lookup"><span data-stu-id="726f7-123">The [`Array` module](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html) supports operations on one-dimensional arrays.</span></span> <span data-ttu-id="726f7-124">Moduły `Array2D` , `Array3D` i `Array4D` zawierają funkcje, które obsługują operacje na tablicach odpowiednio dwa, trzy i cztery wymiary.</span><span class="sxs-lookup"><span data-stu-id="726f7-124">The modules `Array2D`, `Array3D`, and `Array4D` contain functions that support operations on arrays of two, three, and four dimensions, respectively.</span></span> <span data-ttu-id="726f7-125">Można utworzyć tablice rangi większe niż cztery przy użyciu <xref:System.Array?displayProperty=nameWithType> .</span><span class="sxs-lookup"><span data-stu-id="726f7-125">You can create arrays of rank greater than four by using <xref:System.Array?displayProperty=nameWithType>.</span></span>

### <a name="simple-functions"></a><span data-ttu-id="726f7-126">Proste funkcje</span><span class="sxs-lookup"><span data-stu-id="726f7-126">Simple functions</span></span>

<span data-ttu-id="726f7-127">[`Array.get`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#get) Pobiera element.</span><span class="sxs-lookup"><span data-stu-id="726f7-127">[`Array.get`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#get) gets an element.</span></span> <span data-ttu-id="726f7-128">[`Array.length`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#length) podaje długość tablicy.</span><span class="sxs-lookup"><span data-stu-id="726f7-128">[`Array.length`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#length) gives the length of an array.</span></span> <span data-ttu-id="726f7-129">[`Array.set`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#set) Ustawia element na określoną wartość.</span><span class="sxs-lookup"><span data-stu-id="726f7-129">[`Array.set`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#set) sets an element to a specified value.</span></span> <span data-ttu-id="726f7-130">Poniższy przykład kodu ilustruje sposób korzystania z tych funkcji.</span><span class="sxs-lookup"><span data-stu-id="726f7-130">The following code example illustrates the use of these functions.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet9.fs)]

<span data-ttu-id="726f7-131">Dane wyjściowe są następujące:</span><span class="sxs-lookup"><span data-stu-id="726f7-131">The output is as follows.</span></span>

```console
0 1 2 3 4 5 6 7 8 9
```

### <a name="functions-that-create-arrays"></a><span data-ttu-id="726f7-132">Funkcje tworzące tablice</span><span class="sxs-lookup"><span data-stu-id="726f7-132">Functions that create arrays</span></span>

<span data-ttu-id="726f7-133">Kilka funkcji tworzy tablice bez konieczności stosowania istniejącej tablicy.</span><span class="sxs-lookup"><span data-stu-id="726f7-133">Several functions create arrays without requiring an existing array.</span></span> <span data-ttu-id="726f7-134">[`Array.empty`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#empty) tworzy nową tablicę, która nie zawiera żadnych elementów.</span><span class="sxs-lookup"><span data-stu-id="726f7-134">[`Array.empty`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#empty) creates a new array that does not contain any elements.</span></span> <span data-ttu-id="726f7-135">[`Array.create`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#create) Tworzy tablicę o określonym rozmiarze i ustawia wszystkie elementy na dostarczone wartości.</span><span class="sxs-lookup"><span data-stu-id="726f7-135">[`Array.create`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#create) creates an array of a specified size and sets all the elements to provided values.</span></span> <span data-ttu-id="726f7-136">[`Array.init`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#init) Tworzy tablicę z uwzględnieniem wymiaru i funkcji w celu wygenerowania elementów.</span><span class="sxs-lookup"><span data-stu-id="726f7-136">[`Array.init`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#init) creates an array, given a dimension and a function to generate the elements.</span></span> <span data-ttu-id="726f7-137">[`Array.zeroCreate`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#zeroCreate) Tworzy tablicę, w której wszystkie elementy są inicjowane jako wartość zerowa dla typu tablicy.</span><span class="sxs-lookup"><span data-stu-id="726f7-137">[`Array.zeroCreate`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#zeroCreate) creates an array in which all the elements are initialized to the zero value for the array's type.</span></span> <span data-ttu-id="726f7-138">Poniższy kod ilustruje te funkcje.</span><span class="sxs-lookup"><span data-stu-id="726f7-138">The following code demonstrates these functions.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet91.fs)]

<span data-ttu-id="726f7-139">Dane wyjściowe są następujące:</span><span class="sxs-lookup"><span data-stu-id="726f7-139">The output is as follows.</span></span>

```console
Length of empty array: 0
Area of floats set to 5.0: [|5.0; 5.0; 5.0; 5.0; 5.0; 5.0; 5.0; 5.0; 5.0; 5.0|]
Array of squares: [|0; 1; 4; 9; 16; 25; 36; 49; 64; 81|]
```

<span data-ttu-id="726f7-140">[`Array.copy`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#copy) tworzy nową tablicę zawierającą elementy, które są kopiowane z istniejącej tablicy.</span><span class="sxs-lookup"><span data-stu-id="726f7-140">[`Array.copy`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#copy) creates a new array that contains elements that are copied from an existing array.</span></span> <span data-ttu-id="726f7-141">Należy pamiętać, że kopia jest kopią skróconą, co oznacza, że jeśli typem elementu jest typ referencyjny, kopiowane jest tylko odwołanie, a nie obiekt źródłowy.</span><span class="sxs-lookup"><span data-stu-id="726f7-141">Note that the copy is a shallow copy, which means that if the element type is a reference type, only the reference is copied, not the underlying object.</span></span> <span data-ttu-id="726f7-142">Pokazano to w poniższym przykładzie kodu.</span><span class="sxs-lookup"><span data-stu-id="726f7-142">The following code example illustrates this.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet11.fs)]

<span data-ttu-id="726f7-143">Dane wyjściowe powyższego kodu są następujące:</span><span class="sxs-lookup"><span data-stu-id="726f7-143">The output of the preceding code is as follows:</span></span>

```console
[|Test1; Test2; |]
[|; Test2; |]
```

<span data-ttu-id="726f7-144">Ciąg `Test1` pojawia się tylko w pierwszej tablicy, ponieważ operacja tworzenia nowego elementu zastępuje odwołanie w, `firstArray` ale nie wpływa na pierwotne odwołanie do pustego ciągu, który nadal występuje w `secondArray` .</span><span class="sxs-lookup"><span data-stu-id="726f7-144">The string `Test1` appears only in the first array because the operation of creating a new element overwrites the reference in `firstArray` but does not affect the original reference to an empty string that is still present in `secondArray`.</span></span> <span data-ttu-id="726f7-145">Ciąg `Test2` pojawia się w obu tablicach `Insert` , ponieważ operacja na <xref:System.Text.StringBuilder?displayProperty=nameWithType> typie ma wpływ na <xref:System.Text.StringBuilder?displayProperty=nameWithType> obiekt źródłowy, do którego odwołuje się obie tablice.</span><span class="sxs-lookup"><span data-stu-id="726f7-145">The string `Test2` appears in both arrays because the `Insert` operation on the <xref:System.Text.StringBuilder?displayProperty=nameWithType> type affects the underlying <xref:System.Text.StringBuilder?displayProperty=nameWithType> object, which is referenced in both arrays.</span></span>

<span data-ttu-id="726f7-146">[`Array.sub`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#sub) generuje nową tablicę z podzakresu tablicy.</span><span class="sxs-lookup"><span data-stu-id="726f7-146">[`Array.sub`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#sub) generates a new array from a subrange of an array.</span></span> <span data-ttu-id="726f7-147">Należy określić Podzakres, podając początkowy indeks i długość.</span><span class="sxs-lookup"><span data-stu-id="726f7-147">You specify the subrange by providing the starting index and the length.</span></span> <span data-ttu-id="726f7-148">Poniższy kod ilustruje użycie `Array.sub` .</span><span class="sxs-lookup"><span data-stu-id="726f7-148">The following code demonstrates the use of `Array.sub`.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet12.fs)]

<span data-ttu-id="726f7-149">Dane wyjściowe pokazują, że podtablica zaczyna się od elementu 5 i zawiera 10 elementów.</span><span class="sxs-lookup"><span data-stu-id="726f7-149">The output shows that the subarray starts at element 5 and contains 10 elements.</span></span>

```console
[|5; 6; 7; 8; 9; 10; 11; 12; 13; 14|]
```

<span data-ttu-id="726f7-150">[`Array.append`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#append) tworzy nową tablicę przez połączenie dwóch istniejących tablic.</span><span class="sxs-lookup"><span data-stu-id="726f7-150">[`Array.append`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#append) creates a new array by combining two existing arrays.</span></span>

<span data-ttu-id="726f7-151">Poniższy kod ilustruje **tablicę Array. Append**.</span><span class="sxs-lookup"><span data-stu-id="726f7-151">The following code demonstrates **Array.append**.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet13.fs)]

<span data-ttu-id="726f7-152">Dane wyjściowe powyższego kodu są następujące.</span><span class="sxs-lookup"><span data-stu-id="726f7-152">The output of the preceding code is as follows.</span></span>

```console
[|1; 2; 3; 4; 5; 6|]
```

<span data-ttu-id="726f7-153">[`Array.choose`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#choose) wybiera elementy tablicy do uwzględnienia w nowej tablicy.</span><span class="sxs-lookup"><span data-stu-id="726f7-153">[`Array.choose`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#choose) selects elements of an array to include in a new array.</span></span> <span data-ttu-id="726f7-154">Poniższy kod ilustruje `Array.choose` .</span><span class="sxs-lookup"><span data-stu-id="726f7-154">The following code demonstrates `Array.choose`.</span></span> <span data-ttu-id="726f7-155">Należy zauważyć, że typ elementu tablicy nie musi być zgodny z typem wartości zwracanej w typie opcji.</span><span class="sxs-lookup"><span data-stu-id="726f7-155">Note that the element type of the array does not have to match the type of the value returned in the option type.</span></span> <span data-ttu-id="726f7-156">W tym przykładzie typ elementu to `int` i opcja jest wynikiem funkcji wielomianu, `elem*elem - 1` jako liczby zmiennoprzecinkowej.</span><span class="sxs-lookup"><span data-stu-id="726f7-156">In this example, the element type is `int` and the option is the result of a polynomial function, `elem*elem - 1`, as a floating point number.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet14.fs)]

<span data-ttu-id="726f7-157">Dane wyjściowe powyższego kodu są następujące.</span><span class="sxs-lookup"><span data-stu-id="726f7-157">The output of the preceding code is as follows.</span></span>

```console
[|3.0; 15.0; 35.0; 63.0; 99.0|]
```

<span data-ttu-id="726f7-158">[`Array.collect`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#collect) uruchamia określoną funkcję dla każdego elementu tablicy istniejącej tablicy, a następnie zbiera elementy wygenerowane przez funkcję i łączy je w nową tablicę.</span><span class="sxs-lookup"><span data-stu-id="726f7-158">[`Array.collect`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#collect) runs a specified function on each array element of an existing array and then collects the elements generated by the function and combines them into a new array.</span></span> <span data-ttu-id="726f7-159">Poniższy kod ilustruje `Array.collect` .</span><span class="sxs-lookup"><span data-stu-id="726f7-159">The following code demonstrates `Array.collect`.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet15.fs)]

<span data-ttu-id="726f7-160">Dane wyjściowe powyższego kodu są następujące.</span><span class="sxs-lookup"><span data-stu-id="726f7-160">The output of the preceding code is as follows.</span></span>

```console
[|0; 1; 0; 1; 2; 3; 4; 5; 0; 1; 2; 3; 4; 5; 6; 7; 8; 9; 10|]
```

<span data-ttu-id="726f7-161">[`Array.concat`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#concat) wykonuje sekwencję tablic i łączy je w jedną tablicę.</span><span class="sxs-lookup"><span data-stu-id="726f7-161">[`Array.concat`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#concat) takes a sequence of arrays and combines them into a single array.</span></span> <span data-ttu-id="726f7-162">Poniższy kod ilustruje `Array.concat` .</span><span class="sxs-lookup"><span data-stu-id="726f7-162">The following code demonstrates `Array.concat`.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet16.fs)]

<span data-ttu-id="726f7-163">Dane wyjściowe powyższego kodu są następujące.</span><span class="sxs-lookup"><span data-stu-id="726f7-163">The output of the preceding code is as follows.</span></span>

```console
[|(1, 1, 1); (1, 2, 2); (1, 3, 3); (2, 1, 2); (2, 2, 4); (2, 3, 6); (3, 1, 3);
(3, 2, 6); (3, 3, 9)|]
```

<span data-ttu-id="726f7-164">[`Array.filter`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#filter) przyjmuje funkcję warunku logicznego i generuje nową tablicę zawierającą tylko te elementy z tablicy wejściowej, dla których warunek ma wartość true.</span><span class="sxs-lookup"><span data-stu-id="726f7-164">[`Array.filter`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#filter) takes a Boolean condition function and generates a new array that contains only those elements from the input array for which the condition is true.</span></span> <span data-ttu-id="726f7-165">Poniższy kod ilustruje `Array.filter` .</span><span class="sxs-lookup"><span data-stu-id="726f7-165">The following code demonstrates `Array.filter`.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet17.fs)]

<span data-ttu-id="726f7-166">Dane wyjściowe powyższego kodu są następujące.</span><span class="sxs-lookup"><span data-stu-id="726f7-166">The output of the preceding code is as follows.</span></span>

```console
[|2; 4; 6; 8; 10|]
```

<span data-ttu-id="726f7-167">[`Array.rev`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#rev) generuje nową tablicę przez odwracanie kolejności istniejącej tablicy.</span><span class="sxs-lookup"><span data-stu-id="726f7-167">[`Array.rev`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#rev) generates a new array by reversing the order of an existing array.</span></span> <span data-ttu-id="726f7-168">Poniższy kod ilustruje `Array.rev` .</span><span class="sxs-lookup"><span data-stu-id="726f7-168">The following code demonstrates `Array.rev`.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet18.fs)]

<span data-ttu-id="726f7-169">Dane wyjściowe powyższego kodu są następujące.</span><span class="sxs-lookup"><span data-stu-id="726f7-169">The output of the preceding code is as follows.</span></span>

```console
"Hello world!"
```

<span data-ttu-id="726f7-170">Można łatwo połączyć funkcje w module Array, które przekształcają tablice za pomocą operatora potoku ( `|>` ), jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="726f7-170">You can easily combine functions in the array module that transform arrays by using the pipeline operator (`|>`), as shown in the following example.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet19.fs)]

<span data-ttu-id="726f7-171">Dane wyjściowe to</span><span class="sxs-lookup"><span data-stu-id="726f7-171">The output is</span></span>

```console
[|100; 36; 16; 4|]
```

### <a name="multidimensional-arrays"></a><span data-ttu-id="726f7-172">Tablice wielowymiarowe</span><span class="sxs-lookup"><span data-stu-id="726f7-172">Multidimensional arrays</span></span>

<span data-ttu-id="726f7-173">Można utworzyć tablicę wielowymiarową, ale nie ma składni do pisania wielowymiarowego literału tablicy.</span><span class="sxs-lookup"><span data-stu-id="726f7-173">A multidimensional array can be created, but there is no syntax for writing a multidimensional array literal.</span></span> <span data-ttu-id="726f7-174">Użyj operatora, [`array2D`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-array2dmodule.html) Aby utworzyć tablicę z sekwencji sekwencji elementów tablicy.</span><span class="sxs-lookup"><span data-stu-id="726f7-174">Use the operator [`array2D`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-array2dmodule.html) to create an array from a sequence of sequences of array elements.</span></span> <span data-ttu-id="726f7-175">Sekwencje mogą być literałami tablicowymi lub listami.</span><span class="sxs-lookup"><span data-stu-id="726f7-175">The sequences can be array or list literals.</span></span> <span data-ttu-id="726f7-176">Na przykład poniższy kod tworzy tablicę dwuwymiarową.</span><span class="sxs-lookup"><span data-stu-id="726f7-176">For example, the following code creates a two-dimensional array.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet20.fs)]

<span data-ttu-id="726f7-177">Można również użyć funkcji, [`Array2D.init`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-array2dmodule.html#init) Aby zainicjować tablice dwóch wymiarów, a podobne funkcje są dostępne dla tablic trzech i czterech wymiarów.</span><span class="sxs-lookup"><span data-stu-id="726f7-177">You can also use the function [`Array2D.init`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-array2dmodule.html#init) to initialize arrays of two dimensions, and similar functions are available for arrays of three and four dimensions.</span></span> <span data-ttu-id="726f7-178">Funkcje te przyjmują funkcję, która jest używana do tworzenia elementów.</span><span class="sxs-lookup"><span data-stu-id="726f7-178">These functions take a function that is used to create the elements.</span></span> <span data-ttu-id="726f7-179">Aby utworzyć dwuwymiarową tablicę, która zawiera elementy ustawione na wartość początkową zamiast określania funkcji, należy użyć [`Array2D.create`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-array2dmodule.html#create) funkcji, która jest również dostępna dla tablic do czterech wymiarów.</span><span class="sxs-lookup"><span data-stu-id="726f7-179">To create a two-dimensional array that contains elements set to an initial value instead of specifying a function, use the [`Array2D.create`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-array2dmodule.html#create) function, which is also available for arrays up to four dimensions.</span></span> <span data-ttu-id="726f7-180">Poniższy przykład kodu najpierw pokazuje, jak utworzyć tablicę tablic zawierających wymagane elementy, a następnie użyć `Array2D.init` do wygenerowania odpowiedniej tablicy dwuwymiarowej.</span><span class="sxs-lookup"><span data-stu-id="726f7-180">The following code example first shows how to create an array of arrays that contain the desired elements, and then uses `Array2D.init` to generate the desired two-dimensional array.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet21.fs)]

<span data-ttu-id="726f7-181">Składnia indeksowania tablicy i skalowanie wycinków jest obsługiwana w przypadku tablic o wartości do rangi 4.</span><span class="sxs-lookup"><span data-stu-id="726f7-181">Array indexing and slicing syntax is supported for arrays up to rank 4.</span></span> <span data-ttu-id="726f7-182">Po określeniu indeksu w wielu wymiarach, należy użyć przecinków do oddzielenia indeksów, jak pokazano w poniższym przykładzie kodu.</span><span class="sxs-lookup"><span data-stu-id="726f7-182">When you specify an index in multiple dimensions, you use commas to separate the indexes, as illustrated in the following code example.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet22.fs)]

<span data-ttu-id="726f7-183">Typ tablicy dwuwymiarowej jest zapisywana jako `<type>[,]` (na przykład `int[,]` , `double[,]` ), a typ trójwymiarowej tablicy jest zapisywana jako `<type>[,,]` itd. dla tablic o wyższych wymiarach.</span><span class="sxs-lookup"><span data-stu-id="726f7-183">The type of a two-dimensional array is written out as `<type>[,]` (for example, `int[,]`, `double[,]`), and the type of a three-dimensional array is written as `<type>[,,]`, and so on for arrays of higher dimensions.</span></span>

<span data-ttu-id="726f7-184">Tylko podzestaw funkcji dostępnych dla tablic jednowymiarowych jest również dostępny dla tablic wielowymiarowych.</span><span class="sxs-lookup"><span data-stu-id="726f7-184">Only a subset of the functions available for one-dimensional arrays is also available for multidimensional arrays.</span></span>

### <a name="array-slicing-and-multidimensional-arrays"></a><span data-ttu-id="726f7-185">Dzielenie tablic i tablice wielowymiarowe</span><span class="sxs-lookup"><span data-stu-id="726f7-185">Array slicing and multidimensional arrays</span></span>

<span data-ttu-id="726f7-186">W tablicy dwuwymiarowej (macierzy) można wyodrębnić tablicę podrzędną, określając zakresy i używając znaku wieloznacznego ( `*` ) w celu określenia całych wierszy lub kolumn.</span><span class="sxs-lookup"><span data-stu-id="726f7-186">In a two-dimensional array (a matrix), you can extract a sub-matrix by specifying ranges and using a wildcard (`*`) character to specify whole rows or columns.</span></span>

```fsharp
// Get rows 1 to N from an NxM matrix (returns a matrix):
matrix.[1.., *]

// Get rows 1 to 3 from a matrix (returns a matrix):
matrix.[1..3, *]

// Get columns 1 to 3 from a matrix (returns a matrix):
matrix.[*, 1..3]

// Get a 3x3 submatrix:
matrix.[1..3, 1..3]
```

<span data-ttu-id="726f7-187">Można rozłożyć tablicę wielowymiarową na podtablice tego samego lub niższego wymiaru.</span><span class="sxs-lookup"><span data-stu-id="726f7-187">You can decompose a multidimensional array into subarrays of the same or lower dimension.</span></span> <span data-ttu-id="726f7-188">Na przykład można uzyskać wektor z macierzy, określając pojedynczy wiersz lub kolumnę.</span><span class="sxs-lookup"><span data-stu-id="726f7-188">For example, you can obtain a vector from a matrix by specifying a single row or column.</span></span>

```fsharp
// Get row 3 from a matrix as a vector:
matrix.[3, *]

// Get column 3 from a matrix as a vector:
matrix.[*, 3]
```

<span data-ttu-id="726f7-189">Można użyć tej składni wycinków dla typów, które implementują operatory dostępu do elementów i przeciążone `GetSlice` metody.</span><span class="sxs-lookup"><span data-stu-id="726f7-189">You can use this slicing syntax for types that implement the element access operators and overloaded `GetSlice` methods.</span></span> <span data-ttu-id="726f7-190">Na przykład poniższy kod tworzy typ macierzy, która otacza tablicę 2D języka F #, implementuje właściwość elementu w celu zapewnienia obsługi indeksowania tablicy i implementuje trzy wersje programu `GetSlice` .</span><span class="sxs-lookup"><span data-stu-id="726f7-190">For example, the following code creates a Matrix type that wraps the F# 2D array, implements an Item property to provide support for array indexing, and implements three versions of `GetSlice`.</span></span> <span data-ttu-id="726f7-191">Jeśli możesz użyć tego kodu jako szablonu dla typów macierzy, możesz użyć wszystkich operacji tworzenia wycinków, które opisano w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="726f7-191">If you can use this code as a template for your matrix types, you can use all the slicing operations that this section describes.</span></span>

```fsharp
type Matrix<'T>(N: int, M: int) =
    let internalArray = Array2D.zeroCreate<'T> N M

    member this.Item
        with get(a: int, b: int) = internalArray.[a, b]
        and set(a: int, b: int) (value:'T) = internalArray.[a, b] <- value

    member this.GetSlice(rowStart: int option, rowFinish : int option, colStart: int option, colFinish : int option) =
        let rowStart =
            match rowStart with
            | Some(v) -> v
            | None -> 0
        let rowFinish =
            match rowFinish with
            | Some(v) -> v
            | None -> internalArray.GetLength(0) - 1
        let colStart =
            match colStart with
            | Some(v) -> v
            | None -> 0
        let colFinish =
            match colFinish with
            | Some(v) -> v
            | None -> internalArray.GetLength(1) - 1
        internalArray.[rowStart..rowFinish, colStart..colFinish]

    member this.GetSlice(row: int, colStart: int option, colFinish: int option) =
        let colStart =
            match colStart with
            | Some(v) -> v
            | None -> 0
        let colFinish =
            match colFinish with
            | Some(v) -> v
            | None -> internalArray.GetLength(1) - 1
        internalArray.[row, colStart..colFinish]

    member this.GetSlice(rowStart: int option, rowFinish: int option, col: int) =
        let rowStart =
            match rowStart with
            | Some(v) -> v
            | None -> 0
        let rowFinish =
            match rowFinish with
            | Some(v) -> v
            | None -> internalArray.GetLength(0) - 1
        internalArray.[rowStart..rowFinish, col]

module test =
    let generateTestMatrix x y =
        let matrix = new Matrix<float>(3, 3)
        for i in 0..2 do
            for j in 0..2 do
                matrix.[i, j] <- float(i) * x - float(j) * y
        matrix

    let test1 = generateTestMatrix 2.3 1.1
    let submatrix = test1.[0..1, 0..1]
    printfn $"{submatrix}"

    let firstRow = test1.[0,*]
    let secondRow = test1.[1,*]
    let firstCol = test1.[*,0]
    printfn $"{firstCol}"
```

### <a name="boolean-functions-on-arrays"></a><span data-ttu-id="726f7-192">Funkcje logiczne w tablicach</span><span class="sxs-lookup"><span data-stu-id="726f7-192">Boolean functions on arrays</span></span>

<span data-ttu-id="726f7-193">Elementy Functions [`Array.exists`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#exists) i [`Array.exists2`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#exists2) test są odpowiednio w jednej lub dwóch tablicach.</span><span class="sxs-lookup"><span data-stu-id="726f7-193">The functions [`Array.exists`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#exists) and [`Array.exists2`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#exists2) test elements in either one or two arrays, respectively.</span></span> <span data-ttu-id="726f7-194">Te funkcje przyjmują funkcję testową i zwracają, `true` Jeśli istnieje element (lub para elementów dla `Array.exists2` ), który spełnia warunek.</span><span class="sxs-lookup"><span data-stu-id="726f7-194">These functions take a test function and return `true` if there is an element (or element pair for `Array.exists2`) that satisfies the condition.</span></span>

<span data-ttu-id="726f7-195">Poniższy kod ilustruje użycie `Array.exists` i `Array.exists2` .</span><span class="sxs-lookup"><span data-stu-id="726f7-195">The following code demonstrates the use of `Array.exists` and `Array.exists2`.</span></span> <span data-ttu-id="726f7-196">W tych przykładach nowe funkcje są tworzone przez zastosowanie tylko jednego z argumentów, w takich przypadkach, argumentu funkcji.</span><span class="sxs-lookup"><span data-stu-id="726f7-196">In these examples, new functions are created by applying only one of the arguments, in these cases, the function argument.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet23.fs)]

<span data-ttu-id="726f7-197">Dane wyjściowe powyższego kodu są następujące.</span><span class="sxs-lookup"><span data-stu-id="726f7-197">The output of the preceding code is as follows.</span></span>

```console
true
false
false
true
```

<span data-ttu-id="726f7-198">Podobnie funkcja [`Array.forall`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#forall) testuje tablicę, aby określić, czy każdy element spełnia warunek logiczny.</span><span class="sxs-lookup"><span data-stu-id="726f7-198">Similarly, the function [`Array.forall`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#forall) tests an array to determine whether every element satisfies a Boolean condition.</span></span> <span data-ttu-id="726f7-199">Odmiana [`Array.forall2`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#forall2) wykonuje tę samą czynność przy użyciu funkcji logicznej, która obejmuje elementy dwóch tablic o równej długości.</span><span class="sxs-lookup"><span data-stu-id="726f7-199">The variation [`Array.forall2`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#forall2) does the same thing by using a Boolean function that involves elements of two arrays of equal length.</span></span> <span data-ttu-id="726f7-200">Poniższy kod ilustruje sposób korzystania z tych funkcji.</span><span class="sxs-lookup"><span data-stu-id="726f7-200">The following code illustrates the use of these functions.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet24.fs)]

<span data-ttu-id="726f7-201">Dane wyjściowe dla tych przykładów są następujące.</span><span class="sxs-lookup"><span data-stu-id="726f7-201">The output for these examples is as follows.</span></span>

```console
false
true
true
false
```

### <a name="search-arrays"></a><span data-ttu-id="726f7-202">Wyszukaj tablice</span><span class="sxs-lookup"><span data-stu-id="726f7-202">Search arrays</span></span>

<span data-ttu-id="726f7-203">[`Array.find`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#find) przyjmuje funkcję logiczną i zwraca pierwszy element, dla którego funkcja zwraca `true` , lub wywołuje <xref:System.Collections.Generic.KeyNotFoundException?displayProperty=nameWithType> Jeśli nie zostanie znaleziony żaden element, który spełnia warunek.</span><span class="sxs-lookup"><span data-stu-id="726f7-203">[`Array.find`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#find) takes a Boolean function and returns the first element for which the function returns `true`, or raises a <xref:System.Collections.Generic.KeyNotFoundException?displayProperty=nameWithType> if no element that satisfies the condition is found.</span></span> <span data-ttu-id="726f7-204">[`Array.findIndex`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#findIndex) jest podobne `Array.find` , z tą różnicą, że zwraca indeks elementu zamiast samego elementu.</span><span class="sxs-lookup"><span data-stu-id="726f7-204">[`Array.findIndex`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#findIndex) is like `Array.find`, except that it returns the index of the element instead of the element itself.</span></span>

<span data-ttu-id="726f7-205">Poniższy kod używa `Array.find` i, `Array.findIndex` Aby zlokalizować liczbę, która jest idealnym kwadratem i idealnym modułem.</span><span class="sxs-lookup"><span data-stu-id="726f7-205">The following code uses `Array.find` and `Array.findIndex` to locate a number that is both a perfect square and perfect cube.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet25.fs)]

<span data-ttu-id="726f7-206">Dane wyjściowe są następujące:</span><span class="sxs-lookup"><span data-stu-id="726f7-206">The output is as follows.</span></span>

```console
The first element that is both a square and a cube is 64 and its index is 62.
```

<span data-ttu-id="726f7-207">[`Array.tryFind`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#tryFind) jest podobne `Array.find` , z tą różnicą, że jej wynik jest typem opcji i zwraca, `None` Jeśli nie znaleziono żadnego elementu.</span><span class="sxs-lookup"><span data-stu-id="726f7-207">[`Array.tryFind`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#tryFind) is like `Array.find`, except that its result is an option type, and it returns `None` if no element is found.</span></span> <span data-ttu-id="726f7-208">`Array.tryFind` powinien być używany zamiast `Array.find` gdy nie wiadomo, czy pasujący element znajduje się w tablicy.</span><span class="sxs-lookup"><span data-stu-id="726f7-208">`Array.tryFind` should be used instead of `Array.find` when you do not know whether a matching element is in the array.</span></span> <span data-ttu-id="726f7-209">Podobnie, [`Array.tryFindIndex`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#tryFindIndex) jest taka, jak `Array.findIndex` z tą różnicą, że typ opcji jest wartością zwracaną.</span><span class="sxs-lookup"><span data-stu-id="726f7-209">Similarly, [`Array.tryFindIndex`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#tryFindIndex) is like `Array.findIndex` except that the option type is the return value.</span></span> <span data-ttu-id="726f7-210">Jeśli nie zostanie znaleziony żaden element, opcja jest `None` .</span><span class="sxs-lookup"><span data-stu-id="726f7-210">If no element is found, the option is `None`.</span></span>

<span data-ttu-id="726f7-211">Poniższy kod ilustruje użycie `Array.tryFind` .</span><span class="sxs-lookup"><span data-stu-id="726f7-211">The following code demonstrates the use of `Array.tryFind`.</span></span> <span data-ttu-id="726f7-212">Ten kod zależy od poprzedniego kodu.</span><span class="sxs-lookup"><span data-stu-id="726f7-212">This code depends on the previous code.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet26.fs)]

<span data-ttu-id="726f7-213">Dane wyjściowe są następujące:</span><span class="sxs-lookup"><span data-stu-id="726f7-213">The output is as follows.</span></span>

```console
Found an element: 1
Found an element: 729
Failed to find a matching element.
```

<span data-ttu-id="726f7-214">Użyj, [`Array.tryPick`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#tryPick) gdy chcesz przekształcić element, a także go znaleźć.</span><span class="sxs-lookup"><span data-stu-id="726f7-214">Use [`Array.tryPick`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#tryPick) when you need to transform an element in addition to finding it.</span></span> <span data-ttu-id="726f7-215">Wynikiem jest pierwszy element, dla którego funkcja zwraca przekształcony element jako wartość opcji lub `None` Jeśli nie można znaleźć takiego elementu.</span><span class="sxs-lookup"><span data-stu-id="726f7-215">The result is the first element for which the function returns the transformed element as an option value, or `None` if no such element is found.</span></span>

<span data-ttu-id="726f7-216">Poniższy kod ilustruje użycie `Array.tryPick` .</span><span class="sxs-lookup"><span data-stu-id="726f7-216">The following code shows the use of `Array.tryPick`.</span></span> <span data-ttu-id="726f7-217">W tym przypadku zamiast wyrażenia lambda, kilka lokalnych funkcji pomocniczych jest zdefiniowanych do uproszczenia kodu.</span><span class="sxs-lookup"><span data-stu-id="726f7-217">In this case, instead of a lambda expression, several local helper functions are defined to simplify the code.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet27.fs)]

<span data-ttu-id="726f7-218">Dane wyjściowe są następujące:</span><span class="sxs-lookup"><span data-stu-id="726f7-218">The output is as follows.</span></span>

```console
Found an element 1 with square root 1 and cube root 1.
Found an element 64 with square root 8 and cube root 4.
Found an element 729 with square root 27 and cube root 9.
Found an element 4096 with square root 64 and cube root 16.
Did not find an element that is both a perfect square and a perfect cube.
```

### <a name="perform-computations-on-arrays"></a><span data-ttu-id="726f7-219">Wykonywanie obliczeń w tablicach</span><span class="sxs-lookup"><span data-stu-id="726f7-219">Perform computations on arrays</span></span>

<span data-ttu-id="726f7-220">[`Array.average`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#average)Funkcja zwraca średnią każdego elementu w tablicy.</span><span class="sxs-lookup"><span data-stu-id="726f7-220">The [`Array.average`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#average) function returns the average of each element in an array.</span></span> <span data-ttu-id="726f7-221">Jest ono ograniczone do typów elementów, które obsługują dokładne dzielenie przez liczbę całkowitą, która obejmuje typy zmiennoprzecinkowe, ale nie typy całkowite.</span><span class="sxs-lookup"><span data-stu-id="726f7-221">It is limited to element types that support exact division by an integer, which includes floating point types but not integral types.</span></span> <span data-ttu-id="726f7-222">[`Array.averageBy`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#averageBy)Funkcja zwraca średnią wyników wywołania funkcji dla każdego elementu.</span><span class="sxs-lookup"><span data-stu-id="726f7-222">The [`Array.averageBy`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#averageBy) function returns the average of the results of calling a function on each element.</span></span> <span data-ttu-id="726f7-223">W przypadku tablicy typu całkowitego można użyć `Array.averageBy` funkcji i przekonwertować każdy element na typ zmiennoprzecinkowy obliczenia.</span><span class="sxs-lookup"><span data-stu-id="726f7-223">For an array of integral type, you can use `Array.averageBy` and have the function convert each element to a floating point type for the computation.</span></span>

<span data-ttu-id="726f7-224">Użyj [`Array.max`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#max) lub, [`Array.min`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#min) Aby uzyskać maksimum lub minimum elementu, jeśli jest obsługiwany przez typ elementu.</span><span class="sxs-lookup"><span data-stu-id="726f7-224">Use [`Array.max`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#max) or [`Array.min`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#min) to get the maximum or minimum element, if the element type supports it.</span></span> <span data-ttu-id="726f7-225">Podobnie [`Array.maxBy`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#maxBy) i [`Array.minBy`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#minBy) Zezwalaj na wykonywanie funkcji jako pierwszej, na przykład w celu przekształcenia do typu, który obsługuje porównanie.</span><span class="sxs-lookup"><span data-stu-id="726f7-225">Similarly, [`Array.maxBy`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#maxBy) and [`Array.minBy`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#minBy) allow a function to be executed first, perhaps to transform to a type that supports comparison.</span></span>

<span data-ttu-id="726f7-226">[`Array.sum`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#sum) dodaje elementy tablicy i [`Array.sumBy`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#sumBy) wywołuje funkcję dla każdego elementu i dodaje wyniki ze sobą.</span><span class="sxs-lookup"><span data-stu-id="726f7-226">[`Array.sum`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#sum) adds the elements of an array, and [`Array.sumBy`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#sumBy) calls a function on each element and adds the results together.</span></span>

<span data-ttu-id="726f7-227">Aby wykonać funkcję dla każdego elementu w tablicy bez przechowywania wartości zwracanych, użyj [`Array.iter`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#iter) .</span><span class="sxs-lookup"><span data-stu-id="726f7-227">To execute a function on each element in an array without storing the return values, use [`Array.iter`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#iter).</span></span> <span data-ttu-id="726f7-228">Dla funkcji obejmującej dwie tablice o równej długości Użyj [`Array.iter2`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#iter2) .</span><span class="sxs-lookup"><span data-stu-id="726f7-228">For a function involving two arrays of equal length, use [`Array.iter2`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#iter2).</span></span> <span data-ttu-id="726f7-229">Jeśli trzeba również zachować tablicę wyników funkcji, użyj [`Array.map`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#map) lub [`Array.map2`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#map2) , która działa w dwóch tablicach w danym momencie.</span><span class="sxs-lookup"><span data-stu-id="726f7-229">If you also need to keep an array of the results of the function, use [`Array.map`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#map) or [`Array.map2`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#map2), which operates on two arrays at a time.</span></span>

<span data-ttu-id="726f7-230">Różnice [`Array.iteri`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#iteri) i [`Array.iteri2`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#iteri2) zezwalają na indeks elementu, który ma być uwzględniony w obliczeniach; taka sama wartość dotyczy [`Array.mapi`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#mapi) i [`Array.mapi2`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#mapi2) .</span><span class="sxs-lookup"><span data-stu-id="726f7-230">The variations [`Array.iteri`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#iteri) and [`Array.iteri2`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#iteri2) allow the index of the element to be involved in the computation; the same is true for [`Array.mapi`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#mapi) and [`Array.mapi2`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#mapi2).</span></span>

<span data-ttu-id="726f7-231">[`Array.fold`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#fold)Algorytmy Functions,,,, [`Array.foldBack`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#foldBack) [`Array.reduce`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#reduce) [`Array.reduceBack`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#reduceBack) [`Array.scan`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#scan) i Execute, [`Array.scanBack`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#scanBack) które obejmują wszystkie elementy tablicy.</span><span class="sxs-lookup"><span data-stu-id="726f7-231">The functions [`Array.fold`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#fold), [`Array.foldBack`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#foldBack), [`Array.reduce`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#reduce), [`Array.reduceBack`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#reduceBack), [`Array.scan`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#scan), and [`Array.scanBack`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#scanBack) execute algorithms that involve all the elements of an array.</span></span> <span data-ttu-id="726f7-232">Podobnie, różnice [`Array.fold2`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#fold2) i [`Array.foldBack2`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#foldBack2) wykonywanie obliczeń na dwóch tablicach.</span><span class="sxs-lookup"><span data-stu-id="726f7-232">Similarly, the variations [`Array.fold2`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#fold2) and [`Array.foldBack2`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#foldBack2) perform computations on two arrays.</span></span>

<span data-ttu-id="726f7-233">Te funkcje do wykonywania obliczeń odpowiadają funkcjom o tej samej nazwie w [module list](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-listmodule.html).</span><span class="sxs-lookup"><span data-stu-id="726f7-233">These functions for performing computations correspond to the functions of the same name in the [List module](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-listmodule.html).</span></span> <span data-ttu-id="726f7-234">Aby zapoznać się z przykładami użycia, zobacz [listy](lists.md).</span><span class="sxs-lookup"><span data-stu-id="726f7-234">For usage examples, see [Lists](lists.md).</span></span>

### <a name="modify-arrays"></a><span data-ttu-id="726f7-235">Modyfikuj tablice</span><span class="sxs-lookup"><span data-stu-id="726f7-235">Modify arrays</span></span>

<span data-ttu-id="726f7-236">[`Array.set`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#set) Ustawia element na określoną wartość.</span><span class="sxs-lookup"><span data-stu-id="726f7-236">[`Array.set`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#set) sets an element to a specified value.</span></span> <span data-ttu-id="726f7-237">[`Array.fill`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#fill) ustawia zakres elementów w tablicy do określonej wartości.</span><span class="sxs-lookup"><span data-stu-id="726f7-237">[`Array.fill`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#fill) sets a range of elements in an array to a specified value.</span></span> <span data-ttu-id="726f7-238">Poniższy kod zawiera przykład `Array.fill` .</span><span class="sxs-lookup"><span data-stu-id="726f7-238">The following code provides an example of `Array.fill`.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet28.fs)]

<span data-ttu-id="726f7-239">Dane wyjściowe są następujące:</span><span class="sxs-lookup"><span data-stu-id="726f7-239">The output is as follows.</span></span>

```console
[|1; 2; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 23; 24; 25|]
```

<span data-ttu-id="726f7-240">Można użyć, [`Array.blit`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#blit) Aby skopiować podsekcję jednej tablicy do innej tablicy.</span><span class="sxs-lookup"><span data-stu-id="726f7-240">You can use [`Array.blit`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#blit) to copy a subsection of one array to another array.</span></span>

### <a name="convert-to-and-from-other-types"></a><span data-ttu-id="726f7-241">Konwertuj na i z innych typów</span><span class="sxs-lookup"><span data-stu-id="726f7-241">Convert to and from other types</span></span>

<span data-ttu-id="726f7-242">[`Array.ofList`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#ofList) Tworzy tablicę z listy.</span><span class="sxs-lookup"><span data-stu-id="726f7-242">[`Array.ofList`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#ofList) creates an array from a list.</span></span> <span data-ttu-id="726f7-243">[`Array.ofSeq`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#ofSeq) Tworzy tablicę z sekwencji.</span><span class="sxs-lookup"><span data-stu-id="726f7-243">[`Array.ofSeq`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#ofSeq) creates an array from a sequence.</span></span> <span data-ttu-id="726f7-244">[`Array.toList`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#toList) i [`Array.toSeq`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#toSeq) Konwertuj na inne typy kolekcji z typu tablicy.</span><span class="sxs-lookup"><span data-stu-id="726f7-244">[`Array.toList`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#toList) and [`Array.toSeq`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#toSeq) convert to these other collection types from the array type.</span></span>

### <a name="sort-arrays"></a><span data-ttu-id="726f7-245">Sortuj tablice</span><span class="sxs-lookup"><span data-stu-id="726f7-245">Sort arrays</span></span>

<span data-ttu-id="726f7-246">Użyj, [`Array.sort`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#sort) Aby posortować tablicę przy użyciu funkcji porównania generycznej.</span><span class="sxs-lookup"><span data-stu-id="726f7-246">Use [`Array.sort`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#sort) to sort an array by using the generic comparison function.</span></span> <span data-ttu-id="726f7-247">Użyj, [`Array.sortBy`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#sortBy) Aby określić funkcję, która generuje wartość, która jest określana jako *klucz*, aby sortować przy użyciu funkcji porównywania generycznego w kluczu.</span><span class="sxs-lookup"><span data-stu-id="726f7-247">Use [`Array.sortBy`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#sortBy) to specify a function that generates a value, referred to as a *key*, to sort by using the generic comparison function on the key.</span></span> <span data-ttu-id="726f7-248">Użyj, [`Array.sortWith`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#sortWith) Jeśli chcesz podać niestandardową funkcję porównania.</span><span class="sxs-lookup"><span data-stu-id="726f7-248">Use [`Array.sortWith`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#sortWith) if you want to provide a custom comparison function.</span></span> <span data-ttu-id="726f7-249">`Array.sort`, `Array.sortBy` i `Array.sortWith` wszystkie zwracają posortowaną tablicę jako nową tablicę.</span><span class="sxs-lookup"><span data-stu-id="726f7-249">`Array.sort`, `Array.sortBy`, and `Array.sortWith` all return the sorted array as a new array.</span></span> <span data-ttu-id="726f7-250">Zmiany [`Array.sortInPlace`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#sortInPlace) , [`Array.sortInPlaceBy`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#sortInPlaceBy) i [`Array.sortInPlaceWith`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#sortInPlaceWith) modyfikują istniejącą tablicę zamiast zwracać nowe.</span><span class="sxs-lookup"><span data-stu-id="726f7-250">The variations [`Array.sortInPlace`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#sortInPlace), [`Array.sortInPlaceBy`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#sortInPlaceBy), and [`Array.sortInPlaceWith`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#sortInPlaceWith) modify the existing array instead of returning a new one.</span></span>

### <a name="arrays-and-tuples"></a><span data-ttu-id="726f7-251">Tablice i krotki</span><span class="sxs-lookup"><span data-stu-id="726f7-251">Arrays and tuples</span></span>

<span data-ttu-id="726f7-252">Funkcje [`Array.zip`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#zip) i [`Array.unzip`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#unzip) konwertują tablice par krotek na krotki tablic i na odwrót.</span><span class="sxs-lookup"><span data-stu-id="726f7-252">The functions [`Array.zip`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#zip) and [`Array.unzip`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#unzip) convert arrays of tuple pairs to tuples of arrays and vice versa.</span></span> <span data-ttu-id="726f7-253">[`Array.zip3`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#zip3) i [`Array.unzip3`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#unzip3) są podobne, z tą różnicą, że współpracują z krotkami trzech elementów lub krotekmi trzech tablic.</span><span class="sxs-lookup"><span data-stu-id="726f7-253">[`Array.zip3`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#zip3) and [`Array.unzip3`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule.html#unzip3) are similar except that they work with tuples of three elements or tuples of three arrays.</span></span>

## <a name="parallel-computations-on-arrays"></a><span data-ttu-id="726f7-254">Obliczenia równoległe w tablicach</span><span class="sxs-lookup"><span data-stu-id="726f7-254">Parallel computations on arrays</span></span>

<span data-ttu-id="726f7-255">Moduł [`Array.Parallel`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule-parallel.html) zawiera funkcje do wykonywania obliczeń równoległych w tablicach.</span><span class="sxs-lookup"><span data-stu-id="726f7-255">The module [`Array.Parallel`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-arraymodule-parallel.html) contains functions for performing parallel computations on arrays.</span></span> <span data-ttu-id="726f7-256">Ten moduł nie jest dostępny w aplikacjach przeznaczonych dla wersji .NET Framework wcześniejszych niż wersja 4.</span><span class="sxs-lookup"><span data-stu-id="726f7-256">This module is not available in applications that target versions of the .NET Framework prior to version 4.</span></span>

## <a name="see-also"></a><span data-ttu-id="726f7-257">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="726f7-257">See also</span></span>

- [<span data-ttu-id="726f7-258">Dokumentacja języka F #</span><span class="sxs-lookup"><span data-stu-id="726f7-258">F# Language Reference</span></span>](index.md)
- [<span data-ttu-id="726f7-259">Typy F#</span><span class="sxs-lookup"><span data-stu-id="726f7-259">F# Types</span></span>](fsharp-types.md)
