---
title: Struktura projektu dla Blazor aplikacji
description: Dowiedz się, w jaki sposób struktura projektu dla formularzy i projektów ASP.NET sieci Web jest Blazor porównywana.
author: danroth27
ms.author: daroth
no-loc:
- Blazor
- WebAssembly
ms.date: 11/20/2020
ms.openlocfilehash: d91430eb654ee16934408bf064803b34ca700640
ms.sourcegitcommit: 2f485e721f7f34b87856a51181b5b56624b31fd5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/02/2020
ms.locfileid: "96509809"
---
# <a name="project-structure-for-no-locblazor-apps"></a>Struktura projektu dla Blazor aplikacji

Pomimo znaczących różnic struktury projektu, ASP.NET formularzy sieci Web i Blazor udostępniają wiele podobnych koncepcji. Tutaj Przyjrzyjmy się strukturze Blazor projektu i porównać go z projektem formularzy sieci Web ASP.NET.

Aby utworzyć swoją pierwszą Blazor aplikację, postępuj zgodnie z instrukcjami wyświetlanymi w [ Blazor krokach wprowadzenie](/aspnet/core/blazor/get-started). Można postępować zgodnie z instrukcjami w celu utworzenia Blazor aplikacji serwera lub Blazor WebAssembly aplikacji hostowanej w ASP.NET Core. Poza obsługą logiki specyficznej dla modelu, większość kodu w obu projektach jest taka sama.

## <a name="project-file"></a>Plik projektu

Blazor Aplikacje serwera to projekty platformy .NET. Plik projektu dla Blazor aplikacji serwerowej jest bardzo prosty, ponieważ może uzyskać następujące informacje:

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
  </PropertyGroup>

</Project>
```

Plik projektu Blazor WebAssembly aplikacji wygląda nieco więcej (dokładne numery wersji mogą się różnić):

```xml
<Project Sdk="Microsoft.NET.Sdk.BlazorWebAssembly">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Microsoft.AspNetCore.Components.WebAssembly" Version="5.0.0" />
    <PackageReference Include="Microsoft.AspNetCore.Components.WebAssembly.DevServer" Version="5.0.0" PrivateAssets="all" />
    <PackageReference Include="System.Net.Http.Json" Version="5.0.0" />
  </ItemGroup>

</Project>
```

BlazorWebAssemblyelementy docelowe projektu `Microsoft.NET.Sdk.BlazorWebAssembly` zamiast `Microsoft.NET.Sdk.Web` zestawu SDK, ponieważ działają w przeglądarce w WebAssembly środowisku uruchomieniowym .NET opartym na architekturze. Nie można zainstalować programu .NET w przeglądarce internetowej, na przykład na serwerze lub na komputerze dewelopera. W związku z tym projekt odwołuje się do Blazor struktury przy użyciu poszczególnych odwołań do pakietu.

Porównując, domyślny projekt formularzy sieci Web ASP.NET zawiera niemal 300 wierszy XML w pliku *. csproj* , z których większość jest jawnie wyświetlona w projekcie różnego kodu i plików zawartości. Dzięki wydaniu `.NET 5` obu programów `Blazor Server` i `Blazor WebAssembly` aplikacji można łatwo współdzielić jedno ujednolicone środowisko uruchomieniowe.

Chociaż są one obsługiwane, poszczególne odwołania do zestawów są rzadziej używane w projektach .NET. Większość zależności projektu jest obsługiwana jako odwołania do pakietu NuGet. Musisz tylko odwoływać się do zależności pakietów najwyższego poziomu w projektach .NET. Zależności przechodnie są włączane automatycznie. Zamiast korzystać z pliku *packages.config* często znalezionego w projektach formularzy sieci Web ASP.NET do pakietów referencyjnych, odwołania do pakietów są dodawane do pliku projektu przy użyciu `<PackageReference>` elementu.

```xml
<ItemGroup>
  <PackageReference Include="Newtonsoft.Json" Version="12.0.2" />
