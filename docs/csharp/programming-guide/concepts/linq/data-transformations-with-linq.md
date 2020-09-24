---
title: Przekształcanie danych za pomocą LINQ (C#)
description: Dowiedz się, jak przetwarzać dane przy użyciu zapytań LINQ w języku C#. Sekwencję można modyfikować, sortując i grupując i tworząc nowe typy przy użyciu klauzuli select.
ms.date: 07/20/2015
helpviewer_keywords:
- LINQ [C#], data transformations
- source elements [LINQ in C#]
- joining multiple inputs [LINQ in C#]
- multiple outputs for one output sequence [LINQ in C#]
- subset of source elements [LINQ in C#]
- data sources [LINQ in C#], data transformations
- data transformations [LINQ in C#]
ms.assetid: 674eae9e-bc72-4a88-aed3-802b45b25811
ms.openlocfilehash: 2fb4166b9dbcecebf06b9dc3a780b02751dd4dc7
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91159153"
---
# <a name="data-transformations-with-linq-c"></a>Przekształcanie danych za pomocą LINQ (C#)

Zapytanie zintegrowane z językiem (LINQ) nie tylko pobiera dane. Jest to również zaawansowane narzędzie do przekształcania danych. Używając zapytania LINQ, można użyć sekwencji źródłowej jako danych wejściowych i zmodyfikować ją na wiele sposobów, aby utworzyć nową sekwencję wyjściową. Można zmodyfikować samą sekwencję bez modyfikowania samych elementów przez sortowanie i grupowanie. Jednak prawdopodobnie najbardziej wydajną funkcją zapytań LINQ jest możliwość tworzenia nowych typów. Jest to realizowane w klauzuli [SELECT](../../../language-reference/keywords/select-clause.md) . Na przykład można wykonać następujące zadania:  
  
- Scalanie wielu sekwencji wejściowych w jedną sekwencję wyjściową, która ma nowy typ.  
  
- Utwórz sekwencje danych wyjściowych, których elementy składają się tylko z jednej lub kilku właściwości każdego elementu w sekwencji źródłowej.  
  
- Utwórz sekwencje danych wyjściowych, których elementy składają się z wyników operacji wykonanych na danych źródłowych.  
  
- Utwórz sekwencje wyjściowe w innym formacie. Na przykład możesz przekształcić dane z wierszy SQL lub plików tekstowych do formatu XML.  
  
 Poniżej przedstawiono kilka przykładów. Oczywiście te przekształcenia można łączyć na różne sposoby w tym samym zapytaniu. Ponadto sekwencja wyjściowa jednego zapytania może służyć jako sekwencja wejściowa dla nowej kwerendy.  
  
## <a name="joining-multiple-inputs-into-one-output-sequence"></a>Łączenie wielu danych wejściowych w jedną sekwencję wyjściową  

 Za pomocą zapytania LINQ można utworzyć sekwencję wyjściową zawierającą elementy z więcej niż jednej sekwencji danych wejściowych. Poniższy przykład pokazuje, jak połączyć dwie struktury danych w pamięci, ale te same zasady można stosować do łączenia danych ze źródeł XML lub SQL lub zestawów danych. Założono następujące dwa typy klas:  
  
 [!code-csharp[CsLINQGettingStarted#7](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#7)]  
  
 W poniższym przykładzie pokazano zapytanie:  
  
 [!code-csharp[CSLinqGettingStarted#8](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#8)]  
  
 Aby uzyskać więcej informacji, zobacz [Klauzula join](../../../language-reference/keywords/join-clause.md) i [klauzula SELECT](../../../language-reference/keywords/select-clause.md).  
  
## <a name="selecting-a-subset-of-each-source-element"></a>Wybranie podzestawu każdego elementu źródłowego  

 Istnieją dwa podstawowe sposoby wybierania podzbioru każdego elementu w sekwencji źródłowej:  
  
1. Aby zaznaczyć tylko jeden element członkowski elementu źródłowego, użyj operacji z kropką. W poniższym przykładzie Załóżmy, że `Customer` obiekt zawiera kilka właściwości publicznych, w tym ciąg o nazwie `City` . Po wykonaniu to zapytanie będzie generować sekwencję wyjściową ciągów.  
  
    ```csharp
    var query = from cust in Customers  
                select cust.City;  
    ```  
  
2. Aby utworzyć elementy, które zawierają więcej niż jedną właściwość z elementu źródłowego, można użyć inicjatora obiektów z obiektem nazwanym lub typem anonimowym. W poniższym przykładzie pokazano użycie typu anonimowego do hermetyzacji dwóch właściwości z każdego `Customer` elementu:  
  
    ```csharp
    var query = from cust in Customer  
                select new {Name = cust.Name, City = cust.City};  
    ```  
  
 Aby uzyskać więcej informacji, zobacz [Inicjatory obiektów i kolekcji](../../classes-and-structs/object-and-collection-initializers.md) oraz [Typy anonimowe](../../classes-and-structs/anonymous-types.md).  
  
## <a name="transforming-in-memory-objects-into-xml"></a>Przekształcanie obiektów w pamięci do formatu XML  

 Zapytania LINQ ułatwiają Przekształcanie danych między strukturami danych w pamięci, bazami danych SQL, ADO.NETmi i strumieniami XML. Poniższy przykład przekształca obiekty w strukturze danych w pamięci na elementy XML.  
  
 [!code-csharp[CsLINQGettingStarted#9](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#9)]  
  
 Kod generuje następujące dane wyjściowe XML:  
  
```xml  
<Root>  
  <student>  
    <First>Svetlana</First>  
    <Last>Omelchenko</Last>  
    <Scores>97,92,81,60</Scores>  
  </student>  
  <student>  
    <First>Claire</First>  
    <Last>O'Donnell</Last>  
    <Scores>75,84,91,39</Scores>  
  </student>  
  <student>  
    <First>Sven</First>  
    <Last>Mortensen</Last>  
    <Scores>88,94,65,91</Scores>  
  </student>  
</Root>  
```  
  
 Aby uzyskać więcej informacji, zobacz [Tworzenie drzew XML w języku C# (LINQ to XML)](../../../../standard/linq/create-xml-trees.md).  
  
## <a name="performing-operations-on-source-elements"></a>Wykonywanie operacji na elementach źródłowych  

 Sekwencja wyjściowa może nie zawierać żadnych elementów ani właściwości elementów z sekwencji źródłowej. Wyjście może zamiast tego być sekwencją wartości, które są obliczane przy użyciu elementów źródłowych jako argumentów wejściowych.

 Następujące zapytanie zajmie sekwencję liczb reprezentujących promienie okręgów, oblicza obszar dla każdego promienia i zwraca sekwencję wyjściową zawierającą ciągi sformatowane w obszarze obliczeniowym.

 Każdy ciąg dla sekwencji wyjściowej zostanie sformatowany przy użyciu [interpolacji ciągów](../../../language-reference/tokens/interpolated.md). Ciąg interpolowany będzie miał `$` przed znakiem cudzysłowu otwierającego ciąg, a operacje mogą być wykonywane w nawiasach klamrowych umieszczonych wewnątrz ciągu interpolowanego. Po wykonaniu tych operacji wyniki zostaną połączone.
  
> [!NOTE]
> Metody wywołujące w wyrażeniach zapytań nie są obsługiwane, jeśli zapytanie zostanie przetłumaczone na inną domenę. Na przykład nie można wywołać zwykłej metody C# w [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] , ponieważ SQL Server nie ma kontekstu dla tego elementu. Można jednak mapować procedury składowane na metody i wywoływać je. Aby uzyskać więcej informacji, zobacz [procedury składowane](../../../../framework/data/adonet/sql/linq/stored-procedures.md).  
  
 [!code-csharp[CsLINQGettingStarted#10](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#10)]  
  
## <a name="see-also"></a>Zobacz też

- [Language-Integrated Query (LINQ) (C#)](./index.md)
- [LINQ to SQL](../../../../framework/data/adonet/sql/linq/index.md)
- [LINQ do DataSet](../../../../framework/data/adonet/linq-to-dataset.md)
- [LINQ to XML (C#)](../../../../standard/linq/linq-xml-overview.md)
- [Wyrażenia zapytania LINQ](../../../linq/index.md)
- [SELECT — klauzula](../../../language-reference/keywords/select-clause.md)
