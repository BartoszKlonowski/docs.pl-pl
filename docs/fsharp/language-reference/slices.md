---
title: Wycinki
description: 'Dowiedz się, jak używać wycinków dla istniejących typów danych F # i jak definiować własne wycinki dla innych typów danych.'
ms.date: 11/20/2020
ms.openlocfilehash: b776058df5a174dfe48dbf513bf17281036dd83e
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96740383"
---
# <a name="slices"></a><span data-ttu-id="7e77d-103">Wycinki</span><span class="sxs-lookup"><span data-stu-id="7e77d-103">Slices</span></span>

<span data-ttu-id="7e77d-104">W tym artykule wyjaśniono, jak korzystać z wycinków z istniejących typów języka F # i jak definiować własne wycinki.</span><span class="sxs-lookup"><span data-stu-id="7e77d-104">This article explains how to take slices from existing F# types and how to define your own slices.</span></span>

<span data-ttu-id="7e77d-105">W języku F # wycinek jest podzbiorem dowolnego typu danych.</span><span class="sxs-lookup"><span data-stu-id="7e77d-105">In F#, a slice is a subset of any data type.</span></span>  <span data-ttu-id="7e77d-106">Wycinki są podobne do [indeksatorów](./members/indexed-properties.md), ale zamiast zwracać jedną wartość z bazowej struktury danych, uzyskują wiele z nich.</span><span class="sxs-lookup"><span data-stu-id="7e77d-106">Slices are similar to [indexers](./members/indexed-properties.md), but instead of yielding a single value from the underlying data structure, they yield multiple ones.</span></span> <span data-ttu-id="7e77d-107">Wycinki używają `..` składni operatora do wybierania zakresu określonych indeksów w typie danych.</span><span class="sxs-lookup"><span data-stu-id="7e77d-107">Slices use the `..` operator syntax to select the range of specified indices in a data type.</span></span> <span data-ttu-id="7e77d-108">Aby uzyskać więcej informacji, zobacz [artykuł odwołanie do wyrażenia zapętlenia](./loops-for-in-expression.md).</span><span class="sxs-lookup"><span data-stu-id="7e77d-108">For more information, see the [looping expression reference article](./loops-for-in-expression.md).</span></span>

<span data-ttu-id="7e77d-109">Język F # jest obecnie obsługiwany wewnętrznie w przypadku ciągów wycinków, list, tablic i wielowymiarowych (2D, 3W, 4D) tablic.</span><span class="sxs-lookup"><span data-stu-id="7e77d-109">F# currently has intrinsic support for slicing strings, lists, arrays, and multidimensional (2D, 3D, 4D) arrays.</span></span> <span data-ttu-id="7e77d-110">Cięcie jest najczęściej używane z tablicami i listami języka F #.</span><span class="sxs-lookup"><span data-stu-id="7e77d-110">Slicing is most commonly used with F# arrays and lists.</span></span> <span data-ttu-id="7e77d-111">Można dodać wycięcie do niestandardowych typów danych przy użyciu `GetSlice` metody w definicji typu lub w [rozszerzeniu typu](type-extensions.md)w zakresie.</span><span class="sxs-lookup"><span data-stu-id="7e77d-111">You can add slicing to your custom data types by using the `GetSlice` method in your type definition or in an in-scope [type extension](type-extensions.md).</span></span>

## <a name="slicing-f-lists-and-arrays"></a><span data-ttu-id="7e77d-112">Cięcie list i tablic języka F #</span><span class="sxs-lookup"><span data-stu-id="7e77d-112">Slicing F# lists and arrays</span></span>

<span data-ttu-id="7e77d-113">Najpopularniejsze typy danych, które są pofragmentowane, to listy i tablice języka F #.</span><span class="sxs-lookup"><span data-stu-id="7e77d-113">The most common data types that are sliced are F# lists and arrays.</span></span>  <span data-ttu-id="7e77d-114">Poniższy przykład ilustruje sposób wycinania list:</span><span class="sxs-lookup"><span data-stu-id="7e77d-114">The following example demonstrates how to slice lists:</span></span>

