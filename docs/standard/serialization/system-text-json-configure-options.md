---
title: Jak utworzyć wystąpienie JsonSerializerOptions z System.Text.Json
description: Dowiedz się, jak tworzyć wystąpienia JsonSerializerOptions, kopiując istniejące wystąpienia lub korzystając z ustawień domyślnych sieci Web.
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
ms.openlocfilehash: 0febfe15f36856f10699fd327fb17c146277eb9b
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96440033"
---
# <a name="how-to-instantiate-jsonserializeroptions-instances-with-no-locsystemtextjson"></a><span data-ttu-id="a7f4a-103">Jak utworzyć wystąpienie JsonSerializerOptions wystąpień z System.Text.Json</span><span class="sxs-lookup"><span data-stu-id="a7f4a-103">How to instantiate JsonSerializerOptions instances with System.Text.Json</span></span>

<span data-ttu-id="a7f4a-104">W tym artykule dowiesz się, jak tworzyć wystąpienia <xref:System.Text.Json.JsonSerializerOptions> wystąpień przez kopiowanie istniejących wystąpień lub z wartościami domyślnymi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="a7f4a-104">In this article, you'll learn how to instantiate <xref:System.Text.Json.JsonSerializerOptions> instances by copying existing instances or with web defaults.</span></span>

## <a name="copy-jsonserializeroptions"></a><span data-ttu-id="a7f4a-105">Kopiuj JsonSerializerOptions</span><span class="sxs-lookup"><span data-stu-id="a7f4a-105">Copy JsonSerializerOptions</span></span>

::: zone pivot="dotnet-5-0"
<span data-ttu-id="a7f4a-106">Istnieje Konstruktor [JsonSerializerOptions] (linki XREF: System.Text.Json . JsonSerializerOptions .% 23ctor ( System.Text.Json . JsonSerializerOptions)), która umożliwia utworzenie nowego wystąpienia z takimi samymi opcjami jak istniejące wystąpienie, jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="a7f4a-106">There is a [JsonSerializerOptions constructor](xref:System.Text.Json.JsonSerializerOptions.%23ctor(System.Text.Json.JsonSerializerOptions)) that lets you create a new instance with the same options as an existing instance, as shown in the following example:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/CopyOptions.cs" highlight="29":::
::: zone-end

::: zone pivot="dotnet-core-3-1"
<span data-ttu-id="a7f4a-107">`JsonSerializerOptions`Konstruktor, który pobiera istniejące wystąpienie, nie jest dostępny w programie .NET Core 3,1.</span><span class="sxs-lookup"><span data-stu-id="a7f4a-107">A `JsonSerializerOptions` constructor that takes an existing instance is not available in .NET Core 3.1.</span></span>
::: zone-end

## <a name="web-defaults-for-jsonserializeroptions"></a><span data-ttu-id="a7f4a-108">Ustawienia domyślne sieci Web dla JsonSerializerOptions</span><span class="sxs-lookup"><span data-stu-id="a7f4a-108">Web defaults for JsonSerializerOptions</span></span>

::: zone pivot="dotnet-5-0"
<span data-ttu-id="a7f4a-109">Poniżej przedstawiono opcje, które mają różne wartości domyślne dla usługi Web Apps:</span><span class="sxs-lookup"><span data-stu-id="a7f4a-109">Here are the options that have different defaults for web apps:</span></span>

* <xref:System.Text.Json.JsonSerializerOptions.PropertyNameCaseInsensitive%2A> = `true`
* <xref:System.Text.Json.JsonNamingPolicy> = <xref:System.Text.Json.JsonNamingPolicy.CamelCase>
* <xref:System.Text.Json.JsonSerializerOptions.NumberHandling%2A> = <xref:System.Text.Json.Serialization.JsonNumberHandling.AllowReadingFromString>

