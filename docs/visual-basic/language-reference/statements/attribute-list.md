---
title: Lista atrybutów
ms.date: 07/20/2015
helpviewer_keywords:
- attribute list
- attributes [Visual Basic], applying
ms.assetid: 5880073a-68a4-4b6b-8a07-ace32959a4e2
ms.openlocfilehash: e566239c56efa8ca8e83bff92486fec4c434e92b
ms.sourcegitcommit: d2db216e46323f73b32ae312c9e4135258e5d68e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "90874742"
---
# <a name="attribute-list-visual-basic"></a><span data-ttu-id="2671e-102">Lista atrybutów (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="2671e-102">Attribute List (Visual Basic)</span></span>

<span data-ttu-id="2671e-103">Określa atrybuty, które mają zostać zastosowane do zadeklarowanego elementu programowania.</span><span class="sxs-lookup"><span data-stu-id="2671e-103">Specifies the attributes to be applied to a declared programming element.</span></span> <span data-ttu-id="2671e-104">Wiele atrybutów jest oddzielonych przecinkami.</span><span class="sxs-lookup"><span data-stu-id="2671e-104">Multiple attributes are separated by commas.</span></span> <span data-ttu-id="2671e-105">Poniżej znajduje się składnia jednego atrybutu.</span><span class="sxs-lookup"><span data-stu-id="2671e-105">Following is the syntax for one attribute.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="2671e-106">Składnia</span><span class="sxs-lookup"><span data-stu-id="2671e-106">Syntax</span></span>  
  
```vb  
[ attributemodifier ] attributename [ ( attributearguments | attributeinitializer ) ]  
```  
  
## <a name="parts"></a><span data-ttu-id="2671e-107">Części</span><span class="sxs-lookup"><span data-stu-id="2671e-107">Parts</span></span>  

|||
|---|---|
|`attributemodifier`|<span data-ttu-id="2671e-108">Wymagane dla atrybutów zastosowanych na początku pliku źródłowego.</span><span class="sxs-lookup"><span data-stu-id="2671e-108">Required for attributes applied at the beginning of a source file.</span></span> <span data-ttu-id="2671e-109">Może to być [zestaw](../modifiers/assembly.md) lub [moduł](../modifiers/module-keyword.md).</span><span class="sxs-lookup"><span data-stu-id="2671e-109">Can be [Assembly](../modifiers/assembly.md) or [Module](../modifiers/module-keyword.md).</span></span>|
|`attributename`| <span data-ttu-id="2671e-110">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="2671e-110">Required.</span></span> <span data-ttu-id="2671e-111">Nazwa atrybutu.</span><span class="sxs-lookup"><span data-stu-id="2671e-111">Name of the attribute.</span></span>|
|`attributearguments`|<span data-ttu-id="2671e-112">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="2671e-112">Optional.</span></span> <span data-ttu-id="2671e-113">Lista argumentów pozycyjnych dla tego atrybutu.</span><span class="sxs-lookup"><span data-stu-id="2671e-113">List of positional arguments for this attribute.</span></span> <span data-ttu-id="2671e-114">Wiele argumentów jest oddzielonych przecinkami.</span><span class="sxs-lookup"><span data-stu-id="2671e-114">Multiple arguments are separated by commas.</span></span>|
|`attributeinitializer`|<span data-ttu-id="2671e-115">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="2671e-115">Optional.</span></span> <span data-ttu-id="2671e-116">Lista inicjatorów zmiennych lub właściwości dla tego atrybutu.</span><span class="sxs-lookup"><span data-stu-id="2671e-116">List of variable or property initializers for this attribute.</span></span> <span data-ttu-id="2671e-117">Wiele inicjatorów jest oddzielonych przecinkami.</span><span class="sxs-lookup"><span data-stu-id="2671e-117">Multiple initializers are separated by commas.</span></span>|
  
