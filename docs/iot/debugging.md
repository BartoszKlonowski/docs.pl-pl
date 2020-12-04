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
# <a name="debug-net-apps-on-raspberry-pi"></a><span data-ttu-id="2cdd9-103">Debuguj aplikacje .NET na Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="2cdd9-103">Debug .NET apps on Raspberry Pi</span></span>

<span data-ttu-id="2cdd9-104">Debugowanie aplikacji .NET działających na urządzeniach IoT opartych na architekturze ARM, takich jak Raspberry Pi, stanowi unikatowe wyzwanie.</span><span class="sxs-lookup"><span data-stu-id="2cdd9-104">Debugging .NET apps running on ARM-based IoT devices like Raspberry Pi presents a unique challenge.</span></span> <span data-ttu-id="2cdd9-105">Istnieje możliwość tworzenia aplikacji .NET na urządzeniach ARM.</span><span class="sxs-lookup"><span data-stu-id="2cdd9-105">It is possible to develop .NET apps on ARM devices.</span></span> <span data-ttu-id="2cdd9-106">Jednak OmniSharp, który jest wymagany do debugowania aplikacji .NET poza programem Visual Studio, nie jest zgodny z urządzeniami ARM.</span><span class="sxs-lookup"><span data-stu-id="2cdd9-106">However, OmniSharp, which is required for debugging .NET apps outside of Visual Studio, is not compatible with ARM devices.</span></span> <span data-ttu-id="2cdd9-107">W związku z tym aplikacje muszą być debugowane zdalnie z poziomu zgodnej platformy.</span><span class="sxs-lookup"><span data-stu-id="2cdd9-107">As a result, apps must be debugged remotely from a compatible platform.</span></span>

::: zone pivot="vscode"

## <a name="debug-from-visual-studio-code-cross-platform"></a><span data-ttu-id="2cdd9-108">Debugowanie z Visual Studio Code (wiele platform)</span><span class="sxs-lookup"><span data-stu-id="2cdd9-108">Debug from Visual Studio Code (cross-platform)</span></span>

<span data-ttu-id="2cdd9-109">Debugowanie programu .NET na Raspberry Pi z Visual Studio Code wymaga wykonania czynności konfiguracyjnych w Raspberry Pi i w *launch.js* projektu w pliku.</span><span class="sxs-lookup"><span data-stu-id="2cdd9-109">Debugging .NET on Raspberry Pi from Visual Studio Code requires configuration steps on the Raspberry Pi and in the project's *launch.json* file.</span></span>

### <a name="enable-ssh-on-the-raspberry-pi"></a><span data-ttu-id="2cdd9-110">Włącz protokół SSH na Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="2cdd9-110">Enable SSH on the Raspberry Pi</span></span>

