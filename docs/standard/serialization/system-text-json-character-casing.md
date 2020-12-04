---
title: Jak włączyć Dopasowywanie nazw właściwości bez uwzględniania wielkości liter System.Text.Json
description: Dowiedz się, jak włączyć Dopasowywanie nazw właściwości bez uwzględniania wielkości liter podczas serializacji do i deserializacji z JSON w programie .NET.
ms.date: 11/30/2020
no-loc:
- System.Text.Json
- Newtonsoft.Json
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
ms.openlocfilehash: 2d663ac8c1c15d61959a62c40d9a3b0993484032
ms.sourcegitcommit: 9d525bb8109216ca1dc9e39c149d4902f4b43da5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2020
ms.locfileid: "96599079"
---
# <a name="how-to-enable-case-insensitive-property-name-matching-with-no-locsystemtextjson"></a>Jak włączyć Dopasowywanie nazw właściwości bez uwzględniania wielkości liter System.Text.Json

W tym artykule dowiesz się, jak włączyć Dopasowywanie nazw właściwości bez uwzględniania wielkości liter w `System.Text.Json` przestrzeni nazw.

## <a name="case-insensitive-property-matching"></a>Dopasowanie właściwości bez uwzględniania wielkości liter

Domyślnie deserializacja wyszukuje dopasowania nazw właściwości z uwzględnieniem wielkości liter między formatem JSON a właściwościami obiektu docelowego. Aby zmienić to zachowanie, ustaw opcję <xref:System.Text.Json.JsonSerializerOptions.PropertyNameCaseInsensitive?displayProperty=nameWithType> na `true` :

> [!NOTE]
> W [domyślnej sieci Web](system-text-json-configure-options.md#web-defaults-for-jsonserializeroptions) nie jest rozróżniana wielkość liter.

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/DeserializeCaseInsensitive.cs" id="Deserialize":::

Oto przykład JSON z nazwami właściwości przypadku notacji CamelCase. Można ją zdeserializować do następującego typu, który ma nazwy właściwości przypadku języka Pascal.

```json
{
  "date": "2019-08-01T00:00:00-07:00",
  "temperatureCelsius": 25,
  "summary": "Hot",
}
```

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WF":::

## <a name="see-also"></a>Zobacz także

* [System.Text.Json Podsumowanie](system-text-json-overview.md)
* [Tworzenie wystąpienia JsonSerializerOptions](system-text-json-configure-options.md)
* [Dostosowywanie nazw i wartości właściwości](system-text-json-customize-properties.md)
* [Ignorowanie właściwości](system-text-json-ignore-properties.md)
* [Zezwalanie na nieprawidłowy kod JSON](system-text-json-invalid-json.md)
* [Obsługa przepełnienia kodu JSON](system-text-json-handle-overflow.md)
* [Zachowaj odwołania cykliczne](system-text-json-preserve-references.md)
* [Niemodyfikowalne typy i niepubliczne metody dostępu](system-text-json-immutability.md)
* [Serializacja polimorficzna](system-text-json-polymorphism.md)
* [System.Text.Json Dokumentacja interfejsu API](xref:System.Text.Json)
