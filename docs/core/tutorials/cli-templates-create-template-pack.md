---
title: Tworzenie pakietu szablonów dla nowego dotnet
description: Dowiedz się, jak utworzyć plik CSPROJ, który będzie kompilować pakiet szablonów dla nowego polecenia dotnet.
author: adegeo
ms.date: 12/11/2020
ms.topic: tutorial
ms.author: adegeo
ms.openlocfilehash: 2aea143f1e41d580de41a9cc9e924d70b55695db
ms.sourcegitcommit: 635a0ff775d2447a81ef7233a599b8f88b162e5d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/17/2020
ms.locfileid: "97633601"
---
# <a name="tutorial-create-a-template-pack"></a><span data-ttu-id="3e80e-103">Samouczek: Tworzenie pakietu szablonów</span><span class="sxs-lookup"><span data-stu-id="3e80e-103">Tutorial: Create a template pack</span></span>

<span data-ttu-id="3e80e-104">Za pomocą platformy .NET można tworzyć i wdrażać szablony generujące projekty, pliki, nawet zasoby.</span><span class="sxs-lookup"><span data-stu-id="3e80e-104">With .NET, you can create and deploy templates that generate projects, files, even resources.</span></span> <span data-ttu-id="3e80e-105">Ten samouczek jest trzecią częścią serii, która zawiera informacje na temat tworzenia, instalowania i odinstalowywania szablonów do użycia z `dotnet new` poleceniem.</span><span class="sxs-lookup"><span data-stu-id="3e80e-105">This tutorial is part three of a series that teaches you how to create, install, and uninstall templates for use with the `dotnet new` command.</span></span>

<span data-ttu-id="3e80e-106">W tej części serii dowiesz się, jak:</span><span class="sxs-lookup"><span data-stu-id="3e80e-106">In this part of the series you'll learn how to:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="3e80e-107">Utwórz \* projekt. csproj, aby skompilować pakiet szablonów</span><span class="sxs-lookup"><span data-stu-id="3e80e-107">Create a \*.csproj project to build a template pack</span></span>
> * <span data-ttu-id="3e80e-108">Konfigurowanie pliku projektu do pakowania</span><span class="sxs-lookup"><span data-stu-id="3e80e-108">Configure the project file for packing</span></span>
> * <span data-ttu-id="3e80e-109">Instalowanie szablonu z pliku pakietu NuGet</span><span class="sxs-lookup"><span data-stu-id="3e80e-109">Install a template from a NuGet package file</span></span>
> * <span data-ttu-id="3e80e-110">Odinstalowywanie szablonu według identyfikatora pakietu</span><span class="sxs-lookup"><span data-stu-id="3e80e-110">Uninstall a template by package ID</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e80e-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3e80e-111">Prerequisites</span></span>

* <span data-ttu-id="3e80e-112">Ukończ [część 1](cli-templates-create-item-template.md) i [część 2](cli-templates-create-project-template.md) tej serii samouczków.</span><span class="sxs-lookup"><span data-stu-id="3e80e-112">Complete [part 1](cli-templates-create-item-template.md) and [part 2](cli-templates-create-project-template.md) of this tutorial series.</span></span>

  <span data-ttu-id="3e80e-113">Ten samouczek używa dwóch szablonów utworzonych w pierwszych dwóch częściach tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="3e80e-113">This tutorial uses the two templates created in the first two parts of this tutorial.</span></span> <span data-ttu-id="3e80e-114">Możesz użyć innego szablonu, tak długo, jak skopiujesz szablon jako folder do folderu _working\templates \\_ .</span><span class="sxs-lookup"><span data-stu-id="3e80e-114">You can use a different template as long as you copy the template, as a folder, into the _working\templates\\_ folder.</span></span>

* <span data-ttu-id="3e80e-115">Otwórz Terminal i przejdź do folderu _roboczego \\_ .</span><span class="sxs-lookup"><span data-stu-id="3e80e-115">Open a terminal and navigate to the _working\\_ folder.</span></span>

## <a name="create-a-template-pack-project"></a><span data-ttu-id="3e80e-116">Tworzenie projektu pakietu szablonów</span><span class="sxs-lookup"><span data-stu-id="3e80e-116">Create a template pack project</span></span>

