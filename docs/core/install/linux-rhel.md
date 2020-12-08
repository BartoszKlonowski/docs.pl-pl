---
title: Instalowanie platformy .NET w systemie RHEL — .NET
description: Przedstawiono różne sposoby instalowania zestawu .NET SDK i środowiska uruchomieniowego .NET w systemie RHEL.
author: adegeo
ms.author: adegeo
ms.date: 11/10/2020
ms.openlocfilehash: 0b6138185bfd3e2f50c1b31e82779165715a5b6e
ms.sourcegitcommit: 45c7148f2483db2501c1aa696ab6ed2ed8cb71b2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/08/2020
ms.locfileid: "96851643"
---
# <a name="install-the-net-sdk-or-the-net-runtime-on-rhel"></a><span data-ttu-id="3b4df-103">Zainstaluj zestaw .NET SDK lub środowisko uruchomieniowe .NET w systemie RHEL</span><span class="sxs-lookup"><span data-stu-id="3b4df-103">Install the .NET SDK or the .NET Runtime on RHEL</span></span>

<span data-ttu-id="3b4df-104">Platforma .NET jest obsługiwana w systemie RHEL.</span><span class="sxs-lookup"><span data-stu-id="3b4df-104">.NET is supported on RHEL.</span></span> <span data-ttu-id="3b4df-105">W tym artykule opisano sposób instalowania programu .NET w systemie RHEL.</span><span class="sxs-lookup"><span data-stu-id="3b4df-105">This article describes how to install .NET on RHEL.</span></span>

[!INCLUDE [linux-intro-sdk-vs-runtime](includes/linux-intro-sdk-vs-runtime.md)]

## <a name="register-your-red-hat-subscription"></a><span data-ttu-id="3b4df-106">Zarejestruj swoją subskrypcję Red Hat</span><span class="sxs-lookup"><span data-stu-id="3b4df-106">Register your Red Hat subscription</span></span>

