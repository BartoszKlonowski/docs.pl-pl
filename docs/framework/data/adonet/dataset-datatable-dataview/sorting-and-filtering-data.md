---
title: Sortowanie i filtrowanie danych
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: fdd9c753-39df-48cd-9822-2781afe76200
ms.openlocfilehash: 89e2fdf656fb06ee545ba936f033646ad86182d4
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91183380"
---
# <a name="sorting-and-filtering-data"></a>Sortowanie i filtrowanie danych

<xref:System.Data.DataView>Oferuje kilka sposobów sortowania i filtrowania danych w <xref:System.Data.DataTable> :  
  
- Możesz użyć właściwości, <xref:System.Data.DataView.Sort%2A> Aby określić pojedyncze lub wiele kolumn kolejności sortowania oraz uwzględnić parametry ASC (Ascending) i DESC (malejąco).  
  
- Możesz użyć <xref:System.Data.DataView.ApplyDefaultSort%2A> właściwości, aby automatycznie utworzyć porządek sortowania w kolejności rosnącej na podstawie kolumny klucza podstawowego lub kolumn tabeli. <xref:System.Data.DataView.ApplyDefaultSort%2A> stosuje się tylko wtedy, gdy właściwość **sort** jest odwołaniem null lub ciągiem pustym, a tabela ma zdefiniowany klucz podstawowy.  
  
- Możesz użyć właściwości, <xref:System.Data.DataView.RowFilter%2A> Aby określić podzestawy wierszy na podstawie ich wartości kolumn. Aby uzyskać szczegółowe informacje na temat prawidłowych wyrażeń dla właściwości **RowFilter** , zobacz informacje o odwołaniach dla <xref:System.Data.DataColumn.Expression%2A> właściwości <xref:System.Data.DataColumn> klasy.  
  
     Jeśli chcesz zwrócić wyniki konkretnego zapytania dotyczącego danych, w przeciwieństwie do udostępnienia dynamicznego widoku podzbioru danych, użyj <xref:System.Data.DataView.Find%2A> metody lub obiektu <xref:System.Data.DataView.FindRows%2A> **DataView** , aby osiągnąć najlepszą wydajność zamiast ustawić właściwość **RowFilter** . Ustawienie właściwości **RowFilter** powoduje odbudowanie indeksu dla danych, dodanie obciążenia do aplikacji i zmniejszenie wydajności. Właściwość **RowFilter** najlepiej używać w aplikacji powiązanej z danymi, gdzie kontrolka powiązania wyświetla filtrowane wyniki. Metody **Find** i **FindRows** wykorzystują bieżący indeks bez konieczności ponownego kompilowania indeksu. Aby uzyskać więcej informacji na temat metod **Find** i **FindRows** , zobacz [Znajdowanie wierszy](finding-rows.md).  
  
- Możesz użyć właściwości, <xref:System.Data.DataView.RowStateFilter%2A> Aby określić wersje wierszy do wyświetlenia. **Widok DataView** niejawnie określa wersję wiersza do udostępnienia w zależności od **RowState** podstawowego wiersza. Na przykład jeśli **RowStateFilter** jest ustawiony na **DataViewRowState. deleted**, **Widok DataView** ujawnia **pierwotną** wersję wiersza wszystkich **usuniętych** wierszy, ponieważ nie ma **bieżącej** wersji wiersza. Możesz określić, która wersja wiersza ma być ujawniana przy użyciu właściwości **rowversion** **DataRowView**.  
  
     W poniższej tabeli przedstawiono opcje **DataViewRowState**.  
  
    |Opcje DataViewRowState|Opis|  
    |------------------------------|-----------------|  
    |**CurrentRows**|Wersja **bieżącego** wiersza wszystkich **niezmienionych**, **dodanych**i **zmodyfikowanych** wierszy. Jest to opcja domyślna.|  
    |**Dodane**|Wersja **bieżącego** wiersza wszystkich **dodanych** wierszy.|  
    |**Usunięta**|**Oryginalna** wersja wiersza wszystkich **usuniętych** wierszy.|  
    |**ModifiedCurrent**|Wersja **bieżącego** wiersza wszystkich **zmodyfikowanych** wierszy.|  
    |**ModifiedOriginal**|**Oryginalna** wersja wiersza wszystkich **zmodyfikowanych** wierszy.|  
    |**Brak**|Brak wierszy.|  
    |**OriginalRows**|Wersja **oryginalnego** wiersza wszystkich **niezmienionych**, **zmodyfikowanych**i **usuniętych** wierszy.|  
    |**Bez zmian**|Wersja **bieżącego** wiersza wszystkich **niezmienionych** wierszy.|  
  
 Aby uzyskać więcej informacji o Stanach wierszy i wersjach wierszy, zobacz [Stany wiersza i wersje wierszy](row-states-and-row-versions.md).  
  
 Poniższy przykład kodu tworzy widok, który pokazuje wszystkie produkty, w których liczba jednostek w magazynie jest mniejsza lub równa poziomowi zmiany kolejności, posortowane najpierw według identyfikatora dostawcy, a następnie według nazwy produktu.  
  
```vb  
Dim prodView As DataView = New DataView(prodDS.Tables("Products"), _  
   "UnitsInStock <= ReorderLevel", _  
   "SupplierID, ProductName", _  
   DataViewRowState.CurrentRows)  
```  
  
```csharp  
DataView prodView = new DataView(prodDS.Tables["Products"],  
   "UnitsInStock <= ReorderLevel",  
   "SupplierID, ProductName",  
   DataViewRowState.CurrentRows);  
```  
  
## <a name="see-also"></a>Zobacz też

- <xref:System.Data.DataViewRowState>
- <xref:System.Data.DataColumn.Expression%2A?displayProperty=nameWithType>
- <xref:System.Data.DataTable>
- <xref:System.Data.DataView>
- [Elementy DataView](dataviews.md)
- [Omówienie ADO.NET](../ado-net-overview.md)
