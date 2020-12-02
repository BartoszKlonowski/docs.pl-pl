---
title: Migrowanie z formularzy sieci Web ASP.NET do Blazor
description: Dowiedz się, jak podejście do migracji istniejącej aplikacji ASP.NET Web Forms do programu Blazor .
author: twsouthwick
ms.author: tasou
no-loc:
- Blazor
- WebAssembly
ms.date: 11/20/2020
ms.openlocfilehash: 893b6f851681ec540629fe160749b2622b6d5440
ms.sourcegitcommit: 2f485e721f7f34b87856a51181b5b56624b31fd5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/02/2020
ms.locfileid: "96509835"
---
# <a name="migrate-from-aspnet-web-forms-to-no-locblazor"></a><span data-ttu-id="73fd7-103">Migrowanie z formularzy sieci Web ASP.NET do Blazor</span><span class="sxs-lookup"><span data-stu-id="73fd7-103">Migrate from ASP.NET Web Forms to Blazor</span></span>

<span data-ttu-id="73fd7-104">Migrowanie bazy kodu z formularzy sieci Web ASP.NET do Blazor programu to czasochłonne zadanie, które wymaga planowania.</span><span class="sxs-lookup"><span data-stu-id="73fd7-104">Migrating a code base from ASP.NET Web Forms to Blazor is a time-consuming task that requires planning.</span></span> <span data-ttu-id="73fd7-105">W tym rozdziale opisano proces.</span><span class="sxs-lookup"><span data-stu-id="73fd7-105">This chapter outlines the process.</span></span> <span data-ttu-id="73fd7-106">Oto, co może ułatwić przejście aplikacji do architektury *N-warstwowej* , co w przypadku, gdy model aplikacji (w tym przypadku formularzy sieci Web) jest oddzielony od logiki biznesowej.</span><span class="sxs-lookup"><span data-stu-id="73fd7-106">Something that can ease the transition is to ensure the app adheres to an *N-tier* architecture, wherein the app model (in this case, Web Forms) is separate from the business logic.</span></span> <span data-ttu-id="73fd7-107">To logiczne rozdzielenie warstw sprawia, że musi on zostać przeniesiony do platformy .NET Core i Blazor .</span><span class="sxs-lookup"><span data-stu-id="73fd7-107">This logical separation of layers makes it clear what needs to move to .NET Core and Blazor.</span></span>

