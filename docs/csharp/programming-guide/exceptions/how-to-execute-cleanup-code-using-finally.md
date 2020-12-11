---
title: Jak wykonać kod czyszczący za pomocą przewodnika programowania finally w języku C#
description: Dowiedz się, jak wykonać oczyszczanie kodu przy użyciu instrukcji "finally". Instrukcje finally zapewniają, że wszelkie niezbędne czyszczenie obiektów następuje natychmiast.
ms.date: 12/09/2020
helpviewer_keywords:
- try/finally blocks [C#]
- exceptions [C#], try/finally block
- exception handling [C#], try/finally block
ms.assetid: 1b1e5aef-3f32-4a88-9d39-b5fffb33bdaf
ms.openlocfilehash: e9b5d3086488d3f7e3c0709317d6fafd15c439e8
ms.sourcegitcommit: 9b877e160c326577e8aa5ead22a937110d80fa44
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2020
ms.locfileid: "97110185"
---
# <a name="how-to-execute-cleanup-code-using-finally-c-programming-guide"></a>Jak wykonać oczyszczanie kodu za pomocą finally (Przewodnik programowania w języku C#)

Celem `finally` instrukcji jest upewnienie się, że konieczne jest oczyszczenie obiektów, zwykle obiektów, które są zasobami zewnętrznymi, występuje natychmiast, nawet jeśli zostanie zgłoszony wyjątek. Przykładem takiego oczyszczania jest wywoływanie <xref:System.IO.Stream.Close%2A> <xref:System.IO.FileStream> natychmiast po użyciu zamiast oczekiwania na odrzucanie obiektu przez środowisko uruchomieniowe języka wspólnego w następujący sposób:

:::code language="csharp" source="snippets/exceptions/Program.cs" ID="NoCleanup":::

## <a name="example"></a>Przykład

Aby przekształcić poprzedni kod do `try-catch-finally` instrukcji, kod czyszczący jest oddzielony od kodu roboczego w następujący sposób.

:::code language="csharp" source="snippets/exceptions/Program.cs" ID="WithCleanup":::

Ponieważ wyjątek może wystąpić w dowolnym momencie w `try` bloku przed `OpenWrite()` wywołaniem lub `OpenWrite()` samo wywołanie może się nie powieść, nie gwarantujemy, że plik jest otwarty, gdy spróbujemy go zamknąć. `finally`Blok dodaje zaznaczenie, aby upewnić się, że <xref:System.IO.FileStream> obiekt nie jest `null` przed wywołaniem <xref:System.IO.Stream.Close%2A> metody. Bez `null` sprawdzania, `finally` blok może zgłosić swój własny <xref:System.NullReferenceException> , ale w przypadku, gdy jest `finally` to możliwe, należy unikać zgłaszania wyjątków w blokach.

Połączenie z bazą danych jest kolejnym odpowiednim kandydatem do zamknięcia w `finally` bloku. Ponieważ liczba połączeń dozwolonych dla serwera bazy danych jest czasami ograniczona, należy zamknąć połączenia z bazą danych tak szybko, jak to możliwe. Jeśli wyjątek jest zgłaszany przed zamknięciem połączenia, użycie `finally` bloku jest lepsze niż oczekiwanie na wyrzucanie elementów bezużytecznych.

## <a name="see-also"></a>Zobacz też

- [using, instrukcja](../../language-reference/keywords/using-statement.md)
- [try-catch](../../language-reference/keywords/try-catch.md)
- [try-finally](../../language-reference/keywords/try-finally.md)
- [try-catch-finally](../../language-reference/keywords/try-catch-finally.md)
