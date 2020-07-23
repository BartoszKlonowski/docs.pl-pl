---
title: Polimorfizm — Przewodnik programowania w języku C#
description: Dowiedz się więcej na temat polimorfizmu, najważniejszych koncepcji opartych na obiektach programowania, takich jak C#, które opisuje relację między klasą bazową i pochodną.
ms.date: 02/08/2020
helpviewer_keywords:
- C# language, polymorphism
- polymorphism [C#]
ms.assetid: 086af969-29a5-4ce8-a993-0b7d53839dab
ms.openlocfilehash: 59b5f5d2d5a8f274845607aeca370c316670bd68
ms.sourcegitcommit: 40de8df14289e1e05b40d6e5c1daabd3c286d70c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/22/2020
ms.locfileid: "86925452"
---
# <a name="polymorphism-c-programming-guide"></a>Polimorfizm (Przewodnik programowania w języku C#)

Polimorfizm jest często określany jako trzeci filar programowania zorientowanego obiektowo po hermetyzacji i dziedziczeniu. Polimorfizm jest wyrazem greckim, który oznacza "wiele-kształt" i ma dwa odrębne aspekty:
  
- W czasie wykonywania obiekty klasy pochodnej mogą być traktowane jako obiekty klasy bazowej w miejscach takich jak parametry metody i kolekcje lub tablice. Gdy wystąpi ten polimorfizm, zadeklarowany typ obiektu nie jest już identyczny z jego typem w czasie wykonywania.
- Klasy bazowe mogą definiować i implementować *metody* [wirtualne](../../language-reference/keywords/virtual.md) , a klasy pochodne mogą je [przesłonić](../../language-reference/keywords/override.md) , co oznacza, że zapewniają własne definicje i implementacje. W czasie wykonywania, gdy kod klienta wywołuje metodę, środowisko CLR wyszukuje typ obiektu w czasie wykonywania i wywołuje przesłonięcie metody wirtualnej. W kodzie źródłowym można wywołać metodę w klasie bazowej i spowodować, że ma zostać wykonana wersja klasy pochodnej.

Metody wirtualne umożliwiają współpracę z grupami powiązanych obiektów w jednolity sposób. Załóżmy na przykład, że masz aplikację do rysowania, która umożliwia użytkownikowi tworzenie różnych rodzajów kształtów na powierzchni rysunku. W czasie kompilacji, które są tworzone dla poszczególnych typów kształtów, użytkownik nie wie. Jednak aplikacja musi śledzić wszystkie różne typy tworzonych kształtów i musi je zaktualizować w odpowiedzi na akcje myszy wykonywane przez użytkownika. Można użyć polimorfizmu, aby rozwiązać ten problem w dwóch podstawowych krokach:

1. Utwórz hierarchię klas, w której każda klasa określonego kształtu pochodzi ze wspólnej klasy bazowej.
1. Użyj metody wirtualnej do wywołania odpowiedniej metody dla dowolnej klasy pochodnej za pomocą pojedynczego wywołania metody klasy bazowej.

Najpierw Utwórz klasę bazową o nazwie `Shape` i klasy pochodne, takie jak `Rectangle` , `Circle` , i `Triangle` . Nadaj `Shape` klasie metodę wirtualną o nazwie `Draw` i Przesłoń ją w każdej klasie pochodnej, aby narysować określony kształt, który reprezentuje Klasa. Utwórz `List<Shape>` obiekt i Dodaj `Circle` `Triangle` do niego element,, i `Rectangle` .

[!code-csharp[Polymorphism overview](~/samples/snippets/csharp/objectoriented/Inheritance.cs#PolymorphismOverview)]

Aby zaktualizować powierzchnię rysowania, użyj pętli [foreach](../../language-reference/keywords/foreach-in.md) , aby wykonać iterację listy i wywołać `Draw` metodę dla każdego `Shape` obiektu na liście. Mimo że każdy obiekt na liście ma zadeklarowany typ `Shape` , jest typem czasu wykonywania (zastąpioną wersją metody w każdej klasie pochodnej), która zostanie wywołana.

[!code-csharp[Polymorphism overview](~/samples/snippets/csharp/objectoriented/Inheritance.cs#UsePolymorphism)]

W języku C# każdy typ jest polimorficzny, ponieważ wszystkie typy, włącznie z typami zdefiniowanymi przez użytkownika, dziedziczą z <xref:System.Object> .  

## <a name="polymorphism-overview"></a>Omówienie polimorfizmu

### <a name="virtual-members"></a>Wirtualne składowe

Gdy Klasa pochodna dziedziczy z klasy bazowej, uzyskuje wszystkie metody, pola, właściwości i zdarzenia klasy bazowej. Projektant klasy pochodnej ma różne opcje zachowania metod wirtualnych:

- Klasa pochodna może przesłonić wirtualne elementy członkowskie w klasie bazowej, definiując nowe zachowanie.
- Klasa pochodna dziedziczy najbliższą metodę klasy bazowej bez jej przesłaniania, zachowując istniejące zachowanie, ale umożliwiając dalsze klasy pochodne, aby przesłonić metodę.
- Klasa pochodna może definiować nową niewirtualną implementację tych elementów członkowskich, które ukrywają implementacje klas podstawowych.

Klasa pochodna może przesłonić składową klasy bazowej tylko wtedy, gdy element członkowski klasy bazowej jest zadeklarowany jako [wirtualny](../../language-reference/keywords/virtual.md) lub [abstrakcyjny](../../language-reference/keywords/abstract.md). Pochodny element członkowski musi użyć słowa kluczowego [override](../../language-reference/keywords/override.md) , aby jawnie wskazać, że metoda ma uczestniczyć w wywołaniu wirtualnym. Poniższy kod zawiera przykład:

[!code-csharp[Virtual overview](~/samples/snippets/csharp/objectoriented/Inheritance.cs#VirtualMethods)]

Pola nie mogą być wirtualne; tylko metody, właściwości, zdarzenia i indeksatory mogą być wirtualne. Gdy Klasa pochodna przesłania wirtualną składową, ten element członkowski jest wywoływany nawet wtedy, gdy do wystąpienia tej klasy jest uzyskiwany dostęp jako wystąpienie klasy bazowej. Poniższy kod zawiera przykład:

[!code-csharp[Virtual overview example](~/samples/snippets/csharp/objectoriented/Inheritance.cs#SnippetTestVirtualMethods)]

Metody wirtualne i właściwości umożliwiają klasom pochodnym poszerzanie klasy bazowej bez konieczności używania implementacji klasy bazowej metody. Aby uzyskać więcej informacji, zobacz [przechowywanie wersji ze słowami kluczowymi override i New](./versioning-with-the-override-and-new-keywords.md). Interfejs zapewnia inny sposób definiowania metody lub zestawu metod, których implementacja pozostała do klas pochodnych. Aby uzyskać więcej informacji, zobacz [interfejsy](../interfaces/index.md).

### <a name="hide-base-class-members-with-new-members"></a>Ukryj składowe klasy bazowej nowym członkom

Jeśli chcesz, aby Klasa pochodna miała element członkowski o takiej samej nazwie jak element członkowski w klasie bazowej, możesz użyć słowa kluczowego [New](../../language-reference/keywords/new-modifier.md) , aby ukryć element członkowski klasy bazowej. `new`Słowo kluczowe jest umieszczane przed typem zwracanym elementu członkowskiego klasy, który jest zastępowany. Poniższy kod zawiera przykład:

[!code-csharp[New method overview example](~/samples/snippets/csharp/objectoriented/Inheritance.cs#NewMethods)]

Do elementów członkowskich ukrytych klas podstawowych można uzyskać dostęp z kodu klienta, Rzutowanie wystąpienia klasy pochodnej na wystąpienie klasy bazowej. Na przykład:

[!code-csharp[New method overview usage](~/samples/snippets/csharp/objectoriented/Inheritance.cs#UseNewMethods)]

### <a name="prevent-derived-classes-from-overriding-virtual-members"></a>Zapobiegaj przesłanianiu wirtualnych elementów członkowskich klas pochodnych  

Wirtualne elementy członkowskie pozostają wirtualne, niezależnie od tego, ile klas zostało zadeklarowanych między wirtualnym elementem członkowskim a klasą, która pierwotnie została zadeklarowana. Jeśli Klasa `A` deklaruje wirtualną składową, a Klasa `B` pochodzi od `A` , i Klasa pochodzi od klasy, `C` `B` `C` dziedziczy wirtualną składową i może ją przesłonić, niezależnie od tego, czy Klasa `B` deklaruje przesłonięcie dla tego elementu członkowskiego. Poniższy kod zawiera przykład:

[!code-csharp[Basic hierarchy](~/samples/snippets/csharp/objectoriented/Hierarchy.cs#FirstHierarchy)]

Klasa pochodna może zatrzymać Dziedziczenie wirtualne, deklarując przesłonięcie jako [Sealed](../../language-reference/keywords/sealed.md). Zatrzymywanie dziedziczenia wymaga umieszczenia `sealed` słowa kluczowego przed `override` słowem kluczowym w deklaracji składowej klasy. Poniższy kod zawiera przykład:

[!code-csharp[A sealed overridden member](~/samples/snippets/csharp/objectoriented/Hierarchy.cs#SealedOverride)]

W poprzednim przykładzie metoda `DoWork` nie jest już wirtualna dla żadnej klasy pochodnej `C` . Nadal jest ona wirtualna dla wystąpień `C` , nawet jeśli są one rzutowane na typ `B` lub typ `A` . Zapieczętowane metody mogą zostać zastąpione przez klasy pochodne za pomocą `new` słowa kluczowego, jak pokazano w poniższym przykładzie:

[!code-csharp[New method declaration](~/samples/snippets/csharp/objectoriented/Hierarchy.cs#NewDeclaration)]

W tym przypadku, jeśli `DoWork` jest wywoływana `D` przy użyciu zmiennej typu `D` , Nowa `DoWork` jest wywoływana. Jeśli zmienna typu `C` , `B` , lub `A` jest używana w celu uzyskania dostępu do wystąpienia `D` , wywołanie `DoWork` zostanie zgodne z regułami dziedziczenia wirtualnego i routingu tych wywołań do implementacji `DoWork` klasy `C` .

### <a name="access-base-class-virtual-members-from-derived-classes"></a>Dostęp do wirtualnych elementów członkowskich klasy bazowej z klas pochodnych

Klasa pochodna, która zastąpiła lub przesłonięta metodę lub właściwość, może nadal uzyskiwać dostęp do metody lub właściwości w klasie podstawowej przy użyciu `base` słowa kluczowego. Poniższy kod zawiera przykład:

```csharp
public class Base
{
    public virtual void DoWork() {/*...*/ }
}
public class Derived : Base
{
    public override void DoWork()
    {
        //Perform Derived's work here
        //...
        // Call DoWork on base class
        base.DoWork();
    }
}
```

Aby uzyskać więcej informacji, zobacz temat [Base](../../language-reference/keywords/base.md).

> [!NOTE]
> Zaleca się, aby wirtualne składowe używały `base` do wywoływania implementacji klasy bazowej tego elementu członkowskiego we własnej implementacji. Zezwolenie na zachowanie klasy bazowej umożliwia skoncentrowanie się na implementowaniu przez klasę pochodną zachowania związanego z klasą pochodną. Jeśli implementacja klasy bazowej nie jest wywoływana, jest do klasy pochodnej, aby ich zachowanie było zgodne z zachowaniem klasy bazowej.

## <a name="in-this-section"></a>W tej sekcji

- [Przechowywanie wersji przesłonięć i nowych słów kluczowych](./versioning-with-the-override-and-new-keywords.md)
- [Użycie zastępowania i nowych słów kluczowych](./knowing-when-to-use-override-and-new-keywords.md)
- [Porada: zastępowanie metody ToString](./how-to-override-the-tostring-method.md)

## <a name="see-also"></a>Zobacz także

- [Przewodnik programowania w języku C#](../index.md)
- [Dziedziczenie](./inheritance.md)
- [Klasy abstrakcyjne i zapieczętowane oraz członkowie klas](./abstract-and-sealed-classes-and-class-members.md)
- [Metody](./methods.md)
- [Zdarzenia](../events/index.md)
- [Właściwości](./properties.md)
- [Indexers (Indeksatory)](../indexers/index.md)
- [Typy](../types/index.md)