<span data-ttu-id="2cdd9-111">Do zdalnego debugowania jest wymagany protokół SSH.</span><span class="sxs-lookup"><span data-stu-id="2cdd9-111">SSH is required for remote debugging.</span></span> <span data-ttu-id="2cdd9-112">Aby włączyć protokół SSH, [zapoznaj się z tematem *Włączanie protokołu SSH* w dokumentacji Raspberry Pi](https://www.raspberrypi.org/documentation/remote-access/ssh/) <span class="docon docon-navigate-external x-hidden-focus"></span> .</span><span class="sxs-lookup"><span data-stu-id="2cdd9-112">To enable SSH, [refer to *Enable SSH* in the Raspberry Pi documentation](https://www.raspberrypi.org/documentation/remote-access/ssh/) <span class="docon docon-navigate-external x-hidden-focus"></span>.</span></span>

### <a name="install-the-visual-studio-remote-debugger-on-the-raspberry-pi"></a><span data-ttu-id="2cdd9-113">Zainstaluj zdalny debuger programu Visual Studio na Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="2cdd9-113">Install the Visual Studio Remote Debugger on the Raspberry Pi</span></span>

<span data-ttu-id="2cdd9-114">W konsoli programu bash na Raspberry Pi (lokalnie lub za pośrednictwem protokołu SSH) wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="2cdd9-114">Within a Bash console on the Raspberry Pi (either locally or via SSH), complete the following steps:</span></span>

1. <span data-ttu-id="2cdd9-115">Wykonaj następujące polecenie, aby pobrać i zainstalować zdalny debuger programu Visual Studio na Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="2cdd9-115">Execute the following command to download and install the Visual Studio Remote Debugger on the Raspberry Pi:</span></span>

    ```bash
    curl -sSL https://aka.ms/getvsdbgsh | /bin/sh /dev/stdin -v latest -l ~/vsdbg
    ```

1. <span data-ttu-id="2cdd9-116">Debuger wymaga uruchomienia jako `root` .</span><span class="sxs-lookup"><span data-stu-id="2cdd9-116">The debugger requires running as `root`.</span></span> <span data-ttu-id="2cdd9-117">Domyślnie `root` nie ma hasła na Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="2cdd9-117">By default, `root` has no password on Raspberry Pi.</span></span> <span data-ttu-id="2cdd9-118">Ustaw hasło dla programu `root` , wykonując następujące polecenie i postępując zgodnie z instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="2cdd9-118">Set a password for `root` by executing the following command and following the prompts.</span></span>

    ```bash
    sudo passwd root
    ```

1. <span data-ttu-id="2cdd9-119">Visual Studio Code używa protokołu SSH do zdalnego debugowania.</span><span class="sxs-lookup"><span data-stu-id="2cdd9-119">Visual Studio Code uses the SSH protocol to debug remotely.</span></span> <span data-ttu-id="2cdd9-120">Ze względów bezpieczeństwa `root` nie jest dozwolone logowanie za pośrednictwem protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="2cdd9-120">For security purposes, `root` is not permitted to log on via SSH by default.</span></span> <span data-ttu-id="2cdd9-121">Aby włączyć `root` Logowanie za pośrednictwem protokołu SSH, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="2cdd9-121">To enable `root` to log on via SSH, complete the following steps:</span></span>

    1. <span data-ttu-id="2cdd9-122">Wykonaj następujące polecenie, aby otworzyć */etc/ssh/sshd_config* w [nano](https://www.nano-editor.org/docs.php) <span class="docon docon-navigate-external x-hidden-focus"></span> .</span><span class="sxs-lookup"><span data-stu-id="2cdd9-122">Execute the following command to open */etc/ssh/sshd_config* in [nano](https://www.nano-editor.org/docs.php) <span class="docon docon-navigate-external x-hidden-focus"></span>.</span></span>

        ```bash
        sudo nano /etc/ssh/sshd_config
        ```

    1. <span data-ttu-id="2cdd9-123">Naciśnij <kbd>klawisze Ctrl + W</kbd> i wyszukaj ciąg **PermitRootLogin**.</span><span class="sxs-lookup"><span data-stu-id="2cdd9-123">Press <kbd>Ctrl+W</kbd> and search for **PermitRootLogin**.</span></span>
    1. <span data-ttu-id="2cdd9-124">W razie konieczności Usuń komentarz z wiersza z **PermitRootLogin** .</span><span class="sxs-lookup"><span data-stu-id="2cdd9-124">Uncomment the line with **PermitRootLogin** if needed.</span></span>
    1. <span data-ttu-id="2cdd9-125">Zmień wiersz w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="2cdd9-125">Change the line to read as follows:</span></span>

        ```console
        PermitRootLogin yes
        ```

        > [!NOTE]
        > <span data-ttu-id="2cdd9-126">Jeśli nie ma wiersza **PermitRootLogin** w */etc/ssh/sshd_config*, Dodaj nowy wiersz o wartości podanej powyżej.</span><span class="sxs-lookup"><span data-stu-id="2cdd9-126">If there is no **PermitRootLogin** line in */etc/ssh/sshd_config*, add a new line with the value shown above.</span></span>

    1. <span data-ttu-id="2cdd9-127">Naciśnij <kbd>kombinację klawiszy Ctrl + X</kbd> , aby wyjść i zaoszczędzić szansę.</span><span class="sxs-lookup"><span data-stu-id="2cdd9-127">Press <kbd>Ctrl+X</kbd> to exit and save your chances.</span></span> <span data-ttu-id="2cdd9-128">Po wyświetleniu monitu **Zapisz zmodyfikowany bufor?** naciśnij klawisz <kbd>Y</kbd> , aby potwierdzić.</span><span class="sxs-lookup"><span data-stu-id="2cdd9-128">When prompted **Save modified buffer?**, press <kbd>Y</kbd> to confirm.</span></span> <span data-ttu-id="2cdd9-129">Naciśnij klawisz <kbd>Enter</kbd> , aby potwierdzić zastąpienie oryginalnego pliku.</span><span class="sxs-lookup"><span data-stu-id="2cdd9-129">Press <kbd>Enter</kbd> to confirm overwriting the original file.</span></span>
    1. <span data-ttu-id="2cdd9-130">Uruchom ponownie Raspberry Pi, wykonując następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="2cdd9-130">Reboot the Raspberry Pi by executing the following command:</span></span>

        ```bash
        sudo reboot
        ```

### <a name="setup-launchjson-in-visual-studio-code"></a><span data-ttu-id="2cdd9-131">launch.jsInstalatora w programie na platformie programu Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="2cdd9-131">Setup launch.json in Visual Studio Code</span></span>

<span data-ttu-id="2cdd9-132">Dodaj konfigurację uruchamiania do *launch.jsprojektu w*.</span><span class="sxs-lookup"><span data-stu-id="2cdd9-132">Add a launch configuration to the project's *launch.json*.</span></span> <span data-ttu-id="2cdd9-133">Jeśli projekt nie ma *launch.jsw* pliku, Dodaj go, przełączając się na kartę **Run** , wybierając pozycję **Utwórz launch.jsna pliku**, a następnie wybierając pozycję **.NET** lub **.NET Core** w oknie dialogowym.</span><span class="sxs-lookup"><span data-stu-id="2cdd9-133">If the project doesn't have a *launch.json* file, add one by switching to the **Run** tab, selecting **create a launch.json file**, and selecting **.NET** or **.NET Core** in the dialog.</span></span>

<span data-ttu-id="2cdd9-134">Nowa konfiguracja w *launch.js* powinna wyglądać podobnie do tego:</span><span class="sxs-lookup"><span data-stu-id="2cdd9-134">The new configuration in *launch.json* should look similar to this:</span></span>

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

<span data-ttu-id="2cdd9-135">Zapamiętaj poniższe:</span><span class="sxs-lookup"><span data-stu-id="2cdd9-135">Notice the following:</span></span>

- <span data-ttu-id="2cdd9-136">`program` jest ścieżką do środowiska uruchomieniowego .NET na pi.</span><span class="sxs-lookup"><span data-stu-id="2cdd9-136">`program` is the path to the .NET runtime on the Pi.</span></span>
- <span data-ttu-id="2cdd9-137">`args` jest ścieżką do zestawu do debugowania na pi.</span><span class="sxs-lookup"><span data-stu-id="2cdd9-137">`args` is the path to the assembly to debug on the Pi.</span></span>
- <span data-ttu-id="2cdd9-138">`cwd` jest katalogiem roboczym, który ma być używany podczas uruchamiania aplikacji na pi.</span><span class="sxs-lookup"><span data-stu-id="2cdd9-138">`cwd` is the working directory to use when launching the app on the Pi.</span></span>
- <span data-ttu-id="2cdd9-139">`pipeProgram` jest ścieżką do klienta SSH na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="2cdd9-139">`pipeProgram` is the path to an SSH client on the local machine.</span></span>
- <span data-ttu-id="2cdd9-140">`pipeArgs` parametry, które mają zostać przesłane do klienta SSH.</span><span class="sxs-lookup"><span data-stu-id="2cdd9-140">`pipeArgs` are the parameters to be passed to the SSH client.</span></span> <span data-ttu-id="2cdd9-141">Pamiętaj, aby określić parametr password, a także `root` użytkownika w formacie `<user>@<hostname>` .</span><span class="sxs-lookup"><span data-stu-id="2cdd9-141">Be sure to specify the password parameter, as well as the `root` user in the format `<user>@<hostname>`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2cdd9-142">Powyższy przykład używa *Plink*, składnika [PuTTY](https://www.ssh.com/ssh/putty/) <span class="docon docon-navigate-external x-hidden-focus"></span> klienta SSH.</span><span class="sxs-lookup"><span data-stu-id="2cdd9-142">The above example uses *plink*, a component of the [PuTTY](https://www.ssh.com/ssh/putty/)<span class="docon docon-navigate-external x-hidden-focus"></span> SSH client.</span></span> <span data-ttu-id="2cdd9-143">[OpenSSH](https://www.openssh.com/) <span class="docon docon-navigate-external x-hidden-focus"></span> , który znajduje się w ostatnich wersjach systemów Windows i Linux, może być używany w zamian.</span><span class="sxs-lookup"><span data-stu-id="2cdd9-143">[OpenSSH](https://www.openssh.com/)<span class="docon docon-navigate-external x-hidden-focus"></span>, which is included in recent versions of Windows and Linux, may be used instead.</span></span> <span data-ttu-id="2cdd9-144">Jednak OpenSSH nie obsługuje wysyłania haseł jako parametru wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="2cdd9-144">However, OpenSSH doesn't support sending passwords as a command-line parameter.</span></span> <span data-ttu-id="2cdd9-145">Aby użyć OpenSSH, [Skonfiguruj Raspberry Pi dla dostępu SSH bezhasłem](https://www.raspberrypi.org/documentation/remote-access/ssh/passwordless.md) <span class="docon docon-navigate-external x-hidden-focus"></span> .</span><span class="sxs-lookup"><span data-stu-id="2cdd9-145">To use OpenSSH, [configure your Raspberry Pi for passwordless SSH access](https://www.raspberrypi.org/documentation/remote-access/ssh/passwordless.md) <span class="docon docon-navigate-external x-hidden-focus"></span>.</span></span>

### <a name="deploy-the-app"></a><span data-ttu-id="2cdd9-146">Wdrażanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="2cdd9-146">Deploy the app</span></span>

<span data-ttu-id="2cdd9-147">Wdróż aplikację zgodnie z opisem w artykule [wdrażanie aplikacji .NET do Raspberry Pi](deployment.md).</span><span class="sxs-lookup"><span data-stu-id="2cdd9-147">Deploy the app as described in [Deploy .NET apps to Raspberry Pi](deployment.md).</span></span> <span data-ttu-id="2cdd9-148">Upewnij się, że ścieżka wdrożenia jest taka sama jak ścieżka określona w `cwd` parametrze w *launch.js* w konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="2cdd9-148">Ensure the deployment path is the same path specified in the `cwd` parameter in the *launch.json* configuration.</span></span>

### <a name="launch-the-debugger"></a><span data-ttu-id="2cdd9-149">Uruchom debuger</span><span class="sxs-lookup"><span data-stu-id="2cdd9-149">Launch the debugger</span></span>

<span data-ttu-id="2cdd9-150">Na karcie **przebieg** wybierz konfigurację **uruchamiania programu .NET Core (Konsola zdalna)** i wybierz pozycję **Rozpocznij debugowanie**.</span><span class="sxs-lookup"><span data-stu-id="2cdd9-150">On the **Run** tab, select the **.NET Core Launch (remote console)** configuration and select **Start Debugging**.</span></span> <span data-ttu-id="2cdd9-151">Aplikacja zostanie uruchomiona na Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="2cdd9-151">The app launches on the Raspberry Pi.</span></span> <span data-ttu-id="2cdd9-152">Debuger może służyć do ustawiania punktów przerwania, przeprowadzania inspekcji lokalnych i nie tylko.</span><span class="sxs-lookup"><span data-stu-id="2cdd9-152">The debugger may be used to set breakpoints, inspect locals, and more.</span></span>

## <a name="references"></a><span data-ttu-id="2cdd9-153">Odwołania</span><span class="sxs-lookup"><span data-stu-id="2cdd9-153">References</span></span>

<span data-ttu-id="2cdd9-154">[Zdalne debugowanie z vs Code w systemie Windows do Raspberry Pi przy użyciu platformy .NET Core na platformie ARM](https://www.hanselman.com/blog/remote-debugging-with-vs-code-on-windows-to-a-raspberry-pi-using-net-core-on-arm)<span class="docon docon-navigate-external x-hidden-focus"></span></span><span class="sxs-lookup"><span data-stu-id="2cdd9-154">[Remote debugging with VS Code on Windows to a Raspberry Pi using .NET Core on ARM](https://www.hanselman.com/blog/remote-debugging-with-vs-code-on-windows-to-a-raspberry-pi-using-net-core-on-arm) <span class="docon docon-navigate-external x-hidden-focus"></span></span></span>

::: zone-end

::: zone pivot="visualstudio"

## <a name="debug-from-visual-studio-on-windows"></a><span data-ttu-id="2cdd9-155">Debuguj z programu Visual Studio w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="2cdd9-155">Debug from Visual Studio on Windows</span></span>

<span data-ttu-id="2cdd9-156">Program Visual Studio może debugować aplikacje .NET na urządzeniach zdalnych za pośrednictwem protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="2cdd9-156">Visual Studio can debug .NET apps on remote devices via SSH.</span></span> <span data-ttu-id="2cdd9-157">Na urządzeniu nie jest wymagana specjalna konfiguracja.</span><span class="sxs-lookup"><span data-stu-id="2cdd9-157">No specialized configuration is required on the device.</span></span> <span data-ttu-id="2cdd9-158">Aby uzyskać szczegółowe informacje na temat używania programu Visual Studio do zdalnego debugowania programu .NET, zobacz [zdalne debugowanie .NET w systemie Linux przy użyciu protokołu SSH](/visualstudio/debugger/remote-debugging-dotnet-core-linux-with-ssh?view=vs-2019).</span><span class="sxs-lookup"><span data-stu-id="2cdd9-158">For details on using Visual Studio to debug .NET remotely, see [Remote debug .NET on Linux using SSH](/visualstudio/debugger/remote-debugging-dotnet-core-linux-with-ssh?view=vs-2019).</span></span>

::: zone-end
