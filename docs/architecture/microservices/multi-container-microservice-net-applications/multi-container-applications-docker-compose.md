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
# <a name="defining-your-multi-container-application-with-docker-composeyml"></a><span data-ttu-id="d2571-103">Definiowanie aplikacji z wieloma kontenerami za pomocą pliku docker-compose.yml</span><span class="sxs-lookup"><span data-stu-id="d2571-103">Defining your multi-container application with docker-compose.yml</span></span>

<span data-ttu-id="d2571-104">W tym przewodniku plik [Docker-Compose. yml](https://docs.docker.com/compose/compose-file/) został wprowadzony w sekcji [krok 4. Zdefiniuj usługi w Docker-Compose. yml podczas kompilowania aplikacji platformy Docker z obsługą kilku kontenerów](../docker-application-development-process/docker-app-development-workflow.md#step-4-define-your-services-in-docker-composeyml-when-building-a-multi-container-docker-application).</span><span class="sxs-lookup"><span data-stu-id="d2571-104">In this guide, the [docker-compose.yml](https://docs.docker.com/compose/compose-file/) file was introduced in the section [Step 4. Define your services in docker-compose.yml when building a multi-container Docker application](../docker-application-development-process/docker-app-development-workflow.md#step-4-define-your-services-in-docker-composeyml-when-building-a-multi-container-docker-application).</span></span> <span data-ttu-id="d2571-105">Istnieją jednak dodatkowe sposoby używania plików do redagowania platformy Docker, które są bardziej szczegółowe.</span><span class="sxs-lookup"><span data-stu-id="d2571-105">However, there are additional ways to use the docker-compose files that are worth exploring in further detail.</span></span>

<span data-ttu-id="d2571-106">Na przykład można jawnie opisać sposób wdrożenia aplikacji wielokontenera w pliku Docker-Compose. yml.</span><span class="sxs-lookup"><span data-stu-id="d2571-106">For example, you can explicitly describe how you want to deploy your multi-container application in the docker-compose.yml file.</span></span> <span data-ttu-id="d2571-107">Opcjonalnie można również opisać sposób tworzenia niestandardowych obrazów platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="d2571-107">Optionally, you can also describe how you are going to build your custom Docker images.</span></span> <span data-ttu-id="d2571-108">(Niestandardowe obrazy platformy Docker można także skompilować przy użyciu interfejsu wiersza polecenia platformy Docker).</span><span class="sxs-lookup"><span data-stu-id="d2571-108">(Custom Docker images can also be built with the Docker CLI.)</span></span>

<span data-ttu-id="d2571-109">Zasadniczo należy zdefiniować wszystkie kontenery, które mają zostać wdrożone, oraz określone charakterystyki dla każdego wdrożenia kontenera.</span><span class="sxs-lookup"><span data-stu-id="d2571-109">Basically, you define each of the containers you want to deploy plus certain characteristics for each container deployment.</span></span> <span data-ttu-id="d2571-110">Po utworzeniu pliku opisu wdrożenia z zastosowaniem kilku kontenerów można wdrożyć całe rozwiązanie w ramach jednej akcji zorganizowanej przy użyciu interfejsu wiersza polecenia [platformy Docker i utworzyć](https://docs.docker.com/compose/overview/) je w sposób przezroczysty w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d2571-110">Once you have a multi-container deployment description file, you can deploy the whole solution in a single action orchestrated by the [docker-compose up](https://docs.docker.com/compose/overview/) CLI command, or you can deploy it transparently from Visual Studio.</span></span> <span data-ttu-id="d2571-111">W przeciwnym razie należy użyć interfejsu wiersza polecenia platformy Docker, aby wdrożyć kontener między kontenerami w wielu krokach przy użyciu `docker run` polecenia z wiersza poleceń.</span><span class="sxs-lookup"><span data-stu-id="d2571-111">Otherwise, you would need to use the Docker CLI to deploy container-by-container in multiple steps by using the `docker run` command from the command line.</span></span> <span data-ttu-id="d2571-112">W związku z tym każda usługa zdefiniowana w Docker-Compose. yml musi określać dokładnie jeden obraz lub kompilację.</span><span class="sxs-lookup"><span data-stu-id="d2571-112">Therefore, each service defined in docker-compose.yml must specify exactly one image or build.</span></span> <span data-ttu-id="d2571-113">Inne klucze są opcjonalne i są analogiczne do ich `docker run` odpowiedników w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="d2571-113">Other keys are optional, and are analogous to their `docker run` command-line counterparts.</span></span>

<span data-ttu-id="d2571-114">Następujący kod YAML jest definicją możliwego globalnie, ale pojedynczego pliku Docker-Compose. yml dla przykładu eShopOnContainers.</span><span class="sxs-lookup"><span data-stu-id="d2571-114">The following YAML code is the definition of a possible global but single docker-compose.yml file for the eShopOnContainers sample.</span></span> <span data-ttu-id="d2571-115">To nie jest rzeczywisty plik "Docker-Zredaguj" z eShopOnContainers.</span><span class="sxs-lookup"><span data-stu-id="d2571-115">This is not the actual docker-compose file from eShopOnContainers.</span></span> <span data-ttu-id="d2571-116">Zamiast tego jest to wersja uproszczona i skonsolidowana w jednym pliku, co nie jest najlepszym sposobem na korzystanie z plików do redagowania oprogramowania Docker, co zostanie wyjaśnione później.</span><span class="sxs-lookup"><span data-stu-id="d2571-116">Instead, it is a simplified and consolidated version in a single file, which is not the best way to work with docker-compose files, as will be explained later.</span></span>

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

<span data-ttu-id="d2571-117">Kluczem głównym tego pliku są usługi.</span><span class="sxs-lookup"><span data-stu-id="d2571-117">The root key in this file is services.</span></span> <span data-ttu-id="d2571-118">W tym kluczu należy zdefiniować usługi, które mają zostać wdrożone i uruchomione po wykonaniu `docker-compose up` polecenia lub podczas wdrażania z programu Visual Studio przy użyciu tego pliku Docker-Compose. yml.</span><span class="sxs-lookup"><span data-stu-id="d2571-118">Under that key, you define the services you want to deploy and run when you execute the `docker-compose up` command or when you deploy from Visual Studio by using this docker-compose.yml file.</span></span> <span data-ttu-id="d2571-119">W takim przypadku plik Docker-Compose. yml ma zdefiniowane wiele usług, zgodnie z opisem w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="d2571-119">In this case, the docker-compose.yml file has multiple services defined, as described in the following table.</span></span>

| <span data-ttu-id="d2571-120">Nazwa usługi</span><span class="sxs-lookup"><span data-stu-id="d2571-120">Service name</span></span> | <span data-ttu-id="d2571-121">Opis</span><span class="sxs-lookup"><span data-stu-id="d2571-121">Description</span></span> |
|--------------|-------------|
| <span data-ttu-id="d2571-122">webmvc</span><span class="sxs-lookup"><span data-stu-id="d2571-122">webmvc</span></span>       | <span data-ttu-id="d2571-123">Kontener obejmujący aplikację ASP.NET Core MVC korzystającą z mikrousług po stronie serwera (C)\#</span><span class="sxs-lookup"><span data-stu-id="d2571-123">Container including the ASP.NET Core MVC application consuming the microservices from server-side C\#</span></span>|
| <span data-ttu-id="d2571-124">Katalog — interfejs API</span><span class="sxs-lookup"><span data-stu-id="d2571-124">catalog-api</span></span>  | <span data-ttu-id="d2571-125">Kontener, w tym wykaz ASP.NET Core sieci Web API mikrousługi</span><span class="sxs-lookup"><span data-stu-id="d2571-125">Container including the Catalog ASP.NET Core Web API microservice</span></span> |
| <span data-ttu-id="d2571-126">Porządkowanie — API</span><span class="sxs-lookup"><span data-stu-id="d2571-126">ordering-api</span></span> | <span data-ttu-id="d2571-127">Kontener obejmujący porządkowanie ASP.NET Core sieci Web API mikrousług</span><span class="sxs-lookup"><span data-stu-id="d2571-127">Container including the Ordering ASP.NET Core Web API microservice</span></span> |
| <span data-ttu-id="d2571-128">dane SQLdata</span><span class="sxs-lookup"><span data-stu-id="d2571-128">sqldata</span></span>     | <span data-ttu-id="d2571-129">Kontener SQL Server dla systemu Linux, który utrzymuje bazy danych mikrousług</span><span class="sxs-lookup"><span data-stu-id="d2571-129">Container running SQL Server for Linux, holding the microservices databases</span></span> |
| <span data-ttu-id="d2571-130">koszyk — interfejs API</span><span class="sxs-lookup"><span data-stu-id="d2571-130">basket-api</span></span>   | <span data-ttu-id="d2571-131">Kontener z koszykiem ASP.NET Core mikrousługi interfejsu Web API</span><span class="sxs-lookup"><span data-stu-id="d2571-131">Container with the Basket ASP.NET Core Web API microservice</span></span> |
| <span data-ttu-id="d2571-132">basketdata</span><span class="sxs-lookup"><span data-stu-id="d2571-132">basketdata</span></span>  | <span data-ttu-id="d2571-133">Kontener z uruchomioną usługą pamięci podręcznej REDIS z bazą danych koszyka jako pamięć podręczną REDIS</span><span class="sxs-lookup"><span data-stu-id="d2571-133">Container running the REDIS cache service, with the basket database as a REDIS cache</span></span> |

### <a name="a-simple-web-service-api-container"></a><span data-ttu-id="d2571-134">Prosty kontener interfejsu API usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="d2571-134">A simple Web Service API container</span></span>

<span data-ttu-id="d2571-135">Skoncentrowanie się na pojedynczym kontenerze — kontenerem katalogu interfejsu API — mikrousługa ma prostą definicję:</span><span class="sxs-lookup"><span data-stu-id="d2571-135">Focusing on a single container, the catalog-api container-microservice has a straightforward definition:</span></span>

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

<span data-ttu-id="d2571-136">Ta usługa kontenerów ma następującą konfigurację podstawową:</span><span class="sxs-lookup"><span data-stu-id="d2571-136">This containerized service has the following basic configuration:</span></span>

- <span data-ttu-id="d2571-137">Jest on oparty na niestandardowym obrazie **interfejsu API eshop/Catalog** .</span><span class="sxs-lookup"><span data-stu-id="d2571-137">It is based on the custom **eshop/catalog-api** image.</span></span> <span data-ttu-id="d2571-138">Dla uproszczenia w pliku nie ma ustawienia Build: Key.</span><span class="sxs-lookup"><span data-stu-id="d2571-138">For simplicity's sake, there is no build: key setting in the file.</span></span> <span data-ttu-id="d2571-139">Oznacza to, że obraz musi być wcześniej skompilowany (z kompilacją Docker) lub pobrany (za pomocą polecenia docker pull) z dowolnego rejestru platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="d2571-139">This means that the image must have been previously built (with docker build) or have been downloaded (with the docker pull command) from any Docker registry.</span></span>

- <span data-ttu-id="d2571-140">Definiuje zmienną środowiskową o nazwie ConnectionString z parametrami połączenia, które mają być używane przez Entity Framework w celu uzyskania dostępu do wystąpienia SQL Server zawierającego model danych wykazu.</span><span class="sxs-lookup"><span data-stu-id="d2571-140">It defines an environment variable named ConnectionString with the connection string to be used by Entity Framework to access the SQL Server instance that contains the catalog data model.</span></span> <span data-ttu-id="d2571-141">W takim przypadku ten sam kontener SQL Server zawiera wiele baz danych.</span><span class="sxs-lookup"><span data-stu-id="d2571-141">In this case, the same SQL Server container is holding multiple databases.</span></span> <span data-ttu-id="d2571-142">W związku z tym potrzebna jest mniej pamięci na komputerze deweloperskim dla platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="d2571-142">Therefore, you need less memory in your development machine for Docker.</span></span> <span data-ttu-id="d2571-143">Można jednak również wdrożyć jeden kontener SQL Server dla każdej bazy danych mikrousług.</span><span class="sxs-lookup"><span data-stu-id="d2571-143">However, you could also deploy one SQL Server container for each microservice database.</span></span>

- <span data-ttu-id="d2571-144">Nazwa SQL Server to **SQLdata**, która jest taka sama jak nazwa używana dla kontenera, w którym działa wystąpienie SQL Server dla systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="d2571-144">The SQL Server name is **sqldata**, which is the same name used for the container that is running the SQL Server instance for Linux.</span></span> <span data-ttu-id="d2571-145">Jest to wygodne: możliwość użycia tego rozwiązania rozpoznawania nazw (wewnętrznego dla hosta platformy Docker) spowoduje rozpoznanie adresu sieciowego, dzięki czemu nie trzeba znać wewnętrznego adresu IP dla kontenerów, do których uzyskujesz dostęp z innych kontenerów.</span><span class="sxs-lookup"><span data-stu-id="d2571-145">This is convenient; being able to use this name resolution (internal to the Docker host) will resolve the network address so you don't need to know the internal IP for the containers you are accessing from other containers.</span></span>

<span data-ttu-id="d2571-146">Ponieważ parametry połączenia są zdefiniowane przez zmienną środowiskową, można ustawić tę zmienną za pomocą innego mechanizmu i w innym czasie.</span><span class="sxs-lookup"><span data-stu-id="d2571-146">Because the connection string is defined by an environment variable, you could set that variable through a different mechanism and at a different time.</span></span> <span data-ttu-id="d2571-147">Na przykład można ustawić inne parametry połączenia podczas wdrażania w środowisku produkcyjnym na finalnych hostach lub przez wykonanie ich z potoków ciągłej integracji/ciągłego dostarczania w Azure DevOps Services lub w preferowanym systemie DevOps.</span><span class="sxs-lookup"><span data-stu-id="d2571-147">For example, you could set a different connection string when deploying to production in the final hosts, or by doing it from your CI/CD pipelines in Azure DevOps Services or your preferred DevOps system.</span></span>

- <span data-ttu-id="d2571-148">Udostępnia port 80 na potrzeby wewnętrznego dostępu do usługi **katalogowej interfejsu API** w ramach hosta platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="d2571-148">It exposes port 80 for internal access to the **catalog-api** service within the Docker host.</span></span> <span data-ttu-id="d2571-149">Host jest obecnie maszyną wirtualną z systemem Linux, ponieważ jest oparta na obrazie platformy Docker dla systemu Linux, ale zamiast tego można skonfigurować kontener do uruchamiania w obrazie Windows.</span><span class="sxs-lookup"><span data-stu-id="d2571-149">The host is currently a Linux VM because it is based on a Docker image for Linux, but you could configure the container to run on a Windows image instead.</span></span>

- <span data-ttu-id="d2571-150">Przekazuje on uwidoczniony port 80 w kontenerze do portu 5101 na komputerze hosta platformy Docker (maszyna wirtualna systemu Linux).</span><span class="sxs-lookup"><span data-stu-id="d2571-150">It forwards the exposed port 80 on the container to port 5101 on the Docker host machine (the Linux VM).</span></span>

- <span data-ttu-id="d2571-151">Łączy usługę sieci Web z usługą **SQLdata** Service (wystąpienie SQL Server dla bazy danych systemu Linux działającej w kontenerze).</span><span class="sxs-lookup"><span data-stu-id="d2571-151">It links the web service to the **sqldata** service (the SQL Server instance for Linux database running in a container).</span></span> <span data-ttu-id="d2571-152">Po określeniu tej zależności kontener katalogu interfejsu API nie zostanie uruchomiony do momentu rozpoczęcia już kontenera SQLdata. jest to ważne, ponieważ usługa Catalog-API musi mieć najpierw bazę danych SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d2571-152">When you specify this dependency, the catalog-api container will not start until the sqldata container has already started; this is important because catalog-api needs to have the SQL Server database up and running first.</span></span> <span data-ttu-id="d2571-153">Jednak tego rodzaju zależność kontenera jest zbyt mała w wielu przypadkach, ponieważ platforma Docker sprawdza tylko na poziomie kontenera.</span><span class="sxs-lookup"><span data-stu-id="d2571-153">However, this kind of container dependency is not enough in many cases, because Docker checks only at the container level.</span></span> <span data-ttu-id="d2571-154">Czasami usługa (w tym przypadku SQL Server) nadal może nie być gotowa, dlatego zaleca się wdrożenie logiki ponawiania przy użyciu wykładniczej wycofywania w mikrousługach klienta.</span><span class="sxs-lookup"><span data-stu-id="d2571-154">Sometimes the service (in this case SQL Server) might still not be ready, so it is advisable to implement retry logic with exponential backoff in your client microservices.</span></span> <span data-ttu-id="d2571-155">W ten sposób, jeśli kontener zależności nie jest gotowy przez krótki czas, aplikacja nadal będzie odporna na błędy.</span><span class="sxs-lookup"><span data-stu-id="d2571-155">That way, if a dependency container is not ready for a short time, the application will still be resilient.</span></span>

- <span data-ttu-id="d2571-156">Jest skonfigurowany tak, aby zezwalał na dostęp do serwerów zewnętrznych: \_ ustawienie dodatkowe hosty umożliwia dostęp do zewnętrznych serwerów lub maszyn poza hostem platformy Docker (czyli poza domyślną maszyną wirtualną z systemem Linux, która jest hostem platformy Docker), takim jak lokalne wystąpienie SQL Server na komputerze deweloperskim.</span><span class="sxs-lookup"><span data-stu-id="d2571-156">It is configured to allow access to external servers: the extra\_hosts setting allows you to access external servers or machines outside of the Docker host (that is, outside the default Linux VM, which is a development Docker host), such as a local SQL Server instance on your development PC.</span></span>

<span data-ttu-id="d2571-157">Istnieją również inne, bardziej zaawansowane `docker-compose.yml` Ustawienia, które będziemy omawiać w poniższych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="d2571-157">There are also other, more advanced `docker-compose.yml` settings that we'll discuss in the following sections.</span></span>

### <a name="using-docker-compose-files-to-target-multiple-environments"></a><span data-ttu-id="d2571-158">Korzystanie z aplikacji platformy Docker — tworzenie plików przeznaczonych dla wielu środowisk</span><span class="sxs-lookup"><span data-stu-id="d2571-158">Using docker-compose files to target multiple environments</span></span>

<span data-ttu-id="d2571-159">`docker-compose.*.yml`Pliki są plikami definicji i mogą być używane przez wiele infrastruktur, które rozumieją ten format.</span><span class="sxs-lookup"><span data-stu-id="d2571-159">The `docker-compose.*.yml` files are definition files and can be used by multiple infrastructures that understand that format.</span></span> <span data-ttu-id="d2571-160">Najbardziej prostym narzędziem jest polecenie Docker-Zredaguj.</span><span class="sxs-lookup"><span data-stu-id="d2571-160">The most straightforward tool is the docker-compose command.</span></span>

<span data-ttu-id="d2571-161">W związku z tym przy użyciu polecenia Docker-Zredaguj można wskazać następujące główne scenariusze.</span><span class="sxs-lookup"><span data-stu-id="d2571-161">Therefore, by using the docker-compose command you can target the following main scenarios.</span></span>

#### <a name="development-environments"></a><span data-ttu-id="d2571-162">Środowiska deweloperskie</span><span class="sxs-lookup"><span data-stu-id="d2571-162">Development environments</span></span>

<span data-ttu-id="d2571-163">Podczas tworzenia aplikacji należy mieć możliwość uruchamiania aplikacji w izolowanym środowisku programistycznym.</span><span class="sxs-lookup"><span data-stu-id="d2571-163">When you develop applications, it is important to be able to run an application in an isolated development environment.</span></span> <span data-ttu-id="d2571-164">Aby utworzyć środowisko lub program Visual Studio, w którym jest używana funkcja Docker-Zredaguj w obszarze okładek, można użyć polecenia CLI-Create.</span><span class="sxs-lookup"><span data-stu-id="d2571-164">You can use the docker-compose CLI command to create that environment or Visual Studio, which uses docker-compose under the covers.</span></span>

<span data-ttu-id="d2571-165">Plik Docker-Compose. yml umożliwia skonfigurowanie i udokumentowanie wszystkich zależności usług aplikacji (innych usług, pamięci podręcznej, baz danych, kolejek itp.).</span><span class="sxs-lookup"><span data-stu-id="d2571-165">The docker-compose.yml file allows you to configure and document all your application's service dependencies (other services, cache, databases, queues, etc.).</span></span> <span data-ttu-id="d2571-166">Używając interfejsu wiersza polecenia platformy Docker — tworzenie, można utworzyć i uruchomić jeden lub więcej kontenerów dla każdej zależności za pomocą jednego polecenia (platforma Docker — tworzenie).</span><span class="sxs-lookup"><span data-stu-id="d2571-166">Using the docker-compose CLI command, you can create and start one or more containers for each dependency with a single command (docker-compose up).</span></span>

<span data-ttu-id="d2571-167">Pliki Docker-Compose. yml są plikami konfiguracji interpretowanymi przez aparat platformy Docker, ale również stanowią wygodne pliki dokumentacji dotyczące kompozycji aplikacji wielokontenerowych.</span><span class="sxs-lookup"><span data-stu-id="d2571-167">The docker-compose.yml files are configuration files interpreted by Docker engine but also serve as convenient documentation files about the composition of your multi-container application.</span></span>

#### <a name="testing-environments"></a><span data-ttu-id="d2571-168">Środowiska testowe</span><span class="sxs-lookup"><span data-stu-id="d2571-168">Testing environments</span></span>

<span data-ttu-id="d2571-169">Ważnym elementem procesu ciągłego wdrażania (CD) lub ciągłej integracji są testy jednostkowe i testy integracji.</span><span class="sxs-lookup"><span data-stu-id="d2571-169">An important part of any continuous deployment (CD) or continuous integration (CI) process are the unit tests and integration tests.</span></span> <span data-ttu-id="d2571-170">Te zautomatyzowane testy wymagają środowiska izolowanego, przez co użytkownicy nie mają wpływu ani żadnej innej zmiany w danych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d2571-170">These automated tests require an isolated environment so they are not impacted by the users or any other change in the application's data.</span></span>

<span data-ttu-id="d2571-171">Za pomocą Docker Compose można utworzyć i zniszczyć środowisko izolowane bardzo łatwo w kilku poleceniach z poziomu wiersza polecenia lub skryptów, takich jak następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="d2571-171">With Docker Compose, you can create and destroy that isolated environment very easily in a few commands from your command prompt or scripts, like the following commands:</span></span>

```console
docker-compose -f docker-compose.yml -f docker-compose-test.override.yml up -d
./run_unit_tests
docker-compose -f docker-compose.yml -f docker-compose-test.override.yml down
```

#### <a name="production-deployments"></a><span data-ttu-id="d2571-172">Wdrożenia produkcyjne</span><span class="sxs-lookup"><span data-stu-id="d2571-172">Production deployments</span></span>

<span data-ttu-id="d2571-173">Można również użyć tworzenia do wdrożenia w zdalnym aparacie platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="d2571-173">You can also use Compose to deploy to a remote Docker Engine.</span></span> <span data-ttu-id="d2571-174">Typowym przypadkiem jest wdrożenie do jednego wystąpienia hosta platformy Docker (na przykład produkcyjnej maszyny wirtualnej lub serwera z obsługą [maszyny platformy Docker](https://docs.docker.com/machine/overview/)).</span><span class="sxs-lookup"><span data-stu-id="d2571-174">A typical case is to deploy to a single Docker host instance (like a production VM or server provisioned with [Docker Machine](https://docs.docker.com/machine/overview/)).</span></span>

<span data-ttu-id="d2571-175">Jeśli używasz innego programu Orchestrator (Service Fabric platformy Azure, Kubernetes itp.), może być konieczne dodanie ustawień konfiguracji i metadanych, takich jak w Docker-Compose. yml, ale w formacie wymaganym przez inne koordynatora.</span><span class="sxs-lookup"><span data-stu-id="d2571-175">If you are using any other orchestrator (Azure Service Fabric, Kubernetes, etc.), you might need to add setup and metadata configuration settings like those in docker-compose.yml, but in the format required by the other orchestrator.</span></span>

<span data-ttu-id="d2571-176">W każdym przypadku platforma Docker — tworzenie to wygodne narzędzie i format metadanych służący do tworzenia, testowania i produkcji przepływów pracy, chociaż przepływ pracy może się różnić w zależności od używanego programu Orchestrator.</span><span class="sxs-lookup"><span data-stu-id="d2571-176">In any case, docker-compose is a convenient tool and metadata format for development, testing and production workflows, although the production workflow might vary on the orchestrator you are using.</span></span>

### <a name="using-multiple-docker-compose-files-to-handle-several-environments"></a><span data-ttu-id="d2571-177">Używanie wielu plików w programie Docker do obsługi kilku środowisk</span><span class="sxs-lookup"><span data-stu-id="d2571-177">Using multiple docker-compose files to handle several environments</span></span>

<span data-ttu-id="d2571-178">W przypadku określania różnych środowisk należy używać wielu plików redagowania.</span><span class="sxs-lookup"><span data-stu-id="d2571-178">When targeting different environments, you should use multiple compose files.</span></span> <span data-ttu-id="d2571-179">Pozwala to utworzyć wiele wariantów konfiguracji w zależności od środowiska.</span><span class="sxs-lookup"><span data-stu-id="d2571-179">This lets you create multiple configuration variants depending on the environment.</span></span>

#### <a name="overriding-the-base-docker-compose-file"></a><span data-ttu-id="d2571-180">Zastępowanie podstawowego pliku platformy Docker — redagowanie</span><span class="sxs-lookup"><span data-stu-id="d2571-180">Overriding the base docker-compose file</span></span>

<span data-ttu-id="d2571-181">Można użyć pojedynczego pliku Docker-Compose. yml, jak w przykładach uproszczonych przedstawionych w poprzednich sekcjach.</span><span class="sxs-lookup"><span data-stu-id="d2571-181">You could use a single docker-compose.yml file as in the simplified examples shown in previous sections.</span></span> <span data-ttu-id="d2571-182">Jednak nie jest to zalecane w przypadku większości aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d2571-182">However, that is not recommended for most applications.</span></span>

<span data-ttu-id="d2571-183">Domyślnie Redaguj odczytuje dwa pliki, Docker-Compose. yml i opcjonalny plik Docker-Compose. override. yml.</span><span class="sxs-lookup"><span data-stu-id="d2571-183">By default, Compose reads two files, a docker-compose.yml and an optional docker-compose.override.yml file.</span></span> <span data-ttu-id="d2571-184">Jak pokazano na rysunku 6-11, gdy korzystasz z programu Visual Studio i włączasz obsługę platformy Docker, program Visual Studio tworzy również dodatkowy plik Docker-Compose. vs. Debug. g. yml do debugowania aplikacji, można przyjrzeć się temu plikowi w folderze " \\ Docker" \\ w folderze głównym rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="d2571-184">As shown in Figure 6-11, when you are using Visual Studio and enabling Docker support, Visual Studio also creates an additional docker-compose.vs.debug.g.yml file for debugging the application, you can take a look at this file in folder obj\\Docker\\ in the main solution folder.</span></span>

![Pliki w projekcie platformy Docker.](./media/multi-container-applications-docker-compose/docker-compose-file-visual-studio.png)

<span data-ttu-id="d2571-186">**Rysunek 6-11**.</span><span class="sxs-lookup"><span data-stu-id="d2571-186">**Figure 6-11**.</span></span> <span data-ttu-id="d2571-187">Docker — tworzenie plików w programie Visual Studio 2019</span><span class="sxs-lookup"><span data-stu-id="d2571-187">docker-compose files in Visual Studio 2019</span></span>

<span data-ttu-id="d2571-188">Struktura pliku **platformy Docker — tworzenie** projektu:</span><span class="sxs-lookup"><span data-stu-id="d2571-188">**docker-compose** project file structure:</span></span>

- <span data-ttu-id="d2571-189">*. dockerignore* — służy do ignorowania plików</span><span class="sxs-lookup"><span data-stu-id="d2571-189">*.dockerignore* - used to ignore files</span></span>
- <span data-ttu-id="d2571-190">*Docker-Compose. yml* — używany do tworzenia mikrousług</span><span class="sxs-lookup"><span data-stu-id="d2571-190">*docker-compose.yml* - used to compose microservices</span></span>
- <span data-ttu-id="d2571-191">*Docker-Compose. override. yml* — służy do konfigurowania środowiska mikrousług</span><span class="sxs-lookup"><span data-stu-id="d2571-191">*docker-compose.override.yml* - used to configure microservices environment</span></span>

<span data-ttu-id="d2571-192">Można edytować plik platformy Docker z dowolnym edytorem, takim jak Visual Studio Code lub subwapno, i uruchamiać aplikację przy użyciu polecenia Docker-Zredaguj w górę.</span><span class="sxs-lookup"><span data-stu-id="d2571-192">You can edit the docker-compose files with any editor, like Visual Studio Code or Sublime, and run the application with the docker-compose up command.</span></span>

<span data-ttu-id="d2571-193">Zgodnie z Konwencją plik Docker-Compose. yml zawiera konfigurację podstawową i inne ustawienia statyczne.</span><span class="sxs-lookup"><span data-stu-id="d2571-193">By convention, the docker-compose.yml file contains your base configuration and other static settings.</span></span> <span data-ttu-id="d2571-194">Oznacza to, że konfiguracja usługi nie powinna się zmieniać w zależności od używanego środowiska wdrażania.</span><span class="sxs-lookup"><span data-stu-id="d2571-194">That means that the service configuration should not change depending on the deployment environment you are targeting.</span></span>

<span data-ttu-id="d2571-195">Plik Docker-Compose. override. yml, jak jego nazwa sugeruje, zawiera ustawienia konfiguracji, które zastępują konfigurację podstawową, na przykład konfigurację, która zależy od środowiska wdrażania.</span><span class="sxs-lookup"><span data-stu-id="d2571-195">The docker-compose.override.yml file, as its name suggests, contains configuration settings that override the base configuration, such as configuration that depends on the deployment environment.</span></span> <span data-ttu-id="d2571-196">Można również mieć wiele plików przesłonięć o różnych nazwach.</span><span class="sxs-lookup"><span data-stu-id="d2571-196">You can have multiple override files with different names also.</span></span> <span data-ttu-id="d2571-197">Pliki przesłonięć zwykle zawierają dodatkowe informacje, które są konieczne dla aplikacji, ale specyficzne dla środowiska lub wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="d2571-197">The override files usually contain additional information needed by the application but specific to an environment or to a deployment.</span></span>

#### <a name="targeting-multiple-environments"></a><span data-ttu-id="d2571-198">Kierowanie wielu środowisk</span><span class="sxs-lookup"><span data-stu-id="d2571-198">Targeting multiple environments</span></span>

<span data-ttu-id="d2571-199">Typowym przypadkiem użycia jest definiowanie wielu plików redagowania, aby można było kierować wiele środowisk, takich jak produkcja, przemieszczanie, CI lub programowanie.</span><span class="sxs-lookup"><span data-stu-id="d2571-199">A typical use case is when you define multiple compose files so you can target multiple environments, like production, staging, CI, or development.</span></span> <span data-ttu-id="d2571-200">Aby obsłużyć te różnice, można podzielić konfigurację redagowania na wiele plików, jak pokazano na rysunku 6-12.</span><span class="sxs-lookup"><span data-stu-id="d2571-200">To support these differences, you can split your Compose configuration into multiple files, as shown in Figure 6-12.</span></span>

![Diagram trzech plików do redagowania platformy Docker, ustawiony w celu zastąpienia pliku podstawowego.](./media/multi-container-applications-docker-compose/multiple-docker-compose-files-override-base.png)

<span data-ttu-id="d2571-202">**Rysunek 6-12**.</span><span class="sxs-lookup"><span data-stu-id="d2571-202">**Figure 6-12**.</span></span> <span data-ttu-id="d2571-203">Wiele plików programu Docker — tworzenie przesłania wartości w podstawowym pliku Docker-Compose. yml</span><span class="sxs-lookup"><span data-stu-id="d2571-203">Multiple docker-compose files overriding values in the base docker-compose.yml file</span></span>

<span data-ttu-id="d2571-204">Można połączyć wiele plików Docker-Compose\*. yml, aby obsługiwać różne środowiska.</span><span class="sxs-lookup"><span data-stu-id="d2571-204">You can combine multiple docker-compose\*.yml files to handle different environments.</span></span> <span data-ttu-id="d2571-205">Zaczynasz od podstawowego pliku Docker-Compose. yml.</span><span class="sxs-lookup"><span data-stu-id="d2571-205">You start with the base docker-compose.yml file.</span></span> <span data-ttu-id="d2571-206">Ten plik podstawowy zawiera podstawowe lub statyczne ustawienia konfiguracji, które nie zmieniają się w zależności od środowiska.</span><span class="sxs-lookup"><span data-stu-id="d2571-206">This base file contains the base or static configuration settings that do not change depending on the environment.</span></span> <span data-ttu-id="d2571-207">Na przykład aplikacja eShopOnContainers ma następujący plik Docker-Compose. yml (uproszczony z mniejszą liczbą usług) jako plik podstawowy.</span><span class="sxs-lookup"><span data-stu-id="d2571-207">For example, the eShopOnContainers app has the following docker-compose.yml file (simplified with fewer services) as the base file.</span></span>

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

<span data-ttu-id="d2571-208">Wartości w podstawowym pliku Docker-Compose. yml nie należy zmieniać ze względu na inne docelowe środowiska wdrażania.</span><span class="sxs-lookup"><span data-stu-id="d2571-208">The values in the base docker-compose.yml file should not change because of different target deployment environments.</span></span>

<span data-ttu-id="d2571-209">W przypadku określenia usługi webmvc na przykład można zobaczyć, jak te informacje są znacznie takie same niezależnie od tego, jakie środowisko może być ukierunkowane.</span><span class="sxs-lookup"><span data-stu-id="d2571-209">If you focus on the webmvc service definition, for instance, you can see how that information is much the same no matter what environment you might be targeting.</span></span> <span data-ttu-id="d2571-210">Masz następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="d2571-210">You have the following information:</span></span>

- <span data-ttu-id="d2571-211">Nazwa usługi: webmvc.</span><span class="sxs-lookup"><span data-stu-id="d2571-211">The service name: webmvc.</span></span>

- <span data-ttu-id="d2571-212">Obraz niestandardowy kontenera: eshop/webmvc.</span><span class="sxs-lookup"><span data-stu-id="d2571-212">The container's custom image: eshop/webmvc.</span></span>

- <span data-ttu-id="d2571-213">Polecenie służące do kompilowania niestandardowego obrazu platformy Docker wskazujący, którego pliku dockerfile użyć.</span><span class="sxs-lookup"><span data-stu-id="d2571-213">The command to build the custom Docker image, indicating which Dockerfile to use.</span></span>

- <span data-ttu-id="d2571-214">Zależności od innych usług, więc ten kontener nie zostanie uruchomiony do momentu rozpoczęcia innych kontenerów zależności.</span><span class="sxs-lookup"><span data-stu-id="d2571-214">Dependencies on other services, so this container does not start until the other dependency containers have started.</span></span>

<span data-ttu-id="d2571-215">Możesz mieć dodatkową konfigurację, ale ważnym punktem jest to, że w podstawowym pliku Docker-Compose. yml, wystarczy ustawić informacje wspólne w różnych środowiskach.</span><span class="sxs-lookup"><span data-stu-id="d2571-215">You can have additional configuration, but the important point is that in the base docker-compose.yml file, you just want to set the information that is common across environments.</span></span> <span data-ttu-id="d2571-216">Następnie w Docker-Compose. override. yml lub podobnych plikach do produkcji lub przemieszczania należy umieścić konfigurację specyficzną dla każdego środowiska.</span><span class="sxs-lookup"><span data-stu-id="d2571-216">Then in the docker-compose.override.yml or similar files for production or staging, you should place configuration that is specific for each environment.</span></span>

<span data-ttu-id="d2571-217">Zazwyczaj Docker-Compose. override. yml jest używany w środowisku deweloperskim, jak w poniższym przykładzie z eShopOnContainers:</span><span class="sxs-lookup"><span data-stu-id="d2571-217">Usually, the docker-compose.override.yml is used for your development environment, as in the following example from eShopOnContainers:</span></span>

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

<span data-ttu-id="d2571-218">W tym przykładzie konfiguracja przesłonięcia rozwoju uwidacznia niektóre porty hosta, definiuje zmienne środowiskowe z adresami URL przekierowania i określa parametry połączenia dla środowiska deweloperskiego.</span><span class="sxs-lookup"><span data-stu-id="d2571-218">In this example, the development override configuration exposes some ports to the host, defines environment variables with redirect URLs, and specifies connection strings for the development environment.</span></span> <span data-ttu-id="d2571-219">Te ustawienia są przeznaczone tylko dla środowiska deweloperskiego.</span><span class="sxs-lookup"><span data-stu-id="d2571-219">These settings are all just for the development environment.</span></span>

<span data-ttu-id="d2571-220">Gdy uruchamiasz `docker-compose up` (lub uruchamiasz ją z programu Visual Studio), polecenie odczytuje przesłonięcia automatycznie tak, jakby były scalane oba pliki.</span><span class="sxs-lookup"><span data-stu-id="d2571-220">When you run `docker-compose up` (or launch it from Visual Studio), the command reads the overrides automatically as if it were merging both files.</span></span>

<span data-ttu-id="d2571-221">Załóżmy, że chcesz, aby inny plik redagowania był używany w środowisku produkcyjnym, z innymi wartościami konfiguracji, portami lub parametrami połączenia.</span><span class="sxs-lookup"><span data-stu-id="d2571-221">Suppose that you want another Compose file for the production environment, with different configuration values, ports, or connection strings.</span></span> <span data-ttu-id="d2571-222">Można utworzyć inny plik przesłonięcia, taki jak plik o `docker-compose.prod.yml` różnych ustawieniach i zmiennych środowiskowych.</span><span class="sxs-lookup"><span data-stu-id="d2571-222">You can create another override file, like file named `docker-compose.prod.yml` with different settings and environment variables.</span></span> <span data-ttu-id="d2571-223">Ten plik może być przechowywany w innym repozytorium Git lub zarządzany i zabezpieczony przez inny zespół.</span><span class="sxs-lookup"><span data-stu-id="d2571-223">That file might be stored in a different Git repo or managed and secured by a different team.</span></span>

#### <a name="how-to-deploy-with-a-specific-override-file"></a><span data-ttu-id="d2571-224">Jak wdrożyć z określonym plikiem przesłonięcia</span><span class="sxs-lookup"><span data-stu-id="d2571-224">How to deploy with a specific override file</span></span>

<span data-ttu-id="d2571-225">Aby użyć wielu plików przesłonięć lub zastąpić plik z inną nazwą, można użyć opcji-f z poleceniem Docker-Zredaguj i określić pliki.</span><span class="sxs-lookup"><span data-stu-id="d2571-225">To use multiple override files, or an override file with a different name, you can use the -f option with the docker-compose command and specify the files.</span></span> <span data-ttu-id="d2571-226">Redaguj scala pliki w kolejności określonej w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="d2571-226">Compose merges files in the order they are specified on the command line.</span></span> <span data-ttu-id="d2571-227">Poniższy przykład pokazuje, jak wdrożyć przy użyciu plików przesłonięć.</span><span class="sxs-lookup"><span data-stu-id="d2571-227">The following example shows how to deploy with override files.</span></span>

```console
docker-compose -f docker-compose.yml -f docker-compose.prod.yml up -d
```

#### <a name="using-environment-variables-in-docker-compose-files"></a><span data-ttu-id="d2571-228">Używanie zmiennych środowiskowych w programie Docker — tworzenie plików</span><span class="sxs-lookup"><span data-stu-id="d2571-228">Using environment variables in docker-compose files</span></span>

<span data-ttu-id="d2571-229">Jest to wygodne, szczególnie w środowiskach produkcyjnych, aby można było uzyskać informacje o konfiguracji ze zmiennych środowiskowych, jak pokazano w poprzednich przykładach.</span><span class="sxs-lookup"><span data-stu-id="d2571-229">It is convenient, especially in production environments, to be able to get configuration information from environment variables, as we have shown in previous examples.</span></span> <span data-ttu-id="d2571-230">Można odwołać się do zmiennej środowiskowej w plikach tworzących platformy Docker przy użyciu składni $ {MY \_ var}.</span><span class="sxs-lookup"><span data-stu-id="d2571-230">You can reference an environment variable in your docker-compose files using the syntax ${MY\_VAR}.</span></span> <span data-ttu-id="d2571-231">Poniższy wiersz z pliku Docker-Compose. prod. yml pokazuje, jak odwołać się do wartości zmiennej środowiskowej.</span><span class="sxs-lookup"><span data-stu-id="d2571-231">The following line from a docker-compose.prod.yml file shows how to reference the value of an environment variable.</span></span>

```yml
IdentityUrl=http://${ESHOP_PROD_EXTERNAL_DNS_NAME_OR_IP}:5105
```

<span data-ttu-id="d2571-232">Zmienne środowiskowe są tworzone i inicjowane na różne sposoby, w zależności od środowiska hosta (Linux, Windows, klaster w chmurze itp.).</span><span class="sxs-lookup"><span data-stu-id="d2571-232">Environment variables are created and initialized in different ways, depending on your host environment (Linux, Windows, Cloud cluster, etc.).</span></span> <span data-ttu-id="d2571-233">Jednak wygodne podejście polega na użyciu pliku. env.</span><span class="sxs-lookup"><span data-stu-id="d2571-233">However, a convenient approach is to use an .env file.</span></span> <span data-ttu-id="d2571-234">Pliki do tworzenia platformy Docker obsługują deklarowanie domyślnych zmiennych środowiskowych w pliku ENV.</span><span class="sxs-lookup"><span data-stu-id="d2571-234">The docker-compose files support declaring default environment variables in the .env file.</span></span> <span data-ttu-id="d2571-235">Te wartości zmiennych środowiskowych są wartościami domyślnymi.</span><span class="sxs-lookup"><span data-stu-id="d2571-235">These values for the environment variables are the default values.</span></span> <span data-ttu-id="d2571-236">Mogą jednak zostać przesłonięte przez wartości, które mogą być zdefiniowane w poszczególnych środowiskach (system operacyjny hosta lub zmienne środowiskowe z klastra).</span><span class="sxs-lookup"><span data-stu-id="d2571-236">But they can be overridden by the values you might have defined in each of your environments (host OS or environment variables from your cluster).</span></span> <span data-ttu-id="d2571-237">Ten plik ENV zostanie umieszczony w folderze, w którym jest wykonywane polecenie Docker-redagowanie.</span><span class="sxs-lookup"><span data-stu-id="d2571-237">You place this .env file in the folder where the docker-compose command is executed from.</span></span>

<span data-ttu-id="d2571-238">W poniższym przykładzie przedstawiono plik. env, taki jak plik [ENV](https://github.com/dotnet-architecture/eShopOnContainers/blob/master/.env) dla aplikacji eShopOnContainers.</span><span class="sxs-lookup"><span data-stu-id="d2571-238">The following example shows an .env file like the [.env](https://github.com/dotnet-architecture/eShopOnContainers/blob/master/.env) file for the eShopOnContainers application.</span></span>

```sh
# .env file

ESHOP_EXTERNAL_DNS_NAME_OR_IP=localhost

ESHOP_PROD_EXTERNAL_DNS_NAME_OR_IP=10.121.122.92
```

<span data-ttu-id="d2571-239">Docker-redagowanie oczekuje, że każdy wiersz w pliku ENV ma być w formacie \<variable\> = \<value\> .</span><span class="sxs-lookup"><span data-stu-id="d2571-239">Docker-compose expects each line in an .env file to be in the format \<variable\>=\<value\>.</span></span>

<span data-ttu-id="d2571-240">Wartości ustawione w środowisku wykonawczym zawsze przesłonią wartości zdefiniowane wewnątrz pliku ENV.</span><span class="sxs-lookup"><span data-stu-id="d2571-240">The values set in the run-time environment always override the values defined inside the .env file.</span></span> <span data-ttu-id="d2571-241">W podobny sposób wartości przekazane za pośrednictwem argumentów wiersza polecenia również przesłaniają wartości domyślne ustawione w pliku ENV.</span><span class="sxs-lookup"><span data-stu-id="d2571-241">In a similar way, values passed via command-line arguments also override the default values set in the .env file.</span></span>

#### <a name="additional-resources"></a><span data-ttu-id="d2571-242">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="d2571-242">Additional resources</span></span>

- <span data-ttu-id="d2571-243">**Omówienie Docker Compose** </span><span class="sxs-lookup"><span data-stu-id="d2571-243">**Overview of Docker Compose** </span></span>\
    <https://docs.docker.com/compose/overview/>

- <span data-ttu-id="d2571-244">**Wiele plików redagowania** </span><span class="sxs-lookup"><span data-stu-id="d2571-244">**Multiple Compose files** </span></span>\
    [https://docs.docker.com/compose/extends/\#multiple-compose-files](https://docs.docker.com/compose/extends/#multiple-compose-files)

### <a name="building-optimized-aspnet-core-docker-images"></a><span data-ttu-id="d2571-245">Kompilowanie zoptymalizowanych obrazów ASP.NET Core Docker</span><span class="sxs-lookup"><span data-stu-id="d2571-245">Building optimized ASP.NET Core Docker images</span></span>

<span data-ttu-id="d2571-246">Jeśli eksplorujesz platformę Docker i platformę .NET Core w źródłach internetowych, znajdziesz wieloetapowe dockerfile, który pokazuje prostotę tworzenia obrazu platformy Docker przez skopiowanie źródła do kontenera.</span><span class="sxs-lookup"><span data-stu-id="d2571-246">If you are exploring Docker and .NET Core on sources on the Internet, you will find Dockerfiles that demonstrate the simplicity of building a Docker image by copying your source into a container.</span></span> <span data-ttu-id="d2571-247">Te przykłady sugerują, że przy użyciu prostej konfiguracji możesz mieć obraz platformy Docker ze środowiskiem spakowanym z aplikacją.</span><span class="sxs-lookup"><span data-stu-id="d2571-247">These examples suggest that by using a simple configuration, you can have a Docker image with the environment packaged with your application.</span></span> <span data-ttu-id="d2571-248">Poniższy przykład pokazuje prostą pliku dockerfile w tej szyjce.</span><span class="sxs-lookup"><span data-stu-id="d2571-248">The following example shows a simple Dockerfile in this vein.</span></span>

```dockerfile
FROM mcr.microsoft.com/dotnet/sdk:3.1
WORKDIR /app
ENV ASPNETCORE_URLS http://+:80
EXPOSE 80
COPY . .
RUN dotnet restore
ENTRYPOINT ["dotnet", "run"]
```

<span data-ttu-id="d2571-249">Pliku dockerfile taka będzie działała.</span><span class="sxs-lookup"><span data-stu-id="d2571-249">A Dockerfile like this will work.</span></span> <span data-ttu-id="d2571-250">Można jednak znacznie zoptymalizować obrazy, w szczególności obrazy produkcyjne.</span><span class="sxs-lookup"><span data-stu-id="d2571-250">However, you can substantially optimize your images, especially your production images.</span></span>

<span data-ttu-id="d2571-251">W modelu kontenerów i mikrousług są ciągle uruchamiane kontenery.</span><span class="sxs-lookup"><span data-stu-id="d2571-251">In the container and microservices model, you are constantly starting containers.</span></span> <span data-ttu-id="d2571-252">Typowy sposób używania kontenerów nie powoduje ponownego uruchomienia kontenera uśpionego, ponieważ kontener jest jednorazowy.</span><span class="sxs-lookup"><span data-stu-id="d2571-252">The typical way of using containers does not restart a sleeping container, because the container is disposable.</span></span> <span data-ttu-id="d2571-253">Koordynatorzy (na przykład Kubernetes i Azure Service Fabric) po prostu tworzą nowe wystąpienia obrazów.</span><span class="sxs-lookup"><span data-stu-id="d2571-253">Orchestrators (like Kubernetes and Azure Service Fabric) simply create new instances of images.</span></span> <span data-ttu-id="d2571-254">Oznacza to, że trzeba zoptymalizować przez wstępne skompilowanie aplikacji, aby proces tworzenia wystąpienia był szybszy.</span><span class="sxs-lookup"><span data-stu-id="d2571-254">What this means is that you would need to optimize by precompiling the application when it is built so the instantiation process will be faster.</span></span> <span data-ttu-id="d2571-255">Po rozpoczęciu kontenera powinien być gotowy do uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="d2571-255">When the container is started, it should be ready to run.</span></span> <span data-ttu-id="d2571-256">Nie należy przywracać i kompilować w czasie wykonywania za pomocą `dotnet restore` `dotnet build` poleceń i interfejsu wiersza polecenia, które mogą być widoczne w wpisach w blogu na temat platformy .NET Core i platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="d2571-256">Don't restore and compile at run time using the `dotnet restore` and `dotnet build` CLI commands as you may see in blog posts about .NET Core and Docker.</span></span>

<span data-ttu-id="d2571-257">Zespół platformy .NET wykonuje ważne prace w celu udostępnienia platformy .NET Core i ASP.NET Core platformy zoptymalizowanej pod kątem kontenerów.</span><span class="sxs-lookup"><span data-stu-id="d2571-257">The .NET team has been doing important work to make .NET Core and ASP.NET Core a container-optimized framework.</span></span> <span data-ttu-id="d2571-258">Jest to nie tylko platforma .NET Core z małą ilością pamięci. zespół koncentruje się na zoptymalizowanych obrazach platformy Docker dla trzech głównych scenariuszy i publikuje je w rejestrze usługi Docker Hub na platformie *dotnet/Core*, począwszy od wersji 2,1:</span><span class="sxs-lookup"><span data-stu-id="d2571-258">Not only is .NET Core a lightweight framework with a small memory footprint; the team has focused on optimized Docker images for three main scenarios and published them in the Docker Hub registry at *dotnet/core*, beginning with version 2.1:</span></span>

1. <span data-ttu-id="d2571-259">**Programowanie**: priorytet to możliwość szybkiego wykonywania iteracji i debugowania zmian oraz w przypadku, gdy rozmiar jest pomocniczy.</span><span class="sxs-lookup"><span data-stu-id="d2571-259">**Development**: The priority is the ability to quickly iterate and debug changes, and where size is secondary.</span></span>

2. <span data-ttu-id="d2571-260">**Kompilacja**: priorytet kompiluje aplikację, a obraz zawiera dane binarne i inne zależności w celu zoptymalizowania plików binarnych.</span><span class="sxs-lookup"><span data-stu-id="d2571-260">**Build**: The priority is compiling the application, and the image includes binaries and other dependencies to optimize binaries.</span></span>

3. <span data-ttu-id="d2571-261">**Produkcja**: fokus jest szybkim wdrożeniem i początkiem kontenerów, dzięki czemu obrazy te są ograniczone do plików binarnych i zawartości wymaganych do uruchomienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d2571-261">**Production**: The focus is fast deploying and starting of containers, so these images are limited to the binaries and content needed to run the application.</span></span>

<span data-ttu-id="d2571-262">Zespół .NET oferuje cztery podstawowe warianty w programie [dotnet/Core](https://hub.docker.com/_/microsoft-dotnet/) (w usłudze Docker Hub):</span><span class="sxs-lookup"><span data-stu-id="d2571-262">The .NET team provides four basic variants in [dotnet/core](https://hub.docker.com/_/microsoft-dotnet/) (at Docker Hub):</span></span>

1. <span data-ttu-id="d2571-263">**zestaw SDK**: na potrzeby scenariuszy tworzenia i kompilowania</span><span class="sxs-lookup"><span data-stu-id="d2571-263">**sdk**: for development and build scenarios</span></span>
1. <span data-ttu-id="d2571-264">**ASPNET**: for ASP.NET — scenariusze produkcji</span><span class="sxs-lookup"><span data-stu-id="d2571-264">**aspnet**: for ASP.NET production scenarios</span></span>
1. <span data-ttu-id="d2571-265">**środowisko uruchomieniowe**: dla scenariuszy produkcyjnych programu .NET</span><span class="sxs-lookup"><span data-stu-id="d2571-265">**runtime**: for .NET production scenarios</span></span>
1. <span data-ttu-id="d2571-266">**środowisko uruchomieniowe — deps**: dla scenariuszy produkcyjnych [aplikacji samodzielnych](../../../core/deploying/index.md#publish-self-contained)</span><span class="sxs-lookup"><span data-stu-id="d2571-266">**runtime-deps**: for production scenarios of [self-contained applications](../../../core/deploying/index.md#publish-self-contained)</span></span>

<span data-ttu-id="d2571-267">W celu przyspieszenia uruchamiania obrazy środowiska uruchomieniowego również automatycznie ustawiają \_ adresy URL aspnetcore na porcie 80 i używają narzędzia NGen do tworzenia pamięci podręcznej obrazów natywnych zestawów.</span><span class="sxs-lookup"><span data-stu-id="d2571-267">For faster startup, runtime images also automatically set aspnetcore\_urls to port 80 and use Ngen to create a native image cache of assemblies.</span></span>

#### <a name="additional-resources"></a><span data-ttu-id="d2571-268">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="d2571-268">Additional resources</span></span>

- <span data-ttu-id="d2571-269">**Kompilowanie zoptymalizowanych obrazów platformy Docker za pomocą ASP.NET Core**
  <https://docs.microsoft.com/archive/blogs/stevelasker/building-optimized-docker-images-with-asp-net-core></span><span class="sxs-lookup"><span data-stu-id="d2571-269">**Building Optimized Docker Images with ASP.NET Core**
<https://docs.microsoft.com/archive/blogs/stevelasker/building-optimized-docker-images-with-asp-net-core></span></span>

- <span data-ttu-id="d2571-270">**Kompilowanie obrazów platformy Docker dla aplikacji platformy .NET Core**
  [https://docs.microsoft.com/dotnet/core/docker/building-net-docker-images](/aspnet/core/host-and-deploy/docker/building-net-docker-images)</span><span class="sxs-lookup"><span data-stu-id="d2571-270">**Building Docker Images for .NET Core Applications**
[https://docs.microsoft.com/dotnet/core/docker/building-net-docker-images](/aspnet/core/host-and-deploy/docker/building-net-docker-images)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d2571-271">[Poprzedni](data-driven-crud-microservice.md) 
>  [Dalej](database-server-container.md)</span><span class="sxs-lookup"><span data-stu-id="d2571-271">[Previous](data-driven-crud-microservice.md)
[Next](database-server-container.md)</span></span>
