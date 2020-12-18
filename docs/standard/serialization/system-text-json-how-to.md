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
# <a name="how-to-serialize-and-deserialize-marshal-and-unmarshal-json-in-net"></a><span data-ttu-id="51729-104">Jak serializować i deserializować (Marshaling and unmarshaling) JSON w programie .NET</span><span class="sxs-lookup"><span data-stu-id="51729-104">How to serialize and deserialize (marshal and unmarshal) JSON in .NET</span></span>

<span data-ttu-id="51729-105">W tym artykule pokazano, jak używać <xref:System.Text.Json?displayProperty=fullName> przestrzeni nazw do serializacji i deserializacji z JavaScript Object Notation (JSON).</span><span class="sxs-lookup"><span data-stu-id="51729-105">This article shows how to use the <xref:System.Text.Json?displayProperty=fullName> namespace to serialize to and deserialize from JavaScript Object Notation (JSON).</span></span> <span data-ttu-id="51729-106">W przypadku przenoszenia istniejącego kodu z programu `Newtonsoft.Json` zapoznaj się z tematem [jak `System.Text.Json` przeprowadzić migrację do programu ](system-text-json-migrate-from-newtonsoft-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="51729-106">If you're porting existing code from `Newtonsoft.Json`, see [How to migrate to `System.Text.Json`](system-text-json-migrate-from-newtonsoft-how-to.md).</span></span>

<span data-ttu-id="51729-107">Instrukcje i przykładowy kod używają biblioteki bezpośrednio, a nie za pomocą struktury, takiej jak [ASP.NET Core](/aspnet/core/).</span><span class="sxs-lookup"><span data-stu-id="51729-107">The directions and sample code use the library directly, not through a framework such as [ASP.NET Core](/aspnet/core/).</span></span>

<span data-ttu-id="51729-108">Większość przykładowych kodów serializacji <xref:System.Text.Json.JsonSerializerOptions.WriteIndented?displayProperty=nameWithType> do `true` "DB-Print" w formacie JSON (z wcięciem i białym znakiem).</span><span class="sxs-lookup"><span data-stu-id="51729-108">Most of the serialization sample code sets <xref:System.Text.Json.JsonSerializerOptions.WriteIndented?displayProperty=nameWithType> to `true` to "pretty-print" the JSON (with indentation and whitespace for human readability).</span></span> <span data-ttu-id="51729-109">Do użycia w środowisku produkcyjnym zwykle przyjmuje się wartość domyślną `false` dla tego ustawienia.</span><span class="sxs-lookup"><span data-stu-id="51729-109">For production use, you would typically accept the default value of `false` for this setting.</span></span>

<span data-ttu-id="51729-110">Przykłady kodu odnoszą się do następującej klasy i wariantów:</span><span class="sxs-lookup"><span data-stu-id="51729-110">The code examples refer to the following class and variants of it:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WF":::

## <a name="namespaces"></a><span data-ttu-id="51729-111">Przestrzenie nazw</span><span class="sxs-lookup"><span data-stu-id="51729-111">Namespaces</span></span>

<span data-ttu-id="51729-112"><xref:System.Text.Json>Przestrzeń nazw zawiera wszystkie punkty wejścia i typy główne.</span><span class="sxs-lookup"><span data-stu-id="51729-112">The <xref:System.Text.Json> namespace contains all the entry points and the main types.</span></span> <span data-ttu-id="51729-113"><xref:System.Text.Json.Serialization>Przestrzeń nazw zawiera atrybuty i interfejsy API dla zaawansowanych scenariuszy i dostosowań specyficznych dla serializacji i deserializacji.</span><span class="sxs-lookup"><span data-stu-id="51729-113">The <xref:System.Text.Json.Serialization> namespace contains attributes and APIs for advanced scenarios and customization specific to serialization and deserialization.</span></span> <span data-ttu-id="51729-114">Przykłady kodu przedstawione w tym artykule wymagają `using` dyrektyw dla jednej lub obu tych przestrzeni nazw:</span><span class="sxs-lookup"><span data-stu-id="51729-114">The code examples shown in this article require `using` directives for one or both of these namespaces:</span></span>

```csharp
using System.Text.Json;
using System.Text.Json.Serialization;
```

> [!IMPORTANT]
> <span data-ttu-id="51729-115">Atrybuty z <xref:System.Runtime.Serialization> przestrzeni nazw nie są obsługiwane w programie `System.Text.Json` .</span><span class="sxs-lookup"><span data-stu-id="51729-115">Attributes from the <xref:System.Runtime.Serialization> namespace aren't supported in `System.Text.Json`.</span></span>

## <a name="how-to-write-net-objects-as-json-serialize"></a><span data-ttu-id="51729-116">Jak pisać obiekty .NET jako dane JSON (serializować)</span><span class="sxs-lookup"><span data-stu-id="51729-116">How to write .NET objects as JSON (serialize)</span></span>

<span data-ttu-id="51729-117">Aby zapisać dane JSON do ciągu lub do pliku, wywołaj <xref:System.Text.Json.JsonSerializer.Serialize%2A?displayProperty=nameWithType> metodę.</span><span class="sxs-lookup"><span data-stu-id="51729-117">To write JSON to a string or to a file, call the <xref:System.Text.Json.JsonSerializer.Serialize%2A?displayProperty=nameWithType> method.</span></span>

<span data-ttu-id="51729-118">Poniższy przykład tworzy kod JSON jako ciąg:</span><span class="sxs-lookup"><span data-stu-id="51729-118">The following example creates JSON as a string:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripToString.cs" id="Serialize":::

<span data-ttu-id="51729-119">Poniższy przykład używa kodu synchronicznego do utworzenia pliku JSON:</span><span class="sxs-lookup"><span data-stu-id="51729-119">The following example uses synchronous code to create a JSON file:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripToFile.cs" id="Serialize":::

<span data-ttu-id="51729-120">W poniższym przykładzie jest tworzony plik JSON przy użyciu kodu asynchronicznego:</span><span class="sxs-lookup"><span data-stu-id="51729-120">The following example uses asynchronous code to create a JSON file:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripToFileAsync.cs" id="Serialize":::

<span data-ttu-id="51729-121">Powyższe przykłady używają wnioskowania typu dla serializowanego typu.</span><span class="sxs-lookup"><span data-stu-id="51729-121">The preceding examples use type inference for the type being serialized.</span></span> <span data-ttu-id="51729-122">Przeciążenie `Serialize()` przyjmuje parametr typu ogólnego:</span><span class="sxs-lookup"><span data-stu-id="51729-122">An overload of `Serialize()` takes a generic type parameter:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripToString.cs" id="SerializeWithGenericParameter":::

### <a name="serialization-example"></a><span data-ttu-id="51729-123">Przykład serializacji</span><span class="sxs-lookup"><span data-stu-id="51729-123">Serialization example</span></span>

<span data-ttu-id="51729-124">Oto przykładowa Klasa, która zawiera właściwości typu kolekcji i typ zdefiniowany przez użytkownika:</span><span class="sxs-lookup"><span data-stu-id="51729-124">Here's an example class that contains collection-type properties and a user-defined type:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithPOCOs":::

> [!TIP]
> <span data-ttu-id="51729-125">"POCO" oznacza dla [zwykłego starego obiektu CLR](https://en.wikipedia.org/wiki/Plain_old_CLR_object).</span><span class="sxs-lookup"><span data-stu-id="51729-125">"POCO" stands for [plain old CLR object](https://en.wikipedia.org/wiki/Plain_old_CLR_object).</span></span> <span data-ttu-id="51729-126">POCO to typ .NET, który nie jest zależny od żadnych typów specyficznych dla platformy, na przykład przez dziedziczenie lub atrybuty.</span><span class="sxs-lookup"><span data-stu-id="51729-126">A POCO is a .NET type that doesn't depend on any framework-specific types, for example, through inheritance or attributes.</span></span>

<span data-ttu-id="51729-127">Dane wyjściowe JSON serializowania wystąpienia poprzedniego typu wyglądają podobnie jak w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="51729-127">The JSON output from serializing an instance of the preceding type looks like the following example.</span></span> <span data-ttu-id="51729-128">Dane wyjściowe JSON to zminimalizowanego (odstępy, wcięcia i znaki nowego wiersza są domyślnie usuwane):</span><span class="sxs-lookup"><span data-stu-id="51729-128">The JSON output is minified (whitespace, indentation, and new-line characters are removed) by default:</span></span>

```json
{"Date":"2019-08-01T00:00:00-07:00","TemperatureCelsius":25,"Summary":"Hot","DatesAvailable":["2019-08-01T00:00:00-07:00","2019-08-02T00:00:00-07:00"],"TemperatureRanges":{"Cold":{"High":20,"Low":-10},"Hot":{"High":60,"Low":20}},"SummaryWords":["Cool","Windy","Humid"]}
```

<span data-ttu-id="51729-129">W poniższym przykładzie przedstawiono ten sam kod JSON, ale sformatowany (to jest, całkiem wydruk z odstępami i wcięciami):</span><span class="sxs-lookup"><span data-stu-id="51729-129">The following example shows the same JSON, but formatted (that is, pretty-printed with whitespace and indentation):</span></span>

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

## <a name="serialize-to-utf-8"></a><span data-ttu-id="51729-130">Serializacja do UTF-8</span><span class="sxs-lookup"><span data-stu-id="51729-130">Serialize to UTF-8</span></span>

<span data-ttu-id="51729-131">Aby serializować do UTF-8, wywołaj <xref:System.Text.Json.JsonSerializer.SerializeToUtf8Bytes%2A?displayProperty=nameWithType> metodę:</span><span class="sxs-lookup"><span data-stu-id="51729-131">To serialize to UTF-8, call the <xref:System.Text.Json.JsonSerializer.SerializeToUtf8Bytes%2A?displayProperty=nameWithType> method:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripToUtf8.cs" id="Serialize":::

<span data-ttu-id="51729-132"><xref:System.Text.Json.JsonSerializer.Serialize%2A>Dostępne jest również Przeciążenie, które trwa <xref:System.Text.Json.Utf8JsonWriter> .</span><span class="sxs-lookup"><span data-stu-id="51729-132">A <xref:System.Text.Json.JsonSerializer.Serialize%2A> overload that takes a <xref:System.Text.Json.Utf8JsonWriter> is also available.</span></span>

<span data-ttu-id="51729-133">Serializacja do UTF-8 jest szybsza o 5-10% niż przy użyciu metod opartych na ciągach.</span><span class="sxs-lookup"><span data-stu-id="51729-133">Serializing to UTF-8 is about 5-10% faster than using the string-based methods.</span></span> <span data-ttu-id="51729-134">Różnica polega na tym, że bajty (w formacie UTF-8) nie muszą być konwertowane na ciągi (UTF-16).</span><span class="sxs-lookup"><span data-stu-id="51729-134">The difference is because the bytes (as UTF-8) don't need to be converted to strings (UTF-16).</span></span>

## <a name="serialization-behavior"></a><span data-ttu-id="51729-135">Zachowanie serializacji</span><span class="sxs-lookup"><span data-stu-id="51729-135">Serialization behavior</span></span>

::: zone pivot="dotnet-5-0"

* <span data-ttu-id="51729-136">Domyślnie wszystkie właściwości publiczne są serializowane.</span><span class="sxs-lookup"><span data-stu-id="51729-136">By default, all public properties are serialized.</span></span> <span data-ttu-id="51729-137">Można [określić właściwości do ignorowania](system-text-json-ignore-properties.md).</span><span class="sxs-lookup"><span data-stu-id="51729-137">You can [specify properties to ignore](system-text-json-ignore-properties.md).</span></span>
* <span data-ttu-id="51729-138">[Domyślny koder](xref:System.Text.Encodings.Web.JavaScriptEncoder.Default) wyprowadza znaki nienależące do zestawu znaków ASCII, znaki z uwzględnieniem języka HTML w zakresie ASCII i znaków, które muszą zostać zmienione zgodnie z [specyfikacją JSON RFC 8259](https://tools.ietf.org/html/rfc8259#section-7).</span><span class="sxs-lookup"><span data-stu-id="51729-138">The [default encoder](xref:System.Text.Encodings.Web.JavaScriptEncoder.Default) escapes non-ASCII characters, HTML-sensitive characters within the ASCII-range, and characters that must be escaped according to [the RFC 8259 JSON spec](https://tools.ietf.org/html/rfc8259#section-7).</span></span>
* <span data-ttu-id="51729-139">Domyślnie JSON jest zminimalizowanego.</span><span class="sxs-lookup"><span data-stu-id="51729-139">By default, JSON is minified.</span></span> <span data-ttu-id="51729-140">Można tu [wydrukować kod JSON](#serialize-to-formatted-json).</span><span class="sxs-lookup"><span data-stu-id="51729-140">You can [pretty-print the JSON](#serialize-to-formatted-json).</span></span>
* <span data-ttu-id="51729-141">Domyślnie wielkość liter w nazwach JSON jest zgodna z nazwami .NET.</span><span class="sxs-lookup"><span data-stu-id="51729-141">By default, casing of JSON names matches the .NET names.</span></span> <span data-ttu-id="51729-142">Można [dostosować wielkość liter w nazwach JSON](system-text-json-customize-properties.md).</span><span class="sxs-lookup"><span data-stu-id="51729-142">You can [customize JSON name casing](system-text-json-customize-properties.md).</span></span>
* <span data-ttu-id="51729-143">Domyślnie wykryto odwołania cykliczne i zostały zgłoszone wyjątki.</span><span class="sxs-lookup"><span data-stu-id="51729-143">By default, circular references are detected and exceptions thrown.</span></span> <span data-ttu-id="51729-144">Można [zachować odwołania i obsłużyć odwołania cykliczne](system-text-json-preserve-references.md).</span><span class="sxs-lookup"><span data-stu-id="51729-144">You can [preserve references and handle circular references](system-text-json-preserve-references.md).</span></span>
* <span data-ttu-id="51729-145">Domyślnie [pola](../../csharp/programming-guide/classes-and-structs/fields.md) są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="51729-145">By default, [fields](../../csharp/programming-guide/classes-and-structs/fields.md) are ignored.</span></span> <span data-ttu-id="51729-146">Możesz [dołączyć pola](#include-fields).</span><span class="sxs-lookup"><span data-stu-id="51729-146">You can [include fields](#include-fields).</span></span>

<span data-ttu-id="51729-147">Jeśli używasz System.Text.Json bezpośrednio w aplikacji ASP.NET Core, niektóre domyślne zachowania są inne.</span><span class="sxs-lookup"><span data-stu-id="51729-147">When you use System.Text.Json indirectly in an ASP.NET Core app, some default behaviors are different.</span></span> <span data-ttu-id="51729-148">Aby uzyskać więcej informacji, zobacz [Ustawienia domyślne sieci Web dla JsonSerializerOptions](system-text-json-configure-options.md#web-defaults-for-jsonserializeroptions).</span><span class="sxs-lookup"><span data-stu-id="51729-148">For more information, see [Web defaults for JsonSerializerOptions](system-text-json-configure-options.md#web-defaults-for-jsonserializeroptions).</span></span>
::: zone-end

::: zone pivot="dotnet-core-3-1"

* <span data-ttu-id="51729-149">Domyślnie wszystkie właściwości publiczne są serializowane.</span><span class="sxs-lookup"><span data-stu-id="51729-149">By default, all public properties are serialized.</span></span> <span data-ttu-id="51729-150">Można [określić właściwości do ignorowania](system-text-json-ignore-properties.md).</span><span class="sxs-lookup"><span data-stu-id="51729-150">You can [specify properties to ignore](system-text-json-ignore-properties.md).</span></span>
* <span data-ttu-id="51729-151">[Domyślny koder](xref:System.Text.Encodings.Web.JavaScriptEncoder.Default) wyprowadza znaki nienależące do zestawu znaków ASCII, znaki z uwzględnieniem języka HTML w zakresie ASCII i znaków, które muszą zostać zmienione zgodnie z [specyfikacją JSON RFC 8259](https://tools.ietf.org/html/rfc8259#section-7).</span><span class="sxs-lookup"><span data-stu-id="51729-151">The [default encoder](xref:System.Text.Encodings.Web.JavaScriptEncoder.Default) escapes non-ASCII characters, HTML-sensitive characters within the ASCII-range, and characters that must be escaped according to [the RFC 8259 JSON spec](https://tools.ietf.org/html/rfc8259#section-7).</span></span>
* <span data-ttu-id="51729-152">Domyślnie JSON jest zminimalizowanego.</span><span class="sxs-lookup"><span data-stu-id="51729-152">By default, JSON is minified.</span></span> <span data-ttu-id="51729-153">Można tu [wydrukować kod JSON](#serialize-to-formatted-json).</span><span class="sxs-lookup"><span data-stu-id="51729-153">You can [pretty-print the JSON](#serialize-to-formatted-json).</span></span>
* <span data-ttu-id="51729-154">Domyślnie wielkość liter w nazwach JSON jest zgodna z nazwami .NET.</span><span class="sxs-lookup"><span data-stu-id="51729-154">By default, casing of JSON names matches the .NET names.</span></span> <span data-ttu-id="51729-155">Można [dostosować wielkość liter w nazwach JSON](system-text-json-customize-properties.md).</span><span class="sxs-lookup"><span data-stu-id="51729-155">You can [customize JSON name casing](system-text-json-customize-properties.md).</span></span>
* <span data-ttu-id="51729-156">Wykryto odwołania cykliczne i zostały zgłoszone wyjątki.</span><span class="sxs-lookup"><span data-stu-id="51729-156">Circular references are detected and exceptions thrown.</span></span>
* <span data-ttu-id="51729-157">[Pola](../../csharp/programming-guide/classes-and-structs/fields.md) są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="51729-157">[Fields](../../csharp/programming-guide/classes-and-structs/fields.md) are ignored.</span></span>
::: zone-end

<span data-ttu-id="51729-158">Obsługiwane typy to:</span><span class="sxs-lookup"><span data-stu-id="51729-158">Supported types include:</span></span>
::: zone pivot="dotnet-5-0"

* <span data-ttu-id="51729-159">Elementy podstawowe platformy .NET, które są mapowane na elementy podstawowe języka JavaScript, takie jak typy liczbowe, ciągi i wartości logiczne.</span><span class="sxs-lookup"><span data-stu-id="51729-159">.NET primitives that map to JavaScript primitives, such as numeric types, strings, and Boolean.</span></span>
* <span data-ttu-id="51729-160">Obiekty CLR zdefiniowane przez użytkownika [(POCOs)](https://en.wikipedia.org/wiki/Plain_old_CLR_object).</span><span class="sxs-lookup"><span data-stu-id="51729-160">User-defined [plain old CLR objects (POCOs)](https://en.wikipedia.org/wiki/Plain_old_CLR_object).</span></span>
* <span data-ttu-id="51729-161">Tablice jednowymiarowe i nieregularne ( `T[][]` ).</span><span class="sxs-lookup"><span data-stu-id="51729-161">One-dimensional and jagged arrays (`T[][]`).</span></span>
* <span data-ttu-id="51729-162">Kolekcje i słowniki z następujących przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="51729-162">Collections and dictionaries from the following namespaces.</span></span>
  * <xref:System.Collections>
  * <xref:System.Collections.Generic>
  * <xref:System.Collections.Immutable>
  * <xref:System.Collections.Concurrent>
  * <xref:System.Collections.Specialized>
  * <xref:System.Collections.ObjectModel>
::: zone-end

::: zone pivot="dotnet-core-3-1"

* <span data-ttu-id="51729-163">Elementy podstawowe platformy .NET, które są mapowane na elementy podstawowe języka JavaScript, takie jak typy liczbowe, ciągi i wartości logiczne.</span><span class="sxs-lookup"><span data-stu-id="51729-163">.NET primitives that map to JavaScript primitives, such as numeric types, strings, and Boolean.</span></span>
* <span data-ttu-id="51729-164">Obiekty CLR zdefiniowane przez użytkownika [(POCOs)](https://en.wikipedia.org/wiki/Plain_old_CLR_object).</span><span class="sxs-lookup"><span data-stu-id="51729-164">User-defined [plain old CLR objects (POCOs)](https://en.wikipedia.org/wiki/Plain_old_CLR_object).</span></span>
* <span data-ttu-id="51729-165">Tablice jednowymiarowe i nieregularne ( `ArrayName[][]` ).</span><span class="sxs-lookup"><span data-stu-id="51729-165">One-dimensional and jagged arrays (`ArrayName[][]`).</span></span>
* <span data-ttu-id="51729-166">`Dictionary<string,TValue>` gdzie `TValue` is to `object` , `JsonElement` lub poco.</span><span class="sxs-lookup"><span data-stu-id="51729-166">`Dictionary<string,TValue>` where `TValue` is `object`, `JsonElement`, or a POCO.</span></span>
* <span data-ttu-id="51729-167">Kolekcje z następujących przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="51729-167">Collections from the following namespaces.</span></span>
  * <xref:System.Collections>
  * <xref:System.Collections.Generic>
  * <xref:System.Collections.Immutable>
  * <xref:System.Collections.Concurrent>
  * <xref:System.Collections.Specialized>
  * <xref:System.Collections.ObjectModel>
::: zone-end

<span data-ttu-id="51729-168">Można [zaimplementować niestandardowe konwertery](system-text-json-converters-how-to.md) w celu obsługi dodatkowych typów lub zapewnienia funkcjonalności, która nie jest obsługiwana przez wbudowane konwertery.</span><span class="sxs-lookup"><span data-stu-id="51729-168">You can [implement custom converters](system-text-json-converters-how-to.md) to handle additional types or to provide functionality that isn't supported by the built-in converters.</span></span>

## <a name="how-to-read-json-as-net-objects-deserialize"></a><span data-ttu-id="51729-169">Jak odczytać dane JSON jako obiekty .NET (deserializacji)</span><span class="sxs-lookup"><span data-stu-id="51729-169">How to read JSON as .NET objects (deserialize)</span></span>

<span data-ttu-id="51729-170">Aby zdeserializować z ciągu lub pliku, wywołaj <xref:System.Text.Json.JsonSerializer.Deserialize%2A?displayProperty=nameWithType> metodę.</span><span class="sxs-lookup"><span data-stu-id="51729-170">To deserialize from a string or a file, call the <xref:System.Text.Json.JsonSerializer.Deserialize%2A?displayProperty=nameWithType> method.</span></span>

<span data-ttu-id="51729-171">Poniższy przykład odczytuje dane JSON z ciągu i tworzy wystąpienie `WeatherForecastWithPOCOs` klasy pokazanej wcześniej dla [przykładu serializacji](#serialization-example):</span><span class="sxs-lookup"><span data-stu-id="51729-171">The following example reads JSON from a string and creates an instance of the `WeatherForecastWithPOCOs` class shown earlier for the [serialization example](#serialization-example):</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripToString.cs" id="Deserialize":::

<span data-ttu-id="51729-172">Aby zdeserializować z pliku przy użyciu kodu synchronicznego, Odczytaj plik do ciągu, jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="51729-172">To deserialize from a file by using synchronous code, read the file into a string, as shown in the following example:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripToFile.cs" id="Deserialize":::

<span data-ttu-id="51729-173">Aby zdeserializować z pliku przy użyciu kodu asynchronicznego, wywołaj <xref:System.Text.Json.JsonSerializer.DeserializeAsync%2A> metodę:</span><span class="sxs-lookup"><span data-stu-id="51729-173">To deserialize from a file by using asynchronous code, call the <xref:System.Text.Json.JsonSerializer.DeserializeAsync%2A> method:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripToFileAsync.cs" id="Deserialize":::

> [!TIP]
> <span data-ttu-id="51729-174">Jeśli masz kod JSON, który chcesz zdeserializować i nie masz klasy do deserializacji, w programie Visual Studio 2019 można automatycznie wygenerować klasę, której potrzebujesz:</span><span class="sxs-lookup"><span data-stu-id="51729-174">If you have JSON that you want to deserialize, and you don't have the class to deserialize it into, Visual Studio 2019 can automatically generate the class you need:</span></span>
>
> 1. <span data-ttu-id="51729-175">Skopiuj kod JSON, który ma być niezbędny do deserializacji.</span><span class="sxs-lookup"><span data-stu-id="51729-175">Copy the JSON that you need to deserialize.</span></span>
> 1. <span data-ttu-id="51729-176">Utwórz plik klasy i Usuń kod szablonu.</span><span class="sxs-lookup"><span data-stu-id="51729-176">Create a class file and delete the template code.</span></span>
> 1. <span data-ttu-id="51729-177">Wybierz pozycję **Edytuj**  >  **Wklej specjalne**  >  **Wklej dane JSON jako klasy**.</span><span class="sxs-lookup"><span data-stu-id="51729-177">Choose **Edit** > **Paste Special** > **Paste JSON as Classes**.</span></span>
>
> <span data-ttu-id="51729-178">Wynik jest klasą, której można użyć dla celu deserializacji.</span><span class="sxs-lookup"><span data-stu-id="51729-178">The result is a class that you can use for your deserialization target.</span></span>

## <a name="deserialize-from-utf-8"></a><span data-ttu-id="51729-179">Deserializacja z UTF-8</span><span class="sxs-lookup"><span data-stu-id="51729-179">Deserialize from UTF-8</span></span>

<span data-ttu-id="51729-180">Aby zdeserializować z UTF-8, wywołaj <xref:System.Text.Json.JsonSerializer.Deserialize%2A?displayProperty=nameWithType> Przeciążenie, które pobiera `ReadOnlySpan<byte>` lub a `Utf8JsonReader` , jak pokazano w poniższych przykładach.</span><span class="sxs-lookup"><span data-stu-id="51729-180">To deserialize from UTF-8, call a <xref:System.Text.Json.JsonSerializer.Deserialize%2A?displayProperty=nameWithType> overload that takes a `ReadOnlySpan<byte>` or a `Utf8JsonReader`, as shown in the following examples.</span></span> <span data-ttu-id="51729-181">W przykładach założono, że kod JSON znajduje się w tablicy bajtów o nazwie jsonUtf8Bytes.</span><span class="sxs-lookup"><span data-stu-id="51729-181">The examples assume the JSON is in a byte array named jsonUtf8Bytes.</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripToUtf8.cs" id="Deserialize1":::

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripToUtf8.cs" id="Deserialize2":::

## <a name="deserialization-behavior"></a><span data-ttu-id="51729-182">Zachowanie deserializacji</span><span class="sxs-lookup"><span data-stu-id="51729-182">Deserialization behavior</span></span>

<span data-ttu-id="51729-183">Podczas deserializacji kodu JSON stosowane są następujące zachowania:</span><span class="sxs-lookup"><span data-stu-id="51729-183">The following behaviors apply when deserializing JSON:</span></span>

::: zone pivot="dotnet-5-0"

* <span data-ttu-id="51729-184">Domyślnie w dopasowaniu nazw właściwości rozróżniana jest wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="51729-184">By default, property name matching is case-sensitive.</span></span> <span data-ttu-id="51729-185">Można [określić wielkość liter](system-text-json-character-casing.md).</span><span class="sxs-lookup"><span data-stu-id="51729-185">You can [specify case-insensitivity](system-text-json-character-casing.md).</span></span>
* <span data-ttu-id="51729-186">Jeśli kod JSON zawiera wartość właściwości tylko do odczytu, wartość jest ignorowana i nie jest zgłaszany żaden wyjątek.</span><span class="sxs-lookup"><span data-stu-id="51729-186">If the JSON contains a value for a read-only property, the value is ignored and no exception is thrown.</span></span>
* <span data-ttu-id="51729-187">Konstruktory niepubliczne są ignorowane przez serializator.</span><span class="sxs-lookup"><span data-stu-id="51729-187">Non-public constructors are ignored by the serializer.</span></span>
* <span data-ttu-id="51729-188">Obsługa deserializacji do niemodyfikowalnych obiektów lub właściwości tylko do odczytu jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="51729-188">Deserialization to immutable objects or read-only properties is supported.</span></span> <span data-ttu-id="51729-189">Zobacz [zmienne typy i rekordy](system-text-json-immutability.md).</span><span class="sxs-lookup"><span data-stu-id="51729-189">See [Immutable types and Records](system-text-json-immutability.md).</span></span>
* <span data-ttu-id="51729-190">Domyślnie wyliczenia są obsługiwane jako liczby.</span><span class="sxs-lookup"><span data-stu-id="51729-190">By default, enums are supported as numbers.</span></span> <span data-ttu-id="51729-191">[Nazwy wyliczenia można serializować jako ciągi](system-text-json-customize-properties.md#enums-as-strings).</span><span class="sxs-lookup"><span data-stu-id="51729-191">You can [serialize enum names as strings](system-text-json-customize-properties.md#enums-as-strings).</span></span>
* <span data-ttu-id="51729-192">Domyślnie pola są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="51729-192">By default, fields are ignored.</span></span> <span data-ttu-id="51729-193">Możesz [dołączyć pola](#include-fields).</span><span class="sxs-lookup"><span data-stu-id="51729-193">You can [include fields](#include-fields).</span></span>
* <span data-ttu-id="51729-194">Domyślnie komentarze lub końcowe przecinki w wyjątkach throw JSON.</span><span class="sxs-lookup"><span data-stu-id="51729-194">By default, comments or trailing commas in the JSON throw exceptions.</span></span> <span data-ttu-id="51729-195">Można [zezwolić na komentarze i końcowe przecinki](system-text-json-invalid-json.md).</span><span class="sxs-lookup"><span data-stu-id="51729-195">You can [allow comments and trailing commas](system-text-json-invalid-json.md).</span></span>
* <span data-ttu-id="51729-196">[Domyślna głębokość maksymalna](xref:System.Text.Json.JsonReaderOptions.MaxDepth) to 64.</span><span class="sxs-lookup"><span data-stu-id="51729-196">The [default maximum depth](xref:System.Text.Json.JsonReaderOptions.MaxDepth) is 64.</span></span>

<span data-ttu-id="51729-197">Jeśli używasz System.Text.Json bezpośrednio w aplikacji ASP.NET Core, niektóre domyślne zachowania są inne.</span><span class="sxs-lookup"><span data-stu-id="51729-197">When you use System.Text.Json indirectly in an ASP.NET Core app, some default behaviors are different.</span></span> <span data-ttu-id="51729-198">Aby uzyskać więcej informacji, zobacz [Ustawienia domyślne sieci Web dla JsonSerializerOptions](system-text-json-configure-options.md#web-defaults-for-jsonserializeroptions).</span><span class="sxs-lookup"><span data-stu-id="51729-198">For more information, see [Web defaults for JsonSerializerOptions](system-text-json-configure-options.md#web-defaults-for-jsonserializeroptions).</span></span>
::: zone-end

::: zone pivot="dotnet-core-3-1"

* <span data-ttu-id="51729-199">Domyślnie w dopasowaniu nazw właściwości rozróżniana jest wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="51729-199">By default, property name matching is case-sensitive.</span></span> <span data-ttu-id="51729-200">Można [określić wielkość liter](system-text-json-character-casing.md).</span><span class="sxs-lookup"><span data-stu-id="51729-200">You can [specify case-insensitivity](system-text-json-character-casing.md).</span></span> <span data-ttu-id="51729-201">Aplikacje ASP.NET Core [Domyślnie określają wielkość liter](system-text-json-configure-options.md#web-defaults-for-jsonserializeroptions).</span><span class="sxs-lookup"><span data-stu-id="51729-201">ASP.NET Core apps [specify case-insensitivity by default](system-text-json-configure-options.md#web-defaults-for-jsonserializeroptions).</span></span>
* <span data-ttu-id="51729-202">Jeśli kod JSON zawiera wartość właściwości tylko do odczytu, wartość jest ignorowana i nie jest zgłaszany żaden wyjątek.</span><span class="sxs-lookup"><span data-stu-id="51729-202">If the JSON contains a value for a read-only property, the value is ignored and no exception is thrown.</span></span>
* <span data-ttu-id="51729-203">Konstruktor bez parametrów, który może być publiczny, wewnętrzny lub prywatny, jest używany do deserializacji.</span><span class="sxs-lookup"><span data-stu-id="51729-203">A parameterless constructor, which can be public, internal, or private, is used for deserialization.</span></span>
* <span data-ttu-id="51729-204">Deserializacja z niezmiennymi obiektami lub właściwościami tylko do odczytu nie jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="51729-204">Deserialization to immutable objects or read-only properties isn't supported.</span></span>
* <span data-ttu-id="51729-205">Domyślnie wyliczenia są obsługiwane jako liczby.</span><span class="sxs-lookup"><span data-stu-id="51729-205">By default, enums are supported as numbers.</span></span> <span data-ttu-id="51729-206">[Nazwy wyliczenia można serializować jako ciągi](system-text-json-customize-properties.md#enums-as-strings).</span><span class="sxs-lookup"><span data-stu-id="51729-206">You can [serialize enum names as strings](system-text-json-customize-properties.md#enums-as-strings).</span></span>
* <span data-ttu-id="51729-207">Pola nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="51729-207">Fields aren't supported.</span></span>
* <span data-ttu-id="51729-208">Domyślnie komentarze lub końcowe przecinki w wyjątkach throw JSON.</span><span class="sxs-lookup"><span data-stu-id="51729-208">By default, comments or trailing commas in the JSON throw exceptions.</span></span> <span data-ttu-id="51729-209">Można [zezwolić na komentarze i końcowe przecinki](system-text-json-invalid-json.md).</span><span class="sxs-lookup"><span data-stu-id="51729-209">You can [allow comments and trailing commas](system-text-json-invalid-json.md).</span></span>
* <span data-ttu-id="51729-210">[Domyślna głębokość maksymalna](xref:System.Text.Json.JsonReaderOptions.MaxDepth) to 64.</span><span class="sxs-lookup"><span data-stu-id="51729-210">The [default maximum depth](xref:System.Text.Json.JsonReaderOptions.MaxDepth) is 64.</span></span>

<span data-ttu-id="51729-211">Jeśli używasz System.Text.Json bezpośrednio w aplikacji ASP.NET Core, niektóre domyślne zachowania są inne.</span><span class="sxs-lookup"><span data-stu-id="51729-211">When you use System.Text.Json indirectly in an ASP.NET Core app, some default behaviors are different.</span></span> <span data-ttu-id="51729-212">Aby uzyskać więcej informacji, zobacz [Ustawienia domyślne sieci Web dla JsonSerializerOptions](system-text-json-configure-options.md#web-defaults-for-jsonserializeroptions).</span><span class="sxs-lookup"><span data-stu-id="51729-212">For more information, see [Web defaults for JsonSerializerOptions](system-text-json-configure-options.md#web-defaults-for-jsonserializeroptions).</span></span>
::: zone-end

<span data-ttu-id="51729-213">[Konwertery niestandardowe można zaimplementować](system-text-json-converters-how-to.md) w celu zapewnienia funkcjonalności, która nie jest obsługiwana przez wbudowane konwertery.</span><span class="sxs-lookup"><span data-stu-id="51729-213">You can [implement custom converters](system-text-json-converters-how-to.md) to provide functionality that isn't supported by the built-in converters.</span></span>

## <a name="serialize-to-formatted-json"></a><span data-ttu-id="51729-214">Serializacja do sformatowanego pliku JSON</span><span class="sxs-lookup"><span data-stu-id="51729-214">Serialize to formatted JSON</span></span>

<span data-ttu-id="51729-215">Aby całkiem wydrukować dane wyjściowe JSON, ustaw wartość <xref:System.Text.Json.JsonSerializerOptions.WriteIndented?displayProperty=nameWithType> `true` :</span><span class="sxs-lookup"><span data-stu-id="51729-215">To pretty-print the JSON output, set <xref:System.Text.Json.JsonSerializerOptions.WriteIndented?displayProperty=nameWithType> to `true`:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripToString.cs" id="SerializePrettyPrint":::

<span data-ttu-id="51729-216">Oto przykład typu do serializacji i całkiem wydrukowanych danych wyjściowych JSON:</span><span class="sxs-lookup"><span data-stu-id="51729-216">Here's an example type to be serialized and pretty-printed JSON output:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WF":::

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot"
}
```

<span data-ttu-id="51729-217">Jeśli używasz `JsonSerializerOptions` wielokrotnie z tymi samymi opcjami, nie twórz nowego `JsonSerializerOptions` wystąpienia za każdym razem, gdy go używasz.</span><span class="sxs-lookup"><span data-stu-id="51729-217">If you use `JsonSerializerOptions` repeatedly with the same options, don't create a new `JsonSerializerOptions` instance each time you use it.</span></span> <span data-ttu-id="51729-218">Ponownie Użyj tego samego wystąpienia dla każdego wywołania.</span><span class="sxs-lookup"><span data-stu-id="51729-218">Reuse the same instance for every call.</span></span> <span data-ttu-id="51729-219">Aby uzyskać więcej informacji, zobacz [ponowne użycie wystąpień JsonSerializerOptions](system-text-json-configure-options.md#reuse-jsonserializeroptions-instances).</span><span class="sxs-lookup"><span data-stu-id="51729-219">For more information, see [Reuse JsonSerializerOptions instances](system-text-json-configure-options.md#reuse-jsonserializeroptions-instances).</span></span>

## <a name="include-fields"></a><span data-ttu-id="51729-220">Dołącz pola</span><span class="sxs-lookup"><span data-stu-id="51729-220">Include fields</span></span>

::: zone pivot="dotnet-5-0"
<span data-ttu-id="51729-221">Użyj <xref:System.Text.Json.JsonSerializerOptions.IncludeFields?displayProperty=nameWithType> Ustawienia globalnego lub atrybutu [[JsonInclude]](xref:System.Text.Json.Serialization.JsonIncludeAttribute) , aby dołączyć pola podczas serializacji lub deserializacji, jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="51729-221">Use the <xref:System.Text.Json.JsonSerializerOptions.IncludeFields?displayProperty=nameWithType> global setting or the [[JsonInclude]](xref:System.Text.Json.Serialization.JsonIncludeAttribute) attribute to include fields when serializing or deserializing, as shown in the following example:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/Fields.cs" highlight="16,18,20,32-35":::

<span data-ttu-id="51729-222">Aby zignorować pola tylko do odczytu, użyj <xref:System.Text.Json.JsonSerializerOptions.IgnoreReadOnlyFields%2A?displayProperty=nameWithType> Ustawienia globalnego.</span><span class="sxs-lookup"><span data-stu-id="51729-222">To ignore read-only fields, use the <xref:System.Text.Json.JsonSerializerOptions.IgnoreReadOnlyFields%2A?displayProperty=nameWithType> global setting.</span></span>
::: zone-end

::: zone pivot="dotnet-core-3-1"
<span data-ttu-id="51729-223">Pola nie są obsługiwane w System.Text.Json programie .NET Core 3,1.</span><span class="sxs-lookup"><span data-stu-id="51729-223">Fields are not supported in System.Text.Json in .NET Core 3.1.</span></span> <span data-ttu-id="51729-224">Te funkcje mogą zapewniać [konwertery niestandardowe](system-text-json-converters-how-to.md) .</span><span class="sxs-lookup"><span data-stu-id="51729-224">[Custom converters](system-text-json-converters-how-to.md) can provide this functionality.</span></span>
::: zone-end

## <a name="httpclient-and-httpcontent-extension-methods"></a><span data-ttu-id="51729-225">Metody rozszerzenia HttpClient i HttpContent</span><span class="sxs-lookup"><span data-stu-id="51729-225">HttpClient and HttpContent extension methods</span></span>

::: zone pivot="dotnet-5-0"

<span data-ttu-id="51729-226">Serializowanie i deserializacja ładunków JSON z sieci to typowe operacje.</span><span class="sxs-lookup"><span data-stu-id="51729-226">Serializing and deserializing JSON payloads from the network are common operations.</span></span> <span data-ttu-id="51729-227">Metody rozszerzające w [HttpClient](xref:System.Net.Http.Json.HttpClientJsonExtensions) i [HttpContent](xref:System.Net.Http.Json.HttpContentJsonExtensions) umożliwiają wykonywanie tych operacji w jednym wierszu kodu.</span><span class="sxs-lookup"><span data-stu-id="51729-227">Extension methods on [HttpClient](xref:System.Net.Http.Json.HttpClientJsonExtensions) and [HttpContent](xref:System.Net.Http.Json.HttpContentJsonExtensions) let you do these operations in a single line of code.</span></span> <span data-ttu-id="51729-228">Te metody rozszerzające używają [ustawień domyślnych sieci Web dla JsonSerializerOptions](system-text-json-configure-options.md#web-defaults-for-jsonserializeroptions).</span><span class="sxs-lookup"><span data-stu-id="51729-228">These extension methods use [web defaults for JsonSerializerOptions](system-text-json-configure-options.md#web-defaults-for-jsonserializeroptions).</span></span>

<span data-ttu-id="51729-229">Poniższy przykład ilustruje użycie <xref:System.Net.Http.Json.HttpClientJsonExtensions.GetFromJsonAsync%2A?displayProperty=nameWithType> i <xref:System.Net.Http.Json.HttpClientJsonExtensions.PostAsJsonAsync%2A?displayProperty=nameWithType> :</span><span class="sxs-lookup"><span data-stu-id="51729-229">The following example illustrates use of <xref:System.Net.Http.Json.HttpClientJsonExtensions.GetFromJsonAsync%2A?displayProperty=nameWithType> and <xref:System.Net.Http.Json.HttpClientJsonExtensions.PostAsJsonAsync%2A?displayProperty=nameWithType>:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/HttpClientExtensionMethods.cs" highlight="26,33":::

<span data-ttu-id="51729-230">Istnieją również metody rozszerzające dla System.Text.Json [HttpContent](xref:System.Net.Http.Json.HttpContentJsonExtensions).</span><span class="sxs-lookup"><span data-stu-id="51729-230">There are also extension methods for System.Text.Json on [HttpContent](xref:System.Net.Http.Json.HttpContentJsonExtensions).</span></span>
::: zone-end

::: zone pivot="dotnet-core-3-1"
<span data-ttu-id="51729-231">Metody rozszerzające w systemach `HttpClient` i `HttpContent` nie są dostępne w System.Text.Json programie .NET Core 3,1.</span><span class="sxs-lookup"><span data-stu-id="51729-231">Extension methods on `HttpClient` and `HttpContent` are not available in System.Text.Json in .NET Core 3.1.</span></span>
::: zone-end

## <a name="see-also"></a><span data-ttu-id="51729-232">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="51729-232">See also</span></span>

* [<span data-ttu-id="51729-233">System.Text.Json Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="51729-233">System.Text.Json overview</span></span>](system-text-json-overview.md)
* [<span data-ttu-id="51729-234">Tworzenie wystąpienia JsonSerializerOptions wystąpień</span><span class="sxs-lookup"><span data-stu-id="51729-234">Instantiate JsonSerializerOptions instances</span></span>](system-text-json-configure-options.md)
* [<span data-ttu-id="51729-235">Włączanie dopasowywania bez uwzględniania wielkości liter</span><span class="sxs-lookup"><span data-stu-id="51729-235">Enable case-insensitive matching</span></span>](system-text-json-character-casing.md)
* [<span data-ttu-id="51729-236">Dostosowywanie nazw i wartości właściwości</span><span class="sxs-lookup"><span data-stu-id="51729-236">Customize property names and values</span></span>](system-text-json-customize-properties.md)
* [<span data-ttu-id="51729-237">Ignorowanie właściwości</span><span class="sxs-lookup"><span data-stu-id="51729-237">Ignore properties</span></span>](system-text-json-ignore-properties.md)
* [<span data-ttu-id="51729-238">Zezwalanie na nieprawidłowy kod JSON</span><span class="sxs-lookup"><span data-stu-id="51729-238">Allow invalid JSON</span></span>](system-text-json-invalid-json.md)
* [<span data-ttu-id="51729-239">Obsługa przepełnienia kodu JSON</span><span class="sxs-lookup"><span data-stu-id="51729-239">Handle overflow JSON</span></span>](system-text-json-handle-overflow.md)
* [<span data-ttu-id="51729-240">Zachowywanie odwołań</span><span class="sxs-lookup"><span data-stu-id="51729-240">Preserve references</span></span>](system-text-json-preserve-references.md)
* [<span data-ttu-id="51729-241">Niemodyfikowalne typy i niepubliczne metody dostępu</span><span class="sxs-lookup"><span data-stu-id="51729-241">Immutable types and non-public accessors</span></span>](system-text-json-immutability.md)
* [<span data-ttu-id="51729-242">Serializacja polimorficzna</span><span class="sxs-lookup"><span data-stu-id="51729-242">Polymorphic serialization</span></span>](system-text-json-polymorphism.md)
* [<span data-ttu-id="51729-243">Migruj z Newtonsoft.Json do System.Text.Json</span><span class="sxs-lookup"><span data-stu-id="51729-243">Migrate from Newtonsoft.Json to System.Text.Json</span></span>](system-text-json-migrate-from-newtonsoft-how-to.md)
* [<span data-ttu-id="51729-244">Dostosowywanie kodowania znaków</span><span class="sxs-lookup"><span data-stu-id="51729-244">Customize character encoding</span></span>](system-text-json-character-encoding.md)
* [<span data-ttu-id="51729-245">Napisz niestandardowe serializatory i deserializatory</span><span class="sxs-lookup"><span data-stu-id="51729-245">Write custom serializers and deserializers</span></span>](write-custom-serializer-deserializer.md)
* [<span data-ttu-id="51729-246">Zapisz konwertery niestandardowe na potrzeby serializacji JSON</span><span class="sxs-lookup"><span data-stu-id="51729-246">Write custom converters for JSON serialization</span></span>](system-text-json-converters-how-to.md)
* [<span data-ttu-id="51729-247">Obsługa wartości DateTime i DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="51729-247">DateTime and DateTimeOffset support</span></span>](../datetime/system-text-json-support.md)
* <span data-ttu-id="51729-248">[System.Text.Json Dokumentacja interfejsu API](xref:System.Text.Json)</span><span class="sxs-lookup"><span data-stu-id="51729-248">[System.Text.Json API reference](xref:System.Text.Json)</span></span>
* <span data-ttu-id="51729-249">[System.Text.Json. Dokumentacja interfejsu API serializacji](xref:System.Text.Json.Serialization)</span><span class="sxs-lookup"><span data-stu-id="51729-249">[System.Text.Json.Serialization API reference](xref:System.Text.Json.Serialization)</span></span>
