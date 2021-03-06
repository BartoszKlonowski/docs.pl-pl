---
title: Sprawdzanie poprawności schematu XML (XSD) przy użyciu klasy XmlSchemaSet
description: Dowiedz się, jak sprawdzać poprawność dokumentów XML względem schematu języka definicji schematu XML (XSD) przy użyciu klasy XmlSchemaSet w programie .NET.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
ms.assetid: 359b10eb-ec05-4cc6-ac96-c2b060afc4de
ms.openlocfilehash: 82944fd3fb97c3086ffd47fbd2ba1f3192e6deb4
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95672256"
---
# <a name="xml-schema-xsd-validation-with-xmlschemaset"></a>Walidacja schematu XML (XSD) z zestawem XmlSchemaSet

Dokumenty XML można sprawdzić pod kątem schematu języka definicji schematu XML (XSD) w <xref:System.Xml.Schema.XmlSchemaSet> .  
  
## <a name="validate-xml-documents"></a>Sprawdzanie poprawności dokumentów XML  

 Dokumenty XML są sprawdzane za pomocą <xref:System.Xml.XmlReader.Create%2A> metody <xref:System.Xml.XmlReader> klasy. Aby sprawdzić poprawność dokumentu XML, Utwórz <xref:System.Xml.XmlReaderSettings> obiekt, który zawiera schemat języka definicji schematu XML (XSD), za pomocą którego można sprawdzić poprawność dokumentu XML.  
  
> [!NOTE]
> <xref:System.Xml.Schema>Przestrzeń nazw zawiera metody rozszerzające, które ułatwiają Weryfikowanie drzewa XML względem pliku XSD przy użyciu [LINQ to XML (C#)](../../linq/linq-xml-overview.md) i [LINQ to XML (Visual Basic)](../../linq/linq-xml-overview.md). Aby uzyskać więcej informacji na temat walidacji dokumentów XML za pomocą LINQ to XML, zobacz [How to Validate using XSD (LINQ to XML) (C#)](../../linq/validate-xsd.md) i [How to: Validate using XSD (LINQ to XML) (Visual Basic)](../../linq/validate-xsd.md).
  
 Pojedynczy schemat lub zestaw schematów (jako <xref:System.Xml.Schema.XmlSchemaSet> ) można dodać do obiektu, <xref:System.Xml.Schema.XmlSchemaSet> przekazując jeden jako parametr do <xref:System.Xml.Schema.XmlSchemaSet.Add%2A> metody <xref:System.Xml.Schema.XmlSchemaSet> . Podczas sprawdzania poprawności dokumentu docelowa przestrzeń nazw dokumentu musi być zgodna z docelową przestrzenią nazw schematu w zestawie schematów.  
  
 Poniżej znajduje się przykładowy dokument XML.  
  
 [!code-xml[XSDInference Examples #5](../../../../samples/snippets/xml/VS_Snippets_Data/XSDInference Examples/XML/contosoBooks.xml#5)]  
  
 Poniżej znajduje się schemat, który sprawdza poprawność przykładowego dokumentu XML.  
  
 [!code-xml[XSDInference Examples #6](../../../../samples/snippets/xml/VS_Snippets_Data/XSDInference Examples/XML/contosoBooks.xsd#6)]  
  
 W poniższym przykładzie kodu schemat został dodany do <xref:System.Xml.XmlReaderSettings.Schemas%2A> właściwości <xref:System.Xml.XmlReaderSettings> obiektu. <xref:System.Xml.XmlReaderSettings>Obiekt jest przekazaniem jako parametr do <xref:System.Xml.XmlReader.Create%2A> metody <xref:System.Xml.XmlReader> obiektu, który sprawdza powyższy dokument XML.  
  
 <xref:System.Xml.XmlReaderSettings.ValidationType%2A>Właściwość <xref:System.Xml.XmlReaderSettings> obiektu jest ustawiona na tak, aby `Schema` wymuszać walidację dokumentu XML przez <xref:System.Xml.XmlReader.Create%2A> metodę <xref:System.Xml.XmlReader> obiektu. Element <xref:System.Xml.Schema.ValidationEventHandler> jest dodawany do <xref:System.Xml.XmlReaderSettings> obiektu, aby obsłużyć dowolne <xref:System.Xml.Schema.XmlSeverityType.Warning> lub <xref:System.Xml.Schema.XmlSeverityType.Error> zdarzenia zgłoszone przez błędy znalezione podczas procesu weryfikacji zarówno dokumentu XML, jak i schematu.  
  
 [!code-cpp[XmlSchemaSetOverall Example #1](../../../../samples/snippets/cpp/VS_Snippets_Data/XmlSchemaSetOverall Example/CPP/xmlschemasetexample.cpp#1)]
 [!code-csharp[XmlSchemaSetOverall Example #1](../../../../samples/snippets/csharp/VS_Snippets_Data/XmlSchemaSetOverall Example/CS/xmlschemasetexample.cs#1)]
 [!code-vb[XmlSchemaSetOverall Example #1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XmlSchemaSetOverall Example/VB/xmlschemasetexample.vb#1)]  
  
## <a name="see-also"></a>Zobacz także

- [Klasa XmlSchemaSet na potrzeby kompilacji schematu](xmlschemaset-for-schema-compilation.md)
- [Praca ze schematami XML](working-with-xml-schemas.md)
