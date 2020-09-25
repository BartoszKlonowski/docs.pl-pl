---
title: Host ogólny .NET
author: IEvangelist
description: Dowiedz się więcej na temat hosta ogólnego platformy .NET, który jest odpowiedzialny za uruchamianie aplikacji i zarządzanie okresem istnienia.
ms.author: dapine
ms.date: 09/18/2020
ms.openlocfilehash: c1b22b4490dc54d462482976d1c2e512f812c9a9
ms.sourcegitcommit: d2db216e46323f73b32ae312c9e4135258e5d68e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "90875863"
---
# <a name="net-generic-host"></a><span data-ttu-id="7136e-103">Host ogólny .NET</span><span class="sxs-lookup"><span data-stu-id="7136e-103">.NET Generic Host</span></span>

<span data-ttu-id="7136e-104">Szablony usługi procesu roboczego tworzą hosta ogólnego platformy .NET <xref:Microsoft.Extensions.Hosting.HostBuilder> .</span><span class="sxs-lookup"><span data-stu-id="7136e-104">The Worker Service templates create a .NET Generic Host, <xref:Microsoft.Extensions.Hosting.HostBuilder>.</span></span> <span data-ttu-id="7136e-105">Hosta ogólnego można używać z innymi typami aplikacji platformy .NET, takimi jak aplikacje konsolowe.</span><span class="sxs-lookup"><span data-stu-id="7136e-105">The Generic Host can be used with other types of .NET applications, such as Console apps.</span></span>

<span data-ttu-id="7136e-106">*Host* to obiekt, który hermetyzuje zasoby aplikacji, takie jak:</span><span class="sxs-lookup"><span data-stu-id="7136e-106">A *host* is an object that encapsulates an app's resources, such as:</span></span>

- <span data-ttu-id="7136e-107">Iniekcja zależności (DI)</span><span class="sxs-lookup"><span data-stu-id="7136e-107">Dependency injection (DI)</span></span>
- <span data-ttu-id="7136e-108">Rejestrowanie</span><span class="sxs-lookup"><span data-stu-id="7136e-108">Logging</span></span>
- <span data-ttu-id="7136e-109">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="7136e-109">Configuration</span></span>
- <span data-ttu-id="7136e-110">`IHostedService` metod</span><span class="sxs-lookup"><span data-stu-id="7136e-110">`IHostedService` implementations</span></span>

<span data-ttu-id="7136e-111">Po uruchomieniu hosta jest on wywoływany <xref:Microsoft.Extensions.Hosting.IHostedService.StartAsync%2A?displayProperty=nameWithType> dla każdej implementacji <xref:Microsoft.Extensions.Hosting.IHostedService> zarejestrowanej w kolekcji kontenera usługi hostowanej usług.</span><span class="sxs-lookup"><span data-stu-id="7136e-111">When a host starts, it calls <xref:Microsoft.Extensions.Hosting.IHostedService.StartAsync%2A?displayProperty=nameWithType> on each implementation of <xref:Microsoft.Extensions.Hosting.IHostedService> registered in the service container's collection of hosted services.</span></span> <span data-ttu-id="7136e-112">W aplikacji usługi procesu roboczego wszystkie `IHostedService` implementacje, które zawierają <xref:Microsoft.Extensions.Hosting.BackgroundService> wystąpienia, mają <xref:Microsoft.Extensions.Hosting.BackgroundService.ExecuteAsync%2A?displayProperty=nameWithType> metody wywoływane.</span><span class="sxs-lookup"><span data-stu-id="7136e-112">In a worker service app, all `IHostedService` implementations that contain <xref:Microsoft.Extensions.Hosting.BackgroundService> instances have their <xref:Microsoft.Extensions.Hosting.BackgroundService.ExecuteAsync%2A?displayProperty=nameWithType> methods called.</span></span>

