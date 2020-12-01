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
ms.openlocfilehash: 2c40d42b26bc5bd05f592cc51c6b5b9b4c6bbd9e
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96439982"
---
# <a name="how-to-handle-overflow-json-with-no-locsystemtextjson"></a><span data-ttu-id="dc396-103">Jak obsłużyć przepełnienie kodu JSON przy użyciu System.Text.Json</span><span class="sxs-lookup"><span data-stu-id="dc396-103">How to handle overflow JSON with System.Text.Json</span></span>

<span data-ttu-id="dc396-104">W tym artykule dowiesz się, jak obsłużyć przepełnienie kodu JSON przy użyciu `System.Text.Json` przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="dc396-104">In this article, you will learn how to handle overflow JSON with the `System.Text.Json` namespace.</span></span>

## <a name="handle-overflow-json"></a><span data-ttu-id="dc396-105">Obsługa przepełnienia kodu JSON</span><span class="sxs-lookup"><span data-stu-id="dc396-105">Handle overflow JSON</span></span>

<span data-ttu-id="dc396-106">Podczas deserializacji można odbierać dane w formacie JSON, które nie są reprezentowane przez właściwości typu docelowego.</span><span class="sxs-lookup"><span data-stu-id="dc396-106">While deserializing, you might receive data in the JSON that is not represented by properties of the target type.</span></span> <span data-ttu-id="dc396-107">Załóżmy na przykład, że typ docelowy to:</span><span class="sxs-lookup"><span data-stu-id="dc396-107">For example, suppose your target type is this:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WF":::

<span data-ttu-id="dc396-108">I kod JSON do deserializacji jest następujący:</span><span class="sxs-lookup"><span data-stu-id="dc396-108">And the JSON to be deserialized is this:</span></span>

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

<span data-ttu-id="dc396-109">W przypadku deserializacji kodu JSON pokazanego w pokazanym typie, `DatesAvailable` `SummaryWords` właściwości i mają wartość Nowhere to go i są tracone.</span><span class="sxs-lookup"><span data-stu-id="dc396-109">If you deserialize the JSON shown into the type shown, the `DatesAvailable` and `SummaryWords` properties have nowhere to go and are lost.</span></span> <span data-ttu-id="dc396-110">Aby przechwycić dodatkowe dane, takie jak te właściwości, zastosuj atrybut [[JsonExtensionData]](xref:System.Text.Json.Serialization.JsonExtensionDataAttribute) do właściwości typu `Dictionary<string,object>` lub `Dictionary<string,JsonElement>` :</span><span class="sxs-lookup"><span data-stu-id="dc396-110">To capture extra data such as these properties, apply the [[JsonExtensionData]](xref:System.Text.Json.Serialization.JsonExtensionDataAttribute) attribute to a property of type `Dictionary<string,object>` or `Dictionary<string,JsonElement>`:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithExtensionData":::

<span data-ttu-id="dc396-111">Podczas deserializacji kodu JSON pokazanego wcześniej w tym typie próbkowania dodatkowe dane staną się parami klucz-wartość `ExtensionData` Właściwości:</span><span class="sxs-lookup"><span data-stu-id="dc396-111">When you deserialize the JSON shown earlier into this sample type, the extra data becomes key-value pairs of the `ExtensionData` property:</span></span>

| <span data-ttu-id="dc396-112">Właściwość</span><span class="sxs-lookup"><span data-stu-id="dc396-112">Property</span></span> | <span data-ttu-id="dc396-113">Wartość</span><span class="sxs-lookup"><span data-stu-id="dc396-113">Value</span></span> | <span data-ttu-id="dc396-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="dc396-114">Notes</span></span> |
|--|--|--|
| `Date` | `"8/1/2019 12:00:00 AM -07:00"` |  |
| `TemperatureCelsius` | `0` | <span data-ttu-id="dc396-115">Niezgodność z rozróżnianiem wielkości liter ( `temperatureCelsius` w formacie JSON), więc właściwość nie jest ustawiona.</span><span class="sxs-lookup"><span data-stu-id="dc396-115">Case-sensitive mismatch (`temperatureCelsius` in the JSON), so the property isn't set.</span></span> |
| `Summary` | `"Hot"` |  |
| `ExtensionData` | `temperatureCelsius: 25` | <span data-ttu-id="dc396-116">Ponieważ przypadek nie jest zgodny, ta właściwość JSON jest dodatkową i jest parą klucz-wartość w słowniku.</span><span class="sxs-lookup"><span data-stu-id="dc396-116">Since the case didn't match, this JSON property is an extra and becomes a key-value pair in the dictionary.</span></span> |
| `DatesAvailable` | `[ "8/1/2019 12:00:00 AM -07:00", "8/2/2019 12:00:00 AM -07:00" ]` | <span data-ttu-id="dc396-117">Dodatkowa Właściwość JSON zmieni się na parę klucz-wartość, z tablicą jako obiektem wartości.</span><span class="sxs-lookup"><span data-stu-id="dc396-117">Extra property from the JSON becomes a key-value pair, with an array as the value object.</span></span> |
| `SummaryWords` | `[ "Cool", "Windy", "Humid" ]` | <span data-ttu-id="dc396-118">Dodatkowa Właściwość JSON zmieni się na parę klucz-wartość, z tablicą jako obiektem wartości.</span><span class="sxs-lookup"><span data-stu-id="dc396-118">Extra property from the JSON becomes a key-value pair, with an array as the value object.</span></span> |

