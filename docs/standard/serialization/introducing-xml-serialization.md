---
title: Szczegóły serializacji XML
description: Serializacja Konwertuje obiekt na formularz, który można transportować. Ten artykuł zawiera omówienie serializacji XML i klasy XmlSerializer.
ms.date: 12/09/2020
dev_langs:
- csharp
- vb
helpviewer_keywords:
- XML serialization, about XML serialization
- ICollection interface, serializing
- XmlSerializer class, serializing
- serialization, about serialization
- DataSet class, serializing
- XML Schema, serializing
ms.assetid: 8c63200d-db63-4a03-a93d-21641623df62
ms.openlocfilehash: b1b5a90acce55ac7f58c1bde02fee713991dde80
ms.sourcegitcommit: 9b877e160c326577e8aa5ead22a937110d80fa44
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2020
ms.locfileid: "97110159"
---
# <a name="xml-serialization"></a>Serializacja XML

Serializacji to proces konwersji obiektu do formularza, który można łatwo przesłać. Na przykład można serializować obiekt i transportować go za pośrednictwem Internetu przy użyciu protokołu HTTP między klientem a serwerem. Z drugiej deserializacji rekonstruuje obiektów ze strumienia.

 Wykonuje serializacji XML serializację tylko publiczny pól i wartości właściwości obiektu do strumienia XML. Serializacji XML nie zawiera informacji o typie. Na przykład jeśli masz obiekt **książki** , który istnieje w przestrzeni nazw **biblioteki** , nie ma gwarancji, że jest on deserializowany do obiektu tego samego typu.

> [!NOTE]
> Serializacji XML nie konwertuje metody, indeksatory, prywatnych pola lub właściwości tylko do odczytu (z wyjątkiem kolekcji tylko do odczytu). Do serializacji obiektu wszystkie pola i właściwości, zarówno publiczne, jak i prywatnych, użyj <xref:System.Runtime.Serialization.DataContractSerializer> zamiast serializacji XML.

 Centralna Klasa w serializacji XML jest <xref:System.Xml.Serialization.XmlSerializer> klasą, a najważniejsze metody w tej klasie są metodami **serializacji** i **deserializacji** . <xref:System.Xml.Serialization.XmlSerializer> Tworzy PLiki C# i kompiluje je na PLiki z rozszerzeniem dll do wykonania tej serializacji. [Narzędzie XML Serializer Generator (Sgen.exe)](xml-serializer-generator-tool-sgen-exe.md) została zaprojektowana tak, aby generować te zestawy serializacji z wyprzedzeniem, aby można je było wdrożyć wraz z aplikacją i zwiększyć wydajność uruchamiania. Strumień XML wygenerowany przez element **XmlSerializer** jest zgodny z zaleceniami organizacja World Wide Web Consortium (W3C) [XML schematu definicji języka (XSD) 1,0](https://www.w3.org/TR/xslt). Ponadto typy danych wygenerowane są zgodne z dokumentem zatytułowanym "XML schematu część 2: Datatypes".

 Dane w obiektach są opisane przy użyciu konstrukcji języka programowania, takich jak klasy, pola, właściwości, typy pierwotne, tablice, a nawet osadzone XML w postaci obiektów **XmlElement** lub **XmlAttribute** . Istnieje możliwość tworzenia własnych klas oznaczona z atrybutów, lub za pomocą narzędzia definicji schematu XML można wygenerować klas na podstawie istniejącego schematu XML.

 Jeśli masz schematu XML, należy uruchomić narzędzie definicji schematu XML do tworzenia zestaw klasy, które są silnie wpisany schematu i dodawać adnotacje z atrybutami. W przypadku wystąpienia takich klasy jest serializowana, wygenerowany kod XML jest zgodna schematu XML. Zamieszczone w przypadku klasy, można programować względem model obiektów łatwo manipulować spełniającą pewność, że wygenerowany kod XML jest zgodny ze schematem XML. Jest to alternatywa dla użycia innych klas w programie .NET, takich jak klasy **XmlReader** i **XmlWriter** , do analizowania i pisania strumienia XML. Aby uzyskać więcej informacji, zobacz [dokumenty XML i dane](../data/xml/index.md). Klasy te umożliwiają przeanalizować strumieniem XML. W przeciwieństwie, użyj **XmlSerializer** , gdy strumień XML powinien być zgodny ze znanymi schematem XML.

 Atrybuty kontrolują strumień XML wygenerowany przez klasę **XmlSerializer** , co pozwala na ustawienie przestrzeni nazw XML, nazwy elementu, nazwy atrybutu i tak dalej w przypadku strumienia XML. Aby uzyskać więcej informacji o tych atrybutach i sposobach ich kontroli serializacji XML, zobacz [Kontrolowanie serializacji XML przy użyciu atrybutów](controlling-xml-serialization-using-attributes.md). Dla tabeli tych atrybutów, które są używane do kontrolowania wygenerowanego kodu XML, zobacz atrybuty kontrolujące [serializacji XML](attributes-that-control-xml-serialization.md).

 Klasa **XmlSerializer** może bardziej serializować obiekt i generować zakodowany strumień XML protokołu SOAP. Wygenerowany kod XML jest zgodny z sekcją 5 dokumentu organizacja World Wide Web Consortium zatytułowanego "Simple Object Access Protocol (SOAP) 1,1". Aby uzyskać więcej informacji o tym procesie, zobacz [How to: deserializacji obiektu jako SOAP-Encoded strumienia XML](how-to-serialize-an-object-as-a-soap-encoded-xml-stream.md). Aby zapoznać się z tabelą atrybutów kontrolujących wygenerowany kod XML, zobacz atrybuty kontrolujące [zakodowaną serializację protokołu SOAP](attributes-that-control-encoded-soap-serialization.md).

 Klasa **XmlSerializer** generuje komunikaty protokołu SOAP utworzone przez i przekazaną do usług sieci Web XML. Aby kontrolować komunikaty protokołu SOAP, można zastosować atrybuty do klas, zwracanych wartości, parametrów i pól znalezionych w pliku usługi sieci Web XML (. asmx). Można użyć atrybuty wymienione w "Serializacji XML atrybuty czy kontroli" i "Atrybuty czy kontroli kodowany protokołu SOAP serializacji", ponieważ usługi XML sieci Web mogą korzystać styl literału lub zakodowanego protokołu SOAP. Aby uzyskać więcej informacji o używaniu atrybutów do sterowania XML wygenerowanym przez usługę sieci Web XML, zobacz [serializacji XML z usługami sieci Web XML](xml-serialization-with-xml-web-services.md). Aby uzyskać więcej informacji na temat usług sieci Web SOAP i XML, zobacz [Dostosowywanie formatowania komunikatów SOAP](/previous-versions/dotnet/netframework-4.0/dkwy2d72(v=vs.100)).

