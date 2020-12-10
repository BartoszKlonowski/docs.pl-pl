---
title: Jak obsłużyć przepełnienie kodu JSON przy użyciu System.Text.Json
description: Dowiedz się, jak obsłużyć przepełnienie JSON podczas serializacji do i deserializacji z JSON w programie .NET.
ms.date: 11/30/2020
no-loc:
- System.Text.Json
- Newtonsoft.Json
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
ms.openlocfilehash: 265ce4f77d353720419122d17c36e508a377b68f
ms.sourcegitcommit: 81f1bba2c97a67b5ca76bcc57b37333ffca60c7b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/10/2020
ms.locfileid: "97008919"
---
# <a name="how-to-handle-overflow-json-with-no-locsystemtextjson"></a><span data-ttu-id="41628-103">Jak obsłużyć przepełnienie kodu JSON przy użyciu System.Text.Json</span><span class="sxs-lookup"><span data-stu-id="41628-103">How to handle overflow JSON with System.Text.Json</span></span>

<span data-ttu-id="41628-104">W tym artykule dowiesz się, jak obsłużyć przepełnienie kodu JSON przy użyciu `System.Text.Json` przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="41628-104">In this article, you will learn how to handle overflow JSON with the `System.Text.Json` namespace.</span></span>

## <a name="handle-overflow-json"></a><span data-ttu-id="41628-105">Obsługa przepełnienia kodu JSON</span><span class="sxs-lookup"><span data-stu-id="41628-105">Handle overflow JSON</span></span>

<span data-ttu-id="41628-106">Podczas deserializacji można odbierać dane w formacie JSON, które nie są reprezentowane przez właściwości typu docelowego.</span><span class="sxs-lookup"><span data-stu-id="41628-106">While deserializing, you might receive data in the JSON that is not represented by properties of the target type.</span></span> <span data-ttu-id="41628-107">Załóżmy na przykład, że typ docelowy to:</span><span class="sxs-lookup"><span data-stu-id="41628-107">For example, suppose your target type is this:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WF":::

<span data-ttu-id="41628-108">I kod JSON do deserializacji jest następujący:</span><span class="sxs-lookup"><span data-stu-id="41628-108">And the JSON to be deserialized is this:</span></span>

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "temperatureCelsius": 25,
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

<span data-ttu-id="41628-109">W przypadku deserializacji kodu JSON pokazanego w pokazanym typie, `DatesAvailable` `SummaryWords` właściwości i mają wartość Nowhere to go i są tracone.</span><span class="sxs-lookup"><span data-stu-id="41628-109">If you deserialize the JSON shown into the type shown, the `DatesAvailable` and `SummaryWords` properties have nowhere to go and are lost.</span></span> <span data-ttu-id="41628-110">Aby przechwycić dodatkowe dane, takie jak te właściwości, zastosuj atrybut [[JsonExtensionData]](xref:System.Text.Json.Serialization.JsonExtensionDataAttribute) do właściwości typu `Dictionary<string,object>` lub `Dictionary<string,JsonElement>` :</span><span class="sxs-lookup"><span data-stu-id="41628-110">To capture extra data such as these properties, apply the [[JsonExtensionData]](xref:System.Text.Json.Serialization.JsonExtensionDataAttribute) attribute to a property of type `Dictionary<string,object>` or `Dictionary<string,JsonElement>`:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithExtensionData":::

<span data-ttu-id="41628-111">Podczas deserializacji kodu JSON pokazanego wcześniej w tym typie próbkowania dodatkowe dane staną się parami klucz-wartość `ExtensionData` Właściwości:</span><span class="sxs-lookup"><span data-stu-id="41628-111">When you deserialize the JSON shown earlier into this sample type, the extra data becomes key-value pairs of the `ExtensionData` property:</span></span>

| <span data-ttu-id="41628-112">Właściwość</span><span class="sxs-lookup"><span data-stu-id="41628-112">Property</span></span> | <span data-ttu-id="41628-113">Wartość</span><span class="sxs-lookup"><span data-stu-id="41628-113">Value</span></span> | <span data-ttu-id="41628-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="41628-114">Notes</span></span> |
|--|--|--|
| `Date` | `"8/1/2019 12:00:00 AM -07:00"` |  |
| `TemperatureCelsius` | `0` | <span data-ttu-id="41628-115">Niezgodność z rozróżnianiem wielkości liter ( `temperatureCelsius` w formacie JSON), więc właściwość nie jest ustawiona.</span><span class="sxs-lookup"><span data-stu-id="41628-115">Case-sensitive mismatch (`temperatureCelsius` in the JSON), so the property isn't set.</span></span> |
| `Summary` | `"Hot"` |  |
| `ExtensionData` | `temperatureCelsius: 25` | <span data-ttu-id="41628-116">Ponieważ przypadek nie jest zgodny, ta właściwość JSON jest dodatkową i jest parą klucz-wartość w słowniku.</span><span class="sxs-lookup"><span data-stu-id="41628-116">Since the case didn't match, this JSON property is an extra and becomes a key-value pair in the dictionary.</span></span> |
| `DatesAvailable` | `[ "8/1/2019 12:00:00 AM -07:00", "8/2/2019 12:00:00 AM -07:00" ]` | <span data-ttu-id="41628-117">Dodatkowa Właściwość JSON zmieni się na parę klucz-wartość, z tablicą jako obiektem wartości.</span><span class="sxs-lookup"><span data-stu-id="41628-117">Extra property from the JSON becomes a key-value pair, with an array as the value object.</span></span> |
| `SummaryWords` | `[ "Cool", "Windy", "Humid" ]` | <span data-ttu-id="41628-118">Dodatkowa Właściwość JSON zmieni się na parę klucz-wartość, z tablicą jako obiektem wartości.</span><span class="sxs-lookup"><span data-stu-id="41628-118">Extra property from the JSON becomes a key-value pair, with an array as the value object.</span></span> |

