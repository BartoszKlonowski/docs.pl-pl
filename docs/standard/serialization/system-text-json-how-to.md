---
title: Jak serializować kod JSON — .NET
author: tdykstra
ms.author: tdykstra
ms.date: 09/16/2019
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
ms.openlocfilehash: 8ccd7afe4abb928e7723aa740507774012fc85d1
ms.sourcegitcommit: a2d0e1f66367367065bc8dc0dde488ab536da73f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/18/2019
ms.locfileid: "71083109"
---
# <a name="how-to-serialize-json-in-net"></a><span data-ttu-id="6b951-102">Jak serializować kod JSON w programie .NET</span><span class="sxs-lookup"><span data-stu-id="6b951-102">How to serialize JSON in .NET</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6b951-103">Dokumentacja serializacji JSON jest w przygotowaniu.</span><span class="sxs-lookup"><span data-stu-id="6b951-103">The JSON serialization documentation is under construction.</span></span> <span data-ttu-id="6b951-104">Ten artykuł nie obejmuje wszystkich scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="6b951-104">This article doesn't cover all scenarios.</span></span> <span data-ttu-id="6b951-105">Aby uzyskać więcej informacji, należy zapoznać się z tematami [System. Text. JSON](https://github.com/dotnet/corefx/issues?q=is%3Aopen+is%3Aissue+label%3Aarea-System.Text.Json) w repozytorium dotnet/corefx w witrynie GitHub, w szczególności z etykietą [JSON-funkcja-doc](https://github.com/dotnet/corefx/labels/json-functionality-doc).</span><span class="sxs-lookup"><span data-stu-id="6b951-105">For more information, examine [System.Text.Json issues](https://github.com/dotnet/corefx/issues?q=is%3Aopen+is%3Aissue+label%3Aarea-System.Text.Json) in the dotnet/corefx repository on GitHub, especially those labeled [json-functionality-doc](https://github.com/dotnet/corefx/labels/json-functionality-doc).</span></span>

<span data-ttu-id="6b951-106">W tym artykule pokazano, <xref:System.Text.Json> jak używać przestrzeni nazw do serializacji i deserializacji do i z JavaScript Object Notation (JSON).</span><span class="sxs-lookup"><span data-stu-id="6b951-106">This article shows how to use the <xref:System.Text.Json> namespace to serialize and deserialize to and from JavaScript Object Notation (JSON).</span></span> <span data-ttu-id="6b951-107">Instrukcje i przykładowy kod używają biblioteki bezpośrednio, a nie za pomocą struktury, takiej jak [ASP.NET Core](/aspnet/core/).</span><span class="sxs-lookup"><span data-stu-id="6b951-107">The directions and sample code use the library directly, not through a framework such as [ASP.NET Core](/aspnet/core/).</span></span>

## <a name="namespaces"></a><span data-ttu-id="6b951-108">Namespaces</span><span class="sxs-lookup"><span data-stu-id="6b951-108">Namespaces</span></span>

<span data-ttu-id="6b951-109"><xref:System.Text.Json> Przestrzeń nazw zawiera wszystkie punkty wejścia i typy główne.</span><span class="sxs-lookup"><span data-stu-id="6b951-109">The <xref:System.Text.Json> namespace contains all the entry points and the main types.</span></span> <span data-ttu-id="6b951-110"><xref:System.Text.Json.Serialization> Przestrzeń nazw zawiera atrybuty i interfejsy API dla zaawansowanych scenariuszy i dostosowań specyficznych dla serializacji i deserializacji.</span><span class="sxs-lookup"><span data-stu-id="6b951-110">The <xref:System.Text.Json.Serialization> namespace contains attributes and APIs for advanced scenarios and customization specific to serialization and deserialization.</span></span> <span data-ttu-id="6b951-111">W związku z tym przykłady kodu przedstawione w tym artykule wymagają jednej lub obu następujących `using` dyrektyw:</span><span class="sxs-lookup"><span data-stu-id="6b951-111">Therefore, the code examples shown in this article require one or both of the following `using` directives:</span></span>

```csharp
using System.Text.Json;
using System.Text.Json.Serialization;
```

<span data-ttu-id="6b951-112">Atrybuty z <xref:System.Runtime.Serialization> przestrzeni nazw nie są obecnie obsługiwane `System.Text.Json`w programie.</span><span class="sxs-lookup"><span data-stu-id="6b951-112">Attributes from the <xref:System.Runtime.Serialization> namespace aren't currently supported in `System.Text.Json`.</span></span>

## <a name="how-to-write-net-objects-to-json-serialize"></a><span data-ttu-id="6b951-113">Pisanie obiektów .NET w formacie JSON (Serializacja)</span><span class="sxs-lookup"><span data-stu-id="6b951-113">How to write .NET objects to JSON (serialize)</span></span>

<span data-ttu-id="6b951-114">Aby zapisać kod JSON w ciągu, wywołaj <xref:System.Text.Json.JsonSerializer.Serialize%2A?displayProperty=nameWithType> metodę.</span><span class="sxs-lookup"><span data-stu-id="6b951-114">To write JSON to a string, call the <xref:System.Text.Json.JsonSerializer.Serialize%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="6b951-115">Poniższy przykład używa przeciążenia z parametrem typu ogólnego:</span><span class="sxs-lookup"><span data-stu-id="6b951-115">The following example uses an overload with a generic type parameter:</span></span>

```csharp
WeatherForecast weatherForecast;
//...
string json = JsonSerializer.Serialize<WeatherForecast>(weatherForecast);
```

<span data-ttu-id="6b951-116">Można pominąć parametr typu ogólnego i zamiast tego użyć ogólnego wnioskowania o typie:</span><span class="sxs-lookup"><span data-stu-id="6b951-116">You can omit the generic type parameter and use generic type inference instead:</span></span>

```csharp
WeatherForecast weatherForecast;
//...
string json = JsonSerializer.Serialize(weatherForecast);
```

<span data-ttu-id="6b951-117">Oto przykład typu do serializacji, który zawiera kolekcje i klasy zagnieżdżone:</span><span class="sxs-lookup"><span data-stu-id="6b951-117">Here's an example type to be serialized, which contains collections and nested classes:</span></span>

```csharp
public class WeatherForecast
{
    public DateTimeOffset Date { get; set; }
    public int TemperatureC { get; set; }
    public string Summary { get; set; }
    public IList<DateTimeOffset> DatesAvailable { get; set;}
    public Dictionary<string, HighLowTemperatures> TemperatureRanges { get; set; }
    public string [] SummaryWords { get; set; }
}

public class HighLowTemperatures
{
    public Temperature High { get; set; }
    public Temperature Low { get; set; }
}

public class Temperature
{
    public int DegreesCelsius { get; set; }
}
```

<span data-ttu-id="6b951-118">Dane wyjściowe JSON domyślnie są zminimalizowanego:</span><span class="sxs-lookup"><span data-stu-id="6b951-118">The JSON output is minified by default:</span></span> 

```json
{"Date":"2019-08-01T00:00:00-07:00","TemperatureC":25,"Summary":"Hot","DatesAvailable":["2019-08-01T00:00:00-07:00","2019-08-02T00:00:00-07:00"],"TemperatureRanges":{"Cold":{"High":{"DegreesCelsius":20},"Low":{"DegreesCelsius":-10}},"Hot":{"High":{"DegreesCelsius":60},"Low":{"DegreesCelsius":20}}},"SummaryWords":["Cool","Windy","Humid"]}
```

