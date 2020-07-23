---
title: polecenia wypychania NuGet dotnet
description: Polecenie polecenia push NuGet narzędzia dotnet wypycha pakiet do serwera i opublikuje go.
author: karann-msft
ms.date: 02/14/2020
ms.openlocfilehash: 608cd05d94dd6b5cdc53d582cfaa0407f011ff37
ms.sourcegitcommit: 40de8df14289e1e05b40d6e5c1daabd3c286d70c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/22/2020
ms.locfileid: "86925517"
---
# <a name="dotnet-nuget-push"></a><span data-ttu-id="0d56f-103">dotnet nuget push</span><span class="sxs-lookup"><span data-stu-id="0d56f-103">dotnet nuget push</span></span>

<span data-ttu-id="0d56f-104">**Ten artykuł ma zastosowanie do:** ✔️ .NET Core 2. x SDK i nowszych wersji</span><span class="sxs-lookup"><span data-stu-id="0d56f-104">**This article applies to:** ✔️ .NET Core 2.x SDK and later versions</span></span>

## <a name="name"></a><span data-ttu-id="0d56f-105">Nazwa</span><span class="sxs-lookup"><span data-stu-id="0d56f-105">Name</span></span>

<span data-ttu-id="0d56f-106">`dotnet nuget push`— Wypchnij pakiet do serwera i opublikuje go.</span><span class="sxs-lookup"><span data-stu-id="0d56f-106">`dotnet nuget push` - Pushes a package to the server and publishes it.</span></span>

## <a name="synopsis"></a><span data-ttu-id="0d56f-107">Streszczenie</span><span class="sxs-lookup"><span data-stu-id="0d56f-107">Synopsis</span></span>

```dotnetcli
dotnet nuget push [<ROOT>] [-d|--disable-buffering] [--force-english-output]
    [--interactive] [-k|--api-key <API_KEY>] [-n|--no-symbols true]
    [--no-service-endpoint] [-s|--source <SOURCE>] [--skip-duplicate]
    [-sk|--symbol-api-key <API_KEY>] [-ss|--symbol-source <SOURCE>]
    [-t|--timeout <TIMEOUT>]

dotnet nuget push -h|--help
```

## <a name="description"></a><span data-ttu-id="0d56f-108">Opis</span><span class="sxs-lookup"><span data-stu-id="0d56f-108">Description</span></span>

<span data-ttu-id="0d56f-109">`dotnet nuget push`Polecenie wypycha pakiet do serwera i opublikuje go.</span><span class="sxs-lookup"><span data-stu-id="0d56f-109">The `dotnet nuget push` command pushes a package to the server and publishes it.</span></span> <span data-ttu-id="0d56f-110">Polecenie push używa informacji o serwerze i poświadczeniach znajdujących się w pliku konfiguracyjnym NuGet systemu lub w łańcuchu plików konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="0d56f-110">The push command uses server and credential details found in the system's NuGet config file or chain of config files.</span></span> <span data-ttu-id="0d56f-111">Aby uzyskać więcej informacji na temat plików konfiguracji, zobacz [Konfigurowanie zachowania NuGet](/nuget/consume-packages/configuring-nuget-behavior).</span><span class="sxs-lookup"><span data-stu-id="0d56f-111">For more information on config files, see [Configuring NuGet Behavior](/nuget/consume-packages/configuring-nuget-behavior).</span></span> <span data-ttu-id="0d56f-112">Domyślna konfiguracja narzędzia NuGet jest uzyskiwana przez załadowanie pliku *% AppData% \NuGet\NuGet.config* (Windows) lub *$Home/.local/share* (Linux/macOS), a następnie załadowanie dowolnych *nuget.config* lub *.nuget\nuget.config* począwszy od katalogu głównego dysku i kończącego się w bieżącym katalogu.</span><span class="sxs-lookup"><span data-stu-id="0d56f-112">NuGet's default configuration is obtained by loading *%AppData%\NuGet\NuGet.config* (Windows) or *$HOME/.local/share* (Linux/macOS), then loading any *nuget.config* or *.nuget\nuget.config* starting from the root of drive and ending in the current directory.</span></span>

