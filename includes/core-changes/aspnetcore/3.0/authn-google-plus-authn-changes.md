---
ms.openlocfilehash: 14d80f25c34465caa6dec10e5704fe0a3cbccc71
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96476421"
---
### <a name="authentication-google-deprecated-and-replaced"></a><span data-ttu-id="9b0b4-101">Uwierzytelnianie: Firma Google + przestarzała i zastąpiona</span><span class="sxs-lookup"><span data-stu-id="9b0b4-101">Authentication: Google+ deprecated and replaced</span></span>

<span data-ttu-id="9b0b4-102">Firma Google rozpoczyna [zamykanie](https://developers.google.com/+/api-shutdown) usługi Google + logowanie dla aplikacji tak wcześnie, jak 28 stycznia 2019.</span><span class="sxs-lookup"><span data-stu-id="9b0b4-102">Google is starting to [shut down](https://developers.google.com/+/api-shutdown) Google+ Sign-in for apps as early as January 28, 2019.</span></span>

#### <a name="change-description"></a><span data-ttu-id="9b0b4-103">Zmień opis</span><span class="sxs-lookup"><span data-stu-id="9b0b4-103">Change description</span></span>

<span data-ttu-id="9b0b4-104">ASP.NET 4. x i ASP.NET Core używają interfejsów API logowania Google + do uwierzytelniania użytkowników konta Google w aplikacjach sieci Web.</span><span class="sxs-lookup"><span data-stu-id="9b0b4-104">ASP.NET 4.x and ASP.NET Core have been using the Google+ Sign-in APIs to authenticate Google account users in web apps.</span></span> <span data-ttu-id="9b0b4-105">Pakiety NuGet, których to dotyczy, to [Microsoft. AspNetCore. Authentication. Google](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.Google/) for ASP.NET Core i [Microsoft. Owin. Security. google](https://www.nuget.org/packages/Microsoft.Owin.Security.Google/) for `Microsoft.Owin` with ASP.NET Web Forms i MVC.</span><span class="sxs-lookup"><span data-stu-id="9b0b4-105">The affected NuGet packages are [Microsoft.AspNetCore.Authentication.Google](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.Google/) for ASP.NET Core and [Microsoft.Owin.Security.Google](https://www.nuget.org/packages/Microsoft.Owin.Security.Google/) for `Microsoft.Owin` with ASP.NET Web Forms and MVC.</span></span>

<span data-ttu-id="9b0b4-106">Interfejsy API wymiany firmy Google używają innego źródła danych i formatu.</span><span class="sxs-lookup"><span data-stu-id="9b0b4-106">Google's replacement APIs use a different data source and format.</span></span> <span data-ttu-id="9b0b4-107">Środki zaradcze i rozwiązania podane poniżej uwzględniają zmiany strukturalne.</span><span class="sxs-lookup"><span data-stu-id="9b0b4-107">The mitigations and solutions provided below account for the structural changes.</span></span> <span data-ttu-id="9b0b4-108">Aplikacje powinny sprawdzić, czy same dane nadal spełniają wymagania.</span><span class="sxs-lookup"><span data-stu-id="9b0b4-108">Apps should verify the data itself still satisfies their requirements.</span></span> <span data-ttu-id="9b0b4-109">Na przykład nazwy, adresy e-mail, linki profilów i Zdjęcia profilu mogą mieć mniejsze wartości niż poprzednio.</span><span class="sxs-lookup"><span data-stu-id="9b0b4-109">For example, names, email addresses, profile links, and profile photos may provide subtly different values than before.</span></span>

#### <a name="version-introduced"></a><span data-ttu-id="9b0b4-110">Wprowadzona wersja</span><span class="sxs-lookup"><span data-stu-id="9b0b4-110">Version introduced</span></span>

<span data-ttu-id="9b0b4-111">Wszystkie wersje.</span><span class="sxs-lookup"><span data-stu-id="9b0b4-111">All versions.</span></span> <span data-ttu-id="9b0b4-112">Ta zmiana jest zewnętrzna dla ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="9b0b4-112">This change is external to ASP.NET Core.</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="9b0b4-113">Zalecana akcja</span><span class="sxs-lookup"><span data-stu-id="9b0b4-113">Recommended action</span></span>

##### <a name="owin-with-aspnet-web-forms-and-mvc"></a><span data-ttu-id="9b0b4-114">Owin z ASP.NET Web Forms i MVC</span><span class="sxs-lookup"><span data-stu-id="9b0b4-114">Owin with ASP.NET Web Forms and MVC</span></span>

<span data-ttu-id="9b0b4-115">W przypadku `Microsoft.Owin` 3.1.0 i nowszych można znaleźć w [tym miejscu](https://github.com/aspnet/AspNetKatana/issues/251#issuecomment-449587635)tymczasowe środki zaradcze.</span><span class="sxs-lookup"><span data-stu-id="9b0b4-115">For `Microsoft.Owin` 3.1.0 and later, a temporary mitigation is outlined [here](https://github.com/aspnet/AspNetKatana/issues/251#issuecomment-449587635).</span></span> <span data-ttu-id="9b0b4-116">Aplikacje powinny zakończyć testowanie przy użyciu środków zaradczych, aby sprawdzić zmiany w formacie danych.</span><span class="sxs-lookup"><span data-stu-id="9b0b4-116">Apps should complete testing with the mitigation to check for changes in the data format.</span></span> <span data-ttu-id="9b0b4-117">Istnieją plany wydania `Microsoft.Owin` 4.0.1 z poprawkami.</span><span class="sxs-lookup"><span data-stu-id="9b0b4-117">There are plans to release `Microsoft.Owin` 4.0.1 with a fix.</span></span> <span data-ttu-id="9b0b4-118">Aplikacje korzystające ze starszej wersji powinny aktualizować wersję 4.0.1.</span><span class="sxs-lookup"><span data-stu-id="9b0b4-118">Apps using any prior version should update to version 4.0.1.</span></span>

##### <a name="aspnet-core-1x"></a><span data-ttu-id="9b0b4-119">ASP.NET Core 1. x</span><span class="sxs-lookup"><span data-stu-id="9b0b4-119">ASP.NET Core 1.x</span></span>

<span data-ttu-id="9b0b4-120">Środki zaradcze w [Owin z ASP.NET Web Forms i MVC](#owin-with-aspnet-web-forms-and-mvc) można dostosować do ASP.NET Core 1. x.</span><span class="sxs-lookup"><span data-stu-id="9b0b4-120">The mitigation in [Owin with ASP.NET Web Forms and MVC](#owin-with-aspnet-web-forms-and-mvc) can be adapted to ASP.NET Core 1.x.</span></span> <span data-ttu-id="9b0b4-121">Poprawki pakietu NuGet nie są planowane, ponieważ 1. x osiągnął stan [życia](https://dotnet.microsoft.com/platform/support-policy) .</span><span class="sxs-lookup"><span data-stu-id="9b0b4-121">NuGet package patches aren't planned because 1.x has reached [end of life](https://dotnet.microsoft.com/platform/support-policy) status.</span></span>

##### <a name="aspnet-core-2x"></a><span data-ttu-id="9b0b4-122">ASP.NET Core 2. x</span><span class="sxs-lookup"><span data-stu-id="9b0b4-122">ASP.NET Core 2.x</span></span>

<span data-ttu-id="9b0b4-123">W przypadku `Microsoft.AspNetCore.Authentication.Google` wersji 2. x Zastąp istniejące wywołanie do `AddGoogle` programu `Startup.ConfigureServices` przy użyciu następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="9b0b4-123">For `Microsoft.AspNetCore.Authentication.Google` version 2.x, replace your existing call to `AddGoogle` in `Startup.ConfigureServices` with the following code:</span></span>

```csharp
.AddGoogle(o =>
{
    o.ClientId = Configuration["Authentication:Google:ClientId"];
    o.ClientSecret = Configuration["Authentication:Google:ClientSecret"];
    o.UserInformationEndpoint = "https://www.googleapis.com/oauth2/v2/userinfo";
    o.ClaimActions.Clear();
    o.ClaimActions.MapJsonKey(ClaimTypes.NameIdentifier, "id");
    o.ClaimActions.MapJsonKey(ClaimTypes.Name, "name");
    o.ClaimActions.MapJsonKey(ClaimTypes.GivenName, "given_name");
    o.ClaimActions.MapJsonKey(ClaimTypes.Surname, "family_name");
    o.ClaimActions.MapJsonKey("urn:google:profile", "link");
    o.ClaimActions.MapJsonKey(ClaimTypes.Email, "email");
});
```

<span data-ttu-id="9b0b4-124">Poprawki 2,1 lutego i 2,2 dołączone do poprzedniej ponownej konfiguracji jako nowe domyślne.</span><span class="sxs-lookup"><span data-stu-id="9b0b4-124">The February 2.1 and 2.2 patches incorporated the preceding reconfiguration as the new default.</span></span> <span data-ttu-id="9b0b4-125">Nie zaplanowano żadnych poprawek dla ASP.NET Core 2,0, ponieważ osiągnięto [koniec cyklu życia](https://dotnet.microsoft.com/platform/support-policy).</span><span class="sxs-lookup"><span data-stu-id="9b0b4-125">No patch is planned for ASP.NET Core 2.0 since it has reached [end of life](https://dotnet.microsoft.com/platform/support-policy).</span></span>

##### <a name="aspnet-core-30"></a><span data-ttu-id="9b0b4-126">ASP.NET Core 3,0</span><span class="sxs-lookup"><span data-stu-id="9b0b4-126">ASP.NET Core 3.0</span></span>

<span data-ttu-id="9b0b4-127">Środki zaradcze określone dla ASP.NET Core 2. x mogą być również używane dla ASP.NET Core 3,0.</span><span class="sxs-lookup"><span data-stu-id="9b0b4-127">The mitigation given for ASP.NET Core 2.x can also be used for ASP.NET Core 3.0.</span></span> <span data-ttu-id="9b0b4-128">W przyszłości wersje zapoznawcze 3,0 `Microsoft.AspNetCore.Authentication.Google` pakietu mogą zostać usunięte.</span><span class="sxs-lookup"><span data-stu-id="9b0b4-128">In future 3.0 previews, the `Microsoft.AspNetCore.Authentication.Google` package may be removed.</span></span> <span data-ttu-id="9b0b4-129">Użytkownicy będą kierowani do `Microsoft.AspNetCore.Authentication.OpenIdConnect` zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="9b0b4-129">Users would be directed to `Microsoft.AspNetCore.Authentication.OpenIdConnect` instead.</span></span> <span data-ttu-id="9b0b4-130">Poniższy kod ilustruje sposób zamiany na `AddGoogle` `AddOpenIdConnect` w `Startup.ConfigureServices` .</span><span class="sxs-lookup"><span data-stu-id="9b0b4-130">The following code shows how to replace `AddGoogle` with `AddOpenIdConnect` in `Startup.ConfigureServices`.</span></span> <span data-ttu-id="9b0b4-131">Tego zastąpienia można użyć w przypadku ASP.NET Core 2,0 i nowszych. można go dostosować do ASP.NET Core 1. x zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="9b0b4-131">This replacement can be used with ASP.NET Core 2.0 and later and can be adapted for ASP.NET Core 1.x as needed.</span></span>

```csharp
.AddOpenIdConnect("Google", o =>
{
    o.ClientId = Configuration["Authentication:Google:ClientId"];
    o.ClientSecret = Configuration["Authentication:Google:ClientSecret"];
    o.Authority = "https://accounts.google.com";
    o.ResponseType = OpenIdConnectResponseType.Code;
    o.CallbackPath = "/signin-google"; // Or register the default "/signin-oidc"
    o.Scope.Add("email");
});
JwtSecurityTokenHandler.DefaultInboundClaimTypeMap.Clear();
```

#### <a name="category"></a><span data-ttu-id="9b0b4-132">Kategoria</span><span class="sxs-lookup"><span data-stu-id="9b0b4-132">Category</span></span>

<span data-ttu-id="9b0b4-133">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="9b0b4-133">ASP.NET Core</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="9b0b4-134">Dotyczy interfejsów API</span><span class="sxs-lookup"><span data-stu-id="9b0b4-134">Affected APIs</span></span>

<xref:Microsoft.AspNetCore.Authentication.Google?displayProperty=fullName>

<!-- 

#### Affected APIs

`N:Microsoft.AspNetCore.Authentication.Google`

-->