<span data-ttu-id="dc396-119">Gdy obiekt docelowy jest serializowany, pary wartości klucza danych rozszerzenia stają się właściwościami JSON tak samo jak w przychodzących danych JSON:</span><span class="sxs-lookup"><span data-stu-id="dc396-119">When the target object is serialized, the extension data key value pairs become JSON properties just as they were in the incoming JSON:</span></span>

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

<span data-ttu-id="dc396-120">Zauważ, że `ExtensionData` Nazwa właściwości nie pojawia się w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="dc396-120">Notice that the `ExtensionData` property name doesn't appear in the JSON.</span></span> <span data-ttu-id="dc396-121">Takie zachowanie umożliwia wykonywanie operacji okrężnych przez kod JSON bez utraty jakichkolwiek dodatkowych danych, które w przeciwnym razie nie zostały odszeregowane.</span><span class="sxs-lookup"><span data-stu-id="dc396-121">This behavior lets the JSON make a round trip without losing any extra data that otherwise wouldn't be deserialized.</span></span>

## <a name="see-also"></a><span data-ttu-id="dc396-122">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="dc396-122">See also</span></span>

* [<span data-ttu-id="dc396-123">System.Text.Json Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="dc396-123">System.Text.Json overview</span></span>](system-text-json-overview.md)
* [<span data-ttu-id="dc396-124">Tworzenie wystąpienia JsonSerializerOptions</span><span class="sxs-lookup"><span data-stu-id="dc396-124">Instantiate JsonSerializerOptions</span></span>](system-text-json-configure-options.md)
* [<span data-ttu-id="dc396-125">Włącz dopasowywanie bez uwzględniania wielkości liter</span><span class="sxs-lookup"><span data-stu-id="dc396-125">Enable case-insensitive matching</span></span>](system-text-json-character-casing.md)
* [<span data-ttu-id="dc396-126">Dostosowywanie nazw i wartości właściwości</span><span class="sxs-lookup"><span data-stu-id="dc396-126">Customize property names and values</span></span>](system-text-json-customize-properties.md)
* [<span data-ttu-id="dc396-127">Ignoruj właściwości</span><span class="sxs-lookup"><span data-stu-id="dc396-127">Ignore properties</span></span>](system-text-json-ignore-properties.md)
* [<span data-ttu-id="dc396-128">Zezwalaj na nieprawidłowy kod JSON</span><span class="sxs-lookup"><span data-stu-id="dc396-128">Allow invalid JSON</span></span>](system-text-json-invalid-json.md)
* [<span data-ttu-id="dc396-129">Zachowaj odwołania cykliczne</span><span class="sxs-lookup"><span data-stu-id="dc396-129">Preserve circular references</span></span>](system-text-json-preserve-references.md)
* [<span data-ttu-id="dc396-130">Niemodyfikowalne typy i niepubliczne metody dostępu</span><span class="sxs-lookup"><span data-stu-id="dc396-130">Immutable types and non-public accessors</span></span>](system-text-json-immutability.md)
* [<span data-ttu-id="dc396-131">Serializacja polimorficzna</span><span class="sxs-lookup"><span data-stu-id="dc396-131">Polymorphic serialization</span></span>](system-text-json-polymorphism.md)
* <span data-ttu-id="dc396-132">[System.Text.Json Dokumentacja interfejsu API](xref:System.Text.Json)</span><span class="sxs-lookup"><span data-stu-id="dc396-132">[System.Text.Json API reference](xref:System.Text.Json)</span></span>
