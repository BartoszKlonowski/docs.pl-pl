---
title: Jak dostosować nazwy i wartości właściwości przy użyciu System.Text.Json
description: Dowiedz się, jak dostosować nazwy i wartości właściwości podczas serializacji za pomocą programu System.Text.Json .NET.
ms.date: 11/30/2020
no-loc:
- System.Text.Json
- Newtonsoft.Json
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
ms.openlocfilehash: 4b88509313e719ea993e00d889bc6145f4976a2d
ms.sourcegitcommit: 81f1bba2c97a67b5ca76bcc57b37333ffca60c7b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/10/2020
ms.locfileid: "97008906"
---
# <a name="how-to-customize-property-names-and-values-with-no-locsystemtextjson"></a><span data-ttu-id="c450a-103">Jak dostosować nazwy i wartości właściwości przy użyciu System.Text.Json</span><span class="sxs-lookup"><span data-stu-id="c450a-103">How to customize property names and values with System.Text.Json</span></span>

<span data-ttu-id="c450a-104">Domyślnie nazwy właściwości i klucze słownika nie są zmieniane w danych wyjściowych JSON, włącznie z wielkością liter.</span><span class="sxs-lookup"><span data-stu-id="c450a-104">By default, property names and dictionary keys are unchanged in the JSON output, including case.</span></span> <span data-ttu-id="c450a-105">Wartości wyliczeniowe są reprezentowane jako liczby.</span><span class="sxs-lookup"><span data-stu-id="c450a-105">Enum values are represented as numbers.</span></span> <span data-ttu-id="c450a-106">Ten artykuł obejmuje następujące zagadnienia:</span><span class="sxs-lookup"><span data-stu-id="c450a-106">In this article, you'll learn how to:</span></span>

