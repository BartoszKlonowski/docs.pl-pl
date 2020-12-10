---
title: Zainstaluj platformę .NET na macOS
description: Dowiedz się więcej na temat wersji programu macOS, na których można zainstalować platformę .NET.
author: adegeo
ms.author: adegeo
ms.date: 11/10/2020
ms.openlocfilehash: b1434938a8e8e81da81e495a6b99e6c99467aae1
ms.sourcegitcommit: 81f1bba2c97a67b5ca76bcc57b37333ffca60c7b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/10/2020
ms.locfileid: "97009361"
---
# <a name="install-net-on-macos"></a><span data-ttu-id="90068-103">Zainstaluj platformę .NET na macOS</span><span class="sxs-lookup"><span data-stu-id="90068-103">Install .NET on macOS</span></span>

> [!div class="op_single_selector"]
>
> - [Instalowanie w systemie Windows](windows.md)
> - [Instalowanie w systemie macOS](macos.md)
> - [Instalowanie w systemie Linux](linux.md)

<span data-ttu-id="90068-107">W tym artykule dowiesz się, jak zainstalować platformę .NET na macOS.</span><span class="sxs-lookup"><span data-stu-id="90068-107">In this article, you'll learn how to install .NET on macOS.</span></span> <span data-ttu-id="90068-108">Platforma .NET składa się z środowiska uruchomieniowego i zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="90068-108">.NET is made up of the runtime and the SDK.</span></span> <span data-ttu-id="90068-109">Środowisko uruchomieniowe służy do uruchamiania aplikacji .NET i może nie być dołączone do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="90068-109">The runtime is used to run a .NET app and may or may not be included with the app.</span></span> <span data-ttu-id="90068-110">Zestaw SDK służy do tworzenia aplikacji i bibliotek platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="90068-110">The SDK is used to create .NET apps and libraries.</span></span> <span data-ttu-id="90068-111">Środowisko uruchomieniowe .NET jest zawsze instalowane z zestawem SDK.</span><span class="sxs-lookup"><span data-stu-id="90068-111">The .NET runtime is always installed with the SDK.</span></span>

<span data-ttu-id="90068-112">Najnowsza wersja platformy .NET to 5,0.</span><span class="sxs-lookup"><span data-stu-id="90068-112">The latest version of .NET is 5.0.</span></span>

