---
title: Znajdowanie domyślnego stylu akapitu (C#)
description: Dowiedz się, jak przetwarzać dokument WordprocessingML za pomocą LINQ w języku C#. Ten przykład umożliwia znalezienie domyślnego stylu akapitów w dokumencie.
ms.date: 07/20/2015
ms.assetid: be102177-8ab0-444a-b671-7023e555ffdb
ms.openlocfilehash: e18bbbdbd5b2627c9ff4c3c3eedd84d7cb166a62
ms.sourcegitcommit: 04022ca5d00b2074e1b1ffdbd76bec4950697c4c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/23/2020
ms.locfileid: "87103827"
---
# <a name="finding-the-default-paragraph-style-c"></a>Znajdowanie domyślnego stylu akapitu (C#)
Pierwsze zadanie w informacjach manipulowania w programie WordprocessingML Documents to znalezienie domyślnego stylu akapitów w dokumencie.  
  
## <a name="example"></a>Przykład  
  
### <a name="description"></a>Opis  
 W poniższym przykładzie zostanie otwarty dokument pakietu Office Open XML WordprocessingML, znajduje się w nim części dokumentu i stylu pakietu, a następnie wykonywana jest kwerenda, która znajduje domyślną nazwę stylu. Aby uzyskać informacje na temat pakietów dokumentów Office Open XML i części, które składają się z, zobacz [szczegóły dotyczące dokumentów pakietu Office Open XML WordprocessingML (C#)](./wordprocessingml-document-with-styles.md).  
  
 Zapytanie znajduje węzeł o nazwie `w:style` , który ma atrybut o nazwie o `w:type` wartości "Paragraph", a także ma atrybut o nazwie o `w:default` wartości "1". Ponieważ będzie istnieć tylko jeden węzeł XML z tymi atrybutami, zapytanie używa <xref:System.Linq.Enumerable.First%2A?displayProperty=nameWithType> operatora do konwersji kolekcji na pojedynczą. Następnie pobiera wartość atrybutu o nazwie `w:styleId` .  
  
 W tym przykładzie zastosowano klasy z zestawu 'Windowsbase. Używa typów w <xref:System.IO.Packaging?displayProperty=nameWithType> przestrzeni nazw.  
  
### <a name="code"></a>Kod  
  
```csharp  
const string fileName = "SampleDoc.docx";  
  
const string documentRelationshipType =  
  "http://schemas.openxmlformats.org/officeDocument/2006/relationships/officeDocument";  
const string stylesRelationshipType =  
  "http://schemas.openxmlformats.org/officeDocument/2006/relationships/styles";  
const string wordmlNamespace =  
  "http://schemas.openxmlformats.org/wordprocessingml/2006/main";  
XNamespace w = wordmlNamespace;  
  
XDocument xDoc = null;  
XDocument styleDoc = null;  
  
using (Package wdPackage = Package.Open(fileName, FileMode.Open, FileAccess.Read))  
{  
    PackageRelationship docPackageRelationship =  
      wdPackage.GetRelationshipsByType(documentRelationshipType).FirstOrDefault();  
    if (docPackageRelationship != null)  
    {  
        Uri documentUri = PackUriHelper.ResolvePartUri(new Uri("/", UriKind.Relative),  
          docPackageRelationship.TargetUri);  
        PackagePart documentPart = wdPackage.GetPart(documentUri);  
  
        //  Load the document XML in the part into an XDocument instance.  
        xDoc = XDocument.Load(XmlReader.Create(documentPart.GetStream()));  
  
        //  Find the styles part. There will only be one.  
        PackageRelationship styleRelation =  
          documentPart.GetRelationshipsByType(stylesRelationshipType).FirstOrDefault();  
        if (styleRelation != null)  
        {  
            Uri styleUri = PackUriHelper.ResolvePartUri(documentUri, styleRelation.TargetUri);  
            PackagePart stylePart = wdPackage.GetPart(styleUri);  
  
            //  Load the style XML in the part into an XDocument instance.  
            styleDoc = XDocument.Load(XmlReader.Create(stylePart.GetStream()));  
        }  
    }  
}  
  
// The following query finds all the paragraphs that have the default style.  
string defaultStyle =
    (string)(  
        from style in styleDoc.Root.Elements(w + "style")  
        where (string)style.Attribute(w + "type") == "paragraph"&&  
              (string)style.Attribute(w + "default") == "1"  
              select style  
    ).First().Attribute(w + "styleId");  
  
Console.WriteLine("The default style is: {0}", defaultStyle);  
```  
  
### <a name="comments"></a>Komentarze  
 Ten przykład generuje następujące wyniki:  
  
```output  
The default style is: Normal  
```  
  
## <a name="next-steps"></a>Następne kroki  
 W następnym przykładzie utworzysz podobne zapytanie, które znajdzie wszystkie akapity w dokumencie i ich style:  
  
- [Pobieranie akapitów i ich stylów (C#)](./retrieving-the-paragraphs-and-their-styles.md)  
