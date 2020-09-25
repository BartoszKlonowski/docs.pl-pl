---
title: 'Instrukcje: Bezpośrednie wykonywanie zapytań SQL'
description: Dowiedz się, w jaki sposób używać ExecuteQuery do uruchamiania zapytania, a następnie konwertować wyniki bezpośrednio do obiektów w przypadkach, gdy zapytanie LINQ to SQL jest niewystarczające.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: e491b9bf-741a-4296-9f51-76c25ddf6a82
ms.openlocfilehash: 7ebd02581d789266396b58296bbd6ad312dd468e
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91200579"
---
# <a name="how-to-directly-execute-sql-queries"></a>Instrukcje: Bezpośrednie wykonywanie zapytań SQL

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] tłumaczy zapytania zapisywane w sparametryzowanych zapytaniach SQL (w formie tekstowej) i wysyła je do programu SQL Server w celu przetworzenia.  
  
 W programie SQL Server nie można wykonywać różnych metod, które mogą być lokalnie dostępne dla aplikacji. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] próbuje przekonwertować te metody lokalne na równoważne operacje i funkcje, które są dostępne wewnątrz środowiska SQL. Większość metod i operatorów na .NET Framework typów wbudowanych ma bezpośrednie tłumaczenia na polecenia SQL. Niektóre z dostępnych funkcji można wytwarzać. Te, które nie mogą zostać wygenerowane, generują wyjątki w czasie wykonywania. Aby uzyskać więcej informacji, zobacz [Mapowanie typu SQL-CLR](sql-clr-type-mapping.md).  
  
 W przypadkach, gdy [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] zapytanie jest niewystarczające dla wyspecjalizowanego zadania, można użyć <xref:System.Data.Linq.DataContext.ExecuteQuery%2A> metody do wykonania zapytania SQL, a następnie przekonwertować wynik zapytania bezpośrednio do obiektów.  
  
## <a name="example"></a>Przykład  

 W poniższym przykładzie Załóżmy, że dane dla `Customer` klasy są rozłożone na dwie tabele (customer1 i Customer2). Zapytanie zwraca sekwencję `Customer` obiektów.  
  
 [!code-csharp[DLinqQuerying#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQuerying/cs/Program.cs#4)]
 [!code-vb[DLinqQuerying#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQuerying/vb/Module1.vb#4)]  
  
 Tak długo, jak nazwy kolumn w wynikach tabelarycznych są zgodne z właściwościami kolumny klasy Entity, program [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] tworzy obiekty z dowolnego zapytania SQL.  
  
## <a name="example"></a>Przykład  

 <xref:System.Data.Linq.DataContext.ExecuteQuery%2A>Metoda umożliwia również parametry. Użyj poniższego kodu, aby wykonać zapytanie parametryczne.  
  
 [!code-csharp[DLinqQuerying#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQuerying/cs/Program.cs#5)]
 [!code-vb[DLinqQuerying#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQuerying/vb/Module1.vb#5)]  
  
 Parametry są wyrażane w tekście zapytania przy użyciu tej samej notacji klamrowej używanej przez `Console.WriteLine()` i `String.Format()` . W rzeczywistości `String.Format()` jest faktycznie wywoływana w podanym ciągu zapytania, podstawiając parametry klamrowe z wygenerowanymi nazwami parametrów, takimi jak @p0 , @p1 ..., @p (n).  
  
## <a name="see-also"></a>Zobacz też

- [Informacje uzupełniające](background-information.md)
- [wykonywanie zapytania w bazie danych](querying-the-database.md)
