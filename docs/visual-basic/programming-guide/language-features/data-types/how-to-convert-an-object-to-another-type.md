---
title: 'Instrukcje: Konwertowanie obiektu na inny typ'
ms.date: 07/20/2015
helpviewer_keywords:
- objects [Visual Basic], converting
ms.assetid: 60cb5fc7-7ba4-4ab5-9c24-480fa12ddcdc
ms.openlocfilehash: b89e996324d9ec22fc243b59502f3d36fefdee60
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/23/2020
ms.locfileid: "91090225"
---
# <a name="how-to-convert-an-object-to-another-type-in-visual-basic"></a>Porady: konwertowanie obiektu do innego typu w Visual Basic

Zmienną można przekonwertować `Object` na inny typ danych za pomocą słowa kluczowego konwersji, takiego jak [Funkcja CType](../../../language-reference/functions/ctype-function.md).  
  
## <a name="example"></a>Przykład  

 Poniższy przykład konwertuje `Object` zmienną na `Integer` i `String` .  
  
```vb  
Public Sub objectConversion(ByVal anObject As Object)  
    Dim anInteger As Integer  
    Dim aString As String  
    anInteger = CType(anObject, Integer)  
    aString = CType(anObject, String)  
End Sub  
```  
  
 Jeśli wiesz, że zawartość `Object` zmiennej jest określonego typu danych, lepiej jest skonwertować zmienną na ten typ danych. Jeśli nadal używasz `Object` zmiennej, naliczane są *opakowanie* i *rozpakowywanie* (dla typu wartości) lub *późne wiązanie* (dla typu odwołania). Wszystkie te operacje pobierają dodatkowy czas wykonywania i zwiększają wydajność.  
  
## <a name="compile-the-code"></a>Kompiluj kod  

 Ten przykład wymaga:  
  
- Odwołanie do <xref:System?displayProperty=nameWithType> przestrzeni nazw.  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Object>
- [Konwersje plików w Visual Basic](type-conversions.md)
- [Rozszerzanie i zwężanie konwersji](widening-and-narrowing-conversions.md)
- [Konwersje jawne i niejawne](implicit-and-explicit-conversions.md)
- [Konwertowanie między ciągami a innymi typami danych](conversions-between-strings-and-other-types.md)
- [Konwersje tablic](array-conversions.md)
- [Struktury](structures.md)
- [Typy danych](../../../language-reference/data-types/index.md)
- [Funkcje konwersji typu](../../../language-reference/functions/type-conversion-functions.md)
