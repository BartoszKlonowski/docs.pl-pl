---
title: Ukierunkowane na wiele platform dla bibliotek platformy .NET
description: Zalecenia dotyczące najlepszych rozwiązań dotyczących tworzenia bibliotek platformy .NET dla wielu platform.
ms.date: 08/12/2019
ms.openlocfilehash: 038a03904c4cfe49758562b5748fef06ae1afa4b
ms.sourcegitcommit: 7588b1f16b7608bc6833c05f91ae670c22ef56f8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/02/2020
ms.locfileid: "93189254"
---
# <a name="cross-platform-targeting"></a><span data-ttu-id="92e9b-103">Obsługiwane rozwiązania międzyplatformowe</span><span class="sxs-lookup"><span data-stu-id="92e9b-103">Cross-platform targeting</span></span>

<span data-ttu-id="92e9b-104">Nowoczesne środowisko .NET obsługuje wiele systemów operacyjnych i urządzeń.</span><span class="sxs-lookup"><span data-stu-id="92e9b-104">Modern .NET supports multiple operating systems and devices.</span></span> <span data-ttu-id="92e9b-105">Jest to ważne w przypadku bibliotek typu open source programu .NET do obsługi możliwie największej liczby deweloperów, niezależnie od tego, czy tworzą one witrynę sieci Web ASP.NET hostowaną na platformie Azure, czy też grę z platformą .NET w środowisku Unity.</span><span class="sxs-lookup"><span data-stu-id="92e9b-105">It's important for .NET open-source libraries to support as many developers as possible, whether they're building an ASP.NET website hosted in Azure, or a .NET game in Unity.</span></span>

## <a name="net-standard"></a><span data-ttu-id="92e9b-106">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="92e9b-106">.NET Standard</span></span>

<span data-ttu-id="92e9b-107">.NET Standard to najlepszy sposób na dodanie obsługi wielu platform do biblioteki .NET.</span><span class="sxs-lookup"><span data-stu-id="92e9b-107">.NET Standard is the best way to add cross-platform support to a .NET library.</span></span> <span data-ttu-id="92e9b-108">[.NET Standard](../net-standard.md) to specyfikacja interfejsów API platformy .NET, które są dostępne we wszystkich implementacjach platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="92e9b-108">[.NET Standard](../net-standard.md) is a specification of .NET APIs that are available on all .NET implementations.</span></span> <span data-ttu-id="92e9b-109">.NET Standard określania wartości docelowej umożliwia tworzenie bibliotek, które są ograniczone do używania interfejsów API w danej wersji .NET Standard, co oznacza, że są one używane przez wszystkie platformy, które implementują tę wersję .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="92e9b-109">Targeting .NET Standard lets you produce libraries that are constrained to use APIs that are in a given version of .NET Standard, which means it's usable by all platforms that implement that version of .NET Standard.</span></span>

<span data-ttu-id="92e9b-110">![.NET Standard](./media/cross-platform-targeting/platforms-netstandard.png ".NET Standard")</span><span class="sxs-lookup"><span data-stu-id="92e9b-110">![.NET Standard](./media/cross-platform-targeting/platforms-netstandard.png ".NET Standard")</span></span>

<span data-ttu-id="92e9b-111">Kierowanie .NET Standard i pomyślne skompilowanie projektu nie gwarantuje, że biblioteka zostanie uruchomiona pomyślnie na wszystkich platformach:</span><span class="sxs-lookup"><span data-stu-id="92e9b-111">Targeting .NET Standard, and successfully compiling your project, doesn't guarantee the library will run successfully on all platforms:</span></span>

1. <span data-ttu-id="92e9b-112">Interfejsy API specyficzne dla platformy zakończą się niepowodzeniem na innych platformach.</span><span class="sxs-lookup"><span data-stu-id="92e9b-112">Platform-specific APIs will fail on other platforms.</span></span> <span data-ttu-id="92e9b-113">Na przykład program <xref:Microsoft.Win32.Registry?displayProperty=nameWithType> powróci do systemu Windows i zgłosi się <xref:System.PlatformNotSupportedException> w przypadku użycia w innym systemie operacyjnym.</span><span class="sxs-lookup"><span data-stu-id="92e9b-113">For example, <xref:Microsoft.Win32.Registry?displayProperty=nameWithType> will succeed on Windows and throw <xref:System.PlatformNotSupportedException> when used on any other OS.</span></span>
2. <span data-ttu-id="92e9b-114">Interfejsy API mogą zachowywać się inaczej.</span><span class="sxs-lookup"><span data-stu-id="92e9b-114">APIs can behave differently.</span></span> <span data-ttu-id="92e9b-115">Na przykład interfejsy API odbicia mają różne charakterystyki wydajności, gdy aplikacja korzysta z kompilacji przed czasem w systemie iOS lub platformy UWP.</span><span class="sxs-lookup"><span data-stu-id="92e9b-115">For example, reflection APIs have different performance characteristics when an application uses ahead-of-time compilation on iOS or UWP.</span></span>