<span data-ttu-id="73fd7-108">W tym przykładzie jest używana aplikacja eShop dostępna w witrynie [GitHub](https://github.com/dotnet-architecture/eShopOnBlazor) .</span><span class="sxs-lookup"><span data-stu-id="73fd7-108">For this example, the eShop app available on [GitHub](https://github.com/dotnet-architecture/eShopOnBlazor) is used.</span></span> <span data-ttu-id="73fd7-109">eShop to usługa wykazu, która zapewnia możliwości CRUD za pośrednictwem wpisów i walidacji formularza.</span><span class="sxs-lookup"><span data-stu-id="73fd7-109">eShop is a catalog service that provides CRUD capabilities via form entry and validation.</span></span>

<span data-ttu-id="73fd7-110">Dlaczego należy zmigrować działającą aplikację Blazor ?</span><span class="sxs-lookup"><span data-stu-id="73fd7-110">Why should a working app be migrated to Blazor?</span></span> <span data-ttu-id="73fd7-111">Wiele razy nie jest potrzebne.</span><span class="sxs-lookup"><span data-stu-id="73fd7-111">Many times, there's no need.</span></span> <span data-ttu-id="73fd7-112">Formularze sieci Web ASP.NET będą nadal obsługiwane przez wiele lat.</span><span class="sxs-lookup"><span data-stu-id="73fd7-112">ASP.NET Web Forms will continue to be supported for many years.</span></span> <span data-ttu-id="73fd7-113">Jednak wiele funkcji, które zapewnia, Blazor jest obsługiwanych tylko w zmigrowanej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="73fd7-113">However, many of the features that Blazor provides are only supported on a migrated app.</span></span> <span data-ttu-id="73fd7-114">Takie funkcje obejmują:</span><span class="sxs-lookup"><span data-stu-id="73fd7-114">Such features include:</span></span>

- <span data-ttu-id="73fd7-115">Ulepszenia wydajności w ramach platformy, takie jak `Span<T>`</span><span class="sxs-lookup"><span data-stu-id="73fd7-115">Performance improvements in the framework such as `Span<T>`</span></span>
- <span data-ttu-id="73fd7-116">Możliwość uruchamiania jako WebAssembly</span><span class="sxs-lookup"><span data-stu-id="73fd7-116">Ability to run as WebAssembly</span></span>
- <span data-ttu-id="73fd7-117">Obsługa wielu platform dla systemów Linux i macOS</span><span class="sxs-lookup"><span data-stu-id="73fd7-117">Cross-platform support for Linux and macOS</span></span>
- <span data-ttu-id="73fd7-118">Wdrożenie lokalne aplikacji lub wdrożenie platformy udostępnionej bez wpływu na inne aplikacje</span><span class="sxs-lookup"><span data-stu-id="73fd7-118">App-local deployment or shared framework deployment without impacting other apps</span></span>

<span data-ttu-id="73fd7-119">Jeśli te lub inne nowe funkcje są wystarczająco atrakcyjne, może wystąpić wartość migrowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="73fd7-119">If these or other new features are compelling enough, there may be value in migrating the app.</span></span> <span data-ttu-id="73fd7-120">Migracja może mieć różne kształty; może to być cała aplikacja lub tylko niektóre punkty końcowe, które wymagają wprowadzenia zmian.</span><span class="sxs-lookup"><span data-stu-id="73fd7-120">The migration can take different shapes; it can be the entire app, or only certain endpoints that require the changes.</span></span> <span data-ttu-id="73fd7-121">Decyzja o migracji jest ostatecznie oparta na problemach z firmą, które mają zostać rozwiązane przez dewelopera.</span><span class="sxs-lookup"><span data-stu-id="73fd7-121">The decision to migrate is ultimately based on the business problems to be solved by the developer.</span></span>

## <a name="server-side-versus-client-side-hosting"></a><span data-ttu-id="73fd7-122">Klient po stronie serwera a hosting po stronie klienta</span><span class="sxs-lookup"><span data-stu-id="73fd7-122">Server-side versus client-side hosting</span></span>

<span data-ttu-id="73fd7-123">Zgodnie z opisem w rozdziale [hosting modeli hostingu](hosting-models.md) Blazor aplikacja może być hostowana na dwa różne sposoby: po stronie serwera i po stronie klienta.</span><span class="sxs-lookup"><span data-stu-id="73fd7-123">As described in the [hosting models](hosting-models.md) chapter, a Blazor app can be hosted in two different ways: server-side and client-side.</span></span> <span data-ttu-id="73fd7-124">Model po stronie serwera korzysta z połączeń ASP.NET Core sygnalizujących, aby zarządzać aktualizacjami modelu DOM podczas uruchamiania dowolnego rzeczywistego kodu na serwerze.</span><span class="sxs-lookup"><span data-stu-id="73fd7-124">The server-side model uses ASP.NET Core SignalR connections to manage the DOM updates while running any actual code on the server.</span></span> <span data-ttu-id="73fd7-125">Model po stronie klienta działa jak WebAssembly w przeglądarce i nie wymaga połączeń z serwerem.</span><span class="sxs-lookup"><span data-stu-id="73fd7-125">The client-side model runs as WebAssembly within a browser and requires no server connections.</span></span> <span data-ttu-id="73fd7-126">Istnieje wiele różnic, które mogą mieć wpływ na to, co jest najlepsze dla określonej aplikacji:</span><span class="sxs-lookup"><span data-stu-id="73fd7-126">There are a number of differences that may affect which is best for a specific app:</span></span>

- <span data-ttu-id="73fd7-127">Uruchamianie jako WebAssembly nie obsługuje wszystkich funkcji (takich jak wątkowość) w bieżącym czasie</span><span class="sxs-lookup"><span data-stu-id="73fd7-127">Running as WebAssembly doesn't support all features (such as threading) at the current time</span></span>
- <span data-ttu-id="73fd7-128">Komunikacja między klientem a serwerem może powodować problemy z opóźnieniami w trybie po stronie serwera</span><span class="sxs-lookup"><span data-stu-id="73fd7-128">Chatty communication between the client and server may cause latency issues in server-side mode</span></span>
- <span data-ttu-id="73fd7-129">Dostęp do baz danych i wewnętrznych lub chronionych usług wymaga oddzielnej usługi z hostingiem po stronie klienta</span><span class="sxs-lookup"><span data-stu-id="73fd7-129">Access to databases and internal or protected services require a separate service with client-side hosting</span></span>

<span data-ttu-id="73fd7-130">W momencie pisania model po stronie serwera bardziej przypomina formularze sieci Web.</span><span class="sxs-lookup"><span data-stu-id="73fd7-130">At the time of writing, the server-side model more closely resembles Web Forms.</span></span> <span data-ttu-id="73fd7-131">Większość tego rozdziału koncentruje się na modelu hostingu po stronie serwera, ponieważ jest on gotowy do produkcji.</span><span class="sxs-lookup"><span data-stu-id="73fd7-131">Most of this chapter focuses on the server-side hosting model, as it's production-ready.</span></span>

## <a name="create-a-new-project"></a><span data-ttu-id="73fd7-132">Tworzenie nowego projektu</span><span class="sxs-lookup"><span data-stu-id="73fd7-132">Create a new project</span></span>

<span data-ttu-id="73fd7-133">Ten krok początkowej migracji polega na utworzeniu nowego projektu.</span><span class="sxs-lookup"><span data-stu-id="73fd7-133">This initial migration step is to create a new project.</span></span> <span data-ttu-id="73fd7-134">Ten typ projektu jest oparty na projektach w stylu zestawu SDK platformy .NET i upraszcza wiele standardowych, które były używane w poprzednich formatach projektu.</span><span class="sxs-lookup"><span data-stu-id="73fd7-134">This project type is based on the SDK style projects of .NET and simplifies much of the boilerplate that was used in previous project formats.</span></span> <span data-ttu-id="73fd7-135">Aby uzyskać więcej informacji, zobacz rozdział dotyczący [struktury projektu](project-structure.md).</span><span class="sxs-lookup"><span data-stu-id="73fd7-135">For more detail, please see the chapter on [Project Structure](project-structure.md).</span></span>

<span data-ttu-id="73fd7-136">Po utworzeniu projektu Zainstaluj biblioteki, które były używane w poprzednim projekcie.</span><span class="sxs-lookup"><span data-stu-id="73fd7-136">Once the project has been created, install the libraries that were used in the previous project.</span></span> <span data-ttu-id="73fd7-137">W starszych projektach formularzy sieci Web może zostać użyty plik *packages.config* , aby wyświetlić listę wymaganych pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="73fd7-137">In older Web Forms projects, you may have used the *packages.config* file to list the required NuGet packages.</span></span> <span data-ttu-id="73fd7-138">W nowym projekcie w stylu zestawu SDK *packages.config* został zastąpiony `<PackageReference>` elementami w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="73fd7-138">In the new SDK-style project, *packages.config* has been replaced with `<PackageReference>` elements in the project file.</span></span> <span data-ttu-id="73fd7-139">Zaletą tego podejścia jest to, że wszystkie zależności są instalowane w sposób przechodni.</span><span class="sxs-lookup"><span data-stu-id="73fd7-139">A benefit to this approach is that all dependencies are installed transitively.</span></span> <span data-ttu-id="73fd7-140">Można wyświetlić tylko te zależności najwyższego poziomu.</span><span class="sxs-lookup"><span data-stu-id="73fd7-140">You only list the top-level dependencies you care about.</span></span>

<span data-ttu-id="73fd7-141">Wiele zależności, z których korzystasz, jest dostępnych dla platformy .NET, w tym Entity Framework 6 i log4net.</span><span class="sxs-lookup"><span data-stu-id="73fd7-141">Many of the dependencies you're using are available for .NET, including Entity Framework 6 and log4net.</span></span> <span data-ttu-id="73fd7-142">Jeśli nie ma dostępnej wersji platformy .NET lub .NET Standard, można często użyć wersji .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="73fd7-142">If there's no .NET or .NET Standard version available, the .NET Framework version can often be used.</span></span> <span data-ttu-id="73fd7-143">Przebieg może się różnić.</span><span class="sxs-lookup"><span data-stu-id="73fd7-143">Your mileage may vary.</span></span> <span data-ttu-id="73fd7-144">Każdy używany interfejs API, który nie jest dostępny w środowisku .NET, powoduje błąd w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="73fd7-144">Any API used that isn't available in .NET causes a runtime error.</span></span> <span data-ttu-id="73fd7-145">Program Visual Studio powiadamia o takich pakietach.</span><span class="sxs-lookup"><span data-stu-id="73fd7-145">Visual Studio notifies you of such packages.</span></span> <span data-ttu-id="73fd7-146">Żółta ikona pojawia się w węźle **odwołania** projektu w **Eksplorator rozwiązań**.</span><span class="sxs-lookup"><span data-stu-id="73fd7-146">A yellow icon appears on the project's **References** node in **Solution Explorer**.</span></span>

<span data-ttu-id="73fd7-147">W Blazor projekcie eshop opartym na programie można zobaczyć zainstalowane pakiety.</span><span class="sxs-lookup"><span data-stu-id="73fd7-147">In the Blazor-based eShop project, you can see the packages that are installed.</span></span> <span data-ttu-id="73fd7-148">Wcześniej plik *packages.config* wystawiony na każdy pakiet użyty w projekcie, co spowodowało niemal 50 wierszy.</span><span class="sxs-lookup"><span data-stu-id="73fd7-148">Previously, the *packages.config* file listed every package used in the project, resulting in a file almost 50 lines long.</span></span> <span data-ttu-id="73fd7-149">Fragment *packages.config* jest następujący:</span><span class="sxs-lookup"><span data-stu-id="73fd7-149">A snippet of *packages.config* is:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  ...
  <package id="Microsoft.ApplicationInsights.Agent.Intercept" version="2.4.0" targetFramework="net472" />
  <package id="Microsoft.ApplicationInsights.DependencyCollector" version="2.9.1" targetFramework="net472" />
  <package id="Microsoft.ApplicationInsights.PerfCounterCollector" version="2.9.1" targetFramework="net472" />
  <package id="Microsoft.ApplicationInsights.Web" version="2.9.1" targetFramework="net472" />
  <package id="Microsoft.ApplicationInsights.WindowsServer" version="2.9.1" targetFramework="net472" />
  <package id="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel" version="2.9.1" targetFramework="net472" />
  <package id="Microsoft.AspNet.FriendlyUrls" version="1.0.2" targetFramework="net472" />
  <package id="Microsoft.AspNet.FriendlyUrls.Core" version="1.0.2" targetFramework="net472" />
  <package id="Microsoft.AspNet.ScriptManager.MSAjax" version="5.0.0" targetFramework="net472" />
  <package id="Microsoft.AspNet.ScriptManager.WebForms" version="5.0.0" targetFramework="net472" />
  ...
  <package id="System.Memory" version="4.5.1" targetFramework="net472" />
  <package id="System.Numerics.Vectors" version="4.4.0" targetFramework="net472" />
  <package id="System.Runtime.CompilerServices.Unsafe" version="4.5.0" targetFramework="net472" />
  <package id="System.Threading.Channels" version="4.5.0" targetFramework="net472" />
  <package id="System.Threading.Tasks.Extensions" version="4.5.1" targetFramework="net472" />
  <package id="WebGrease" version="1.6.0" targetFramework="net472" />
</packages>
```

<span data-ttu-id="73fd7-150">`<packages>`Element zawiera wszystkie wymagane zależności.</span><span class="sxs-lookup"><span data-stu-id="73fd7-150">The `<packages>` element includes all necessary dependencies.</span></span> <span data-ttu-id="73fd7-151">Trudno jest zidentyfikować, które z tych pakietów są uwzględniane, ponieważ są one wymagane.</span><span class="sxs-lookup"><span data-stu-id="73fd7-151">It's difficult to identify which of these packages are included because you require them.</span></span> <span data-ttu-id="73fd7-152">Niektóre `<package>` elementy są wyświetlane po prostu do zaspokajania potrzeb wymaganych zależności.</span><span class="sxs-lookup"><span data-stu-id="73fd7-152">Some `<package>` elements are listed simply to satisfy the needs of dependencies you require.</span></span>

<span data-ttu-id="73fd7-153">BlazorProjekt zawiera listę zależności, które są wymagane w `<ItemGroup>` elemencie w pliku projektu:</span><span class="sxs-lookup"><span data-stu-id="73fd7-153">The Blazor project lists the dependencies you require within an `<ItemGroup>` element in the project file:</span></span>

```xml
<ItemGroup>
    <PackageReference Include="Autofac" Version="4.9.3" />
    <PackageReference Include="EntityFramework" Version="6.4.4" />
    <PackageReference Include="log4net" Version="2.0.12" />
    <PackageReference Include="Microsoft.Extensions.Logging.Log4Net.AspNetCore" Version="2.2.12" />
</ItemGroup>
```

<span data-ttu-id="73fd7-154">Jednym pakietem NuGet, który upraszcza życie deweloperów formularzy sieci Web, jest [pakiet zgodności systemu Windows](../../core/porting/windows-compat-pack.md).</span><span class="sxs-lookup"><span data-stu-id="73fd7-154">One NuGet package that simplifies the life of Web Forms developers is the [Windows Compatibility Pack](../../core/porting/windows-compat-pack.md).</span></span> <span data-ttu-id="73fd7-155">Chociaż platforma .NET działa na wielu platformach, niektóre funkcje są dostępne tylko w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="73fd7-155">Although .NET is cross-platform, some features are only available on Windows.</span></span> <span data-ttu-id="73fd7-156">Funkcje specyficzne dla systemu Windows są udostępniane przez zainstalowanie pakietu zgodności.</span><span class="sxs-lookup"><span data-stu-id="73fd7-156">Windows-specific features are made available by installing the compatibility pack.</span></span> <span data-ttu-id="73fd7-157">Przykłady takich funkcji obejmują rejestr, WMI i usługi katalogowe.</span><span class="sxs-lookup"><span data-stu-id="73fd7-157">Examples of such features include the Registry, WMI, and Directory Services.</span></span> <span data-ttu-id="73fd7-158">Pakiet dodaje około 20 000 interfejsów API i aktywuje wiele usług, za pomocą których użytkownik może już znać.</span><span class="sxs-lookup"><span data-stu-id="73fd7-158">The package adds around 20,000 APIs and activates many services with which you may already be familiar.</span></span> <span data-ttu-id="73fd7-159">Projekt eShop nie wymaga pakietu zgodności. ale jeśli projekty korzystają z funkcji specyficznych dla systemu Windows, pakiet ułatwia pracę z migracją.</span><span class="sxs-lookup"><span data-stu-id="73fd7-159">The eShop project doesn't require the compatibility pack; but if your projects use Windows-specific features, the package eases the migration efforts.</span></span>

## <a name="enable-startup-process"></a><span data-ttu-id="73fd7-160">Włącz proces uruchamiania</span><span class="sxs-lookup"><span data-stu-id="73fd7-160">Enable startup process</span></span>

<span data-ttu-id="73fd7-161">Proces uruchamiania programu Blazor został zmieniony z formularzy sieci Web i działa podobnie jak w przypadku innych usług ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="73fd7-161">The startup process for Blazor has changed from Web Forms and follows a similar setup for other ASP.NET Core services.</span></span> <span data-ttu-id="73fd7-162">Po stronie serwera Blazor składniki są uruchamiane w ramach normalnej aplikacji ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="73fd7-162">When hosted server-side, Blazor components are run as part of a normal ASP.NET Core app.</span></span> <span data-ttu-id="73fd7-163">W przypadku korzystania z przeglądarki w WebAssembly programie Blazor składniki używają podobnego modelu hostingu.</span><span class="sxs-lookup"><span data-stu-id="73fd7-163">When hosted in the browser with WebAssembly, Blazor components use a similar hosting model.</span></span> <span data-ttu-id="73fd7-164">Różnica polega na tym, że składniki są uruchamiane jako osobna usługa z dowolnego procesu zaplecza.</span><span class="sxs-lookup"><span data-stu-id="73fd7-164">The difference is the components are run as a separate service from any of the backend processes.</span></span> <span data-ttu-id="73fd7-165">W obu przypadkach uruchamianie jest podobne.</span><span class="sxs-lookup"><span data-stu-id="73fd7-165">Either way, the startup is similar.</span></span>

<span data-ttu-id="73fd7-166">Plik *Global.asax.cs* jest domyślną stroną startową dla projektów formularzy sieci Web.</span><span class="sxs-lookup"><span data-stu-id="73fd7-166">The *Global.asax.cs* file is the default startup page for Web Forms projects.</span></span> <span data-ttu-id="73fd7-167">W projekcie eShop ten plik konfiguruje kontener Inversion of Control (IoC) i obsługuje różne zdarzenia cyklu życia aplikacji lub żądania.</span><span class="sxs-lookup"><span data-stu-id="73fd7-167">In the eShop project, this file configures the Inversion of Control (IoC) container and handles the various lifecycle events of the app or request.</span></span> <span data-ttu-id="73fd7-168">Niektóre z tych zdarzeń są obsługiwane za pomocą oprogramowania pośredniczącego (takiego jak `Application_BeginRequest` ).</span><span class="sxs-lookup"><span data-stu-id="73fd7-168">Some of these events are handled with middleware (such as `Application_BeginRequest`).</span></span> <span data-ttu-id="73fd7-169">Inne zdarzenia wymagają zastąpienia określonych usług za pośrednictwem iniekcji zależności (DI).</span><span class="sxs-lookup"><span data-stu-id="73fd7-169">Other events require the overriding of specific services via dependency injection (DI).</span></span>

<span data-ttu-id="73fd7-170">Na przykład plik *Global.asax.cs* dla eshop zawiera następujący kod:</span><span class="sxs-lookup"><span data-stu-id="73fd7-170">By way of example, the *Global.asax.cs* file for eShop, contains the following code:</span></span>

```csharp
public class Global : HttpApplication, IContainerProviderAccessor
{
    private static readonly ILog _log = LogManager.GetLogger(System.Reflection.MethodBase.GetCurrentMethod().DeclaringType);

    static IContainerProvider _containerProvider;
    IContainer container;

    public IContainerProvider ContainerProvider
    {
        get { return _containerProvider; }
    }

    protected void Application_Start(object sender, EventArgs e)
    {
        // Code that runs on app startup
        RouteConfig.RegisterRoutes(RouteTable.Routes);
        BundleConfig.RegisterBundles(BundleTable.Bundles);
        ConfigureContainer();
        ConfigDataBase();
    }

    /// <summary>
    /// Track the machine name and the start time for the session inside the current session
    /// </summary>
    protected void Session_Start(Object sender, EventArgs e)
    {
        HttpContext.Current.Session["MachineName"] = Environment.MachineName;
        HttpContext.Current.Session["SessionStartTime"] = DateTime.Now;
    }

    /// <summary>
    /// https://autofaccn.readthedocs.io/en/latest/integration/webforms.html
    /// </summary>
    private void ConfigureContainer()
    {
        var builder = new ContainerBuilder();
        var mockData = bool.Parse(ConfigurationManager.AppSettings["UseMockData"]);
        builder.RegisterModule(new ApplicationModule(mockData));
        container = builder.Build();
        _containerProvider = new ContainerProvider(container);
    }

    private void ConfigDataBase()
    {
        var mockData = bool.Parse(ConfigurationManager.AppSettings["UseMockData"]);

        if (!mockData)
        {
            Database.SetInitializer<CatalogDBContext>(container.Resolve<CatalogDBInitializer>());
        }
    }

    protected void Application_BeginRequest(object sender, EventArgs e)
    {
        //set the property to our new object
        LogicalThreadContext.Properties["activityid"] = new ActivityIdHelper();

        LogicalThreadContext.Properties["requestinfo"] = new WebRequestInfo();

        _log.Debug("Application_BeginRequest");
    }
}
```

<span data-ttu-id="73fd7-171">Poprzedni plik stał się `Startup` klasą po stronie serwera Blazor :</span><span class="sxs-lookup"><span data-stu-id="73fd7-171">The preceding file becomes the `Startup` class in server-side Blazor:</span></span>

```csharp
public class Startup
{
    public Startup(IConfiguration configuration, IWebHostEnvironment env)
    {
        Configuration = configuration;
        Env = env;
    }

    public IConfiguration Configuration { get; }

    public IWebHostEnvironment Env { get; }

    // This method gets called by the runtime. Use this method to add services to the container.
    // For more information on how to configure your application, visit https://go.microsoft.com/fwlink/?LinkID=398940
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddRazorPages();
        services.AddServerSideBlazor();

        if (Configuration.GetValue<bool>("UseMockData"))
        {
            services.AddSingleton<ICatalogService, CatalogServiceMock>();
        }
        else
        {
            services.AddScoped<ICatalogService, CatalogService>();
            services.AddScoped<IDatabaseInitializer<CatalogDBContext>, CatalogDBInitializer>();
            services.AddSingleton<CatalogItemHiLoGenerator>();
            services.AddScoped(_ => new CatalogDBContext(Configuration.GetConnectionString("CatalogDBContext")));
        }
    }

    // This method gets called by the runtime. Use this method to configure the HTTP request pipeline.
    public void Configure(IApplicationBuilder app, ILoggerFactory loggerFactory)
    {
        loggerFactory.AddLog4Net("log4Net.xml");

        if (Env.IsDevelopment())
        {
            app.UseDeveloperExceptionPage();
        }
        else
        {
            app.UseExceptionHandler("/Home/Error");
        }

        // Middleware for Application_BeginRequest
        app.Use((ctx, next) =>
        {
            LogicalThreadContext.Properties["activityid"] = new ActivityIdHelper(ctx);
            LogicalThreadContext.Properties["requestinfo"] = new WebRequestInfo(ctx);
            return next();
        });

        app.UseStaticFiles();

        app.UseRouting();

        app.UseEndpoints(endpoints =>
        {
            endpoints.MapBlazorHub();
            endpoints.MapFallbackToPage("/_Host");
        });

        ConfigDataBase(app);
    }

    private void ConfigDataBase(IApplicationBuilder app)
    {
        using (var scope = app.ApplicationServices.CreateScope())
        {
            var initializer = scope.ServiceProvider.GetService<IDatabaseInitializer<CatalogDBContext>>();

            if (initializer != null)
            {
                Database.SetInitializer(initializer);
            }
        }
    }
}
```

<span data-ttu-id="73fd7-172">Jedną z znaczących zmian, które można zauważyć w formularzach sieci Web, jest wyeksponowanie DI.</span><span class="sxs-lookup"><span data-stu-id="73fd7-172">One significant change you may notice from Web Forms is the prominence of DI.</span></span> <span data-ttu-id="73fd7-173">DI ma regułę identyfikatora GUID w projekcie ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="73fd7-173">DI has been a guiding principle in the ASP.NET Core design.</span></span> <span data-ttu-id="73fd7-174">Obsługuje on dostosowanie niemal wszystkich aspektów ASP.NET Core Framework.</span><span class="sxs-lookup"><span data-stu-id="73fd7-174">It supports customization of almost all aspects of the ASP.NET Core framework.</span></span> <span data-ttu-id="73fd7-175">Istnieje nawet wbudowany dostawca usług, który może być używany w wielu scenariuszach.</span><span class="sxs-lookup"><span data-stu-id="73fd7-175">There's even a built-in service provider that can be used for many scenarios.</span></span> <span data-ttu-id="73fd7-176">Jeśli wymagane jest dalsze dostosowanie, może ono być obsługiwane przez wiele projektów społecznościowych.</span><span class="sxs-lookup"><span data-stu-id="73fd7-176">If more customization is required, it can be supported by many community projects.</span></span> <span data-ttu-id="73fd7-177">Na przykład możesz przenieść swoją inwestycję w inną firmę.</span><span class="sxs-lookup"><span data-stu-id="73fd7-177">For example, you can carry forward your third-party DI library investment.</span></span>

<span data-ttu-id="73fd7-178">W oryginalnej aplikacji eShop istnieje pewna Konfiguracja zarządzania sesją.</span><span class="sxs-lookup"><span data-stu-id="73fd7-178">In the original eShop app, there's some configuration for session management.</span></span> <span data-ttu-id="73fd7-179">Ze względu na to, że po stronie serwera Blazor ASP.NET Core sygnalizujący komunikację, stan sesji nie jest obsługiwany, ponieważ połączenia mogą wystąpić niezależnie od kontekstu http.</span><span class="sxs-lookup"><span data-stu-id="73fd7-179">Since server-side Blazor uses ASP.NET Core SignalR for communication, the session state isn't supported as the connections may occur independent of an HTTP context.</span></span> <span data-ttu-id="73fd7-180">Aplikacja, która używa stanu sesji, wymaga ponownej architektury przed uruchomieniem Blazor aplikacji.</span><span class="sxs-lookup"><span data-stu-id="73fd7-180">An app that uses the session state requires rearchitecting before running as a Blazor app.</span></span>

<span data-ttu-id="73fd7-181">Aby uzyskać więcej informacji o uruchamianiu aplikacji, zobacz [Uruchamianie aplikacji](app-startup.md).</span><span class="sxs-lookup"><span data-stu-id="73fd7-181">For more information about app startup, see [App startup](app-startup.md).</span></span>

## <a name="migrate-http-modules-and-handlers-to-middleware"></a><span data-ttu-id="73fd7-182">Migrowanie modułów i programów obsługi HTTP do oprogramowania pośredniczącego</span><span class="sxs-lookup"><span data-stu-id="73fd7-182">Migrate HTTP modules and handlers to middleware</span></span>

<span data-ttu-id="73fd7-183">Moduły i programy obsługi HTTP są typowymi wzorcami w formularzach sieci Web w celu kontrolowania potoku żądań HTTP.</span><span class="sxs-lookup"><span data-stu-id="73fd7-183">HTTP modules and handlers are common patterns in Web Forms to control the HTTP request pipeline.</span></span> <span data-ttu-id="73fd7-184">Klasy implementujące `IHttpModule` lub `IHttpHandler` mogą być zarejestrowane i przetwarzać żądania przychodzące.</span><span class="sxs-lookup"><span data-stu-id="73fd7-184">Classes that implement `IHttpModule` or `IHttpHandler` could be registered and process incoming requests.</span></span> <span data-ttu-id="73fd7-185">Formularze sieci Web konfigurują moduły i programy obsługi w pliku *web.config* .</span><span class="sxs-lookup"><span data-stu-id="73fd7-185">Web Forms configure modules and handlers in the *web.config* file.</span></span> <span data-ttu-id="73fd7-186">Formularze sieci Web są również intensywnie oparte na obsłudze zdarzeń cyklu życia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="73fd7-186">Web Forms is also heavily based on app lifecycle event handling.</span></span> <span data-ttu-id="73fd7-187">ASP.NET Core zamiast tego używa oprogramowania pośredniczącego.</span><span class="sxs-lookup"><span data-stu-id="73fd7-187">ASP.NET Core uses middleware instead.</span></span> <span data-ttu-id="73fd7-188">Oprogramowanie pośredniczące jest zarejestrowane w `Configure` metodzie `Startup` klasy.</span><span class="sxs-lookup"><span data-stu-id="73fd7-188">Middleware is registered in the `Configure` method of the `Startup` class.</span></span> <span data-ttu-id="73fd7-189">Kolejność wykonywania oprogramowania pośredniczącego zależy od kolejności rejestracji.</span><span class="sxs-lookup"><span data-stu-id="73fd7-189">Middleware execution order is determined by the registration order.</span></span>

<span data-ttu-id="73fd7-190">W sekcji [Włączanie procesu uruchamiania](#enable-startup-process) zdarzenie cyklu życia zostało zgłoszone przez formularze sieci Web jako `Application_BeginRequest` metodę.</span><span class="sxs-lookup"><span data-stu-id="73fd7-190">In the [Enable startup process](#enable-startup-process) section, a lifecycle event was raised by Web Forms as the `Application_BeginRequest` method.</span></span> <span data-ttu-id="73fd7-191">To zdarzenie nie jest dostępne w ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="73fd7-191">This event isn't available in ASP.NET Core.</span></span> <span data-ttu-id="73fd7-192">Jednym ze sposobów osiągnięcia tego zachowania jest wdrożenie oprogramowania pośredniczącego, jak pokazano w przykładzie pliku *Startup.cs* .</span><span class="sxs-lookup"><span data-stu-id="73fd7-192">One way to achieve this behavior is to implement middleware as seen in the *Startup.cs* file example.</span></span> <span data-ttu-id="73fd7-193">To oprogramowanie pośredniczące wykonuje tę samą logikę, a następnie przekazuje kontrolę do kolejnej procedury obsługi w potoku programu pośredniczącego.</span><span class="sxs-lookup"><span data-stu-id="73fd7-193">This middleware does the same logic and then transfers control to the next handler in the middleware pipeline.</span></span>

<span data-ttu-id="73fd7-194">Aby uzyskać więcej informacji na temat migrowania modułów i programów obsługi, zobacz [Migrowanie programów obsługi i modułów HTTP w celu ASP.NET Core oprogramowania pośredniczącego](/aspnet/core/migration/http-modules).</span><span class="sxs-lookup"><span data-stu-id="73fd7-194">For more information on migrating modules and handlers, see [Migrate HTTP handlers and modules to ASP.NET Core middleware](/aspnet/core/migration/http-modules).</span></span>

## <a name="migrate-static-files"></a><span data-ttu-id="73fd7-195">Migrowanie plików statycznych</span><span class="sxs-lookup"><span data-stu-id="73fd7-195">Migrate static files</span></span>

<span data-ttu-id="73fd7-196">Aby można było obsługiwać pliki statyczne (na przykład HTML, CSS, obrazy i JavaScript), pliki muszą być udostępniane przez oprogramowanie pośredniczące.</span><span class="sxs-lookup"><span data-stu-id="73fd7-196">To serve static files (for example, HTML, CSS, images, and JavaScript), the files must be exposed by middleware.</span></span> <span data-ttu-id="73fd7-197">Wywołanie `UseStaticFiles` metody umożliwia obsługę plików statycznych z ścieżki katalogu głównego sieci Web.</span><span class="sxs-lookup"><span data-stu-id="73fd7-197">Calling the `UseStaticFiles` method enables the serving of static files from the web root path.</span></span> <span data-ttu-id="73fd7-198">Domyślny katalog główny sieci Web to *wwwroot*, ale można go dostosować.</span><span class="sxs-lookup"><span data-stu-id="73fd7-198">The default web root directory is *wwwroot*, but it can be customized.</span></span> <span data-ttu-id="73fd7-199">Jak zawarta w `Configure` metodzie `Startup` klasy eshop:</span><span class="sxs-lookup"><span data-stu-id="73fd7-199">As included in the `Configure` method of eShop's `Startup` class:</span></span>

```csharp
public void Configure(IApplicationBuilder app)
{
    ...

    app.UseStaticFiles();

    ...
}
```

<span data-ttu-id="73fd7-200">Projekt eShop umożliwia dostęp do podstawowego pliku statycznego.</span><span class="sxs-lookup"><span data-stu-id="73fd7-200">The eShop project enables basic static file access.</span></span> <span data-ttu-id="73fd7-201">Istnieje wiele dostosowań dostępnych w przypadku dostępu do pliku statycznego.</span><span class="sxs-lookup"><span data-stu-id="73fd7-201">There are many customizations available for static file access.</span></span> <span data-ttu-id="73fd7-202">Aby uzyskać informacje na temat włączania plików domyślnych lub przeglądarki plików, zobacz [pliki statyczne w ASP.NET Core](/aspnet/core/fundamentals/static-files).</span><span class="sxs-lookup"><span data-stu-id="73fd7-202">For information on enabling default files or a file browser, see [Static files in ASP.NET Core](/aspnet/core/fundamentals/static-files).</span></span>

## <a name="migrate-runtime-bundling-and-minification-setup"></a><span data-ttu-id="73fd7-203">Migruj konfigurację i minifikacja środowiska uruchomieniowego</span><span class="sxs-lookup"><span data-stu-id="73fd7-203">Migrate runtime bundling and minification setup</span></span>

<span data-ttu-id="73fd7-204">Tworzenie i minifikacja to techniki optymalizacji wydajności umożliwiające zmniejszenie liczby i rozmiaru żądań serwera w celu pobrania określonych typów plików.</span><span class="sxs-lookup"><span data-stu-id="73fd7-204">Bundling and minification are performance optimization techniques for reducing the number and size of server requests to retrieve certain file types.</span></span> <span data-ttu-id="73fd7-205">JavaScript i CSS są często poddawane pewnej formie minifikacja przed wysłaniem do klienta.</span><span class="sxs-lookup"><span data-stu-id="73fd7-205">JavaScript and CSS often undergo some form of bundling or minification before being sent to the client.</span></span> <span data-ttu-id="73fd7-206">W programie ASP.NET Web Forms te optymalizacje są obsługiwane w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="73fd7-206">In ASP.NET Web Forms, these optimizations are handled at runtime.</span></span> <span data-ttu-id="73fd7-207">Konwencje optymalizacji są zdefiniowane *App_Start pliku/bundleconfig.cs* .</span><span class="sxs-lookup"><span data-stu-id="73fd7-207">The optimization conventions are defined an *App_Start/BundleConfig.cs* file.</span></span> <span data-ttu-id="73fd7-208">W ASP.NET Core zostanie przyjęte bardziej deklaracyjne podejście.</span><span class="sxs-lookup"><span data-stu-id="73fd7-208">In ASP.NET Core, a more declarative approach is adopted.</span></span> <span data-ttu-id="73fd7-209">Plik zawiera listę plików, które mają być zminimalizowanego, oraz określonych ustawień minifikacja.</span><span class="sxs-lookup"><span data-stu-id="73fd7-209">A file lists the files to be minified, along with specific minification settings.</span></span>

<span data-ttu-id="73fd7-210">Aby uzyskać więcej informacji na temat grupowania i minifikacja, zobacz [zestawy i zminifikować zasobów statycznych w ASP.NET Core](/aspnet/core/client-side/bundling-and-minification).</span><span class="sxs-lookup"><span data-stu-id="73fd7-210">For more information on bundling and minification, see [Bundle and minify static assets in ASP.NET Core](/aspnet/core/client-side/bundling-and-minification).</span></span>

## <a name="migrate-aspx-pages"></a><span data-ttu-id="73fd7-211">Migrowanie stron ASPX</span><span class="sxs-lookup"><span data-stu-id="73fd7-211">Migrate ASPX pages</span></span>

<span data-ttu-id="73fd7-212">Strona w aplikacji formularzy sieci Web jest plikiem z rozszerzeniem *. aspx* .</span><span class="sxs-lookup"><span data-stu-id="73fd7-212">A page in a Web Forms app is a file with the *.aspx* extension.</span></span> <span data-ttu-id="73fd7-213">Strona formularzy sieci Web może być często mapowana na składnik programu Blazor .</span><span class="sxs-lookup"><span data-stu-id="73fd7-213">A Web Forms page can often be mapped to a component in Blazor.</span></span> <span data-ttu-id="73fd7-214">BlazorSkładnik jest tworzony w pliku z rozszerzeniem *. Razor* .</span><span class="sxs-lookup"><span data-stu-id="73fd7-214">A Blazor component is authored in a file with the *.razor* extension.</span></span> <span data-ttu-id="73fd7-215">W przypadku projektu eShop pięć stron jest konwertowanych na stronę Razor.</span><span class="sxs-lookup"><span data-stu-id="73fd7-215">For the eShop project, five pages are converted to a Razor page.</span></span>

<span data-ttu-id="73fd7-216">Na przykład widok szczegółów składa się z trzech plików w projekcie formularzy sieci Web: *details. aspx*, *details.aspx.cs* i *details.aspx.Designer.cs*.</span><span class="sxs-lookup"><span data-stu-id="73fd7-216">For example, the details view comprises three files in the Web Forms project: *Details.aspx*, *Details.aspx.cs*, and *Details.aspx.designer.cs*.</span></span> <span data-ttu-id="73fd7-217">Podczas konwertowania do Blazor , kod źródłowy i znaczniki są łączone do *details. Razor*.</span><span class="sxs-lookup"><span data-stu-id="73fd7-217">When converting to Blazor, the code-behind and markup are combined into *Details.razor*.</span></span> <span data-ttu-id="73fd7-218">Kompilacja Razor (równoważna z plikami *Designer.cs* ) jest przechowywana w katalogu *obj* i nie jest domyślnie wyświetlana w **Eksplorator rozwiązań**.</span><span class="sxs-lookup"><span data-stu-id="73fd7-218">Razor compilation (equivalent to what's in *.designer.cs* files) is stored in the *obj* directory and isn't, by default, viewable in **Solution Explorer**.</span></span> <span data-ttu-id="73fd7-219">Strona formularzy sieci Web składa się z następujących oznaczeń:</span><span class="sxs-lookup"><span data-stu-id="73fd7-219">The Web Forms page consists of the following markup:</span></span>

```aspx-csharp
<%@ Page Title="Details" Language="C#" MasterPageFile="~/Site.Master" AutoEventWireup="true" CodeBehind="Details.aspx.cs" Inherits="eShopLegacyWebForms.Catalog.Details" %>

