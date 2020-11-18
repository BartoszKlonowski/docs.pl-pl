---
title: 'Instrukcje: Tworzenie obiektów GenericPrincipal i GenericIdentity'
ms.date: 07/15/2020
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Creating Generic Identity Objects
- GenericPrincipal Objects
- Creating GenericPrincipal Objects
- GenericIdentity Objects
ms.assetid: 465694cf-258b-4747-9dae-35b01a5bcdbb
ms.openlocfilehash: cde4669a1bac49d1d9fde39c99707561379aec19
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "94818996"
---
# <a name="how-to-create-genericprincipal-and-genericidentity-objects"></a>Instrukcje: Tworzenie obiektów GenericPrincipal i GenericIdentity

> [!NOTE]
> Ten artykuł dotyczy systemu Windows.
>
> Aby uzyskać informacje na temat ASP.NET Core, zobacz [Omówienie zabezpieczeń ASP.NET Core](/aspnet/core/security/).

Można użyć <xref:System.Security.Principal.GenericIdentity> klasy w połączeniu z <xref:System.Security.Principal.GenericPrincipal> klasą, aby utworzyć schemat autoryzacji, który istnieje niezależnie od domeny systemu Windows.

### <a name="to-create-a-genericprincipal-object"></a>Aby utworzyć obiekt GenericPrincipal —

1. Utwórz nowe wystąpienie klasy Identity i zainicjuj je nazwą, która ma zostać wstrzymana. Poniższy kod tworzy nowy obiekt **GenericIdentity** i inicjuje go nazwą `MyUser` .

    ```vb
    Dim myIdentity As New GenericIdentity("MyUser")
    ```

    ```csharp
    GenericIdentity myIdentity = new GenericIdentity("MyUser");
    ```

2. Utwórz nowe wystąpienie klasy **GenericPrincipal —** i zainicjuj je za pomocą wcześniej utworzonego obiektu **GenericIdentity** i tablicy ciągów reprezentujących role, które mają być skojarzone z tym podmiotem zabezpieczeń. Poniższy przykład kodu określa tablicę ciągów, które reprezentują rolę administratora i rolę użytkownika. **GenericPrincipal —** zostaje następnie zainicjowany z poprzednią **GenericIdentity** i tablicą ciągów.

    ```vb
    Dim myStringArray As String() = {"Manager", "Teller"}
    DIm myPrincipal As New GenericPrincipal(myIdentity, myStringArray)
    ```

    ```csharp
    String[] myStringArray = {"Manager", "Teller"};
    GenericPrincipal myPrincipal = new GenericPrincipal(myIdentity, myStringArray);
    ```

3. Użyj poniższego kodu, aby dołączyć podmiot zabezpieczeń do bieżącego wątku. Jest to przydatne w sytuacjach, w których podmiot zabezpieczeń musi być zweryfikowany kilka razy, musi być zweryfikowany przez inny kod uruchomiony w aplikacji lub musi być zweryfikowany przez <xref:System.Security.Permissions.PrincipalPermission> obiekt. Można nadal wykonywać walidację na obiekcie Principal, bez dołączania go do wątku. Aby uzyskać więcej informacji, zobacz [zastępowanie obiektu podmiotu zabezpieczeń](replacing-a-principal-object.md).

    ```vb
    Thread.CurrentPrincipal = myPrincipal
    ```

    ```csharp
    Thread.CurrentPrincipal = myPrincipal;
    ```

## <a name="example"></a>Przykład

Poniższy przykład kodu demonstruje, jak utworzyć wystąpienie elementu **GenericPrincipal —** i **GenericIdentity**. Ten kod wyświetla wartości tych obiektów w konsoli programu.

```vb
Imports System.Security.Principal
Imports System.Threading

Public Class Class1

    Public Shared Sub Main()
        ' Create generic identity.
        Dim myIdentity As New GenericIdentity("MyIdentity")

        ' Create generic principal.
        Dim myStringArray As String() =  {"Manager", "Teller"}
        Dim myPrincipal As New GenericPrincipal(myIdentity, myStringArray)

        ' Attach the principal to the current thread.
        ' This is not required unless repeated validation must occur,
        ' other code in your application must validate, or the
        ' PrincipalPermission object is used.
        Thread.CurrentPrincipal = myPrincipal

        ' Print values to the console.
        Dim name As String = myPrincipal.Identity.Name
        Dim auth As Boolean = myPrincipal.Identity.IsAuthenticated
        Dim isInRole As Boolean = myPrincipal.IsInRole("Manager")

        Console.WriteLine("The name is: {0}", name)
        Console.WriteLine("The isAuthenticated is: {0}", auth)
        Console.WriteLine("Is this a Manager? {0}", isInRole)

    End Sub

End Class
```

```csharp
using System;
using System.Security.Principal;
using System.Threading;

public class Class1
{
    public static int Main(string[] args)
    {
    // Create generic identity.
    GenericIdentity myIdentity = new GenericIdentity("MyIdentity");

    // Create generic principal.
    String[] myStringArray = {"Manager", "Teller"};
    GenericPrincipal myPrincipal =
        new GenericPrincipal(myIdentity, myStringArray);

    // Attach the principal to the current thread.
    // This is not required unless repeated validation must occur,
    // other code in your application must validate, or the
    // PrincipalPermission object is used.
    Thread.CurrentPrincipal = myPrincipal;

    // Print values to the console.
    String name =  myPrincipal.Identity.Name;
    bool auth =  myPrincipal.Identity.IsAuthenticated;
    bool isInRole =  myPrincipal.IsInRole("Manager");

    Console.WriteLine("The name is: {0}", name);
    Console.WriteLine("The isAuthenticated is: {0}", auth);
    Console.WriteLine("Is this a Manager? {0}", isInRole);

    return 0;
    }
}
```

Po wykonaniu aplikacja wyświetli dane wyjściowe podobne do poniższych.

```console
The Name is: MyIdentity
The IsAuthenticated is: True
Is this a Manager? True
```

## <a name="see-also"></a>Zobacz także

- <xref:System.Security.Principal.GenericIdentity>
- <xref:System.Security.Principal.GenericPrincipal>
- <xref:System.Security.Permissions.PrincipalPermission>
- [Zastępowanie obiektu głównego](replacing-a-principal-object.md)
- [Obiekty główne i obiekty tożsamości](principal-and-identity-objects.md)
