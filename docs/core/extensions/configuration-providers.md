---
title: Dostawcy konfiguracji w programie .NET
description: Dowiedz się, w jaki sposób interfejs API dostawcy konfiguracji jest używany do konfigurowania aplikacji platformy .NET.
author: IEvangelist
ms.author: dapine
ms.date: 12/04/2020
ms.openlocfilehash: 301e23170428f2291ccaa1bd882007cadfbce3b1
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96740012"
---
# <a name="configuration-providers-in-net"></a><span data-ttu-id="e04c2-103">Dostawcy konfiguracji w programie .NET</span><span class="sxs-lookup"><span data-stu-id="e04c2-103">Configuration providers in .NET</span></span>

<span data-ttu-id="e04c2-104">Konfiguracja w programie .NET jest możliwa z dostawcami konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="e04c2-104">Configuration in .NET is possible with configuration providers.</span></span> <span data-ttu-id="e04c2-105">Istnieje kilka typów dostawców korzystających z różnych źródeł konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="e04c2-105">There are several types of providers that rely on various configuration sources.</span></span> <span data-ttu-id="e04c2-106">Ten artykuł zawiera szczegółowe informacje o różnych dostawcach konfiguracji i odpowiednich źródłach.</span><span class="sxs-lookup"><span data-stu-id="e04c2-106">This article details all of the different configuration providers and their corresponding sources.</span></span>

