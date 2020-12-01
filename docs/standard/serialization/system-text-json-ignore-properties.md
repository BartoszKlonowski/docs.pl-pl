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
# <a name="how-to-ignore-properties-with-no-locsystemtextjson"></a><span data-ttu-id="050a5-103">Jak zignorować właściwości System.Text.Json</span><span class="sxs-lookup"><span data-stu-id="050a5-103">How to ignore properties with System.Text.Json</span></span>

<span data-ttu-id="050a5-104">Podczas serializacji obiektów C# do JavaScript Object Notation (JSON), domyślnie wszystkie właściwości publiczne są serializowane.</span><span class="sxs-lookup"><span data-stu-id="050a5-104">When serializing C# objects to JavaScript Object Notation (JSON), by default, all public properties are serialized.</span></span> <span data-ttu-id="050a5-105">Jeśli nie chcesz, aby niektóre z nich były wyświetlane w wynikach JSON, masz kilka opcji.</span><span class="sxs-lookup"><span data-stu-id="050a5-105">If you don't want some of them to appear in the resulting JSON, you have several options.</span></span> <span data-ttu-id="050a5-106">W tym artykule dowiesz się, jak zignorować właściwości na podstawie różnych kryteriów:</span><span class="sxs-lookup"><span data-stu-id="050a5-106">In this article you learn how to ignore properties based on various criteria:</span></span>

::: zone pivot="dotnet-5-0"

