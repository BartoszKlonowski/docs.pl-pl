---
title: Jak pisać konwertery niestandardowe na potrzeby serializacji JSON — .NET
ms.date: 01/10/2020
no-loc:
- System.Text.Json
- Newtonsoft.Json
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
- converters
ms.openlocfilehash: abda23ea538c2c0da6ada4f359ce745602dca45d
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/02/2020
ms.locfileid: "84279766"
---
# <a name="how-to-write-custom-converters-for-json-serialization-marshalling-in-net"></a><span data-ttu-id="d2bd3-102">Jak pisać konwertery niestandardowe na potrzeby serializacji JSON (kierowanie) w programie .NET</span><span class="sxs-lookup"><span data-stu-id="d2bd3-102">How to write custom converters for JSON serialization (marshalling) in .NET</span></span>

<span data-ttu-id="d2bd3-103">W tym artykule pokazano, jak utworzyć niestandardowe konwertery dla klas serializacji JSON, które są dostępne w <xref:System.Text.Json> przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-103">This article shows how to create custom converters for the JSON serialization classes that are provided in the <xref:System.Text.Json> namespace.</span></span> <span data-ttu-id="d2bd3-104">Wprowadzenie do programu można `System.Text.Json` znaleźć [w temacie jak serializować i DESERIALIZOWAĆ kod JSON w programie .NET](system-text-json-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="d2bd3-104">For an introduction to `System.Text.Json`, see [How to serialize and deserialize JSON in .NET](system-text-json-how-to.md).</span></span>

<span data-ttu-id="d2bd3-105">*Konwerter* jest klasą, która konwertuje obiekt lub wartość do i z formatu JSON.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-105">A *converter* is a class that converts an object or a value to and from JSON.</span></span> <span data-ttu-id="d2bd3-106">`System.Text.Json`Przestrzeń nazw ma wbudowane konwertery dla większości typów pierwotnych, które są mapowane na elementy pierwotne języka JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-106">The `System.Text.Json` namespace has built-in converters for most primitive types that map to JavaScript primitives.</span></span> <span data-ttu-id="d2bd3-107">Możesz pisać niestandardowe konwertery:</span><span class="sxs-lookup"><span data-stu-id="d2bd3-107">You can write custom converters:</span></span>

* <span data-ttu-id="d2bd3-108">Aby zastąpić domyślne zachowanie konwertera wbudowanego.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-108">To override the default behavior of a built-in converter.</span></span> <span data-ttu-id="d2bd3-109">Na przykład, możesz chcieć `DateTime` przedstawić wartości w formacie mm/dd/rrrr zamiast domyślnego formatu ISO 8601-1:2019.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-109">For example, you might want `DateTime` values to be represented by mm/dd/yyyy format instead of the default  ISO 8601-1:2019 format.</span></span>
* <span data-ttu-id="d2bd3-110">Do obsługi niestandardowego typu wartości.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-110">To support a custom value type.</span></span> <span data-ttu-id="d2bd3-111">Na przykład `PhoneNumber` Struktura.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-111">For example, a `PhoneNumber` struct.</span></span>

<span data-ttu-id="d2bd3-112">Możesz również napisać niestandardowe konwertery, aby dostosować lub zwiększyć `System.Text.Json` funkcjonalność, która nie jest uwzględniona w bieżącej wersji.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-112">You can also write custom converters to customize or extend `System.Text.Json` with functionality not included in the current release.</span></span> <span data-ttu-id="d2bd3-113">Poniższe scenariusze zostały omówione w dalszej części tego artykułu:</span><span class="sxs-lookup"><span data-stu-id="d2bd3-113">The following scenarios are covered later in this article:</span></span>