<span data-ttu-id="6b951-119">W poniższym przykładzie przedstawiono ten sam kod JSON, sformatowany (to jest całkiem wydruk z odstępami i wcięciami):</span><span class="sxs-lookup"><span data-stu-id="6b951-119">The following example shows the same JSON, formatted (that is, pretty-printed with whitespace and indentation):</span></span>

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureC": 25,
  "Summary": "Hot",
  "DatesAvailable": [
    "2019-08-01T00:00:00-07:00",
    "2019-08-02T00:00:00-07:00"
  ],
  "TemperatureRanges": {
    "Cold": {
      "High": {
        "DegreesCelsius": 20
      },
      "Low": {
        "DegreesCelsius": -10
      }
    },
    "Hot": {
      "High": {
        "DegreesCelsius": 60
      },
      "Low": {
        "DegreesCelsius": 20
      }
    }
  },
  "SummaryWords": [
    "Cool",
    "Windy",
    "Humid"
  ]
}
```

<span data-ttu-id="6b951-120">Przeciążenia można serializować <xref:System.IO.Stream>do. <xref:System.Text.Json.JsonSerializer.Serialize%2A></span><span class="sxs-lookup"><span data-stu-id="6b951-120">Overloads of <xref:System.Text.Json.JsonSerializer.Serialize%2A> let you serialize to a <xref:System.IO.Stream>.</span></span> <span data-ttu-id="6b951-121">Asynchroniczne wersje `Stream` przeciążeń są dostępne.</span><span class="sxs-lookup"><span data-stu-id="6b951-121">Async versions of the `Stream` overloads are available.</span></span>

### <a name="serialize-to-utf-8"></a><span data-ttu-id="6b951-122">Serializacja do UTF-8</span><span class="sxs-lookup"><span data-stu-id="6b951-122">Serialize to UTF-8</span></span>

<span data-ttu-id="6b951-123">Aby serializować do UTF-8, wywołaj <xref:System.Text.Json.JsonSerializer.SerializeToUtf8Bytes%2A?displayProperty=nameWithType> metodę:</span><span class="sxs-lookup"><span data-stu-id="6b951-123">To serialize to UTF-8, call the <xref:System.Text.Json.JsonSerializer.SerializeToUtf8Bytes%2A?displayProperty=nameWithType> method:</span></span>

```csharp
byte[] utf8Json = JsonSerializer.SerializeToUtf8Bytes<WeatherForecast>(weatherForecast);
```

<span data-ttu-id="6b951-124">Alternatywnie, <xref:System.Text.Json.JsonSerializer.Serialize%2A> Przeciążenie, które <xref:System.Text.Json.Utf8JsonWriter> trwa, jest dostępne.</span><span class="sxs-lookup"><span data-stu-id="6b951-124">As an alternative, a <xref:System.Text.Json.JsonSerializer.Serialize%2A> overload that takes a <xref:System.Text.Json.Utf8JsonWriter> is available.</span></span>

<span data-ttu-id="6b951-125">Serializacja do UTF-8 jest szybsza o 5-10% niż przy użyciu metod opartych na ciągach.</span><span class="sxs-lookup"><span data-stu-id="6b951-125">Serializing to UTF-8 is about 5-10% faster than using the string-based methods.</span></span> <span data-ttu-id="6b951-126">Różnica polega na tym, że bajty (w formacie UTF-8) nie muszą być konwertowane na ciągi (UTF-16).</span><span class="sxs-lookup"><span data-stu-id="6b951-126">The difference is because the bytes (as UTF-8) don't need to be converted to strings (UTF-16).</span></span>

## <a name="serialization-behavior"></a><span data-ttu-id="6b951-127">Zachowanie serializacji</span><span class="sxs-lookup"><span data-stu-id="6b951-127">Serialization behavior</span></span>

* <span data-ttu-id="6b951-128">Domyślnie wszystkie właściwości publiczne są serializowane.</span><span class="sxs-lookup"><span data-stu-id="6b951-128">By default, all public properties are serialized.</span></span> <span data-ttu-id="6b951-129">Można [określić właściwości do wykluczenia](#exclude-properties).</span><span class="sxs-lookup"><span data-stu-id="6b951-129">You can [specify properties to exclude](#exclude-properties).</span></span>
* <span data-ttu-id="6b951-130">[Domyślny koder](xref:System.Text.Encodings.Web.JavaScriptEncoder.Default) wyprowadza znaki nienależące do zestawu znaków ASCII, znaki z uwzględnieniem kodu HTML w zakresie ASCII i znaków, które muszą zostać zmienione zgodnie z [specyfikacją JSON](https://tools.ietf.org/html/rfc8259#section-7).</span><span class="sxs-lookup"><span data-stu-id="6b951-130">The [default encoder](xref:System.Text.Encodings.Web.JavaScriptEncoder.Default) escapes non-ASCII characters, HTML-sensitive characters within the ASCII-range, and characters that must be escaped according to [the JSON spec](https://tools.ietf.org/html/rfc8259#section-7).</span></span>
* <span data-ttu-id="6b951-131">Domyślnie JSON jest zminimalizowanego.</span><span class="sxs-lookup"><span data-stu-id="6b951-131">By default, JSON is minified.</span></span> <span data-ttu-id="6b951-132">Można tu [wydrukować kod JSON](#serialize-to-formatted-json).</span><span class="sxs-lookup"><span data-stu-id="6b951-132">You can [pretty-print the JSON](#serialize-to-formatted-json).</span></span>
* <span data-ttu-id="6b951-133">Domyślnie wielkość liter w nazwach JSON jest zgodna z nazwami .NET.</span><span class="sxs-lookup"><span data-stu-id="6b951-133">By default, casing of JSON names matches the .NET names.</span></span> <span data-ttu-id="6b951-134">Można [dostosować wielkość liter w nazwach JSON](#customize-json-names).</span><span class="sxs-lookup"><span data-stu-id="6b951-134">You can [customize JSON name casing](#customize-json-names).</span></span>
* <span data-ttu-id="6b951-135">Wykryto odwołania cykliczne i zostały zgłoszone wyjątki.</span><span class="sxs-lookup"><span data-stu-id="6b951-135">Circular references are detected and exceptions thrown.</span></span> <span data-ttu-id="6b951-136">Aby uzyskać więcej informacji, zobacz [problem dotyczący odwołań cyklicznych](https://github.com/dotnet/corefx/issues/38579) w repozytorium dotnet/corefx w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="6b951-136">For more information, see the [issue on circular references](https://github.com/dotnet/corefx/issues/38579) in the dotnet/corefx repository on GitHub.</span></span>
* <span data-ttu-id="6b951-137">Obecnie pola są wykluczone.</span><span class="sxs-lookup"><span data-stu-id="6b951-137">Currently, fields are excluded.</span></span>

<span data-ttu-id="6b951-138">Obsługiwane typy to:</span><span class="sxs-lookup"><span data-stu-id="6b951-138">Supported types include:</span></span>

* <span data-ttu-id="6b951-139">Elementy podstawowe platformy .NET, które są mapowane na elementy podstawowe języka JavaScript, takie jak typy liczbowe, ciągi i wartości logiczne.</span><span class="sxs-lookup"><span data-stu-id="6b951-139">.NET primitives that map to JavaScript primitives, such as numeric types, strings, and Boolean.</span></span>
* <span data-ttu-id="6b951-140">Obiekty CLR zdefiniowane przez użytkownika [(POCOs)](https://stackoverflow.com/questions/250001/poco-definition).</span><span class="sxs-lookup"><span data-stu-id="6b951-140">User-defined [Plain Old CLR Objects (POCOs)](https://stackoverflow.com/questions/250001/poco-definition).</span></span>
* <span data-ttu-id="6b951-141">Tablice jednowymiarowe i nieregularne (`ArrayName[][]`).</span><span class="sxs-lookup"><span data-stu-id="6b951-141">One-dimensional and jagged arrays (`ArrayName[][]`).</span></span>
* <span data-ttu-id="6b951-142">`Dictionary<string,TValue>`gdzie `TValue` is `object`to ,`JsonElement`lub poco.</span><span class="sxs-lookup"><span data-stu-id="6b951-142">`Dictionary<string,TValue>` where `TValue` is `object`, `JsonElement`, or a POCO.</span></span>
* <span data-ttu-id="6b951-143">Kolekcje z następujących przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="6b951-143">Collections from the following namespaces.</span></span> <span data-ttu-id="6b951-144">Aby uzyskać więcej informacji, zobacz [problem związany z obsługą kolekcji](https://github.com/dotnet/corefx/issues/36643) w repozytorium dotnet/corefx w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="6b951-144">For more information, see the [issue on collection support](https://github.com/dotnet/corefx/issues/36643) in the dotnet/corefx repository on GitHub.</span></span>
  * <xref:System.Collections>
  * <xref:System.Collections.Generic>
  * <xref:System.Collections.Immutable>

## <a name="how-to-read-json-into-net-objects-deserialize"></a><span data-ttu-id="6b951-145">Jak odczytywać dane JSON do obiektów .NET (deserializacji)</span><span class="sxs-lookup"><span data-stu-id="6b951-145">How to read JSON into .NET objects (deserialize)</span></span>

<span data-ttu-id="6b951-146">Aby zdeserializować z ciągu, wywołaj <xref:System.Text.Json.JsonSerializer.Deserialize%2A?displayProperty=nameWithType> metodę, jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="6b951-146">To deserialize from a string, call the <xref:System.Text.Json.JsonSerializer.Deserialize%2A?displayProperty=nameWithType> method, as shown in the following example:</span></span>

```csharp
string json = ... ;

