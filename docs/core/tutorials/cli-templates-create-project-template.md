---
title: Utwórz szablon projektu dla nowego dotnet
description: Dowiedz się, jak utworzyć szablon projektu dla nowego polecenia dotnet.
author: adegeo
ms.date: 12/11/2020
ms.topic: tutorial
ms.author: adegeo
ms.openlocfilehash: ed40cfd303c70c7b8f198a0f5b593bf1e1ebeaf8
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2020
ms.locfileid: "97513136"
---
# <a name="tutorial-create-a-project-template"></a><span data-ttu-id="0df5c-103">Samouczek: Tworzenie szablonu projektu</span><span class="sxs-lookup"><span data-stu-id="0df5c-103">Tutorial: Create a project template</span></span>

<span data-ttu-id="0df5c-104">Za pomocą platformy .NET można tworzyć i wdrażać szablony generujące projekty, pliki, nawet zasoby.</span><span class="sxs-lookup"><span data-stu-id="0df5c-104">With .NET, you can create and deploy templates that generate projects, files, even resources.</span></span> <span data-ttu-id="0df5c-105">Ten samouczek jest drugą częścią serii, która zawiera informacje na temat tworzenia, instalowania i odinstalowywania szablonów do użycia z `dotnet new` poleceniem.</span><span class="sxs-lookup"><span data-stu-id="0df5c-105">This tutorial is part two of a series that teaches you how to create, install, and uninstall, templates for use with the `dotnet new` command.</span></span>

<span data-ttu-id="0df5c-106">W tej części serii dowiesz się, jak:</span><span class="sxs-lookup"><span data-stu-id="0df5c-106">In this part of the series you'll learn how to:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="0df5c-107">Tworzenie zasobów szablonu projektu</span><span class="sxs-lookup"><span data-stu-id="0df5c-107">Create the resources of a project template</span></span>
> * <span data-ttu-id="0df5c-108">Tworzenie folderu i pliku konfiguracji szablonu</span><span class="sxs-lookup"><span data-stu-id="0df5c-108">Create the template config folder and file</span></span>
> * <span data-ttu-id="0df5c-109">Instalowanie szablonu ze ścieżki pliku</span><span class="sxs-lookup"><span data-stu-id="0df5c-109">Install a template from a file path</span></span>
> * <span data-ttu-id="0df5c-110">Testowanie szablonu elementu</span><span class="sxs-lookup"><span data-stu-id="0df5c-110">Test an item template</span></span>
> * <span data-ttu-id="0df5c-111">Odinstaluj szablon elementu</span><span class="sxs-lookup"><span data-stu-id="0df5c-111">Uninstall an item template</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0df5c-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0df5c-112">Prerequisites</span></span>

* <span data-ttu-id="0df5c-113">Ukończ [część 1](cli-templates-create-item-template.md) tej serii samouczków.</span><span class="sxs-lookup"><span data-stu-id="0df5c-113">Complete [part 1](cli-templates-create-item-template.md) of this tutorial series.</span></span>
* <span data-ttu-id="0df5c-114">Otwórz Terminal i przejdź do folderu _working\templates_ .</span><span class="sxs-lookup"><span data-stu-id="0df5c-114">Open a terminal and navigate to the _working\templates_ folder.</span></span>

## <a name="create-a-project-template"></a><span data-ttu-id="0df5c-115">Utwórz szablon projektu</span><span class="sxs-lookup"><span data-stu-id="0df5c-115">Create a project template</span></span>

<span data-ttu-id="0df5c-116">Szablony projektów tworzą gotowe do uruchomienia projekty, które ułatwiają użytkownikom rozpoczęcie pracy z zestawem roboczym kodu.</span><span class="sxs-lookup"><span data-stu-id="0df5c-116">Project templates produce ready-to-run projects that make it easy for users to start with a working set of code.</span></span> <span data-ttu-id="0df5c-117">Platforma .NET zawiera kilka szablonów projektu, takich jak Aplikacja konsolowa lub Biblioteka klas.</span><span class="sxs-lookup"><span data-stu-id="0df5c-117">.NET includes a few project templates such as a console application or a class library.</span></span> <span data-ttu-id="0df5c-118">W tym przykładzie utworzysz nowy projekt konsoli, który umożliwia C# 9,0 i tworzy `async main` punkt wejścia.</span><span class="sxs-lookup"><span data-stu-id="0df5c-118">In this example, you'll create a new console project that enables C# 9.0 and produces an `async main` entry point.</span></span>

