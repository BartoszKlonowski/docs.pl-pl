---
title: Sprawdzanie poprawności przy użyciu XSD (LINQ to XML) (C#)
description: Dowiedz się, jak sprawdzać poprawność drzewa XML względem pliku języka definicji schematu XML (XSD). Zobacz przykłady kodu i wyświetlaj dodatkowe zasoby.
ms.date: 07/20/2015
ms.assetid: 6a7f83a9-2d74-4c2b-8417-0a8595879516
ms.openlocfilehash: 3b4d2137d511efbe20e4d31ad27e4975d5444ec9
ms.sourcegitcommit: 6f58a5f75ceeb936f8ee5b786e9adb81a9a3bee9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/28/2020
ms.locfileid: "87302636"
---
# <a name="how-to-validate-using-xsd-linq-to-xml-c"></a>Sprawdzanie poprawności przy użyciu XSD (LINQ to XML) (C#)
<xref:System.Xml.Schema>Przestrzeń nazw zawiera metody rozszerzające, które ułatwiają Weryfikowanie drzewa XML względem pliku języka definicji schematu XML (XSD). Aby uzyskać więcej informacji, zobacz <xref:System.Xml.Schema.Extensions.Validate%2A> dokumentację metody.  
  
## <a name="example"></a>Przykład  
 Poniższy przykład tworzy <xref:System.Xml.Schema.XmlSchemaSet> , a następnie weryfikuje dwa <xref:System.Xml.Linq.XDocument> obiekty względem zestawu schematów. Jeden z dokumentów jest prawidłowy, drugi nie jest.  
  
```csharp  
string xsdMarkup =  
    @"<xsd:schema xmlns:xsd='http://www.w3.org/2001/XMLSchema'>  
       <xsd:element name='Root'>  
        <xsd:complexType>  
         <xsd:sequence>  
          <xsd:element name='Child1' minOccurs='1' maxOccurs='1'/>  
          <xsd:element name='Child2' minOccurs='1' maxOccurs='1'/>  
         </xsd:sequence>  
        </xsd:complexType>  
       </xsd:element>  
      </xsd:schema>";  
XmlSchemaSet schemas = new XmlSchemaSet();  
schemas.Add("", XmlReader.Create(new StringReader(xsdMarkup)));  
  
XDocument doc1 = new XDocument(  
    new XElement("Root",  
        new XElement("Child1", "content1"),  
        new XElement("Child2", "content1")  
    )  
);  
  
XDocument doc2 = new XDocument(  
    new XElement("Root",  
        new XElement("Child1", "content1"),  
        new XElement("Child3", "content1")  
    )  
);  
  
Console.WriteLine("Validating doc1");  
bool errors = false;  
doc1.Validate(schemas, (o, e) =>  
                     {  
                         Console.WriteLine("{0}", e.Message);  
                         errors = true;  
                     });  
Console.WriteLine("doc1 {0}", errors ? "did not validate" : "validated");  
  
Console.WriteLine();  
Console.WriteLine("Validating doc2");  
errors = false;  
doc2.Validate(schemas, (o, e) =>  
                     {  
                         Console.WriteLine("{0}", e.Message);  
                         errors = true;  
                     });  
Console.WriteLine("doc2 {0}", errors ? "did not validate" : "validated");  
```  
  
 Ten przykład generuje następujące wyniki:  
  
```output  
Validating doc1  
doc1 validated  
  
Validating doc2  
The element 'Root' has invalid child element 'Child3'. List of possible elements expected: 'Child2'.  
doc2 did not validate  
```  
  
## <a name="example"></a>Przykład  
 Poniższy przykład sprawdza, czy dokument XML z [przykładowego pliku XML: klienci i zamówienia (LINQ to XML)](./sample-xml-file-customers-and-orders-linq-to-xml-2.md) są prawidłowe dla schematu z [przykładowego pliku XSD: klienci i zamówienia](./sample-xsd-file-customers-and-orders1.md). Następnie modyfikuje źródłowy dokument XML. Zmienia `CustomerID` atrybut pierwszego klienta. Po zmianie zamówienia odwołują się do klienta, który nie istnieje, więc dokument XML nie zostanie już zweryfikowany.  
  
 W tym przykładzie zastosowano następujący dokument XML: [przykładowy plik XML: Customers i Orders (LINQ to XML)](./sample-xml-file-customers-and-orders-linq-to-xml-2.md).  
  
 W tym przykładzie zastosowano następujący schemat XSD: [przykładowy plik XSD: klienci i zamówienia](./sample-xsd-file-customers-and-orders1.md).  
  
```csharp  
XmlSchemaSet schemas = new XmlSchemaSet();  
schemas.Add("", "CustomersOrders.xsd");  
  
Console.WriteLine("Attempting to validate");  
XDocument custOrdDoc = XDocument.Load("CustomersOrders.xml");  
bool errors = false;  
custOrdDoc.Validate(schemas, (o, e) =>  
                     {  
                         Console.WriteLine("{0}", e.Message);  
                         errors = true;  
                     });  
Console.WriteLine("custOrdDoc {0}", errors ? "did not validate" : "validated");  
  
Console.WriteLine();  
// Modify the source document so that it will not validate.  
custOrdDoc.Root.Element("Orders").Element("Order").Element("CustomerID").Value = "AAAAA";  
Console.WriteLine("Attempting to validate after modification");  
errors = false;  
custOrdDoc.Validate(schemas, (o, e) =>  
                     {  
                         Console.WriteLine("{0}", e.Message);  
                         errors = true;  
                     });  
Console.WriteLine("custOrdDoc {0}", errors ? "did not validate" : "validated");  
```  
  
 Ten przykład generuje następujące wyniki:  
  
```output  
Attempting to validate  
custOrdDoc validated  
  
Attempting to validate after modification  
The key sequence 'AAAAA' in Keyref fails to refer to some key.  
custOrdDoc did not validate  
```  
  
## <a name="see-also"></a>Zobacz też

- <xref:System.Xml.Schema.Extensions.Validate%2A>
- [Tworzenie drzew XML (C#)](creating-xml-trees-linq-to-xml-2.md)
