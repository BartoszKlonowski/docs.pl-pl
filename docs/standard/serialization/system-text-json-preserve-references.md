---
title: Jak zachować odwołania za pomocą System.Text.Json
description: Dowiedz się, jak zachować odwołania i obsłużyć odwołania cykliczne podczas serializacji do i deserializacji z JSON w programie .NET.
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
ms.openlocfilehash: 9254ca261c7d748c04c311fa56359014f752ff31
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96439970"
---
# <a name="how-to-handle-circular-references-with-no-locsystemtextjson"></a><span data-ttu-id="59b02-103">Jak obsłużyć odwołania cykliczne z System.Text.Json</span><span class="sxs-lookup"><span data-stu-id="59b02-103">How to handle circular references with System.Text.Json</span></span>

<span data-ttu-id="59b02-104">W tym artykule dowiesz się, jak obsługiwać odwołania cykliczne z `System.Text.Json` przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="59b02-104">In this article, you will learn how to handle circular references with the `System.Text.Json` namespace.</span></span>

## <a name="preserve-references-and-handle-circular-references"></a><span data-ttu-id="59b02-105">Zachowaj odwołania i dojścia cykliczne odwołania</span><span class="sxs-lookup"><span data-stu-id="59b02-105">Preserve references and handle circular references</span></span>

::: zone pivot="dotnet-5-0"

<span data-ttu-id="59b02-106">Aby zachować odwołania i obsłużyć odwołania cykliczne, ustaw wartość <xref:System.Text.Json.JsonSerializerOptions.ReferenceHandler%2A> <xref:System.Text.Json.Serialization.ReferenceHandler.Preserve%2A> .</span><span class="sxs-lookup"><span data-stu-id="59b02-106">To preserve references and handle circular references, set <xref:System.Text.Json.JsonSerializerOptions.ReferenceHandler%2A> to <xref:System.Text.Json.Serialization.ReferenceHandler.Preserve%2A>.</span></span> <span data-ttu-id="59b02-107">To ustawienie powoduje następujące zachowanie:</span><span class="sxs-lookup"><span data-stu-id="59b02-107">This setting causes the following behavior:</span></span>

* <span data-ttu-id="59b02-108">Podczas serializacji:</span><span class="sxs-lookup"><span data-stu-id="59b02-108">On serialize:</span></span>

  <span data-ttu-id="59b02-109">Podczas pisania typów złożonych, serializator również zapisuje właściwości metadanych ( `$id` , `$values` i `$ref` ).</span><span class="sxs-lookup"><span data-stu-id="59b02-109">When writing complex types, the serializer also writes metadata properties (`$id`, `$values`, and `$ref`).</span></span>

* <span data-ttu-id="59b02-110">Przy deserializacji:</span><span class="sxs-lookup"><span data-stu-id="59b02-110">On deserialize:</span></span>

  <span data-ttu-id="59b02-111">Oczekiwana jest wartość metadanych (choć nie jest obowiązkowa), a Deserializator próbuje zrozumieć ten element.</span><span class="sxs-lookup"><span data-stu-id="59b02-111">Metadata is expected (although not mandatory), and the deserializer tries to understand it.</span></span>

<span data-ttu-id="59b02-112">Poniższy kod ilustruje użycie tego `Preserve` Ustawienia.</span><span class="sxs-lookup"><span data-stu-id="59b02-112">The following code illustrates use of the `Preserve` setting.</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/PreserveReferences.cs" highlight="34":::

<span data-ttu-id="59b02-113">Tej funkcji nie można używać do zachowywania typów wartości lub niezmiennych typów.</span><span class="sxs-lookup"><span data-stu-id="59b02-113">This feature can't be used to preserve value types or immutable types.</span></span> <span data-ttu-id="59b02-114">Podczas deserializacji wystąpienie niezmiennego typu jest tworzone po odczytaniu całego ładunku.</span><span class="sxs-lookup"><span data-stu-id="59b02-114">On deserialization, the instance of an immutable type is created after the entire payload is read.</span></span> <span data-ttu-id="59b02-115">W związku z tym może być niemożliwe deserializacja tego samego wystąpienia, jeśli odwołanie do niego pojawia się w ramach ładunku JSON.</span><span class="sxs-lookup"><span data-stu-id="59b02-115">So it would be impossible to deserialize the same instance if a reference to it appears within the JSON payload.</span></span>

<span data-ttu-id="59b02-116">W przypadku typów wartości, niemodyfikowalnych typów i tablic nie są serializowane żadne metadane odwołania.</span><span class="sxs-lookup"><span data-stu-id="59b02-116">For value types, immutable types, and arrays, no reference metadata is serialized.</span></span> <span data-ttu-id="59b02-117">Podczas deserializacji wyjątek jest zgłaszany, jeśli `$ref` lub `$id` zostanie znaleziony.</span><span class="sxs-lookup"><span data-stu-id="59b02-117">On deserialization, an exception is thrown if `$ref` or `$id` is found.</span></span> <span data-ttu-id="59b02-118">Jednak typy wartości ignorują `$id` (i `$values` w przypadku kolekcji), aby umożliwić deserializacji ładunków, które zostały zserializowane przy użyciu Newtonsoft.Json .</span><span class="sxs-lookup"><span data-stu-id="59b02-118">However, value types ignore `$id` (and `$values` in the case of collections) to make it possible to deserialize payloads that were serialized by using Newtonsoft.Json.</span></span>  <span data-ttu-id="59b02-119">Newtonsoft.Json wykonuje serializacji metadanych dla takich typów.</span><span class="sxs-lookup"><span data-stu-id="59b02-119">Newtonsoft.Json does serialize metadata for such types.</span></span>

