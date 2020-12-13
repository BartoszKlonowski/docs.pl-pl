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
# <a name="install-extra-mlnet-dependencies"></a>Instalowanie dodatkowych zależności ML.NET

W większości przypadków w przypadku wszystkich systemów operacyjnych Instalowanie ML.NET jest proste, ponieważ odwołuje się do odpowiedniego pakietu NuGet.

```dotnetcli
dotnet add package Microsoft.ML
```

W niektórych przypadkach istnieją dodatkowe wymagania dotyczące instalacji, zwłaszcza w przypadku, gdy wymagane są składniki natywne. W tym dokumencie opisano wymagania dotyczące instalacji tych przypadków. Sekcje są podzielone według określonego `Microsoft.ML.*` pakietu NuGet, który ma dodatkową zależność.

## <a name="microsoftmltimeseries-microsoftmlautoml"></a>Microsoft. ML. szeregów czasowych, Microsoft. ML. AutoML

Oba te pakiety mają zależność od `Microsoft.ML.MKL.Redist` , która ma zależność od `libomp` .

### <a name="windows"></a>Windows

Nie są wymagane żadne dodatkowe kroki instalacji. Biblioteka jest instalowana, gdy pakiet NuGet zostanie dodany do projektu.

### <a name="linux"></a>Linux

1. Instalowanie klucza GPG dla repozytorium

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

2. Dodawanie repozytorium APT dla MKL

    ```bash
    sudo sh -c 'echo deb https://apt.repos.intel.com/mkl all main > /etc/apt/sources.list.d/intel-mkl.list'
    ```

3. Pakiety aktualizacji

    ```bash
    sudo apt-get update
    ```

4. Zainstaluj MKL

    ```bash
    sudo apt-get install <COMPONENT>-<VERSION>.<UPDATE>-<BUILD_NUMBER>
    ```

    Na przykład:

    ```bash
    sudo apt-get install intel-mkl-64bit-2020.0-088
    ```

    Określ lokalizację `libiomp.so`

    ```bash
    find /opt -name "libiomp5.so"
    ```

    Na przykład:

    ```output
    /opt/intel/compilers_and_libraries_2020.0.166/linux/compiler/lib/intel64_lin/libiomp5.so
    ```

5. Dodaj tę lokalizację do ścieżki biblioteki ładowania:

    ```bash
    sudo ldconfig /opt/intel/compilers_and_libraries_2020.0.166/linux/compiler/lib/intel64_lin
    ```

### <a name="mac"></a>Mac

1. Zainstaluj bibliotekę z `Homebrew`

    ```bash
    brew update && brew install https://raw.githubusercontent.com/Homebrew/homebrew-core/f5b1ac99a7fba27c19cee0bc4f036775c889b359/Formula/libomp.rb && brew link libomp --force
    ```
