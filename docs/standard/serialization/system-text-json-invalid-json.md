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
ms.openlocfilehash: 1b6402952c4765290d22b530834ed831a68bd2fe
ms.sourcegitcommit: 45c7148f2483db2501c1aa696ab6ed2ed8cb71b2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/08/2020
ms.locfileid: "96851246"
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

Na przykład:

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

## <a name="see-also"></a>Zobacz też

* [System.Text.Json Podsumowanie](system-text-json-overview.md)
* [Tworzenie wystąpienia JsonSerializerOptions](system-text-json-configure-options.md)
* [Włączanie dopasowywania bez uwzględniania wielkości liter](system-text-json-character-casing.md)
* [Dostosowywanie nazw i wartości właściwości](system-text-json-customize-properties.md)
* [Ignorowanie właściwości](system-text-json-ignore-properties.md)
* [Obsługa przepełnienia kodu JSON](system-text-json-handle-overflow.md)
* [Zachowaj odwołania cykliczne](system-text-json-preserve-references.md)
* [Niemodyfikowalne typy i niepubliczne metody dostępu](system-text-json-immutability.md)
* [Serializacja polimorficzna](system-text-json-polymorphism.md)
* [System.Text.Json Dokumentacja interfejsu API](xref:System.Text.Json)
