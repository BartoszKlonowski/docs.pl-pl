---
title: Jak zignorować właściwości System.Text.Json
description: Dowiedz się, jak ignorować właściwości podczas serializacji za pomocą programu System.Text.Json .NET.
ms.date: 11/30/2020
no-loc:
- System.Text.Json
- Newtonsoft.Json
zone_pivot_groups: dotnet-version
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
ms.openlocfilehash: ed7ef8509d6660bbbbaf194a87aa9d4815143507
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96439953"
---
# <a name="how-to-ignore-properties-with-no-locsystemtextjson"></a>Jak zignorować właściwości System.Text.Json

Podczas serializacji obiektów C# do JavaScript Object Notation (JSON), domyślnie wszystkie właściwości publiczne są serializowane. Jeśli nie chcesz, aby niektóre z nich były wyświetlane w wynikach JSON, masz kilka opcji. W tym artykule dowiesz się, jak zignorować właściwości na podstawie różnych kryteriów:

::: zone pivot="dotnet-5-0"

* [Poszczególne właściwości](#ignore-individual-properties)
* [Wszystkie właściwości tylko do odczytu](#ignore-all-read-only-properties)
* [Wszystkie właściwości o wartości null](#ignore-all-null-value-properties)
* [Wszystkie właściwości domyślne wartości](#ignore-all-default-value-properties)
::: zone-end

::: zone pivot="dotnet-core-3-1"

* [Poszczególne właściwości](#ignore-individual-properties)
* [Wszystkie właściwości tylko do odczytu](#ignore-all-read-only-properties)
* [Wszystkie właściwości o wartości null](#ignore-all-null-value-properties)
::: zone-end

## <a name="ignore-individual-properties"></a>Ignoruj poszczególne właściwości

Aby zignorować poszczególne właściwości, Użyj atrybutu [[JsonIgnore]](xref:System.Text.Json.Serialization.JsonIgnoreAttribute) .

Oto przykład typu do serializacji i danych wyjściowych JSON:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithIgnoreAttribute":::

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
}
```

::: zone pivot="dotnet-5-0"
Aby określić wykluczenie warunkowe, należy ustawić właściwość [[JsonIgnore]](xref:System.Text.Json.Serialization.JsonIgnoreAttribute) atrybutu `Condition` . <xref:System.Text.Json.Serialization.JsonIgnoreCondition>Wyliczenie zapewnia następujące opcje:

* `Always` -Właściwość jest zawsze ignorowana. Jeśli `Condition` wartość nie jest określona, założono, że ta opcja jest.
* `Never` -Właściwość jest zawsze serializowana i deserializowana, niezależnie od `DefaultIgnoreCondition` `IgnoreReadOnlyProperties` `IgnoreReadOnlyFields` ustawień globalnych, i.
* `WhenWritingDefault` -Właściwość jest ignorowana podczas serializacji, jeśli jest typem referencyjnym `null` , typem wartości null `null` lub typem wartości `default` .
* `WhenWritingNull` -Właściwość jest ignorowana podczas serializacji, jeśli jest typem referencyjnym `null` lub typem wartości null `null` .

Poniższy przykład ilustruje użycie właściwości [[JsonIgnore]](xref:System.Text.Json.Serialization.JsonIgnoreAttribute) atrybutu `Condition` :

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/JsonIgnoreAttributeExample.cs" highlight="10,13,16":::
::: zone-end

## <a name="ignore-all-read-only-properties"></a>Ignoruj wszystkie właściwości tylko do odczytu

Właściwość jest tylko do odczytu, jeśli zawiera publiczną metodę pobierającą, ale nie do publicznej metody ustawiającej. Aby zignorować wszystkie właściwości tylko do odczytu podczas serializacji, ustaw wartość <xref:System.Text.Json.JsonSerializerOptions.IgnoreReadOnlyProperties?displayProperty=nameWithType> na `true` , jak pokazano w następującym przykładzie:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/SerializeExcludeReadOnlyProperties.cs" id="Serialize":::

Oto przykład typu do serializacji i danych wyjściowych JSON:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithROProperty":::

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot",
}
```

Ta opcja ma zastosowanie tylko do serializacji. Podczas deserializacji właściwości tylko do odczytu są domyślnie ignorowane.

::: zone pivot="dotnet-5-0"
Ta opcja ma zastosowanie tylko do właściwości. Aby zignorować pola tylko do odczytu podczas [serializacji pól](system-text-json-how-to.md#include-fields), użyj <xref:System.Text.Json.JsonSerializerOptions.IgnoreReadOnlyFields%2A?displayProperty=nameWithType> Ustawienia globalnego.
::: zone-end

## <a name="ignore-all-null-value-properties"></a>Ignoruj wszystkie właściwości o wartości null

::: zone pivot="dotnet-5-0"
Aby zignorować wszystkie właściwości wartości null, należy ustawić <xref:System.Text.Json.JsonSerializerOptions.DefaultIgnoreCondition> Właściwość na <xref:System.Text.Json.Serialization.JsonIgnoreCondition.WhenWritingNull> , jak pokazano w następującym przykładzie:

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/IgnoreNullOnSerialize.cs" highlight="28":::

::: zone-end

::: zone pivot="dotnet-core-3-1"
Aby ignorować wszystkie właściwości null wartości podczas serializacji, należy ustawić <xref:System.Text.Json.JsonSerializerOptions.IgnoreNullValues> Właściwość na `true` , jak pokazano w następującym przykładzie:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/SerializeExcludeNullValueProperties.cs" id="Serialize":::

Oto przykład obiektu do serializacji i danych wyjściowych JSON:

| Właściwość             | Wartość                         |
|----------------------|-------------------------------|
| `Date`               | `8/1/2019 12:00:00 AM -07:00` |
| `TemperatureCelsius` | `25`                          |
| `Summary`            | `null`                        |

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25
}
```

::: zone-end

## <a name="ignore-all-default-value-properties"></a>Ignoruj wszystkie właściwości domyślne wartości

::: zone pivot="dotnet-5-0"
Aby zapobiec serializacji wartości domyślnych we właściwościach typu wartości, ustaw <xref:System.Text.Json.JsonSerializerOptions.DefaultIgnoreCondition> Właściwość na <xref:System.Text.Json.Serialization.JsonIgnoreCondition.WhenWritingDefault> , jak pokazano w następującym przykładzie:

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/IgnoreValueDefaultOnSerialize.cs" highlight="28":::
::: zone-end

<xref:System.Text.Json.Serialization.JsonIgnoreCondition.WhenWritingDefault>Ustawienie uniemożliwia również serializację typu odwołania o wartości null i właściwości typu wartości null.

::: zone pivot="dotnet-core-3-1"
Nie ma wbudowanego sposobu, aby zapobiec serializacji właściwości z wartościami domyślnymi typu wartości w `System.Text.Json` programie .NET Core 3,1.
::: zone-end

## <a name="see-also"></a>Zobacz też

* [System.Text.Json Podsumowanie](system-text-json-overview.md)
* [Tworzenie wystąpienia JsonSerializerOptions](system-text-json-configure-options.md)
* [Włącz dopasowywanie bez uwzględniania wielkości liter](system-text-json-character-casing.md)
* [Dostosowywanie nazw i wartości właściwości](system-text-json-customize-properties.md)
* [Zezwalaj na nieprawidłowy kod JSON](system-text-json-invalid-json.md)
* [Obsługa przepełnienia kodu JSON](system-text-json-handle-overflow.md)
* [Zachowaj odwołania cykliczne](system-text-json-preserve-references.md)
* [Niemodyfikowalne typy i niepubliczne metody dostępu](system-text-json-immutability.md)
* [Serializacja polimorficzna](system-text-json-polymorphism.md)
* [System.Text.Json Dokumentacja interfejsu API](xref:System.Text.Json)
