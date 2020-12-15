---
title: 'Samouczek: Tworzenie narzędzia platformy .NET'
description: Dowiedz się, jak utworzyć narzędzie platformy .NET. Narzędzie jest aplikacją konsolową, która jest instalowana przy użyciu interfejsu wiersza polecenia platformy .NET.
ms.topic: tutorial
ms.date: 02/12/2020
ms.openlocfilehash: 8f2dd15982aff9fe2d9db9ce2cff8ac1b22e440e
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2020
ms.locfileid: "97512635"
---
# <a name="tutorial-create-a-net-tool-using-the-net-cli"></a><span data-ttu-id="3c139-104">Samouczek: Tworzenie narzędzia platformy .NET przy użyciu interfejsu wiersza polecenia platformy .NET</span><span class="sxs-lookup"><span data-stu-id="3c139-104">Tutorial: Create a .NET tool using the .NET CLI</span></span>

<span data-ttu-id="3c139-105">**Ten artykuł ma zastosowanie do:** ✔️ .net Core 2,1 SDK i nowszych wersjach</span><span class="sxs-lookup"><span data-stu-id="3c139-105">**This article applies to:** ✔️ .NET Core 2.1 SDK and later versions</span></span>

<span data-ttu-id="3c139-106">W tym samouczku przedstawiono sposób tworzenia i pakowania narzędzia platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="3c139-106">This tutorial teaches you how to create and package a .NET tool.</span></span> <span data-ttu-id="3c139-107">Interfejs wiersza polecenia platformy .NET umożliwia tworzenie aplikacji konsolowej jako narzędzia, które mogą być instalowane i uruchamiane przez inne osoby.</span><span class="sxs-lookup"><span data-stu-id="3c139-107">The .NET CLI lets you create a console application as a tool, which others can install and run.</span></span> <span data-ttu-id="3c139-108">Narzędzia .NET Tools są pakietami NuGet, które są instalowane z interfejsu wiersza polecenia platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="3c139-108">.NET tools are NuGet packages that are installed from the .NET CLI.</span></span> <span data-ttu-id="3c139-109">Aby uzyskać więcej informacji na temat narzędzi, zobacz temat [Narzędzia .NET — Omówienie](global-tools.md).</span><span class="sxs-lookup"><span data-stu-id="3c139-109">For more information about tools, see [.NET tools overview](global-tools.md).</span></span>

<span data-ttu-id="3c139-110">Tworzone narzędzie jest aplikacją konsolową, która przyjmuje komunikat jako dane wejściowe i wyświetla komunikat wraz z wierszami tekstu, które tworzą obraz robota.</span><span class="sxs-lookup"><span data-stu-id="3c139-110">The tool that you'll create is a console application that takes a message as input and displays the message along with lines of text that create the image of a robot.</span></span>

