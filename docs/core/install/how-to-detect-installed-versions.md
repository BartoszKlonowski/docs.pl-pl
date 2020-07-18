---
title: Sprawdzanie zainstalowanych wersji programu .NET Core w systemach Windows, Linux i macOS — .NET Core
description: Dowiedz się, jak wyświetlić listę wersji platformy .NET Core zainstalowanych na komputerze. Obejmuje to środowisko uruchomieniowe platformy .NET Core i zestaw SDK.
author: adegeo
ms.author: adegeo
ms.date: 12/04/2019
ms.custom: updateeachrelease
zone_pivot_groups: operating-systems-set-one
ms.openlocfilehash: b8825dee595c601e8adef0a52e651ac4a4f04831
ms.sourcegitcommit: 3492dafceb5d4183b6b0d2f3bdf4a1abc4d5ed8c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/16/2020
ms.locfileid: "86416044"
---
# <a name="how-to-check-that-net-core-is-already-installed"></a><span data-ttu-id="e7711-104">Jak sprawdzić, czy program .NET Core jest już zainstalowany</span><span class="sxs-lookup"><span data-stu-id="e7711-104">How to check that .NET Core is already installed</span></span>

<span data-ttu-id="e7711-105">W tym artykule przedstawiono sposób sprawdzania, które wersje środowiska uruchomieniowego .NET Core i zestawu SDK są zainstalowane na komputerze.</span><span class="sxs-lookup"><span data-stu-id="e7711-105">This article teaches you how to check which versions of the .NET Core runtime and SDK are installed on your computer.</span></span> <span data-ttu-id="e7711-106">Program .NET Core mógł już być zainstalowany, jeśli masz zintegrowane środowisko programistyczne, takie jak Visual Studio lub Visual Studio dla komputerów Mac.</span><span class="sxs-lookup"><span data-stu-id="e7711-106">.NET core may have already been installed if you have an integrated development environment, such as Visual Studio or Visual Studio for Mac.</span></span>

<span data-ttu-id="e7711-107">Zainstalowanie zestawu SDK instaluje odpowiednie środowisko uruchomieniowe.</span><span class="sxs-lookup"><span data-stu-id="e7711-107">Installing an SDK installs the corresponding runtime.</span></span>

<span data-ttu-id="e7711-108">Jeśli którykolwiek z poleceń w tym artykule nie powiedzie się, nie masz zainstalowanego środowiska uruchomieniowego lub zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="e7711-108">If any command in this article fails, you don't have the runtime or SDK installed.</span></span> <span data-ttu-id="e7711-109">Aby uzyskać więcej informacji, zobacz artykuły instalacyjne dla [systemu Windows](windows.md), [macOS](macos.md)lub [Linux](linux.md).</span><span class="sxs-lookup"><span data-stu-id="e7711-109">For more information, see the install articles for [Windows](windows.md), [macOS](macos.md), or [Linux](linux.md).</span></span>

## <a name="check-sdk-versions"></a><span data-ttu-id="e7711-110">Sprawdź wersje zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="e7711-110">Check SDK versions</span></span>

<span data-ttu-id="e7711-111">Możesz sprawdzić, które wersje zestaw .NET Core SDK są obecnie zainstalowane z terminalem.</span><span class="sxs-lookup"><span data-stu-id="e7711-111">You can see which versions of the .NET Core SDK are currently installed with a terminal.</span></span> <span data-ttu-id="e7711-112">Otwórz Terminal i uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="e7711-112">Open a terminal and run the following command.</span></span>

```dotnetcli
dotnet --list-sdks
```

<span data-ttu-id="e7711-113">Dane wyjściowe są podobne do poniższych.</span><span class="sxs-lookup"><span data-stu-id="e7711-113">You get output similar to the following.</span></span>

::: zone pivot="os-windows"

```console
2.1.500 [C:\program files\dotnet\sdk]
2.1.502 [C:\program files\dotnet\sdk]
2.1.504 [C:\program files\dotnet\sdk]
2.1.600 [C:\program files\dotnet\sdk]
2.1.602 [C:\program files\dotnet\sdk]
2.2.101 [C:\program files\dotnet\sdk]
3.0.100 [C:\program files\dotnet\sdk]
3.1.100 [C:\program files\dotnet\sdk]
```

::: zone-end

::: zone pivot="os-linux"

```bash
2.1.500 [/home/user/dotnet/sdk]
2.1.502 [/home/user/dotnet/sdk]
2.1.504 [/home/user/dotnet/sdk]
2.1.600 [/home/user/dotnet/sdk]
2.1.602 [/home/user/dotnet/sdk]
2.2.101 [/home/user/dotnet/sdk]
3.0.100 [/home/user/dotnet/sdk]
3.1.100 [/home/user/dotnet/sdk]
```