<span data-ttu-id="59b02-120">Aby określić, czy obiekty są równe, System.Text.Json używa <xref:System.Collections.Generic.ReferenceEqualityComparer.Instance%2A?displayProperty=nameWithType> , który używa równości odwołań ( <xref:System.Object.ReferenceEquals(System.Object,System.Object)?displayProperty=nameWithType> ) zamiast równości wartości ( <xref:System.Object.Equals(System.Object)?displayProperty=nameWithType> podczas porównywania dwóch wystąpień obiektów.</span><span class="sxs-lookup"><span data-stu-id="59b02-120">To determine if objects are equal, System.Text.Json uses <xref:System.Collections.Generic.ReferenceEqualityComparer.Instance%2A?displayProperty=nameWithType>, which uses reference equality (<xref:System.Object.ReferenceEquals(System.Object,System.Object)?displayProperty=nameWithType>) instead of value equality (<xref:System.Object.Equals(System.Object)?displayProperty=nameWithType> when comparing two object instances.</span></span>

<span data-ttu-id="59b02-121">Aby uzyskać więcej informacji o tym, jak odwołania są serializowane i deserializowane, zobacz <xref:System.Text.Json.Serialization.ReferenceHandler.Preserve%2A?displayProperty=nameWithType> .</span><span class="sxs-lookup"><span data-stu-id="59b02-121">For more information about how references are serialized and deserialized, see <xref:System.Text.Json.Serialization.ReferenceHandler.Preserve%2A?displayProperty=nameWithType>.</span></span>

<span data-ttu-id="59b02-122"><xref:System.Text.Json.Serialization.ReferenceResolver>Klasa definiuje zachowanie zachowywania odwołań podczas serializacji i deserializacji.</span><span class="sxs-lookup"><span data-stu-id="59b02-122">The <xref:System.Text.Json.Serialization.ReferenceResolver> class defines the behavior of preserving references on serialization and deserialization.</span></span> <span data-ttu-id="59b02-123">Utwórz klasę pochodną, aby określić zachowanie niestandardowe.</span><span class="sxs-lookup"><span data-stu-id="59b02-123">Create a derived class to specify custom behavior.</span></span> <span data-ttu-id="59b02-124">Aby zapoznać się z przykładem, zobacz [GuidReferenceResolver](https://github.com/dotnet/docs/blob/9d5e88edbd7f12be463775ffebbf07ac8415fe18/docs/standard/serialization/snippets/system-text-json-how-to-5-0/csharp/GuidReferenceResolverExample.cs).</span><span class="sxs-lookup"><span data-stu-id="59b02-124">For an example, see [GuidReferenceResolver](https://github.com/dotnet/docs/blob/9d5e88edbd7f12be463775ffebbf07ac8415fe18/docs/standard/serialization/snippets/system-text-json-how-to-5-0/csharp/GuidReferenceResolverExample.cs).</span></span>

::: zone-end

::: zone pivot="dotnet-core-3-1"
<span data-ttu-id="59b02-125">System.Text.Json w programie .NET Core 3,1 obsługuje Serializacja przez wartość i zgłasza wyjątek dla odwołań cyklicznych.</span><span class="sxs-lookup"><span data-stu-id="59b02-125">System.Text.Json in .NET Core 3.1 only supports serialization by value and throws an exception for circular references.</span></span>
::: zone-end

## <a name="see-also"></a><span data-ttu-id="59b02-126">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="59b02-126">See also</span></span>

* [<span data-ttu-id="59b02-127">System.Text.Json Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="59b02-127">System.Text.Json overview</span></span>](system-text-json-overview.md)
* [<span data-ttu-id="59b02-128">Tworzenie wystąpienia JsonSerializerOptions</span><span class="sxs-lookup"><span data-stu-id="59b02-128">Instantiate JsonSerializerOptions</span></span>](system-text-json-configure-options.md)
* [<span data-ttu-id="59b02-129">Włącz dopasowywanie bez uwzględniania wielkości liter</span><span class="sxs-lookup"><span data-stu-id="59b02-129">Enable case-insensitive matching</span></span>](system-text-json-character-casing.md)
* [<span data-ttu-id="59b02-130">Dostosowywanie nazw i wartości właściwości</span><span class="sxs-lookup"><span data-stu-id="59b02-130">Customize property names and values</span></span>](system-text-json-customize-properties.md)
* [<span data-ttu-id="59b02-131">Ignoruj właściwości</span><span class="sxs-lookup"><span data-stu-id="59b02-131">Ignore properties</span></span>](system-text-json-ignore-properties.md)
* [<span data-ttu-id="59b02-132">Zezwalaj na nieprawidłowy kod JSON</span><span class="sxs-lookup"><span data-stu-id="59b02-132">Allow invalid JSON</span></span>](system-text-json-invalid-json.md)
* [<span data-ttu-id="59b02-133">Obsługa przepełnienia kodu JSON</span><span class="sxs-lookup"><span data-stu-id="59b02-133">Handle overflow JSON</span></span>](system-text-json-handle-overflow.md)
* [<span data-ttu-id="59b02-134">Niemodyfikowalne typy i niepubliczne metody dostępu</span><span class="sxs-lookup"><span data-stu-id="59b02-134">Immutable types and non-public accessors</span></span>](system-text-json-immutability.md)
* [<span data-ttu-id="59b02-135">Serializacja polimorficzna</span><span class="sxs-lookup"><span data-stu-id="59b02-135">Polymorphic serialization</span></span>](system-text-json-polymorphism.md)
* <span data-ttu-id="59b02-136">[System.Text.Json Dokumentacja interfejsu API](xref:System.Text.Json)</span><span class="sxs-lookup"><span data-stu-id="59b02-136">[System.Text.Json API reference](xref:System.Text.Json)</span></span>