<span data-ttu-id="7136e-113">Główną przyczyną uwzględnienia wszystkich zasobów zależnych od aplikacji w jednym obiekcie jest zarządzanie okresem istnienia: Kontrola uruchamiania aplikacji i bezpieczne zamykanie.</span><span class="sxs-lookup"><span data-stu-id="7136e-113">The main reason for including all of the app's interdependent resources in one object is lifetime management: control over app startup and graceful shutdown.</span></span> <span data-ttu-id="7136e-114">Uzyskuje się to za pomocą pakietu NuGet [Microsoft. Extensions. host](https://www.nuget.org/packages/Microsoft.Extensions.Hosting) .</span><span class="sxs-lookup"><span data-stu-id="7136e-114">This is achieved with the [Microsoft.Extensions.Hosting](https://www.nuget.org/packages/Microsoft.Extensions.Hosting) NuGet package.</span></span>

## <a name="set-up-a-host"></a><span data-ttu-id="7136e-115">Konfigurowanie hosta</span><span class="sxs-lookup"><span data-stu-id="7136e-115">Set up a host</span></span>

<span data-ttu-id="7136e-116">Host jest zazwyczaj konfigurowany, zbudowany i uruchamiany przez kod w `Program` klasie.</span><span class="sxs-lookup"><span data-stu-id="7136e-116">The host is typically configured, built, and run by code in the `Program` class.</span></span> <span data-ttu-id="7136e-117">`Main`Metoda:</span><span class="sxs-lookup"><span data-stu-id="7136e-117">The `Main` method:</span></span>

- <span data-ttu-id="7136e-118">Wywołuje <xref:Microsoft.Extensions.Hosting.Host.CreateDefaultBuilder> metodę, aby utworzyć i skonfigurować obiekt konstruktora.</span><span class="sxs-lookup"><span data-stu-id="7136e-118">Calls a <xref:Microsoft.Extensions.Hosting.Host.CreateDefaultBuilder> method to create and configure a builder object.</span></span>
- <span data-ttu-id="7136e-119">Wywołuje <xref:Microsoft.Extensions.Hosting.IHostBuilder.Build> Tworzenie <xref:Microsoft.Extensions.Hosting.IHost> wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="7136e-119">Calls <xref:Microsoft.Extensions.Hosting.IHostBuilder.Build> to create an <xref:Microsoft.Extensions.Hosting.IHost> instance.</span></span>
- <span data-ttu-id="7136e-120">Wywołania <xref:Microsoft.Extensions.Hosting.HostingAbstractionsHostExtensions.Run%2A> lub <xref:Microsoft.Extensions.Hosting.HostingAbstractionsHostExtensions.RunAsync%2A> Metoda w obiekcie hosta.</span><span class="sxs-lookup"><span data-stu-id="7136e-120">Calls <xref:Microsoft.Extensions.Hosting.HostingAbstractionsHostExtensions.Run%2A> or <xref:Microsoft.Extensions.Hosting.HostingAbstractionsHostExtensions.RunAsync%2A> method on the host object.</span></span>

