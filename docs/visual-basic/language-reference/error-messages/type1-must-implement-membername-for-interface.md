---
title: Element <type1>„<typename>” musi implementować element „<membername>” dla interfejsu „<interfacename>”
ms.date: 07/20/2015
f1_keywords:
- vbc30154
- bc30154
helpviewer_keywords:
- BC30154
ms.assetid: 259afdfa-3608-4760-adcb-88ec0da5020d
ms.openlocfilehash: a036097d778daae59ef3bbd74ab8507cd16e6e24
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2020
ms.locfileid: "92161858"
---
# <a name="bc30154-type1typename-must-implement-membername-for-interface-interfacename"></a>BC30154: \<type1> " \<typename> " musi implementować element " \<membername> " dla interfejsu " \<interfacename> "

element " \<typename> " musi implementować element " \<membername> " dla interfejsu " \<interfacename> ". Implementacja właściwości musi mieć pasujące specyfikatory "ReadOnly"/"WriteOnly".

 Klasa lub struktura oświadczenia do implementacji interfejsu, ale nie implementuje procedury, właściwości lub zdarzenia zdefiniowanego przez interfejs. Każdy element członkowski interfejsu musi być zaimplementowany.

 **Identyfikator błędu:** BC30154

## <a name="to-correct-this-error"></a>Aby poprawić ten błąd

1. Zadeklaruj element członkowski o takiej samej nazwie i podpisie, jak zdefiniowano w interfejsie. Pamiętaj o uwzględnieniu co najmniej `End Function` instrukcji, `End Sub` , lub `End Property` .

2. Dodaj `Implements` klauzulę na końcu `Function` `Sub` instrukcji,, `Property` lub `Event` . Na przykład:

    ```vb
    Public Event ItHappened() Implements IBaseInterface.ItHappened
    ```

3. Podczas implementowania właściwości upewnij się, że `ReadOnly` `WriteOnly` jest ona używana w taki sam sposób jak w definicji interfejsu.

4. Podczas implementowania właściwości, deklaracji `Get` i `Set` procedur, zgodnie z potrzebami.

## <a name="see-also"></a>Zobacz też

- [Implements — Instrukcja](../statements/implements-statement.md)
- [Interfejsy](../../programming-guide/language-features/interfaces/index.md)
