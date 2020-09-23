---
title: Promocja typu
ms.date: 07/20/2015
helpviewer_keywords:
- declared elements [Visual Basic], scope
- visibility [Visual Basic], declared elements
- Partial keyword [Visual Basic], unexpected results with type promotion
- scope [Visual Basic], declared elements
- scope [Visual Basic], Visual Basic
- type promotion
- declared elements [Visual Basic], visibility
ms.assetid: 035eeb15-e4c5-4288-ab3c-6bd5d22f7051
ms.openlocfilehash: 6c28ca22e96616ff09e147400bfdb2adb922ff0e
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/23/2020
ms.locfileid: "91085805"
---
# <a name="type-promotion-visual-basic"></a><span data-ttu-id="6338a-102">Promocja typu (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="6338a-102">Type Promotion (Visual Basic)</span></span>

<span data-ttu-id="6338a-103">Kiedy deklarujesz element programowania w module, Visual Basic promuje swój zakres do przestrzeni nazw zawierającej moduł.</span><span class="sxs-lookup"><span data-stu-id="6338a-103">When you declare a programming element in a module, Visual Basic promotes its scope to the namespace containing the module.</span></span> <span data-ttu-id="6338a-104">Jest to tzw. *Promocja typu*.</span><span class="sxs-lookup"><span data-stu-id="6338a-104">This is known as *type promotion*.</span></span>  
  
 <span data-ttu-id="6338a-105">Poniższy przykład przedstawia definicję szkieletu modułu i dwóch członków tego modułu.</span><span class="sxs-lookup"><span data-stu-id="6338a-105">The following example shows a skeleton definition of a module and two members of that module.</span></span>  
  
 [!code-vb[VbVbalrDeclaredElements#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDeclaredElements/VB/Class1.vb#1)]  
  
 <span data-ttu-id="6338a-106">W programie `projModule` elementy programistyczne zadeklarowane na poziomie modułu są podwyższane do `projNamespace` .</span><span class="sxs-lookup"><span data-stu-id="6338a-106">Within `projModule`, programming elements declared at module level are promoted to `projNamespace`.</span></span> <span data-ttu-id="6338a-107">W poprzednim przykładzie `basicEnum` i `innerClass` są awansowane, ale `numberSub` nie jest, ponieważ nie jest zadeklarowany na poziomie modułu.</span><span class="sxs-lookup"><span data-stu-id="6338a-107">In the preceding example, `basicEnum` and `innerClass` are promoted, but `numberSub` is not, because it is not declared at module level.</span></span>  
  
## <a name="effect-of-type-promotion"></a><span data-ttu-id="6338a-108">Efekt promocji typu</span><span class="sxs-lookup"><span data-stu-id="6338a-108">Effect of Type Promotion</span></span>  

 <span data-ttu-id="6338a-109">Efektem promocji typu jest to, że ciąg kwalifikacji nie musi zawierać nazwy modułu.</span><span class="sxs-lookup"><span data-stu-id="6338a-109">The effect of type promotion is that a qualification string does not need to include the module name.</span></span> <span data-ttu-id="6338a-110">Poniższy przykład wykonuje dwa wywołania procedury w poprzednim przykładzie.</span><span class="sxs-lookup"><span data-stu-id="6338a-110">The following example makes two calls to the procedure in the preceding example.</span></span>  
  
 [!code-vb[VbVbalrDeclaredElements#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDeclaredElements/VB/Class1.vb#2)]  
  
 <span data-ttu-id="6338a-111">W poprzednim przykładzie pierwsze wywołanie używa kompletnych ciągów kwalifikacyjnych.</span><span class="sxs-lookup"><span data-stu-id="6338a-111">In the preceding example, the first call uses complete qualification strings.</span></span> <span data-ttu-id="6338a-112">Nie jest to jednak konieczne ze względu na promocję typu.</span><span class="sxs-lookup"><span data-stu-id="6338a-112">However, this is not necessary because of type promotion.</span></span> <span data-ttu-id="6338a-113">Drugie wywołanie również uzyskuje dostęp do członków modułu bez uwzględniania ich `projModule` w ciągach kwalifikacji.</span><span class="sxs-lookup"><span data-stu-id="6338a-113">The second call also accesses the module's members without including `projModule` in the qualification strings.</span></span>  
  
## <a name="defeat-of-type-promotion"></a><span data-ttu-id="6338a-114">Sprawowanie promocji typu</span><span class="sxs-lookup"><span data-stu-id="6338a-114">Defeat of Type Promotion</span></span>  

 <span data-ttu-id="6338a-115">Jeśli przestrzeń nazw ma już element członkowski o takiej samej nazwie jak element członkowski modułu, podwyższanie poziomu dla tego elementu członkowskiego modułu zostanie poddana przeniesieniu.</span><span class="sxs-lookup"><span data-stu-id="6338a-115">If the namespace already has a member with the same name as a module member, type promotion is defeated for that module member.</span></span> <span data-ttu-id="6338a-116">Poniższy przykład przedstawia definicję szkieletu wyliczenia i modułu w tej samej przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="6338a-116">The following example shows a skeleton definition of an enumeration and a module within the same namespace.</span></span>  
  
 [!code-vb[VbVbalrDeclaredElements#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDeclaredElements/VB/Class1.vb#3)]  
  
 <span data-ttu-id="6338a-117">W poprzednim przykładzie Visual Basic nie można podwyższyć poziomu klasy `abc` do, `thisNameSpace` ponieważ istnieje już Wyliczenie o tej samej nazwie na poziomie przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="6338a-117">In the preceding example, Visual Basic cannot promote class `abc` to `thisNameSpace` because there is already an enumeration with the same name at namespace level.</span></span> <span data-ttu-id="6338a-118">Aby uzyskać dostęp `abcSub` , musisz użyć pełnego ciągu kwalifikacji `thisNamespace.thisModule.abc.abcSub` .</span><span class="sxs-lookup"><span data-stu-id="6338a-118">To access `abcSub`, you must use the full qualification string `thisNamespace.thisModule.abc.abcSub`.</span></span> <span data-ttu-id="6338a-119">Jednak Klasa `xyz` jest nadal promowana i można uzyskać do `xyzSub` niej dostęp przy użyciu krótszego ciągu kwalifikacji `thisNamespace.xyz.xyzSub` .</span><span class="sxs-lookup"><span data-stu-id="6338a-119">However, class `xyz` is still promoted, and you can access `xyzSub` with the shorter qualification string `thisNamespace.xyz.xyzSub`.</span></span>  
  
### <a name="defeat-of-type-promotion-for-partial-types"></a><span data-ttu-id="6338a-120">Sprawowanie promocji typu dla typów częściowych</span><span class="sxs-lookup"><span data-stu-id="6338a-120">Defeat of Type Promotion for Partial Types</span></span>  

 <span data-ttu-id="6338a-121">Jeśli klasa lub struktura wewnątrz modułu używa słowa kluczowego [częściowe](../../../language-reference/modifiers/partial.md) , promocja typu jest automatycznie obniżana dla tej klasy lub struktury, niezależnie od tego, czy przestrzeń nazw ma element członkowski o tej samej nazwie.</span><span class="sxs-lookup"><span data-stu-id="6338a-121">If a class or structure inside a module uses the [Partial](../../../language-reference/modifiers/partial.md) keyword, type promotion is automatically defeated for that class or structure, whether or not the namespace has a member with the same name.</span></span> <span data-ttu-id="6338a-122">Inne elementy w module nadal kwalifikują się do podwyższenia poziomu.</span><span class="sxs-lookup"><span data-stu-id="6338a-122">Other elements in the module are still eligible for type promotion.</span></span>  
  
 <span data-ttu-id="6338a-123">**Konsekwencj.**</span><span class="sxs-lookup"><span data-stu-id="6338a-123">**Consequences.**</span></span> <span data-ttu-id="6338a-124">Sprawność promocji typu częściowej definicji może spowodować nieoczekiwane wyniki, a nawet błędy kompilatora.</span><span class="sxs-lookup"><span data-stu-id="6338a-124">Defeat of type promotion of a partial definition can cause unexpected results and even compiler errors.</span></span> <span data-ttu-id="6338a-125">Poniższy przykład pokazuje szkieletowe definicje części klasy, z których jedna znajduje się w module.</span><span class="sxs-lookup"><span data-stu-id="6338a-125">The following example shows skeleton partial definitions of a class, one of which is inside a module.</span></span>  
  
 [!code-vb[VbVbalrDeclaredElements#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDeclaredElements/VB/Class1.vb#4)]  
  
 <span data-ttu-id="6338a-126">W poprzednim przykładzie deweloper może oczekiwać, że kompilator Scala dwie częściowe definicje `sampleClass` .</span><span class="sxs-lookup"><span data-stu-id="6338a-126">In the preceding example, the developer might expect the compiler to merge the two partial definitions of `sampleClass`.</span></span> <span data-ttu-id="6338a-127">Jednak kompilator nie rozważa podwyższania poziomu definicji częściowej `sampleModule` .</span><span class="sxs-lookup"><span data-stu-id="6338a-127">However, the compiler does not consider promotion for the partial definition inside `sampleModule`.</span></span> <span data-ttu-id="6338a-128">W związku z tym próbuje skompilować dwie osobne i odrębne klasy, zarówno nazwane, jak i `sampleClass` różne ścieżki kwalifikacji.</span><span class="sxs-lookup"><span data-stu-id="6338a-128">As a result, it attempts to compile two separate and distinct classes, both named `sampleClass` but with different qualification paths.</span></span>  
  
 <span data-ttu-id="6338a-129">Kompilator Scala definicje częściowe tylko wtedy, gdy ich w pełni kwalifikowane ścieżki są identyczne.</span><span class="sxs-lookup"><span data-stu-id="6338a-129">The compiler merges partial definitions only when their fully qualified paths are identical.</span></span>  
  
## <a name="recommendations"></a><span data-ttu-id="6338a-130">Zalecenia</span><span class="sxs-lookup"><span data-stu-id="6338a-130">Recommendations</span></span>  

 <span data-ttu-id="6338a-131">Poniższe zalecenia stanowią dobre rozwiązanie programistyczne.</span><span class="sxs-lookup"><span data-stu-id="6338a-131">The following recommendations represent good programming practice.</span></span>  
  
- <span data-ttu-id="6338a-132">**Unikatowe nazwy.**</span><span class="sxs-lookup"><span data-stu-id="6338a-132">**Unique Names.**</span></span> <span data-ttu-id="6338a-133">Jeśli masz pełną kontrolę nad nazewnictwem elementów programistycznych, zawsze dobrym pomysłem jest używanie unikatowych nazw wszędzie.</span><span class="sxs-lookup"><span data-stu-id="6338a-133">When you have full control over the naming of programming elements, it is always a good idea to use unique names everywhere.</span></span> <span data-ttu-id="6338a-134">Identyczne nazwy wymagają dodatkowej kwalifikacji i mogą utrudniać odczytywanie kodu.</span><span class="sxs-lookup"><span data-stu-id="6338a-134">Identical names require extra qualification and can make your code harder to read.</span></span> <span data-ttu-id="6338a-135">Mogą również prowadzić do delikatnych błędów i nieoczekiwanych wyników.</span><span class="sxs-lookup"><span data-stu-id="6338a-135">They can also lead to subtle errors and unexpected results.</span></span>  
  
- <span data-ttu-id="6338a-136">**Pełna kwalifikacje.**</span><span class="sxs-lookup"><span data-stu-id="6338a-136">**Full Qualification.**</span></span> <span data-ttu-id="6338a-137">Podczas pracy z modułami i innymi elementami w tym samym obszarze nazw najbezpieczniejszym podejściem jest zawsze używanie pełnej kwalifikacji dla wszystkich elementów programistycznych.</span><span class="sxs-lookup"><span data-stu-id="6338a-137">When you are working with modules and other elements in the same namespace, the safest approach is to always use full qualification for all programming elements.</span></span> <span data-ttu-id="6338a-138">Jeśli Promocja typu jest obniżana dla elementu członkowskiego modułu i nie masz w pełni kwalifikacji tego elementu członkowskiego, można przypadkowo uzyskać dostęp do innego elementu programistycznego.</span><span class="sxs-lookup"><span data-stu-id="6338a-138">If type promotion is defeated for a module member and you do not fully qualify that member, you could inadvertently access a different programming element.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="6338a-139">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="6338a-139">See also</span></span>

- [<span data-ttu-id="6338a-140">Module — Instrukcja</span><span class="sxs-lookup"><span data-stu-id="6338a-140">Module Statement</span></span>](../../../language-reference/statements/module-statement.md)
- [<span data-ttu-id="6338a-141">Namespace — Instrukcja</span><span class="sxs-lookup"><span data-stu-id="6338a-141">Namespace Statement</span></span>](../../../language-reference/statements/namespace-statement.md)
- [<span data-ttu-id="6338a-142">Częściowe</span><span class="sxs-lookup"><span data-stu-id="6338a-142">Partial</span></span>](../../../language-reference/modifiers/partial.md)
- [<span data-ttu-id="6338a-143">Zakres w Visual Basic</span><span class="sxs-lookup"><span data-stu-id="6338a-143">Scope in Visual Basic</span></span>](scope.md)
- [<span data-ttu-id="6338a-144">Instrukcje: kontrolowanie zakresu zmiennej</span><span class="sxs-lookup"><span data-stu-id="6338a-144">How to: Control the Scope of a Variable</span></span>](how-to-control-the-scope-of-a-variable.md)
- [<span data-ttu-id="6338a-145">Odwołania do elementów zadeklarowanych</span><span class="sxs-lookup"><span data-stu-id="6338a-145">References to Declared Elements</span></span>](references-to-declared-elements.md)
