---
title: Zabezpieczanie obsługi wyjątków
description: Zobacz, jak zapewnić obsługę wyjątków Secure w kodzie .NET. Sprawdź kolejność, w której kod jest uruchamiany, jeśli istnieją instrukcje try, EXCEPT, catch i finally.
ms.date: 03/30/2017
dev_langs:
- cpp
helpviewer_keywords:
- code security, exception handling
- security [.NET Framework], exception handling
- secure coding, exception handling
- exception handling, security
ms.assetid: 1f3da743-9742-47ff-96e6-d0dd1e9e1c19
ms.openlocfilehash: 009e587c0458488db6c2aa92e13311ddc08a64b1
ms.sourcegitcommit: 97ce5363efa88179dd76e09de0103a500ca9b659
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/13/2020
ms.locfileid: "86281998"
---
# <a name="securing-exception-handling"></a><span data-ttu-id="f68bd-104">Zabezpieczanie obsługi wyjątków</span><span class="sxs-lookup"><span data-stu-id="f68bd-104">Securing Exception Handling</span></span>
<span data-ttu-id="f68bd-105">W Visual C++ i Visual Basic, wyrażenie filtru uzupełnia stos działa przed jakąkolwiek instrukcją **finally** .</span><span class="sxs-lookup"><span data-stu-id="f68bd-105">In Visual C++ and Visual Basic, a filter expression further up the stack runs before any **finally** statement.</span></span> <span data-ttu-id="f68bd-106">Blok **catch** skojarzony z tym filtrem jest uruchamiany po instrukcji **finally** .</span><span class="sxs-lookup"><span data-stu-id="f68bd-106">The **catch** block associated with that filter runs after the **finally** statement.</span></span> <span data-ttu-id="f68bd-107">Aby uzyskać więcej informacji, zobacz [Używanie wyjątków filtrowanych przez użytkownika](../../standard/exceptions/using-user-filtered-exception-handlers.md).</span><span class="sxs-lookup"><span data-stu-id="f68bd-107">For more information, see [Using User-Filtered Exceptions](../../standard/exceptions/using-user-filtered-exception-handlers.md).</span></span> <span data-ttu-id="f68bd-108">Ta sekcja analizuje implikacje związane z bezpieczeństwem tej kolejności.</span><span class="sxs-lookup"><span data-stu-id="f68bd-108">This section examines the security implications of this order.</span></span> <span data-ttu-id="f68bd-109">Rozważmy następujący przykład pseudokodzie, który ilustruje kolejność, w której są uruchamiane instrukcje filtru i **finally** .</span><span class="sxs-lookup"><span data-stu-id="f68bd-109">Consider the following pseudocode example that illustrates the order in which filter statements and **finally** statements run.</span></span>  
  
```cpp  
void Main()
{  
    try
    {  
        Sub();  
    }
    except (Filter())
    {  
        Console.WriteLine("catch");  
    }  
}  
bool Filter () {  
    Console.WriteLine("filter");  
    return true;  
}  
void Sub()
{  
    try
    {  
        Console.WriteLine("throw");  
        throw new Exception();  
    }
    finally
    {  
        Console.WriteLine("finally");  
    }  
}
```  
  
 <span data-ttu-id="f68bd-110">Ten kod drukuje następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="f68bd-110">This code prints the following.</span></span>  
  
```output
Throw  
Filter  
Finally  
Catch  
```  
  
 <span data-ttu-id="f68bd-111">Filtr jest uruchamiany przed instrukcją **finally** , więc problemy z zabezpieczeniami mogą być wprowadzane przez wszystkie elementy, które wprowadzają zmianę stanu, w którym może zostać wykorzystana funkcja innego kodu.</span><span class="sxs-lookup"><span data-stu-id="f68bd-111">The filter runs before the **finally** statement, so security issues can be introduced by anything that makes a state change where execution of other code could take advantage.</span></span> <span data-ttu-id="f68bd-112">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="f68bd-112">For example:</span></span>  
  