</ItemGroup>
```

## <a name="entry-point"></a>Punkt wejścia

BlazorPunkt wejścia aplikacji serwera jest zdefiniowany w pliku *program.cs* , jak widać w aplikacji konsolowej. Gdy aplikacja jest wykonywana, tworzy i uruchamia wystąpienie hosta sieci Web przy użyciu ustawień domyślnych, które są specyficzne dla aplikacji sieci Web. Host sieci Web zarządza Blazor cyklem życia aplikacji serwera i konfiguruje usługi na poziomie hosta. Przykładami takich usług są konfiguracje, rejestrowanie, iniekcja zależności i serwer HTTP. Ten kod jest głównie zwyczajowy i często pozostaje niezmieniony.

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateHostBuilder(args).Build().Run();
    }

    public static IHostBuilder CreateHostBuilder(string[] args) =>
        Host.CreateDefaultBuilder(args)
            .ConfigureWebHostDefaults(webBuilder =>
            {
                webBuilder.UseStartup<Startup>();
            });
}
```

BlazorWebAssemblyaplikacje definiują również punkt wejścia w *program.cs*. Kod wygląda nieco inaczej. Kod jest podobny w przypadku konfigurowania hosta aplikacji w celu zapewnienia tej samej aplikacji na poziomie hosta. WebAssemblyHost aplikacji nie jest jednak skonfigurowany jako serwer http, ponieważ jest wykonywany bezpośrednio w przeglądarce.

Blazor aplikacje mają `Startup` klasę zamiast pliku *Global. asax* do definiowania logiki uruchamiania aplikacji. `Startup`Klasa służy do konfigurowania aplikacji i wszystkich usług specyficznych dla aplikacji. W Blazor aplikacji serwerowej Klasa służy `Startup` do konfigurowania punktu końcowego dla połączenia w czasie rzeczywistym używanego przez Blazor między przeglądarkami klienta a serwerem. W Blazor WebAssembly aplikacji `Startup` Klasa definiuje główne składniki aplikacji i miejsce, w którym powinny być renderowane. Zajmiemy się bardziej szczegółowymi `Startup` klasami w sekcji [uruchamiania aplikacji](./app-startup.md) .

## <a name="static-files"></a>Pliki statyczne

W przeciwieństwie do projektów ASP.NET Web Forms, nie wszystkie pliki w Blazor projekcie mogą być żądane jako pliki statyczne. Tylko pliki w folderze *wwwroot* są adresami sieci Web. Ten folder jest określany jako "katalog główny sieci Web" aplikacji. Wszystkie elementy poza elementem głównym sieci Web aplikacji *nie są* adresami sieci Web. Ta konfiguracja zapewnia dodatkowy poziom zabezpieczeń, który uniemożliwia przypadkowe ujawnienie plików projektu za pośrednictwem sieci Web.

## <a name="configuration"></a>Konfigurowanie

