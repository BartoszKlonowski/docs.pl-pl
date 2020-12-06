---
title: Byrefs
description: 'Dowiedz się więcej na temat typów ByRef i ByRef w języku F #, które są używane do programowania niskiego poziomu.'
ms.date: 11/04/2019
ms.openlocfilehash: ff2c06d8940f7341d5d8b1d942be264bfac586c5
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96740318"
---
# <a name="byrefs"></a><span data-ttu-id="7f464-103">Byrefs</span><span class="sxs-lookup"><span data-stu-id="7f464-103">Byrefs</span></span>

<span data-ttu-id="7f464-104">Język F # ma dwa główne obszary funkcji, które zajmują miejsce w programowaniu niskiego poziomu:</span><span class="sxs-lookup"><span data-stu-id="7f464-104">F# has two major feature areas that deal in the space of low-level programming:</span></span>

* <span data-ttu-id="7f464-105">`byref` / `inref` / `outref` Typy, które są wskaźnikami zarządzanymi.</span><span class="sxs-lookup"><span data-stu-id="7f464-105">The `byref`/`inref`/`outref` types, which are managed pointers.</span></span> <span data-ttu-id="7f464-106">Mają ograniczenia dotyczące użycia, dzięki czemu nie można skompilować programu, który jest nieprawidłowy w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="7f464-106">They have restrictions on usage so that you cannot compile a program that is invalid at run time.</span></span>
* <span data-ttu-id="7f464-107">Struktury `byref` podobnej do [struktury](structures.md) , która ma podobną semantykę i te same ograniczenia czasu kompilacji, co `byref<'T>` .</span><span class="sxs-lookup"><span data-stu-id="7f464-107">A `byref`-like struct, which is a [structure](structures.md) that has similar semantics and the same compile-time restrictions as `byref<'T>`.</span></span> <span data-ttu-id="7f464-108">Przykładem jest <xref:System.Span%601> .</span><span class="sxs-lookup"><span data-stu-id="7f464-108">One example is <xref:System.Span%601>.</span></span>

## <a name="syntax"></a><span data-ttu-id="7f464-109">Składnia</span><span class="sxs-lookup"><span data-stu-id="7f464-109">Syntax</span></span>

```fsharp
// Byref types as parameters
let f (x: byref<'T>) = ()
let g (x: inref<'T>) = ()
let h (x: outref<'T>) = ()

// Calling a function with a byref parameter
let mutable x = 3
f &x

// Declaring a byref-like struct
open System.Runtime.CompilerServices

[<Struct; IsByRefLike>]
type S(count1: int, count2: int) =
    member x.Count1 = count1
    member x.Count2 = count2
```

## <a name="byref-inref-and-outref"></a><span data-ttu-id="7f464-110">ByRef, inref i outref</span><span class="sxs-lookup"><span data-stu-id="7f464-110">Byref, inref, and outref</span></span>

<span data-ttu-id="7f464-111">Istnieją trzy formy `byref` :</span><span class="sxs-lookup"><span data-stu-id="7f464-111">There are three forms of `byref`:</span></span>

* <span data-ttu-id="7f464-112">`inref<'T>`, zarządzany wskaźnik odczytu wartości źródłowej.</span><span class="sxs-lookup"><span data-stu-id="7f464-112">`inref<'T>`, a managed pointer for reading the underlying value.</span></span>
* <span data-ttu-id="7f464-113">`outref<'T>`, zarządzany wskaźnik zapisu do podstawowej wartości.</span><span class="sxs-lookup"><span data-stu-id="7f464-113">`outref<'T>`, a managed pointer for writing to the underlying value.</span></span>
* <span data-ttu-id="7f464-114">`byref<'T>`zarządzany wskaźnik służący do odczytywania i zapisywania podstawowej wartości.</span><span class="sxs-lookup"><span data-stu-id="7f464-114">`byref<'T>`, a managed pointer for reading and writing the underlying value.</span></span>

