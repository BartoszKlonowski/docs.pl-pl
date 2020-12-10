---
title: Jak zezwolić na niektóre rodzaje nieprawidłowego kodu JSON z System.Text.Json
description: Dowiedz się, jak zezwalać na komentarze, końcowe przecinki i liczby ujęte w cudzysłów podczas serializacji do i deserializacji z formatu JSON w programie .NET.
ms.date: 12/03/2020
no-loc:
- System.Text.Json
- Newtonsoft.Json
zone_pivot_groups: dotnet-version
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
ms.openlocfilehash: 2559b081010fb0a2fa208b121cb095efdeb8da2e
ms.sourcegitcommit: 81f1bba2c97a67b5ca76bcc57b37333ffca60c7b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/10/2020
ms.locfileid: "97009812"
---
# <a name="how-to-allow-some-kinds-of-invalid-json-with-no-locsystemtextjson"></a>Jak zezwolić na niektóre rodzaje nieprawidłowego kodu JSON z System.Text.Json

W tym artykule dowiesz się, jak zezwolić na komentarze, końcowe przecinki i liczby ujęte w cudzysłów w formacie JSON oraz jak pisać liczby jako ciągi.

## <a name="allow-comments-and-trailing-commas"></a>Zezwalaj na komentarze i końcowe przecinki

Domyślnie Komentarze i końcowe przecinki są niedozwolone w notacji JSON. Aby zezwolić na komentarze w formacie JSON, ustaw <xref:System.Text.Json.JsonSerializerOptions.ReadCommentHandling?displayProperty=nameWithType> Właściwość na `JsonCommentHandling.Skip` .
I aby zezwolić na końcowe przecinki, należy ustawić <xref:System.Text.Json.JsonSerializerOptions.AllowTrailingCommas?displayProperty=nameWithType> Właściwość na `true` . Poniższy przykład pokazuje, jak:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/DeserializeCommasComments.cs" id="Deserialize":::

Oto przykładowy kod JSON z komentarzami i końcowym przecinkiem:

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25, // Fahrenheit 77
  "Summary": "Hot", /* Zharko */
  // Comments on
  /* separate lines */
}
```

## <a name="allow-or-write-numbers-in-quotes"></a>Zezwalaj lub zapisuj liczby w cudzysłowach

::: zone pivot="dotnet-5-0"

Niektóre serializatory kodują liczby jako ciągi JSON (ujęte w cudzysłowy).

Przykład:

```json
{
    "DegreesCelsius": "23"
}
```

Zamiast:

```json
{
    "DegreesCelsius": 23
}
```

Aby serializować liczby w cudzysłowach lub zaakceptować liczby cudzysłowów w całym grafie obiektów wejściowych, ustaw <xref:System.Text.Json.JsonSerializerOptions.NumberHandling%2A?displayProperty=nameWithType> jak pokazano w następującym przykładzie:

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/QuotedNumbers.cs" highlight="27-29":::

W przypadku użycia `System.Text.Json` pośrednio za pomocą ASP.NET Core, w przypadku deserializacji są dozwolone liczby ujęte w cudzysłów, ponieważ ASP.NET Core określa [domyślne opcje sieci Web](xref:System.Text.Json.JsonSerializerDefaults.Web).

Aby dopuszczać lub zapisywać liczby ujęte w cudzysłów dla określonych właściwości, pól lub typów, Użyj atrybutu [[JsonNumberHandling]](xref:System.Text.Json.Serialization.JsonNumberHandlingAttribute) .
::: zone-end

::: zone pivot="dotnet-core-3-1"
`System.Text.Json` w programie .NET Core 3,1 nie obsługuje serializacji ani deserializacji numerów ujętych w cudzysłów. Aby uzyskać więcej informacji, zobacz [dopuszczanie lub zapisywanie numerów w cudzysłowach](system-text-json-migrate-from-newtonsoft-how-to.md#allow-or-write-numbers-in-quotes).
::: zone-end

## <a name="see-also"></a>Zobacz także

* [System.Text.Json Podsumowanie](system-text-json-overview.md)
* [Jak serializować i deserializować dane JSON](system-text-json-how-to.md)
* [Tworzenie wystąpienia JsonSerializerOptions wystąpień](system-text-json-configure-options.md)
* [Włączanie dopasowywania bez uwzględniania wielkości liter](system-text-json-character-casing.md)
* [Dostosowywanie nazw i wartości właściwości](system-text-json-customize-properties.md)
* [Ignorowanie właściwości](system-text-json-ignore-properties.md)
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
