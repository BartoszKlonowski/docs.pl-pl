---
title: Typowe architektury aplikacji internetowych
description: Tworzenie architektury nowoczesnych aplikacji sieci Web przy użyciu ASP.NET Core i platformy Azure | Poznaj typowe architektury aplikacji sieci Web
author: ardalis
ms.author: wiwagn
ms.date: 12/01/2020
ms.openlocfilehash: c9c593788d4cdbb5a1d4c57ac91880ef965f06fa
ms.sourcegitcommit: 45c7148f2483db2501c1aa696ab6ed2ed8cb71b2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/08/2020
ms.locfileid: "96851741"
---
# <a name="common-web-application-architectures"></a>Typowe architektury aplikacji internetowych

> "Jeśli sądzisz, że dobra architektura jest kosztowna, wypróbuj złą architekturę".
> _-Brian i Joseph Yoder_

Większość tradycyjnych aplikacji .NET jest wdrażana jako pojedyncze jednostki odpowiadające plikowi wykonywalnemu lub pojedynczej aplikacji sieci Web uruchomionej w ramach jednej domeny AppDomain usług IIS. To podejście jest najprostszym modelem wdrażania i jest bardzo dobrze obsługiwane w przypadku wielu wewnętrznych i mniejszych aplikacji publicznych. Jednak nawet w przypadku tej pojedynczej jednostki wdrożenia większość aplikacji nieuproszczonych korzysta z niektórych logicznych rozbarwień na kilku warstwach.

## <a name="what-is-a-monolithic-application"></a>Co to jest aplikacja monolityczna?

Aplikacja monolityczna to ta, która jest całkowicie niezależna, w warunkach jego działania. Może ona współdziałać z innymi usługami lub magazynami danych w trakcie wykonywania operacji, ale jego rdzeń jest uruchamiany w ramach własnego procesu, a cała aplikacja jest zwykle wdrażana jako pojedyncza jednostka. Jeśli taka aplikacja musi skalować w poziomie, zazwyczaj cała aplikacja jest duplikowana na wielu serwerach lub maszynach wirtualnych.

## <a name="all-in-one-applications"></a>Wszystkie aplikacje w jednym miejscu

Najmniejsza możliwa liczba projektów dla architektury aplikacji to jedna z nich. W tej architekturze Cała logika aplikacji jest zawarta w pojedynczym projekcie, skompilowana do jednego zestawu i wdrożona jako pojedyncza jednostka.

Nowy projekt ASP.NET Core, niezależnie od tego, czy został utworzony w programie Visual Studio, czy z wiersza polecenia, jest uruchamiany jako proste monolitu "All-in-one". Zawiera wszystkie zachowania aplikacji, w tym logiki dostępu do prezentacji, biznesowego i danych. Rysunek 5-1 przedstawia strukturę plików aplikacji pojedynczego projektu.

![Aplikacja ASP.NET Core pojedynczego projektu](./media/image5-1.png)

**Rysunek 5-1.** Pojedynczy projekt ASP.NET Core aplikacji.

W scenariuszu pojedynczego projektu rozdzielenie problemów odbywa się za pomocą folderów. Szablon domyślny zawiera oddzielne foldery dla obowiązków wzorca MVC dla modeli, widoków i kontrolerów, a także dodatkowe foldery dla danych i usług. W tym rozmieszczeniu szczegóły prezentacji powinny być ograniczone możliwie jak najwięcej do folderu widoki, a szczegóły implementacji dostępu do danych powinny być ograniczone do klas przechowywanych w folderze danych. Logika biznesowa powinna znajdować się w usługach i klasach w folderze modele.