<span data-ttu-id="7136e-121">Szablony usługi programu .NET Worker generują następujący kod w celu utworzenia hosta generycznego:</span><span class="sxs-lookup"><span data-stu-id="7136e-121">The .NET Worker Service templates generate the following code to create a Generic Host:</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateHostBuilder(args).Build().Run();
    }

    public static IHostBuilder CreateHostBuilder(string[] args) =>
        Host.CreateDefaultBuilder(args)
            .ConfigureServices((hostContext, services) =>
            {
                services.AddHostedService<Worker>();
            });
}
```

## <a name="default-builder-settings"></a><span data-ttu-id="7136e-122">Ustawienia domyślnego konstruktora</span><span class="sxs-lookup"><span data-stu-id="7136e-122">Default builder settings</span></span>

<span data-ttu-id="7136e-123"><xref:Microsoft.Extensions.Hosting.Host.CreateDefaultBuilder%2A>Metoda:</span><span class="sxs-lookup"><span data-stu-id="7136e-123">The <xref:Microsoft.Extensions.Hosting.Host.CreateDefaultBuilder%2A> method:</span></span>

- <span data-ttu-id="7136e-124">Ustawia katalog główny zawartości na ścieżkę zwracaną przez <xref:System.IO.Directory.GetCurrentDirectory> .</span><span class="sxs-lookup"><span data-stu-id="7136e-124">Sets the content root to the path returned by <xref:System.IO.Directory.GetCurrentDirectory>.</span></span>
- <span data-ttu-id="7136e-125">Ładuje [konfigurację hosta](#host-configuration) z:</span><span class="sxs-lookup"><span data-stu-id="7136e-125">Loads [host configuration](#host-configuration) from:</span></span>
  - <span data-ttu-id="7136e-126">Zmienne środowiskowe poprzedzone prefiksem `DOTNET_` .</span><span class="sxs-lookup"><span data-stu-id="7136e-126">Environment variables prefixed with `DOTNET_`.</span></span>
  - <span data-ttu-id="7136e-127">Argumenty wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="7136e-127">Command-line arguments.</span></span>
- <span data-ttu-id="7136e-128">Ładuje konfigurację aplikacji z:</span><span class="sxs-lookup"><span data-stu-id="7136e-128">Loads app configuration from:</span></span>
  - <span data-ttu-id="7136e-129">*appsettings.js*.</span><span class="sxs-lookup"><span data-stu-id="7136e-129">*appsettings.json*.</span></span>
  - <span data-ttu-id="7136e-130">*appSettings. {Environment}. JSON*.</span><span class="sxs-lookup"><span data-stu-id="7136e-130">*appsettings.{Environment}.json*.</span></span>
  - <span data-ttu-id="7136e-131">Secret Manager, gdy aplikacja jest uruchamiana w `Development` środowisku.</span><span class="sxs-lookup"><span data-stu-id="7136e-131">Secret Manager when the app runs in the `Development` environment.</span></span>
  - <span data-ttu-id="7136e-132">Zmienne środowiskowe.</span><span class="sxs-lookup"><span data-stu-id="7136e-132">Environment variables.</span></span>
  - <span data-ttu-id="7136e-133">Argumenty wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="7136e-133">Command-line arguments.</span></span>
- <span data-ttu-id="7136e-134">Dodaje następujących dostawców rejestrowania:</span><span class="sxs-lookup"><span data-stu-id="7136e-134">Adds the following logging providers:</span></span>
  - <span data-ttu-id="7136e-135">Konsola</span><span class="sxs-lookup"><span data-stu-id="7136e-135">Console</span></span>
  - <span data-ttu-id="7136e-136">Debugowanie</span><span class="sxs-lookup"><span data-stu-id="7136e-136">Debug</span></span>
  - <span data-ttu-id="7136e-137">EventSource</span><span class="sxs-lookup"><span data-stu-id="7136e-137">EventSource</span></span>
  - <span data-ttu-id="7136e-138">EventLog (tylko w przypadku uruchamiania w systemie Windows)</span><span class="sxs-lookup"><span data-stu-id="7136e-138">EventLog (only when running on Windows)</span></span>
- <span data-ttu-id="7136e-139">Umożliwia weryfikację zakresu i [Sprawdzanie poprawności zależności](xref:Microsoft.Extensions.DependencyInjection.ServiceProviderOptions.ValidateOnBuild) , gdy środowisko jest `Development` .</span><span class="sxs-lookup"><span data-stu-id="7136e-139">Enables scope validation and [dependency validation](xref:Microsoft.Extensions.DependencyInjection.ServiceProviderOptions.ValidateOnBuild) when the environment is `Development`.</span></span>

<span data-ttu-id="7136e-140">Metoda ta umożliwia `ConfigureServices` Dodawanie usług do <xref:Microsoft.Extensions.DependencyInjection.IServiceCollection?displayProperty=nameWithType> wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="7136e-140">The `ConfigureServices` method exposes the ability to add services to the <xref:Microsoft.Extensions.DependencyInjection.IServiceCollection?displayProperty=nameWithType> instance.</span></span> <span data-ttu-id="7136e-141">Później te usługi mogą być udostępniane z iniekcji zależności.</span><span class="sxs-lookup"><span data-stu-id="7136e-141">Later, these services can be made available from dependency injection.</span></span>

## <a name="framework-provided-services"></a><span data-ttu-id="7136e-142">Usługi udostępniane przez platformę</span><span class="sxs-lookup"><span data-stu-id="7136e-142">Framework-provided services</span></span>

<span data-ttu-id="7136e-143">Następujące usługi są rejestrowane automatycznie:</span><span class="sxs-lookup"><span data-stu-id="7136e-143">The following services are registered automatically:</span></span>

- [<span data-ttu-id="7136e-144">IHostApplicationLifetime</span><span class="sxs-lookup"><span data-stu-id="7136e-144">IHostApplicationLifetime</span></span>](#ihostapplicationlifetime)
- [<span data-ttu-id="7136e-145">IHostLifetime</span><span class="sxs-lookup"><span data-stu-id="7136e-145">IHostLifetime</span></span>](#ihostlifetime)
- [<span data-ttu-id="7136e-146">IHostEnvironment</span><span class="sxs-lookup"><span data-stu-id="7136e-146">IHostEnvironment</span></span>](#ihostenvironment)

## <a name="ihostapplicationlifetime"></a><span data-ttu-id="7136e-147">IHostApplicationLifetime</span><span class="sxs-lookup"><span data-stu-id="7136e-147">IHostApplicationLifetime</span></span>

<span data-ttu-id="7136e-148">Wsuń <xref:Microsoft.Extensions.Hosting.IHostApplicationLifetime> usługę do dowolnej klasy w celu obsługi zadań po uruchomieniu i bezpiecznego zamykania.</span><span class="sxs-lookup"><span data-stu-id="7136e-148">Inject the <xref:Microsoft.Extensions.Hosting.IHostApplicationLifetime> service into any class to handle post-startup and graceful shutdown tasks.</span></span> <span data-ttu-id="7136e-149">Trzy właściwości interfejsu to tokeny anulowania używane do rejestrowania metod obsługi zdarzeń uruchamiania i zatrzymywania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7136e-149">Three properties on the interface are cancellation tokens used to register app start and app stop event handler methods.</span></span> <span data-ttu-id="7136e-150">Interfejs zawiera również <xref:Microsoft.Extensions.Hosting.IHostApplicationLifetime.StopApplication> metodę.</span><span class="sxs-lookup"><span data-stu-id="7136e-150">The interface also includes a <xref:Microsoft.Extensions.Hosting.IHostApplicationLifetime.StopApplication> method.</span></span>

<span data-ttu-id="7136e-151">Poniższy przykład to `IHostedService` implementacja, która rejestruje `IHostApplicationLifetime` zdarzenia:</span><span class="sxs-lookup"><span data-stu-id="7136e-151">The following example is an `IHostedService` implementation that registers `IHostApplicationLifetime` events:</span></span>

:::code language="csharp" source="snippets/configuration/app-lifetime/ExampleHostedService.cs" highlight="18-20":::

<span data-ttu-id="7136e-152">Aby dodać implementację, można zmodyfikować szablon usługi procesu roboczego `ExampleHostedService` :</span><span class="sxs-lookup"><span data-stu-id="7136e-152">The Worker Service template could be modified to add the `ExampleHostedService` implementation:</span></span>

:::code language="csharp" source="snippets/configuration/app-lifetime/Program.cs" range="1-16,36" highlight="15":::

<span data-ttu-id="7136e-153">Aplikacja zapisze następujące przykładowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="7136e-153">The application would write the following sample output:</span></span>

:::code language="csharp" source="snippets/configuration/app-lifetime/Program.cs" range="17-35":::

## <a name="ihostlifetime"></a><span data-ttu-id="7136e-154">IHostLifetime</span><span class="sxs-lookup"><span data-stu-id="7136e-154">IHostLifetime</span></span>

<span data-ttu-id="7136e-155"><xref:Microsoft.Extensions.Hosting.IHostLifetime>Implementacja kontroluje moment uruchomienia hosta i jego zatrzymania.</span><span class="sxs-lookup"><span data-stu-id="7136e-155">The <xref:Microsoft.Extensions.Hosting.IHostLifetime> implementation controls when the host starts and when it stops.</span></span> <span data-ttu-id="7136e-156">Używana jest Ostatnia zarejestrowana implementacja.</span><span class="sxs-lookup"><span data-stu-id="7136e-156">The last implementation registered is used.</span></span>

<span data-ttu-id="7136e-157">`Microsoft.Extensions.Hosting.Internal.ConsoleLifetime` jest `IHostLifetime` implementacją domyślną.</span><span class="sxs-lookup"><span data-stu-id="7136e-157">`Microsoft.Extensions.Hosting.Internal.ConsoleLifetime` is the default `IHostLifetime` implementation.</span></span> <span data-ttu-id="7136e-158">`ConsoleLifetime`:</span><span class="sxs-lookup"><span data-stu-id="7136e-158">`ConsoleLifetime`:</span></span>

- <span data-ttu-id="7136e-159">Nasłuchuje <kbd>kombinacji klawiszy CTRL</kbd> + <kbd>C</kbd>, [SIGINT](https://en.wikipedia.org/wiki/Signal_(IPC)#SIGINT)lub [SIGTERM](https://en.wikipedia.org/wiki/Signal_(IPC)#SIGTERM) i wywołań, <xref:Microsoft.Extensions.Hosting.IHostApplicationLifetime.StopApplication%2A> Aby rozpocząć proces zamykania.</span><span class="sxs-lookup"><span data-stu-id="7136e-159">Listens for <kbd>Ctrl</kbd>+<kbd>C</kbd>, [SIGINT](https://en.wikipedia.org/wiki/Signal_(IPC)#SIGINT), or [SIGTERM](https://en.wikipedia.org/wiki/Signal_(IPC)#SIGTERM) and calls <xref:Microsoft.Extensions.Hosting.IHostApplicationLifetime.StopApplication%2A> to start the shutdown process.</span></span>
- <span data-ttu-id="7136e-160">Odblokowuje rozszerzenia, takie jak `RunAsync` i `WaitForShutdownAsync` .</span><span class="sxs-lookup"><span data-stu-id="7136e-160">Unblocks extensions such as `RunAsync` and `WaitForShutdownAsync`.</span></span>

## <a name="ihostenvironment"></a><span data-ttu-id="7136e-161">IHostEnvironment</span><span class="sxs-lookup"><span data-stu-id="7136e-161">IHostEnvironment</span></span>

<span data-ttu-id="7136e-162">Wsuń <xref:Microsoft.Extensions.Hosting.IHostEnvironment> usługę do klasy, aby uzyskać informacje o następujących ustawieniach:</span><span class="sxs-lookup"><span data-stu-id="7136e-162">Inject the <xref:Microsoft.Extensions.Hosting.IHostEnvironment> service into a class to get information about the following settings:</span></span>

- <xref:Microsoft.Extensions.Hosting.IHostEnvironment.ApplicationName?displayProperty=nameWithType>
- <xref:Microsoft.Extensions.Hosting.IHostEnvironment.ContentRootFileProvider?displayProperty=nameWithType>
- <xref:Microsoft.Extensions.Hosting.IHostEnvironment.ContentRootPath?displayProperty=nameWithType>
- <xref:Microsoft.Extensions.Hosting.IHostEnvironment.EnvironmentName?displayProperty=nameWithType>

## <a name="host-configuration"></a><span data-ttu-id="7136e-163">Konfiguracja hosta</span><span class="sxs-lookup"><span data-stu-id="7136e-163">Host configuration</span></span>

<span data-ttu-id="7136e-164">Konfiguracja hosta jest używana we właściwościach <xref:Microsoft.Extensions.Hosting.IHostEnvironment> implementacji.</span><span class="sxs-lookup"><span data-stu-id="7136e-164">Host configuration is used for the properties of the <xref:Microsoft.Extensions.Hosting.IHostEnvironment> implementation.</span></span>

<span data-ttu-id="7136e-165">Konfiguracja hosta jest dostępna w [HostBuilderContext.Configwersja](xref:Microsoft.Extensions.Hosting.HostBuilderContext.Configuration) <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration%2A> .</span><span class="sxs-lookup"><span data-stu-id="7136e-165">Host configuration is available from [HostBuilderContext.Configuration](xref:Microsoft.Extensions.Hosting.HostBuilderContext.Configuration) inside <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration%2A>.</span></span> <span data-ttu-id="7136e-166">Po `ConfigureAppConfiguration` program `HostBuilderContext.Configuration` zostanie zastąpiony konfiguracją aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7136e-166">After `ConfigureAppConfiguration`, `HostBuilderContext.Configuration` is replaced with the app config.</span></span>

<span data-ttu-id="7136e-167">Aby dodać konfigurację hosta, wywołaj polecenie <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureHostConfiguration%2A> `IHostBuilder` .</span><span class="sxs-lookup"><span data-stu-id="7136e-167">To add host configuration, call <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureHostConfiguration%2A> on `IHostBuilder`.</span></span> <span data-ttu-id="7136e-168">`ConfigureHostConfiguration` może być wywoływana wiele razy z wynikami.</span><span class="sxs-lookup"><span data-stu-id="7136e-168">`ConfigureHostConfiguration` can be called multiple times with additive results.</span></span> <span data-ttu-id="7136e-169">Host używa dowolnej opcji ustawia wartość ostatnią dla danego klucza.</span><span class="sxs-lookup"><span data-stu-id="7136e-169">The host uses whichever option sets a value last on a given key.</span></span>

<span data-ttu-id="7136e-170">Poniższy przykład umożliwia utworzenie konfiguracji hosta:</span><span class="sxs-lookup"><span data-stu-id="7136e-170">The following example creates host configuration:</span></span>

:::code language="csharp" source="snippets/configuration/console-host/Program.cs" highlight="13-19":::

## <a name="app-configuration"></a><span data-ttu-id="7136e-171">Konfiguracja aplikacji</span><span class="sxs-lookup"><span data-stu-id="7136e-171">App configuration</span></span>

<span data-ttu-id="7136e-172">Konfiguracja aplikacji jest tworzona przez wywołanie metody <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration%2A> on `IHostBuilder` .</span><span class="sxs-lookup"><span data-stu-id="7136e-172">App configuration is created by calling <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration%2A> on `IHostBuilder`.</span></span> <span data-ttu-id="7136e-173">`ConfigureAppConfiguration` może być wywoływana wiele razy z wynikami.</span><span class="sxs-lookup"><span data-stu-id="7136e-173">`ConfigureAppConfiguration` can be called multiple times with additive results.</span></span> <span data-ttu-id="7136e-174">Aplikacja używa dowolnej opcji ustawia wartość ostatnią dla danego klucza.</span><span class="sxs-lookup"><span data-stu-id="7136e-174">The app uses whichever option sets a value last on a given key.</span></span>

<span data-ttu-id="7136e-175">Konfiguracja utworzona przez program `ConfigureAppConfiguration` jest dostępna w [HostBuilderContext.Configwersja](xref:Microsoft.Extensions.Hosting.HostBuilderContext.Configuration%2A) na potrzeby kolejnych operacji i jako usługa z di.</span><span class="sxs-lookup"><span data-stu-id="7136e-175">The configuration created by `ConfigureAppConfiguration` is available at [HostBuilderContext.Configuration](xref:Microsoft.Extensions.Hosting.HostBuilderContext.Configuration%2A) for subsequent operations and as a service from DI.</span></span> <span data-ttu-id="7136e-176">Konfiguracja hosta jest również dodawana do konfiguracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7136e-176">The host configuration is also added to the app configuration.</span></span>

<span data-ttu-id="7136e-177">Aby uzyskać więcej informacji, zobacz [Konfiguracja w programie .NET](configuration.md).</span><span class="sxs-lookup"><span data-stu-id="7136e-177">For more information, see [Configuration in .NET](configuration.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="7136e-178">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="7136e-178">See also</span></span>

- [<span data-ttu-id="7136e-179">Konfiguracja w programie .NET</span><span class="sxs-lookup"><span data-stu-id="7136e-179">Configuration in .NET</span></span>](configuration.md)
- [<span data-ttu-id="7136e-180">ASP.NET Core hosta sieci Web</span><span class="sxs-lookup"><span data-stu-id="7136e-180">ASP.NET Core Web Host</span></span>](/aspnet/core/fundamentals/host/web-host)