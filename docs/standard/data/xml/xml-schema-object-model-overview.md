---
title: Model SOM (XML Schema Object Model) ― omówienie
ms.date: 03/30/2017
ms.assetid: 896a1e12-5655-42c6-8cdd-89c12862b34b
ms.openlocfilehash: 62560b641c43f2210b052e9880f2d945dbae0c6f
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95733103"
---
# <a name="xml-schema-object-model-overview"></a>Model SOM (XML Schema Object Model) ― omówienie

Model obiektów schematu (SOM) w Microsoft .NET Framework to bogaty interfejs API, który umożliwia Programistyczne tworzenie, edytowanie i sprawdzanie poprawności schematów. Model SOM działa na dokumentach schematu XML podobnie do sposobu działania Document Object Model (DOM) w dokumentach XML. Dokumenty schematu XML są prawidłowymi plikami XML, które po załadowaniu do modelu SOM, przekazując znaczenie dotyczące struktury i ważności innych dokumentów XML, które są zgodne ze schematem.  
  
 Schemat to dokument XML, który definiuje klasę dokumentów XML, określając strukturę lub model dokumentów XML dla określonego schematu. Schemat identyfikuje ograniczenia dotyczące zawartości dokumentów XML i opisuje słownictwo (reguły lub gramatyki) zgodne dokumenty XML muszą być przestrzegane, aby można je było traktować jako schemat-prawidłowy z tym konkretnym schematem. Walidacja dokumentu XML jest procesem, który gwarantuje, że dokument jest zgodny z gramatyką określoną przez schemat.  
  
 Poniżej przedstawiono sposoby tworzenia, edytowania i weryfikowania schematów przy użyciu interfejsu API modelu SOM w .NET Framework.  
  
- Załaduj i Zapisz prawidłowe schematy do i z plików.  
  
- Twórz schematy w pamięci przy użyciu klas silnie wpisanych.  
  
- Współpracuj z <xref:System.Xml.Schema.XmlSchemaSet> klasą, aby buforować, kompilować i pobierać schematy.  
  
- Współdziałanie z <xref:System.Xml.XmlReader.Create%2A> metodą <xref:System.Xml.XmlReader> klasy w celu walidacji dokumentów wystąpień XML w schematach.  
  
- Redaktorzy kompilacji do tworzenia i obsługi schematów.  
  
- Dynamicznie Edytuj schemat, który może być zgodny i zapisany do użycia w walidacji dokumentów wystąpienia XML.  
  
## <a name="the-schema-object-model"></a>Model obiektu schematu  

 Model SOM zawiera rozbudowany zestaw klas w <xref:System.Xml.Schema?displayProperty=nameWithType> przestrzeni nazw odpowiadający elementom w schemacie XML. Na przykład element jest `<xsd:schema>...</xsd:schema>` mapowany do <xref:System.Xml.Schema.XmlSchema?displayProperty=nameWithType> klasy, a wszystkie informacje, które mogą być zawarte w `<xsd:schema/>` elemencie mogą być reprezentowane za pomocą <xref:System.Xml.Schema.XmlSchema> klasy. Podobnie `<xsd:element>...</xsd:element>` elementy i są `<xsd:attribute>...</xsd:attribute>` mapowane <xref:System.Xml.Schema.XmlSchemaElement?displayProperty=nameWithType> odpowiednio do klas i <xref:System.Xml.Schema.XmlSchemaAttribute?displayProperty=nameWithType> . To mapowanie będzie kontynuowane dla wszystkich elementów schematu XML tworzących model obiektów schematu XML w <xref:System.Xml.Schema> przestrzeni nazw przedstawiony na poniższym diagramie.  
  
 ![System.Xml. Model obiektów schematu](./media/xml-schema-object-model-overview/xml-schema-object-model.gif)  
  
 Aby uzyskać więcej informacji na temat każdej klasy w <xref:System.Xml.Schema> przestrzeni nazw, zobacz <xref:System.Xml.Schema> dokumentację odwołań do przestrzeni nazw w bibliotece klas .NET Framework.  
  
## <a name="see-also"></a>Zobacz także

- [Odczytywanie i zapisywanie schematów XML](reading-and-writing-xml-schemas.md)
- [Tworzenie schematów XML](building-xml-schemas.md)
- [Przechodzenie schematów XML](traversing-xml-schemas.md)
- [Edytowanie schematów XML](editing-xml-schemas.md)
- [Uwzględnianie lub importowanie schematów XML](including-or-importing-xml-schemas.md)
- [Klasa XmlSchemaSet na potrzeby kompilacji schematu](xmlschemaset-for-schema-compilation.md)
- [Zestaw informacji po kompilacji schematu](post-schema-compilation-infoset.md)
