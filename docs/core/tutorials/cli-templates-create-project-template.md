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
# <a name="tutorial-create-a-project-template"></a>Samouczek: Tworzenie szablonu projektu

Za pomocą platformy .NET można tworzyć i wdrażać szablony generujące projekty, pliki, nawet zasoby. Ten samouczek jest drugą częścią serii, która zawiera informacje na temat tworzenia, instalowania i odinstalowywania szablonów do użycia z `dotnet new` poleceniem.

W tej części serii dowiesz się, jak:

> [!div class="checklist"]
>
> * Tworzenie zasobów szablonu projektu
> * Tworzenie folderu i pliku konfiguracji szablonu
> * Instalowanie szablonu ze ścieżki pliku
> * Testowanie szablonu elementu
> * Odinstaluj szablon elementu

## <a name="prerequisites"></a>Wymagania wstępne

* Ukończ [część 1](cli-templates-create-item-template.md) tej serii samouczków.
* Otwórz Terminal i przejdź do folderu _working\templates_ .

## <a name="create-a-project-template"></a>Utwórz szablon projektu

Szablony projektów tworzą gotowe do uruchomienia projekty, które ułatwiają użytkownikom rozpoczęcie pracy z zestawem roboczym kodu. Platforma .NET zawiera kilka szablonów projektu, takich jak Aplikacja konsolowa lub Biblioteka klas. W tym przykładzie utworzysz nowy projekt konsoli, który umożliwia C# 9,0 i tworzy `async main` punkt wejścia.

W terminalu przejdź do folderu _working\templates_ i Utwórz nowy podfolder o nazwie _consoleasync_. Wprowadź podfolder i uruchom `dotnet new console` w celu wygenerowania standardowej aplikacji konsolowej. Będziesz edytować pliki utworzone przez ten szablon w celu utworzenia nowego szablonu.

```console
working
└───templates
    └───consoleasync
            consoleasync.csproj
            Program.cs
```

## <a name="modify-programcs"></a>Modyfikuj Program.cs

Otwórz plik _program.cs_ . Projekt konsoli nie używa asynchronicznego punktu wejścia, więc Dodajmy ten element. Zmień kod na następujący i Zapisz plik.

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

## <a name="modify-consoleasynccsproj"></a>Modyfikuj consoleasync. csproj

Zaktualizujmy wersję języka C# używaną przez projekt do wersji 9,0. Edytuj plik _consoleasync. csproj_ i Dodaj `<LangVersion>` ustawienie do `<PropertyGroup>` węzła.

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net5.0</TargetFramework>

    <LangVersion>9.0</LangVersion>

  </PropertyGroup>
  
</Project>
```

## <a name="build-the-project"></a>Kompilowanie projektu

Przed ukończeniem szablonu projektu należy go przetestować, aby upewnić się, że kompiluje i działa poprawnie.

W terminalu uruchom następujące polecenie.

```dotnetcli
dotnet run
```

Otrzymujesz następujące dane wyjściowe.

```console
Hello World with C# 9.0!
```

Można usunąć foldery _obj_ i _bin_ utworzone przy użyciu `dotnet run` . Usunięcie tych plików gwarantuje, że szablon zawiera tylko pliki powiązane z szablonem, a nie wszystkie pliki, które wynikają z akcji kompilacji.

Teraz, gdy masz już utworzoną zawartość szablonu, musisz utworzyć konfigurację szablonu w folderze głównym szablonu.

## <a name="create-the-template-config"></a>Utwórz konfigurację szablonu

Szablony są rozpoznawane w programie .NET według specjalnego folderu i pliku konfiguracji, który istnieje w katalogu głównym szablonu. W tym samouczku folder szablonu znajduje się w lokalizacji _working\templates\consoleasync_.

Podczas tworzenia szablonu wszystkie pliki i foldery znajdujące się w folderze szablonów są uwzględniane jako część szablonu, z wyjątkiem folderu specjalnej konfiguracji. Ten folder konfiguracji ma nazwę _.template.config_.

Najpierw utwórz nowy podfolder o nazwie _.template.config_, wprowadź go. Następnie utwórz nowy plik o nazwie _template.json_. Struktura folderów powinna wyglądać następująco.

```console
working
└───templates
    └───consoleasync
        └───.template.config
                template.json
