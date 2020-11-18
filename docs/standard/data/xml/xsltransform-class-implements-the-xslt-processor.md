---
title: Implementowanie procesora XSLT przy użyciu klasy XslTransform
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 88373fe2-4a6b-44f9-8a62-8a3e348e3a46
ms.openlocfilehash: 57632321edf086b644da7ea4fca893edb589834f
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "94818182"
---
# <a name="xsltransform-class-implements-the-xslt-processor"></a>Implementowanie procesora XSLT przy użyciu klasy XslTransform

> [!NOTE]
> <xref:System.Xml.Xsl.XslTransform>Klasa jest przestarzała w .NET Framework 2,0. Można wykonać przekształcenia Extensible Stylesheet Language for Transformations (XSLT) przy użyciu <xref:System.Xml.Xsl.XslCompiledTransform> klasy. Aby uzyskać więcej informacji, zobacz [Używanie klasy XslCompiledTransform](using-the-xslcompiledtransform-class.md) i [Migrowanie z klasy XslTransform](migrating-from-the-xsltransform-class.md) .

<xref:System.Xml.Xsl.XslTransform>Klasa to procesor XSLT implementujący zalecenia dotyczące wersji 1,0 przekształcenia XSL (XSLT). <xref:System.Xml.Xsl.XslTransform.Load%2A>Metoda lokalizuje i odczytuje arkusze stylów, a <xref:System.Xml.Xsl.XslTransform.Transform%2A> Metoda przekształca dany dokument źródłowy. Dowolny magazyn, który implementuje <xref:System.Xml.XPath.IXPathNavigable> interfejs, może być używany jako dokument źródłowy dla <xref:System.Xml.Xsl.XslTransform> . .NET Framework obecnie implementuje <xref:System.Xml.XPath.IXPathNavigable> interfejs w <xref:System.Xml.XmlDocument> ,, <xref:System.Xml.XmlDataDocument> i <xref:System.Xml.XPath.XPathDocument> , dlatego wszystkie z nich mogą być używane jako wejściowy dokument źródłowy do przekształcenia.

<xref:System.Xml.Xsl.XslTransform>Obiekt w .NET Framework obsługuje specyfikację XSLT 1,0, zdefiniowaną za pomocą następującej przestrzeni nazw:

```xml
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" version="1.0">
```

Arkusz stylów można załadować przy użyciu <xref:System.Xml.Xsl.XslTransform.Load%2A> metody z jednej z następujących klas:

- Pustym XPathNavigator

- Elementu

- Ciąg reprezentujący adres URL

Istnieje inna <xref:System.Xml.Xsl.XslTransform.Load%2A> Metoda dla każdej z powyższych klas wejściowych. Niektóre metody przyjmują kombinację jednej z tych klas i <xref:System.Xml.XmlResolver> klasy jako argumenty. <xref:System.Xml.XmlResolver>Lokalizuje zasoby, do których odwołuje się `<xsl:import>` lub które `<xsl:include>` znajdują się w arkuszu stylów. Następujące metody przyjmują ciąg, <xref:System.Xml.XmlReader> lub <xref:System.Xml.XPath.XPathNavigator> jako dane wejściowe.

```vb
Overloads Public Sub Load(String)
```

```csharp
public void Load(string);
```

```vb
Overloads Public Sub Load(String, XmlResolver)
```

```csharp
public void Load(string, XmlResolver);
```

```vb
Overloads Public Sub Load(XmlReader, XmlResolver, Evidence)
```

```csharp
public void Load(XmlReader, XmlResolver, Evidence);
```

```vb
Overloads Public Sub Load(XPathNavigator, XmlResolver, Evidence)
```

```csharp
public void Load(XPathNavigator, XmlResolver, Evidence);
```

Większość <xref:System.Xml.Xsl.XslTransform.Load%2A> metod przedstawionych powyżej przyjmuje <xref:System.Xml.XmlResolver> jako parametr. <xref:System.Xml.XmlResolver>Służy do ładowania arkusza stylów i wszystkich arkuszy stylów, do których odwołuje się element xsl: import i xsl: include.

Większość <xref:System.Xml.Xsl.XslTransform.Load%2A> metod przyjmuje również dowody jako parametr. Parametr zeznania jest <xref:System.Security.Policy.Evidence> skojarzony z arkuszem stylów. Poziom zabezpieczeń arkusza stylów wpływa na poziom zabezpieczeń wszelkich kolejnych zasobów, do których się odwołuje, takich jak skrypt, który zawiera, wszelkie `document()` używane przez niego funkcje i wszystkie obiekty rozszerzeń używane przez <xref:System.Xml.Xsl.XsltArgumentList> .

