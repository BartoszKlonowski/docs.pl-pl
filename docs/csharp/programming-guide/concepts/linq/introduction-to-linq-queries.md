---
title: Wprowadzenie do kwerend LINQ (C#)
description: LINQ oferuje spójny model dla zapytań dotyczących danych w różnych rodzajach źródeł danych i formatach. W zapytaniu LINQ zawsze pracujesz z obiektami.
ms.date: 07/20/2015
helpviewer_keywords:
- deferred execution [LINQ]
- LINQ, queries
- LINQ, deferred execution
- queries [LINQ], about LINQ queries
ms.assetid: 37895c02-268c-41d5-be39-f7d936fa88a8
ms.openlocfilehash: f81c3f4e355215f1a750a764c617ad47430adc31
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91170574"
---
# <a name="introduction-to-linq-queries-c"></a>Wprowadzenie do kwerend LINQ (C#)

*Zapytanie* jest wyrażeniem, które pobiera dane ze źródła danych. Zapytania są zwykle wyrażane w wyspecjalizowanym języku zapytań. Różne języki zostały opracowane z upływem czasu dla różnych typów źródeł danych, na przykład SQL dla relacyjnych baz danych i XQuery dla XML. W związku z tym deweloperzy musieli poznać nowy język zapytań dla każdego typu źródła danych lub formatu danych, które muszą być obsługiwane przez program. LINQ upraszcza tę sytuację, oferując spójny model do pracy z danymi w różnych rodzajach źródeł danych i formatach. W zapytaniu LINQ zawsze pracujesz z obiektami. Te same podstawowe wzorce kodowania służą do wykonywania zapytań i przekształcania danych w dokumentach XML, baz danych SQL, ADO.NET, kolekcjach platformy .NET i innych formatach, dla których jest dostępny dostawca LINQ.  
  
## <a name="three-parts-of-a-query-operation"></a>Trzy części operacji zapytania  

 Wszystkie operacje zapytań LINQ składają się z trzech odrębnych akcji:  
  
1. Uzyskanie źródła danych.  
  
2. Utwórz zapytanie.  
  
3. Wykonaj zapytanie.  
  
 Poniższy przykład pokazuje, jak trzy części operacji zapytania są wyrażone w kodzie źródłowym. W przykładzie jest wykorzystywana tablica liczb całkowitych jako źródło danych dla wygody; Jednak te same koncepcje odnoszą się również do innych źródeł danych. Ten przykład jest określany w pozostałej części tego tematu.  
  
 [!code-csharp[CsLINQGettingStarted#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#1)]  
  
 Na poniższej ilustracji przedstawiono wykonywanie operacji zapytania. W LINQ, wykonywanie zapytania jest różne od samego zapytania. Innymi słowy, nie pobrano żadnych danych tylko przez utworzenie zmiennej zapytania.  
  
 ![Diagram pełnej operacji zapytania LINQ.](./media/introduction-to-linq-queries/linq-query-complete-operation.png)  
  
## <a name="the-data-source"></a>Źródło danych  

 W poprzednim przykładzie, ponieważ źródło danych jest tablicą, niejawnie obsługuje <xref:System.Collections.Generic.IEnumerable%601> interfejs ogólny. Oznacza to, że można to zrobić za pomocą LINQ. Zapytanie jest wykonywane w `foreach` instrukcji i `foreach` wymaga <xref:System.Collections.IEnumerable> lub <xref:System.Collections.Generic.IEnumerable%601> . Typy obsługujące <xref:System.Collections.Generic.IEnumerable%601> lub interfejs pochodny, takie jak generyczne, <xref:System.Linq.IQueryable%601> są nazywane *typami Queryable*.  
  
 Typ Queryable nie wymaga modyfikacji ani specjalnego traktowania, które ma stanowić źródło danych LINQ. Jeśli dane źródłowe nie są jeszcze w pamięci jako typ queryable, dostawca LINQ musi je przedstawić jako taki. Na przykład [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] wczytuje dokument XML do <xref:System.Xml.Linq.XElement> typu queryable:  
  
 [!code-csharp[CsLINQGettingStarted#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#2)]  
  
 W programie należy [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] najpierw utworzyć mapowanie relacyjne obiektu w czasie projektowania ręcznie lub za pomocą [narzędzi LINQ to SQL w programie Visual Studio](/visualstudio/data-tools/linq-to-sql-tools-in-visual-studio2). Zapytania są zapisywane względem obiektów i w czasie wykonywania [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] obsługują komunikację z bazą danych. W poniższym przykładzie `Customers` reprezentuje określoną tabelę w bazie danych, a typ wyniku zapytania, <xref:System.Linq.IQueryable%601> , pochodzi od <xref:System.Collections.Generic.IEnumerable%601> .  
  
```csharp  
Northwnd db = new Northwnd(@"c:\northwnd.mdf");  
  
// Query for customers in London.  
IQueryable<Customer> custQuery =  
    from cust in db.Customers  
    where cust.City == "London"  
    select cust;  
```  
  
 Więcej informacji o sposobach tworzenia określonych typów źródeł danych znajduje się w dokumentacji dotyczącej różnych dostawców LINQ. Podstawowa reguła jest jednak bardzo prosta: źródłem danych LINQ jest każdy obiekt, który obsługuje <xref:System.Collections.Generic.IEnumerable%601> interfejs ogólny lub interfejs, który dziedziczy z niego.  
  
> [!NOTE]
> Typy takie jak <xref:System.Collections.ArrayList> obsługujące interfejs nieogólny <xref:System.Collections.IEnumerable> mogą również służyć jako źródło danych LINQ. Aby uzyskać więcej informacji, zobacz [How to Query The ArrayList with LINQ (C#)](./how-to-query-an-arraylist-with-linq.md).  
  
## <a name="the-query"></a><a name="query"></a> Zapytanie  

 Zapytanie określa, jakie informacje mają być pobierane ze źródła danych lub źródeł. Opcjonalnie zapytanie określa również, jak te informacje powinny być sortowane, grupowane i ukształtowane przed zwróceniem. Zapytanie jest przechowywane w zmiennej zapytania i inicjowane z wyrażeniem zapytania. Aby ułatwić Pisanie zapytań, język C# wprowadził nową składnię zapytania.  
  
 Zapytanie w poprzednim przykładzie zwraca wszystkie liczby parzyste z tablicy liczb całkowitych. Wyrażenie zapytania zawiera trzy klauzule: `from` , `where` i `select` . (Jeśli znasz program SQL, zobaczysz, że kolejność klauzul została odwrócona z kolejności w języku SQL). `from` Klauzula określa źródło danych, `where` klauzula stosuje filtr, a `select` klauzula określa typ zwracanych elementów. Te i inne klauzule zapytań są szczegółowo omówione w sekcji [Language Integrated Query (LINQ)](../../../linq/index.md) . Na razie istotnym punktem jest to, że w LINQ, zmienna zapytania nie przyjmuje żadnych akcji i nie zwraca żadnych danych. Po prostu przechowuje informacje, które są wymagane do wygenerowania wyników, gdy zapytanie jest wykonywane w późniejszym momencie. Aby uzyskać więcej informacji o tym, jak zapytania są konstruowane w tle, zobacz [standardowe operatory zapytań — Omówienie (C#)](./standard-query-operators-overview.md).  
  
> [!NOTE]
> Zapytania można również wyrazić przy użyciu składni metody. Aby uzyskać więcej informacji, zobacz [składnia zapytań i składnia metod w LINQ](./query-syntax-and-method-syntax-in-linq.md).  
  
## <a name="query-execution"></a>Wykonywanie zapytania  
  
### <a name="deferred-execution"></a>Wykonanie odroczone  

 Jak wspomniano wcześniej, zmienna zapytania zawiera tylko polecenia zapytania. Rzeczywiste wykonanie zapytania jest odroczone do czasu przetworzenia iteracji względem zmiennej zapytania w `foreach` instrukcji. Koncepcja ta jest nazywana *wykonywaniem odroczonym* i przedstawiono w poniższym przykładzie:  
  
 [!code-csharp[csLinqGettingStarted#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#4)]  
  
 `foreach`Instrukcja jest również miejscem, w którym są pobierane wyniki zapytania. Na przykład w poprzedniej kwerendzie Zmienna iteracji `num` przechowuje każdą wartość (pojedynczo) w zwracanej sekwencji.  
  
 Ponieważ sama zmienna zapytania nigdy nie przechowuje wyników zapytania, można wykonać ją tak często, jak chcesz. Na przykład może istnieć baza danych, która jest stale aktualizowana przez oddzielną aplikację. W aplikacji można utworzyć jedno zapytanie, które pobiera najnowsze dane, i można wykonać je wielokrotnie w pewnym interwale, aby pobierać różne wyniki za każdym razem.  
  
### <a name="forcing-immediate-execution"></a>Wymuszanie natychmiastowego wykonania  

 Zapytania, które wykonują funkcje agregacji dla zakresu elementów źródłowych, muszą najpierw wykonać iterację tych elementów. Przykładami takich zapytań są `Count` , `Max` , `Average` , i `First` . Te wykonywanie bez jawnej `foreach` instrukcji, ponieważ zapytanie musi być używane `foreach` w celu zwrócenia wyniku. Należy zauważyć, że te typy zapytań zwracają pojedynczą wartość, a nie `IEnumerable` kolekcję. Następujące zapytanie zwraca liczbę liczb parzystych w tablicy źródłowej:  
  
 [!code-csharp[csLinqGettingStarted#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#5)]  
  
 Aby wymusić natychmiastowe wykonywanie dowolnych zapytań i buforować wyniki, można <xref:System.Linq.Enumerable.ToList%2A> wywołać <xref:System.Linq.Enumerable.ToArray%2A> metody lub.  
  
 [!code-csharp[csLinqGettingStarted#6](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#6)]  
  
 Możesz również wymusić wykonywanie przez umieszczenie `foreach` pętli bezpośrednio po wyrażeniu zapytania. Jednak przez wywołanie `ToList` lub `ToArray` można również buforować wszystkie dane w jednym obiekcie kolekcji.  
  
## <a name="see-also"></a>Zobacz też

- [Wprowadzenie do korzystania z LINQ w C#](index.md)
- [Przewodnik: Pisanie zapytań w języku C #](./walkthrough-writing-queries-linq.md)
- [Language Integrated Query (LINQ)](../../../linq/index.md)
- [foreach, in](../../../language-reference/keywords/foreach-in.md)
- [Słowa kluczowe zapytania (LINQ)](../../../language-reference/keywords/query-keywords.md)
