---
title: Jak napisać Serializatory niestandardowe i deserializacji za pomocą System.Text.Json
description: Dowiedz się, jak napisać niestandardowe serializatory i deserializatory dla formatu JSON przy użyciu System.Text.Json przestrzeni nazw.
ms.date: 11/30/2020
no-loc:
- System.Text.Json
- Newtonsoft.Json
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
ms.openlocfilehash: a01d3c8dd18c114ea1c3aabc402bc841a6025ffe
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96440025"
---
# <a name="how-to-write-custom-serializers-and-deserializers-with-no-locsystemtextjson"></a>Jak napisać Serializatory niestandardowe i deserializacji za pomocą System.Text.Json

<xref:System.Text.Json.Utf8JsonReader?displayProperty=fullName> jest wysoką wydajnością, niskim alokacją, czytnikiem tylko do przodu dla tekstu JSON zakodowanego w formacie UTF-8, Odczytaj z `ReadOnlySpan<byte>` lub `ReadOnlySequence<byte>` . `Utf8JsonReader`Jest typem niskiego poziomu, który może służyć do tworzenia niestandardowych analizatorów i deserializacji. <xref:System.Text.Json.JsonSerializer.Deserialize%2A?displayProperty=nameWithType>Metoda używa `Utf8JsonReader` w obszarze okładki.

<xref:System.Text.Json.Utf8JsonWriter?displayProperty=fullName> jest wysoce wydajnym sposobem pisania zakodowanego tekstu JSON w formacie UTF-8 ze wspólnych typów platformy .NET, takich jak `String` , `Int32` , i `DateTime` . Składnik zapisywania jest typu niskiego poziomu, który może służyć do tworzenia serializatorów niestandardowych. <xref:System.Text.Json.JsonSerializer.Serialize%2A?displayProperty=nameWithType>Metoda używa `Utf8JsonWriter` w obszarze okładki.

<xref:System.Text.Json.JsonDocument?displayProperty=fullName> zapewnia możliwość tworzenia Document Object Model tylko do odczytu (DOM) za pomocą programu `Utf8JsonReader` . DOM zapewnia losowy dostęp do danych w ładunku JSON. Do elementów JSON, które tworzą ładunek, można uzyskać dostęp za pośrednictwem <xref:System.Text.Json.JsonElement> typu. `JsonElement`Typ udostępnia moduł wyliczający tablic i obiektów oraz interfejsy API służące do konwertowania tekstu JSON na popularne typy .NET. `JsonDocument` uwidacznia <xref:System.Text.Json.JsonDocument.RootElement> Właściwość.

W poniższych sekcjach pokazano, jak używać tych narzędzi do odczytywania i pisania danych JSON.

## <a name="use-jsondocument-for-access-to-data"></a>Korzystanie z JsonDocument do uzyskiwania dostępu do danych

Poniższy przykład pokazuje, jak używać <xref:System.Text.Json.JsonDocument> klasy do losowego dostępu do danych w ciągu JSON:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/JsonDocumentDataAccess.cs" id="AverageGrades1":::

Powyższy kod ma następujące działanie:

* Przyjęto, że kod JSON do analizy jest w ciągu o nazwie `jsonString` .
* Oblicza średnią ocenę dla obiektów w `Students` tablicy, która ma `Grade` Właściwość.
* Przypisuje domyślną ocenę 70 dla studentów, którzy nie posiadają klasy.
* Zlicza uczniów przez zwiększenie `count` zmiennej przy każdej iteracji. Alternatywą jest wywołanie <xref:System.Text.Json.JsonElement.GetArrayLength%2A> , jak pokazano w następującym przykładzie:

  :::code language="csharp" source="snippets/system-text-json-how-to/csharp/JsonDocumentDataAccess.cs" id="AverageGrades2":::

Oto przykład pliku JSON, który jest przetwarzany przez ten kod:

:::code language="json" source="snippets/system-text-json-how-to/csharp/GradesPrettyPrint.json":::

## <a name="use-jsondocument-to-write-json"></a>Użyj JsonDocument, aby zapisać kod JSON

Poniższy przykład pokazuje, jak napisać kod JSON z <xref:System.Text.Json.JsonDocument> :

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/JsonDocumentWriteJson.cs" id="Serialize":::

Powyższy kod ma następujące działanie:

* Odczytuje plik JSON, ładuje dane do `JsonDocument` i zapisuje sformatowany plik JSON w formacie.
* Używa <xref:System.Text.Json.JsonDocumentOptions> do określenia, czy komentarze w wejściowym formacie JSON są dozwolone, ale ignorowane.
* Po zakończeniu wywołania <xref:System.Text.Json.Utf8JsonWriter.Flush%2A> na składniku zapisywania. Alternatywą jest umożliwienie autoopróżniania składnika zapisywania, gdy zostanie on usunięty.

Oto przykład danych wejściowych JSON do przetworzenia przez przykładowy kod:

:::code language="json" source="snippets/system-text-json-how-to/csharp/Grades.json":::

Wynikiem są następujące niedrukowane dane wyjściowe JSON:

:::code language="json" source="snippets/system-text-json-how-to/csharp/GradesPrettyPrint.json":::

## <a name="use-utf8jsonwriter"></a>Użyj Utf8JsonWriter

Poniższy przykład pokazuje, jak używać <xref:System.Text.Json.Utf8JsonWriter> klasy:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/Utf8WriterToStream.cs" id="Serialize":::

## <a name="use-utf8jsonreader"></a>Użyj Utf8JsonReader

Poniższy przykład pokazuje, jak używać <xref:System.Text.Json.Utf8JsonReader> klasy:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/Utf8ReaderFromBytes.cs" id="Deserialize":::