<span data-ttu-id="0d56f-113">Polecenie wypycha istniejący pakiet.</span><span class="sxs-lookup"><span data-stu-id="0d56f-113">The command pushes an existing package.</span></span> <span data-ttu-id="0d56f-114">Nie tworzy pakietu.</span><span class="sxs-lookup"><span data-stu-id="0d56f-114">It doesn't create a package.</span></span> <span data-ttu-id="0d56f-115">Aby utworzyć pakiet, użyj [`dotnet pack`](dotnet-pack.md) .</span><span class="sxs-lookup"><span data-stu-id="0d56f-115">To create a package, use [`dotnet pack`](dotnet-pack.md).</span></span>

## <a name="arguments"></a><span data-ttu-id="0d56f-116">Argumenty</span><span class="sxs-lookup"><span data-stu-id="0d56f-116">Arguments</span></span>

- **`ROOT`**

  <span data-ttu-id="0d56f-117">Określa ścieżkę pliku do pakietu do wypchnięcia.</span><span class="sxs-lookup"><span data-stu-id="0d56f-117">Specifies the file path to the package to be pushed.</span></span>

## <a name="options"></a><span data-ttu-id="0d56f-118">Opcje</span><span class="sxs-lookup"><span data-stu-id="0d56f-118">Options</span></span>

- **`-d|--disable-buffering`**

  <span data-ttu-id="0d56f-119">Wyłącza buforowanie podczas wypychania do serwera HTTP (S) w celu zmniejszenia użycia pamięci.</span><span class="sxs-lookup"><span data-stu-id="0d56f-119">Disables buffering when pushing to an HTTP(S) server to reduce memory usage.</span></span>

- **`--force-english-output`**

  <span data-ttu-id="0d56f-120">Wymusza uruchomienie aplikacji przy użyciu niezmiennej, opartej na języku angielskim kultury.</span><span class="sxs-lookup"><span data-stu-id="0d56f-120">Forces the application to run using an invariant, English-based culture.</span></span>

- **`-h|--help`**

  <span data-ttu-id="0d56f-121">Drukuje krótką pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="0d56f-121">Prints out a short help for the command.</span></span>

- **`--interactive`**

  <span data-ttu-id="0d56f-122">Umożliwia zablokowanie polecenia i wymaga ręcznej akcji dla operacji takich jak uwierzytelnianie.</span><span class="sxs-lookup"><span data-stu-id="0d56f-122">Allows the command to block and requires manual action for operations like authentication.</span></span> <span data-ttu-id="0d56f-123">Opcja dostępna od wersji .NET Core 2,2 SDK.</span><span class="sxs-lookup"><span data-stu-id="0d56f-123">Option available since .NET Core 2.2 SDK.</span></span>

- **`-k|--api-key <API_KEY>`**

  <span data-ttu-id="0d56f-124">Klucz interfejsu API dla serwera programu.</span><span class="sxs-lookup"><span data-stu-id="0d56f-124">The API key for the server.</span></span>

- **`-n|--no-symbols true`**

  <span data-ttu-id="0d56f-125">Nie Wypychaj symboli (nawet jeśli istnieją).</span><span class="sxs-lookup"><span data-stu-id="0d56f-125">Doesn't push symbols (even if present).</span></span>

- **`--no-service-endpoint`**

  <span data-ttu-id="0d56f-126">Nie dołącza "API/v2/Package" do źródłowego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="0d56f-126">Doesn't append "api/v2/package" to the source URL.</span></span> <span data-ttu-id="0d56f-127">Opcja dostępna od wersji .NET Core 2,1 SDK.</span><span class="sxs-lookup"><span data-stu-id="0d56f-127">Option available since .NET Core 2.1 SDK.</span></span>

