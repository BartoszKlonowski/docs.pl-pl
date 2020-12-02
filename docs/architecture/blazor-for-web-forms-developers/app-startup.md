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
# <a name="app-startup"></a><span data-ttu-id="fb760-103">Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="fb760-103">App startup</span></span>

<span data-ttu-id="fb760-104">Aplikacje, które są przeznaczone dla ASP.NET zazwyczaj mają `global.asax.cs` plik, który definiuje `Application_Start` zdarzenie kontrolujące, które usługi są skonfigurowane i udostępniane do obsługi renderowania HTML i przetwarzania .NET.</span><span class="sxs-lookup"><span data-stu-id="fb760-104">Applications that are written for ASP.NET typically have a `global.asax.cs` file that defines the `Application_Start` event that controls which services are configured and made available for both HTML rendering and .NET processing.</span></span> <span data-ttu-id="fb760-105">W tym rozdziale przedstawiono, jak nieco różnią się różnice między ASP.NET Core i serwerem Blazor.</span><span class="sxs-lookup"><span data-stu-id="fb760-105">This chapter looks at how things are slightly different with ASP.NET Core and Blazor Server.</span></span>

## <a name="application_start-and-web-forms"></a><span data-ttu-id="fb760-106">Application_Start i formularze sieci Web</span><span class="sxs-lookup"><span data-stu-id="fb760-106">Application_Start and Web Forms</span></span>

<span data-ttu-id="fb760-107">Domyślna metoda formularzy sieci Web `Application_Start` została wyhodowana w celu przekroczenia lat w celu obsługi wielu zadań konfiguracyjnych.</span><span class="sxs-lookup"><span data-stu-id="fb760-107">The default web forms `Application_Start` method has grown in purpose over years to handle many configuration tasks.</span></span>  <span data-ttu-id="fb760-108">Nowy projekt formularzy sieci Web z domyślnym szablonem w programie Visual Studio 2019 zawiera teraz następującą logikę konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="fb760-108">A fresh web forms project with the default template in Visual Studio 2019 now contains the following configuration logic:</span></span>

- <span data-ttu-id="fb760-109">`RouteConfig` -Routing adresów URL aplikacji</span><span class="sxs-lookup"><span data-stu-id="fb760-109">`RouteConfig` - Application URL routing</span></span>
- <span data-ttu-id="fb760-110">`BundleConfig` -CSS i JavaScript i minifikacja</span><span class="sxs-lookup"><span data-stu-id="fb760-110">`BundleConfig` - CSS and JavaScript bundling and minification</span></span>

<span data-ttu-id="fb760-111">Każdy z tych pojedynczych plików znajduje się w `App_Start` folderze i uruchamiany tylko raz na początku naszej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fb760-111">Each of these individual files resides in the `App_Start` folder and run only once at the start of our application.</span></span>  <span data-ttu-id="fb760-112">`RouteConfig` w domyślnym szablonie projektu dodaje `FriendlyUrlSettings` formularze for Web Forms, aby zezwolić na adresy URL aplikacji, aby pominąć `.ASPX` rozszerzenie pliku.</span><span class="sxs-lookup"><span data-stu-id="fb760-112">`RouteConfig` in the default project template adds the `FriendlyUrlSettings` for web forms to allow application URLs to omit the `.ASPX` file extension.</span></span>  <span data-ttu-id="fb760-113">Szablon domyślny zawiera również dyrektywę, która dostarcza stałe kody stanu przekierowywania HTTP (HTTP 301) dla `.ASPX` stron do przyjaznego adresu URL z nazwą pliku, który pomija rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="fb760-113">The default template also contains a directive that provides permanent HTTP redirect status codes (HTTP 301) for the `.ASPX` pages to the friendly URL with the file name that omits the extension.</span></span>

<span data-ttu-id="fb760-114">W przypadku ASP.NET Core i Blazor te metody są uproszczone i skonsolidowane w `Startup` klasie lub są eliminowane na rzecz wspólnych technologii sieci Web.</span><span class="sxs-lookup"><span data-stu-id="fb760-114">With ASP.NET Core and Blazor, these methods are either simplified and consolidated into the `Startup` class or they are eliminated in favor of common web technologies.</span></span>

