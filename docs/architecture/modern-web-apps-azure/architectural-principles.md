---
title: Zasady dotyczące architektury
description: Tworzenie architektury nowoczesnych aplikacji sieci Web przy użyciu ASP.NET Core i platformy Azure | Zasady architektury
author: ardalis
ms.author: wiwagn
ms.date: 12/01/2020
ms.openlocfilehash: f4079e0409c1675e8f8a3e494303683daeef29c1
ms.sourcegitcommit: 45c7148f2483db2501c1aa696ab6ed2ed8cb71b2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/08/2020
ms.locfileid: "96851415"
---
# <a name="architectural-principles"></a>Zasady dotyczące architektury

> "Jeśli konstruktory skompilowane przez programistów w sposób, w jaki programiści zapisały programy, to pierwszy Woodpecker, który miał być zniszczony Civilization".  
> _\- Gerald Weinberg_

Należy wziąć pod uwagę możliwość tworzenia i projektowania rozwiązań programistycznych. Zasady przedstawione w tej sekcji mogą ułatwić podejmowanie decyzji dotyczących architektury, które będą powodowały czyste i utrzymywane w obsłudze aplikacje. Ogólnie rzecz biorąc, te zasady przeprowadzą Cię przez proces tworzenia aplikacji poza dyskretnymi składnikami, które nie są ściśle powiązane z innymi częściami aplikacji, ale raczej komunikują się przez jawne interfejsy lub systemy obsługi komunikatów.

## <a name="common-design-principles"></a>Typowe zasady projektowania

### <a name="separation-of-concerns"></a>Rozdzielenie problemów

Zasada identyfikatora GUID podczas opracowywania polega na **rozdzieleniu obaw**. Ta zasada potwierdza, że oprogramowanie powinno być oddzielone w zależności od rodzaju wykonywanych przez niego zadań. Rozważmy na przykład aplikację, która zawiera logikę do identyfikowania wartych elementów do wyświetlenia użytkownikowi, a także formatuje takie elementy w określony sposób, aby były bardziej zauważalne. Zachowanie odpowiedzialne za wybór, które elementy mają być sformatowane, powinno być przechowywane niezależnie od zachowania odpowiedzialnego za formatowanie elementów, ponieważ te zachowania są oddzielnymi problemami, które są tylko ze sobą powiązane ze sobą.

Architektura aplikacji może być logicznie skompilowana, aby przestrzegać tej zasady, oddzielając podstawowe zachowanie biznesowe od infrastruktury i logiki interfejsu użytkownika. W idealnym przypadku reguły biznesowe i logika powinny znajdować się w osobnym projekcie, który nie powinien zależeć od innych projektów w aplikacji. Ta separacja pomaga zapewnić, że model biznesowy jest łatwy do przetestowania i może zostać rozmieszczony bez ścisłej współpracy z szczegółami implementacji niskiego poziomu. Rozdzielenie problemów jest najważniejszym zagadnieniem związanym z użyciem warstw w architekturze aplikacji.

### <a name="encapsulation"></a>Encapsulation

Różne części aplikacji powinny używać **hermetyzacji** do izolowania ich od innych części aplikacji. Składniki aplikacji i warstwy powinny mieć możliwość dostosowania ich wewnętrznej implementacji bez przerywania współpracowników, tak długo, jak kontrakty zewnętrzne nie zostały naruszone. Odpowiednie użycie hermetyzacji pomaga osiągnąć swobodny sprzężenie i modułowość w projektach aplikacji, ponieważ obiekty i pakiety można zamienić na alternatywne implementacje, o ile ten sam interfejs jest obsługiwany.

W klasach hermetyzacja jest realizowana przez ograniczenie poza dostępem do stanu wewnętrznego klasy. Jeśli aktor zewnętrzny chce manipulować stanem obiektu, należy to zrobić za pośrednictwem dobrze zdefiniowanej funkcji (lub metody ustawiającej właściwości), a nie bezpośredniego dostępu do stanu prywatnego obiektu. Podobnie składniki aplikacji i aplikacje powinny ujawniać dobrze zdefiniowane interfejsy dla współpracowników, zamiast zezwalać na bezpośrednie modyfikowanie ich stanu. Takie podejście zwalnia projekt wewnętrzny aplikacji do rozbudowania z upływem czasu bez obaw, że takie działanie spowoduje przerwanie współpracowników, dopóki są utrzymywane umowy publiczne.

### <a name="dependency-inversion"></a>Niewersja zależności

