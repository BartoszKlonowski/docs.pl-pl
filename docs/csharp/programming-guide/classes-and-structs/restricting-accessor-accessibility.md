---
title: Ograniczanie dostępności metody dostępu — Przewodnik programowania w języku C#
description: Metody dostępu get i set właściwości w języku C# mają ten sam poziom widoczności lub dostępu domyślnie, jak właściwość, do której należą. Można ograniczyć dostęp.
ms.date: 07/20/2015
helpviewer_keywords:
- read-only properties [C#]
- read-only indexers [C#]
- accessors [C#]
- properties [C#], read-only
- asymmetric accessor accessibility [C#]
- indexers [C#], read-only
ms.assetid: 6e655798-e112-4301-a680-6310a6e012e1
ms.openlocfilehash: be7be4fc67a9a6f62a71f8473d6daa1fac49e842
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91199032"
---
# <a name="restricting-accessor-accessibility-c-programming-guide"></a>Ograniczanie dostępności metody dostępu (Przewodnik programowania w języku C#)

Fragmenty [Get](../../language-reference/keywords/get.md) i [Set](../../language-reference/keywords/set.md) właściwości lub indeksatora są nazywane metodyą *dostępu*. Domyślnie te metody dostępu mają ten sam poziom widoczności lub dostępu do właściwości lub indeksatora, do którego należą. Aby uzyskać więcej informacji, zobacz [poziomy ułatwień dostępu](../../language-reference/keywords/accessibility-levels.md). Jednak czasami warto ograniczyć dostęp do jednego z tych metod dostępu. Zazwyczaj obejmuje to ograniczenie dostępności `set` metody dostępu, zachowując `get` publicznie dostępną metodę dostępu. Na przykład:  
  
 [!code-csharp[csProgGuideIndexers#6](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideIndexers/CS/Indexers.cs#6)]  
  
 W tym przykładzie właściwość o nazwie `Name` definiuje `get` a i `set` akcesor. `get`Metoda dostępu odbiera poziom dostępności samej właściwości, `public` w tym przypadku, gdy `set` metoda dostępu jest jawnie ograniczona przez zastosowanie modyfikatora dostępu [chronionego](../../language-reference/keywords/protected.md) do samej metody dostępu.  
  
## <a name="restrictions-on-access-modifiers-on-accessors"></a>Ograniczenia dotyczące modyfikatorów dostępu w przypadku metod dostępu  

 Używanie modyfikatorów metody dostępu we właściwościach lub indeksatorach podlega następujących warunkom:  
  
- Nie można używać modyfikatorów metody dostępu dla interfejsu lub jawnej implementacji elementu członkowskiego [interfejsu](../../language-reference/keywords/interface.md) .  
  
- Modyfikatory metody dostępu można używać tylko wtedy, gdy właściwość lub indeksator ma zarówno metody `set` dostępu, jak i `get` . W takim przypadku modyfikator jest dozwolony tylko dla jednego z dwóch metod dostępu.  
  
- Jeśli właściwość lub indeksator ma modyfikator [przesłonięcia](../../language-reference/keywords/override.md) , modyfikator metody dostępu musi być zgodny z akcesorem przesłoniętej metody dostępu, jeśli istnieje.  
  
- Poziom dostępności na metodzie dostępu musi być bardziej restrykcyjny niż poziom dostępności właściwości lub indeksatora.  
  
## <a name="access-modifiers-on-overriding-accessors"></a>Modyfikatory dostępu podczas zastępowania metod dostępu  

 Podczas przesłonięcia właściwości lub indeksatora zastępowane metody dostępu muszą być dostępne dla zastępujący kod. Ponadto dostępność właściwości/indeksatora i jego metod dostępu musi być zgodna z odpowiadającą jej przesłoniętą właściwością/indeksatorem oraz jej metod dostępu. Na przykład:  
  
 [!code-csharp[csProgGuideIndexers#7](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideIndexers/CS/Indexers.cs#7)]  
  
## <a name="implementing-interfaces"></a>Implementowanie interfejsów  

 W przypadku użycia metody dostępu do zaimplementowania interfejsu metoda dostępu może nie mieć modyfikatora dostępu. Jednak w przypadku zaimplementowania interfejsu przy użyciu jednej metody dostępu, takiej jak `get` , inna metoda dostępu może mieć Modyfikator dostęp, jak w poniższym przykładzie:  
  
 [!code-csharp[csProgGuideIndexers#8](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideIndexers/CS/Indexers.cs#8)]  
  
## <a name="accessor-accessibility-domain"></a>Domena dostępności metody dostępu  

 Jeśli używasz modyfikatora dostępu do akcesora, [domena dostępności](../../language-reference/keywords/accessibility-domain.md) metody dostępu jest określana przez ten modyfikator.  
  
 Jeśli nie używasz modyfikatora dostępu do akcesora, domena dostępności metody dostępu jest określana na podstawie poziomu dostępności właściwości lub indeksatora.  
  
## <a name="example"></a>Przykład  

 Poniższy przykład zawiera trzy klasy, `BaseClass` , `DerivedClass` , i `MainClass` . Istnieją dwie właściwości w `BaseClass` `Name` i `Id` dla obu klas. W przykładzie pokazano, jak Właściwość `Id` włączona `DerivedClass` może być ukryta przez właściwość `Id` w `BaseClass` przypadku używania ograniczonego modyfikatora dostępu, takiego jak [Protected](../../language-reference/keywords/protected.md) lub [Private](../../language-reference/keywords/private.md). W związku z tym podczas przypisywania wartości do tej właściwości `BaseClass` zamiast niej wywoływana jest właściwość klasy. Zastąpienie modyfikatora dostępu [publicznego](../../language-reference/keywords/public.md) spowoduje udostępnienie właściwości.  
  
 W przykładzie pokazano również, że restrykcyjny modyfikator dostępu, taki jak `private` lub `protected` , w `set` metodzie dostępu `Name` właściwości w programie `DerivedClass` uniemożliwia dostęp do akcesora i generuje błąd podczas przypisywania do niego.  
  
 [!code-csharp[csProgGuideIndexers#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideIndexers/CS/Indexers.cs#5)]  
  
## <a name="comments"></a>Komentarze  

 Zwróć uwagę, że w przypadku zastąpienia deklaracji `new private string Id` przez, otrzymujesz `new public string Id` dane wyjściowe:  
  
 `Name and ID in the base class: Name-BaseClass, ID-BaseClass`  
  
 `Name and ID in the derived class: John, John123`  
  
## <a name="see-also"></a>Zobacz też

- [Przewodnik programowania w języku C#](../index.md)
- [Właściwości](./properties.md)
- [Indexers (Indeksatory)](../indexers/index.md)
- [Modyfikatory dostępu](./access-modifiers.md)
