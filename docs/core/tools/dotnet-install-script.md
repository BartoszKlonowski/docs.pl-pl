---
title: dotnet-install scripts
description: Więcej informacji na temat skryptów programu dotnet-Install w celu zainstalowania zestaw .NET Core SDK i udostępnionego środowiska uruchomieniowego.
ms.date: 04/30/2020
ms.openlocfilehash: c3aa6549a0b521db7fc19c6ff44665e3c4ba0c5f
ms.sourcegitcommit: 1e6439ec4d5889fc08cf3bfb4dac2b91931eb827
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/08/2020
ms.locfileid: "88024657"
---
# <a name="dotnet-install-scripts-reference"></a><span data-ttu-id="90691-103">dotnet — informacje o skryptach instalacji</span><span class="sxs-lookup"><span data-stu-id="90691-103">dotnet-install scripts reference</span></span>

## <a name="name"></a><span data-ttu-id="90691-104">Nazwa</span><span class="sxs-lookup"><span data-stu-id="90691-104">Name</span></span>

<span data-ttu-id="90691-105">`dotnet-install.ps1` | `dotnet-install.sh`-Skrypt służący do instalowania zestaw .NET Core SDK i udostępnionego środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="90691-105">`dotnet-install.ps1` | `dotnet-install.sh` - Script used to install the .NET Core SDK and the shared runtime.</span></span>

## <a name="synopsis"></a><span data-ttu-id="90691-106">Streszczenie</span><span class="sxs-lookup"><span data-stu-id="90691-106">Synopsis</span></span>

<span data-ttu-id="90691-107">W systemie Windows:</span><span class="sxs-lookup"><span data-stu-id="90691-107">Windows:</span></span>

```powershell
dotnet-install.ps1 [-Architecture <ARCHITECTURE>] [-AzureFeed]
    [-Channel <CHANNEL>] [-DryRun] [-FeedCredential]
    [-InstallDir <DIRECTORY>] [-JSonFile <JSONFILE>]
    [-NoCdn] [-NoPath] [-ProxyAddress] [-ProxyBypassList <LIST_OF_URLS>]
    [-ProxyUseDefaultCredentials] [-Runtime <RUNTIME>]
    [-SkipNonVersionedFiles] [-UncachedFeed] [-Verbose]
    [-Version <VERSION>]

Get-Help ./dotnet-install.ps1
```

<span data-ttu-id="90691-108">Linux/macOS:</span><span class="sxs-lookup"><span data-stu-id="90691-108">Linux/macOS:</span></span>

```bash
dotnet-install.sh  [--architecture <ARCHITECTURE>] [--azure-feed]
    [--channel <CHANNEL>] [--dry-run] [--feed-credential]
    [--install-dir <DIRECTORY>] [--jsonfile <JSONFILE>]
    [--no-cdn] [--no-path] [--runtime <RUNTIME>] [--runtime-id <RID>]
    [--skip-non-versioned-files] [--uncached-feed] [--verbose]
    [--version <VERSION>]

dotnet-install.sh --help
```

<span data-ttu-id="90691-109">Skrypt bash odczytuje również przełączniki programu PowerShell, dzięki czemu można użyć przełączników programu PowerShell z skryptem w systemach Linux/macOS.</span><span class="sxs-lookup"><span data-stu-id="90691-109">The bash script also reads PowerShell switches, so you can use PowerShell switches with the script on Linux/macOS systems.</span></span>

## <a name="description"></a><span data-ttu-id="90691-110">Opis</span><span class="sxs-lookup"><span data-stu-id="90691-110">Description</span></span>

<span data-ttu-id="90691-111">`dotnet-install`Skrypty przeprowadzili instalację niebędącą administratorem zestaw .NET Core SDK, która obejmuje interfejs wiersza polecenia platformy .NET Core i udostępnione środowisko uruchomieniowe.</span><span class="sxs-lookup"><span data-stu-id="90691-111">The `dotnet-install` scripts perform a non-admin installation of the .NET Core SDK, which includes the .NET Core CLI and the shared runtime.</span></span> <span data-ttu-id="90691-112">Istnieją dwa skrypty:</span><span class="sxs-lookup"><span data-stu-id="90691-112">There are two scripts:</span></span>

