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
# <a name="how-to-write-custom-serializers-and-deserializers-with-no-locsystemtextjson"></a><span data-ttu-id="60eb7-103">Jak napisać Serializatory niestandardowe i deserializacji za pomocą System.Text.Json</span><span class="sxs-lookup"><span data-stu-id="60eb7-103">How to write custom serializers and deserializers with System.Text.Json</span></span>

<span data-ttu-id="60eb7-104"><xref:System.Text.Json.Utf8JsonReader?displayProperty=fullName> jest wysoką wydajnością, niskim alokacją, czytnikiem tylko do przodu dla tekstu JSON zakodowanego w formacie UTF-8, Odczytaj z `ReadOnlySpan<byte>` lub `ReadOnlySequence<byte>` .</span><span class="sxs-lookup"><span data-stu-id="60eb7-104"><xref:System.Text.Json.Utf8JsonReader?displayProperty=fullName> is a high-performance, low allocation, forward-only reader for UTF-8 encoded JSON text, read from a `ReadOnlySpan<byte>` or `ReadOnlySequence<byte>`.</span></span> <span data-ttu-id="60eb7-105">`Utf8JsonReader`Jest typem niskiego poziomu, który może służyć do tworzenia niestandardowych analizatorów i deserializacji.</span><span class="sxs-lookup"><span data-stu-id="60eb7-105">The `Utf8JsonReader` is a low-level type that can be used to build custom parsers and deserializers.</span></span> <span data-ttu-id="60eb7-106"><xref:System.Text.Json.JsonSerializer.Deserialize%2A?displayProperty=nameWithType>Metoda używa `Utf8JsonReader` w obszarze okładki.</span><span class="sxs-lookup"><span data-stu-id="60eb7-106">The <xref:System.Text.Json.JsonSerializer.Deserialize%2A?displayProperty=nameWithType> method uses `Utf8JsonReader` under the covers.</span></span>

<span data-ttu-id="60eb7-107"><xref:System.Text.Json.Utf8JsonWriter?displayProperty=fullName> jest wysoce wydajnym sposobem pisania zakodowanego tekstu JSON w formacie UTF-8 ze wspólnych typów platformy .NET, takich jak `String` , `Int32` , i `DateTime` .</span><span class="sxs-lookup"><span data-stu-id="60eb7-107"><xref:System.Text.Json.Utf8JsonWriter?displayProperty=fullName> is a high-performance way to write UTF-8 encoded JSON text from common .NET types like `String`, `Int32`, and `DateTime`.</span></span> <span data-ttu-id="60eb7-108">Składnik zapisywania jest typu niskiego poziomu, który może służyć do tworzenia serializatorów niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="60eb7-108">The writer is a low-level type that can be used to build custom serializers.</span></span> <span data-ttu-id="60eb7-109"><xref:System.Text.Json.JsonSerializer.Serialize%2A?displayProperty=nameWithType>Metoda używa `Utf8JsonWriter` w obszarze okładki.</span><span class="sxs-lookup"><span data-stu-id="60eb7-109">The <xref:System.Text.Json.JsonSerializer.Serialize%2A?displayProperty=nameWithType> method uses `Utf8JsonWriter` under the covers.</span></span>

<span data-ttu-id="60eb7-110"><xref:System.Text.Json.JsonDocument?displayProperty=fullName> zapewnia możliwość tworzenia Document Object Model tylko do odczytu (DOM) za pomocą programu `Utf8JsonReader` .</span><span class="sxs-lookup"><span data-stu-id="60eb7-110"><xref:System.Text.Json.JsonDocument?displayProperty=fullName> provides the ability to build a read-only Document Object Model (DOM) by using `Utf8JsonReader`.</span></span> <span data-ttu-id="60eb7-111">DOM zapewnia losowy dostęp do danych w ładunku JSON.</span><span class="sxs-lookup"><span data-stu-id="60eb7-111">The DOM provides random access to data in a JSON payload.</span></span> <span data-ttu-id="60eb7-112">Do elementów JSON, które tworzą ładunek, można uzyskać dostęp za pośrednictwem <xref:System.Text.Json.JsonElement> typu.</span><span class="sxs-lookup"><span data-stu-id="60eb7-112">The JSON elements that compose the payload can be accessed via the <xref:System.Text.Json.JsonElement> type.</span></span> <span data-ttu-id="60eb7-113">`JsonElement`Typ udostępnia moduł wyliczający tablic i obiektów oraz interfejsy API służące do konwertowania tekstu JSON na popularne typy .NET.</span><span class="sxs-lookup"><span data-stu-id="60eb7-113">The `JsonElement` type provides array and object enumerators along with APIs to convert JSON text to common .NET types.</span></span> <span data-ttu-id="60eb7-114">`JsonDocument` uwidacznia <xref:System.Text.Json.JsonDocument.RootElement> Właściwość.</span><span class="sxs-lookup"><span data-stu-id="60eb7-114">`JsonDocument` exposes a <xref:System.Text.Json.JsonDocument.RootElement> property.</span></span>

