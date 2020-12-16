---
title: Analizator zgodności platformy
description: Analizator Roslyn, który może pomóc w wykrywaniu problemów ze zgodnością platformy w aplikacjach i bibliotekach dla wielu platform.
author: buyaa-n
ms.date: 09/17/2020
ms.openlocfilehash: 427a2d8ae61a82699e5cf0987fcd1c5a45152cac
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/16/2020
ms.locfileid: "97594920"
---
# <a name="platform-compatibility-analyzer"></a><span data-ttu-id="3c34a-103">Analizator zgodności platformy</span><span class="sxs-lookup"><span data-stu-id="3c34a-103">Platform compatibility analyzer</span></span>

<span data-ttu-id="3c34a-104">Prawdopodobnie przesłuchasz motto "jeden .NET": pojedynczej, ujednoliconej platformy do tworzenia aplikacji dowolnego typu.</span><span class="sxs-lookup"><span data-stu-id="3c34a-104">You've probably heard the motto of "One .NET": a single, unified platform for building any type of application.</span></span> <span data-ttu-id="3c34a-105">Zestaw SDK programu .NET 5,0 zawiera ASP.NET Core, Entity Framework Core, WinForms, WPF, Xamarin i ML.NET, a także doda obsługę większej liczby platform w czasie.</span><span class="sxs-lookup"><span data-stu-id="3c34a-105">The .NET 5.0 SDK includes ASP.NET Core, Entity Framework Core, WinForms, WPF, Xamarin, and ML.NET, and will add support for more platforms over time.</span></span> <span data-ttu-id="3c34a-106">Program .NET 5,0 dokłada starań, aby zapewnić środowisko, w którym nie trzeba mieć powodów dotyczących różnych wersji platformy .NET, ale nie próbuje w pełni abstrakcji bazowego systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="3c34a-106">.NET 5.0 strives to provide an experience where you don't have to reason about the different flavors of .NET, but doesn't attempt to fully abstract away the underlying operating system (OS).</span></span> <span data-ttu-id="3c34a-107">Nadal będziesz mieć możliwość wywoływania interfejsów API specyficznych dla platformy, na przykład P/Invoke, WinRT lub powiązań Xamarin dla systemów iOS i Android.</span><span class="sxs-lookup"><span data-stu-id="3c34a-107">You'll continue to be able to call platform-specific APIs, for example, P/Invokes, WinRT, or the Xamarin bindings for iOS and Android.</span></span>

<span data-ttu-id="3c34a-108">Jednak używanie interfejsów API specyficznych dla platformy na składniku oznacza, że kod nie działa już na wszystkich platformach.</span><span class="sxs-lookup"><span data-stu-id="3c34a-108">But using platform-specific APIs on a component means the code no longer works across all platforms.</span></span> <span data-ttu-id="3c34a-109">Potrzebujemy sposobu na wykrycie tego rozwiązania w czasie projektowania, aby deweloperzy mogli uzyskać diagnostykę, gdy przypadkowo używają interfejsów API specyficznych dla platformy.</span><span class="sxs-lookup"><span data-stu-id="3c34a-109">We needed a way to detect this at design time so developers get diagnostics when they inadvertently use platform-specific APIs.</span></span> <span data-ttu-id="3c34a-110">Aby osiągnąć ten cel, w programie .NET 5,0 wprowadzono [analizatora zgodności platformy](../../fundamentals/code-analysis/quality-rules/ca1416.md) i uzupełniające się interfejsy API, które ułatwiają deweloperom identyfikowanie i Używanie interfejsów API specyficznych dla platformy w miarę potrzeb.</span><span class="sxs-lookup"><span data-stu-id="3c34a-110">To achieve this goal, .NET 5.0 introduces the [platform compatibility analyzer](../../fundamentals/code-analysis/quality-rules/ca1416.md) and complementary APIs to help developers identify and use platform-specific APIs where appropriate.</span></span>

<span data-ttu-id="3c34a-111">Nowe interfejsy API obejmują:</span><span class="sxs-lookup"><span data-stu-id="3c34a-111">The new APIs include:</span></span>

