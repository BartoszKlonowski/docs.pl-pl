---
title: Wyrażenia obiektów
description: 'Dowiedz się, jak używać wyrażeń obiektów F #, gdy chcesz uniknąć dodatkowego kodu i obciążenia wymaganego do utworzenia nowego, nazwanego typu.'
ms.date: 02/08/2019
ms.openlocfilehash: 8a3e40b7833b551eefb95ec62b935acd1ba7b1f9
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96740305"
---
# <a name="object-expressions"></a><span data-ttu-id="d5c47-103">Wyrażenia obiektów</span><span class="sxs-lookup"><span data-stu-id="d5c47-103">Object Expressions</span></span>

<span data-ttu-id="d5c47-104">*Wyrażenie obiektu* jest wyrażeniem, które tworzy nowe wystąpienie dynamicznie utworzonego, anonimowego typu obiektu, który jest oparty na istniejącym typie podstawowym, interfejsie lub zestawie interfejsów.</span><span class="sxs-lookup"><span data-stu-id="d5c47-104">An *object expression* is an expression that creates a new instance of a dynamically created, anonymous object type that is based on an existing base type, interface, or set of interfaces.</span></span>

## <a name="syntax"></a><span data-ttu-id="d5c47-105">Składnia</span><span class="sxs-lookup"><span data-stu-id="d5c47-105">Syntax</span></span>

```fsharp
// When typename is a class:
{ new typename [type-params]arguments with
    member-definitions
    [ additional-interface-definitions ]
}
// When typename is not a class:
{ new typename [generic-type-args] with
    member-definitions
    [ additional-interface-definitions ]
}
```

## <a name="remarks"></a><span data-ttu-id="d5c47-106">Uwagi</span><span class="sxs-lookup"><span data-stu-id="d5c47-106">Remarks</span></span>

<span data-ttu-id="d5c47-107">W poprzedniej składni *Właściwość TypeName* reprezentuje istniejący typ klasy lub typ interfejsu.</span><span class="sxs-lookup"><span data-stu-id="d5c47-107">In the previous syntax, the *typename* represents an existing class type or interface type.</span></span> <span data-ttu-id="d5c47-108">*Type-params* opisuje opcjonalne parametry typu ogólnego.</span><span class="sxs-lookup"><span data-stu-id="d5c47-108">*type-params* describes the optional generic type parameters.</span></span> <span data-ttu-id="d5c47-109">*Argumenty* są używane tylko dla typów klas, które wymagają parametrów konstruktora.</span><span class="sxs-lookup"><span data-stu-id="d5c47-109">The *arguments* are used only for class types, which require constructor parameters.</span></span> <span data-ttu-id="d5c47-110">*Definicje elementów członkowskich* to zastąpienia metod klasy bazowej lub implementacje metod abstrakcyjnych z klasy podstawowej lub interfejsu.</span><span class="sxs-lookup"><span data-stu-id="d5c47-110">The *member-definitions* are overrides of base class methods, or implementations of abstract methods from either a base class or an interface.</span></span>

<span data-ttu-id="d5c47-111">Poniższy przykład ilustruje kilka różnych typów wyrażeń obiektów.</span><span class="sxs-lookup"><span data-stu-id="d5c47-111">The following example illustrates several different types of object expressions.</span></span>

```fsharp
// This object expression specifies a System.Object but overrides the
// ToString method.
let obj1 = { new System.Object() with member x.ToString() = "F#" }
printfn $"{obj1}"

// This object expression implements the IFormattable interface.
let delimiter(delim1: string, delim2: string, value: string) =
    { new System.IFormattable with
        member x.ToString(format: string, provider: System.IFormatProvider) =
            if format = "D" then
                delim1 + value + delim2
            else
                value }

let obj2 = delimiter("{","}", "Bananas!");

printfn "%A" (System.String.Format("{0:D}", obj2))

// Define two interfaces
type IFirst =
  abstract F : unit -> unit
  abstract G : unit -> unit

type ISecond =
  inherit IFirst
  abstract H : unit -> unit
  abstract J : unit -> unit

// This object expression implements both interfaces.
let implementer() =
    { new ISecond with
        member this.H() = ()
        member this.J() = ()
      interface IFirst with
        member this.F() = ()
        member this.G() = () }
```

## <a name="using-object-expressions"></a><span data-ttu-id="d5c47-112">Używanie wyrażeń obiektów</span><span class="sxs-lookup"><span data-stu-id="d5c47-112">Using Object Expressions</span></span>

<span data-ttu-id="d5c47-113">Wyrażenia obiektów są używane, gdy chcesz uniknąć dodatkowego kodu i obciążenia, które jest wymagane do utworzenia nowego, nazwanego typu.</span><span class="sxs-lookup"><span data-stu-id="d5c47-113">You use object expressions when you want to avoid the extra code and overhead that is required to create a new, named type.</span></span> <span data-ttu-id="d5c47-114">Jeśli używasz wyrażeń obiektów do zminimalizowania liczby typów utworzonych w programie, możesz zmniejszyć liczbę wierszy kodu i zapobiec niepotrzebnemu rozprzestrzenianiu typów.</span><span class="sxs-lookup"><span data-stu-id="d5c47-114">If you use object expressions to minimize the number of types created in a program, you can reduce the number of lines of code and prevent the unnecessary proliferation of types.</span></span> <span data-ttu-id="d5c47-115">Zamiast tworzyć wiele typów tylko do obsługi określonych sytuacji, można użyć wyrażenia obiektu, które dostosowuje istniejący typ lub zapewnia odpowiednią implementację interfejsu dla konkretnego przypadku.</span><span class="sxs-lookup"><span data-stu-id="d5c47-115">Instead of creating many types just to handle specific situations, you can use an object expression that customizes an existing type or provides an appropriate implementation of an interface for the specific case at hand.</span></span>

## <a name="see-also"></a><span data-ttu-id="d5c47-116">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="d5c47-116">See also</span></span>

- [<span data-ttu-id="d5c47-117">Dokumentacja języka F #</span><span class="sxs-lookup"><span data-stu-id="d5c47-117">F# Language Reference</span></span>](index.md)
