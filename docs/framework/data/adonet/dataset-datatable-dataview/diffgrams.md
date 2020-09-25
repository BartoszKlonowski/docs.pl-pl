---
title: Elementy DiffGram
ms.date: 03/30/2017
ms.assetid: 037f3991-7bbc-424b-b52e-8b03585d3e34
ms.openlocfilehash: aff9c2347fab51d853e19bd9dc16666c4ed549b5
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91172804"
---
# <a name="diffgrams"></a>Elementy DiffGram

Plik DiffGram jest formatem XML, który identyfikuje bieżące i oryginalne wersje elementów danych. <xref:System.Data.DataSet>Używa formatu DiffGram do ładowania i utrwalania jego zawartości oraz do serializacji jego zawartości do transportu przez połączenie sieciowe. Gdy <xref:System.Data.DataSet> jest zapisywana w formacie DiffGram, wypełnia ona plik DiffGram ze wszystkimi informacjami niezbędnymi, aby dokładnie odtworzyć zawartość, ale nie schemat programu, w <xref:System.Data.DataSet> tym wartości kolumn z zarówno **oryginalnej** , jak i **bieżącej** wersji wiersza, informacji o błędzie wiersza i kolejności wierszy.  
  
 W przypadku wysyłania i pobierania <xref:System.Data.DataSet> z usługi sieci Web XML, format DiffGram jest niejawnie używany. Ponadto podczas ładowania zawartości <xref:System.Data.DataSet> z pliku XML przy użyciu metody **ReadXml** lub podczas zapisywania zawartości <xref:System.Data.DataSet> w formacie XML przy użyciu metody **WriteXml** można określić, że zawartość ma być odczytywana lub zapisywana jako plik DiffGram. Aby uzyskać więcej informacji, zobacz [Ładowanie zestawu danych z XML](loading-a-dataset-from-xml.md) i [zapisywanie zawartości zestawu danych jako danych XML](writing-dataset-contents-as-xml-data.md).  
  
 Chociaż format DiffGram jest używany głównie przez .NET Framework jako format serializacji zawartości <xref:System.Data.DataSet> , można również użyć DiffGrams do modyfikacji danych w tabelach w bazie danych Microsoft SQL Server.  
  
 Element DiffGram jest generowany przez zapisanie zawartości wszystkich tabel do **\<diffgram>** elementu.  
  
### <a name="to-generate-a-diffgram"></a>Aby wygenerować w formacie DiffGram  
  
1. Wygeneruj listę tabel głównych (czyli tabel bez żadnych elementów nadrzędnych).  
  
2. Dla każdej tabeli i jej elementów podrzędnych na liście Zapisz bieżącą wersję wszystkich wierszy w pierwszej sekcji DiffGram.  
  
3. W przypadku każdej tabeli w programie <xref:System.Data.DataSet> należy zapisać oryginalną wersję wszystkich wierszy, jeśli istnieje, w sekcji w formacie **\<before>** DiffGram.  
  
4. W przypadku wierszy, które mają Błędy, Zapisz zawartość błędu w **\<errors>** sekcji w formacie DiffGram.  
  
 Element DiffGram jest przetwarzany w kolejności od początku pliku XML do końca.  
  
### <a name="to-process-a-diffgram"></a>Aby przetworzyć w formacie DiffGram  
  
1. Przetwórz pierwszą sekcję w formacie DiffGram, która zawiera bieżącą wersję wierszy.  
  
2. Przetwórz drugą lub **\<before>** sekcję zawierającą oryginalną wersję wiersza zmodyfikowanych i usuniętych wierszy.  
  
    > [!NOTE]
    > Jeśli wiersz został oznaczony jako usunięty, operacja usuwania może również usunąć elementy podrzędne wiersza, w zależności od `Cascade` właściwości bieżącej <xref:System.Data.DataSet> .  
  
3. Przetwórz **\<errors>** sekcję. Ustaw informacje o błędzie dla określonego wiersza i kolumny dla każdego elementu w tej sekcji.  
  
> [!NOTE]
> Jeśli ustawisz wartość w formacie <xref:System.Data.XmlWriteMode> DiffGram, zawartość elementu docelowego <xref:System.Data.DataSet> i oryginalnego <xref:System.Data.DataSet> może się różnić.  
  
