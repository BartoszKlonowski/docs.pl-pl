---
title: Jak serializować i deserializować kod JSON przy użyciu języka C# — .NET
description: Dowiedz się, jak używać System.Text.Json przestrzeni nazw do serializacji i deserializacji z JSON w programie .NET. Zawiera przykładowy kod.
ms.date: 12/16/2020
ms.custom: contperf-fy21q2
no-loc:
- System.Text.Json
- Newtonsoft.Json
zone_pivot_groups: dotnet-version
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
ms.openlocfilehash: b69dfd6238f529c3b315d63a93a82da0f316f459
ms.sourcegitcommit: 4b79862c5b41fbd86cf38f926f6a49516059f6f2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/18/2020
ms.locfileid: "97678255"
---
# <a name="how-to-serialize-and-deserialize-marshal-and-unmarshal-json-in-net"></a>Jak serializować i deserializować (Marshaling and unmarshaling) JSON w programie .NET

W tym artykule pokazano, jak używać <xref:System.Text.Json?displayProperty=fullName> przestrzeni nazw do serializacji i deserializacji z JavaScript Object Notation (JSON). W przypadku przenoszenia istniejącego kodu z programu `Newtonsoft.Json` zapoznaj się z tematem [jak `System.Text.Json` przeprowadzić migrację do programu ](system-text-json-migrate-from-newtonsoft-how-to.md).

Instrukcje i przykładowy kod używają biblioteki bezpośrednio, a nie za pomocą struktury, takiej jak [ASP.NET Core](/aspnet/core/).

Większość przykładowych kodów serializacji <xref:System.Text.Json.JsonSerializerOptions.WriteIndented?displayProperty=nameWithType> do `true` "DB-Print" w formacie JSON (z wcięciem i białym znakiem). Do użycia w środowisku produkcyjnym zwykle przyjmuje się wartość domyślną `false` dla tego ustawienia.

Przykłady kodu odnoszą się do następującej klasy i wariantów:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WF":::

## <a name="namespaces"></a>Przestrzenie nazw

<xref:System.Text.Json>Przestrzeń nazw zawiera wszystkie punkty wejścia i typy główne. <xref:System.Text.Json.Serialization>Przestrzeń nazw zawiera atrybuty i interfejsy API dla zaawansowanych scenariuszy i dostosowań specyficznych dla serializacji i deserializacji. Przykłady kodu przedstawione w tym artykule wymagają `using` dyrektyw dla jednej lub obu tych przestrzeni nazw:

```csharp
using System.Text.Json;
using System.Text.Json.Serialization;
```

> [!IMPORTANT]
> Atrybuty z <xref:System.Runtime.Serialization> przestrzeni nazw nie są obsługiwane w programie `System.Text.Json` .

## <a name="how-to-write-net-objects-as-json-serialize"></a>Jak pisać obiekty .NET jako dane JSON (serializować)

Aby zapisać dane JSON do ciągu lub do pliku, wywołaj <xref:System.Text.Json.JsonSerializer.Serialize%2A?displayProperty=nameWithType> metodę.

Poniższy przykład tworzy kod JSON jako ciąg:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripToString.cs" id="Serialize":::

Poniższy przykład używa kodu synchronicznego do utworzenia pliku JSON:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripToFile.cs" id="Serialize":::

W poniższym przykładzie jest tworzony plik JSON przy użyciu kodu asynchronicznego:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripToFileAsync.cs" id="Serialize":::

Powyższe przykłady używają wnioskowania typu dla serializowanego typu. Przeciążenie `Serialize()` przyjmuje parametr typu ogólnego:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripToString.cs" id="SerializeWithGenericParameter":::

### <a name="serialization-example"></a>Przykład serializacji

Oto przykładowa Klasa, która zawiera właściwości typu kolekcji i typ zdefiniowany przez użytkownika:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithPOCOs":::

