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
ms.openlocfilehash: 257c99e117dea9a9b3ab2352c9a442d71a2cdabd
ms.sourcegitcommit: 0014aa4d5cb2da56a70e03fc68f663d64df5247a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/09/2020
ms.locfileid: "96918557"
---
# <a name="how-to-instantiate-jsonserializeroptions-instances-with-no-locsystemtextjson"></a><span data-ttu-id="b7492-103">Jak utworzyć wystąpienie JsonSerializerOptions wystąpień z System.Text.Json</span><span class="sxs-lookup"><span data-stu-id="b7492-103">How to instantiate JsonSerializerOptions instances with System.Text.Json</span></span>

<span data-ttu-id="b7492-104">W tym artykule wyjaśniono, jak uniknąć problemów z wydajnością podczas korzystania z programu <xref:System.Text.Json.JsonSerializerOptions> .</span><span class="sxs-lookup"><span data-stu-id="b7492-104">This article explains how to avoid performance problems when you use <xref:System.Text.Json.JsonSerializerOptions>.</span></span> <span data-ttu-id="b7492-105">Pokazano również, jak używać konstruktorów sparametryzowanych, które są dostępne.</span><span class="sxs-lookup"><span data-stu-id="b7492-105">It also shows how to use the parameterized constructors that are available.</span></span>

## <a name="reuse-jsonserializeroptions-instances"></a><span data-ttu-id="b7492-106">Ponowne użycie wystąpień JsonSerializerOptions</span><span class="sxs-lookup"><span data-stu-id="b7492-106">Reuse JsonSerializerOptions instances</span></span>

<span data-ttu-id="b7492-107">Jeśli używasz `JsonSerializerOptions` wielokrotnie z tymi samymi opcjami, nie twórz nowego `JsonSerializerOptions` wystąpienia za każdym razem, gdy go używasz.</span><span class="sxs-lookup"><span data-stu-id="b7492-107">If you use `JsonSerializerOptions` repeatedly with the same options, don't create a new `JsonSerializerOptions` instance each time you use it.</span></span> <span data-ttu-id="b7492-108">Ponownie Użyj tego samego wystąpienia dla każdego wywołania.</span><span class="sxs-lookup"><span data-stu-id="b7492-108">Reuse the same instance for every call.</span></span> <span data-ttu-id="b7492-109">Te wskazówki odnoszą się do kodu zapisanego w przypadku konwerterów niestandardowych i podczas wywoływania <xref:System.Text.Json.JsonSerializer.Serialize%2A?displayProperty=nameWithType> lub <xref:System.Text.Json.JsonSerializer.Deserialize%2A?displayProperty=nameWithType> .</span><span class="sxs-lookup"><span data-stu-id="b7492-109">This guidance applies to code you write for custom converters and when you call <xref:System.Text.Json.JsonSerializer.Serialize%2A?displayProperty=nameWithType> or <xref:System.Text.Json.JsonSerializer.Deserialize%2A?displayProperty=nameWithType>.</span></span>

<span data-ttu-id="b7492-110">Poniższy kod ilustruje spadek wydajności przy użyciu nowych wystąpień opcji.</span><span class="sxs-lookup"><span data-stu-id="b7492-110">The following code demonstrates the performance penalty for using new options instances.</span></span>

:::code language="csharp" source="snippets/system-text-json-configure-options/csharp/ReuseOptionsInstances.cs":::

<span data-ttu-id="b7492-111">Poprzedni kod serializować mały obiekt 100 000 razy przy użyciu tego samego wystąpienia opcji.</span><span class="sxs-lookup"><span data-stu-id="b7492-111">The preceding code serializes a small object 100,000 times using the same options instance.</span></span> <span data-ttu-id="b7492-112">Następnie deserializacji ten sam obiekt o tej samej liczbie razy i tworzy nowe wystąpienie opcji za każdym razem.</span><span class="sxs-lookup"><span data-stu-id="b7492-112">Then it serializes the same object the same number of times and creates a new options instance each time.</span></span> <span data-ttu-id="b7492-113">Typowa różnica czasu wykonywania jest 190 w porównaniu do 40 140 milisekund.</span><span class="sxs-lookup"><span data-stu-id="b7492-113">A typical run time difference is 190 compared to 40,140 milliseconds.</span></span> <span data-ttu-id="b7492-114">Różnica jest jeszcze większa w przypadku zwiększenia liczby iteracji.</span><span class="sxs-lookup"><span data-stu-id="b7492-114">The difference is even greater if you increase the number of iterations.</span></span>

