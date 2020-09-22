---
title: Instrukcje „Module” mogą wystąpić tylko na poziomie pliku lub przestrzeni nazw
ms.date: 07/20/2015
f1_keywords:
- bc30617
- vbc30617
helpviewer_keywords:
- BC30617
ms.assetid: 5e9de8e5-d26b-4fb2-9e28-814413fe9cef
ms.openlocfilehash: 91e6c81bb64c259411cbef8a36629b8b320ea584
ms.sourcegitcommit: d2db216e46323f73b32ae312c9e4135258e5d68e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "90873751"
---
# <a name="module-statements-can-occur-only-at-file-or-namespace-level"></a><span data-ttu-id="88561-102">Instrukcje „Module” mogą wystąpić tylko na poziomie pliku lub przestrzeni nazw</span><span class="sxs-lookup"><span data-stu-id="88561-102">'Module' statements can occur only at file or namespace level</span></span>

<span data-ttu-id="88561-103">`Module` instrukcje muszą pojawić się w górnej części pliku źródłowego bezpośrednio po `Option` i `Imports` instrukcjach, atrybutach globalnych i deklaracjach przestrzeni nazw, ale przed wszystkimi innymi deklaracjami.</span><span class="sxs-lookup"><span data-stu-id="88561-103">`Module` statements must appear at the top of your source file immediately after `Option` and `Imports` statements, global attributes, and namespace declarations, but before all other declarations.</span></span>  
  
 <span data-ttu-id="88561-104">**Identyfikator błędu:** BC30617</span><span class="sxs-lookup"><span data-stu-id="88561-104">**Error ID:** BC30617</span></span>  
  
## <a name="to-correct-this-error"></a><span data-ttu-id="88561-105">Aby poprawić ten błąd</span><span class="sxs-lookup"><span data-stu-id="88561-105">To correct this error</span></span>  
  
- <span data-ttu-id="88561-106">Przenieś `Module` instrukcję do początku deklaracji przestrzeni nazw lub pliku źródłowego.</span><span class="sxs-lookup"><span data-stu-id="88561-106">Move the `Module` statement to the top of your namespace declaration or source file.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="88561-107">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="88561-107">See also</span></span>

- [<span data-ttu-id="88561-108">Module — Instrukcja</span><span class="sxs-lookup"><span data-stu-id="88561-108">Module Statement</span></span>](../statements/module-statement.md)
