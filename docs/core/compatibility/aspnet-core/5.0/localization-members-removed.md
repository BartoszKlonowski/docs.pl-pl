---
title: 'Nieprzerwana zmiana: Lokalizacja: Usunięto klasę ResourceManagerWithCultureStringLocalizer i element członkowski interfejsu WithCulture'
description: 'Dowiedz się więcej o zmianach w 5,0 ASP.NET Core lokalizacji zatytułowanej: Klasa ResourceManagerWithCultureStringLocalizer i element członkowski interfejsu WithCulture usunięte'
author: scottaddie
ms.author: scaddie
ms.date: 10/01/2020
ms.openlocfilehash: ac7723cd9b961b34b3f87a55119d421668c87417
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96437853"
---
# <a name="localization-resourcemanagerwithculturestringlocalizer-class-and-withculture-interface-member-removed"></a><span data-ttu-id="c6ac1-103">Lokalizacja: Usunięto klasę ResourceManagerWithCultureStringLocalizer i element członkowski interfejsu WithCulture</span><span class="sxs-lookup"><span data-stu-id="c6ac1-103">Localization: ResourceManagerWithCultureStringLocalizer class and WithCulture interface member removed</span></span>

<span data-ttu-id="c6ac1-104">Klasa [ResourceManagerWithCultureStringLocalizer](/dotnet/api/microsoft.extensions.localization.resourcemanagerwithculturestringlocalizer?view=dotnet-plat-ext-3.1) i Metoda [WithCulture](/dotnet/api/microsoft.extensions.localization.resourcemanagerstringlocalizer.withculture?view=dotnet-plat-ext-3.1) zostały usunięte w programie .NET 5,0 Preview 1.</span><span class="sxs-lookup"><span data-stu-id="c6ac1-104">The [ResourceManagerWithCultureStringLocalizer](/dotnet/api/microsoft.extensions.localization.resourcemanagerwithculturestringlocalizer?view=dotnet-plat-ext-3.1) class and [WithCulture](/dotnet/api/microsoft.extensions.localization.resourcemanagerstringlocalizer.withculture?view=dotnet-plat-ext-3.1) method were removed in .NET 5.0 Preview 1.</span></span>