::: zone-end

::: zone pivot="os-macos"

```bash
2.1.500 [/usr/local/share/dotnet/sdk]
2.1.502 [/usr/local/share/dotnet/sdk]
2.1.504 [/usr/local/share/dotnet/sdk]
2.1.600 [/usr/local/share/dotnet/sdk]
2.1.602 [/usr/local/share/dotnet/sdk]
2.2.101 [/usr/local/share/dotnet/sdk]
3.0.100 [/usr/local/share/dotnet/sdk]
3.1.100 [/usr/local/share/dotnet/sdk]
```

::: zone-end

## <a name="check-runtime-versions"></a><span data-ttu-id="e7711-114">Sprawdź wersje środowiska uruchomieniowego</span><span class="sxs-lookup"><span data-stu-id="e7711-114">Check runtime versions</span></span>

<span data-ttu-id="e7711-115">Możesz sprawdzić, które wersje środowiska uruchomieniowego .NET Core są obecnie zainstalowane przy użyciu następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="e7711-115">You can see which versions of the .NET Core runtime are currently installed with the following command.</span></span>

```dotnetcli
dotnet --list-runtimes
```

<span data-ttu-id="e7711-116">Dane wyjściowe są podobne do poniższych.</span><span class="sxs-lookup"><span data-stu-id="e7711-116">You get output similar to the following.</span></span>

::: zone pivot="os-windows"

```console
Microsoft.AspNetCore.All 2.1.7 [c:\program files\dotnet\shared\Microsoft.AspNetCore.All]
Microsoft.AspNetCore.All 2.1.13 [c:\program files\dotnet\shared\Microsoft.AspNetCore.All]
Microsoft.AspNetCore.All 2.2.0 [c:\program files\dotnet\shared\Microsoft.AspNetCore.All]
Microsoft.AspNetCore.All 2.2.3 [c:\program files\dotnet\shared\Microsoft.AspNetCore.All]
Microsoft.AspNetCore.All 2.2.7 [c:\program files\dotnet\shared\Microsoft.AspNetCore.All]
Microsoft.AspNetCore.App 2.1.6 [c:\program files\dotnet\shared\Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 2.1.7 [c:\program files\dotnet\shared\Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 2.1.13 [c:\program files\dotnet\shared\Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 2.2.0 [c:\program files\dotnet\shared\Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 2.2.7 [c:\program files\dotnet\shared\Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 3.0.0 [c:\program files\dotnet\shared\Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 3.1.0 [c:\program files\dotnet\shared\Microsoft.AspNetCore.App]
Microsoft.NETCore.App 2.1.7 [c:\program files\dotnet\shared\Microsoft.NETCore.App]
Microsoft.NETCore.App 2.1.13 [c:\program files\dotnet\shared\Microsoft.NETCore.App]
Microsoft.NETCore.App 2.2.0 [c:\program files\dotnet\shared\Microsoft.NETCore.App]
Microsoft.NETCore.App 2.2.3 [c:\program files\dotnet\shared\Microsoft.NETCore.App]
Microsoft.NETCore.App 2.2.7 [c:\program files\dotnet\shared\Microsoft.NETCore.App]
Microsoft.NETCore.App 3.0.0 [c:\program files\dotnet\shared\Microsoft.NETCore.App]
Microsoft.NETCore.App 3.1.0 [c:\program files\dotnet\shared\Microsoft.NETCore.App]
Microsoft.WindowsDesktop.App 3.0.0 [c:\program files\dotnet\shared\Microsoft.WindowsDesktop.App]
Microsoft.WindowsDesktop.App 3.1.0 [c:\program files\dotnet\shared\Microsoft.WindowsDesktop.App]
```

::: zone-end

::: zone pivot="os-linux"

```bash
Microsoft.AspNetCore.All 2.1.7 [/home/user/dotnet/shared/Microsoft.AspNetCore.All]
Microsoft.AspNetCore.All 2.1.13 [/home/user/dotnet/shared/Microsoft.AspNetCore.All]
Microsoft.AspNetCore.All 2.2.0 [/home/user/dotnet/shared/Microsoft.AspNetCore.All]
Microsoft.AspNetCore.All 2.2.3 [/home/user/dotnet/shared/Microsoft.AspNetCore.All]
Microsoft.AspNetCore.All 2.2.7 [/home/user/dotnet/shared/Microsoft.AspNetCore.All]
Microsoft.AspNetCore.App 2.1.6 [/home/user/dotnet/shared/Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 2.1.7 [/home/user/dotnet/shared/Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 2.1.13 [/home/user/dotnet/shared/Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 2.2.0 [/home/user/dotnet/shared/Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 2.2.7 [/home/user/dotnet/shared/Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 3.0.0 [/home/user/dotnet/shared/Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 3.1.0 [/home/user/dotnet/shared/Microsoft.AspNetCore.App]
Microsoft.NETCore.App 2.1.7 [/home/user/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 2.1.13 [/home/user/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 2.2.0 [/home/user/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 2.2.3 [/home/user/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 2.2.7 [/home/user/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 3.0.0 [/home/user/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 3.1.0 [/home/user/dotnet/shared/Microsoft.NETCore.App]
```

