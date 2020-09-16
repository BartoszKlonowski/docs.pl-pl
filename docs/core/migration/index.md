---
title: Migracja platformy .NET Core z project.jsna
description: Dowiedz się, jak przeprowadzić migrację starszego projektu .NET Core przy użyciu project.jsna
ms.date: 07/19/2017
ms.openlocfilehash: 0d4190a02389089a888d8b52dd8e7c412636b575
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90538253"
---
# <a name="migrating-net-core-projects-from-projectjson"></a>Migrowanie projektów .NET Core z project.jsna

W tym dokumencie opisano następujące trzy scenariusze migracji dla projektów programu .NET Core:

1. [Migracja z prawidłowego najnowszego schematu *project.jsna* *csproj*](#migration-from-projectjson-to-csproj)
2. [Migracja z środowiska DNX do csproj](#migration-from-dnx-to-csproj)
3. [Migracja z RC3 i poprzednich projektów .NET Core csproj do końcowego formatu](#migration-from-earlier-net-core-csproj-formats-to-rtm-csproj)

Ten dokument ma zastosowanie tylko do starszych projektów programu .NET Core, które używają project.json. Nie dotyczy migrowania z .NET Framework do programu .NET Core.

## <a name="migration-from-projectjson-to-csproj"></a>Migracja z project.jsna csproj

Migracja z *project.js* do *. csproj* można wykonać przy użyciu jednej z następujących metod:

- [Visual Studio](#visual-studio)
- [Narzędzie wiersza polecenia migracji dotnet](#dotnet-migrate)

Obie metody używają tego samego aparatu podstawowego do migrowania projektów, dlatego wyniki będą takie same dla obu tych metod. W większości przypadków użycie jednego z tych dwóch metod migracji *project.js* do *csproj* jest jedyną potrzebną operacją i nie jest konieczne żadne dalsze ręczne edytowanie pliku projektu. Utworzony plik *csproj* będzie taki sam jak nazwa katalogu zawierającego.

### <a name="visual-studio"></a>Visual Studio

Po otwarciu pliku *. xproj* lub pliku rozwiązania, który odwołuje się do plików *. Xproj* w programie Visual Studio 2017 lub Visual studio 2019 w wersji 16,2 i starszej, zostanie wyświetlone okno dialogowe **uaktualnianie jednokierunkowe** . W oknie dialogowym zostaną wyświetlone projekty do migracji. Jeśli otworzysz plik rozwiązania, zostaną wyświetlone wszystkie projekty określone w pliku rozwiązania. Przejrzyj listę projektów do migracji i wybierz **przycisk OK**.

![Jednokierunkowe okno dialogowe uaktualniania zawierające listę projektów do migracji](media/one-way-upgrade.jpg)

Program Visual Studio automatycznie migruje wybrane projekty. W przypadku migrowania rozwiązania, jeśli nie wybrano wszystkich projektów, zostanie wyświetlone okno dialogowe z prośbą o uaktualnienie pozostałych projektów z tego rozwiązania. Po przeprowadzeniu migracji projektu można zobaczyć i zmodyfikować jego zawartość, klikając prawym przyciskiem myszy projekt w oknie **Eksplorator rozwiązań** i wybierając polecenie **Edit \<project name> . csproj**.

Pliki migrowane (*project.json*, *global.json*, *xproj*i plik rozwiązania) są przenoszone do folderu *kopii zapasowej* . Migrowany plik rozwiązania jest uaktualniany do programu Visual Studio 2017 lub Visual Studio 2019 i nie będzie można otworzyć tego pliku rozwiązania w programie Visual Studio 2015 lub jego wcześniejszych wersjach. Plik o nazwie *UpgradeLog.htm* zawierający raport migracji również jest automatycznie zapisywany i otwierany.

> [!IMPORTANT]
> W programie Visual Studio 2019 w wersji 16,3 i nowszych nie można załadować ani zmigrować pliku *. xproj* . Ponadto program Visual Studio 2015 nie zapewnia możliwości migrowania pliku *. xproj* . Jeśli używasz jednej z tych wersji programu Visual Studio, zainstaluj odpowiednią wersję programu Visual Studio lub użyj narzędzia migracji wiersza polecenia opisanego dalej.

### <a name="dotnet-migrate"></a>dotnet migrate

W scenariuszu wiersza polecenia można użyć [`dotnet migrate`](../tools/dotnet-migrate.md) polecenia. Migruje projekt, rozwiązanie lub zestaw folderów w tej kolejności, w zależności od tego, które zostały znalezione. Podczas migrowania projektu, projekt i wszystkie jego zależności są migrowane.

Pliki migrowane (*project.json*, *global.json*i *. xproj*) są przenoszone do folderu *kopii zapasowej* .

> [!NOTE]
> Jeśli używasz Visual Studio Code, `dotnet migrate` polecenie nie modyfikuje plików specyficznych dla Visual Studio Code, takich jak *tasks.js*. Te pliki należy zmienić ręcznie.
> Jest to również prawdziwe, jeśli używasz edytora lub zintegrowanego środowiska programistycznego (IDE) innego niż program Visual Studio.

Zapoznaj [się z mapowaniem między właściwościami project.jsna i csproj](../tools/project-json-to-csproj.md) , aby porównać *project.jsw* formatach i *. csproj* .

Jeśli wystąpi błąd:

> Nie znaleziono pliku wykonywalnego zgodnego z poleceniem dotnet-Migrowanie

Uruchom, `dotnet --version` Aby zobaczyć, której wersji używasz. [`dotnet migrate`](../tools/dotnet-migrate.md) został wprowadzony w zestaw .NET Core SDK 1.0.0 i usunięty w wersji 3.0.100.
Ten błąd zostanie wyświetlony, jeśli masz *global.jsw* pliku w bieżącym lub nadrzędnym katalogu, a wersja, którą `sdk` określisz, jest spoza tego zakresu.

## <a name="migration-from-dnx-to-csproj"></a>Migracja z środowiska DNX do csproj

Jeśli nadal używasz programu środowiska DNX do programowania w środowisku .NET Core, proces migracji powinien odbywać się w dwóch etapach:

1. Użyj [istniejących wskazówek dotyczących migracji środowiska DNX](from-dnx.md) , aby przeprowadzić migrację z środowiska DNX do interfejsu wiersza polecenia z włączonym kodem JSON.
2. Postępuj zgodnie z instrukcjami z poprzedniej sekcji, aby przeprowadzić migrację z *project.js* do *. csproj*.

> [!NOTE]
> ŚRODOWISKA DNX jest oficjalnie przestarzałe w wersji zapoznawczej 1 interfejs wiersza polecenia platformy .NET Core.

## <a name="migration-from-earlier-net-core-csproj-formats-to-rtm-csproj"></a>Migracja z wcześniejszych formatów programu .NET Core csproj do wersji RTM csproj

Format programu .NET Core csproj został zmieniony i rozwijający się za pomocą każdej nowej wersji wstępnej narzędzi. Nie ma narzędzia, które przeprowadzi migrację pliku projektu z wcześniejszych wersji csproj do najnowszej, więc musisz ręcznie edytować plik projektu. Rzeczywiste kroki zależą od wersji migrowanego pliku projektu. Poniżej znajdują się wskazówki, które należy wziąć pod uwagę w zależności od zmian, które wystąpiły między wersjami:

- Usuń właściwość wersja narzędzi z `<Project>` elementu, jeśli istnieje.
- Usuń przestrzeń nazw XML ( `xmlns` ) z `<Project>` elementu.
- Jeśli nie istnieje, Dodaj `Sdk` atrybut do `<Project>` elementu i ustaw go na `Microsoft.NET.Sdk` lub `Microsoft.NET.Sdk.Web` . Ten atrybut określa, że projekt używa zestawu SDK, który ma być używany. `Microsoft.NET.Sdk.Web` jest używany dla aplikacji sieci Web.
- Usuń `<Import Project="$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\Microsoft.Common.props" />` instrukcje i `<Import Project="$(MSBuildToolsPath)\Microsoft.CSharp.targets" />` z góry i u dołu projektu. Te instrukcje importu są implikowane przez zestaw SDK, więc nie ma potrzeby, aby były one w projekcie.
- Jeśli masz `Microsoft.NETCore.App` lub `NETStandard.Library` `<PackageReference>` elementy w projekcie, należy je usunąć. Te odwołania do pakietów są [implikowane przez zestaw SDK](../tools/csproj.md).
- Usuń `Microsoft.NET.Sdk` `<PackageReference>` element, jeśli istnieje. Odwołanie do zestawu SDK zawiera `Sdk` atrybut w `<Project>` elemencie.
- Usuń [elementy globalne](https://en.wikipedia.org/wiki/Glob_(programming)) , które są [implikowane przez zestaw SDK](../project-sdk/overview.md#default-compilation-includes). Pozostawienie tych elementy globalne w projekcie spowoduje wystąpienie błędu podczas kompilacji, ponieważ elementy kompilacji zostaną zduplikowane.

Po wykonaniu tych kroków projekt powinien być w pełni zgodny z formatem CSPROJ RTM platformy .NET Core.

Aby zapoznać się z przykładami przed i po migracji ze starego formatu csproj do nowego, zobacz artykuł [Aktualizacja programu Visual Studio 2017 RC — udoskonalenia narzędzi dla programu .NET Core](https://devblogs.microsoft.com/dotnet/updating-visual-studio-2017-rc-net-core-tooling-improvements/) w blogu platformy .NET.

## <a name="see-also"></a>Zobacz także

- [Przenoszenie, migrowanie i uaktualnianie projektów programu Visual Studio](/visualstudio/porting/port-migrate-and-upgrade-visual-studio-projects)
