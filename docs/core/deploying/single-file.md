---
title: Aplikacja pojedynczego pliku
description: Dowiedz się, co to jest aplikacja z pojedynczym plikiem i dlaczego należy rozważyć użycie tego modelu wdrażania aplikacji.
author: lakshanf
ms.author: lakshanf
ms.date: 12/17/2020
ms.openlocfilehash: e2d2c9ed4c28d11a77e4f840602982a36cf1c80c
ms.sourcegitcommit: 4b79862c5b41fbd86cf38f926f6a49516059f6f2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/18/2020
ms.locfileid: "97678146"
---
# <a name="single-file-deployment-and-executable"></a><span data-ttu-id="da7d2-103">Wdrażanie i wykonywanie przy użyciu jednego pliku</span><span class="sxs-lookup"><span data-stu-id="da7d2-103">Single file deployment and executable</span></span>

<span data-ttu-id="da7d2-104">Zgrupowanie wszystkich plików zależnych od aplikacji do jednego pliku binarnego zapewnia deweloperowi aplikacji z opcją atrakcyjną w celu wdrożenia i dystrybucji aplikacji jako pojedynczy plik.</span><span class="sxs-lookup"><span data-stu-id="da7d2-104">Bundling all application-dependent files into a single binary provides an application developer with the attractive option to deploy and distribute the application as a single file.</span></span> <span data-ttu-id="da7d2-105">Ten model wdrażania został udostępniony od platformy .NET Core 3,0 i został ulepszony w programie .NET 5,0.</span><span class="sxs-lookup"><span data-stu-id="da7d2-105">This deployment model has been available since .NET Core 3.0 and has been enhanced in .NET 5.0.</span></span> <span data-ttu-id="da7d2-106">Wcześniej w programie .NET Core 3,0, gdy użytkownik uruchamia aplikację z jednym plikiem, host .NET Core najpierw wyodrębnia wszystkie pliki do katalogu tymczasowego przed uruchomieniem aplikacji.</span><span class="sxs-lookup"><span data-stu-id="da7d2-106">Previously in .NET Core 3.0, when a user runs your single-file app, .NET Core host first extracts all files to a temporary directory before running the application.</span></span> <span data-ttu-id="da7d2-107">Program .NET 5,0 podnosi to środowisko, bezpośrednio uruchamiając kod bez konieczności wyodrębniania plików z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="da7d2-107">.NET 5.0 improves this experience by directly running the code without the need to extract the files from the app.</span></span>

