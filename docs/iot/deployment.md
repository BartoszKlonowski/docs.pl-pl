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
# <a name="deploy-net-apps-to-raspberry-pi"></a>Wdrażanie aplikacji .NET do Raspberry Pi

Wdrażanie aplikacji .NET do Raspberry Pi jest takie samo jak w przypadku dowolnej innej platformy. Aplikacja może działać jako tryby wdrażania *samodzielnego* lub *zależnego od platformy* . Istnieją zalety każdej strategii. Aby uzyskać więcej informacji, zobacz [Omówienie publikowania aplikacji .NET](../core/deploying/index.md).

## <a name="deploying-a-framework-dependent-app"></a>Wdrażanie aplikacji zależnej od platformy

Aby wdrożyć aplikację jako aplikację zależną od platformy, wykonaj następujące czynności:

1. [!INCLUDE [ensure-ssh](includes/ensure-ssh.md)]

1. Zainstaluj platformę .NET na Raspberry Pi przy użyciu [skryptów dotnet-Install](../core/tools/dotnet-install-script.md). Wykonaj następujące kroki w wierszu polecenia bash na Raspberry Pi (Local lub SSH):
    1. Uruchom następujące polecenie, aby zainstalować program .NET:

        ```bash
        curl -sSL https://dot.net/v1/dotnet-install.sh | bash /dev/stdin
        ```

        > [!NOTE]
        > Spowoduje to zainstalowanie najnowszej wersji. Jeśli potrzebujesz określonej wersji, Dodaj `--version <VERSION>` do końca, gdzie `<VERSION>` jest określona wersja kompilacji.

    1. Aby uprościć rozpoznawanie ścieżki, Dodaj `DOTNET_ROOT` zmienną środowiskową i Dodaj katalog *. dotnet* do `$PATH` następujących poleceń:

        ```bash
        echo 'export DOTNET_ROOT=$HOME/.dotnet' >> ~/.bashrc
        echo 'export PATH=$PATH:$HOME/.dotnet' >> ~/.bashrc
        source ~/.bashrc
        ```

    1. Sprawdź instalację platformy .NET przy użyciu następującego polecenia:

        ```dotnetcli
        dotnet --version
        ```

        Sprawdź, czy wyświetlana wersja jest zgodna z zainstalowaną wersją.

1. Opublikuj aplikację na komputerze deweloperskim w następujący sposób, w zależności od środowiska deweloperskiego.
    - Jeśli używasz **programu Visual Studio**, [Wdróż aplikację w folderze lokalnym](/visualstudio/deployment/quickstart-deploy-to-local-folder?view=vs-2019). Przed opublikowaniem wybierz pozycję **Edytuj** w podsumowaniu profilu publikowania i wybierz kartę **Ustawienia** . Upewnij się, że **Tryb wdrożenia** jest ustawiony na wartość *zależny od platformy* , a **docelowy środowisko uruchomieniowe** jest ustawione na *przenośne*.
    - Jeśli używasz **interfejsu wiersza polecenia platformy .NET**, użyj [dotnet Publish](../core/tools/dotnet-publish.md) polecenie. Nie są wymagane żadne dodatkowe argumenty.

1. [!INCLUDE [sftp-client](includes/sftp-client.md)]

1. Z poziomu monitu bash na Raspberry Pi (lokalnego lub SSH) Uruchom aplikację. W tym celu należy ustawić folder wdrożenia jako bieżący katalog i wykonać następujące polecenie (gdzie *HelloWorld.dll* jest punktem wejścia aplikacji):

    ```dotnetcli
    dotnet HelloWorld.dll
    ```

## <a name="deploying-a-self-contained-app"></a>Wdrażanie aplikacji samodzielnej

Aby wdrożyć aplikację jako samodzielną aplikację, wykonaj następujące czynności:

1. [!INCLUDE [ensure-ssh](includes/ensure-ssh.md)]

1. Opublikuj aplikację na komputerze deweloperskim w następujący sposób, w zależności od środowiska deweloperskiego.
    - Jeśli używasz **programu Visual Studio**, [Wdróż aplikację w folderze lokalnym](/visualstudio/deployment/quickstart-deploy-to-local-folder?view=vs-2019). Przed opublikowaniem wybierz pozycję **Edytuj** w podsumowaniu profilu publikowania i wybierz kartę **Ustawienia** . Upewnij się, że **Tryb wdrożenia** jest ustawiony na *własny* i **docelowy środowisko uruchomieniowe** ma ustawioną wartość *Linux-ARM*.
    - Jeśli używasz **interfejsu wiersza polecenia platformy .NET**, użyj [dotnet Publish](../core/tools/dotnet-publish.md) polecenie z `-r linux-arm` argumentem:

        ```dotnetcli
        dotnet publish -r linux-arm
        ```

1. [!INCLUDE [sftp-client](includes/sftp-client.md)]

1. Z poziomu monitu bash na Raspberry Pi (lokalnego lub SSH) Uruchom aplikację. W tym celu ustaw bieżący katalog na lokalizację wdrożenia i wykonaj następujące czynności:
    1. Nadaj plikowi wykonywalnemu uprawnienia *Execute* (gdzie `HelloWorld` jest nazwą pliku wykonywalnego).

        ```bash
        chmod +x HelloWorld
        ```

    1. Uruchom plik wykonywalny.

        ```bash
        ./HelloWorld
        ```
