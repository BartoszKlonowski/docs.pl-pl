---
title: 'Zmiana podziału: Blazor: zmiany w logice routingu w aplikacjach Blazor'
description: 'Dowiedz się więcej o istotnej zmianie w ASP.NET Core 5,0 zatytułowanej Blazor: zmiany w logice routingu w aplikacjach Blazor'
author: scottaddie
ms.author: scaddie
ms.date: 12/14/2020
ms.openlocfilehash: 4ab8289565c88b17eb204a11724bb12a09b033c2
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2020
ms.locfileid: "97513524"
---
# <a name="blazor-route-precedence-logic-changed-in-blazor-apps"></a><span data-ttu-id="2057f-103">Blazor: Logika pierwszeństwa trasy została zmieniona w aplikacjach Blazor</span><span class="sxs-lookup"><span data-stu-id="2057f-103">Blazor: Route precedence logic changed in Blazor apps</span></span>

<span data-ttu-id="2057f-104">Usterka w implementacji routingu Blazor ma wpływ na sposób określania priorytetu tras.</span><span class="sxs-lookup"><span data-stu-id="2057f-104">A bug in the Blazor routing implementation affected how the precedence of routes was determined.</span></span> <span data-ttu-id="2057f-105">Ta usterka ma wpływ na wszystkie trasy lub trasy z opcjonalnymi parametrami w aplikacji Blazor.</span><span class="sxs-lookup"><span data-stu-id="2057f-105">This bug affects catch-all routes or routes with optional parameters within your Blazor app.</span></span>

## <a name="version-introduced"></a><span data-ttu-id="2057f-106">Wprowadzona wersja</span><span class="sxs-lookup"><span data-stu-id="2057f-106">Version introduced</span></span>

<span data-ttu-id="2057f-107">5.0.1</span><span class="sxs-lookup"><span data-stu-id="2057f-107">5.0.1</span></span>

## <a name="old-behavior"></a><span data-ttu-id="2057f-108">Stare zachowanie</span><span class="sxs-lookup"><span data-stu-id="2057f-108">Old behavior</span></span>

<span data-ttu-id="2057f-109">W przypadku błędnego zachowania trasy o niższym priorytecie są brane pod uwagę i dopasowywane przez trasy o wyższym priorytecie.</span><span class="sxs-lookup"><span data-stu-id="2057f-109">With the erroneous behavior, routes with lower precedence are considered and matched over routes with higher precedence.</span></span> <span data-ttu-id="2057f-110">Na przykład `{*slug}` trasa jest dopasowana wcześniej `/customer/{id}` .</span><span class="sxs-lookup"><span data-stu-id="2057f-110">For example, the `{*slug}` route is matched before `/customer/{id}`.</span></span>

## <a name="new-behavior"></a><span data-ttu-id="2057f-111">Nowe zachowanie</span><span class="sxs-lookup"><span data-stu-id="2057f-111">New behavior</span></span>

<span data-ttu-id="2057f-112">Bieżące zachowanie jest dokładniej zgodne z zachowaniem routingu zdefiniowanym w ASP.NET Core aplikacjach.</span><span class="sxs-lookup"><span data-stu-id="2057f-112">The current behavior more closely matches the routing behavior defined in ASP.NET Core apps.</span></span> <span data-ttu-id="2057f-113">Struktura określa najpierw pierwszeństwo tras dla każdego segmentu.</span><span class="sxs-lookup"><span data-stu-id="2057f-113">The framework determines the route precedence for each segment first.</span></span> <span data-ttu-id="2057f-114">Długość trasy jest używana tylko jako drugie kryterium podziału powiązań.</span><span class="sxs-lookup"><span data-stu-id="2057f-114">The route's length is used only as a second criteria to break ties.</span></span>

## <a name="reason-for-change"></a><span data-ttu-id="2057f-115">Przyczyna zmiany</span><span class="sxs-lookup"><span data-stu-id="2057f-115">Reason for change</span></span>

<span data-ttu-id="2057f-116">Oryginalne zachowanie jest uznawane za usterkę w implementacji.</span><span class="sxs-lookup"><span data-stu-id="2057f-116">The original behavior is considered a bug in the implementation.</span></span> <span data-ttu-id="2057f-117">W rezultacie system routingu w aplikacjach Blazor powinien działać tak samo jak w przypadku systemu routingu w pozostałej części ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="2057f-117">As a goal, the routing system in Blazor apps should behave the same way as the routing system in the rest of ASP.NET Core.</span></span>

## <a name="recommended-action"></a><span data-ttu-id="2057f-118">Zalecana akcja</span><span class="sxs-lookup"><span data-stu-id="2057f-118">Recommended action</span></span>

<span data-ttu-id="2057f-119">W przypadku uaktualniania z poprzednich wersji programu Blazor do 5. x Użyj `PreferExactMatches` atrybutu `Router` składnika.</span><span class="sxs-lookup"><span data-stu-id="2057f-119">If upgrading from previous versions of Blazor to 5.x, use the `PreferExactMatches` attribute on the `Router` component.</span></span> <span data-ttu-id="2057f-120">Ten atrybut może być używany do poprawnego działania.</span><span class="sxs-lookup"><span data-stu-id="2057f-120">This attribute can be used to opt into the correct behavior.</span></span> <span data-ttu-id="2057f-121">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="2057f-121">For example:</span></span>

```razor
<Router AppAssembly="@typeof(Program).Assembly" PreferExactMatches="true">
```

<span data-ttu-id="2057f-122">Gdy `PreferExactMatches` jest ustawiona na `true` , dopasowanie trasy preferuje dokładne dopasowania w przypadku symboli wieloznacznych.</span><span class="sxs-lookup"><span data-stu-id="2057f-122">When `PreferExactMatches` is set to `true`, route matching prefers exact matches over wildcards.</span></span>

## <a name="affected-apis"></a><span data-ttu-id="2057f-123">Dotyczy interfejsów API</span><span class="sxs-lookup"><span data-stu-id="2057f-123">Affected APIs</span></span>

<span data-ttu-id="2057f-124">Brak</span><span class="sxs-lookup"><span data-stu-id="2057f-124">None</span></span>

<!--

## Category

ASP.NET Core

## Affected APIs

Not detectable via API analysis

-->
