---
title: Konfiguracja aplikacji
description: Dowiedz się, jak skonfigurować Blazor aplikacje bez korzystania z programu ConfigurationManager.
author: csharpfritz
ms.author: jefritz
no-loc:
- Blazor
ms.date: 11/20/2020
ms.openlocfilehash: 360d9077bc981a2e9875bb1f86b49c0029424d6e
ms.sourcegitcommit: 2f485e721f7f34b87856a51181b5b56624b31fd5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/02/2020
ms.locfileid: "96509796"
---
# <a name="app-configuration"></a>Konfiguracja aplikacji

Podstawowym sposobem ładowania konfiguracji aplikacji w formularzach sieci Web jest wprowadzenie wpisów w pliku *web.config* &mdash; na serwerze lub związanym pliku konfiguracji, do którego odwołuje się *web.config*. Można użyć obiektu statycznego `ConfigurationManager` do współpracy z ustawieniami aplikacji, parametrami połączenia repozytorium danych i innymi dostawcami konfiguracji rozszerzonej, które są dodawane do aplikacji. Typowym sposobem jest wyświetlenie interakcji z konfiguracją aplikacji, jak pokazano w poniższym kodzie:

```csharp
var configurationValue = ConfigurationManager.AppSettings["ConfigurationSettingName"];
var connectionString = ConfigurationManager.ConnectionStrings["MyDatabaseConnectionName"].ConnectionString;
```

W przypadku ASP.NET Core i po stronie serwera Blazor *web.config* plik może być obecny, jeśli aplikacja jest hostowana na serwerze Windows IIS. Nie ma jednak `ConfigurationManager` interakcji z tą konfiguracją i można uzyskać bardziej strukturalną konfigurację aplikacji z innych źródeł. Zapoznaj się z informacjami na temat sposobu zbierania konfiguracji i uzyskiwania dostępu do informacji konfiguracyjnych z pliku *web.config* .

## <a name="configuration-sources"></a>Źródła konfiguracji

ASP.NET Core rozpoznaje istnieje wiele źródeł konfiguracji, które mogą być używane w aplikacji. Platforma próbuje domyślnie oferować najlepsze z tych funkcji. Konfiguracja jest odczytywana i agregowana z tych różnych źródeł przez ASP.NET Core. Późniejsze wartości załadowane dla tego samego klucza konfiguracji mają pierwszeństwo przed wcześniejszymi wartościami.

ASP.NET Core została zaprojektowana tak, aby była oparta na chmurze, a konfiguracja aplikacji była łatwiejsza dla operatorów i deweloperów. ASP.NET Core jest oparta na środowisku i wie, że jest uruchomiona w `Production` środowisku lub `Development` . Wskaźnik środowiska jest ustawiany w `ASPNETCORE_ENVIRONMENT` zmiennej środowiskowej system. Jeśli żadna wartość nie jest skonfigurowana, domyślnie działa w `Production` środowisku.

Aplikacja może wyzwolić konfigurację i dodać ją z kilku źródeł na podstawie nazwy środowiska. Domyślnie konfiguracja jest ładowana z następujących zasobów w podanej kolejności:

1. *appsettings.jsw* pliku, jeśli jest obecny
1. *appSettings. {ENVIRONMENT_NAME}. plik JSON* (jeśli istnieje)
1. Plik tajny użytkownika na dysku, jeśli jest obecny
1. Zmienne środowiskowe
1. Argumenty wiersza polecenia

## <a name="appsettingsjson-format-and-access"></a>appsettings.jsw formacie i dostępie

*appsettings.jsw* pliku może być hierarchiczny z wartościami strukturalnymi, takimi jak poniższy kod JSON:

```json
{
  "section0": {
    "key0": "value",
    "key1": "value"
  },
  "section1": {
    "key0": "value",
    "key1": "value"
  }
}
```

W przypadku powyższego kodu JSON system konfiguracji spłaszcza wartości podrzędne i odwołuje się do ich w pełni kwalifikowanych hierarchicznych ścieżek. Znak dwukropka ( `:` ) oddziela każdą właściwość w hierarchii. Na przykład klucz konfiguracji `section1:key0` uzyskuje dostęp do `section1` wartości literału obiektu `key0` .