<span data-ttu-id="7f464-115">`byref<'T>`Można przesłać w miejscu, w którym `inref<'T>` jest oczekiwany.</span><span class="sxs-lookup"><span data-stu-id="7f464-115">A `byref<'T>` can be passed where an `inref<'T>` is expected.</span></span> <span data-ttu-id="7f464-116">Podobnie `byref<'T>` można przesłać, gdzie `outref<'T>` oczekiwano.</span><span class="sxs-lookup"><span data-stu-id="7f464-116">Similarly, a `byref<'T>` can be passed where an `outref<'T>` is expected.</span></span>

## <a name="using-byrefs"></a><span data-ttu-id="7f464-117">Korzystanie z ByRef</span><span class="sxs-lookup"><span data-stu-id="7f464-117">Using byrefs</span></span>

<span data-ttu-id="7f464-118">Aby użyć `inref<'T>` , należy uzyskać wartość wskaźnika przy użyciu `&` :</span><span class="sxs-lookup"><span data-stu-id="7f464-118">To use a `inref<'T>`, you need to get a pointer value with `&`:</span></span>

```fsharp
open System

let f (dt: inref<DateTime>) =
    printfn $"Now: %O{dt}"

let usage =
    let dt = DateTime.Now
    f &dt // Pass a pointer to 'dt'
```

<span data-ttu-id="7f464-119">Aby zapisać na wskaźniku przy użyciu `outref<'T>` lub `byref<'T>` , należy również wprowadzić wartość, do której będzie można uzyskać wskaźnik `mutable` .</span><span class="sxs-lookup"><span data-stu-id="7f464-119">To write to the pointer by using an `outref<'T>` or `byref<'T>`, you must also make the value you grab a pointer to `mutable`.</span></span>

```fsharp
open System

let f (dt: byref<DateTime>) =
    printfn $"Now: %O{dt}"
    dt <- DateTime.Now

// Make 'dt' mutable
let mutable dt = DateTime.Now

// Now you can pass the pointer to 'dt'
f &dt
```

<span data-ttu-id="7f464-120">Jeśli chcesz tylko napisać wskaźnik zamiast odczytywać go, rozważ użycie `outref<'T>` zamiast `byref<'T>` .</span><span class="sxs-lookup"><span data-stu-id="7f464-120">If you are only writing the pointer instead of reading it, consider using `outref<'T>` instead of `byref<'T>`.</span></span>

### <a name="inref-semantics"></a><span data-ttu-id="7f464-121">Semantyka Inref</span><span class="sxs-lookup"><span data-stu-id="7f464-121">Inref semantics</span></span>

<span data-ttu-id="7f464-122">Spójrzmy na poniższy kod:</span><span class="sxs-lookup"><span data-stu-id="7f464-122">Consider the following code:</span></span>

```fsharp
let f (x: inref<SomeStruct>) = x.SomeField
```

<span data-ttu-id="7f464-123">Semantycznie:</span><span class="sxs-lookup"><span data-stu-id="7f464-123">Semantically, this means the following:</span></span>

* <span data-ttu-id="7f464-124">Symbol zastępczy `x` wskaźnika może używać go tylko do odczytu wartości.</span><span class="sxs-lookup"><span data-stu-id="7f464-124">The holder of the `x` pointer may only use it to read the value.</span></span>
* <span data-ttu-id="7f464-125">Dowolny wskaźnik uzyskany do `struct` pól zagnieżdżonych w ramach `SomeStruct` danego typu `inref<_>` .</span><span class="sxs-lookup"><span data-stu-id="7f464-125">Any pointer acquired to `struct` fields nested within `SomeStruct` are given type `inref<_>`.</span></span>

<span data-ttu-id="7f464-126">Spełnione są również następujące kwestie:</span><span class="sxs-lookup"><span data-stu-id="7f464-126">The following is also true:</span></span>

