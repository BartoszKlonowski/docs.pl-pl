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
ms.openlocfilehash: 28f7d03ae9f794f6e5ea34a95082a059451daec6
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96439983"
---
# <a name="how-to-customize-property-names-and-values-with-no-locsystemtextjson"></a>Jak dostosować nazwy i wartości właściwości przy użyciu System.Text.Json

Domyślnie nazwy właściwości i klucze słownika nie są zmieniane w danych wyjściowych JSON, włącznie z wielkością liter. Wartości wyliczeniowe są reprezentowane jako liczby. Ten artykuł obejmuje następujące zagadnienia:

> [!NOTE]
> [Ustawienia domyślne sieci Web](system-text-json-configure-options.md#web-defaults-for-jsonserializeroptions) to notacji CamelCase.

* [Dostosowywanie poszczególnych nazw właściwości](#customize-individual-property-names)
* [Konwertuj wszystkie nazwy właściwości na notacji CamelCase przypadku](#use-camel-case-for-all-json-property-names)
* [Implementowanie zasad nazewnictwa właściwości niestandardowych](#use-a-custom-json-property-naming-policy)
* [Konwertuj klucze słownika na notacji CamelCase](#camel-case-dictionary-keys)
* [Konwertuj wyliczenia na ciągi i notacji CamelCase wielkość liter](#enums-as-strings)

W przypadku innych scenariuszy, które wymagają specjalnej obsługi nazw i wartości właściwości JSON, można [zaimplementować konwertery niestandardowe](system-text-json-converters-how-to.md).

## <a name="customize-individual-property-names"></a>Dostosowywanie poszczególnych nazw właściwości

Aby ustawić nazwę poszczególnych właściwości, Użyj atrybutu [[JsonPropertyName]](xref:System.Text.Json.Serialization.JsonPropertyNameAttribute) .

Oto przykład typu do serializacji i powstającego JSON:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithPropertyNameAttribute":::

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot",
  "Wind": 35
}
```

Nazwa właściwości ustawiona przez ten atrybut:

* Stosuje się w obu kierunkach dla serializacji i deserializacji.
* Ma pierwszeństwo przed zasadami nazewnictwa właściwości.

## <a name="use-camel-case-for-all-json-property-names"></a>Użyj notacji CamelCase przypadku dla wszystkich nazw właściwości JSON

Aby użyć notacji CamelCase przypadku wszystkich nazw właściwości JSON, ustaw wartość <xref:System.Text.Json.JsonSerializerOptions.PropertyNamingPolicy?displayProperty=nameWithType> `JsonNamingPolicy.CamelCase` tak, jak pokazano w następującym przykładzie:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundTripCamelCasePropertyNames.cs" id="Serialize":::

Oto przykładowa Klasa do serializacji i danych wyjściowych JSON:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithPropertyNameAttribute":::

```json
{
  "date": "2019-08-01T00:00:00-07:00",
  "temperatureCelsius": 25,
  "summary": "Hot",
  "Wind": 35
}
```

Zasady nazewnictwa właściwości przypadku notacji CamelCase:

* Dotyczy serializacji i deserializacji.
* Jest zastępowany przez `[JsonPropertyName]` atrybuty. Jest to dlatego, że nazwa właściwości JSON `Wind` w przykładzie nie jest notacji CamelCase.

## <a name="use-a-custom-json-property-naming-policy"></a>Użyj niestandardowych zasad nazewnictwa właściwości JSON

Aby użyć niestandardowych zasad nazewnictwa właściwości JSON, Utwórz klasę, która pochodzi od <xref:System.Text.Json.JsonNamingPolicy> i przesłania <xref:System.Text.Json.JsonNamingPolicy.ConvertName%2A> metodę, jak pokazano w następującym przykładzie:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/UpperCaseNamingPolicy.cs":::

Następnie ustaw <xref:System.Text.Json.JsonSerializerOptions.PropertyNamingPolicy?displayProperty=nameWithType> Właściwość na wystąpienie klasy zasad nazewnictwa:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripPropertyNamingPolicy.cs" id="Serialize":::

Oto przykładowa Klasa do serializacji i danych wyjściowych JSON:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithPropertyNameAttribute":::

```json
{
  "DATE": "2019-08-01T00:00:00-07:00",
  "TEMPERATURECELSIUS": 25,
  "SUMMARY": "Hot",
  "Wind": 35
}
```

Zasady nazewnictwa właściwości JSON:

* Dotyczy serializacji i deserializacji.
* Jest zastępowany przez `[JsonPropertyName]` atrybuty. Jest to dlatego, że nazwa właściwości JSON `Wind` w przykładzie nie jest wielką literą.

## <a name="camel-case-dictionary-keys"></a>Klucze słownika przypadku notacji CamelCase

Jeśli właściwość obiektu, który ma zostać Zserializowany, jest typu `Dictionary<string,TValue>` , `string` klucze mogą być konwertowane na notacji CamelCase przypadku. W tym celu ustaw wartość <xref:System.Text.Json.JsonSerializerOptions.DictionaryKeyPolicy> `JsonNamingPolicy.CamelCase` , jak pokazano w następującym przykładzie:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/SerializeCamelCaseDictionaryKeys.cs" id="Serialize":::

Serializacja obiektu ze słownikiem o nazwie `TemperatureRanges` , który ma pary klucz-wartość `"ColdMinTemp", 20` i `"HotMinTemp", 40` spowodowałaby wyjście JSON podobne do poniższego przykładu:

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

Zasady nazewnictwa przypadków notacji CamelCase dla kluczy słownika mają zastosowanie tylko do serializacji. W przypadku deserializacji słownika klucze będą zgodne z plikiem JSON nawet w przypadku określenia `JsonNamingPolicy.CamelCase` dla `DictionaryKeyPolicy` .

## <a name="enums-as-strings"></a>Wyliczenia jako ciągi

Domyślnie wyliczenia są serializowane jako liczby. Aby serializować nazwy wyliczenia jako ciągi, użyj <xref:System.Text.Json.Serialization.JsonStringEnumConverter> .

Załóżmy na przykład, że trzeba serializować następujące klasy, które mają Wyliczenie:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithEnum":::

Jeśli podsumowanie jest `Hot` , domyślnie serializowany kod JSON ma wartość liczbową 3:

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": 3
}
```

Następujący przykładowy kod serializować nazwy wyliczenia zamiast wartości liczbowych i konwertuje nazwy na notacji CamelCase:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripEnumAsString.cs" id="Serialize":::

Wynikowy kod JSON wygląda podobnie do poniższego przykładu:

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "hot"
}
```

Można również deserializować nazwy ciągów wyliczenia, jak pokazano w następującym przykładzie:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripEnumAsString.cs" id="Deserialize":::

## <a name="see-also"></a>Zobacz też

* [System.Text.Json Podsumowanie](system-text-json-overview.md)
* [Tworzenie wystąpienia JsonSerializerOptions](system-text-json-configure-options.md)
* [Włącz dopasowywanie bez uwzględniania wielkości liter](system-text-json-character-casing.md)
* [Ignoruj właściwości](system-text-json-ignore-properties.md)
* [Zezwalaj na nieprawidłowy kod JSON](system-text-json-invalid-json.md)
* [Obsługa przepełnienia kodu JSON](system-text-json-handle-overflow.md)
* [Zachowaj odwołania cykliczne](system-text-json-preserve-references.md)
* [Niemodyfikowalne typy i niepubliczne metody dostępu](system-text-json-immutability.md)
* [Serializacja polimorficzna](system-text-json-polymorphism.md)
* [System.Text.Json Dokumentacja interfejsu API](xref:System.Text.Json)
