---
title: Uruchamianie aplikacji
description: Dowiedz się, jak zdefiniować logikę uruchamiania dla aplikacji.
author: csharpfritz
ms.author: jefritz
ms.date: 11/20/2020
ms.openlocfilehash: d812079f84f67409334d07c4c10c5577446503be
ms.sourcegitcommit: 2f485e721f7f34b87856a51181b5b56624b31fd5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/02/2020
ms.locfileid: "96509705"
---
# <a name="app-startup"></a>Uruchamianie aplikacji

Aplikacje, które są przeznaczone dla ASP.NET zazwyczaj mają `global.asax.cs` plik, który definiuje `Application_Start` zdarzenie kontrolujące, które usługi są skonfigurowane i udostępniane do obsługi renderowania HTML i przetwarzania .NET. W tym rozdziale przedstawiono, jak nieco różnią się różnice między ASP.NET Core i serwerem Blazor.

## <a name="application_start-and-web-forms"></a>Application_Start i formularze sieci Web

Domyślna metoda formularzy sieci Web `Application_Start` została wyhodowana w celu przekroczenia lat w celu obsługi wielu zadań konfiguracyjnych.  Nowy projekt formularzy sieci Web z domyślnym szablonem w programie Visual Studio 2019 zawiera teraz następującą logikę konfiguracji:

- `RouteConfig` -Routing adresów URL aplikacji
- `BundleConfig` -CSS i JavaScript i minifikacja

Każdy z tych pojedynczych plików znajduje się w `App_Start` folderze i uruchamiany tylko raz na początku naszej aplikacji.  `RouteConfig` w domyślnym szablonie projektu dodaje `FriendlyUrlSettings` formularze for Web Forms, aby zezwolić na adresy URL aplikacji, aby pominąć `.ASPX` rozszerzenie pliku.  Szablon domyślny zawiera również dyrektywę, która dostarcza stałe kody stanu przekierowywania HTTP (HTTP 301) dla `.ASPX` stron do przyjaznego adresu URL z nazwą pliku, który pomija rozszerzenie.

W przypadku ASP.NET Core i Blazor te metody są uproszczone i skonsolidowane w `Startup` klasie lub są eliminowane na rzecz wspólnych technologii sieci Web.

## <a name="blazor-server-startup-structure"></a>Struktura uruchamiania serwera Blazor

Aplikacje serwera Blazor znajdują się na ASP.NET Core w wersji 3,0 lub nowszej.  ASP.NET Core aplikacje sieci Web są konfigurowane za pomocą pary metod w `Startup.cs` klasie w folderze głównym aplikacji.  Domyślna zawartość klasy startowej jest wymieniona poniżej

```csharp
public class Startup
{
  public Startup(IConfiguration configuration)
  {
    Configuration = configuration;
  }

  public IConfiguration Configuration { get; }

  // This method gets called by the runtime. Use this method to add services to the container.
  // For more information on how to configure your application, visit https://go.microsoft.com/fwlink/?LinkID=398940
  public void ConfigureServices(IServiceCollection services)
  {
    services.AddRazorPages();
    services.AddServerSideBlazor();
    services.AddSingleton<WeatherForecastService>();
  }

  // This method gets called by the runtime. Use this method to configure the HTTP request pipeline.
  public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
  {
    if (env.IsDevelopment())
    {
      app.UseDeveloperExceptionPage();
    }
    else
    {
      app.UseExceptionHandler("/Error");
      // The default HSTS value is 30 days. You may want to change this for production scenarios, see https://aka.ms/aspnetcore-hsts.
      app.UseHsts();
    }

    app.UseHttpsRedirection();
    app.UseStaticFiles();

    app.UseRouting();

    app.UseEndpoints(endpoints =>
    {
      endpoints.MapBlazorHub();
      endpoints.MapFallbackToPage("/_Host");
   });
  }
 }
```

Podobnie jak w przypadku pozostałej części ASP.NET Core, Klasa startowa jest tworzona z zasadami iniekcji zależności.  `IConfiguration`Jest dostarczany do konstruktora i umieszczany we właściwości publicznej na potrzeby późniejszego dostępu podczas konfiguracji.

`ConfigureServices`Metoda wprowadzona w ASP.NET Core umożliwia skonfigurowanie różnych usług ASP.NET Core Framework dla wbudowanego kontenera wstrzykiwania zależności struktury.  Różne `services.Add*` metody umożliwiają dodanie usług, które udostępniają funkcje, takie jak uwierzytelnianie, strony Razor, routing kontrolerów MVC, sygnalizacja i Blazor interakcje serwera między wieloma innymi.  Ta metoda nie była wymagana w formularzach sieci Web, ponieważ analizowanie i obsługa plików ASPX, ASCX, ASHX i ASMX zostało zdefiniowane przez odwołanie do ASP.NET w pliku konfiguracji web.config.  Więcej informacji o iniekcji zależności w ASP.NET Core jest dostępny w [dokumentacji online](/aspnet/core/fundamentals/dependency-injection).

