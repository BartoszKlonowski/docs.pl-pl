---
title: Jak zachować odwołania za pomocą System.Text.Json
description: Dowiedz się, jak zachować odwołania i obsłużyć odwołania cykliczne podczas serializacji do i deserializacji z JSON w programie .NET.
ms.date: 12/09/2020
no-loc:
- System.Text.Json
- Newtonsoft.Json
zone_pivot_groups: dotnet-version
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
ms.openlocfilehash: d358c953c0979ca097c080fcd750d5ef95b07de0
ms.sourcegitcommit: 81f1bba2c97a67b5ca76bcc57b37333ffca60c7b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/10/2020
ms.locfileid: "97008737"
---
# <a name="how-to-preserve-references-and-handle-circular-references-with-no-locsystemtextjson"></a><span data-ttu-id="b4b28-103">Jak zachować odwołania i obsłużyć odwołania cykliczne z System.Text.Json</span><span class="sxs-lookup"><span data-stu-id="b4b28-103">How to preserve references and handle circular references with System.Text.Json</span></span>

::: zone pivot="dotnet-5-0"

<span data-ttu-id="b4b28-104">Aby zachować odwołania i obsłużyć odwołania cykliczne, ustaw wartość <xref:System.Text.Json.JsonSerializerOptions.ReferenceHandler%2A> <xref:System.Text.Json.Serialization.ReferenceHandler.Preserve%2A> .</span><span class="sxs-lookup"><span data-stu-id="b4b28-104">To preserve references and handle circular references, set <xref:System.Text.Json.JsonSerializerOptions.ReferenceHandler%2A> to <xref:System.Text.Json.Serialization.ReferenceHandler.Preserve%2A>.</span></span> <span data-ttu-id="b4b28-105">To ustawienie powoduje następujące zachowanie:</span><span class="sxs-lookup"><span data-stu-id="b4b28-105">This setting causes the following behavior:</span></span>

* <span data-ttu-id="b4b28-106">Podczas serializacji:</span><span class="sxs-lookup"><span data-stu-id="b4b28-106">On serialize:</span></span>

  <span data-ttu-id="b4b28-107">Podczas pisania typów złożonych, serializator również zapisuje właściwości metadanych ( `$id` , `$values` i `$ref` ).</span><span class="sxs-lookup"><span data-stu-id="b4b28-107">When writing complex types, the serializer also writes metadata properties (`$id`, `$values`, and `$ref`).</span></span>

* <span data-ttu-id="b4b28-108">Przy deserializacji:</span><span class="sxs-lookup"><span data-stu-id="b4b28-108">On deserialize:</span></span>

  <span data-ttu-id="b4b28-109">Oczekiwana jest wartość metadanych (choć nie jest obowiązkowa), a Deserializator próbuje zrozumieć ten element.</span><span class="sxs-lookup"><span data-stu-id="b4b28-109">Metadata is expected (although not mandatory), and the deserializer tries to understand it.</span></span>

<span data-ttu-id="b4b28-110">Poniższy kod ilustruje użycie tego `Preserve` Ustawienia.</span><span class="sxs-lookup"><span data-stu-id="b4b28-110">The following code illustrates use of the `Preserve` setting.</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/PreserveReferences.cs" highlight="34":::

<span data-ttu-id="b4b28-111">Tej funkcji nie można używać do zachowywania typów wartości lub niezmiennych typów.</span><span class="sxs-lookup"><span data-stu-id="b4b28-111">This feature can't be used to preserve value types or immutable types.</span></span> <span data-ttu-id="b4b28-112">Podczas deserializacji wystąpienie niezmiennego typu jest tworzone po odczytaniu całego ładunku.</span><span class="sxs-lookup"><span data-stu-id="b4b28-112">On deserialization, the instance of an immutable type is created after the entire payload is read.</span></span> <span data-ttu-id="b4b28-113">W związku z tym może być niemożliwe deserializacja tego samego wystąpienia, jeśli odwołanie do niego pojawia się w ramach ładunku JSON.</span><span class="sxs-lookup"><span data-stu-id="b4b28-113">So it would be impossible to deserialize the same instance if a reference to it appears within the JSON payload.</span></span>

