---
title: Narzędzia platformy .NET
description: Jak instalować, używać, aktualizować i usuwać narzędzia platformy .NET. Obejmuje narzędzia globalne, narzędzia ścieżki narzędzi i narzędzia lokalne.
author: KathleenDollard
ms.topic: how-to
ms.date: 02/12/2020
ms.openlocfilehash: 8839fd4fba72c9f973d906eabb72919306a847dd
ms.sourcegitcommit: 635a0ff775d2447a81ef7233a599b8f88b162e5d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/17/2020
ms.locfileid: "97633887"
---
# <a name="how-to-manage-net-tools"></a><span data-ttu-id="17983-104">Jak zarządzać narzędziami .NET</span><span class="sxs-lookup"><span data-stu-id="17983-104">How to manage .NET tools</span></span>

<span data-ttu-id="17983-105">**Ten artykuł ma zastosowanie do:** ✔️ .net Core 2,1 SDK i nowszych wersjach</span><span class="sxs-lookup"><span data-stu-id="17983-105">**This article applies to:** ✔️ .NET Core 2.1 SDK and later versions</span></span>

<span data-ttu-id="17983-106">Narzędzie .NET jest specjalnym pakietem NuGet, który zawiera aplikację konsolową.</span><span class="sxs-lookup"><span data-stu-id="17983-106">A .NET tool is a special NuGet package that contains a console application.</span></span> <span data-ttu-id="17983-107">Narzędzie można zainstalować na maszynie w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="17983-107">A tool can be installed on your machine in the following ways:</span></span>

* <span data-ttu-id="17983-108">Jako narzędzie globalne.</span><span class="sxs-lookup"><span data-stu-id="17983-108">As a global tool.</span></span>

  <span data-ttu-id="17983-109">Pliki binarne narzędzia są instalowane w katalogu domyślnym, który jest dodawany do zmiennej środowiskowej PATH.</span><span class="sxs-lookup"><span data-stu-id="17983-109">The tool binaries are installed in a default directory that is added to the PATH environment variable.</span></span> <span data-ttu-id="17983-110">Można wywołać narzędzie z dowolnego katalogu na maszynie bez określania jego lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="17983-110">You can invoke the tool from any directory on the machine without specifying its location.</span></span> <span data-ttu-id="17983-111">Jedna wersja narzędzia jest używana dla wszystkich katalogów na komputerze.</span><span class="sxs-lookup"><span data-stu-id="17983-111">One version of a tool is used for all directories on the machine.</span></span>

* <span data-ttu-id="17983-112">Jako narzędzie globalne w niestandardowej lokalizacji (nazywanej również narzędziem ścieżki narzędzia).</span><span class="sxs-lookup"><span data-stu-id="17983-112">As a global tool in a custom location (also known as a tool-path tool).</span></span>

  <span data-ttu-id="17983-113">Pliki binarne narzędzia są instalowane w określonej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="17983-113">The tool binaries are installed in a location that you specify.</span></span> <span data-ttu-id="17983-114">Możesz wywołać narzędzie z katalogu instalacyjnego lub podając katalog z nazwą polecenia lub dodając katalog do zmiennej środowiskowej PATH.</span><span class="sxs-lookup"><span data-stu-id="17983-114">You can invoke the tool from the installation directory or by providing the directory with the command name or by adding the directory to the PATH environment variable.</span></span> <span data-ttu-id="17983-115">Jedna wersja narzędzia jest używana dla wszystkich katalogów na komputerze.</span><span class="sxs-lookup"><span data-stu-id="17983-115">One version of a tool is used for all directories on the machine.</span></span>

