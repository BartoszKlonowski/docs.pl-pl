---
title: Obsługa wyjątków — Przewodnik programowania w języku C#
description: Dowiedz się więcej o obsłudze wyjątków. Zobacz przykłady instrukcji try-catch, try-finally i try-catch-finally.
ms.date: 12/09/2020
helpviewer_keywords:
- exception handling [C#], about exception handling
- exceptions [C#], handling
ms.assetid: b4e4ecf2-b907-4e58-891f-2563762258e9
ms.openlocfilehash: fabf1413ba498232e67f45460195fe96e25fab0a
ms.sourcegitcommit: 9b877e160c326577e8aa5ead22a937110d80fa44
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2020
ms.locfileid: "97110198"
---
# <a name="exception-handling-c-programming-guide"></a>Obsługa wyjątków (Przewodnik programowania w języku C#)

Programiści języka C# używają bloku [try](../../language-reference/keywords/try-catch.md) do partycjonowania kodu, który może mieć wpływ na wyjątek. Skojarzone bloki [catch](../../language-reference/keywords/try-catch.md) są używane do obsługi wszelkich wyjątków z wynikiem. Blok [finally](../../language-reference/keywords/try-finally.md) zawiera kod, który jest uruchamiany niezależnie od tego, czy wyjątek jest zgłaszany w `try` bloku, na przykład zwalniając zasoby, które są przydzieloną w `try` bloku. `try`Blok wymaga jednego lub większej liczby skojarzonych `catch` bloków albo bloku lub `finally` obu tych wartości.

W poniższych przykładach pokazano `try-catch` instrukcję, `try-finally` instrukcję i `try-catch-finally` instrukcję.

:::code language="csharp" source="snippets/exceptions/Program.cs" id="TryCatchStructure":::

:::code language="csharp" source="snippets/exceptions/Program.cs" id="TryFinallyStructure":::

:::code language="csharp" source="snippets/exceptions/Program.cs" id="TryCatchFinallyStructure":::

`try`Blok bez `catch` `finally` bloku lub powoduje błąd kompilatora.

## <a name="catch-blocks"></a>Bloki catch

`catch`Blok może określać typ wyjątku do przechwycenia. Specyfikacja typu jest nazywana *filtrem wyjątków*. Typ wyjątku powinien pochodzić od <xref:System.Exception> . Ogólnie rzecz biorąc nie określaj <xref:System.Exception> jako filtr wyjątku, chyba że wiesz, jak obsługiwać wszystkie wyjątki, które mogą być zgłaszane w `try` bloku, lub dodaliśmy instrukcję [throw](../../language-reference/keywords/throw.md) na końcu `catch` bloku.

Wiele `catch` bloków z różnymi klasami wyjątków może być łańcucha ze sobą. `catch`Bloki są oceniane z góry do dołu w kodzie, ale tylko jeden `catch` blok jest wykonywany dla każdego zgłoszonego wyjątku. `catch`Zostanie wykonany pierwszy blok, który określa typ dokładny lub Klasa bazowa zgłoszonego wyjątku. Jeśli żaden `catch` blok nie określa zgodnej klasy wyjątku, `catch` blok, który nie ma żadnego typu, nie jest zaznaczony, jeśli jeden jest obecny w instrukcji. Ważne jest, aby umieścić `catch` bloki z najbardziej szczegółowymi (najbardziej pochodnymi) klasami wyjątków.

Przechwyć wyjątki, gdy są spełnione następujące warunki:

- Warto zapoznać się z informacją o tym, dlaczego wyjątek może być zgłaszany, i można zaimplementować konkretne odzyskiwanie, na przykład monitowanie użytkownika o wprowadzenie nowej nazwy pliku podczas przechwytywania <xref:System.IO.FileNotFoundException> obiektu.
- Można utworzyć i zgłosić nowy, bardziej szczegółowy wyjątek.
  :::code language="csharp" source="snippets/exceptions/Program.cs" id="ThrowMoreSpecificException":::
- Chcesz częściowo obsłużyć wyjątek przed przekazaniem go do dodatkowej obsługi. W poniższym przykładzie `catch` blok jest używany do dodawania wpisu do dziennika błędów przed ponownym zgłoszeniem wyjątku.
  :::code language="csharp" source="snippets/exceptions/Program.cs" id="RethrowError":::

Można również określić *filtry wyjątków* , aby dodać wyrażenie logiczne do klauzuli catch. Wskazują one, że określona klauzula catch dopasowuje się tylko wtedy, gdy warunek ma wartość true. W poniższym przykładzie obie klauzule catch używają tej samej klasy wyjątku, ale jest sprawdzany dodatkowy warunek, aby utworzyć inny komunikat o błędzie:

:::code language="csharp" source="snippets/exceptions/ExceptionFilter.cs" ID="DemonstrateExceptionFilter":::

Filtr wyjątku, który zawsze zwraca wartość, `false` może być używany do badania wszystkich wyjątków, ale nie ich przetwarzania. Typowym zastosowaniem jest rejestrowanie wyjątków:

:::code language="csharp" source="snippets/exceptions/ExceptionFilter.cs" ID="ShowExceptionFilter":::

`LogException`Metoda zawsze zwraca `false` , żadna `catch` klauzula używająca tego filtru wyjątków nie jest zgodna. Klauzula catch może być ogólna, przy użyciu <xref:System.Exception?displayProperty=nameWithType> , a późniejsze klauzule mogą przetwarzać bardziej specyficzne klasy wyjątków.

## <a name="finally-blocks"></a>Bloki finally

`finally`Blok umożliwia czyszczenie akcji wykonywanych w `try` bloku. Jeśli jest obecny, `finally` blok jest wykonywany jako ostatni, po `try` bloku i dowolnym dopasowanym `catch` bloku. `finally`Blok jest zawsze uruchamiany, niezależnie od tego, czy występuje wyjątek, czy `catch` znaleziono blok pasujący do typu wyjątku.

`finally`Blok może służyć do zwolnienia zasobów, takich jak strumienie plików, połączenia z bazą danych i uchwyty grafiki, bez oczekiwania na zakończenie działania modułu zbierającego elementy bezużyteczne w środowisku uruchomieniowym. Aby uzyskać więcej informacji, zobacz [instrukcję using](../../language-reference/keywords/using-statement.md).

W poniższym przykładzie `finally` blok jest używany do zamykania pliku, który jest otwarty w `try` bloku. Przed zamknięciem pliku należy zauważyć, że jego stan jest sprawdzany. Jeśli `try` blok nie może otworzyć pliku, dojście do pliku nadal ma wartość, `null` a `finally` blok nie próbuje go zamknąć. Zamiast tego, jeśli plik zostanie pomyślnie otwarty w `try` bloku, `finally` blok zamknie otwarty plik.

:::code language="csharp" source="snippets/exceptions/Program.cs" id="CleanupIfNotNull":::

## <a name="c-language-specification"></a>Specyfikacja języka C#

Aby uzyskać więcej informacji, zobacz [wyjątki](~/_csharplang/spec/exceptions.md) i [Instrukcje try](~/_csharplang/spec/statements.md#the-try-statement) w [specyfikacji języka C#](/dotnet/csharp/language-reference/language-specification/introduction). Specyfikacja języka jest ostatecznym źródłem informacji o składni i użyciu języka C#.
  
## <a name="see-also"></a>Zobacz też

- [Odwołanie w C#](../../language-reference/index.md)
- [try-catch](../../language-reference/keywords/try-catch.md)
- [try-finally](../../language-reference/keywords/try-finally.md)
- [try-catch-finally](../../language-reference/keywords/try-catch-finally.md)
- [using, instrukcja](../../language-reference/keywords/using-statement.md)