<span data-ttu-id="0df5c-119">W terminalu przejdź do folderu _working\templates_ i Utwórz nowy podfolder o nazwie _consoleasync_.</span><span class="sxs-lookup"><span data-stu-id="0df5c-119">In your terminal, navigate to the _working\templates_ folder and create a new subfolder named _consoleasync_.</span></span> <span data-ttu-id="0df5c-120">Wprowadź podfolder i uruchom `dotnet new console` w celu wygenerowania standardowej aplikacji konsolowej.</span><span class="sxs-lookup"><span data-stu-id="0df5c-120">Enter the subfolder and run `dotnet new console` to generate the standard console application.</span></span> <span data-ttu-id="0df5c-121">Będziesz edytować pliki utworzone przez ten szablon w celu utworzenia nowego szablonu.</span><span class="sxs-lookup"><span data-stu-id="0df5c-121">You'll be editing the files produced by this template to create a new template.</span></span>

```console
working
└───templates
    └───consoleasync
            consoleasync.csproj
            Program.cs
```

## <a name="modify-programcs"></a><span data-ttu-id="0df5c-122">Modyfikuj Program.cs</span><span class="sxs-lookup"><span data-stu-id="0df5c-122">Modify Program.cs</span></span>

<span data-ttu-id="0df5c-123">Otwórz plik _program.cs_ .</span><span class="sxs-lookup"><span data-stu-id="0df5c-123">Open up the _program.cs_ file.</span></span> <span data-ttu-id="0df5c-124">Projekt konsoli nie używa asynchronicznego punktu wejścia, więc Dodajmy ten element.</span><span class="sxs-lookup"><span data-stu-id="0df5c-124">The console project doesn't use an asynchronous entry point, so let's add that.</span></span> <span data-ttu-id="0df5c-125">Zmień kod na następujący i Zapisz plik.</span><span class="sxs-lookup"><span data-stu-id="0df5c-125">Change your code to the following and save the file.</span></span>

```csharp
using System;
using System.Threading.Tasks;

namespace consoleasync
{
    class Program
    {
        static async Task Main(string[] args)
        {
            await Console.Out.WriteAsync("Hello World with C# 9.0!");
        }
    }
}
```

## <a name="modify-consoleasynccsproj"></a><span data-ttu-id="0df5c-126">Modyfikuj consoleasync. csproj</span><span class="sxs-lookup"><span data-stu-id="0df5c-126">Modify consoleasync.csproj</span></span>

<span data-ttu-id="0df5c-127">Zaktualizujmy wersję języka C# używaną przez projekt do wersji 9,0.</span><span class="sxs-lookup"><span data-stu-id="0df5c-127">Let's update the C# language version the project uses to version 9.0.</span></span> <span data-ttu-id="0df5c-128">Edytuj plik _consoleasync. csproj_ i Dodaj `<LangVersion>` ustawienie do `<PropertyGroup>` węzła.</span><span class="sxs-lookup"><span data-stu-id="0df5c-128">Edit the _consoleasync.csproj_ file and add the `<LangVersion>` setting to a `<PropertyGroup>` node.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net5.0</TargetFramework>

    <LangVersion>9.0</LangVersion>

  </PropertyGroup>
  