- **`-s|--source <SOURCE>`**

  <span data-ttu-id="0d56f-128">Określa adres URL serwera.</span><span class="sxs-lookup"><span data-stu-id="0d56f-128">Specifies the server URL.</span></span> <span data-ttu-id="0d56f-129">Ta opcja jest wymagana, chyba że `DefaultPushSource` wartość konfiguracji jest ustawiona w pliku konfiguracyjnym NuGet.</span><span class="sxs-lookup"><span data-stu-id="0d56f-129">This option is required unless `DefaultPushSource` config value is set in the NuGet config file.</span></span>

- **`--skip-duplicate`**

  <span data-ttu-id="0d56f-130">Podczas wypychania wielu pakietów do serwera HTTP (S) program traktuje wszystkie 409 odpowiedzi w konflikcie jako ostrzeżenie, aby można było kontynuować wypychanie.</span><span class="sxs-lookup"><span data-stu-id="0d56f-130">When pushing multiple packages to an HTTP(S) server, treats any 409 Conflict response as a warning so that the push can continue.</span></span> <span data-ttu-id="0d56f-131">Dostępne od wersji .NET Core 3,1 SDK.</span><span class="sxs-lookup"><span data-stu-id="0d56f-131">Available since .NET Core 3.1 SDK.</span></span>

- **`-sk|--symbol-api-key <API_KEY>`**

  <span data-ttu-id="0d56f-132">Klucz interfejsu API dla serwera symboli.</span><span class="sxs-lookup"><span data-stu-id="0d56f-132">The API key for the symbol server.</span></span>

- **`-ss|--symbol-source <SOURCE>`**

  <span data-ttu-id="0d56f-133">Określa adres URL serwera symboli.</span><span class="sxs-lookup"><span data-stu-id="0d56f-133">Specifies the symbol server URL.</span></span>

- **`-t|--timeout <TIMEOUT>`**

  <span data-ttu-id="0d56f-134">Określa limit czasu wypychania do serwera w sekundach.</span><span class="sxs-lookup"><span data-stu-id="0d56f-134">Specifies the timeout for pushing to a server in seconds.</span></span> <span data-ttu-id="0d56f-135">Wartość domyślna to 300 sekund (5 minut).</span><span class="sxs-lookup"><span data-stu-id="0d56f-135">Defaults to 300 seconds (5 minutes).</span></span> <span data-ttu-id="0d56f-136">Wartość domyślna to 0 (zero sekund).</span><span class="sxs-lookup"><span data-stu-id="0d56f-136">Specifying 0 (zero seconds) applies the default value.</span></span>

## <a name="examples"></a><span data-ttu-id="0d56f-137">Przykłady</span><span class="sxs-lookup"><span data-stu-id="0d56f-137">Examples</span></span>

- <span data-ttu-id="0d56f-138">Wypychanie *foo. nupkg* do domyślnego źródła push, określając klucz interfejsu API:</span><span class="sxs-lookup"><span data-stu-id="0d56f-138">Push *foo.nupkg* to the default push source, specifying an API key:</span></span>

  ```dotnetcli
  dotnet nuget push foo.nupkg -k 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a
  ```

- <span data-ttu-id="0d56f-139">Wypychanie *foo. nupkg* do oficjalnego serwera NuGet, określając klucz interfejsu API:</span><span class="sxs-lookup"><span data-stu-id="0d56f-139">Push *foo.nupkg* to the official NuGet server, specifying an API key:</span></span>

  ```dotnetcli
  dotnet nuget push foo.nupkg -k 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s https://api.nuget.org/v3/index.json
  ```
  
  * <span data-ttu-id="0d56f-140">Wypychanie *foo. nupkg* do niestandardowego źródła wypychania `https://customsource` , określając klucz interfejsu API:</span><span class="sxs-lookup"><span data-stu-id="0d56f-140">Push *foo.nupkg* to the custom push source `https://customsource`, specifying an API key:</span></span>

  ```dotnetcli
  dotnet nuget push foo.nupkg -k 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s https://customsource/
  ```