<span data-ttu-id="3e80e-117">Pakiet szablonów to jeden lub więcej szablonów pakowanych do pliku.</span><span class="sxs-lookup"><span data-stu-id="3e80e-117">A template pack is one or more templates packaged into a file.</span></span> <span data-ttu-id="3e80e-118">Podczas instalowania lub odinstalowywania pakietu wszystkie szablony zawarte w pakiecie są dodawane lub usuwane odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="3e80e-118">When you install or uninstall a pack, all templates contained in the pack are added or removed, respectively.</span></span> <span data-ttu-id="3e80e-119">Poprzednie części tej serii samouczków działały tylko z poszczególnymi szablonami.</span><span class="sxs-lookup"><span data-stu-id="3e80e-119">The previous parts of this tutorial series only worked with individual templates.</span></span> <span data-ttu-id="3e80e-120">Aby udostępnić niespakowany szablon, należy skopiować folder szablonu i zainstalować go za pośrednictwem tego folderu.</span><span class="sxs-lookup"><span data-stu-id="3e80e-120">To share a non-packed template, you have to copy the template folder and install via that folder.</span></span> <span data-ttu-id="3e80e-121">Ponieważ pakiet szablonów może mieć więcej niż jeden szablon w tym samym pliku, udostępnianie jest łatwiejsze.</span><span class="sxs-lookup"><span data-stu-id="3e80e-121">Because a template pack can have more than one template in it, and is a single file, sharing is easier.</span></span>

<span data-ttu-id="3e80e-122">Pakiety szablonów są reprezentowane przez plik pakietu NuGet (_. nupkg_).</span><span class="sxs-lookup"><span data-stu-id="3e80e-122">Template packs are represented by a NuGet package (_.nupkg_) file.</span></span> <span data-ttu-id="3e80e-123">Podobnie jak każdy pakiet NuGet, można przekazać pakiet szablonów do źródła danych NuGet.</span><span class="sxs-lookup"><span data-stu-id="3e80e-123">And, like any NuGet package, you can upload the template pack to a NuGet feed.</span></span> <span data-ttu-id="3e80e-124">`dotnet new -i`Polecenie obsługuje instalowanie pakietu Template Pack z kanału informacyjnego pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="3e80e-124">The `dotnet new -i` command supports installing template pack from a NuGet package feed.</span></span> <span data-ttu-id="3e80e-125">Ponadto można bezpośrednio zainstalować pakiet szablonów z pliku _. nupkg_ .</span><span class="sxs-lookup"><span data-stu-id="3e80e-125">Additionally, you can install a template pack from a _.nupkg_ file directly.</span></span>

<span data-ttu-id="3e80e-126">Zwykle plik projektu C# jest używany do kompilowania kodu i tworzenia danych binarnych.</span><span class="sxs-lookup"><span data-stu-id="3e80e-126">Normally you use a C# project file to compile code and produce a binary.</span></span> <span data-ttu-id="3e80e-127">Jednak projekt może być również używany do generowania pakietu szablonów.</span><span class="sxs-lookup"><span data-stu-id="3e80e-127">However, the project can also be used to generate a template pack.</span></span> <span data-ttu-id="3e80e-128">Zmieniając ustawienia elementu _. csproj_, można zapobiec kompilacji dowolnego kodu, a zamiast tego dołączyć wszystkie zasoby szablonów jako zasoby.</span><span class="sxs-lookup"><span data-stu-id="3e80e-128">By changing the settings of the _.csproj_, you can prevent it from compiling any code and instead include all the assets of your templates as resources.</span></span> <span data-ttu-id="3e80e-129">Po skompilowaniu tego projektu tworzy pakiet NuGet pakietu szablonów.</span><span class="sxs-lookup"><span data-stu-id="3e80e-129">When this project is built, it produces a template pack NuGet package.</span></span>

