---
title: Utwórz szablon elementu dla nowego interfejs wiersza polecenia platformy .NET Core dotnet
description: Dowiedz się, jak utworzyć szablon elementu dla nowego polecenia dotnet. Szablony elementów mogą zawierać dowolną liczbę plików.
author: adegeo
ms.date: 06/25/2019
ms.topic: tutorial
ms.author: adegeo
ms.openlocfilehash: 0b804d26b2f33d4d600c17de2f7f71101a0f9c98
ms.sourcegitcommit: dc2feef0794cf41dbac1451a13b8183258566c0e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/24/2020
ms.locfileid: "85324369"
---
# <a name="tutorial-create-an-item-template"></a>Samouczek: Tworzenie szablonu elementu

Za pomocą platformy .NET Core można tworzyć i wdrażać szablony generujące projekty, pliki, nawet zasoby. Ten samouczek jest częścią jednej z serii, która uczy się, jak tworzyć, instalować i odinstalowywać szablony do użycia z `dotnet new` poleceniem.

W tej części serii dowiesz się, jak:

> [!div class="checklist"]
>
> * Tworzenie klasy dla szablonu elementu
> * Tworzenie folderu i pliku konfiguracji szablonu
> * Instalowanie szablonu ze ścieżki pliku
> * Testowanie szablonu elementu
> * Odinstaluj szablon elementu

## <a name="prerequisites"></a>Wymagania wstępne