```cpp  
try
{  
    Alter_Security_State();  
    // This means changing anything (state variables,  
    // switching unmanaged context, impersonation, and
    // so on) that could be exploited if malicious
    // code ran before state is restored.  
    Do_some_work();  
}
finally
{  
    Restore_Security_State();  
    // This simply restores the state change above.  
}  
```  
  
 <span data-ttu-id="f68bd-113">Ta pseudokodzie umożliwia filtrowi zwiększenie poziomu stosu do uruchamiania dowolnego kodu.</span><span class="sxs-lookup"><span data-stu-id="f68bd-113">This pseudocode allows a filter higher up the stack to run arbitrary code.</span></span> <span data-ttu-id="f68bd-114">Inne przykłady operacji, które byłyby podobne, są tymczasowym personifikacją innej tożsamości, ustawiając wewnętrzną flagę, która pomija pewne sprawdzanie zabezpieczeń lub zmieniając kulturę skojarzoną z wątkiem.</span><span class="sxs-lookup"><span data-stu-id="f68bd-114">Other examples of operations that would have a similar effect are temporary impersonation of another identity, setting an internal flag that bypasses some security check, or changing the culture associated with the thread.</span></span> <span data-ttu-id="f68bd-115">Zalecanym rozwiązaniem jest wprowadzenie procedury obsługi wyjątków w celu odizolowania zmian kodu stanu wątku z bloków filtrów wywołujących.</span><span class="sxs-lookup"><span data-stu-id="f68bd-115">The recommended solution is to introduce an exception handler to isolate the code's changes to thread state from callers' filter blocks.</span></span> <span data-ttu-id="f68bd-116">Należy jednak pamiętać, że program obsługi wyjątków został poprawnie wprowadzony lub ten problem nie zostanie rozwiązany.</span><span class="sxs-lookup"><span data-stu-id="f68bd-116">However, it is important that the exception handler be properly introduced or this problem will not be fixed.</span></span> <span data-ttu-id="f68bd-117">Poniższy przykład przełącza kulturę interfejsu użytkownika, ale każdy rodzaj zmiany stanu wątku może być podobnie narażony.</span><span class="sxs-lookup"><span data-stu-id="f68bd-117">The following example switches the UI culture, but any kind of thread state change could be similarly exposed.</span></span>  
  
```cpp  
YourObject.YourMethod()  
{  
   CultureInfo saveCulture = Thread.CurrentThread.CurrentUICulture;  
   try {  
      Thread.CurrentThread.CurrentUICulture = new CultureInfo("de-DE");  
      // Do something that throws an exception.  
}  
   finally {  
      Thread.CurrentThread.CurrentUICulture = saveCulture;  
   }  
}  
```  
  
```vb  
Public Class UserCode  
   Public Shared Sub Main()  
      Try  
         Dim obj As YourObject = new YourObject  
         obj.YourMethod()  
      Catch e As Exception When FilterFunc  
         Console.WriteLine("An error occurred: '{0}'", e)  
         Console.WriteLine("Current Culture: {0}",
Thread.CurrentThread.CurrentUICulture)  
      End Try  
   End Sub  
  
   Public Function FilterFunc As Boolean  
      Console.WriteLine("Current Culture: {0}", Thread.CurrentThread.CurrentUICulture)  
      Return True  
   End Sub  
  
End Class  
```  
  
 <span data-ttu-id="f68bd-118">Poprawna poprawka w tym przypadku polega na zawijaniu istniejącego bloku **try** / **finally** w bloku **try** / **catch** .</span><span class="sxs-lookup"><span data-stu-id="f68bd-118">The correct fix in this case is to wrap the existing **try**/**finally** block in a **try**/**catch** block.</span></span> <span data-ttu-id="f68bd-119">Po prostu wprowadzenie klauzuli **catch-throw** do istniejącego bloku **try** / **finally** nie rozwiąże problemu, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="f68bd-119">Simply introducing a **catch-throw** clause into the existing **try**/**finally** block does not fix the problem, as shown in the following example.</span></span>  
  
```cpp  
YourObject.YourMethod()  
{  
    CultureInfo saveCulture = Thread.CurrentThread.CurrentUICulture;  
  
    try
    {  
        Thread.CurrentThread.CurrentUICulture = new CultureInfo("de-DE");  
        // Do something that throws an exception.  
    }  
    catch { throw; }  
    finally
    {  
        Thread.CurrentThread.CurrentUICulture = saveCulture;  
    }  
}  
```  
  
 <span data-ttu-id="f68bd-120">Nie rozwiąże to problemu, ponieważ instrukcja **finally** nie została uruchomiona przed `FilterFunc` formantem get.</span><span class="sxs-lookup"><span data-stu-id="f68bd-120">This does not fix the problem because the **finally** statement has not run before the `FilterFunc` gets control.</span></span>  
  
 <span data-ttu-id="f68bd-121">Poniższy przykład rozwiązuje problem, upewniając się, że klauzula **finally** została wykonana przed wystąpieniem wyjątku filtru wyjątków wywołań.</span><span class="sxs-lookup"><span data-stu-id="f68bd-121">The following example fixes the problem by ensuring that the **finally** clause has executed before offering an exception up the callers' exception filter blocks.</span></span>  
  
```cpp  
YourObject.YourMethod()  
{  
    CultureInfo saveCulture = Thread.CurrentThread.CurrentUICulture;  
    try
    {  
        try
        {  
            Thread.CurrentThread.CurrentUICulture = new CultureInfo("de-DE");  
            // Do something that throws an exception.  
        }  
        finally
        {  
            Thread.CurrentThread.CurrentUICulture = saveCulture;  
        }  
    }  
    catch { throw; }  
}  
```  
  
## <a name="see-also"></a><span data-ttu-id="f68bd-122">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="f68bd-122">See also</span></span>

- [<span data-ttu-id="f68bd-123">Wytyczne dotyczące bezpiecznego programowania</span><span class="sxs-lookup"><span data-stu-id="f68bd-123">Secure Coding Guidelines</span></span>](../../standard/security/secure-coding-guidelines.md)