- [<span data-ttu-id="e04c2-107">Dostawca konfiguracji plików</span><span class="sxs-lookup"><span data-stu-id="e04c2-107">File configuration provider</span></span>](#file-configuration-provider)
- [<span data-ttu-id="e04c2-108">Dostawca konfiguracji zmiennej środowiskowej</span><span class="sxs-lookup"><span data-stu-id="e04c2-108">Environment variable configuration provider</span></span>](#environment-variable-configuration-provider)
- [<span data-ttu-id="e04c2-109">Dostawca konfiguracji wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="e04c2-109">Command-line configuration provider</span></span>](#command-line-configuration-provider)
- [<span data-ttu-id="e04c2-110">Dostawca konfiguracji klucza dla plików</span><span class="sxs-lookup"><span data-stu-id="e04c2-110">Key-per-file configuration provider</span></span>](#key-per-file-configuration-provider)
- [<span data-ttu-id="e04c2-111">Dostawca konfiguracji pamięci</span><span class="sxs-lookup"><span data-stu-id="e04c2-111">Memory configuration provider</span></span>](#memory-configuration-provider)

## <a name="file-configuration-provider"></a><span data-ttu-id="e04c2-112">Dostawca konfiguracji plików</span><span class="sxs-lookup"><span data-stu-id="e04c2-112">File configuration provider</span></span>

<span data-ttu-id="e04c2-113"><xref:Microsoft.Extensions.Configuration.FileConfigurationProvider> jest klasą bazową do ładowania konfiguracji z systemu plików.</span><span class="sxs-lookup"><span data-stu-id="e04c2-113"><xref:Microsoft.Extensions.Configuration.FileConfigurationProvider> is the base class for loading configuration from the file system.</span></span> <span data-ttu-id="e04c2-114">Następujący dostawcy konfiguracji pochodzą z `FileConfigurationProvider` :</span><span class="sxs-lookup"><span data-stu-id="e04c2-114">The following configuration providers derive from `FileConfigurationProvider`:</span></span>

- [<span data-ttu-id="e04c2-115">Dostawca konfiguracji JSON</span><span class="sxs-lookup"><span data-stu-id="e04c2-115">JSON configuration provider</span></span>](#json-configuration-provider)
- [<span data-ttu-id="e04c2-116">Dostawca konfiguracji XML</span><span class="sxs-lookup"><span data-stu-id="e04c2-116">XML configuration provider</span></span>](#xml-configuration-provider)
- [<span data-ttu-id="e04c2-117">Dostawca konfiguracji pliku INI</span><span class="sxs-lookup"><span data-stu-id="e04c2-117">INI configuration provider</span></span>](#ini-configuration-provider)

### <a name="json-configuration-provider"></a><span data-ttu-id="e04c2-118">Dostawca konfiguracji JSON</span><span class="sxs-lookup"><span data-stu-id="e04c2-118">JSON configuration provider</span></span>

<span data-ttu-id="e04c2-119"><xref:Microsoft.Extensions.Configuration.Json.JsonConfigurationProvider>Klasa ładuje konfigurację z pliku JSON.</span><span class="sxs-lookup"><span data-stu-id="e04c2-119">The <xref:Microsoft.Extensions.Configuration.Json.JsonConfigurationProvider> class loads configuration from a JSON file.</span></span> <span data-ttu-id="e04c2-120">Zainstaluj [`Microsoft.Extensions.Configuration.Json`](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.Json) pakiet NuGet.</span><span class="sxs-lookup"><span data-stu-id="e04c2-120">Install the [`Microsoft.Extensions.Configuration.Json`](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.Json) NuGet package.</span></span>

<span data-ttu-id="e04c2-121">Przeciążenia mogą określać:</span><span class="sxs-lookup"><span data-stu-id="e04c2-121">Overloads can specify:</span></span>

- <span data-ttu-id="e04c2-122">Czy plik jest opcjonalny</span><span class="sxs-lookup"><span data-stu-id="e04c2-122">Whether the file is optional</span></span>
- <span data-ttu-id="e04c2-123">Czy konfiguracja zostanie ponownie załadowana w przypadku zmiany pliku</span><span class="sxs-lookup"><span data-stu-id="e04c2-123">Whether the configuration is reloaded if the file changes</span></span>

<span data-ttu-id="e04c2-124">Spójrzmy na poniższy kod:</span><span class="sxs-lookup"><span data-stu-id="e04c2-124">Consider the following code:</span></span>

:::code language="csharp" source="snippets/configuration/console-json/Program.cs" range="1-39,43-44" highlight="23-29":::

<span data-ttu-id="e04c2-125">Powyższy kod ma następujące działanie:</span><span class="sxs-lookup"><span data-stu-id="e04c2-125">The preceding code:</span></span>

- <span data-ttu-id="e04c2-126">Czyści wszystkich istniejących dostawców konfiguracji, którzy zostali dodani domyślnie w <xref:Microsoft.Extensions.Hosting.Host.CreateDefaultBuilder(System.String[])> metodzie.</span><span class="sxs-lookup"><span data-stu-id="e04c2-126">Clears all existing configuration providers that were added by default in the <xref:Microsoft.Extensions.Hosting.Host.CreateDefaultBuilder(System.String[])> method.</span></span>
- <span data-ttu-id="e04c2-127">Konfiguruje dostawcę konfiguracji JSON w celu załadowania *appsettings.jsw* i  *AppSettings* `Environment` . pliki *JSON* z następującymi opcjami:</span><span class="sxs-lookup"><span data-stu-id="e04c2-127">Configures the JSON configuration provider to load the *appsettings.json* and  *appsettings*.`Environment`.*json* files with the following options:</span></span>
  - <span data-ttu-id="e04c2-128">`optional: true`: Plik jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="e04c2-128">`optional: true`: The file is optional.</span></span>
  - <span data-ttu-id="e04c2-129">`reloadOnChange: true` : Plik zostanie ponownie załadowany podczas zapisywania zmian.</span><span class="sxs-lookup"><span data-stu-id="e04c2-129">`reloadOnChange: true` : The file is reloaded when changes are saved.</span></span>

<span data-ttu-id="e04c2-130">Ustawienia JSON są zastępowane przez ustawienia w obszarze [dostawca konfiguracji zmiennych środowiskowych](#environment-variable-configuration-provider) i [dostawca konfiguracji wiersza polecenia](#command-line-configuration-provider).</span><span class="sxs-lookup"><span data-stu-id="e04c2-130">The JSON settings are overridden by settings in the [Environment variables configuration provider](#environment-variable-configuration-provider) and the [Command-line configuration provider](#command-line-configuration-provider).</span></span>

<span data-ttu-id="e04c2-131">Przykład *appsettings.jsw* pliku z różnymi ustawieniami konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="e04c2-131">An example *appsettings.json* file with various configuration settings follows:</span></span>

:::code language="json" source="snippets/configuration/console-json/appsettings.json":::

<span data-ttu-id="e04c2-132">Z tego <xref:Microsoft.Extensions.Configuration.IConfigurationBuilder> wystąpienia po dodaniu dostawców konfiguracji można wywołać, <xref:Microsoft.Extensions.Configuration.IConfigurationBuilder.Build?displayProperty=nameWithType> Aby uzyskać <xref:Microsoft.Extensions.Configuration.IConfigurationRoot> obiekt.</span><span class="sxs-lookup"><span data-stu-id="e04c2-132">From the <xref:Microsoft.Extensions.Configuration.IConfigurationBuilder> instance, after configuration providers have been added you can call <xref:Microsoft.Extensions.Configuration.IConfigurationBuilder.Build?displayProperty=nameWithType> to get the <xref:Microsoft.Extensions.Configuration.IConfigurationRoot> object.</span></span> <span data-ttu-id="e04c2-133">Katalog główny konfiguracji reprezentuje element główny hierarchii konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="e04c2-133">The configuration root represents the root of a configuration hierarchy.</span></span> <span data-ttu-id="e04c2-134">Sekcje z konfiguracji można powiązać z wystąpieniami obiektów .NET i w późniejszym czasie <xref:Microsoft.Extensions.Options.IOptions%601> za pośrednictwem iniekcji zależności.</span><span class="sxs-lookup"><span data-stu-id="e04c2-134">Sections from the configuration can be bound to instances of .NET objects, and later provided as <xref:Microsoft.Extensions.Options.IOptions%601> through dependency injection.</span></span>

<span data-ttu-id="e04c2-135">Należy wziąć pod uwagę `TransientFaultHandlingOptions` Typ rekordu zdefiniowany w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="e04c2-135">Consider the `TransientFaultHandlingOptions` record type defined as follows:</span></span>

:::code language="csharp" source="snippets/configuration/console-json/TransientFaultHandlingOptions.cs":::

<span data-ttu-id="e04c2-136">Aby uzyskać informacje na temat typów rekordów, zobacz [typy rekordów w języku C# 9](../../csharp/whats-new/csharp-9.md#record-types).</span><span class="sxs-lookup"><span data-stu-id="e04c2-136">For information on record types, see [Record types in C# 9](../../csharp/whats-new/csharp-9.md#record-types).</span></span>

<span data-ttu-id="e04c2-137">Poniższy kod kompiluje katalog główny konfiguracji, tworzy powiązanie sekcji z `TransientFaultHandlingOptions` typem rekordu i drukuje powiązane wartości do okna konsoli:</span><span class="sxs-lookup"><span data-stu-id="e04c2-137">The following code builds the configuration root, binds a section to the `TransientFaultHandlingOptions` record type, and prints the bound values to the console window:</span></span>

:::code language="csharp" source="snippets/configuration/console-json/Program.cs" range="31-38":::

<span data-ttu-id="e04c2-138">Aplikacja zapisze następujące przykładowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="e04c2-138">The application would write the following sample output:</span></span>

:::code language="csharp" source="snippets/configuration/console-json/Program.cs" range="40-42":::

### <a name="xml-configuration-provider"></a><span data-ttu-id="e04c2-139">Dostawca konfiguracji XML</span><span class="sxs-lookup"><span data-stu-id="e04c2-139">XML configuration provider</span></span>

<span data-ttu-id="e04c2-140"><xref:Microsoft.Extensions.Configuration.Xml.XmlConfigurationProvider>Klasa ładuje konfigurację z pliku XML w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="e04c2-140">The <xref:Microsoft.Extensions.Configuration.Xml.XmlConfigurationProvider> class loads configuration from an XML file at runtime.</span></span> <span data-ttu-id="e04c2-141">Zainstaluj [`Microsoft.Extensions.Configuration.Xml`](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.Xml) pakiet NuGet.</span><span class="sxs-lookup"><span data-stu-id="e04c2-141">Install the [`Microsoft.Extensions.Configuration.Xml`](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.Xml) NuGet package.</span></span>

<span data-ttu-id="e04c2-142">Poniższy kod ilustruje konfigurację plików XML przy użyciu dostawcy konfiguracji XML.</span><span class="sxs-lookup"><span data-stu-id="e04c2-142">The following code demonstrates configuration of XML files using the XML configuration provider.</span></span>

:::code language="csharp" source="snippets/configuration/console-xml/Program.cs" range="1-34,52,58-59" highlight="23-34":::

<span data-ttu-id="e04c2-143">Powyższy kod ma następujące działanie:</span><span class="sxs-lookup"><span data-stu-id="e04c2-143">The preceding code:</span></span>

- <span data-ttu-id="e04c2-144">Czyści wszystkich istniejących dostawców konfiguracji, którzy zostali dodani domyślnie w <xref:Microsoft.Extensions.Hosting.Host.CreateDefaultBuilder(System.String[])> metodzie.</span><span class="sxs-lookup"><span data-stu-id="e04c2-144">Clears all existing configuration providers that were added by default in the <xref:Microsoft.Extensions.Hosting.Host.CreateDefaultBuilder(System.String[])> method.</span></span>
- <span data-ttu-id="e04c2-145">Konfiguruje dostawcę konfiguracji XML do ładowania *appsettings.xml* i *repeating-example.xml* plików z następującymi opcjami:</span><span class="sxs-lookup"><span data-stu-id="e04c2-145">Configures the XML configuration provider to load the *appsettings.xml* and *repeating-example.xml* files with the following options:</span></span>
  - <span data-ttu-id="e04c2-146">`optional: true`: Plik jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="e04c2-146">`optional: true`: The file is optional.</span></span>
  - <span data-ttu-id="e04c2-147">`reloadOnChange: true` : Plik zostanie ponownie załadowany podczas zapisywania zmian.</span><span class="sxs-lookup"><span data-stu-id="e04c2-147">`reloadOnChange: true` : The file is reloaded when changes are saved.</span></span>
- <span data-ttu-id="e04c2-148">Konfiguruje dostawcę konfiguracji zmiennych środowiskowych.</span><span class="sxs-lookup"><span data-stu-id="e04c2-148">Configures the environment variables configuration provider.</span></span>
- <span data-ttu-id="e04c2-149">Konfiguruje dostawcę konfiguracji wiersza polecenia, jeśli podano `args` argumenty.</span><span class="sxs-lookup"><span data-stu-id="e04c2-149">Configures the command-line configuration provider if the given `args` contains arguments.</span></span>

<span data-ttu-id="e04c2-150">Ustawienia XML są zastępowane przez ustawienia w obszarze [dostawca konfiguracji zmiennych środowiskowych](#environment-variable-configuration-provider) i [dostawca konfiguracji wiersza polecenia](#command-line-configuration-provider).</span><span class="sxs-lookup"><span data-stu-id="e04c2-150">The XML settings are overridden by settings in the [Environment variables configuration provider](#environment-variable-configuration-provider) and the [Command-line configuration provider](#command-line-configuration-provider).</span></span>

<span data-ttu-id="e04c2-151">Przykładowy plik *appsettings.xml* z różnymi ustawieniami konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="e04c2-151">An example *appsettings.xml* file with various configuration settings follows:</span></span>

:::code language="xml" source="snippets/configuration/console-xml/appsettings.xml":::

<span data-ttu-id="e04c2-152">Powtarzające się elementy, które używają tej samej nazwy elementu, działają, jeśli `name` atrybut jest używany do odróżnienia elementów:</span><span class="sxs-lookup"><span data-stu-id="e04c2-152">Repeating elements that use the same element name work if the `name` attribute is used to distinguish the elements:</span></span>

:::code language="xml" source="snippets/configuration/console-xml/repeating-example.xml":::

<span data-ttu-id="e04c2-153">Poniższy kod odczytuje poprzedni plik konfiguracji i wyświetla klucze i wartości:</span><span class="sxs-lookup"><span data-stu-id="e04c2-153">The following code reads the previous configuration file and displays the keys and values:</span></span>

:::code language="csharp" source="snippets/configuration/console-xml/Program.cs" range="36-51":::

<span data-ttu-id="e04c2-154">Aplikacja zapisze następujące przykładowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="e04c2-154">The application would write the following sample output:</span></span>

:::code language="csharp" source="snippets/configuration/console-xml/Program.cs" range="53-57":::

<span data-ttu-id="e04c2-155">Atrybuty mogą służyć do dostarczania wartości:</span><span class="sxs-lookup"><span data-stu-id="e04c2-155">Attributes can be used to supply values:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <key attribute="value" />
  <section>
    <key attribute="value" />
  </section>
</configuration>
```

<span data-ttu-id="e04c2-156">Poprzedni plik konfiguracji ładuje następujące klucze z `value` :</span><span class="sxs-lookup"><span data-stu-id="e04c2-156">The previous configuration file loads the following keys with `value`:</span></span>

- `key:attribute`
- `section:key:attribute`

### <a name="ini-configuration-provider"></a><span data-ttu-id="e04c2-157">Dostawca konfiguracji pliku INI</span><span class="sxs-lookup"><span data-stu-id="e04c2-157">INI configuration provider</span></span>

<span data-ttu-id="e04c2-158"><xref:Microsoft.Extensions.Configuration.Ini.IniConfigurationProvider>Klasa ładuje konfigurację z pliku ini w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="e04c2-158">The <xref:Microsoft.Extensions.Configuration.Ini.IniConfigurationProvider> class loads configuration from an INI file at runtime.</span></span> <span data-ttu-id="e04c2-159">Zainstaluj [`Microsoft.Extensions.Configuration.Ini`](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.Ini)  pakiet NuGet.</span><span class="sxs-lookup"><span data-stu-id="e04c2-159">Install the [`Microsoft.Extensions.Configuration.Ini`](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.Ini)  NuGet package.</span></span>

<span data-ttu-id="e04c2-160">Poniższy kod czyści wszystkich dostawców konfiguracji i dodaje `IniConfigurationProvider` dwa pliki ini jako Źródło:</span><span class="sxs-lookup"><span data-stu-id="e04c2-160">The following code clears all the configuration providers and adds the `IniConfigurationProvider` with two INI files as the source:</span></span>

:::code language="csharp" source="snippets/configuration/console-ini/Program.cs" range="1-37,44-45" highlight="24-30":::

<span data-ttu-id="e04c2-161">Przykładowy plik *appsettings.ini* z różnymi ustawieniami konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="e04c2-161">An example *appsettings.ini* file with various configuration settings follows:</span></span>

:::code language="ini" source="snippets/configuration/console-ini/appsettings.ini":::

<span data-ttu-id="e04c2-162">Poniższy kod wyświetla poprzednie ustawienia konfiguracji, pisząc je w oknie konsoli:</span><span class="sxs-lookup"><span data-stu-id="e04c2-162">The following code displays the preceding configuration settings by writing them to the console window:</span></span>

:::code language="csharp" source="snippets/configuration/console-ini/Program.cs" range="32-36":::

<span data-ttu-id="e04c2-163">Aplikacja zapisze następujące przykładowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="e04c2-163">The application would write the following sample output:</span></span>

:::code language="csharp" source="snippets/configuration/console-ini/Program.cs" range="38-43":::

## <a name="environment-variable-configuration-provider"></a><span data-ttu-id="e04c2-164">Dostawca konfiguracji zmiennej środowiskowej</span><span class="sxs-lookup"><span data-stu-id="e04c2-164">Environment variable configuration provider</span></span>

<span data-ttu-id="e04c2-165">Przy użyciu konfiguracji domyślnej, <xref:Microsoft.Extensions.Configuration.EnvironmentVariables.EnvironmentVariablesConfigurationProvider> Ładowanie konfiguracji ze zmiennej środowiskowej par klucz-wartość po czytaniu *appsettings.jsw*, *appSettings.* `Environment` *. JSON* i Menedżer wpisów tajnych.</span><span class="sxs-lookup"><span data-stu-id="e04c2-165">Using the default configuration, the <xref:Microsoft.Extensions.Configuration.EnvironmentVariables.EnvironmentVariablesConfigurationProvider> loads configuration from environment variable key-value pairs after reading *appsettings.json*, *appsettings.*`Environment`*.json*, and Secret manager.</span></span> <span data-ttu-id="e04c2-166">W związku z tym kluczowe wartości są odczytywane z wartości zastąpienia środowiska odczytywane z *appsettings.jsw*, *appSettings.* `Environment` *. JSON* i Menedżer wpisów tajnych.</span><span class="sxs-lookup"><span data-stu-id="e04c2-166">Therefore, key values read from the environment override values read from *appsettings.json*, *appsettings.*`Environment`*.json*, and Secret manager.</span></span>

<span data-ttu-id="e04c2-167">`:`Separator nie działa ze zmiennymi kluczy hierarchicznych na wszystkich platformach.</span><span class="sxs-lookup"><span data-stu-id="e04c2-167">The `:` separator doesn't work with environment variable hierarchical keys on all platforms.</span></span> <span data-ttu-id="e04c2-168">Podwójne podkreślenie ( `__` ) jest automatycznie zastępowane przez `:` i jest obsługiwane przez wszystkie platformy.</span><span class="sxs-lookup"><span data-stu-id="e04c2-168">The double underscore (`__`) is automatically replaced by a `:` and is supported by all platforms.</span></span> <span data-ttu-id="e04c2-169">Na przykład `:` separator nie jest obsługiwany przez [bash](https://linuxhint.com/bash-environment-variables), ale `__` jest.</span><span class="sxs-lookup"><span data-stu-id="e04c2-169">For example, the `:` separator is not supported by [Bash](https://linuxhint.com/bash-environment-variables), but `__` is.</span></span>

<span data-ttu-id="e04c2-170">Następujące `set` polecenia:</span><span class="sxs-lookup"><span data-stu-id="e04c2-170">The following `set` commands:</span></span>

- <span data-ttu-id="e04c2-171">Ustaw klucze środowiska i wartości z poprzedniego przykładu w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="e04c2-171">Set the environment keys and values of the preceding example on Windows.</span></span>
- <span data-ttu-id="e04c2-172">Przetestuj ustawienia, zmieniając ich wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="e04c2-172">Test the settings by changing them from their default values.</span></span> <span data-ttu-id="e04c2-173">`dotnet run`Polecenie musi być uruchamiane w katalogu projektu.</span><span class="sxs-lookup"><span data-stu-id="e04c2-173">The `dotnet run` command must be run in the project directory.</span></span>

```dotnetcli
set SecretKey="Secret key from environment"
set TransientFaultHandlingOptions__Enabled="true"
set TransientFaultHandlingOptions__AutoRetryDelay="00:00:13"

dotnet run
```

<span data-ttu-id="e04c2-174">Poprzednie ustawienia środowiska:</span><span class="sxs-lookup"><span data-stu-id="e04c2-174">The preceding environment settings:</span></span>

- <span data-ttu-id="e04c2-175">Są ustawiane tylko w ramach procesów uruchomionych z poziomu okna polecenia, które zostały ustawione w.</span><span class="sxs-lookup"><span data-stu-id="e04c2-175">Are only set in processes launched from the command window they were set in.</span></span>
- <span data-ttu-id="e04c2-176">Nie będą odczytywane przez aplikacje sieci Web uruchomione przy użyciu programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e04c2-176">Won't be read by web apps launched with Visual Studio.</span></span>

<span data-ttu-id="e04c2-177">Następujące polecenia [setx](/windows-server/administration/windows-commands/setx) mogą służyć do ustawiania kluczy środowiskowych i wartości w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="e04c2-177">The following [setx](/windows-server/administration/windows-commands/setx) commands can be used to set the environment keys and values on Windows.</span></span> <span data-ttu-id="e04c2-178">W przeciwieństwie do `set` , `setx` Ustawienia są utrwalane.</span><span class="sxs-lookup"><span data-stu-id="e04c2-178">Unlike `set`, `setx` settings are persisted.</span></span> <span data-ttu-id="e04c2-179">`/M` ustawia zmienną w środowisku systemowym.</span><span class="sxs-lookup"><span data-stu-id="e04c2-179">`/M` sets the variable in the system environment.</span></span> <span data-ttu-id="e04c2-180">Jeśli `/M` przełącznik nie jest używany, zmienna środowiskowa użytkownika jest ustawiona.</span><span class="sxs-lookup"><span data-stu-id="e04c2-180">If the `/M` switch isn't used, a user environment variable is set.</span></span>

```dotnetcli
setx SecretKey "Secret key from setx environment" /M
setx TransientFaultHandlingOptions__Enabled "true" /M
setx TransientFaultHandlingOptions__AutoRetryDelay "00:00:05" /M

dotnet run
```

<span data-ttu-id="e04c2-181">Aby sprawdzić, czy poprzednie polecenia zastępują *appsettings.js* i *appSettings.* `Environment` *. JSON*:</span><span class="sxs-lookup"><span data-stu-id="e04c2-181">To test that the preceding commands override *appsettings.json* and *appsettings.*`Environment`*.json*:</span></span>

- <span data-ttu-id="e04c2-182">Za pomocą programu Visual Studio: Zamknij i uruchom ponownie program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e04c2-182">With Visual Studio: Exit and restart Visual Studio.</span></span>
- <span data-ttu-id="e04c2-183">Za pomocą interfejsu wiersza polecenia: Uruchom nowe okno poleceń i wprowadź `dotnet run` .</span><span class="sxs-lookup"><span data-stu-id="e04c2-183">With the CLI: Start a new command window and enter `dotnet run`.</span></span>

<span data-ttu-id="e04c2-184">Połącz <xref:Microsoft.Extensions.Configuration.EnvironmentVariablesExtensions.AddEnvironmentVariables%2A> z ciągiem, aby określić prefiks dla zmiennych środowiskowych:</span><span class="sxs-lookup"><span data-stu-id="e04c2-184">Call <xref:Microsoft.Extensions.Configuration.EnvironmentVariablesExtensions.AddEnvironmentVariables%2A> with a string to specify a prefix for environment variables:</span></span>

:::code language="csharp" source="snippets/configuration/console-env/Program.cs" highlight="21-22":::

<span data-ttu-id="e04c2-185">Powyższy kod ma następujące działanie:</span><span class="sxs-lookup"><span data-stu-id="e04c2-185">In the preceding code:</span></span>

- <span data-ttu-id="e04c2-186">`config.AddEnvironmentVariables(prefix: "CustomPrefix_")` zostanie dodany po domyślnych dostawcach konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="e04c2-186">`config.AddEnvironmentVariables(prefix: "CustomPrefix_")` is added after the default configuration providers.</span></span> <span data-ttu-id="e04c2-187">Przykład określania kolejności dostawców konfiguracji można znaleźć w temacie [dostawca konfiguracji XML](#xml-configuration-provider).</span><span class="sxs-lookup"><span data-stu-id="e04c2-187">For an example of ordering the configuration providers, see [XML configuration provider](#xml-configuration-provider).</span></span>
- <span data-ttu-id="e04c2-188">Zmienne środowiskowe ustawione z `CustomPrefix_` prefiksem przesłaniają domyślnych dostawców konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="e04c2-188">Environment variables set with the `CustomPrefix_` prefix override the default configuration providers.</span></span> <span data-ttu-id="e04c2-189">Obejmuje to zmienne środowiskowe bez prefiksu.</span><span class="sxs-lookup"><span data-stu-id="e04c2-189">This includes environment variables without the prefix.</span></span>

<span data-ttu-id="e04c2-190">Prefiks jest usuwany, gdy pary klucz konfiguracji-wartość są odczytywane.</span><span class="sxs-lookup"><span data-stu-id="e04c2-190">The prefix is stripped off when the configuration key-value pairs are read.</span></span>

<span data-ttu-id="e04c2-191">Następujące polecenia testują prefiks niestandardowy:</span><span class="sxs-lookup"><span data-stu-id="e04c2-191">The following commands test the custom prefix:</span></span>

```dotnetcli
set CustomPrefix__SecretKey="Secret key with CustomPrefix_ environment"
set CustomPrefix_TransientFaultHandlingOptions__Enabled=true
set CustomPrefix_TransientFaultHandlingOptions__AutoRetryDelay=00:00:21

dotnet run
```

<span data-ttu-id="e04c2-192">Konfiguracja domyślna ładuje zmienne środowiskowe i argumenty wiersza polecenia poprzedzone prefiksem `DOTNET_` .</span><span class="sxs-lookup"><span data-stu-id="e04c2-192">The default configuration loads environment variables and command-line arguments prefixed with `DOTNET_`.</span></span> <span data-ttu-id="e04c2-193">`DOTNET_`Prefiks jest używany przez platformę .NET do [konfiguracji](generic-host.md#app-configuration) [hosta](generic-host.md#host-configuration) i aplikacji, ale nie do konfiguracji użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e04c2-193">The `DOTNET_` prefix is used by .NET for [host](generic-host.md#host-configuration) and [app configuration](generic-host.md#app-configuration), but not for user configuration.</span></span>

<span data-ttu-id="e04c2-194">Aby uzyskać więcej informacji na temat konfiguracji hosta i aplikacji, zobacz [host ogólny programu .NET](generic-host.md).</span><span class="sxs-lookup"><span data-stu-id="e04c2-194">For more information on host and app configuration, see [.NET Generic Host](generic-host.md).</span></span>

<span data-ttu-id="e04c2-195">Na [Azure App Service](https://azure.microsoft.com/services/app-service)wybierz pozycję **nowe ustawienie aplikacji** na stronie **Konfiguracja > ustawienia** .</span><span class="sxs-lookup"><span data-stu-id="e04c2-195">On [Azure App Service](https://azure.microsoft.com/services/app-service), select **New application setting** on the **Settings > Configuration** page.</span></span> <span data-ttu-id="e04c2-196">Ustawienia aplikacji Azure App Service są następujące:</span><span class="sxs-lookup"><span data-stu-id="e04c2-196">Azure App Service application settings are:</span></span>

- <span data-ttu-id="e04c2-197">Szyfrowane i przesyłane przez zaszyfrowanego kanału.</span><span class="sxs-lookup"><span data-stu-id="e04c2-197">Encrypted at rest and transmitted over an encrypted channel.</span></span>
- <span data-ttu-id="e04c2-198">Uwidocznione jako zmienne środowiskowe.</span><span class="sxs-lookup"><span data-stu-id="e04c2-198">Exposed as environment variables.</span></span>

### <a name="connection-string-prefixes"></a><span data-ttu-id="e04c2-199">Prefiksy parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="e04c2-199">Connection string prefixes</span></span>

<span data-ttu-id="e04c2-200">Interfejs API konfiguracji ma specjalne reguły przetwarzania dla czterech zmiennych środowiskowych parametrów połączenia.</span><span class="sxs-lookup"><span data-stu-id="e04c2-200">The Configuration API has special processing rules for four connection string environment variables.</span></span> <span data-ttu-id="e04c2-201">Te parametry połączenia są związane z konfigurowaniem parametrów połączenia platformy Azure dla środowiska aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e04c2-201">These connection strings are involved in configuring Azure connection strings for the app environment.</span></span> <span data-ttu-id="e04c2-202">Zmienne środowiskowe z prefiksami podanymi w tabeli są ładowane do aplikacji z konfiguracją domyślną lub gdy nie podano prefiksu `AddEnvironmentVariables` .</span><span class="sxs-lookup"><span data-stu-id="e04c2-202">Environment variables with the prefixes shown in the table are loaded into the app with the default configuration or when no prefix is supplied to `AddEnvironmentVariables`.</span></span>

| <span data-ttu-id="e04c2-203">Prefiks parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="e04c2-203">Connection string prefix</span></span> | <span data-ttu-id="e04c2-204">Dostawca</span><span class="sxs-lookup"><span data-stu-id="e04c2-204">Provider</span></span>                                                                |
|--------------------------|-------------------------------------------------------------------------|
| `CUSTOMCONNSTR_`         | <span data-ttu-id="e04c2-205">Dostawca niestandardowy</span><span class="sxs-lookup"><span data-stu-id="e04c2-205">Custom provider</span></span>                                                         |
| `MYSQLCONNSTR_`          | [<span data-ttu-id="e04c2-206">MySQL</span><span class="sxs-lookup"><span data-stu-id="e04c2-206">MySQL</span></span>](https://www.mysql.com)                                          |
| `SQLAZURECONNSTR_`       | [<span data-ttu-id="e04c2-207">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="e04c2-207">Azure SQL Database</span></span>](https://azure.microsoft.com/services/sql-database) |
| `SQLCONNSTR_`            | [<span data-ttu-id="e04c2-208">SQL Server</span><span class="sxs-lookup"><span data-stu-id="e04c2-208">SQL Server</span></span>](https://www.microsoft.com/sql-server)                      |

<span data-ttu-id="e04c2-209">Gdy zmienna środowiskowa zostanie odnaleziona i załadowana do konfiguracji z dowolnymi z czterech prefiksów pokazanych w tabeli:</span><span class="sxs-lookup"><span data-stu-id="e04c2-209">When an environment variable is discovered and loaded into configuration with any of the four prefixes shown in the table:</span></span>

- <span data-ttu-id="e04c2-210">Klucz konfiguracji jest tworzony przez usunięcie prefiksu zmiennej środowiskowej i dodanie sekcji klucza konfiguracji ( `ConnectionStrings` ).</span><span class="sxs-lookup"><span data-stu-id="e04c2-210">The configuration key is created by removing the environment variable prefix and adding a configuration key section (`ConnectionStrings`).</span></span>
- <span data-ttu-id="e04c2-211">Zostanie utworzona nowa para klucz-wartość konfiguracji, która reprezentuje dostawcę połączenia bazy danych (z wyjątkiem tego `CUSTOMCONNSTR_` , który nie ma określonego dostawcy).</span><span class="sxs-lookup"><span data-stu-id="e04c2-211">A new configuration key-value pair is created that represents the database connection provider (except for `CUSTOMCONNSTR_`, which has no stated provider).</span></span>

| <span data-ttu-id="e04c2-212">Klucz zmiennej środowiskowej</span><span class="sxs-lookup"><span data-stu-id="e04c2-212">Environment variable key</span></span> | <span data-ttu-id="e04c2-213">Przekonwertowany klucz konfiguracji</span><span class="sxs-lookup"><span data-stu-id="e04c2-213">Converted configuration key</span></span> | <span data-ttu-id="e04c2-214">Wpis konfiguracji dostawcy</span><span class="sxs-lookup"><span data-stu-id="e04c2-214">Provider configuration entry</span></span>                                                    |
|--------------------------|-----------------------------|---------------------------------------------------------------------------------|
| `CUSTOMCONNSTR_{KEY}`    | `ConnectionStrings:{KEY}`   | <span data-ttu-id="e04c2-215">Wpis konfiguracji nie został utworzony.</span><span class="sxs-lookup"><span data-stu-id="e04c2-215">Configuration entry not created.</span></span>                                                |
| `MYSQLCONNSTR_{KEY}`     | `ConnectionStrings:{KEY}`   | <span data-ttu-id="e04c2-216">Klucz: `ConnectionStrings:{KEY}_ProviderName` :</span><span class="sxs-lookup"><span data-stu-id="e04c2-216">Key: `ConnectionStrings:{KEY}_ProviderName`:</span></span><br><span data-ttu-id="e04c2-217">Wartość: `MySql.Data.MySqlClient`</span><span class="sxs-lookup"><span data-stu-id="e04c2-217">Value: `MySql.Data.MySqlClient`</span></span> |
| `SQLAZURECONNSTR_{KEY}`  | `ConnectionStrings:{KEY}`   | <span data-ttu-id="e04c2-218">Klucz: `ConnectionStrings:{KEY}_ProviderName` :</span><span class="sxs-lookup"><span data-stu-id="e04c2-218">Key: `ConnectionStrings:{KEY}_ProviderName`:</span></span><br><span data-ttu-id="e04c2-219">Wartość: `System.Data.SqlClient`</span><span class="sxs-lookup"><span data-stu-id="e04c2-219">Value: `System.Data.SqlClient`</span></span>  |
| `SQLCONNSTR_{KEY}`       | `ConnectionStrings:{KEY}`   | <span data-ttu-id="e04c2-220">Klucz: `ConnectionStrings:{KEY}_ProviderName` :</span><span class="sxs-lookup"><span data-stu-id="e04c2-220">Key: `ConnectionStrings:{KEY}_ProviderName`:</span></span><br><span data-ttu-id="e04c2-221">Wartość: `System.Data.SqlClient`</span><span class="sxs-lookup"><span data-stu-id="e04c2-221">Value: `System.Data.SqlClient`</span></span>  |

### <a name="environment-variables-set-in-launchsettingsjson"></a><span data-ttu-id="e04c2-222">Zmienne środowiskowe ustawione w launchSettings.jsna</span><span class="sxs-lookup"><span data-stu-id="e04c2-222">Environment variables set in launchSettings.json</span></span>

<span data-ttu-id="e04c2-223">Zmienne środowiskowe ustawione w *launchSettings.jsna* zastępują te ustawienia w środowisku systemowym.</span><span class="sxs-lookup"><span data-stu-id="e04c2-223">Environment variables set in *launchSettings.json* override those set in the system environment.</span></span>

## <a name="command-line-configuration-provider"></a><span data-ttu-id="e04c2-224">Dostawca konfiguracji wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="e04c2-224">Command-line configuration provider</span></span>

<span data-ttu-id="e04c2-225">Korzystając z konfiguracji domyślnej, <xref:Microsoft.Extensions.Configuration.CommandLine.CommandLineConfigurationProvider> ładuje konfigurację z par klucz-wartość argumentu wiersza polecenia po następujących źródłach konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="e04c2-225">Using the default configuration, the <xref:Microsoft.Extensions.Configuration.CommandLine.CommandLineConfigurationProvider> loads configuration from command-line argument key-value pairs after the following configuration sources:</span></span>

- <span data-ttu-id="e04c2-226">*appsettings.jsna* i *AppSettings*. `Environment` . pliki *JSON* .</span><span class="sxs-lookup"><span data-stu-id="e04c2-226">*appsettings.json* and *appsettings*.`Environment`.*json* files.</span></span>
- <span data-ttu-id="e04c2-227">Wpisy tajne aplikacji (Secret Manager) w `Development` środowisku.</span><span class="sxs-lookup"><span data-stu-id="e04c2-227">App secrets (Secret Manager) in the `Development` environment.</span></span>
- <span data-ttu-id="e04c2-228">Zmienne środowiskowe.</span><span class="sxs-lookup"><span data-stu-id="e04c2-228">Environment variables.</span></span>

<span data-ttu-id="e04c2-229">Domyślnie wartości konfiguracyjne ustawione w wierszu polecenia przesłaniają wartości konfiguracyjne ustawione dla wszystkich innych dostawców konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="e04c2-229">By default, configuration values set on the command line override configuration values set with all the other configuration providers.</span></span>

### <a name="command-line-arguments"></a><span data-ttu-id="e04c2-230">Argumenty wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="e04c2-230">Command-line arguments</span></span>

<span data-ttu-id="e04c2-231">Następujące polecenie ustawia klucze i wartości przy użyciu `=` :</span><span class="sxs-lookup"><span data-stu-id="e04c2-231">The following command sets keys and values using `=`:</span></span>

```dotnetcli
dotnet run SecretKey="Secret key from command line"
```

<span data-ttu-id="e04c2-232">Następujące polecenie ustawia klucze i wartości przy użyciu `/` :</span><span class="sxs-lookup"><span data-stu-id="e04c2-232">The following command sets keys and values using `/`:</span></span>

```dotnetcli
dotnet run /SecretKey "Secret key set from forward slash"
```

<span data-ttu-id="e04c2-233">Następujące polecenie ustawia klucze i wartości przy użyciu `--` :</span><span class="sxs-lookup"><span data-stu-id="e04c2-233">The following command sets keys and values using `--`:</span></span>

```dotnetcli
dotnet run --SecretKey "Secret key set from double hyphen"
```

<span data-ttu-id="e04c2-234">Wartość klucza:</span><span class="sxs-lookup"><span data-stu-id="e04c2-234">The key value:</span></span>

- <span data-ttu-id="e04c2-235">Musi `=` być zgodna lub musi mieć prefiks lub, gdy wartość znajduje się w `--` `/` miejscu.</span><span class="sxs-lookup"><span data-stu-id="e04c2-235">Must follow `=`, or the key must have a prefix of `--` or `/` when the value follows a space.</span></span>
- <span data-ttu-id="e04c2-236">Nie jest wymagane, jeśli `=` jest używany.</span><span class="sxs-lookup"><span data-stu-id="e04c2-236">Isn't required if `=` is used.</span></span> <span data-ttu-id="e04c2-237">Na przykład `SomeKey=`.</span><span class="sxs-lookup"><span data-stu-id="e04c2-237">For example, `SomeKey=`.</span></span>

<span data-ttu-id="e04c2-238">W tym samym poleceniu nie należy mieszać par klucz-wartość argumentu wiersza polecenia, które są używane `=` z parami klucz-wartość, które używają spacji.</span><span class="sxs-lookup"><span data-stu-id="e04c2-238">Within the same command, don't mix command-line argument key-value pairs that use `=` with key-value pairs that use a space.</span></span>

## <a name="key-per-file-configuration-provider"></a><span data-ttu-id="e04c2-239">Dostawca konfiguracji klucza dla plików</span><span class="sxs-lookup"><span data-stu-id="e04c2-239">Key-per-file configuration provider</span></span>

<span data-ttu-id="e04c2-240"><xref:Microsoft.Extensions.Configuration.KeyPerFile.KeyPerFileConfigurationProvider>Używa plików katalogu jako par klucz konfiguracji i wartość.</span><span class="sxs-lookup"><span data-stu-id="e04c2-240">The <xref:Microsoft.Extensions.Configuration.KeyPerFile.KeyPerFileConfigurationProvider> uses a directory's files as configuration key-value pairs.</span></span> <span data-ttu-id="e04c2-241">Kluczem jest nazwa pliku.</span><span class="sxs-lookup"><span data-stu-id="e04c2-241">The key is the file name.</span></span> <span data-ttu-id="e04c2-242">Wartość jest zawartością pliku.</span><span class="sxs-lookup"><span data-stu-id="e04c2-242">The value is the file's contents.</span></span> <span data-ttu-id="e04c2-243">Dostawca konfiguracji klucza dla plików jest używany w scenariuszach hostingu platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="e04c2-243">The Key-per-file configuration provider is used in Docker hosting scenarios.</span></span>

<span data-ttu-id="e04c2-244">Aby uaktywnić konfigurację klucza dla plików, wywołaj <xref:Microsoft.Extensions.Configuration.KeyPerFileConfigurationBuilderExtensions.AddKeyPerFile%2A> metodę rozszerzenia w wystąpieniu <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder> .</span><span class="sxs-lookup"><span data-stu-id="e04c2-244">To activate key-per-file configuration, call the <xref:Microsoft.Extensions.Configuration.KeyPerFileConfigurationBuilderExtensions.AddKeyPerFile%2A> extension method on an instance of <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder>.</span></span> <span data-ttu-id="e04c2-245">`directoryPath`Do plików musi być ścieżką bezwzględną.</span><span class="sxs-lookup"><span data-stu-id="e04c2-245">The `directoryPath` to the files must be an absolute path.</span></span>

<span data-ttu-id="e04c2-246">Przeciążania Zezwalaj na określanie:</span><span class="sxs-lookup"><span data-stu-id="e04c2-246">Overloads permit specifying:</span></span>

- <span data-ttu-id="e04c2-247">`Action<KeyPerFileConfigurationSource>`Delegat, który konfiguruje źródło.</span><span class="sxs-lookup"><span data-stu-id="e04c2-247">An `Action<KeyPerFileConfigurationSource>` delegate that configures the source.</span></span>
- <span data-ttu-id="e04c2-248">Określa, czy katalog jest opcjonalny, i ścieżkę do katalogu.</span><span class="sxs-lookup"><span data-stu-id="e04c2-248">Whether the directory is optional and the path to the directory.</span></span>

<span data-ttu-id="e04c2-249">Podwójny znak podkreślenia ( `__` ) jest używany jako ogranicznik klucza konfiguracji w nazwach plików.</span><span class="sxs-lookup"><span data-stu-id="e04c2-249">The double-underscore (`__`) is used as a configuration key delimiter in file names.</span></span> <span data-ttu-id="e04c2-250">Na przykład nazwa pliku `Logging__LogLevel__System` generuje klucz konfiguracji `Logging:LogLevel:System` .</span><span class="sxs-lookup"><span data-stu-id="e04c2-250">For example, the file name `Logging__LogLevel__System` produces the configuration key `Logging:LogLevel:System`.</span></span>

<span data-ttu-id="e04c2-251">Wywołaj `ConfigureAppConfiguration` podczas kompilowania hosta, aby określić konfigurację aplikacji:</span><span class="sxs-lookup"><span data-stu-id="e04c2-251">Call `ConfigureAppConfiguration` when building the host to specify the app's configuration:</span></span>

```csharp
.ConfigureAppConfiguration((_, configuration) =>
{
    var path = Path.Combine(
        Directory.GetCurrentDirectory(), "path/to/files");

    configuration.AddKeyPerFile(directoryPath: path, optional: true);
})
```

## <a name="memory-configuration-provider"></a><span data-ttu-id="e04c2-252">Dostawca konfiguracji pamięci</span><span class="sxs-lookup"><span data-stu-id="e04c2-252">Memory configuration provider</span></span>

<span data-ttu-id="e04c2-253"><xref:Microsoft.Extensions.Configuration.Memory.MemoryConfigurationProvider>Używa kolekcji w pamięci jako par klucz konfiguracji-wartość.</span><span class="sxs-lookup"><span data-stu-id="e04c2-253">The <xref:Microsoft.Extensions.Configuration.Memory.MemoryConfigurationProvider> uses an in-memory collection as configuration key-value pairs.</span></span>

<span data-ttu-id="e04c2-254">Poniższy kod dodaje kolekcję pamięci do systemu konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="e04c2-254">The following code adds a memory collection to the configuration system:</span></span>

:::code language="csharp" source="snippets/configuration/console-memory/Program.cs" highlight="22-29":::

<span data-ttu-id="e04c2-255">W powyższym kodzie program <xref:Microsoft.Extensions.Configuration.MemoryConfigurationBuilderExtensions.AddInMemoryCollection(Microsoft.Extensions.Configuration.IConfigurationBuilder,System.Collections.Generic.IEnumerable{System.Collections.Generic.KeyValuePair{System.String,System.String}})?displayProperty=nameWithType> dodaje dostawcę pamięci po domyślnych dostawcach konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="e04c2-255">In the preceding code, <xref:Microsoft.Extensions.Configuration.MemoryConfigurationBuilderExtensions.AddInMemoryCollection(Microsoft.Extensions.Configuration.IConfigurationBuilder,System.Collections.Generic.IEnumerable{System.Collections.Generic.KeyValuePair{System.String,System.String}})?displayProperty=nameWithType> adds the memory provider after the default configuration providers.</span></span> <span data-ttu-id="e04c2-256">Przykład określania kolejności dostawców konfiguracji można znaleźć w temacie [dostawca konfiguracji XML](#xml-configuration-provider).</span><span class="sxs-lookup"><span data-stu-id="e04c2-256">For an example of ordering the configuration providers, see [XML configuration provider](#xml-configuration-provider).</span></span>

## <a name="see-also"></a><span data-ttu-id="e04c2-257">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="e04c2-257">See also</span></span>

- [<span data-ttu-id="e04c2-258">Konfiguracja w programie .NET</span><span class="sxs-lookup"><span data-stu-id="e04c2-258">Configuration in .NET</span></span>](configuration.md)
- [<span data-ttu-id="e04c2-259">Host ogólny .NET</span><span class="sxs-lookup"><span data-stu-id="e04c2-259">.NET Generic Host</span></span>](generic-host.md)
- [<span data-ttu-id="e04c2-260">Implementowanie niestandardowego dostawcy konfiguracji</span><span class="sxs-lookup"><span data-stu-id="e04c2-260">Implement a custom configuration provider</span></span>](custom-configuration-provider.md)
