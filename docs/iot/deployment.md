---
title: Wdrażanie aplikacji .NET do Raspberry Pi
description: Dowiedz się, jak wdrażać aplikacje .NET do Raspberry Pi.
author: camsoper
ms.author: casoper
ms.date: 11/13/2020
ms.topic: how-to
ms.prod: dotnet
ms.openlocfilehash: 4da558e2cdfc283d21f2a5497cb71dc746109614
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96590048"
---
# <a name="deploy-net-apps-to-raspberry-pi"></a><span data-ttu-id="ce1b9-103">Wdrażanie aplikacji .NET do Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="ce1b9-103">Deploy .NET apps to Raspberry Pi</span></span>

<span data-ttu-id="ce1b9-104">Wdrażanie aplikacji .NET do Raspberry Pi jest takie samo jak w przypadku dowolnej innej platformy.</span><span class="sxs-lookup"><span data-stu-id="ce1b9-104">Deployment of .NET apps to Raspberry Pi is identical to that of any other platform.</span></span> <span data-ttu-id="ce1b9-105">Aplikacja może działać jako tryby wdrażania *samodzielnego* lub *zależnego od platformy* .</span><span class="sxs-lookup"><span data-stu-id="ce1b9-105">Your app can run as *self-contained* or *framework-dependent* deployment modes.</span></span> <span data-ttu-id="ce1b9-106">Istnieją zalety każdej strategii.</span><span class="sxs-lookup"><span data-stu-id="ce1b9-106">There are advantages to each strategy.</span></span> <span data-ttu-id="ce1b9-107">Aby uzyskać więcej informacji, zobacz [Omówienie publikowania aplikacji .NET](../core/deploying/index.md).</span><span class="sxs-lookup"><span data-stu-id="ce1b9-107">For more information, see [.NET application publishing overview](../core/deploying/index.md).</span></span>

## <a name="deploying-a-framework-dependent-app"></a><span data-ttu-id="ce1b9-108">Wdrażanie aplikacji zależnej od platformy</span><span class="sxs-lookup"><span data-stu-id="ce1b9-108">Deploying a framework-dependent app</span></span>

<span data-ttu-id="ce1b9-109">Aby wdrożyć aplikację jako aplikację zależną od platformy, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ce1b9-109">To deploy your app as a framework-dependent app, complete the following steps:</span></span>

1. [!INCLUDE [ensure-ssh](includes/ensure-ssh.md)]

1. <span data-ttu-id="ce1b9-110">Zainstaluj platformę .NET na Raspberry Pi przy użyciu [skryptów dotnet-Install](../core/tools/dotnet-install-script.md).</span><span class="sxs-lookup"><span data-stu-id="ce1b9-110">Install .NET on the Raspberry Pi using the [dotnet-install scripts](../core/tools/dotnet-install-script.md).</span></span> <span data-ttu-id="ce1b9-111">Wykonaj następujące kroki w wierszu polecenia bash na Raspberry Pi (Local lub SSH):</span><span class="sxs-lookup"><span data-stu-id="ce1b9-111">Complete the following steps from a Bash prompt on the Raspberry Pi (local or SSH):</span></span>
    1. <span data-ttu-id="ce1b9-112">Uruchom następujące polecenie, aby zainstalować program .NET:</span><span class="sxs-lookup"><span data-stu-id="ce1b9-112">Run the following command to install .NET:</span></span>

        ```bash
        curl -sSL https://dot.net/v1/dotnet-install.sh | bash /dev/stdin
        ```

        > [!NOTE]
        > <span data-ttu-id="ce1b9-113">Spowoduje to zainstalowanie najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="ce1b9-113">This installs the latest version.</span></span> <span data-ttu-id="ce1b9-114">Jeśli potrzebujesz określonej wersji, Dodaj `--version <VERSION>` do końca, gdzie `<VERSION>` jest określona wersja kompilacji.</span><span class="sxs-lookup"><span data-stu-id="ce1b9-114">If you need a specific version, add `--version <VERSION>` to the end, where `<VERSION>` is the specific build version.</span></span>

    1. <span data-ttu-id="ce1b9-115">Aby uprościć rozpoznawanie ścieżki, Dodaj `DOTNET_ROOT` zmienną środowiskową i Dodaj katalog *. dotnet* do `$PATH` następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="ce1b9-115">To simplify path resolution, add a `DOTNET_ROOT` environment variable and add the *.dotnet* directory to `$PATH` with the following commands:</span></span>

        ```bash
        echo 'export DOTNET_ROOT=$HOME/.dotnet' >> ~/.bashrc
        echo 'export PATH=$PATH:$HOME/.dotnet' >> ~/.bashrc
        source ~/.bashrc
        ```

    1. <span data-ttu-id="ce1b9-116">Sprawdź instalację platformy .NET przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="ce1b9-116">Verify the .NET installation with the following command:</span></span>

        ```dotnetcli
        dotnet --version
        ```

        <span data-ttu-id="ce1b9-117">Sprawdź, czy wyświetlana wersja jest zgodna z zainstalowaną wersją.</span><span class="sxs-lookup"><span data-stu-id="ce1b9-117">Verify the displayed version matches the version you installed.</span></span>

