---
title: Informacje o F# Interactive (dotnet)
description: 'Dowiedz się, jak F# Interactive (dotnet FSI) służy do interaktywnego uruchamiania kodu F # za pomocą konsoli programu lub wykonywania skryptów języka F #.'
ms.date: 11/29/2020
f1_keywords:
- VS.ToolsOptionsPages.F#_Tools.F#_Interactive
ms.openlocfilehash: 92177c41dc6b31d9186bae8176f85787e2fb89e0
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96438041"
---
# <a name="interactive-programming-with-f"></a>Programowanie interaktywne przy użyciu języka F\#

F# Interactive (dotnet FSI) służy do interaktywnego uruchamiania kodu F # za pomocą konsoli programu lub do wykonywania skryptów języka F #. Inaczej mówiąc, program F # Interactive wykonuje REPL (odczyt, oszacowanie i drukowanie) dla języka F #.

Aby uruchomić F# Interactive z konsoli programu, uruchom polecenie `dotnet fsi` . Znajdziesz się `dotnet fsi` w dowolnym zestawie SDK platformy .NET.

Aby uzyskać informacje o dostępnych opcjach wiersza polecenia, zobacz [opcje F# Interactive](../../language-reference/fsharp-interactive-options.md).

## <a name="executing-code-directly-in-f-interactive"></a>Wykonywanie kodu bezpośrednio w F# Interactive

Ponieważ F# Interactive jest pętlą REPL (Read-eval-Print), można wykonać kod interaktywnie. Oto przykład sesji interaktywnej po wykonaniu `dotnet fsi` z wiersza polecenia:

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

Zauważysz dwa główne elementy:

1. Cały kod musi zostać zakończony przy użyciu podwójnego średnika ( `;;` ), który ma zostać obliczony
2. Kod jest obliczany i przechowywany w `it` wartości. Możesz odwoływać się `it` interaktywnie.

F# Interactive obsługuje także wielowierszowe dane wejściowe. Wystarczy przerwać przesłane dane przy użyciu podwójnego średnika ( `;;` ). Rozważmy następujący fragment kodu, który został wklejony do i oceniony przez F# Interactive:

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

Formatowanie kodu jest zachowywane i występuje podwójny średnik ( `;;` ) kończący dane wejściowe. F# Interactive następnie ocenił kod i Wydrukowano wyniki.

## <a name="scripting-with-f"></a>Wykonywanie skryptów przy użyciu języka F\#

Interaktywny ocenianie kodu w F# Interactive może być doskonałym narzędziem do uczenia, ale szybko znajdziesz, że nie jest to wydajne w przypadku pisania kodu w normalnym edytorze. Aby obsłużyć normalną edycję kodu, można napisać skrypty języka F #.

Skrypty używają rozszerzenia pliku **FSX**. Zamiast kompilowania kodu źródłowego, a następnie uruchamiania skompilowanego zestawu, można po prostu uruchomić polecenie **dotnet FSI** i określić nazwę pliku skryptu kodu źródłowego języka f #, a program F # Interactive odczytuje kod i wykonuje go w czasie rzeczywistym. Rozważmy na przykład następujący skrypt o nazwie `Script.fsx` :

```fsharp
let getOddSquares xs =
    xs
    |> List.filter (fun x -> x % 2 <> 0)
    |> List.map (fun x -> x * x)

printfn "%A" (getOddSquares [1..10])
```

Po utworzeniu tego pliku na komputerze można uruchomić go z `dotnet fsi` i wyświetlić dane wyjściowe bezpośrednio w oknie terminalu:

```console
dotnet fsi Script.fsx
[1; 9; 25; 49; 81]
```

Obsługa skryptów języka F # jest natywnie obsługiwana w programie [Visual Studio](../../get-started/get-started-visual-studio.md), [Visual Studio Code](../../get-started/get-started-vscode.md)i [Visual Studio dla komputerów Mac](../../get-started/get-started-with-visual-studio-for-mac.md).

## <a name="referencing-packages-in-f-interactive"></a>Odwoływanie się do pakietów w F# Interactive

F# Interactive obsługuje odwołania do pakietów NuGet z `#r "nuget:"` składnią i opcjonalną wersją:

```fsharp
#r "nuget: Newtonsoft.Json"
open Newtonsoft.Json

let data = {| Name = "Don Syme"; Occupation = "F# Creator" |}
JsonConvert.SerializeObject(data)
```

Jeśli wersja nie zostanie określona, zostanie pobrany najwyższy dostępny pakiet niebędący w wersji zapoznawczej. Aby odwołać się do określonej wersji, wprowadź wersję za pomocą przecinka. Może to być przydatne w przypadku odwoływania się do wersji zapoznawczej pakietu. Rozważmy na przykład ten skrypt przy użyciu wersji zapoznawczej [DiffSharp](https://diffsharp.github.io/):

```fsharp
#r "nuget: DiffSharp-lite, 1.0.0-preview-328097867"
open DiffSharp

// A 1D tensor
let t1 = dsharp.tensor [ 0.0 .. 0.2 .. 1.0 ]

// A 2x2 tensor
let t2 = dsharp.tensor [ [ 0; 1 ]; [ 2; 2 ] ]

// Define a scalar-to-scalar function
let f (x: Tensor) = sin (sqrt x)

printfn "%A" (f (dsharp.tensor 1.2))
```

### <a name="specifying-a-package-source"></a>Określanie źródła pakietu

Możesz również określić źródło pakietu przy użyciu `#i` polecenia. W poniższym przykładzie określono Źródło zdalne i lokalne:

```fsharp
#i "nuget:https://my-remote-package-source/index.json
#i @"path-to-my-local-source"
```

Poinformuje aparat rozpoznawania w obszarze okładek, aby uwzględnić również źródła zdalne i/lub lokalne dodane do skryptu.

Można określić dowolną liczbę odwołań do pakietów w skrypcie.

> [!NOTE]
> Obecnie istnieje ograniczenie dotyczące skryptów, które używają odwołań do struktury (np. `Microsoft.NET.Sdk.Web` lub  `Microsoft.NET.Sdk.WindowsDesktop` ). Pakiety, takie jak Saturn, Giraffe, WinForms, są niedostępne. Jest to śledzone w [#9417](https://github.com/dotnet/fsharp/issues/9417)problemu.

## <a name="referencing-assemblies-on-disk-with-f-interactive"></a>Odwołujące się do zestawów na dysku przy użyciu języka F # Interactive

Alternatywnie, jeśli masz zestaw na dysku i chcesz odwołać się do niego w skrypcie, możesz użyć `#r` składni do określenia zestawu. Rozważmy następujący kod w projekcie skompilowanym w `MyAssembly.dll` :

```fsharp
// MyAssembly.fs
module MyAssembly
let myFunction x y = x + 2 * y
```

Jeden skompilowany, można odwoływać się do niego w pliku o nazwie `Script.fsx` podobnej do:

```fsharp
#r "path/to/MyAssembly.dll"

printfn "%A" (MyAssembly.myFunction 10 40)
```

Wynik jest następujący:

```console
dotnet fsi Script.fsx
90
```

W skrypcie można określić dowolną liczbę odwołań do zestawów.

## <a name="loading-other-scripts"></a>Ładowanie innych skryptów

Podczas tworzenia skryptów często pomocne może być użycie różnych skryptów dla różnych zadań. Czasami może być konieczne ponowne użycie kodu z poziomu skryptu w innym. Zamiast kopiować zawartość wklejaną do pliku, można je łatwo załadować i oszacować `#load` .

Rozważ następujące kwestie `Script1.fsx` :

```fsharp
let square x = x * x
```

I plik zużywany, `Script2.fsx` :

```fsharp
#load "Script1.fsx"
open Script1

printfn "%d" (square 12)
```

Należy pamiętać, że `open Script1` Deklaracja jest wymagana. Wynika to z faktu, że konstrukcje w skrypcie języka F # są kompilowane do modułu najwyższego poziomu, który jest nazwą pliku skryptu, w którym znajduje się.

Można to oszacować `Script2.fsx` w następujący sposób:

```console
dotnet fsi Script2.fsx
144
```

Można określić dowolną liczbę `#load` dyrektyw w skrypcie.

## <a name="using-the-fsi-object-in-f-code"></a>Używanie `fsi` obiektu w kodzie F #

Skrypty języka F # mają dostęp do niestandardowego `fsi` obiektu, który reprezentuje sesję F# Interactive. Umożliwia dostosowanie takich elementów jak formatowanie danych wyjściowych. Istnieje również możliwość uzyskania dostępu do argumentów wiersza polecenia.

Poniższy przykład pokazuje, jak uzyskać i używać argumentów wiersza polecenia:

```fsharp
let args = fsi.CommandLineArgs

for arg in args do
    printfn "%s" arg
```

Gdy jest oceniane, drukuje wszystkie argumenty. Pierwszy argument jest zawsze nazwą obliczanego skryptu:

```dotnet
dotnet fsi Script1.fsx hello world from fsi
Script1.fsx
hello
world
from
fsi
```

Można również użyć `System.Environment.GetCommandLineArgs()` , aby uzyskać dostęp do tych samych argumentów.

## <a name="f-interactive-directive-reference"></a>Dokumentacja dyrektywy F# Interactive

`#r`Dyrektywy i `#load` obserwowane wcześniej są dostępne tylko w F# Interactive. Istnieje kilka dyrektyw dostępnych tylko w F# Interactive:

|Dyrektywę|Opis|
|---------|-----------|
|`#r "nuget:..."`|Odwołuje się do pakietu z narzędzia NuGet|
|`#r "assembly-name.dll"`|Odwołuje się do zestawu na dysku|
|`#load "file-name.fsx"`|Odczytuje plik źródłowy, kompiluje go i uruchamia.|
|`#help`|Wyświetla informacje dotyczące dostępnych dyrektyw.|
|`#I`|Określa ścieżkę wyszukiwania zestawu w cudzysłowie.|
|`#quit`|Kończy sesję F# Interactive.|
|`#time "on"` lub `#time "off"`|Niezależnie od tego, `#time` czy mają być wyświetlane informacje o wydajności. W takim przypadku `"on"` F# Interactive miary czasu rzeczywistego, czasu procesora oraz informacje o wyrzucaniu elementów bezużytecznych dla każdej sekcji kodu, który jest interpretowany i wykonywany.|

Gdy określisz pliki lub ścieżki w F# Interactive, oczekiwano literału ciągu. W związku z tym pliki i ścieżki muszą być ujęte w znaki cudzysłowu, a normalne znaki ucieczki mają zastosowanie. Można użyć znaku, `@` Aby spowodować, F# Interactive interpretuje ciąg, który zawiera ścieżkę jako ciąg Verbatim. Powoduje to, że F# Interactive ignoruje wszystkie znaki ucieczki.

## <a name="interactive-and-compiled-preprocessor-directives"></a>Interaktywne i skompilowane dyrektywy preprocesora

Podczas kompilowania kodu w F# Interactive, niezależnie od tego, czy uruchamiasz **interaktywnie** , czy uruchamiasz skrypt, jest zdefiniowany symbol Interactive. Podczas kompilowania kodu w kompilatorze jest zdefiniowany symbol **skompilowany** . W tym przypadku, jeśli kod musi być inny w skompilowanych i interaktywnych trybach, można użyć tych dyrektyw preprocesora dla kompilacji warunkowej, aby określić, która z nich ma być używana. Przykład:

```fsharp
#if INTERACTIVE
// Some code that executes only in FSI
// ...
#endif
```

## <a name="using-f-interactive-in-visual-studio"></a>Używanie F# Interactive w programie Visual Studio

Aby uruchomić F# Interactive za pomocą programu Visual Studio, można kliknąć odpowiedni przycisk paska narzędzi z etykietą **F# Interactive** lub użyć klawiszy **Ctrl + Alt + F**. Spowoduje to otwarcie okna interaktywnego, okna narzędzia z uruchomioną sesją F# Interactive. Możesz również wybrać kod, który ma być uruchamiany w oknie interaktywnym i nacisnąć kombinację klawiszy **ALT + ENTER**. F# Interactive uruchamia się w oknie narzędzia z etykietą **F# Interactive**. W przypadku korzystania z tej kombinacji klawiszy upewnij się, że okno edytora ma fokus.

Niezależnie od tego, czy używasz konsoli programu, czy programu Visual Studio, zostanie wyświetlony wiersz polecenia, a interpreter czeka na dane wejściowe. Możesz wprowadzić kod tak samo jak w pliku kodu. Aby skompilować i wykonać kod, wprowadź dwa średnika (**;;**), aby zakończyć wiersz lub kilka wierszy danych wejściowych.

F# Interactive próbuje skompilować kod i, jeśli to się powiedzie, wykonuje kod i drukuje sygnaturę typów i wartości, które zostały skompilowane. Jeśli wystąpią błędy, interpreter wyświetla komunikaty o błędach.

Kod wprowadzony w tej samej sesji ma dostęp do dowolnych wcześniej wprowadzonych konstrukcji, dzięki czemu można kompilować programy. Obszerny bufor w oknie narzędzi umożliwia skopiowanie kodu do pliku w razie potrzeby.

W przypadku uruchamiania w programie Visual Studio F# Interactive uruchamiane niezależnie od projektu, więc na przykład nie można używać konstrukcji zdefiniowanych w projekcie w F# Interactive, chyba że skopiujesz kod funkcji do okna interaktywnego.

Można kontrolować F# Interactive argumenty wiersza polecenia (Opcje) przez dostosowanie ustawień. W menu **Narzędzia** wybierz pozycję **Opcje...**, a następnie rozwiń węzeł **Narzędzia języka F #**. Te dwie ustawienia, które można zmienić, to opcje F# Interactive i ustawienie **F# Interactive 64-bitowe** , które jest istotne tylko w przypadku uruchamiania F# Interactive na komputerze 64-bitowym. To ustawienie określa, czy chcesz uruchomić dedykowaną 64-bitową wersję **fsi.exe** lub **fsianycpu.exe**, która korzysta z architektury komputera, aby określić, czy uruchomić program jako proces 32-bitowy czy 64-bitowy.

## <a name="related-articles"></a>Pokrewne artykuły:

|Tytuł|Opis|
|-----|-----------|
|[Opcje interakcyjne F#](../../language-reference/fsharp-interactive-options.md)|Opisuje składnię i opcje wiersza polecenia dla F# Interactive, fsi.exe.|
