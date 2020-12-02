---
title: 'Zabezpieczenia: uwierzytelnianie i autoryzacja w ASP.NET Web Forms i Blazor'
description: Dowiedz się, jak obsługiwać uwierzytelnianie i autoryzację w ASP.NET Web Forms i Blazor .
author: ardalis
ms.author: daroth
no-loc:
- Blazor
ms.date: 11/20/2020
ms.openlocfilehash: 0344960237a5d9da61eb0d85987c44e136f1be48
ms.sourcegitcommit: 2f485e721f7f34b87856a51181b5b56624b31fd5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/02/2020
ms.locfileid: "96509848"
---
# <a name="security-authentication-and-authorization-in-aspnet-web-forms-and-no-locblazor"></a>Zabezpieczenia: uwierzytelnianie i autoryzacja w ASP.NET Web Forms i Blazor

Migrowanie z aplikacji ASP.NET Web Forms do programu Blazor niemal z pewnością wymaga aktualizacji sposobu uwierzytelniania i autoryzacji, przy założeniu, że aplikacja ma skonfigurowane uwierzytelnianie. W tym rozdziale zawarto informacje na temat migracji z modelu uniwersalnego dostawcy formularzy sieci Web ASP.NET (dla członkostwa, ról i profilów użytkowników) oraz sposobu pracy z tożsamością ASP.NET Core z Blazor aplikacji. Ten rozdział będzie obejmować ogólne kroki i zagadnienia, ale szczegółowe instrukcje i skrypty można znaleźć w dokumentacji, do której się odwołuje.

## <a name="aspnet-universal-providers"></a>ASP.NET dostawcy uniwersalnego

