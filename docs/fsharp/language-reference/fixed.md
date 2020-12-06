---
title: FIXED — słowo kluczowe
description: Dowiedz się, jak za pomocą słowa kluczowego "Fixed" można przypiąć element jako lokalny na stosie.
ms.date: 08/15/2020
ms.openlocfilehash: b4b0d1ae101d5f7b65bff80fa070c9fd54de8d66
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96740357"
---
# <a name="the-fixed-keyword"></a><span data-ttu-id="a5a68-103">FIXED — słowo kluczowe</span><span class="sxs-lookup"><span data-stu-id="a5a68-103">The fixed keyword</span></span>

<span data-ttu-id="a5a68-104">`fixed`Słowo kluczowe pozwala na "przypiąć" na stosie, aby uniemożliwić jego zbieranie lub przenoszenie podczas odzyskiwania pamięci.</span><span class="sxs-lookup"><span data-stu-id="a5a68-104">The `fixed` keyword allows you to "pin" a local onto the stack to prevent it from being collected or moved during garbage-collection.</span></span>  <span data-ttu-id="a5a68-105">Jest ona używana w scenariuszach programowania niskiego poziomu.</span><span class="sxs-lookup"><span data-stu-id="a5a68-105">It is used for low-level programming scenarios.</span></span>

## <a name="syntax"></a><span data-ttu-id="a5a68-106">Składnia</span><span class="sxs-lookup"><span data-stu-id="a5a68-106">Syntax</span></span>

```fsharp
use ptr = fixed expression
```

## <a name="remarks"></a><span data-ttu-id="a5a68-107">Uwagi</span><span class="sxs-lookup"><span data-stu-id="a5a68-107">Remarks</span></span>

<span data-ttu-id="a5a68-108">Rozszerza to składnię wyrażeń, aby umożliwić wyodrębnienie wskaźnika i powiązanie go z nazwą, która nie może być zbierana lub przenoszona podczas zbierania elementów bezużytecznych.</span><span class="sxs-lookup"><span data-stu-id="a5a68-108">This extends the syntax of expressions to allow extracting a pointer and binding it to a name which is prevented from being collected or moved during garbage-collection.</span></span>  

<span data-ttu-id="a5a68-109">Wskaźnik z wyrażenia jest ustalony za pomocą `fixed` słowa kluczowego jest powiązane z identyfikatorem za pomocą `use` słowa kluczowego.</span><span class="sxs-lookup"><span data-stu-id="a5a68-109">A pointer from an expression is fixed via the `fixed` keyword is bound to an identifier via the `use` keyword.</span></span>  <span data-ttu-id="a5a68-110">Semantyka tej metody przypomina zarządzanie zasobami za pomocą `use` słowa kluczowego.</span><span class="sxs-lookup"><span data-stu-id="a5a68-110">The semantics of this are similar to resource management via the `use` keyword.</span></span>  <span data-ttu-id="a5a68-111">Wskaźnik zostanie naprawiony, gdy znajduje się w zakresie, a poza zakresem, nie jest już naprawiony.</span><span class="sxs-lookup"><span data-stu-id="a5a68-111">The pointer is fixed while it is in scope, and once it is out of scope, it is no longer fixed.</span></span>  <span data-ttu-id="a5a68-112">`fixed` nie można użyć poza kontekstem `use` powiązania.</span><span class="sxs-lookup"><span data-stu-id="a5a68-112">`fixed` cannot be used outside the context of a `use` binding.</span></span>  <span data-ttu-id="a5a68-113">Należy powiązać wskaźnik z nazwą z `use` .</span><span class="sxs-lookup"><span data-stu-id="a5a68-113">You must bind the pointer to a name with `use`.</span></span>

<span data-ttu-id="a5a68-114">Użycie `fixed` musi następować wewnątrz wyrażenia w funkcji lub metodzie.</span><span class="sxs-lookup"><span data-stu-id="a5a68-114">Use of `fixed` must occur within an expression in a function or a method.</span></span>  <span data-ttu-id="a5a68-115">Nie można jej użyć w zakresie skryptu lub poziomu modułu.</span><span class="sxs-lookup"><span data-stu-id="a5a68-115">It cannot be used at a script-level or module-level scope.</span></span>

<span data-ttu-id="a5a68-116">Podobnie jak w przypadku wszystkich kodów wskaźnika, jest to niebezpieczna funkcja i emituje ostrzeżenie, gdy zostanie użyta.</span><span class="sxs-lookup"><span data-stu-id="a5a68-116">Like all pointer code, this is an unsafe feature and will emit a warning when used.</span></span>

## <a name="example"></a><span data-ttu-id="a5a68-117">Przykład</span><span class="sxs-lookup"><span data-stu-id="a5a68-117">Example</span></span>

```fsharp
open Microsoft.FSharp.NativeInterop

type Point = { mutable X: int; mutable Y: int}

let squareWithPointer (p: nativeptr<int>) =
    // Dereference the pointer at the 0th address.
    let mutable value = NativePtr.get p 0

    // Perform some work
    value <- value * value

    // Set the value in the pointer at the 0th address.
    NativePtr.set p 0 value

let pnt = { X = 1; Y = 2 }
printfn $"pnt before - X: %d{pnt.X} Y: %d{pnt.Y}" // prints 1 and 2

// Note that the use of 'fixed' is inside a function.
// You cannot fix a pointer at a script-level or module-level scope.
let doPointerWork() =
    use ptr = fixed &pnt.Y

    // Square the Y value
    squareWithPointer ptr
    printfn $"pnt after - X: %d{pnt.X} Y: %d{pnt.Y}" // prints 1 and 4

doPointerWork()
```

## <a name="see-also"></a><span data-ttu-id="a5a68-118">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="a5a68-118">See also</span></span>

- [<span data-ttu-id="a5a68-119">Moduł NativePtr</span><span class="sxs-lookup"><span data-stu-id="a5a68-119">NativePtr Module</span></span>](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-nativeinterop-nativeptrmodule.html)
