---
title: Tworzenie biblioteki klas .NET przy użyciu Visual Studio Code
description: Dowiedz się, jak utworzyć bibliotekę klas .NET przy użyciu Visual Studio Code.
ms.date: 11/18/2020
ms.openlocfilehash: 4473163b76060623b364d7dabf7366c3575e3dcd
ms.sourcegitcommit: 9d525bb8109216ca1dc9e39c149d4902f4b43da5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2020
ms.locfileid: "96599502"
---
# <a name="tutorial-create-a-net-class-library-using-visual-studio-code"></a>Samouczek: Tworzenie biblioteki klas .NET przy użyciu Visual Studio Code

W tym samouczku utworzysz prostą bibliotekę narzędzi, która zawiera pojedynczą metodę obsługi ciągów.

*Biblioteka klas* definiuje typy i metody, które są wywoływane przez aplikację. Jeśli biblioteka jest przeznaczona .NET Standard 2,0, może być wywoływana przez dowolną implementację platformy .NET (w tym .NET Framework), która obsługuje .NET Standard 2,0. Jeśli biblioteka jest przeznaczona dla platformy .NET 5, może być wywoływana przez dowolną aplikację, która jest przeznaczona dla platformy .NET 5. W tym samouczku przedstawiono sposób ukierunkowania platformy .NET 5.

Podczas tworzenia biblioteki klas można ją rozpowszechnić jako składnik innej firmy lub jako składnik pakietu z jedną lub wieloma aplikacjami.

## <a name="prerequisites"></a>Wymagania wstępne