* <span data-ttu-id="17983-116">Jako narzędzie lokalne (dotyczy zestaw .NET Core SDK 3,0 i nowszych).</span><span class="sxs-lookup"><span data-stu-id="17983-116">As a local tool (applies to .NET Core SDK 3.0 and later).</span></span>

  <span data-ttu-id="17983-117">Pliki binarne narzędzia są instalowane w katalogu domyślnym.</span><span class="sxs-lookup"><span data-stu-id="17983-117">The tool binaries are installed in a default directory.</span></span> <span data-ttu-id="17983-118">Należy wywołać narzędzie z katalogu instalacyjnego lub któregokolwiek z jego podkatalogów.</span><span class="sxs-lookup"><span data-stu-id="17983-118">You invoke the tool from the installation directory or any of its subdirectories.</span></span> <span data-ttu-id="17983-119">Różne katalogi mogą korzystać z różnych wersji tego samego narzędzia.</span><span class="sxs-lookup"><span data-stu-id="17983-119">Different directories can use different versions of the same tool.</span></span>
  
  <span data-ttu-id="17983-120">Interfejs wiersza polecenia platformy .NET używa plików manifestu do śledzenia, które narzędzia są instalowane jako lokalne w katalogu.</span><span class="sxs-lookup"><span data-stu-id="17983-120">The .NET CLI uses manifest files to keep track of which tools are installed as local to a directory.</span></span> <span data-ttu-id="17983-121">Gdy plik manifestu jest zapisywany w katalogu głównym repozytorium kodu źródłowego, współautor może sklonować repozytorium i wywoływać pojedyncze polecenie interfejsu wiersza polecenia platformy .NET, które instaluje wszystkie narzędzia wymienione w plikach manifestu.</span><span class="sxs-lookup"><span data-stu-id="17983-121">When the manifest file is saved in the root directory of a source code repository, a contributor can clone the repository and invoke a single .NET CLI command that installs all of the tools listed in the manifest files.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="17983-122">Narzędzia platformy .NET działają w trybie pełnego zaufania.</span><span class="sxs-lookup"><span data-stu-id="17983-122">.NET tools run in full trust.</span></span> <span data-ttu-id="17983-123">Nie instaluj narzędzia platformy .NET, chyba że ufasz autorowi.</span><span class="sxs-lookup"><span data-stu-id="17983-123">Do not install a .NET tool unless you trust the author.</span></span>

## <a name="find-a-tool"></a><span data-ttu-id="17983-124">Znajdź narzędzie</span><span class="sxs-lookup"><span data-stu-id="17983-124">Find a tool</span></span>

<span data-ttu-id="17983-125">Oto kilka sposobów znajdowania narzędzi:</span><span class="sxs-lookup"><span data-stu-id="17983-125">Here are some ways to find tools:</span></span>

