---
title: Określanie, które wersje programu .NET Framework są zainstalowane
description: Użyj kodu, regedit.exe lub programu PowerShell, aby wykryć, które wersje .NET Framework są zainstalowane na komputerze, badając rejestr systemu Windows.
ms.date: 12/04/2020
dev_langs:
- csharp
- vb
helpviewer_keywords:
- versions, determining for .NET Framework
- .NET Framework, determining installed versions
ms.assetid: 40a67826-e4df-4f59-a651-d9eb0fdc755d
ms.openlocfilehash: a219514fafdcb17db259e089afa8318dbab24811
ms.sourcegitcommit: 45c7148f2483db2501c1aa696ab6ed2ed8cb71b2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/08/2020
ms.locfileid: "96851832"
---
# <a name="how-to-determine-which-net-framework-versions-are-installed"></a><span data-ttu-id="32c4d-103">Instrukcje: Określanie, które wersje .NET Framework są zainstalowane</span><span class="sxs-lookup"><span data-stu-id="32c4d-103">How to: Determine which .NET Framework versions are installed</span></span>

<span data-ttu-id="32c4d-104">Użytkownicy mogą [instalować](../install/index.md) i uruchamiać wiele wersji .NET Framework na swoich komputerach.</span><span class="sxs-lookup"><span data-stu-id="32c4d-104">Users can [install](../install/index.md) and run multiple versions of .NET Framework on their computers.</span></span> <span data-ttu-id="32c4d-105">Podczas opracowywania lub wdrażania aplikacji może być konieczne, aby wiedzieć, które wersje .NET Framework są zainstalowane na komputerze użytkownika.</span><span class="sxs-lookup"><span data-stu-id="32c4d-105">When you develop or deploy your app, you might need to know which .NET Framework versions are installed on the user's computer.</span></span> <span data-ttu-id="32c4d-106">Rejestr zawiera listę wersji .NET Framework zainstalowanych na komputerze.</span><span class="sxs-lookup"><span data-stu-id="32c4d-106">The registry contains a list of the versions of .NET Framework installed on the computer.</span></span>

> [!NOTE]
> <span data-ttu-id="32c4d-107">Ten artykuł dotyczy .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="32c4d-107">This article is specific to .NET Framework.</span></span> <span data-ttu-id="32c4d-108">Aby określić, które zestawy SDK i środowiska uruchomieniowe platformy .NET Core i .NET 5 są zainstalowane, zobacz [Jak sprawdzić, czy program .NET jest już zainstalowany](../../core/install/how-to-detect-installed-versions.md).</span><span class="sxs-lookup"><span data-stu-id="32c4d-108">To determine which .NET Core and .NET 5+ SDKs and runtimes are installed, see [How to check that .NET is already installed](../../core/install/how-to-detect-installed-versions.md).</span></span>

<span data-ttu-id="32c4d-109">.NET Framework składa się z dwóch głównych składników, które są osobno dla wersji:</span><span class="sxs-lookup"><span data-stu-id="32c4d-109">.NET Framework consists of two main components, which are versioned separately:</span></span>

- <span data-ttu-id="32c4d-110">Zestaw zestawów, które są kolekcjami typów i zasobów zapewniających funkcje dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="32c4d-110">A set of assemblies, which are collections of types and resources that provide the functionality for your apps.</span></span> <span data-ttu-id="32c4d-111">.NET Framework i zestawy mają ten sam numer wersji.</span><span class="sxs-lookup"><span data-stu-id="32c4d-111">.NET Framework and the assemblies share the same version number.</span></span> <span data-ttu-id="32c4d-112">Na przykład .NET Framework wersje obejmują 4,5, 4.6.1 i 4.7.2.</span><span class="sxs-lookup"><span data-stu-id="32c4d-112">For example, .NET Framework versions include 4.5, 4.6.1, and 4.7.2.</span></span>

- <span data-ttu-id="32c4d-113">Środowisko uruchomieniowe języka wspólnego (CLR), które zarządza kodem aplikacji i go wykonuje.</span><span class="sxs-lookup"><span data-stu-id="32c4d-113">The common language runtime (CLR), which manages and executes your app's code.</span></span> <span data-ttu-id="32c4d-114">Jedna wersja środowiska CLR obsługuje zazwyczaj wiele wersji .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="32c4d-114">A single CLR version typically supports multiple .NET Framework versions.</span></span> <span data-ttu-id="32c4d-115">Na przykład środowisko CLR w wersji 4.0.30319. *XXXXX* , gdzie *XXXXX* jest mniejszy niż 42000, obsługuje .NET Framework wersji 4 do 4.5.2.</span><span class="sxs-lookup"><span data-stu-id="32c4d-115">For example, CLR version 4.0.30319.*xxxxx* where *xxxxx* is less than 42000, supports .NET Framework versions 4 through 4.5.2.</span></span> <span data-ttu-id="32c4d-116">Wersja środowiska CLR o wartości większej lub równej 4.0.30319.42000 obsługuje wersje .NET Framework począwszy od .NET Framework 4,6.</span><span class="sxs-lookup"><span data-stu-id="32c4d-116">CLR version greater than or equal to 4.0.30319.42000 supports .NET Framework versions starting with .NET Framework 4.6.</span></span>

<span data-ttu-id="32c4d-117">Narzędzia obsługiwane przez społeczność są dostępne, aby pomóc w wykrywaniu, które wersje .NET Framework są zainstalowane:</span><span class="sxs-lookup"><span data-stu-id="32c4d-117">Community-maintained tools are available to help detect which .NET Framework versions are installed:</span></span>