<span data-ttu-id="3e80e-130">Tworzony pakiet będzie obejmował [szablon elementu](cli-templates-create-item-template.md) i [szablon pakietu](cli-templates-create-project-template.md) utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="3e80e-130">The pack you'll create will include the [item template](cli-templates-create-item-template.md) and [package template](cli-templates-create-project-template.md) previously created.</span></span> <span data-ttu-id="3e80e-131">Ze względu na to, że dwa szablony są pogrupowane w folderze _working\templates \\_ , możemy użyć folderu _roboczego_ dla pliku _. csproj_ .</span><span class="sxs-lookup"><span data-stu-id="3e80e-131">Because we grouped the two templates into the _working\templates\\_ folder, we can use the _working_ folder for the _.csproj_ file.</span></span>

<span data-ttu-id="3e80e-132">W terminalu przejdź do folderu _roboczego_ .</span><span class="sxs-lookup"><span data-stu-id="3e80e-132">In your terminal, navigate to the _working_ folder.</span></span> <span data-ttu-id="3e80e-133">Utwórz nowy projekt i ustaw dla niego nazwę `templatepack` i folder wyjściowy w bieżącym folderze.</span><span class="sxs-lookup"><span data-stu-id="3e80e-133">Create a new project and set the name to `templatepack` and the output folder to the current folder.</span></span>

```dotnetcli
dotnet new console -n templatepack -o .
```

<span data-ttu-id="3e80e-134">`-n`Parametr ustawia nazwę pliku _. csproj_ na _templatepack. csproj_.</span><span class="sxs-lookup"><span data-stu-id="3e80e-134">The `-n` parameter sets the _.csproj_ filename to _templatepack.csproj_.</span></span> <span data-ttu-id="3e80e-135">`-o`Parametr tworzy pliki w bieżącym katalogu.</span><span class="sxs-lookup"><span data-stu-id="3e80e-135">The `-o` parameter creates the files in the current directory.</span></span> <span data-ttu-id="3e80e-136">Powinien zostać wyświetlony wynik podobny do następującego: dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="3e80e-136">You should see a result similar to the following output.</span></span>

```console
The template "Console Application" was created successfully.

Processing post-creation actions...
Running 'dotnet restore' on .\templatepack.csproj...
  Restore completed in 52.38 ms for C:\working\templatepack.csproj.

Restore succeeded.
```

<span data-ttu-id="3e80e-137">Następnie otwórz plik _templatepack. csproj_ w ulubionym edytorze i Zastąp zawartość następującym kodem XML:</span><span class="sxs-lookup"><span data-stu-id="3e80e-137">Next, open the _templatepack.csproj_ file in your favorite editor and replace the content with the following XML:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <PackageType>Template</PackageType>
    <PackageVersion>1.0</PackageVersion>
    <PackageId>AdatumCorporation.Utility.Templates</PackageId>
    <Title>AdatumCorporation Templates</Title>
    <Authors>Me</Authors>
    <Description>Templates to use when creating an application for Adatum Corporation.</Description>
    <PackageTags>dotnet-new;templates;contoso</PackageTags>

    <TargetFramework>netstandard2.0</TargetFramework>

    <IncludeContentInPack>true</IncludeContentInPack>
    <IncludeBuildOutput>false</IncludeBuildOutput>
    <ContentTargetFolders>content</ContentTargetFolders>
    <NoWarn>$(NoWarn);NU5128</NoWarn>
  </PropertyGroup>

  <ItemGroup>
    <Content Include="templates\**\*" Exclude="templates\**\bin\**;templates\**\obj\**" />
    <Compile Remove="**\*" />
  </ItemGroup>