* <span data-ttu-id="7f464-127">Nie ma żadnego znaczenia, że inne wątki lub aliasy nie mają dostępu do zapisu `x` .</span><span class="sxs-lookup"><span data-stu-id="7f464-127">There is no implication that other threads or aliases do not have write access to `x`.</span></span>
* <span data-ttu-id="7f464-128">Nie ma żadnych implikacji, które `SomeStruct` są niezmienne w wyniku `x` `inref` .</span><span class="sxs-lookup"><span data-stu-id="7f464-128">There is no implication that `SomeStruct` is immutable by virtue of `x` being an `inref`.</span></span>

<span data-ttu-id="7f464-129">Jednak dla typów wartości języka F #, które **są** niezmienne, `this` wskaźnik jest wywnioskowany jako `inref` .</span><span class="sxs-lookup"><span data-stu-id="7f464-129">However, for F# value types that **are** immutable, the `this` pointer is inferred to be an `inref`.</span></span>

<span data-ttu-id="7f464-130">Wszystkie te reguły razem oznaczają, że posiadacz `inref` wskaźnika nie modyfikuje natychmiastowej zawartości wskazanej pamięci.</span><span class="sxs-lookup"><span data-stu-id="7f464-130">All of these rules together mean that the holder of an `inref` pointer may not modify the immediate contents of the memory being pointed to.</span></span>

### <a name="outref-semantics"></a><span data-ttu-id="7f464-131">Semantyka Outref</span><span class="sxs-lookup"><span data-stu-id="7f464-131">Outref semantics</span></span>

<span data-ttu-id="7f464-132">Celem `outref<'T>` jest wskazanie, że na wskaźniku należy tylko pisać.</span><span class="sxs-lookup"><span data-stu-id="7f464-132">The purpose of `outref<'T>` is to indicate that the pointer should only be written to.</span></span> <span data-ttu-id="7f464-133">Nieoczekiwanie `outref<'T>` zezwala na odczytywanie wartości źródłowej pomimo jej nazwy.</span><span class="sxs-lookup"><span data-stu-id="7f464-133">Unexpectedly, `outref<'T>` permits reading the underlying value despite its name.</span></span> <span data-ttu-id="7f464-134">Jest to przeznaczone do celów zgodności.</span><span class="sxs-lookup"><span data-stu-id="7f464-134">This is for compatibility purposes.</span></span> <span data-ttu-id="7f464-135">Semantyka `outref<'T>` nie różni się od `byref<'T>` .</span><span class="sxs-lookup"><span data-stu-id="7f464-135">Semantically, `outref<'T>` is no different than `byref<'T>`.</span></span>

### <a name="interop-with-c"></a><span data-ttu-id="7f464-136">Współdziałanie z C\#</span><span class="sxs-lookup"><span data-stu-id="7f464-136">Interop with C\#</span></span>

<span data-ttu-id="7f464-137">Język C# obsługuje `in ref` `out ref` słowa kluczowe i, a nie `ref` zwraca.</span><span class="sxs-lookup"><span data-stu-id="7f464-137">C# supports the `in ref` and `out ref` keywords, in addition to `ref` returns.</span></span> <span data-ttu-id="7f464-138">W poniższej tabeli przedstawiono, w jaki sposób F # interpretuje, co emituje w języku C#:</span><span class="sxs-lookup"><span data-stu-id="7f464-138">The following table shows how F# interprets what C# emits:</span></span>

