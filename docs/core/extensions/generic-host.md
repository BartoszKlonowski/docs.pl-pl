---
title: Host ogólny .NET
author: IEvangelist
description: Dowiedz się więcej na temat hosta ogólnego platformy .NET, który jest odpowiedzialny za uruchamianie aplikacji i zarządzanie okresem istnienia.
ms.author: dapine
ms.date: 12/04/2020
ms.openlocfilehash: ddb71b70d15121b7f59899fba38b2bf861219878
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96740098"
---
# <a name="net-generic-host"></a>Host ogólny .NET

Szablony usługi procesu roboczego tworzą hosta ogólnego platformy .NET <xref:Microsoft.Extensions.Hosting.HostBuilder> . Hosta ogólnego można używać z innymi typami aplikacji platformy .NET, takimi jak aplikacje konsolowe.

*Host* to obiekt, który hermetyzuje zasoby aplikacji, takie jak:

- Iniekcja zależności (DI)
- Rejestrowanie
- Konfiguracja
- `IHostedService` metod

Po uruchomieniu hosta jest on wywoływany <xref:Microsoft.Extensions.Hosting.IHostedService.StartAsync%2A?displayProperty=nameWithType> dla każdej implementacji <xref:Microsoft.Extensions.Hosting.IHostedService> zarejestrowanej w kolekcji kontenera usługi hostowanej usług. W aplikacji usługi procesu roboczego wszystkie `IHostedService` implementacje, które zawierają <xref:Microsoft.Extensions.Hosting.BackgroundService> wystąpienia, mają <xref:Microsoft.Extensions.Hosting.BackgroundService.ExecuteAsync%2A?displayProperty=nameWithType> metody wywoływane.