<span data-ttu-id="3b4df-107">Aby zainstalować platformę .NET z systemu Red Hat na RHEL, musisz najpierw zarejestrować się przy użyciu Menedżera subskrypcji Red Hat.</span><span class="sxs-lookup"><span data-stu-id="3b4df-107">To install .NET from Red Hat on RHEL, you first need to register using the Red Hat Subscription Manager.</span></span> <span data-ttu-id="3b4df-108">Jeśli nie zostało to zrobione w systemie lub nie masz pewności, zobacz [dokumentację produktu Red Hat dla platformy .NET](https://access.redhat.com/documentation/net/5.0/).</span><span class="sxs-lookup"><span data-stu-id="3b4df-108">If this hasn't been done on your system, or if you're unsure, see the [Red Hat Product Documentation for .NET](https://access.redhat.com/documentation/net/5.0/).</span></span>

## <a name="supported-distributions"></a><span data-ttu-id="3b4df-109">Obsługiwane dystrybucje</span><span class="sxs-lookup"><span data-stu-id="3b4df-109">Supported distributions</span></span>

<span data-ttu-id="3b4df-110">Poniższa tabela zawiera listę obecnie obsługiwanych wersji platformy .NET w systemach RHEL 7 i RHEL 8.</span><span class="sxs-lookup"><span data-stu-id="3b4df-110">The following table is a list of currently supported .NET releases on both RHEL 7 and RHEL 8.</span></span> <span data-ttu-id="3b4df-111">Te wersje pozostają obsługiwane, dopóki wersja [platformy .NET nie osiągnie końca obsługi](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) lub wersja RHEL nie jest już obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="3b4df-111">These versions remain supported until either the version of [.NET reaches end-of-support](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) or the version of RHEL is no longer supported.</span></span>

- <span data-ttu-id="3b4df-112">✔️ wskazuje, że wersja programu RHEL lub .NET jest nadal obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="3b4df-112">A ✔️ indicates that the version of RHEL or .NET is still supported.</span></span>
- <span data-ttu-id="3b4df-113">❌Wskazuje, że wersja programu RHEL lub .NET nie jest obsługiwana w tej wersji RHEL.</span><span class="sxs-lookup"><span data-stu-id="3b4df-113">A ❌ indicates that the version of RHEL or .NET isn't supported on that RHEL release.</span></span>
- <span data-ttu-id="3b4df-114">Gdy wersja programu RHEL i wersja platformy .NET mają ✔️, obsługiwane są kombinacje systemów operacyjnych i .NET.</span><span class="sxs-lookup"><span data-stu-id="3b4df-114">When both a version of RHEL and a version of .NET have ✔️, that OS and .NET combination is supported.</span></span>

| <span data-ttu-id="3b4df-115">RHEL</span><span class="sxs-lookup"><span data-stu-id="3b4df-115">RHEL</span></span>                     | <span data-ttu-id="3b4df-116">.NET Core 2.1</span><span class="sxs-lookup"><span data-stu-id="3b4df-116">.NET Core 2.1</span></span> | <span data-ttu-id="3b4df-117">.NET Core 3.1</span><span class="sxs-lookup"><span data-stu-id="3b4df-117">.NET Core 3.1</span></span> | <span data-ttu-id="3b4df-118">.NET 5.0</span><span class="sxs-lookup"><span data-stu-id="3b4df-118">.NET 5.0</span></span> |
|--------------------------|---------------|---------------|----------------|
| <span data-ttu-id="3b4df-119">✔️ [8](#rhel-8-)</span><span class="sxs-lookup"><span data-stu-id="3b4df-119">✔️ [8](#rhel-8-)</span></span>        | <span data-ttu-id="3b4df-120">✔️ 2,1</span><span class="sxs-lookup"><span data-stu-id="3b4df-120">✔️ 2.1</span></span>        | <span data-ttu-id="3b4df-121">✔️ 3,1</span><span class="sxs-lookup"><span data-stu-id="3b4df-121">✔️ 3.1</span></span>        | <span data-ttu-id="3b4df-122">✔️ 5,0</span><span class="sxs-lookup"><span data-stu-id="3b4df-122">✔️ 5.0</span></span> |
| <span data-ttu-id="3b4df-123">✔️ [7](#rhel-7--net-50)</span><span class="sxs-lookup"><span data-stu-id="3b4df-123">✔️ [7](#rhel-7--net-50)</span></span> | <span data-ttu-id="3b4df-124">✔️ 2,1</span><span class="sxs-lookup"><span data-stu-id="3b4df-124">✔️ 2.1</span></span>        | <span data-ttu-id="3b4df-125">✔️ [3,1](#rhel-7--net-core-31)</span><span class="sxs-lookup"><span data-stu-id="3b4df-125">✔️ [3.1](#rhel-7--net-core-31)</span></span>        | <span data-ttu-id="3b4df-126">✔️ [5,0](#rhel-7--net-50)</span><span class="sxs-lookup"><span data-stu-id="3b4df-126">✔️ [5.0](#rhel-7--net-50)</span></span> |

<span data-ttu-id="3b4df-127">Następujące wersje platformy .NET nie są już obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="3b4df-127">The following versions of .NET are no longer supported.</span></span> <span data-ttu-id="3b4df-128">Pliki do pobrania dla tych nadal są publikowane:</span><span class="sxs-lookup"><span data-stu-id="3b4df-128">The downloads for these still remain published:</span></span>

- <span data-ttu-id="3b4df-129">3.0</span><span class="sxs-lookup"><span data-stu-id="3b4df-129">3.0</span></span>
- <span data-ttu-id="3b4df-130">2.2</span><span class="sxs-lookup"><span data-stu-id="3b4df-130">2.2</span></span>
- <span data-ttu-id="3b4df-131">2,0</span><span class="sxs-lookup"><span data-stu-id="3b4df-131">2.0</span></span>

## <a name="remove-preview-versions"></a><span data-ttu-id="3b4df-132">Usuń wersje w wersji zapoznawczej</span><span class="sxs-lookup"><span data-stu-id="3b4df-132">Remove preview versions</span></span>

[!INCLUDE [package-manager uninstall notice](./includes/linux-uninstall-preview-info.md)]

## <a name="how-to-install-other-versions"></a><span data-ttu-id="3b4df-133">Jak zainstalować inne wersje</span><span class="sxs-lookup"><span data-stu-id="3b4df-133">How to install other versions</span></span>

<span data-ttu-id="3b4df-134">Zapoznaj się z [dokumentacją firmy Red Hat dla platformy .NET](https://access.redhat.com/documentation/net/5.0/) , wykonując kroki wymagane do zainstalowania innych wersji platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="3b4df-134">Consult the [Red Hat documentation for .NET](https://access.redhat.com/documentation/net/5.0/) on the steps required to install other releases of .NET.</span></span>

## <a name="rhel-8-"></a><span data-ttu-id="3b4df-135">RHEL 8 ✔️</span><span class="sxs-lookup"><span data-stu-id="3b4df-135">RHEL 8 ✔️</span></span>

<span data-ttu-id="3b4df-136">Platforma .NET jest uwzględniona w repozytoriach AppStream dla RHEL 8.</span><span class="sxs-lookup"><span data-stu-id="3b4df-136">.NET is included in the AppStream repositories for RHEL 8.</span></span>

[!INCLUDE [linux-dnf-install-50](includes/linux-install-50-dnf.md)]

## <a name="rhel-7--net-50"></a><span data-ttu-id="3b4df-137">RHEL 7 ✔️ .NET 5,0</span><span class="sxs-lookup"><span data-stu-id="3b4df-137">RHEL 7 ✔️ .NET 5.0</span></span>

<span data-ttu-id="3b4df-138">Następujące polecenie instaluje `scl-utils` pakiet:</span><span class="sxs-lookup"><span data-stu-id="3b4df-138">The following command installs the `scl-utils` package:</span></span>

```bash
sudo yum install scl-utils
```

### <a name="install-the-sdk"></a><span data-ttu-id="3b4df-139">Instalacja zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="3b4df-139">Install the SDK</span></span>

<span data-ttu-id="3b4df-140">Zestaw SDK platformy .NET umożliwia tworzenie aplikacji przy użyciu platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="3b4df-140">The .NET SDK allows you to develop apps with .NET .</span></span> <span data-ttu-id="3b4df-141">W przypadku instalowania zestawu .NET SDK nie trzeba instalować odpowiedniego środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="3b4df-141">If you install the .NET SDK, you don't need to install the corresponding runtime.</span></span> <span data-ttu-id="3b4df-142">Aby zainstalować zestaw .NET SDK, uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="3b4df-142">To install .NET SDK, run the following commands:</span></span>

```bash
subscription-manager repos --enable=rhel-7-server-dotnet-rpms
yum install rh-dotnet50 -y
scl enable rh-dotnet50 bash
```

<span data-ttu-id="3b4df-143">Red Hat nie zaleca trwałego włączania `rh-dotnet50` , ponieważ może to mieć wpływ na inne programy.</span><span class="sxs-lookup"><span data-stu-id="3b4df-143">Red Hat does not recommend permanently enabling `rh-dotnet50` because it may affect other programs.</span></span> <span data-ttu-id="3b4df-144">Jeśli chcesz `rh-dotnet` trwale włączyć, Dodaj następujący wiersz do pliku _~/.bashrc._ .</span><span class="sxs-lookup"><span data-stu-id="3b4df-144">If you want to enable `rh-dotnet` permanently, add the following line to your _~/.bashrc_ file.</span></span>

```bash
source scl_source enable rh-dotnet50
```

### <a name="install-the-runtime"></a><span data-ttu-id="3b4df-145">Instalowanie środowiska uruchomieniowego</span><span class="sxs-lookup"><span data-stu-id="3b4df-145">Install the runtime</span></span>

<span data-ttu-id="3b4df-146">Środowisko uruchomieniowe platformy .NET umożliwia uruchamianie aplikacji utworzonych przy użyciu platformy .NET, które nie zawierały środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="3b4df-146">The .NET Runtime allows you to run apps that were made with .NET that didn't include the runtime.</span></span> <span data-ttu-id="3b4df-147">Poniższe polecenia instalują środowisko uruchomieniowe ASP.NET Core, które jest najbardziej zgodnym środowiskiem uruchomieniowym dla platformy .NET Core.</span><span class="sxs-lookup"><span data-stu-id="3b4df-147">The commands below install the ASP.NET Core Runtime, which is the most compatible runtime for .NET Core.</span></span> <span data-ttu-id="3b4df-148">W terminalu uruchom następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="3b4df-148">In your terminal, run the following commands.</span></span>

```bash
subscription-manager repos --enable=rhel-7-server-dotnet-rpms
yum install rh-dotnet50-aspnetcore-runtime-5.0 -y
scl enable rh-dotnet50 bash
```

<span data-ttu-id="3b4df-149">Red Hat nie zaleca trwałego włączania `rh-dotnet50` , ponieważ może to mieć wpływ na inne programy.</span><span class="sxs-lookup"><span data-stu-id="3b4df-149">Red Hat does not recommend permanently enabling `rh-dotnet50` because it may affect other programs.</span></span> <span data-ttu-id="3b4df-150">Jeśli chcesz `rh-dotnet50` trwale włączyć, Dodaj następujący wiersz do pliku _~/.bashrc._ .</span><span class="sxs-lookup"><span data-stu-id="3b4df-150">If you want to enable `rh-dotnet50` permanently, add the following line to your _~/.bashrc_ file.</span></span>

```bash
source scl_source enable rh-dotnet50
```

<span data-ttu-id="3b4df-151">Jako alternatywę dla środowiska uruchomieniowego ASP.NET Core można zainstalować środowisko uruchomieniowe platformy .NET, które nie obejmuje ASP.NET Core obsługi: Zastąp `rh-dotnet50-aspnetcore-runtime-5.0` w poleceniach powyżej `rh-dotnet50-dotnet-runtime-5.0` .</span><span class="sxs-lookup"><span data-stu-id="3b4df-151">As an alternative to the ASP.NET Core Runtime, you can install the .NET Runtime that doesn't include ASP.NET Core support: replace `rh-dotnet50-aspnetcore-runtime-5.0` in the commands above with `rh-dotnet50-dotnet-runtime-5.0`.</span></span>

## <a name="rhel-7--net-core-31"></a><span data-ttu-id="3b4df-152">RHEL 7 ✔️ .NET Core 3,1</span><span class="sxs-lookup"><span data-stu-id="3b4df-152">RHEL 7 ✔️ .NET Core 3.1</span></span>

[!INCLUDE [linux-prep-intro-generic](includes/linux-prep-intro-generic.md)]

<span data-ttu-id="3b4df-153">Następujące polecenie instaluje `scl-utils` pakiet:</span><span class="sxs-lookup"><span data-stu-id="3b4df-153">The following command installs the `scl-utils` package:</span></span>

```bash
sudo yum install scl-utils
```

### <a name="install-the-sdk"></a><span data-ttu-id="3b4df-154">Instalacja zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="3b4df-154">Install the SDK</span></span>

<span data-ttu-id="3b4df-155">Zestaw .NET Core SDK umożliwia tworzenie aplikacji przy użyciu platformy .NET Core.</span><span class="sxs-lookup"><span data-stu-id="3b4df-155">.NET Core SDK allows you to develop apps with .NET Core.</span></span> <span data-ttu-id="3b4df-156">W przypadku zainstalowania zestaw .NET Core SDK nie trzeba instalować odpowiedniego środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="3b4df-156">If you install .NET Core SDK, you don't need to install the corresponding runtime.</span></span> <span data-ttu-id="3b4df-157">Aby zainstalować zestaw .NET Core SDK, uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="3b4df-157">To install .NET Core SDK, run the following commands:</span></span>

```bash
subscription-manager repos --enable=rhel-7-server-dotnet-rpms
yum install rh-dotnet31 -y
scl enable rh-dotnet31 bash
```

<span data-ttu-id="3b4df-158">Red Hat nie zaleca trwałego włączania `rh-dotnet31` , ponieważ może to mieć wpływ na inne programy.</span><span class="sxs-lookup"><span data-stu-id="3b4df-158">Red Hat does not recommend permanently enabling `rh-dotnet31` because it may affect other programs.</span></span> <span data-ttu-id="3b4df-159">Program zawiera na przykład `rh-dotnet31` wersję `libcurl` , która różni się od bazowej wersji RHEL.</span><span class="sxs-lookup"><span data-stu-id="3b4df-159">For example, `rh-dotnet31` includes a version of `libcurl` that differs from the base RHEL version.</span></span> <span data-ttu-id="3b4df-160">Może to prowadzić do problemów z programami, które nie oczekują innej wersji programu `libcurl` .</span><span class="sxs-lookup"><span data-stu-id="3b4df-160">This may lead to issues in programs that do not expect a different version of `libcurl`.</span></span> <span data-ttu-id="3b4df-161">Jeśli chcesz `rh-dotnet` trwale włączyć, Dodaj następujący wiersz do pliku _~/.bashrc._ .</span><span class="sxs-lookup"><span data-stu-id="3b4df-161">If you want to enable `rh-dotnet` permanently, add the following line to your _~/.bashrc_ file.</span></span>

```bash
source scl_source enable rh-dotnet31
```

### <a name="install-the-runtime"></a><span data-ttu-id="3b4df-162">Instalowanie środowiska uruchomieniowego</span><span class="sxs-lookup"><span data-stu-id="3b4df-162">Install the runtime</span></span>

<span data-ttu-id="3b4df-163">Środowisko uruchomieniowe programu .NET Core umożliwia uruchamianie aplikacji, które zostały wykonane przy użyciu platformy .NET Core, które nie zawierały środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="3b4df-163">The .NET Core Runtime allows you to run apps that were made with .NET Core that didn't include the runtime.</span></span> <span data-ttu-id="3b4df-164">Poniższe polecenia instalują środowisko uruchomieniowe ASP.NET Core, które jest najbardziej zgodnym środowiskiem uruchomieniowym dla platformy .NET Core.</span><span class="sxs-lookup"><span data-stu-id="3b4df-164">The commands below install the ASP.NET Core Runtime, which is the most compatible runtime for .NET Core.</span></span> <span data-ttu-id="3b4df-165">W terminalu uruchom następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="3b4df-165">In your terminal, run the following commands.</span></span>

```bash
subscription-manager repos --enable=rhel-7-server-dotnet-rpms
yum install rh-dotnet31-aspnetcore-runtime-3.1 -y
scl enable rh-dotnet31 bash
```

<span data-ttu-id="3b4df-166">Red Hat nie zaleca trwałego włączania `rh-dotnet31` , ponieważ może to mieć wpływ na inne programy.</span><span class="sxs-lookup"><span data-stu-id="3b4df-166">Red Hat does not recommend permanently enabling `rh-dotnet31` because it may affect other programs.</span></span> <span data-ttu-id="3b4df-167">Program zawiera na przykład `rh-dotnet31` wersję `libcurl` , która różni się od bazowej wersji RHEL.</span><span class="sxs-lookup"><span data-stu-id="3b4df-167">For example, `rh-dotnet31` includes a version of `libcurl` that differs from the base RHEL version.</span></span> <span data-ttu-id="3b4df-168">Może to prowadzić do problemów z programami, które nie oczekują innej wersji programu `libcurl` .</span><span class="sxs-lookup"><span data-stu-id="3b4df-168">This may lead to issues in programs that do not expect a different version of `libcurl`.</span></span> <span data-ttu-id="3b4df-169">Jeśli chcesz `rh-dotnet31` trwale włączyć, Dodaj następujący wiersz do pliku _~/.bashrc._ .</span><span class="sxs-lookup"><span data-stu-id="3b4df-169">If you want to enable `rh-dotnet31` permanently, add the following line to your _~/.bashrc_ file.</span></span>

```bash
source scl_source enable rh-dotnet31
```

<span data-ttu-id="3b4df-170">Jako alternatywę dla środowiska uruchomieniowego ASP.NET Core można zainstalować środowisko uruchomieniowe programu .NET Core, które nie obejmuje ASP.NET Core Support: Zastąp `rh-dotnet31-aspnetcore-runtime-3.1` w poleceniach powyżej `rh-dotnet31-dotnet-runtime-3.1` .</span><span class="sxs-lookup"><span data-stu-id="3b4df-170">As an alternative to the ASP.NET Core Runtime, you can install the .NET Core Runtime that doesn't include ASP.NET Core support: replace `rh-dotnet31-aspnetcore-runtime-3.1` in the commands above with `rh-dotnet31-dotnet-runtime-3.1`.</span></span>

## <a name="snap"></a><span data-ttu-id="3b4df-171">Przystawki</span><span class="sxs-lookup"><span data-stu-id="3b4df-171">Snap</span></span>

[!INCLUDE [linux-install-snap](includes/linux-install-snap.md)]

## <a name="dependencies"></a><span data-ttu-id="3b4df-172">Zależności</span><span class="sxs-lookup"><span data-stu-id="3b4df-172">Dependencies</span></span>

[!INCLUDE [linux-rpm-install-dependencies](includes/linux-rpm-install-dependencies.md)]

## <a name="scripted-install"></a><span data-ttu-id="3b4df-173">Instalacja z skryptami</span><span class="sxs-lookup"><span data-stu-id="3b4df-173">Scripted install</span></span>

[!INCLUDE [linux-install-scripted](includes/linux-install-scripted.md)]

## <a name="manual-install"></a><span data-ttu-id="3b4df-174">Instalacja ręczna</span><span class="sxs-lookup"><span data-stu-id="3b4df-174">Manual install</span></span>

[!INCLUDE [linux-install-manual](includes/linux-install-manual.md)]

## <a name="next-steps"></a><span data-ttu-id="3b4df-175">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3b4df-175">Next steps</span></span>

- [<span data-ttu-id="3b4df-176">Samouczek: Tworzenie aplikacji konsolowej za pomocą zestawu .NET SDK przy użyciu Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="3b4df-176">Tutorial: Create a console application with .NET SDK using Visual Studio Code</span></span>](../tutorials/with-visual-studio-code.md)
