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
ms.openlocfilehash: 6d703156d50a3e00a33cea5e15be2df911ed7c1b
ms.sourcegitcommit: 81f1bba2c97a67b5ca76bcc57b37333ffca60c7b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/10/2020
ms.locfileid: "97008815"
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

## <a name="see-also"></a>Zobacz także

* [System.Text.Json Podsumowanie](system-text-json-overview.md)
* [Jak serializować i deserializować dane JSON](system-text-json-how-to.md)
* [Tworzenie wystąpienia JsonSerializerOptions wystąpień](system-text-json-configure-options.md)
* [Włączanie dopasowywania bez uwzględniania wielkości liter](system-text-json-character-casing.md)
* [Dostosowywanie nazw i wartości właściwości](system-text-json-customize-properties.md)
* [Zezwalanie na nieprawidłowy kod JSON](system-text-json-invalid-json.md)
* [Obsługa przepełnienia kodu JSON](system-text-json-handle-overflow.md)
* [Zachowywanie odwołań](system-text-json-preserve-references.md)
* [Niemodyfikowalne typy i niepubliczne metody dostępu](system-text-json-immutability.md)
* [Serializacja polimorficzna](system-text-json-polymorphism.md)
* [Migruj z Newtonsoft.Json do System.Text.Json](system-text-json-migrate-from-newtonsoft-how-to.md)
* [Dostosowywanie kodowania znaków](system-text-json-character-encoding.md)
* [Napisz niestandardowe serializatory i deserializatory](write-custom-serializer-deserializer.md)
* [Zapisz konwertery niestandardowe na potrzeby serializacji JSON](system-text-json-converters-how-to.md)
* [Obsługa wartości DateTime i DateTimeOffset](../datetime/system-text-json-support.md)
* [System.Text.Json Dokumentacja interfejsu API](xref:System.Text.Json)
* [System.Text.Json. Dokumentacja interfejsu API serializacji](xref:System.Text.Json.Serialization)
