---
title: Co nowego w języku C# 7.1
description: Omówienie nowych funkcji w języku C# 7,1.
ms.date: 04/09/2019
ms.openlocfilehash: fe6e49eb01e24a27bc7970900c05150378ab194a
ms.sourcegitcommit: cb27c01a8b0b4630148374638aff4e2221f90b22
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/09/2020
ms.locfileid: "86174773"
---
# <a name="whats-new-in-c-71"></a>Co nowego w języku C# 7.1

C# 7,1 to wersja pierwszego punktu w języku C#. Oznacza to zwiększoną erze wydania dla danego języka. Możesz użyć nowych funkcji szybciej, najlepiej, gdy każda nowa funkcja jest gotowa. W języku C# 7,1 Dodano możliwość skonfigurowania kompilatora w celu dopasowania do określonej wersji języka. Dzięki temu można rozdzielić decyzje dotyczące uaktualniania narzędzi z decyzji o uaktualnieniu wersji językowych.

W języku C# 7,1 dodano element konfiguracji [wyboru wersji języka](../language-reference/configure-language-version.md) , trzy nowe funkcje językowe oraz nowe zachowanie kompilatora.

Nowe funkcje języka w tej wersji są następujące:

- [`async``Main`Metoda](#async-main)
  - Punkt wejścia dla aplikacji może mieć `async` modyfikator.
- [`default`wyrażenia literału](#default-literal-expressions)
  - Można użyć domyślnych wyrażeń literałów w wyrażeniach wartości domyślnych, gdy można wywnioskować typ docelowy.
- [Wywnioskowane nazwy elementów krotki](#inferred-tuple-element-names)
  - Nazwy elementów krotki można wywnioskować na podstawie inicjalizacji krotki w wielu przypadkach.
- [Dopasowanie wzorca dla parametrów typu ogólnego](#pattern-matching-on-generic-type-parameters)
  - Wyrażeń dopasowania wzorców można używać w zmiennych, których typem jest parametr typu ogólnego.

Na koniec kompilator ma dwie opcje `-refout` i `-refonly` umożliwia [wygenerowanie zestawu odwołań](#reference-assembly-generation).

Aby użyć najnowszych funkcji w wersji próbnej, należy [skonfigurować wersję języka kompilatora](../language-reference/configure-language-version.md) i wybrać wersję.

Pozostała część tego artykułu zawiera omówienie każdej funkcji. Dla każdej funkcji znajdziesz jej uzasadnienie. Poznasz składnię. Te funkcje można eksplorować w środowisku za pomocą `dotnet try` Narzędzia globalnego:

1. Zainstaluj narzędzie [dotnet-try](https://github.com/dotnet/try/blob/master/README.md#setup) Global.
1. Sklonuj repozytorium [dotnet/try-Samples](https://github.com/dotnet/try-samples) .
1. Ustaw bieżący katalog na podkatalog *csharp7* dla repozytorium *try-Samples* .
1. Uruchom polecenie `dotnet try`.

## <a name="async-main"></a>Asynchroniczny, główny

Metoda *Async Main* umożliwia korzystanie `await` z `Main` metody.
Wcześniej należy napisać:

```csharp
static int Main()
{
    return DoAsyncWork().GetAwaiter().GetResult();
}
```

Teraz możesz napisać:

```csharp
static async Task<int> Main()
{
    // This could also be replaced with the body
    // DoAsyncWork, including its await expressions:
    return await DoAsyncWork();
}
```

Jeśli program nie zwraca kodu zakończenia, można zadeklarować `Main` metodę, która zwraca <xref:System.Threading.Tasks.Task> :

```csharp
static async Task Main()
{
    await SomeAsyncMethod();
}
```

Więcej informacji na temat szczegółowych informacji można znaleźć w artykule dotyczącym [asynchronicznego](../programming-guide/main-and-command-args/index.md) artykułu w przewodniku programowania.

## <a name="default-literal-expressions"></a>Domyślne wyrażenia literału

Domyślne wyrażenia literałów to ulepszenie wyrażeń wartości domyślnych.
Te wyrażenia inicjują zmienną do wartości domyślnej. Gdzie wcześniej warto napisać:

```csharp
Func<string, bool> whereClause = default(Func<string, bool>);
```

Możesz teraz pominąć typ po prawej stronie inicjalizacji:

```csharp
Func<string, bool> whereClause = default;
```

Aby uzyskać więcej informacji, zobacz sekcję [domyślny literał](../language-reference/operators/default.md#default-literal) w artykule [domyślny operator](../language-reference/operators/default.md) .

## <a name="inferred-tuple-element-names"></a>Wywnioskowane nazwy elementów krotki

Ta funkcja to małe rozszerzenie funkcji kroteks wprowadzonej w języku C# 7,0. Wiele razy po zainicjowaniu krotki zmienne używane dla prawej strony przypisania są takie same jak nazwy dla elementów krotki:

```csharp
int count = 5;
string label = "Colors used in the map";
var pair = (count: count, label: label);
```

Nazwy elementów krotki można wywnioskować na podstawie zmiennych używanych do inicjowania krotki w języku C# 7,1:

```csharp
int count = 5;
string label = "Colors used in the map";
var pair = (count, label); // element names are "count" and "label"
```

Więcej informacji na temat tej funkcji można znaleźć w artykule [typy krotek](../language-reference/builtin-types/value-tuples.md) .

## <a name="pattern-matching-on-generic-type-parameters"></a>Dopasowanie wzorca dla parametrów typu ogólnego

Począwszy od języka C# 7,1 wyrażenie wzorca dla `is` i `switch` wzorzec typu może mieć typ parametru typu ogólnego. Może to być najbardziej przydatne podczas sprawdzania typów, które mogą być `struct` albo `class` typu, i chcesz uniknąć pakowania.

## <a name="reference-assembly-generation"></a>Generowanie zestawu odwołań

Istnieją dwie nowe opcje kompilatora, które generują *zestawy tylko do odwołania*: [-opcji refout](../language-reference/compiler-options/refout-compiler-option.md) i [-refonly](../language-reference/compiler-options/refonly-compiler-option.md).
Połączone artykuły wyjaśniają te opcje i zestawy referencyjne bardziej szczegółowo.