> [!TIP]
> <span data-ttu-id="92e9b-116">Zespół .NET [oferuje Analizator Roslyn](../analyzers/api-analyzer.md) , który ułatwia odnajdywanie potencjalnych problemów.</span><span class="sxs-lookup"><span data-stu-id="92e9b-116">The .NET team [offers a Roslyn analyzer](../analyzers/api-analyzer.md) to help you discover possible issues.</span></span>

<span data-ttu-id="92e9b-117">✔️ Zacznij od uwzględnienia `netstandard2.0` celu.</span><span class="sxs-lookup"><span data-stu-id="92e9b-117">✔️ DO start with including a `netstandard2.0` target.</span></span>

> <span data-ttu-id="92e9b-118">Większość bibliotek ogólnego przeznaczenia nie powinna potrzebować interfejsów API poza .NET Standard 2,0.</span><span class="sxs-lookup"><span data-stu-id="92e9b-118">Most general-purpose libraries should not need APIs outside of .NET Standard 2.0.</span></span> <span data-ttu-id="92e9b-119">.NET Standard 2,0 jest obsługiwane przez wszystkie nowoczesne platformy i jest zalecanym sposobem obsługi wielu platform z jednym obiektem docelowym.</span><span class="sxs-lookup"><span data-stu-id="92e9b-119">.NET Standard 2.0 is supported by all modern platforms and is the recommended way to support multiple platforms with one target.</span></span>

<span data-ttu-id="92e9b-120">❌ Należy unikać uwzględniania `netstandard1.x` celu.</span><span class="sxs-lookup"><span data-stu-id="92e9b-120">❌ AVOID including a `netstandard1.x` target.</span></span>

> <span data-ttu-id="92e9b-121">.NET Standard 1. x jest dystrybuowany jako szczegółowy zestaw pakietów NuGet, co tworzy wykres zależności pakietu i umożliwia deweloperom pobieranie dużej liczby pakietów podczas kompilowania.</span><span class="sxs-lookup"><span data-stu-id="92e9b-121">.NET Standard 1.x is distributed as a granular set of NuGet packages, which creates a large package dependency graph and results in developers downloading a lot of packages when building.</span></span> <span data-ttu-id="92e9b-122">Nowoczesne implementacje platformy .NET obsługują .NET Standard 2,0.</span><span class="sxs-lookup"><span data-stu-id="92e9b-122">Modern .NET implementations support .NET Standard 2.0.</span></span> <span data-ttu-id="92e9b-123">Należy określić tylko .NET Standard 1. x, jeśli konieczne jest ukierunkowanie starszej platformy.</span><span class="sxs-lookup"><span data-stu-id="92e9b-123">You should only target .NET Standard 1.x if you specifically need to target an older platform.</span></span>

<span data-ttu-id="92e9b-124">✔️ Uwzględnij `netstandard2.0` element docelowy, jeśli jest wymagany `netstandard1.x` element docelowy.</span><span class="sxs-lookup"><span data-stu-id="92e9b-124">✔️ DO include a `netstandard2.0` target if you require a `netstandard1.x` target.</span></span>

> <span data-ttu-id="92e9b-125">Wszystkie platformy obsługujące .NET Standard 2,0 będą używać `netstandard2.0` elementu docelowego i korzyści z posiadania mniejszego grafu pakietu, a starsze platformy będą nadal działały i powracają do korzystania z `netstandard1.x` miejsca docelowego.</span><span class="sxs-lookup"><span data-stu-id="92e9b-125">All platforms supporting .NET Standard 2.0 will use the `netstandard2.0` target and benefit from having a smaller package graph while older platforms will still work and fall back to using the `netstandard1.x` target.</span></span>