<asp:Content ID="Details" ContentPlaceHolderID="MainContent" runat="server">
    <h2 class="esh-body-title">Details</h2>

    <div class="container">
        <div class="row">
            <asp:Image runat="server" CssClass="col-md-6 esh-picture" ImageUrl='<%#"/Pics/" + product.PictureFileName%>' />
            <dl class="col-md-6 dl-horizontal">
                <dt>Name
                </dt>

                <dd>
                    <asp:Label runat="server" Text='<%#product.Name%>' />
                </dd>

                <dt>Description
                </dt>

                <dd>
                    <asp:Label runat="server" Text='<%#product.Description%>' />
                </dd>

                <dt>Brand
                </dt>

                <dd>
                    <asp:Label runat="server" Text='<%#product.CatalogBrand.Brand%>' />
                </dd>

                <dt>Type
                </dt>

                <dd>
                    <asp:Label runat="server" Text='<%#product.CatalogType.Type%>' />
                </dd>
                <dt>Price
                </dt>

                <dd>
                    <asp:Label CssClass="esh-price" runat="server" Text='<%#product.Price%>' />
                </dd>

                <dt>Picture name
                </dt>

                <dd>
                    <asp:Label runat="server" Text='<%#product.PictureFileName%>' />
                </dd>

                <dt>Stock
                </dt>

                <dd>
                    <asp:Label runat="server" Text='<%#product.AvailableStock%>' />
                </dd>

                <dt>Restock
                </dt>

                <dd>
                    <asp:Label runat="server" Text='<%#product.RestockThreshold%>' />
                </dd>

                <dt>Max stock
                </dt>

                <dd>
                    <asp:Label runat="server" Text='<%#product.MaxStockThreshold%>' />
                </dd>

            </dl>
        </div>

        <div class="form-actions no-color esh-link-list">
            <a runat="server" href='<%# GetRouteUrl("EditProductRoute", new {id =product.Id}) %>' class="esh-link-item">Edit
            </a>
            |
            <a runat="server" href="~" class="esh-link-item">Back to list
            </a>
        </div>

    </div>
