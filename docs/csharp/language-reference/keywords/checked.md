---
description: Checked — odwołanie w C#
title: Checked — odwołanie w C#
ms.date: 07/20/2015
f1_keywords:
- checked_CSharpKeyword
- checked
helpviewer_keywords:
- checked keyword [C#]
ms.assetid: 718a1194-988d-48a3-b089-d6ee8bd1608d
ms.openlocfilehash: 4dd8bc02d3af89d6bab3aef55a88cb8b40704da6
ms.sourcegitcommit: d579fb5e4b46745fd0f1f8874c94c6469ce58604
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/30/2020
ms.locfileid: "89138283"
---
# <a name="checked-c-reference"></a>checked (odwołanie w C#)

`checked`Słowo kluczowe jest używane do jawnego włączania sprawdzania przepełnienia dla operacji arytmetycznych i konwersji typu całkowitego.

Domyślnie wyrażenie zawierające tylko stałe wartości powoduje błąd kompilatora, jeśli wyrażenie generuje wartość spoza zakresu typu docelowego. Jeśli wyrażenie zawiera jedną lub więcej wartości niestałych, kompilator nie wykrywa przepełnienia. Obliczenie wyrażenia przypisanego do `i2` w poniższym przykładzie nie powoduje błędu kompilatora.

[!code-csharp[csrefKeywordsChecked#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsChecked/CS/csrefKeywordsChecked.cs#3)]

Domyślnie te wyrażenia niestałe nie są sprawdzane w celu przepełnienia w czasie wykonywania i nie powodują wyjątków przepełnienia. W poprzednim przykładzie przedstawiono wartość-2 147 483 639 jako sumę dwóch dodatnich liczb całkowitych.

Sprawdzanie przepełnienia można włączyć przez opcje kompilatora, konfigurację środowiska lub użycie `checked` słowa kluczowego. W poniższych przykładach pokazano, jak używać `checked` wyrażenia lub `checked` bloku do wykrywania przepełnienia, który jest generowany przez poprzednią sumę w czasie wykonywania. Oba przykłady powodują wyjątek przepełnienia.

[!code-csharp[csrefKeywordsChecked#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsChecked/CS/csrefKeywordsChecked.cs#4)]

[Niesprawdzone](./unchecked.md) słowo kluczowe może służyć do zapobiegania sprawdzaniu przepełnienia.

## <a name="example"></a>Przykład

Ten przykład pokazuje, jak używać `checked` do włączania sprawdzania przepełnienia w czasie wykonywania.

[!code-csharp[csrefKeywordsChecked#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsChecked/CS/csrefKeywordsChecked.cs#1)]

## <a name="c-language-specification"></a>specyfikacja języka C#

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>Zobacz też

- [Odwołanie w C#](../index.md)
- [Przewodnik programowania w języku C#](../../programming-guide/index.md)
- [Słowa kluczowe języka C#](./index.md)
- [checked i unchecked](./checked-and-unchecked.md)
- [unchecked](./unchecked.md)