<span data-ttu-id="b4b28-114">W przypadku typów wartości, niemodyfikowalnych typów i tablic nie są serializowane żadne metadane odwołania.</span><span class="sxs-lookup"><span data-stu-id="b4b28-114">For value types, immutable types, and arrays, no reference metadata is serialized.</span></span> <span data-ttu-id="b4b28-115">Podczas deserializacji wyjątek jest zgłaszany, jeśli `$ref` lub `$id` zostanie znaleziony.</span><span class="sxs-lookup"><span data-stu-id="b4b28-115">On deserialization, an exception is thrown if `$ref` or `$id` is found.</span></span> <span data-ttu-id="b4b28-116">Jednak typy wartości ignorują `$id` (i `$values` w przypadku kolekcji), aby umożliwić deserializacji ładunków, które zostały zserializowane przy użyciu Newtonsoft.Json .</span><span class="sxs-lookup"><span data-stu-id="b4b28-116">However, value types ignore `$id` (and `$values` in the case of collections) to make it possible to deserialize payloads that were serialized by using Newtonsoft.Json.</span></span>  <span data-ttu-id="b4b28-117">Newtonsoft.Json wykonuje serializacji metadanych dla takich typów.</span><span class="sxs-lookup"><span data-stu-id="b4b28-117">Newtonsoft.Json does serialize metadata for such types.</span></span>