</asp:Content>
```

<span data-ttu-id="73fd7-220">Poprzedzający kod znacznika zawiera następujący kod:</span><span class="sxs-lookup"><span data-stu-id="73fd7-220">The preceding markup's code-behind includes the following code:</span></span>

```csharp
using eShopLegacyWebForms.Models;
using eShopLegacyWebForms.Services;
using log4net;
using System;
using System.Web.UI;

namespace eShopLegacyWebForms.Catalog
{
    public partial class Details : System.Web.UI.Page
    {
        private static readonly ILog _log = LogManager.GetLogger(System.Reflection.MethodBase.GetCurrentMethod().DeclaringType);

        protected CatalogItem product;

        public ICatalogService CatalogService { get; set; }

        protected void Page_Load(object sender, EventArgs e)
        {
            var productId = Convert.ToInt32(Page.RouteData.Values["id"]);
            _log.Info($"Now loading... /Catalog/Details.aspx?id={productId}");
            product = CatalogService.FindCatalogItem(productId);

            this.DataBind();
        }
    }
}
```

<span data-ttu-id="73fd7-221">W przypadku przekonwertowania na Blazor , Strona formularzy sieci Web tłumaczy do następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="73fd7-221">When converted to Blazor, the Web Forms page translates to the following code:</span></span>

```razor
@page "/Catalog/Details/{id:int}"
@inject ICatalogService CatalogService
@inject ILogger<Details> Logger