<span data-ttu-id="3c139-111">Jest to pierwsza z serii trzech samouczków.</span><span class="sxs-lookup"><span data-stu-id="3c139-111">This is the first in a series of three tutorials.</span></span> <span data-ttu-id="3c139-112">Ten samouczek obejmuje tworzenie i pakowanie narzędzi.</span><span class="sxs-lookup"><span data-stu-id="3c139-112">In this tutorial, you create and package a tool.</span></span> <span data-ttu-id="3c139-113">W następnych dwóch samouczkach [użyjesz narzędzia jako narzędzia globalnego](global-tools-how-to-use.md) i [Użyj tego narzędzia jako narzędzia lokalnego](local-tools-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="3c139-113">In the next two tutorials you [use the tool as a global tool](global-tools-how-to-use.md) and [use the tool as a local tool](local-tools-how-to-use.md).</span></span> <span data-ttu-id="3c139-114">Procedury tworzenia narzędzia są takie same, niezależnie od tego, czy są używane jako narzędzie globalne, czy jako narzędzie lokalne.</span><span class="sxs-lookup"><span data-stu-id="3c139-114">The procedures for creating a tool are the same whether you use it as a global tool or as a local tool.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3c139-115">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3c139-115">Prerequisites</span></span>

- <span data-ttu-id="3c139-116">[Zestaw .NET SDK 5,0](https://dotnet.microsoft.com/download) lub nowsza wersja.</span><span class="sxs-lookup"><span data-stu-id="3c139-116">[.NET SDK 5.0](https://dotnet.microsoft.com/download) or a later version.</span></span>

  <span data-ttu-id="3c139-117">W tym samouczku jest używany zestaw SDK programu .NET 5,0, ale narzędzia globalne są dostępne począwszy od zestaw .NET Core SDK 2,1.</span><span class="sxs-lookup"><span data-stu-id="3c139-117">This tutorial uses .NET SDK 5.0, but global tools are available starting in .NET Core SDK 2.1.</span></span> <span data-ttu-id="3c139-118">Narzędzia lokalne są dostępne począwszy od zestaw .NET Core SDK 3,0.</span><span class="sxs-lookup"><span data-stu-id="3c139-118">Local tools are available starting in .NET Core SDK 3.0.</span></span>
  
- <span data-ttu-id="3c139-119">Wybrany edytor tekstu lub edytor kodu.</span><span class="sxs-lookup"><span data-stu-id="3c139-119">A text editor or code editor of your choice.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="3c139-120">Tworzenie projektu</span><span class="sxs-lookup"><span data-stu-id="3c139-120">Create a project</span></span>

1. <span data-ttu-id="3c139-121">Otwórz wiersz polecenia i Utwórz folder o nazwie *Repository*.</span><span class="sxs-lookup"><span data-stu-id="3c139-121">Open a command prompt and create a folder named *repository*.</span></span>

1. <span data-ttu-id="3c139-122">Przejdź do folderu *repozytorium* i wprowadź następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="3c139-122">Navigate to the *repository* folder and enter the following command:</span></span>

   ```dotnetcli
   dotnet new console -n microsoft.botsay
   ```

   <span data-ttu-id="3c139-123">Polecenie tworzy nowy folder o nazwie *Microsoft. botsay* w folderze *repozytorium* .</span><span class="sxs-lookup"><span data-stu-id="3c139-123">The command creates a new folder named *microsoft.botsay* under the *repository* folder.</span></span>

1. <span data-ttu-id="3c139-124">Przejdź do folderu *Microsoft. botsay* .</span><span class="sxs-lookup"><span data-stu-id="3c139-124">Navigate to the *microsoft.botsay* folder.</span></span>

   ```console
   cd microsoft.botsay
   ```

## <a name="add-the-code"></a><span data-ttu-id="3c139-125">Dodawanie kodu</span><span class="sxs-lookup"><span data-stu-id="3c139-125">Add the code</span></span>

1. <span data-ttu-id="3c139-126">Otwórz `Program.cs` plik z edytorem kodu.</span><span class="sxs-lookup"><span data-stu-id="3c139-126">Open the `Program.cs` file with your code editor.</span></span>

1. <span data-ttu-id="3c139-127">Dodaj następującą `using` dyrektywę na początku pliku:</span><span class="sxs-lookup"><span data-stu-id="3c139-127">Add the following `using` directive to the top of the file:</span></span>

   ```csharp
   using System.Reflection;
   ```

1. <span data-ttu-id="3c139-128">Zastąp `Main` metodę poniższym kodem, aby przetworzyć argumenty wiersza polecenia dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3c139-128">Replace the `Main` method with the following code to process the command-line arguments for the application.</span></span>

   ```csharp
   static void Main(string[] args)
   {
       if (args.Length == 0)
       {
           var versionString = Assembly.GetEntryAssembly()
                                   .GetCustomAttribute<AssemblyInformationalVersionAttribute>()
                                   .InformationalVersion
                                   .ToString();

           Console.WriteLine($"botsay v{versionString}");
           Console.WriteLine("-------------");
           Console.WriteLine("\nUsage:");
           Console.WriteLine("  botsay <message>");
           return;
       }

       ShowBot(string.Join(' ', args));
   }
   ```

   <span data-ttu-id="3c139-129">Jeśli nie przechodzą żadnych argumentów, zostanie wyświetlony krótki komunikat pomocy.</span><span class="sxs-lookup"><span data-stu-id="3c139-129">If no arguments are passed, a short help message is displayed.</span></span> <span data-ttu-id="3c139-130">W przeciwnym razie wszystkie argumenty są łączone w jeden ciąg i drukowane przez wywołanie `ShowBot` metody utworzonej w następnym kroku.</span><span class="sxs-lookup"><span data-stu-id="3c139-130">Otherwise, all of the arguments are concatenated into a single string and printed by calling the `ShowBot` method that you create in the next step.</span></span>

1. <span data-ttu-id="3c139-131">Dodaj nową metodę o nazwie `ShowBot` , która przyjmuje parametr ciągu.</span><span class="sxs-lookup"><span data-stu-id="3c139-131">Add a new method named `ShowBot` that takes a string parameter.</span></span> <span data-ttu-id="3c139-132">Metoda drukuje komunikat i obraz robota przy użyciu wierszy tekstu.</span><span class="sxs-lookup"><span data-stu-id="3c139-132">The method prints out the message and an image of a robot using lines of text.</span></span>

   ```csharp
   static void ShowBot(string message)
   {
       string bot = $"\n        {message}";
       bot += @"
       __________________
                         \
                          \
                             ....
                             ....'
                              ....
                           ..........
                       .............'..'..
                    ................'..'.....
                  .......'..........'..'..'....
                 ........'..........'..'..'.....
                .'....'..'..........'..'.......'.
                .'..................'...   ......
                .  ......'.........         .....
                .    _            __        ......
               ..    #            ##        ......
              ....       .                 .......
              ......  .......          ............
               ................  ......................
               ........................'................
              ......................'..'......    .......
           .........................'..'.....       .......
        ........    ..'.............'..'....      ..........
      ..'..'...      ...............'.......      ..........
     ...'......     ...... ..........  ......         .......
    ...........   .......              ........        ......
   .......        '...'.'.              '.'.'.'         ....
   .......       .....'..               ..'.....
      ..       ..........               ..'........
             ............               ..............
            .............               '..............
           ...........'..              .'.'............
          ...............              .'.'.............
         .............'..               ..'..'...........
         ...............                 .'..............
          .........                        ..............
           .....
   ";
       Console.WriteLine(bot);
   }
   ```

1. <span data-ttu-id="3c139-133">Zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="3c139-133">Save your changes.</span></span>

## <a name="test-the-application"></a><span data-ttu-id="3c139-134">Testowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="3c139-134">Test the application</span></span>

<span data-ttu-id="3c139-135">Uruchom projekt i zobacz dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="3c139-135">Run the project and see the output.</span></span> <span data-ttu-id="3c139-136">Wypróbuj te Wariacje w wierszu polecenia, aby zobaczyć różne wyniki:</span><span class="sxs-lookup"><span data-stu-id="3c139-136">Try these variations at the command line to see different results:</span></span>

```dotnetcli
dotnet run
dotnet run -- "Hello from the bot"
dotnet run -- Hello from the bot
```

<span data-ttu-id="3c139-137">Wszystkie argumenty po `--` ograniczniku są przesyłane do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3c139-137">All arguments after the `--` delimiter are passed to your application.</span></span>

## <a name="package-the-tool"></a><span data-ttu-id="3c139-138">Pakowanie narzędzia</span><span class="sxs-lookup"><span data-stu-id="3c139-138">Package the tool</span></span>

<span data-ttu-id="3c139-139">Przed spakowaniem i dystrybucją aplikacji jako narzędzia należy zmodyfikować plik projektu.</span><span class="sxs-lookup"><span data-stu-id="3c139-139">Before you can pack and distribute the application as a tool, you need to modify the project file.</span></span>

1. <span data-ttu-id="3c139-140">Otwórz plik *Microsoft. botsay. csproj* i Dodaj trzy nowe węzły XML na końcu `<PropertyGroup>` węzła:</span><span class="sxs-lookup"><span data-stu-id="3c139-140">Open the *microsoft.botsay.csproj* file and add three new XML nodes to the end of the `<PropertyGroup>` node:</span></span>

   ```xml
   <PackAsTool>true</PackAsTool>
   <ToolCommandName>botsay</ToolCommandName>
   <PackageOutputPath>./nupkg</PackageOutputPath>
   ```

   <span data-ttu-id="3c139-141">`<ToolCommandName>` to opcjonalny element określający polecenie, które spowoduje wywołanie narzędzia po jego zainstalowaniu.</span><span class="sxs-lookup"><span data-stu-id="3c139-141">`<ToolCommandName>` is an optional element that specifies the command that will invoke the tool after it's installed.</span></span> <span data-ttu-id="3c139-142">Jeśli ten element nie zostanie podany, nazwa polecenia dla narzędzia jest nazwą pliku projektu bez rozszerzenia *. csproj* .</span><span class="sxs-lookup"><span data-stu-id="3c139-142">If this element isn't provided, the command name for the tool is the project file name without the *.csproj* extension.</span></span>

   <span data-ttu-id="3c139-143">`<PackageOutputPath>` to opcjonalny element określający, gdzie zostanie utworzony pakiet NuGet.</span><span class="sxs-lookup"><span data-stu-id="3c139-143">`<PackageOutputPath>` is an optional element that determines where the NuGet package will be produced.</span></span> <span data-ttu-id="3c139-144">Pakiet NuGet jest używany przez interfejs wiersza polecenia platformy .NET do instalowania narzędzia.</span><span class="sxs-lookup"><span data-stu-id="3c139-144">The NuGet package is what the .NET CLI uses to install your tool.</span></span>

   <span data-ttu-id="3c139-145">Plik projektu wygląda teraz tak, jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="3c139-145">The project file now looks like the following example:</span></span>

   ```xml
   <Project Sdk="Microsoft.NET.Sdk">
  
     <PropertyGroup>

       <OutputType>Exe</OutputType>
       <TargetFramework>net5.0</TargetFramework>
  
       <PackAsTool>true</PackAsTool>
       <ToolCommandName>botsay</ToolCommandName>
       <PackageOutputPath>./nupkg</PackageOutputPath>
  
     </PropertyGroup>

   </Project>
   ```

1. <span data-ttu-id="3c139-146">Utwórz pakiet NuGet, uruchamiając polecenie [dotnet Pack](dotnet-pack.md) :</span><span class="sxs-lookup"><span data-stu-id="3c139-146">Create a NuGet package by running the [dotnet pack](dotnet-pack.md) command:</span></span>

   ```dotnetcli
   dotnet pack
   ```

   <span data-ttu-id="3c139-147">Plik *Microsoft. botsay. 1.0.0. nupkg* jest tworzony w folderze identyfikowanym przez `<PackageOutputPath>` wartość z pliku *Microsoft. botsay. csproj* , który w tym przykładzie jest folderem *./nupkg* .</span><span class="sxs-lookup"><span data-stu-id="3c139-147">The *microsoft.botsay.1.0.0.nupkg* file is created in the folder identified by the `<PackageOutputPath>` value from the *microsoft.botsay.csproj* file, which in this example is the *./nupkg* folder.</span></span>
  
   <span data-ttu-id="3c139-148">Po udostępnieniu narzędzia publicznie można przekazać je do programu `https://www.nuget.org` .</span><span class="sxs-lookup"><span data-stu-id="3c139-148">When you want to release a tool publicly, you can upload it to `https://www.nuget.org`.</span></span> <span data-ttu-id="3c139-149">Po udostępnieniu narzędzia w narzędziu NuGet deweloperzy mogą zainstalować narzędzie za pomocą polecenia [Install narzędzia dotnet](dotnet-tool-install.md) .</span><span class="sxs-lookup"><span data-stu-id="3c139-149">Once the tool is available on NuGet, developers can install the tool by using the [dotnet tool install](dotnet-tool-install.md) command.</span></span> <span data-ttu-id="3c139-150">Na potrzeby tego samouczka zainstalujesz pakiet bezpośrednio z lokalnego folderu *NUPKG* , więc nie ma potrzeby przekazywania pakietu do narzędzia NuGet.</span><span class="sxs-lookup"><span data-stu-id="3c139-150">For this tutorial you install the package directly from the local *nupkg* folder, so there's no need to upload the package to NuGet.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="3c139-151">Rozwiąż problemy</span><span class="sxs-lookup"><span data-stu-id="3c139-151">Troubleshoot</span></span>

<span data-ttu-id="3c139-152">Jeśli podczas wykonywania samouczka zostanie wyświetlony komunikat o błędzie, zobacz [Rozwiązywanie problemów z użyciem narzędzia platformy .NET](troubleshoot-usage-issues.md).</span><span class="sxs-lookup"><span data-stu-id="3c139-152">If you get an error message while following the tutorial, see [Troubleshoot .NET tool usage issues](troubleshoot-usage-issues.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c139-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3c139-153">Next steps</span></span>

<span data-ttu-id="3c139-154">W tym samouczku utworzysz aplikację konsolową i spakowano ją jako narzędzie.</span><span class="sxs-lookup"><span data-stu-id="3c139-154">In this tutorial, you created a console application and packaged it as a tool.</span></span> <span data-ttu-id="3c139-155">Aby dowiedzieć się, jak używać narzędzia jako narzędzia globalnego, przejdź do następnego samouczka.</span><span class="sxs-lookup"><span data-stu-id="3c139-155">To learn how to use the tool as a global tool, advance to the next tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3c139-156">Instalowanie i używanie narzędzia globalnego</span><span class="sxs-lookup"><span data-stu-id="3c139-156">Install and use a global tool</span></span>](global-tools-how-to-use.md)

<span data-ttu-id="3c139-157">Jeśli wolisz, możesz pominąć samouczek dotyczący narzędzi globalnych i przejść bezpośrednio do samouczka dotyczącego narzędzi lokalnych.</span><span class="sxs-lookup"><span data-stu-id="3c139-157">If you prefer, you can skip the global tools tutorial and go directly to the local tools tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3c139-158">Instalowanie i używanie narzędzia lokalnego</span><span class="sxs-lookup"><span data-stu-id="3c139-158">Install and use a local tool</span></span>](local-tools-how-to-use.md)
