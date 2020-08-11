---
title: Dodatki do formatu csproj dla platformy .NET Core
description: Dowiedz się więcej o różnicach między istniejącymi a plikami csproj programu .NET Core
ms.topic: reference
ms.date: 04/08/2019
ms.openlocfilehash: 4f45362fbb3df053b95156b8e633903f011a85ad
ms.sourcegitcommit: 7476c20d2f911a834a00b8a7f5e8926bae6804d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/11/2020
ms.locfileid: "88062876"
---
# <a name="additions-to-the-csproj-format-for-net-core"></a><span data-ttu-id="c9046-103">Dodatki do formatu csproj dla platformy .NET Core</span><span class="sxs-lookup"><span data-stu-id="c9046-103">Additions to the csproj format for .NET Core</span></span>

<span data-ttu-id="c9046-104">Ten dokument zawiera opis zmian, które zostały dodane do plików projektu w ramach przenoszenia z *project.js* do *csproj* i [MSBuild](https://github.com/Microsoft/MSBuild).</span><span class="sxs-lookup"><span data-stu-id="c9046-104">This document outlines the changes that were added to the project files as part of the move from *project.json* to *csproj* and [MSBuild](https://github.com/Microsoft/MSBuild).</span></span> <span data-ttu-id="c9046-105">Aby uzyskać więcej informacji na temat ogólnej składni pliku projektu i odwołania, zobacz dokumentację [pliku projektu programu MSBuild](/visualstudio/msbuild/msbuild-project-file-schema-reference) .</span><span class="sxs-lookup"><span data-stu-id="c9046-105">For more information about general project file syntax and reference, see [the MSBuild project file](/visualstudio/msbuild/msbuild-project-file-schema-reference) documentation.</span></span>

## <a name="implicit-package-references"></a><span data-ttu-id="c9046-106">Odwołania do pakietów niejawnych</span><span class="sxs-lookup"><span data-stu-id="c9046-106">Implicit package references</span></span>

<span data-ttu-id="c9046-107">Elementy pakietu są niejawnie przywoływane na podstawie platform docelowych określonych we `<TargetFramework>` `<TargetFrameworks>` właściwości lub pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="c9046-107">Metapackages are implicitly referenced based on the target framework(s) specified in the `<TargetFramework>` or `<TargetFrameworks>` property of your project file.</span></span> <span data-ttu-id="c9046-108">`<TargetFrameworks>`jest ignorowany `<TargetFramework>` , jeśli jest określony, niezależnie od kolejności.</span><span class="sxs-lookup"><span data-stu-id="c9046-108">`<TargetFrameworks>` is ignored if `<TargetFramework>` is specified, independent of order.</span></span>

```xml
 <PropertyGroup>
   <TargetFramework>netcoreapp2.1</TargetFramework>
 </PropertyGroup>
 ```

 ```xml
 <PropertyGroup>
   <TargetFrameworks>netcoreapp2.1;net462</TargetFrameworks>
 </PropertyGroup>
 ```

### <a name="recommendations"></a><span data-ttu-id="c9046-109">Zalecenia</span><span class="sxs-lookup"><span data-stu-id="c9046-109">Recommendations</span></span>

<span data-ttu-id="c9046-110">Ponieważ `Microsoft.NETCore.App` lub `NETStandard.Library` pakiety są niejawnie przywoływane, zalecane są następujące najlepsze rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="c9046-110">Since `Microsoft.NETCore.App` or `NETStandard.Library` metapackages are implicitly referenced, the following are our recommended best practices:</span></span>

- <span data-ttu-id="c9046-111">W przypadku określania wartości docelowej .NET Core lub .NET Standard nigdy nie ma jawnego odwołania do `Microsoft.NETCore.App` `NETStandard.Library` elementów i pakietów `<PackageReference>` w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="c9046-111">When targeting .NET Core or .NET Standard, never have an explicit reference to the `Microsoft.NETCore.App` or `NETStandard.Library` metapackages via a `<PackageReference>` item in your project file.</span></span>
- <span data-ttu-id="c9046-112">Jeśli potrzebna jest określona wersja środowiska uruchomieniowego w przypadku określania wartości docelowej .NET Core, należy użyć `<RuntimeFrameworkVersion>` właściwości w projekcie (na przykład `1.0.4` ) zamiast odwoływać się do pakietu.</span><span class="sxs-lookup"><span data-stu-id="c9046-112">If you need a specific version of the runtime when targeting .NET Core, you should use the `<RuntimeFrameworkVersion>` property in your project (for example, `1.0.4`) instead of referencing the metapackage.</span></span>
  - <span data-ttu-id="c9046-113">Taka sytuacja może wystąpić, jeśli używasz [własnych wdrożeń](../deploying/index.md#publish-self-contained) i potrzebujesz określonej wersji poprawki środowiska uruchomieniowego 1.0.0 LTS, na przykład.</span><span class="sxs-lookup"><span data-stu-id="c9046-113">This might happen if you are using [self-contained deployments](../deploying/index.md#publish-self-contained) and you need a specific patch version of 1.0.0 LTS runtime, for example.</span></span>
- <span data-ttu-id="c9046-114">Jeśli potrzebujesz konkretnej wersji `NETStandard.Library` pakietu w przypadku określania wartości docelowej .NET Standard, możesz użyć `<NetStandardImplicitPackageVersion>` właściwości i ustawić potrzebną wersję.</span><span class="sxs-lookup"><span data-stu-id="c9046-114">If you need a specific version of the `NETStandard.Library` metapackage when targeting .NET Standard, you can use the `<NetStandardImplicitPackageVersion>` property and set the version you need.</span></span>
- <span data-ttu-id="c9046-115">Nie należy jawnie dodawać ani aktualizować odwołań do `Microsoft.NETCore.App` lub do `NETStandard.Library` pakietu w projektach .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="c9046-115">Don't explicitly add or update references to either the `Microsoft.NETCore.App` or `NETStandard.Library` metapackage in .NET Framework projects.</span></span> <span data-ttu-id="c9046-116">Jeśli dowolna wersja programu `NETStandard.Library` jest wymagana w przypadku korzystania z pakietu NuGet opartego na .NET Standard, pakiet NuGet automatycznie zainstaluje tę wersję.</span><span class="sxs-lookup"><span data-stu-id="c9046-116">If any version of `NETStandard.Library` is needed when using a .NET Standard-based NuGet package, NuGet automatically installs that version.</span></span>

## <a name="implicit-version-for-some-package-references"></a><span data-ttu-id="c9046-117">Niejawna wersja dla niektórych odwołań do pakietów</span><span class="sxs-lookup"><span data-stu-id="c9046-117">Implicit version for some package references</span></span>

<span data-ttu-id="c9046-118">Większość zastosowań [`<PackageReference>`](#packagereference) wymaga ustawienia `Version` atrybutu w celu określenia wersji pakietu NuGet do użycia.</span><span class="sxs-lookup"><span data-stu-id="c9046-118">Most usages of [`<PackageReference>`](#packagereference) require setting the `Version` attribute to specify the NuGet package version to be used.</span></span> <span data-ttu-id="c9046-119">W przypadku korzystania z platformy .NET Core 2,1 lub 2,2 i odwoływania się do [Microsoft. AspNetCore. app](/aspnet/core/fundamentals/metapackage-app) lub [Microsoft. AspNetCore. All](/aspnet/core/fundamentals/metapackage), jednak atrybut jest zbędny.</span><span class="sxs-lookup"><span data-stu-id="c9046-119">When using .NET Core 2.1 or 2.2 and referencing [Microsoft.AspNetCore.App](/aspnet/core/fundamentals/metapackage-app) or [Microsoft.AspNetCore.All](/aspnet/core/fundamentals/metapackage), however, the  attribute is unnecessary.</span></span> <span data-ttu-id="c9046-120">Zestaw .NET Core SDK może automatycznie wybrać wersję tych pakietów, które mają być używane.</span><span class="sxs-lookup"><span data-stu-id="c9046-120">The .NET Core SDK can automatically select the version of these packages that should be used.</span></span>

### <a name="recommendation"></a><span data-ttu-id="c9046-121">Rekomendacja</span><span class="sxs-lookup"><span data-stu-id="c9046-121">Recommendation</span></span>

<span data-ttu-id="c9046-122">W przypadku odwoływania się do `Microsoft.AspNetCore.App` `Microsoft.AspNetCore.All` pakietów lub nie należy określać ich wersji.</span><span class="sxs-lookup"><span data-stu-id="c9046-122">When referencing the `Microsoft.AspNetCore.App` or `Microsoft.AspNetCore.All` packages, do not specify their version.</span></span> <span data-ttu-id="c9046-123">Jeśli określona jest wersja, zestaw SDK może generować ostrzeżenie NETSDK1071.</span><span class="sxs-lookup"><span data-stu-id="c9046-123">If a version is specified, the SDK may produce warning NETSDK1071.</span></span> <span data-ttu-id="c9046-124">Aby usunąć to ostrzeżenie, Usuń wersję pakietu, taką jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="c9046-124">To fix this warning, remove the package version like in the following example:</span></span>

```xml
<ItemGroup>
  <PackageReference Include="Microsoft.AspNetCore.App" />
</ItemGroup>
```

> <span data-ttu-id="c9046-125">Znany problem: zestaw SDK platformy .NET Core 2,1 obsługuje tę składnię tylko wtedy, gdy projekt używa także Microsoft. NET. Sdk. Web.</span><span class="sxs-lookup"><span data-stu-id="c9046-125">Known issue: the .NET Core 2.1 SDK only supported this syntax when the project also uses Microsoft.NET.Sdk.Web.</span></span> <span data-ttu-id="c9046-126">Ten problem został rozwiązany w zestawie SDK platformy .NET Core 2,2.</span><span class="sxs-lookup"><span data-stu-id="c9046-126">This is resolved in the .NET Core 2.2 SDK.</span></span>

<span data-ttu-id="c9046-127">Te odwołania do ASP.NET Core pakietu są nieco inne niż w przypadku większości normalnych pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="c9046-127">These references to ASP.NET Core metapackages have a slightly different behavior from most normal NuGet packages.</span></span> <span data-ttu-id="c9046-128">Wdrożenia aplikacji korzystających z tych pakietów w [ramach platformy](../deploying/index.md#publish-runtime-dependent) są automatycznie wykorzystywane w ramach platformy udostępnionej ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="c9046-128">[Framework-dependent deployments](../deploying/index.md#publish-runtime-dependent) of applications that use these metapackages automatically take advantage of the ASP.NET Core shared framework.</span></span> <span data-ttu-id="c9046-129">W przypadku korzystania z pakietów trwałych nie są wdrażane **żadne** zasoby z przywoływanych ASP.NET Core pakietów NuGet w aplikacji — ASP.NET Core współdzielona architektura zawiera te zasoby.</span><span class="sxs-lookup"><span data-stu-id="c9046-129">When you use the metapackages, **no** assets from the referenced ASP.NET Core NuGet packages are deployed with the application—the ASP.NET Core shared framework contains these assets.</span></span> <span data-ttu-id="c9046-130">Zasoby w strukturze udostępnionej są zoptymalizowane pod kątem platformy docelowej w celu poprawienia czasu uruchamiania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c9046-130">The assets in the shared framework are optimized for the target platform to improve application startup time.</span></span> <span data-ttu-id="c9046-131">Aby uzyskać więcej informacji na temat platformy udostępnionej, zobacz [pakiet dystrybucji .NET Core](../distribution-packaging.md).</span><span class="sxs-lookup"><span data-stu-id="c9046-131">For more information about shared framework, see [.NET Core distribution packaging](../distribution-packaging.md).</span></span>

<span data-ttu-id="c9046-132">Jeśli określona *jest* wersja, jest ona traktowana jako *minimalna* wersja ASP.NET Core udostępnionej platformy dla wdrożeń zależnych od platformy i jako *dokładna* wersja wdrożeń samodzielnych.</span><span class="sxs-lookup"><span data-stu-id="c9046-132">If a version *is* specified, it's treated as the *minimum* version of ASP.NET Core shared framework for framework-dependent deployments and as an *exact* version for self-contained deployments.</span></span> <span data-ttu-id="c9046-133">Może to mieć następujące konsekwencje:</span><span class="sxs-lookup"><span data-stu-id="c9046-133">This can have the following consequences:</span></span>

- <span data-ttu-id="c9046-134">Jeśli wersja ASP.NET Core zainstalowana na serwerze jest mniejsza niż wersja określona w PackageReference, uruchomienie procesu platformy .NET Core kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="c9046-134">If the version of ASP.NET Core installed on the server is less than the version specified on the PackageReference, the .NET Core process fails to launch.</span></span> <span data-ttu-id="c9046-135">Aktualizacje pakietu NuGet.org są często dostępne na platformie Microsoft, zanim zostaną udostępnione aktualizacje w środowiskach hostingu, takich jak Azure.</span><span class="sxs-lookup"><span data-stu-id="c9046-135">Updates to the metapackage are often available on NuGet.org before updates have been made available in hosting environments such as Azure.</span></span> <span data-ttu-id="c9046-136">Zaktualizowanie wersji na PackageReference w celu ASP.NET Core może spowodować niepowodzenie wdrożonej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c9046-136">Updating the version on the PackageReference to ASP.NET Core could cause a deployed application to fail.</span></span>
- <span data-ttu-id="c9046-137">Jeśli aplikacja jest wdrażana jako [wdrożenie samodzielne](../deploying/index.md#publish-self-contained), aplikacja może nie zawierać najnowszych aktualizacji zabezpieczeń do programu .NET Core.</span><span class="sxs-lookup"><span data-stu-id="c9046-137">If the application is deployed as a [self-contained deployment](../deploying/index.md#publish-self-contained), the application may not contain the latest security updates to .NET Core.</span></span> <span data-ttu-id="c9046-138">Jeśli wersja nie jest określona, zestaw SDK może automatycznie dołączać najnowszą wersję ASP.NET Core w samodzielnym wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="c9046-138">When a version isn't specified, the SDK can automatically include the newest version of ASP.NET Core in the self-contained deployment.</span></span>

## <a name="default-compilation-includes-in-net-core-projects"></a><span data-ttu-id="c9046-139">Domyślna kompilacja obejmuje projekty .NET Core</span><span class="sxs-lookup"><span data-stu-id="c9046-139">Default compilation includes in .NET Core projects</span></span>

<span data-ttu-id="c9046-140">Po przeniesieniu do formatu *csproj* w najnowszej wersji zestawu SDK przeniesiono domyślną wartość dołączania i wykluczania dla elementów kompilowania i zasobów osadzonych do plików właściwości zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="c9046-140">With the move to the *csproj* format in the latest SDK versions, we've moved the default includes and excludes for compile items and embedded resources to the SDK properties files.</span></span> <span data-ttu-id="c9046-141">Oznacza to, że nie trzeba już określać tych elementów w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="c9046-141">This means that you no longer need to specify these items in your project file.</span></span>

<span data-ttu-id="c9046-142">Głównym powodem tego jest zmniejszenie bałaganu w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="c9046-142">The main reason for doing this is to reduce the clutter in your project file.</span></span> <span data-ttu-id="c9046-143">Wartości domyślne, które są obecne w zestawie SDK, powinny obejmować najbardziej typowe przypadki użycia, więc nie trzeba powtarzać ich w każdym tworzonym projekcie.</span><span class="sxs-lookup"><span data-stu-id="c9046-143">The defaults that are present in the SDK should cover most common use cases, so there is no need to repeat them in every project that you create.</span></span> <span data-ttu-id="c9046-144">Prowadzi to do mniejszych plików projektu, które są znacznie łatwiejsze do zrozumienia, a także do edycji, w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="c9046-144">This leads to smaller project files that are much easier to understand as well as edit by hand, if needed.</span></span>

<span data-ttu-id="c9046-145">W poniższej tabeli przedstawiono, który element i które [elementy globalne](https://en.wikipedia.org/wiki/Glob_(programming)) są uwzględnione i wykluczone w zestawie SDK:</span><span class="sxs-lookup"><span data-stu-id="c9046-145">The following table shows which element and which [globs](https://en.wikipedia.org/wiki/Glob_(programming)) are both included and excluded in the SDK:</span></span>

| <span data-ttu-id="c9046-146">Element</span><span class="sxs-lookup"><span data-stu-id="c9046-146">Element</span></span>           | <span data-ttu-id="c9046-147">Uwzględnij globalizowania</span><span class="sxs-lookup"><span data-stu-id="c9046-147">Include glob</span></span>                              | <span data-ttu-id="c9046-148">Wyklucz globalizowania</span><span class="sxs-lookup"><span data-stu-id="c9046-148">Exclude glob</span></span>                                                  | <span data-ttu-id="c9046-149">Usuń globalizowania</span><span class="sxs-lookup"><span data-stu-id="c9046-149">Remove glob</span></span>              |
|-------------------|-------------------------------------------|---------------------------------------------------------------|----------------------------|
| <span data-ttu-id="c9046-150">Opracowania</span><span class="sxs-lookup"><span data-stu-id="c9046-150">Compile</span></span>           | <span data-ttu-id="c9046-151">\*\*/\*. cs (lub inne rozszerzenia językowe)</span><span class="sxs-lookup"><span data-stu-id="c9046-151">\*\*/\*.cs (or other language extensions)</span></span> | <span data-ttu-id="c9046-152">\*\*/\*Użytkownicy  \*\*/\*.\* proj  \*\*/\*. sln  \*\*/\*. vssscc</span><span class="sxs-lookup"><span data-stu-id="c9046-152">\*\*/\*.user;  \*\*/\*.\*proj;  \*\*/\*.sln;  \*\*/\*.vssscc</span></span>  | <span data-ttu-id="c9046-153">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="c9046-153">N/A</span></span>                      |
| <span data-ttu-id="c9046-154">EmbeddedResource</span><span class="sxs-lookup"><span data-stu-id="c9046-154">EmbeddedResource</span></span>  | <span data-ttu-id="c9046-155">\*\*/\*. resx</span><span class="sxs-lookup"><span data-stu-id="c9046-155">\*\*/\*.resx</span></span>                              | <span data-ttu-id="c9046-156">\*\*/\*Użytkownicy \*\*/\*.\* proj \*\*/\*. sln \*\*/\*. vssscc</span><span class="sxs-lookup"><span data-stu-id="c9046-156">\*\*/\*.user; \*\*/\*.\*proj; \*\*/\*.sln; \*\*/\*.vssscc</span></span>     | <span data-ttu-id="c9046-157">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="c9046-157">N/A</span></span>                      |
| <span data-ttu-id="c9046-158">Brak</span><span class="sxs-lookup"><span data-stu-id="c9046-158">None</span></span>              | \*\*/\*                                   | <span data-ttu-id="c9046-159">\*\*/\*Użytkownicy \*\*/\*.\* proj \*\*/\*. sln \*\*/\*. vssscc</span><span class="sxs-lookup"><span data-stu-id="c9046-159">\*\*/\*.user; \*\*/\*.\*proj; \*\*/\*.sln; \*\*/\*.vssscc</span></span>     | <span data-ttu-id="c9046-160">\*\*/\*Rejestr \*\*/\*. resx</span><span class="sxs-lookup"><span data-stu-id="c9046-160">\*\*/\*.cs; \*\*/\*.resx</span></span>   |

> [!NOTE]
> <span data-ttu-id="c9046-161">Polecenie **exclude globalizowania** zawsze wyklucza `./bin` foldery i `./obj` , które są reprezentowane odpowiednio przez `$(BaseOutputPath)` właściwości i programu `$(BaseIntermediateOutputPath)` MSBuild.</span><span class="sxs-lookup"><span data-stu-id="c9046-161">**Exclude glob** always excludes the `./bin` and `./obj` folders, which are represented by the `$(BaseOutputPath)` and `$(BaseIntermediateOutputPath)` MSBuild properties, respectively.</span></span> <span data-ttu-id="c9046-162">Jako całość wszystkie wykluczenia są reprezentowane przez `$(DefaultItemExcludes)` .</span><span class="sxs-lookup"><span data-stu-id="c9046-162">As a whole, all excludes are represented by `$(DefaultItemExcludes)`.</span></span>

<span data-ttu-id="c9046-163">Jeśli masz elementy globalne w projekcie i spróbujesz skompilować go przy użyciu najnowszego zestawu SDK, zostanie wyświetlony następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="c9046-163">If you have globs in your project and you try to build it using the newest SDK, you'll get the following error:</span></span>

> <span data-ttu-id="c9046-164">Uwzględniono zduplikowane elementy kompilacji.</span><span class="sxs-lookup"><span data-stu-id="c9046-164">Duplicate Compile items were included.</span></span> <span data-ttu-id="c9046-165">Zestaw SDK platformy .NET domyślnie zawiera elementy kompilacji z katalogu projektu.</span><span class="sxs-lookup"><span data-stu-id="c9046-165">The .NET SDK includes Compile items from your project directory by default.</span></span> <span data-ttu-id="c9046-166">Możesz usunąć te elementy z pliku projektu lub ustawić właściwość "EnableDefaultCompileItems" na wartość "false", jeśli chcesz jawnie uwzględnić je w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="c9046-166">You can either remove these items from your project file, or set the 'EnableDefaultCompileItems' property to 'false' if you want to explicitly include them in your project file.</span></span>

<span data-ttu-id="c9046-167">Aby obejść ten błąd, można usunąć jawne `Compile` elementy, które pasują do tych wymienionych w poprzedniej tabeli, lub ustawić `<EnableDefaultCompileItems>` Właściwość na `false` , tak jak to:</span><span class="sxs-lookup"><span data-stu-id="c9046-167">In order to get around this error, you can either remove the explicit `Compile` items that match the ones listed on the previous table, or you can set the `<EnableDefaultCompileItems>` property to `false`, like this:</span></span>

```xml
<PropertyGroup>
    <EnableDefaultCompileItems>false</EnableDefaultCompileItems>
</PropertyGroup>
```

<span data-ttu-id="c9046-168">Ustawienie tej właściwości na wartość `false` spowoduje wyłączenie niejawnego dołączania, przywrócenie do zachowania poprzednich zestawów SDK, gdzie należy określić domyślny elementy globalne w projekcie.</span><span class="sxs-lookup"><span data-stu-id="c9046-168">Setting this property to `false` will disable implicit inclusion, reverting to the behavior of previous SDKs where you had to specify the default globs in your project.</span></span>

<span data-ttu-id="c9046-169">Ta zmiana nie modyfikuje głównej Mechanics innych dołączeń.</span><span class="sxs-lookup"><span data-stu-id="c9046-169">This change does not modify the main mechanics of other includes.</span></span> <span data-ttu-id="c9046-170">Jeśli jednak chcesz określić, na przykład niektóre pliki do opublikowania w aplikacji, możesz nadal używać znanych mechanizmów w *csproj* dla tego (na przykład `<Content>` elementu).</span><span class="sxs-lookup"><span data-stu-id="c9046-170">However, if you wish to specify, for example, some files to get published with your app, you can still use the known mechanisms in *csproj* for that (for example, the `<Content>` element).</span></span>

<span data-ttu-id="c9046-171">`<EnableDefaultCompileItems>`wyłącza tylko `Compile` elementy globalne, ale nie wpływa na inne elementy globalne, takie jak niejawne `None` globalizowania, które również dotyczą \* elementów cs.</span><span class="sxs-lookup"><span data-stu-id="c9046-171">`<EnableDefaultCompileItems>` only disables `Compile` globs but doesn't affect other globs, like the implicit `None` glob, which also applies to \*.cs items.</span></span> <span data-ttu-id="c9046-172">Z tego powodu, **Eksplorator rozwiązań** będzie kontynuować wyświetlanie \* elementów CS jako części projektu, zawartych jako `None` elementy.</span><span class="sxs-lookup"><span data-stu-id="c9046-172">Because of that, **Solution Explorer** will continue show \*.cs items as part of the project, included as `None` items.</span></span> <span data-ttu-id="c9046-173">W podobny sposób można ustawić `<EnableDefaultNoneItems>` wartość false, aby wyłączyć niejawną `None` globalizowania w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="c9046-173">In a similar way, you can set `<EnableDefaultNoneItems>` to false to disable the implicit `None` glob, like this:</span></span>

```xml
<PropertyGroup>
    <EnableDefaultNoneItems>false</EnableDefaultNoneItems>
</PropertyGroup>
```

<span data-ttu-id="c9046-174">Aby wyłączyć **wszystkie niejawne elementy globalne**, można ustawić `<EnableDefaultItems>` Właściwość na `false` tak jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="c9046-174">To disable **all implicit globs**, you can set the `<EnableDefaultItems>` property to `false` as in the following example:</span></span>

```xml
<PropertyGroup>
    <EnableDefaultItems>false</EnableDefaultItems>
</PropertyGroup>
```

## <a name="how-to-see-the-whole-project-as-msbuild-sees-it"></a><span data-ttu-id="c9046-175">Jak wyświetlić cały projekt, gdy jest on widoczny dla MSBuild</span><span class="sxs-lookup"><span data-stu-id="c9046-175">How to see the whole project as MSBuild sees it</span></span>

<span data-ttu-id="c9046-176">Chociaż te csproj zmieniają znacznie uproszczenie plików projektu, warto zobaczyć w pełni rozwinięty projekt, ponieważ program MSBuild zobaczy go po dołączeniu zestawu SDK i jego obiektów docelowych.</span><span class="sxs-lookup"><span data-stu-id="c9046-176">While those csproj changes greatly simplify project files, you might want to see the fully expanded project as MSBuild sees it once the SDK and its targets are included.</span></span> <span data-ttu-id="c9046-177">Przetwórz wstępnie projekt przy [użyciu `/pp` przełącznika](/visualstudio/msbuild/msbuild-command-line-reference#preprocess) [`dotnet msbuild`](dotnet-msbuild.md) polecenia, który pokazuje, które pliki są importowane, ich źródła i ich wkład do kompilacji bez rzeczywistego tworzenia projektu:</span><span class="sxs-lookup"><span data-stu-id="c9046-177">Preprocess the project with [the `/pp` switch](/visualstudio/msbuild/msbuild-command-line-reference#preprocess) of the [`dotnet msbuild`](dotnet-msbuild.md) command, which shows which files are imported, their sources, and their contributions to the build without actually building the project:</span></span>

`dotnet msbuild -pp:fullproject.xml`

<span data-ttu-id="c9046-178">Jeśli projekt ma wiele platform docelowych, wyniki polecenia powinny być skoncentrowane tylko na jednym z nich, określając go jako właściwość programu MSBuild:</span><span class="sxs-lookup"><span data-stu-id="c9046-178">If the project has multiple target frameworks, the results of the command should be focused on only one of them by specifying it as an MSBuild property:</span></span>

`dotnet msbuild -p:TargetFramework=netcoreapp2.0 -pp:fullproject.xml`

## <a name="additions"></a><span data-ttu-id="c9046-179">Zwiększenia</span><span class="sxs-lookup"><span data-stu-id="c9046-179">Additions</span></span>

### <a name="sdk-attribute"></a><span data-ttu-id="c9046-180">Atrybut zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="c9046-180">Sdk attribute</span></span>

<span data-ttu-id="c9046-181">Element główny `<Project>` pliku *. csproj* ma nowy atrybut o nazwie `Sdk` .</span><span class="sxs-lookup"><span data-stu-id="c9046-181">The root `<Project>` element of the *.csproj* file has a new attribute called `Sdk`.</span></span> <span data-ttu-id="c9046-182">`Sdk`Określa, który zestaw SDK będzie używany przez ten projekt.</span><span class="sxs-lookup"><span data-stu-id="c9046-182">`Sdk` specifies which SDK will be used by the project.</span></span> <span data-ttu-id="c9046-183">Zestaw SDK, zgodnie z opisem w dokumencie zawierającym [warstwy](cli-msbuild-architecture.md) , to zestaw [zadań](/visualstudio/msbuild/msbuild-tasks) i [elementów docelowych](/visualstudio/msbuild/msbuild-targets) programu MSBuild, które mogą kompilować kod platformy .NET Core.</span><span class="sxs-lookup"><span data-stu-id="c9046-183">The SDK, as the [layering document](cli-msbuild-architecture.md) describes, is a set of MSBuild [tasks](/visualstudio/msbuild/msbuild-tasks) and [targets](/visualstudio/msbuild/msbuild-targets) that can build .NET Core code.</span></span> <span data-ttu-id="c9046-184">Dostępne są następujące zestawy SDK dla platformy .NET Core:</span><span class="sxs-lookup"><span data-stu-id="c9046-184">The following SDKs are available for .NET Core:</span></span>

1. <span data-ttu-id="c9046-185">Zestaw .NET Core SDK o IDENTYFIKATORze`Microsoft.NET.Sdk`</span><span class="sxs-lookup"><span data-stu-id="c9046-185">The .NET Core SDK with the ID of `Microsoft.NET.Sdk`</span></span>
2. <span data-ttu-id="c9046-186">Zestaw SDK sieci Web platformy .NET Core o IDENTYFIKATORze`Microsoft.NET.Sdk.Web`</span><span class="sxs-lookup"><span data-stu-id="c9046-186">The .NET Core web SDK with the ID of `Microsoft.NET.Sdk.Web`</span></span>
3. <span data-ttu-id="c9046-187">Zestaw SDK biblioteki klas programu .NET Core z IDENTYFIKATORem`Microsoft.NET.Sdk.Razor`</span><span class="sxs-lookup"><span data-stu-id="c9046-187">The .NET Core Razor Class Library SDK with the ID of `Microsoft.NET.Sdk.Razor`</span></span>
4. <span data-ttu-id="c9046-188">Usługa programu .NET Core Worker o IDENTYFIKATORze `Microsoft.NET.Sdk.Worker` (od programu .net core 3,0)</span><span class="sxs-lookup"><span data-stu-id="c9046-188">The .NET Core Worker Service with the ID of `Microsoft.NET.Sdk.Worker` (since .NET Core 3.0)</span></span>
5. <span data-ttu-id="c9046-189">Podstawowe WinForms i WPF platformy .NET z IDENTYFIKATORem `Microsoft.NET.Sdk.WindowsDesktop` (ponieważ .NET Core 3,0)</span><span class="sxs-lookup"><span data-stu-id="c9046-189">The .NET Core WinForms and WPF with the ID of `Microsoft.NET.Sdk.WindowsDesktop` (since .NET Core 3.0)</span></span>

<span data-ttu-id="c9046-190">Musisz mieć `Sdk` atrybut ustawiony na jeden z tych identyfikatorów w `<Project>` elemencie, aby można było użyć narzędzi .NET Core i skompilować swój kod.</span><span class="sxs-lookup"><span data-stu-id="c9046-190">You need to have the `Sdk` attribute set to one of those IDs on the `<Project>` element in order to use the .NET Core tools and build your code.</span></span>

### <a name="packagereference"></a><span data-ttu-id="c9046-191">PackageReference</span><span class="sxs-lookup"><span data-stu-id="c9046-191">PackageReference</span></span>

<span data-ttu-id="c9046-192">Element `<PackageReference>` Item określa [zależność NuGet w projekcie](/nuget/consume-packages/package-references-in-project-files).</span><span class="sxs-lookup"><span data-stu-id="c9046-192">A `<PackageReference>` item element specifies a [NuGet dependency in the project](/nuget/consume-packages/package-references-in-project-files).</span></span> <span data-ttu-id="c9046-193">Ten `Include` atrybut określa identyfikator pakietu.</span><span class="sxs-lookup"><span data-stu-id="c9046-193">The `Include` attribute specifies the package ID.</span></span>

```xml
<PackageReference Include="package-id" Version="" PrivateAssets="" IncludeAssets="" ExcludeAssets="" />
```

#### <a name="version"></a><span data-ttu-id="c9046-194">Wersja</span><span class="sxs-lookup"><span data-stu-id="c9046-194">Version</span></span>

<span data-ttu-id="c9046-195">Wymagany `Version` atrybut określa wersję pakietu do przywrócenia.</span><span class="sxs-lookup"><span data-stu-id="c9046-195">The required `Version` attribute specifies the version of the package to restore.</span></span> <span data-ttu-id="c9046-196">Ten atrybut uwzględnia reguły schematu [zakresu wersji NuGet](/nuget/concepts/package-versioning#version-ranges) .</span><span class="sxs-lookup"><span data-stu-id="c9046-196">The attribute respects the rules of the [NuGet version range](/nuget/concepts/package-versioning#version-ranges) scheme.</span></span> <span data-ttu-id="c9046-197">Domyślnym zachowaniem jest wersja minimalna, włącznie.</span><span class="sxs-lookup"><span data-stu-id="c9046-197">The default behavior is a minimum version, inclusive match.</span></span> <span data-ttu-id="c9046-198">Na przykład określenie `Version="1.2.3"` jest równoznaczne z notacją NuGet `[1.2.3, )` i oznacza, że rozpoznany pakiet będzie miał wersję 1.2.3, jeśli jest dostępny lub większy w inny sposób.</span><span class="sxs-lookup"><span data-stu-id="c9046-198">For example, specifying `Version="1.2.3"` is equivalent to NuGet notation `[1.2.3, )` and means the resolved package will have the version 1.2.3 if available or greater otherwise.</span></span>

#### <a name="includeassets-excludeassets-and-privateassets"></a><span data-ttu-id="c9046-199">IncludeAssets, ExcludeAssets i PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="c9046-199">IncludeAssets, ExcludeAssets, and PrivateAssets</span></span>

<span data-ttu-id="c9046-200">`IncludeAssets`atrybut określa, które zasoby należące do pakietu określonego przez `<PackageReference>` powinny być używane.</span><span class="sxs-lookup"><span data-stu-id="c9046-200">`IncludeAssets` attribute specifies which assets belonging to the package specified by `<PackageReference>` should be consumed.</span></span> <span data-ttu-id="c9046-201">Domyślnie są uwzględniane wszystkie zasoby pakietu.</span><span class="sxs-lookup"><span data-stu-id="c9046-201">By default, all package assets are included.</span></span>

<span data-ttu-id="c9046-202">`ExcludeAssets`atrybut określa, które zasoby należące do pakietu określonego przez `<PackageReference>` nie powinny być używane.</span><span class="sxs-lookup"><span data-stu-id="c9046-202">`ExcludeAssets` attribute specifies which assets belonging to the package specified by `<PackageReference>` should not be consumed.</span></span>

<span data-ttu-id="c9046-203">`PrivateAssets`atrybut określa, które zasoby należące do pakietu określonego przez `<PackageReference>` powinny być zużywane, ale nie można ich przepływać do następnego projektu.</span><span class="sxs-lookup"><span data-stu-id="c9046-203">`PrivateAssets` attribute specifies which assets belonging to the package specified by `<PackageReference>` should be consumed but not flow to the next project.</span></span> <span data-ttu-id="c9046-204">`Analyzers` `Build` `ContentFiles` Elementy i są domyślnie prywatne, gdy ten atrybut nie jest obecny.</span><span class="sxs-lookup"><span data-stu-id="c9046-204">The `Analyzers`, `Build` and `ContentFiles` assets are private by default when this attribute is not present.</span></span>

> [!NOTE]
> <span data-ttu-id="c9046-205">`PrivateAssets`jest odpowiednikiem *project.jsw* / elemencie*xproj* `SuppressParent` .</span><span class="sxs-lookup"><span data-stu-id="c9046-205">`PrivateAssets` is equivalent to the *project.json*/*xproj* `SuppressParent` element.</span></span>

<span data-ttu-id="c9046-206">Te atrybuty mogą zawierać co najmniej jeden z następujących elementów, oddzielonych znakiem średniego, `;` Jeśli jest wyświetlany więcej niż jeden:</span><span class="sxs-lookup"><span data-stu-id="c9046-206">These attributes can contain one or more of the following items, separated by the semicolon `;` character if more than one is listed:</span></span>

- <span data-ttu-id="c9046-207">`Compile`— zawartość folderu *lib* jest dostępna do skompilowania.</span><span class="sxs-lookup"><span data-stu-id="c9046-207">`Compile` – the contents of the *lib* folder are available to compile against.</span></span>
- <span data-ttu-id="c9046-208">`Runtime`— zawartość folderu *środowiska uruchomieniowego* jest dystrybuowana.</span><span class="sxs-lookup"><span data-stu-id="c9046-208">`Runtime` – the contents of the *runtime* folder are distributed.</span></span>
- <span data-ttu-id="c9046-209">`ContentFiles`— zawartość folderu *contentfiles* jest używana.</span><span class="sxs-lookup"><span data-stu-id="c9046-209">`ContentFiles` – the contents of the *contentfiles* folder are used.</span></span>
- <span data-ttu-id="c9046-210">`Build`— są używane elementy props/targets w folderze *Build* .</span><span class="sxs-lookup"><span data-stu-id="c9046-210">`Build` – the props/targets in the *build* folder are used.</span></span>
- <span data-ttu-id="c9046-211">`Native`— zawartość zasobów natywnych jest kopiowana do folderu *wyjściowego* dla środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="c9046-211">`Native` – the contents from native assets are copied to the *output* folder for runtime.</span></span>
- <span data-ttu-id="c9046-212">`Analyzers`– Analizatory są używane.</span><span class="sxs-lookup"><span data-stu-id="c9046-212">`Analyzers` – the analyzers are used.</span></span>

<span data-ttu-id="c9046-213">Alternatywnie, atrybut może zawierać:</span><span class="sxs-lookup"><span data-stu-id="c9046-213">Alternatively, the attribute can contain:</span></span>

- <span data-ttu-id="c9046-214">`None`— żaden z elementów zawartości nie jest używany.</span><span class="sxs-lookup"><span data-stu-id="c9046-214">`None` – none of the assets are used.</span></span>
- <span data-ttu-id="c9046-215">`All`— wszystkie zasoby są używane.</span><span class="sxs-lookup"><span data-stu-id="c9046-215">`All` – all assets are used.</span></span>

### <a name="dotnetclitoolreference"></a><span data-ttu-id="c9046-216">DotNetCliToolReference</span><span class="sxs-lookup"><span data-stu-id="c9046-216">DotNetCliToolReference</span></span>

<span data-ttu-id="c9046-217">Element `<DotNetCliToolReference>` Item określa narzędzie interfejsu wiersza polecenia, które użytkownik chce przywrócić w kontekście projektu.</span><span class="sxs-lookup"><span data-stu-id="c9046-217">A `<DotNetCliToolReference>` item element specifies the CLI tool that the user wants to restore in the context of the project.</span></span> <span data-ttu-id="c9046-218">Jest to zamiennik dla `tools` węzła w *project.js*.</span><span class="sxs-lookup"><span data-stu-id="c9046-218">It's a replacement for the `tools` node in *project.json*.</span></span>

```xml
<DotNetCliToolReference Include="<package-id>" Version="" />
```

<span data-ttu-id="c9046-219">Należy pamiętać, że `DotNetCliToolReference` obecnie jest ona [przestarzała](https://github.com/dotnet/announcements/issues/107) na rzecz [lokalnych narzędzi .NET Core](./global-tools.md#install-a-local-tool).</span><span class="sxs-lookup"><span data-stu-id="c9046-219">Note that `DotNetCliToolReference` is [now deprecated](https://github.com/dotnet/announcements/issues/107) in favor of [.NET Core Local Tools](./global-tools.md#install-a-local-tool).</span></span>

#### <a name="version"></a><span data-ttu-id="c9046-220">Wersja</span><span class="sxs-lookup"><span data-stu-id="c9046-220">Version</span></span>

<span data-ttu-id="c9046-221">`Version`Określa wersję pakietu do przywrócenia.</span><span class="sxs-lookup"><span data-stu-id="c9046-221">`Version` specifies the version of the package to restore.</span></span> <span data-ttu-id="c9046-222">Ten atrybut przestrzega reguł schematu obsługi wersji programu [NuGet](/nuget/create-packages/dependency-versions#version-ranges) .</span><span class="sxs-lookup"><span data-stu-id="c9046-222">The attribute respects the rules of the [NuGet versioning](/nuget/create-packages/dependency-versions#version-ranges) scheme.</span></span> <span data-ttu-id="c9046-223">Domyślnym zachowaniem jest wersja minimalna, włącznie.</span><span class="sxs-lookup"><span data-stu-id="c9046-223">The default behavior is a minimum version, inclusive match.</span></span> <span data-ttu-id="c9046-224">Na przykład określenie `Version="1.2.3"` jest równoznaczne z notacją NuGet `[1.2.3, )` i oznacza, że rozpoznany pakiet będzie miał wersję 1.2.3, jeśli jest dostępny lub większy w inny sposób.</span><span class="sxs-lookup"><span data-stu-id="c9046-224">For example, specifying `Version="1.2.3"` is equivalent to NuGet notation `[1.2.3, )` and means the resolved package will have the version 1.2.3 if available or greater otherwise.</span></span>

### <a name="runtimeidentifiers"></a><span data-ttu-id="c9046-225">RuntimeIdentifiers</span><span class="sxs-lookup"><span data-stu-id="c9046-225">RuntimeIdentifiers</span></span>

<span data-ttu-id="c9046-226">`<RuntimeIdentifiers>`Element Property pozwala określić rozdzielaną średnikami listę [identyfikatorów środowiska uruchomieniowego (RID)](../rid-catalog.md) dla projektu.</span><span class="sxs-lookup"><span data-stu-id="c9046-226">The `<RuntimeIdentifiers>` property element lets you specify a semicolon-delimited list of [Runtime Identifiers (RIDs)](../rid-catalog.md) for the project.</span></span>
<span data-ttu-id="c9046-227">RID — umożliwia publikowanie wdrożeń samodzielnych.</span><span class="sxs-lookup"><span data-stu-id="c9046-227">RIDs enable publishing self-contained deployments.</span></span>

```xml
<RuntimeIdentifiers>win10-x64;osx.10.11-x64;ubuntu.16.04-x64</RuntimeIdentifiers>
```

### <a name="runtimeidentifier"></a><span data-ttu-id="c9046-228">RuntimeIdentifier</span><span class="sxs-lookup"><span data-stu-id="c9046-228">RuntimeIdentifier</span></span>

<span data-ttu-id="c9046-229">`<RuntimeIdentifier>`Element Property umożliwia określenie tylko jednego [identyfikatora środowiska uruchomieniowego (RID)](../rid-catalog.md) dla projektu.</span><span class="sxs-lookup"><span data-stu-id="c9046-229">The `<RuntimeIdentifier>` property element allows you to specify only one [Runtime Identifier (RID)](../rid-catalog.md) for the project.</span></span> <span data-ttu-id="c9046-230">Identyfikator RID umożliwia publikowanie samodzielnego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="c9046-230">The RID enables publishing a self-contained deployment.</span></span>

```xml
<RuntimeIdentifier>ubuntu.16.04-x64</RuntimeIdentifier>
```

<span data-ttu-id="c9046-231">`<RuntimeIdentifiers>`Zamiast tego użyj (plural), jeśli chcesz opublikować dla wielu środowisk uruchomieniowych.</span><span class="sxs-lookup"><span data-stu-id="c9046-231">Use `<RuntimeIdentifiers>` (plural) instead if you need to publish for multiple runtimes.</span></span> <span data-ttu-id="c9046-232">`<RuntimeIdentifier>`może zapewnić szybsze kompilacje, gdy wymagane jest tylko jedno środowisko uruchomieniowe.</span><span class="sxs-lookup"><span data-stu-id="c9046-232">`<RuntimeIdentifier>` can provide faster builds when only a single runtime is required.</span></span>

### <a name="packagetargetfallback"></a><span data-ttu-id="c9046-233">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="c9046-233">PackageTargetFallback</span></span>

<span data-ttu-id="c9046-234">`<PackageTargetFallback>`Element Property umożliwia określenie zestawu zgodnych elementów docelowych, które mają być używane podczas przywracania pakietów.</span><span class="sxs-lookup"><span data-stu-id="c9046-234">The `<PackageTargetFallback>` property element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="c9046-235">Została zaprojektowana tak, aby zezwalać na pakiety, które używają [TxM dotnet (target x moniker)](/nuget/schema/target-frameworks) do działania z pakietami, które nie deklarują TxM dotnet.</span><span class="sxs-lookup"><span data-stu-id="c9046-235">It's designed to allow packages that use the dotnet [TxM (Target x Moniker)](/nuget/schema/target-frameworks) to operate with packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="c9046-236">Jeśli w projekcie jest używany TxM dotnet, wszystkie pakiety, od których zależy, muszą także mieć TxM dotnet, chyba że dodasz `<PackageTargetFallback>` do projektu w celu umożliwienia zgodności z platformą dotnet.</span><span class="sxs-lookup"><span data-stu-id="c9046-236">If your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="c9046-237">W poniższym przykładzie przedstawiono rezerwy dla wszystkich obiektów docelowych w projekcie:</span><span class="sxs-lookup"><span data-stu-id="c9046-237">The following example provides the fallbacks for all targets in your project:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win8+wpa81+wp8
</PackageTargetFallback >
```

<span data-ttu-id="c9046-238">W poniższym przykładzie określono rezerwy tylko dla `netcoreapp2.1` elementu docelowego:</span><span class="sxs-lookup"><span data-stu-id="c9046-238">The following example specifies the fallbacks only for the `netcoreapp2.1` target:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netcoreapp2.1'">
    $(PackageTargetFallback);portable-net45+win8+wpa81+wp8
</PackageTargetFallback >
```

## <a name="build-events"></a><span data-ttu-id="c9046-239">Zdarzenia kompilacji</span><span class="sxs-lookup"><span data-stu-id="c9046-239">Build events</span></span>

<span data-ttu-id="c9046-240">Sposób, w jaki zdarzenia przed kompilacją i po kompilacji są określone w pliku projektu, zostały zmienione.</span><span class="sxs-lookup"><span data-stu-id="c9046-240">The way that pre-build and post-build events are specified in the project file has changed.</span></span> <span data-ttu-id="c9046-241">Właściwości PreBuildEvent i PostBuildEvent nie są zalecane w formacie projektu w stylu zestawu SDK, ponieważ makra takie jak $ (ProjectDir) nie są rozpoznawane.</span><span class="sxs-lookup"><span data-stu-id="c9046-241">The properties PreBuildEvent and PostBuildEvent are not recommended in the SDK-style project format, because macros such as $(ProjectDir) are not resolved.</span></span> <span data-ttu-id="c9046-242">Na przykład następujący kod nie jest już obsługiwany:</span><span class="sxs-lookup"><span data-stu-id="c9046-242">For example, the following code is no longer supported:</span></span>

```xml
<PropertyGroup>
    <PreBuildEvent>"$(ProjectDir)PreBuildEvent.bat" "$(ProjectDir)..\" "$(ProjectDir)" "$(TargetDir)"</PreBuildEvent>
</PropertyGroup>
```

<span data-ttu-id="c9046-243">W projektach w stylu zestawu SDK Użyj elementu docelowego programu MSBuild o nazwie `PreBuild` lub `PostBuild` i ustaw dla właściwości `BeforeTargets` Właściwość `PreBuild` lub `AfterTargets` Właściwość `PostBuild` .</span><span class="sxs-lookup"><span data-stu-id="c9046-243">In SDK-style projects, use an MSBuild target named `PreBuild` or `PostBuild` and set the `BeforeTargets` property for `PreBuild` or the `AfterTargets` property for `PostBuild`.</span></span> <span data-ttu-id="c9046-244">W poprzednim przykładzie Użyj następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="c9046-244">For the preceding example, use the following code:</span></span>

```xml
<Target Name="PreBuild" BeforeTargets="PreBuildEvent">
    <Exec Command="&quot;$(ProjectDir)PreBuildEvent.bat&quot; &quot;$(ProjectDir)..\&quot; &quot;$(ProjectDir)&quot; &quot;$(TargetDir)&quot;" />
</Target>

<Target Name="PostBuild" AfterTargets="PostBuildEvent">
   <Exec Command="echo Output written to $(TargetDir)" />
</Target>
```

> [!NOTE]
><span data-ttu-id="c9046-245">Możesz użyć dowolnej nazwy dla obiektów docelowych programu MSBuild, ale środowisko IDE programu Visual Studio rozpoznaje `PreBuild` i ma `PostBuild` elementy docelowe, dlatego zalecamy używanie tych nazw, aby można było edytować polecenia w środowisku IDE programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c9046-245">You can use any name for the MSBuild targets, but the Visual Studio IDE recognizes `PreBuild` and `PostBuild` targets, so we recommend using those names so that you can edit the commands in the Visual Studio IDE.</span></span>

## <a name="nuget-metadata-properties"></a><span data-ttu-id="c9046-246">Właściwości metadanych NuGet</span><span class="sxs-lookup"><span data-stu-id="c9046-246">NuGet metadata properties</span></span>

<span data-ttu-id="c9046-247">Po przeniesieniu do programu MSBuild przeniesiono metadane wejściowe, które są używane podczas pakowania pakietu NuGet z *project.jsna* pliki *. csproj* .</span><span class="sxs-lookup"><span data-stu-id="c9046-247">With the move to MSBuild, we have moved the input metadata that is used when packing a NuGet package from *project.json* to *.csproj* files.</span></span> <span data-ttu-id="c9046-248">Dane wejściowe są właściwościami programu MSBuild, dzięki czemu muszą one znajdować się w `<PropertyGroup>` grupie.</span><span class="sxs-lookup"><span data-stu-id="c9046-248">The inputs are MSBuild properties so they have to go within a `<PropertyGroup>` group.</span></span> <span data-ttu-id="c9046-249">Poniżej znajduje się lista właściwości, które są używane jako dane wejściowe procesu pakowania przy użyciu `dotnet pack` polecenia lub `Pack` elementu docelowego programu MSBuild, który jest częścią zestawu SDK:</span><span class="sxs-lookup"><span data-stu-id="c9046-249">The following is the list of properties that are used as inputs to the packing process when using the `dotnet pack` command or the `Pack` MSBuild target that is part of the SDK:</span></span>

### <a name="ispackable"></a><span data-ttu-id="c9046-250">Ispacking</span><span class="sxs-lookup"><span data-stu-id="c9046-250">IsPackable</span></span>

<span data-ttu-id="c9046-251">Wartość logiczna określająca, czy projekt może być spakowany.</span><span class="sxs-lookup"><span data-stu-id="c9046-251">A Boolean value that specifies whether the project can be packed.</span></span> <span data-ttu-id="c9046-252">Wartość domyślna to `true`.</span><span class="sxs-lookup"><span data-stu-id="c9046-252">The default value is `true`.</span></span>

### <a name="packageversion"></a><span data-ttu-id="c9046-253">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="c9046-253">PackageVersion</span></span>

<span data-ttu-id="c9046-254">Określa wersję, która będzie miała pakiet otrzymany.</span><span class="sxs-lookup"><span data-stu-id="c9046-254">Specifies the version that the resulting package will have.</span></span> <span data-ttu-id="c9046-255">Akceptuje wszystkie formy ciągu wersji NuGet.</span><span class="sxs-lookup"><span data-stu-id="c9046-255">Accepts all forms of NuGet version string.</span></span> <span data-ttu-id="c9046-256">Wartość domyślna to `$(Version)` , czyli Właściwość `Version` w projekcie.</span><span class="sxs-lookup"><span data-stu-id="c9046-256">Default is the value of `$(Version)`, that is, of the property `Version` in the project.</span></span>

### <a name="packageid"></a><span data-ttu-id="c9046-257">PackageId</span><span class="sxs-lookup"><span data-stu-id="c9046-257">PackageId</span></span>

<span data-ttu-id="c9046-258">Określa nazwę pakietu, który ma zostać utworzony.</span><span class="sxs-lookup"><span data-stu-id="c9046-258">Specifies the name for the resulting package.</span></span> <span data-ttu-id="c9046-259">Jeśli nie zostanie określony, `pack` operacja będzie domyślnie używać `AssemblyName` nazwy katalogu jako nazwy pakietu.</span><span class="sxs-lookup"><span data-stu-id="c9046-259">If not specified, the `pack` operation will default to using the `AssemblyName` or directory name as the name of the package.</span></span>

### <a name="title"></a><span data-ttu-id="c9046-260">Tytuł</span><span class="sxs-lookup"><span data-stu-id="c9046-260">Title</span></span>

<span data-ttu-id="c9046-261">Przyjazny dla człowieka tytuł pakietu, zazwyczaj używany w interfejsie użytkownika jako nuget.org i Menedżer pakietów w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c9046-261">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> <span data-ttu-id="c9046-262">Jeśli nie zostanie określony, zamiast niego zostanie użyty identyfikator pakietu.</span><span class="sxs-lookup"><span data-stu-id="c9046-262">If not specified, the package ID is used instead.</span></span>

### <a name="authors"></a><span data-ttu-id="c9046-263">Autorzy</span><span class="sxs-lookup"><span data-stu-id="c9046-263">Authors</span></span>

<span data-ttu-id="c9046-264">Rozdzielana średnikami lista autorów pakietów pasujących do nazw profilów w nuget.org. Są one wyświetlane w galerii NuGet w witrynie nuget.org i służą do krzyżowego odwoływania się do pakietów przez tych samych autorów.</span><span class="sxs-lookup"><span data-stu-id="c9046-264">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span>

### <a name="packagedescription"></a><span data-ttu-id="c9046-265">PackageDescription</span><span class="sxs-lookup"><span data-stu-id="c9046-265">PackageDescription</span></span>

<span data-ttu-id="c9046-266">Długi opis pakietu do wyświetlania interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c9046-266">A long description of the package for UI display.</span></span>

### <a name="description"></a><span data-ttu-id="c9046-267">Opis</span><span class="sxs-lookup"><span data-stu-id="c9046-267">Description</span></span>

<span data-ttu-id="c9046-268">Długi opis zestawu.</span><span class="sxs-lookup"><span data-stu-id="c9046-268">A long description for the assembly.</span></span> <span data-ttu-id="c9046-269">Jeśli `PackageDescription` nie jest określony, ta właściwość jest również używana jako Opis pakietu.</span><span class="sxs-lookup"><span data-stu-id="c9046-269">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span>

### <a name="copyright"></a><span data-ttu-id="c9046-270">Prawa autorskie</span><span class="sxs-lookup"><span data-stu-id="c9046-270">Copyright</span></span>

<span data-ttu-id="c9046-271">Szczegóły dotyczące praw autorskich pakietu.</span><span class="sxs-lookup"><span data-stu-id="c9046-271">Copyright details for the package.</span></span>

### <a name="packagerequirelicenseacceptance"></a><span data-ttu-id="c9046-272">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="c9046-272">PackageRequireLicenseAcceptance</span></span>

<span data-ttu-id="c9046-273">Wartość logiczna określająca, czy klient musi monitować konsumenta o zaakceptowanie licencji pakietu przed zainstalowaniem pakietu.</span><span class="sxs-lookup"><span data-stu-id="c9046-273">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> <span data-ttu-id="c9046-274">Wartość domyślna to `false`.</span><span class="sxs-lookup"><span data-stu-id="c9046-274">The default is `false`.</span></span>

### <a name="developmentdependency"></a><span data-ttu-id="c9046-275">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="c9046-275">DevelopmentDependency</span></span>

<span data-ttu-id="c9046-276">Wartość logiczna określająca, czy pakiet jest oznaczony jako zależność tylko do programowania, który uniemożliwia dołączenie pakietu jako zależności w innych pakietach.</span><span class="sxs-lookup"><span data-stu-id="c9046-276">A Boolean value that specifies whether the package is marked as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="c9046-277">W przypadku PackageReference (NuGet 4.8 +) Flaga ta oznacza również, że zasoby czasu kompilacji są wykluczone z kompilacji.</span><span class="sxs-lookup"><span data-stu-id="c9046-277">With PackageReference (NuGet 4.8+), this flag also means that compile-time assets are excluded from compilation.</span></span> <span data-ttu-id="c9046-278">Aby uzyskać więcej informacji, zobacz [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span><span class="sxs-lookup"><span data-stu-id="c9046-278">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span>

### <a name="packagelicenseexpression"></a><span data-ttu-id="c9046-279">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="c9046-279">PackageLicenseExpression</span></span>

<span data-ttu-id="c9046-280">Identyfikator lub wyrażenie [licencji SPDX](https://spdx.org/licenses/) .</span><span class="sxs-lookup"><span data-stu-id="c9046-280">An [SPDX license identifier](https://spdx.org/licenses/) or expression.</span></span> <span data-ttu-id="c9046-281">Na przykład `Apache-2.0`.</span><span class="sxs-lookup"><span data-stu-id="c9046-281">For example, `Apache-2.0`.</span></span>

<span data-ttu-id="c9046-282">Oto pełna lista [identyfikatorów licencji SPDX](https://spdx.org/licenses/).</span><span class="sxs-lookup"><span data-stu-id="c9046-282">Here is the complete list of [SPDX license identifiers](https://spdx.org/licenses/).</span></span> <span data-ttu-id="c9046-283">NuGet.org akceptuje tylko zatwierdzone licencje OSI lub FSF przy użyciu wyrażenia typu licencji.</span><span class="sxs-lookup"><span data-stu-id="c9046-283">NuGet.org accepts only OSI or FSF approved licenses when using license type expression.</span></span>

<span data-ttu-id="c9046-284">Dokładna składnia wyrażeń licencji została opisana poniżej w [ABNF](https://tools.ietf.org/html/rfc5234).</span><span class="sxs-lookup"><span data-stu-id="c9046-284">The exact syntax of the license expressions is described below in [ABNF](https://tools.ietf.org/html/rfc5234).</span></span>

```abnf
license-id            = <short form license identifier from https://spdx.org/spdx-specification-21-web-version#h.luq9dgcle9mo>

license-exception-id  = <short form license exception identifier from https://spdx.org/spdx-specification-21-web-version#h.ruv3yl8g6czd>

simple-expression = license-id / license-id”+”

compound-expression =  1*1(simple-expression /
                simple-expression "WITH" license-exception-id /
                compound-expression "AND" compound-expression /
                compound-expression "OR" compound-expression ) /
                "(" compound-expression ")" )

license-expression =  1*1(simple-expression / compound-expression / UNLICENSED)
```

> [!NOTE]
> <span data-ttu-id="c9046-285">Tylko jeden z `PackageLicenseExpression` `PackageLicenseFile` i `PackageLicenseUrl` można określić w danym momencie.</span><span class="sxs-lookup"><span data-stu-id="c9046-285">Only one of `PackageLicenseExpression`, `PackageLicenseFile` and `PackageLicenseUrl` can be specified at a time.</span></span>

### <a name="packagelicensefile"></a><span data-ttu-id="c9046-286">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="c9046-286">PackageLicenseFile</span></span>

<span data-ttu-id="c9046-287">Ścieżka do pliku licencji w pakiecie, jeśli używasz licencji, która nie ma przypisanego identyfikatora SPDX lub jest licencją niestandardową (w przeciwnym razie `PackageLicenseExpression` jest preferowana)</span><span class="sxs-lookup"><span data-stu-id="c9046-287">Path to a license file within the package if you are using a license that hasn’t been assigned an SPDX identifier, or it is a custom license (Otherwise `PackageLicenseExpression` is preferred)</span></span>

<span data-ttu-id="c9046-288">Zamienia `PackageLicenseUrl` , nie można łączyć z `PackageLicenseExpression` i wymaga programu Visual Studio w wersji 15.9.4 i .NET SDK 2.1.502 lub 2.2.101 lub nowszego.</span><span class="sxs-lookup"><span data-stu-id="c9046-288">Replaces `PackageLicenseUrl`, can't be combined with `PackageLicenseExpression`, and requires Visual Studio version 15.9.4 and .NET SDK 2.1.502 or 2.2.101 or newer.</span></span>

<span data-ttu-id="c9046-289">Należy upewnić się, że plik licencji jest spakowany przez dodanie go jawnie do projektu, przykładowe użycie:</span><span class="sxs-lookup"><span data-stu-id="c9046-289">You will need to ensure the license file is packed by adding it explicitly to the project, example usage:</span></span>

```xml
<PropertyGroup>
  <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>
<ItemGroup>
  <None Include="licenses\LICENSE.txt" Pack="true" PackagePath="$(PackageLicenseFile)"/>
</ItemGroup>
```

### <a name="packagelicenseurl"></a><span data-ttu-id="c9046-290">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="c9046-290">PackageLicenseUrl</span></span>

<span data-ttu-id="c9046-291">Adres URL do licencji, która ma zastosowanie do pakietu.</span><span class="sxs-lookup"><span data-stu-id="c9046-291">A URL to the license that is applicable to the package.</span></span> <span data-ttu-id="c9046-292">(_przestarzałe, ponieważ Visual Studio 15.9.4, .NET SDK 2.1.502 i 2.2.101_)</span><span class="sxs-lookup"><span data-stu-id="c9046-292">(_deprecated since Visual Studio 15.9.4, .NET SDK 2.1.502 and 2.2.101_)</span></span>

### <a name="packageicon"></a><span data-ttu-id="c9046-293">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="c9046-293">PackageIcon</span></span>

<span data-ttu-id="c9046-294">Ścieżka do obrazu w pakiecie do użycia jako ikona pakietu.</span><span class="sxs-lookup"><span data-stu-id="c9046-294">A path to an image in the package to use as a package icon.</span></span> <span data-ttu-id="c9046-295">Przeczytaj więcej na temat [ `icon` metadanych](/nuget/reference/nuspec#icon).</span><span class="sxs-lookup"><span data-stu-id="c9046-295">Read more about [`icon` metadata](/nuget/reference/nuspec#icon).</span></span> <span data-ttu-id="c9046-296">[PackageIconUrl jest przestarzała](/nuget/reference/msbuild-targets#packageiconurl) na rzecz PackageIcon.</span><span class="sxs-lookup"><span data-stu-id="c9046-296">[PackageIconUrl is deprecated](/nuget/reference/msbuild-targets#packageiconurl) in favor of PackageIcon.</span></span>

### <a name="packagereleasenotes"></a><span data-ttu-id="c9046-297">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="c9046-297">PackageReleaseNotes</span></span>

<span data-ttu-id="c9046-298">Informacje o wersji pakietu.</span><span class="sxs-lookup"><span data-stu-id="c9046-298">Release notes for the package.</span></span>

### <a name="packagetags"></a><span data-ttu-id="c9046-299">PackageTags</span><span class="sxs-lookup"><span data-stu-id="c9046-299">PackageTags</span></span>

<span data-ttu-id="c9046-300">Rozdzielana średnikami lista znaczników, które wyznaczają pakiet.</span><span class="sxs-lookup"><span data-stu-id="c9046-300">A semicolon-delimited list of tags that designates the package.</span></span>

### <a name="packageoutputpath"></a><span data-ttu-id="c9046-301">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="c9046-301">PackageOutputPath</span></span>

<span data-ttu-id="c9046-302">Określa ścieżkę wyjściową, w której zostanie usunięty spakowany pakiet.</span><span class="sxs-lookup"><span data-stu-id="c9046-302">Determines the output path in which the packed package will be dropped.</span></span> <span data-ttu-id="c9046-303">Wartość domyślna to `$(OutputPath)`.</span><span class="sxs-lookup"><span data-stu-id="c9046-303">Default is `$(OutputPath)`.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="c9046-304">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="c9046-304">IncludeSymbols</span></span>
<span data-ttu-id="c9046-305">Ta wartość logiczna wskazuje, czy pakiet powinien utworzyć dodatkowy pakiet symboli podczas pakowania projektu.</span><span class="sxs-lookup"><span data-stu-id="c9046-305">This Boolean value indicates whether the package should create an additional symbols package when the project is packed.</span></span> <span data-ttu-id="c9046-306">Format pakietu symboli jest kontrolowany przez `SymbolPackageFormat` Właściwość.</span><span class="sxs-lookup"><span data-stu-id="c9046-306">The symbols package's format is controlled by the `SymbolPackageFormat` property.</span></span>

### <a name="symbolpackageformat"></a><span data-ttu-id="c9046-307">SymbolPackageFormat</span><span class="sxs-lookup"><span data-stu-id="c9046-307">SymbolPackageFormat</span></span>
<span data-ttu-id="c9046-308">Określa format pakietu symboli.</span><span class="sxs-lookup"><span data-stu-id="c9046-308">Specifies the format of the symbols package.</span></span> <span data-ttu-id="c9046-309">W przypadku wystąpienia "Symbols. nupkg" zostanie utworzony pakiet ze starszymi symbolami z rozszerzeniem *. Symbols. nupkg* zawierającym plików PDB, DLL i inne pliki wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="c9046-309">If "symbols.nupkg", a legacy symbols package will be created with a *.symbols.nupkg* extension containing PDBs, DLLs, and other output files.</span></span> <span data-ttu-id="c9046-310">W przypadku elementu "snupkg" zostanie utworzony pakiet symboli snupkg zawierający przenośne plików PDB.</span><span class="sxs-lookup"><span data-stu-id="c9046-310">If "snupkg", a snupkg symbol package will be created containing the portable PDBs.</span></span> <span data-ttu-id="c9046-311">Wartość domyślna to "Symbols. nupkg".</span><span class="sxs-lookup"><span data-stu-id="c9046-311">Default is "symbols.nupkg".</span></span>

### <a name="includesource"></a><span data-ttu-id="c9046-312">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="c9046-312">IncludeSource</span></span>

<span data-ttu-id="c9046-313">Ta wartość logiczna wskazuje, czy proces pakietu powinien utworzyć pakiet źródłowy.</span><span class="sxs-lookup"><span data-stu-id="c9046-313">This Boolean value indicates whether the pack process should create a source package.</span></span> <span data-ttu-id="c9046-314">Pakiet źródłowy zawiera kod źródłowy biblioteki, a także pliki PDB.</span><span class="sxs-lookup"><span data-stu-id="c9046-314">The source package contains the library's source code as well as PDB files.</span></span> <span data-ttu-id="c9046-315">Pliki źródłowe są umieszczane w `src/ProjectName` katalogu w pliku pakietu, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="c9046-315">Source files are put under the `src/ProjectName` directory in the resulting package file.</span></span>

### <a name="istool"></a><span data-ttu-id="c9046-316">Istool</span><span class="sxs-lookup"><span data-stu-id="c9046-316">IsTool</span></span>

<span data-ttu-id="c9046-317">Określa, czy wszystkie pliki wyjściowe są kopiowane do folderu *Tools* zamiast folderu *lib* .</span><span class="sxs-lookup"><span data-stu-id="c9046-317">Specifies whether all output files are copied to the *tools* folder instead of the *lib* folder.</span></span> <span data-ttu-id="c9046-318">Różni się to od elementu `DotNetCliTool` , który jest określany przez ustawienie `PackageType` w pliku *. csproj* .</span><span class="sxs-lookup"><span data-stu-id="c9046-318">This is different from a `DotNetCliTool`, which is specified by setting the `PackageType` in the *.csproj* file.</span></span>

### <a name="repositoryurl"></a><span data-ttu-id="c9046-319">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="c9046-319">RepositoryUrl</span></span>

<span data-ttu-id="c9046-320">Określa adres URL repozytorium, w którym znajduje się kod źródłowy pakietu i/lub z którego jest tworzony.</span><span class="sxs-lookup"><span data-stu-id="c9046-320">Specifies the URL for the repository where the source code for the package resides and/or from which it's being built.</span></span>

### <a name="repositorytype"></a><span data-ttu-id="c9046-321">Repozytorium</span><span class="sxs-lookup"><span data-stu-id="c9046-321">RepositoryType</span></span>

<span data-ttu-id="c9046-322">Określa typ repozytorium.</span><span class="sxs-lookup"><span data-stu-id="c9046-322">Specifies the type of the repository.</span></span> <span data-ttu-id="c9046-323">Wartość domyślna to "Git".</span><span class="sxs-lookup"><span data-stu-id="c9046-323">Default is "git".</span></span>

### <a name="repositorybranch"></a><span data-ttu-id="c9046-324">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="c9046-324">RepositoryBranch</span></span>
<span data-ttu-id="c9046-325">Określa nazwę gałęzi źródłowej w repozytorium.</span><span class="sxs-lookup"><span data-stu-id="c9046-325">Specifies the name of the source branch in the repository.</span></span> <span data-ttu-id="c9046-326">Gdy projekt jest spakowany w pakiecie NuGet, jest dodawany do metadanych pakietu.</span><span class="sxs-lookup"><span data-stu-id="c9046-326">When the project is packaged in a NuGet package, it's added to the package metadata.</span></span>

### <a name="repositorycommit"></a><span data-ttu-id="c9046-327">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="c9046-327">RepositoryCommit</span></span>
<span data-ttu-id="c9046-328">Opcjonalne zatwierdzenie lub zestaw zmian repozytorium, aby wskazać, z którym źródłem został skompilowany pakiet.</span><span class="sxs-lookup"><span data-stu-id="c9046-328">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="c9046-329">`RepositoryUrl`należy również określić, aby ta właściwość została uwzględniona.</span><span class="sxs-lookup"><span data-stu-id="c9046-329">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="c9046-330">Gdy projekt jest spakowany w pakiecie NuGet, to zatwierdzenie lub zestaw zmian zostanie dodany do metadanych pakietu.</span><span class="sxs-lookup"><span data-stu-id="c9046-330">When the project is packaged in a NuGet package, this commit or changeset is added to the package metadata.</span></span>

### <a name="nopackageanalysis"></a><span data-ttu-id="c9046-331">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="c9046-331">NoPackageAnalysis</span></span>

<span data-ttu-id="c9046-332">Określa, że pakiet nie powinien uruchamiać analizy pakietu po skompilowaniu pakietu.</span><span class="sxs-lookup"><span data-stu-id="c9046-332">Specifies that pack should not run package analysis after building the package.</span></span>

### <a name="minclientversion"></a><span data-ttu-id="c9046-333">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="c9046-333">MinClientVersion</span></span>

<span data-ttu-id="c9046-334">Określa minimalną wersję klienta NuGet, który może zainstalować ten pakiet, wymuszony przez nuget.exe i Menedżera pakietów programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c9046-334">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span>

### <a name="includebuildoutput"></a><span data-ttu-id="c9046-335">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="c9046-335">IncludeBuildOutput</span></span>

<span data-ttu-id="c9046-336">Ta wartość logiczna określa, czy zestawy danych wyjściowych kompilacji powinny być pakowane do pliku *. nupkg* , czy nie.</span><span class="sxs-lookup"><span data-stu-id="c9046-336">This Boolean value specifies whether the build output assemblies should be packed into the *.nupkg* file or not.</span></span>

### <a name="includecontentinpack"></a><span data-ttu-id="c9046-337">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="c9046-337">IncludeContentInPack</span></span>

<span data-ttu-id="c9046-338">Ta wartość logiczna określa, czy wszystkie elementy, które mają typ, `Content` zostaną dołączone do pakietu w wyniku.</span><span class="sxs-lookup"><span data-stu-id="c9046-338">This Boolean value specifies whether any items that have a type of `Content` will be included in the resulting package automatically.</span></span> <span data-ttu-id="c9046-339">Wartość domyślna to `true`.</span><span class="sxs-lookup"><span data-stu-id="c9046-339">The default is `true`.</span></span>

### <a name="buildoutputtargetfolder"></a><span data-ttu-id="c9046-340">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="c9046-340">BuildOutputTargetFolder</span></span>

<span data-ttu-id="c9046-341">Określa folder, w którym mają zostać umieszczone zestawy wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="c9046-341">Specifies the folder where to place the output assemblies.</span></span> <span data-ttu-id="c9046-342">Zestawy wyjściowe (i inne pliki wyjściowe) są kopiowane do odpowiednich folderów struktury.</span><span class="sxs-lookup"><span data-stu-id="c9046-342">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="contenttargetfolders"></a><span data-ttu-id="c9046-343">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="c9046-343">ContentTargetFolders</span></span>

<span data-ttu-id="c9046-344">Ta właściwość określa domyślną lokalizację, w której należy wykonać wszystkie pliki zawartości, jeśli `PackagePath` nie została określona dla nich.</span><span class="sxs-lookup"><span data-stu-id="c9046-344">This property specifies the default location of where all the content files should go if `PackagePath` is not specified for them.</span></span> <span data-ttu-id="c9046-345">Wartość domyślna to "Content; contentFiles".</span><span class="sxs-lookup"><span data-stu-id="c9046-345">The default value is "content;contentFiles".</span></span>

### <a name="nuspecfile"></a><span data-ttu-id="c9046-346">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="c9046-346">NuspecFile</span></span>

<span data-ttu-id="c9046-347">Ścieżka względna lub bezwzględna do pliku *. nuspec* używanego do pakowania.</span><span class="sxs-lookup"><span data-stu-id="c9046-347">Relative or absolute path to the *.nuspec* file being used for packing.</span></span>

> [!NOTE]
> <span data-ttu-id="c9046-348">Jeśli plik *. nuspec* jest określony, jest używany **wyłącznie** na potrzeby informacji o pakowaniu i nie są używane żadne informacje w projektach.</span><span class="sxs-lookup"><span data-stu-id="c9046-348">If the *.nuspec* file is specified, it's used **exclusively** for packaging information and any information in the projects is not used.</span></span>

### <a name="nuspecbasepath"></a><span data-ttu-id="c9046-349">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="c9046-349">NuspecBasePath</span></span>

<span data-ttu-id="c9046-350">Ścieżka podstawowa pliku *. nuspec* .</span><span class="sxs-lookup"><span data-stu-id="c9046-350">Base path for the *.nuspec* file.</span></span>

### <a name="nuspecproperties"></a><span data-ttu-id="c9046-351">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="c9046-351">NuspecProperties</span></span>

<span data-ttu-id="c9046-352">Rozdzielana średnikami lista par klucz = wartość.</span><span class="sxs-lookup"><span data-stu-id="c9046-352">Semicolon separated list of key=value pairs.</span></span>

## <a name="assemblyinfo-properties"></a><span data-ttu-id="c9046-353">Właściwości AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="c9046-353">AssemblyInfo properties</span></span>

<span data-ttu-id="c9046-354">[Atrybuty zestawu](../../standard/assembly/set-attributes.md) , które były zazwyczaj obecne w pliku *AssemblyInfo* , są teraz automatycznie generowane na podstawie właściwości.</span><span class="sxs-lookup"><span data-stu-id="c9046-354">[Assembly attributes](../../standard/assembly/set-attributes.md) that were typically present in an *AssemblyInfo* file are now automatically generated from properties.</span></span>

### <a name="properties-per-attribute"></a><span data-ttu-id="c9046-355">Właściwości na atrybut</span><span class="sxs-lookup"><span data-stu-id="c9046-355">Properties per attribute</span></span>

<span data-ttu-id="c9046-356">Jak pokazano w poniższej tabeli, każdy atrybut ma właściwość, która kontroluje jej zawartość, a druga, która wyłącza jej generowanie:</span><span class="sxs-lookup"><span data-stu-id="c9046-356">As shown in the following table, each attribute has a property that controls its content and another that disables its generation:</span></span>

| <span data-ttu-id="c9046-357">Atrybut</span><span class="sxs-lookup"><span data-stu-id="c9046-357">Attribute</span></span>                                                      | <span data-ttu-id="c9046-358">Właściwość</span><span class="sxs-lookup"><span data-stu-id="c9046-358">Property</span></span>               | <span data-ttu-id="c9046-359">Właściwość do wyłączenia</span><span class="sxs-lookup"><span data-stu-id="c9046-359">Property to disable</span></span>                             |
|----------------------------------------------------------------|------------------------|-------------------------------------------------|
| <xref:System.Reflection.AssemblyCompanyAttribute>              | `Company`              | `GenerateAssemblyCompanyAttribute`              |
| <xref:System.Reflection.AssemblyConfigurationAttribute>        | `Configuration`        | `GenerateAssemblyConfigurationAttribute`        |
| <xref:System.Reflection.AssemblyCopyrightAttribute>            | `Copyright`            | `GenerateAssemblyCopyrightAttribute`            |
| <xref:System.Reflection.AssemblyDescriptionAttribute>          | `Description`          | `GenerateAssemblyDescriptionAttribute`          |
| <xref:System.Reflection.AssemblyFileVersionAttribute>          | `FileVersion`          | `GenerateAssemblyFileVersionAttribute`          |
| <xref:System.Reflection.AssemblyInformationalVersionAttribute> | `InformationalVersion` | `GenerateAssemblyInformationalVersionAttribute` |
| <xref:System.Reflection.AssemblyProductAttribute>              | `Product`              | `GenerateAssemblyProductAttribute`              |
| <xref:System.Reflection.AssemblyTitleAttribute>                | `AssemblyTitle`        | `GenerateAssemblyTitleAttribute`                |
| <xref:System.Reflection.AssemblyVersionAttribute>              | `AssemblyVersion`      | `GenerateAssemblyVersionAttribute`              |
| <xref:System.Resources.NeutralResourcesLanguageAttribute>      | `NeutralLanguage`      | `GenerateNeutralResourcesLanguageAttribute`     |

<span data-ttu-id="c9046-360">Uwagi:</span><span class="sxs-lookup"><span data-stu-id="c9046-360">Notes:</span></span>

- <span data-ttu-id="c9046-361">`AssemblyVersion`i `FileVersion` domyślnie przyjmuje wartość `$(Version)` bez sufiksu.</span><span class="sxs-lookup"><span data-stu-id="c9046-361">`AssemblyVersion` and `FileVersion` default is to take the value of `$(Version)` without suffix.</span></span> <span data-ttu-id="c9046-362">Na przykład, jeśli `$(Version)` jest `1.2.3-beta.4` , wartość będzie równa `1.2.3` .</span><span class="sxs-lookup"><span data-stu-id="c9046-362">For example, if `$(Version)` is `1.2.3-beta.4`, then the value would be `1.2.3`.</span></span>
- <span data-ttu-id="c9046-363">`InformationalVersion`wartość domyślna to `$(Version)` .</span><span class="sxs-lookup"><span data-stu-id="c9046-363">`InformationalVersion` defaults to the value of `$(Version)`.</span></span>
- <span data-ttu-id="c9046-364">`InformationalVersion``$(SourceRevisionId)`dołącza, jeśli właściwość jest obecna.</span><span class="sxs-lookup"><span data-stu-id="c9046-364">`InformationalVersion` has `$(SourceRevisionId)` appended if the property is present.</span></span> <span data-ttu-id="c9046-365">Można go wyłączyć przy użyciu `IncludeSourceRevisionInInformationalVersion` .</span><span class="sxs-lookup"><span data-stu-id="c9046-365">It can be disabled using `IncludeSourceRevisionInInformationalVersion`.</span></span>
- <span data-ttu-id="c9046-366">`Copyright`i `Description` właściwości są również używane dla metadanych narzędzia NuGet.</span><span class="sxs-lookup"><span data-stu-id="c9046-366">`Copyright` and `Description` properties are also used for NuGet metadata.</span></span>
- <span data-ttu-id="c9046-367">`Configuration`jest współużytkowany ze wszystkimi procesami kompilacji i ustawiany za pośrednictwem `--configuration` parametru `dotnet` poleceń.</span><span class="sxs-lookup"><span data-stu-id="c9046-367">`Configuration` is shared with all the build process and set via the `--configuration` parameter of `dotnet` commands.</span></span>

### <a name="generateassemblyinfo"></a><span data-ttu-id="c9046-368">GenerateAssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="c9046-368">GenerateAssemblyInfo</span></span>

<span data-ttu-id="c9046-369">Wartość logiczna, która włącza lub wyłącza wszystkie generowanie AssemblyInfo.</span><span class="sxs-lookup"><span data-stu-id="c9046-369">A Boolean that enable or disable all the AssemblyInfo generation.</span></span> <span data-ttu-id="c9046-370">Wartość domyślna to `true`.</span><span class="sxs-lookup"><span data-stu-id="c9046-370">The default value is `true`.</span></span>

### <a name="generatedassemblyinfofile"></a><span data-ttu-id="c9046-371">GeneratedAssemblyInfoFile</span><span class="sxs-lookup"><span data-stu-id="c9046-371">GeneratedAssemblyInfoFile</span></span>

<span data-ttu-id="c9046-372">Ścieżka wygenerowanego pliku informacji o zestawie.</span><span class="sxs-lookup"><span data-stu-id="c9046-372">The path of the generated assembly info file.</span></span> <span data-ttu-id="c9046-373">Domyślnie do pliku w `$(IntermediateOutputPath)` katalogu (obj).</span><span class="sxs-lookup"><span data-stu-id="c9046-373">Default to a file in the `$(IntermediateOutputPath)` (obj) directory.</span></span>
