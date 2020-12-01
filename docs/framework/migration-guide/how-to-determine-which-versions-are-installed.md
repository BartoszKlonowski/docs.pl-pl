---
title: Określanie, które wersje programu .NET Framework są zainstalowane
description: Użyj kodu, regedit.exe lub programu PowerShell, aby wykryć, które wersje .NET Framework są zainstalowane na komputerze, badając rejestr systemu Windows.
ms.date: 02/03/2020
dev_langs:
- csharp
- vb
helpviewer_keywords:
- versions, determining for .NET Framework
- .NET Framework, determining version
ms.assetid: 40a67826-e4df-4f59-a651-d9eb0fdc755d
ms.openlocfilehash: b4c5b6911a4be4f9ac156b600646c649549f88f8
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96438139"
---
# <a name="how-to-determine-which-net-framework-versions-are-installed"></a><span data-ttu-id="d79d9-103">Instrukcje: Określanie, które wersje .NET Framework są zainstalowane</span><span class="sxs-lookup"><span data-stu-id="d79d9-103">How to: Determine which .NET Framework versions are installed</span></span>

<span data-ttu-id="d79d9-104">Użytkownicy mogą [instalować](../install/index.md) i uruchamiać wiele wersji .NET Framework na swoich komputerach.</span><span class="sxs-lookup"><span data-stu-id="d79d9-104">Users can [install](../install/index.md) and run multiple versions of .NET Framework on their computers.</span></span> <span data-ttu-id="d79d9-105">Podczas opracowywania lub wdrażania aplikacji może być konieczne, aby wiedzieć, które wersje .NET Framework są zainstalowane na komputerze użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d79d9-105">When you develop or deploy your app, you might need to know which .NET Framework versions are installed on the user's computer.</span></span> <span data-ttu-id="d79d9-106">Rejestr zawiera listę wersji .NET Framework zainstalowanych na komputerze.</span><span class="sxs-lookup"><span data-stu-id="d79d9-106">The registry contains a list of the versions of .NET Framework installed on the computer.</span></span>

<span data-ttu-id="d79d9-107">.NET Framework składa się z dwóch głównych składników, które są osobno dla wersji:</span><span class="sxs-lookup"><span data-stu-id="d79d9-107">.NET Framework consists of two main components, which are versioned separately:</span></span>

- <span data-ttu-id="d79d9-108">Zestaw zestawów, które są kolekcjami typów i zasobów zapewniających funkcje dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d79d9-108">A set of assemblies, which are collections of types and resources that provide the functionality for your apps.</span></span> <span data-ttu-id="d79d9-109">.NET Framework i zestawy mają ten sam numer wersji.</span><span class="sxs-lookup"><span data-stu-id="d79d9-109">.NET Framework and the assemblies share the same version number.</span></span> <span data-ttu-id="d79d9-110">Na przykład .NET Framework wersje obejmują 4,5, 4.6.1 i 4.7.2.</span><span class="sxs-lookup"><span data-stu-id="d79d9-110">For example, .NET Framework versions include 4.5, 4.6.1, and 4.7.2.</span></span>

- <span data-ttu-id="d79d9-111">Środowisko uruchomieniowe języka wspólnego (CLR), które zarządza kodem aplikacji i go wykonuje.</span><span class="sxs-lookup"><span data-stu-id="d79d9-111">The common language runtime (CLR), which manages and executes your app's code.</span></span> <span data-ttu-id="d79d9-112">Jedna wersja środowiska CLR obsługuje zazwyczaj wiele wersji .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="d79d9-112">A single CLR version typically supports multiple .NET Framework versions.</span></span> <span data-ttu-id="d79d9-113">Na przykład środowisko CLR w wersji 4.0.30319. *XXXXX* , gdzie *XXXXX* jest mniejszy niż 42000, obsługuje .NET Framework wersji 4 do 4.5.2.</span><span class="sxs-lookup"><span data-stu-id="d79d9-113">For example, CLR version 4.0.30319.*xxxxx* where *xxxxx* is less than 42000, supports .NET Framework versions 4 through 4.5.2.</span></span> <span data-ttu-id="d79d9-114">Wersja środowiska CLR o wartości większej lub równej 4.0.30319.42000 obsługuje wersje .NET Framework począwszy od .NET Framework 4,6.</span><span class="sxs-lookup"><span data-stu-id="d79d9-114">CLR version greater than or equal to 4.0.30319.42000 supports .NET Framework versions starting with .NET Framework 4.6.</span></span>

<span data-ttu-id="d79d9-115">Narzędzia obsługiwane przez społeczność są dostępne, aby pomóc w wykrywaniu, które wersje .NET Framework są zainstalowane:</span><span class="sxs-lookup"><span data-stu-id="d79d9-115">Community-maintained tools are available to help detect which .NET Framework versions are installed:</span></span>