Kierunek zależności w aplikacji powinien mieć kierunek abstrakcji, a nie szczegóły implementacji. Większość aplikacji jest zapisywana w taki sposób, że przepływy zależności czasu kompilacji w kierunku wykonywania środowiska uruchomieniowego, generujący wykres zależności bezpośredniej. Oznacza to, że jeśli moduł A wywołuje funkcję w module B, która wywołuje funkcję w module C, a następnie w czasie kompilacji A będzie zależeć od B, która będzie zależeć od C, jak pokazano na rysunku 4-1.

![Wykres zależności bezpośredniej](./media/image4-1.png)

**Rysunek 4-1.** Wykres zależności bezpośredniej.

Zastosowanie zasady odróżniania zależności umożliwia wywoływanie metod w ramach abstrakcji, które B implementuje, dzięki czemu można wywołać B w czasie wykonywania, ale dla B, aby zależały od interfejsu kontrolowanego przez w czasie kompilacji (w rezultacie *odwrócić* typowy zależność czasu kompilacji). W czasie wykonywania przepływ wykonywania programu pozostaje niezmieniony, ale wprowadzenie interfejsów oznacza, że można łatwo podłączyć różne implementacje tych interfejsów.

![Wykres odwróconej zależności](./media/image4-2.png)

**Rysunek 4-2.** Odwrócony wykres zależności.

**Wersja zależności** jest kluczową częścią tworzenia luźno powiązanych aplikacji, ponieważ szczegóły implementacji można napisać, aby zależały od i wdrożyć abstrakcje wyższego poziomu, a nie inne sposoby. Aplikacje wynikowe są bardziej weryfikowalne, modularne i utrzymywane w wyniku. Zaleca się *iniekcję zależności* , postępując zgodnie z zasadą Inwersja zależności.

### <a name="explicit-dependencies"></a>Jawne zależności

**Metody i klasy powinny jawnie wymagać wszelkich obiektów współpracy, które są potrzebne do poprawnego działania.** Konstruktory klas zapewniają szansę dla klas, aby identyfikować elementy, których potrzebują, aby były w prawidłowym stanie i działać prawidłowo. W przypadku zdefiniowania klas, które mogą być skonstruowane i wywoływane, ale które będą działać prawidłowo tylko wtedy, gdy są używane pewne składniki globalne lub infrastruktury, te klasy są *DISHONEST* z klientami. Kontrakt konstruktora mówi klientowi, że potrzebuje tylko określonych elementów (prawdopodobnie nic nie tylko wtedy, gdy Klasa korzysta tylko z konstruktora bez parametrów), ale w czasie wykonywania obiekt naprawdę nie wymaga czegoś innego.

Zgodnie z zasadą jawnych zależności, klasy i metody są uczciwie związane z klientami na temat tego, czego potrzebują do działania. Zgodnie z zasadą sprawia, że kod jest bardziej czytelny, a kontrakty związane z kodowaniem są bardziej przyjazne dla użytkownika, ponieważ użytkownicy będą mieli zaufanie, o ile są one wymagane w formie parametrów metody lub konstruktora, obiekty, z którymi pracują, działają poprawnie w czasie wykonywania.

### <a name="single-responsibility"></a>Pojedyncza odpowiedzialność

Zasada pojedynczej odpowiedzialności dotyczy projektowania zorientowanego obiektowo, ale można ją również traktować jako zasadę architektoniczną podobną do rozdzielenia obaw. Pozwala to na to, że obiekty powinny mieć tylko jedną odpowiedzialność i mieć tylko jedną przyczynę do zmiany. Jedyną sytuacją, w której obiekt powinien zostać zmieniony, jest to, że w sposób, w jaki wykonuje swoją odpowiedzialność, należy zaktualizować. Zgodnie z tą zasadą, można utworzyć bardziej luźno powiązane systemy i moduły, ponieważ wiele rodzajów nowych zachowań może być implementowane jako nowe klasy, a nie przez dodanie dodatkowej odpowiedzialności do istniejących klas. Dodawanie nowych klas jest zawsze bezpieczniejsze niż zmiana istniejących klas, ponieważ żaden kod nie zależy jeszcze od nowych klas.

W aplikacji monolitycznej możemy zastosować pojedynczą regułę odpowiedzialności na wysokim poziomie do warstw w aplikacji. Odpowiedzialność za prezentację powinna pozostawać w projekcie interfejsu użytkownika, a odpowiedzialność za dostęp do danych powinna być przechowywana w ramach projektu infrastruktury. Logika biznesowa powinna być przechowywana w podstawowym projekcie aplikacji, w którym można ją łatwo przetestować i może się rozwijać niezależnie od innych obowiązków.

Gdy ta zasada jest stosowana do architektury aplikacji i została przełączona do jej logicznego punktu końcowego, uzyskasz mikrousługi. Dana mikrousługa powinna mieć jedną odpowiedzialność. Jeśli musisz zwiększyć zachowanie systemu, zazwyczaj lepiej jest to zrobić poprzez dodanie dodatkowych mikrousług, a nie przez dodanie odpowiedzialności do istniejącej usługi.

