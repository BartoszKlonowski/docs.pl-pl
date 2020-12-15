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
# <a name="tutorial-create-a-net-tool-using-the-net-cli"></a>Samouczek: Tworzenie narzędzia platformy .NET przy użyciu interfejsu wiersza polecenia platformy .NET

**Ten artykuł ma zastosowanie do:** ✔️ .net Core 2,1 SDK i nowszych wersjach

W tym samouczku przedstawiono sposób tworzenia i pakowania narzędzia platformy .NET. Interfejs wiersza polecenia platformy .NET umożliwia tworzenie aplikacji konsolowej jako narzędzia, które mogą być instalowane i uruchamiane przez inne osoby. Narzędzia .NET Tools są pakietami NuGet, które są instalowane z interfejsu wiersza polecenia platformy .NET. Aby uzyskać więcej informacji na temat narzędzi, zobacz temat [Narzędzia .NET — Omówienie](global-tools.md).

Tworzone narzędzie jest aplikacją konsolową, która przyjmuje komunikat jako dane wejściowe i wyświetla komunikat wraz z wierszami tekstu, które tworzą obraz robota.

Jest to pierwsza z serii trzech samouczków. Ten samouczek obejmuje tworzenie i pakowanie narzędzi. W następnych dwóch samouczkach [użyjesz narzędzia jako narzędzia globalnego](global-tools-how-to-use.md) i [Użyj tego narzędzia jako narzędzia lokalnego](local-tools-how-to-use.md). Procedury tworzenia narzędzia są takie same, niezależnie od tego, czy są używane jako narzędzie globalne, czy jako narzędzie lokalne.

## <a name="prerequisites"></a>Wymagania wstępne

- [Zestaw .NET SDK 5,0](https://dotnet.microsoft.com/download) lub nowsza wersja.

  W tym samouczku jest używany zestaw SDK programu .NET 5,0, ale narzędzia globalne są dostępne począwszy od zestaw .NET Core SDK 2,1. Narzędzia lokalne są dostępne począwszy od zestaw .NET Core SDK 3,0.
  
- Wybrany edytor tekstu lub edytor kodu.

## <a name="create-a-project"></a>Tworzenie projektu

1. Otwórz wiersz polecenia i Utwórz folder o nazwie *Repository*.

1. Przejdź do folderu *repozytorium* i wprowadź następujące polecenie:

   ```dotnetcli
   dotnet new console -n microsoft.botsay
   ```

   Polecenie tworzy nowy folder o nazwie *Microsoft. botsay* w folderze *repozytorium* .

1. Przejdź do folderu *Microsoft. botsay* .

   ```console
   cd microsoft.botsay
   ```

## <a name="add-the-code"></a>Dodawanie kodu

1. Otwórz `Program.cs` plik z edytorem kodu.

1. Dodaj następującą `using` dyrektywę na początku pliku:

   ```csharp
   using System.Reflection;
   ```

1. Zastąp `Main` metodę poniższym kodem, aby przetworzyć argumenty wiersza polecenia dla aplikacji.

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

   Jeśli nie przechodzą żadnych argumentów, zostanie wyświetlony krótki komunikat pomocy. W przeciwnym razie wszystkie argumenty są łączone w jeden ciąg i drukowane przez wywołanie `ShowBot` metody utworzonej w następnym kroku.

1. Dodaj nową metodę o nazwie `ShowBot` , która przyjmuje parametr ciągu. Metoda drukuje komunikat i obraz robota przy użyciu wierszy tekstu.

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

1. Zapisz zmiany.

## <a name="test-the-application"></a>Testowanie aplikacji

Uruchom projekt i zobacz dane wyjściowe. Wypróbuj te Wariacje w wierszu polecenia, aby zobaczyć różne wyniki:

```dotnetcli
dotnet run
dotnet run -- "Hello from the bot"
dotnet run -- Hello from the bot
```

Wszystkie argumenty po `--` ograniczniku są przesyłane do aplikacji.

## <a name="package-the-tool"></a>Pakowanie narzędzia

Przed spakowaniem i dystrybucją aplikacji jako narzędzia należy zmodyfikować plik projektu.

1. Otwórz plik *Microsoft. botsay. csproj* i Dodaj trzy nowe węzły XML na końcu `<PropertyGroup>` węzła:

   ```xml
   <PackAsTool>true</PackAsTool>
   <ToolCommandName>botsay</ToolCommandName>
   <PackageOutputPath>./nupkg</PackageOutputPath>
   ```

   `<ToolCommandName>` to opcjonalny element określający polecenie, które spowoduje wywołanie narzędzia po jego zainstalowaniu. Jeśli ten element nie zostanie podany, nazwa polecenia dla narzędzia jest nazwą pliku projektu bez rozszerzenia *. csproj* .

   `<PackageOutputPath>` to opcjonalny element określający, gdzie zostanie utworzony pakiet NuGet. Pakiet NuGet jest używany przez interfejs wiersza polecenia platformy .NET do instalowania narzędzia.

   Plik projektu wygląda teraz tak, jak w poniższym przykładzie:

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

1. Utwórz pakiet NuGet, uruchamiając polecenie [dotnet Pack](dotnet-pack.md) :

   ```dotnetcli
   dotnet pack
   ```

   Plik *Microsoft. botsay. 1.0.0. nupkg* jest tworzony w folderze identyfikowanym przez `<PackageOutputPath>` wartość z pliku *Microsoft. botsay. csproj* , który w tym przykładzie jest folderem *./nupkg* .
  
   Po udostępnieniu narzędzia publicznie można przekazać je do programu `https://www.nuget.org` . Po udostępnieniu narzędzia w narzędziu NuGet deweloperzy mogą zainstalować narzędzie za pomocą polecenia [Install narzędzia dotnet](dotnet-tool-install.md) . Na potrzeby tego samouczka zainstalujesz pakiet bezpośrednio z lokalnego folderu *NUPKG* , więc nie ma potrzeby przekazywania pakietu do narzędzia NuGet.

## <a name="troubleshoot"></a>Rozwiąż problemy

Jeśli podczas wykonywania samouczka zostanie wyświetlony komunikat o błędzie, zobacz [Rozwiązywanie problemów z użyciem narzędzia platformy .NET](troubleshoot-usage-issues.md).

## <a name="next-steps"></a>Następne kroki

W tym samouczku utworzysz aplikację konsolową i spakowano ją jako narzędzie. Aby dowiedzieć się, jak używać narzędzia jako narzędzia globalnego, przejdź do następnego samouczka.

> [!div class="nextstepaction"]
> [Instalowanie i używanie narzędzia globalnego](global-tools-how-to-use.md)

Jeśli wolisz, możesz pominąć samouczek dotyczący narzędzi globalnych i przejść bezpośrednio do samouczka dotyczącego narzędzi lokalnych.

> [!div class="nextstepaction"]
> [Instalowanie i używanie narzędzia lokalnego](local-tools-how-to-use.md)
