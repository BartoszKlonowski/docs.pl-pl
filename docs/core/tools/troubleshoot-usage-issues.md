---
title: Rozwiązywanie problemów z użyciem narzędzia .NET Core
description: Poznaj typowe problemy występujące podczas uruchamiania narzędzi .NET Core i możliwych rozwiązań.
author: kdollard
ms.topic: troubleshooting
ms.date: 02/14/2020
ms.openlocfilehash: db88958e1605fef589c5dbcb12065a6318183705
ms.sourcegitcommit: cbb19e56d48cf88375d35d0c27554d4722761e0d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2020
ms.locfileid: "88608316"
---
# <a name="troubleshoot-net-core-tool-usage-issues"></a>Rozwiązywanie problemów z użyciem narzędzia .NET Core

Podczas próby zainstalowania lub uruchomienia narzędzia platformy .NET Core może wystąpić problem, który może być globalnym narzędziem lub narzędziem lokalnym. W tym artykule opisano typowe główne przyczyny i niektóre możliwe rozwiązania.

## <a name="installed-net-core-tool-fails-to-run"></a>Nie można uruchomić zainstalowanego narzędzia .NET Core

W przypadku niepowodzenia uruchomienia narzędzia .NET Core najprawdopodobniej wystąpił jeden z następujących problemów:

* Nie znaleziono pliku wykonywalnego dla narzędzia.
* Nie znaleziono prawidłowej wersji środowiska uruchomieniowego .NET Core.

### <a name="executable-file-not-found"></a>Nie znaleziono pliku wykonywalnego

Jeśli plik wykonywalny nie zostanie znaleziony, zostanie wyświetlony komunikat podobny do następującego:

```console
Could not execute because the specified command or file was not found.
Possible reasons for this include:
  * You misspelled a built-in dotnet command.
  * You intended to execute a .NET Core program, but dotnet-xyz does not exist.
  * You intended to run a global tool, but a dotnet-prefixed executable with this name could not be found on the PATH.
```

Nazwa pliku wykonywalnego określa sposób wywołania narzędzia. W poniższej tabeli opisano format:

| Format nazwy pliku wykonywalnego  | Format wywołania   |
|-------------------------|---------------------|
| `dotnet-<toolName>.exe` | `dotnet <toolName>` |
| `<toolName>.exe`        | `<toolName>`        |

* Narzędzia globalne

  Narzędzia globalne można zainstalować w katalogu domyślnym lub w określonej lokalizacji. Domyślne katalogi są następujące:

  | System operacyjny          | Ścieżka                          |
  |-------------|-------------------------------|
  | Linux/macOS | `$HOME/.dotnet/tools`         |
  | Windows     | `%USERPROFILE%\.dotnet\tools` |

  Jeśli próbujesz uruchomić narzędzie globalne, sprawdź, czy `PATH` zmienna środowiskowa na komputerze zawiera ścieżkę, w której zainstalowano narzędzie globalne i czy plik wykonywalny znajduje się w tej ścieżce.

  Interfejs wiersza polecenia platformy .NET Core próbuje dodać domyślną lokalizację do zmiennej środowiskowej PATH przy pierwszym użyciu. Istnieją jednak sytuacje, w których lokalizacja nie może być automatycznie dodawana do ścieżki:

  * Jeśli używasz systemu Linux i zainstalowano zestaw .NET Core SDK przy użyciu plików *tar. gz* , a nie apt-get lub RPM.
  * Jeśli używasz macOS 10,15 "Catalina" lub nowszych wersji.
  * Jeśli używasz macOS 10,14 "Mojave" lub wcześniejszych wersji, a zainstalowano zestaw .NET Core SDK przy użyciu plików *tar. gz* , a nie *. pkg*.
  * Jeśli zainstalowano zestaw SDK programu .NET Core 3,0 i ustawisz `DOTNET_ADD_GLOBAL_TOOLS_TO_PATH` zmienną środowiskową na `false` .
  * Jeśli zainstalowano zestaw .NET Core 2,2 SDK lub wcześniejsze wersje, a `DOTNET_SKIP_FIRST_TIME_EXPERIENCE` zmienna środowiskowa jest ustawiona na `true` .

  W tych scenariuszach lub w przypadku wybrania `--tool-path` opcji `PATH` zmienna środowiskowa na komputerze nie zawiera automatycznie ścieżki, w której zainstalowano narzędzie globalne. W takim przypadku należy dołączyć lokalizację narzędzia (na przykład `$HOME/.dotnet/tools` ) do `PATH` zmiennej środowiskowej przy użyciu dowolnej metody zapewnianej przez powłokę do aktualizowania zmiennych środowiskowych. Aby uzyskać więcej informacji, zobacz [Narzędzia platformy .NET Core](global-tools.md).

