---
title: Jak serializować właściwości klas pochodnych przy użyciu System.Text.Json
description: Dowiedz się, jak serializować obiekty polimorficzne podczas serializacji do i deserializacji z JSON w programie .NET.
ms.date: 11/30/2020
no-loc:
- System.Text.Json
- Newtonsoft.Json
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
ms.openlocfilehash: c0bc16c60d3bf96a380bc29bbf7f4765f752b320
ms.sourcegitcommit: 81f1bba2c97a67b5ca76bcc57b37333ffca60c7b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/10/2020
ms.locfileid: "97008750"
---
# <a name="how-to-serialize-properties-of-derived-classes-with-no-locsystemtextjson"></a>Jak serializować właściwości klas pochodnych przy użyciu System.Text.Json

W tym artykule dowiesz się, jak serializować właściwości klas pochodnych z `System.Text.Json` przestrzenią nazw.

## <a name="serialize-properties-of-derived-classes"></a>Serializowanie właściwości klas pochodnych

Serializacja hierarchii typów polimorficznych _nie_ jest obsługiwana. Na przykład, jeśli właściwość jest zdefiniowana jako interfejs lub Klasa abstrakcyjna, tylko właściwości zdefiniowane w interfejsie lub klasie abstrakcyjnej są serializowane, nawet jeśli typ środowiska uruchomieniowego ma dodatkowe właściwości. Wyjątki dotyczące tego zachowania zostały omówione w tej sekcji.

Załóżmy na przykład, że masz `WeatherForecast` klasę i klasę pochodną `WeatherForecastDerived` :

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WF":::

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFDerived":::

I Załóżmy, że argument typu `Serialize` metody w czasie kompilacji to `WeatherForecast` :

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/SerializePolymorphic.cs" id="SerializeDefault":::

W tym scenariuszu `WindSpeed` Właściwość nie jest serializowana, nawet jeśli `weatherForecast` obiekt jest rzeczywiście `WeatherForecastDerived` obiektem. Tylko właściwości klasy bazowej są serializowane:

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot"
}
```

Takie zachowanie ma na celu zapobieganie przypadkowemu narażeniu danych w pochodnym typie tworzonym przez środowisko uruchomieniowe.

Aby serializować właściwości typu pochodnego w poprzednim przykładzie, należy użyć jednej z następujących metod:

* Wywołaj Przeciążenie <xref:System.Text.Json.JsonSerializer.Serialize%2A> , które pozwala określić typ w czasie wykonywania:

  :::code language="csharp" source="snippets/system-text-json-how-to/csharp/SerializePolymorphic.cs" id="SerializeGetType":::

* Zadeklaruj obiekt, który ma zostać Zserializowany jako `object` .

  :::code language="csharp" source="snippets/system-text-json-how-to/csharp/SerializePolymorphic.cs" id="SerializeObject":::

W poprzednim przykładowym scenariuszu oba podejścia powodują, że `WindSpeed` Właściwość powinna zostać uwzględniona w danych wyjściowych JSON:

```json
{
  "WindSpeed": 35,
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot"
}
```

> [!IMPORTANT]
> Te podejścia zapewniają serializację polimorficzne tylko dla obiektu głównego, który ma być serializowany, a nie dla właściwości tego obiektu głównego.

Można uzyskać serializację polimorficzny dla obiektów niższego poziomu, jeśli zdefiniujesz je jako typ `object` . Na przykład załóżmy, `WeatherForecast` że Klasa ma właściwość o nazwie `PreviousForecast` , która może być zdefiniowana jako typ `WeatherForecast` lub `object` :

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithPrevious":::

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithPreviousAsObject":::

Jeśli `PreviousForecast` Właściwość zawiera wystąpienie `WeatherForecastDerived` :

* Dane wyjściowe JSON z serializacji `WeatherForecastWithPrevious` **nie obejmują** `WindSpeed` .
* Dane wyjściowe JSON z serializacji `WeatherForecastWithPreviousAsObject` **obejmują** `WindSpeed` .

Aby serializować `WeatherForecastWithPreviousAsObject` , nie jest konieczne wywołanie `Serialize<object>` lub `GetType` ponieważ obiekt główny nie jest tym, który może znajdować się w typie pochodnym. Poniższy przykład kodu nie wywołuje `Serialize<object>` lub `GetType` :

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/SerializePolymorphic.cs" id="SerializeSecondLevel":::

Powyższy kod poprawnie serializować `WeatherForecastWithPreviousAsObject` :

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot",
  "PreviousForecast": {
    "WindSpeed": 35,
    "Date": "2019-08-01T00:00:00-07:00",
    "TemperatureCelsius": 25,
    "Summary": "Hot"
  }
}
```

To samo podejście do definiowania właściwości jako `object` współdziałanie z interfejsami. Załóżmy, że masz następujący interfejs i implementacja, i chcesz serializować klasę o właściwościach zawierających wystąpienia implementacji:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/IForecast.cs":::

Podczas serializacji wystąpienia elementu `Forecasts` , `Tuesday` wyświetlana `WindSpeed` jest tylko właściwość, ponieważ `Tuesday` jest zdefiniowana jako `object` :

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/SerializePolymorphic.cs" id="SerializeInterface":::

Poniższy przykład pokazuje kod JSON, który wynika z poprzedniego kodu:

```json
{
  "Monday": {
    "Date": "2020-01-06T00:00:00-08:00",
    "TemperatureCelsius": 10,
    "Summary": "Cool"
  },
  "Tuesday": {
    "Date": "2020-01-07T00:00:00-08:00",
    "TemperatureCelsius": 11,
    "Summary": "Rainy",
    "WindSpeed": 10
  }
}
```

Aby uzyskać więcej informacji na temat **serializacji** polimorficznej i informacje o **deserializacji**, zobacz [Jak przeprowadzić migrację z Newtonsoft.Json do System.Text.Json](system-text-json-migrate-from-newtonsoft-how-to.md#polymorphic-serialization).

## <a name="see-also"></a>Zobacz także

* [System.Text.Json Podsumowanie](system-text-json-overview.md)
* [Jak serializować i deserializować dane JSON](system-text-json-how-to.md)
* [Tworzenie wystąpienia JsonSerializerOptions wystąpień](system-text-json-configure-options.md)
* [Włączanie dopasowywania bez uwzględniania wielkości liter](system-text-json-character-casing.md)
* [Dostosowywanie nazw i wartości właściwości](system-text-json-customize-properties.md)
* [Ignorowanie właściwości](system-text-json-ignore-properties.md)
* [Zezwalanie na nieprawidłowy kod JSON](system-text-json-invalid-json.md)
* [Obsługa przepełnienia kodu JSON](system-text-json-handle-overflow.md)
* [Zachowywanie odwołań](system-text-json-preserve-references.md)
* [Niemodyfikowalne typy i niepubliczne metody dostępu](system-text-json-immutability.md)
* [Migruj z Newtonsoft.Json do System.Text.Json](system-text-json-migrate-from-newtonsoft-how-to.md)
* [Dostosowywanie kodowania znaków](system-text-json-character-encoding.md)
* [Napisz niestandardowe serializatory i deserializatory](write-custom-serializer-deserializer.md)
* [Zapisz konwertery niestandardowe na potrzeby serializacji JSON](system-text-json-converters-how-to.md)
* [Obsługa wartości DateTime i DateTimeOffset](../datetime/system-text-json-support.md)
* [System.Text.Json Dokumentacja interfejsu API](xref:System.Text.Json)
* [System.Text.Json. Dokumentacja interfejsu API serializacji](xref:System.Text.Json.Serialization)