`Configure`Metoda wprowadza koncepcję potoku HTTP do ASP.NET Core.  W tej metodzie deklarujemy od góry do dołu [oprogramowanie pośredniczące](middleware.md) , które będzie obsługiwało każde żądanie wysyłane do naszej aplikacji. Większość z tych funkcji w konfiguracji domyślnej została rozłożona na wiele plików konfiguracji formularzy sieci Web i znajduje się teraz w jednym miejscu, aby ułatwić sobie odwołanie.

Nie jest już konfiguracją niestandardowej strony błędu umieszczonej w `web.config` pliku, ale teraz jest ona zawsze wyświetlana, jeśli środowisko aplikacji nie ma etykiety `Development` .  Ponadto aplikacje ASP.NET Core są teraz skonfigurowane do obsłużenia bezpiecznych stron z protokołem TLS domyślnie przy użyciu `UseHttpsRedirection` wywołania metody.

Następnie zostanie wyświetlona nieoczekiwana Metoda konfiguracji `UseStaticFiles` .  W ASP.NET Core obsługa żądań plików statycznych (takich jak pliki JavaScript, CSS i Image) musi być jawnie włączona, a tylko pliki w folderze katalogu *wwwroot* aplikacji są publicznie adresowane.

Następnym wierszem jest pierwsza, która replikuje jedną z opcji konfiguracji z formularzy sieci Web: `UseRouting` .  Ta metoda dodaje router ASP.NET Core do potoku i można go skonfigurować w tym miejscu lub w poszczególnych plikach, do których może rozważyć Routing.  Więcej informacji na temat konfiguracji routingu można znaleźć w [sekcji Routing](pages-routing-layouts.md).

Końcowa instrukcja w tej metodzie definiuje punkty końcowe, na których nasłuchuje ASP.NET Core.  Te trasy to lokalizacje dostępne w sieci Web, do których można uzyskać dostęp na serwerze sieci Web i które odbierają zawartość obsłużoną przez platformę .NET i zwracają do Ciebie.  Pierwszy wpis `MapBlazorHub` umożliwia skonfigurowanie centrum sygnałów do użycia w czasie rzeczywistym i trwałego połączenia z serwerem, w którym jest obsługiwany stan i renderowanie składników Blazor.  `MapFallbackToPage`Wywołanie metody wskazuje lokalizację dostępną do sieci Web strony, która uruchamia aplikację Blazor, a także konfiguruje aplikację do obsługi żądań z głębokością konsolidacji po stronie klienta.  Ta funkcja zostanie wyświetlona w pracy, jeśli otworzysz przeglądarkę i nawiguj bezpośrednio do Blazor obsłużonej trasy w aplikacji, na przykład `/counter` w domyślnym szablonie projektu. Żądanie jest obsługiwane przez stronę rezerwową *_Host. cshtml* , która następnie uruchamia router Blazor i renderuje stronę licznika.

## <a name="upgrading-the-bundleconfig-process"></a>Uaktualnianie procesu BundleConfig

Technologie tworzenia zasobów, takich jak arkusze stylów CSS i pliki JavaScript, znacznie wzrosły, z innymi technologiami, które zapewniają szybkie i bardziej zmieniające się narzędzia i techniki zarządzania tymi zasobami.  W tym celu zalecamy użycie narzędzia wiersza polecenia węzła, takiego jak Grunt/Gulp/WebPack, aby spakować zasoby statyczne.

Narzędzia wiersza polecenia grunt, Gulp i WebPack oraz skojarzone z nimi konfiguracje można dodać do aplikacji, a ASP.NET Core w sposób cichy zignoruje te pliki podczas procesu tworzenia aplikacji.  Możesz dodać wywołanie do uruchamiania swoich zadań, dodając `Target` wewnątrz pliku projektu składnię podobną do następującej, która wywoła skrypt Gulp i `min` element docelowy wewnątrz tego skryptu

```xml
<Target Name="MyPreCompileTarget" BeforeTargets="Build">
  <Exec Command="gulp min" />
</Target>
```

Więcej szczegółów na temat obu strategii zarządzania plikami CSS i JavaScript jest dostępnych w [zbiorze i zminifikować zasobów statycznych w dokumentacji ASP.NET Core](/aspnet/core/client-side/bundling-and-minification) .

>[!div class="step-by-step"]
>[Poprzedni](project-structure.md) 
> [Dalej](components.md)
