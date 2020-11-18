---
title: Weryfikacja schematu XML (XSD) przy użyciu klasy XmlSchemaCollection
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: ad0b5717-3d32-41ad-a4d7-072c3e492b82
ms.openlocfilehash: 08eeb8440f89e488685e474bed607002f8ab6386
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "94824587"
---
# <a name="xml-schema-xsd-validation-with-xmlschemacollection"></a>Weryfikacja schematu XML (XSD) przy użyciu klasy XmlSchemaCollection
Za pomocą programu można <xref:System.Xml.Schema.XmlSchemaCollection> sprawdzić poprawność dokumentu XML względem schematów języka definicji schematu XML (XSD). <xref:System.Xml.Schema.XmlSchemaCollection>Zwiększa wydajność dzięki przechowywaniu schematów w kolekcji, tak aby nie były ładowane do pamięci po każdym wystąpieniu walidacji. Jeśli schemat istnieje w kolekcji schematów, ten `schemaLocation` atrybut jest używany do wyszukania schematu w kolekcji.  
  
> [!IMPORTANT]
> <xref:System.Xml.Schema.XmlSchemaCollection>Klasa jest obecnie przestarzała i została zastąpiona <xref:System.Xml.Schema.XmlSchemaSet> klasą. Aby uzyskać więcej informacji na temat <xref:System.Xml.Schema.XmlSchemaSet> klasy, zobacz zestaw [XmlSchemaSet dla kompilacji schematu](xmlschemaset-for-schema-compilation.md).  
  
 Poniższy przykład pokazuje element główny pliku danych.  
  
```xml  
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"  
    xmlns="urn:bookstore-schema"  
    elementFormDefault="qualified"  
    targetNamespace="urn:bookstore-schema">  
```  
  
 Na potrzeby tego przykładu wartość `targetNamespace` atrybutu jest `urn:bookstore-schema` , która jest tą samą przestrzenią nazw, która jest używana podczas dodawania schematu do obiektu <xref:System.Xml.Schema.XmlSchemaCollection> .  
  
 Poniższy przykład kodu dodaje schemat XML do obiektu <xref:System.Xml.Schema.XmlSchemaCollection> .  
  
```vb  
Dim xsc As New XmlSchemaCollection()  
' XML Schema.  
xsc.Add("urn:bookstore-schema", schema)
reader = New XmlTextReader(filename)  
vreader = New XmlValidatingReader(reader)  
vreader.Schemas.Add(xsc)  
```  
  
```csharp  
XmlSchemaCollection xsc = new XmlSchemaCollection();  
// XML Schema.  
xsc.Add("urn:bookstore-schema", schema);  
reader = new XmlTextReader (filename);  
vreader = new XmlValidatingReader (reader);  
vreader.Schemas.Add(xsc);  
```  
  
 Ten `targetNamespace` atrybut jest zazwyczaj używany podczas dodawania `namespaceURI` właściwości <xref:System.Xml.Schema.XmlSchemaCollection.Add%2A> metody dla <xref:System.Xml.Schema.XmlSchemaCollection> . Można określić odwołanie o wartości null przed dodaniem schematu do elementu <xref:System.Xml.Schema.XmlSchemaCollection> . Pusty ciąg ("") powinien być używany w schematach bez przestrzeni nazw. <xref:System.Xml.Schema.XmlSchemaCollection>Może mieć tylko jeden schemat bez przestrzeni nazw.  
  
 Poniższy przykład kodu dodaje schemat XML, wartość osobowy. xsd, do <xref:System.Xml.Schema.XmlSchemaCollection> i sprawdza poprawność HeadCount.xml.  
  
```vb  
Imports System  
Imports System.IO  
Imports System.Xml  
Imports System.Xml.Schema  
  
Namespace ValidationSample  
  
   Class Sample  
  
      Public Shared Sub Main()  
         Dim tr As New XmlTextReader("HeadCount.xml")  
         Dim vr As New XmlValidatingReader(tr)  
  
         vr.Schemas.Add("xsdHeadCount", "HeadCount.xsd")  
         vr.ValidationType = ValidationType.Schema  
         AddHandler vr.ValidationEventHandler, AddressOf ValidationHandler  
  
         While vr.Read()  
         End While  
         Console.WriteLine("Validation finished")  
      End Sub  
      ' Main  
  
      Public Shared Sub ValidationHandler(sender As Object, args As ValidationEventArgs)  
         Console.WriteLine("***Validation error")  
         Console.WriteLine("Severity:{0}", args.Severity)  
         Console.WriteLine("Message:{0}", args.Message)  
      End Sub  
      ' ValidationHandler  
   End Class  
   ' Sample  
End Namespace  
' ValidationSample  
```  
  