```fsharp
// Generate a list of 100 integers
let fullList = [ 1 .. 100 ]

// Create a slice from indices 1-5 (inclusive)
let smallSlice = fullList.[1..5]
printfn $"Small slice: {smallSlice}"

// Create a slice from the beginning to index 5 (inclusive)
let unboundedBeginning = fullList.[..5]
printfn $"Unbounded beginning slice: {unboundedBeginning}"

// Create a slice from an index to the end of the list
let unboundedEnd = fullList.[94..]
printfn $"Unbounded end slice: {unboundedEnd}"
```

<span data-ttu-id="7e77d-115">Tablice odcięć są podobne do list wycinków:</span><span class="sxs-lookup"><span data-stu-id="7e77d-115">Slicing arrays is just like slicing lists:</span></span>

```fsharp
// Generate an array of 100 integers
let fullArray = [| 1 .. 100 |]

// Create a slice from indices 1-5 (inclusive)
let smallSlice = fullArray.[1..5]
printfn $"Small slice: {smallSlice}"

// Create a slice from the beginning to index 5 (inclusive)
let unboundedBeginning = fullArray.[..5]
printfn $"Unbounded beginning slice: {unboundedBeginning}"

// Create a slice from an index to the end of the list
let unboundedEnd = fullArray.[94..]
printfn $"Unbounded end slice: {unboundedEnd}"
```

## <a name="slicing-multidimensional-arrays"></a><span data-ttu-id="7e77d-116">Dzielenie tablic wielowymiarowych</span><span class="sxs-lookup"><span data-stu-id="7e77d-116">Slicing multidimensional arrays</span></span>

<span data-ttu-id="7e77d-117">Język F # obsługuje tablice wielowymiarowe w podstawowej bibliotece języka F #.</span><span class="sxs-lookup"><span data-stu-id="7e77d-117">F# supports multidimensional arrays in the F# core library.</span></span> <span data-ttu-id="7e77d-118">Podobnie jak w przypadku tablic jednowymiarowych, wycinki tablic wielowymiarowych mogą być również użyteczne.</span><span class="sxs-lookup"><span data-stu-id="7e77d-118">As with one-dimensional arrays, slices of multidimensional arrays can also be useful.</span></span> <span data-ttu-id="7e77d-119">Jednak wprowadzenie dodatkowych wymiarów zezwala na nieznacznie inną składnię, dzięki czemu można przyjmować plasterki określonych wierszy i kolumn.</span><span class="sxs-lookup"><span data-stu-id="7e77d-119">However, the introduction of additional dimensions mandates a slightly different syntax so that you can take slices of specific rows and columns.</span></span>

<span data-ttu-id="7e77d-120">W poniższych przykładach pokazano, jak wydzielić tablicę 2D:</span><span class="sxs-lookup"><span data-stu-id="7e77d-120">The following examples demonstrate how to slice a 2D array:</span></span>

```fsharp
// Generate a 3x3 2D matrix
let A = array2D [[1;2;3];[4;5;6];[7;8;9]]
printfn $"Full matrix:\n {A}"

// Take the first row
let row0 = A.[0,*]
printfn $"{row0}"

// Take the first column
let col0 = A.[*,0]
printfn $"{col0}"

// Take all rows but only two columns
let subA = A.[*,0..1]
printfn $"{subA}"

// Take two rows and all columns
let subA' = A.[0..1,*]
printfn $"{subA}"

// Slice a 2x2 matrix out of the full 3x3 matrix
let twoByTwo = A.[0..1,0..1]
printfn $"{twoByTwo}"
```

## <a name="defining-slices-for-other-data-structures"></a><span data-ttu-id="7e77d-121">Definiowanie wycinków dla innych struktur danych</span><span class="sxs-lookup"><span data-stu-id="7e77d-121">Defining slices for other data structures</span></span>

