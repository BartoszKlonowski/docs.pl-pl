---
title: Przepływ pracy tworzenia oprogramowania dla aplikacji platformy Docker
description: Zapoznaj się ze szczegółami przepływu pracy dotyczącymi tworzenia aplikacji opartych na platformie Docker. Rozpocznij krok po kroku i przejdź do szczegółów, aby zoptymalizować wieloetapowe dockerfile i zakończyć pracę z uproszczonym przepływem pracy dostępnym w przypadku korzystania z programu Visual Studio.
ms.date: 01/07/2019
ms.openlocfilehash: 34d2a90cb5208736b1b414e25ac3e627929f45a0
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/30/2019
ms.locfileid: "70296176"
---
# <a name="development-workflow-for-docker-apps"></a><span data-ttu-id="c6596-104">Przepływ pracy tworzenia oprogramowania dla aplikacji platformy Docker</span><span class="sxs-lookup"><span data-stu-id="c6596-104">Development workflow for Docker apps</span></span>

<span data-ttu-id="c6596-105">Cykl życia aplikacji jest uruchamiany na komputerze, jako deweloper, w którym można nakodować aplikację przy użyciu preferowanego języka i testować go lokalnie.</span><span class="sxs-lookup"><span data-stu-id="c6596-105">The application development life cycle starts at your computer, as a developer, where you code the application using your preferred language and test it locally.</span></span> <span data-ttu-id="c6596-106">Za pomocą tego przepływu pracy niezależnie od tego, jaki język, struktura i platforma wybierzesz, zawsze opracowujesz i testujesz kontenery Docker, ale wykonujesz je lokalnie.</span><span class="sxs-lookup"><span data-stu-id="c6596-106">With this workflow, no matter which language, framework, and platform you choose, you're always developing and testing Docker containers, but doing so locally.</span></span>

<span data-ttu-id="c6596-107">Każdy kontener (wystąpienie obrazu platformy Docker) zawiera następujące składniki:</span><span class="sxs-lookup"><span data-stu-id="c6596-107">Each container (an instance of a Docker image) includes the following components:</span></span>

- <span data-ttu-id="c6596-108">Wybór systemu operacyjnego, na przykład, dystrybucja systemu Linux, Windows nano Server lub Windows Server Core.</span><span class="sxs-lookup"><span data-stu-id="c6596-108">An operating system selection, for example, a Linux distribution, Windows Nano Server, or Windows Server Core.</span></span>

- <span data-ttu-id="c6596-109">Pliki dodawane podczas opracowywania, na przykład kod źródłowy i pliki binarne aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c6596-109">Files added during development, for example, source code and application binaries.</span></span>

- <span data-ttu-id="c6596-110">Informacje o konfiguracji, takie jak ustawienia środowiska i zależności.</span><span class="sxs-lookup"><span data-stu-id="c6596-110">Configuration information, such as environment settings and dependencies.</span></span>

## <a name="workflow-for-developing-docker-container-based-applications"></a><span data-ttu-id="c6596-111">Przepływ pracy dla opracowywania aplikacji opartych na kontenerach platformy Docker</span><span class="sxs-lookup"><span data-stu-id="c6596-111">Workflow for developing Docker container-based applications</span></span>

<span data-ttu-id="c6596-112">W tej sekcji opisano przepływ pracy programowania w *pętli wewnętrznej* dla aplikacji opartych na kontenerach platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="c6596-112">This section describes the *inner-loop* development workflow for Docker container-based applications.</span></span> <span data-ttu-id="c6596-113">Przepływ pracy z pętlą wewnętrzną oznacza, że nie rozważa on szerszego przepływu pracy DevOps, który może obejmować wdrożenie w środowisku produkcyjnym, a jedynie koncentruje się na rozwoju pracy na komputerze dewelopera.</span><span class="sxs-lookup"><span data-stu-id="c6596-113">The inner-loop workflow means it's not considering the broader DevOps workflow, that can include up to production deployment, and just focuses on the development work done on the developer's computer.</span></span> <span data-ttu-id="c6596-114">Początkowe kroki konfigurowania środowiska nie są uwzględniane, ponieważ te kroki są wykonywane tylko raz.</span><span class="sxs-lookup"><span data-stu-id="c6596-114">The initial steps to set up the environment aren't included, since those steps are done only once.</span></span>

<span data-ttu-id="c6596-115">Aplikacja składa się z własnych usług i dodatkowych bibliotek (zależności).</span><span class="sxs-lookup"><span data-stu-id="c6596-115">An application is composed of your own services plus additional libraries (dependencies).</span></span> <span data-ttu-id="c6596-116">Poniżej przedstawiono podstawowe kroki, które zwykle są wykonywane podczas kompilowania aplikacji platformy Docker, jak pokazano na rysunku 5-1.</span><span class="sxs-lookup"><span data-stu-id="c6596-116">The following are the basic steps you usually take when building a Docker application, as illustrated in Figure 5-1.</span></span>

![<span data-ttu-id="c6596-117">Proces opracowywania aplikacji platformy Docker: 1. Zakoduj aplikację, 2-Write pliku dockerfile/s, 3 — Tworzenie obrazów zdefiniowanych w pliku dockerfile/s, 4 — (opcjonalnie) redagowanie usług w pliku Docker-Compose. yml, 5-lub aplikacji platformy Docker, 6 — Testowanie aplikacji lub mikrousług, 7 — wypychanie do repozytorium i powtarzanie.</span><span class="sxs-lookup"><span data-stu-id="c6596-117">The development process for Docker apps: 1 - Code your App, 2 - Write Dockerfile/s, 3 - Create images defined at Dockerfile/s, 4 - (optional) Compose services in the docker-compose.yml file, 5 - Run container or docker-compose app, 6 - Test your app or microservices, 7 - Push to repo and repeat.</span></span> ](./media/image1.png)

<span data-ttu-id="c6596-118">**Rysunek 5-1.**</span><span class="sxs-lookup"><span data-stu-id="c6596-118">**Figure 5-1.**</span></span> <span data-ttu-id="c6596-119">Przepływ pracy krok po kroku dla opracowywania aplikacji w kontenerze platformy Docker</span><span class="sxs-lookup"><span data-stu-id="c6596-119">Step-by-step workflow for developing Docker containerized apps</span></span>

<span data-ttu-id="c6596-120">W tej sekcji opisano szczegółowy proces, a każdy z najważniejszych kroków jest wyjaśniony przez skoncentrowanie się na środowisku programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c6596-120">In this section, this whole process is detailed and every major step is explained by focusing on a Visual Studio environment.</span></span>

<span data-ttu-id="c6596-121">W przypadku korzystania z podejścia edytora/interfejsu wiersza polecenia (na przykład Visual Studio Code i interfejsu wiersza polecenia platformy Docker w systemie macOS lub Windows) należy wiedzieć każdy krok, ogólnie bardziej szczegółowo niż w przypadku korzystania z programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c6596-121">When you're using an editor/CLI development approach (for example, Visual Studio Code plus Docker CLI on macOS or Windows), you need to know every step, generally in more detail than if you're using Visual Studio.</span></span> <span data-ttu-id="c6596-122">Aby uzyskać więcej informacji na temat pracy w środowisku interfejsu wiersza polecenia, zapoznaj się z [cyklem życia aplikacji platformy Docker w książce elektronicznej przy użyciu platform i narzędzi firmy Microsoft](https://aka.ms/dockerlifecycleebook/).</span><span class="sxs-lookup"><span data-stu-id="c6596-122">For more information about working in a CLI environment, see the e-book [Containerized Docker Application lifecycle with Microsoft Platforms and Tools](https://aka.ms/dockerlifecycleebook/).</span></span>

<span data-ttu-id="c6596-123">W przypadku korzystania z programu Visual Studio 2017 wiele z tych kroków jest obsługiwanych przez Ciebie, co znacznie zwiększa wydajność pracy.</span><span class="sxs-lookup"><span data-stu-id="c6596-123">When you're using Visual Studio 2017, many of those steps are handled for you, which dramatically improves your productivity.</span></span> <span data-ttu-id="c6596-124">Jest to szczególnie prawdziwe w przypadku korzystania z programu Visual Studio 2017 i określania aplikacji obsługujących wiele kontenerów.</span><span class="sxs-lookup"><span data-stu-id="c6596-124">This is especially true when you're using Visual Studio 2017 and targeting multi-container applications.</span></span> <span data-ttu-id="c6596-125">Na przykład po kliknięciu tylko jednego kliknięcia myszą program Visual Studio dodaje plik pliku dockerfile i Docker-Compose. yml do projektów z konfiguracją dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c6596-125">For instance, with just one mouse click, Visual Studio adds the Dockerfile and docker-compose.yml file to your projects with the configuration for your application.</span></span> <span data-ttu-id="c6596-126">Po uruchomieniu aplikacji w programie Visual Studio kompiluje ona obraz platformy Docker i uruchamia aplikację wielokontenerową bezpośrednio w Docker; Umożliwia to nawet debugowanie kilku kontenerów jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="c6596-126">When you run the application in Visual Studio, it builds the Docker image and runs the multi-container application directly in Docker; it even allows you to debug several containers at once.</span></span> <span data-ttu-id="c6596-127">Te funkcje spowodują zwiększenie szybkości tworzenia oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="c6596-127">These features will boost your development speed.</span></span>

<span data-ttu-id="c6596-128">Jednak po prostu, ponieważ program Visual Studio wykonuje te czynności automatycznie nie oznacza to, że nie musisz wiedzieć, co się dzieje w objściu z platformą Docker.</span><span class="sxs-lookup"><span data-stu-id="c6596-128">However, just because Visual Studio makes those steps automatic doesn't mean that you don't need to know what's going on underneath with Docker.</span></span> <span data-ttu-id="c6596-129">W związku z tym poniższe wskazówki zawierają szczegółowe informacje o każdym kroku.</span><span class="sxs-lookup"><span data-stu-id="c6596-129">Therefore, the following guidance details every step.</span></span>

![1 — kod aplikacji](./media/image2.png)

## <a name="step-1-start-coding-and-create-your-initial-application-or-service-baseline"></a><span data-ttu-id="c6596-131">Krok 1.</span><span class="sxs-lookup"><span data-stu-id="c6596-131">Step 1.</span></span> <span data-ttu-id="c6596-132">Rozpocznij kodowanie i Utwórz początkową aplikację lub linię bazową usługi</span><span class="sxs-lookup"><span data-stu-id="c6596-132">Start coding and create your initial application or service baseline</span></span>

<span data-ttu-id="c6596-133">Tworzenie aplikacji platformy Docker jest podobne do sposobu tworzenia aplikacji bez platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="c6596-133">Developing a Docker application is similar to the way you develop an application without Docker.</span></span> <span data-ttu-id="c6596-134">Różnica polega na tym, że podczas tworzenia aplikacji dla platformy Docker wdrażane i testowane są aplikacje lub usługi działające w kontenerach platformy Docker w środowisku lokalnym (Konfiguracja maszyny wirtualnej z systemem Linux przez platformę Docker lub bezpośrednio w systemie Windows, jeśli są używane kontenery systemu Windows).</span><span class="sxs-lookup"><span data-stu-id="c6596-134">The difference is that while developing for Docker, you're deploying and testing your application or services running within Docker containers in your local environment (either a Linux VM setup by Docker or directly Windows if using Windows Containers).</span></span>

### <a name="set-up-your-local-environment-with-visual-studio"></a><span data-ttu-id="c6596-135">Konfigurowanie środowiska lokalnego przy użyciu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c6596-135">Set up your local environment with Visual Studio</span></span>

