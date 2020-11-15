---
title: polecenie kompilacji dotnet
description: Polecenie kompilacji dotnet kompiluje projekt i wszystkie jego zależności.
ms.date: 02/14/2020
ms.openlocfilehash: ea0291129aeaed3bebef5c454ff003131bd3562b
ms.sourcegitcommit: b201d177e01480a139622f3bf8facd367657a472
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/15/2020
ms.locfileid: "94634484"
---
# <a name="dotnet-build"></a><span data-ttu-id="8ff7a-103">dotnet build</span><span class="sxs-lookup"><span data-stu-id="8ff7a-103">dotnet build</span></span>

<span data-ttu-id="8ff7a-104">**Ten artykuł ma zastosowanie do:** ✔️ .NET Core 2. x SDK i nowszych wersji</span><span class="sxs-lookup"><span data-stu-id="8ff7a-104">**This article applies to:** ✔️ .NET Core 2.x SDK and later versions</span></span>

## <a name="name"></a><span data-ttu-id="8ff7a-105">Nazwa</span><span class="sxs-lookup"><span data-stu-id="8ff7a-105">Name</span></span>

<span data-ttu-id="8ff7a-106">`dotnet build` -Kompiluje projekt i wszystkie jego zależności.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-106">`dotnet build` - Builds a project and all of its dependencies.</span></span>

## <a name="synopsis"></a><span data-ttu-id="8ff7a-107">Streszczenie</span><span class="sxs-lookup"><span data-stu-id="8ff7a-107">Synopsis</span></span>

```dotnetcli
dotnet build [<PROJECT>|<SOLUTION>] [-c|--configuration <CONFIGURATION>]
    [-f|--framework <FRAMEWORK>] [--force] [--interactive] [--no-dependencies]
    [--no-incremental] [--no-restore] [--nologo] [-o|--output <OUTPUT_DIRECTORY>]
    [-r|--runtime <RUNTIME_IDENTIFIER>] [--source <SOURCE>]
    [-v|--verbosity <LEVEL>] [--version-suffix <VERSION_SUFFIX>]

dotnet build -h|--help
```

## <a name="description"></a><span data-ttu-id="8ff7a-108">Opis</span><span class="sxs-lookup"><span data-stu-id="8ff7a-108">Description</span></span>

<span data-ttu-id="8ff7a-109">`dotnet build`Polecenie kompiluje projekt i jego zależności do zestawu plików binarnych.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-109">The `dotnet build` command builds the project and its dependencies into a set of binaries.</span></span> <span data-ttu-id="8ff7a-110">Pliki binarne zawierają kod projektu w plikach języka pośredniego (IL) z rozszerzeniem *. dll* .</span><span class="sxs-lookup"><span data-stu-id="8ff7a-110">The binaries include the project's code in Intermediate Language (IL) files with a *.dll* extension.</span></span>  <span data-ttu-id="8ff7a-111">W zależności od typu projektu i ustawień można uwzględnić inne pliki, takie jak:</span><span class="sxs-lookup"><span data-stu-id="8ff7a-111">Depending on the project type and settings, other files may be included, such as:</span></span>

- <span data-ttu-id="8ff7a-112">Plik wykonywalny, który może służyć do uruchamiania aplikacji, jeśli typem projektu jest plik wykonywalny przeznaczony dla platformy .NET Core 3,0 lub nowszego.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-112">An executable that can be used to run the application, if the project type is an executable targeting .NET Core 3.0 or later.</span></span>
- <span data-ttu-id="8ff7a-113">Pliki symboli używane do debugowania z rozszerzeniem *. pdb* .</span><span class="sxs-lookup"><span data-stu-id="8ff7a-113">Symbol files used for debugging with a *.pdb* extension.</span></span>
- <span data-ttu-id="8ff7a-114">*.deps.jsw* pliku, który zawiera listę zależności aplikacji lub biblioteki.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-114">A *.deps.json* file, which lists the dependencies of the application or library.</span></span>
- <span data-ttu-id="8ff7a-115">*.runtimeconfig.jsw* pliku, który określa udostępnione środowisko uruchomieniowe i jego wersję dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-115">A *.runtimeconfig.json* file, which specifies the shared runtime and its version for an application.</span></span>
- <span data-ttu-id="8ff7a-116">Inne biblioteki, od których zależy projekt (za pośrednictwem odwołań projektu lub pakietów NuGet).</span><span class="sxs-lookup"><span data-stu-id="8ff7a-116">Other libraries that the project depends on (via project references or NuGet package references).</span></span>