* <span data-ttu-id="d2bd3-114">[Deserializacja wywnioskowanych typów do właściwości obiektu](#deserialize-inferred-types-to-object-properties).</span><span class="sxs-lookup"><span data-stu-id="d2bd3-114">[Deserialize inferred types to object properties](#deserialize-inferred-types-to-object-properties).</span></span>
* <span data-ttu-id="d2bd3-115">[Obsługa słownika z kluczem niebędącym ciągiem](#support-dictionary-with-non-string-key).</span><span class="sxs-lookup"><span data-stu-id="d2bd3-115">[Support Dictionary with non-string key](#support-dictionary-with-non-string-key).</span></span>
* <span data-ttu-id="d2bd3-116">[Obsługa deserializacji polimorficznej](#support-polymorphic-deserialization).</span><span class="sxs-lookup"><span data-stu-id="d2bd3-116">[Support polymorphic deserialization](#support-polymorphic-deserialization).</span></span>
* <span data-ttu-id="d2bd3-117">[Obsługa rundy dla stosu \<T> ](#support-round-trip-for-stackt).</span><span class="sxs-lookup"><span data-stu-id="d2bd3-117">[Support round-trip for Stack\<T>](#support-round-trip-for-stackt).</span></span>

## <a name="custom-converter-patterns"></a><span data-ttu-id="d2bd3-118">Wzorce niestandardowego konwertera</span><span class="sxs-lookup"><span data-stu-id="d2bd3-118">Custom converter patterns</span></span>

<span data-ttu-id="d2bd3-119">Istnieją dwa wzorce do tworzenia niestandardowego konwertera: wzorzec podstawowy i wzorzec fabryki.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-119">There are two patterns for creating a custom converter: the basic pattern and the factory pattern.</span></span> <span data-ttu-id="d2bd3-120">Wzorzec fabryki jest przeznaczony dla konwerterów, które obsługują typ `Enum` lub otwierają typy ogólne.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-120">The factory pattern is for converters that handle type `Enum` or open generics.</span></span> <span data-ttu-id="d2bd3-121">Wzorzec podstawowy dotyczy typów ogólnych nieogólnych i zamkniętych.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-121">The basic pattern is for non-generic and closed generic types.</span></span>  <span data-ttu-id="d2bd3-122">Na przykład konwertery dla następujących typów wymagają wzorca fabryki:</span><span class="sxs-lookup"><span data-stu-id="d2bd3-122">For example, converters for the following types require the factory pattern:</span></span>

* `Dictionary<TKey, TValue>`
* `Enum`
* `List<T>`

<span data-ttu-id="d2bd3-123">Niektóre przykłady typów, które mogą być obsługiwane przez wzorzec Basic, obejmują:</span><span class="sxs-lookup"><span data-stu-id="d2bd3-123">Some examples of types that can be handled by the basic pattern include:</span></span>

* `Dictionary<int, string>`
* `WeekdaysEnum`
* `List<DateTimeOffset>`
* `DateTime`
* `Int32`

<span data-ttu-id="d2bd3-124">Wzorzec podstawowy tworzy klasę, która może obsługiwać jeden typ.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-124">The basic pattern creates a class that can handle one type.</span></span> <span data-ttu-id="d2bd3-125">Wzorzec fabryki tworzy klasę, która określa, w czasie wykonywania, który określony typ jest wymagany i dynamicznie tworzy odpowiedni konwerter.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-125">The factory pattern creates a class that determines, at run time, which specific type is required and dynamically creates the appropriate converter.</span></span>

## <a name="sample-basic-converter"></a><span data-ttu-id="d2bd3-126">Przykładowy konwerter podstawowy</span><span class="sxs-lookup"><span data-stu-id="d2bd3-126">Sample basic converter</span></span>

<span data-ttu-id="d2bd3-127">Poniższy przykład to konwerter, który zastąpi domyślną serializację dla istniejącego typu danych.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-127">The following sample is a converter that overrides default serialization for an existing data type.</span></span> <span data-ttu-id="d2bd3-128">Konwerter używa formatu mm/dd/rrrr dla `DateTimeOffset` właściwości.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-128">The converter uses mm/dd/yyyy format for `DateTimeOffset` properties.</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/DateTimeOffsetConverter.cs)]

## <a name="sample-factory-pattern-converter"></a><span data-ttu-id="d2bd3-129">Przykładowy konwerter wzorców fabryki</span><span class="sxs-lookup"><span data-stu-id="d2bd3-129">Sample factory pattern converter</span></span>

<span data-ttu-id="d2bd3-130">Poniższy kod przedstawia niestandardowy konwerter, który współpracuje z `Dictionary<Enum,TValue>` .</span><span class="sxs-lookup"><span data-stu-id="d2bd3-130">The following code shows a custom converter that works with `Dictionary<Enum,TValue>`.</span></span> <span data-ttu-id="d2bd3-131">Kod jest zgodny z wzorcem fabryki, ponieważ pierwszy parametr typu ogólnego to `Enum` , a drugi jest otwarty.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-131">The code follows the factory pattern because the first generic type parameter is `Enum` and the second is open.</span></span> <span data-ttu-id="d2bd3-132">`CanConvert`Metoda zwraca `true` tylko dla `Dictionary` z dwoma parametrami ogólnymi, z których pierwszy jest `Enum` typem.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-132">The `CanConvert` method returns `true` only for a `Dictionary` with two generic parameters, the first of which is an `Enum` type.</span></span> <span data-ttu-id="d2bd3-133">Wewnętrzny konwerter pobiera istniejący konwerter do obsługi dowolnego typu w czasie wykonywania dla `TValue` .</span><span class="sxs-lookup"><span data-stu-id="d2bd3-133">The inner converter gets an existing converter to handle whichever type is provided at run time for `TValue`.</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/DictionaryTKeyEnumTValueConverter.cs)]