<span data-ttu-id="c6596-136">Aby rozpocząć, upewnij się, że masz zainstalowaną [platformę Docker Community Edition (CE)](https://docs.docker.com/docker-for-windows/) dla systemu Windows, zgodnie z opisem w poniższych instrukcjach:</span><span class="sxs-lookup"><span data-stu-id="c6596-136">To begin, make sure you have [Docker Community Edition (CE)](https://docs.docker.com/docker-for-windows/) for Windows installed, as explained in the following instructions:</span></span>

[<span data-ttu-id="c6596-137">Wprowadzenie do Docker CE for Windows</span><span class="sxs-lookup"><span data-stu-id="c6596-137">Get started with Docker CE for Windows</span></span>](https://docs.docker.com/docker-for-windows/)

<span data-ttu-id="c6596-138">Ponadto konieczne jest zainstalowanie programu Visual Studio 2017 w wersji 15,7 lub nowszej z zainstalowanym **międzyplatformowym obciążeniem programistycznym platformy .NET Core** , jak pokazano na rysunku 5-2.</span><span class="sxs-lookup"><span data-stu-id="c6596-138">In addition, you need Visual Studio 2017 version 15.7 or later, with the **.NET Core cross-platform development** workload installed, as shown in Figure 5-2.</span></span>

![Wybór obciążenia dla wielu platform w programie .NET Core podczas instalacji programu Visual Studio.](./media/image3.png)

<span data-ttu-id="c6596-140">**Rysunek 5-2**.</span><span class="sxs-lookup"><span data-stu-id="c6596-140">**Figure 5-2**.</span></span> <span data-ttu-id="c6596-141">Wybieranie obciążenia **programowania dla wielu platform .NET Core** podczas instalacji programu Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="c6596-141">Selecting the **.NET Core cross-platform development** workload during Visual Studio 2017 setup</span></span>

<span data-ttu-id="c6596-142">Możesz rozpocząć kodowanie aplikacji w zwykłym środowisku .NET (zwykle w programie .NET Core, jeśli planujesz korzystanie z kontenerów) nawet przed włączeniem platformy Docker w aplikacji oraz wdrożenie i przetestowanie na platformie Docker.</span><span class="sxs-lookup"><span data-stu-id="c6596-142">You can start coding your application in plain .NET (usually in .NET Core if you're planning to use containers) even before enabling Docker in your application and deploying and testing in Docker.</span></span> <span data-ttu-id="c6596-143">Zaleca się jednak rozpoczęcie pracy z platformą Docker najszybciej, jak to możliwe, ponieważ będzie to realne środowisko i ewentualne problemy mogą zostać odnalezione najszybciej, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="c6596-143">However, it is recommended that you start working on Docker as soon as possible, because that will be the real environment and any issues can be discovered as soon as possible.</span></span> <span data-ttu-id="c6596-144">Jest to zalecane, ponieważ program Visual Studio ułatwia współpracę z platformą Docker, która niemal jest przejrzysta — najlepszym przykładem w przypadku debugowania aplikacji wielokontenerowych z programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c6596-144">This is encouraged because Visual Studio makes it so easy to work with Docker that it almost feels transparent—the best example when debugging multi-container applications from Visual Studio.</span></span>

### <a name="additional-resources"></a><span data-ttu-id="c6596-145">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="c6596-145">Additional resources</span></span>

- <span data-ttu-id="c6596-146">**Wprowadzenie do Docker CE for Windows** </span><span class="sxs-lookup"><span data-stu-id="c6596-146">**Get started with Docker CE for Windows** </span></span>\
  <https://docs.docker.com/docker-for-windows/>

- <span data-ttu-id="c6596-147">**Visual Studio 2017** </span><span class="sxs-lookup"><span data-stu-id="c6596-147">**Visual Studio 2017** </span></span>\
  [https://visualstudio.microsoft.com/downloads/](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2017)

![2 — wieloetapowe dockerfile zapisu](./media/image4.png)

## <a name="step-2-create-a-dockerfile-related-to-an-existing-net-base-image"></a><span data-ttu-id="c6596-149">Krok 2.</span><span class="sxs-lookup"><span data-stu-id="c6596-149">Step 2.</span></span> <span data-ttu-id="c6596-150">Tworzenie pliku dockerfile związanych z istniejącym obrazem podstawowym platformy .NET</span><span class="sxs-lookup"><span data-stu-id="c6596-150">Create a Dockerfile related to an existing .NET base image</span></span>

<span data-ttu-id="c6596-151">Dla każdego niestandardowego obrazu, który chcesz skompilować, potrzebujesz pliku dockerfile. wymagany jest również pliku dockerfile dla każdego kontenera do wdrożenia, niezależnie od tego, czy wdrażasz automatycznie z programu Visual Studio, czy ręcznie przy użyciu interfejsu wiersza polecenia platformy Docker (narzędzia Docker Run i Docker-redagowanie).</span><span class="sxs-lookup"><span data-stu-id="c6596-151">You need a Dockerfile for each custom image you want to build; you also need a Dockerfile for each container to be deployed, whether you deploy automatically from Visual Studio or manually using the Docker CLI (docker run and docker-compose commands).</span></span> <span data-ttu-id="c6596-152">Jeśli aplikacja zawiera pojedynczą usługę niestandardową, potrzebna jest jedna pliku dockerfile.</span><span class="sxs-lookup"><span data-stu-id="c6596-152">If your application contains a single custom service, you need a single Dockerfile.</span></span> <span data-ttu-id="c6596-153">Jeśli aplikacja zawiera wiele usług (podobnie jak w przypadku architektury mikrousług), potrzebna jest jedna pliku dockerfile dla każdej usługi.</span><span class="sxs-lookup"><span data-stu-id="c6596-153">If your application contains multiple services (as in a microservices architecture), you need one Dockerfile for each service.</span></span>

<span data-ttu-id="c6596-154">Pliku dockerfile jest umieszczany w folderze głównym aplikacji lub usługi.</span><span class="sxs-lookup"><span data-stu-id="c6596-154">The Dockerfile is placed in the root folder of your application or service.</span></span> <span data-ttu-id="c6596-155">Zawiera polecenia, które informują platformę Docker, jak skonfigurować i uruchomić aplikację lub usługę w kontenerze.</span><span class="sxs-lookup"><span data-stu-id="c6596-155">It contains the commands that tell Docker how to set up and run your application or service in a container.</span></span> <span data-ttu-id="c6596-156">Możesz ręcznie utworzyć pliku dockerfile w kodzie i dodać go do projektu wraz z zależnościami programu .NET.</span><span class="sxs-lookup"><span data-stu-id="c6596-156">You can manually create a Dockerfile in code and add it to your project along with your .NET dependencies.</span></span>

<span data-ttu-id="c6596-157">Za pomocą programu Visual Studio i jego narzędzi dla platformy Docker to zadanie wymaga tylko kilku kliknięć myszą.</span><span class="sxs-lookup"><span data-stu-id="c6596-157">With Visual Studio and its tools for Docker, this task requires only a few mouse clicks.</span></span> <span data-ttu-id="c6596-158">Podczas tworzenia nowego projektu w programie Visual Studio 2017 istnieje opcja o nazwie **Włącz kontener (Docker)** , jak pokazano na rysunku 5-3.</span><span class="sxs-lookup"><span data-stu-id="c6596-158">When you create a new project in Visual Studio 2017, there's an option named **Enable Container (Docker) Support**, as shown in Figure 5-3.</span></span>

![Pole wyboru Włącz obsługę platformy Docker podczas tworzenia nowego projektu ASP.NET Core w programie Visual Studio 2017](./media/image5.png)

<span data-ttu-id="c6596-160">**Rysunek 5-3**.</span><span class="sxs-lookup"><span data-stu-id="c6596-160">**Figure 5-3**.</span></span> <span data-ttu-id="c6596-161">Włączanie obsługi platformy Docker podczas tworzenia nowego projektu ASP.NET Core w programie Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="c6596-161">Enabling Docker Support when creating a new ASP.NET Core project in Visual Studio 2017</span></span>

<span data-ttu-id="c6596-162">Możesz również włączyć obsługę platformy Docker w istniejącym projekcie aplikacji sieci Web ASP.NET Core, klikając prawym przyciskiem myszy projekt w **Eksplorator rozwiązań** i wybierając polecenie **Dodaj** > **obsługę platformy Docker**, jak pokazano na rysunku 5-4.</span><span class="sxs-lookup"><span data-stu-id="c6596-162">You can also enable Docker support on an existing ASP.NET Core web app project by right-clicking the project in **Solution Explorer** and selecting **Add** > **Docker Support**, as shown in Figure 5-4.</span></span>

![Opcja menu Dodaj obsługę platformy Docker w programie Visual Studio](./media/image6.png)

<span data-ttu-id="c6596-164">**Rysunek 5-4**.</span><span class="sxs-lookup"><span data-stu-id="c6596-164">**Figure 5-4**.</span></span> <span data-ttu-id="c6596-165">Włączanie obsługi platformy Docker w istniejącym projekcie programu Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="c6596-165">Enabling Docker support in an existing Visual Studio 2017 project</span></span>

<span data-ttu-id="c6596-166">Ta akcja dodaje *pliku dockerfile* do projektu z wymaganą konfiguracją i jest dostępna tylko w projektach ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="c6596-166">This action adds a *Dockerfile* to the project with the required configuration, and is only available on ASP.NET Core projects.</span></span>

<span data-ttu-id="c6596-167">W podobny sposób program Visual Studio może również dodać plik Docker-Compose. yml dla całego rozwiązania przy użyciu opcji **dodaj > kontener Orchestrator support**.</span><span class="sxs-lookup"><span data-stu-id="c6596-167">In a similar fashion, Visual Studio can also add a docker-compose.yml file for the whole solution with the option **Add > Container Orchestrator Support**.</span></span> <span data-ttu-id="c6596-168">W kroku 4 podaliśmy tę opcję bardziej szczegółowo.</span><span class="sxs-lookup"><span data-stu-id="c6596-168">In step 4, we'll explore this option in greater detail.</span></span>

### <a name="using-an-existing-official-net-docker-image"></a><span data-ttu-id="c6596-169">Korzystanie z istniejącego oficjalnego obrazu platformy Docker .NET</span><span class="sxs-lookup"><span data-stu-id="c6596-169">Using an existing official .NET Docker image</span></span>

<span data-ttu-id="c6596-170">Zwykle można utworzyć niestandardowy obraz dla kontenera na podstawie obrazu podstawowego, który uzyskuje się z oficjalnego repozytorium, takiego jak rejestr usługi [Docker Hub](https://hub.docker.com/) .</span><span class="sxs-lookup"><span data-stu-id="c6596-170">You usually build a custom image for your container on top of a base image you get from an official repository like the [Docker Hub](https://hub.docker.com/) registry.</span></span> <span data-ttu-id="c6596-171">To dokładnie, co się dzieje w przypadku włączenia obsługi platformy Docker w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c6596-171">That is precisely what happens under the covers when you enable Docker support in Visual Studio.</span></span> <span data-ttu-id="c6596-172">Pliku dockerfile będzie używać istniejącego `aspnetcore` obrazu.</span><span class="sxs-lookup"><span data-stu-id="c6596-172">Your Dockerfile will use an existing `aspnetcore` image.</span></span>

<span data-ttu-id="c6596-173">Wcześniej objaśniono, które obrazy platformy Docker i repozytoria, których można użyć, w zależności od wybranego środowiska i systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="c6596-173">Earlier we explained which Docker images and repos you can use, depending on the framework and OS you have chosen.</span></span> <span data-ttu-id="c6596-174">Na przykład jeśli chcesz używać ASP.NET Core (Linux lub Windows), obraz do użycia to `mcr.microsoft.com/dotnet/core/aspnet:2.2`.</span><span class="sxs-lookup"><span data-stu-id="c6596-174">For instance, if you want to use ASP.NET Core (Linux or Windows), the image to use is `mcr.microsoft.com/dotnet/core/aspnet:2.2`.</span></span> <span data-ttu-id="c6596-175">W związku z tym wystarczy określić podstawowy obraz platformy Docker, który będzie używany w danym kontenerze.</span><span class="sxs-lookup"><span data-stu-id="c6596-175">Therefore, you just need to specify what base Docker image you will use for your container.</span></span> <span data-ttu-id="c6596-176">Możesz to zrobić, dodając `FROM mcr.microsoft.com/dotnet/core/aspnet:2.2` do pliku dockerfile.</span><span class="sxs-lookup"><span data-stu-id="c6596-176">You do that by adding `FROM mcr.microsoft.com/dotnet/core/aspnet:2.2` to your Dockerfile.</span></span> <span data-ttu-id="c6596-177">Ta wartość zostanie automatycznie wykonana przez program Visual Studio, ale jeśli zaktualizowano wersję, należy ją zaktualizować.</span><span class="sxs-lookup"><span data-stu-id="c6596-177">This will be automatically performed by Visual Studio, but if you were to update the version, you update this value.</span></span>

<span data-ttu-id="c6596-178">Korzystanie z oficjalnego repozytorium programu .NET Image z usługi Docker Hub z numerem wersji zapewnia, że te same funkcje językowe są dostępne na wszystkich komputerach (w tym na temat programowania, testowania i produkcji).</span><span class="sxs-lookup"><span data-stu-id="c6596-178">Using an official .NET image repository from Docker Hub with a version number ensures that the same language features are available on all machines (including development, testing, and production).</span></span>

<span data-ttu-id="c6596-179">W poniższym przykładzie przedstawiono przykładową pliku dockerfile dla kontenera ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="c6596-179">The following example shows a sample Dockerfile for an ASP.NET Core container.</span></span>

```Dockerfile
FROM mcr.microsoft.com/dotnet/core/aspnet:2.2
ARG source
WORKDIR /app
EXPOSE 80
COPY ${source:-obj/Docker/publish} .
ENTRYPOINT ["dotnet", " MySingleContainerWebApp.dll "]
```

<span data-ttu-id="c6596-180">W tym przypadku obraz jest oparty na wersji 2,2 ASP.NET Core oficjalnego obrazu platformy Docker (wiele rozwiązań dla systemów Linux i Windows).</span><span class="sxs-lookup"><span data-stu-id="c6596-180">In this case, the image is based on version 2.2 of the official ASP.NET Core Docker image (multi-arch for Linux and Windows).</span></span> <span data-ttu-id="c6596-181">To ustawienie `FROM mcr.microsoft.com/dotnet/core/aspnet:2.2`.</span><span class="sxs-lookup"><span data-stu-id="c6596-181">This is the setting `FROM mcr.microsoft.com/dotnet/core/aspnet:2.2`.</span></span> <span data-ttu-id="c6596-182">(Aby uzyskać więcej informacji na temat tego obrazu podstawowego, zobacz stronę [obrazu platformy Docker programu .NET Core](https://hub.docker.com/_/microsoft-dotnet-core/) ). W pliku dockerfile należy również nakazać platformie Docker nasłuchiwanie na porcie TCP, który będzie używany w środowisku uruchomieniowym (w tym przypadku port 80, zgodnie z konfiguracją ustawienia UWIDACZNIAnia).</span><span class="sxs-lookup"><span data-stu-id="c6596-182">(For more information about this base image, see the [.NET Core Docker Image](https://hub.docker.com/_/microsoft-dotnet-core/) page.) In the Dockerfile, you also need to instruct Docker to listen on the TCP port you will use at runtime (in this case, port 80, as configured with the EXPOSE setting).</span></span>

<span data-ttu-id="c6596-183">Możesz określić dodatkowe ustawienia konfiguracji w pliku dockerfile, w zależności od używanego języka i platformy.</span><span class="sxs-lookup"><span data-stu-id="c6596-183">You can specify additional configuration settings in the Dockerfile, depending on the language and framework you're using.</span></span> <span data-ttu-id="c6596-184">Na przykład wiersz `["dotnet", "MySingleContainerWebApp.dll"]` punktu wejścia informuje platformę Docker, aby uruchomić aplikację platformy .NET Core.</span><span class="sxs-lookup"><span data-stu-id="c6596-184">For instance, the ENTRYPOINT line with `["dotnet", "MySingleContainerWebApp.dll"]` tells Docker to run a .NET Core application.</span></span> <span data-ttu-id="c6596-185">Jeśli używasz zestawu SDK i interfejs wiersza polecenia platformy .NET Core (interfejs dotnet CLI) do kompilowania i uruchamiania aplikacji .NET, to ustawienie będzie inne.</span><span class="sxs-lookup"><span data-stu-id="c6596-185">If you're using the SDK and the .NET Core CLI (dotnet CLI) to build and run the .NET application, this setting would be different.</span></span> <span data-ttu-id="c6596-186">Dolna linia polega na tym, że linia ENTRYPOINT i inne ustawienia będą się różnić w zależności od języka i platformy wybranej dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c6596-186">The bottom line is that the ENTRYPOINT line and other settings will be different depending on the language and platform you choose for your application.</span></span>

### <a name="additional-resources"></a><span data-ttu-id="c6596-187">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="c6596-187">Additional resources</span></span>

- <span data-ttu-id="c6596-188">**Kompilowanie obrazów platformy Docker dla aplikacji platformy .NET Core** </span><span class="sxs-lookup"><span data-stu-id="c6596-188">**Building Docker Images for .NET Core Applications** </span></span>\
  [https://docs.microsoft.com/dotnet/core/docker/building-net-docker-images](../../../core/docker/building-net-docker-images.md)

- <span data-ttu-id="c6596-189">**Utwórz własny obraz**.</span><span class="sxs-lookup"><span data-stu-id="c6596-189">**Build your own image**.</span></span> <span data-ttu-id="c6596-190">W oficjalnej dokumentacji platformy Docker. </span><span class="sxs-lookup"><span data-stu-id="c6596-190">In the official Docker documentation.</span></span>\
  <https://docs.docker.com/engine/tutorials/dockerimages/>

- <span data-ttu-id="c6596-191">**Aktualne z użyciem obrazów kontenerów platformy .NET** </span><span class="sxs-lookup"><span data-stu-id="c6596-191">**Staying up-to-date with .NET Container Images** </span></span>\
  <https://devblogs.microsoft.com/dotnet/staying-up-to-date-with-net-container-images/>

- <span data-ttu-id="c6596-192">**Korzystanie z programu .NET i platformy Docker razem z aktualizacją DockerCon 2018** </span><span class="sxs-lookup"><span data-stu-id="c6596-192">**Using .NET and Docker Together - DockerCon 2018 Update** </span></span>\
  <https://devblogs.microsoft.com/dotnet/using-net-and-docker-together-dockercon-2018-update/>

### <a name="using-multi-arch-image-repositories"></a><span data-ttu-id="c6596-193">Używanie repozytoriów obrazów wieloskładnikowych</span><span class="sxs-lookup"><span data-stu-id="c6596-193">Using multi-arch image repositories</span></span>

<span data-ttu-id="c6596-194">Pojedyncze repozytorium może zawierać warianty platformy, takie jak obraz systemu Linux i obraz Windows.</span><span class="sxs-lookup"><span data-stu-id="c6596-194">A single repo can contain platform variants, such as a Linux image and a Windows image.</span></span> <span data-ttu-id="c6596-195">Ta funkcja umożliwia dostawcom, takim jak firma Microsoft (twórcy obrazów podstawowych), tworzenie jednego repozytorium w celu pokrycia wielu platform (z systemem Linux i Windows).</span><span class="sxs-lookup"><span data-stu-id="c6596-195">This feature allows vendors like Microsoft (base image creators) to create a single repo to cover multiple platforms (that is Linux and Windows).</span></span> <span data-ttu-id="c6596-196">Na przykład repozytorium [dotnet/Core](https://hub.docker.com/_/microsoft-dotnet-core/) dostępne w rejestrze usługi Docker Hub zapewnia obsługę systemu Linux i Windows nano Server przy użyciu tej samej nazwy repozytorium.</span><span class="sxs-lookup"><span data-stu-id="c6596-196">For example, the [dotnet/core](https://hub.docker.com/_/microsoft-dotnet-core/) repository available in the Docker Hub registry provides support for Linux and Windows Nano Server by using the same repo name.</span></span>

<span data-ttu-id="c6596-197">Jeśli określisz tag, nadajesz platformie, która jest jawna, jak w następujących przypadkach:</span><span class="sxs-lookup"><span data-stu-id="c6596-197">If you specify a tag, targeting a platform that is explicit like in the following cases:</span></span>

- `microsoft/dotnet:2.2-aspnetcore-runtime-stretch-slim` \
  <span data-ttu-id="c6596-198">Elementy docelowe: środowisko uruchomieniowe programu .NET Core 2,2 — tylko w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="c6596-198">Targets: .NET Core 2.2 runtime-only on Linux</span></span>

- `microsoft/dotnet:2.2-aspnetcore-runtime-nanoserver-1809` \
  <span data-ttu-id="c6596-199">Targets: środowisko uruchomieniowe programu .NET Core 2,2 — tylko w systemie Windows nano Server</span><span class="sxs-lookup"><span data-stu-id="c6596-199">Targets: .NET Core 2.2 runtime-only on Windows Nano Server</span></span>

<span data-ttu-id="c6596-200">Ale w przypadku określenia tej samej nazwy obrazu, nawet w tym samym tagu, obrazy z obsługą wielodostępności (na `aspnetcore` przykład obraz) będą używały wersji systemu Linux lub Windows w zależności od wdrażanego systemu operacyjnego hosta platformy Docker, jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="c6596-200">But, if you specify the same image name, even with the same tag, the multi-arch images (like the `aspnetcore` image) will use the Linux or Windows version depending on the Docker host OS you're deploying, as shown in the following example:</span></span>

- `microsoft/dotnet:2.2-aspnetcore-runtime` \
  <span data-ttu-id="c6596-201">Wiele arch: środowisko uruchomieniowe programu .NET Core 2,2 — tylko w systemie Linux lub Windows nano Server w zależności od systemu operacyjnego hosta platformy Docker</span><span class="sxs-lookup"><span data-stu-id="c6596-201">Multi-arch: .NET Core 2.2 runtime-only on Linux or Windows Nano Server depending on the Docker host OS</span></span>

<span data-ttu-id="c6596-202">W ten sposób podczas ściągania obrazu z hosta z systemem Windows zostanie ściągnięty wariant systemu Windows, a pociągnięcie tego samego obrazu z hosta z systemem Linux spowoduje pobranie wariantu z systemem Linux.</span><span class="sxs-lookup"><span data-stu-id="c6596-202">This way, when you pull an image from a Windows host, it will pull the Windows variant, and pulling the same image name from a Linux host will pull the Linux variant.</span></span>

### <a name="multi-stage-builds-in-dockerfile"></a><span data-ttu-id="c6596-203">Kompilacje wieloetapowe w pliku dockerfile</span><span class="sxs-lookup"><span data-stu-id="c6596-203">Multi-stage builds in Dockerfile</span></span>

<span data-ttu-id="c6596-204">Pliku dockerfile jest podobny do skryptu wsadowego.</span><span class="sxs-lookup"><span data-stu-id="c6596-204">The Dockerfile is similar to a batch script.</span></span> <span data-ttu-id="c6596-205">Podobnie jak w przypadku konfigurowania maszyny z poziomu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="c6596-205">Similar to what you would do if you had to set up the machine from the command line.</span></span>

<span data-ttu-id="c6596-206">Rozpoczyna się od obrazu podstawowego, który konfiguruje kontekst początkowy, podobnie jak startowy system plików, który znajduje się na szczycie systemu operacyjnego hosta.</span><span class="sxs-lookup"><span data-stu-id="c6596-206">It starts with a base image that sets up the initial context, it's like the startup filesystem, that sits on top of the host OS.</span></span> <span data-ttu-id="c6596-207">Nie jest to system operacyjny, ale możesz określić, czy tak jak w przypadku systemu operacyjnego w kontenerze.</span><span class="sxs-lookup"><span data-stu-id="c6596-207">It's not an OS, but you can think of if like "the" OS inside the container.</span></span>

<span data-ttu-id="c6596-208">Wykonanie każdego wiersza polecenia powoduje utworzenie nowej warstwy w systemie plików ze zmianami z poprzedniego, tak aby w przypadku łączenia wygenerowała system plików w systemie.</span><span class="sxs-lookup"><span data-stu-id="c6596-208">The execution of every command line creates a new layer on the filesystem with the changes from the previous one, so that, when combined, produce the resulting filesystem.</span></span>

<span data-ttu-id="c6596-209">Ze względu na to, że każda nowa warstwa "zatrzyma się" na poprzednim, a rozmiar obrazu pojawia się w każdym poleceniu, obrazy mogą być bardzo duże, jeśli trzeba je uwzględnić, na przykład zestaw SDK, który jest wymagany do kompilowania i publikowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c6596-209">Since every new layer "rests" on top of the previous one and the resulting image size increases with every command, images can get very large if they have to include, for example, the SDK needed to build and publish an application.</span></span>

<span data-ttu-id="c6596-210">Jest to miejsce, w którym kompilacje wieloetapowe są uzyskiwane na powierzchni (od platformy Docker 17,05 lub nowszej), aby wykonać ich magiczną.</span><span class="sxs-lookup"><span data-stu-id="c6596-210">This is where multi-stage builds get into the plot (from Docker 17.05 and higher) to do their magic.</span></span>

<span data-ttu-id="c6596-211">Głównym pomysłem jest to, że można oddzielić proces wykonywania pliku dockerfile w etapach, gdzie etap jest obrazem początkowym, po którym następuje co najmniej jedno polecenie, a ostatni etap Określa końcowy rozmiar obrazu.</span><span class="sxs-lookup"><span data-stu-id="c6596-211">The core idea is that you can separate the Dockerfile execution process in stages, where a stage is an initial image followed by one or more commands, and the last stage determines the final image size.</span></span>

<span data-ttu-id="c6596-212">W krótkim przypadku kompilacje wieloetapowe umożliwiają podział tworzenia w różnych fazach, a następnie złożenie obrazu końcowego, pobierając tylko odpowiednie katalogi z etapów pośrednich.</span><span class="sxs-lookup"><span data-stu-id="c6596-212">In short, multi-stage builds allow splitting the creation in different "phases" and then assemble the final image taking only the relevant directories from the intermediate stages.</span></span> <span data-ttu-id="c6596-213">Ogólna strategia korzystania z tej funkcji to:</span><span class="sxs-lookup"><span data-stu-id="c6596-213">The general strategy to use this feature is:</span></span>

1. <span data-ttu-id="c6596-214">Użyj podstawowego obrazu zestawu SDK (niezależnie od tego, jak jest to duże), ze wszystkimi elementami potrzebnymi do kompilowania i publikowania aplikacji w folderze, a następnie</span><span class="sxs-lookup"><span data-stu-id="c6596-214">Use a base SDK image (doesn't matter how large), with everything needed to build and publish the application to a folder and then</span></span>

2. <span data-ttu-id="c6596-215">Użyj obrazu podstawowego, małego, samego środowiska uruchomieniowego i skopiuj folder publikacji z poprzedniego etapu, aby utworzyć mały obraz końcowy.</span><span class="sxs-lookup"><span data-stu-id="c6596-215">Use a base, small, runtime-only image and copy the publishing folder from the previous stage to produce a small final image.</span></span>

<span data-ttu-id="c6596-216">Prawdopodobnie najlepszym sposobem na zrozumienie wieloetapowego jest przechodzenie przez pliku dockerfile szczegóły, wiersz po wierszu, więc zaczynamy od początkowego pliku dockerfile utworzonego przez program Visual Studio podczas dodawania obsługi platformy Docker do projektu i przejdziesz do pewnych optymalizacji później.</span><span class="sxs-lookup"><span data-stu-id="c6596-216">Probably the best way to understand multi-stage is going through a Dockerfile in detail, line by line, so let's begin with the initial Dockerfile created by Visual Studio when adding Docker support to a project and will get into some optimizations later.</span></span>

<span data-ttu-id="c6596-217">Początkowy pliku dockerfile może wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="c6596-217">The initial Dockerfile might look something like this:</span></span>

```Dockerfile
 1  FROM mcr.microsoft.com/dotnet/core/aspnet:2.2 AS base
 2  WORKDIR /app
 3  EXPOSE 80
 4
 5  FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build
 6  WORKDIR /src
 7  COPY src/Services/Catalog/Catalog.API/Catalog.API.csproj …
 8  COPY src/BuildingBlocks/HealthChecks/src/Microsoft.AspNetCore.HealthChecks …
 9  COPY src/BuildingBlocks/HealthChecks/src/Microsoft.Extensions.HealthChecks …
10  COPY src/BuildingBlocks/EventBus/IntegrationEventLogEF/ …
11  COPY src/BuildingBlocks/EventBus/EventBus/EventBus.csproj …
12  COPY src/BuildingBlocks/EventBus/EventBusRabbitMQ/EventBusRabbitMQ.csproj …
13  COPY src/BuildingBlocks/EventBus/EventBusServiceBus/EventBusServiceBus.csproj …
14  COPY src/BuildingBlocks/WebHostCustomization/WebHost.Customization …
15  COPY src/BuildingBlocks/HealthChecks/src/Microsoft.Extensions …
16  COPY src/BuildingBlocks/HealthChecks/src/Microsoft.Extensions …
17  RUN dotnet restore src/Services/Catalog/Catalog.API/Catalog.API.csproj
18  COPY . .
19  WORKDIR /src/src/Services/Catalog/Catalog.API
20  RUN dotnet build Catalog.API.csproj -c Release -o /app
21
22  FROM build AS publish
23  RUN dotnet publish Catalog.API.csproj -c Release -o /app
24
25  FROM base AS final
26  WORKDIR /app
27  COPY --from=publish /app .
28  ENTRYPOINT ["dotnet", "Catalog.API.dll"]
```

<span data-ttu-id="c6596-218">Są to szczegóły, wiersz po wierszu:</span><span class="sxs-lookup"><span data-stu-id="c6596-218">And these are the details, line by line:</span></span>

<!-- markdownlint-disable MD029-->
1. <span data-ttu-id="c6596-219">Rozpocznij etap z obrazem podstawowym "mały" tylko środowisko uruchomieniowe, wywołaj jego **bazę** jako odwołanie.</span><span class="sxs-lookup"><span data-stu-id="c6596-219">Begin a stage with a "small" runtime-only base image, call it **base** for reference.</span></span>
2. <span data-ttu-id="c6596-220">Utwórz katalog **/App** w obrazie.</span><span class="sxs-lookup"><span data-stu-id="c6596-220">Create **/app** directory in the image.</span></span>
3. <span data-ttu-id="c6596-221">Uwidocznij port **80**.</span><span class="sxs-lookup"><span data-stu-id="c6596-221">Expose port **80**.</span></span>
<!-- skip -->
5. <span data-ttu-id="c6596-222">Rozpocznij nowy etap przy użyciu obrazu "Large" do kompilowania/publikowania, wywołaj **kompilację do kompilacji** w celu uzyskania odwołania.</span><span class="sxs-lookup"><span data-stu-id="c6596-222">Begin a new stage with "large" image for building/publishing, call it **build** for reference.</span></span>
6. <span data-ttu-id="c6596-223">Utwórz katalog **/src** w obrazie.</span><span class="sxs-lookup"><span data-stu-id="c6596-223">Create directory **/src** in the image.</span></span>
7. <span data-ttu-id="c6596-224">Do wiersza 16, skopiuj przywoływane pliki projects **. csproj** , aby umożliwić późniejsze przywracanie pakietów.</span><span class="sxs-lookup"><span data-stu-id="c6596-224">Up to line 16, copy referenced projects **.csproj** files, to be able to restore packages later.</span></span>
<!-- skip -->
17. <span data-ttu-id="c6596-225">Przywróć pakiety dla projektu **Catalog. API** i projektów, do których istnieją odwołania.</span><span class="sxs-lookup"><span data-stu-id="c6596-225">Restore packages for the **Catalog.API** project and the referenced projects.</span></span>
18. <span data-ttu-id="c6596-226">Skopiuj **wszystkie drzewa katalogów dla rozwiązania** (z wyjątkiem plików/katalogów znajdujących się w pliku **. dockerignore** ) z katalogu **/src** w obrazie.</span><span class="sxs-lookup"><span data-stu-id="c6596-226">Copy **all directory tree for the solution** (except the files/directories included in the **.dockerignore** file) from to the **/src** directory in the image.</span></span>
19. <span data-ttu-id="c6596-227">Zmień bieżący folder na **katalog. interfejs API** .</span><span class="sxs-lookup"><span data-stu-id="c6596-227">Change current folder to **Catalog.API** project.</span></span>
20. <span data-ttu-id="c6596-228">Kompiluj projekt (i inne zależności projektu) i dane wyjściowe do katalogu **/App** w obrazie.</span><span class="sxs-lookup"><span data-stu-id="c6596-228">Build project (and other project dependencies) and output to **/app** directory in the image.</span></span>
<!-- skip -->
22. <span data-ttu-id="c6596-229">Rozpocznij nowy etap Kontynuuj od kompilacji, wywołaj go **,** Aby uzyskać odwołanie.</span><span class="sxs-lookup"><span data-stu-id="c6596-229">Begin a new stage continuing from build, call it **publish** for reference.</span></span>
23. <span data-ttu-id="c6596-230">Publikuj projekt (i zależności) i dane wyjściowe do katalogu **/App** w obrazie.</span><span class="sxs-lookup"><span data-stu-id="c6596-230">Publish project (and dependencies) and output to **/app** directory in the image.</span></span>
<!-- skip -->
25. <span data-ttu-id="c6596-231">Rozpocznij nowy etap, kontynuując od **podstaw** i Wywołaj **ostateczną**</span><span class="sxs-lookup"><span data-stu-id="c6596-231">Begin a new stage continuing from **base** and call it **final**</span></span>
26. <span data-ttu-id="c6596-232">Zmień bieżący katalog na **/App**</span><span class="sxs-lookup"><span data-stu-id="c6596-232">Change current directory to **/app**</span></span>
27. <span data-ttu-id="c6596-233">Skopiuj katalog **/App** z **publikacji** Stage do bieżącego katalogu</span><span class="sxs-lookup"><span data-stu-id="c6596-233">Copy the **/app** directory from stage **publish** to the current directory</span></span>
28. <span data-ttu-id="c6596-234">Zdefiniuj polecenie do uruchomienia po rozpoczęciu kontenera.</span><span class="sxs-lookup"><span data-stu-id="c6596-234">Define the command to run when the container is started.</span></span>
<!-- markdownlint-enable MD029-->

<span data-ttu-id="c6596-235">Teraz zapoznaj się z pewnymi optymalizacjami, aby zwiększyć wydajność całego procesu, która w przypadku eShopOnContainers, oznacza około 22 minut lub dłużej, aby skompilować kompletne rozwiązanie w kontenerach systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="c6596-235">Now let's explore some optimizations to improve the whole process performance that, in the case of eShopOnContainers, means about 22 minutes or more to build the complete solution in Linux containers.</span></span>

<span data-ttu-id="c6596-236">Będziesz korzystać z funkcji pamięci podręcznej warstwy platformy Docker, która jest dość prosta: Jeśli obraz podstawowy i polecenia są takie same jak niektóre wcześniej wykonane, można po prostu użyć warstwy, bez konieczności wykonywania poleceń, co spowoduje zapisanie pewnego czasu.</span><span class="sxs-lookup"><span data-stu-id="c6596-236">You'll take advantage of Docker's layer cache feature, which is quite simple: if the base image and the commands are the same as some previously executed, it can just use the resulting layer without the need to execute the commands, thus saving some time.</span></span>

<span data-ttu-id="c6596-237">W związku z tym skupmy się na etapie **kompilacji** , wiersze 5-6 są w większości takie same, ale linie 7-17 są różne dla każdej usługi z eShopOnContainers, więc muszą być wykonywane co jeden raz, jednak Jeśli zmieniono wiersze 7-16 na:</span><span class="sxs-lookup"><span data-stu-id="c6596-237">So, let's focus on the **build** stage, lines 5-6 are mostly the same, but lines 7-17 are different for every service from eShopOnContainers, so they have to execute every single time, however if you changed lines 7-16 to:</span></span>

```Dockerfile
COPY . .
```

<span data-ttu-id="c6596-238">Następnie będzie ona taka sama dla każdej usługi, dlatego skopiuje całe rozwiązanie i utworzy większą warstwę, ale:</span><span class="sxs-lookup"><span data-stu-id="c6596-238">Then it would be just the same for every service, it would copy the whole solution and would create a larger layer but:</span></span>

1) <span data-ttu-id="c6596-239">Proces kopiowania będzie wykonywany tylko po raz pierwszy (oraz podczas ponownego kompilowania, gdy plik zostanie zmieniony) i użyje pamięci podręcznej dla wszystkich innych usług i</span><span class="sxs-lookup"><span data-stu-id="c6596-239">The copy process would only be executed the first time (and when rebuilding if a file is changed) and would use the cache for all other services and</span></span>

2) <span data-ttu-id="c6596-240">Ponieważ większy obraz występuje w pośrednim etapie, nie ma wpływu na końcowy rozmiar obrazu.</span><span class="sxs-lookup"><span data-stu-id="c6596-240">Since the larger image occurs in an intermediate stage it, doesn't affect the final image size.</span></span>

<span data-ttu-id="c6596-241">Kolejna znacząca Optymalizacja obejmuje `restore` polecenie wykonane w wierszu 17, które jest również inne dla każdej usługi eShopOnContainers.</span><span class="sxs-lookup"><span data-stu-id="c6596-241">The next significant optimization involves the `restore` command executed in line 17, which is also different for every service of eShopOnContainers.</span></span> <span data-ttu-id="c6596-242">Jeśli zmienisz ten wiersz na tylko:</span><span class="sxs-lookup"><span data-stu-id="c6596-242">If you change that line to just:</span></span>

```Dockerfile
RUN dotnet restore
```

<span data-ttu-id="c6596-243">Spowoduje to przywrócenie pakietów dla całego rozwiązania, ale następnie ponownie, będzie miało miejsce tylko raz, a nie 15 razy z bieżącą strategią.</span><span class="sxs-lookup"><span data-stu-id="c6596-243">It would restore the packages for the whole solution, but then again, it would do it just once, instead of the 15 times with the current strategy.</span></span>

<span data-ttu-id="c6596-244">Jednak program `dotnet restore` jest uruchamiany tylko wtedy, gdy w folderze istnieje pojedynczy plik projektu lub rozwiązania, więc osiągnięcie tego jest nieco bardziej skomplikowane i sposób jego rozwiązania, bez konieczności zbyt wielu szczegółów:</span><span class="sxs-lookup"><span data-stu-id="c6596-244">However, `dotnet restore` only runs if there's a single project or solution file in the folder, so achieving this is a bit more complicated and the way to solve it, without getting into too many details, is this:</span></span>

1. <span data-ttu-id="c6596-245">Dodaj następujące wiersze do **. dockerignore**:</span><span class="sxs-lookup"><span data-stu-id="c6596-245">Add the following lines to **.dockerignore**:</span></span>

   - <span data-ttu-id="c6596-246">`*.sln`, aby zignorować wszystkie pliki rozwiązań w głównym drzewie folderów</span><span class="sxs-lookup"><span data-stu-id="c6596-246">`*.sln`, to ignore all solution files in the main folder tree</span></span>

   - <span data-ttu-id="c6596-247">`!eShopOnContainers-ServicesAndWebApps.sln`, aby uwzględnić tylko ten plik rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="c6596-247">`!eShopOnContainers-ServicesAndWebApps.sln`, to include only this solution file.</span></span>

2. <span data-ttu-id="c6596-248">Uwzględnij `dotnet restore`argument do, dlatego również ignoruje projekt platformy Docker-Zredaguj i przywraca tylko pakiety dla rozwiązania eShopOnContainers-ServicesAndWebApps. `/ignoreprojectextensions:.dcproj`</span><span class="sxs-lookup"><span data-stu-id="c6596-248">Include the `/ignoreprojectextensions:.dcproj` argument to `dotnet restore`, so it also ignores the docker-compose project and only restores the packages for the eShopOnContainers-ServicesAndWebApps solution.</span></span>

<span data-ttu-id="c6596-249">W przypadku optymalizacji końcowej następuje po prostu, że wiersz 20 jest nadmiarowy, ponieważ wiersz 23 również kompiluje aplikację i znajduje się w stanie, bezpośrednio po wierszu 20, dlatego inne czasochłonne polecenie.</span><span class="sxs-lookup"><span data-stu-id="c6596-249">For the final optimization, it just happens that line 20 is redundant, as line 23 also builds the application and comes, in essence, right after line 20, so there goes another time-consuming command.</span></span>

<span data-ttu-id="c6596-250">Otrzymany plik jest następnie:</span><span class="sxs-lookup"><span data-stu-id="c6596-250">The resulting file is then:</span></span>

```Dockerfile
 1  FROM mcr.microsoft.com/dotnet/core/aspnet:2.2 AS base
 2  WORKDIR /app
 3  EXPOSE 80
 4
 5  FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS publish
 6  WORKDIR /src
 7  COPY . .
 8  RUN dotnet restore /ignoreprojectextensions:.dcproj
 9  WORKDIR /src/src/Services/Catalog/Catalog.API
10  RUN dotnet publish Catalog.API.csproj -c Release -0 /app
11
12  FROM base AS final
13  WORKDIR /app
14  COPY --from=publish /app
15  ENTRYPOINT ["dotnet", "Catalog.API.dll"]
```

### <a name="creating-your-base-image-from-scratch"></a><span data-ttu-id="c6596-251">Tworzenie obrazu podstawowego od podstaw</span><span class="sxs-lookup"><span data-stu-id="c6596-251">Creating your base image from scratch</span></span>

<span data-ttu-id="c6596-252">Możesz utworzyć własny obraz podstawowy platformy Docker od podstaw.</span><span class="sxs-lookup"><span data-stu-id="c6596-252">You can create your own Docker base image from scratch.</span></span> <span data-ttu-id="c6596-253">Ten scenariusz nie jest zalecany dla osoby, która rozpoczyna się od platformy Docker, ale jeśli chcesz ustawić określone bity obrazu podstawowego, możesz to zrobić.</span><span class="sxs-lookup"><span data-stu-id="c6596-253">This scenario is not recommended for someone who is starting with Docker, but if you want to set the specific bits of your own base image, you can do so.</span></span>

### <a name="additional-resources"></a><span data-ttu-id="c6596-254">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="c6596-254">Additional resources</span></span>

- <span data-ttu-id="c6596-255">**Obrazy .NET Core z obsługą wielodostępności**. </span><span class="sxs-lookup"><span data-stu-id="c6596-255">**Multi-arch .NET Core images**.</span></span>\
  <https://github.com/dotnet/announcements/issues/14>

- <span data-ttu-id="c6596-256">**Utwórz obraz podstawowy**.</span><span class="sxs-lookup"><span data-stu-id="c6596-256">**Create a base image**.</span></span> <span data-ttu-id="c6596-257">Oficjalna dokumentacja platformy Docker. </span><span class="sxs-lookup"><span data-stu-id="c6596-257">Official Docker documentation.</span></span>\
  <https://docs.docker.com/develop/develop-images/baseimages/>

![3 — Tworzenie obrazów zdefiniowanych w wieloetapowe dockerfile](./media/image7.png)

## <a name="step-3-create-your-custom-docker-images-and-embed-your-application-or-service-in-them"></a><span data-ttu-id="c6596-259">Krok 3.</span><span class="sxs-lookup"><span data-stu-id="c6596-259">Step 3.</span></span> <span data-ttu-id="c6596-260">Tworzenie niestandardowych obrazów platformy Docker i osadzanie w nich aplikacji lub usługi</span><span class="sxs-lookup"><span data-stu-id="c6596-260">Create your custom Docker images and embed your application or service in them</span></span>

<span data-ttu-id="c6596-261">Dla każdej usługi w aplikacji należy utworzyć powiązany obraz.</span><span class="sxs-lookup"><span data-stu-id="c6596-261">For each service in your application, you need to create a related image.</span></span> <span data-ttu-id="c6596-262">Jeśli aplikacja składa się z pojedynczej usługi lub aplikacji sieci Web, wystarczy tylko jeden obraz.</span><span class="sxs-lookup"><span data-stu-id="c6596-262">If your application is made up of a single service or web application, you just need a single image.</span></span>

<span data-ttu-id="c6596-263">Należy pamiętać, że obrazy platformy Docker są kompilowane automatycznie w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c6596-263">Note that the Docker images are built automatically for you in Visual Studio.</span></span> <span data-ttu-id="c6596-264">Poniższe kroki są wymagane tylko w przypadku przepływu pracy edytora/interfejsu wiersza polecenia i wyjaśniono, aby wyjaśnić, co się dzieje poniżej.</span><span class="sxs-lookup"><span data-stu-id="c6596-264">The following steps are only needed for the editor/CLI workflow and explained for clarity about what happens underneath.</span></span>

<span data-ttu-id="c6596-265">Programista musi opracowywać i testować lokalnie do momentu wypchnięcia ukończonej funkcji lub zmiany systemu kontroli źródła (na przykład do usługi GitHub).</span><span class="sxs-lookup"><span data-stu-id="c6596-265">You, as a developer, need to develop and test locally until you push a completed feature or change to your source control system (for example, to GitHub).</span></span> <span data-ttu-id="c6596-266">Oznacza to, że należy utworzyć obrazy platformy Docker i wdrożyć kontenery na lokalnym hoście platformy Docker (maszynie wirtualnej z systemem Windows lub Linux) i uruchamiać, testować i debugować względem tych lokalnych kontenerów.</span><span class="sxs-lookup"><span data-stu-id="c6596-266">This means that you need to create the Docker images and deploy containers to a local Docker host (Windows or Linux VM) and run, test, and debug against those local containers.</span></span>

<span data-ttu-id="c6596-267">Aby utworzyć niestandardowy obraz w środowisku lokalnym przy użyciu interfejsu wiersza polecenia platformy Docker i pliku dockerfile, można użyć narzędzia Docker Build, jak pokazano na rysunku 5-5.</span><span class="sxs-lookup"><span data-stu-id="c6596-267">To create a custom image in your local environment by using Docker CLI and your Dockerfile, you can use the docker build command, as in Figure 5-5.</span></span>

![Ekran postępu tworzenia obrazu platformy Docker](./media/image8.png)

<span data-ttu-id="c6596-269">**Rysunek 5-5**.</span><span class="sxs-lookup"><span data-stu-id="c6596-269">**Figure 5-5**.</span></span> <span data-ttu-id="c6596-270">Tworzenie niestandardowego obrazu platformy Docker</span><span class="sxs-lookup"><span data-stu-id="c6596-270">Creating a custom Docker image</span></span>

<span data-ttu-id="c6596-271">Opcjonalnie, zamiast bezpośrednio uruchamiać kompilację platformy Docker z folderu projektu, można najpierw wygenerować folder do wdrożenia z wymaganymi bibliotekami i plikami binarnymi platformy .NET `dotnet publish`, uruchamiając `docker build` polecenie, a następnie użyć polecenia.</span><span class="sxs-lookup"><span data-stu-id="c6596-271">Optionally, instead of directly running docker build from the project folder, you can first generate a deployable folder with the required .NET libraries and binaries by running `dotnet publish`, and then use the `docker build` command.</span></span>

<span data-ttu-id="c6596-272">Spowoduje to utworzenie obrazu platformy Docker o nazwie `cesardl/netcore-webapi-microservice-docker:first`.</span><span class="sxs-lookup"><span data-stu-id="c6596-272">This will create a Docker image with the name `cesardl/netcore-webapi-microservice-docker:first`.</span></span> <span data-ttu-id="c6596-273">W tym przypadku: pierwszy jest tagiem reprezentującym określoną wersję.</span><span class="sxs-lookup"><span data-stu-id="c6596-273">In this case, :first is a tag representing a specific version.</span></span> <span data-ttu-id="c6596-274">Możesz powtórzyć ten krok dla każdego niestandardowego obrazu, który trzeba utworzyć dla złożonej aplikacji platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="c6596-274">You can repeat this step for each custom image you need to create for your composed Docker application.</span></span>

<span data-ttu-id="c6596-275">Gdy aplikacja składa się z wielu kontenerów (czyli aplikacji z wieloma kontenerami), można również użyć `docker-compose up --build` polecenia, aby skompilować wszystkie powiązane obrazy za pomocą jednego polecenia, korzystając z metadanych uwidocznionych w pokrewnych plikach Docker-Compose. yml .</span><span class="sxs-lookup"><span data-stu-id="c6596-275">When an application is made of multiple containers (that is, it is a multi-container application), you can also use the `docker-compose up --build` command to build all the related images with a single command by using the metadata exposed in the related docker-compose.yml files.</span></span>

<span data-ttu-id="c6596-276">Istniejące obrazy można znaleźć w lokalnym repozytorium za pomocą polecenia Docker images, jak pokazano na rysunku 5-6.</span><span class="sxs-lookup"><span data-stu-id="c6596-276">You can find the existing images in your local repository by using the docker images command, as shown in Figure 5-6.</span></span>

![Widok ekranu obrazów z listy obrazów platformy Docker](./media/image9.png)

<span data-ttu-id="c6596-278">**Rysunek 5-6.**</span><span class="sxs-lookup"><span data-stu-id="c6596-278">**Figure 5-6.**</span></span> <span data-ttu-id="c6596-279">Wyświetlanie istniejących obrazów przy użyciu polecenia Docker images</span><span class="sxs-lookup"><span data-stu-id="c6596-279">Viewing existing images using the docker images command</span></span>

### <a name="creating-docker-images-with-visual-studio"></a><span data-ttu-id="c6596-280">Tworzenie obrazów platformy Docker za pomocą programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c6596-280">Creating Docker images with Visual Studio</span></span>

<span data-ttu-id="c6596-281">Gdy używasz programu Visual Studio do tworzenia projektu z obsługą platformy Docker, nie utworzysz jawnie obrazu.</span><span class="sxs-lookup"><span data-stu-id="c6596-281">When you use Visual Studio to create a project with Docker support, you don't explicitly create an image.</span></span> <span data-ttu-id="c6596-282">Zamiast tego obraz jest tworzony po naciśnięciu klawisza **F5** (lub **klawisza CTRL-F5**), aby uruchomić aplikację lub usługę dockerized.</span><span class="sxs-lookup"><span data-stu-id="c6596-282">Instead, the image is created for you when you press **F5** (or **Ctrl-F5**) to run the dockerized application or service.</span></span> <span data-ttu-id="c6596-283">Ten krok jest automatycznie w programie Visual Studio i nie jest wyświetlany, ale ważne jest, aby wiedzieć, co się dzieje poniżej.</span><span class="sxs-lookup"><span data-stu-id="c6596-283">This step is automatic in Visual Studio and you won't see it happen, but it's important that you know what's going on underneath.</span></span>

![4 — (opcjonalnie) redagowanie usług w pliku Docker-Compose. yml](./media/image10.png)

## <a name="step-4-define-your-services-in-docker-composeyml-when-building-a-multi-container-docker-application"></a><span data-ttu-id="c6596-285">Krok 4.</span><span class="sxs-lookup"><span data-stu-id="c6596-285">Step 4.</span></span> <span data-ttu-id="c6596-286">Zdefiniuj usługi w Docker-Compose. yml podczas kompilowania aplikacji platformy Docker z obsługą kontenera</span><span class="sxs-lookup"><span data-stu-id="c6596-286">Define your services in docker-compose.yml when building a multi-container Docker application</span></span>

<span data-ttu-id="c6596-287">Plik [Docker-Compose. yml](https://docs.docker.com/compose/compose-file/) umożliwia zdefiniowanie zestawu powiązanych usług, które mają zostać wdrożone jako aplikacja złożona z poleceniami wdrażania.</span><span class="sxs-lookup"><span data-stu-id="c6596-287">The [docker-compose.yml](https://docs.docker.com/compose/compose-file/) file lets you define a set of related services to be deployed as a composed application with deployment commands.</span></span> <span data-ttu-id="c6596-288">Konfiguruje także relacje zależności i konfigurację uruchomieniową.</span><span class="sxs-lookup"><span data-stu-id="c6596-288">It also configures its dependency relations and run-time configuration.</span></span>

<span data-ttu-id="c6596-289">Aby użyć pliku Docker-Compose. yml, należy utworzyć plik w głównym lub głównym folderze rozwiązania o zawartości podobnej do następującej w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="c6596-289">To use a docker-compose.yml file, you need to create the file in your main or root solution folder, with content similar to that in the following example:</span></span>

```yml
version: '3.4'

services:

  webmvc:
    image: eshop/web
    environment:
      - CatalogUrl=http://catalog.api
      - OrderingUrl=http://ordering.api
    ports:
      - "80:80"
    depends_on:
      - catalog.api
      - ordering.api

  catalog.api:
    image: eshop/catalog.api
    environment:
      - ConnectionString=Server=sql.data;Port=1433;Database=CatalogDB;…
    ports:
      - "81:80"
    depends_on:
      - sql.data

  ordering.api:
    image: eshop/ordering.api
    environment:
      - ConnectionString=Server=sql.data;Database=OrderingDb;…
    ports:
      - "82:80"
    extra_hosts:
      - "CESARDLBOOKVHD:10.0.75.1"
    depends_on:
      - sql.data

  sql.data:
    image: mssql-server-linux:latest
    environment:
      - SA_PASSWORD=Pass@word
      - ACCEPT_EULA=Y
    ports:
      - "5433:1433"
```

<span data-ttu-id="c6596-290">Ten plik Docker-Compose. yml jest uproszczoną i scaloną wersją.</span><span class="sxs-lookup"><span data-stu-id="c6596-290">This docker-compose.yml file is a simplified and merged version.</span></span> <span data-ttu-id="c6596-291">Zawiera statyczne dane konfiguracji dla każdego kontenera (takie jak nazwa obrazu niestandardowego), które jest zawsze wymagane i informacje o konfiguracji, które mogą być zależne od środowiska wdrażania, takie jak parametry połączenia.</span><span class="sxs-lookup"><span data-stu-id="c6596-291">It contains static configuration data for each container (like the name of the custom image), which is always required, and configuration information that might depend on the deployment environment, like the connection string.</span></span> <span data-ttu-id="c6596-292">W kolejnych sekcjach dowiesz się, jak podzielić konfigurację Docker-Compose. yml na wiele plików programu Docker i zastąpić wartości w zależności od typu środowiska i wykonywania (debugowanie lub wydanie).</span><span class="sxs-lookup"><span data-stu-id="c6596-292">In later sections, you will learn how to split the docker-compose.yml configuration into multiple docker-compose files and override values depending on the environment and execution type (debug or release).</span></span>

<span data-ttu-id="c6596-293">Przykład pliku Docker-Compose. yml definiuje cztery usługi `webmvc` : usługa (aplikacja sieci Web), dwa mikrousługi (`ordering.api` i `basket.api` `sql.data`) oraz jeden kontener źródła danych, na podstawie SQL Server dla systemu Linux działającego jako wbudowane.</span><span class="sxs-lookup"><span data-stu-id="c6596-293">The docker-compose.yml file example defines four services: the `webmvc` service (a web application), two microservices (`ordering.api` and `basket.api`), and one data source container, `sql.data`, based on SQL Server for Linux running as a container.</span></span> <span data-ttu-id="c6596-294">Każda usługa zostanie wdrożona jako kontener, dlatego dla każdego z nich wymagany jest obraz platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="c6596-294">Each service will be deployed as a container, so a Docker image is required for each.</span></span>

<span data-ttu-id="c6596-295">Plik Docker-Compose. yml określa nie tylko te kontenery, które są używane, ale w jaki sposób są indywidualnie skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="c6596-295">The docker-compose.yml file specifies not only what containers are being used, but how they are individually configured.</span></span> <span data-ttu-id="c6596-296">Na przykład `webmvc` definicja kontenera w pliku. yml:</span><span class="sxs-lookup"><span data-stu-id="c6596-296">For instance, the `webmvc` container definition in the .yml file:</span></span>

- <span data-ttu-id="c6596-297">Używa wstępnie skompilowanego `eshop/web:latest` obrazu.</span><span class="sxs-lookup"><span data-stu-id="c6596-297">Uses a pre-built `eshop/web:latest` image.</span></span> <span data-ttu-id="c6596-298">Można jednak skonfigurować obraz, który ma zostać skompilowany w ramach wykonywania operacji Docker — tworzenie z dodatkową konfiguracją w oparciu o kompilację: sekcja w pliku Docker-redagowanie.</span><span class="sxs-lookup"><span data-stu-id="c6596-298">However, you could also configure the image to be built as part of the docker-compose execution with an additional configuration based on a build: section in the docker-compose file.</span></span>

- <span data-ttu-id="c6596-299">Inicjuje dwie zmienne środowiskowe (CatalogUrl i OrderingUrl).</span><span class="sxs-lookup"><span data-stu-id="c6596-299">Initializes two environment variables (CatalogUrl and OrderingUrl).</span></span>

- <span data-ttu-id="c6596-300">Przekazuje uwidoczniony port 80 w kontenerze do zewnętrznego portu 80 na komputerze-hoście.</span><span class="sxs-lookup"><span data-stu-id="c6596-300">Forwards the exposed port 80 on the container to the external port 80 on the host machine.</span></span>

- <span data-ttu-id="c6596-301">Łączy aplikację sieci Web z katalogiem i usługą porządkowania przy użyciu ustawienia depends_on.</span><span class="sxs-lookup"><span data-stu-id="c6596-301">Links the web app to the catalog and ordering service with the depends_on setting.</span></span> <span data-ttu-id="c6596-302">Powoduje to, że usługa czeka na uruchomienie tych usług.</span><span class="sxs-lookup"><span data-stu-id="c6596-302">This causes the service to wait until those services are started.</span></span>

<span data-ttu-id="c6596-303">Będziemy ponownie odwiedzać plik Docker-Compose. yml w dalszej części, gdy będziemy omawiać sposób implementacji mikrousług i aplikacji wielokontenerowych.</span><span class="sxs-lookup"><span data-stu-id="c6596-303">We will revisit the docker-compose.yml file in a later section when we cover how to implement microservices and multi-container apps.</span></span>

### <a name="working-with-docker-composeyml-in-visual-studio-2017"></a><span data-ttu-id="c6596-304">Praca z Docker-Compose. yml w programie Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="c6596-304">Working with docker-compose.yml in Visual Studio 2017</span></span>

<span data-ttu-id="c6596-305">Oprócz dodania pliku dockerfile do projektu, jak wspomniano wcześniej, program Visual Studio 2017 (z 15,8 on) może dodać obsługę programu Orchestrator dla Docker Compose do rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="c6596-305">Besides adding a Dockerfile to a project, as we mentioned before, Visual Studio 2017 (from 15.8 on) can add orchestrator support for Docker Compose to a solution.</span></span>

<span data-ttu-id="c6596-306">Po dodaniu obsługi programu Orchestrator Container, jak pokazano na rysunku 5-7 po raz pierwszy, program Visual Studio tworzy pliku dockerfile dla projektu i tworzy nowy projekt (sekcja usługi) w rozwiązaniu z kilkoma plikami globalnymi `docker-compose*.yml` , a następnie dodaje projekt do tych plików.</span><span class="sxs-lookup"><span data-stu-id="c6596-306">When you add container orchestrator support, as shown in Figure 5-7, for the first time, Visual Studio creates the Dockerfile for the project and creates a new (service section) project in your solution with several global `docker-compose*.yml` files, and then adds the project to those files.</span></span> <span data-ttu-id="c6596-307">Następnie możesz otworzyć pliki Docker-Compose. yml i zaktualizować je za pomocą dodatkowych funkcji.</span><span class="sxs-lookup"><span data-stu-id="c6596-307">You can then open the docker-compose.yml files and update them with additional features.</span></span>

<span data-ttu-id="c6596-308">Musisz powtórzyć ten formularz dla każdego projektu, który ma zostać uwzględniony w pliku Docker-Compose. yml.</span><span class="sxs-lookup"><span data-stu-id="c6596-308">You have to repeat this operation form every project you want to include in the docker-compose.yml file.</span></span>

<span data-ttu-id="c6596-309">W czasie tego pisania program Visual Studio obsługuje Docker Compose i Service Fabric koordynatorów.</span><span class="sxs-lookup"><span data-stu-id="c6596-309">At the time of this writing, Visual Studio supports Docker Compose and Service Fabric orchestrators.</span></span>

![Opcja menu kontekstowego umożliwiająca dodanie obsługi programu Orchestrator do projektu ASP.NET Core](./media/image21.png)

<span data-ttu-id="c6596-311">**Rysunek 5-7**.</span><span class="sxs-lookup"><span data-stu-id="c6596-311">**Figure 5-7**.</span></span> <span data-ttu-id="c6596-312">Dodawanie obsługi platformy Docker w programie Visual Studio 2017 przez kliknięcie prawym przyciskiem myszy ASP.NET Core projektu</span><span class="sxs-lookup"><span data-stu-id="c6596-312">Adding Docker support in Visual Studio 2017 by right-clicking an ASP.NET Core project</span></span>

<span data-ttu-id="c6596-313">Po dodaniu obsługi programu Orchestrator do rozwiązania w programie Visual Studio zobaczysz również nowy węzeł (w `docker-compose.dcproj` pliku projektu) w Eksplorator rozwiązań zawierającym dodane pliki Docker-Compose. yml, jak pokazano na rysunku 5-8.</span><span class="sxs-lookup"><span data-stu-id="c6596-313">After you add orchestrator support to your solution in Visual Studio, you will also see a new node (in the `docker-compose.dcproj` project file) in Solution Explorer that contains the added docker-compose.yml files, as shown in Figure 5-8.</span></span>

![Docker — Tworzenie węzła w Eksplorator rozwiązań](./media/image11.png)

<span data-ttu-id="c6596-315">**Rysunek 5-8**.</span><span class="sxs-lookup"><span data-stu-id="c6596-315">**Figure 5-8**.</span></span> <span data-ttu-id="c6596-316">Węzeł drzewa **platformy Docker — tworzenie** w programie Visual Studio 2017 Eksplorator rozwiązań</span><span class="sxs-lookup"><span data-stu-id="c6596-316">The **docker-compose** tree node added in Visual Studio 2017 Solution Explorer</span></span>

<span data-ttu-id="c6596-317">Za pomocą `docker-compose up` polecenia można wdrożyć wielokontenerową aplikację z pojedynczym plikiem Docker-Compose. yml.</span><span class="sxs-lookup"><span data-stu-id="c6596-317">You could deploy a multi-container application with a single docker-compose.yml file by using the `docker-compose up` command.</span></span> <span data-ttu-id="c6596-318">Jednak program Visual Studio dodaje grupę tych grup, aby można było przesłonić wartości w zależności od środowiska (programowania lub produkcji) oraz typu wykonywania (wersja lub debugowanie).</span><span class="sxs-lookup"><span data-stu-id="c6596-318">However, Visual Studio adds a group of them so you can override values depending on the environment (development or production) and execution type (release or debug).</span></span> <span data-ttu-id="c6596-319">Ta funkcja zostanie omówiona w dalszych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="c6596-319">This capability will be explained in later sections.</span></span>

![5 — Uruchamianie kontenerów lub aplikacji złożonej](./media/image12.png)

## <a name="step-5-build-and-run-your-docker-application"></a><span data-ttu-id="c6596-321">Krok 5.</span><span class="sxs-lookup"><span data-stu-id="c6596-321">Step 5.</span></span> <span data-ttu-id="c6596-322">Kompilowanie i uruchamianie aplikacji platformy Docker</span><span class="sxs-lookup"><span data-stu-id="c6596-322">Build and run your Docker application</span></span>

<span data-ttu-id="c6596-323">Jeśli aplikacja ma tylko jeden kontener, można uruchomić ją, wdrażając ją na hoście platformy Docker (maszynie wirtualnej lub serwerze fizycznym).</span><span class="sxs-lookup"><span data-stu-id="c6596-323">If your application only has a single container, you can run it by deploying it to your Docker host (VM or physical server).</span></span> <span data-ttu-id="c6596-324">Jeśli jednak aplikacja zawiera wiele usług, można wdrożyć ją jako aplikację składającą się z pojedynczego interfejsu wiersza polecenia (Docker-Zredaguj) lub z programem Visual Studio, który będzie używać tego polecenia w obszarze okładki.</span><span class="sxs-lookup"><span data-stu-id="c6596-324">However, if your application contains multiple services, you can deploy it as a composed application, either using a single CLI command (docker-compose up), or with Visual Studio, which will use that command under the covers.</span></span> <span data-ttu-id="c6596-325">Przyjrzyjmy się różnym opcjom.</span><span class="sxs-lookup"><span data-stu-id="c6596-325">Let's look at the different options.</span></span>

### <a name="option-a-running-a-single-container-application"></a><span data-ttu-id="c6596-326">Opcja A: Uruchamianie aplikacji z jednym kontenerem</span><span class="sxs-lookup"><span data-stu-id="c6596-326">Option A: Running a single-container application</span></span>

#### <a name="using-docker-cli"></a><span data-ttu-id="c6596-327">Korzystanie z interfejsu wiersza polecenia platformy Docker</span><span class="sxs-lookup"><span data-stu-id="c6596-327">Using Docker CLI</span></span>

<span data-ttu-id="c6596-328">Kontener platformy Docker można uruchomić za pomocą `docker run` polecenia, jak pokazano na rysunku 5-9:</span><span class="sxs-lookup"><span data-stu-id="c6596-328">You can run a Docker container using the `docker run` command, as shown in Figure 5-9:</span></span>

```console
  docker run -t -d -p 80:5000 cesardl/netcore-webapi-microservice-docker:first
```

<span data-ttu-id="c6596-329">Powyższe polecenie spowoduje utworzenie nowego wystąpienia kontenera z określonego obrazu przy każdym uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="c6596-329">The above command will create a new container instance from the specified image, every time it's run.</span></span> <span data-ttu-id="c6596-330">Można użyć `--name` parametru, aby nadać nazwę kontenerowi, a następnie użyć `docker start {name}` (lub użyć identyfikatora kontenera lub nazwy automatycznej) do uruchomienia istniejącego wystąpienia kontenera.</span><span class="sxs-lookup"><span data-stu-id="c6596-330">You can use the `--name` parameter to give a name to the container and then use `docker start {name}` (or use the container id or automatic name) to run an existing container instance.</span></span>

![Widok ekranu podczas uruchamiania kontenera Docker przy użyciu polecenia Docker Run](./media/image13.png)

<span data-ttu-id="c6596-332">**Rysunek 5-9**.</span><span class="sxs-lookup"><span data-stu-id="c6596-332">**Figure 5-9**.</span></span> <span data-ttu-id="c6596-333">Uruchamianie kontenera Docker przy użyciu polecenia Docker Run</span><span class="sxs-lookup"><span data-stu-id="c6596-333">Running a Docker container using the docker run command</span></span>

<span data-ttu-id="c6596-334">W takim przypadku polecenie powiąże wewnętrzny port 5000 kontenera z portem 80 komputera hosta.</span><span class="sxs-lookup"><span data-stu-id="c6596-334">In this case, the command binds the internal port 5000 of the container to port 80 of the host machine.</span></span> <span data-ttu-id="c6596-335">Oznacza to, że host nasłuchuje na porcie 80 i przesyła dalej do portu 5000 w kontenerze.</span><span class="sxs-lookup"><span data-stu-id="c6596-335">This means that the host is listening on port 80 and forwarding to port 5000 on the container.</span></span>

<span data-ttu-id="c6596-336">Wyświetlany skrót jest identyfikatorem kontenera i jest również przypisywany losowo czytelną nazwę, `--name` Jeśli opcja nie jest używana.</span><span class="sxs-lookup"><span data-stu-id="c6596-336">The hash shown is the container id and it’s also assigned a random readable name if the `--name` option is not used.</span></span>

#### <a name="using-visual-studio"></a><span data-ttu-id="c6596-337">Korzystanie z programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c6596-337">Using Visual Studio</span></span>

<span data-ttu-id="c6596-338">Jeśli nie dodano obsługi usługi Orchestrator kontenera, możesz również uruchomić aplikację z jednym kontenerem w programie Visual Studio, naciskając **klawisze CTRL-F5** i można także użyć klawisza **F5** do debugowania aplikacji w kontenerze.</span><span class="sxs-lookup"><span data-stu-id="c6596-338">If you haven't added container orchestrator support, you can also run a single container app in Visual Studio by pressing **Ctrl-F5** and you can also use **F5** to debug the application within the container.</span></span> <span data-ttu-id="c6596-339">Kontener jest uruchamiany lokalnie przy użyciu uruchomienia platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="c6596-339">The container runs locally using docker run.</span></span>

### <a name="option-b-running-a-multi-container-application"></a><span data-ttu-id="c6596-340">Opcja B: Uruchamianie aplikacji z obsługą kontenera</span><span class="sxs-lookup"><span data-stu-id="c6596-340">Option B: Running a multi-container application</span></span>

<span data-ttu-id="c6596-341">W większości scenariuszy przedsiębiorstwa aplikacja platformy Docker będzie składać się z wielu usług, co oznacza, że należy uruchomić aplikację obejmującą wiele kontenerów, jak pokazano na rysunku 5-10.</span><span class="sxs-lookup"><span data-stu-id="c6596-341">In most enterprise scenarios, a Docker application will be composed of multiple services, which means you need to run a multi-container application, as shown in Figure 5-10.</span></span>

![Maszyna wirtualna z kilkoma kontenerami platformy Docker](./media/image14.png)

<span data-ttu-id="c6596-343">**Rysunek 5-10**.</span><span class="sxs-lookup"><span data-stu-id="c6596-343">**Figure 5-10**.</span></span> <span data-ttu-id="c6596-344">Maszyna wirtualna z wdrożonymi kontenerami platformy Docker</span><span class="sxs-lookup"><span data-stu-id="c6596-344">VM with Docker containers deployed</span></span>

#### <a name="using-docker-cli"></a><span data-ttu-id="c6596-345">Korzystanie z interfejsu wiersza polecenia platformy Docker</span><span class="sxs-lookup"><span data-stu-id="c6596-345">Using Docker CLI</span></span>

<span data-ttu-id="c6596-346">Aby uruchomić aplikację z obsługą kontenera przy użyciu interfejsu wiersza polecenia platformy Docker, `docker-compose up` należy wykonać polecenie.</span><span class="sxs-lookup"><span data-stu-id="c6596-346">To run a multi-container application with the Docker CLI, you use the `docker-compose up` command.</span></span> <span data-ttu-id="c6596-347">To polecenie używa pliku **Docker-Compose. yml** , który posiadasz na poziomie rozwiązania do wdrożenia aplikacji wielokontenerowej.</span><span class="sxs-lookup"><span data-stu-id="c6596-347">This command uses the **docker-compose.yml** file that you have at the solution level to deploy a multi-container application.</span></span> <span data-ttu-id="c6596-348">Rysunek 5-11 przedstawia wyniki podczas uruchamiania polecenia z głównego katalogu rozwiązania, który zawiera plik Docker-Compose. yml.</span><span class="sxs-lookup"><span data-stu-id="c6596-348">Figure 5-11 shows the results when running the command from your main solution directory, which contains the docker-compose.yml file.</span></span>

![Widok ekranu podczas uruchamiania polecenia Docker-Zredaguj w górę](./media/image15.png)

<span data-ttu-id="c6596-350">**Rysunek 5-11**.</span><span class="sxs-lookup"><span data-stu-id="c6596-350">**Figure 5-11**.</span></span> <span data-ttu-id="c6596-351">Przykładowe wyniki podczas uruchamiania polecenia Docker-Zredaguj w górę</span><span class="sxs-lookup"><span data-stu-id="c6596-351">Example results when running the docker-compose up command</span></span>

<span data-ttu-id="c6596-352">Po uruchomieniu polecenia "Docker-Zredaguj" aplikacja i powiązane z nim kontenery zostaną wdrożone na hoście platformy Docker, jak przedstawiono na rysunku 5-10.</span><span class="sxs-lookup"><span data-stu-id="c6596-352">After the docker-compose up command runs, the application and its related containers are deployed into your Docker host, as depicted in Figure 5-10.</span></span>

#### <a name="using-visual-studio"></a><span data-ttu-id="c6596-353">Korzystanie z programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c6596-353">Using Visual Studio</span></span>

<span data-ttu-id="c6596-354">Uruchamianie aplikacji wielokontenerowej przy użyciu programu Visual Studio 2017 nie może być prostsze.</span><span class="sxs-lookup"><span data-stu-id="c6596-354">Running a multi-container application using Visual Studio 2017 can't get any simpler.</span></span> <span data-ttu-id="c6596-355">Wystarczy nacisnąć **kombinację klawiszy CTRL-F5** , aby uruchomić lub **F5** w celu debugowania, jak zwykle, konfigurując projekt **Docker-Zredaguj** jako projekt startowy.</span><span class="sxs-lookup"><span data-stu-id="c6596-355">You just press **Ctrl-F5** to run or **F5** to debug, as usual, setting up the **docker-compose** project as the startup project.</span></span>  <span data-ttu-id="c6596-356">Program Visual Studio obsługuje wszystkie potrzebne ustawienia, dzięki czemu można tworzyć punkty przerwania w zwykły sposób i debugować, co kończy się niezależnymi procesami uruchomionymi na "serwerach zdalnych", podobnie jak w przypadku tego.</span><span class="sxs-lookup"><span data-stu-id="c6596-356">Visual Studio handles all needed setup, so you can create breakpoints as usual and debug what finally become independent processes running in "remote servers", just like that.</span></span>

<span data-ttu-id="c6596-357">Jak wspomniano wcześniej, za każdym razem, gdy dodasz obsługę rozwiązania Docker do projektu w ramach rozwiązania, ten projekt jest konfigurowany w pliku globalnym (na poziomie rozwiązania) Docker-Compose. yml, który umożliwia jednoczesne uruchamianie lub debugowanie całego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="c6596-357">As mentioned before, each time you add Docker solution support to a project within a solution, that project is configured in the global (solution-level) docker-compose.yml file, which lets you run or debug the whole solution at once.</span></span> <span data-ttu-id="c6596-358">Program Visual Studio uruchomi jeden kontener dla każdego projektu, który ma włączoną obsługę rozwiązania Docker, i wykona wszystkie czynności wewnętrzne (dotnet publish, kompilacja platformy Docker itp.).</span><span class="sxs-lookup"><span data-stu-id="c6596-358">Visual Studio will start one container for each project that has Docker solution support enabled, and perform all the internal steps for you (dotnet publish, docker build, etc.).</span></span>

<span data-ttu-id="c6596-359">Jeśli chcesz skorzystać ze wszystkich drudgery, zapoznaj się z plikiem:</span><span class="sxs-lookup"><span data-stu-id="c6596-359">If you want to take a peek at all the drudgery, take a look at the file:</span></span>

`{root solution folder}\obj\Docker\docker-compose.vs.debug.g.yml`

<span data-ttu-id="c6596-360">Ważnym punktem jest to, jak pokazano na rysunku 5-12 w programie Visual Studio 2017 istnieje dodatkowe polecenie **platformy Docker** dla akcji klawisza F5.</span><span class="sxs-lookup"><span data-stu-id="c6596-360">The important point here is that, as shown in Figure 5-12, in Visual Studio 2017 there is an additional **Docker** command for the F5 key action.</span></span> <span data-ttu-id="c6596-361">Ta opcja umożliwia uruchamianie lub debugowanie aplikacji wielokontenerowych przez uruchomienie wszystkich kontenerów, które są zdefiniowane w plikach Docker-Compose. yml na poziomie rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="c6596-361">This option lets you run or debug a multi-container application by running all the containers that are defined in the docker-compose.yml files at the solution level.</span></span> <span data-ttu-id="c6596-362">Możliwość debugowania rozwiązań obejmujących wiele kontenerów oznacza, że można ustawić kilka punktów przerwania, każdy punkt przerwania w innym projekcie (kontener), a podczas debugowania z programu Visual Studio zatrzymano punkty przerwania zdefiniowane w różnych projektach i uruchomione na różne kontenery.</span><span class="sxs-lookup"><span data-stu-id="c6596-362">The ability to debug multiple-container solutions means that you can set several breakpoints, each breakpoint in a different project (container), and while debugging from Visual Studio you will stop at breakpoints defined in different projects and running on different containers.</span></span>

![Pasek narzędzi debugowania programu Visual Studio z uruchomionym programem Docker — redagowanie projektu](./media/image16.png)

<span data-ttu-id="c6596-364">**Rysunek 5-12**.</span><span class="sxs-lookup"><span data-stu-id="c6596-364">**Figure 5-12**.</span></span> <span data-ttu-id="c6596-365">Uruchamianie aplikacji z obsługą kontenera w programie Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="c6596-365">Running multi-container apps in Visual Studio 2017</span></span>

### <a name="additional-resources"></a><span data-ttu-id="c6596-366">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="c6596-366">Additional resources</span></span>

- <span data-ttu-id="c6596-367">**Wdrażanie kontenera ASP.NET na zdalnym hoście platformy Docker** </span><span class="sxs-lookup"><span data-stu-id="c6596-367">**Deploy an ASP.NET container to a remote Docker host** </span></span>\
  <https://docs.microsoft.com/azure/vs-azure-tools-docker-hosting-web-apps-in-docker>

### <a name="a-note-about-testing-and-deploying-with-orchestrators"></a><span data-ttu-id="c6596-368">Uwaga dotycząca testowania i wdrażania w programie Orchestrator</span><span class="sxs-lookup"><span data-stu-id="c6596-368">A note about testing and deploying with orchestrators</span></span>

<span data-ttu-id="c6596-369">Polecenia platformy Docker — tworzenie i Docker (lub uruchamianie i debugowanie kontenerów w programie Visual Studio) są odpowiednie do testowania kontenerów w środowisku deweloperskim.</span><span class="sxs-lookup"><span data-stu-id="c6596-369">The docker-compose up and docker run commands (or running and debugging the containers in Visual Studio) are adequate for testing containers in your development environment.</span></span> <span data-ttu-id="c6596-370">Nie należy jednak używać tej metody w przypadku wdrożeń produkcyjnych, w których należy kierować się koordynatorami, takimi jak [Kubernetes](https://kubernetes.io/) lub [Service Fabric](https://azure.microsoft.com/services/service-fabric/).</span><span class="sxs-lookup"><span data-stu-id="c6596-370">But you should not use this approach for production deployments, where you should target orchestrators like [Kubernetes](https://kubernetes.io/) or [Service Fabric](https://azure.microsoft.com/services/service-fabric/).</span></span> <span data-ttu-id="c6596-371">Jeśli używasz programu Kubernetes, musisz użyć [zasobników](https://kubernetes.io/docs/concepts/workloads/pods/pod/) , aby organizować kontenery i [usługi](https://kubernetes.io/docs/concepts/services-networking/service/) w sieci.</span><span class="sxs-lookup"><span data-stu-id="c6596-371">If you're using Kubernetes you have to use [pods](https://kubernetes.io/docs/concepts/workloads/pods/pod/) to organize containers and [services](https://kubernetes.io/docs/concepts/services-networking/service/) to network them.</span></span> <span data-ttu-id="c6596-372">[Wdrożenia](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) są również używane do organizowania pod względem tworzenia i modyfikowania.</span><span class="sxs-lookup"><span data-stu-id="c6596-372">You also use [deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) to organize pod creation and modification.</span></span>

![6 — Testowanie aplikacji lub mikrousług](./media/image17.png)

## <a name="step-6-test-your-docker-application-using-your-local-docker-host"></a><span data-ttu-id="c6596-374">Krok 6.</span><span class="sxs-lookup"><span data-stu-id="c6596-374">Step 6.</span></span> <span data-ttu-id="c6596-375">Testowanie aplikacji platformy Docker przy użyciu lokalnego hosta platformy Docker</span><span class="sxs-lookup"><span data-stu-id="c6596-375">Test your Docker application using your local Docker host</span></span>

<span data-ttu-id="c6596-376">Ten krok będzie się różnić w zależności od tego, co aplikacja działa.</span><span class="sxs-lookup"><span data-stu-id="c6596-376">This step will vary depending on what your application is doing.</span></span> <span data-ttu-id="c6596-377">W prostej aplikacji sieci Web platformy .NET Core wdrożonej jako pojedynczy kontener lub usługa można uzyskać dostęp do usługi, otwierając przeglądarkę na hoście platformy Docker i przechodząc do tej lokacji, jak pokazano na rysunku 5-13.</span><span class="sxs-lookup"><span data-stu-id="c6596-377">In a simple .NET Core Web application that is deployed as a single container or service, you can access the service by opening a browser on the Docker host and navigating to that site, as shown in Figure 5-13.</span></span> <span data-ttu-id="c6596-378">(Jeśli konfiguracja w pliku dockerfile mapuje kontener na port na hoście, który jest inny niż 80, Uwzględnij port hosta w adresie URL).</span><span class="sxs-lookup"><span data-stu-id="c6596-378">(If the configuration in the Dockerfile maps the container to a port on the host that is anything other than 80, include the host port in the URL.)</span></span>

![Widok przeglądarki odpowiedzi punktu końcowego interfejsu API](./media/image18.png)

<span data-ttu-id="c6596-380">**Rysunek 5-13**.</span><span class="sxs-lookup"><span data-stu-id="c6596-380">**Figure 5-13**.</span></span> <span data-ttu-id="c6596-381">Przykład testowania aplikacji platformy Docker lokalnie przy użyciu hosta lokalnego</span><span class="sxs-lookup"><span data-stu-id="c6596-381">Example of testing your Docker application locally using localhost</span></span>

<span data-ttu-id="c6596-382">Jeśli localhost nie wskazuje adresu IP hosta platformy Docker (domyślnie w przypadku korzystania z platformy Docker CE powinien), aby przejść do usługi, użyj adresu IP karty sieciowej maszyny.</span><span class="sxs-lookup"><span data-stu-id="c6596-382">If localhost is not pointing to the Docker host IP (by default, when using Docker CE, it should), to navigate to your service, use the IP address of your machine's network card.</span></span>

<span data-ttu-id="c6596-383">Należy zauważyć, że ten adres URL w przeglądarce używa portu 80 dla określonego przykładowego kontenera.</span><span class="sxs-lookup"><span data-stu-id="c6596-383">Note that this URL in the browser uses port 80 for the particular container example being discussed.</span></span> <span data-ttu-id="c6596-384">Jednak wewnętrznie żądania są przekierowywane do portu 5000, ponieważ było ono wdrożone przy użyciu polecenia Docker Run, zgodnie z opisem w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="c6596-384">However, internally the requests are being redirected to port 5000, because that was how it was deployed with the docker run command, as explained in a previous step.</span></span>

<span data-ttu-id="c6596-385">Możesz również testować aplikację przy użyciu zwinięcia z terminalu, jak pokazano na rysunku 5-14.</span><span class="sxs-lookup"><span data-stu-id="c6596-385">You can also test the application using curl from the terminal, as shown in Figure 5-14.</span></span> <span data-ttu-id="c6596-386">W przypadku instalacji platformy Docker w systemie Windows domyślny adres IP hosta platformy Docker jest zawsze 10.0.75.1 oprócz rzeczywistego adresu IP maszyny.</span><span class="sxs-lookup"><span data-stu-id="c6596-386">In a Docker installation on Windows, the default Docker Host IP is always 10.0.75.1 in addition to your machine's actual IP address.</span></span>

![Widok ekranu odpowiedzi punktu końcowego interfejsu API z zwinięciem](./media/image19.png)

<span data-ttu-id="c6596-388">**Rysunek 5-14**.</span><span class="sxs-lookup"><span data-stu-id="c6596-388">**Figure 5-14**.</span></span> <span data-ttu-id="c6596-389">Przykład testowania aplikacji platformy Docker lokalnie przy użyciu narzędzia zwinięcie</span><span class="sxs-lookup"><span data-stu-id="c6596-389">Example of testing your Docker application locally using curl</span></span>

### <a name="testing-and-debugging-containers-with-visual-studio-2017"></a><span data-ttu-id="c6596-390">Testowanie i debugowanie kontenerów za pomocą programu Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="c6596-390">Testing and debugging containers with Visual Studio 2017</span></span>

<span data-ttu-id="c6596-391">Podczas uruchamiania i debugowania kontenerów za pomocą programu Visual Studio 2017 można debugować aplikację .NET w taki sam sposób, jak w przypadku uruchamiania bez kontenerów.</span><span class="sxs-lookup"><span data-stu-id="c6596-391">When running and debugging the containers with Visual Studio 2017, you can debug the .NET application in much the same way as you would when running without containers.</span></span>

### <a name="testing-and-debugging-without-visual-studio"></a><span data-ttu-id="c6596-392">Testowanie i debugowanie bez programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c6596-392">Testing and debugging without Visual Studio</span></span>

<span data-ttu-id="c6596-393">Jeśli tworzysz program przy użyciu podejścia edytora/interfejsu wiersza polecenia, debugowanie kontenerów jest trudniejsze i chcesz debugować, generując dane śledzenia.</span><span class="sxs-lookup"><span data-stu-id="c6596-393">If you're developing using the editor/CLI approach, debugging containers is more difficult and you will want to debug by generating traces.</span></span>

### <a name="additional-resources"></a><span data-ttu-id="c6596-394">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="c6596-394">Additional resources</span></span>

- <span data-ttu-id="c6596-395">**Debugowanie aplikacji w lokalnym kontenerze platformy Docker** </span><span class="sxs-lookup"><span data-stu-id="c6596-395">**Debugging apps in a local Docker container** </span></span>\
  [https://docs.microsoft.com/visualstudio/containers/edit-and-refresh](/visualstudio/containers/edit-and-refresh)

- <span data-ttu-id="c6596-396">**Steve Lasker. Kompiluj, Debuguj i wdrażaj ASP.NET Core aplikacje przy użyciu platformy Docker.**</span><span class="sxs-lookup"><span data-stu-id="c6596-396">**Steve Lasker. Build, Debug, Deploy ASP.NET Core Apps with Docker.**</span></span> <span data-ttu-id="c6596-397">Plików.</span><span class="sxs-lookup"><span data-stu-id="c6596-397">Video.</span></span> \
  <https://channel9.msdn.com/Events/Visual-Studio/Visual-Studio-2017-Launch/T115>

## <a name="simplified-workflow-when-developing-containers-with-visual-studio"></a><span data-ttu-id="c6596-398">Uproszczony przepływ pracy podczas tworzenia kontenerów za pomocą programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c6596-398">Simplified workflow when developing containers with Visual Studio</span></span>

<span data-ttu-id="c6596-399">Efektywnie, przepływ pracy w przypadku korzystania z programu Visual Studio jest znacznie prostszy niż w przypadku korzystania z metody edytora/interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="c6596-399">Effectively, the workflow when using Visual Studio is a lot simpler than if you use the editor/CLI approach.</span></span> <span data-ttu-id="c6596-400">Większość kroków wymaganych przez platformę Docker związanych z plikami pliku dockerfile i Docker-Compose. yml jest ukryta lub uproszczona przez program Visual Studio, jak pokazano na rysunku 5-15.</span><span class="sxs-lookup"><span data-stu-id="c6596-400">Most of the steps required by Docker related to the Dockerfile and docker-compose.yml files are hidden or simplified by Visual Studio, as shown in Figure 5-15.</span></span>

![Uproszczony przepływ pracy tworzenia kontenerów za pomocą programu Visual Studio: 1. Zakoduj aplikację, 2 — Dodaj obsługę platformy Docker do projektów (tylko raz), 3-uruchamiaj kontener lub aplikację Docker-Zredaguj, 4 — Przetestuj aplikację lub mikrousługi, 5 — wypychanie do repozytorium i powtarzanie.](./media/image20.png)

<span data-ttu-id="c6596-402">**Rysunek 5-15**.</span><span class="sxs-lookup"><span data-stu-id="c6596-402">**Figure 5-15**.</span></span> <span data-ttu-id="c6596-403">Uproszczony przepływ pracy podczas programowania przy użyciu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c6596-403">Simplified workflow when developing with Visual Studio</span></span>

<span data-ttu-id="c6596-404">Ponadto należy wykonać krok 2 (dodanie obsługi platformy Docker do projektów) tylko raz.</span><span class="sxs-lookup"><span data-stu-id="c6596-404">In addition, you need to perform step 2 (adding Docker support to your projects) just once.</span></span> <span data-ttu-id="c6596-405">W związku z tym przepływ pracy jest podobny do zwykłych zadań programistycznych podczas korzystania z platformy .NET do innych celów programistycznych.</span><span class="sxs-lookup"><span data-stu-id="c6596-405">Therefore, the workflow is similar to your usual development tasks when using .NET for any other development.</span></span> <span data-ttu-id="c6596-406">Musisz wiedzieć, co się dzieje w obszarze okładki (proces kompilowania obrazu, jakie obrazy podstawowe są używane, wdrożenia kontenerów itp.), a czasami trzeba również edytować plik pliku dockerfile lub Docker-Compose. yml w celu dostosowania zachowań.</span><span class="sxs-lookup"><span data-stu-id="c6596-406">You need to know what is going on under the covers (the image build process, what base images you're using, deployment of containers, etc.) and sometimes you will also need to edit the Dockerfile or docker-compose.yml file to customize behaviors.</span></span> <span data-ttu-id="c6596-407">Jednak większość pracy jest znacznie uproszczona przy użyciu programu Visual Studio, dzięki czemu znacznie zwiększa produktywność.</span><span class="sxs-lookup"><span data-stu-id="c6596-407">But most of the work is greatly simplified by using Visual Studio, making you a lot more productive.</span></span>

### <a name="additional-resources"></a><span data-ttu-id="c6596-408">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="c6596-408">Additional resources</span></span>

- <span data-ttu-id="c6596-409">**Steve Lasker. Programowanie platformy .NET Docker za pomocą programu Visual Studio 2017** </span><span class="sxs-lookup"><span data-stu-id="c6596-409">**Steve Lasker. .NET Docker Development with Visual Studio 2017** </span></span>\
  <https://channel9.msdn.com/Events/Visual-Studio/Visual-Studio-2017-Launch/T111>

## <a name="using-powershell-commands-in-a-dockerfile-to-set-up-windows-containers"></a><span data-ttu-id="c6596-410">Konfigurowanie kontenerów systemu Windows za pomocą poleceń programu PowerShell w pliku dockerfile</span><span class="sxs-lookup"><span data-stu-id="c6596-410">Using PowerShell commands in a Dockerfile to set up Windows Containers</span></span>

<span data-ttu-id="c6596-411">[Kontenery systemu Windows](https://docs.microsoft.com/virtualization/windowscontainers/about/index) umożliwiają konwertowanie istniejących aplikacji systemu Windows do obrazów platformy Docker i wdrażanie ich przy użyciu tych samych narzędzi, co w pozostałej części ekosystemu platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="c6596-411">[Windows Containers](https://docs.microsoft.com/virtualization/windowscontainers/about/index) allow you to convert your existing Windows applications into Docker images and deploy them with the same tools as the rest of the Docker ecosystem.</span></span> <span data-ttu-id="c6596-412">Aby korzystać z kontenerów systemu Windows, należy uruchomić polecenia programu PowerShell w pliku dockerfile, jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="c6596-412">To use Windows Containers, you run PowerShell commands in the Dockerfile, as shown in the following example:</span></span>

```Dockerfile
FROM microsoft/windowsservercore
LABEL Description="IIS" Vendor="Microsoft" Version="10"
RUN powershell -Command Add-WindowsFeature Web-Server
CMD [ "ping", "localhost", "-t" ]
```

<span data-ttu-id="c6596-413">W takim przypadku używany jest podstawowy obraz systemu Windows Server Core (ustawienie od) i Instalowanie usług IIS za pomocą polecenia programu PowerShell (ustawienie URUCHOMIENIOWe).</span><span class="sxs-lookup"><span data-stu-id="c6596-413">In this case, we are using a Windows Server Core base image (the FROM setting) and installing IIS with a PowerShell command (the RUN setting).</span></span> <span data-ttu-id="c6596-414">W podobny sposób można również użyć poleceń programu PowerShell, aby skonfigurować dodatkowe składniki, takie jak ASP.NET 4. x, .NET 4,6 lub dowolne inne oprogramowanie systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="c6596-414">In a similar way, you could also use PowerShell commands to set up additional components like ASP.NET 4.x, .NET 4.6, or any other Windows software.</span></span> <span data-ttu-id="c6596-415">Na przykład następujące polecenie w pliku dockerfile konfiguruje ASP.NET 4,5:</span><span class="sxs-lookup"><span data-stu-id="c6596-415">For example, the following command in a Dockerfile sets up ASP.NET 4.5:</span></span>

```Dockerfile
RUN powershell add-windowsfeature web-asp-net45
```

### <a name="additional-resources"></a><span data-ttu-id="c6596-416">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="c6596-416">Additional resources</span></span>

- <span data-ttu-id="c6596-417">**aspnet-docker/Dockerfile.**</span><span class="sxs-lookup"><span data-stu-id="c6596-417">**aspnet-docker/Dockerfile.**</span></span> <span data-ttu-id="c6596-418">Przykładowe polecenia programu PowerShell do uruchomienia z wieloetapowe dockerfile w celu uwzględnienia funkcji systemu Windows. </span><span class="sxs-lookup"><span data-stu-id="c6596-418">Example PowerShell commands to run from dockerfiles to include Windows features.</span></span>\
  <https://github.com/Microsoft/aspnet-docker/blob/master/4.7.1-windowsservercore-ltsc2016/runtime/Dockerfile>

>[!div class="step-by-step"]
><span data-ttu-id="c6596-419">[Poprzedni](index.md)Następny
>[](../multi-container-microservice-net-applications/index.md)</span><span class="sxs-lookup"><span data-stu-id="c6596-419">[Previous](index.md)
[Next](../multi-container-microservice-net-applications/index.md)</span></span>