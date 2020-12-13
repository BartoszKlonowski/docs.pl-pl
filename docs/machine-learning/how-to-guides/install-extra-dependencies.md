---
title: Instalowanie dodatkowych zależności ML.NET
description: Dowiedz się, jak zainstalować wszystkie biblioteki natywne, od których są zależne pakiety ML.NET, ale nie są instalowane z pakietami NuGet
ms.date: 04/02/2020
author: natke
ms.author: nakersha
ms.custom: how-to
ms.openlocfilehash: 75d29c6bafdce5c9bb104229ddc8d7b847f57e29
ms.sourcegitcommit: fcbe432482464b1639decad78cc4dc8387c6269e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/12/2020
ms.locfileid: "97366802"
---
# <a name="install-extra-mlnet-dependencies"></a><span data-ttu-id="af5df-103">Instalowanie dodatkowych zależności ML.NET</span><span class="sxs-lookup"><span data-stu-id="af5df-103">Install extra ML.NET dependencies</span></span>

<span data-ttu-id="af5df-104">W większości przypadków w przypadku wszystkich systemów operacyjnych Instalowanie ML.NET jest proste, ponieważ odwołuje się do odpowiedniego pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="af5df-104">In most cases, on all operating systems, installing ML.NET is as simple as referencing the appropriate NuGet package.</span></span>

```dotnetcli
dotnet add package Microsoft.ML
```

<span data-ttu-id="af5df-105">W niektórych przypadkach istnieją dodatkowe wymagania dotyczące instalacji, zwłaszcza w przypadku, gdy wymagane są składniki natywne.</span><span class="sxs-lookup"><span data-stu-id="af5df-105">In some cases though, there are additional installation requirements, particularly when native components are required.</span></span> <span data-ttu-id="af5df-106">W tym dokumencie opisano wymagania dotyczące instalacji tych przypadków.</span><span class="sxs-lookup"><span data-stu-id="af5df-106">This document describes the installation requirements for those cases.</span></span> <span data-ttu-id="af5df-107">Sekcje są podzielone według określonego `Microsoft.ML.*` pakietu NuGet, który ma dodatkową zależność.</span><span class="sxs-lookup"><span data-stu-id="af5df-107">The sections are broken down by the specific `Microsoft.ML.*` NuGet package that has the additional dependency.</span></span>

## <a name="microsoftmltimeseries-microsoftmlautoml"></a><span data-ttu-id="af5df-108">Microsoft. ML. szeregów czasowych, Microsoft. ML. AutoML</span><span class="sxs-lookup"><span data-stu-id="af5df-108">Microsoft.ML.TimeSeries, Microsoft.ML.AutoML</span></span>

<span data-ttu-id="af5df-109">Oba te pakiety mają zależność od `Microsoft.ML.MKL.Redist` , która ma zależność od `libomp` .</span><span class="sxs-lookup"><span data-stu-id="af5df-109">Both of these packages have a dependency on `Microsoft.ML.MKL.Redist`, which has a dependency on `libomp`.</span></span>

### <a name="windows"></a><span data-ttu-id="af5df-110">Windows</span><span class="sxs-lookup"><span data-stu-id="af5df-110">Windows</span></span>

<span data-ttu-id="af5df-111">Nie są wymagane żadne dodatkowe kroki instalacji.</span><span class="sxs-lookup"><span data-stu-id="af5df-111">No extra installation steps required.</span></span> <span data-ttu-id="af5df-112">Biblioteka jest instalowana, gdy pakiet NuGet zostanie dodany do projektu.</span><span class="sxs-lookup"><span data-stu-id="af5df-112">The library is installed when the NuGet package is added to the project.</span></span>

### <a name="linux"></a><span data-ttu-id="af5df-113">Linux</span><span class="sxs-lookup"><span data-stu-id="af5df-113">Linux</span></span>

1. <span data-ttu-id="af5df-114">Instalowanie klucza GPG dla repozytorium</span><span class="sxs-lookup"><span data-stu-id="af5df-114">Install the GPG key for the repository</span></span>

    ```bash
    sudo bash
    # <type your user password when prompted.  this will put you in a root shell>
    # cd to /tmp where this shell has write permission
    cd /tmp
    # now get the key:
    wget https://apt.repos.intel.com/intel-gpg-keys/GPG-PUB-KEY-INTEL-SW-PRODUCTS-2019.PUB
    # now install that key
    apt-key add GPG-PUB-KEY-INTEL-SW-PRODUCTS-2019.PUB
    # now remove the public key file exit the root shell
    rm GPG-PUB-KEY-INTEL-SW-PRODUCTS-2019.PUB
    exit
    ```

2. <span data-ttu-id="af5df-115">Dodawanie repozytorium APT dla MKL</span><span class="sxs-lookup"><span data-stu-id="af5df-115">Add the APT Repository for MKL</span></span>

    ```bash
    sudo sh -c 'echo deb https://apt.repos.intel.com/mkl all main > /etc/apt/sources.list.d/intel-mkl.list'
    ```

3. <span data-ttu-id="af5df-116">Pakiety aktualizacji</span><span class="sxs-lookup"><span data-stu-id="af5df-116">Update packages</span></span>

    ```bash
    sudo apt-get update
    ```

4. <span data-ttu-id="af5df-117">Zainstaluj MKL</span><span class="sxs-lookup"><span data-stu-id="af5df-117">Install MKL</span></span>

    ```bash
    sudo apt-get install <COMPONENT>-<VERSION>.<UPDATE>-<BUILD_NUMBER>
    ```

    <span data-ttu-id="af5df-118">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="af5df-118">For example:</span></span>

    ```bash
    sudo apt-get install intel-mkl-64bit-2020.0-088
    ```

    <span data-ttu-id="af5df-119">Określ lokalizację `libiomp.so`</span><span class="sxs-lookup"><span data-stu-id="af5df-119">Determine the location of `libiomp.so`</span></span>

    ```bash
    find /opt -name "libiomp5.so"
    ```

    <span data-ttu-id="af5df-120">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="af5df-120">For example:</span></span>

    ```output
    /opt/intel/compilers_and_libraries_2020.0.166/linux/compiler/lib/intel64_lin/libiomp5.so
    ```

5. <span data-ttu-id="af5df-121">Dodaj tę lokalizację do ścieżki biblioteki ładowania:</span><span class="sxs-lookup"><span data-stu-id="af5df-121">Add this location to the load library path:</span></span>

    ```bash
    sudo ldconfig /opt/intel/compilers_and_libraries_2020.0.166/linux/compiler/lib/intel64_lin
    ```

### <a name="mac"></a><span data-ttu-id="af5df-122">Mac</span><span class="sxs-lookup"><span data-stu-id="af5df-122">Mac</span></span>

1. <span data-ttu-id="af5df-123">Zainstaluj bibliotekę z `Homebrew`</span><span class="sxs-lookup"><span data-stu-id="af5df-123">Install the library with `Homebrew`</span></span>

    ```bash
    brew update && brew install https://raw.githubusercontent.com/Homebrew/homebrew-core/f5b1ac99a7fba27c19cee0bc4f036775c889b359/Formula/libomp.rb && brew link libomp --force
    ```