<span data-ttu-id="8ff7a-117">W przypadku projektów wykonywalnych przeznaczonych dla wersji wcześniejszej niż .NET Core 3,0, zależności biblioteki z NuGet nie są zwykle kopiowane do folderu wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-117">For executable projects targeting versions earlier than .NET Core 3.0, library dependencies from NuGet are typically NOT copied to the output folder.</span></span>  <span data-ttu-id="8ff7a-118">Są one rozpoznawane z folderu pakietów globalnych NuGet w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-118">They're resolved from the NuGet global packages folder at run time.</span></span> <span data-ttu-id="8ff7a-119">Z tego względu produkt `dotnet build` nie jest gotowy do przeniesienia na inną maszynę do uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-119">With that in mind, the product of `dotnet build` isn't ready to be transferred to another machine to run.</span></span> <span data-ttu-id="8ff7a-120">Aby utworzyć wersję aplikacji, którą można wdrożyć, należy ją opublikować (na przykład przy użyciu polecenia [dotnet Publish](dotnet-publish.md) ).</span><span class="sxs-lookup"><span data-stu-id="8ff7a-120">To create a version of the application that can be deployed, you need to publish it (for example, with the [dotnet publish](dotnet-publish.md) command).</span></span> <span data-ttu-id="8ff7a-121">Aby uzyskać więcej informacji, zobacz [wdrażanie aplikacji .NET](../deploying/index.md).</span><span class="sxs-lookup"><span data-stu-id="8ff7a-121">For more information, see [.NET Application Deployment](../deploying/index.md).</span></span>

<span data-ttu-id="8ff7a-122">W przypadku projektów wykonywalnych przeznaczonych dla platformy .NET Core 3,0 i nowszych zależności biblioteki są kopiowane do folderu wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-122">For executable projects targeting .NET Core 3.0 and later, library dependencies are copied to the output folder.</span></span> <span data-ttu-id="8ff7a-123">Oznacza to, że jeśli nie ma żadnej innej logiki specyficznej dla publikacji (takiej jak projekty sieci Web), dane wyjściowe kompilacji powinny być możliwe do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-123">This means that if there isn't any other publish-specific logic (such as Web projects have), the build output should be deployable.</span></span>

### <a name="implicit-restore"></a><span data-ttu-id="8ff7a-124">Przywracanie niejawne</span><span class="sxs-lookup"><span data-stu-id="8ff7a-124">Implicit restore</span></span>

<span data-ttu-id="8ff7a-125">Kompilowanie wymaga *project.assets.jsw* pliku, który zawiera listę zależności aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-125">Building requires the *project.assets.json* file, which lists the dependencies of your application.</span></span> <span data-ttu-id="8ff7a-126">Plik jest tworzony, gdy [`dotnet restore`](dotnet-restore.md) jest wykonywany.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-126">The file is created when [`dotnet restore`](dotnet-restore.md) is executed.</span></span> <span data-ttu-id="8ff7a-127">Bez pliku zasobów na miejscu narzędzia nie mogą rozpoznać zestawów referencyjnych, które powodują błędy.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-127">Without the assets file in place, the tooling can't resolve reference assemblies, which results in errors.</span></span>

[!INCLUDE[dotnet restore note + options](~/includes/dotnet-restore-note-options.md)]

### <a name="executable-or-library-output"></a><span data-ttu-id="8ff7a-128">Plik wykonywalny lub biblioteka wyjściowa</span><span class="sxs-lookup"><span data-stu-id="8ff7a-128">Executable or library output</span></span>

<span data-ttu-id="8ff7a-129">Czy projekt jest plikiem wykonywalnym, czy nie jest określony przez `<OutputType>` Właściwość w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-129">Whether the project is executable or not is determined by the `<OutputType>` property in the project file.</span></span> <span data-ttu-id="8ff7a-130">W poniższym przykładzie przedstawiono projekt tworzący kod wykonywalny:</span><span class="sxs-lookup"><span data-stu-id="8ff7a-130">The following example shows a project that produces executable code:</span></span>