<span data-ttu-id="41628-119">Gdy obiekt docelowy jest serializowany, pary wartości klucza danych rozszerzenia stają się właściwościami JSON tak samo jak w przychodzących danych JSON:</span><span class="sxs-lookup"><span data-stu-id="41628-119">When the target object is serialized, the extension data key value pairs become JSON properties just as they were in the incoming JSON:</span></span>

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 0,
  "Summary": "Hot",
  "temperatureCelsius": 25,
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

<span data-ttu-id="41628-120">Zauważ, że `ExtensionData` Nazwa właściwości nie pojawia się w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="41628-120">Notice that the `ExtensionData` property name doesn't appear in the JSON.</span></span> <span data-ttu-id="41628-121">Takie zachowanie umożliwia wykonywanie operacji okrężnych przez kod JSON bez utraty jakichkolwiek dodatkowych danych, które w przeciwnym razie nie zostały odszeregowane.</span><span class="sxs-lookup"><span data-stu-id="41628-121">This behavior lets the JSON make a round trip without losing any extra data that otherwise wouldn't be deserialized.</span></span>

## <a name="see-also"></a><span data-ttu-id="41628-122">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="41628-122">See also</span></span>

* [<span data-ttu-id="41628-123">System.Text.Json Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="41628-123">System.Text.Json overview</span></span>](system-text-json-overview.md)
* [<span data-ttu-id="41628-124">Jak serializować i deserializować dane JSON</span><span class="sxs-lookup"><span data-stu-id="41628-124">How to serialize and deserialize JSON</span></span>](system-text-json-how-to.md)
* [<span data-ttu-id="41628-125">Tworzenie wystąpienia JsonSerializerOptions wystąpień</span><span class="sxs-lookup"><span data-stu-id="41628-125">Instantiate JsonSerializerOptions instances</span></span>](system-text-json-configure-options.md)
* [<span data-ttu-id="41628-126">Włączanie dopasowywania bez uwzględniania wielkości liter</span><span class="sxs-lookup"><span data-stu-id="41628-126">Enable case-insensitive matching</span></span>](system-text-json-character-casing.md)
* [<span data-ttu-id="41628-127">Dostosowywanie nazw i wartości właściwości</span><span class="sxs-lookup"><span data-stu-id="41628-127">Customize property names and values</span></span>](system-text-json-customize-properties.md)
* [<span data-ttu-id="41628-128">Ignorowanie właściwości</span><span class="sxs-lookup"><span data-stu-id="41628-128">Ignore properties</span></span>](system-text-json-ignore-properties.md)
* [<span data-ttu-id="41628-129">Zezwalanie na nieprawidłowy kod JSON</span><span class="sxs-lookup"><span data-stu-id="41628-129">Allow invalid JSON</span></span>](system-text-json-invalid-json.md)
* [<span data-ttu-id="41628-130">Zachowywanie odwołań</span><span class="sxs-lookup"><span data-stu-id="41628-130">Preserve references</span></span>](system-text-json-preserve-references.md)
* [<span data-ttu-id="41628-131">Niemodyfikowalne typy i niepubliczne metody dostępu</span><span class="sxs-lookup"><span data-stu-id="41628-131">Immutable types and non-public accessors</span></span>](system-text-json-immutability.md)
* [<span data-ttu-id="41628-132">Serializacja polimorficzna</span><span class="sxs-lookup"><span data-stu-id="41628-132">Polymorphic serialization</span></span>](system-text-json-polymorphism.md)
* [<span data-ttu-id="41628-133">Migruj z Newtonsoft.Json do System.Text.Json</span><span class="sxs-lookup"><span data-stu-id="41628-133">Migrate from Newtonsoft.Json to System.Text.Json</span></span>](system-text-json-migrate-from-newtonsoft-how-to.md)
* [<span data-ttu-id="41628-134">Dostosowywanie kodowania znaków</span><span class="sxs-lookup"><span data-stu-id="41628-134">Customize character encoding</span></span>](system-text-json-character-encoding.md)
* [<span data-ttu-id="41628-135">Napisz niestandardowe serializatory i deserializatory</span><span class="sxs-lookup"><span data-stu-id="41628-135">Write custom serializers and deserializers</span></span>](write-custom-serializer-deserializer.md)
* [<span data-ttu-id="41628-136">Zapisz konwertery niestandardowe na potrzeby serializacji JSON</span><span class="sxs-lookup"><span data-stu-id="41628-136">Write custom converters for JSON serialization</span></span>](system-text-json-converters-how-to.md)
* [<span data-ttu-id="41628-137">Obsługa wartości DateTime i DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="41628-137">DateTime and DateTimeOffset support</span></span>](../datetime/system-text-json-support.md)
* <span data-ttu-id="41628-138">[System.Text.Json Dokumentacja interfejsu API](xref:System.Text.Json)</span><span class="sxs-lookup"><span data-stu-id="41628-138">[System.Text.Json API reference](xref:System.Text.Json)</span></span>
* <span data-ttu-id="41628-139">[System.Text.Json. Dokumentacja interfejsu API serializacji](xref:System.Text.Json.Serialization)</span><span class="sxs-lookup"><span data-stu-id="41628-139">[System.Text.Json.Serialization API reference](xref:System.Text.Json.Serialization)</span></span>
