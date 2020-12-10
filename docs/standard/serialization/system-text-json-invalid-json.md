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
# <a name="how-to-allow-some-kinds-of-invalid-json-with-no-locsystemtextjson"></a><span data-ttu-id="6d233-103">Jak zezwolić na niektóre rodzaje nieprawidłowego kodu JSON z System.Text.Json</span><span class="sxs-lookup"><span data-stu-id="6d233-103">How to allow some kinds of invalid JSON with System.Text.Json</span></span>

<span data-ttu-id="6d233-104">W tym artykule dowiesz się, jak zezwolić na komentarze, końcowe przecinki i liczby ujęte w cudzysłów w formacie JSON oraz jak pisać liczby jako ciągi.</span><span class="sxs-lookup"><span data-stu-id="6d233-104">In this article, you will learn how to allow comments, trailing commas, and quoted numbers in JSON, and how to write numbers as strings.</span></span>

## <a name="allow-comments-and-trailing-commas"></a><span data-ttu-id="6d233-105">Zezwalaj na komentarze i końcowe przecinki</span><span class="sxs-lookup"><span data-stu-id="6d233-105">Allow comments and trailing commas</span></span>

<span data-ttu-id="6d233-106">Domyślnie Komentarze i końcowe przecinki są niedozwolone w notacji JSON.</span><span class="sxs-lookup"><span data-stu-id="6d233-106">By default, comments and trailing commas are not allowed in JSON.</span></span> <span data-ttu-id="6d233-107">Aby zezwolić na komentarze w formacie JSON, ustaw <xref:System.Text.Json.JsonSerializerOptions.ReadCommentHandling?displayProperty=nameWithType> Właściwość na `JsonCommentHandling.Skip` .</span><span class="sxs-lookup"><span data-stu-id="6d233-107">To allow comments in the JSON, set the <xref:System.Text.Json.JsonSerializerOptions.ReadCommentHandling?displayProperty=nameWithType> property to `JsonCommentHandling.Skip`.</span></span>
<span data-ttu-id="6d233-108">I aby zezwolić na końcowe przecinki, należy ustawić <xref:System.Text.Json.JsonSerializerOptions.AllowTrailingCommas?displayProperty=nameWithType> Właściwość na `true` .</span><span class="sxs-lookup"><span data-stu-id="6d233-108">And to allow trailing commas, set the <xref:System.Text.Json.JsonSerializerOptions.AllowTrailingCommas?displayProperty=nameWithType> property to `true`.</span></span> <span data-ttu-id="6d233-109">Poniższy przykład pokazuje, jak:</span><span class="sxs-lookup"><span data-stu-id="6d233-109">The following example shows how to allow both:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/DeserializeCommasComments.cs" id="Deserialize":::

