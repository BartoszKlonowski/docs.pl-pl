---
title: Wykonywanie zapytania XPath w elemencie DataSet
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 7e828566-fffe-4d38-abb2-4d68fd73f663
ms.openlocfilehash: d7897815874f2e9de2f4c24d3c141d464a296b31
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91201242"
---
# <a name="performing-an-xpath-query-on-a-dataset"></a>Wykonywanie zapytania XPath w elemencie DataSet

Relacja między zsynchronizowaną <xref:System.Data.DataSet> i <xref:System.Xml.XmlDataDocument> umożliwia korzystanie z usług XML, takich jak zapytanie XML Path Language (XPath), które uzyskuje dostęp do **XmlDataDocument** i może działać bardziej wygodnie niż bezpośredni dostęp do **zestawu danych** . Na przykład zamiast używać metody **SELECT** elementu <xref:System.Data.DataTable> do nawigacji relacji do innych tabel w **zestawie danych**, można wykonać zapytanie XPath na **XmlDataDocument** , który jest synchronizowany z **zestawem danych**, aby uzyskać listę elementów XML w postaci <xref:System.Xml.XmlNodeList> . Węzły w **XmlNodeList**, rzutowania jako <xref:System.Xml.XmlElement> węzły, mogą następnie zostać przesłane do metody **GetRowFromElement** **XmlDataDocument**, aby zwracały pasujące <xref:System.Data.DataRow> odwołania do wierszy tabeli w synchronizowanym **zestawie danych**.  
  
 Na przykład poniższy kod przykład wykonuje zapytanie XPath "grandchild". **Zestaw danych** jest wypełniony trzema tabelami **: Customers**, **Orders**i **OrderDetails**. W przykładzie relacja nadrzędny-podrzędny jest najpierw tworzona między tabelami **Customers** i **Orders** oraz między tabelami **Orders** i **OrderDetails** . Następnie zostanie wykonane zapytanie XPath w celu zwrócenia **XmlNodeList** węzłów **klientów** , gdzie węzeł grandchild **OrderDetails** ma węzeł **ProductID** o wartości 43. W zasadzie przykład używa zapytania XPath, aby określić, którzy klienci mają zamówiony produkt o identyfikatorze **ProductID** 43.  
  
```vb  
' Assumes that connection is a valid SqlConnection.  
connection.Open()  
Dim dataSet As DataSet = New DataSet("CustomerOrders")  
Dim customerAdapter As SqlDataAdapter = New SqlDataAdapter( _  
  "SELECT * FROM Customers", connection)  
customerAdapter.Fill(dataSet, "Customers")  
  
Dim orderAdapter As SqlDataAdapter = New SqlDataAdapter( _  
  "SELECT * FROM Orders", connection)  
orderAdapter.Fill(dataSet, "Orders")  
  
Dim detailAdapter As SqlDataAdapter = New SqlDataAdapter( _  
  "SELECT * FROM [Order Details]", connection)  
detailAdapter.Fill(dataSet, "OrderDetails")  
  
connection.Close()  
  
dataSet.Relations.Add("CustOrders", _  
dataSet.Tables("Customers").Columns("CustomerID"), _  
dataSet.Tables("Orders").Columns("CustomerID")).Nested = true  
  
dataSet.Relations.Add("OrderDetail", _  
  dataSet.Tables("Orders").Columns("OrderID"), _  
dataSet.Tables("OrderDetails").Columns("OrderID"), false).Nested = true  
  
Dim xmlDoc As XmlDataDocument = New XmlDataDocument(dataSet)
  
Dim nodeList As XmlNodeList = xmlDoc.DocumentElement.SelectNodes( _  
  "descendant::Customers[*/OrderDetails/ProductID=43]")  
  
Dim dataRow As DataRow  
Dim xmlNode As XmlNode  
  
For Each xmlNode In nodeList  
  dataRow = xmlDoc.GetRowFromElement(CType(xmlNode, XmlElement))  
  
  If Not dataRow Is Nothing then Console.WriteLine(xmlRow(0).ToString())  
Next  
```  
  
```csharp  
// Assumes that connection is a valid SqlConnection.  
connection.Open();  
  
DataSet dataSet = new DataSet("CustomerOrders");  
  
SqlDataAdapter customerAdapter = new SqlDataAdapter(  
  "SELECT * FROM Customers", connection);  
customerAdapter.Fill(dataSet, "Customers");  
  
SqlDataAdapter orderAdapter = new SqlDataAdapter(  
  "SELECT * FROM Orders", connection);  
orderAdapter.Fill(dataSet, "Orders");  
  
SqlDataAdapter detailAdapter = new SqlDataAdapter(  
  "SELECT * FROM [Order Details]", connection);  
detailAdapter.Fill(dataSet, "OrderDetails");  
  
connection.Close();  
  
dataSet.Relations.Add("CustOrders",  
  dataSet.Tables["Customers"].Columns["CustomerID"],  
 dataSet.Tables["Orders"].Columns["CustomerID"]).Nested = true;  
  
dataSet.Relations.Add("OrderDetail",  
  dataSet.Tables["Orders"].Columns["OrderID"],  
  dataSet.Tables["OrderDetails"].Columns["OrderID"],
  false).Nested = true;  
  
XmlDataDocument xmlDoc = new XmlDataDocument(dataSet);
  
XmlNodeList nodeList = xmlDoc.DocumentElement.SelectNodes(  
  "descendant::Customers[*/OrderDetails/ProductID=43]");  
  
DataRow dataRow;  
foreach (XmlNode xmlNode in nodeList)  
{  
  dataRow = xmlDoc.GetRowFromElement((XmlElement)xmlNode);  
  if (dataRow != null)  
    Console.WriteLine(dataRow[0]);  
}  
```  
  
## <a name="see-also"></a>Zobacz też

- [Synchronizacja elementów DataSet i XmlDataDocument](dataset-and-xmldatadocument-synchronization.md)
- [Omówienie ADO.NET](../ado-net-overview.md)