|<span data-ttu-id="7f464-139">Konstrukcja języka C#</span><span class="sxs-lookup"><span data-stu-id="7f464-139">C# construct</span></span>|<span data-ttu-id="7f464-140">Liczba wniosku w języku F #</span><span class="sxs-lookup"><span data-stu-id="7f464-140">F# infers</span></span>|
|------------|---------|
|<span data-ttu-id="7f464-141">`ref` wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="7f464-141">`ref` return value</span></span>|`outref<'T>`|
|<span data-ttu-id="7f464-142">`ref readonly` wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="7f464-142">`ref readonly` return value</span></span>|`inref<'T>`|
|<span data-ttu-id="7f464-143">`in ref` konstruktora</span><span class="sxs-lookup"><span data-stu-id="7f464-143">`in ref` parameter</span></span>|`inref<'T>`|
|<span data-ttu-id="7f464-144">`out ref` konstruktora</span><span class="sxs-lookup"><span data-stu-id="7f464-144">`out ref` parameter</span></span>|`outref<'T>`|

<span data-ttu-id="7f464-145">W poniższej tabeli pokazano, co emituje F #:</span><span class="sxs-lookup"><span data-stu-id="7f464-145">The following table shows what F# emits:</span></span>

|<span data-ttu-id="7f464-146">Konstrukcja języka F #</span><span class="sxs-lookup"><span data-stu-id="7f464-146">F# construct</span></span>|<span data-ttu-id="7f464-147">Wyemitowana konstrukcja</span><span class="sxs-lookup"><span data-stu-id="7f464-147">Emitted construct</span></span>|
|------------|-----------------|
|<span data-ttu-id="7f464-148">Argument `inref<'T>`</span><span class="sxs-lookup"><span data-stu-id="7f464-148">`inref<'T>` argument</span></span>|<span data-ttu-id="7f464-149">`[In]` atrybut argumentu</span><span class="sxs-lookup"><span data-stu-id="7f464-149">`[In]` attribute on argument</span></span>|
|<span data-ttu-id="7f464-150">`inref<'T>` przesłać</span><span class="sxs-lookup"><span data-stu-id="7f464-150">`inref<'T>` return</span></span>|<span data-ttu-id="7f464-151">`modreq` atrybut wartości</span><span class="sxs-lookup"><span data-stu-id="7f464-151">`modreq` attribute on value</span></span>|
|<span data-ttu-id="7f464-152">`inref<'T>` w nieabstrakcyjnym gnieździe lub implementacji</span><span class="sxs-lookup"><span data-stu-id="7f464-152">`inref<'T>` in abstract slot or implementation</span></span>|<span data-ttu-id="7f464-153">`modreq` on argument lub Return</span><span class="sxs-lookup"><span data-stu-id="7f464-153">`modreq` on argument or return</span></span>|
|<span data-ttu-id="7f464-154">Argument `outref<'T>`</span><span class="sxs-lookup"><span data-stu-id="7f464-154">`outref<'T>` argument</span></span>|<span data-ttu-id="7f464-155">`[Out]` atrybut argumentu</span><span class="sxs-lookup"><span data-stu-id="7f464-155">`[Out]` attribute on argument</span></span>|

### <a name="type-inference-and-overloading-rules"></a><span data-ttu-id="7f464-156">Wnioskowanie o typie i reguły przeciążania</span><span class="sxs-lookup"><span data-stu-id="7f464-156">Type inference and overloading rules</span></span>

<span data-ttu-id="7f464-157">`inref<'T>`Typ jest wnioskowany przez kompilator F # w następujących przypadkach:</span><span class="sxs-lookup"><span data-stu-id="7f464-157">An `inref<'T>` type is inferred by the F# compiler in the following cases:</span></span>

1. <span data-ttu-id="7f464-158">Parametr .NET lub zwracany typ, który ma `IsReadOnly` atrybut.</span><span class="sxs-lookup"><span data-stu-id="7f464-158">A .NET parameter or return type that has an `IsReadOnly` attribute.</span></span>
2. <span data-ttu-id="7f464-159">`this`Wskaźnik na typie struktury, który nie ma modyfikowalnych pól.</span><span class="sxs-lookup"><span data-stu-id="7f464-159">The `this` pointer on a struct type that has no mutable fields.</span></span>
3. <span data-ttu-id="7f464-160">Adres lokalizacji pamięci pochodzącej od innego `inref<_>` wskaźnika.</span><span class="sxs-lookup"><span data-stu-id="7f464-160">The address of a memory location derived from another `inref<_>` pointer.</span></span>