## <a name="remarks"></a><span data-ttu-id="2671e-118">Uwagi</span><span class="sxs-lookup"><span data-stu-id="2671e-118">Remarks</span></span>  

 <span data-ttu-id="2671e-119">Można zastosować jeden lub więcej atrybutów do niemal każdego elementu programistycznego (typy, procedury, właściwości i tak dalej).</span><span class="sxs-lookup"><span data-stu-id="2671e-119">You can apply one or more attributes to nearly any programming element (types, procedures, properties, and so forth).</span></span> <span data-ttu-id="2671e-120">Atrybuty są wyświetlane w metadanych zestawu i mogą ułatwić Dodawanie adnotacji do kodu lub określić sposób użycia określonego elementu programistycznego.</span><span class="sxs-lookup"><span data-stu-id="2671e-120">Attributes appear in your assembly's metadata, and they can help you annotate your code or specify how to use a particular programming element.</span></span> <span data-ttu-id="2671e-121">Można stosować atrybuty zdefiniowane przez Visual Basic i .NET Framework, a także definiować własne atrybuty.</span><span class="sxs-lookup"><span data-stu-id="2671e-121">You can apply attributes defined by Visual Basic and the .NET Framework, and you can define your own attributes.</span></span>  

 <span data-ttu-id="2671e-122">Aby uzyskać więcej informacji na temat sytuacji, w których należy używać atrybutów, zobacz [Omówienie atrybutów](../../programming-guide/concepts/attributes/index.md).</span><span class="sxs-lookup"><span data-stu-id="2671e-122">For more information on when to use attributes, see [Attributes overview](../../programming-guide/concepts/attributes/index.md).</span></span> <span data-ttu-id="2671e-123">Aby uzyskać informacje na temat nazw atrybutów, zobacz [zadeklarowane nazwy elementów](../../programming-guide/language-features/declared-elements/declared-element-names.md).</span><span class="sxs-lookup"><span data-stu-id="2671e-123">For information on attribute names, see [Declared Element Names](../../programming-guide/language-features/declared-elements/declared-element-names.md).</span></span>  
  
## <a name="rules"></a><span data-ttu-id="2671e-124">Reguły</span><span class="sxs-lookup"><span data-stu-id="2671e-124">Rules</span></span>  
  
- <span data-ttu-id="2671e-125">**Jęcia.**</span><span class="sxs-lookup"><span data-stu-id="2671e-125">**Placement.**</span></span> <span data-ttu-id="2671e-126">Atrybuty można stosować do najbardziej zadeklarowanych elementów programistycznych.</span><span class="sxs-lookup"><span data-stu-id="2671e-126">You can apply attributes to most declared programming elements.</span></span> <span data-ttu-id="2671e-127">Aby zastosować jeden lub więcej atrybutów, należy umieścić *blok atrybutu* na początku deklaracji elementu.</span><span class="sxs-lookup"><span data-stu-id="2671e-127">To apply one or more attributes, you place an *attribute block* at the beginning of the element declaration.</span></span> <span data-ttu-id="2671e-128">Każdy wpis na liście atrybutów określa atrybut, który ma zostać zastosowany, oraz modyfikator i argumenty, które są używane dla tego wywołania atrybutu.</span><span class="sxs-lookup"><span data-stu-id="2671e-128">Each entry in the attribute list specifies an attribute you wish to apply, and the modifier and arguments you are using for this invocation of the attribute.</span></span>  
  
- <span data-ttu-id="2671e-129">**Nawiasy ostre.**</span><span class="sxs-lookup"><span data-stu-id="2671e-129">**Angle Brackets.**</span></span> <span data-ttu-id="2671e-130">W przypadku podania listy atrybutów należy ująć ją w nawiasy ostre (" `<` " i " `>` ").</span><span class="sxs-lookup"><span data-stu-id="2671e-130">If you supply an attribute list, you must enclose it in angle brackets ("`<`" and "`>`").</span></span>  
  
- <span data-ttu-id="2671e-131">**Część deklaracji.**</span><span class="sxs-lookup"><span data-stu-id="2671e-131">**Part of the Declaration.**</span></span> <span data-ttu-id="2671e-132">Atrybut musi być częścią deklaracji elementu, a nie oddzielną instrukcją.</span><span class="sxs-lookup"><span data-stu-id="2671e-132">The attribute must be part of the element declaration, not a separate statement.</span></span> <span data-ttu-id="2671e-133">Można użyć sekwencji kontynuacji wiersza (" `_` ") w celu przedłużenia instrukcji deklaracji na wiele wierszy kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="2671e-133">You can use the line-continuation sequence (" `_`") to extend the declaration statement onto multiple source-code lines.</span></span>  
  
