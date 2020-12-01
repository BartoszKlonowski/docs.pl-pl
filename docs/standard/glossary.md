---
title: Słownik platformy .NET
description: Sprawdź znaczenie wybranych terminów używanych w dokumentacji programu .NET.
ms.date: 11/16/2020
ms.openlocfilehash: 77ed506fb1c5bd4018b5fe0c14cc0bf37cb08113
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96438190"
---
# <a name="net-glossary"></a>Słownik platformy .NET

Głównym celem tego słownika jest wyjaśnienie znaczenia wybranych terminów i akronimów, które często pojawiają się w dokumentacji programu .NET bez definicji.

## <a name="aot"></a>AOT

Kompilator przed czasem.

Podobnie jak w przypadku [JIT](#jit), ten kompilator tłumaczy również [Il](#il) na kod maszynowy. W przeciwieństwie do kompilacji JIT kompilacja AOT jest wykonywana przed wykonaniem aplikacji i zwykle jest wykonywana na innym komputerze. Ponieważ w czasie wykonywania nie są kompilowane łańcuchy narzędzi AOT, nie trzeba minimalizować czasu kompilowania. Oznacza to, że mogą oni poświęcać więcej czasu na optymalizację. Ponieważ kontekst AOT jest całą aplikacją, kompilator AOT wykonuje również łączenie między modułami i analizę całego programu, co oznacza, że wszystkie odwołania są obserwowane i tworzony jest pojedynczy plik wykonywalny.

Zobacz [CoreRT](#corert) i [.NET Native](#net-native).

## <a name="app-model"></a>model aplikacji

Interfejs API specyficzny dla [obciążenia](#workload). Oto kilka przykładów:

* ASP.NET
* ASP.NET Web API
* Entity Framework (EF)
* Windows Presentation Foundation (WPF)
* Windows Communication Foundation (WCF)
* Program Windows Workflow Foundation (WF)
* Windows Forms (WinForms)

## <a name="aspnet"></a>ASP.NET

Oryginalna implementacja ASP.NET, która jest dostarczana z .NET Framework.

Czasami ASP.NET jest terminem parasola, który odwołuje się do obu implementacji ASP.NET, w tym ASP.NET Core. Oznacza to, że termin odbywa się w każdym podanym wystąpieniu jest określony przez kontekstu. Zapoznaj się z ASP.NET 4. x, jeśli chcesz, aby było jasne, że nie używasz ASP.NET do oznaczania obu implementacji.

Zobacz [dokumentację ASP.NET](/aspnet/#pivot=aspnet).

## <a name="aspnet-core"></a>ASP.NET Core

Oparta na wielu platformach implementacja typu open source ASP.NET.

Zobacz [dokumentację ASP.NET Core](/aspnet/#pivot=core).

## <a name="assembly"></a>zestaw

Plik *. dll* / *. exe* , który może zawierać kolekcję interfejsów API, które mogą być wywoływane przez aplikacje lub inne zestawy.

Zestaw może zawierać typy, takie jak interfejsy, klasy, struktury, wyliczenia i Delegaty. Zestawy w folderze *bin* projektu są czasami określane jako *pliki binarne*. Zobacz również [Biblioteka](#library).

## <a name="bcl"></a>BCL

Biblioteka klas bazowych.

Zestaw bibliotek, które składają się na system. \* (i do ograniczonego zakresu firmy Microsoft \* ). przestrzeni. BCL jest ogólnym celem, na niższym poziomie, które platformy aplikacji wyższego poziomu, takie jak ASP.NET Core, Kompiluj na.

Kod źródłowy BCL dla [programu .NET 5 (i .NET Core) i nowszych wersji](#net-5-and-later-versions) znajduje się w [repozytorium środowiska uruchomieniowego platformy .NET](https://github.com/dotnet/runtime). Większość tych interfejsów API BCL są również dostępne w .NET Framework, więc można traktować ten kod źródłowy jako rozwidlenie kodu źródłowego .NET Framework BCL.

Poniższe terminy często odnoszą się do tej samej kolekcji interfejsów API, do których odnosi się BCL:

- [podstawowe biblioteki .NET](../core/compatibility/corefx.md)
- [biblioteki struktury](#framework-libraries)
- [biblioteki środowiska uruchomieniowego](#runtime)
- [współdzielona architektura](#shared-framework)

## <a name="clr"></a>CLR

Środowisko uruchomieniowe języka wspólnego.

Dokładne znaczenie zależy od kontekstu. Środowisko uruchomieniowe języka wspólnego dotyczy zazwyczaj środowiska uruchomieniowego [.NET Framework](#net-framework) lub środowiska uruchomieniowego programu [.NET 5 (oraz platformy .NET Core) i nowszych wersji](#net-5-and-later-versions).

Środowisko CLR obsługuje alokacje pamięci i zarządzanie nimi. Środowisko CLR jest również maszyną wirtualną, która nie tylko wykonuje aplikacje, ale również generuje i kompiluje kod na bieżąco przy użyciu kompilatora [JIT](#jit) .

Implementacja środowiska CLR dla .NET Framework jest tylko system Windows.

Implementacja środowiska CLR dla programu .NET 5 i nowszych wersji (znanej również jako rdzeń CLR) jest tworzona na podstawie tej samej bazy kodu co .NET Framework CLR. Początkowo środowisko uruchomieniowe programu Silverlight zostało zaprojektowane na wiele platform, w tym w systemach Windows i OS X. Nadal jest to środowisko uruchomieniowe dla wielu [platform](#cross-platform) , w tym teraz obsługiwane są różne dystrybucje systemu Linux.

Zobacz również [środowisko uruchomieniowe](#runtime).

## <a name="core-clr"></a>Podstawowe środowisko CLR

Środowisko uruchomieniowe języka wspólnego dla [programu .NET 5 (i .NET Core) i nowsze wersje](#net-5-and-later-versions).

Zobacz [CLR](#clr)

## <a name="corert"></a>CoreRT

W przeciwieństwie do [środowiska CLR](#clr)CoreRT nie jest maszyną wirtualną, co oznacza, że nie obejmuje ona obiektów do generowania i uruchamiania kodu na bieżąco, ponieważ nie zawiera on [JIT](#jit). Obejmuje to jednak funkcję [GC](#gc) i możliwość identyfikacji typu czasu wykonywania (RTTI) i odbicia. Jednak jego system typów został zaprojektowany tak, aby metadane odbicia nie były wymagane. Niewymaganie metadanych umożliwia korzystanie z łańcucha narzędzi [AOT](#aot) , który może łączyć zbędne metadane i (dokładniej) identyfikować kod nieużywany przez aplikację. CoreRT jest w trakcie opracowywania.

Zapoznaj [się z wprowadzeniem do .NET Native i CoreRT](https://github.com/dotnet/corert/blob/master/Documentation/intro-to-corert.md).

## <a name="cross-platform"></a>na wiele platform

Możliwość tworzenia i uruchamiania aplikacji, która może być używana w wielu różnych systemach operacyjnych, takich jak Linux, Windows i iOS, bez konieczności ponownego zapisywania dla każdej z nich. Umożliwia to ponowne użycie kodu i spójność między aplikacjami na różnych platformach.

## <a name="ecosystem"></a>uwolnieni

Wszystkie oprogramowanie środowiska uruchomieniowego, narzędzia programistyczne i zasoby społeczności, które są używane do kompilowania i uruchamiania aplikacji dla danej technologii.

Termin "ekosystem .NET" różni się od podobnych warunków, takich jak "stos .NET" w ramach dołączania do aplikacji i bibliotek innych firm. Oto przykład w zdaniu:

- "Motywacja za [.NET Standard](#net-standard) polega na ustanowieniu większej jednorodności w ekosystemie .NET".

## <a name="framework"></a>szablon

Ogólnie kompleksowe zbieranie interfejsów API, które ułatwiają tworzenie i wdrażanie aplikacji opartych na określonej technologii. W tym ogólnym sensie ASP.NET Core i Windows Forms są przykładami struktur aplikacji. Zobacz również [Biblioteka](#library).

Słowo "Framework" ma inne znaczenie w następujących warunkach:

- [biblioteki struktury](#framework-libraries)
- [.NET Framework](#net-framework)
- [współdzielona architektura](#shared-framework)
- [Platforma docelowa](#target-framework)
- [TFM (moniker struktury docelowej)](#tfm)
- [aplikacja zależna od struktury](../core/deploying/index.md#publish-framework-dependent)

Czasami "Framework" odnosi się do [implementacji platformy .NET](#implementation-of-net). Na przykład artykuł może wywoływać platformę .NET 5 a.

## <a name="framework-libraries"></a>biblioteki struktury

Znaczenie zależy od kontekstu. Może odwoływać się do bibliotek platformy [.NET 5 (i .NET Core) i nowszych](#net-5-and-later-versions), w takim przypadku odwołują się do tych samych bibliotek, do których odwołuje się [BCL](#bcl) . Może on również odnosić się do bibliotek ASP.NET Core Framework, które kompilują się w BCL i zapewniają dodatkowe interfejsy API dla aplikacji sieci Web.

## <a name="gc"></a>GC

Moduł zbierający elementy bezużyteczne.

Moduł wyrzucania elementów bezużytecznych jest implementacją automatycznego zarządzania pamięcią.  GC zwalnia pamięć zajętą przez obiekty, które nie są już używane.

Zobacz [odzyskiwanie pamięci](garbage-collection/index.md).

## <a name="il"></a>IL

Język pośredni.

Języki platformy .NET wyższego poziomu, takie jak C#, Kompiluj w dół do zestawu instrukcji niezależny od sprzętu, który jest nazywany językiem pośrednim (IL). Kod IL jest czasami określany jako MSIL (Microsoft IL) lub CIL (Common IL).

## <a name="jit"></a>JIT

Kompilator just in Time.

Podobnie jak w przypadku [drzewa AOT](#aot), ten kompilator tłumaczy [Il](#il) na kod maszynowy, który jest rozpoznawany przez procesor. W przeciwieństwie do drzewa AOT, kompilacja JIT odbywa się na żądanie i jest wykonywana na tym samym komputerze, na którym kod musi być uruchomiony. Ponieważ kompilacja JIT odbywa się podczas wykonywania aplikacji, czas kompilacji jest częścią czasu wykonywania. W efekcie kompilatory JIT muszą zrównoważyć czas spędzony na optymalizowaniu kodu przed oszczędnościami, które może wyprodukować ten kod. Jednak kompilator JIT wie o rzeczywistym sprzęcie i może zwolnić deweloperów, którzy muszą dostarczać różne implementacje.

## <a name="implementation-of-net"></a>Implementacja platformy .NET

Implementacja programu .NET obejmuje:

- Co najmniej jedno środowisko uruchomieniowe. Przykłady: [CLR](#clr), [CoreRT](#corert).
- Biblioteka klas implementująca wersję .NET Standard i może zawierać dodatkowe interfejsy API. Przykłady: [BCLs](#bcl) dla [.NET Framework](#net-framework) i [.NET 5 (oraz .NET Core) i nowszych](#net-5-and-later-versions).
- Opcjonalnie co najmniej jedna struktura aplikacji. Przykłady: [ASP.NET](#aspnet), Windows Forms i WPF są zawarte w .NET Framework i .NET 5.
- Opcjonalnie narzędzia programistyczne. Niektóre narzędzia programistyczne są współużytkowane przez wiele implementacji.

Przykłady implementacji platformy .NET:

- [.NET Framework](#net-framework)
- [.NET 5 i nowsze wersje (w tym .NET Core 2.1-3.1)](#net-5-and-later-versions)
- [Platforma uniwersalna systemu Windows (UWP)](#uwp)
- [Mono](#mono)

## <a name="library"></a>biblioteka

Kolekcja interfejsów API, które mogą być wywoływane przez aplikacje lub inne biblioteki. Biblioteka .NET składa się z co najmniej jednego [zestawu.](#assembly)

Słowa Library i [Framework](#framework) są często używane.

## <a name="mono"></a>Mono

Mono to [wieloplatformowa](#cross-platform) implementacja platformy .NET, która jest używana głównie w przypadku, gdy wymagane jest małe środowisko uruchomieniowe. Jest to środowisko uruchomieniowe, które umożliwia aplikacjom platformy Xamarin w systemach Android, Mac, iOS, systemu tvOS i systemu watchOS i koncentruje się głównie na aplikacjach, które wymagają małego rozmiaru.

Obsługuje ona wszystkie aktualnie opublikowane wersje .NET Standard.

W przeszłości, mono zaimplementowano większy interfejs API .NET Framework i emuluje niektóre z najpopularniejszych możliwości w systemie UNIX. Jest on czasami używany do uruchamiania aplikacji .NET, które są zależne od tych funkcji w systemie UNIX.

Mono jest zazwyczaj używany z [kompilatorem just-in-Time](#jit), ale również zawiera pełny [statyczny kompilator (kompilacja przed czasem)](#aot) , która jest używana na platformach takich jak iOS.

Zapoznaj się z [dokumentacją narzędzia mono](https://www.mono-project.com/docs/).

## <a name="net"></a>.NET

Termin parasol dla [.NET Standard](#net-standard) i wszystkie [implementacje i obciążenia platformy .NET](#implementation-of-net) . Zawsze w pełni skapitalizowane, nigdy ".NET".

Po wydaniu [programu .NET 5](#net-5-and-later-versions) (obecnie w wersji zapoznawczej) będzie to zalecana implementacja platformy .NET dla wszystkich nowych rozwiązań związanych z platformą .NET. w niektórych kontekstach ".NET" będzie oznaczać ".NET 5 i nowsze wersje".

Zobacz [.NET — podstawy](../fundamentals/index.yml)

## <a name="net-5-and-later-versions"></a>.NET 5 i nowsze wersje

Oparta na wielu platformach implementacja platformy .NET typu open source. Obejmuje środowisko uruchomieniowe języka wspólnego ([CLR](#clr)), środowisko uruchomieniowe [AOT](#aot) ([CoreRT](#corert), w trakcie tworzenia), podstawową bibliotekę klas ([BCL](#bcl)) i [zestaw .NET SDK](#net-sdk).

Wcześniejsze wersje tej implementacji platformy .NET są znane jako .NET Core. .NET 5,0 to następna wersja z programu .NET Core 3,1. Wersja 4 została pominięta, aby uniknąć pomyłki w tej nowszej implementacji platformy .NET ze starszą implementacją, która jest znana jako [.NET Framework](#net-framework). Bieżąca wersja .NET Framework to 4,8.

Zobacz [.NET Fundamentals](../fundamentals/index.yml).

## <a name="net-cli"></a>INTERFEJS WIERSZA POLECENIA PLATFORMY .NET

Międzyplatformowe łańcucha narzędzi do tworzenia aplikacji i bibliotek dla [platformy .NET 5 (oraz platformy .NET Core) i nowszych](#net-5-and-later-versions). Znana także jako interfejs wiersza polecenia platformy .NET Core.

Zobacz [interfejs wiersza polecenia platformy .NET](../core/tools/index.md).

## <a name="net-core"></a>.NET Core

Zobacz [.NET 5 i nowsze wersje](#net-5-and-later-versions).

## <a name="net-framework"></a>.NET Framework

Implementacja programu .NET, która działa tylko w systemie Windows. Obejmuje środowisko uruchomieniowe języka wspólnego ([CLR](#clr)), bibliotekę klas podstawowych ([BCL](#bcl)) i biblioteki struktury aplikacji, takie jak [ASP.NET](#aspnet), Windows Forms i WPF.

Zobacz [przewodnik .NET Framework](../framework/index.yml).

## <a name="net-native"></a>Architektura .NET Native

Łańcuch narzędzi kompilatora, który generuje kod natywny ([AOT](#aot)), w przeciwieństwie do just-in-Time ([JIT](#jit)).

Kompilacja odbywa się na komputerze dewelopera podobnym do sposobu działania kompilatora i konsolidatora języka C++. Usuwa nieużywany kod i poświęca więcej czasu na optymalizację. Wyodrębnia kod z bibliotek i scala je do pliku wykonywalnego. Wynikiem jest pojedynczy moduł, który reprezentuje całą aplikację.

PLATFORMY UWP była pierwszą platformą aplikacji obsługiwaną przez .NET Native. Teraz obsługujemy tworzenie natywnych aplikacji konsolowych dla systemów Windows, macOS i Linux.

Zobacz [wprowadzenie do .NET Native i CoreRT](https://github.com/dotnet/corert/blob/master/Documentation/intro-to-corert.md)

## <a name="net-sdk"></a>Zestaw SDK .NET

Zestaw bibliotek i narzędzi umożliwiających deweloperom tworzenie aplikacji i bibliotek platformy .NET dla [platformy .NET 5 (oraz platformy .NET Core) i nowszych wersji](#net-5-and-later-versions). Znana także jako zestaw .NET Core SDK.

Obejmuje [interfejs wiersza polecenia platformy .NET](#net-cli) do kompilowania aplikacji, bibliotek .NET i środowiska uruchomieniowego na potrzeby kompilowania i uruchamiania aplikacji oraz plików wykonywalnych dotnet (*dotnet.exe*), które uruchamiają polecenia CLI i uruchamiają aplikacje.

Zobacz [Omówienie zestawu SDK platformy .NET](../core/sdk.md).

## <a name="net-standard"></a>.NET Standard

Formalna Specyfikacja interfejsów API platformy .NET, które są dostępne w każdej implementacji platformy .NET.

Specyfikacja .NET Standard jest czasami nazywana biblioteką w dokumentacji. Ponieważ biblioteka zawiera implementacje interfejsu API, a nie tylko specyfikacje (interfejsy), nie prowadzi do wywołania .NET Standard "biblioteki".

Zobacz [.NET Standard](net-standard.md).

## <a name="ngen"></a>NGEN

Generowanie natywne (obraz).

Tę technologię można traktować jako trwały kompilator [JIT](#jit) . Zwykle kompiluje kod na komputerze, na którym wykonywany jest kod, ale kompilacja zwykle występuje w czasie instalacji.

## <a name="package"></a>package

Pakiet NuGet &mdash; lub tylko pakiet &mdash; to plik *. zip* z co najmniej jednym zestawem o tej samej nazwie wraz z dodatkowymi metadanymi, takimi jak nazwa autora.

Plik *. zip* ma rozszerzenie *. nupkg* i może zawierać elementy zawartości, takie jak pliki *. dll* i pliki *. XML* , do użycia z wieloma platformami i wersjami docelowymi. Po zainstalowaniu w aplikacji lub bibliotece odpowiednie zasoby są wybierane na podstawie platformy docelowej określonej przez aplikację lub bibliotekę. Elementy zawartości definiujące interfejs znajdują się w folderze *ref* , a zasoby, które definiują implementację, znajdują się w folderze *lib* .

## <a name="platform"></a>platforma

System operacyjny i sprzęt, na którym działa program, na przykład Windows, macOS, Linux, iOS i Android.

Poniżej przedstawiono przykłady użycia w zdaniach:

- ".NET Core to wieloplatformowa implementacja platformy .NET".
- "Profile PCL reprezentują platformy firmy Microsoft, a .NET Standard są niezależny od na platformę".

Starsza dokumentacja platformy .NET czasami używa "platformy .NET" do oznaczania [implementacji platformy .NET](#implementation-of-net) lub [stosu](#stack) .NET, w tym wszystkich implementacji. Oba te zastosowania mogą być pomylone z podstawowym (system operacyjny/sprzętowy) znaczeniem, więc spróbujemy uniknąć tych zastosowań.

"Platforma" ma inne znaczenie w frazie "platforma dewelopera", która odnosi się do oprogramowania, które udostępnia narzędzia i biblioteki do kompilowania i uruchamiania aplikacji. .NET to międzyplatformowa platforma deweloperskia typu open source umożliwiająca tworzenie wielu różnych typów aplikacji.

## <a name="runtime"></a>środowisko uruchomieniowe

Ogólnie rzecz biorąc, środowisko wykonawcze dla programu zarządzanego. System operacyjny jest częścią środowiska uruchomieniowego, ale nie należy do środowiska uruchomieniowego .NET. Poniżej przedstawiono kilka przykładów środowiska uruchomieniowego .NET w tym sensie:

- Środowisko uruchomieniowe języka wspólnego ([CLR](#clr))
- .NET Native (dla platformy UWP)
- Środowisko uruchomieniowe mono

Słowo "środowisko uruchomieniowe" ma inne znaczenie w niektórych kontekstach:

* *Środowisko uruchomieniowe .NET* na [stronie pobierania programu .NET 5,0](https://dotnet.microsoft.com/download/dotnet/5.0).

  Możesz pobrać *środowisko uruchomieniowe platformy .NET* lub inne środowiska uruchomieniowe, takie jak *środowisko uruchomieniowe ASP.NET Core*. *Środowisko uruchomieniowe* w tym wykorzystaniu to zestaw składników, które muszą być zainstalowane na komputerze, aby uruchomić aplikację [zależną od platformy](../core/deploying/index.md#publish-framework-dependent) na komputerze. Środowisko uruchomieniowe platformy .NET zawiera [środowisko CLR](#clr) i [współdzielone](#shared-framework)środowisko .NET, które udostępnia [BCL](#bcl).

* *Biblioteki środowiska uruchomieniowego platformy .NET*

  Odwołuje się do tych samych bibliotek, do których odwołuje się [BCL](#bcl) . Jednak inne środowiska uruchomieniowe, takie jak środowisko uruchomieniowe ASP.NET Core, mają różne [platformy udostępnione](#shared-framework), z dodatkowymi bibliotekami, które kompilują się na BCL.

* [Identyfikator środowiska uruchomieniowego (RID)](../core/rid-catalog.md).

  *Środowisko uruchomieniowe* to oznacza platformę systemu operacyjnego i architekturę procesora CPU, na której działa aplikacja .NET, na przykład: `linux-x64` .

* Czasami "środowisko uruchomieniowe" jest używane w sensie [implementacji platformy .NET](#implementation-of-net), jak w następujących przykładach:

  - "Różne środowiska uruchomieniowe platformy .NET implementują określone wersje .NET Standard. … Każda wersja środowiska uruchomieniowego .NET anonsuje najwyższą wersję .NET Standard obsługiwaną przez program... "
  - "Biblioteki, które są przeznaczone do uruchamiania w wielu środowiskach uruchomieniowych, powinny być ukierunkowane na tę platformę". (odwołujące się do .NET Standard)

## <a name="shared-framework"></a>współdzielona architektura

Znaczenie zależy od kontekstu. Platforma *udostępniona platformy .NET* odnosi się do bibliotek zawartych w [środowisku uruchomieniowym .NET](#runtime). W takim przypadku *współdzielona struktura* dla [platformy .NET 5 (i .NET Core) i nowszych wersji](#net-5-and-later-versions) odwołuje się do tych samych bibliotek, do których odwołuje się [BCL](#bcl) .

Istnieją inne struktury udostępnione. *ASP.NET Core Shared Framework* odnosi się do bibliotek zawartych w [środowisku uruchomieniowym ASP.NET Core](#runtime), które obejmują BCL oraz dodatkowe interfejsy API do użycia przez aplikacje sieci Web.

W przypadku [aplikacji zależnych od platformy](../core/deploying/index.md#publish-framework-dependent)współdzielona platforma składa się z bibliotek znajdujących się w zestawach zainstalowanych w folderze na komputerze, na którym jest uruchomiona aplikacja. W przypadku [aplikacji samodzielnych](../core/deploying/index.md#publish-self-contained)zestawy wspólnych struktur są dołączone do aplikacji.

Aby uzyskać więcej informacji, zobacz [głębokie szczegółowe w programie .NET Core — elementy podstawowe, część 2: współdzielona struktura](https://natemcmaster.com/blog/2018/08/29/netcore-primitives-2/).

## <a name="stack"></a>stack

Zestaw technologii programistycznych, które są używane razem do kompilowania i uruchamiania aplikacji.

"Stos .NET" odnosi się do .NET Standard i wszystkich implementacji platformy .NET. Fraza "stos platformy .NET" może odnosić się do jednej implementacji platformy .NET.

## <a name="target-framework"></a>Platforma docelowa

Kolekcja interfejsów API, na których opiera się aplikacja lub biblioteka platformy .NET.

Aplikacja lub biblioteka może kierować do wersji .NET Standard (na przykład .NET Standard 2,0), która jest specyfikacją standardowego zestawu interfejsów API we wszystkich implementacjach platformy .NET. Aplikacja lub biblioteka może być również ukierunkowana na wersję konkretnej implementacji platformy .NET, w takim przypadku uzyskuje dostęp do interfejsów API specyficznych dla implementacji. Na przykład aplikacja przeznaczona dla platformy Xamarin. iOS uzyskuje dostęp do otok interfejsu API systemu iOS dostarczonych przez platformę Xamarin.

W przypadku niektórych platform docelowych (na przykład .NET Framework) dostępne interfejsy API są definiowane przez zestawy, które są instalowane przez implementację .NET w systemie, który może obejmować interfejsy API platformy aplikacji (na przykład ASP.NET, WinForms). W przypadku platform docelowych opartych na pakietach (takich jak .NET Standard i .NET Core) interfejsy API platformy są definiowane przez pakiety zainstalowane w aplikacji lub bibliotece. W takim przypadku platforma docelowa niejawnie określa pakiet, który odwołuje się do wszystkich pakietów, które razem tworzą strukturę.

Zobacz [platformę docelową](frameworks.md).

## <a name="tfm"></a>TFM

Moniker platformy docelowej.

Standardowy format tokenu służący do określania docelowej platformy aplikacji lub biblioteki platformy .NET. Struktury docelowe są zwykle przywoływane przez krótką nazwę, na przykład `net462` . Long-form TFMs (na przykład. NETFramework, Version = 4.6.2) istnieje, ale nie są zwykle używane do określania platformy docelowej.

Zobacz [platformę docelową](frameworks.md).

## <a name="uwp"></a>Platforma UWP

platforma uniwersalna systemu Windows.

Implementacja platformy .NET, która jest używana do tworzenia nowoczesnych aplikacji i oprogramowania systemu Windows z obsługą dotykową dla Internet rzeczy (IoT). Ma ona na celu ujednolicenie różnych typów urządzeń docelowych, w tym komputerów, tabletów, telefonów, a nawet konsoli Xbox. Usługa platformy UWP udostępnia wiele usług, takich jak scentralizowany magazyn aplikacji, środowisko wykonawcze i zestaw interfejsów API systemu Windows, które mają być używane zamiast Win32 (WinRT). Aplikacje można napisać w językach C++, C#, Visual Basic i JavaScript. W przypadku korzystania z języka C# i Visual Basic interfejsy API platformy .NET są udostępniane przez platformę .NET 5 (i platformę .NET Core) i nowsze wersje.

## <a name="workload"></a>workload

Typ kogoś, kto kompiluje aplikację. Bardziej ogólny niż [model aplikacji](#app-model). Na przykład w górnej części każdej strony z dokumentacją platformy .NET, w tym ten, jest listą rozwijaną dla **obciążeń**, która umożliwia przełączenie do dokumentacji dotyczącej **sieci Web**, **urządzeń przenośnych**, **chmury**, **pulpitu** i **Machine Learning \& danych**.

W niektórych kontekstach *obciążenie* dotyczy kolekcji funkcji programu Visual Studio, które można zainstalować w celu obsługi określonego typu aplikacji. Aby zapoznać się z przykładem, zobacz [Wybieranie obciążenia](../core/install/windows.md#select-a-workload).

## <a name="see-also"></a>Zobacz też

- [Podstawy programu .NET](../fundamentals/index.yml)
- [Przewodnik programu .NET Framework](../framework/index.yml)
- [ASP.NET — Omówienie](/aspnet/index#pivot=aspnet)
- [Przegląd ASP.NET Core](/aspnet/index#pivot=core)
