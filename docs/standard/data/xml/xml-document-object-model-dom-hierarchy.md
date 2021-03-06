---
title: Hierarchia modelu DOM (XML Document Object Model)
ms.date: 03/30/2017
ms.assetid: 9d187d4f-c76e-4223-a670-cc290783ce47
ms.openlocfilehash: 24ef51a18392fe3034e64bd585d879941fca4b95
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95718361"
---
# <a name="xml-document-object-model-dom-hierarchy"></a>Hierarchia modelu DOM (XML Document Object Model)

Na poniższej ilustracji przedstawiono hierarchię klas dla Document Object Model XML (DOM), z nazwą organizacja World Wide Web Consortium (W3C) w nawiasie wraz z nazwą klasy, w której ma zastosowanie.  
  
 ![Hierarchia&#41; Document Object Model XML &#40;DOM](media/dom-class-hierarchy.gif "Dom_class_hierarchy")  
Hierarchia XML Document Object Model (DOM)  
  
 Następujące klasy nie dziedziczą z **XmlNode**:  
  
- **XmlImplementation**  
  
- **XmlNamedNodeMap**  
  
- **XmlNodeList**  
  
- **XmlNodeChangedEventArgs**  
  
 Klasa **XmlImplementation** służy do tworzenia dokumentu XML. Aby uzyskać więcej informacji, zobacz [Tworzenie dokumentów XML](xml-document-creation.md).  
  
 Klasa **XmlNamedNodeMap** obsługuje nieuporządkowany zestaw węzłów. Aby uzyskać więcej informacji, zobacz [nieuporządkowane pobieranie węzłów według nazwy lub indeksu](unordered-node-retrieval-by-name-or-index.md).  
  
 Klasa **XmlNodeList** obsługuje uporządkowaną listę węzłów. Aby uzyskać więcej informacji, zobacz [uporządkowane pobieranie węzłów według indeksu](ordered-node-retrieval-by-index.md).  
  
 Klasa **XmlNodeChangedEventArgs** obsługuje programy obsługi zdarzeń zarejestrowane w **dokumencie XmlDocument**. Aby uzyskać więcej informacji, zobacz [Obsługa zdarzeń w dokumencie XML przy użyciu XmlNodeChangedEventArgs](event-handling-in-an-xml-document-using-the-xmlnodechangedeventargs.md).  
  
 Klasa **XmlLinkedNode** dziedziczy z klasy **XmlNode**. Celem jest przesłonięcie dwóch metod z klasy **XmlNode**: metod **PreviousSibling** i **NextSibling** . Te zastąpione metody są następnie dziedziczone i używane przez **XmlCharacterData**, **xmldeklaracji**, **XmlDocumentType**, **XmlElement**, **XmlEntityReference** i **XmlProcessingInstruction**, które są klasami, które mają poprzednie i następne elementy równorzędne.  
  
## <a name="see-also"></a>Zobacz także

- [XML Document Object Model (DOM)](xml-document-object-model-dom.md)