var weatherForecast = JsonSerializer.Deserialize<WeatherForecast>(json);
```

<span data-ttu-id="6b951-147">Aby zapoznać się z przykładem, zapoznaj się z sekcją [serializacji](#how-to-write-net-objects-to-json-serialize) .</span><span class="sxs-lookup"><span data-stu-id="6b951-147">For an example, see the [serialize](#how-to-write-net-objects-to-json-serialize) section.</span></span> <span data-ttu-id="6b951-148">Obiekty JSON i .NET są takie same, ale kierunek jest odwrócony.</span><span class="sxs-lookup"><span data-stu-id="6b951-148">The JSON and .NET object are the same, but the direction is reversed.</span></span>

<span data-ttu-id="6b951-149">Przeciążenia programu <xref:System.Text.Json.JsonSerializer.Deserialize*> umożliwiają deserializacji `Stream`z.</span><span class="sxs-lookup"><span data-stu-id="6b951-149">Overloads of <xref:System.Text.Json.JsonSerializer.Deserialize*> let you deserialize from a `Stream`.</span></span>  <span data-ttu-id="6b951-150">Asynchroniczne wersje `Stream` przeciążeń są dostępne.</span><span class="sxs-lookup"><span data-stu-id="6b951-150">Async versions of the `Stream` overloads are available.</span></span>

### <a name="deserialize-from-utf-8"></a><span data-ttu-id="6b951-151">Deserializacja z UTF-8</span><span class="sxs-lookup"><span data-stu-id="6b951-151">Deserialize from UTF-8</span></span>

<span data-ttu-id="6b951-152">Aby zdeserializować z UTF-8, wywołaj <xref:System.Text.Json.JsonSerializer.Deserialize%2A?displayProperty=nameWithType> Przeciążenie, które `Utf8JsonReader` przyjmuje lub a `ReadOnlySpan<byte>`, jak pokazano w następujących przykładach:</span><span class="sxs-lookup"><span data-stu-id="6b951-152">To deserialize from UTF-8, call a <xref:System.Text.Json.JsonSerializer.Deserialize%2A?displayProperty=nameWithType> overload that takes a `Utf8JsonReader` or a `ReadOnlySpan<byte>`, as shown in the following examples:</span></span>

```csharp
byte[] utf8Json;
//...
var readOnlySpan = new ReadOnlySpan<byte>(utf8Json);
weatherForecast = JsonSerializer.Deserialize<WeatherForecastMin>(readOnlySpan);
```

```csharp
byte[] utf8Json;
//...
var utf8Reader = new Utf8JsonReader(utf8Json);
weatherForecast = JsonSerializer.Deserialize<WeatherForecastMin>(ref utf8Reader);
```

## <a name="deserialization-behavior"></a><span data-ttu-id="6b951-153">Zachowanie deserializacji</span><span class="sxs-lookup"><span data-stu-id="6b951-153">Deserialization behavior</span></span>

* <span data-ttu-id="6b951-154">Domyślnie w dopasowaniu nazw właściwości rozróżniana jest wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="6b951-154">By default, property name matching is case-sensitive.</span></span> <span data-ttu-id="6b951-155">Można [określić wielkość liter](#case-insensitive-property-matching).</span><span class="sxs-lookup"><span data-stu-id="6b951-155">You can [specify case-insensitivity](#case-insensitive-property-matching).</span></span>
* <span data-ttu-id="6b951-156">Jeśli kod JSON zawiera wartość właściwości tylko do odczytu, wartość jest ignorowana i nie jest zgłaszany żaden wyjątek.</span><span class="sxs-lookup"><span data-stu-id="6b951-156">If the JSON contains a value for a read-only property, the value is ignored and no exception is thrown.</span></span>
* <span data-ttu-id="6b951-157">Deserializacja do typów referencyjnych bez bezparametrowego konstruktora nie jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="6b951-157">Deserialization to reference types without a parameterless constructor isn't supported.</span></span>
* <span data-ttu-id="6b951-158">Deserializacja z niezmiennymi obiektami lub właściwościami tylko do odczytu nie jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="6b951-158">Deserialization to immutable objects or read-only properties isn't supported.</span></span> <span data-ttu-id="6b951-159">Aby uzyskać więcej informacji, zobacz [problem z obsługą usługi GitHub dla niemodyfikowalnych obiektów](https://github.com/dotnet/corefx/issues/38569) i [problem związany z obsługą właściwości tylko do odczytu](https://github.com/dotnet/corefx/issues/38163) w repozytorium dotnet/corefx w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="6b951-159">For more information, see the GitHub [issue on immutable object support](https://github.com/dotnet/corefx/issues/38569) and the [issue on read-only property support](https://github.com/dotnet/corefx/issues/38163) in the dotnet/corefx repository on GitHub.</span></span>
* <span data-ttu-id="6b951-160">Domyślnie wyliczenia są obsługiwane jako liczby.</span><span class="sxs-lookup"><span data-stu-id="6b951-160">By default, enums are supported as numbers.</span></span>
* <span data-ttu-id="6b951-161">Pola nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="6b951-161">Fields aren't supported.</span></span>
* <span data-ttu-id="6b951-162">Domyślnie komentarze lub końcowe przecinki w wyjątkach throw JSON.</span><span class="sxs-lookup"><span data-stu-id="6b951-162">By default, comments or trailing commas in the JSON throw exceptions.</span></span> <span data-ttu-id="6b951-163">W razie konieczności można [zezwolić na komentarze i końcowe przecinki](#allow-comments-and-trailing-commas) .</span><span class="sxs-lookup"><span data-stu-id="6b951-163">You can [allow comments and trailing commas](#allow-comments-and-trailing-commas) if needed.</span></span>
* <span data-ttu-id="6b951-164">[Domyślna głębokość maksymalna](xref:System.Text.Json.JsonReaderOptions.MaxDepth) to 64.</span><span class="sxs-lookup"><span data-stu-id="6b951-164">The [default maximum depth](xref:System.Text.Json.JsonReaderOptions.MaxDepth) is 64.</span></span>

## <a name="serialize-to-formatted-json"></a><span data-ttu-id="6b951-165">Serializacja do sformatowanego pliku JSON</span><span class="sxs-lookup"><span data-stu-id="6b951-165">Serialize to formatted JSON</span></span>

<span data-ttu-id="6b951-166">Aby całkiem wydrukować dane wyjściowe JSON, ustaw wartość <xref:System.Text.Json.JsonSerializerOptions.WriteIndented?displayProperty=nameWithType>: `true`</span><span class="sxs-lookup"><span data-stu-id="6b951-166">To pretty-print the JSON output, set <xref:System.Text.Json.JsonSerializerOptions.WriteIndented?displayProperty=nameWithType> to `true`:</span></span>

```csharp
var options = new JsonSerializerOptions
{
    WriteIndented = true,
};
json = JsonSerializer.Serialize(weatherForecast, options);
```

<span data-ttu-id="6b951-167">Oto przykład typu do serializacji i danych wyjściowych JSON:</span><span class="sxs-lookup"><span data-stu-id="6b951-167">Here's an example type to be serialized and JSON output:</span></span>

```csharp
class WeatherForecast
{
    public DateTimeOffset Date { get; set; }
    public int TemperatureC { get; set; }
    public string Summary { get; set; }
}
```

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureC": 25,
  "Summary": "Hot"
}
```

## <a name="allow-comments-and-trailing-commas"></a><span data-ttu-id="6b951-168">Zezwalaj na komentarze i końcowe przecinki</span><span class="sxs-lookup"><span data-stu-id="6b951-168">Allow comments and trailing commas</span></span>