## <a name="blazor-server-startup-structure"></a><span data-ttu-id="fb760-115">Struktura uruchamiania serwera Blazor</span><span class="sxs-lookup"><span data-stu-id="fb760-115">Blazor Server Startup Structure</span></span>

<span data-ttu-id="fb760-116">Aplikacje serwera Blazor znajdują się na ASP.NET Core w wersji 3,0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="fb760-116">Blazor Server applications reside on top of an ASP.NET Core 3.0 or later version.</span></span>  <span data-ttu-id="fb760-117">ASP.NET Core aplikacje sieci Web są konfigurowane za pomocą pary metod w `Startup.cs` klasie w folderze głównym aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fb760-117">ASP.NET Core web applications are configured through a pair of methods in the `Startup.cs` class on the root folder of the application.</span></span>  <span data-ttu-id="fb760-118">Domyślna zawartość klasy startowej jest wymieniona poniżej</span><span class="sxs-lookup"><span data-stu-id="fb760-118">The Startup class's default content is listed below</span></span>

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

<span data-ttu-id="fb760-119">Podobnie jak w przypadku pozostałej części ASP.NET Core, Klasa startowa jest tworzona z zasadami iniekcji zależności.</span><span class="sxs-lookup"><span data-stu-id="fb760-119">Like the rest of ASP.NET Core, the Startup class is created with dependency injection principles.</span></span>  <span data-ttu-id="fb760-120">`IConfiguration`Jest dostarczany do konstruktora i umieszczany we właściwości publicznej na potrzeby późniejszego dostępu podczas konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="fb760-120">The `IConfiguration` is provided to the constructor and stashed in a public property for later access during configuration.</span></span>

<span data-ttu-id="fb760-121">`ConfigureServices`Metoda wprowadzona w ASP.NET Core umożliwia skonfigurowanie różnych usług ASP.NET Core Framework dla wbudowanego kontenera wstrzykiwania zależności struktury.</span><span class="sxs-lookup"><span data-stu-id="fb760-121">The `ConfigureServices` method introduced in ASP.NET Core allows for the various ASP.NET Core framework services to be configured for the framework's built-in dependency injection container.</span></span>  <span data-ttu-id="fb760-122">Różne `services.Add*` metody umożliwiają dodanie usług, które udostępniają funkcje, takie jak uwierzytelnianie, strony Razor, routing kontrolerów MVC, sygnalizacja i Blazor interakcje serwera między wieloma innymi.</span><span class="sxs-lookup"><span data-stu-id="fb760-122">The various `services.Add*` methods add services that enable features such as authentication, razor pages, MVC controller routing, SignalR, and Blazor Server interactions among many others.</span></span>  <span data-ttu-id="fb760-123">Ta metoda nie była wymagana w formularzach sieci Web, ponieważ analizowanie i obsługa plików ASPX, ASCX, ASHX i ASMX zostało zdefiniowane przez odwołanie do ASP.NET w pliku konfiguracji web.config.</span><span class="sxs-lookup"><span data-stu-id="fb760-123">This method was not needed in web forms, as the parsing and handling of the ASPX, ASCX, ASHX, and ASMX files were defined by referencing ASP.NET in the web.config configuration file.</span></span>  <span data-ttu-id="fb760-124">Więcej informacji o iniekcji zależności w ASP.NET Core jest dostępny w [dokumentacji online](/aspnet/core/fundamentals/dependency-injection).</span><span class="sxs-lookup"><span data-stu-id="fb760-124">More information about dependency injection in ASP.NET Core is available in the [online documentation](/aspnet/core/fundamentals/dependency-injection).</span></span>

<span data-ttu-id="fb760-125">`Configure`Metoda wprowadza koncepcję potoku HTTP do ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="fb760-125">The `Configure` method introduces the concept of the HTTP pipeline to ASP.NET Core.</span></span>  <span data-ttu-id="fb760-126">W tej metodzie deklarujemy od góry do dołu [oprogramowanie pośredniczące](middleware.md) , które będzie obsługiwało każde żądanie wysyłane do naszej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fb760-126">In this method, we declare from top to bottom the [Middleware](middleware.md) that will handle every request sent to our application.</span></span> <span data-ttu-id="fb760-127">Większość z tych funkcji w konfiguracji domyślnej została rozłożona na wiele plików konfiguracji formularzy sieci Web i znajduje się teraz w jednym miejscu, aby ułatwić sobie odwołanie.</span><span class="sxs-lookup"><span data-stu-id="fb760-127">Most of these features in the default configuration were scattered across the web forms configuration files and are now in one place for ease of reference.</span></span>

