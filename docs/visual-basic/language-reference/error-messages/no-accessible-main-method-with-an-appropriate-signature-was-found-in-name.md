---
title: W elemencie „<name>” nie odnaleziono dostępnej metody „Main” z odpowiednim podpisem.
ms.date: 07/20/2015
f1_keywords:
- bc30737
- vbc30737
helpviewer_keywords:
- BC30737
ms.assetid: 3f40bacd-3fac-4741-b204-852f693d4340
ms.openlocfilehash: e1f95484a153bdcac9543508b7f2708dc6b7d942
ms.sourcegitcommit: ff5a4eb5cffbcac9521bc44a907a118cd7e8638d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2020
ms.locfileid: "92160044"
---
# <a name="bc30737-no-accessible-main-method-with-an-appropriate-signature-was-found-in-name"></a><span data-ttu-id="7ad43-102">BC30737: w elemencie "" nie znaleziono dostępnej metody "Main" z odpowiednim podpisem. \<name></span><span class="sxs-lookup"><span data-stu-id="7ad43-102">BC30737: No accessible 'Main' method with an appropriate signature was found in '\<name>'</span></span>

<span data-ttu-id="7ad43-103">Aplikacje wiersza polecenia muszą mieć `Sub Main` zdefiniowany.</span><span class="sxs-lookup"><span data-stu-id="7ad43-103">Command-line applications must have a `Sub Main` defined.</span></span> <span data-ttu-id="7ad43-104">`Main` musi być zadeklarowany tak, jakby `Public Shared` jest zdefiniowana w klasie lub tak, jakby została `Public` zdefiniowana w module.</span><span class="sxs-lookup"><span data-stu-id="7ad43-104">`Main` must be declared as `Public Shared` if it is defined in a class, or as `Public` if defined in a module.</span></span>

 <span data-ttu-id="7ad43-105">**Identyfikator błędu:** BC30737</span><span class="sxs-lookup"><span data-stu-id="7ad43-105">**Error ID:** BC30737</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="7ad43-106">Aby poprawić ten błąd</span><span class="sxs-lookup"><span data-stu-id="7ad43-106">To correct this error</span></span>

- <span data-ttu-id="7ad43-107">Zdefiniuj `Public Sub Main` procedurę dla projektu.</span><span class="sxs-lookup"><span data-stu-id="7ad43-107">Define a `Public Sub Main` procedure for your project.</span></span> <span data-ttu-id="7ad43-108">Zadeklaruj go jako `Shared` if i tylko wtedy, gdy zdefiniujesz go wewnątrz klasy.</span><span class="sxs-lookup"><span data-stu-id="7ad43-108">Declare it as `Shared` if and only if you define it inside a class.</span></span>

## <a name="see-also"></a><span data-ttu-id="7ad43-109">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="7ad43-109">See also</span></span>

- [<span data-ttu-id="7ad43-110">Struktura programu Visual Basic</span><span class="sxs-lookup"><span data-stu-id="7ad43-110">Structure of a Visual Basic Program</span></span>](../../programming-guide/program-structure/structure-of-a-visual-basic-program.md)
- [<span data-ttu-id="7ad43-111">Procedury</span><span class="sxs-lookup"><span data-stu-id="7ad43-111">Procedures</span></span>](../../programming-guide/language-features/procedures/index.md)
