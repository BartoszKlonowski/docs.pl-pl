---
title: Właściwości programu MSBuild dla Microsoft. NET. Sdk
description: Odwołanie do właściwości i elementów programu MSBuild, które są zrozumiałe dla zestawu .NET SDK.
ms.date: 02/14/2020
ms.topic: reference
ms.custom: updateeachrelease
ms.openlocfilehash: 3b58fd080439c73ee30d5c8dc59c50c0410db164
ms.sourcegitcommit: 45c7148f2483db2501c1aa696ab6ed2ed8cb71b2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/08/2020
ms.locfileid: "96851578"
---
# <a name="msbuild-reference-for-net-sdk-projects"></a><span data-ttu-id="feec5-103">Dokumentacja programu MSBuild dla projektów zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="feec5-103">MSBuild reference for .NET SDK projects</span></span>

<span data-ttu-id="feec5-104">Ta strona jest odwołaniem do właściwości i elementów programu MSBuild, których można użyć do konfigurowania projektów platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="feec5-104">This page is a reference for the MSBuild properties and items that you can use to configure .NET projects.</span></span>

> [!NOTE]
> <span data-ttu-id="feec5-105">Ta strona jest w toku i nie zawiera wszystkich przydatnych właściwości programu MSBuild dla zestawu .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="feec5-105">This page is a work in progress and does not list all of the useful MSBuild properties for the .NET SDK.</span></span> <span data-ttu-id="feec5-106">Aby zapoznać się z listą typowych właściwości programu MSBuild, zobacz [typowe właściwości programu MSBuild](/visualstudio/msbuild/common-msbuild-project-properties).</span><span class="sxs-lookup"><span data-stu-id="feec5-106">For a list of common MSBuild properties, see [Common MSBuild properties](/visualstudio/msbuild/common-msbuild-project-properties).</span></span>

## <a name="framework-properties"></a><span data-ttu-id="feec5-107">Właściwości struktury</span><span class="sxs-lookup"><span data-stu-id="feec5-107">Framework properties</span></span>