1. [Visual Studio Code](https://code.visualstudio.com/) z zainstalowanym [rozszerzeniem języka C#](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp) . Aby uzyskać informacje na temat sposobu instalowania rozszerzeń na Visual Studio Code, zobacz [vs Code rozszerzenia Marketplace](https://code.visualstudio.com/docs/editor/extension-gallery).
2. [Zestaw .net 5,0 SDK lub nowszy](https://dotnet.microsoft.com/download)

## <a name="create-a-solution"></a>Tworzenie rozwiązania

Zacznij od utworzenia pustego rozwiązania, aby umieścić projekt biblioteki klas w. Rozwiązanie służy jako kontener dla jednego lub wielu projektów. Dodasz kolejne powiązane projekty do tego samego rozwiązania.

1. Uruchom program Visual Studio Code.

1. Wybierz pozycję **plik**  >  **Otwórz folder** (**Otwórz...** na macOS) z menu głównego

1. W oknie dialogowym **Otwieranie folderu** Utwórz folder *ClassLibraryProjects* , a następnie kliknij pozycję **Wybierz folder** (**Otwórz** w macOS).

1. Otwórz **Terminal** w Visual Studio Code, wybierając pozycję **Wyświetl**  >  **Terminal** z menu głównego.

   Zostanie otwarty **Terminal** z wierszem polecenia w folderze *ClassLibraryProjects* .

1. W **terminalu** wprowadź następujące polecenie:

   ```dotnetcli
   dotnet new sln
   ```

   Dane wyjściowe terminalu wyglądają podobnie jak w poniższym przykładzie:

   ```output
   The template "Solution File" was created successfully.
   ```

## <a name="create-a-class-library-project"></a>Tworzenie projektu biblioteki klas

Dodaj nowy projekt biblioteki klas .NET o nazwie "StringLibrary" do rozwiązania.

1. W terminalu uruchom następujące polecenie, aby utworzyć projekt biblioteki:

   ```dotnetcli
   dotnet new classlib -o StringLibrary
   ```

   `-o`Polecenie lub `--output` określa lokalizację, w której mają zostać umieszczone wygenerowane dane wyjściowe.

   Dane wyjściowe terminalu wyglądają podobnie jak w poniższym przykładzie:

   ```output
   The template "Class library" was created successfully.
   Processing post-creation actions...
   Running 'dotnet restore' on StringLibrary\StringLibrary.csproj...
     Determining projects to restore...
     Restored C:\Projects\ClassLibraryProjects\StringLibrary\StringLibrary.csproj (in 328 ms).
   Restore succeeded.
   ```

1. Uruchom następujące polecenie, aby dodać projekt biblioteki do rozwiązania:

   ```dotnetcli
   dotnet sln add StringLibrary/StringLibrary.csproj
   ```

   Dane wyjściowe terminalu wyglądają podobnie jak w poniższym przykładzie:

   ```output
   Project `StringLibrary\StringLibrary.csproj` added to the solution.
   ```

1. Upewnij się, że biblioteka jest przeznaczona dla platformy .NET 5. W **Eksploratorze** Otwórz *StringLibrary/StringLibrary. csproj*.

   `TargetFramework`Element pokazuje, że projekt jest przeznaczony dla programu .net 5,0.

   ```xml
   <Project Sdk="Microsoft.NET.Sdk">

     <PropertyGroup>
       <TargetFramework>net5.0</TargetFramework>
     </PropertyGroup>

   </Project>
   ```

1. Otwórz *Class1.cs* i Zastąp kod następującym kodem.

   :::code language="csharp" source="./snippets/library-with-visual-studio/csharp/StringLibrary/Class1.cs":::

   Biblioteka klas, `UtilityLibraries.StringLibrary` ,,, zawiera metodę o nazwie `StartsWithUpper` . Ta metoda zwraca <xref:System.Boolean> wartość wskazującą, czy bieżące wystąpienie ciągu zaczyna się od wielkiej litery. Standard Unicode rozróżnia wielkie litery od małych liter. <xref:System.Char.IsUpper(System.Char)?displayProperty=nameWithType>Metoda zwraca `true` czy znak jest pisany wielką literą.

1. Zapisz plik.

1. Uruchom następujące polecenie, aby skompilować rozwiązanie i sprawdzić, czy projekt kompiluje się bez błędu.

   ```dotnetcli
   dotnet build
   ```

   Dane wyjściowe terminalu wyglądają podobnie jak w poniższym przykładzie:

   ```output
   Microsoft (R) Build Engine version 16.7.0+b89cb5fde for .NET
   Copyright (C) Microsoft Corporation. All rights reserved.
     Determining projects to restore...
     All projects are up-to-date for restore.
     StringLibrary -> C:\Projects\ClassLibraryProjects\StringLibrary\bin\Debug\net5.0\StringLibrary.dll
   Build succeeded.
       0 Warning(s)
       0 Error(s)
   Time Elapsed 00:00:02.78
   ```

## <a name="add-a-console-app-to-the-solution"></a>Dodawanie aplikacji konsolowej do rozwiązania

Dodaj aplikację konsolową, która używa biblioteki klas. Aplikacja wyświetli monit o wprowadzenie ciągu i zgłoszenie, czy ciąg rozpoczyna się od wielkiej litery.

1. W terminalu uruchom następujące polecenie, aby utworzyć projekt aplikacji konsoli:

   ```dotnetcli
   dotnet new console -o ShowCase
   ```

   Dane wyjściowe terminalu wyglądają podobnie jak w poniższym przykładzie:

   ```output
   The template "Console Application" was created successfully.
   Processing post-creation actions...
   Running 'dotnet restore' on ShowCase\ShowCase.csproj...  
     Determining projects to restore...
     Restored C:\Projects\ClassLibraryProjects\ShowCase\ShowCase.csproj (in 210 ms).
   Restore succeeded.
   ```

1. Uruchom następujące polecenie, aby dodać projekt aplikacji konsolowej do rozwiązania:

   ```dotnetcli
   dotnet sln add ShowCase/ShowCase.csproj
   ```

   Dane wyjściowe terminalu wyglądają podobnie jak w poniższym przykładzie:

   ```output
   Project `ShowCase\ShowCase.csproj` added to the solution.
   ```

1. Otwórz *Pokaz/Program. cs* i Zastąp cały kod następującym kodem.

   :::code language="csharp" source="./snippets/library-with-visual-studio/csharp/ShowCase/Program.cs":::

   Kod używa `row` zmiennej do obsługi liczby wierszy danych zapisywana w oknie konsoli. Za każdym razem, gdy jest większy lub równy 25, kod czyści okno konsoli i wyświetla komunikat dla użytkownika.

   Program poprosi użytkownika o wprowadzenie ciągu. Wskazuje, czy ciąg rozpoczyna się od wielkiej litery. Jeśli użytkownik naciśnie klawisz <kbd>Enter</kbd> bez wprowadzania ciągu, aplikacja zostanie zakończona, a okno konsoli zostanie zamknięte.

1. Zapisz zmiany.

## <a name="add-a-project-reference"></a>Dodaj odwołanie do projektu

Początkowo nowy projekt aplikacji konsolowej nie ma dostępu do biblioteki klas. Aby zezwolić na wywoływanie metod w bibliotece klas, Utwórz odwołanie do projektu do projektu biblioteki klas.

1. Uruchom następujące polecenie:

   ```dotnetcli
   dotnet add ShowCase/ShowCase.csproj reference StringLibrary/StringLibrary.csproj
   ```

   Dane wyjściowe terminalu wyglądają podobnie jak w poniższym przykładzie:

   ```output
   Reference `..\StringLibrary\StringLibrary.csproj` added to the project.
   ```

## <a name="run-the-app"></a>Uruchamianie aplikacji

1. W terminalu uruchom następujące polecenie:

   ```dotnetcli
   dotnet run --project ShowCase/ShowCase.csproj
   ```

1. Wypróbuj program, wprowadzając ciągi i naciskając klawisz <kbd>Enter</kbd>, a następnie naciśnij klawisz <kbd>Enter</kbd> , aby wyjść.

   Dane wyjściowe terminalu wyglądają podobnie jak w poniższym przykładzie:

   ```output
   Press <Enter> only to exit; otherwise, enter a string and press <Enter>:

   A string that starts with an uppercase letter
   Input: A string that starts with an uppercase letter
   Begins with uppercase? : Yes

   a string that starts with a lowercase letter
   Input: a string that starts with a lowercase letter
   Begins with uppercase? : No
   ```

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Tworzenie bibliotek przy użyciu interfejsu wiersza polecenia platformy .NET](libraries.md)
* [Wersje .NET Standard i obsługiwane przez nich platformy](../../standard/net-standard.md).

## <a name="next-steps"></a>Następne kroki

W tym samouczku utworzono rozwiązanie, dodano projekt biblioteki i dodano projekt aplikacji konsolowej, który używa biblioteki. W następnym samouczku dodasz projekt testu jednostkowego do rozwiązania.

> [!div class="nextstepaction"]
> [Testowanie biblioteki klas .NET za pomocą platformy .NET przy użyciu Visual Studio Code](testing-library-with-visual-studio-code.md)
