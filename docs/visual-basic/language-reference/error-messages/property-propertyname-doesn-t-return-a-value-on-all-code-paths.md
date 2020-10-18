---
title: Właściwość „<propertyname>” nie zwraca wartości we wszystkich ścieżkach kodu
ms.date: 07/20/2015
f1_keywords:
- bc42107
- vbc42107
helpviewer_keywords:
- BC42107
ms.assetid: 06800966-9c3b-4844-9f13-83ac95607d32
ms.openlocfilehash: 0736e2cbcdea1422d40161c88f898d487f72e3bc
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2020
ms.locfileid: "92162391"
---
# <a name="bc42107-property-propertyname-doesnt-return-a-value-on-all-code-paths"></a>BC42107: Właściwość " \<propertyname> " nie zwraca wartości we wszystkich ścieżkach kodu

Właściwość " \<propertyname> " nie zwraca wartości we wszystkich ścieżkach kodu. W czasie wykonywania może wystąpić wyjątek odwołania o wartości null, gdy zostanie użyty wynik.

Procedura właściwości `Get` ma co najmniej jedną możliwą ścieżkę za pomocą kodu, który nie zwraca wartości.

 Można zwrócić wartość z `Get` procedury właściwości w dowolny z następujących sposobów:

- Przypisz wartość do nazwy właściwości, a następnie wykonaj `Exit Property` instrukcję.

- Przypisz wartość do nazwy właściwości, a następnie wykonaj `End Get` instrukcję.

- Dołącz wartość do [instrukcji return](../statements/return-statement.md).

Jeśli kontrola przechodzi do `Exit Property` lub `End Get` i nie przypisano żadnej wartości do nazwy właściwości, `Get` procedura zwraca wartość domyślną typu danych właściwości. Aby uzyskać więcej informacji, zobacz "zachowanie" w [instrukcji funkcji](../statements/function-statement.md).

Domyślnie ten komunikat jest ostrzeżeniem. Aby uzyskać więcej informacji na temat ukrywania ostrzeżeń lub leczenia ostrzeżeń jako błędów, zobacz [Konfigurowanie ostrzeżeń w Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic).

**Identyfikator błędu:** BC42107

## <a name="to-correct-this-error"></a>Aby poprawić ten błąd

- Sprawdź logikę przepływu sterowania i upewnij się, że przypiszesz wartość przed każdą instrukcją, która powoduje zwrócenie.

  Łatwiej jest zagwarantować, że każde zwrócenie z procedury zwraca wartość, jeśli zawsze używasz `Return` instrukcji. Jeśli to zrobisz, ostatnią instrukcją przed `End Get` powinien być `Return` instrukcja.

## <a name="see-also"></a>Zobacz też

- [Procedury własności](../../programming-guide/language-features/procedures/property-procedures.md)
- [Property — Instrukcja](../statements/property-statement.md)
- [Get — Instrukcja](../statements/get-statement.md)
