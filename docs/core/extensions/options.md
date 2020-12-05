---
title: Wzorzec opcji w programie .NET
author: IEvangelist
description: Informacje na temat używania wzorca opcji do reprezentowania grup powiązanych ustawień w aplikacjach .NET.
ms.author: dapine
ms.date: 12/04/2020
ms.openlocfilehash: 76d99337c51920115a38c400daca1649d0e74a99
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96740019"
---
# <a name="options-pattern-in-net"></a><span data-ttu-id="f9301-103">Wzorzec opcji w programie .NET</span><span class="sxs-lookup"><span data-stu-id="f9301-103">Options pattern in .NET</span></span>

<span data-ttu-id="f9301-104">Wzorzec opcji używa klas, aby zapewnić dostęp z jednoznacznie określonym grupom ustawień pokrewnych.</span><span class="sxs-lookup"><span data-stu-id="f9301-104">The options pattern uses classes to provide strongly-typed access to groups of related settings.</span></span> <span data-ttu-id="f9301-105">Gdy [Ustawienia konfiguracji](configuration.md) są izolowane według scenariusza w osobnych klasach, aplikacja będzie zgodna z dwoma ważnymi zasadami inżynierii oprogramowania:</span><span class="sxs-lookup"><span data-stu-id="f9301-105">When [configuration settings](configuration.md) are isolated by scenario into separate classes, the app adheres to two important software engineering principles:</span></span>