* <span data-ttu-id="90691-113">Skrypt programu PowerShell, który działa w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="90691-113">A PowerShell script that works on Windows.</span></span>
* <span data-ttu-id="90691-114">Skrypt bash, który działa w systemie Linux/macOS.</span><span class="sxs-lookup"><span data-stu-id="90691-114">A bash script that works on Linux/macOS.</span></span>

### <a name="purpose"></a><span data-ttu-id="90691-115">Przeznaczenie</span><span class="sxs-lookup"><span data-stu-id="90691-115">Purpose</span></span>

 <span data-ttu-id="90691-116">Zamierzone użycie skryptów dotyczy scenariuszy ciągłej integracji (CI), gdzie:</span><span class="sxs-lookup"><span data-stu-id="90691-116">The intended use of the scripts is for Continuous Integration (CI) scenarios, where:</span></span>

* <span data-ttu-id="90691-117">Zestaw SDK należy zainstalować bez udziału użytkownika i bez uprawnień administratora.</span><span class="sxs-lookup"><span data-stu-id="90691-117">The SDK needs to be installed without user interaction and without admin rights.</span></span>
* <span data-ttu-id="90691-118">Instalacja zestawu SDK nie wymaga utrwalania wielu przebiegów elementów konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="90691-118">The SDK installation doesn't need to persist across multiple CI runs.</span></span>

  <span data-ttu-id="90691-119">Typowa sekwencja zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="90691-119">The typical sequence of events:</span></span>
  * <span data-ttu-id="90691-120">Wyzwalanie elementu konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="90691-120">CI is triggered.</span></span>
  * <span data-ttu-id="90691-121">Element CI instaluje zestaw SDK przy użyciu jednego z tych skryptów.</span><span class="sxs-lookup"><span data-stu-id="90691-121">CI installs the SDK using one of these scripts.</span></span>
  * <span data-ttu-id="90691-122">Element CI kończy pracę i czyści dane tymczasowe, w tym instalację zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="90691-122">CI finishes its work and clears temporary data including the SDK installation.</span></span>

<span data-ttu-id="90691-123">Aby skonfigurować środowisko programistyczne lub uruchamiać aplikacje, należy użyć instalatorów zamiast skryptów.</span><span class="sxs-lookup"><span data-stu-id="90691-123">To set up a development environment or to run apps, use the installers rather than these scripts.</span></span>

### <a name="recommended-version"></a><span data-ttu-id="90691-124">Zalecana wersja</span><span class="sxs-lookup"><span data-stu-id="90691-124">Recommended version</span></span>

<span data-ttu-id="90691-125">Zalecamy użycie stabilnej wersji skryptów:</span><span class="sxs-lookup"><span data-stu-id="90691-125">We recommend that you use the stable version of the scripts:</span></span>

- <span data-ttu-id="90691-126">Bash (Linux/macOS):<https://dot.net/v1/dotnet-install.sh></span><span class="sxs-lookup"><span data-stu-id="90691-126">Bash (Linux/macOS): <https://dot.net/v1/dotnet-install.sh></span></span>
- <span data-ttu-id="90691-127">PowerShell (Windows):<https://dot.net/v1/dotnet-install.ps1></span><span class="sxs-lookup"><span data-stu-id="90691-127">PowerShell (Windows): <https://dot.net/v1/dotnet-install.ps1></span></span>

### <a name="script-behavior"></a><span data-ttu-id="90691-128">Zachowanie skryptu</span><span class="sxs-lookup"><span data-stu-id="90691-128">Script behavior</span></span>

<span data-ttu-id="90691-129">Oba skrypty mają takie samo zachowanie.</span><span class="sxs-lookup"><span data-stu-id="90691-129">Both scripts have the same behavior.</span></span> <span data-ttu-id="90691-130">Pobierają one plik ZIP/plik tar z kompilacji interfejsu wiersza polecenia, a następnie instalują go w lokalizacji domyślnej lub w lokalizacji określonej przez `-InstallDir|--install-dir` .</span><span class="sxs-lookup"><span data-stu-id="90691-130">They download the ZIP/tarball file from the CLI build drops and proceed to install it in either the default location or in a location specified by `-InstallDir|--install-dir`.</span></span>

