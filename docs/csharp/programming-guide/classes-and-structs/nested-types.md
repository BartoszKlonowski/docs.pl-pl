---
title: Typy zagnieżdżone — Przewodnik programowania w języku C#
description: Typ zdefiniowany w klasie, strukturze lub interfejsie jest nazywany typem zagnieżdżonym w języku C#.
ms.date: 02/08/2020
helpviewer_keywords:
- nested types [C#]
ms.assetid: f2e1b315-e3d1-48ce-977f-7bae0960ba99
ms.openlocfilehash: 0741ae88103b16ce34fd5a38b789beaf428e734a
ms.sourcegitcommit: 0014aa4d5cb2da56a70e03fc68f663d64df5247a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/09/2020
ms.locfileid: "96918583"
---
# <a name="nested-types-c-programming-guide"></a>Zagnieżdżone typy (Przewodnik programowania w języku C#)

Typ zdefiniowany w obrębie [klasy](../../language-reference/keywords/class.md), [struktury](../../language-reference/builtin-types/struct.md), [delegata](../../language-reference/builtin-types/reference-types.md#the-delegate-type) lub [interfejsu](../../language-reference/keywords/interface.md) jest nazywany typem zagnieżdżonym. Na przykład

[!code-csharp[DeclareNestedClass](~/samples/snippets/csharp/objectoriented/nestedtypes.cs#DeclareNestedClass)]

Niezależnie od tego, czy typ zewnętrzny jest klasą, interfejsem lub strukturą, zagnieżdżone typy domyślne to [Private](../../language-reference/keywords/private.md); są one dostępne tylko z tego typu zawierającego. W poprzednim przykładzie `Nested` Klasa jest niedostępna dla typów zewnętrznych.

Można również określić [modyfikator dostępu](../../language-reference/keywords/access-modifiers.md) , aby zdefiniować dostępność typu zagnieżdżonego w następujący sposób:

- Zagnieżdżone typy **klasy** mogą być [publiczne](../../language-reference/keywords/public.md), [chronione](../../language-reference/keywords/protected.md), [wewnętrzne](../../language-reference/keywords/internal.md), [chronione wewnętrznie](../../language-reference/keywords/protected-internal.md), [prywatne](../../language-reference/keywords/private.md) i [prywatne](../../language-reference/keywords/private-protected.md).

   Jednak zdefiniowanie `protected` klasy, `protected internal` lub `private protected` Klasa zagnieżdżona wewnątrz [klasy zapieczętowanej](../../language-reference/keywords/sealed.md) generuje ostrzeżenie kompilatora [CS0628](../../misc/cs0628.md), "Nowa chroniona składowa zadeklarowana w klasie zapieczętowanej".
  
- Zagnieżdżone typy **struktury** mogą być [publiczne](../../language-reference/keywords/public.md), [wewnętrzne](../../language-reference/keywords/internal.md)lub [prywatne](../../language-reference/keywords/private.md).

W poniższym przykładzie Klasa jest `Nested` publiczna:

[!code-csharp[PublicNestedClass](~/samples/snippets/csharp/objectoriented/nestedtypes.cs#PublicNestedClass)]

Zagnieżdżony, lub wewnętrzny, typ może uzyskać dostęp do typu zawierającego lub zewnątrz. Aby uzyskać dostęp do typu zawierającego, przekaż go jako argument do konstruktora typu zagnieżdżonego. Na przykład:

[!code-csharp[DeclareNestedInstance](~/samples/snippets/csharp/objectoriented/nestedtypes.cs#DeclareNestedInstance)]

Typ zagnieżdżony ma dostęp do wszystkich elementów członkowskich, które są dostępne dla typu zawierającego. Może uzyskiwać dostęp do prywatnych i chronionych składowych typu zawierającego, w tym wszystkich dziedziczonych chronionych elementów członkowskich.

W poprzedniej deklaracji, pełna nazwa klasy `Nested` to `Container.Nested` . Jest to nazwa używana do tworzenia nowego wystąpienia klasy zagnieżdżonej w następujący sposób:

[!code-csharp[UseNestedInstance](~/samples/snippets/csharp/objectoriented/nestedtypes.cs#UseNestedInstance)]

## <a name="see-also"></a>Zobacz też

- [Przewodnik programowania w języku C#](../index.md)
- [Klasy i struktury](./index.md)
- [Modyfikatory dostępu](./access-modifiers.md)
- [Konstruktory](./constructors.md)