- [https://github.com/jmalarcon/DotNetVersions](https://github.com/jmalarcon/DotNetVersions)

  <span data-ttu-id="32c4d-118">Narzędzie wiersza polecenia .NET Framework 2,0.</span><span class="sxs-lookup"><span data-stu-id="32c4d-118">A .NET Framework 2.0 command-line tool.</span></span>

- [https://github.com/EliteLoser/DotNetVersionLister](https://github.com/EliteLoser/DotNetVersionLister)

  <span data-ttu-id="32c4d-119">Moduł programu PowerShell 2,0.</span><span class="sxs-lookup"><span data-stu-id="32c4d-119">A PowerShell 2.0 module.</span></span>

<span data-ttu-id="32c4d-120">Aby uzyskać informacje dotyczące wykrywania zainstalowanych aktualizacji dla każdej wersji .NET Framework, zobacz [How to: Określanie, które aktualizacje .NET Framework są zainstalowane](how-to-determine-which-net-framework-updates-are-installed.md).</span><span class="sxs-lookup"><span data-stu-id="32c4d-120">For information about detecting the installed updates for each version of .NET Framework, see [How to: Determine which .NET Framework updates are installed](how-to-determine-which-net-framework-updates-are-installed.md).</span></span>

## <a name="determine-which-net-implementation-and-version-an-app-is-running-on"></a><span data-ttu-id="32c4d-121">Określanie implementacji i wersji platformy .NET, na której działa aplikacja</span><span class="sxs-lookup"><span data-stu-id="32c4d-121">Determine which .NET implementation and version an app is running on</span></span>

<span data-ttu-id="32c4d-122">Możesz użyć właściwości, <xref:System.Runtime.InteropServices.RuntimeInformation.FrameworkDescription?displayProperty=nameWithType> Aby wykonać zapytanie dotyczące implementacji i wersji platformy .NET, na której działa aplikacja.</span><span class="sxs-lookup"><span data-stu-id="32c4d-122">You can use the <xref:System.Runtime.InteropServices.RuntimeInformation.FrameworkDescription?displayProperty=nameWithType> property to query for which .NET implementation and version your app is running on.</span></span> <span data-ttu-id="32c4d-123">Jeśli aplikacja działa na .NET Framework, dane wyjściowe będą podobne do:</span><span class="sxs-lookup"><span data-stu-id="32c4d-123">If the app is running on .NET Framework, the output will be similar to:</span></span>

```output
.NET Framework 4.8.4250.0
```

<span data-ttu-id="32c4d-124">Porównując, jeśli aplikacja działa w środowisku .NET Core lub .NET 5 +, dane wyjściowe będą podobne do:</span><span class="sxs-lookup"><span data-stu-id="32c4d-124">By comparison, if the app is running on .NET Core or .NET 5+, the output will be similar to:</span></span>

```output
.NET Core 3.1.9
.NET 5.0.0
```

## <a name="detect-net-framework-45-and-later-versions"></a><span data-ttu-id="32c4d-125">Wykryj .NET Framework 4,5 i nowsze wersje</span><span class="sxs-lookup"><span data-stu-id="32c4d-125">Detect .NET Framework 4.5 and later versions</span></span>

<span data-ttu-id="32c4d-126">Wersja .NET Framework (4,5 lub nowsza) zainstalowana na komputerze jest wymieniona w rejestrze w **HKEY_LOCAL_MACHINE \\ oprogramowania \\ Microsoft \\ NET Framework Setup \\ NDP \\ v4 \\**.</span><span class="sxs-lookup"><span data-stu-id="32c4d-126">The version of .NET Framework (4.5 and later) installed on a machine is listed in the registry at **HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\NET Framework Setup\\NDP\\v4\\Full**.</span></span> <span data-ttu-id="32c4d-127">Jeśli brakuje **pełnego** podklucza, to .NET Framework 4,5 lub nowsze nie są zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="32c4d-127">If the **Full** subkey is missing, then .NET Framework 4.5 or above isn't installed.</span></span>

> [!NOTE]
> <span data-ttu-id="32c4d-128">Podklucz **instalacji programu .NET Framework** w ścieżce rejestru *nie* zaczyna się od kropki.</span><span class="sxs-lookup"><span data-stu-id="32c4d-128">The **NET Framework Setup** subkey in the registry path does *not* begin with a period.</span></span>

<span data-ttu-id="32c4d-129">Wartość REG_DWORD **wydania** w rejestrze reprezentuje wersję zainstalowanej .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="32c4d-129">The **Release** REG_DWORD value in the registry represents the version of .NET Framework installed.</span></span>

<a name="version_table"></a>

| <span data-ttu-id="32c4d-130">Wersja programu .NET Framework</span><span class="sxs-lookup"><span data-stu-id="32c4d-130">.NET Framework version</span></span> | <span data-ttu-id="32c4d-131">Wartość **wydania**</span><span class="sxs-lookup"><span data-stu-id="32c4d-131">Value of **Release**</span></span> |
| ---------------------- | -------------------------- |
| <span data-ttu-id="32c4d-132">.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="32c4d-132">.NET Framework 4.5</span></span>     | <span data-ttu-id="32c4d-133">Wszystkie systemy operacyjne Windows: 378389</span><span class="sxs-lookup"><span data-stu-id="32c4d-133">All Windows operating systems: 378389</span></span> |
| <span data-ttu-id="32c4d-134">.NET Framework 4.5.1</span><span class="sxs-lookup"><span data-stu-id="32c4d-134">.NET Framework 4.5.1</span></span>   | <span data-ttu-id="32c4d-135">W systemach Windows 8.1 i Windows Server 2012 R2:378675</span><span class="sxs-lookup"><span data-stu-id="32c4d-135">On Windows 8.1 and Windows Server 2012 R2: 378675</span></span><br /><span data-ttu-id="32c4d-136">We wszystkich innych systemach operacyjnych Windows: 378758</span><span class="sxs-lookup"><span data-stu-id="32c4d-136">On all other Windows operating systems: 378758</span></span> |
| <span data-ttu-id="32c4d-137">.NET Framework 4.5.2</span><span class="sxs-lookup"><span data-stu-id="32c4d-137">.NET Framework 4.5.2</span></span>   | <span data-ttu-id="32c4d-138">Wszystkie systemy operacyjne Windows: 379893</span><span class="sxs-lookup"><span data-stu-id="32c4d-138">All Windows operating systems: 379893</span></span> |
| <span data-ttu-id="32c4d-139">Program .NET Framework 4.6</span><span class="sxs-lookup"><span data-stu-id="32c4d-139">.NET Framework 4.6</span></span>     | <span data-ttu-id="32c4d-140">W systemie Windows 10:393295</span><span class="sxs-lookup"><span data-stu-id="32c4d-140">On Windows 10: 393295</span></span><br /><span data-ttu-id="32c4d-141">We wszystkich innych systemach operacyjnych Windows: 393297</span><span class="sxs-lookup"><span data-stu-id="32c4d-141">On all other Windows operating systems: 393297</span></span> |
| <span data-ttu-id="32c4d-142">.NET Framework 4.6.1</span><span class="sxs-lookup"><span data-stu-id="32c4d-142">.NET Framework 4.6.1</span></span>   | <span data-ttu-id="32c4d-143">W systemach aktualizacji systemu Windows 10 listopad: 394254</span><span class="sxs-lookup"><span data-stu-id="32c4d-143">On Windows 10 November Update systems: 394254</span></span><br /><span data-ttu-id="32c4d-144">We wszystkich innych systemach operacyjnych Windows (w tym Windows 10): 394271</span><span class="sxs-lookup"><span data-stu-id="32c4d-144">On all other Windows operating systems (including Windows 10): 394271</span></span> |
| <span data-ttu-id="32c4d-145">.NET Framework 4.6.2</span><span class="sxs-lookup"><span data-stu-id="32c4d-145">.NET Framework 4.6.2</span></span>   | <span data-ttu-id="32c4d-146">W rocznicowej aktualizacji systemu Windows 10 i Windows Server 2016:394802</span><span class="sxs-lookup"><span data-stu-id="32c4d-146">On Windows 10 Anniversary Update and Windows Server 2016: 394802</span></span><br /><span data-ttu-id="32c4d-147">Wszystkie inne systemy operacyjne Windows (w tym inne systemy operacyjne Windows 10): 394806</span><span class="sxs-lookup"><span data-stu-id="32c4d-147">On all other Windows operating systems (including other Windows 10 operating systems): 394806</span></span> |
| <span data-ttu-id="32c4d-148"> .NET Framework 4.7</span><span class="sxs-lookup"><span data-stu-id="32c4d-148">.NET Framework 4.7</span></span>     | <span data-ttu-id="32c4d-149">Aktualizacja systemu Windows 10 dla twórców: 460798</span><span class="sxs-lookup"><span data-stu-id="32c4d-149">On Windows 10 Creators Update: 460798</span></span><br /><span data-ttu-id="32c4d-150">Wszystkie inne systemy operacyjne Windows (w tym inne systemy operacyjne Windows 10): 460805</span><span class="sxs-lookup"><span data-stu-id="32c4d-150">On all other Windows operating systems (including other Windows 10 operating systems): 460805</span></span> |
| <span data-ttu-id="32c4d-151">.NET Framework 4.7.1</span><span class="sxs-lookup"><span data-stu-id="32c4d-151">.NET Framework 4.7.1</span></span>   | <span data-ttu-id="32c4d-152">W przypadku aktualizacji systemu Windows 10 dla twórców i systemu Windows Server w wersji 1709:461308</span><span class="sxs-lookup"><span data-stu-id="32c4d-152">On Windows 10 Fall Creators Update and Windows Server, version 1709: 461308</span></span><br/><span data-ttu-id="32c4d-153">Wszystkie inne systemy operacyjne Windows (w tym inne systemy operacyjne Windows 10): 461310</span><span class="sxs-lookup"><span data-stu-id="32c4d-153">On all other Windows operating systems (including other Windows 10 operating systems): 461310</span></span> |
| <span data-ttu-id="32c4d-154"> .NET Framework 4.7.2</span><span class="sxs-lookup"><span data-stu-id="32c4d-154">.NET Framework 4.7.2</span></span>   | <span data-ttu-id="32c4d-155">W systemie Windows 10 kwiecień 2018 Update i Windows Server w wersji 1803:461808</span><span class="sxs-lookup"><span data-stu-id="32c4d-155">On Windows 10 April 2018 Update and Windows Server, version 1803: 461808</span></span><br/><span data-ttu-id="32c4d-156">We wszystkich systemach operacyjnych Windows innych niż Windows 10 kwiecień 2018 Update i Windows Server w wersji 1803:461814</span><span class="sxs-lookup"><span data-stu-id="32c4d-156">On all Windows operating systems other than Windows 10 April 2018 Update and Windows Server, version 1803: 461814</span></span> |
| <span data-ttu-id="32c4d-157"> .NET Framework 4.8</span><span class="sxs-lookup"><span data-stu-id="32c4d-157">.NET Framework 4.8</span></span>     | <span data-ttu-id="32c4d-158">W systemie Windows 10 maja 2019 Update i aktualizacja Windows 10 listopad 2019:528040</span><span class="sxs-lookup"><span data-stu-id="32c4d-158">On Windows 10 May 2019 Update and Windows 10 November 2019 Update: 528040</span></span><br/><span data-ttu-id="32c4d-159">Aktualizacje systemu Windows 10 maja 2020 Update i Windows 10 października 2020:528372</span><span class="sxs-lookup"><span data-stu-id="32c4d-159">On Windows 10 May 2020 Update and Windows 10 October 2020 Update: 528372</span></span><br/><span data-ttu-id="32c4d-160">Wszystkie inne systemy operacyjne Windows (w tym inne systemy operacyjne Windows 10): 528049</span><span class="sxs-lookup"><span data-stu-id="32c4d-160">On all other Windows operating systems (including other Windows 10 operating systems): 528049</span></span> |

### <a name="minimum-version"></a><span data-ttu-id="32c4d-161">Minimalna wersja</span><span class="sxs-lookup"><span data-stu-id="32c4d-161">Minimum version</span></span>

<span data-ttu-id="32c4d-162">Aby określić, czy jest dostępna *minimalna* wersja .NET Framework, sprawdź, czy wartość **wydania** REG_DWORD, która jest większa lub równa odpowiadającej wartości wymienionej w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="32c4d-162">To determine whether a *minimum* version of .NET Framework is present, check for a **Release** REG_DWORD value that's greater than or equal to the corresponding value listed in the following table.</span></span> <span data-ttu-id="32c4d-163">Na przykład, jeśli aplikacja działa w .NET Framework 4,8 lub nowszej wersji, należy sprawdzić, czy w **wersji** REG_DWORD wartość jest *większa niż lub równa* 528040.</span><span class="sxs-lookup"><span data-stu-id="32c4d-163">For example, if your application runs under .NET Framework 4.8 or a later version, test for a **Release** REG_DWORD value that's *greater than or equal to* 528040.</span></span>

| <span data-ttu-id="32c4d-164">Wersja programu .NET Framework</span><span class="sxs-lookup"><span data-stu-id="32c4d-164">.NET Framework version</span></span> | <span data-ttu-id="32c4d-165">Wartość minimalna</span><span class="sxs-lookup"><span data-stu-id="32c4d-165">Minimum value</span></span> |
| ---------------------- | ------------- |
| <span data-ttu-id="32c4d-166">.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="32c4d-166">.NET Framework 4.5</span></span>     | <span data-ttu-id="32c4d-167">378389</span><span class="sxs-lookup"><span data-stu-id="32c4d-167">378389</span></span> |
| <span data-ttu-id="32c4d-168">.NET Framework 4.5.1</span><span class="sxs-lookup"><span data-stu-id="32c4d-168">.NET Framework 4.5.1</span></span>   | <span data-ttu-id="32c4d-169">378675</span><span class="sxs-lookup"><span data-stu-id="32c4d-169">378675</span></span> |
| <span data-ttu-id="32c4d-170">.NET Framework 4.5.2</span><span class="sxs-lookup"><span data-stu-id="32c4d-170">.NET Framework 4.5.2</span></span>   | <span data-ttu-id="32c4d-171">379893</span><span class="sxs-lookup"><span data-stu-id="32c4d-171">379893</span></span> |
| <span data-ttu-id="32c4d-172">Program .NET Framework 4.6</span><span class="sxs-lookup"><span data-stu-id="32c4d-172">.NET Framework 4.6</span></span>     | <span data-ttu-id="32c4d-173">393295</span><span class="sxs-lookup"><span data-stu-id="32c4d-173">393295</span></span> |
| <span data-ttu-id="32c4d-174">.NET Framework 4.6.1</span><span class="sxs-lookup"><span data-stu-id="32c4d-174">.NET Framework 4.6.1</span></span>   | <span data-ttu-id="32c4d-175">394254</span><span class="sxs-lookup"><span data-stu-id="32c4d-175">394254</span></span> |
| <span data-ttu-id="32c4d-176">.NET Framework 4.6.2</span><span class="sxs-lookup"><span data-stu-id="32c4d-176">.NET Framework 4.6.2</span></span>   | <span data-ttu-id="32c4d-177">394802</span><span class="sxs-lookup"><span data-stu-id="32c4d-177">394802</span></span> |
| <span data-ttu-id="32c4d-178"> .NET Framework 4.7</span><span class="sxs-lookup"><span data-stu-id="32c4d-178">.NET Framework 4.7</span></span>     | <span data-ttu-id="32c4d-179">460798</span><span class="sxs-lookup"><span data-stu-id="32c4d-179">460798</span></span> |
| <span data-ttu-id="32c4d-180">.NET Framework 4.7.1</span><span class="sxs-lookup"><span data-stu-id="32c4d-180">.NET Framework 4.7.1</span></span>   | <span data-ttu-id="32c4d-181">461308</span><span class="sxs-lookup"><span data-stu-id="32c4d-181">461308</span></span> |
| <span data-ttu-id="32c4d-182"> .NET Framework 4.7.2</span><span class="sxs-lookup"><span data-stu-id="32c4d-182">.NET Framework 4.7.2</span></span>   | <span data-ttu-id="32c4d-183">461808</span><span class="sxs-lookup"><span data-stu-id="32c4d-183">461808</span></span> |
| <span data-ttu-id="32c4d-184"> .NET Framework 4.8</span><span class="sxs-lookup"><span data-stu-id="32c4d-184">.NET Framework 4.8</span></span>     | <span data-ttu-id="32c4d-185">528040</span><span class="sxs-lookup"><span data-stu-id="32c4d-185">528040</span></span> |

### <a name="use-registry-editor"></a><span data-ttu-id="32c4d-186">Korzystanie z edytora rejestru</span><span class="sxs-lookup"><span data-stu-id="32c4d-186">Use Registry Editor</span></span>

1. <span data-ttu-id="32c4d-187">Z menu **Start** wybierz polecenie **Uruchom**, wpisz polecenie *regedit*, a następnie wybierz przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="32c4d-187">From the **Start** menu, choose **Run**, enter *regedit*, and then select **OK**.</span></span>

   <span data-ttu-id="32c4d-188">(Musisz mieć poświadczenia administracyjne, aby uruchomić regedit).</span><span class="sxs-lookup"><span data-stu-id="32c4d-188">(You must have administrative credentials to run regedit.)</span></span>

1. <span data-ttu-id="32c4d-189">W Edytorze rejestru Otwórz następujący podklucz: **HKEY_LOCAL_MACHINE \\ Software \\ Microsoft \\ .NET Framework Setup \\ NDP \\ v4 \\**.</span><span class="sxs-lookup"><span data-stu-id="32c4d-189">In the Registry Editor, open the following subkey: **HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\NET Framework Setup\\NDP\\v4\\Full**.</span></span> <span data-ttu-id="32c4d-190">Jeśli **pełny** podklucz nie jest obecny, nie masz zainstalowanego .NET Framework 4,5 lub nowszego.</span><span class="sxs-lookup"><span data-stu-id="32c4d-190">If the **Full** subkey isn't present, then you don't have .NET Framework 4.5 or later installed.</span></span>

1. <span data-ttu-id="32c4d-191">Sprawdź, czy REG_DWORD wpis o nazwie **Release**.</span><span class="sxs-lookup"><span data-stu-id="32c4d-191">Check for a REG_DWORD entry named **Release**.</span></span> <span data-ttu-id="32c4d-192">Jeśli istnieje, jest zainstalowana .NET Framework 4,5 lub nowsza.</span><span class="sxs-lookup"><span data-stu-id="32c4d-192">If it exists, then you have .NET Framework 4.5 or later installed.</span></span> <span data-ttu-id="32c4d-193">Jego wartość odnosi się do określonej wersji .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="32c4d-193">Its value corresponds to a particular version of .NET Framework.</span></span> <span data-ttu-id="32c4d-194">Na przykład, wartość wpisu **zlecenia** to 528040, który jest kluczem wydania dla .NET Framework 4,8.</span><span class="sxs-lookup"><span data-stu-id="32c4d-194">In the following figure, for example, the value of the **Release** entry is 528040, which is the release key for .NET Framework 4.8.</span></span>

   ![Wpis rejestru dla .NET Framework 4,5](./media/clr-installdir.png )

### <a name="use-powershell-to-check-for-a-minimum-version"></a><span data-ttu-id="32c4d-196">Sprawdzanie minimalnej wersji przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="32c4d-196">Use PowerShell to check for a minimum version</span></span>

<span data-ttu-id="32c4d-197">Użyj poleceń programu PowerShell, aby sprawdzić wartość wpisu **Release** w **HKEY_LOCAL_MACHINE \\ oprogramowania \\ Microsoft \\ NET Framework Setup \\ NDP \\ v4 \\ Full** podklucza.</span><span class="sxs-lookup"><span data-stu-id="32c4d-197">Use PowerShell commands to check the value of the **Release** entry of the **HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\NET Framework Setup\\NDP\\v4\\Full** subkey.</span></span>

<span data-ttu-id="32c4d-198">W poniższych przykładach Sprawdź wartość wpisu **Zwolnij** , aby określić, czy .NET Framework 4.6.2 czy nowsza.</span><span class="sxs-lookup"><span data-stu-id="32c4d-198">The following examples check the value of the **Release** entry to determine whether .NET Framework 4.6.2 or later is installed.</span></span> <span data-ttu-id="32c4d-199">Ten kod zwraca `True` , jeśli jest zainstalowany i `False` w przeciwnym razie.</span><span class="sxs-lookup"><span data-stu-id="32c4d-199">This code returns `True` if it's installed and `False` otherwise.</span></span>

```powershell
(Get-ItemProperty "HKLM:\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full").Release -ge 394802
```

### <a name="query-the-registry-using-code"></a><span data-ttu-id="32c4d-200">Tworzenie zapytań dotyczących rejestru przy użyciu kodu</span><span class="sxs-lookup"><span data-stu-id="32c4d-200">Query the registry using code</span></span>

01. <span data-ttu-id="32c4d-201">Użyj <xref:Microsoft.Win32.RegistryKey.OpenBaseKey%2A?displayProperty=nameWithType> metod i, <xref:Microsoft.Win32.RegistryKey.OpenSubKey%2A?displayProperty=nameWithType> Aby uzyskać dostęp do **HKEY_LOCAL_MACHINE \\ oprogramowania \\ Microsoft \\ .NET Framework Setup \\ NDP \\ v4 \\** w rejestrze systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="32c4d-201">Use the <xref:Microsoft.Win32.RegistryKey.OpenBaseKey%2A?displayProperty=nameWithType> and <xref:Microsoft.Win32.RegistryKey.OpenSubKey%2A?displayProperty=nameWithType> methods to access the **HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\NET Framework Setup\\NDP\\v4\\Full** subkey in the Windows registry.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="32c4d-202">Jeśli uruchomiona aplikacja jest 32-bitowa i działa w 64-bitowym systemie Windows, ścieżki rejestru będą inne niż wymienione wcześniej.</span><span class="sxs-lookup"><span data-stu-id="32c4d-202">If the app you're running is 32-bit and running in 64-bit Windows, the registry paths will be different than previously listed.</span></span> <span data-ttu-id="32c4d-203">Rejestr 64-bitowy jest dostępny HKEY_LOCAL_MACHINE w podkluczu **\\ \\ Wow6432Node \\ oprogramowania** .</span><span class="sxs-lookup"><span data-stu-id="32c4d-203">The 64-bit registry is available in the **HKEY_LOCAL_MACHINE\\SOFTWARE\\Wow6432Node\\** subkey.</span></span> <span data-ttu-id="32c4d-204">Na przykład podklucz rejestru dla .NET Framework 4,5 to **HKEY_LOCAL_MACHINE \\ Software \\ Wow6432Node \\ Microsoft \\ .NET Framework Setup \\ NDP \\ v4 \\ Full**.</span><span class="sxs-lookup"><span data-stu-id="32c4d-204">For example, the registry subkey for .NET Framework 4.5 is **HKEY_LOCAL_MACHINE\\SOFTWARE\\Wow6432Node\\Microsoft\\NET Framework Setup\\NDP\\v4\\Full**.</span></span>

01. <span data-ttu-id="32c4d-205">Sprawdź wartość REG_DWORD **wydania** , aby określić zainstalowaną wersję.</span><span class="sxs-lookup"><span data-stu-id="32c4d-205">Check the **Release** REG_DWORD value to determine the installed version.</span></span> <span data-ttu-id="32c4d-206">Aby można było przesłać dalej, sprawdź, czy wartość jest większa niż lub równa wartości wymienionej w [tabeli wersji .NET Framework](#version_table).</span><span class="sxs-lookup"><span data-stu-id="32c4d-206">To be forward-compatible, check for a value greater than or equal to the value listed in the [.NET Framework version table](#version_table).</span></span>

<span data-ttu-id="32c4d-207">Poniższy przykład sprawdza wartość wpisu **Release** w rejestrze, aby znaleźć zainstalowane wersje .NET Framework 4.5-4.8:</span><span class="sxs-lookup"><span data-stu-id="32c4d-207">The following example checks the value of the **Release** entry in the registry to find the versions of .NET Framework 4.5-4.8 that are installed:</span></span>

:::code language="csharp" source="snippets/csharp/versions-installed.cs" id="2":::

:::code language="vb" source="snippets/visual-basic/versions-installed.vb" id="2":::

<span data-ttu-id="32c4d-208">Przykład wyświetla dane wyjściowe podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="32c4d-208">The example displays output like the following:</span></span>

```output
.NET Framework Version: 4.6.1
```

<span data-ttu-id="32c4d-209">Ten przykład jest zgodny z zalecaną metodą sprawdzania wersji:</span><span class="sxs-lookup"><span data-stu-id="32c4d-209">This example follows the recommended practice for version checking:</span></span>

- <span data-ttu-id="32c4d-210">Sprawdza, czy wartość wpisu **wydania** jest *większa niż lub równa* wartości znanych kluczy wydania.</span><span class="sxs-lookup"><span data-stu-id="32c4d-210">It checks whether the value of the **Release** entry is *greater than or equal to* the value of the known release keys.</span></span>
- <span data-ttu-id="32c4d-211">Sprawdza w kolejności od najnowszej wersji do najwcześniejszej wersji.</span><span class="sxs-lookup"><span data-stu-id="32c4d-211">It checks in order from most recent version to earliest version.</span></span>

## <a name="detect-net-framework-10-through-40"></a><span data-ttu-id="32c4d-212">Wykryj .NET Framework 1,0 do 4,0</span><span class="sxs-lookup"><span data-stu-id="32c4d-212">Detect .NET Framework 1.0 through 4.0</span></span>

<span data-ttu-id="32c4d-213">Każda wersja .NET Framework od 1,1 do 4,0 jest wyświetlana jako podklucz w **HKEY_LOCAL_MACHINE \\ oprogramowaniu \\ Microsoft \\ .NET Framework Setup \\ NDP**.</span><span class="sxs-lookup"><span data-stu-id="32c4d-213">Each version of .NET Framework from 1.1 to 4.0 is listed as a subkey at **HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\NET Framework Setup\\NDP**.</span></span> <span data-ttu-id="32c4d-214">Poniższa tabela zawiera listę ścieżek do poszczególnych wersji .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="32c4d-214">The following table lists the path to each .NET Framework version.</span></span> <span data-ttu-id="32c4d-215">W przypadku większości wersji **istnieje REG_DWORD wartość** , aby wskazać, że `1` Ta wersja jest zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="32c4d-215">For most versions, there's an **Install** REG_DWORD value of `1` to indicate this version is installed.</span></span> <span data-ttu-id="32c4d-216">W tych podkluczach istnieje również **wersja** REG_SZ wartość, która zawiera ciąg wersji.</span><span class="sxs-lookup"><span data-stu-id="32c4d-216">In these subkeys, there's also a **Version** REG_SZ value that contains a version string.</span></span>

> [!NOTE]
> <span data-ttu-id="32c4d-217">Podklucz **instalacji programu .NET Framework** w ścieżce rejestru *nie* zaczyna się od kropki.</span><span class="sxs-lookup"><span data-stu-id="32c4d-217">The **NET Framework Setup** subkey in the registry path does *not* begin with a period.</span></span>

| <span data-ttu-id="32c4d-218">Wersja struktury</span><span class="sxs-lookup"><span data-stu-id="32c4d-218">Framework Version</span></span>  | <span data-ttu-id="32c4d-219">Podklucz rejestru</span><span class="sxs-lookup"><span data-stu-id="32c4d-219">Registry Subkey</span></span> | <span data-ttu-id="32c4d-220">Wartość</span><span class="sxs-lookup"><span data-stu-id="32c4d-220">Value</span></span> |
| ------------------ | --------------- | ----- |
| <span data-ttu-id="32c4d-221">1.0</span><span class="sxs-lookup"><span data-stu-id="32c4d-221">1.0</span></span>                | <span data-ttu-id="32c4d-222">**HKLM \\ oprogramowanie \\ Microsoft \\ . NETFramework \\ Policy \\ v 1.0 \\ 3705**</span><span class="sxs-lookup"><span data-stu-id="32c4d-222">**HKLM\\Software\\Microsoft\\.NETFramework\\Policy\\v1.0\\3705**</span></span>     | <span data-ttu-id="32c4d-223">**Zainstaluj** program REG_SZ równa się `1`</span><span class="sxs-lookup"><span data-stu-id="32c4d-223">**Install** REG_SZ equals `1`</span></span> |
| <span data-ttu-id="32c4d-224">1,1</span><span class="sxs-lookup"><span data-stu-id="32c4d-224">1.1</span></span>                | <span data-ttu-id="32c4d-225">**HKLM \\ oprogramowanie \\ Microsoft \\ .NET Framework Setup \\ NDP \\ v 1.1.4322**</span><span class="sxs-lookup"><span data-stu-id="32c4d-225">**HKLM\\Software\\Microsoft\\NET Framework Setup\\NDP\\v1.1.4322**</span></span>   | <span data-ttu-id="32c4d-226">**Zainstaluj** program REG_DWORD równa się `1`</span><span class="sxs-lookup"><span data-stu-id="32c4d-226">**Install** REG_DWORD equals `1`</span></span> |
| <span data-ttu-id="32c4d-227">2,0</span><span class="sxs-lookup"><span data-stu-id="32c4d-227">2.0</span></span>                | <span data-ttu-id="32c4d-228">**HKLM \\ oprogramowanie \\ Microsoft \\ .NET Framework Setup \\ NDP \\ v 2.0.50727**</span><span class="sxs-lookup"><span data-stu-id="32c4d-228">**HKLM\\Software\\Microsoft\\NET Framework Setup\\NDP\\v2.0.50727**</span></span>  | <span data-ttu-id="32c4d-229">**Zainstaluj** program REG_DWORD równa się `1`</span><span class="sxs-lookup"><span data-stu-id="32c4d-229">**Install** REG_DWORD equals `1`</span></span> |
| <span data-ttu-id="32c4d-230">3.0</span><span class="sxs-lookup"><span data-stu-id="32c4d-230">3.0</span></span>                | <span data-ttu-id="32c4d-231">**HKLM \\ oprogramowanie \\ Microsoft \\ .NET Framework Setup \\ NDP \\ v 3.0 \\ Setup**</span><span class="sxs-lookup"><span data-stu-id="32c4d-231">**HKLM\\Software\\Microsoft\\NET Framework Setup\\NDP\\v3.0\\Setup**</span></span> | <span data-ttu-id="32c4d-232">**InstallSuccess** REG_DWORD równa się `1`</span><span class="sxs-lookup"><span data-stu-id="32c4d-232">**InstallSuccess** REG_DWORD equals `1`</span></span> |
| <span data-ttu-id="32c4d-233">3,5</span><span class="sxs-lookup"><span data-stu-id="32c4d-233">3.5</span></span>                | <span data-ttu-id="32c4d-234">**HKLM \\ oprogramowanie \\ Microsoft \\ .NET Framework Setup \\ NDP \\ v 3.5**</span><span class="sxs-lookup"><span data-stu-id="32c4d-234">**HKLM\\Software\\Microsoft\\NET Framework Setup\\NDP\\v3.5**</span></span>        | <span data-ttu-id="32c4d-235">**Zainstaluj** program REG_DWORD równa się `1`</span><span class="sxs-lookup"><span data-stu-id="32c4d-235">**Install** REG_DWORD equals `1`</span></span> |
| <span data-ttu-id="32c4d-236">4,0 profil klienta</span><span class="sxs-lookup"><span data-stu-id="32c4d-236">4.0 Client Profile</span></span> | <span data-ttu-id="32c4d-237">**HKLM \\ oprogramowanie \\ Microsoft \\ .NET Framework Setup \\ NDP \\ v4 \\ Client**</span><span class="sxs-lookup"><span data-stu-id="32c4d-237">**HKLM\\Software\\Microsoft\\NET Framework Setup\\NDP\\v4\\Client**</span></span>  | <span data-ttu-id="32c4d-238">**Zainstaluj** program REG_DWORD równa się `1`</span><span class="sxs-lookup"><span data-stu-id="32c4d-238">**Install** REG_DWORD equals `1`</span></span> |
| <span data-ttu-id="32c4d-239">pełny profil 4,0</span><span class="sxs-lookup"><span data-stu-id="32c4d-239">4.0 Full Profile</span></span>   | <span data-ttu-id="32c4d-240">**HKLM \\ oprogramowanie \\ Microsoft \\ .NET Framework Setup \\ NDP \\ v4 \\ Full**</span><span class="sxs-lookup"><span data-stu-id="32c4d-240">**HKLM\\Software\\Microsoft\\NET Framework Setup\\NDP\\v4\\Full**</span></span>    | <span data-ttu-id="32c4d-241">**Zainstaluj** program REG_DWORD równa się `1`</span><span class="sxs-lookup"><span data-stu-id="32c4d-241">**Install** REG_DWORD equals `1`</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="32c4d-242">Jeśli uruchomiona aplikacja jest 32-bitowa i działa w 64-bitowym systemie Windows, ścieżki rejestru będą inne niż wymienione wcześniej.</span><span class="sxs-lookup"><span data-stu-id="32c4d-242">If the app you're running is 32-bit and running in 64-bit Windows, the registry paths will be different than previously listed.</span></span> <span data-ttu-id="32c4d-243">Rejestr 64-bitowy jest dostępny HKEY_LOCAL_MACHINE w podkluczu **\\ \\ Wow6432Node \\ oprogramowania** .</span><span class="sxs-lookup"><span data-stu-id="32c4d-243">The 64-bit registry is available in the **HKEY_LOCAL_MACHINE\\SOFTWARE\\Wow6432Node\\** subkey.</span></span> <span data-ttu-id="32c4d-244">Na przykład podklucz rejestru dla .NET Framework 3,5 jest **HKEY_LOCAL_MACHINE \\ oprogramowania \\ Wow6432Node \\ Microsoft \\ .NET Framework Setup \\ NDP \\ v 3.5**.</span><span class="sxs-lookup"><span data-stu-id="32c4d-244">For example, the registry subkey for .NET Framework 3.5 is **HKEY_LOCAL_MACHINE\\SOFTWARE\\Wow6432Node\\Microsoft\\NET Framework Setup\\NDP\\v3.5**.</span></span>

<span data-ttu-id="32c4d-245">Zwróć uwagę, że ścieżka rejestru do podklucza .NET Framework 1,0 różni się od innych.</span><span class="sxs-lookup"><span data-stu-id="32c4d-245">Notice that the registry path to the .NET Framework 1.0 subkey is different from the others.</span></span>

### <a name="use-registry-editor-older-framework-versions"></a><span data-ttu-id="32c4d-246">Użyj edytora rejestru (starsze wersje Framework)</span><span class="sxs-lookup"><span data-stu-id="32c4d-246">Use Registry Editor (older framework versions)</span></span>

01. <span data-ttu-id="32c4d-247">Z menu **Start** wybierz polecenie **Uruchom**, wpisz polecenie *regedit*, a następnie wybierz przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="32c4d-247">From the **Start** menu, choose **Run**, enter *regedit*, and then select **OK**.</span></span>

    <span data-ttu-id="32c4d-248">Musisz mieć poświadczenia administracyjne, aby uruchomić regedit.</span><span class="sxs-lookup"><span data-stu-id="32c4d-248">You must have administrative credentials to run regedit.</span></span>

01. <span data-ttu-id="32c4d-249">Otwórz podklucz pasujący do wersji, którą chcesz sprawdzić.</span><span class="sxs-lookup"><span data-stu-id="32c4d-249">Open the subkey that matches the version you want to check.</span></span> <span data-ttu-id="32c4d-250">Skorzystaj z tabeli w sekcji [wykrywanie .NET Framework 1,0 do 4,0](#detect-net-framework-10-through-40) .</span><span class="sxs-lookup"><span data-stu-id="32c4d-250">Use the table in the [Detect .NET Framework 1.0 through 4.0](#detect-net-framework-10-through-40) section.</span></span>

    <span data-ttu-id="32c4d-251">Na poniższej ilustracji przedstawiono podklucz i jego wartość **wersji** dla .NET Framework 3,5.</span><span class="sxs-lookup"><span data-stu-id="32c4d-251">The following figure shows the subkey and its **Version** value for .NET Framework 3.5.</span></span>

    <span data-ttu-id="32c4d-252">![Wpis rejestru dla .NET Framework 3,5.](./media/net-4-and-earlier.png ".NET Framework 3,5 i wcześniejsze wersje")</span><span class="sxs-lookup"><span data-stu-id="32c4d-252">![The registry entry for .NET Framework 3.5.](./media/net-4-and-earlier.png ".NET Framework 3.5 and earlier versions")</span></span>

### <a name="query-the-registry-using-code-older-framework-versions"></a><span data-ttu-id="32c4d-253">Wykonywanie zapytania dotyczącego rejestru przy użyciu kodu (starsze wersje Framework)</span><span class="sxs-lookup"><span data-stu-id="32c4d-253">Query the registry using code (older framework versions)</span></span>

<span data-ttu-id="32c4d-254">Użyj <xref:Microsoft.Win32.RegistryKey?displayProperty=nameWithType> klasy, aby uzyskać HKEY_LOCAL_MACHINE dostęp do podklucza **\\ \\ NDP oprogramowania Microsoft \\ .NET Framework Instalatora \\** w rejestrze systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="32c4d-254">Use the <xref:Microsoft.Win32.RegistryKey?displayProperty=nameWithType> class to access the **HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\NET Framework Setup\\NDP** subkey in the Windows registry.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="32c4d-255">Jeśli uruchomiona aplikacja jest 32-bitowa i działa w 64-bitowym systemie Windows, ścieżki rejestru będą inne niż wymienione wcześniej.</span><span class="sxs-lookup"><span data-stu-id="32c4d-255">If the app you're running is 32-bit and running in 64-bit Windows, the registry paths will be different than previously listed.</span></span> <span data-ttu-id="32c4d-256">Rejestr 64-bitowy jest dostępny HKEY_LOCAL_MACHINE w podkluczu **\\ \\ Wow6432Node \\ oprogramowania** .</span><span class="sxs-lookup"><span data-stu-id="32c4d-256">The 64-bit registry is available in the **HKEY_LOCAL_MACHINE\\SOFTWARE\\Wow6432Node\\** subkey.</span></span> <span data-ttu-id="32c4d-257">Na przykład podklucz rejestru dla .NET Framework 3,5 jest **HKEY_LOCAL_MACHINE \\ oprogramowania \\ Wow6432Node \\ Microsoft \\ .NET Framework Setup \\ NDP \\ v 3.5**.</span><span class="sxs-lookup"><span data-stu-id="32c4d-257">For example, the registry subkey for .NET Framework 3.5 is **HKEY_LOCAL_MACHINE\\SOFTWARE\\Wow6432Node\\Microsoft\\NET Framework Setup\\NDP\\v3.5**.</span></span>

<span data-ttu-id="32c4d-258">Poniższy przykład umożliwia znalezienie zainstalowanych wersji .NET Framework 1-4:</span><span class="sxs-lookup"><span data-stu-id="32c4d-258">The following example finds the versions of .NET Framework 1-4 that are installed:</span></span>

:::code language="csharp" source="snippets/csharp/versions-installed.cs" id="1":::

:::code language="vb" source="snippets/visual-basic/versions-installed.vb" id="1":::

<span data-ttu-id="32c4d-259">W przykładzie przedstawiono dane wyjściowe podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="32c4d-259">The example displays output similar to the following:</span></span>

```output
v2.0.50727  2.0.50727.4927  SP2
v3.0  3.0.30729.4926  SP2
v3.5  3.5.30729.4926  SP1
v4.0
  Client  4.0.0.0
```

## <a name="find-clr-versions"></a><span data-ttu-id="32c4d-260">Znajdź wersje środowiska CLR</span><span class="sxs-lookup"><span data-stu-id="32c4d-260">Find CLR versions</span></span>

<span data-ttu-id="32c4d-261">.NET Framework środowisko CLR zainstalowane z .NET Framework jest używane oddzielnie.</span><span class="sxs-lookup"><span data-stu-id="32c4d-261">The .NET Framework CLR installed with .NET Framework is versioned separately.</span></span> <span data-ttu-id="32c4d-262">Istnieją dwa sposoby wykrywania wersji .NET Framework CLR:</span><span class="sxs-lookup"><span data-stu-id="32c4d-262">There are two ways to detect the version of the .NET Framework CLR:</span></span>

- <span data-ttu-id="32c4d-263">**Narzędzie Clrver.exe**</span><span class="sxs-lookup"><span data-stu-id="32c4d-263">**The Clrver.exe tool**</span></span>

  <span data-ttu-id="32c4d-264">Użyj [Narzędzia wersji środowiska CLR (Clrver.exe)](../tools/clrver-exe-clr-version-tool.md) , aby określić, które wersje środowiska CLR są zainstalowane na komputerze.</span><span class="sxs-lookup"><span data-stu-id="32c4d-264">Use the [CLR Version tool (Clrver.exe)](../tools/clrver-exe-clr-version-tool.md) to determine which versions of the CLR are installed on a computer.</span></span> <span data-ttu-id="32c4d-265">Otwórz [wiersz polecenia dla deweloperów dla programu Visual Studio](../tools/developer-command-prompt-for-vs.md) i wprowadź `clrver` .</span><span class="sxs-lookup"><span data-stu-id="32c4d-265">Open the [Developer Command Prompt for Visual Studio](../tools/developer-command-prompt-for-vs.md) and enter `clrver`.</span></span>

  <span data-ttu-id="32c4d-266">Przykładowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="32c4d-266">Sample output:</span></span>

  ```console
  Versions installed on the machine:
  v2.0.50727
  v4.0.30319
  ```

- <span data-ttu-id="32c4d-267">**`Environment`Klasa**</span><span class="sxs-lookup"><span data-stu-id="32c4d-267">**The `Environment` class**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="32c4d-268">W przypadku .NET Framework 4,5 i nowszych wersji nie należy używać <xref:System.Environment.Version%2A?displayProperty=nameWithType> właściwości do wykrywania wersji środowiska CLR.</span><span class="sxs-lookup"><span data-stu-id="32c4d-268">For .NET Framework 4.5 and later versions, don't use the <xref:System.Environment.Version%2A?displayProperty=nameWithType> property to detect the version of the CLR.</span></span> <span data-ttu-id="32c4d-269">Zamiast tego należy wykonać zapytanie dotyczące rejestru zgodnie z opisem w artykule [wykrywanie .NET Framework 4,5 i nowszych wersji](#detect-net-framework-45-and-later-versions).</span><span class="sxs-lookup"><span data-stu-id="32c4d-269">Instead, query the registry as described in [Detect .NET Framework 4.5 and later versions](#detect-net-framework-45-and-later-versions).</span></span>

  1. <span data-ttu-id="32c4d-270">Zbadaj <xref:System.Environment.Version?displayProperty=nameWithType> Właściwość w celu pobrania <xref:System.Version> obiektu.</span><span class="sxs-lookup"><span data-stu-id="32c4d-270">Query the <xref:System.Environment.Version?displayProperty=nameWithType> property to retrieve a <xref:System.Version> object.</span></span>

     <span data-ttu-id="32c4d-271">Zwrócony `System.Version` obiekt identyfikuje wersję środowiska uruchomieniowego, które aktualnie wykonuje kod.</span><span class="sxs-lookup"><span data-stu-id="32c4d-271">The returned `System.Version` object identifies the version of the runtime that's currently executing the code.</span></span> <span data-ttu-id="32c4d-272">Nie zwraca wersji zestawu ani innych wersji środowiska uruchomieniowego, które mogły zostać zainstalowane na komputerze.</span><span class="sxs-lookup"><span data-stu-id="32c4d-272">It doesn't return assembly versions or other versions of the runtime that may have been installed on the computer.</span></span>

     <span data-ttu-id="32c4d-273">W przypadku .NET Framework w wersji 4, 4,5, 4.5.1 i 4.5.2 ciąg reprezentujący zwracanego <xref:System.Version> obiektu ma postać 4.0.30319.*XXXXX*, gdzie *XXXXX* jest mniejszy niż 42000.</span><span class="sxs-lookup"><span data-stu-id="32c4d-273">For .NET Framework versions 4, 4.5, 4.5.1, and 4.5.2, the string representation of the returned <xref:System.Version> object has the form 4.0.30319.*xxxxx*, where *xxxxx* is less than 42000.</span></span> <span data-ttu-id="32c4d-274">W przypadku .NET Framework 4,6 i nowszych wersje ma postać 4.0.30319.42000.</span><span class="sxs-lookup"><span data-stu-id="32c4d-274">For .NET Framework 4.6 and later versions, it has the form 4.0.30319.42000.</span></span>

  1. <span data-ttu-id="32c4d-275">Po utworzeniu obiektu **wersji** wykonaj zapytanie w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="32c4d-275">After you have the **Version** object, query it as follows:</span></span>

     - <span data-ttu-id="32c4d-276">Aby uzyskać informacje o głównym identyfikatorze wydania (na przykład *4* dla wersji 4,0), użyj <xref:System.Version.Major%2A?displayProperty=nameWithType> właściwości.</span><span class="sxs-lookup"><span data-stu-id="32c4d-276">For the major release identifier (for example, *4* for version 4.0), use the <xref:System.Version.Major%2A?displayProperty=nameWithType> property.</span></span>

     - <span data-ttu-id="32c4d-277">W przypadku pomocniczego identyfikatora wydania (na przykład *0* w przypadku wersji 4,0) należy użyć <xref:System.Version.Minor%2A?displayProperty=nameWithType> właściwości.</span><span class="sxs-lookup"><span data-stu-id="32c4d-277">For the minor release identifier (for example, *0* for version 4.0), use the <xref:System.Version.Minor%2A?displayProperty=nameWithType> property.</span></span>

     - <span data-ttu-id="32c4d-278">Dla całego ciągu wersji (na przykład *4.0.30319.18010*) Użyj <xref:System.Version.ToString%2A?displayProperty=nameWithType> metody.</span><span class="sxs-lookup"><span data-stu-id="32c4d-278">For the entire version string (for example, *4.0.30319.18010*), use the <xref:System.Version.ToString%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="32c4d-279">Ta metoda zwraca pojedynczą wartość odzwierciedlającą wersję środowiska uruchomieniowego, które wykonuje kod.</span><span class="sxs-lookup"><span data-stu-id="32c4d-279">This method returns a single value that reflects the version of the runtime that's executing the code.</span></span> <span data-ttu-id="32c4d-280">Nie zwraca wersji zestawu ani innych wersji środowiska uruchomieniowego, które mogą być zainstalowane na komputerze.</span><span class="sxs-lookup"><span data-stu-id="32c4d-280">It doesn't return assembly versions or other runtime versions that may be installed on the computer.</span></span>

  <span data-ttu-id="32c4d-281">W poniższym przykładzie zastosowano <xref:System.Environment.Version%2A?displayProperty=nameWithType> Właściwość w celu pobrania informacji o wersji środowiska CLR:</span><span class="sxs-lookup"><span data-stu-id="32c4d-281">The following example uses the <xref:System.Environment.Version%2A?displayProperty=nameWithType> property to retrieve CLR version information:</span></span>

  ```csharp
  Console.WriteLine($"Version: {Environment.Version}");
  ```

  ```vb
  Console.WriteLine($"Version: {Environment.Version}")
  ```

  <span data-ttu-id="32c4d-282">W przykładzie przedstawiono dane wyjściowe podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="32c4d-282">The example displays output similar to the following:</span></span>

  ```output
  Version: 4.0.30319.18010
  ```

## <a name="see-also"></a><span data-ttu-id="32c4d-283">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="32c4d-283">See also</span></span>

- [<span data-ttu-id="32c4d-284">Instrukcje: Określanie, które aktualizacje .NET Framework są zainstalowane</span><span class="sxs-lookup"><span data-stu-id="32c4d-284">How to: Determine which .NET Framework updates are installed</span></span>](how-to-determine-which-net-framework-updates-are-installed.md)
- [<span data-ttu-id="32c4d-285">Zainstaluj .NET Framework dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="32c4d-285">Install .NET Framework for developers</span></span>](../install/guide-for-developers.md)
- [<span data-ttu-id="32c4d-286">.NET Framework wersje i zależności</span><span class="sxs-lookup"><span data-stu-id="32c4d-286">.NET Framework versions and dependencies</span></span>](versions-and-dependencies.md)