Jeśli arkusz stylów jest ładowany przy użyciu metody zawierającej <xref:System.Xml.Xsl.XslTransform.Load%2A> parametr adresu URL, a żadne dowody nie są dostarczane, dowód arkusza stylów jest obliczany przez połączenie podanego adresu URL ze swoją lokacją i strefą.

Jeśli nie podano żadnego identyfikatora URI lub dowodu, oznacza to, że dowody ustawione dla arkusza stylów są w pełni zaufane. Nie Ładuj arkuszy stylów z niezaufanych źródeł ani nie dodawaj niezaufanych obiektów rozszerzenia do <xref:System.Xml.Xsl.XsltArgumentList> .

Aby uzyskać więcej informacji na temat poziomów zabezpieczeń i dowodów, jak ma to wpływ na skrypty, zobacz [XSLT stylesheet Scripting using \<msxsl:script> ](xslt-stylesheet-scripting-using-msxsl-script.md). Aby uzyskać informacje na temat poziomów zabezpieczeń i dowodów, jak ma to wpływ na obiekty rozszerzeń, zobacz [XsltArgumentList for Style Sheet Parameters and Extension Objects](xsltargumentlist-for-style-sheet-parameters-and-extension-objects.md).

Aby uzyskać informacje na temat poziomów zabezpieczeń i dowodów, jak ma to wpływ na `document()` funkcję, zobacz [rozpoznawanie zewnętrznych arkuszy stylów XSLT i dokumentów](resolving-external-xslt-style-sheets-and-documents.md).

Arkusz stylów może być dostarczony z liczbą parametrów wejściowych. Arkusz stylów może również wywoływać funkcje dla obiektów rozszerzeń. Oba parametry i obiekty rozszerzeń są dostarczane do arkusza stylów przy użyciu <xref:System.Xml.Xsl.XsltArgumentList> klasy. Aby uzyskać więcej informacji na temat <xref:System.Xml.Xsl.XsltArgumentList> , zobacz <xref:System.Xml.Xsl.XsltArgumentList> .

## <a name="recommended-secure-use-of-xsltransform-class"></a>Zalecane bezpieczne użycie klasy XslTransform

Uprawnienia zabezpieczeń arkusza stylów zależą od dostarczonych dowodów. Poniższa tabela zawiera podsumowanie lokalizacji arkusza stylów i zawiera objaśnienie typu dowodu do przekazania.

- Arkusz stylów XSLT nie ma odwołań zewnętrznych lub arkusz stylów pochodzi z zaufanej podstawy kodu.

  - Podaj dowody z Twojego zestawu:

    ```vb
    Dim xslt = New XslTransform() xslt.Load(stylesheet, resolver, Me.GetType().Assembly.Evidence)

    XsltTransform xslt = new XslTransform();  xslt.Load(stylesheet, resolver, this.GetType().Assembly.Evidence);
    ```

- Arkusz stylów XSLT pochodzi ze źródła zewnętrznego. Źródło źródła jest znane i istnieje zweryfikowany identyfikator URI.

  - Utwórz dowód przy użyciu identyfikatora URI.

    ```vb
    Dim xslt As New XslTransform() Dim ev As Evidence = XmlSecureResolver.CreateEvidenceForUrl(stylesheetUri) xslt.Load(stylesheet, resolver, evidence)

    XslTransform xslt = new XslTransform(); Evidence ev = XmlSecureResolver.CreateEvidenceForUrl(stylesheetUri); xslt.Load(stylesheet, resolver, evidence);
    ```

- Arkusz stylów XSLT pochodzi ze źródła zewnętrznego. Źródło źródła jest nieznane.

  - Ustaw dowód na `null` . Bloki skryptów nie są przetwarzane, funkcja XSLT `document()` nie jest obsługiwana, a uprzywilejowane obiekty rozszerzeń są niedozwolone.

    Ponadto można również ustawić `resolver` parametr na `null` to gwarantuje, że `xsl:import` `xsl:include` elementy i nie są przetwarzane.

- Arkusz stylów XSLT pochodzi ze źródła zewnętrznego. Źródło źródła jest nieznane, ale wymagana jest obsługa skryptów.

  - Zażądaj dowodu od wywołującego.

## <a name="transformation-of-xml-data"></a>Przekształcanie danych XML

Po załadowaniu arkusza stylów transformację rozpocznie się, wywołując jedną z <xref:System.Xml.Xsl.XslTransform.Transform%2A> metod i dostarczając wejściowy dokument źródłowy. <xref:System.Xml.Xsl.XslTransform.Transform%2A>Metoda jest przeciążona, aby zapewnić różne wyjścia transformacji. Transformacja może spowodować następujące formaty wyjściowe:

- <xref:System.Xml.XmlReader>

- <xref:System.Xml.XmlWriter>

- <xref:System.IO.TextWriter>

- <xref:System.IO.Stream>

