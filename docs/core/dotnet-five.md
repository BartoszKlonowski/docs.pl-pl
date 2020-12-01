---
title: Co nowego w wersji .NET 5
description: Dowiedz się więcej na temat platformy .NET 5 — platformy deweloperskiej obejmującej wiele platform i typu "open source", która jest kolejną ewolucją platformy .NET Core.
ms.date: 11/30/2020
ms.topic: overview
ms.author: dapine
author: IEvangelist
ms.openlocfilehash: d0b8533dd63dd7d24f49e11093770b52d7daea89
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96437864"
---
# <a name="whats-new-in-net-5"></a>Co nowego w wersji .NET 5

.NET 5,0 to następna wersja główna programu .NET Core, która jest następująca: 3,1. Ta nowa wersja programu .NET 5,0 zamiast programu .NET Core 4,0 została nazywana z dwóch powodów:

- Pominięto numery wersji 4. x, aby uniknąć pomyłek w .NET Framework 4. x.
- Porzucamy "rdzeń" z nazwy, aby podkreślić, że jest to główna implementacja platformy .NET do przodu. Platforma .NET 5,0 obsługuje więcej typów aplikacji i więcej platform niż .NET Core lub .NET Framework.

ASP.NET Core 5,0 jest oparty na platformie .NET 5,0, ale zachowuje nazwę "rdzeń", aby uniknąć pomyłki z ASP.NET MVC 5. Podobnie, Entity Framework Core 5,0 zachowuje nazwę "rdzeń", aby uniknąć pomyłki z Entity Framework 5 i 6.

Program .NET 5,0 zawiera następujące ulepszenia i nowe funkcje w porównaniu z programem .NET Core 3,1:

- [Aktualizacje w języku C#](#c-updates)
- [Aktualizacje języka F #](#f-updates)
- [Aktualizacje Visual Basic](#visual-basic-updates)
- [System.Text.Jsnowych funkcji](#systemtextjson-new-features)
- [Aplikacje pojedynczego pliku](deploying/single-file.md)
- [Przycinanie aplikacji](https://devblogs.microsoft.com/dotnet/app-trimming-in-net-5)
- Funkcje wewnętrzne ARM64 i ARM64 systemu Windows
- Narzędzia obsługujące debugowanie zrzutów
- Biblioteki środowiska uruchomieniowego są 80% adnotacją dla [typów odwołań dopuszczających wartości null](../csharp/nullable-references.md)
- Ulepszenia wydajności:
  - [Odzyskiwanie pamięci (GC)](https://devblogs.microsoft.com/dotnet/performance-improvements-in-net-5/#gc)
  - [System.Text.Json](https://devblogs.microsoft.com/dotnet/performance-improvements-in-net-5/#json)
  - [System.Text.RegularExpressions](https://devblogs.microsoft.com/dotnet/regex-performance-improvements-in-net-5)
  - [Asynchroniczne buforowanie ValueTask](https://devblogs.microsoft.com/dotnet/async-valuetask-pooling-in-net-5)
  - [Optymalizacje rozmiaru kontenera](https://github.com/dotnet/dotnet-docker/issues/1814#issuecomment-625294750)
  - [Wiele więcej obszarów](https://devblogs.microsoft.com/dotnet/performance-improvements-in-net-5)

## <a name="net-50-doesnt-replace-net-framework"></a>.NET 5,0 nie zastępuje .NET Framework

.NET 5,0 to główna implementacja platformy .NET do przodu i .NET Framework 4. x jest nadal obsługiwana.

Nie ma żadnych planów dotyczących portów z .NET Framework do .NET 5,0, ale istnieją alternatywy w programie .NET 5,0:

| Technologia            | Zalecana alternatywa                                                                         |
|-----------------------|-------------------------------------------------------------------------------------------------|
| Formularze sieci Web             | ASP.NET Core [Blazor](/aspnet/core/blazor) lub [Razor Pages](/aspnet/core/tutorials/razor-pages) |
| Windows Workflow (WF) | [CoreWF "open source"](https://github.com/UiPath-Open/corewf)                                     |

### <a name="windows-communication-foundation"></a>Windows Communication Foundation

Oryginalna implementacja programu [Windows Communication Foundation (WCF)](../framework/wcf/index.md) była obsługiwana tylko w systemie Windows. Istnieje jednak Port klienta dostępny w programie .NET Foundation. Jest to całkowicie [Open Source](https://github.com/dotnet/wcf), cross platform i obsługiwane przez firmę Microsoft. Poniżej wymieniono podstawowe pakiety NuGet:

- [System. ServiceModel. Duplex](https://www.nuget.org/packages/System.ServiceModel.Duplex)
- [System. ServiceModel. Federation](https://www.nuget.org/packages/System.ServiceModel.Federation)
- [System. ServiceModel. http](https://www.nuget.org/packages/System.ServiceModel.Http)
- [System. ServiceModel. NetTcp](https://www.nuget.org/packages/System.ServiceModel.NetTcp)
- [System. ServiceModel. Prymityws](https://www.nuget.org/packages/System.ServiceModel.Primitives)
- [System. ServiceModel. Security](https://www.nuget.org/packages/System.ServiceModel.Security)

Społeczność zachowuje składniki serwera, które uzupełniają wymienione wyżej biblioteki klienta. Repozytorium GitHub można znaleźć pod adresem [CoreWCF](https://github.com/CoreWCF/CoreWCF). Składniki serwera _nie_ są oficjalnie obsługiwane przez firmę Microsoft. Aby zapoznać się z alternatywą dla WCF, należy rozważyć [gRPC](/aspnet/core/grpc).

## <a name="net-50-doesnt-replace-net-standard"></a>.NET 5,0 nie zastępuje .NET Standard

Nowe opracowywanie aplikacji może określać `net5.0` moniker platformy docelowej (TFM) dla wszystkich typów projektów, w tym biblioteki klas. Udostępnianie kodu między obciążeniami programu .NET 5 jest uproszczone w tym, że wszystko, co jest potrzebne, to `net5.0` TFM.

W przypadku aplikacji i bibliotek programu .NET 5,0, `net5.0` moniker struktury docelowej (TFM) łączy i zastępuje `netcoreapp` `netstandard` TFMs. Jeśli jednak planujesz udostępnianie kodu między obciążeniami .NET Framework, .NET Core i .NET 5, możesz to zrobić, określając `netstandard2.0` jako TFM. Aby uzyskać więcej informacji, zobacz [.NET Standard](../standard/net-standard.md).

## <a name="c-updates"></a>Aktualizacje w języku C#

Deweloperzy piszący aplikacje .NET 5 będą mieli dostęp do najnowszej wersji i funkcji języka C#. Program .NET 5 jest sparowany z językiem C# 9, który oferuje wiele nowych funkcji w języku. Oto kilka świateł:

- Rekordy: typy referencyjne z semantyką równości opartej na wartościach i mutacją nieniszczącą obsługiwaną przez nowe `with` wyrażenie.
- Dopasowywanie do wzorca relacyjnego: rozszerza możliwości dopasowania wzorców do operatorów relacyjnych dla obliczeń porównawczych i wyrażeń, w tym wzorców logicznych — nowe słowa kluczowe `and` , `or` i `not` .
- Instrukcje najwyższego poziomu: jako metody przyspieszania wdrażania i uczenia się języka C#, `Main` Metoda może zostać pominięta, a aplikacja jako prosta jest prawidłowa:

   ```csharp
   System.Console.Write("Hello world!");
   ```

- Wskaźniki funkcji: konstrukcje języka, które uwidaczniają następujące kod w języku pośrednim (IL): `ldftn` i `calli` .

Aby uzyskać więcej informacji na temat dostępnych funkcji języka C# 9, zobacz [co nowego w języku c# 9](../csharp/whats-new/csharp-9.md).

### <a name="source-generators"></a>Generatory źródeł

Oprócz niektórych wyróżnionych nowych funkcji języka C#, generatory źródeł są gotowe do projektów deweloperskich. Generatory źródła umożliwiają kod, który jest uruchamiany podczas kompilacji w celu sprawdzenia programu i tworzenia dodatkowych plików, które są kompilowane razem z resztą kodu.

Aby uzyskać więcej informacji na temat generatorów źródeł, zobacz [wprowadzenie do źródłowych generatorów języka c#](https://devblogs.microsoft.com/dotnet/introducing-c-source-generators) i [próbek generatora źródła c#](https://devblogs.microsoft.com/dotnet/new-c-source-generator-samples).

## <a name="f-updates"></a>Aktualizacje języka F #

F # to język programowania funkcjonalny .NET, a w przypadku platformy .NET 5 deweloperzy mają dostęp do programu F # 5. Oto kilka nowych funkcji języka F # 5:

### <a name="interpolated-strings"></a>Ciągi interpolowane

Podobnie jak ciąg interpolowany w języku C#, a nawet JavaScript, język F # obsługuje interpolację ciągów podstawowych.

```fsharp
let name = "David"
let age = 36
let message = $"{name} is {age} years old."
```

Oprócz podstawowej interpolacji ciągów jest wpisana Interpolacja. Po wpisaniu interpolacji, dany typ musi być zgodny ze specyfikatorem formatu.

```fsharp
let name = "David"
let age = 36
let message = $"%s{name} is %d{age} years old."
```

Jest to podobne do [`sprintf`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-printfmodule.html#sprintf) funkcji, która formatuje ciąg w oparciu o dane wejściowe bezpieczne dla typów. <!-- For more information, see [What's new in F# 5](fsharp/whats-new/fsharp-50.md). -->

## <a name="visual-basic-updates"></a>Aktualizacje Visual Basic

Nie ma nowych funkcji języka dla Visual Basic w programie .NET 5. Jednak w przypadku platformy .NET 5 obsługa Visual Basic została rozszerzona o następujące:

| Opis                            | `dotnet new` konstruktora |
|----------------------------------------|------------------------|
| Aplikacja konsoli                    | `console`              |
| Biblioteka klas                          | `classlib`             |
| Aplikacja WPF                        | `wpf`                  |
| Biblioteka klas WPF                      | `wpflib`               |
| Biblioteka kontrolek niestandardowych WPF             | `wpfcustomcontrollib`  |
| Biblioteka kontrolek użytkownika WPF               | `wpfusercontrollib`    |
| Aplikacja Windows Forms (WinForms)   | `winforms`             |
| Biblioteka klas Windows Forms (WinForms) | `winformslib`          |
| Projekt testu jednostkowego                      | `mstest`               |
| Projekt testowy NUnit 3                   | `nunit`                |
| Element testowy NUnit 3                      | `nunit-test`           |
| Projekt testu xUnit                     | `xunit`                |

Aby uzyskać więcej informacji na temat szablonów projektów z interfejsu wiersza polecenia platformy .NET, zobacz [`dotnet new`](tools/dotnet-new.md) .

## <a name="systemtextjson-new-features"></a>System.Text.Jsnowych funkcji

W [ systemach iSystem.Text.Js](../standard/serialization/system-text-json-overview.md)są dostępne nowe funkcje:

- [Zachowaj odwołania i dojścia cykliczne odwołania](../standard/serialization/system-text-json-preserve-references.md)
- [Metody rozszerzenia HttpClient i HttpContent](../standard/serialization/system-text-json-how-to.md#httpclient-and-httpcontent-extension-methods)
- [Zezwalaj lub zapisuj liczby w cudzysłowach](../standard/serialization/system-text-json-invalid-json.md#allow-or-write-numbers-in-quotes)
- [Obsługa niemodyfikowalnych typów i rekordów C# 9](../standard/serialization/system-text-json-immutability.md)
- [Obsługa metod dostępu do właściwości niepublicznych](../standard/serialization/system-text-json-immutability.md)
- [Pola pomocy technicznej](../standard/serialization/system-text-json-how-to.md#include-fields)
- [Ignoruj warunkowo właściwości](../standard/serialization/system-text-json-ignore-properties.md)
- [Obsługa słowników z kluczami niebędącymi ciągami](../standard/serialization/system-text-json-migrate-from-newtonsoft-how-to.md#dictionary-with-non-string-key)
- [Zezwalaj na obsługę niestandardowych konwerterów o wartości null](../standard/serialization/system-text-json-converters-how-to.md#handle-null-values)
- [Kopiuj JsonSerializerOptions](../standard/serialization/system-text-json-configure-options.md#copy-jsonserializeroptions)
- [Tworzenie JsonSerializerOptions przy użyciu ustawień domyślnych sieci Web](../standard/serialization/system-text-json-configure-options.md#web-defaults-for-jsonserializeroptions)

## <a name="see-also"></a>Zobacz też

- [Podróż do jednego programu .NET](https://channel9.msdn.com/Events/Build/2020/BOD106)
- [Ulepszenia wydajności w programie .NET 5](https://devblogs.microsoft.com/dotnet/performance-improvements-in-net-5)
- [Pobierz zestaw .NET SDK](https://dotnet.microsoft.com/download)
