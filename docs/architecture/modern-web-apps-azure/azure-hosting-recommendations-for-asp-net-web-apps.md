---
title: Zalecenia dotyczące hostingu platformy Azure dla ASP.NET Core aplikacji sieci Web
description: Tworzenie architektury nowoczesnych aplikacji sieci Web przy użyciu ASP.NET Core i platformy Azure | Zalecenia dotyczące hostingu platformy Azure dla usługi ASP.NET Web Apps
author: ardalis
ms.author: wiwagn
ms.date: 12/01/2020
ms.openlocfilehash: c209a7fa9ce89e12466424f750d5583a59f8b980
ms.sourcegitcommit: 45c7148f2483db2501c1aa696ab6ed2ed8cb71b2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/08/2020
ms.locfileid: "96851721"
---
# <a name="azure-hosting-recommendations-for-aspnet-core-web-apps"></a>Zalecenia dotyczące hostingu platformy Azure dla ASP.NET Core aplikacji sieci Web

> "Liderzy biznesowi wszędzie są pomijani usługi IT, aby uzyskiwać aplikacje z chmury (znane również jako SaaS) i płacić za nie tak jak w przypadku subskrypcji magazynu. Gdy usługa nie jest już wymagana, może anulować subskrypcję bez żadnego sprzętu nieużywanego w rogu ".  
> _\- Daryl Plummer, analityk firmy Gartner_

W zależności od potrzeb i architektury aplikacji Microsoft Azure może ją obsłużyć. Twoje potrzeby hostingu mogą być proste jako statyczna Witryna internetowa lub zaawansowana aplikacja składająca się z wielu usług. W przypadku ASP.NET Core monolitycznych aplikacji sieci Web i usług pomocniczych istnieje kilka dobrze znanych konfiguracji, które są zalecane. Zalecenia dotyczące tego artykułu są pogrupowane w zależności od rodzaju zasobu, który ma być hostowany, od tego, czy są to pełne aplikacje, poszczególne procesy czy dane.

## <a name="web-applications"></a>Aplikacje internetowe

Aplikacje sieci Web mogą być hostowane przy użyciu:

- App Service Web Apps

- Kontenery (kilka opcji)

- Virtual Machines (maszyny wirtualne)

Z tych App Service Web Apps jest zalecanym rozwiązaniem dla większości scenariuszy, w tym prostych aplikacji opartych na kontenerach. W przypadku architektur mikrousług należy wziąć pod uwagę podejście oparte na kontenerach. Jeśli potrzebujesz większej kontroli nad maszynami, na których działa aplikacja, weź pod uwagę Virtual Machines platformy Azure.

### <a name="app-service-web-apps"></a>App Service Web Apps

App Service Web Apps oferuje w pełni zarządzaną platformę zoptymalizowaną pod kątem hostowania aplikacji sieci Web. Jest to oferta platformy jako usługi (PaaS), która umożliwia skoncentrowanie się na logice biznesowej, a platforma Azure zajmuje się infrastrukturą potrzebną do uruchamiania i skalowania aplikacji. Niektóre kluczowe funkcje App Service Web Apps:

- Optymalizacja DevOps (ciągła integracja i dostarczanie, wiele środowisk, testowanie A/B, obsługa skryptów).

- Globalna skala i wysoka dostępność.

- Połączenia z platformami SaaS i danymi lokalnymi.

- Zabezpieczenia i zgodność.

- Integracja z programem Visual Studio.

Usługa Azure App Service to najlepszy wybór w przypadku większości aplikacji internetowych. Wdrażanie i zarządzanie są zintegrowane z platformą, witryny można szybko skalować na potrzeby obsługi dużych obciążeń generowanych przez ruch sieciowy, a wbudowane równoważenie obciążenia i usługa Traffic Manager zapewniają wysoką dostępność. Istniejące Lokacje można przenosić do Azure App Service łatwo przy użyciu narzędzia do migracji w trybie online. Możesz użyć aplikacji typu open source z galerii aplikacji sieci Web lub utworzyć nową witrynę za pomocą wybranej platformy i narzędzi. Zadania WebJob upraszczają dodawanie przetwarzania zadań w tle do aplikacji internetowej usługi App Service. Jeśli masz istniejącą aplikację ASP.NET hostowaną lokalnie przy użyciu lokalnej bazy danych, istnieje wyraźna ścieżka do migracji. Możesz użyć App Service aplikacji sieci Web z Azure SQL Database (lub bezpiecznego dostępu do lokalnego serwera bazy danych, jeśli jest preferowany).

![Zalecana strategia migracji lokalnych aplikacji .NET do Azure App Service](./media/image1-6.png)

