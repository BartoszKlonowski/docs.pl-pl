---
title: Jak serializować i deserializować kod JSON przy użyciu języka C# — .NET
description: Dowiedz się, jak używać System.Text.Json przestrzeni nazw do serializacji i deserializacji z JSON w programie .NET. Zawiera przykładowy kod.
ms.date: 11/30/2020
ms.custom: contperfq2
no-loc:
- System.Text.Json
- Newtonsoft.Json
zone_pivot_groups: dotnet-version
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
ms.openlocfilehash: 9ea9e2fef5ef66f2a5ff816168abfbd7b2e75276
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96437675"
---
# <a name="how-to-serialize-and-deserialize-marshal-and-unmarshal-json-in-net"></a><span data-ttu-id="363b9-104">Jak serializować i deserializować (Marshaling and unmarshaling) JSON w programie .NET</span><span class="sxs-lookup"><span data-stu-id="363b9-104">How to serialize and deserialize (marshal and unmarshal) JSON in .NET</span></span>

<span data-ttu-id="363b9-105">W tym artykule pokazano, jak używać <xref:System.Text.Json?displayProperty=fullName> przestrzeni nazw do serializacji i deserializacji z JavaScript Object Notation (JSON).</span><span class="sxs-lookup"><span data-stu-id="363b9-105">This article shows how to use the <xref:System.Text.Json?displayProperty=fullName> namespace to serialize to and deserialize from JavaScript Object Notation (JSON).</span></span> <span data-ttu-id="363b9-106">W przypadku przenoszenia istniejącego kodu z programu `Newtonsoft.Json` zapoznaj się z tematem [jak `System.Text.Json` przeprowadzić migrację do programu ](system-text-json-migrate-from-newtonsoft-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="363b9-106">If you're porting existing code from `Newtonsoft.Json`, see [How to migrate to `System.Text.Json`](system-text-json-migrate-from-newtonsoft-how-to.md).</span></span>

<span data-ttu-id="363b9-107">Instrukcje i przykładowy kod używają biblioteki bezpośrednio, a nie za pomocą struktury, takiej jak [ASP.NET Core](/aspnet/core/).</span><span class="sxs-lookup"><span data-stu-id="363b9-107">The directions and sample code use the library directly, not through a framework such as [ASP.NET Core](/aspnet/core/).</span></span>

<span data-ttu-id="363b9-108">Większość przykładowych kodów serializacji <xref:System.Text.Json.JsonSerializerOptions.WriteIndented?displayProperty=nameWithType> do `true` "DB-Print" w formacie JSON (z wcięciem i białym znakiem).</span><span class="sxs-lookup"><span data-stu-id="363b9-108">Most of the serialization sample code sets <xref:System.Text.Json.JsonSerializerOptions.WriteIndented?displayProperty=nameWithType> to `true` to "pretty-print" the JSON (with indentation and whitespace for human readability).</span></span> <span data-ttu-id="363b9-109">Do użycia w środowisku produkcyjnym zwykle przyjmuje się wartość domyślną `false` dla tego ustawienia.</span><span class="sxs-lookup"><span data-stu-id="363b9-109">For production use, you would typically accept the default value of `false` for this setting.</span></span>

<span data-ttu-id="363b9-110">Przykłady kodu odnoszą się do następującej klasy i wariantów:</span><span class="sxs-lookup"><span data-stu-id="363b9-110">The code examples refer to the following class and variants of it:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WF":::

## <a name="namespaces"></a><span data-ttu-id="363b9-111">Przestrzenie nazw</span><span class="sxs-lookup"><span data-stu-id="363b9-111">Namespaces</span></span>

<span data-ttu-id="363b9-112"><xref:System.Text.Json>Przestrzeń nazw zawiera wszystkie punkty wejścia i typy główne.</span><span class="sxs-lookup"><span data-stu-id="363b9-112">The <xref:System.Text.Json> namespace contains all the entry points and the main types.</span></span> <span data-ttu-id="363b9-113"><xref:System.Text.Json.Serialization>Przestrzeń nazw zawiera atrybuty i interfejsy API dla zaawansowanych scenariuszy i dostosowań specyficznych dla serializacji i deserializacji.</span><span class="sxs-lookup"><span data-stu-id="363b9-113">The <xref:System.Text.Json.Serialization> namespace contains attributes and APIs for advanced scenarios and customization specific to serialization and deserialization.</span></span> <span data-ttu-id="363b9-114">Przykłady kodu przedstawione w tym artykule wymagają `using` dyrektyw dla jednej lub obu tych przestrzeni nazw:</span><span class="sxs-lookup"><span data-stu-id="363b9-114">The code examples shown in this article require `using` directives for one or both of these namespaces:</span></span>

```csharp
using System.Text.Json;
using System.Text.Json.Serialization;
```

> [!IMPORTANT]
> <span data-ttu-id="363b9-115">Atrybuty z <xref:System.Runtime.Serialization> przestrzeni nazw nie są obsługiwane w programie `System.Text.Json` .</span><span class="sxs-lookup"><span data-stu-id="363b9-115">Attributes from the <xref:System.Runtime.Serialization> namespace aren't supported in `System.Text.Json`.</span></span>

## <a name="how-to-write-net-objects-as-json-serialize"></a><span data-ttu-id="363b9-116">Jak pisać obiekty .NET jako dane JSON (serializować)</span><span class="sxs-lookup"><span data-stu-id="363b9-116">How to write .NET objects as JSON (serialize)</span></span>

<span data-ttu-id="363b9-117">Aby zapisać dane JSON do ciągu lub do pliku, wywołaj <xref:System.Text.Json.JsonSerializer.Serialize%2A?displayProperty=nameWithType> metodę.</span><span class="sxs-lookup"><span data-stu-id="363b9-117">To write JSON to a string or to a file, call the <xref:System.Text.Json.JsonSerializer.Serialize%2A?displayProperty=nameWithType> method.</span></span>

<span data-ttu-id="363b9-118">Poniższy przykład tworzy kod JSON jako ciąg:</span><span class="sxs-lookup"><span data-stu-id="363b9-118">The following example creates JSON as a string:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripToString.cs" id="Serialize":::

<span data-ttu-id="363b9-119">Poniższy przykład używa kodu synchronicznego do utworzenia pliku JSON:</span><span class="sxs-lookup"><span data-stu-id="363b9-119">The following example uses synchronous code to create a JSON file:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripToFile.cs" id="Serialize":::

<span data-ttu-id="363b9-120">W poniższym przykładzie jest tworzony plik JSON przy użyciu kodu asynchronicznego:</span><span class="sxs-lookup"><span data-stu-id="363b9-120">The following example uses asynchronous code to create a JSON file:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripToFileAsync.cs" id="Serialize":::

<span data-ttu-id="363b9-121">Powyższe przykłady używają wnioskowania typu dla serializowanego typu.</span><span class="sxs-lookup"><span data-stu-id="363b9-121">The preceding examples use type inference for the type being serialized.</span></span> <span data-ttu-id="363b9-122">Przeciążenie `Serialize()` przyjmuje parametr typu ogólnego:</span><span class="sxs-lookup"><span data-stu-id="363b9-122">An overload of `Serialize()` takes a generic type parameter:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripToString.cs" id="SerializeWithGenericParameter":::

### <a name="serialization-example"></a><span data-ttu-id="363b9-123">Przykład serializacji</span><span class="sxs-lookup"><span data-stu-id="363b9-123">Serialization example</span></span>

<span data-ttu-id="363b9-124">Oto przykładowa Klasa, która zawiera właściwości typu kolekcji i typ zdefiniowany przez użytkownika:</span><span class="sxs-lookup"><span data-stu-id="363b9-124">Here's an example class that contains collection-type properties and a user-defined type:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithPOCOs":::

> [!TIP]
> <span data-ttu-id="363b9-125">"POCO" oznacza dla [zwykłego starego obiektu CLR](https://en.wikipedia.org/wiki/Plain_old_CLR_object).</span><span class="sxs-lookup"><span data-stu-id="363b9-125">"POCO" stands for [plain old CLR object](https://en.wikipedia.org/wiki/Plain_old_CLR_object).</span></span> <span data-ttu-id="363b9-126">POCO to typ .NET, który nie jest zależny od żadnych typów specyficznych dla platformy, na przykład przez dziedziczenie lub atrybuty.</span><span class="sxs-lookup"><span data-stu-id="363b9-126">A POCO is a .NET type that doesn't depend on any framework-specific types, for example, through inheritance or attributes.</span></span>

<span data-ttu-id="363b9-127">Dane wyjściowe JSON serializowania wystąpienia poprzedniego typu wyglądają podobnie jak w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="363b9-127">The JSON output from serializing an instance of the preceding type looks like the following example.</span></span> <span data-ttu-id="363b9-128">Dane wyjściowe JSON to zminimalizowanego (odstępy, wcięcia i znaki nowego wiersza są domyślnie usuwane):</span><span class="sxs-lookup"><span data-stu-id="363b9-128">The JSON output is minified (whitespace, indentation, and new-line characters are removed) by default:</span></span>

```json
{"Date":"2019-08-01T00:00:00-07:00","TemperatureCelsius":25,"Summary":"Hot","DatesAvailable":["2019-08-01T00:00:00-07:00","2019-08-02T00:00:00-07:00"],"TemperatureRanges":{"Cold":{"High":20,"Low":-10},"Hot":{"High":60,"Low":20}},"SummaryWords":["Cool","Windy","Humid"]}
```

<span data-ttu-id="363b9-129">W poniższym przykładzie przedstawiono ten sam kod JSON, ale sformatowany (to jest, całkiem wydruk z odstępami i wcięciami):</span><span class="sxs-lookup"><span data-stu-id="363b9-129">The following example shows the same JSON, but formatted (that is, pretty-printed with whitespace and indentation):</span></span>

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

## <a name="serialize-to-utf-8"></a><span data-ttu-id="363b9-130">Serializacja do UTF-8</span><span class="sxs-lookup"><span data-stu-id="363b9-130">Serialize to UTF-8</span></span>

<span data-ttu-id="363b9-131">Aby serializować do UTF-8, wywołaj <xref:System.Text.Json.JsonSerializer.SerializeToUtf8Bytes%2A?displayProperty=nameWithType> metodę:</span><span class="sxs-lookup"><span data-stu-id="363b9-131">To serialize to UTF-8, call the <xref:System.Text.Json.JsonSerializer.SerializeToUtf8Bytes%2A?displayProperty=nameWithType> method:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripToUtf8.cs" id="Serialize":::

<span data-ttu-id="363b9-132"><xref:System.Text.Json.JsonSerializer.Serialize%2A>Dostępne jest również Przeciążenie, które trwa <xref:System.Text.Json.Utf8JsonWriter> .</span><span class="sxs-lookup"><span data-stu-id="363b9-132">A <xref:System.Text.Json.JsonSerializer.Serialize%2A> overload that takes a <xref:System.Text.Json.Utf8JsonWriter> is also available.</span></span>

<span data-ttu-id="363b9-133">Serializacja do UTF-8 jest szybsza o 5-10% niż przy użyciu metod opartych na ciągach.</span><span class="sxs-lookup"><span data-stu-id="363b9-133">Serializing to UTF-8 is about 5-10% faster than using the string-based methods.</span></span> <span data-ttu-id="363b9-134">Różnica polega na tym, że bajty (w formacie UTF-8) nie muszą być konwertowane na ciągi (UTF-16).</span><span class="sxs-lookup"><span data-stu-id="363b9-134">The difference is because the bytes (as UTF-8) don't need to be converted to strings (UTF-16).</span></span>

## <a name="serialization-behavior"></a><span data-ttu-id="363b9-135">Zachowanie serializacji</span><span class="sxs-lookup"><span data-stu-id="363b9-135">Serialization behavior</span></span>

::: zone pivot="dotnet-5-0"

* <span data-ttu-id="363b9-136">Domyślnie wszystkie właściwości publiczne są serializowane.</span><span class="sxs-lookup"><span data-stu-id="363b9-136">By default, all public properties are serialized.</span></span> <span data-ttu-id="363b9-137">Można [określić właściwości do ignorowania](system-text-json-ignore-properties.md).</span><span class="sxs-lookup"><span data-stu-id="363b9-137">You can [specify properties to ignore](system-text-json-ignore-properties.md).</span></span>
* <span data-ttu-id="363b9-138">[Domyślny koder](xref:System.Text.Encodings.Web.JavaScriptEncoder.Default) wyprowadza znaki nienależące do zestawu znaków ASCII, znaki z uwzględnieniem języka HTML w zakresie ASCII i znaków, które muszą zostać zmienione zgodnie z [specyfikacją JSON RFC 8259](https://tools.ietf.org/html/rfc8259#section-7).</span><span class="sxs-lookup"><span data-stu-id="363b9-138">The [default encoder](xref:System.Text.Encodings.Web.JavaScriptEncoder.Default) escapes non-ASCII characters, HTML-sensitive characters within the ASCII-range, and characters that must be escaped according to [the RFC 8259 JSON spec](https://tools.ietf.org/html/rfc8259#section-7).</span></span>
* <span data-ttu-id="363b9-139">Domyślnie JSON jest zminimalizowanego.</span><span class="sxs-lookup"><span data-stu-id="363b9-139">By default, JSON is minified.</span></span> <span data-ttu-id="363b9-140">Można tu [wydrukować kod JSON](#serialize-to-formatted-json).</span><span class="sxs-lookup"><span data-stu-id="363b9-140">You can [pretty-print the JSON](#serialize-to-formatted-json).</span></span>
* <span data-ttu-id="363b9-141">Domyślnie wielkość liter w nazwach JSON jest zgodna z nazwami .NET.</span><span class="sxs-lookup"><span data-stu-id="363b9-141">By default, casing of JSON names matches the .NET names.</span></span> <span data-ttu-id="363b9-142">Można [dostosować wielkość liter w nazwach JSON](system-text-json-customize-properties.md).</span><span class="sxs-lookup"><span data-stu-id="363b9-142">You can [customize JSON name casing](system-text-json-customize-properties.md).</span></span>
* <span data-ttu-id="363b9-143">Domyślnie wykryto odwołania cykliczne i zostały zgłoszone wyjątki.</span><span class="sxs-lookup"><span data-stu-id="363b9-143">By default, circular references are detected and exceptions thrown.</span></span> <span data-ttu-id="363b9-144">Można [zachować odwołania i obsłużyć odwołania cykliczne](system-text-json-preserve-references.md).</span><span class="sxs-lookup"><span data-stu-id="363b9-144">You can [preserve references and handle circular references](system-text-json-preserve-references.md).</span></span>
* <span data-ttu-id="363b9-145">Domyślnie [pola](../../csharp/programming-guide/classes-and-structs/fields.md) są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="363b9-145">By default, [fields](../../csharp/programming-guide/classes-and-structs/fields.md) are ignored.</span></span> <span data-ttu-id="363b9-146">Możesz [dołączyć pola](#include-fields).</span><span class="sxs-lookup"><span data-stu-id="363b9-146">You can [include fields](#include-fields).</span></span>

<span data-ttu-id="363b9-147">Jeśli używasz System.Text.Json bezpośrednio w aplikacji ASP.NET Core, niektóre domyślne zachowania są inne.</span><span class="sxs-lookup"><span data-stu-id="363b9-147">When you use System.Text.Json indirectly in an ASP.NET Core app, some default behaviors are different.</span></span> <span data-ttu-id="363b9-148">Aby uzyskać więcej informacji, zobacz [Ustawienia domyślne sieci Web dla JsonSerializerOptions](system-text-json-configure-options.md#web-defaults-for-jsonserializeroptions).</span><span class="sxs-lookup"><span data-stu-id="363b9-148">For more information, see [Web defaults for JsonSerializerOptions](system-text-json-configure-options.md#web-defaults-for-jsonserializeroptions).</span></span>
::: zone-end

::: zone pivot="dotnet-core-3-1"

* <span data-ttu-id="363b9-149">Domyślnie wszystkie właściwości publiczne są serializowane.</span><span class="sxs-lookup"><span data-stu-id="363b9-149">By default, all public properties are serialized.</span></span> <span data-ttu-id="363b9-150">Można [określić właściwości do ignorowania](system-text-json-ignore-properties.md).</span><span class="sxs-lookup"><span data-stu-id="363b9-150">You can [specify properties to ignore](system-text-json-ignore-properties.md).</span></span>
* <span data-ttu-id="363b9-151">[Domyślny koder](xref:System.Text.Encodings.Web.JavaScriptEncoder.Default) wyprowadza znaki nienależące do zestawu znaków ASCII, znaki z uwzględnieniem języka HTML w zakresie ASCII i znaków, które muszą zostać zmienione zgodnie z [specyfikacją JSON RFC 8259](https://tools.ietf.org/html/rfc8259#section-7).</span><span class="sxs-lookup"><span data-stu-id="363b9-151">The [default encoder](xref:System.Text.Encodings.Web.JavaScriptEncoder.Default) escapes non-ASCII characters, HTML-sensitive characters within the ASCII-range, and characters that must be escaped according to [the RFC 8259 JSON spec](https://tools.ietf.org/html/rfc8259#section-7).</span></span>
* <span data-ttu-id="363b9-152">Domyślnie JSON jest zminimalizowanego.</span><span class="sxs-lookup"><span data-stu-id="363b9-152">By default, JSON is minified.</span></span> <span data-ttu-id="363b9-153">Można tu [wydrukować kod JSON](#serialize-to-formatted-json).</span><span class="sxs-lookup"><span data-stu-id="363b9-153">You can [pretty-print the JSON](#serialize-to-formatted-json).</span></span>
* <span data-ttu-id="363b9-154">Domyślnie wielkość liter w nazwach JSON jest zgodna z nazwami .NET.</span><span class="sxs-lookup"><span data-stu-id="363b9-154">By default, casing of JSON names matches the .NET names.</span></span> <span data-ttu-id="363b9-155">Można [dostosować wielkość liter w nazwach JSON](system-text-json-customize-properties.md).</span><span class="sxs-lookup"><span data-stu-id="363b9-155">You can [customize JSON name casing](system-text-json-customize-properties.md).</span></span>
* <span data-ttu-id="363b9-156">Wykryto odwołania cykliczne i zostały zgłoszone wyjątki.</span><span class="sxs-lookup"><span data-stu-id="363b9-156">Circular references are detected and exceptions thrown.</span></span>
* <span data-ttu-id="363b9-157">[Pola](../../csharp/programming-guide/classes-and-structs/fields.md) są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="363b9-157">[Fields](../../csharp/programming-guide/classes-and-structs/fields.md) are ignored.</span></span>
::: zone-end

<span data-ttu-id="363b9-158">Obsługiwane typy to:</span><span class="sxs-lookup"><span data-stu-id="363b9-158">Supported types include:</span></span>
::: zone pivot="dotnet-5-0"

* <span data-ttu-id="363b9-159">Elementy podstawowe platformy .NET, które są mapowane na elementy podstawowe języka JavaScript, takie jak typy liczbowe, ciągi i wartości logiczne.</span><span class="sxs-lookup"><span data-stu-id="363b9-159">.NET primitives that map to JavaScript primitives, such as numeric types, strings, and Boolean.</span></span>
* <span data-ttu-id="363b9-160">Obiekty CLR zdefiniowane przez użytkownika [(POCOs)](https://en.wikipedia.org/wiki/Plain_old_CLR_object).</span><span class="sxs-lookup"><span data-stu-id="363b9-160">User-defined [plain old CLR objects (POCOs)](https://en.wikipedia.org/wiki/Plain_old_CLR_object).</span></span>
* <span data-ttu-id="363b9-161">Tablice jednowymiarowe i nieregularne ( `T[][]` ).</span><span class="sxs-lookup"><span data-stu-id="363b9-161">One-dimensional and jagged arrays (`T[][]`).</span></span>
* <span data-ttu-id="363b9-162">Kolekcje i słowniki z następujących przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="363b9-162">Collections and dictionaries from the following namespaces.</span></span>
  * <xref:System.Collections>
  * <xref:System.Collections.Generic>
  * <xref:System.Collections.Immutable>
  * <xref:System.Collections.Concurrent>
  * <xref:System.Collections.Specialized>
  * <xref:System.Collections.ObjectModel>
::: zone-end

::: zone pivot="dotnet-core-3-1"

* <span data-ttu-id="363b9-163">Elementy podstawowe platformy .NET, które są mapowane na elementy podstawowe języka JavaScript, takie jak typy liczbowe, ciągi i wartości logiczne.</span><span class="sxs-lookup"><span data-stu-id="363b9-163">.NET primitives that map to JavaScript primitives, such as numeric types, strings, and Boolean.</span></span>
* <span data-ttu-id="363b9-164">Obiekty CLR zdefiniowane przez użytkownika [(POCOs)](https://en.wikipedia.org/wiki/Plain_old_CLR_object).</span><span class="sxs-lookup"><span data-stu-id="363b9-164">User-defined [plain old CLR objects (POCOs)](https://en.wikipedia.org/wiki/Plain_old_CLR_object).</span></span>
* <span data-ttu-id="363b9-165">Tablice jednowymiarowe i nieregularne ( `ArrayName[][]` ).</span><span class="sxs-lookup"><span data-stu-id="363b9-165">One-dimensional and jagged arrays (`ArrayName[][]`).</span></span>
* <span data-ttu-id="363b9-166">`Dictionary<string,TValue>` gdzie `TValue` is to `object` , `JsonElement` lub poco.</span><span class="sxs-lookup"><span data-stu-id="363b9-166">`Dictionary<string,TValue>` where `TValue` is `object`, `JsonElement`, or a POCO.</span></span>
* <span data-ttu-id="363b9-167">Kolekcje z następujących przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="363b9-167">Collections from the following namespaces.</span></span>
  * <xref:System.Collections>
  * <xref:System.Collections.Generic>
  * <xref:System.Collections.Immutable>
  * <xref:System.Collections.Concurrent>
  * <xref:System.Collections.Specialized>
  * <xref:System.Collections.ObjectModel>
::: zone-end

<span data-ttu-id="363b9-168">Można [zaimplementować niestandardowe konwertery](system-text-json-converters-how-to.md) w celu obsługi dodatkowych typów lub zapewnienia funkcjonalności, która nie jest obsługiwana przez wbudowane konwertery.</span><span class="sxs-lookup"><span data-stu-id="363b9-168">You can [implement custom converters](system-text-json-converters-how-to.md) to handle additional types or to provide functionality that isn't supported by the built-in converters.</span></span>

## <a name="how-to-read-json-as-net-objects-deserialize"></a><span data-ttu-id="363b9-169">Jak odczytać dane JSON jako obiekty .NET (deserializacji)</span><span class="sxs-lookup"><span data-stu-id="363b9-169">How to read JSON as .NET objects (deserialize)</span></span>

<span data-ttu-id="363b9-170">Aby zdeserializować z ciągu lub pliku, wywołaj <xref:System.Text.Json.JsonSerializer.Deserialize%2A?displayProperty=nameWithType> metodę.</span><span class="sxs-lookup"><span data-stu-id="363b9-170">To deserialize from a string or a file, call the <xref:System.Text.Json.JsonSerializer.Deserialize%2A?displayProperty=nameWithType> method.</span></span>

<span data-ttu-id="363b9-171">Poniższy przykład odczytuje dane JSON z ciągu i tworzy wystąpienie `WeatherForecastWithPOCOs` klasy pokazanej wcześniej dla [przykładu serializacji](#serialization-example):</span><span class="sxs-lookup"><span data-stu-id="363b9-171">The following example reads JSON from a string and creates an instance of the `WeatherForecastWithPOCOs` class shown earlier for the [serialization example](#serialization-example):</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripToString.cs" id="Deserialize":::

<span data-ttu-id="363b9-172">Aby zdeserializować z pliku przy użyciu kodu synchronicznego, Odczytaj plik do ciągu, jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="363b9-172">To deserialize from a file by using synchronous code, read the file into a string, as shown in the following example:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripToFile.cs" id="Deserialize":::

<span data-ttu-id="363b9-173">Aby zdeserializować z pliku przy użyciu kodu asynchronicznego, wywołaj <xref:System.Text.Json.JsonSerializer.DeserializeAsync%2A> metodę:</span><span class="sxs-lookup"><span data-stu-id="363b9-173">To deserialize from a file by using asynchronous code, call the <xref:System.Text.Json.JsonSerializer.DeserializeAsync%2A> method:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripToFileAsync.cs" id="Deserialize":::

## <a name="deserialize-from-utf-8"></a><span data-ttu-id="363b9-174">Deserializacja z UTF-8</span><span class="sxs-lookup"><span data-stu-id="363b9-174">Deserialize from UTF-8</span></span>

<span data-ttu-id="363b9-175">Aby zdeserializować z UTF-8, wywołaj <xref:System.Text.Json.JsonSerializer.Deserialize%2A?displayProperty=nameWithType> Przeciążenie, które pobiera `ReadOnlySpan<byte>` lub a `Utf8JsonReader` , jak pokazano w poniższych przykładach.</span><span class="sxs-lookup"><span data-stu-id="363b9-175">To deserialize from UTF-8, call a <xref:System.Text.Json.JsonSerializer.Deserialize%2A?displayProperty=nameWithType> overload that takes a `ReadOnlySpan<byte>` or a `Utf8JsonReader`, as shown in the following examples.</span></span> <span data-ttu-id="363b9-176">W przykładach założono, że kod JSON znajduje się w tablicy bajtów o nazwie jsonUtf8Bytes.</span><span class="sxs-lookup"><span data-stu-id="363b9-176">The examples assume the JSON is in a byte array named jsonUtf8Bytes.</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripToUtf8.cs" id="Deserialize1":::

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripToUtf8.cs" id="Deserialize2":::

## <a name="deserialization-behavior"></a><span data-ttu-id="363b9-177">Zachowanie deserializacji</span><span class="sxs-lookup"><span data-stu-id="363b9-177">Deserialization behavior</span></span>

<span data-ttu-id="363b9-178">Podczas deserializacji kodu JSON stosowane są następujące zachowania:</span><span class="sxs-lookup"><span data-stu-id="363b9-178">The following behaviors apply when deserializing JSON:</span></span>

::: zone pivot="dotnet-5-0"

* <span data-ttu-id="363b9-179">Domyślnie w dopasowaniu nazw właściwości rozróżniana jest wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="363b9-179">By default, property name matching is case-sensitive.</span></span> <span data-ttu-id="363b9-180">Można [określić wielkość liter](system-text-json-character-casing.md).</span><span class="sxs-lookup"><span data-stu-id="363b9-180">You can [specify case-insensitivity](system-text-json-character-casing.md).</span></span>
* <span data-ttu-id="363b9-181">Jeśli kod JSON zawiera wartość właściwości tylko do odczytu, wartość jest ignorowana i nie jest zgłaszany żaden wyjątek.</span><span class="sxs-lookup"><span data-stu-id="363b9-181">If the JSON contains a value for a read-only property, the value is ignored and no exception is thrown.</span></span>
* <span data-ttu-id="363b9-182">Konstruktory niepubliczne są ignorowane przez serializator.</span><span class="sxs-lookup"><span data-stu-id="363b9-182">Non-public constructors are ignored by the serializer.</span></span>
* <span data-ttu-id="363b9-183">Obsługa deserializacji do niemodyfikowalnych obiektów lub właściwości tylko do odczytu jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="363b9-183">Deserialization to immutable objects or read-only properties is supported.</span></span> <span data-ttu-id="363b9-184">Zobacz [zmienne typy i rekordy](system-text-json-immutability.md).</span><span class="sxs-lookup"><span data-stu-id="363b9-184">See [Immutable types and Records](system-text-json-immutability.md).</span></span>
* <span data-ttu-id="363b9-185">Domyślnie wyliczenia są obsługiwane jako liczby.</span><span class="sxs-lookup"><span data-stu-id="363b9-185">By default, enums are supported as numbers.</span></span> <span data-ttu-id="363b9-186">[Nazwy wyliczenia można serializować jako ciągi](system-text-json-customize-properties.md#enums-as-strings).</span><span class="sxs-lookup"><span data-stu-id="363b9-186">You can [serialize enum names as strings](system-text-json-customize-properties.md#enums-as-strings).</span></span>
* <span data-ttu-id="363b9-187">Domyślnie pola są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="363b9-187">By default, fields are ignored.</span></span> <span data-ttu-id="363b9-188">Możesz [dołączyć pola](#include-fields).</span><span class="sxs-lookup"><span data-stu-id="363b9-188">You can [include fields](#include-fields).</span></span>
* <span data-ttu-id="363b9-189">Domyślnie komentarze lub końcowe przecinki w wyjątkach throw JSON.</span><span class="sxs-lookup"><span data-stu-id="363b9-189">By default, comments or trailing commas in the JSON throw exceptions.</span></span> <span data-ttu-id="363b9-190">Można [zezwolić na komentarze i końcowe przecinki](system-text-json-invalid-json.md).</span><span class="sxs-lookup"><span data-stu-id="363b9-190">You can [allow comments and trailing commas](system-text-json-invalid-json.md).</span></span>
* <span data-ttu-id="363b9-191">[Domyślna głębokość maksymalna](xref:System.Text.Json.JsonReaderOptions.MaxDepth) to 64.</span><span class="sxs-lookup"><span data-stu-id="363b9-191">The [default maximum depth](xref:System.Text.Json.JsonReaderOptions.MaxDepth) is 64.</span></span>

<span data-ttu-id="363b9-192">Jeśli używasz System.Text.Json bezpośrednio w aplikacji ASP.NET Core, niektóre domyślne zachowania są inne.</span><span class="sxs-lookup"><span data-stu-id="363b9-192">When you use System.Text.Json indirectly in an ASP.NET Core app, some default behaviors are different.</span></span> <span data-ttu-id="363b9-193">Aby uzyskać więcej informacji, zobacz [Ustawienia domyślne sieci Web dla JsonSerializerOptions](system-text-json-configure-options.md#web-defaults-for-jsonserializeroptions).</span><span class="sxs-lookup"><span data-stu-id="363b9-193">For more information, see [Web defaults for JsonSerializerOptions](system-text-json-configure-options.md#web-defaults-for-jsonserializeroptions).</span></span>
::: zone-end

::: zone pivot="dotnet-core-3-1"

* <span data-ttu-id="363b9-194">Domyślnie w dopasowaniu nazw właściwości rozróżniana jest wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="363b9-194">By default, property name matching is case-sensitive.</span></span> <span data-ttu-id="363b9-195">Można [określić wielkość liter](system-text-json-character-casing.md).</span><span class="sxs-lookup"><span data-stu-id="363b9-195">You can [specify case-insensitivity](system-text-json-character-casing.md).</span></span> <span data-ttu-id="363b9-196">Aplikacje ASP.NET Core [Domyślnie określają wielkość liter](system-text-json-configure-options.md#web-defaults-for-jsonserializeroptions).</span><span class="sxs-lookup"><span data-stu-id="363b9-196">ASP.NET Core apps [specify case-insensitivity by default](system-text-json-configure-options.md#web-defaults-for-jsonserializeroptions).</span></span>
* <span data-ttu-id="363b9-197">Jeśli kod JSON zawiera wartość właściwości tylko do odczytu, wartość jest ignorowana i nie jest zgłaszany żaden wyjątek.</span><span class="sxs-lookup"><span data-stu-id="363b9-197">If the JSON contains a value for a read-only property, the value is ignored and no exception is thrown.</span></span>
* <span data-ttu-id="363b9-198">Konstruktor bez parametrów, który może być publiczny, wewnętrzny lub prywatny, jest używany do deserializacji.</span><span class="sxs-lookup"><span data-stu-id="363b9-198">A parameterless constructor, which can be public, internal, or private, is used for deserialization.</span></span>
* <span data-ttu-id="363b9-199">Deserializacja z niezmiennymi obiektami lub właściwościami tylko do odczytu nie jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="363b9-199">Deserialization to immutable objects or read-only properties isn't supported.</span></span>
* <span data-ttu-id="363b9-200">Domyślnie wyliczenia są obsługiwane jako liczby.</span><span class="sxs-lookup"><span data-stu-id="363b9-200">By default, enums are supported as numbers.</span></span> <span data-ttu-id="363b9-201">[Nazwy wyliczenia można serializować jako ciągi](system-text-json-customize-properties.md#enums-as-strings).</span><span class="sxs-lookup"><span data-stu-id="363b9-201">You can [serialize enum names as strings](system-text-json-customize-properties.md#enums-as-strings).</span></span>
* <span data-ttu-id="363b9-202">Pola nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="363b9-202">Fields aren't supported.</span></span>
* <span data-ttu-id="363b9-203">Domyślnie komentarze lub końcowe przecinki w wyjątkach throw JSON.</span><span class="sxs-lookup"><span data-stu-id="363b9-203">By default, comments or trailing commas in the JSON throw exceptions.</span></span> <span data-ttu-id="363b9-204">Można [zezwolić na komentarze i końcowe przecinki](system-text-json-invalid-json.md).</span><span class="sxs-lookup"><span data-stu-id="363b9-204">You can [allow comments and trailing commas](system-text-json-invalid-json.md).</span></span>
* <span data-ttu-id="363b9-205">[Domyślna głębokość maksymalna](xref:System.Text.Json.JsonReaderOptions.MaxDepth) to 64.</span><span class="sxs-lookup"><span data-stu-id="363b9-205">The [default maximum depth](xref:System.Text.Json.JsonReaderOptions.MaxDepth) is 64.</span></span>

<span data-ttu-id="363b9-206">Jeśli używasz System.Text.Json bezpośrednio w aplikacji ASP.NET Core, niektóre domyślne zachowania są inne.</span><span class="sxs-lookup"><span data-stu-id="363b9-206">When you use System.Text.Json indirectly in an ASP.NET Core app, some default behaviors are different.</span></span> <span data-ttu-id="363b9-207">Aby uzyskać więcej informacji, zobacz [Ustawienia domyślne sieci Web dla JsonSerializerOptions](system-text-json-configure-options.md#web-defaults-for-jsonserializeroptions).</span><span class="sxs-lookup"><span data-stu-id="363b9-207">For more information, see [Web defaults for JsonSerializerOptions](system-text-json-configure-options.md#web-defaults-for-jsonserializeroptions).</span></span>
::: zone-end

<span data-ttu-id="363b9-208">[Konwertery niestandardowe można zaimplementować](system-text-json-converters-how-to.md) w celu zapewnienia funkcjonalności, która nie jest obsługiwana przez wbudowane konwertery.</span><span class="sxs-lookup"><span data-stu-id="363b9-208">You can [implement custom converters](system-text-json-converters-how-to.md) to provide functionality that isn't supported by the built-in converters.</span></span>

## <a name="serialize-to-formatted-json"></a><span data-ttu-id="363b9-209">Serializacja do sformatowanego pliku JSON</span><span class="sxs-lookup"><span data-stu-id="363b9-209">Serialize to formatted JSON</span></span>

<span data-ttu-id="363b9-210">Aby całkiem wydrukować dane wyjściowe JSON, ustaw wartość <xref:System.Text.Json.JsonSerializerOptions.WriteIndented?displayProperty=nameWithType> `true` :</span><span class="sxs-lookup"><span data-stu-id="363b9-210">To pretty-print the JSON output, set <xref:System.Text.Json.JsonSerializerOptions.WriteIndented?displayProperty=nameWithType> to `true`:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripToString.cs" id="SerializePrettyPrint":::

<span data-ttu-id="363b9-211">Oto przykład typu do serializacji i całkiem wydrukowanych danych wyjściowych JSON:</span><span class="sxs-lookup"><span data-stu-id="363b9-211">Here's an example type to be serialized and pretty-printed JSON output:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WF":::

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot"
}
```

## <a name="include-fields"></a><span data-ttu-id="363b9-212">Dołącz pola</span><span class="sxs-lookup"><span data-stu-id="363b9-212">Include fields</span></span>

::: zone pivot="dotnet-5-0"
<span data-ttu-id="363b9-213">Użyj <xref:System.Text.Json.JsonSerializerOptions.IncludeFields?displayProperty=nameWithType> Ustawienia globalnego lub atrybutu [[JsonInclude]](xref:System.Text.Json.Serialization.JsonIncludeAttribute) , aby dołączyć pola podczas serializacji lub deserializacji, jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="363b9-213">Use the <xref:System.Text.Json.JsonSerializerOptions.IncludeFields?displayProperty=nameWithType> global setting or the [[JsonInclude]](xref:System.Text.Json.Serialization.JsonIncludeAttribute) attribute to include fields when serializing or deserializing, as shown in the following example:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/Fields.cs" highlight="16,18,20,32-35":::

<span data-ttu-id="363b9-214">Aby zignorować pola tylko do odczytu, użyj <xref:System.Text.Json.JsonSerializerOptions.IgnoreReadOnlyFields%2A?displayProperty=nameWithType> Ustawienia globalnego.</span><span class="sxs-lookup"><span data-stu-id="363b9-214">To ignore read-only fields, use the <xref:System.Text.Json.JsonSerializerOptions.IgnoreReadOnlyFields%2A?displayProperty=nameWithType> global setting.</span></span>
::: zone-end

::: zone pivot="dotnet-core-3-1"
<span data-ttu-id="363b9-215">Pola nie są obsługiwane w System.Text.Json programie .NET Core 3,1.</span><span class="sxs-lookup"><span data-stu-id="363b9-215">Fields are not supported in System.Text.Json in .NET Core 3.1.</span></span> <span data-ttu-id="363b9-216">Te funkcje mogą zapewniać [konwertery niestandardowe](system-text-json-converters-how-to.md) .</span><span class="sxs-lookup"><span data-stu-id="363b9-216">[Custom converters](system-text-json-converters-how-to.md) can provide this functionality.</span></span>
::: zone-end

## <a name="httpclient-and-httpcontent-extension-methods"></a><span data-ttu-id="363b9-217">Metody rozszerzenia HttpClient i HttpContent</span><span class="sxs-lookup"><span data-stu-id="363b9-217">HttpClient and HttpContent extension methods</span></span>

::: zone pivot="dotnet-5-0"

<span data-ttu-id="363b9-218">Serializowanie i deserializacja ładunków JSON z sieci to typowe operacje.</span><span class="sxs-lookup"><span data-stu-id="363b9-218">Serializing and deserializing JSON payloads from the network are common operations.</span></span> <span data-ttu-id="363b9-219">Metody rozszerzające w [HttpClient](xref:System.Net.Http.Json.HttpClientJsonExtensions) i [HttpContent](xref:System.Net.Http.Json.HttpContentJsonExtensions) umożliwiają wykonywanie tych operacji w jednym wierszu kodu.</span><span class="sxs-lookup"><span data-stu-id="363b9-219">Extension methods on [HttpClient](xref:System.Net.Http.Json.HttpClientJsonExtensions) and [HttpContent](xref:System.Net.Http.Json.HttpContentJsonExtensions) let you do these operations in a single line of code.</span></span> <span data-ttu-id="363b9-220">Te metody rozszerzające używają [ustawień domyślnych sieci Web dla JsonSerializerOptions](system-text-json-configure-options.md#web-defaults-for-jsonserializeroptions).</span><span class="sxs-lookup"><span data-stu-id="363b9-220">These extension methods use [web defaults for JsonSerializerOptions](system-text-json-configure-options.md#web-defaults-for-jsonserializeroptions).</span></span>

<span data-ttu-id="363b9-221">Poniższy przykład ilustruje użycie <xref:System.Net.Http.Json.HttpClientJsonExtensions.GetFromJsonAsync%2A?displayProperty=nameWithType> i <xref:System.Net.Http.Json.HttpClientJsonExtensions.PostAsJsonAsync%2A?displayProperty=nameWithType> :</span><span class="sxs-lookup"><span data-stu-id="363b9-221">The following example illustrates use of <xref:System.Net.Http.Json.HttpClientJsonExtensions.GetFromJsonAsync%2A?displayProperty=nameWithType> and <xref:System.Net.Http.Json.HttpClientJsonExtensions.PostAsJsonAsync%2A?displayProperty=nameWithType>:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/HttpClientExtensionMethods.cs" highlight="26,33":::

<span data-ttu-id="363b9-222">Istnieją również metody rozszerzające dla System.Text.Json [HttpContent](xref:System.Net.Http.Json.HttpContentJsonExtensions).</span><span class="sxs-lookup"><span data-stu-id="363b9-222">There are also extension methods for System.Text.Json on [HttpContent](xref:System.Net.Http.Json.HttpContentJsonExtensions).</span></span>
::: zone-end

::: zone pivot="dotnet-core-3-1"
<span data-ttu-id="363b9-223">Metody rozszerzające w systemach `HttpClient` i `HttpContent` nie są dostępne w System.Text.Json programie .NET Core 3,1.</span><span class="sxs-lookup"><span data-stu-id="363b9-223">Extension methods on `HttpClient` and `HttpContent` are not available in System.Text.Json in .NET Core 3.1.</span></span>
::: zone-end

## <a name="see-also"></a><span data-ttu-id="363b9-224">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="363b9-224">See also</span></span>

* [<span data-ttu-id="363b9-225">System.Text.Json Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="363b9-225">System.Text.Json overview</span></span>](system-text-json-overview.md)
* [<span data-ttu-id="363b9-226">Jak pisać konwertery niestandardowe</span><span class="sxs-lookup"><span data-stu-id="363b9-226">How to write custom converters</span></span>](system-text-json-converters-how-to.md)
* [<span data-ttu-id="363b9-227">Jak przeprowadzić migrację z Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="363b9-227">How to migrate from Newtonsoft.Json</span></span>](system-text-json-migrate-from-newtonsoft-how-to.md)
* [<span data-ttu-id="363b9-228">Obsługa DateTime i DateTimeOffset w System.Text.Json</span><span class="sxs-lookup"><span data-stu-id="363b9-228">DateTime and DateTimeOffset support in System.Text.Json</span></span>](../datetime/system-text-json-support.md)
* <span data-ttu-id="363b9-229">[System.Text.Json Dokumentacja interfejsu API](xref:System.Text.Json)</span><span class="sxs-lookup"><span data-stu-id="363b9-229">[System.Text.Json API reference](xref:System.Text.Json)</span></span>
<!-- * [System.Text.Json roadmap](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/roadmap/README.md)-->