</Project>
```

<span data-ttu-id="3e80e-138">`<PropertyGroup>`Ustawienia w pliku XML powyżej są podzielone na trzy grupy.</span><span class="sxs-lookup"><span data-stu-id="3e80e-138">The `<PropertyGroup>` settings in the XML above is broken into three groups.</span></span> <span data-ttu-id="3e80e-139">Pierwsza grupa zajmuje się właściwościami wymaganymi dla pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="3e80e-139">The first group deals with properties required for a NuGet package.</span></span> <span data-ttu-id="3e80e-140">Trzy `<Package*>` Ustawienia muszą wykonać przy użyciu właściwości pakietu NuGet, aby zidentyfikować pakiet w źródle danych NuGet.</span><span class="sxs-lookup"><span data-stu-id="3e80e-140">The three `<Package*>` settings have to do with the NuGet package properties to identify your package on a NuGet feed.</span></span> <span data-ttu-id="3e80e-141">W `<PackageId>` celu odinstalowania pakietu Template Pack o pojedynczej nazwie zamiast ścieżki do katalogu zostanie użyta wartość.</span><span class="sxs-lookup"><span data-stu-id="3e80e-141">Specifically the `<PackageId>` value is used to uninstall the template pack with a single name instead of a directory path.</span></span> <span data-ttu-id="3e80e-142">Można go również użyć do zainstalowania pakietu Template Pack ze źródła danych NuGet.</span><span class="sxs-lookup"><span data-stu-id="3e80e-142">It can also be used to install the template pack from a NuGet feed.</span></span> <span data-ttu-id="3e80e-143">Pozostałe ustawienia, takie jak `<Title>` i, `<PackageTags>` muszą zawierać metadane wyświetlane w źródle danych NuGet.</span><span class="sxs-lookup"><span data-stu-id="3e80e-143">The remaining settings such as `<Title>` and `<PackageTags>` have to do with metadata displayed on the NuGet feed.</span></span> <span data-ttu-id="3e80e-144">Aby uzyskać więcej informacji na temat ustawień NuGet, zobacz [Właściwości narzędzia NuGet i programu MSBuild](/nuget/reference/msbuild-targets).</span><span class="sxs-lookup"><span data-stu-id="3e80e-144">For more information about NuGet settings, see [NuGet and MSBuild properties](/nuget/reference/msbuild-targets).</span></span>

<span data-ttu-id="3e80e-145">`<TargetFramework>`Ustawienie musi być ustawione tak, aby program MSBuild działał prawidłowo po uruchomieniu polecenia Pack w celu skompilowania i spakowania projektu.</span><span class="sxs-lookup"><span data-stu-id="3e80e-145">The `<TargetFramework>` setting must be set so that MSBuild will run properly when you run the pack command to compile and pack the project.</span></span>

<span data-ttu-id="3e80e-146">Trzy następne ustawienia należy wykonać w celu poprawnego skonfigurowania projektu w celu uwzględnienia szablonów w odpowiednim folderze w pakiecie NuGet, gdy zostanie on utworzony.</span><span class="sxs-lookup"><span data-stu-id="3e80e-146">The next three settings have to do with configuring the project correctly to include the templates in the appropriate folder in the NuGet pack when it's created.</span></span>

<span data-ttu-id="3e80e-147">Ostatnie ustawienie pomija komunikat ostrzegawczy, który nie ma zastosowania do projektów pakietu szablonów.</span><span class="sxs-lookup"><span data-stu-id="3e80e-147">The last setting suppresses a warning message that doesn't apply to template pack projects.</span></span>

<span data-ttu-id="3e80e-148">`<ItemGroup>`Zawiera dwa ustawienia.</span><span class="sxs-lookup"><span data-stu-id="3e80e-148">The `<ItemGroup>` contains two settings.</span></span> <span data-ttu-id="3e80e-149">Pierwsze `<Content>` ustawienie uwzględnia wszystkie elementy w folderze _templates_ jako zawartość.</span><span class="sxs-lookup"><span data-stu-id="3e80e-149">First, the `<Content>` setting includes everything in the _templates_ folder as content.</span></span> <span data-ttu-id="3e80e-150">Jest również ustawiony na wykluczenie dowolnego folderu _bin_ lub _obj_ , aby zapobiec dołączeniu kodu skompilowanego (w przypadku przetestowania i skompilowania szablonów).</span><span class="sxs-lookup"><span data-stu-id="3e80e-150">It's also set to exclude any _bin_ folder or _obj_ folder to prevent any compiled code (if you tested and compiled your templates) from being included.</span></span> <span data-ttu-id="3e80e-151">Po drugie, `<Compile>` ustawienie wyklucza wszystkie pliki kodu z kompilacji niezależnie od tego, gdzie się znajdują.</span><span class="sxs-lookup"><span data-stu-id="3e80e-151">Second, the `<Compile>` setting excludes all code files from compiling no matter where they're located.</span></span> <span data-ttu-id="3e80e-152">To ustawienie uniemożliwia projekt używany do tworzenia pakietu szablonów na podstawie próby skompilowania kodu w hierarchii folderów _szablonów_ .</span><span class="sxs-lookup"><span data-stu-id="3e80e-152">This setting prevents the project being used to create a template pack from trying to compile the code in the _templates_ folder hierarchy.</span></span>

## <a name="build-and-install"></a><span data-ttu-id="3e80e-153">Kompiluj i zainstaluj</span><span class="sxs-lookup"><span data-stu-id="3e80e-153">Build and install</span></span>

<span data-ttu-id="3e80e-154">Zapisz ten plik, a następnie uruchom polecenie Pack</span><span class="sxs-lookup"><span data-stu-id="3e80e-154">Save this file and then run the pack command</span></span>

```dotnetcli
dotnet pack
```

<span data-ttu-id="3e80e-155">To polecenie spowoduje skompilowanie projektu i utworzenie pakietu NuGet w tym folderze _working\bin\Debug_ .</span><span class="sxs-lookup"><span data-stu-id="3e80e-155">This command will build your project and create a NuGet package in This should be the _working\bin\Debug_ folder.</span></span>

```dotnetcli
dotnet pack
```

```console
Microsoft (R) Build Engine version 16.8.0+126527ff1 for .NET
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 123.86 ms for C:\working\templatepack.csproj.

  templatepack -> C:\working\bin\Debug\netstandard2.0\templatepack.dll
  Successfully created package 'C:\working\bin\Debug\AdatumCorporation.Utility.Templates.1.0.0.nupkg'.
