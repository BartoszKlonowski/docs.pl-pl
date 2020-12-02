---
title: Zabezpieczenia platformy Azure dla aplikacji natywnych w chmurze
description: Tworzenie architektury natywnych aplikacji .NET w chmurze dla platformy Azure | Zabezpieczenia platformy Azure dla natywnych aplikacji w chmurze
ms.date: 12/01/2020
ms.openlocfilehash: 5e541606c762ea192ab8767e78e9b7346b3ec9c1
ms.sourcegitcommit: 2f485e721f7f34b87856a51181b5b56624b31fd5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/02/2020
ms.locfileid: "96509822"
---
# <a name="azure-security-for-cloud-native-apps"></a>Zabezpieczenia platformy Azure dla aplikacji natywnych w chmurze

Aplikacje natywne w chmurze mogą być łatwiejsze i trudniejsze do zabezpieczenia niż tradycyjne aplikacje. W minusem należy zabezpieczyć bardziej mniejsze aplikacje i przeznaczyć większą energię do tworzenia infrastruktury zabezpieczeń. Niejednorodny charakter języków programowania i stylów w większości wdrożeń usług oznacza również, że należy zwrócić uwagę na Biuletyny zabezpieczeń od wielu różnych dostawców.

Na stronie Przerzucanie mniejszych usług, z których każdy ma własny magazyn danych, ogranicza zakres ataku. Jeśli osoba atakująca naruszy jeden system, prawdopodobnie okaże się, że osoba atakująca będzie mogła przeskoczyć do innego systemu niż w aplikacji monolitycznej. Granice procesu są silnymi granicami. Ponadto, jeśli kopia zapasowa bazy danych jest ujawniona, uszkodzenie jest bardziej ograniczone, ponieważ ta baza danych zawiera tylko podzestaw danych i najprawdopodobniej nie będzie zawierać danych osobowych.

## <a name="threat-modeling"></a>Threat Modeling

Niezależnie od tego, czy zalety przewyższają wady aplikacji natywnych w chmurze, należy przestrzegać tego samego całościowego sposób myślenia zabezpieczeń. Bezpieczeństwo i bezpieczna myślące muszą być częścią każdego kroku projektowania i działania. Podczas planowania aplikacji zadawaj pytania takie jak:

- Jaki będzie wpływ tych danych na utratę?
- Jak można ograniczyć szkody z nieprawidłowych danych wprowadzanych do tej usługi?
- Kto powinien mieć dostęp do tych danych?
- Czy istnieją zasady inspekcji dotyczące procesu tworzenia i zwalniania?

Wszystkie te pytania są częścią procesu nazywanego [modelem zagrożeń](/azure/security/azure-security-threat-modeling-tool). Ten proces próbuje odpowiedzieć na pytanie dotyczące zagrożeń związanych z systemem, jak najprawdopodobniej zagrożenia i potencjalne szkody.