Główną przyczyną uwzględnienia wszystkich zasobów zależnych od aplikacji w jednym obiekcie jest zarządzanie okresem istnienia: Kontrola uruchamiania aplikacji i bezpieczne zamykanie. Uzyskuje się to za pomocą pakietu NuGet [Microsoft. Extensions. host](https://www.nuget.org/packages/Microsoft.Extensions.Hosting) .

## <a name="set-up-a-host"></a>Konfigurowanie hosta

Host jest zazwyczaj konfigurowany, zbudowany i uruchamiany przez kod w `Program` klasie. `Main`Metoda:

- Wywołuje <xref:Microsoft.Extensions.Hosting.Host.CreateDefaultBuilder> metodę, aby utworzyć i skonfigurować obiekt konstruktora.
- Wywołuje <xref:Microsoft.Extensions.Hosting.IHostBuilder.Build> Tworzenie <xref:Microsoft.Extensions.Hosting.IHost> wystąpienia.
- Wywołania <xref:Microsoft.Extensions.Hosting.HostingAbstractionsHostExtensions.Run%2A> lub <xref:Microsoft.Extensions.Hosting.HostingAbstractionsHostExtensions.RunAsync%2A> Metoda w obiekcie hosta.

Szablony usługi programu .NET Worker generują następujący kod w celu utworzenia hosta generycznego:

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

## <a name="default-builder-settings"></a>Ustawienia domyślnego konstruktora

<xref:Microsoft.Extensions.Hosting.Host.CreateDefaultBuilder%2A>Metoda:

- Ustawia katalog główny zawartości na ścieżkę zwracaną przez <xref:System.IO.Directory.GetCurrentDirectory> .
- Ładuje [konfigurację hosta](#host-configuration) z:
  - Zmienne środowiskowe poprzedzone prefiksem `DOTNET_` .
  - Argumenty wiersza polecenia.
- Ładuje konfigurację aplikacji z:
  - *appsettings.js*.
  - *appSettings. {Environment}. JSON*.
  - Secret Manager, gdy aplikacja jest uruchamiana w `Development` środowisku.
  - Zmienne środowiskowe.
  - Argumenty wiersza polecenia.
- Dodaje następujących dostawców rejestrowania:
  - Konsola
  - Debugowanie
  - EventSource
  - EventLog (tylko w przypadku uruchamiania w systemie Windows)
- Umożliwia weryfikację zakresu i [Sprawdzanie poprawności zależności](xref:Microsoft.Extensions.DependencyInjection.ServiceProviderOptions.ValidateOnBuild) , gdy środowisko jest `Development` .

Metoda ta umożliwia `ConfigureServices` Dodawanie usług do <xref:Microsoft.Extensions.DependencyInjection.IServiceCollection?displayProperty=nameWithType> wystąpienia. Później te usługi mogą być udostępniane z iniekcji zależności.

## <a name="framework-provided-services"></a>Usługi udostępniane przez platformę

Następujące usługi są rejestrowane automatycznie:

- [IHostApplicationLifetime](#ihostapplicationlifetime)
- [IHostLifetime](#ihostlifetime)
- [IHostEnvironment](#ihostenvironment)

## <a name="ihostapplicationlifetime"></a>IHostApplicationLifetime

Wsuń <xref:Microsoft.Extensions.Hosting.IHostApplicationLifetime> usługę do dowolnej klasy w celu obsługi zadań po uruchomieniu i bezpiecznego zamykania. Trzy właściwości interfejsu to tokeny anulowania używane do rejestrowania metod obsługi zdarzeń uruchamiania i zatrzymywania aplikacji. Interfejs zawiera również <xref:Microsoft.Extensions.Hosting.IHostApplicationLifetime.StopApplication> metodę.

Poniższy przykład to `IHostedService` implementacja, która rejestruje `IHostApplicationLifetime` zdarzenia:

:::code language="csharp" source="snippets/configuration/app-lifetime/ExampleHostedService.cs" highlight="18-20":::

Aby dodać implementację, można zmodyfikować szablon usługi procesu roboczego `ExampleHostedService` :

:::code language="csharp" source="snippets/configuration/app-lifetime/Program.cs" range="1-16,36" highlight="15":::

Aplikacja zapisze następujące przykładowe dane wyjściowe:

:::code language="csharp" source="snippets/configuration/app-lifetime/Program.cs" range="17-35":::

## <a name="ihostlifetime"></a>IHostLifetime

<xref:Microsoft.Extensions.Hosting.IHostLifetime>Implementacja kontroluje moment uruchomienia hosta i jego zatrzymania. Używana jest Ostatnia zarejestrowana implementacja.

`Microsoft.Extensions.Hosting.Internal.ConsoleLifetime` jest `IHostLifetime` implementacją domyślną. `ConsoleLifetime`:

- Nasłuchuje <kbd>kombinacji klawiszy CTRL</kbd> + <kbd>C</kbd>, [SIGINT](https://en.wikipedia.org/wiki/Signal_(IPC)#SIGINT)lub [SIGTERM](https://en.wikipedia.org/wiki/Signal_(IPC)#SIGTERM) i wywołań, <xref:Microsoft.Extensions.Hosting.IHostApplicationLifetime.StopApplication%2A> Aby rozpocząć proces zamykania.
- Odblokowuje rozszerzenia, takie jak `RunAsync` i `WaitForShutdownAsync` .

## <a name="ihostenvironment"></a>IHostEnvironment

Wsuń <xref:Microsoft.Extensions.Hosting.IHostEnvironment> usługę do klasy, aby uzyskać informacje o następujących ustawieniach:

- <xref:Microsoft.Extensions.Hosting.IHostEnvironment.ApplicationName?displayProperty=nameWithType>
- <xref:Microsoft.Extensions.Hosting.IHostEnvironment.ContentRootFileProvider?displayProperty=nameWithType>
- <xref:Microsoft.Extensions.Hosting.IHostEnvironment.ContentRootPath?displayProperty=nameWithType>
- <xref:Microsoft.Extensions.Hosting.IHostEnvironment.EnvironmentName?displayProperty=nameWithType>

## <a name="host-configuration"></a>Konfiguracja hosta

Konfiguracja hosta jest używana we właściwościach <xref:Microsoft.Extensions.Hosting.IHostEnvironment> implementacji.

Konfiguracja hosta jest dostępna w [HostBuilderContext.Configwersja](xref:Microsoft.Extensions.Hosting.HostBuilderContext.Configuration) <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration%2A> . Po `ConfigureAppConfiguration` program `HostBuilderContext.Configuration` zostanie zastąpiony konfiguracją aplikacji.

Aby dodać konfigurację hosta, wywołaj polecenie <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureHostConfiguration%2A> `IHostBuilder` . `ConfigureHostConfiguration` może być wywoływana wiele razy z wynikami. Host używa dowolnej opcji ustawia wartość ostatnią dla danego klucza.

Poniższy przykład umożliwia utworzenie konfiguracji hosta:

:::code language="csharp" source="snippets/configuration/console-host/Program.cs" highlight="19-25":::

## <a name="app-configuration"></a>Konfiguracja aplikacji

Konfiguracja aplikacji jest tworzona przez wywołanie metody <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration%2A> on `IHostBuilder` . `ConfigureAppConfiguration` może być wywoływana wiele razy z wynikami. Aplikacja używa dowolnej opcji ustawia wartość ostatnią dla danego klucza.

Konfiguracja utworzona przez program `ConfigureAppConfiguration` jest dostępna w [HostBuilderContext.Configwersja](xref:Microsoft.Extensions.Hosting.HostBuilderContext.Configuration%2A) na potrzeby kolejnych operacji i jako usługa z di. Konfiguracja hosta jest również dodawana do konfiguracji aplikacji.

Aby uzyskać więcej informacji, zobacz [Konfiguracja w programie .NET](configuration.md).

## <a name="see-also"></a>Zobacz także

- [Konfiguracja w programie .NET](configuration.md)
- [ASP.NET Core hosta sieci Web](/aspnet/core/fundamentals/host/web-host)
- Błędy hostów ogólnych powinny być tworzone w repozytorium [GitHub.com/dotnet/Extensions](https://github.com/dotnet/extensions/issues)
