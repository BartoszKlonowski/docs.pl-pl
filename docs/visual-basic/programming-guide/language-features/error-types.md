---
title: Typy błędów
ms.date: 07/20/2015
helpviewer_keywords:
- exceptions, types
- errors [Visual Basic], types
- errors [Visual Basic], logic
- errors [Visual Basic], syntax
- logic errors [Visual Basic], Visual Basic
- run-time errors [Visual Basic], types of errors
- syntax errors [Visual Basic], Visual Basic
ms.assetid: 3048aabf-8c97-4e13-9150-853769cb5f6f
ms.openlocfilehash: caeaab9a358e3e3a995c1df7274d16daaff7a667
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/23/2020
ms.locfileid: "91083998"
---
# <a name="error-types-visual-basic"></a>Error — Typy (Visual Basic)

W Visual Basic błędy należą do jednej z trzech kategorii: Błędy składniowe, błędy czasu wykonywania i błędy logiki.

## <a name="syntax-errors"></a>Błędy składniowe

 *Błędy składni* są te, które pojawiają się podczas pisania kodu. Jeśli używasz programu Visual Studio, Visual Basic sprawdza kod w trakcie wpisywania go w oknie **edytora kodu** i ostrzega użytkownika w przypadku pomyłki, takich jak błąd pisowni wyrazu lub nieprawidłowe użycie elementu języka. W przypadku kompilowania z wiersza polecenia Visual Basic wyświetla błąd kompilatora z informacjami o błędzie składni. Błędy składni są najczęściej spotykanym typem błędów. Można je łatwo rozwiązać w środowisku kodowania, gdy tylko wystąpią.

> [!NOTE]
> `Option Explicit`Instrukcja to jeden z metod unikania błędów składniowych. Wymusza z wyprzedzeniem zadeklarować wszystkie zmienne, które mają być używane w aplikacji. W związku z tym, gdy te zmienne są używane w kodzie, wszelkie błędy typograficzne są przechwytywane natychmiast i można je naprawić.

## <a name="run-time-errors"></a>Błędy czasu wykonywania

 *Błędy czasu wykonywania* to te, które są wyświetlane dopiero po skompilowaniu i uruchomieniu kodu. Są to kod, który może wydawać się poprawny w tym, że nie ma błędów składniowych, ale nie zostanie wykonany. Na przykład można prawidłowo napisać wiersz kodu, aby otworzyć plik. Ale jeśli plik nie istnieje, aplikacja nie może otworzyć pliku i zgłasza wyjątek. Większość błędów czasu wykonywania można naprawić, przepisując błędny kod lub korzystając z [obsługi wyjątków](../../language-reference/statements/try-catch-finally-statement.md), a następnie ponownie kompilując i uruchamiając go.
  
## <a name="logic-errors"></a>Błędy logiki

 *Błędy logiczne* są te, które pojawiają się, gdy aplikacja jest używana. Najczęściej występują błędne założenia wykonywane przez dewelopera lub niechciane lub nieoczekiwane wyniki w reakcji na działania użytkownika. Na przykład błędnie wpisany klucz może dostarczyć błędne informacje do metody lub można założyć, że prawidłowa wartość jest zawsze przekazywana do metody, gdy nie jest to przypadek. Chociaż błędy logiczne mogą być obsługiwane przy użyciu [obsługi wyjątków](../../language-reference/statements/try-catch-finally-statement.md) (na przykład przez testowanie, czy argument jest `Nothing` i zgłaszany <xref:System.ArgumentNullException> ), najczęściej należy je rozwiązać przez skorygowanie błędu w logice i ponowne skompilowanie aplikacji.

## <a name="see-also"></a>Zobacz także

- [Try...Catch...Finally, instrukcja](../../language-reference/statements/try-catch-finally-statement.md)
- [Podstawowe informacje o debugerze](/visualstudio/debugger/debugger-feature-tour)