<span data-ttu-id="d2bd3-134">Poprzedni kod jest taki sam jak w [słowniku pomocy technicznej z kluczem innym niż ciąg](#support-dictionary-with-non-string-key) w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-134">The preceding code is the same as what is shown in the [Support Dictionary with non-string key](#support-dictionary-with-non-string-key) later in this article.</span></span>

## <a name="steps-to-follow-the-basic-pattern"></a><span data-ttu-id="d2bd3-135">Kroki prowadzące do wzorca podstawowego</span><span class="sxs-lookup"><span data-stu-id="d2bd3-135">Steps to follow the basic pattern</span></span>

<span data-ttu-id="d2bd3-136">Poniższe kroki wyjaśniają, jak utworzyć konwerter, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d2bd3-136">The following steps explain how to create a converter by following the basic pattern:</span></span>

* <span data-ttu-id="d2bd3-137">Utwórz klasę, która pochodzi od elementu WHERE, który <xref:System.Text.Json.Serialization.JsonConverter%601> `T` ma być serializowany i deserializowany.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-137">Create a class that derives from <xref:System.Text.Json.Serialization.JsonConverter%601> where `T` is the type to be serialized and deserialized.</span></span>
* <span data-ttu-id="d2bd3-138">Zastąp `Read` metodę w celu deserializacji przychodzącego pliku JSON i przekonwertuj go na typ `T` .</span><span class="sxs-lookup"><span data-stu-id="d2bd3-138">Override the `Read` method to deserialize the incoming JSON and convert it to type `T`.</span></span> <span data-ttu-id="d2bd3-139">Użyj <xref:System.Text.Json.Utf8JsonReader> , która jest przenoszona do metody odczytu JSON.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-139">Use the <xref:System.Text.Json.Utf8JsonReader> that is passed to the method to read the JSON.</span></span>
* <span data-ttu-id="d2bd3-140">Zastąp `Write` metodę, aby serializować obiekt przychodzący typu `T` .</span><span class="sxs-lookup"><span data-stu-id="d2bd3-140">Override the `Write` method to serialize the incoming object of type `T`.</span></span> <span data-ttu-id="d2bd3-141">Użyj <xref:System.Text.Json.Utf8JsonWriter> , która jest przenoszona do metody, aby zapisać kod JSON.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-141">Use the <xref:System.Text.Json.Utf8JsonWriter> that is passed to the method to write the JSON.</span></span>
* <span data-ttu-id="d2bd3-142">Zastąp `CanConvert` metodę tylko w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-142">Override the `CanConvert` method only if necessary.</span></span> <span data-ttu-id="d2bd3-143">Domyślna implementacja zwraca, `true` gdy typ do konwersji jest typem `T` .</span><span class="sxs-lookup"><span data-stu-id="d2bd3-143">The default implementation returns `true` when the type to convert is of type `T`.</span></span> <span data-ttu-id="d2bd3-144">W związku z tym konwertery obsługujące tylko typ `T` nie muszą przesłaniać tej metody.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-144">Therefore, converters that support only type `T` don't need to override this method.</span></span> <span data-ttu-id="d2bd3-145">Aby zapoznać się z przykładem konwertera, który musi przesłonić tę metodę, zobacz sekcję [deserializacji polimorficzną](#support-polymorphic-deserialization) w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-145">For an example of a converter that does need to override this method, see the [polymorphic deserialization](#support-polymorphic-deserialization) section later in this article.</span></span>

<span data-ttu-id="d2bd3-146">Możesz odwołać się do [wbudowanego kodu źródłowego konwerterów](https://github.com/dotnet/runtime/tree/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/src/System/Text/Json/Serialization/Converters/) jako implementacji odwołań do pisania konwerterów niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-146">You can refer to the [built-in converters source code](https://github.com/dotnet/runtime/tree/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/src/System/Text/Json/Serialization/Converters/) as reference implementations for writing custom converters.</span></span>

## <a name="steps-to-follow-the-factory-pattern"></a><span data-ttu-id="d2bd3-147">Kroki prowadzące do wzorca fabryki</span><span class="sxs-lookup"><span data-stu-id="d2bd3-147">Steps to follow the factory pattern</span></span>

<span data-ttu-id="d2bd3-148">Poniższe kroki wyjaśniają, jak utworzyć konwerter, postępując zgodnie z wzorcem fabryki:</span><span class="sxs-lookup"><span data-stu-id="d2bd3-148">The following steps explain how to create a converter by following the factory pattern:</span></span>

* <span data-ttu-id="d2bd3-149">Utwórz klasę, która pochodzi od <xref:System.Text.Json.Serialization.JsonConverterFactory> .</span><span class="sxs-lookup"><span data-stu-id="d2bd3-149">Create a class that derives from <xref:System.Text.Json.Serialization.JsonConverterFactory>.</span></span>
* <span data-ttu-id="d2bd3-150">Zastąp `CanConvert` metodę, aby zwracał wartość true, gdy typ do przekonwertowania jest taki, który może obsłużyć konwerter.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-150">Override the `CanConvert` method to return true when the type to convert is one that the converter can handle.</span></span> <span data-ttu-id="d2bd3-151">Na przykład, jeśli konwerter jest przeznaczony dla `List<T>` , może obsłużyć tylko `List<int>` , `List<string>` i `List<DateTime>` .</span><span class="sxs-lookup"><span data-stu-id="d2bd3-151">For example, if the converter is for `List<T>` it might only handle `List<int>`, `List<string>`, and `List<DateTime>`.</span></span>
* <span data-ttu-id="d2bd3-152">Zastąp `CreateConverter` metodę, aby zwrócić wystąpienie klasy konwertera, która będzie obsługiwała typ do konwersji, który jest dostarczany w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-152">Override the `CreateConverter` method to return an instance of a converter class that will handle the type-to-convert that is provided at run time.</span></span>
* <span data-ttu-id="d2bd3-153">Utwórz klasę konwertera, którą `CreateConverter` tworzy wystąpienie metody.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-153">Create the converter class that the `CreateConverter` method instantiates.</span></span>

<span data-ttu-id="d2bd3-154">Wzorzec fabryki jest wymagany do otwierania typów ogólnych, ponieważ kod do konwersji obiektu na i z ciągu nie jest taki sam dla wszystkich typów.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-154">The factory pattern is required for open generics because the code to convert an object to and from a string isn't the same for all types.</span></span> <span data-ttu-id="d2bd3-155">Konwerter dla otwartego typu ogólnego ( `List<T>` na przykład) musi utworzyć konwerter dla zamkniętego typu ogólnego ( `List<DateTime>` na przykład) w tle.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-155">A converter for an open generic type (`List<T>`, for example) has to create a converter for a closed generic type (`List<DateTime>`, for example) behind the scenes.</span></span> <span data-ttu-id="d2bd3-156">Kod musi być zapisany, aby obsługiwał każdy zamknięty typ ogólny, który może obsłużyć konwerter.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-156">Code must be written to handle each closed-generic type that the converter can handle.</span></span>

<span data-ttu-id="d2bd3-157">`Enum`Typ jest podobny do otwartego typu ogólnego: konwerter dla programu `Enum` musi utworzyć konwerter dla określonego `Enum` ( `WeekdaysEnum` na przykład) w tle.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-157">The `Enum` type is similar to an open generic type: a converter for `Enum` has to create a converter for a specific `Enum` (`WeekdaysEnum`, for example) behind the scenes.</span></span>

## <a name="error-handling"></a><span data-ttu-id="d2bd3-158">Obsługa błędów</span><span class="sxs-lookup"><span data-stu-id="d2bd3-158">Error handling</span></span>

<span data-ttu-id="d2bd3-159">Jeśli musisz zgłosić wyjątek w kodzie obsługi błędu, rozważ przegenerowanie <xref:System.Text.Json.JsonException> bez komunikatu.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-159">If you need to throw an exception in error-handling code, consider throwing a <xref:System.Text.Json.JsonException> without a message.</span></span> <span data-ttu-id="d2bd3-160">Ten typ wyjątku powoduje automatyczne utworzenie komunikatu zawierającego ścieżkę do części JSON, która spowodowała błąd.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-160">This exception type automatically creates a message that includes the path to the part of the JSON that caused the error.</span></span> <span data-ttu-id="d2bd3-161">Na przykład instrukcja `throw new JsonException();` generuje komunikat o błędzie, jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="d2bd3-161">For example, the statement `throw new JsonException();` produces an error message like the following example:</span></span>

```
Unhandled exception. System.Text.Json.JsonException:
The JSON value could not be converted to System.Object.
Path: $.Date | LineNumber: 1 | BytePositionInLine: 37.
```

<span data-ttu-id="d2bd3-162">Jeśli zostanie wyświetlony komunikat (na przykład `throw new JsonException("Error occurred")` , wyjątek nadal zapewnia ścieżkę we <xref:System.Text.Json.JsonException.Path> właściwości.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-162">If you do provide a message (for example, `throw new JsonException("Error occurred")`, the exception still provides the path in the <xref:System.Text.Json.JsonException.Path> property.</span></span>

## <a name="register-a-custom-converter"></a><span data-ttu-id="d2bd3-163">Rejestrowanie niestandardowego konwertera</span><span class="sxs-lookup"><span data-stu-id="d2bd3-163">Register a custom converter</span></span>

<span data-ttu-id="d2bd3-164">*Zarejestruj* konwerter niestandardowy, aby `Serialize` `Deserialize` zastosować metody i.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-164">*Register* a custom converter to make the `Serialize` and `Deserialize` methods use it.</span></span> <span data-ttu-id="d2bd3-165">Wybierz jedną z następujących metod:</span><span class="sxs-lookup"><span data-stu-id="d2bd3-165">Choose one of the following approaches:</span></span>

* <span data-ttu-id="d2bd3-166">Dodaj wystąpienie klasy Converter do <xref:System.Text.Json.JsonSerializerOptions.Converters?displayProperty=nameWithType> kolekcji.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-166">Add an instance of the converter class to the <xref:System.Text.Json.JsonSerializerOptions.Converters?displayProperty=nameWithType> collection.</span></span>
* <span data-ttu-id="d2bd3-167">Zastosuj atrybut [[JsonConverter]](xref:System.Text.Json.Serialization.JsonConverterAttribute) do właściwości, które wymagają konwertera niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-167">Apply the [[JsonConverter]](xref:System.Text.Json.Serialization.JsonConverterAttribute) attribute to the properties that require the custom converter.</span></span>
* <span data-ttu-id="d2bd3-168">Zastosuj atrybut [[JsonConverter]](xref:System.Text.Json.Serialization.JsonConverterAttribute) do klasy lub struktury, która reprezentuje niestandardowy typ wartości.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-168">Apply the [[JsonConverter]](xref:System.Text.Json.Serialization.JsonConverterAttribute) attribute to a class or a struct that represents a custom value type.</span></span>

## <a name="registration-sample---converters-collection"></a><span data-ttu-id="d2bd3-169">Przykład rejestracji — kolekcja konwerterów</span><span class="sxs-lookup"><span data-stu-id="d2bd3-169">Registration sample - Converters collection</span></span>

<span data-ttu-id="d2bd3-170">Oto przykład, który sprawia, że <xref:System.ComponentModel.DateTimeOffsetConverter> domyślne właściwości typu <xref:System.DateTimeOffset> :</span><span class="sxs-lookup"><span data-stu-id="d2bd3-170">Here's an example that makes the <xref:System.ComponentModel.DateTimeOffsetConverter> the default for properties of type <xref:System.DateTimeOffset>:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/RegisterConverterWithConvertersCollection.cs?name=SnippetSerialize)]

<span data-ttu-id="d2bd3-171">Załóżmy, że Serializacja wystąpienia następującego typu:</span><span class="sxs-lookup"><span data-stu-id="d2bd3-171">Suppose you serialize an instance of the following type:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWF)]

<span data-ttu-id="d2bd3-172">Oto przykład danych wyjściowych JSON, które pokazują, że użyto niestandardowego konwertera:</span><span class="sxs-lookup"><span data-stu-id="d2bd3-172">Here's an example of JSON output that shows the custom converter was used:</span></span>

```json
{
  "Date": "08/01/2019",
  "TemperatureCelsius": 25,
  "Summary": "Hot"
}
```

<span data-ttu-id="d2bd3-173">Poniższy kod używa tego samego podejścia do deserializacji przy użyciu niestandardowego `DateTimeOffset` konwertera:</span><span class="sxs-lookup"><span data-stu-id="d2bd3-173">The following code uses the same approach to deserialize using the custom `DateTimeOffset` converter:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/RegisterConverterWithConvertersCollection.cs?name=SnippetDeserialize)]