```xml
<PropertyGroup>
  <OutputType>Exe</OutputType>
</PropertyGroup>
```

<span data-ttu-id="8ff7a-131">Aby utworzyć bibliotekę, Pomiń `<OutputType>` Właściwość lub zmień jej wartość na `Library` .</span><span class="sxs-lookup"><span data-stu-id="8ff7a-131">To produce a library, omit the `<OutputType>` property or change its value to `Library`.</span></span> <span data-ttu-id="8ff7a-132">Biblioteka DLL IL dla biblioteki nie zawiera punktów wejścia i nie można jej wykonać.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-132">The IL DLL for a library doesn't contain entry points and can't be executed.</span></span>

### <a name="msbuild"></a><span data-ttu-id="8ff7a-133">MSBuild</span><span class="sxs-lookup"><span data-stu-id="8ff7a-133">MSBuild</span></span>

<span data-ttu-id="8ff7a-134">`dotnet build` używa programu MSBuild do skompilowania projektu, aby obsługiwał kompilacje równoległe i przyrostowe.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-134">`dotnet build` uses MSBuild to build the project, so it supports both parallel and incremental builds.</span></span> <span data-ttu-id="8ff7a-135">Aby uzyskać więcej informacji, zobacz [Kompilacje przyrostowe](/visualstudio/msbuild/incremental-builds).</span><span class="sxs-lookup"><span data-stu-id="8ff7a-135">For more information, see [Incremental Builds](/visualstudio/msbuild/incremental-builds).</span></span>

<span data-ttu-id="8ff7a-136">Oprócz opcji, `dotnet build` polecenie akceptuje Opcje programu MSBuild, takie jak `-p` właściwości ustawienia lub `-l` definiowania rejestratora.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-136">In addition to its options, the `dotnet build` command accepts MSBuild options, such as `-p` for setting properties or `-l` to define a logger.</span></span> <span data-ttu-id="8ff7a-137">Aby uzyskać więcej informacji na temat tych opcji, zobacz informacje o programie [MSBuild Command-Line](/visualstudio/msbuild/msbuild-command-line-reference).</span><span class="sxs-lookup"><span data-stu-id="8ff7a-137">For more information about these options, see the [MSBuild Command-Line Reference](/visualstudio/msbuild/msbuild-command-line-reference).</span></span> <span data-ttu-id="8ff7a-138">Lub można również użyć polecenia programu [dotnet MSBuild](dotnet-msbuild.md) .</span><span class="sxs-lookup"><span data-stu-id="8ff7a-138">Or you can also use the [dotnet msbuild](dotnet-msbuild.md) command.</span></span>

<span data-ttu-id="8ff7a-139">Uruchomienie `dotnet build` jest równoważne działaniu `dotnet msbuild -restore` , jednak domyślna szczegółowość danych wyjściowych jest inna.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-139">Running `dotnet build` is equivalent to running `dotnet msbuild -restore`; however, the default verbosity of the output is different.</span></span>

## <a name="arguments"></a><span data-ttu-id="8ff7a-140">Argumenty</span><span class="sxs-lookup"><span data-stu-id="8ff7a-140">Arguments</span></span>

`PROJECT | SOLUTION`

<span data-ttu-id="8ff7a-141">Plik projektu lub rozwiązania do skompilowania.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-141">The project or solution file to build.</span></span> <span data-ttu-id="8ff7a-142">Jeśli plik projektu lub rozwiązania nie zostanie określony, program MSBuild przeszukuje bieżący katalog roboczy dla pliku, który ma rozszerzenie pliku, które kończy się w *proj* lub *sln* i używa tego pliku.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-142">If a project or solution file isn't specified, MSBuild searches the current working directory for a file that has a file extension that ends in either *proj* or *sln* and uses that file.</span></span>

## <a name="options"></a><span data-ttu-id="8ff7a-143">Opcje</span><span class="sxs-lookup"><span data-stu-id="8ff7a-143">Options</span></span>

- **`-c|--configuration <CONFIGURATION>`**

  <span data-ttu-id="8ff7a-144">Definiuje konfigurację kompilacji.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-144">Defines the build configuration.</span></span> <span data-ttu-id="8ff7a-145">Wartością domyślną dla większości projektów jest `Debug` , ale można zastąpić ustawienia konfiguracji kompilacji w projekcie.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-145">The default for most projects is `Debug`, but you can override the build configuration settings in your project.</span></span>

