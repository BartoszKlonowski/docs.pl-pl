---
title: Zmienna „<variablename>” jest używana, zanim zostanie do niej przypisana wartość
ms.date: 07/20/2015
f1_keywords:
- vbc42104
- BC42104
helpviewer_keywords:
- BC42104
ms.assetid: 6909aa0b-b4a1-46f5-a18c-ba3e565c1dd8
ms.openlocfilehash: a60afe0907e974dfb345d20d18762cb5f84127d9
ms.sourcegitcommit: d2db216e46323f73b32ae312c9e4135258e5d68e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "90875038"
---
# <a name="variable-variablename-is-used-before-it-has-been-assigned-a-value"></a><span data-ttu-id="fd3b7-102">Zmienna „\<variablename>” jest używana, zanim zostanie do niej przypisana wartość</span><span class="sxs-lookup"><span data-stu-id="fd3b7-102">Variable '\<variablename>' is used before it has been assigned a value</span></span>

<span data-ttu-id="fd3b7-103">Zmienna " \<variablename> " jest używana przed przypisaniem do niej wartości.</span><span class="sxs-lookup"><span data-stu-id="fd3b7-103">Variable '\<variablename>' is used before it has been assigned a value.</span></span> <span data-ttu-id="fd3b7-104">Wyjątek odwołania o wartości null może wynikać w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="fd3b7-104">A null reference exception could result at run time.</span></span>  
  
 <span data-ttu-id="fd3b7-105">Aplikacja ma co najmniej jedną możliwą ścieżkę za pomocą kodu, który odczytuje zmienną przed przypisaniem do niej żadnej wartości.</span><span class="sxs-lookup"><span data-stu-id="fd3b7-105">An application has at least one possible path through its code that reads a variable before any value is assigned to it.</span></span>  
  
 <span data-ttu-id="fd3b7-106">Jeśli zmienna nie ma przypisanej wartości, ma wartość domyślną dla tego typu danych.</span><span class="sxs-lookup"><span data-stu-id="fd3b7-106">If a variable has never been assigned a value, it holds the default value for its data type.</span></span> <span data-ttu-id="fd3b7-107">Dla typu danych referencyjnych wartość domyślna to [Nothing](../nothing.md).</span><span class="sxs-lookup"><span data-stu-id="fd3b7-107">For a reference data type, that default value is [Nothing](../nothing.md).</span></span> <span data-ttu-id="fd3b7-108">Odczytywanie zmiennej odniesienia, która ma wartość, `Nothing` może spowodować wystąpienie <xref:System.NullReferenceException> w pewnych okolicznościach.</span><span class="sxs-lookup"><span data-stu-id="fd3b7-108">Reading a reference variable that has a value of `Nothing` can cause a <xref:System.NullReferenceException> in some circumstances.</span></span>  
  
 <span data-ttu-id="fd3b7-109">Domyślnie ten komunikat jest ostrzeżeniem.</span><span class="sxs-lookup"><span data-stu-id="fd3b7-109">By default, this message is a warning.</span></span> <span data-ttu-id="fd3b7-110">Aby uzyskać więcej informacji na temat ukrywania ostrzeżeń lub leczenia ostrzeżeń jako błędów, zobacz [Konfigurowanie ostrzeżeń w Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic).</span><span class="sxs-lookup"><span data-stu-id="fd3b7-110">For more information on hiding warnings or treating warnings as errors, see [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic).</span></span>  
  
 <span data-ttu-id="fd3b7-111">**Identyfikator błędu:** BC42104</span><span class="sxs-lookup"><span data-stu-id="fd3b7-111">**Error ID:** BC42104</span></span>  
  
## <a name="to-correct-this-error"></a><span data-ttu-id="fd3b7-112">Aby poprawić ten błąd</span><span class="sxs-lookup"><span data-stu-id="fd3b7-112">To correct this error</span></span>  
  
- <span data-ttu-id="fd3b7-113">Sprawdź logikę przepływu sterowania i upewnij się, że zmienna ma prawidłową wartość przed przekazaniem kontroli do dowolnej instrukcji, która odczytuje ją.</span><span class="sxs-lookup"><span data-stu-id="fd3b7-113">Check your control flow logic and make sure the variable has a valid value before control passes to any statement that reads it.</span></span>  
  
- <span data-ttu-id="fd3b7-114">Jednym ze sposobów zagwarantowania, że zmienna zawsze ma prawidłową wartość, jest zainicjowanie jej jako części swojej deklaracji.</span><span class="sxs-lookup"><span data-stu-id="fd3b7-114">One way to guarantee that the variable always has a valid value is to initialize it as part of its declaration.</span></span> <span data-ttu-id="fd3b7-115">Zobacz "Inicjalizacja" w [instrukcji Dim](../statements/dim-statement.md).</span><span class="sxs-lookup"><span data-stu-id="fd3b7-115">See "Initialization" in [Dim Statement](../statements/dim-statement.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="fd3b7-116">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="fd3b7-116">See also</span></span>

- [<span data-ttu-id="fd3b7-117">Dim, instrukcja</span><span class="sxs-lookup"><span data-stu-id="fd3b7-117">Dim Statement</span></span>](../statements/dim-statement.md)
- [<span data-ttu-id="fd3b7-118">Deklaracja zmiennej</span><span class="sxs-lookup"><span data-stu-id="fd3b7-118">Variable Declaration</span></span>](../../programming-guide/language-features/variables/variable-declaration.md)
- [<span data-ttu-id="fd3b7-119">Rozwiązywanie problemów związanych ze zmiennymi</span><span class="sxs-lookup"><span data-stu-id="fd3b7-119">Troubleshooting Variables</span></span>](../../programming-guide/language-features/variables/troubleshooting-variables.md)