<span data-ttu-id="fb760-128">Nie jest już konfiguracją niestandardowej strony błędu umieszczonej w `web.config` pliku, ale teraz jest ona zawsze wyświetlana, jeśli środowisko aplikacji nie ma etykiety `Development` .</span><span class="sxs-lookup"><span data-stu-id="fb760-128">No longer is the configuration of the custom error page placed in a `web.config` file, but now is configured to always be shown if the application environment is not labeled `Development`.</span></span>  <span data-ttu-id="fb760-129">Ponadto aplikacje ASP.NET Core są teraz skonfigurowane do obsłużenia bezpiecznych stron z protokołem TLS domyślnie przy użyciu `UseHttpsRedirection` wywołania metody.</span><span class="sxs-lookup"><span data-stu-id="fb760-129">Additionally, ASP.NET Core applications are now configured to serve secure pages with TLS by default with the `UseHttpsRedirection` method call.</span></span>

<span data-ttu-id="fb760-130">Następnie zostanie wyświetlona nieoczekiwana Metoda konfiguracji `UseStaticFiles` .</span><span class="sxs-lookup"><span data-stu-id="fb760-130">Next, an unexpected configuration method is listed to `UseStaticFiles`.</span></span>  <span data-ttu-id="fb760-131">W ASP.NET Core obsługa żądań plików statycznych (takich jak pliki JavaScript, CSS i Image) musi być jawnie włączona, a tylko pliki w folderze katalogu *wwwroot* aplikacji są publicznie adresowane.</span><span class="sxs-lookup"><span data-stu-id="fb760-131">In ASP.NET Core, support for requests for static files (like JavaScript, CSS, and image files) must be explicitly enabled, and only files in the app's *wwwroot* folder are publicly addressable by default.</span></span>

<span data-ttu-id="fb760-132">Następnym wierszem jest pierwsza, która replikuje jedną z opcji konfiguracji z formularzy sieci Web: `UseRouting` .</span><span class="sxs-lookup"><span data-stu-id="fb760-132">The next line is the first that replicates one of the configuration options from web forms: `UseRouting`.</span></span>  <span data-ttu-id="fb760-133">Ta metoda dodaje router ASP.NET Core do potoku i można go skonfigurować w tym miejscu lub w poszczególnych plikach, do których może rozważyć Routing.</span><span class="sxs-lookup"><span data-stu-id="fb760-133">This method adds the ASP.NET Core router to the pipeline and it can be either configured here or in the individual files that it can consider routing to.</span></span>  <span data-ttu-id="fb760-134">Więcej informacji na temat konfiguracji routingu można znaleźć w [sekcji Routing](pages-routing-layouts.md).</span><span class="sxs-lookup"><span data-stu-id="fb760-134">More information about routing configuration can be found in the [Routing section](pages-routing-layouts.md).</span></span>

<span data-ttu-id="fb760-135">Końcowa instrukcja w tej metodzie definiuje punkty końcowe, na których nasłuchuje ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="fb760-135">The final statement in this method defines the endpoints that ASP.NET Core is listening on.</span></span>  <span data-ttu-id="fb760-136">Te trasy to lokalizacje dostępne w sieci Web, do których można uzyskać dostęp na serwerze sieci Web i które odbierają zawartość obsłużoną przez platformę .NET i zwracają do Ciebie.</span><span class="sxs-lookup"><span data-stu-id="fb760-136">These routes are the web accessible locations that you can access on the web server and receive some content handled by .NET and returned to you.</span></span>  <span data-ttu-id="fb760-137">Pierwszy wpis `MapBlazorHub` umożliwia skonfigurowanie centrum sygnałów do użycia w czasie rzeczywistym i trwałego połączenia z serwerem, w którym jest obsługiwany stan i renderowanie składników Blazor.</span><span class="sxs-lookup"><span data-stu-id="fb760-137">The first entry, `MapBlazorHub` configures a SignalR hub for use in providing the real-time and persistent connection to the server where the state and rendering of Blazor components is handled.</span></span>  <span data-ttu-id="fb760-138">`MapFallbackToPage`Wywołanie metody wskazuje lokalizację dostępną do sieci Web strony, która uruchamia aplikację Blazor, a także konfiguruje aplikację do obsługi żądań z głębokością konsolidacji po stronie klienta.</span><span class="sxs-lookup"><span data-stu-id="fb760-138">The `MapFallbackToPage` method call indicates the web-accessible location of the page that starts the Blazor application and also configures the application to handle deep-linking requests from the client-side.</span></span>  <span data-ttu-id="fb760-139">Ta funkcja zostanie wyświetlona w pracy, jeśli otworzysz przeglądarkę i nawiguj bezpośrednio do Blazor obsłużonej trasy w aplikacji, na przykład `/counter` w domyślnym szablonie projektu.</span><span class="sxs-lookup"><span data-stu-id="fb760-139">You will see this feature at work if you open a browser and navigate directly to Blazor handled route in your application, such as `/counter` in the default project template.</span></span> <span data-ttu-id="fb760-140">Żądanie jest obsługiwane przez stronę rezerwową *_Host. cshtml* , która następnie uruchamia router Blazor i renderuje stronę licznika.</span><span class="sxs-lookup"><span data-stu-id="fb760-140">The request gets handled by the *_Host.cshtml* fallback page, which then runs the Blazor router and renders the counter page.</span></span>

