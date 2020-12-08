---
title: Rejestrowanie w programie .NET
author: IEvangelist
description: Dowiedz się, jak używać struktury rejestrowania dostarczonej przez pakiet NuGet Microsoft. Extensions. Logging.
ms.author: dapine
ms.date: 09/30/2020
ms.openlocfilehash: 73c16c80e7e000533b880e908b38109d2b1e88fd
ms.sourcegitcommit: 45c7148f2483db2501c1aa696ab6ed2ed8cb71b2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/08/2020
ms.locfileid: "96851730"
---
# <a name="logging-in-net"></a><span data-ttu-id="2e86d-103">Rejestrowanie w programie .NET</span><span class="sxs-lookup"><span data-stu-id="2e86d-103">Logging in .NET</span></span>

<span data-ttu-id="2e86d-104">Platforma .NET obsługuje interfejs API rejestrowania, który współpracuje z różnymi dostawcami rejestrowania wbudowanych i innych firm.</span><span class="sxs-lookup"><span data-stu-id="2e86d-104">.NET supports a logging API that works with a variety of built-in and third-party logging providers.</span></span> <span data-ttu-id="2e86d-105">W tym artykule pokazano, jak używać interfejsu API rejestrowania z wbudowanymi dostawcami.</span><span class="sxs-lookup"><span data-stu-id="2e86d-105">This article shows how to use the logging API with built-in providers.</span></span> <span data-ttu-id="2e86d-106">Większość przykładów kodu przedstawionych w tym artykule ma zastosowanie do dowolnej aplikacji platformy .NET korzystającej z [hosta ogólnego](generic-host.md).</span><span class="sxs-lookup"><span data-stu-id="2e86d-106">Most of the code examples shown in this article apply to any .NET app that uses the [Generic Host](generic-host.md).</span></span> <span data-ttu-id="2e86d-107">W przypadku aplikacji, które nie korzystają z hosta ogólnego, zobacz [Aplikacja konsolowa niebędąca hostem](#non-host-console-app).</span><span class="sxs-lookup"><span data-stu-id="2e86d-107">For apps that don't use the Generic Host, see [Non-host console app](#non-host-console-app).</span></span>

## <a name="create-logs"></a><span data-ttu-id="2e86d-108">Tworzenie dzienników</span><span class="sxs-lookup"><span data-stu-id="2e86d-108">Create logs</span></span>

<span data-ttu-id="2e86d-109">Aby utworzyć dzienniki, użyj <xref:Microsoft.Extensions.Logging.ILogger%601> obiektu z [iniekcji zależności (di)](dependency-injection.md).</span><span class="sxs-lookup"><span data-stu-id="2e86d-109">To create logs, use an <xref:Microsoft.Extensions.Logging.ILogger%601> object from [dependency injection (DI)](dependency-injection.md).</span></span>

<span data-ttu-id="2e86d-110">Poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="2e86d-110">The following example:</span></span>

- <span data-ttu-id="2e86d-111">Tworzy rejestrator, `ILogger<Worker>` który używa *kategorii* dziennika w pełni kwalifikowanej nazwy typu `Worker` .</span><span class="sxs-lookup"><span data-stu-id="2e86d-111">Creates a logger, `ILogger<Worker>`, which uses a log *category* of the fully qualified name of the type `Worker`.</span></span> <span data-ttu-id="2e86d-112">Kategoria dziennika jest ciągiem, który jest skojarzony z każdym dziennikiem.</span><span class="sxs-lookup"><span data-stu-id="2e86d-112">The log category is a string that is associated with each log.</span></span>
- <span data-ttu-id="2e86d-113">Wywołania <xref:Microsoft.Extensions.Logging.LoggerExtensions.LogInformation%2A> do rejestrowania na `Information` poziomie.</span><span class="sxs-lookup"><span data-stu-id="2e86d-113">Calls <xref:Microsoft.Extensions.Logging.LoggerExtensions.LogInformation%2A> to log at the `Information` level.</span></span> <span data-ttu-id="2e86d-114">*Poziom* dziennika wskazuje ważność rejestrowanego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="2e86d-114">The Log *level* indicates the severity of the logged event.</span></span>

:::code language="csharp" source="snippets/configuration/worker-service/Worker.cs" range="9-24" highlight="12":::

<span data-ttu-id="2e86d-115">[Poziomy](#log-level) i [Kategorie](#log-category) zostały wyjaśnione bardziej szczegółowo w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="2e86d-115">[Levels](#log-level) and [categories](#log-category) are explained in more detail later in this article.</span></span>

## <a name="configure-logging"></a><span data-ttu-id="2e86d-116">Konfigurowanie rejestrowania</span><span class="sxs-lookup"><span data-stu-id="2e86d-116">Configure logging</span></span>

<span data-ttu-id="2e86d-117">Konfiguracja rejestrowania jest zwykle udostępniana w `Logging` sekcji *AppSettings*. `{Environment}` pliki *. JSON* .</span><span class="sxs-lookup"><span data-stu-id="2e86d-117">Logging configuration is commonly provided by the `Logging` section of *appsettings*.`{Environment}`*.json* files.</span></span> <span data-ttu-id="2e86d-118">Następujące *appsettings.Development.js* pliku są generowane przez szablony usługi procesu roboczego platformy .NET:</span><span class="sxs-lookup"><span data-stu-id="2e86d-118">The following *appsettings.Development.json* file is generated by the .NET Worker service templates:</span></span>

:::code language="json" source="snippets/configuration/worker-service/appsettings.Development.json":::

<span data-ttu-id="2e86d-119">W powyższym kodzie JSON:</span><span class="sxs-lookup"><span data-stu-id="2e86d-119">In the preceding JSON:</span></span>

- <span data-ttu-id="2e86d-120">`"Default"`Określono, `"Microsoft"` , i `"Microsoft.Hosting.Lifetime"` Kategorie.</span><span class="sxs-lookup"><span data-stu-id="2e86d-120">The `"Default"`, `"Microsoft"`, and `"Microsoft.Hosting.Lifetime"` categories are specified.</span></span>
- <span data-ttu-id="2e86d-121">`"Microsoft"`Kategoria dotyczy wszystkich kategorii, które zaczynają się od `"Microsoft"` .</span><span class="sxs-lookup"><span data-stu-id="2e86d-121">The `"Microsoft"` category applies to all categories that start with `"Microsoft"`.</span></span>
- <span data-ttu-id="2e86d-122">`"Microsoft"`Kategoria rejestruje się na poziomie dziennika `Warning` lub wyższym.</span><span class="sxs-lookup"><span data-stu-id="2e86d-122">The `"Microsoft"` category logs at log level `Warning` and higher.</span></span>
- <span data-ttu-id="2e86d-123">`"Microsoft.Hosting.Lifetime"`Kategoria jest bardziej precyzyjna niż `"Microsoft"` Kategoria, więc jest `"Microsoft.Hosting.Lifetime"` rejestrowana w kategorii na poziomie dziennika "informacje" i wyższych.</span><span class="sxs-lookup"><span data-stu-id="2e86d-123">The `"Microsoft.Hosting.Lifetime"` category is more specific than the `"Microsoft"` category, so the `"Microsoft.Hosting.Lifetime"` category logs at log level "Information" and higher.</span></span>
- <span data-ttu-id="2e86d-124">Określony dostawca dziennika nie został określony, dlatego `LogLevel` dotyczy wszystkich włączonych dostawców rejestrowania z wyjątkiem [dziennika zdarzeń systemu Windows](logging-providers.md#windows-eventlog).</span><span class="sxs-lookup"><span data-stu-id="2e86d-124">A specific log provider is not specified, so `LogLevel` applies to all the enabled logging providers except for the [Windows EventLog](logging-providers.md#windows-eventlog).</span></span>

<span data-ttu-id="2e86d-125">`Logging`Właściwość może mieć <xref:Microsoft.Extensions.Logging.LogLevel> właściwości dostawcy dzienników i.</span><span class="sxs-lookup"><span data-stu-id="2e86d-125">The `Logging` property can have <xref:Microsoft.Extensions.Logging.LogLevel> and log provider properties.</span></span> <span data-ttu-id="2e86d-126">`LogLevel`Określa minimalny [poziom](#log-level) rejestrowania wybranych kategorii.</span><span class="sxs-lookup"><span data-stu-id="2e86d-126">The `LogLevel` specifies the minimum [level](#log-level) to log for selected categories.</span></span> <span data-ttu-id="2e86d-127">W poprzednim pliku JSON `Information` i `Warning` poziomy dziennika są określone.</span><span class="sxs-lookup"><span data-stu-id="2e86d-127">In the preceding JSON, `Information` and `Warning` log levels are specified.</span></span> <span data-ttu-id="2e86d-128">`LogLevel` wskazuje ważność dziennika i zakres od 0 do 6:</span><span class="sxs-lookup"><span data-stu-id="2e86d-128">`LogLevel` indicates the severity of the log and ranges from 0 to 6:</span></span>

<span data-ttu-id="2e86d-129">`Trace` = 0, `Debug` = 1, `Information` = 2, `Warning` = 3, `Error` = 4, `Critical` = 5 i `None` = 6.</span><span class="sxs-lookup"><span data-stu-id="2e86d-129">`Trace` = 0, `Debug` = 1, `Information` = 2, `Warning` = 3, `Error` = 4, `Critical` = 5, and `None` = 6.</span></span>

<span data-ttu-id="2e86d-130">Gdy `LogLevel` jest określony, funkcja rejestrowania jest włączona dla komunikatów na określonym poziomie i wyższych.</span><span class="sxs-lookup"><span data-stu-id="2e86d-130">When a `LogLevel` is specified, logging is enabled for messages at the specified level and higher.</span></span> <span data-ttu-id="2e86d-131">W poprzednim pliku JSON `Default` Kategoria jest zarejestrowana dla `Information` i wyższa.</span><span class="sxs-lookup"><span data-stu-id="2e86d-131">In the preceding JSON, the `Default` category is logged for `Information` and higher.</span></span> <span data-ttu-id="2e86d-132">Na przykład,,, `Information` `Warning` `Error` i `Critical` komunikaty są rejestrowane.</span><span class="sxs-lookup"><span data-stu-id="2e86d-132">For example, `Information`, `Warning`, `Error`, and `Critical` messages are logged.</span></span> <span data-ttu-id="2e86d-133">Jeśli nie `LogLevel` jest określony, rejestrowane są wartości domyślne na `Information` poziomie.</span><span class="sxs-lookup"><span data-stu-id="2e86d-133">If no `LogLevel` is specified, logging defaults to the `Information` level.</span></span> <span data-ttu-id="2e86d-134">Aby uzyskać więcej informacji, zobacz [poziomy dzienników](#log-level).</span><span class="sxs-lookup"><span data-stu-id="2e86d-134">For more information, see [Log levels](#log-level).</span></span>

<span data-ttu-id="2e86d-135">Właściwość dostawcy może określać `LogLevel` Właściwość.</span><span class="sxs-lookup"><span data-stu-id="2e86d-135">A provider property can specify a `LogLevel` property.</span></span> <span data-ttu-id="2e86d-136">`LogLevel` w obszarze dostawca Określa poziomy do rejestrowania dla tego dostawcy i zastępuje ustawienia dziennika niedostawcy.</span><span class="sxs-lookup"><span data-stu-id="2e86d-136">`LogLevel` under a provider specifies levels to log for that provider, and overrides the non-provider log settings.</span></span> <span data-ttu-id="2e86d-137">Rozważmy następujące *appsettings.js* pliku:</span><span class="sxs-lookup"><span data-stu-id="2e86d-137">Consider the following *appsettings.json* file:</span></span>

:::code language="json" source="snippets/configuration/worker-service/appsettings.Staging.json":::

<span data-ttu-id="2e86d-138">Ustawienia w `Logging.{ProviderName}.LogLevel` ustawieniach przesłonięcia w programie `Logging.LogLevel` .</span><span class="sxs-lookup"><span data-stu-id="2e86d-138">Settings in `Logging.{ProviderName}.LogLevel` override settings in `Logging.LogLevel`.</span></span> <span data-ttu-id="2e86d-139">W powyższym kodzie JSON `Debug` domyślny poziom rejestrowania dostawcy jest ustawiany na `Information` :</span><span class="sxs-lookup"><span data-stu-id="2e86d-139">In the preceding JSON, the `Debug` provider's default log level is set to `Information`:</span></span>

`Logging:Debug:LogLevel:Default:Information`

<span data-ttu-id="2e86d-140">Powyższe ustawienie określa `Information` poziom rejestrowania dla każdej `Logging:Debug:` kategorii z wyjątkiem `Microsoft.Hosting` .</span><span class="sxs-lookup"><span data-stu-id="2e86d-140">The preceding setting specifies the `Information` log level for every `Logging:Debug:` category except `Microsoft.Hosting`.</span></span> <span data-ttu-id="2e86d-141">Gdy określona kategoria jest wymieniona, określona Kategoria zastępuje domyślną kategorię.</span><span class="sxs-lookup"><span data-stu-id="2e86d-141">When a specific category is listed, the specific category overrides the default category.</span></span> <span data-ttu-id="2e86d-142">W powyższym formacie JSON `Logging:Debug:LogLevel` Kategorie `"Microsoft.Hosting"` i `"Default"` zastępują ustawienia w `Logging:LogLevel`</span><span class="sxs-lookup"><span data-stu-id="2e86d-142">In the preceding JSON, the `Logging:Debug:LogLevel` categories `"Microsoft.Hosting"` and `"Default"` override the settings in `Logging:LogLevel`</span></span>

<span data-ttu-id="2e86d-143">Minimalny poziom dziennika można określić dla dowolnego z:</span><span class="sxs-lookup"><span data-stu-id="2e86d-143">The minimum log level can be specified for any of:</span></span>

- <span data-ttu-id="2e86d-144">Określeni dostawcy: na przykład `Logging:EventSource:LogLevel:Default:Information`</span><span class="sxs-lookup"><span data-stu-id="2e86d-144">Specific providers:  For example, `Logging:EventSource:LogLevel:Default:Information`</span></span>
- <span data-ttu-id="2e86d-145">Określone kategorie: na przykład `Logging:LogLevel:Microsoft:Warning`</span><span class="sxs-lookup"><span data-stu-id="2e86d-145">Specific categories: For example, `Logging:LogLevel:Microsoft:Warning`</span></span>
- <span data-ttu-id="2e86d-146">Wszyscy dostawcy i wszystkie kategorie: `Logging:LogLevel:Default:Warning`</span><span class="sxs-lookup"><span data-stu-id="2e86d-146">All providers and all categories: `Logging:LogLevel:Default:Warning`</span></span>

<span data-ttu-id="2e86d-147">Wszystkie dzienniki poniżej minimalnego poziomu są \***not** _:</span><span class="sxs-lookup"><span data-stu-id="2e86d-147">Any logs below the minimum level are \***not** _:</span></span>

- <span data-ttu-id="2e86d-148">Przeszedł do dostawcy.</span><span class="sxs-lookup"><span data-stu-id="2e86d-148">Passed to the provider.</span></span>
- <span data-ttu-id="2e86d-149">Zarejestrowane lub wyświetlone.</span><span class="sxs-lookup"><span data-stu-id="2e86d-149">Logged or displayed.</span></span>

<span data-ttu-id="2e86d-150">Aby pominąć wszystkie dzienniki, należy określić [wartość LogLevel. None](xref:Microsoft.Extensions.Logging.LogLevel).</span><span class="sxs-lookup"><span data-stu-id="2e86d-150">To suppress all logs, specify [LogLevel.None](xref:Microsoft.Extensions.Logging.LogLevel).</span></span> <span data-ttu-id="2e86d-151">`LogLevel.None` ma wartość 6, która jest większa niż `LogLevel.Critical` (5).</span><span class="sxs-lookup"><span data-stu-id="2e86d-151">`LogLevel.None` has a value of 6, which is higher than `LogLevel.Critical` (5).</span></span>

<span data-ttu-id="2e86d-152">Jeśli dostawca obsługuje [zakresy rejestrowania](#log-scopes), `IncludeScopes` wskazuje, czy są one włączone.</span><span class="sxs-lookup"><span data-stu-id="2e86d-152">If a provider supports [log scopes](#log-scopes), `IncludeScopes` indicates whether they're enabled.</span></span> <span data-ttu-id="2e86d-153">Aby uzyskać więcej informacji, zobacz [zakresy dzienników](#log-scopes)</span><span class="sxs-lookup"><span data-stu-id="2e86d-153">For more information, see [log scopes](#log-scopes)</span></span>

<span data-ttu-id="2e86d-154">Następujące _appsettings.jsw pliku \* zawierają ustawienia dla wszystkich wbudowanych dostawców:</span><span class="sxs-lookup"><span data-stu-id="2e86d-154">The following _appsettings.json\* file contains settings for all of the built-in providers:</span></span>

:::code language="json" source="snippets/configuration/worker-service/appsettings.Production.json":::

<span data-ttu-id="2e86d-155">W poprzednim przykładzie:</span><span class="sxs-lookup"><span data-stu-id="2e86d-155">In the preceding sample:</span></span>

- <span data-ttu-id="2e86d-156">Kategorie i poziomy nie są sugerowanymi wartościami.</span><span class="sxs-lookup"><span data-stu-id="2e86d-156">The categories and levels are not suggested values.</span></span> <span data-ttu-id="2e86d-157">Przykład podano, aby wyświetlić wszystkich dostawców domyślnych.</span><span class="sxs-lookup"><span data-stu-id="2e86d-157">The sample is provided to show all the default providers.</span></span>
- <span data-ttu-id="2e86d-158">Ustawienia w `Logging.{ProviderName}.LogLevel` ustawieniach przesłonięcia w programie `Logging.LogLevel` .</span><span class="sxs-lookup"><span data-stu-id="2e86d-158">Settings in `Logging.{ProviderName}.LogLevel` override settings in `Logging.LogLevel`.</span></span> <span data-ttu-id="2e86d-159">Na przykład poziom w `Debug.LogLevel.Default` zastępują poziom w `LogLevel.Default` .</span><span class="sxs-lookup"><span data-stu-id="2e86d-159">For example, the level in `Debug.LogLevel.Default` overrides the level in `LogLevel.Default`.</span></span>
- <span data-ttu-id="2e86d-160">*Alias* każdego dostawcy jest używany.</span><span class="sxs-lookup"><span data-stu-id="2e86d-160">Each provider's *alias* is used.</span></span> <span data-ttu-id="2e86d-161">Każdy dostawca definiuje *alias* , który może być używany w konfiguracji zamiast w pełni kwalifikowanej nazwy typu.</span><span class="sxs-lookup"><span data-stu-id="2e86d-161">Each provider defines an *alias* that can be used in configuration in place of the fully qualified type name.</span></span> <span data-ttu-id="2e86d-162">Aliasy wbudowane dostawcy to:</span><span class="sxs-lookup"><span data-stu-id="2e86d-162">The built-in providers' aliases are:</span></span>
  - <span data-ttu-id="2e86d-163">Konsola</span><span class="sxs-lookup"><span data-stu-id="2e86d-163">Console</span></span>
  - <span data-ttu-id="2e86d-164">Debugowanie</span><span class="sxs-lookup"><span data-stu-id="2e86d-164">Debug</span></span>
  - <span data-ttu-id="2e86d-165">EventSource</span><span class="sxs-lookup"><span data-stu-id="2e86d-165">EventSource</span></span>
  - <span data-ttu-id="2e86d-166">Elemencie</span><span class="sxs-lookup"><span data-stu-id="2e86d-166">EventLog</span></span>
  - <span data-ttu-id="2e86d-167">AzureAppServicesFile</span><span class="sxs-lookup"><span data-stu-id="2e86d-167">AzureAppServicesFile</span></span>
  - <span data-ttu-id="2e86d-168">AzureAppServicesBlob</span><span class="sxs-lookup"><span data-stu-id="2e86d-168">AzureAppServicesBlob</span></span>
  - <span data-ttu-id="2e86d-169">ApplicationInsights</span><span class="sxs-lookup"><span data-stu-id="2e86d-169">ApplicationInsights</span></span>

### <a name="set-log-level-by-command-line-environment-variables-and-other-configuration"></a><span data-ttu-id="2e86d-170">Ustawianie poziomu dziennika według wiersza polecenia, zmiennych środowiskowych i innych konfiguracji</span><span class="sxs-lookup"><span data-stu-id="2e86d-170">Set log level by command line, environment variables, and other configuration</span></span>

<span data-ttu-id="2e86d-171">Poziom dziennika może być ustawiony przez dowolnego [dostawcę konfiguracji](configuration-providers.md).</span><span class="sxs-lookup"><span data-stu-id="2e86d-171">Log level can be set by any of the [configuration providers](configuration-providers.md).</span></span>

<span data-ttu-id="2e86d-172">Następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="2e86d-172">The following commands:</span></span>

- <span data-ttu-id="2e86d-173">Ustaw klucz środowiska na `Logging:LogLevel:Microsoft` wartość `Information` w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="2e86d-173">Set the environment key `Logging:LogLevel:Microsoft` to a value of `Information` on Windows.</span></span>
- <span data-ttu-id="2e86d-174">Przetestuj ustawienia w przypadku korzystania z aplikacji utworzonej przy użyciu szablonów usługi procesu roboczego platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="2e86d-174">Test the settings when using an app created with the .NET Worker service templates.</span></span> <span data-ttu-id="2e86d-175">`dotnet run`Polecenie musi być uruchamiane w katalogu projektu po użyciu `set` .</span><span class="sxs-lookup"><span data-stu-id="2e86d-175">The `dotnet run` command must be run in the project directory after using `set`.</span></span>

```cmd
set Logging__LogLevel__Microsoft=Information
dotnet run
```

<span data-ttu-id="2e86d-176">Poprzednie ustawienie środowiska:</span><span class="sxs-lookup"><span data-stu-id="2e86d-176">The preceding environment setting:</span></span>

- <span data-ttu-id="2e86d-177">Jest ustawiana tylko w ramach procesów uruchomionych z poziomu okna polecenia, które zostały ustawione w.</span><span class="sxs-lookup"><span data-stu-id="2e86d-177">Is only set in processes launched from the command window they were set in.</span></span>
- <span data-ttu-id="2e86d-178">Nie są odczytywane przez aplikacje uruchomione w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2e86d-178">Isn't read by apps launched with Visual Studio.</span></span>

<span data-ttu-id="2e86d-179">Następujące polecenie [setx](/windows-server/administration/windows-commands/setx) ustawia również klucz środowiska i wartość w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="2e86d-179">The following [setx](/windows-server/administration/windows-commands/setx) command also sets the environment key and value on Windows.</span></span> <span data-ttu-id="2e86d-180">W przeciwieństwie do `set` , `setx` Ustawienia są utrwalane.</span><span class="sxs-lookup"><span data-stu-id="2e86d-180">Unlike `set`, `setx` settings are persisted.</span></span> <span data-ttu-id="2e86d-181">`/M`Przełącznik ustawia zmienną w środowisku systemowym.</span><span class="sxs-lookup"><span data-stu-id="2e86d-181">The `/M` switch sets the variable in the system environment.</span></span> <span data-ttu-id="2e86d-182">Jeśli `/M` nie jest używany, zmienna środowiskowa użytkownika jest ustawiona.</span><span class="sxs-lookup"><span data-stu-id="2e86d-182">If `/M` isn't used, a user environment variable is set.</span></span>

```cmd
setx Logging__LogLevel__Microsoft=Information /M
```

<span data-ttu-id="2e86d-183">Na [Azure App Service](https://azure.microsoft.com/services/app-service/)wybierz pozycję **nowe ustawienie aplikacji** na stronie **Konfiguracja > ustawienia** .</span><span class="sxs-lookup"><span data-stu-id="2e86d-183">On [Azure App Service](https://azure.microsoft.com/services/app-service/), select **New application setting** on the **Settings > Configuration** page.</span></span> <span data-ttu-id="2e86d-184">Ustawienia aplikacji Azure App Service są następujące:</span><span class="sxs-lookup"><span data-stu-id="2e86d-184">Azure App Service application settings are:</span></span>

- <span data-ttu-id="2e86d-185">Szyfrowane i przesyłane przez zaszyfrowanego kanału.</span><span class="sxs-lookup"><span data-stu-id="2e86d-185">Encrypted at rest and transmitted over an encrypted channel.</span></span>
- <span data-ttu-id="2e86d-186">Uwidocznione jako zmienne środowiskowe.</span><span class="sxs-lookup"><span data-stu-id="2e86d-186">Exposed as environment variables.</span></span>

<span data-ttu-id="2e86d-187">Aby uzyskać więcej informacji na temat ustawiania wartości konfiguracyjnych platformy .NET przy użyciu zmiennych środowiskowych, zobacz [zmienne środowiskowe](configuration-providers.md#environment-variable-configuration-provider).</span><span class="sxs-lookup"><span data-stu-id="2e86d-187">For more information on setting .NET configuration values using environment variables, see [environment variables](configuration-providers.md#environment-variable-configuration-provider).</span></span>

## <a name="how-filtering-rules-are-applied"></a><span data-ttu-id="2e86d-188">Jak są stosowane reguły filtrowania</span><span class="sxs-lookup"><span data-stu-id="2e86d-188">How filtering rules are applied</span></span>

<span data-ttu-id="2e86d-189">Po <xref:Microsoft.Extensions.Logging.ILogger%601> utworzeniu obiektu <xref:Microsoft.Extensions.Logging.ILoggerFactory> obiekt wybiera jedną regułę dla każdego dostawcy, która ma zostać zastosowana do tego rejestratora.</span><span class="sxs-lookup"><span data-stu-id="2e86d-189">When an <xref:Microsoft.Extensions.Logging.ILogger%601> object is created, the <xref:Microsoft.Extensions.Logging.ILoggerFactory> object selects a single rule per provider to apply to that logger.</span></span> <span data-ttu-id="2e86d-190">Wszystkie komunikaty zapisywane przez `ILogger` wystąpienie są filtrowane na podstawie wybranych reguł.</span><span class="sxs-lookup"><span data-stu-id="2e86d-190">All messages written by an `ILogger` instance are filtered based on the selected rules.</span></span> <span data-ttu-id="2e86d-191">Dla każdego dostawcy i pary kategorii jest wybierana najbardziej konkretna reguła z dostępnych reguł.</span><span class="sxs-lookup"><span data-stu-id="2e86d-191">The most specific rule for each provider and category pair is selected from the available rules.</span></span>

<span data-ttu-id="2e86d-192">Następujący algorytm jest używany dla każdego dostawcy, gdy `ILogger` jest tworzony dla danej kategorii:</span><span class="sxs-lookup"><span data-stu-id="2e86d-192">The following algorithm is used for each provider when an `ILogger` is created for a given category:</span></span>

- <span data-ttu-id="2e86d-193">Wybierz wszystkie reguły, które pasują do dostawcy lub jego aliasu.</span><span class="sxs-lookup"><span data-stu-id="2e86d-193">Select all rules that match the provider or its alias.</span></span> <span data-ttu-id="2e86d-194">Jeśli nie zostanie znalezione dopasowanie, zaznacz wszystkie reguły z pustym dostawcą.</span><span class="sxs-lookup"><span data-stu-id="2e86d-194">If no match is found, select all rules with an empty provider.</span></span>
- <span data-ttu-id="2e86d-195">W wyniku poprzedniego kroku wybierz pozycję reguły z najdłuższym prefiksem kategorii.</span><span class="sxs-lookup"><span data-stu-id="2e86d-195">From the result of the preceding step, select rules with longest matching category prefix.</span></span> <span data-ttu-id="2e86d-196">Jeśli nie zostanie znalezione dopasowanie, zaznacz wszystkie reguły, które nie określają kategorii.</span><span class="sxs-lookup"><span data-stu-id="2e86d-196">If no match is found, select all rules that don't specify a category.</span></span>
- <span data-ttu-id="2e86d-197">Jeśli wybrano wiele reguł, zrób to **ostatnie** .</span><span class="sxs-lookup"><span data-stu-id="2e86d-197">If multiple rules are selected, take the **last** one.</span></span>
- <span data-ttu-id="2e86d-198">Jeśli nie wybrano żadnych reguł, użyj, <xref:Microsoft.Extensions.Logging.LoggingBuilderExtensions.SetMinimumLevel(Microsoft.Extensions.Logging.ILoggingBuilder,Microsoft.Extensions.Logging.LogLevel)?displayProperty=nameWithType> Aby określić minimalny poziom rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="2e86d-198">If no rules are selected, use <xref:Microsoft.Extensions.Logging.LoggingBuilderExtensions.SetMinimumLevel(Microsoft.Extensions.Logging.ILoggingBuilder,Microsoft.Extensions.Logging.LogLevel)?displayProperty=nameWithType> to specify the minimum logging level.</span></span>

## <a name="log-category"></a><span data-ttu-id="2e86d-199">Kategoria dziennika</span><span class="sxs-lookup"><span data-stu-id="2e86d-199">Log category</span></span>

<span data-ttu-id="2e86d-200">Po `ILogger` utworzeniu obiektu zostanie określona *Kategoria* .</span><span class="sxs-lookup"><span data-stu-id="2e86d-200">When an `ILogger` object is created, a *category* is specified.</span></span> <span data-ttu-id="2e86d-201">Ta kategoria jest dołączona do każdego komunikatu dziennika utworzonego przez to wystąpienie `ILogger` .</span><span class="sxs-lookup"><span data-stu-id="2e86d-201">That category is included with each log message created by that instance of `ILogger`.</span></span> <span data-ttu-id="2e86d-202">Ciąg kategorii jest dowolny, ale Konwencja ma używać nazwy klasy.</span><span class="sxs-lookup"><span data-stu-id="2e86d-202">The category string is arbitrary, but the convention is to use the class name.</span></span> <span data-ttu-id="2e86d-203">Na przykład w aplikacji z usługą zdefiniowaną jako następujący obiekt może być kategorią `"Example.DefaultService"` :</span><span class="sxs-lookup"><span data-stu-id="2e86d-203">For example, in an application with a service define like the following object, the category might be `"Example.DefaultService"`:</span></span>

```csharp
namespace Example
{
    public class DefaultService : IService
    {
        private readonly ILogger<DefaultService> _logger;

        public DefaultService(ILogger<DefaultService> logger) =>
            _logger = logger;

        // ...
    }
}
```

<span data-ttu-id="2e86d-204">Aby jawnie określić kategorię, wywołaj <xref:Microsoft.Extensions.Logging.LoggerFactory.CreateLogger%2A?displayProperty=nameWithType> :</span><span class="sxs-lookup"><span data-stu-id="2e86d-204">To explicitly specify the category, call <xref:Microsoft.Extensions.Logging.LoggerFactory.CreateLogger%2A?displayProperty=nameWithType>:</span></span>

```csharp
namespace Example
{
    public class DefaultService : IService
    {
        private readonly ILogger _logger;

        public DefaultService(ILoggerFactory loggerFactory) =>
            _logger = loggerFactory.CreateLogger("CustomCategory");

        // ...
    }
}
```

<span data-ttu-id="2e86d-205">Wywoływanie `CreateLogger` przy użyciu stałej nazwy może być przydatne w przypadku używania wielu metod, dzięki czemu zdarzenia mogą być zorganizowane według kategorii.</span><span class="sxs-lookup"><span data-stu-id="2e86d-205">Calling `CreateLogger` with a fixed name can be useful when used in multiple methods so the events can be organized by category.</span></span>

<span data-ttu-id="2e86d-206">`ILogger<T>` jest odpowiednikiem wywołania `CreateLogger` z w pełni kwalifikowaną nazwą typu `T` .</span><span class="sxs-lookup"><span data-stu-id="2e86d-206">`ILogger<T>` is equivalent to calling `CreateLogger` with the fully qualified type name of `T`.</span></span>

## <a name="log-level"></a><span data-ttu-id="2e86d-207">Poziom dziennika</span><span class="sxs-lookup"><span data-stu-id="2e86d-207">Log level</span></span>

<span data-ttu-id="2e86d-208">W poniższej tabeli wymieniono <xref:Microsoft.Extensions.Logging.LogLevel> wartości, wygodną `Log{LogLevel}` metodę rozszerzenia oraz Sugerowane użycie:</span><span class="sxs-lookup"><span data-stu-id="2e86d-208">The following table lists the <xref:Microsoft.Extensions.Logging.LogLevel> values, the convenience `Log{LogLevel}` extension method, and the suggested usage:</span></span>

| <span data-ttu-id="2e86d-209">LogLevel</span><span class="sxs-lookup"><span data-stu-id="2e86d-209">LogLevel</span></span> | <span data-ttu-id="2e86d-210">Wartość</span><span class="sxs-lookup"><span data-stu-id="2e86d-210">Value</span></span> | <span data-ttu-id="2e86d-211">Metoda</span><span class="sxs-lookup"><span data-stu-id="2e86d-211">Method</span></span> | <span data-ttu-id="2e86d-212">Opis</span><span class="sxs-lookup"><span data-stu-id="2e86d-212">Description</span></span> |
|--|--|--|--|
| [<span data-ttu-id="2e86d-213">Ślad</span><span class="sxs-lookup"><span data-stu-id="2e86d-213">Trace</span></span>](xref:Microsoft.Extensions.Logging.LogLevel) | <span data-ttu-id="2e86d-214">0</span><span class="sxs-lookup"><span data-stu-id="2e86d-214">0</span></span> | <xref:Microsoft.Extensions.Logging.LoggerExtensions.LogTrace%2A> | <span data-ttu-id="2e86d-215">Zawierają najwięcej szczegółowych komunikatów.</span><span class="sxs-lookup"><span data-stu-id="2e86d-215">Contain the most detailed messages.</span></span> <span data-ttu-id="2e86d-216">Te komunikaty mogą zawierać poufne dane aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2e86d-216">These messages may contain sensitive app data.</span></span> <span data-ttu-id="2e86d-217">Te komunikaty są domyślnie wyłączone i **nie** powinny być włączone w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="2e86d-217">These messages are disabled by default and should \***not** _ be enabled in production.</span></span> |
| [<span data-ttu-id="2e86d-218">Debugowanie</span><span class="sxs-lookup"><span data-stu-id="2e86d-218">Debug</span></span>](xref:Microsoft.Extensions.Logging.LogLevel) | <span data-ttu-id="2e86d-219">1</span><span class="sxs-lookup"><span data-stu-id="2e86d-219">1</span></span> | <xref:Microsoft.Extensions.Logging.LoggerExtensions.LogDebug%2A> | <span data-ttu-id="2e86d-220">Na potrzeby debugowania i programowania.</span><span class="sxs-lookup"><span data-stu-id="2e86d-220">For debugging and development.</span></span> <span data-ttu-id="2e86d-221">W środowisku produkcyjnym należy używać ostrożnie z powodu dużego wolumenu.</span><span class="sxs-lookup"><span data-stu-id="2e86d-221">Use with caution in production due to the high volume.</span></span> |
| [<span data-ttu-id="2e86d-222">Informacje</span><span class="sxs-lookup"><span data-stu-id="2e86d-222">Information</span></span>](xref:Microsoft.Extensions.Logging.LogLevel) | <span data-ttu-id="2e86d-223">2</span><span class="sxs-lookup"><span data-stu-id="2e86d-223">2</span></span> | <xref:Microsoft.Extensions.Logging.LoggerExtensions.LogInformation%2A> | <span data-ttu-id="2e86d-224">Śledzi ogólny przepływ aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2e86d-224">Tracks the general flow of the app.</span></span> <span data-ttu-id="2e86d-225">Może mieć wartość długoterminową.</span><span class="sxs-lookup"><span data-stu-id="2e86d-225">May have long-term value.</span></span> |
| [<span data-ttu-id="2e86d-226">Ostrzeżenie</span><span class="sxs-lookup"><span data-stu-id="2e86d-226">Warning</span></span>](xref:Microsoft.Extensions.Logging.LogLevel) | <span data-ttu-id="2e86d-227">3</span><span class="sxs-lookup"><span data-stu-id="2e86d-227">3</span></span> | <xref:Microsoft.Extensions.Logging.LoggerExtensions.LogWarning%2A> | <span data-ttu-id="2e86d-228">Dla nietypowych lub nieoczekiwanych zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="2e86d-228">For abnormal or unexpected events.</span></span> <span data-ttu-id="2e86d-229">Zwykle zawiera błędy lub warunki, które nie powodują błędu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2e86d-229">Typically includes errors or conditions that don't cause the app to fail.</span></span> |
| [<span data-ttu-id="2e86d-230">Błąd</span><span class="sxs-lookup"><span data-stu-id="2e86d-230">Error</span></span>](xref:Microsoft.Extensions.Logging.LogLevel) | <span data-ttu-id="2e86d-231">4</span><span class="sxs-lookup"><span data-stu-id="2e86d-231">4</span></span> | <xref:Microsoft.Extensions.Logging.LoggerExtensions.LogError%2A> | <span data-ttu-id="2e86d-232">W przypadku błędów i wyjątków, których nie można obsłużyć.</span><span class="sxs-lookup"><span data-stu-id="2e86d-232">For errors and exceptions that cannot be handled.</span></span> <span data-ttu-id="2e86d-233">Te komunikaty wskazują na niepowodzenie podczas bieżącej operacji lub żądania, a nie awarię całej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2e86d-233">These messages indicate a failure in the current operation or request, not an app-wide failure.</span></span> |
| [<span data-ttu-id="2e86d-234">Krytyczne</span><span class="sxs-lookup"><span data-stu-id="2e86d-234">Critical</span></span>](xref:Microsoft.Extensions.Logging.LogLevel) | <span data-ttu-id="2e86d-235">5</span><span class="sxs-lookup"><span data-stu-id="2e86d-235">5</span></span> | <xref:Microsoft.Extensions.Logging.LoggerExtensions.LogCritical%2A> | <span data-ttu-id="2e86d-236">Dla niepowodzeń, które wymagają natychmiastowej uwagi.</span><span class="sxs-lookup"><span data-stu-id="2e86d-236">For failures that require immediate attention.</span></span> <span data-ttu-id="2e86d-237">Przykłady: scenariusze utraty danych, brak miejsca na dysku.</span><span class="sxs-lookup"><span data-stu-id="2e86d-237">Examples: data loss scenarios, out of disk space.</span></span> |
| [<span data-ttu-id="2e86d-238">Brak</span><span class="sxs-lookup"><span data-stu-id="2e86d-238">None</span></span>](xref:Microsoft.Extensions.Logging.LogLevel) | <span data-ttu-id="2e86d-239">6</span><span class="sxs-lookup"><span data-stu-id="2e86d-239">6</span></span> |  | <span data-ttu-id="2e86d-240">Określa, że nie należy zapisywać żadnych komunikatów.</span><span class="sxs-lookup"><span data-stu-id="2e86d-240">Specifies that no messages should be written.</span></span> |

<span data-ttu-id="2e86d-241">W poprzedniej tabeli `LogLevel` znajduje się na liście od najniższej do najwyższej wagi.</span><span class="sxs-lookup"><span data-stu-id="2e86d-241">In the previous table, the `LogLevel` is listed from lowest to highest severity.</span></span>

<span data-ttu-id="2e86d-242">Pierwszy parametr metody [log](xref:Microsoft.Extensions.Logging.LoggerExtensions) <xref:Microsoft.Extensions.Logging.LogLevel> wskazuje ważność dziennika.</span><span class="sxs-lookup"><span data-stu-id="2e86d-242">The [Log](xref:Microsoft.Extensions.Logging.LoggerExtensions) method's first parameter, <xref:Microsoft.Extensions.Logging.LogLevel>, indicates the severity of the log.</span></span> <span data-ttu-id="2e86d-243">Zamiast wywoływania `Log(LogLevel, ...)` , większość deweloperów wywołuje metody rozszerzenia [dziennika {LogLevel}](xref:Microsoft.Extensions.Logging.LoggerExtensions) .</span><span class="sxs-lookup"><span data-stu-id="2e86d-243">Rather than calling `Log(LogLevel, ...)`, most developers call the [Log{LogLevel}](xref:Microsoft.Extensions.Logging.LoggerExtensions) extension methods.</span></span> <span data-ttu-id="2e86d-244">`Log{LogLevel}`Metody rozszerzające [wywołują metodę log i określają wartość LogLevel](https://github.com/dotnet/extensions/blob/release/3.1/src/Logging/Logging.Abstractions/src/LoggerExtensions.cs).</span><span class="sxs-lookup"><span data-stu-id="2e86d-244">The `Log{LogLevel}` extension methods [call the Log method and specify the LogLevel](https://github.com/dotnet/extensions/blob/release/3.1/src/Logging/Logging.Abstractions/src/LoggerExtensions.cs).</span></span> <span data-ttu-id="2e86d-245">Na przykład następujące dwa wywołania rejestrowania są funkcjonalnie równoważne i generują ten sam dziennik:</span><span class="sxs-lookup"><span data-stu-id="2e86d-245">For example, the following two logging calls are functionally equivalent and produce the same log:</span></span>

```csharp
public void LogDetails()
{
    var logMessage = "Details for log.";

    _logger.Log(LogLevel.Information, AppLogEvents.Details, logMessage);
    _logger.LogInformation(AppLogEvents.Details, logMessage);
}
```

<span data-ttu-id="2e86d-246">`AppLogEvents.Details` jest IDENTYFIKATORem zdarzenia i jest niejawnie reprezentowany przez wartość stałą <xref:System.Int32> .</span><span class="sxs-lookup"><span data-stu-id="2e86d-246">`AppLogEvents.Details` is the event ID, and is implicitly represented by a constant <xref:System.Int32> value.</span></span> <span data-ttu-id="2e86d-247">`AppLogEvents` jest klasą, która ujawnia różne nazwane identyfikatory i jest wyświetlana w sekcji [Identyfikator zdarzenia dziennika](#log-event-id) .</span><span class="sxs-lookup"><span data-stu-id="2e86d-247">`AppLogEvents` is a class that exposes various named identifier constants and is displayed in the [Log event ID](#log-event-id) section.</span></span>

<span data-ttu-id="2e86d-248">Poniższy kod tworzy `Information` i `Warning` rejestruje:</span><span class="sxs-lookup"><span data-stu-id="2e86d-248">The following code creates `Information` and `Warning` logs:</span></span>

```csharp
public async Task<T> GetAsync<T>(string id)
{
    _logger.LogInformation(AppLogEvents.Read, "Reading value for {Id}", id);

    var result = await _repository.GetAsync(id);
    if (result is null)
    {
        _logger.LogWarning(AppLogEvents.ReadNotFound, "GetAsync({Id}) not found", id);
    }

    return result;
}
```

<span data-ttu-id="2e86d-249">W poprzednim kodzie pierwszy `Log{LogLevel}` parametr, `AppLogEvents.Read` , jest [Identyfikator zdarzenia dziennika](#log-event-id).</span><span class="sxs-lookup"><span data-stu-id="2e86d-249">In the preceding code, the first `Log{LogLevel}` parameter,`AppLogEvents.Read`, is the [Log event ID](#log-event-id).</span></span> <span data-ttu-id="2e86d-250">Drugi parametr jest szablonem wiadomości z symbolami zastępczymi dla wartości argumentów dostarczonych przez pozostałe parametry metody.</span><span class="sxs-lookup"><span data-stu-id="2e86d-250">The second parameter is a message template with placeholders for argument values provided by the remaining method parameters.</span></span> <span data-ttu-id="2e86d-251">Parametry metody zostały wyjaśnione w sekcji [szablon komunikatu](#log-message-template) w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="2e86d-251">The method parameters are explained in the [message template](#log-message-template) section later in this article.</span></span>

<span data-ttu-id="2e86d-252">Skonfiguruj odpowiedni poziom dziennika i Wywołaj odpowiednie `Log{LogLevel}` metody, aby kontrolować, ile danych wyjściowych dziennika jest zapisywana w określonym nośniku magazynowania.</span><span class="sxs-lookup"><span data-stu-id="2e86d-252">Configure the appropriate log level and call the correct `Log{LogLevel}` methods to control how much log output is written to a particular storage medium.</span></span> <span data-ttu-id="2e86d-253">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="2e86d-253">For example:</span></span>

- <span data-ttu-id="2e86d-254">W środowisku produkcyjnym:</span><span class="sxs-lookup"><span data-stu-id="2e86d-254">In production:</span></span>
  - <span data-ttu-id="2e86d-255">Rejestrowanie na poziomie `Trace` lub `Information` powoduje utworzenie dużej ilości szczegółowych komunikatów dziennika.</span><span class="sxs-lookup"><span data-stu-id="2e86d-255">Logging at the `Trace` or `Information` levels produces a high-volume of detailed log messages.</span></span> <span data-ttu-id="2e86d-256">Aby kontrolować koszty i nie przekraczać limitów magazynowania danych `Trace` , `Information` komunikaty dzienników i na poziomie magazynu o dużej ilości danych.</span><span class="sxs-lookup"><span data-stu-id="2e86d-256">To control costs and not exceed data storage limits, log `Trace` and `Information` level messages to a high-volume, low-cost data store.</span></span> <span data-ttu-id="2e86d-257">Rozważ ograniczenie `Trace` i `Information` do określonych kategorii.</span><span class="sxs-lookup"><span data-stu-id="2e86d-257">Consider limiting `Trace` and `Information` to specific categories.</span></span>
  - <span data-ttu-id="2e86d-258">Rejestrowanie przy `Warning` użyciu `Critical` poziomów powinno generować kilka komunikatów dziennika.</span><span class="sxs-lookup"><span data-stu-id="2e86d-258">Logging at `Warning` through `Critical` levels should produce few log messages.</span></span>
    - <span data-ttu-id="2e86d-259">Koszty i limity magazynu zazwyczaj nie są przedmiotem obaw.</span><span class="sxs-lookup"><span data-stu-id="2e86d-259">Costs and storage limits usually aren't a concern.</span></span>
    - <span data-ttu-id="2e86d-260">Niektóre dzienniki zapewniają większą elastyczność w zakresie wyboru magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="2e86d-260">Few logs allow more flexibility in data store choices.</span></span>
- <span data-ttu-id="2e86d-261">W programie Development:</span><span class="sxs-lookup"><span data-stu-id="2e86d-261">In development:</span></span>
  - <span data-ttu-id="2e86d-262">Ustaw wartość `Warning`.</span><span class="sxs-lookup"><span data-stu-id="2e86d-262">Set to `Warning`.</span></span>
  - <span data-ttu-id="2e86d-263">Dodawanie `Trace` lub `Information` komunikaty podczas rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="2e86d-263">Add `Trace` or `Information` messages when troubleshooting.</span></span> <span data-ttu-id="2e86d-264">Aby ograniczyć ilość danych wyjściowych, ustaw `Trace` lub `Information` tylko dla kategorii poddawanych badaniu.</span><span class="sxs-lookup"><span data-stu-id="2e86d-264">To limit output, set `Trace` or `Information` only for the categories under investigation.</span></span>

<span data-ttu-id="2e86d-265">Następujące zestawy JSON `Logging:Console:LogLevel:Microsoft:Information` :</span><span class="sxs-lookup"><span data-stu-id="2e86d-265">The following JSON sets `Logging:Console:LogLevel:Microsoft:Information`:</span></span>

:::code language="json" source="snippets/configuration/worker-service/appsettings.MSFT.json":::

## <a name="log-event-id"></a><span data-ttu-id="2e86d-266">Identyfikator zdarzenia dziennika</span><span class="sxs-lookup"><span data-stu-id="2e86d-266">Log event ID</span></span>

<span data-ttu-id="2e86d-267">Każdy dziennik może określać _event identyfikator \*, <xref:Microsoft.Extensions.Logging.EventId> jest strukturą z `Id` i opcjonalnymi `Name` właściwościami tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="2e86d-267">Each log can specify an _event identifer\*, the <xref:Microsoft.Extensions.Logging.EventId> is a structure with an `Id` and optional `Name` readonly properties.</span></span> <span data-ttu-id="2e86d-268">Przykładowy kod źródłowy używa `AppLogEvents` klasy do definiowania identyfikatorów zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="2e86d-268">The sample source code uses the `AppLogEvents` class to define event IDs:</span></span>

```csharp
internal static class AppLogEvents
{
    internal const int Create = 1000;
    internal const int Read = 1001;
    internal const int Update = 1002;
    internal const int Delete = 1003;

    internal const int Details = 3000;
    internal const int Error = 3001;

    internal const int ReadNotFound = 4000;
    internal const int UpdateNotFound = 4001;

    // ...
}
```

<span data-ttu-id="2e86d-269">Identyfikator zdarzenia kojarzy zestaw zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="2e86d-269">An event ID associates a set of events.</span></span> <span data-ttu-id="2e86d-270">Na przykład wszystkie dzienniki związane z odczytem wartości z repozytorium mogą być `1001` .</span><span class="sxs-lookup"><span data-stu-id="2e86d-270">For example, all logs related to reading values from a repository might be `1001`.</span></span>

<span data-ttu-id="2e86d-271">Dostawca rejestrowania może rejestrować identyfikator zdarzenia w polu identyfikatora, w komunikacie rejestrowania lub wcale.</span><span class="sxs-lookup"><span data-stu-id="2e86d-271">The logging provider may log the event ID in an ID field, in the logging message, or not at all.</span></span> <span data-ttu-id="2e86d-272">Dostawca debugowania nie pokazuje identyfikatorów zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="2e86d-272">The Debug provider doesn't show event IDs.</span></span> <span data-ttu-id="2e86d-273">Dostawca konsoli pokazuje identyfikatory zdarzeń w nawiasach po kategorii:</span><span class="sxs-lookup"><span data-stu-id="2e86d-273">The console provider shows event IDs in brackets after the category:</span></span>

```console
info: Example.DefaultService.GetAsync[1001]
      Reading value for a1b2c3
warn: Example.DefaultService.GetAsync[4000]
      GetAsync(a1b2c3) not found
```

<span data-ttu-id="2e86d-274">Niektórzy dostawcy rejestrowania przechowują identyfikator zdarzenia w polu, co umożliwia filtrowanie identyfikatorów.</span><span class="sxs-lookup"><span data-stu-id="2e86d-274">Some logging providers store the event ID in a field, which allows for filtering on the ID.</span></span>

## <a name="log-message-template"></a><span data-ttu-id="2e86d-275">Szablon komunikatu dziennika</span><span class="sxs-lookup"><span data-stu-id="2e86d-275">Log message template</span></span>

<span data-ttu-id="2e86d-276">Każdy interfejs API dziennika używa szablonu wiadomości.</span><span class="sxs-lookup"><span data-stu-id="2e86d-276">Each log API uses a message template.</span></span> <span data-ttu-id="2e86d-277">Szablon wiadomości może zawierać symbole zastępcze, dla których podano argumenty.</span><span class="sxs-lookup"><span data-stu-id="2e86d-277">The message template can contain placeholders for which arguments are provided.</span></span> <span data-ttu-id="2e86d-278">Użyj nazw dla symboli zastępczych, a nie liczby.</span><span class="sxs-lookup"><span data-stu-id="2e86d-278">Use names for the placeholders, not numbers.</span></span> <span data-ttu-id="2e86d-279">Kolejność symboli zastępczych, nie ich nazw, określa, które parametry są używane do dostarczania ich wartości.</span><span class="sxs-lookup"><span data-stu-id="2e86d-279">The order of placeholders, not their names, determines which parameters are used to provide their values.</span></span> <span data-ttu-id="2e86d-280">W poniższym kodzie nazwy parametrów są spoza sekwencji w szablonie wiadomości:</span><span class="sxs-lookup"><span data-stu-id="2e86d-280">In the following code, the parameter names are out of sequence in the message template:</span></span>

```csharp
string p1 = "param1";
string p2 = "param2";
_logger.LogInformation("Parameter values: {p2}, {p1}", p1, p2);
```

<span data-ttu-id="2e86d-281">Poprzedni kod tworzy komunikat dziennika z wartościami parametrów w kolejności:</span><span class="sxs-lookup"><span data-stu-id="2e86d-281">The preceding code creates a log message with the parameter values in sequence:</span></span>

```text
Parameter values: param1, param2
```

<span data-ttu-id="2e86d-282">Takie podejście umożliwia dostawcom rejestrowania implementowanie [semantyki lub rejestrowania strukturalnego](https://github.com/NLog/NLog/wiki/How-to-use-structured-logging).</span><span class="sxs-lookup"><span data-stu-id="2e86d-282">This approach allows logging providers to implement [semantic or structured logging](https://github.com/NLog/NLog/wiki/How-to-use-structured-logging).</span></span> <span data-ttu-id="2e86d-283">Same argumenty są przesyłane do systemu rejestrowania, a nie tylko dla sformatowanego szablonu wiadomości.</span><span class="sxs-lookup"><span data-stu-id="2e86d-283">The arguments themselves are passed to the logging system, not just the formatted message template.</span></span> <span data-ttu-id="2e86d-284">Umożliwia to dostawcom rejestrowania przechowywanie wartości parametrów jako pól.</span><span class="sxs-lookup"><span data-stu-id="2e86d-284">This enables logging providers to store the parameter values as fields.</span></span> <span data-ttu-id="2e86d-285">Rozważmy następujące metody rejestrowania:</span><span class="sxs-lookup"><span data-stu-id="2e86d-285">Consider the following logger method:</span></span>

```csharp
_logger.LogInformation("Getting item {Id} at {RunTime}", id, DateTime.Now);
```

<span data-ttu-id="2e86d-286">Na przykład podczas rejestrowania w usłudze Azure Table Storage:</span><span class="sxs-lookup"><span data-stu-id="2e86d-286">For example, when logging to Azure Table Storage:</span></span>

- <span data-ttu-id="2e86d-287">Każda jednostka tabeli platformy Azure może `ID` mieć `RunTime` właściwości i.</span><span class="sxs-lookup"><span data-stu-id="2e86d-287">Each Azure Table entity can have `ID` and `RunTime` properties.</span></span>
- <span data-ttu-id="2e86d-288">Tabele z właściwościami upraszczają zapytania dotyczące zarejestrowanych danych.</span><span class="sxs-lookup"><span data-stu-id="2e86d-288">Tables with properties simplify queries on logged data.</span></span> <span data-ttu-id="2e86d-289">Na przykład zapytanie może znaleźć wszystkie dzienniki w określonym `RunTime` zakresie bez konieczności analizowania limitu czasu wiadomości tekstowej.</span><span class="sxs-lookup"><span data-stu-id="2e86d-289">For example, a query can find all logs within a particular `RunTime` range without having to parse the time out of the text message.</span></span>

## <a name="log-exceptions"></a><span data-ttu-id="2e86d-290">Rejestrowanie wyjątków</span><span class="sxs-lookup"><span data-stu-id="2e86d-290">Log exceptions</span></span>

<span data-ttu-id="2e86d-291">Metody rejestratora mają przeciążenia przyjmujące parametr wyjątku:</span><span class="sxs-lookup"><span data-stu-id="2e86d-291">The logger methods have overloads that take an exception parameter:</span></span>

```csharp
public void Test(string id)
{
    try
    {
        if (id == "none")
        {
            throw new Exception("Default Id detected.");
        }
    }
    catch (Exception ex)
    {
        _logger.LogWarning(
            AppLogEvents.Error, ex,
            "Failed to process iteration: {Id}", id)
    }
}
```

<span data-ttu-id="2e86d-292">Rejestrowanie wyjątków jest specyficzne dla dostawcy.</span><span class="sxs-lookup"><span data-stu-id="2e86d-292">Exception logging is provider-specific.</span></span>

### <a name="default-log-level"></a><span data-ttu-id="2e86d-293">Domyślny poziom dziennika</span><span class="sxs-lookup"><span data-stu-id="2e86d-293">Default log level</span></span>

<span data-ttu-id="2e86d-294">Jeśli domyślny poziom rejestrowania nie jest ustawiony, domyślna wartość poziomu dziennika to `Information` .</span><span class="sxs-lookup"><span data-stu-id="2e86d-294">If the default log level is not set, the default log level value is `Information`.</span></span>

<span data-ttu-id="2e86d-295">Rozważmy na przykład następującą aplikację usługi Worker:</span><span class="sxs-lookup"><span data-stu-id="2e86d-295">For example, consider the following worker service app:</span></span>

- <span data-ttu-id="2e86d-296">Utworzono za pomocą szablonów procesów roboczych platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="2e86d-296">Created with the .NET Worker templates.</span></span>
- <span data-ttu-id="2e86d-297">*appsettings.json* i *appsettings.Development.jspo* usunięciu lub zmianie nazwy.</span><span class="sxs-lookup"><span data-stu-id="2e86d-297">*appsettings.json* and *appsettings.Development.json* deleted or renamed.</span></span>

<span data-ttu-id="2e86d-298">Po powyższej instalacji przechodzenie do strony prywatność lub Strona główna powoduje utworzenie wielu `Trace` , `Debug` i `Information`  komunikatów z `Microsoft` nazwą kategorii.</span><span class="sxs-lookup"><span data-stu-id="2e86d-298">With the preceding setup, navigating to the privacy or home page produces many `Trace`, `Debug`, and `Information`  messages with `Microsoft` in the category name.</span></span>

<span data-ttu-id="2e86d-299">Poniższy kod ustawia domyślny poziom rejestrowania, jeśli domyślny poziom rejestrowania nie jest ustawiony w konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="2e86d-299">The following code sets the default log level when the default log level is not set in configuration:</span></span>

```csharp
class Program
{
    static Task Main(string[] args) =>
        CreateHostBuilder(args).Build().RunAsync();

    static IHostBuilder CreateHostBuilder(string[] args) =>
        Host.CreateDefaultBuilder(args)
            .ConfigureLogging(logging => logging.SetMinimumLevel(LogLevel.Warning));
}
```

### <a name="filter-function"></a><span data-ttu-id="2e86d-300">Funkcja filtrowania</span><span class="sxs-lookup"><span data-stu-id="2e86d-300">Filter function</span></span>

<span data-ttu-id="2e86d-301">Funkcja filtru jest wywoływana dla wszystkich dostawców i kategorii, które nie mają przypisanych do nich reguł przez konfigurację lub kod:</span><span class="sxs-lookup"><span data-stu-id="2e86d-301">A filter function is invoked for all providers and categories that don't have rules assigned to them by configuration or code:</span></span>

```csharp
class Program
{
    static Task Main(string[] args) =>
        CreateHostBuilder(args).Build().RunAsync();

    static IHostBuilder CreateHostBuilder(string[] args) =>
        Host.CreateDefaultBuilder(args)
            .ConfigureLogging(logging =>
                logging.AddFilter((provider, category, logLevel) =>
                {
                    return provider.Contains("ConsoleLoggerProvider")
                        && (category.Contains("Example") || category.Contains("Microsoft"))
                        && logLevel >= LogLevel.Information;
                }));
}
```

<span data-ttu-id="2e86d-302">Poprzedni kod wyświetla dzienniki konsoli, gdy kategoria zawiera `Example` lub `Microsoft` i poziom dziennika jest `Information` lub wyższy.</span><span class="sxs-lookup"><span data-stu-id="2e86d-302">The preceding code displays console logs when the category contains `Example` or `Microsoft` and the log level is `Information` or higher.</span></span>

## <a name="log-scopes"></a><span data-ttu-id="2e86d-303">Zakresy dziennika</span><span class="sxs-lookup"><span data-stu-id="2e86d-303">Log scopes</span></span>

 <span data-ttu-id="2e86d-304">*Zakres* może grupować zestaw operacji logicznych.</span><span class="sxs-lookup"><span data-stu-id="2e86d-304">A *scope* can group a set of logical operations.</span></span> <span data-ttu-id="2e86d-305">Takie grupowanie może służyć do dołączania tych samych danych do każdego dziennika, który został utworzony jako część zestawu.</span><span class="sxs-lookup"><span data-stu-id="2e86d-305">This grouping can be used to attach the same data to each log that's created as part of a set.</span></span> <span data-ttu-id="2e86d-306">Na przykład każdy dziennik utworzony w ramach przetwarzania transakcji może zawierać identyfikator transakcji.</span><span class="sxs-lookup"><span data-stu-id="2e86d-306">For example, every log created as part of processing a transaction can include the transaction ID.</span></span>

<span data-ttu-id="2e86d-307">Zakres:</span><span class="sxs-lookup"><span data-stu-id="2e86d-307">A scope:</span></span>

- <span data-ttu-id="2e86d-308">Jest <xref:System.IDisposable> typem zwracanym przez <xref:Microsoft.Extensions.Logging.ILogger.BeginScope%2A> metodę.</span><span class="sxs-lookup"><span data-stu-id="2e86d-308">Is an <xref:System.IDisposable> type that's returned by the <xref:Microsoft.Extensions.Logging.ILogger.BeginScope%2A> method.</span></span>
- <span data-ttu-id="2e86d-309">Obowiązuje do momentu jego usunięcia.</span><span class="sxs-lookup"><span data-stu-id="2e86d-309">Lasts until it's disposed.</span></span>

<span data-ttu-id="2e86d-310">Następujące dostawcy obsługują zakresy:</span><span class="sxs-lookup"><span data-stu-id="2e86d-310">The following providers support scopes:</span></span>

- `Console`
- [<span data-ttu-id="2e86d-311">AzureAppServicesFile i AzureAppServicesBlob</span><span class="sxs-lookup"><span data-stu-id="2e86d-311">AzureAppServicesFile and AzureAppServicesBlob</span></span>](xref:Microsoft.Extensions.Logging.AzureAppServices.BatchingLoggerOptions.IncludeScopes)

<span data-ttu-id="2e86d-312">Użyj zakresu przez Zawijanie wywołań rejestratora w `using` bloku:</span><span class="sxs-lookup"><span data-stu-id="2e86d-312">Use a scope by wrapping logger calls in a `using` block:</span></span>

```csharp
public async Task<T> GetAsync<T>(string id)
{
    T result;

    using (_logger.BeginScope("using block message"))
    {
        _logger.LogInformation(
            AppLogEvents.Read, "Reading value for {Id}", id);

        var result = await _repository.GetAsync(id);
        if (result is null)
        {
            _logger.LogWarning(
                AppLogEvents.ReadNotFound, "GetAsync({Id}) not found", id);
        }
    }

    return result;
}
```

<span data-ttu-id="2e86d-313">Poniższy kod JSON włącza zakresy dla dostawcy konsoli:</span><span class="sxs-lookup"><span data-stu-id="2e86d-313">The following JSON enables scopes for the console provider:</span></span>

:::code language="json" source="snippets/configuration/worker-service/appsettings.IncludeScopes.json" highlight="9":::

<span data-ttu-id="2e86d-314">Poniższy kod włącza zakresy dla dostawcy konsoli:</span><span class="sxs-lookup"><span data-stu-id="2e86d-314">The following code enables scopes for the console provider:</span></span>

```csharp
class Program
{
    static Task Main(string[] args) =>
        CreateHostBuilder(args).Build().RunAsync();

    static IHostBuilder CreateHostBuilder(string[] args) =>
        Host.CreateDefaultBuilder(args)
            .ConfigureLogging((_, logging) =>
                logging.ClearProviders()
                    .AddConsole(options => options.IncludeScopes = true));
}
```

## <a name="non-host-console-app"></a><span data-ttu-id="2e86d-315">Aplikacja konsolowa niebędąca hostem</span><span class="sxs-lookup"><span data-stu-id="2e86d-315">Non-host console app</span></span>

<span data-ttu-id="2e86d-316">Rejestrowanie kodu dla aplikacji, które nie jest [hostem ogólnym](generic-host.md) , różni się w sposób, w jaki [są dodawane dostawcy](logging-providers.md#built-in-logging-providers) i [są tworzone rejestratory](#create-logs).</span><span class="sxs-lookup"><span data-stu-id="2e86d-316">Logging code for apps without a [Generic Host](generic-host.md) differs in the way [providers are added](logging-providers.md#built-in-logging-providers) and [loggers are created](#create-logs).</span></span> <span data-ttu-id="2e86d-317">W aplikacji konsolowej innej niż host Wywołaj `Add{provider name}` metodę rozszerzenia dostawcy podczas tworzenia `LoggerFactory` :</span><span class="sxs-lookup"><span data-stu-id="2e86d-317">In a non-host console app, call the provider's `Add{provider name}` extension method while creating a `LoggerFactory`:</span></span>

```csharp
class Program
{
    static void Main(string[] args)
    {
        using var loggerFactory = LoggerFactory.Create(builder =>
        {
            builder
                .AddFilter("Microsoft", LogLevel.Warning)
                .AddFilter("System", LogLevel.Warning)
                .AddFilter("LoggingConsoleApp.Program", LogLevel.Debug)
                .AddConsole();
        });

        ILogger logger = loggerFactory.CreateLogger<Program>();
        logger.LogInformation("Example log message");
    }
}
```

<span data-ttu-id="2e86d-318">`loggerFactory`Obiekt jest używany do tworzenia <xref:Microsoft.Extensions.Logging.ILogger> wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="2e86d-318">The `loggerFactory` object is used to create an <xref:Microsoft.Extensions.Logging.ILogger> instance.</span></span>

## <a name="create-logs-in-main"></a><span data-ttu-id="2e86d-319">Tworzenie dzienników w głównej</span><span class="sxs-lookup"><span data-stu-id="2e86d-319">Create logs in Main</span></span>

<span data-ttu-id="2e86d-320">Następujący kod jest zarejestrowana `Main` przez pobranie `ILogger` wystąpienia z programu di po skompilowaniu hosta:</span><span class="sxs-lookup"><span data-stu-id="2e86d-320">The following code logs in `Main` by getting an `ILogger` instance from DI after building the host:</span></span>

```csharp
using System;
using System.Threading.Tasks;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
using Microsoft.Extensions.Logging;

class Program
{
    static Task Main(string[] args)
    {
        IHost host = Host.CreateDefaultBuilder(args).Build();

        var logger = host.Services.GetRequiredService<ILogger<Program>>();
        logger.LogInformation("Host created.");

        return host.RunAsync();
    }
}
```

### <a name="no-asynchronous-logger-methods"></a><span data-ttu-id="2e86d-321">Brak metod rejestratora asynchronicznego</span><span class="sxs-lookup"><span data-stu-id="2e86d-321">No asynchronous logger methods</span></span>

<span data-ttu-id="2e86d-322">Rejestracja powinna być tak szybka, że nie jest to koszt wydajności kodu asynchronicznego.</span><span class="sxs-lookup"><span data-stu-id="2e86d-322">Logging should be so fast that it isn't worth the performance cost of asynchronous code.</span></span> <span data-ttu-id="2e86d-323">Jeśli magazyn danych rejestrowania jest wolny, nie zapisuj go bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="2e86d-323">If a logging data store is slow, don't write to it directly.</span></span> <span data-ttu-id="2e86d-324">Rozważ ręczne zapisanie komunikatów dziennika w szybkim magazynie, a następnie przeniesienie ich do wolnego magazynu później.</span><span class="sxs-lookup"><span data-stu-id="2e86d-324">Consider writing the log messages to a fast store initially, then moving them to the slow store later.</span></span> <span data-ttu-id="2e86d-325">Na przykład podczas rejestrowania do SQL Server nie należy tego robić bezpośrednio w `Log` metodzie, ponieważ `Log` metody są synchroniczne.</span><span class="sxs-lookup"><span data-stu-id="2e86d-325">For example, when logging to SQL Server, don't do so directly in a `Log` method, since the `Log` methods are synchronous.</span></span> <span data-ttu-id="2e86d-326">Zamiast tego można synchronicznie dodawać komunikaty dziennika do kolejki w pamięci, a proces roboczy w tle ściągał komunikaty z kolejki, aby wykonać asynchroniczne działanie wypychania danych do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2e86d-326">Instead, synchronously add log messages to an in-memory queue and have a background worker pull the messages out of the queue to do the asynchronous work of pushing data to SQL Server.</span></span>

## <a name="change-log-levels-in-a-running-app"></a><span data-ttu-id="2e86d-327">Zmień poziomy dziennika w działającej aplikacji</span><span class="sxs-lookup"><span data-stu-id="2e86d-327">Change log levels in a running app</span></span>

<span data-ttu-id="2e86d-328">Interfejs API rejestrowania nie zawiera scenariusza zmiany poziomów rejestrowania, gdy aplikacja jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="2e86d-328">The Logging API doesn't include a scenario to change log levels while an app is running.</span></span> <span data-ttu-id="2e86d-329">Niektórzy dostawcy konfiguracji mogą jednak ponownie ładować konfigurację, która zacznie natychmiastowo wpływać na konfigurację rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="2e86d-329">However, some configuration providers are capable of reloading configuration, which takes immediate effect on logging configuration.</span></span> <span data-ttu-id="2e86d-330">Na przykład [dostawca konfiguracji plików](configuration-providers.md#file-configuration-provider) ponownie ładuje konfigurację rejestrowania domyślnie.</span><span class="sxs-lookup"><span data-stu-id="2e86d-330">For example, the [File Configuration Provider](configuration-providers.md#file-configuration-provider) reloads logging configuration by default.</span></span> <span data-ttu-id="2e86d-331">Jeśli konfiguracja zostanie zmieniona w kodzie w czasie, gdy aplikacja jest uruchomiona, aplikacja może wywołać [IConfigurationRoot. reload](xref:Microsoft.Extensions.Configuration.IConfigurationRoot.Reload%2A) , aby zaktualizować konfigurację rejestrowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2e86d-331">If configuration is changed in code while an app is running, the app can call [IConfigurationRoot.Reload](xref:Microsoft.Extensions.Configuration.IConfigurationRoot.Reload%2A) to update the app's logging configuration.</span></span>

## <a name="nuget-packages"></a><span data-ttu-id="2e86d-332">Pakiety NuGet</span><span class="sxs-lookup"><span data-stu-id="2e86d-332">NuGet packages</span></span>

<span data-ttu-id="2e86d-333"><xref:Microsoft.Extensions.Logging.ILogger%601>Interfejsy i <xref:Microsoft.Extensions.Logging.ILoggerFactory> i implementacje są zawarte w zestaw .NET Core SDK.</span><span class="sxs-lookup"><span data-stu-id="2e86d-333">The <xref:Microsoft.Extensions.Logging.ILogger%601> and <xref:Microsoft.Extensions.Logging.ILoggerFactory> interfaces and implementations are included in the .NET Core SDK.</span></span> <span data-ttu-id="2e86d-334">Są one również dostępne w następujących pakietach NuGet:</span><span class="sxs-lookup"><span data-stu-id="2e86d-334">They are also available in the following NuGet packages:</span></span>

- <span data-ttu-id="2e86d-335">Interfejsy są w [Microsoft. Extensions. Logging. Abstracts](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Abstractions).</span><span class="sxs-lookup"><span data-stu-id="2e86d-335">The interfaces are in [Microsoft.Extensions.Logging.Abstractions](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Abstractions).</span></span>
- <span data-ttu-id="2e86d-336">Implementacje domyślne są w [Microsoft. Extensions. Logging](https://www.nuget.org/packages/microsoft.extensions.logging).</span><span class="sxs-lookup"><span data-stu-id="2e86d-336">The default implementations are in [Microsoft.Extensions.Logging](https://www.nuget.org/packages/microsoft.extensions.logging).</span></span>

## <a name="apply-log-filter-rules-in-code"></a><span data-ttu-id="2e86d-337">Zastosuj reguły filtru dziennika w kodzie</span><span class="sxs-lookup"><span data-stu-id="2e86d-337">Apply log filter rules in code</span></span>

<span data-ttu-id="2e86d-338">Preferowanym podejściem do ustawiania reguł filtru dziennika jest użycie [konfiguracji](configuration.md).</span><span class="sxs-lookup"><span data-stu-id="2e86d-338">The preferred approach for setting log filter rules is by using [Configuration](configuration.md).</span></span>

<span data-ttu-id="2e86d-339">Poniższy przykład pokazuje, jak zarejestrować reguły filtru w kodzie:</span><span class="sxs-lookup"><span data-stu-id="2e86d-339">The following example shows how to register filter rules in code:</span></span>

```csharp
class Program
{
    static Task Main(string[] args) =>
        CreateHostBuilder(args).Build().RunAsync();

    static IHostBuilder CreateHostBuilder(string[] args) =>
        Host.CreateDefaultBuilder(args)
            .ConfigureLogging(logging =>
               logging.AddFilter("System", LogLevel.Debug)
                  .AddFilter<DebugLoggerProvider>("Microsoft", LogLevel.Information)
                  .AddFilter<ConsoleLoggerProvider>("Microsoft", LogLevel.Trace));
}
```

<span data-ttu-id="2e86d-340">`logging.AddFilter("System", LogLevel.Debug)` Określa `System` kategorię i poziom dziennika `Debug` .</span><span class="sxs-lookup"><span data-stu-id="2e86d-340">`logging.AddFilter("System", LogLevel.Debug)` specifies the `System` category and log level `Debug`.</span></span> <span data-ttu-id="2e86d-341">Filtr jest stosowany do wszystkich dostawców, ponieważ określony dostawca nie został skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="2e86d-341">The filter is applied to all providers because a specific provider was not configured.</span></span>

<span data-ttu-id="2e86d-342">`AddFilter<DebugLoggerProvider>("Microsoft", LogLevel.Information)` określając</span><span class="sxs-lookup"><span data-stu-id="2e86d-342">`AddFilter<DebugLoggerProvider>("Microsoft", LogLevel.Information)` specifies:</span></span>

- <span data-ttu-id="2e86d-343">`Debug`Dostawca rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="2e86d-343">The `Debug` logging provider.</span></span>
- <span data-ttu-id="2e86d-344">Poziom dziennika `Information` lub wyższy.</span><span class="sxs-lookup"><span data-stu-id="2e86d-344">Log level `Information` and higher.</span></span>
- <span data-ttu-id="2e86d-345">Wszystkie kategorie zaczynające się od `"Microsoft"` .</span><span class="sxs-lookup"><span data-stu-id="2e86d-345">All categories starting with `"Microsoft"`.</span></span>

## <a name="see-also"></a><span data-ttu-id="2e86d-346">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="2e86d-346">See also</span></span>

- [<span data-ttu-id="2e86d-347">Dostawcy rejestrowania w programie .NET</span><span class="sxs-lookup"><span data-stu-id="2e86d-347">Logging providers in .NET</span></span>](logging-providers.md)
- [<span data-ttu-id="2e86d-348">Implementowanie niestandardowego dostawcy rejestrowania w programie .NET</span><span class="sxs-lookup"><span data-stu-id="2e86d-348">Implement a custom logging provider in .NET</span></span>](custom-logging-provider.md)
- [<span data-ttu-id="2e86d-349">Formatowanie dziennika konsoli</span><span class="sxs-lookup"><span data-stu-id="2e86d-349">Console log formatting</span></span>](console-log-formatter.md)
- [<span data-ttu-id="2e86d-350">Rejestrowanie o wysokiej wydajności w programie .NET</span><span class="sxs-lookup"><span data-stu-id="2e86d-350">High-performance logging in .NET</span></span>](high-performance-logging.md)
- <span data-ttu-id="2e86d-351">Błędy rejestrowania należy utworzyć w repozytorium [GitHub.com/dotnet/Extensions](https://github.com/dotnet/extensions/issues)</span><span class="sxs-lookup"><span data-stu-id="2e86d-351">Logging bugs should be created in the [github.com/dotnet/extensions](https://github.com/dotnet/extensions/issues) repo</span></span>
