---
title: Jak serializować właściwości klas pochodnych przy użyciu System.Text.Json
description: Dowiedz się, jak serializować obiekty polimorficzne podczas serializacji do i deserializacji z JSON w programie .NET.
ms.date: 11/30/2020
no-loc:
- System.Text.Json
- Newtonsoft.Json
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
ms.openlocfilehash: 4b99a402ea4f4c664d3bfd75627ffaf94948d493
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96439971"
---
# <a name="how-to-serialize-properties-of-derived-classes-with-no-locsystemtextjson"></a><span data-ttu-id="f38cb-103">Jak serializować właściwości klas pochodnych przy użyciu System.Text.Json</span><span class="sxs-lookup"><span data-stu-id="f38cb-103">How to serialize properties of derived classes with System.Text.Json</span></span>

<span data-ttu-id="f38cb-104">W tym artykule dowiesz się, jak serializować właściwości klas pochodnych z `System.Text.Json` przestrzenią nazw.</span><span class="sxs-lookup"><span data-stu-id="f38cb-104">In this article, you will learn how to serialize properties of derived classes with the `System.Text.Json` namespace.</span></span>

## <a name="serialize-properties-of-derived-classes"></a><span data-ttu-id="f38cb-105">Serializowanie właściwości klas pochodnych</span><span class="sxs-lookup"><span data-stu-id="f38cb-105">Serialize properties of derived classes</span></span>

<span data-ttu-id="f38cb-106">Serializacja hierarchii typów polimorficznych _nie_ jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="f38cb-106">Serialization of a polymorphic type hierarchy is _not_ supported.</span></span> <span data-ttu-id="f38cb-107">Na przykład, jeśli właściwość jest zdefiniowana jako interfejs lub Klasa abstrakcyjna, tylko właściwości zdefiniowane w interfejsie lub klasie abstrakcyjnej są serializowane, nawet jeśli typ środowiska uruchomieniowego ma dodatkowe właściwości.</span><span class="sxs-lookup"><span data-stu-id="f38cb-107">For example, if a property is defined as an interface or an abstract class, only the properties defined on the interface or abstract class are serialized, even if the runtime type has additional properties.</span></span> <span data-ttu-id="f38cb-108">Wyjątki dotyczące tego zachowania zostały omówione w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="f38cb-108">The exceptions to this behavior are explained in this section.</span></span>

<span data-ttu-id="f38cb-109">Załóżmy na przykład, że masz `WeatherForecast` klasę i klasę pochodną `WeatherForecastDerived` :</span><span class="sxs-lookup"><span data-stu-id="f38cb-109">For example, suppose you have a `WeatherForecast` class and a derived class `WeatherForecastDerived`:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WF":::

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFDerived":::

<span data-ttu-id="f38cb-110">I Załóżmy, że argument typu `Serialize` metody w czasie kompilacji to `WeatherForecast` :</span><span class="sxs-lookup"><span data-stu-id="f38cb-110">And suppose the type argument of the `Serialize` method at compile time is `WeatherForecast`:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/SerializePolymorphic.cs" id="SerializeDefault":::