## <a name="diffgram-format"></a>Format DiffGram  

 Format DiffGram jest podzielony na trzy sekcje: bieżące dane, oryginalne (lub "przed") dane i sekcję błędów, jak pokazano w poniższym przykładzie.  
  
```xml  
<?xml version="1.0"?>  
<diffgr:diffgram
         xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"  
         xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1"  
         xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
  
   <DataInstance>  
   </DataInstance>  
  
  <diffgr:before>  
  </diffgr:before>  
  
  <diffgr:errors>  
  </diffgr:errors>  
</diffgr:diffgram>  
```  
  
 Format DiffGram składa się z następujących bloków danych:  
  
 **\<**  ***DataInstance***  **>**  
 Nazwa tego elementu ( ***DataInstance***) służy do wyjaśnienia w tej dokumentacji. Element ***DataInstance*** reprezentuje <xref:System.Data.DataSet> lub wiersz a <xref:System.Data.DataTable> . Zamiast *DataInstance*, element będzie zawierać nazwę <xref:System.Data.DataSet> lub <xref:System.Data.DataTable> . Ten blok formatu DiffGram zawiera bieżące dane, bez względu na to, czy został on zmodyfikowany, czy nie. Element lub wiersz, który został zmodyfikowany, jest identyfikowany za pomocą adnotacji **diffgr: hasChanges** .  
  
 **\<diffgr:before>**  
 Ten blok formatu DiffGram zawiera oryginalną wersję wiersza. Elementy w tym bloku są dopasowywane do elementów w bloku ***DataInstance*** przy użyciu adnotacji **diffgr: ID** .  
  
 **\<diffgr:errors>**  
 Ten blok formatu DiffGram zawiera informacje o błędach dla określonego wiersza w bloku ***DataInstance*** . Elementy w tym bloku są dopasowywane do elementów w bloku ***DataInstance*** przy użyciu adnotacji **diffgr: ID** .  
  
## <a name="diffgram-annotations"></a>Adnotacje w formacie DiffGram  

 DiffGrams użyć kilku adnotacji do powiązania elementów z różnych bloków DiffGram, które reprezentują różne wersje wierszy lub informacje o błędach w <xref:System.Data.DataSet> .  
  
 W poniższej tabeli opisano adnotacje w formacie DiffGram, które są zdefiniowane w przestrzeni nazw DiffGram **Nazwa urn: schematy-Microsoft-com: XML-DiffGram-V1**.  
  
|Adnotacja|Opis|  
|----------------|-----------------|  
|**id**|Służy do parowania elementów w blokach **\<diffgr:before>** i **\<diffgr:errors>** do elementów w **\<** ***DataInstance*** **>** bloku. Wartości z adnotacją **diffgr: ID** są w postaci *[TableName] [RowIdentifier]*. Na przykład: `<Customers diffgr:id="Customers1">`.|  
|**parentId**|Określa, który element z **\<** ***DataInstance*** **>** bloku jest elementem nadrzędnym bieżącego elementu. Wartości z adnotacją **diffgr: parentID** znajdują się w postaci *[TableName] [RowIdentifier]*. Na przykład: `<Orders diffgr:parentId="Customers1">`.|  
|**hasChanges**|Identyfikuje wiersz w **\<** ***DataInstance*** **>** bloku jako zmodyfikowany. Adnotacja **HasChanges** może mieć jedną z następujących dwóch wartości:<br /><br /> **wstawiany**<br /> Identyfikuje **dodany** wiersz.<br /><br /> **zmodyfikowano**<br /> Identyfikuje **zmodyfikowany** wiersz, który zawiera **oryginalną** wersję wiersza w **\<diffgr:before>** bloku. Należy zauważyć, że **usunięte** wiersze będą mieć **oryginalną** wersję wiersza w **\<diffgr:before>** bloku, ale w bloku nie będzie żadnych elementów z adnotacjami **\<** ***DataInstance*** **>** .|  
|**hasErrors**|Identyfikuje wiersz w **\<** ***DataInstance*** **>** bloku z **RowError**. Element Error jest umieszczany w **\<diffgr:errors>** bloku.|  
|**Błąd**|Zawiera tekst **RowError** dla określonego elementu w **\<diffgr:errors>** bloku.|  
  
 <xref:System.Data.DataSet>Zawiera dodatkowe adnotacje podczas odczytywania lub zapisywania zawartości w formacie DiffGram. W poniższej tabeli opisano te dodatkowe adnotacje, które są zdefiniowane w przestrzeni nazw **urn: schematy-Microsoft-com: XML-msdata**.  
  