Po ustaleniu listy zagrożeń należy zdecydować, czy są one cennym problemem. Czasami zagrożenie jest mało prawdopodobne i kosztowne do zaplanowania, że nie jest to konieczne. Na przykład niektóre aktory poziomu stanu mogą wstrzyknąć zmiany do projektu procesu, który jest używany przez miliony urządzeń. Teraz zamiast uruchamiania pewnego fragmentu kodu w [pierścieniu 3](https://en.wikipedia.org/wiki/Protection_ring), ten kod jest uruchamiany w pierścieniu 0. Ten proces umożliwia korzystanie z luki w zabezpieczeniach, która może pominąć funkcję hypervisor i uruchomić kod ataku na komputerach bez systemu operacyjnego, umożliwiając ataki na wszystkie maszyny wirtualne, na których działa ten sprzęt.

Zmiany procesorów są trudne do wykrycia bez mikrozakresu i zaawansowanej wiedzy na temat projektowania krzemu tego procesora. Ten scenariusz jest mało prawdopodobny i kosztowny, aby uniknąć tego problemu, dlatego model zagrożeń nie zaleca tworzenia ochrony przed atakami.

Bardziej atrakcyjne zagrożenia, takie jak uszkodzone kontrole dostępu pozwalające `Id` zwiększyć ataki (zastąpienie `Id=2` przy użyciu `Id=3` adresu URL) lub iniekcja SQL, są bardziej atrakcyjne dla programu. Środki zaradcze dla tych zagrożeń są dość uzasadnione do kompilowania i zapobiegania gorzejom zabezpieczeń, które odnoszą się do reputacji firmy.

## <a name="principle-of-least-privilege"></a>Zasada najniższych uprawnień

Jednym z znalezionych koncepcji zabezpieczeń komputera jest zasada najniższych uprawnień (POLP). Jest to w rzeczywistości podstawą, w której w większości przypadków zabezpieczenia są cyfrowe lub fizyczne. Krótko mówiąc, zasada polega na tym, że każdy użytkownik lub proces powinien mieć możliwie najmniejszą liczbę praw do wykonania zadania.

Załóżmy na przykład, że ponosisz informacje o kasjerach w banku: dostęp do bezpiecznego jest nietypowym działaniem. Dlatego średnika nie może całkowicie otworzyć samego siebie. Aby uzyskać dostęp, muszą oni eskalować swoje żądania za pomocą Menedżera banku, który wykonuje dodatkowe kontrole zabezpieczeń.

W systemie komputerowym fantastycznie przykładem są prawa użytkownika łączącego się z bazą danych. W wielu przypadkach istnieje jedno konto użytkownika używane do tworzenia struktury bazy danych i uruchamiania aplikacji. Z wyjątkiem przypadków ekstremalnych konto z uruchomioną aplikacją nie wymaga możliwości aktualizowania informacji o schemacie. Powinno istnieć kilka kont, które zapewniają różne poziomy uprawnień. Aplikacja powinna używać tylko poziomu uprawnień, który przyznaje dostęp do odczytu i zapisu do danych w tabelach. Ten rodzaj ochrony eliminuje ataki mające na celu usunięcie tabel bazy danych lub wprowadzenie złośliwych wyzwalaczy.

Prawie każda część tworzenia aplikacji natywnej w chmurze może korzystać z zasad najniższych uprawnień. Można go znaleźć podczas konfigurowania zapór, sieciowych grup zabezpieczeń, ról i zakresów w kontroli dostępu opartej na rolach (RBAC).

## <a name="penetration-testing"></a>Testy penetracyjne

Gdy aplikacje stają się coraz bardziej skomplikowane, liczba wektorów ataków zwiększa się o współczynnik alarmu. Modelowanie zagrożeń jest wykrywane przez te same osoby, które tworzą system. W taki sam sposób, w jaki wielu deweloperów ma problemy z planowanie interakcje użytkowników, a następnie tworzenie interfejsów użytkownika, których nie można używać, większość deweloperów ma trudności z widzeniem każdego ataku. Istnieje również możliwość, że deweloperzy tworzący system nie są dobrze w metodologii ataków i nie mają znaczenia.

Testowanie penetracji lub "testowanie piórem" obejmuje nadawanie zewnętrznym podmiotom próby ataku na system. Osoby atakujące mogą być zewnętrznymi firmami konsultingowymi lub innymi programistami z dobrą wiedzą o zabezpieczeniach z innej części firmy. Są one Blanche koszyka, aby próbować podwyższyć poziomu systemu. Często zawierają one rozległe luki w zabezpieczeniach, które muszą zostać poprawione. Czasami wektor ataku będzie miał całkowicie nieoczekiwany, taki jak wykorzystanie ataku wyłudzające informacje na dyrektor naczelny.

Sama platforma Azure nieustannie przechodzą ataki od [zespołu hakerów w firmie Microsoft](https://azure.microsoft.com/resources/videos/red-vs-blue-internal-security-penetration-testing-of-microsoft-azure/). W ciągu lat były pierwsze, aby znaleźć dziesiątki potencjalnie katastrofalnych wektorów ataków, aby je zamknąć. Im bardziej skłonne miejsce docelowe, tym bardziej prawdopodobnie uczestnicy Eternal będą próbować go wykorzystać, a na świecie istnieje kilka celów, które są bardziej skłonne niż platforma Azure.

## <a name="monitoring"></a>Monitorowanie

Jeśli osoba atakująca podejmie próbę przeprowadzenia tej aplikacji, powinien mieć pewne ostrzeżenie. Często ataki można wybadać, badając dzienniki z usług. Ataki opuszczają znaki kontrolne, które mogą zostać nawiązane przed sukcesem. Na przykład osoba atakująca próbująca odgadnąć hasło będzie wykonywać wiele żądań do systemu logowania. Monitorowanie całego systemu logowania może wykryć wzorce brzmienia, które są poza wierszem ze typowym wzorcem dostępu. To monitorowanie można włączyć w alercie, który może z kolei wysyłać alert do osoby pracującej w celu aktywowania niektórych rodzajów środków zaradczych. Wysoce dojrzały system monitorowania może nawet podejmować działania w oparciu o te odchylenia, które aktywnie dodają reguły do blokowania żądań lub ograniczania odpowiedzi.

## <a name="securing-the-build"></a>Zabezpieczanie kompilacji

W jednym miejscu, w którym zabezpieczenia często się pojawiają, jest około procesu kompilacji. Nie tylko w przypadku, gdy kompilacja przeprowadza sprawdzanie zabezpieczeń, takich jak skanowanie w poszukiwaniu niezabezpieczonego kodu lub poświadczenia zaewidencjonowania, ale sama kompilacja powinna być zabezpieczona. Jeśli serwer kompilacji ma naruszone zabezpieczenia, udostępnia on fantastycznie Vector do wprowadzania dowolnego kodu do produktu.

Załóżmy, że osoba atakująca będzie odkraść hasła osób logujących się do aplikacji sieci Web. Mogą oni wprowadzić krok kompilacji, który modyfikuje wyewidencjonowany kod w celu dublowania żądania logowania do innego serwera. Następnym razem, gdy kod przechodzi przez kompilację, zostanie on zaktualizowany w trybie dyskretnym. Skanowanie luk w zabezpieczeniach kodu źródłowego nie przechwytuje tych luk w zabezpieczeniach przed kompilacją. Jednak nikt nie przechwytuje go w przeglądzie kodu, ponieważ etapy kompilacji na serwerze kompilacji. Wykorzystany kod zostanie przeszedł do środowiska produkcyjnego, w którym będzie można zebrać hasła. Prawdopodobnie nie istnieje dziennik inspekcji procesu kompilacji lub co najmniej nikt nie powinien monitorować inspekcji.

Ten scenariusz jest idealnym przykładem niedrogiego obiektu docelowego, który może zostać użyty do przerwania w systemie. Gdy osoba atakująca naruszy obwód systemu, może rozpocząć pracę nad znalezieniem sposobów podniesienia poziomu uprawnień do momentu, w którym mogą one spowodować rzeczywiste szkody w dowolnym miejscu.

## <a name="building-secure-code"></a>Kompilowanie bezpiecznego kodu

.NET Framework jest już dość bezpieczną strukturą. Pozwala to uniknąć niektórych pułapek kodu niezarządzanego, takich jak wychodzenie z końca tablic. Prace są aktywnie gotowe do naprawienia luk w zabezpieczeniach podczas ich odnajdywania. Istnieje nawet [program Bounty usterki](https://www.microsoft.com/msrc/bounty) , który płaci badaczom, aby znaleźć problemy w strukturze i zgłosić je zamiast korzystać z nich.

Istnieje wiele sposobów zabezpieczania kodu platformy .NET. Poniższe wskazówki, takie jak [wskazówki dotyczące bezpiecznego kodowania dla programu .NET](../../standard/security/secure-coding-guidelines.md) , to rozsądny krok do zagwarantowania, że kod jest bezpieczny od podstaw. [OWASP 10 najważniejszych](https://owasp.org/www-project-top-ten/) jest innym niecennym przewodnikiem do tworzenia bezpiecznego kodu.

Proces kompilacji jest dobrym miejscem do umieszczania narzędzi do skanowania w celu wykrywania problemów w kodzie źródłowym przed wprowadzeniem ich do środowiska produkcyjnego. Większość każdego projektu ma zależności od innych pakietów. Narzędzie, które może skanować w poszukiwaniu przestarzałych pakietów, będzie przechwytywać problemy w porze nocnej kompilacji. Nawet podczas kompilowania obrazów platformy Docker warto sprawdzić i upewnić się, że podstawowy obraz nie ma znanych luk w zabezpieczeniach. Innym zadaniem do sprawdzenia jest to, że nikt nie został przypadkowo zaewidencjonowany poświadczenia.

## <a name="built-in-security"></a>Zabezpieczenia wbudowane

Platforma Azure została zaprojektowana tak, aby zrównoważyć użyteczność i bezpieczeństwo większości użytkowników. Różni użytkownicy mają różne wymagania dotyczące zabezpieczeń, dlatego muszą dostosować podejście do zabezpieczeń w chmurze. Firma Microsoft publikuje ogromne informacje o zabezpieczeniach w [Centrum zaufania](https://azure.microsoft.com/support/trust-center/). Ten zasób powinien być pierwszym stopniem dla tych specjalistów, którzy chcą zrozumieć, jak działają Wbudowane technologie ograniczające ataki.

W Azure Portal [Azure Advisor](https://azure.microsoft.com/services/advisor/) jest systemem, który stale skanuje środowisko i udostępnia zalecenia. Niektóre z tych zaleceń zostały zaprojektowane w celu zaoszczędzenia użytkownikom pieniędzy, ale inne zostały zaprojektowane w celu zidentyfikowania potencjalnie niezabezpieczonych konfiguracji, takich jak posiadanie otwartego kontenera magazynu na świecie i nie jest chronione przez Virtual Network.

## <a name="azure-network-infrastructure"></a>Infrastruktura sieci platformy Azure

W środowisku lokalnym wdrożenia bardzo duże rozmieszczenie energii jest przeznaczone do konfigurowania sieci. Konfigurowanie routerów, przełączników i takich zadań jest skomplikowana. Sieci umożliwiają niektórym zasobom komunikowanie się z innymi zasobami i zapobieganie dostępowi w niektórych przypadkach. Częstą regułą sieci jest ograniczanie dostępu do środowiska produkcyjnego ze środowiska programistycznego, z wyłączeniem tego, że połowa rozwiniętego fragmentu kodu działa awry i usuwa Swath danych.

Większość zasobów platformy Azure PaaS ma tylko najbardziej podstawową i niepotrzebną konfigurację sieci. Na przykład każdy w Internecie może uzyskać dostęp do usługi App Service. Nowe wystąpienia usługi SQL Server zwykle są ograniczone, dzięki czemu strony zewnętrzne nie mogą uzyskać do nich dostępu, ale zakresy adresów IP używane przez samą platformę Azure są dozwolone przez. W związku z tym, gdy program SQL Server jest chroniony przed zagrożeniami zewnętrznymi, osoba atakująca musi skonfigurować serwer czołowy platformy Azure, z którego mogą uruchamiać ataki na wszystkich wystąpieniach SQL na platformie Azure.

Na szczęście większość zasobów platformy Azure można umieścić w Virtual Network platformy Azure, która umożliwia precyzyjne sterowanie dostępem. Podobnie jak w przypadku sieci lokalnych, które są chronione za pośrednictwem szerszego świata, sieci wirtualne to wyspy prywatnych adresów IP, które znajdują się w sieci platformy Azure.

![Rysunek 9-1 sieci wirtualnej na platformie Azure](./media/virtual-network.png)

**Rysunek 9-1**. Sieć wirtualna na platformie Azure.

W taki sam sposób, w jaki sieci lokalne mają zaporę, która zarządza dostępem do sieci, można nawiązać podobną zaporę na granicy sieci wirtualnej. Domyślnie wszystkie zasoby w sieci wirtualnej mogą nadal komunikować się z Internetem. Jest to tylko połączenia przychodzące wymagające pewnej postaci jawnego wyjątku zapory.

Po ustanowieniu sieci zasoby wewnętrzne, takie jak konta magazynu, można skonfigurować tak, aby zezwalały na dostęp tylko przez zasoby, które znajdują się również na Virtual Network. Zapora zapewnia dodatkowy poziom zabezpieczeń, w przypadku których klucze dla tego konta magazynu mogą zostać ujawnione, osoby atakujące nie będą mogły połączyć się z nim w celu wykorzystania nieujawnionych kluczy. Ten scenariusz jest kolejnym przykładem zasady najniższych uprawnień.

Węzły w klastrze usługi Azure Kubernetes mogą uczestniczyć w sieci wirtualnej tak samo jak inne zasoby, które są bardziej natywne dla platformy Azure. Ta funkcja jest nazywana [interfejsem usługi Azure Container Network](https://github.com/Azure/azure-container-networking/blob/master/docs/cni.md). W efekcie przypisuje podsieci w sieci wirtualnej, w której są przydzielane maszyny wirtualne i obrazy kontenerów.

Kontynuowanie ścieżki ilustrującej zasadę najniższych uprawnień, nie każdy zasób w ramach Virtual Network musi komunikować się z każdym innym zasobem. Na przykład w aplikacji udostępniającej internetowy interfejs API w ramach konta magazynu i bazy danych SQL jest mało prawdopodobne, że baza danych i konto magazynu muszą komunikować się ze sobą. Każde udostępnianie danych między nimi spowoduje przejście przez aplikację sieci Web. Dlatego w celu odmowy ruchu między obiema usługami można użyć [sieciowej grupy zabezpieczeń (sieciowej grupy zabezpieczeń)](/azure/virtual-network/security-overview) .

Zasady odmawiające komunikacji między zasobami mogą być irytujące do zaimplementowania, szczególnie pochodzące z tła platformy Azure bez ograniczeń ruchu. W przypadku niektórych innych chmur koncepcje grup zabezpieczeń sieci są znacznie bardziej powszechne. Na przykład zasady domyślne w AWS to, że zasoby nie mogą komunikować się między sobą, dopóki nie zostaną włączone przez reguły w sieciowej grupy zabezpieczeń. Jednak wolniejsze tworzenie tego środowiska zapewnia bezpieczniejsze ustawienia domyślne. Korzystanie z odpowiednich praktyk DevOps, zwłaszcza przy użyciu [Azure Resource Manager lub Terraform](infrastructure-as-code.md) do zarządzania uprawnieniami, może ułatwić kontrolowanie reguł.

Sieci wirtualne mogą być również przydatne podczas konfigurowania komunikacji między zasobami lokalnymi i w chmurze. Wirtualna sieć prywatna może służyć do bezproblemowego dołączania dwóch sieci. Takie podejście umożliwia uruchamianie sieci wirtualnej bez żadnych postanowień w przypadku scenariuszy, w których wszyscy użytkownicy znajdują się w lokacji. Istnieje wiele technologii, których można użyć do ustanowienia tej sieci. Najprostszą jest użycie [sieci VPN typu lokacja-lokacja](/azure/vpn-gateway/vpn-gateway-about-vpngateways?toc=%252fazure%252fvirtual-network%252ftoc.json#s2smulti) , którą można nawiązać między wieloma routerami i platformą Azure. Ruch jest szyfrowany i tunelowany przez Internet przy użyciu tego samego kosztu na bajt, co inny ruch. W przypadku scenariuszy, w których jest wymagana większa przepustowość lub większa, platforma Azure oferuje usługę o nazwie [Express Route](/azure/vpn-gateway/vpn-gateway-about-vpngateways?toc=%252fazure%252fvirtual-network%252ftoc.json#ExpressRoute) , która używa obwodu prywatnego między siecią lokalną a platformą Azure. Jest to tańsze i trudne do ustanowienia, ale również bezpieczniejsze.

## <a name="role-based-access-control-for-restricting-access-to-azure-resources"></a>Kontrola dostępu oparta na rolach w celu ograniczenia dostępu do zasobów platformy Azure

RBAC to system, który zapewnia tożsamość dla aplikacji działających na platformie Azure. Aplikacje mogą uzyskiwać dostęp do zasobów przy użyciu tej tożsamości zamiast lub oprócz używania kluczy lub haseł.

## <a name="security-principals"></a>Podmioty zabezpieczeń

Pierwszy składnik w RBAC jest podmiotem zabezpieczeń. Podmiotem zabezpieczeń może być użytkownik, Grupa, nazwa główna usługi lub tożsamość zarządzana.

![Rysunek 9-2 różne typy podmiotów zabezpieczeń](./media/rbac-security-principal.png)

**Rysunek 9-2**. Różne typy podmiotów zabezpieczeń.

- Użytkownik — każdy użytkownik, który ma konto w Azure Active Directory jest użytkownikiem.
- Grupa — kolekcja użytkowników z Azure Active Directory. Jako członek grupy, użytkownik przejmuje role należące do tej grupy.
- Nazwa główna usługi — tożsamość zabezpieczeń, pod którą uruchamiane są usługi lub aplikacje.
- Tożsamość zarządzana — tożsamość Azure Active Directory zarządzana przez platformę Azure. Tożsamości zarządzane są zwykle używane podczas tworzenia aplikacji w chmurze, które zarządzają poświadczeniami do uwierzytelniania w usługach platformy Azure.

Podmiot zabezpieczeń można zastosować do większości zasobów. Oznacza to, że istnieje możliwość przypisania podmiotu zabezpieczeń do kontenera działającego w usłudze Azure Kubernetes, co umożliwia mu dostęp do wpisów tajnych przechowywanych w Key Vault. Funkcja platformy Azure może podejmować uprawnienia zezwalające na komunikowanie się z wystąpieniem Active Directory w celu sprawdzenia poprawności tokenu JWT dla użytkownika wywołującego. Gdy usługi są włączone przy użyciu nazwy głównej usługi, ich uprawnienia mogą być zarządzane w sposób szczegółowy przy użyciu ról i zakresów.

## <a name="roles"></a>Role

Podmiot zabezpieczeń może przejąć wiele ról lub, przy użyciu bardziej sartorialych analogowych, zużywać wiele systemyów. Każda rola definiuje serię uprawnień, takich jak "Odczyt wiadomości z Azure Service Bus punktu końcowego". Obowiązującym zestawem uprawnień podmiotu zabezpieczeń jest kombinacja wszystkich uprawnień przypisanych do wszystkich ról, które ma podmiot zabezpieczeń. Platforma Azure ma wiele wbudowanych ról, a użytkownicy mogą definiować własne role.

![Rysunek 9-3 definicje ról RBAC](./media/rbac-role-definition.png)

**Rysunek 9-3**. Definicje ról RBAC.

Wbudowana w platformę Azure to również szereg ról wysokiego poziomu, takich jak właściciel, współautor, czytelnik i administrator konta użytkownika. Przy użyciu roli właściciela podmiot zabezpieczeń może uzyskać dostęp do wszystkich zasobów i przypisać uprawnienia innym użytkownikom. Współautor ma ten sam poziom dostępu do wszystkich zasobów, ale nie może przypisywać uprawnień. Czytelnik może wyświetlać tylko istniejące zasoby platformy Azure, a administrator konta użytkownika może zarządzać dostępem do zasobów platformy Azure.

Bardziej szczegółowe role wbudowane, takie jak [współautor strefy DNS](/azure/role-based-access-control/built-in-roles#dns-zone-contributor) , mają uprawnienia ograniczone do pojedynczej usługi. Podmioty zabezpieczeń mogą wykonać dowolną liczbę ról.

## <a name="scopes"></a>Zakresy

Role można stosować do ograniczonego zestawu zasobów na platformie Azure. Na przykład zastosowanie zakresu do poprzedniego przykładu odczytu z kolejki Service Bus, można zawęzić uprawnienie do pojedynczej kolejki: "Odczyt wiadomości z punktu końcowego Azure Service Bus `blah.servicebus.windows.net/queue1` "

Zakres może być tak wąski jako pojedynczy zasób lub można go zastosować do całej grupy zasobów, subskrypcji, a nawet grupy zarządzania.

Podczas testowania, jeśli podmiot zabezpieczeń ma określone uprawnienie, połączenie roli i zakresu jest brane pod uwagę. Ta kombinacja zapewnia zaawansowany mechanizm autoryzacji.

## <a name="deny"></a>Zablokuj

Wcześniej reguły RBAC były dozwolone tylko dla reguł "Zezwalaj". Takie zachowanie jest skomplikowane dla kompilowania niektórych zakresów. Na przykład zezwolenie na dostęp podmiotu zabezpieczeń do wszystkich kont magazynu z wyjątkiem jednego wymaganego przyznania jawnego uprawnienia do potencjalnie nieograniczonej listy kont magazynu. Za każdym razem, gdy nowe konto magazynu zostało utworzone, należy je dodać do tej listy kont. To dodatkowe obciążenie związane z zarządzaniem, które nie było pożądane.

Reguły odmowy mają pierwszeństwo przed regułami Zezwalaj. Teraz reprezentujący ten sam zakres "Zezwalaj na wszystkie, ale jeden" może być reprezentowany jako dwie reguły "Zezwalaj na wszystkie" i "Odmów jednej konkretnej". Reguły odmowy nie tylko ułatwiają zarządzanie, ale zezwalają na zasoby, które są bardzo bezpieczne przez odmowę dostępu do każdego z nich.

## <a name="checking-access"></a>Sprawdzanie dostępu

Jak można wyobrazić, posiadanie dużej liczby ról i zakresów może sprawiać, że efektywne uprawnienia jednostki usługi są dość trudne. Piling reguły odmowy na tym, tylko w celu zwiększenia złożoności. Na szczęście istnieje [Kalkulator uprawnień](/azure/role-based-access-control/check-access) , który może wyświetlać czynne uprawnienia dla każdej jednostki usługi. Zazwyczaj znajduje się on na karcie IAM w portalu, jak pokazano na rysunku 9-3.

![Rysunek 9-4 Kalkulator uprawnień dla usługi App Service](./media/check-rbac.png)

**Rysunek 9-4**. Kalkulator uprawnień dla usługi App Service.

## <a name="securing-secrets"></a>Zabezpieczanie wpisów tajnych

Hasła i certyfikaty są typowym wektorem ataków dla osób atakujących. Sprzęt z krakingu haseł może podejmować ataki z wymuszeniem i próbować złamać miliardów haseł na sekundę. Dlatego ważne jest, aby hasła, które są używane do uzyskiwania dostępu do zasobów, były silne, z dużą gamą znaków. Hasła te są dokładnie rodzajem haseł, które nie są zapamiętywane. Na szczęście hasła na platformie Azure nie muszą być w rzeczywistości znane dla ludzi.

Wielu ekspertów ds. zabezpieczeń [sugeruje](https://www.troyhunt.com/password-managers-dont-have-to-be-perfect-they-just-have-to-be-better-than-not-having-one/) , że korzystanie z Menedżera haseł w celu zachowania własnych haseł jest najlepszym rozwiązaniem. Podczas scentralizowania haseł w jednej lokalizacji można także używać wysoce złożonych haseł i zapewnić, że są one unikatowe dla każdego konta. Ten sam system istnieje na platformie Azure: Magazyn centralny dla wpisów tajnych.

## <a name="azure-key-vault"></a>Azure Key Vault

Azure Key Vault zapewnia scentralizowaną lokalizację do przechowywania haseł dla elementów, takich jak bazy danych, klucze interfejsu API i certyfikaty. Po wprowadzeniu wpisu tajnego do magazynu nigdy nie jest on ponownie wyświetlany, a polecenia wyodrębniania i wyświetlania są celowo całkowicie skomplikowane. Informacje w bezpiecznym obszarze są chronione za pomocą modułów zabezpieczeń sprzętowych lub FIPS 140-2 Level 2.

Dostęp do magazynu kluczy jest dostarczany za pomocą RBAC, co oznacza, że nie tylko każdy użytkownik może uzyskać dostęp do informacji w magazynie. Załóżmy, że aplikacja sieci Web chce uzyskać dostęp do parametrów połączenia bazy danych przechowywanych w Azure Key Vault. Aby uzyskać dostęp, aplikacje muszą być uruchamiane przy użyciu nazwy głównej usługi. W ramach tej roli założono, że mogą odczytywać wpisy tajne z bezpiecznego. Istnieje wiele różnych ustawień zabezpieczeń, które mogą dodatkowo ograniczyć dostęp do magazynu aplikacji, dzięki czemu nie można zaktualizować wpisów tajnych, ale tylko je odczytać.

Dostęp do magazynu kluczy można monitorować, aby upewnić się, że tylko oczekiwane aplikacje uzyskują dostęp do magazynu. Dzienniki można zintegrować z powrotem do Azure Monitor, odblokując możliwość konfigurowania alertów w przypadku napotkania nieoczekiwanych warunków.

## <a name="kubernetes"></a>Kubernetes

W ramach programu Kubernetes istnieje podobna usługa do obsługi małych fragmentów informacji o kluczowym znaczeniu. Wpisy tajne Kubernetes można ustawić za pomocą typowego `kubectl` pliku wykonywalnego.

Tworzenie klucza tajnego jest proste, ponieważ jest możliwe znalezienie wersji Base64 wartości, które mają być przechowywane:

```console
echo -n 'admin' | base64
YWRtaW4=
echo -n '1f2d1e2e67df' | base64
MWYyZDFlMmU2N2Rm
```

Następnie dodanie go do pliku tajnego o nazwie `secret.yml` , który wygląda podobnie do poniższego przykładu:

```yml
apiVersion: v1
kind: Secret
metadata:
  name: mysecret
type: Opaque
data:
  username: YWRtaW4=
  password: MWYyZDFlMmU2N2Rm
```

Na koniec ten plik można załadować do Kubernetes, uruchamiając następujące polecenie:

```console
kubectl apply -f ./secret.yaml
```

Te klucze tajne można następnie zainstalować na woluminach lub uwidocznić w ramach procesów kontenerów za poorednictwem zmiennych środowiskowych. [Zbliżające się podejście](https://12factor.net/) do kompilowania aplikacji sugeruje użycie najniższego wspólnego mianownika do przesyłania ustawień do aplikacji. Zmienne środowiskowe są najniższym typowym mianownikiem, ponieważ są obsługiwane bez względu na system operacyjny lub aplikację.

Alternatywą dla korzystania z wbudowanych wpisów tajnych Kubernetes jest uzyskanie dostępu do wpisów tajnych w Azure Key Vault z poziomu usługi Kubernetes. Najprostszym sposobem, aby to zrobić, jest przypisanie roli RBAC do kontenera, który ma ładować wpisy tajne. Aplikacja może następnie użyć interfejsów API Azure Key Vault, aby uzyskać dostęp do wpisów tajnych. Jednak takie podejście wymaga modyfikacji kodu i nie jest zgodne ze wzorcem używania zmiennych środowiskowych. Zamiast tego można wstrzyknąć wartości do kontenera. Takie podejście jest faktycznie bezpieczniejsze niż używanie Kubernetes Secret bezpośrednio, ponieważ są one dostępne dla użytkowników w klastrze.

## <a name="encryption-in-transit-and-at-rest"></a>Szyfrowanie podczas przesyłania i w spoczynku

Przechowywanie danych jest ważne, niezależnie od tego, czy są one na dysku, czy przesyłane między różnymi różnymi usługami. Najbardziej skutecznym sposobem utrzymywania danych przed wyciekiem jest zaszyfrowanie go w formacie, który nie może być łatwo odczytany przez inne osoby. Platforma Azure obsługuje szeroką gamę opcji szyfrowania.

### <a name="in-transit"></a>Przesyłanie

Istnieje kilka sposobów na szyfrowanie ruchu sieciowego w sieci na platformie Azure. Dostęp do usług platformy Azure zwykle odbywa się za pośrednictwem połączeń używających Transport Layer Security (TLS). Na przykład wszystkie połączenia z interfejsami API platformy Azure wymagają połączeń TLS. Podobnie połączenia z punktami końcowymi w usłudze Azure Storage mogą być ograniczone do pracy tylko przy użyciu szyfrowanych połączeń TLS.

TLS to skomplikowany protokół i po prostu wiedzą, że połączenie korzysta z protokołu TLS nie jest wystarczające, aby zapewnić bezpieczeństwo. Na przykład protokół TLS 1,0 jest chronicznie niezabezpieczony i protokół TLS 1,1 nie jest znacznie lepszy. Nawet w ramach wersji protokołu TLS istnieją różne ustawienia, które mogą ułatwić odszyfrowanie połączeń. Najlepszym sposobem na wykonanie akcji jest sprawdzenie i sprawdzenie, czy połączenie z serwerem używa aktualnych i dobrze skonfigurowanych protokołów.

To sprawdzenie może odbywać się przez zewnętrzną usługę, taką jak test serwera SSL laboratoriów SSL. Przebieg testu względem typowego punktu końcowego platformy Azure, w tym przypadku punkt końcowy usługi Service Bus, daje blisko idealny wynik.

Nawet usług takich jak bazy danych Azure SQL Database używa szyfrowania TLS, aby zachować ukryte dane. Interesująca część dotycząca szyfrowania danych przesyłanych przy użyciu protokołu TLS nie jest możliwa, nawet w przypadku firmy Microsoft, nasłuchiwanie połączenia między komputerami z uruchomionym protokołem TLS. Zapewnia to wygodę dla firm, które mogą być narażone na ryzyko ze strony firmy Microsoft, a nawet aktora stanu z większą liczbą zasobów niż w przypadku standardowej osoby atakującej.

![Rysunek 9-5. Raport laboratoriów SSL przedstawiający ocenę dla punktu końcowego Service Bus.](./media/ssl-report.png)

**Rysunek 9-5**. Raport laboratoriów SSL przedstawiający ocenę dla punktu końcowego Service Bus.

Ten poziom szyfrowania nie będzie wystarczający przez cały czas, dlatego należy mieć pewność, że połączenia protokołu TLS platformy Azure są bardzo bezpieczne. Platforma Azure będzie nadal rozwijać standardy zabezpieczeń jako udoskonalenia szyfrowania. Warto wiedzieć, że ktoś ogląda standardy zabezpieczeń i aktualizuje platformę Azure w miarę ich ulepszania.

### <a name="at-rest"></a>Magazynowanie

W dowolnej aplikacji istnieje wiele miejsc, w których dane są przechowywane na dysku. Sam kod aplikacji jest ładowany z jakiegoś mechanizmu magazynu. Większość aplikacji używa również pewnego rodzaju bazy danych, takiej jak SQL Server, Cosmos DB, lub nawet bardzo wydajne Table Storage cenowe. Te bazy danych wykorzystują silnie zaszyfrowane magazyny, aby zapewnić, że nikt inny niż aplikacje z odpowiednimi uprawnieniami mogą odczytywać dane. Nawet operatorzy systemu nie mogą odczytywać zaszyfrowanych danych. Dzięki temu klienci mogą nadal mieć pewność, że tajne informacje pozostają tajne.

### <a name="storage"></a>Magazyn

Nadmierne Przypinanie wielu platform Azure to aparat usługi Azure Storage. Dyski maszyny wirtualnej są instalowane w usłudze Azure Storage. Usługa Azure Kubernetes działa na maszynach wirtualnych, które są hostowane w usłudze Azure Storage. Nawet w przypadku technologii bezserwerowych, takich jak Azure Functions aplikacje i Azure Container Instances, należy uruchomić poza dyskiem, który jest częścią usługi Azure Storage.

Jeśli usługa Azure Storage jest dobrze zaszyfrowana, umożliwia ona również podstawę dla większości innych elementów. Usługa Azure Storage [jest zaszyfrowana](/azure/storage/common/storage-service-encryption) przy użyciu zgodności ze [standardem FIPS 140-2](https://en.wikipedia.org/wiki/FIPS_140) [256-bitowym AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard). Jest to dobrze uznana technologia szyfrowania, która była przedmiotem rozbudowanej kontroli naukowej w ciągu ostatnich 20 lub lat. Obecnie nie ma znanego praktycznego ataku, który zezwoli komuś bez znajomości klucza w celu odczytania danych szyfrowanych przez algorytm AES.

Domyślnie klucze używane do szyfrowania usługi Azure Storage są zarządzane przez firmę Microsoft. Istnieją rozległe zabezpieczenia zapewniające zapobieganie złośliwemu dostępowi do tych kluczy. Jednak użytkownicy z określonymi wymaganiami dotyczącymi szyfrowania mogą również [udostępniać własne klucze magazynu](/azure/storage/common/storage-encryption-keys-powershell) zarządzane w programie Azure Key Vault. Te klucze można odwołać w dowolnym momencie, co mogłoby efektywnie renderować zawartość konta magazynu przy użyciu ich niedostępności.

Maszyny wirtualne korzystają z zaszyfrowanego magazynu, ale istnieje możliwość zapewnienia innej warstwy szyfrowania przy użyciu technologii, takich jak funkcja BitLocker w systemie Windows lub DM-Crypt na komputerze z systemem Linux. Te technologie oznaczają, że nawet w przypadku przecieku obrazu dysku poza magazynem nie można go odczytać.

### <a name="azure-sql"></a>Azure SQL

Bazy danych hostowane w usłudze Azure SQL wykorzystują technologię o nazwie [transparent Data Encryption (TDE)](/sql/relational-databases/security/encryption/transparent-data-encryption) , aby zapewnić, że dane pozostaną zaszyfrowane. Jest on domyślnie włączony dla wszystkich nowo utworzonych baz danych SQL, ale musi być włączony ręcznie dla starszych baz danych. TDE wykonuje szyfrowanie w czasie rzeczywistym i odszyfrowywanie nie tylko dla bazy danych, ale również kopie zapasowe i dzienniki transakcji.

Parametry szyfrowania są przechowywane w `master` bazie danych programu i po uruchomieniu są odczytywane w pamięci dla pozostałych operacji. Oznacza to, że `master` baza danych musi pozostać niezaszyfrowana. Rzeczywistym kluczem zarządza firma Microsoft. Jednak użytkownicy z dokładnymi wymaganiami dotyczącymi bezpieczeństwa mogą zapewnić własny klucz w Key Vault w podobny sposób, jak w przypadku usługi Azure Storage. Key Vault zapewnia takie usługi jak rotacja kluczy i odwoływanie.

Część "przezroczyste" strumienia TDS pochodzi z faktu, że nie są potrzebne zmiany klienta wymagające użycia zaszyfrowanej bazy danych. Chociaż takie podejście zapewnia dobrą ochronę, przeciek hasła bazy danych jest wystarczający, aby użytkownicy mogli odszyfrować dane. Istnieje inne podejście, które szyfruje pojedyncze kolumny lub tabele w bazie danych. [Always Encrypted](/azure/sql-database/sql-database-always-encrypted-azure-key-vault) zapewnia, że dane zaszyfrowane nie będą wyświetlane w postaci zwykłego tekstu wewnątrz bazy danych.

Skonfigurowanie tej warstwy szyfrowania wymaga uruchomienia przez kreatora w SQL Server Management Studio, aby wybrać sortowanie szyfrowania i miejsce, w którym w Key Vault mają być przechowywane skojarzone klucze.

![Rysunek 9-6 Wybieranie kolumn w tabeli, które mają być szyfrowane przy użyciu Always Encrypted](./media/always-encrypted.png)

**Rysunek 9-6**. Wybieranie kolumn w tabeli do zaszyfrowania przy użyciu Always Encrypted.

Aplikacje klienckie, które odczytują informacje z tych zaszyfrowanych kolumn, muszą wprowadzić specjalne Dodatki do odczytu zaszyfrowanych danych. Parametry połączenia muszą zostać zaktualizowane przy użyciu programu `Column Encryption Setting=Enabled` , a poświadczenia klienta muszą zostać pobrane z Key Vault. Klient SQL Server musi być następnie przy użyciu kluczy szyfrowania kolumn. Po wykonaniu tej czynności pozostałe akcje używają standardowych interfejsów do programu SQL Client. Oznacza to, że narzędzia takie jak Dapper i Entity Framework, które są tworzone na podstawie klienta SQL, będą nadal działały bez zmian. Always Encrypted mogą jeszcze nie być dostępne dla każdego sterownika SQL Server w każdym języku.

Kombinacja TDE i Always Encrypted, które mogą być używane z kluczami specyficznymi dla klienta, zapewnia, że nawet najbardziej dokładne wymagania dotyczące szyfrowania są obsługiwane.

### <a name="cosmos-db"></a>Usługa Cosmos DB

Cosmos DB to najnowsza baza danych udostępniona przez firmę Microsoft na platformie Azure. Została skompilowana od podstaw z myślą o zabezpieczeniach i kryptografii. Szyfrowanie AES-256bit jest standardem dla wszystkich baz danych Cosmos DB i nie można go wyłączyć. W połączeniu z wymaganiami protokołu TLS 1,2 do komunikacji, całe rozwiązanie magazynu jest zaszyfrowane.

![Rysunek 9-7 przepływ szyfrowania danych w Cosmos DB](./media/cosmos-encryption.png)

**Rysunek 9-7**. Przepływ szyfrowania danych w Cosmos DB.

Mimo że Cosmos DB nie zapewnia do dostarczania kluczy szyfrowania klienta, w celu zapewnienia, że zespół pozostanie niezgodny ze standardem PCI-DSS. Cosmos DB również nie obsługuje żadnego sortowania szyfrowania pojedynczej kolumny podobnej do Always Encrypted usługi Azure SQL.

## <a name="keeping-secure"></a>Zabezpieczanie

Platforma Azure ma wszystkie narzędzia niezbędne do zwolnienia wysoce bezpiecznego produktu. Jednak łańcuch jest tylko tak silny jak jego słaby link. Jeśli aplikacje wdrożone na platformie Azure nie są opracowywane przy użyciu właściwej sposób myślenia zabezpieczeń i dobrych inspekcji zabezpieczeń, stają się one słabymi łączami w łańcuchu. Istnieje wiele doskonałych narzędzi do analizy statycznej, bibliotek szyfrowania i praktyk zabezpieczeń, których można użyć w celu zapewnienia, że oprogramowanie zainstalowane na platformie Azure jest tak bezpieczne jak platforma Azure. Przykłady obejmują [statyczne narzędzia analityczne](https://www.whitesourcesoftware.com/), [biblioteki szyfrowania](https://www.libressl.org/)i [praktyki zabezpieczeń](https://azure.microsoft.com/resources/videos/red-vs-blue-internal-security-penetration-testing-of-microsoft-azure/).

>[!div class="step-by-step"]
>[Poprzedni](security.md) 
> [Dalej](devops.md)
