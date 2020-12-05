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
# <a name="configuration-providers-in-net"></a>Dostawcy konfiguracji w programie .NET

Konfiguracja w programie .NET jest możliwa z dostawcami konfiguracji. Istnieje kilka typów dostawców korzystających z różnych źródeł konfiguracji. Ten artykuł zawiera szczegółowe informacje o różnych dostawcach konfiguracji i odpowiednich źródłach.

- [Dostawca konfiguracji plików](#file-configuration-provider)
- [Dostawca konfiguracji zmiennej środowiskowej](#environment-variable-configuration-provider)
- [Dostawca konfiguracji wiersza polecenia](#command-line-configuration-provider)
- [Dostawca konfiguracji klucza dla plików](#key-per-file-configuration-provider)
- [Dostawca konfiguracji pamięci](#memory-configuration-provider)

## <a name="file-configuration-provider"></a>Dostawca konfiguracji plików

<xref:Microsoft.Extensions.Configuration.FileConfigurationProvider> jest klasą bazową do ładowania konfiguracji z systemu plików. Następujący dostawcy konfiguracji pochodzą z `FileConfigurationProvider` :

- [Dostawca konfiguracji JSON](#json-configuration-provider)
- [Dostawca konfiguracji XML](#xml-configuration-provider)
- [Dostawca konfiguracji pliku INI](#ini-configuration-provider)

### <a name="json-configuration-provider"></a>Dostawca konfiguracji JSON

<xref:Microsoft.Extensions.Configuration.Json.JsonConfigurationProvider>Klasa ładuje konfigurację z pliku JSON. Zainstaluj [`Microsoft.Extensions.Configuration.Json`](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.Json) pakiet NuGet.

Przeciążenia mogą określać:

- Czy plik jest opcjonalny
- Czy konfiguracja zostanie ponownie załadowana w przypadku zmiany pliku

Spójrzmy na poniższy kod:

:::code language="csharp" source="snippets/configuration/console-json/Program.cs" range="1-39,43-44" highlight="23-29":::

Powyższy kod ma następujące działanie:

- Czyści wszystkich istniejących dostawców konfiguracji, którzy zostali dodani domyślnie w <xref:Microsoft.Extensions.Hosting.Host.CreateDefaultBuilder(System.String[])> metodzie.
- Konfiguruje dostawcę konfiguracji JSON w celu załadowania *appsettings.jsw* i  *AppSettings* `Environment` . pliki *JSON* z następującymi opcjami:
  - `optional: true`: Plik jest opcjonalny.
  - `reloadOnChange: true` : Plik zostanie ponownie załadowany podczas zapisywania zmian.

Ustawienia JSON są zastępowane przez ustawienia w obszarze [dostawca konfiguracji zmiennych środowiskowych](#environment-variable-configuration-provider) i [dostawca konfiguracji wiersza polecenia](#command-line-configuration-provider).

Przykład *appsettings.jsw* pliku z różnymi ustawieniami konfiguracji:

:::code language="json" source="snippets/configuration/console-json/appsettings.json":::

Z tego <xref:Microsoft.Extensions.Configuration.IConfigurationBuilder> wystąpienia po dodaniu dostawców konfiguracji można wywołać, <xref:Microsoft.Extensions.Configuration.IConfigurationBuilder.Build?displayProperty=nameWithType> Aby uzyskać <xref:Microsoft.Extensions.Configuration.IConfigurationRoot> obiekt. Katalog główny konfiguracji reprezentuje element główny hierarchii konfiguracji. Sekcje z konfiguracji można powiązać z wystąpieniami obiektów .NET i w późniejszym czasie <xref:Microsoft.Extensions.Options.IOptions%601> za pośrednictwem iniekcji zależności.

Należy wziąć pod uwagę `TransientFaultHandlingOptions` Typ rekordu zdefiniowany w następujący sposób:

:::code language="csharp" source="snippets/configuration/console-json/TransientFaultHandlingOptions.cs":::

Aby uzyskać informacje na temat typów rekordów, zobacz [typy rekordów w języku C# 9](../../csharp/whats-new/csharp-9.md#record-types).

Poniższy kod kompiluje katalog główny konfiguracji, tworzy powiązanie sekcji z `TransientFaultHandlingOptions` typem rekordu i drukuje powiązane wartości do okna konsoli:

:::code language="csharp" source="snippets/configuration/console-json/Program.cs" range="31-38":::

Aplikacja zapisze następujące przykładowe dane wyjściowe:

:::code language="csharp" source="snippets/configuration/console-json/Program.cs" range="40-42":::

### <a name="xml-configuration-provider"></a>Dostawca konfiguracji XML

<xref:Microsoft.Extensions.Configuration.Xml.XmlConfigurationProvider>Klasa ładuje konfigurację z pliku XML w czasie wykonywania. Zainstaluj [`Microsoft.Extensions.Configuration.Xml`](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.Xml) pakiet NuGet.

Poniższy kod ilustruje konfigurację plików XML przy użyciu dostawcy konfiguracji XML.

:::code language="csharp" source="snippets/configuration/console-xml/Program.cs" range="1-34,52,58-59" highlight="23-34":::

Powyższy kod ma następujące działanie:

- Czyści wszystkich istniejących dostawców konfiguracji, którzy zostali dodani domyślnie w <xref:Microsoft.Extensions.Hosting.Host.CreateDefaultBuilder(System.String[])> metodzie.
- Konfiguruje dostawcę konfiguracji XML do ładowania *appsettings.xml* i *repeating-example.xml* plików z następującymi opcjami:
  - `optional: true`: Plik jest opcjonalny.
  - `reloadOnChange: true` : Plik zostanie ponownie załadowany podczas zapisywania zmian.
- Konfiguruje dostawcę konfiguracji zmiennych środowiskowych.
- Konfiguruje dostawcę konfiguracji wiersza polecenia, jeśli podano `args` argumenty.

Ustawienia XML są zastępowane przez ustawienia w obszarze [dostawca konfiguracji zmiennych środowiskowych](#environment-variable-configuration-provider) i [dostawca konfiguracji wiersza polecenia](#command-line-configuration-provider).

Przykładowy plik *appsettings.xml* z różnymi ustawieniami konfiguracji:

:::code language="xml" source="snippets/configuration/console-xml/appsettings.xml":::

Powtarzające się elementy, które używają tej samej nazwy elementu, działają, jeśli `name` atrybut jest używany do odróżnienia elementów:

:::code language="xml" source="snippets/configuration/console-xml/repeating-example.xml":::

Poniższy kod odczytuje poprzedni plik konfiguracji i wyświetla klucze i wartości:

:::code language="csharp" source="snippets/configuration/console-xml/Program.cs" range="36-51":::

Aplikacja zapisze następujące przykładowe dane wyjściowe:

:::code language="csharp" source="snippets/configuration/console-xml/Program.cs" range="53-57":::

Atrybuty mogą służyć do dostarczania wartości:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <key attribute="value" />
  <section>
    <key attribute="value" />
  </section>
</configuration>
```

Poprzedni plik konfiguracji ładuje następujące klucze z `value` :

- `key:attribute`
- `section:key:attribute`

### <a name="ini-configuration-provider"></a>Dostawca konfiguracji pliku INI

<xref:Microsoft.Extensions.Configuration.Ini.IniConfigurationProvider>Klasa ładuje konfigurację z pliku ini w czasie wykonywania. Zainstaluj [`Microsoft.Extensions.Configuration.Ini`](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.Ini)  pakiet NuGet.

Poniższy kod czyści wszystkich dostawców konfiguracji i dodaje `IniConfigurationProvider` dwa pliki ini jako Źródło:

:::code language="csharp" source="snippets/configuration/console-ini/Program.cs" range="1-37,44-45" highlight="24-30":::

Przykładowy plik *appsettings.ini* z różnymi ustawieniami konfiguracji:

:::code language="ini" source="snippets/configuration/console-ini/appsettings.ini":::

Poniższy kod wyświetla poprzednie ustawienia konfiguracji, pisząc je w oknie konsoli:

:::code language="csharp" source="snippets/configuration/console-ini/Program.cs" range="32-36":::

Aplikacja zapisze następujące przykładowe dane wyjściowe:

:::code language="csharp" source="snippets/configuration/console-ini/Program.cs" range="38-43":::

## <a name="environment-variable-configuration-provider"></a>Dostawca konfiguracji zmiennej środowiskowej

Przy użyciu konfiguracji domyślnej, <xref:Microsoft.Extensions.Configuration.EnvironmentVariables.EnvironmentVariablesConfigurationProvider> Ładowanie konfiguracji ze zmiennej środowiskowej par klucz-wartość po czytaniu *appsettings.jsw*, *appSettings.* `Environment` *. JSON* i Menedżer wpisów tajnych. W związku z tym kluczowe wartości są odczytywane z wartości zastąpienia środowiska odczytywane z *appsettings.jsw*, *appSettings.* `Environment` *. JSON* i Menedżer wpisów tajnych.

`:`Separator nie działa ze zmiennymi kluczy hierarchicznych na wszystkich platformach. Podwójne podkreślenie ( `__` ) jest automatycznie zastępowane przez `:` i jest obsługiwane przez wszystkie platformy. Na przykład `:` separator nie jest obsługiwany przez [bash](https://linuxhint.com/bash-environment-variables), ale `__` jest.

Następujące `set` polecenia:

- Ustaw klucze środowiska i wartości z poprzedniego przykładu w systemie Windows.
- Przetestuj ustawienia, zmieniając ich wartości domyślne. `dotnet run`Polecenie musi być uruchamiane w katalogu projektu.

```dotnetcli
set SecretKey="Secret key from environment"
set TransientFaultHandlingOptions__Enabled="true"
set TransientFaultHandlingOptions__AutoRetryDelay="00:00:13"

dotnet run
```

Poprzednie ustawienia środowiska:

- Są ustawiane tylko w ramach procesów uruchomionych z poziomu okna polecenia, które zostały ustawione w.
- Nie będą odczytywane przez aplikacje sieci Web uruchomione przy użyciu programu Visual Studio.

Następujące polecenia [setx](/windows-server/administration/windows-commands/setx) mogą służyć do ustawiania kluczy środowiskowych i wartości w systemie Windows. W przeciwieństwie do `set` , `setx` Ustawienia są utrwalane. `/M` ustawia zmienną w środowisku systemowym. Jeśli `/M` przełącznik nie jest używany, zmienna środowiskowa użytkownika jest ustawiona.

```dotnetcli
setx SecretKey "Secret key from setx environment" /M
setx TransientFaultHandlingOptions__Enabled "true" /M
setx TransientFaultHandlingOptions__AutoRetryDelay "00:00:05" /M

dotnet run
```

Aby sprawdzić, czy poprzednie polecenia zastępują *appsettings.js* i *appSettings.* `Environment` *. JSON*:

- Za pomocą programu Visual Studio: Zamknij i uruchom ponownie program Visual Studio.
- Za pomocą interfejsu wiersza polecenia: Uruchom nowe okno poleceń i wprowadź `dotnet run` .

Połącz <xref:Microsoft.Extensions.Configuration.EnvironmentVariablesExtensions.AddEnvironmentVariables%2A> z ciągiem, aby określić prefiks dla zmiennych środowiskowych:

:::code language="csharp" source="snippets/configuration/console-env/Program.cs" highlight="21-22":::

Powyższy kod ma następujące działanie:

- `config.AddEnvironmentVariables(prefix: "CustomPrefix_")` zostanie dodany po domyślnych dostawcach konfiguracji. Przykład określania kolejności dostawców konfiguracji można znaleźć w temacie [dostawca konfiguracji XML](#xml-configuration-provider).
- Zmienne środowiskowe ustawione z `CustomPrefix_` prefiksem przesłaniają domyślnych dostawców konfiguracji. Obejmuje to zmienne środowiskowe bez prefiksu.

Prefiks jest usuwany, gdy pary klucz konfiguracji-wartość są odczytywane.

Następujące polecenia testują prefiks niestandardowy:

```dotnetcli
set CustomPrefix__SecretKey="Secret key with CustomPrefix_ environment"
set CustomPrefix_TransientFaultHandlingOptions__Enabled=true
set CustomPrefix_TransientFaultHandlingOptions__AutoRetryDelay=00:00:21

dotnet run
```

Konfiguracja domyślna ładuje zmienne środowiskowe i argumenty wiersza polecenia poprzedzone prefiksem `DOTNET_` . `DOTNET_`Prefiks jest używany przez platformę .NET do [konfiguracji](generic-host.md#app-configuration) [hosta](generic-host.md#host-configuration) i aplikacji, ale nie do konfiguracji użytkownika.

Aby uzyskać więcej informacji na temat konfiguracji hosta i aplikacji, zobacz [host ogólny programu .NET](generic-host.md).

Na [Azure App Service](https://azure.microsoft.com/services/app-service)wybierz pozycję **nowe ustawienie aplikacji** na stronie **Konfiguracja > ustawienia** . Ustawienia aplikacji Azure App Service są następujące:

- Szyfrowane i przesyłane przez zaszyfrowanego kanału.
- Uwidocznione jako zmienne środowiskowe.

### <a name="connection-string-prefixes"></a>Prefiksy parametrów połączenia

Interfejs API konfiguracji ma specjalne reguły przetwarzania dla czterech zmiennych środowiskowych parametrów połączenia. Te parametry połączenia są związane z konfigurowaniem parametrów połączenia platformy Azure dla środowiska aplikacji. Zmienne środowiskowe z prefiksami podanymi w tabeli są ładowane do aplikacji z konfiguracją domyślną lub gdy nie podano prefiksu `AddEnvironmentVariables` .

| Prefiks parametrów połączenia | Dostawca                                                                |
|--------------------------|-------------------------------------------------------------------------|
| `CUSTOMCONNSTR_`         | Dostawca niestandardowy                                                         |
| `MYSQLCONNSTR_`          | [MySQL](https://www.mysql.com)                                          |
| `SQLAZURECONNSTR_`       | [Azure SQL Database](https://azure.microsoft.com/services/sql-database) |
| `SQLCONNSTR_`            | [SQL Server](https://www.microsoft.com/sql-server)                      |

Gdy zmienna środowiskowa zostanie odnaleziona i załadowana do konfiguracji z dowolnymi z czterech prefiksów pokazanych w tabeli:

- Klucz konfiguracji jest tworzony przez usunięcie prefiksu zmiennej środowiskowej i dodanie sekcji klucza konfiguracji ( `ConnectionStrings` ).
- Zostanie utworzona nowa para klucz-wartość konfiguracji, która reprezentuje dostawcę połączenia bazy danych (z wyjątkiem tego `CUSTOMCONNSTR_` , który nie ma określonego dostawcy).

| Klucz zmiennej środowiskowej | Przekonwertowany klucz konfiguracji | Wpis konfiguracji dostawcy                                                    |
|--------------------------|-----------------------------|---------------------------------------------------------------------------------|
| `CUSTOMCONNSTR_{KEY}`    | `ConnectionStrings:{KEY}`   | Wpis konfiguracji nie został utworzony.                                                |
| `MYSQLCONNSTR_{KEY}`     | `ConnectionStrings:{KEY}`   | Klucz: `ConnectionStrings:{KEY}_ProviderName` :<br>Wartość: `MySql.Data.MySqlClient` |
| `SQLAZURECONNSTR_{KEY}`  | `ConnectionStrings:{KEY}`   | Klucz: `ConnectionStrings:{KEY}_ProviderName` :<br>Wartość: `System.Data.SqlClient`  |
| `SQLCONNSTR_{KEY}`       | `ConnectionStrings:{KEY}`   | Klucz: `ConnectionStrings:{KEY}_ProviderName` :<br>Wartość: `System.Data.SqlClient`  |

### <a name="environment-variables-set-in-launchsettingsjson"></a>Zmienne środowiskowe ustawione w launchSettings.jsna

Zmienne środowiskowe ustawione w *launchSettings.jsna* zastępują te ustawienia w środowisku systemowym.

## <a name="command-line-configuration-provider"></a>Dostawca konfiguracji wiersza polecenia

Korzystając z konfiguracji domyślnej, <xref:Microsoft.Extensions.Configuration.CommandLine.CommandLineConfigurationProvider> ładuje konfigurację z par klucz-wartość argumentu wiersza polecenia po następujących źródłach konfiguracji:

- *appsettings.jsna* i *AppSettings*. `Environment` . pliki *JSON* .
- Wpisy tajne aplikacji (Secret Manager) w `Development` środowisku.
- Zmienne środowiskowe.

Domyślnie wartości konfiguracyjne ustawione w wierszu polecenia przesłaniają wartości konfiguracyjne ustawione dla wszystkich innych dostawców konfiguracji.

### <a name="command-line-arguments"></a>Argumenty wiersza polecenia

Następujące polecenie ustawia klucze i wartości przy użyciu `=` :

```dotnetcli
dotnet run SecretKey="Secret key from command line"
```

Następujące polecenie ustawia klucze i wartości przy użyciu `/` :

```dotnetcli
dotnet run /SecretKey "Secret key set from forward slash"
```

Następujące polecenie ustawia klucze i wartości przy użyciu `--` :

```dotnetcli
dotnet run --SecretKey "Secret key set from double hyphen"
```

Wartość klucza:

- Musi `=` być zgodna lub musi mieć prefiks lub, gdy wartość znajduje się w `--` `/` miejscu.
- Nie jest wymagane, jeśli `=` jest używany. Na przykład `SomeKey=`.

W tym samym poleceniu nie należy mieszać par klucz-wartość argumentu wiersza polecenia, które są używane `=` z parami klucz-wartość, które używają spacji.

## <a name="key-per-file-configuration-provider"></a>Dostawca konfiguracji klucza dla plików

<xref:Microsoft.Extensions.Configuration.KeyPerFile.KeyPerFileConfigurationProvider>Używa plików katalogu jako par klucz konfiguracji i wartość. Kluczem jest nazwa pliku. Wartość jest zawartością pliku. Dostawca konfiguracji klucza dla plików jest używany w scenariuszach hostingu platformy Docker.

Aby uaktywnić konfigurację klucza dla plików, wywołaj <xref:Microsoft.Extensions.Configuration.KeyPerFileConfigurationBuilderExtensions.AddKeyPerFile%2A> metodę rozszerzenia w wystąpieniu <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder> . `directoryPath`Do plików musi być ścieżką bezwzględną.

Przeciążania Zezwalaj na określanie:

- `Action<KeyPerFileConfigurationSource>`Delegat, który konfiguruje źródło.
- Określa, czy katalog jest opcjonalny, i ścieżkę do katalogu.

Podwójny znak podkreślenia ( `__` ) jest używany jako ogranicznik klucza konfiguracji w nazwach plików. Na przykład nazwa pliku `Logging__LogLevel__System` generuje klucz konfiguracji `Logging:LogLevel:System` .

Wywołaj `ConfigureAppConfiguration` podczas kompilowania hosta, aby określić konfigurację aplikacji:

```csharp
.ConfigureAppConfiguration((_, configuration) =>
{
    var path = Path.Combine(
        Directory.GetCurrentDirectory(), "path/to/files");

    configuration.AddKeyPerFile(directoryPath: path, optional: true);
})
```

## <a name="memory-configuration-provider"></a>Dostawca konfiguracji pamięci

<xref:Microsoft.Extensions.Configuration.Memory.MemoryConfigurationProvider>Używa kolekcji w pamięci jako par klucz konfiguracji-wartość.

Poniższy kod dodaje kolekcję pamięci do systemu konfiguracji:

:::code language="csharp" source="snippets/configuration/console-memory/Program.cs" highlight="22-29":::

W powyższym kodzie program <xref:Microsoft.Extensions.Configuration.MemoryConfigurationBuilderExtensions.AddInMemoryCollection(Microsoft.Extensions.Configuration.IConfigurationBuilder,System.Collections.Generic.IEnumerable{System.Collections.Generic.KeyValuePair{System.String,System.String}})?displayProperty=nameWithType> dodaje dostawcę pamięci po domyślnych dostawcach konfiguracji. Przykład określania kolejności dostawców konfiguracji można znaleźć w temacie [dostawca konfiguracji XML](#xml-configuration-provider).

## <a name="see-also"></a>Zobacz także

- [Konfiguracja w programie .NET](configuration.md)
- [Host ogólny .NET](generic-host.md)
- [Implementowanie niestandardowego dostawcy konfiguracji](custom-configuration-provider.md)