Chociaż proste, jednoprojektowe rozwiązanie monolityczne ma pewne wady. Wraz ze wzrostem rozmiaru i złożoności projektu liczba plików i folderów nadal rośnie. Problemy związane z interfejsem użytkownika (modele, widoki, kontrolery) znajdują się w wielu folderach, które nie są pogrupowane w kolejności alfabetycznej. Ten problem występuje tylko wtedy, gdy dodatkowe konstrukcje poziomu interfejsu użytkownika, takie jak filters lub ModelBinders, są dodawane do własnych folderów. Logika biznesowa jest rozproszeni między modelami i folderami usług i nie istnieje jasne wskazanie klas, w których foldery powinny być zależne od innych. Brak organizacji na poziomie projektu często prowadzi do [kodu spaghetti](https://deviq.com/spaghetti-code/).

Aby rozwiązać te problemy, aplikacje często są rozłożone na rozwiązania obejmujące wiele projektów, w których każdy projekt jest traktowany jako znajdujący się w określonej _warstwie_ aplikacji.

## <a name="what-are-layers"></a>Co to są warstwy logiczne?

W miarę wzrostu złożoności aplikacji jeden ze sposobów zarządzania tą złożonością polega na rozdzieleniu aplikacji zależnie od jej obowiązków lub obaw. Takie podejście stosuje się do oddzielenia zasad i może pomóc w utrzymaniu zorganizowanej bazy kodu w taki sposób, aby deweloperzy mogli łatwo znajdować określone funkcje. Architektura warstwowa oferuje wiele korzyści poza organizacją kodu, chociaż.

Organizując kod na warstwy, typowe funkcje niskiego poziomu mogą być ponownie używane w całej aplikacji. To ponowne użycie jest korzystne, ponieważ oznacza to, że nie trzeba pisać kodu i ponieważ może on umożliwić standaryzację aplikacji w ramach jednej implementacji, zgodnie z zasadą [nie powtarzaj siebie (sucha)](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself) .

W przypadku architektury warstwowej aplikacje mogą wymuszać ograniczenia dotyczące tego, które warstwy mogą komunikować się z innymi warstwami. Ta architektura pomaga w osiągnięciu hermetyzacji. Po zmianie lub wymianie warstwy należy mieć wpływ tylko na te warstwy, które z nią pracują. Ograniczając warstwy, które są zależne od tego, które warstwy, wpływ zmian można zmniejszyć, tak aby jedna zmiana nie miała wpływu na całą aplikację.

Warstwy (i hermetyzacja) znacznie ułatwiają zamianę funkcji w aplikacji. Na przykład aplikacja może początkowo używać własnej SQL Server bazy danych do trwałości, ale później może zdecydować się na korzystanie z strategii trwałości opartej na chmurze lub jednej za interfejsem API sieci Web. Jeśli aplikacja prawidłowo hermetyzuje swoją implementację trwałości w warstwie logicznej, taka warstwa SQL Server może zostać zastąpiona przez nową, implementując ten sam interfejs publiczny.

Oprócz możliwości zamiany implementacji w odpowiedzi na przyszłe zmiany w wymaganiach, warstwy aplikacji mogą także ułatwić wymianę implementacji na potrzeby testowania. Zamiast konieczności pisania testów, które działają względem warstwy danych rzeczywistych lub warstwy interfejsu użytkownika aplikacji, te warstwy mogą zostać zastąpione w czasie testu przy użyciu fałszywych implementacji, które zapewniają znane odpowiedzi na żądania. Takie podejście zwykle sprawia, że testy znacznie ułatwiają pisanie i szybsze wykonywanie w porównaniu z uruchamianiem testów względem rzeczywistej infrastruktury aplikacji.

Warstwami logicznymi jest typowa technika ulepszania organizacji kodu w aplikacjach oprogramowania dla przedsiębiorstw. istnieje kilka sposobów, w których kod może być zorganizowany do warstw.

> [!NOTE]
 > _Warstwy_ reprezentują logiczne separacje w aplikacji. W przypadku, gdy logika aplikacji jest fizycznie dystrybuowana do oddzielnych serwerów lub procesów, te oddzielne elementy docelowe wdrożenia są określane jako _warstwy_. Jest to możliwe, i dość często, aby mieć aplikację N-warstwową, która jest wdrażana w jednej warstwie.

## <a name="traditional-n-layer-architecture-applications"></a>Tradycyjne aplikacje architektury "N-Layer"

Najbardziej powszechną organizacją logiki aplikacji do warstw przedstawiono na rysunku 5-2.

![Typowe warstwy aplikacji](./media/image5-2.png)

**Rysunek 5-2.** Typowe warstwy aplikacji.

Te warstwy są często skracane jako interfejs użytkownika, LOGIKI biznesowej (warstwa logiki biznesowej) i DAL (warstwa dostępu do danych). Korzystając z tej architektury, użytkownicy wysyłają żądania za pośrednictwem warstwy interfejsu użytkownika, które współdziałają tylko z LOGIKI biznesowej. LOGIKI biznesowej z kolei może wywoływać DAL dla żądań dostępu do danych. Warstwa interfejsu użytkownika nie powinna bezpośrednio wykonywać żadnych żądań do DAL, ani nie powinna być współpracująca z trwałością bezpośrednio za pośrednictwem innych metod. Podobnie LOGIKI biznesowej powinna współistnieć z trwałością, przechodząc przez DAL. W ten sposób każda warstwa ma własną dobrze znaną odpowiedzialność.

Jedną z wadą tego tradycyjnego podejścia do warstw jest to, że zależności czasu kompilacji są uruchamiane od góry do dołu. Oznacza to, że warstwa interfejsu użytkownika zależy od LOGIKI biznesowej, która zależy od DAL. Oznacza to, że LOGIKI biznesowej, który zwykle zawiera najważniejsze logiki w aplikacji, zależy od szczegółów implementacji dostępu do danych (i często w przypadku istnienia bazy danych). Testowanie logiki biznesowej w takiej architekturze jest często trudne i wymaga testowej bazy danych. Zasady Inversion dotyczącej zależności mogą służyć do rozwiązywania tego problemu, jak widać w następnej sekcji.

Na rysunku 5-3 przedstawiono przykładowe rozwiązanie, które dzieli aplikację na trzy projekty według odpowiedzialności (lub warstwy).

![Prosta aplikacja monolityczna z trzema projektami](./media/image5-3.png)

**Rysunek 5-3.** Prosta aplikacja monolityczna z trzema projektami.

Mimo że ta aplikacja korzysta z kilku projektów do celów organizacyjnych, nadal jest wdrażana jako jedna jednostka, a jej klienci będą korzystać z niej jako pojedynczej aplikacji sieci Web. Pozwala to na bardzo prosty proces wdrażania. Rysunek 5-4 pokazuje, jak taka aplikacja może być hostowana przy użyciu platformy Azure.

![Proste wdrażanie aplikacji sieci Web platformy Azure](./media/image5-4.png)

**Rysunek 5-4.** Proste wdrażanie aplikacji sieci Web platformy Azure

W miarę wzrostu potrzeb aplikacji mogą być wymagane bardziej złożone i niezawodne rozwiązania wdrożeniowe. Rysunek 5-5 przedstawia przykład bardziej złożonego planu wdrożenia, który obsługuje dodatkowe możliwości.

![Wdrażanie aplikacji sieci Web w Azure App Service](./media/image5-5.png)

**Rysunek 5-5.** Wdrażanie aplikacji sieci Web w Azure App Service

Wewnętrznie organizacja tego projektu w wielu projektach na podstawie odpowiedzialności usprawnia łatwość utrzymania aplikacji.

Tę jednostkę można skalować w górę lub w dół, aby korzystać z skalowalności na żądanie funkcji opartych na chmurze. Skalowanie w górę oznacza dodanie dodatkowego procesora CPU, pamięci, miejsca na dysku lub innych zasobów do serwerów obsługujących aplikację. Skalowanie w dół oznacza dodanie dodatkowych wystąpień takich serwerów, niezależnie od tego, czy są to serwery fizyczne, maszyny wirtualne czy kontenery. Gdy aplikacja jest hostowana w wielu wystąpieniach, moduł równoważenia obciążenia jest używany do przypisywania żądań do poszczególnych wystąpień aplikacji.

Najprostszym podejściem do skalowania aplikacji sieci Web na platformie Azure jest ręczne skonfigurowanie skalowania w planie App Service aplikacji. Rysunek 5-6 przedstawia odpowiedni ekran pulpitu nawigacyjnego platformy Azure, aby skonfigurować liczbę wystąpień obsługujących aplikację.

![Skalowanie planu App Service na platformie Azure](./media/image5-6.png)

**Rysunek 5-6.** Skalowanie planu App Service na platformie Azure.

## <a name="clean-architecture"></a>Czysta architektura

Aplikacje, które są zgodne z zasadą niezależności zależności, a także zasady projektowania Domain-Driven (DDD), które mają zostać przydzielone do podobnej architektury. Ta architektura została przełączona przez wiele nazw w latach. Jedna z pierwszych nazw była architekturą sześciokątną, a po niej porty i karty. Niedawno jest to zacytowane jako [Architektura cebuli](https://jeffreypalermo.com/blog/the-onion-architecture-part-1/) lub [czysta architektura](https://8thlight.com/blog/uncle-bob/2012/08/13/the-clean-architecture.html). Ta druga nazwa, czysta architektura, jest używana jako nazwa tej architektury w tej książce elektronicznej.

Aplikacja referencyjna eShopOnWeb korzysta z metody czystego architektury w organizowaniu kodu do projektów. Możesz znaleźć szablon rozwiązania, którego można użyć jako punktu wyjścia dla własnego ASP.NET Core w repozytorium GitHub [ardalis/cleanarchitecture](https://github.com/ardalis/cleanarchitecture) .

Czysty architektura powoduje umieszczenie logiki biznesowej i modelu aplikacji w centrum aplikacji. Zamiast mieć logikę biznesową zależą od dostępu do danych lub innych problemów związanych z infrastrukturą, ta zależność jest odwrócona: szczegóły infrastruktury i implementacji zależą od rdzenia aplikacji. Ta funkcja jest osiągana przez zdefiniowanie abstrakcji lub interfejsów w rdzeń aplikacji, które następnie są implementowane przez typy zdefiniowane w warstwie infrastruktury. Typowym sposobem wizualizacji tej architektury jest użycie serii okręgów koncentrycznych, podobnie jak w przypadku cebuli. Rysunek 5-7 pokazuje przykład tego stylu reprezentacji architektury.

![Czysta architektura; Widok cebuli](./media/image5-7.png)

**Rysunek 5-7.** Czysta architektura; Widok cebuli

Na tym diagramie zależności przepływu w kierunku najbardziej wewnętrznego okręgu. Rdzeń aplikacji przyjmuje swoją nazwę z pozycji na początku tego diagramu. Na diagramie można zobaczyć, że rdzeń aplikacji nie ma żadnych zależności od innych warstw aplikacji. Jednostki i interfejsy aplikacji są w bardzo wyśrodkowane. Po prostu poza, ale nadal w rdzeń aplikacji, są usługi domenowe, które zwykle implementują interfejsy zdefiniowane w okręgu wewnętrznym. Poza rdzeniem aplikacji zarówno interfejs użytkownika, jak i warstwy infrastruktury zależą od rdzenia aplikacji, ale nie na siebie (koniecznie).

Rysunek 5-8 pokazuje bardziej tradycyjny poziomy diagram warstwowy, który lepiej odzwierciedla zależność między interfejsem użytkownika a innymi warstwami.

![Czysta architektura; Widok warstwy poziomej](./media/image5-8.png)

**Rysunek 5-8.** Czysta architektura; Widok warstwy poziomej

Należy zauważyć, że pełne strzałki reprezentują zależności czasu kompilacji, natomiast strzałka kreskowana reprezentuje zależność tylko do wykonania. W przypadku czystej architektury warstwa interfejsu użytkownika współpracuje z interfejsami zdefiniowanymi w rdzeń aplikacji w czasie kompilacji i najlepiej nie należy wiedzieć o typach implementacji zdefiniowanych w warstwie infrastruktury. Jednak w czasie wykonywania, te typy implementacji są wymagane do wykonania aplikacji, dlatego muszą być obecne i rozłączone do interfejsów podstawowych aplikacji za pomocą iniekcji zależności.

Na rysunku 5-9 przedstawiono bardziej szczegółowy widok architektury aplikacji ASP.NET Core po skompilowaniu tych zaleceń.

![ASP.NET Core diagram architektury po czystej architekturze](./media/image5-9.png)

**Rysunek 5-9.** ASP.NET Core diagram architektury po czystej architekturze.

Ponieważ podstawowe aplikacje nie zależą od infrastruktury, bardzo proste jest zapisanie zautomatyzowanych testów jednostkowych dla tej warstwy. Ilustracje 5-10 i 5-11 pokazują, jak testy mieszczą się w tej architekturze.

![UnitTestCore](./media/image5-10.png)

**Rysunek 5-10.** Podstawowe testy jednostkowe aplikacji w izolacji.

![IntegrationTests](./media/image5-11.png)

**Rysunek 5-11.** Integracja polega na testowaniu implementacji infrastruktury z zależnościami zewnętrznymi.

Ze względu na to, że warstwa interfejsu użytkownika nie ma żadnej bezpośredniej zależności od typów zdefiniowanych w projekcie infrastruktury, można bardzo łatwo zamienić implementacje, aby ułatwić testowanie lub reagowanie na zmieniające się wymagania aplikacji. Wbudowana w ASP.NET Core funkcja i obsługa iniekcji zależności sprawia, że ta architektura jest najlepszym sposobem na strukturę nieuproszczonych aplikacji.

W przypadku aplikacji monolitycznych wszystkie projekty aplikacji, infrastruktury i interfejsu użytkownika są uruchamiane jako pojedyncze aplikacje. Architektura aplikacji środowiska uruchomieniowego może wyglądać podobnie do ilustracji 5-12.

![Architektura ASP.NET Core 2](./media/image5-12.png)

**Rysunek 5-12.** Przykładowa architektura środowiska uruchomieniowego aplikacji ASP.NET Core.

### <a name="organizing-code-in-clean-architecture"></a>Organizowanie kodu w czystej architekturze

W rozwiązaniu czystego architektury każdy projekt ma wyraźne obowiązki. W związku z tym niektóre typy należą do każdego projektu i często znajdują się foldery odpowiadające tym typom w odpowiednim projekcie.

#### <a name="application-core"></a>Rdzeń aplikacji

Rdzeń aplikacji zawiera model biznesowy, który obejmuje jednostki, usługi i interfejsy. Te interfejsy obejmują abstrakcje operacji, które będą wykonywane przy użyciu infrastruktury, takiej jak dostęp do danych, dostęp do systemu plików, wywołania sieciowe itp. Czasami usługi lub interfejsy zdefiniowane w tej warstwie muszą współdziałać z typami nienależącymi do jednostki, które nie są zależne od interfejsu użytkownika ani infrastruktury. Można je definiować jako proste Transfer danych obiekty (DTO).

##### <a name="application-core-types"></a>Typy podstawowe aplikacji

- Jednostki (utrwalone klasy modelu biznesowego)
- Interfejsy
- Usługi
- DTO

#### <a name="infrastructure"></a>Infrastruktura

Projekt infrastruktury zazwyczaj obejmuje implementacje dostępu do danych. W typowej aplikacji sieci Web ASP.NET Core te implementacje obejmują Entity Framework (EF) DbContext, wszystkie EF Core `Migration` obiekty, które zostały zdefiniowane, oraz klasy implementacji dostępu do danych. Najbardziej typowym sposobem na abstrakcyjny kod implementacji dostępu do danych jest użycie [wzorca projektowego repozytorium](https://deviq.com/repository-pattern/).

Oprócz implementacji dostępu do danych, projekt infrastruktury powinien zawierać implementacje usług, które muszą wchodzić w skład z obaw związanych z infrastrukturą. Te usługi powinny implementować interfejsy zdefiniowane w rdzeniu aplikacji, a więc infrastruktura powinna mieć odwołanie do projektu podstawowego aplikacji.

##### <a name="infrastructure-types"></a>Typy infrastruktury

- Typy EF Core ( `DbContext` , `Migration` )
- Typy implementacji dostępu do danych (repozytoria)
- Usługi specyficzne dla infrastruktury (na przykład `FileLogger` lub `SmtpNotifier` )

#### <a name="ui-layer"></a>Warstwa interfejsu użytkownika

Warstwa interfejsu użytkownika w aplikacji ASP.NET Core MVC jest punktem wejścia dla aplikacji. Ten projekt powinien odwoływać się do projektu podstawowego aplikacji, a jego typy powinny współdziałać z infrastrukturą przez interfejsy zdefiniowane w podstawowym aplikacji. W warstwie interfejsu użytkownika nie powinny być dozwolone żadne bezpośrednie wystąpienia ani statyczne wywołania do typów warstw infrastruktury.

##### <a name="ui-layer-types"></a>Typy warstw interfejsu użytkownika

- Kontrolery
- Filtry
- Widoki
- Modele widoków
- Uruchamianie

Klasa startowa jest odpowiedzialna za skonfigurowanie aplikacji oraz w celu zapewnienia obsługi typów implementacji w interfejsach, co pozwala na prawidłowe działanie iniekcji zależności w czasie wykonywania.

> [!NOTE]
> Aby można było połączyć iniekcję zależności w ConfigureServices w pliku Startup.cs projektu interfejsu użytkownika, projekt może wymagać odniesienia do projektu infrastruktury. Tę zależność można wyeliminować, najłatwiej przy użyciu niestandardowego kontenera DI. Na potrzeby tego przykładu najprostszym podejściem jest umożliwienie projektowi interfejsu użytkownika odwoływania się do projektu infrastruktury.

## <a name="monolithic-applications-and-containers"></a>Monolityczne aplikacje i kontenery

Można utworzyć pojedynczą i monolityczną aplikację sieci Web lub usługę opartą na wdrożeniu, a następnie wdrożyć ją jako kontener. W aplikacji może nie być lity, ale zorganizowany w kilka bibliotek, składników ani warstw. Zewnętrznie jest to pojedynczy kontener, taki jak pojedynczy proces, pojedyncza aplikacja internetowa lub jedna usługa.

Aby zarządzać tym modelem, należy wdrożyć pojedynczy kontener do reprezentowania aplikacji. Aby skalować, po prostu Dodaj dodatkowe kopie przy użyciu modułu równoważenia obciążenia. Prostota pochodzi z zarządzania pojedynczym wdrożeniem w jednym kontenerze lub maszynie wirtualnej.

![Rysunek 5-13](./media/image5-13.png)

W każdym kontenerze można uwzględnić wiele składników/bibliotek lub warstwy wewnętrzne, jak pokazano na rysunku 5-13. Jednak zgodnie z zasadą kontenera _"kontener wykonuje jedną czynność i robi to w jednym procesie_", wzorzec monolityczny może stanowić konflikt.

Minusem tego podejścia ma miejsce, gdy aplikacja zostanie powiększona, co wymaga jego skalowania. Jeśli cała aplikacja jest skalowana, problem nie występuje. Jednak w większości przypadków kilka części aplikacji to punkty podlewki wymagające skalowania, a inne składniki są mniej.

Przy użyciu typowego przykładu handlu elektronicznego, co jest potrzebne do skalowania, to składnik informacji o produkcie. Wielu więcej klientów przegląda produkty od ich zakupu. Więcej klientów korzysta z koszyka niż w przypadku korzystania z potoku płatności. Mniejsza liczba klientów umożliwia dodanie komentarzy lub wyświetlenie ich historii zakupów. Najkorzystniej masz kilku pracowników w jednym regionie, który musi zarządzać kampanią zawartości i kampanii marketingowej. Poprzez skalowanie projektu monolitycznego cały kod jest wdrażany wiele razy.

Oprócz problemu "Skaluj wszystko" zmiany w pojedynczym składniku wymagają pełnego przetestowania całej aplikacji oraz całkowitego ponownego wdrożenia wszystkich wystąpień.

Podejście monolityczne jest wspólne, a wiele organizacji opracowuje w ramach tego podejścia do architektury. Wiele z nich ma wystarczającą ilość wyników, a inne to limity. Wiele zaprojektowanych aplikacji w tym modelu, ponieważ narzędzia i infrastruktura były zbyt trudne do budowania architektury zorientowanej na usługi (SOA) i nie widzą potrzeb, dopóki aplikacja nie przezwiększyła się. Jeśli okaże się, że zbliżasz się do ograniczeń podejścia monolitycznego, Podziel aplikację, aby umożliwić jej lepsze wykorzystanie kontenerów i mikrousług.

![Rysunek 5-14](./media/image5-14.png)

Wdrażanie aplikacji monolitycznych w Microsoft Azure można osiągnąć przy użyciu dedykowanych maszyn wirtualnych dla każdego wystąpienia. Za pomocą [usługi Azure Virtual Machine Scale Sets](/azure/virtual-machine-scale-sets/)można łatwo skalować maszyny wirtualne. [Usługa Azure App Services](https://azure.microsoft.com/services/app-service/) może uruchamiać aplikacje monolityczne i łatwo skalować wystąpienia bez potrzeby zarządzania maszynami wirtualnymi. Usługa Azure App Services może również uruchamiać pojedyncze wystąpienia kontenerów platformy Docker, upraszczając wdrażanie. Przy użyciu platformy Docker można wdrożyć pojedynczą maszynę wirtualną jako hosta platformy Docker i uruchamiać wiele wystąpień. Korzystając z modułu równoważenia obciążenia platformy Azure, jak pokazano na rysunku 5-14, można zarządzać skalowaniem.

Wdrożenie na różnych hostach może być zarządzane przy użyciu tradycyjnych technik wdrażania. Hosty platformy Docker mogą być zarządzane za pomocą poleceń, takich jak **uruchomienie platformy Docker** , wykonywane ręcznie lub za pomocą automatyzacji, takich jak potoki ciągłego dostarczania (CD).

### <a name="monolithic-application-deployed-as-a-container"></a>Aplikacja monolityczna wdrożona jako kontener

Istnieją zalety używania kontenerów do zarządzania wdrożeniami aplikacji monolitycznych. Skalowanie wystąpień kontenerów jest znacznie szybsze i łatwiejsze niż wdrażanie dodatkowych maszyn wirtualnych. Nawet w przypadku używania zestawów skalowania maszyn wirtualnych do skalowania maszyn wirtualnych trwają one czas. W przypadku wdrożenia jako wystąpienia aplikacji Konfiguracja aplikacji jest zarządzana w ramach maszyny wirtualnej.

Wdrażanie aktualizacji jako obrazów platformy Docker odbywa się znacznie szybciej i wydajniej. Obrazy platformy Docker zwykle zaczynają się w ciągu sekund, co przyspiesza wprowadzanie. Przerywanie wystąpienia platformy Docker jest tak proste jak wydawanie `docker stop` polecenia, zwykle kończącego się w mniej niż drugim.

Ponieważ kontenery są z natury niezmienne przez zaprojektowanie, nigdy nie trzeba martwić się o uszkodzone maszyny wirtualne, natomiast skrypty aktualizacji mogą zapomnieć, że dla konkretnej konfiguracji lub pliku pozostawiono na dysku.

Kontenerów platformy Docker można używać do monolitycznego wdrażania prostszych aplikacji sieci Web. Takie podejście ulepsza ciągłą integrację i ciągłe wdrażanie potoków, a następnie pomaga osiągnąć sukces wdrożenia do produkcji. Nie ma więcej "działa na mojej maszynie, dlaczego nie działa w środowisku produkcyjnym?"

Architektura oparta na mikrousługach ma wiele korzyści, ale te korzyści mają na celu zwiększenie złożoności. W niektórych przypadkach koszty te zwiększają korzyści, więc jest to lepsza aplikacja do wdrożenia działająca w jednym kontenerze lub w zaledwie kilku kontenerach.

Aplikacja monolityczna może nie być łatwo można jej przetworzyć w dobrze rozdzielonych mikrousługach. Mikrousługi powinny działać niezależnie od siebie, aby zapewnić bardziej odporną aplikację. Jeśli nie można dostarczyć niezależnych wycinków funkcji aplikacji, oddzielenie go tylko zwiększa złożoność.

Aplikacja może jeszcze nie mieć możliwości skalowania funkcji niezależnie. Wiele aplikacji, gdy wymagają skalowania poza pojedynczym wystąpieniem, może to zrobić za pomocą stosunkowo prostego procesu klonowania całego wystąpienia. Dodatkowa służba do rozdzielania aplikacji na osobne usługi zapewniają minimalną korzyść, gdy skalowanie pełnych wystąpień aplikacji jest proste i ekonomiczne.

Na wczesnym etapie opracowywania aplikacji może nie mieć jasnego pomysłu, w którym naturalne granice funkcjonalności są. Podczas opracowywania minimalnego produktu, którego oddzielenie prawdopodobnie nie zostało jeszcze wykonane. Niektóre z tych warunków mogą być tymczasowe. Można zacząć od utworzenia aplikacji monolitycznej i późniejszego oddzielenia niektórych funkcji, które mają być opracowane i wdrożone jako mikrousługi. Inne warunki mogą być niezbędne w przypadku problemów z aplikacją, co oznacza, że aplikacja może nigdy nie być uszkodzona w wielu mikrousługach.

Rozdzielenie aplikacji na wiele procesów dyskretnych powoduje również zwiększenie nakładu pracy. Istnieje większa złożoność oddzielająca funkcje do różnych procesów. Protokoły komunikacyjne stają się bardziej skomplikowane. Zamiast wywołań metod, należy używać komunikacji asynchronicznej między usługami. Podczas przechodzenia do architektury mikrousług należy dodać wiele bloków konstrukcyjnych zaimplementowanych w wersji mikrousług aplikacji eShopOnContainers: obsługa magistrali zdarzeń, odporność na wiadomości i ponawianie prób, spójność ostateczna i inne.

Znacznie prostsze [aplikacje referencyjne eShopOnWeb](https://github.com/dotnet-architecture/eShopOnWeb) obsługują użycie kontenerów monolitycznych jednego kontenera. Aplikacja zawiera jedną aplikację sieci Web, która zawiera tradycyjne widoki MVC, interfejsy API sieci Web i Razor Pages. Ta aplikacja może być uruchamiana z poziomu głównego rozwiązania przy `docker-compose build` użyciu `docker-compose up` poleceń i. To polecenie umożliwia skonfigurowanie kontenera dla wystąpienia sieci Web przy użyciu `Dockerfile` znalezionego w katalogu głównym projektu sieci Web i uruchomienie kontenera na określonym porcie. Możesz pobrać źródło dla tej aplikacji z usługi GitHub i uruchomić ją lokalnie. Nawet ta monolityczna aplikacja nie będzie wdrażana w środowisku kontenera.

W przypadku jednego z kontenerów wdrożenie to oznacza, że każde wystąpienie aplikacji działa w tym samym środowisku. To podejście obejmuje środowisko deweloperskie, w którym odbywa się wczesne testowanie i programowanie. Zespół programistyczny może uruchomić aplikację w środowisku kontenerów, które pasuje do środowiska produkcyjnego.

Ponadto aplikacje kontenera są skalowane z niższym kosztem. Użycie środowiska kontenera pozwala zwiększyć udostępnianie zasobów niż tradycyjne środowiska maszyn wirtualnych.

Na koniec konteneryzowania aplikacja wymusza rozdzielenie między logiką biznesową a serwerem magazynu. W miarę skalowania aplikacji, wiele kontenerów będzie polegać na jednym fizycznym nośniku magazynowania. Ten nośnik magazynu zazwyczaj jest serwerem o wysokiej dostępności z uruchomioną SQL Server bazą danych.

## <a name="docker-support"></a>Obsługa platformy Docker

`eShopOnWeb`Projekt jest uruchamiany na platformie .NET. W związku z tym może działać w kontenerach opartych na systemie Linux lub Windows. Należy pamiętać, że w przypadku wdrożenia platformy Docker chcesz użyć tego samego typu hosta dla SQL Server. Kontenery oparte na systemie Linux umożliwiają mniejsze rozmiary i są preferowane.

Aby dodać obsługę platformy Docker do istniejącej aplikacji, można użyć programu Visual Studio 2017 lub nowszego, klikając prawym przyciskiem myszy projekt w **Eksplorator rozwiązań** i wybierając polecenie **Dodaj**  >  **obsługę platformy Docker**. Ten krok powoduje dodanie plików wymaganych i zmodyfikowanie projektu w celu ich użycia. Bieżący `eShopOnWeb` przykład ma już te pliki.

Plik poziomu rozwiązania `docker-compose.yml` zawiera informacje o obrazach do skompilowania oraz o kontenerach do uruchomienia. Plik umożliwia używanie `docker-compose` polecenia do uruchamiania wielu aplikacji w tym samym czasie. W tym przypadku uruchamia tylko projekt sieci Web. Można go również użyć do skonfigurowania zależności, takich jak oddzielny kontener bazy danych.

```yml
version: '3'

services:
  eshopwebmvc:
    image: eshopwebmvc
    build:
      context: .
      dockerfile: src/Web/Dockerfile
    environment:
      - ASPNETCORE_ENVIRONMENT=Development
    ports:
      - "5106:5106"

networks:
  default:
    external:
      name: nat
```

`docker-compose.yml`Plik odwołuje się do `Dockerfile` `Web` projektu. Służy `Dockerfile` do określenia, który kontener bazowy będzie używany, oraz sposobu ich konfiguracji. `Web`" `Dockerfile` :

```dockerfile
FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /app

COPY *.sln .
COPY . .
WORKDIR /app/src/Web
RUN dotnet restore

RUN dotnet publish -c Release -o out

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS runtime
WORKDIR /app
COPY --from=build /app/src/Web/out ./

ENTRYPOINT ["dotnet", "Web.dll"]
```

### <a name="troubleshooting-docker-problems"></a>Rozwiązywanie problemów z platformą Docker

Po uruchomieniu aplikacji kontenera nadal będzie ona działać do momentu jej zatrzymania. Możesz zobaczyć, które kontenery są uruchomione przy użyciu `docker ps` polecenia. Można zatrzymać uruchomiony kontener przy użyciu `docker stop` polecenia i OKREŚLAJĄC identyfikator kontenera.

Należy pamiętać, że uruchomione kontenery platformy Docker mogą być powiązane z portami, z których możesz próbować korzystać w środowisku deweloperskim. W przypadku próby uruchomienia lub debugowania aplikacji przy użyciu tego samego portu co uruchomiony kontener platformy Docker zostanie wyświetlony komunikat o błędzie informujący o tym, że serwer nie może powiązać z tym portem. Po ponownym zatrzymywaniu kontenera należy rozwiązać ten problem.

Jeśli chcesz dodać obsługę platformy Docker do aplikacji przy użyciu programu Visual Studio, upewnij się, że program Docker Desktop jest uruchomiony, gdy to zrobisz. Kreator nie będzie działać prawidłowo, jeśli program Docker Desktop nie zostanie uruchomiony po uruchomieniu kreatora. Ponadto Kreator sprawdza bieżący kontener, aby dodać poprawną obsługę platformy Docker. Aby dodać obsługę kontenerów systemu Windows, należy uruchomić kreatora, gdy jest uruchomiony pulpit Docker z skonfigurowanymi kontenerami systemu Windows. Jeśli chcesz dodać, obsłużyć kontenery systemu Linux, uruchom kreatora, gdy zainstalowano Aparat Docker z skonfigurowanymi kontenerami systemu Linux.

### <a name="references--common-web-architectures"></a>Odwołania — wspólne architektury sieci Web

- **Czysta architektura**  
  <https://8thlight.com/blog/uncle-bob/2012/08/13/the-clean-architecture.html>
- **Architektura cebuli**  
  <https://jeffreypalermo.com/blog/the-onion-architecture-part-1/>
- **Wzorzec repozytorium**  
  <https://deviq.com/repository-pattern/>
- **Szablon rozwiązania czystego architektury**  
  <https://github.com/ardalis/cleanarchitecture>
- **Tworzenie architektury książki elektronicznej mikrousług**  
  <https://aka.ms/MicroservicesEbook>
- **DDD (Projektowanie oparte na domenie)**  
  <https://docs.microsoft.com/dotnet/architecture/microservices/microservice-ddd-cqrs-patterns/>

>[!div class="step-by-step"]
>[Poprzedni](architectural-principles.md) 
> [Dalej](common-client-side-web-technologies.md)