<span data-ttu-id="7f464-161">Gdy jest używany niejawny adres `inref` , Przeciążenie z argumentem typu `SomeType` jest preferowany do przeciążenia z argumentem typu `inref<SomeType>` .</span><span class="sxs-lookup"><span data-stu-id="7f464-161">When an implicit address of an `inref` is being taken, an overload with an argument of type `SomeType` is preferred to an overload with an argument of type `inref<SomeType>`.</span></span> <span data-ttu-id="7f464-162">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="7f464-162">For example:</span></span>

```fsharp
type C() =
    static member M(x: System.DateTime) = x.AddDays(1.0)
    static member M(x: inref<System.DateTime>) = x.AddDays(2.0)
    static member M2(x: System.DateTime, y: int) = x.AddDays(1.0)
    static member M2(x: inref<System.DateTime>, y: int) = x.AddDays(2.0)

let res = System.DateTime.Now
let v =  C.M(res)
let v2 =  C.M2(res, 4)
```

<span data-ttu-id="7f464-163">W obu przypadkach przeciążenia `System.DateTime` są rozwiązywane, a nie przez pobieranie przeciążenia `inref<System.DateTime>` .</span><span class="sxs-lookup"><span data-stu-id="7f464-163">In both cases, the overloads taking `System.DateTime` are resolved rather than the overloads taking `inref<System.DateTime>`.</span></span>

## <a name="byref-like-structs"></a><span data-ttu-id="7f464-164">Struktury podobne do ByRef</span><span class="sxs-lookup"><span data-stu-id="7f464-164">Byref-like structs</span></span>

<span data-ttu-id="7f464-165">Oprócz `byref` / `inref` / `outref` trójka można definiować własne struktury, które mogą stosować się do `byref` semantyki podobnej.</span><span class="sxs-lookup"><span data-stu-id="7f464-165">In addition to the `byref`/`inref`/`outref` trio, you can define your own structs that can adhere to `byref`-like semantics.</span></span> <span data-ttu-id="7f464-166">Jest to realizowane z <xref:System.Runtime.CompilerServices.IsByRefLikeAttribute> atrybutem:</span><span class="sxs-lookup"><span data-stu-id="7f464-166">This is done with the <xref:System.Runtime.CompilerServices.IsByRefLikeAttribute> attribute:</span></span>

```fsharp
open System
open System.Runtime.CompilerServices

[<IsByRefLike; Struct>]
type S(count1: Span<int>, count2: Span<int>) =
    member x.Count1 = count1
    member x.Count2 = count2
```

<span data-ttu-id="7f464-167">`IsByRefLike` nie oznacza `Struct` .</span><span class="sxs-lookup"><span data-stu-id="7f464-167">`IsByRefLike` does not imply `Struct`.</span></span> <span data-ttu-id="7f464-168">Oba muszą być obecne w typie.</span><span class="sxs-lookup"><span data-stu-id="7f464-168">Both must be present on the type.</span></span>

<span data-ttu-id="7f464-169">Struktura " `byref` like" w języku F # jest typem wartości powiązanej ze stosem.</span><span class="sxs-lookup"><span data-stu-id="7f464-169">A "`byref`-like" struct in F# is a stack-bound value type.</span></span> <span data-ttu-id="7f464-170">Nigdy nie jest przydzielany na zarządzanym stosie.</span><span class="sxs-lookup"><span data-stu-id="7f464-170">It is never allocated on the managed heap.</span></span> <span data-ttu-id="7f464-171">`byref`Struktura przypominająca podobne rozwiązanie jest przydatna w programowaniu o wysokiej wydajności, ponieważ jest wymuszana z zestawem silnych sprawdzeń i bez przechwycenia.</span><span class="sxs-lookup"><span data-stu-id="7f464-171">A `byref`-like struct is useful for high-performance programming, as it is enforced with set of strong checks about lifetime and non-capture.</span></span> <span data-ttu-id="7f464-172">Reguły są następujące:</span><span class="sxs-lookup"><span data-stu-id="7f464-172">The rules are:</span></span>