## <a name="upgrading-the-bundleconfig-process"></a><span data-ttu-id="fb760-141">Uaktualnianie procesu BundleConfig</span><span class="sxs-lookup"><span data-stu-id="fb760-141">Upgrading the BundleConfig Process</span></span>

<span data-ttu-id="fb760-142">Technologie tworzenia zasobów, takich jak arkusze stylów CSS i pliki JavaScript, znacznie wzrosły, z innymi technologiami, które zapewniają szybkie i bardziej zmieniające się narzędzia i techniki zarządzania tymi zasobami.</span><span class="sxs-lookup"><span data-stu-id="fb760-142">Technologies for bundling assets like CSS stylesheets and JavaScript files have evolved significantly, with other technologies providing quickly evolving tools and techniques for managing these resources.</span></span>  <span data-ttu-id="fb760-143">W tym celu zalecamy użycie narzędzia wiersza polecenia węzła, takiego jak Grunt/Gulp/WebPack, aby spakować zasoby statyczne.</span><span class="sxs-lookup"><span data-stu-id="fb760-143">To this end, we recommend using a Node command-line tool such as Grunt / Gulp / WebPack to package your static assets.</span></span>

<span data-ttu-id="fb760-144">Narzędzia wiersza polecenia grunt, Gulp i WebPack oraz skojarzone z nimi konfiguracje można dodać do aplikacji, a ASP.NET Core w sposób cichy zignoruje te pliki podczas procesu tworzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fb760-144">The Grunt, Gulp, and WebPack command-line tools and their associated configurations can be added to your application and ASP.NET Core will quietly ignore those files during the application build process.</span></span>  <span data-ttu-id="fb760-145">Możesz dodać wywołanie do uruchamiania swoich zadań, dodając `Target` wewnątrz pliku projektu składnię podobną do następującej, która wywoła skrypt Gulp i `min` element docelowy wewnątrz tego skryptu</span><span class="sxs-lookup"><span data-stu-id="fb760-145">You can add a call to run their tasks by adding a `Target` inside your project file with syntax similar to the following that would trigger a gulp script and the `min` target inside that script</span></span>

```xml
<Target Name="MyPreCompileTarget" BeforeTargets="Build">
  <Exec Command="gulp min" />
</Target>
```

<span data-ttu-id="fb760-146">Więcej szczegółów na temat obu strategii zarządzania plikami CSS i JavaScript jest dostępnych w [zbiorze i zminifikować zasobów statycznych w dokumentacji ASP.NET Core](/aspnet/core/client-side/bundling-and-minification) .</span><span class="sxs-lookup"><span data-stu-id="fb760-146">More details about both strategies to manage your CSS and JavaScript files are available in the [Bundle and minify static assets in ASP.NET Core](/aspnet/core/client-side/bundling-and-minification) documentation.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="fb760-147">[Poprzedni](project-structure.md) 
> [Dalej](components.md)</span><span class="sxs-lookup"><span data-stu-id="fb760-147">[Previous](project-structure.md)
[Next](components.md)</span></span>
