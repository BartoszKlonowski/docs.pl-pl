---
title: Instalowanie platformy .NET w systemie CentOS — .NET
description: Przedstawiono różne sposoby instalowania zestawu .NET SDK i środowiska uruchomieniowego .NET w systemie CentOS.
author: adegeo
ms.author: adegeo
ms.date: 11/10/2020
ms.openlocfilehash: 2c3453c79a1dc31f01577bc0c1b9e320eb307c0a
ms.sourcegitcommit: 45c7148f2483db2501c1aa696ab6ed2ed8cb71b2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/08/2020
ms.locfileid: "96851682"
---
# <a name="install-the-net-sdk-or-the-net-runtime-on-centos"></a><span data-ttu-id="f1371-103">Zainstaluj zestaw .NET SDK lub środowisko uruchomieniowe .NET w systemie CentOS</span><span class="sxs-lookup"><span data-stu-id="f1371-103">Install the .NET SDK or the .NET Runtime on CentOS</span></span>

<span data-ttu-id="f1371-104">Platforma .NET jest obsługiwana w systemie CentOS.</span><span class="sxs-lookup"><span data-stu-id="f1371-104">.NET is supported on CentOS.</span></span> <span data-ttu-id="f1371-105">W tym artykule opisano sposób instalowania programu .NET w systemie CentOS.</span><span class="sxs-lookup"><span data-stu-id="f1371-105">This article describes how to install .NET on CentOS.</span></span>

[!INCLUDE [linux-intro-sdk-vs-runtime](includes/linux-intro-sdk-vs-runtime.md)]

[!INCLUDE [linux-install-package-manager-x64-vs-arm](includes/linux-install-package-manager-x64-vs-arm.md)]

## <a name="supported-distributions"></a><span data-ttu-id="f1371-106">Obsługiwane dystrybucje</span><span class="sxs-lookup"><span data-stu-id="f1371-106">Supported distributions</span></span>

<span data-ttu-id="f1371-107">Poniższa tabela zawiera listę obecnie obsługiwanych wersji platformy .NET w systemach CentOS 7 i CentOS 8.</span><span class="sxs-lookup"><span data-stu-id="f1371-107">The following table is a list of currently supported .NET releases on both CentOS 7 and CentOS 8.</span></span> <span data-ttu-id="f1371-108">Te wersje pozostają obsługiwane, dopóki wersja [platformy .NET nie osiągnie końca obsługi](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) lub wersja CentOS nie jest już obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="f1371-108">These versions remain supported until either the version of [.NET reaches end-of-support](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) or the version of CentOS is no longer supported.</span></span>

- <span data-ttu-id="f1371-109">✔️ wskazuje, że wersja programu CentOS lub .NET jest nadal obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="f1371-109">A ✔️ indicates that the version of CentOS or .NET is still supported.</span></span>
- <span data-ttu-id="f1371-110">❌Wskazuje, że wersja programu CentOS lub .NET nie jest obsługiwana w tej wersji CentOS.</span><span class="sxs-lookup"><span data-stu-id="f1371-110">A ❌ indicates that the version of CentOS or .NET isn't supported on that CentOS release.</span></span>
- <span data-ttu-id="f1371-111">Gdy wersja programu CentOS i wersja platformy .NET mają ✔️, obsługiwane są kombinacje systemów operacyjnych i .NET.</span><span class="sxs-lookup"><span data-stu-id="f1371-111">When both a version of CentOS and a version of .NET have ✔️, that OS and .NET combination is supported.</span></span>