<span data-ttu-id="a7f4a-110">Istnieje Konstruktor [JsonSerializerOptions] (linki XREF: System.Text.Json . JsonSerializerOptions .% 23ctor ( System.Text.Json . JsonSerializerDefaults)? View = NET-5,0&Preserve-View = true), która umożliwia utworzenie nowego wystąpienia z opcjami domyślnymi, które ASP.NET Core używane przez aplikacje sieci Web, jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="a7f4a-110">There's a [JsonSerializerOptions constructor](xref:System.Text.Json.JsonSerializerOptions.%23ctor(System.Text.Json.JsonSerializerDefaults)?view=net-5.0&preserve-view=true) that lets you create a new instance with the default options that ASP.NET Core uses for web apps, as shown in the following example:</span></span>

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/OptionsDefaults.cs" highlight="24":::
::: zone-end

::: zone pivot="dotnet-core-3-1"
<span data-ttu-id="a7f4a-111">Poniżej przedstawiono opcje, które mają różne wartości domyślne dla usługi Web Apps:</span><span class="sxs-lookup"><span data-stu-id="a7f4a-111">Here are the options that have different defaults for web apps:</span></span>

* <xref:System.Text.Json.JsonSerializerOptions.PropertyNameCaseInsensitive%2A> = `true`
* <xref:System.Text.Json.JsonNamingPolicy> = <xref:System.Text.Json.JsonNamingPolicy.CamelCase>

<span data-ttu-id="a7f4a-112">`JsonSerializerOptions`Konstruktor, który określa zestaw ustawień domyślnych, nie jest dostępny w programie .NET Core 3,1.</span><span class="sxs-lookup"><span data-stu-id="a7f4a-112">A `JsonSerializerOptions` constructor that specifies a set of defaults is not available in .NET Core 3.1.</span></span>
::: zone-end

## <a name="see-also"></a><span data-ttu-id="a7f4a-113">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="a7f4a-113">See also</span></span>

* [<span data-ttu-id="a7f4a-114">System.Text.Json Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="a7f4a-114">System.Text.Json overview</span></span>](system-text-json-overview.md)
* [<span data-ttu-id="a7f4a-115">Włącz dopasowywanie bez uwzględniania wielkości liter</span><span class="sxs-lookup"><span data-stu-id="a7f4a-115">Enable case-insensitive matching</span></span>](system-text-json-character-casing.md)
* [<span data-ttu-id="a7f4a-116">Dostosowywanie nazw i wartości właściwości</span><span class="sxs-lookup"><span data-stu-id="a7f4a-116">Customize property names and values</span></span>](system-text-json-customize-properties.md)
* [<span data-ttu-id="a7f4a-117">Ignoruj właściwości</span><span class="sxs-lookup"><span data-stu-id="a7f4a-117">Ignore properties</span></span>](system-text-json-ignore-properties.md)
* [<span data-ttu-id="a7f4a-118">Zezwalaj na nieprawidłowy kod JSON</span><span class="sxs-lookup"><span data-stu-id="a7f4a-118">Allow invalid JSON</span></span>](system-text-json-invalid-json.md)
* [<span data-ttu-id="a7f4a-119">Obsługa przepełnienia kodu JSON</span><span class="sxs-lookup"><span data-stu-id="a7f4a-119">Handle overflow JSON</span></span>](system-text-json-handle-overflow.md)
* [<span data-ttu-id="a7f4a-120">Zachowaj odwołania cykliczne</span><span class="sxs-lookup"><span data-stu-id="a7f4a-120">Preserve circular references</span></span>](system-text-json-preserve-references.md)
* [<span data-ttu-id="a7f4a-121">Niemodyfikowalne typy i niepubliczne metody dostępu</span><span class="sxs-lookup"><span data-stu-id="a7f4a-121">Immutable types and non-public accessors</span></span>](system-text-json-immutability.md)
* [<span data-ttu-id="a7f4a-122">Serializacja polimorficzna</span><span class="sxs-lookup"><span data-stu-id="a7f4a-122">Polymorphic serialization</span></span>](system-text-json-polymorphism.md)
* <span data-ttu-id="a7f4a-123">[System.Text.Json Dokumentacja interfejsu API](xref:System.Text.Json)</span><span class="sxs-lookup"><span data-stu-id="a7f4a-123">[System.Text.Json API reference](xref:System.Text.Json)</span></span>