```

<span data-ttu-id="3e80e-156">Następnie Zainstaluj plik pakietu szablonów przy użyciu `dotnet new -i PATH_TO_NUPKG_FILE` polecenia.</span><span class="sxs-lookup"><span data-stu-id="3e80e-156">Next, install the template pack file with the `dotnet new -i PATH_TO_NUPKG_FILE` command.</span></span>

```console
C:\working> dotnet new -i C:\working\bin\Debug\AdatumCorporation.Utility.Templates.1.0.0.nupkg
Usage: new [options]

Options:
  -h, --help          Displays help for this command.
  -l, --list          Lists templates containing the specified name. If no name is specified, lists all templates.

... cut to save space ...

Templates                                         Short Name               Language          Tags
--------------------------------------------      -------------------      ------------      ----------------------
Example templates: string extensions              stringext                [C#]              Common/Code
Console Application                               console                  [C#], F#, VB      Common/Console
Example templates: async project                  consoleasync             [C#]              Common/Console/C#9
Class library                                     classlib                 [C#], F#, VB      Common/Library
```

<span data-ttu-id="3e80e-157">Jeśli pakiet NuGet został przekazany do źródła danych NuGet, można użyć `dotnet new -i PACKAGEID` polecenia, gdzie jest taka `PACKAGEID` sama jak `<PackageId>` ustawienie z pliku _. csproj_ .</span><span class="sxs-lookup"><span data-stu-id="3e80e-157">If you uploaded the NuGet package to a NuGet feed, you can use the `dotnet new -i PACKAGEID` command where `PACKAGEID` is the same as the `<PackageId>` setting from the _.csproj_ file.</span></span> <span data-ttu-id="3e80e-158">Ten identyfikator pakietu jest taki sam jak identyfikator pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="3e80e-158">This package ID is the same as the NuGet package identifier.</span></span>

## <a name="uninstall-the-template-pack"></a><span data-ttu-id="3e80e-159">Odinstalowywanie pakietu szablonów</span><span class="sxs-lookup"><span data-stu-id="3e80e-159">Uninstall the template pack</span></span>

<span data-ttu-id="3e80e-160">Niezależnie od tego, jak został zainstalowany pakiet szablonów, z plikiem _. nupkg_ bezpośrednio lub przez źródło danych NuGet, usunięcie pakietu szablonu jest takie samo.</span><span class="sxs-lookup"><span data-stu-id="3e80e-160">No matter how you installed the template pack, either with the _.nupkg_ file directly or by NuGet feed, removing a template pack is the same.</span></span> <span data-ttu-id="3e80e-161">Użyj `<PackageId>` szablonu, który chcesz odinstalować.</span><span class="sxs-lookup"><span data-stu-id="3e80e-161">Use the `<PackageId>` of the template you want to uninstall.</span></span> <span data-ttu-id="3e80e-162">Listę zainstalowanych szablonów można uzyskać, uruchamiając `dotnet new -u` polecenie.</span><span class="sxs-lookup"><span data-stu-id="3e80e-162">You can get a list of templates that are installed by running the `dotnet new -u` command.</span></span>

```dotnetcli
dotnet new -u
```

```console
Template Instantiation Commands for .NET Core CLI

Currently installed items:
  Microsoft.DotNet.Common.ProjectTemplates.2.2
    Details:
      NuGetPackageId: Microsoft.DotNet.Common.ProjectTemplates.2.2
      Version: 1.0.2-beta4
      Author: Microsoft
    Templates:
      Class library (classlib) C#
      Class library (classlib) F#
      Class library (classlib) VB
      Console Application (console) C#
      Console Application (console) F#
      Console Application (console) VB
    Uninstall Command:
      dotnet new -u Microsoft.DotNet.Common.ProjectTemplates.2.2

... cut to save space ...

  AdatumCorporation.Utility.Templates
    Details:
      NuGetPackageId: AdatumCorporation.Utility.Templates
      Version: 1.0.0
      Author: Me
    Templates:
      Example templates: async project (consoleasync) C#
      Example templates: string extensions (stringext) C#
    Uninstall Command:
      dotnet new -u AdatumCorporation.Utility.Templates
```

<span data-ttu-id="3e80e-163">Uruchom, `dotnet new -u AdatumCorporation.Utility.Templates` Aby odinstalować szablon.</span><span class="sxs-lookup"><span data-stu-id="3e80e-163">Run `dotnet new -u AdatumCorporation.Utility.Templates` to uninstall the template.</span></span> <span data-ttu-id="3e80e-164">`dotnet new`Polecenie będzie wyprowadzać informacje pomocy, które powinny pominąć wcześniej zainstalowane szablony.</span><span class="sxs-lookup"><span data-stu-id="3e80e-164">The `dotnet new` command will output help information that should omit the templates you previously installed.</span></span>

<span data-ttu-id="3e80e-165">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="3e80e-165">Congratulations!</span></span> <span data-ttu-id="3e80e-166">Pakiet szablonów został zainstalowany i odinstalowany.</span><span class="sxs-lookup"><span data-stu-id="3e80e-166">you've installed and uninstalled a template pack.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e80e-167">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3e80e-167">Next steps</span></span>

<span data-ttu-id="3e80e-168">Aby dowiedzieć się więcej o szablonach, z których większość już wiesz, zobacz [Szablony niestandardowe dla nowego](../tools/custom-templates.md) artykułu usługi dotnet.</span><span class="sxs-lookup"><span data-stu-id="3e80e-168">To learn more about templates, most of which you've already learned, see the [Custom templates for dotnet new](../tools/custom-templates.md) article.</span></span>

* [<span data-ttu-id="3e80e-169">Witryna typu wiki repozytorium usługi GitHub/tworzenia szablonów</span><span class="sxs-lookup"><span data-stu-id="3e80e-169">dotnet/templating GitHub repo Wiki</span></span>](https://github.com/dotnet/templating/wiki)
* [<span data-ttu-id="3e80e-170">dotnet/dotnet-Template-przykłady repozytorium GitHub</span><span class="sxs-lookup"><span data-stu-id="3e80e-170">dotnet/dotnet-template-samples GitHub repo</span></span>](https://github.com/dotnet/dotnet-template-samples)
* [<span data-ttu-id="3e80e-171">*template.jsw* schemacie w magazynie schematów JSON</span><span class="sxs-lookup"><span data-stu-id="3e80e-171">*template.json* schema at the JSON Schema Store</span></span>](http://json.schemastore.org/template)