<span data-ttu-id="90691-131">Domyślnie skrypty instalacyjne pobierają zestaw SDK i instalują go.</span><span class="sxs-lookup"><span data-stu-id="90691-131">By default, the installation scripts download the SDK and install it.</span></span> <span data-ttu-id="90691-132">Jeśli chcesz uzyskać tylko udostępnione środowisko uruchomieniowe, określ `-Runtime|--runtime` argument.</span><span class="sxs-lookup"><span data-stu-id="90691-132">If you wish to only obtain the shared runtime, specify the `-Runtime|--runtime` argument.</span></span>

<span data-ttu-id="90691-133">Domyślnie skrypt dodaje lokalizację instalacji do $PATH bieżącej sesji.</span><span class="sxs-lookup"><span data-stu-id="90691-133">By default, the script adds the install location to the $PATH for the current session.</span></span> <span data-ttu-id="90691-134">Zastąp to zachowanie domyślne, określając `-NoPath|--no-path` argument.</span><span class="sxs-lookup"><span data-stu-id="90691-134">Override this default behavior by specifying the `-NoPath|--no-path` argument.</span></span> <span data-ttu-id="90691-135">Skrypt nie ustawi `DOTNET_ROOT` zmiennej środowiskowej.</span><span class="sxs-lookup"><span data-stu-id="90691-135">The script doesn't set the `DOTNET_ROOT` environment variable.</span></span>

