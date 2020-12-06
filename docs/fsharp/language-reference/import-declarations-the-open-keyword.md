---
title: 'Deklaracje importowania: open — Słowo kluczowe'
description: 'Dowiedz się więcej o deklaracjach importu F # i sposobach określania modułu lub przestrzeni nazw, których elementy można odwołać bez użycia w pełni kwalifikowanej nazwy.'
ms.date: 08/15/2020
ms.openlocfilehash: 4d3fd159aa4b334e9db0d7f756047470ad9c0829
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96739688"
---
# <a name="import-declarations-the-open-keyword"></a>Deklaracje importu: `open` słowo kluczowe

*Deklaracja importu* określa moduł lub przestrzeń nazw, których elementy można odwoływać bez używania w pełni kwalifikowanej nazwy.

## <a name="syntax"></a>Składnia

```fsharp
open module-or-namespace-name
open type type-name
```

## <a name="remarks"></a>Uwagi

Odwoływanie się do kodu przy użyciu w pełni kwalifikowanej przestrzeni nazw lub ścieżki modułu za każdym razem, gdy program może utworzyć kod, który jest trudno pisać, czytać i konserwować. Zamiast tego można użyć `open` słowa kluczowego dla często używanych modułów i przestrzeni nazw, aby podczas odwoływania się do elementu członkowskiego tego modułu lub przestrzeni nazw można użyć krótkiej formy nazwy zamiast w pełni kwalifikowanej nazwy. To słowo kluczowe jest podobne do `using` słowa kluczowego w języku C#, `using namespace` w Visual C++ i `Imports` w Visual Basic.

Dostarczony moduł lub przestrzeń nazw muszą znajdować się w tym samym projekcie lub w przywoływanym projekcie lub zestawie. Jeśli tak nie jest, można dodać odwołanie do projektu lub użyć `-reference` opcji wiersza polecenia (lub jego skrótu `-r` ). Aby uzyskać więcej informacji, zobacz [Opcje kompilatora](compiler-options.md).

Deklaracja importu udostępnia nazwy dostępne w kodzie, który następuje po deklaracji, do końca otaczającej przestrzeni nazw, modułu lub pliku.

Jeśli używasz wielu deklaracji importu, powinny one pojawiać się w osobnych wierszach.

Poniższy kod ilustruje użycie `open` słowa kluczowego w celu uproszczenia kodu.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6801.fs)]

Kompilator F # nie emituje błędu lub ostrzeżenia, gdy niejasności występuje, gdy ta sama nazwa wystąpi w więcej niż jednym otwartym module lub przestrzeni nazw. Gdy wystąpi niejasności, język F # zapewnia preferencję dla ostatnio otwartego modułu lub przestrzeni nazw. Na przykład, w poniższym kodzie, oznacza, chociaż znajduje się `empty` `Seq.empty` `empty` zarówno w `List` module, jak i `Seq` .

```fsharp
open List
open Seq
printfn %"{empty}"
```

W związku z tym należy zachować ostrożność podczas otwierania modułów lub przestrzeni nazw, takich jak `List` lub zawierających `Seq` składowe o identycznych nazwach. zamiast tego należy rozważyć użycie kwalifikowanych nazw. Należy unikać każdej sytuacji, w której kod jest zależny od kolejności deklaracji importu.

## <a name="open-type-declarations"></a>Otwieranie deklaracji typu

Język F # obsługuje `open` Typ podobny do tego:

```fsharp
open type System.Math
PI
```

Spowoduje to udostępnienie wszystkich dostępnych pól statycznych i elementów członkowskich w typie.

Można również `open` określić typ [rekordu](records.md) i [Unii rozłącznych](discriminated-unions.md) , aby udostępnić statyczne elementy członkowskie. W przypadku związków rozłącznych można również uwidocznić przypadki Unii. Może to być przydatne w przypadku uzyskiwania dostępu do przypadków Unii w typie zadeklarowanym wewnątrz modułu, który może nie być otwarty, tak więc:

```fsharp
module M =
    type DU = A | B | C

    let someOtherFunction x = x + 1

// Open only the type inside the module
open type M.DU

printfn "%A" A
```

## <a name="namespaces-that-are-open-by-default"></a>Obszary nazw, które są domyślnie otwarte

Niektóre przestrzenie nazw są często używane w kodzie języka F #, które są otwierane niejawnie bez potrzeby jawnej deklaracji importu. W poniższej tabeli przedstawiono obszary nazw, które są domyślnie otwarte.

|Przestrzeń nazw|Opis|
|---------|-----------|
|`FSharp.Core`|Zawiera podstawowe definicje typu języka F # dla typów wbudowanych, takich jak `int` i `float` .|
|`FSharp.Core.Operators`|Zawiera podstawowe operacje arytmetyczne, takie jak `+` i `*` .|
|`FSharp.Collections`|Zawiera niezmienne klasy kolekcji, takie jak `List` i `Array` .|
|`FSharp.Control`|Zawiera typy dla konstrukcji kontroli, takich jak Ocena z opóźnieniem i asynchroniczne przepływy pracy.|
|`FSharp.Text`|Zawiera funkcje dla sformatowanych operacji we/wy, takich jak `printf` Funkcja.|

## <a name="autoopen-attribute"></a>AutoOpen — atrybut

Można zastosować `AutoOpen` atrybut do zestawu, jeśli chcesz automatycznie otworzyć przestrzeń nazw lub moduł, gdy odwołanie do zestawu. Można również zastosować `AutoOpen` atrybut do modułu, aby automatycznie otworzyć ten moduł po otwarciu modułu nadrzędnego lub przestrzeni nazw. Aby uzyskać więcej informacji, zobacz [AutoOpenAttribute](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-autoopenattribute.html).

## <a name="requirequalifiedaccess-attribute"></a>RequireQualifiedAccess — atrybut

Niektóre moduły, rekordy lub typy Unii mogą określać `RequireQualifiedAccess` atrybut. Gdy odwołujesz się do elementów tych modułów, rekordów lub Unii, musisz użyć kwalifikowanej nazwy bez względu na to, czy dołączysz deklarację importu. Jeśli ten atrybut jest używany strategicznie dla typów, które definiują często używane nazwy, można uniknąć kolizji nazw, a tym samym zwiększyć odporność kodu na zmiany w bibliotekach. Aby uzyskać więcej informacji, zobacz [RequireQualifiedAccessAttribute —](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-requirequalifiedaccessattribute.html).

## <a name="see-also"></a>Zobacz także

- [Dokumentacja języka F #](index.md)
- [Przestrzenie nazw](namespaces.md)
- [Moduły](modules.md)