<span data-ttu-id="7e77d-122">Biblioteka podstawowa F # definiuje wycinki dla ograniczonego zestawu typów.</span><span class="sxs-lookup"><span data-stu-id="7e77d-122">The F# core library defines slices for a limited set of types.</span></span> <span data-ttu-id="7e77d-123">Jeśli chcesz zdefiniować wycinki dla większej liczby typów danych, możesz to zrobić w samej definicji typu lub w rozszerzeniu typu.</span><span class="sxs-lookup"><span data-stu-id="7e77d-123">If you wish to define slices for more data types, you can do so either in the type definition itself or in a type extension.</span></span>

<span data-ttu-id="7e77d-124">Na przykład poniżej przedstawiono sposób definiowania wycinków klasy umożliwiającej <xref:System.ArraySegment%601> wygodne manipulowanie danymi:</span><span class="sxs-lookup"><span data-stu-id="7e77d-124">For example, here's how you might define slices for the <xref:System.ArraySegment%601> class to allow for convenient data manipulation:</span></span>

```fsharp
open System

type ArraySegment<'TItem> with
    member segment.GetSlice(start, finish) =
        let start = defaultArg start 0
        let finish = defaultArg finish segment.Count
        ArraySegment(segment.Array, segment.Offset + start, finish - start)

let arr = ArraySegment [| 1 .. 10 |]
let slice = arr.[2..5] //[ 3; 4; 5]
```

<span data-ttu-id="7e77d-125">Inny przykład użycia <xref:System.Span%601> typów i <xref:System.ReadOnlySpan%601> :</span><span class="sxs-lookup"><span data-stu-id="7e77d-125">Another example using the <xref:System.Span%601> and <xref:System.ReadOnlySpan%601> types:</span></span>

```fsharp
open System

type ReadOnlySpan<'T> with
    member sp.GetSlice(startIdx, endIdx) =
        let s = defaultArg startIdx 0
        let e = defaultArg endIdx sp.Length
        sp.Slice(s, e - s)

type Span<'T> with
    member sp.GetSlice(startIdx, endIdx) =
        let s = defaultArg startIdx 0
        let e = defaultArg endIdx sp.Length
        sp.Slice(s, e - s)

let printSpan (sp: Span<int>) =
    let arr = sp.ToArray()
    printfn $"{arr}"

let sp = [| 1; 2; 3; 4; 5 |].AsSpan()
printSpan sp.[0..] // [|1; 2; 3; 4; 5|]
printSpan sp.[..5] // [|1; 2; 3; 4; 5|]
printSpan sp.[0..3] // [|1; 2; 3|]
printSpan sp.[1..3] // |2; 3|]
```

## <a name="built-in-f-slices-are-end-inclusive"></a><span data-ttu-id="7e77d-126">Wbudowane wycinki języka F # to wszystko końcowe</span><span class="sxs-lookup"><span data-stu-id="7e77d-126">Built-in F# slices are end-inclusive</span></span>

<span data-ttu-id="7e77d-127">Wszystkie wycinki wewnętrzne w języku F # są końcowe włącznie; oznacza to, że górna granica jest uwzględniona w wycinku.</span><span class="sxs-lookup"><span data-stu-id="7e77d-127">All intrinsic slices in F# are end-inclusive; that is, the upper bound is included in the slice.</span></span> <span data-ttu-id="7e77d-128">Dla danego wycinka z indeksem początkowym `x` i końcowym indeksem `y` , powstający wycink będzie zawierać wartość *Yth* .</span><span class="sxs-lookup"><span data-stu-id="7e77d-128">For a given slice with starting index `x` and ending index `y`, the resulting slice will include the *yth* value.</span></span>

```fsharp
// Define a new list
let xs = [1 .. 10]

printfn $"{xs.[2..5]}" // Includes the 5th index
```

