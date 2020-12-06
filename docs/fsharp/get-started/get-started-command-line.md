---
title: 'Wprowadzenie do języka F # z narzędziami wiersza polecenia'
description: 'Dowiedz się, jak utworzyć proste rozwiązanie z obsługą kilku projektów w języku F # przy użyciu interfejs wiersza polecenia platformy .NET Core na dowolnym systemie operacyjnym (Windows, macOS lub Linux).'
ms.date: 08/15/2020
ms.openlocfilehash: f890e31fe8c665874dc3034aebfae32e38b9031a
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96739918"
---
# <a name="get-started-with-f-with-the-net-core-cli"></a>Wprowadzenie do języka F # z interfejs wiersza polecenia platformy .NET Core

W tym artykule opisano, jak rozpocząć pracę z językiem F # w dowolnym systemie operacyjnym (Windows, macOS lub Linux) przy użyciu interfejs wiersza polecenia platformy .NET Core. Odbywa się to przez utworzenie rozwiązania obejmującego wiele projektów z biblioteką klas, która jest wywoływana przez aplikację konsolową.

## <a name="prerequisites"></a>Wymagania wstępne

Aby rozpocząć, należy zainstalować najnowszą [zestaw .NET Core SDK](https://dotnet.microsoft.com/download).

W tym artykule przyjęto założenie, że wiesz, jak używać wiersza polecenia i mieć preferowany Edytor tekstu. Jeśli nie jest już używany, [Visual Studio Code](get-started-vscode.md) jest doskonałym rozwiązaniem jako edytor tekstu dla języka F #.

## <a name="build-a-simple-multi-project-solution"></a>Tworzenie prostego rozwiązania z obsługą kilku projektów

Otwórz wiersz polecenia/Terminal i użyj polecenia [dotnet New](../../core/tools/dotnet-new.md) , aby utworzyć nowy plik rozwiązania o nazwie `FSNetCore` :

```dotnetcli
dotnet new sln -o FSNetCore
```

Następująca struktura katalogów jest generowana po uruchomieniu poprzedniego polecenia:

```console
FSNetCore
    ├── FSNetCore.sln
```

### <a name="write-a-class-library"></a>Napisz bibliotekę klas

Zmień katalogi na *FSNetCore*.

Za pomocą `dotnet new` polecenia Utwórz projekt biblioteki klas w folderze **src** o nazwie Library.

```dotnetcli
dotnet new classlib -lang "F#" -o src/Library
```

Następująca struktura katalogów jest generowana po uruchomieniu poprzedniego polecenia:

```console
└── FSNetCore
    ├── FSNetCore.sln
    └── src
        └── Library
            ├── Library.fs
            └── Library.fsproj
```

Zastąp zawartość `Library.fs` następującym kodem:

```fsharp
module Library

open Newtonsoft.Json

let getJsonNetJson value =
    let json = JsonConvert.SerializeObject(value)
    $"I used to be {value} but now I'm {json} thanks to JSON.NET!"
```

Dodaj Newtonsoft.Jsw pakiecie NuGet do projektu biblioteki.

```dotnetcli
dotnet add src/Library/Library.fsproj package Newtonsoft.Json
```

Dodaj `Library` projekt do `FSNetCore` rozwiązania przy użyciu polecenia [dotnet sln Add](../../core/tools/dotnet-sln.md) :

```dotnetcli
dotnet sln add src/Library/Library.fsproj
```

Uruchom, `dotnet build` Aby skompilować projekt. Nierozwiązane zależności zostaną przywrócone podczas kompilowania.

### <a name="write-a-console-application-that-consumes-the-class-library"></a>Napisz aplikację konsolową, która używa biblioteki klas

Za pomocą `dotnet new` polecenia Utwórz aplikację konsolową w folderze **src** o nazwie App.

```dotnetcli
dotnet new console -lang "F#" -o src/App
```

Następująca struktura katalogów jest generowana po uruchomieniu poprzedniego polecenia:

```console
└── FSNetCore
    ├── FSNetCore.sln
    └── src
        ├── App
        │   ├── App.fsproj
        │   ├── Program.fs
        └── Library
            ├── Library.fs
            └── Library.fsproj
```

Zastąp zawartość pliku `Program.fs` następującym kodem:

```fsharp
open System
open Library

[<EntryPoint>]
let main argv =
    printfn "Nice command-line arguments! Here's what JSON.NET has to say about them:"

    for arg in argv do
        let value = getJsonNetJson arg
        printfn $"{value}"

    0 // return an integer exit code
```

Dodaj odwołanie do `Library` projektu przy użyciu [dodatku dotnet Dodaj odwołanie](../../core/tools/dotnet-add-reference.md).

```dotnetcli
dotnet add src/App/App.fsproj reference src/Library/Library.fsproj
```

Dodaj `App` projekt do `FSNetCore` rozwiązania przy użyciu `dotnet sln add` polecenia:

```dotnetcli
dotnet sln add src/App/App.fsproj
```

Przywróć zależności NuGet `dotnet restore` i uruchom polecenie, `dotnet build` Aby skompilować projekt.

Zmień katalog na `src/App` projekt konsoli i uruchom przekazywanie projektu `Hello World` jako argumenty:

```dotnetcli
cd src/App
dotnet run Hello World
```

Powinny zostać wyświetlone następujące wyniki:

```console
Nice command-line arguments! Here's what JSON.NET has to say about them:

I used to be Hello but now I'm ""Hello"" thanks to JSON.NET!
I used to be World but now I'm ""World"" thanks to JSON.NET!
```

## <a name="next-steps"></a>Następne kroki

Następnie zapoznaj się z [przewodnikiem po języku f #](../tour.md) , aby dowiedzieć się więcej o różnych funkcjach języka f #.
