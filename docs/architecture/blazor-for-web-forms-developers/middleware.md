---
title: Moduły, programy obsługi i oprogramowanie pośredniczące
description: Dowiedz się więcej na temat obsługi żądań HTTP za pomocą modułów, programów obsługi i oprogramowania pośredniczącego.
author: danroth27
ms.author: daroth
no-loc:
- Blazor
ms.date: 10/11/2019
ms.openlocfilehash: 639755dd78892df1b70ea5245a9584e575fbf691
ms.sourcegitcommit: 0100be20fcf23f61dab672deced70059ed71bb2e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/17/2020
ms.locfileid: "88267883"
---
# <a name="modules-handlers-and-middleware"></a><span data-ttu-id="58301-103">Moduły, programy obsługi i oprogramowanie pośredniczące</span><span class="sxs-lookup"><span data-stu-id="58301-103">Modules, handlers, and middleware</span></span>

<span data-ttu-id="58301-104">Aplikacja ASP.NET Core jest oparta na serii *oprogramowania pośredniczącego*.</span><span class="sxs-lookup"><span data-stu-id="58301-104">An ASP.NET Core app is built upon a series of *middleware*.</span></span> <span data-ttu-id="58301-105">Oprogramowanie pośredniczące to programy obsługi, które są rozmieszczone w potoku, aby obsługiwać żądania i odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="58301-105">Middleware is handlers that are arranged into a pipeline to handle requests and responses.</span></span> <span data-ttu-id="58301-106">W aplikacji formularzy sieci Web programy obsługi HTTP i moduły rozwiązują podobne problemy.</span><span class="sxs-lookup"><span data-stu-id="58301-106">In a Web Forms app, HTTP handlers and modules solve similar problems.</span></span> <span data-ttu-id="58301-107">W ASP.NET Core, moduły, programy obsługi, *Global.asax.cs*i cykl życia aplikacji są zastępowane przez oprogramowanie pośredniczące.</span><span class="sxs-lookup"><span data-stu-id="58301-107">In ASP.NET Core, modules, handlers, *Global.asax.cs*, and the app life cycle are replaced with middleware.</span></span> <span data-ttu-id="58301-108">W tym rozdziale opisano, co to jest oprogramowanie pośredniczące w kontekście Blazor aplikacji.</span><span class="sxs-lookup"><span data-stu-id="58301-108">In this chapter, you'll learn what middleware in the context of a Blazor app.</span></span>

## <a name="overview"></a><span data-ttu-id="58301-109">Omówienie</span><span class="sxs-lookup"><span data-stu-id="58301-109">Overview</span></span>

<span data-ttu-id="58301-110">Potok żądania ASP.NET Core składa się z sekwencji delegatów żądań o nazwie jeden po drugim.</span><span class="sxs-lookup"><span data-stu-id="58301-110">The ASP.NET Core request pipeline consists of a sequence of request delegates, called one after the other.</span></span> <span data-ttu-id="58301-111">Na poniższym diagramie przedstawiono koncepcję.</span><span class="sxs-lookup"><span data-stu-id="58301-111">The following diagram demonstrates the concept.</span></span> <span data-ttu-id="58301-112">Wątek wykonywania jest zgodny z czarnym strzałką.</span><span class="sxs-lookup"><span data-stu-id="58301-112">The thread of execution follows the black arrows.</span></span>

![proces](media/middleware/request-delegate-pipeline.png)

<span data-ttu-id="58301-114">Poprzedni diagram nie ma koncepcji zdarzeń cyklu życia.</span><span class="sxs-lookup"><span data-stu-id="58301-114">The preceding diagram lacks a concept of lifecycle events.</span></span> <span data-ttu-id="58301-115">To pojęcie jest podstawą, w jaki sposób obsługiwane są żądania ASP.NET Web Forms.</span><span class="sxs-lookup"><span data-stu-id="58301-115">This concept is foundational to how ASP.NET Web Forms requests are handled.</span></span> <span data-ttu-id="58301-116">Ten system ułatwia powód, w jakim proces jest wykonywany i umożliwia wstawianie oprogramowania pośredniczącego w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="58301-116">This system makes it easier to reason about what process is occurring and allows middleware to be inserted at any point.</span></span> <span data-ttu-id="58301-117">Oprogramowanie pośredniczące jest wykonywane w kolejności, w jakiej zostało dodane do potoku żądania.</span><span class="sxs-lookup"><span data-stu-id="58301-117">Middleware executes in the order in which it's added to the request pipeline.</span></span> <span data-ttu-id="58301-118">Są one również dodawane do kodu zamiast plików konfiguracji, zwykle w *Startup.cs*.</span><span class="sxs-lookup"><span data-stu-id="58301-118">They're also added in code instead of configuration files, usually in *Startup.cs*.</span></span>

