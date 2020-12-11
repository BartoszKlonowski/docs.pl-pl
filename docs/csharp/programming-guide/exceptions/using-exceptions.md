---
title: Korzystanie z wyjątków — Przewodnik programowania w języku C#
description: Dowiedz się, jak używać wyjątków. Wyjątki są zgłaszane przez kod, który napotka błąd i przechwycony przez kod, który koryguje błąd.
ms.date: 12/09/2020
helpviewer_keywords:
- exception handling [C#], about exception handling
- exceptions [C#], about exceptions
ms.assetid: 71472c62-320a-470a-97d2-67995180389d
ms.openlocfilehash: 30a7c3eecb599493dfa74d664c4899836c1b9276
ms.sourcegitcommit: 9b877e160c326577e8aa5ead22a937110d80fa44
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2020
ms.locfileid: "97110224"
---
# <a name="use-exceptions-c-programming-guide"></a>Używanie wyjątków (Przewodnik programowania w języku C#)

W języku C# błędy w programie w czasie wykonywania są propagowane za pośrednictwem programu przy użyciu mechanizmu nazywanego wyjątkami. Wyjątki są zgłaszane przez kod, który napotka błąd i przechwycony przez kod, który może poprawić błąd. Wyjątki mogą być zgłaszane przez środowisko uruchomieniowe .NET lub kod w programie. Gdy wyjątek jest zgłaszany, propaguje stos wywołań do momentu `catch` znalezienia instrukcji dla wyjątku. Nieprzechwycone wyjątki są obsługiwane przez ogólną procedurę obsługi wyjątków dostarczoną przez system, który wyświetla okno dialogowe.

Wyjątki są reprezentowane przez klasy pochodne od <xref:System.Exception> . Ta klasa identyfikuje typ wyjątku i zawiera właściwości, które zawierają szczegółowe informacje o wyjątku. Zgłaszanie wyjątku obejmuje utworzenie wystąpienia klasy pochodnej wyjątku, opcjonalnie skonfigurowanie właściwości wyjątku, a następnie wygenerowanie obiektu za pomocą `throw` słowa kluczowego. Na przykład:

:::code language="csharp" source="snippets/exceptions/Program.cs" id="ThrowException":::

Po zgłoszeniu wyjątku środowisko uruchomieniowe sprawdza bieżącą instrukcję, aby sprawdzić, czy znajduje się w `try` bloku. Jeśli tak jest, wszystkie `catch` bloki skojarzone z `try` blokiem są sprawdzane w celu sprawdzenia, czy mogą przechwytywać wyjątek. `Catch` bloki zwykle określają typy wyjątków; Jeśli typ `catch` bloku jest tego samego typu co wyjątek lub Klasa bazowa wyjątku, `catch` blok może obsłużyć metodę. Na przykład:

:::code language="csharp" source="snippets/exceptions/Program.cs" id="CatchException":::

Jeśli instrukcja zwracająca wyjątek nie znajduje się w `try` bloku lub jeśli `try` blok, który go zawiera, nie ma pasującego `catch` bloku, środowisko uruchomieniowe sprawdza metodę wywołującą dla `try` instrukcji i `catch` bloków. Środowisko uruchomieniowe kontynuuje wywoływanie stosu, wyszukując zgodny `catch` blok. Po `catch` znalezieniu i wykonaniu bloku, kontrola jest przenoszona do następnej instrukcji po tym `catch` bloku.

`try`Instrukcja może zawierać więcej niż jeden `catch` blok. Pierwsza `catch` instrukcja, która może obsłużyć wyjątek, jest wykonywana; wszelkie poniższe `catch` instrukcje, nawet jeśli są zgodne, są ignorowane. Bloki catch powinny zawsze być uporządkowane z najbardziej konkretnych (lub najbardziej pochodnych) do najmniej określonych. Na przykład:

:::code language="csharp" source="snippets/exceptions/CatchOrder.cs":::

Przed `catch` wykonaniem bloku program sprawdza bloki w czasie wykonywania `finally` . `Finally` bloki umożliwiają programistom czyszczenie dowolnego niejednoznacznego stanu, który może być pozostawiony przez przerwany `try` blok, lub do zwalniania zasobów zewnętrznych (takich jak uchwyty grafiki, połączenia z bazami danych lub strumienie plików) bez czekania na zakończenie działania modułu wyrzucania elementów bezużytecznych w środowisku uruchomieniowym. Na przykład:

:::code language="csharp" source="snippets/exceptions/Program.cs" id="TestFinally":::

Jeśli `WriteByte()` wywołał wyjątek, kod w drugim `try` bloku, który próbuje ponownie otworzyć plik, będzie kończyć się niepowodzeniem `file.Close()` , jeśli nie zostanie wywołany, a plik pozostanie zablokowany. Ponieważ `finally` bloki są wykonywane nawet w przypadku zgłoszenia wyjątku, `finally` blok w poprzednim przykładzie umożliwia poprawne zamknięcie pliku i pomaga uniknąć błędu.

Jeśli nie `catch` odnaleziono zgodnego bloku w stosie wywołań po zgłoszeniu wyjątku, wystąpi jedno z trzech rzeczy:

- Jeśli wyjątek znajduje się w obrębie finalizatora, finalizator zostanie przerwany i zostanie wywołany podstawowy finalizator, jeśli istnieje.
- Jeśli stos wywołań zawiera statyczny Konstruktor lub zostaje zgłoszony inicjator pola statycznego, <xref:System.TypeInitializationException> z pierwotnym wyjątkiem przypisanym do <xref:System.Exception.InnerException%2A> właściwości nowego wyjątku.
- Jeśli początek wątku zostanie osiągnięty, wątek zostanie zakończony.