## <a name="registration-sample---jsonconverter-on-a-property"></a><span data-ttu-id="d2bd3-174">Przykład rejestracji — [JsonConverter] na właściwości</span><span class="sxs-lookup"><span data-stu-id="d2bd3-174">Registration sample - [JsonConverter] on a property</span></span>

<span data-ttu-id="d2bd3-175">Poniższy kod wybiera niestandardowy konwerter dla `Date` Właściwości:</span><span class="sxs-lookup"><span data-stu-id="d2bd3-175">The following code selects a custom converter for the `Date` property:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWFWithConverterAttribute)]

<span data-ttu-id="d2bd3-176">Kod do serializacji `WeatherForecastWithConverterAttribute` nie wymaga użycia `JsonSerializeOptions.Converters` :</span><span class="sxs-lookup"><span data-stu-id="d2bd3-176">The code to serialize `WeatherForecastWithConverterAttribute` doesn't require the use of `JsonSerializeOptions.Converters`:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/RegisterConverterWithAttributeOnProperty.cs?name=SnippetSerialize)]

<span data-ttu-id="d2bd3-177">Kod do deserializacji również nie wymaga użycia `Converters` :</span><span class="sxs-lookup"><span data-stu-id="d2bd3-177">The code to deserialize also doesn't require the use of `Converters`:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/RegisterConverterWithAttributeOnProperty.cs?name=SnippetDeserialize)]

## <a name="registration-sample---jsonconverter-on-a-type"></a><span data-ttu-id="d2bd3-178">Przykład rejestracji — [JsonConverter] w typie</span><span class="sxs-lookup"><span data-stu-id="d2bd3-178">Registration sample - [JsonConverter] on a type</span></span>

<span data-ttu-id="d2bd3-179">Tutaj kod, który tworzy strukturę i stosuje `[JsonConverter]` do niego atrybut:</span><span class="sxs-lookup"><span data-stu-id="d2bd3-179">Here's code that creates a struct and applies the `[JsonConverter]` attribute to it:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/Temperature.cs)]

<span data-ttu-id="d2bd3-180">Oto niestandardowy konwerter dla poprzedniej struktury:</span><span class="sxs-lookup"><span data-stu-id="d2bd3-180">Here's the custom converter for the preceding struct:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/TemperatureConverter.cs)]

<span data-ttu-id="d2bd3-181">`[JsonConvert]`Atrybut w strukturze rejestruje niestandardowy konwerter jako domyślny dla właściwości typu `Temperature` .</span><span class="sxs-lookup"><span data-stu-id="d2bd3-181">The `[JsonConvert]` attribute on the struct registers the custom converter as the default for properties of type `Temperature`.</span></span> <span data-ttu-id="d2bd3-182">Konwerter jest automatycznie używany we `TemperatureCelsius` Właściwości następującego typu podczas serializacji lub deserializacji:</span><span class="sxs-lookup"><span data-stu-id="d2bd3-182">The converter is automatically used on the `TemperatureCelsius` property of the following type when you serialize or deserialize it:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWFWithTemperatureStruct)]

