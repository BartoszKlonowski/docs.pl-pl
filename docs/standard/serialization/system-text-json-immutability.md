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
ms.openlocfilehash: d3e61d44ce22b7f50838b6d3ba9cf64004bd3725
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96439964"
---
# <a name="how-to-use-immutable-types-and-non-public-accessors-with-no-locsystemtextjson"></a><span data-ttu-id="61ed0-103">Jak używać niejawnych typów i niepublicznych metod dostępu za pomocą System.Text.Json</span><span class="sxs-lookup"><span data-stu-id="61ed0-103">How to use immutable types and non-public accessors with System.Text.Json</span></span>

<span data-ttu-id="61ed0-104">W tym artykule dowiesz się, jak używać niemodyfikowalnych typów, takich jak rekordy, z `System.Text.Json` przestrzenią nazw.</span><span class="sxs-lookup"><span data-stu-id="61ed0-104">In this article, you will learn how to use immutable types, such as Records, with the `System.Text.Json` namespace.</span></span>

## <a name="immutable-types-and-records"></a><span data-ttu-id="61ed0-105">Niezmienne typy i rekordy</span><span class="sxs-lookup"><span data-stu-id="61ed0-105">Immutable types and Records</span></span>

::: zone pivot="dotnet-5-0"
<span data-ttu-id="61ed0-106">`System.Text.Json` można użyć sparametryzowanego konstruktora, który umożliwia deserializacja niezmiennej klasy lub struktury.</span><span class="sxs-lookup"><span data-stu-id="61ed0-106">`System.Text.Json` can use a parameterized constructor, which makes it possible to deserialize an immutable class or struct.</span></span> <span data-ttu-id="61ed0-107">W przypadku klasy, jeśli jedynym konstruktorem jest sparametryzowane, ten Konstruktor zostanie użyty.</span><span class="sxs-lookup"><span data-stu-id="61ed0-107">For a class, if the only constructor is a parameterized one, that constructor will be used.</span></span> <span data-ttu-id="61ed0-108">Dla struktury lub klasy z wieloma konstruktorami Określ tę, która ma być używana przez zastosowanie atrybutu [[JsonConstructor]](xref:System.Text.Json.Serialization.JsonConstructorAttribute.%23ctor%2A) .</span><span class="sxs-lookup"><span data-stu-id="61ed0-108">For a struct, or a class with multiple constructors, specify the one to use by applying the [[JsonConstructor]](xref:System.Text.Json.Serialization.JsonConstructorAttribute.%23ctor%2A) attribute.</span></span> <span data-ttu-id="61ed0-109">Gdy atrybut nie jest używany, w przypadku obecności jest zawsze używany publiczny Konstruktor bez parametrów.</span><span class="sxs-lookup"><span data-stu-id="61ed0-109">When the attribute is not used, a public parameterless constructor is always used if present.</span></span> <span data-ttu-id="61ed0-110">Atrybutu można używać tylko z konstruktorami publicznymi.</span><span class="sxs-lookup"><span data-stu-id="61ed0-110">The attribute can only be used with public constructors.</span></span> <span data-ttu-id="61ed0-111">W poniższym przykładzie zastosowano `[JsonConstructor]` atrybut:</span><span class="sxs-lookup"><span data-stu-id="61ed0-111">The following example uses the `[JsonConstructor]` attribute:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/ImmutableTypes.cs" highlight="13":::

<span data-ttu-id="61ed0-112">Rekordy w języku C# 9 są również obsługiwane, jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="61ed0-112">Records in C# 9 are also supported, as shown in the following example:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/Records.cs":::