<span data-ttu-id="60eb7-115">W poniższych sekcjach pokazano, jak używać tych narzędzi do odczytywania i pisania danych JSON.</span><span class="sxs-lookup"><span data-stu-id="60eb7-115">The following sections show how to use these tools for reading and writing JSON.</span></span>

## <a name="use-jsondocument-for-access-to-data"></a><span data-ttu-id="60eb7-116">Korzystanie z JsonDocument do uzyskiwania dostępu do danych</span><span class="sxs-lookup"><span data-stu-id="60eb7-116">Use JsonDocument for access to data</span></span>

<span data-ttu-id="60eb7-117">Poniższy przykład pokazuje, jak używać <xref:System.Text.Json.JsonDocument> klasy do losowego dostępu do danych w ciągu JSON:</span><span class="sxs-lookup"><span data-stu-id="60eb7-117">The following example shows how to use the <xref:System.Text.Json.JsonDocument> class for random access to data in a JSON string:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/JsonDocumentDataAccess.cs" id="AverageGrades1":::

<span data-ttu-id="60eb7-118">Powyższy kod ma następujące działanie:</span><span class="sxs-lookup"><span data-stu-id="60eb7-118">The preceding code:</span></span>

* <span data-ttu-id="60eb7-119">Przyjęto, że kod JSON do analizy jest w ciągu o nazwie `jsonString` .</span><span class="sxs-lookup"><span data-stu-id="60eb7-119">Assumes the JSON to analyze is in a string named `jsonString`.</span></span>
* <span data-ttu-id="60eb7-120">Oblicza średnią ocenę dla obiektów w `Students` tablicy, która ma `Grade` Właściwość.</span><span class="sxs-lookup"><span data-stu-id="60eb7-120">Calculates an average grade for objects in a `Students` array that have a `Grade` property.</span></span>
* <span data-ttu-id="60eb7-121">Przypisuje domyślną ocenę 70 dla studentów, którzy nie posiadają klasy.</span><span class="sxs-lookup"><span data-stu-id="60eb7-121">Assigns a default grade of 70 for students who don't have a grade.</span></span>
* <span data-ttu-id="60eb7-122">Zlicza uczniów przez zwiększenie `count` zmiennej przy każdej iteracji.</span><span class="sxs-lookup"><span data-stu-id="60eb7-122">Counts students by incrementing a `count` variable with each iteration.</span></span> <span data-ttu-id="60eb7-123">Alternatywą jest wywołanie <xref:System.Text.Json.JsonElement.GetArrayLength%2A> , jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="60eb7-123">An alternative is to call <xref:System.Text.Json.JsonElement.GetArrayLength%2A>, as shown in the following example:</span></span>

  :::code language="csharp" source="snippets/system-text-json-how-to/csharp/JsonDocumentDataAccess.cs" id="AverageGrades2":::

<span data-ttu-id="60eb7-124">Oto przykład pliku JSON, który jest przetwarzany przez ten kod:</span><span class="sxs-lookup"><span data-stu-id="60eb7-124">Here's an example of the JSON that this code processes:</span></span>

:::code language="json" source="snippets/system-text-json-how-to/csharp/GradesPrettyPrint.json":::

## <a name="use-jsondocument-to-write-json"></a><span data-ttu-id="60eb7-125">Użyj JsonDocument, aby zapisać kod JSON</span><span class="sxs-lookup"><span data-stu-id="60eb7-125">Use JsonDocument to write JSON</span></span>