> [!div class="button"]
> [<span data-ttu-id="90068-113">Pobierz program .NET Core</span><span class="sxs-lookup"><span data-stu-id="90068-113">Download .NET Core</span></span>](https://dotnet.microsoft.com/download/dotnet-core)

## <a name="supported-releases"></a><span data-ttu-id="90068-114">Obsługiwane wersje</span><span class="sxs-lookup"><span data-stu-id="90068-114">Supported releases</span></span>

<span data-ttu-id="90068-115">Poniższa tabela zawiera listę obecnie obsługiwanych wersji platformy .NET i wersje macOS, w których są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="90068-115">The following table is a list of currently supported .NET releases and the versions of macOS they're supported on.</span></span> <span data-ttu-id="90068-116">Te wersje pozostają obsługiwane albo wersja [platformy .NET osiągnie koniec obsługi](https://dotnet.microsoft.com/platform/support/policy/dotnet-core).</span><span class="sxs-lookup"><span data-stu-id="90068-116">These versions remain supported either the version of [.NET reaches end-of-support](https://dotnet.microsoft.com/platform/support/policy/dotnet-core).</span></span>

- <span data-ttu-id="90068-117">✔️ wskazuje, że wersja platformy .NET Core jest nadal obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="90068-117">A ✔️ indicates that the version of .NET Core is still supported.</span></span>
- <span data-ttu-id="90068-118">❌Wskazuje, że wersja programu .NET Core nie jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="90068-118">A ❌ indicates that the version of .NET Core isn't supported.</span></span>

| <span data-ttu-id="90068-119">System operacyjny</span><span class="sxs-lookup"><span data-stu-id="90068-119">Operating System</span></span>          | <span data-ttu-id="90068-120">.NET Core 2.1</span><span class="sxs-lookup"><span data-stu-id="90068-120">.NET Core 2.1</span></span> | <span data-ttu-id="90068-121">.NET Core 3.1</span><span class="sxs-lookup"><span data-stu-id="90068-121">.NET Core 3.1</span></span> | <span data-ttu-id="90068-122">.NET 5.0</span><span class="sxs-lookup"><span data-stu-id="90068-122">.NET 5.0</span></span> |
|---------------------------|---------------|---------------|----------------|
| <span data-ttu-id="90068-123">macOS 11,0 "Big Sur"</span><span class="sxs-lookup"><span data-stu-id="90068-123">macOS 11.0 "Big Sur"</span></span>        | <span data-ttu-id="90068-124">✔️ 2,1 ([Informacje o wersji][release-notes-21])</span><span class="sxs-lookup"><span data-stu-id="90068-124">✔️ 2.1 ([Release notes][release-notes-21])</span></span> | <span data-ttu-id="90068-125">✔️ 3,1 ([Informacje o wersji][release-notes-31])</span><span class="sxs-lookup"><span data-stu-id="90068-125">✔️ 3.1 ([Release notes][release-notes-31])</span></span> | <span data-ttu-id="90068-126">✔️ 5,0 ([Informacje o wersji][release-notes-50])</span><span class="sxs-lookup"><span data-stu-id="90068-126">✔️ 5.0 ([Release notes][release-notes-50])</span></span> |
| <span data-ttu-id="90068-127">macOS 10,15 "Catalina"</span><span class="sxs-lookup"><span data-stu-id="90068-127">macOS 10.15 "Catalina"</span></span>    | <span data-ttu-id="90068-128">✔️ 2,1 ([Informacje o wersji][release-notes-21])</span><span class="sxs-lookup"><span data-stu-id="90068-128">✔️ 2.1 ([Release notes][release-notes-21])</span></span> | <span data-ttu-id="90068-129">✔️ 3,1 ([Informacje o wersji][release-notes-31])</span><span class="sxs-lookup"><span data-stu-id="90068-129">✔️ 3.1 ([Release notes][release-notes-31])</span></span> | <span data-ttu-id="90068-130">✔️ 5,0 ([Informacje o wersji][release-notes-50])</span><span class="sxs-lookup"><span data-stu-id="90068-130">✔️ 5.0 ([Release notes][release-notes-50])</span></span> |
| <span data-ttu-id="90068-131">macOS 10,14 "Mojave"</span><span class="sxs-lookup"><span data-stu-id="90068-131">macOS 10.14 "Mojave"</span></span>      | <span data-ttu-id="90068-132">✔️ 2,1 ([Informacje o wersji][release-notes-21])</span><span class="sxs-lookup"><span data-stu-id="90068-132">✔️ 2.1 ([Release notes][release-notes-21])</span></span> | <span data-ttu-id="90068-133">✔️ 3,1 ([Informacje o wersji][release-notes-31])</span><span class="sxs-lookup"><span data-stu-id="90068-133">✔️ 3.1 ([Release notes][release-notes-31])</span></span> | <span data-ttu-id="90068-134">✔️ 5,0 ([Informacje o wersji][release-notes-50])</span><span class="sxs-lookup"><span data-stu-id="90068-134">✔️ 5.0 ([Release notes][release-notes-50])</span></span> |
| <span data-ttu-id="90068-135">macOS 10,13 "wysoka firma Sierra"</span><span class="sxs-lookup"><span data-stu-id="90068-135">macOS 10.13 "High Sierra"</span></span> | <span data-ttu-id="90068-136">✔️ 2,1 ([Informacje o wersji][release-notes-21])</span><span class="sxs-lookup"><span data-stu-id="90068-136">✔️ 2.1 ([Release notes][release-notes-21])</span></span> | <span data-ttu-id="90068-137">✔️ 3,1 ([Informacje o wersji][release-notes-31])</span><span class="sxs-lookup"><span data-stu-id="90068-137">✔️ 3.1 ([Release notes][release-notes-31])</span></span> | <span data-ttu-id="90068-138">✔️ 5,0 ([Informacje o wersji][release-notes-50])</span><span class="sxs-lookup"><span data-stu-id="90068-138">✔️ 5.0 ([Release notes][release-notes-50])</span></span> |
| <span data-ttu-id="90068-139">macOS 10,12 "Sierra"</span><span class="sxs-lookup"><span data-stu-id="90068-139">macOS 10.12 "Sierra"</span></span>      | <span data-ttu-id="90068-140">✔️ 2,1 ([Informacje o wersji][release-notes-21])</span><span class="sxs-lookup"><span data-stu-id="90068-140">✔️ 2.1 ([Release notes][release-notes-21])</span></span> | <span data-ttu-id="90068-141">❌ 3,1 ([Informacje o wersji][release-notes-31])</span><span class="sxs-lookup"><span data-stu-id="90068-141">❌ 3.1 ([Release notes][release-notes-31])</span></span> | <span data-ttu-id="90068-142">❌ 5,0 ([Informacje o wersji][release-notes-50])</span><span class="sxs-lookup"><span data-stu-id="90068-142">❌ 5.0 ([Release notes][release-notes-50])</span></span> |

## <a name="unsupported-releases"></a><span data-ttu-id="90068-143">Nieobsługiwane wersje</span><span class="sxs-lookup"><span data-stu-id="90068-143">Unsupported releases</span></span>

<span data-ttu-id="90068-144">Następujące wersje platformy .NET nie są ❌ już obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="90068-144">The following versions of .NET are ❌ no longer supported.</span></span> <span data-ttu-id="90068-145">Pliki do pobrania dla tych nadal są publikowane:</span><span class="sxs-lookup"><span data-stu-id="90068-145">The downloads for these still remain published:</span></span>

- <span data-ttu-id="90068-146">3,0 ([Informacje o wersji][release-notes-30])</span><span class="sxs-lookup"><span data-stu-id="90068-146">3.0 ([Release notes][release-notes-30])</span></span>
- <span data-ttu-id="90068-147">2,2 ([Informacje o wersji][release-notes-22])</span><span class="sxs-lookup"><span data-stu-id="90068-147">2.2 ([Release notes][release-notes-22])</span></span>
- <span data-ttu-id="90068-148">2,0 ([Informacje o wersji][release-notes-20])</span><span class="sxs-lookup"><span data-stu-id="90068-148">2.0 ([Release notes][release-notes-20])</span></span>

## <a name="runtime-information"></a><span data-ttu-id="90068-149">Informacje o środowisku uruchomieniowym</span><span class="sxs-lookup"><span data-stu-id="90068-149">Runtime information</span></span>

<span data-ttu-id="90068-150">Środowisko uruchomieniowe służy do uruchamiania aplikacji utworzonych przy użyciu platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="90068-150">The runtime is used to run apps created with .NET.</span></span> <span data-ttu-id="90068-151">Gdy autor aplikacji publikuje aplikację, może ona obejmować środowisko uruchomieniowe wraz z ich aplikacjami.</span><span class="sxs-lookup"><span data-stu-id="90068-151">When an app author publishes an app, they can include the runtime with their app.</span></span> <span data-ttu-id="90068-152">Jeśli nie obejmują środowiska uruchomieniowego, można zainstalować środowisko uruchomieniowe.</span><span class="sxs-lookup"><span data-stu-id="90068-152">If they don't include the runtime, it's up to the user to install the runtime.</span></span>

<span data-ttu-id="90068-153">Istnieją trzy różne środowiska uruchomieniowe, które można zainstalować w systemie macOS:</span><span class="sxs-lookup"><span data-stu-id="90068-153">There are three different runtimes you can install on macOS:</span></span>

<span data-ttu-id="90068-154">*Środowisko uruchomieniowe ASP.NET Core*</span><span class="sxs-lookup"><span data-stu-id="90068-154">*ASP.NET Core runtime*</span></span>\
<span data-ttu-id="90068-155">Uruchamia ASP.NET Core aplikacje.</span><span class="sxs-lookup"><span data-stu-id="90068-155">Runs ASP.NET Core apps.</span></span> <span data-ttu-id="90068-156">Obejmuje środowisko uruchomieniowe platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="90068-156">Includes the .NET runtime.</span></span>

<span data-ttu-id="90068-157">*Środowisko uruchomieniowe platformy .NET*</span><span class="sxs-lookup"><span data-stu-id="90068-157">*.NET runtime*</span></span>\
<span data-ttu-id="90068-158">To środowisko uruchomieniowe jest najprostszym środowiskiem uruchomieniowym i nie zawiera żadnego innego środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="90068-158">This runtime is the simplest runtime and doesn't include any other runtime.</span></span> <span data-ttu-id="90068-159">Zdecydowanie zaleca się zainstalowanie *ASP.NET Core środowiska uruchomieniowego* w celu uzyskania najlepszej zgodności z aplikacjami .NET.</span><span class="sxs-lookup"><span data-stu-id="90068-159">It's highly recommended that you install *ASP.NET Core runtime* for the best compatibility with .NET apps.</span></span>

> [!div class="button"]
> [<span data-ttu-id="90068-160">Pobierz środowisko uruchomieniowe platformy .NET</span><span class="sxs-lookup"><span data-stu-id="90068-160">Download .NET Runtime</span></span>](https://dotnet.microsoft.com/download/dotnet-core)

## <a name="sdk-information"></a><span data-ttu-id="90068-161">Informacje o zestawie SDK</span><span class="sxs-lookup"><span data-stu-id="90068-161">SDK information</span></span>

<span data-ttu-id="90068-162">Zestaw SDK służy do kompilowania i publikowania aplikacji i bibliotek platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="90068-162">The SDK is used to build and publish .NET apps and libraries.</span></span> <span data-ttu-id="90068-163">Instalowanie zestawu SDK obejmuje zarówno [środowisko uruchomieniowe](#runtime-information): ASP.NET Core, jak i .NET.</span><span class="sxs-lookup"><span data-stu-id="90068-163">Installing the SDK includes both [runtimes](#runtime-information): ASP.NET Core and .NET.</span></span>

## <a name="dependencies"></a><span data-ttu-id="90068-164">Zależności</span><span class="sxs-lookup"><span data-stu-id="90068-164">Dependencies</span></span>

<span data-ttu-id="90068-165">Platforma .NET jest obsługiwana w następujących wersjach macOS:</span><span class="sxs-lookup"><span data-stu-id="90068-165">.NET is supported on the following macOS releases:</span></span>

> [!NOTE]
> <span data-ttu-id="90068-166">`+`Symbol reprezentuje wersję minimalną.</span><span class="sxs-lookup"><span data-stu-id="90068-166">A `+` symbol represents the minimum version.</span></span>

| <span data-ttu-id="90068-167">Wersja platformy .NET Core</span><span class="sxs-lookup"><span data-stu-id="90068-167">.NET Core Version</span></span> | <span data-ttu-id="90068-168">macOS</span><span class="sxs-lookup"><span data-stu-id="90068-168">macOS</span></span>                 | <span data-ttu-id="90068-169">Architektury</span><span class="sxs-lookup"><span data-stu-id="90068-169">Architectures</span></span> | <span data-ttu-id="90068-170">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="90068-170">More information</span></span>    |
| ----------------- | --------------------- | --------------| --- |
| <span data-ttu-id="90068-171">5,0</span><span class="sxs-lookup"><span data-stu-id="90068-171">5.0</span></span>               | <span data-ttu-id="90068-172">Wysoka firma Sierra (10.13 +)</span><span class="sxs-lookup"><span data-stu-id="90068-172">High Sierra (10.13+)</span></span>  | <span data-ttu-id="90068-173">x64</span><span class="sxs-lookup"><span data-stu-id="90068-173">x64</span></span> | [<span data-ttu-id="90068-174">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="90068-174">More information</span></span>](https://github.com/dotnet/core/blob/master/release-notes/5.0/5.0-supported-os.md) |
| <span data-ttu-id="90068-175">3,1</span><span class="sxs-lookup"><span data-stu-id="90068-175">3.1</span></span>               | <span data-ttu-id="90068-176">Wysoka firma Sierra (10.13 +)</span><span class="sxs-lookup"><span data-stu-id="90068-176">High Sierra (10.13+)</span></span>  | <span data-ttu-id="90068-177">x64</span><span class="sxs-lookup"><span data-stu-id="90068-177">x64</span></span> | [<span data-ttu-id="90068-178">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="90068-178">More information</span></span>](https://github.com/dotnet/core/blob/master/release-notes/3.1/3.1-supported-os.md) |
| <span data-ttu-id="90068-179">3.0</span><span class="sxs-lookup"><span data-stu-id="90068-179">3.0</span></span>               | <span data-ttu-id="90068-180">Wysoka firma Sierra (10.13 +)</span><span class="sxs-lookup"><span data-stu-id="90068-180">High Sierra (10.13+)</span></span>  | <span data-ttu-id="90068-181">x64</span><span class="sxs-lookup"><span data-stu-id="90068-181">x64</span></span> | [<span data-ttu-id="90068-182">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="90068-182">More information</span></span>](https://github.com/dotnet/core/blob/master/release-notes/3.0/3.0-supported-os.md) |
| <span data-ttu-id="90068-183">2.2</span><span class="sxs-lookup"><span data-stu-id="90068-183">2.2</span></span>               | <span data-ttu-id="90068-184">Sierra (10.12 +)</span><span class="sxs-lookup"><span data-stu-id="90068-184">Sierra (10.12+)</span></span>       | <span data-ttu-id="90068-185">x64</span><span class="sxs-lookup"><span data-stu-id="90068-185">x64</span></span> | [<span data-ttu-id="90068-186">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="90068-186">More information</span></span>](https://github.com/dotnet/core/blob/master/release-notes/2.2/2.2-supported-os.md) |
| <span data-ttu-id="90068-187">2.1</span><span class="sxs-lookup"><span data-stu-id="90068-187">2.1</span></span>               | <span data-ttu-id="90068-188">Sierra (10.12 +)</span><span class="sxs-lookup"><span data-stu-id="90068-188">Sierra (10.12+)</span></span>       | <span data-ttu-id="90068-189">x64</span><span class="sxs-lookup"><span data-stu-id="90068-189">x64</span></span> | [<span data-ttu-id="90068-190">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="90068-190">More information</span></span>](https://github.com/dotnet/core/blob/master/release-notes/2.1/2.1-supported-os.md) |

<span data-ttu-id="90068-191">Począwszy od programu macOS Catalina (wersja 10,15), całe oprogramowanie skompilowane po 1 czerwca 2019, które jest dystrybuowane z IDENTYFIKATORem dewelopera, musi być notarialne.</span><span class="sxs-lookup"><span data-stu-id="90068-191">Beginning with macOS Catalina (version 10.15), all software built after June 1, 2019 that is distributed with Developer ID, must be notarized.</span></span> <span data-ttu-id="90068-192">To wymaganie dotyczy środowiska uruchomieniowego .NET, zestawu .NET SDK i oprogramowania utworzonego przy użyciu platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="90068-192">This requirement applies to the .NET runtime, .NET SDK, and software created with .NET.</span></span>

<span data-ttu-id="90068-193">Programy instalacyjne środowiska uruchomieniowego i zestawu SDK dla programów .NET 5,0 i .NET Core 3,1, 3,0 i 2,1 zostały zgłoszone od 18 lutego 2020.</span><span class="sxs-lookup"><span data-stu-id="90068-193">The runtime and SDK installers for .NET 5.0 and .NET Core 3.1, 3.0, and 2.1, have been notarized since February 18, 2020.</span></span> <span data-ttu-id="90068-194">Wcześniejsze wersje nie zostały ujawnione.</span><span class="sxs-lookup"><span data-stu-id="90068-194">Prior released versions aren't notarized.</span></span> <span data-ttu-id="90068-195">Jeśli uruchomisz zanotarialną aplikację, zobaczysz komunikat o błędzie podobny do następującego:</span><span class="sxs-lookup"><span data-stu-id="90068-195">If you run a non-notarized app, you'll see an error similar to the following image:</span></span>

![Alert notarization macOS Catalina](media/dependencies/macos-notarized-pkg-warning.png)

<span data-ttu-id="90068-197">Aby uzyskać więcej informacji na temat sposobu, w jaki wymuszone — notarization wpływa na platformę .NET (i aplikacje .NET), zobacz [Praca z MacOS Catalina notarization](macos-notarization-issues.md).</span><span class="sxs-lookup"><span data-stu-id="90068-197">For more information about how enforced-notarization affects .NET (and your .NET apps), see [Working with macOS Catalina Notarization](macos-notarization-issues.md).</span></span>

## <a name="libgdiplus"></a><span data-ttu-id="90068-198">libgdiplus</span><span class="sxs-lookup"><span data-stu-id="90068-198">libgdiplus</span></span>

<span data-ttu-id="90068-199">Aplikacje .NET, które używają zestawu *System. Drawing. Common* , wymagają zainstalowania libgdiplus.</span><span class="sxs-lookup"><span data-stu-id="90068-199">.NET applications that use the *System.Drawing.Common* assembly require libgdiplus to be installed.</span></span>

<span data-ttu-id="90068-200">Łatwym sposobem uzyskania libgdiplus jest użycie Menedżera pakietów [oprogramowania homebrew ("rozwiązania brew")](https://brew.sh/) dla macOS.</span><span class="sxs-lookup"><span data-stu-id="90068-200">An easy way to obtain libgdiplus is by using the [Homebrew ("brew")](https://brew.sh/) package manager for macOS.</span></span> <span data-ttu-id="90068-201">Po zainstalowaniu *rozwiązania brew* Zainstaluj libgdiplus, wykonując następujące polecenia w wierszu terminalu (polecenie):</span><span class="sxs-lookup"><span data-stu-id="90068-201">After installing *brew*, install libgdiplus by executing the following commands at a Terminal (command) prompt:</span></span>

```console
brew update
brew install mono-libgdiplus
```

## <a name="install-with-an-installer"></a><span data-ttu-id="90068-202">Instalowanie za pomocą Instalatora</span><span class="sxs-lookup"><span data-stu-id="90068-202">Install with an installer</span></span>

<span data-ttu-id="90068-203">macOS ma autonomiczne Instalatory, których można użyć do zainstalowania zestawu .NET 5,0 SDK:</span><span class="sxs-lookup"><span data-stu-id="90068-203">macOS has standalone installers that can be used to install the .NET 5.0 SDK:</span></span>

- [<span data-ttu-id="90068-204">Procesory x64 (64-bitowe)</span><span class="sxs-lookup"><span data-stu-id="90068-204">x64 (64-bit) CPUs</span></span>](https://dotnet.microsoft.com/download/dotnet-core/5.0)

## <a name="download-and-manually-install"></a><span data-ttu-id="90068-205">Pobierz i ręcznie zainstaluj</span><span class="sxs-lookup"><span data-stu-id="90068-205">Download and manually install</span></span>

<!-- Note, this content is taken from includes/linux-install-manual.md but changed for macOS. Any fixes should be applied there too, though content may be different -->

<span data-ttu-id="90068-206">Jako alternatywę dla instalatorów macOS dla platformy .NET można pobrać i ręcznie zainstalować zestaw SDK i środowisko uruchomieniowe.</span><span class="sxs-lookup"><span data-stu-id="90068-206">As an alternative to the macOS installers for .NET, you can download and manually install the SDK and runtime.</span></span> <span data-ttu-id="90068-207">Instalacja ręczna jest zwykle wykonywana w ramach testowania ciągłej integracji.</span><span class="sxs-lookup"><span data-stu-id="90068-207">Manual install is usually performed as part of continuous integration testing.</span></span> <span data-ttu-id="90068-208">Dla deweloperów lub użytkowników zazwyczaj lepiej jest użyć [Instalatora](https://dotnet.microsoft.com/download/dotnet-core).</span><span class="sxs-lookup"><span data-stu-id="90068-208">For a developer or user, it's generally better to use an [installer](https://dotnet.microsoft.com/download/dotnet-core).</span></span>

<span data-ttu-id="90068-209">W przypadku instalowania zestawu .NET SDK nie trzeba instalować odpowiedniego środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="90068-209">If you install .NET SDK, you don't need to install the corresponding runtime.</span></span> <span data-ttu-id="90068-210">Najpierw pobierz wydanie **binarne** dla zestawu SDK lub środowiska uruchomieniowego z jednej z następujących lokacji:</span><span class="sxs-lookup"><span data-stu-id="90068-210">First, download a **binary** release for either the SDK or the runtime from one of the following sites:</span></span>

- <span data-ttu-id="90068-211">✔️ [pliki do pobrania w programie .net 5,0](https://dotnet.microsoft.com/download/dotnet/5.0)</span><span class="sxs-lookup"><span data-stu-id="90068-211">✔️ [.NET 5.0 downloads](https://dotnet.microsoft.com/download/dotnet/5.0)</span></span>
- <span data-ttu-id="90068-212">[pliki do pobrania ✔️ .NET Core 3,1](https://dotnet.microsoft.com/download/dotnet-core/3.1)</span><span class="sxs-lookup"><span data-stu-id="90068-212">✔️ [.NET Core 3.1 downloads](https://dotnet.microsoft.com/download/dotnet-core/3.1)</span></span>
- <span data-ttu-id="90068-213">[pliki do pobrania ✔️ .NET Core 2,1](https://dotnet.microsoft.com/download/dotnet-core/2.1)</span><span class="sxs-lookup"><span data-stu-id="90068-213">✔️ [.NET Core 2.1 downloads](https://dotnet.microsoft.com/download/dotnet-core/2.1)</span></span>
- [<span data-ttu-id="90068-214">Wszystkie pliki do pobrania z platformy .NET Core</span><span class="sxs-lookup"><span data-stu-id="90068-214">All .NET Core downloads</span></span>](https://dotnet.microsoft.com/download/dotnet-core)

<span data-ttu-id="90068-215">Następnie wyodrębnij pobrany plik i użyj polecenia, `export` Aby ustawić zmienne używane przez platformę .NET, a następnie upewnij się, że platforma .NET znajduje się w ścieżce.</span><span class="sxs-lookup"><span data-stu-id="90068-215">Next, extract the downloaded file and use the `export` command to set variables used by .NET and then ensure .NET is in PATH.</span></span>

<span data-ttu-id="90068-216">Aby wyodrębnić środowisko uruchomieniowe i udostępnić polecenie interfejsu wiersza polecenia platformy .NET w terminalu, najpierw Pobierz wydanie binarne platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="90068-216">To extract the runtime and make the .NET CLI commands available at the terminal, first download a .NET binary release.</span></span> <span data-ttu-id="90068-217">Następnie otwórz Terminal i uruchom następujące polecenia z katalogu, w którym zapisano plik.</span><span class="sxs-lookup"><span data-stu-id="90068-217">Then, open a terminal and run the following commands from the directory where the file was saved.</span></span> <span data-ttu-id="90068-218">Nazwa pliku archiwum może się różnić w zależności od pobranych informacji.</span><span class="sxs-lookup"><span data-stu-id="90068-218">The archive file name may be different depending on what you downloaded.</span></span>

<span data-ttu-id="90068-219">**Aby wyodrębnić środowisko uruchomieniowe, użyj następującego polecenia**:</span><span class="sxs-lookup"><span data-stu-id="90068-219">**Use the following command to extract the runtime**:</span></span>

```bash
mkdir -p "$HOME/dotnet" && tar zxf aspnetcore-runtime-5.0.0-osx-x64.tar.gz -C "$HOME/dotnet"
export DOTNET_ROOT=$HOME/dotnet
export PATH=$PATH:$HOME/dotnet
```

<span data-ttu-id="90068-220">**Użyj następującego polecenia, aby wyodrębnić zestaw SDK**:</span><span class="sxs-lookup"><span data-stu-id="90068-220">**Use the following command to extract the SDK**:</span></span>

```bash
mkdir -p "$HOME/dotnet" && tar zxf dotnet-sdk-5.0.100-osx-x64.tar.gz -C "$HOME/dotnet"
export DOTNET_ROOT=$HOME/dotnet
export PATH=$PATH:$HOME/dotnet
```

> [!TIP]
> <span data-ttu-id="90068-221">Powyższe `export` polecenia sprawiają, że dla sesji terminala, w której został uruchomiony, są dostępne tylko polecenia interfejsu CLI platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="90068-221">The preceding `export` commands only make the .NET CLI commands available for the terminal session in which it was run.</span></span>
>
> <span data-ttu-id="90068-222">Możesz edytować profil powłoki, aby trwale dodać polecenia.</span><span class="sxs-lookup"><span data-stu-id="90068-222">You can edit your shell profile to permanently add the commands.</span></span> <span data-ttu-id="90068-223">Istnieje wiele różnych powłok dostępnych dla systemu Linux, a każdy z nich ma inny profil.</span><span class="sxs-lookup"><span data-stu-id="90068-223">There are a number of different shells available for Linux and each has a different profile.</span></span> <span data-ttu-id="90068-224">Przykład:</span><span class="sxs-lookup"><span data-stu-id="90068-224">For example:</span></span>
>
> - <span data-ttu-id="90068-225">**Bash Shell**: *~/.bash_profile*, *~/.bashrc.*</span><span class="sxs-lookup"><span data-stu-id="90068-225">**Bash Shell**: *~/.bash_profile*, *~/.bashrc*</span></span>
> - <span data-ttu-id="90068-226">**Powłoka Korn**: *~/.KSHRC* lub *. profile*</span><span class="sxs-lookup"><span data-stu-id="90068-226">**Korn Shell**: *~/.kshrc* or *.profile*</span></span>
> - <span data-ttu-id="90068-227">**Powłoka Z**: *~/.zshrc* lub *. zprofile*</span><span class="sxs-lookup"><span data-stu-id="90068-227">**Z Shell**: *~/.zshrc* or *.zprofile*</span></span>
>
> <span data-ttu-id="90068-228">Edytuj odpowiedni plik źródłowy dla powłoki i Dodaj `:$HOME/dotnet` na końcu istniejącej `PATH` instrukcji.</span><span class="sxs-lookup"><span data-stu-id="90068-228">Edit the appropriate source file for your shell and add `:$HOME/dotnet` to the end of the existing `PATH` statement.</span></span> <span data-ttu-id="90068-229">Jeśli `PATH` instrukcja nie jest uwzględniona, Dodaj nowy wiersz za pomocą `export PATH=$PATH:$HOME/dotnet` .</span><span class="sxs-lookup"><span data-stu-id="90068-229">If no `PATH` statement is included, add a new line with `export PATH=$PATH:$HOME/dotnet`.</span></span>
>
> <span data-ttu-id="90068-230">Ponadto Dodaj `export DOTNET_ROOT=$HOME/dotnet` na końcu pliku.</span><span class="sxs-lookup"><span data-stu-id="90068-230">Also, add `export DOTNET_ROOT=$HOME/dotnet` to the end of the file.</span></span>

<span data-ttu-id="90068-231">Takie podejście umożliwia zainstalowanie różnych wersji w oddzielnych lokalizacjach i wybór jawny, który ma być używany przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="90068-231">This approach lets you install different versions into separate locations and choose explicitly which one to use by which application.</span></span>

## <a name="install-with-visual-studio-for-mac"></a><span data-ttu-id="90068-232">Zainstaluj przy użyciu Visual Studio dla komputerów Mac</span><span class="sxs-lookup"><span data-stu-id="90068-232">Install with Visual Studio for Mac</span></span>

<span data-ttu-id="90068-233">Visual Studio dla komputerów Mac instaluje zestaw .NET SDK przy wybranym obciążeniu **.NET** .</span><span class="sxs-lookup"><span data-stu-id="90068-233">Visual Studio for Mac installs the .NET SDK when the **.NET** workload is selected.</span></span> <span data-ttu-id="90068-234">Aby rozpocząć programowanie na platformie .NET w systemie macOS, zobacz [Instalowanie programu Visual Studio 2019 for Mac](/visualstudio/mac/installation).</span><span class="sxs-lookup"><span data-stu-id="90068-234">To get started with .NET development on macOS, see [Install Visual Studio 2019 for Mac](/visualstudio/mac/installation).</span></span>

| <span data-ttu-id="90068-235">Wersja zestawu SDK platformy .NET</span><span class="sxs-lookup"><span data-stu-id="90068-235">.NET SDK version</span></span>      | <span data-ttu-id="90068-236">Wersja programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="90068-236">Visual Studio version</span></span>                      |
| --------------------- | ------------------------------------------ |
| <span data-ttu-id="90068-237">5,0</span><span class="sxs-lookup"><span data-stu-id="90068-237">5.0</span></span>                   | <span data-ttu-id="90068-238">Program Visual Studio 2019 dla komputerów Mac w wersji 8,8 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="90068-238">Visual Studio 2019 for Mac version 8.8 or higher.</span></span> |
| <span data-ttu-id="90068-239">3,1</span><span class="sxs-lookup"><span data-stu-id="90068-239">3.1</span></span>                   | <span data-ttu-id="90068-240">Program Visual Studio 2019 dla komputerów Mac w wersji 8,4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="90068-240">Visual Studio 2019 for Mac version 8.4 or higher.</span></span> |
| <span data-ttu-id="90068-241">2.1</span><span class="sxs-lookup"><span data-stu-id="90068-241">2.1</span></span>                   | <span data-ttu-id="90068-242">Program Visual Studio 2019 dla komputerów Mac w wersji 8,0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="90068-242">Visual Studio 2019 for Mac version 8.0 or higher.</span></span> |

<span data-ttu-id="90068-243">[![macOS programu Visual Studio 2019 for Mac z funkcją obciążenia .NET](media/install-sdk/mac-install-selection.png)](media/install-sdk/mac-install-selection.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="90068-243">[![macOS Visual Studio 2019 for Mac with .NET workload feature](media/install-sdk/mac-install-selection.png)](media/install-sdk/mac-install-selection.png#lightbox)</span></span>

## <a name="install-alongside-visual-studio-code"></a><span data-ttu-id="90068-244">Zainstaluj obok Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="90068-244">Install alongside Visual Studio Code</span></span>

<span data-ttu-id="90068-245">Visual Studio Code to zaawansowany i lekki Edytor kodu źródłowego, który jest uruchamiany na pulpicie.</span><span class="sxs-lookup"><span data-stu-id="90068-245">Visual Studio Code is a powerful and lightweight source code editor that runs on your desktop.</span></span> <span data-ttu-id="90068-246">Visual Studio Code jest dostępny dla systemów Windows, macOS i Linux.</span><span class="sxs-lookup"><span data-stu-id="90068-246">Visual Studio Code is available for Windows, macOS, and Linux.</span></span>

<span data-ttu-id="90068-247">Mimo że Visual Studio Code nie jest dołączony do zautomatyzowanego Instalatora platformy .NET, takiego jak Visual Studio, Dodawanie obsługi platformy .NET jest proste.</span><span class="sxs-lookup"><span data-stu-id="90068-247">While Visual Studio Code doesn't come with an automated .NET installer like Visual Studio does, adding .NET support is simple.</span></span>

01. <span data-ttu-id="90068-248">[Pobierz i zainstaluj Visual Studio Code](https://code.visualstudio.com/Download).</span><span class="sxs-lookup"><span data-stu-id="90068-248">[Download and install Visual Studio Code](https://code.visualstudio.com/Download).</span></span>
01. <span data-ttu-id="90068-249">[Pobierz i Zainstaluj zestaw SDK platformy .NET](https://dotnet.microsoft.com/download/dotnet-core).</span><span class="sxs-lookup"><span data-stu-id="90068-249">[Download and install the .NET SDK](https://dotnet.microsoft.com/download/dotnet-core).</span></span>
01. <span data-ttu-id="90068-250">[Zainstaluj rozszerzenie C# z witryny Visual Studio Code Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp).</span><span class="sxs-lookup"><span data-stu-id="90068-250">[Install the C# extension from the Visual Studio Code marketplace](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp).</span></span>

## <a name="install-with-bash-automation"></a><span data-ttu-id="90068-251">Instalowanie przy użyciu usługi Bash Automation</span><span class="sxs-lookup"><span data-stu-id="90068-251">Install with bash automation</span></span>

<span data-ttu-id="90068-252">[Skrypty programu dotnet-Install](../tools/dotnet-install-script.md) są używane na potrzeby automatyzacji i instalacji niebędących administratorami środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="90068-252">The [dotnet-install scripts](../tools/dotnet-install-script.md) are used for automation and non-admin installs of the runtime.</span></span> <span data-ttu-id="90068-253">Skrypt można pobrać ze [strony odniesienia do skryptu dotnet-Install](../tools/dotnet-install-script.md).</span><span class="sxs-lookup"><span data-stu-id="90068-253">You can download the script from the [dotnet-install script reference page](../tools/dotnet-install-script.md).</span></span>

<span data-ttu-id="90068-254">Skrypt domyślnie instaluje najnowszą [LTS](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) wersję, która jest platformą .net Core 3,1.</span><span class="sxs-lookup"><span data-stu-id="90068-254">The script defaults to installing the latest [long term support (LTS)](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) version, which is .NET Core 3.1.</span></span> <span data-ttu-id="90068-255">Możesz wybrać określoną wersję, określając `current` przełącznik.</span><span class="sxs-lookup"><span data-stu-id="90068-255">You can choose a specific release by specifying the `current` switch.</span></span> <span data-ttu-id="90068-256">Dołącz `runtime` przełącznik, aby zainstalować środowisko uruchomieniowe.</span><span class="sxs-lookup"><span data-stu-id="90068-256">Include the `runtime` switch to install a runtime.</span></span> <span data-ttu-id="90068-257">W przeciwnym razie skrypt instaluje [zestaw SDK](./windows.md).</span><span class="sxs-lookup"><span data-stu-id="90068-257">Otherwise, the script installs the [SDK](./windows.md).</span></span>

```bash
./dotnet-install.sh --channel 5.0 --runtime aspnetcore
```

> [!NOTE]
> <span data-ttu-id="90068-258">Poprzednie polecenie instaluje środowisko uruchomieniowe ASP.NET Core, aby uzyskać maksymalną zgodność.</span><span class="sxs-lookup"><span data-stu-id="90068-258">The previous command installs the ASP.NET Core runtime for maximum compatability.</span></span> <span data-ttu-id="90068-259">Środowisko uruchomieniowe ASP.NET Core obejmuje również standardowe środowisko uruchomieniowe platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="90068-259">The ASP.NET Core runtime also includes the standard .NET runtime.</span></span>

## <a name="docker"></a><span data-ttu-id="90068-260">Docker</span><span class="sxs-lookup"><span data-stu-id="90068-260">Docker</span></span>

<span data-ttu-id="90068-261">Kontenery zapewniają lekki sposób izolowania aplikacji od pozostałej części systemu hosta.</span><span class="sxs-lookup"><span data-stu-id="90068-261">Containers provide a lightweight way to isolate your application from the rest of the host system.</span></span> <span data-ttu-id="90068-262">Kontenery na tym samym komputerze udostępniają tylko jądro i używają zasobów przyznanych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="90068-262">Containers on the same machine share just the kernel and use resources given to your application.</span></span>

<span data-ttu-id="90068-263">Środowisko .NET można uruchomić w kontenerze platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="90068-263">.NET can run in a Docker container.</span></span> <span data-ttu-id="90068-264">Oficjalne obrazy platformy .NET Docker są publikowane w Container Registry firmy Microsoft (MCR) i można je odnajdywać w [repozytorium Microsoft .NET Core Docker Hub](https://hub.docker.com/_/microsoft-dotnet/).</span><span class="sxs-lookup"><span data-stu-id="90068-264">Official .NET Docker images are published to the Microsoft Container Registry (MCR) and are discoverable at the [Microsoft .NET Core Docker Hub repository](https://hub.docker.com/_/microsoft-dotnet/).</span></span> <span data-ttu-id="90068-265">Każde repozytorium zawiera obrazy różnych kombinacji platformy .NET (zestawu SDK lub środowiska uruchomieniowego) i systemu operacyjnego, których można użyć.</span><span class="sxs-lookup"><span data-stu-id="90068-265">Each repository contains images for different combinations of the .NET (SDK or Runtime) and OS that you can use.</span></span>

<span data-ttu-id="90068-266">Firma Microsoft udostępnia obrazy dostosowane do konkretnych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="90068-266">Microsoft provides images that are tailored for specific scenarios.</span></span> <span data-ttu-id="90068-267">Na przykład [repozytorium ASP.NET Core](https://hub.docker.com/_/microsoft-dotnet-aspnet) zawiera obrazy skompilowane do uruchamiania aplikacji ASP.NET Core w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="90068-267">For example, the [ASP.NET Core repository](https://hub.docker.com/_/microsoft-dotnet-aspnet) provides images that are built for running ASP.NET Core apps in production.</span></span>

<span data-ttu-id="90068-268">Aby uzyskać więcej informacji na temat korzystania z platformy .NET Core w kontenerze platformy Docker, zobacz [wprowadzenie do oprogramowania .NET i platformy Docker](../docker/introduction.md) i [przykładów](https://github.com/dotnet/dotnet-docker/blob/master/samples/README.md).</span><span class="sxs-lookup"><span data-stu-id="90068-268">For more information about using .NET Core in a Docker container, see [Introduction to .NET and Docker](../docker/introduction.md) and [Samples](https://github.com/dotnet/dotnet-docker/blob/master/samples/README.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="90068-269">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="90068-269">Next steps</span></span>

- <span data-ttu-id="90068-270">[Jak sprawdzić, czy program .NET Core jest już zainstalowany](how-to-detect-installed-versions.md?pivots=os-macos).</span><span class="sxs-lookup"><span data-stu-id="90068-270">[How to check if .NET Core is already installed](how-to-detect-installed-versions.md?pivots=os-macos).</span></span>
- <span data-ttu-id="90068-271">[Praca z MacOS Catalina notarization](macos-notarization-issues.md).</span><span class="sxs-lookup"><span data-stu-id="90068-271">[Working with macOS Catalina notarization](macos-notarization-issues.md).</span></span>
- <span data-ttu-id="90068-272">[Samouczek: Rozpoczynanie pracy w witrynie macOS](../tutorials/with-visual-studio-mac.md).</span><span class="sxs-lookup"><span data-stu-id="90068-272">[Tutorial: Get started on macOS](../tutorials/with-visual-studio-mac.md).</span></span>
- <span data-ttu-id="90068-273">[Samouczek: Tworzenie nowej aplikacji przy użyciu Visual Studio Code](../tutorials/with-visual-studio-code.md).</span><span class="sxs-lookup"><span data-stu-id="90068-273">[Tutorial: Create a new app with Visual Studio Code](../tutorials/with-visual-studio-code.md).</span></span>
- <span data-ttu-id="90068-274">[Samouczek: konteneryzowanie aplikacji .NET Core](../docker/build-container.md).</span><span class="sxs-lookup"><span data-stu-id="90068-274">[Tutorial: Containerize a .NET Core app](../docker/build-container.md).</span></span>

[release-notes-21]: https://github.com/dotnet/core/blob/master/release-notes/2.1/2.1-supported-os.md
[release-notes-31]: https://github.com/dotnet/core/blob/master/release-notes/3.1/3.1-supported-os.md
[release-notes-50]: https://github.com/dotnet/core/blob/master/release-notes/5.0/5.0-supported-os.md
[release-notes-20]: https://github.com/dotnet/core/blob/master/release-notes/2.0/2.0-supported-os.md
[release-notes-22]: https://github.com/dotnet/core/blob/master/release-notes/2.2/2.2-supported-os.md
[release-notes-30]: https://github.com/dotnet/core/blob/master/release-notes/3.0/3.0-supported-os.md
