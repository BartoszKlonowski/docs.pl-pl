---
title: 'Porady: tworzenie procedury, która zwraca wartość'
ms.date: 07/20/2015
helpviewer_keywords:
- procedures [Visual Basic], defining
- Visual Basic code, procedures
- procedures [Visual Basic], returning a value
ms.assetid: 8ee19f95-a9ef-4033-963b-d224dca207c4
ms.openlocfilehash: 3d28162d2a2103477a20b08fc03c937de8b5a475
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/23/2020
ms.locfileid: "91071875"
---
# <a name="how-to-create-a-procedure-that-returns-a-value-visual-basic"></a>Porady: tworzenie procedury, która zwraca wartość (Visual Basic)

Używasz `Function` procedury do zwrócenia wartości do kodu wywołującego.  
  
### <a name="to-create-a-procedure-that-returns-a-value"></a>Aby utworzyć procedurę zwracającą wartość  
  
1. Poza inną procedurą Użyj `Function` instrukcji, a po niej `End Function` instrukcji.  
  
2. W `Function` instrukcji wykonaj `Function` słowo kluczowe z nazwą procedury, a następnie listę parametrów w nawiasach.  
  
3. Użyj nawiasów z `As` klauzulą, aby określić typ danych zwracanej wartości.  
  
4. Umieść instrukcje kodu procedury między `Function` `End Function` instrukcjami i.  
  
5. Użyj `Return` instrukcji, aby zwrócić wartość do kodu wywołującego.  
  
     Poniższa `Function` procedura oblicza najdłuższy Trójkąt lub przeciwprostokątnej, z prawej strony, z uwzględnieniem wartości pozostałych dwóch stron.  
  
     [!code-vb[VbVbcnProcedures#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#1)]  
  
     Poniższy przykład przedstawia typowe wywołanie `hypotenuse` .  
  
     [!code-vb[VbVbcnProcedures#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#6)]  
  
## <a name="see-also"></a>Zobacz także

- [Procedury](./index.md)
- [Sub, procedury](./sub-procedures.md)
- [Procedury własności](./property-procedures.md)
- [Procedury operatorów](./operator-procedures.md)
- [Parametry i argumenty procedur](./procedure-parameters-and-arguments.md)
- [Function, instrukcja](../../../language-reference/statements/function-statement.md)
- [Porady: zwracanie wartości z procedury](./how-to-return-a-value-from-a-procedure.md)
- [Instrukcje: wywoływanie procedury zwracającej wartość](./how-to-call-a-procedure-that-returns-a-value.md)