::: zone-end

::: zone pivot="os-macos"

```bash
Microsoft.AspNetCore.All 2.1.7 [/usr/local/share/dotnet/shared/Microsoft.AspNetCore.All]
Microsoft.AspNetCore.All 2.1.13 [/usr/local/share/dotnet/shared/Microsoft.AspNetCore.All]
Microsoft.AspNetCore.All 2.2.0 [/usr/local/share/dotnet/shared/Microsoft.AspNetCore.All]
Microsoft.AspNetCore.All 2.2.3 [/usr/local/share/dotnet/shared/Microsoft.AspNetCore.All]
Microsoft.AspNetCore.All 2.2.7 [/usr/local/share/dotnet/shared/Microsoft.AspNetCore.All]
Microsoft.AspNetCore.App 2.1.6 [/usr/local/share/dotnet/shared/Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 2.1.7 [/usr/local/share/dotnet/shared/Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 2.1.13 [/usr/local/share/dotnet/shared/Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 2.2.0 [/usr/local/share/dotnet/shared/Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 2.2.7 [/usr/local/share/dotnet/shared/Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 3.0.0 [/usr/local/share/dotnet/shared/Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 3.1.0 [/usr/local/share/dotnet/shared/Microsoft.AspNetCore.App]
Microsoft.NETCore.App 2.1.7 [/usr/local/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 2.1.13 [/usr/local/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 2.2.0 [/usr/local/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 2.2.3 [/usr/local/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 2.2.7 [/usr/local/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 3.0.0 [/usr/local/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 3.1.0 [/usr/local/share/dotnet/shared/Microsoft.NETCore.App]
```

::: zone-end

## <a name="check-for-install-folders"></a><span data-ttu-id="e7711-117">Sprawdź foldery instalacji</span><span class="sxs-lookup"><span data-stu-id="e7711-117">Check for install folders</span></span>

<span data-ttu-id="e7711-118">Jest możliwe, że platforma .NET Core jest zainstalowana, ale nie została dodana do `PATH` zmiennej dla systemu operacyjnego lub profilu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e7711-118">It's possible that .NET Core is installed but not added to the `PATH` variable for your operating system or user profile.</span></span> <span data-ttu-id="e7711-119">Uruchamianie poleceń z poprzednich sekcji może nie działać.</span><span class="sxs-lookup"><span data-stu-id="e7711-119">Running the commands from the previous sections may not work.</span></span> <span data-ttu-id="e7711-120">Alternatywnie można sprawdzić, czy istnieją foldery instalacji programu .NET Core.</span><span class="sxs-lookup"><span data-stu-id="e7711-120">As an alternative, you can check that the .NET Core install folders exist.</span></span>

<span data-ttu-id="e7711-121">W przypadku instalowania programu .NET Core z Instalatora lub skryptu jest on instalowany w folderze Standard.</span><span class="sxs-lookup"><span data-stu-id="e7711-121">When you install .NET Core from an installer or script, it's installed to a standard folder.</span></span> <span data-ttu-id="e7711-122">Większość czasu Instalator lub skrypt używany do instalowania programu .NET Core zapewnia opcję instalacji do innego folderu.</span><span class="sxs-lookup"><span data-stu-id="e7711-122">Much of the time the installer or script you're using to install .NET Core gives you an option to install to a different folder.</span></span> <span data-ttu-id="e7711-123">Jeśli zdecydujesz się zainstalować w innym folderze, Dostosuj początek ścieżki folderu.</span><span class="sxs-lookup"><span data-stu-id="e7711-123">If you choose to install to a different folder, adjust the start of the folder path.</span></span>

::: zone pivot="os-windows"

- <span data-ttu-id="e7711-124">**plik wykonywalny dotnet**</span><span class="sxs-lookup"><span data-stu-id="e7711-124">**dotnet executable**</span></span>\
<span data-ttu-id="e7711-125">_C: \\ program files \\ \\dotnet.exedotnet_</span><span class="sxs-lookup"><span data-stu-id="e7711-125">_C:\\program files\\dotnet\\dotnet.exe_</span></span>