</Project>
```

## <a name="build-the-project"></a><span data-ttu-id="0df5c-129">Kompilowanie projektu</span><span class="sxs-lookup"><span data-stu-id="0df5c-129">Build the project</span></span>

<span data-ttu-id="0df5c-130">Przed ukończeniem szablonu projektu należy go przetestować, aby upewnić się, że kompiluje i działa poprawnie.</span><span class="sxs-lookup"><span data-stu-id="0df5c-130">Before you complete a project template, you should test it to make sure it compiles and runs correctly.</span></span>

<span data-ttu-id="0df5c-131">W terminalu uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="0df5c-131">In your terminal, run the following command.</span></span>

```dotnetcli
dotnet run
```

<span data-ttu-id="0df5c-132">Otrzymujesz następujące dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="0df5c-132">You get the following output.</span></span>

```console
Hello World with C# 9.0!
```

<span data-ttu-id="0df5c-133">Można usunąć foldery _obj_ i _bin_ utworzone przy użyciu `dotnet run` .</span><span class="sxs-lookup"><span data-stu-id="0df5c-133">You can delete the _obj_ and _bin_ folders created by using `dotnet run`.</span></span> <span data-ttu-id="0df5c-134">Usunięcie tych plików gwarantuje, że szablon zawiera tylko pliki powiązane z szablonem, a nie wszystkie pliki, które wynikają z akcji kompilacji.</span><span class="sxs-lookup"><span data-stu-id="0df5c-134">Deleting these files ensures your template only includes the files related to your template and not any files that result from a build action.</span></span>

<span data-ttu-id="0df5c-135">Teraz, gdy masz już utworzoną zawartość szablonu, musisz utworzyć konfigurację szablonu w folderze głównym szablonu.</span><span class="sxs-lookup"><span data-stu-id="0df5c-135">Now that you have the content of the template created, you need to create the template config at the root folder of the template.</span></span>

## <a name="create-the-template-config"></a><span data-ttu-id="0df5c-136">Utwórz konfigurację szablonu</span><span class="sxs-lookup"><span data-stu-id="0df5c-136">Create the template config</span></span>

<span data-ttu-id="0df5c-137">Szablony są rozpoznawane w programie .NET według specjalnego folderu i pliku konfiguracji, który istnieje w katalogu głównym szablonu.</span><span class="sxs-lookup"><span data-stu-id="0df5c-137">Templates are recognized in .NET by a special folder and config file that exist at the root of your template.</span></span> <span data-ttu-id="0df5c-138">W tym samouczku folder szablonu znajduje się w lokalizacji _working\templates\consoleasync_.</span><span class="sxs-lookup"><span data-stu-id="0df5c-138">In this tutorial, your template folder is located at _working\templates\consoleasync_.</span></span>

<span data-ttu-id="0df5c-139">Podczas tworzenia szablonu wszystkie pliki i foldery znajdujące się w folderze szablonów są uwzględniane jako część szablonu, z wyjątkiem folderu specjalnej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="0df5c-139">When you create a template, all files and folders in the template folder are included as part of the template except for the special config folder.</span></span> <span data-ttu-id="0df5c-140">Ten folder konfiguracji ma nazwę _.template.config_.</span><span class="sxs-lookup"><span data-stu-id="0df5c-140">This config folder is named _.template.config_.</span></span>

<span data-ttu-id="0df5c-141">Najpierw utwórz nowy podfolder o nazwie _.template.config_, wprowadź go.</span><span class="sxs-lookup"><span data-stu-id="0df5c-141">First, create a new subfolder named _.template.config_, enter it.</span></span> <span data-ttu-id="0df5c-142">Następnie utwórz nowy plik o nazwie _template.json_.</span><span class="sxs-lookup"><span data-stu-id="0df5c-142">Then, create a new file named _template.json_.</span></span> <span data-ttu-id="0df5c-143">Struktura folderów powinna wyglądać następująco.</span><span class="sxs-lookup"><span data-stu-id="0df5c-143">Your folder structure should look like this.</span></span>

```console
working
└───templates
    └───consoleasync
        └───.template.config
                template.json
