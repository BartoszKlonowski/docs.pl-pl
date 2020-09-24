---
title: Nawigowanie w elementach DataRelation
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: e5e673f4-9b44-45ae-aaea-c504d1cc5d3e
ms.openlocfilehash: 5eb2ee16712be5ccd5e9aa0af4dde22dcaaeea09
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91148389"
---
# <a name="navigating-datarelations"></a>Nawigowanie w elementach DataRelation

Jedną z podstawowych funkcji programu <xref:System.Data.DataRelation> jest umożliwienie nawigacji od jednego <xref:System.Data.DataTable> do drugiego w obrębie <xref:System.Data.DataSet> . Dzięki temu można pobrać wszystkie powiązane <xref:System.Data.DataRow> obiekty w jednej **DataTable** , gdy podaje jeden element **DataRow** z powiązanej **tabeli DataTable**. Na przykład po ustaleniu **relacji** między tabelą klientów a tabelą zamówień można pobrać wszystkie wiersze zamówienia dla danego wiersza klienta przy użyciu **GetChildRows**.  
  
 Poniższy przykład kodu tworzy **relację** między tabelą **Customers** i tabelą **Orders** **zestawu danych** i zwraca wszystkie zamówienia dla każdego klienta.  
  
 [!code-csharp[DataWorks Data.DataTableRelation#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks Data.DataTableRelation/CS/source.cs#1)]
 [!code-vb[DataWorks Data.DataTableRelation#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks Data.DataTableRelation/VB/source.vb#1)]  
  
 Następny przykład jest oparty na powyższym przykładzie, łącznie z czterema tabelami i nawigowaniem w tych relacjach. Tak jak w poprzednim przykładzie, **CustomerID** powiąże tabelę **Customers** z tabelą **Orders** . Dla każdego klienta w tabeli **Customers** są określane wszystkie wiersze podrzędne w tabeli **Orders** , aby można było zwrócić liczbę zamówień określonych przez określonego klienta i ich wartości **IDZamówienia** .  
  
 Rozwinięty przykład zwraca również wartości z tabel **OrderDetails** i **Products** . Tabela **Orders** jest powiązana z tabelą **OrderDetails** przy użyciu funkcji **IDZamówienia** , aby określić, jakie produkty i ilości zostały uporządkowane według kolejności. Ponieważ tabela **OrderDetails** zawiera tylko identyfikator **ProductID** uporządkowanego produktu, **OrderDetails** jest związana z **produktami** przy użyciu klasy **ProductID** w celu zwrócenia **ProductName**. W tej relacji tabela **Products** jest elementem nadrzędnym, a tabela **Order Details** jest elementem podrzędnym. W związku z tym podczas iterowania za pomocą tabeli **OrderDetails** zostaje wywołana funkcja **GetParentRow** w celu pobrania pokrewnej wartości **ProductName** .  
  
 Należy zauważyć, że po utworzeniu **relacji** dla tabel **Customers** i **Orders** nie określono żadnej wartości dla flagi **xmlconstraint** (wartość domyślna to **true**). Przyjęto założenie, że wszystkie wiersze w tabeli **Orders** mają wartość **CustomerID** , która istnieje w tabeli nadrzędnych **klientów** . Jeśli element **CustomerID** istnieje w tabeli **Orders** , która nie istnieje w tabeli **Customers** , powoduje to <xref:System.Data.ForeignKeyConstraint> wystąpienie wyjątku.  
  
 Gdy kolumna podrzędna może zawierać wartości, których kolumna nadrzędna nie zawiera, ustaw dla flagi " **isconstraint** **" wartość false** podczas dodawania **relacji**między elementami. W przykładzie flaga **"** **isconstraint** " ma wartość false dla **relacji** między tabelą **Orders** i tabelą **OrderDetails** . Dzięki temu aplikacja zwróci wszystkie rekordy z tabeli **OrderDetails** i tylko podzestaw rekordów z tabeli **Orders** bez generowania wyjątku w czasie wykonywania. Rozwinięty przykład generuje dane wyjściowe w następującym formacie.  
  
```output  
Customer ID: NORTS  
  Order ID: 10517  
        Order Date: 4/24/1997 12:00:00 AM  
           Product: Filo Mix  
          Quantity: 6  
           Product: Raclette Courdavault  
          Quantity: 4  
           Product: Outback Lager  
          Quantity: 6  
  Order ID: 11057  
        Order Date: 4/29/1998 12:00:00 AM  
           Product: Outback Lager  
          Quantity: 3  
```  
  
 Poniższy przykład kodu jest rozwiniętą próbką, gdy zwracane są wartości z tabeli **OrderDetails** i **Products** , z tylko podzbiorem rekordów w tabeli **Orders** .  
  
 [!code-csharp[DataWorks Data.DataTableNavigation#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks Data.DataTableNavigation/CS/source.cs#1)]
 [!code-vb[DataWorks Data.DataTableNavigation#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks Data.DataTableNavigation/VB/source.vb#1)]  
  
## <a name="see-also"></a>Zobacz też

- [Elementy DataSet, DataTable i DataView](index.md)
- [Omówienie ADO.NET](../ado-net-overview.md)