> [!TIP]
> "POCO" oznacza dla [zwykłego starego obiektu CLR](https://en.wikipedia.org/wiki/Plain_old_CLR_object). POCO to typ .NET, który nie jest zależny od żadnych typów specyficznych dla platformy, na przykład przez dziedziczenie lub atrybuty.

Dane wyjściowe JSON serializowania wystąpienia poprzedniego typu wyglądają podobnie jak w poniższym przykładzie. Dane wyjściowe JSON to zminimalizowanego (odstępy, wcięcia i znaki nowego wiersza są domyślnie usuwane):

```json
{"Date":"2019-08-01T00:00:00-07:00","TemperatureCelsius":25,"Summary":"Hot","DatesAvailable":["2019-08-01T00:00:00-07:00","2019-08-02T00:00:00-07:00"],"TemperatureRanges":{"Cold":{"High":20,"Low":-10},"Hot":{"High":60,"Low":20}},"SummaryWords":["Cool","Windy","Humid"]}
```

W poniższym przykładzie przedstawiono ten sam kod JSON, ale sformatowany (to jest, całkiem wydruk z odstępami i wcięciami):

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot",
  "DatesAvailable": [
    "2019-08-01T00:00:00-07:00",
    "2019-08-02T00:00:00-07:00"
  ],
  "TemperatureRanges": {
    "Cold": {
      "High": 20,
      "Low": -10
    },
    "Hot": {
      "High": 60,
      "Low": 20
    }
  },
  "SummaryWords": [
    "Cool",
    "Windy",
    "Humid"
  ]
}
```

## <a name="serialize-to-utf-8"></a>Serializacja do UTF-8

Aby serializować do UTF-8, wywołaj <xref:System.Text.Json.JsonSerializer.SerializeToUtf8Bytes%2A?displayProperty=nameWithType> metodę:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripToUtf8.cs" id="Serialize":::

<xref:System.Text.Json.JsonSerializer.Serialize%2A>Dostępne jest również Przeciążenie, które trwa <xref:System.Text.Json.Utf8JsonWriter> .

Serializacja do UTF-8 jest szybsza o 5-10% niż przy użyciu metod opartych na ciągach. Różnica polega na tym, że bajty (w formacie UTF-8) nie muszą być konwertowane na ciągi (UTF-16).

## <a name="serialization-behavior"></a>Zachowanie serializacji

::: zone pivot="dotnet-5-0"

* Domyślnie wszystkie właściwości publiczne są serializowane. Można [określić właściwości do ignorowania](system-text-json-ignore-properties.md).
* [Domyślny koder](xref:System.Text.Encodings.Web.JavaScriptEncoder.Default) wyprowadza znaki nienależące do zestawu znaków ASCII, znaki z uwzględnieniem języka HTML w zakresie ASCII i znaków, które muszą zostać zmienione zgodnie z [specyfikacją JSON RFC 8259](https://tools.ietf.org/html/rfc8259#section-7).
* Domyślnie JSON jest zminimalizowanego. Można tu [wydrukować kod JSON](#serialize-to-formatted-json).
* Domyślnie wielkość liter w nazwach JSON jest zgodna z nazwami .NET. Można [dostosować wielkość liter w nazwach JSON](system-text-json-customize-properties.md).
* Domyślnie wykryto odwołania cykliczne i zostały zgłoszone wyjątki. Można [zachować odwołania i obsłużyć odwołania cykliczne](system-text-json-preserve-references.md).
* Domyślnie [pola](../../csharp/programming-guide/classes-and-structs/fields.md) są ignorowane. Możesz [dołączyć pola](#include-fields).

Jeśli używasz System.Text.Json bezpośrednio w aplikacji ASP.NET Core, niektóre domyślne zachowania są inne. Aby uzyskać więcej informacji, zobacz [Ustawienia domyślne sieci Web dla JsonSerializerOptions](system-text-json-configure-options.md#web-defaults-for-jsonserializeroptions).
::: zone-end

::: zone pivot="dotnet-core-3-1"

* Domyślnie wszystkie właściwości publiczne są serializowane. Można [określić właściwości do ignorowania](system-text-json-ignore-properties.md).
* [Domyślny koder](xref:System.Text.Encodings.Web.JavaScriptEncoder.Default) wyprowadza znaki nienależące do zestawu znaków ASCII, znaki z uwzględnieniem języka HTML w zakresie ASCII i znaków, które muszą zostać zmienione zgodnie z [specyfikacją JSON RFC 8259](https://tools.ietf.org/html/rfc8259#section-7).
* Domyślnie JSON jest zminimalizowanego. Można tu [wydrukować kod JSON](#serialize-to-formatted-json).
* Domyślnie wielkość liter w nazwach JSON jest zgodna z nazwami .NET. Można [dostosować wielkość liter w nazwach JSON](system-text-json-customize-properties.md).
* Wykryto odwołania cykliczne i zostały zgłoszone wyjątki.
* [Pola](../../csharp/programming-guide/classes-and-structs/fields.md) są ignorowane.
::: zone-end

Obsługiwane typy to:
::: zone pivot="dotnet-5-0"

* Elementy podstawowe platformy .NET, które są mapowane na elementy podstawowe języka JavaScript, takie jak typy liczbowe, ciągi i wartości logiczne.
* Obiekty CLR zdefiniowane przez użytkownika [(POCOs)](https://en.wikipedia.org/wiki/Plain_old_CLR_object).
* Tablice jednowymiarowe i nieregularne ( `T[][]` ).
* Kolekcje i słowniki z następujących przestrzeni nazw.
  * <xref:System.Collections>
  * <xref:System.Collections.Generic>
  * <xref:System.Collections.Immutable>
  * <xref:System.Collections.Concurrent>
  * <xref:System.Collections.Specialized>
  * <xref:System.Collections.ObjectModel>
::: zone-end

::: zone pivot="dotnet-core-3-1"

* Elementy podstawowe platformy .NET, które są mapowane na elementy podstawowe języka JavaScript, takie jak typy liczbowe, ciągi i wartości logiczne.
* Obiekty CLR zdefiniowane przez użytkownika [(POCOs)](https://en.wikipedia.org/wiki/Plain_old_CLR_object).
* Tablice jednowymiarowe i nieregularne ( `ArrayName[][]` ).
* `Dictionary<string,TValue>` gdzie `TValue` is to `object` , `JsonElement` lub poco.
* Kolekcje z następujących przestrzeni nazw.
  * <xref:System.Collections>
  * <xref:System.Collections.Generic>
  * <xref:System.Collections.Immutable>
  * <xref:System.Collections.Concurrent>
  * <xref:System.Collections.Specialized>
  * <xref:System.Collections.ObjectModel>
::: zone-end

Można [zaimplementować niestandardowe konwertery](system-text-json-converters-how-to.md) w celu obsługi dodatkowych typów lub zapewnienia funkcjonalności, która nie jest obsługiwana przez wbudowane konwertery.

## <a name="how-to-read-json-as-net-objects-deserialize"></a>Jak odczytać dane JSON jako obiekty .NET (deserializacji)

Aby zdeserializować z ciągu lub pliku, wywołaj <xref:System.Text.Json.JsonSerializer.Deserialize%2A?displayProperty=nameWithType> metodę.

Poniższy przykład odczytuje dane JSON z ciągu i tworzy wystąpienie `WeatherForecastWithPOCOs` klasy pokazanej wcześniej dla [przykładu serializacji](#serialization-example):

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripToString.cs" id="Deserialize":::

Aby zdeserializować z pliku przy użyciu kodu synchronicznego, Odczytaj plik do ciągu, jak pokazano w następującym przykładzie:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripToFile.cs" id="Deserialize":::

Aby zdeserializować z pliku przy użyciu kodu asynchronicznego, wywołaj <xref:System.Text.Json.JsonSerializer.DeserializeAsync%2A> metodę:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripToFileAsync.cs" id="Deserialize":::

> [!TIP]
> Jeśli masz kod JSON, który chcesz zdeserializować i nie masz klasy do deserializacji, w programie Visual Studio 2019 można automatycznie wygenerować klasę, której potrzebujesz:
>
> 1. Skopiuj kod JSON, który ma być niezbędny do deserializacji.
> 1. Utwórz plik klasy i Usuń kod szablonu.
> 1. Wybierz pozycję **Edytuj**  >  **Wklej specjalne**  >  **Wklej dane JSON jako klasy**.
>
> Wynik jest klasą, której można użyć dla celu deserializacji.

## <a name="deserialize-from-utf-8"></a>Deserializacja z UTF-8

Aby zdeserializować z UTF-8, wywołaj <xref:System.Text.Json.JsonSerializer.Deserialize%2A?displayProperty=nameWithType> Przeciążenie, które pobiera `ReadOnlySpan<byte>` lub a `Utf8JsonReader` , jak pokazano w poniższych przykładach. W przykładach założono, że kod JSON znajduje się w tablicy bajtów o nazwie jsonUtf8Bytes.

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripToUtf8.cs" id="Deserialize1":::

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripToUtf8.cs" id="Deserialize2":::

## <a name="deserialization-behavior"></a>Zachowanie deserializacji

Podczas deserializacji kodu JSON stosowane są następujące zachowania:

::: zone pivot="dotnet-5-0"

* Domyślnie w dopasowaniu nazw właściwości rozróżniana jest wielkość liter. Można [określić wielkość liter](system-text-json-character-casing.md).
* Jeśli kod JSON zawiera wartość właściwości tylko do odczytu, wartość jest ignorowana i nie jest zgłaszany żaden wyjątek.
* Konstruktory niepubliczne są ignorowane przez serializator.
* Obsługa deserializacji do niemodyfikowalnych obiektów lub właściwości tylko do odczytu jest obsługiwana. Zobacz [zmienne typy i rekordy](system-text-json-immutability.md).
* Domyślnie wyliczenia są obsługiwane jako liczby. [Nazwy wyliczenia można serializować jako ciągi](system-text-json-customize-properties.md#enums-as-strings).
* Domyślnie pola są ignorowane. Możesz [dołączyć pola](#include-fields).
* Domyślnie komentarze lub końcowe przecinki w wyjątkach throw JSON. Można [zezwolić na komentarze i końcowe przecinki](system-text-json-invalid-json.md).
* [Domyślna głębokość maksymalna](xref:System.Text.Json.JsonReaderOptions.MaxDepth) to 64.

Jeśli używasz System.Text.Json bezpośrednio w aplikacji ASP.NET Core, niektóre domyślne zachowania są inne. Aby uzyskać więcej informacji, zobacz [Ustawienia domyślne sieci Web dla JsonSerializerOptions](system-text-json-configure-options.md#web-defaults-for-jsonserializeroptions).
::: zone-end

::: zone pivot="dotnet-core-3-1"

* Domyślnie w dopasowaniu nazw właściwości rozróżniana jest wielkość liter. Można [określić wielkość liter](system-text-json-character-casing.md). Aplikacje ASP.NET Core [Domyślnie określają wielkość liter](system-text-json-configure-options.md#web-defaults-for-jsonserializeroptions).
* Jeśli kod JSON zawiera wartość właściwości tylko do odczytu, wartość jest ignorowana i nie jest zgłaszany żaden wyjątek.
* Konstruktor bez parametrów, który może być publiczny, wewnętrzny lub prywatny, jest używany do deserializacji.
* Deserializacja z niezmiennymi obiektami lub właściwościami tylko do odczytu nie jest obsługiwana.
* Domyślnie wyliczenia są obsługiwane jako liczby. [Nazwy wyliczenia można serializować jako ciągi](system-text-json-customize-properties.md#enums-as-strings).
* Pola nie są obsługiwane.
* Domyślnie komentarze lub końcowe przecinki w wyjątkach throw JSON. Można [zezwolić na komentarze i końcowe przecinki](system-text-json-invalid-json.md).
* [Domyślna głębokość maksymalna](xref:System.Text.Json.JsonReaderOptions.MaxDepth) to 64.

Jeśli używasz System.Text.Json bezpośrednio w aplikacji ASP.NET Core, niektóre domyślne zachowania są inne. Aby uzyskać więcej informacji, zobacz [Ustawienia domyślne sieci Web dla JsonSerializerOptions](system-text-json-configure-options.md#web-defaults-for-jsonserializeroptions).
::: zone-end

[Konwertery niestandardowe można zaimplementować](system-text-json-converters-how-to.md) w celu zapewnienia funkcjonalności, która nie jest obsługiwana przez wbudowane konwertery.

## <a name="serialize-to-formatted-json"></a>Serializacja do sformatowanego pliku JSON

Aby całkiem wydrukować dane wyjściowe JSON, ustaw wartość <xref:System.Text.Json.JsonSerializerOptions.WriteIndented?displayProperty=nameWithType> `true` :

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripToString.cs" id="SerializePrettyPrint":::

Oto przykład typu do serializacji i całkiem wydrukowanych danych wyjściowych JSON:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WF":::

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot"
}
```