* Narzędzia lokalne

  Jeśli próbujesz uruchomić narzędzie lokalne, sprawdź, czy istnieje plik manifestu o nazwie *dotnet-tools.json* w bieżącym katalogu lub w dowolnym z jego katalogów nadrzędnych. Ten plik może również znajdować się w folderze o nazwie *. config* gdziekolwiek w hierarchii folderów projektu, a nie w folderze głównym. Jeśli *dotnet-tools.json* istnieje, otwórz go i sprawdź narzędzie, które próbujesz uruchomić. Jeśli plik nie zawiera wpisu dla programu `"isRoot": true` , należy również zapoznać się z tematem dalszej hierarchii plików dla dodatkowych plików manifestu narzędzia.

  Jeśli próbujesz uruchomić narzędzie .NET Core, które zostało zainstalowane z określoną ścieżką, musisz dołączyć tę ścieżkę podczas korzystania z narzędzia. Przykładem użycia narzędzia z zainstalowaną ścieżką narzędzia jest:

  ```console
  ..\<toolDirectory>\dotnet-<toolName>
  ```

### <a name="runtime-not-found"></a>Nie znaleziono środowiska uruchomieniowego

Narzędzia .NET Core są [aplikacjami zależnymi od](../deploying/index.md#publish-framework-dependent)platformy, co oznacza, że korzystają z środowiska uruchomieniowego .NET Core zainstalowanego na komputerze. Jeśli oczekiwane środowisko uruchomieniowe nie zostanie znalezione, są one zgodne z normalnymi regułami przetaczania w czasie wykonywania w środowisku .NET Core

* Aplikacja przenosi do przodu do najwyższej wersji poprawki określonej głównej i pomocniczej.
* Jeśli nie ma pasującego środowiska uruchomieniowego z odpowiadającym mu numerem wersji głównej i pomocniczej, używana jest kolejna wyższa wersja pomocnicza.
* Przewinięcie do przodu nie występuje między wersjami w wersji zapoznawczej środowiska uruchomieniowego a wersjami zapoznawczymi i wersjami. W związku z tym narzędzia programu .NET Core utworzone przy użyciu wersji zapoznawczej muszą zostać odbudowane i ponownie opublikowane przez autora oraz zainstalowaną ponowną instalację.

Przekazanie do przodu nie będzie odbywać się domyślnie w dwóch typowych scenariuszach:

* Dostępne są tylko małe wersje środowiska uruchomieniowego. Przekazanie do przodu wybiera tylko późniejsze wersje środowiska uruchomieniowego.
* Dostępne są tylko nowsze wersje główne środowiska uruchomieniowego. Przekazanie do przodu nie przekracza głównych granic wersji.

Jeśli aplikacja nie może znaleźć odpowiedniego środowiska uruchomieniowego, nie można uruchomić i zgłosi błąd.

Aby dowiedzieć się, które środowiska uruchomieniowe platformy .NET Core są zainstalowane na maszynie, użyj jednego z następujących poleceń:

```dotnetcli
dotnet --list-runtimes
dotnet --info
```

Jeśli uważasz, że narzędzie powinno obsługiwać aktualnie zainstalowaną wersję środowiska uruchomieniowego, możesz skontaktować się z autorem narzędzia i sprawdzić, czy może zaktualizować numer wersji lub wiele obiektów docelowych. Po ponownym skompilowaniu i ponownym opublikowaniu pakietu narzędzi do NuGet przy użyciu zaktualizowanego numeru wersji można zaktualizować kopię. Chociaż to się nie dzieje, najszybszym rozwiązaniem jest zainstalowanie wersji środowiska uruchomieniowego, która będzie działać z narzędziem, które próbujesz uruchomić. Aby pobrać konkretną wersję środowiska uruchomieniowego platformy .NET Core, odwiedź [stronę pobierania programu .NET Core](https://dotnet.microsoft.com/download/dotnet-core).

W przypadku zainstalowania zestaw .NET Core SDK w lokalizacji innej niż domyślna należy ustawić dla zmiennej środowiskowej `DOTNET_ROOT` katalog zawierający `dotnet` plik wykonywalny.

## <a name="net-core-tool-installation-fails"></a>Instalacja narzędzia .NET Core kończy się niepowodzeniem

Istnieje kilka powodów, dla których instalacja narzędzia globalnego lub lokalnego programu .NET Core może zakończyć się niepowodzeniem. Gdy instalacja narzędzia nie powiedzie się, zostanie wyświetlony komunikat podobny do następującego:

```console
Tool '{0}' failed to install. This failure may have been caused by:

* You are attempting to install a preview release and did not use the --version option to specify the version.
* A package by this name was found, but it was not a .NET Core tool.
* The required NuGet feed cannot be accessed, perhaps because of an Internet connection problem.
* You mistyped the name of the tool.

For more reasons, including package naming enforcement, visit https://aka.ms/failure-installing-tool
```

Aby pomóc zdiagnozować te błędy, komunikaty NuGet są wyświetlane bezpośrednio użytkownikowi wraz z poprzednią wiadomością. Komunikat NuGet może pomóc w zidentyfikowaniu problemu.

### <a name="package-naming-enforcement"></a>Wymuszanie nazewnictwa pakietów

Firma Microsoft zmieniła swoje wskazówki dotyczące identyfikatora pakietu dla narzędzi, co spowodowało, że nie znaleziono wielu narzędzi z przewidywaną nazwą. Nowe wskazówki polegają na tym, że wszystkie narzędzia firmy Microsoft są poprzedzone prefiksem "Microsoft". Ten prefiks jest zarezerwowany i może być używany tylko w przypadku pakietów podpisanych za pomocą autoryzowanego certyfikatu firmy Microsoft.

W trakcie przejścia niektóre narzędzia firmy Microsoft będą miały starą postać identyfikatora pakietu, a inne będą miały nowy formularz:

```dotnetcli
dotnet tool install -g Microsoft.<toolName>
dotnet tool install -g <toolName>
```

W miarę aktualizowania identyfikatorów pakietów należy zmienić identyfikator pakietu, aby pobrać najnowsze aktualizacje. Pakiety z uproszczoną nazwą narzędzia będą przestarzałe.

### <a name="preview-releases"></a>Wersje zapoznawcze

* Podjęto próbę zainstalowania wersji zapoznawczej i nie użyto `--version` opcji do określenia wersji.

Narzędzia .NET Core, które są w wersji zapoznawczej, muszą być określone przy użyciu części nazwy, aby wskazać, że są one w wersji zapoznawczej. Nie musisz zawierać całej wersji zapoznawczej. Przy założeniu, że numery wersji mają oczekiwany format, można użyć podobnej do poniższego przykładu:

```dotnetcli
dotnet tool install -g --version 1.1.0-pre <toolName>
```

### <a name="package-isnt-a-net-core-tool"></a>Pakiet nie jest narzędziem platformy .NET Core

* Znaleziono pakiet NuGet o tej nazwie, ale nie jest to narzędzie .NET Core.

Jeśli spróbujesz zainstalować pakiet NuGet, który jest regularnym pakietem NuGet, a nie narzędziem .NET Core, zobaczysz błąd podobny do poniższego:

> NU1212: Nieprawidłowa kombinacja projektu — pakiet dla `<ToolName>` . Styl projektu DotnetToolReference może zawierać tylko odwołania do typu DotnetTool.

### <a name="nuget-feed-cant-be-accessed"></a>Nie można uzyskać dostępu do źródła danych NuGet

* Nie można uzyskać dostępu do wymaganego kanału informacyjnego NuGet, prawdopodobnie z powodu problemu z połączeniem internetowym.

Instalacja narzędzia wymaga dostępu do źródła danych NuGet zawierającego pakiet narzędzi. Nie powiedzie się, jeśli źródło danych nie jest dostępne. Można zmienić źródła danych z `nuget.config` , zażądać określonego `nuget.config` pliku lub określić dodatkowe źródła danych za pomocą `--add-source` przełącznika. Domyślnie NuGet zgłasza błąd dla każdego źródła danych, które nie może nawiązać połączenia. Flaga `--ignore-failed-sources` może pominąć te źródła nieosiągalne.

### <a name="package-id-incorrect"></a>Nieprawidłowy identyfikator pakietu

* Nazwa narzędzia nie została wpisana.

Typową przyczyną błędu jest to, że nazwa narzędzia nie jest poprawna. Może się to zdarzyć z powodu błędnego wpisania lub, ponieważ narzędzie zostało przeniesione lub zostało zaniechane. W przypadku narzędzi w systemie NuGet.org należy upewnić się, że nazwa jest poprawna, aby wyszukać narzędzie pod adresem NuGet.org i skopiować polecenie instalacji.

## <a name="see-also"></a>Zobacz też

* [Narzędzia .NET Core](global-tools.md)
