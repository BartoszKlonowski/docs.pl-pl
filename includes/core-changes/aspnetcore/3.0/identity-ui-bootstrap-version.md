---
ms.openlocfilehash: c8f44ae1a500ed240dbff7d9a2c1479af368b7f1
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/25/2020
ms.locfileid: "96032792"
---
### <a name="identity-default-bootstrap-version-of-ui-changed"></a>Tożsamość: domyślna wersja użytkownika Bootstrap została zmieniona

Począwszy od ASP.NET Core 3,0, interfejs użytkownika tożsamości jest domyślnie używany w wersji 4 programu Bootstrap.

#### <a name="version-introduced"></a>Wprowadzona wersja

3.0

#### <a name="old-behavior"></a>Stare zachowanie

`services.AddDefaultIdentity<IdentityUser>().AddDefaultUI();`Wywołanie metody było takie samo jak`services.AddDefaultIdentity<IdentityUser>().AddDefaultUI(UIFramework.Bootstrap3);`

#### <a name="new-behavior"></a>Nowe zachowanie

`services.AddDefaultIdentity<IdentityUser>().AddDefaultUI();`Wywołanie metody jest takie samo jak`services.AddDefaultIdentity<IdentityUser>().AddDefaultUI(UIFramework.Bootstrap4);`

#### <a name="reason-for-change"></a>Przyczyna zmiany

Uruchomienie Bootstrap 4 zostało wydane w okresie ASP.NET Core 3,0.

#### <a name="recommended-action"></a>Zalecana akcja

Ta zmiana jest zależna od tego, czy używany jest domyślny interfejs użytkownika tożsamości i czy został on dodany w programie `Startup.ConfigureServices` , jak pokazano w następującym przykładzie:

```csharp
services.AddDefaultIdentity<IdentityUser>().AddDefaultUI();
```

Wykonaj jedno z następujących działań:

- Przeprowadź migrację aplikacji, aby użyć ładowania początkowego 4 przy użyciu ich [przewodnika migracji](https://getbootstrap.com/docs/4.0/migration).
- Aktualizacja `Startup.ConfigureServices` w celu wymuszenia użycia programu Bootstrap 3. Przykład:

    ```csharp
    services.AddDefaultIdentity<IdentityUser>().AddDefaultUI(UIFramework.Bootstrap3);
    ```

#### <a name="category"></a>Kategoria

ASP.NET Core

#### <a name="affected-apis"></a>Dotyczy interfejsów API

Brak

<!-- 

#### Affected APIs

Not detectable via API analysis

-->