```

Otwórz _template.jsw_ ulubionym edytorze tekstu i wklej go w poniższym kodzie JSON i Zapisz.

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

Ten plik konfiguracji zawiera wszystkie ustawienia szablonu. Można zobaczyć ustawienia podstawowe, takie jak `name` i, `shortName` ale również `tags/type` wartość, która jest ustawiona na `project` . Spowoduje to wyznaczenie szablonu jako szablonu projektu. Nie ma ograniczeń dotyczących typu tworzonego szablonu. `item`Wartości i `project` są wspólnymi nazwami zalecanymi przez platformę .NET, aby umożliwić użytkownikom łatwe filtrowanie typu szukanego szablonu.

`classifications`Element reprezentuje kolumnę **Tagi** , która pojawia się po uruchomieniu `dotnet new` i wyświetleniu listy szablonów. Użytkownicy mogą również wyszukiwać w oparciu o znaczniki klasyfikacji. Nie należy mylić `tags` właściwości w pliku JSON z `classifications` listą tagów. Te dwa różne rzeczy są uważane za podobne. Pełny schemat *template.jsw* pliku znajduje się w [magazynie schematów JSON](http://json.schemastore.org/template). Aby uzyskać więcej informacji na temat *template.jsw* pliku, zobacz stronę [typu "dotnet tworzenia szablonów wiki](https://github.com/dotnet/templating/wiki)".

Teraz, gdy masz prawidłowy _.template.config/template.jsdla_ pliku, szablon jest gotowy do zainstalowania. Przed zainstalowaniem szablonu upewnij się, że usunięto wszystkie foldery i pliki dodatkowe pliki, które nie mają być dołączone do szablonu, takie jak foldery _bin_ lub _obj_ . W terminalu przejdź do folderu _consoleasync_ i uruchom polecenie, `dotnet new -i .\` Aby zainstalować szablon znajdujący się w bieżącym folderze. Jeśli używasz systemu operacyjnego Linux lub macOS, użyj ukośnika: `dotnet new -i ./` .

To polecenie wyświetla listę zainstalowanych szablonów, które powinny obejmować użytkownika.

```dotnetcli
dotnet new -i .\
```

Dane wyjściowe są podobne do poniższych.

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

### <a name="test-the-project-template"></a>Testowanie szablonu projektu

Teraz, gdy masz zainstalowany szablon projektu, przetestuj go.

1. Przejdź do folderu _testowego_

1. Utwórz nową aplikację konsolową przy użyciu następującego polecenia, które generuje projekt roboczy, który można łatwo przetestować przy użyciu `dotnet run` polecenia.

    ```dotnetcli
    dotnet new consoleasync
    ```

    Otrzymujesz następujące dane wyjściowe.

    ```console
    The template "Example templates: async project" was created successfully.
    ```

1. Uruchom projekt przy użyciu następującego polecenia.

    ```dotnetcli
    dotnet run
    ```

    Otrzymujesz następujące dane wyjściowe.

    ```console
    Hello World with C# 9.0!
    ```

Gratulacje! Szablon projektu został utworzony i wdrożony przy użyciu platformy .NET. W ramach przygotowania do następnej części tej serii samouczków należy odinstalować utworzony szablon. Pamiętaj, aby usunąć wszystkie pliki z folderu _testowego_ . Spowoduje to powrót do stanu czystego gotowego do następnej głównej sekcji tego samouczka.

### <a name="uninstall-the-template"></a>Odinstaluj szablon

Ponieważ szablon został zainstalowany przy użyciu ścieżki pliku, należy go odinstalować z **bezwzględną** ścieżką pliku. Listę zainstalowanych szablonów można wyświetlić, uruchamiając `dotnet new -u` polecenie. Szablon powinien zostać wyświetlony jako ostatni. Użyj `Uninstall Command` listy, aby odinstalować szablon.

```dotnetcli
dotnet new -u
```

Dane wyjściowe są podobne do poniższych.

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

Aby odinstalować utworzony szablon, uruchom polecenie `Uninstall Command` , które jest wyświetlane w danych wyjściowych.

```dotnetcli
dotnet new -u C:\working\templates\consoleasync
```

## <a name="next-steps"></a>Następne kroki

W tym samouczku utworzono szablon projektu. Aby dowiedzieć się, jak spakować szablon elementu i projektu do łatwego w użyciu pliku, Kontynuuj tę serię samouczków.

> [!div class="nextstepaction"]
> [Tworzenie pakietu szablonów](cli-templates-create-template-pack.md)