```csharp  
using System;  
using System.IO;  
using System.Xml;  
using System.Xml.Schema;  
  
namespace ValidationSample  
{  
   class Sample  
   {  
      public static void Main()  
      {  
         XmlTextReader tr = new XmlTextReader("HeadCount.xml");  
         XmlValidatingReader vr = new XmlValidatingReader(tr);  
  
         vr.Schemas.Add("xsdHeadCount", "HeadCount.xsd");  
         vr.ValidationType = ValidationType.Schema;  
         vr.ValidationEventHandler += new ValidationEventHandler (ValidationHandler);  
  
         while(vr.Read());  
         Console.WriteLine("Validation finished");  
      }  
  
      public static void ValidationHandler(object sender, ValidationEventArgs args)  
      {  
         Console.WriteLine("***Validation error");  
         Console.WriteLine("\tSeverity:{0}", args.Severity);  
         Console.WriteLine("\tMessage  :{0}", args.Message);  
      }  
   }  
}  
```  
  
 Poniżej przedstawiono zawartość pliku wejściowego, HeadCount.xml, aby sprawdzić poprawność.  
  
```xml  
<!--Load HeadCount.xsd in SchemaCollection for Validation-->  
<hc:HeadCount xmlns:hc='xsdHeadCount'>  
   <Name>Waldo Pepper</Name>  
   <Name>Red Pepper</Name>  
</hc:HeadCount>  
```  
  
 Poniżej przedstawiono zawartość pliku schematu XML, np. xsd, do zweryfikowania.  
  
```xml  
<xs:schema xmlns="xsdHeadCount" targetNamespace="xsdHeadCount" xmlns:xs="http://www.w3.org/2001/XMLSchema">  
   <xs:element name='HeadCount' type="HEADCOUNT"/>  
   <xs:complexType name="HEADCOUNT">  
      <xs:sequence>  
         <xs:element name='Name' type='xs:string' maxOccurs='unbounded'/>  
      </xs:sequence>  
      <xs:attribute name='division' type='xs:int' use='optional' default='8'/>  
   </xs:complexType>  
</xs:schema>  
```  
  
 Poniższy przykład kodu tworzy obiekt <xref:System.Xml.XmlValidatingReader> , który przyjmuje <xref:System.Xml.XmlTextReader> . Plik wejściowy, sample4.xml, jest sprawdzany pod kątem schematu XML, sample4. xsd.  
  
```vb  
Dim tr As New XmlTextReader("sample4.xml")  
Dim vr As New XmlValidatingReader(tr)  
vr.ValidationType = ValidationType.Schema  
vr.Schemas.Add("datatypesTest", "sample4.xsd")  
AddHandler vr.ValidationEventHandler, AddressOf ValidationCallBack  
While vr.Read()  
   Console.WriteLine("NodeType: {0} NodeName: {1}", vr.NodeType, vr.Name)  
End While  
```  
  
```csharp  
XmlTextReader tr = new XmlTextReader("sample4.xml");  
XmlValidatingReader vr = new XmlValidatingReader(tr);  
vr.ValidationType = ValidationType.Schema;  
        vr.Schemas.Add("datatypesTest", "sample4.xsd");  
vr.ValidationEventHandler += new ValidationEventHandler(ValidationCallBack);  
while(vr.Read()) {  
    Console.WriteLine("NodeType: {0} NodeName: {1}", vr.NodeType, vr.Name);  
    }  
```  
  
 Poniżej przedstawiono zawartość pliku wejściowego, sample4.xml, aby sprawdzić poprawność.  
  
```xml  
<datatypes xmlns="datatypesTest">  
    <number>  
        <number_1>123</number_1>  
    </number>  
</datatypes>  
```  
  
 Poniżej przedstawiono zawartość pliku schematu XML, sample4. xsd, aby sprawdzić poprawność.  
  
```xml  
<xs:schema
    xmlns:xs="http://www.w3.org/2001/XMLSchema"
    xmlns:tns="datatypesTest"
    targetNamespace="datatypesTest"  
    elementFormDefault="qualified">  
  
<xs:element name = "datatypes">  
  <xs:complexType>  
    <xs:all>  
        <xs:element name="number">  
            <xs:complexType>  
                <xs:sequence>  
                    <xs:element name="number_1" type="xs:decimal" maxOccurs="unbounded"/>  
                </xs:sequence>  
            </xs:complexType>  
        </xs:element>  
    </xs:all>  
  </xs:complexType>  
</xs:element>  
</xs:schema>  
```  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Xml.XmlParserContext>
- <xref:System.Xml.XmlValidatingReader.ValidationEventHandler?displayProperty=nameWithType>
- <xref:System.Xml.XmlValidatingReader.Schemas%2A?displayProperty=nameWithType>
- [Kompilacja schematu a klasa XmlSchemaCollection](xmlschemacollection-schema-compilation.md)