- [https://github.com/jmalarcon/DotNetVersions](https://github.com/jmalarcon/DotNetVersions)

  <span data-ttu-id="d79d9-116">Narzędzie wiersza polecenia .NET Framework 2,0.</span><span class="sxs-lookup"><span data-stu-id="d79d9-116">A .NET Framework 2.0 command-line tool.</span></span>

- [https://github.com/EliteLoser/DotNetVersionLister](https://github.com/EliteLoser/DotNetVersionLister)

  <span data-ttu-id="d79d9-117">Moduł programu PowerShell 2,0.</span><span class="sxs-lookup"><span data-stu-id="d79d9-117">A PowerShell 2.0 module.</span></span>

<span data-ttu-id="d79d9-118">Aby uzyskać informacje dotyczące wykrywania zainstalowanych aktualizacji dla każdej wersji .NET Framework, zobacz [How to: Określanie, które aktualizacje .NET Framework są zainstalowane](how-to-determine-which-net-framework-updates-are-installed.md).</span><span class="sxs-lookup"><span data-stu-id="d79d9-118">For information about detecting the installed updates for each version of .NET Framework, see [How to: Determine which .NET Framework updates are installed](how-to-determine-which-net-framework-updates-are-installed.md).</span></span>

## <a name="detect-net-framework-45-and-later-versions"></a><span data-ttu-id="d79d9-119">Wykryj .NET Framework 4,5 i nowsze wersje</span><span class="sxs-lookup"><span data-stu-id="d79d9-119">Detect .NET Framework 4.5 and later versions</span></span>

<span data-ttu-id="d79d9-120">Wersja .NET Framework (4,5 lub nowsza) zainstalowana na komputerze jest wymieniona w rejestrze w **HKEY_LOCAL_MACHINE \\ oprogramowania \\ Microsoft \\ NET Framework Setup \\ NDP \\ v4 \\**.</span><span class="sxs-lookup"><span data-stu-id="d79d9-120">The version of .NET Framework (4.5 and later) installed on a machine is listed in the registry at **HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\NET Framework Setup\\NDP\\v4\\Full**.</span></span> <span data-ttu-id="d79d9-121">Jeśli brakuje **pełnego** podklucza, to .NET Framework 4,5 lub nowsze nie są zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="d79d9-121">If the **Full** subkey is missing, then .NET Framework 4.5 or above isn't installed.</span></span>

> [!NOTE]
> <span data-ttu-id="d79d9-122">Podklucz **instalacji programu .NET Framework** w ścieżce rejestru *nie* zaczyna się od kropki.</span><span class="sxs-lookup"><span data-stu-id="d79d9-122">The **NET Framework Setup** subkey in the registry path does *not* begin with a period.</span></span>

<span data-ttu-id="d79d9-123">Wartość REG_DWORD **wydania** w rejestrze reprezentuje wersję zainstalowanej .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="d79d9-123">The **Release** REG_DWORD value in the registry represents the version of .NET Framework installed.</span></span>

<a name="version_table"></a>

| <span data-ttu-id="d79d9-124">Wersja programu .NET Framework</span><span class="sxs-lookup"><span data-stu-id="d79d9-124">.NET Framework version</span></span> | <span data-ttu-id="d79d9-125">Wartość **wydania**</span><span class="sxs-lookup"><span data-stu-id="d79d9-125">Value of **Release**</span></span> |
| ---------------------- | -------------------------- |
| <span data-ttu-id="d79d9-126">.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="d79d9-126">.NET Framework 4.5</span></span>     | <span data-ttu-id="d79d9-127">Wszystkie systemy operacyjne Windows: 378389</span><span class="sxs-lookup"><span data-stu-id="d79d9-127">All Windows operating systems: 378389</span></span> |
| <span data-ttu-id="d79d9-128">.NET Framework 4.5.1</span><span class="sxs-lookup"><span data-stu-id="d79d9-128">.NET Framework 4.5.1</span></span>   | <span data-ttu-id="d79d9-129">W systemach Windows 8.1 i Windows Server 2012 R2:378675</span><span class="sxs-lookup"><span data-stu-id="d79d9-129">On Windows 8.1 and Windows Server 2012 R2: 378675</span></span><br /><span data-ttu-id="d79d9-130">We wszystkich innych systemach operacyjnych Windows: 378758</span><span class="sxs-lookup"><span data-stu-id="d79d9-130">On all other Windows operating systems: 378758</span></span> |
| <span data-ttu-id="d79d9-131">.NET Framework 4.5.2</span><span class="sxs-lookup"><span data-stu-id="d79d9-131">.NET Framework 4.5.2</span></span>   | <span data-ttu-id="d79d9-132">Wszystkie systemy operacyjne Windows: 379893</span><span class="sxs-lookup"><span data-stu-id="d79d9-132">All Windows operating systems: 379893</span></span> |
| <span data-ttu-id="d79d9-133">Program .NET Framework 4.6</span><span class="sxs-lookup"><span data-stu-id="d79d9-133">.NET Framework 4.6</span></span>     | <span data-ttu-id="d79d9-134">W systemie Windows 10:393295</span><span class="sxs-lookup"><span data-stu-id="d79d9-134">On Windows 10: 393295</span></span><br /><span data-ttu-id="d79d9-135">We wszystkich innych systemach operacyjnych Windows: 393297</span><span class="sxs-lookup"><span data-stu-id="d79d9-135">On all other Windows operating systems: 393297</span></span> |
| <span data-ttu-id="d79d9-136">.NET Framework 4.6.1</span><span class="sxs-lookup"><span data-stu-id="d79d9-136">.NET Framework 4.6.1</span></span>   | <span data-ttu-id="d79d9-137">W systemach aktualizacji systemu Windows 10 listopad: 394254</span><span class="sxs-lookup"><span data-stu-id="d79d9-137">On Windows 10 November Update systems: 394254</span></span><br /><span data-ttu-id="d79d9-138">We wszystkich innych systemach operacyjnych Windows (w tym Windows 10): 394271</span><span class="sxs-lookup"><span data-stu-id="d79d9-138">On all other Windows operating systems (including Windows 10): 394271</span></span> |
| <span data-ttu-id="d79d9-139">.NET Framework 4.6.2</span><span class="sxs-lookup"><span data-stu-id="d79d9-139">.NET Framework 4.6.2</span></span>   | <span data-ttu-id="d79d9-140">W rocznicowej aktualizacji systemu Windows 10 i Windows Server 2016:394802</span><span class="sxs-lookup"><span data-stu-id="d79d9-140">On Windows 10 Anniversary Update and Windows Server 2016: 394802</span></span><br /><span data-ttu-id="d79d9-141">Wszystkie inne systemy operacyjne Windows (w tym inne systemy operacyjne Windows 10): 394806</span><span class="sxs-lookup"><span data-stu-id="d79d9-141">On all other Windows operating systems (including other Windows 10 operating systems): 394806</span></span> |
| <span data-ttu-id="d79d9-142"> .NET Framework 4.7</span><span class="sxs-lookup"><span data-stu-id="d79d9-142">.NET Framework 4.7</span></span>     | <span data-ttu-id="d79d9-143">Aktualizacja systemu Windows 10 dla twórców: 460798</span><span class="sxs-lookup"><span data-stu-id="d79d9-143">On Windows 10 Creators Update: 460798</span></span><br /><span data-ttu-id="d79d9-144">Wszystkie inne systemy operacyjne Windows (w tym inne systemy operacyjne Windows 10): 460805</span><span class="sxs-lookup"><span data-stu-id="d79d9-144">On all other Windows operating systems (including other Windows 10 operating systems): 460805</span></span> |
| <span data-ttu-id="d79d9-145">.NET Framework 4.7.1</span><span class="sxs-lookup"><span data-stu-id="d79d9-145">.NET Framework 4.7.1</span></span>   | <span data-ttu-id="d79d9-146">W przypadku aktualizacji systemu Windows 10 dla twórców i systemu Windows Server w wersji 1709:461308</span><span class="sxs-lookup"><span data-stu-id="d79d9-146">On Windows 10 Fall Creators Update and Windows Server, version 1709: 461308</span></span><br/><span data-ttu-id="d79d9-147">Wszystkie inne systemy operacyjne Windows (w tym inne systemy operacyjne Windows 10): 461310</span><span class="sxs-lookup"><span data-stu-id="d79d9-147">On all other Windows operating systems (including other Windows 10 operating systems): 461310</span></span> |
| <span data-ttu-id="d79d9-148"> .NET Framework 4.7.2</span><span class="sxs-lookup"><span data-stu-id="d79d9-148">.NET Framework 4.7.2</span></span>   | <span data-ttu-id="d79d9-149">W systemie Windows 10 kwiecień 2018 Update i Windows Server w wersji 1803:461808</span><span class="sxs-lookup"><span data-stu-id="d79d9-149">On Windows 10 April 2018 Update and Windows Server, version 1803: 461808</span></span><br/><span data-ttu-id="d79d9-150">We wszystkich systemach operacyjnych Windows innych niż Windows 10 kwiecień 2018 Update i Windows Server w wersji 1803:461814</span><span class="sxs-lookup"><span data-stu-id="d79d9-150">On all Windows operating systems other than Windows 10 April 2018 Update and Windows Server, version 1803: 461814</span></span> |
| <span data-ttu-id="d79d9-151"> .NET Framework 4.8</span><span class="sxs-lookup"><span data-stu-id="d79d9-151">.NET Framework 4.8</span></span>     | <span data-ttu-id="d79d9-152">W systemie Windows 10 maja 2019 Update i aktualizacja Windows 10 listopad 2019:528040</span><span class="sxs-lookup"><span data-stu-id="d79d9-152">On Windows 10 May 2019 Update and Windows 10 November 2019 Update: 528040</span></span><br/><span data-ttu-id="d79d9-153">Aktualizacje systemu Windows 10 maja 2020 Update i Windows 10 października 2020:528372</span><span class="sxs-lookup"><span data-stu-id="d79d9-153">On Windows 10 May 2020 Update and Windows 10 October 2020 Update: 528372</span></span><br/><span data-ttu-id="d79d9-154">Wszystkie inne systemy operacyjne Windows (w tym inne systemy operacyjne Windows 10): 528049</span><span class="sxs-lookup"><span data-stu-id="d79d9-154">On all other Windows operating systems (including other Windows 10 operating systems): 528049</span></span> |

### <a name="minimum-version"></a><span data-ttu-id="d79d9-155">Minimalna wersja</span><span class="sxs-lookup"><span data-stu-id="d79d9-155">Minimum version</span></span>

<span data-ttu-id="d79d9-156">Aby określić, czy jest dostępna *minimalna* wersja .NET Framework, sprawdź, czy wartość **wydania** REG_DWORD, która jest większa lub równa odpowiadającej wartości wymienionej w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="d79d9-156">To determine whether a *minimum* version of .NET Framework is present, check for a **Release** REG_DWORD value that's greater than or equal to the corresponding value listed in the following table.</span></span> <span data-ttu-id="d79d9-157">Na przykład, jeśli aplikacja działa w .NET Framework 4,8 lub nowszej wersji, należy sprawdzić, czy w **wersji** REG_DWORD wartość jest *większa niż lub równa* 528040.</span><span class="sxs-lookup"><span data-stu-id="d79d9-157">For example, if your application runs under .NET Framework 4.8 or a later version, test for a **Release** REG_DWORD value that's *greater than or equal to* 528040.</span></span>

| <span data-ttu-id="d79d9-158">Wersja programu .NET Framework</span><span class="sxs-lookup"><span data-stu-id="d79d9-158">.NET Framework version</span></span> | <span data-ttu-id="d79d9-159">Wartość minimalna</span><span class="sxs-lookup"><span data-stu-id="d79d9-159">Minimum value</span></span> |
| ---------------------- | ------------- |
| <span data-ttu-id="d79d9-160">.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="d79d9-160">.NET Framework 4.5</span></span>     | <span data-ttu-id="d79d9-161">378389</span><span class="sxs-lookup"><span data-stu-id="d79d9-161">378389</span></span> |
| <span data-ttu-id="d79d9-162">.NET Framework 4.5.1</span><span class="sxs-lookup"><span data-stu-id="d79d9-162">.NET Framework 4.5.1</span></span>   | <span data-ttu-id="d79d9-163">378675</span><span class="sxs-lookup"><span data-stu-id="d79d9-163">378675</span></span> |
| <span data-ttu-id="d79d9-164">.NET Framework 4.5.2</span><span class="sxs-lookup"><span data-stu-id="d79d9-164">.NET Framework 4.5.2</span></span>   | <span data-ttu-id="d79d9-165">379893</span><span class="sxs-lookup"><span data-stu-id="d79d9-165">379893</span></span> |
| <span data-ttu-id="d79d9-166">Program .NET Framework 4.6</span><span class="sxs-lookup"><span data-stu-id="d79d9-166">.NET Framework 4.6</span></span>     | <span data-ttu-id="d79d9-167">393295</span><span class="sxs-lookup"><span data-stu-id="d79d9-167">393295</span></span> |
| <span data-ttu-id="d79d9-168">.NET Framework 4.6.1</span><span class="sxs-lookup"><span data-stu-id="d79d9-168">.NET Framework 4.6.1</span></span>   | <span data-ttu-id="d79d9-169">394254</span><span class="sxs-lookup"><span data-stu-id="d79d9-169">394254</span></span> |
| <span data-ttu-id="d79d9-170">.NET Framework 4.6.2</span><span class="sxs-lookup"><span data-stu-id="d79d9-170">.NET Framework 4.6.2</span></span>   | <span data-ttu-id="d79d9-171">394802</span><span class="sxs-lookup"><span data-stu-id="d79d9-171">394802</span></span> |
| <span data-ttu-id="d79d9-172"> .NET Framework 4.7</span><span class="sxs-lookup"><span data-stu-id="d79d9-172">.NET Framework 4.7</span></span>     | <span data-ttu-id="d79d9-173">460798</span><span class="sxs-lookup"><span data-stu-id="d79d9-173">460798</span></span> |
| <span data-ttu-id="d79d9-174">.NET Framework 4.7.1</span><span class="sxs-lookup"><span data-stu-id="d79d9-174">.NET Framework 4.7.1</span></span>   | <span data-ttu-id="d79d9-175">461308</span><span class="sxs-lookup"><span data-stu-id="d79d9-175">461308</span></span> |
| <span data-ttu-id="d79d9-176"> .NET Framework 4.7.2</span><span class="sxs-lookup"><span data-stu-id="d79d9-176">.NET Framework 4.7.2</span></span>   | <span data-ttu-id="d79d9-177">461808</span><span class="sxs-lookup"><span data-stu-id="d79d9-177">461808</span></span> |
| <span data-ttu-id="d79d9-178"> .NET Framework 4.8</span><span class="sxs-lookup"><span data-stu-id="d79d9-178">.NET Framework 4.8</span></span>     | <span data-ttu-id="d79d9-179">528040</span><span class="sxs-lookup"><span data-stu-id="d79d9-179">528040</span></span> |

### <a name="use-registry-editor"></a><span data-ttu-id="d79d9-180">Korzystanie z edytora rejestru</span><span class="sxs-lookup"><span data-stu-id="d79d9-180">Use Registry Editor</span></span>

01. <span data-ttu-id="d79d9-181">Z menu **Start** wybierz polecenie **Uruchom**, wpisz polecenie *regedit*, a następnie wybierz przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d79d9-181">From the **Start** menu, choose **Run**, enter *regedit*, and then select **OK**.</span></span>

   <span data-ttu-id="d79d9-182">(Musisz mieć poświadczenia administracyjne, aby uruchomić regedit).</span><span class="sxs-lookup"><span data-stu-id="d79d9-182">(You must have administrative credentials to run regedit.)</span></span>

01. <span data-ttu-id="d79d9-183">W Edytorze rejestru Otwórz następujący podklucz: **HKEY_LOCAL_MACHINE \\ Software \\ Microsoft \\ .NET Framework Setup \\ NDP \\ v4 \\**.</span><span class="sxs-lookup"><span data-stu-id="d79d9-183">In the Registry Editor, open the following subkey: **HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\NET Framework Setup\\NDP\\v4\\Full**.</span></span> <span data-ttu-id="d79d9-184">Jeśli **pełny** podklucz nie jest obecny, nie masz zainstalowanego .NET Framework 4,5 lub nowszego.</span><span class="sxs-lookup"><span data-stu-id="d79d9-184">If the **Full** subkey isn't present, then you don't have .NET Framework 4.5 or later installed.</span></span>

01. <span data-ttu-id="d79d9-185">Sprawdź, czy REG_DWORD wpis o nazwie **Release**.</span><span class="sxs-lookup"><span data-stu-id="d79d9-185">Check for a REG_DWORD entry named **Release**.</span></span> <span data-ttu-id="d79d9-186">Jeśli istnieje, jest zainstalowana .NET Framework 4,5 lub nowsza.</span><span class="sxs-lookup"><span data-stu-id="d79d9-186">If it exists, then you have .NET Framework 4.5 or later installed.</span></span> <span data-ttu-id="d79d9-187">Jego wartość odnosi się do określonej wersji .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="d79d9-187">Its value corresponds to a particular version of .NET Framework.</span></span> <span data-ttu-id="d79d9-188">Na przykład, wartość wpisu **zlecenia** to 528040, który jest kluczem wydania dla .NET Framework 4,8.</span><span class="sxs-lookup"><span data-stu-id="d79d9-188">In the following figure, for example, the value of the **Release** entry is 528040, which is the release key for .NET Framework 4.8.</span></span>

   ![Wpis rejestru dla .NET Framework 4,5](./media/clr-installdir.png )

### <a name="use-powershell-to-check-for-a-minimum-version"></a><span data-ttu-id="d79d9-190">Sprawdzanie minimalnej wersji przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="d79d9-190">Use PowerShell to check for a minimum version</span></span>

<span data-ttu-id="d79d9-191">Użyj poleceń programu PowerShell, aby sprawdzić wartość wpisu **Release** w **HKEY_LOCAL_MACHINE \\ oprogramowania \\ Microsoft \\ NET Framework Setup \\ NDP \\ v4 \\ Full** podklucza.</span><span class="sxs-lookup"><span data-stu-id="d79d9-191">Use PowerShell commands to check the value of the **Release** entry of the **HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\NET Framework Setup\\NDP\\v4\\Full** subkey.</span></span>

<span data-ttu-id="d79d9-192">W poniższych przykładach Sprawdź wartość wpisu **Zwolnij** , aby określić, czy .NET Framework 4.6.2 czy nowsza.</span><span class="sxs-lookup"><span data-stu-id="d79d9-192">The following examples check the value of the **Release** entry to determine whether .NET Framework 4.6.2 or later is installed.</span></span> <span data-ttu-id="d79d9-193">Ten kod zwraca `True` , jeśli jest zainstalowany i `False` w przeciwnym razie.</span><span class="sxs-lookup"><span data-stu-id="d79d9-193">This code returns `True` if it's installed and `False` otherwise.</span></span>

```powershell
(Get-ItemProperty "HKLM:\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full").Release -ge 394802
```

### <a name="query-the-registry-using-code"></a><span data-ttu-id="d79d9-194">Tworzenie zapytań dotyczących rejestru przy użyciu kodu</span><span class="sxs-lookup"><span data-stu-id="d79d9-194">Query the registry using code</span></span>

01. <span data-ttu-id="d79d9-195">Użyj <xref:Microsoft.Win32.RegistryKey.OpenBaseKey%2A?displayProperty=nameWithType> metod i, <xref:Microsoft.Win32.RegistryKey.OpenSubKey%2A?displayProperty=nameWithType> Aby uzyskać dostęp do **HKEY_LOCAL_MACHINE \\ oprogramowania \\ Microsoft \\ .NET Framework Setup \\ NDP \\ v4 \\** w rejestrze systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="d79d9-195">Use the <xref:Microsoft.Win32.RegistryKey.OpenBaseKey%2A?displayProperty=nameWithType> and <xref:Microsoft.Win32.RegistryKey.OpenSubKey%2A?displayProperty=nameWithType> methods to access the **HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\NET Framework Setup\\NDP\\v4\\Full** subkey in the Windows registry.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="d79d9-196">Jeśli uruchomiona aplikacja jest 32-bitowa i działa w 64-bitowym systemie Windows, ścieżki rejestru będą inne niż wymienione wcześniej.</span><span class="sxs-lookup"><span data-stu-id="d79d9-196">If the app you're running is 32-bit and running in 64-bit Windows, the registry paths will be different than previously listed.</span></span> <span data-ttu-id="d79d9-197">Rejestr 64-bitowy jest dostępny HKEY_LOCAL_MACHINE w podkluczu **\\ \\ Wow6432Node \\ oprogramowania** .</span><span class="sxs-lookup"><span data-stu-id="d79d9-197">The 64-bit registry is available in the **HKEY_LOCAL_MACHINE\\SOFTWARE\\Wow6432Node\\** subkey.</span></span> <span data-ttu-id="d79d9-198">Na przykład podklucz rejestru dla .NET Framework 4,5 to **HKEY_LOCAL_MACHINE \\ Software \\ Wow6432Node \\ Microsoft \\ .NET Framework Setup \\ NDP \\ v4 \\ Full**.</span><span class="sxs-lookup"><span data-stu-id="d79d9-198">For example, the registry subkey for .NET Framework 4.5 is **HKEY_LOCAL_MACHINE\\SOFTWARE\\Wow6432Node\\Microsoft\\NET Framework Setup\\NDP\\v4\\Full**.</span></span>

01. <span data-ttu-id="d79d9-199">Sprawdź wartość REG_DWORD **wydania** , aby określić zainstalowaną wersję.</span><span class="sxs-lookup"><span data-stu-id="d79d9-199">Check the **Release** REG_DWORD value to determine the installed version.</span></span> <span data-ttu-id="d79d9-200">Aby można było przesłać dalej, sprawdź, czy wartość jest większa niż lub równa wartości wymienionej w [tabeli wersji .NET Framework](#version_table).</span><span class="sxs-lookup"><span data-stu-id="d79d9-200">To be forward-compatible, check for a value greater than or equal to the value listed in the [.NET Framework version table](#version_table).</span></span>

<span data-ttu-id="d79d9-201">Poniższy przykład sprawdza wartość wpisu **Release** w rejestrze, aby znaleźć zainstalowane wersje .NET Framework 4.5-4.8:</span><span class="sxs-lookup"><span data-stu-id="d79d9-201">The following example checks the value of the **Release** entry in the registry to find the versions of .NET Framework 4.5-4.8 that are installed:</span></span>

:::code language="csharp" source="snippets/csharp/versions-installed.cs" id="2":::

:::code language="vb" source="snippets/visual-basic/versions-installed.vb" id="2":::

<span data-ttu-id="d79d9-202">Przykład wyświetla dane wyjściowe podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="d79d9-202">The example displays output like the following:</span></span>

```output
.NET Framework Version: 4.6.1
```

<span data-ttu-id="d79d9-203">Ten przykład jest zgodny z zalecaną metodą sprawdzania wersji:</span><span class="sxs-lookup"><span data-stu-id="d79d9-203">This example follows the recommended practice for version checking:</span></span>

- <span data-ttu-id="d79d9-204">Sprawdza, czy wartość wpisu **wydania** jest *większa niż lub równa* wartości znanych kluczy wydania.</span><span class="sxs-lookup"><span data-stu-id="d79d9-204">It checks whether the value of the **Release** entry is *greater than or equal to* the value of the known release keys.</span></span>
- <span data-ttu-id="d79d9-205">Sprawdza w kolejności od najnowszej wersji do najwcześniejszej wersji.</span><span class="sxs-lookup"><span data-stu-id="d79d9-205">It checks in order from most recent version to earliest version.</span></span>

## <a name="detect-net-framework-10-through-40"></a><span data-ttu-id="d79d9-206">Wykryj .NET Framework 1,0 do 4,0</span><span class="sxs-lookup"><span data-stu-id="d79d9-206">Detect .NET Framework 1.0 through 4.0</span></span>

<span data-ttu-id="d79d9-207">Każda wersja .NET Framework od 1,1 do 4,0 jest wyświetlana jako podklucz w **HKEY_LOCAL_MACHINE \\ oprogramowaniu \\ Microsoft \\ .NET Framework Setup \\ NDP**.</span><span class="sxs-lookup"><span data-stu-id="d79d9-207">Each version of .NET Framework from 1.1 to 4.0 is listed as a subkey at **HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\NET Framework Setup\\NDP**.</span></span> <span data-ttu-id="d79d9-208">Poniższa tabela zawiera listę ścieżek do poszczególnych wersji .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="d79d9-208">The following table lists the path to each .NET Framework version.</span></span> <span data-ttu-id="d79d9-209">W przypadku większości wersji **istnieje REG_DWORD wartość** , aby wskazać, że `1` Ta wersja jest zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="d79d9-209">For most versions, there's an **Install** REG_DWORD value of `1` to indicate this version is installed.</span></span> <span data-ttu-id="d79d9-210">W tych podkluczach istnieje również **wersja** REG_SZ wartość, która zawiera ciąg wersji.</span><span class="sxs-lookup"><span data-stu-id="d79d9-210">In these subkeys, there's also a **Version** REG_SZ value that contains a version string.</span></span>

> [!NOTE]
> <span data-ttu-id="d79d9-211">Podklucz **instalacji programu .NET Framework** w ścieżce rejestru *nie* zaczyna się od kropki.</span><span class="sxs-lookup"><span data-stu-id="d79d9-211">The **NET Framework Setup** subkey in the registry path does *not* begin with a period.</span></span>

| <span data-ttu-id="d79d9-212">Wersja struktury</span><span class="sxs-lookup"><span data-stu-id="d79d9-212">Framework Version</span></span>  | <span data-ttu-id="d79d9-213">Podklucz rejestru</span><span class="sxs-lookup"><span data-stu-id="d79d9-213">Registry Subkey</span></span> | <span data-ttu-id="d79d9-214">Wartość</span><span class="sxs-lookup"><span data-stu-id="d79d9-214">Value</span></span> |
| ------------------ | --------------- | ----- |
| <span data-ttu-id="d79d9-215">1,0</span><span class="sxs-lookup"><span data-stu-id="d79d9-215">1.0</span></span>                | <span data-ttu-id="d79d9-216">**HKLM \\ oprogramowanie \\ Microsoft \\ . NETFramework \\ Policy \\ v 1.0 \\ 3705**</span><span class="sxs-lookup"><span data-stu-id="d79d9-216">**HKLM\\Software\\Microsoft\\.NETFramework\\Policy\\v1.0\\3705**</span></span>     | <span data-ttu-id="d79d9-217">**Zainstaluj** program REG_SZ równa się `1`</span><span class="sxs-lookup"><span data-stu-id="d79d9-217">**Install** REG_SZ equals `1`</span></span> |
| <span data-ttu-id="d79d9-218">1,1</span><span class="sxs-lookup"><span data-stu-id="d79d9-218">1.1</span></span>                | <span data-ttu-id="d79d9-219">**HKLM \\ oprogramowanie \\ Microsoft \\ .NET Framework Setup \\ NDP \\ v 1.1.4322**</span><span class="sxs-lookup"><span data-stu-id="d79d9-219">**HKLM\\Software\\Microsoft\\NET Framework Setup\\NDP\\v1.1.4322**</span></span>   | <span data-ttu-id="d79d9-220">**Zainstaluj** program REG_DWORD równa się `1`</span><span class="sxs-lookup"><span data-stu-id="d79d9-220">**Install** REG_DWORD equals `1`</span></span> |
| <span data-ttu-id="d79d9-221">2,0</span><span class="sxs-lookup"><span data-stu-id="d79d9-221">2.0</span></span>                | <span data-ttu-id="d79d9-222">**HKLM \\ oprogramowanie \\ Microsoft \\ .NET Framework Setup \\ NDP \\ v 2.0.50727**</span><span class="sxs-lookup"><span data-stu-id="d79d9-222">**HKLM\\Software\\Microsoft\\NET Framework Setup\\NDP\\v2.0.50727**</span></span>  | <span data-ttu-id="d79d9-223">**Zainstaluj** program REG_DWORD równa się `1`</span><span class="sxs-lookup"><span data-stu-id="d79d9-223">**Install** REG_DWORD equals `1`</span></span> |
| <span data-ttu-id="d79d9-224">3.0</span><span class="sxs-lookup"><span data-stu-id="d79d9-224">3.0</span></span>                | <span data-ttu-id="d79d9-225">**HKLM \\ oprogramowanie \\ Microsoft \\ .NET Framework Setup \\ NDP \\ v 3.0 \\ Setup**</span><span class="sxs-lookup"><span data-stu-id="d79d9-225">**HKLM\\Software\\Microsoft\\NET Framework Setup\\NDP\\v3.0\\Setup**</span></span> | <span data-ttu-id="d79d9-226">**InstallSuccess** REG_DWORD równa się `1`</span><span class="sxs-lookup"><span data-stu-id="d79d9-226">**InstallSuccess** REG_DWORD equals `1`</span></span> |
| <span data-ttu-id="d79d9-227">3,5</span><span class="sxs-lookup"><span data-stu-id="d79d9-227">3.5</span></span>                | <span data-ttu-id="d79d9-228">**HKLM \\ oprogramowanie \\ Microsoft \\ .NET Framework Setup \\ NDP \\ v 3.5**</span><span class="sxs-lookup"><span data-stu-id="d79d9-228">**HKLM\\Software\\Microsoft\\NET Framework Setup\\NDP\\v3.5**</span></span>        | <span data-ttu-id="d79d9-229">**Zainstaluj** program REG_DWORD równa się `1`</span><span class="sxs-lookup"><span data-stu-id="d79d9-229">**Install** REG_DWORD equals `1`</span></span> |
| <span data-ttu-id="d79d9-230">4,0 profil klienta</span><span class="sxs-lookup"><span data-stu-id="d79d9-230">4.0 Client Profile</span></span> | <span data-ttu-id="d79d9-231">**HKLM \\ oprogramowanie \\ Microsoft \\ .NET Framework Setup \\ NDP \\ v4 \\ Client**</span><span class="sxs-lookup"><span data-stu-id="d79d9-231">**HKLM\\Software\\Microsoft\\NET Framework Setup\\NDP\\v4\\Client**</span></span>  | <span data-ttu-id="d79d9-232">**Zainstaluj** program REG_DWORD równa się `1`</span><span class="sxs-lookup"><span data-stu-id="d79d9-232">**Install** REG_DWORD equals `1`</span></span> |
| <span data-ttu-id="d79d9-233">pełny profil 4,0</span><span class="sxs-lookup"><span data-stu-id="d79d9-233">4.0 Full Profile</span></span>   | <span data-ttu-id="d79d9-234">**HKLM \\ oprogramowanie \\ Microsoft \\ .NET Framework Setup \\ NDP \\ v4 \\ Full**</span><span class="sxs-lookup"><span data-stu-id="d79d9-234">**HKLM\\Software\\Microsoft\\NET Framework Setup\\NDP\\v4\\Full**</span></span>    | <span data-ttu-id="d79d9-235">**Zainstaluj** program REG_DWORD równa się `1`</span><span class="sxs-lookup"><span data-stu-id="d79d9-235">**Install** REG_DWORD equals `1`</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="d79d9-236">Jeśli uruchomiona aplikacja jest 32-bitowa i działa w 64-bitowym systemie Windows, ścieżki rejestru będą inne niż wymienione wcześniej.</span><span class="sxs-lookup"><span data-stu-id="d79d9-236">If the app you're running is 32-bit and running in 64-bit Windows, the registry paths will be different than previously listed.</span></span> <span data-ttu-id="d79d9-237">Rejestr 64-bitowy jest dostępny HKEY_LOCAL_MACHINE w podkluczu **\\ \\ Wow6432Node \\ oprogramowania** .</span><span class="sxs-lookup"><span data-stu-id="d79d9-237">The 64-bit registry is available in the **HKEY_LOCAL_MACHINE\\SOFTWARE\\Wow6432Node\\** subkey.</span></span> <span data-ttu-id="d79d9-238">Na przykład podklucz rejestru dla .NET Framework 3,5 jest **HKEY_LOCAL_MACHINE \\ oprogramowania \\ Wow6432Node \\ Microsoft \\ .NET Framework Setup \\ NDP \\ v 3.5**.</span><span class="sxs-lookup"><span data-stu-id="d79d9-238">For example, the registry subkey for .NET Framework 3.5 is **HKEY_LOCAL_MACHINE\\SOFTWARE\\Wow6432Node\\Microsoft\\NET Framework Setup\\NDP\\v3.5**.</span></span>

<span data-ttu-id="d79d9-239">Zwróć uwagę, że ścieżka rejestru do podklucza .NET Framework 1,0 różni się od innych.</span><span class="sxs-lookup"><span data-stu-id="d79d9-239">Notice that the registry path to the .NET Framework 1.0 subkey is different from the others.</span></span>

### <a name="use-registry-editor-older-framework-versions"></a><span data-ttu-id="d79d9-240">Użyj edytora rejestru (starsze wersje Framework)</span><span class="sxs-lookup"><span data-stu-id="d79d9-240">Use Registry Editor (older framework versions)</span></span>

01. <span data-ttu-id="d79d9-241">Z menu **Start** wybierz polecenie **Uruchom**, wpisz polecenie *regedit*, a następnie wybierz przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d79d9-241">From the **Start** menu, choose **Run**, enter *regedit*, and then select **OK**.</span></span>

    <span data-ttu-id="d79d9-242">Musisz mieć poświadczenia administracyjne, aby uruchomić regedit.</span><span class="sxs-lookup"><span data-stu-id="d79d9-242">You must have administrative credentials to run regedit.</span></span>

01. <span data-ttu-id="d79d9-243">Otwórz podklucz pasujący do wersji, którą chcesz sprawdzić.</span><span class="sxs-lookup"><span data-stu-id="d79d9-243">Open the subkey that matches the version you want to check.</span></span> <span data-ttu-id="d79d9-244">Skorzystaj z tabeli w sekcji [wykrywanie .NET Framework 1,0 do 4,0](#detect-net-framework-10-through-40) .</span><span class="sxs-lookup"><span data-stu-id="d79d9-244">Use the table in the [Detect .NET Framework 1.0 through 4.0](#detect-net-framework-10-through-40) section.</span></span>

    <span data-ttu-id="d79d9-245">Na poniższej ilustracji przedstawiono podklucz i jego wartość **wersji** dla .NET Framework 3,5.</span><span class="sxs-lookup"><span data-stu-id="d79d9-245">The following figure shows the subkey and its **Version** value for .NET Framework 3.5.</span></span>

    <span data-ttu-id="d79d9-246">![Wpis rejestru dla .NET Framework 3,5.](./media/net-4-and-earlier.png ".NET Framework 3,5 i wcześniejsze wersje")</span><span class="sxs-lookup"><span data-stu-id="d79d9-246">![The registry entry for .NET Framework 3.5.](./media/net-4-and-earlier.png ".NET Framework 3.5 and earlier versions")</span></span>

### <a name="query-the-registry-using-code-older-framework-versions"></a><span data-ttu-id="d79d9-247">Wykonywanie zapytania dotyczącego rejestru przy użyciu kodu (starsze wersje Framework)</span><span class="sxs-lookup"><span data-stu-id="d79d9-247">Query the registry using code (older framework versions)</span></span>

<span data-ttu-id="d79d9-248">Użyj <xref:Microsoft.Win32.RegistryKey?displayProperty=nameWithType> klasy, aby uzyskać HKEY_LOCAL_MACHINE dostęp do podklucza **\\ \\ NDP oprogramowania Microsoft \\ .NET Framework Instalatora \\** w rejestrze systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="d79d9-248">Use the <xref:Microsoft.Win32.RegistryKey?displayProperty=nameWithType> class to access the **HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\NET Framework Setup\\NDP** subkey in the Windows registry.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d79d9-249">Jeśli uruchomiona aplikacja jest 32-bitowa i działa w 64-bitowym systemie Windows, ścieżki rejestru będą inne niż wymienione wcześniej.</span><span class="sxs-lookup"><span data-stu-id="d79d9-249">If the app you're running is 32-bit and running in 64-bit Windows, the registry paths will be different than previously listed.</span></span> <span data-ttu-id="d79d9-250">Rejestr 64-bitowy jest dostępny HKEY_LOCAL_MACHINE w podkluczu **\\ \\ Wow6432Node \\ oprogramowania** .</span><span class="sxs-lookup"><span data-stu-id="d79d9-250">The 64-bit registry is available in the **HKEY_LOCAL_MACHINE\\SOFTWARE\\Wow6432Node\\** subkey.</span></span> <span data-ttu-id="d79d9-251">Na przykład podklucz rejestru dla .NET Framework 3,5 jest **HKEY_LOCAL_MACHINE \\ oprogramowania \\ Wow6432Node \\ Microsoft \\ .NET Framework Setup \\ NDP \\ v 3.5**.</span><span class="sxs-lookup"><span data-stu-id="d79d9-251">For example, the registry subkey for .NET Framework 3.5 is **HKEY_LOCAL_MACHINE\\SOFTWARE\\Wow6432Node\\Microsoft\\NET Framework Setup\\NDP\\v3.5**.</span></span>

<span data-ttu-id="d79d9-252">Poniższy przykład umożliwia znalezienie zainstalowanych wersji .NET Framework 1-4:</span><span class="sxs-lookup"><span data-stu-id="d79d9-252">The following example finds the versions of .NET Framework 1-4 that are installed:</span></span>

:::code language="csharp" source="snippets/csharp/versions-installed.cs" id="1":::

:::code language="vb" source="snippets/visual-basic/versions-installed.vb" id="1":::

<span data-ttu-id="d79d9-253">W przykładzie przedstawiono dane wyjściowe podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="d79d9-253">The example displays output similar to the following:</span></span>

```output
v2.0.50727  2.0.50727.4927  SP2
v3.0  3.0.30729.4926  SP2
v3.5  3.5.30729.4926  SP1
v4.0
  Client  4.0.0.0
```

## <a name="find-clr-versions"></a><span data-ttu-id="d79d9-254">Znajdź wersje środowiska CLR</span><span class="sxs-lookup"><span data-stu-id="d79d9-254">Find CLR versions</span></span>

<span data-ttu-id="d79d9-255">.NET Framework środowisko CLR zainstalowane z .NET Framework jest używane oddzielnie.</span><span class="sxs-lookup"><span data-stu-id="d79d9-255">The .NET Framework CLR installed with .NET Framework is versioned separately.</span></span> <span data-ttu-id="d79d9-256">Istnieją dwa sposoby wykrywania wersji .NET Framework CLR:</span><span class="sxs-lookup"><span data-stu-id="d79d9-256">There are two ways to detect the version of the .NET Framework CLR:</span></span>

- <span data-ttu-id="d79d9-257">**Narzędzie Clrver.exe**</span><span class="sxs-lookup"><span data-stu-id="d79d9-257">**The Clrver.exe tool**</span></span>

  <span data-ttu-id="d79d9-258">Użyj [Narzędzia wersji środowiska CLR (Clrver.exe)](../tools/clrver-exe-clr-version-tool.md) , aby określić, które wersje środowiska CLR są zainstalowane na komputerze.</span><span class="sxs-lookup"><span data-stu-id="d79d9-258">Use the [CLR Version tool (Clrver.exe)](../tools/clrver-exe-clr-version-tool.md) to determine which versions of the CLR are installed on a computer.</span></span> <span data-ttu-id="d79d9-259">Otwórz [wiersz polecenia dla deweloperów dla programu Visual Studio](../tools/developer-command-prompt-for-vs.md) i wprowadź `clrver` .</span><span class="sxs-lookup"><span data-stu-id="d79d9-259">Open the [Developer Command Prompt for Visual Studio](../tools/developer-command-prompt-for-vs.md) and enter `clrver`.</span></span>

  <span data-ttu-id="d79d9-260">Przykładowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="d79d9-260">Sample output:</span></span>

  ```console
  Versions installed on the machine:
  v2.0.50727
  v4.0.30319
  ```

- <span data-ttu-id="d79d9-261">**`Environment`Klasa**</span><span class="sxs-lookup"><span data-stu-id="d79d9-261">**The `Environment` class**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="d79d9-262">W przypadku .NET Framework 4,5 i nowszych wersji nie należy używać <xref:System.Environment.Version%2A?displayProperty=nameWithType> właściwości do wykrywania wersji środowiska CLR.</span><span class="sxs-lookup"><span data-stu-id="d79d9-262">For .NET Framework 4.5 and later versions, don't use the <xref:System.Environment.Version%2A?displayProperty=nameWithType> property to detect the version of the CLR.</span></span> <span data-ttu-id="d79d9-263">Zamiast tego należy wykonać zapytanie dotyczące rejestru zgodnie z opisem w artykule [wykrywanie .NET Framework 4,5 i nowszych wersji](#detect-net-framework-45-and-later-versions).</span><span class="sxs-lookup"><span data-stu-id="d79d9-263">Instead, query the registry as described in [Detect .NET Framework 4.5 and later versions](#detect-net-framework-45-and-later-versions).</span></span>

  1. <span data-ttu-id="d79d9-264">Zbadaj <xref:System.Environment.Version?displayProperty=nameWithType> Właściwość w celu pobrania <xref:System.Version> obiektu.</span><span class="sxs-lookup"><span data-stu-id="d79d9-264">Query the <xref:System.Environment.Version?displayProperty=nameWithType> property to retrieve a <xref:System.Version> object.</span></span>

     <span data-ttu-id="d79d9-265">Zwrócony `System.Version` obiekt identyfikuje wersję środowiska uruchomieniowego, które aktualnie wykonuje kod.</span><span class="sxs-lookup"><span data-stu-id="d79d9-265">The returned `System.Version` object identifies the version of the runtime that's currently executing the code.</span></span> <span data-ttu-id="d79d9-266">Nie zwraca wersji zestawu ani innych wersji środowiska uruchomieniowego, które mogły zostać zainstalowane na komputerze.</span><span class="sxs-lookup"><span data-stu-id="d79d9-266">It doesn't return assembly versions or other versions of the runtime that may have been installed on the computer.</span></span>

     <span data-ttu-id="d79d9-267">W przypadku .NET Framework w wersji 4, 4,5, 4.5.1 i 4.5.2 ciąg reprezentujący zwracanego <xref:System.Version> obiektu ma postać 4.0.30319.*XXXXX*, gdzie *XXXXX* jest mniejszy niż 42000.</span><span class="sxs-lookup"><span data-stu-id="d79d9-267">For .NET Framework versions 4, 4.5, 4.5.1, and 4.5.2, the string representation of the returned <xref:System.Version> object has the form 4.0.30319.*xxxxx*, where *xxxxx* is less than 42000.</span></span> <span data-ttu-id="d79d9-268">W przypadku .NET Framework 4,6 i nowszych wersje ma postać 4.0.30319.42000.</span><span class="sxs-lookup"><span data-stu-id="d79d9-268">For .NET Framework 4.6 and later versions, it has the form 4.0.30319.42000.</span></span>

  1. <span data-ttu-id="d79d9-269">Po utworzeniu obiektu **wersji** wykonaj zapytanie w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="d79d9-269">After you have the **Version** object, query it as follows:</span></span>

     - <span data-ttu-id="d79d9-270">Aby uzyskać informacje o głównym identyfikatorze wydania (na przykład *4* dla wersji 4,0), użyj <xref:System.Version.Major%2A?displayProperty=nameWithType> właściwości.</span><span class="sxs-lookup"><span data-stu-id="d79d9-270">For the major release identifier (for example, *4* for version 4.0), use the <xref:System.Version.Major%2A?displayProperty=nameWithType> property.</span></span>

     - <span data-ttu-id="d79d9-271">W przypadku pomocniczego identyfikatora wydania (na przykład *0* w przypadku wersji 4,0) należy użyć <xref:System.Version.Minor%2A?displayProperty=nameWithType> właściwości.</span><span class="sxs-lookup"><span data-stu-id="d79d9-271">For the minor release identifier (for example, *0* for version 4.0), use the <xref:System.Version.Minor%2A?displayProperty=nameWithType> property.</span></span>

     - <span data-ttu-id="d79d9-272">Dla całego ciągu wersji (na przykład *4.0.30319.18010*) Użyj <xref:System.Version.ToString%2A?displayProperty=nameWithType> metody.</span><span class="sxs-lookup"><span data-stu-id="d79d9-272">For the entire version string (for example, *4.0.30319.18010*), use the <xref:System.Version.ToString%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="d79d9-273">Ta metoda zwraca pojedynczą wartość odzwierciedlającą wersję środowiska uruchomieniowego, które wykonuje kod.</span><span class="sxs-lookup"><span data-stu-id="d79d9-273">This method returns a single value that reflects the version of the runtime that's executing the code.</span></span> <span data-ttu-id="d79d9-274">Nie zwraca wersji zestawu ani innych wersji środowiska uruchomieniowego, które mogą być zainstalowane na komputerze.</span><span class="sxs-lookup"><span data-stu-id="d79d9-274">It doesn't return assembly versions or other runtime versions that may be installed on the computer.</span></span>

  <span data-ttu-id="d79d9-275">W poniższym przykładzie zastosowano <xref:System.Environment.Version%2A?displayProperty=nameWithType> Właściwość w celu pobrania informacji o wersji środowiska CLR:</span><span class="sxs-lookup"><span data-stu-id="d79d9-275">The following example uses the <xref:System.Environment.Version%2A?displayProperty=nameWithType> property to retrieve CLR version information:</span></span>

  ```csharp
  Console.WriteLine($"Version: {Environment.Version}");
  ```

  ```vb
  Console.WriteLine($"Version: {Environment.Version}")
  ```

  <span data-ttu-id="d79d9-276">W przykładzie przedstawiono dane wyjściowe podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="d79d9-276">The example displays output similar to the following:</span></span>

  ```output
  Version: 4.0.30319.18010
  ```

## <a name="see-also"></a><span data-ttu-id="d79d9-277">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="d79d9-277">See also</span></span>

- [<span data-ttu-id="d79d9-278">Instrukcje: Określanie, które aktualizacje .NET Framework są zainstalowane</span><span class="sxs-lookup"><span data-stu-id="d79d9-278">How to: Determine which .NET Framework updates are installed</span></span>](how-to-determine-which-net-framework-updates-are-installed.md)
- [<span data-ttu-id="d79d9-279">Zainstaluj .NET Framework dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="d79d9-279">Install .NET Framework for developers</span></span>](../install/guide-for-developers.md)
- [<span data-ttu-id="d79d9-280">.NET Framework wersje i zależności</span><span class="sxs-lookup"><span data-stu-id="d79d9-280">.NET Framework versions and dependencies</span></span>](versions-and-dependencies.md)