1. <span data-ttu-id="ce1b9-118">Opublikuj aplikację na komputerze deweloperskim w następujący sposób, w zależności od środowiska deweloperskiego.</span><span class="sxs-lookup"><span data-stu-id="ce1b9-118">Publish the app on the development computer as follows, depending on development environment.</span></span>
    - <span data-ttu-id="ce1b9-119">Jeśli używasz **programu Visual Studio**, [Wdróż aplikację w folderze lokalnym](/visualstudio/deployment/quickstart-deploy-to-local-folder?view=vs-2019).</span><span class="sxs-lookup"><span data-stu-id="ce1b9-119">If using **Visual Studio**, [deploy the app to a local folder](/visualstudio/deployment/quickstart-deploy-to-local-folder?view=vs-2019).</span></span> <span data-ttu-id="ce1b9-120">Przed opublikowaniem wybierz pozycję **Edytuj** w podsumowaniu profilu publikowania i wybierz kartę **Ustawienia** . Upewnij się, że **Tryb wdrożenia** jest ustawiony na wartość *zależny od platformy* , a **docelowy środowisko uruchomieniowe** jest ustawione na *przenośne*.</span><span class="sxs-lookup"><span data-stu-id="ce1b9-120">Before publishing, select **Edit** in the publish profile summary and select the **Settings** tab. Ensure that **Deployment mode** is set to *Framework-dependent* and **Target runtime** is set to *Portable*.</span></span>
    - <span data-ttu-id="ce1b9-121">Jeśli używasz **interfejsu wiersza polecenia platformy .NET**, użyj [dotnet Publish](../core/tools/dotnet-publish.md) polecenie.</span><span class="sxs-lookup"><span data-stu-id="ce1b9-121">If using the **.NET CLI**, use the [dotnet publish](../core/tools/dotnet-publish.md) command.</span></span> <span data-ttu-id="ce1b9-122">Nie są wymagane żadne dodatkowe argumenty.</span><span class="sxs-lookup"><span data-stu-id="ce1b9-122">No additional arguments are required.</span></span>

1. [!INCLUDE [sftp-client](includes/sftp-client.md)]

1. <span data-ttu-id="ce1b9-123">Z poziomu monitu bash na Raspberry Pi (lokalnego lub SSH) Uruchom aplikację.</span><span class="sxs-lookup"><span data-stu-id="ce1b9-123">From a Bash prompt on the Raspberry Pi (local or SSH), run the app.</span></span> <span data-ttu-id="ce1b9-124">W tym celu należy ustawić folder wdrożenia jako bieżący katalog i wykonać następujące polecenie (gdzie *HelloWorld.dll* jest punktem wejścia aplikacji):</span><span class="sxs-lookup"><span data-stu-id="ce1b9-124">To do this, set the deployment folder as the current directory and execute the following command (where *HelloWorld.dll* is the entry point of the app):</span></span>

    ```dotnetcli
    dotnet HelloWorld.dll
    ```

