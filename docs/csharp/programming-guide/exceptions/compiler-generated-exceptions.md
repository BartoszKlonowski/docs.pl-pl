---
title: Wyjątki Compiler-Generated — Przewodnik programowania w języku C#
description: Informacje o wyjątkach wygenerowanych przez kompilator. Przejrzyj listę automatycznie zgłaszanych wyjątków i ich Stanów błędów.
ms.date: 12/09/2020
helpviewer_keywords:
- exceptions [C#], compiler-generated
ms.assetid: 53b52f97-b366-4ed7-b05b-9eb78096b7f9
ms.openlocfilehash: 43bacbb1025bc0af3a5f21979315b3d1b0d61066
ms.sourcegitcommit: 9b877e160c326577e8aa5ead22a937110d80fa44
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2020
ms.locfileid: "97110354"
---
# <a name="compiler-generated-exceptions-c-programming-guide"></a>Wyjątki generowane przez kompilator (Przewodnik programowania w języku C#)

Niektóre wyjątki są generowane automatycznie przez środowisko uruchomieniowe .NET, gdy podstawowe operacje zakończą się niepowodzeniem. Te wyjątki i ich warunki błędu są wymienione w poniższej tabeli.

|Wyjątek|Opis|
|---------------|-----------------|
|<xref:System.ArithmeticException>|Klasa bazowa dla wyjątków, które występują podczas operacji arytmetycznych, takich jak <xref:System.DivideByZeroException> i <xref:System.OverflowException> .|
|<xref:System.ArrayTypeMismatchException>|Zgłaszany, gdy tablica nie może przechowywać danego elementu, ponieważ rzeczywisty typ elementu jest niezgodny z rzeczywistym typem tablicy.|
|<xref:System.DivideByZeroException>|Zgłaszany, gdy podejmowana jest próba dzielenia wartości całkowitej przez zero.|
|<xref:System.IndexOutOfRangeException>|Zgłaszany, gdy podejmowana jest próba indeksowania tablicy, gdy indeks jest mniejszy od zera lub poza granicami tablicy.|
|<xref:System.InvalidCastException>|Zgłaszany, gdy jawna konwersja z typu podstawowego do interfejsu lub typu pochodnego kończy się niepowodzeniem w czasie wykonywania.|
|<xref:System.NullReferenceException>|Zgłaszany, gdy podejmowana jest próba odwołująca się do obiektu, którego wartość jest [równa null](../../language-reference/keywords/null.md).|
|<xref:System.OutOfMemoryException>|Zgłaszany, gdy próba przydzielenia pamięci przy użyciu operatora [New](../../language-reference/operators/new-operator.md) zakończy się niepowodzeniem. Ten wyjątek wskazuje na wyczerpanie pamięci dostępnej dla środowiska uruchomieniowego języka wspólnego.|
|<xref:System.OverflowException>|Zgłaszane w przypadku przepełnienia operacji arytmetycznej w `checked` kontekście.|
|<xref:System.StackOverflowException>|Zgłaszany, gdy stos wykonywania został wyczerpany przez zbyt wiele oczekujących wywołań metod; zwykle wskazuje bardzo głęboką lub nieskończoną rekursję.|
|<xref:System.TypeInitializationException>|Zgłaszany, gdy Konstruktor statyczny zgłasza wyjątek i nie `catch` istnieje zgodna klauzula, aby ją przechwycić.|

## <a name="see-also"></a>Zobacz też

- [try-catch](../../language-reference/keywords/try-catch.md)
- [try-finally](../../language-reference/keywords/try-finally.md)
- [try-catch-finally](../../language-reference/keywords/try-catch-finally.md)