> [!NOTE]
> <span data-ttu-id="c450a-107">[Wartość domyślna w sieci Web](system-text-json-configure-options.md#web-defaults-for-jsonserializeroptions) to notacji CamelCase.</span><span class="sxs-lookup"><span data-stu-id="c450a-107">The [web default](system-text-json-configure-options.md#web-defaults-for-jsonserializeroptions) is camel case.</span></span>

* [<span data-ttu-id="c450a-108">Dostosowywanie poszczególnych nazw właściwości</span><span class="sxs-lookup"><span data-stu-id="c450a-108">Customize individual property names</span></span>](#customize-individual-property-names)
* [<span data-ttu-id="c450a-109">Konwertuj wszystkie nazwy właściwości na notacji CamelCase przypadku</span><span class="sxs-lookup"><span data-stu-id="c450a-109">Convert all property names to camel case</span></span>](#use-camel-case-for-all-json-property-names)
* [<span data-ttu-id="c450a-110">Implementowanie zasad nazewnictwa właściwości niestandardowych</span><span class="sxs-lookup"><span data-stu-id="c450a-110">Implement a custom property naming policy</span></span>](#use-a-custom-json-property-naming-policy)
* [<span data-ttu-id="c450a-111">Konwertuj klucze słownika na notacji CamelCase</span><span class="sxs-lookup"><span data-stu-id="c450a-111">Convert dictionary keys to camel case</span></span>](#camel-case-dictionary-keys)
* [<span data-ttu-id="c450a-112">Konwertuj wyliczenia na ciągi i notacji CamelCase wielkość liter</span><span class="sxs-lookup"><span data-stu-id="c450a-112">Convert enums to strings and camel case</span></span>](#enums-as-strings)

<span data-ttu-id="c450a-113">W przypadku innych scenariuszy, które wymagają specjalnej obsługi nazw i wartości właściwości JSON, można [zaimplementować konwertery niestandardowe](system-text-json-converters-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="c450a-113">For other scenarios that require special handling of JSON property names and values, you can [implement custom converters](system-text-json-converters-how-to.md).</span></span>

## <a name="customize-individual-property-names"></a><span data-ttu-id="c450a-114">Dostosowywanie poszczególnych nazw właściwości</span><span class="sxs-lookup"><span data-stu-id="c450a-114">Customize individual property names</span></span>

<span data-ttu-id="c450a-115">Aby ustawić nazwę poszczególnych właściwości, Użyj atrybutu [[JsonPropertyName]](xref:System.Text.Json.Serialization.JsonPropertyNameAttribute) .</span><span class="sxs-lookup"><span data-stu-id="c450a-115">To set the name of individual properties, use the [[JsonPropertyName]](xref:System.Text.Json.Serialization.JsonPropertyNameAttribute) attribute.</span></span>

<span data-ttu-id="c450a-116">Oto przykład typu do serializacji i powstającego JSON:</span><span class="sxs-lookup"><span data-stu-id="c450a-116">Here's an example type to serialize and resulting JSON:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithPropertyNameAttribute":::

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot",
  "Wind": 35
}
```

<span data-ttu-id="c450a-117">Nazwa właściwości ustawiona przez ten atrybut:</span><span class="sxs-lookup"><span data-stu-id="c450a-117">The property name set by this attribute:</span></span>

* <span data-ttu-id="c450a-118">Stosuje się w obu kierunkach dla serializacji i deserializacji.</span><span class="sxs-lookup"><span data-stu-id="c450a-118">Applies in both directions, for serialization and deserialization.</span></span>
* <span data-ttu-id="c450a-119">Ma pierwszeństwo przed zasadami nazewnictwa właściwości.</span><span class="sxs-lookup"><span data-stu-id="c450a-119">Takes precedence over property naming policies.</span></span>

## <a name="use-camel-case-for-all-json-property-names"></a><span data-ttu-id="c450a-120">Użyj notacji CamelCase przypadku dla wszystkich nazw właściwości JSON</span><span class="sxs-lookup"><span data-stu-id="c450a-120">Use camel case for all JSON property names</span></span>

<span data-ttu-id="c450a-121">Aby użyć notacji CamelCase przypadku wszystkich nazw właściwości JSON, ustaw wartość <xref:System.Text.Json.JsonSerializerOptions.PropertyNamingPolicy?displayProperty=nameWithType> `JsonNamingPolicy.CamelCase` tak, jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="c450a-121">To use camel case for all JSON property names, set <xref:System.Text.Json.JsonSerializerOptions.PropertyNamingPolicy?displayProperty=nameWithType> to `JsonNamingPolicy.CamelCase`, as shown in the following example:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundTripCamelCasePropertyNames.cs" id="Serialize":::

<span data-ttu-id="c450a-122">Oto przykładowa Klasa do serializacji i danych wyjściowych JSON:</span><span class="sxs-lookup"><span data-stu-id="c450a-122">Here's an example class to serialize and JSON output:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithPropertyNameAttribute":::

```json
{
  "date": "2019-08-01T00:00:00-07:00",
  "temperatureCelsius": 25,
  "summary": "Hot",
  "Wind": 35
}
```

<span data-ttu-id="c450a-123">Zasady nazewnictwa właściwości przypadku notacji CamelCase:</span><span class="sxs-lookup"><span data-stu-id="c450a-123">The camel case property naming policy:</span></span>

* <span data-ttu-id="c450a-124">Dotyczy serializacji i deserializacji.</span><span class="sxs-lookup"><span data-stu-id="c450a-124">Applies to serialization and deserialization.</span></span>
* <span data-ttu-id="c450a-125">Jest zastępowany przez `[JsonPropertyName]` atrybuty.</span><span class="sxs-lookup"><span data-stu-id="c450a-125">Is overridden by `[JsonPropertyName]` attributes.</span></span> <span data-ttu-id="c450a-126">Jest to dlatego, że nazwa właściwości JSON `Wind` w przykładzie nie jest notacji CamelCase.</span><span class="sxs-lookup"><span data-stu-id="c450a-126">This is why the JSON property name `Wind` in the example is not camel case.</span></span>

## <a name="use-a-custom-json-property-naming-policy"></a><span data-ttu-id="c450a-127">Użyj niestandardowych zasad nazewnictwa właściwości JSON</span><span class="sxs-lookup"><span data-stu-id="c450a-127">Use a custom JSON property naming policy</span></span>

<span data-ttu-id="c450a-128">Aby użyć niestandardowych zasad nazewnictwa właściwości JSON, Utwórz klasę, która pochodzi od <xref:System.Text.Json.JsonNamingPolicy> i przesłania <xref:System.Text.Json.JsonNamingPolicy.ConvertName%2A> metodę, jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="c450a-128">To use a custom JSON property naming policy, create a class that derives from <xref:System.Text.Json.JsonNamingPolicy> and override the <xref:System.Text.Json.JsonNamingPolicy.ConvertName%2A> method, as shown in the following example:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/UpperCaseNamingPolicy.cs":::

<span data-ttu-id="c450a-129">Następnie ustaw <xref:System.Text.Json.JsonSerializerOptions.PropertyNamingPolicy?displayProperty=nameWithType> Właściwość na wystąpienie klasy zasad nazewnictwa:</span><span class="sxs-lookup"><span data-stu-id="c450a-129">Then set the <xref:System.Text.Json.JsonSerializerOptions.PropertyNamingPolicy?displayProperty=nameWithType> property to an instance of your naming policy class:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripPropertyNamingPolicy.cs" id="Serialize":::

<span data-ttu-id="c450a-130">Oto przykładowa Klasa do serializacji i danych wyjściowych JSON:</span><span class="sxs-lookup"><span data-stu-id="c450a-130">Here's an example class to serialize and JSON output:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithPropertyNameAttribute":::

```json
{
  "DATE": "2019-08-01T00:00:00-07:00",
  "TEMPERATURECELSIUS": 25,
  "SUMMARY": "Hot",
  "Wind": 35
}
```

<span data-ttu-id="c450a-131">Zasady nazewnictwa właściwości JSON:</span><span class="sxs-lookup"><span data-stu-id="c450a-131">The JSON property naming policy:</span></span>

* <span data-ttu-id="c450a-132">Dotyczy serializacji i deserializacji.</span><span class="sxs-lookup"><span data-stu-id="c450a-132">Applies to serialization and deserialization.</span></span>
* <span data-ttu-id="c450a-133">Jest zastępowany przez `[JsonPropertyName]` atrybuty.</span><span class="sxs-lookup"><span data-stu-id="c450a-133">Is overridden by `[JsonPropertyName]` attributes.</span></span> <span data-ttu-id="c450a-134">Jest to dlatego, że nazwa właściwości JSON `Wind` w przykładzie nie jest wielką literą.</span><span class="sxs-lookup"><span data-stu-id="c450a-134">This is why the JSON property name `Wind` in the example is not upper case.</span></span>

## <a name="camel-case-dictionary-keys"></a><span data-ttu-id="c450a-135">Klucze słownika przypadku notacji CamelCase</span><span class="sxs-lookup"><span data-stu-id="c450a-135">Camel case dictionary keys</span></span>

<span data-ttu-id="c450a-136">Jeśli właściwość obiektu, który ma zostać Zserializowany, jest typu `Dictionary<string,TValue>` , `string` klucze mogą być konwertowane na notacji CamelCase przypadku.</span><span class="sxs-lookup"><span data-stu-id="c450a-136">If a property of an object to be serialized is of type `Dictionary<string,TValue>`, the `string` keys can be converted to camel case.</span></span> <span data-ttu-id="c450a-137">W tym celu ustaw wartość <xref:System.Text.Json.JsonSerializerOptions.DictionaryKeyPolicy> `JsonNamingPolicy.CamelCase` , jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="c450a-137">To do that, set <xref:System.Text.Json.JsonSerializerOptions.DictionaryKeyPolicy> to `JsonNamingPolicy.CamelCase`, as shown in the following example:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/SerializeCamelCaseDictionaryKeys.cs" id="Serialize":::

<span data-ttu-id="c450a-138">Serializacja obiektu ze słownikiem o nazwie `TemperatureRanges` , który ma pary klucz-wartość `"ColdMinTemp", 20` i `"HotMinTemp", 40` spowodowałaby wyjście JSON podobne do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="c450a-138">Serializing an object with a dictionary named `TemperatureRanges` that has key-value pairs `"ColdMinTemp", 20` and `"HotMinTemp", 40` would result in JSON output like the following example:</span></span>

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot",
  "TemperatureRanges": {
    "coldMinTemp": 20,
    "hotMinTemp": 40
  }
}
```

<span data-ttu-id="c450a-139">Zasady nazewnictwa przypadków notacji CamelCase dla kluczy słownika mają zastosowanie tylko do serializacji.</span><span class="sxs-lookup"><span data-stu-id="c450a-139">The camel case naming policy for dictionary keys applies to serialization only.</span></span> <span data-ttu-id="c450a-140">W przypadku deserializacji słownika klucze będą zgodne z plikiem JSON nawet w przypadku określenia `JsonNamingPolicy.CamelCase` dla `DictionaryKeyPolicy` .</span><span class="sxs-lookup"><span data-stu-id="c450a-140">If you deserialize a dictionary, the keys will match the JSON file even if you specify `JsonNamingPolicy.CamelCase` for the `DictionaryKeyPolicy`.</span></span>

## <a name="enums-as-strings"></a><span data-ttu-id="c450a-141">Wyliczenia jako ciągi</span><span class="sxs-lookup"><span data-stu-id="c450a-141">Enums as strings</span></span>

<span data-ttu-id="c450a-142">Domyślnie wyliczenia są serializowane jako liczby.</span><span class="sxs-lookup"><span data-stu-id="c450a-142">By default, enums are serialized as numbers.</span></span> <span data-ttu-id="c450a-143">Aby serializować nazwy wyliczenia jako ciągi, użyj <xref:System.Text.Json.Serialization.JsonStringEnumConverter> .</span><span class="sxs-lookup"><span data-stu-id="c450a-143">To serialize enum names as strings, use the <xref:System.Text.Json.Serialization.JsonStringEnumConverter>.</span></span>

<span data-ttu-id="c450a-144">Załóżmy na przykład, że trzeba serializować następujące klasy, które mają Wyliczenie:</span><span class="sxs-lookup"><span data-stu-id="c450a-144">For example, suppose you need to serialize the following class that has an enum:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithEnum":::

<span data-ttu-id="c450a-145">Jeśli podsumowanie jest `Hot` , domyślnie serializowany kod JSON ma wartość liczbową 3:</span><span class="sxs-lookup"><span data-stu-id="c450a-145">If the Summary is `Hot`, by default the serialized JSON has the numeric value 3:</span></span>

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": 3
}
```

<span data-ttu-id="c450a-146">Następujący przykładowy kod serializować nazwy wyliczenia zamiast wartości liczbowych i konwertuje nazwy na notacji CamelCase:</span><span class="sxs-lookup"><span data-stu-id="c450a-146">The following sample code serializes the enum names instead of the numeric values, and converts the names to camel case:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripEnumAsString.cs" id="Serialize":::

<span data-ttu-id="c450a-147">Wynikowy kod JSON wygląda podobnie do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="c450a-147">The resulting JSON looks like the following example:</span></span>

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "hot"
}
```

<span data-ttu-id="c450a-148">Można również deserializować nazwy ciągów wyliczenia, jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="c450a-148">Enum string names can be deserialized as well, as shown in the following example:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripEnumAsString.cs" id="Deserialize":::

## <a name="see-also"></a><span data-ttu-id="c450a-149">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="c450a-149">See also</span></span>

* [<span data-ttu-id="c450a-150">System.Text.Json Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="c450a-150">System.Text.Json overview</span></span>](system-text-json-overview.md)
* [<span data-ttu-id="c450a-151">Jak serializować i deserializować dane JSON</span><span class="sxs-lookup"><span data-stu-id="c450a-151">How to serialize and deserialize JSON</span></span>](system-text-json-how-to.md)
* [<span data-ttu-id="c450a-152">Tworzenie wystąpienia JsonSerializerOptions wystąpień</span><span class="sxs-lookup"><span data-stu-id="c450a-152">Instantiate JsonSerializerOptions instances</span></span>](system-text-json-configure-options.md)
* [<span data-ttu-id="c450a-153">Włączanie dopasowywania bez uwzględniania wielkości liter</span><span class="sxs-lookup"><span data-stu-id="c450a-153">Enable case-insensitive matching</span></span>](system-text-json-character-casing.md)
* [<span data-ttu-id="c450a-154">Ignorowanie właściwości</span><span class="sxs-lookup"><span data-stu-id="c450a-154">Ignore properties</span></span>](system-text-json-ignore-properties.md)
* [<span data-ttu-id="c450a-155">Zezwalanie na nieprawidłowy kod JSON</span><span class="sxs-lookup"><span data-stu-id="c450a-155">Allow invalid JSON</span></span>](system-text-json-invalid-json.md)
* [<span data-ttu-id="c450a-156">Obsługa przepełnienia kodu JSON</span><span class="sxs-lookup"><span data-stu-id="c450a-156">Handle overflow JSON</span></span>](system-text-json-handle-overflow.md)
* [<span data-ttu-id="c450a-157">Zachowywanie odwołań</span><span class="sxs-lookup"><span data-stu-id="c450a-157">Preserve references</span></span>](system-text-json-preserve-references.md)
* [<span data-ttu-id="c450a-158">Niemodyfikowalne typy i niepubliczne metody dostępu</span><span class="sxs-lookup"><span data-stu-id="c450a-158">Immutable types and non-public accessors</span></span>](system-text-json-immutability.md)
* [<span data-ttu-id="c450a-159">Serializacja polimorficzna</span><span class="sxs-lookup"><span data-stu-id="c450a-159">Polymorphic serialization</span></span>](system-text-json-polymorphism.md)
* [<span data-ttu-id="c450a-160">Migruj z Newtonsoft.Json do System.Text.Json</span><span class="sxs-lookup"><span data-stu-id="c450a-160">Migrate from Newtonsoft.Json to System.Text.Json</span></span>](system-text-json-migrate-from-newtonsoft-how-to.md)
* [<span data-ttu-id="c450a-161">Dostosowywanie kodowania znaków</span><span class="sxs-lookup"><span data-stu-id="c450a-161">Customize character encoding</span></span>](system-text-json-character-encoding.md)
* [<span data-ttu-id="c450a-162">Napisz niestandardowe serializatory i deserializatory</span><span class="sxs-lookup"><span data-stu-id="c450a-162">Write custom serializers and deserializers</span></span>](write-custom-serializer-deserializer.md)
* [<span data-ttu-id="c450a-163">Zapisz konwertery niestandardowe na potrzeby serializacji JSON</span><span class="sxs-lookup"><span data-stu-id="c450a-163">Write custom converters for JSON serialization</span></span>](system-text-json-converters-how-to.md)
* [<span data-ttu-id="c450a-164">Obsługa wartości DateTime i DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="c450a-164">DateTime and DateTimeOffset support</span></span>](../datetime/system-text-json-support.md)
* <span data-ttu-id="c450a-165">[System.Text.Json Dokumentacja interfejsu API](xref:System.Text.Json)</span><span class="sxs-lookup"><span data-stu-id="c450a-165">[System.Text.Json API reference](xref:System.Text.Json)</span></span>
* <span data-ttu-id="c450a-166">[System.Text.Json. Dokumentacja interfejsu API serializacji](xref:System.Text.Json.Serialization)</span><span class="sxs-lookup"><span data-stu-id="c450a-166">[System.Text.Json.Serialization API reference](xref:System.Text.Json.Serialization)</span></span>