- <span data-ttu-id="f9301-106">[Zasada segregowania interfejsu (ISP) lub hermetyzacja](../../architecture/modern-web-apps-azure/architectural-principles.md#encapsulation): scenariusze (klasy), które są zależne od ustawień konfiguracji, zależą tylko od ustawień konfiguracji, których używają.</span><span class="sxs-lookup"><span data-stu-id="f9301-106">The [Interface Segregation Principle (ISP) or Encapsulation](../../architecture/modern-web-apps-azure/architectural-principles.md#encapsulation): Scenarios (classes) that depend on configuration settings depend only on the configuration settings that they use.</span></span>
- <span data-ttu-id="f9301-107">[Separacja obaw](../../architecture/modern-web-apps-azure/architectural-principles.md#separation-of-concerns): ustawienia dla różnych części aplikacji nie są zależne ani powiązane ze sobą.</span><span class="sxs-lookup"><span data-stu-id="f9301-107">[Separation of Concerns](../../architecture/modern-web-apps-azure/architectural-principles.md#separation-of-concerns): Settings for different parts of the app aren't dependent or coupled to one another.</span></span>

<span data-ttu-id="f9301-108">Opcje umożliwiają również mechanizm weryfikacji danych konfiguracyjnych.</span><span class="sxs-lookup"><span data-stu-id="f9301-108">Options also provide a mechanism to validate configuration data.</span></span> <span data-ttu-id="f9301-109">Aby uzyskać więcej informacji, zobacz sekcję [Opcje walidacji](#options-validation) .</span><span class="sxs-lookup"><span data-stu-id="f9301-109">For more information, see the [Options validation](#options-validation) section.</span></span>

## <a name="bind-hierarchical-configuration"></a><span data-ttu-id="f9301-110">Powiąż hierarchiczną konfigurację</span><span class="sxs-lookup"><span data-stu-id="f9301-110">Bind hierarchical configuration</span></span>

<span data-ttu-id="f9301-111">Preferowanym sposobem odczytywania pokrewnych wartości konfiguracji jest użycie wzorca opcji.</span><span class="sxs-lookup"><span data-stu-id="f9301-111">The preferred way to read related configuration values is using the options pattern.</span></span> <span data-ttu-id="f9301-112">Na przykład, aby odczytać następujące wartości konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="f9301-112">For example, to read the following configuration values:</span></span>

:::code language="json" source="snippets/configuration/console-json/appsettings.json" range="3-6":::

<span data-ttu-id="f9301-113">Utwórz następującą `TransientFaultHandlingOptions` klasę:</span><span class="sxs-lookup"><span data-stu-id="f9301-113">Create the following `TransientFaultHandlingOptions` class:</span></span>

:::code language="csharp" source="snippets/configuration/console-json/TransientFaultHandlingOptions.cs" range="5-6":::

<span data-ttu-id="f9301-114">Klasa opcji:</span><span class="sxs-lookup"><span data-stu-id="f9301-114">An options class:</span></span>

* <span data-ttu-id="f9301-115">Nie może być abstrakcyjny z publicznym konstruktorem bez parametrów</span><span class="sxs-lookup"><span data-stu-id="f9301-115">Must be non-abstract with a public parameterless constructor</span></span>
* <span data-ttu-id="f9301-116">Zawierają publiczne właściwości odczytu i zapisu do powiązania (pola \*\*są \*\*\* niepowiązane)</span><span class="sxs-lookup"><span data-stu-id="f9301-116">Contain public read-write properties to bind (fields are \***not** _ bound)</span></span>

<span data-ttu-id="f9301-117">Następujący kod:</span><span class="sxs-lookup"><span data-stu-id="f9301-117">The following code:</span></span>

<span data-ttu-id="f9301-118">_ Wywołuje [ConfigurationBinder. bind](xref:Microsoft.Extensions.Configuration.ConfigurationBinder.Bind%2A) , aby powiązać `TransientFaultHandlingOptions` klasę z `"TransientFaultHandlingOptions"` sekcją.</span><span class="sxs-lookup"><span data-stu-id="f9301-118">_ Calls [ConfigurationBinder.Bind](xref:Microsoft.Extensions.Configuration.ConfigurationBinder.Bind%2A) to bind the `TransientFaultHandlingOptions` class to the `"TransientFaultHandlingOptions"` section.</span></span>
* <span data-ttu-id="f9301-119">Wyświetla dane konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f9301-119">Displays the configuration data.</span></span>

:::code language="csharp" source="snippets/configuration/console-json/Program.cs" range="31-38":::

<span data-ttu-id="f9301-120">W poprzednim kodzie zmiany w pliku konfiguracji JSON po rozpoczęciu aplikacji są odczytywane.</span><span class="sxs-lookup"><span data-stu-id="f9301-120">In the preceding code, changes to the JSON configuration file after the app has started are read.</span></span>

<span data-ttu-id="f9301-121">[`ConfigurationBinder.Get<T>`](xref:Microsoft.Extensions.Configuration.ConfigurationBinder.Get%2A) tworzy powiązania i zwraca określony typ.</span><span class="sxs-lookup"><span data-stu-id="f9301-121">[`ConfigurationBinder.Get<T>`](xref:Microsoft.Extensions.Configuration.ConfigurationBinder.Get%2A) binds and returns the specified type.</span></span> <span data-ttu-id="f9301-122">`ConfigurationBinder.Get<T>` może być wygodniejsze niż używanie `ConfigurationBinder.Bind` .</span><span class="sxs-lookup"><span data-stu-id="f9301-122">`ConfigurationBinder.Get<T>` may be more convenient than using `ConfigurationBinder.Bind`.</span></span> <span data-ttu-id="f9301-123">Poniższy kod przedstawia sposób użycia `ConfigurationBinder.Get<T>` z `TransientFaultHandlingOptions` klasą:</span><span class="sxs-lookup"><span data-stu-id="f9301-123">The following code shows how to use `ConfigurationBinder.Get<T>` with the `TransientFaultHandlingOptions` class:</span></span>

```csharp
IConfigurationRoot configurationRoot = configuration.Build();

var options =
    configurationRoot.GetSection(nameof(TransientFaultHandlingOptions))
        .Get<TransientFaultHandlingOptions>();

Console.WriteLine($"TransientFaultHandlingOptions.Enabled={options.Enabled}");
Console.WriteLine($"TransientFaultHandlingOptions.AutoRetryDelay={options.AutoRetryDelay}");
```

<span data-ttu-id="f9301-124">W poprzednim kodzie zmiany w pliku konfiguracji JSON po rozpoczęciu aplikacji są odczytywane.</span><span class="sxs-lookup"><span data-stu-id="f9301-124">In the preceding code, changes to the JSON configuration file after the app has started are read.</span></span>

<span data-ttu-id="f9301-125">Alternatywne podejście w przypadku używania wzorca opcji ma na celu powiązanie `"TransientFaultHandlingOptions"` sekcji i dodanie jej do [kontenera usługi iniekcji zależności](dependency-injection.md).</span><span class="sxs-lookup"><span data-stu-id="f9301-125">An alternative approach when using the options pattern is to bind the `"TransientFaultHandlingOptions"` section and add it to the [dependency injection service container](dependency-injection.md).</span></span> <span data-ttu-id="f9301-126">W poniższym kodzie `TransientFaultHandlingOptions` został dodany do kontenera usługi z <xref:Microsoft.Extensions.DependencyInjection.OptionsConfigurationServiceCollectionExtensions.Configure%2A> i powiązana z konfiguracją:</span><span class="sxs-lookup"><span data-stu-id="f9301-126">In the following code, `TransientFaultHandlingOptions` is added to the service container with <xref:Microsoft.Extensions.DependencyInjection.OptionsConfigurationServiceCollectionExtensions.Configure%2A> and bound to configuration:</span></span>

```csharp
services.Configure<TransientFaultHandlingOptions>(
    configurationRoot.GetSection(
        key: nameof(TransientFaultHandlingOptions)));
```

> [!TIP]
> <span data-ttu-id="f9301-127">`key`Parametr jest nazwą sekcji konfiguracji do wyszukania.</span><span class="sxs-lookup"><span data-stu-id="f9301-127">The `key` parameter is the name of the configuration section to search for.</span></span> <span data-ttu-id="f9301-128">*Nie musi być* zgodna z nazwą typu, który go reprezentuje.</span><span class="sxs-lookup"><span data-stu-id="f9301-128">It does *not* have to match the name of the type that represents it.</span></span> <span data-ttu-id="f9301-129">Na przykład można mieć sekcję o nazwie `"FaultHandling"` i może być reprezentowana przez `TransientFaultHandlingOptions` klasę.</span><span class="sxs-lookup"><span data-stu-id="f9301-129">For example, you could have a section named `"FaultHandling"` and it could be represented by the `TransientFaultHandlingOptions` class.</span></span> <span data-ttu-id="f9301-130">W tym przypadku zamiast tego przejdziesz `"FaultHandling"` do <xref:Microsoft.Extensions.Configuration.IConfiguration.GetSection%2A> funkcji.</span><span class="sxs-lookup"><span data-stu-id="f9301-130">In this instance, you'd pass `"FaultHandling"` to the <xref:Microsoft.Extensions.Configuration.IConfiguration.GetSection%2A> function instead.</span></span> <span data-ttu-id="f9301-131">`nameof`Operator jest używany jako wygoda, gdy nazwana sekcja pasuje do typu, do którego odnosi się.</span><span class="sxs-lookup"><span data-stu-id="f9301-131">The `nameof` operator is used as a convenience when the named section matches the type it corresponds to.</span></span>

<span data-ttu-id="f9301-132">Korzystając z powyższego kodu, poniższy kod odczytuje opcje pozycji:</span><span class="sxs-lookup"><span data-stu-id="f9301-132">Using the preceding code, the following code reads the position options:</span></span>

:::code language="csharp" source="snippets/configuration/console-json/ExampleService.cs":::

<span data-ttu-id="f9301-133">W powyższym kodzie zmiany w pliku konfiguracji JSON po rozpoczęciu aplikacji \*\*są \*\*\* nie_.</span><span class="sxs-lookup"><span data-stu-id="f9301-133">In the preceding code, changes to the JSON configuration file after the app has started are \***not** _ read.</span></span> <span data-ttu-id="f9301-134">Aby odczytać zmiany po rozpoczęciu pracy aplikacji, użyj [IOptionsSnapshot](#use-ioptionssnapshot-to-read-updated-data).</span><span class="sxs-lookup"><span data-stu-id="f9301-134">To read changes after the app has started, use [IOptionsSnapshot](#use-ioptionssnapshot-to-read-updated-data).</span></span>

## <a name="options-interfaces"></a><span data-ttu-id="f9301-135">Interfejsy opcji</span><span class="sxs-lookup"><span data-stu-id="f9301-135">Options interfaces</span></span>

<span data-ttu-id="f9301-136"><xref:Microsoft.Extensions.Options.IOptions%601>:</span><span class="sxs-lookup"><span data-stu-id="f9301-136"><xref:Microsoft.Extensions.Options.IOptions%601>:</span></span>

- <span data-ttu-id="f9301-137">Nie _*_obsługuje:_*_</span><span class="sxs-lookup"><span data-stu-id="f9301-137">Does _*_not_*_ support:</span></span>
  - <span data-ttu-id="f9301-138">Odczytywanie danych konfiguracji po rozpoczęciu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f9301-138">Reading of configuration data after the app has started.</span></span>
  - [<span data-ttu-id="f9301-139">Nazwane opcje</span><span class="sxs-lookup"><span data-stu-id="f9301-139">Named options</span></span>](#named-options-support-using-iconfigurenamedoptions)
- <span data-ttu-id="f9301-140">Jest zarejestrowany jako [pojedynczy](dependency-injection.md#singleton) i można go wstrzyknąć w dowolnym [okresie istnienia usługi](dependency-injection.md#service-lifetimes).</span><span class="sxs-lookup"><span data-stu-id="f9301-140">Is registered as a [Singleton](dependency-injection.md#singleton) and can be injected into any [service lifetime](dependency-injection.md#service-lifetimes).</span></span>

<span data-ttu-id="f9301-141"><xref:Microsoft.Extensions.Options.IOptionsSnapshot%601>:</span><span class="sxs-lookup"><span data-stu-id="f9301-141"><xref:Microsoft.Extensions.Options.IOptionsSnapshot%601>:</span></span>

- <span data-ttu-id="f9301-142">Jest przydatne w scenariuszach, w których opcje powinny być ponownie obliczane dla każdego rozpoznawania iniekcji w [zakresie lub przejściowych okresach istnienia](dependency-injection.md#service-lifetimes).</span><span class="sxs-lookup"><span data-stu-id="f9301-142">Is useful in scenarios where options should be recomputed on every injection resolution, in [scoped or transient lifetimes](dependency-injection.md#service-lifetimes).</span></span> <span data-ttu-id="f9301-143">Aby uzyskać więcej informacji, zobacz [Użyj IOptionsSnapshot do odczytu zaktualizowanych danych](#use-ioptionssnapshot-to-read-updated-data).</span><span class="sxs-lookup"><span data-stu-id="f9301-143">For more information, see [Use IOptionsSnapshot to read updated data](#use-ioptionssnapshot-to-read-updated-data).</span></span>
- <span data-ttu-id="f9301-144">Jest zarejestrowany jako [zakres](dependency-injection.md#scoped) i w związku z tym nie można go wstrzyknąć do pojedynczej usługi.</span><span class="sxs-lookup"><span data-stu-id="f9301-144">Is registered as [Scoped](dependency-injection.md#scoped) and therefore cannot be injected into a Singleton service.</span></span>
- <span data-ttu-id="f9301-145">Obsługuje [nazwane opcje](#named-options-support-using-iconfigurenamedoptions)</span><span class="sxs-lookup"><span data-stu-id="f9301-145">Supports [named options](#named-options-support-using-iconfigurenamedoptions)</span></span>

<span data-ttu-id="f9301-146"><xref:Microsoft.Extensions.Options.IOptionsMonitor%601>:</span><span class="sxs-lookup"><span data-stu-id="f9301-146"><xref:Microsoft.Extensions.Options.IOptionsMonitor%601>:</span></span>

- <span data-ttu-id="f9301-147">Służy do pobierania opcji i zarządzania powiadomieniami o `TOptions` wystąpieniach.</span><span class="sxs-lookup"><span data-stu-id="f9301-147">Is used to retrieve options and manage options notifications for `TOptions` instances.</span></span>
- <span data-ttu-id="f9301-148">Jest zarejestrowany jako [pojedynczy](dependency-injection.md#singleton) i można go wstrzyknąć w dowolnym [okresie istnienia usługi](dependency-injection.md#service-lifetimes).</span><span class="sxs-lookup"><span data-stu-id="f9301-148">Is registered as a [Singleton](dependency-injection.md#singleton) and can be injected into any [service lifetime](dependency-injection.md#service-lifetimes).</span></span>
- <span data-ttu-id="f9301-149">Uguje</span><span class="sxs-lookup"><span data-stu-id="f9301-149">Supports:</span></span>
  - <span data-ttu-id="f9301-150">Powiadomienia o zmianie</span><span class="sxs-lookup"><span data-stu-id="f9301-150">Change notifications</span></span>
  - [<span data-ttu-id="f9301-151">Nazwane opcje</span><span class="sxs-lookup"><span data-stu-id="f9301-151">Named options</span></span>](#named-options-support-using-iconfigurenamedoptions)
  - [<span data-ttu-id="f9301-152">Konfiguracja do ponownego ładowania</span><span class="sxs-lookup"><span data-stu-id="f9301-152">Reloadable configuration</span></span>](#use-ioptionssnapshot-to-read-updated-data)
  - <span data-ttu-id="f9301-153">Unieważnianie opcji selektywnych ( <xref:Microsoft.Extensions.Options.IOptionsMonitorCache%601> )</span><span class="sxs-lookup"><span data-stu-id="f9301-153">Selective options invalidation (<xref:Microsoft.Extensions.Options.IOptionsMonitorCache%601>)</span></span>
  
<span data-ttu-id="f9301-154"><xref:Microsoft.Extensions.Options.IOptionsFactory%601> jest odpowiedzialny za tworzenie nowych wystąpień opcji.</span><span class="sxs-lookup"><span data-stu-id="f9301-154"><xref:Microsoft.Extensions.Options.IOptionsFactory%601> is responsible for creating new options instances.</span></span> <span data-ttu-id="f9301-155">Ma jedną <xref:Microsoft.Extensions.Options.IOptionsFactory%601.Create%2A> metodę.</span><span class="sxs-lookup"><span data-stu-id="f9301-155">It has a single <xref:Microsoft.Extensions.Options.IOptionsFactory%601.Create%2A> method.</span></span> <span data-ttu-id="f9301-156">Domyślna implementacja przyjmuje wszystkie zarejestrowane <xref:Microsoft.Extensions.Options.IConfigureOptions%601> i <xref:Microsoft.Extensions.Options.IPostConfigureOptions%601> uruchamia najpierw wszystkie konfiguracje, po których następuje po zakończeniu konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f9301-156">The default implementation takes all registered <xref:Microsoft.Extensions.Options.IConfigureOptions%601> and <xref:Microsoft.Extensions.Options.IPostConfigureOptions%601> and runs all the configurations first, followed by the post-configuration.</span></span> <span data-ttu-id="f9301-157">Odróżnia między <xref:Microsoft.Extensions.Options.IConfigureNamedOptions%601> i <xref:Microsoft.Extensions.Options.IConfigureOptions%601> i tylko wywołuje odpowiedni interfejs.</span><span class="sxs-lookup"><span data-stu-id="f9301-157">It distinguishes between <xref:Microsoft.Extensions.Options.IConfigureNamedOptions%601> and <xref:Microsoft.Extensions.Options.IConfigureOptions%601> and only calls the appropriate interface.</span></span>

<span data-ttu-id="f9301-158"><xref:Microsoft.Extensions.Options.IOptionsMonitorCache%601> jest używany przez program <xref:Microsoft.Extensions.Options.IOptionsMonitor%601> do buforowania `TOptions` wystąpień.</span><span class="sxs-lookup"><span data-stu-id="f9301-158"><xref:Microsoft.Extensions.Options.IOptionsMonitorCache%601> is used by <xref:Microsoft.Extensions.Options.IOptionsMonitor%601> to cache `TOptions` instances.</span></span> <span data-ttu-id="f9301-159"><xref:Microsoft.Extensions.Options.IOptionsMonitorCache%601>Unieważnia wystąpienia opcji w monitorze, aby wartość była ponownie obliczana ( <xref:Microsoft.Extensions.Options.IOptionsMonitorCache%601.TryRemove%2A> ).</span><span class="sxs-lookup"><span data-stu-id="f9301-159">The <xref:Microsoft.Extensions.Options.IOptionsMonitorCache%601> invalidates options instances in the monitor so that the value is recomputed (<xref:Microsoft.Extensions.Options.IOptionsMonitorCache%601.TryRemove%2A>).</span></span> <span data-ttu-id="f9301-160">Wartości można wprowadzać ręcznie przy użyciu <xref:Microsoft.Extensions.Options.IOptionsMonitorCache%601.TryAdd%2A> .</span><span class="sxs-lookup"><span data-stu-id="f9301-160">Values can be manually introduced with <xref:Microsoft.Extensions.Options.IOptionsMonitorCache%601.TryAdd%2A>.</span></span> <span data-ttu-id="f9301-161"><xref:Microsoft.Extensions.Options.IOptionsMonitorCache%601.Clear%2A>Metoda jest używana, gdy wszystkie nazwane wystąpienia powinny być ponownie tworzone na żądanie.</span><span class="sxs-lookup"><span data-stu-id="f9301-161">The <xref:Microsoft.Extensions.Options.IOptionsMonitorCache%601.Clear%2A> method is used when all named instances should be recreated on demand.</span></span>

## <a name="use-ioptionssnapshot-to-read-updated-data"></a><span data-ttu-id="f9301-162">Użyj IOptionsSnapshot do odczytu zaktualizowanych danych</span><span class="sxs-lookup"><span data-stu-id="f9301-162">Use IOptionsSnapshot to read updated data</span></span>

<span data-ttu-id="f9301-163">w przypadku korzystania <xref:Microsoft.Extensions.Options.IOptionsSnapshot%601> z programu opcje są obliczane raz dla każdego żądania, gdy uzyskuje się dostęp i są buforowane przez okres istnienia żądania.</span><span class="sxs-lookup"><span data-stu-id="f9301-163">when you use <xref:Microsoft.Extensions.Options.IOptionsSnapshot%601>, options are computed once per request when accessed and are cached for the lifetime of the request.</span></span> <span data-ttu-id="f9301-164">Zmiany w konfiguracji są odczytywane po uruchomieniu aplikacji podczas korzystania z dostawców konfiguracji, którzy obsługują odczytywanie zaktualizowanych wartości konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f9301-164">Changes to the configuration are read after the app starts when using configuration providers that support reading updated configuration values.</span></span>

<span data-ttu-id="f9301-165">Różnica między `IOptionsMonitor` i `IOptionsSnapshot` to:</span><span class="sxs-lookup"><span data-stu-id="f9301-165">The difference between `IOptionsMonitor` and `IOptionsSnapshot` is that:</span></span>

- <span data-ttu-id="f9301-166">`IOptionsMonitor` jest [usługą singleton](dependency-injection.md#singleton) , która pobiera bieżące wartości opcji w dowolnym momencie, która jest szczególnie przydatna w pojedynczych zależnościach.</span><span class="sxs-lookup"><span data-stu-id="f9301-166">`IOptionsMonitor` is a [singleton service](dependency-injection.md#singleton) that retrieves current option values at any time, which is especially useful in singleton dependencies.</span></span>
- <span data-ttu-id="f9301-167">`IOptionsSnapshot` jest [usługą objętą zakresem](dependency-injection.md#scoped) i zawiera migawkę opcji w czasie `IOptionsSnapshot<T>` konstruowania obiektu.</span><span class="sxs-lookup"><span data-stu-id="f9301-167">`IOptionsSnapshot` is a [scoped service](dependency-injection.md#scoped) and provides a snapshot of the options at the time the `IOptionsSnapshot<T>` object is constructed.</span></span> <span data-ttu-id="f9301-168">Migawki opcji są przeznaczone do użycia z zależnościami przejściowymi i zakresowymi.</span><span class="sxs-lookup"><span data-stu-id="f9301-168">Options snapshots are designed for use with transient and scoped dependencies.</span></span>

<span data-ttu-id="f9301-169">Poniższy kod używa <xref:Microsoft.Extensions.Options.IOptionsSnapshot%601> .</span><span class="sxs-lookup"><span data-stu-id="f9301-169">The following code uses <xref:Microsoft.Extensions.Options.IOptionsSnapshot%601>.</span></span>

:::code language="csharp" source="snippets/configuration/console-json/ScopedService.cs":::

<span data-ttu-id="f9301-170">Poniższy kod rejestruje wystąpienie konfiguracji, które `TransientFaultHandlingOptions` wiąże się z:</span><span class="sxs-lookup"><span data-stu-id="f9301-170">The following code registers a configuration instance which `TransientFaultHandlingOptions` binds against:</span></span>

```csharp
services.Configure<TransientFaultHandlingOptions>(
    configurationRoot.GetSection(
        nameof(TransientFaultHandlingOptions)));
```

<span data-ttu-id="f9301-171">W poprzednim kodzie zmiany w pliku konfiguracji JSON po rozpoczęciu aplikacji są odczytywane.</span><span class="sxs-lookup"><span data-stu-id="f9301-171">In the preceding code, changes to the JSON configuration file after the app has started are read.</span></span>

## <a name="ioptionsmonitor"></a><span data-ttu-id="f9301-172">IOptionsMonitor</span><span class="sxs-lookup"><span data-stu-id="f9301-172">IOptionsMonitor</span></span>

<span data-ttu-id="f9301-173">Poniższy kod rejestruje wystąpienie konfiguracji, które `TransientFaultHandlingOptions` wiąże się z.</span><span class="sxs-lookup"><span data-stu-id="f9301-173">The following code registers a configuration instance which `TransientFaultHandlingOptions` binds against.</span></span>

```csharp
services.Configure<TransientFaultHandlingOptions>(
    configurationRoot.GetSection(
        nameof(TransientFaultHandlingOptions)));
```

<span data-ttu-id="f9301-174">W poniższym przykładzie zastosowano <xref:Microsoft.Extensions.Options.IOptionsMonitor%601> :</span><span class="sxs-lookup"><span data-stu-id="f9301-174">The following example uses <xref:Microsoft.Extensions.Options.IOptionsMonitor%601>:</span></span>

:::code language="csharp" source="snippets/configuration/console-json/MonitorService.cs":::

<span data-ttu-id="f9301-175">W poprzednim kodzie zmiany w pliku konfiguracji JSON po rozpoczęciu aplikacji są odczytywane.</span><span class="sxs-lookup"><span data-stu-id="f9301-175">In the preceding code, changes to the JSON configuration file after the app has started are read.</span></span>

## <a name="named-options-support-using-iconfigurenamedoptions"></a><span data-ttu-id="f9301-176">Obsługa nazwanych opcji przy użyciu IConfigureNamedOptions</span><span class="sxs-lookup"><span data-stu-id="f9301-176">Named options support using IConfigureNamedOptions</span></span>

<span data-ttu-id="f9301-177">Nazwane opcje:</span><span class="sxs-lookup"><span data-stu-id="f9301-177">Named options:</span></span>

- <span data-ttu-id="f9301-178">Są przydatne, gdy wiele sekcji konfiguracji wiąże się z tymi samymi właściwościami.</span><span class="sxs-lookup"><span data-stu-id="f9301-178">Are useful when multiple configuration sections bind to the same properties.</span></span>
- <span data-ttu-id="f9301-179">Uwzględnia wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="f9301-179">Are case-sensitive.</span></span>

<span data-ttu-id="f9301-180">Rozważmy następujące _appsettings.jspliku \*:</span><span class="sxs-lookup"><span data-stu-id="f9301-180">Consider the following _appsettings.json\* file:</span></span>

```json
{
  "Features": {
    "Personalize": {
      "Enabled": true,
      "ApiKey": "aGEgaGEgeW91IHRob3VnaHQgdGhhdCB3YXMgcmVhbGx5IHNvbWV0aGluZw=="
    },
    "WeatherStation": {
      "Enabled": true,
      "ApiKey": "QXJlIHlvdSBhdHRlbXB0aW5nIHRvIGhhY2sgdXM/"
    }
  }
}
```

<span data-ttu-id="f9301-181">Zamiast tworzyć dwie klasy do powiązania `Features:Personalize` i `Features:WeatherStation` , dla każdej sekcji jest używana następująca Klasa:</span><span class="sxs-lookup"><span data-stu-id="f9301-181">Rather than creating two classes to bind `Features:Personalize` and `Features:WeatherStation`, the following class is used for each section:</span></span>

```csharp
public class Features
{
    public const string Personalize = nameof(Personalize);
    public const string WeatherStation = nameof(WeatherStation);

    public bool Enabled { get; set; }
    public string ApiKey { get; set; }
}
```

<span data-ttu-id="f9301-182">Poniższy kod umożliwia skonfigurowanie nazwanych opcji:</span><span class="sxs-lookup"><span data-stu-id="f9301-182">The following code configures the named options:</span></span>

```csharp
ConfigureServices(services =>
{
    services.Configure<Features>(
        Features.Personalize,
        Configuration.GetSection("Features:Personalize"));

    services.Configure<Features>(
        Features.WeatherStation,
        Configuration.GetSection("Features:WeatherStation"));
});
```

<span data-ttu-id="f9301-183">Poniższy kod wyświetla nazwane opcje:</span><span class="sxs-lookup"><span data-stu-id="f9301-183">The following code displays the named options:</span></span>

```csharp
public class Service
{
    private readonly Features _personalizeFeature;
    private readonly Features _weatherStationFeature;

    public Service(IOptionsSnapshot<Features> namedOptionsAccessor)
    {
        _personalizeFeature = namedOptionsAccessor.Get(Features.Personalize);
        _weatherStationFeature = namedOptionsAccessor.Get(Features.WeatherStation);
    }
}
```

<span data-ttu-id="f9301-184">Wszystkie opcje są nazwanymi wystąpieniami.</span><span class="sxs-lookup"><span data-stu-id="f9301-184">All options are named instances.</span></span> <span data-ttu-id="f9301-185"><xref:Microsoft.Extensions.Options.IConfigureOptions%601> wystąpienia są traktowane jako docelowe dla `Options.DefaultName` wystąpienia, czyli `string.Empty` .</span><span class="sxs-lookup"><span data-stu-id="f9301-185"><xref:Microsoft.Extensions.Options.IConfigureOptions%601> instances are treated as targeting the `Options.DefaultName` instance, which is `string.Empty`.</span></span> <span data-ttu-id="f9301-186"><xref:Microsoft.Extensions.Options.IConfigureNamedOptions%601> implementuje także <xref:Microsoft.Extensions.Options.IConfigureOptions%601> .</span><span class="sxs-lookup"><span data-stu-id="f9301-186"><xref:Microsoft.Extensions.Options.IConfigureNamedOptions%601> also implements <xref:Microsoft.Extensions.Options.IConfigureOptions%601>.</span></span> <span data-ttu-id="f9301-187">Domyślna implementacja <xref:Microsoft.Extensions.Options.IOptionsFactory%601> logiki ma na celu odpowiednie użycie.</span><span class="sxs-lookup"><span data-stu-id="f9301-187">The default implementation of the <xref:Microsoft.Extensions.Options.IOptionsFactory%601> has logic to use each appropriately.</span></span> <span data-ttu-id="f9301-188">`null`Nazwana opcja służy do określania wszystkich wystąpień nazwanych zamiast określonego wystąpienia nazwanego.</span><span class="sxs-lookup"><span data-stu-id="f9301-188">The `null` named option is used to target all of the named instances instead of a specific named instance.</span></span> <span data-ttu-id="f9301-189"><xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.ConfigureAll%2A> i <xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.PostConfigureAll%2A> Użyj tej Konwencji.</span><span class="sxs-lookup"><span data-stu-id="f9301-189"><xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.ConfigureAll%2A> and <xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.PostConfigureAll%2A> use this convention.</span></span>

## <a name="optionsbuilder-api"></a><span data-ttu-id="f9301-190">Interfejs API OptionsBuilder</span><span class="sxs-lookup"><span data-stu-id="f9301-190">OptionsBuilder API</span></span>

<span data-ttu-id="f9301-191"><xref:Microsoft.Extensions.Options.OptionsBuilder%601> służy do konfigurowania `TOptions` wystąpień.</span><span class="sxs-lookup"><span data-stu-id="f9301-191"><xref:Microsoft.Extensions.Options.OptionsBuilder%601> is used to configure `TOptions` instances.</span></span> <span data-ttu-id="f9301-192">`OptionsBuilder` usprawnia Tworzenie nazwanych opcji, ponieważ jest tylko pojedynczym parametrem do początkowego `AddOptions<TOptions>(string optionsName)` wywołania, a nie pojawia się we wszystkich kolejnych wywołaniach.</span><span class="sxs-lookup"><span data-stu-id="f9301-192">`OptionsBuilder` streamlines creating named options as it's only a single parameter to the initial `AddOptions<TOptions>(string optionsName)` call instead of appearing in all of the subsequent calls.</span></span> <span data-ttu-id="f9301-193">Sprawdzanie poprawności opcji i `ConfigureOptions` przeciążenia, które akceptują zależności usługi, są dostępne tylko za pośrednictwem programu `OptionsBuilder` .</span><span class="sxs-lookup"><span data-stu-id="f9301-193">Options validation and the `ConfigureOptions` overloads that accept service dependencies are only available via `OptionsBuilder`.</span></span>

<span data-ttu-id="f9301-194">`OptionsBuilder` jest używany w sekcji [Walidacja opcji](#options-validation) .</span><span class="sxs-lookup"><span data-stu-id="f9301-194">`OptionsBuilder` is used in the [Options validation](#options-validation) section.</span></span>

## <a name="use-di-services-to-configure-options"></a><span data-ttu-id="f9301-195">Korzystanie z usług DI Services w celu konfigurowania opcji</span><span class="sxs-lookup"><span data-stu-id="f9301-195">Use DI services to configure options</span></span>

<span data-ttu-id="f9301-196">Usługi są dostępne z iniekcji zależności podczas konfigurowania opcji na dwa sposoby:</span><span class="sxs-lookup"><span data-stu-id="f9301-196">Services can be accessed from dependency injection while configuring options in two ways:</span></span>

- <span data-ttu-id="f9301-197">Przekaż delegat konfiguracji w celu [skonfigurowania](xref:Microsoft.Extensions.Options.OptionsBuilder%601.Configure%2A) w usłudze [OptionsBuilder \<TOptions> ](xref:Microsoft.Extensions.Options.OptionsBuilder%601).</span><span class="sxs-lookup"><span data-stu-id="f9301-197">Pass a configuration delegate to [Configure](xref:Microsoft.Extensions.Options.OptionsBuilder%601.Configure%2A) on [OptionsBuilder\<TOptions>](xref:Microsoft.Extensions.Options.OptionsBuilder%601).</span></span> <span data-ttu-id="f9301-198">`OptionsBuilder<TOptions>` zapewnia przeciążenia [konfiguracji](xref:Microsoft.Extensions.Options.OptionsBuilder%601.Configure%2A) , które umożliwiają korzystanie z maksymalnie pięciu usług w celu konfigurowania opcji:</span><span class="sxs-lookup"><span data-stu-id="f9301-198">`OptionsBuilder<TOptions>` provides overloads of [Configure](xref:Microsoft.Extensions.Options.OptionsBuilder%601.Configure%2A) that allow use of up to five services to configure options:</span></span>

  ```csharp
  services.AddOptions<MyOptions>("optionalName")
      .Configure<ExampleService, ScopedService, MonitorService>(
          (options, es, ss, ms) =>
              options.Property = DoSomethingWith(es, ss, ms));
  ```

- <span data-ttu-id="f9301-199">Utwórz typ, który implementuje <xref:Microsoft.Extensions.Options.IConfigureOptions%601> lub <xref:Microsoft.Extensions.Options.IConfigureNamedOptions%601> i rejestruje typ jako usługę.</span><span class="sxs-lookup"><span data-stu-id="f9301-199">Create a type that implements <xref:Microsoft.Extensions.Options.IConfigureOptions%601> or <xref:Microsoft.Extensions.Options.IConfigureNamedOptions%601> and register the type as a service.</span></span>

<span data-ttu-id="f9301-200">Zalecamy przekazanie delegata konfiguracji w celu [skonfigurowania](xref:Microsoft.Extensions.Options.OptionsBuilder%601.Configure%2A), ponieważ tworzenie usługi jest bardziej skomplikowane.</span><span class="sxs-lookup"><span data-stu-id="f9301-200">We recommend passing a configuration delegate to [Configure](xref:Microsoft.Extensions.Options.OptionsBuilder%601.Configure%2A), since creating a service is more complex.</span></span> <span data-ttu-id="f9301-201">Tworzenie typu jest równoznaczne z tym, co platforma wykonuje podczas wywoływania [konfiguracji](xref:Microsoft.Extensions.Options.OptionsBuilder%601.Configure%2A).</span><span class="sxs-lookup"><span data-stu-id="f9301-201">Creating a type is equivalent to what the framework does when calling [Configure](xref:Microsoft.Extensions.Options.OptionsBuilder%601.Configure%2A).</span></span> <span data-ttu-id="f9301-202">Wywołanie [konfiguracji](xref:Microsoft.Extensions.Options.OptionsBuilder%601.Configure%2A) rejestruje przejściowe ogólne <xref:Microsoft.Extensions.Options.IConfigureNamedOptions%601> , który ma konstruktora akceptującego określone typy usług ogólnych.</span><span class="sxs-lookup"><span data-stu-id="f9301-202">Calling [Configure](xref:Microsoft.Extensions.Options.OptionsBuilder%601.Configure%2A) registers a transient generic <xref:Microsoft.Extensions.Options.IConfigureNamedOptions%601>, which has a constructor that accepts the generic service types specified.</span></span>

## <a name="options-validation"></a><span data-ttu-id="f9301-203">Sprawdzanie poprawności opcji</span><span class="sxs-lookup"><span data-stu-id="f9301-203">Options validation</span></span>

<span data-ttu-id="f9301-204">Sprawdzanie poprawności opcji umożliwia zweryfikowanie wartości opcji.</span><span class="sxs-lookup"><span data-stu-id="f9301-204">Options validation enables option values to be validated.</span></span>

<span data-ttu-id="f9301-205">Rozważmy następujące *appsettings.js* pliku:</span><span class="sxs-lookup"><span data-stu-id="f9301-205">Consider the following *appsettings.json* file:</span></span>

```json
{
  "Settings": {
    "SiteTitle": "Amazing docs from Awesome people!",
    "Scale": 10,
    "VerbosityLevel": 32
  }
}
```

<span data-ttu-id="f9301-206">Następująca Klasa wiąże się z `"Settings"` sekcją konfiguracji i stosuje kilka `DataAnnotations` reguł:</span><span class="sxs-lookup"><span data-stu-id="f9301-206">The following class binds to the `"Settings"` configuration section and applies a couple of `DataAnnotations` rules:</span></span>

:::code language="csharp" source="snippets/configuration/console-json/SettingsOptions.cs":::

<span data-ttu-id="f9301-207">Następujący kod:</span><span class="sxs-lookup"><span data-stu-id="f9301-207">The following code:</span></span>

- <span data-ttu-id="f9301-208">Wywołuje metodę <xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.AddOptions%2A> get [OptionsBuilder \<TOptions> ](xref:Microsoft.Extensions.Options.OptionsBuilder%601) , która wiąże się z `SettingsOptions` klasą.</span><span class="sxs-lookup"><span data-stu-id="f9301-208">Calls <xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.AddOptions%2A> to get an [OptionsBuilder\<TOptions>](xref:Microsoft.Extensions.Options.OptionsBuilder%601) that binds to the `SettingsOptions` class.</span></span>
- <span data-ttu-id="f9301-209">Wywołania umożliwiające <xref:Microsoft.Extensions.DependencyInjection.OptionsBuilderDataAnnotationsExtensions.ValidateDataAnnotations%2A> włączenie walidacji przy użyciu `DataAnnotations` .</span><span class="sxs-lookup"><span data-stu-id="f9301-209">Calls <xref:Microsoft.Extensions.DependencyInjection.OptionsBuilderDataAnnotationsExtensions.ValidateDataAnnotations%2A> to enable validation using `DataAnnotations`.</span></span>

```csharp
services.AddOptions<SettingsOptions>()
    .Bind(Configuration.GetSection(SettingsOptions.Settings))
    .ValidateDataAnnotations();
```

<span data-ttu-id="f9301-210">`ValidateDataAnnotations`Metoda rozszerzenia jest zdefiniowana w pakiecie NuGet [Microsoft. Extensions. options. DataAnnotations](https://www.nuget.org/packages/Microsoft.Extensions.Options.DataAnnotations) .</span><span class="sxs-lookup"><span data-stu-id="f9301-210">The `ValidateDataAnnotations` extension method is defined in the [Microsoft.Extensions.Options.DataAnnotations](https://www.nuget.org/packages/Microsoft.Extensions.Options.DataAnnotations) NuGet package.</span></span>

<span data-ttu-id="f9301-211">Poniższy kod wyświetla wartości konfiguracyjne lub błędy walidacji:</span><span class="sxs-lookup"><span data-stu-id="f9301-211">The following code displays the configuration values or the validation errors:</span></span>

:::code language="csharp" source="snippets/configuration/console-json/ValidationService.cs":::

<span data-ttu-id="f9301-212">Poniższy kod stosuje bardziej złożoną regułę walidacji przy użyciu delegata:</span><span class="sxs-lookup"><span data-stu-id="f9301-212">The following code applies a more complex validation rule using a delegate:</span></span>

```csharp
services.AddOptions<SettingsOptions>()
    .Bind(Configuration.GetSection(SettingsOptions.Settings))
    .ValidateDataAnnotations()
    .Validate(config =>
    {
        if (config.Scale != 0)
        {
            return config.VerbosityLevel > config.Scale;
        }

        return true;
    }, "VerbosityLevel must be > than Scale.");
```

### <a name="ivalidateoptions-for-complex-validation"></a><span data-ttu-id="f9301-213">IValidateOptions na potrzeby złożonej walidacji</span><span class="sxs-lookup"><span data-stu-id="f9301-213">IValidateOptions for complex validation</span></span>

<span data-ttu-id="f9301-214">Następująca Klasa implementuje <xref:Microsoft.Extensions.Options.IValidateOptions%601> :</span><span class="sxs-lookup"><span data-stu-id="f9301-214">The following class implements <xref:Microsoft.Extensions.Options.IValidateOptions%601>:</span></span>

:::code language="csharp" source="snippets/configuration/console-json/ValidateSettingsOptions.cs":::

<span data-ttu-id="f9301-215">`IValidateOptions` umożliwia przeniesienie kodu weryfikacyjnego do klasy.</span><span class="sxs-lookup"><span data-stu-id="f9301-215">`IValidateOptions` enables moving the validation code into a class.</span></span>

<span data-ttu-id="f9301-216">Przy użyciu powyższego kodu sprawdzanie poprawności jest włączane w programie `ConfigureServices` przy użyciu następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="f9301-216">Using the preceding code, validation is enabled in `ConfigureServices` with the following code:</span></span>

```csharp
services.Configure<SettingsOptions>(
    Configuration.GetSection(
        SettingsOptions.Settings));
services.TryAddEnumerable(
    ServiceDescriptor.Singleton
        <IValidateOptions<SettingsOptions>, ValidateSettingsOptions>());
```

## <a name="options-post-configuration"></a><span data-ttu-id="f9301-217">Opcje po konfiguracji</span><span class="sxs-lookup"><span data-stu-id="f9301-217">Options post-configuration</span></span>

<span data-ttu-id="f9301-218">Ustaw wartość po konfiguracji za pomocą <xref:Microsoft.Extensions.Options.IPostConfigureOptions%601> .</span><span class="sxs-lookup"><span data-stu-id="f9301-218">Set post-configuration with <xref:Microsoft.Extensions.Options.IPostConfigureOptions%601>.</span></span> <span data-ttu-id="f9301-219">Po wykonaniu wszystkich czynności konfiguracja zostanie uruchomiona po zakończeniu konfiguracji <xref:Microsoft.Extensions.Options.IConfigureOptions%601> , co może być przydatne w scenariuszach, gdy trzeba przesłonić konfigurację:</span><span class="sxs-lookup"><span data-stu-id="f9301-219">Post-configuration runs after all <xref:Microsoft.Extensions.Options.IConfigureOptions%601> configuration occurs, and can be useful in scenarios when you need to override configuration:</span></span>

```csharp
services.PostConfigure<CustomOptions>(customOptions =>
{
    customOptions.Option1 = "post_configured_option1_value";
});
```

<span data-ttu-id="f9301-220"><xref:Microsoft.Extensions.Options.IPostConfigureOptions%601.PostConfigure%2A> jest dostępny do po skonfigurowaniu nazwanych opcji:</span><span class="sxs-lookup"><span data-stu-id="f9301-220"><xref:Microsoft.Extensions.Options.IPostConfigureOptions%601.PostConfigure%2A> is available to post-configure named options:</span></span>

```csharp
services.PostConfigure<CustomOptions>("named_options_1", customOptions =>
{
    customOptions.Option1 = "post_configured_option1_value";
});
```

<span data-ttu-id="f9301-221">Użyj <xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.PostConfigureAll%2A> , aby skonfigurować wszystkie wystąpienia konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="f9301-221">Use <xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.PostConfigureAll%2A> to post-configure all configuration instances:</span></span>

```csharp
services.PostConfigureAll<CustomOptions>(customOptions =>
{
    customOptions.Option1 = "post_configured_option1_value";
});
```

## <a name="see-also"></a><span data-ttu-id="f9301-222">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="f9301-222">See also</span></span>

- [<span data-ttu-id="f9301-223">Konfiguracja w programie .NET</span><span class="sxs-lookup"><span data-stu-id="f9301-223">Configuration in .NET</span></span>](configuration.md)
