---
ms.openlocfilehash: 959f3959c28c7d0159be7a213986345e2865b9a2
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/25/2020
ms.locfileid: "96032865"
---
### <a name="shared-framework-removed-microsoftaspnetcoreall"></a>Udostępnione środowisko: Usunięto Microsoft. AspNetCore. All

Począwszy od ASP.NET Core 3,0, `Microsoft.AspNetCore.All` `Microsoft.AspNetCore.All` nie jest już tworzony pakiet i zgodna struktura współdzielona. Ten pakiet jest dostępny w ASP.NET Core 2,2 i nadal będzie otrzymywać aktualizacje obsługi w programie ASP.NET Core 2,1.

#### <a name="version-introduced"></a>Wprowadzona wersja

3.0

#### <a name="old-behavior"></a>Stare zachowanie

Aplikacje mogą używać `Microsoft.AspNetCore.All` pakietu dla `Microsoft.AspNetCore.All` platformy udostępnionej w programie .NET Core.

#### <a name="new-behavior"></a>Nowe zachowanie

Platforma .NET Core 3,0 nie obejmuje `Microsoft.AspNetCore.All` współdzielonej struktury.

#### <a name="reason-for-change"></a>Przyczyna zmiany

`Microsoft.AspNetCore.All`Pakietbinding zawiera dużą liczbę zależności zewnętrznych.

#### <a name="recommended-action"></a>Zalecana akcja

Migruj projekt, aby użyć `Microsoft.AspNetCore.App` struktury. Składniki, które wcześniej były dostępne w programie, `Microsoft.AspNetCore.All` są nadal dostępne w programie NuGet. Te składniki są teraz wdrażane wraz z aplikacją, a nie uwzględniane w strukturze udostępnionej.

#### <a name="category"></a>Kategoria

ASP.NET Core

#### <a name="affected-apis"></a>Dotyczy interfejsów API

Brak

<!-- 

#### Affected APIs

Not detectable via API analysis

-->