<span data-ttu-id="6b951-169">Domyślnie Komentarze i końcowe przecinki są niedozwolone w notacji JSON.</span><span class="sxs-lookup"><span data-stu-id="6b951-169">By default comments and trailing commas are not allowed in JSON.</span></span> <span data-ttu-id="6b951-170">Aby zezwolić na komentarze w formacie JSON, ustaw <xref:System.Text.Json.JsonSerializerOptions.ReadCommentHandling?displayProperty=nameWithType> właściwość na `JsonCommentHandling.Skip`.</span><span class="sxs-lookup"><span data-stu-id="6b951-170">To allow comments in the JSON, set the <xref:System.Text.Json.JsonSerializerOptions.ReadCommentHandling?displayProperty=nameWithType> property to `JsonCommentHandling.Skip`.</span></span> <span data-ttu-id="6b951-171">I aby zezwolić na końcowe przecinki, należy ustawić <xref:System.Text.Json.JsonSerializerOptions.AllowTrailingCommas?displayProperty=nameWithType> właściwość na `true`.</span><span class="sxs-lookup"><span data-stu-id="6b951-171">And to allow trailing commas, set the <xref:System.Text.Json.JsonSerializerOptions.AllowTrailingCommas?displayProperty=nameWithType> property to `true`.</span></span> <span data-ttu-id="6b951-172">Poniższy przykład pokazuje, jak:</span><span class="sxs-lookup"><span data-stu-id="6b951-172">The following example shows how to allow both:</span></span>

```csharp
var options = new JsonSerializerOptions
{
    ReadCommentHandling = JsonCommentHandling.Skip,
    AllowTrailingCommas = true
};
var weatherForecast = JsonSerializer.Deserialize<WeatherForecast>(json);
```

<span data-ttu-id="6b951-173">Oto przykładowy kod JSON z komentarzami i końcowym przecinkiem:</span><span class="sxs-lookup"><span data-stu-id="6b951-173">Here's example JSON with comments and a trailing comma:</span></span>

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureC": 25, // Fahrenheit 77
  "Summary": "Hot", /* Zharko */
}
```

## <a name="customize-json-names"></a><span data-ttu-id="6b951-174">Dostosuj nazwy JSON</span><span class="sxs-lookup"><span data-stu-id="6b951-174">Customize JSON names</span></span>

<span data-ttu-id="6b951-175">Domyślnie nazwy właściwości i klucze słownika nie są zmieniane w danych wyjściowych JSON, włącznie z wielkością liter.</span><span class="sxs-lookup"><span data-stu-id="6b951-175">By default, property names and dictionary keys are unchanged in the JSON output, including case.</span></span> <span data-ttu-id="6b951-176">W tej sekcji wyjaśniono, jak:</span><span class="sxs-lookup"><span data-stu-id="6b951-176">This section explains how to:</span></span>

* <span data-ttu-id="6b951-177">Dostosowywanie poszczególnych nazw właściwości</span><span class="sxs-lookup"><span data-stu-id="6b951-177">Customize individual property names</span></span>
* <span data-ttu-id="6b951-178">Konwertuj wszystkie nazwy właściwości na notacji CamelCase przypadku</span><span class="sxs-lookup"><span data-stu-id="6b951-178">Convert all property names to camel case</span></span>
* <span data-ttu-id="6b951-179">Implementowanie zasad nazewnictwa właściwości niestandardowych</span><span class="sxs-lookup"><span data-stu-id="6b951-179">Implement a custom property naming policy</span></span>
* <span data-ttu-id="6b951-180">Konwertuj klucze słownika na notacji CamelCase</span><span class="sxs-lookup"><span data-stu-id="6b951-180">Convert dictionary keys to camel case</span></span>

<span data-ttu-id="6b951-181">Obecnie nie jest obsługiwane automatyczne konwertowanie tekstów stałych na notacji CamelCase przypadku.</span><span class="sxs-lookup"><span data-stu-id="6b951-181">Currently, there's no support for automatically converting enums to camel case.</span></span> <span data-ttu-id="6b951-182">Aby uzyskać więcej informacji, zapoznaj się z tematem [problem związany z obsługą przypadku wyliczeniowego notacji CamelCase](https://github.com/dotnet/corefx/issues/37725) w repozytorium dotnet/corefx w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="6b951-182">For more information, see the [issue on enum camel case support](https://github.com/dotnet/corefx/issues/37725) in the dotnet/corefx repository on GitHub.</span></span>

### <a name="customize-individual-property-names"></a><span data-ttu-id="6b951-183">Dostosowywanie poszczególnych nazw właściwości</span><span class="sxs-lookup"><span data-stu-id="6b951-183">Customize individual property names</span></span>

<span data-ttu-id="6b951-184">Aby ustawić nazwę poszczególnych właściwości, Użyj atrybutu [[JsonPropertyName]](xref:System.Text.Json.Serialization.JsonPropertyNameAttribute) .</span><span class="sxs-lookup"><span data-stu-id="6b951-184">To set the name of individual properties, use the [[JsonPropertyName]](xref:System.Text.Json.Serialization.JsonPropertyNameAttribute) attribute.</span></span>

<span data-ttu-id="6b951-185">Oto przykład typu do serializacji i powstającego JSON:</span><span class="sxs-lookup"><span data-stu-id="6b951-185">Here's an example type to serialize and resulting JSON:</span></span>

```csharp
class WeatherForecast
{
    public DateTimeOffset Date { get; set; }
    public int TemperatureC { get; set; }
    public string Summary { get; set; }
    [JsonPropertyName("Wind")]
    public int WindSpeed { get; set; }
}
```

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureC": 25,
  "Summary": "Hot",
  "Wind": 35
}
```

<span data-ttu-id="6b951-186">Nazwa właściwości ustawiona przez ten atrybut:</span><span class="sxs-lookup"><span data-stu-id="6b951-186">The property name set by this attribute:</span></span>

* <span data-ttu-id="6b951-187">Stosuje się w obu kierunkach dla serializacji i deserializacji.</span><span class="sxs-lookup"><span data-stu-id="6b951-187">Applies in both directions, for serialization and deserialization.</span></span>
* <span data-ttu-id="6b951-188">Ma pierwszeństwo przed zasadami nazewnictwa właściwości.</span><span class="sxs-lookup"><span data-stu-id="6b951-188">Takes precedence over property naming policies.</span></span>

### <a name="use-camel-case-for-all-json-property-names"></a><span data-ttu-id="6b951-189">Użyj notacji CamelCase przypadku dla wszystkich nazw właściwości JSON</span><span class="sxs-lookup"><span data-stu-id="6b951-189">Use camel case for all JSON property names</span></span>

<span data-ttu-id="6b951-190">Aby użyć notacji CamelCase przypadku wszystkich nazw właściwości JSON, ustaw wartość <xref:System.Text.Json.JsonSerializerOptions.PropertyNamingPolicy?displayProperty=nameWithType> `JsonNamingPolicy.CamelCase`tak, jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="6b951-190">To use camel case for all JSON property names, set <xref:System.Text.Json.JsonSerializerOptions.PropertyNamingPolicy?displayProperty=nameWithType> to `JsonNamingPolicy.CamelCase`, as shown in the following example:</span></span>

```csharp
var options = new JsonSerializerOptions
{
    PropertyNamingPolicy = JsonNamingPolicy.CamelCase
};
json = JsonSerializer.Serialize(weatherForecast, options);
```

<span data-ttu-id="6b951-191">Oto przykładowa Klasa do serializacji i danych wyjściowych JSON:</span><span class="sxs-lookup"><span data-stu-id="6b951-191">Here's an example class to serialize and JSON output:</span></span>

```csharp
class WeatherForecast
{
    public DateTimeOffset Date { get; set; }
    public int TemperatureC { get; set; }
    public string Summary { get; set; }
    [JsonPropertyName("Wind")]
    public int WindSpeed { get; set; }
}
```

```json
{
  "date": "2019-08-01T00:00:00-07:00",
  "temperatureC": 25,
  "summary": "Hot",
  "Wind": 35
}
```

<span data-ttu-id="6b951-192">Zasady nazewnictwa właściwości przypadku notacji CamelCase:</span><span class="sxs-lookup"><span data-stu-id="6b951-192">The camel case property naming policy:</span></span>

* <span data-ttu-id="6b951-193">Dotyczy serializacji i deserializacji.</span><span class="sxs-lookup"><span data-stu-id="6b951-193">Applies to serialization and deserialization.</span></span>
* <span data-ttu-id="6b951-194">Jest zastępowany `[JsonPropertyName]` przez atrybuty.</span><span class="sxs-lookup"><span data-stu-id="6b951-194">Is overridden by `[JsonPropertyName]` attributes.</span></span>

### <a name="use-a-custom-json-property-naming-policy"></a><span data-ttu-id="6b951-195">Użyj niestandardowych zasad nazewnictwa właściwości JSON</span><span class="sxs-lookup"><span data-stu-id="6b951-195">Use a custom JSON property naming policy</span></span>