W większości przypadków przechodzenie z lokalnie hostowanej aplikacji ASP.NET do aplikacji sieci Web App Service jest procesem prostym. Niewielka zmiana powinna być wymagana przez samą aplikację i można szybko zacząć korzystać z wielu funkcji, które Azure App Service Web Apps oferta.

Oprócz aplikacji, które nie są zoptymalizowane pod kątem chmury, Azure App Service Web Apps to doskonałe rozwiązanie dla wielu prostych aplikacji monolitycznych (nierozproszonych), takich jak wiele aplikacji ASP.NET Core. W tym podejściu architektura jest podstawowa i prosta do zrozumienia i zarządzania:

![Podstawowa architektura platformy Azure](./media/image1-5.png)

Niewielka liczba zasobów w pojedynczej grupie zasobów jest zwykle wystarczająca do zarządzania taką aplikacją. Aplikacje, które są zwykle wdrażane jako pojedyncze jednostki, a nie aplikacje, które składają się z wielu oddzielnych procesów, są dobrym kandydatami do tego [podstawowego podejścia do architektury](/azure/architecture/reference-architectures/app-service-web-app/basic-web-app). Chociaż skalowalne w poziomie, takie podejście nadal zezwala aplikacji hostowanej na skalowanie w górę (więcej zasobów na węzeł) i na zewnątrz (więcej węzłów hostowanych), aby sprostać dowolnemu wzrostowi popytu. Dzięki funkcji automatycznego skalowania aplikacja może być skonfigurowana w taki sposób, aby automatycznie dostosowywać liczbę węzłów obsługujących aplikację na podstawie popytu i średniego obciążenia między węzłami.

### <a name="app-service-web-apps-for-containers"></a>App Service Web Apps kontenerów

