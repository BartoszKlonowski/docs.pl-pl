---
title: Narzędzie definicji schematu XML i serializacja XML
description: Narzędzie definicji schematu XML generuje pliki klasy C# lub Visual Basic dla schematu XSD i generuje schemat XML z biblioteki lub pliku wykonywalnego.
ms.date: 03/30/2017
helpviewer_keywords:
- Xsd.exe
- XML serialization, XML Schema Definition tool
- XML Schema Definition tool
- serialization, XML Schema Definition tool
ms.assetid: 3c03f855-f931-47ff-bbc6-50c0367a16e4
ms.openlocfilehash: 6451f3b5f6e8ec2c1454e5cf7ffb95a96b620214
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90554986"
---
# <a name="the-xml-schema-definition-tool-and-xml-serialization"></a>Narzędzie definicji schematu XML i serializacja XML

Narzędzie definicji schematu XML ([narzędzie definicji schematu XML (Xsd.exe)](xml-schema-definition-tool-xsd-exe.md)) jest instalowane wraz z narzędziami .NET Framework w ramach &reg; zestawu SDK (Software Development Kit) systemu Windows. To narzędzie jest przeznaczony głównie do dwóch celów:  
  
- Aby wygenerować C# lub Visual Basic PLików klasy, które są zgodne z określonego schematu języka (XSD) definicji schematu XML. Narzędzie wykonuje schematu XML jako argument i generuje PLik, który zawiera wiele klas, gdy serializowany z <xref:System.Xml.Serialization.XmlSerializer>, zgodny ze schematem. Aby uzyskać informacje na temat sposobu użycia narzędzia do generowania klas, które są zgodne z określonym schematem, zobacz [How to: use a XML Schema Definition Tool to Generating Classes and XML Schema Documents](xml-schema-def-tool-gen.md).  
  
- Do generowania dokumentu XML schematu z PLiku .dll lub .exe. Aby wyświetlić schemat zestaw PLiki, których zostanie utworzony lub, który został zmodyfikowany z atrybutów, należy przekazać wartość DLL lub EXE jako argument do narzędzia do generowania schematu XML. Aby uzyskać informacje o sposobach generowania dokumentu schematu XML z zestawu klas przy użyciu narzędzia, zobacz [How to: use a XML Schema Definition Tool to Generating Classes and XML Schema Documents](xml-schema-def-tool-gen.md).  
  
Aby uzyskać więcej informacji na temat korzystania z tego narzędzia, zobacz [narzędzie definicji schematu XML (Xsd.exe)](xml-schema-definition-tool-xsd-exe.md).  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.Data.DataSet>
- [Wprowadzenie do serializacji XML](introducing-xml-serialization.md)
- [Narzędzie definicji schematu XML (Xsd.exe)](xml-schema-definition-tool-xsd-exe.md)
- <xref:System.Xml.Serialization.XmlSerializer>
- [Instrukcje: Serializacja obiektu](how-to-serialize-an-object.md)
- [Instrukcje: Deserializacja obiektu](how-to-deserialize-an-object.md)
- [Instrukcje: Generowanie klas i dokumentów schematu XML przy użyciu narzędzia definicji schematu XML](xml-schema-def-tool-gen.md)
- [Obsługa powiązań schematu XML](/previous-versions/dotnet/netframework-4.0/sh1e66zd(v=vs.100))
