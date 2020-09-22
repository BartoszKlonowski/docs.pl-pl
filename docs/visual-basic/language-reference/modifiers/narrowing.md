---
title: Narrowing
ms.date: 07/20/2015
f1_keywords:
- vb.narrowing
helpviewer_keywords:
- conversions [Visual Basic], type
- type conversion [Visual Basic]
- conversions [Visual Basic], data type
- Narrowing keyword [Visual Basic]
- data type conversion [Visual Basic]
ms.assetid: a207ee91-aca4-4771-b4e2-713f029bf2bb
ms.openlocfilehash: 77515357ac9dc972992df09c471695aad13985c4
ms.sourcegitcommit: d2db216e46323f73b32ae312c9e4135258e5d68e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "90867927"
---
# <a name="narrowing-visual-basic"></a>Narrowing (Visual Basic)

Wskazuje, że Operator konwersji ( `CType` ) konwertuje klasę lub strukturę do typu, który może nie być w stanie przechowywać niektórych możliwych wartości oryginalnej klasy lub struktury.  
  
## <a name="converting-with-the-narrowing-keyword"></a>Konwertowanie za pomocą słowa kluczowego Narrowing  

 Procedura konwersji musi być określona `Public Shared` poza `Narrowing` .  
  
 Konwersje wąskie nie zawsze kończą się powodzeniem w czasie wykonywania i mogą kończyć się niepowodzeniem lub spowodować utratę danych. Przykłady to `Long` `Integer` , `String` do `Date` i typ podstawowy dla typu pochodnego. Ta ostatnia konwersja jest zawężana, ponieważ typ podstawowy może nie zawierać wszystkich elementów członkowskich typu pochodnego, w związku z czym nie jest wystąpieniem typu pochodnego.  
  
 Jeśli `Option Strict` jest `On` , kod zużywający musi używać `CType` dla wszystkich konwersji zawężających.  
  
 `Narrowing`Słowo kluczowe może być używane w tym kontekście:  
  
 [Operator — Instrukcja](../statements/operator-statement.md)  
  
## <a name="see-also"></a>Zobacz też

- [Operator — Instrukcja](../statements/operator-statement.md)
- [Widening](widening.md)
- [Rozszerzanie i zwężanie konwersji](../../programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)
- [Instrukcje: definiowanie operatora](../../programming-guide/language-features/procedures/how-to-define-an-operator.md)
- [CType — Funkcja](../functions/ctype-function.md)
- [Option Strict — Instrukcja](../statements/option-strict-statement.md)
