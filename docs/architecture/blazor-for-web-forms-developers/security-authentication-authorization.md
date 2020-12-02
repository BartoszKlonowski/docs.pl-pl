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
# <a name="security-authentication-and-authorization-in-aspnet-web-forms-and-no-locblazor"></a><span data-ttu-id="7abdf-103">Zabezpieczenia: uwierzytelnianie i autoryzacja w ASP.NET Web Forms i Blazor</span><span class="sxs-lookup"><span data-stu-id="7abdf-103">Security: Authentication and Authorization in ASP.NET Web Forms and Blazor</span></span>

<span data-ttu-id="7abdf-104">Migrowanie z aplikacji ASP.NET Web Forms do programu Blazor niemal z pewnością wymaga aktualizacji sposobu uwierzytelniania i autoryzacji, przy założeniu, że aplikacja ma skonfigurowane uwierzytelnianie.</span><span class="sxs-lookup"><span data-stu-id="7abdf-104">Migrating from an ASP.NET Web Forms application to Blazor will almost certainly require updating how authentication and authorization are performed, assuming the application had authentication configured.</span></span> <span data-ttu-id="7abdf-105">W tym rozdziale zawarto informacje na temat migracji z modelu uniwersalnego dostawcy formularzy sieci Web ASP.NET (dla członkostwa, ról i profilów użytkowników) oraz sposobu pracy z tożsamością ASP.NET Core z Blazor aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7abdf-105">This chapter will cover how to migrate from the ASP.NET Web Forms universal provider model (for membership, roles, and user profiles) and how to work with ASP.NET Core Identity from Blazor apps.</span></span> <span data-ttu-id="7abdf-106">Ten rozdział będzie obejmować ogólne kroki i zagadnienia, ale szczegółowe instrukcje i skrypty można znaleźć w dokumentacji, do której się odwołuje.</span><span class="sxs-lookup"><span data-stu-id="7abdf-106">While this chapter will cover the high-level steps and considerations, the detailed steps and scripts may be found in the referenced documentation.</span></span>

## <a name="aspnet-universal-providers"></a><span data-ttu-id="7abdf-107">ASP.NET dostawcy uniwersalnego</span><span class="sxs-lookup"><span data-stu-id="7abdf-107">ASP.NET universal providers</span></span>