Konfiguracja w aplikacjach ASP.NET Web Forms jest zwykle obsługiwana przy użyciu co najmniej jednego pliku *web.config* . Blazor aplikacje nie mają zwykle plików *web.config* . Jeśli tak, plik jest używany tylko do konfigurowania ustawień specyficznych dla usług IIS, które są hostowane w usługach IIS. Zamiast tego Blazor aplikacje serwera używają abstrakcji konfiguracji ASP.NET Core ( Blazor WebAssembly aplikacje nie obsługują obecnie tych samych abstrakcji konfiguracji, ale mogą to być funkcje dodane w przyszłości). Na przykład domyślna Blazor aplikacja serwerowa przechowuje niektóre ustawienia w *appsettings.js*.

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft": "Warning",
      "Microsoft.Hosting.Lifetime": "Information"
    }
  },
  "AllowedHosts": "*"
}
```

Dowiesz się więcej na temat konfiguracji w projektach ASP.NET Core w sekcji [konfiguracji](./config.md) .

## <a name="razor-components"></a>Składniki Razor

Większość plików w Blazor projektach to pliki *Razor* . Razor to tworzenia szablonów język oparty na języku HTML i C#, który jest używany do dynamicznego generowania interfejsu użytkownika sieci Web. Pliki *. Razor* definiują składniki tworzące interfejs użytkownika aplikacji. W większości przypadków składniki są identyczne zarówno dla Blazor serwera, jak i Blazor WebAssembly aplikacji. Składniki w programie Blazor są analogiczne do kontrolek użytkownika w ASP.NET Web Forms.

Każdy plik składnika Razor jest kompilowany do klasy .NET podczas kompilowania projektu. Wygenerowana Klasa przechwytuje stan składnika, logiki renderowania, metody cyklu życia, procedury obsługi zdarzeń i inne logiki. W sekcji [Tworzenie składników interfejsu użytkownika wielokrotnego użytku Blazor ](./components.md) należy zapoznać się z sekcją.

Pliki *_Imports. Razor* nie są plikami składników Razor. Zamiast tego definiują zestaw dyrektyw Razor do zaimportowania do innych plików *Razor* w tym samym folderze i w jego podfolderach. Na przykład plik *_Imports. Razor* jest konwencjonalnym sposobem dodawania `using` dyrektyw dla często używanych przestrzeni nazw:

```razor
@using System.Net.Http
@using Microsoft.AspNetCore.Authorization
@using Microsoft.AspNetCore.Components.Authorization
@using Microsoft.AspNetCore.Components.Forms
@using Microsoft.AspNetCore.Components.Routing
@using Microsoft.AspNetCore.Components.Web
@using Microsoft.JSInterop
@using BlazorApp1
@using BlazorApp1.Shared
```

## <a name="pages"></a>Pages

Gdzie znajdują się strony w Blazor aplikacjach? Blazor nie definiuje oddzielnego rozszerzenia pliku dla stron adresowanych, takich jak pliki *aspx* w aplikacjach ASP.NET Web Forms. Zamiast tego strony są definiowane przez przypisanie tras do składników programu. Trasa jest zwykle przypisana przy użyciu `@page` dyrektywy Razor. Na przykład `Counter` składnik utworzony w pliku *Pages/Counter. Razor* definiuje następującą trasę:

```razor
@page "/counter"
```

Routing w programie Blazor jest obsługiwany po stronie klienta, a nie na serwerze. Gdy użytkownik nawiguje w przeglądarce, Blazor przechwytuje nawigację, a następnie renderuje składnik przy użyciu pasującej trasy.

Trasy składników nie są obecnie wywnioskowane przez lokalizację pliku składnika, tak jak w przypadku stron *. aspx* . Ta funkcja może zostać dodana w przyszłości. Poszczególne trasy muszą być jawnie określone w składniku. Przechowywanie składników rutowanych w folderze *Pages* nie ma specjalnego znaczenia i jest czysto Konwencji.

Więcej szczegółów na temat routingu znajduje się w Blazor sekcji [strony, Routing i układy](./pages-routing-layouts.md) .

## <a name="layout"></a>Layout

W aplikacjach ASP.NET Web Forms typowy układ strony jest obsługiwany przy użyciu stron wzorcowych (*site. Master*). W Blazor aplikacjach układ strony jest obsługiwany przy użyciu składników układu (*Shared/MainLayout. Razor*). Składniki układu zostaną omówione bardziej szczegółowo w sekcji [strony, routingu i układów](./pages-routing-layouts.md) .

## <a name="bootstrap-no-locblazor"></a>Bootstrap Blazor

Aby załadować Blazor aplikację, należy wykonać następujące polecenie:

- Określ, gdzie na stronie ma być renderowany składnik główny (*App. Razor*).
- Dodaj odpowiedni Blazor skrypt struktury.

W Blazor aplikacji serwera strona hosta składnika głównego jest zdefiniowana w pliku *_Host. cshtml* . Ten plik definiuje stronę Razor, a nie składnik. Razor Pages używać składnia Razor do definiowania strony z adresami serwera, podobnie jak strona *. aspx* . `Html.RenderComponentAsync<TComponent>(RenderMode)`Metoda służy do definiowania miejsca, w którym ma być renderowany składnik poziomu głównego. `RenderMode`Opcja wskazuje sposób, w jaki składnik powinien być renderowany. W poniższej tabeli przedstawiono obsługiwane `RenderMode` Opcje.

|Opcja                        |Opis       |
|------------------------------|------------------|
|`RenderMode.Server`           |Renderowane interaktywnie po nawiązaniu połączenia z przeglądarką|
|`RenderMode.ServerPrerendered`|Pierwsze, wstępnie renderowane i renderowane interaktywnie|
|`RenderMode.Static`           |Renderowane jako zawartość statyczna|

Odwołanie do skryptu do *_framework/blazor.server.js* nawiązuje połączenie w czasie rzeczywistym z serwerem, a następnie zajmuje się wszystkimi interakcjami użytkowników i AKTUALIZACJAmi interfejsu użytkownika.

```razor
@page "/"
@namespace BlazorApp1.Pages
@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>BlazorApp1</title>
    <base href="~/" />
    <link rel="stylesheet" href="css/bootstrap/bootstrap.min.css" />
    <link href="css/site.css" rel="stylesheet" />