## <a name="converter-registration-precedence"></a><span data-ttu-id="d2bd3-183">Pierwszeństwo rejestracji konwertera</span><span class="sxs-lookup"><span data-stu-id="d2bd3-183">Converter registration precedence</span></span>

<span data-ttu-id="d2bd3-184">Podczas serializacji lub deserializacji konwerter jest wybierany dla każdego elementu JSON w następującej kolejności, na podstawie najwyższego priorytetu:</span><span class="sxs-lookup"><span data-stu-id="d2bd3-184">During serialization or deserialization, a converter is chosen for each JSON element in the following order, listed from highest priority to lowest:</span></span>

* <span data-ttu-id="d2bd3-185">`[JsonConverter]`zastosowano do właściwości.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-185">`[JsonConverter]` applied to a property.</span></span>
* <span data-ttu-id="d2bd3-186">Konwerter dodany do `Converters` kolekcji.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-186">A converter added to the `Converters` collection.</span></span>
* <span data-ttu-id="d2bd3-187">`[JsonConverter]`stosowane do niestandardowego typu wartości lub POCO.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-187">`[JsonConverter]` applied to a custom value type or POCO.</span></span>

<span data-ttu-id="d2bd3-188">Jeśli wiele konwerterów niestandardowych dla typu są zarejestrowane w `Converters` kolekcji, używany jest pierwszy konwerter zwracający wartość true dla `CanConvert` .</span><span class="sxs-lookup"><span data-stu-id="d2bd3-188">If multiple custom converters for a type are registered in the `Converters` collection, the first converter that returns true for `CanConvert` is used.</span></span>

<span data-ttu-id="d2bd3-189">Wbudowany konwerter jest wybierany tylko wtedy, gdy nie zarejestrowano żadnego odpowiedniego konwertera niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-189">A built-in converter is chosen only if no applicable custom converter is registered.</span></span>

## <a name="converter-samples-for-common-scenarios"></a><span data-ttu-id="d2bd3-190">Przykłady konwerterów dla typowych scenariuszy</span><span class="sxs-lookup"><span data-stu-id="d2bd3-190">Converter samples for common scenarios</span></span>

<span data-ttu-id="d2bd3-191">Poniższe sekcje zawierają przykłady konwerterów, które dotyczą niektórych typowych scenariuszy, które nie obsługują funkcji wbudowanych.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-191">The following sections provide converter samples that address some common scenarios that built-in functionality doesn't handle.</span></span>

* [<span data-ttu-id="d2bd3-192">Deserializacja wywnioskowanych typów do właściwości obiektu</span><span class="sxs-lookup"><span data-stu-id="d2bd3-192">Deserialize inferred types to object properties</span></span>](#deserialize-inferred-types-to-object-properties)
* [<span data-ttu-id="d2bd3-193">Obsługa słownika z kluczem niebędącym ciągiem</span><span class="sxs-lookup"><span data-stu-id="d2bd3-193">Support Dictionary with non-string key</span></span>](#support-dictionary-with-non-string-key)
* [<span data-ttu-id="d2bd3-194">Obsługa deserializacji polimorficzna</span><span class="sxs-lookup"><span data-stu-id="d2bd3-194">Support polymorphic deserialization</span></span>](#support-polymorphic-deserialization)
* <span data-ttu-id="d2bd3-195">[Obsługa rundy dla stosu \<T> ](#support-round-trip-for-stackt).</span><span class="sxs-lookup"><span data-stu-id="d2bd3-195">[Support round-trip for Stack\<T>](#support-round-trip-for-stackt).</span></span>

### <a name="deserialize-inferred-types-to-object-properties"></a><span data-ttu-id="d2bd3-196">Deserializacja wywnioskowanych typów do właściwości obiektu</span><span class="sxs-lookup"><span data-stu-id="d2bd3-196">Deserialize inferred types to object properties</span></span>

<span data-ttu-id="d2bd3-197">Podczas deserializacji do właściwości typu `object` , `JsonElement` tworzony jest obiekt.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-197">When deserializing to a property of type `object`, a `JsonElement` object is created.</span></span> <span data-ttu-id="d2bd3-198">Przyczyną jest to, że Deserializator nie wie, jakie typy CLR należy utworzyć, i nie próbuje go odgadnąć.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-198">The reason is that the deserializer doesn't know what CLR type to create, and it doesn't try to guess.</span></span> <span data-ttu-id="d2bd3-199">Na przykład, jeśli właściwość JSON ma wartość "true", Deserializator nie uzna, że wartość jest a `Boolean` , a jeśli element ma "01/01/2019", Deserializator nie uzna, że jest to `DateTime` .</span><span class="sxs-lookup"><span data-stu-id="d2bd3-199">For example, if a JSON property has "true", the deserializer doesn't infer that the value is a `Boolean`, and if an element has "01/01/2019", the deserializer doesn't infer that it's a `DateTime`.</span></span>

<span data-ttu-id="d2bd3-200">Wnioskowanie o typie może być niedokładne.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-200">Type inference can be inaccurate.</span></span> <span data-ttu-id="d2bd3-201">Jeśli Deserializator analizuje numer JSON, który nie ma punktu dziesiętnego jako `long` , co może spowodować problemy poza zakresem, jeśli wartość została pierwotnie zserializowana jako `ulong` lub `BigInteger` .</span><span class="sxs-lookup"><span data-stu-id="d2bd3-201">If the deserializer parses a JSON number that has no decimal point as a `long`, that might result in out-of-range issues if the value was originally serialized as a `ulong` or `BigInteger`.</span></span> <span data-ttu-id="d2bd3-202">Analizowanie liczby, która ma przecinek dziesiętny w postaci, `double` może spowodować utratę precyzji, jeśli liczba została pierwotnie zserializowana jako `decimal` .</span><span class="sxs-lookup"><span data-stu-id="d2bd3-202">Parsing a number that has a decimal point as a `double` might lose precision if the number was originally serialized as a `decimal`.</span></span>

<span data-ttu-id="d2bd3-203">W przypadku scenariuszy, które wymagają wnioskowania o typie, poniższy kod przedstawia niestandardowy konwerter `object` właściwości.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-203">For scenarios that require type inference, the following code shows a custom converter for `object` properties.</span></span> <span data-ttu-id="d2bd3-204">Kod konwertuje:</span><span class="sxs-lookup"><span data-stu-id="d2bd3-204">The code converts:</span></span>

* <span data-ttu-id="d2bd3-205">`true`i `false` do`Boolean`</span><span class="sxs-lookup"><span data-stu-id="d2bd3-205">`true` and `false` to `Boolean`</span></span>
* <span data-ttu-id="d2bd3-206">Liczby bez wartości dziesiętnej na`long`</span><span class="sxs-lookup"><span data-stu-id="d2bd3-206">Numbers without a decimal to `long`</span></span>
* <span data-ttu-id="d2bd3-207">Liczby z liczbą dziesiętną do`double`</span><span class="sxs-lookup"><span data-stu-id="d2bd3-207">Numbers with a decimal to `double`</span></span>
* <span data-ttu-id="d2bd3-208">Daty do`DateTime`</span><span class="sxs-lookup"><span data-stu-id="d2bd3-208">Dates to `DateTime`</span></span>
* <span data-ttu-id="d2bd3-209">Ciągi do`string`</span><span class="sxs-lookup"><span data-stu-id="d2bd3-209">Strings to `string`</span></span>
* <span data-ttu-id="d2bd3-210">Wszystko inne do`JsonElement`</span><span class="sxs-lookup"><span data-stu-id="d2bd3-210">Everything else to `JsonElement`</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/ObjectToInferredTypesConverter.cs)]

<span data-ttu-id="d2bd3-211">Następujący kod rejestruje konwerter:</span><span class="sxs-lookup"><span data-stu-id="d2bd3-211">The following code registers the converter:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/DeserializeInferredTypesToObject.cs?name=SnippetRegister)]

