---
title: Informacje o F# Interactive (dotnet)
description: 'Dowiedz się, jak F# Interactive (dotnet FSI) służy do interaktywnego uruchamiania kodu F # za pomocą konsoli programu lub wykonywania skryptów języka F #.'
ms.date: 10/31/2020
f1_keywords:
- VS.ToolsOptionsPages.F#_Tools.F#_Interactive
ms.openlocfilehash: 89570a54ecebe625a1612e4b97b01c3693e4707c
ms.sourcegitcommit: 48466b8fb7332ececff5dc388f19f6b3ff503dd4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/05/2020
ms.locfileid: "93400869"
---
# <a name="interactive-programming-with-f"></a><span data-ttu-id="c5b33-103">Programowanie interaktywne przy użyciu języka F\#</span><span class="sxs-lookup"><span data-stu-id="c5b33-103">Interactive programming with F\#</span></span>

<span data-ttu-id="c5b33-104">F# Interactive (dotnet FSI) służy do interaktywnego uruchamiania kodu F # za pomocą konsoli programu lub do wykonywania skryptów języka F #.</span><span class="sxs-lookup"><span data-stu-id="c5b33-104">F# Interactive (dotnet fsi) is used to run F# code interactively at the console, or to execute F# scripts.</span></span> <span data-ttu-id="c5b33-105">Inaczej mówiąc, program F # Interactive wykonuje REPL (odczyt, oszacowanie i drukowanie) dla języka F #.</span><span class="sxs-lookup"><span data-stu-id="c5b33-105">In other words, F# interactive executes a REPL (Read, Evaluate, Print Loop) for the F# language.</span></span>

<span data-ttu-id="c5b33-106">Aby uruchomić F# Interactive z konsoli programu, uruchom polecenie `dotnet fsi` .</span><span class="sxs-lookup"><span data-stu-id="c5b33-106">To run F# Interactive from the console, run `dotnet fsi`.</span></span> <span data-ttu-id="c5b33-107">Znajdziesz się `dotnet fsi` w dowolnym zestawie SDK platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="c5b33-107">You will find `dotnet fsi` in any .NET SDK.</span></span>