<h2 class="esh-body-title">Details</h2>

<div class="container">
    <div class="row">
        <img class="col-md-6 esh-picture" src="@($"/Pics/{_item.PictureFileName}")">

        <dl class="col-md-6 dl-horizontal">
            <dt>
                Name
            </dt>

            <dd>
                @_item.Name
            </dd>

            <dt>
                Description
            </dt>

            <dd>
                @_item.Description
            </dd>

            <dt>
                Brand
            </dt>

            <dd>
                @_item.CatalogBrand.Brand
            </dd>

            <dt>
                Type
            </dt>

            <dd>
                @_item.CatalogType.Type
            </dd>
            <dt>
                Price
            </dt>

            <dd>
                @_item.Price
            </dd>

            <dt>
                Picture name
            </dt>

            <dd>
                @_item.PictureFileName
            </dd>

            <dt>
                Stock
            </dt>

            <dd>
                @_item.AvailableStock
            </dd>

            <dt>
                Restock
            </dt>

            <dd>
                @_item.RestockThreshold
            </dd>

            <dt>
                Max stock
            </dt>

            <dd>
                @_item.MaxStockThreshold
            </dd>

        </dl>
    </div>

    <div class="form-actions no-color esh-link-list">
        <a href="@($"/Catalog/Edit/{_item.Id}")" class="esh-link-item">
            Edit
        </a>
        |
        <a href="/" class="esh-link-item">
            Back to list
        </a>
    </div>