Od ASP.NET 2,0 platforma formularzy sieci Web ASP.NET obsługuje model dostawcy dla różnych funkcji, w tym do członkostwa. Uniwersalny dostawca członkostwa wraz z opcjonalnym dostawcą roli jest często wdrażany przy użyciu aplikacji formularzy sieci Web ASP.NET. Oferuje ona niezawodny i bezpieczny sposób zarządzania uwierzytelnianiem i autoryzacją, które w dalszym ciągu działają prawidłowo. Najnowsza oferta tych dostawców uniwersalnych jest dostępna jako pakiet NuGet, [Microsoft. ASPNET. Providers](https://www.nuget.org/packages/Microsoft.AspNet.Providers).

Dostawcy Uniwersalni pracują ze schematem bazy danych SQL, który zawiera tabele takie jak `aspnet_Applications` ,, `aspnet_Membership` `aspnet_Roles` i `aspnet_Users` . Po skonfigurowaniu [ poleceniaaspnet_regsql.exe](/previous-versions/ms229862(v=vs.140))dostawcy instalują tabele i procedury składowane, które zawierają wszystkie niezbędne zapytania i polecenia do pracy z danymi źródłowymi. Schemat bazy danych i te procedury składowane nie są zgodne z nowszymi ASP.NET Identity i ASP.NET Core systemami tożsamości, dlatego istniejące dane muszą zostać zmigrowane do nowego systemu. Rysunek 1 przedstawia przykładowy schemat tabeli skonfigurowany dla dostawców uniwersalnych.

![Schemat dostawców uniwersalnych](./media/security/membership-tables.png)

Dostawca uniwersalny obsługuje użytkowników, członkostwo, role i profile. Użytkownicy są przypisani globalnie unikatowymi identyfikatorami i podstawowymi informacjami, takimi jak userId, userName itp., są przechowywane w `aspnet_Users` tabeli. Informacje o uwierzytelnianiu, takie jak hasło, format hasła, sól hasła, liczniki i szczegóły blokady itp., są przechowywane w `aspnet_Membership` tabeli. Role składają się po prostu z nazw i unikatowych identyfikatorów, które są przypisane do użytkowników za pośrednictwem `aspnet_UsersInRoles` tabeli skojarzenia, zapewniając relację wiele-do-wielu.

Jeśli istniejący system korzysta z ról oprócz przynależności do członkostwa, należy przeprowadzić migrację kont użytkowników, skojarzonych haseł, ról i członkostwa w roli do ASP.NET Core tożsamość. Najprawdopodobniej trzeba będzie zaktualizować kod, w którym obecnie wykonywane są operacje sprawdzania ról przy użyciu instrukcji if, aby zamiast tego użyć filtrów deklaratywnych, atrybutów i/lub pomocników tagów. Na końcu tego rozdziału będziemy szczegółowo zapoznać się z zagadnieniami dotyczącymi migracji.

### <a name="authorization-configuration-in-web-forms"></a>Konfiguracja autoryzacji w formularzach sieci Web

Aby skonfigurować autoryzowany dostęp do niektórych stron w aplikacji ASP.NET Web Forms, zazwyczaj należy określić, że niektóre strony lub foldery są niedostępne dla użytkowników anonimowych. Ta konfiguracja jest wykonywana w pliku web.config:

```xml
<?xml version="1.0"?>
<configuration>
    <system.web>
      <authentication mode="Forms">
        <forms defaultUrl="~/home.aspx" loginUrl="~/login.aspx"
          slidingExpiration="true" timeout="2880"></forms>
      </authentication>

      <authorization>
        <deny users="?" />
      </authorization>
    </system.web>
</configuration>
```

`authentication`Sekcja konfiguracji konfiguruje uwierzytelnianie formularzy dla aplikacji. `authorization`Sekcja jest używana, aby uniemożliwić anonimowym użytkownikom całej aplikacji. Można jednak zapewnić bardziej szczegółowe reguły autoryzacji dla poszczególnych lokalizacji, a także stosować testy autoryzacji oparte na rolach.

```xml
<location path="login.aspx">
  <system.web>
    <authorization>
      <allow users="*" />
    </authorization>
  </system.web>
</location>
```

Powyższa konfiguracja, w połączeniu z pierwszym, zezwoli anonimowym użytkownikom na dostęp do strony logowania, zastępując ograniczenie dotyczące całej lokacji nieuwierzytelnionym użytkownikom.

```xml
<location path="/admin">
  <system.web>
    <authorization>
      <allow roles="Administrators" />
      <deny users="*" />
    </authorization>
  </system.web>
</location>
```

Powyższa konfiguracja, w połączeniu z innymi, ogranicza dostęp do `/admin` folderu i wszystkich znajdujących się w nim zasobów do członków roli "Administratorzy". To ograniczenie można również zastosować, umieszczając oddzielny `web.config` plik w `/admin` katalogu głównym folderu.

### <a name="authorization-code-in-web-forms"></a>Kod autoryzacji w formularzach sieci Web

Oprócz konfigurowania dostępu przy użyciu programu `web.config` można również programowo skonfigurować dostęp i zachowanie w aplikacji formularzy sieci Web. Na przykład można ograniczyć możliwość wykonywania określonych operacji lub wyświetlania określonych danych w oparciu o rolę użytkownika.

Ten kod może być używany zarówno w logice związanej z kodem, jak i na samej stronie:

```html
<% if (HttpContext.Current.User.IsInRole("Administrators")) { %>
  <a href="/admin">Go To Admin</a>
<% } %>
```

Oprócz sprawdzania przynależności do roli użytkownika można także określić, czy są one uwierzytelniane (często jest to lepiej wykonane przy użyciu konfiguracji opartej na lokalizacji powyżej). Poniżej znajduje się przykład tego podejścia.

```csharp
protected void Page_Load(object sender, EventArgs e)
{
    if (!User.Identity.IsAuthenticated)
    {
        FormsAuthentication.RedirectToLoginPage();
    }
    if (!Roles.IsUserInRole(User.Identity.Name, "Administrators"))
    {
        MessageLabel.Text = "Only administrators can view this.";
        SecretPanel.Visible = false;
    }
}
```

W powyższym kodzie kontrola dostępu oparta na rolach (RBAC) służy do określenia, czy pewne elementy strony, takie jak `SecretPanel` , są widoczne w oparciu o rolę bieżącego użytkownika.

Zazwyczaj aplikacje formularzy sieci Web ASP.NET konfigurują zabezpieczenia w `web.config` pliku, a następnie dodają dodatkowe sprawdzenia, w razie konieczności na `.aspx` stronach i związanych z nimi plikami związanymi z `.aspx.cs` kodem. Większość aplikacji korzysta z uniwersalnego dostawcy członkostwa, często z dodatkowym dostawcą roli.

## <a name="aspnet-core-identity"></a>ASP.NET Core tożsamość

Mimo że zadanie jest nadal wykonywane z uwierzytelnianiem i autoryzacją, ASP.NET Core tożsamość używa różnego zestawu streszczeń i założeń w porównaniu z dostawcami uniwersalnymi. Na przykład nowy model tożsamości obsługuje uwierzytelnianie innych firm, umożliwiając użytkownikom uwierzytelnianie przy użyciu konta mediów społecznościowych lub innego zaufanego dostawcy uwierzytelniania. ASP.NET Core Identity obsługuje interfejs użytkownika dla często wymaganych stron, takich jak logowanie, wylogowywanie i rejestrowanie. Wykorzystuje EF Core do uzyskiwania dostępu do danych i używa migracji EF Core w celu wygenerowania schematu niezbędnego do obsługi jego modelu danych. [Wprowadzenie do tożsamości na ASP.NET Core](/aspnet/core/security/authentication/identity) zawiera dobry przegląd informacji o tym, co jest dołączone do ASP.NET Core tożsamości i jak rozpocząć pracę z nim. Jeśli nie skonfigurowano jeszcze tożsamości ASP.NET Core w aplikacji i jej bazie danych, pomoże Ci rozpocząć pracę.

### <a name="roles-claims-and-policies"></a>Role, oświadczenia i zasady

Zarówno dostawcy Uniwersalni, jak i tożsamość ASP.NET Core obsługują koncepcję ról. Można tworzyć role dla użytkowników i przypisywać użytkowników do ról. Użytkownicy mogą należeć do dowolnej liczby ról i można zweryfikować członkostwo w roli w ramach implementacji autoryzacji.

Oprócz ról ASP.NET Core tożsamość obsługuje koncepcje oświadczeń i zasad. Mimo że rola powinna być zgodna z zestawem zasobów, użytkownik w tej roli powinien mieć dostęp do żądania, a po prostu jest częścią tożsamości użytkownika. Jest to para wartości Nazwa, która reprezentuje temat, a nie co może zrobić.

Można bezpośrednio sprawdzić oświadczenia użytkownika i określić na podstawie tych wartości, czy użytkownik powinien mieć dostęp do zasobu. Jednak takie sprawdzenia są często powtarzane i rozpraszane w całym systemie. Lepszym rozwiązaniem jest zdefiniowanie *zasad*.

Zasady autoryzacji składają się z co najmniej jednego wymagania. Zasady są rejestrowane w ramach konfiguracji usługi autoryzacji w `ConfigureServices` metodzie `Startup.cs` . Na przykład poniższy fragment kodu konfiguruje zasady o nazwie "CanadiansOnly", które mają wymaganie, aby użytkownik miał wartość "Kanada".

```csharp
services.AddAuthorization(options =>
{
    options.AddPolicy("CanadiansOnly", policy => policy.RequireClaim(ClaimTypes.Country, "Canada"));
});
```

Więcej informacji na [temat tworzenia zasad niestandardowych można znaleźć w dokumentacji](/aspnet/core/security/authorization/policies)programu.

Bez względu na to, czy korzystasz z zasad, czy ról, możesz określić, że określona Strona w Blazor aplikacji wymaga, aby dana rola lub zasady z `[Authorize]` atrybutem zostały zastosowane z `@attribute` dyrektywą.

Wymaganie roli:

```csharp
@attribute [Authorize(Roles ="administrators")]
```

Wymaganie spełnienia zasad:

```csharp
@attribute [Authorize(Policy ="CanadiansOnly")]
```

Jeśli potrzebujesz dostępu do stanu uwierzytelniania, ról lub oświadczeń użytkownika w kodzie, istnieją dwa podstawowe sposoby osiągnięcia tej funkcji. Pierwszym elementem jest otrzymanie stanu uwierzytelniania jako parametru kaskadowego. Drugim jest uzyskanie dostępu do stanu przy użyciu wstrzykiwanego `AuthenticationStateProvider` . Szczegóły każdego z tych metod zostały opisane w dokumentacji dotyczącej [ Blazor zabezpieczeń](/aspnet/core/blazor/security/).

Poniższy kod pokazuje, jak odebrać `AuthenticationState` jako parametr kaskadowy:

```csharp
[CascadingParameter]
private Task<AuthenticationState> authenticationStateTask { get; set; }
```

Gdy ten parametr jest używany, można uzyskać użytkownika przy użyciu tego kodu:

```csharp
var authState = await authenticationStateTask;
var user = authState.User;
```

Poniższy kod pokazuje, jak wstrzyknąć `AuthenticationStateProvider` :

```csharp
@using Microsoft.AspNetCore.Components.Authorization
@inject AuthenticationStateProvider AuthenticationStateProvider
```

Korzystając z dostawcy, możesz uzyskać dostęp do użytkownika przy użyciu następującego kodu:

```csharp
AuthenticationState authState = await AuthenticationStateProvider.GetAuthenticationStateAsync();
ClaimsPrincipal user = authState.User;

if (user.Identity.IsAuthenticated)
{
  // work with user.Claims and/or user.Roles
}
```

**Uwaga:** `AuthorizeView` Składnik omówiony w dalszej części tego rozdziału stanowi deklaratywny sposób sterowania tym, co użytkownik widzi na stronie lub w składniku.

Aby współpracować z użytkownikami i oświadczeniami (w Blazor aplikacjach serwerowych), może być również konieczne wstrzyknięcie `UserManager<T>` ( `IdentityUser` domyślne użycie), którego można użyć do wyliczania i modyfikowania oświadczeń dla użytkownika. Najpierw wstrzyknąć typ i przypisz go do właściwości:

```csharp
@inject UserManager<IdentityUser> MyUserManager
```

Następnie użyj jej do pracy z oświadczeniami użytkownika. Poniższy przykład przedstawia sposób dodawania i utrwalania roszczeń użytkownika:

```csharp
private async Task AddCountryClaim()
{
    var authState = await AuthenticationStateProvider.GetAuthenticationStateAsync();
    var user = authState.User;
    var identityUser = await MyUserManager.FindByNameAsync(user.Identity.Name);

    if (!user.HasClaim(c => c.Type == ClaimTypes.Country))
    {
        // stores the claim in the cookie
        ClaimsIdentity id = new ClaimsIdentity();
        id.AddClaim(new Claim(ClaimTypes.Country, "Canada"));
        user.AddIdentity(id);

        // save the claim in the database
        await MyUserManager.AddClaimAsync(identityUser, new Claim(ClaimTypes.Country, "Canada"));
    }
}
```

Jeśli musisz współpracować z rolami, postępuj zgodnie z tym samym podejściem. `RoleManager<T>`Aby wyświetlić same role i zarządzać nimi, może być konieczne wstrzyknięcie (użycie `IdentityRole` dla typu domyślnego).

**Uwaga:** W Blazor projektach Webassembly należy udostępnić interfejsy API serwera, aby wykonać te operacje (zamiast używać `UserManager<T>` lub `RoleManager<T>` bezpośrednio). BlazorAplikacja kliencka webassembly będzie zarządzać oświadczeniami i/lub rolami przez bezpieczne wywoływanie punktów końcowych interfejsu API uwidocznionych w tym celu.

### <a name="migration-guide"></a>Przewodnik migracji

Migracja z ASP.NET Web Forms i uniwersalnych dostawców do ASP.NET Core Identity wymaga kilku kroków:

1. Utwórz schemat bazy danych tożsamości ASP.NET Core w docelowej bazie danych
2. Migruj dane ze schematu uniwersalnego dostawcy do ASP.NET Core schematu tożsamości
3. Migruj konfigurację z programu `web.config` do oprogramowania pośredniczącego i usług, zazwyczaj w `Startup.cs`
4. Aktualizować poszczególne strony przy użyciu kontrolek i warunkowych, aby używać pomocników tagów i nowych interfejsów API tożsamości.

Wszystkie wymienione kroki zostały szczegółowo opisane poniżej.

### <a name="creating-the-aspnet-core-identity-schema"></a>Tworzenie schematu tożsamości ASP.NET Core

Istnieje kilka sposobów, aby utworzyć niezbędną strukturę tabeli służącą do ASP.NET Core tożsamości. Najprostszą jest utworzenie nowej aplikacji sieci Web ASP.NET Core. Wybierz pozycję aplikacja sieci Web, a następnie zmień uwierzytelnianie, aby korzystać z poszczególnych kont użytkowników.

![Nowy projekt z kontami poszczególnych użytkowników](./media/security/individual-user-accounts.png)

W wierszu polecenia można wykonać tę samą czynność, uruchamiając polecenie `dotnet new webapp -au Individual` . Po utworzeniu aplikacji uruchom ją i zarejestruj w witrynie. Należy wyzwolić stronę tak jak pokazano poniżej:

![Strona zastosowania migracji](./media/security/apply-migrations-page.png)

Kliknij przycisk "Zastosuj migracje", a następnie należy utworzyć niezbędne tabele baz danych. Ponadto pliki migracji powinny pojawić się w projekcie, jak pokazano poniżej:

![Pliki migracji](./media/security/migration-files.png)

Można uruchomić migrację samodzielnie, bez uruchamiania aplikacji sieci Web, za pomocą tego narzędzia wiersza polecenia:

```powershell
dotnet ef database update
```

Jeśli wolisz uruchomić skrypt w celu zastosowania nowego schematu do istniejącej bazy danych, możesz wykonać skrypty tych migracji z wiersza polecenia. Uruchom to polecenie, aby wygenerować skrypt:

```powershell
dotnet ef migrations script -o auth.sql
```

Powyższe polecenie spowoduje utworzenie w pliku wyjściowym skryptu SQL `auth.sql` , który można następnie uruchomić dla dowolnej bazy danych, której chcesz użyć. Jeśli masz problemy z uruchamianiem `dotnet ef` poleceń, [upewnij się, że masz narzędzia EF Core zainstalowane w systemie](/ef/core/miscellaneous/cli/dotnet).

W przypadku, gdy w tabeli źródłowej znajdują się dodatkowe kolumny, należy zidentyfikować najlepszą lokalizację dla tych kolumn w nowym schemacie. Na ogół kolumny Znalezione w `aspnet_Membership` tabeli powinny być mapowane na `AspNetUsers` tabelę. Kolumny na `aspnet_Roles` powinny być mapowane na `AspNetRoles` . Wszystkie dodatkowe kolumny w `aspnet_UsersInRoles` tabeli zostaną dodane do `AspNetUserRoles` tabeli.

Warto również rozważać wprowadzanie wszelkich dodatkowych kolumn w oddzielnych tabelach. Tak więc przyszłe migracje nie muszą uwzględniać takich dostosowań domyślnego schematu tożsamości.

### <a name="migrating-data-from-universal-providers-to-aspnet-core-identity"></a>Migrowanie danych od dostawców uniwersalnych do ASP.NET Core Identity

Gdy masz docelowy schemat tabeli, następnym krokiem jest Migrowanie rekordów użytkownika i roli do nowego schematu. Pełna lista różnic między schematami, w tym te, które kolumny są mapowane na nowe kolumny, można znaleźć [tutaj](/aspnet/core/migration/proper-to-2x/membership-to-core-identity).

Aby przeprowadzić migrację użytkowników z członkostwa do nowych tabel tożsamości, należy [wykonać kroki opisane w dokumentacji](/aspnet/core/migration/proper-to-2x/membership-to-core-identity). Po wykonaniu tych kroków i podanego skryptu użytkownicy będą musieli zmienić hasło przy następnym logowaniu.

Możliwe jest Migrowanie haseł użytkowników, ale proces jest znacznie bardziej powiązany. Wymaganie od użytkowników aktualizowania haseł w ramach procesu migracji i zachęcania ich do korzystania z nowych, unikatowych haseł może wzmocnić ogólne zabezpieczenia aplikacji.

### <a name="migrating-security-settings-from-webconfig-to-startupcs"></a>Migrowanie ustawień zabezpieczeń z web.config do Startup.cs

Jak wspomniano powyżej, ASP.NET członkostwa i dostawcy ról są konfigurowane w pliku aplikacji `web.config` . Ponieważ ASP.NET Core aplikacje nie są powiązane z usługami IIS i używają osobnego systemu do konfiguracji, te ustawienia muszą być skonfigurowane w innym miejscu. W większości przypadków ASP.NET Core tożsamość jest konfigurowana w `Startup.cs` pliku. Otwórz projekt sieci Web, który został utworzony wcześniej (aby wygenerować schemat tabeli tożsamości) i przejrzyj jego `Startup.cs` plik.

Domyślna metoda ConfigureServices dodaje obsługę EF Core i tożsamości:

```csharp
// This method gets called by the runtime. Use this method to add services to the container.
public void ConfigureServices(IServiceCollection services)
{
    services.AddDbContext<ApplicationDbContext>(options =>
        options.UseSqlServer(
            Configuration.GetConnectionString("DefaultConnection")));

    services.AddDefaultIdentity<IdentityUser>(options => options.SignIn.RequireConfirmedAccount = true)
        .AddEntityFrameworkStores<ApplicationDbContext>();

    services.AddRazorPages();
}
```

`AddDefaultIdentity`Metoda rozszerzenia służy do konfigurowania tożsamości do używania domyślnego `ApplicationDbContext` i `IdentityUser` typu struktury. Jeśli używasz niestandardowego `IdentityUser` , pamiętaj o określeniu jego typu w tym miejscu. Jeśli te metody rozszerzające nie działają w aplikacji, sprawdź, czy masz odpowiednie instrukcje using i czy masz wymagane odwołania do pakietu NuGet. Na przykład projekt powinien mieć pewną wersję `Microsoft.AspNetCore.Identity.EntityFrameworkCore` pakietów i, `Microsoft.AspNetCore.Identity.UI` do których się odwołuje.

Ponadto `Startup.cs` należy zobaczyć wymagane oprogramowanie pośredniczące skonfigurowane dla danej lokacji. `UseAuthentication`I `UseAuthorization` należy je skonfigurować i w odpowiedniej lokalizacji.

```csharp

// This method gets called by the runtime. Use this method to configure the HTTP request pipeline.
public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
{
    if (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
        app.UseDatabaseErrorPage();
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

    app.UseAuthentication();
    app.UseAuthorization();

    app.UseEndpoints(endpoints =>
    {
        endpoints.MapRazorPages();
    });
}
```

ASP.NET Identity nie konfiguruje dostępu anonimowego lub opartego na rolach do lokalizacji z programu `Startup.cs` . Należy przeprowadzić migrację danych konfiguracji autoryzacji specyficznych dla lokalizacji do filtrów w ASP.NET Core. Zanotuj, które foldery i strony będą wymagały takich aktualizacji. Te zmiany zostaną wprowadzone w następnej sekcji.

### <a name="updating-individual-pages-to-use-aspnet-core-identity-abstractions"></a>Aktualizowanie poszczególnych stron do użycia w ASP.NET Core Abstracts Identity

W aplikacji formularze sieci Web ASP.NET, jeśli masz `web.config` Ustawienia, aby odmówić dostępu do określonych stron lub folderów użytkownikom anonimowym, należy zmigrować te zmiany, dodając `[Authorize]` atrybut do takich stron:

```razor
@attribute [Authorize]
```

Jeśli chcesz jeszcze odmówić dostępu z wyjątkiem tych użytkowników należących do określonej roli, Przeprowadź migrację tego zachowania, dodając atrybut określający rolę:

```razor
@attribute [Authorize(Roles ="administrators")]
```

Ten `[Authorize]` atrybut działa tylko na `@page` składnikach, które są osiągalne za pośrednictwem Blazor routera. Ten atrybut nie działa ze składnikami podrzędnymi, które należy zamiast tego używać `AuthorizeView` .

Jeśli masz logikę w ramach znaczników strony, aby określić, czy ma być wyświetlany jakiś kod dla określonego użytkownika, możesz zastąpić ten `AuthorizeView` składnik. [Składnik AuthorizeView](/aspnet/core/blazor/security#authorizeview-component) selektywnie wyświetla interfejs użytkownika w zależności od tego, czy użytkownik jest uprawniony do jego wyświetlania. Udostępnia również `context` zmienną, której można użyć w celu uzyskania dostępu do informacji o użytkowniku.

```razor
<AuthorizeView>
    <Authorized>
        <h1>Hello, @context.User.Identity.Name!</h1>
        <p>You can only see this content if you are authenticated.</p>
    </Authorized>
    <NotAuthorized>
        <h1>Authentication Failure!</h1>
        <p>You are not signed in.</p>
    </NotAuthorized>
</AuthorizeView>
```

Możesz uzyskać dostęp do stanu uwierzytelniania w ramach logiki proceduralnej, uzyskując dostęp do użytkownika ze `Task<AuthenticationState` skonfigurowanego za pomocą `[CascadingParameter]` atrybutu. Ta konfiguracja umożliwi użytkownikowi dostęp do użytkownika, który może określić, czy są uwierzytelniani i czy należą do określonej roli. Jeśli konieczne jest ocenę zasad proceduralnych, można wstrzyknąć wystąpienie obiektu `IAuthorizationService` i wywołać `AuthorizeAsync` metodę. Następujący przykładowy kod demonstruje, jak uzyskać informacje o użytkowniku i zezwolić autoryzowanemu użytkownikowi na wykonanie zadania ograniczonego przez `content-editor` zasady.

```razor
@using Microsoft.AspNetCore.Authorization
@inject IAuthorizationService AuthorizationService

<button @onclick="@DoSomething">Do something important</button>

@code {
    [CascadingParameter]
    private Task<AuthenticationState> authenticationStateTask { get; set; }

    private async Task DoSomething()
    {
        var user = (await authenticationStateTask).User;

        if (user.Identity.IsAuthenticated)
        {
            // Perform an action only available to authenticated (signed-in) users.
        }

        if (user.IsInRole("admin"))
        {
            // Perform an action only available to users in the 'admin' role.
        }

        if ((await AuthorizationService.AuthorizeAsync(user, "content-editor"))
            .Succeeded)
        {
            // Perform an action only available to users satisfying the
            // 'content-editor' policy.
        }
    }
}
```

`AuthenticationState`Najpierw należy skonfigurować jako wartość kaskadową, zanim będzie można powiązać ją z parametrem kaskadowym podobnym do tego. Zwykle jest to wykonywane przy użyciu `CascadingAuthenticationState` składnika. Ta konfiguracja jest zazwyczaj wykonywana w `App.razor` :

```razor
<CascadingAuthenticationState>
    <Router AppAssembly="@typeof(Program).Assembly">
        <Found Context="routeData">
            <AuthorizeRouteView RouteData="@routeData"
                DefaultLayout="@typeof(MainLayout)" />
        </Found>
        <NotFound>
            <LayoutView Layout="@typeof(MainLayout)">
                <p>Sorry, there's nothing at this address.</p>
            </LayoutView>
        </NotFound>
    </Router>
</CascadingAuthenticationState>
```

## <a name="summary"></a>Podsumowanie

Blazor używa tego samego modelu zabezpieczeń co ASP.NET Core, który jest ASP.NET Core tożsamością. Migracja z uniwersalnych dostawców do ASP.NET Core tożsamość jest stosunkowo prosta, przy założeniu, że nie zbyt dużo dostosowania zostało zastosowane do oryginalnego schematu danych. Po przeprowadzeniu migracji danych Praca z uwierzytelnianiem i autoryzacją w Blazor aplikacjach jest dobrze udokumentowana, z możliwością konfiguracji oraz obsługą techniczną w przypadku większości wymagań dotyczących zabezpieczeń.

## <a name="references"></a>Odwołania

- [Wprowadzenie do tożsamości na ASP.NET Core](/aspnet/core/security/authentication/identity)
- [Migrowanie z uwierzytelniania członkostwa ASP.NET do tożsamości ASP.NET Core 2,0](/aspnet/core/migration/proper-to-2x/membership-to-core-identity)
- [Migrowanie uwierzytelniania i tożsamości do ASP.NET Core](/aspnet/core/migration/identity)
- [ASP.NET Core Blazor uwierzytelnianie i autoryzacja](/aspnet/core/blazor/security/)

>[!div class="step-by-step"]
>[Poprzedni](config.md) 
> [Dalej](migration.md)
