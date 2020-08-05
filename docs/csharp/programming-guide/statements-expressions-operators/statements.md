---
title: Instrukcje — Przewodnik programowania w języku C#
description: Dowiedz się więcej na temat instrukcji w programowaniu w języku C#. Zobacz listę typów instrukcji i Wyświetl przykłady kodu i dodatkowe zasoby.
ms.date: 07/20/2015
helpviewer_keywords:
- statements [C#], about statements
- C# language, statements
ms.assetid: 901bcde7-87de-4e15-833c-f9cfd40c8ce3
ms.openlocfilehash: 3f8ac88525c44f9572f4f647145ad251537aba57
ms.sourcegitcommit: b7a8b09828bab4e90f66af8d495ecd7024c45042
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/04/2020
ms.locfileid: "87556751"
---
# <a name="statements-c-programming-guide"></a>Instrukcje (Przewodnik programowania w języku C#)

Akcje podejmowane przez program są wyrażone w instrukcjach. Typowe akcje obejmują deklarowanie zmiennych, przypisywanie wartości, wywoływanie metod, zapętlenie za pomocą kolekcji i rozgałęzianie do jednego lub innego bloku kodu, w zależności od danego warunku. Kolejność, w której instrukcje są wykonywane w programie, nazywa się przepływem sterowania lub przepływu wykonania. Przepływ sterowania może się różnić przy każdym uruchomieniu programu, w zależności od tego, jak program reaguje na dane wejściowe w czasie wykonywania.

Instrukcja może składać się z jednego wiersza kodu, który jest kończący się średnikiem lub serii instrukcji jednowierszowych w bloku. Blok instrukcji jest ujęty w {} nawiasy klamrowe i może zawierać zagnieżdżone bloki. Poniższy kod przedstawia dwa przykłady instrukcji jednowierszowych i blok instrukcji wielowierszowej:

[!code-csharp[csProgGuideStatements#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#1)]

## <a name="types-of-statements"></a>Typy instrukcji

W poniższej tabeli wymieniono różne typy instrukcji w języku C# i powiązane z nimi słowa kluczowe, z łączami do tematów zawierających więcej informacji:

|Kategoria|Słowa kluczowe języka C#/uwagi|
|--------------|---------------------------|
|[Deklaracje deklaracji](#declaration-statements)|Instrukcja deklaracji wprowadza nową zmienną lub stałą. Deklaracja zmiennej może opcjonalnie przypisać wartość do zmiennej. W deklaracji stałej jest wymagane przypisanie.|
|[Instrukcje wyrażeń](#expression-statements)|Instrukcje wyrażenia, które obliczają wartość, muszą przechowywać wartość w zmiennej.|
|Instrukcje wyboru|Instrukcje wyboru umożliwiają rozgałęzienie z różnymi sekcjami kodu, w zależności od jednego lub większej liczby określonych warunków. Aby uzyskać więcej informacji, zobacz następujące tematy: <ul><li>[if](../../language-reference/keywords/if-else.md)</li><li>[else](../../language-reference/keywords/if-else.md)</li><li>[przełącznika](../../language-reference/keywords/switch.md)</li><li>[spraw](../../language-reference/keywords/switch.md)</li></ul>|
|Instrukcje iteracji|Instrukcje iteracji umożliwiają pętlę za pomocą kolekcji, takich jak tablice, lub wielokrotne wykonywanie tego samego zestawu instrukcji do czasu spełnienia określonego warunku. Aby uzyskać więcej informacji, zobacz następujące tematy: <ul><li>[do](../../language-reference/keywords/do.md)</li><li>[dla](../../language-reference/keywords/for.md)</li><li>[foreach](../../language-reference/keywords/foreach-in.md)</li><li>[podczas](../../language-reference/keywords/foreach-in.md)</li><li>[while](../../language-reference/keywords/while.md)</li></ul>|
|Instrukcje skoku|Przeskocz kontrolę transferu do innej sekcji kodu. Aby uzyskać więcej informacji, zobacz następujące tematy: <ul><li>[break](../../language-reference/keywords/break.md)</li><li>[utrzymać](../../language-reference/keywords/continue.md)</li><li>[wartooć](../../language-reference/keywords/switch.md)</li><li>[goto](../../language-reference/keywords/goto.md)</li><li>[return](../../language-reference/keywords/return.md)</li><li>[yield](../../language-reference/keywords/yield.md)</li></ul>|
|Instrukcje obsługi wyjątków|Instrukcje obsługi wyjątków umożliwiają bezpieczne odzyskiwanie z wyjątkowych warunków występujących w czasie wykonywania. Aby uzyskać więcej informacji, zobacz następujące tematy: <ul><li>[throw](../../language-reference/keywords/throw.md)</li><li>[try-catch](../../language-reference/keywords/try-catch.md)</li><li>[try-finally](../../language-reference/keywords/try-finally.md)</li><li>[try-catch-finally](../../language-reference/keywords/try-catch-finally.md)</li></ul>|
|[Zaznaczone i niezaznaczone](../../language-reference/keywords/checked-and-unchecked.md)|Instrukcje sprawdzone i niesprawdzone umożliwiają określenie, czy operacje numeryczne mogą spowodować przepełnienie, gdy wynik jest przechowywany w zmiennej, która jest zbyt mała, aby pomieścić wynikową wartość. Aby uzyskać więcej informacji, zobacz [zaznaczone](../../language-reference/keywords/checked.md) i [niezaznaczone](../../language-reference/keywords/unchecked.md).|
|`await`Instrukcja|Jeśli oznaczesz metodę za pomocą modyfikatora [asynchronicznego](../../language-reference/keywords/async.md) , możesz użyć operatora [await](../../language-reference/operators/await.md) w metodzie. Gdy kontrolka osiągnie `await` wyrażenie w metodzie asynchronicznej, sterowanie powraca do obiektu wywołującego, a postęp w metodzie jest zawieszony do momentu zakończenia zadania oczekiwania. Po zakończeniu zadania wykonywanie może zostać wznowione w metodzie.<br /><br /> Aby zapoznać się z prostym przykładem, zobacz sekcję "metody asynchroniczne" w temacie [metody](../classes-and-structs/methods.md). Aby uzyskać więcej informacji, zobacz [programowanie asynchroniczne z Async i await](../concepts/async/index.md).|
|`yield return`Instrukcja|Iterator wykonuje niestandardową iterację w kolekcji, na przykład listę lub tablicę. Iterator używa instrukcji [yield return](../../language-reference/keywords/yield.md) , aby zwrócić każdy element po jednym naraz. Po `yield return` osiągnięciu instrukcji zostanie zapamiętana bieżąca lokalizacja w kodzie. Wykonanie jest uruchamiane ponownie z tej lokalizacji, kiedy iterator jest wywoływana następnym razem.<br /><br /> Aby uzyskać więcej informacji, zobacz [Iteratory](../concepts/iterators.md).|
|`fixed`Instrukcja|Stała instrukcja uniemożliwia ponowne lokalizowanie ruchomej zmiennej przez moduł wyrzucania elementów bezużytecznych. Aby uzyskać więcej informacji, zobacz [FIXED](../../language-reference/keywords/fixed-statement.md).|
|`lock`Instrukcja|Instrukcja lock umożliwia ograniczenie dostępu do bloków kodu tylko do jednego wątku naraz. Aby uzyskać więcej informacji, zobacz [Blokada](../../language-reference/keywords/lock-statement.md).|
|Instrukcje oznaczone|Możesz nadać instrukcji etykietę, a następnie użyć słowa kluczowego [goto](../../language-reference/keywords/goto.md) , aby przejść do instrukcji oznaczonej etykietą. (Zobacz przykład w następującym wierszu).|
|[Pusta instrukcja](#the-empty-statement)|Pusta instrukcja składa się z pojedynczego średnika. Nic nie robi i może być używane w miejscach, w których instrukcja jest wymagana, ale nie trzeba wykonywać żadnych czynności.|

## <a name="declaration-statements"></a>Deklaracje deklaracji

Poniższy kod przedstawia przykłady deklaracji zmiennych z przypisaniem wstępnym i bez niego oraz stałą deklarację z wymaganą inicjalizacją.

[!code-csharp[csProgGuideStatements#23](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#23)]

## <a name="expression-statements"></a>Instrukcje wyrażeń

Poniższy kod przedstawia przykłady instrukcji wyrażeń, w tym przypisanie, tworzenie obiektów z przypisaniem i wywoływanie metody.

[!code-csharp[csProgGuideStatements#24](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#24)]

## <a name="the-empty-statement"></a>Pusta instrukcja

W poniższych przykładach przedstawiono dwa zastosowania dla pustej instrukcji:

[!code-csharp[csProgGuideStatements#25](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#25)]

## <a name="embedded-statements"></a>Osadzone instrukcje

Niektóre instrukcje, w [tym do,](../../language-reference/keywords/do.md) [while](../../language-reference/keywords/while.md), [for](../../language-reference/keywords/for.md)i [foreach](../../language-reference/keywords/foreach-in.md), zawsze mają osadzoną instrukcję, która następuje po nich. Ta osadzona instrukcja może być pojedynczą instrukcją lub wieloma instrukcją ujętą {} w nawiasy kwadratowe bloku instrukcji. Nawet osadzone instrukcje jednowierszowe mogą być ujęte w {} nawiasy, jak pokazano w następującym przykładzie:

[!code-csharp[csProgGuideStatements#26](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#26)]

Osadzona instrukcja, która nie jest ujęta w {} nawiasy kwadratowe nie może być instrukcją deklaracji ani instrukcją etykiety. Pokazano to w następującym przykładzie:

[!code-csharp[csProgGuideStatements#27](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#27)]

Umieść osadzoną instrukcję w bloku, aby naprawić błąd:

[!code-csharp[csProgGuideStatements#28](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#28)]

## <a name="nested-statement-blocks"></a>Zagnieżdżone bloki instrukcji

Bloki instrukcji mogą być zagnieżdżane, jak pokazano w poniższym kodzie:

[!code-csharp[csProgGuideStatements#29](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#29)]

## <a name="unreachable-statements"></a>Nieosiągalne instrukcje

Jeśli kompilator określi, że przepływ sterowania nigdy nie dociera do konkretnej instrukcji w jakichkolwiek okolicznościach, spowoduje to wygenerowanie ostrzeżenia CS0162, jak pokazano w następującym przykładzie:

[!code-csharp[csProgGuideStatements#22](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#22)]

## <a name="c-language-specification"></a>specyfikacja języka C#

Aby uzyskać więcej informacji, zobacz sekcję [instrukcje](~/_csharplang/spec/statements.md) [specyfikacji języka C#](~/_csharplang/spec/introduction.md).

## <a name="see-also"></a>Zobacz też

- [Przewodnik programowania w języku C#](../index.md)
- [Słowa kluczowe instrukcji](../../language-reference/keywords/statement-keywords.md)
- [Operatory i wyrażenia języka C#](../../language-reference/operators/index.md)