<span data-ttu-id="6b951-196">Aby użyć niestandardowych zasad nazewnictwa właściwości JSON, Utwórz klasę, która pochodzi od <xref:System.Text.Json.JsonNamingPolicy> i <xref:System.Text.Json.JsonNamingPolicy.ConvertName%2A> przesłania metodę, jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="6b951-196">To use a custom JSON property naming policy, create a class that derives from <xref:System.Text.Json.JsonNamingPolicy> and override the <xref:System.Text.Json.JsonNamingPolicy.ConvertName%2A> method, as shown in the following example:</span></span>

```csharp
class UpperCaseNamingPolicy : JsonNamingPolicy
{
    public override string ConvertName(string name)
    {
        return name.ToUpper();
    }
}
```

<span data-ttu-id="6b951-197">Następnie ustaw <xref:System.Text.Json.JsonSerializerOptions.PropertyNamingPolicy?displayProperty=nameWithType> właściwość na wystąpienie klasy zasad nazewnictwa:</span><span class="sxs-lookup"><span data-stu-id="6b951-197">Then set the <xref:System.Text.Json.JsonSerializerOptions.PropertyNamingPolicy?displayProperty=nameWithType> property to an instance of your naming policy class:</span></span>

```csharp
var options = new JsonSerializerOptions
{
    PropertyNamingPolicy = new UpperCaseNamingPolicy()
};
json = JsonSerializer.Serialize(weatherForecast, options);
```

<span data-ttu-id="6b951-198">Oto przykładowa Klasa do serializacji i danych wyjściowych JSON:</span><span class="sxs-lookup"><span data-stu-id="6b951-198">Here's an example class to serialize and JSON output:</span></span>

```csharp
class WeatherForecast
{
    public DateTimeOffset Date { get; set; }
    public int TemperatureC { get; set; }
    public string Summary { get; set; }
    [JsonPropertyName("Wind")]
    public int WindSpeed { get; set; }
}
```

```json
{
  "DATE": "2019-08-01T00:00:00-07:00",
  "TEMPERATUREC": 25,
  "SUMMARY": "Hot",
  "Wind": 35
}
```

<span data-ttu-id="6b951-199">Zasady nazewnictwa właściwości JSON:</span><span class="sxs-lookup"><span data-stu-id="6b951-199">The JSON property naming policy:</span></span>

* <span data-ttu-id="6b951-200">Dotyczy serializacji i deserializacji.</span><span class="sxs-lookup"><span data-stu-id="6b951-200">Applies to serialization and deserialization.</span></span>
* <span data-ttu-id="6b951-201">Jest zastępowany `[JsonPropertyName]` przez atrybuty.</span><span class="sxs-lookup"><span data-stu-id="6b951-201">Is overridden by `[JsonPropertyName]` attributes.</span></span>

### <a name="camel-case-dictionary-keys"></a><span data-ttu-id="6b951-202">Klucze słownika przypadku notacji CamelCase</span><span class="sxs-lookup"><span data-stu-id="6b951-202">Camel case dictionary keys</span></span>

<span data-ttu-id="6b951-203">Jeśli właściwość obiektu `string` , który ma zostać Zserializowany, jest typu `Dictionary<string,TValue>`, klucze mogą być konwertowane na notacji CamelCase przypadku.</span><span class="sxs-lookup"><span data-stu-id="6b951-203">If a property of an object to be serialized is of type `Dictionary<string,TValue>`, the `string` keys can be converted to camel case.</span></span> <span data-ttu-id="6b951-204">W tym celu ustaw wartość <xref:System.Text.Json.JsonSerializerOptions.DictionaryKeyPolicy> `JsonNamingPolicy.CamelCase`, jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="6b951-204">To do that, set <xref:System.Text.Json.JsonSerializerOptions.DictionaryKeyPolicy> to `JsonNamingPolicy.CamelCase`, as shown in the following example:</span></span>

```csharp
var options = new JsonSerializerOptions
{
    DictionaryKeyPolicy = JsonNamingPolicy.CamelCase
};
json = JsonSerializer.Serialize(weatherForecast, options);
```

<span data-ttu-id="6b951-205">Oto przykład obiektu do serializacji i danych wyjściowych JSON:</span><span class="sxs-lookup"><span data-stu-id="6b951-205">Here's an example object to serialize and JSON output:</span></span>

|<span data-ttu-id="6b951-206">Właściwość</span><span class="sxs-lookup"><span data-stu-id="6b951-206">Property</span></span> |<span data-ttu-id="6b951-207">Wartość</span><span class="sxs-lookup"><span data-stu-id="6b951-207">Value</span></span>  |
|---------|---------|
| <span data-ttu-id="6b951-208">Data</span><span class="sxs-lookup"><span data-stu-id="6b951-208">Date</span></span>    | <span data-ttu-id="6b951-209">8/1/2019 12:00:00 AM – 07:00</span><span class="sxs-lookup"><span data-stu-id="6b951-209">8/1/2019 12:00:00 AM -07:00</span></span>|
| <span data-ttu-id="6b951-210">TemperatureC</span><span class="sxs-lookup"><span data-stu-id="6b951-210">TemperatureC</span></span>| <span data-ttu-id="6b951-211">25</span><span class="sxs-lookup"><span data-stu-id="6b951-211">25</span></span> |
| <span data-ttu-id="6b951-212">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="6b951-212">Summary</span></span>| <span data-ttu-id="6b951-213">ręczne</span><span class="sxs-lookup"><span data-stu-id="6b951-213">Hot</span></span>|
| <span data-ttu-id="6b951-214">TemperatureRanges</span><span class="sxs-lookup"><span data-stu-id="6b951-214">TemperatureRanges</span></span> | <span data-ttu-id="6b951-215">Zimna, 20</span><span class="sxs-lookup"><span data-stu-id="6b951-215">Cold, 20</span></span><br><span data-ttu-id="6b951-216">Gorąca, 40</span><span class="sxs-lookup"><span data-stu-id="6b951-216">Hot, 40</span></span>|

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureC": 25,
  "Summary": "Hot",
  "TemperatureRanges": {
    "cold": 20,
    "hot": 40
  }
}
```

<span data-ttu-id="6b951-217">Zasady nazewnictwa przypadków notacji CamelCase mają zastosowanie tylko do serializacji.</span><span class="sxs-lookup"><span data-stu-id="6b951-217">The camel case naming policy applies to serialization only.</span></span>

## <a name="exclude-properties"></a><span data-ttu-id="6b951-218">Właściwości wykluczenia</span><span class="sxs-lookup"><span data-stu-id="6b951-218">Exclude properties</span></span>

<span data-ttu-id="6b951-219">Domyślnie wszystkie właściwości publiczne są serializowane.</span><span class="sxs-lookup"><span data-stu-id="6b951-219">By default, all public properties are serialized.</span></span> <span data-ttu-id="6b951-220">Jeśli nie chcesz, aby niektóre z nich pojawiały się w danych wyjściowych JSON, masz kilka opcji.</span><span class="sxs-lookup"><span data-stu-id="6b951-220">If you don't want some of them to appear in the JSON output, you have several options.</span></span> <span data-ttu-id="6b951-221">W tej sekcji wyjaśniono, jak wykluczyć:</span><span class="sxs-lookup"><span data-stu-id="6b951-221">This section explains how to exclude:</span></span>

* <span data-ttu-id="6b951-222">Poszczególne właściwości</span><span class="sxs-lookup"><span data-stu-id="6b951-222">Individual properties</span></span>
* <span data-ttu-id="6b951-223">Wszystkie właściwości tylko do odczytu</span><span class="sxs-lookup"><span data-stu-id="6b951-223">All read-only properties</span></span>
* <span data-ttu-id="6b951-224">Wszystkie właściwości o wartości null</span><span class="sxs-lookup"><span data-stu-id="6b951-224">All null-value properties</span></span> 

### <a name="exclude-individual-properties"></a><span data-ttu-id="6b951-225">Wyklucz pojedyncze właściwości</span><span class="sxs-lookup"><span data-stu-id="6b951-225">Exclude individual properties</span></span>

<span data-ttu-id="6b951-226">Aby zignorować poszczególne właściwości, Użyj atrybutu [[JsonIgnore]](xref:System.Text.Json.Serialization.JsonIgnoreAttribute) .</span><span class="sxs-lookup"><span data-stu-id="6b951-226">To ignore individual properties, use the [[JsonIgnore]](xref:System.Text.Json.Serialization.JsonIgnoreAttribute) attribute.</span></span>

<span data-ttu-id="6b951-227">Oto przykład typu do serializacji i danych wyjściowych JSON:</span><span class="sxs-lookup"><span data-stu-id="6b951-227">Here's an example type to serialize and JSON output:</span></span>

```csharp
class WeatherForecast
{
    public DateTimeOffset Date { get; set; }
    public int TemperatureC { get; set; }
    public string Summary { get; set; }
    [JsonIgnore]
    public int WindSpeed { get; set; }
}
```

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureC": 25,
  "Summary": "Hot"
}
```

