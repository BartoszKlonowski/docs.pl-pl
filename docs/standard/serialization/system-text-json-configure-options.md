---
title: Jak utworzyć wystąpienie JsonSerializerOptions z System.Text.Json
description: Dowiedz się, jak uniknąć problemów z wydajnością oraz jak używać konstruktorów dostępnych dla wystąpień JsonSerializerOptions.
ms.date: 12/02/2020
no-loc:
- System.Text.Json
- Newtonsoft.Json
zone_pivot_groups: dotnet-version
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
ms.openlocfilehash: 5f32e1369e58dd9550f28abc822f187dee46c022
ms.sourcegitcommit: 81f1bba2c97a67b5ca76bcc57b37333ffca60c7b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/10/2020
ms.locfileid: "97009836"
---
# <a name="how-to-instantiate-jsonserializeroptions-instances-with-no-locsystemtextjson"></a><span data-ttu-id="81948-103">Jak utworzyć wystąpienie JsonSerializerOptions wystąpień z System.Text.Json</span><span class="sxs-lookup"><span data-stu-id="81948-103">How to instantiate JsonSerializerOptions instances with System.Text.Json</span></span>

<span data-ttu-id="81948-104">W tym artykule wyjaśniono, jak uniknąć problemów z wydajnością podczas korzystania z programu <xref:System.Text.Json.JsonSerializerOptions> .</span><span class="sxs-lookup"><span data-stu-id="81948-104">This article explains how to avoid performance problems when you use <xref:System.Text.Json.JsonSerializerOptions>.</span></span> <span data-ttu-id="81948-105">Pokazano również, jak używać konstruktorów sparametryzowanych, które są dostępne.</span><span class="sxs-lookup"><span data-stu-id="81948-105">It also shows how to use the parameterized constructors that are available.</span></span>

## <a name="reuse-jsonserializeroptions-instances"></a><span data-ttu-id="81948-106">Ponowne użycie wystąpień JsonSerializerOptions</span><span class="sxs-lookup"><span data-stu-id="81948-106">Reuse JsonSerializerOptions instances</span></span>

<span data-ttu-id="81948-107">Jeśli używasz `JsonSerializerOptions` wielokrotnie z tymi samymi opcjami, nie twórz nowego `JsonSerializerOptions` wystąpienia za każdym razem, gdy go używasz.</span><span class="sxs-lookup"><span data-stu-id="81948-107">If you use `JsonSerializerOptions` repeatedly with the same options, don't create a new `JsonSerializerOptions` instance each time you use it.</span></span> <span data-ttu-id="81948-108">Ponownie Użyj tego samego wystąpienia dla każdego wywołania.</span><span class="sxs-lookup"><span data-stu-id="81948-108">Reuse the same instance for every call.</span></span> <span data-ttu-id="81948-109">Te wskazówki odnoszą się do kodu zapisanego w przypadku konwerterów niestandardowych i podczas wywoływania <xref:System.Text.Json.JsonSerializer.Serialize%2A?displayProperty=nameWithType> lub <xref:System.Text.Json.JsonSerializer.Deserialize%2A?displayProperty=nameWithType> .</span><span class="sxs-lookup"><span data-stu-id="81948-109">This guidance applies to code you write for custom converters and when you call <xref:System.Text.Json.JsonSerializer.Serialize%2A?displayProperty=nameWithType> or <xref:System.Text.Json.JsonSerializer.Deserialize%2A?displayProperty=nameWithType>.</span></span>

<span data-ttu-id="81948-110">Poniższy kod ilustruje spadek wydajności przy użyciu nowych wystąpień opcji.</span><span class="sxs-lookup"><span data-stu-id="81948-110">The following code demonstrates the performance penalty for using new options instances.</span></span>

:::code language="csharp" source="snippets/system-text-json-configure-options/csharp/ReuseOptionsInstances.cs":::