|Adnotacja|Opis|  
|----------------|-----------------|  
|**RowOrder**|Zachowuje kolejność wierszy oryginalnych danych i identyfikuje indeks wiersza w określonym <xref:System.Data.DataTable> .|  
|**Ukryte**|Identyfikuje kolumnę jako posiadającą Właściwość **ColumnMapping** ustawioną na wartość **MappingType. Hidden**. Atrybut jest zapisywana w formacie **msdata: Hidden** *[ColumnName]*= "*Value*". Na przykład: `<Customers diffgr:id="Customers1" msdata:hiddenContactTitle="Owner">`.<br /><br /> Należy zauważyć, że ukryte kolumny są zapisywane tylko jako atrybut DiffGram, jeśli zawierają dane. W przeciwnym razie są one ignorowane.|  
  
## <a name="sample-diffgram"></a>Przykładowy format DiffGram  

 Poniżej przedstawiono przykładowy format DiffGram. Ten przykład pokazuje wynik aktualizacji wiersza w tabeli przed zatwierdzeniem zmian. Wiersz z identyfikatorem IDKlienta "ALFKI" został zmodyfikowany, ale nie został zaktualizowany. W efekcie istnieje **bieżący** wiersz z **diffgr: identyfikatorem** "Customers1" w **\<** ***DataInstance*** **>** bloku i **oryginalny** wiersz z **diffgr: ID** elementu "Customers1" w **\<diffgr:before>** bloku. Wiersz z identyfikatorem CustomerID "ANATR" zawiera element **RowError**, więc ma on adnotację z `diffgr:hasErrors="true"` i zawiera powiązany element w **\<diffgr:errors>** bloku.  
  
```xml  
<diffgr:diffgram xmlns:msdata="urn:schemas-microsoft-com:xml-msdata" xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
  <CustomerDataSet>  
    <Customers diffgr:id="Customers1" msdata:rowOrder="0" diffgr:hasChanges="modified">  
      <CustomerID>ALFKI</CustomerID>  
      <CompanyName>New Company</CompanyName>  
    </Customers>  
    <Customers diffgr:id="Customers2" msdata:rowOrder="1" diffgram:hasErrors="true">  
      <CustomerID>ANATR</CustomerID>  
      <CompanyName>Ana Trujillo Emparedados y Helados</CompanyName>  
    </Customers>  
    <Customers diffgr:id="Customers3" msdata:rowOrder="2">  
      <CustomerID>ANTON</CustomerID>  
      <CompanyName>Antonio Moreno Taquera</CompanyName>  
    </Customers>  
    <Customers diffgr:id="Customers4" msdata:rowOrder="3">  
      <CustomerID>AROUT</CustomerID>  
      <CompanyName>Around the Horn</CompanyName>  
    </Customers>  
  </CustomerDataSet>  
  <diffgr:before>  
    <Customers diffgr:id="Customers1" msdata:rowOrder="0">  
      <CustomerID>ALFKI</CustomerID>  
      <CompanyName>Alfreds Futterkiste</CompanyName>  
    </Customers>  
  </diffgr:before>  
  <diffgr:errors>  
    <Customers diffgr:id="Customers2" diffgr:Error="An optimistic concurrency violation has occurred for this row."/>  
  </diffgr:errors>  
</diffgr:diffgram>  
```  
  
## <a name="see-also"></a>Zobacz też

- [Używanie języka XML w elemencie DataSet](using-xml-in-a-dataset.md)
- [Ładowanie elementu DataSet z pliku XML](loading-a-dataset-from-xml.md)
- [Zapisywanie zawartości elementu DataSet jako danych XML](writing-dataset-contents-as-xml-data.md)
- [Elementy DataSet, DataTable i DataView](index.md)
- [Omówienie ADO.NET](../ado-net-overview.md)