Oprócz obsługi bezpośredniego hostowania aplikacji sieci Web [App Service Web Apps dla kontenerów](https://azure.microsoft.com/services/app-service/containers/) mogą służyć do uruchamiania aplikacji kontenerowych w systemach Windows i Linux. Korzystając z tej usługi, można łatwo wdrażać i uruchamiać aplikacje z kontenerami, które można skalować w miarę rozwoju firmy. Aplikacje mają wszystkie funkcje App Service Web Apps wymienionych powyżej. Ponadto Web Apps dla kontenerów obsługuje usprawnione ciągłe wdrażanie/ciągłe dostarczanie za pomocą usługi Docker Hub, Azure Container Registry i usługi GitHub. Za pomocą usługi Azure DevOps można definiować potoki kompilacji i wdrażania, które publikują zmiany w rejestrze. Te zmiany można następnie przetestować w środowisku przejściowym i wdrożyć je automatycznie do produkcji przy użyciu miejsc wdrożenia, co umożliwia uaktualnianie bez przestojów. Przywrócenie poprzednich wersji może odbywać się równie łatwo.

Istnieje kilka scenariuszy, w których Web Apps for Containers są najbardziej sensowne. Jeśli masz istniejące aplikacje, które możesz konteneryzowanie, niezależnie od tego, czy znajdują się w kontenerach systemu Windows lub Linux, możesz je hostować za pomocą tego zestawu narzędzi. Po prostu opublikuj kontener, a następnie skonfiguruj Web Apps dla kontenerów w celu ściągnięcia najnowszej wersji tego obrazu z wybranego rejestru. Jest to podejście "Unieś i Shift" służące do migrowania z modeli hostingu aplikacji klasycznych do modelu zoptymalizowanego pod kątem chmury.

![Migrowanie kontenera lokalnej aplikacji .NET do usługi Azure Web Apps dla kontenerów](./media/image1-8.png)

Takie podejście również sprawdza się również wtedy, gdy zespół programistyczny może przejść do procesu programowania opartego na kontenerach. "Pętla wewnętrzna" opracowywania aplikacji z kontenerami obejmuje tworzenie aplikacji z kontenerami. Zmiany wprowadzone w kodzie oraz do konfiguracji kontenera są przekazywane do kontroli źródła, a zautomatyzowana kompilacja jest odpowiedzialna za publikowanie nowych obrazów kontenera do rejestru, takiego jak Docker Hub lub Azure Container Registry. Te obrazy są następnie używane jako podstawa dodatkowego programowania, a także w przypadku wdrożeń do produkcji, jak pokazano na poniższym diagramie:

![Kompleksowy przepływ pracy cyklu życia DevOps platformy Docker](./media/image1-7.png)

Programowanie przy użyciu kontenerów oferuje wiele korzyści, zwłaszcza gdy kontenery są używane w środowisku produkcyjnym. Ta sama konfiguracja kontenera jest używana do hostowania aplikacji w każdym środowisku, w którym jest uruchomiona, z lokalnej maszyny deweloperskiej w celu utworzenia i przetestowania systemów do produkcji. Takie podejście znacznie zmniejsza prawdopodobieństwo wystąpienia wad wynikających z różnic między konfiguracją komputera lub wersjami oprogramowania. Deweloperzy mogą również korzystać ze wszystkich narzędzi, które są najbardziej produktywne, w tym systemu operacyjnego, ponieważ kontenery mogą być uruchamiane w dowolnym systemie operacyjnym. W niektórych przypadkach aplikacje rozproszone obejmujące wiele kontenerów mogą być bardzo czasochłonne, aby można je było uruchamiać na jednym komputerze deweloperskim. W tym scenariuszu warto przeprowadzić uaktualnienie do korzystania z Kubernetes i Azure Dev Spaces, które opisano w następnej sekcji.

W miarę jak część większych aplikacji jest dzielona na własne, niezależne *mikrousługi*, można użyć dodatkowych wzorców projektowych, aby poprawić zachowanie aplikacji. Zamiast bezpośrednio pracować z poszczególnymi usługami, *brama interfejsu API* może uprościć dostęp i oddzielić klienta od jego zaplecza. Istnienie osobnych zaplecza usługi dla różnych frontonów pozwala również na rozwój usług w porozumieniu z klientami. Dostęp do wspólnych usług można uzyskać za pośrednictwem oddzielnego kontenera *przyczepek* , który może obejmować typowe biblioteki łączności klienta przy użyciu wzorca *ambasadora* .

![Mikrousługi — Przykładowa architektura z kilkoma typowymi wzorcami projektowymi.](./media/image1-10.png)

[Dowiedz się więcej o wzorcach projektowych, które należy wziąć pod uwagę podczas tworzenia systemów mikrousług.](/azure/architecture/microservices/design/patterns)

### <a name="azure-kubernetes-service"></a>Azure Kubernetes Service

Usługa Azure Kubernetes Service (AKS) zarządza hostowanym środowiskiem Kubernetes, dzięki czemu można szybko i łatwo wdrażać konteneryzowane aplikacje i zarządzać nimi bez specjalistycznej wiedzy z zakresu aranżacji kontenerów. Eliminuje to również obciążenie trwających operacji i konserwacji dzięki aprowizacji, uaktualnianiu i skalowaniu zasobów na żądanie bez przełączania aplikacji do trybu offline.

Usługa AKS zmniejsza złożoność i nakłady operacyjne związane z zarządzaniem klastrem Kubernetes, przenosząc znaczną część tej odpowiedzialności na platformę Azure. Jako hostowana usługa Kubernetes, platforma Azure obsługuje krytyczne zadania, takie jak monitorowanie kondycji i konserwacja. Ponadto płacisz tylko za węzły agentów w klastrach, a nie dla wzorców. Jako zarządzana usługa Kubernetes, usługa AKS zapewnia:

- Zautomatyzowane uaktualnienia i poprawki wersji Kubernetes.
- Łatwe skalowanie klastra.
- Samonaprawiana płaszczyzna kontroli (Master).
- Oszczędność kosztów — płacisz tylko za uruchomione węzły puli agentów.

Dzięki temu, że platforma Azure obsługuje zarządzanie węzłami w klastrze AKS, nie musisz już ręcznie wykonywać wielu zadań, takich jak uaktualnianie klastra. Ponieważ platforma Azure obsługuje te krytyczne zadania konserwacji, AKS nie zapewnia bezpośredniego dostępu (na przykład do protokołu SSH) do klastra.

Zespoły, które korzystają z AKS, mogą również korzystać z Azure Dev Spaces. Azure Dev Spaces ułatwia zespołom skoncentrowanie się na opracowywaniu i szybkiej iteracji aplikacji mikrousług przez umożliwienie zespołom pracy bezpośrednio z całą architekturą mikrousług lub aplikacją działającą w AKS. Azure Dev Spaces również umożliwia niezależne aktualizowanie części architektury mikrousług w izolacji bez wpływu na resztę klastra AKS lub innych deweloperów.

![Przykład Azure Dev Spaces przepływu pracy](./media/image1-9.gif)

Azure Dev Spaces:

- Minimalizuj czas instalacji komputera lokalnego i wymagania dotyczące zasobów
- Zezwalaj zespołom na szybsze wykonywanie iteracji
- Zmniejsz liczbę środowisk integracji wymaganych przez zespół
- Usuń potrzebę zasymulować niektóre usługi w systemie rozproszonym podczas tworzenia/testowania

[Dowiedz się więcej o Azure Dev Spaces](/azure/dev-spaces/about)

### <a name="azure-virtual-machines"></a>Azure Virtual Machines

Jeśli masz istniejącą aplikację, która będzie wymagała znaczących modyfikacji do uruchomienia w App Service, możesz wybrać Virtual Machines, aby uprościć migrację do chmury. Jednak prawidłowe Konfigurowanie, zabezpieczanie i konserwowanie maszyn wirtualnych wymaga znacznie więcej czasu i wiedza IT w porównaniu z Azure App Service. Jeśli rozważasz platformę Azure Virtual Machines, pamiętaj, aby wziąć pod uwagę trwającą pracę konserwacyjną wymaganą do naprawienia i zaktualizowania środowiska maszyn wirtualnych oraz zarządzania nim. Azure Virtual Machines to infrastruktura jako usługa (IaaS), a App Service to PaaS. Należy również rozważyć, czy wdrażanie aplikacji jako kontenera systemu Windows do Web App for Containers może być możliwością dla Twojego scenariusza.

## <a name="logical-processes"></a>Procesy logiczne

Poszczególne procesy logiczne, które mogą być oddzielone od reszty aplikacji, mogą zostać wdrożone niezależnie w celu Azure Functions w sposób "bezserwerowy". Azure Functions pozwala napisać kod, który jest potrzebny dla danego problemu, bez obaw o działanie aplikacji lub infrastruktury w celu jej uruchomienia. Dostępne są różne języki programowania, w tym C \# , F \# , Node.js, Python i php, dzięki czemu można wybrać najbardziej wydajny język zadania. Podobnie jak w przypadku większości rozwiązań opartych na chmurze, płacisz tylko za wykorzystywany czas i możesz ufać Azure Functions w miarę potrzeb.

## <a name="data"></a>Dane

System Azure oferuje szeroką gamę opcji przechowywania danych, dzięki czemu aplikacja może używać odpowiedniego dostawcy danych dla danych, których dotyczy.

W przypadku transakcyjnych danych relacyjnych usługi Azure SQL Database są najlepszą opcją. W celu uzyskania danych o wysokiej wydajności do odczytu, Redis pamięć podręczna, której kopia zapasowa jest tworzona za pomocą Azure SQL Database jest dobrym rozwiązaniem.

Dane JSON bez struktury mogą być przechowywane na różne sposoby, od SQL Database kolumn do obiektów blob lub tabel w usłudze Azure Storage, aby Azure Cosmos DB. Z tych Azure Cosmos DB oferuje najlepszą funkcję wykonywania zapytań i jest to zalecana opcja dla dużej liczby dokumentów opartych na notacji JSON, które muszą obsługiwać wykonywanie zapytań.

Przejściowe lub oparte na zdarzeniach dane służące do organizowania zachowań aplikacji mogą korzystać z Azure Service Bus lub kolejek usługi Azure Storage. Azure Service Bus zapewnia większą elastyczność i jest to zalecana usługa dla nieuproszczonych komunikatów w ramach i między aplikacjami.

## <a name="architecture-recommendations"></a>Zalecenia dotyczące architektury

Wymagania aplikacji powinny dyktować swoją architekturę. Dostępnych jest wiele różnych usług platformy Azure. Wybranie jednego z nich jest ważną decyzją. Firma Microsoft oferuje galerię architektur referencyjnych, która pomaga identyfikować typowe architektury zoptymalizowane pod kątem typowych scenariuszy. Możesz znaleźć architekturę referencyjną, która jest ściśle mapowana na wymagania aplikacji, lub co najmniej oferuje punkt początkowy.

Na rysunku 11-1 przedstawiono przykładową architekturę referencyjną. Na tym diagramie opisano zalecane podejście architektury dla witryny sieci Web systemu zarządzania zawartością Sitecore zoptymalizowanej pod kątem marketingu.

![Rysunek 11-1](./media/image11-2.png)

**Rysunek 11-1.** Architektura referencyjna witryny internetowej marketingowej Sitecore.

**Odwołania — zalecenia dotyczące hostingu platformy Azure**

- Architektury rozwiązań platformy Azure \
  <https://azure.microsoft.com/solutions/architecture/>

- Podstawowa architektura aplikacji sieci Web platformy Azure \
  <https://docs.microsoft.com/azure/architecture/reference-architectures/app-service-web-app/basic-web-app>

- Wzorce projektowe dla mikrousług \
  <https://docs.microsoft.com/azure/architecture/microservices/design/patterns>

- Przewodnik dewelopera platformy Azure \
  <https://azure.microsoft.com/campaigns/developer-guide/>

- Przegląd Web Apps \
  <https://docs.microsoft.com/azure/app-service/app-service-web-overview>

- Web App for Containers \
  <https://azure.microsoft.com/services/app-service/containers/>

- Wprowadzenie do usługi Azure Kubernetes Service (AKS) \
  <https://docs.microsoft.com/azure/aks/intro-kubernetes>

>[!div class="step-by-step"]
>[Poprzednie](development-process-for-azure.md)