## <a name="security-considerations-for-xmlserializer-applications"></a>Zagadnienia dotyczące zabezpieczeń aplikacji XmlSerializer

Podczas tworzenia aplikacji korzystającej z **elementu XmlSerializer** należy pamiętać o następujących elementach i ich następstwie:

- **XmlSerializer** tworzy pliki C# (. cs) i kompiluje je do plików DLL w katalogu o nazwie przez zmienną środowiskową temp; Serializacja występuje z tymi bibliotekami DLL.

  > [!NOTE]
  > Te zestawy serializacji można wygenerowane z góry i podpisane za pomocą narzędzia SGen.exe. Nie działa to na serwerze usług sieci Web. Innymi słowy jest tylko do użytku klienta i ręczne serializacji.

  Kod i biblioteki DLL są podatne na złośliwego procesu w czasie tworzenia i kompilacji. Podczas używania na komputerze z systemem Microsoft Windows NT 4.0 lub nowszy, może być możliwe dla co najmniej dwa użytkownikom udostępnianie katalogu TEMP. Udostępnianie katalogu TEMP jest niebezpieczne, jeśli dwa konta mają różne uprawnienia zabezpieczeń, a konto wyższego uprawnienia uruchamia aplikację przy użyciu **elementu XmlSerializer**. W takim przypadku jeden użytkownik może naruszyć bezpieczeństwo komputera, zastępując plik. cs lub. dll, który jest kompilowany. Aby usunąć ten problem, zawsze upewnij się, że każde konto na komputerze ma własny profil. Domyślnie zmienna środowiskowa TEMP wskazuje inny folder dla każdego konta.

- Jeśli złośliwy użytkownik wyśle ciągły strumień danych XML do serwera sieci Web (atak typu "odmowa usługi"), wówczas obiekt **XmlSerializer** kontynuuje przetwarzanie danych do momentu, gdy na komputerze nie będzie działać niska ilość zasobów.

  Ten rodzaj ataku jest eliminowany, jeśli używasz komputera z systemem Internet Information Services (IIS), a aplikacja jest uruchomiona w ramach usług IIS. Program IIS zawiera bramę, która nie może przetwarzać strumieni dłużej niż pewną liczbę (wartość domyślna to 4 KB). Jeśli tworzysz aplikację, która nie korzysta z usług IIS i deserializacji z **XmlSerializer**, należy zaimplementować podobną bramę, która uniemożliwia atak typu "odmowa usługi".

