---
title: Używanie obsługi wyjątków filtrowanej przez użytkownika
description: Dowiedz się, jak korzystać z obsługi wyjątków filtrowanych przez użytkownika w językach C# i Visual Basic.
ms.date: 12/14/2020
helpviewer_keywords:
- user-filtered exceptions
- exceptions, user-filtered
dev_langs:
- csharp
- vb
ms.openlocfilehash: 2dba43ad2fc685a6555ab43fc973814fd7f359a3
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2020
ms.locfileid: "97512674"
---
# <a name="use-user-filtered-exception-handlers"></a><span data-ttu-id="cf10c-103">Używanie obsługi wyjątków filtrowanej przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="cf10c-103">Use user-filtered exception handlers</span></span>

<span data-ttu-id="cf10c-104">Programy obsługi wyjątków filtrowane przez użytkownika przechwytują i obsługują wyjątki na podstawie wymagań zdefiniowanych dla wyjątku.</span><span class="sxs-lookup"><span data-stu-id="cf10c-104">User-filtered exception handlers catch and handle exceptions based on requirements you define for the exception.</span></span> <span data-ttu-id="cf10c-105">Te programy obsługi wykorzystują `catch` instrukcję ze `when` słowem kluczowym ( `Catch` i `When` w Visual Basic).</span><span class="sxs-lookup"><span data-stu-id="cf10c-105">These handlers use the `catch` statement with the `when` keyword (`Catch` and `When` in Visual Basic).</span></span>  
  
 <span data-ttu-id="cf10c-106">Ta technika jest przydatna, gdy określony obiekt wyjątku odnosi się do wielu błędów.</span><span class="sxs-lookup"><span data-stu-id="cf10c-106">This technique is useful when a particular exception object corresponds to multiple errors.</span></span> <span data-ttu-id="cf10c-107">W takim przypadku obiekt ma zazwyczaj właściwość, która zawiera konkretny kod błędu skojarzony z błędem.</span><span class="sxs-lookup"><span data-stu-id="cf10c-107">In this case, the object typically has a property that contains the specific error code associated with the error.</span></span> <span data-ttu-id="cf10c-108">Możesz użyć właściwości kod błędu w wyrażeniu, aby wybrać tylko konkretny błąd, który ma być obsługiwany w tej `catch` klauzuli.</span><span class="sxs-lookup"><span data-stu-id="cf10c-108">You can use the error code property in the expression to select only the particular error you want to handle in that `catch` clause.</span></span>  
  
 <span data-ttu-id="cf10c-109">Poniższy przykład ilustruje `catch` / `when` instrukcję.</span><span class="sxs-lookup"><span data-stu-id="cf10c-109">The following example illustrates the `catch`/`when` statement.</span></span>

```csharp
try
{
    //Try statements.  
}
catch (Exception ex) when (ex.Message.Contains("404"))
{
    //Catch statements.
}
```  
  
```vb
Try  
    'Try statements.  
    Catch When Err = VBErr_ClassLoadException
    'Catch statements.
End Try  
```  
  
 <span data-ttu-id="cf10c-110">Wyrażenie filtrowanej przez użytkownika klauzuli nie jest w żaden sposób ograniczone.</span><span class="sxs-lookup"><span data-stu-id="cf10c-110">The expression of the user-filtered clause is not restricted in any way.</span></span> <span data-ttu-id="cf10c-111">Jeśli wystąpi wyjątek podczas wykonywania wyrażenia filtrowanego przez użytkownika, ten wyjątek zostanie odrzucony i wyrażenie filtru jest uważane za szacowane na wartość false.</span><span class="sxs-lookup"><span data-stu-id="cf10c-111">If an exception occurs during execution of the user-filtered expression, that exception is discarded and the filter expression is considered to have evaluated to false.</span></span> <span data-ttu-id="cf10c-112">W takim przypadku środowisko uruchomieniowe języka wspólnego kontynuuje wyszukiwanie programu obsługi dla bieżącego wyjątku.</span><span class="sxs-lookup"><span data-stu-id="cf10c-112">In this case, the common language runtime continues the search for a handler for the current exception.</span></span>  
  
## <a name="combine-the-specific-exception-and-the-user-filtered-clauses"></a><span data-ttu-id="cf10c-113">Połącz określony wyjątek i klauzule filtrowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="cf10c-113">Combine the specific exception and the user-filtered clauses</span></span>  

 <span data-ttu-id="cf10c-114">`catch`Instrukcja może zawierać zarówno konkretny wyjątek, jak i filtrowane przez użytkownika klauzule.</span><span class="sxs-lookup"><span data-stu-id="cf10c-114">A `catch` statement can contain both the specific exception and the user-filtered clauses.</span></span> <span data-ttu-id="cf10c-115">Środowisko uruchomieniowe najpierw sprawdza konkretny wyjątek.</span><span class="sxs-lookup"><span data-stu-id="cf10c-115">The runtime tests the specific exception first.</span></span> <span data-ttu-id="cf10c-116">Jeśli konkretny wyjątek się powiedzie, środowisko uruchomieniowe wykonuje filtr użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cf10c-116">If the specific exception succeeds, the runtime executes the user filter.</span></span> <span data-ttu-id="cf10c-117">Filtr generyczny może zawierać odwołanie do zmiennej zadeklarowanej w filtrze klas.</span><span class="sxs-lookup"><span data-stu-id="cf10c-117">The generic filter can contain a reference to the variable declared in the class filter.</span></span> <span data-ttu-id="cf10c-118">Należy zauważyć, że nie można odwrócić kolejności dwóch klauzul filtru.</span><span class="sxs-lookup"><span data-stu-id="cf10c-118">Note that the order of the two filter clauses cannot be reversed.</span></span>  
  
 <span data-ttu-id="cf10c-119">Poniższy przykład pokazuje konkretny wyjątek w instrukcji **catch** , a także klauzulę filtrowana przez użytkownika przy użyciu słowa kluczowego **when** .</span><span class="sxs-lookup"><span data-stu-id="cf10c-119">The following example shows a specific exception in the **catch** statement as well as the user-filtered clause using the **when** keyword.</span></span>  
  
```csharp
try
{
    //Try statements.  
}
catch (System.Net.Http.HttpRequestException ex) when (ex.Message.Contains("404"))
{
    //Catch statements.
}
```  
  
```vb
Try  
    'Try statements.
    Catch cle As ClassLoadException When cle.IsRecoverable()  
    'Catch statements.
End Try  
```  

## <a name="see-also"></a><span data-ttu-id="cf10c-120">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="cf10c-120">See also</span></span>

- [<span data-ttu-id="cf10c-121">Wyjątki</span><span class="sxs-lookup"><span data-stu-id="cf10c-121">Exceptions</span></span>](index.md)
