---
description: Odwołanie do języka C#
title: Odwołanie do języka C#
ms.date: 05/28/2018
f1_keywords:
- do_CSharpKeyword
- do
helpviewer_keywords:
- do keyword [C#]
ms.assetid: 50725f79-9ba6-4898-aa78-6e331568a1bb
ms.openlocfilehash: 601231f23a58e8af8339a733677f0bbd92bb4ffc
ms.sourcegitcommit: d579fb5e4b46745fd0f1f8874c94c6469ce58604
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/30/2020
ms.locfileid: "89126960"
---
# <a name="do-c-reference"></a>do (odwołanie w C#)

`do`Instrukcja wykonuje instrukcję lub blok instrukcji, gdy określone wyrażenie logiczne zwraca wartość `true` . Ponieważ to wyrażenie jest oceniane po każdym wykonaniu pętli, `do-while` Pętla wykonuje jeden lub więcej razy. Różni się to od pętli [while](while.md) , która wykonuje zero lub więcej razy.

W dowolnym momencie w `do` bloku instrukcji można przerwać pętlę przy użyciu instrukcji [Break](break.md) .

Możesz przejść bezpośrednio do oceny `while` wyrażenia przy użyciu instrukcji [Continue](continue.md) . Jeśli wyrażenie zwróci wartość `true` , wykonywanie jest kontynuowane na pierwszej instrukcji w pętli. W przeciwnym razie wykonywanie jest kontynuowane po pierwszej instrukcji po pętli.

Możesz również wyjść z `do-while` pętli przez instrukcje [goto](goto.md), [Return](return.md)lub [throw](throw.md) .

## <a name="example"></a>Przykład

W poniższym przykładzie pokazano sposób użycia `do` instrukcji. Wybierz pozycję **Uruchom** , aby uruchomić przykładowy kod. Następnie można zmodyfikować kod i uruchomić go ponownie.

[!code-csharp-interactive[do loop example](snippets/IterationKeywordsExamples.cs#4)]

## <a name="c-language-specification"></a>specyfikacja języka C#

Aby uzyskać więcej informacji, zobacz sekcję do [instrukcji](~/_csharplang/spec/statements.md#the-do-statement) w [specyfikacji języka C#](/dotnet/csharp/language-reference/language-specification/introduction).

## <a name="see-also"></a>Zobacz też

- [Odwołanie w C#](../index.md)
- [Przewodnik programowania w języku C#](../../programming-guide/index.md)
- [Słowa kluczowe języka C#](index.md)
- [while, instrukcja](while.md)