- **XmlSerializer** wykonuje serializacji danych i uruchamia dowolny kod przy użyciu dowolnego typu danego elementu.

  Istnieją dwie metody, w których obiekt złośliwego przedstawia zagrożenia. Może uruchomić złośliwy kod lub może wstrzyknąć złośliwy kod do pliku C# utworzonego przez **XmlSerializer**. W drugim przypadku istnieje teoretyczna możliwość, że złośliwy obiekt może w jakiś sposób wstrzyknąć kod do pliku C# utworzonego przez **XmlSerializer**. Mimo że ten problem zbadaniu dokładnie i takiego ataku jest uznawany za mało prawdopodobne, należy podjąć środki ostrożności nigdy nie szeregowania danych o typie nieznany i niezaufane.

- Zserializowany poufnych danych może być narażony.

  Gdy obiekt **XmlSerializer** ma serializowane dane, można go zapisać jako plik XML lub inny magazyn danych. Sklepu danych jest dostępna dla innych procesów, czy jest widoczny w intranecie lub w Internecie, dane mogą skradziony i użyty w sposób złośliwy. Jeśli na przykład utworzysz aplikację, która serializować zamówienia zawierające numery kart kredytowych, dane są bardzo poufne. Aby zapobiec, zawsze ochrony magazynu danych i wykonać kroki, aby utrzymać ją prywatnych.

## <a name="serialization-of-a-simple-class"></a>Serializacja klasy prostej

Poniższy przykład kodu pokazuje klasę podstawową z polem publicznym.

```vb
Public Class OrderForm
    Public OrderDate As DateTime
End Class
```

```csharp
public class OrderForm
{
    public DateTime OrderDate;
}
```

W przypadku wystąpienia tej klasy jest serializowana, jego może wyglądać w następujący sposób.

```xml
<OrderForm>
    <OrderDate>12/12/01</OrderDate>
</OrderForm>
```

Aby uzyskać więcej przykładów serializacji, zobacz [przykłady serializacji XML](examples-of-xml-serialization.md).

## <a name="items-that-can-be-serialized"></a>Elementy, które można wykonywać serializację

Następujące elementy można serializować przy użyciu klasy **XmlSerializer** :

- Właściwości publiczne odczytu/zapisu i pola publiczne klas.

- Klasy implementujące **interfejs ICollection** lub **IEnumerable**.

  > [!NOTE]
  > Tylko kolekcje są serializacji, nie publiczny właściwości.

- Obiekty **XmlElement** .

- Obiekty **XmlNode** .

- Obiekty **DataSet** .

 Aby uzyskać więcej informacji na temat serializacji lub deserializacji obiektów, zobacz [How to:](how-to-serialize-an-object.md) deserializacji obiektu i [instrukcje:](how-to-deserialize-an-object.md)deserializacja obiektu.

## <a name="advantages-of-using-xml-serialization"></a>Korzyści wynikające z używania serializacji XML

Klasa **XmlSerializer** zapewnia kompletną i elastyczną kontrolę podczas serializacji obiektu jako XML. W przypadku tworzenia usługi sieci Web XML można zastosować atrybuty kontrolujące serializację do klas i składowych, aby upewnić się, że dane wyjściowe XML są zgodne z określonym schematem.

Na przykład **XmlSerializer** umożliwia:

- Określ, czy pole lub właściwość powinien być kodowany jako atrybut lub element.

- Określ przestrzeni nazw XML do użycia.

- Określ nazwę elementu lub atrybutu, jeśli nazwa pola lub właściwości jest nieodpowiedni.

Inną zaletą serializacji XML jest to, że nie masz żadnych ograniczeń dotyczących tworzonych aplikacji, o ile strumień XML, który jest generowany jest zgodny z danym schematem. Wyobraź sobie schematu, używany do opisania książki. Zawiera funkcje tytuł, autor, Wydawca i ISBN numer elementu. Możesz opracować aplikację, która przetwarza dane XML w dowolny sposób, na przykład jako zamówienie książki lub spis książek. W obu przypadkach jedynym wymaganiem jest, czy strumień XML jest zgodny ze schematem określonego języka (XSD) definicji schematu XML.

## <a name="xml-serialization-considerations"></a>Uwagi dotyczące serializacji XML

Przy użyciu klasy **XmlSerializer** należy wziąć pod uwagę następujące kwestie:

- Narzędzie Sgen.exe wyraźnie jest przeznaczona do generowania zestawów serializacji w celu uzyskania optymalnej wydajności.

- Serializowane dane zawiera tylko danych i struktury klas. Informacje o tożsamości i zestawu typu nie są uwzględniane.