<span data-ttu-id="6d233-110">Oto przykładowy kod JSON z komentarzami i końcowym przecinkiem:</span><span class="sxs-lookup"><span data-stu-id="6d233-110">Here's example JSON with comments and a trailing comma:</span></span>

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25, // Fahrenheit 77
  "Summary": "Hot", /* Zharko */
  // Comments on
  /* separate lines */
}
```

## <a name="allow-or-write-numbers-in-quotes"></a><span data-ttu-id="6d233-111">Zezwalaj lub zapisuj liczby w cudzysłowach</span><span class="sxs-lookup"><span data-stu-id="6d233-111">Allow or write numbers in quotes</span></span>

::: zone pivot="dotnet-5-0"

<span data-ttu-id="6d233-112">Niektóre serializatory kodują liczby jako ciągi JSON (ujęte w cudzysłowy).</span><span class="sxs-lookup"><span data-stu-id="6d233-112">Some serializers encode numbers as JSON strings (surrounded by quotes).</span></span>

<span data-ttu-id="6d233-113">Przykład:</span><span class="sxs-lookup"><span data-stu-id="6d233-113">For example:</span></span>

```json
{
    "DegreesCelsius": "23"
}
```

<span data-ttu-id="6d233-114">Zamiast:</span><span class="sxs-lookup"><span data-stu-id="6d233-114">Instead of:</span></span>

```json
{
    "DegreesCelsius": 23
}
```

<span data-ttu-id="6d233-115">Aby serializować liczby w cudzysłowach lub zaakceptować liczby cudzysłowów w całym grafie obiektów wejściowych, ustaw <xref:System.Text.Json.JsonSerializerOptions.NumberHandling%2A?displayProperty=nameWithType> jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="6d233-115">To serialize numbers in quotes or accept numbers in quotes across the entire input object graph, set <xref:System.Text.Json.JsonSerializerOptions.NumberHandling%2A?displayProperty=nameWithType> as shown in the following example:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/QuotedNumbers.cs" highlight="27-29":::

<span data-ttu-id="6d233-116">W przypadku użycia `System.Text.Json` pośrednio za pomocą ASP.NET Core, w przypadku deserializacji są dozwolone liczby ujęte w cudzysłów, ponieważ ASP.NET Core określa [domyślne opcje sieci Web](xref:System.Text.Json.JsonSerializerDefaults.Web).</span><span class="sxs-lookup"><span data-stu-id="6d233-116">When you use `System.Text.Json` indirectly through ASP.NET Core, quoted numbers are allowed when deserializing because ASP.NET Core specifies [web default options](xref:System.Text.Json.JsonSerializerDefaults.Web).</span></span>

<span data-ttu-id="6d233-117">Aby dopuszczać lub zapisywać liczby ujęte w cudzysłów dla określonych właściwości, pól lub typów, Użyj atrybutu [[JsonNumberHandling]](xref:System.Text.Json.Serialization.JsonNumberHandlingAttribute) .</span><span class="sxs-lookup"><span data-stu-id="6d233-117">To allow or write quoted numbers for specific properties, fields, or types, use the [[JsonNumberHandling]](xref:System.Text.Json.Serialization.JsonNumberHandlingAttribute) attribute.</span></span>
::: zone-end

::: zone pivot="dotnet-core-3-1"
<span data-ttu-id="6d233-118">`System.Text.Json` w programie .NET Core 3,1 nie obsługuje serializacji ani deserializacji numerów ujętych w cudzysłów.</span><span class="sxs-lookup"><span data-stu-id="6d233-118">`System.Text.Json` in .NET Core 3.1 doesn't support serializing or deserializing numbers surrounded by quotation marks.</span></span> <span data-ttu-id="6d233-119">Aby uzyskać więcej informacji, zobacz [dopuszczanie lub zapisywanie numerów w cudzysłowach](system-text-json-migrate-from-newtonsoft-how-to.md#allow-or-write-numbers-in-quotes).</span><span class="sxs-lookup"><span data-stu-id="6d233-119">For more information, see [Allow or write numbers in quotes](system-text-json-migrate-from-newtonsoft-how-to.md#allow-or-write-numbers-in-quotes).</span></span>
::: zone-end

## <a name="see-also"></a><span data-ttu-id="6d233-120">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="6d233-120">See also</span></span>

* [<span data-ttu-id="6d233-121">System.Text.Json Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="6d233-121">System.Text.Json overview</span></span>](system-text-json-overview.md)
* [<span data-ttu-id="6d233-122">Jak serializować i deserializować dane JSON</span><span class="sxs-lookup"><span data-stu-id="6d233-122">How to serialize and deserialize JSON</span></span>](system-text-json-how-to.md)
* [<span data-ttu-id="6d233-123">Tworzenie wystąpienia JsonSerializerOptions wystąpień</span><span class="sxs-lookup"><span data-stu-id="6d233-123">Instantiate JsonSerializerOptions instances</span></span>](system-text-json-configure-options.md)
* [<span data-ttu-id="6d233-124">Włączanie dopasowywania bez uwzględniania wielkości liter</span><span class="sxs-lookup"><span data-stu-id="6d233-124">Enable case-insensitive matching</span></span>](system-text-json-character-casing.md)
* [<span data-ttu-id="6d233-125">Dostosowywanie nazw i wartości właściwości</span><span class="sxs-lookup"><span data-stu-id="6d233-125">Customize property names and values</span></span>](system-text-json-customize-properties.md)
* [<span data-ttu-id="6d233-126">Ignorowanie właściwości</span><span class="sxs-lookup"><span data-stu-id="6d233-126">Ignore properties</span></span>](system-text-json-ignore-properties.md)
* [<span data-ttu-id="6d233-127">Obsługa przepełnienia kodu JSON</span><span class="sxs-lookup"><span data-stu-id="6d233-127">Handle overflow JSON</span></span>](system-text-json-handle-overflow.md)
* [<span data-ttu-id="6d233-128">Zachowywanie odwołań</span><span class="sxs-lookup"><span data-stu-id="6d233-128">Preserve references</span></span>](system-text-json-preserve-references.md)
* [<span data-ttu-id="6d233-129">Niemodyfikowalne typy i niepubliczne metody dostępu</span><span class="sxs-lookup"><span data-stu-id="6d233-129">Immutable types and non-public accessors</span></span>](system-text-json-immutability.md)
* [<span data-ttu-id="6d233-130">Serializacja polimorficzna</span><span class="sxs-lookup"><span data-stu-id="6d233-130">Polymorphic serialization</span></span>](system-text-json-polymorphism.md)
* [<span data-ttu-id="6d233-131">Migruj z Newtonsoft.Json do System.Text.Json</span><span class="sxs-lookup"><span data-stu-id="6d233-131">Migrate from Newtonsoft.Json to System.Text.Json</span></span>](system-text-json-migrate-from-newtonsoft-how-to.md)
* [<span data-ttu-id="6d233-132">Dostosowywanie kodowania znaków</span><span class="sxs-lookup"><span data-stu-id="6d233-132">Customize character encoding</span></span>](system-text-json-character-encoding.md)
* [<span data-ttu-id="6d233-133">Napisz niestandardowe serializatory i deserializatory</span><span class="sxs-lookup"><span data-stu-id="6d233-133">Write custom serializers and deserializers</span></span>](write-custom-serializer-deserializer.md)
* [<span data-ttu-id="6d233-134">Zapisz konwertery niestandardowe na potrzeby serializacji JSON</span><span class="sxs-lookup"><span data-stu-id="6d233-134">Write custom converters for JSON serialization</span></span>](system-text-json-converters-how-to.md)
* [<span data-ttu-id="6d233-135">Obsługa wartości DateTime i DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="6d233-135">DateTime and DateTimeOffset support</span></span>](../datetime/system-text-json-support.md)
* <span data-ttu-id="6d233-136">[System.Text.Json Dokumentacja interfejsu API](xref:System.Text.Json)</span><span class="sxs-lookup"><span data-stu-id="6d233-136">[System.Text.Json API reference](xref:System.Text.Json)</span></span>
* <span data-ttu-id="6d233-137">[System.Text.Json. Dokumentacja interfejsu API serializacji](xref:System.Text.Json.Serialization)</span><span class="sxs-lookup"><span data-stu-id="6d233-137">[System.Text.Json.Serialization API reference](xref:System.Text.Json.Serialization)</span></span>