```

<span data-ttu-id="0df5c-144">Otwórz _template.jsw_ ulubionym edytorze tekstu i wklej go w poniższym kodzie JSON i Zapisz.</span><span class="sxs-lookup"><span data-stu-id="0df5c-144">Open the _template.json_ with your favorite text editor and paste in the following json code and save it.</span></span>

```json
{
  "$schema": "http://json.schemastore.org/template",
  "author": "Me",
  "classifications": [ "Common", "Console", "C#9" ],
  "identity": "ExampleTemplate.AsyncProject",
  "name": "Example templates: async project",
  "shortName": "consoleasync",
  "tags": {
    "language": "C#",
    "type": "project"
  }
}
```

<span data-ttu-id="0df5c-145">Ten plik konfiguracji zawiera wszystkie ustawienia szablonu.</span><span class="sxs-lookup"><span data-stu-id="0df5c-145">This config file contains all of the settings for your template.</span></span> <span data-ttu-id="0df5c-146">Można zobaczyć ustawienia podstawowe, takie jak `name` i, `shortName` ale również `tags/type` wartość, która jest ustawiona na `project` .</span><span class="sxs-lookup"><span data-stu-id="0df5c-146">You can see the basic settings such as `name` and `shortName` but also there's a `tags/type` value that's set to `project`.</span></span> <span data-ttu-id="0df5c-147">Spowoduje to wyznaczenie szablonu jako szablonu projektu.</span><span class="sxs-lookup"><span data-stu-id="0df5c-147">This designates your template as a project template.</span></span> <span data-ttu-id="0df5c-148">Nie ma ograniczeń dotyczących typu tworzonego szablonu.</span><span class="sxs-lookup"><span data-stu-id="0df5c-148">There's no restriction on the type of template you create.</span></span> <span data-ttu-id="0df5c-149">`item`Wartości i `project` są wspólnymi nazwami zalecanymi przez platformę .NET, aby umożliwić użytkownikom łatwe filtrowanie typu szukanego szablonu.</span><span class="sxs-lookup"><span data-stu-id="0df5c-149">The `item` and `project` values are common names that .NET recommends so that users can easily filter the type of template they're searching for.</span></span>

<span data-ttu-id="0df5c-150">`classifications`Element reprezentuje kolumnę **Tagi** , która pojawia się po uruchomieniu `dotnet new` i wyświetleniu listy szablonów.</span><span class="sxs-lookup"><span data-stu-id="0df5c-150">The `classifications` item represents the **tags** column you see when you run `dotnet new` and get a list of templates.</span></span> <span data-ttu-id="0df5c-151">Użytkownicy mogą również wyszukiwać w oparciu o znaczniki klasyfikacji.</span><span class="sxs-lookup"><span data-stu-id="0df5c-151">Users can also search based on classification tags.</span></span> <span data-ttu-id="0df5c-152">Nie należy mylić `tags` właściwości w pliku JSON z `classifications` listą tagów.</span><span class="sxs-lookup"><span data-stu-id="0df5c-152">Don't confuse the `tags` property in the json file with the `classifications` tags list.</span></span> <span data-ttu-id="0df5c-153">Te dwa różne rzeczy są uważane za podobne.</span><span class="sxs-lookup"><span data-stu-id="0df5c-153">They're two different things unfortunately named similarly.</span></span> <span data-ttu-id="0df5c-154">Pełny schemat *template.jsw* pliku znajduje się w [magazynie schematów JSON](http://json.schemastore.org/template).</span><span class="sxs-lookup"><span data-stu-id="0df5c-154">The full schema for the *template.json* file is found at the [JSON Schema Store](http://json.schemastore.org/template).</span></span> <span data-ttu-id="0df5c-155">Aby uzyskać więcej informacji na temat *template.jsw* pliku, zobacz stronę [typu "dotnet tworzenia szablonów wiki](https://github.com/dotnet/templating/wiki)".</span><span class="sxs-lookup"><span data-stu-id="0df5c-155">For more information about the *template.json* file, see the [dotnet templating wiki](https://github.com/dotnet/templating/wiki).</span></span>

<span data-ttu-id="0df5c-156">Teraz, gdy masz prawidłowy _.template.config/template.jsdla_ pliku, szablon jest gotowy do zainstalowania.</span><span class="sxs-lookup"><span data-stu-id="0df5c-156">Now that you have a valid _.template.config/template.json_ file, your template is ready to be installed.</span></span> <span data-ttu-id="0df5c-157">Przed zainstalowaniem szablonu upewnij się, że usunięto wszystkie foldery i pliki dodatkowe pliki, które nie mają być dołączone do szablonu, takie jak foldery _bin_ lub _obj_ .</span><span class="sxs-lookup"><span data-stu-id="0df5c-157">Before you install the template, make sure that you delete any extra files folders and files you don't want included in your template, like the _bin_ or _obj_ folders.</span></span> <span data-ttu-id="0df5c-158">W terminalu przejdź do folderu _consoleasync_ i uruchom polecenie, `dotnet new -i .\` Aby zainstalować szablon znajdujący się w bieżącym folderze.</span><span class="sxs-lookup"><span data-stu-id="0df5c-158">In your terminal, navigate to the _consoleasync_ folder and run `dotnet new -i .\` to install the template located at the current folder.</span></span> <span data-ttu-id="0df5c-159">Jeśli używasz systemu operacyjnego Linux lub macOS, użyj ukośnika: `dotnet new -i ./` .</span><span class="sxs-lookup"><span data-stu-id="0df5c-159">If you're using a Linux or macOS operating system, use a forward slash: `dotnet new -i ./`.</span></span>

<span data-ttu-id="0df5c-160">To polecenie wyświetla listę zainstalowanych szablonów, które powinny obejmować użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0df5c-160">This command outputs the list of templates installed, which should include yours.</span></span>

```dotnetcli
dotnet new -i .\
```

<span data-ttu-id="0df5c-161">Dane wyjściowe są podobne do poniższych.</span><span class="sxs-lookup"><span data-stu-id="0df5c-161">You get output similar to the following.</span></span>

```console
Usage: new [options]