<span data-ttu-id="92e9b-126">❌ Nie dodawaj elementu docelowego .NET Standard, jeśli biblioteka korzysta z modelu aplikacji specyficznego dla platformy.</span><span class="sxs-lookup"><span data-stu-id="92e9b-126">❌ DO NOT include a .NET Standard target if the library relies on a platform-specific app model.</span></span>

> <span data-ttu-id="92e9b-127">Na przykład biblioteka zestawu narzędzi platformy UWP Control zależy od modelu aplikacji, który jest dostępny tylko w platformy UWP.</span><span class="sxs-lookup"><span data-stu-id="92e9b-127">For example, a UWP control toolkit library depends on an app model that is only available on UWP.</span></span> <span data-ttu-id="92e9b-128">Interfejsy API specyficzne dla modelu aplikacji nie będą dostępne w .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="92e9b-128">App model specific APIs will not be available in .NET Standard.</span></span>

## <a name="multi-targeting"></a><span data-ttu-id="92e9b-129">Wiele elementów docelowych</span><span class="sxs-lookup"><span data-stu-id="92e9b-129">Multi-targeting</span></span>

<span data-ttu-id="92e9b-130">Czasami trzeba uzyskać dostęp do interfejsów API specyficznych dla platformy z bibliotek.</span><span class="sxs-lookup"><span data-stu-id="92e9b-130">Sometimes you need to access framework-specific APIs from your libraries.</span></span> <span data-ttu-id="92e9b-131">Najlepszym sposobem wywołania interfejsów API specyficznych dla platformy jest użycie wielu elementów docelowych, które kompilują projekt dla wielu platform [docelowych .NET](../frameworks.md) , a nie tylko dla jednego.</span><span class="sxs-lookup"><span data-stu-id="92e9b-131">The best way to call framework-specific APIs is using multi-targeting, which builds your project for many [.NET target frameworks](../frameworks.md) rather than for just one.</span></span>

<span data-ttu-id="92e9b-132">Aby chronić odbiorców przed koniecznością kompilowania dla poszczególnych platform, należy dążyć do uzyskania .NET Standard danych wyjściowych i jednego lub kilku wyjść specyficznych dla platformy.</span><span class="sxs-lookup"><span data-stu-id="92e9b-132">To shield your consumers from having to build for individual frameworks, you should strive to have a .NET Standard output plus one or more framework-specific outputs.</span></span> <span data-ttu-id="92e9b-133">W przypadku wiele elementów docelowych wszystkie zestawy są pakowane w ramach jednego pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="92e9b-133">With multi-targeting, all assemblies are packaged inside a single NuGet package.</span></span> <span data-ttu-id="92e9b-134">Następnie konsumenci mogą odwoływać się do tego samego pakietu, a pakiet NuGet wybierze odpowiednią implementację.</span><span class="sxs-lookup"><span data-stu-id="92e9b-134">Consumers can then reference the same package and NuGet will pick the appropriate implementation.</span></span> <span data-ttu-id="92e9b-135">Biblioteka .NET Standard służy jako biblioteka rezerwowa używana wszędzie, z wyjątkiem przypadków, w których pakiet NuGet oferuje implementację specyficzną dla platformy.</span><span class="sxs-lookup"><span data-stu-id="92e9b-135">Your .NET Standard library serves as the fallback library that is used everywhere, except for the cases where your NuGet package offers a framework-specific implementation.</span></span> <span data-ttu-id="92e9b-136">Wiele elementów docelowych umożliwia użycie kompilacji warunkowej w kodzie i wywołań interfejsów API specyficznych dla platformy.</span><span class="sxs-lookup"><span data-stu-id="92e9b-136">Multi-targeting allows you to use conditional compilation in your code and call framework-specific APIs.</span></span>

<span data-ttu-id="92e9b-137">![Pakiet NuGet z wieloma zestawami](./media/cross-platform-targeting/nuget-package-multiple-assemblies.png "Pakiet NuGet z wieloma zestawami")</span><span class="sxs-lookup"><span data-stu-id="92e9b-137">![NuGet package with multiple assemblies](./media/cross-platform-targeting/nuget-package-multiple-assemblies.png "NuGet package with multiple assemblies")</span></span>

