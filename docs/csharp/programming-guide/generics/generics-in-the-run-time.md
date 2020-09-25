---
title: Typy ogólne w przewodniku programowania w języku C#
description: Dowiedz się więcej o typach ogólnych w czasie wykonywania. Zobacz przykłady kodu i Wyświetl dodatkowe dostępne zasoby.
ms.date: 07/20/2015
helpviewer_keywords:
- generics [C#], at run time
ms.assetid: 119df7e6-9ceb-49df-af36-24f8f8c0747f
ms.openlocfilehash: 1d2afd34d1a80841ba711897492cd4cd6412fa53
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91184121"
---
# <a name="generics-in-the-run-time-c-programming-guide"></a>Typy ogólne w czasie wykonywania (Przewodnik programowania w języku C#)

Gdy typ ogólny lub metoda jest kompilowany do języka pośredniego firmy Microsoft (MSIL), zawiera metadane, które identyfikują go jako parametry typu. Sposób użycia MSIL dla typu ogólnego różni się w zależności od tego, czy dostarczony parametr typu jest typem wartości czy typem referencyjnym.  
  
 Gdy typ ogólny jest najpierw konstruowany z typem wartości jako parametr, środowisko uruchomieniowe tworzy wyspecjalizowany typ ogólny z dostarczonym parametrem lub parametrami zastępowanymi w odpowiednich lokalizacjach w języku MSIL. Wyspecjalizowane typy ogólne są tworzone jednokrotnie dla każdego unikatowego typu wartości, który jest używany jako parametr.  
  
 Załóżmy na przykład, że kod programu deklaruje stos, który jest zbudowany z liczb całkowitych:  
  
 [!code-csharp[csProgGuideGenerics#42](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#42)]  
  
 W tym momencie środowisko uruchomieniowe generuje wyspecjalizowaną wersję <xref:System.Collections.Generic.Stack%601> klasy, która ma odpowiednią liczbę całkowitą podstawioną odpowiednio do parametru. Teraz za każdym razem, gdy kod programu używa stosu liczb całkowitych, środowisko uruchomieniowe ponownie używa wygenerowanej klasy wyspecjalizowanej <xref:System.Collections.Generic.Stack%601> . W poniższym przykładzie są tworzone dwa wystąpienia stosu liczb całkowitych i współużytkują pojedyncze wystąpienie `Stack<int>` kodu:  
  
 [!code-csharp[csProgGuideGenerics#43](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#43)]  
  
 Jednakże Załóżmy, że inna <xref:System.Collections.Generic.Stack%601> Klasa o innym typie wartości, taka jak `long` lub struktura zdefiniowana przez użytkownika, jest tworzona w innym punkcie w kodzie. W efekcie środowisko uruchomieniowe generuje inną wersję typu ogólnego i zastępuje je `long` w odpowiednich lokalizacjach w języku MSIL. Konwersje nie są już potrzebne, ponieważ każda wyspecjalizowana Klasa ogólna natywnie zawiera typ wartości.  
  
 Typy ogólne działają nieco inaczej w przypadku typów referencyjnych. Pierwszy raz, gdy typ ogólny jest konstruowany przy użyciu dowolnego typu referencyjnego, środowisko uruchomieniowe tworzy wyspecjalizowany typ ogólny z odwołaniami do obiektów, które zastępują parametry w MSIL. Następnie, za każdym razem, gdy tworzony jest typ wystąpienia typu referencyjnego jako jego parametr, niezależnie od tego, jakiego typu jest, środowisko uruchomieniowe ponownie używa wcześniej utworzonej wyspecjalizowanej wersji typu ogólnego. Jest to możliwe, ponieważ wszystkie odwołania mają ten sam rozmiar.  
  
 Załóżmy na przykład, że istniały dwa typy referencyjne, `Customer` Klasa i `Order` Klasa, a także Załóżmy, że utworzono stos `Customer` typów:  
  
 [!code-csharp[csProgGuideGenerics#47](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#47)]  
  
 [!code-csharp[csProgGuideGenerics#44](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#44)]  
  
 W tym momencie środowisko uruchomieniowe generuje wyspecjalizowaną wersję <xref:System.Collections.Generic.Stack%601> klasy, która przechowuje odwołania do obiektów, które zostaną uzupełnione później, zamiast przechowywać dane. Załóżmy, że następny wiersz kodu tworzy stos innego typu referencyjnego, który nosi nazwę `Order` :  
  
 [!code-csharp[csProgGuideGenerics#45](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#45)]  
  
 W przeciwieństwie do typów wartości, inna wyspecjalizowana wersja <xref:System.Collections.Generic.Stack%601> klasy nie jest tworzona dla tego `Order` typu. Zamiast tego tworzone jest wystąpienie wyspecjalizowanej wersji klasy, <xref:System.Collections.Generic.Stack%601> a `orders` zmienna jest ustawiana jako odwołująca się do niej. Załóżmy, że napotkasz wiersz kodu w celu utworzenia stosu `Customer` typu:  
  
 [!code-csharp[csProgGuideGenerics#46](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#46)]  
  
 Podobnie jak w przypadku poprzedniego użycia <xref:System.Collections.Generic.Stack%601> klasy utworzonej przy użyciu `Order` typu, tworzone jest inne wystąpienie klasy wyspecjalizowanej <xref:System.Collections.Generic.Stack%601> . Znajdujące się w nim wskaźniki są ustawiane jako odwołujące się do obszaru pamięci o rozmiarze `Customer` typu. Ze względu na to, że liczba typów referencyjnych może się różnić w zależności od programu do programu, implementacja języka C# generycznych znacznie zmniejsza ilość kodu przez zredukowanie do jednej z wielu wyspecjalizowanych klas utworzonych przez kompilator dla klas ogólnych typów referencyjnych.  
  
 Ponadto podczas tworzenia wystąpienia generycznej klasy C# przy użyciu typu wartości lub parametru typu odwołania odbicie może wysyłać zapytania do niego w czasie wykonywania i można ustalić zarówno jego rzeczywisty typ, jak i jego parametr typu.  
  
## <a name="see-also"></a>Zobacz też

- <xref:System.Collections.Generic>
- [Przewodnik programowania w języku C#](../index.md)
- [Wprowadzenie do typów ogólnych](./index.md)
- [Typy ogólne](../../../standard/generics/index.md)