<span data-ttu-id="da7d2-108">Wdrożenie pojedynczego pliku jest dostępne zarówno dla [modelu wdrażania zależnego od platformy](index.md#publish-framework-dependent) , jak i [aplikacji samodzielnych](index.md#publish-self-contained).</span><span class="sxs-lookup"><span data-stu-id="da7d2-108">Single File deployment is available for both the [framework-dependent deployment model](index.md#publish-framework-dependent) and [self-contained applications](index.md#publish-self-contained).</span></span> <span data-ttu-id="da7d2-109">Rozmiar pojedynczego pliku w aplikacji samodzielnej jest duży, ponieważ będzie obejmował środowisko uruchomieniowe i biblioteki struktury.</span><span class="sxs-lookup"><span data-stu-id="da7d2-109">The size of the single file in a self-contained application will be large since it will include the runtime and the framework libraries.</span></span> <span data-ttu-id="da7d2-110">Opcja wdrożenia pojedynczego pliku może być łączona z [ReadyToRun](ready-to-run.md) i [Trim (funkcja eksperymentalna w programie .NET 5,0)](trim-self-contained.md) opcje publikowania.</span><span class="sxs-lookup"><span data-stu-id="da7d2-110">The single file deployment option can be combined with [ReadyToRun](ready-to-run.md) and [Trim (an experimental feature in .NET 5.0)](trim-self-contained.md) publish options.</span></span>

## <a name="api-incompatibility"></a><span data-ttu-id="da7d2-111">Niezgodność interfejsu API</span><span class="sxs-lookup"><span data-stu-id="da7d2-111">API incompatibility</span></span>

<span data-ttu-id="da7d2-112">Niektóre interfejsy API nie są zgodne z wdrożeniem pojedynczego pliku, a aplikacje mogą wymagać modyfikacji, jeśli korzystają z tych interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="da7d2-112">Some APIs are not compatible with single-file deployment and applications may require modification if they use these APIs.</span></span> <span data-ttu-id="da7d2-113">Jeśli używasz struktury lub pakietu innej firmy, istnieje możliwość, że mogą one również korzystać z jednego z tych interfejsów API i wymagać modyfikacji.</span><span class="sxs-lookup"><span data-stu-id="da7d2-113">If you use a third-party framework or package, it's possible that they may also use one of these APIs and need modification.</span></span> <span data-ttu-id="da7d2-114">Najczęstsze przyczyny problemów są zależne od ścieżek plików plików lub bibliotek DLL dostarczanych z aplikacją.</span><span class="sxs-lookup"><span data-stu-id="da7d2-114">The most common cause of problems is dependence on file paths for files or DLLs shipped with the application.</span></span>

<span data-ttu-id="da7d2-115">W poniższej tabeli znajdują się odpowiednie szczegóły interfejsu API biblioteki środowiska uruchomieniowego dotyczące użycia pojedynczego pliku.</span><span class="sxs-lookup"><span data-stu-id="da7d2-115">The table below has the relevant runtime library API details for single-file use.</span></span>

| <span data-ttu-id="da7d2-116">Interfejs API</span><span class="sxs-lookup"><span data-stu-id="da7d2-116">API</span></span>                            | <span data-ttu-id="da7d2-117">Uwaga</span><span class="sxs-lookup"><span data-stu-id="da7d2-117">Note</span></span>                                                                   |
|--------------------------------|------------------------------------------------------------------------|
| `Assembly.Location`            | <span data-ttu-id="da7d2-118">Zwraca pusty ciąg.</span><span class="sxs-lookup"><span data-stu-id="da7d2-118">Returns an empty string.</span></span>                                               |
| `Module.FullyQualifiedName`    | <span data-ttu-id="da7d2-119">Zwraca ciąg z wartością `<Unknown>` lub zgłasza wyjątek.</span><span class="sxs-lookup"><span data-stu-id="da7d2-119">Returns a string with the value of `<Unknown>` or throws an exception.</span></span> |
| `Module.Name`                  | <span data-ttu-id="da7d2-120">Zwraca ciąg o wartości `<Unknown>` .</span><span class="sxs-lookup"><span data-stu-id="da7d2-120">Returns a string with the value of `<Unknown>`.</span></span>                        |
| `Assembly.GetFile`             | <span data-ttu-id="da7d2-121">Zgłasza <xref:System.IO.IOException> .</span><span class="sxs-lookup"><span data-stu-id="da7d2-121">Throws <xref:System.IO.IOException>.</span></span>                                   |
| `Assembly.GetFiles`            | <span data-ttu-id="da7d2-122">Zgłasza <xref:System.IO.IOException> .</span><span class="sxs-lookup"><span data-stu-id="da7d2-122">Throws <xref:System.IO.IOException>.</span></span>                                   |
| `Assembly.CodeBase`            | <span data-ttu-id="da7d2-123">Zgłasza <xref:System.PlatformNotSupportedException> .</span><span class="sxs-lookup"><span data-stu-id="da7d2-123">Throws <xref:System.PlatformNotSupportedException>.</span></span>                    |
| `Assembly.EscapedCodeBase`     | <span data-ttu-id="da7d2-124">Zgłasza <xref:System.PlatformNotSupportedException> .</span><span class="sxs-lookup"><span data-stu-id="da7d2-124">Throws <xref:System.PlatformNotSupportedException>.</span></span>                    |
| `AssemblyName.CodeBase`        | <span data-ttu-id="da7d2-125">Zwraca wartość `null`.</span><span class="sxs-lookup"><span data-stu-id="da7d2-125">Returns `null`.</span></span>                                                        |
| `AssemblyName.EscapedCodeBase` | <span data-ttu-id="da7d2-126">Zwraca wartość `null`.</span><span class="sxs-lookup"><span data-stu-id="da7d2-126">Returns `null`.</span></span>                                                        |

<span data-ttu-id="da7d2-127">Mamy pewne zalecenia dotyczące rozwiązywania typowych scenariuszy:</span><span class="sxs-lookup"><span data-stu-id="da7d2-127">We have some recommendations for fixing common scenarios:</span></span>

* <span data-ttu-id="da7d2-128">Aby uzyskać dostęp do plików obok pliku wykonywalnego, użyj programu <xref:System.AppContext.BaseDirectory?displayProperty=nameWithType> .</span><span class="sxs-lookup"><span data-stu-id="da7d2-128">To access files next to the executable, use <xref:System.AppContext.BaseDirectory?displayProperty=nameWithType>.</span></span>

* <span data-ttu-id="da7d2-129">Aby znaleźć nazwę pliku wykonywalnego, użyj pierwszego elementu <xref:System.Environment.GetCommandLineArgs?displayProperty=nameWithType> .</span><span class="sxs-lookup"><span data-stu-id="da7d2-129">To find the file name of the executable, use the first element of <xref:System.Environment.GetCommandLineArgs?displayProperty=nameWithType>.</span></span>

* <span data-ttu-id="da7d2-130">Aby uniknąć całkowitego wysyłania luźnych plików, należy rozważyć użycie [zasobów osadzonych](../../framework/resources/creating-resource-files-for-desktop-apps.md).</span><span class="sxs-lookup"><span data-stu-id="da7d2-130">To avoid shipping loose files entirely, consider using [embedded resources](../../framework/resources/creating-resource-files-for-desktop-apps.md).</span></span>

## <a name="attaching-a-debugger"></a><span data-ttu-id="da7d2-131">Dołączanie debugera</span><span class="sxs-lookup"><span data-stu-id="da7d2-131">Attaching a debugger</span></span>

<span data-ttu-id="da7d2-132">W systemie Linux jedynym debugerem, który może dołączyć do samodzielnego procesu pojedynczego pliku lub Zrzuty awaryjne debugowania, jest [sos z LLDB](../diagnostics/dotnet-sos.md).</span><span class="sxs-lookup"><span data-stu-id="da7d2-132">On Linux, the only debugger which can attach to self-contained single-file processes or debug crash dumps is [SOS with LLDB](../diagnostics/dotnet-sos.md).</span></span>

<span data-ttu-id="da7d2-133">W systemach Windows i Mac program Visual Studio i VS Code mogą służyć do debugowania zrzutów awaryjnych.</span><span class="sxs-lookup"><span data-stu-id="da7d2-133">On Windows and Mac, Visual Studio and VS Code can be used to debug crash dumps.</span></span> <span data-ttu-id="da7d2-134">Dołączanie do uruchomionego samodzielnego pliku wykonywalnego wymaga dodatkowego pliku: _mscordbi. { DLL, dlatego}_.</span><span class="sxs-lookup"><span data-stu-id="da7d2-134">Attaching to a running self-contained single-file executable requires an extra file: _mscordbi.{dll,so}_.</span></span>

<span data-ttu-id="da7d2-135">Bez tego pliku program Visual Studio może generować błąd "nie można dołączyć do procesu.</span><span class="sxs-lookup"><span data-stu-id="da7d2-135">Without this file Visual Studio may produce the error "Unable to attach to the process.</span></span> <span data-ttu-id="da7d2-136">Składnik debugowania nie jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="da7d2-136">A debug component is not installed."</span></span> <span data-ttu-id="da7d2-137">i VS Code mogą generować błąd "nie można dołączyć do procesu: nieznany błąd: 0x80131c3c".</span><span class="sxs-lookup"><span data-stu-id="da7d2-137">and VS Code may produce the error "Failed to attach to process: Unknown Error: 0x80131c3c."</span></span>

<span data-ttu-id="da7d2-138">Aby naprawić te błędy, _mscordbi_ musi zostać skopiowana obok pliku wykonywalnego.</span><span class="sxs-lookup"><span data-stu-id="da7d2-138">To fix these errors, _mscordbi_ needs to be copied next to the executable.</span></span> <span data-ttu-id="da7d2-139">_mscordbi_ jest `publish` Domyślnie ED w PODkatalogu z identyfikatorem środowiska uruchomieniowego aplikacji.</span><span class="sxs-lookup"><span data-stu-id="da7d2-139">_mscordbi_ is `publish`ed by default in the subdirectory with the application's runtime ID.</span></span> <span data-ttu-id="da7d2-140">Na przykład jeśli jedna z nich była opublikowana samodzielny plik wykonywalny przy użyciu `dotnet` interfejsu wiersza polecenia dla systemu Windows za pomocą parametrów `-r win-x64` , plik wykonywalny zostanie umieszczony w pliku _bin/debug/NET 5.0/win-x64/Publish_.</span><span class="sxs-lookup"><span data-stu-id="da7d2-140">So, for example, if one were to publish a self-contained single-file executable using the `dotnet` CLI for Windows using the parameters `-r win-x64`, the executable would be placed in _bin/Debug/net5.0/win-x64/publish_.</span></span> <span data-ttu-id="da7d2-141">Kopia _mscordbi.dll_ byłaby obecna w _bin/debug/NET 5.0/win-x64_.</span><span class="sxs-lookup"><span data-stu-id="da7d2-141">A copy of _mscordbi.dll_ would be present in _bin/Debug/net5.0/win-x64_.</span></span>

## <a name="other-considerations"></a><span data-ttu-id="da7d2-142">Inne zagadnienia</span><span class="sxs-lookup"><span data-stu-id="da7d2-142">Other considerations</span></span>

<span data-ttu-id="da7d2-143">Pojedynczy plik domyślnie nie obsługuje bibliotek natywnych.</span><span class="sxs-lookup"><span data-stu-id="da7d2-143">Single-file doesn't bundle native libraries by default.</span></span> <span data-ttu-id="da7d2-144">W systemie Linux wstępnie łączymy środowisko uruchomieniowe z pakietem i tylko biblioteki natywne aplikacji są wdrażane w tym samym katalogu, w którym znajduje się aplikacja Jednoplikowa.</span><span class="sxs-lookup"><span data-stu-id="da7d2-144">On Linux, we prelink the runtime into the bundle and only application native libraries are deployed to the same directory as the single-file app.</span></span> <span data-ttu-id="da7d2-145">W systemie Windows połączymy tylko kod hostingu, a biblioteki natywne środowiska uruchomieniowego i aplikacji są wdrażane w tym samym katalogu, w którym znajduje się aplikacja pojedynczego pliku.</span><span class="sxs-lookup"><span data-stu-id="da7d2-145">On Windows, we prelink only the hosting code and both the runtime and application native libraries are deployed to the same directory as the single-file app.</span></span> <span data-ttu-id="da7d2-146">Jest to konieczne w celu zapewnienia dobrego środowiska debugowania, które wymaga wykluczenia plików natywnych z pojedynczego pliku.</span><span class="sxs-lookup"><span data-stu-id="da7d2-146">This is to ensure a good debugging experience, which requires native files to be excluded from the single file.</span></span> <span data-ttu-id="da7d2-147">Istnieje możliwość ustawienia flagi, `IncludeNativeLibrariesForSelfExtract` Aby uwzględnić biblioteki natywne w pojedynczym zbiorze plików, ale te pliki zostaną wyodrębnione do katalogu tymczasowego na komputerze klienckim po uruchomieniu aplikacji pojedynczego pliku.</span><span class="sxs-lookup"><span data-stu-id="da7d2-147">There is an option to set a flag, `IncludeNativeLibrariesForSelfExtract`, to include native libraries in the single file bundle, but these files will be extracted to a temporary directory in the client machine when the single file application is run.</span></span>

<span data-ttu-id="da7d2-148">Aplikacja Jednoplikowa będzie zawierała wszystkie powiązane pliki PDB obok niej i nie zostanie domyślnie zawiązana.</span><span class="sxs-lookup"><span data-stu-id="da7d2-148">Single-file application will have all related PDB files alongside it and will not be bundled by default.</span></span> <span data-ttu-id="da7d2-149">Jeśli chcesz uwzględnić plików pdb wewnątrz zestawu dla projektów, które tworzysz, ustaw polecenie `DebugType` na zgodnie z `embedded` [poniższym](#include-pdb-files-inside-the-bundle) opisem.</span><span class="sxs-lookup"><span data-stu-id="da7d2-149">If you want to include PDBs inside the assembly for projects you build, set the `DebugType` to `embedded` as described [below](#include-pdb-files-inside-the-bundle) in detail.</span></span>

<span data-ttu-id="da7d2-150">Zarządzane składniki języka C++ nie są dobrze dopasowane do wdrożenia jednoplikowego i zalecamy zapisanie aplikacji w języku C# lub innym niezarządzanym języku C++ w celu zapewnienia zgodności z pojedynczym plikiem.</span><span class="sxs-lookup"><span data-stu-id="da7d2-150">Managed C++ components aren't well suited for single-file deployment and we recommend that you write applications in C# or another non-managed C++ language to be single-file compatible.</span></span>

## <a name="exclude-files-from-being-embedded"></a><span data-ttu-id="da7d2-151">Wykluczanie plików z osadzania</span><span class="sxs-lookup"><span data-stu-id="da7d2-151">Exclude files from being embedded</span></span>

<span data-ttu-id="da7d2-152">Niektóre pliki można jawnie wykluczyć z osadzania w pojedynczym pliku przez ustawienie następujących metadanych:</span><span class="sxs-lookup"><span data-stu-id="da7d2-152">Certain files can be explicitly excluded from being embedded in the single-file by setting following metadata:</span></span>

```xml
<ExcludeFromSingleFile>true</ExcludeFromSingleFile>
```

<span data-ttu-id="da7d2-153">Na przykład w celu umieszczenia niektórych plików w katalogu publikowania, ale nie są one powiązane z pojedynczym plikiem:</span><span class="sxs-lookup"><span data-stu-id="da7d2-153">For example, to place some files in the publish directory but not bundle them in the single-file:</span></span>

```xml
<ItemGroup>
  <Content Update="Plugin.dll">
    <CopyToPublishDirectory>PreserveNewest</CopyToPublishDirectory>
    <ExcludeFromSingleFile>true</ExcludeFromSingleFile>
  </Content>
</ItemGroup>
```

## <a name="include-pdb-files-inside-the-bundle"></a><span data-ttu-id="da7d2-154">Uwzględnij pliki PDB wewnątrz pakietu</span><span class="sxs-lookup"><span data-stu-id="da7d2-154">Include PDB files inside the bundle</span></span>

<span data-ttu-id="da7d2-155">Plik PDB zestawu może być osadzony w samym zestawie ( `.dll` ) przy użyciu poniższego ustawienia.</span><span class="sxs-lookup"><span data-stu-id="da7d2-155">The PDB file for an assembly can be embedded into the assembly itself (the `.dll`) using the setting below.</span></span> <span data-ttu-id="da7d2-156">Ponieważ symbole są częścią zestawu, będą również częścią aplikacji jednoplikowej:</span><span class="sxs-lookup"><span data-stu-id="da7d2-156">Since the symbols are part of the assembly, they will be part of the single-file application as well:</span></span>

```xml
<DebugType>embedded</DebugType>
```

<span data-ttu-id="da7d2-157">Na przykład Dodaj następującą właściwość do pliku projektu zestawu, aby osadzić plik PDB w tym zestawie:</span><span class="sxs-lookup"><span data-stu-id="da7d2-157">For example, add the following property to the project file of an assembly to embed the PDB file to that assembly:</span></span>

```xml
<PropertyGroup>
  <DebugType>embedded</DebugType>
</PropertyGroup>
```

## <a name="publish-a-single-file-app---sample-project-file"></a><span data-ttu-id="da7d2-158">Publikowanie pojedynczego pliku aplikacji — przykładowego pliku projektu</span><span class="sxs-lookup"><span data-stu-id="da7d2-158">Publish a single file app - sample project file</span></span>

<span data-ttu-id="da7d2-159">Oto przykładowy plik projektu, który określa publikację pojedynczego pliku:</span><span class="sxs-lookup"><span data-stu-id="da7d2-159">Here's a sample project file that specifies single-file publishing:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net5.0</TargetFramework>
    <PublishSingleFile>true</PublishSingleFile>
    <SelfContained>true</SelfContained>
    <RuntimeIdentifier>win-x64</RuntimeIdentifier>
    <PublishTrimmed>true</PublishTrimmed>
    <PublishReadyToRun>true</PublishReadyToRun>
  </PropertyGroup>

</Project>
```

<span data-ttu-id="da7d2-160">Te właściwości mają następujące funkcje:</span><span class="sxs-lookup"><span data-stu-id="da7d2-160">These properties have the following functions:</span></span>

* <span data-ttu-id="da7d2-161">`PublishSingleFile` -Włącza publikowanie Jednoplikowe.</span><span class="sxs-lookup"><span data-stu-id="da7d2-161">`PublishSingleFile` - Enables single-file publishing.</span></span>
* <span data-ttu-id="da7d2-162">`SelfContained` -Określa, czy aplikacja będzie samodzielna lub zależna od struktury.</span><span class="sxs-lookup"><span data-stu-id="da7d2-162">`SelfContained` - Determines whether the app will be self-contained or framework-dependent.</span></span>
* <span data-ttu-id="da7d2-163">`RuntimeIdentifier` -Określa docelowy [Typ systemu operacyjnego i procesora CPU](../rid-catalog.md) .</span><span class="sxs-lookup"><span data-stu-id="da7d2-163">`RuntimeIdentifier` - Specifies the [OS and CPU type](../rid-catalog.md) you are targeting.</span></span>
* <span data-ttu-id="da7d2-164">`PublishTrimmed` -Umożliwia użycie [przycinania zestawu](trim-self-contained.md), który jest obsługiwany tylko w przypadku aplikacji samodzielnych.</span><span class="sxs-lookup"><span data-stu-id="da7d2-164">`PublishTrimmed` - Enables use of [assembly trimming](trim-self-contained.md), which is only supported for self-contained apps.</span></span>
* <span data-ttu-id="da7d2-165">`PublishReadyToRun` -Włącza [kompilację w czasie (AOT)](ready-to-run.md).</span><span class="sxs-lookup"><span data-stu-id="da7d2-165">`PublishReadyToRun` - Enables [ahead-of-time (AOT) compilation](ready-to-run.md).</span></span>

<span data-ttu-id="da7d2-166">**Uwagi:**</span><span class="sxs-lookup"><span data-stu-id="da7d2-166">**Notes:**</span></span>

* <span data-ttu-id="da7d2-167">Aplikacje są zależne od systemu operacyjnego i architektury.</span><span class="sxs-lookup"><span data-stu-id="da7d2-167">Apps are OS and architecture-specific.</span></span> <span data-ttu-id="da7d2-168">Należy opublikować dla każdej konfiguracji, na przykład Linux x64, Linux ARM64, Windows x64 i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="da7d2-168">You need to publish for each configuration, such as Linux x64, Linux ARM64, Windows x64, and so forth.</span></span>
* <span data-ttu-id="da7d2-169">Pliki konfiguracji, takie jak *\*.runtimeconfig.json*, są zawarte w pojedynczym pliku.</span><span class="sxs-lookup"><span data-stu-id="da7d2-169">Configuration files, such as *\*.runtimeconfig.json*, are included in the single file.</span></span> <span data-ttu-id="da7d2-170">Jeśli jest wymagany dodatkowy plik konfiguracji, możesz go umieścić obok pojedynczego pliku.</span><span class="sxs-lookup"><span data-stu-id="da7d2-170">If an additional configuration file is needed, you can place it beside the single file.</span></span>

## <a name="publish-a-single-file-app---cli"></a><span data-ttu-id="da7d2-171">Publikowanie pojedynczego pliku aplikacji — interfejs wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="da7d2-171">Publish a single file app - CLI</span></span>

<span data-ttu-id="da7d2-172">Opublikuj aplikację pojedynczego pliku przy użyciu polecenia [dotnet Publish](../tools/dotnet-publish.md) .</span><span class="sxs-lookup"><span data-stu-id="da7d2-172">Publish a single file application using the [dotnet publish](../tools/dotnet-publish.md) command.</span></span> <span data-ttu-id="da7d2-173">Po opublikowaniu aplikacji ustaw następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="da7d2-173">When you publish your app, set the following properties:</span></span>

- <span data-ttu-id="da7d2-174">Publikuj dla określonego środowiska uruchomieniowego: `-r win-x64`</span><span class="sxs-lookup"><span data-stu-id="da7d2-174">Publish for a specific runtime: `-r win-x64`</span></span>
- <span data-ttu-id="da7d2-175">Publikuj jako pojedynczy plik: `-p:PublishSingleFile=true`</span><span class="sxs-lookup"><span data-stu-id="da7d2-175">Publish as a single-file: `-p:PublishSingleFile=true`</span></span>

<span data-ttu-id="da7d2-176">W poniższym przykładzie jest publikowana aplikacja dla systemu Windows jako samodzielna aplikacja pojedynczego pliku.</span><span class="sxs-lookup"><span data-stu-id="da7d2-176">The following example publishes an app for Windows as a self-contained single file application.</span></span>

```dotnetcli
dotnet publish -r win-x64 -p:PublishSingleFile=true --self-contained true
```

<span data-ttu-id="da7d2-177">Poniższy przykład umożliwia opublikowanie aplikacji dla systemu Linux jako zależnej od struktury aplikacji pojedynczego pliku.</span><span class="sxs-lookup"><span data-stu-id="da7d2-177">The following example publishes an app for Linux as a framework dependent single file application.</span></span>

```dotnetcli
dotnet publish -r linux-x64 -p:PublishSingleFile=true --self-contained false
```

<span data-ttu-id="da7d2-178">Aby uzyskać więcej informacji, zobacz [publikowanie aplikacji .NET Core za pomocą interfejs wiersza polecenia platformy .NET Core](deploy-with-cli.md).</span><span class="sxs-lookup"><span data-stu-id="da7d2-178">For more information, see [Publish .NET Core apps with .NET Core CLI](deploy-with-cli.md).</span></span>

## <a name="publish-a-single-file-app---visual-studio"></a><span data-ttu-id="da7d2-179">Publikowanie aplikacji pojedynczego pliku — Visual Studio</span><span class="sxs-lookup"><span data-stu-id="da7d2-179">Publish a single file app - Visual Studio</span></span>

<span data-ttu-id="da7d2-180">Program Visual Studio tworzy Profile publikowania wielokrotnego użytku, które kontrolują sposób publikowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="da7d2-180">Visual Studio creates reusable publishing profiles that control how your application is published.</span></span>

01. <span data-ttu-id="da7d2-181">W okienku **Eksplorator rozwiązań** kliknij prawym przyciskiem myszy projekt, który chcesz opublikować.</span><span class="sxs-lookup"><span data-stu-id="da7d2-181">On the **Solution Explorer** pane, right-click on the project you want to publish.</span></span> <span data-ttu-id="da7d2-182">Kliknij opcję **Opublikuj**.</span><span class="sxs-lookup"><span data-stu-id="da7d2-182">Select **Publish**.</span></span>

    :::image type="content" source="media/single-file/visual-studio-solution-explorer.png" alt-text="Eksplorator rozwiązań z menu po kliknięciu prawym przyciskiem myszy wyróżnianie opcji Publikuj.":::

    <span data-ttu-id="da7d2-184">Jeśli nie masz jeszcze profilu publikowania, postępuj zgodnie z instrukcjami, aby utworzyć jeden, i wybierz typ docelowy **folderu** .</span><span class="sxs-lookup"><span data-stu-id="da7d2-184">If you don't already have a publishing profile, follow the instructions to create one and choose the **Folder** target-type.</span></span>

01. <span data-ttu-id="da7d2-185">Wybierz pozycję **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="da7d2-185">Choose **Edit**.</span></span>

    :::image type="content" source="media/single-file/visual-studio-publish-edit-settings.png" alt-text="Profil publikacji programu Visual Studio za pomocą przycisku Edytuj.":::

01. <span data-ttu-id="da7d2-187">W oknie dialogowym **Ustawienia profilu** ustaw następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="da7d2-187">In the **Profile settings** dialog, set the following options:</span></span>

    - <span data-ttu-id="da7d2-188">Ustaw **Tryb wdrożenia** na **własny**.</span><span class="sxs-lookup"><span data-stu-id="da7d2-188">Set **Deployment mode** to **Self-contained**.</span></span>
    - <span data-ttu-id="da7d2-189">Ustaw **docelowy środowisko uruchomieniowe** na platformę, w której chcesz publikować.</span><span class="sxs-lookup"><span data-stu-id="da7d2-189">Set **Target runtime** to the platform you want to publish to.</span></span>
    - <span data-ttu-id="da7d2-190">Wybierz pozycję **Wygeneruj pojedynczy plik**.</span><span class="sxs-lookup"><span data-stu-id="da7d2-190">Select **Produce single file**.</span></span>

    <span data-ttu-id="da7d2-191">Wybierz pozycję **Zapisz** , aby zapisać ustawienia i powrócić do okna dialogowego **Publikowanie** .</span><span class="sxs-lookup"><span data-stu-id="da7d2-191">Choose **Save** to save the settings and return to the **Publish** dialog.</span></span>

    :::image type="content" source="media/single-file/visual-studio-publish-single-file-properties.png" alt-text="Okno dialogowe ustawień profilu z trybem wdrożenia, docelowym środowiskiem uruchomieniowym i opcją pojedynczego pliku.":::

01. <span data-ttu-id="da7d2-193">Wybierz pozycję **Publikuj** , aby opublikować aplikację jako pojedynczy plik.</span><span class="sxs-lookup"><span data-stu-id="da7d2-193">Choose **Publish** to publish your app as a single file.</span></span>

<span data-ttu-id="da7d2-194">Aby uzyskać więcej informacji, zobacz [publikowanie aplikacji .NET Core za pomocą programu Visual Studio](deploy-with-vs.md).</span><span class="sxs-lookup"><span data-stu-id="da7d2-194">For more information, see [Publish .NET Core apps with Visual Studio](deploy-with-vs.md).</span></span>

## <a name="publish-a-single-file-app---visual-studio-for-mac"></a><span data-ttu-id="da7d2-195">Publikowanie aplikacji pojedynczego pliku — Visual Studio dla komputerów Mac</span><span class="sxs-lookup"><span data-stu-id="da7d2-195">Publish a single file app - Visual Studio for Mac</span></span>

<span data-ttu-id="da7d2-196">Visual Studio dla komputerów Mac nie udostępnia opcji publikowania aplikacji jako pojedynczego pliku.</span><span class="sxs-lookup"><span data-stu-id="da7d2-196">Visual Studio for Mac doesn't provide options to publish your app as a single file.</span></span> <span data-ttu-id="da7d2-197">Należy opublikować ręcznie, postępując zgodnie z instrukcjami zawartymi w sekcji [Publikowanie pojedynczego pliku App-CLI](#publish-a-single-file-app---cli) .</span><span class="sxs-lookup"><span data-stu-id="da7d2-197">You'll need to publish manually by following the instructions from the [Publish a single file app - CLI](#publish-a-single-file-app---cli) section.</span></span> <span data-ttu-id="da7d2-198">Aby uzyskać więcej informacji, zobacz [publikowanie aplikacji .NET Core za pomocą interfejs wiersza polecenia platformy .NET Core](deploy-with-cli.md).</span><span class="sxs-lookup"><span data-stu-id="da7d2-198">For more information, see [Publish .NET Core apps with .NET Core CLI](deploy-with-cli.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="da7d2-199">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="da7d2-199">See also</span></span>

- <span data-ttu-id="da7d2-200">[Wdrażanie aplikacji .NET Core](index.md).</span><span class="sxs-lookup"><span data-stu-id="da7d2-200">[.NET Core application deployment](index.md).</span></span>
- <span data-ttu-id="da7d2-201">[Publikowanie aplikacji platformy .NET Core za pomocą interfejs wiersza polecenia platformy .NET Core](deploy-with-cli.md).</span><span class="sxs-lookup"><span data-stu-id="da7d2-201">[Publish .NET Core apps with .NET Core CLI](deploy-with-cli.md).</span></span>
- <span data-ttu-id="da7d2-202">[Publikowanie aplikacji platformy .NET Core w programie Visual Studio](deploy-with-vs.md).</span><span class="sxs-lookup"><span data-stu-id="da7d2-202">[Publish .NET Core apps with Visual Studio](deploy-with-vs.md).</span></span>
- <span data-ttu-id="da7d2-203">[ `dotnet publish` polecenie](../tools/dotnet-publish.md).</span><span class="sxs-lookup"><span data-stu-id="da7d2-203">[`dotnet publish` command](../tools/dotnet-publish.md).</span></span>
