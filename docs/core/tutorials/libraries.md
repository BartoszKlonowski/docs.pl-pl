---
title: Tworzenie bibliotek przy użyciu interfejsu wiersza polecenia platformy .NET
description: Dowiedz się, jak tworzyć biblioteki .NET przy użyciu interfejsu wiersza polecenia platformy .NET. Utworzysz bibliotekę, która obsługuje wiele platform.
author: cartermp
ms.topic: how-to
ms.date: 12/14/2020
ms.openlocfilehash: 5a70cec4a991f673f4d5d3e7b00cd704c6799f47
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2020
ms.locfileid: "97512414"
---
# <a name="develop-libraries-with-the-net-cli"></a>Tworzenie bibliotek przy użyciu interfejsu wiersza polecenia platformy .NET

W tym artykule opisano sposób pisania bibliotek dla platformy .NET przy użyciu interfejsu wiersza polecenia platformy .NET. Interfejs wiersza polecenia zapewnia wydajne i niskie środowisko, które działa w ramach dowolnego obsługiwanego systemu operacyjnego. Nadal możesz tworzyć biblioteki za pomocą programu Visual Studio, a jeśli jest to preferowane środowisko, [zapoznaj się z przewodnikiem programu Visual Studio](library-with-visual-studio.md).

## <a name="prerequisites"></a>Wymagania wstępne