### <a name="exclude-all-read-only-properties"></a><span data-ttu-id="6b951-228">Wyklucz wszystkie właściwości tylko do odczytu</span><span class="sxs-lookup"><span data-stu-id="6b951-228">Exclude all read-only properties</span></span>

<span data-ttu-id="6b951-229">Aby wykluczyć wszystkie właściwości tylko <xref:System.Text.Json.JsonSerializerOptions.IgnoreReadOnlyProperties?displayProperty=nameWithType> do odczytu, ustaw wartość na `true`, jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="6b951-229">To exclude all read-only properties, set the <xref:System.Text.Json.JsonSerializerOptions.IgnoreReadOnlyProperties?displayProperty=nameWithType> to `true`, as shown in the following example:</span></span>

```csharp
var options = new JsonSerializerOptions
{
    IgnoreReadOnlyProperties = true
};
json = JsonSerializer.Serialize(weatherForecast, options);
```

<span data-ttu-id="6b951-230">Oto przykład typu do serializacji i danych wyjściowych JSON:</span><span class="sxs-lookup"><span data-stu-id="6b951-230">Here's an example type to serialize and JSON output:</span></span>

```csharp
class WeatherForecast
{
    public DateTimeOffset Date { get; set; }
    public int TemperatureC { get; set; }
    public string Summary { get; set; }
    public int WindSpeed { get; private set; }
}
```

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureC": 25,
  "Summary": "Hot",
}
```

<span data-ttu-id="6b951-231">Ta opcja ma zastosowanie tylko do serializacji.</span><span class="sxs-lookup"><span data-stu-id="6b951-231">This option applies only to serialization.</span></span> <span data-ttu-id="6b951-232">Podczas deserializacji właściwości tylko do odczytu są domyślnie ignorowane.</span><span class="sxs-lookup"><span data-stu-id="6b951-232">During deserialization, read-only properties are ignored by default.</span></span> <span data-ttu-id="6b951-233">Właściwość jest tylko do odczytu, jeśli zawiera publiczną metodę pobierającą, ale nie do publicznej metody ustawiającej.</span><span class="sxs-lookup"><span data-stu-id="6b951-233">A property is read-only if it contains a public getter but not a public setter.</span></span>

### <a name="exclude-all-null-value-properties"></a><span data-ttu-id="6b951-234">Wyklucz wszystkie właściwości wartości null</span><span class="sxs-lookup"><span data-stu-id="6b951-234">Exclude all null value properties</span></span>

<span data-ttu-id="6b951-235">Aby wykluczyć wszystkie właściwości wartości null, należy ustawić <xref:System.Text.Json.JsonSerializerOptions.IgnoreNullValues> właściwość na `true`, jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="6b951-235">To exclude all null value properties, set the <xref:System.Text.Json.JsonSerializerOptions.IgnoreNullValues> property to `true`, as shown in the following example:</span></span>

```csharp
var options = new JsonSerializerOptions
{
    IgnoreNullValues = true
};
json = JsonSerializer.Serialize(weatherForecast, options);
```

<span data-ttu-id="6b951-236">Oto przykład obiektu do serializacji i danych wyjściowych JSON:</span><span class="sxs-lookup"><span data-stu-id="6b951-236">Here's an example object to serialize and JSON output:</span></span>

|<span data-ttu-id="6b951-237">Właściwość</span><span class="sxs-lookup"><span data-stu-id="6b951-237">Property</span></span> |<span data-ttu-id="6b951-238">Wartość</span><span class="sxs-lookup"><span data-stu-id="6b951-238">Value</span></span>  |
|---------|---------|
| <span data-ttu-id="6b951-239">Data</span><span class="sxs-lookup"><span data-stu-id="6b951-239">Date</span></span>    | <span data-ttu-id="6b951-240">8/1/2019 12:00:00 AM – 07:00</span><span class="sxs-lookup"><span data-stu-id="6b951-240">8/1/2019 12:00:00 AM -07:00</span></span>|
| <span data-ttu-id="6b951-241">TemperatureC</span><span class="sxs-lookup"><span data-stu-id="6b951-241">TemperatureC</span></span>| <span data-ttu-id="6b951-242">25</span><span class="sxs-lookup"><span data-stu-id="6b951-242">25</span></span> |
| <span data-ttu-id="6b951-243">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="6b951-243">Summary</span></span>| <span data-ttu-id="6b951-244">wartość null</span><span class="sxs-lookup"><span data-stu-id="6b951-244">null</span></span>|

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureC": 25
}
```

