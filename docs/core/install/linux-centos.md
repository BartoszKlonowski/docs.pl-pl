---
title: Instalowanie programu .NET Core w systemie CentOS — .NET Core
description: Ilustruje różne sposoby instalowania zestaw .NET Core SDK i środowiska uruchomieniowego .NET Core w systemie CentOS.
author: thraka
ms.author: adegeo
ms.date: 06/04/2020
ms.openlocfilehash: 743bd4ce47fdecef512f9605d8ec5503eb6da9ba
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/09/2020
ms.locfileid: "84603140"
---
# <a name="install-net-core-sdk-or-net-core-runtime-on-centos"></a><span data-ttu-id="bf806-103">Zainstaluj zestaw .NET Core SDK lub środowisko uruchomieniowe platformy .NET Core w systemie CentOS</span><span class="sxs-lookup"><span data-stu-id="bf806-103">Install .NET Core SDK or .NET Core Runtime on CentOS</span></span>

<span data-ttu-id="bf806-104">Platforma .NET Core jest obsługiwana w systemie CentOS.</span><span class="sxs-lookup"><span data-stu-id="bf806-104">.NET Core is supported on CentOS.</span></span> <span data-ttu-id="bf806-105">W tym artykule opisano sposób instalowania programu .NET Core w systemie CentOS.</span><span class="sxs-lookup"><span data-stu-id="bf806-105">This article describes how to install .NET Core on CentOS.</span></span>

[!INCLUDE [linux-intro-sdk-vs-runtime](includes/linux-intro-sdk-vs-runtime.md)]

[!INCLUDE [linux-install-package-manager-x64-vs-arm](includes/linux-install-package-manager-x64-vs-arm.md)]

## <a name="supported-distributions"></a><span data-ttu-id="bf806-106">Obsługiwane dystrybucje</span><span class="sxs-lookup"><span data-stu-id="bf806-106">Supported distributions</span></span>

<span data-ttu-id="bf806-107">Poniższa tabela zawiera listę obecnie obsługiwanych wersji programu .NET Core w systemach CentOS 7 i CentOS 8.</span><span class="sxs-lookup"><span data-stu-id="bf806-107">The following table is a list of currently supported .NET Core releases on both CentOS 7 and CentOS 8.</span></span> <span data-ttu-id="bf806-108">Te wersje pozostają obsługiwane, dopóki wersja [platformy .NET Core osiągnie koniec obsługi](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) lub wersja programu CentOS nie jest już obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="bf806-108">These versions remain supported until either the version of [.NET Core reaches end-of-support](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) or the version of CentOS is no longer supported.</span></span>

- <span data-ttu-id="bf806-109">✔️ wskazuje, że wersja programu CentOS lub .NET Core jest nadal obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="bf806-109">A ✔️ indicates that the version of CentOS or .NET Core is still supported.</span></span>
- <span data-ttu-id="bf806-110">❌Wskazuje, że wersja CentOS lub .NET Core nie jest obsługiwana w tej wersji CentOS.</span><span class="sxs-lookup"><span data-stu-id="bf806-110">A ❌ indicates that the version of CentOS or .NET Core isn't supported on that CentOS release.</span></span>
- <span data-ttu-id="bf806-111">Gdy wersja CentOS i wersja platformy .NET Core mają ✔️, obsługiwane są kombinacje systemów operacyjnych i .NET.</span><span class="sxs-lookup"><span data-stu-id="bf806-111">When both a version of CentOS and a version of .NET Core have ✔️, that OS and .NET combination are supported.</span></span>