<span data-ttu-id="61ed0-113">W przypadku typów, które są niezmienne, ponieważ wszystkie ich metody ustawiające właściwości są niepubliczne, zapoznaj się z następującą sekcją dotyczącą [metod dostępu do właściwości niepublicznych](#non-public-property-accessors).</span><span class="sxs-lookup"><span data-stu-id="61ed0-113">For types that are immutable because all their property setters are non-public, see the following section about [non-public property accessors](#non-public-property-accessors).</span></span>
::: zone-end

::: zone pivot="dotnet-core-3-1"
<span data-ttu-id="61ed0-114">`JsonConstructorAttribute` Obsługa rekordów w języku C# 9 nie jest dostępna w programie .NET Core 3,1.</span><span class="sxs-lookup"><span data-stu-id="61ed0-114">`JsonConstructorAttribute` and C# 9 Record support aren't available in .NET Core 3.1.</span></span>
::: zone-end

## <a name="non-public-property-accessors"></a><span data-ttu-id="61ed0-115">Metody dostępu do właściwości niepublicznych</span><span class="sxs-lookup"><span data-stu-id="61ed0-115">Non-public property accessors</span></span>

::: zone pivot="dotnet-5-0"
<span data-ttu-id="61ed0-116">Aby włączyć użycie niepublicznego dostępu do właściwości, Użyj atrybutu [[JsonInclude]](xref:System.Text.Json.Serialization.JsonIncludeAttribute) , jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="61ed0-116">To enable use of a non-public property accessor, use the [[JsonInclude]](xref:System.Text.Json.Serialization.JsonIncludeAttribute) attribute, as shown in the following example:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/NonPublicAccessors.cs" highlight="12,15":::
::: zone-end

::: zone pivot="dotnet-core-3-1"
<span data-ttu-id="61ed0-117">Metody dostępu do właściwości niepublicznych nie są obsługiwane w programie .NET Core 3,1.</span><span class="sxs-lookup"><span data-stu-id="61ed0-117">Non-public property accessors are not supported in .NET Core 3.1.</span></span> <span data-ttu-id="61ed0-118">Aby uzyskać więcej informacji, zobacz [Migrowanie z Newtonsoft.Json artykułu](system-text-json-migrate-from-newtonsoft-how-to.md#non-public-property-setters-and-getters).</span><span class="sxs-lookup"><span data-stu-id="61ed0-118">For more information, see [the Migrate from Newtonsoft.Json article](system-text-json-migrate-from-newtonsoft-how-to.md#non-public-property-setters-and-getters).</span></span>
::: zone-end

## <a name="see-also"></a><span data-ttu-id="61ed0-119">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="61ed0-119">See also</span></span>

* [<span data-ttu-id="61ed0-120">System.Text.Json Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="61ed0-120">System.Text.Json overview</span></span>](system-text-json-overview.md)
* [<span data-ttu-id="61ed0-121">Tworzenie wystąpienia JsonSerializerOptions</span><span class="sxs-lookup"><span data-stu-id="61ed0-121">Instantiate JsonSerializerOptions</span></span>](system-text-json-configure-options.md)
* [<span data-ttu-id="61ed0-122">Włącz dopasowywanie bez uwzględniania wielkości liter</span><span class="sxs-lookup"><span data-stu-id="61ed0-122">Enable case-insensitive matching</span></span>](system-text-json-character-casing.md)
* [<span data-ttu-id="61ed0-123">Dostosowywanie nazw i wartości właściwości</span><span class="sxs-lookup"><span data-stu-id="61ed0-123">Customize property names and values</span></span>](system-text-json-customize-properties.md)
* [<span data-ttu-id="61ed0-124">Ignoruj właściwości</span><span class="sxs-lookup"><span data-stu-id="61ed0-124">Ignore properties</span></span>](system-text-json-ignore-properties.md)
* [<span data-ttu-id="61ed0-125">Zezwalaj na nieprawidłowy kod JSON</span><span class="sxs-lookup"><span data-stu-id="61ed0-125">Allow invalid JSON</span></span>](system-text-json-invalid-json.md)
* [<span data-ttu-id="61ed0-126">Obsługa przepełnienia kodu JSON</span><span class="sxs-lookup"><span data-stu-id="61ed0-126">Handle overflow JSON</span></span>](system-text-json-handle-overflow.md)
* [<span data-ttu-id="61ed0-127">Zachowaj odwołania cykliczne</span><span class="sxs-lookup"><span data-stu-id="61ed0-127">Preserve circular references</span></span>](system-text-json-preserve-references.md)
* [<span data-ttu-id="61ed0-128">Serializacja polimorficzna</span><span class="sxs-lookup"><span data-stu-id="61ed0-128">Polymorphic serialization</span></span>](system-text-json-polymorphism.md)
* <span data-ttu-id="61ed0-129">[System.Text.Json Dokumentacja interfejsu API](xref:System.Text.Json)</span><span class="sxs-lookup"><span data-stu-id="61ed0-129">[System.Text.Json API reference](xref:System.Text.Json)</span></span>