<span data-ttu-id="b7492-115">Serializator przeprowadzi fazę rozgrzewania podczas pierwszej serializacji każdego typu na grafie obiektów, gdy do niego zostanie przesłane nowe wystąpienie opcji.</span><span class="sxs-lookup"><span data-stu-id="b7492-115">The serializer undergoes a warm-up phase during the first serialization of each type in the object graph when a new options instance is passed to it.</span></span> <span data-ttu-id="b7492-116">Ta rozgrzewanie obejmuje tworzenie pamięci podręcznej metadanych, która jest wymagana do serializacji.</span><span class="sxs-lookup"><span data-stu-id="b7492-116">This warm-up includes creating a cache of metadata that is needed for serialization.</span></span> <span data-ttu-id="b7492-117">Metadane obejmują delegatów do metod pobierających właściwości, Setters, argumentów konstruktora, określonych atrybutów i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="b7492-117">The metadata includes delegates to property getters, setters, constructor arguments, specified attributes, and so forth.</span></span> <span data-ttu-id="b7492-118">Ta pamięć podręczna metadanych jest przechowywana w wystąpieniu opcji.</span><span class="sxs-lookup"><span data-stu-id="b7492-118">This metadata cache is stored in the options instance.</span></span> <span data-ttu-id="b7492-119">Ten sam proces rozgrzewania i pamięć podręczna stosuje się do deserializacji.</span><span class="sxs-lookup"><span data-stu-id="b7492-119">The same warm-up process and cache applies to deserialization.</span></span>

<span data-ttu-id="b7492-120">Rozmiar pamięci podręcznej metadanych w `JsonSerializerOptions` wystąpieniu zależy od liczby typów do serializacji.</span><span class="sxs-lookup"><span data-stu-id="b7492-120">The size of the metadata cache in a `JsonSerializerOptions` instance depends on the number of types to be serialized.</span></span> <span data-ttu-id="b7492-121">W przypadku przekazania wielu typów — na przykład dynamicznie generowanych typów — do serializatora rozmiar pamięci podręcznej będzie nadal wzrastał i może zakończyć działanie `OutOfMemoryException` .</span><span class="sxs-lookup"><span data-stu-id="b7492-121">If you pass numerous types—for example, dynamically generated types—to the serializer, the cache size will continue to grow and can end up causing an `OutOfMemoryException`.</span></span>

## <a name="copy-jsonserializeroptions"></a><span data-ttu-id="b7492-122">Kopiuj JsonSerializerOptions</span><span class="sxs-lookup"><span data-stu-id="b7492-122">Copy JsonSerializerOptions</span></span>

::: zone pivot="dotnet-5-0"
<span data-ttu-id="b7492-123">Istnieje Konstruktor [JsonSerializerOptions] (linki XREF: System.Text.Json . JsonSerializerOptions .% 23ctor ( System.Text.Json . JsonSerializerOptions)), która umożliwia utworzenie nowego wystąpienia z takimi samymi opcjami jak istniejące wystąpienie, jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="b7492-123">There is a [JsonSerializerOptions constructor](xref:System.Text.Json.JsonSerializerOptions.%23ctor(System.Text.Json.JsonSerializerOptions)) that lets you create a new instance with the same options as an existing instance, as shown in the following example:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/CopyOptions.cs" highlight="29":::
::: zone-end

::: zone pivot="dotnet-core-3-1"
<span data-ttu-id="b7492-124">`JsonSerializerOptions`Konstruktor, który pobiera istniejące wystąpienie, nie jest dostępny w programie .NET Core 3,1.</span><span class="sxs-lookup"><span data-stu-id="b7492-124">A `JsonSerializerOptions` constructor that takes an existing instance is not available in .NET Core 3.1.</span></span>
::: zone-end

## <a name="web-defaults-for-jsonserializeroptions"></a><span data-ttu-id="b7492-125">Ustawienia domyślne sieci Web dla JsonSerializerOptions</span><span class="sxs-lookup"><span data-stu-id="b7492-125">Web defaults for JsonSerializerOptions</span></span>

::: zone pivot="dotnet-5-0"
<span data-ttu-id="b7492-126">Poniżej przedstawiono opcje, które mają różne wartości domyślne dla usługi Web Apps:</span><span class="sxs-lookup"><span data-stu-id="b7492-126">Here are the options that have different defaults for web apps:</span></span>

