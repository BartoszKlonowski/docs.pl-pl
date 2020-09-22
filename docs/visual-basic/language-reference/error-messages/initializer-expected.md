---
title: Oczekiwano inicjatora
ms.date: 07/20/2015
f1_keywords:
- vbc30996
- bc30996
helpviewer_keywords:
- BC30996
ms.assetid: 6e183fe0-8888-43ed-a062-01571079455f
ms.openlocfilehash: 2c5a65443dc16a600e25fcf6dfd11c4597b3a086
ms.sourcegitcommit: d2db216e46323f73b32ae312c9e4135258e5d68e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "90873951"
---
# <a name="initializer-expected"></a><span data-ttu-id="d394c-102">Oczekiwano inicjatora</span><span class="sxs-lookup"><span data-stu-id="d394c-102">Initializer expected</span></span>

<span data-ttu-id="d394c-103">Podjęto próbę zadeklarować wystąpienie klasy za pomocą inicjatora obiektu, w którym lista inicjalizacji jest pusta, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="d394c-103">You have tried to declare an instance of a class by using an object initializer in which the initialization list is empty, as shown in the following example.</span></span>  
  
 `' Not valid.`  
  
 `' Dim aStudent As New Student With {}`  
  
 <span data-ttu-id="d394c-104">Na liście inicjatorów musi być zainicjowana co najmniej jedno pole lub właściwość, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="d394c-104">At least one field or property must be initialized in the initializer list, as shown in the following example.</span></span>  
  
 `Dim aStudent As New Student With {.year = "Senior"}`  
  
 <span data-ttu-id="d394c-105">**Identyfikator błędu:** BC30996</span><span class="sxs-lookup"><span data-stu-id="d394c-105">**Error ID:** BC30996</span></span>  
  
## <a name="to-correct-this-error"></a><span data-ttu-id="d394c-106">Aby poprawić ten błąd</span><span class="sxs-lookup"><span data-stu-id="d394c-106">To correct this error</span></span>  
  
1. <span data-ttu-id="d394c-107">Zainicjuj co najmniej jedno pole lub właściwość w inicjatorze lub nie używaj inicjatora obiektów.</span><span class="sxs-lookup"><span data-stu-id="d394c-107">Initialize at least one field or property in the initializer, or do not use an object initializer.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="d394c-108">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="d394c-108">See also</span></span>

- [<span data-ttu-id="d394c-109">Inicjatory obiektów: typy nazwane i anonimowe</span><span class="sxs-lookup"><span data-stu-id="d394c-109">Object Initializers: Named and Anonymous Types</span></span>](../../programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)
- [<span data-ttu-id="d394c-110">Instrukcje: deklarowanie obiektu za pomocą inicjatora obiektów</span><span class="sxs-lookup"><span data-stu-id="d394c-110">How to: Declare an Object by Using an Object Initializer</span></span>](../../programming-guide/language-features/objects-and-classes/how-to-declare-an-object-by-using-an-object-initializer.md)
