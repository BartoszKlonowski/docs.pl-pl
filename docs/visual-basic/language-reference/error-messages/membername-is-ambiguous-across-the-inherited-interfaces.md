---
title: Element „<membername>” jest niejednoznaczny w dziedziczonych interfejsach „<interfacename1>” i „<interfacename2>”
ms.date: 07/20/2015
f1_keywords:
- vbc30685
- bc30685
helpviewer_keywords:
- BC30685
ms.assetid: 756add7a-23d5-4b4f-a48d-8297d6459c73
ms.openlocfilehash: 8fb8f84b07c488c817fd85fdd256d9aca7558a77
ms.sourcegitcommit: d2db216e46323f73b32ae312c9e4135258e5d68e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "90873796"
---
# <a name="membername-is-ambiguous-across-the-inherited-interfaces-interfacename1-and-interfacename2"></a>Element „\<membername>” jest niejednoznaczny w dziedziczonych interfejsach „\<interfacename1>” i „\<interfacename2>”

Interfejs dziedziczy co najmniej dwa elementy członkowskie o tej samej nazwie z wielu interfejsów.  
  
 **Identyfikator błędu:** BC30685  
  
## <a name="to-correct-this-error"></a>Aby poprawić ten błąd  
  
- Rzutowanie wartości na interfejs podstawowy, który ma być używany; na przykład:  
  
    ```vb  
    Interface Left  
        Sub MySub()  
    End Interface  
  
    Interface Right  
        Sub MySub()  
    End Interface  
  
    Interface LeftRight  
        Inherits Left, Right  
    End Interface  
  
    Module test  
        Sub Main()  
            Dim x As LeftRight  
            ' x.MySub()  'x is ambiguous.  
            CType(x, Left).MySub() ' Cast to base type.  
            CType(x, Right).MySub() ' Call the other base type.  
        End Sub  
    End Module  
    ```  
  
## <a name="see-also"></a>Zobacz też

- [Interfejsy](../../programming-guide/language-features/interfaces/index.md)