## <a name="deploying-a-self-contained-app"></a><span data-ttu-id="ce1b9-125">Wdrażanie aplikacji samodzielnej</span><span class="sxs-lookup"><span data-stu-id="ce1b9-125">Deploying a self-contained app</span></span>

<span data-ttu-id="ce1b9-126">Aby wdrożyć aplikację jako samodzielną aplikację, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ce1b9-126">To deploy your app as a self-contained app, complete the following steps:</span></span>

1. [!INCLUDE [ensure-ssh](includes/ensure-ssh.md)]

1. <span data-ttu-id="ce1b9-127">Opublikuj aplikację na komputerze deweloperskim w następujący sposób, w zależności od środowiska deweloperskiego.</span><span class="sxs-lookup"><span data-stu-id="ce1b9-127">Publish the app on the development computer as follows, depending on development environment.</span></span>
    - <span data-ttu-id="ce1b9-128">Jeśli używasz **programu Visual Studio**, [Wdróż aplikację w folderze lokalnym](/visualstudio/deployment/quickstart-deploy-to-local-folder?view=vs-2019).</span><span class="sxs-lookup"><span data-stu-id="ce1b9-128">If using **Visual Studio**, [deploy the app to a local folder](/visualstudio/deployment/quickstart-deploy-to-local-folder?view=vs-2019).</span></span> <span data-ttu-id="ce1b9-129">Przed opublikowaniem wybierz pozycję **Edytuj** w podsumowaniu profilu publikowania i wybierz kartę **Ustawienia** . Upewnij się, że **Tryb wdrożenia** jest ustawiony na *własny* i **docelowy środowisko uruchomieniowe** ma ustawioną wartość *Linux-ARM*.</span><span class="sxs-lookup"><span data-stu-id="ce1b9-129">Before publishing, select **Edit** in the publish profile summary and select the **Settings** tab. Ensure that **Deployment mode** is set to *Self-contained* and **Target runtime** is set to *linux-arm*.</span></span>
    - <span data-ttu-id="ce1b9-130">Jeśli używasz **interfejsu wiersza polecenia platformy .NET**, użyj [dotnet Publish](../core/tools/dotnet-publish.md) polecenie z `-r linux-arm` argumentem:</span><span class="sxs-lookup"><span data-stu-id="ce1b9-130">If using the **.NET CLI**, use the [dotnet publish](../core/tools/dotnet-publish.md) command with the `-r linux-arm` argument:</span></span>

        ```dotnetcli
        dotnet publish -r linux-arm
        ```

1. [!INCLUDE [sftp-client](includes/sftp-client.md)]

1. <span data-ttu-id="ce1b9-131">Z poziomu monitu bash na Raspberry Pi (lokalnego lub SSH) Uruchom aplikację.</span><span class="sxs-lookup"><span data-stu-id="ce1b9-131">From a Bash prompt on the Raspberry Pi (local or SSH), run the app.</span></span> <span data-ttu-id="ce1b9-132">W tym celu ustaw bieżący katalog na lokalizację wdrożenia i wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ce1b9-132">To do this, set the current directory to the deployment location and complete the following steps:</span></span>
    1. <span data-ttu-id="ce1b9-133">Nadaj plikowi wykonywalnemu uprawnienia *Execute* (gdzie `HelloWorld` jest nazwą pliku wykonywalnego).</span><span class="sxs-lookup"><span data-stu-id="ce1b9-133">Give the executable *execute* permission (where `HelloWorld` is the executable file name).</span></span>

        ```bash
        chmod +x HelloWorld
        ```

    1. <span data-ttu-id="ce1b9-134">Uruchom plik wykonywalny.</span><span class="sxs-lookup"><span data-stu-id="ce1b9-134">Run the executable.</span></span>

        ```bash
        ./HelloWorld
        ```