- <span data-ttu-id="0d56f-141">Wypychanie *foo. nupkg* do domyślnego źródła push:</span><span class="sxs-lookup"><span data-stu-id="0d56f-141">Push *foo.nupkg* to the default push source:</span></span>

  ```dotnetcli
  dotnet nuget push foo.nupkg
  ```

- <span data-ttu-id="0d56f-142">Wypchnij *foo. Symbols. nupkg* do domyślnego źródła symboli:</span><span class="sxs-lookup"><span data-stu-id="0d56f-142">Push *foo.symbols.nupkg* to the default symbols source:</span></span>

  ```dotnetcli
  dotnet nuget push foo.symbols.nupkg
  ```

- <span data-ttu-id="0d56f-143">Wypchnij *foo. nupkg* do domyślnego źródła push, określając 360-sekundowy limit czasu:</span><span class="sxs-lookup"><span data-stu-id="0d56f-143">Push *foo.nupkg* to the default push source, specifying a 360-second timeout:</span></span>

  ```dotnetcli
  dotnet nuget push foo.nupkg --timeout 360
  ```

- <span data-ttu-id="0d56f-144">Wypchnij wszystkie pliki *. nupkg* w bieżącym katalogu do domyślnego źródła push:</span><span class="sxs-lookup"><span data-stu-id="0d56f-144">Push all *.nupkg* files in the current directory to the default push source:</span></span>

  ```dotnetcli
  dotnet nuget push *.nupkg
  ```

  > [!NOTE]
  > <span data-ttu-id="0d56f-145">Jeśli to polecenie nie działa, może to być spowodowane usterką, która istniała we wcześniejszych wersjach zestawu SDK (zestaw SDK programu .NET Core 2,1 i wcześniejsze wersje).</span><span class="sxs-lookup"><span data-stu-id="0d56f-145">If this command doesn't work, it might be due to a bug that existed in older versions of the SDK (.NET Core 2.1 SDK and earlier versions).</span></span>
  > <span data-ttu-id="0d56f-146">Aby rozwiązać ten problem, Uaktualnij wersję zestawu SDK lub zamiast tego Uruchom następujące polecenie:`dotnet nuget push **/*.nupkg`</span><span class="sxs-lookup"><span data-stu-id="0d56f-146">To fix this, upgrade your SDK version or run the following command instead: `dotnet nuget push **/*.nupkg`</span></span>

- <span data-ttu-id="0d56f-147">Wypchnij wszystkie pliki *NUPKG* , nawet jeśli odpowiedź na 409 jest zwracana przez serwer http (S):</span><span class="sxs-lookup"><span data-stu-id="0d56f-147">Push all *.nupkg* files even if a 409 Conflict response is returned by an HTTP(S) server:</span></span>

  ```dotnetcli
  dotnet nuget push *.nupkg --skip-duplicate
  ```

- <span data-ttu-id="0d56f-148">Wypchnij wszystkie pliki *. nupkg* w bieżącym katalogu do katalogu lokalnego źródła danych:</span><span class="sxs-lookup"><span data-stu-id="0d56f-148">Push all *.nupkg* files in the current directory to a local feed directory:</span></span>

  ```dotnetcli
  dotnet nuget push *.nupkg -s c:\mydir
  ```

  <span data-ttu-id="0d56f-149">To polecenie nie przechowuje pakietów w hierarchicznej strukturze folderów, co jest zalecane w celu zoptymalizowania wydajności.</span><span class="sxs-lookup"><span data-stu-id="0d56f-149">This command doesn't store packages in a hierarchical folder structure, which is recommended to optimize performance.</span></span> <span data-ttu-id="0d56f-150">Aby uzyskać więcej informacji, zobacz [lokalne źródła danych](/nuget/hosting-packages/local-feeds).</span><span class="sxs-lookup"><span data-stu-id="0d56f-150">For more information, see [Local feeds](/nuget/hosting-packages/local-feeds).</span></span>  
