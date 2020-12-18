---
title: Moduły, programy obsługi i oprogramowanie pośredniczące
description: Dowiedz się więcej na temat obsługi żądań HTTP za pomocą modułów, programów obsługi i oprogramowania pośredniczącego.
author: danroth27
ms.author: daroth
no-loc:
- Blazor
ms.date: 10/11/2019
ms.openlocfilehash: dbb0a94b0401d58139c024fd8ca3e00353a19efa
ms.sourcegitcommit: 4b79862c5b41fbd86cf38f926f6a49516059f6f2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/18/2020
ms.locfileid: "97678034"
---
# <a name="modules-handlers-and-middleware"></a>Moduły, programy obsługi i oprogramowanie pośredniczące

Aplikacja ASP.NET Core jest oparta na serii *oprogramowania pośredniczącego*. Oprogramowanie pośredniczące to programy obsługi, które są rozmieszczone w potoku, aby obsługiwać żądania i odpowiedzi. W aplikacji formularzy sieci Web programy obsługi HTTP i moduły rozwiązują podobne problemy. W ASP.NET Core, moduły, programy obsługi, *Global.asax.cs* i cykl życia aplikacji są zastępowane przez oprogramowanie pośredniczące. W tym rozdziale przedstawiono informacje na temat oprogramowania pośredniczącego w kontekście Blazor aplikacji.

## <a name="overview"></a>Omówienie

Potok żądania ASP.NET Core składa się z sekwencji delegatów żądań o nazwie jeden po drugim. Na poniższym diagramie przedstawiono koncepcję. Wątek wykonywania jest zgodny z czarnym strzałką.

![proces](media/middleware/request-delegate-pipeline.png)

Poprzedni diagram nie ma koncepcji zdarzeń cyklu życia. To pojęcie jest podstawą, w jaki sposób obsługiwane są żądania ASP.NET Web Forms. Ten system ułatwia powód, w jakim proces jest wykonywany i umożliwia wstawianie oprogramowania pośredniczącego w dowolnym momencie. Oprogramowanie pośredniczące jest wykonywane w kolejności, w jakiej zostało dodane do potoku żądania. Są one również dodawane do kodu zamiast plików konfiguracji, zwykle w *Startup.cs*.

## <a name="katana"></a>Katana

Czytelnicy znający Katana będą mieć doświadczenie w ASP.NET Core. W rzeczywistości Katana jest strukturą, z której pochodzą ASP.NET Core. Wprowadzono podobne wzorce oprogramowania pośredniczącego i potoków dla ASP.NET 4. x. Oprogramowanie pośredniczące przeznaczone do Katana można dostosować do pracy z potokiem ASP.NET Core.

## <a name="common-middleware"></a>Typowe oprogramowanie pośredniczące

ASP.NET 4. x zawiera wiele modułów. W podobny sposób ASP.NET Core ma również wiele dostępnych składników oprogramowania pośredniczącego. W niektórych przypadkach można używać modułów usług IIS z ASP.NET Core. W innych przypadkach może być dostępne oprogramowanie pośredniczące Native ASP.NET Core.

W poniższej tabeli wymieniono zamienne oprogramowanie i składniki programu w ASP.NET Core.

|Moduł                 |ASP.NET 4. x — moduł           |Opcja ASP.NET Core|
|-----------------------|-----------------------------|-------------------|
|Błędy HTTP            |`CustomErrorModule`          |[Oprogramowanie pośredniczące stron kodu stanu](/aspnet/core/fundamentals/error-handling#usestatuscodepages)|
|Dokument domyślny       |`DefaultDocumentModule`      |[Pliki domyślne oprogramowania pośredniczącego](/aspnet/core/fundamentals/static-files#serve-a-default-document)|
|Przeglądanie katalogów     |`DirectoryListingModule`     |[Oprogramowanie pośredniczące przeglądania katalogów](/aspnet/core/fundamentals/static-files#enable-directory-browsing)|
|Kompresja dynamiczna    |`DynamicCompressionModule`   |[Oprogramowanie pośredniczące kompresji odpowiedzi](/aspnet/core/performance/response-compression)|
|Śledzenie nieudanych żądań|`FailedRequestsTracingModule`|[Rejestrowanie ASP.NET Core](/aspnet/core/fundamentals/logging/index#tracesource-provider)|
|Buforowanie plików           |`FileCacheModule`            |[Oprogramowanie pośredniczące buforowania odpowiedzi](/aspnet/core/performance/caching/middleware)|
|Buforowanie HTTP           |`HttpCacheModule`            |[Oprogramowanie pośredniczące buforowania odpowiedzi](/aspnet/core/performance/caching/middleware)|
|Rejestrowanie HTTP           |`HttpLoggingModule`          |[Rejestrowanie ASP.NET Core](/aspnet/core/fundamentals/logging/index)|
|Przekierowywanie HTTP       |`HttpRedirectionModule`      |[Oprogramowanie pośredniczące ponownego zapisywania adresów URL](/aspnet/core/fundamentals/url-rewriting)|
|Filtry ISAPI          |`IsapiFilterModule`          |[Oprogramowanie pośredniczące](/aspnet/core/fundamentals/middleware/index)|
|INTERCEPTOR                  |`IsapiModule`                |[Oprogramowanie pośredniczące](/aspnet/core/fundamentals/middleware/index)|
|Filtrowanie żądań      |`RequestFilteringModule`     |[Ponowne zapisywanie adresów URL IRule oprogramowania pośredniczącego](/aspnet/core/fundamentals/url-rewriting#irule-based-rule)|
|Ponowne zapisywanie adresów URL&#8224;   |`RewriteModule`              |[Oprogramowanie pośredniczące ponownego zapisywania adresów URL](/aspnet/core/fundamentals/url-rewriting)|
|Kompresja statyczna     |`StaticCompressionModule`    |[Oprogramowanie pośredniczące kompresji odpowiedzi](/aspnet/core/performance/response-compression)|
|Zawartość statyczna         |`StaticFileModule`           |[Oprogramowanie pośredniczące plików statycznych](/aspnet/core/fundamentals/static-files)|
|Autoryzacja adresów URL      |`UrlAuthorizationModule`     |[ASP.NET Core tożsamość](/aspnet/core/security/authentication/identity)|

Ta lista nie jest wyczerpująca, ale powinna zawierać pomysł dotyczący tego, jakie mapowanie istnieje między tymi dwoma strukturami. Aby uzyskać bardziej szczegółową listę, zobacz [moduły usług IIS z ASP.NET Core](/aspnet/core/host-and-deploy/iis/modules).

## <a name="custom-middleware"></a>Niestandardowe oprogramowanie pośredniczące

Wbudowane oprogramowanie pośredniczące może nie obsługiwać wszystkich scenariuszy wymaganych przez aplikację. W takich przypadkach warto utworzyć własne oprogramowanie pośredniczące. Istnieje wiele sposobów definiowania oprogramowania pośredniczącego, z najprostszym delegatem. Weź pod uwagę następujące oprogramowanie pośredniczące, które akceptuje żądanie kultury z ciągu zapytania:

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

Oprogramowanie pośredniczące może być również zdefiniowane jako Klasa przez implementację `IMiddleware` interfejsu lub przez następującą konwencję pośredniczącą. Aby uzyskać więcej informacji, zobacz [Zapisywanie niestandardowych ASP.NET Core oprogramowania pośredniczącego](/aspnet/core/fundamentals/middleware/write).

>[!div class="step-by-step"]
>[Poprzedni](data.md) 
> [Dalej](config.md)