- **`-f|--framework <FRAMEWORK>`**

  <span data-ttu-id="8ff7a-146">Kompiluje dla określonej [struktury](../../standard/frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="8ff7a-146">Compiles for a specific [framework](../../standard/frameworks.md).</span></span> <span data-ttu-id="8ff7a-147">Struktura musi być zdefiniowana w [pliku projektu](csproj.md).</span><span class="sxs-lookup"><span data-stu-id="8ff7a-147">The framework must be defined in the [project file](csproj.md).</span></span>

- **`--force`**

  <span data-ttu-id="8ff7a-148">Wymusza rozpoznanie wszystkich zależności, nawet jeśli ostatnie przywracanie zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-148">Forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="8ff7a-149">Określenie tej flagi jest takie samo jak usuwanie *project.assets.jsw* pliku.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-149">Specifying this flag is the same as deleting the *project.assets.json* file.</span></span>

- **`-h|--help`**

  <span data-ttu-id="8ff7a-150">Drukuje krótką pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-150">Prints out a short help for the command.</span></span>

- **`--interactive`**

  <span data-ttu-id="8ff7a-151">Zezwala na zatrzymanie polecenia i oczekiwanie na dane wejściowe użytkownika lub akcję.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-151">Allows the command to stop and wait for user input or action.</span></span> <span data-ttu-id="8ff7a-152">Na przykład, aby ukończyć uwierzytelnianie.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-152">For example, to complete authentication.</span></span> <span data-ttu-id="8ff7a-153">Dostępne od wersji .NET Core 3,0 SDK.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-153">Available since .NET Core 3.0 SDK.</span></span>

- **`--no-dependencies`**

  <span data-ttu-id="8ff7a-154">Ignoruje odwołania między projektami i projektami (P2P) i kompiluje tylko określony projekt główny.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-154">Ignores project-to-project (P2P) references and only builds the specified root project.</span></span>

- **`--no-incremental`**

  <span data-ttu-id="8ff7a-155">Oznacza kompilację jako niebezpieczną dla kompilacji przyrostowej.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-155">Marks the build as unsafe for incremental build.</span></span> <span data-ttu-id="8ff7a-156">Ta flaga powoduje wyłączenie kompilacji przyrostowej i wymuszenie czystej odbudowy wykresu zależności projektu.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-156">This flag turns off incremental compilation and forces a clean rebuild of the project's dependency graph.</span></span>

- **`--no-restore`**

  <span data-ttu-id="8ff7a-157">Nie wykonuje przywracania niejawnego podczas kompilacji.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-157">Doesn't execute an implicit restore during build.</span></span>

- **`--nologo`**

  <span data-ttu-id="8ff7a-158">Nie wyświetla transparentu początkowego ani komunikatu o prawach autorskich.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-158">Doesn't display the startup banner or the copyright message.</span></span> <span data-ttu-id="8ff7a-159">Dostępne od wersji .NET Core 3,0 SDK.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-159">Available since .NET Core 3.0 SDK.</span></span>

- **`-o|--output <OUTPUT_DIRECTORY>`**

  <span data-ttu-id="8ff7a-160">Katalog, w którym mają zostać umieszczone skompilowane pliki binarne.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-160">Directory in which to place the built binaries.</span></span> <span data-ttu-id="8ff7a-161">Jeśli nie zostanie określony, ścieżka domyślna to `./bin/<configuration>/<framework>/` .</span><span class="sxs-lookup"><span data-stu-id="8ff7a-161">If not specified, the default path is `./bin/<configuration>/<framework>/`.</span></span>  <span data-ttu-id="8ff7a-162">W przypadku projektów z wieloma platformami docelowymi (za pośrednictwem `TargetFrameworks` Właściwości) należy również zdefiniować, `--framework` kiedy należy określić tę opcję.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-162">For projects with multiple target frameworks (via the `TargetFrameworks` property), you also need to define `--framework` when you specify this option.</span></span>

- **`-r|--runtime <RUNTIME_IDENTIFIER>`**

  <span data-ttu-id="8ff7a-163">Określa docelowy środowisko uruchomieniowe.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-163">Specifies the target runtime.</span></span> <span data-ttu-id="8ff7a-164">Aby uzyskać listę identyfikatorów środowiska uruchomieniowego (RID), zobacz [wykaz identyfikatorów RID](../rid-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="8ff7a-164">For a list of Runtime Identifiers (RIDs), see the [RID catalog](../rid-catalog.md).</span></span>

- **`--source <SOURCE>`**

  <span data-ttu-id="8ff7a-165">Identyfikator URI źródła pakietu NuGet do użycia podczas operacji przywracania.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-165">The URI of the NuGet package source to use during the restore operation.</span></span>

- **`-v|--verbosity <LEVEL>`**

  <span data-ttu-id="8ff7a-166">Ustawia poziom szczegółowości programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-166">Sets the MSBuild verbosity level.</span></span> <span data-ttu-id="8ff7a-167">Dozwolone wartości to `q[uiet]` , `m[inimal]` , `n[ormal]` , `d[etailed]` i `diag[nostic]` .</span><span class="sxs-lookup"><span data-stu-id="8ff7a-167">Allowed values are `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`, and `diag[nostic]`.</span></span> <span data-ttu-id="8ff7a-168">Wartość domyślna to `minimal`.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-168">The default is `minimal`.</span></span>

- **`--version-suffix <VERSION_SUFFIX>`**

  <span data-ttu-id="8ff7a-169">Ustawia wartość `$(VersionSuffix)` właściwości, która ma być używana podczas kompilowania projektu.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-169">Sets the value of the `$(VersionSuffix)` property to use when building the project.</span></span> <span data-ttu-id="8ff7a-170">Działa to tylko wtedy, gdy `$(Version)` Właściwość nie jest ustawiona.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-170">This only works if the `$(Version)` property isn't set.</span></span> <span data-ttu-id="8ff7a-171">Następnie `$(Version)` jest ustawiona na `$(VersionPrefix)` połączone z `$(VersionSuffix)` , oddzielone kreską.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-171">Then, `$(Version)` is set to the `$(VersionPrefix)` combined with the `$(VersionSuffix)`, separated by a dash.</span></span>

## <a name="examples"></a><span data-ttu-id="8ff7a-172">Przykłady</span><span class="sxs-lookup"><span data-stu-id="8ff7a-172">Examples</span></span>

- <span data-ttu-id="8ff7a-173">Kompiluj projekt i jego zależności:</span><span class="sxs-lookup"><span data-stu-id="8ff7a-173">Build a project and its dependencies:</span></span>

  ```dotnetcli
  dotnet build
  ```

- <span data-ttu-id="8ff7a-174">Kompilowanie projektu i jego zależności przy użyciu konfiguracji wydania:</span><span class="sxs-lookup"><span data-stu-id="8ff7a-174">Build a project and its dependencies using Release configuration:</span></span>

  ```dotnetcli
  dotnet build --configuration Release
  ```

- <span data-ttu-id="8ff7a-175">Kompiluj projekt i jego zależności dla określonego środowiska uruchomieniowego (w tym przykładzie Ubuntu 18,04):</span><span class="sxs-lookup"><span data-stu-id="8ff7a-175">Build a project and its dependencies for a specific runtime (in this example, Ubuntu 18.04):</span></span>

  ```dotnetcli
  dotnet build --runtime ubuntu.18.04-x64
  ```

- <span data-ttu-id="8ff7a-176">Kompiluj projekt i Użyj określonego źródła pakietu NuGet podczas operacji przywracania:</span><span class="sxs-lookup"><span data-stu-id="8ff7a-176">Build the project and use the specified NuGet package source during the restore operation:</span></span>

  ```dotnetcli
  dotnet build --source c:\packages\mypackages
  ```

- <span data-ttu-id="8ff7a-177">Skompiluj projekt i ustaw wersję 1.2.3.4 jako parametr kompilacji przy użyciu `-p` [opcji MSBuild](#msbuild):</span><span class="sxs-lookup"><span data-stu-id="8ff7a-177">Build the project and set version 1.2.3.4 as a build parameter using the `-p` [MSBuild option](#msbuild):</span></span>

  ```dotnetcli
  dotnet build -p:Version=1.2.3.4
  ```
