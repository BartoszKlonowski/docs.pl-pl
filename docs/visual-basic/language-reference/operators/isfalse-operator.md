---
title: IsFalse, operator
ms.date: 07/20/2015
f1_keywords:
- vb.isfalse
helpviewer_keywords:
- AndAlso operator [Visual Basic]
- IsFalse operator [Visual Basic]
ms.assetid: 37fc9dbf-e5cc-4570-b93f-7213447974df
ms.openlocfilehash: bbcdb9bcf645a4e9cb54c657ccd46e04437d207e
ms.sourcegitcommit: d2db216e46323f73b32ae312c9e4135258e5d68e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "90873375"
---
# <a name="isfalse-operator-visual-basic"></a>IsFalse — Operator (Visual Basic)

Określa, czy wyrażenie jest `False` .  
  
 Nie można `IsFalse` jawnie wywołać w kodzie, ale kompilator Visual Basic może użyć go do wygenerowania kodu z `AndAlso` klauzul. W przypadku zdefiniowania klasy lub struktury, a następnie użycia zmiennej tego typu w `AndAlso` klauzuli, należy zdefiniować `IsFalse` dla tej klasy lub struktury.  
  
 Kompilator traktuje `IsFalse` Operatory i `IsTrue` jako *pasującą parę*. Oznacza to, że w przypadku zdefiniowania jednego z nich należy również zdefiniować drugi.  
  
> [!NOTE]
> `IsFalse`Operator może być *przeciążony*, co oznacza, że Klasa lub struktura może zmienić jego zachowanie, gdy jego operand ma typ tej klasy lub struktury. Jeśli Twój kod używa tego operatora dla takiej klasy lub struktury, pamiętaj o tym, aby zrozumieć jego ponownie zdefiniowane zachowanie. Aby uzyskać więcej informacji, zobacz [procedury operatorów](../../programming-guide/language-features/procedures/operator-procedures.md).  
  
## <a name="example"></a>Przykład  

 Poniższy przykład kodu definiuje kontur struktury, która zawiera definicje `IsFalse` `IsTrue` operatorów i.  
  
 [!code-vb[VbVbalrOperators#28](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#28)]  
  
## <a name="see-also"></a>Zobacz też

- [IsTrue, operator](istrue-operator.md)
- [Instrukcje: definiowanie operatora](../../programming-guide/language-features/procedures/how-to-define-an-operator.md)
- [AndAlso, operator](andalso-operator.md)