<span data-ttu-id="6b951-245">To ustawienie dotyczy serializacji i deserializacji.</span><span class="sxs-lookup"><span data-stu-id="6b951-245">This setting applies to serialization and deserialization.</span></span> <span data-ttu-id="6b951-246">Podczas deserializacji wartości null w formacie JSON są ignorowane tylko wtedy, gdy są prawidłowe.</span><span class="sxs-lookup"><span data-stu-id="6b951-246">During deserialization, null values in the JSON are ignored only if they are valid.</span></span> <span data-ttu-id="6b951-247">Wartości null dla typów wartości, które nie dopuszczają wartości null, powodują wyjątki.</span><span class="sxs-lookup"><span data-stu-id="6b951-247">Null values for non-nullable value types cause exceptions.</span></span> <span data-ttu-id="6b951-248">Aby uzyskać więcej informacji, zobacz [problem związany z typami wartości niedopuszczających wartości null](https://github.com/dotnet/corefx/issues/40922) w repozytorium dotnet/corefx w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="6b951-248">For more information, see the [issue on non-nullable value types](https://github.com/dotnet/corefx/issues/40922) in the dotnet/corefx repository on GitHub.</span></span>

## <a name="case-insensitive-property-matching"></a><span data-ttu-id="6b951-249">Dopasowanie właściwości bez uwzględniania wielkości liter</span><span class="sxs-lookup"><span data-stu-id="6b951-249">Case-insensitive property matching</span></span>

<span data-ttu-id="6b951-250">Domyślnie deserializacja wyszukuje dopasowania nazw właściwości z uwzględnieniem wielkości liter między formatem JSON a właściwościami obiektu docelowego.</span><span class="sxs-lookup"><span data-stu-id="6b951-250">By default, deserialization looks for case-sensitive property name matches between JSON and the target object properties.</span></span> <span data-ttu-id="6b951-251">Aby zmienić to zachowanie, ustaw <xref:System.Text.Json.JsonSerializerOptions.PropertyNameCaseInsensitive?displayProperty=nameWithType> wartość na: `true`</span><span class="sxs-lookup"><span data-stu-id="6b951-251">To change that behavior, set the <xref:System.Text.Json.JsonSerializerOptions.PropertyNameCaseInsensitive?displayProperty=nameWithType> to `true`:</span></span>

```csharp
var options = new JsonSerializerOptions
{
    PropertyNameCaseInsensitive = true,
};
var weatherForecast = JsonSerializer.Deserialize<WeatherForecast>(weatherForecast, options);
```

<span data-ttu-id="6b951-252">Oto przykład JSON z nazwami właściwości przypadku notacji CamelCase.</span><span class="sxs-lookup"><span data-stu-id="6b951-252">Here's example JSON with camel case property names.</span></span> <span data-ttu-id="6b951-253">Można ją zdeserializować do następującego typu, który ma nazwy właściwości przypadku języka Pascal.</span><span class="sxs-lookup"><span data-stu-id="6b951-253">It can be deserialized into the following type that has Pascal case property names.</span></span>

```json
{
  "date": "2019-08-01T00:00:00-07:00",
  "temperatureC": 25,
  "summary": "Hot",
}
```

```csharp
class WeatherForecast
{
    public DateTimeOffset Date { get; set; }
    public int TemperatureC { get; set; }
    public string Summary { get; set; }
}
```

## <a name="include-properties-of-derived-classes"></a><span data-ttu-id="6b951-254">Dołącz właściwości klas pochodnych</span><span class="sxs-lookup"><span data-stu-id="6b951-254">Include properties of derived classes</span></span>

<span data-ttu-id="6b951-255">Serializacja polimorficzna nie jest obsługiwana w przypadku określenia w czasie kompilacji typu, który ma być serializowany.</span><span class="sxs-lookup"><span data-stu-id="6b951-255">Polymorphic serialization isn't supported when you specify at compile time the type to be serialized.</span></span> <span data-ttu-id="6b951-256">Załóżmy na przykład, że masz `WeatherForecast` klasę i klasę `WeatherForecastWithWind`pochodną:</span><span class="sxs-lookup"><span data-stu-id="6b951-256">For example, suppose you have a `WeatherForecast` class and a derived class `WeatherForecastWithWind`:</span></span>

```csharp
class WeatherForecast
{
    public DateTimeOffset Date { get; set; }
    public int TemperatureC { get; set; }
    public string Summary { get; set; }
}
class WeatherForecastWithWind : WeatherForecast
{
    public int WindSpeed { get; set; }
}
```

<span data-ttu-id="6b951-257">I Załóżmy, że typ przeszedł do, lub wywnioskowany przez, `Serialize` Metoda w czasie kompilacji to `WeatherForecast`:</span><span class="sxs-lookup"><span data-stu-id="6b951-257">And suppose the type passed to, or inferred by, the `Serialize` method at compile time is `WeatherForecast`:</span></span>

```csharp
string json = JsonSerializer.Serialize<WeatherForecast>(weatherForecast);
```

```csharp
WeatherForecast weatherForecast;
//...
json = JsonSerializer.Serialize(weatherForecast);
```

<span data-ttu-id="6b951-258">W tym scenariuszu `WindSpeed` właściwość nie jest serializowana, nawet `weatherForecast` Jeśli obiekt jest rzeczywiście `WeatherForecastWithWind` obiektem.</span><span class="sxs-lookup"><span data-stu-id="6b951-258">In this scenario, the `WindSpeed` property is not serialized even if the `weatherForecast` object is actually a `WeatherForecastWithWind` object.</span></span> <span data-ttu-id="6b951-259">Tylko właściwości klasy bazowej są serializowane:</span><span class="sxs-lookup"><span data-stu-id="6b951-259">Only the base class properties are serialized:</span></span>

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureC": 25,
  "Summary": "Hot"
}
```

<span data-ttu-id="6b951-260">Takie zachowanie ma na celu zapobieganie przypadkowemu narażeniu danych w pochodnym typie tworzonym przez środowisko uruchomieniowe.</span><span class="sxs-lookup"><span data-stu-id="6b951-260">This behavior is intended to help prevent accidental exposure of data in a derived runtime-created type.</span></span>

<span data-ttu-id="6b951-261">Aby serializować właściwości typu pochodnego, należy użyć jednej z następujących metod:</span><span class="sxs-lookup"><span data-stu-id="6b951-261">To serialize the properties of the derived type, use one of the following approaches:</span></span>

* <span data-ttu-id="6b951-262">Wywołaj Przeciążenie <xref:System.Text.Json.JsonSerializer.Serialize%2A> , które pozwala określić typ w czasie wykonywania:</span><span class="sxs-lookup"><span data-stu-id="6b951-262">Call an overload of <xref:System.Text.Json.JsonSerializer.Serialize%2A> that lets you specify the type at runtime:</span></span>

  ```csharp
  json = JsonSerializer.Serialize(weatherForecast, weatherForecast.GetType());
  ```

* <span data-ttu-id="6b951-263">Zadeklaruj obiekt, który ma zostać `object`Zserializowany jako.</span><span class="sxs-lookup"><span data-stu-id="6b951-263">Declare the object to be serialized as `object`.</span></span>

  ```csharp
  json = JsonSerializer.Serialize<object>(weatherForecast);
  ```

<span data-ttu-id="6b951-264">W poprzednim przykładowym scenariuszu oba podejścia powodują `WindSpeed` , że właściwość powinna zostać uwzględniona w danych wyjściowych JSON:</span><span class="sxs-lookup"><span data-stu-id="6b951-264">In the preceding example scenario, both approaches cause the `WindSpeed` property to be included in the JSON output:</span></span>

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureC": 25,
  "Summary": "Hot",
  "WindSpeed": 35
}
```

## <a name="handle-overflow-json"></a><span data-ttu-id="6b951-265">Obsługa przepełnienia kodu JSON</span><span class="sxs-lookup"><span data-stu-id="6b951-265">Handle overflow JSON</span></span>

<span data-ttu-id="6b951-266">Podczas deserializacji można odbierać dane w formacie JSON, które nie są reprezentowane przez właściwości typu docelowego.</span><span class="sxs-lookup"><span data-stu-id="6b951-266">While deserializing, you might receive data in the JSON that is not represented by properties of the target type.</span></span> <span data-ttu-id="6b951-267">Załóżmy na przykład, że typ docelowy to:</span><span class="sxs-lookup"><span data-stu-id="6b951-267">For example, suppose your target type is this:</span></span>

```csharp
class WeatherForecast
{
    public DateTimeOffset Date { get; set; }
    public int TemperatureC { get; set; }
    public string Summary { get; set; }
}
```