Jeśli używasz `JsonSerializerOptions` wielokrotnie z tymi samymi opcjami, nie twórz nowego `JsonSerializerOptions` wystąpienia za każdym razem, gdy go używasz. Ponownie Użyj tego samego wystąpienia dla każdego wywołania. Aby uzyskać więcej informacji, zobacz [ponowne użycie wystąpień JsonSerializerOptions](system-text-json-configure-options.md#reuse-jsonserializeroptions-instances).

## <a name="include-fields"></a>Dołącz pola

::: zone pivot="dotnet-5-0"
Użyj <xref:System.Text.Json.JsonSerializerOptions.IncludeFields?displayProperty=nameWithType> Ustawienia globalnego lub atrybutu [[JsonInclude]](xref:System.Text.Json.Serialization.JsonIncludeAttribute) , aby dołączyć pola podczas serializacji lub deserializacji, jak pokazano w następującym przykładzie:

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/Fields.cs" highlight="16,18,20,32-35":::

Aby zignorować pola tylko do odczytu, użyj <xref:System.Text.Json.JsonSerializerOptions.IgnoreReadOnlyFields%2A?displayProperty=nameWithType> Ustawienia globalnego.
::: zone-end

::: zone pivot="dotnet-core-3-1"
Pola nie są obsługiwane w System.Text.Json programie .NET Core 3,1. Te funkcje mogą zapewniać [konwertery niestandardowe](system-text-json-converters-how-to.md) .
::: zone-end

## <a name="httpclient-and-httpcontent-extension-methods"></a>Metody rozszerzenia HttpClient i HttpContent

::: zone pivot="dotnet-5-0"

Serializowanie i deserializacja ładunków JSON z sieci to typowe operacje. Metody rozszerzające w [HttpClient](xref:System.Net.Http.Json.HttpClientJsonExtensions) i [HttpContent](xref:System.Net.Http.Json.HttpContentJsonExtensions) umożliwiają wykonywanie tych operacji w jednym wierszu kodu. Te metody rozszerzające używają [ustawień domyślnych sieci Web dla JsonSerializerOptions](system-text-json-configure-options.md#web-defaults-for-jsonserializeroptions).

Poniższy przykład ilustruje użycie <xref:System.Net.Http.Json.HttpClientJsonExtensions.GetFromJsonAsync%2A?displayProperty=nameWithType> i <xref:System.Net.Http.Json.HttpClientJsonExtensions.PostAsJsonAsync%2A?displayProperty=nameWithType> :

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/HttpClientExtensionMethods.cs" highlight="26,33":::

Istnieją również metody rozszerzające dla System.Text.Json [HttpContent](xref:System.Net.Http.Json.HttpContentJsonExtensions).
::: zone-end

::: zone pivot="dotnet-core-3-1"
Metody rozszerzające w systemach `HttpClient` i `HttpContent` nie są dostępne w System.Text.Json programie .NET Core 3,1.
::: zone-end

## <a name="see-also"></a>Zobacz także

* [System.Text.Json Podsumowanie](system-text-json-overview.md)
* [Tworzenie wystąpienia JsonSerializerOptions wystąpień](system-text-json-configure-options.md)
* [Włączanie dopasowywania bez uwzględniania wielkości liter](system-text-json-character-casing.md)
* [Dostosowywanie nazw i wartości właściwości](system-text-json-customize-properties.md)
* [Ignorowanie właściwości](system-text-json-ignore-properties.md)
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
