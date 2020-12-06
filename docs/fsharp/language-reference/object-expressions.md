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
# <a name="object-expressions"></a>Wyrażenia obiektów

*Wyrażenie obiektu* jest wyrażeniem, które tworzy nowe wystąpienie dynamicznie utworzonego, anonimowego typu obiektu, który jest oparty na istniejącym typie podstawowym, interfejsie lub zestawie interfejsów.

## <a name="syntax"></a>Składnia

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

## <a name="remarks"></a>Uwagi

W poprzedniej składni *Właściwość TypeName* reprezentuje istniejący typ klasy lub typ interfejsu. *Type-params* opisuje opcjonalne parametry typu ogólnego. *Argumenty* są używane tylko dla typów klas, które wymagają parametrów konstruktora. *Definicje elementów członkowskich* to zastąpienia metod klasy bazowej lub implementacje metod abstrakcyjnych z klasy podstawowej lub interfejsu.

Poniższy przykład ilustruje kilka różnych typów wyrażeń obiektów.

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

## <a name="using-object-expressions"></a>Używanie wyrażeń obiektów

Wyrażenia obiektów są używane, gdy chcesz uniknąć dodatkowego kodu i obciążenia, które jest wymagane do utworzenia nowego, nazwanego typu. Jeśli używasz wyrażeń obiektów do zminimalizowania liczby typów utworzonych w programie, możesz zmniejszyć liczbę wierszy kodu i zapobiec niepotrzebnemu rozprzestrzenianiu typów. Zamiast tworzyć wiele typów tylko do obsługi określonych sytuacji, można użyć wyrażenia obiektu, które dostosowuje istniejący typ lub zapewnia odpowiednią implementację interfejsu dla konkretnego przypadku.

## <a name="see-also"></a>Zobacz także

- [Dokumentacja języka F #](index.md)
