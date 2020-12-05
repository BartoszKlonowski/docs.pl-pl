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
# <a name="options-pattern-in-net"></a>Wzorzec opcji w programie .NET

Wzorzec opcji używa klas, aby zapewnić dostęp z jednoznacznie określonym grupom ustawień pokrewnych. Gdy [Ustawienia konfiguracji](configuration.md) są izolowane według scenariusza w osobnych klasach, aplikacja będzie zgodna z dwoma ważnymi zasadami inżynierii oprogramowania:

- [Zasada segregowania interfejsu (ISP) lub hermetyzacja](../../architecture/modern-web-apps-azure/architectural-principles.md#encapsulation): scenariusze (klasy), które są zależne od ustawień konfiguracji, zależą tylko od ustawień konfiguracji, których używają.
- [Separacja obaw](../../architecture/modern-web-apps-azure/architectural-principles.md#separation-of-concerns): ustawienia dla różnych części aplikacji nie są zależne ani powiązane ze sobą.

Opcje umożliwiają również mechanizm weryfikacji danych konfiguracyjnych. Aby uzyskać więcej informacji, zobacz sekcję [Opcje walidacji](#options-validation) .

## <a name="bind-hierarchical-configuration"></a>Powiąż hierarchiczną konfigurację

Preferowanym sposobem odczytywania pokrewnych wartości konfiguracji jest użycie wzorca opcji. Na przykład, aby odczytać następujące wartości konfiguracji:

:::code language="json" source="snippets/configuration/console-json/appsettings.json" range="3-6":::

Utwórz następującą `TransientFaultHandlingOptions` klasę:

:::code language="csharp" source="snippets/configuration/console-json/TransientFaultHandlingOptions.cs" range="5-6":::

Klasa opcji:

* Nie może być abstrakcyjny z publicznym konstruktorem bez parametrów
* Zawierają publiczne właściwości odczytu i zapisu do powiązania (pola **są *** niepowiązane)

Następujący kod:

_ Wywołuje [ConfigurationBinder. bind](xref:Microsoft.Extensions.Configuration.ConfigurationBinder.Bind%2A) , aby powiązać `TransientFaultHandlingOptions` klasę z `"TransientFaultHandlingOptions"` sekcją.
* Wyświetla dane konfiguracji.

:::code language="csharp" source="snippets/configuration/console-json/Program.cs" range="31-38":::

W poprzednim kodzie zmiany w pliku konfiguracji JSON po rozpoczęciu aplikacji są odczytywane.

[`ConfigurationBinder.Get<T>`](xref:Microsoft.Extensions.Configuration.ConfigurationBinder.Get%2A) tworzy powiązania i zwraca określony typ. `ConfigurationBinder.Get<T>` może być wygodniejsze niż używanie `ConfigurationBinder.Bind` . Poniższy kod przedstawia sposób użycia `ConfigurationBinder.Get<T>` z `TransientFaultHandlingOptions` klasą:

```csharp
IConfigurationRoot configurationRoot = configuration.Build();

var options =
    configurationRoot.GetSection(nameof(TransientFaultHandlingOptions))
        .Get<TransientFaultHandlingOptions>();

Console.WriteLine($"TransientFaultHandlingOptions.Enabled={options.Enabled}");
Console.WriteLine($"TransientFaultHandlingOptions.AutoRetryDelay={options.AutoRetryDelay}");
```

W poprzednim kodzie zmiany w pliku konfiguracji JSON po rozpoczęciu aplikacji są odczytywane.

Alternatywne podejście w przypadku używania wzorca opcji ma na celu powiązanie `"TransientFaultHandlingOptions"` sekcji i dodanie jej do [kontenera usługi iniekcji zależności](dependency-injection.md). W poniższym kodzie `TransientFaultHandlingOptions` został dodany do kontenera usługi z <xref:Microsoft.Extensions.DependencyInjection.OptionsConfigurationServiceCollectionExtensions.Configure%2A> i powiązana z konfiguracją:

```csharp
services.Configure<TransientFaultHandlingOptions>(
    configurationRoot.GetSection(
        key: nameof(TransientFaultHandlingOptions)));
```

> [!TIP]
> `key`Parametr jest nazwą sekcji konfiguracji do wyszukania. *Nie musi być* zgodna z nazwą typu, który go reprezentuje. Na przykład można mieć sekcję o nazwie `"FaultHandling"` i może być reprezentowana przez `TransientFaultHandlingOptions` klasę. W tym przypadku zamiast tego przejdziesz `"FaultHandling"` do <xref:Microsoft.Extensions.Configuration.IConfiguration.GetSection%2A> funkcji. `nameof`Operator jest używany jako wygoda, gdy nazwana sekcja pasuje do typu, do którego odnosi się.

Korzystając z powyższego kodu, poniższy kod odczytuje opcje pozycji:

:::code language="csharp" source="snippets/configuration/console-json/ExampleService.cs":::

W powyższym kodzie zmiany w pliku konfiguracji JSON po rozpoczęciu aplikacji **są *** nie_. Aby odczytać zmiany po rozpoczęciu pracy aplikacji, użyj [IOptionsSnapshot](#use-ioptionssnapshot-to-read-updated-data).

## <a name="options-interfaces"></a>Interfejsy opcji

<xref:Microsoft.Extensions.Options.IOptions%601>:

- Nie _*_obsługuje:_*_
  - Odczytywanie danych konfiguracji po rozpoczęciu aplikacji.
  - [Nazwane opcje](#named-options-support-using-iconfigurenamedoptions)
- Jest zarejestrowany jako [pojedynczy](dependency-injection.md#singleton) i można go wstrzyknąć w dowolnym [okresie istnienia usługi](dependency-injection.md#service-lifetimes).

<xref:Microsoft.Extensions.Options.IOptionsSnapshot%601>:

- Jest przydatne w scenariuszach, w których opcje powinny być ponownie obliczane dla każdego rozpoznawania iniekcji w [zakresie lub przejściowych okresach istnienia](dependency-injection.md#service-lifetimes). Aby uzyskać więcej informacji, zobacz [Użyj IOptionsSnapshot do odczytu zaktualizowanych danych](#use-ioptionssnapshot-to-read-updated-data).
- Jest zarejestrowany jako [zakres](dependency-injection.md#scoped) i w związku z tym nie można go wstrzyknąć do pojedynczej usługi.
- Obsługuje [nazwane opcje](#named-options-support-using-iconfigurenamedoptions)

<xref:Microsoft.Extensions.Options.IOptionsMonitor%601>:

- Służy do pobierania opcji i zarządzania powiadomieniami o `TOptions` wystąpieniach.
- Jest zarejestrowany jako [pojedynczy](dependency-injection.md#singleton) i można go wstrzyknąć w dowolnym [okresie istnienia usługi](dependency-injection.md#service-lifetimes).
- Uguje
  - Powiadomienia o zmianie
  - [Nazwane opcje](#named-options-support-using-iconfigurenamedoptions)
  - [Konfiguracja do ponownego ładowania](#use-ioptionssnapshot-to-read-updated-data)
  - Unieważnianie opcji selektywnych ( <xref:Microsoft.Extensions.Options.IOptionsMonitorCache%601> )
  
<xref:Microsoft.Extensions.Options.IOptionsFactory%601> jest odpowiedzialny za tworzenie nowych wystąpień opcji. Ma jedną <xref:Microsoft.Extensions.Options.IOptionsFactory%601.Create%2A> metodę. Domyślna implementacja przyjmuje wszystkie zarejestrowane <xref:Microsoft.Extensions.Options.IConfigureOptions%601> i <xref:Microsoft.Extensions.Options.IPostConfigureOptions%601> uruchamia najpierw wszystkie konfiguracje, po których następuje po zakończeniu konfiguracji. Odróżnia między <xref:Microsoft.Extensions.Options.IConfigureNamedOptions%601> i <xref:Microsoft.Extensions.Options.IConfigureOptions%601> i tylko wywołuje odpowiedni interfejs.

<xref:Microsoft.Extensions.Options.IOptionsMonitorCache%601> jest używany przez program <xref:Microsoft.Extensions.Options.IOptionsMonitor%601> do buforowania `TOptions` wystąpień. <xref:Microsoft.Extensions.Options.IOptionsMonitorCache%601>Unieważnia wystąpienia opcji w monitorze, aby wartość była ponownie obliczana ( <xref:Microsoft.Extensions.Options.IOptionsMonitorCache%601.TryRemove%2A> ). Wartości można wprowadzać ręcznie przy użyciu <xref:Microsoft.Extensions.Options.IOptionsMonitorCache%601.TryAdd%2A> . <xref:Microsoft.Extensions.Options.IOptionsMonitorCache%601.Clear%2A>Metoda jest używana, gdy wszystkie nazwane wystąpienia powinny być ponownie tworzone na żądanie.

## <a name="use-ioptionssnapshot-to-read-updated-data"></a>Użyj IOptionsSnapshot do odczytu zaktualizowanych danych

w przypadku korzystania <xref:Microsoft.Extensions.Options.IOptionsSnapshot%601> z programu opcje są obliczane raz dla każdego żądania, gdy uzyskuje się dostęp i są buforowane przez okres istnienia żądania. Zmiany w konfiguracji są odczytywane po uruchomieniu aplikacji podczas korzystania z dostawców konfiguracji, którzy obsługują odczytywanie zaktualizowanych wartości konfiguracji.

Różnica między `IOptionsMonitor` i `IOptionsSnapshot` to:

- `IOptionsMonitor` jest [usługą singleton](dependency-injection.md#singleton) , która pobiera bieżące wartości opcji w dowolnym momencie, która jest szczególnie przydatna w pojedynczych zależnościach.
- `IOptionsSnapshot` jest [usługą objętą zakresem](dependency-injection.md#scoped) i zawiera migawkę opcji w czasie `IOptionsSnapshot<T>` konstruowania obiektu. Migawki opcji są przeznaczone do użycia z zależnościami przejściowymi i zakresowymi.

Poniższy kod używa <xref:Microsoft.Extensions.Options.IOptionsSnapshot%601> .

:::code language="csharp" source="snippets/configuration/console-json/ScopedService.cs":::

Poniższy kod rejestruje wystąpienie konfiguracji, które `TransientFaultHandlingOptions` wiąże się z:

```csharp
services.Configure<TransientFaultHandlingOptions>(
    configurationRoot.GetSection(
        nameof(TransientFaultHandlingOptions)));
```

W poprzednim kodzie zmiany w pliku konfiguracji JSON po rozpoczęciu aplikacji są odczytywane.

## <a name="ioptionsmonitor"></a>IOptionsMonitor

Poniższy kod rejestruje wystąpienie konfiguracji, które `TransientFaultHandlingOptions` wiąże się z.

```csharp
services.Configure<TransientFaultHandlingOptions>(
    configurationRoot.GetSection(
        nameof(TransientFaultHandlingOptions)));
```

W poniższym przykładzie zastosowano <xref:Microsoft.Extensions.Options.IOptionsMonitor%601> :

:::code language="csharp" source="snippets/configuration/console-json/MonitorService.cs":::

W poprzednim kodzie zmiany w pliku konfiguracji JSON po rozpoczęciu aplikacji są odczytywane.

## <a name="named-options-support-using-iconfigurenamedoptions"></a>Obsługa nazwanych opcji przy użyciu IConfigureNamedOptions

Nazwane opcje:

- Są przydatne, gdy wiele sekcji konfiguracji wiąże się z tymi samymi właściwościami.
- Uwzględnia wielkość liter.

Rozważmy następujące _appsettings.jspliku *:

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

Zamiast tworzyć dwie klasy do powiązania `Features:Personalize` i `Features:WeatherStation` , dla każdej sekcji jest używana następująca Klasa:

```csharp
public class Features
{
    public const string Personalize = nameof(Personalize);
    public const string WeatherStation = nameof(WeatherStation);

    public bool Enabled { get; set; }
    public string ApiKey { get; set; }
}
```

Poniższy kod umożliwia skonfigurowanie nazwanych opcji:

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

Poniższy kod wyświetla nazwane opcje:

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

Wszystkie opcje są nazwanymi wystąpieniami. <xref:Microsoft.Extensions.Options.IConfigureOptions%601> wystąpienia są traktowane jako docelowe dla `Options.DefaultName` wystąpienia, czyli `string.Empty` . <xref:Microsoft.Extensions.Options.IConfigureNamedOptions%601> implementuje także <xref:Microsoft.Extensions.Options.IConfigureOptions%601> . Domyślna implementacja <xref:Microsoft.Extensions.Options.IOptionsFactory%601> logiki ma na celu odpowiednie użycie. `null`Nazwana opcja służy do określania wszystkich wystąpień nazwanych zamiast określonego wystąpienia nazwanego. <xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.ConfigureAll%2A> i <xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.PostConfigureAll%2A> Użyj tej Konwencji.

## <a name="optionsbuilder-api"></a>Interfejs API OptionsBuilder

<xref:Microsoft.Extensions.Options.OptionsBuilder%601> służy do konfigurowania `TOptions` wystąpień. `OptionsBuilder` usprawnia Tworzenie nazwanych opcji, ponieważ jest tylko pojedynczym parametrem do początkowego `AddOptions<TOptions>(string optionsName)` wywołania, a nie pojawia się we wszystkich kolejnych wywołaniach. Sprawdzanie poprawności opcji i `ConfigureOptions` przeciążenia, które akceptują zależności usługi, są dostępne tylko za pośrednictwem programu `OptionsBuilder` .

`OptionsBuilder` jest używany w sekcji [Walidacja opcji](#options-validation) .

## <a name="use-di-services-to-configure-options"></a>Korzystanie z usług DI Services w celu konfigurowania opcji

Usługi są dostępne z iniekcji zależności podczas konfigurowania opcji na dwa sposoby:

- Przekaż delegat konfiguracji w celu [skonfigurowania](xref:Microsoft.Extensions.Options.OptionsBuilder%601.Configure%2A) w usłudze [OptionsBuilder \<TOptions> ](xref:Microsoft.Extensions.Options.OptionsBuilder%601). `OptionsBuilder<TOptions>` zapewnia przeciążenia [konfiguracji](xref:Microsoft.Extensions.Options.OptionsBuilder%601.Configure%2A) , które umożliwiają korzystanie z maksymalnie pięciu usług w celu konfigurowania opcji:

  ```csharp
  services.AddOptions<MyOptions>("optionalName")
      .Configure<ExampleService, ScopedService, MonitorService>(
          (options, es, ss, ms) =>
              options.Property = DoSomethingWith(es, ss, ms));
  ```

- Utwórz typ, który implementuje <xref:Microsoft.Extensions.Options.IConfigureOptions%601> lub <xref:Microsoft.Extensions.Options.IConfigureNamedOptions%601> i rejestruje typ jako usługę.

Zalecamy przekazanie delegata konfiguracji w celu [skonfigurowania](xref:Microsoft.Extensions.Options.OptionsBuilder%601.Configure%2A), ponieważ tworzenie usługi jest bardziej skomplikowane. Tworzenie typu jest równoznaczne z tym, co platforma wykonuje podczas wywoływania [konfiguracji](xref:Microsoft.Extensions.Options.OptionsBuilder%601.Configure%2A). Wywołanie [konfiguracji](xref:Microsoft.Extensions.Options.OptionsBuilder%601.Configure%2A) rejestruje przejściowe ogólne <xref:Microsoft.Extensions.Options.IConfigureNamedOptions%601> , który ma konstruktora akceptującego określone typy usług ogólnych.

## <a name="options-validation"></a>Sprawdzanie poprawności opcji

Sprawdzanie poprawności opcji umożliwia zweryfikowanie wartości opcji.

Rozważmy następujące *appsettings.js* pliku:

```json
{
  "Settings": {
    "SiteTitle": "Amazing docs from Awesome people!",
    "Scale": 10,
    "VerbosityLevel": 32
  }
}
```

Następująca Klasa wiąże się z `"Settings"` sekcją konfiguracji i stosuje kilka `DataAnnotations` reguł:

:::code language="csharp" source="snippets/configuration/console-json/SettingsOptions.cs":::

Następujący kod:

- Wywołuje metodę <xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.AddOptions%2A> get [OptionsBuilder \<TOptions> ](xref:Microsoft.Extensions.Options.OptionsBuilder%601) , która wiąże się z `SettingsOptions` klasą.
- Wywołania umożliwiające <xref:Microsoft.Extensions.DependencyInjection.OptionsBuilderDataAnnotationsExtensions.ValidateDataAnnotations%2A> włączenie walidacji przy użyciu `DataAnnotations` .

```csharp
services.AddOptions<SettingsOptions>()
    .Bind(Configuration.GetSection(SettingsOptions.Settings))
    .ValidateDataAnnotations();
```

`ValidateDataAnnotations`Metoda rozszerzenia jest zdefiniowana w pakiecie NuGet [Microsoft. Extensions. options. DataAnnotations](https://www.nuget.org/packages/Microsoft.Extensions.Options.DataAnnotations) .

Poniższy kod wyświetla wartości konfiguracyjne lub błędy walidacji:

:::code language="csharp" source="snippets/configuration/console-json/ValidationService.cs":::

Poniższy kod stosuje bardziej złożoną regułę walidacji przy użyciu delegata:

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

### <a name="ivalidateoptions-for-complex-validation"></a>IValidateOptions na potrzeby złożonej walidacji

Następująca Klasa implementuje <xref:Microsoft.Extensions.Options.IValidateOptions%601> :

:::code language="csharp" source="snippets/configuration/console-json/ValidateSettingsOptions.cs":::

`IValidateOptions` umożliwia przeniesienie kodu weryfikacyjnego do klasy.

Przy użyciu powyższego kodu sprawdzanie poprawności jest włączane w programie `ConfigureServices` przy użyciu następującego kodu:

```csharp
services.Configure<SettingsOptions>(
    Configuration.GetSection(
        SettingsOptions.Settings));
services.TryAddEnumerable(
    ServiceDescriptor.Singleton
        <IValidateOptions<SettingsOptions>, ValidateSettingsOptions>());
```

## <a name="options-post-configuration"></a>Opcje po konfiguracji

Ustaw wartość po konfiguracji za pomocą <xref:Microsoft.Extensions.Options.IPostConfigureOptions%601> . Po wykonaniu wszystkich czynności konfiguracja zostanie uruchomiona po zakończeniu konfiguracji <xref:Microsoft.Extensions.Options.IConfigureOptions%601> , co może być przydatne w scenariuszach, gdy trzeba przesłonić konfigurację:

```csharp
services.PostConfigure<CustomOptions>(customOptions =>
{
    customOptions.Option1 = "post_configured_option1_value";
});
```

<xref:Microsoft.Extensions.Options.IPostConfigureOptions%601.PostConfigure%2A> jest dostępny do po skonfigurowaniu nazwanych opcji:

```csharp
services.PostConfigure<CustomOptions>("named_options_1", customOptions =>
{
    customOptions.Option1 = "post_configured_option1_value";
});
```

Użyj <xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.PostConfigureAll%2A> , aby skonfigurować wszystkie wystąpienia konfiguracji:

```csharp
services.PostConfigureAll<CustomOptions>(customOptions =>
{
    customOptions.Option1 = "post_configured_option1_value";
});
```

## <a name="see-also"></a>Zobacz także

- [Konfiguracja w programie .NET](configuration.md)