- Adres URL ciągu pliku

Ten ostatni format, adres URL ciągu, zapewnia często używany scenariusz do przekształcania dokumentu wejściowego znajdującego się w adresie URL i zapisywania dokumentu w wyjściowym adresie URL. Ta <xref:System.Xml.Xsl.XslTransform.Transform%2A> Metoda jest wygodną metodą ładowania dokumentu XML z pliku, wykonywania transformacji XSLT i zapisywania danych wyjściowych do pliku. Uniemożliwia to utworzenie i załadowanie wejściowego dokumentu źródłowego, a następnie zapisanie go w strumieniu pliku. Poniższy przykład kodu pokazuje użycie <xref:System.Xml.Xsl.XslTransform.Transform%2A> metody przy użyciu ciągu adresu URL jako dane wejściowe i wyjściowe:

```vb
Dim xsltransform As XslTransform = New XslTransform()
xsltransform.Load("favorite.xsl")
xsltransform.Transform("MyDocument.Xml", "TransformResult.xml", Nothing)
```

```csharp
XslTransform xsltransform = new XslTransform();
xsltransform.Load("favorite.xsl");
xsltransform.Transform("MyDocument.xml", "TransformResult.xml", null);
```

## <a name="transforming-a-section-of-an-xml-document"></a>Przekształcanie sekcji dokumentu XML

Przekształcenia są stosowane do dokumentu jako całości. Innymi słowy, jeśli przejdziesz do węzła innego niż węzeł główny dokumentu, nie uniemożliwi to proces przekształcania uzyskuje dostęp do wszystkich węzłów w załadowanym dokumencie. Aby przekształcić fragment drzewa wyników, należy utworzyć <xref:System.Xml.XmlDocument> zawierający tylko fragment drzewa wynik i przekazać go <xref:System.Xml.XmlDocument> do <xref:System.Xml.Xsl.XslTransform.Transform%2A> metody. Poniższy przykład wykonuje transformację fragmentu drzewa wynik.

```vb
Dim xslt As New XslTransform()
xslt.Load("print_root.xsl")
Dim doc As New XmlDocument()
doc.Load("library.xml")
' Create a new document containing just the result tree fragment.
Dim testNode As XmlNode = doc.DocumentElement.FirstChild
Dim tmpDoc As New XmlDocument()
tmpDoc.LoadXml(testNode.OuterXml)
' Pass the document containing the result tree fragment
' to the Transform method.
Console.WriteLine(("Passing " + tmpDoc.OuterXml + " to print_root.xsl"))
xslt.Transform(tmpDoc, Nothing, Console.Out, Nothing)
```

```csharp
XslTransform xslt = new XslTransform();
xslt.Load("print_root.xsl");
XmlDocument doc = new XmlDocument();
doc.Load("library.xml");
// Create a new document containing just the result tree fragment.
XmlNode testNode = doc.DocumentElement.FirstChild;
XmlDocument tmpDoc = new XmlDocument();
tmpDoc.LoadXml(testNode.OuterXml);
// Pass the document containing the result tree fragment
// to the Transform method.
Console.WriteLine("Passing " + tmpDoc.OuterXml + " to print_root.xsl");
xslt.Transform(tmpDoc, null, Console.Out, null);
```

W przykładzie używa się plików library.xml i print_root. xsl jako danych wejściowych i wyprowadza następujące dane do konsoli programu:

```console
Passing <book genre="novel" ISBN="1-861001-57-5"><title>Pride And Prejudice</title></book> to print_root.xsl
Root node is book.
```

library.xml

```xml
<library>
  <book genre='novel' ISBN='1-861001-57-5'>
     <title>Pride And Prejudice</title>
  </book>
  <book genre='novel' ISBN='1-81920-21-2'>
     <title>Hook</title>
  </book>
</library>
```

print_root. xsl

```xml
<stylesheet version="1.0" xmlns="http://www.w3.org/1999/XSL/Transform" >
  <output method="text" />
  <template match="/">
     Root node is  <value-of select="local-name(//*[position() = 1])" />
  </template>
</stylesheet>
```

## <a name="migration-of-xslt-from-net-framework-version-10-to-net-framework-version-11"></a>Migracja XSLT z .NET Framework wersja 1,0 do .NET Framework wersja 1,1

W poniższej tabeli przedstawiono przestarzałe metody .NET Framework w wersji 1,0 oraz nowe metody .NET Framework w wersji 1,1 dla <xref:System.Xml.Xsl.XslTransform.Load%2A> metody. Nowe metody umożliwiają ograniczenie uprawnień arkusza stylów przez określenie dowodu.

