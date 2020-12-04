---
title: Debuguj aplikacje .NET na Raspberry Pi
description: Dowiedz się, jak debugować aplikacje .NET na Raspberry Pi i podobnych urządzeniach.
author: camsoper
ms.author: casoper
ms.date: 11/13/2020
ms.topic: how-to
ms.prod: dotnet
zone_pivot_groups: ide-set-one
ms.openlocfilehash: 7b9872304ee53071452772e3da02081a7def4d80
ms.sourcegitcommit: b201d177e01480a139622f3bf8facd367657a472
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/15/2020
ms.locfileid: "96589975"
---
# <a name="debug-net-apps-on-raspberry-pi"></a>Debuguj aplikacje .NET na Raspberry Pi

Debugowanie aplikacji .NET działających na urządzeniach IoT opartych na architekturze ARM, takich jak Raspberry Pi, stanowi unikatowe wyzwanie. Istnieje możliwość tworzenia aplikacji .NET na urządzeniach ARM. Jednak OmniSharp, który jest wymagany do debugowania aplikacji .NET poza programem Visual Studio, nie jest zgodny z urządzeniami ARM. W związku z tym aplikacje muszą być debugowane zdalnie z poziomu zgodnej platformy.

::: zone pivot="vscode"

## <a name="debug-from-visual-studio-code-cross-platform"></a>Debugowanie z Visual Studio Code (wiele platform)

Debugowanie programu .NET na Raspberry Pi z Visual Studio Code wymaga wykonania czynności konfiguracyjnych w Raspberry Pi i w *launch.js* projektu w pliku.

### <a name="enable-ssh-on-the-raspberry-pi"></a>Włącz protokół SSH na Raspberry Pi

