---
title: ASP.NET Core istotne zmiany
titleSuffix: ''
description: Wyświetla listę istotnych zmian w ASP.NET Core 3,0 i 3,1.
ms.date: 11/03/2020
author: scottaddie
ms.author: scaddie
ms.openlocfilehash: 40dfda77dd51ed46366ec6cd8f6598070e8ce846
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "96032688"
---
# <a name="aspnet-core-breaking-changes-for-versions-30-and-31"></a>ASP.NET Core istotne zmiany w wersjach 3,0 i 3,1

ASP.NET Core udostępnia funkcje deweloperskie aplikacji sieci Web używane przez platformę .NET Core.

Wybierz jedno z poniższych linków, aby uzyskać istotne zmiany w określonej wersji:

* [ASP.NET Core 3,1](#aspnet-core-31)
* [ASP.NET Core 3,0](#aspnet-core-30)

Następujące istotne zmiany w ASP.NET Core 3,0 i 3,1 zostały udokumentowane na tej stronie:

- [Usunięto przestarzałe interfejsy API "antysfałszowane", "CORS, Diagnostics, MVC i Routing"](#obsolete-antiforgery-cors-diagnostics-mvc-and-routing-apis-removed)
- [Uwierzytelnianie: Google + zaniechana](#authentication-google-deprecated-and-replaced)
- [Uwierzytelnianie: Właściwość HttpContext. Authentication została usunięta](#authentication-httpcontextauthentication-property-removed)
- [Uwierzytelnianie: Newtonsoft.Jstypów zamieniono](#authentication-newtonsoftjson-types-replaced)
- [Uwierzytelnianie: OAuthHandler ExchangeCodeAsync zmieniono sygnaturę](#authentication-oauthhandler-exchangecodeasync-signature-changed)
- [Autoryzacja: Przeciążenie metody addauthorization przeniesiono do innego zestawu](#authorization-addauthorization-overload-moved-to-different-assembly)
- [Autoryzacja: Usunięto IAllowAnonymous z AuthorizationFilterContext. filters](#authorization-iallowanonymous-removed-from-authorizationfiltercontextfilters)
- [Autoryzacja: implementacje IAuthorizationPolicyProvider wymagają nowej metody](#authorization-iauthorizationpolicyprovider-implementations-require-new-method)
- [Buforowanie: Usunięto Właściwość CompactOnMemoryPressure](#caching-compactonmemorypressure-property-removed)
- [Buforowanie: Microsoft. Extensions. buforowanie. SqlServer używa nowego pakietu SqlClient](#caching-microsoftextensionscachingsqlserver-uses-new-sqlclient-package)
- [Ochrona danych: dataprotection. obiekty blob używają nowych interfejsów API usługi Azure Storage](#data-protection-dataprotectionblobs-uses-new-azure-storage-apis)
- [Hosting: AspNetCoreModule V1 został usunięty z pakietu hostingu systemu Windows](#hosting-aspnetcoremodule-v1-removed-from-windows-hosting-bundle)
- [Hosting: Host ogólny ogranicza iniekcję konstruktora startowego](#hosting-generic-host-restricts-startup-constructor-injection)
- [Hosting: włączono przekierowywanie protokołu HTTPS dla aplikacji pozaprocesowych usług IIS](#hosting-https-redirection-enabled-for-iis-out-of-process-apps)
- [Hosting: zamieniono typy IHostingEnvironment i IApplicationLifetime](#hosting-ihostingenvironment-and-iapplicationlifetime-types-marked-obsolete-and-replaced)
- [Hosting: ObjectPoolProvider usunięte z zależności WebHostBuilder](#hosting-objectpoolprovider-removed-from-webhostbuilder-dependencies)
- [HTTP: zmiana SameSite w przeglądarce wpływa na uwierzytelnianie](#http-browser-samesite-changes-impact-authentication)
- [HTTP: Usunięto rozszerzalność DefaultHttpContext](#http-defaulthttpcontext-extensibility-removed)
- [HTTP: pola HeaderNames zostały zmienione na statyczny tylko do odczytu](#http-headernames-constants-changed-to-static-readonly)
- [HTTP: zmiany infrastruktury treści odpowiedzi](#http-response-body-infrastructure-changes)
- [HTTP: zmieniono domyślne wartości SameSite w pliku cookie](#http-some-cookie-samesite-defaults-changed-to-none)
- [HTTP: synchroniczne operacje we/wy są wyłączone domyślnie](#http-synchronous-io-disabled-in-all-servers)
- [Tożsamość: Usunięto Przeciążenie metody AddDefaultUI](#identity-adddefaultui-method-overload-removed)
- [Tożsamość: zmiana wersji ładowania początkowego interfejsu użytkownika](#identity-default-bootstrap-version-of-ui-changed)
- [Tożsamość: SignInAsync zgłasza wyjątek dla nieuwierzytelnionej tożsamości](#identity-signinasync-throws-exception-for-unauthenticated-identity)
- [Tożsamość: Konstruktor SignInManager akceptuje nowy parametr](#identity-signinmanager-constructor-accepts-new-parameter)
- [Tożsamość: interfejs użytkownika używa funkcji statyczne zasoby sieci Web](#identity-ui-uses-static-web-assets-feature)
- [Kestrel: Usunięto karty połączeń](#kestrel-connection-adapters-removed)
- [Kestrel: Usunięto pusty zestaw HTTPS](#kestrel-empty-https-assembly-removed)
- [Kestrel: przeniesiono nagłówki przyczepki do nowej kolekcji](#kestrel-request-trailer-headers-moved-to-new-collection)
- [Kestrel: transportowe zmiany warstwy abstrakcji](#kestrel-transport-abstractions-removed-and-made-public)
- [Lokalizacja: interfejsy API oznaczone jako przestarzałe](#localization-resourcemanagerwithculturestringlocalizer-and-withculture-marked-obsolete)
- [Rejestrowanie: Klasa DebugLogger wykonana wewnętrznie](#logging-debuglogger-class-made-internal)
- [MVC: Usunięto sufiks asynchroniczny akcji kontrolera](#mvc-async-suffix-trimmed-from-controller-action-names)
- [MVC: JsonResult przeniesiony do Microsoft. AspNetCore. MVC. Core](#mvc-jsonresult-moved-to-microsoftaspnetcoremvccore)
- [MVC: Narzędzie wstępnej kompilacji zostało zaniechane](#mvc-precompilation-tool-deprecated)
- [MVC: zmieniono typy na wewnętrzne](#mvc-pubternal-types-changed-to-internal)
- [MVC: Usunięto podkładkę zgodności z interfejsem API sieci Web](#mvc-web-api-compatibility-shim-removed)
- [Razor: Usunięto interfejs API RazorTemplateEngine](#razor-razortemplateengine-api-removed)
- [Razor: Kompilacja środowiska uruchomieniowego została przeniesiona do pakietu](#razor-runtime-compilation-moved-to-a-package)
- [Stan sesji: Usunięto przestarzałe interfejsy API](#session-state-obsolete-apis-removed)
- [Współdzielona struktura: usuwanie zestawu z Microsoft. AspNetCore. App](#shared-framework-assemblies-removed-from-microsoftaspnetcoreapp)
- [Współdzielona struktura: Microsoft. AspNetCore. All usunięte](#shared-framework-removed-microsoftaspnetcoreall)
- [Sygnalizujący: HandshakeProtocol. SuccessHandshakeData został zastąpiony](#signalr-handshakeprotocolsuccesshandshakedata-replaced)
- [Sygnalizacja: Usunięto metody HubConnection](#signalr-hubconnection-resetsendping-and-resettimeout-methods-removed)
- [Sygnalizacja: zmieniono konstruktory HubConnectionContext](#signalr-hubconnectioncontext-constructors-changed)
- [Sygnalizacja: zmiana nazwy pakietu klienta języka JavaScript](#signalr-javascript-client-package-name-changed)
- [Sygnalizujący: przestarzałe interfejsy API](#signalr-usesignalr-and-useconnections-methods-marked-obsolete)
- [Aplikacji jednostronicowych: SpaServices i NodeServices domyślna zmiana ustawień rejestru](#spas-spaservices-and-nodeservices-no-longer-fall-back-to-console-logger)
- [Aplikacji jednostronicowych: SpaServices i NodeServices oznaczone jako przestarzałe](#spas-spaservices-and-nodeservices-marked-obsolete)
- [Platforma docelowa: nie .NET Framework obsługiwana](#target-framework-net-framework-support-dropped)

## <a name="aspnet-core-31"></a>ASP.NET Core 3,1

[!INCLUDE[HTTP: Browser SameSite changes impact authentication](~/includes/core-changes/aspnetcore/3.1/http-cookie-samesite-authn-impacts.md)]

***

## <a name="aspnet-core-30"></a>ASP.NET Core 3,0

[!INCLUDE[Obsolete Antiforgery, CORS, Diagnostics, MVC, and Routing APIs removed](~/includes/core-changes/aspnetcore/3.0/obsolete-apis-removed.md)]

**_

[!INCLUDE[Authentication: Google+ deprecation](~/includes/core-changes/aspnetcore/3.0/authn-google-plus-authn-changes.md)]

_*_

[!INCLUDE[Authentication: HttpContext.Authentication property removed](~/includes/core-changes/aspnetcore/3.0/authn-httpcontext-property-removed.md)]

_*_

[!INCLUDE[Authentication: Newtonsoft.Json types replaced](~/includes/core-changes/aspnetcore/3.0/authn-apis-json-types.md)]

_*_

[!INCLUDE[Authentication: OAuthHandler ExchangeCodeAsync signature changed](~/includes/core-changes/aspnetcore/3.0/authn-exchangecodeasync-signature-change.md)]

_*_

[!INCLUDE[Authorization: AddAuthorization overload assembly change](~/includes/core-changes/aspnetcore/3.0/authz-assembly-change.md)]

_*_

[!INCLUDE[Authorization: IAllowAnonymous removed from AuthorizationFilterContext.Filters](~/includes/core-changes/aspnetcore/3.0/authz-iallowanonymous-removed-from-collection.md)]

_*_

[!INCLUDE[Authorization: IAuthorizationPolicyProvider implementations require new method](~/includes/core-changes/aspnetcore/3.0/authz-iauthzpolicyprovider-new-method.md)]

_*_

[!INCLUDE[Caching: CompactOnMemoryPressure property removed](~/includes/core-changes/aspnetcore/3.0/caching-memory-property-removed.md)]

_*_

[!INCLUDE[Caching: Microsoft.Extensions.Caching.SqlServer uses new SqlClient package](~/includes/core-changes/aspnetcore/3.0/caching-new-sqlclient-package.md)]

_*_

[!INCLUDE[Caching: ResponseCaching types changed to internal](~/includes/core-changes/aspnetcore/3.0/caching-response-pubternal-to-internal.md)]

_*_

[!INCLUDE[Data Protection: DataProtection.AzureStorage uses new Azure Storage APIs](~/includes/core-changes/aspnetcore/3.0/dataprotection-azstorage-using-azstorage-apis.md)]

_*_

[!INCLUDE[Hosting: ANCM version 1 removed from hosting bundle](~/includes/core-changes/aspnetcore/3.0/hosting-ancmv1-hosting-bundle-removal.md)]

_*_

[!INCLUDE[Hosting: Generic host restriction on Startup constructor injection](~/includes/core-changes/aspnetcore/3.0/hosting-generic-host-startup-ctor-restriction.md)]

_*_

[!INCLUDE[Hosting: HTTPS redirection enabled for IIS OutOfProcess](~/includes/core-changes/aspnetcore/3.0/hosting-https-redirection-iis-outofprocess.md)]

_*_

[!INCLUDE[Hosting: IHostingEnvironment and IApplicationLifetime types replaced](~/includes/core-changes/aspnetcore/3.0/hosting-ihostingenv-iapplifetime-types-replaced.md)]

_*_

[!INCLUDE[Hosting: ObjectPoolProvider removed from WebHostBuilder dependencies](~/includes/core-changes/aspnetcore/3.0/hosting-objectpoolprovider-webhostbuilder-dependencies.md)]

_*_

[!INCLUDE[HTTP: DefaultHttpContext extensibility removed](~/includes/core-changes/aspnetcore/3.0/http-defaulthttpcontext-extensibility-removed.md)]

_*_

[!INCLUDE[HTTP: HeaderNames fields changed to static readonly](~/includes/core-changes/aspnetcore/3.0/http-headernames-constants-staticreadonly.md)]

_*_

[!INCLUDE[HTTP: Response body infrastructure changes](~/includes/core-changes/aspnetcore/3.0/http-response-body-changes.md)]

_*_

[!INCLUDE[HTTP: Some cookie SameSite default values changed](~/includes/core-changes/aspnetcore/3.0/http-cookie-samesite-defaults-change.md)]

_*_

[!INCLUDE[HTTP: Synchronous IO disabled by default](~/includes/core-changes/aspnetcore/3.0/http-synchronous-io-disabled.md)]

_*_

[!INCLUDE[Identity: AddDefaultUI method overload removed](~/includes/core-changes/aspnetcore/3.0/identity-ui-adddefaultui-overload-removed.md)]

_*_

[!INCLUDE[Identity: UI Bootstrap version change](~/includes/core-changes/aspnetcore/3.0/identity-ui-bootstrap-version.md)]

_*_

[!INCLUDE[Identity: SignInAsync throws exception for unauthenticated identity](~/includes/core-changes/aspnetcore/3.0/identity-signinasync-throws-exception.md)]

_*_

[!INCLUDE[Identity: SignInManager constructor accepts new parameter](~/includes/core-changes/aspnetcore/3.0/identity-signinmanager-ctor-parameter.md)]

_*_

[!INCLUDE[Identity: UI uses static web assets feature](~/includes/core-changes/aspnetcore/3.0/identity-ui-static-web-assets.md)]

_*_

[!INCLUDE[Kestrel: Connection adapters removed](~/includes/core-changes/aspnetcore/3.0/kestrel-connection-adapters-removed.md)]

_*_

[!INCLUDE[Kestrel: Empty HTTPS assembly removed](~/includes/core-changes/aspnetcore/3.0/kestrel-empty-assembly-removed.md)]

_*_

[!INCLUDE[Kestrel: Request trailer headers moved to new collection](~/includes/core-changes/aspnetcore/3.0/kestrel-request-trailer-headers.md)]

_*_

[!INCLUDE[Kestrel: Transport abstraction layer changes](~/includes/core-changes/aspnetcore/3.0/kestrel-transport-abstractions.md)]

_*_

[!INCLUDE[Localization: APIs marked obsolete](~/includes/core-changes/aspnetcore/3.0/localization-apis-marked-obsolete.md)]

_*_

[!INCLUDE[Logging: DebugLogger class made internal](~/includes/core-changes/aspnetcore/3.0/logging-debuglogger-to-internal.md)]

_*_

[!INCLUDE[MVC: Controller action Async suffix removed](~/includes/core-changes/aspnetcore/3.0/mvc-action-async-suffix-trimmed.md)]

_*_

[!INCLUDE[MVC: JsonResult moved to Microsoft.AspNetCore.Mvc.Core](~/includes/core-changes/aspnetcore/3.0/mvc-jsonresult-moved.md)]

_*_

[!INCLUDE[MVC: Precompilation tool deprecated](~/includes/core-changes/aspnetcore/3.0/mvc-precompilation-tool-deprecated.md)]

_*_

[!INCLUDE[MVC: Types changed to internal](~/includes/core-changes/aspnetcore/3.0/mvc-pubternal-to-internal.md)]

_*_

[!INCLUDE[MVC: Web API compatibility shim removed](~/includes/core-changes/aspnetcore/3.0/mvc-webapi-compat-shim-removed.md)]

_*_

[!INCLUDE[Razor: RazorTemplatEengine API removed](~/includes/core-changes/aspnetcore/3.0/razor-razortemplateengine-api-removed.md)]

_*_

[!INCLUDE[Razor: Runtime compilation moved to a package](~/includes/core-changes/aspnetcore/3.0/razor-runtime-compilation-package.md)]

_*_

[!INCLUDE[Session state: Obsolete APIs removed](~/includes/core-changes/aspnetcore/3.0/session-obsolete-apis-removed.md)]

_*_

[!INCLUDE[Shared framework: Assembly removal from Microsoft.AspNetCore.App](~/includes/core-changes/aspnetcore/3.0/sharedfx-app-shared-framework-assemblies.md)]

_*_

[!INCLUDE[Shared framework: Microsoft.AspNetCore.All removed](~/includes/core-changes/aspnetcore/3.0/sharedfx-all-framework-removed.md)]

_*_

[!INCLUDE[SignalR: HandshakeProtocol.SuccessHandshakeData replaced](~/includes/core-changes/aspnetcore/3.0/signalr-successhandshakedata-replaced.md)]

_*_

[!INCLUDE[SignalR: HubConnection methods removed](~/includes/core-changes/aspnetcore/3.0/signalr-hubconnection-methods-removed.md)]

_*_

[!INCLUDE[SignalR: HubConnectionContext constructors changed](~/includes/core-changes/aspnetcore/3.0/signalr-hubconnectioncontext-ctors.md)]

_*_

[!INCLUDE[SignalR: JavaScript client package name change](~/includes/core-changes/aspnetcore/3.0/signalr-js-client-package-name.md)]

_*_

[!INCLUDE[SignalR: Obsolete APIs](~/includes/core-changes/aspnetcore/3.0/signalr-obsolete-apis.md)]

_*_

[!INCLUDE[SPAs: SpaServices and NodeServices marked obsolete](~/includes/core-changes/aspnetcore/3.0/spas-spaservices-nodeservices-obsolete.md)]

_*_

[!INCLUDE[SPAs: SpaServices and NodeServices console logger fallback default change](~/includes/core-changes/aspnetcore/3.0/spas-spaservices-nodeservices-fallback.md)]

_*_

[!INCLUDE[Target framework: .NET Framework not supported](~/includes/core-changes/aspnetcore/3.0/targetfx-netfx-tfm-support.md)]

_**
