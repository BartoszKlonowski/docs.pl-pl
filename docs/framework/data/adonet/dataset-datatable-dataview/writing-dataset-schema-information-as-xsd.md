---
title: Zapisywanie informacji o schemacie elementu DataSet jako pliku XSD
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 4e530831-695e-49ff-8f0b-e5b0c526b8eb
ms.openlocfilehash: 7634dfc8415b6f73fc60f2ebe59c92a0c31f83a2
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91173734"
---
# <a name="writing-dataset-schema-information-as-xsd"></a>Zapisywanie informacji o schemacie elementu DataSet jako pliku XSD

Można napisać schemat programu <xref:System.Data.DataSet> jako schemat języka definicji schematu XML (XSD), dzięki czemu można transportować go z lub bez powiązanych danych w dokumencie XML. Schemat XML można zapisać w pliku, strumieniu, a <xref:System.Xml.XmlWriter> lub ciągu; jest to przydatne w przypadku generowania **zestawu danych**o jednoznacznie określonym typie. Aby uzyskać więcej informacji na temat obiektów typu **zestaw danych** o jednoznacznie określonym typie, zobacz [zestawy danych z określonym typem](typed-datasets.md).  
  
 Można określić sposób, w jaki kolumna tabeli jest reprezentowana w schemacie XML przy użyciu właściwości **ColumnMapping** <xref:System.Data.DataColumn> obiektu. Aby uzyskać więcej informacji, zobacz "Mapowanie kolumn do elementów XML, atrybutów i tekstu" w [treści zestawu danych jako dane XML](writing-dataset-contents-as-xml-data.md).  
  
 Aby zapisać schemat **zestawu danych** jako schemat XML, do pliku, strumienia lub **XmlWriter**, użyj metody **WriteXmlSchema** **zestawu danych**. **WriteXmlSchema** przyjmuje jeden parametr, który określa miejsce docelowe uzyskanego schematu XML. Poniższy przykład kodu pokazuje, jak napisać schemat XML **zestawu danych** do pliku, przekazując ciąg zawierający nazwę pliku i <xref:System.IO.StreamWriter> obiekt.  
  
```vb  
dataSet.WriteXmlSchema("Customers.xsd")  
```  
  
```csharp  
dataSet.WriteXmlSchema("Customers.xsd");  
```  
  
```vb  
Dim writer As System.IO.StreamWriter = New System.IO.StreamWriter("Customers.xsd")  
dataSet.WriteXmlSchema(writer)  
writer.Close()  
```  
  
```csharp  
System.IO.StreamWriter writer = new System.IO.StreamWriter("Customers.xsd");  
dataSet.WriteXmlSchema(writer);  
writer.Close();  
```  
  
 Aby uzyskać schemat **zestawu danych** i zapisać go jako ciąg schematu XML, należy **użyć metody GetXml,** jak pokazano w poniższym przykładzie.  
  
```vb  
Dim schemaString As String = dataSet.GetXmlSchema()  
```  
  
```csharp  
string schemaString = dataSet.GetXmlSchema();  
```  
  
## <a name="see-also"></a>Zobacz też

- [Używanie języka XML w elemencie DataSet](using-xml-in-a-dataset.md)
- [Zapisywanie zawartości elementu DataSet jako danych XML](writing-dataset-contents-as-xml-data.md)
- [Typizowane elementy DataSet](typed-datasets.md)
- [Elementy DataSet, DataTable i DataView](index.md)
- [Omówienie ADO.NET](../ado-net-overview.md)