<span data-ttu-id="6b951-268">I kod JSON do deserializacji jest następujący:</span><span class="sxs-lookup"><span data-stu-id="6b951-268">And the JSON to be deserialized is this:</span></span>

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "temperatureC": 25,
  "Summary": "Hot",
  "DatesAvailable": [
    "2019-08-01T00:00:00-07:00",
    "2019-08-02T00:00:00-07:00"
  ],
  "SummaryWords": [
    "Cool",
    "Windy",
    "Humid"
  ]
}
```

<span data-ttu-id="6b951-269">W przypadku deserializacji kodu JSON pokazanego w pokazanym `SummaryWords` typie, właściwości i mają wartość `DatesAvailable` Nowhere to go i są tracone.</span><span class="sxs-lookup"><span data-stu-id="6b951-269">If you deserialize the JSON shown into the type shown, the `DatesAvailable` and `SummaryWords` properties have nowhere to go and are lost.</span></span> <span data-ttu-id="6b951-270">Aby przechwycić dodatkowe dane, takie jak te właściwości, zastosuj atrybut [JsonExtensionData](xref:System.Text.Json.Serialization.JsonExtensionDataAttribute) do właściwości typu `Dictionary<string,object>` lub: `Dictionary<string,JsonElement>`</span><span class="sxs-lookup"><span data-stu-id="6b951-270">To capture extra data such as these properties, apply the [JsonExtensionData](xref:System.Text.Json.Serialization.JsonExtensionDataAttribute) attribute to a property of type `Dictionary<string,object>` or `Dictionary<string,JsonElement>`:</span></span>

```csharp
class WeatherForecast
{
    public DateTimeOffset Date { get; set; }
    public int TemperatureC { get; set; }
    public string Summary { get; set; }
    [JsonExtensionData]
    public Dictionary<string, object> ExtensionData { get; set; }
}
```

<span data-ttu-id="6b951-271">Podczas deserializacji kodu JSON pokazanego wcześniej w tym typie próbkowania dodatkowe dane staną się parami `ExtensionData` klucz-wartość właściwości:</span><span class="sxs-lookup"><span data-stu-id="6b951-271">When you deserialize the JSON shown earlier into this sample type, the extra data becomes key-value pairs of the `ExtensionData` property:</span></span>

|<span data-ttu-id="6b951-272">Właściwość</span><span class="sxs-lookup"><span data-stu-id="6b951-272">Property</span></span> |<span data-ttu-id="6b951-273">Wartość</span><span class="sxs-lookup"><span data-stu-id="6b951-273">Value</span></span>  |<span data-ttu-id="6b951-274">Uwagi</span><span class="sxs-lookup"><span data-stu-id="6b951-274">Notes</span></span>  |
|---------|---------|---------|
| <span data-ttu-id="6b951-275">Data</span><span class="sxs-lookup"><span data-stu-id="6b951-275">Date</span></span>    | <span data-ttu-id="6b951-276">8/1/2019 12:00:00 AM – 07:00</span><span class="sxs-lookup"><span data-stu-id="6b951-276">8/1/2019 12:00:00 AM -07:00</span></span>||
| <span data-ttu-id="6b951-277">TemperatureC</span><span class="sxs-lookup"><span data-stu-id="6b951-277">TemperatureC</span></span>| <span data-ttu-id="6b951-278">0</span><span class="sxs-lookup"><span data-stu-id="6b951-278">0</span></span> | <span data-ttu-id="6b951-279">Niezgodność z rozróżnianiem`temperatureC` wielkości liter (w formacie JSON), więc właściwość nie jest ustawiona.</span><span class="sxs-lookup"><span data-stu-id="6b951-279">Case-sensitive mismatch (`temperatureC` in the JSON), so the property isn't set.</span></span> |
| <span data-ttu-id="6b951-280">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="6b951-280">Summary</span></span> | <span data-ttu-id="6b951-281">ręczne</span><span class="sxs-lookup"><span data-stu-id="6b951-281">Hot</span></span> ||
| <span data-ttu-id="6b951-282">ExtensionData —</span><span class="sxs-lookup"><span data-stu-id="6b951-282">ExtensionData</span></span> | <span data-ttu-id="6b951-283">temperatureC: 25</span><span class="sxs-lookup"><span data-stu-id="6b951-283">temperatureC: 25</span></span> |<span data-ttu-id="6b951-284">Ponieważ przypadek nie jest zgodny, ta właściwość JSON jest dodatkową i jest parą klucz-wartość w słowniku.</span><span class="sxs-lookup"><span data-stu-id="6b951-284">Since the case didn't match, this JSON property is an extra and becomes a key-value pair in the dictionary.</span></span>|
|| <span data-ttu-id="6b951-285">DatesAvailable:</span><span class="sxs-lookup"><span data-stu-id="6b951-285">DatesAvailable:</span></span><br>  <span data-ttu-id="6b951-286">8/1/2019 12:00:00 AM – 07:00</span><span class="sxs-lookup"><span data-stu-id="6b951-286">8/1/2019 12:00:00 AM -07:00</span></span><br><span data-ttu-id="6b951-287">8/2/2019 12:00:00 AM – 07:00</span><span class="sxs-lookup"><span data-stu-id="6b951-287">8/2/2019 12:00:00 AM -07:00</span></span> |<span data-ttu-id="6b951-288">Dodatkowa Właściwość JSON zmieni się na parę klucz-wartość, z tablicą jako obiektem wartości.</span><span class="sxs-lookup"><span data-stu-id="6b951-288">Extra property from the JSON becomes a key-value pair, with an array as the value object.</span></span>|
| |<span data-ttu-id="6b951-289">SummaryWords:</span><span class="sxs-lookup"><span data-stu-id="6b951-289">SummaryWords:</span></span><br><span data-ttu-id="6b951-290">Ochłodzenia</span><span class="sxs-lookup"><span data-stu-id="6b951-290">Cool</span></span><br><span data-ttu-id="6b951-291">Wiatr</span><span class="sxs-lookup"><span data-stu-id="6b951-291">Windy</span></span><br><span data-ttu-id="6b951-292">Humid</span><span class="sxs-lookup"><span data-stu-id="6b951-292">Humid</span></span> |<span data-ttu-id="6b951-293">Dodatkowa Właściwość JSON zmieni się na parę klucz-wartość, z tablicą jako obiektem wartości.</span><span class="sxs-lookup"><span data-stu-id="6b951-293">Extra property from the JSON becomes a key-value pair, with an array as the value object.</span></span>|

<span data-ttu-id="6b951-294">Gdy obiekt docelowy jest serializowany, pary wartości klucza danych rozszerzenia stają się właściwościami JSON tak samo jak w przychodzących danych JSON:</span><span class="sxs-lookup"><span data-stu-id="6b951-294">When the target object is serialized, the extension data key value pairs become JSON properties just as they were in the incoming JSON:</span></span>

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureC": 0,
  "Summary": "Hot",
  "temperatureC": 25,
  "DatesAvailable": [
    "2019-08-01T00:00:00-07:00",
    "2019-08-02T00:00:00-07:00"
  ],
  "SummaryWords": [
    "Cool",
    "Windy",
    "Humid"
  ]
}
```

<span data-ttu-id="6b951-295">Zauważ, że `ExtensionData` nazwa właściwości nie pojawia się w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="6b951-295">Notice that the `ExtensionData` property name doesn't appear in the JSON.</span></span> <span data-ttu-id="6b951-296">Takie zachowanie umożliwia wykonywanie operacji okrężnych przez kod JSON bez utraty jakichkolwiek dodatkowych danych, które w przeciwnym razie nie zostały odszeregowane.</span><span class="sxs-lookup"><span data-stu-id="6b951-296">This behavior lets the JSON make a round trip without losing any extra data that otherwise wouldn't be deserialized.</span></span>

## <a name="use-utf8jsonwriter-directly"></a><span data-ttu-id="6b951-297">Używaj Utf8JsonWriter bezpośrednio</span><span class="sxs-lookup"><span data-stu-id="6b951-297">Use Utf8JsonWriter directly</span></span>

<span data-ttu-id="6b951-298">Poniższy przykład pokazuje, <xref:System.Text.Json.Utf8JsonWriter> jak używać klasy bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="6b951-298">The following example shows how to use the <xref:System.Text.Json.Utf8JsonWriter> class directly.</span></span>

```csharp
var options = new JsonWriterOptions
{
    Indented = true
};

using (var stream = new MemoryStream())
{
    using (var writer = new Utf8JsonWriter(stream, options))
    {
        writer.WriteStartObject();
        writer.WriteString("date", DateTimeOffset.UtcNow);
        writer.WriteNumber("temp", 42);
        writer.WriteEndObject();
    }

    string json = Encoding.UTF8.GetString(stream.ToArray());
    Console.WriteLine(json);
}
```

## <a name="use-utf8jsonreader-directly"></a><span data-ttu-id="6b951-299">Używaj Utf8JsonReader bezpośrednio</span><span class="sxs-lookup"><span data-stu-id="6b951-299">Use Utf8JsonReader directly</span></span>

<span data-ttu-id="6b951-300">Poniższy przykład pokazuje, <xref:System.Text.Json.Utf8JsonReader> jak używać klasy bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="6b951-300">The following example shows how to use the <xref:System.Text.Json.Utf8JsonReader> class directly.</span></span> <span data-ttu-id="6b951-301">W kodzie przyjęto, `jsonUtf8` że zmienna jest tablicą bajtów, która zawiera prawidłowy kod JSON zakodowany jako UTF-8.</span><span class="sxs-lookup"><span data-stu-id="6b951-301">The code assumes that the `jsonUtf8` variable is a byte array that contains valid JSON, encoded as UTF-8.</span></span>

```csharp
var options = new JsonReaderOptions
{
    AllowTrailingCommas = true,
    CommentHandling = JsonCommentHandling.Skip
};
Utf8JsonReader reader = new Utf8JsonReader(jsonUtf8, options);

while (reader.Read())
{
    Console.Write(reader.TokenType);

    switch (reader.TokenType)
    {
        case JsonTokenType.PropertyName:
        case JsonTokenType.String:
            {
                string text = reader.GetString();
                Console.Write(" ");
                Console.Write(text);
                break;
            }

        case JsonTokenType.Number:
            {
                int value = reader.GetInt32();
                Console.Write(" ");
                Console.Write(value);
                break;
            }

            // Other token types elided for brevity
    }

    Console.WriteLine();
}
```

## <a name="additional-resources"></a><span data-ttu-id="6b951-302">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="6b951-302">Additional resources</span></span>

* [<span data-ttu-id="6b951-303">System. Text. JSON — Omówienie</span><span class="sxs-lookup"><span data-stu-id="6b951-303">System.Text.Json overview</span></span>](system-text-json-overview.md)
* [<span data-ttu-id="6b951-304">Dokumentacja interfejsu API System. Text. JSON</span><span class="sxs-lookup"><span data-stu-id="6b951-304">System.Text.Json API reference</span></span>](xref:System.Text.Json)
* [<span data-ttu-id="6b951-305">Obsługa DateTime i DateTimeOffset w pliku System. Text. JSON</span><span class="sxs-lookup"><span data-stu-id="6b951-305">DateTime and DateTimeOffset support in System.Text.Json</span></span>](../datetime/system-text-json-support.md)