---
title: Klasyfikacja standardowych operatorów zapytań według sposobu wykonywania (C#)
description: 'Dowiedz się więcej o sposobie wykonywania standardowego operatora zapytań w języku C# dla LINQ to Objects: natychmiastowe, odroczone przesyłanie strumieniowe i odroczone przesyłanie strumieniowe.'
ms.date: 07/20/2015
ms.assetid: b9435ce5-a7cf-4182-9f01-f3468a5533dc
ms.openlocfilehash: dd496e232de2c7ed10a8aaa7cec84f8136495cce
ms.sourcegitcommit: 04022ca5d00b2074e1b1ffdbd76bec4950697c4c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/23/2020
ms.locfileid: "87105495"
---
# <a name="classification-of-standard-query-operators-by-manner-of-execution-c"></a>Klasyfikacja standardowych operatorów zapytań według sposobu wykonywania (C#)
Implementacje LINQ to Objects standardowych metod operatora zapytania są wykonywane na jednym z dwóch głównych sposobów: natychmiastowe lub odroczone. Operatory zapytań, które korzystają z odroczonego wykonania, można dodatkowo podzielić na dwie kategorie: streaming i bez przesyłania strumieniowego. Jeśli wiesz, jak są wykonywane różne operatory zapytań, może to pomóc w zrozumieniu wyników uzyskanych z danego zapytania. Jest to szczególnie prawdziwe w przypadku zmiany źródła danych lub tworzenia zapytania na podstawie innego zapytania. Ten temat klasyfikuje standardowe operatory zapytań zgodnie z ich sposobem wykonania.  
  
## <a name="manners-of-execution"></a>Sposób wykonywania  
  
### <a name="immediate"></a>Bezpośredniego  
 Natychmiastowe wykonanie oznacza, że źródło danych jest odczytywane i operacja jest wykonywana w punkcie w kodzie, w którym jest zadeklarowane zapytanie. Wszystkie standardowe operatory zapytań, które zwracają pojedynczy, nieprzeliczalny wynik wykonania.  
  
### <a name="deferred"></a>Odroczone  
 Wykonanie odroczone oznacza, że operacja nie jest wykonywana w punkcie w kodzie, w którym jest zadeklarowane zapytanie. Operacja jest wykonywana tylko wtedy, gdy zmienna zapytania jest wyliczana, na przykład za pomocą `foreach` instrukcji. Oznacza to, że wyniki wykonywania zapytania zależą od zawartości źródła danych, gdy zapytanie jest wykonywane, a nie po zdefiniowaniu zapytania. Jeśli zmienna zapytania jest wyliczana wiele razy, wyniki mogą się różnić za każdym razem. Prawie wszystkie standardowe operatory zapytań, których typ zwracany jest <xref:System.Collections.Generic.IEnumerable%601> lub <xref:System.Linq.IOrderedEnumerable%601> wykonywany w sposób odroczony.  
  
 Operatory zapytań, które korzystają z odroczonego wykonania, można dodatkowo klasyfikować jako strumieniowe lub niestrumieniowe.  
  
#### <a name="streaming"></a>Przesyłanie strumieniowe  
 Operatory przesyłania strumieniowego nie muszą odczytywać wszystkich danych źródłowych przed ich zwróceniem. Podczas wykonywania operator przesyłania strumieniowego wykonuje swoją operację na każdym elemencie źródłowym w miarę odczytu i dostarcza element, jeśli jest to konieczne. Operator przesyłania strumieniowego kontynuuje odczytywanie elementów źródłowych do momentu wygenerowania elementu wynik. Oznacza to, że więcej niż jeden element źródłowy może być odczytany w celu utworzenia jednego elementu wynik.  
  
#### <a name="non-streaming"></a>Bez przesyłania strumieniowego  
 Operatory niestrumieniowe muszą odczytywać wszystkie dane źródłowe, zanim będą mogły dać element wynik. Operacje, takie jak sortowanie lub grupowanie, znajdują się w tej kategorii. W czasie wykonywania operatory zapytań bez przesyłania strumieniowego odczytują wszystkie dane źródłowe, umieszczają je w strukturze danych, wykonują operację i dają elementy wyników.  
  
## <a name="classification-table"></a>Tabela klasyfikacji  
 Poniższa tabela klasyfikuje każdą standardową metodę operatora zapytań zgodnie z jej metodą wykonywania.  
  
> [!NOTE]
> Jeśli operator jest oznaczony w dwóch kolumnach, dwie sekwencje wejściowe są uwzględniane w operacji, a każda sekwencja jest szacowana inaczej. W takich przypadkach zawsze jest to pierwsza sekwencja na liście parametrów, która jest oceniana w sposób odroczony, przesyłany strumieniowo.  
  
|Standardowy operator zapytań|Typ zwracany|Natychmiastowe wykonanie|Wykonywanie odroczonego przesyłania strumieniowego|Odroczone wykonywanie bez przesyłania strumieniowego|  
|-----------------------------|-----------------|-------------------------|----------------------------------|---------------------------------------|  
|<xref:System.Linq.Enumerable.Aggregate%2A>|TSource|X|||  
|<xref:System.Linq.Enumerable.All%2A>|<xref:System.Boolean>|X|||  
|<xref:System.Linq.Enumerable.Any%2A>|<xref:System.Boolean>|X|||  
|<xref:System.Linq.Enumerable.AsEnumerable%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
|<xref:System.Linq.Enumerable.Average%2A>|Pojedyncza wartość liczbowa|X|||  
|<xref:System.Linq.Enumerable.Cast%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
|<xref:System.Linq.Enumerable.Concat%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
|<xref:System.Linq.Enumerable.Contains%2A>|<xref:System.Boolean>|X|||  
|<xref:System.Linq.Enumerable.Count%2A>|<xref:System.Int32>|X|||  
|<xref:System.Linq.Enumerable.DefaultIfEmpty%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
|<xref:System.Linq.Enumerable.Distinct%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
|<xref:System.Linq.Enumerable.ElementAt%2A>|TSource|X|||  
|<xref:System.Linq.Enumerable.ElementAtOrDefault%2A>|TSource|X|||  
|<xref:System.Linq.Enumerable.Empty%2A>|<xref:System.Collections.Generic.IEnumerable%601>|X|||  
|<xref:System.Linq.Enumerable.Except%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X|X|  
|<xref:System.Linq.Enumerable.First%2A>|TSource|X|||  
|<xref:System.Linq.Enumerable.FirstOrDefault%2A>|TSource|X|||  
|<xref:System.Linq.Enumerable.GroupBy%2A>|<xref:System.Collections.Generic.IEnumerable%601>|||X|  
|<xref:System.Linq.Enumerable.GroupJoin%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X|X|  
<xref:System.Linq.Enumerable.Intersect%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X|X|  
|<xref:System.Linq.Enumerable.Join%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X|X|  
|<xref:System.Linq.Enumerable.Last%2A>|TSource|X|||  
|<xref:System.Linq.Enumerable.LastOrDefault%2A>|TSource|X|||  
|<xref:System.Linq.Enumerable.LongCount%2A>|<xref:System.Int64>|X|||  
|<xref:System.Linq.Enumerable.Max%2A>|Pojedyncza wartość liczbowa, TSource lub TResult|X|||  
|<xref:System.Linq.Enumerable.Min%2A>|Pojedyncza wartość liczbowa, TSource lub TResult|X|||  
|<xref:System.Linq.Enumerable.OfType%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
|<xref:System.Linq.Enumerable.OrderBy%2A>|<xref:System.Linq.IOrderedEnumerable%601>|||X|  
|<xref:System.Linq.Enumerable.OrderByDescending%2A>|<xref:System.Linq.IOrderedEnumerable%601>|||X|  
|<xref:System.Linq.Enumerable.Range%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
|<xref:System.Linq.Enumerable.Repeat%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
|<xref:System.Linq.Enumerable.Reverse%2A>|<xref:System.Collections.Generic.IEnumerable%601>|||X|  
|<xref:System.Linq.Enumerable.Select%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
|<xref:System.Linq.Enumerable.SelectMany%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
|<xref:System.Linq.Enumerable.SequenceEqual%2A>|<xref:System.Boolean>|X|||  
|<xref:System.Linq.Enumerable.Single%2A>|TSource|X|||  
|<xref:System.Linq.Enumerable.SingleOrDefault%2A>|TSource|X|||  
|<xref:System.Linq.Enumerable.Skip%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
|<xref:System.Linq.Enumerable.SkipWhile%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
|<xref:System.Linq.Enumerable.Sum%2A>|Pojedyncza wartość liczbowa|X|||  
|<xref:System.Linq.Enumerable.Take%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
<xref:System.Linq.Enumerable.TakeWhile%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
|<xref:System.Linq.Enumerable.ThenBy%2A>|<xref:System.Linq.IOrderedEnumerable%601>|||X|  
|<xref:System.Linq.Enumerable.ThenByDescending%2A>|<xref:System.Linq.IOrderedEnumerable%601>|||X|  
|<xref:System.Linq.Enumerable.ToArray%2A>|TSource — tablica|X|||  
|<xref:System.Linq.Enumerable.ToDictionary%2A>|<xref:System.Collections.Generic.Dictionary%602>|X|||  
|<xref:System.Linq.Enumerable.ToList%2A>|<xref:System.Collections.Generic.IList%601>|X|||  
|<xref:System.Linq.Enumerable.ToLookup%2A>|<xref:System.Linq.ILookup%602>|X|||  
|<xref:System.Linq.Enumerable.Union%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
|<xref:System.Linq.Enumerable.Where%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
  
## <a name="see-also"></a>Zobacz też

- <xref:System.Linq.Enumerable>
- [Standardowe operatory zapytań — Omówienie (C#)](./standard-query-operators-overview.md)
- [Składnia wyrażenia zapytania dla standardowych operatorów zapytań (C#)](./query-expression-syntax-for-standard-query-operators.md)
- [LINQ to Objects (C#)](./linq-to-objects.md)
