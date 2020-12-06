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
# <a name="the-fixed-keyword"></a>FIXED — słowo kluczowe

`fixed`Słowo kluczowe pozwala na "przypiąć" na stosie, aby uniemożliwić jego zbieranie lub przenoszenie podczas odzyskiwania pamięci.  Jest ona używana w scenariuszach programowania niskiego poziomu.

## <a name="syntax"></a>Składnia

```fsharp
use ptr = fixed expression
```

## <a name="remarks"></a>Uwagi

Rozszerza to składnię wyrażeń, aby umożliwić wyodrębnienie wskaźnika i powiązanie go z nazwą, która nie może być zbierana lub przenoszona podczas zbierania elementów bezużytecznych.  

Wskaźnik z wyrażenia jest ustalony za pomocą `fixed` słowa kluczowego jest powiązane z identyfikatorem za pomocą `use` słowa kluczowego.  Semantyka tej metody przypomina zarządzanie zasobami za pomocą `use` słowa kluczowego.  Wskaźnik zostanie naprawiony, gdy znajduje się w zakresie, a poza zakresem, nie jest już naprawiony.  `fixed` nie można użyć poza kontekstem `use` powiązania.  Należy powiązać wskaźnik z nazwą z `use` .

Użycie `fixed` musi następować wewnątrz wyrażenia w funkcji lub metodzie.  Nie można jej użyć w zakresie skryptu lub poziomu modułu.

Podobnie jak w przypadku wszystkich kodów wskaźnika, jest to niebezpieczna funkcja i emituje ostrzeżenie, gdy zostanie użyta.

## <a name="example"></a>Przykład

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

## <a name="see-also"></a>Zobacz także

- [Moduł NativePtr](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-nativeinterop-nativeptrmodule.html)
