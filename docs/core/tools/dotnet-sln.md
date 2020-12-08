---
title: dotnet sln — polecenie
description: Polecenie dotnet-sln udostępnia wygodną opcję dodawania, usuwania i wyświetlania listy projektów w pliku rozwiązania.
ms.date: 12/07/2020
ms.openlocfilehash: 480634550f6fa1983bb46f51b439dc8a686ead3c
ms.sourcegitcommit: 45c7148f2483db2501c1aa696ab6ed2ed8cb71b2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/08/2020
ms.locfileid: "96851704"
---
# <a name="dotnet-sln"></a><span data-ttu-id="f1eac-103">dotnet sln</span><span class="sxs-lookup"><span data-stu-id="f1eac-103">dotnet sln</span></span>

<span data-ttu-id="f1eac-104">**Ten artykuł ma zastosowanie do:** ✔️ .NET Core 2. x SDK i nowszych wersji</span><span class="sxs-lookup"><span data-stu-id="f1eac-104">**This article applies to:** ✔️ .NET Core 2.x SDK and later versions</span></span>

## <a name="name"></a><span data-ttu-id="f1eac-105">Nazwa</span><span class="sxs-lookup"><span data-stu-id="f1eac-105">Name</span></span>

<span data-ttu-id="f1eac-106">`dotnet sln` -Wyświetla lub modyfikuje projekty w pliku rozwiązania platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="f1eac-106">`dotnet sln` - Lists or modifies the projects in a .NET solution file.</span></span>

## <a name="synopsis"></a><span data-ttu-id="f1eac-107">Streszczenie</span><span class="sxs-lookup"><span data-stu-id="f1eac-107">Synopsis</span></span>

```dotnetcli
dotnet sln [<SOLUTION_FILE>] [command]

dotnet sln [command] -h|--help
```

## <a name="description"></a><span data-ttu-id="f1eac-108">Opis</span><span class="sxs-lookup"><span data-stu-id="f1eac-108">Description</span></span>

<span data-ttu-id="f1eac-109">`dotnet sln`Polecenie zapewnia wygodny sposób wyświetlania i modyfikowania projektów w pliku rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f1eac-109">The `dotnet sln` command provides a convenient way to list and modify projects in a solution file.</span></span>

<span data-ttu-id="f1eac-110">Aby użyć `dotnet sln` polecenia, plik rozwiązania musi już istnieć.</span><span class="sxs-lookup"><span data-stu-id="f1eac-110">To use the `dotnet sln` command, the solution file must already exist.</span></span> <span data-ttu-id="f1eac-111">Jeśli trzeba ją utworzyć, użyj polecenia [dotnet New](dotnet-new.md) , jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="f1eac-111">If you need to create one, use the [dotnet new](dotnet-new.md) command, as in the following example:</span></span>

```dotnetcli
dotnet new sln
```

## <a name="arguments"></a><span data-ttu-id="f1eac-112">Argumenty</span><span class="sxs-lookup"><span data-stu-id="f1eac-112">Arguments</span></span>

- **`SOLUTION_FILE`**

  <span data-ttu-id="f1eac-113">Plik rozwiązania, który ma być używany.</span><span class="sxs-lookup"><span data-stu-id="f1eac-113">The solution file to use.</span></span> <span data-ttu-id="f1eac-114">Jeśli ten argument zostanie pominięty, polecenie przeszukuje bieżący katalog.</span><span class="sxs-lookup"><span data-stu-id="f1eac-114">If this argument is omitted, the command searches the current directory for one.</span></span> <span data-ttu-id="f1eac-115">Jeśli nie zostanie znaleziony żaden plik rozwiązania lub wiele plików rozwiązania, polecenie nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="f1eac-115">If it finds no solution file or multiple solution files, the command fails.</span></span>

## <a name="options"></a><span data-ttu-id="f1eac-116">Opcje</span><span class="sxs-lookup"><span data-stu-id="f1eac-116">Options</span></span>

- **`-h|--help`**

  <span data-ttu-id="f1eac-117">Drukuje opis sposobu użycia polecenia.</span><span class="sxs-lookup"><span data-stu-id="f1eac-117">Prints out a description of how to use the command.</span></span>

## <a name="commands"></a><span data-ttu-id="f1eac-118">Polecenia</span><span class="sxs-lookup"><span data-stu-id="f1eac-118">Commands</span></span>

### `list`