* [Zestaw .NET Core 2,2 SDK](https://dotnet.microsoft.com/download) lub jego nowsze wersje.
* Przeczytaj artykuł referencyjny [Szablony niestandardowe dla usługi dotnet New](../tools/custom-templates.md).

  W artykule referencyjnym objaśniono podstawowe informacje dotyczące szablonów i sposobu ich umieszczania. Niektóre z tych informacji zostaną ponownie powtórzone w tym miejscu.

* Otwórz Terminal i przejdź do folderu _working\templates_ .

## <a name="create-the-required-folders"></a>Tworzenie wymaganych folderów

Ta seria używa "folderu roboczego", w którym znajduje się źródło szablonu, oraz "folderu testowego" używanego do testowania szablonów. Folder roboczy i folder testowania powinny znajdować się w tym samym folderze nadrzędnym.

Najpierw utwórz folder nadrzędny, a nazwa nie ma znaczenia. Następnie utwórz podfolder o nazwie _Work_. W folderze _roboczym_ utwórz podfolder o nazwie _templates_.

Następnie utwórz folder w folderze nadrzędnym o nazwie _test_. Struktura folderów powinna wyglądać następująco.

```console
parent_folder
├───test
└───working
    └───templates
```

## <a name="create-an-item-template"></a>Utwórz szablon elementu

Szablon elementu jest określonym typem szablonu, który zawiera jeden lub więcej plików. Te typy szablonów są przydatne, gdy chcesz wygenerować coś takiego jak konfiguracja, kod lub plik rozwiązania. W tym przykładzie utworzysz klasę, która dodaje metodę rozszerzenia do typu ciągu.

W terminalu przejdź do folderu _working\templates_ i Utwórz nowy podfolder o nazwie _extensionss_. Wprowadź folder.

```console
working
└───templates
    └───extensions
```

Utwórz nowy plik o nazwie _CommonExtensions.cs_ i otwórz go za pomocą ulubionego edytora tekstu. Ta klasa zapewni metodę rozszerzenia o nazwie `Reverse` , która odwraca zawartość ciągu. Wklej następujący kod i Zapisz plik:

```csharp
using System;

namespace System
{
    public static class StringExtensions
    {
        public static string Reverse(this string value)
        {
            var tempArray = value.ToCharArray();
            Array.Reverse(tempArray);
            return new string(tempArray);
        }
    }
}
```

Teraz, gdy masz już utworzoną zawartość szablonu, musisz utworzyć konfigurację szablonu w folderze głównym szablonu.

## <a name="create-the-template-config"></a>Utwórz konfigurację szablonu

Szablony są rozpoznawane w programie .NET Core za pomocą specjalnego folderu i pliku konfiguracji, który istnieje w katalogu głównym szablonu. W tym samouczku folder szablonu znajduje się w lokalizacji _working\templates\extensions_.

Podczas tworzenia szablonu wszystkie pliki i foldery znajdujące się w folderze szablonów są uwzględniane jako część szablonu, z wyjątkiem folderu specjalnej konfiguracji. Ten folder konfiguracji ma nazwę _.template.config_.

Najpierw utwórz nowy podfolder o nazwie _.template.config_, wprowadź go. Następnie utwórz nowy plik o nazwie _template.json_. Struktura folderów powinna wyglądać następująco:

```console
working
└───templates
    └───extensions
        └───.template.config
                template.json
```

Otwórz _template.jsw_ ulubionym edytorze tekstu i wklej go w poniższym kodzie JSON i Zapisz.

```json
{
  "$schema": "http://json.schemastore.org/template",
  "author": "Me",
  "classifications": [ "Common", "Code" ],
  "identity": "ExampleTemplate.StringExtensions",
  "name": "Example templates: string extensions",
  "shortName": "stringext",
  "tags": {
    "language": "C#",
    "type": "item"
  }
}
```

Ten plik konfiguracji zawiera wszystkie ustawienia szablonu. Można wyświetlić ustawienia podstawowe, takie jak `name` i `shortName` , ale istnieje również `tags/type` wartość, która jest ustawiona na `item` . Spowoduje to kategoryzację szablonu jako szablonu elementu. Nie ma ograniczeń dotyczących typu tworzonego szablonu. `item`Wartości i `project` są wspólnymi nazwami zalecanymi przez platformę .NET Core, dzięki czemu użytkownicy mogą łatwo filtrować typ szukanego szablonu.

`classifications`Element reprezentuje kolumnę **Tagi** , która pojawia się po uruchomieniu `dotnet new` i wyświetleniu listy szablonów. Użytkownicy mogą również wyszukiwać w oparciu o znaczniki klasyfikacji. Nie należy mylić `tags` właściwości w \* pliku JSON z `classifications` listą tagów. Te dwa różne rzeczy są uważane za podobne. Pełny schemat *template.jsw* pliku znajduje się w [magazynie schematów JSON](http://json.schemastore.org/template). Aby uzyskać więcej informacji na temat *template.jsw* pliku, zobacz stronę [typu "dotnet tworzenia szablonów wiki](https://github.com/dotnet/templating/wiki)".

Teraz, gdy masz prawidłowy _.template.config/template.jsdla_ pliku, szablon jest gotowy do zainstalowania. W terminalu przejdź do folderu _Extensions_ i uruchom następujące polecenie, aby zainstalować szablon znajdujący się w bieżącym folderze:

* **W systemie Windows**:`dotnet new -i .\`
* **W systemie Linux lub macOS**:`dotnet new -i ./`

To polecenie wyświetla listę zainstalowanych szablonów, które powinny obejmować użytkownika.

```console
C:\working\templates\extensions> dotnet new -i .\
Usage: new [options]

Options:
  -h, --help          Displays help for this command.
  -l, --list          Lists templates containing the specified name. If no name is specified, lists all templates.

... cut to save space ...

Templates                                         Short Name            Language          Tags
-------------------------------------------------------------------------------------------------------------------------------
Example templates: string extensions              stringext             [C#]              Common/Code
Console Application                               console               [C#], F#, VB      Common/Console
Class library                                     classlib              [C#], F#, VB      Common/Library
WPF Application                                   wpf                   [C#], VB          Common/WPF
Windows Forms (WinForms) Application              winforms              [C#], VB          Common/WinForms
Worker Service                                    worker                [C#]              Common/Worker/Web
```

## <a name="test-the-item-template"></a>Testowanie szablonu elementu

Teraz, gdy masz zainstalowany szablon elementu, przetestuj go. Przejdź do folderu _test/_ folder i Utwórz nową aplikację konsolową przy użyciu programu `dotnet new console` . Spowoduje to wygenerowanie projektu roboczego, który można łatwo przetestować przy użyciu `dotnet run` polecenia.

```dotnetcli
dotnet new console
```

Dane wyjściowe są podobne do poniższych.

```console
The template "Console Application" was created successfully.

Processing post-creation actions...
Running 'dotnet restore' on C:\test\test.csproj...
  Restore completed in 54.82 ms for C:\test\test.csproj.

Restore succeeded.
```

Uruchom projekt przy użyciu.

```dotnetcli
dotnet run
```

Otrzymujesz następujące dane wyjściowe.

```console
Hello World!
```

Następnie uruchom polecenie, `dotnet new stringext` Aby wygenerować _CommonExtensions.cs_ na podstawie szablonu.

```dotnetcli
dotnet new stringext
```

Otrzymujesz następujące dane wyjściowe.

```console
The template "Example templates: string extensions" was created successfully.
```

Zmień kod w _program.cs_ , aby odwrócić `"Hello World"` ciąg z użyciem metody rozszerzającej dostarczonej przez szablon.

```csharp
Console.WriteLine("Hello World!".Reverse());
```

Ponownie uruchom program i zobaczysz, że wynik jest odwrócony.

```dotnetcli
dotnet run
```

Otrzymujesz następujące dane wyjściowe.

```console
!dlroW olleH
```

Gratulacje! Utworzono i wdrożono szablon elementu z platformą .NET Core. W ramach przygotowania do następnej części tej serii samouczków należy odinstalować utworzony szablon. Pamiętaj, aby usunąć wszystkie pliki z folderu _testowego_ . Spowoduje to powrót do stanu czystego gotowego do następnej głównej sekcji tego samouczka.

## <a name="uninstall-the-template"></a>Odinstaluj szablon

Ponieważ szablon został zainstalowany według ścieżki pliku, należy go odinstalować z **bezwzględną** ścieżką pliku. Listę zainstalowanych szablonów można wyświetlić, uruchamiając `dotnet new -u` polecenie. Szablon powinien zostać wyświetlony jako ostatni. Użyj podanej ścieżki, aby odinstalować szablon przy użyciu `dotnet new -u <ABSOLUTE PATH TO TEMPLATE DIRECTORY>` polecenia.

```dotnetcli
dotnet new -u
```

Dane wyjściowe są podobne do poniższych.

```console
Template Instantiation Commands for .NET Core CLI

Currently installed items:
  Microsoft.DotNet.Common.ItemTemplates
    Templates:
      dotnet gitignore file (gitignore)
      global.json file (globaljson)
      NuGet Config (nugetconfig)
      Solution File (sln)
      Dotnet local tool manifest file (tool-manifest)
      Web Config (webconfig)

... cut to save space ...

  NUnit3.DotNetNew.Template
    Templates:
      NUnit 3 Test Project (nunit) C#
      NUnit 3 Test Item (nunit-test) C#
      NUnit 3 Test Project (nunit) F#
      NUnit 3 Test Item (nunit-test) F#
      NUnit 3 Test Project (nunit) VB
      NUnit 3 Test Item (nunit-test) VB
  C:\working\templates\extensions
    Templates:
      Example templates: string extensions (stringext) C#
```

Aby odinstalować szablon, uruchom następujące polecenie.

```dotnetcli
dotnet new -u C:\working\templates\extensions
```

## <a name="next-steps"></a>Następne kroki

W tym samouczku utworzono szablon elementu. Aby dowiedzieć się, jak utworzyć szablon projektu, Kontynuuj tę serię samouczków.

> [!div class="nextstepaction"]
> [Utwórz szablon projektu](cli-templates-create-project-template.md)