- Może być Zserializowany tylko właściwości publiczne i pola. Właściwości muszą mieć publiczne metody dostępu (Pobieranie i ustawianie metody). Jeśli muszą serializację danych bez publicznego, użyj <xref:System.Runtime.Serialization.DataContractSerializer> klasy zamiast serializacji XML.

- Klasa musi mieć konstruktora bez parametrów, aby można było serializować ją przy użyciu **elementu XmlSerializer**.

- Nie można serializować metody.

- **XmlSerializer** może przetwarzać klasy implementujące **interfejsy IEnumerable** lub **ICollection** inaczej, jeśli spełniają określone wymagania, w następujący sposób.

  Klasa implementująca **interfejs IEnumerable** musi implementować publiczną metodę **Add** , która przyjmuje jeden parametr. Parametr **Add** Method musi być spójny (polimorficzny) z typem zwracanym z właściwości **IEnumerator. Current** zwracanego z metody **GetEnumerator** .

  Klasa implementująca **interfejs ICollection** oprócz **interfejsu IEnumerable** (na przykład **CollectionBase**) musi mieć Właściwość indeksowaną **elementu** publicznego (indeksator w języku C#), która przyjmuje liczbę całkowitą i musi mieć publiczną właściwość **Count** typu **Integer**. Parametr przesłany do metody **Add** musi być tym samym typem, który został zwrócony z właściwości **Item** lub jednej z baz danych tego typu.

  W przypadku klas implementujących **interfejs ICollection** wartości, które mają być serializowane, są pobierane z właściwości **element** indeksowany, a nie przez wywołanie metody **GetEnumerator**. Ponadto pola publiczne i właściwości nie są serializowane, z wyjątkiem pól publicznych, które zwracają inną klasę kolekcji (jedną implementującą **interfejs ICollection**). Aby zapoznać się z przykładem, zobacz [przykłady serializacji XML](examples-of-xml-serialization.md).

## <a name="xsd-data-type-mapping"></a>Mapowania typów danych XSD

Dokument W3C o tytule [schematu XML część 2:](https://www.w3.org/TR/xmlschema-2/) typy danych określa, że w schemacie języka definicji schematu XML (XSD) można używać prostych, które są dozwolone. Dla wielu z nich (na przykład **int** i **Decimal**) istnieje odpowiedni typ danych w programie .NET. Jednak niektóre typy danych XML nie mają odpowiadającego im typu danych .NET, na przykład typ danych **NMTOKEN** . W takich przypadkach, jeśli używasz narzędzia definicji schematu XML ([narzędzie definicji schematu XML (Xsd.exe)](xml-schema-definition-tool-xsd-exe.md)) do generowania klas ze schematu, odpowiedni atrybut jest stosowany do składowej typu String, a jej właściwość **DataType** jest ustawiona na nazwę typu danych XML. Na przykład, jeśli schemat zawiera element o nazwie "mój token" z obiektem typu danych XML, wygenerowana Klasa może zawierać element **członkowski, jak** pokazano w poniższym przykładzie.

```vb
<XmlElement(DataType:="NMTOKEN")> _
Public MyToken As String
```

```csharp
[XmlElement(DataType = "NMTOKEN")]
public string MyToken;
```

Podobnie, jeśli tworzysz klasę, która musi być zgodna z określonym schematem XML (XSD), należy zastosować odpowiedni atrybut i ustawić jego właściwość **DataType** na żądaną nazwę typu danych XML.

Aby uzyskać pełną listę mapowań typów, zobacz Właściwość **DataType** dla którejkolwiek z następujących klas atrybutów:

- <xref:System.Xml.Serialization.SoapAttributeAttribute>

- <xref:System.Xml.Serialization.SoapElementAttribute>

- <xref:System.Xml.Serialization.XmlArrayItemAttribute>

- <xref:System.Xml.Serialization.XmlAttributeAttribute>

- <xref:System.Xml.Serialization.XmlElementAttribute>

- <xref:System.Xml.Serialization.XmlRootAttribute>

## <a name="see-also"></a>Zobacz też

- <xref:System.Xml.Serialization.XmlSerializer>
- <xref:System.Runtime.Serialization.DataContractSerializer>
- <xref:System.IO.FileStream>
- [Serializacja XML i SOAP](xml-and-soap-serialization.md)
- [Serializacja binarna](binary-serialization.md)
- [Serializacja](index.md)
- <xref:System.Xml.Serialization.XmlSerializer>
- [Przykłady serializacji XML](examples-of-xml-serialization.md)
- [Instrukcje: Serializacja obiektu](how-to-serialize-an-object.md)
- [Instrukcje: Deserializacja obiektu](how-to-deserialize-an-object.md)