</head>
<body>
    <app>
        @(await Html.RenderComponentAsync<App>(RenderMode.ServerPrerendered))
    </app>

    <script src="_framework/blazor.server.js"></script>
</body>
</html>
```

W Blazor WebAssembly aplikacji strona hosta to prosty statyczny plik HTML w katalogu *wwwroot/index.html*. `<div>`Element o identyfikatorze nazwa `app` jest używany do wskazania, gdzie ma być renderowany składnik główny.

```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
    <title>BlazorApp2</title>
    <base href="/" />
    <link href="css/bootstrap/bootstrap.min.css" rel="stylesheet" />
    <link href="css/app.css" rel="stylesheet" />
    <link href="blazor-web.styles.css" rel="stylesheet" />
</head>

<body>
    <div id="app">Loading...</div>

    <div id="blazor-error-ui">
        An unhandled error has occurred.
        <a href="" class="reload">Reload</a>
        <a class="dismiss">🗙</a>
    </div>
    <script src="_framework/blazor.webassembly.js"></script>
</body>

</html>

```

Składnik główny do renderowania jest skonfigurowany w `Program.Main` metodzie aplikacji z elastycznością do rejestrowania różnych usług przy użyciu iniekcji zależności. Dodawanie usług do aplikacji można znaleźć w [ Blazor WebAssembly ](https://docs.microsoft.com/aspnet/core/blazor/fundamentals/dependency-injection?view=aspnetcore-5.0#blazor-webassembly) temacie

```csharp
public class Program
{
    public static async Task Main(string[] args)
    {
        var builder = WebAssemblyHostBuilder.CreateDefault(args);
        builder.RootComponents.Add<App>("#app");

        ....
        ....
    }
}
```

## <a name="build-output"></a>Dane wyjściowe kompilacji

Po Blazor skompilowaniu projektu wszystkie składniki i pliki kodu Razor są kompilowane do jednego zestawu. W przeciwieństwie do projektów ASP.NET Web Forms, Blazor nie obsługuje kompilowania logiki interfejsu użytkownika w czasie wykonywania.

## <a name="run-the-app"></a>Uruchamianie aplikacji

Aby uruchomić Blazor aplikację serwerową, naciśnij klawisz `F5` w programie Visual Studio. Blazor aplikacje nie obsługują kompilacji w czasie wykonywania. Aby zobaczyć wyniki zmian kodu i znaczników składnika, ponownie skompiluj i ponownie uruchom aplikację z dołączonym debugerem. Jeśli uruchomisz bez dołączonego debugera ( `Ctrl+F5` ), program Visual Studio przeczujuje się pod kątem zmian plików i ponownie uruchomi aplikację w miarę wprowadzania zmian. Przeglądarka ręcznie jest odświeżana w miarę wprowadzania zmian.

Aby uruchomić Blazor WebAssembly aplikację, wybierz jedną z następujących metod:

- Uruchom projekt klienta bezpośrednio przy użyciu serwera deweloperskiego.
- Uruchom projekt serwera podczas hostowania aplikacji przy użyciu ASP.NET Core.

BlazorWebAssemblyaplikacje mogą być debugowane w przeglądarce i w programie Visual Studio. zobacz [ASP.NET Core Blazor WebAssembly debugowania](/aspnet/core/blazor/debug) , aby uzyskać szczegółowe informacje.

>[!div class="step-by-step"]
>[Poprzedni](hosting-models.md) 
> [Dalej](app-startup.md)