- <span data-ttu-id="e7711-126">**ZESTAW SDK PLATFORMY .NET**</span><span class="sxs-lookup"><span data-stu-id="e7711-126">**.NET SDK**</span></span>\
<span data-ttu-id="e7711-127">_C: \\ Program Files \\ \\ zestaw dotnet SDK \\ {Version}\\_</span><span class="sxs-lookup"><span data-stu-id="e7711-127">_C:\\program files\\dotnet\\sdk\\{version}\\_</span></span>

- <span data-ttu-id="e7711-128">**Środowisko uruchomieniowe platformy .NET**</span><span class="sxs-lookup"><span data-stu-id="e7711-128">**.NET Runtime**</span></span>\
<span data-ttu-id="e7711-129">_C: \\ Program Files \\ \\ Shared dotnet \\ {Runtime-Type} \\ {Version}\\_</span><span class="sxs-lookup"><span data-stu-id="e7711-129">_C:\\program files\\dotnet\\shared\\{runtime-type}\\{version}\\_</span></span>

::: zone-end

::: zone pivot="os-linux"

- <span data-ttu-id="e7711-130">**plik wykonywalny dotnet**</span><span class="sxs-lookup"><span data-stu-id="e7711-130">**dotnet executable**</span></span>\
<span data-ttu-id="e7711-131">_/home/user/share/dotnet/dotnet_</span><span class="sxs-lookup"><span data-stu-id="e7711-131">_/home/user/share/dotnet/dotnet_</span></span>

- <span data-ttu-id="e7711-132">**ZESTAW SDK PLATFORMY .NET**</span><span class="sxs-lookup"><span data-stu-id="e7711-132">**.NET SDK**</span></span>\
<span data-ttu-id="e7711-133">_/home/user/share/dotnet/sdk/{version}/_</span><span class="sxs-lookup"><span data-stu-id="e7711-133">_/home/user/share/dotnet/sdk/{version}/_</span></span>

- <span data-ttu-id="e7711-134">**Środowisko uruchomieniowe platformy .NET**</span><span class="sxs-lookup"><span data-stu-id="e7711-134">**.NET Runtime**</span></span>\
<span data-ttu-id="e7711-135">_/home/user/share/dotnet/shared/{runtime-type}/{version}/_</span><span class="sxs-lookup"><span data-stu-id="e7711-135">_/home/user/share/dotnet/shared/{runtime-type}/{version}/_</span></span>

::: zone-end

::: zone pivot="os-macos"

- <span data-ttu-id="e7711-136">**plik wykonywalny dotnet**</span><span class="sxs-lookup"><span data-stu-id="e7711-136">**dotnet executable**</span></span>\
<span data-ttu-id="e7711-137">_/usr/local/share/dotnet/dotnet_</span><span class="sxs-lookup"><span data-stu-id="e7711-137">_/usr/local/share/dotnet/dotnet_</span></span>

- <span data-ttu-id="e7711-138">**ZESTAW SDK PLATFORMY .NET**</span><span class="sxs-lookup"><span data-stu-id="e7711-138">**.NET SDK**</span></span>\
<span data-ttu-id="e7711-139">_/usr/local/share/dotnet/sdk/{version}/_</span><span class="sxs-lookup"><span data-stu-id="e7711-139">_/usr/local/share/dotnet/sdk/{version}/_</span></span>

- <span data-ttu-id="e7711-140">**Środowisko uruchomieniowe platformy .NET**</span><span class="sxs-lookup"><span data-stu-id="e7711-140">**.NET Runtime**</span></span>\
<span data-ttu-id="e7711-141">_/usr/local/share/dotnet/shared/{runtime-type}/{version}/_</span><span class="sxs-lookup"><span data-stu-id="e7711-141">_/usr/local/share/dotnet/shared/{runtime-type}/{version}/_</span></span>

::: zone-end

## <a name="more-information"></a><span data-ttu-id="e7711-142">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="e7711-142">More information</span></span>

<span data-ttu-id="e7711-143">Można wyświetlić zarówno wersje zestawu SDK, jak i wersje środowiska uruchomieniowego za pomocą polecenia `dotnet --info` .</span><span class="sxs-lookup"><span data-stu-id="e7711-143">You can see both the SDK versions and runtime versions with the command `dotnet --info`.</span></span> <span data-ttu-id="e7711-144">Uzyskasz również inne informacje dotyczące środowiska, takie jak wersja systemu operacyjnego i identyfikator środowiska uruchomieniowego (RID).</span><span class="sxs-lookup"><span data-stu-id="e7711-144">You'll also get other environmental related information, such as the operating system version and runtime identifier (RID).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e7711-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e7711-145">Next steps</span></span>

- <span data-ttu-id="e7711-146">[Zainstaluj środowisko uruchomieniowe programu .NET Core i zestaw SDK](windows.md).</span><span class="sxs-lookup"><span data-stu-id="e7711-146">[Install the .NET Core Runtime and SDK](windows.md).</span></span>