## <a name="katana"></a><span data-ttu-id="58301-119">Katana</span><span class="sxs-lookup"><span data-stu-id="58301-119">Katana</span></span>

<span data-ttu-id="58301-120">Czytelnicy znający Katana będą mieć doświadczenie w ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="58301-120">Readers familiar with Katana will feel comfortable in ASP.NET Core.</span></span> <span data-ttu-id="58301-121">W rzeczywistości Katana jest strukturą, z której pochodzą ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="58301-121">In fact, Katana is a framework from which ASP.NET Core derives.</span></span> <span data-ttu-id="58301-122">Wprowadzono podobne wzorce oprogramowania pośredniczącego i potoków dla ASP.NET 4. x.</span><span class="sxs-lookup"><span data-stu-id="58301-122">It introduced similar middleware and pipeline patterns for ASP.NET 4.x.</span></span> <span data-ttu-id="58301-123">Oprogramowanie pośredniczące przeznaczone do Katana można dostosować do pracy z potokiem ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="58301-123">Middleware designed for Katana can be adapted to work with the ASP.NET Core pipeline.</span></span>

## <a name="common-middleware"></a><span data-ttu-id="58301-124">Typowe oprogramowanie pośredniczące</span><span class="sxs-lookup"><span data-stu-id="58301-124">Common middleware</span></span>

<span data-ttu-id="58301-125">ASP.NET 4. x zawiera wiele modułów.</span><span class="sxs-lookup"><span data-stu-id="58301-125">ASP.NET 4.x includes many modules.</span></span> <span data-ttu-id="58301-126">W podobny sposób ASP.NET Core ma również wiele dostępnych składników oprogramowania pośredniczącego.</span><span class="sxs-lookup"><span data-stu-id="58301-126">In a similar fashion, ASP.NET Core has many middleware components available as well.</span></span> <span data-ttu-id="58301-127">W niektórych przypadkach można używać modułów usług IIS z ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="58301-127">IIS modules may be used in some cases with ASP.NET Core.</span></span> <span data-ttu-id="58301-128">W innych przypadkach może być dostępne oprogramowanie pośredniczące Native ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="58301-128">In other cases, native ASP.NET Core middleware may be available.</span></span>

<span data-ttu-id="58301-129">W poniższej tabeli wymieniono zamienne oprogramowanie i składniki programu w ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="58301-129">The following table lists replacement middleware and components in ASP.NET Core.</span></span>