<span data-ttu-id="c5b33-108">Aby uzyskać informacje o dostępnych opcjach wiersza polecenia, zobacz [opcje F# Interactive](../../language-reference/fsharp-interactive-options.md).</span><span class="sxs-lookup"><span data-stu-id="c5b33-108">For information about available command-line options, see [F# Interactive Options](../../language-reference/fsharp-interactive-options.md).</span></span>

## <a name="executing-code-directly-in-f-interactive"></a><span data-ttu-id="c5b33-109">Wykonywanie kodu bezpośrednio w F# Interactive</span><span class="sxs-lookup"><span data-stu-id="c5b33-109">Executing code directly in F# Interactive</span></span>

<span data-ttu-id="c5b33-110">Ponieważ F# Interactive jest pętlą REPL (Read-eval-Print), można wykonać kod interaktywnie.</span><span class="sxs-lookup"><span data-stu-id="c5b33-110">Because F# Interactive is a REPL (read-eval-print loop), you can execute code interactively in it.</span></span> <span data-ttu-id="c5b33-111">Oto przykład sesji interaktywnej po wykonaniu `dotnet fsi` z wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="c5b33-111">Here is an example of an interactive session after executing `dotnet fsi` from the command line:</span></span>

```console
Microsoft (R) F# Interactive version 11.0.0.0 for F# 5.0
Copyright (c) Microsoft Corporation. All Rights Reserved.

For help type #help;;

> let square x = x *  x;;
val square : x:int -> int

> square 12;;
val it : int = 144

> printfn "Hello, FSI!"
- ;;
Hello, FSI!
val it : unit = ()
```

<span data-ttu-id="c5b33-112">Zauważysz dwa główne elementy:</span><span class="sxs-lookup"><span data-stu-id="c5b33-112">You'll notice two main things:</span></span>

1. <span data-ttu-id="c5b33-113">Cały kod musi zostać zakończony przy użyciu podwójnego średnika ( `;;` ), który ma zostać obliczony</span><span class="sxs-lookup"><span data-stu-id="c5b33-113">All code must be terminated with a double semicolon (`;;`) to be evaluated</span></span>
2. <span data-ttu-id="c5b33-114">Kod jest obliczany i przechowywany w `it` wartości.</span><span class="sxs-lookup"><span data-stu-id="c5b33-114">Code is evaluated and stored in an `it` value.</span></span> <span data-ttu-id="c5b33-115">Możesz odwoływać się `it` interaktywnie.</span><span class="sxs-lookup"><span data-stu-id="c5b33-115">You can reference `it` interactively.</span></span>

<span data-ttu-id="c5b33-116">F# Interactive obsługuje także wielowierszowe dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="c5b33-116">F# Interactive also supports multi-line input.</span></span> <span data-ttu-id="c5b33-117">Wystarczy przerwać przesłane dane przy użyciu podwójnego średnika ( `;;` ).</span><span class="sxs-lookup"><span data-stu-id="c5b33-117">You just need to terminate your submission with a double semicolon (`;;`).</span></span> <span data-ttu-id="c5b33-118">Rozważmy następujący fragment kodu, który został wklejony do i oceniony przez F# Interactive:</span><span class="sxs-lookup"><span data-stu-id="c5b33-118">Consider the following snippet that has been pasted into and evaluated by F# Interactive:</span></span>

```console
> let getOddSquares xs =
-     xs
-     |> List.filter (fun x -> x % 2 <> 0)
-     |> List.map (fun x -> x * x)
-
- printfn "%A" (getOddSquares [1..10]);;
[1; 9; 25; 49; 81]
val getOddSquares : xs:int list -> int list
val it : unit = ()

>
```

<span data-ttu-id="c5b33-119">Formatowanie kodu jest zachowywane i występuje podwójny średnik ( `;;` ) kończący dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="c5b33-119">The code's formatting is preserved, and there is a double semicolon (`;;`) terminating the input.</span></span> <span data-ttu-id="c5b33-120">F# Interactive następnie ocenił kod i Wydrukowano wyniki.</span><span class="sxs-lookup"><span data-stu-id="c5b33-120">F# Interactive then evaluated the code and printed the results!</span></span>

## <a name="scripting-with-f"></a><span data-ttu-id="c5b33-121">Wykonywanie skryptów przy użyciu języka F\#</span><span class="sxs-lookup"><span data-stu-id="c5b33-121">Scripting with F\#</span></span>

<span data-ttu-id="c5b33-122">Interaktywny ocenianie kodu w F# Interactive może być doskonałym narzędziem do uczenia, ale szybko znajdziesz, że nie jest to wydajne w przypadku pisania kodu w normalnym edytorze.</span><span class="sxs-lookup"><span data-stu-id="c5b33-122">Evaluating code interactively in F# Interactive can be a great learning tool, but you'll quickly find that it's not as productive as writing code in a normal editor.</span></span> <span data-ttu-id="c5b33-123">Aby obsłużyć normalną edycję kodu, można napisać skrypty języka F #.</span><span class="sxs-lookup"><span data-stu-id="c5b33-123">To support normal code editing, you can write F# scripts.</span></span>

<span data-ttu-id="c5b33-124">Skrypty używają rozszerzenia pliku **FSX**.</span><span class="sxs-lookup"><span data-stu-id="c5b33-124">Scripts use the file extension **.fsx**.</span></span> <span data-ttu-id="c5b33-125">Zamiast kompilowania kodu źródłowego, a następnie uruchamiania skompilowanego zestawu, można po prostu uruchomić polecenie **dotnet FSI** i określić nazwę pliku skryptu kodu źródłowego języka f #, a program F # Interactive odczytuje kod i wykonuje go w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="c5b33-125">Instead of compiling source code and then later running the compiled assembly, you can just run **dotnet fsi** and specify the filename of the script of F# source code, and F# interactive reads the code and executes it in real time.</span></span> <span data-ttu-id="c5b33-126">Rozważmy na przykład następujący skrypt o nazwie `Script.fsx` :</span><span class="sxs-lookup"><span data-stu-id="c5b33-126">For example, consider the following script called `Script.fsx`:</span></span>

```fsharp
let getOddSquares xs =
    xs
    |> List.filter (fun x -> x % 2 <> 0)
    |> List.map (fun x -> x * x)

getOddSquares [1..10]
```

<span data-ttu-id="c5b33-127">Po utworzeniu tego pliku na komputerze można uruchomić go z `dotnet fsi` i wyświetlić dane wyjściowe bezpośrednio w oknie terminalu:</span><span class="sxs-lookup"><span data-stu-id="c5b33-127">When this file is created in your machine, you can run it with `dotnet fsi` and see the output directly in your terminal window:</span></span>

```console
dotnet fsi Script.fsx
[1; 9; 25; 49; 81]
```

<span data-ttu-id="c5b33-128">Obsługa skryptów języka F # jest natywnie obsługiwana w programie [Visual Studio](../../get-started/get-started-visual-studio.md), [Visual Studio Code](../../get-started/get-started-vscode.md)i [Visual Studio dla komputerów Mac](../../get-started/get-started-with-visual-studio-for-mac.md).</span><span class="sxs-lookup"><span data-stu-id="c5b33-128">F# scripting is natively supported in [Visual Studio](../../get-started/get-started-visual-studio.md), [Visual Studio Code](../../get-started/get-started-vscode.md), and [Visual Studio for Mac](../../get-started/get-started-with-visual-studio-for-mac.md).</span></span>

## <a name="referencing-packages-in-f-interactive"></a><span data-ttu-id="c5b33-129">Odwoływanie się do pakietów w F# Interactive</span><span class="sxs-lookup"><span data-stu-id="c5b33-129">Referencing packages in F# Interactive</span></span>

> [!NOTE]
> <span data-ttu-id="c5b33-130">Zarządzanie pakietami jest funkcją języka F # 5 i jest obecnie dostępna przy użyciu najnowszego zestawu SDK programu .NET 5.</span><span class="sxs-lookup"><span data-stu-id="c5b33-130">Package management is an F# 5 feature and is currently available using the latest .NET 5 SDK.</span></span>

<span data-ttu-id="c5b33-131">F# Interactive obsługuje odwołania do pakietów NuGet z `#r "nuget:"` składnią i opcjonalną wersją:</span><span class="sxs-lookup"><span data-stu-id="c5b33-131">F# Interactive supports referencing NuGet packages with the `#r "nuget:"` syntax and an optional version:</span></span>

```fsharp
#r "nuget: Newtonsoft.Json"
open Newtonsoft.Json

let data = {| Name = "Don Syme"; Occupation = "F# Creator" |}
JsonConvert.SerializeObject(data)
```

<span data-ttu-id="c5b33-132">Jeśli wersja nie zostanie określona, zostanie pobrany najwyższy dostępny pakiet niebędący w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="c5b33-132">If a version is not specified, the highest available non-preview package is taken.</span></span> <span data-ttu-id="c5b33-133">Aby odwołać się do określonej wersji, wprowadź wersję za pomocą przecinka.</span><span class="sxs-lookup"><span data-stu-id="c5b33-133">To reference a specific version, introduce the version via a comma.</span></span> <span data-ttu-id="c5b33-134">Może to być przydatne w przypadku odwoływania się do wersji zapoznawczej pakietu.</span><span class="sxs-lookup"><span data-stu-id="c5b33-134">This can be handy when referencing a preview version of a package.</span></span> <span data-ttu-id="c5b33-135">Rozważmy na przykład ten skrypt przy użyciu wersji zapoznawczej [DiffSharp](https://diffsharp.github.io/):</span><span class="sxs-lookup"><span data-stu-id="c5b33-135">For example, consider this script using a preview version of [DiffSharp](https://diffsharp.github.io/):</span></span>

```fsharp
#r "nuget: DiffSharp-lite,1.0.0-preview-328097867"
open DiffSharp

// A 1D tensor
let t1 = dsharp.tensor [ 0.0 .. 0.2 .. 1.0 ]

// A 2x2 tensor
let t2 = dsharp.tensor [ [ 0; 1 ]; [ 2; 2 ] ]

// Define a scalar-to-scalar function
let f (x: Tensor) = sin (sqrt x)

printfn "%A" (f (dsharp.tensor 1.2))
```

<span data-ttu-id="c5b33-136">Można określić dowolną liczbę odwołań do pakietów w skrypcie.</span><span class="sxs-lookup"><span data-stu-id="c5b33-136">You can specify as many package references as you like in a script.</span></span>

## <a name="referencing-assemblies-on-disk-with-f-interactive"></a><span data-ttu-id="c5b33-137">Odwołujące się do zestawów na dysku przy użyciu języka F # Interactive</span><span class="sxs-lookup"><span data-stu-id="c5b33-137">Referencing assemblies on disk with F# interactive</span></span>

<span data-ttu-id="c5b33-138">Alternatywnie, jeśli masz zestaw na dysku i chcesz odwołać się do niego w skrypcie, możesz użyć `#r` składni do określenia zestawu.</span><span class="sxs-lookup"><span data-stu-id="c5b33-138">Alternatively, if you have an assembly on disk and wish to reference that in a script, you can use the `#r` syntax to specify an assembly.</span></span> <span data-ttu-id="c5b33-139">Rozważmy następujący kod w projekcie skompilowanym w `MyAssembly.dll` :</span><span class="sxs-lookup"><span data-stu-id="c5b33-139">Consider the following code in a project compiled into `MyAssembly.dll`:</span></span>

```fsharp
// MyAssembly.fs
module MyAssembly
let myFunction x y = x + 2 * y
```

<span data-ttu-id="c5b33-140">Jeden skompilowany, można odwoływać się do niego w pliku o nazwie `Script.fsx` podobnej do:</span><span class="sxs-lookup"><span data-stu-id="c5b33-140">One compiled, you can reference it in a file called `Script.fsx` like so:</span></span>

```fsharp
#r "path/to/MyAssembly.dll"

printfn "%A" (MyAssembly.myFunction 10 40)
```

<span data-ttu-id="c5b33-141">Wynik jest następujący:</span><span class="sxs-lookup"><span data-stu-id="c5b33-141">The output is as follows:</span></span>

```console
dotnet fsi Script.fsx
90
```

<span data-ttu-id="c5b33-142">W skrypcie można określić dowolną liczbę odwołań do zestawów.</span><span class="sxs-lookup"><span data-stu-id="c5b33-142">You can specify as many assembly references as you like in a script.</span></span>

## <a name="loading-other-scripts"></a><span data-ttu-id="c5b33-143">Ładowanie innych skryptów</span><span class="sxs-lookup"><span data-stu-id="c5b33-143">Loading other scripts</span></span>

<span data-ttu-id="c5b33-144">Podczas tworzenia skryptów często pomocne może być użycie różnych skryptów dla różnych zadań.</span><span class="sxs-lookup"><span data-stu-id="c5b33-144">When scripting, it can often be helpful to use different scripts for different tasks.</span></span> <span data-ttu-id="c5b33-145">Czasami może być konieczne ponowne użycie kodu z poziomu skryptu w innym.</span><span class="sxs-lookup"><span data-stu-id="c5b33-145">Sometimes you may want to reuse code from on script in another.</span></span> <span data-ttu-id="c5b33-146">Zamiast kopiować zawartość wklejaną do pliku, można je łatwo załadować i oszacować `#load` .</span><span class="sxs-lookup"><span data-stu-id="c5b33-146">Rather than copy-pasting its contents into your file, you can simple load and evaluate it with `#load`.</span></span>

<span data-ttu-id="c5b33-147">Rozważ następujące kwestie `Script1.fsx` :</span><span class="sxs-lookup"><span data-stu-id="c5b33-147">Consider the following `Script1.fsx`:</span></span>

```fsharp
let square x = x * x
```

<span data-ttu-id="c5b33-148">I plik zużywany, `Script2.fsx` :</span><span class="sxs-lookup"><span data-stu-id="c5b33-148">And the consuming file, `Script2.fsx`:</span></span>

```fsharp
#load "Script1.fsx"
open Script1

printfn "%d" (square 12)
```

<span data-ttu-id="c5b33-149">Należy pamiętać, że `open Script1` Deklaracja jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="c5b33-149">Note that the `open Script1` declaration is required.</span></span> <span data-ttu-id="c5b33-150">Wynika to z faktu, że konstrukcje w skrypcie języka F # są kompilowane do modułu najwyższego poziomu, który jest nazwą pliku skryptu, w którym znajduje się.</span><span class="sxs-lookup"><span data-stu-id="c5b33-150">This is because constructs in an F# script are compiled into a top-level module that is the name of the script file it is in.</span></span>

<span data-ttu-id="c5b33-151">Można to oszacować `Script2.fsx` w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="c5b33-151">You can evaluate `Script2.fsx` like so:</span></span>

```console
dotnet fsi Script2.fsx
144
```

<span data-ttu-id="c5b33-152">Można określić dowolną liczbę `#load` dyrektyw w skrypcie.</span><span class="sxs-lookup"><span data-stu-id="c5b33-152">You can specify as many `#load` directives as you like in a script.</span></span>

## <a name="using-the-fsi-object-in-f-code"></a><span data-ttu-id="c5b33-153">Używanie `fsi` obiektu w kodzie F #</span><span class="sxs-lookup"><span data-stu-id="c5b33-153">Using the `fsi` object in F# code</span></span>

<span data-ttu-id="c5b33-154">Skrypty języka F # mają dostęp do niestandardowego `fsi` obiektu, który reprezentuje sesję F# Interactive.</span><span class="sxs-lookup"><span data-stu-id="c5b33-154">F# scripts have access to a custom `fsi` object that represents the F# Interactive session.</span></span> <span data-ttu-id="c5b33-155">Umożliwia dostosowanie takich elementów jak formatowanie danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="c5b33-155">It allows you to customize things like output formatting.</span></span> <span data-ttu-id="c5b33-156">Istnieje również możliwość uzyskania dostępu do argumentów wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="c5b33-156">It is also how you can access command-line arguments.</span></span>

<span data-ttu-id="c5b33-157">Poniższy przykład pokazuje, jak uzyskać i używać argumentów wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="c5b33-157">The following example shows how to get and use command-line arguments:</span></span>

```fsharp
let args = fsi.CommandLineArgs

for arg in args do
    printfn "%s" arg
```

<span data-ttu-id="c5b33-158">Gdy jest oceniane, drukuje wszystkie argumenty.</span><span class="sxs-lookup"><span data-stu-id="c5b33-158">When evaluated, it prints all arguments.</span></span> <span data-ttu-id="c5b33-159">Pierwszy argument jest zawsze nazwą obliczanego skryptu:</span><span class="sxs-lookup"><span data-stu-id="c5b33-159">The first argument is always the name of the script that is evaluated:</span></span>

```dotnet
dotnet fsi Script1.fsx hello world from fsi
Script1.fsx
hello
world
from
fsi
```

<span data-ttu-id="c5b33-160">Można również użyć `System.Environment.GetCommandLineArgs()` , aby uzyskać dostęp do tych samych argumentów.</span><span class="sxs-lookup"><span data-stu-id="c5b33-160">You can also use `System.Environment.GetCommandLineArgs()` to access the same arguments.</span></span>

## <a name="f-interactive-directive-reference"></a><span data-ttu-id="c5b33-161">Dokumentacja dyrektywy F# Interactive</span><span class="sxs-lookup"><span data-stu-id="c5b33-161">F# Interactive directive reference</span></span>

<span data-ttu-id="c5b33-162">`#r`Dyrektywy i `#load` obserwowane wcześniej są dostępne tylko w F# Interactive.</span><span class="sxs-lookup"><span data-stu-id="c5b33-162">The `#r` and `#load` directives seen previously are only available in F# Interactive.</span></span> <span data-ttu-id="c5b33-163">Istnieje kilka dyrektyw dostępnych tylko w F# Interactive:</span><span class="sxs-lookup"><span data-stu-id="c5b33-163">There are several directives only available in F# Interactive:</span></span>

|<span data-ttu-id="c5b33-164">Dyrektywę</span><span class="sxs-lookup"><span data-stu-id="c5b33-164">Directive</span></span>|<span data-ttu-id="c5b33-165">Opis</span><span class="sxs-lookup"><span data-stu-id="c5b33-165">Description</span></span>|
|---------|-----------|
|`#r "nuget:..."`|<span data-ttu-id="c5b33-166">Odwołuje się do pakietu z narzędzia NuGet</span><span class="sxs-lookup"><span data-stu-id="c5b33-166">References a package from NuGet</span></span>|
|`#r "assembly-name.dll"`|<span data-ttu-id="c5b33-167">Odwołuje się do zestawu na dysku</span><span class="sxs-lookup"><span data-stu-id="c5b33-167">References an assembly on disk</span></span>|
|`#load "file-name.fsx"`|<span data-ttu-id="c5b33-168">Odczytuje plik źródłowy, kompiluje go i uruchamia.</span><span class="sxs-lookup"><span data-stu-id="c5b33-168">Reads a source file, compiles it, and runs it.</span></span>|
|`#help`|<span data-ttu-id="c5b33-169">Wyświetla informacje dotyczące dostępnych dyrektyw.</span><span class="sxs-lookup"><span data-stu-id="c5b33-169">Displays information about available directives.</span></span>|
|`#I`|<span data-ttu-id="c5b33-170">Określa ścieżkę wyszukiwania zestawu w cudzysłowie.</span><span class="sxs-lookup"><span data-stu-id="c5b33-170">Specifies an assembly search path in quotation marks.</span></span>|
|`#quit`|<span data-ttu-id="c5b33-171">Kończy sesję F# Interactive.</span><span class="sxs-lookup"><span data-stu-id="c5b33-171">Terminates an F# Interactive session.</span></span>|
|<span data-ttu-id="c5b33-172">`#time "on"` lub `#time "off"`</span><span class="sxs-lookup"><span data-stu-id="c5b33-172">`#time "on"` or `#time "off"`</span></span>|<span data-ttu-id="c5b33-173">Niezależnie od tego, `#time` czy mają być wyświetlane informacje o wydajności.</span><span class="sxs-lookup"><span data-stu-id="c5b33-173">By itself, `#time` toggles whether to display performance information.</span></span> <span data-ttu-id="c5b33-174">W takim przypadku `"on"` F# Interactive miary czasu rzeczywistego, czasu procesora oraz informacje o wyrzucaniu elementów bezużytecznych dla każdej sekcji kodu, który jest interpretowany i wykonywany.</span><span class="sxs-lookup"><span data-stu-id="c5b33-174">When it is `"on"`, F# Interactive measures real time, CPU time, and garbage collection information for each section of code that is interpreted and executed.</span></span>|

<span data-ttu-id="c5b33-175">Gdy określisz pliki lub ścieżki w F# Interactive, oczekiwano literału ciągu.</span><span class="sxs-lookup"><span data-stu-id="c5b33-175">When you specify files or paths in F# Interactive, a string literal is expected.</span></span> <span data-ttu-id="c5b33-176">W związku z tym pliki i ścieżki muszą być ujęte w znaki cudzysłowu, a normalne znaki ucieczki mają zastosowanie.</span><span class="sxs-lookup"><span data-stu-id="c5b33-176">Therefore, files and paths must be in quotation marks, and the usual escape characters apply.</span></span> <span data-ttu-id="c5b33-177">Można użyć znaku, `@` Aby spowodować, F# Interactive interpretuje ciąg, który zawiera ścieżkę jako ciąg Verbatim.</span><span class="sxs-lookup"><span data-stu-id="c5b33-177">You can use the `@` character to cause F# Interactive to interpret a string that contains a path as a verbatim string.</span></span> <span data-ttu-id="c5b33-178">Powoduje to, że F# Interactive ignoruje wszystkie znaki ucieczki.</span><span class="sxs-lookup"><span data-stu-id="c5b33-178">This causes F# Interactive to ignore any escape characters.</span></span>

## <a name="interactive-and-compiled-preprocessor-directives"></a><span data-ttu-id="c5b33-179">Interaktywne i skompilowane dyrektywy preprocesora</span><span class="sxs-lookup"><span data-stu-id="c5b33-179">Interactive and compiled preprocessor directives</span></span>

<span data-ttu-id="c5b33-180">Podczas kompilowania kodu w F# Interactive, niezależnie od tego, czy uruchamiasz **interaktywnie** , czy uruchamiasz skrypt, jest zdefiniowany symbol Interactive.</span><span class="sxs-lookup"><span data-stu-id="c5b33-180">When you compile code in F# Interactive, whether you are running interactively or running a script, the symbol **INTERACTIVE** is defined.</span></span> <span data-ttu-id="c5b33-181">Podczas kompilowania kodu w kompilatorze jest zdefiniowany symbol **skompilowany** .</span><span class="sxs-lookup"><span data-stu-id="c5b33-181">When you compile code in the compiler, the symbol **COMPILED** is defined.</span></span> <span data-ttu-id="c5b33-182">W tym przypadku, jeśli kod musi być inny w skompilowanych i interaktywnych trybach, można użyć tych dyrektyw preprocesora dla kompilacji warunkowej, aby określić, która z nich ma być używana.</span><span class="sxs-lookup"><span data-stu-id="c5b33-182">Thus, if code needs to be different in compiled and interactive modes, you can use these preprocessor directives for conditional compilation to determine which to use.</span></span> <span data-ttu-id="c5b33-183">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="c5b33-183">For example:</span></span>

```fsharp
#if INTERACTIVE
// Some code that executes only in FSI
// ...
#endif
```

## <a name="using-f-interactive-in-visual-studio"></a><span data-ttu-id="c5b33-184">Używanie F# Interactive w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c5b33-184">Using F# Interactive in Visual Studio</span></span>

<span data-ttu-id="c5b33-185">Aby uruchomić F# Interactive za pomocą programu Visual Studio, można kliknąć odpowiedni przycisk paska narzędzi z etykietą **F# Interactive** lub użyć klawiszy **Ctrl + Alt + F**.</span><span class="sxs-lookup"><span data-stu-id="c5b33-185">To run F# Interactive through Visual Studio, you can click the appropriate toolbar button labeled **F# Interactive** , or use the keys **Ctrl+Alt+F**.</span></span> <span data-ttu-id="c5b33-186">Spowoduje to otwarcie okna interaktywnego, okna narzędzia z uruchomioną sesją F# Interactive.</span><span class="sxs-lookup"><span data-stu-id="c5b33-186">Doing this will open the interactive window, a tool window running an F# Interactive session.</span></span> <span data-ttu-id="c5b33-187">Możesz również wybrać kod, który ma być uruchamiany w oknie interaktywnym i nacisnąć kombinację klawiszy **ALT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="c5b33-187">You can also select some code that you want to run in the interactive window and hit the key combination **Alt+Enter**.</span></span> <span data-ttu-id="c5b33-188">F# Interactive uruchamia się w oknie narzędzia z etykietą **F# Interactive**.</span><span class="sxs-lookup"><span data-stu-id="c5b33-188">F# Interactive starts in a tool window labeled **F# Interactive**.</span></span> <span data-ttu-id="c5b33-189">W przypadku korzystania z tej kombinacji klawiszy upewnij się, że okno edytora ma fokus.</span><span class="sxs-lookup"><span data-stu-id="c5b33-189">When you use this key combination, make sure that the editor window has the focus.</span></span>

<span data-ttu-id="c5b33-190">Niezależnie od tego, czy używasz konsoli programu, czy programu Visual Studio, zostanie wyświetlony wiersz polecenia, a interpreter czeka na dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="c5b33-190">Whether you are using the console or Visual Studio, a command prompt appears and the interpreter awaits your input.</span></span> <span data-ttu-id="c5b33-191">Możesz wprowadzić kod tak samo jak w pliku kodu.</span><span class="sxs-lookup"><span data-stu-id="c5b33-191">You can enter code just as you would in a code file.</span></span> <span data-ttu-id="c5b33-192">Aby skompilować i wykonać kod, wprowadź dwa średnika ( **;;** ), aby zakończyć wiersz lub kilka wierszy danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="c5b33-192">To compile and execute the code, enter two semicolons ( **;;** ) to terminate a line or several lines of input.</span></span>

<span data-ttu-id="c5b33-193">F# Interactive próbuje skompilować kod i, jeśli to się powiedzie, wykonuje kod i drukuje sygnaturę typów i wartości, które zostały skompilowane.</span><span class="sxs-lookup"><span data-stu-id="c5b33-193">F# Interactive attempts to compile the code and, if successful, it executes the code and prints the signature of the types and values that it compiled.</span></span> <span data-ttu-id="c5b33-194">Jeśli wystąpią błędy, interpreter wyświetla komunikaty o błędach.</span><span class="sxs-lookup"><span data-stu-id="c5b33-194">If errors occur, the interpreter prints the error messages.</span></span>

<span data-ttu-id="c5b33-195">Kod wprowadzony w tej samej sesji ma dostęp do dowolnych wcześniej wprowadzonych konstrukcji, dzięki czemu można kompilować programy.</span><span class="sxs-lookup"><span data-stu-id="c5b33-195">Code entered in the same session has access to any constructs entered previously, so you can build up programs.</span></span> <span data-ttu-id="c5b33-196">Obszerny bufor w oknie narzędzi umożliwia skopiowanie kodu do pliku w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="c5b33-196">An extensive buffer in the tool window allows you to copy the code into a file if needed.</span></span>

<span data-ttu-id="c5b33-197">W przypadku uruchamiania w programie Visual Studio F# Interactive uruchamiane niezależnie od projektu, więc na przykład nie można używać konstrukcji zdefiniowanych w projekcie w F# Interactive, chyba że skopiujesz kod funkcji do okna interaktywnego.</span><span class="sxs-lookup"><span data-stu-id="c5b33-197">When run in Visual Studio, F# Interactive runs independently of your project, so, for example, you cannot use constructs defined in your project in F# Interactive unless you copy the code for the function into the interactive window.</span></span>

<span data-ttu-id="c5b33-198">Można kontrolować F# Interactive argumenty wiersza polecenia (Opcje) przez dostosowanie ustawień.</span><span class="sxs-lookup"><span data-stu-id="c5b33-198">You can control the F# Interactive command-line arguments (options) by adjusting the settings.</span></span> <span data-ttu-id="c5b33-199">W menu **Narzędzia** wybierz pozycję **Opcje...** , a następnie rozwiń węzeł **Narzędzia języka F #**.</span><span class="sxs-lookup"><span data-stu-id="c5b33-199">On the **Tools** menu, select **Options...** , and then expand **F# Tools**.</span></span> <span data-ttu-id="c5b33-200">Te dwie ustawienia, które można zmienić, to opcje F# Interactive i ustawienie **F# Interactive 64-bitowe** , które jest istotne tylko w przypadku uruchamiania F# Interactive na komputerze 64-bitowym.</span><span class="sxs-lookup"><span data-stu-id="c5b33-200">The two settings that you can change are the F# Interactive options and the **64-bit F# Interactive** setting, which is relevant only if you are running F# Interactive on a 64-bit machine.</span></span> <span data-ttu-id="c5b33-201">To ustawienie określa, czy chcesz uruchomić dedykowaną 64-bitową wersję **fsi.exe** lub **fsianycpu.exe** , która korzysta z architektury komputera, aby określić, czy uruchomić program jako proces 32-bitowy czy 64-bitowy.</span><span class="sxs-lookup"><span data-stu-id="c5b33-201">This setting determines whether you want to run the dedicated 64-bit version of **fsi.exe** or **fsianycpu.exe** , which uses the machine architecture to determine whether to run as a 32-bit or 64-bit process.</span></span>

## <a name="related-articles"></a><span data-ttu-id="c5b33-202">Pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="c5b33-202">Related articles</span></span>

|<span data-ttu-id="c5b33-203">Tytuł</span><span class="sxs-lookup"><span data-stu-id="c5b33-203">Title</span></span>|<span data-ttu-id="c5b33-204">Opis</span><span class="sxs-lookup"><span data-stu-id="c5b33-204">Description</span></span>|
|-----|-----------|
|[<span data-ttu-id="c5b33-205">Opcje interakcyjne F#</span><span class="sxs-lookup"><span data-stu-id="c5b33-205">F# Interactive Options</span></span>](../../language-reference/fsharp-interactive-options.md)|<span data-ttu-id="c5b33-206">Opisuje składnię i opcje wiersza polecenia dla F# Interactive, fsi.exe.</span><span class="sxs-lookup"><span data-stu-id="c5b33-206">Describes command-line syntax and options for the F# Interactive, fsi.exe.</span></span>|