<span data-ttu-id="c6ac1-105">W przypadku kontekstu zobacz [ASPNET/anonse # 346](https://github.com/aspnet/Announcements/issues/346) i [dotnet/aspnetcore # 3324](https://github.com/dotnet/aspnetcore/issues/3324).</span><span class="sxs-lookup"><span data-stu-id="c6ac1-105">For context, see [aspnet/Announcements#346](https://github.com/aspnet/Announcements/issues/346) and [dotnet/aspnetcore#3324](https://github.com/dotnet/aspnetcore/issues/3324).</span></span> <span data-ttu-id="c6ac1-106">Aby uzyskać więcej dyskusji na temat tej zmiany, zobacz [dotnet/aspnetcore # 7756](https://github.com/dotnet/aspnetcore/issues/7756).</span><span class="sxs-lookup"><span data-stu-id="c6ac1-106">For discussion on this change, see [dotnet/aspnetcore#7756](https://github.com/dotnet/aspnetcore/issues/7756).</span></span>

## <a name="version-introduced"></a><span data-ttu-id="c6ac1-107">Wprowadzona wersja</span><span class="sxs-lookup"><span data-stu-id="c6ac1-107">Version introduced</span></span>

<span data-ttu-id="c6ac1-108">5,0 wersja zapoznawcza 1</span><span class="sxs-lookup"><span data-stu-id="c6ac1-108">5.0 Preview 1</span></span>

## <a name="old-behavior"></a><span data-ttu-id="c6ac1-109">Stare zachowanie</span><span class="sxs-lookup"><span data-stu-id="c6ac1-109">Old behavior</span></span>

<span data-ttu-id="c6ac1-110">`ResourceManagerWithCultureStringLocalizer`Klasa i `ResourceManagerStringLocalizer.WithCulture` Metoda są [przestarzałe w programie .NET Core 3,0 w wersji zapoznawczej 3 i nowszych](../../3.0.md#localization-resourcemanagerwithculturestringlocalizer-and-withculture-marked-obsolete).</span><span class="sxs-lookup"><span data-stu-id="c6ac1-110">The `ResourceManagerWithCultureStringLocalizer` class and the `ResourceManagerStringLocalizer.WithCulture` method are [obsolete in .NET Core 3.0 Preview 3 and later](../../3.0.md#localization-resourcemanagerwithculturestringlocalizer-and-withculture-marked-obsolete).</span></span>

## <a name="new-behavior"></a><span data-ttu-id="c6ac1-111">Nowe zachowanie</span><span class="sxs-lookup"><span data-stu-id="c6ac1-111">New behavior</span></span>

<span data-ttu-id="c6ac1-112">`ResourceManagerWithCultureStringLocalizer`Klasa i Metoda zostały `ResourceManagerStringLocalizer.WithCulture` usunięte w programie .NET 5,0 Preview 1.</span><span class="sxs-lookup"><span data-stu-id="c6ac1-112">The `ResourceManagerWithCultureStringLocalizer` class and the `ResourceManagerStringLocalizer.WithCulture` method have been removed in .NET 5.0 Preview 1.</span></span> <span data-ttu-id="c6ac1-113">Aby uzyskać spis zmian wprowadzonych w programie, zobacz żądanie ściągnięcia w programie [dotnet/Extensions # 2562](https://github.com/dotnet/extensions/pull/2562/files).</span><span class="sxs-lookup"><span data-stu-id="c6ac1-113">For an inventory of the changes made, see the pull request at [dotnet/extensions#2562](https://github.com/dotnet/extensions/pull/2562/files).</span></span>

## <a name="reason-for-change"></a><span data-ttu-id="c6ac1-114">Przyczyna zmiany</span><span class="sxs-lookup"><span data-stu-id="c6ac1-114">Reason for change</span></span>

<span data-ttu-id="c6ac1-115">Metody [ResourceManagerWithCultureStringLocalizer](/dotnet/api/microsoft.extensions.localization.resourcemanagerwithculturestringlocalizer?view=dotnet-plat-ext-3.1) i [ResourceManagerStringLocalizer. WithCulture](/dotnet/api/microsoft.extensions.localization.resourcemanagerstringlocalizer.withculture?view=dotnet-plat-ext-3.1) często są źródłami pomyłek dla użytkowników lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="c6ac1-115">The [ResourceManagerWithCultureStringLocalizer](/dotnet/api/microsoft.extensions.localization.resourcemanagerwithculturestringlocalizer?view=dotnet-plat-ext-3.1) class and [ResourceManagerStringLocalizer.WithCulture](/dotnet/api/microsoft.extensions.localization.resourcemanagerstringlocalizer.withculture?view=dotnet-plat-ext-3.1) method were often sources of confusion for users of localization.</span></span> <span data-ttu-id="c6ac1-116">Pomyłka była szczególnie wysoka podczas tworzenia niestandardowej <xref:Microsoft.Extensions.Localization.IStringLocalizer> implementacji.</span><span class="sxs-lookup"><span data-stu-id="c6ac1-116">The confusion was especially high when creating a custom <xref:Microsoft.Extensions.Localization.IStringLocalizer> implementation.</span></span> <span data-ttu-id="c6ac1-117">Ta klasa i Metoda zapewniają konsumentom wrażenie, że `IStringLocalizer` wystąpienie jest oczekiwane na "dla poszczególnych zasobów".</span><span class="sxs-lookup"><span data-stu-id="c6ac1-117">This class and method give consumers the impression that an `IStringLocalizer` instance is expected to be "per-language, per-resource".</span></span> <span data-ttu-id="c6ac1-118">W rzeczywistości wystąpienie powinno mieć tylko wartość "dla zasobu".</span><span class="sxs-lookup"><span data-stu-id="c6ac1-118">In reality, the instance should only be "per-resource".</span></span> <span data-ttu-id="c6ac1-119">W czasie wykonywania <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=nameWithType> Właściwość określa język, który ma być używany.</span><span class="sxs-lookup"><span data-stu-id="c6ac1-119">At run time, the <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=nameWithType> property determines the language to be used.</span></span>

## <a name="recommended-action"></a><span data-ttu-id="c6ac1-120">Zalecana akcja</span><span class="sxs-lookup"><span data-stu-id="c6ac1-120">Recommended action</span></span>

<span data-ttu-id="c6ac1-121">Zatrzymaj korzystanie z `ResourceManagerWithCultureStringLocalizer` klasy i `ResourceManagerStringLocalizer.WithCulture` metody.</span><span class="sxs-lookup"><span data-stu-id="c6ac1-121">Stop using the `ResourceManagerWithCultureStringLocalizer` class and the `ResourceManagerStringLocalizer.WithCulture` method.</span></span>

## <a name="affected-apis"></a><span data-ttu-id="c6ac1-122">Dotyczy interfejsów API</span><span class="sxs-lookup"><span data-stu-id="c6ac1-122">Affected APIs</span></span>

- [<span data-ttu-id="c6ac1-123">ResourceManagerWithCultureStringLocalizer</span><span class="sxs-lookup"><span data-stu-id="c6ac1-123">ResourceManagerWithCultureStringLocalizer</span></span>](/dotnet/api/microsoft.extensions.localization.resourcemanagerwithculturestringlocalizer?view=dotnet-plat-ext-3.1)
- [<span data-ttu-id="c6ac1-124">ResourceManagerStringLocalizer.WithCulture</span><span class="sxs-lookup"><span data-stu-id="c6ac1-124">ResourceManagerStringLocalizer.WithCulture</span></span>](/dotnet/api/microsoft.extensions.localization.resourcemanagerstringlocalizer.withculture?view=dotnet-plat-ext-3.1)

<!--

### Category

ASP.NET Core

### Affected APIs

- `T:Microsoft.Extensions.Localization.ResourceManagerWithCultureStringLocalizer`
- `Overload:Microsoft.Extensions.Localization.ResourceManagerStringLocalizer.WithCulture`

-->