<span data-ttu-id="92e9b-138">✔️ Rozważ uwzględnienie implementacji platformy .NET oprócz .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="92e9b-138">✔️ CONSIDER targeting .NET implementations in addition to .NET Standard.</span></span>

> <span data-ttu-id="92e9b-139">Elementy docelowe implementacji platformy .NET umożliwiają wywoływanie interfejsów API specyficznych dla platformy, które znajdują się poza programem .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="92e9b-139">Targeting .NET implementations allows you to call platform-specific APIs that are outside of .NET Standard.</span></span>
>
> <span data-ttu-id="92e9b-140">Nie porzucaj obsługi .NET Standard, gdy to zrobisz.</span><span class="sxs-lookup"><span data-stu-id="92e9b-140">Do not drop support for .NET Standard when you do this.</span></span> <span data-ttu-id="92e9b-141">Zamiast tego należy zgłosić z interfejsów API możliwości implementacji i oferty.</span><span class="sxs-lookup"><span data-stu-id="92e9b-141">Instead, throw from the implementation and offer capability APIs.</span></span> <span data-ttu-id="92e9b-142">Dzięki temu biblioteka może być używana w dowolnym miejscu i obsługuje środowisko uruchomieniowe funkcji.</span><span class="sxs-lookup"><span data-stu-id="92e9b-142">This way, your library can be used anywhere and supports runtime light-up of features.</span></span>

```csharp
public static class GpsLocation
{
    // This project uses multi-targeting to expose device-specific APIs to .NET Standard.
    public static async Task<(double latitude, double longitude)> GetCoordinatesAsync()
    {
#if NET461
        return CallDotNetFramworkApi();
#elif WINDOWS_UWP
        return CallUwpApi();
#else
        throw new PlatformNotSupportedException();
#endif
    }

    // Allows callers to check without having to catch PlatformNotSupportedException
    // or replicating the OS check.
    public static bool IsSupported
    {
        get
        {
#if NET461 || WINDOWS_UWP
            return true;
#else
            return false;
#endif
        }
    }
}
```

<span data-ttu-id="92e9b-143">❌ Należy unikać określania elementów docelowych i .NET Standard, jeśli kod źródłowy jest taki sam dla wszystkich obiektów docelowych.</span><span class="sxs-lookup"><span data-stu-id="92e9b-143">❌ AVOID multi-targeting as well as targeting .NET Standard, if your source code is the same for all targets.</span></span>

> <span data-ttu-id="92e9b-144">Zestaw .NET Standard będzie automatycznie używany przez pakiet NuGet.</span><span class="sxs-lookup"><span data-stu-id="92e9b-144">The .NET Standard assembly will automatically be used by NuGet.</span></span> <span data-ttu-id="92e9b-145">Kierowanie poszczególnych implementacji platformy .NET zwiększa `*.nupkg` rozmiar w przypadku braku korzyści.</span><span class="sxs-lookup"><span data-stu-id="92e9b-145">Targeting individual .NET implementations increases the `*.nupkg` size for no benefit.</span></span>

<span data-ttu-id="92e9b-146">✔️ Rozważ dodanie elementu docelowego dla `net461` , gdy tworzysz ofertę `netstandard2.0` docelową.</span><span class="sxs-lookup"><span data-stu-id="92e9b-146">✔️ CONSIDER adding a target for `net461` when you're offering a `netstandard2.0` target.</span></span>

> <span data-ttu-id="92e9b-147">Korzystanie z .NET Standard 2,0 z .NET Framework ma problemy, które zostały rozwiązane w .NET Framework 4.7.2.</span><span class="sxs-lookup"><span data-stu-id="92e9b-147">Using .NET Standard 2.0 from .NET Framework has some issues that were addressed in .NET Framework 4.7.2.</span></span> <span data-ttu-id="92e9b-148">Możesz poprawić środowisko dla deweloperów, którzy nadal znajdują się w .NET Framework 4.6.1-4.7.1, oferując im plik binarny, który jest skompilowany dla .NET Framework 4.6.1.</span><span class="sxs-lookup"><span data-stu-id="92e9b-148">You can improve the experience for developers that are still on .NET Framework 4.6.1 - 4.7.1 by offering them a binary that is built for .NET Framework 4.6.1.</span></span>

<span data-ttu-id="92e9b-149">✔️ Przeprowadź dystrybucję biblioteki przy użyciu pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="92e9b-149">✔️ DO distribute your library using a NuGet package.</span></span>