</div>

@code {
    private CatalogItem _item;

    [Parameter]
    public int Id { get; set; }

    protected override void OnInitialized()
    {
        Logger.LogInformation("Now loading... /Catalog/Details/{Id}", Id);

        _item = CatalogService.FindCatalogItem(Id);
    }
}
```

<span data-ttu-id="73fd7-222">Zauważ, że kod i znaczniki są w tym samym pliku.</span><span class="sxs-lookup"><span data-stu-id="73fd7-222">Notice that the code and markup are in the same file.</span></span> <span data-ttu-id="73fd7-223">Wszystkie wymagane usługi są udostępniane przy użyciu `@inject` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="73fd7-223">Any required services are made accessible with the `@inject` attribute.</span></span> <span data-ttu-id="73fd7-224">Na `@page` Tę stronę można uzyskać dostęp do tej strony na `Catalog/Details/{id}` trasie.</span><span class="sxs-lookup"><span data-stu-id="73fd7-224">Per the `@page` directive, this page can be accessed at the `Catalog/Details/{id}` route.</span></span> <span data-ttu-id="73fd7-225">Wartość `{id}` symbolu zastępczego trasy została ograniczona do liczby całkowitej.</span><span class="sxs-lookup"><span data-stu-id="73fd7-225">The value of the route's `{id}` placeholder has been constrained to an integer.</span></span> <span data-ttu-id="73fd7-226">Zgodnie z opisem w sekcji [Routing](pages-routing-layouts.md) , w przeciwieństwie do formularzy sieci Web, składnik Razor jawnie określa swoją trasę i wszystkie parametry, które są zawarte.</span><span class="sxs-lookup"><span data-stu-id="73fd7-226">As described in the [routing](pages-routing-layouts.md) section, unlike Web Forms, a Razor component explicitly states its route and any parameters that are included.</span></span> <span data-ttu-id="73fd7-227">Wiele kontrolek formularzy sieci Web może nie mieć dokładnych odpowiedników w Blazor .</span><span class="sxs-lookup"><span data-stu-id="73fd7-227">Many Web Forms controls may not have exact counterparts in Blazor.</span></span> <span data-ttu-id="73fd7-228">Często istnieje odpowiednik fragmentu kodu HTML, który będzie służyć do tego samego celu.</span><span class="sxs-lookup"><span data-stu-id="73fd7-228">There's often an equivalent HTML snippet that will serve the same purpose.</span></span> <span data-ttu-id="73fd7-229">Na przykład `<asp:Label />` formant może zostać zamieniony na `<label>` element HTML.</span><span class="sxs-lookup"><span data-stu-id="73fd7-229">For example, the `<asp:Label />` control can be replaced with an HTML `<label>` element.</span></span>

### <a name="model-validation-in-no-locblazor"></a><span data-ttu-id="73fd7-230">Walidacja modelu w Blazor</span><span class="sxs-lookup"><span data-stu-id="73fd7-230">Model validation in Blazor</span></span>

<span data-ttu-id="73fd7-231">Jeśli kod formularzy sieci Web zawiera walidację, można przekazać wiele z nich, aby nie było zmian.</span><span class="sxs-lookup"><span data-stu-id="73fd7-231">If your Web Forms code includes validation, you can transfer much of what you have with little-to-no changes.</span></span> <span data-ttu-id="73fd7-232">Korzyścią uruchomienia programu w programie Blazor jest taka sama logika walidacji, bez konieczności wykonywania niestandardowych skryptów języka JavaScript.</span><span class="sxs-lookup"><span data-stu-id="73fd7-232">A benefit to running in Blazor is that the same validation logic can be run without needing custom JavaScript.</span></span> <span data-ttu-id="73fd7-233">Adnotacje danych umożliwiają łatwe sprawdzanie poprawności modeli.</span><span class="sxs-lookup"><span data-stu-id="73fd7-233">Data annotations enable easy model validation.</span></span>

<span data-ttu-id="73fd7-234">Na przykład strona *Create. aspx* zawiera formularz wprowadzania danych z walidacją.</span><span class="sxs-lookup"><span data-stu-id="73fd7-234">For example, the *Create.aspx* page has a data entry form with validation.</span></span> <span data-ttu-id="73fd7-235">Przykładowy fragment będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="73fd7-235">An example snippet would look like this:</span></span>

```aspx
<div class="form-group">
    <label class="control-label col-md-2">Name</label>
    <div class="col-md-3">
        <asp:TextBox ID="Name" runat="server" CssClass="form-control"></asp:TextBox>
        <asp:RequiredFieldValidator runat="server" ControlToValidate="Name" Display="Dynamic"
            CssClass="field-validation-valid text-danger" ErrorMessage="The Name field is required." />
    </div>
</div>
```

<span data-ttu-id="73fd7-236">W programie Blazor równoważne znaczniki są podane w pliku *Create. Razor* :</span><span class="sxs-lookup"><span data-stu-id="73fd7-236">In Blazor, the equivalent markup is provided in a *Create.razor* file:</span></span>

```razor
<EditForm Model="_item" OnValidSubmit="@...">
    <DataAnnotationsValidator />

    <div class="form-group">
        <label class="control-label col-md-2">Name</label>
        <div class="col-md-3">
            <InputText class="form-control" @bind-Value="_item.Name" />
            <ValidationMessage For="(() => _item.Name)" />
        </div>
    </div>

    ...