Poprzedni kod założono, że `jsonUtf8` zmienna jest tablicą bajtową, która zawiera prawidłowy kod JSON zakodowany jako UTF-8.

### <a name="filter-data-using-utf8jsonreader"></a>Filtrowanie danych za pomocą Utf8JsonReader

Poniższy przykład pokazuje, jak synchronicznie odczytać plik i wyszukać wartość.

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/Utf8ReaderFromFile.cs":::

Aby zapoznać się z wersją asynchroniczną tego przykładu, zobacz [projekt Samples w formacie JSON programu .NET](https://github.com/dotnet/samples/blob/18e31a5f1abd4f347bf96bfdc3e40e2cfb36e319/core/json/Program.cs).

Powyższy kod ma następujące działanie:

* Przyjęto, że kod JSON zawiera tablicę obiektów, a każdy obiekt może zawierać właściwość "name" typu String.
* Zlicza obiekty i wartości właściwości "name", które kończą się znakiem "University".
* Przyjęto założenie, że plik jest zakodowany jako UTF-16 i transkoduje go do UTF-8. Plik zakodowany jako UTF-8 może być odczytywany bezpośrednio do programu `ReadOnlySpan<byte>` , przy użyciu następującego kodu:

  ```csharp
  ReadOnlySpan<byte> jsonReadOnlySpan = File.ReadAllBytes(fileName);
  ```

  Jeśli plik zawiera znacznik kolejności bajtów UTF-8, usuń go przed przekazaniem bajtów do `Utf8JsonReader` , ponieważ czytnik oczekuje tekstu. W przeciwnym razie BOM jest traktowany jako nieprawidłowy kod JSON, a czytelnik zgłasza wyjątek.

Oto przykład JSON, który może odczytać poprzedzający kod. Otrzymany komunikat podsumowujący to "2 z 4 mają nazwy kończące się na" University ":

:::code language="json" source="snippets/system-text-json-how-to/csharp/Universities.json":::

### <a name="read-from-a-stream-using-utf8jsonreader"></a>Odczytaj ze strumienia przy użyciu Utf8JsonReader

W przypadku odczytywania dużego pliku (na przykład gigabajta lub więcej) można uniknąć konieczności załadowania całego pliku do pamięci jednocześnie. W tym scenariuszu można użyć <xref:System.IO.FileStream> .

W przypadku `Utf8JsonReader` odczytywania ze strumienia przy użyciu programu, obowiązują następujące reguły:

* Bufor zawierający częściowy ładunek JSON musi być co najmniej tak duży jak największy token JSON w nim, tak aby czytelnik mógł postępować dalej.
* Bufor musi być co najmniej tak duże, jak największą sekwencję białych znaków w formacie JSON.
* Czytnik nie śledzi danych, które zostały odczytane, dopóki nie zostaną całkowicie odczytane dalej <xref:System.Text.Json.Utf8JsonReader.TokenType%2A> w ładunku JSON. Tak więc, gdy bajty są pozostawione w buforze, należy ponownie przekazać je do czytnika. Możesz użyć, <xref:System.Text.Json.Utf8JsonReader.BytesConsumed%2A> Aby określić, ile bajtów pozostało.

Poniższy kod ilustruje sposób odczytywania ze strumienia. Przykład pokazuje <xref:System.IO.MemoryStream> . Podobny kod będzie działał z <xref:System.IO.FileStream> , z wyjątkiem sytuacji, gdy `FileStream` zawiera BOM w formacie UTF-8. W takim przypadku należy rozdzielić te trzy bajty z buforu przed przekazaniem pozostałych bajtów do `Utf8JsonReader` . W przeciwnym razie czytelnik zgłosi wyjątek, ponieważ BOM nie jest traktowany jako prawidłowa część JSON.

Przykładowy kod rozpoczyna się od buforu 4 KB i podwaja rozmiar buforu za każdym razem, gdy okaże się, że rozmiar nie jest wystarczająco duży, aby dopasować pełny token JSON, który jest wymagany, aby czytnik mógł postępować w ładunku JSON. Przykład JSON podany w fragmencie kodu wyzwala zwiększenie rozmiaru buforu tylko wtedy, gdy ustawisz bardzo mały początkowy rozmiar buforu, na przykład 10 bajtów. Jeśli ustawisz początkowy rozmiar buforu na 10, `Console.WriteLine` instrukcje ilustrują przyczynę i wpływ rozmiaru buforu. W początkowym rozmiarze bufora 4 KB cały przykładowy kod JSON jest pokazywany przez każdy z nich `Console.WriteLine` , a rozmiar buforu nigdy nie musi zostać zwiększony.

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/Utf8ReaderPartialRead.cs":::

W powyższym przykładzie nie ustawiono limitu rozmiaru buforu. Jeśli rozmiar tokenu jest zbyt duży, kod może zakończyć się niepowodzeniem z <xref:System.OutOfMemoryException> wyjątkiem. Taka sytuacja może wystąpić, jeśli kod JSON zawiera token o rozmiarze około 1 GB lub więcej, ponieważ Podwajanie rozmiaru 1 GB spowoduje, że rozmiar jest zbyt duży, aby zmieścił się w `int32` buforze.

## <a name="see-also"></a>Zobacz też

* [System.Text.Json Podsumowanie](system-text-json-overview.md)
* [Jak dostosować kodowanie znaków](system-text-json-character-encoding.md)
* [Jak napisać konwertery niestandardowe na potrzeby serializacji JSON](system-text-json-converters-how-to.md)
* [System.Text.Json Dokumentacja interfejsu API](xref:System.Text.Json)
