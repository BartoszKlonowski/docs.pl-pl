---
title: Jak zastąpić metodę ToString — Przewodnik programowania w języku C#
description: Dowiedz się, jak zastąpić metodę ToString w języku C#. Każda klasa lub struktura dziedziczy obiekt i pobiera ToString, który zwraca ciąg reprezentujący ten obiekt.
ms.date: 07/20/2015
helpviewer_keywords:
- ToString method, overriding in C#
- inheritance [C#], overriding OnPaint and ToString
ms.topic: how-to
ms.custom: contperf-fy21q2
ms.assetid: 8016db69-1f19-420c-8e17-98e8bebb7749
ms.openlocfilehash: 9573e6b97383d6f422c6a2802040fb9d6db709dd
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2020
ms.locfileid: "97512746"
---
# <a name="how-to-override-the-tostring-method-c-programming-guide"></a>Jak zastąpić metodę ToString (Przewodnik programowania w języku C#)

Każda klasa lub struktura w języku C# niejawnie dziedziczy <xref:System.Object> klasę. W związku z tym każdy obiekt w C# pobiera <xref:System.Object.ToString%2A> metodę, która zwraca ciąg reprezentujący ten obiekt. Na przykład wszystkie zmienne typu `int` mają `ToString` metodę, która umożliwia im zwracanie ich zawartości jako ciągu:  
  
 [!code-csharp[csProgGuideInheritance#37](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#37)]  
  
 Podczas tworzenia niestandardowej klasy lub struktury należy zastąpić <xref:System.Object.ToString%2A> metodę, aby podać informacje o typie kodu klienta.  
  
 Aby uzyskać informacje o sposobach używania ciągów formatowania i innych typów formatowania niestandardowego z `ToString` metodą, zobacz [Typy formatowania](../../../standard/base-types/formatting-types.md).  
  
> [!IMPORTANT]
> W przypadku podjęcia decyzji o tym, jakie informacje mają być zawarte w tej metodzie, należy rozważyć, czy dana klasa lub struktura będzie kiedykolwiek używana przez kod niezaufany. Należy zachować ostrożność, aby upewnić się, że nie podano żadnych informacji, które mogą być wykorzystywane przez złośliwy kod.  
  
Aby zastąpić `ToString` metodę w klasie lub strukturze:
  
1. Zadeklaruj `ToString` metodę z następującymi modyfikatorami i zwracanym typem:  
  
    ```csharp  
    public override string ToString(){}  
    ```  
  
2. Zaimplementuj metodę, tak aby zwracała ciąg.  
  
     Poniższy przykład zwraca nazwę klasy oprócz danych specyficznych dla określonego wystąpienia klasy.  
  
     [!code-csharp[csProgGuideInheritance#36](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#36)]  
  
     Możesz przetestować `ToString` metodę, jak pokazano w poniższym przykładzie kodu:  
  
     [!code-csharp[csProgGuideInheritance#38](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#38)]  
  
## <a name="see-also"></a>Zobacz też

- <xref:System.IFormattable>
- [Przewodnik programowania w języku C#](../index.md)
- [Klasy i struktury](./index.md)
- [Ciągi](../strings/index.md)
- [parametry](../../language-reference/builtin-types/reference-types.md)
- [override](../../language-reference/keywords/override.md)
- [wirtualnej](../../language-reference/keywords/virtual.md)
- [Formatowanie typów](../../../standard/base-types/formatting-types.md)
