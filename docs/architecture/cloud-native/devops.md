---
title: DevOps
description: DevOps uwagi dotyczące aplikacji natywnych w chmurze
ms.date: 05/13/2020
ms.openlocfilehash: 1a04f5178877f3fdde707753e94718ce0f0bb49d
ms.sourcegitcommit: 635a0ff775d2447a81ef7233a599b8f88b162e5d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/17/2020
ms.locfileid: "97633718"
---
# <a name="devops"></a>DevOps

Ulubiony mantrą konsultantów oprogramowania ma na celu odpowiedzenie "jest to zależne" z wszelkimi powodowanymi pytaniami. Nie wynika to z faktu, że konsultanci Fond nie pobierają pozycji. Wynika to z faktu, że nie ma żadnej prawdziwej odpowiedzi na pytania w oprogramowaniu. Nie ma bezwzględnych praw i nieprawidłowych, ale raczej równowagi między przeciwieństwem.

Na przykład dwa główne szkoły tworzenia aplikacji sieci Web: aplikacje jednostronicowe (aplikacji jednostronicowych) i aplikacje po stronie serwera. Z jednej strony środowisko użytkownika będzie lepiej aplikacji jednostronicowych i ilość ruchu sieciowego do serwera sieci Web może być zminimalizowana, co umożliwia hostowanie ich w taki sposób, jak hosting statyczny. Z drugiej strony aplikacji jednostronicowych się coraz wolniej, aby rozwijać i utrudniać ich testowanie. Który z nich jest odpowiedni wybór? Jest to również zależne od sytuacji.

Aplikacje natywne w chmurze nie są odporne na te same dichotomy. Mają jasne zalety w zakresie rozwoju, stabilności i skalowalności, ale zarządzanie nimi może być nieco trudniejsze.

Lata temu nie było nietypowego dla procesu przechodzenia aplikacji z programowania do produkcji w ciągu miesiąca lub jeszcze więcej. Firmy wydały oprogramowanie w 6-miesięcznym lub nawet każdym roku erze. Jeden z nich musi wyszukać nie więcej niż Microsoft Windows, aby uzyskać pomysł na erze wydań, które były akceptowalne przed zielonymi dniami systemu Windows 10. Pięć lat przeszedł między Windows XP i Vista, a kolejne 3 między Vista a Windows 7.

Teraz dość dobrze jest ustalić, że umożliwienie szybszego wydawania oprogramowania pozwala na szybkie przechodzenie firm do znacznie większej liczby Sloth konkurentów. Z tego powodu wszystkie aktualizacje systemu Windows 10 są teraz co sześć miesięcy.

Wzorce i praktyki, które umożliwiają szybsze, bardziej niezawodne wydania do dostarczania wartości do firmy, są określane zbiorczo jako DevOps. Składają się one z szerokiego zakresu pomysłów obejmujących cały cykl życia opracowywania oprogramowania od określania aplikacji w taki sposób, aby można było dostarczać i obdziałać tę aplikację.

DevOpse przed mikrousługami i prawdopodobne jest, że przemieszczanie się w kierunku mniejszych usług nie byłoby możliwe bez DevOps, aby zwolnić i obsłużyć nie tylko jedną, ale wiele aplikacji w środowisku produkcyjnym.

![Rysunek 10-1 trendów wyszukiwania pokazuje, że wzrost w mikrousługach nie rozpoczyna się do momentu, gdy DevOps jest dość dobrze ustalone.](./media/microservices-vs-devops.png)

**Rysunek 10-1** -DevOps i mikrousługi.

Dzięki dobrym praktykom DevOpsm można korzystać z zalet aplikacji natywnych w chmurze, bez suffocating w ramach góry pracy, która faktycznie działa z aplikacjami.

Brak złotej młota, gdy DevOps. Nikt nie może sprzedawać kompletnych i wszystkich rozwiązań obejmujących wydawanie i obsługę wysokiej jakości aplikacji. Wynika to z faktu, że każda aplikacja różni się od wszystkich innych. Jednak dostępne są narzędzia, które mogą DevOps znacznie mniej zniechęcające propozycji. Jeden z tych narzędzi jest znany jako Azure DevOps.

## <a name="azure-devops"></a>Azure DevOps

Usługa Azure DevOps ma długotrwałe rodowody. Może śledzić swoje katalogi główne z powrotem do momentu Team Foundation Server po raz pierwszy przeniesiona w tryb online i przy użyciu różnych zmian nazw: Visual Studio Online i Visual Studio Team Services. W latach, jednak stała się znacznie większa niż jego poprzedniki.

Usługa Azure DevOps jest podzielona na pięć głównych składników:

![Rysunek 10-2 pięć głównych obszarów usługi Azure DevOps](./media/devops-components.png)

**Rysunek 10-2** — Azure DevOps.

**Azure Repos** — Zarządzanie kodem źródłowym, które obsługuje Venerable Kontrola wersji serwera Team Foundation (TFVC) oraz ulubioną w branży usługę [git](https://en.wikipedia.org/wiki/Git). Żądania ściągnięcia umożliwiają umożliwienie kodowania społecznościowego poprzez wspieranie dyskusji o zmianach w miarę ich wprowadzania.

**Azure Boards** — zawiera narzędzie do śledzenia problemu i elementów roboczych, które ma na celu umożliwienie użytkownikom wyboru przepływów pracy, które najlepiej odpowiadają. Zawiera ona wiele wstępnie skonfigurowanych szablonów, w tym te, które obsługują style SCRUM i Kanban rozwoju.

**Azure Pipelines** — system zarządzania kompilacjami i wydaniami, który obsługuje ścisłą integrację z platformą Azure. Kompilacje można uruchamiać na różnych platformach z systemu Windows do Linux do MacOS. Agenci kompilacji mogą być obsługiwani w chmurze lub lokalnie.

**Azure test Plans** — żadna osoba odpowiedzialna za zarządzanie testami i testowanie poznawcze oferowane przez funkcję test Plans nie zostanie pozostawione.

**Azure Artifacts** — Źródło artefaktów, które umożliwia firmom tworzenie własnych, wewnętrznych, wersji NuGet, npm i innych. W przypadku niepowodzenia scentralizowanego repozytorium działa jako pamięć podręczna pakietów nadrzędnych.

Jednostka organizacyjna najwyższego poziomu w usłudze Azure DevOps jest nazywana projektem. W każdym projekcie różne składniki, takie jak Azure Artifacts, można włączać i wyłączać. Każdy z tych składników oferuje różne zalety aplikacji natywnych w chmurze. Trzy najbardziej przydatne są repozytoria, tablice i potoki. Jeśli użytkownicy chcą zarządzać kodem źródłowym w innym stosie repozytorium, takim jak GitHub, ale nadal korzystają z Azure Pipelines i innych składników, to doskonale możliwe.

Na szczęście zespoły deweloperów mają wiele opcji podczas wybierania repozytorium. Jednym z nich jest serwis GitHub.

## <a name="github-actions"></a>Funkcja GitHub Actions

2009 w witrynie GitHub jest to szeroko popularne repozytorium oparte na sieci Web służące do hostowania projektów, dokumentacji i kodu. Wiele dużych firm technicznych, takich jak Apple, Amazon, Google i Large Corporation, korzysta z usługi GitHub. Usługa GitHub używa rozproszonego systemu kontroli wersji (Open Source) o nazwie git jako podstawy. Następnie dodaje swój własny zestaw funkcji, w tym śledzenie defektów, żądania funkcji i żądań ściągnięcia, zarządzanie zadaniami i wiki dla każdej bazy kodu.

W miarę rozwoju usługi GitHub jest również dodawana funkcja DevOps. Na przykład usługa GitHub ma własne potoki ciągłej integracji/ciągłego dostarczania (CI/CD) o nazwie `GitHub Actions` . Akcje GitHub to narzędzie do automatyzacji przepływu pracy, które jest obsługiwane przez społeczność. Umożliwia zespołom DevOps integrację z istniejącymi narzędziami, mieszanie i dopasowywanie nowych produktów oraz Podłączanie do ich cyklu życia oprogramowania, w tym istniejących partnerów CI/CD.

Serwis GitHub ma ponad 40 000 000 użytkowników, co sprawia, że jest to największy Host kodu źródłowego na świecie. W październiku 2018 firma Microsoft zakupiła witrynę GitHub. Firma Microsoft zabrała, że usługa GitHub pozostanie [otwartą platformą](https://techcrunch.com/2018/06/04/microsoft-promises-to-keep-github-independent-and-open/) , którą każdy deweloper może podłączyć i zwiększyć. Nadal działa jako niezależna firma. Serwis GitHub oferuje plany dotyczące kont przedsiębiorstwa, zespołów, profesjonalnych i bezpłatnych.

## <a name="source-control"></a>Kontrola źródła

Organizacja kodu dla aplikacji natywnej w chmurze może być wyzwaniem. Zamiast pojedynczej aplikacji bardzo duże aplikacje natywne w chmurze składają się z sieci Web mniejszych aplikacji, które komunikują się ze sobą. Podobnie jak w przypadku wszystkich rzeczy na platformie obliczeniowej, najlepszym rozwiązaniem kodu pozostaje otwarte pytanie. Istnieją przykłady pomyślnych aplikacji korzystających z różnych rodzajów układów, ale dwie odmiany wydają się mieć największą popularność.

Przed przystąpieniem do rzeczywistej kontroli źródła, prawdopodobnie warto określić liczbę projektów, które są odpowiednie. W jednym projekcie jest obsługiwana obsługa wielu repozytoriów i potoków kompilacji. Tablice są nieco bardziej skomplikowane, ale zbyt wiele zadań można łatwo przypisać do wielu zespołów w ramach pojedynczego projektu. Istnieje możliwość obsługi setek, nawet tysięcy deweloperów, z jednego projektu usługi Azure DevOps. Jest to prawdopodobnie najlepszym podejściem, ponieważ zapewnia to pojedyncze miejsce, dla którego wszyscy deweloperzy nie mogą pracować, i zmniejszają problemy z znalezieniem, że jedna aplikacja nie ma pewności, w którym projekcie, w którym się znajdują.

Dzielenie kodu dla mikrousług w projekcie usługi Azure DevOps może być nieco trudniejsze.

![Rysunek 10-3 pojedyncze a wiele repozytoriów](./media/single-repository-vs-multiple.png)

**Rysunek 10-3** — jeden i wiele repozytoriów.

### <a name="repository-per-microservice"></a>Repozytorium na mikrousługę

Na pierwszy rzut oka wygląda to najbardziej logiczne podejście do dzielenia kodu źródłowego dla mikrousług. Każde repozytorium może zawierać kod, który jest wymagany do utworzenia jednej mikrousługi. Zalety tej metody są łatwo widoczne:

1. Instrukcje dotyczące tworzenia i obsługi aplikacji można dodać do pliku Readme w katalogu głównym każdego repozytorium. Podczas przechodzenia przez repozytoria można łatwo znaleźć te instrukcje i skrócić czas jej trwania dla deweloperów.
2. Każda usługa znajduje się w miejscu logicznym i można ją łatwo znaleźć, znając nazwę usługi.
3. Kompilacje można łatwo skonfigurować w taki sposób, aby były wyzwalane tylko wtedy, gdy dokonywana jest zmiana w repozytorium będącym właścicielem.
4. Liczba zmian wprowadzonych w repozytorium jest ograniczona do niewielkiej liczby deweloperów pracujących nad projektem.
5. Zabezpieczenia można łatwo skonfigurować, ograniczając repozytoria, do których deweloperzy mają uprawnienia do odczytu i zapisu.
6. Ustawienia poziomu repozytorium mogą być zmieniane przez zespół będący właścicielem z co najmniej dyskusjami z innymi.

Jednym z kluczowych koncepcji związanych z mikrousługą jest to, że usługi powinny być przesłonięte i oddzielone od siebie. W przypadku korzystania z projektu opartego na domenie w celu określenia granic dla usług usługi działają jako granice transakcyjne. Aktualizacje bazy danych nie mogą obejmować wielu usług. Ta kolekcja powiązanych danych jest nazywana kontekstem ograniczonym.  Ten pomysł jest odzwierciedlony przez izolację danych mikrousług w oddzielnym i niezależnym od reszty usług. Jest to bardzo duże rozwiązanie do przeprowadzenia tego pomysłu w sposób umożliwiający przechodzenie do kodu źródłowego.

Jednak takie podejście nie ma żadnych problemów. Jednym z bardziej gnarlyych problemów programistycznych jest zarządzanie zależnościami. Weź pod uwagę liczbę plików, które składają się na średni `node_modules` katalog. Nowa instalacja tego elementu `create-react-app` jest prawdopodobnie taka sama jak tysiące pakietów. Pytanie, jak zarządzać tymi zależnościami, jest trudne.

W przypadku zaktualizowania zależności, pakiety podrzędne muszą także aktualizować Tę zależność. Niestety, dzięki czemu Praca programistyczna niezmiennie, `node_modules` katalog zostaje zakończony z wieloma wersjami jednego pakietu, każda z nich jest zależna od innego pakietu, który jest w niewielkim stopniu różny erze. W przypadku wdrażania aplikacji należy użyć wersji zależności? Wersja, która jest obecnie w środowisku produkcyjnym? Wersja, która jest obecnie w wersji beta, ale może być w środowisku produkcyjnym przez czas, przez który odbiorca wprowadza do produkcji? Trudne problemy, które nie są rozwiązywane przez użycie mikrousług.

Istnieją biblioteki, które są zależne od wielu różnych projektów. Dzieląc mikrousługi z jednym w każdym repozytorium, można najlepiej rozwiązać wewnętrzne zależności przy użyciu wewnętrznego repozytorium, Azure Artifacts. Kompilacje dla bibliotek spowodują wypchnięcie najnowszych wersji do Azure Artifacts na użytek wewnętrzny. Projekt podrzędny należy nadal zaktualizować ręcznie, aby wziąć zależność od nowo zaktualizowanych pakietów.

Inna wadą jest sama podczas przesuwania kodu między usługami. Chociaż warto przypuszczać, że pierwsze dzielenie aplikacji na mikrousługi ma poprawność 100%, rzeczywistość jest taka, że rzadko Prescient się, że nie wystąpiły żadne błędy dzielenia usługi. Z tego względu funkcje i kod, który dysków należy przenieść z usługi do usługi: repozytorium do repozytorium. Podczas przestępnia z jednego repozytorium do innego kod utraci swoją historię. Istnieje wiele przypadków, szczególnie w przypadku inspekcji, gdzie Pełna historia fragmentów kodu jest niecenna.

Ostatnia i najważniejsza wadą jest koordynacja zmian. W aplikacji o prawdziwej mikrousługach nie powinno być żadnych zależności wdrożenia między usługami. Powinno być możliwe wdrożenie usług A, B i C w dowolnej kolejności, gdy mają one luźne sprzężenia. W rzeczywistości jednak czasami trzeba wprowadzić zmianę, która przecina wiele repozytoriów w tym samym czasie. Niektóre przykłady obejmują Aktualizowanie biblioteki w celu zamknięcia otworu zabezpieczeń lub zmiany protokołu komunikacyjnego używanego przez wszystkie usługi.

Aby dokonać zmiany między repozytorium, należy wykonać zatwierdzenie dla każdego repozytorium. Każda zmiana w każdym repozytorium musi być wymagana do ściągnięcia i przeanalizowana osobno. Może to być trudne do skoordynowania.

Alternatywą dla korzystania z wielu repozytoriów jest umieszczenie całego kodu źródłowego w bardzo duże, wszystkie wiedzący o pojedynczym repozytorium.

### <a name="single-repository"></a>Pojedyncze repozytorium

W tej metodzie, czasami nazywanej [transrepozytorium](https://danluu.com/monorepo/), cały kod źródłowy każdej usługi jest umieszczany w tym samym repozytorium. Początkowo wygląda to na przykład z pomysłem jaszczurów, który może prowadzić do postępowania z kodem źródłowym nieporęczny. Istnieją jednak pewne korzyści, które mogą działać w ten sposób.

Pierwszym z nich jest łatwiejsze zarządzanie zależnościami między projektami. Zamiast polegać na zewnętrznym źródle artefaktów, projekty mogą być bezpośrednio importowane. Oznacza to, że aktualizacje są błyskawiczne, a w czasie kompilacji na stacji roboczej dewelopera mogą znajdować się wersje powodujące konflikt. W efekcie przesuniesz niektóre z pozostałych testów integracji.

Podczas przenoszenia kodu między projektami łatwiej jest zachować historię, ponieważ pliki zostaną wykryte jako przenoszone zamiast ponownie zapisywane.

Inna korzyść polega na tym, że szerokie zmiany przekraczające granice międzyusługowe mogą być wykonywane w ramach jednego zatwierdzenia. Pozwala to zmniejszyć nakład pracy związany z potencjalnie dziesiątymi zmianami, które mogą być przeglądane pojedynczo.

Istnieje wiele narzędzi, które mogą wykonywać statyczne analizy kodu w celu wykrywania niezabezpieczonych praktyk programistycznych lub problemów z wykorzystaniem interfejsów API. W przypadku wielorepozytorium na świecie każde repozytorium będzie musiało zostać powtórzone w celu znalezienia występujących w nich problemów. Pojedyncze repozytorium umożliwia uruchamianie analizy wszystko w jednym miejscu.

Istnieje również wiele wad podejścia do jednego repozytorium. Jedną z najbardziej martwych się rzeczy jest to, że posiadanie jednego repozytorium stwarza problemy związane z bezpieczeństwem. Jeśli zawartość repozytorium jest wycieka w repozytorium na model usługi, ilość utraconych kodu jest minimalna. W przypadku jednego repozytorium wszystkie elementy należące do firmy mogą zostać utracone. Istniało wiele przykładów w przeszłości i wycofanie całego wysiłku związanego z programowaniem gier. Posiadanie wielu repozytoriów jest mniej powierzchniowe, co jest pożądanymi cechami w większości praktyk dotyczących zabezpieczeń.

Rozmiar pojedynczego repozytorium może być niemożliwy do szybkiego zarządzania. Przedstawia to pewne interesujące konsekwencje związane z wydajnością. Może być konieczne użycie wyspecjalizowanych narzędzi, takich jak [wirtualny system plików dla usługi git](https://github.com/Microsoft/VFSForGit), który pierwotnie został zaprojektowany w celu poprawy środowiska dla deweloperów w zespole systemu Windows.

Często argument służący do korzystania z jednego repozytorium jest przebiegać do argumentu, który w serwisie Facebook lub Google używa tej metody do rozmieszczenia kodu źródłowego. Jeśli takie podejście jest wystarczające dla tych firm, należy upewnić się, że jest to poprawne podejście dla wszystkich firm. Prawdziwość sprawy polega na tym, że kilka firm działa w taki sam sposób jak w przypadku skali serwisu Facebook lub Google. Problemy występujące w tych skalach różnią się od tych, które są używane dla większości deweloperów. To, co jest dobre dla gęsi, może nie być dobre dla Gander.

Na końcu można użyć dowolnego rozwiązania do hostowania kodu źródłowego dla mikrousług. Jednak w większości przypadków koszty związane z zarządzaniem i pracą inżynieryjną w ramach jednego repozytorium nie są takie same jak zalety meager. Dzielenie kodu przez wiele repozytoriów zachęca do lepszego rozdzielenia problemów i zachęca do autonomii wśród zespołów programistycznych.

### <a name="standard-directory-structure"></a>Standardowa struktura katalogów

Bez względu na to, czy wiele repozytoriów jest debata każdej usługi, będzie mieć własny katalog. Jednym z najlepszych optymalizacji, aby umożliwić deweloperom szybkie przechodzenie między projektami, jest zachowanie standardowej struktury katalogów.

![Rysunek 10-4 Standardowa struktura katalogów dla usług poczty e-mail i logowania](./media/dir-struct.png)

**Rysunek 10-4** — standardowa struktura katalogów.

Za każdym razem, gdy tworzony jest nowy projekt, należy użyć szablonu, który umieszcza prawidłową strukturę. Ten szablon może również zawierać takie przydatne elementy jak szkieletowy plik Readme i `azure-pipelines.yml` . W dowolnej architekturze mikrousług, wysoki stopień wariancji między projektami sprawia, że operacje zbiorcze w odniesieniu do usług są trudniejsze.

Istnieje wiele narzędzi, które mogą zapewnić tworzenia szablonów dla całego katalogu zawierającego kilka katalogów kodu źródłowego. [Narzędzia Yeoman](https://yeoman.io/) jest popularne w świecie JavaScript, a serwis GitHub niedawno wydał [Szablony repozytorium](https://github.blog/2019-06-06-generate-new-repositories-with-repository-templates/), które zapewniają wiele takich samych funkcji.

## <a name="task-management"></a>Zarządzanie zadaniami

Zarządzanie zadaniami w dowolnym projekcie może być trudne. Na bieżąco są niezliczone pytania dotyczące sortowania przepływów pracy, które należy skonfigurować w celu zapewnienia optymalnej produktywności dla deweloperów.

Aplikacje natywne w chmurze mogą być mniejsze niż tradycyjne produkty lub co najmniej te, które są podzielone na mniejsze usługi. Śledzenie problemów lub zadań związanych z tymi usługami pozostaje tak ważne jak w przypadku każdego innego projektu oprogramowania. Nikt nie chce utracić śledzenia niektórych elementów roboczych lub wyjaśnić klientowi, że ich problem nie został poprawnie zarejestrowany. Tablice są konfigurowane na poziomie projektu, ale w poszczególnych projektach można definiować obszary. Umożliwiają one rozbicie problemów między kilka składników. Zalety utrzymywania całej pracy dla całej aplikacji w jednym miejscu polega na tym, że można łatwo przenieść elementy robocze z jednego zespołu do drugiego, jeśli są one lepiej zrozumiałe.

Usługa Azure DevOps udostępnia wiele popularnych szablonów, które zostały wstępnie skonfigurowane. W najbardziej podstawowej konfiguracji wszystko, co jest potrzebne do uzyskania informacji, to to, co znajduje się w zaległościach, do czego pracują. Ważne jest, aby mieć wgląd w proces tworzenia oprogramowania, dzięki czemu można określić priorytety pracy i zadania zgłoszone dla klienta. Oczywiście kilka projektów oprogramowania jest przygotowanych do procesu tak proste jak `to do` , `doing` , i `done` . Rozpoczęcie dodawania kroków takich jak `QA` lub do procesu nie zajmie dużo czasu `Detailed Specification` .

Jedną z ważniejszych części metodologii Agile jest samodzielne introspekcji w regularnych odstępach czasu. Te przeglądy mają na celu zapewnienie wglądu w informacje o problemach zespołu i sposobach ich udoskonalania. Często oznacza to zmianę przepływu problemów i funkcji za pośrednictwem procesu tworzenia oprogramowania. Tak więc doskonale dobra powiększanie układów tablic z dodatkowymi etapami.

Etapy na tablicach nie są jedynym narzędziem organizacji. W zależności od konfiguracji tablicy istnieje hierarchia elementów roboczych. Najbardziej szczegółowym elementem, który może być wyświetlany na tablicy, jest zadanie. Z pola zadanie zawiera pola dla tytułu, opisu, priorytetu, oszacowania ilości pozostałej pracy oraz możliwość łączenia z innymi elementami roboczymi lub elementami deweloperskimi (gałęzie, zatwierdzenia, żądania ściągnięcia, kompilacje itd.). Elementy robocze mogą być klasyfikowane do różnych obszarów aplikacji i różnych iteracji (przebiegów), aby ułatwić łatwiejsze znajdowanie.

![Rysunek 10-5 przykładowe zadanie w usłudze Azure DevOps](./media/task-details.png)

**Rysunek 10-5** — zadanie w usłudze Azure DevOps.

Pole Description obsługuje style normalne, których oczekujesz (pogrubienie, podkreślenie kursywą i przekreślenie) oraz możliwość wstawiania obrazów. Sprawia to, że jest to zaawansowane narzędzie do użycia podczas określania pracy lub błędów.

Zadania mogą być rzutowane na funkcje, które definiują większą liczbę jednostek pracy. Z kolei funkcje mogą być [rzutowane na epiki](/azure/devops/boards/backlogs/define-features-epics?view=azure-devops). Klasyfikowanie zadań w tej hierarchii ułatwia zrozumienie, jak zamknięcie dużej funkcji jest możliwe.

![Rysunek 10-6 typów elementów roboczych skonfigurowanych domyślnie w szablonie procesu podstawowego](./media/board-issue-types.png)

**Rysunek 10-6** . element roboczy w usłudze Azure DevOps.

Istnieją różne rodzaje widoków problemów w Azure Boards. Elementy, które nie zostały jeszcze zaplanowane, są wyświetlane w zaległości. Z tego miejsca można przypisywać je do przebiegu. Przebieg jest przedziałem czasu, w którym oczekuje się, że pewna ilość pracy zostanie ukończona. To zadanie może obejmować zadania, ale również rozwiązywanie biletów. Za każdym razem można zarządzać całym przebiegiem z sekcji tablica przebiegu. Ten widok pokazuje, jak działa postęp i zawiera wykres spalania, aby zapewnić kiedykolwiek aktualizowane oszacowanie, jeśli przebieg zakończy się pomyślnie.

![Rysunek 10-7 tablicę z zdefiniowanym przebiegiem](./media/sprint-board.png)

**Rysunek 10-7** — tablica na platformie Azure DevOps.

Teraz powinno być oczywiste, że w usłudze Azure DevOps jest bardzo dużo miejsca na energię. W przypadku deweloperów istnieją proste widoki, nad którymi pracujesz. Menedżerowie projektów wyświetlają się w nadchodzącej pracy, a także w przeglądzie istniejącej pracy. Dla menedżerów istnieje wiele raportów o przeniesieniu i pojemności. Niestety, nic nie Magical o aplikacje natywne w chmurze, które eliminują konieczność śledzenia pracy. Ale jeśli musisz śledzić pracę, istnieje kilka miejsc, w których środowisko jest lepsze niż w przypadku usługi Azure DevOps.

## <a name="cicd-pipelines"></a>Potoki ciągłej integracji/ciągłego wdrażania

Prawie nie wprowadzono zmian w cyklu życia opracowywania oprogramowania, ponieważ pojawieniu ciągłej integracji (CI) i ciągłe dostarczanie (CD). Kompilowanie i uruchamianie zautomatyzowanych testów względem kodu źródłowego projektu zaraz po sprawdzeniu, że zmiany są błędne. Przed pojawieniu kompilacji ciągłej integracji nie będzie można ściągnąć kodu z repozytorium i znajdować się, że nie przeszedł testów lub nie można było nawet skompilować. Spowodowało to śledzenie źródła zerwania.

Tradycyjna wysyłka oprogramowania do środowiska produkcyjnego wymaga obszernej dokumentacji i listy kroków. Każdą z tych kroków należy wykonać ręcznie w procesie podatności na błędy.

![Rysunek 10-8 listy kontrolnej](./media/checklist.png)

**Rysunek 10-8** -Lista kontrolna.

Siostrzana ciągła integracja to ciągłe dostarczanie, w których są wdrażane skompilowane pakiety w środowisku. Proces ręczny nie może być skalowany w taki sposób, aby pasował do szybkości opracowywania, aby Automatyzacja była ważniejsze. Listy kontrolne są zastępowane przez skrypty, które mogą szybciej i bardziej precyzyjnie wykonywać te same zadania.

Środowisko, do którego dostarcza ciągłe dostarczanie, może być środowiskiem testowym lub, tak jak w wielu głównych firmach technologicznych, może być środowiskiem produkcyjnym. Drugie wymaga inwestycji w testy wysokiej jakości, które mogą mieć pewność, że zmiana nie powoduje przerwania produkcji dla użytkowników. W taki sam sposób, w jaki ciągła integracja przechwyciła problemy w przypadku wczesnego ciągłego dostarczania kodu, należy wcześniej przechwycić problemy w procesie wdrażania.

Automatyzacja procesu kompilowania i dostarczania jest accentuated przez aplikacje natywne w chmurze. Wdrożenia są wykonywane częściej i w większej liczbie środowisk, dzięki czemu ręczne wdrażanie obramowań jest niemożliwe.

### <a name="azure-builds"></a>Kompilacje platformy Azure

Usługa Azure DevOps udostępnia zestaw narzędzi umożliwiających ciągłą integrację i wdrażanie. Te narzędzia znajdują się w obszarze Azure Pipelines. Pierwsze z nich to kompilacje platformy Azure, czyli narzędzie do uruchamiania definicji kompilacji opartych na YAML na dużą skalę. Użytkownicy mogą albo przenieść własne maszyny do kompilacji (doskonałe dla sytuacji, gdy kompilacja wymaga środowiska konfiguracji lubiane), albo użyć maszyny z stale odświeżanej puli hostowanych maszyn wirtualnych platformy Azure. Te hostowane agenci kompilacji są wstępnie zainstalowani z szeroką gamę narzędzi programistycznych, a nie tylko na platformie .NET.

DevOps zawiera szeroką gamę definicji kompilacji pól, które można dostosować dla każdej kompilacji. Definicje kompilacji są zdefiniowane w pliku o nazwie `azure-pipelines.yml` i zaewidencjonowane do repozytorium, dzięki czemu mogą być poddane wersji wraz z kodem źródłowym. Dzięki temu można znacznie łatwiej wprowadzać zmiany w potoku kompilacji w gałęzi, ponieważ zmiany mogą zostać zaewidencjonowane tylko do tej gałęzi. Przykładem `azure-pipelines.yml` tworzenia aplikacji sieci web ASP.NET na platformie Full przedstawiono na rysunku 10-9.

```yml
name: $(rev:r)

variables:
  version: 9.2.0.$(Build.BuildNumber)
  solution: Portals.sln
  artifactName: drop
  buildPlatform: any cpu
  buildConfiguration: release

pool:
  name: Hosted VS2017
  demands:
  - msbuild
  - visualstudio
  - vstest

steps:
- task: NuGetToolInstaller@0
  displayName: 'Use NuGet 4.4.1'
  inputs:
    versionSpec: 4.4.1

- task: NuGetCommand@2
  displayName: 'NuGet restore'
  inputs:
    restoreSolution: '$(solution)'

- task: VSBuild@1
  displayName: 'Build solution'
  inputs:
    solution: '$(solution)'
    msbuildArgs: '-p:DeployOnBuild=true -p:WebPublishMethod=Package -p:PackageAsSingleFile=true -p:SkipInvalidConfigurations=true -p:PackageLocation="$(build.artifactstagingdirectory)\\"'
    platform: '$(buildPlatform)'
    configuration: '$(buildConfiguration)'

- task: VSTest@2
  displayName: 'Test Assemblies'
  inputs:
    testAssemblyVer2: |
     **\$(buildConfiguration)\**\*test*.dll
     !**\obj\**
     !**\*testadapter.dll
    platform: '$(buildPlatform)'
    configuration: '$(buildConfiguration)'

- task: CopyFiles@2
  displayName: 'Copy UI Test Files to: $(build.artifactstagingdirectory)'
  inputs:
    SourceFolder: UITests
    TargetFolder: '$(build.artifactstagingdirectory)/uitests'

- task: PublishBuildArtifacts@1
  displayName: 'Publish Artifact'
  inputs:
    PathtoPublish: '$(build.artifactstagingdirectory)'
    ArtifactName: '$(artifactName)'
  condition: succeededOrFailed()
```

**Rysunek 10-9** — przykład Azure-Pipelines. yml

Ta definicja kompilacji używa wielu wbudowanych zadań, które tworzą kompilacje tak proste jak kompilowanie zestawu o wysokiej rozdzielczości (prostszego niż bardzo duże Millennium Falcon). Na przykład zadanie NuGet przywraca pakiety NuGet, podczas gdy zadanie VSBuild wywołuje narzędzia kompilacji programu Visual Studio w celu wykonania rzeczywistej kompilacji. Istnieją setki różnych zadań dostępnych w usłudze Azure DevOps z tysiącami, które są utrzymywane przez społeczność. Prawdopodobnie nie ma znaczenia, jakie zadania kompilacji, które chcesz uruchomić, ktoś już ją utworzył.

Kompilacje mogą być wyzwalane ręcznie, przez zaewidencjonowanie, zgodnie z harmonogramem lub przez zakończenie innej kompilacji. W większości przypadków jest wymagane Kompilowanie każdej zaewidencjonowania. Kompilacje można filtrować w taki sposób, aby różne kompilacje były uruchamiane dla różnych części repozytorium lub do różnych gałęzi. Pozwala to na wykonywanie scenariuszy, takich jak uruchamianie szybkich kompilacji z ograniczoną testowaniem żądań ściągnięcia i uruchamianie pełnego pakietu regresji na magistrali w nocy.

Wynik końcowy kompilacji to kolekcja plików znana jako artefakty kompilacji. Te artefakty mogą być przesyłane do następnego kroku w procesie kompilacji lub dodawane do źródła artefaktów platformy Azure, dzięki czemu mogą być używane przez inne kompilacje.

### <a name="azure-devops-releases"></a>Wersje usługi Azure DevOps

Kompilacje wymagają skompilowania oprogramowania do pakietu możliwego do wysyłki, ale artefakty nadal muszą zostać wypchnięte do środowiska testowego w celu ukończenia ciągłego dostarczania. W takim przypadku usługa Azure DevOps używa osobnego narzędzia o nazwie releases. Narzędzie releases korzysta z tej samej biblioteki zadań, która była dostępna dla kompilacji, ale wprowadza koncepcję "etapów". Etap jest izolowanym środowiskiem, w którym jest zainstalowany pakiet. Na przykład produkt może wykorzystywać programowanie, pytania i odpowiedzi oraz środowisko produkcyjne. Kod jest stale dostarczany do środowiska programistycznego, w którym można uruchomić testy automatyczne. Po przejściu tych testów do środowiska pytań i odpowiedzi na testowanie ręczne. Na koniec kod jest wypychany do środowiska produkcyjnego, w którym jest widoczny dla każdego.

![Rysunek 10-10 przykład potoku wydania z etapami opracowywania, kontroli jakości i produkcji](./media/release-pipeline.png)

**Rysunek 10-10** — potoku wydania

Każdy etap kompilacji może być automatycznie wyzwalany przez zakończenie poprzedniej fazy. Jednak w wielu przypadkach nie jest to pożądane. Przeniesienie kodu do produkcji może wymagać od kogoś zatwierdzenia. Narzędzie releases obsługuje to przez umożliwienie zatwierdzania na każdym etapie potoku wydania. Zasady można skonfigurować w taki sposób, aby określona osoba lub grupa osób musiała się wylogować w wersji przed rozpoczęciem pracy w środowisku produkcyjnym. Te bramy umożliwiają ręczne sprawdzanie jakości oraz zgodność z wymaganiami prawnymi związanymi z kontrolą, co prowadzi do produkcji.

### <a name="everybody-gets-a-build-pipeline"></a>Każdy pobiera potok kompilacji

Nie ma kosztu konfigurowania wielu potoków kompilacji, więc korzystne jest posiadanie co najmniej jednego potoku kompilacji dla mikrousług. W idealnym przypadku mikrousługi są niezależnie wdrażane w dowolnym środowisku, dzięki czemu każdy z nich jest możliwy do zwolnienia za pośrednictwem własnego potoku bez zwalniania masy niepowiązanego kodu jest idealnym rozwiązaniem. Każdy potok może mieć swój własny zestaw zatwierdzeń, który pozwala na różnice w procesie kompilacji dla każdej usługi.

### <a name="versioning-releases"></a>Wersje wersji

Jedną z wad korzystania z funkcji wydań jest to, że nie można jej zdefiniować w pliku zaewidencjonowania `azure-pipelines.yml` . Istnieje wiele powodów, dla których warto wykonać te czynności, aby można było dołączać do nich szkielet wydania w szablonie projektu. Na szczęście przesuniemy niektóre etapy obsługi do składnika kompilacji. Ta wartość będzie znana jako kompilacja wieloetapowa, a [Pierwsza wersja jest teraz dostępna](https://devblogs.microsoft.com/devops/whats-new-with-azure-pipelines/)!

>[!div class="step-by-step"]
>[Poprzedni](azure-security.md) 
> [Dalej](feature-flags.md)