Do zdalnego debugowania jest wymagany protokół SSH. Aby włączyć protokół SSH, [zapoznaj się z tematem *Włączanie protokołu SSH* w dokumentacji Raspberry Pi](https://www.raspberrypi.org/documentation/remote-access/ssh/) <span class="docon docon-navigate-external x-hidden-focus"></span> .

### <a name="install-the-visual-studio-remote-debugger-on-the-raspberry-pi"></a>Zainstaluj zdalny debuger programu Visual Studio na Raspberry Pi

W konsoli programu bash na Raspberry Pi (lokalnie lub za pośrednictwem protokołu SSH) wykonaj następujące czynności:

1. Wykonaj następujące polecenie, aby pobrać i zainstalować zdalny debuger programu Visual Studio na Raspberry Pi:

    ```bash
    curl -sSL https://aka.ms/getvsdbgsh | /bin/sh /dev/stdin -v latest -l ~/vsdbg
    ```

1. Debuger wymaga uruchomienia jako `root` . Domyślnie `root` nie ma hasła na Raspberry Pi. Ustaw hasło dla programu `root` , wykonując następujące polecenie i postępując zgodnie z instrukcjami.

    ```bash
    sudo passwd root
    ```

1. Visual Studio Code używa protokołu SSH do zdalnego debugowania. Ze względów bezpieczeństwa `root` nie jest dozwolone logowanie za pośrednictwem protokołu SSH. Aby włączyć `root` Logowanie za pośrednictwem protokołu SSH, wykonaj następujące czynności:

    1. Wykonaj następujące polecenie, aby otworzyć */etc/ssh/sshd_config* w [nano](https://www.nano-editor.org/docs.php) <span class="docon docon-navigate-external x-hidden-focus"></span> .

        ```bash
        sudo nano /etc/ssh/sshd_config
        ```

    1. Naciśnij <kbd>klawisze Ctrl + W</kbd> i wyszukaj ciąg **PermitRootLogin**.
    1. W razie konieczności Usuń komentarz z wiersza z **PermitRootLogin** .
    1. Zmień wiersz w następujący sposób:

        ```console
        PermitRootLogin yes
        ```

        > [!NOTE]
        > Jeśli nie ma wiersza **PermitRootLogin** w */etc/ssh/sshd_config*, Dodaj nowy wiersz o wartości podanej powyżej.

    1. Naciśnij <kbd>kombinację klawiszy Ctrl + X</kbd> , aby wyjść i zaoszczędzić szansę. Po wyświetleniu monitu **Zapisz zmodyfikowany bufor?** naciśnij klawisz <kbd>Y</kbd> , aby potwierdzić. Naciśnij klawisz <kbd>Enter</kbd> , aby potwierdzić zastąpienie oryginalnego pliku.
    1. Uruchom ponownie Raspberry Pi, wykonując następujące polecenie:

        ```bash
        sudo reboot
        ```

### <a name="setup-launchjson-in-visual-studio-code"></a>launch.jsInstalatora w programie na platformie programu Visual Studio Code

Dodaj konfigurację uruchamiania do *launch.jsprojektu w*. Jeśli projekt nie ma *launch.jsw* pliku, Dodaj go, przełączając się na kartę **Run** , wybierając pozycję **Utwórz launch.jsna pliku**, a następnie wybierając pozycję **.NET** lub **.NET Core** w oknie dialogowym.

Nowa konfiguracja w *launch.js* powinna wyglądać podobnie do tego:

```json
"configurations": [
    {
        "name": ".NET Core Launch (remote console)",
        "type": "coreclr",
        "request": "launch",
        "preLaunchTask": "build",
        "program": "/home/pi/.dotnet/dotnet",
        "args": ["/home/pi/sample/Sample.dll"],
        "cwd": "/home/pi/sample",
        "stopAtEntry": false,
        "console": "internalConsole",
        "pipeTransport": {
            "pipeCwd": "${workspaceFolder}",
            "pipeProgram": "C:\\Program Files\\PuTTY\\PLINK.EXE",
            "pipeArgs": [
                "-pw",
                "P@ssw0rd",
                "root@raspberrypi"
            ],
            "debuggerPath": "/home/pi/vsdbg/vsdbg"
        }
    },
```

Zapamiętaj poniższe:

- `program` jest ścieżką do środowiska uruchomieniowego .NET na pi.
- `args` jest ścieżką do zestawu do debugowania na pi.
- `cwd` jest katalogiem roboczym, który ma być używany podczas uruchamiania aplikacji na pi.
- `pipeProgram` jest ścieżką do klienta SSH na komputerze lokalnym.
- `pipeArgs` parametry, które mają zostać przesłane do klienta SSH. Pamiętaj, aby określić parametr password, a także `root` użytkownika w formacie `<user>@<hostname>` .

> [!IMPORTANT]
> Powyższy przykład używa *Plink*, składnika [PuTTY](https://www.ssh.com/ssh/putty/) <span class="docon docon-navigate-external x-hidden-focus"></span> klienta SSH. [OpenSSH](https://www.openssh.com/) <span class="docon docon-navigate-external x-hidden-focus"></span> , który znajduje się w ostatnich wersjach systemów Windows i Linux, może być używany w zamian. Jednak OpenSSH nie obsługuje wysyłania haseł jako parametru wiersza polecenia. Aby użyć OpenSSH, [Skonfiguruj Raspberry Pi dla dostępu SSH bezhasłem](https://www.raspberrypi.org/documentation/remote-access/ssh/passwordless.md) <span class="docon docon-navigate-external x-hidden-focus"></span> .

### <a name="deploy-the-app"></a>Wdrażanie aplikacji

Wdróż aplikację zgodnie z opisem w artykule [wdrażanie aplikacji .NET do Raspberry Pi](deployment.md). Upewnij się, że ścieżka wdrożenia jest taka sama jak ścieżka określona w `cwd` parametrze w *launch.js* w konfiguracji.

### <a name="launch-the-debugger"></a>Uruchom debuger

Na karcie **przebieg** wybierz konfigurację **uruchamiania programu .NET Core (Konsola zdalna)** i wybierz pozycję **Rozpocznij debugowanie**. Aplikacja zostanie uruchomiona na Raspberry Pi. Debuger może służyć do ustawiania punktów przerwania, przeprowadzania inspekcji lokalnych i nie tylko.

## <a name="references"></a>Odwołania

[Zdalne debugowanie z vs Code w systemie Windows do Raspberry Pi przy użyciu platformy .NET Core na platformie ARM](https://www.hanselman.com/blog/remote-debugging-with-vs-code-on-windows-to-a-raspberry-pi-using-net-core-on-arm)<span class="docon docon-navigate-external x-hidden-focus"></span>

::: zone-end

::: zone pivot="visualstudio"

## <a name="debug-from-visual-studio-on-windows"></a>Debuguj z programu Visual Studio w systemie Windows

Program Visual Studio może debugować aplikacje .NET na urządzeniach zdalnych za pośrednictwem protokołu SSH. Na urządzeniu nie jest wymagana specjalna konfiguracja. Aby uzyskać szczegółowe informacje na temat używania programu Visual Studio do zdalnego debugowania programu .NET, zobacz [zdalne debugowanie .NET w systemie Linux przy użyciu protokołu SSH](/visualstudio/debugger/remote-debugging-dotnet-core-linux-with-ssh?view=vs-2019).

::: zone-end
