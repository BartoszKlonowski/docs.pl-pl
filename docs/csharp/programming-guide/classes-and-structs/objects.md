---
title: Obiekty — Przewodnik programowania w języku C#
description: C# używa klasy lub definicji struktury do definiowania typów obiektów. W języku zorientowanym na obiektach, takim jak C#, program składa się z obiektów, które współpracują dynamicznie.
ms.date: 07/20/2015
helpviewer_keywords:
- objects [C#], about objects
- variables [C#]
ms.assetid: af4a5230-fbf3-4eea-95e1-8b883c2f845c
ms.openlocfilehash: 61d79f5647fa05edade9aef90653544b08c20c83
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91181833"
---
# <a name="objects-c-programming-guide"></a>Obiekty (Przewodnik programowania w języku C#)

Definicja klasy lub struktury jest taka sama jak w przypadku planu, który określa, jaki typ może być wykonywany. Obiekt jest w zasadzie blok pamięci, który został przydzielony i skonfigurowany zgodnie z planem. Program może utworzyć wiele obiektów tej samej klasy. Obiekty są również nazywane wystąpieniami i mogą być przechowywane w zmiennej nazwanej lub w tablicy lub kolekcji. Kod klienta to kod, który używa tych zmiennych do wywoływania metod i uzyskiwania dostępu do właściwości publicznych obiektu. W języku zorientowanym obiektowo, takim jak C#, typowy program składa się z wielu obiektów, które współpracują dynamicznie.  
  
> [!NOTE]
> Typy statyczne zachowują się inaczej niż opisane w tym miejscu. Aby uzyskać więcej informacji, zobacz [klasy statyczne i statyczne elementy członkowskie klas](./static-classes-and-static-class-members.md).
  
## <a name="struct-instances-vs-class-instances"></a>Wystąpienia struktury a wystąpienia klas  

 Ponieważ klasy są typami odwołań, zmienna obiektu klasy przechowuje odwołanie do adresu obiektu na zarządzanym stosie. Jeśli drugi obiekt tego samego typu jest przypisany do pierwszego obiektu, obie zmienne odwołują się do obiektu na tym adresie. Ten punkt jest omówiona bardziej szczegółowo w dalszej części tego tematu.  
  
 Wystąpienia klas są tworzone przy użyciu [operatora new](../../language-reference/operators/new-operator.md). W poniższym przykładzie `Person` jest typem i `person1` i `person 2` są wystąpieniami lub obiektami tego typu.  
  
 [!code-csharp[csProgGuideStatements#30](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#30)]  
  
 Ponieważ struktury są typami wartości, zmienna obiektu struktury przechowuje kopię całego obiektu. Wystąpienia struktur można także utworzyć przy użyciu `new` operatora, ale nie jest to wymagane, jak pokazano w następującym przykładzie:  
  
 [!code-csharp[csProgGuideStatements#31](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#31)]  
  
 Pamięć dla obu `p1` i `p2` jest przypisana na stosie wątków. Ta pamięć jest odzyskiwana wraz z typem lub metodą, w której jest zadeklarowana. Jest to jedną z przyczyn, dlaczego struktury są kopiowane podczas przypisywania. Z kolei, pamięć przydzieloną dla wystąpienia klasy jest automatycznie odzyskiwana (nieelementy bezużyteczne) przez środowisko uruchomieniowe języka wspólnego, gdy wszystkie odwołania do obiektu zostały utracone poza zakresem. Nie można deterministycznie zniszczyć obiektu klasy, takiego jak można w języku C++. Aby uzyskać więcej informacji dotyczących wyrzucania elementów bezużytecznych w programie .NET, zobacz [odzyskiwanie pamięci](../../../standard/garbage-collection/index.md).  
  
> [!NOTE]
> Alokacja i cofanie alokacji pamięci na stercie zarządzanej jest wysoce zoptymalizowana w środowisku uruchomieniowym języka wspólnego. W większości przypadków nie ma znaczącej różnicy kosztu wydajności alokacji wystąpienia klasy na stercie i przydzielania wystąpienia struktury na stosie.
  
## <a name="object-identity-vs-value-equality"></a>Tożsamość obiektu a równość wartości  

 Porównując dwa obiekty pod kątem równości, należy najpierw rozróżnić, czy chcesz wiedzieć, czy dwie zmienne reprezentują ten sam obiekt w pamięci, czy też wartości co najmniej jednego z tych pól są równoważne. Jeśli zamierzasz porównywać wartości, należy wziąć pod uwagę, czy obiekty są wystąpieniami typów wartości (struktur) czy typy odwołań (klasy, delegatów, tablice).  
  
- Aby określić, czy dwa wystąpienia klasy odwołują się do tej samej lokalizacji w pamięci (co oznacza, że mają tę samą *tożsamość*), użyj metody statycznej <xref:System.Object.Equals%2A> . ( <xref:System.Object?displayProperty=nameWithType> jest niejawną klasą bazową dla wszystkich typów wartości i typów referencyjnych, łącznie z strukturami i klasami zdefiniowanymi przez użytkownika).  
  
- Aby określić, czy pola wystąpienia w dwóch wystąpieniach struktury mają te same wartości, użyj <xref:System.ValueType.Equals%2A?displayProperty=nameWithType> metody. Ponieważ wszystkie struktury niejawnie dziedziczą z <xref:System.ValueType?displayProperty=nameWithType> , należy wywołać metodę bezpośrednio w obiekcie, jak pokazano w następującym przykładzie:  
  
 [!code-csharp[csProgGuideStatements#32](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#32)]  
  
 <xref:System.ValueType?displayProperty=nameWithType>Implementacja `Equals` używa odbicia, ponieważ musi być w stanie określić, jakie pola znajdują się w dowolnej strukturze. Podczas tworzenia własnych struktur Zastąp `Equals` metodę, aby zapewnić wydajny algorytm równości, który jest specyficzny dla danego typu.  
  
- Aby określić, czy wartości pól w dwóch wystąpieniach klasy są równe, może być możliwe użycie <xref:System.Object.Equals%2A> metody lub [operatora = =](../../language-reference/operators/equality-operators.md#equality-operator-). Jednak należy ich używać tylko wtedy, gdy klasa została zastąpiona lub przeciążona, aby zapewnić niestandardową definicję "Równość" dla obiektów tego typu. Klasa może również implementować <xref:System.IEquatable%601> interfejs lub <xref:System.Collections.Generic.IEqualityComparer%601> interfejs. Oba interfejsy zapewniają metody, których można użyć do testowania równości wartości. Podczas projektowania własnych klas, które zastępują `Equals` , należy postępować zgodnie ze wskazówkami podanymi w temacie [jak zdefiniować równość wartości dla typu](../statements-expressions-operators/how-to-define-value-equality-for-a-type.md) i <xref:System.Object.Equals%28System.Object%29?displayProperty=nameWithType> .
  
## <a name="related-sections"></a>Sekcje pokrewne  

 Więcej informacji:  
  
- [Klasy](./classes.md)  
  
- [Konstruktory](./constructors.md)  
  
- [Finalizatory](./destructors.md)  
  
- [Zdarzenia](../events/index.md)  
  
## <a name="see-also"></a>Zobacz też

- [Przewodnik programowania w języku C#](../index.md)
- [object](../../language-reference/builtin-types/reference-types.md)
- [Dziedziczenie](./inheritance.md)
- [określonej](../../language-reference/keywords/class.md)
- [Typy struktur](../../language-reference/builtin-types/struct.md)
- [Operator new](../../language-reference/operators/new-operator.md)
- [Wspólny system typów](../../../standard/base-types/common-type-system.md)