## <a name="user-secrets"></a>Wpisy tajne użytkownika

Wpisy tajne użytkownika:

* Wartości konfiguracyjne przechowywane w pliku JSON na stacji roboczej dewelopera poza folderem tworzenia aplikacji.
* Ładowany tylko w `Development` środowisku.
* Skojarzone z określoną aplikacją.
* Zarządzana za pomocą polecenia interfejsu CLI platformy .NET `user-secrets` .

Skonfiguruj aplikację do przechowywania wpisów tajnych, wykonując `user-secrets` polecenie:

```dotnetcli
dotnet user-secrets init
```

Poprzednie polecenie dodaje `UserSecretsId` element do pliku projektu. Element zawiera identyfikator GUID, który jest używany do kojarzenia wpisów tajnych z aplikacją. Następnie można zdefiniować wpis tajny za pomocą `set` polecenia. Na przykład:

```dotnetcli
dotnet user-secrets set "Parent:ApiKey" "12345"
```

Poprzednie polecenie sprawia, że `Parent:ApiKey` klucz konfiguracji jest dostępny na stacji roboczej dewelopera z wartością `12345` .

Aby uzyskać więcej informacji na temat tworzenia, przechowywania i zarządzania kluczami tajnymi użytkowników, zobacz [bezpieczny magazyn wpisów tajnych aplikacji w programie Development w ASP.NET Core](/aspnet/core/security/app-secrets) dokumencie.

## <a name="environment-variables"></a>Zmienne środowiskowe

Następny zbiór wartości załadowanych do konfiguracji aplikacji jest zmiennymi środowiskowymi systemu. Wszystkie ustawienia zmiennych środowiskowych systemu są teraz dostępne przez interfejs API konfiguracji. Wartości hierarchiczne są spłaszczone i oddzielane średnikami podczas odczytu w aplikacji. Jednak niektóre systemy operacyjne nie zezwalają na nazwy zmiennych środowiskowych. ASP.NET Core rozwiązuje to ograniczenie przez konwertowanie wartości, które mają podwójne podkreślenia ( `__` ) na dwukropek, gdy są dostępne. `Parent:ApiKey`Wartość z powyższej sekcji Secret użytkownika może zostać zastąpiona zmienną środowiskową `Parent__ApiKey` .

## <a name="command-line-arguments"></a>Argumenty wiersza polecenia

Konfigurację można również określić jako argumenty wiersza polecenia, gdy aplikacja jest uruchomiona. Użyj podwójnej kreski ( `--` ) lub zapisu do przodu ( `/` ), aby wskazać nazwę wartości konfiguracji do ustawienia i wartość do skonfigurowania. Składnia przypomina następujące polecenia:

```dotnetcli
dotnet run CommandLineKey1=value1 --CommandLineKey2=value2 /CommandLineKey3=value3
dotnet run --CommandLineKey1 value1 /CommandLineKey2 value2
dotnet run Parent:ApiKey=67890
```

## <a name="the-return-of-webconfig"></a>Zwrot web.config

Jeśli aplikacja została wdrożona w systemie Windows w usługach IIS, plik *web.config* nadal KONFIGURUJE usługi IIS do zarządzania aplikacją. Domyślnie usługi IIS dodają odwołanie do modułu ASP.NET Core (ANCM). ANCM to natywny moduł IIS, który hostuje aplikację zamiast serwera sieci Web Kestrel. Ta sekcja *web.config* przypomina następujące znaczniki XML:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <location path="." inheritInChildApplications="false">
    <system.webServer>
      <handlers>
        <add name="aspNetCore" path="*" verb="*" modules="AspNetCoreModuleV2" resourceType="Unspecified" />
      </handlers>
      <aspNetCore processPath=".\MyApp.exe"
                  stdoutLogEnabled="false"
                  stdoutLogFile=".\logs\stdout"
                  hostingModel="inprocess" />
    </system.webServer>
  </location>
