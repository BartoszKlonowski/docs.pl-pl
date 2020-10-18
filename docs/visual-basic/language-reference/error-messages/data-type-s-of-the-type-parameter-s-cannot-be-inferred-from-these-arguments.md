---
title: Na podstawie tych argumentów nie można wywnioskować typów danych parametrów typu
ms.date: 07/20/2015
f1_keywords:
- bc36644
- bc36647
- vbc36647
- vbc36644
helpviewer_keywords:
- BC36644
- BC36647
ms.assetid: 0e0050f2-2039-4311-b260-f0ebfde84189
ms.openlocfilehash: 85798e6453bc6cea6174ecc536b35835865e0459
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2020
ms.locfileid: "92163457"
---
# <a name="bc36647-and-bc36644-data-types-of-the-type-parameters-cannot-be-inferred-from-these-arguments"></a><span data-ttu-id="cd51d-102">BC36647 i BC36644: na podstawie tych argumentów nie można wywnioskować typów danych parametrów typu</span><span class="sxs-lookup"><span data-stu-id="cd51d-102">BC36647 and BC36644: Data type(s) of the type parameter(s) cannot be inferred from these arguments</span></span>

<span data-ttu-id="cd51d-103">Na podstawie tych argumentów nie można wywnioskować typów danych parametrów typu.</span><span class="sxs-lookup"><span data-stu-id="cd51d-103">Data type(s) of the type parameter(s) cannot be inferred from these arguments.</span></span> <span data-ttu-id="cd51d-104">Jawne określenie typów danych może naprawić ten błąd.</span><span class="sxs-lookup"><span data-stu-id="cd51d-104">Specifying the data type(s) explicitly might correct this error.</span></span>

<span data-ttu-id="cd51d-105">Ten błąd występuje, gdy Rozpoznanie przeciążenia nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="cd51d-105">This error occurs when overload resolution has failed.</span></span> <span data-ttu-id="cd51d-106">Występuje jako komunikat podrzędny informujący o tym, dlaczego określony kandydat przeciążenia został wyeliminowany.</span><span class="sxs-lookup"><span data-stu-id="cd51d-106">It occurs as a subordinate message that states why a particular overload candidate has been eliminated.</span></span> <span data-ttu-id="cd51d-107">W komunikacie o błędzie wyjaśniono, że kompilator nie może użyć wnioskowania typu w celu znalezienia typów danych dla parametrów typu.</span><span class="sxs-lookup"><span data-stu-id="cd51d-107">The error message explains that the compiler cannot use type inference to find data types for the type parameters.</span></span>

> [!NOTE]
> <span data-ttu-id="cd51d-108">Gdy określenie argumentów nie jest opcją (na przykład w przypadku operatorów zapytań w wyrażeniach zapytań), komunikat o błędzie jest wyświetlany bez drugiego zdania.</span><span class="sxs-lookup"><span data-stu-id="cd51d-108">When specifying arguments is not an option (for example, for query operators in query expressions), the error message appears without the second sentence.</span></span>

<span data-ttu-id="cd51d-109">Poniższy kod ilustruje błąd.</span><span class="sxs-lookup"><span data-stu-id="cd51d-109">The following code demonstrates the error.</span></span>

```vb
Module Module1

    Sub Main()

        '' Not Valid.
        'OverloadedGenericMethod("Hello", "World")

    End Sub

    Sub OverloadedGenericMethod(Of T)(ByVal x As String,
                                      ByVal y As InterfaceExample(Of T))
    End Sub

    Sub OverloadedGenericMethod(Of T, R)(ByVal x As T,
                                         ByVal y As InterfaceExample(Of R))
    End Sub

End Module

Interface InterfaceExample(Of T)
End Interface
```

<span data-ttu-id="cd51d-110">**Identyfikator błędu:** BC36647 i BC36644</span><span class="sxs-lookup"><span data-stu-id="cd51d-110">**Error ID:** BC36647 and BC36644</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="cd51d-111">Aby poprawić ten błąd</span><span class="sxs-lookup"><span data-stu-id="cd51d-111">To correct this error</span></span>

<span data-ttu-id="cd51d-112">Możesz określić typ danych dla parametru lub parametrów typu, zamiast polegać na wnioskach o typie.</span><span class="sxs-lookup"><span data-stu-id="cd51d-112">You may be able to specify a data type for the type parameter or parameters instead of relying on type inference.</span></span>

## <a name="see-also"></a><span data-ttu-id="cd51d-113">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="cd51d-113">See also</span></span>

- [<span data-ttu-id="cd51d-114">Swobodna konwersja delegatów</span><span class="sxs-lookup"><span data-stu-id="cd51d-114">Relaxed Delegate Conversion</span></span>](../../programming-guide/language-features/delegates/relaxed-delegate-conversion.md)
- [<span data-ttu-id="cd51d-115">Procedury ogólne w Visual Basic</span><span class="sxs-lookup"><span data-stu-id="cd51d-115">Generic Procedures in Visual Basic</span></span>](../../programming-guide/language-features/data-types/generic-procedures.md)
- [<span data-ttu-id="cd51d-116">Konwersje plików w Visual Basic</span><span class="sxs-lookup"><span data-stu-id="cd51d-116">Type Conversions in Visual Basic</span></span>](../../programming-guide/language-features/data-types/type-conversions.md)
