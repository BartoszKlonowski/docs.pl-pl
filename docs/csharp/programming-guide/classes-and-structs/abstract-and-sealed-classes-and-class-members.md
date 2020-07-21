---
title: Klasy abstrakcyjne i zapieczętowane oraz członkowie klas — Przewodnik programowania w języku C#
description: Abstrakcyjne słowo kluczowe w języku C# tworzy niekompletne klasy i składowe klas. Zapieczętowane słowo kluczowe uniemożliwia dziedziczenie wcześniej klas wirtualnych lub elementów członkowskich klas.
ms.date: 07/20/2015
helpviewer_keywords:
- abstract classes [C#]
- sealed classes [C#]
- C# language, abstract classes
- C# language, sealed
ms.assetid: 99aa52f7-b435-43f9-936e-2470af734c4e
ms.openlocfilehash: 391a8ccbb1fbe6626d1cd5a4b6fcfd9ace3506e6
ms.sourcegitcommit: cf5a800a33de64d0aad6d115ffcc935f32375164
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/20/2020
ms.locfileid: "86474491"
---
# <a name="abstract-and-sealed-classes-and-class-members-c-programming-guide"></a>Klasy abstrakcyjne i zapieczętowane oraz członkowie klas (Przewodnik programowania w języku C#)
[Abstrakcyjne](../../language-reference/keywords/abstract.md) słowo kluczowe umożliwia tworzenie klas i składowych [klas](../../language-reference/keywords/class.md) , które są niekompletne i muszą być zaimplementowane w klasie pochodnej.  
  
 [Zapieczętowane](../../language-reference/keywords/sealed.md) słowo kluczowe pozwala uniknąć dziedziczenia klasy lub niektórych elementów członkowskich klasy, które zostały wcześniej oznaczone jako [wirtualne](../../language-reference/keywords/virtual.md).  
  
## <a name="abstract-classes-and-class-members"></a>Klasy abstrakcyjne i składowe klas  
 Klasy mogą być deklarowane jako abstrakcyjne poprzez umieszczenie słowa kluczowego `abstract` przed definicją klasy. Na przykład:  
  
 [!code-csharp[csProgGuideInheritance#13](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#13)]  
  
 Nie można utworzyć wystąpienia klasy abstrakcyjnej. Celem klasy abstrakcyjnej jest zapewnienie wspólnej definicji klasy bazowej, która może być współużytkowana przez wiele klas pochodnych. Na przykład Biblioteka klas może definiować klasę abstrakcyjną, która jest używana jako parametr do wielu funkcji, i wymagać programiści używających tej biblioteki do zapewnienia własnej implementacji klasy przez utworzenie klasy pochodnej.  
  
 Klasy abstrakcyjne mogą również definiować metody abstrakcyjne. Jest to osiągane przez dodanie słowa kluczowego `abstract` przed typem zwracanym metody. Na przykład:  
  
 [!code-csharp[csProgGuideInheritance#14](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#14)]  
  
 Metody abstrakcyjne nie mają implementacji, dlatego w definicji metody następuje średnik zamiast zwykłego bloku metody. Klasy pochodne klasy abstrakcyjnej muszą implementować wszystkie metody abstrakcyjne. Gdy Klasa abstrakcyjna dziedziczy metodę wirtualną z klasy bazowej, Klasa abstrakcyjna może zastąpić metodę wirtualną metodą abstrakcyjną. Na przykład:  
  
 [!code-csharp[csProgGuideInheritance#15](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#15)]  
  
 Jeśli `virtual` Metoda jest zadeklarowana `abstract` , jest nadal wirtualna dla każdej klasy dziedziczące z klasy abstrakcyjnej. Klasa dziedziczące metodę abstrakcyjną nie może uzyskać dostępu do oryginalnej implementacji metody — w poprzednim przykładzie w `DoWork` klasie F nie można wywołać `DoWork` klasy D. W ten sposób Klasa abstrakcyjna może wymusić, aby klasy pochodne zapewniały nowe implementacje metod wirtualnych.  
  
## <a name="sealed-classes-and-class-members"></a>Klasy zapieczętowane i składowe klas  
 Klasy mogą być deklarowane jako [zapieczętowane](../../language-reference/keywords/sealed.md) poprzez umieszczenie słowa kluczowego `sealed` przed definicją klasy. Na przykład:  
  
 [!code-csharp[csProgGuideInheritance#16](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#16)]  
  
 Klasa zapieczętowana nie może być używana jako klasa bazowa. Z tego powodu nie może być również klasą abstrakcyjną. Zapieczętowane klasy uniemożliwiają wyprowadzanie. Ponieważ nigdy nie mogą być używane jako klasa bazowa, niektóre optymalizacje w czasie wykonywania mogą znacznie przyspieszyć wywoływanie zapieczętowanych elementów członkowskich klas.  
  
 Metoda, indeksator, właściwość lub zdarzenie w klasie pochodnej, która zastępuje wirtualną składową klasy bazowej, może zadeklarować ten element jako zapieczętowany. Spowoduje to negację wirtualnego aspektu elementu członkowskiego dla żadnej dalszej klasy pochodnej. Jest to realizowane przez umieszczenie `sealed` słowa kluczowego przed słowem kluczowym [override](../../language-reference/keywords/override.md) w deklaracji składowej klasy. Na przykład:  
  
 [!code-csharp[csProgGuideInheritance#17](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#17)]  
  
## <a name="see-also"></a>Zobacz także

- [Przewodnik programowania w języku C#](../index.md)
- [Klasy i struktury](./index.md)
- [Dziedziczenie](./inheritance.md)
- [Metody](./methods.md)
- [Pola](./fields.md)
- [Porada: definiowanie właściwości abstrakcyjnych](./how-to-define-abstract-properties.md)