## <a name="built-in-f-empty-slices"></a><span data-ttu-id="7e77d-129">Wbudowane puste wycinki języka F #</span><span class="sxs-lookup"><span data-stu-id="7e77d-129">Built-in F# empty slices</span></span>

<span data-ttu-id="7e77d-130">Listy języka F #, tablice, sekwencje, ciągi, wielowymiarowe (2D, 3D, 4D) będą generować pusty plasterek, Jeśli składnia może utworzyć wycinek, który nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="7e77d-130">F# lists, arrays, sequences, strings, multidimensional (2D, 3D, 4D) arrays will all produce an empty slice if the syntax could produce a slice that doesn't exist.</span></span>

<span data-ttu-id="7e77d-131">Rozpatrzmy następujący przykład:</span><span class="sxs-lookup"><span data-stu-id="7e77d-131">Consider the following example:</span></span>

```fsharp
let l = [ 1..10 ]
let a = [| 1..10 |]
let s = "hello!"

let emptyList = l.[-2..(-1)]
let emptyArray = a.[-2..(-1)]
let emptyString = s.[-2..(-1)]
```

> [!IMPORTANT]
> <span data-ttu-id="7e77d-132">Deweloperzy języka C# mogą oczekiwać, że nie generują pustego wycinka.</span><span class="sxs-lookup"><span data-stu-id="7e77d-132">C# developers may expect these to throw an exception rather than produce an empty slice.</span></span> <span data-ttu-id="7e77d-133">Jest to podjęcie decyzji dotyczącej projektu w przypadku, gdy puste kolekcje tworzą w języku F #.</span><span class="sxs-lookup"><span data-stu-id="7e77d-133">This is a design decision rooted in the fact that empty collections compose in F#.</span></span> <span data-ttu-id="7e77d-134">Pusta lista języka F # może być złożona z inną listą języka F #, pusty ciąg może zostać dodany do istniejącego ciągu i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="7e77d-134">An empty F# list can be composed with another F# list, an empty string can be added to an existing string, and so on.</span></span> <span data-ttu-id="7e77d-135">Może to być typowe dla wycinków na podstawie wartości przeprowadzonych jako parametry i odporności poza granice > przez wygenerowanie pustej kolekcji dopasowuje się do charakteru składowej kodu F #.</span><span class="sxs-lookup"><span data-stu-id="7e77d-135">It can be common to take slices based on values passed in as parameters, and being tolerant of out-of-bounds > by producing an empty collection fits with the compositional nature of F# code.</span></span>

## <a name="fixed-index-slices-for-3d-and-4d-arrays"></a><span data-ttu-id="7e77d-136">Wycinków o stałym indeksie dla tablic 3W i 4D</span><span class="sxs-lookup"><span data-stu-id="7e77d-136">Fixed-index slices for 3D and 4D arrays</span></span>

<span data-ttu-id="7e77d-137">W przypadku tablic języka F # 3D i 4D można poprawić określony indeks i wydzielić Inne wymiary przy użyciu tego indeksu.</span><span class="sxs-lookup"><span data-stu-id="7e77d-137">For F# 3D and 4D arrays, you can "fix" a particular index and slice other dimensions with that index fixed.</span></span>

<span data-ttu-id="7e77d-138">Aby to zilustrować, weź pod uwagę następującą tablicę 3W:</span><span class="sxs-lookup"><span data-stu-id="7e77d-138">To illustrate this, consider the following 3D array:</span></span>

<span data-ttu-id="7e77d-139">*z = 0*</span><span class="sxs-lookup"><span data-stu-id="7e77d-139">*z = 0*</span></span>