</EditForm>
```

<span data-ttu-id="73fd7-237">`EditForm`Kontekst zawiera obsługę walidacji i może być opakowany wokół danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="73fd7-237">The `EditForm` context includes validation support and can be wrapped around an input.</span></span> <span data-ttu-id="73fd7-238">Adnotacje danych są typowym sposobem dodawania walidacji.</span><span class="sxs-lookup"><span data-stu-id="73fd7-238">Data annotations are a common way to add validation.</span></span> <span data-ttu-id="73fd7-239">Takie wsparcie sprawdzania poprawności można dodać za pośrednictwem `DataAnnotationsValidator` składnika.</span><span class="sxs-lookup"><span data-stu-id="73fd7-239">Such validation support can be added via the `DataAnnotationsValidator` component.</span></span> <span data-ttu-id="73fd7-240">Aby uzyskać więcej informacji na temat tego mechanizmu, zobacz [ASP.NET Core Blazor formularzy i walidacji](/aspnet/core/blazor/forms-validation).</span><span class="sxs-lookup"><span data-stu-id="73fd7-240">For more information on this mechanism, see [ASP.NET Core Blazor forms and validation](/aspnet/core/blazor/forms-validation).</span></span>

## <a name="migrate-configuration"></a><span data-ttu-id="73fd7-241">Migruj konfigurację</span><span class="sxs-lookup"><span data-stu-id="73fd7-241">Migrate configuration</span></span>

<span data-ttu-id="73fd7-242">W projekcie formularzy sieci Web dane konfiguracyjne są najczęściej przechowywane w pliku *web.config* .</span><span class="sxs-lookup"><span data-stu-id="73fd7-242">In a Web Forms project, configuration data is most commonly stored in the *web.config* file.</span></span> <span data-ttu-id="73fd7-243">Dostęp do danych konfiguracyjnych z programu `ConfigurationManager` .</span><span class="sxs-lookup"><span data-stu-id="73fd7-243">The configuration data is accessed with `ConfigurationManager`.</span></span> <span data-ttu-id="73fd7-244">Usługi były często wymagane do analizowania obiektów.</span><span class="sxs-lookup"><span data-stu-id="73fd7-244">Services were often required to parse objects.</span></span> <span data-ttu-id="73fd7-245">W przypadku .NET Framework 4.7.2, możliwość tworzenia została dodana do konfiguracji za pośrednictwem `ConfigurationBuilders` .</span><span class="sxs-lookup"><span data-stu-id="73fd7-245">With .NET Framework 4.7.2, composability was added to the configuration via `ConfigurationBuilders`.</span></span> <span data-ttu-id="73fd7-246">Ci deweloperzy mogą dodawać różne źródła dla konfiguracji, która następnie została złożona w czasie wykonywania w celu pobrania niezbędnych wartości.</span><span class="sxs-lookup"><span data-stu-id="73fd7-246">These builders allowed developers to add various sources for the configuration that was then composed at runtime to retrieve the necessary values.</span></span>

<span data-ttu-id="73fd7-247">ASP.NET Core wprowadzono elastyczny system konfiguracji, który pozwala zdefiniować źródło lub źródła konfiguracji używane przez aplikację i wdrożenie.</span><span class="sxs-lookup"><span data-stu-id="73fd7-247">ASP.NET Core introduced a flexible configuration system that allows you to define the configuration source or sources used by your app and deployment.</span></span> <span data-ttu-id="73fd7-248">`ConfigurationBuilder`Infrastruktura, która może być używana w aplikacji formularzy sieci Web, została modelowana po pojęciach używanych w systemie konfiguracji ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="73fd7-248">The `ConfigurationBuilder` infrastructure that you may be using in your Web Forms app was modeled after the concepts used in the ASP.NET Core configuration system.</span></span>

<span data-ttu-id="73fd7-249">Poniższy fragment kodu ilustruje, jak projekt Web Forms eShop używa *web.config* do przechowywania wartości konfiguracyjnych:</span><span class="sxs-lookup"><span data-stu-id="73fd7-249">The following snippet demonstrates how the Web Forms eShop project uses *web.config* to store configuration values:</span></span>

```xml
<configuration>
  <configSections>
    <section name="entityFramework" type="System.Data.Entity.Internal.ConfigFile.EntityFrameworkSection, EntityFramework, Version=6.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" requirePermission="false" />
  </configSections>
  <connectionStrings>
    <add name="CatalogDBContext" connectionString="Data Source=(localdb)\MSSQLLocalDB; Initial Catalog=Microsoft.eShopOnContainers.Services.CatalogDb; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
  </connectionStrings>
  <appSettings>
    <add key="UseMockData" value="true" />
    <add key="UseCustomizationData" value="false" />
  </appSettings>
</configuration>
```

<span data-ttu-id="73fd7-250">Jest to typowe dla wpisów tajnych, takich jak parametry połączenia bazy danych, które mają być przechowywane w *web.config*. Wpisy tajne są bezwątpliwie utrwalane w niezabezpieczonych lokalizacjach, takich jak kontrola źródła.</span><span class="sxs-lookup"><span data-stu-id="73fd7-250">It's common for secrets, such as database connection strings, to be stored within the *web.config*. The secrets are inevitably persisted in unsecure locations, such as source control.</span></span> <span data-ttu-id="73fd7-251">W przypadku Blazor ASP.NET Core wcześniejsza Konfiguracja oparta na kodzie XML jest zastępowana następującym kodem JSON:</span><span class="sxs-lookup"><span data-stu-id="73fd7-251">With Blazor on ASP.NET Core, the preceding XML-based configuration is replaced with the following JSON:</span></span>

```json
{
  "ConnectionStrings": {
    "CatalogDBContext": "Data Source=(localdb)\\MSSQLLocalDB; Initial Catalog=Microsoft.eShopOnContainers.Services.CatalogDb; Integrated Security=True; MultipleActiveResultSets=True;"
  },
  "UseMockData": true,
  "UseCustomizationData": false
}
```

<span data-ttu-id="73fd7-252">Format JSON jest domyślnym formatem konfiguracji; jednak ASP.NET Core obsługuje wiele innych formatów, w tym XML.</span><span class="sxs-lookup"><span data-stu-id="73fd7-252">JSON is the default configuration format; however, ASP.NET Core supports many other formats, including XML.</span></span> <span data-ttu-id="73fd7-253">Istnieje również kilka formatów obsługiwanych przez społeczność.</span><span class="sxs-lookup"><span data-stu-id="73fd7-253">There are also several community-supported formats.</span></span>

<span data-ttu-id="73fd7-254">Konstruktor w Blazor `Startup` klasie projektu akceptuje `IConfiguration` wystąpienie za pomocą metody di, znanej jako iniekcja konstruktora:</span><span class="sxs-lookup"><span data-stu-id="73fd7-254">The constructor in the Blazor project's `Startup` class accepts an `IConfiguration` instance through a DI technique known as constructor injection:</span></span>

```csharp
public class Startup
{
    public Startup(IConfiguration configuration, IWebHostEnvironment env)
    {
        Configuration = configuration;
        Env = env;
    }