<span data-ttu-id="d2bd3-212">Oto przykładowy typ z `object` właściwościami:</span><span class="sxs-lookup"><span data-stu-id="d2bd3-212">Here's an example type with `object` properties:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWFWithObjectProperties)]

<span data-ttu-id="d2bd3-213">Poniższy przykład JSON do deserializacji zawiera wartości, które zostaną rozszeregowane jako `DateTime` , `long` i `string` :</span><span class="sxs-lookup"><span data-stu-id="d2bd3-213">The following example of JSON to deserialize contains values that will be deserialized as `DateTime`, `long`, and `string`:</span></span>

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot",
}
```

<span data-ttu-id="d2bd3-214">Bez niestandardowego konwertera deserializacja umieszcza `JsonElement` w każdej właściwości.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-214">Without the custom converter, deserialization puts a `JsonElement` in each property.</span></span>

<span data-ttu-id="d2bd3-215">[Folder testów jednostkowych](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/) w `System.Text.Json.Serialization` przestrzeni nazw zawiera więcej przykładów niestandardowych konwerterów, które obsługują deserializacja `object` właściwości.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-215">The [unit tests folder](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/) in the `System.Text.Json.Serialization` namespace has more examples of custom converters that handle deserialization to `object` properties.</span></span>

### <a name="support-dictionary-with-non-string-key"></a><span data-ttu-id="d2bd3-216">Obsługa słownika z kluczem niebędącym ciągiem</span><span class="sxs-lookup"><span data-stu-id="d2bd3-216">Support Dictionary with non-string key</span></span>

<span data-ttu-id="d2bd3-217">Wbudowana obsługa kolekcji słowników jest dla programu `Dictionary<string, TValue>` .</span><span class="sxs-lookup"><span data-stu-id="d2bd3-217">The built-in support for dictionary collections is for `Dictionary<string, TValue>`.</span></span> <span data-ttu-id="d2bd3-218">Oznacza to, że klucz musi być ciągiem.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-218">That is, the key must be a string.</span></span> <span data-ttu-id="d2bd3-219">Aby zapewnić obsługę słownika z liczbą całkowitą lub innym typem jako klucz, wymagany jest konwerter niestandardowy.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-219">To support a dictionary with an integer or some other type as the key, a custom converter is required.</span></span>

<span data-ttu-id="d2bd3-220">Poniższy kod przedstawia niestandardowy konwerter, który współpracuje z `Dictionary<Enum,TValue>` :</span><span class="sxs-lookup"><span data-stu-id="d2bd3-220">The following code shows a custom converter that works with `Dictionary<Enum,TValue>`:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/DictionaryTKeyEnumTValueConverter.cs)]

<span data-ttu-id="d2bd3-221">Następujący kod rejestruje konwerter:</span><span class="sxs-lookup"><span data-stu-id="d2bd3-221">The following code registers the converter:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/RoundtripDictionaryTkeyEnumTValue.cs?name=SnippetRegister)]

<span data-ttu-id="d2bd3-222">Konwerter może serializować i deserializować `TemperatureRanges` Właściwości następującej klasy, która używa następujących elementów `Enum` :</span><span class="sxs-lookup"><span data-stu-id="d2bd3-222">The converter can serialize and deserialize the `TemperatureRanges` property of the following class that uses the following `Enum`:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWFWithEnumDictionary)]

<span data-ttu-id="d2bd3-223">Dane wyjściowe JSON z serializacji wyglądają podobnie jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="d2bd3-223">The JSON output from serialization looks like the following example:</span></span>

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot",
  "TemperatureRanges": {
    "Cold": 20,
    "Hot": 40
  }
}
```

<span data-ttu-id="d2bd3-224">[Folder testów jednostkowych](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/) w `System.Text.Json.Serialization` przestrzeni nazw zawiera więcej przykładów niestandardowych konwerterów, które obsługują słowniki niebędące ciągami.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-224">The [unit tests folder](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/) in the `System.Text.Json.Serialization` namespace has more examples of custom converters that handle non-string-key dictionaries.</span></span>

### <a name="support-polymorphic-deserialization"></a><span data-ttu-id="d2bd3-225">Obsługa deserializacji polimorficzna</span><span class="sxs-lookup"><span data-stu-id="d2bd3-225">Support polymorphic deserialization</span></span>