<span data-ttu-id="f1eac-119">Wyświetla wszystkie projekty w pliku rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f1eac-119">Lists all projects in a solution file.</span></span>

#### <a name="synopsis"></a><span data-ttu-id="f1eac-120">Streszczenie</span><span class="sxs-lookup"><span data-stu-id="f1eac-120">Synopsis</span></span>

```dotnetcli
dotnet sln list [-h|--help]
```

#### <a name="arguments"></a><span data-ttu-id="f1eac-121">Argumenty</span><span class="sxs-lookup"><span data-stu-id="f1eac-121">Arguments</span></span>

- **`SOLUTION_FILE`**

  <span data-ttu-id="f1eac-122">Plik rozwiązania, który ma być używany.</span><span class="sxs-lookup"><span data-stu-id="f1eac-122">The solution file to use.</span></span> <span data-ttu-id="f1eac-123">Jeśli ten argument zostanie pominięty, polecenie przeszukuje bieżący katalog.</span><span class="sxs-lookup"><span data-stu-id="f1eac-123">If this argument is omitted, the command searches the current directory for one.</span></span> <span data-ttu-id="f1eac-124">Jeśli nie zostanie znaleziony żaden plik rozwiązania lub wiele plików rozwiązania, polecenie nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="f1eac-124">If it finds no solution file or multiple solution files, the command fails.</span></span>

#### <a name="options"></a><span data-ttu-id="f1eac-125">Opcje</span><span class="sxs-lookup"><span data-stu-id="f1eac-125">Options</span></span>

- **`-h|--help`**

  <span data-ttu-id="f1eac-126">Drukuje opis sposobu użycia polecenia.</span><span class="sxs-lookup"><span data-stu-id="f1eac-126">Prints out a description of how to use the command.</span></span>
  
### `add`

<span data-ttu-id="f1eac-127">Dodaje jeden lub więcej projektów do pliku rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f1eac-127">Adds one or more projects to the solution file.</span></span>

#### <a name="synopsis"></a><span data-ttu-id="f1eac-128">Streszczenie</span><span class="sxs-lookup"><span data-stu-id="f1eac-128">Synopsis</span></span>

```dotnetcli
dotnet sln [<SOLUTION_FILE>] add [--in-root] [-s|--solution-folder <PATH>] <PROJECT_PATH> [<PROJECT_PATH>...]
dotnet sln add [-h|--help]
```

#### <a name="arguments"></a><span data-ttu-id="f1eac-129">Argumenty</span><span class="sxs-lookup"><span data-stu-id="f1eac-129">Arguments</span></span>

- **`SOLUTION_FILE`**

  <span data-ttu-id="f1eac-130">Plik rozwiązania, który ma być używany.</span><span class="sxs-lookup"><span data-stu-id="f1eac-130">The solution file to use.</span></span> <span data-ttu-id="f1eac-131">Jeśli nie jest określony, polecenie przeszukuje bieżący katalog dla jednego i kończy się niepowodzeniem, jeśli istnieje wiele plików rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f1eac-131">If it is unspecified, the command searches the current directory for one and fails if there are multiple solution files.</span></span>

- **`PROJECT_PATH`**

  <span data-ttu-id="f1eac-132">Ścieżka do projektu lub projektów, które mają zostać dodane do rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f1eac-132">The path to the project or projects to add to the solution.</span></span> <span data-ttu-id="f1eac-133">Rozszerzenia [wzorca obsługi symboli wieloznacznych](https://en.wikipedia.org/wiki/Glob_(programming)) powłoki systemu UNIX/Linux są przetwarzane prawidłowo przez `dotnet sln` polecenie.</span><span class="sxs-lookup"><span data-stu-id="f1eac-133">Unix/Linux shell [globbing pattern](https://en.wikipedia.org/wiki/Glob_(programming)) expansions are processed correctly by the `dotnet sln` command.</span></span>

#### <a name="options"></a><span data-ttu-id="f1eac-134">Opcje</span><span class="sxs-lookup"><span data-stu-id="f1eac-134">Options</span></span>

- **`-h|--help`**

  <span data-ttu-id="f1eac-135">Drukuje opis sposobu użycia polecenia.</span><span class="sxs-lookup"><span data-stu-id="f1eac-135">Prints out a description of how to use the command.</span></span>