- [<span data-ttu-id="feec5-108">TargetFramework</span><span class="sxs-lookup"><span data-stu-id="feec5-108">TargetFramework</span></span>](#targetframework)
- [<span data-ttu-id="feec5-109">TargetFrameworks</span><span class="sxs-lookup"><span data-stu-id="feec5-109">TargetFrameworks</span></span>](#targetframeworks)
- [<span data-ttu-id="feec5-110">NetStandardImplicitPackageVersion</span><span class="sxs-lookup"><span data-stu-id="feec5-110">NetStandardImplicitPackageVersion</span></span>](#netstandardimplicitpackageversion)

### <a name="targetframework"></a><span data-ttu-id="feec5-111">TargetFramework</span><span class="sxs-lookup"><span data-stu-id="feec5-111">TargetFramework</span></span>

<span data-ttu-id="feec5-112">`TargetFramework`Właściwość określa wersję platformy docelowej dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="feec5-112">The `TargetFramework` property specifies the target framework version for the app.</span></span> <span data-ttu-id="feec5-113">Aby zapoznać się z listą prawidłowych monikerów platformy docelowej, zobacz [platformę docelową w projektach w stylu zestawu SDK](../../standard/frameworks.md#supported-target-frameworks).</span><span class="sxs-lookup"><span data-stu-id="feec5-113">For a list of valid target framework monikers, see [Target frameworks in SDK-style projects](../../standard/frameworks.md#supported-target-frameworks).</span></span>

```xml
<PropertyGroup>
  <TargetFramework>netcoreapp3.1</TargetFramework>
</PropertyGroup>
```

<span data-ttu-id="feec5-114">Aby uzyskać więcej informacji, zobacz [Platformy docelowe w projektach w stylu zestawu SDK](../../standard/frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="feec5-114">For more information, see [Target frameworks in SDK-style projects](../../standard/frameworks.md).</span></span>

### <a name="targetframeworks"></a><span data-ttu-id="feec5-115">TargetFrameworks</span><span class="sxs-lookup"><span data-stu-id="feec5-115">TargetFrameworks</span></span>

<span data-ttu-id="feec5-116">Użyj `TargetFrameworks` właściwości, jeśli chcesz, aby aplikacja była przeznaczona dla wielu platform.</span><span class="sxs-lookup"><span data-stu-id="feec5-116">Use the `TargetFrameworks` property when you want your app to target multiple platforms.</span></span> <span data-ttu-id="feec5-117">Aby zapoznać się z listą prawidłowych monikerów platformy docelowej, zobacz [platformę docelową w projektach w stylu zestawu SDK](../../standard/frameworks.md#supported-target-frameworks).</span><span class="sxs-lookup"><span data-stu-id="feec5-117">For a list of valid target framework monikers, see [Target frameworks in SDK-style projects](../../standard/frameworks.md#supported-target-frameworks).</span></span>

> [!NOTE]
> <span data-ttu-id="feec5-118">Ta właściwość jest ignorowana, jeśli `TargetFramework` określono (pojedynczo).</span><span class="sxs-lookup"><span data-stu-id="feec5-118">This property is ignored if `TargetFramework` (singular) is specified.</span></span>

```xml
<PropertyGroup>
  <TargetFrameworks>netcoreapp3.1;net462</TargetFrameworks>
</PropertyGroup>
```

<span data-ttu-id="feec5-119">Aby uzyskać więcej informacji, zobacz [Platformy docelowe w projektach w stylu zestawu SDK](../../standard/frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="feec5-119">For more information, see [Target frameworks in SDK-style projects](../../standard/frameworks.md).</span></span>

### <a name="netstandardimplicitpackageversion"></a><span data-ttu-id="feec5-120">NetStandardImplicitPackageVersion</span><span class="sxs-lookup"><span data-stu-id="feec5-120">NetStandardImplicitPackageVersion</span></span>

> [!NOTE]
> <span data-ttu-id="feec5-121">Ta właściwość ma zastosowanie tylko do projektów korzystających z programu `netstandard1.x` .</span><span class="sxs-lookup"><span data-stu-id="feec5-121">This property only applies to projects using `netstandard1.x`.</span></span> <span data-ttu-id="feec5-122">Nie dotyczy to projektów, które używają `netstandard2.x` .</span><span class="sxs-lookup"><span data-stu-id="feec5-122">It doesn't apply to projects that use `netstandard2.x`.</span></span>

<span data-ttu-id="feec5-123">Użyj `NetStandardImplicitPackageVersion` właściwości, aby określić wersję platformy, która jest starsza niż wersja pakietu.</span><span class="sxs-lookup"><span data-stu-id="feec5-123">Use the `NetStandardImplicitPackageVersion` property when you want to specify a framework version that's lower than the metapackage version.</span></span> <span data-ttu-id="feec5-124">Plik projektu w poniższym przykładzie docelowym `netstandard1.3` , ale używa wersji 1.6.0 `NETStandard.Library` .</span><span class="sxs-lookup"><span data-stu-id="feec5-124">The project file in the following example targets `netstandard1.3` but uses the 1.6.0 version of `NETStandard.Library`.</span></span>

```xml
<PropertyGroup>
  <TargetFramework>netstandard1.3</TargetFramework>
  <NetStandardImplicitPackageVersion>1.6.0</NetStandardImplicitPackageVersion>
</PropertyGroup>
```

## <a name="package-properties"></a><span data-ttu-id="feec5-125">Właściwości pakietu</span><span class="sxs-lookup"><span data-stu-id="feec5-125">Package properties</span></span>

<span data-ttu-id="feec5-126">Można określić właściwości, takie jak `PackageId` ,,, `PackageVersion` `PackageIcon` `Title` i, `Description` aby opisać pakiet, który zostanie utworzony na podstawie projektu.</span><span class="sxs-lookup"><span data-stu-id="feec5-126">You can specify properties such as `PackageId`, `PackageVersion`, `PackageIcon`, `Title`, and `Description` to describe the package that gets created from your project.</span></span> <span data-ttu-id="feec5-127">Aby uzyskać informacje o tych i innych właściwościach, zobacz [pakiet Target](/nuget/reference/msbuild-targets#pack-target).</span><span class="sxs-lookup"><span data-stu-id="feec5-127">For information about these and other properties, see [pack target](/nuget/reference/msbuild-targets#pack-target).</span></span>

```xml
<PropertyGroup>
  ...
  <PackageId>ClassLibDotNetStandard</PackageId>
  <Version>1.0.0</Version>
  <Authors>John Doe</Authors>
  <Company>Contoso</Company>
</PropertyGroup>
```

## <a name="publish-properties-and-items"></a><span data-ttu-id="feec5-128">Publikowanie właściwości i elementów</span><span class="sxs-lookup"><span data-stu-id="feec5-128">Publish properties and items</span></span>

- [<span data-ttu-id="feec5-129">CopyLocalLockFileAssemblies</span><span class="sxs-lookup"><span data-stu-id="feec5-129">CopyLocalLockFileAssemblies</span></span>](#copylocallockfileassemblies)
- [<span data-ttu-id="feec5-130">RuntimeIdentifier</span><span class="sxs-lookup"><span data-stu-id="feec5-130">RuntimeIdentifier</span></span>](#runtimeidentifier)
- [<span data-ttu-id="feec5-131">RuntimeIdentifiers</span><span class="sxs-lookup"><span data-stu-id="feec5-131">RuntimeIdentifiers</span></span>](#runtimeidentifiers)
- [<span data-ttu-id="feec5-132">TrimmerRootAssembly</span><span class="sxs-lookup"><span data-stu-id="feec5-132">TrimmerRootAssembly</span></span>](#trimmerrootassembly)
- [<span data-ttu-id="feec5-133">UseAppHost</span><span class="sxs-lookup"><span data-stu-id="feec5-133">UseAppHost</span></span>](#useapphost)

### <a name="copylocallockfileassemblies"></a><span data-ttu-id="feec5-134">CopyLocalLockFileAssemblies</span><span class="sxs-lookup"><span data-stu-id="feec5-134">CopyLocalLockFileAssemblies</span></span>

<span data-ttu-id="feec5-135">`CopyLocalLockFileAssemblies`Właściwość jest przydatna w przypadku projektów wtyczek, które mają zależności od innych bibliotek.</span><span class="sxs-lookup"><span data-stu-id="feec5-135">The `CopyLocalLockFileAssemblies` property is useful for plugin projects that have dependencies on other libraries.</span></span> <span data-ttu-id="feec5-136">W przypadku ustawienia tej właściwości na wartość `true` wszystkie zależności pakietów NuGet są kopiowane do katalogu wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="feec5-136">If you set this property to `true`, any NuGet package dependencies are copied to the output directory.</span></span> <span data-ttu-id="feec5-137">Oznacza to, że możesz użyć danych wyjściowych programu, `dotnet build` Aby uruchomić wtyczkę na dowolnym komputerze.</span><span class="sxs-lookup"><span data-stu-id="feec5-137">That means you can use the output of `dotnet build` to run your plugin on any machine.</span></span>

```xml
<PropertyGroup>
  <CopyLocalLockFileAssemblies>true</CopyLocalLockFileAssemblies>
</PropertyGroup>
```

> [!TIP]
> <span data-ttu-id="feec5-138">Alternatywnie można użyć `dotnet publish` programu do opublikowania biblioteki klas.</span><span class="sxs-lookup"><span data-stu-id="feec5-138">Alternatively, you can use `dotnet publish` to publish the class library.</span></span> <span data-ttu-id="feec5-139">Aby uzyskać więcej informacji, zobacz [dotnet Publish](../tools/dotnet-publish.md).</span><span class="sxs-lookup"><span data-stu-id="feec5-139">For more information, see [dotnet publish](../tools/dotnet-publish.md).</span></span>

### <a name="runtimeidentifier"></a><span data-ttu-id="feec5-140">RuntimeIdentifier</span><span class="sxs-lookup"><span data-stu-id="feec5-140">RuntimeIdentifier</span></span>

<span data-ttu-id="feec5-141">`RuntimeIdentifier`Właściwość umożliwia określenie pojedynczego [identyfikatora środowiska uruchomieniowego (RID)](../rid-catalog.md) dla projektu.</span><span class="sxs-lookup"><span data-stu-id="feec5-141">The `RuntimeIdentifier` property lets you specify a single [runtime identifier (RID)](../rid-catalog.md) for the project.</span></span> <span data-ttu-id="feec5-142">Identyfikator RID umożliwia publikowanie samodzielnego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="feec5-142">The RID enables publishing a self-contained deployment.</span></span>

```xml
<PropertyGroup>
  <RuntimeIdentifier>ubuntu.16.04-x64</RuntimeIdentifier>
</PropertyGroup>
```

### <a name="runtimeidentifiers"></a><span data-ttu-id="feec5-143">RuntimeIdentifiers</span><span class="sxs-lookup"><span data-stu-id="feec5-143">RuntimeIdentifiers</span></span>

<span data-ttu-id="feec5-144">`RuntimeIdentifiers`Właściwość pozwala określić rozdzielaną średnikami listę [identyfikatorów środowiska uruchomieniowego (RID)](../rid-catalog.md) dla projektu.</span><span class="sxs-lookup"><span data-stu-id="feec5-144">The `RuntimeIdentifiers` property lets you specify a semicolon-delimited list of [runtime identifiers (RIDs)](../rid-catalog.md) for the project.</span></span> <span data-ttu-id="feec5-145">Użyj tej właściwości, jeśli chcesz opublikować dla wielu środowisk uruchomieniowych.</span><span class="sxs-lookup"><span data-stu-id="feec5-145">Use this property if you need to publish for multiple runtimes.</span></span> <span data-ttu-id="feec5-146">`RuntimeIdentifiers` jest używany podczas przywracania, aby upewnić się, że odpowiednie zasoby znajdują się na wykresie.</span><span class="sxs-lookup"><span data-stu-id="feec5-146">`RuntimeIdentifiers` is used at restore time to ensure the right assets are in the graph.</span></span>

> [!TIP]
> <span data-ttu-id="feec5-147">`RuntimeIdentifier` (pojedyncze) może zapewnić szybsze kompilacje, gdy wymagane jest tylko jedno środowisko uruchomieniowe.</span><span class="sxs-lookup"><span data-stu-id="feec5-147">`RuntimeIdentifier` (singular) can provide faster builds when only a single runtime is required.</span></span>

```xml
<PropertyGroup>
  <RuntimeIdentifiers>win10-x64;osx.10.11-x64;ubuntu.16.04-x64</RuntimeIdentifiers>
</PropertyGroup>
```

### <a name="trimmerrootassembly"></a><span data-ttu-id="feec5-148">TrimmerRootAssembly</span><span class="sxs-lookup"><span data-stu-id="feec5-148">TrimmerRootAssembly</span></span>

<span data-ttu-id="feec5-149">`TrimmerRootAssembly`Element umożliwia wykluczenie zestawu z [*przycinania*](../deploying/trim-self-contained.md).</span><span class="sxs-lookup"><span data-stu-id="feec5-149">The `TrimmerRootAssembly` item lets you exclude an assembly from [*trimming*](../deploying/trim-self-contained.md).</span></span> <span data-ttu-id="feec5-150">Przycinanie jest procesem usuwania nieużywanych części środowiska uruchomieniowego z spakowanej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="feec5-150">Trimming is the process of removing unused parts of the runtime from a packaged application.</span></span> <span data-ttu-id="feec5-151">W niektórych przypadkach przycinanie może niepoprawnie usunąć wymagane odwołania.</span><span class="sxs-lookup"><span data-stu-id="feec5-151">In some cases, trimming might incorrectly remove required references.</span></span>

<span data-ttu-id="feec5-152">Poniższy kod XML wyklucza `System.Security` zestaw z przycinania.</span><span class="sxs-lookup"><span data-stu-id="feec5-152">The following XML excludes the `System.Security` assembly from trimming.</span></span>

```xml
<ItemGroup>
  <TrimmerRootAssembly Include="System.Security" />
</ItemGroup>
```

### <a name="useapphost"></a><span data-ttu-id="feec5-153">UseAppHost</span><span class="sxs-lookup"><span data-stu-id="feec5-153">UseAppHost</span></span>

<span data-ttu-id="feec5-154">`UseAppHost`Właściwość określa, czy dla wdrożenia jest tworzony natywny plik wykonywalny.</span><span class="sxs-lookup"><span data-stu-id="feec5-154">The `UseAppHost` property controls whether or not a native executable is created for a deployment.</span></span> <span data-ttu-id="feec5-155">Natywny plik wykonywalny jest wymagany w przypadku wdrożeń samodzielnych.</span><span class="sxs-lookup"><span data-stu-id="feec5-155">A native executable is required for self-contained deployments.</span></span>

<span data-ttu-id="feec5-156">W programie .NET Core 3,0 i jego nowszych wersjach domyślnie tworzony jest plik wykonywalny zależny od platformy.</span><span class="sxs-lookup"><span data-stu-id="feec5-156">In .NET Core 3.0 and later versions, a framework-dependent executable is created by default.</span></span> <span data-ttu-id="feec5-157">Ustaw `UseAppHost` Właściwość na `false` , aby wyłączyć generowanie pliku wykonywalnego.</span><span class="sxs-lookup"><span data-stu-id="feec5-157">Set the `UseAppHost` property to `false` to disable generation of the executable.</span></span>

```xml
<PropertyGroup>
  <UseAppHost>false</UseAppHost>
</PropertyGroup>
```

<span data-ttu-id="feec5-158">Aby uzyskać więcej informacji o wdrażaniu, zobacz [wdrażanie aplikacji .NET](../deploying/index.md).</span><span class="sxs-lookup"><span data-stu-id="feec5-158">For more information about deployment, see [.NET application deployment](../deploying/index.md).</span></span>

## <a name="compile-properties"></a><span data-ttu-id="feec5-159">Kompiluj właściwości</span><span class="sxs-lookup"><span data-stu-id="feec5-159">Compile properties</span></span>

- [<span data-ttu-id="feec5-160">EmbeddedResourceUseDependentUponConvention</span><span class="sxs-lookup"><span data-stu-id="feec5-160">EmbeddedResourceUseDependentUponConvention</span></span>](#embeddedresourceusedependentuponconvention)
- [<span data-ttu-id="feec5-161">LangVersion</span><span class="sxs-lookup"><span data-stu-id="feec5-161">LangVersion</span></span>](#langversion)

### <a name="embeddedresourceusedependentuponconvention"></a><span data-ttu-id="feec5-162">EmbeddedResourceUseDependentUponConvention</span><span class="sxs-lookup"><span data-stu-id="feec5-162">EmbeddedResourceUseDependentUponConvention</span></span>

<span data-ttu-id="feec5-163">`EmbeddedResourceUseDependentUponConvention`Właściwość określa, czy nazwy plików manifestu zasobów są generowane na podstawie informacji o typie w plikach źródłowych, które znajdują się w plikach zasobów.</span><span class="sxs-lookup"><span data-stu-id="feec5-163">The `EmbeddedResourceUseDependentUponConvention` property defines whether resource manifest file names are generated from type information in source files that are colocated with resource files.</span></span> <span data-ttu-id="feec5-164">Na przykład jeśli *Form1. resx* znajduje się w tym samym folderze co *Form1.cs* i `EmbeddedResourceUseDependentUponConvention` jest ustawiona na `true` , wygenerowany plik *resources* przyjmuje swoją nazwę z pierwszego typu zdefiniowanego w *Form1.cs*.</span><span class="sxs-lookup"><span data-stu-id="feec5-164">For example, if *Form1.resx* is in the same folder as *Form1.cs*, and `EmbeddedResourceUseDependentUponConvention` is set to `true`, the generated *.resources* file takes its name from the first type that's defined in *Form1.cs*.</span></span> <span data-ttu-id="feec5-165">Na przykład, jeśli `MyNamespace.Form1` jest pierwszym typem zdefiniowanym w *Form1.cs*, wygenerowana nazwa pliku ma *nazwę. Form1. resources*.</span><span class="sxs-lookup"><span data-stu-id="feec5-165">For example, if `MyNamespace.Form1` is the first type defined in *Form1.cs*, the generated file name is *MyNamespace.Form1.resources*.</span></span>

> [!NOTE]
> <span data-ttu-id="feec5-166">Jeśli `LogicalName` `ManifestResourceName` `DependentUpon` dla elementu określono wartość, lub lub metadanych `EmbeddedResource` , wygenerowana nazwa pliku manifestu dla tego pliku zasobów jest oparta na tym metadanych.</span><span class="sxs-lookup"><span data-stu-id="feec5-166">If `LogicalName`, `ManifestResourceName`, or `DependentUpon` metadata is specified for an `EmbeddedResource` item, the generated manifest file name for that resource file is based on that metadata instead.</span></span>

<span data-ttu-id="feec5-167">Domyślnie w nowym projekcie .NET ta właściwość jest ustawiona na `true` .</span><span class="sxs-lookup"><span data-stu-id="feec5-167">By default, in a new .NET project, this property is set to `true`.</span></span> <span data-ttu-id="feec5-168">Jeśli `false` `LogicalName` `ManifestResourceName` dla elementu w pliku projektu zostanie ustawiona wartość, i nie, lub `DependentUpon` dla tego parametru, `EmbeddedResource` Nazwa pliku manifestu zasobu jest oparta na głównej przestrzeni nazw projektu i względnej ścieżce pliku do pliku *resx* .</span><span class="sxs-lookup"><span data-stu-id="feec5-168">If set to `false`, and no `LogicalName`, `ManifestResourceName`, or `DependentUpon` metadata is specified for the `EmbeddedResource` item in the project file, the resource manifest file name is based off the root namespace for the project and the relative file path to the *.resx* file.</span></span> <span data-ttu-id="feec5-169">Aby uzyskać więcej informacji, zobacz [jak nazywa się plik manifestu zasobu](../resources/manifest-file-names.md).</span><span class="sxs-lookup"><span data-stu-id="feec5-169">For more information, see [How resource manifest files are named](../resources/manifest-file-names.md).</span></span>

```xml
<PropertyGroup>
  <EmbeddedResourceUseDependentUponConvention>true</EmbeddedResourceUseDependentUponConvention>
</PropertyGroup>
```

### <a name="langversion"></a><span data-ttu-id="feec5-170">LangVersion</span><span class="sxs-lookup"><span data-stu-id="feec5-170">LangVersion</span></span>

<span data-ttu-id="feec5-171">`LangVersion`Właściwość umożliwia określenie konkretnej wersji języka programowania.</span><span class="sxs-lookup"><span data-stu-id="feec5-171">The `LangVersion` property lets you specify a specific programming language version.</span></span> <span data-ttu-id="feec5-172">Na przykład jeśli chcesz uzyskać dostęp do funkcji wersji zapoznawczej języka C#, ustaw wartość `LangVersion` `preview` .</span><span class="sxs-lookup"><span data-stu-id="feec5-172">For example, if you want access to C# preview features, set `LangVersion` to `preview`.</span></span>

```xml
<PropertyGroup>
  <LangVersion>preview</LangVersion>
</PropertyGroup>
```

<span data-ttu-id="feec5-173">Aby uzyskać więcej informacji, zobacz [wersja języka C#](../../csharp/language-reference/configure-language-version.md#override-a-default).</span><span class="sxs-lookup"><span data-stu-id="feec5-173">For more information, see [C# language versioning](../../csharp/language-reference/configure-language-version.md#override-a-default).</span></span>

## <a name="code-analysis-properties"></a><span data-ttu-id="feec5-174">Właściwości analizy kodu</span><span class="sxs-lookup"><span data-stu-id="feec5-174">Code analysis properties</span></span>

### <a name="analysislevel"></a><span data-ttu-id="feec5-175">AnalysisLevel</span><span class="sxs-lookup"><span data-stu-id="feec5-175">AnalysisLevel</span></span>

<span data-ttu-id="feec5-176">`AnalysisLevel`Właściwość pozwala określić poziom analizy kodu.</span><span class="sxs-lookup"><span data-stu-id="feec5-176">The `AnalysisLevel` property lets you specify a code analysis level.</span></span> <span data-ttu-id="feec5-177">Jeśli na przykład chcesz uzyskać dostęp do analizatorów kodu w wersji zapoznawczej, ustaw wartość `AnalysisLevel` `preview` .</span><span class="sxs-lookup"><span data-stu-id="feec5-177">For example, if you want access to preview code analyzers, set `AnalysisLevel` to `preview`.</span></span> <span data-ttu-id="feec5-178">Wartość domyślna to `latest`.</span><span class="sxs-lookup"><span data-stu-id="feec5-178">The default value is `latest`.</span></span>

```xml
<PropertyGroup>
  <AnalysisLevel>preview</AnalysisLevel>
</PropertyGroup>
```

<span data-ttu-id="feec5-179">W poniższej tabeli przedstawiono dostępne opcje.</span><span class="sxs-lookup"><span data-stu-id="feec5-179">The following table shows the available options.</span></span>

| <span data-ttu-id="feec5-180">Wartość</span><span class="sxs-lookup"><span data-stu-id="feec5-180">Value</span></span> | <span data-ttu-id="feec5-181">Znaczenie</span><span class="sxs-lookup"><span data-stu-id="feec5-181">Meaning</span></span> |
|-|-|
| `latest` | <span data-ttu-id="feec5-182">Używane są najnowsze analizatory kodu, które zostały wydane.</span><span class="sxs-lookup"><span data-stu-id="feec5-182">The latest code analyzers that have been released are used.</span></span> <span data-ttu-id="feec5-183">Jest to opcja domyślna.</span><span class="sxs-lookup"><span data-stu-id="feec5-183">This is the default.</span></span> |
| `preview` | <span data-ttu-id="feec5-184">Są używane najnowsze analizatory kodu, nawet jeśli są one w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="feec5-184">The latest code analyzers are used, even if they are in preview.</span></span> |
| `5.0` | <span data-ttu-id="feec5-185">Używany jest zestaw reguł, które zostały włączone dla wydania .NET 5,0, nawet jeśli są dostępne nowsze reguły.</span><span class="sxs-lookup"><span data-stu-id="feec5-185">The set of rules that was enabled for the .NET 5.0 release is used, even if newer rules are available.</span></span> |
| `5` | <span data-ttu-id="feec5-186">Używany jest zestaw reguł, które zostały włączone dla wydania .NET 5,0, nawet jeśli są dostępne nowsze reguły.</span><span class="sxs-lookup"><span data-stu-id="feec5-186">The set of rules that was enabled for the .NET 5.0 release is used, even if newer rules are available.</span></span> |

### <a name="analysismode"></a><span data-ttu-id="feec5-187">Analizamode</span><span class="sxs-lookup"><span data-stu-id="feec5-187">AnalysisMode</span></span>

<span data-ttu-id="feec5-188">Począwszy od platformy .NET 5,0, zestaw SDK platformy .NET jest dostarczany ze wszystkimi [regułami dotyczącymi jakości kodu "CA"](../../fundamentals/code-analysis/quality-rules/index.md).</span><span class="sxs-lookup"><span data-stu-id="feec5-188">Starting with .NET 5.0, the .NET SDK ships with all of the ["CA" code quality rules](../../fundamentals/code-analysis/quality-rules/index.md).</span></span> <span data-ttu-id="feec5-189">Domyślnie tylko [niektóre reguły są włączane](../../fundamentals/code-analysis/overview.md#enabled-rules) jako ostrzeżenia kompilacji.</span><span class="sxs-lookup"><span data-stu-id="feec5-189">By default, only [some rules are enabled](../../fundamentals/code-analysis/overview.md#enabled-rules) as build warnings.</span></span> <span data-ttu-id="feec5-190">`AnalysisMode`Właściwość umożliwia dostosowanie zestawu reguł, które są domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="feec5-190">The `AnalysisMode` property lets you customize the set of rules that are enabled by default.</span></span> <span data-ttu-id="feec5-191">Można przełączać się na bardziej agresywny tryb analizy lub bardziej ostrożny tryb analizy.</span><span class="sxs-lookup"><span data-stu-id="feec5-191">You can either switch to a more aggressive (opt-out) analysis mode or a more conservative (opt-in) analysis mode.</span></span> <span data-ttu-id="feec5-192">Na przykład jeśli chcesz włączyć wszystkie reguły domyślnie jako ostrzeżenia kompilacji, ustaw wartość na `AllEnabledByDefault` .</span><span class="sxs-lookup"><span data-stu-id="feec5-192">For example, if you want to enable all rules by default as build warnings, set the value to `AllEnabledByDefault`.</span></span>

```xml
<PropertyGroup>
  <AnalysisMode>AllEnabledByDefault</AnalysisMode>
</PropertyGroup>
```

<span data-ttu-id="feec5-193">W poniższej tabeli przedstawiono dostępne opcje.</span><span class="sxs-lookup"><span data-stu-id="feec5-193">The following table shows the available options.</span></span>

| <span data-ttu-id="feec5-194">Wartość</span><span class="sxs-lookup"><span data-stu-id="feec5-194">Value</span></span> | <span data-ttu-id="feec5-195">Znaczenie</span><span class="sxs-lookup"><span data-stu-id="feec5-195">Meaning</span></span> |
|-|-|
| `Default` | <span data-ttu-id="feec5-196">Domyślny tryb, w którym niektóre reguły są włączone jako ostrzeżenia kompilacji, niektóre reguły są włączane jako sugestie środowiska IDE programu Visual Studio, a reszta jest wyłączona.</span><span class="sxs-lookup"><span data-stu-id="feec5-196">Default mode, where certain rules are enabled as build warnings, certain rules are enabled as Visual Studio IDE suggestions, and the remainder are disabled.</span></span> |
| `AllEnabledByDefault` | <span data-ttu-id="feec5-197">Tryb agresywny lub rezygnacji, w którym wszystkie reguły są domyślnie włączone jako ostrzeżenia kompilacji.</span><span class="sxs-lookup"><span data-stu-id="feec5-197">Aggressive or opt-out mode, where all rules are enabled by default as build warnings.</span></span> <span data-ttu-id="feec5-198">Możesz selektywnie [zrezygnować](../../fundamentals/code-analysis/configuration-options.md) z poszczególnych reguł, aby je wyłączyć.</span><span class="sxs-lookup"><span data-stu-id="feec5-198">You can selectively [opt out](../../fundamentals/code-analysis/configuration-options.md) of individual rules to disable them.</span></span> |
| `AllDisabledByDefault` | <span data-ttu-id="feec5-199">Tryb wyłączania lub niewłączania, gdzie wszystkie reguły są domyślnie wyłączone.</span><span class="sxs-lookup"><span data-stu-id="feec5-199">Conservative or opt-in mode, where all rules are disabled by default.</span></span> <span data-ttu-id="feec5-200">Można [wybiórczo](../../fundamentals/code-analysis/configuration-options.md) wybierać poszczególne reguły, aby je włączyć.</span><span class="sxs-lookup"><span data-stu-id="feec5-200">You can selectively [opt into](../../fundamentals/code-analysis/configuration-options.md) individual rules to enable them.</span></span> |

### <a name="codeanalysistreatwarningsaserrors"></a><span data-ttu-id="feec5-201">CodeAnalysisTreatWarningsAsErrors</span><span class="sxs-lookup"><span data-stu-id="feec5-201">CodeAnalysisTreatWarningsAsErrors</span></span>

<span data-ttu-id="feec5-202">`CodeAnalysisTreatWarningsAsErrors`Właściwość umożliwia skonfigurowanie, czy ostrzeżenia analizy jakości kodu (CAxxxx) powinny być traktowane jako ostrzeżenia i przerywać kompilację.</span><span class="sxs-lookup"><span data-stu-id="feec5-202">The `CodeAnalysisTreatWarningsAsErrors` property lets you configure whether code quality analysis warnings (CAxxxx) should be treated as warnings and break the build.</span></span> <span data-ttu-id="feec5-203">Jeśli używasz `-warnaserror` flagi podczas kompilowania projektów, ostrzeżenia [analizy jakości kodu platformy .NET](../../fundamentals/code-analysis/overview.md#code-quality-analysis) również są traktowane jako błędy.</span><span class="sxs-lookup"><span data-stu-id="feec5-203">If you use the `-warnaserror` flag when you build your projects, [.NET code quality analysis](../../fundamentals/code-analysis/overview.md#code-quality-analysis) warnings are also treated as errors.</span></span> <span data-ttu-id="feec5-204">Jeśli nie chcesz, aby ostrzeżenia analizy jakości kodu były traktowane jako błędy, możesz ustawić `CodeAnalysisTreatWarningsAsErrors` Właściwość programu MSBuild na `false` w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="feec5-204">If you do not want code quality analysis warnings to be treated as errors, you can set the `CodeAnalysisTreatWarningsAsErrors` MSBuild property to `false` in your project file.</span></span>

```xml
<PropertyGroup>
  <CodeAnalysisTreatWarningsAsErrors>false</CodeAnalysisTreatWarningsAsErrors>
</PropertyGroup>
```

### <a name="enablenetanalyzers"></a><span data-ttu-id="feec5-205">EnableNETAnalyzers</span><span class="sxs-lookup"><span data-stu-id="feec5-205">EnableNETAnalyzers</span></span>

<span data-ttu-id="feec5-206">[Analiza jakości kodu platformy .NET](../../fundamentals/code-analysis/overview.md#code-quality-analysis) jest domyślnie włączona dla projektów przeznaczonych dla platformy .NET 5,0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="feec5-206">[.NET code quality analysis](../../fundamentals/code-analysis/overview.md#code-quality-analysis) is enabled, by default, for projects that target .NET 5.0 or later.</span></span> <span data-ttu-id="feec5-207">Można włączyć analizę kodu platformy .NET dla projektów przeznaczonych dla wcześniejszych wersji platformy .NET przez ustawienie `EnableNETAnalyzers` właściwości na `true` .</span><span class="sxs-lookup"><span data-stu-id="feec5-207">You can enable .NET code analysis for projects that target earlier versions of .NET by setting the `EnableNETAnalyzers` property to `true`.</span></span> <span data-ttu-id="feec5-208">Aby wyłączyć analizę kodu w dowolnym projekcie, należy ustawić tę właściwość na `false` .</span><span class="sxs-lookup"><span data-stu-id="feec5-208">To disable code analysis in any project, set this property to `false`.</span></span>

```xml
<PropertyGroup>
  <EnableNETAnalyzers>true</EnableNETAnalyzers>
</PropertyGroup>
```

> [!TIP]
> <span data-ttu-id="feec5-209">Innym sposobem na włączenie analizy kodu .NET dla projektów przeznaczonych dla wersji .NET wcześniejszych niż .NET 5,0 jest ustawienie właściwości [AnalysisLevel](#analysislevel) na `latest` .</span><span class="sxs-lookup"><span data-stu-id="feec5-209">Another way to enable .NET code analysis on projects that target .NET versions prior to .NET 5.0 is to set the [AnalysisLevel](#analysislevel) property to `latest`.</span></span>

### <a name="enforcecodestyleinbuild"></a><span data-ttu-id="feec5-210">EnforceCodeStyleInBuild</span><span class="sxs-lookup"><span data-stu-id="feec5-210">EnforceCodeStyleInBuild</span></span>

> [!NOTE]
> <span data-ttu-id="feec5-211">Ta funkcja jest obecnie eksperymentalna i może ulec zmianie między wersjami .NET 5 i .NET 6.</span><span class="sxs-lookup"><span data-stu-id="feec5-211">This feature is currently experimental and may change between the .NET 5 and .NET 6 releases.</span></span>

<span data-ttu-id="feec5-212">[Analiza stylu kodu platformy .NET](../../fundamentals/code-analysis/overview.md#code-style-analysis) jest domyślnie wyłączona w przypadku kompilacji dla wszystkich projektów .NET.</span><span class="sxs-lookup"><span data-stu-id="feec5-212">[.NET code style analysis](../../fundamentals/code-analysis/overview.md#code-style-analysis) is disabled, by default, on build for all .NET projects.</span></span> <span data-ttu-id="feec5-213">Można włączyć analizę stylu kodu dla projektów .NET, ustawiając `EnforceCodeStyleInBuild` Właściwość na `true` .</span><span class="sxs-lookup"><span data-stu-id="feec5-213">You can enable code style analysis for .NET projects by setting the `EnforceCodeStyleInBuild` property to `true`.</span></span>

```xml
<PropertyGroup>
  <EnforceCodeStyleInBuild>true</EnforceCodeStyleInBuild>
</PropertyGroup>
```

<span data-ttu-id="feec5-214">Wszystkie reguły stylu kodu, które są [skonfigurowane](../../fundamentals/code-analysis/overview.md#code-style-analysis) do wyświetlania ostrzeżeń lub błędów, będą wykonywane w przypadku naruszeń kompilacji i raportu.</span><span class="sxs-lookup"><span data-stu-id="feec5-214">All code style rules that are [configured](../../fundamentals/code-analysis/overview.md#code-style-analysis) to be warnings or errors will execute on build and report violations.</span></span>

## <a name="run-time-configuration-properties"></a><span data-ttu-id="feec5-215">Właściwości konfiguracji czasu wykonywania</span><span class="sxs-lookup"><span data-stu-id="feec5-215">Run-time configuration properties</span></span>

<span data-ttu-id="feec5-216">Niektóre zachowania w czasie wykonywania można skonfigurować, określając właściwości programu MSBuild w pliku projektu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="feec5-216">You can configure some run-time behaviors by specifying MSBuild properties in the project file of the app.</span></span> <span data-ttu-id="feec5-217">Aby uzyskać informacje na temat innych sposobów konfigurowania zachowania w czasie wykonywania, zobacz [Ustawienia konfiguracji w czasie wykonywania](../run-time-config/index.md).</span><span class="sxs-lookup"><span data-stu-id="feec5-217">For information about other ways of configuring run-time behavior, see [Run-time configuration settings](../run-time-config/index.md).</span></span>

- [<span data-ttu-id="feec5-218">ConcurrentGarbageCollection</span><span class="sxs-lookup"><span data-stu-id="feec5-218">ConcurrentGarbageCollection</span></span>](#concurrentgarbagecollection)
- [<span data-ttu-id="feec5-219">InvariantGlobalization</span><span class="sxs-lookup"><span data-stu-id="feec5-219">InvariantGlobalization</span></span>](#invariantglobalization)
- [<span data-ttu-id="feec5-220">RetainVMGarbageCollection</span><span class="sxs-lookup"><span data-stu-id="feec5-220">RetainVMGarbageCollection</span></span>](#retainvmgarbagecollection)
- [<span data-ttu-id="feec5-221">ServerGarbageCollection</span><span class="sxs-lookup"><span data-stu-id="feec5-221">ServerGarbageCollection</span></span>](#servergarbagecollection)
- [<span data-ttu-id="feec5-222">ThreadPoolMaxThreads</span><span class="sxs-lookup"><span data-stu-id="feec5-222">ThreadPoolMaxThreads</span></span>](#threadpoolmaxthreads)
- [<span data-ttu-id="feec5-223">ThreadPoolMinThreads</span><span class="sxs-lookup"><span data-stu-id="feec5-223">ThreadPoolMinThreads</span></span>](#threadpoolminthreads)
- [<span data-ttu-id="feec5-224">TieredCompilation</span><span class="sxs-lookup"><span data-stu-id="feec5-224">TieredCompilation</span></span>](#tieredcompilation)
- [<span data-ttu-id="feec5-225">TieredCompilationQuickJit</span><span class="sxs-lookup"><span data-stu-id="feec5-225">TieredCompilationQuickJit</span></span>](#tieredcompilationquickjit)
- [<span data-ttu-id="feec5-226">TieredCompilationQuickJitForLoops</span><span class="sxs-lookup"><span data-stu-id="feec5-226">TieredCompilationQuickJitForLoops</span></span>](#tieredcompilationquickjitforloops)

### <a name="concurrentgarbagecollection"></a><span data-ttu-id="feec5-227">ConcurrentGarbageCollection</span><span class="sxs-lookup"><span data-stu-id="feec5-227">ConcurrentGarbageCollection</span></span>

<span data-ttu-id="feec5-228">`ConcurrentGarbageCollection`Właściwość określa, czy jest włączone [wyrzucanie elementów bezużytecznych w tle](../../standard/garbage-collection/background-gc.md) .</span><span class="sxs-lookup"><span data-stu-id="feec5-228">The `ConcurrentGarbageCollection` property configures whether [background (concurrent) garbage collection](../../standard/garbage-collection/background-gc.md) is enabled.</span></span> <span data-ttu-id="feec5-229">Ustaw wartość na `false` , aby wyłączyć wyrzucanie elementów bezużytecznych w tle.</span><span class="sxs-lookup"><span data-stu-id="feec5-229">Set the value to `false` to disable background garbage collection.</span></span> <span data-ttu-id="feec5-230">Aby uzyskać więcej informacji, zobacz w [tle GC](../run-time-config/garbage-collector.md#background-gc).</span><span class="sxs-lookup"><span data-stu-id="feec5-230">For more information, see [Background GC](../run-time-config/garbage-collector.md#background-gc).</span></span>

```xml
<PropertyGroup>
  <ConcurrentGarbageCollection>false</ConcurrentGarbageCollection>
</PropertyGroup>
```

### <a name="invariantglobalization"></a><span data-ttu-id="feec5-231">InvariantGlobalization</span><span class="sxs-lookup"><span data-stu-id="feec5-231">InvariantGlobalization</span></span>

<span data-ttu-id="feec5-232">`InvariantGlobalization`Właściwość określa, czy aplikacja jest uruchamiana w trybie *globalizacji-niezmiennym* , co oznacza, że nie ma dostępu do danych specyficznych dla kultury.</span><span class="sxs-lookup"><span data-stu-id="feec5-232">The `InvariantGlobalization` property configures whether the app runs in *globalization-invariant* mode, which means it doesn't have access to culture-specific data.</span></span> <span data-ttu-id="feec5-233">Ustaw wartość tak, aby była `true` uruchamiana w trybie niezmiennym globalizacji.</span><span class="sxs-lookup"><span data-stu-id="feec5-233">Set the value to `true` to run in globalization-invariant mode.</span></span> <span data-ttu-id="feec5-234">Aby uzyskać więcej informacji, zobacz [tryb niezmienny](../run-time-config/globalization.md#invariant-mode).</span><span class="sxs-lookup"><span data-stu-id="feec5-234">For more information, see [Invariant mode](../run-time-config/globalization.md#invariant-mode).</span></span>

```xml
<PropertyGroup>
  <InvariantGlobalization>true</InvariantGlobalization>
</PropertyGroup>
```

### <a name="retainvmgarbagecollection"></a><span data-ttu-id="feec5-235">RetainVMGarbageCollection</span><span class="sxs-lookup"><span data-stu-id="feec5-235">RetainVMGarbageCollection</span></span>

<span data-ttu-id="feec5-236">`RetainVMGarbageCollection`Właściwość konfiguruje moduł wyrzucania elementów bezużytecznych w celu umieszczenia usuniętych segmentów pamięci na liście gotowości do użycia w przyszłości lub zwolnienia.</span><span class="sxs-lookup"><span data-stu-id="feec5-236">The `RetainVMGarbageCollection` property configures the garbage collector to put deleted memory segments on a standby list for future use or release them.</span></span> <span data-ttu-id="feec5-237">Ustawienie wartości `true` informującej Moduł wyrzucania elementów bezużytecznych w celu umieszczenia segmentów na liście gotowości.</span><span class="sxs-lookup"><span data-stu-id="feec5-237">Setting the value to `true` tells the garbage collector to put the segments on a standby list.</span></span> <span data-ttu-id="feec5-238">Aby uzyskać więcej informacji, zobacz temat [zachowywanie maszyny wirtualnej](../run-time-config/garbage-collector.md#retain-vm).</span><span class="sxs-lookup"><span data-stu-id="feec5-238">For more information, see [Retain VM](../run-time-config/garbage-collector.md#retain-vm).</span></span>

```xml
<PropertyGroup>
  <RetainVMGarbageCollection>true</RetainVMGarbageCollection>
</PropertyGroup>
```

### <a name="servergarbagecollection"></a><span data-ttu-id="feec5-239">ServerGarbageCollection</span><span class="sxs-lookup"><span data-stu-id="feec5-239">ServerGarbageCollection</span></span>

<span data-ttu-id="feec5-240">`ServerGarbageCollection`Właściwość określa, czy aplikacja używa [wyrzucania elementów bezużytecznych stacji roboczej lub odzyskiwania pamięci serwera](../../standard/garbage-collection/workstation-server-gc.md).</span><span class="sxs-lookup"><span data-stu-id="feec5-240">The `ServerGarbageCollection` property configures whether the application uses [workstation garbage collection or server garbage collection](../../standard/garbage-collection/workstation-server-gc.md).</span></span> <span data-ttu-id="feec5-241">Ustaw wartość na, aby `true` użyć wyrzucania elementów bezużytecznych serwera.</span><span class="sxs-lookup"><span data-stu-id="feec5-241">Set the value to `true` to use server garbage collection.</span></span> <span data-ttu-id="feec5-242">Aby uzyskać więcej informacji, zobacz [stacja robocza a serwer](../run-time-config/garbage-collector.md#workstation-vs-server).</span><span class="sxs-lookup"><span data-stu-id="feec5-242">For more information, see [Workstation vs. server](../run-time-config/garbage-collector.md#workstation-vs-server).</span></span>

```xml
<PropertyGroup>
  <ServerGarbageCollection>true</ServerGarbageCollection>
</PropertyGroup>
```

### <a name="threadpoolmaxthreads"></a><span data-ttu-id="feec5-243">ThreadPoolMaxThreads</span><span class="sxs-lookup"><span data-stu-id="feec5-243">ThreadPoolMaxThreads</span></span>

<span data-ttu-id="feec5-244">`ThreadPoolMaxThreads`Właściwość określa maksymalną liczbę wątków dla puli wątków roboczych.</span><span class="sxs-lookup"><span data-stu-id="feec5-244">The `ThreadPoolMaxThreads` property configures the maximum number of threads for the worker thread pool.</span></span> <span data-ttu-id="feec5-245">Aby uzyskać więcej informacji, zobacz [maksymalne wątki](../run-time-config/threading.md#maximum-threads).</span><span class="sxs-lookup"><span data-stu-id="feec5-245">For more information, see [Maximum threads](../run-time-config/threading.md#maximum-threads).</span></span>

```xml
<PropertyGroup>
  <ThreadPoolMaxThreads>20</ThreadPoolMaxThreads>
</PropertyGroup>
```

### <a name="threadpoolminthreads"></a><span data-ttu-id="feec5-246">ThreadPoolMinThreads</span><span class="sxs-lookup"><span data-stu-id="feec5-246">ThreadPoolMinThreads</span></span>

<span data-ttu-id="feec5-247">`ThreadPoolMinThreads`Właściwość konfiguruje minimalną liczbę wątków dla puli wątków roboczych.</span><span class="sxs-lookup"><span data-stu-id="feec5-247">The `ThreadPoolMinThreads` property configures the minimum number of threads for the worker thread pool.</span></span> <span data-ttu-id="feec5-248">Aby uzyskać więcej informacji, zobacz [minimalna liczba wątków](../run-time-config/threading.md#minimum-threads).</span><span class="sxs-lookup"><span data-stu-id="feec5-248">For more information, see [Minimum threads](../run-time-config/threading.md#minimum-threads).</span></span>

```xml
<PropertyGroup>
  <ThreadPoolMinThreads>4</ThreadPoolMinThreads>
</PropertyGroup>
```

### <a name="tieredcompilation"></a><span data-ttu-id="feec5-249">TieredCompilation</span><span class="sxs-lookup"><span data-stu-id="feec5-249">TieredCompilation</span></span>

<span data-ttu-id="feec5-250">`TieredCompilation`Właściwość określa, czy kompilator just in Time (JIT) używa [kompilacji warstwowej](../whats-new/dotnet-core-3-0.md#tiered-compilation).</span><span class="sxs-lookup"><span data-stu-id="feec5-250">The `TieredCompilation` property configures whether the just-in-time (JIT) compiler uses [tiered compilation](../whats-new/dotnet-core-3-0.md#tiered-compilation).</span></span> <span data-ttu-id="feec5-251">Ustaw wartość na, aby `false` wyłączyć kompilację warstwową.</span><span class="sxs-lookup"><span data-stu-id="feec5-251">Set the value to `false` to disable tiered compilation.</span></span> <span data-ttu-id="feec5-252">Aby uzyskać więcej informacji, zobacz temat [kompilacja warstwowa](../run-time-config/compilation.md#tiered-compilation).</span><span class="sxs-lookup"><span data-stu-id="feec5-252">For more information, see [Tiered compilation](../run-time-config/compilation.md#tiered-compilation).</span></span>

```xml
<PropertyGroup>
  <TieredCompilation>false</TieredCompilation>
</PropertyGroup>
```

### <a name="tieredcompilationquickjit"></a><span data-ttu-id="feec5-253">TieredCompilationQuickJit</span><span class="sxs-lookup"><span data-stu-id="feec5-253">TieredCompilationQuickJit</span></span>

<span data-ttu-id="feec5-254">`TieredCompilationQuickJit`Właściwość określa, czy KOMPILATOR JIT używa szybkiej JIT.</span><span class="sxs-lookup"><span data-stu-id="feec5-254">The `TieredCompilationQuickJit` property configures whether the JIT compiler uses quick JIT.</span></span> <span data-ttu-id="feec5-255">Ustaw wartość na `false` , aby wyłączyć szybkie JIT.</span><span class="sxs-lookup"><span data-stu-id="feec5-255">Set the value to `false` to disable quick JIT.</span></span> <span data-ttu-id="feec5-256">Aby uzyskać więcej informacji, zobacz [szybkie JIT](../run-time-config/compilation.md#quick-jit).</span><span class="sxs-lookup"><span data-stu-id="feec5-256">For more information, see [Quick JIT](../run-time-config/compilation.md#quick-jit).</span></span>

```xml
<PropertyGroup>
  <TieredCompilationQuickJit>false</TieredCompilationQuickJit>
</PropertyGroup>
```

### <a name="tieredcompilationquickjitforloops"></a><span data-ttu-id="feec5-257">TieredCompilationQuickJitForLoops</span><span class="sxs-lookup"><span data-stu-id="feec5-257">TieredCompilationQuickJitForLoops</span></span>

<span data-ttu-id="feec5-258">`TieredCompilationQuickJitForLoops`Właściwość określa, czy KOMPILATOR JIT używa szybkiej JIT metod, które zawierają pętle.</span><span class="sxs-lookup"><span data-stu-id="feec5-258">The `TieredCompilationQuickJitForLoops` property configures whether the JIT compiler uses quick JIT on methods that contain loops.</span></span> <span data-ttu-id="feec5-259">Ustaw wartość na, aby `true` włączyć funkcję szybkiego JIT dla metod, które zawierają pętle.</span><span class="sxs-lookup"><span data-stu-id="feec5-259">Set the value to `true` to enable quick JIT on methods that contain loops.</span></span> <span data-ttu-id="feec5-260">Aby uzyskać więcej informacji, zobacz [szybkie JIT dla pętli](../run-time-config/compilation.md#quick-jit-for-loops).</span><span class="sxs-lookup"><span data-stu-id="feec5-260">For more information, see [Quick JIT for loops](../run-time-config/compilation.md#quick-jit-for-loops).</span></span>

```xml
<PropertyGroup>
  <TieredCompilationQuickJitForLoops>true</TieredCompilationQuickJitForLoops>
</PropertyGroup>
```

## <a name="reference-properties-and-items"></a><span data-ttu-id="feec5-261">Właściwości odwołania i elementy</span><span class="sxs-lookup"><span data-stu-id="feec5-261">Reference properties and items</span></span>

- [<span data-ttu-id="feec5-262">AssetTargetFallback</span><span class="sxs-lookup"><span data-stu-id="feec5-262">AssetTargetFallback</span></span>](#assettargetfallback)
- [<span data-ttu-id="feec5-263">PackageReference</span><span class="sxs-lookup"><span data-stu-id="feec5-263">PackageReference</span></span>](#packagereference)
- [<span data-ttu-id="feec5-264">Elementu ProjectReference</span><span class="sxs-lookup"><span data-stu-id="feec5-264">ProjectReference</span></span>](#projectreference)
- [<span data-ttu-id="feec5-265">Odwołanie</span><span class="sxs-lookup"><span data-stu-id="feec5-265">Reference</span></span>](#reference)
- [<span data-ttu-id="feec5-266">Właściwości związane z przywracaniem</span><span class="sxs-lookup"><span data-stu-id="feec5-266">Restore-related properties</span></span>](#restore-related-properties)

### <a name="assettargetfallback"></a><span data-ttu-id="feec5-267">AssetTargetFallback</span><span class="sxs-lookup"><span data-stu-id="feec5-267">AssetTargetFallback</span></span>

<span data-ttu-id="feec5-268">`AssetTargetFallback`Właściwość pozwala określić dodatkowe zgodne wersje architektury dla odwołań do projektu i pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="feec5-268">The `AssetTargetFallback` property lets you specify additional compatible framework versions for project references and NuGet packages.</span></span> <span data-ttu-id="feec5-269">Na przykład, jeśli określisz zależność pakietu przy użyciu programu `PackageReference` , ale ten pakiet nie zawiera zasobów, które są zgodne z projektem `TargetFramework` , `AssetTargetFallback` Właściwość jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="feec5-269">For example, if you specify a package dependency using `PackageReference` but that package doesn't contain assets that are compatible with your projects's `TargetFramework`, the `AssetTargetFallback` property comes into play.</span></span> <span data-ttu-id="feec5-270">Zgodność przywoływanego pakietu jest ponownie sprawdzana przy użyciu każdej platformy docelowej określonej w `AssetTargetFallback` .</span><span class="sxs-lookup"><span data-stu-id="feec5-270">The compatibility of the referenced package is rechecked using each target framework that's specified in `AssetTargetFallback`.</span></span>

<span data-ttu-id="feec5-271">Można ustawić `AssetTargetFallback` Właściwość na co najmniej jedną [docelową wersję platformy](../../standard/frameworks.md#supported-target-frameworks).</span><span class="sxs-lookup"><span data-stu-id="feec5-271">You can set the `AssetTargetFallback` property to one or more [target framework versions](../../standard/frameworks.md#supported-target-frameworks).</span></span>

```xml
<PropertyGroup>
  <AssetTargetFallback>net461</AssetTargetFallback>
</PropertyGroup>
```

### <a name="packagereference"></a><span data-ttu-id="feec5-272">PackageReference</span><span class="sxs-lookup"><span data-stu-id="feec5-272">PackageReference</span></span>

<span data-ttu-id="feec5-273">`PackageReference`Element definiuje odwołanie do pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="feec5-273">The `PackageReference` item defines a reference to a NuGet package.</span></span>

<span data-ttu-id="feec5-274">Ten `Include` atrybut określa identyfikator pakietu.</span><span class="sxs-lookup"><span data-stu-id="feec5-274">The `Include` attribute specifies the package ID.</span></span> <span data-ttu-id="feec5-275">Ten `Version` atrybut określa wersję lub zakres wersji.</span><span class="sxs-lookup"><span data-stu-id="feec5-275">The `Version` attribute specifies the version or version range.</span></span> <span data-ttu-id="feec5-276">Aby uzyskać informacje na temat określania minimalnej wersji, maksymalnej wersji, zakresu lub dokładnego dopasowania, zobacz [zakres wersji](/nuget/concepts/package-versioning#version-ranges).</span><span class="sxs-lookup"><span data-stu-id="feec5-276">For information about how to specify a minimum version, maximum version, range, or exact match, see [Version ranges](/nuget/concepts/package-versioning#version-ranges).</span></span> <span data-ttu-id="feec5-277">Można również dodać następujące metadane do odwołania do projektu: `IncludeAssets` , `ExcludeAssets` , i `PrivateAssets` .</span><span class="sxs-lookup"><span data-stu-id="feec5-277">You can also add the following metadata to a project reference: `IncludeAssets`, `ExcludeAssets`, and `PrivateAssets`.</span></span>

<span data-ttu-id="feec5-278">Fragment pliku projektu w poniższym przykładzie odwołuje się do pakietu [System. Runtime](https://www.nuget.org/packages/System.Runtime/) .</span><span class="sxs-lookup"><span data-stu-id="feec5-278">The project file snippet in the following example references the [System.Runtime](https://www.nuget.org/packages/System.Runtime/) package.</span></span>

```xml
<ItemGroup>
  <PackageReference Include="System.Runtime" Version="4.3.0" />
</ItemGroup>
```

<span data-ttu-id="feec5-279">Aby uzyskać więcej informacji, zobacz [odwołania do pakietów w plikach projektu](/nuget/consume-packages/package-references-in-project-files).</span><span class="sxs-lookup"><span data-stu-id="feec5-279">For more information, see [Package references in project files](/nuget/consume-packages/package-references-in-project-files).</span></span>

### <a name="projectreference"></a><span data-ttu-id="feec5-280">Elementu ProjectReference</span><span class="sxs-lookup"><span data-stu-id="feec5-280">ProjectReference</span></span>

<span data-ttu-id="feec5-281">`ProjectReference`Element definiuje odwołanie do innego projektu.</span><span class="sxs-lookup"><span data-stu-id="feec5-281">The `ProjectReference` item defines a reference to another project.</span></span> <span data-ttu-id="feec5-282">Przywoływany projekt jest dodawany jako zależność pakietu NuGet, czyli jest traktowany tak samo jak `PackageReference` .</span><span class="sxs-lookup"><span data-stu-id="feec5-282">The referenced project is added as a NuGet package dependency, that is, it's treated the same as a `PackageReference`.</span></span>

<span data-ttu-id="feec5-283">Ten `Include` atrybut określa ścieżkę do projektu.</span><span class="sxs-lookup"><span data-stu-id="feec5-283">The `Include` attribute specifies the path to the project.</span></span> <span data-ttu-id="feec5-284">Można również dodać następujące metadane do odwołania do projektu: `IncludeAssets` , `ExcludeAssets` , i `PrivateAssets` .</span><span class="sxs-lookup"><span data-stu-id="feec5-284">You can also add the following metadata to a project reference: `IncludeAssets`, `ExcludeAssets`, and `PrivateAssets`.</span></span>

<span data-ttu-id="feec5-285">Fragment pliku projektu w poniższym przykładzie odwołuje się do projektu o nazwie `Project2` .</span><span class="sxs-lookup"><span data-stu-id="feec5-285">The project file snippet in the following example references a project named `Project2`.</span></span>

```xml
<ItemGroup>
  <ProjectReference Include="..\Project2.csproj" />
</ItemGroup>
```

### <a name="reference"></a><span data-ttu-id="feec5-286">Odwołanie</span><span class="sxs-lookup"><span data-stu-id="feec5-286">Reference</span></span>

<span data-ttu-id="feec5-287">`Reference`Element definiuje odwołanie do pliku zestawu.</span><span class="sxs-lookup"><span data-stu-id="feec5-287">The `Reference` item defines a reference to an assembly file.</span></span>

<span data-ttu-id="feec5-288">`Include`Atrybut określa nazwę pliku, a `HintPath` metadane określa ścieżkę do zestawu.</span><span class="sxs-lookup"><span data-stu-id="feec5-288">The `Include` attribute specifies the name of the file, and the `HintPath` metadata specifies the path to the assembly.</span></span>

```xml
<ItemGroup>
  <Reference Include="MyAssembly">
    <HintPath>..\..\Assemblies\MyAssembly.dll</HintPath>
  </Reference>
</ItemGroup>
```

### <a name="restore-related-properties"></a><span data-ttu-id="feec5-289">Właściwości związane z przywracaniem</span><span class="sxs-lookup"><span data-stu-id="feec5-289">Restore-related properties</span></span>

<span data-ttu-id="feec5-290">Przywracanie przywoływanego pakietu instaluje wszystkie jego bezpośrednie zależności i wszystkie zależności tych zależności.</span><span class="sxs-lookup"><span data-stu-id="feec5-290">Restoring a referenced package installs all of its direct dependencies and all the dependencies of those dependencies.</span></span> <span data-ttu-id="feec5-291">Przywracanie pakietu można dostosować, określając właściwości, takie jak `RestorePackagesPath` i `RestoreIgnoreFailedSources` .</span><span class="sxs-lookup"><span data-stu-id="feec5-291">You can customize package restoration by specifying properties such as `RestorePackagesPath` and `RestoreIgnoreFailedSources`.</span></span> <span data-ttu-id="feec5-292">Aby uzyskać więcej informacji na temat tych i innych właściwości, zobacz [Restore Target](/nuget/reference/msbuild-targets#restore-target).</span><span class="sxs-lookup"><span data-stu-id="feec5-292">For more information about these and other properties, see [restore target](/nuget/reference/msbuild-targets#restore-target).</span></span>

```xml
<PropertyGroup>
  <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

## <a name="hosting-properties-and-items"></a><span data-ttu-id="feec5-293">Hostowanie właściwości i elementów</span><span class="sxs-lookup"><span data-stu-id="feec5-293">Hosting properties and items</span></span>

- [<span data-ttu-id="feec5-294">EnableComHosting</span><span class="sxs-lookup"><span data-stu-id="feec5-294">EnableComHosting</span></span>](#enablecomhosting)
- [<span data-ttu-id="feec5-295">EnableDynamicLoading</span><span class="sxs-lookup"><span data-stu-id="feec5-295">EnableDynamicLoading</span></span>](#enabledynamicloading)

### <a name="enablecomhosting"></a><span data-ttu-id="feec5-296">EnableComHosting</span><span class="sxs-lookup"><span data-stu-id="feec5-296">EnableComHosting</span></span>

<span data-ttu-id="feec5-297">`EnableComHosting`Właściwość wskazuje, że zestaw udostępnia serwer com.</span><span class="sxs-lookup"><span data-stu-id="feec5-297">The `EnableComHosting` property indicates that an assembly provides a COM server.</span></span> <span data-ttu-id="feec5-298">Ustawienie to `EnableComHosting` `true` oznacza również, że [EnableDynamicLoading](#enabledynamicloading) ma wartość `true` .</span><span class="sxs-lookup"><span data-stu-id="feec5-298">Setting the `EnableComHosting` to `true` also implies that [EnableDynamicLoading](#enabledynamicloading) is `true`.</span></span>

```xml
<PropertyGroup>
  <EnableComHosting>True</EnableComHosting>
</PropertyGroup>
```

<span data-ttu-id="feec5-299">Aby uzyskać więcej informacji, zobacz [Udostępnianie składników .NET do modelu COM](../native-interop/expose-components-to-com.md).</span><span class="sxs-lookup"><span data-stu-id="feec5-299">For more information, see [Expose .NET components to COM](../native-interop/expose-components-to-com.md).</span></span>

### <a name="enabledynamicloading"></a><span data-ttu-id="feec5-300">EnableDynamicLoading</span><span class="sxs-lookup"><span data-stu-id="feec5-300">EnableDynamicLoading</span></span>

<span data-ttu-id="feec5-301">`EnableDynamicLoading`Właściwość wskazuje, że zestaw jest składnikiem ładowanym dynamicznie.</span><span class="sxs-lookup"><span data-stu-id="feec5-301">The `EnableDynamicLoading` property indicates that an assembly is a dynamically loaded component.</span></span> <span data-ttu-id="feec5-302">Składnik może być [biblioteką com](/windows/win32/com/the-component-object-model) lub biblioteką niebędącą modelem COM, która może być [używana z macierzystego hosta](../tutorials/netcore-hosting.md).</span><span class="sxs-lookup"><span data-stu-id="feec5-302">The component could be a [COM library](/windows/win32/com/the-component-object-model) or a non-COM library that can be [used from a native host](../tutorials/netcore-hosting.md).</span></span> <span data-ttu-id="feec5-303">Ustawienie tej właściwości na `true` ma następujące skutki:</span><span class="sxs-lookup"><span data-stu-id="feec5-303">Setting this property to `true` has the following effects:</span></span>

- <span data-ttu-id="feec5-304">Generowany jest *.runtimeconfig.js* pliku.</span><span class="sxs-lookup"><span data-stu-id="feec5-304">A *.runtimeconfig.json* file is generated.</span></span>
- <span data-ttu-id="feec5-305">[Przewinięcie do przodu](../whats-new/dotnet-core-3-0.md#major-version-runtime-roll-forward) jest ustawione na `LatestMinor` .</span><span class="sxs-lookup"><span data-stu-id="feec5-305">[Roll forward](../whats-new/dotnet-core-3-0.md#major-version-runtime-roll-forward) is set to `LatestMinor`.</span></span>
- <span data-ttu-id="feec5-306">Odwołania NuGet są kopiowane lokalnie.</span><span class="sxs-lookup"><span data-stu-id="feec5-306">NuGet references are copied locally.</span></span>

```xml
<PropertyGroup>
  <EnableDynamicLoading>true</EnableDynamicLoading>
</PropertyGroup>
```

## <a name="see-also"></a><span data-ttu-id="feec5-307">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="feec5-307">See also</span></span>

- [<span data-ttu-id="feec5-308">Odwołanie do schematu programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="feec5-308">MSBuild schema reference</span></span>](/visualstudio/msbuild/msbuild-project-file-schema-reference)
- [<span data-ttu-id="feec5-309">Typowe właściwości programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="feec5-309">Common MSBuild properties</span></span>](/visualstudio/msbuild/common-msbuild-project-properties)
- [<span data-ttu-id="feec5-310">Właściwości programu MSBuild dla pakietu NuGet</span><span class="sxs-lookup"><span data-stu-id="feec5-310">MSBuild properties for NuGet pack</span></span>](/nuget/reference/msbuild-targets#pack-target)
- [<span data-ttu-id="feec5-311">Właściwości programu MSBuild do przywracania NuGet</span><span class="sxs-lookup"><span data-stu-id="feec5-311">MSBuild properties for NuGet restore</span></span>](/nuget/reference/msbuild-targets#restore-properties)
- [<span data-ttu-id="feec5-312">Dostosuj kompilację</span><span class="sxs-lookup"><span data-stu-id="feec5-312">Customize a build</span></span>](/visualstudio/msbuild/customize-your-build)