| <span data-ttu-id="bf806-112">CentOS</span><span class="sxs-lookup"><span data-stu-id="bf806-112">CentOS</span></span>                   | <span data-ttu-id="bf806-113">.NET Core 2.1</span><span class="sxs-lookup"><span data-stu-id="bf806-113">.NET Core 2.1</span></span> | <span data-ttu-id="bf806-114">.NET Core 3,1</span><span class="sxs-lookup"><span data-stu-id="bf806-114">.NET Core 3.1</span></span> | <span data-ttu-id="bf806-115">.NET 5 (wersja zapoznawcza) (tylko instalacja ręczna)</span><span class="sxs-lookup"><span data-stu-id="bf806-115">.NET 5 Preview (manual install only)</span></span> |
|--------------------------|---------------|---------------|----------------|
| <span data-ttu-id="bf806-116">✔️ [8](#centos-8-)</span><span class="sxs-lookup"><span data-stu-id="bf806-116">✔️ [8](#centos-8-)</span></span> | <span data-ttu-id="bf806-117">✔️ 2,1</span><span class="sxs-lookup"><span data-stu-id="bf806-117">✔️ 2.1</span></span>        | <span data-ttu-id="bf806-118">✔️ 3,1</span><span class="sxs-lookup"><span data-stu-id="bf806-118">✔️ 3.1</span></span>        | <span data-ttu-id="bf806-119">✔️ 5,0 — wersja zapoznawcza</span><span class="sxs-lookup"><span data-stu-id="bf806-119">✔️ 5.0 Preview</span></span> |
| <span data-ttu-id="bf806-120">✔️ [7](#centos-7-)</span><span class="sxs-lookup"><span data-stu-id="bf806-120">✔️ [7](#centos-7-)</span></span> | <span data-ttu-id="bf806-121">✔️ 2,1</span><span class="sxs-lookup"><span data-stu-id="bf806-121">✔️ 2.1</span></span>        | <span data-ttu-id="bf806-122">✔️ 3,1</span><span class="sxs-lookup"><span data-stu-id="bf806-122">✔️ 3.1</span></span>        | <span data-ttu-id="bf806-123">✔️ 5,0 — wersja zapoznawcza</span><span class="sxs-lookup"><span data-stu-id="bf806-123">✔️ 5.0 Preview</span></span> |

<span data-ttu-id="bf806-124">Następujące wersje programu .NET Core nie są już obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="bf806-124">The following versions of .NET Core are no longer supported.</span></span> <span data-ttu-id="bf806-125">Pliki do pobrania dla tych nadal są publikowane:</span><span class="sxs-lookup"><span data-stu-id="bf806-125">The downloads for these still remain published:</span></span>

- <span data-ttu-id="bf806-126">3.0</span><span class="sxs-lookup"><span data-stu-id="bf806-126">3.0</span></span>
- <span data-ttu-id="bf806-127">2.2</span><span class="sxs-lookup"><span data-stu-id="bf806-127">2.2</span></span>
- <span data-ttu-id="bf806-128">2.0</span><span class="sxs-lookup"><span data-stu-id="bf806-128">2.0</span></span>

[!INCLUDE [linux-install-package-manager-x64-vs-arm](includes/linux-install-package-manager-x64-vs-arm.md)]

## <a name="how-to-install-other-versions"></a><span data-ttu-id="bf806-129">Jak zainstalować inne wersje</span><span class="sxs-lookup"><span data-stu-id="bf806-129">How to install other versions</span></span>

[!INCLUDE [package-manager-switcher](./includes/package-manager-heading-hack-pkgname.md)]

## <a name="centos-8-"></a><span data-ttu-id="bf806-130">CentOS 8 ✔️</span><span class="sxs-lookup"><span data-stu-id="bf806-130">CentOS 8 ✔️</span></span>

<span data-ttu-id="bf806-131">Program .NET Core 3,1 jest dostępny w repozytoriach pakietów domyślnych dla CentOS 8.</span><span class="sxs-lookup"><span data-stu-id="bf806-131">.NET Core 3.1 is available in the default package repositories for CentOS 8.</span></span>

[!INCLUDE [linux-dnf-install-31](includes/linux-install-31-dnf.md)]

## <a name="centos-7-"></a><span data-ttu-id="bf806-132">CentOS ✔️ 7</span><span class="sxs-lookup"><span data-stu-id="bf806-132">CentOS 7 ✔️</span></span>

[!INCLUDE [linux-prep-intro-generic](includes/linux-prep-intro-generic.md)]

```bash
sudo rpm -Uvh https://packages.microsoft.com/config/centos/7/packages-microsoft-prod.rpm
```

[!INCLUDE [linux-yum-install-31](includes/linux-install-31-yum.md)]

## <a name="troubleshoot-the-package-manager"></a><span data-ttu-id="bf806-133">Rozwiązywanie problemów z menedżerem pakietów</span><span class="sxs-lookup"><span data-stu-id="bf806-133">Troubleshoot the package manager</span></span>

<span data-ttu-id="bf806-134">Ta sekcja zawiera informacje o typowych błędach, które mogą wystąpić podczas korzystania z Menedżera pakietów w celu zainstalowania platformy .NET Core.</span><span class="sxs-lookup"><span data-stu-id="bf806-134">This section provides information on common errors you may get while using the package manager to install .NET Core.</span></span>

### <a name="failed-to-fetch"></a><span data-ttu-id="bf806-135">Nie można pobrać</span><span class="sxs-lookup"><span data-stu-id="bf806-135">Failed to fetch</span></span>

[!INCLUDE [package-manager-failed-to-fetch-rpm](includes/package-manager-failed-to-fetch-rpm.md)]

## <a name="snap"></a><span data-ttu-id="bf806-136">Przystawki</span><span class="sxs-lookup"><span data-stu-id="bf806-136">Snap</span></span>

[!INCLUDE [linux-install-snap](includes/linux-install-snap.md)]

## <a name="dependencies"></a><span data-ttu-id="bf806-137">Zależności</span><span class="sxs-lookup"><span data-stu-id="bf806-137">Dependencies</span></span>

[!INCLUDE [linux-install-dependencies](includes/linux-install-dependencies.md)]

## <a name="scripted-install"></a><span data-ttu-id="bf806-138">Instalacja z skryptami</span><span class="sxs-lookup"><span data-stu-id="bf806-138">Scripted install</span></span>

[!INCLUDE [linux-install-scripted](includes/linux-install-scripted.md)]

## <a name="manual-install"></a><span data-ttu-id="bf806-139">Instalacja ręczna</span><span class="sxs-lookup"><span data-stu-id="bf806-139">Manual install</span></span>

[!INCLUDE [linux-install-manual](includes/linux-install-manual.md)]

## <a name="next-steps"></a><span data-ttu-id="bf806-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bf806-140">Next steps</span></span>

- [<span data-ttu-id="bf806-141">Samouczek: Tworzenie aplikacji konsolowej z zestaw .NET Core SDK przy użyciu Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="bf806-141">Tutorial: Create a console application with .NET Core SDK using Visual Studio Code</span></span>](../tutorials/with-visual-studio-code.md)