- **`--in-root`**

  <span data-ttu-id="f1eac-136">Umieszcza projekty w katalogu głównym rozwiązania zamiast tworzenia folderu rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f1eac-136">Places the projects in the root of the solution, rather than creating a solution folder.</span></span> <span data-ttu-id="f1eac-137">Dostępne od wersji .NET Core 3,0 SDK.</span><span class="sxs-lookup"><span data-stu-id="f1eac-137">Available since .NET Core 3.0 SDK.</span></span>

- **`-s|--solution-folder <PATH>`**

  <span data-ttu-id="f1eac-138">Ścieżka folderu rozwiązania docelowego, do którego mają zostać dodane projekty.</span><span class="sxs-lookup"><span data-stu-id="f1eac-138">The destination solution folder path to add the projects to.</span></span> <span data-ttu-id="f1eac-139">Dostępne od wersji .NET Core 3,0 SDK.</span><span class="sxs-lookup"><span data-stu-id="f1eac-139">Available since .NET Core 3.0 SDK.</span></span>

### `remove`

<span data-ttu-id="f1eac-140">Usuwa projekt lub wiele projektów z pliku rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f1eac-140">Removes a project or multiple projects from the solution file.</span></span>

#### <a name="synopsis"></a><span data-ttu-id="f1eac-141">Streszczenie</span><span class="sxs-lookup"><span data-stu-id="f1eac-141">Synopsis</span></span>

```dotnetcli
dotnet sln [<SOLUTION_FILE>] remove <PROJECT_PATH> [<PROJECT_PATH>...]
dotnet sln [<SOLUTION_FILE>] remove [-h|--help]
```

#### <a name="arguments"></a><span data-ttu-id="f1eac-142">Argumenty</span><span class="sxs-lookup"><span data-stu-id="f1eac-142">Arguments</span></span>

- **`SOLUTION_FILE`**

  <span data-ttu-id="f1eac-143">Plik rozwiązania, który ma być używany.</span><span class="sxs-lookup"><span data-stu-id="f1eac-143">The solution file to use.</span></span> <span data-ttu-id="f1eac-144">Jeśli pozostanie nieokreślony, polecenie przeszukuje bieżący katalog dla jednego i kończy się niepowodzeniem, jeśli istnieje wiele plików rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f1eac-144">If is left unspecified, the command searches the current directory for one and fails if there are multiple solution files.</span></span>

- **`PROJECT_PATH`**

  <span data-ttu-id="f1eac-145">Ścieżka do projektu lub projektów, które mają zostać dodane do rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f1eac-145">The path to the project or projects to add to the solution.</span></span> <span data-ttu-id="f1eac-146">Rozszerzenia [wzorca obsługi symboli wieloznacznych](https://en.wikipedia.org/wiki/Glob_(programming)) powłoki systemu UNIX/Linux są przetwarzane prawidłowo przez `dotnet sln` polecenie.</span><span class="sxs-lookup"><span data-stu-id="f1eac-146">Unix/Linux shell [globbing pattern](https://en.wikipedia.org/wiki/Glob_(programming)) expansions are processed correctly by the `dotnet sln` command.</span></span>

#### <a name="options"></a><span data-ttu-id="f1eac-147">Opcje</span><span class="sxs-lookup"><span data-stu-id="f1eac-147">Options</span></span>

- **`-h|--help`**

  <span data-ttu-id="f1eac-148">Drukuje opis sposobu użycia polecenia.</span><span class="sxs-lookup"><span data-stu-id="f1eac-148">Prints out a description of how to use the command.</span></span>

## <a name="examples"></a><span data-ttu-id="f1eac-149">Przykłady</span><span class="sxs-lookup"><span data-stu-id="f1eac-149">Examples</span></span>

- <span data-ttu-id="f1eac-150">Utwórz listę projektów w rozwiązaniu:</span><span class="sxs-lookup"><span data-stu-id="f1eac-150">List the projects in a solution:</span></span>

  ```dotnetcli
  dotnet sln todo.sln list
  ```

- <span data-ttu-id="f1eac-151">Dodaj projekt C# do rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="f1eac-151">Add a C# project to a solution:</span></span>

  ```dotnetcli
  dotnet sln add todo-app/todo-app.csproj
  ```

- <span data-ttu-id="f1eac-152">Usuń projekt C# z rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="f1eac-152">Remove a C# project from a solution:</span></span>

  ```dotnetcli
  dotnet sln remove todo-app/todo-app.csproj
  ```