<span data-ttu-id="81948-111">Poprzedni kod serializować mały obiekt 100 000 razy przy użyciu tego samego wystąpienia opcji.</span><span class="sxs-lookup"><span data-stu-id="81948-111">The preceding code serializes a small object 100,000 times using the same options instance.</span></span> <span data-ttu-id="81948-112">Następnie deserializacji ten sam obiekt o tej samej liczbie razy i tworzy nowe wystąpienie opcji za każdym razem.</span><span class="sxs-lookup"><span data-stu-id="81948-112">Then it serializes the same object the same number of times and creates a new options instance each time.</span></span> <span data-ttu-id="81948-113">Typowa różnica czasu wykonywania jest 190 w porównaniu do 40 140 milisekund.</span><span class="sxs-lookup"><span data-stu-id="81948-113">A typical run time difference is 190 compared to 40,140 milliseconds.</span></span> <span data-ttu-id="81948-114">Różnica jest jeszcze większa w przypadku zwiększenia liczby iteracji.</span><span class="sxs-lookup"><span data-stu-id="81948-114">The difference is even greater if you increase the number of iterations.</span></span>

<span data-ttu-id="81948-115">Serializator przeprowadzi fazę rozgrzewania podczas pierwszej serializacji każdego typu na grafie obiektów, gdy do niego zostanie przesłane nowe wystąpienie opcji.</span><span class="sxs-lookup"><span data-stu-id="81948-115">The serializer undergoes a warm-up phase during the first serialization of each type in the object graph when a new options instance is passed to it.</span></span> <span data-ttu-id="81948-116">Ta rozgrzewanie obejmuje tworzenie pamięci podręcznej metadanych, która jest wymagana do serializacji.</span><span class="sxs-lookup"><span data-stu-id="81948-116">This warm-up includes creating a cache of metadata that is needed for serialization.</span></span> <span data-ttu-id="81948-117">Metadane obejmują delegatów do metod pobierających właściwości, Setters, argumentów konstruktora, określonych atrybutów i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="81948-117">The metadata includes delegates to property getters, setters, constructor arguments, specified attributes, and so forth.</span></span> <span data-ttu-id="81948-118">Ta pamięć podręczna metadanych jest przechowywana w wystąpieniu opcji.</span><span class="sxs-lookup"><span data-stu-id="81948-118">This metadata cache is stored in the options instance.</span></span> <span data-ttu-id="81948-119">Ten sam proces rozgrzewania i pamięć podręczna stosuje się do deserializacji.</span><span class="sxs-lookup"><span data-stu-id="81948-119">The same warm-up process and cache applies to deserialization.</span></span>

<span data-ttu-id="81948-120">Rozmiar pamięci podręcznej metadanych w `JsonSerializerOptions` wystąpieniu zależy od liczby typów do serializacji.</span><span class="sxs-lookup"><span data-stu-id="81948-120">The size of the metadata cache in a `JsonSerializerOptions` instance depends on the number of types to be serialized.</span></span> <span data-ttu-id="81948-121">W przypadku przekazania wielu typów — na przykład dynamicznie generowanych typów — do serializatora rozmiar pamięci podręcznej będzie nadal wzrastał i może zakończyć działanie `OutOfMemoryException` .</span><span class="sxs-lookup"><span data-stu-id="81948-121">If you pass numerous types—for example, dynamically generated types—to the serializer, the cache size will continue to grow and can end up causing an `OutOfMemoryException`.</span></span>

## <a name="copy-jsonserializeroptions"></a><span data-ttu-id="81948-122">Kopiuj JsonSerializerOptions</span><span class="sxs-lookup"><span data-stu-id="81948-122">Copy JsonSerializerOptions</span></span>