[Dowiedz się więcej o architekturze mikrousług](https://aka.ms/MicroservicesEbook)

### <a name="dont-repeat-yourself-dry"></a>Nie powtarzaj siebie (SUCHa)

Aplikacja powinna unikać określania zachowania związanego z konkretną koncepcją w wielu miejscach, ponieważ to rozwiązanie jest częstym źródłem błędów. W pewnym momencie zmiana wymagań będzie wymagała zmiany tego zachowania. Prawdopodobnie nie będzie można zaktualizować co najmniej jednego wystąpienia zachowania, a system będzie niespójnie zachowywać się.

Zamiast duplikowania logiki należy hermetyzować ją w konstrukcji programistycznej. Uczyń ten konstrukcja pojedynczym urzędem w tym zachowaniu i w każdej innej części aplikacji, która wymaga tego zachowania, użyj nowej konstrukcji.

> [!NOTE]
> Unikaj powiązań wspólnie z zachowaniem, które jest jedynym przypadkiem powtarzające się. Na przykład, tylko ponieważ dwie różne stałe mają tę samą wartość, nie oznacza to, że powinna istnieć tylko jedna stała, jeśli koncepcyjnie odwołują się do różnych rzeczy.

### <a name="persistence-ignorance"></a>Ignorujących trwałości

**Ignorujących trwałości** (PI) odnosi się do typów, które muszą być utrwalane, ale których kod nie ma wpływać na wybór technologii trwałości. Takie typy w programie .NET są czasami określane jako zwykłe stare obiekty CLR (POCOs), ponieważ nie muszą dziedziczyć z określonej klasy bazowej ani implementować określonego interfejsu. Trwałość ignorujących jest cenna, ponieważ pozwala na utrwalenie tego samego modelu biznesowego na wiele sposobów, oferując dodatkową elastyczność aplikacji. Opcje trwałości mogą ulec zmianie z upływem czasu, z jednej technologii bazy danych na inną, a oprócz tego mogą być wymagane dodatkowe formy trwałości (na przykład użycie pamięci podręcznej Redis lub Azure Cosmos DB oprócz relacyjnej bazy danych).

Niektóre przykłady naruszeń tej zasady obejmują:

- Wymagana Klasa bazowa.

- Wymagana implementacja interfejsu.

- Klasy odpowiedzialne za zapisywanie siebie (na przykład wzorzec rekordu aktywnego).

- Wymagany Konstruktor bez parametrów.

- Właściwości wymagające słowa kluczowego Virtual.

- Wymagane atrybuty dotyczące trwałości.

Wymaganie, aby klasy miały dowolne z powyższych funkcji lub zachowań, dodaje sprzężenie między typami, które mają być utrwalane i wybór technologii trwałości, utrudniając w przyszłości nowe strategie dostępu do danych.

### <a name="bounded-contexts"></a>Powiązane konteksty

**Powiązane konteksty** są głównym wzorcem w projekcie Domain-Driven. Zapewniają one sposób działania złożoności w dużych aplikacjach lub organizacjach, dzieląc je na osobne moduły koncepcyjne. Każdy moduł koncepcyjny reprezentuje kontekst, który jest oddzielony od innych kontekstów (w związku z czym jest ograniczony) i może się niezależnie rozwijać. Każdy związany kontekst powinien być bezpłatny, aby można było wybrać własne nazwy dla koncepcji w nim i powinien mieć wyłączny dostęp do własnego magazynu trwałości.

Co najmniej poszczególne aplikacje sieci Web powinny dążyć do własnego kontekstu, z własnym magazynem trwałości dla ich modelu biznesowego, a nie do udostępniania bazy danych innym aplikacjom. Komunikacja między kontekstami ograniczonymi odbywa się za pomocą interfejsów programistycznych, a nie za pomocą udostępnionej bazy danych, która umożliwia wykonywanie logiki biznesowej i zdarzeń w odpowiedzi na zmiany, które mają miejsce. Powiązane konteksty są ściśle mapowane na mikrousługi, które są również idealnie zaimplementowane jako własne powiązane konteksty.

## <a name="additional-resources"></a>Dodatkowe zasoby

- [Wzorce projektowe JAVA: zasady](https://java-design-patterns.com/principles/)
- [Ograniczony kontekst](https://martinfowler.com/bliki/BoundedContext.html)

>[!div class="step-by-step"]
>[Poprzedni](choose-between-traditional-web-and-single-page-apps.md) 
> [Dalej](common-web-application-architectures.md)