|Przestarzałe metody ładowania .NET Framework w wersji 1,0|Zastępowanie metod ładowania .NET Framework w wersji 1,1|
|------------------------------------------------------|---------------------------------------------------------|
|Załaduj (dane wejściowe XPathNavigator);<br /><br /> Załaduj (dane wejściowe.|Załaduj (XPathNavigator StyleSheet, sqlresolverer, dowód potwierdzający);|
|Ładowanie (arkusz stylów IXPathNavigable);<br /><br /> Załaduj (IXPathNavigable StyleSheet, sqlresolverer);|Load (IXPathNavigable StyleSheet, procedura rozpoznawania nazw XmlResolver, dowód dowodu);|
|Ładowanie (arkusz stylów XmlReader);<br /><br /> Załaduj (XmlReader StyleSheet, xmlresolverer);|Załaduj (XmlReader StyleSheet, XmlResolver, resolver, dowód potwierdzający);|

W poniższej tabeli przedstawiono przestarzałe i nowe metody dla <xref:System.Xml.Xsl.XslTransform.Transform%2A> metody. Nowe metody przyjmują <xref:System.Xml.XmlResolver> obiekt.

|Przestarzałe metody transformacji .NET Framework w wersji 1,0|Zastępowanie metod 1,1 .NET Framework wersja przekształcenia|
|-----------------------------------------------------------|--------------------------------------------------------------|
|Transformacja XmlReader (dane wejściowe XPathNavigator, XsltArgumentList args)|Przekształcanie XmlReader (dane wejściowe XPathNavigator, XsltArgumentList args, mechanizm rozwiązywania konfliktów XmlResolver)|
|XmlReader Transform (IXPathNavigable Input, XsltArgumentList args)|XmlReader Transform (IXPathNavigable Input, XsltArgumentList args, xmlresolverer)|
|Unieważnij transformację (dane wejściowe XPathNavigator, XsltArgumentList args, wynik XmlWriter)|Unieważnij transformację (dane wejściowe XPathNavigator, XsltArgumentList args, dane wyjściowe XmlWriter, mechanizm rozwiązywania konfliktów XmlResolver)|
|Void Transform (dane wejściowe IXPathNavigable, XsltArgumentList args, dane wyjściowe XmlWriter)|Unieważnij transformację (dane wejściowe IXpathNavigable, XsltArgumentList args, dane wyjściowe XmlWriter, mechanizm rozwiązywania konfliktów XmlResolver)|
|Void Transform (dane wejściowe XPathNavigator, XsltArgumentList argumentów, wynik TextWriter)|Unieważnij transformację (dane wejściowe XPathNavigator, XsltArgumentList args, dane wyjściowe TextWriter, mechanizm rozwiązywania konfliktów XmlResolver)|
|Void Transform (IXPathNavigable Input, XsltArgumentList args, TextWriter Output)|Void Transform (dane wejściowe IXPathNavigable, XsltArgumentList args, TextWriter Output, resolver XmlResolver)|
|Void Transform (dane wejściowe XPathNavigator, XsltArgumentList args, wyjście strumienia)|Void Transform (dane wejściowe XPathNavigator, XsltArgumentList args, dane wyjściowe strumienia, mechanizm rozwiązywania konfliktów XmlResolver)|
|Void Transform (IXPathNavigable Input, XsltArgumentList args, strumień wyjściowy)|Void Transform (dane wejściowe IXPathNavigable, XsltArgumentList args, dane wyjściowe strumienia, mechanizm rozwiązywania konfliktów XmlResolver)|
|Void Transform (ciąg wejściowy, ciąg wyjściowy);|Unieważnij transformację (dane wejściowe ciągów, ciągi danych wyjściowych, mechanizm rozwiązywania konfliktów XmlResolver);|

<xref:System.Xml.Xsl.XslTransform.XmlResolver%2A?displayProperty=nameWithType>Właściwość jest przestarzała w .NET Framework w wersji 1,1. Zamiast tego należy użyć nowych <xref:System.Xml.Xsl.XslTransform.Transform%2A> przeciążeń, które pobierają <xref:System.Xml.XmlResolver> obiekt.

## <a name="see-also"></a>Zobacz także

- <xref:System.Xml.Xsl.XslTransform>
- [Przekształcenia XSLT przy użyciu klasy XslTransform](xslt-transformations-with-the-xsltransform-class.md)
- [Klasa XPathNavigator w przekształceniach](xpathnavigator-in-transformations.md)
- [Klasa XPathNodeIterator w przekształceniach](xpathnodeiterator-in-transformations.md)
- [Dane wejściowe obiektu XPathDocument klasy XslTransform](xpathdocument-input-to-xsltransform.md)
- [Dane wejściowe obiektu XmlDataDocument klasy XslTransform](xmldatadocument-input-to-xsltransform.md)
- [Dane wejściowe obiektu XmlDocument klasy XslTransform](xmldocument-input-to-xsltransform.md)