- <span data-ttu-id="3c34a-112"><xref:System.Runtime.Versioning.SupportedOSPlatformAttribute> Dodawanie adnotacji do interfejsów API jako specyficznych dla platformy i <xref:System.Runtime.Versioning.UnsupportedOSPlatformAttribute> Dodawanie adnotacji do interfejsów API jako nieobsługiwanych w określonym systemie operacyjnym.</span><span class="sxs-lookup"><span data-stu-id="3c34a-112"><xref:System.Runtime.Versioning.SupportedOSPlatformAttribute> to annotate APIs as being platform-specific and <xref:System.Runtime.Versioning.UnsupportedOSPlatformAttribute> to annotate APIs as being unsupported on a particular OS.</span></span> <span data-ttu-id="3c34a-113">Te atrybuty mogą opcjonalnie zawierać numer wersji i zostały już zastosowane do niektórych interfejsów API specyficznych dla platformy w podstawowych bibliotekach platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="3c34a-113">These attributes can optionally include the version number, and have already been applied to some platform-specific APIs in the core .NET libraries.</span></span>
- <span data-ttu-id="3c34a-114">`Is<Platform>()` i `Is<Platform>VersionAtLeast(int major, int minor = 0, int build = 0, int revision = 0)` metody statyczne w <xref:System.OperatingSystem?displayProperty=nameWithType> klasie w celu bezpiecznego wywoływania interfejsów API specyficznych dla platformy.</span><span class="sxs-lookup"><span data-stu-id="3c34a-114">`Is<Platform>()` and `Is<Platform>VersionAtLeast(int major, int minor = 0, int build = 0, int revision = 0)` static methods in the <xref:System.OperatingSystem?displayProperty=nameWithType> class for safely calling platform-specific APIs.</span></span> <span data-ttu-id="3c34a-115">Na przykład <xref:System.OperatingSystem.IsWindows?displayProperty=nameWithType> może służyć do ochrony wywołania interfejsu API specyficznego dla systemu Windows, a <xref:System.OperatingSystem.IsWindowsVersionAtLeast%2A?displayProperty=nameWithType> () może służyć do ochrony wywołania interfejsu API specyficznego dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="3c34a-115">For example, <xref:System.OperatingSystem.IsWindows?displayProperty=nameWithType> can be used to guard a call to a Windows-specific API, and <xref:System.OperatingSystem.IsWindowsVersionAtLeast%2A?displayProperty=nameWithType>() can be used to guard a versioned Windows-specific API call.</span></span> <span data-ttu-id="3c34a-116">Zapoznaj się z tymi [przykładami](#guard-platform-specific-apis-with-guard-methods) , jak te metody mogą być używane jako osłony odwołań do interfejsów API specyficznych dla platformy.</span><span class="sxs-lookup"><span data-stu-id="3c34a-116">See these [examples](#guard-platform-specific-apis-with-guard-methods) of how these methods can be used as guards of platform-specific API references.</span></span>

> [!TIP]
> <span data-ttu-id="3c34a-117">Analizator zgodności platformy uaktualnia i zastępuje funkcję [odnajdywania problemów między platformami](../../standard/analyzers/api-analyzer.md#discover-cross-platform-issues) w [analizatorze interfejsu API platformy .NET](../../standard/analyzers/api-analyzer.md).</span><span class="sxs-lookup"><span data-stu-id="3c34a-117">The platform compatibility analyzer upgrades and replaces the [Discovering cross-platform issues](../../standard/analyzers/api-analyzer.md#discover-cross-platform-issues) feature of the [.NET API analyzer](../../standard/analyzers/api-analyzer.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3c34a-118">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3c34a-118">Prerequisites</span></span>

<span data-ttu-id="3c34a-119">Analizator zgodności platformy jest jednym z Roslynjących analiz jakości kodu.</span><span class="sxs-lookup"><span data-stu-id="3c34a-119">The platform compatibility analyzer is one of the Roslyn code quality analyzers.</span></span> <span data-ttu-id="3c34a-120">Począwszy od wersji .NET 5.0 te analizatory są [uwzględnione w zestawie .NET SDK](../../fundamentals/code-analysis/overview.md).</span><span class="sxs-lookup"><span data-stu-id="3c34a-120">Starting in .NET 5.0, these analyzers are [included with the .NET SDK](../../fundamentals/code-analysis/overview.md).</span></span> <span data-ttu-id="3c34a-121">Analizator zgodności platformy jest domyślnie włączony tylko w przypadku projektów docelowych `net5.0` lub nowszych.</span><span class="sxs-lookup"><span data-stu-id="3c34a-121">The platform compatibility analyzer is enabled by default only for projects that target `net5.0` or a later version.</span></span> <span data-ttu-id="3c34a-122">Można [go jednak włączyć](../../fundamentals/code-analysis/quality-rules/ca1416.md#configure-code-to-analyze) dla projektów przeznaczonych dla innych platform.</span><span class="sxs-lookup"><span data-stu-id="3c34a-122">However, you can [enable it](../../fundamentals/code-analysis/quality-rules/ca1416.md#configure-code-to-analyze) for projects that target other frameworks.</span></span>

## <a name="how-the-analyzer-determines-platform-dependency"></a><span data-ttu-id="3c34a-123">Jak Analizator określa zależność platformy</span><span class="sxs-lookup"><span data-stu-id="3c34a-123">How the analyzer determines platform dependency</span></span>

- <span data-ttu-id="3c34a-124">**Nieprzypisany interfejs API** jest uznawany za działający na **wszystkich platformach systemu operacyjnego**.</span><span class="sxs-lookup"><span data-stu-id="3c34a-124">An **unattributed API** is considered to work on **all OS platforms**.</span></span>
- <span data-ttu-id="3c34a-125">Interfejs API oznaczony jako with `[SupportedOSPlatform("platform")]` jest traktowany jako przenośny tylko w określonym systemie operacyjnym `platform` .</span><span class="sxs-lookup"><span data-stu-id="3c34a-125">An API marked with `[SupportedOSPlatform("platform")]` is considered only portable to the specified OS `platform`.</span></span>
  - <span data-ttu-id="3c34a-126">Ten atrybut można zastosować wiele razy, aby wskazać **obsługę wielu platform** ( `[SupportedOSPlatform("windows"), SupportedOSPlatform("Android6.0")]` ).</span><span class="sxs-lookup"><span data-stu-id="3c34a-126">The attribute can be applied multiple times to indicate **multiple platform support** (`[SupportedOSPlatform("windows"), SupportedOSPlatform("Android6.0")]`).</span></span>
  - <span data-ttu-id="3c34a-127">Analizator wyświetli **Ostrzeżenie** , jeśli do interfejsów API specyficznych dla platformy są przywoływane bez odpowiedniego **kontekstu platformy**:</span><span class="sxs-lookup"><span data-stu-id="3c34a-127">The analyzer will produce a **warning** if platform-specific APIs are referenced without a proper **platform context**:</span></span>
    - <span data-ttu-id="3c34a-128">**Ostrzega** , jeśli projekt nie jest celem obsługiwanej platformy (na przykład wywołania interfejsu API określonego dla systemu Windows i obiektów docelowych projektu `<TargetFramework>net5.0-ios14.0</TargetFramework>` ).</span><span class="sxs-lookup"><span data-stu-id="3c34a-128">**Warns** if the project doesn't target the supported platform (for example, a Windows-specific API call and the project targets `<TargetFramework>net5.0-ios14.0</TargetFramework>`).</span></span>
    - <span data-ttu-id="3c34a-129">**Ostrzega** , jeśli projekt jest przeznaczony do wielowymiarowego ( `<TargetFramework>net5.0</TargetFramework>` ).</span><span class="sxs-lookup"><span data-stu-id="3c34a-129">**Warns** if the project is multi-targeted (`<TargetFramework>net5.0</TargetFramework>`).</span></span>
    - <span data-ttu-id="3c34a-130">**Nie ostrzega** o tym, czy w ramach projektu, który jest przeznaczony dla określonych **platform** (na przykład dla wywołania interfejsu API określonego dla systemu Windows i elementów docelowych projektu), jest przywoływany interfejs API specyficzny dla platformy `<TargetFramework>net5.0-windows</TargetFramework>` .</span><span class="sxs-lookup"><span data-stu-id="3c34a-130">**Doesn't warn** if the platform-specific API is referenced within a project that targets any of the **specified platforms** (for example, for a Windows-specific API call and the project targets `<TargetFramework>net5.0-windows</TargetFramework>`).</span></span>
    - <span data-ttu-id="3c34a-131">**Nie ostrzega** , jeśli wywołanie interfejsu API specyficzne dla platformy jest chronione przez odpowiednie metody sprawdzania platformy (na przykład `if(OperatingSystem.IsWindows())` ).</span><span class="sxs-lookup"><span data-stu-id="3c34a-131">**Doesn't warn** if the platform-specific API call is guarded by corresponding platform-check methods (for example, `if(OperatingSystem.IsWindows())`).</span></span>
    - <span data-ttu-id="3c34a-132">**Nie ostrzega** , jeśli interfejs API specyficzny dla platformy jest przywoływany z tego samego kontekstu specyficznego dla platformy (**połączenie jest również przypisane** do `[SupportedOSPlatform("platform")` ).</span><span class="sxs-lookup"><span data-stu-id="3c34a-132">**Doesn't warn** if the platform-specific API is referenced from the same platform-specific context (**call site also attributed** with `[SupportedOSPlatform("platform")`).</span></span>
- <span data-ttu-id="3c34a-133">Interfejs API oznaczony za pomocą `[UnsupportedOSPlatform("platform")]` jest uznawany za nieobsługiwany tylko w określonym systemie operacyjnym, `platform` ale jest obsługiwany przez wszystkie inne platformy.</span><span class="sxs-lookup"><span data-stu-id="3c34a-133">An API marked with `[UnsupportedOSPlatform("platform")]` is considered unsupported only on the specified OS `platform` but supported for all other platforms.</span></span>
  - <span data-ttu-id="3c34a-134">Ten atrybut może być stosowany wiele razy z różnymi platformami, na przykład `[UnsupportedOSPlatform("iOS"), UnsupportedOSPlatform("Android6.0")]` .</span><span class="sxs-lookup"><span data-stu-id="3c34a-134">The attribute can be applied multiple times with different platforms, for example, `[UnsupportedOSPlatform("iOS"), UnsupportedOSPlatform("Android6.0")]`.</span></span>
  - <span data-ttu-id="3c34a-135">Analizator generuje **Ostrzeżenie** tylko wtedy, gdy `platform` jest skuteczny dla witryny wywołania:</span><span class="sxs-lookup"><span data-stu-id="3c34a-135">The analyzer produces a **warning** only if the `platform` is effective for the call site:</span></span>
    - <span data-ttu-id="3c34a-136">**Ostrzega** , jeśli projekt jest przeznaczony dla platformy, która jest przypisana jako nieobsługiwana (na przykład jeśli interfejs API jest przypisany do `[UnsupportedOSPlatform("windows")]` i dla obiektów docelowych lokacji wywołania `<TargetFramework>net5.0-windows</TargetFramework>` ).</span><span class="sxs-lookup"><span data-stu-id="3c34a-136">**Warns** if the project targets the platform that's attributed as unsupported (for example, if the API is attributed with `[UnsupportedOSPlatform("windows")]` and the call site targets `<TargetFramework>net5.0-windows</TargetFramework>`).</span></span>
    - <span data-ttu-id="3c34a-137">**Ostrzega** o tym, czy projekt jest przeznaczony do wielowymiarowego i `platform` znajduje się w domyślnej grupie elementów programu [ `<SupportedPlatform>` MSBuild](https://github.com/dotnet/sdk/blob/master/src/Tasks/Microsoft.NET.Build.Tasks/targets/Microsoft.NET.SupportedPlatforms.props) , czy też `platform` jest zawarty ręcznie w `MSBuild` \<SupportedPlatform> grupie Items:</span><span class="sxs-lookup"><span data-stu-id="3c34a-137">**Warns** if the project is multi-targeted and the `platform` is included in the default [MSBuild `<SupportedPlatform>`](https://github.com/dotnet/sdk/blob/master/src/Tasks/Microsoft.NET.Build.Tasks/targets/Microsoft.NET.SupportedPlatforms.props) items group, or the `platform` is manually included within the `MSBuild` \<SupportedPlatform> items group:</span></span>

      ```XML
      <ItemGroup>
          <SupportedPlatform Include="platform" />
      </ItemGroup>
      ```

    - <span data-ttu-id="3c34a-138">**Nie ostrzega** w przypadku kompilowania aplikacji, która nie jest przeznaczona dla nieobsługiwanej platformy lub ma wiele obiektów docelowych, a platforma nie jest uwzględniona w domyślnej grupie elementów programu [MSBuild `<SupportedPlatform>`](https://github.com/dotnet/sdk/blob/master/src/Tasks/Microsoft.NET.Build.Tasks/targets/Microsoft.NET.SupportedPlatforms.props) .</span><span class="sxs-lookup"><span data-stu-id="3c34a-138">**Doesn't warn** if you're building an app that doesn't target the unsupported platform or is multi-targeted and the platform is not included in the default [MSBuild `<SupportedPlatform>`](https://github.com/dotnet/sdk/blob/master/src/Tasks/Microsoft.NET.Build.Tasks/targets/Microsoft.NET.SupportedPlatforms.props) items group.</span></span>
- <span data-ttu-id="3c34a-139">Oba atrybuty mogą być tworzone z numerami wersji lub bez nich w ramach nazwy platformy.</span><span class="sxs-lookup"><span data-stu-id="3c34a-139">Both attributes can be instantiated with or without version numbers as part of the platform name.</span></span>
  - <span data-ttu-id="3c34a-140">Numery wersji są `major.minor[.build[.revision]]` `major.minor` wymagane, a `build` `revision` części i są opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="3c34a-140">Version numbers are in the format of `major.minor[.build[.revision]]`; `major.minor` is required and the `build` and `revision` parts are optional.</span></span> <span data-ttu-id="3c34a-141">Na przykład "system Windows 7.0" wskazuje system Windows w wersji 7,0, ale "Windows" jest interpretowany jako Windows 0,0.</span><span class="sxs-lookup"><span data-stu-id="3c34a-141">For example, "Windows7.0" indicates Windows version 7.0, but "Windows" is interpreted as Windows 0.0.</span></span>

<span data-ttu-id="3c34a-142">Aby uzyskać więcej informacji, zobacz [przykłady działania atrybutów i ich przyczyny](#examples-of-how-the-attributes-work-and-what-diagnostics-they-produce).</span><span class="sxs-lookup"><span data-stu-id="3c34a-142">For more information, see [examples of how the attributes work and what diagnostics they cause](#examples-of-how-the-attributes-work-and-what-diagnostics-they-produce).</span></span>

### <a name="advanced-scenarios-for-combining-attributes"></a><span data-ttu-id="3c34a-143">Zaawansowane scenariusze łączenia atrybutów</span><span class="sxs-lookup"><span data-stu-id="3c34a-143">Advanced scenarios for combining attributes</span></span>

- <span data-ttu-id="3c34a-144">Jeśli istnieją kombinacje `[SupportedOSPlatform]` i `[UnsupportedOSPlatform]` atrybuty, wszystkie atrybuty są pogrupowane według identyfikatora platformy systemu operacyjnego:</span><span class="sxs-lookup"><span data-stu-id="3c34a-144">If a combination of `[SupportedOSPlatform]` and `[UnsupportedOSPlatform]` attributes are present, all attributes are grouped by OS platform identifier:</span></span>
  - <span data-ttu-id="3c34a-145">**Tylko obsługiwana lista**.</span><span class="sxs-lookup"><span data-stu-id="3c34a-145">**Supported only list**.</span></span> <span data-ttu-id="3c34a-146">Jeśli najniższa wersja dla każdej platformy systemu operacyjnego jest `[SupportedOSPlatform]` atrybutem, interfejs API jest uznawany za obsługiwany przez wymienione platformy i nieobsługiwany przez wszystkie inne platformy.</span><span class="sxs-lookup"><span data-stu-id="3c34a-146">If the lowest version for each OS platform is a `[SupportedOSPlatform]` attribute, the API is considered to only be supported by the listed platforms and unsupported by all other platforms.</span></span> <span data-ttu-id="3c34a-147">Atrybuty opcjonalne `[UnsupportedOSPlatform]` dla każdej platformy mogą mieć tylko wyższą wersję minimalnej obsługiwanej wersji, co oznacza, że interfejs API zostanie usunięty od określonej wersji.</span><span class="sxs-lookup"><span data-stu-id="3c34a-147">The optional `[UnsupportedOSPlatform]` attributes for each platform can only have higher version of the minimum supported version, which denotes that the API is removed starting from the specified version.</span></span>

    ```csharp
    // The API only supported on Windows 8.0 and later, not supported for all other.
    // The API is removed/unsupported from version 10.0.19041.0.
    [SupportedOSPlatform("windows8.0")]
    [UnsupportedOSPlatform("windows10.0.19041.0")]
    public void ApiSupportedFromWindows80SupportFromCertainVersion();
    ```

  - <span data-ttu-id="3c34a-148">**Nieobsługiwana lista**.</span><span class="sxs-lookup"><span data-stu-id="3c34a-148">**Unsupported only list**.</span></span> <span data-ttu-id="3c34a-149">Jeśli najniższa wersja dla każdej platformy systemu operacyjnego jest `[UnsupportedOSPlatform]` atrybutem, interfejs API jest uznawany za nieobsługiwany przez wymienione platformy i obsługiwany przez wszystkie inne platformy.</span><span class="sxs-lookup"><span data-stu-id="3c34a-149">If the lowest version for each OS platform is an `[UnsupportedOSPlatform]` attribute, then the API is considered to only be unsupported by the listed platforms and supported by all other platforms.</span></span> <span data-ttu-id="3c34a-150">Lista może mieć `[SupportedOSPlatform]` atrybut o tej samej platformie, ale wyższej wersji, co oznacza, że interfejs API jest obsługiwany w tej wersji.</span><span class="sxs-lookup"><span data-stu-id="3c34a-150">The list could have `[SupportedOSPlatform]` attribute with the same platform but a higher version, which denotes that the API is supported starting from that version.</span></span>

    ```csharp
    // The API was unsupported on Windows until version 10.0.19041.0.
    // The API is considered supported everywhere else without constraints.
    [UnsupportedOSPlatform("windows")]
    [SupportedOSPlatform("windows10.0.19041.0")]
    public void ApiSupportedFromWindows8UnsupportFromWindows10();
    ```

  - <span data-ttu-id="3c34a-151">**Niespójna lista**.</span><span class="sxs-lookup"><span data-stu-id="3c34a-151">**Inconsistent list**.</span></span> <span data-ttu-id="3c34a-152">Jeśli najniższa wersja dla niektórych platform jest inna niż w przypadku `[SupportedOSPlatform]` `[UnsupportedOSPlatform]` innych platform, jest uważana za niespójną, co nie jest obsługiwane w przypadku analizatora.</span><span class="sxs-lookup"><span data-stu-id="3c34a-152">If the lowest version for some platforms is `[SupportedOSPlatform]` while it is `[UnsupportedOSPlatform]` for other platforms, it's considered to be inconsistent, which is not supported for the analyzer.</span></span>
  - <span data-ttu-id="3c34a-153">Jeśli najmniejsze wersje `[SupportedOSPlatform]` i `[UnsupportedOSPlatform]` atrybuty są równe, Analizator traktuje platformę jako część **obsługiwanej listy**.</span><span class="sxs-lookup"><span data-stu-id="3c34a-153">If the lowest versions of `[SupportedOSPlatform]` and `[UnsupportedOSPlatform]` attributes are equal, the analyzer considers the platform as part of the **Supported only list**.</span></span>
- <span data-ttu-id="3c34a-154">Atrybuty platformy można stosować do typów, elementów członkowskich (metod, pól, właściwości i zdarzeń) i zestawów z różnymi nazwami lub wersjami platform.</span><span class="sxs-lookup"><span data-stu-id="3c34a-154">Platform attributes can be applied to types, members (methods, fields, properties, and events) and assemblies with different platform names or versions.</span></span>
  - <span data-ttu-id="3c34a-155">Atrybuty zastosowane na najwyższym poziomie `target` mają wpływ na wszystkie jej składowe i typy.</span><span class="sxs-lookup"><span data-stu-id="3c34a-155">Attributes applied at the top level `target` affect all of its members and types.</span></span>
  - <span data-ttu-id="3c34a-156">Atrybuty na poziomie podrzędnym są stosowane tylko wtedy, gdy są zgodne z regułą "adnotacje potomne mogą zawęzić obsługę platform, ale nie mogą ich poszerzyć".</span><span class="sxs-lookup"><span data-stu-id="3c34a-156">Child-level attributes only apply if they adhere to the rule "child annotations can narrow the platforms support, but they cannot widen it".</span></span>
    - <span data-ttu-id="3c34a-157">Gdy element nadrzędny ma **obsługiwaną tylko** listę, a następnie podrzędne atrybuty elementu członkowskiego nie można dodać nowej obsługi platformy, ponieważ spowodowałoby to rozszerzenie obsługi nadrzędnej.</span><span class="sxs-lookup"><span data-stu-id="3c34a-157">When parent has **Supported only** list, then child member attributes cannot add a new platform support, as that would be extending parent support.</span></span> <span data-ttu-id="3c34a-158">Obsługę nowej platformy można dodać tylko do samego siebie.</span><span class="sxs-lookup"><span data-stu-id="3c34a-158">Support for a new platform can only be added to the parent itself.</span></span> <span data-ttu-id="3c34a-159">Ale element podrzędny może mieć `Supported` atrybut dla tej samej platformy z nowszymi wersjami, co zawęża pomoc techniczną.</span><span class="sxs-lookup"><span data-stu-id="3c34a-159">But the child can have the `Supported` attribute for the same platform with later versions as that narrows the support.</span></span> <span data-ttu-id="3c34a-160">Ponadto element podrzędny może mieć `Unsupported` atrybut o tej samej platformie, co umożliwia również zawężenie obsługi nadrzędnej.</span><span class="sxs-lookup"><span data-stu-id="3c34a-160">Also, the child can have the `Unsupported` attribute with the same platform as that also narrows parent support.</span></span>
    - <span data-ttu-id="3c34a-161">Gdy element nadrzędny ma **nieobsługiwaną** listę, wówczas atrybuty elementu członkowskiego podrzędnego mogą dodać obsługę nowej platformy, ponieważ powoduje to zawężenie obsługi nadrzędnej.</span><span class="sxs-lookup"><span data-stu-id="3c34a-161">When parent has **Unsupported only** list, then child member attributes can add support for a new platform, as that narrows parent support.</span></span> <span data-ttu-id="3c34a-162">Ale nie może mieć `Supported` atrybutu dla tej samej platformy, co element nadrzędny, ponieważ rozszerza obsługę elementu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="3c34a-162">But it cannot have the `Supported` attribute for the same platform as the parent, because that extends parent support.</span></span> <span data-ttu-id="3c34a-163">Obsługę tej samej platformy można dodać tylko do elementu nadrzędnego, w którym `Unsupported` zastosowano oryginalny atrybut.</span><span class="sxs-lookup"><span data-stu-id="3c34a-163">Support for the same platform can only be added to the parent where the original `Unsupported` attribute was applied.</span></span>
  - <span data-ttu-id="3c34a-164">Jeśli `[SupportedOSPlatform("platformVersion")]` zastosowano więcej niż jeden raz dla interfejsu API o tej samej `platform` nazwie, Analizator traktuje tylko ten element z minimalną wersją.</span><span class="sxs-lookup"><span data-stu-id="3c34a-164">If `[SupportedOSPlatform("platformVersion")]` is applied more than once for an API with the same `platform` name, the analyzer only considers the one with the minimum version.</span></span>
  - <span data-ttu-id="3c34a-165">Jeśli `[UnsupportedOSPlatform("platformVersion")]` zastosowano więcej niż dwa razy dla interfejsu API o tej samej `platform` nazwie, Analizator uwzględnia tylko dwa z najwcześniejszymi wersjami.</span><span class="sxs-lookup"><span data-stu-id="3c34a-165">If `[UnsupportedOSPlatform("platformVersion")]` is applied more than twice for an API with the same `platform` name, the analyzer only considers the two with the earliest versions.</span></span>

  > [!NOTE]
  > <span data-ttu-id="3c34a-166">Nie oczekuje się, że interfejs API, który był obsługiwany początkowo, ale nie jest obsługiwany (usunięty) w nowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="3c34a-166">An API that was supported initially but unsupported (removed) in a later version is not expected to get resupported in an even later version.</span></span>

### <a name="examples-of-how-the-attributes-work-and-what-diagnostics-they-produce"></a><span data-ttu-id="3c34a-167">Przykłady działania atrybutów i ich diagnostyki</span><span class="sxs-lookup"><span data-stu-id="3c34a-167">Examples of how the attributes work and what diagnostics they produce</span></span>

  ```csharp
  // An API supported only on Windows.
  [SupportedOSPlatform("Windows")]
  public void WindowsOnlyApi() { }

  // an API supported on Windows and Linux.
  [SupportedOSPlatform("Windows")]
  [SupportedOSPlatform("Linux")]
  public void SupportedOnWindowsAndLinuxOnly() { }

  // an API only supported on Windows 8.0 and later, not supported for all other.
  // an API is removed/unsupported from version 10.0.19041.0.
  [SupportedOSPlatform("windows8.0")]
  [UnsupportedOSPlatform("windows10.0.19041.0")]
  public void ApiSupportedFromWindows8UnsupportFromWindows10() { }

  // an Assembly supported on Windows, the API added from version 10.0.19041.0.
  [assembly: SupportedOSPlatform("Windows")]
  [SupportedOSPlatform("windows10.0.19041.0")]
  public void AssemblySupportedOnWindowsApiSupportedFromWindows10() { }

  public void Caller()
  {
      WindowsOnlyApi(); // warns: 'WindowsOnlyApi' is supported on 'windows'

      // warns: 'SupportedOnWindowsAndLinuxOnly' is supported on 'Windows'
      // warns: 'SupportedOnWindowsAndLinuxOnly' is supported on 'Linux'
      SupportedOnWindowsAndLinuxOnly();

      // warns: 'ApiSupportedFromWindows8UnsupportFromWindows10' is supported on 'windows' 8.0 and later
      // warns: 'ApiSupportedFromWindows8UnsupportFromWindows10' is unsupported on 'windows' 10.0.19041.0 and later
      ApiSupportedFromWindows8UnsupportFromWindows10();

      // warns: 'ApiSupportedFromWindows8UnsupportFromWindows10' is supported on 'windows' 10.0.19041.0 and later
      // for same platform analyzer only warn for the latest version.
      AssemblySupportedOnWindowsApiSupportedFromWindows10();
  }

  // an API not supported on android but supported on all other.
  [UnsupportedOSPlatform("android")]
  public void DoesNotWorkOnAndroid() { }

  // an API was unsupported on Windows until version 8.0.
  // The API is considered supported everywhere else without constraints.
  [UnsupportedOSPlatform("windows")]
  [SupportedOSPlatform("windows8.0")]
  public void StartedWindowsSupportFromVersion8() { }

  // an API was unsupported on Windows until version8.0.
  // Then the API is removed (unsupported) from version 10.0.19041.0.
  // The API is considered supported everywhere else without constraints.
  [UnsupportedOSPlatform("windows")]
  [SupportedOSPlatform("windows8.0")]
  [UnsupportedOSPlatform("windows10.0.19041.0")]
  public void StartedWindowsSupportFrom8UnsupportedFrom10() { }

  public void Caller2()
  {
      DoesNotWorkOnAndroid(); // warns 'DoesNotWorkOnAndroid' is unsupported on 'android'

      // warns:'StartedWindowsSupportFromVersion8' is unsupported on 'windows'
      // warns:'StartedWindowsSupportFromVersion8' is supported on 'windows' 8.0 and later
      StartedWindowsSupportFromVersion8();

      // warns:'StartedWindowsSupportFrom8UnsupportedFrom10' is unsupported on 'windows'
      // warns:'StartedWindowsSupportFrom8UnsupportedFrom10' is supported on 'windows' 8.0 and later
      // even there were 3 diagnostics found analyzer warn only for the first 2.
      StartedWindowsSupportFrom8UnsupportedFrom10();
  }
  ```

## <a name="handle-reported-warnings"></a><span data-ttu-id="3c34a-168">Obsługa ostrzeżeń raportowanych</span><span class="sxs-lookup"><span data-stu-id="3c34a-168">Handle reported warnings</span></span>

<span data-ttu-id="3c34a-169">Zalecanym sposobem postępowania z tą diagnostyką jest upewnienie się, że interfejsy API specyficzne dla platformy są wywoływane tylko w przypadku uruchamiania na odpowiedniej platformie.</span><span class="sxs-lookup"><span data-stu-id="3c34a-169">The recommended way to deal with these diagnostics is to make sure you only call platform-specific APIs when running on an appropriate platform.</span></span> <span data-ttu-id="3c34a-170">Poniżej przedstawiono opcje, których można użyć do rozwiązywania ostrzeżeń; Wybierz opcję, która jest najbardziej odpowiednia dla danej sytuacji:</span><span class="sxs-lookup"><span data-stu-id="3c34a-170">Following are the options you can use to address the warnings; choose whichever is most appropriate for your situation:</span></span>

- <span data-ttu-id="3c34a-171">**Ochrona wywołania**.</span><span class="sxs-lookup"><span data-stu-id="3c34a-171">**Guard the call**.</span></span> <span data-ttu-id="3c34a-172">Można to osiągnąć, warunkowo wywołując kod w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="3c34a-172">You can achieve this by conditionally calling the code at run time.</span></span> <span data-ttu-id="3c34a-173">Sprawdź, czy pracujesz w żądanym `Platform` miejscu przy użyciu jednej z metod sprawdzania platformy, na przykład `OperatingSystem.Is<Platform>()` lub `OperatingSystem.Is<Platform>VersionAtLeast(int major, int minor = 0, int build = 0, int revision = 0)` .</span><span class="sxs-lookup"><span data-stu-id="3c34a-173">Check whether you're running on a desired `Platform` by using one of platform-check methods, for example, `OperatingSystem.Is<Platform>()` or `OperatingSystem.Is<Platform>VersionAtLeast(int major, int minor = 0, int build = 0, int revision = 0)`.</span></span>

- <span data-ttu-id="3c34a-174">**Oznacz lokację wywołania jako specyficzną dla platformy**.</span><span class="sxs-lookup"><span data-stu-id="3c34a-174">**Mark the call site as platform-specific**.</span></span> <span data-ttu-id="3c34a-175">Możesz także oznaczyć własne interfejsy API jako charakterystyczne dla danej platformy, co skutecznie tylko przekazuje wymagania do obiektów wywołujących.</span><span class="sxs-lookup"><span data-stu-id="3c34a-175">You can also choose to mark your own APIs as being platform-specific, thus effectively just forwarding the requirements to your callers.</span></span> <span data-ttu-id="3c34a-176">Oznacz zawierającą metodę lub typ lub cały zestaw z tymi samymi atrybutami, co odwołanie zależne od platformy.</span><span class="sxs-lookup"><span data-stu-id="3c34a-176">Mark the containing method or type or the entire assembly with the same attributes as the referenced platform-dependent call.</span></span> <span data-ttu-id="3c34a-177">[Przykłady](#mark-call-site-as-platform-specific).</span><span class="sxs-lookup"><span data-stu-id="3c34a-177">[Examples](#mark-call-site-as-platform-specific).</span></span>

- <span data-ttu-id="3c34a-178">**Potwierdź witrynę wywołania przy użyciu sprawdzenia platformy**.</span><span class="sxs-lookup"><span data-stu-id="3c34a-178">**Assert the call site with platform check**.</span></span> <span data-ttu-id="3c34a-179">Jeśli nie chcesz obciążać dodatkowej `if` instrukcji w czasie wykonywania, użyj <xref:System.Diagnostics.Debug.Assert(System.Boolean)?displayProperty=nameWithType> .</span><span class="sxs-lookup"><span data-stu-id="3c34a-179">If you don't want the overhead of an additional `if` statement at run time, use <xref:System.Diagnostics.Debug.Assert(System.Boolean)?displayProperty=nameWithType>.</span></span> <span data-ttu-id="3c34a-180">[Przykład](#assert-the-call-site-with-platform-check).</span><span class="sxs-lookup"><span data-stu-id="3c34a-180">[Example](#assert-the-call-site-with-platform-check).</span></span>

- <span data-ttu-id="3c34a-181">**Usuń kod**.</span><span class="sxs-lookup"><span data-stu-id="3c34a-181">**Delete the code**.</span></span> <span data-ttu-id="3c34a-182">Na ogół nie jest to potrzebne, ponieważ oznacza to utratę wierności, gdy kod jest używany przez użytkowników systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="3c34a-182">Generally not what you want because it means you lose fidelity when your code is used by Windows users.</span></span> <span data-ttu-id="3c34a-183">W przypadku, gdy istnieje alternatywa dla wielu platform, najlepiej jest ją używać w przypadku interfejsów API specyficznych dla platformy.</span><span class="sxs-lookup"><span data-stu-id="3c34a-183">For cases where a cross-platform alternative exists, you're likely better off using that over platform-specific APIs.</span></span>

- <span data-ttu-id="3c34a-184">**Pomiń ostrzeżenie**.</span><span class="sxs-lookup"><span data-stu-id="3c34a-184">**Suppress the warning**.</span></span> <span data-ttu-id="3c34a-185">Możesz również po prostu pominąć ostrzeżenie za pośrednictwem wpisu EditorConfig lub `#pragma warning disable ca1416` .</span><span class="sxs-lookup"><span data-stu-id="3c34a-185">You can also simply suppress the warning, either via an EditorConfig entry or `#pragma warning disable ca1416`.</span></span> <span data-ttu-id="3c34a-186">Jednak ta opcja powinna być ostatnią możliwością w przypadku korzystania z interfejsów API specyficznych dla platformy.</span><span class="sxs-lookup"><span data-stu-id="3c34a-186">However, this option should be a last resort when using platform-specific APIs.</span></span>

### <a name="guard-platform-specific-apis-with-guard-methods"></a><span data-ttu-id="3c34a-187">Ochrona interfejsów API specyficznych dla platformy przy użyciu metod Guard</span><span class="sxs-lookup"><span data-stu-id="3c34a-187">Guard platform-specific APIs with guard methods</span></span>

<span data-ttu-id="3c34a-188">Nazwa platformy metody Guard powinna być zgodna z nazwą platformy interfejsu API zależnej od platformy wywołującej.</span><span class="sxs-lookup"><span data-stu-id="3c34a-188">The guard method's platform name should match with the calling platform-dependent API platform name.</span></span> <span data-ttu-id="3c34a-189">Jeśli ciąg platformy wywołującego interfejsu API zawiera wersję:</span><span class="sxs-lookup"><span data-stu-id="3c34a-189">If the platform string of the calling API includes the version:</span></span>

- <span data-ttu-id="3c34a-190">Dla `[SupportedOSPlatform("platformVersion")]` atrybutu platforma metody Guard `version` powinna być większa lub równa platformie wywołującej `Version` .</span><span class="sxs-lookup"><span data-stu-id="3c34a-190">For the `[SupportedOSPlatform("platformVersion")]` attribute, the guard method platform `version` should be greater than or equal to the calling platform's `Version`.</span></span>
- <span data-ttu-id="3c34a-191">Dla `[UnsupportedOSPlatform("platformVersion")]` atrybutu platforma metody Guard `version` powinna być mniejsza lub równa platformie wywołującej `Version` .</span><span class="sxs-lookup"><span data-stu-id="3c34a-191">For the `[UnsupportedOSPlatform("platformVersion")]` attribute, the guard method's platform `version` should be less than or equal to the calling platform's `Version`.</span></span>

  ```csharp
  public void CallingSupportedOnlyApis() // Allow list calls
  {
      if (OperatingSystem.IsWindows())
      {
          WindowsOnlyApi(); // will not warn
      }

      if (OperatingSystem.IsLinux())
      {
          SupportedOnWindowsAndLinuxOnly(); // will not warn, within one of the supported context
      }

      // Can use &&, || logical operators to guard combined attributes
      if (OperatingSystem.IsWindowsVersionAtLeast(8) && !OperatingSystem.IsWindowsVersionAtLeast(10.0.19041)))
      {
          ApiSupportedFromWindows8UnsupportFromWindows10();
      }

      if (OperatingSystem.IsWindowsVersionAtLeast(10, 0, 1903))
      {
          AssemblySupportedOnWindowsApiSupportedFromWindows10(); // Only need to check latest supported version
      }
  }

  public void CallingUnsupportedApis()
  {
      if (!OperatingSystem.IsAndroid())
      {
          DoesNotWorkOnAndroid(); // will not warn
      }

      if (!OperatingSystem.IsWindows() || OperatingSystem.IsWindowsVersionAtLeast(8))
      {
          StartedWindowsSupportFromVersion8(); // will not warn
      }

      if (!OperatingSystem.IsWindows() || // supported all other platforms
         (OperatingSystem.IsWindowsVersionAtLeast(8) && !OperatingSystem.IsWindowsVersionAtLeast(10, 0, 1903)))
      {
          StartedWindowsSupportFrom8UnsupportedFrom10(); // will not warn
      }
  }
  ```

- <span data-ttu-id="3c34a-192">Jeśli musisz zabezpieczyć kod, którego dotyczy `netstandard` lub `netcoreapp` gdzie nowe <xref:System.OperatingSystem> interfejsy API nie są dostępne, <xref:System.Runtime.InteropServices.RuntimeInformation.IsOSPlatform%2A?displayProperty=nameWithType> można użyć interfejsu API i będzie on przestrzegany przez analizator.</span><span class="sxs-lookup"><span data-stu-id="3c34a-192">If you need to guard code that targets `netstandard` or `netcoreapp` where new <xref:System.OperatingSystem> APIs are not available, the <xref:System.Runtime.InteropServices.RuntimeInformation.IsOSPlatform%2A?displayProperty=nameWithType> API can be used and will be respected by the analyzer.</span></span> <span data-ttu-id="3c34a-193">Ale nie jest tak zoptymalizowany jak nowe interfejsy API dodane w programie <xref:System.OperatingSystem> .</span><span class="sxs-lookup"><span data-stu-id="3c34a-193">But it's not as optimized as the new APIs added in <xref:System.OperatingSystem>.</span></span> <span data-ttu-id="3c34a-194">Jeśli platforma nie jest obsługiwana w <xref:System.Runtime.InteropServices.OSPlatform> strukturze, można wywołać metodę <xref:System.Runtime.InteropServices.OSPlatform.Create(System.String)?displayProperty=nameWithType> i przekazać ją do nazwy platformy, która również odnosi się do analizatora.</span><span class="sxs-lookup"><span data-stu-id="3c34a-194">If the platform is not supported in the <xref:System.Runtime.InteropServices.OSPlatform> struct, you can call <xref:System.Runtime.InteropServices.OSPlatform.Create(System.String)?displayProperty=nameWithType> and pass in the platform name, which the analyzer also respects.</span></span>

  ```csharp
  public void CallingSupportedOnlyApis()
  {
      if (RuntimeInformation.IsOSPlatform(OSPlatform.Windows))
      {
          SupportedOnWindowsAndLinuxOnly(); // will not warn
      }

      if (RuntimeInformation.IsOSPlatform(OSPlatform.Create("browser")))
      {
          ApiOnlySupportedOnBrowser(); // call of browser specific API
      }
  }
  ```

### <a name="mark-call-site-as-platform-specific"></a><span data-ttu-id="3c34a-195">Oznacz lokację wywołania jako specyficzną dla platformy</span><span class="sxs-lookup"><span data-stu-id="3c34a-195">Mark call site as platform-specific</span></span>

<span data-ttu-id="3c34a-196">Nazwy platform powinny być zgodne z interfejsem API zależnym od platformy wywołującej.</span><span class="sxs-lookup"><span data-stu-id="3c34a-196">Platform names should match the calling platform-dependent API.</span></span> <span data-ttu-id="3c34a-197">Jeśli ciąg platformy zawiera wersję:</span><span class="sxs-lookup"><span data-stu-id="3c34a-197">If the platform string includes a version:</span></span>

- <span data-ttu-id="3c34a-198">Dla `[SupportedOSPlatform("platformVersion")]` atrybutu platforma lokacji wywołania `version` powinna być większa lub równa platformie wywołującej `Version`</span><span class="sxs-lookup"><span data-stu-id="3c34a-198">For the `[SupportedOSPlatform("platformVersion")]` attribute, the call site platform `version` should be greater than or equal to the calling platform's `Version`</span></span>
- <span data-ttu-id="3c34a-199">Dla `[UnsupportedOSPlatform("platformVersion")]` atrybutu platforma lokacji wywołania `version` powinna być mniejsza lub równa platformie wywołującej `Version`</span><span class="sxs-lookup"><span data-stu-id="3c34a-199">For the `[UnsupportedOSPlatform("platformVersion")]` attribute, the call site platform `version` should be less than or equal to the calling platform's `Version`</span></span>

  ```csharp
  // an API supported only on Windows.
  [SupportedOSPlatform("windows")]
  public void WindowsOnlyApi() { }

  // an API supported on Windows and Linux.
  [SupportedOSPlatform("Windows")]
  [SupportedOSPlatform("Linux")]
  public void SupportedOnWindowsAndLinuxOnly() { }

  // an API only supported on Windows 8.0 and later, not supported for all other.
  // an API is removed/unsupported from version 10.0.19041.0.
  [SupportedOSPlatform("windows8.0")]
  [UnsupportedOSPlatform("windows10.0.19041.0")]
  public void ApiSupportedFromWindows8UnsupportFromWindows10() { }

  // an Assembly supported on Windows, the API added from version 10.0.19041.0.
  [assembly: SupportedOSPlatform("Windows")]
  [SupportedOSPlatform("windows10.0.19041.0")]
  public void AssemblySupportedOnWindowsApiSupportedFromWindows10() { }

  [SupportedOSPlatform("windows8.0")] // call site attributed Windows 8.0 or above.
  public void Caller()
  {
      WindowsOnlyApi(); // will not warn as call site is for Windows.

      // will not warn as call site is for Windows.
      SupportedOnWindowsAndLinuxOnly();

      // will not warn for the API's [SupportedOSPlatform("windows8.0")] attribute.
      // Warns: 'ApiSupportedFromWindows8UnsupportFromWindows10' is unsupported on 'windows' 10.0.19041.0 and later
      ApiSupportedFromWindows8UnsupportFromWindows10();

      // warns: 'ApiSupportedFromWindows8UnsupportFromWindows10' is supported on 'windows' 10.0.19041.0 and later
      // as the call site version is lower than calling version.
      AssemblySupportedOnWindowsApiSupportedFromWindows10();
  }

  [SupportedOSPlatform("windows11.0")] // call site attributed with windows 11.0 or above.
  public void Caller2()
  {
      // Warns: 'ApiSupportedFromWindows8UnsupportFromWindows10' is unsupported on 'windows' 10.0.19041.0 and later
      ApiSupportedFromWindows8UnsupportFromWindows10();

      // will not warn as call site version higher than calling API.
      AssemblySupportedOnWindowsApiSupportedFromWindows10();
  }

  [SupportedOSPlatform("windows8.0")]
  [UnsupportedOSPlatform("windows10.0.19041.0")] // call site supports Windows from version 8.0 to 10.0.19041.0.
  public void Caller3()
  {
      // will not warn as caller has exact same attributes.
      ApiSupportedFromWindows8UnsupportFromWindows10();

      // Warns: 'ApiSupportedFromWindows8UnsupportFromWindows10' is supported on 'windows' 10.0.19041.0 and later
      // As call site stopped support from that version.
      AssemblySupportedOnWindowsApiSupportedFromWindows10();
  }

  // an API not supported on Android but supported on all other.
  [UnsupportedOSPlatform("android")]
  public void DoesNotWorkOnAndroid() { }

  // an API was unsupported on Windows until version 8.0.
  // The API is considered supported everywhere else without constraints.
  [UnsupportedOSPlatform("windows")]
  [SupportedOSPlatform("windows8.0")]
  public void StartedWindowsSupportFromVersion8() { }

  // an API was unsupported on Windows until version8.0.
  // Then the API is removed (unsupported) from version 10.0.19041.0.
  // The API is considered supported everywhere else without constraints.
  [UnsupportedOSPlatform("windows")]
  [SupportedOSPlatform("windows8.0")]
  [UnsupportedOSPlatform("windows10.0.19041.0")]
  public void StartedWindowsSupportFrom8UnsupportedFrom10() { }

  [UnsupportedOSPlatform("windows")] // Caller no support Windows for any version.
  public void Caller4()
  {
      DoesNotWorkOnAndroid(); // warns 'DoesNotWorkOnAndroid' is unsupported on 'Android'.

      // will not warns as the call site not support Windows at all, but supports all other.
      StartedWindowsSupportFromVersion8();

      // same, will not warns as the call site not support Windows at all, but supports all other.
      StartedWindowsSupportFrom8UnsupportedFrom10();
  }

  [UnsupportedOSPlatform("windows")]
  [UnsupportedOSPlatform("android")] // Caller not support Windows and Android for any version.
  public void Caller4()
  {
      DoesNotWorkOnAndroid(); // will not warn as call site not supports Android.

      // will not warns as the call site not support Windows at all, but supports all other.
      StartedWindowsSupportFromVersion8();

      // same, will not warns as the call site not support Windows at all, but supports all other.
      StartedWindowsSupportFrom8UnsupportedFrom10();
  }
  ```

### <a name="assert-the-call-site-with-platform-check"></a><span data-ttu-id="3c34a-200">Zapoznaj się z sprawdzeniem połączenia z platformą</span><span class="sxs-lookup"><span data-stu-id="3c34a-200">Assert the call-site with platform check</span></span>

<span data-ttu-id="3c34a-201">Jako warunek dla programu można również użyć wszystkich testów warunkowych użytych w [przykładach funkcji ochrony platformy](#guard-platform-specific-apis-with-guard-methods) <xref:System.Diagnostics.Debug.Assert(System.Boolean)?displayProperty=nameWithType> .</span><span class="sxs-lookup"><span data-stu-id="3c34a-201">All the conditional checks used in the [platform guard examples](#guard-platform-specific-apis-with-guard-methods) can also be used as the condition for <xref:System.Diagnostics.Debug.Assert(System.Boolean)?displayProperty=nameWithType>.</span></span>

  ```csharp
  // An API supported only on Linux.
  [SupportedOSPlatform("linux")]
  public void LinuxOnlyApi() { }

  public void Caller()
  {
      Debug.Assert(OperatingSystem.IsLinux());

      LinuxOnlyApi(); // will not warn
  }
  ```

## <a name="see-also"></a><span data-ttu-id="3c34a-202">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="3c34a-202">See also</span></span>

- [<span data-ttu-id="3c34a-203">Nazwy platformy docelowej w programie .NET 5</span><span class="sxs-lookup"><span data-stu-id="3c34a-203">Target Framework Names in .NET 5</span></span>](https://github.com/dotnet/designs/blob/master/accepted/2020/net5/net5.md)
- [<span data-ttu-id="3c34a-204">Dodawanie adnotacji do interfejsów API specyficznych dla platformy i wykrywanie ich użycia</span><span class="sxs-lookup"><span data-stu-id="3c34a-204">Annotating platform-specific APIs and detecting its use</span></span>](https://github.com/dotnet/designs/blob/master/accepted/2020/platform-checks/platform-checks.md)
- [<span data-ttu-id="3c34a-205">Dodawanie adnotacji do interfejsów API jako nieobsługiwanych na określonych platformach</span><span class="sxs-lookup"><span data-stu-id="3c34a-205">Annotating APIs as unsupported on specific platforms</span></span>](https://github.com/dotnet/designs/blob/master/accepted/2020/platform-exclusion/platform-exclusion.md)
- [<span data-ttu-id="3c34a-206">Analizator zgodności platformy CA1416</span><span class="sxs-lookup"><span data-stu-id="3c34a-206">CA1416 Platform compatibility analyzer</span></span>](../../fundamentals/code-analysis/quality-rules/ca1416.md)
- [<span data-ttu-id="3c34a-207">Analizator interfejsów API platformy .NET</span><span class="sxs-lookup"><span data-stu-id="3c34a-207">.NET API analyzer</span></span>](../../standard/analyzers/api-analyzer.md)