<span data-ttu-id="f38cb-111">W tym scenariuszu `WindSpeed` Właściwość nie jest serializowana, nawet jeśli `weatherForecast` obiekt jest rzeczywiście `WeatherForecastDerived` obiektem.</span><span class="sxs-lookup"><span data-stu-id="f38cb-111">In this scenario, the `WindSpeed` property is not serialized even if the `weatherForecast` object is actually a `WeatherForecastDerived` object.</span></span> <span data-ttu-id="f38cb-112">Tylko właściwości klasy bazowej są serializowane:</span><span class="sxs-lookup"><span data-stu-id="f38cb-112">Only the base class properties are serialized:</span></span>

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot"
}
```

<span data-ttu-id="f38cb-113">Takie zachowanie ma na celu zapobieganie przypadkowemu narażeniu danych w pochodnym typie tworzonym przez środowisko uruchomieniowe.</span><span class="sxs-lookup"><span data-stu-id="f38cb-113">This behavior is intended to help prevent accidental exposure of data in a derived runtime-created type.</span></span>

<span data-ttu-id="f38cb-114">Aby serializować właściwości typu pochodnego w poprzednim przykładzie, należy użyć jednej z następujących metod:</span><span class="sxs-lookup"><span data-stu-id="f38cb-114">To serialize the properties of the derived type in the preceding example, use one of the following approaches:</span></span>

* <span data-ttu-id="f38cb-115">Wywołaj Przeciążenie <xref:System.Text.Json.JsonSerializer.Serialize%2A> , które pozwala określić typ w czasie wykonywania:</span><span class="sxs-lookup"><span data-stu-id="f38cb-115">Call an overload of <xref:System.Text.Json.JsonSerializer.Serialize%2A> that lets you specify the type at run time:</span></span>

  :::code language="csharp" source="snippets/system-text-json-how-to/csharp/SerializePolymorphic.cs" id="SerializeGetType":::

* <span data-ttu-id="f38cb-116">Zadeklaruj obiekt, który ma zostać Zserializowany jako `object` .</span><span class="sxs-lookup"><span data-stu-id="f38cb-116">Declare the object to be serialized as `object`.</span></span>

  :::code language="csharp" source="snippets/system-text-json-how-to/csharp/SerializePolymorphic.cs" id="SerializeObject":::

<span data-ttu-id="f38cb-117">W poprzednim przykładowym scenariuszu oba podejścia powodują, że `WindSpeed` Właściwość powinna zostać uwzględniona w danych wyjściowych JSON:</span><span class="sxs-lookup"><span data-stu-id="f38cb-117">In the preceding example scenario, both approaches cause the `WindSpeed` property to be included in the JSON output:</span></span>

```json
{
  "WindSpeed": 35,
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot"
}
```

> [!IMPORTANT]
> <span data-ttu-id="f38cb-118">Te podejścia zapewniają serializację polimorficzne tylko dla obiektu głównego, który ma być serializowany, a nie dla właściwości tego obiektu głównego.</span><span class="sxs-lookup"><span data-stu-id="f38cb-118">These approaches provide polymorphic serialization only for the root object to be serialized, not for properties of that root object.</span></span>

<span data-ttu-id="f38cb-119">Można uzyskać serializację polimorficzny dla obiektów niższego poziomu, jeśli zdefiniujesz je jako typ `object` .</span><span class="sxs-lookup"><span data-stu-id="f38cb-119">You can get polymorphic serialization for lower-level objects if you define them as type `object`.</span></span> <span data-ttu-id="f38cb-120">Na przykład załóżmy, `WeatherForecast` że Klasa ma właściwość o nazwie `PreviousForecast` , która może być zdefiniowana jako typ `WeatherForecast` lub `object` :</span><span class="sxs-lookup"><span data-stu-id="f38cb-120">For example, suppose your `WeatherForecast` class has a property named `PreviousForecast` that can be defined as type `WeatherForecast` or `object`:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithPrevious":::

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithPreviousAsObject":::

<span data-ttu-id="f38cb-121">Jeśli `PreviousForecast` Właściwość zawiera wystąpienie `WeatherForecastDerived` :</span><span class="sxs-lookup"><span data-stu-id="f38cb-121">If the `PreviousForecast` property contains an instance of `WeatherForecastDerived`:</span></span>

* <span data-ttu-id="f38cb-122">Dane wyjściowe JSON z serializacji `WeatherForecastWithPrevious` **nie obejmują** `WindSpeed` .</span><span class="sxs-lookup"><span data-stu-id="f38cb-122">The JSON output from serializing `WeatherForecastWithPrevious` **doesn't include** `WindSpeed`.</span></span>
* <span data-ttu-id="f38cb-123">Dane wyjściowe JSON z serializacji `WeatherForecastWithPreviousAsObject` **obejmują** `WindSpeed` .</span><span class="sxs-lookup"><span data-stu-id="f38cb-123">The JSON output from serializing `WeatherForecastWithPreviousAsObject` **includes** `WindSpeed`.</span></span>

<span data-ttu-id="f38cb-124">Aby serializować `WeatherForecastWithPreviousAsObject` , nie jest konieczne wywołanie `Serialize<object>` lub `GetType` ponieważ obiekt główny nie jest tym, który może znajdować się w typie pochodnym.</span><span class="sxs-lookup"><span data-stu-id="f38cb-124">To serialize `WeatherForecastWithPreviousAsObject`, it isn't necessary to call `Serialize<object>` or `GetType` because the root object isn't the one that may be of a derived type.</span></span> <span data-ttu-id="f38cb-125">Poniższy przykład kodu nie wywołuje `Serialize<object>` lub `GetType` :</span><span class="sxs-lookup"><span data-stu-id="f38cb-125">The following code example doesn't call `Serialize<object>` or `GetType`:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/SerializePolymorphic.cs" id="SerializeSecondLevel":::

<span data-ttu-id="f38cb-126">Powyższy kod poprawnie serializować `WeatherForecastWithPreviousAsObject` :</span><span class="sxs-lookup"><span data-stu-id="f38cb-126">The preceding code correctly serializes `WeatherForecastWithPreviousAsObject`:</span></span>

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot",
  "PreviousForecast": {
    "WindSpeed": 35,
    "Date": "2019-08-01T00:00:00-07:00",
    "TemperatureCelsius": 25,
    "Summary": "Hot"
  }
}
```