| <span data-ttu-id="f1371-112">CentOS</span><span class="sxs-lookup"><span data-stu-id="f1371-112">CentOS</span></span>                   | <span data-ttu-id="f1371-113">.NET Core 2.1</span><span class="sxs-lookup"><span data-stu-id="f1371-113">.NET Core 2.1</span></span> | <span data-ttu-id="f1371-114">.NET Core 3.1</span><span class="sxs-lookup"><span data-stu-id="f1371-114">.NET Core 3.1</span></span> | <span data-ttu-id="f1371-115">.NET 5.0</span><span class="sxs-lookup"><span data-stu-id="f1371-115">.NET 5.0</span></span> |
|--------------------------|---------------|---------------|----------------|
| <span data-ttu-id="f1371-116">✔️ [8](#centos-8-)</span><span class="sxs-lookup"><span data-stu-id="f1371-116">✔️ [8](#centos-8-)</span></span> | <span data-ttu-id="f1371-117">✔️ 2,1</span><span class="sxs-lookup"><span data-stu-id="f1371-117">✔️ 2.1</span></span>        | <span data-ttu-id="f1371-118">✔️ 3,1</span><span class="sxs-lookup"><span data-stu-id="f1371-118">✔️ 3.1</span></span>        | <span data-ttu-id="f1371-119">✔️ 5,0</span><span class="sxs-lookup"><span data-stu-id="f1371-119">✔️ 5.0</span></span> |
| <span data-ttu-id="f1371-120">✔️ [7](#centos-7-)</span><span class="sxs-lookup"><span data-stu-id="f1371-120">✔️ [7](#centos-7-)</span></span> | <span data-ttu-id="f1371-121">✔️ 2,1</span><span class="sxs-lookup"><span data-stu-id="f1371-121">✔️ 2.1</span></span>        | <span data-ttu-id="f1371-122">✔️ 3,1</span><span class="sxs-lookup"><span data-stu-id="f1371-122">✔️ 3.1</span></span>        | <span data-ttu-id="f1371-123">✔️ 5,0</span><span class="sxs-lookup"><span data-stu-id="f1371-123">✔️ 5.0</span></span> |

<span data-ttu-id="f1371-124">Następujące wersje platformy .NET nie są już obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="f1371-124">The following versions of .NET are no longer supported.</span></span> <span data-ttu-id="f1371-125">Pliki do pobrania dla tych nadal są publikowane:</span><span class="sxs-lookup"><span data-stu-id="f1371-125">The downloads for these still remain published:</span></span>

- <span data-ttu-id="f1371-126">3.0</span><span class="sxs-lookup"><span data-stu-id="f1371-126">3.0</span></span>
- <span data-ttu-id="f1371-127">2.2</span><span class="sxs-lookup"><span data-stu-id="f1371-127">2.2</span></span>
- <span data-ttu-id="f1371-128">2,0</span><span class="sxs-lookup"><span data-stu-id="f1371-128">2.0</span></span>

[!INCLUDE [linux-install-package-manager-x64-vs-arm](includes/linux-install-package-manager-x64-vs-arm.md)]

## <a name="remove-preview-versions"></a><span data-ttu-id="f1371-129">Usuń wersje w wersji zapoznawczej</span><span class="sxs-lookup"><span data-stu-id="f1371-129">Remove preview versions</span></span>

[!INCLUDE [package-manager uninstall notice](./includes/linux-uninstall-preview-info.md)]

## <a name="how-to-install-other-versions"></a><span data-ttu-id="f1371-130">Jak zainstalować inne wersje</span><span class="sxs-lookup"><span data-stu-id="f1371-130">How to install other versions</span></span>

[!INCLUDE [package-manager-switcher](./includes/package-manager-heading-hack-pkgname.md)]

## <a name="centos-8-"></a><span data-ttu-id="f1371-131">CentOS 8 ✔️</span><span class="sxs-lookup"><span data-stu-id="f1371-131">CentOS 8 ✔️</span></span>

<span data-ttu-id="f1371-132">Program .NET 5,0 jest dostępny w domyślnych repozytoriach pakietów dla CentOS 8.</span><span class="sxs-lookup"><span data-stu-id="f1371-132">.NET 5.0 is available in the default package repositories for CentOS 8.</span></span>

[!INCLUDE [linux-dnf-install-50](includes/linux-install-50-dnf.md)]

## <a name="centos-7-"></a><span data-ttu-id="f1371-133">CentOS ✔️ 7</span><span class="sxs-lookup"><span data-stu-id="f1371-133">CentOS 7 ✔️</span></span>

[!INCLUDE [linux-prep-intro-generic](includes/linux-prep-intro-generic.md)]

```bash
sudo rpm -Uvh https://packages.microsoft.com/config/centos/7/packages-microsoft-prod.rpm
```

[!INCLUDE [linux-yum-install-50](includes/linux-install-50-yum.md)]

## <a name="troubleshoot-the-package-manager"></a><span data-ttu-id="f1371-134">Rozwiązywanie problemów z menedżerem pakietów</span><span class="sxs-lookup"><span data-stu-id="f1371-134">Troubleshoot the package manager</span></span>

<span data-ttu-id="f1371-135">Ta sekcja zawiera informacje o typowych błędach, które mogą wystąpić podczas instalowania programu .NET przy użyciu Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="f1371-135">This section provides information on common errors you may get while using the package manager to install .NET.</span></span>

### <a name="unable-to-find-package"></a><span data-ttu-id="f1371-136">Nie można znaleźć pakietu</span><span class="sxs-lookup"><span data-stu-id="f1371-136">Unable to find package</span></span>

[!INCLUDE [linux-install-package-manager-x64-vs-arm](includes/linux-install-package-manager-x64-vs-arm.md)]

### <a name="failed-to-fetch"></a><span data-ttu-id="f1371-137">Nie można pobrać</span><span class="sxs-lookup"><span data-stu-id="f1371-137">Failed to fetch</span></span>

[!INCLUDE [package-manager-failed-to-fetch-rpm](includes/package-manager-failed-to-fetch-rpm.md)]

## <a name="snap"></a><span data-ttu-id="f1371-138">Przystawki</span><span class="sxs-lookup"><span data-stu-id="f1371-138">Snap</span></span>

[!INCLUDE [linux-install-snap](includes/linux-install-snap.md)]

## <a name="dependencies"></a><span data-ttu-id="f1371-139">Zależności</span><span class="sxs-lookup"><span data-stu-id="f1371-139">Dependencies</span></span>

[!INCLUDE [linux-rpm-install-dependencies](includes/linux-rpm-install-dependencies.md)]

## <a name="scripted-install"></a><span data-ttu-id="f1371-140">Instalacja z skryptami</span><span class="sxs-lookup"><span data-stu-id="f1371-140">Scripted install</span></span>

[!INCLUDE [linux-install-scripted](includes/linux-install-scripted.md)]

## <a name="manual-install"></a><span data-ttu-id="f1371-141">Instalacja ręczna</span><span class="sxs-lookup"><span data-stu-id="f1371-141">Manual install</span></span>

[!INCLUDE [linux-install-manual](includes/linux-install-manual.md)]

## <a name="next-steps"></a><span data-ttu-id="f1371-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f1371-142">Next steps</span></span>

- [<span data-ttu-id="f1371-143">Samouczek: Tworzenie aplikacji konsolowej za pomocą zestawu .NET SDK przy użyciu Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="f1371-143">Tutorial: Create a console application with .NET SDK using Visual Studio Code</span></span>](../tutorials/with-visual-studio-code.md)