Options:
  -h, --help          Displays help for this command.
  -l, --list          Lists templates containing the specified name. If no name is specified, lists all templates.

... cut to save space ...

Templates                                         Short Name               Language          Tags
--------------------------------------------      -------------------      ------------      ----------------------
Console Application                               console                  [C#], F#, VB      Common/Console
Example templates: async project                  consoleasync             [C#]              Common/Console/C#9
Class library                                     classlib                 [C#], F#, VB      Common/Library
WPF Application                                   wpf                      [C#], VB          Common/WPF
```

### <a name="test-the-project-template"></a><span data-ttu-id="0df5c-162">Testowanie szablonu projektu</span><span class="sxs-lookup"><span data-stu-id="0df5c-162">Test the project template</span></span>

<span data-ttu-id="0df5c-163">Teraz, gdy masz zainstalowany szablon projektu, przetestuj go.</span><span class="sxs-lookup"><span data-stu-id="0df5c-163">Now that you have a project template installed, test it.</span></span>

1. <span data-ttu-id="0df5c-164">Przejdź do folderu _testowego_</span><span class="sxs-lookup"><span data-stu-id="0df5c-164">Navigate to the _test_ folder</span></span>

1. <span data-ttu-id="0df5c-165">Utwórz nową aplikację konsolową przy użyciu następującego polecenia, które generuje projekt roboczy, który można łatwo przetestować przy użyciu `dotnet run` polecenia.</span><span class="sxs-lookup"><span data-stu-id="0df5c-165">Create a new console application with the following command which generates a working project you can easily test with the `dotnet run` command.</span></span>

    ```dotnetcli
    dotnet new consoleasync
    ```

    <span data-ttu-id="0df5c-166">Otrzymujesz następujące dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="0df5c-166">You get the following output.</span></span>

    ```console
    The template "Example templates: async project" was created successfully.
    ```

1. <span data-ttu-id="0df5c-167">Uruchom projekt przy użyciu następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="0df5c-167">Run the project using the following command.</span></span>

    ```dotnetcli
    dotnet run
    ```

    <span data-ttu-id="0df5c-168">Otrzymujesz następujące dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="0df5c-168">You get the following output.</span></span>

    ```console
    Hello World with C# 9.0!
    ```

<span data-ttu-id="0df5c-169">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="0df5c-169">Congratulations!</span></span> <span data-ttu-id="0df5c-170">Szablon projektu został utworzony i wdrożony przy użyciu platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="0df5c-170">You created and deployed a project template with .NET.</span></span> <span data-ttu-id="0df5c-171">W ramach przygotowania do następnej części tej serii samouczków należy odinstalować utworzony szablon.</span><span class="sxs-lookup"><span data-stu-id="0df5c-171">In preparation for the next part of this tutorial series, you must uninstall the template you created.</span></span> <span data-ttu-id="0df5c-172">Pamiętaj, aby usunąć wszystkie pliki z folderu _testowego_ .</span><span class="sxs-lookup"><span data-stu-id="0df5c-172">Make sure to delete all files from the _test_ folder too.</span></span> <span data-ttu-id="0df5c-173">Spowoduje to powrót do stanu czystego gotowego do następnej głównej sekcji tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="0df5c-173">This will get you back to a clean state ready for the next major section of this tutorial.</span></span>

### <a name="uninstall-the-template"></a><span data-ttu-id="0df5c-174">Odinstaluj szablon</span><span class="sxs-lookup"><span data-stu-id="0df5c-174">Uninstall the template</span></span>

<span data-ttu-id="0df5c-175">Ponieważ szablon został zainstalowany przy użyciu ścieżki pliku, należy go odinstalować z **bezwzględną** ścieżką pliku.</span><span class="sxs-lookup"><span data-stu-id="0df5c-175">Because you installed the template by using a file path, you must uninstall it with the **absolute** file path.</span></span> <span data-ttu-id="0df5c-176">Listę zainstalowanych szablonów można wyświetlić, uruchamiając `dotnet new -u` polecenie.</span><span class="sxs-lookup"><span data-stu-id="0df5c-176">You can see a list of templates installed by running the `dotnet new -u` command.</span></span> <span data-ttu-id="0df5c-177">Szablon powinien zostać wyświetlony jako ostatni.</span><span class="sxs-lookup"><span data-stu-id="0df5c-177">Your template should be listed last.</span></span> <span data-ttu-id="0df5c-178">Użyj `Uninstall Command` listy, aby odinstalować szablon.</span><span class="sxs-lookup"><span data-stu-id="0df5c-178">Use the `Uninstall Command` listed to uninstall your template.</span></span>

```dotnetcli
dotnet new -u
```

<span data-ttu-id="0df5c-179">Dane wyjściowe są podobne do poniższych.</span><span class="sxs-lookup"><span data-stu-id="0df5c-179">You get output similar to the following.</span></span>

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

  C:\Test\templatetutorial\working\templates\consoleasync
    Templates:
      Example templates: async project (consoleasync) C#
    Uninstall Command:
      dotnet new -u C:\working\templates\consoleasync
```

<span data-ttu-id="0df5c-180">Aby odinstalować utworzony szablon, uruchom polecenie `Uninstall Command` , które jest wyświetlane w danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="0df5c-180">To uninstall the template that you created, run the `Uninstall Command` that is shown in the output.</span></span>

```dotnetcli
dotnet new -u C:\working\templates\consoleasync
```

## <a name="next-steps"></a><span data-ttu-id="0df5c-181">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0df5c-181">Next steps</span></span>

<span data-ttu-id="0df5c-182">W tym samouczku utworzono szablon projektu.</span><span class="sxs-lookup"><span data-stu-id="0df5c-182">In this tutorial, you created a project template.</span></span> <span data-ttu-id="0df5c-183">Aby dowiedzieć się, jak spakować szablon elementu i projektu do łatwego w użyciu pliku, Kontynuuj tę serię samouczków.</span><span class="sxs-lookup"><span data-stu-id="0df5c-183">To learn how to package both the item and project templates into an easy-to-use file, continue this tutorial series.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0df5c-184">Tworzenie pakietu szablonów</span><span class="sxs-lookup"><span data-stu-id="0df5c-184">Create a template pack</span></span>](cli-templates-create-template-pack.md)
