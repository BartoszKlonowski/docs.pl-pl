---
title: ASP.NET Core istotne zmiany
titleSuffix: ''
description: Wyświetla listę istotnych zmian w ASP.NET Core.
ms.date: 08/20/2020
author: scottaddie
ms.author: scaddie
ms.openlocfilehash: 8b37ae5c5eea9e192a269092fccf435ab4877e61
ms.sourcegitcommit: b9122d1af21898eaba81e990c70fef46fef74a8d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88867675"
---
# <a name="aspnet-core-breaking-changes"></a><span data-ttu-id="223cb-103">ASP.NET Core istotne zmiany</span><span class="sxs-lookup"><span data-stu-id="223cb-103">ASP.NET Core breaking changes</span></span>

<span data-ttu-id="223cb-104">ASP.NET Core udostępnia funkcje deweloperskie aplikacji sieci Web używane przez platformę .NET Core.</span><span class="sxs-lookup"><span data-stu-id="223cb-104">ASP.NET Core provides the web app development features used by .NET Core.</span></span>

<span data-ttu-id="223cb-105">Wybierz jedno z poniższych linków, aby uzyskać istotne zmiany w określonej wersji:</span><span class="sxs-lookup"><span data-stu-id="223cb-105">Select one of the following links for breaking changes in a specific version:</span></span>