|<span data-ttu-id="58301-130">Moduł</span><span class="sxs-lookup"><span data-stu-id="58301-130">Module</span></span>                 |<span data-ttu-id="58301-131">ASP.NET 4. x — moduł</span><span class="sxs-lookup"><span data-stu-id="58301-131">ASP.NET 4.x module</span></span>           |<span data-ttu-id="58301-132">Opcja ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="58301-132">ASP.NET Core option</span></span>|
|-----------------------|-----------------------------|-------------------|
|<span data-ttu-id="58301-133">Błędy HTTP</span><span class="sxs-lookup"><span data-stu-id="58301-133">HTTP errors</span></span>            |`CustomErrorModule`          |[<span data-ttu-id="58301-134">Oprogramowanie pośredniczące stron kodu stanu</span><span class="sxs-lookup"><span data-stu-id="58301-134">Status Code Pages Middleware</span></span>](/aspnet/core/fundamentals/error-handling#usestatuscodepages)|
|<span data-ttu-id="58301-135">Dokument domyślny</span><span class="sxs-lookup"><span data-stu-id="58301-135">Default document</span></span>       |`DefaultDocumentModule`      |[<span data-ttu-id="58301-136">Pliki domyślne oprogramowania pośredniczącego</span><span class="sxs-lookup"><span data-stu-id="58301-136">Default Files Middleware</span></span>](/aspnet/core/fundamentals/static-files#serve-a-default-document)|
|<span data-ttu-id="58301-137">Przeglądanie katalogów</span><span class="sxs-lookup"><span data-stu-id="58301-137">Directory browsing</span></span>     |`DirectoryListingModule`     |[<span data-ttu-id="58301-138">Oprogramowanie pośredniczące przeglądania katalogów</span><span class="sxs-lookup"><span data-stu-id="58301-138">Directory Browsing Middleware</span></span>](/aspnet/core/fundamentals/static-files#enable-directory-browsing)|
|<span data-ttu-id="58301-139">Kompresja dynamiczna</span><span class="sxs-lookup"><span data-stu-id="58301-139">Dynamic compression</span></span>    |`DynamicCompressionModule`   |[<span data-ttu-id="58301-140">Oprogramowanie pośredniczące kompresji odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="58301-140">Response Compression Middleware</span></span>](/aspnet/core/performance/response-compression)|
|<span data-ttu-id="58301-141">Śledzenie nieudanych żądań</span><span class="sxs-lookup"><span data-stu-id="58301-141">Failed requests tracing</span></span>|`FailedRequestsTracingModule`|[<span data-ttu-id="58301-142">Rejestrowanie ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="58301-142">ASP.NET Core Logging</span></span>](/aspnet/core/fundamentals/logging/index#tracesource-provider)|
|<span data-ttu-id="58301-143">Buforowanie plików</span><span class="sxs-lookup"><span data-stu-id="58301-143">File caching</span></span>           |`FileCacheModule`            |[<span data-ttu-id="58301-144">Oprogramowanie pośredniczące buforowania odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="58301-144">Response Caching Middleware</span></span>](/aspnet/core/performance/caching/middleware)|
|<span data-ttu-id="58301-145">Buforowanie HTTP</span><span class="sxs-lookup"><span data-stu-id="58301-145">HTTP caching</span></span>           |`HttpCacheModule`            |[<span data-ttu-id="58301-146">Oprogramowanie pośredniczące buforowania odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="58301-146">Response Caching Middleware</span></span>](/aspnet/core/performance/caching/middleware)|
|<span data-ttu-id="58301-147">Rejestrowanie HTTP</span><span class="sxs-lookup"><span data-stu-id="58301-147">HTTP logging</span></span>           |`HttpLoggingModule`          |[<span data-ttu-id="58301-148">Rejestrowanie ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="58301-148">ASP.NET Core Logging</span></span>](/aspnet/core/fundamentals/logging/index)|
|<span data-ttu-id="58301-149">Przekierowywanie HTTP</span><span class="sxs-lookup"><span data-stu-id="58301-149">HTTP redirection</span></span>       |`HttpRedirectionModule`      |[<span data-ttu-id="58301-150">Oprogramowanie pośredniczące ponownego zapisywania adresów URL</span><span class="sxs-lookup"><span data-stu-id="58301-150">URL Rewriting Middleware</span></span>](/aspnet/core/fundamentals/url-rewriting)|
|<span data-ttu-id="58301-151">Filtry ISAPI</span><span class="sxs-lookup"><span data-stu-id="58301-151">ISAPI filters</span></span>          |`IsapiFilterModule`          |[<span data-ttu-id="58301-152">Oprogramowanie pośredniczące</span><span class="sxs-lookup"><span data-stu-id="58301-152">Middleware</span></span>](/aspnet/core/fundamentals/middleware/index)|
|<span data-ttu-id="58301-153">INTERCEPTOR</span><span class="sxs-lookup"><span data-stu-id="58301-153">ISAPI</span></span>                  |`IsapiModule`                |[<span data-ttu-id="58301-154">Oprogramowanie pośredniczące</span><span class="sxs-lookup"><span data-stu-id="58301-154">Middleware</span></span>](/aspnet/core/fundamentals/middleware/index)|
|<span data-ttu-id="58301-155">Filtrowanie żądań</span><span class="sxs-lookup"><span data-stu-id="58301-155">Request filtering</span></span>      |`RequestFilteringModule`     |[<span data-ttu-id="58301-156">Ponowne zapisywanie adresów URL IRule oprogramowania pośredniczącego</span><span class="sxs-lookup"><span data-stu-id="58301-156">URL Rewriting Middleware IRule</span></span>](/aspnet/core/fundamentals/url-rewriting#irule-based-rule)|
|<span data-ttu-id="58301-157">Ponowne zapisywanie adresów URL&#8224;</span><span class="sxs-lookup"><span data-stu-id="58301-157">URL rewriting&#8224;</span></span>   |`RewriteModule`              |[<span data-ttu-id="58301-158">Oprogramowanie pośredniczące ponownego zapisywania adresów URL</span><span class="sxs-lookup"><span data-stu-id="58301-158">URL Rewriting Middleware</span></span>](/aspnet/core/fundamentals/url-rewriting)|
|<span data-ttu-id="58301-159">Kompresja statyczna</span><span class="sxs-lookup"><span data-stu-id="58301-159">Static compression</span></span>     |`StaticCompressionModule`    |[<span data-ttu-id="58301-160">Oprogramowanie pośredniczące kompresji odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="58301-160">Response Compression Middleware</span></span>](/aspnet/core/performance/response-compression)|
|<span data-ttu-id="58301-161">Zawartość statyczna</span><span class="sxs-lookup"><span data-stu-id="58301-161">Static content</span></span>         |`StaticFileModule`           |[<span data-ttu-id="58301-162">Oprogramowanie pośredniczące plików statycznych</span><span class="sxs-lookup"><span data-stu-id="58301-162">Static File Middleware</span></span>](/aspnet/core/fundamentals/static-files)|
|<span data-ttu-id="58301-163">Autoryzacja adresów URL</span><span class="sxs-lookup"><span data-stu-id="58301-163">URL authorization</span></span>      |`UrlAuthorizationModule`     |[<span data-ttu-id="58301-164">ASP.NET Core tożsamość</span><span class="sxs-lookup"><span data-stu-id="58301-164">ASP.NET Core Identity</span></span>](/aspnet/core/security/authentication/identity)|

<span data-ttu-id="58301-165">Ta lista nie jest wyczerpująca, ale powinna zawierać pomysł dotyczący tego, jakie mapowanie istnieje między tymi dwoma strukturami.</span><span class="sxs-lookup"><span data-stu-id="58301-165">This list isn't exhaustive but should give an idea of what mapping exists between the two frameworks.</span></span> <span data-ttu-id="58301-166">Aby uzyskać bardziej szczegółową listę, zobacz [moduły usług IIS z ASP.NET Core](/aspnet/core/host-and-deploy/iis/modules).</span><span class="sxs-lookup"><span data-stu-id="58301-166">For a more detailed list, see [IIS modules with ASP.NET Core](/aspnet/core/host-and-deploy/iis/modules).</span></span>

## <a name="custom-middleware"></a><span data-ttu-id="58301-167">Niestandardowe oprogramowanie pośredniczące</span><span class="sxs-lookup"><span data-stu-id="58301-167">Custom middleware</span></span>

<span data-ttu-id="58301-168">Wbudowane oprogramowanie pośredniczące może nie obsługiwać wszystkich scenariuszy wymaganych przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="58301-168">Built-in middleware may not handle all scenarios needed for an app.</span></span> <span data-ttu-id="58301-169">W takich przypadkach warto utworzyć własne oprogramowanie pośredniczące.</span><span class="sxs-lookup"><span data-stu-id="58301-169">In such cases, it makes sense to create your own middleware.</span></span> <span data-ttu-id="58301-170">Istnieje wiele sposobów definiowania oprogramowania pośredniczącego, z najprostszym delegatem.</span><span class="sxs-lookup"><span data-stu-id="58301-170">There are multiple ways of defining middleware, with the simplest being a simple delegate.</span></span> <span data-ttu-id="58301-171">Weź pod uwagę następujące oprogramowanie pośredniczące, które akceptuje żądanie kultury z ciągu zapytania:</span><span class="sxs-lookup"><span data-stu-id="58301-171">Consider the following middleware, which accepts a culture request from a query string:</span></span>

```csharp
public class Startup
{
    public void Configure(IApplicationBuilder app)
    {
        app.Use(async (context, next) =>
        {
            var cultureQuery = context.Request.Query["culture"];

            if (!string.IsNullOrWhiteSpace(cultureQuery))
            {
                var culture = new CultureInfo(cultureQuery);

                CultureInfo.CurrentCulture = culture;
                CultureInfo.CurrentUICulture = culture;
            }

            // Call the next delegate/middleware in the pipeline
            await next();
        });

        app.Run(async (context) =>
            await context.Response.WriteAsync(
                $"Hello {CultureInfo.CurrentCulture.DisplayName}"));
    }
}
```

<span data-ttu-id="58301-172">Oprogramowanie pośredniczące może być również zdefiniowane jako Klasa przez implementację `IMiddleware` interfejsu lub przez następującą konwencję pośredniczącą.</span><span class="sxs-lookup"><span data-stu-id="58301-172">Middleware can also be defined as class, either by implementing the `IMiddleware` interface or by following middleware convention.</span></span> <span data-ttu-id="58301-173">Aby uzyskać więcej informacji, zobacz [Zapisywanie niestandardowych ASP.NET Core oprogramowania pośredniczącego](/aspnet/core/fundamentals/middleware/write).</span><span class="sxs-lookup"><span data-stu-id="58301-173">For more information, see [Write custom ASP.NET Core middleware](/aspnet/core/fundamentals/middleware/write).</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="58301-174">[Poprzedni](data.md) 
> [Dalej](config.md)</span><span class="sxs-lookup"><span data-stu-id="58301-174">[Previous](data.md)
[Next](config.md)</span></span>
