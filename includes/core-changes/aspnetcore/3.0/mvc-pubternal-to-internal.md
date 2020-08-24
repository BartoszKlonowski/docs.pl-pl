---
ms.openlocfilehash: 5741e8cdd51e00d5459c4c1032a56682429aab17
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/14/2020
ms.locfileid: "75901690"
---
### <a name="mvc-pubternal-types-changed-to-internal"></a>MVC: typy "Pubternal" zostały zmienione na wewnętrzne

W ASP.NET Core 3,0 wszystkie typy "pubternal" w MVC zostały zaktualizowane do `public` obsługiwanej przestrzeni nazw lub w zależności `internal` od potrzeb.

#### <a name="change-description"></a>Zmień opis

W ASP.NET Core typy "pubternal" są zadeklarowane jako, `public` ale znajdują się `.Internal` w przestrzeni nazw z sufiksem. Chociaż te typy są `public` , nie mają zasad pomocy technicznej i podlegają istotnym zmianom. Niestety, przypadkowe użycie tych typów było wspólne, co spowodowało istotne zmiany w tych projektach i ograniczenie możliwości utrzymania struktury.

#### <a name="version-introduced"></a>Wprowadzona wersja

3,0

#### <a name="old-behavior"></a>Stare zachowanie

Niektóre typy w MVC były, `public` ale w `.Internal` przestrzeni nazw. Te typy nie miały zasad pomocy technicznej i podlegają istotnym zmianom.

#### <a name="new-behavior"></a>Nowe zachowanie

Wszystkie takie typy są aktualizowane, aby były `public` w obsługiwanej przestrzeni nazw lub oznaczone jako `internal` .

#### <a name="reason-for-change"></a>Przyczyna zmiany

Przypadkowe użycie typów "pubternal" jest wspólne, co skutkuje istotnymi zmianami w tych projektach i ograniczeniem możliwości utrzymania struktury.

#### <a name="recommended-action"></a>Zalecana akcja

Jeśli używasz typów, które staną się naprawdę `public` i zostały przeniesione do nowej, obsługiwanej przestrzeni nazw, zaktualizuj odwołania, aby odpowiadały nowym przestrzeniom nazw.

Jeśli używasz typów, które zostały oznaczone jako, musisz `internal` znaleźć alternatywę. Wcześniej typy "pubternal" nigdy nie były obsługiwane do użytku publicznego. Jeśli istnieją określone typy w tych obszarach nazw, które mają krytyczne znaczenie dla aplikacji, należy rozwiązać problem w programie [dotnet/aspnetcore](https://github.com/dotnet/aspnetcore/issues). W przypadku tworzenia żądanych typów mogą być brane pod uwagę `public` .

#### <a name="category"></a>Kategoria

ASP.NET Core

#### <a name="affected-apis"></a>Dotyczy interfejsów API

Ta zmiana obejmuje typy w następujących przestrzeniach nazw:

- `Microsoft.AspNetCore.Mvc.Cors.Internal`
- `Microsoft.AspNetCore.Mvc.DataAnnotations.Internal`
- `Microsoft.AspNetCore.Mvc.Formatters.Internal`
- `Microsoft.AspNetCore.Mvc.Formatters.Json.Internal`
- `Microsoft.AspNetCore.Mvc.Formatters.Xml.Internal`
- `Microsoft.AspNetCore.Mvc.Internal`
- `Microsoft.AspNetCore.Mvc.ModelBinding.Internal`
- `Microsoft.AspNetCore.Mvc.Razor.Internal`
- `Microsoft.AspNetCore.Mvc.RazorPages.Internal`
- `Microsoft.AspNetCore.Mvc.TagHelpers.Internal`
- `Microsoft.AspNetCore.Mvc.ViewFeatures.Internal`

<!--

#### Affected APIs

- `N:Microsoft.AspNetCore.Mvc.Cors.Internal`
- `N:Microsoft.AspNetCore.Mvc.DataAnnotations.Internal`
- `N:Microsoft.AspNetCore.Mvc.Formatters.Internal`
- `N:Microsoft.AspNetCore.Mvc.Formatters.Json.Internal`
- `N:Microsoft.AspNetCore.Mvc.Formatters.Xml.Internal`
- `N:Microsoft.AspNetCore.Mvc.Internal`
- `N:Microsoft.AspNetCore.Mvc.ModelBinding.Internal`
- `N:Microsoft.AspNetCore.Mvc.Razor.Internal`
- `N:Microsoft.AspNetCore.Mvc.RazorPages.Internal`
- `N:Microsoft.AspNetCore.Mvc.TagHelpers.Internal`
- `N:Microsoft.AspNetCore.Mvc.ViewFeatures.Internal`

-->