    ...
}
```

<span data-ttu-id="73fd7-255">Domyślnie zmienne środowiskowe, pliki JSON (*appsettings.json* i *appSettings. { Environment}. JSON*), a opcje wiersza polecenia są rejestrowane jako prawidłowe źródła konfiguracji w obiekcie Configuration.</span><span class="sxs-lookup"><span data-stu-id="73fd7-255">By default, environment variables, JSON files (*appsettings.json* and *appsettings.{Environment}.json*), and command-line options are registered as valid configuration sources in the configuration object.</span></span> <span data-ttu-id="73fd7-256">Dostęp do źródeł konfiguracji można uzyskać za pośrednictwem programu `Configuration[key]` .</span><span class="sxs-lookup"><span data-stu-id="73fd7-256">The configuration sources can be accessed via `Configuration[key]`.</span></span> <span data-ttu-id="73fd7-257">Bardziej zaawansowaną techniką jest powiązanie danych konfiguracji z obiektami przy użyciu wzorca opcji.</span><span class="sxs-lookup"><span data-stu-id="73fd7-257">A more advanced technique is to bind the configuration data to objects using the options pattern.</span></span> <span data-ttu-id="73fd7-258">Aby uzyskać więcej informacji na temat konfiguracji i wzorca opcji, zobacz odpowiednio [Konfiguracja w ASP.NET Core](/aspnet/core/fundamentals/configuration/) i [wzorzec opcji w ASP.NET Core](/aspnet/core/fundamentals/configuration/options).</span><span class="sxs-lookup"><span data-stu-id="73fd7-258">For more information on configuration and the options pattern, see [Configuration in ASP.NET Core](/aspnet/core/fundamentals/configuration/) and [Options pattern in ASP.NET Core](/aspnet/core/fundamentals/configuration/options), respectively.</span></span>

## <a name="migrate-data-access"></a><span data-ttu-id="73fd7-259">Migrowanie dostępu do danych</span><span class="sxs-lookup"><span data-stu-id="73fd7-259">Migrate data access</span></span>

<span data-ttu-id="73fd7-260">Dostęp do danych jest ważnym aspektem każdej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="73fd7-260">Data access is an important aspect of any app.</span></span> <span data-ttu-id="73fd7-261">Projekt eShop przechowuje informacje o katalogu w bazie danych i pobiera dane z Entity Framework (EF) 6.</span><span class="sxs-lookup"><span data-stu-id="73fd7-261">The eShop project stores catalog information in a database and retrieves the data with Entity Framework (EF) 6.</span></span> <span data-ttu-id="73fd7-262">Ponieważ program Dr 6 jest obsługiwany w programie .NET 5,0, nadal można z niego korzystać.</span><span class="sxs-lookup"><span data-stu-id="73fd7-262">Since EF 6 is supported in .NET 5.0, the project can continue to use it.</span></span>

<span data-ttu-id="73fd7-263">Następujące zmiany związane z EF były niezbędne do eShop:</span><span class="sxs-lookup"><span data-stu-id="73fd7-263">The following EF-related changes were necessary to eShop:</span></span>

- <span data-ttu-id="73fd7-264">W .NET Framework `DbContext` obiekt akceptuje ciąg o *nazwie form = ConnectionString* i używa parametrów połączenia z `ConfigurationManager.AppSettings[ConnectionString]` w celu nawiązania połączenia.</span><span class="sxs-lookup"><span data-stu-id="73fd7-264">In .NET Framework, the `DbContext` object accepts a string of the form *name=ConnectionString* and uses the connection string from `ConfigurationManager.AppSettings[ConnectionString]` to connect.</span></span> <span data-ttu-id="73fd7-265">W programie .NET Core nie jest to obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="73fd7-265">In .NET Core, this isn't supported.</span></span> <span data-ttu-id="73fd7-266">Należy podać parametry połączenia.</span><span class="sxs-lookup"><span data-stu-id="73fd7-266">The connection string must be supplied.</span></span>
- <span data-ttu-id="73fd7-267">Dostęp do bazy danych odbywa się synchronicznie.</span><span class="sxs-lookup"><span data-stu-id="73fd7-267">The database was accessed in a synchronous way.</span></span> <span data-ttu-id="73fd7-268">To działanie może mieć wpływ na skalowalność.</span><span class="sxs-lookup"><span data-stu-id="73fd7-268">Though this works, scalability may suffer.</span></span> <span data-ttu-id="73fd7-269">Ta logika powinna zostać przeniesiona do wzorca asynchronicznego.</span><span class="sxs-lookup"><span data-stu-id="73fd7-269">This logic should be moved to an asynchronous pattern.</span></span>

<span data-ttu-id="73fd7-270">Chociaż nie ma tej samej natywnej obsługi powiązań zestawu danych, Blazor zapewnia elastyczność i moc z obsługą języka C# na stronie Razor.</span><span class="sxs-lookup"><span data-stu-id="73fd7-270">Although there isn't the same native support for dataset binding, Blazor provides flexibility and power with its C# support in a Razor page.</span></span> <span data-ttu-id="73fd7-271">Na przykład można wykonać obliczenia i wyświetlić wynik.</span><span class="sxs-lookup"><span data-stu-id="73fd7-271">For example, you can perform calculations and display the result.</span></span> <span data-ttu-id="73fd7-272">Aby uzyskać więcej informacji na temat wzorców danych w programie Blazor , zobacz rozdział dotyczący [dostępu do danych](data.md) .</span><span class="sxs-lookup"><span data-stu-id="73fd7-272">For more information on data patterns in Blazor, see the [Data access](data.md) chapter.</span></span>

## <a name="architectural-changes"></a><span data-ttu-id="73fd7-273">Zmiany w architekturze</span><span class="sxs-lookup"><span data-stu-id="73fd7-273">Architectural changes</span></span>

<span data-ttu-id="73fd7-274">Na koniec należy wziąć pod uwagę pewne istotne różnice w architekturze podczas migrowania do programu Blazor .</span><span class="sxs-lookup"><span data-stu-id="73fd7-274">Finally, there are some important architectural differences to consider when migrating to Blazor.</span></span> <span data-ttu-id="73fd7-275">Wiele z tych zmian ma zastosowanie do wszystkich elementów opartych na platformie .NET Core lub ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="73fd7-275">Many of these changes are applicable to anything based on .NET Core or ASP.NET Core.</span></span>

<span data-ttu-id="73fd7-276">Ze względu Blazor na to, że program jest oparty na platformie .NET Core, istnieją zagadnienia dotyczące zapewniania pomocy technicznej na platformie .NET Core</span><span class="sxs-lookup"><span data-stu-id="73fd7-276">Because Blazor is built on .NET Core, there are considerations in ensuring support on .NET Core.</span></span> <span data-ttu-id="73fd7-277">Niektóre istotne zmiany obejmują usunięcie następujących funkcji:</span><span class="sxs-lookup"><span data-stu-id="73fd7-277">Some of the major changes include the removal of the following features:</span></span>

- <span data-ttu-id="73fd7-278">Wiele domen aplikacji</span><span class="sxs-lookup"><span data-stu-id="73fd7-278">Multiple AppDomains</span></span>
- <span data-ttu-id="73fd7-279">Komunikacji zdalnej</span><span class="sxs-lookup"><span data-stu-id="73fd7-279">Remoting</span></span>
- <span data-ttu-id="73fd7-280">Zabezpieczenia dostępu kodu (CAS)</span><span class="sxs-lookup"><span data-stu-id="73fd7-280">Code Access Security (CAS)</span></span>
- <span data-ttu-id="73fd7-281">Przejrzystość zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="73fd7-281">Security Transparency</span></span>

<span data-ttu-id="73fd7-282">Aby uzyskać więcej informacji na temat technik umożliwiających identyfikację niezbędnych zmian w celu obsługi programu .NET Core, zobacz [Porting Code from .NET Framework to .NET Core](../../core/porting/index.md).</span><span class="sxs-lookup"><span data-stu-id="73fd7-282">For more information on techniques to identify necessary changes to support running on .NET Core, see [Port your code from .NET Framework to .NET Core](../../core/porting/index.md).</span></span>

<span data-ttu-id="73fd7-283">ASP.NET Core jest reobrazną wersją ASP.NET i zawiera pewne zmiany, które mogą nie być początkowo oczywiste.</span><span class="sxs-lookup"><span data-stu-id="73fd7-283">ASP.NET Core is a reimagined version of ASP.NET and has some changes that may not initially seem obvious.</span></span> <span data-ttu-id="73fd7-284">Główne zmiany są następujące:</span><span class="sxs-lookup"><span data-stu-id="73fd7-284">The main changes are:</span></span>

- <span data-ttu-id="73fd7-285">Brak kontekstu synchronizacji, co oznacza, że nie ma żadnych `HttpContext.Current` , `Thread.CurrentPrincipal` lub innych metod dostępu statycznego</span><span class="sxs-lookup"><span data-stu-id="73fd7-285">No synchronization context, which means there's no `HttpContext.Current`, `Thread.CurrentPrincipal`, or other static accessors</span></span>
- <span data-ttu-id="73fd7-286">Brak kopiowania w tle</span><span class="sxs-lookup"><span data-stu-id="73fd7-286">No shadow copying</span></span>
- <span data-ttu-id="73fd7-287">Brak kolejki żądań</span><span class="sxs-lookup"><span data-stu-id="73fd7-287">No request queue</span></span>

<span data-ttu-id="73fd7-288">Wiele operacji w ASP.NET Core jest asynchronicznych, co umożliwia łatwiejsze ładowanie zadań związanych z operacjami we/wy.</span><span class="sxs-lookup"><span data-stu-id="73fd7-288">Many operations in ASP.NET Core are asynchronous, which allows easier off-loading of I/O-bound tasks.</span></span> <span data-ttu-id="73fd7-289">Ważne jest, aby nigdy nie blokować za pomocą `Task.Wait()` lub `Task.GetResult()` , co może szybko wyczerpać zasoby puli wątków.</span><span class="sxs-lookup"><span data-stu-id="73fd7-289">It's important to never block by using `Task.Wait()` or `Task.GetResult()`, which can quickly exhaust thread pool resources.</span></span>

## <a name="migration-conclusion"></a><span data-ttu-id="73fd7-290">Wniosek o migrację</span><span class="sxs-lookup"><span data-stu-id="73fd7-290">Migration conclusion</span></span>

<span data-ttu-id="73fd7-291">W tym momencie zobaczysz wiele przykładów potrzebnych do przeniesienia projektu formularzy sieci Web do programu Blazor .</span><span class="sxs-lookup"><span data-stu-id="73fd7-291">At this point, you've seen many examples of what it takes to move a Web Forms project to Blazor.</span></span> <span data-ttu-id="73fd7-292">Pełny przykład można znaleźć w projekcie [eShopOn Blazor ](https://github.com/dotnet-architecture/eShopOnBlazor) .</span><span class="sxs-lookup"><span data-stu-id="73fd7-292">For a full example, see the [eShopOnBlazor](https://github.com/dotnet-architecture/eShopOnBlazor) project.</span></span>

>[!div class="step-by-step"]
>[<span data-ttu-id="73fd7-293">Poprzednie</span><span class="sxs-lookup"><span data-stu-id="73fd7-293">Previous</span></span>](security-authentication-authorization.md)