* <xref:System.Text.Json.JsonSerializerOptions.PropertyNameCaseInsensitive%2A> = `true`
* <xref:System.Text.Json.JsonNamingPolicy> = <xref:System.Text.Json.JsonNamingPolicy.CamelCase>
* <xref:System.Text.Json.JsonSerializerOptions.NumberHandling%2A> = <xref:System.Text.Json.Serialization.JsonNumberHandling.AllowReadingFromString>

<span data-ttu-id="b7492-127">Istnieje Konstruktor [JsonSerializerOptions] (linki XREF: System.Text.Json . JsonSerializerOptions .% 23ctor ( System.Text.Json . JsonSerializerDefaults)? View = NET-5,0&Preserve-View = true), która umożliwia utworzenie nowego wystąpienia z opcjami domyślnymi, które ASP.NET Core używane przez aplikacje sieci Web, jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="b7492-127">There's a [JsonSerializerOptions constructor](xref:System.Text.Json.JsonSerializerOptions.%23ctor(System.Text.Json.JsonSerializerDefaults)?view=net-5.0&preserve-view=true) that lets you create a new instance with the default options that ASP.NET Core uses for web apps, as shown in the following example:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/OptionsDefaults.cs" highlight="24":::
::: zone-end

::: zone pivot="dotnet-core-3-1"
<span data-ttu-id="b7492-128">Poniżej przedstawiono opcje, które mają różne wartości domyślne dla usługi Web Apps:</span><span class="sxs-lookup"><span data-stu-id="b7492-128">Here are the options that have different defaults for web apps:</span></span>

* <xref:System.Text.Json.JsonSerializerOptions.PropertyNameCaseInsensitive%2A> = `true`
* <xref:System.Text.Json.JsonNamingPolicy> = <xref:System.Text.Json.JsonNamingPolicy.CamelCase>

<span data-ttu-id="b7492-129">`JsonSerializerOptions`Konstruktor, który określa zestaw ustawień domyślnych, nie jest dostępny w programie .NET Core 3,1.</span><span class="sxs-lookup"><span data-stu-id="b7492-129">A `JsonSerializerOptions` constructor that specifies a set of defaults is not available in .NET Core 3.1.</span></span>
::: zone-end

## <a name="see-also"></a><span data-ttu-id="b7492-130">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="b7492-130">See also</span></span>

* [<span data-ttu-id="b7492-131">System.Text.Json Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="b7492-131">System.Text.Json overview</span></span>](system-text-json-overview.md)
* [<span data-ttu-id="b7492-132">Włączanie dopasowywania bez uwzględniania wielkości liter</span><span class="sxs-lookup"><span data-stu-id="b7492-132">Enable case-insensitive matching</span></span>](system-text-json-character-casing.md)
* [<span data-ttu-id="b7492-133">Dostosowywanie nazw i wartości właściwości</span><span class="sxs-lookup"><span data-stu-id="b7492-133">Customize property names and values</span></span>](system-text-json-customize-properties.md)
* [<span data-ttu-id="b7492-134">Ignorowanie właściwości</span><span class="sxs-lookup"><span data-stu-id="b7492-134">Ignore properties</span></span>](system-text-json-ignore-properties.md)
* [<span data-ttu-id="b7492-135">Zezwalanie na nieprawidłowy kod JSON</span><span class="sxs-lookup"><span data-stu-id="b7492-135">Allow invalid JSON</span></span>](system-text-json-invalid-json.md)
* [<span data-ttu-id="b7492-136">Obsługa przepełnienia kodu JSON</span><span class="sxs-lookup"><span data-stu-id="b7492-136">Handle overflow JSON</span></span>](system-text-json-handle-overflow.md)
* [<span data-ttu-id="b7492-137">Zachowaj odwołania cykliczne</span><span class="sxs-lookup"><span data-stu-id="b7492-137">Preserve circular references</span></span>](system-text-json-preserve-references.md)
* [<span data-ttu-id="b7492-138">Niemodyfikowalne typy i niepubliczne metody dostępu</span><span class="sxs-lookup"><span data-stu-id="b7492-138">Immutable types and non-public accessors</span></span>](system-text-json-immutability.md)
* [<span data-ttu-id="b7492-139">Serializacja polimorficzna</span><span class="sxs-lookup"><span data-stu-id="b7492-139">Polymorphic serialization</span></span>](system-text-json-polymorphism.md)
* <span data-ttu-id="b7492-140">[System.Text.Json Dokumentacja interfejsu API](xref:System.Text.Json)</span><span class="sxs-lookup"><span data-stu-id="b7492-140">[System.Text.Json API reference](xref:System.Text.Json)</span></span>