<span data-ttu-id="90691-136">Przed uruchomieniem skryptu Zainstaluj wymagane [zależności](../install/windows.md#dependencies).</span><span class="sxs-lookup"><span data-stu-id="90691-136">Before running the script, install the required [dependencies](../install/windows.md#dependencies).</span></span>

<span data-ttu-id="90691-137">Można zainstalować określoną wersję przy użyciu `-Version|--version` argumentu.</span><span class="sxs-lookup"><span data-stu-id="90691-137">You can install a specific version using the `-Version|--version` argument.</span></span> <span data-ttu-id="90691-138">Wersja musi być określona jako numer wersji trzech części, np `2.1.0` ..</span><span class="sxs-lookup"><span data-stu-id="90691-138">The version must be specified as a three-part version number, such as `2.1.0`.</span></span> <span data-ttu-id="90691-139">Jeśli wersja nie jest określona, skrypt instaluje `latest` wersję.</span><span class="sxs-lookup"><span data-stu-id="90691-139">If the version isn't specified, the script installs the `latest` version.</span></span>

<span data-ttu-id="90691-140">Skrypty instalacji nie aktualizują rejestru w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="90691-140">The install scripts do not update the registry on Windows.</span></span> <span data-ttu-id="90691-141">Po prostu pobieramy spakowane pliki binarne i skopiują je do folderu.</span><span class="sxs-lookup"><span data-stu-id="90691-141">They just download the zipped binaries and copy them to a folder.</span></span> <span data-ttu-id="90691-142">Jeśli chcesz, aby wartości klucza rejestru były aktualizowane, użyj instalatorów platformy .NET Core.</span><span class="sxs-lookup"><span data-stu-id="90691-142">If you want registry key values to be updated, use the .NET Core installers.</span></span>

## <a name="options"></a><span data-ttu-id="90691-143">Opcje</span><span class="sxs-lookup"><span data-stu-id="90691-143">Options</span></span>

- **`-Architecture|--architecture <ARCHITECTURE>`**

  <span data-ttu-id="90691-144">Architektura plików binarnych platformy .NET Core do zainstalowania.</span><span class="sxs-lookup"><span data-stu-id="90691-144">Architecture of the .NET Core binaries to install.</span></span> <span data-ttu-id="90691-145">Możliwe wartości to `<auto>` , `amd64` , `x64` , `x86` , `arm64` i `arm` .</span><span class="sxs-lookup"><span data-stu-id="90691-145">Possible values are `<auto>`, `amd64`, `x64`, `x86`, `arm64`, and `arm`.</span></span> <span data-ttu-id="90691-146">Wartość domyślna to `<auto>` , która reprezentuje aktualnie uruchomioną architekturę systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="90691-146">The default value is `<auto>`, which represents the currently running OS architecture.</span></span>

- **`-AzureFeed|--azure-feed`**

  <span data-ttu-id="90691-147">Określa adres URL źródła danych platformy Azure do Instalatora.</span><span class="sxs-lookup"><span data-stu-id="90691-147">Specifies the URL for the Azure feed to the installer.</span></span> <span data-ttu-id="90691-148">Zaleca się, aby nie zmieniać tej wartości.</span><span class="sxs-lookup"><span data-stu-id="90691-148">We recommended that you don't change this value.</span></span> <span data-ttu-id="90691-149">Wartość domyślna to `https://dotnetcli.azureedge.net/dotnet`.</span><span class="sxs-lookup"><span data-stu-id="90691-149">The default value is `https://dotnetcli.azureedge.net/dotnet`.</span></span>

- **`-Channel|--channel <CHANNEL>`**

  <span data-ttu-id="90691-150">Określa kanał źródłowy instalacji.</span><span class="sxs-lookup"><span data-stu-id="90691-150">Specifies the source channel for the installation.</span></span> <span data-ttu-id="90691-151">Możliwe wartości są następujące:</span><span class="sxs-lookup"><span data-stu-id="90691-151">The possible values are:</span></span>

  - <span data-ttu-id="90691-152">`Current`-Najnowsza wersja.</span><span class="sxs-lookup"><span data-stu-id="90691-152">`Current` - Most current release.</span></span>
  - <span data-ttu-id="90691-153">`LTS`-Długoterminowy kanał pomocy technicznej (większość aktualnie obsługiwanych wersji).</span><span class="sxs-lookup"><span data-stu-id="90691-153">`LTS` - Long-Term Support channel (most current supported release).</span></span>
  - <span data-ttu-id="90691-154">Dwuczęściowa wersja w formacie X. Y reprezentującym określoną wersję (na przykład `2.1` lub `3.0` ).</span><span class="sxs-lookup"><span data-stu-id="90691-154">Two-part version in X.Y format representing a specific release (for example, `2.1` or `3.0`).</span></span>
  - <span data-ttu-id="90691-155">Nazwa gałęzi: na przykład `release/3.1.1xx` lub `master` (dla nocnych wydań).</span><span class="sxs-lookup"><span data-stu-id="90691-155">Branch name: for example, `release/3.1.1xx` or `master` (for nightly releases).</span></span> <span data-ttu-id="90691-156">Użyj tej opcji, aby zainstalować wersję z kanału w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="90691-156">Use this option to install a version from a preview channel.</span></span> <span data-ttu-id="90691-157">Użyj nazwy kanału wymienionej w [instalatorze i plikach binarnych](https://github.com/dotnet/core-sdk#installers-and-binaries).</span><span class="sxs-lookup"><span data-stu-id="90691-157">Use the name of the channel as listed in [Installers and Binaries](https://github.com/dotnet/core-sdk#installers-and-binaries).</span></span>

  <span data-ttu-id="90691-158">Wartość domyślna to `LTS`.</span><span class="sxs-lookup"><span data-stu-id="90691-158">The default value is `LTS`.</span></span> <span data-ttu-id="90691-159">Aby uzyskać więcej informacji na temat kanałów pomocy technicznej platformy .NET, zobacz stronę [zasady pomocy technicznej platformy .NET](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) .</span><span class="sxs-lookup"><span data-stu-id="90691-159">For more information on .NET support channels, see the [.NET Support Policy](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) page.</span></span>

- **`-DryRun|--dry-run`**

  <span data-ttu-id="90691-160">W przypadku ustawienia skrypt nie wykona instalacji.</span><span class="sxs-lookup"><span data-stu-id="90691-160">If set, the script won't perform the installation.</span></span> <span data-ttu-id="90691-161">Zamiast tego Wyświetla on wiersz polecenia, który służy do spójnej instalacji aktualnie żądanej wersji interfejs wiersza polecenia platformy .NET Core.</span><span class="sxs-lookup"><span data-stu-id="90691-161">Instead, it displays what command line to use to consistently install the currently requested version of the .NET Core CLI.</span></span> <span data-ttu-id="90691-162">Jeśli na przykład zostanie określona wersja `latest` , zostanie wyświetlony link z określoną wersją, aby można było użyć tego polecenia w sposób jednoznaczny w skrypcie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="90691-162">For example, if you specify version `latest`, it displays a link with the specific version so that this command can be used deterministically in a build script.</span></span> <span data-ttu-id="90691-163">Wyświetla również lokalizację pliku binarnego, jeśli wolisz zainstalować lub pobrać ją samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="90691-163">It also displays the binary's location if you prefer to install or download it yourself.</span></span>

- **`-FeedCredential|--feed-credential`**

  <span data-ttu-id="90691-164">Służy jako ciąg zapytania do dołączenia do kanału informacyjnego platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="90691-164">Used as a query string to append to the Azure feed.</span></span> <span data-ttu-id="90691-165">Umożliwia on zmianę adresu URL w celu korzystania z niepublicznych kont magazynu obiektów BLOB.</span><span class="sxs-lookup"><span data-stu-id="90691-165">It allows changing the URL to use non-public blob storage accounts.</span></span>

- **`--help`**

  <span data-ttu-id="90691-166">Drukuje pomoc dla skryptu.</span><span class="sxs-lookup"><span data-stu-id="90691-166">Prints out help for the script.</span></span> <span data-ttu-id="90691-167">Dotyczy tylko skryptu bash.</span><span class="sxs-lookup"><span data-stu-id="90691-167">Applies only to bash script.</span></span> <span data-ttu-id="90691-168">W przypadku programu PowerShell należy użyć polecenia `Get-Help ./dotnet-install.ps1` .</span><span class="sxs-lookup"><span data-stu-id="90691-168">For PowerShell, use `Get-Help ./dotnet-install.ps1`.</span></span>

- **`-InstallDir|--install-dir <DIRECTORY>`**

  <span data-ttu-id="90691-169">Określa ścieżkę instalacji.</span><span class="sxs-lookup"><span data-stu-id="90691-169">Specifies the installation path.</span></span> <span data-ttu-id="90691-170">Katalog zostanie utworzony, jeśli nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="90691-170">The directory is created if it doesn't exist.</span></span> <span data-ttu-id="90691-171">Wartość domyślna to *%LocalAppData%\Microsoft\dotnet* w systemach Windows i */usr/share/dotnet* w systemie Linux/macOS.</span><span class="sxs-lookup"><span data-stu-id="90691-171">The default value is *%LocalAppData%\Microsoft\dotnet* on Windows and */usr/share/dotnet* on Linux/macOS.</span></span> <span data-ttu-id="90691-172">Pliki binarne są umieszczane bezpośrednio w tym katalogu.</span><span class="sxs-lookup"><span data-stu-id="90691-172">Binaries are placed directly in this directory.</span></span>

- **`-JSonFile|--jsonfile <JSONFILE>`**

  <span data-ttu-id="90691-173">Określa ścieżkę do [global.jsw](global-json.md) pliku, która zostanie użyta do określenia wersji zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="90691-173">Specifies a path to a [global.json](global-json.md) file that will be used to determine the SDK version.</span></span> <span data-ttu-id="90691-174">*global.jsw* pliku musi mieć wartość dla `sdk:version` .</span><span class="sxs-lookup"><span data-stu-id="90691-174">The *global.json* file must have a value for `sdk:version`.</span></span>

- **`-NoCdn|--no-cdn`**

  <span data-ttu-id="90691-175">Wyłącza pobieranie z [usługi Azure Content Delivery Network (CDN)](https://docs.microsoft.com/azure/cdn/cdn-overview) i bezpośrednio używa niebuforowanego źródła danych.</span><span class="sxs-lookup"><span data-stu-id="90691-175">Disables downloading from the [Azure Content Delivery Network (CDN)](https://docs.microsoft.com/azure/cdn/cdn-overview) and uses the uncached feed directly.</span></span>

- **`-NoPath|--no-path`**

  <span data-ttu-id="90691-176">W przypadku ustawienia folder instalacyjny nie zostanie wyeksportowany do ścieżki bieżącej sesji.</span><span class="sxs-lookup"><span data-stu-id="90691-176">If set, the installation folder isn't exported to the path for the current session.</span></span> <span data-ttu-id="90691-177">Domyślnie skrypt modyfikuje ścieżkę, co sprawia, że interfejs wiersza polecenia platformy .NET Core dostępne natychmiast po instalacji.</span><span class="sxs-lookup"><span data-stu-id="90691-177">By default, the script modifies the PATH, which makes the .NET Core CLI available immediately after install.</span></span>

- **`-ProxyAddress`**

  <span data-ttu-id="90691-178">W przypadku ustawienia Instalator używa serwera proxy podczas wykonywania żądań sieci Web.</span><span class="sxs-lookup"><span data-stu-id="90691-178">If set, the installer uses the proxy when making web requests.</span></span> <span data-ttu-id="90691-179">(Prawidłowe dla systemu Windows).</span><span class="sxs-lookup"><span data-stu-id="90691-179">(Only valid for Windows.)</span></span>

- **`-ProxyBypassList <LIST_OF_URLS>`**

  <span data-ttu-id="90691-180">Jeśli ustawienie with `ProxyAddress` zawiera listę adresów URL oddzielonych przecinkami, które będą pomijać serwer proxy.</span><span class="sxs-lookup"><span data-stu-id="90691-180">If set with `ProxyAddress`, provides a list of comma-separated urls that will bypass the proxy.</span></span> <span data-ttu-id="90691-181">(Prawidłowe dla systemu Windows).</span><span class="sxs-lookup"><span data-stu-id="90691-181">(Only valid for Windows.)</span></span>

- **`ProxyUseDefaultCredentials`**

  <span data-ttu-id="90691-182">Jeśli ta wartość jest ustawiona, Instalator użyje poświadczeń bieżącego użytkownika przy użyciu adresu serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="90691-182">If set, the installer uses the credentials of the current user when using proxy address.</span></span> <span data-ttu-id="90691-183">(Prawidłowe dla systemu Windows).</span><span class="sxs-lookup"><span data-stu-id="90691-183">(Only valid for Windows.)</span></span>

- **`-Runtime|--runtime <RUNTIME>`**

  <span data-ttu-id="90691-184">Instaluje tylko udostępnione środowisko uruchomieniowe, a nie cały zestaw SDK.</span><span class="sxs-lookup"><span data-stu-id="90691-184">Installs just the shared runtime, not the entire SDK.</span></span> <span data-ttu-id="90691-185">Możliwe wartości są następujące:</span><span class="sxs-lookup"><span data-stu-id="90691-185">The possible values are:</span></span>

  - <span data-ttu-id="90691-186">`dotnet`— `Microsoft.NETCore.App` udostępnione środowisko uruchomieniowe.</span><span class="sxs-lookup"><span data-stu-id="90691-186">`dotnet` - the `Microsoft.NETCore.App` shared runtime.</span></span>
  - <span data-ttu-id="90691-187">`aspnetcore`— `Microsoft.AspNetCore.App` udostępnione środowisko uruchomieniowe.</span><span class="sxs-lookup"><span data-stu-id="90691-187">`aspnetcore` - the `Microsoft.AspNetCore.App` shared runtime.</span></span>
  - <span data-ttu-id="90691-188">`windowsdesktop`— `Microsoft.WindowsDesktop.App` udostępnione środowisko uruchomieniowe.</span><span class="sxs-lookup"><span data-stu-id="90691-188">`windowsdesktop` - the `Microsoft.WindowsDesktop.App` shared runtime.</span></span>

- **`--runtime-id <RID>`**

  <span data-ttu-id="90691-189">Określa [Identyfikator środowiska uruchomieniowego](../rid-catalog.md) , dla którego instalowane są narzędzia.</span><span class="sxs-lookup"><span data-stu-id="90691-189">Specifies the [runtime identifier](../rid-catalog.md) for which the tools are being installed.</span></span> <span data-ttu-id="90691-190">Używany `linux-x64` dla przenośnego systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="90691-190">Use `linux-x64` for portable Linux.</span></span> <span data-ttu-id="90691-191">(Prawidłowy tylko dla systemu Linux/macOS).</span><span class="sxs-lookup"><span data-stu-id="90691-191">(Only valid for Linux/macOS.)</span></span>

- **`-SharedRuntime|--shared-runtime`**

  > [!NOTE]
  > <span data-ttu-id="90691-192">Ten parametr jest przestarzały i może zostać usunięty w przyszłej wersji skryptu.</span><span class="sxs-lookup"><span data-stu-id="90691-192">This parameter is obsolete and may be removed in a future version of the script.</span></span> <span data-ttu-id="90691-193">Zalecaną alternatywą jest `-Runtime|--runtime` opcja.</span><span class="sxs-lookup"><span data-stu-id="90691-193">The recommended alternative is the `-Runtime|--runtime` option.</span></span>

  <span data-ttu-id="90691-194">Instaluje tylko udostępnione bity środowiska uruchomieniowego, a nie cały zestaw SDK.</span><span class="sxs-lookup"><span data-stu-id="90691-194">Installs just the shared runtime bits, not the entire SDK.</span></span> <span data-ttu-id="90691-195">Ta opcja jest równoważna z określeniem `-Runtime|--runtime dotnet` .</span><span class="sxs-lookup"><span data-stu-id="90691-195">This option is equivalent to specifying `-Runtime|--runtime dotnet`.</span></span>

- **`-SkipNonVersionedFiles|--skip-non-versioned-files`**

  <span data-ttu-id="90691-196">Pomija Instalowanie plików nienależących do wersji, takich jak *dotnet.exe*, jeśli już istnieją.</span><span class="sxs-lookup"><span data-stu-id="90691-196">Skips installing non-versioned files, such as *dotnet.exe*, if they already exist.</span></span>

- **`-UncachedFeed|--uncached-feed`**

  <span data-ttu-id="90691-197">Umożliwia zmianę adresu URL dla niebuforowanego źródła danych używanego przez ten Instalator.</span><span class="sxs-lookup"><span data-stu-id="90691-197">Allows changing the URL for the uncached feed used by this installer.</span></span> <span data-ttu-id="90691-198">Zaleca się, aby nie zmieniać tej wartości.</span><span class="sxs-lookup"><span data-stu-id="90691-198">We recommended that you don't change this value.</span></span>

- **`-Verbose|--verbose`**

  <span data-ttu-id="90691-199">Wyświetla informacje diagnostyczne.</span><span class="sxs-lookup"><span data-stu-id="90691-199">Displays diagnostics information.</span></span>

- **`-Version|--version <VERSION>`**

  <span data-ttu-id="90691-200">Reprezentuje konkretną wersję kompilacji.</span><span class="sxs-lookup"><span data-stu-id="90691-200">Represents a specific build version.</span></span> <span data-ttu-id="90691-201">Możliwe wartości są następujące:</span><span class="sxs-lookup"><span data-stu-id="90691-201">The possible values are:</span></span>

  - <span data-ttu-id="90691-202">`latest`-Najnowsza kompilacja w kanale (używana z `-Channel` opcją).</span><span class="sxs-lookup"><span data-stu-id="90691-202">`latest` - Latest build on the channel (used with the `-Channel` option).</span></span>
  - <span data-ttu-id="90691-203">`coherent`-Najnowsza spójna kompilacja na kanale; używa najnowszej stabilnej kombinacji pakietów (używanej z `-Channel` opcjami nazw gałęzi).</span><span class="sxs-lookup"><span data-stu-id="90691-203">`coherent` - Latest coherent build on the channel; uses the latest stable package combination (used with Branch name `-Channel` options).</span></span>
  - <span data-ttu-id="90691-204">Wersja z trzech części w formacie X. Y. Z, reprezentująca konkretną wersję kompilacji; zastępuje `-Channel` opcję.</span><span class="sxs-lookup"><span data-stu-id="90691-204">Three-part version in X.Y.Z format representing a specific build version; supersedes the `-Channel` option.</span></span> <span data-ttu-id="90691-205">Na przykład: `2.0.0-preview2-006120`.</span><span class="sxs-lookup"><span data-stu-id="90691-205">For example: `2.0.0-preview2-006120`.</span></span>

  <span data-ttu-id="90691-206">Jeśli nie zostanie określony, `-Version` wartością domyślną jest `latest` .</span><span class="sxs-lookup"><span data-stu-id="90691-206">If not specified, `-Version` defaults to `latest`.</span></span>

## <a name="examples"></a><span data-ttu-id="90691-207">Przykłady</span><span class="sxs-lookup"><span data-stu-id="90691-207">Examples</span></span>

- <span data-ttu-id="90691-208">Zainstaluj najnowszą wersję długoterminową (LTS) w lokalizacji domyślnej:</span><span class="sxs-lookup"><span data-stu-id="90691-208">Install the latest long-term supported (LTS) version to the default location:</span></span>

  <span data-ttu-id="90691-209">W systemie Windows:</span><span class="sxs-lookup"><span data-stu-id="90691-209">Windows:</span></span>

  ```powershell
  ./dotnet-install.ps1 -Channel LTS
  ```

  <span data-ttu-id="90691-210">macOS/Linux:</span><span class="sxs-lookup"><span data-stu-id="90691-210">macOS/Linux:</span></span>

  ```bash
  ./dotnet-install.sh --channel LTS
  ```

- <span data-ttu-id="90691-211">Zainstaluj najnowszą wersję z kanału 3,1 do określonej lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="90691-211">Install the latest version from 3.1 channel to the specified location:</span></span>

  <span data-ttu-id="90691-212">W systemie Windows:</span><span class="sxs-lookup"><span data-stu-id="90691-212">Windows:</span></span>

  ```powershell
  ./dotnet-install.ps1 -Channel 3.1 -InstallDir C:\cli
  ```

  <span data-ttu-id="90691-213">macOS/Linux:</span><span class="sxs-lookup"><span data-stu-id="90691-213">macOS/Linux:</span></span>

  ```bash
  ./dotnet-install.sh --channel 3.1 --install-dir ~/cli
  ```

- <span data-ttu-id="90691-214">Zainstaluj wersję 3.0.0 udostępnionego środowiska uruchomieniowego:</span><span class="sxs-lookup"><span data-stu-id="90691-214">Install the 3.0.0 version of the shared runtime:</span></span>

  <span data-ttu-id="90691-215">W systemie Windows:</span><span class="sxs-lookup"><span data-stu-id="90691-215">Windows:</span></span>

  ```powershell
  ./dotnet-install.ps1 -Runtime dotnet -Version 3.0.0
  ```

  <span data-ttu-id="90691-216">macOS/Linux:</span><span class="sxs-lookup"><span data-stu-id="90691-216">macOS/Linux:</span></span>

  ```bash
  ./dotnet-install.sh --runtime dotnet --version 3.0.0
  ```

- <span data-ttu-id="90691-217">Uzyskaj skrypt i Zainstaluj wersję 2.1.2 za firmowym serwerem proxy (tylko system Windows):</span><span class="sxs-lookup"><span data-stu-id="90691-217">Obtain script and install the 2.1.2 version behind a corporate proxy (Windows only):</span></span>

  ```powershell
  Invoke-WebRequest 'https://dot.net/v1/dotnet-install.ps1' -Proxy $env:HTTP_PROXY -ProxyUseDefaultCredentials -OutFile 'dotnet-install.ps1';
  ./dotnet-install.ps1 -InstallDir '~/.dotnet' -Version '2.1.2' -ProxyAddress $env:HTTP_PROXY -ProxyUseDefaultCredentials;
  ```

- <span data-ttu-id="90691-218">Uzyskaj skrypt i zainstaluj interfejs wiersza polecenia platformy .NET Core przykłady jednoliniowe:</span><span class="sxs-lookup"><span data-stu-id="90691-218">Obtain script and install .NET Core CLI one-liner examples:</span></span>

  <span data-ttu-id="90691-219">W systemie Windows:</span><span class="sxs-lookup"><span data-stu-id="90691-219">Windows:</span></span>

  ```powershell
  # Run a separate PowerShell process because the script calls exit, so it will end the current PowerShell session.
  &powershell -NoProfile -ExecutionPolicy unrestricted -Command "[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12; &([scriptblock]::Create((Invoke-WebRequest -UseBasicParsing 'https://dot.net/v1/dotnet-install.ps1'))) <additional install-script args>"
  ```

  <span data-ttu-id="90691-220">macOS/Linux:</span><span class="sxs-lookup"><span data-stu-id="90691-220">macOS/Linux:</span></span>

  ```bash
  curl -sSL https://dot.net/v1/dotnet-install.sh | bash /dev/stdin <additional install-script args>
  ```

## <a name="see-also"></a><span data-ttu-id="90691-221">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="90691-221">See also</span></span>

- [<span data-ttu-id="90691-222">Wersje platformy .NET Core</span><span class="sxs-lookup"><span data-stu-id="90691-222">.NET Core releases</span></span>](https://github.com/dotnet/core/releases)
- [<span data-ttu-id="90691-223">Środowisko uruchomieniowe programu .NET Core i archiwum pobierania zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="90691-223">.NET Core Runtime and SDK download archive</span></span>](https://github.com/dotnet/core/blob/master/release-notes/download-archive.md)