* [<span data-ttu-id="223cb-106">ASP.NET Core 5,0</span><span class="sxs-lookup"><span data-stu-id="223cb-106">ASP.NET Core 5.0</span></span>](#aspnet-core-50)
* [<span data-ttu-id="223cb-107">ASP.NET Core 3,1</span><span class="sxs-lookup"><span data-stu-id="223cb-107">ASP.NET Core 3.1</span></span>](#aspnet-core-31)
* [<span data-ttu-id="223cb-108">ASP.NET Core 3,0</span><span class="sxs-lookup"><span data-stu-id="223cb-108">ASP.NET Core 3.0</span></span>](#aspnet-core-30)

<span data-ttu-id="223cb-109">Następujące istotne zmiany w ASP.NET Core 3,0, 3,1 i 5,0 są udokumentowane na tej stronie:</span><span class="sxs-lookup"><span data-stu-id="223cb-109">The following breaking changes in ASP.NET Core 3.0, 3.1, and 5.0 are documented on this page:</span></span>

- [<span data-ttu-id="223cb-110">Usunięto przestarzałe interfejsy API "antysfałszowane", "CORS, Diagnostics, MVC i Routing"</span><span class="sxs-lookup"><span data-stu-id="223cb-110">Obsolete Antiforgery, CORS, Diagnostics, MVC, and Routing APIs removed</span></span>](#obsolete-antiforgery-cors-diagnostics-mvc-and-routing-apis-removed)
- [<span data-ttu-id="223cb-111">Uwierzytelnianie: Google + zaniechana</span><span class="sxs-lookup"><span data-stu-id="223cb-111">Authentication: Google+ deprecation</span></span>](#authentication-google-deprecated-and-replaced)
- [<span data-ttu-id="223cb-112">Uwierzytelnianie: Właściwość HttpContext. Authentication została usunięta</span><span class="sxs-lookup"><span data-stu-id="223cb-112">Authentication: HttpContext.Authentication property removed</span></span>](#authentication-httpcontextauthentication-property-removed)
- [<span data-ttu-id="223cb-113">Uwierzytelnianie: Newtonsoft.Jstypów zamieniono</span><span class="sxs-lookup"><span data-stu-id="223cb-113">Authentication: Newtonsoft.Json types replaced</span></span>](#authentication-newtonsoftjson-types-replaced)
- [<span data-ttu-id="223cb-114">Uwierzytelnianie: OAuthHandler ExchangeCodeAsync zmieniono sygnaturę</span><span class="sxs-lookup"><span data-stu-id="223cb-114">Authentication: OAuthHandler ExchangeCodeAsync signature changed</span></span>](#authentication-oauthhandler-exchangecodeasync-signature-changed)
- [<span data-ttu-id="223cb-115">Autoryzacja: Przeciążenie metody addauthorization przeniesiono do innego zestawu</span><span class="sxs-lookup"><span data-stu-id="223cb-115">Authorization: AddAuthorization overload moved to different assembly</span></span>](#authorization-addauthorization-overload-moved-to-different-assembly)
- [<span data-ttu-id="223cb-116">Autoryzacja: Usunięto IAllowAnonymous z AuthorizationFilterContext. filters</span><span class="sxs-lookup"><span data-stu-id="223cb-116">Authorization: IAllowAnonymous removed from AuthorizationFilterContext.Filters</span></span>](#authorization-iallowanonymous-removed-from-authorizationfiltercontextfilters)
- [<span data-ttu-id="223cb-117">Autoryzacja: implementacje IAuthorizationPolicyProvider wymagają nowej metody</span><span class="sxs-lookup"><span data-stu-id="223cb-117">Authorization: IAuthorizationPolicyProvider implementations require new method</span></span>](#authorization-iauthorizationpolicyprovider-implementations-require-new-method)
- [<span data-ttu-id="223cb-118">Autoryzacja: zasób w routingu punktu końcowego jest obiektem HttpContext</span><span class="sxs-lookup"><span data-stu-id="223cb-118">Authorization: Resource in endpoint routing is HttpContext</span></span>](#authorization-resource-in-endpoint-routing-is-httpcontext)
- [<span data-ttu-id="223cb-119">Azure: Usunięto wstępnie ustalone pakiety integracji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="223cb-119">Azure: Microsoft-prefixed Azure integration packages removed</span></span>](#azure-microsoft-prefixed-azure-integration-packages-removed)
- [<span data-ttu-id="223cb-120">Metody serializacji BinaryFormatter są przestarzałe i zabronione w aplikacjach ASP.NET</span><span class="sxs-lookup"><span data-stu-id="223cb-120">BinaryFormatter serialization methods are obsolete and prohibited in ASP.NET apps</span></span>](#binaryformatter-serialization-methods-are-obsolete-and-prohibited-in-aspnet-apps)
- [<span data-ttu-id="223cb-121">Blazor: nieznaczące odstępy są obcinane ze składników w czasie kompilacji</span><span class="sxs-lookup"><span data-stu-id="223cb-121">Blazor: Insignificant whitespace trimmed from components at compile time</span></span>](#blazor-insignificant-whitespace-trimmed-from-components-at-compile-time)
- [<span data-ttu-id="223cb-122">Blazor: zmieniono platformę docelową pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="223cb-122">Blazor: Target framework of NuGet packages changed</span></span>](#blazor-target-framework-of-nuget-packages-changed)
- [<span data-ttu-id="223cb-123">Buforowanie: Usunięto Właściwość CompactOnMemoryPressure</span><span class="sxs-lookup"><span data-stu-id="223cb-123">Caching: CompactOnMemoryPressure property removed</span></span>](#caching-compactonmemorypressure-property-removed)
- [<span data-ttu-id="223cb-124">Buforowanie: Microsoft. Extensions. buforowanie. SqlServer używa nowego pakietu SqlClient</span><span class="sxs-lookup"><span data-stu-id="223cb-124">Caching: Microsoft.Extensions.Caching.SqlServer uses new SqlClient package</span></span>](#caching-microsoftextensionscachingsqlserver-uses-new-sqlclient-package)
- [<span data-ttu-id="223cb-125">Buforowanie: typy ResponseCaching "pubternal" zostały zmienione na wewnętrzne</span><span class="sxs-lookup"><span data-stu-id="223cb-125">Caching: ResponseCaching "pubternal" types changed to internal</span></span>](#caching-responsecaching-pubternal-types-changed-to-internal)
- [<span data-ttu-id="223cb-126">Ochrona danych: usługa dataprotection. AzureStorage używa nowych interfejsów API usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="223cb-126">Data Protection: DataProtection.AzureStorage uses new Azure Storage APIs</span></span>](#data-protection-dataprotectionazurestorage-uses-new-azure-storage-apis)
- [<span data-ttu-id="223cb-127">Rozszerzenia: zmiany odwołania do pakietów wpływające na niektóre pakiety NuGet</span><span class="sxs-lookup"><span data-stu-id="223cb-127">Extensions: Package reference changes affecting some NuGet packages</span></span>](#extensions-package-reference-changes-affecting-some-nuget-packages)
- [<span data-ttu-id="223cb-128">Hosting: AspNetCoreModule V1 został usunięty z pakietu hostingu systemu Windows</span><span class="sxs-lookup"><span data-stu-id="223cb-128">Hosting: AspNetCoreModule V1 removed from Windows Hosting Bundle</span></span>](#hosting-aspnetcoremodule-v1-removed-from-windows-hosting-bundle)
- [<span data-ttu-id="223cb-129">Hosting: Host ogólny ogranicza iniekcję konstruktora startowego</span><span class="sxs-lookup"><span data-stu-id="223cb-129">Hosting: Generic host restricts Startup constructor injection</span></span>](#hosting-generic-host-restricts-startup-constructor-injection)
- [<span data-ttu-id="223cb-130">Hosting: włączono przekierowywanie protokołu HTTPS dla aplikacji pozaprocesowych usług IIS</span><span class="sxs-lookup"><span data-stu-id="223cb-130">Hosting: HTTPS redirection enabled for IIS out-of-process apps</span></span>](#hosting-https-redirection-enabled-for-iis-out-of-process-apps)
- [<span data-ttu-id="223cb-131">Hosting: zamieniono typy IHostingEnvironment i IApplicationLifetime</span><span class="sxs-lookup"><span data-stu-id="223cb-131">Hosting: IHostingEnvironment and IApplicationLifetime types replaced</span></span>](#hosting-ihostingenvironment-and-iapplicationlifetime-types-marked-obsolete-and-replaced)
- [<span data-ttu-id="223cb-132">Hosting: ObjectPoolProvider usunięte z zależności WebHostBuilder</span><span class="sxs-lookup"><span data-stu-id="223cb-132">Hosting: ObjectPoolProvider removed from WebHostBuilder dependencies</span></span>](#hosting-objectpoolprovider-removed-from-webhostbuilder-dependencies)
- [<span data-ttu-id="223cb-133">HTTP: Kestrel i IIS BadHttpRequestException typy oznaczone jako przestarzałe i zastąpione</span><span class="sxs-lookup"><span data-stu-id="223cb-133">HTTP: Kestrel and IIS BadHttpRequestException types marked obsolete and replaced</span></span>](#http-kestrel-and-iis-badhttprequestexception-types-marked-obsolete-and-replaced)
- [<span data-ttu-id="223cb-134">HTTP: zmiana SameSite w przeglądarce wpływa na uwierzytelnianie</span><span class="sxs-lookup"><span data-stu-id="223cb-134">HTTP: Browser SameSite changes impact authentication</span></span>](#http-browser-samesite-changes-impact-authentication)
- [<span data-ttu-id="223cb-135">HTTP: Usunięto rozszerzalność DefaultHttpContext</span><span class="sxs-lookup"><span data-stu-id="223cb-135">HTTP: DefaultHttpContext extensibility removed</span></span>](#http-defaulthttpcontext-extensibility-removed)
- [<span data-ttu-id="223cb-136">HTTP: pola HeaderNames zostały zmienione na statyczny tylko do odczytu</span><span class="sxs-lookup"><span data-stu-id="223cb-136">HTTP: HeaderNames fields changed to static readonly</span></span>](#http-headernames-constants-changed-to-static-readonly)
- [<span data-ttu-id="223cb-137">HTTP: wystąpienia HttpClient utworzone przez kody stanu liczby całkowitej dziennika IHttpClientFactory</span><span class="sxs-lookup"><span data-stu-id="223cb-137">HTTP: HttpClient instances created by IHttpClientFactory log integer status codes</span></span>](#http-httpclient-instances-created-by-ihttpclientfactory-log-integer-status-codes)
- [<span data-ttu-id="223cb-138">HTTP: zmiany infrastruktury treści odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="223cb-138">HTTP: Response body infrastructure changes</span></span>](#http-response-body-infrastructure-changes)
- [<span data-ttu-id="223cb-139">HTTP: zmieniono domyślne wartości SameSite w pliku cookie</span><span class="sxs-lookup"><span data-stu-id="223cb-139">HTTP: Some cookie SameSite default values changed</span></span>](#http-some-cookie-samesite-defaults-changed-to-none)
- [<span data-ttu-id="223cb-140">HTTP: synchroniczne operacje we/wy są wyłączone domyślnie</span><span class="sxs-lookup"><span data-stu-id="223cb-140">HTTP: Synchronous IO disabled by default</span></span>](#http-synchronous-io-disabled-in-all-servers)
- [<span data-ttu-id="223cb-141">HttpSys: ponowne negocjowanie certyfikatu klienta jest wyłączone domyślnie</span><span class="sxs-lookup"><span data-stu-id="223cb-141">HttpSys: Client certificate renegotiation disabled by default</span></span>](#httpsys-client-certificate-renegotiation-disabled-by-default)
- [<span data-ttu-id="223cb-142">Tożsamość: Usunięto Przeciążenie metody AddDefaultUI</span><span class="sxs-lookup"><span data-stu-id="223cb-142">Identity: AddDefaultUI method overload removed</span></span>](#identity-adddefaultui-method-overload-removed)
- [<span data-ttu-id="223cb-143">Tożsamość: zmiana wersji ładowania początkowego interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="223cb-143">Identity: UI Bootstrap version change</span></span>](#identity-default-bootstrap-version-of-ui-changed)
- [<span data-ttu-id="223cb-144">Tożsamość: SignInAsync zgłasza wyjątek dla nieuwierzytelnionej tożsamości</span><span class="sxs-lookup"><span data-stu-id="223cb-144">Identity: SignInAsync throws exception for unauthenticated identity</span></span>](#identity-signinasync-throws-exception-for-unauthenticated-identity)
- [<span data-ttu-id="223cb-145">Tożsamość: Konstruktor SignInManager akceptuje nowy parametr</span><span class="sxs-lookup"><span data-stu-id="223cb-145">Identity: SignInManager constructor accepts new parameter</span></span>](#identity-signinmanager-constructor-accepts-new-parameter)
- [<span data-ttu-id="223cb-146">Tożsamość: interfejs użytkownika używa funkcji statyczne zasoby sieci Web</span><span class="sxs-lookup"><span data-stu-id="223cb-146">Identity: UI uses static web assets feature</span></span>](#identity-ui-uses-static-web-assets-feature)
- [<span data-ttu-id="223cb-147">IIS: UrlRewrite ciągi zapytania oprogramowania pośredniczącego są zachowywane</span><span class="sxs-lookup"><span data-stu-id="223cb-147">IIS: UrlRewrite middleware query strings are preserved</span></span>](#iis-urlrewrite-middleware-query-strings-are-preserved)
- [<span data-ttu-id="223cb-148">Kestrel: domyślnie wykryto zmiany konfiguracji w czasie wykonywania</span><span class="sxs-lookup"><span data-stu-id="223cb-148">Kestrel: Configuration changes at run time detected by default</span></span>](#kestrel-configuration-changes-at-run-time-detected-by-default)
- [<span data-ttu-id="223cb-149">Kestrel: Usunięto karty połączeń</span><span class="sxs-lookup"><span data-stu-id="223cb-149">Kestrel: Connection adapters removed</span></span>](#kestrel-connection-adapters-removed)
- [<span data-ttu-id="223cb-150">Kestrel: zmieniono domyślne wersje protokołu TLS</span><span class="sxs-lookup"><span data-stu-id="223cb-150">Kestrel: Default supported TLS protocol versions changed</span></span>](#kestrel-default-supported-tls-protocol-versions-changed)
- [<span data-ttu-id="223cb-151">Kestrel: Usunięto pusty zestaw HTTPS</span><span class="sxs-lookup"><span data-stu-id="223cb-151">Kestrel: Empty HTTPS assembly removed</span></span>](#kestrel-empty-https-assembly-removed)
- [<span data-ttu-id="223cb-152">Kestrel: protokół HTTP/2 został wyłączony przy użyciu protokołu TLS dla niezgodnych wersji systemu Windows</span><span class="sxs-lookup"><span data-stu-id="223cb-152">Kestrel: HTTP/2 disabled over TLS on incompatible Windows versions</span></span>](#kestrel-http2-disabled-over-tls-on-incompatible-windows-versions)
- [<span data-ttu-id="223cb-153">Kestrel: transport Libuv oznaczony jako przestarzały</span><span class="sxs-lookup"><span data-stu-id="223cb-153">Kestrel: Libuv transport marked as obsolete</span></span>](#kestrel-libuv-transport-marked-as-obsolete)
- [<span data-ttu-id="223cb-154">Kestrel: przeniesiono nagłówki przyczepki do nowej kolekcji</span><span class="sxs-lookup"><span data-stu-id="223cb-154">Kestrel: Request trailer headers moved to new collection</span></span>](#kestrel-request-trailer-headers-moved-to-new-collection)
- [<span data-ttu-id="223cb-155">Kestrel: transportowe zmiany warstwy abstrakcji</span><span class="sxs-lookup"><span data-stu-id="223cb-155">Kestrel: Transport abstraction layer changes</span></span>](#kestrel-transport-abstractions-removed-and-made-public)
- [<span data-ttu-id="223cb-156">Lokalizacja: interfejsy API oznaczone jako przestarzałe</span><span class="sxs-lookup"><span data-stu-id="223cb-156">Localization: APIs marked obsolete</span></span>](#localization-resourcemanagerwithculturestringlocalizer-and-withculture-marked-obsolete)
- [<span data-ttu-id="223cb-157">Lokalizacja: Usunięto interfejsy API "Pubternal"</span><span class="sxs-lookup"><span data-stu-id="223cb-157">Localization: "Pubternal" APIs removed</span></span>](#localization-pubternal-apis-removed)
- [<span data-ttu-id="223cb-158">Lokalizacja: przestarzały Konstruktor został usunięty z oprogramowania pośredniczącego w lokalizacji żądania</span><span class="sxs-lookup"><span data-stu-id="223cb-158">Localization: Obsolete constructor removed in request localization middleware</span></span>](#localization-obsolete-constructor-removed-in-request-localization-middleware)
- [<span data-ttu-id="223cb-159">Lokalizacja: Usunięto klasę ResourceManagerWithCultureStringLocalizer i element członkowski interfejsu WithCulture</span><span class="sxs-lookup"><span data-stu-id="223cb-159">Localization: ResourceManagerWithCultureStringLocalizer class and WithCulture interface member removed</span></span>](#localization-resourcemanagerwithculturestringlocalizer-class-and-withculture-interface-member-removed)
- [<span data-ttu-id="223cb-160">Rejestrowanie: Klasa DebugLogger wykonana wewnętrznie</span><span class="sxs-lookup"><span data-stu-id="223cb-160">Logging: DebugLogger class made internal</span></span>](#logging-debuglogger-class-made-internal)
- [<span data-ttu-id="223cb-161">Oprogramowanie pośredniczące: Strona błędu bazy danych oznaczona jako przestarzała</span><span class="sxs-lookup"><span data-stu-id="223cb-161">Middleware: Database error page marked as obsolete</span></span>](#middleware-database-error-page-marked-as-obsolete)
- [<span data-ttu-id="223cb-162">MVC: Usunięto sufiks asynchroniczny akcji kontrolera</span><span class="sxs-lookup"><span data-stu-id="223cb-162">MVC: Controller action Async suffix removed</span></span>](#mvc-async-suffix-trimmed-from-controller-action-names)
- [<span data-ttu-id="223cb-163">MVC: JsonResult przeniesiony do Microsoft. AspNetCore. MVC. Core</span><span class="sxs-lookup"><span data-stu-id="223cb-163">MVC: JsonResult moved to Microsoft.AspNetCore.Mvc.Core</span></span>](#mvc-jsonresult-moved-to-microsoftaspnetcoremvccore)
- [<span data-ttu-id="223cb-164">MVC: Narzędzie wstępnej kompilacji zostało zaniechane</span><span class="sxs-lookup"><span data-stu-id="223cb-164">MVC: Precompilation tool deprecated</span></span>](#mvc-precompilation-tool-deprecated)
- [<span data-ttu-id="223cb-165">MVC: zmieniono typy na wewnętrzne</span><span class="sxs-lookup"><span data-stu-id="223cb-165">MVC: Types changed to internal</span></span>](#mvc-pubternal-types-changed-to-internal)
- [<span data-ttu-id="223cb-166">MVC: Usunięto podkładkę zgodności z interfejsem API sieci Web</span><span class="sxs-lookup"><span data-stu-id="223cb-166">MVC: Web API compatibility shim removed</span></span>](#mvc-web-api-compatibility-shim-removed)
- [<span data-ttu-id="223cb-167">Razor: Kompilacja środowiska uruchomieniowego została przeniesiona do pakietu</span><span class="sxs-lookup"><span data-stu-id="223cb-167">Razor: Runtime compilation moved to a package</span></span>](#razor-runtime-compilation-moved-to-a-package)
- [<span data-ttu-id="223cb-168">Zabezpieczenia: kodowanie nazwy pliku cookie zostało usunięte</span><span class="sxs-lookup"><span data-stu-id="223cb-168">Security: Cookie name encoding removed</span></span>](#security-cookie-name-encoding-removed)
- [<span data-ttu-id="223cb-169">Bezpieczeństwo: Zaktualizowano wersje pakietów NuGet IdentityModel</span><span class="sxs-lookup"><span data-stu-id="223cb-169">Security: IdentityModel NuGet package versions updated</span></span>](#security-identitymodel-nuget-package-versions-updated)
- [<span data-ttu-id="223cb-170">Stan sesji: Usunięto przestarzałe interfejsy API</span><span class="sxs-lookup"><span data-stu-id="223cb-170">Session state: Obsolete APIs removed</span></span>](#session-state-obsolete-apis-removed)
- [<span data-ttu-id="223cb-171">Współdzielona struktura: usuwanie zestawu z Microsoft. AspNetCore. App</span><span class="sxs-lookup"><span data-stu-id="223cb-171">Shared framework: Assembly removal from Microsoft.AspNetCore.App</span></span>](#shared-framework-assemblies-removed-from-microsoftaspnetcoreapp)
- [<span data-ttu-id="223cb-172">Współdzielona struktura: Microsoft. AspNetCore. All usunięte</span><span class="sxs-lookup"><span data-stu-id="223cb-172">Shared framework: Microsoft.AspNetCore.All removed</span></span>](#shared-framework-removed-microsoftaspnetcoreall)
- [<span data-ttu-id="223cb-173">Sygnalizujący: HandshakeProtocol. SuccessHandshakeData został zastąpiony</span><span class="sxs-lookup"><span data-stu-id="223cb-173">SignalR: HandshakeProtocol.SuccessHandshakeData replaced</span></span>](#signalr-handshakeprotocolsuccesshandshakedata-replaced)
- [<span data-ttu-id="223cb-174">Sygnalizacja: Usunięto metody HubConnection</span><span class="sxs-lookup"><span data-stu-id="223cb-174">SignalR: HubConnection methods removed</span></span>](#signalr-hubconnection-resetsendping-and-resettimeout-methods-removed)
- [<span data-ttu-id="223cb-175">Sygnalizacja: zmieniono konstruktory HubConnectionContext</span><span class="sxs-lookup"><span data-stu-id="223cb-175">SignalR: HubConnectionContext constructors changed</span></span>](#signalr-hubconnectioncontext-constructors-changed)
- [<span data-ttu-id="223cb-176">Sygnalizacja: zmiana nazwy pakietu klienta języka JavaScript</span><span class="sxs-lookup"><span data-stu-id="223cb-176">SignalR: JavaScript client package name change</span></span>](#signalr-javascript-client-package-name-changed)
- [<span data-ttu-id="223cb-177">Sygnalizacja: przeniesiono protokół MessagePack Hub do pakietu MessagePack 2. x</span><span class="sxs-lookup"><span data-stu-id="223cb-177">SignalR: MessagePack Hub Protocol moved to MessagePack 2.x package</span></span>](#signalr-messagepack-hub-protocol-moved-to-messagepack-2x-package)
- [<span data-ttu-id="223cb-178">Sygnalizacja: Zmieniono typ opcji protokołu MessagePack Hub</span><span class="sxs-lookup"><span data-stu-id="223cb-178">SignalR: MessagePack Hub Protocol options type changed</span></span>](#signalr-messagepack-hub-protocol-options-type-changed)
- [<span data-ttu-id="223cb-179">Sygnalizujący: przestarzałe interfejsy API</span><span class="sxs-lookup"><span data-stu-id="223cb-179">SignalR: Obsolete APIs</span></span>](#signalr-usesignalr-and-useconnections-methods-marked-obsolete)
- [<span data-ttu-id="223cb-180">Sygnalizacja: Usunięto metody UseSignalR i UseConnections</span><span class="sxs-lookup"><span data-stu-id="223cb-180">SignalR: UseSignalR and UseConnections methods removed</span></span>](#signalr-usesignalr-and-useconnections-methods-removed)
- [<span data-ttu-id="223cb-181">Aplikacji jednostronicowych: SpaServices i NodeServices domyślna zmiana ustawień rejestru</span><span class="sxs-lookup"><span data-stu-id="223cb-181">SPAs: SpaServices and NodeServices console logger fallback default change</span></span>](#spas-spaservices-and-nodeservices-no-longer-fall-back-to-console-logger)
- [<span data-ttu-id="223cb-182">Aplikacji jednostronicowych: SpaServices i NodeServices oznaczone jako przestarzałe</span><span class="sxs-lookup"><span data-stu-id="223cb-182">SPAs: SpaServices and NodeServices marked obsolete</span></span>](#spas-spaservices-and-nodeservices-marked-obsolete)
- [<span data-ttu-id="223cb-183">Pliki statyczne: typ zawartości CSV został zmieniony na zgodny ze standardami</span><span class="sxs-lookup"><span data-stu-id="223cb-183">Static files: CSV content type changed to standards-compliant</span></span>](#static-files-csv-content-type-changed-to-standards-compliant)
- [<span data-ttu-id="223cb-184">Platforma docelowa: nie .NET Framework obsługiwana</span><span class="sxs-lookup"><span data-stu-id="223cb-184">Target framework: .NET Framework not supported</span></span>](#target-framework-net-framework-support-dropped)

## <a name="aspnet-core-50"></a><span data-ttu-id="223cb-185">ASP.NET Core 5,0</span><span class="sxs-lookup"><span data-stu-id="223cb-185">ASP.NET Core 5.0</span></span>

[!INCLUDE[Authorization: Resource in endpoint routing is HttpContext](~/includes/core-changes/aspnetcore/5.0/authorization-resource-in-endpoint-routing.md)]

***

[!INCLUDE[Azure: Microsoft-prefixed Azure integration packages removed](~/includes/core-changes/aspnetcore/5.0/azure-integration-packages-removed.md)]

***

[!INCLUDE [binaryformatter-serialization-obsolete](../../../includes/core-changes/corefx/5.0/binaryformatter-serialization-obsolete.md)]

***

[!INCLUDE[Blazor: Insignificant whitespace trimmed from components at compile time](~/includes/core-changes/aspnetcore/5.0/blazor-components-trim-insignificant-whitespace.md)]

***

[!INCLUDE[Blazor: Target framework of NuGet packages changed](~/includes/core-changes/aspnetcore/5.0/blazor-packages-target-framework-changed.md)]

***

[!INCLUDE[Extensions: Package reference changes](~/includes/core-changes/aspnetcore/5.0/extensions-package-reference-changes.md)]

***

[!INCLUDE[HTTP: HttpClient instances created by IHttpClientFactory log integer status codes](~/includes/core-changes/aspnetcore/5.0/http-httpclient-instances-log-integer-status-codes.md)]

***

[!INCLUDE[HTTP: Kestrel and IIS BadHttpRequestException types marked obsolete and replaced](~/includes/core-changes/aspnetcore/5.0/http-badhttprequestexception-obsolete.md)]

***

[!INCLUDE[HttpSys: Client certificate renegotiation disabled by default](~/includes/core-changes/aspnetcore/5.0/httpsys-client-certificate-renegotiation-disabled-by-default.md)]

***

[!INCLUDE[IIS: UrlRewrite middleware query strings are preserved](~/includes/core-changes/aspnetcore/5.0/iis-urlrewrite-middleware-query-strings-are-preserved.md)]

***

[!INCLUDE[Kestrel: Configuration changes at run time detected by default](~/includes/core-changes/aspnetcore/5.0/kestrel-configuration-changes-at-run-time-detected-by-default.md)]

***
[!INCLUDE[Kestrel: Default supported TLS protocol versions changed](~/includes/core-changes/aspnetcore/5.0/kestrel-default-supported-tls-protocol-versions-changed.md)]

***

[!INCLUDE[Kestrel: HTTP/2 disabled over TLS on incompatible Windows versions](~/includes/core-changes/aspnetcore/5.0/kestrel-disables-http2-over-tls.md)]

***

[!INCLUDE[Kestrel: Libuv transport marked as obsolete](~/includes/core-changes/aspnetcore/5.0/kestrel-libuv-transport-obsolete.md)]

***

[!INCLUDE[Localization: "Pubternal" APIs removed](~/includes/core-changes/aspnetcore/5.0/localization-pubternal-apis-removed.md)]

***

[!INCLUDE[Localization: Obsolete constructor removed in request localization middleware](~/includes/core-changes/aspnetcore/5.0/localization-requestlocalizationmiddleware-constructor-removed.md)]

***

[!INCLUDE[Localization: ResourceManagerWithCultureStringLocalizer class and WithCulture interface member removed](~/includes/core-changes/aspnetcore/5.0/localization-members-removed.md)]

***

[!INCLUDE[Middleware: Database error page marked as obsolete](~/includes/core-changes/aspnetcore/5.0/middleware-database-error-page-obsolete.md)]

***

[!INCLUDE[Security: Cookie name encoding removed](~/includes/core-changes/aspnetcore/5.0/security-cookie-name-encoding-removed.md)]

***

[!INCLUDE[Security: IdentityModel NuGet package versions updated](~/includes/core-changes/aspnetcore/5.0/security-identitymodel-nuget-package-versions-updated.md)]

***

[!INCLUDE[SignalR: MessagePack Hub Protocol moved to MessagePack 2.x package](~/includes/core-changes/aspnetcore/5.0/signalr-messagepack-package.md)]

***

[!INCLUDE[SignalR: MessagePack Hub Protocol options type changed](~/includes/core-changes/aspnetcore/5.0/signalr-messagepack-hub-protocol-options-changed.md)]

***

[!INCLUDE[SignalR: UseSignalR and UseConnections methods removed](~/includes/core-changes/aspnetcore/5.0/signalr-usesignalr-useconnections-removed.md)]

***

[!INCLUDE[Static files: CSV content type changed to standards-compliant](~/includes/core-changes/aspnetcore/5.0/static-files-csv-content-type-changed.md)]

***

## <a name="aspnet-core-31"></a><span data-ttu-id="223cb-186">ASP.NET Core 3,1</span><span class="sxs-lookup"><span data-stu-id="223cb-186">ASP.NET Core 3.1</span></span>

[!INCLUDE[HTTP: Browser SameSite changes impact authentication](~/includes/core-changes/aspnetcore/3.1/http-cookie-samesite-authn-impacts.md)]

***

## <a name="aspnet-core-30"></a><span data-ttu-id="223cb-187">ASP.NET Core 3,0</span><span class="sxs-lookup"><span data-stu-id="223cb-187">ASP.NET Core 3.0</span></span>

[!INCLUDE[Obsolete Antiforgery, CORS, Diagnostics, MVC, and Routing APIs removed](~/includes/core-changes/aspnetcore/3.0/obsolete-apis-removed.md)]

***

[!INCLUDE[Authentication: Google+ deprecation](~/includes/core-changes/aspnetcore/3.0/authn-google-plus-authn-changes.md)]

***

[!INCLUDE[Authentication: HttpContext.Authentication property removed](~/includes/core-changes/aspnetcore/3.0/authn-httpcontext-property-removed.md)]

***

[!INCLUDE[Authentication: Newtonsoft.Json types replaced](~/includes/core-changes/aspnetcore/3.0/authn-apis-json-types.md)]

***

[!INCLUDE[Authentication: OAuthHandler ExchangeCodeAsync signature changed](~/includes/core-changes/aspnetcore/3.0/authn-exchangecodeasync-signature-change.md)]

***

[!INCLUDE[Authorization: AddAuthorization overload assembly change](~/includes/core-changes/aspnetcore/3.0/authz-assembly-change.md)]

***

[!INCLUDE[Authorization: IAllowAnonymous removed from AuthorizationFilterContext.Filters](~/includes/core-changes/aspnetcore/3.0/authz-iallowanonymous-removed-from-collection.md)]

***

[!INCLUDE[Authorization: IAuthorizationPolicyProvider implementations require new method](~/includes/core-changes/aspnetcore/3.0/authz-iauthzpolicyprovider-new-method.md)]

***

[!INCLUDE[Caching: CompactOnMemoryPressure property removed](~/includes/core-changes/aspnetcore/3.0/caching-memory-property-removed.md)]

***

[!INCLUDE[Caching: Microsoft.Extensions.Caching.SqlServer uses new SqlClient package](~/includes/core-changes/aspnetcore/3.0/caching-new-sqlclient-package.md)]

***

[!INCLUDE[Caching: ResponseCaching types changed to internal](~/includes/core-changes/aspnetcore/3.0/caching-response-pubternal-to-internal.md)]

***

[!INCLUDE[Data Protection: DataProtection.AzureStorage uses new Azure Storage APIs](~/includes/core-changes/aspnetcore/3.0/dataprotection-azstorage-using-azstorage-apis.md)]

***

[!INCLUDE[Hosting: ANCM version 1 removed from hosting bundle](~/includes/core-changes/aspnetcore/3.0/hosting-ancmv1-hosting-bundle-removal.md)]

***

[!INCLUDE[Hosting: Generic host restriction on Startup constructor injection](~/includes/core-changes/aspnetcore/3.0/hosting-generic-host-startup-ctor-restriction.md)]

***

[!INCLUDE[Hosting: HTTPS redirection enabled for IIS OutOfProcess](~/includes/core-changes/aspnetcore/3.0/hosting-https-redirection-iis-outofprocess.md)]

***

[!INCLUDE[Hosting: IHostingEnvironment and IApplicationLifetime types replaced](~/includes/core-changes/aspnetcore/3.0/hosting-ihostingenv-iapplifetime-types-replaced.md)]

***

[!INCLUDE[Hosting: ObjectPoolProvider removed from WebHostBuilder dependencies](~/includes/core-changes/aspnetcore/3.0/hosting-objectpoolprovider-webhostbuilder-dependencies.md)]

***

[!INCLUDE[HTTP: DefaultHttpContext extensibility removed](~/includes/core-changes/aspnetcore/3.0/http-defaulthttpcontext-extensibility-removed.md)]

***

[!INCLUDE[HTTP: HeaderNames fields changed to static readonly](~/includes/core-changes/aspnetcore/3.0/http-headernames-constants-staticreadonly.md)]

***

[!INCLUDE[HTTP: Response body infrastructure changes](~/includes/core-changes/aspnetcore/3.0/http-response-body-changes.md)]

***

[!INCLUDE[HTTP: Some cookie SameSite default values changed](~/includes/core-changes/aspnetcore/3.0/http-cookie-samesite-defaults-change.md)]

***

[!INCLUDE[HTTP: Synchronous IO disabled by default](~/includes/core-changes/aspnetcore/3.0/http-synchronous-io-disabled.md)]

***

[!INCLUDE[Identity: AddDefaultUI method overload removed](~/includes/core-changes/aspnetcore/3.0/identity-ui-adddefaultui-overload-removed.md)]

***

[!INCLUDE[Identity: UI Bootstrap version change](~/includes/core-changes/aspnetcore/3.0/identity-ui-bootstrap-version.md)]

***

[!INCLUDE[Identity: SignInAsync throws exception for unauthenticated identity](~/includes/core-changes/aspnetcore/3.0/identity-signinasync-throws-exception.md)]

***

[!INCLUDE[Identity: SignInManager constructor accepts new parameter](~/includes/core-changes/aspnetcore/3.0/identity-signinmanager-ctor-parameter.md)]

***

[!INCLUDE[Identity: UI uses static web assets feature](~/includes/core-changes/aspnetcore/3.0/identity-ui-static-web-assets.md)]

***

[!INCLUDE[Kestrel: Connection adapters removed](~/includes/core-changes/aspnetcore/3.0/kestrel-connection-adapters-removed.md)]

***

[!INCLUDE[Kestrel: Empty HTTPS assembly removed](~/includes/core-changes/aspnetcore/3.0/kestrel-empty-assembly-removed.md)]

***

[!INCLUDE[Kestrel: Request trailer headers moved to new collection](~/includes/core-changes/aspnetcore/3.0/kestrel-request-trailer-headers.md)]

***

[!INCLUDE[Kestrel: Transport abstraction layer changes](~/includes/core-changes/aspnetcore/3.0/kestrel-transport-abstractions.md)]

***

[!INCLUDE[Localization: APIs marked obsolete](~/includes/core-changes/aspnetcore/3.0/localization-apis-marked-obsolete.md)]

***

[!INCLUDE[Logging: DebugLogger class made internal](~/includes/core-changes/aspnetcore/3.0/logging-debuglogger-to-internal.md)]

***

[!INCLUDE[MVC: Controller action Async suffix removed](~/includes/core-changes/aspnetcore/3.0/mvc-action-async-suffix-trimmed.md)]

***

[!INCLUDE[MVC: JsonResult moved to Microsoft.AspNetCore.Mvc.Core](~/includes/core-changes/aspnetcore/3.0/mvc-jsonresult-moved.md)]

***

[!INCLUDE[MVC: Precompilation tool deprecated](~/includes/core-changes/aspnetcore/3.0/mvc-precompilation-tool-deprecated.md)]

***

[!INCLUDE[MVC: Types changed to internal](~/includes/core-changes/aspnetcore/3.0/mvc-pubternal-to-internal.md)]

***

[!INCLUDE[MVC: Web API compatibility shim removed](~/includes/core-changes/aspnetcore/3.0/mvc-webapi-compat-shim-removed.md)]

***

[!INCLUDE[Razor: Runtime compilation moved to a package](~/includes/core-changes/aspnetcore/3.0/razor-runtime-compilation-package.md)]

***

[!INCLUDE[Session state: Obsolete APIs removed](~/includes/core-changes/aspnetcore/3.0/session-obsolete-apis-removed.md)]

***

[!INCLUDE[Shared framework: Assembly removal from Microsoft.AspNetCore.App](~/includes/core-changes/aspnetcore/3.0/sharedfx-app-shared-framework-assemblies.md)]

***

[!INCLUDE[Shared framework: Microsoft.AspNetCore.All removed](~/includes/core-changes/aspnetcore/3.0/sharedfx-all-framework-removed.md)]

***

[!INCLUDE[SignalR: HandshakeProtocol.SuccessHandshakeData replaced](~/includes/core-changes/aspnetcore/3.0/signalr-successhandshakedata-replaced.md)]

***

[!INCLUDE[SignalR: HubConnection methods removed](~/includes/core-changes/aspnetcore/3.0/signalr-hubconnection-methods-removed.md)]

***

[!INCLUDE[SignalR: HubConnectionContext constructors changed](~/includes/core-changes/aspnetcore/3.0/signalr-hubconnectioncontext-ctors.md)]

***

[!INCLUDE[SignalR: JavaScript client package name change](~/includes/core-changes/aspnetcore/3.0/signalr-js-client-package-name.md)]

***

[!INCLUDE[SignalR: Obsolete APIs](~/includes/core-changes/aspnetcore/3.0/signalr-obsolete-apis.md)]

***

[!INCLUDE[SPAs: SpaServices and NodeServices marked obsolete](~/includes/core-changes/aspnetcore/3.0/spas-spaservices-nodeservices-obsolete.md)]

***

[!INCLUDE[SPAs: SpaServices and NodeServices console logger fallback default change](~/includes/core-changes/aspnetcore/3.0/spas-spaservices-nodeservices-fallback.md)]

***

[!INCLUDE[Target framework: .NET Framework not supported](~/includes/core-changes/aspnetcore/3.0/targetfx-netfx-tfm-support.md)]

***