::: zone pivot="dotnet-5-0"
<span data-ttu-id="81948-123">Istnieje Konstruktor [JsonSerializerOptions] (linki XREF: System.Text.Json . JsonSerializerOptions .% 23ctor ( System.Text.Json . JsonSerializerOptions)), która umożliwia utworzenie nowego wystąpienia z takimi samymi opcjami jak istniejące wystąpienie, jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="81948-123">There is a [JsonSerializerOptions constructor](xref:System.Text.Json.JsonSerializerOptions.%23ctor(System.Text.Json.JsonSerializerOptions)) that lets you create a new instance with the same options as an existing instance, as shown in the following example:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/CopyOptions.cs" highlight="29":::
::: zone-end

::: zone pivot="dotnet-core-3-1"
<span data-ttu-id="81948-124">`JsonSerializerOptions`Konstruktor, który pobiera istniejące wystąpienie, nie jest dostępny w programie .NET Core 3,1.</span><span class="sxs-lookup"><span data-stu-id="81948-124">A `JsonSerializerOptions` constructor that takes an existing instance is not available in .NET Core 3.1.</span></span>
::: zone-end

## <a name="web-defaults-for-jsonserializeroptions"></a><span data-ttu-id="81948-125">Ustawienia domyślne sieci Web dla JsonSerializerOptions</span><span class="sxs-lookup"><span data-stu-id="81948-125">Web defaults for JsonSerializerOptions</span></span>

::: zone pivot="dotnet-5-0"
<span data-ttu-id="81948-126">Poniżej przedstawiono opcje, które mają różne wartości domyślne dla usługi Web Apps:</span><span class="sxs-lookup"><span data-stu-id="81948-126">Here are the options that have different defaults for web apps:</span></span>

* <xref:System.Text.Json.JsonSerializerOptions.PropertyNameCaseInsensitive%2A> = `true`
* <xref:System.Text.Json.JsonNamingPolicy> = <xref:System.Text.Json.JsonNamingPolicy.CamelCase>
* <xref:System.Text.Json.JsonSerializerOptions.NumberHandling%2A> = <xref:System.Text.Json.Serialization.JsonNumberHandling.AllowReadingFromString>

<span data-ttu-id="81948-127">Istnieje Konstruktor [JsonSerializerOptions] (linki XREF: System.Text.Json . JsonSerializerOptions .% 23ctor ( System.Text.Json . JsonSerializerDefaults)? View = NET-5,0&Preserve-View = true), która umożliwia utworzenie nowego wystąpienia z opcjami domyślnymi, które ASP.NET Core używane przez aplikacje sieci Web, jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="81948-127">There's a [JsonSerializerOptions constructor](xref:System.Text.Json.JsonSerializerOptions.%23ctor(System.Text.Json.JsonSerializerDefaults)?view=net-5.0&preserve-view=true) that lets you create a new instance with the default options that ASP.NET Core uses for web apps, as shown in the following example:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/OptionsDefaults.cs" highlight="24":::
::: zone-end

::: zone pivot="dotnet-core-3-1"
<span data-ttu-id="81948-128">Poniżej przedstawiono opcje, które mają różne wartości domyślne dla usługi Web Apps:</span><span class="sxs-lookup"><span data-stu-id="81948-128">Here are the options that have different defaults for web apps:</span></span>

* <xref:System.Text.Json.JsonSerializerOptions.PropertyNameCaseInsensitive%2A> = `true`
* <xref:System.Text.Json.JsonNamingPolicy> = <xref:System.Text.Json.JsonNamingPolicy.CamelCase>

<span data-ttu-id="81948-129">`JsonSerializerOptions`Konstruktor, który określa zestaw ustawień domyślnych, nie jest dostępny w programie .NET Core 3,1.</span><span class="sxs-lookup"><span data-stu-id="81948-129">A `JsonSerializerOptions` constructor that specifies a set of defaults is not available in .NET Core 3.1.</span></span>
::: zone-end

## <a name="see-also"></a><span data-ttu-id="81948-130">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="81948-130">See also</span></span>