<span data-ttu-id="7abdf-108">Od ASP.NET 2,0 platforma formularzy sieci Web ASP.NET obsługuje model dostawcy dla różnych funkcji, w tym do członkostwa.</span><span class="sxs-lookup"><span data-stu-id="7abdf-108">Since ASP.NET 2.0, the ASP.NET Web Forms platform has supported a provider model for a variety of features, including membership.</span></span> <span data-ttu-id="7abdf-109">Uniwersalny dostawca członkostwa wraz z opcjonalnym dostawcą roli jest często wdrażany przy użyciu aplikacji formularzy sieci Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="7abdf-109">The universal membership provider, along with the optional role provider, is commonly deployed with ASP.NET Web Forms applications.</span></span> <span data-ttu-id="7abdf-110">Oferuje ona niezawodny i bezpieczny sposób zarządzania uwierzytelnianiem i autoryzacją, które w dalszym ciągu działają prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="7abdf-110">It offers a robust and secure way to manage authentication and authorization that continues to work well today.</span></span> <span data-ttu-id="7abdf-111">Najnowsza oferta tych dostawców uniwersalnych jest dostępna jako pakiet NuGet, [Microsoft. ASPNET. Providers](https://www.nuget.org/packages/Microsoft.AspNet.Providers).</span><span class="sxs-lookup"><span data-stu-id="7abdf-111">The most recent offering of these universal providers is available as a NuGet package, [Microsoft.AspNet.Providers](https://www.nuget.org/packages/Microsoft.AspNet.Providers).</span></span>

<span data-ttu-id="7abdf-112">Dostawcy Uniwersalni pracują ze schematem bazy danych SQL, który zawiera tabele takie jak `aspnet_Applications` ,, `aspnet_Membership` `aspnet_Roles` i `aspnet_Users` .</span><span class="sxs-lookup"><span data-stu-id="7abdf-112">The Universal Providers work with a SQL database schema that includes tables like `aspnet_Applications`, `aspnet_Membership`, `aspnet_Roles`, and `aspnet_Users`.</span></span> <span data-ttu-id="7abdf-113">Po skonfigurowaniu [ poleceniaaspnet_regsql.exe](/previous-versions/ms229862(v=vs.140))dostawcy instalują tabele i procedury składowane, które zawierają wszystkie niezbędne zapytania i polecenia do pracy z danymi źródłowymi.</span><span class="sxs-lookup"><span data-stu-id="7abdf-113">When configured by running the [aspnet_regsql.exe command](/previous-versions/ms229862(v=vs.140)), the providers install tables and stored procedures that provide all of the necessary queries and commands to work with the underlying data.</span></span> <span data-ttu-id="7abdf-114">Schemat bazy danych i te procedury składowane nie są zgodne z nowszymi ASP.NET Identity i ASP.NET Core systemami tożsamości, dlatego istniejące dane muszą zostać zmigrowane do nowego systemu.</span><span class="sxs-lookup"><span data-stu-id="7abdf-114">The database schema and these stored procedures are not compatible with newer ASP.NET Identity and ASP.NET Core Identity systems, so existing data must be migrated into the new system.</span></span> <span data-ttu-id="7abdf-115">Rysunek 1 przedstawia przykładowy schemat tabeli skonfigurowany dla dostawców uniwersalnych.</span><span class="sxs-lookup"><span data-stu-id="7abdf-115">Figure 1 shows an example table schema configured for universal providers.</span></span>

![Schemat dostawców uniwersalnych](./media/security/membership-tables.png)

<span data-ttu-id="7abdf-117">Dostawca uniwersalny obsługuje użytkowników, członkostwo, role i profile.</span><span class="sxs-lookup"><span data-stu-id="7abdf-117">The universal provider handles users, membership, roles, and profiles.</span></span> <span data-ttu-id="7abdf-118">Użytkownicy są przypisani globalnie unikatowymi identyfikatorami i podstawowymi informacjami, takimi jak userId, userName itp., są przechowywane w `aspnet_Users` tabeli.</span><span class="sxs-lookup"><span data-stu-id="7abdf-118">Users are assigned globally unique identifiers and basic information like userId, userName etc. are stored in the `aspnet_Users` table.</span></span> <span data-ttu-id="7abdf-119">Informacje o uwierzytelnianiu, takie jak hasło, format hasła, sól hasła, liczniki i szczegóły blokady itp., są przechowywane w `aspnet_Membership` tabeli.</span><span class="sxs-lookup"><span data-stu-id="7abdf-119">Authentication information, such as password, password format, password salt, lockout counters and details, etc. are stored in the `aspnet_Membership` table.</span></span> <span data-ttu-id="7abdf-120">Role składają się po prostu z nazw i unikatowych identyfikatorów, które są przypisane do użytkowników za pośrednictwem `aspnet_UsersInRoles` tabeli skojarzenia, zapewniając relację wiele-do-wielu.</span><span class="sxs-lookup"><span data-stu-id="7abdf-120">Roles consist simply of names and unique identifiers, which are assigned to users via the `aspnet_UsersInRoles` association table, providing a many-to-many relationship.</span></span>

<span data-ttu-id="7abdf-121">Jeśli istniejący system korzysta z ról oprócz przynależności do członkostwa, należy przeprowadzić migrację kont użytkowników, skojarzonych haseł, ról i członkostwa w roli do ASP.NET Core tożsamość.</span><span class="sxs-lookup"><span data-stu-id="7abdf-121">If your existing system is using roles in addition to membership, you will need to migrate the user accounts, the associated passwords, the roles, and the role membership into ASP.NET Core Identity.</span></span> <span data-ttu-id="7abdf-122">Najprawdopodobniej trzeba będzie zaktualizować kod, w którym obecnie wykonywane są operacje sprawdzania ról przy użyciu instrukcji if, aby zamiast tego użyć filtrów deklaratywnych, atrybutów i/lub pomocników tagów.</span><span class="sxs-lookup"><span data-stu-id="7abdf-122">You will also most likely need to update your code where you're currently performing role checks using if statements to instead leverage declarative filters, attributes, and/or tag helpers.</span></span> <span data-ttu-id="7abdf-123">Na końcu tego rozdziału będziemy szczegółowo zapoznać się z zagadnieniami dotyczącymi migracji.</span><span class="sxs-lookup"><span data-stu-id="7abdf-123">We will review migration considerations in greater detail at the end of this chapter.</span></span>

### <a name="authorization-configuration-in-web-forms"></a><span data-ttu-id="7abdf-124">Konfiguracja autoryzacji w formularzach sieci Web</span><span class="sxs-lookup"><span data-stu-id="7abdf-124">Authorization configuration in Web Forms</span></span>

<span data-ttu-id="7abdf-125">Aby skonfigurować autoryzowany dostęp do niektórych stron w aplikacji ASP.NET Web Forms, zazwyczaj należy określić, że niektóre strony lub foldery są niedostępne dla użytkowników anonimowych.</span><span class="sxs-lookup"><span data-stu-id="7abdf-125">To configure authorized access to certain pages in an ASP.NET Web Forms application, typically you specify that certain pages or folders are inaccessible to anonymous users.</span></span> <span data-ttu-id="7abdf-126">Ta konfiguracja jest wykonywana w pliku web.config:</span><span class="sxs-lookup"><span data-stu-id="7abdf-126">This configuration is done in the web.config file:</span></span>

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

<span data-ttu-id="7abdf-127">`authentication`Sekcja konfiguracji konfiguruje uwierzytelnianie formularzy dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7abdf-127">The `authentication` configuration section sets up the forms authentication for the application.</span></span> <span data-ttu-id="7abdf-128">`authorization`Sekcja jest używana, aby uniemożliwić anonimowym użytkownikom całej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7abdf-128">The `authorization` section is used to disallow anonymous users for the entire application.</span></span> <span data-ttu-id="7abdf-129">Można jednak zapewnić bardziej szczegółowe reguły autoryzacji dla poszczególnych lokalizacji, a także stosować testy autoryzacji oparte na rolach.</span><span class="sxs-lookup"><span data-stu-id="7abdf-129">However, you can provide more granular authorization rules on a per-location basis as well as apply role-based authorization checks.</span></span>

```xml
<location path="login.aspx">
  <system.web>
    <authorization>
      <allow users="*" />
    </authorization>
  </system.web>
</location>
```

<span data-ttu-id="7abdf-130">Powyższa konfiguracja, w połączeniu z pierwszym, zezwoli anonimowym użytkownikom na dostęp do strony logowania, zastępując ograniczenie dotyczące całej lokacji nieuwierzytelnionym użytkownikom.</span><span class="sxs-lookup"><span data-stu-id="7abdf-130">The above configuration, when combined with the first one, would allow anonymous users to access the login page, overriding the site-wide restriction on non-authenticated users.</span></span>

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

<span data-ttu-id="7abdf-131">Powyższa konfiguracja, w połączeniu z innymi, ogranicza dostęp do `/admin` folderu i wszystkich znajdujących się w nim zasobów do członków roli "Administratorzy".</span><span class="sxs-lookup"><span data-stu-id="7abdf-131">The above configuration, when combined with the others, restricts access to the `/admin` folder and all resources within it to members of the "Administrators" role.</span></span> <span data-ttu-id="7abdf-132">To ograniczenie można również zastosować, umieszczając oddzielny `web.config` plik w `/admin` katalogu głównym folderu.</span><span class="sxs-lookup"><span data-stu-id="7abdf-132">This restriction could also be applied by placing a separate `web.config` file within the `/admin` folder root.</span></span>

### <a name="authorization-code-in-web-forms"></a><span data-ttu-id="7abdf-133">Kod autoryzacji w formularzach sieci Web</span><span class="sxs-lookup"><span data-stu-id="7abdf-133">Authorization code in Web Forms</span></span>

<span data-ttu-id="7abdf-134">Oprócz konfigurowania dostępu przy użyciu programu `web.config` można również programowo skonfigurować dostęp i zachowanie w aplikacji formularzy sieci Web.</span><span class="sxs-lookup"><span data-stu-id="7abdf-134">In addition to configuring access using `web.config`, you can also programmatically configure access and behavior in your Web Forms application.</span></span> <span data-ttu-id="7abdf-135">Na przykład można ograniczyć możliwość wykonywania określonych operacji lub wyświetlania określonych danych w oparciu o rolę użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7abdf-135">For instance, you can restrict the ability to perform certain operations or view certain data based on the user's role.</span></span>

<span data-ttu-id="7abdf-136">Ten kod może być używany zarówno w logice związanej z kodem, jak i na samej stronie:</span><span class="sxs-lookup"><span data-stu-id="7abdf-136">This code can be used both in code-behind logic as well as in the page itself:</span></span>

```html
<% if (HttpContext.Current.User.IsInRole("Administrators")) { %>
  <a href="/admin">Go To Admin</a>
<% } %>
```

<span data-ttu-id="7abdf-137">Oprócz sprawdzania przynależności do roli użytkownika można także określić, czy są one uwierzytelniane (często jest to lepiej wykonane przy użyciu konfiguracji opartej na lokalizacji powyżej).</span><span class="sxs-lookup"><span data-stu-id="7abdf-137">In addition to checking user role membership, you can also determine if they are authenticated (though often this is better done using the location-based configuration covered above).</span></span> <span data-ttu-id="7abdf-138">Poniżej znajduje się przykład tego podejścia.</span><span class="sxs-lookup"><span data-stu-id="7abdf-138">Below is an example of this approach.</span></span>

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

<span data-ttu-id="7abdf-139">W powyższym kodzie kontrola dostępu oparta na rolach (RBAC) służy do określenia, czy pewne elementy strony, takie jak `SecretPanel` , są widoczne w oparciu o rolę bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7abdf-139">In the code above, role-based access control (RBAC) is used to determine whether certain elements of the page, such as a `SecretPanel`, are visible based on the current user's role.</span></span>

<span data-ttu-id="7abdf-140">Zazwyczaj aplikacje formularzy sieci Web ASP.NET konfigurują zabezpieczenia w `web.config` pliku, a następnie dodają dodatkowe sprawdzenia, w razie konieczności na `.aspx` stronach i związanych z nimi plikami związanymi z `.aspx.cs` kodem.</span><span class="sxs-lookup"><span data-stu-id="7abdf-140">Typically, ASP.NET Web Forms applications configure security within the `web.config` file and then add additional checks where needed in `.aspx` pages and their related `.aspx.cs` code-behind files.</span></span> <span data-ttu-id="7abdf-141">Większość aplikacji korzysta z uniwersalnego dostawcy członkostwa, często z dodatkowym dostawcą roli.</span><span class="sxs-lookup"><span data-stu-id="7abdf-141">Most applications leverage the universal membership provider, frequently with the additional role provider.</span></span>

## <a name="aspnet-core-identity"></a><span data-ttu-id="7abdf-142">ASP.NET Core tożsamość</span><span class="sxs-lookup"><span data-stu-id="7abdf-142">ASP.NET Core Identity</span></span>

<span data-ttu-id="7abdf-143">Mimo że zadanie jest nadal wykonywane z uwierzytelnianiem i autoryzacją, ASP.NET Core tożsamość używa różnego zestawu streszczeń i założeń w porównaniu z dostawcami uniwersalnymi.</span><span class="sxs-lookup"><span data-stu-id="7abdf-143">Although still tasked with authentication and authorization, ASP.NET Core Identity uses a different set of abstractions and assumptions when compared to the universal providers.</span></span> <span data-ttu-id="7abdf-144">Na przykład nowy model tożsamości obsługuje uwierzytelnianie innych firm, umożliwiając użytkownikom uwierzytelnianie przy użyciu konta mediów społecznościowych lub innego zaufanego dostawcy uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="7abdf-144">For example, the new Identity model supports third party authentication, allowing users to authenticate using a social media account or other trusted authentication provider.</span></span> <span data-ttu-id="7abdf-145">ASP.NET Core Identity obsługuje interfejs użytkownika dla często wymaganych stron, takich jak logowanie, wylogowywanie i rejestrowanie.</span><span class="sxs-lookup"><span data-stu-id="7abdf-145">ASP.NET Core Identity supports UI for commonly needed pages like login, logout, and register.</span></span> <span data-ttu-id="7abdf-146">Wykorzystuje EF Core do uzyskiwania dostępu do danych i używa migracji EF Core w celu wygenerowania schematu niezbędnego do obsługi jego modelu danych.</span><span class="sxs-lookup"><span data-stu-id="7abdf-146">It leverages EF Core for its data access, and uses EF Core migrations to generate the necessary schema required to support its data model.</span></span> <span data-ttu-id="7abdf-147">[Wprowadzenie do tożsamości na ASP.NET Core](/aspnet/core/security/authentication/identity) zawiera dobry przegląd informacji o tym, co jest dołączone do ASP.NET Core tożsamości i jak rozpocząć pracę z nim.</span><span class="sxs-lookup"><span data-stu-id="7abdf-147">This [introduction to Identity on ASP.NET Core](/aspnet/core/security/authentication/identity) provides a good overview of what is included with ASP.NET Core Identity and how to get started working with it.</span></span> <span data-ttu-id="7abdf-148">Jeśli nie skonfigurowano jeszcze tożsamości ASP.NET Core w aplikacji i jej bazie danych, pomoże Ci rozpocząć pracę.</span><span class="sxs-lookup"><span data-stu-id="7abdf-148">If you haven't already set up ASP.NET Core Identity in your application and its database, it will help you get started.</span></span>

### <a name="roles-claims-and-policies"></a><span data-ttu-id="7abdf-149">Role, oświadczenia i zasady</span><span class="sxs-lookup"><span data-stu-id="7abdf-149">Roles, claims, and policies</span></span>

<span data-ttu-id="7abdf-150">Zarówno dostawcy Uniwersalni, jak i tożsamość ASP.NET Core obsługują koncepcję ról.</span><span class="sxs-lookup"><span data-stu-id="7abdf-150">Both the universal providers and ASP.NET Core Identity support the concept of roles.</span></span> <span data-ttu-id="7abdf-151">Można tworzyć role dla użytkowników i przypisywać użytkowników do ról.</span><span class="sxs-lookup"><span data-stu-id="7abdf-151">You can create roles for users and assign users to roles.</span></span> <span data-ttu-id="7abdf-152">Użytkownicy mogą należeć do dowolnej liczby ról i można zweryfikować członkostwo w roli w ramach implementacji autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="7abdf-152">Users can belong to any number of roles, and you can verify role membership as part of your authorization implementation.</span></span>

<span data-ttu-id="7abdf-153">Oprócz ról ASP.NET Core tożsamość obsługuje koncepcje oświadczeń i zasad.</span><span class="sxs-lookup"><span data-stu-id="7abdf-153">In addition to roles, ASP.NET Core identity supports the concepts of claims and policies.</span></span> <span data-ttu-id="7abdf-154">Mimo że rola powinna być zgodna z zestawem zasobów, użytkownik w tej roli powinien mieć dostęp do żądania, a po prostu jest częścią tożsamości użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7abdf-154">While a role should specifically correspond to a set of resources a user in that role should be able to access, a claim is simply part of a user's identity.</span></span> <span data-ttu-id="7abdf-155">Jest to para wartości Nazwa, która reprezentuje temat, a nie co może zrobić.</span><span class="sxs-lookup"><span data-stu-id="7abdf-155">A claim is a name value pair that represents what the subject is, not what the subject can do.</span></span>

<span data-ttu-id="7abdf-156">Można bezpośrednio sprawdzić oświadczenia użytkownika i określić na podstawie tych wartości, czy użytkownik powinien mieć dostęp do zasobu.</span><span class="sxs-lookup"><span data-stu-id="7abdf-156">It is possible to directly inspect a user's claims and determine based on these values whether a user should be given access to a resource.</span></span> <span data-ttu-id="7abdf-157">Jednak takie sprawdzenia są często powtarzane i rozpraszane w całym systemie.</span><span class="sxs-lookup"><span data-stu-id="7abdf-157">However, such checks are often repetitive and scattered throughout the system.</span></span> <span data-ttu-id="7abdf-158">Lepszym rozwiązaniem jest zdefiniowanie *zasad*.</span><span class="sxs-lookup"><span data-stu-id="7abdf-158">A better approach is to define a *policy*.</span></span>

<span data-ttu-id="7abdf-159">Zasady autoryzacji składają się z co najmniej jednego wymagania.</span><span class="sxs-lookup"><span data-stu-id="7abdf-159">An authorization policy consists of one or more requirements.</span></span> <span data-ttu-id="7abdf-160">Zasady są rejestrowane w ramach konfiguracji usługi autoryzacji w `ConfigureServices` metodzie `Startup.cs` .</span><span class="sxs-lookup"><span data-stu-id="7abdf-160">Policies are registered as part of the authorization service configuration in the `ConfigureServices` method of `Startup.cs`.</span></span> <span data-ttu-id="7abdf-161">Na przykład poniższy fragment kodu konfiguruje zasady o nazwie "CanadiansOnly", które mają wymaganie, aby użytkownik miał wartość "Kanada".</span><span class="sxs-lookup"><span data-stu-id="7abdf-161">For example, the following code snippet configures a policy called "CanadiansOnly", which has the requirement that the user has the Country claim with the value of "Canada".</span></span>

```csharp
services.AddAuthorization(options =>
{
    options.AddPolicy("CanadiansOnly", policy => policy.RequireClaim(ClaimTypes.Country, "Canada"));
});
```

<span data-ttu-id="7abdf-162">Więcej informacji na [temat tworzenia zasad niestandardowych można znaleźć w dokumentacji](/aspnet/core/security/authorization/policies)programu.</span><span class="sxs-lookup"><span data-stu-id="7abdf-162">You can [learn more about how to create custom policies in the documentation](/aspnet/core/security/authorization/policies).</span></span>

<span data-ttu-id="7abdf-163">Bez względu na to, czy korzystasz z zasad, czy ról, możesz określić, że określona Strona w Blazor aplikacji wymaga, aby dana rola lub zasady z `[Authorize]` atrybutem zostały zastosowane z `@attribute` dyrektywą.</span><span class="sxs-lookup"><span data-stu-id="7abdf-163">Whether you're using policies or roles, you can specify that a particular page in your Blazor application requires that role or policy with the `[Authorize]` attribute, applied with the `@attribute` directive.</span></span>

<span data-ttu-id="7abdf-164">Wymaganie roli:</span><span class="sxs-lookup"><span data-stu-id="7abdf-164">Requiring a role:</span></span>

```csharp
@attribute [Authorize(Roles ="administrators")]
```

<span data-ttu-id="7abdf-165">Wymaganie spełnienia zasad:</span><span class="sxs-lookup"><span data-stu-id="7abdf-165">Requiring a policy be satisfied:</span></span>

```csharp
@attribute [Authorize(Policy ="CanadiansOnly")]
```

<span data-ttu-id="7abdf-166">Jeśli potrzebujesz dostępu do stanu uwierzytelniania, ról lub oświadczeń użytkownika w kodzie, istnieją dwa podstawowe sposoby osiągnięcia tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="7abdf-166">If you need access to a user's authentication state, roles, or claims in your code, there are two primary ways to achieve this functionality.</span></span> <span data-ttu-id="7abdf-167">Pierwszym elementem jest otrzymanie stanu uwierzytelniania jako parametru kaskadowego.</span><span class="sxs-lookup"><span data-stu-id="7abdf-167">The first is to receive the authentication state as a cascading parameter.</span></span> <span data-ttu-id="7abdf-168">Drugim jest uzyskanie dostępu do stanu przy użyciu wstrzykiwanego `AuthenticationStateProvider` .</span><span class="sxs-lookup"><span data-stu-id="7abdf-168">The second is to access the state using an injected `AuthenticationStateProvider`.</span></span> <span data-ttu-id="7abdf-169">Szczegóły każdego z tych metod zostały opisane w dokumentacji dotyczącej [ Blazor zabezpieczeń](/aspnet/core/blazor/security/).</span><span class="sxs-lookup"><span data-stu-id="7abdf-169">The details of each of these approaches are described in the [Blazor Security documentation](/aspnet/core/blazor/security/).</span></span>

<span data-ttu-id="7abdf-170">Poniższy kod pokazuje, jak odebrać `AuthenticationState` jako parametr kaskadowy:</span><span class="sxs-lookup"><span data-stu-id="7abdf-170">The following code shows how to receive the `AuthenticationState` as a cascading parameter:</span></span>

```csharp
[CascadingParameter]
private Task<AuthenticationState> authenticationStateTask { get; set; }
```

<span data-ttu-id="7abdf-171">Gdy ten parametr jest używany, można uzyskać użytkownika przy użyciu tego kodu:</span><span class="sxs-lookup"><span data-stu-id="7abdf-171">With this parameter in place, you can get the user using this code:</span></span>

```csharp
var authState = await authenticationStateTask;
var user = authState.User;
```

<span data-ttu-id="7abdf-172">Poniższy kod pokazuje, jak wstrzyknąć `AuthenticationStateProvider` :</span><span class="sxs-lookup"><span data-stu-id="7abdf-172">The following code shows how to inject the `AuthenticationStateProvider`:</span></span>

```csharp
@using Microsoft.AspNetCore.Components.Authorization
@inject AuthenticationStateProvider AuthenticationStateProvider
```

<span data-ttu-id="7abdf-173">Korzystając z dostawcy, możesz uzyskać dostęp do użytkownika przy użyciu następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="7abdf-173">With the provider in place, you can gain access to the user with the following code:</span></span>

```csharp
AuthenticationState authState = await AuthenticationStateProvider.GetAuthenticationStateAsync();
ClaimsPrincipal user = authState.User;

if (user.Identity.IsAuthenticated)
{
  // work with user.Claims and/or user.Roles
}
```

<span data-ttu-id="7abdf-174">**Uwaga:** `AuthorizeView` Składnik omówiony w dalszej części tego rozdziału stanowi deklaratywny sposób sterowania tym, co użytkownik widzi na stronie lub w składniku.</span><span class="sxs-lookup"><span data-stu-id="7abdf-174">**Note:** The `AuthorizeView` component, covered later in this chapter, provides a declarative way to control what a user sees on a page or component.</span></span>

<span data-ttu-id="7abdf-175">Aby współpracować z użytkownikami i oświadczeniami (w Blazor aplikacjach serwerowych), może być również konieczne wstrzyknięcie `UserManager<T>` ( `IdentityUser` domyślne użycie), którego można użyć do wyliczania i modyfikowania oświadczeń dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7abdf-175">To work with users and claims (in Blazor Server applications) you may also need to inject a `UserManager<T>` (use `IdentityUser` for default) which you can use to enumerate and modify claims for a user.</span></span> <span data-ttu-id="7abdf-176">Najpierw wstrzyknąć typ i przypisz go do właściwości:</span><span class="sxs-lookup"><span data-stu-id="7abdf-176">First inject the type and assign it to a property:</span></span>

```csharp
@inject UserManager<IdentityUser> MyUserManager
```

<span data-ttu-id="7abdf-177">Następnie użyj jej do pracy z oświadczeniami użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7abdf-177">Then use it to work with the user's claims.</span></span> <span data-ttu-id="7abdf-178">Poniższy przykład przedstawia sposób dodawania i utrwalania roszczeń użytkownika:</span><span class="sxs-lookup"><span data-stu-id="7abdf-178">The following sample shows how to add and persist a claim on a user:</span></span>

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

<span data-ttu-id="7abdf-179">Jeśli musisz współpracować z rolami, postępuj zgodnie z tym samym podejściem.</span><span class="sxs-lookup"><span data-stu-id="7abdf-179">If you need to work with roles, follow the same approach.</span></span> <span data-ttu-id="7abdf-180">`RoleManager<T>`Aby wyświetlić same role i zarządzać nimi, może być konieczne wstrzyknięcie (użycie `IdentityRole` dla typu domyślnego).</span><span class="sxs-lookup"><span data-stu-id="7abdf-180">You may need to inject a `RoleManager<T>` (use `IdentityRole` for default type) to list and manage the roles themselves.</span></span>

<span data-ttu-id="7abdf-181">**Uwaga:** W Blazor projektach Webassembly należy udostępnić interfejsy API serwera, aby wykonać te operacje (zamiast używać `UserManager<T>` lub `RoleManager<T>` bezpośrednio).</span><span class="sxs-lookup"><span data-stu-id="7abdf-181">**Note:** In Blazor WebAssembly projects, you will need to provide server APIs to perform these operations (instead of using `UserManager<T>` or `RoleManager<T>` directly).</span></span> <span data-ttu-id="7abdf-182">BlazorAplikacja kliencka webassembly będzie zarządzać oświadczeniami i/lub rolami przez bezpieczne wywoływanie punktów końcowych interfejsu API uwidocznionych w tym celu.</span><span class="sxs-lookup"><span data-stu-id="7abdf-182">A Blazor WebAssembly client application would manage claims and/or roles by securely calling API endpoints exposed for this purpose.</span></span>

### <a name="migration-guide"></a><span data-ttu-id="7abdf-183">Przewodnik migracji</span><span class="sxs-lookup"><span data-stu-id="7abdf-183">Migration guide</span></span>

<span data-ttu-id="7abdf-184">Migracja z ASP.NET Web Forms i uniwersalnych dostawców do ASP.NET Core Identity wymaga kilku kroków:</span><span class="sxs-lookup"><span data-stu-id="7abdf-184">Migrating from ASP.NET Web Forms and universal providers to ASP.NET Core Identity requires several steps:</span></span>

1. <span data-ttu-id="7abdf-185">Utwórz schemat bazy danych tożsamości ASP.NET Core w docelowej bazie danych</span><span class="sxs-lookup"><span data-stu-id="7abdf-185">Create ASP.NET Core Identity database schema in the destination database</span></span>
2. <span data-ttu-id="7abdf-186">Migruj dane ze schematu uniwersalnego dostawcy do ASP.NET Core schematu tożsamości</span><span class="sxs-lookup"><span data-stu-id="7abdf-186">Migrate data from universal provider schema to ASP.NET Core Identity schema</span></span>
3. <span data-ttu-id="7abdf-187">Migruj konfigurację z programu `web.config` do oprogramowania pośredniczącego i usług, zazwyczaj w `Startup.cs`</span><span class="sxs-lookup"><span data-stu-id="7abdf-187">Migrate configuration from the `web.config` to middleware and services, typically in `Startup.cs`</span></span>
4. <span data-ttu-id="7abdf-188">Aktualizować poszczególne strony przy użyciu kontrolek i warunkowych, aby używać pomocników tagów i nowych interfejsów API tożsamości.</span><span class="sxs-lookup"><span data-stu-id="7abdf-188">Update individual pages using controls and conditionals to use tag helpers and new identity APIs.</span></span>

<span data-ttu-id="7abdf-189">Wszystkie wymienione kroki zostały szczegółowo opisane poniżej.</span><span class="sxs-lookup"><span data-stu-id="7abdf-189">Each of these steps is described in detail in the following sections.</span></span>

### <a name="creating-the-aspnet-core-identity-schema"></a><span data-ttu-id="7abdf-190">Tworzenie schematu tożsamości ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="7abdf-190">Creating the ASP.NET Core Identity schema</span></span>

<span data-ttu-id="7abdf-191">Istnieje kilka sposobów, aby utworzyć niezbędną strukturę tabeli służącą do ASP.NET Core tożsamości.</span><span class="sxs-lookup"><span data-stu-id="7abdf-191">There are several ways to create the necessary table structure used for ASP.NET Core Identity.</span></span> <span data-ttu-id="7abdf-192">Najprostszą jest utworzenie nowej aplikacji sieci Web ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="7abdf-192">The simplest is to create a new ASP.NET Core Web application.</span></span> <span data-ttu-id="7abdf-193">Wybierz pozycję aplikacja sieci Web, a następnie zmień uwierzytelnianie, aby korzystać z poszczególnych kont użytkowników.</span><span class="sxs-lookup"><span data-stu-id="7abdf-193">Choose Web Application and then change Authentication to use Individual User Accounts.</span></span>

![Nowy projekt z kontami poszczególnych użytkowników](./media/security/individual-user-accounts.png)

<span data-ttu-id="7abdf-195">W wierszu polecenia można wykonać tę samą czynność, uruchamiając polecenie `dotnet new webapp -au Individual` .</span><span class="sxs-lookup"><span data-stu-id="7abdf-195">From the command line, you can do the same thing by running `dotnet new webapp -au Individual`.</span></span> <span data-ttu-id="7abdf-196">Po utworzeniu aplikacji uruchom ją i zarejestruj w witrynie.</span><span class="sxs-lookup"><span data-stu-id="7abdf-196">Once the app has been created, run it and register on the site.</span></span> <span data-ttu-id="7abdf-197">Należy wyzwolić stronę tak jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="7abdf-197">You should trigger a page like the one shown below:</span></span>

![Strona zastosowania migracji](./media/security/apply-migrations-page.png)

<span data-ttu-id="7abdf-199">Kliknij przycisk "Zastosuj migracje", a następnie należy utworzyć niezbędne tabele baz danych.</span><span class="sxs-lookup"><span data-stu-id="7abdf-199">Click on the "Apply Migrations" button and the necessary database tables should be created for you.</span></span> <span data-ttu-id="7abdf-200">Ponadto pliki migracji powinny pojawić się w projekcie, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="7abdf-200">In addition, the migration files should appear in your project, as shown:</span></span>

![Pliki migracji](./media/security/migration-files.png)

<span data-ttu-id="7abdf-202">Można uruchomić migrację samodzielnie, bez uruchamiania aplikacji sieci Web, za pomocą tego narzędzia wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="7abdf-202">You can run the migration yourself, without running the web application, using this command-line tool:</span></span>

```powershell
dotnet ef database update
```

<span data-ttu-id="7abdf-203">Jeśli wolisz uruchomić skrypt w celu zastosowania nowego schematu do istniejącej bazy danych, możesz wykonać skrypty tych migracji z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="7abdf-203">If you would rather run a script to apply the new schema to an existing database, you can script these migrations from the command-line.</span></span> <span data-ttu-id="7abdf-204">Uruchom to polecenie, aby wygenerować skrypt:</span><span class="sxs-lookup"><span data-stu-id="7abdf-204">Run this command to generate the script:</span></span>

```powershell
dotnet ef migrations script -o auth.sql
```

<span data-ttu-id="7abdf-205">Powyższe polecenie spowoduje utworzenie w pliku wyjściowym skryptu SQL `auth.sql` , który można następnie uruchomić dla dowolnej bazy danych, której chcesz użyć.</span><span class="sxs-lookup"><span data-stu-id="7abdf-205">The above command will produce a SQL script in the output file `auth.sql`, which can then be run against whatever database you like.</span></span> <span data-ttu-id="7abdf-206">Jeśli masz problemy z uruchamianiem `dotnet ef` poleceń, [upewnij się, że masz narzędzia EF Core zainstalowane w systemie](/ef/core/miscellaneous/cli/dotnet).</span><span class="sxs-lookup"><span data-stu-id="7abdf-206">If you have any trouble running `dotnet ef` commands, [make sure you have the EF Core tools installed on your system](/ef/core/miscellaneous/cli/dotnet).</span></span>

<span data-ttu-id="7abdf-207">W przypadku, gdy w tabeli źródłowej znajdują się dodatkowe kolumny, należy zidentyfikować najlepszą lokalizację dla tych kolumn w nowym schemacie.</span><span class="sxs-lookup"><span data-stu-id="7abdf-207">In the event you have additional columns on your source tables, you will need to identify the best location for these columns in the new schema.</span></span> <span data-ttu-id="7abdf-208">Na ogół kolumny Znalezione w `aspnet_Membership` tabeli powinny być mapowane na `AspNetUsers` tabelę.</span><span class="sxs-lookup"><span data-stu-id="7abdf-208">Generally, columns found on the `aspnet_Membership` table should be mapped to the `AspNetUsers` table.</span></span> <span data-ttu-id="7abdf-209">Kolumny na `aspnet_Roles` powinny być mapowane na `AspNetRoles` .</span><span class="sxs-lookup"><span data-stu-id="7abdf-209">Columns on `aspnet_Roles` should be mapped to `AspNetRoles`.</span></span> <span data-ttu-id="7abdf-210">Wszystkie dodatkowe kolumny w `aspnet_UsersInRoles` tabeli zostaną dodane do `AspNetUserRoles` tabeli.</span><span class="sxs-lookup"><span data-stu-id="7abdf-210">Any additional columns on the `aspnet_UsersInRoles` table would be added to the `AspNetUserRoles` table.</span></span>

<span data-ttu-id="7abdf-211">Warto również rozważać wprowadzanie wszelkich dodatkowych kolumn w oddzielnych tabelach.</span><span class="sxs-lookup"><span data-stu-id="7abdf-211">It's also worth considering putting any additional columns on separate tables.</span></span> <span data-ttu-id="7abdf-212">Tak więc przyszłe migracje nie muszą uwzględniać takich dostosowań domyślnego schematu tożsamości.</span><span class="sxs-lookup"><span data-stu-id="7abdf-212">So that future migrations won't need to take into account such customizations of the default identity schema.</span></span>

### <a name="migrating-data-from-universal-providers-to-aspnet-core-identity"></a><span data-ttu-id="7abdf-213">Migrowanie danych od dostawców uniwersalnych do ASP.NET Core Identity</span><span class="sxs-lookup"><span data-stu-id="7abdf-213">Migrating data from universal providers to ASP.NET Core Identity</span></span>

<span data-ttu-id="7abdf-214">Gdy masz docelowy schemat tabeli, następnym krokiem jest Migrowanie rekordów użytkownika i roli do nowego schematu.</span><span class="sxs-lookup"><span data-stu-id="7abdf-214">Once you have the destination table schema in place, the next step is to migrate your user and role records to the new schema.</span></span> <span data-ttu-id="7abdf-215">Pełna lista różnic między schematami, w tym te, które kolumny są mapowane na nowe kolumny, można znaleźć [tutaj](/aspnet/core/migration/proper-to-2x/membership-to-core-identity).</span><span class="sxs-lookup"><span data-stu-id="7abdf-215">A complete list of the schema differences, including which columns map to which new columns, can be found [here](/aspnet/core/migration/proper-to-2x/membership-to-core-identity).</span></span>

<span data-ttu-id="7abdf-216">Aby przeprowadzić migrację użytkowników z członkostwa do nowych tabel tożsamości, należy [wykonać kroki opisane w dokumentacji](/aspnet/core/migration/proper-to-2x/membership-to-core-identity).</span><span class="sxs-lookup"><span data-stu-id="7abdf-216">To migrate your users from membership to the new identity tables, you should [follow the steps described in the documentation](/aspnet/core/migration/proper-to-2x/membership-to-core-identity).</span></span> <span data-ttu-id="7abdf-217">Po wykonaniu tych kroków i podanego skryptu użytkownicy będą musieli zmienić hasło przy następnym logowaniu.</span><span class="sxs-lookup"><span data-stu-id="7abdf-217">After following these steps and the script provided, your users will need to change their password the next time they log in.</span></span>

<span data-ttu-id="7abdf-218">Możliwe jest Migrowanie haseł użytkowników, ale proces jest znacznie bardziej powiązany.</span><span class="sxs-lookup"><span data-stu-id="7abdf-218">It is possible to migrate user passwords but the process is much more involved.</span></span> <span data-ttu-id="7abdf-219">Wymaganie od użytkowników aktualizowania haseł w ramach procesu migracji i zachęcania ich do korzystania z nowych, unikatowych haseł może wzmocnić ogólne zabezpieczenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7abdf-219">Requiring users to update their passwords as part of the migration process, and encouraging them to use new, unique passwords, is likely to enhance the overall security of the application.</span></span>

### <a name="migrating-security-settings-from-webconfig-to-startupcs"></a><span data-ttu-id="7abdf-220">Migrowanie ustawień zabezpieczeń z web.config do Startup.cs</span><span class="sxs-lookup"><span data-stu-id="7abdf-220">Migrating security settings from web.config to Startup.cs</span></span>

<span data-ttu-id="7abdf-221">Jak wspomniano powyżej, ASP.NET członkostwa i dostawcy ról są konfigurowane w pliku aplikacji `web.config` .</span><span class="sxs-lookup"><span data-stu-id="7abdf-221">As noted above, ASP.NET membership and role providers are configured in the application's `web.config` file.</span></span> <span data-ttu-id="7abdf-222">Ponieważ ASP.NET Core aplikacje nie są powiązane z usługami IIS i używają osobnego systemu do konfiguracji, te ustawienia muszą być skonfigurowane w innym miejscu.</span><span class="sxs-lookup"><span data-stu-id="7abdf-222">Since ASP.NET Core apps are not tied to IIS and use a separate system for configuration, these settings must be configured elsewhere.</span></span> <span data-ttu-id="7abdf-223">W większości przypadków ASP.NET Core tożsamość jest konfigurowana w `Startup.cs` pliku.</span><span class="sxs-lookup"><span data-stu-id="7abdf-223">For the most part, ASP.NET Core Identity is configured in the `Startup.cs` file.</span></span> <span data-ttu-id="7abdf-224">Otwórz projekt sieci Web, który został utworzony wcześniej (aby wygenerować schemat tabeli tożsamości) i przejrzyj jego `Startup.cs` plik.</span><span class="sxs-lookup"><span data-stu-id="7abdf-224">Open the web project that was created earlier (to generate the identity table schema) and review its `Startup.cs` file.</span></span>

<span data-ttu-id="7abdf-225">Domyślna metoda ConfigureServices dodaje obsługę EF Core i tożsamości:</span><span class="sxs-lookup"><span data-stu-id="7abdf-225">The default ConfigureServices method adds support for EF Core and Identity:</span></span>

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

<span data-ttu-id="7abdf-226">`AddDefaultIdentity`Metoda rozszerzenia służy do konfigurowania tożsamości do używania domyślnego `ApplicationDbContext` i `IdentityUser` typu struktury.</span><span class="sxs-lookup"><span data-stu-id="7abdf-226">The `AddDefaultIdentity` extension method is used to configure Identity to use the default `ApplicationDbContext` and the framework's `IdentityUser` type.</span></span> <span data-ttu-id="7abdf-227">Jeśli używasz niestandardowego `IdentityUser` , pamiętaj o określeniu jego typu w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="7abdf-227">If you're using a custom `IdentityUser`, be sure to specify its type here.</span></span> <span data-ttu-id="7abdf-228">Jeśli te metody rozszerzające nie działają w aplikacji, sprawdź, czy masz odpowiednie instrukcje using i czy masz wymagane odwołania do pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="7abdf-228">If these extension methods aren't working in your application, check that you have the appropriate using statements and that you have the necessary NuGet package references.</span></span> <span data-ttu-id="7abdf-229">Na przykład projekt powinien mieć pewną wersję `Microsoft.AspNetCore.Identity.EntityFrameworkCore` pakietów i, `Microsoft.AspNetCore.Identity.UI` do których się odwołuje.</span><span class="sxs-lookup"><span data-stu-id="7abdf-229">For example, your project should have some version of the `Microsoft.AspNetCore.Identity.EntityFrameworkCore` and `Microsoft.AspNetCore.Identity.UI` packages referenced.</span></span>

<span data-ttu-id="7abdf-230">Ponadto `Startup.cs` należy zobaczyć wymagane oprogramowanie pośredniczące skonfigurowane dla danej lokacji.</span><span class="sxs-lookup"><span data-stu-id="7abdf-230">Also in `Startup.cs` you should see the necessary middleware configured for the site.</span></span> <span data-ttu-id="7abdf-231">`UseAuthentication`I `UseAuthorization` należy je skonfigurować i w odpowiedniej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="7abdf-231">Specifically, `UseAuthentication` and `UseAuthorization` should be set up, and in the proper location.</span></span>

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

<span data-ttu-id="7abdf-232">ASP.NET Identity nie konfiguruje dostępu anonimowego lub opartego na rolach do lokalizacji z programu `Startup.cs` .</span><span class="sxs-lookup"><span data-stu-id="7abdf-232">ASP.NET Identity does not configure anonymous or role-based access to locations from `Startup.cs`.</span></span> <span data-ttu-id="7abdf-233">Należy przeprowadzić migrację danych konfiguracji autoryzacji specyficznych dla lokalizacji do filtrów w ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="7abdf-233">You will need to migrate any location-specific authorization configuration data to filters in ASP.NET Core.</span></span> <span data-ttu-id="7abdf-234">Zanotuj, które foldery i strony będą wymagały takich aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="7abdf-234">Make note of which folders and pages will require such updates.</span></span> <span data-ttu-id="7abdf-235">Te zmiany zostaną wprowadzone w następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="7abdf-235">You will make these changes in the next section.</span></span>

### <a name="updating-individual-pages-to-use-aspnet-core-identity-abstractions"></a><span data-ttu-id="7abdf-236">Aktualizowanie poszczególnych stron do użycia w ASP.NET Core Abstracts Identity</span><span class="sxs-lookup"><span data-stu-id="7abdf-236">Updating individual pages to use ASP.NET Core Identity abstractions</span></span>

<span data-ttu-id="7abdf-237">W aplikacji formularze sieci Web ASP.NET, jeśli masz `web.config` Ustawienia, aby odmówić dostępu do określonych stron lub folderów użytkownikom anonimowym, należy zmigrować te zmiany, dodając `[Authorize]` atrybut do takich stron:</span><span class="sxs-lookup"><span data-stu-id="7abdf-237">In your ASP.NET Web Forms application, if you had `web.config` settings to deny access to certain pages or folders to anonymous users, you would migrate these changes by adding the `[Authorize]` attribute to such pages:</span></span>

```razor
@attribute [Authorize]
```

<span data-ttu-id="7abdf-238">Jeśli chcesz jeszcze odmówić dostępu z wyjątkiem tych użytkowników należących do określonej roli, Przeprowadź migrację tego zachowania, dodając atrybut określający rolę:</span><span class="sxs-lookup"><span data-stu-id="7abdf-238">If you further had denied access except to those users belonging to a certain role, you would likewise migrate this behavior by adding an attribute specifying a role:</span></span>

```razor
@attribute [Authorize(Roles ="administrators")]
```

<span data-ttu-id="7abdf-239">Ten `[Authorize]` atrybut działa tylko na `@page` składnikach, które są osiągalne za pośrednictwem Blazor routera.</span><span class="sxs-lookup"><span data-stu-id="7abdf-239">The `[Authorize]` attribute only works on `@page` components that are reached via the Blazor Router.</span></span> <span data-ttu-id="7abdf-240">Ten atrybut nie działa ze składnikami podrzędnymi, które należy zamiast tego używać `AuthorizeView` .</span><span class="sxs-lookup"><span data-stu-id="7abdf-240">The attribute does not work with child components, which should instead use `AuthorizeView`.</span></span>

<span data-ttu-id="7abdf-241">Jeśli masz logikę w ramach znaczników strony, aby określić, czy ma być wyświetlany jakiś kod dla określonego użytkownika, możesz zastąpić ten `AuthorizeView` składnik.</span><span class="sxs-lookup"><span data-stu-id="7abdf-241">If you have logic within page markup for determining whether to display some code to a certain user, you can replace this with the `AuthorizeView` component.</span></span> <span data-ttu-id="7abdf-242">[Składnik AuthorizeView](/aspnet/core/blazor/security#authorizeview-component) selektywnie wyświetla interfejs użytkownika w zależności od tego, czy użytkownik jest uprawniony do jego wyświetlania.</span><span class="sxs-lookup"><span data-stu-id="7abdf-242">The [AuthorizeView component](/aspnet/core/blazor/security#authorizeview-component) selectively displays UI depending on whether the user is authorized to see it.</span></span> <span data-ttu-id="7abdf-243">Udostępnia również `context` zmienną, której można użyć w celu uzyskania dostępu do informacji o użytkowniku.</span><span class="sxs-lookup"><span data-stu-id="7abdf-243">It also exposes a `context` variable that can be used to access user information.</span></span>

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

<span data-ttu-id="7abdf-244">Możesz uzyskać dostęp do stanu uwierzytelniania w ramach logiki proceduralnej, uzyskując dostęp do użytkownika ze `Task<AuthenticationState` skonfigurowanego za pomocą `[CascadingParameter]` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="7abdf-244">You can access the authentication state within procedural logic by accessing the user from a `Task<AuthenticationState` configured with the `[CascadingParameter]` attribute.</span></span> <span data-ttu-id="7abdf-245">Ta konfiguracja umożliwi użytkownikowi dostęp do użytkownika, który może określić, czy są uwierzytelniani i czy należą do określonej roli.</span><span class="sxs-lookup"><span data-stu-id="7abdf-245">This configuration will get you access to the user, which can let you determine if they are authenticated and if they belong to a particular role.</span></span> <span data-ttu-id="7abdf-246">Jeśli konieczne jest ocenę zasad proceduralnych, można wstrzyknąć wystąpienie obiektu `IAuthorizationService` i wywołać `AuthorizeAsync` metodę.</span><span class="sxs-lookup"><span data-stu-id="7abdf-246">If you need to evaluate a policy procedurally, you can inject an instance of the `IAuthorizationService` and calls the `AuthorizeAsync` method on it.</span></span> <span data-ttu-id="7abdf-247">Następujący przykładowy kod demonstruje, jak uzyskać informacje o użytkowniku i zezwolić autoryzowanemu użytkownikowi na wykonanie zadania ograniczonego przez `content-editor` zasady.</span><span class="sxs-lookup"><span data-stu-id="7abdf-247">The following sample code demonstrates how to get user information and allow an authorized user to perform a task restricted by the `content-editor` policy.</span></span>

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

<span data-ttu-id="7abdf-248">`AuthenticationState`Najpierw należy skonfigurować jako wartość kaskadową, zanim będzie można powiązać ją z parametrem kaskadowym podobnym do tego.</span><span class="sxs-lookup"><span data-stu-id="7abdf-248">The `AuthenticationState` first need to be set up as a cascading value before it can be bound to a cascading parameter like this.</span></span> <span data-ttu-id="7abdf-249">Zwykle jest to wykonywane przy użyciu `CascadingAuthenticationState` składnika.</span><span class="sxs-lookup"><span data-stu-id="7abdf-249">That's typically done using the `CascadingAuthenticationState` component.</span></span> <span data-ttu-id="7abdf-250">Ta konfiguracja jest zazwyczaj wykonywana w `App.razor` :</span><span class="sxs-lookup"><span data-stu-id="7abdf-250">This configuration is typically done in `App.razor`:</span></span>

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

## <a name="summary"></a><span data-ttu-id="7abdf-251">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="7abdf-251">Summary</span></span>

<span data-ttu-id="7abdf-252">Blazor używa tego samego modelu zabezpieczeń co ASP.NET Core, który jest ASP.NET Core tożsamością.</span><span class="sxs-lookup"><span data-stu-id="7abdf-252">Blazor uses the same security model as ASP.NET Core, which is ASP.NET Core Identity.</span></span> <span data-ttu-id="7abdf-253">Migracja z uniwersalnych dostawców do ASP.NET Core tożsamość jest stosunkowo prosta, przy założeniu, że nie zbyt dużo dostosowania zostało zastosowane do oryginalnego schematu danych.</span><span class="sxs-lookup"><span data-stu-id="7abdf-253">Migrating from universal providers to ASP.NET Core Identity is relatively straightforward, assuming not too much customization was applied to the original data schema.</span></span> <span data-ttu-id="7abdf-254">Po przeprowadzeniu migracji danych Praca z uwierzytelnianiem i autoryzacją w Blazor aplikacjach jest dobrze udokumentowana, z możliwością konfiguracji oraz obsługą techniczną w przypadku większości wymagań dotyczących zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="7abdf-254">Once the data has been migrated, working with authentication and authorization in Blazor apps is well documented, with configurable as well as programmatic support for most security requirements.</span></span>

## <a name="references"></a><span data-ttu-id="7abdf-255">Odwołania</span><span class="sxs-lookup"><span data-stu-id="7abdf-255">References</span></span>

- [<span data-ttu-id="7abdf-256">Wprowadzenie do tożsamości na ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="7abdf-256">Introduction to Identity on ASP.NET Core</span></span>](/aspnet/core/security/authentication/identity)
- [<span data-ttu-id="7abdf-257">Migrowanie z uwierzytelniania członkostwa ASP.NET do tożsamości ASP.NET Core 2,0</span><span class="sxs-lookup"><span data-stu-id="7abdf-257">Migrate from ASP.NET Membership authentication to ASP.NET Core 2.0 Identity</span></span>](/aspnet/core/migration/proper-to-2x/membership-to-core-identity)
- [<span data-ttu-id="7abdf-258">Migrowanie uwierzytelniania i tożsamości do ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="7abdf-258">Migrate Authentication and Identity to ASP.NET Core</span></span>](/aspnet/core/migration/identity)
- [<span data-ttu-id="7abdf-259">ASP.NET Core Blazor uwierzytelnianie i autoryzacja</span><span class="sxs-lookup"><span data-stu-id="7abdf-259">ASP.NET Core Blazor authentication and authorization</span></span>](/aspnet/core/blazor/security/)

>[!div class="step-by-step"]
><span data-ttu-id="7abdf-260">[Poprzedni](config.md) 
> [Dalej](migration.md)</span><span class="sxs-lookup"><span data-stu-id="7abdf-260">[Previous](config.md)
[Next](migration.md)</span></span>