- <span data-ttu-id="2671e-134">**Modyfikatory.**</span><span class="sxs-lookup"><span data-stu-id="2671e-134">**Modifiers.**</span></span> <span data-ttu-id="2671e-135">Modyfikator atrybutu ( `Assembly` lub `Module` ) jest wymagany dla każdego atrybutu zastosowanego do elementu programowania na początku pliku źródłowego.</span><span class="sxs-lookup"><span data-stu-id="2671e-135">An attribute modifier (`Assembly` or `Module`) is required on every attribute applied to a programming element at the beginning of a source file.</span></span> <span data-ttu-id="2671e-136">Modyfikatory atrybutów są niedozwolone w przypadku atrybutów zastosowanych do elementów, które nie znajdują się na początku pliku źródłowego.</span><span class="sxs-lookup"><span data-stu-id="2671e-136">Attribute modifiers are not allowed on attributes applied to elements that are not at the beginning of a source file.</span></span>  
  
- <span data-ttu-id="2671e-137">**Argumentu.**</span><span class="sxs-lookup"><span data-stu-id="2671e-137">**Arguments.**</span></span> <span data-ttu-id="2671e-138">Wszystkie argumenty pozycyjne dla atrybutu muszą poprzedzać wszelkie inicjatory zmiennych lub właściwości.</span><span class="sxs-lookup"><span data-stu-id="2671e-138">All positional arguments for an attribute must precede any variable or property initializers.</span></span>  
  
## <a name="example"></a><span data-ttu-id="2671e-139">Przykład</span><span class="sxs-lookup"><span data-stu-id="2671e-139">Example</span></span>  

 <span data-ttu-id="2671e-140">Poniższy przykład stosuje <xref:System.Runtime.InteropServices.DllImportAttribute> atrybut do definicji szkieletowej `Function` procedury.</span><span class="sxs-lookup"><span data-stu-id="2671e-140">The following example applies the <xref:System.Runtime.InteropServices.DllImportAttribute> attribute to a skeleton definition of a `Function` procedure.</span></span>  
  
 [!code-vb[VbVbalrStatements#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#1)]  
  
 <span data-ttu-id="2671e-141"><xref:System.Runtime.InteropServices.DllImportAttribute> wskazuje, że procedura Attribute reprezentuje punkt wejścia w niezarządzanej bibliotece dołączanej dynamicznie (DLL).</span><span class="sxs-lookup"><span data-stu-id="2671e-141"><xref:System.Runtime.InteropServices.DllImportAttribute> indicates that the attributed procedure represents an entry point in an unmanaged dynamic-link library (DLL).</span></span> <span data-ttu-id="2671e-142">Atrybut dostarcza nazwę biblioteki DLL jako argument pozycyjny oraz inne informacje jako inicjatory zmiennych.</span><span class="sxs-lookup"><span data-stu-id="2671e-142">The attribute supplies the DLL name as a positional argument and the other information as variable initializers.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="2671e-143">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="2671e-143">See also</span></span>

- [<span data-ttu-id="2671e-144">Zestaw</span><span class="sxs-lookup"><span data-stu-id="2671e-144">Assembly</span></span>](../modifiers/assembly.md)
- [<span data-ttu-id="2671e-145">Elementu \<keyword></span><span class="sxs-lookup"><span data-stu-id="2671e-145">Module \<keyword></span></span>](../modifiers/module-keyword.md)
- [<span data-ttu-id="2671e-146">Przegląd atrybutów</span><span class="sxs-lookup"><span data-stu-id="2671e-146">Attributes overview</span></span>](../../programming-guide/concepts/attributes/index.md)
- [<span data-ttu-id="2671e-147">Instrukcje: Przerywanie i łączenie instrukcji w kodzie</span><span class="sxs-lookup"><span data-stu-id="2671e-147">How to: Break and Combine Statements in Code</span></span>](../../programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md)
