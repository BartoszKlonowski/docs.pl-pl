---
title: Jak używać niejawnych typów i niepublicznych metod dostępu za pomocą System.Text.Json
description: Dowiedz się, jak korzystać z niemodyfikowalnych typów i niepublicznych metod dostępu podczas serializacji do i deserializacji z formatu JSON w programie .NET.
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
ms.openlocfilehash: ff8ecec0d70c877b7cbbd0297b85f0d9578ab828
ms.sourcegitcommit: 81f1bba2c97a67b5ca76bcc57b37333ffca60c7b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/10/2020
ms.locfileid: "97008828"
---
# <a name="how-to-use-immutable-types-and-non-public-accessors-with-no-locsystemtextjson"></a><span data-ttu-id="9e450-103">Jak używać niejawnych typów i niepublicznych metod dostępu za pomocą System.Text.Json</span><span class="sxs-lookup"><span data-stu-id="9e450-103">How to use immutable types and non-public accessors with System.Text.Json</span></span>

<span data-ttu-id="9e450-104">W tym artykule dowiesz się, jak używać niemodyfikowalnych typów, takich jak rekordy, z `System.Text.Json` przestrzenią nazw.</span><span class="sxs-lookup"><span data-stu-id="9e450-104">In this article, you will learn how to use immutable types, such as Records, with the `System.Text.Json` namespace.</span></span>

## <a name="immutable-types-and-records"></a><span data-ttu-id="9e450-105">Niezmienne typy i rekordy</span><span class="sxs-lookup"><span data-stu-id="9e450-105">Immutable types and Records</span></span>

::: zone pivot="dotnet-5-0"
<span data-ttu-id="9e450-106">`System.Text.Json` można użyć sparametryzowanego konstruktora, który umożliwia deserializacja niezmiennej klasy lub struktury.</span><span class="sxs-lookup"><span data-stu-id="9e450-106">`System.Text.Json` can use a parameterized constructor, which makes it possible to deserialize an immutable class or struct.</span></span> <span data-ttu-id="9e450-107">W przypadku klasy, jeśli jedynym konstruktorem jest sparametryzowane, ten Konstruktor zostanie użyty.</span><span class="sxs-lookup"><span data-stu-id="9e450-107">For a class, if the only constructor is a parameterized one, that constructor will be used.</span></span> <span data-ttu-id="9e450-108">Dla struktury lub klasy z wieloma konstruktorami Określ tę, która ma być używana przez zastosowanie atrybutu [[JsonConstructor]](xref:System.Text.Json.Serialization.JsonConstructorAttribute.%23ctor%2A) .</span><span class="sxs-lookup"><span data-stu-id="9e450-108">For a struct, or a class with multiple constructors, specify the one to use by applying the [[JsonConstructor]](xref:System.Text.Json.Serialization.JsonConstructorAttribute.%23ctor%2A) attribute.</span></span> <span data-ttu-id="9e450-109">Gdy atrybut nie jest używany, w przypadku obecności jest zawsze używany publiczny Konstruktor bez parametrów.</span><span class="sxs-lookup"><span data-stu-id="9e450-109">When the attribute is not used, a public parameterless constructor is always used if present.</span></span> <span data-ttu-id="9e450-110">Atrybutu można używać tylko z konstruktorami publicznymi.</span><span class="sxs-lookup"><span data-stu-id="9e450-110">The attribute can only be used with public constructors.</span></span> <span data-ttu-id="9e450-111">W poniższym przykładzie zastosowano `[JsonConstructor]` atrybut:</span><span class="sxs-lookup"><span data-stu-id="9e450-111">The following example uses the `[JsonConstructor]` attribute:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/ImmutableTypes.cs" highlight="13":::

<span data-ttu-id="9e450-112">Rekordy w języku C# 9 są również obsługiwane, jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="9e450-112">Records in C# 9 are also supported, as shown in the following example:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/Records.cs":::