<span data-ttu-id="d2bd3-226">Wbudowane funkcje zapewniają ograniczony zakres [serializacji polimorficznej](system-text-json-how-to.md#serialize-properties-of-derived-classes) , ale nie obsługują deserializacji.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-226">Built-in features provide a limited range of [polymorphic serialization](system-text-json-how-to.md#serialize-properties-of-derived-classes) but no support for deserialization at all.</span></span> <span data-ttu-id="d2bd3-227">Deserializacja wymaga konwertera niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-227">Deserialization requires a custom converter.</span></span>

<span data-ttu-id="d2bd3-228">Załóżmy na przykład, że masz `Person` abstrakcyjną klasę bazową z `Employee` i `Customer` klasami pochodnymi.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-228">Suppose, for example, you have a `Person` abstract base class, with `Employee` and `Customer` derived classes.</span></span> <span data-ttu-id="d2bd3-229">Deserializacja polimorficzna oznacza, że w czasie projektowania można określić `Person` jako element docelowy deserializacji, `Customer` a `Employee` obiekty w formacie JSON są poprawnie deserializowane w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-229">Polymorphic deserialization means that at design time you can specify `Person` as the deserialization target, and `Customer` and `Employee` objects in the JSON are correctly deserialized at run time.</span></span> <span data-ttu-id="d2bd3-230">Podczas deserializacji należy znaleźć wskazówki, które identyfikują wymagany typ w kodzie JSON.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-230">During deserialization, you have to find clues that identify the required type in the JSON.</span></span> <span data-ttu-id="d2bd3-231">Rodzaje dostępnych wskazówek różnią się w zależności od scenariusza.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-231">The kinds of clues available vary with each scenario.</span></span> <span data-ttu-id="d2bd3-232">Na przykład może być dostępna właściwość rozróżniacza lub może zależeć od obecności lub braku określonej właściwości.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-232">For example, a discriminator property might be available or you might have to rely on the presence or absence of a particular property.</span></span> <span data-ttu-id="d2bd3-233">Bieżąca wersja programu `System.Text.Json` nie udostępnia atrybutów, aby określić sposób obsługi scenariuszy deserializacji polimorficznych, dlatego wymagane są niestandardowe konwertery.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-233">The current release of `System.Text.Json` doesn't provide attributes to specify how to handle polymorphic deserialization scenarios, so custom converters are required.</span></span>

<span data-ttu-id="d2bd3-234">Poniższy kod przedstawia klasę bazową, dwie klasy pochodne i niestandardowy konwerter dla nich.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-234">The following code shows a base class, two derived classes, and a custom converter for them.</span></span> <span data-ttu-id="d2bd3-235">Konwerter używa właściwości rozróżniacza do wykonywania deserializacji polimorficznej.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-235">The converter uses a discriminator property to do polymorphic deserialization.</span></span> <span data-ttu-id="d2bd3-236">Rozróżniacz typu nie znajduje się w definicjach klas, ale jest tworzony podczas serializacji i jest odczytywany podczas deserializacji.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-236">The type discriminator isn't in the class definitions but is created during serialization and is read during deserialization.</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/Person.cs?name=SnippetPerson)]

[!code-csharp[](snippets/system-text-json-how-to/csharp/PersonConverterWithTypeDiscriminator.cs)]

<span data-ttu-id="d2bd3-237">Następujący kod rejestruje konwerter:</span><span class="sxs-lookup"><span data-stu-id="d2bd3-237">The following code registers the converter:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/RoundtripPolymorphic.cs?name=SnippetRegister)]

<span data-ttu-id="d2bd3-238">Konwerter może deserializować kod JSON, który został utworzony przy użyciu tego samego konwertera do serializacji, na przykład:</span><span class="sxs-lookup"><span data-stu-id="d2bd3-238">The converter can deserialize JSON that was created by using the same converter to serialize, for example:</span></span>

```json
[
  {
    "TypeDiscriminator": 1,
    "CreditLimit": 10000,
    "Name": "John"
  },
  {
    "TypeDiscriminator": 2,
    "OfficeNumber": "555-1234",
    "Name": "Nancy"
  }
]
```

<span data-ttu-id="d2bd3-239">Kod konwertera w poprzednim przykładzie odczytuje i zapisuje każdą właściwość ręcznie.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-239">The converter code in the preceding example reads and writes each property manually.</span></span> <span data-ttu-id="d2bd3-240">Alternatywą jest wywołanie `Deserialize` lub `Serialize` wykonanie niektórych zadań.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-240">An alternative is to call `Deserialize` or `Serialize` to do some of the work.</span></span> <span data-ttu-id="d2bd3-241">Aby zapoznać się z przykładem, zobacz [ten StackOverflow post](https://stackoverflow.com/a/59744873/12509023).</span><span class="sxs-lookup"><span data-stu-id="d2bd3-241">For an example, see [this StackOverflow post](https://stackoverflow.com/a/59744873/12509023).</span></span>

### <a name="support-round-trip-for-stackt"></a><span data-ttu-id="d2bd3-242">Obsługa rundy dla stosu\<T></span><span class="sxs-lookup"><span data-stu-id="d2bd3-242">Support round-trip for Stack\<T></span></span>

<span data-ttu-id="d2bd3-243">W przypadku deserializacji ciągu JSON do <xref:System.Collections.Generic.Stack%601> obiektu, a następnie serializacji tego obiektu, zawartość stosu jest w odwrotnej kolejności.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-243">If you deserialize a JSON string into a <xref:System.Collections.Generic.Stack%601> object and then serialize that object, the contents of the stack are in reverse order.</span></span> <span data-ttu-id="d2bd3-244">To zachowanie dotyczy następujących typów i interfejsów oraz typów zdefiniowanych przez użytkownika, które pochodzą z nich:</span><span class="sxs-lookup"><span data-stu-id="d2bd3-244">This behavior applies to the following types and interface, and user-defined types that derive from them:</span></span>

* <xref:System.Collections.Stack>
* <xref:System.Collections.Generic.Stack%601>
* <xref:System.Collections.Concurrent.ConcurrentStack%601>
* <xref:System.Collections.Immutable.ImmutableStack%601>
* <xref:System.Collections.Immutable.IImmutableStack%601>

<span data-ttu-id="d2bd3-245">Aby zapewnić obsługę serializacji i deserializacji, która zachowuje oryginalną kolejność w stosie, wymagany jest konwerter niestandardowy.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-245">To support serialization and deserialization that retains the original order in the stack, a custom converter is required.</span></span>

<span data-ttu-id="d2bd3-246">Poniższy kod przedstawia niestandardowy konwerter, który umożliwia wykonywanie rundy i z `Stack<T>` obiektów:</span><span class="sxs-lookup"><span data-stu-id="d2bd3-246">The following code shows a custom converter that enables round-tripping to and from `Stack<T>` objects:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/JsonConverterFactoryForStackOfT.cs)]

