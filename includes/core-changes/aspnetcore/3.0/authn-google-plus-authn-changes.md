---
ms.openlocfilehash: 14d80f25c34465caa6dec10e5704fe0a3cbccc71
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96476421"
---
### <a name="authentication-google-deprecated-and-replaced"></a>Uwierzytelnianie: Firma Google + przestarzała i zastąpiona

Firma Google rozpoczyna [zamykanie](https://developers.google.com/+/api-shutdown) usługi Google + logowanie dla aplikacji tak wcześnie, jak 28 stycznia 2019.

#### <a name="change-description"></a>Zmień opis

ASP.NET 4. x i ASP.NET Core używają interfejsów API logowania Google + do uwierzytelniania użytkowników konta Google w aplikacjach sieci Web. Pakiety NuGet, których to dotyczy, to [Microsoft. AspNetCore. Authentication. Google](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.Google/) for ASP.NET Core i [Microsoft. Owin. Security. google](https://www.nuget.org/packages/Microsoft.Owin.Security.Google/) for `Microsoft.Owin` with ASP.NET Web Forms i MVC.

Interfejsy API wymiany firmy Google używają innego źródła danych i formatu. Środki zaradcze i rozwiązania podane poniżej uwzględniają zmiany strukturalne. Aplikacje powinny sprawdzić, czy same dane nadal spełniają wymagania. Na przykład nazwy, adresy e-mail, linki profilów i Zdjęcia profilu mogą mieć mniejsze wartości niż poprzednio.

#### <a name="version-introduced"></a>Wprowadzona wersja

Wszystkie wersje. Ta zmiana jest zewnętrzna dla ASP.NET Core.

#### <a name="recommended-action"></a>Zalecana akcja

##### <a name="owin-with-aspnet-web-forms-and-mvc"></a>Owin z ASP.NET Web Forms i MVC

W przypadku `Microsoft.Owin` 3.1.0 i nowszych można znaleźć w [tym miejscu](https://github.com/aspnet/AspNetKatana/issues/251#issuecomment-449587635)tymczasowe środki zaradcze. Aplikacje powinny zakończyć testowanie przy użyciu środków zaradczych, aby sprawdzić zmiany w formacie danych. Istnieją plany wydania `Microsoft.Owin` 4.0.1 z poprawkami. Aplikacje korzystające ze starszej wersji powinny aktualizować wersję 4.0.1.

##### <a name="aspnet-core-1x"></a>ASP.NET Core 1. x

Środki zaradcze w [Owin z ASP.NET Web Forms i MVC](#owin-with-aspnet-web-forms-and-mvc) można dostosować do ASP.NET Core 1. x. Poprawki pakietu NuGet nie są planowane, ponieważ 1. x osiągnął stan [życia](https://dotnet.microsoft.com/platform/support-policy) .

##### <a name="aspnet-core-2x"></a>ASP.NET Core 2. x

W przypadku `Microsoft.AspNetCore.Authentication.Google` wersji 2. x Zastąp istniejące wywołanie do `AddGoogle` programu `Startup.ConfigureServices` przy użyciu następującego kodu:

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

Poprawki 2,1 lutego i 2,2 dołączone do poprzedniej ponownej konfiguracji jako nowe domyślne. Nie zaplanowano żadnych poprawek dla ASP.NET Core 2,0, ponieważ osiągnięto [koniec cyklu życia](https://dotnet.microsoft.com/platform/support-policy).

##### <a name="aspnet-core-30"></a>ASP.NET Core 3,0

Środki zaradcze określone dla ASP.NET Core 2. x mogą być również używane dla ASP.NET Core 3,0. W przyszłości wersje zapoznawcze 3,0 `Microsoft.AspNetCore.Authentication.Google` pakietu mogą zostać usunięte. Użytkownicy będą kierowani do `Microsoft.AspNetCore.Authentication.OpenIdConnect` zamiast tego. Poniższy kod ilustruje sposób zamiany na `AddGoogle` `AddOpenIdConnect` w `Startup.ConfigureServices` . Tego zastąpienia można użyć w przypadku ASP.NET Core 2,0 i nowszych. można go dostosować do ASP.NET Core 1. x zgodnie z potrzebami.

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

#### <a name="category"></a>Kategoria

ASP.NET Core

#### <a name="affected-apis"></a>Dotyczy interfejsów API

<xref:Microsoft.AspNetCore.Authentication.Google?displayProperty=fullName>

<!-- 

#### Affected APIs

`N:Microsoft.AspNetCore.Authentication.Google`

-->