<span data-ttu-id="60eb7-126">Poniższy przykład pokazuje, jak napisać kod JSON z <xref:System.Text.Json.JsonDocument> :</span><span class="sxs-lookup"><span data-stu-id="60eb7-126">The following example shows how to write JSON from a <xref:System.Text.Json.JsonDocument>:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/JsonDocumentWriteJson.cs" id="Serialize":::

<span data-ttu-id="60eb7-127">Powyższy kod ma następujące działanie:</span><span class="sxs-lookup"><span data-stu-id="60eb7-127">The preceding code:</span></span>

* <span data-ttu-id="60eb7-128">Odczytuje plik JSON, ładuje dane do `JsonDocument` i zapisuje sformatowany plik JSON w formacie.</span><span class="sxs-lookup"><span data-stu-id="60eb7-128">Reads a JSON file, loads the data into a `JsonDocument`, and writes formatted (pretty-printed) JSON to a file.</span></span>
* <span data-ttu-id="60eb7-129">Używa <xref:System.Text.Json.JsonDocumentOptions> do określenia, czy komentarze w wejściowym formacie JSON są dozwolone, ale ignorowane.</span><span class="sxs-lookup"><span data-stu-id="60eb7-129">Uses <xref:System.Text.Json.JsonDocumentOptions> to specify that comments in the input JSON are allowed but ignored.</span></span>
* <span data-ttu-id="60eb7-130">Po zakończeniu wywołania <xref:System.Text.Json.Utf8JsonWriter.Flush%2A> na składniku zapisywania.</span><span class="sxs-lookup"><span data-stu-id="60eb7-130">When finished, calls <xref:System.Text.Json.Utf8JsonWriter.Flush%2A> on the writer.</span></span> <span data-ttu-id="60eb7-131">Alternatywą jest umożliwienie autoopróżniania składnika zapisywania, gdy zostanie on usunięty.</span><span class="sxs-lookup"><span data-stu-id="60eb7-131">An alternative is to let the writer auto-flush when it's disposed.</span></span>

<span data-ttu-id="60eb7-132">Oto przykład danych wejściowych JSON do przetworzenia przez przykładowy kod:</span><span class="sxs-lookup"><span data-stu-id="60eb7-132">Here's an example of JSON input to be processed by the example code:</span></span>

:::code language="json" source="snippets/system-text-json-how-to/csharp/Grades.json":::

<span data-ttu-id="60eb7-133">Wynikiem są następujące niedrukowane dane wyjściowe JSON:</span><span class="sxs-lookup"><span data-stu-id="60eb7-133">The result is the following pretty-printed JSON output:</span></span>

:::code language="json" source="snippets/system-text-json-how-to/csharp/GradesPrettyPrint.json":::

## <a name="use-utf8jsonwriter"></a><span data-ttu-id="60eb7-134">Użyj Utf8JsonWriter</span><span class="sxs-lookup"><span data-stu-id="60eb7-134">Use Utf8JsonWriter</span></span>

<span data-ttu-id="60eb7-135">Poniższy przykład pokazuje, jak używać <xref:System.Text.Json.Utf8JsonWriter> klasy:</span><span class="sxs-lookup"><span data-stu-id="60eb7-135">The following example shows how to use the <xref:System.Text.Json.Utf8JsonWriter> class:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/Utf8WriterToStream.cs" id="Serialize":::

## <a name="use-utf8jsonreader"></a><span data-ttu-id="60eb7-136">Użyj Utf8JsonReader</span><span class="sxs-lookup"><span data-stu-id="60eb7-136">Use Utf8JsonReader</span></span>

<span data-ttu-id="60eb7-137">Poniższy przykład pokazuje, jak używać <xref:System.Text.Json.Utf8JsonReader> klasy:</span><span class="sxs-lookup"><span data-stu-id="60eb7-137">The following example shows how to use the <xref:System.Text.Json.Utf8JsonReader> class:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/Utf8ReaderFromBytes.cs" id="Deserialize":::

<span data-ttu-id="60eb7-138">Poprzedni kod założono, że `jsonUtf8` zmienna jest tablicą bajtową, która zawiera prawidłowy kod JSON zakodowany jako UTF-8.</span><span class="sxs-lookup"><span data-stu-id="60eb7-138">The preceding code assumes that the `jsonUtf8` variable is a byte array that contains valid JSON, encoded as UTF-8.</span></span>