* <span data-ttu-id="7f464-173">Mogą one być używane jako parametry funkcji, parametry metody, zmienne lokalne, Metoda Return.</span><span class="sxs-lookup"><span data-stu-id="7f464-173">They can be used as function parameters, method parameters, local variables, method returns.</span></span>
* <span data-ttu-id="7f464-174">Nie mogą być statyczne ani składowe wystąpień klasy ani normalnej struktury.</span><span class="sxs-lookup"><span data-stu-id="7f464-174">They cannot be static or instance members of a class or normal struct.</span></span>
* <span data-ttu-id="7f464-175">Nie mogą być przechwytywane przez żadną konstrukcję zamknięcia ( `async` metody lub wyrażenia lambda).</span><span class="sxs-lookup"><span data-stu-id="7f464-175">They cannot be captured by any closure construct (`async` methods or lambda expressions).</span></span>
* <span data-ttu-id="7f464-176">Nie mogą być używane jako parametr generyczny.</span><span class="sxs-lookup"><span data-stu-id="7f464-176">They cannot be used as a generic parameter.</span></span>

<span data-ttu-id="7f464-177">Ten ostatni punkt jest decydujący dla programowania w stylu potoku języka F #, podobnie jak `|>` ogólna funkcja, która parameterizes jego typy wejściowe.</span><span class="sxs-lookup"><span data-stu-id="7f464-177">This last point is crucial for F# pipeline-style programming, as `|>` is a generic function that parameterizes its input types.</span></span> <span data-ttu-id="7f464-178">To ograniczenie może być `|>` w przyszłości swobodne, ponieważ jest wbudowane i nie wykonuje żadnych wywołań funkcji ogólnych, które nie są określone w treści.</span><span class="sxs-lookup"><span data-stu-id="7f464-178">This restriction may be relaxed for `|>` in the future, as it is inline and does not make any calls to non-inlined generic functions in its body.</span></span>

<span data-ttu-id="7f464-179">Chociaż te reguły silnie ograniczają użycie, robią to w celu zapewnienia bezpieczeństwa obliczeń o wysokiej wydajności w bezpieczny sposób.</span><span class="sxs-lookup"><span data-stu-id="7f464-179">Although these rules strongly restrict usage, they do so to fulfill the promise of high-performance computing in a safe manner.</span></span>

## <a name="byref-returns"></a><span data-ttu-id="7f464-180">Zwracane przez ByRef</span><span class="sxs-lookup"><span data-stu-id="7f464-180">Byref returns</span></span>

<span data-ttu-id="7f464-181">Funkcja ByRef zwraca z funkcji F # lub elementów członkowskich, które mogą być tworzone i używane.</span><span class="sxs-lookup"><span data-stu-id="7f464-181">Byref returns from F# functions or members can be produced and consumed.</span></span> <span data-ttu-id="7f464-182">Podczas konsumowania `byref` metody zwracanej wartość jest niejawnie wykorzystana.</span><span class="sxs-lookup"><span data-stu-id="7f464-182">When consuming a `byref`-returning method, the value is implicitly dereferenced.</span></span> <span data-ttu-id="7f464-183">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="7f464-183">For example:</span></span>

```fsharp
let squareAndPrint (data : byref<int>) =
    let squared = data*data    // data is implicitly dereferenced
    printfn $"%d{squared}"
```