* <span data-ttu-id="17983-126">Użyj polecenia [Search narzędzia dotnet](dotnet-tool-search.md) , aby znaleźć narzędzie, które jest publikowane w usłudze NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="17983-126">Use the [dotnet tool search](dotnet-tool-search.md) command to find a tool that is published to NuGet.org.</span></span>
* <span data-ttu-id="17983-127">Przeszukaj witrynę sieci Web [NuGet](https://www.nuget.org) przy użyciu filtru typu pakietu "narzędzie .NET".</span><span class="sxs-lookup"><span data-stu-id="17983-127">Search the [NuGet](https://www.nuget.org) website by using the ".NET tool" package type filter.</span></span> <span data-ttu-id="17983-128">Aby uzyskać więcej informacji, zobacz [Znajdowanie i wybieranie pakietów](/nuget/consume-packages/finding-and-choosing-packages).</span><span class="sxs-lookup"><span data-stu-id="17983-128">For more information, see [Finding and choosing packages](/nuget/consume-packages/finding-and-choosing-packages).</span></span>
* <span data-ttu-id="17983-129">Zobacz kod źródłowy narzędzi utworzonych przez zespół ASP.NET Core w [katalogu Tools w repozytorium GitHub/aspnetcore](https://github.com/dotnet/aspnetcore/tree/master/src/Tools).</span><span class="sxs-lookup"><span data-stu-id="17983-129">See the source code for the tools created by the ASP.NET Core team in the [Tools directory of the dotnet/aspnetcore GitHub repository](https://github.com/dotnet/aspnetcore/tree/master/src/Tools).</span></span>
* <span data-ttu-id="17983-130">Informacje o narzędziach diagnostycznych w [narzędziach diagnostycznych platformy .NET](../diagnostics/index.md#net-core-diagnostic-global-tools).</span><span class="sxs-lookup"><span data-stu-id="17983-130">Learn about diagnostic tools at [.NET diagnostic tools](../diagnostics/index.md#net-core-diagnostic-global-tools).</span></span>

## <a name="check-the-author-and-statistics"></a><span data-ttu-id="17983-131">Sprawdź autora i statystyki</span><span class="sxs-lookup"><span data-stu-id="17983-131">Check the author and statistics</span></span>

<span data-ttu-id="17983-132">Ponieważ narzędzia platformy .NET działają w trybie pełnego zaufania, a narzędzia globalne są dodawane do zmiennej środowiskowej PATH, mogą być bardzo wydajne.</span><span class="sxs-lookup"><span data-stu-id="17983-132">Since .NET tools run in full trust, and global tools are added to the PATH environment variable, they can be very powerful.</span></span> <span data-ttu-id="17983-133">Nie pobieraj narzędzi z osób, które nie są zaufane.</span><span class="sxs-lookup"><span data-stu-id="17983-133">Don't download tools from people you don't trust.</span></span>

<span data-ttu-id="17983-134">Jeśli narzędzie jest hostowane w usłudze NuGet, można sprawdzić autora i statystyk, wyszukując narzędzie.</span><span class="sxs-lookup"><span data-stu-id="17983-134">If the tool is hosted on NuGet, you can check the author and statistics by searching for the tool.</span></span>

## <a name="install-a-global-tool"></a><span data-ttu-id="17983-135">Instalowanie narzędzia globalnego</span><span class="sxs-lookup"><span data-stu-id="17983-135">Install a global tool</span></span>

<span data-ttu-id="17983-136">Aby zainstalować narzędzie jako narzędzie globalne, użyj `-g` lub `--global` opcji [instalacji narzędzia dotnet](dotnet-tool-install.md), jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="17983-136">To install a tool as a global tool, use the `-g` or `--global` option of [dotnet tool install](dotnet-tool-install.md), as shown in the following example:</span></span>

```dotnetcli
dotnet tool install -g dotnetsay
```

<span data-ttu-id="17983-137">Dane wyjściowe przedstawiają polecenie używane do wywołania narzędzia i zainstalowanej wersji, podobnie jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="17983-137">The output shows the command used to invoke the tool and the version installed, similar to the following example:</span></span>

```output
You can invoke the tool using the following command: dotnetsay
Tool 'dotnetsay' (version '2.1.4') was successfully installed.
```

<span data-ttu-id="17983-138">Domyślna lokalizacja plików binarnych narzędzia zależy od systemu operacyjnego:</span><span class="sxs-lookup"><span data-stu-id="17983-138">The default location for a tool's binaries depends on the operating system:</span></span>

| <span data-ttu-id="17983-139">System operacyjny</span><span class="sxs-lookup"><span data-stu-id="17983-139">OS</span></span>          | <span data-ttu-id="17983-140">Ścieżka</span><span class="sxs-lookup"><span data-stu-id="17983-140">Path</span></span>                          |
|-------------|-------------------------------|
| <span data-ttu-id="17983-141">Linux/macOS</span><span class="sxs-lookup"><span data-stu-id="17983-141">Linux/macOS</span></span> | `$HOME/.dotnet/tools`         |
| <span data-ttu-id="17983-142">Windows</span><span class="sxs-lookup"><span data-stu-id="17983-142">Windows</span></span>     | `%USERPROFILE%\.dotnet\tools` |

<span data-ttu-id="17983-143">Ta lokalizacja jest dodawana do ścieżki użytkownika podczas pierwszego uruchomienia zestawu SDK, dzięki czemu narzędzia globalne mogą być wywoływane z dowolnego katalogu bez określania lokalizacji narzędzia.</span><span class="sxs-lookup"><span data-stu-id="17983-143">This location is added to the user's path when the SDK is first run, so global tools can be invoked from any directory without specifying the tool location.</span></span>

<span data-ttu-id="17983-144">Dostęp do narzędzi to specyficzne dla użytkownika, a nie globalne maszyny.</span><span class="sxs-lookup"><span data-stu-id="17983-144">Tool access is user-specific, not machine global.</span></span> <span data-ttu-id="17983-145">Narzędzie globalne jest dostępne tylko dla użytkownika, który zainstalował narzędzie.</span><span class="sxs-lookup"><span data-stu-id="17983-145">A global tool is only available to the user that installed the tool.</span></span>

### <a name="install-a-global-tool-in-a-custom-location"></a><span data-ttu-id="17983-146">Instalowanie narzędzia globalnego w niestandardowej lokalizacji</span><span class="sxs-lookup"><span data-stu-id="17983-146">Install a global tool in a custom location</span></span>

<span data-ttu-id="17983-147">Aby zainstalować narzędzie jako narzędzie globalne w niestandardowej lokalizacji, użyj `--tool-path` opcji [Instalacja narzędzia dotnet](dotnet-tool-install.md), jak pokazano w poniższych przykładach.</span><span class="sxs-lookup"><span data-stu-id="17983-147">To install a tool as a global tool in a custom location, use the `--tool-path` option of [dotnet tool install](dotnet-tool-install.md), as shown in the following examples.</span></span>

<span data-ttu-id="17983-148">W systemie Windows:</span><span class="sxs-lookup"><span data-stu-id="17983-148">On Windows:</span></span>

```dotnetcli
dotnet tool install dotnetsay --tool-path c:\dotnet-tools
```

<span data-ttu-id="17983-149">W systemie Linux lub macOS:</span><span class="sxs-lookup"><span data-stu-id="17983-149">On Linux or macOS:</span></span>

```dotnetcli
dotnet tool install dotnetsay --tool-path ~/bin
```

<span data-ttu-id="17983-150">Zestaw SDK platformy .NET nie dodaje automatycznie tej lokalizacji do zmiennej środowiskowej PATH.</span><span class="sxs-lookup"><span data-stu-id="17983-150">The .NET SDK doesn't add this location automatically to the PATH environment variable.</span></span> <span data-ttu-id="17983-151">Aby [wywołać narzędzie ścieżki narzędzi](#invoke-a-tool-path-tool), należy upewnić się, że polecenie jest dostępne za pomocą jednej z następujących metod:</span><span class="sxs-lookup"><span data-stu-id="17983-151">To [invoke a tool-path tool](#invoke-a-tool-path-tool), you have to make sure the command is available by using one of the following methods:</span></span>

* <span data-ttu-id="17983-152">Dodaj katalog instalacyjny do zmiennej środowiskowej PATH.</span><span class="sxs-lookup"><span data-stu-id="17983-152">Add the installation directory to the PATH environment variable.</span></span>
* <span data-ttu-id="17983-153">Określ pełną ścieżkę do narzędzia podczas jego wywoływania.</span><span class="sxs-lookup"><span data-stu-id="17983-153">Specify the full path to the tool when you invoke it.</span></span>
* <span data-ttu-id="17983-154">Wywołaj narzędzie z katalogu instalacyjnego.</span><span class="sxs-lookup"><span data-stu-id="17983-154">Invoke the tool from within the installation directory.</span></span>

## <a name="install-a-local-tool"></a><span data-ttu-id="17983-155">Instalowanie narzędzia lokalnego</span><span class="sxs-lookup"><span data-stu-id="17983-155">Install a local tool</span></span>

<span data-ttu-id="17983-156">**Dotyczy zestawu .NET Core 3,0 SDK i nowszych wersji.**</span><span class="sxs-lookup"><span data-stu-id="17983-156">**Applies to .NET Core 3.0 SDK and later.**</span></span>

<span data-ttu-id="17983-157">Aby zainstalować narzędzie tylko do dostępu lokalnego (dla bieżącego katalogu i podkatalogów), należy dodać je do pliku manifestu narzędzia.</span><span class="sxs-lookup"><span data-stu-id="17983-157">To install a tool for local access only (for the current directory and subdirectories), it has to be added to a tool manifest file.</span></span> <span data-ttu-id="17983-158">Aby utworzyć plik manifestu narzędzia, uruchom `dotnet new tool-manifest` polecenie:</span><span class="sxs-lookup"><span data-stu-id="17983-158">To create a tool manifest file, run the `dotnet new tool-manifest` command:</span></span>

```dotnetcli
dotnet new tool-manifest
```

<span data-ttu-id="17983-159">To polecenie tworzy plik manifestu o nazwie *dotnet-tools.jsw* katalogu *. config* .</span><span class="sxs-lookup"><span data-stu-id="17983-159">This command creates a manifest file named *dotnet-tools.json* under the *.config* directory.</span></span> <span data-ttu-id="17983-160">Aby dodać narzędzie lokalne do pliku manifestu, należy użyć polecenia [Zainstaluj narzędzie dotnet](dotnet-tool-install.md) i **pominąć** `--global` `--tool-path` Opcje i, jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="17983-160">To add a local tool to the manifest file, use the [dotnet tool install](dotnet-tool-install.md) command and **omit** the `--global` and `--tool-path` options, as shown in the following example:</span></span>

```dotnetcli
dotnet tool install dotnetsay
```

<span data-ttu-id="17983-161">Dane wyjściowe polecenia pokazują plik manifestu, w którym znajduje się nowo zainstalowane narzędzie, podobnie jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="17983-161">The command output shows which manifest file the newly installed tool is in, similar to the following example:</span></span>

```console
You can invoke the tool from this directory using the following command:
dotnet tool run dotnetsay
Tool 'dotnetsay' (version '2.1.4') was successfully installed.
Entry is added to the manifest file /home/name/botsay/.config/dotnet-tools.json.
```

<span data-ttu-id="17983-162">W poniższym przykładzie przedstawiono plik manifestu z zainstalowanymi dwoma lokalnymi narzędziami:</span><span class="sxs-lookup"><span data-stu-id="17983-162">The following example shows a manifest file with two local tools installed:</span></span>

```json
{
  "version": 1,
  "isRoot": true,
  "tools": {
    "botsay": {
      "version": "1.0.0",
      "commands": [
        "botsay"
      ]
    },
    "dotnetsay": {
      "version": "2.1.3",
      "commands": [
        "dotnetsay"
      ]
    }
  }
}
```

<span data-ttu-id="17983-163">Zazwyczaj można dodać lokalne narzędzie do katalogu głównego repozytorium.</span><span class="sxs-lookup"><span data-stu-id="17983-163">You typically add a local tool to the root directory of the repository.</span></span> <span data-ttu-id="17983-164">Po zaewidencjonowaniu pliku manifestu do repozytorium, deweloperzy, którzy ewidencjonują kod z repozytorium, pobierają najnowszy plik manifestu.</span><span class="sxs-lookup"><span data-stu-id="17983-164">After you check in the manifest file to the repository, developers who check out code from the repository get the latest manifest file.</span></span> <span data-ttu-id="17983-165">Aby zainstalować wszystkie narzędzia wymienione w pliku manifestu, uruchom `dotnet tool restore` polecenie:</span><span class="sxs-lookup"><span data-stu-id="17983-165">To install all of the tools listed in the manifest file, they run the `dotnet tool restore` command:</span></span>

```dotnetcli
dotnet tool restore
```

<span data-ttu-id="17983-166">Dane wyjściowe wskazują, które narzędzia zostały przywrócone:</span><span class="sxs-lookup"><span data-stu-id="17983-166">The output indicates which tools were restored:</span></span>

```console
Tool 'botsay' (version '1.0.0') was restored. Available commands: botsay
Tool 'dotnetsay' (version '2.1.3') was restored. Available commands: dotnetsay
Restore was successful.
```

## <a name="install-a-specific-tool-version"></a><span data-ttu-id="17983-167">Zainstaluj określoną wersję narzędzia</span><span class="sxs-lookup"><span data-stu-id="17983-167">Install a specific tool version</span></span>

<span data-ttu-id="17983-168">Aby zainstalować wersję wstępną lub określoną wersję narzędzia, należy określić numer wersji przy użyciu `--version` opcji, jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="17983-168">To install a pre-release version or a specific version of a tool, specify the version number by using the `--version` option, as shown in the following example:</span></span>

```dotnetcli
dotnet tool install dotnetsay --version 2.1.3
```

## <a name="use-a-tool"></a><span data-ttu-id="17983-169">Korzystanie z narzędzia</span><span class="sxs-lookup"><span data-stu-id="17983-169">Use a tool</span></span>

<span data-ttu-id="17983-170">Polecenie używane do wywoływania narzędzia może różnić się od nazwy instalowanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="17983-170">The command that you use to invoke a tool may be different from the name of the package that you install.</span></span> <span data-ttu-id="17983-171">Aby wyświetlić wszystkie narzędzia aktualnie zainstalowane na komputerze dla bieżącego użytkownika, użyj polecenia z [listy narzędzi dotnet](dotnet-tool-list.md) :</span><span class="sxs-lookup"><span data-stu-id="17983-171">To display all of the tools currently installed on the machine for the current user, use the [dotnet tool list](dotnet-tool-list.md) command:</span></span>

```dotnetcli
dotnet tool list
```

<span data-ttu-id="17983-172">Dane wyjściowe wyświetlają wersję i polecenie każdego narzędzia, podobnie jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="17983-172">The output shows each tool's version and command, similar to the following example:</span></span>

```console
Package Id      Version      Commands       Manifest
-------------------------------------------------------------------------------------------
botsay          1.0.0        botsay         /home/name/repository/.config/dotnet-tools.json
dotnetsay       2.1.3        dotnetsay      /home/name/repository/.config/dotnet-tools.json
```

<span data-ttu-id="17983-173">Jak pokazano w tym przykładzie, lista zawiera narzędzia lokalne.</span><span class="sxs-lookup"><span data-stu-id="17983-173">As shown in this example, the list shows local tools.</span></span> <span data-ttu-id="17983-174">Aby wyświetlić narzędzia globalne, użyj `--global` opcji i, aby zobaczyć narzędzia ścieżki narzędzi, użyj `--tool-path` opcji.</span><span class="sxs-lookup"><span data-stu-id="17983-174">To see global tools, use the `--global` option, and to see tool-path tools, use the `--tool-path` option.</span></span>

### <a name="invoke-a-global-tool"></a><span data-ttu-id="17983-175">Wywołaj narzędzie globalne</span><span class="sxs-lookup"><span data-stu-id="17983-175">Invoke a global tool</span></span>

<span data-ttu-id="17983-176">W przypadku narzędzi globalnych Użyj narzędzia.</span><span class="sxs-lookup"><span data-stu-id="17983-176">For global tools, use the tool command by itself.</span></span> <span data-ttu-id="17983-177">Na przykład jeśli polecenie jest `dotnetsay` lub, to jest `dotnet-doc` używane do wywołania polecenia:</span><span class="sxs-lookup"><span data-stu-id="17983-177">For example, if the command is `dotnetsay` or `dotnet-doc`, that's what you use to invoke the command:</span></span>

```console
dotnetsay
dotnet-doc
```

<span data-ttu-id="17983-178">Jeśli polecenie zaczyna się od prefiksu `dotnet-` , alternatywnym sposobem wywołania narzędzia jest użycie `dotnet` polecenia i pominięcie prefiksu polecenia narzędzia.</span><span class="sxs-lookup"><span data-stu-id="17983-178">If the command begins with the prefix `dotnet-`, an alternative way to invoke the tool is to use the `dotnet` command and omit the tool command prefix.</span></span> <span data-ttu-id="17983-179">Na przykład, jeśli polecenie ma wartość `dotnet-doc` , następujące polecenie wywołuje narzędzie:</span><span class="sxs-lookup"><span data-stu-id="17983-179">For example, if the command is `dotnet-doc`, the following command invokes the tool:</span></span>

```dotnetcli
dotnet doc
```

<span data-ttu-id="17983-180">Jednak w poniższym scenariuszu nie można użyć `dotnet` polecenia do wywołania narzędzia globalnego:</span><span class="sxs-lookup"><span data-stu-id="17983-180">However, in the following scenario you can't use the `dotnet` command to invoke a global tool:</span></span>

* <span data-ttu-id="17983-181">Narzędzie globalne i narzędzie lokalne mają to samo polecenie poprzedzone przez program `dotnet-` .</span><span class="sxs-lookup"><span data-stu-id="17983-181">A global tool and a local tool have the same command prefixed by `dotnet-`.</span></span>
* <span data-ttu-id="17983-182">Chcesz wywołać narzędzie globalne z katalogu, który znajduje się w zakresie dla narzędzia lokalnego.</span><span class="sxs-lookup"><span data-stu-id="17983-182">You want to invoke the global tool from a directory that is in scope for the local tool.</span></span>

<span data-ttu-id="17983-183">W tym scenariuszu `dotnet doc` i `dotnet dotnet-doc` Wywołaj narzędzie lokalne.</span><span class="sxs-lookup"><span data-stu-id="17983-183">In this scenario, `dotnet doc` and `dotnet dotnet-doc` invoke the local tool.</span></span> <span data-ttu-id="17983-184">Aby wywołać narzędzie globalne, użyj polecenia przez samego siebie:</span><span class="sxs-lookup"><span data-stu-id="17983-184">To invoke the global tool, use the command by itself:</span></span>

```dotnetcli
dotnet-doc
```

### <a name="invoke-a-tool-path-tool"></a><span data-ttu-id="17983-185">Wywołaj narzędzie ścieżki narzędziowej</span><span class="sxs-lookup"><span data-stu-id="17983-185">Invoke a tool-path tool</span></span>

<span data-ttu-id="17983-186">Aby wywołać narzędzie globalne, które jest instalowane przy użyciu `tool-path` opcji, upewnij się, że polecenie jest dostępne, zgodnie z opisem [we wcześniejszej części tego artykułu](#install-a-global-tool-in-a-custom-location).</span><span class="sxs-lookup"><span data-stu-id="17983-186">To invoke a global tool that is installed by using the `tool-path` option, make sure the command is available, as explained [earlier in this article](#install-a-global-tool-in-a-custom-location).</span></span>

### <a name="invoke-a-local-tool"></a><span data-ttu-id="17983-187">Wywoływanie narzędzia lokalnego</span><span class="sxs-lookup"><span data-stu-id="17983-187">Invoke a local tool</span></span>

<span data-ttu-id="17983-188">Aby wywołać narzędzie lokalne, należy użyć `dotnet` polecenia z katalogu instalacyjnego.</span><span class="sxs-lookup"><span data-stu-id="17983-188">To invoke a local tool, you have to use the `dotnet` command from within the installation directory.</span></span> <span data-ttu-id="17983-189">Możesz użyć długiej formy ( `dotnet tool run <COMMAND_NAME>` ) lub krótkiej formy ( `dotnet <COMMAND_NAME>` ), jak pokazano w następujących przykładach:</span><span class="sxs-lookup"><span data-stu-id="17983-189">You can use the long form (`dotnet tool run <COMMAND_NAME>`) or the short form (`dotnet <COMMAND_NAME>`), as shown in the following examples:</span></span>

```dotnetcli
dotnet tool run dotnetsay
dotnet dotnetsay
```

<span data-ttu-id="17983-190">Jeśli polecenie jest poprzedzone przez `dotnet-` , można dołączyć lub pominąć prefiks po wywołaniu narzędzia.</span><span class="sxs-lookup"><span data-stu-id="17983-190">If the command is prefixed by `dotnet-`, you can include or omit the prefix when you invoke the tool.</span></span> <span data-ttu-id="17983-191">Na przykład, jeśli polecenie jest `dotnet-doc` , każdy z poniższych przykładów wywoła narzędzie lokalne:</span><span class="sxs-lookup"><span data-stu-id="17983-191">For example, if the command is `dotnet-doc`, any of the following examples invokes the local tool:</span></span>

```dotnetcli
dotnet tool run dotnet-doc
dotnet dotnet-doc
dotnet doc
```

## <a name="update-a-tool"></a><span data-ttu-id="17983-192">Aktualizowanie narzędzia</span><span class="sxs-lookup"><span data-stu-id="17983-192">Update a tool</span></span>

<span data-ttu-id="17983-193">Aktualizacja narzędzia polega na odinstalowaniu i ponownym zainstalowaniu go z najnowszą stabilną wersją.</span><span class="sxs-lookup"><span data-stu-id="17983-193">Updating a tool involves uninstalling and reinstalling it with the latest stable version.</span></span> <span data-ttu-id="17983-194">Aby zaktualizować narzędzie, należy użyć polecenia " [Update" narzędzia dotnet](dotnet-tool-update.md) z tą samą opcją, która została użyta do zainstalowania narzędzia:</span><span class="sxs-lookup"><span data-stu-id="17983-194">To update a tool, use the [dotnet tool update](dotnet-tool-update.md) command with the same option that you used to install the tool:</span></span>

```dotnetcli
dotnet tool update --global <packagename>
dotnet tool update --tool-path <packagename>
dotnet tool update <packagename>
```

<span data-ttu-id="17983-195">W przypadku narzędzia lokalnego zestaw SDK znajduje pierwszy plik manifestu zawierający identyfikator pakietu, przeszukując bieżący katalog i katalogi nadrzędne.</span><span class="sxs-lookup"><span data-stu-id="17983-195">For a local tool, the SDK finds the first manifest file that contains the package ID by looking in the current directory and parent directories.</span></span> <span data-ttu-id="17983-196">Jeśli w pliku manifestu nie ma takiego identyfikatora pakietu, zestaw SDK dodaje nowy wpis do najbliższego pliku manifestu.</span><span class="sxs-lookup"><span data-stu-id="17983-196">If there is no such package ID in any manifest file, the SDK adds a new entry to the closest manifest file.</span></span>

## <a name="uninstall-a-tool"></a><span data-ttu-id="17983-197">Odinstalowywanie narzędzia</span><span class="sxs-lookup"><span data-stu-id="17983-197">Uninstall a tool</span></span>

<span data-ttu-id="17983-198">Usuń narzędzie za pomocą [Narzędzia dotnet Command Uninstall](dotnet-tool-uninstall.md) polecenie z tą samą opcją, która została użyta do zainstalowania narzędzia:</span><span class="sxs-lookup"><span data-stu-id="17983-198">Remove a tool by using the [dotnet tool uninstall](dotnet-tool-uninstall.md) command with the same option that you used to install the tool:</span></span>

```dotnetcli
dotnet tool uninstall --global <packagename>
dotnet tool uninstall --tool-path <packagename>
dotnet tool uninstall <packagename>
```

<span data-ttu-id="17983-199">W przypadku narzędzia lokalnego zestaw SDK znajduje pierwszy plik manifestu zawierający identyfikator pakietu, przeszukując bieżący katalog i katalogi nadrzędne.</span><span class="sxs-lookup"><span data-stu-id="17983-199">For a local tool, the SDK finds the first manifest file that contains the package ID by looking in the current directory and parent directories.</span></span>

## <a name="get-help-and-troubleshoot"></a><span data-ttu-id="17983-200">Uzyskiwanie pomocy i rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="17983-200">Get help and troubleshoot</span></span>

<span data-ttu-id="17983-201">Aby uzyskać listę dostępnych `dotnet tool` poleceń, wprowadź następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="17983-201">To get a list of available `dotnet tool` commands, enter the following command:</span></span>

```dotnetcli
dotnet tool --help
```

<span data-ttu-id="17983-202">Aby uzyskać instrukcje dotyczące użycia narzędzia, wprowadź jedno z następujących poleceń lub zapoznaj się z witryną sieci Web narzędzia:</span><span class="sxs-lookup"><span data-stu-id="17983-202">To get tool usage instructions, enter one of the following commands or see the tool's website:</span></span>

```dotnetcli
<command> --help
dotnet <command> --help
```

<span data-ttu-id="17983-203">Jeśli instalacja lub uruchomienie narzędzia nie powiedzie się, zobacz [Rozwiązywanie problemów z użyciem narzędzia platformy .NET](troubleshoot-usage-issues.md).</span><span class="sxs-lookup"><span data-stu-id="17983-203">If a tool fails to install or run, see [Troubleshoot .NET tool usage issues](troubleshoot-usage-issues.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="17983-204">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="17983-204">See also</span></span>

- [<span data-ttu-id="17983-205">Samouczek: Tworzenie narzędzia platformy .NET przy użyciu interfejsu wiersza polecenia platformy .NET</span><span class="sxs-lookup"><span data-stu-id="17983-205">Tutorial: Create a .NET tool using the .NET CLI</span></span>](global-tools-how-to-create.md)
- [<span data-ttu-id="17983-206">Samouczek: Instalowanie i używanie narzędzia globalnego platformy .NET przy użyciu interfejsu wiersza polecenia platformy .NET</span><span class="sxs-lookup"><span data-stu-id="17983-206">Tutorial: Install and use a .NET global tool using the .NET CLI</span></span>](global-tools-how-to-use.md)
- [<span data-ttu-id="17983-207">Samouczek: Instalowanie i używanie lokalnego narzędzia .NET przy użyciu interfejsu wiersza polecenia platformy .NET</span><span class="sxs-lookup"><span data-stu-id="17983-207">Tutorial: Install and use a .NET local tool using the .NET CLI</span></span>](local-tools-how-to-use.md)