* [<span data-ttu-id="81948-131">System.Text.Json Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="81948-131">System.Text.Json overview</span></span>](system-text-json-overview.md)
* [<span data-ttu-id="81948-132">Jak serializować i deserializować dane JSON</span><span class="sxs-lookup"><span data-stu-id="81948-132">How to serialize and deserialize JSON</span></span>](system-text-json-how-to.md)
* [<span data-ttu-id="81948-133">Włączanie dopasowywania bez uwzględniania wielkości liter</span><span class="sxs-lookup"><span data-stu-id="81948-133">Enable case-insensitive matching</span></span>](system-text-json-character-casing.md)
* [<span data-ttu-id="81948-134">Dostosowywanie nazw i wartości właściwości</span><span class="sxs-lookup"><span data-stu-id="81948-134">Customize property names and values</span></span>](system-text-json-customize-properties.md)
* [<span data-ttu-id="81948-135">Ignorowanie właściwości</span><span class="sxs-lookup"><span data-stu-id="81948-135">Ignore properties</span></span>](system-text-json-ignore-properties.md)
* [<span data-ttu-id="81948-136">Zezwalanie na nieprawidłowy kod JSON</span><span class="sxs-lookup"><span data-stu-id="81948-136">Allow invalid JSON</span></span>](system-text-json-invalid-json.md)
* [<span data-ttu-id="81948-137">Obsługa przepełnienia kodu JSON</span><span class="sxs-lookup"><span data-stu-id="81948-137">Handle overflow JSON</span></span>](system-text-json-handle-overflow.md)
* [<span data-ttu-id="81948-138">Zachowywanie odwołań</span><span class="sxs-lookup"><span data-stu-id="81948-138">Preserve references</span></span>](system-text-json-preserve-references.md)
* [<span data-ttu-id="81948-139">Niemodyfikowalne typy i niepubliczne metody dostępu</span><span class="sxs-lookup"><span data-stu-id="81948-139">Immutable types and non-public accessors</span></span>](system-text-json-immutability.md)
* [<span data-ttu-id="81948-140">Serializacja polimorficzna</span><span class="sxs-lookup"><span data-stu-id="81948-140">Polymorphic serialization</span></span>](system-text-json-polymorphism.md)
* [<span data-ttu-id="81948-141">Migruj z Newtonsoft.Json do System.Text.Json</span><span class="sxs-lookup"><span data-stu-id="81948-141">Migrate from Newtonsoft.Json to System.Text.Json</span></span>](system-text-json-migrate-from-newtonsoft-how-to.md)
* [<span data-ttu-id="81948-142">Dostosowywanie kodowania znaków</span><span class="sxs-lookup"><span data-stu-id="81948-142">Customize character encoding</span></span>](system-text-json-character-encoding.md)
* [<span data-ttu-id="81948-143">Napisz niestandardowe serializatory i deserializatory</span><span class="sxs-lookup"><span data-stu-id="81948-143">Write custom serializers and deserializers</span></span>](write-custom-serializer-deserializer.md)
* [<span data-ttu-id="81948-144">Zapisz konwertery niestandardowe na potrzeby serializacji JSON</span><span class="sxs-lookup"><span data-stu-id="81948-144">Write custom converters for JSON serialization</span></span>](system-text-json-converters-how-to.md)
* [<span data-ttu-id="81948-145">Obsługa wartości DateTime i DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="81948-145">DateTime and DateTimeOffset support</span></span>](../datetime/system-text-json-support.md)
* <span data-ttu-id="81948-146">[System.Text.Json Dokumentacja interfejsu API](xref:System.Text.Json)</span><span class="sxs-lookup"><span data-stu-id="81948-146">[System.Text.Json API reference](xref:System.Text.Json)</span></span>
* <span data-ttu-id="81948-147">[System.Text.Json. Dokumentacja interfejsu API serializacji](xref:System.Text.Json.Serialization)</span><span class="sxs-lookup"><span data-stu-id="81948-147">[System.Text.Json.Serialization API reference](xref:System.Text.Json.Serialization)</span></span>
