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
ms.openlocfilehash: 4bd57d32120f51ffd1ff09c9817edbafa28a3f19
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96439946"
---
# <a name="how-to-enable-case-insensitive-property-name-matching-with-no-locsystemtextjson"></a><span data-ttu-id="735b5-103">Jak włączyć Dopasowywanie nazw właściwości bez uwzględniania wielkości liter System.Text.Json</span><span class="sxs-lookup"><span data-stu-id="735b5-103">How to enable case-insensitive property name matching with System.Text.Json</span></span>

<span data-ttu-id="735b5-104">W tym artykule dowiesz się, jak włączyć Dopasowywanie nazw właściwości bez uwzględniania wielkości liter w `System.Text.Json` przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="735b5-104">In this article, you will learn how to enable case-insensitive property name matching with the `System.Text.Json` namespace.</span></span>

## <a name="case-insensitive-property-matching"></a><span data-ttu-id="735b5-105">Dopasowanie właściwości bez uwzględniania wielkości liter</span><span class="sxs-lookup"><span data-stu-id="735b5-105">Case-insensitive property matching</span></span>

<span data-ttu-id="735b5-106">Domyślnie deserializacja wyszukuje dopasowania nazw właściwości z uwzględnieniem wielkości liter między formatem JSON a właściwościami obiektu docelowego.</span><span class="sxs-lookup"><span data-stu-id="735b5-106">By default, deserialization looks for case-sensitive property name matches between JSON and the target object properties.</span></span> <span data-ttu-id="735b5-107">Aby zmienić to zachowanie, ustaw opcję <xref:System.Text.Json.JsonSerializerOptions.PropertyNameCaseInsensitive?displayProperty=nameWithType> na `true` :</span><span class="sxs-lookup"><span data-stu-id="735b5-107">To change that behavior, set <xref:System.Text.Json.JsonSerializerOptions.PropertyNameCaseInsensitive?displayProperty=nameWithType> to `true`:</span></span>

> [!NOTE]
> <span data-ttu-id="735b5-108">W [ustawieniach domyślnych sieci Web](system-text-json-configure-options.md#web-defaults-for-jsonserializeroptions) jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="735b5-108">The [web defaults](system-text-json-configure-options.md#web-defaults-for-jsonserializeroptions) is case-insensitive.</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/DeserializeCaseInsensitive.cs" id="Deserialize":::

<span data-ttu-id="735b5-109">Oto przykład JSON z nazwami właściwości przypadku notacji CamelCase.</span><span class="sxs-lookup"><span data-stu-id="735b5-109">Here's example JSON with camel case property names.</span></span> <span data-ttu-id="735b5-110">Można ją zdeserializować do następującego typu, który ma nazwy właściwości przypadku języka Pascal.</span><span class="sxs-lookup"><span data-stu-id="735b5-110">It can be deserialized into the following type that has Pascal case property names.</span></span>

```json
{
  "date": "2019-08-01T00:00:00-07:00",
  "temperatureCelsius": 25,
  "summary": "Hot",
}
```

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WF":::

## <a name="see-also"></a><span data-ttu-id="735b5-111">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="735b5-111">See also</span></span>

* [<span data-ttu-id="735b5-112">System.Text.Json Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="735b5-112">System.Text.Json overview</span></span>](system-text-json-overview.md)
* [<span data-ttu-id="735b5-113">Tworzenie wystąpienia JsonSerializerOptions</span><span class="sxs-lookup"><span data-stu-id="735b5-113">Instantiate JsonSerializerOptions</span></span>](system-text-json-configure-options.md)
* [<span data-ttu-id="735b5-114">Dostosowywanie nazw i wartości właściwości</span><span class="sxs-lookup"><span data-stu-id="735b5-114">Customize property names and values</span></span>](system-text-json-customize-properties.md)
* [<span data-ttu-id="735b5-115">Ignoruj właściwości</span><span class="sxs-lookup"><span data-stu-id="735b5-115">Ignore properties</span></span>](system-text-json-ignore-properties.md)
* [<span data-ttu-id="735b5-116">Zezwalaj na nieprawidłowy kod JSON</span><span class="sxs-lookup"><span data-stu-id="735b5-116">Allow invalid JSON</span></span>](system-text-json-invalid-json.md)
* [<span data-ttu-id="735b5-117">Obsługa przepełnienia kodu JSON</span><span class="sxs-lookup"><span data-stu-id="735b5-117">Handle overflow JSON</span></span>](system-text-json-handle-overflow.md)
* [<span data-ttu-id="735b5-118">Zachowaj odwołania cykliczne</span><span class="sxs-lookup"><span data-stu-id="735b5-118">Preserve circular references</span></span>](system-text-json-preserve-references.md)
* [<span data-ttu-id="735b5-119">Niemodyfikowalne typy i niepubliczne metody dostępu</span><span class="sxs-lookup"><span data-stu-id="735b5-119">Immutable types and non-public accessors</span></span>](system-text-json-immutability.md)
* [<span data-ttu-id="735b5-120">Serializacja polimorficzna</span><span class="sxs-lookup"><span data-stu-id="735b5-120">Polymorphic serialization</span></span>](system-text-json-polymorphism.md)
* <span data-ttu-id="735b5-121">[System.Text.Json Dokumentacja interfejsu API](xref:System.Text.Json)</span><span class="sxs-lookup"><span data-stu-id="735b5-121">[System.Text.Json API reference](xref:System.Text.Json)</span></span>