- <span data-ttu-id="f1eac-153">Dodaj wiele projektów C# do katalogu głównego rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="f1eac-153">Add multiple C# projects to the root of a solution:</span></span>

  ```dotnetcli
  dotnet sln todo.sln add todo-app/todo-app.csproj back-end/back-end.csproj --in-root
  ```

- <span data-ttu-id="f1eac-154">Dodaj wiele projektów C# do rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="f1eac-154">Add multiple C# projects to a solution:</span></span>

  ```dotnetcli
  dotnet sln todo.sln add todo-app/todo-app.csproj back-end/back-end.csproj
  ```

- <span data-ttu-id="f1eac-155">Usuń wiele projektów C# z rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="f1eac-155">Remove multiple C# projects from a solution:</span></span>

  ```dotnetcli
  dotnet sln todo.sln remove todo-app/todo-app.csproj back-end/back-end.csproj
  ```

- <span data-ttu-id="f1eac-156">Dodawanie wielu projektów C# do rozwiązania przy użyciu wzorca obsługi symboli wieloznacznych (tylko w systemie UNIX/Linux):</span><span class="sxs-lookup"><span data-stu-id="f1eac-156">Add multiple C# projects to a solution using a globbing pattern (Unix/Linux only):</span></span>

  ```dotnetcli
  dotnet sln todo.sln add **/*.csproj
  ```

- <span data-ttu-id="f1eac-157">Dodawanie wielu projektów C# do rozwiązania przy użyciu wzorca obsługi symboli wieloznacznych (tylko program Windows PowerShell):</span><span class="sxs-lookup"><span data-stu-id="f1eac-157">Add multiple C# projects to a solution using a globbing pattern (Windows PowerShell only):</span></span>

  ```dotnetcli
  dotnet sln todo.sln add (ls -r **/*.csproj)
  ```

- <span data-ttu-id="f1eac-158">Usuwanie wielu projektów C# z rozwiązania przy użyciu wzorca obsługi symboli wieloznacznych (tylko w systemie UNIX/Linux):</span><span class="sxs-lookup"><span data-stu-id="f1eac-158">Remove multiple C# projects from a solution using a globbing pattern (Unix/Linux only):</span></span>

  ```dotnetcli
  dotnet sln todo.sln remove **/*.csproj
  ```

- <span data-ttu-id="f1eac-159">Usuwanie wielu projektów C# z rozwiązania przy użyciu wzorca obsługi symboli wieloznacznych (tylko program Windows PowerShell):</span><span class="sxs-lookup"><span data-stu-id="f1eac-159">Remove multiple C# projects from a solution using a globbing pattern (Windows PowerShell only):</span></span>

  ```dotnetcli
  dotnet sln todo.sln remove (ls -r **/*.csproj)
  ```

- <span data-ttu-id="f1eac-160">Tworzenie rozwiązania, aplikacji konsolowej i dwóch bibliotek klas.</span><span class="sxs-lookup"><span data-stu-id="f1eac-160">Create a solution, a console app, and two class libraries.</span></span> <span data-ttu-id="f1eac-161">Dodaj projekty do rozwiązania i Użyj `--solution-folder` opcji, `dotnet sln` Aby zorganizować biblioteki klas w folderze rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f1eac-161">Add the projects to the solution, and use the `--solution-folder` option of `dotnet sln` to organize the class libraries into a solution folder.</span></span>

  ```dotnetcli
  dotnet new sln -n mysolution
  dotnet new console -o myapp
  dotnet new classlib -o mylib1
  dotnet new classlib -o mylib2
  dotnet sln mysolution.sln add myapp\myapp.csproj
  dotnet sln mysolution.sln add mylib1\mylib1.csproj --solution-folder mylibs
  dotnet sln mysolution.sln add mylib2\mylib2.csproj --solution-folder mylibs
  ```

  <span data-ttu-id="f1eac-162">Poniższy zrzut ekranu przedstawia wynik w programie Visual Studio 2019 **Eksplorator rozwiązań**:</span><span class="sxs-lookup"><span data-stu-id="f1eac-162">The following screenshot shows the result in Visual Studio 2019 **Solution Explorer**:</span></span>

  :::image type="content" source="media/dotnet-sln/dotnet-sln-solution-folder.png" alt-text="Eksplorator rozwiązań pokazujący projekty biblioteki klas pogrupowane w folderze rozwiązania.":::
