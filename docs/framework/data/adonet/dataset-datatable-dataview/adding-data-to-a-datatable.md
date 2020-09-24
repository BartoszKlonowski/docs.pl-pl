---
title: Dodawanie danych do elementu DataTable
description: Zapoznaj się z tym przykładowym kodem, aby dodać nowe wiersze danych do tabeli w ADO.NET, po utworzeniu elementu DataTable i zdefiniowaniu jego struktury przy użyciu kolumn i ograniczeń.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d6aa8474-7bde-48f7-949d-20dc38a1625b
ms.openlocfilehash: aac2d90cc57a4af823c42f8c7eb2adcd43c63caf
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91164821"
---
# <a name="adding-data-to-a-datatable"></a>Dodawanie danych do elementu DataTable

Po utworzeniu <xref:System.Data.DataTable> i zdefiniowaniu struktury przy użyciu kolumn i ograniczeń można dodać do tabeli nowe wiersze danych. Aby dodać nowy wiersz, Zadeklaruj nową zmienną jako typ <xref:System.Data.DataRow> . Nowy obiekt **DataRow** jest zwracany po wywołaniu <xref:System.Data.DataTable.NewRow%2A> metody. Element **DataTable** następnie tworzy obiekt **DataRow** na podstawie struktury tabeli zdefiniowanej przez <xref:System.Data.DataColumnCollection> .  
  
 W poniższym przykładzie pokazano, jak utworzyć nowy wiersz przez wywołanie metody **NewRow** .  
  
```vb  
Dim workRow As DataRow = workTable.NewRow()  
```  
  
```csharp  
DataRow workRow = workTable.NewRow();  
```  
  
 Następnie można manipulować nowo dodanym wierszem przy użyciu indeksu lub nazwy kolumny, jak pokazano w poniższym przykładzie.  
  
```vb  
workRow("CustLName") = "Smith"  
workRow(1) = "Smith"  
```  
  
```csharp  
workRow["CustLName"] = "Smith";  
workRow[1] = "Smith";  
```  
  
 Po wstawieniu danych do nowego wiersza, Metoda **Dodaj** służy do dodawania wiersza do <xref:System.Data.DataRowCollection> , jak pokazano w poniższym kodzie.  
  
```vb  
workTable.Rows.Add(workRow)  
```  
  
```csharp  
workTable.Rows.Add(workRow);  
```  
  
 Możesz również wywołać metodę **Add** , aby dodać nowy wiersz przez przekazanie tablicy wartości, <xref:System.Object> tak jak pokazano w poniższym przykładzie.  
  
```vb  
workTable.Rows.Add(new Object() {1, "Smith"})  
```  
  
```csharp  
workTable.Rows.Add(new Object[] {1, "Smith"});  
```  
  
 Przekazanie tablicy wartości, wpisanej jako **obiekt**, do metody **Add** tworzy nowy wiersz wewnątrz tabeli i ustawia jego wartości kolumny na wartości w tablicy obiektów. Należy zauważyć, że wartości w tablicy są dopasowane sekwencyjnie do kolumn, na podstawie kolejności ich wyświetlania w tabeli.  
  
 Poniższy przykład dodaje 10 wierszy do nowo utworzonej tabeli **Customers** .  
  
```vb  
Dim workRow As DataRow  
Dim i As Integer  
  
For i = 0 To 9  
  workRow = workTable.NewRow()  
  workRow(0) = i  
  workRow(1) = "CustName" & I.ToString()  
  workTable.Rows.Add(workRow)  
Next  
```  
  
```csharp  
DataRow workRow;  
  
for (int i = 0; i <= 9; i++)
{  
  workRow = workTable.NewRow();  
  workRow[0] = i;  
  workRow[1] = "CustName" + i.ToString();  
  workTable.Rows.Add(workRow);  
}  
```  
  
## <a name="see-also"></a>Zobacz też

- <xref:System.Data.DataColumnCollection>
- <xref:System.Data.DataRow>
- <xref:System.Data.DataRowCollection>
- <xref:System.Data.DataTable>
- [Operowanie na danych w elemencie DataTable](manipulating-data-in-a-datatable.md)
- [Omówienie ADO.NET](../ado-net-overview.md)