<span data-ttu-id="d2bd3-247">Następujący kod rejestruje konwerter:</span><span class="sxs-lookup"><span data-stu-id="d2bd3-247">The following code registers the converter:</span></span>

[!code-csharp[](snippets/system-text-json-how-to/csharp/RoundtripStackOfT.cs?name=SnippetRegister)]

## <a name="other-custom-converter-samples"></a><span data-ttu-id="d2bd3-248">Inne przykłady konwerterów niestandardowych</span><span class="sxs-lookup"><span data-stu-id="d2bd3-248">Other custom converter samples</span></span>

<span data-ttu-id="d2bd3-249">[Migracja z Newtonsoft.Json do System.Text.Json ](system-text-json-migrate-from-newtonsoft-how-to.md) artykułu zawiera dodatkowe przykłady konwerterów niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-249">The [Migrate from Newtonsoft.Json to System.Text.Json](system-text-json-migrate-from-newtonsoft-how-to.md) article contains additional samples of custom converters.</span></span>

<span data-ttu-id="d2bd3-250">[Folder testów jednostkowych](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/) w `System.Text.Json.Serialization` kodzie źródłowym zawiera inne przykłady niestandardowego konwertera, takie jak:</span><span class="sxs-lookup"><span data-stu-id="d2bd3-250">The [unit tests folder](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/) in the `System.Text.Json.Serialization` source code includes other custom converter samples, such as:</span></span>

* <span data-ttu-id="d2bd3-251">[Konwerter Int32, który konwertuje wartość null na wartość 0 podczas deserializacji](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/CustomConverterTests.NullValueType.cs)</span><span class="sxs-lookup"><span data-stu-id="d2bd3-251">[Int32 converter that converts null to 0 on deserialize](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/CustomConverterTests.NullValueType.cs)</span></span>
* <span data-ttu-id="d2bd3-252">[Konwerter Int32, który zezwala na wartości typu String i Number przy deserializacji](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/CustomConverterTests.Int32.cs)</span><span class="sxs-lookup"><span data-stu-id="d2bd3-252">[Int32 converter that allows both string and number values on deserialize](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/CustomConverterTests.Int32.cs)</span></span>
* <span data-ttu-id="d2bd3-253">[Konwerter wyliczenia](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/CustomConverterTests.Enum.cs)</span><span class="sxs-lookup"><span data-stu-id="d2bd3-253">[Enum converter](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/CustomConverterTests.Enum.cs)</span></span>
* <span data-ttu-id="d2bd3-254">[\<T>Konwerter listy akceptujący dane zewnętrzne](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/CustomConverterTests.List.cs)</span><span class="sxs-lookup"><span data-stu-id="d2bd3-254">[List\<T> converter that accepts external data](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/CustomConverterTests.List.cs)</span></span>
* <span data-ttu-id="d2bd3-255">[Długi konwerter [], który działa z rozdzielaną przecinkami listą liczb](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/CustomConverterTests.Array.cs)</span><span class="sxs-lookup"><span data-stu-id="d2bd3-255">[Long[] converter that works with a comma-delimited list of numbers](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/CustomConverterTests.Array.cs)</span></span>

<span data-ttu-id="d2bd3-256">Jeśli musisz utworzyć konwerter, który modyfikuje zachowanie istniejącego wbudowanego konwertera, możesz uzyskać [kod źródłowy istniejącego konwertera](https://github.com/dotnet/runtime/tree/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/src/System/Text/Json/Serialization/Converters) , który będzie używany jako punkt wyjścia do dostosowania.</span><span class="sxs-lookup"><span data-stu-id="d2bd3-256">If you need to make a converter that modifies the behavior of an existing built-in converter, you can get [the source code of the existing converter](https://github.com/dotnet/runtime/tree/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/src/System/Text/Json/Serialization/Converters) to serve as a starting point for customization.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d2bd3-257">Zasoby dodatkowe</span><span class="sxs-lookup"><span data-stu-id="d2bd3-257">Additional resources</span></span>

* <span data-ttu-id="d2bd3-258">[Kod źródłowy wbudowanych konwerterów](https://github.com/dotnet/runtime/tree/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/src/System/Text/Json/Serialization/Converters)</span><span class="sxs-lookup"><span data-stu-id="d2bd3-258">[Source code for built-in converters](https://github.com/dotnet/runtime/tree/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/src/System/Text/Json/Serialization/Converters)</span></span>
* <span data-ttu-id="d2bd3-259">[Obsługa DateTime i DateTimeOffset wSystem.Text.Json](../datetime/system-text-json-support.md)</span><span class="sxs-lookup"><span data-stu-id="d2bd3-259">[DateTime and DateTimeOffset support in System.Text.Json](../datetime/system-text-json-support.md)</span></span>
* <span data-ttu-id="d2bd3-260">[System.Text.JsonPodsumowanie](system-text-json-overview.md)</span><span class="sxs-lookup"><span data-stu-id="d2bd3-260">[System.Text.Json overview](system-text-json-overview.md)</span></span>
* <span data-ttu-id="d2bd3-261">[Jak używaćSystem.Text.Json](system-text-json-how-to.md)</span><span class="sxs-lookup"><span data-stu-id="d2bd3-261">[How to use System.Text.Json](system-text-json-how-to.md)</span></span>
* <span data-ttu-id="d2bd3-262">[Jak przeprowadzić migrację zNewtonsoft.Json](system-text-json-migrate-from-newtonsoft-how-to.md)</span><span class="sxs-lookup"><span data-stu-id="d2bd3-262">[How to migrate from Newtonsoft.Json](system-text-json-migrate-from-newtonsoft-how-to.md)</span></span>
* <span data-ttu-id="d2bd3-263">[System.Text.JsonDokumentacja interfejsu API](xref:System.Text.Json)</span><span class="sxs-lookup"><span data-stu-id="d2bd3-263">[System.Text.Json API reference](xref:System.Text.Json)</span></span>
* <span data-ttu-id="d2bd3-264">[System.Text.Json. Dokumentacja interfejsu API serializacji](xref:System.Text.Json.Serialization)</span><span class="sxs-lookup"><span data-stu-id="d2bd3-264">[System.Text.Json.Serialization API reference](xref:System.Text.Json.Serialization)</span></span>
<!-- * [System.Text.Json roadmap](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/roadmap/README.md)-->