| <span data-ttu-id="7e77d-140">x\y</span><span class="sxs-lookup"><span data-stu-id="7e77d-140">x\y</span></span>   | <span data-ttu-id="7e77d-141">0</span><span class="sxs-lookup"><span data-stu-id="7e77d-141">0</span></span> | <span data-ttu-id="7e77d-142">1</span><span class="sxs-lookup"><span data-stu-id="7e77d-142">1</span></span> |
|-------|---|---|
| <span data-ttu-id="7e77d-143">**0**</span><span class="sxs-lookup"><span data-stu-id="7e77d-143">**0**</span></span> | <span data-ttu-id="7e77d-144">0</span><span class="sxs-lookup"><span data-stu-id="7e77d-144">0</span></span> | <span data-ttu-id="7e77d-145">1</span><span class="sxs-lookup"><span data-stu-id="7e77d-145">1</span></span> |
| <span data-ttu-id="7e77d-146">**1**</span><span class="sxs-lookup"><span data-stu-id="7e77d-146">**1**</span></span> | <span data-ttu-id="7e77d-147">2</span><span class="sxs-lookup"><span data-stu-id="7e77d-147">2</span></span> | <span data-ttu-id="7e77d-148">3</span><span class="sxs-lookup"><span data-stu-id="7e77d-148">3</span></span> |

<span data-ttu-id="7e77d-149">*z = 1*</span><span class="sxs-lookup"><span data-stu-id="7e77d-149">*z = 1*</span></span>

| <span data-ttu-id="7e77d-150">x\y</span><span class="sxs-lookup"><span data-stu-id="7e77d-150">x\y</span></span>   | <span data-ttu-id="7e77d-151">0</span><span class="sxs-lookup"><span data-stu-id="7e77d-151">0</span></span> | <span data-ttu-id="7e77d-152">1</span><span class="sxs-lookup"><span data-stu-id="7e77d-152">1</span></span> |
|-------|---|---|
| <span data-ttu-id="7e77d-153">**0**</span><span class="sxs-lookup"><span data-stu-id="7e77d-153">**0**</span></span> | <span data-ttu-id="7e77d-154">4</span><span class="sxs-lookup"><span data-stu-id="7e77d-154">4</span></span> | <span data-ttu-id="7e77d-155">5</span><span class="sxs-lookup"><span data-stu-id="7e77d-155">5</span></span> |
| <span data-ttu-id="7e77d-156">**1**</span><span class="sxs-lookup"><span data-stu-id="7e77d-156">**1**</span></span> | <span data-ttu-id="7e77d-157">6</span><span class="sxs-lookup"><span data-stu-id="7e77d-157">6</span></span> | <span data-ttu-id="7e77d-158">7</span><span class="sxs-lookup"><span data-stu-id="7e77d-158">7</span></span> |

<span data-ttu-id="7e77d-159">Jeśli chcesz wyodrębnić wycinek `[| 4; 5 |]` z tablicy, użyj wycinka o stałym indeksie.</span><span class="sxs-lookup"><span data-stu-id="7e77d-159">If you want to extract the slice `[| 4; 5 |]` from the array, use a fixed-index slice.</span></span>

```fsharp
let dim = 2
let m = Array3D.zeroCreate<int> dim dim dim

let mutable count = 0

for z in 0..dim-1 do
    for y in 0..dim-1 do
        for x in 0..dim-1 do
            m.[x,y,z] <- count
            count <- count + 1

// Now let's get the [4;5] slice!
m.[*, 0, 1]
```

<span data-ttu-id="7e77d-160">Ostatni wiersz naprawia `y` i `z` indeksuje tablicę 3W i pobiera resztę `x` wartości, które odpowiadają macierzy.</span><span class="sxs-lookup"><span data-stu-id="7e77d-160">The last line fixes the `y` and `z` indices of the 3D array and takes the rest of the `x` values that correspond to the matrix.</span></span>

## <a name="see-also"></a><span data-ttu-id="7e77d-161">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="7e77d-161">See also</span></span>

- [<span data-ttu-id="7e77d-162">Właściwości indeksowane</span><span class="sxs-lookup"><span data-stu-id="7e77d-162">Indexed properties</span></span>](./members/indexed-properties.md)