</configuration>
```

Konfigurację specyficzną dla aplikacji można zdefiniować przez zagnieżdżanie `environmentVariables` elementu w `aspNetCore` elemencie. Wartości zdefiniowane w tej sekcji są prezentowane ASP.NET Core aplikacji jako zmienne środowiskowe. Zmienne środowiskowe są ładowane odpowiednio w ramach tego segmentu uruchamiania aplikacji.

```xml
<aspNetCore processPath="dotnet"
      arguments=".\MyApp.dll"
      stdoutLogEnabled="false"
      stdoutLogFile=".\logs\stdout"
      hostingModel="inprocess">
  <environmentVariables>
    <environmentVariable name="ASPNETCORE_ENVIRONMENT" value="Development" />
    <environmentVariable name="Parent:ApiKey" value="67890" />
  </environmentVariables>
</aspNetCore>
```

## <a name="read-configuration-in-the-app"></a>Odczytaj konfigurację w aplikacji

ASP.NET Core zapewnia konfigurację aplikacji za pomocą <xref:Microsoft.Extensions.Configuration.IConfiguration> interfejsu. Ten interfejs konfiguracji powinien być żądany przez Blazor składniki, Blazor strony i wszystkie inne klasy zarządzane przez ASP.NET Core, które wymagają dostępu do konfiguracji. Platforma ASP.NET Core automatycznie wypełni ten interfejs ze skonfigurowaną wcześniej rozpoznaną konfiguracją. Na Blazor stronie lub znaczniku Razor składnika można wstrzyknąć `IConfiguration` obiekt z `@inject` dyrektywą w górnej części pliku *. Razor* , jak to:

```razor
@inject IConfiguration Configuration
```

Ta Poprzednia instrukcja sprawia, że `IConfiguration` obiekt jest dostępny jako `Configuration` zmienna w całej pozostałej części szablonu Razor.

Poszczególne ustawienia konfiguracji można odczytać, określając hierarchię ustawień konfiguracji poszukiwaną jako parametr indeksatora:

```csharp
var mySetting = Configuration["section1:key0"];
```

Wszystkie sekcje konfiguracji można pobrać przy użyciu <xref:Microsoft.Extensions.Configuration.IConfiguration.GetSection%2A> metody pobierania kolekcji kluczy w określonej lokalizacji z składnią podobną do `GetSection("section1")` , aby pobrać konfigurację Section1 z wcześniejszego przykładu.

## <a name="strongly-typed-configuration"></a>Konfiguracja o jednoznacznie określonym typie

Za pomocą formularzy sieci Web można utworzyć typ konfiguracji o jednoznacznie określonym typie, który dziedziczy z <xref:System.Configuration.ConfigurationSection> typu i skojarzonych typów. `ConfigurationSection`Można skonfigurować niektóre reguły biznesowe i przetwarzać te wartości konfiguracyjne.

W ASP.NET Core można określić hierarchię klas, która będzie odbierać wartości konfiguracyjne. Następujące klasy:

* Nie trzeba dziedziczyć z klasy nadrzędnej.
* Powinien zawierać `public` właściwości, które pasują do właściwości i typów odwołań dla struktury konfiguracji, która ma zostać przechwycona.

W przypadku wcześniejszych *appsettings.jsna* przykład można zdefiniować następujące klasy do przechwytywania wartości:

```csharp
public class MyConfig
{
    public MyConfigSection section0 { get; set;}

    public MyConfigSection section1 { get; set;}
}

public class MyConfigSection
{
    public string key0 { get; set; }

    public string key1 { get; set; }
}
```

Tę hierarchię klas można wypełnić, dodając następujący wiersz do `Startup.ConfigureServices` metody:

```csharp
services.Configure<MyConfig>(Configuration);
```

W pozostałej części aplikacji można dodać parametr wejściowy do klas lub `@inject` dyrektywy w szablonach Razor typu, `IOptions<MyConfig>` Aby otrzymać ustawienia konfiguracji o jednoznacznie określonym typie. `IOptions<MyConfig>.Value`Właściwość zwróci `MyConfig` wartość wypełnioną z ustawień konfiguracji.

```razor
@inject IOptions<MyConfig> options
@code {
    var MyConfiguration = options.Value;
    var theSetting = MyConfiguration.section1.key0;
}
```

Więcej informacji o funkcji opcji można znaleźć w [wzorcu opcji w ASP.NET Core](/aspnet/core/fundamentals/configuration/options#options-interfaces) dokumencie.

>[!div class="step-by-step"]
>[Poprzedni](middleware.md) 
> [Dalej](security-authentication-authorization.md)
