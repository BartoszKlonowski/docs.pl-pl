---
title: Błąd SYSLIB0002
description: Dowiedz się więcej o obsoletion, który generuje błąd czasu kompilowania SYSLIB0002.
ms.topic: reference
ms.date: 10/20/2020
ms.openlocfilehash: 774675e96d11a8e1b5d82767695d0defd1e8cfad
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/16/2020
ms.locfileid: "97596568"
---
# <a name="syslib0002-principalpermissionattribute-is-obsolete"></a>SYSLIB0002: PrincipalPermissionAttribute jest przestarzała

<xref:System.Security.Permissions.PrincipalPermissionAttribute>Konstruktor jest przestarzały i generuje błąd czasu kompilacji `SYSLIB0002` , rozpoczynając od platformy .NET 5,0. Nie można utworzyć wystąpienia tego atrybutu lub zastosować go do metody.

W przeciwieństwie do innych ostrzeżeń obsoletion nie można pominąć tego błędu.

## <a name="workarounds"></a>Obejścia

- Jeśli stosujesz atrybut do metody akcji ASP.NET MVC:

  Rozważ użycie środowiska ASP. Wbudowana infrastruktura autoryzacji w sieci. Poniższy kod ilustruje sposób dodawania adnotacji do kontrolera z <xref:System.Web.Mvc.AuthorizeAttribute> atrybutem. Środowisko uruchomieniowe ASP.NET będzie autoryzować użytkownika przed wykonaniem akcji.

  ```csharp
  using Microsoft.AspNetCore.Authorization;

  namespace MySampleApp
  {
      [Authorize(Roles = "Administrator")]
      public class AdministrationController : Controller
      {
          public ActionResult MyAction()
          {
              // This code won't run unless the current user
              // is in the 'Administrator' role.
          }
      }
  }
  ```

  Aby uzyskać więcej informacji, zobacz [Autoryzacja oparta na rolach w ASP.NET Core](/aspnet/core/security/authorization/roles) i [wprowadzenie do autoryzacji w programie ASP.NET Core](/aspnet/core/security/authorization/introduction).

- Jeśli stosujesz atrybut do kodu biblioteki poza kontekstem aplikacji sieci Web:

  Ręcznie wykonaj testy na początku metody, wywołując <xref:System.Security.Principal.IPrincipal.IsInRole(System.String)?displayProperty=nameWithType> metodę.

  ```csharp
  using System.Threading;

  void DoSomething()
  {
      if (Thread.CurrentPrincipal == null
          || !Thread.CurrentPrincipal.IsInRole("Administrators"))
      {
          throw new Exception("User is anonymous or isn't an admin.");
      }

      // Code that should run only when user is an administrator.
  }
  ```

[!INCLUDE [suppress-syslib-warning](../../../../includes/suppress-syslib-warning.md)]

## <a name="see-also"></a>Zobacz także

- [PrincipalPermissionAttribute jest przestarzały jako błąd](../core-libraries/5.0/principalpermissionattribute-obsolete.md)
