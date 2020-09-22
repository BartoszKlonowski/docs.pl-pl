---
title: Elementu <keyword>
ms.date: 07/20/2015
f1_keywords:
- vb.ModuleAttribute
helpviewer_keywords:
- Module keyword [Visual Basic]
- Module modifier
- attribute blocks, Module keyword
ms.assetid: d971b940-05ab-4d56-8485-e3b8a661906b
ms.openlocfilehash: 6c4f24ad161302835be683e9d324ce32b16c4087
ms.sourcegitcommit: d2db216e46323f73b32ae312c9e4135258e5d68e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "90867979"
---
# <a name="module-keyword-visual-basic"></a><span data-ttu-id="0f221-102">Module \<keyword> (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="0f221-102">Module \<keyword> (Visual Basic)</span></span>

<span data-ttu-id="0f221-103">Określa, że atrybut na początku pliku źródłowego dotyczy bieżącego modułu zestawu.</span><span class="sxs-lookup"><span data-stu-id="0f221-103">Specifies that an attribute at the beginning of a source file applies to the current assembly module.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="0f221-104">Uwagi</span><span class="sxs-lookup"><span data-stu-id="0f221-104">Remarks</span></span>  

 <span data-ttu-id="0f221-105">Wiele atrybutów odnosi się do pojedynczego elementu programistycznego, takiego jak Klasa lub właściwość.</span><span class="sxs-lookup"><span data-stu-id="0f221-105">Many attributes pertain to an individual programming element, such as a class or property.</span></span> <span data-ttu-id="0f221-106">Ten atrybut jest stosowany przez dołączenie bloku atrybutu w nawiasach kątowych ( `< >` ) bezpośrednio do instrukcji deklaracji.</span><span class="sxs-lookup"><span data-stu-id="0f221-106">You apply such an attribute by attaching the attribute block, within angle brackets (`< >`), directly to the declaration statement.</span></span>  
  
 <span data-ttu-id="0f221-107">Jeśli atrybut dotyczy nie tylko następującego elementu, ale do bieżącego modułu zestawu, umieścisz blok atrybutu na początku pliku źródłowego i zidentyfikujesz atrybut za pomocą `Module` słowa kluczowego.</span><span class="sxs-lookup"><span data-stu-id="0f221-107">If an attribute pertains not only to the following element but to the current assembly module, you place the attribute block at the beginning of the source file and identify the attribute with the `Module` keyword.</span></span> <span data-ttu-id="0f221-108">Jeśli dotyczy całego zestawu, użyj słowa kluczowego [Assembly](assembly.md) .</span><span class="sxs-lookup"><span data-stu-id="0f221-108">If it applies to the entire assembly, you use the [Assembly](assembly.md) keyword.</span></span>  
  
 <span data-ttu-id="0f221-109">`Module`Modyfikator nie jest taki sam jak [instrukcja modułu](../statements/module-statement.md).</span><span class="sxs-lookup"><span data-stu-id="0f221-109">The `Module` modifier is not the same as the [Module Statement](../statements/module-statement.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="0f221-110">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="0f221-110">See also</span></span>

- [<span data-ttu-id="0f221-111">Zestaw</span><span class="sxs-lookup"><span data-stu-id="0f221-111">Assembly</span></span>](assembly.md)
- [<span data-ttu-id="0f221-112">Module — Instrukcja</span><span class="sxs-lookup"><span data-stu-id="0f221-112">Module Statement</span></span>](../statements/module-statement.md)
- [<span data-ttu-id="0f221-113">Przegląd atrybutów</span><span class="sxs-lookup"><span data-stu-id="0f221-113">Attributes overview</span></span>](../../programming-guide/concepts/attributes/index.md)
