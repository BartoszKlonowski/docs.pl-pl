---
title: Definiowanie aplikacji z wieloma kontenerami za pomocą pliku docker-compose.yml
description: Jak określić kompozycję mikrousług dla aplikacji wielokontenera z Docker-Compose. yml.
ms.date: 01/30/2020
ms.openlocfilehash: 81303be621da54b7336228585e86d1120a6b7598
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96739792"
---
# <a name="defining-your-multi-container-application-with-docker-composeyml"></a>Definiowanie aplikacji z wieloma kontenerami za pomocą pliku docker-compose.yml

W tym przewodniku plik [Docker-Compose. yml](https://docs.docker.com/compose/compose-file/) został wprowadzony w sekcji [krok 4. Zdefiniuj usługi w Docker-Compose. yml podczas kompilowania aplikacji platformy Docker z obsługą kilku kontenerów](../docker-application-development-process/docker-app-development-workflow.md#step-4-define-your-services-in-docker-composeyml-when-building-a-multi-container-docker-application). Istnieją jednak dodatkowe sposoby używania plików do redagowania platformy Docker, które są bardziej szczegółowe.

Na przykład można jawnie opisać sposób wdrożenia aplikacji wielokontenera w pliku Docker-Compose. yml. Opcjonalnie można również opisać sposób tworzenia niestandardowych obrazów platformy Docker. (Niestandardowe obrazy platformy Docker można także skompilować przy użyciu interfejsu wiersza polecenia platformy Docker).

Zasadniczo należy zdefiniować wszystkie kontenery, które mają zostać wdrożone, oraz określone charakterystyki dla każdego wdrożenia kontenera. Po utworzeniu pliku opisu wdrożenia z zastosowaniem kilku kontenerów można wdrożyć całe rozwiązanie w ramach jednej akcji zorganizowanej przy użyciu interfejsu wiersza polecenia [platformy Docker i utworzyć](https://docs.docker.com/compose/overview/) je w sposób przezroczysty w programie Visual Studio. W przeciwnym razie należy użyć interfejsu wiersza polecenia platformy Docker, aby wdrożyć kontener między kontenerami w wielu krokach przy użyciu `docker run` polecenia z wiersza poleceń. W związku z tym każda usługa zdefiniowana w Docker-Compose. yml musi określać dokładnie jeden obraz lub kompilację. Inne klucze są opcjonalne i są analogiczne do ich `docker run` odpowiedników w wierszu polecenia.

Następujący kod YAML jest definicją możliwego globalnie, ale pojedynczego pliku Docker-Compose. yml dla przykładu eShopOnContainers. To nie jest rzeczywisty plik "Docker-Zredaguj" z eShopOnContainers. Zamiast tego jest to wersja uproszczona i skonsolidowana w jednym pliku, co nie jest najlepszym sposobem na korzystanie z plików do redagowania oprogramowania Docker, co zostanie wyjaśnione później.

```yml
version: '3.4'

services:
  webmvc:
    image: eshop/webmvc
    environment:
      - CatalogUrl=http://catalog-api
      - OrderingUrl=http://ordering-api
      - BasketUrl=http://basket-api
    ports:
      - "5100:80"
    depends_on:
      - catalog-api
      - ordering-api
      - basket-api

  catalog-api:
    image: eshop/catalog-api
    environment:
      - ConnectionString=Server=sqldata;Initial Catalog=CatalogData;User Id=sa;Password=[PLACEHOLDER]
    expose:
      - "80"
    ports:
      - "5101:80"
    #extra hosts can be used for standalone SQL Server or services at the dev PC
    extra_hosts:
      - "CESARDLSURFBOOK:10.0.75.1"
    depends_on:
      - sqldata

  ordering-api:
    image: eshop/ordering-api
    environment:
      - ConnectionString=Server=sqldata;Database=Services.OrderingDb;User Id=sa;Password=[PLACEHOLDER]
    ports:
      - "5102:80"
    #extra hosts can be used for standalone SQL Server or services at the dev PC
    extra_hosts:
      - "CESARDLSURFBOOK:10.0.75.1"
    depends_on:
      - sqldata

  basket-api:
    image: eshop/basket-api
    environment:
      - ConnectionString=sqldata
    ports:
      - "5103:80"
    depends_on:
      - sqldata

  sqldata:
    environment:
      - SA_PASSWORD=[PLACEHOLDER]
      - ACCEPT_EULA=Y
    ports:
      - "5434:1433"

  basketdata:
    image: redis
```

Kluczem głównym tego pliku są usługi. W tym kluczu należy zdefiniować usługi, które mają zostać wdrożone i uruchomione po wykonaniu `docker-compose up` polecenia lub podczas wdrażania z programu Visual Studio przy użyciu tego pliku Docker-Compose. yml. W takim przypadku plik Docker-Compose. yml ma zdefiniowane wiele usług, zgodnie z opisem w poniższej tabeli.

| Nazwa usługi | Opis |
|--------------|-------------|
| webmvc       | Kontener obejmujący aplikację ASP.NET Core MVC korzystającą z mikrousług po stronie serwera (C)\#|
| Katalog — interfejs API  | Kontener, w tym wykaz ASP.NET Core sieci Web API mikrousługi |
| Porządkowanie — API | Kontener obejmujący porządkowanie ASP.NET Core sieci Web API mikrousług |
| dane SQLdata     | Kontener SQL Server dla systemu Linux, który utrzymuje bazy danych mikrousług |
| koszyk — interfejs API   | Kontener z koszykiem ASP.NET Core mikrousługi interfejsu Web API |
| basketdata  | Kontener z uruchomioną usługą pamięci podręcznej REDIS z bazą danych koszyka jako pamięć podręczną REDIS |

### <a name="a-simple-web-service-api-container"></a>Prosty kontener interfejsu API usługi sieci Web

Skoncentrowanie się na pojedynczym kontenerze — kontenerem katalogu interfejsu API — mikrousługa ma prostą definicję:

```yml
  catalog-api:
    image: eshop/catalog-api
    environment:
      - ConnectionString=Server=sqldata;Initial Catalog=CatalogData;User Id=sa;Password=[PLACEHOLDER]
    expose:
      - "80"
    ports:
      - "5101:80"
    #extra hosts can be used for standalone SQL Server or services at the dev PC
    extra_hosts:
      - "CESARDLSURFBOOK:10.0.75.1"
    depends_on:
      - sqldata
```

Ta usługa kontenerów ma następującą konfigurację podstawową:

- Jest on oparty na niestandardowym obrazie **interfejsu API eshop/Catalog** . Dla uproszczenia w pliku nie ma ustawienia Build: Key. Oznacza to, że obraz musi być wcześniej skompilowany (z kompilacją Docker) lub pobrany (za pomocą polecenia docker pull) z dowolnego rejestru platformy Docker.

- Definiuje zmienną środowiskową o nazwie ConnectionString z parametrami połączenia, które mają być używane przez Entity Framework w celu uzyskania dostępu do wystąpienia SQL Server zawierającego model danych wykazu. W takim przypadku ten sam kontener SQL Server zawiera wiele baz danych. W związku z tym potrzebna jest mniej pamięci na komputerze deweloperskim dla platformy Docker. Można jednak również wdrożyć jeden kontener SQL Server dla każdej bazy danych mikrousług.

- Nazwa SQL Server to **SQLdata**, która jest taka sama jak nazwa używana dla kontenera, w którym działa wystąpienie SQL Server dla systemu Linux. Jest to wygodne: możliwość użycia tego rozwiązania rozpoznawania nazw (wewnętrznego dla hosta platformy Docker) spowoduje rozpoznanie adresu sieciowego, dzięki czemu nie trzeba znać wewnętrznego adresu IP dla kontenerów, do których uzyskujesz dostęp z innych kontenerów.

Ponieważ parametry połączenia są zdefiniowane przez zmienną środowiskową, można ustawić tę zmienną za pomocą innego mechanizmu i w innym czasie. Na przykład można ustawić inne parametry połączenia podczas wdrażania w środowisku produkcyjnym na finalnych hostach lub przez wykonanie ich z potoków ciągłej integracji/ciągłego dostarczania w Azure DevOps Services lub w preferowanym systemie DevOps.

- Udostępnia port 80 na potrzeby wewnętrznego dostępu do usługi **katalogowej interfejsu API** w ramach hosta platformy Docker. Host jest obecnie maszyną wirtualną z systemem Linux, ponieważ jest oparta na obrazie platformy Docker dla systemu Linux, ale zamiast tego można skonfigurować kontener do uruchamiania w obrazie Windows.

- Przekazuje on uwidoczniony port 80 w kontenerze do portu 5101 na komputerze hosta platformy Docker (maszyna wirtualna systemu Linux).

- Łączy usługę sieci Web z usługą **SQLdata** Service (wystąpienie SQL Server dla bazy danych systemu Linux działającej w kontenerze). Po określeniu tej zależności kontener katalogu interfejsu API nie zostanie uruchomiony do momentu rozpoczęcia już kontenera SQLdata. jest to ważne, ponieważ usługa Catalog-API musi mieć najpierw bazę danych SQL Server. Jednak tego rodzaju zależność kontenera jest zbyt mała w wielu przypadkach, ponieważ platforma Docker sprawdza tylko na poziomie kontenera. Czasami usługa (w tym przypadku SQL Server) nadal może nie być gotowa, dlatego zaleca się wdrożenie logiki ponawiania przy użyciu wykładniczej wycofywania w mikrousługach klienta. W ten sposób, jeśli kontener zależności nie jest gotowy przez krótki czas, aplikacja nadal będzie odporna na błędy.

- Jest skonfigurowany tak, aby zezwalał na dostęp do serwerów zewnętrznych: \_ ustawienie dodatkowe hosty umożliwia dostęp do zewnętrznych serwerów lub maszyn poza hostem platformy Docker (czyli poza domyślną maszyną wirtualną z systemem Linux, która jest hostem platformy Docker), takim jak lokalne wystąpienie SQL Server na komputerze deweloperskim.

Istnieją również inne, bardziej zaawansowane `docker-compose.yml` Ustawienia, które będziemy omawiać w poniższych sekcjach.

### <a name="using-docker-compose-files-to-target-multiple-environments"></a>Korzystanie z aplikacji platformy Docker — tworzenie plików przeznaczonych dla wielu środowisk

`docker-compose.*.yml`Pliki są plikami definicji i mogą być używane przez wiele infrastruktur, które rozumieją ten format. Najbardziej prostym narzędziem jest polecenie Docker-Zredaguj.

W związku z tym przy użyciu polecenia Docker-Zredaguj można wskazać następujące główne scenariusze.

#### <a name="development-environments"></a>Środowiska deweloperskie

Podczas tworzenia aplikacji należy mieć możliwość uruchamiania aplikacji w izolowanym środowisku programistycznym. Aby utworzyć środowisko lub program Visual Studio, w którym jest używana funkcja Docker-Zredaguj w obszarze okładek, można użyć polecenia CLI-Create.

Plik Docker-Compose. yml umożliwia skonfigurowanie i udokumentowanie wszystkich zależności usług aplikacji (innych usług, pamięci podręcznej, baz danych, kolejek itp.). Używając interfejsu wiersza polecenia platformy Docker — tworzenie, można utworzyć i uruchomić jeden lub więcej kontenerów dla każdej zależności za pomocą jednego polecenia (platforma Docker — tworzenie).

Pliki Docker-Compose. yml są plikami konfiguracji interpretowanymi przez aparat platformy Docker, ale również stanowią wygodne pliki dokumentacji dotyczące kompozycji aplikacji wielokontenerowych.

#### <a name="testing-environments"></a>Środowiska testowe

Ważnym elementem procesu ciągłego wdrażania (CD) lub ciągłej integracji są testy jednostkowe i testy integracji. Te zautomatyzowane testy wymagają środowiska izolowanego, przez co użytkownicy nie mają wpływu ani żadnej innej zmiany w danych aplikacji.

Za pomocą Docker Compose można utworzyć i zniszczyć środowisko izolowane bardzo łatwo w kilku poleceniach z poziomu wiersza polecenia lub skryptów, takich jak następujące polecenia:

```console
docker-compose -f docker-compose.yml -f docker-compose-test.override.yml up -d
./run_unit_tests
docker-compose -f docker-compose.yml -f docker-compose-test.override.yml down
```

#### <a name="production-deployments"></a>Wdrożenia produkcyjne

Można również użyć tworzenia do wdrożenia w zdalnym aparacie platformy Docker. Typowym przypadkiem jest wdrożenie do jednego wystąpienia hosta platformy Docker (na przykład produkcyjnej maszyny wirtualnej lub serwera z obsługą [maszyny platformy Docker](https://docs.docker.com/machine/overview/)).

Jeśli używasz innego programu Orchestrator (Service Fabric platformy Azure, Kubernetes itp.), może być konieczne dodanie ustawień konfiguracji i metadanych, takich jak w Docker-Compose. yml, ale w formacie wymaganym przez inne koordynatora.

W każdym przypadku platforma Docker — tworzenie to wygodne narzędzie i format metadanych służący do tworzenia, testowania i produkcji przepływów pracy, chociaż przepływ pracy może się różnić w zależności od używanego programu Orchestrator.

### <a name="using-multiple-docker-compose-files-to-handle-several-environments"></a>Używanie wielu plików w programie Docker do obsługi kilku środowisk

W przypadku określania różnych środowisk należy używać wielu plików redagowania. Pozwala to utworzyć wiele wariantów konfiguracji w zależności od środowiska.

#### <a name="overriding-the-base-docker-compose-file"></a>Zastępowanie podstawowego pliku platformy Docker — redagowanie

Można użyć pojedynczego pliku Docker-Compose. yml, jak w przykładach uproszczonych przedstawionych w poprzednich sekcjach. Jednak nie jest to zalecane w przypadku większości aplikacji.

Domyślnie Redaguj odczytuje dwa pliki, Docker-Compose. yml i opcjonalny plik Docker-Compose. override. yml. Jak pokazano na rysunku 6-11, gdy korzystasz z programu Visual Studio i włączasz obsługę platformy Docker, program Visual Studio tworzy również dodatkowy plik Docker-Compose. vs. Debug. g. yml do debugowania aplikacji, można przyjrzeć się temu plikowi w folderze " \\ Docker" \\ w folderze głównym rozwiązania.

![Pliki w projekcie platformy Docker.](./media/multi-container-applications-docker-compose/docker-compose-file-visual-studio.png)

**Rysunek 6-11**. Docker — tworzenie plików w programie Visual Studio 2019

Struktura pliku **platformy Docker — tworzenie** projektu:

- *. dockerignore* — służy do ignorowania plików
- *Docker-Compose. yml* — używany do tworzenia mikrousług
- *Docker-Compose. override. yml* — służy do konfigurowania środowiska mikrousług

Można edytować plik platformy Docker z dowolnym edytorem, takim jak Visual Studio Code lub subwapno, i uruchamiać aplikację przy użyciu polecenia Docker-Zredaguj w górę.

Zgodnie z Konwencją plik Docker-Compose. yml zawiera konfigurację podstawową i inne ustawienia statyczne. Oznacza to, że konfiguracja usługi nie powinna się zmieniać w zależności od używanego środowiska wdrażania.

Plik Docker-Compose. override. yml, jak jego nazwa sugeruje, zawiera ustawienia konfiguracji, które zastępują konfigurację podstawową, na przykład konfigurację, która zależy od środowiska wdrażania. Można również mieć wiele plików przesłonięć o różnych nazwach. Pliki przesłonięć zwykle zawierają dodatkowe informacje, które są konieczne dla aplikacji, ale specyficzne dla środowiska lub wdrożenia.

#### <a name="targeting-multiple-environments"></a>Kierowanie wielu środowisk

Typowym przypadkiem użycia jest definiowanie wielu plików redagowania, aby można było kierować wiele środowisk, takich jak produkcja, przemieszczanie, CI lub programowanie. Aby obsłużyć te różnice, można podzielić konfigurację redagowania na wiele plików, jak pokazano na rysunku 6-12.

![Diagram trzech plików do redagowania platformy Docker, ustawiony w celu zastąpienia pliku podstawowego.](./media/multi-container-applications-docker-compose/multiple-docker-compose-files-override-base.png)

**Rysunek 6-12**. Wiele plików programu Docker — tworzenie przesłania wartości w podstawowym pliku Docker-Compose. yml

Można połączyć wiele plików Docker-Compose*. yml, aby obsługiwać różne środowiska. Zaczynasz od podstawowego pliku Docker-Compose. yml. Ten plik podstawowy zawiera podstawowe lub statyczne ustawienia konfiguracji, które nie zmieniają się w zależności od środowiska. Na przykład aplikacja eShopOnContainers ma następujący plik Docker-Compose. yml (uproszczony z mniejszą liczbą usług) jako plik podstawowy.

```yml
#docker-compose.yml (Base)
version: '3.4'
services:
  basket-api:
    image: eshop/basket-api:${TAG:-latest}
    build:
      context: .
      dockerfile: src/Services/Basket/Basket.API/Dockerfile
    depends_on:
      - basketdata
      - identity-api
      - rabbitmq

  catalog-api:
    image: eshop/catalog-api:${TAG:-latest}
    build:
      context: .
      dockerfile: src/Services/Catalog/Catalog.API/Dockerfile
    depends_on:
      - sqldata
      - rabbitmq

  marketing-api:
    image: eshop/marketing-api:${TAG:-latest}
    build:
      context: .
      dockerfile: src/Services/Marketing/Marketing.API/Dockerfile
    depends_on:
      - sqldata
      - nosqldata
      - identity-api
      - rabbitmq

  webmvc:
    image: eshop/webmvc:${TAG:-latest}
    build:
      context: .
      dockerfile: src/Web/WebMVC/Dockerfile
    depends_on:
      - catalog-api
      - ordering-api
      - identity-api
      - basket-api
      - marketing-api

  sqldata:
    image: mcr.microsoft.com/mssql/server:2017-latest

  nosqldata:
    image: mongo

  basketdata:
    image: redis

  rabbitmq:
    image: rabbitmq:3-management

```

Wartości w podstawowym pliku Docker-Compose. yml nie należy zmieniać ze względu na inne docelowe środowiska wdrażania.

W przypadku określenia usługi webmvc na przykład można zobaczyć, jak te informacje są znacznie takie same niezależnie od tego, jakie środowisko może być ukierunkowane. Masz następujące informacje:

- Nazwa usługi: webmvc.

- Obraz niestandardowy kontenera: eshop/webmvc.

- Polecenie służące do kompilowania niestandardowego obrazu platformy Docker wskazujący, którego pliku dockerfile użyć.

- Zależności od innych usług, więc ten kontener nie zostanie uruchomiony do momentu rozpoczęcia innych kontenerów zależności.

Możesz mieć dodatkową konfigurację, ale ważnym punktem jest to, że w podstawowym pliku Docker-Compose. yml, wystarczy ustawić informacje wspólne w różnych środowiskach. Następnie w Docker-Compose. override. yml lub podobnych plikach do produkcji lub przemieszczania należy umieścić konfigurację specyficzną dla każdego środowiska.

Zazwyczaj Docker-Compose. override. yml jest używany w środowisku deweloperskim, jak w poniższym przykładzie z eShopOnContainers:

```yml
#docker-compose.override.yml (Extended config for DEVELOPMENT env.)
version: '3.4'

services:
# Simplified number of services here:

  basket-api:
    environment:
      - ASPNETCORE_ENVIRONMENT=Development
      - ASPNETCORE_URLS=http://0.0.0.0:80
      - ConnectionString=${ESHOP_AZURE_REDIS_BASKET_DB:-basketdata}
      - identityUrl=http://identity-api
      - IdentityUrlExternal=http://${ESHOP_EXTERNAL_DNS_NAME_OR_IP}:5105
      - EventBusConnection=${ESHOP_AZURE_SERVICE_BUS:-rabbitmq}
      - EventBusUserName=${ESHOP_SERVICE_BUS_USERNAME}
      - EventBusPassword=${ESHOP_SERVICE_BUS_PASSWORD}
      - AzureServiceBusEnabled=False
      - ApplicationInsights__InstrumentationKey=${INSTRUMENTATION_KEY}
      - OrchestratorType=${ORCHESTRATOR_TYPE}
      - UseLoadTest=${USE_LOADTEST:-False}

    ports:
      - "5103:80"

  catalog-api:
    environment:
      - ASPNETCORE_ENVIRONMENT=Development
      - ASPNETCORE_URLS=http://0.0.0.0:80
      - ConnectionString=${ESHOP_AZURE_CATALOG_DB:-Server=sqldata;Database=Microsoft.eShopOnContainers.Services.CatalogDb;User Id=sa;Password=[PLACEHOLDER]}
      - PicBaseUrl=${ESHOP_AZURE_STORAGE_CATALOG_URL:-http://localhost:5202/api/v1/catalog/items/[0]/pic/}
      - EventBusConnection=${ESHOP_AZURE_SERVICE_BUS:-rabbitmq}
      - EventBusUserName=${ESHOP_SERVICE_BUS_USERNAME}
      - EventBusPassword=${ESHOP_SERVICE_BUS_PASSWORD}
      - AzureStorageAccountName=${ESHOP_AZURE_STORAGE_CATALOG_NAME}
      - AzureStorageAccountKey=${ESHOP_AZURE_STORAGE_CATALOG_KEY}
      - UseCustomizationData=True
      - AzureServiceBusEnabled=False
      - AzureStorageEnabled=False
      - ApplicationInsights__InstrumentationKey=${INSTRUMENTATION_KEY}
      - OrchestratorType=${ORCHESTRATOR_TYPE}
    ports:
      - "5101:80"

  marketing-api:
    environment:
      - ASPNETCORE_ENVIRONMENT=Development
      - ASPNETCORE_URLS=http://0.0.0.0:80
      - ConnectionString=${ESHOP_AZURE_MARKETING_DB:-Server=sqldata;Database=Microsoft.eShopOnContainers.Services.MarketingDb;User Id=sa;Password=[PLACEHOLDER]}
      - MongoConnectionString=${ESHOP_AZURE_COSMOSDB:-mongodb://nosqldata}
      - MongoDatabase=MarketingDb
      - EventBusConnection=${ESHOP_AZURE_SERVICE_BUS:-rabbitmq}
      - EventBusUserName=${ESHOP_SERVICE_BUS_USERNAME}
      - EventBusPassword=${ESHOP_SERVICE_BUS_PASSWORD}
      - identityUrl=http://identity-api
      - IdentityUrlExternal=http://${ESHOP_EXTERNAL_DNS_NAME_OR_IP}:5105
      - CampaignDetailFunctionUri=${ESHOP_AZUREFUNC_CAMPAIGN_DETAILS_URI}
      - PicBaseUrl=${ESHOP_AZURE_STORAGE_MARKETING_URL:-http://localhost:5110/api/v1/campaigns/[0]/pic/}
      - AzureStorageAccountName=${ESHOP_AZURE_STORAGE_MARKETING_NAME}
      - AzureStorageAccountKey=${ESHOP_AZURE_STORAGE_MARKETING_KEY}
      - AzureServiceBusEnabled=False
      - AzureStorageEnabled=False
      - ApplicationInsights__InstrumentationKey=${INSTRUMENTATION_KEY}
      - OrchestratorType=${ORCHESTRATOR_TYPE}
      - UseLoadTest=${USE_LOADTEST:-False}
    ports:
      - "5110:80"

  webmvc:
    environment:
      - ASPNETCORE_ENVIRONMENT=Development
      - ASPNETCORE_URLS=http://0.0.0.0:80
      - PurchaseUrl=http://webshoppingapigw
      - IdentityUrl=http://10.0.75.1:5105
      - MarketingUrl=http://webmarketingapigw
      - CatalogUrlHC=http://catalog-api/hc
      - OrderingUrlHC=http://ordering-api/hc
      - IdentityUrlHC=http://identity-api/hc
      - BasketUrlHC=http://basket-api/hc
      - MarketingUrlHC=http://marketing-api/hc
      - PaymentUrlHC=http://payment-api/hc
      - SignalrHubUrl=http://${ESHOP_EXTERNAL_DNS_NAME_OR_IP}:5202
      - UseCustomizationData=True
      - ApplicationInsights__InstrumentationKey=${INSTRUMENTATION_KEY}
      - OrchestratorType=${ORCHESTRATOR_TYPE}
      - UseLoadTest=${USE_LOADTEST:-False}
    ports:
      - "5100:80"
  sqldata:
    environment:
      - SA_PASSWORD=[PLACEHOLDER]
      - ACCEPT_EULA=Y
    ports:
      - "5433:1433"
  nosqldata:
    ports:
      - "27017:27017"
  basketdata:
    ports:
      - "6379:6379"
  rabbitmq:
    ports:
      - "15672:15672"
      - "5672:5672"

```

W tym przykładzie konfiguracja przesłonięcia rozwoju uwidacznia niektóre porty hosta, definiuje zmienne środowiskowe z adresami URL przekierowania i określa parametry połączenia dla środowiska deweloperskiego. Te ustawienia są przeznaczone tylko dla środowiska deweloperskiego.

Gdy uruchamiasz `docker-compose up` (lub uruchamiasz ją z programu Visual Studio), polecenie odczytuje przesłonięcia automatycznie tak, jakby były scalane oba pliki.

Załóżmy, że chcesz, aby inny plik redagowania był używany w środowisku produkcyjnym, z innymi wartościami konfiguracji, portami lub parametrami połączenia. Można utworzyć inny plik przesłonięcia, taki jak plik o `docker-compose.prod.yml` różnych ustawieniach i zmiennych środowiskowych. Ten plik może być przechowywany w innym repozytorium Git lub zarządzany i zabezpieczony przez inny zespół.

#### <a name="how-to-deploy-with-a-specific-override-file"></a>Jak wdrożyć z określonym plikiem przesłonięcia

Aby użyć wielu plików przesłonięć lub zastąpić plik z inną nazwą, można użyć opcji-f z poleceniem Docker-Zredaguj i określić pliki. Redaguj scala pliki w kolejności określonej w wierszu polecenia. Poniższy przykład pokazuje, jak wdrożyć przy użyciu plików przesłonięć.

```console
docker-compose -f docker-compose.yml -f docker-compose.prod.yml up -d
```

#### <a name="using-environment-variables-in-docker-compose-files"></a>Używanie zmiennych środowiskowych w programie Docker — tworzenie plików

Jest to wygodne, szczególnie w środowiskach produkcyjnych, aby można było uzyskać informacje o konfiguracji ze zmiennych środowiskowych, jak pokazano w poprzednich przykładach. Można odwołać się do zmiennej środowiskowej w plikach tworzących platformy Docker przy użyciu składni $ {MY \_ var}. Poniższy wiersz z pliku Docker-Compose. prod. yml pokazuje, jak odwołać się do wartości zmiennej środowiskowej.

```yml
IdentityUrl=http://${ESHOP_PROD_EXTERNAL_DNS_NAME_OR_IP}:5105
```

Zmienne środowiskowe są tworzone i inicjowane na różne sposoby, w zależności od środowiska hosta (Linux, Windows, klaster w chmurze itp.). Jednak wygodne podejście polega na użyciu pliku. env. Pliki do tworzenia platformy Docker obsługują deklarowanie domyślnych zmiennych środowiskowych w pliku ENV. Te wartości zmiennych środowiskowych są wartościami domyślnymi. Mogą jednak zostać przesłonięte przez wartości, które mogą być zdefiniowane w poszczególnych środowiskach (system operacyjny hosta lub zmienne środowiskowe z klastra). Ten plik ENV zostanie umieszczony w folderze, w którym jest wykonywane polecenie Docker-redagowanie.

W poniższym przykładzie przedstawiono plik. env, taki jak plik [ENV](https://github.com/dotnet-architecture/eShopOnContainers/blob/master/.env) dla aplikacji eShopOnContainers.

```sh
# .env file

ESHOP_EXTERNAL_DNS_NAME_OR_IP=localhost

ESHOP_PROD_EXTERNAL_DNS_NAME_OR_IP=10.121.122.92
```

Docker-redagowanie oczekuje, że każdy wiersz w pliku ENV ma być w formacie \<variable\> = \<value\> .

Wartości ustawione w środowisku wykonawczym zawsze przesłonią wartości zdefiniowane wewnątrz pliku ENV. W podobny sposób wartości przekazane za pośrednictwem argumentów wiersza polecenia również przesłaniają wartości domyślne ustawione w pliku ENV.

#### <a name="additional-resources"></a>Dodatkowe zasoby

- **Omówienie Docker Compose** \
    <https://docs.docker.com/compose/overview/>

- **Wiele plików redagowania** \
    [https://docs.docker.com/compose/extends/\#multiple-compose-files](https://docs.docker.com/compose/extends/#multiple-compose-files)

### <a name="building-optimized-aspnet-core-docker-images"></a>Kompilowanie zoptymalizowanych obrazów ASP.NET Core Docker

Jeśli eksplorujesz platformę Docker i platformę .NET Core w źródłach internetowych, znajdziesz wieloetapowe dockerfile, który pokazuje prostotę tworzenia obrazu platformy Docker przez skopiowanie źródła do kontenera. Te przykłady sugerują, że przy użyciu prostej konfiguracji możesz mieć obraz platformy Docker ze środowiskiem spakowanym z aplikacją. Poniższy przykład pokazuje prostą pliku dockerfile w tej szyjce.

```dockerfile
FROM mcr.microsoft.com/dotnet/sdk:3.1
WORKDIR /app
ENV ASPNETCORE_URLS http://+:80
EXPOSE 80
COPY . .
RUN dotnet restore
ENTRYPOINT ["dotnet", "run"]
```

Pliku dockerfile taka będzie działała. Można jednak znacznie zoptymalizować obrazy, w szczególności obrazy produkcyjne.

W modelu kontenerów i mikrousług są ciągle uruchamiane kontenery. Typowy sposób używania kontenerów nie powoduje ponownego uruchomienia kontenera uśpionego, ponieważ kontener jest jednorazowy. Koordynatorzy (na przykład Kubernetes i Azure Service Fabric) po prostu tworzą nowe wystąpienia obrazów. Oznacza to, że trzeba zoptymalizować przez wstępne skompilowanie aplikacji, aby proces tworzenia wystąpienia był szybszy. Po rozpoczęciu kontenera powinien być gotowy do uruchomienia. Nie należy przywracać i kompilować w czasie wykonywania za pomocą `dotnet restore` `dotnet build` poleceń i interfejsu wiersza polecenia, które mogą być widoczne w wpisach w blogu na temat platformy .NET Core i platformy Docker.

Zespół platformy .NET wykonuje ważne prace w celu udostępnienia platformy .NET Core i ASP.NET Core platformy zoptymalizowanej pod kątem kontenerów. Jest to nie tylko platforma .NET Core z małą ilością pamięci. zespół koncentruje się na zoptymalizowanych obrazach platformy Docker dla trzech głównych scenariuszy i publikuje je w rejestrze usługi Docker Hub na platformie *dotnet/Core*, począwszy od wersji 2,1:

1. **Programowanie**: priorytet to możliwość szybkiego wykonywania iteracji i debugowania zmian oraz w przypadku, gdy rozmiar jest pomocniczy.

2. **Kompilacja**: priorytet kompiluje aplikację, a obraz zawiera dane binarne i inne zależności w celu zoptymalizowania plików binarnych.

3. **Produkcja**: fokus jest szybkim wdrożeniem i początkiem kontenerów, dzięki czemu obrazy te są ograniczone do plików binarnych i zawartości wymaganych do uruchomienia aplikacji.

Zespół .NET oferuje cztery podstawowe warianty w programie [dotnet/Core](https://hub.docker.com/_/microsoft-dotnet/) (w usłudze Docker Hub):

1. **zestaw SDK**: na potrzeby scenariuszy tworzenia i kompilowania
1. **ASPNET**: for ASP.NET — scenariusze produkcji
1. **środowisko uruchomieniowe**: dla scenariuszy produkcyjnych programu .NET
1. **środowisko uruchomieniowe — deps**: dla scenariuszy produkcyjnych [aplikacji samodzielnych](../../../core/deploying/index.md#publish-self-contained)

W celu przyspieszenia uruchamiania obrazy środowiska uruchomieniowego również automatycznie ustawiają \_ adresy URL aspnetcore na porcie 80 i używają narzędzia NGen do tworzenia pamięci podręcznej obrazów natywnych zestawów.

#### <a name="additional-resources"></a>Dodatkowe zasoby

- **Kompilowanie zoptymalizowanych obrazów platformy Docker za pomocą ASP.NET Core**
  <https://docs.microsoft.com/archive/blogs/stevelasker/building-optimized-docker-images-with-asp-net-core>

- **Kompilowanie obrazów platformy Docker dla aplikacji platformy .NET Core**
  [https://docs.microsoft.com/dotnet/core/docker/building-net-docker-images](/aspnet/core/host-and-deploy/docker/building-net-docker-images)

> [!div class="step-by-step"]
> [Poprzedni](data-driven-crud-microservice.md) 
>  [Dalej](database-server-container.md)
