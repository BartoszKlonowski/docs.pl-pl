---
title: Jak pisać konwertery niestandardowe na potrzeby serializacji JSON — .NET
description: Dowiedz się, jak utworzyć niestandardowe konwertery dla klas serializacji JSON, które są dostępne w System.Text.Json przestrzeni nazw.
ms.date: 12/14/2020
no-loc:
- System.Text.Json
- Newtonsoft.Json
zone_pivot_groups: dotnet-version
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
- converters
ms.openlocfilehash: 390438e3dca7a5d40dd9957090f498b495996e05
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2020
ms.locfileid: "97513201"
---
# <a name="how-to-write-custom-converters-for-json-serialization-marshalling-in-net"></a><span data-ttu-id="c9150-103">Jak pisać konwertery niestandardowe na potrzeby serializacji JSON (kierowanie) w programie .NET</span><span class="sxs-lookup"><span data-stu-id="c9150-103">How to write custom converters for JSON serialization (marshalling) in .NET</span></span>

<span data-ttu-id="c9150-104">W tym artykule pokazano, jak utworzyć niestandardowe konwertery dla klas serializacji JSON, które są dostępne w <xref:System.Text.Json> przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="c9150-104">This article shows how to create custom converters for the JSON serialization classes that are provided in the <xref:System.Text.Json> namespace.</span></span> <span data-ttu-id="c9150-105">Wprowadzenie do programu można `System.Text.Json` znaleźć [w temacie jak serializować i DESERIALIZOWAĆ kod JSON w programie .NET](system-text-json-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="c9150-105">For an introduction to `System.Text.Json`, see [How to serialize and deserialize JSON in .NET](system-text-json-how-to.md).</span></span>

<span data-ttu-id="c9150-106">*Konwerter* jest klasą, która konwertuje obiekt lub wartość do i z formatu JSON.</span><span class="sxs-lookup"><span data-stu-id="c9150-106">A *converter* is a class that converts an object or a value to and from JSON.</span></span> <span data-ttu-id="c9150-107">`System.Text.Json`Przestrzeń nazw ma wbudowane konwertery dla większości typów pierwotnych, które są mapowane na elementy pierwotne języka JavaScript.</span><span class="sxs-lookup"><span data-stu-id="c9150-107">The `System.Text.Json` namespace has built-in converters for most primitive types that map to JavaScript primitives.</span></span> <span data-ttu-id="c9150-108">Możesz pisać niestandardowe konwertery:</span><span class="sxs-lookup"><span data-stu-id="c9150-108">You can write custom converters:</span></span>

* <span data-ttu-id="c9150-109">Aby zastąpić domyślne zachowanie konwertera wbudowanego.</span><span class="sxs-lookup"><span data-stu-id="c9150-109">To override the default behavior of a built-in converter.</span></span> <span data-ttu-id="c9150-110">Na przykład, możesz chcieć `DateTime` przedstawić wartości w formacie mm/dd/rrrr.</span><span class="sxs-lookup"><span data-stu-id="c9150-110">For example, you might want `DateTime` values to be represented by mm/dd/yyyy format.</span></span> <span data-ttu-id="c9150-111">Domyślnie ISO 8601-1:2019 jest obsługiwany łącznie z profilem RFC 3339.</span><span class="sxs-lookup"><span data-stu-id="c9150-111">By default, ISO 8601-1:2019 is supported, including the RFC 3339 profile.</span></span> <span data-ttu-id="c9150-112">Aby uzyskać więcej informacji, zobacz [Obsługa DateTime i DateTimeOffset System.Text.Json w ](../datetime/system-text-json-support.md).</span><span class="sxs-lookup"><span data-stu-id="c9150-112">For more information, see [DateTime and DateTimeOffset support in System.Text.Json](../datetime/system-text-json-support.md).</span></span>
* <span data-ttu-id="c9150-113">Do obsługi niestandardowego typu wartości.</span><span class="sxs-lookup"><span data-stu-id="c9150-113">To support a custom value type.</span></span> <span data-ttu-id="c9150-114">Na przykład `PhoneNumber` Struktura.</span><span class="sxs-lookup"><span data-stu-id="c9150-114">For example, a `PhoneNumber` struct.</span></span>

<span data-ttu-id="c9150-115">Możesz również napisać niestandardowe konwertery, aby dostosować lub zwiększyć `System.Text.Json` funkcjonalność, która nie jest uwzględniona w bieżącej wersji.</span><span class="sxs-lookup"><span data-stu-id="c9150-115">You can also write custom converters to customize or extend `System.Text.Json` with functionality not included in the current release.</span></span> <span data-ttu-id="c9150-116">Poniższe scenariusze zostały omówione w dalszej części tego artykułu:</span><span class="sxs-lookup"><span data-stu-id="c9150-116">The following scenarios are covered later in this article:</span></span>

::: zone pivot="dotnet-5-0"

* <span data-ttu-id="c9150-117">[Deserializacja wywnioskowanych typów do właściwości obiektu](#deserialize-inferred-types-to-object-properties).</span><span class="sxs-lookup"><span data-stu-id="c9150-117">[Deserialize inferred types to object properties](#deserialize-inferred-types-to-object-properties).</span></span>
* <span data-ttu-id="c9150-118">[Obsługa deserializacji polimorficznej](#support-polymorphic-deserialization).</span><span class="sxs-lookup"><span data-stu-id="c9150-118">[Support polymorphic deserialization](#support-polymorphic-deserialization).</span></span>
* <span data-ttu-id="c9150-119">[Obsługa rundy dla stosu \<T> ](#support-round-trip-for-stackt).</span><span class="sxs-lookup"><span data-stu-id="c9150-119">[Support round-trip for Stack\<T>](#support-round-trip-for-stackt).</span></span>
::: zone-end

::: zone pivot="dotnet-core-3-1"

* <span data-ttu-id="c9150-120">[Deserializacja wywnioskowanych typów do właściwości obiektu](#deserialize-inferred-types-to-object-properties).</span><span class="sxs-lookup"><span data-stu-id="c9150-120">[Deserialize inferred types to object properties](#deserialize-inferred-types-to-object-properties).</span></span>
* <span data-ttu-id="c9150-121">[Obsługa słownika z kluczem niebędącym ciągiem](#support-dictionary-with-non-string-key).</span><span class="sxs-lookup"><span data-stu-id="c9150-121">[Support Dictionary with non-string key](#support-dictionary-with-non-string-key).</span></span>
* <span data-ttu-id="c9150-122">[Obsługa deserializacji polimorficznej](#support-polymorphic-deserialization).</span><span class="sxs-lookup"><span data-stu-id="c9150-122">[Support polymorphic deserialization](#support-polymorphic-deserialization).</span></span>
* <span data-ttu-id="c9150-123">[Obsługa rundy dla stosu \<T> ](#support-round-trip-for-stackt).</span><span class="sxs-lookup"><span data-stu-id="c9150-123">[Support round-trip for Stack\<T>](#support-round-trip-for-stackt).</span></span>
::: zone-end

<span data-ttu-id="c9150-124">W kodzie napisanym dla niestandardowego konwertera należy pamiętać o znacznej wydajności związanej z korzystaniem z nowych <xref:System.Text.Json.JsonSerializerOptions> wystąpień.</span><span class="sxs-lookup"><span data-stu-id="c9150-124">In the code you write for a custom converter, be aware of the substantial performance penalty for using new <xref:System.Text.Json.JsonSerializerOptions> instances.</span></span> <span data-ttu-id="c9150-125">Aby uzyskać więcej informacji, zobacz [ponowne użycie wystąpień JsonSerializerOptions](system-text-json-configure-options.md#reuse-jsonserializeroptions-instances).</span><span class="sxs-lookup"><span data-stu-id="c9150-125">For more information, see [Reuse JsonSerializerOptions instances](system-text-json-configure-options.md#reuse-jsonserializeroptions-instances).</span></span>

## <a name="custom-converter-patterns"></a><span data-ttu-id="c9150-126">Wzorce niestandardowego konwertera</span><span class="sxs-lookup"><span data-stu-id="c9150-126">Custom converter patterns</span></span>

<span data-ttu-id="c9150-127">Istnieją dwa wzorce do tworzenia niestandardowego konwertera: wzorzec podstawowy i wzorzec fabryki.</span><span class="sxs-lookup"><span data-stu-id="c9150-127">There are two patterns for creating a custom converter: the basic pattern and the factory pattern.</span></span> <span data-ttu-id="c9150-128">Wzorzec fabryki jest przeznaczony dla konwerterów, które obsługują typ `Enum` lub otwierają typy ogólne.</span><span class="sxs-lookup"><span data-stu-id="c9150-128">The factory pattern is for converters that handle type `Enum` or open generics.</span></span> <span data-ttu-id="c9150-129">Wzorzec podstawowy dotyczy typów ogólnych nieogólnych i zamkniętych.</span><span class="sxs-lookup"><span data-stu-id="c9150-129">The basic pattern is for non-generic and closed generic types.</span></span>  <span data-ttu-id="c9150-130">Na przykład konwertery dla następujących typów wymagają wzorca fabryki:</span><span class="sxs-lookup"><span data-stu-id="c9150-130">For example, converters for the following types require the factory pattern:</span></span>

* <xref:System.Collections.Generic.Dictionary%602>
* <xref:System.Enum>
* <xref:System.Collections.Generic.List%601>

<span data-ttu-id="c9150-131">Niektóre przykłady typów, które mogą być obsługiwane przez wzorzec Basic, obejmują:</span><span class="sxs-lookup"><span data-stu-id="c9150-131">Some examples of types that can be handled by the basic pattern include:</span></span>

* `Dictionary<int, string>`
* `WeekdaysEnum`
* `List<DateTimeOffset>`
* <xref:System.DateTime>
* <xref:System.Int32>

<span data-ttu-id="c9150-132">Wzorzec podstawowy tworzy klasę, która może obsługiwać jeden typ.</span><span class="sxs-lookup"><span data-stu-id="c9150-132">The basic pattern creates a class that can handle one type.</span></span> <span data-ttu-id="c9150-133">Wzorzec fabryki tworzy klasę, która określa, w czasie wykonywania, który określony typ jest wymagany i dynamicznie tworzy odpowiedni konwerter.</span><span class="sxs-lookup"><span data-stu-id="c9150-133">The factory pattern creates a class that determines, at run time, which specific type is required and dynamically creates the appropriate converter.</span></span>

## <a name="sample-basic-converter"></a><span data-ttu-id="c9150-134">Przykładowy konwerter podstawowy</span><span class="sxs-lookup"><span data-stu-id="c9150-134">Sample basic converter</span></span>

<span data-ttu-id="c9150-135">Poniższy przykład to konwerter, który zastąpi domyślną serializację dla istniejącego typu danych.</span><span class="sxs-lookup"><span data-stu-id="c9150-135">The following sample is a converter that overrides default serialization for an existing data type.</span></span> <span data-ttu-id="c9150-136">Konwerter używa formatu mm/dd/rrrr dla `DateTimeOffset` właściwości.</span><span class="sxs-lookup"><span data-stu-id="c9150-136">The converter uses mm/dd/yyyy format for `DateTimeOffset` properties.</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/DateTimeOffsetConverter.cs":::

## <a name="sample-factory-pattern-converter"></a><span data-ttu-id="c9150-137">Przykładowy konwerter wzorców fabryki</span><span class="sxs-lookup"><span data-stu-id="c9150-137">Sample factory pattern converter</span></span>

<span data-ttu-id="c9150-138">Poniższy kod przedstawia niestandardowy konwerter, który współpracuje z `Dictionary<Enum,TValue>` .</span><span class="sxs-lookup"><span data-stu-id="c9150-138">The following code shows a custom converter that works with `Dictionary<Enum,TValue>`.</span></span> <span data-ttu-id="c9150-139">Kod jest zgodny z wzorcem fabryki, ponieważ pierwszy parametr typu ogólnego to `Enum` , a drugi jest otwarty.</span><span class="sxs-lookup"><span data-stu-id="c9150-139">The code follows the factory pattern because the first generic type parameter is `Enum` and the second is open.</span></span> <span data-ttu-id="c9150-140">`CanConvert`Metoda zwraca `true` tylko dla `Dictionary` z dwoma parametrami ogólnymi, z których pierwszy jest `Enum` typem.</span><span class="sxs-lookup"><span data-stu-id="c9150-140">The `CanConvert` method returns `true` only for a `Dictionary` with two generic parameters, the first of which is an `Enum` type.</span></span> <span data-ttu-id="c9150-141">Wewnętrzny konwerter pobiera istniejący konwerter do obsługi dowolnego typu w czasie wykonywania dla `TValue` .</span><span class="sxs-lookup"><span data-stu-id="c9150-141">The inner converter gets an existing converter to handle whichever type is provided at run time for `TValue`.</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/DictionaryTKeyEnumTValueConverter.cs":::

<span data-ttu-id="c9150-142">Poprzedni kod jest taki sam jak w [słowniku pomocy technicznej z kluczem innym niż ciąg](#support-dictionary-with-non-string-key) w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="c9150-142">The preceding code is the same as what is shown in the [Support Dictionary with non-string key](#support-dictionary-with-non-string-key) later in this article.</span></span>

## <a name="steps-to-follow-the-basic-pattern"></a><span data-ttu-id="c9150-143">Kroki prowadzące do wzorca podstawowego</span><span class="sxs-lookup"><span data-stu-id="c9150-143">Steps to follow the basic pattern</span></span>

<span data-ttu-id="c9150-144">Poniższe kroki wyjaśniają, jak utworzyć konwerter, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c9150-144">The following steps explain how to create a converter by following the basic pattern:</span></span>

* <span data-ttu-id="c9150-145">Utwórz klasę, która pochodzi od elementu WHERE, który <xref:System.Text.Json.Serialization.JsonConverter%601> `T` ma być serializowany i deserializowany.</span><span class="sxs-lookup"><span data-stu-id="c9150-145">Create a class that derives from <xref:System.Text.Json.Serialization.JsonConverter%601> where `T` is the type to be serialized and deserialized.</span></span>
* <span data-ttu-id="c9150-146">Zastąp `Read` metodę w celu deserializacji przychodzącego pliku JSON i przekonwertuj go na typ `T` .</span><span class="sxs-lookup"><span data-stu-id="c9150-146">Override the `Read` method to deserialize the incoming JSON and convert it to type `T`.</span></span> <span data-ttu-id="c9150-147">Użyj <xref:System.Text.Json.Utf8JsonReader> , która jest przenoszona do metody odczytu JSON.</span><span class="sxs-lookup"><span data-stu-id="c9150-147">Use the <xref:System.Text.Json.Utf8JsonReader> that is passed to the method to read the JSON.</span></span> <span data-ttu-id="c9150-148">Nie musisz martwić się o obsługę częściowych danych, ponieważ serializator przekazuje wszystkie dane dla bieżącego zakresu JSON.</span><span class="sxs-lookup"><span data-stu-id="c9150-148">You don't have to worry about handling partial data, as the serializer passes all the data for the current JSON scope.</span></span> <span data-ttu-id="c9150-149">Dlatego nie jest konieczne Wywołaj <xref:System.Text.Json.Utf8JsonReader.Skip%2A> lub <xref:System.Text.Json.Utf8JsonReader.TrySkip%2A> lub, aby potwierdzić, że <xref:System.Text.Json.Utf8JsonReader.Read%2A> zwraca `true` .</span><span class="sxs-lookup"><span data-stu-id="c9150-149">So it isn't necessary to call <xref:System.Text.Json.Utf8JsonReader.Skip%2A> or <xref:System.Text.Json.Utf8JsonReader.TrySkip%2A> or to validate that <xref:System.Text.Json.Utf8JsonReader.Read%2A> returns `true`.</span></span>
* <span data-ttu-id="c9150-150">Zastąp `Write` metodę, aby serializować obiekt przychodzący typu `T` .</span><span class="sxs-lookup"><span data-stu-id="c9150-150">Override the `Write` method to serialize the incoming object of type `T`.</span></span> <span data-ttu-id="c9150-151">Użyj <xref:System.Text.Json.Utf8JsonWriter> , która jest przenoszona do metody, aby zapisać kod JSON.</span><span class="sxs-lookup"><span data-stu-id="c9150-151">Use the <xref:System.Text.Json.Utf8JsonWriter> that is passed to the method to write the JSON.</span></span>
* <span data-ttu-id="c9150-152">Zastąp `CanConvert` metodę tylko w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="c9150-152">Override the `CanConvert` method only if necessary.</span></span> <span data-ttu-id="c9150-153">Domyślna implementacja zwraca, `true` gdy typ do konwersji jest typem `T` .</span><span class="sxs-lookup"><span data-stu-id="c9150-153">The default implementation returns `true` when the type to convert is of type `T`.</span></span> <span data-ttu-id="c9150-154">W związku z tym konwertery obsługujące tylko typ `T` nie muszą przesłaniać tej metody.</span><span class="sxs-lookup"><span data-stu-id="c9150-154">Therefore, converters that support only type `T` don't need to override this method.</span></span> <span data-ttu-id="c9150-155">Aby zapoznać się z przykładem konwertera, który musi przesłonić tę metodę, zobacz sekcję [deserializacji polimorficzną](#support-polymorphic-deserialization) w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="c9150-155">For an example of a converter that does need to override this method, see the [polymorphic deserialization](#support-polymorphic-deserialization) section later in this article.</span></span>

<span data-ttu-id="c9150-156">Możesz odwołać się do [wbudowanego kodu źródłowego konwerterów](https://github.com/dotnet/runtime/tree/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/src/System/Text/Json/Serialization/Converters/) jako implementacji odwołań do pisania konwerterów niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="c9150-156">You can refer to the [built-in converters source code](https://github.com/dotnet/runtime/tree/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/src/System/Text/Json/Serialization/Converters/) as reference implementations for writing custom converters.</span></span>

## <a name="steps-to-follow-the-factory-pattern"></a><span data-ttu-id="c9150-157">Kroki prowadzące do wzorca fabryki</span><span class="sxs-lookup"><span data-stu-id="c9150-157">Steps to follow the factory pattern</span></span>

<span data-ttu-id="c9150-158">Poniższe kroki wyjaśniają, jak utworzyć konwerter, postępując zgodnie z wzorcem fabryki:</span><span class="sxs-lookup"><span data-stu-id="c9150-158">The following steps explain how to create a converter by following the factory pattern:</span></span>

* <span data-ttu-id="c9150-159">Utwórz klasę, która pochodzi od <xref:System.Text.Json.Serialization.JsonConverterFactory> .</span><span class="sxs-lookup"><span data-stu-id="c9150-159">Create a class that derives from <xref:System.Text.Json.Serialization.JsonConverterFactory>.</span></span>
* <span data-ttu-id="c9150-160">Zastąp `CanConvert` metodę, aby zwracał wartość true, gdy typ do przekonwertowania jest taki, który może obsłużyć konwerter.</span><span class="sxs-lookup"><span data-stu-id="c9150-160">Override the `CanConvert` method to return true when the type to convert is one that the converter can handle.</span></span> <span data-ttu-id="c9150-161">Na przykład, jeśli konwerter jest przeznaczony dla `List<T>` , może obsłużyć tylko `List<int>` , `List<string>` i `List<DateTime>` .</span><span class="sxs-lookup"><span data-stu-id="c9150-161">For example, if the converter is for `List<T>` it might only handle `List<int>`, `List<string>`, and `List<DateTime>`.</span></span>
* <span data-ttu-id="c9150-162">Zastąp `CreateConverter` metodę, aby zwrócić wystąpienie klasy konwertera, która będzie obsługiwała typ do konwersji, który jest dostarczany w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="c9150-162">Override the `CreateConverter` method to return an instance of a converter class that will handle the type-to-convert that is provided at run time.</span></span>
* <span data-ttu-id="c9150-163">Utwórz klasę konwertera, którą `CreateConverter` tworzy wystąpienie metody.</span><span class="sxs-lookup"><span data-stu-id="c9150-163">Create the converter class that the `CreateConverter` method instantiates.</span></span>

<span data-ttu-id="c9150-164">Wzorzec fabryki jest wymagany do otwierania typów ogólnych, ponieważ kod do konwersji obiektu na i z ciągu nie jest taki sam dla wszystkich typów.</span><span class="sxs-lookup"><span data-stu-id="c9150-164">The factory pattern is required for open generics because the code to convert an object to and from a string isn't the same for all types.</span></span> <span data-ttu-id="c9150-165">Konwerter dla otwartego typu ogólnego ( `List<T>` na przykład) musi utworzyć konwerter dla zamkniętego typu ogólnego ( `List<DateTime>` na przykład) w tle.</span><span class="sxs-lookup"><span data-stu-id="c9150-165">A converter for an open generic type (`List<T>`, for example) has to create a converter for a closed generic type (`List<DateTime>`, for example) behind the scenes.</span></span> <span data-ttu-id="c9150-166">Kod musi być zapisany, aby obsługiwał każdy zamknięty typ ogólny, który może obsłużyć konwerter.</span><span class="sxs-lookup"><span data-stu-id="c9150-166">Code must be written to handle each closed-generic type that the converter can handle.</span></span>

<span data-ttu-id="c9150-167">`Enum`Typ jest podobny do otwartego typu ogólnego: konwerter dla programu `Enum` musi utworzyć konwerter dla określonego `Enum` ( `WeekdaysEnum` na przykład) w tle.</span><span class="sxs-lookup"><span data-stu-id="c9150-167">The `Enum` type is similar to an open generic type: a converter for `Enum` has to create a converter for a specific `Enum` (`WeekdaysEnum`, for example) behind the scenes.</span></span>

## <a name="error-handling"></a><span data-ttu-id="c9150-168">Obsługa błędów</span><span class="sxs-lookup"><span data-stu-id="c9150-168">Error handling</span></span>

<span data-ttu-id="c9150-169">Serializator zapewnia specjalną obsługę typów wyjątków <xref:System.Text.Json.JsonException> i <xref:System.NotSupportedException> .</span><span class="sxs-lookup"><span data-stu-id="c9150-169">The serializer provides special handling for exception types <xref:System.Text.Json.JsonException> and <xref:System.NotSupportedException>.</span></span>

### <a name="jsonexception"></a><span data-ttu-id="c9150-170">Jsonexception</span><span class="sxs-lookup"><span data-stu-id="c9150-170">JsonException</span></span>

<span data-ttu-id="c9150-171">W przypadku zgłoszenia `JsonException` bez komunikatu, serializator tworzy komunikat, który zawiera ścieżkę do części JSON, która spowodowała błąd.</span><span class="sxs-lookup"><span data-stu-id="c9150-171">If you throw a `JsonException` without a message, the serializer creates a message that includes the path to the part of the JSON that caused the error.</span></span> <span data-ttu-id="c9150-172">Na przykład instrukcja `throw new JsonException()` generuje komunikat o błędzie, jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="c9150-172">For example, the statement `throw new JsonException()` produces an error message like the following example:</span></span>

```output
Unhandled exception. System.Text.Json.JsonException:
The JSON value could not be converted to System.Object.
Path: $.Date | LineNumber: 1 | BytePositionInLine: 37.
```

<span data-ttu-id="c9150-173">Jeśli zostanie wyświetlony komunikat (na przykład `throw new JsonException("Error occurred")` , serializator nadal ustawia <xref:System.Text.Json.JsonException.Path> <xref:System.Text.Json.JsonException.LineNumber> właściwości,, i <xref:System.Text.Json.JsonException.BytePositionInLine> .</span><span class="sxs-lookup"><span data-stu-id="c9150-173">If you do provide a message (for example, `throw new JsonException("Error occurred")`, the serializer still sets the <xref:System.Text.Json.JsonException.Path>, <xref:System.Text.Json.JsonException.LineNumber>, and <xref:System.Text.Json.JsonException.BytePositionInLine> properties.</span></span>

### <a name="notsupportedexception"></a><span data-ttu-id="c9150-174">NotSupportedException</span><span class="sxs-lookup"><span data-stu-id="c9150-174">NotSupportedException</span></span>

<span data-ttu-id="c9150-175">W przypadku zgłoszenia elementu należy `NotSupportedException` zawsze uzyskać informacje o ścieżce w komunikacie.</span><span class="sxs-lookup"><span data-stu-id="c9150-175">If you throw a `NotSupportedException`, you always get the path information in the message.</span></span> <span data-ttu-id="c9150-176">Jeśli zostanie wyświetlony komunikat, do niego są dołączane informacje o ścieżce.</span><span class="sxs-lookup"><span data-stu-id="c9150-176">If you provide a message, the path information is appended to it.</span></span> <span data-ttu-id="c9150-177">Na przykład instrukcja `throw new NotSupportedException("Error occurred.")` generuje komunikat o błędzie, jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="c9150-177">For example, the statement `throw new NotSupportedException("Error occurred.")` produces an error message like the following example:</span></span>

```output
Error occurred. The unsupported member type is located on type
'System.Collections.Generic.Dictionary`2[Samples.SummaryWords,System.Int32]'.
Path: $.TemperatureRanges | LineNumber: 4 | BytePositionInLine: 24
```

### <a name="when-to-throw-which-exception-type"></a><span data-ttu-id="c9150-178">Kiedy należy zgłosić typ wyjątku</span><span class="sxs-lookup"><span data-stu-id="c9150-178">When to throw which exception type</span></span>

<span data-ttu-id="c9150-179">Gdy ładunek JSON zawiera tokeny, które nie są prawidłowe dla deserializowanego typu, throw `JsonException` .</span><span class="sxs-lookup"><span data-stu-id="c9150-179">When the JSON payload contains tokens that are not valid for the type being deserialized, throw a `JsonException`.</span></span>

<span data-ttu-id="c9150-180">Jeśli chcesz uniemożliwić określone typy, throw `NotSupportedException` .</span><span class="sxs-lookup"><span data-stu-id="c9150-180">When you want to disallow certain types, throw a `NotSupportedException`.</span></span> <span data-ttu-id="c9150-181">Ten wyjątek jest tym, co serializator automatycznie zgłasza dla typów, które nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="c9150-181">This exception is what the serializer automatically throws for types that are not supported.</span></span> <span data-ttu-id="c9150-182">Na przykład `System.Type` nie jest obsługiwana ze względów bezpieczeństwa, dlatego próba deserializacji powoduje wystąpienie `NotSupportedException` .</span><span class="sxs-lookup"><span data-stu-id="c9150-182">For example, `System.Type` is not supported for security reasons, so an attempt to deserialize it results in a `NotSupportedException`.</span></span>

<span data-ttu-id="c9150-183">W razie konieczności można zgłosić inne wyjątki, ale nie zawierają one automatycznie informacji o ścieżce JSON.</span><span class="sxs-lookup"><span data-stu-id="c9150-183">You can throw other exceptions as needed, but they don't automatically include JSON path information.</span></span>

## <a name="register-a-custom-converter"></a><span data-ttu-id="c9150-184">Rejestrowanie niestandardowego konwertera</span><span class="sxs-lookup"><span data-stu-id="c9150-184">Register a custom converter</span></span>

<span data-ttu-id="c9150-185">*Zarejestruj* konwerter niestandardowy, aby `Serialize` `Deserialize` zastosować metody i.</span><span class="sxs-lookup"><span data-stu-id="c9150-185">*Register* a custom converter to make the `Serialize` and `Deserialize` methods use it.</span></span> <span data-ttu-id="c9150-186">Wybierz jedną z następujących metod:</span><span class="sxs-lookup"><span data-stu-id="c9150-186">Choose one of the following approaches:</span></span>

* <span data-ttu-id="c9150-187">Dodaj wystąpienie klasy Converter do <xref:System.Text.Json.JsonSerializerOptions.Converters?displayProperty=nameWithType> kolekcji.</span><span class="sxs-lookup"><span data-stu-id="c9150-187">Add an instance of the converter class to the <xref:System.Text.Json.JsonSerializerOptions.Converters?displayProperty=nameWithType> collection.</span></span>
* <span data-ttu-id="c9150-188">Zastosuj atrybut [[JsonConverter]](xref:System.Text.Json.Serialization.JsonConverterAttribute) do właściwości, które wymagają konwertera niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="c9150-188">Apply the [[JsonConverter]](xref:System.Text.Json.Serialization.JsonConverterAttribute) attribute to the properties that require the custom converter.</span></span>
* <span data-ttu-id="c9150-189">Zastosuj atrybut [[JsonConverter]](xref:System.Text.Json.Serialization.JsonConverterAttribute) do klasy lub struktury, która reprezentuje niestandardowy typ wartości.</span><span class="sxs-lookup"><span data-stu-id="c9150-189">Apply the [[JsonConverter]](xref:System.Text.Json.Serialization.JsonConverterAttribute) attribute to a class or a struct that represents a custom value type.</span></span>

## <a name="registration-sample---converters-collection"></a><span data-ttu-id="c9150-190">Przykład rejestracji — kolekcja konwerterów</span><span class="sxs-lookup"><span data-stu-id="c9150-190">Registration sample - Converters collection</span></span>

<span data-ttu-id="c9150-191">Oto przykład, który sprawia, że <xref:System.ComponentModel.DateTimeOffsetConverter> domyślne właściwości typu <xref:System.DateTimeOffset> :</span><span class="sxs-lookup"><span data-stu-id="c9150-191">Here's an example that makes the <xref:System.ComponentModel.DateTimeOffsetConverter> the default for properties of type <xref:System.DateTimeOffset>:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RegisterConverterWithConvertersCollection.cs" id="Serialize":::

<span data-ttu-id="c9150-192">Załóżmy, że Serializacja wystąpienia następującego typu:</span><span class="sxs-lookup"><span data-stu-id="c9150-192">Suppose you serialize an instance of the following type:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WF":::

<span data-ttu-id="c9150-193">Oto przykład danych wyjściowych JSON, które pokazują, że użyto niestandardowego konwertera:</span><span class="sxs-lookup"><span data-stu-id="c9150-193">Here's an example of JSON output that shows the custom converter was used:</span></span>

```json
{
  "Date": "08/01/2019",
  "TemperatureCelsius": 25,
  "Summary": "Hot"
}
```

<span data-ttu-id="c9150-194">Poniższy kod używa tego samego podejścia do deserializacji przy użyciu niestandardowego `DateTimeOffset` konwertera:</span><span class="sxs-lookup"><span data-stu-id="c9150-194">The following code uses the same approach to deserialize using the custom `DateTimeOffset` converter:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RegisterConverterWithConvertersCollection.cs" id="Deserialize":::

## <a name="registration-sample---jsonconverter-on-a-property"></a><span data-ttu-id="c9150-195">Przykład rejestracji — [JsonConverter] na właściwości</span><span class="sxs-lookup"><span data-stu-id="c9150-195">Registration sample - [JsonConverter] on a property</span></span>

<span data-ttu-id="c9150-196">Poniższy kod wybiera niestandardowy konwerter dla `Date` Właściwości:</span><span class="sxs-lookup"><span data-stu-id="c9150-196">The following code selects a custom converter for the `Date` property:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithConverterAttribute":::

<span data-ttu-id="c9150-197">Kod do serializacji `WeatherForecastWithConverterAttribute` nie wymaga użycia `JsonSerializeOptions.Converters` :</span><span class="sxs-lookup"><span data-stu-id="c9150-197">The code to serialize `WeatherForecastWithConverterAttribute` doesn't require the use of `JsonSerializeOptions.Converters`:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RegisterConverterWithAttributeOnProperty.cs" id="Serialize":::

<span data-ttu-id="c9150-198">Kod do deserializacji również nie wymaga użycia `Converters` :</span><span class="sxs-lookup"><span data-stu-id="c9150-198">The code to deserialize also doesn't require the use of `Converters`:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RegisterConverterWithAttributeOnProperty.cs" id="Deserialize":::

## <a name="registration-sample---jsonconverter-on-a-type"></a><span data-ttu-id="c9150-199">Przykład rejestracji — [JsonConverter] w typie</span><span class="sxs-lookup"><span data-stu-id="c9150-199">Registration sample - [JsonConverter] on a type</span></span>

<span data-ttu-id="c9150-200">Tutaj kod, który tworzy strukturę i stosuje `[JsonConverter]` do niego atrybut:</span><span class="sxs-lookup"><span data-stu-id="c9150-200">Here's code that creates a struct and applies the `[JsonConverter]` attribute to it:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/Temperature.cs":::

<span data-ttu-id="c9150-201">Oto niestandardowy konwerter dla poprzedniej struktury:</span><span class="sxs-lookup"><span data-stu-id="c9150-201">Here's the custom converter for the preceding struct:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/TemperatureConverter.cs":::

<span data-ttu-id="c9150-202">`[JsonConvert]`Atrybut w strukturze rejestruje niestandardowy konwerter jako domyślny dla właściwości typu `Temperature` .</span><span class="sxs-lookup"><span data-stu-id="c9150-202">The `[JsonConvert]` attribute on the struct registers the custom converter as the default for properties of type `Temperature`.</span></span> <span data-ttu-id="c9150-203">Konwerter jest automatycznie używany we `TemperatureCelsius` Właściwości następującego typu podczas serializacji lub deserializacji:</span><span class="sxs-lookup"><span data-stu-id="c9150-203">The converter is automatically used on the `TemperatureCelsius` property of the following type when you serialize or deserialize it:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithTemperatureStruct":::

## <a name="converter-registration-precedence"></a><span data-ttu-id="c9150-204">Pierwszeństwo rejestracji konwertera</span><span class="sxs-lookup"><span data-stu-id="c9150-204">Converter registration precedence</span></span>

<span data-ttu-id="c9150-205">Podczas serializacji lub deserializacji konwerter jest wybierany dla każdego elementu JSON w następującej kolejności, na podstawie najwyższego priorytetu:</span><span class="sxs-lookup"><span data-stu-id="c9150-205">During serialization or deserialization, a converter is chosen for each JSON element in the following order, listed from highest priority to lowest:</span></span>

* <span data-ttu-id="c9150-206">`[JsonConverter]` zastosowano do właściwości.</span><span class="sxs-lookup"><span data-stu-id="c9150-206">`[JsonConverter]` applied to a property.</span></span>
* <span data-ttu-id="c9150-207">Konwerter dodany do `Converters` kolekcji.</span><span class="sxs-lookup"><span data-stu-id="c9150-207">A converter added to the `Converters` collection.</span></span>
* <span data-ttu-id="c9150-208">`[JsonConverter]` stosowane do niestandardowego typu wartości lub POCO.</span><span class="sxs-lookup"><span data-stu-id="c9150-208">`[JsonConverter]` applied to a custom value type or POCO.</span></span>

<span data-ttu-id="c9150-209">Jeśli wiele konwerterów niestandardowych dla typu są zarejestrowane w `Converters` kolekcji, używany jest pierwszy konwerter zwracający wartość true dla `CanConvert` .</span><span class="sxs-lookup"><span data-stu-id="c9150-209">If multiple custom converters for a type are registered in the `Converters` collection, the first converter that returns true for `CanConvert` is used.</span></span>

<span data-ttu-id="c9150-210">Wbudowany konwerter jest wybierany tylko wtedy, gdy nie zarejestrowano żadnego odpowiedniego konwertera niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="c9150-210">A built-in converter is chosen only if no applicable custom converter is registered.</span></span>

## <a name="converter-samples-for-common-scenarios"></a><span data-ttu-id="c9150-211">Przykłady konwerterów dla typowych scenariuszy</span><span class="sxs-lookup"><span data-stu-id="c9150-211">Converter samples for common scenarios</span></span>

<span data-ttu-id="c9150-212">Poniższe sekcje zawierają przykłady konwerterów, które dotyczą niektórych typowych scenariuszy, które nie obsługują funkcji wbudowanych.</span><span class="sxs-lookup"><span data-stu-id="c9150-212">The following sections provide converter samples that address some common scenarios that built-in functionality doesn't handle.</span></span>

::: zone pivot="dotnet-5-0"

* <span data-ttu-id="c9150-213">[Deserializacja wywnioskowanych typów do właściwości obiektu](#deserialize-inferred-types-to-object-properties).</span><span class="sxs-lookup"><span data-stu-id="c9150-213">[Deserialize inferred types to object properties](#deserialize-inferred-types-to-object-properties).</span></span>
* <span data-ttu-id="c9150-214">[Obsługa deserializacji polimorficznej](#support-polymorphic-deserialization).</span><span class="sxs-lookup"><span data-stu-id="c9150-214">[Support polymorphic deserialization](#support-polymorphic-deserialization).</span></span>
* <span data-ttu-id="c9150-215">[Obsługa rundy dla stosu \<T> ](#support-round-trip-for-stackt).</span><span class="sxs-lookup"><span data-stu-id="c9150-215">[Support round-trip for Stack\<T>](#support-round-trip-for-stackt).</span></span>
::: zone-end

::: zone pivot="dotnet-core-3-1"

* <span data-ttu-id="c9150-216">[Deserializacja wywnioskowanych typów do właściwości obiektu](#deserialize-inferred-types-to-object-properties).</span><span class="sxs-lookup"><span data-stu-id="c9150-216">[Deserialize inferred types to object properties](#deserialize-inferred-types-to-object-properties).</span></span>
* <span data-ttu-id="c9150-217">[Obsługa słownika z kluczem niebędącym ciągiem](#support-dictionary-with-non-string-key).</span><span class="sxs-lookup"><span data-stu-id="c9150-217">[Support Dictionary with non-string key](#support-dictionary-with-non-string-key).</span></span>
* <span data-ttu-id="c9150-218">[Obsługa deserializacji polimorficznej](#support-polymorphic-deserialization).</span><span class="sxs-lookup"><span data-stu-id="c9150-218">[Support polymorphic deserialization](#support-polymorphic-deserialization).</span></span>
* <span data-ttu-id="c9150-219">[Obsługa rundy dla stosu \<T> ](#support-round-trip-for-stackt).</span><span class="sxs-lookup"><span data-stu-id="c9150-219">[Support round-trip for Stack\<T>](#support-round-trip-for-stackt).</span></span>
::: zone-end

### <a name="deserialize-inferred-types-to-object-properties"></a><span data-ttu-id="c9150-220">Deserializacja wywnioskowanych typów do właściwości obiektu</span><span class="sxs-lookup"><span data-stu-id="c9150-220">Deserialize inferred types to object properties</span></span>

<span data-ttu-id="c9150-221">Podczas deserializacji do właściwości typu `object` , `JsonElement` tworzony jest obiekt.</span><span class="sxs-lookup"><span data-stu-id="c9150-221">When deserializing to a property of type `object`, a `JsonElement` object is created.</span></span> <span data-ttu-id="c9150-222">Przyczyną jest to, że Deserializator nie wie, jakie typy CLR należy utworzyć, i nie próbuje go odgadnąć.</span><span class="sxs-lookup"><span data-stu-id="c9150-222">The reason is that the deserializer doesn't know what CLR type to create, and it doesn't try to guess.</span></span> <span data-ttu-id="c9150-223">Na przykład, jeśli właściwość JSON ma wartość "true", Deserializator nie uzna, że wartość jest a `Boolean` , a jeśli element ma "01/01/2019", Deserializator nie uzna, że jest to `DateTime` .</span><span class="sxs-lookup"><span data-stu-id="c9150-223">For example, if a JSON property has "true", the deserializer doesn't infer that the value is a `Boolean`, and if an element has "01/01/2019", the deserializer doesn't infer that it's a `DateTime`.</span></span>

<span data-ttu-id="c9150-224">Wnioskowanie o typie może być niedokładne.</span><span class="sxs-lookup"><span data-stu-id="c9150-224">Type inference can be inaccurate.</span></span> <span data-ttu-id="c9150-225">Jeśli Deserializator analizuje numer JSON, który nie ma punktu dziesiętnego jako `long` , co może spowodować problemy poza zakresem, jeśli wartość została pierwotnie zserializowana jako `ulong` lub `BigInteger` .</span><span class="sxs-lookup"><span data-stu-id="c9150-225">If the deserializer parses a JSON number that has no decimal point as a `long`, that might result in out-of-range issues if the value was originally serialized as a `ulong` or `BigInteger`.</span></span> <span data-ttu-id="c9150-226">Analizowanie liczby, która ma przecinek dziesiętny w postaci, `double` może spowodować utratę precyzji, jeśli liczba została pierwotnie zserializowana jako `decimal` .</span><span class="sxs-lookup"><span data-stu-id="c9150-226">Parsing a number that has a decimal point as a `double` might lose precision if the number was originally serialized as a `decimal`.</span></span>

<span data-ttu-id="c9150-227">W przypadku scenariuszy, które wymagają wnioskowania o typie, poniższy kod przedstawia niestandardowy konwerter `object` właściwości.</span><span class="sxs-lookup"><span data-stu-id="c9150-227">For scenarios that require type inference, the following code shows a custom converter for `object` properties.</span></span> <span data-ttu-id="c9150-228">Kod konwertuje:</span><span class="sxs-lookup"><span data-stu-id="c9150-228">The code converts:</span></span>

* <span data-ttu-id="c9150-229">`true` i `false` do `Boolean`</span><span class="sxs-lookup"><span data-stu-id="c9150-229">`true` and `false` to `Boolean`</span></span>
* <span data-ttu-id="c9150-230">Liczby bez wartości dziesiętnej na `long`</span><span class="sxs-lookup"><span data-stu-id="c9150-230">Numbers without a decimal to `long`</span></span>
* <span data-ttu-id="c9150-231">Liczby z liczbą dziesiętną do `double`</span><span class="sxs-lookup"><span data-stu-id="c9150-231">Numbers with a decimal to `double`</span></span>
* <span data-ttu-id="c9150-232">Daty do `DateTime`</span><span class="sxs-lookup"><span data-stu-id="c9150-232">Dates to `DateTime`</span></span>
* <span data-ttu-id="c9150-233">Ciągi do `string`</span><span class="sxs-lookup"><span data-stu-id="c9150-233">Strings to `string`</span></span>
* <span data-ttu-id="c9150-234">Wszystko inne do `JsonElement`</span><span class="sxs-lookup"><span data-stu-id="c9150-234">Everything else to `JsonElement`</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/ObjectToInferredTypesConverter.cs":::

<span data-ttu-id="c9150-235">Następujący kod rejestruje konwerter:</span><span class="sxs-lookup"><span data-stu-id="c9150-235">The following code registers the converter:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/DeserializeInferredTypesToObject.cs" id="Register":::

<span data-ttu-id="c9150-236">Oto przykładowy typ z `object` właściwościami:</span><span class="sxs-lookup"><span data-stu-id="c9150-236">Here's an example type with `object` properties:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithObjectProperties":::

<span data-ttu-id="c9150-237">Poniższy przykład JSON do deserializacji zawiera wartości, które zostaną rozszeregowane jako `DateTime` , `long` i `string` :</span><span class="sxs-lookup"><span data-stu-id="c9150-237">The following example of JSON to deserialize contains values that will be deserialized as `DateTime`, `long`, and `string`:</span></span>

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot",
}
```

<span data-ttu-id="c9150-238">Bez niestandardowego konwertera deserializacja umieszcza `JsonElement` w każdej właściwości.</span><span class="sxs-lookup"><span data-stu-id="c9150-238">Without the custom converter, deserialization puts a `JsonElement` in each property.</span></span>

<span data-ttu-id="c9150-239">[Folder testów jednostkowych](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/) w `System.Text.Json.Serialization` przestrzeni nazw zawiera więcej przykładów niestandardowych konwerterów, które obsługują deserializacja `object` właściwości.</span><span class="sxs-lookup"><span data-stu-id="c9150-239">The [unit tests folder](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/) in the `System.Text.Json.Serialization` namespace has more examples of custom converters that handle deserialization to `object` properties.</span></span>

::: zone pivot="dotnet-core-3-1"

### <a name="support-dictionary-with-non-string-key"></a><span data-ttu-id="c9150-240">Obsługa słownika z kluczem niebędącym ciągiem</span><span class="sxs-lookup"><span data-stu-id="c9150-240">Support Dictionary with non-string key</span></span>

<span data-ttu-id="c9150-241">Wbudowana obsługa kolekcji słowników jest dla programu `Dictionary<string, TValue>` .</span><span class="sxs-lookup"><span data-stu-id="c9150-241">The built-in support for dictionary collections is for `Dictionary<string, TValue>`.</span></span> <span data-ttu-id="c9150-242">Oznacza to, że klucz musi być ciągiem.</span><span class="sxs-lookup"><span data-stu-id="c9150-242">That is, the key must be a string.</span></span> <span data-ttu-id="c9150-243">Aby zapewnić obsługę słownika z liczbą całkowitą lub innym typem jako klucz, wymagany jest konwerter niestandardowy.</span><span class="sxs-lookup"><span data-stu-id="c9150-243">To support a dictionary with an integer or some other type as the key, a custom converter is required.</span></span>

<span data-ttu-id="c9150-244">Poniższy kod przedstawia niestandardowy konwerter, który współpracuje z `Dictionary<Enum,TValue>` :</span><span class="sxs-lookup"><span data-stu-id="c9150-244">The following code shows a custom converter that works with `Dictionary<Enum,TValue>`:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/DictionaryTKeyEnumTValueConverter.cs":::

<span data-ttu-id="c9150-245">Następujący kod rejestruje konwerter:</span><span class="sxs-lookup"><span data-stu-id="c9150-245">The following code registers the converter:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripDictionaryTkeyEnumTValue.cs" id="Register":::

<span data-ttu-id="c9150-246">Konwerter może serializować i deserializować `TemperatureRanges` Właściwości następującej klasy, która używa następujących elementów `Enum` :</span><span class="sxs-lookup"><span data-stu-id="c9150-246">The converter can serialize and deserialize the `TemperatureRanges` property of the following class that uses the following `Enum`:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithEnumDictionary":::

<span data-ttu-id="c9150-247">Dane wyjściowe JSON z serializacji wyglądają podobnie jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="c9150-247">The JSON output from serialization looks like the following example:</span></span>

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

<span data-ttu-id="c9150-248">[Folder testów jednostkowych](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/) w `System.Text.Json.Serialization` przestrzeni nazw zawiera więcej przykładów niestandardowych konwerterów, które obsługują słowniki niebędące ciągami.</span><span class="sxs-lookup"><span data-stu-id="c9150-248">The [unit tests folder](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/) in the `System.Text.Json.Serialization` namespace has more examples of custom converters that handle non-string-key dictionaries.</span></span>
::: zone-end

### <a name="support-polymorphic-deserialization"></a><span data-ttu-id="c9150-249">Obsługa deserializacji polimorficzna</span><span class="sxs-lookup"><span data-stu-id="c9150-249">Support polymorphic deserialization</span></span>

<span data-ttu-id="c9150-250">Wbudowane funkcje zapewniają ograniczony zakres [serializacji polimorficznej](system-text-json-polymorphism.md) , ale nie obsługują deserializacji.</span><span class="sxs-lookup"><span data-stu-id="c9150-250">Built-in features provide a limited range of [polymorphic serialization](system-text-json-polymorphism.md) but no support for deserialization at all.</span></span> <span data-ttu-id="c9150-251">Deserializacja wymaga konwertera niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="c9150-251">Deserialization requires a custom converter.</span></span>

<span data-ttu-id="c9150-252">Załóżmy na przykład, że masz `Person` abstrakcyjną klasę bazową z `Employee` i `Customer` klasami pochodnymi.</span><span class="sxs-lookup"><span data-stu-id="c9150-252">Suppose, for example, you have a `Person` abstract base class, with `Employee` and `Customer` derived classes.</span></span> <span data-ttu-id="c9150-253">Deserializacja polimorficzna oznacza, że w czasie projektowania można określić `Person` jako element docelowy deserializacji, `Customer` a `Employee` obiekty w formacie JSON są poprawnie deserializowane w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="c9150-253">Polymorphic deserialization means that at design time you can specify `Person` as the deserialization target, and `Customer` and `Employee` objects in the JSON are correctly deserialized at run time.</span></span> <span data-ttu-id="c9150-254">Podczas deserializacji należy znaleźć wskazówki, które identyfikują wymagany typ w kodzie JSON.</span><span class="sxs-lookup"><span data-stu-id="c9150-254">During deserialization, you have to find clues that identify the required type in the JSON.</span></span> <span data-ttu-id="c9150-255">Rodzaje dostępnych wskazówek różnią się w zależności od scenariusza.</span><span class="sxs-lookup"><span data-stu-id="c9150-255">The kinds of clues available vary with each scenario.</span></span> <span data-ttu-id="c9150-256">Na przykład może być dostępna właściwość rozróżniacza lub może zależeć od obecności lub braku określonej właściwości.</span><span class="sxs-lookup"><span data-stu-id="c9150-256">For example, a discriminator property might be available or you might have to rely on the presence or absence of a particular property.</span></span> <span data-ttu-id="c9150-257">Bieżąca wersja programu `System.Text.Json` nie udostępnia atrybutów, aby określić sposób obsługi scenariuszy deserializacji polimorficznych, dlatego wymagane są niestandardowe konwertery.</span><span class="sxs-lookup"><span data-stu-id="c9150-257">The current release of `System.Text.Json` doesn't provide attributes to specify how to handle polymorphic deserialization scenarios, so custom converters are required.</span></span>

<span data-ttu-id="c9150-258">Poniższy kod przedstawia klasę bazową, dwie klasy pochodne i niestandardowy konwerter dla nich.</span><span class="sxs-lookup"><span data-stu-id="c9150-258">The following code shows a base class, two derived classes, and a custom converter for them.</span></span> <span data-ttu-id="c9150-259">Konwerter używa właściwości rozróżniacza do wykonywania deserializacji polimorficznej.</span><span class="sxs-lookup"><span data-stu-id="c9150-259">The converter uses a discriminator property to do polymorphic deserialization.</span></span> <span data-ttu-id="c9150-260">Rozróżniacz typu nie znajduje się w definicjach klas, ale jest tworzony podczas serializacji i jest odczytywany podczas deserializacji.</span><span class="sxs-lookup"><span data-stu-id="c9150-260">The type discriminator isn't in the class definitions but is created during serialization and is read during deserialization.</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/Person.cs" id="Person":::

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/PersonConverterWithTypeDiscriminator.cs":::

<span data-ttu-id="c9150-261">Następujący kod rejestruje konwerter:</span><span class="sxs-lookup"><span data-stu-id="c9150-261">The following code registers the converter:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripPolymorphic.cs" id="Register":::

<span data-ttu-id="c9150-262">Konwerter może deserializować kod JSON, który został utworzony przy użyciu tego samego konwertera do serializacji, na przykład:</span><span class="sxs-lookup"><span data-stu-id="c9150-262">The converter can deserialize JSON that was created by using the same converter to serialize, for example:</span></span>

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

<span data-ttu-id="c9150-263">Kod konwertera w poprzednim przykładzie odczytuje i zapisuje każdą właściwość ręcznie.</span><span class="sxs-lookup"><span data-stu-id="c9150-263">The converter code in the preceding example reads and writes each property manually.</span></span> <span data-ttu-id="c9150-264">Alternatywą jest wywołanie `Deserialize` lub `Serialize` wykonanie niektórych zadań.</span><span class="sxs-lookup"><span data-stu-id="c9150-264">An alternative is to call `Deserialize` or `Serialize` to do some of the work.</span></span> <span data-ttu-id="c9150-265">Aby zapoznać się z przykładem, zobacz [ten StackOverflow post](https://stackoverflow.com/a/59744873/12509023).</span><span class="sxs-lookup"><span data-stu-id="c9150-265">For an example, see [this StackOverflow post](https://stackoverflow.com/a/59744873/12509023).</span></span>

### <a name="support-round-trip-for-stackt"></a><span data-ttu-id="c9150-266">Obsługa rundy dla stosu\<T></span><span class="sxs-lookup"><span data-stu-id="c9150-266">Support round trip for Stack\<T></span></span>

<span data-ttu-id="c9150-267">W przypadku deserializacji ciągu JSON do <xref:System.Collections.Generic.Stack%601> obiektu, a następnie serializacji tego obiektu, zawartość stosu jest w odwrotnej kolejności.</span><span class="sxs-lookup"><span data-stu-id="c9150-267">If you deserialize a JSON string into a <xref:System.Collections.Generic.Stack%601> object and then serialize that object, the contents of the stack are in reverse order.</span></span> <span data-ttu-id="c9150-268">To zachowanie dotyczy następujących typów i interfejsów oraz typów zdefiniowanych przez użytkownika, które pochodzą z nich:</span><span class="sxs-lookup"><span data-stu-id="c9150-268">This behavior applies to the following types and interface, and user-defined types that derive from them:</span></span>

* <xref:System.Collections.Stack>
* <xref:System.Collections.Generic.Stack%601>
* <xref:System.Collections.Concurrent.ConcurrentStack%601>
* <xref:System.Collections.Immutable.ImmutableStack%601>
* <xref:System.Collections.Immutable.IImmutableStack%601>

<span data-ttu-id="c9150-269">Aby zapewnić obsługę serializacji i deserializacji, która zachowuje oryginalną kolejność w stosie, wymagany jest konwerter niestandardowy.</span><span class="sxs-lookup"><span data-stu-id="c9150-269">To support serialization and deserialization that retains the original order in the stack, a custom converter is required.</span></span>

<span data-ttu-id="c9150-270">Poniższy kod przedstawia niestandardowy konwerter, który umożliwia wykonywanie rundy i z `Stack<T>` obiektów:</span><span class="sxs-lookup"><span data-stu-id="c9150-270">The following code shows a custom converter that enables round-tripping to and from `Stack<T>` objects:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/JsonConverterFactoryForStackOfT.cs":::

<span data-ttu-id="c9150-271">Następujący kod rejestruje konwerter:</span><span class="sxs-lookup"><span data-stu-id="c9150-271">The following code registers the converter:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripStackOfT.cs" id="Register":::

## <a name="handle-null-values"></a><span data-ttu-id="c9150-272">Obsługa wartości null</span><span class="sxs-lookup"><span data-stu-id="c9150-272">Handle null values</span></span>

<span data-ttu-id="c9150-273">Domyślnie serializator obsługuje wartości null w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="c9150-273">By default, the serializer handles null values as follows:</span></span>

* <span data-ttu-id="c9150-274">Dla typów i typów referencyjnych <xref:System.Nullable%601> :</span><span class="sxs-lookup"><span data-stu-id="c9150-274">For reference types and <xref:System.Nullable%601> types:</span></span>

  * <span data-ttu-id="c9150-275">Nie przekazuje `null` do konwerterów niestandardowych podczas serializacji.</span><span class="sxs-lookup"><span data-stu-id="c9150-275">It does not pass `null` to custom converters on serialization.</span></span>
  * <span data-ttu-id="c9150-276">Nie przekazuje `JsonTokenType.Null` do konwerterów niestandardowych podczas deserializacji.</span><span class="sxs-lookup"><span data-stu-id="c9150-276">It does not pass `JsonTokenType.Null` to custom converters on deserialization.</span></span>
  * <span data-ttu-id="c9150-277">Zwraca `null` wystąpienie podczas deserializacji.</span><span class="sxs-lookup"><span data-stu-id="c9150-277">It returns a `null` instance on deserialization.</span></span>
  * <span data-ttu-id="c9150-278">Zapisuje `null` bezpośrednio przy użyciu składnika zapisywania przy serializacji.</span><span class="sxs-lookup"><span data-stu-id="c9150-278">It writes `null` directly with the writer on serialization.</span></span>

* <span data-ttu-id="c9150-279">Dla typów wartości niedopuszczających wartości null:</span><span class="sxs-lookup"><span data-stu-id="c9150-279">For non-nullable value types:</span></span>

  * <span data-ttu-id="c9150-280">Przechodzi `JsonTokenType.Null` do konwerterów niestandardowych podczas deserializacji.</span><span class="sxs-lookup"><span data-stu-id="c9150-280">It passes `JsonTokenType.Null` to custom converters on deserialization.</span></span> <span data-ttu-id="c9150-281">(Jeśli konwerter niestandardowy nie jest dostępny, `JsonException` wyjątek jest zgłaszany przez wewnętrzny konwerter typu).</span><span class="sxs-lookup"><span data-stu-id="c9150-281">(If no custom converter is available, a `JsonException` exception is thrown by the internal converter for the type.)</span></span>

<span data-ttu-id="c9150-282">To zachowanie obsługi wartości null polega głównie na optymalizowaniu wydajności przez pominięcie dodatkowego wywołania do konwertera.</span><span class="sxs-lookup"><span data-stu-id="c9150-282">This null-handling behavior is primarily to optimize performance by skipping an extra call to the converter.</span></span> <span data-ttu-id="c9150-283">Ponadto pozwala to uniknąć wymuszania konwerterów dla typów dopuszczających wartość null do sprawdzenia na `null` początku każdego `Read` i `Write` przesłonięcia metody.</span><span class="sxs-lookup"><span data-stu-id="c9150-283">In addition, it avoids forcing converters for nullable types to check for `null` at the start of every `Read` and `Write` method override.</span></span>

::: zone pivot="dotnet-5-0"
<span data-ttu-id="c9150-284">Aby włączyć obsługę niestandardowego konwertera `null` dla typu odwołania lub wartości, Przesłoń <xref:System.Text.Json.Serialization.JsonConverter%601.HandleNull%2A?displayProperty=nameWithType> to Return `true` , jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="c9150-284">To enable a custom converter to handle `null` for a reference or value type, override <xref:System.Text.Json.Serialization.JsonConverter%601.HandleNull%2A?displayProperty=nameWithType> to return `true`, as shown in the following example:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/CustomConverterHandleNull.cs" highlight="18":::
::: zone-end

## <a name="other-custom-converter-samples"></a><span data-ttu-id="c9150-285">Inne przykłady konwerterów niestandardowych</span><span class="sxs-lookup"><span data-stu-id="c9150-285">Other custom converter samples</span></span>

<span data-ttu-id="c9150-286">[Migracja z Newtonsoft.Json do System.Text.Json ](system-text-json-migrate-from-newtonsoft-how-to.md) artykułu zawiera dodatkowe przykłady konwerterów niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="c9150-286">The [Migrate from Newtonsoft.Json to System.Text.Json](system-text-json-migrate-from-newtonsoft-how-to.md) article contains additional samples of custom converters.</span></span>

<span data-ttu-id="c9150-287">[Folder testów jednostkowych](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/) w `System.Text.Json.Serialization` kodzie źródłowym zawiera inne przykłady niestandardowego konwertera, takie jak:</span><span class="sxs-lookup"><span data-stu-id="c9150-287">The [unit tests folder](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/) in the `System.Text.Json.Serialization` source code includes other custom converter samples, such as:</span></span>

* <span data-ttu-id="c9150-288">[Konwerter Int32, który konwertuje wartość null na wartość 0 podczas deserializacji](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/CustomConverterTests.NullValueType.cs)</span><span class="sxs-lookup"><span data-stu-id="c9150-288">[Int32 converter that converts null to 0 on deserialize](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/CustomConverterTests.NullValueType.cs)</span></span>
* <span data-ttu-id="c9150-289">[Konwerter Int32, który zezwala na wartości typu String i Number przy deserializacji](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/CustomConverterTests.Int32.cs)</span><span class="sxs-lookup"><span data-stu-id="c9150-289">[Int32 converter that allows both string and number values on deserialize](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/CustomConverterTests.Int32.cs)</span></span>
* <span data-ttu-id="c9150-290">[Konwerter wyliczenia](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/CustomConverterTests.Enum.cs)</span><span class="sxs-lookup"><span data-stu-id="c9150-290">[Enum converter](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/CustomConverterTests.Enum.cs)</span></span>
* <span data-ttu-id="c9150-291">[\<T>Konwerter listy akceptujący dane zewnętrzne](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/CustomConverterTests.List.cs)</span><span class="sxs-lookup"><span data-stu-id="c9150-291">[List\<T> converter that accepts external data](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/CustomConverterTests.List.cs)</span></span>
* <span data-ttu-id="c9150-292">[Długi konwerter [], który działa z rozdzielaną przecinkami listą liczb](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/CustomConverterTests.Array.cs)</span><span class="sxs-lookup"><span data-stu-id="c9150-292">[Long[] converter that works with a comma-delimited list of numbers](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/CustomConverterTests.Array.cs)</span></span>

<span data-ttu-id="c9150-293">Jeśli musisz utworzyć konwerter, który modyfikuje zachowanie istniejącego wbudowanego konwertera, możesz uzyskać [kod źródłowy istniejącego konwertera](https://github.com/dotnet/runtime/tree/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/src/System/Text/Json/Serialization/Converters) , który będzie używany jako punkt wyjścia do dostosowania.</span><span class="sxs-lookup"><span data-stu-id="c9150-293">If you need to make a converter that modifies the behavior of an existing built-in converter, you can get [the source code of the existing converter](https://github.com/dotnet/runtime/tree/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/src/System/Text/Json/Serialization/Converters) to serve as a starting point for customization.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c9150-294">Zasoby dodatkowe</span><span class="sxs-lookup"><span data-stu-id="c9150-294">Additional resources</span></span>

* <span data-ttu-id="c9150-295">[Kod źródłowy wbudowanych konwerterów](https://github.com/dotnet/runtime/tree/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/src/System/Text/Json/Serialization/Converters)</span><span class="sxs-lookup"><span data-stu-id="c9150-295">[Source code for built-in converters](https://github.com/dotnet/runtime/tree/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/src/System/Text/Json/Serialization/Converters)</span></span>
* [<span data-ttu-id="c9150-296">System.Text.Json Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="c9150-296">System.Text.Json overview</span></span>](system-text-json-overview.md)
* [<span data-ttu-id="c9150-297">Jak serializować i deserializować dane JSON</span><span class="sxs-lookup"><span data-stu-id="c9150-297">How to serialize and deserialize JSON</span></span>](system-text-json-how-to.md)
* [<span data-ttu-id="c9150-298">Tworzenie wystąpienia JsonSerializerOptions wystąpień</span><span class="sxs-lookup"><span data-stu-id="c9150-298">Instantiate JsonSerializerOptions instances</span></span>](system-text-json-configure-options.md)
* [<span data-ttu-id="c9150-299">Włączanie dopasowywania bez uwzględniania wielkości liter</span><span class="sxs-lookup"><span data-stu-id="c9150-299">Enable case-insensitive matching</span></span>](system-text-json-character-casing.md)
* [<span data-ttu-id="c9150-300">Dostosowywanie nazw i wartości właściwości</span><span class="sxs-lookup"><span data-stu-id="c9150-300">Customize property names and values</span></span>](system-text-json-customize-properties.md)
* [<span data-ttu-id="c9150-301">Ignorowanie właściwości</span><span class="sxs-lookup"><span data-stu-id="c9150-301">Ignore properties</span></span>](system-text-json-ignore-properties.md)
* [<span data-ttu-id="c9150-302">Zezwalanie na nieprawidłowy kod JSON</span><span class="sxs-lookup"><span data-stu-id="c9150-302">Allow invalid JSON</span></span>](system-text-json-invalid-json.md)
* [<span data-ttu-id="c9150-303">Obsługa przepełnienia kodu JSON</span><span class="sxs-lookup"><span data-stu-id="c9150-303">Handle overflow JSON</span></span>](system-text-json-handle-overflow.md)
* [<span data-ttu-id="c9150-304">Zachowywanie odwołań</span><span class="sxs-lookup"><span data-stu-id="c9150-304">Preserve references</span></span>](system-text-json-preserve-references.md)
* [<span data-ttu-id="c9150-305">Niemodyfikowalne typy i niepubliczne metody dostępu</span><span class="sxs-lookup"><span data-stu-id="c9150-305">Immutable types and non-public accessors</span></span>](system-text-json-immutability.md)
* [<span data-ttu-id="c9150-306">Serializacja polimorficzna</span><span class="sxs-lookup"><span data-stu-id="c9150-306">Polymorphic serialization</span></span>](system-text-json-polymorphism.md)
* [<span data-ttu-id="c9150-307">Migruj z Newtonsoft.Json do System.Text.Json</span><span class="sxs-lookup"><span data-stu-id="c9150-307">Migrate from Newtonsoft.Json to System.Text.Json</span></span>](system-text-json-migrate-from-newtonsoft-how-to.md)
* [<span data-ttu-id="c9150-308">Dostosowywanie kodowania znaków</span><span class="sxs-lookup"><span data-stu-id="c9150-308">Customize character encoding</span></span>](system-text-json-character-encoding.md)
* [<span data-ttu-id="c9150-309">Napisz niestandardowe serializatory i deserializatory</span><span class="sxs-lookup"><span data-stu-id="c9150-309">Write custom serializers and deserializers</span></span>](write-custom-serializer-deserializer.md)
* [<span data-ttu-id="c9150-310">Obsługa wartości DateTime i DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="c9150-310">DateTime and DateTimeOffset support</span></span>](../datetime/system-text-json-support.md)
* <span data-ttu-id="c9150-311">[System.Text.Json Dokumentacja interfejsu API](xref:System.Text.Json)</span><span class="sxs-lookup"><span data-stu-id="c9150-311">[System.Text.Json API reference](xref:System.Text.Json)</span></span>
* <span data-ttu-id="c9150-312">[System.Text.Json. Dokumentacja interfejsu API serializacji](xref:System.Text.Json.Serialization)</span><span class="sxs-lookup"><span data-stu-id="c9150-312">[System.Text.Json.Serialization API reference](xref:System.Text.Json.Serialization)</span></span>