<span data-ttu-id="f38cb-127">To samo podejście do definiowania właściwości jako `object` współdziałanie z interfejsami.</span><span class="sxs-lookup"><span data-stu-id="f38cb-127">The same approach of defining properties as `object` works with interfaces.</span></span> <span data-ttu-id="f38cb-128">Załóżmy, że masz następujący interfejs i implementacja, i chcesz serializować klasę o właściwościach zawierających wystąpienia implementacji:</span><span class="sxs-lookup"><span data-stu-id="f38cb-128">Suppose you have the following interface and implementation, and you want to serialize a class with properties that contain implementation instances:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/IForecast.cs":::

<span data-ttu-id="f38cb-129">Podczas serializacji wystąpienia elementu `Forecasts` , `Tuesday` wyświetlana `WindSpeed` jest tylko właściwość, ponieważ `Tuesday` jest zdefiniowana jako `object` :</span><span class="sxs-lookup"><span data-stu-id="f38cb-129">When you serialize an instance of `Forecasts`, only `Tuesday` shows the `WindSpeed` property, because `Tuesday` is defined as `object`:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/SerializePolymorphic.cs" id="SerializeInterface":::

<span data-ttu-id="f38cb-130">Poniższy przykład pokazuje kod JSON, który wynika z poprzedniego kodu:</span><span class="sxs-lookup"><span data-stu-id="f38cb-130">The following example shows the JSON that results from the preceding code:</span></span>

```json
{
  "Monday": {
    "Date": "2020-01-06T00:00:00-08:00",
    "TemperatureCelsius": 10,
    "Summary": "Cool"
  },
  "Tuesday": {
    "Date": "2020-01-07T00:00:00-08:00",
    "TemperatureCelsius": 11,
    "Summary": "Rainy",
    "WindSpeed": 10
  }
}
```

<span data-ttu-id="f38cb-131">Aby uzyskać więcej informacji na temat **serializacji** polimorficznej i informacje o **deserializacji**, zobacz [Jak przeprowadzić migrację z Newtonsoft.Json do System.Text.Json](system-text-json-migrate-from-newtonsoft-how-to.md#polymorphic-serialization).</span><span class="sxs-lookup"><span data-stu-id="f38cb-131">For more information about polymorphic **serialization**, and for information about **deserialization**, see [How to migrate from Newtonsoft.Json to System.Text.Json](system-text-json-migrate-from-newtonsoft-how-to.md#polymorphic-serialization).</span></span>

## <a name="see-also"></a><span data-ttu-id="f38cb-132">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="f38cb-132">See also</span></span>

* [<span data-ttu-id="f38cb-133">System.Text.Json Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="f38cb-133">System.Text.Json overview</span></span>](system-text-json-overview.md)
* [<span data-ttu-id="f38cb-134">Tworzenie wystąpienia JsonSerializerOptions</span><span class="sxs-lookup"><span data-stu-id="f38cb-134">Instantiate JsonSerializerOptions</span></span>](system-text-json-configure-options.md)
* [<span data-ttu-id="f38cb-135">Włącz dopasowywanie bez uwzględniania wielkości liter</span><span class="sxs-lookup"><span data-stu-id="f38cb-135">Enable case-insensitive matching</span></span>](system-text-json-character-casing.md)
* [<span data-ttu-id="f38cb-136">Dostosowywanie nazw i wartości właściwości</span><span class="sxs-lookup"><span data-stu-id="f38cb-136">Customize property names and values</span></span>](system-text-json-customize-properties.md)
* [<span data-ttu-id="f38cb-137">Ignoruj właściwości</span><span class="sxs-lookup"><span data-stu-id="f38cb-137">Ignore properties</span></span>](system-text-json-ignore-properties.md)
* [<span data-ttu-id="f38cb-138">Zezwalaj na nieprawidłowy kod JSON</span><span class="sxs-lookup"><span data-stu-id="f38cb-138">Allow invalid JSON</span></span>](system-text-json-invalid-json.md)
* [<span data-ttu-id="f38cb-139">Obsługa przepełnienia kodu JSON</span><span class="sxs-lookup"><span data-stu-id="f38cb-139">Handle overflow JSON</span></span>](system-text-json-handle-overflow.md)
* [<span data-ttu-id="f38cb-140">Zachowaj odwołania cykliczne</span><span class="sxs-lookup"><span data-stu-id="f38cb-140">Preserve circular references</span></span>](system-text-json-preserve-references.md)
* [<span data-ttu-id="f38cb-141">Niemodyfikowalne typy i niepubliczne metody dostępu</span><span class="sxs-lookup"><span data-stu-id="f38cb-141">Immutable types and non-public accessors</span></span>](system-text-json-immutability.md)
* <span data-ttu-id="f38cb-142">[System.Text.Json Dokumentacja interfejsu API](xref:System.Text.Json)</span><span class="sxs-lookup"><span data-stu-id="f38cb-142">[System.Text.Json API reference](xref:System.Text.Json)</span></span>
