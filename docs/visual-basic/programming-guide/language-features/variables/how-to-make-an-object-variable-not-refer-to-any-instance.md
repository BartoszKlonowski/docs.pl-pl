---
title: 'Porady: sprawianie, aby zmienna obiektu nie odwoływała się do żadnego wystąpienia'
ms.date: 07/20/2015
helpviewer_keywords:
- Nothing keyword [Visual Basic], variable assignment
- object variables [Visual Basic], null reference
ms.assetid: e6d30578-bdae-4142-a3ac-a10697bf696a
ms.openlocfilehash: 61bb06401ebd1e479c9256a80a12d87240831063
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/23/2020
ms.locfileid: "91080258"
---
# <a name="how-to-make-an-object-variable-not-refer-to-any-instance-visual-basic"></a>Porady: sprawianie, aby zmienna obiektu nie odwoływała się do żadnego wystąpienia (Visual Basic)

Można usunąć skojarzenie zmiennej obiektu z dowolnego wystąpienia obiektu, ustawiając dla niego wartość [Nothing](../../../language-reference/nothing.md).  
  
### <a name="to-disassociate-an-object-variable-from-any-object-instance"></a>Aby usunąć skojarzenie zmiennej obiektu z dowolnego wystąpienia obiektu  
  
- Ustaw zmienną na `Nothing` w instrukcji przypisania.  
  
    ```vb  
    ' Assume account is a defined class  
    Dim currentAccount As account  
    currentAccount = Nothing  
    ```  
  
## <a name="robust-programming"></a>Niezawodne programowanie  

 Jeśli kod próbuje uzyskać dostęp do elementu członkowskiego zmiennej obiektu, która została ustawiona na `Nothing` , <xref:System.NullReferenceException> występuje. Jeśli zmienna obiektu jest ustawiana na `Nothing` często lub jeśli jest możliwe, zmienna nie jest zainicjowana, dobrym pomysłem jest zawrzeć dostęp do składowych w `Try...Catch...Finally` bloku.  
  
## <a name="net-framework-security"></a>Zabezpieczenia.NET Framework  

 Jeśli używasz zmiennej obiektu dla obiektów, które zawierają dane poufne lub poufne, możesz ustawić zmienną na, `Nothing` gdy nie będziesz aktywnie korzystać z jednego z tych obiektów. Zmniejsza to prawdopodobieństwo złośliwego kodu, który uzyskuje dostęp do danych.  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.NullReferenceException>
- [Zmienne obiektów](object-variables.md)
- [Przypisanie zmiennej obiektu](object-variable-assignment.md)
- [Nothing](../../../language-reference/nothing.md)
- [Try...Catch...Finally, instrukcja](../../../language-reference/statements/try-catch-finally-statement.md)