<span data-ttu-id="7f464-184">Aby zwrócić wartość ByRef, zmienna, która zawiera wartość, musi znajdować się na żywo dłużej niż bieżący zakres.</span><span class="sxs-lookup"><span data-stu-id="7f464-184">To return a value byref, the variable that contains the value must live longer than the current scope.</span></span>
<span data-ttu-id="7f464-185">Ponadto, aby zwrócić element ByRef, użyj `&value` (gdzie Value jest zmienną, która jest dłuższa niż bieżący zakres).</span><span class="sxs-lookup"><span data-stu-id="7f464-185">Also, to return byref, use `&value` (where value is a variable that lives longer than the current scope).</span></span>

```fsharp
let mutable sum = 0
let safeSum (bytes: Span<byte>) =
    for i in 0 .. bytes.Length - 1 do
        sum <- sum + int bytes.[i]
    &sum  // sum lives longer than the scope of this function.
```

<span data-ttu-id="7f464-186">Aby uniknąć niejawnego odwołania, na przykład przekazywania odwołania przez wiele wywołań łańcucha, użyj `&x` (gdzie `x` jest wartością).</span><span class="sxs-lookup"><span data-stu-id="7f464-186">To avoid the implicit dereference, such as passing a reference through multiple chained calls, use `&x` (where `x` is the value).</span></span>

<span data-ttu-id="7f464-187">Możesz również bezpośrednio przypisać do powrotu `byref` .</span><span class="sxs-lookup"><span data-stu-id="7f464-187">You can also directly assign to a return `byref`.</span></span> <span data-ttu-id="7f464-188">Weź pod uwagę następujący (wysoce bezwzględny) program:</span><span class="sxs-lookup"><span data-stu-id="7f464-188">Consider the following (highly imperative) program:</span></span>

```fsharp
type C() =
    let mutable nums = [| 1; 3; 7; 15; 31; 63; 127; 255; 511; 1023 |]

    override _.ToString() = String.Join(' ', nums)

    member _.FindLargestSmallerThan(target: int) =
        let mutable ctr = nums.Length - 1

        while ctr > 0 && nums.[ctr] >= target do ctr <- ctr - 1

        if ctr > 0 then &nums.[ctr] else &nums.[0]

[<EntryPoint>]
let main argv =
    let c = C()
    printfn $"Original sequence: %O{c}"

    let v = &c.FindLargestSmallerThan 16

    v <- v*2 // Directly assign to the byref return

    printfn $"New sequence:      %O{c}"

    0 // return an integer exit code
```

<span data-ttu-id="7f464-189">Jest to produkt wyjściowy:</span><span class="sxs-lookup"><span data-stu-id="7f464-189">This is the output:</span></span>

```console
Original sequence: 1 3 7 15 31 63 127 255 511 1023
New sequence:      1 3 7 30 31 63 127 255 511 1023
```

## <a name="scoping-for-byrefs"></a><span data-ttu-id="7f464-190">Określanie zakresu dla ByRef</span><span class="sxs-lookup"><span data-stu-id="7f464-190">Scoping for byrefs</span></span>

<span data-ttu-id="7f464-191">`let`Wartość powiązania nie może mieć odwołania przekraczającego zakres, w którym został zdefiniowany.</span><span class="sxs-lookup"><span data-stu-id="7f464-191">A `let`-bound value cannot have its reference exceed the scope in which it was defined.</span></span> <span data-ttu-id="7f464-192">Na przykład następujące elementy są niedozwolone:</span><span class="sxs-lookup"><span data-stu-id="7f464-192">For example, the following is disallowed:</span></span>

```fsharp
let test2 () =
    let x = 12
    &x // Error: 'x' exceeds its defined scope!

let test () =
    let x =
        let y = 1
        &y // Error: `y` exceeds its defined scope!
    ()
```

<span data-ttu-id="7f464-193">Dzięki temu można uzyskać różne wyniki w zależności od tego, czy kompilujesz z optymalizacją.</span><span class="sxs-lookup"><span data-stu-id="7f464-193">This prevents you from getting different results depending on if you compile with optimizations or not.</span></span>