### <a name="filter-data-using-utf8jsonreader"></a><span data-ttu-id="60eb7-139">Filtrowanie danych za pomocą Utf8JsonReader</span><span class="sxs-lookup"><span data-stu-id="60eb7-139">Filter data using Utf8JsonReader</span></span>

<span data-ttu-id="60eb7-140">Poniższy przykład pokazuje, jak synchronicznie odczytać plik i wyszukać wartość.</span><span class="sxs-lookup"><span data-stu-id="60eb7-140">The following example shows how to synchronously read a file, and search for a value.</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/Utf8ReaderFromFile.cs":::

<span data-ttu-id="60eb7-141">Aby zapoznać się z wersją asynchroniczną tego przykładu, zobacz [projekt Samples w formacie JSON programu .NET](https://github.com/dotnet/samples/blob/18e31a5f1abd4f347bf96bfdc3e40e2cfb36e319/core/json/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="60eb7-141">For an asynchronous version of this example, see [.NET samples JSON project](https://github.com/dotnet/samples/blob/18e31a5f1abd4f347bf96bfdc3e40e2cfb36e319/core/json/Program.cs).</span></span>

<span data-ttu-id="60eb7-142">Powyższy kod ma następujące działanie:</span><span class="sxs-lookup"><span data-stu-id="60eb7-142">The preceding code:</span></span>

* <span data-ttu-id="60eb7-143">Przyjęto, że kod JSON zawiera tablicę obiektów, a każdy obiekt może zawierać właściwość "name" typu String.</span><span class="sxs-lookup"><span data-stu-id="60eb7-143">Assumes the JSON contains an array of objects and each object may contain a "name" property of type string.</span></span>
* <span data-ttu-id="60eb7-144">Zlicza obiekty i wartości właściwości "name", które kończą się znakiem "University".</span><span class="sxs-lookup"><span data-stu-id="60eb7-144">Counts objects and "name" property values that end with "University".</span></span>
* <span data-ttu-id="60eb7-145">Przyjęto założenie, że plik jest zakodowany jako UTF-16 i transkoduje go do UTF-8.</span><span class="sxs-lookup"><span data-stu-id="60eb7-145">Assumes the file is encoded as UTF-16 and transcodes it into UTF-8.</span></span> <span data-ttu-id="60eb7-146">Plik zakodowany jako UTF-8 może być odczytywany bezpośrednio do programu `ReadOnlySpan<byte>` , przy użyciu następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="60eb7-146">A file encoded as UTF-8 can be read directly into a `ReadOnlySpan<byte>`, by using the following code:</span></span>

  ```csharp
  ReadOnlySpan<byte> jsonReadOnlySpan = File.ReadAllBytes(fileName);
  ```

  <span data-ttu-id="60eb7-147">Jeśli plik zawiera znacznik kolejności bajtów UTF-8, usuń go przed przekazaniem bajtów do `Utf8JsonReader` , ponieważ czytnik oczekuje tekstu.</span><span class="sxs-lookup"><span data-stu-id="60eb7-147">If the file contains a UTF-8 byte order mark (BOM), remove it before passing the bytes to the `Utf8JsonReader`, since the reader expects text.</span></span> <span data-ttu-id="60eb7-148">W przeciwnym razie BOM jest traktowany jako nieprawidłowy kod JSON, a czytelnik zgłasza wyjątek.</span><span class="sxs-lookup"><span data-stu-id="60eb7-148">Otherwise, the BOM is considered invalid JSON, and the reader throws an exception.</span></span>

<span data-ttu-id="60eb7-149">Oto przykład JSON, który może odczytać poprzedzający kod.</span><span class="sxs-lookup"><span data-stu-id="60eb7-149">Here's a JSON sample that the preceding code can read.</span></span> <span data-ttu-id="60eb7-150">Otrzymany komunikat podsumowujący to "2 z 4 mają nazwy kończące się na" University ":</span><span class="sxs-lookup"><span data-stu-id="60eb7-150">The resulting summary message is "2 out of 4 have names that end with 'University'":</span></span>

:::code language="json" source="snippets/system-text-json-how-to/csharp/Universities.json":::

### <a name="read-from-a-stream-using-utf8jsonreader"></a><span data-ttu-id="60eb7-151">Odczytaj ze strumienia przy użyciu Utf8JsonReader</span><span class="sxs-lookup"><span data-stu-id="60eb7-151">Read from a stream using Utf8JsonReader</span></span>

<span data-ttu-id="60eb7-152">W przypadku odczytywania dużego pliku (na przykład gigabajta lub więcej) można uniknąć konieczności załadowania całego pliku do pamięci jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="60eb7-152">When reading a large file (a gigabyte or more in size, for example), you might want to avoid having to load the entire file into memory at once.</span></span> <span data-ttu-id="60eb7-153">W tym scenariuszu można użyć <xref:System.IO.FileStream> .</span><span class="sxs-lookup"><span data-stu-id="60eb7-153">For this scenario, you can use a <xref:System.IO.FileStream>.</span></span>

<span data-ttu-id="60eb7-154">W przypadku `Utf8JsonReader` odczytywania ze strumienia przy użyciu programu, obowiązują następujące reguły:</span><span class="sxs-lookup"><span data-stu-id="60eb7-154">When using the `Utf8JsonReader` to read from a stream, the following rules apply:</span></span>

* <span data-ttu-id="60eb7-155">Bufor zawierający częściowy ładunek JSON musi być co najmniej tak duży jak największy token JSON w nim, tak aby czytelnik mógł postępować dalej.</span><span class="sxs-lookup"><span data-stu-id="60eb7-155">The buffer containing the partial JSON payload must be at least as large as the largest JSON token within it so that the reader can make forward progress.</span></span>
* <span data-ttu-id="60eb7-156">Bufor musi być co najmniej tak duże, jak największą sekwencję białych znaków w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="60eb7-156">The buffer must be at least as large as the largest sequence of white space within the JSON.</span></span>
* <span data-ttu-id="60eb7-157">Czytnik nie śledzi danych, które zostały odczytane, dopóki nie zostaną całkowicie odczytane dalej <xref:System.Text.Json.Utf8JsonReader.TokenType%2A> w ładunku JSON.</span><span class="sxs-lookup"><span data-stu-id="60eb7-157">The reader doesn't keep track of the data it has read until it completely reads the next <xref:System.Text.Json.Utf8JsonReader.TokenType%2A> in the JSON payload.</span></span> <span data-ttu-id="60eb7-158">Tak więc, gdy bajty są pozostawione w buforze, należy ponownie przekazać je do czytnika.</span><span class="sxs-lookup"><span data-stu-id="60eb7-158">So when there are bytes left over in the buffer, you have to pass them to the reader again.</span></span> <span data-ttu-id="60eb7-159">Możesz użyć, <xref:System.Text.Json.Utf8JsonReader.BytesConsumed%2A> Aby określić, ile bajtów pozostało.</span><span class="sxs-lookup"><span data-stu-id="60eb7-159">You can use <xref:System.Text.Json.Utf8JsonReader.BytesConsumed%2A> to determine how many bytes are left over.</span></span>

<span data-ttu-id="60eb7-160">Poniższy kod ilustruje sposób odczytywania ze strumienia.</span><span class="sxs-lookup"><span data-stu-id="60eb7-160">The following code illustrates how to read from a stream.</span></span> <span data-ttu-id="60eb7-161">Przykład pokazuje <xref:System.IO.MemoryStream> .</span><span class="sxs-lookup"><span data-stu-id="60eb7-161">The example shows a <xref:System.IO.MemoryStream>.</span></span> <span data-ttu-id="60eb7-162">Podobny kod będzie działał z <xref:System.IO.FileStream> , z wyjątkiem sytuacji, gdy `FileStream` zawiera BOM w formacie UTF-8.</span><span class="sxs-lookup"><span data-stu-id="60eb7-162">Similar code will work with a <xref:System.IO.FileStream>, except when the `FileStream` contains a UTF-8 BOM at the start.</span></span> <span data-ttu-id="60eb7-163">W takim przypadku należy rozdzielić te trzy bajty z buforu przed przekazaniem pozostałych bajtów do `Utf8JsonReader` .</span><span class="sxs-lookup"><span data-stu-id="60eb7-163">In that case, you need to strip those three bytes from the buffer before passing the remaining bytes to the `Utf8JsonReader`.</span></span> <span data-ttu-id="60eb7-164">W przeciwnym razie czytelnik zgłosi wyjątek, ponieważ BOM nie jest traktowany jako prawidłowa część JSON.</span><span class="sxs-lookup"><span data-stu-id="60eb7-164">Otherwise the reader would throw an exception, since the BOM is not considered a valid part of the JSON.</span></span>

<span data-ttu-id="60eb7-165">Przykładowy kod rozpoczyna się od buforu 4 KB i podwaja rozmiar buforu za każdym razem, gdy okaże się, że rozmiar nie jest wystarczająco duży, aby dopasować pełny token JSON, który jest wymagany, aby czytnik mógł postępować w ładunku JSON.</span><span class="sxs-lookup"><span data-stu-id="60eb7-165">The sample code starts with a 4KB buffer and doubles the buffer size each time it finds that the size is not large enough to fit a complete JSON token, which is required for the reader to make forward progress on the JSON payload.</span></span> <span data-ttu-id="60eb7-166">Przykład JSON podany w fragmencie kodu wyzwala zwiększenie rozmiaru buforu tylko wtedy, gdy ustawisz bardzo mały początkowy rozmiar buforu, na przykład 10 bajtów.</span><span class="sxs-lookup"><span data-stu-id="60eb7-166">The JSON sample provided in the snippet triggers a buffer size increase only if you set a very small initial buffer size, for example, 10 bytes.</span></span> <span data-ttu-id="60eb7-167">Jeśli ustawisz początkowy rozmiar buforu na 10, `Console.WriteLine` instrukcje ilustrują przyczynę i wpływ rozmiaru buforu.</span><span class="sxs-lookup"><span data-stu-id="60eb7-167">If you set the initial buffer size to 10, the `Console.WriteLine` statements illustrate the cause and effect of buffer size increases.</span></span> <span data-ttu-id="60eb7-168">W początkowym rozmiarze bufora 4 KB cały przykładowy kod JSON jest pokazywany przez każdy z nich `Console.WriteLine` , a rozmiar buforu nigdy nie musi zostać zwiększony.</span><span class="sxs-lookup"><span data-stu-id="60eb7-168">At the 4KB initial buffer size, the entire sample JSON is shown by each `Console.WriteLine`, and the buffer size never has to be increased.</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/Utf8ReaderPartialRead.cs":::

<span data-ttu-id="60eb7-169">W powyższym przykładzie nie ustawiono limitu rozmiaru buforu.</span><span class="sxs-lookup"><span data-stu-id="60eb7-169">The preceding example sets no limit to how large the buffer can grow.</span></span> <span data-ttu-id="60eb7-170">Jeśli rozmiar tokenu jest zbyt duży, kod może zakończyć się niepowodzeniem z <xref:System.OutOfMemoryException> wyjątkiem.</span><span class="sxs-lookup"><span data-stu-id="60eb7-170">If the token size is too large, the code could fail with an <xref:System.OutOfMemoryException> exception.</span></span> <span data-ttu-id="60eb7-171">Taka sytuacja może wystąpić, jeśli kod JSON zawiera token o rozmiarze około 1 GB lub więcej, ponieważ Podwajanie rozmiaru 1 GB spowoduje, że rozmiar jest zbyt duży, aby zmieścił się w `int32` buforze.</span><span class="sxs-lookup"><span data-stu-id="60eb7-171">This can happen if the JSON contains a token that is around 1 GB or more in size, because doubling the 1 GB size results in a size that is too large to fit into an `int32` buffer.</span></span>

## <a name="see-also"></a><span data-ttu-id="60eb7-172">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="60eb7-172">See also</span></span>

* [<span data-ttu-id="60eb7-173">System.Text.Json Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="60eb7-173">System.Text.Json overview</span></span>](system-text-json-overview.md)
* [<span data-ttu-id="60eb7-174">Jak dostosować kodowanie znaków</span><span class="sxs-lookup"><span data-stu-id="60eb7-174">How to customize character encoding</span></span>](system-text-json-character-encoding.md)
* [<span data-ttu-id="60eb7-175">Jak napisać konwertery niestandardowe na potrzeby serializacji JSON</span><span class="sxs-lookup"><span data-stu-id="60eb7-175">How to write custom converters for JSON serialization</span></span>](system-text-json-converters-how-to.md)
* <span data-ttu-id="60eb7-176">[System.Text.Json Dokumentacja interfejsu API](xref:System.Text.Json)</span><span class="sxs-lookup"><span data-stu-id="60eb7-176">[System.Text.Json API reference](xref:System.Text.Json)</span></span>