* [<span data-ttu-id="050a5-107">Poszczególne właściwości</span><span class="sxs-lookup"><span data-stu-id="050a5-107">Individual properties</span></span>](#ignore-individual-properties)
* [<span data-ttu-id="050a5-108">Wszystkie właściwości tylko do odczytu</span><span class="sxs-lookup"><span data-stu-id="050a5-108">All read-only properties</span></span>](#ignore-all-read-only-properties)
* [<span data-ttu-id="050a5-109">Wszystkie właściwości o wartości null</span><span class="sxs-lookup"><span data-stu-id="050a5-109">All null-value properties</span></span>](#ignore-all-null-value-properties)
* [<span data-ttu-id="050a5-110">Wszystkie właściwości domyślne wartości</span><span class="sxs-lookup"><span data-stu-id="050a5-110">All default-value properties</span></span>](#ignore-all-default-value-properties)
::: zone-end

::: zone pivot="dotnet-core-3-1"

* [<span data-ttu-id="050a5-111">Poszczególne właściwości</span><span class="sxs-lookup"><span data-stu-id="050a5-111">Individual properties</span></span>](#ignore-individual-properties)
* [<span data-ttu-id="050a5-112">Wszystkie właściwości tylko do odczytu</span><span class="sxs-lookup"><span data-stu-id="050a5-112">All read-only properties</span></span>](#ignore-all-read-only-properties)
* [<span data-ttu-id="050a5-113">Wszystkie właściwości o wartości null</span><span class="sxs-lookup"><span data-stu-id="050a5-113">All null-value properties</span></span>](#ignore-all-null-value-properties)
::: zone-end

## <a name="ignore-individual-properties"></a><span data-ttu-id="050a5-114">Ignoruj poszczególne właściwości</span><span class="sxs-lookup"><span data-stu-id="050a5-114">Ignore individual properties</span></span>

<span data-ttu-id="050a5-115">Aby zignorować poszczególne właściwości, Użyj atrybutu [[JsonIgnore]](xref:System.Text.Json.Serialization.JsonIgnoreAttribute) .</span><span class="sxs-lookup"><span data-stu-id="050a5-115">To ignore individual properties, use the [[JsonIgnore]](xref:System.Text.Json.Serialization.JsonIgnoreAttribute) attribute.</span></span>

<span data-ttu-id="050a5-116">Oto przykład typu do serializacji i danych wyjściowych JSON:</span><span class="sxs-lookup"><span data-stu-id="050a5-116">Here's an example type to serialize and JSON output:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithIgnoreAttribute":::

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
}
```

::: zone pivot="dotnet-5-0"
<span data-ttu-id="050a5-117">Aby określić wykluczenie warunkowe, należy ustawić właściwość [[JsonIgnore]](xref:System.Text.Json.Serialization.JsonIgnoreAttribute) atrybutu `Condition` .</span><span class="sxs-lookup"><span data-stu-id="050a5-117">You can specify conditional exclusion by setting the [[JsonIgnore]](xref:System.Text.Json.Serialization.JsonIgnoreAttribute) attribute's `Condition` property.</span></span> <span data-ttu-id="050a5-118"><xref:System.Text.Json.Serialization.JsonIgnoreCondition>Wyliczenie zapewnia następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="050a5-118">The <xref:System.Text.Json.Serialization.JsonIgnoreCondition> enum provides the following options:</span></span>

* <span data-ttu-id="050a5-119">`Always` -Właściwość jest zawsze ignorowana.</span><span class="sxs-lookup"><span data-stu-id="050a5-119">`Always` - The property is always ignored.</span></span> <span data-ttu-id="050a5-120">Jeśli `Condition` wartość nie jest określona, założono, że ta opcja jest.</span><span class="sxs-lookup"><span data-stu-id="050a5-120">If no `Condition` is specified, this option is assumed.</span></span>
* <span data-ttu-id="050a5-121">`Never` -Właściwość jest zawsze serializowana i deserializowana, niezależnie od `DefaultIgnoreCondition` `IgnoreReadOnlyProperties` `IgnoreReadOnlyFields` ustawień globalnych, i.</span><span class="sxs-lookup"><span data-stu-id="050a5-121">`Never` - The property is always serialized and deserialized, regardless of the `DefaultIgnoreCondition`, `IgnoreReadOnlyProperties`, and `IgnoreReadOnlyFields` global settings.</span></span>
* <span data-ttu-id="050a5-122">`WhenWritingDefault` -Właściwość jest ignorowana podczas serializacji, jeśli jest typem referencyjnym `null` , typem wartości null `null` lub typem wartości `default` .</span><span class="sxs-lookup"><span data-stu-id="050a5-122">`WhenWritingDefault` - The property is ignored on serialization if it's a reference type `null`, a nullable value type `null`, or a value type `default`.</span></span>
* <span data-ttu-id="050a5-123">`WhenWritingNull` -Właściwość jest ignorowana podczas serializacji, jeśli jest typem referencyjnym `null` lub typem wartości null `null` .</span><span class="sxs-lookup"><span data-stu-id="050a5-123">`WhenWritingNull` - The property is ignored on serialization if it's a reference type `null`, or a nullable value type `null`.</span></span>

<span data-ttu-id="050a5-124">Poniższy przykład ilustruje użycie właściwości [[JsonIgnore]](xref:System.Text.Json.Serialization.JsonIgnoreAttribute) atrybutu `Condition` :</span><span class="sxs-lookup"><span data-stu-id="050a5-124">The following example illustrates use of the [[JsonIgnore]](xref:System.Text.Json.Serialization.JsonIgnoreAttribute) attribute's `Condition` property:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/JsonIgnoreAttributeExample.cs" highlight="10,13,16":::
::: zone-end

## <a name="ignore-all-read-only-properties"></a><span data-ttu-id="050a5-125">Ignoruj wszystkie właściwości tylko do odczytu</span><span class="sxs-lookup"><span data-stu-id="050a5-125">Ignore all read-only properties</span></span>

<span data-ttu-id="050a5-126">Właściwość jest tylko do odczytu, jeśli zawiera publiczną metodę pobierającą, ale nie do publicznej metody ustawiającej.</span><span class="sxs-lookup"><span data-stu-id="050a5-126">A property is read-only if it contains a public getter but not a public setter.</span></span> <span data-ttu-id="050a5-127">Aby zignorować wszystkie właściwości tylko do odczytu podczas serializacji, ustaw wartość <xref:System.Text.Json.JsonSerializerOptions.IgnoreReadOnlyProperties?displayProperty=nameWithType> na `true` , jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="050a5-127">To ignore all read-only properties when serializing, set the <xref:System.Text.Json.JsonSerializerOptions.IgnoreReadOnlyProperties?displayProperty=nameWithType> to `true`, as shown in the following example:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/SerializeExcludeReadOnlyProperties.cs" id="Serialize":::

<span data-ttu-id="050a5-128">Oto przykład typu do serializacji i danych wyjściowych JSON:</span><span class="sxs-lookup"><span data-stu-id="050a5-128">Here's an example type to serialize and JSON output:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithROProperty":::

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot",
}
```

<span data-ttu-id="050a5-129">Ta opcja ma zastosowanie tylko do serializacji.</span><span class="sxs-lookup"><span data-stu-id="050a5-129">This option applies only to serialization.</span></span> <span data-ttu-id="050a5-130">Podczas deserializacji właściwości tylko do odczytu są domyślnie ignorowane.</span><span class="sxs-lookup"><span data-stu-id="050a5-130">During deserialization, read-only properties are ignored by default.</span></span>

::: zone pivot="dotnet-5-0"
<span data-ttu-id="050a5-131">Ta opcja ma zastosowanie tylko do właściwości.</span><span class="sxs-lookup"><span data-stu-id="050a5-131">This option applies only to properties.</span></span> <span data-ttu-id="050a5-132">Aby zignorować pola tylko do odczytu podczas [serializacji pól](system-text-json-how-to.md#include-fields), użyj <xref:System.Text.Json.JsonSerializerOptions.IgnoreReadOnlyFields%2A?displayProperty=nameWithType> Ustawienia globalnego.</span><span class="sxs-lookup"><span data-stu-id="050a5-132">To ignore read-only fields when [serializing fields](system-text-json-how-to.md#include-fields), use the <xref:System.Text.Json.JsonSerializerOptions.IgnoreReadOnlyFields%2A?displayProperty=nameWithType> global setting.</span></span>
::: zone-end

## <a name="ignore-all-null-value-properties"></a><span data-ttu-id="050a5-133">Ignoruj wszystkie właściwości o wartości null</span><span class="sxs-lookup"><span data-stu-id="050a5-133">Ignore all null-value properties</span></span>

::: zone pivot="dotnet-5-0"
<span data-ttu-id="050a5-134">Aby zignorować wszystkie właściwości wartości null, należy ustawić <xref:System.Text.Json.JsonSerializerOptions.DefaultIgnoreCondition> Właściwość na <xref:System.Text.Json.Serialization.JsonIgnoreCondition.WhenWritingNull> , jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="050a5-134">To ignore all null-value properties, set the <xref:System.Text.Json.JsonSerializerOptions.DefaultIgnoreCondition> property to <xref:System.Text.Json.Serialization.JsonIgnoreCondition.WhenWritingNull>, as shown in the following example:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/IgnoreNullOnSerialize.cs" highlight="28":::

::: zone-end

::: zone pivot="dotnet-core-3-1"
<span data-ttu-id="050a5-135">Aby ignorować wszystkie właściwości null wartości podczas serializacji, należy ustawić <xref:System.Text.Json.JsonSerializerOptions.IgnoreNullValues> Właściwość na `true` , jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="050a5-135">To ignore all null-value properties when serializing, set the <xref:System.Text.Json.JsonSerializerOptions.IgnoreNullValues> property to `true`, as shown in the following example:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/SerializeExcludeNullValueProperties.cs" id="Serialize":::

<span data-ttu-id="050a5-136">Oto przykład obiektu do serializacji i danych wyjściowych JSON:</span><span class="sxs-lookup"><span data-stu-id="050a5-136">Here's an example object to serialize and JSON output:</span></span>

| <span data-ttu-id="050a5-137">Właściwość</span><span class="sxs-lookup"><span data-stu-id="050a5-137">Property</span></span>             | <span data-ttu-id="050a5-138">Wartość</span><span class="sxs-lookup"><span data-stu-id="050a5-138">Value</span></span>                         |
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

## <a name="ignore-all-default-value-properties"></a><span data-ttu-id="050a5-139">Ignoruj wszystkie właściwości domyślne wartości</span><span class="sxs-lookup"><span data-stu-id="050a5-139">Ignore all default-value properties</span></span>

::: zone pivot="dotnet-5-0"
<span data-ttu-id="050a5-140">Aby zapobiec serializacji wartości domyślnych we właściwościach typu wartości, ustaw <xref:System.Text.Json.JsonSerializerOptions.DefaultIgnoreCondition> Właściwość na <xref:System.Text.Json.Serialization.JsonIgnoreCondition.WhenWritingDefault> , jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="050a5-140">To prevent serialization of default values in value type properties, set the <xref:System.Text.Json.JsonSerializerOptions.DefaultIgnoreCondition> property to <xref:System.Text.Json.Serialization.JsonIgnoreCondition.WhenWritingDefault>, as shown in the following example:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/IgnoreValueDefaultOnSerialize.cs" highlight="28":::
::: zone-end

<span data-ttu-id="050a5-141"><xref:System.Text.Json.Serialization.JsonIgnoreCondition.WhenWritingDefault>Ustawienie uniemożliwia również serializację typu odwołania o wartości null i właściwości typu wartości null.</span><span class="sxs-lookup"><span data-stu-id="050a5-141">The <xref:System.Text.Json.Serialization.JsonIgnoreCondition.WhenWritingDefault> setting also prevents serialization of null-value reference type and nullable value type properties.</span></span>

::: zone pivot="dotnet-core-3-1"
<span data-ttu-id="050a5-142">Nie ma wbudowanego sposobu, aby zapobiec serializacji właściwości z wartościami domyślnymi typu wartości w `System.Text.Json` programie .NET Core 3,1.</span><span class="sxs-lookup"><span data-stu-id="050a5-142">There is no built-in way to prevent serialization of properties with value type defaults in `System.Text.Json` in .NET Core 3.1.</span></span>
::: zone-end

## <a name="see-also"></a><span data-ttu-id="050a5-143">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="050a5-143">See also</span></span>

* [<span data-ttu-id="050a5-144">System.Text.Json Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="050a5-144">System.Text.Json overview</span></span>](system-text-json-overview.md)
* [<span data-ttu-id="050a5-145">Tworzenie wystąpienia JsonSerializerOptions</span><span class="sxs-lookup"><span data-stu-id="050a5-145">Instantiate JsonSerializerOptions</span></span>](system-text-json-configure-options.md)
* [<span data-ttu-id="050a5-146">Włącz dopasowywanie bez uwzględniania wielkości liter</span><span class="sxs-lookup"><span data-stu-id="050a5-146">Enable case-insensitive matching</span></span>](system-text-json-character-casing.md)
* [<span data-ttu-id="050a5-147">Dostosowywanie nazw i wartości właściwości</span><span class="sxs-lookup"><span data-stu-id="050a5-147">Customize property names and values</span></span>](system-text-json-customize-properties.md)
* [<span data-ttu-id="050a5-148">Zezwalaj na nieprawidłowy kod JSON</span><span class="sxs-lookup"><span data-stu-id="050a5-148">Allow invalid JSON</span></span>](system-text-json-invalid-json.md)
* [<span data-ttu-id="050a5-149">Obsługa przepełnienia kodu JSON</span><span class="sxs-lookup"><span data-stu-id="050a5-149">Handle overflow JSON</span></span>](system-text-json-handle-overflow.md)
* [<span data-ttu-id="050a5-150">Zachowaj odwołania cykliczne</span><span class="sxs-lookup"><span data-stu-id="050a5-150">Preserve circular references</span></span>](system-text-json-preserve-references.md)
* [<span data-ttu-id="050a5-151">Niemodyfikowalne typy i niepubliczne metody dostępu</span><span class="sxs-lookup"><span data-stu-id="050a5-151">Immutable types and non-public accessors</span></span>](system-text-json-immutability.md)
* [<span data-ttu-id="050a5-152">Serializacja polimorficzna</span><span class="sxs-lookup"><span data-stu-id="050a5-152">Polymorphic serialization</span></span>](system-text-json-polymorphism.md)
* <span data-ttu-id="050a5-153">[System.Text.Json Dokumentacja interfejsu API](xref:System.Text.Json)</span><span class="sxs-lookup"><span data-stu-id="050a5-153">[System.Text.Json API reference](xref:System.Text.Json)</span></span>