Na komputerze musi być zainstalowany [zestaw SDK dla platformy .NET i interfejs wiersza polecenia](https://dotnet.microsoft.com/download) .

W przypadku sekcji tego dokumentu, w których znajdują się .NET Framework wersje, potrzebne są [.NET Framework](https://dotnet.microsoft.com) zainstalowane na komputerze z systemem Windows.

Ponadto, jeśli chcesz obsługiwać starsze elementy docelowe .NET Framework, musisz zainstalować pakiety językowe lub pakiety deweloperskie ze [strony archiwa pobierania programu .NET](https://dotnet.microsoft.com/download/archives). Zapoznaj się z tą tabelą:

| Wersja programu .NET Framework | Co należy pobrać                                       |
| ---------------------- | ------------------------------------------------------ |
| 4.6.1                  | .NET Framework 4.6.1                    |
| 4,6                    | Pakiet docelowy .NET Framework 4,6                      |
| 4.5.2                  | .NET Framework 4.5.2 — Pakiet dewelopera                    |
| 4.5.1                  | .NET Framework 4.5.1 — pakiet dewelopera                    |
| 4.5                    | Zestaw Windows Software Development Kit dla systemu Windows 8         |
| 4,0                    | Windows SDK dla systemów Windows 7 i .NET Framework 4         |
| 2,0, 3,0 i 3,5      | Środowisko uruchomieniowe .NET Framework 3,5 z dodatkiem SP1 (lub Windows 8 + wersja) |

## <a name="how-to-target-net-50-or-net-standard"></a>Jak kierować platformą .NET 5,0 lub .NET Standard

Możesz sterować platformą docelową projektu, dodając ją do pliku projektu (*. csproj* lub *. fsproj*). Aby uzyskać wskazówki dotyczące wyboru między elementem docelowym .NET 5,0 lub .NET Standard [, zobacz .NET 5 i .NET Standard](../../standard/net-standard.md#net-5-and-net-standard).

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
  </PropertyGroup>
</Project>
```

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
  </PropertyGroup>
</Project>
```

Jeśli chcesz dowiedzieć się, .NET Framework wersji 4,0 lub niższej, lub chcesz użyć interfejsu API dostępnego w .NET Framework, ale nie w .NET Standard (na przykład `System.Drawing` ), przeczytaj następujące sekcje i Dowiedz się, jak utworzyć element.

## <a name="how-to-target-net-framework"></a>Jak kierować .NET Framework

> [!NOTE]
> W tych instrukcjach przyjęto założenie, że na komputerze zainstalowano .NET Framework. Zapoznaj się z [wymaganiami wstępnymi](#prerequisites) , aby uzyskać zainstalowane zależności.

Należy pamiętać, że niektóre wersje .NET Framework używane w tym miejscu nie są już obsługiwane. Zapoznaj się z [zasadami cyklu pomocy technicznej .NET Framework — często zadawane pytania](https://support.microsoft.com/gp/framework_faq/en-us) dotyczące nieobsługiwanych wersji.

Jeśli chcesz osiągnąć maksymalną liczbę deweloperów i projektów, użyj .NET Framework 4,0 jako celu punktu odniesienia. Aby docelowa .NET Framework, Zacznij od używania prawidłowej monikera platformy docelowej (TFM) odpowiadającej wersji .NET Framework, która ma być obsługiwana.

| Wersja programu .NET Framework | TFM      |
| ---------------------- | -------- |
| .NET Framework 2.0     | `net20`  |
| .NET Framework 3.0     | `net30`  |
| Program .NET Framework 3,5     | `net35`  |
| .NET Framework 4.0     | `net40`  |
| .NET Framework 4.5     | `net45`  |
| .NET Framework 4.5.1   | `net451` |
| .NET Framework 4.5.2   | `net452` |
| Program .NET Framework 4.6     | `net46`  |
| .NET Framework 4.6.1   | `net461` |
| .NET Framework 4.6.2   | `net462` |
|  .NET Framework 4.7     | `net47`  |
|  .NET Framework 4.8     | `net48`  |

Następnie należy wstawić ten TFM do `TargetFramework` sekcji pliku projektu. Załóżmy na przykład, że napiszesz bibliotekę, która jest przeznaczona dla .NET Framework 4,0:

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>net40</TargetFramework>
  </PropertyGroup>
</Project>
```

I to wszystko. Chociaż jest to kompilowane tylko dla .NET Framework 4, można użyć biblioteki w nowszych wersjach .NET Framework.

## <a name="how-to-multitarget"></a>Jak wieloelementowy

> [!NOTE]
> W poniższych instrukcjach przyjęto założenie, że na komputerze zainstalowano .NET Framework. Zapoznaj się z sekcją [wymagania wstępne](#prerequisites) , aby dowiedzieć się, które zależności należy zainstalować i skąd mają być pobierane.

Może być konieczne określenie starszych wersji .NET Framework, gdy projekt obsługuje zarówno .NET Framework, jak i .NET. W tym scenariuszu, jeśli chcesz użyć nowszych interfejsów API i konstrukcji językowych dla nowszych elementów docelowych, użyj `#if` dyrektyw w kodzie. Może być również konieczne dodanie różnych pakietów i zależności dla każdej platformy docelowej, która obejmuje różne interfejsy API potrzebne do każdego przypadku.

Załóżmy na przykład, że masz bibliotekę, która wykonuje operacje sieciowe za pośrednictwem protokołu HTTP. W przypadku .NET Standard i .NET Framework wersji 4,5 lub nowszej można użyć `HttpClient` klasy z `System.Net.Http` przestrzeni nazw. Jednak wcześniejsze wersje .NET Framework nie posiadają `HttpClient` klasy, więc `WebClient` zamiast tego można użyć klasy z `System.Net` przestrzeni nazw.

Plik projektu może wyglądać następująco:

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0;net40;net45</TargetFrameworks>
  </PropertyGroup>

  <!-- Need to conditionally bring in references for the .NET Framework 4.0 target -->
  <ItemGroup Condition="'$(TargetFramework)' == 'net40'">
    <Reference Include="System.Net" />
  </ItemGroup>

  <!-- Need to conditionally bring in references for the .NET Framework 4.5 target -->
  <ItemGroup Condition="'$(TargetFramework)' == 'net45'">
    <Reference Include="System.Net.Http" />
    <Reference Include="System.Threading.Tasks" />
  </ItemGroup>
</Project>
```

Zobaczysz trzy najważniejsze zmiany tutaj:

1. `TargetFramework`Węzeł został zastąpiony przez `TargetFrameworks` , a trzy TFMs są wyrażone wewnątrz.
1. Istnieje `<ItemGroup>` węzeł `net40` docelowy ściągania w jednym .NET Framework odwołanie.
1. Istnieje `<ItemGroup>` węzeł `net45` docelowy ściągania dwóch odwołań .NET Framework.

System kompilacji ma świadomość następujących symboli preprocesora używanych w `#if` dyrektywach:

[!INCLUDE [Preprocessor symbols](../../../includes/preprocessor-symbols.md)]

Oto przykład użycia kompilacji warunkowej dla elementu docelowego:

```csharp
using System;
using System.Text.RegularExpressions;
#if NET40
// This only compiles for the .NET Framework 4 targets
using System.Net;
#else
 // This compiles for all other targets
using System.Net.Http;
using System.Threading.Tasks;
#endif

namespace MultitargetLib
{
    public class Library
    {
#if NET40
        private readonly WebClient _client = new WebClient();
        private readonly object _locker = new object();
#else
        private readonly HttpClient _client = new HttpClient();
#endif

#if NET40
        // .NET Framework 4.0 does not have async/await
        public string GetDotNetCount()
        {
            string url = "https://www.dotnetfoundation.org/";

            var uri = new Uri(url);

            string result = "";

            // Lock here to provide thread-safety.
            lock(_locker)
            {
                result = _client.DownloadString(uri);
            }

            int dotNetCount = Regex.Matches(result, ".NET").Count;

            return $"Dotnet Foundation mentions .NET {dotNetCount} times!";
        }
#else
        // .NET Framework 4.5+ can use async/await!
        public async Task<string> GetDotNetCountAsync()
        {
            string url = "https://www.dotnetfoundation.org/";

            // HttpClient is thread-safe, so no need to explicitly lock here
            var result = await _client.GetStringAsync(url);

            int dotNetCount = Regex.Matches(result, ".NET").Count;

            return $"dotnetfoundation.org mentions .NET {dotNetCount} times in its HTML!";
        }
#endif
    }
}
```

W przypadku skompilowania projektu za pomocą programu `dotnet build` zauważysz, że trzy katalogi w `bin/` folderze:

```
net40/
net45/
netstandard2.0/
```

Każdy z tych elementów zawiera `.dll` pliki dla każdego obiektu docelowego.

## <a name="how-to-test-libraries-on-net"></a>Jak przetestować biblioteki na platformie .NET

Ważne jest, aby móc testować między platformami. Możesz użyć [xUnit](https://xunit.github.io/) lub MSTest z pola. Oba są doskonale odpowiednie do testowania jednostkowego biblioteki na platformie .NET. Sposób konfigurowania rozwiązania przy użyciu projektów testowych będzie zależeć od [struktury rozwiązania](#structuring-a-solution). W poniższym przykładzie przyjęto założenie, że katalogi testowe i źródłowe znajdują się w tym samym katalogu najwyższego poziomu.

> [!NOTE]
> Spowoduje to użycie niektórych poleceń [interfejsu wiersza polecenia platformy .NET](../tools/index.md) . Aby uzyskać więcej informacji, zobacz temat [dotnet New](../tools/dotnet-new.md) i [dotnet sln](../tools/dotnet-sln.md) .

1. Skonfiguruj rozwiązanie. Można to zrobić za pomocą następujących poleceń:

   ```dotnetcli
   mkdir SolutionWithSrcAndTest
   cd SolutionWithSrcAndTest
   dotnet new sln
   dotnet new classlib -o MyProject
   dotnet new xunit -o MyProject.Test
   dotnet sln add MyProject/MyProject.csproj
   dotnet sln add MyProject.Test/MyProject.Test.csproj
   ```

   Spowoduje to utworzenie projektów i połączenie ich ze sobą w rozwiązaniu. Katalog dla `SolutionWithSrcAndTest` powinien wyglądać następująco:

   ```
   /SolutionWithSrcAndTest
   |__SolutionWithSrcAndTest.sln
   |__MyProject/
   |__MyProject.Test/
   ```

1. Przejdź do katalogu projektu testowego i Dodaj odwołanie do elementu `MyProject.Test` from `MyProject` .

   ```dotnetcli
   cd MyProject.Test
   dotnet add reference ../MyProject/MyProject.csproj
   ```

1. Przywróć pakiety i projekty kompilacji:

   ```dotnetcli
   dotnet restore
   dotnet build
   ```

1. Sprawdź, czy xUnit jest uruchamiana przez wykonanie `dotnet test` polecenia. W przypadku wybrania opcji używania MSTest, zamiast tego należy uruchomić moduł uruchamiający konsolę programu MSTest.

I to wszystko. Teraz można testować bibliotekę na wszystkich platformach przy użyciu narzędzi wiersza polecenia. Aby kontynuować testowanie teraz, gdy wszystko jest skonfigurowane, testowanie biblioteki jest bardzo proste:

1. Wprowadź zmiany w bibliotece.
1. Uruchom testy z wiersza polecenia w katalogu testowym przy użyciu `dotnet test` polecenia.

Kod zostanie automatycznie odbudowany po wywołaniu `dotnet test` polecenia.

## <a name="how-to-use-multiple-projects"></a>Jak używać wielu projektów

Typowym potrzebą dla większych bibliotek jest umieszczenie funkcjonalności w różnych projektach.

Załóżmy, że chcesz skompilować bibliotekę, która może być używana w idiomatyczne C# i F #. Oznacza to, że konsumenci biblioteki wykorzystują ją w sposób naturalny dla języka C# lub F #. Na przykład w języku C# można użyć biblioteki w następujący sposób:

```csharp
using AwesomeLibrary.CSharp;

public Task DoThings(Data data)
{
    var convertResult = await AwesomeLibrary.ConvertAsync(data);
    var result = AwesomeLibrary.Process(convertResult);
    // do something with result
}
```

W języku F # może wyglądać następująco:

```fsharp
open AwesomeLibrary.FSharp

let doWork data = async {
    let! result = AwesomeLibrary.AsyncConvert data // Uses an F# async function rather than C# async method
    // do something with result
}
```

Scenariusze użycia, takie jak to znaczy, że dostępne interfejsy API muszą mieć inną strukturę dla języków C# i F #.  Typowym podejściem do osiągnięcia tego celu jest spełnienie wszystkich logiki biblioteki w projekcie podstawowym, z projektami C# i F # definiującymi warstwy interfejsu API, które wywołują do tego projektu podstawowego.  Pozostała część sekcji będzie używać następujących nazw:

* **AwesomeLibrary. Core** — projekt podstawowy, który zawiera wszystkie logike dla biblioteki
* **AwesomeLibrary. CSharp** — projekt z publicznymi interfejsami API przeznaczonymi do użycia w języku C #
* **AwesomeLibrary. FSharp** — projekt z publicznymi interfejsami API przeznaczonymi do użycia w języku F #

W terminalu można uruchomić następujące polecenia, aby utworzyć tę samą strukturę co ten przewodnik:

```dotnetcli
mkdir AwesomeLibrary && cd AwesomeLibrary
dotnet new sln
mkdir AwesomeLibrary.Core && cd AwesomeLibrary.Core && dotnet new classlib
cd ..
mkdir AwesomeLibrary.CSharp && cd AwesomeLibrary.CSharp && dotnet new classlib
cd ..
mkdir AwesomeLibrary.FSharp && cd AwesomeLibrary.FSharp && dotnet new classlib -lang "F#"
cd ..
dotnet sln add AwesomeLibrary.Core/AwesomeLibrary.Core.csproj
dotnet sln add AwesomeLibrary.CSharp/AwesomeLibrary.CSharp.csproj
dotnet sln add AwesomeLibrary.FSharp/AwesomeLibrary.FSharp.fsproj
```

Spowoduje to dodanie trzech projektów powyżej i pliku rozwiązania, który łączy je ze sobą. Tworzenie pliku rozwiązania i łączenie projektów umożliwi przywracanie i Kompilowanie projektów na poziomie najwyższego poziomu.

### <a name="project-to-project-referencing"></a>Odwołanie projektu do projektu

Najlepszym sposobem odwoływania się do projektu jest użycie interfejsu wiersza polecenia platformy .NET do dodania odwołania do projektu. Z katalogów projektów **AwesomeLibrary. CSharp** i **AwesomeLibrary. FSharp** można uruchomić następujące polecenie:

```dotnetcli
dotnet add reference ../AwesomeLibrary.Core/AwesomeLibrary.Core.csproj
```

Pliki projektu dla obu **AwesomeLibrary. CSharp** i **AwesomeLibrary. FSharp** będą teraz odwoływać się do **AwesomeLibrary. Core** jako `ProjectReference` element docelowy.  Można to sprawdzić, sprawdzając pliki projektu i wyświetlając następujące elementy:

```xml
<ItemGroup>
  <ProjectReference Include="..\AwesomeLibrary.Core\AwesomeLibrary.Core.csproj" />
</ItemGroup>
```

Tę sekcję można dodać do każdego pliku projektu ręcznie, jeśli wolisz nie używać interfejsu wiersza polecenia platformy .NET.

### <a name="structuring-a-solution"></a>Tworzenie struktury rozwiązania

Innym ważnym aspektem rozwiązań z zakresu projektów jest ustanowienie dobrej ogólnej struktury projektu. Możesz zorganizować kod w dowolny sposób, a dopóki każdy projekt zostanie połączony z plikiem rozwiązania za pomocą programu `dotnet sln add` , będzie można uruchamiać `dotnet restore` i `dotnet build` na poziomie rozwiązania.