<span data-ttu-id="b4b28-118">Aby określić, czy obiekty są równe, System.Text.Json używa <xref:System.Collections.Generic.ReferenceEqualityComparer.Instance%2A?displayProperty=nameWithType> , który używa równości odwołań ( <xref:System.Object.ReferenceEquals(System.Object,System.Object)?displayProperty=nameWithType> ) zamiast równości wartości ( <xref:System.Object.Equals(System.Object)?displayProperty=nameWithType> podczas porównywania dwóch wystąpień obiektów.</span><span class="sxs-lookup"><span data-stu-id="b4b28-118">To determine if objects are equal, System.Text.Json uses <xref:System.Collections.Generic.ReferenceEqualityComparer.Instance%2A?displayProperty=nameWithType>, which uses reference equality (<xref:System.Object.ReferenceEquals(System.Object,System.Object)?displayProperty=nameWithType>) instead of value equality (<xref:System.Object.Equals(System.Object)?displayProperty=nameWithType> when comparing two object instances.</span></span>

<span data-ttu-id="b4b28-119">Aby uzyskać więcej informacji o tym, jak odwołania są serializowane i deserializowane, zobacz <xref:System.Text.Json.Serialization.ReferenceHandler.Preserve%2A?displayProperty=nameWithType> .</span><span class="sxs-lookup"><span data-stu-id="b4b28-119">For more information about how references are serialized and deserialized, see <xref:System.Text.Json.Serialization.ReferenceHandler.Preserve%2A?displayProperty=nameWithType>.</span></span>

<span data-ttu-id="b4b28-120"><xref:System.Text.Json.Serialization.ReferenceResolver>Klasa definiuje zachowanie zachowywania odwołań podczas serializacji i deserializacji.</span><span class="sxs-lookup"><span data-stu-id="b4b28-120">The <xref:System.Text.Json.Serialization.ReferenceResolver> class defines the behavior of preserving references on serialization and deserialization.</span></span> <span data-ttu-id="b4b28-121">Utwórz klasę pochodną, aby określić zachowanie niestandardowe.</span><span class="sxs-lookup"><span data-stu-id="b4b28-121">Create a derived class to specify custom behavior.</span></span> <span data-ttu-id="b4b28-122">Aby zapoznać się z przykładem, zobacz [GuidReferenceResolver](https://github.com/dotnet/docs/blob/9d5e88edbd7f12be463775ffebbf07ac8415fe18/docs/standard/serialization/snippets/system-text-json-how-to-5-0/csharp/GuidReferenceResolverExample.cs).</span><span class="sxs-lookup"><span data-stu-id="b4b28-122">For an example, see [GuidReferenceResolver](https://github.com/dotnet/docs/blob/9d5e88edbd7f12be463775ffebbf07ac8415fe18/docs/standard/serialization/snippets/system-text-json-how-to-5-0/csharp/GuidReferenceResolverExample.cs).</span></span>

::: zone-end

::: zone pivot="dotnet-core-3-1"
<span data-ttu-id="b4b28-123">System.Text.Json w programie .NET Core 3,1 obsługuje Serializacja przez wartość i zgłasza wyjątek dla odwołań cyklicznych.</span><span class="sxs-lookup"><span data-stu-id="b4b28-123">System.Text.Json in .NET Core 3.1 only supports serialization by value and throws an exception for circular references.</span></span>
::: zone-end

## <a name="see-also"></a><span data-ttu-id="b4b28-124">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="b4b28-124">See also</span></span>

* [<span data-ttu-id="b4b28-125">System.Text.Json Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="b4b28-125">System.Text.Json overview</span></span>](system-text-json-overview.md)
* [<span data-ttu-id="b4b28-126">Jak serializować i deserializować dane JSON</span><span class="sxs-lookup"><span data-stu-id="b4b28-126">How to serialize and deserialize JSON</span></span>](system-text-json-how-to.md)
* [<span data-ttu-id="b4b28-127">Tworzenie wystąpienia JsonSerializerOptions wystąpień</span><span class="sxs-lookup"><span data-stu-id="b4b28-127">Instantiate JsonSerializerOptions instances</span></span>](system-text-json-configure-options.md)
* [<span data-ttu-id="b4b28-128">Włączanie dopasowywania bez uwzględniania wielkości liter</span><span class="sxs-lookup"><span data-stu-id="b4b28-128">Enable case-insensitive matching</span></span>](system-text-json-character-casing.md)
* [<span data-ttu-id="b4b28-129">Dostosowywanie nazw i wartości właściwości</span><span class="sxs-lookup"><span data-stu-id="b4b28-129">Customize property names and values</span></span>](system-text-json-customize-properties.md)
* [<span data-ttu-id="b4b28-130">Ignorowanie właściwości</span><span class="sxs-lookup"><span data-stu-id="b4b28-130">Ignore properties</span></span>](system-text-json-ignore-properties.md)
* [<span data-ttu-id="b4b28-131">Zezwalanie na nieprawidłowy kod JSON</span><span class="sxs-lookup"><span data-stu-id="b4b28-131">Allow invalid JSON</span></span>](system-text-json-invalid-json.md)
* [<span data-ttu-id="b4b28-132">Obsługa przepełnienia kodu JSON</span><span class="sxs-lookup"><span data-stu-id="b4b28-132">Handle overflow JSON</span></span>](system-text-json-handle-overflow.md)
* [<span data-ttu-id="b4b28-133">Niemodyfikowalne typy i niepubliczne metody dostępu</span><span class="sxs-lookup"><span data-stu-id="b4b28-133">Immutable types and non-public accessors</span></span>](system-text-json-immutability.md)
* [<span data-ttu-id="b4b28-134">Serializacja polimorficzna</span><span class="sxs-lookup"><span data-stu-id="b4b28-134">Polymorphic serialization</span></span>](system-text-json-polymorphism.md)
* [<span data-ttu-id="b4b28-135">Migruj z Newtonsoft.Json do System.Text.Json</span><span class="sxs-lookup"><span data-stu-id="b4b28-135">Migrate from Newtonsoft.Json to System.Text.Json</span></span>](system-text-json-migrate-from-newtonsoft-how-to.md)
* [<span data-ttu-id="b4b28-136">Dostosowywanie kodowania znaków</span><span class="sxs-lookup"><span data-stu-id="b4b28-136">Customize character encoding</span></span>](system-text-json-character-encoding.md)
* [<span data-ttu-id="b4b28-137">Napisz niestandardowe serializatory i deserializatory</span><span class="sxs-lookup"><span data-stu-id="b4b28-137">Write custom serializers and deserializers</span></span>](write-custom-serializer-deserializer.md)
* [<span data-ttu-id="b4b28-138">Zapisz konwertery niestandardowe na potrzeby serializacji JSON</span><span class="sxs-lookup"><span data-stu-id="b4b28-138">Write custom converters for JSON serialization</span></span>](system-text-json-converters-how-to.md)
* [<span data-ttu-id="b4b28-139">Obsługa wartości DateTime i DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="b4b28-139">DateTime and DateTimeOffset support</span></span>](../datetime/system-text-json-support.md)
* <span data-ttu-id="b4b28-140">[System.Text.Json Dokumentacja interfejsu API](xref:System.Text.Json)</span><span class="sxs-lookup"><span data-stu-id="b4b28-140">[System.Text.Json API reference](xref:System.Text.Json)</span></span>
* <span data-ttu-id="b4b28-141">[System.Text.Json. Dokumentacja interfejsu API serializacji](xref:System.Text.Json.Serialization)</span><span class="sxs-lookup"><span data-stu-id="b4b28-141">[System.Text.Json.Serialization API reference](xref:System.Text.Json.Serialization)</span></span>