<span data-ttu-id="9e450-113">W przypadku typów, które są niezmienne, ponieważ wszystkie ich metody ustawiające właściwości są niepubliczne, zapoznaj się z następującą sekcją dotyczącą [metod dostępu do właściwości niepublicznych](#non-public-property-accessors).</span><span class="sxs-lookup"><span data-stu-id="9e450-113">For types that are immutable because all their property setters are non-public, see the following section about [non-public property accessors](#non-public-property-accessors).</span></span>
::: zone-end

::: zone pivot="dotnet-core-3-1"
<span data-ttu-id="9e450-114">`JsonConstructorAttribute` Obsługa rekordów w języku C# 9 nie jest dostępna w programie .NET Core 3,1.</span><span class="sxs-lookup"><span data-stu-id="9e450-114">`JsonConstructorAttribute` and C# 9 Record support aren't available in .NET Core 3.1.</span></span>
::: zone-end

## <a name="non-public-property-accessors"></a><span data-ttu-id="9e450-115">Metody dostępu do właściwości niepublicznych</span><span class="sxs-lookup"><span data-stu-id="9e450-115">Non-public property accessors</span></span>

::: zone pivot="dotnet-5-0"
<span data-ttu-id="9e450-116">Aby włączyć użycie niepublicznego dostępu do właściwości, Użyj atrybutu [[JsonInclude]](xref:System.Text.Json.Serialization.JsonIncludeAttribute) , jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="9e450-116">To enable use of a non-public property accessor, use the [[JsonInclude]](xref:System.Text.Json.Serialization.JsonIncludeAttribute) attribute, as shown in the following example:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/NonPublicAccessors.cs" highlight="12,15":::
::: zone-end

::: zone pivot="dotnet-core-3-1"
<span data-ttu-id="9e450-117">Metody dostępu do właściwości niepublicznych nie są obsługiwane w programie .NET Core 3,1.</span><span class="sxs-lookup"><span data-stu-id="9e450-117">Non-public property accessors are not supported in .NET Core 3.1.</span></span> <span data-ttu-id="9e450-118">Aby uzyskać więcej informacji, zobacz [Migrowanie z Newtonsoft.Json artykułu](system-text-json-migrate-from-newtonsoft-how-to.md#non-public-property-setters-and-getters).</span><span class="sxs-lookup"><span data-stu-id="9e450-118">For more information, see [the Migrate from Newtonsoft.Json article](system-text-json-migrate-from-newtonsoft-how-to.md#non-public-property-setters-and-getters).</span></span>
::: zone-end

## <a name="see-also"></a><span data-ttu-id="9e450-119">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="9e450-119">See also</span></span>

* [<span data-ttu-id="9e450-120">System.Text.Json Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="9e450-120">System.Text.Json overview</span></span>](system-text-json-overview.md)
* [<span data-ttu-id="9e450-121">Jak serializować i deserializować dane JSON</span><span class="sxs-lookup"><span data-stu-id="9e450-121">How to serialize and deserialize JSON</span></span>](system-text-json-how-to.md)
* [<span data-ttu-id="9e450-122">Tworzenie wystąpienia JsonSerializerOptions wystąpień</span><span class="sxs-lookup"><span data-stu-id="9e450-122">Instantiate JsonSerializerOptions instances</span></span>](system-text-json-configure-options.md)
* [<span data-ttu-id="9e450-123">Włączanie dopasowywania bez uwzględniania wielkości liter</span><span class="sxs-lookup"><span data-stu-id="9e450-123">Enable case-insensitive matching</span></span>](system-text-json-character-casing.md)
* [<span data-ttu-id="9e450-124">Dostosowywanie nazw i wartości właściwości</span><span class="sxs-lookup"><span data-stu-id="9e450-124">Customize property names and values</span></span>](system-text-json-customize-properties.md)
* [<span data-ttu-id="9e450-125">Ignorowanie właściwości</span><span class="sxs-lookup"><span data-stu-id="9e450-125">Ignore properties</span></span>](system-text-json-ignore-properties.md)
* [<span data-ttu-id="9e450-126">Zezwalanie na nieprawidłowy kod JSON</span><span class="sxs-lookup"><span data-stu-id="9e450-126">Allow invalid JSON</span></span>](system-text-json-invalid-json.md)
* [<span data-ttu-id="9e450-127">Obsługa przepełnienia kodu JSON</span><span class="sxs-lookup"><span data-stu-id="9e450-127">Handle overflow JSON</span></span>](system-text-json-handle-overflow.md)
* [<span data-ttu-id="9e450-128">Zachowywanie odwołań</span><span class="sxs-lookup"><span data-stu-id="9e450-128">Preserve references</span></span>](system-text-json-preserve-references.md)
* [<span data-ttu-id="9e450-129">Serializacja polimorficzna</span><span class="sxs-lookup"><span data-stu-id="9e450-129">Polymorphic serialization</span></span>](system-text-json-polymorphism.md)
* [<span data-ttu-id="9e450-130">Migruj z Newtonsoft.Json do System.Text.Json</span><span class="sxs-lookup"><span data-stu-id="9e450-130">Migrate from Newtonsoft.Json to System.Text.Json</span></span>](system-text-json-migrate-from-newtonsoft-how-to.md)
* [<span data-ttu-id="9e450-131">Dostosowywanie kodowania znaków</span><span class="sxs-lookup"><span data-stu-id="9e450-131">Customize character encoding</span></span>](system-text-json-character-encoding.md)
* [<span data-ttu-id="9e450-132">Napisz niestandardowe serializatory i deserializatory</span><span class="sxs-lookup"><span data-stu-id="9e450-132">Write custom serializers and deserializers</span></span>](write-custom-serializer-deserializer.md)
* [<span data-ttu-id="9e450-133">Zapisz konwertery niestandardowe na potrzeby serializacji JSON</span><span class="sxs-lookup"><span data-stu-id="9e450-133">Write custom converters for JSON serialization</span></span>](system-text-json-converters-how-to.md)
* [<span data-ttu-id="9e450-134">Obsługa wartości DateTime i DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="9e450-134">DateTime and DateTimeOffset support</span></span>](../datetime/system-text-json-support.md)
* <span data-ttu-id="9e450-135">[System.Text.Json Dokumentacja interfejsu API](xref:System.Text.Json)</span><span class="sxs-lookup"><span data-stu-id="9e450-135">[System.Text.Json API reference](xref:System.Text.Json)</span></span>
* <span data-ttu-id="9e450-136">[System.Text.Json. Dokumentacja interfejsu API serializacji](xref:System.Text.Json.Serialization)</span><span class="sxs-lookup"><span data-stu-id="9e450-136">[System.Text.Json.Serialization API reference](xref:System.Text.Json.Serialization)</span></span>