> <span data-ttu-id="92e9b-150">Pakiet NuGet wybierze najlepszy cel dla dewelopera i osłonę, aby wybrać odpowiednią implementację.</span><span class="sxs-lookup"><span data-stu-id="92e9b-150">NuGet will select the best target for the developer and shield them having to pick the appropriate implementation.</span></span>

<span data-ttu-id="92e9b-151">✔️ Użyj właściwości pliku projektu, `TargetFrameworks` gdy wiele obiektów docelowych.</span><span class="sxs-lookup"><span data-stu-id="92e9b-151">✔️ DO use a project file's `TargetFrameworks` property when multi-targeting.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <!-- This project will output netstandard2.0 and net461 assemblies -->
    <TargetFrameworks>netstandard2.0;net461</TargetFrameworks>
  </PropertyGroup>
</Project>
```

<span data-ttu-id="92e9b-152">✔️ ROZWAŻYĆ użycie programu [MSBuild. Sdk. Extras](https://github.com/onovotny/MSBuildSdkExtras) , gdy wiele obiektów docelowych dla platformy UWP i Xamarin jest znacznie upraszcza plik projektu.</span><span class="sxs-lookup"><span data-stu-id="92e9b-152">✔️ CONSIDER using [MSBuild.Sdk.Extras](https://github.com/onovotny/MSBuildSdkExtras) when multi-targeting for UWP and Xamarin as it greatly simplifies your project file.</span></span>

## <a name="older-targets"></a><span data-ttu-id="92e9b-153">Starsze elementy docelowe</span><span class="sxs-lookup"><span data-stu-id="92e9b-153">Older targets</span></span>

<span data-ttu-id="92e9b-154">Platforma .NET obsługuje docelowe wersje .NET Framework, które są nieobsługiwane, a także platformy, które nie są już powszechnie używane.</span><span class="sxs-lookup"><span data-stu-id="92e9b-154">.NET supports targeting versions of .NET Framework that are long out of support as well as platforms that are no longer commonly used.</span></span> <span data-ttu-id="92e9b-155">Chociaż istnieje wartość w tym, że Twoja biblioteka działa jak największej liczbie obiektów docelowych, bez obejścia interfejsów API, można zwiększyć znaczący koszt.</span><span class="sxs-lookup"><span data-stu-id="92e9b-155">While there's value in making your library work on as many targets as possible, having to work around missing APIs can add significant overhead.</span></span> <span data-ttu-id="92e9b-156">Uważamy, że pewne struktury nie są już ukierunkowane na to, biorąc pod uwagę ich zasięg i ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="92e9b-156">We believe certain frameworks are no longer worth targeting, considering their reach and limitations.</span></span>

<span data-ttu-id="92e9b-157">❌ NIE dołączaj obiektu docelowego biblioteki klas przenośnych (PCL).</span><span class="sxs-lookup"><span data-stu-id="92e9b-157">❌ DO NOT include a Portable Class Library (PCL) target.</span></span> <span data-ttu-id="92e9b-158">Na przykład `portable-net45+win8+wpa81+wp8`.</span><span class="sxs-lookup"><span data-stu-id="92e9b-158">For example, `portable-net45+win8+wpa81+wp8`.</span></span>

> <span data-ttu-id="92e9b-159">.NET Standard to nowoczesny sposób obsługi bibliotek platformy .NET dla wielu platform i zastępuje PCLs.</span><span class="sxs-lookup"><span data-stu-id="92e9b-159">.NET Standard is the modern way to support cross-platform .NET libraries and replaces PCLs.</span></span>

<span data-ttu-id="92e9b-160">❌ NIE należy dołączać obiektów docelowych dla platform .NET, które nie są już obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="92e9b-160">❌ DO NOT include targets for .NET platforms that are no longer supported.</span></span> <span data-ttu-id="92e9b-161">Na przykład `SL4` , `WP` .</span><span class="sxs-lookup"><span data-stu-id="92e9b-161">For example, `SL4`, `WP`.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="92e9b-162">[Poprzedni](get-started.md) 
> [Dalej](strong-naming.md)</span><span class="sxs-lookup"><span data-stu-id="92e9b-162">[Previous](get-started.md)
[Next](strong-naming.md)</span></span>
