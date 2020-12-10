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
ms.openlocfilehash: 3e2fb8cbdd35e772b5e97c731199f69aa834bd0a
ms.sourcegitcommit: 81f1bba2c97a67b5ca76bcc57b37333ffca60c7b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/10/2020
ms.locfileid: "97009745"
---
# <a name="how-to-enable-case-insensitive-property-name-matching-with-no-locsystemtextjson"></a><span data-ttu-id="0fcd5-103">Jak włączyć Dopasowywanie nazw właściwości bez uwzględniania wielkości liter System.Text.Json</span><span class="sxs-lookup"><span data-stu-id="0fcd5-103">How to enable case-insensitive property name matching with System.Text.Json</span></span>

<span data-ttu-id="0fcd5-104">W tym artykule dowiesz się, jak włączyć Dopasowywanie nazw właściwości bez uwzględniania wielkości liter w `System.Text.Json` przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="0fcd5-104">In this article, you will learn how to enable case-insensitive property name matching with the `System.Text.Json` namespace.</span></span>

## <a name="case-insensitive-property-matching"></a><span data-ttu-id="0fcd5-105">Dopasowanie właściwości bez uwzględniania wielkości liter</span><span class="sxs-lookup"><span data-stu-id="0fcd5-105">Case-insensitive property matching</span></span>

<span data-ttu-id="0fcd5-106">Domyślnie deserializacja wyszukuje dopasowania nazw właściwości z uwzględnieniem wielkości liter między formatem JSON a właściwościami obiektu docelowego.</span><span class="sxs-lookup"><span data-stu-id="0fcd5-106">By default, deserialization looks for case-sensitive property name matches between JSON and the target object properties.</span></span> <span data-ttu-id="0fcd5-107">Aby zmienić to zachowanie, ustaw opcję <xref:System.Text.Json.JsonSerializerOptions.PropertyNameCaseInsensitive?displayProperty=nameWithType> na `true` :</span><span class="sxs-lookup"><span data-stu-id="0fcd5-107">To change that behavior, set <xref:System.Text.Json.JsonSerializerOptions.PropertyNameCaseInsensitive?displayProperty=nameWithType> to `true`:</span></span>

> [!NOTE]
> <span data-ttu-id="0fcd5-108">W [domyślnej sieci Web](system-text-json-configure-options.md#web-defaults-for-jsonserializeroptions) nie jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="0fcd5-108">The [web default](system-text-json-configure-options.md#web-defaults-for-jsonserializeroptions) is case-insensitive.</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/DeserializeCaseInsensitive.cs" id="Deserialize":::

<span data-ttu-id="0fcd5-109">Oto przykład JSON z nazwami właściwości przypadku notacji CamelCase.</span><span class="sxs-lookup"><span data-stu-id="0fcd5-109">Here's example JSON with camel case property names.</span></span> <span data-ttu-id="0fcd5-110">Można ją zdeserializować do następującego typu, który ma nazwy właściwości przypadku języka Pascal.</span><span class="sxs-lookup"><span data-stu-id="0fcd5-110">It can be deserialized into the following type that has Pascal case property names.</span></span>

```json
{
  "date": "2019-08-01T00:00:00-07:00",
  "temperatureCelsius": 25,
  "summary": "Hot",
}
```

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WF":::

## <a name="see-also"></a><span data-ttu-id="0fcd5-111">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="0fcd5-111">See also</span></span>

* [<span data-ttu-id="0fcd5-112">System.Text.Json Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="0fcd5-112">System.Text.Json overview</span></span>](system-text-json-overview.md)
* [<span data-ttu-id="0fcd5-113">Jak serializować i deserializować dane JSON</span><span class="sxs-lookup"><span data-stu-id="0fcd5-113">How to serialize and deserialize JSON</span></span>](system-text-json-how-to.md)
* [<span data-ttu-id="0fcd5-114">Tworzenie wystąpienia JsonSerializerOptions wystąpień</span><span class="sxs-lookup"><span data-stu-id="0fcd5-114">Instantiate JsonSerializerOptions instances</span></span>](system-text-json-configure-options.md)
* [<span data-ttu-id="0fcd5-115">Dostosowywanie nazw i wartości właściwości</span><span class="sxs-lookup"><span data-stu-id="0fcd5-115">Customize property names and values</span></span>](system-text-json-customize-properties.md)
* [<span data-ttu-id="0fcd5-116">Ignorowanie właściwości</span><span class="sxs-lookup"><span data-stu-id="0fcd5-116">Ignore properties</span></span>](system-text-json-ignore-properties.md)
* [<span data-ttu-id="0fcd5-117">Zezwalanie na nieprawidłowy kod JSON</span><span class="sxs-lookup"><span data-stu-id="0fcd5-117">Allow invalid JSON</span></span>](system-text-json-invalid-json.md)
* [<span data-ttu-id="0fcd5-118">Obsługa przepełnienia kodu JSON</span><span class="sxs-lookup"><span data-stu-id="0fcd5-118">Handle overflow JSON</span></span>](system-text-json-handle-overflow.md)
* [<span data-ttu-id="0fcd5-119">Zachowywanie odwołań</span><span class="sxs-lookup"><span data-stu-id="0fcd5-119">Preserve references</span></span>](system-text-json-preserve-references.md)
* [<span data-ttu-id="0fcd5-120">Niemodyfikowalne typy i niepubliczne metody dostępu</span><span class="sxs-lookup"><span data-stu-id="0fcd5-120">Immutable types and non-public accessors</span></span>](system-text-json-immutability.md)
* [<span data-ttu-id="0fcd5-121">Serializacja polimorficzna</span><span class="sxs-lookup"><span data-stu-id="0fcd5-121">Polymorphic serialization</span></span>](system-text-json-polymorphism.md)
* [<span data-ttu-id="0fcd5-122">Migruj z Newtonsoft.Json do System.Text.Json</span><span class="sxs-lookup"><span data-stu-id="0fcd5-122">Migrate from Newtonsoft.Json to System.Text.Json</span></span>](system-text-json-migrate-from-newtonsoft-how-to.md)
* [<span data-ttu-id="0fcd5-123">Dostosowywanie kodowania znaków</span><span class="sxs-lookup"><span data-stu-id="0fcd5-123">Customize character encoding</span></span>](system-text-json-character-encoding.md)
* [<span data-ttu-id="0fcd5-124">Napisz niestandardowe serializatory i deserializatory</span><span class="sxs-lookup"><span data-stu-id="0fcd5-124">Write custom serializers and deserializers</span></span>](write-custom-serializer-deserializer.md)
* [<span data-ttu-id="0fcd5-125">Zapisz konwertery niestandardowe na potrzeby serializacji JSON</span><span class="sxs-lookup"><span data-stu-id="0fcd5-125">Write custom converters for JSON serialization</span></span>](system-text-json-converters-how-to.md)
* [<span data-ttu-id="0fcd5-126">Obsługa wartości DateTime i DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="0fcd5-126">DateTime and DateTimeOffset support</span></span>](../datetime/system-text-json-support.md)
* <span data-ttu-id="0fcd5-127">[System.Text.Json Dokumentacja interfejsu API](xref:System.Text.Json)</span><span class="sxs-lookup"><span data-stu-id="0fcd5-127">[System.Text.Json API reference](xref:System.Text.Json)</span></span>
* <span data-ttu-id="0fcd5-128">[System.Text.Json. Dokumentacja interfejsu API serializacji](xref:System.Text.Json.Serialization)</span><span class="sxs-lookup"><span data-stu-id="0fcd5-128">[System.Text.Json.Serialization API reference](xref:System.Text.Json.Serialization)</span></span>
