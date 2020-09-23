---
title: Deklaracja zmiennej
ms.date: 07/20/2015
helpviewer_keywords:
- variables [Visual Basic], declaring
- member variables [Visual Basic], declarations
- Dim statement [Visual Basic], variable declaration
- declaring variables [Visual Basic]
- variables [Visual Basic], scope
- variables [Visual Basic], data types
- data types [Visual Basic], variable declarations
- lifetime [Visual Basic], variables
- variables [Visual Basic], lifetime
- access levels [Visual Basic], variables
- scope [Visual Basic], declaration statements
- variables [Visual Basic], access level
- local variables [Visual Basic], declarations
- scope [Visual Basic], variables
ms.assetid: d8f10226-92b1-480f-9f53-df377b2d7e15
ms.openlocfilehash: 8d78509e1604fee4a151608f6166de6fc8ccfdaa
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/23/2020
ms.locfileid: "91080156"
---
# <a name="variable-declaration-in-visual-basic"></a><span data-ttu-id="936bf-102">Deklaracja zmiennej w Visual Basic</span><span class="sxs-lookup"><span data-stu-id="936bf-102">Variable Declaration in Visual Basic</span></span>

<span data-ttu-id="936bf-103">Należy zadeklarować zmienną, aby określić jej nazwę i cechy.</span><span class="sxs-lookup"><span data-stu-id="936bf-103">You declare a variable to specify its name and characteristics.</span></span> <span data-ttu-id="936bf-104">Instrukcja deklaracji dla zmiennych jest [instrukcją Dim](../../../language-reference/statements/dim-statement.md).</span><span class="sxs-lookup"><span data-stu-id="936bf-104">The declaration statement for variables is the [Dim Statement](../../../language-reference/statements/dim-statement.md).</span></span> <span data-ttu-id="936bf-105">Jego lokalizacja i zawartość określają cechy zmiennych.</span><span class="sxs-lookup"><span data-stu-id="936bf-105">Its location and contents determine the variable's characteristics.</span></span>  
  
 <span data-ttu-id="936bf-106">Aby poznać zmienne reguły nazewnictwa i zagadnienia, zobacz [zadeklarowane nazwy elementów](../declared-elements/declared-element-names.md).</span><span class="sxs-lookup"><span data-stu-id="936bf-106">For variable naming rules and considerations, see [Declared Element Names](../declared-elements/declared-element-names.md).</span></span>  
  
## <a name="declaration-levels"></a><span data-ttu-id="936bf-107">Poziomy deklaracji</span><span class="sxs-lookup"><span data-stu-id="936bf-107">Declaration Levels</span></span>  
  
### <a name="local-and-member-variables"></a><span data-ttu-id="936bf-108">Zmienne lokalne i Członkowskie</span><span class="sxs-lookup"><span data-stu-id="936bf-108">Local and Member Variables</span></span>  

 <span data-ttu-id="936bf-109">*Zmienna lokalna* jest taka, która jest zadeklarowana w ramach procedury.</span><span class="sxs-lookup"><span data-stu-id="936bf-109">A *local variable* is one that is declared within a procedure.</span></span> <span data-ttu-id="936bf-110">*Zmienna członkowska* jest elementem członkowskim typu Visual Basic; jest on zadeklarowany na poziomie modułu, wewnątrz klasy, struktury lub modułu, ale nie w żadnej procedurze wewnętrznej dla tej klasy, struktury lub modułu.</span><span class="sxs-lookup"><span data-stu-id="936bf-110">A *member variable* is a member of a Visual Basic type; it is declared at module level, inside a class, structure, or module, but not within any procedure internal to that class, structure, or module.</span></span>  
  
### <a name="shared-and-instance-variables"></a><span data-ttu-id="936bf-111">Zmienne udostępnione i wystąpienia</span><span class="sxs-lookup"><span data-stu-id="936bf-111">Shared and Instance Variables</span></span>  

 <span data-ttu-id="936bf-112">W klasie lub strukturze Kategoria zmiennej składowej zależy od tego, czy jest ona udostępniona.</span><span class="sxs-lookup"><span data-stu-id="936bf-112">In a class or structure, the category of a member variable depends on whether or not it is shared.</span></span> <span data-ttu-id="936bf-113">Jeśli jest zadeklarowany za pomocą słowa kluczowego [Shared](../../../language-reference/modifiers/shared.md) , jest to *zmienna udostępniona*i istnieje w pojedynczej kopii współdzielonej między wszystkimi wystąpieniami klasy lub struktury.</span><span class="sxs-lookup"><span data-stu-id="936bf-113">If it is declared with the [Shared](../../../language-reference/modifiers/shared.md) keyword, it is a *shared variable*, and it exists in a single copy shared among all instances of the class or structure.</span></span>  
  
 <span data-ttu-id="936bf-114">W przeciwnym razie jest to *zmienna wystąpienia*, a oddzielna kopia jest tworzona dla każdego wystąpienia klasy lub struktury.</span><span class="sxs-lookup"><span data-stu-id="936bf-114">Otherwise it is an *instance variable*, and a separate copy of it is created for each instance of the class or structure.</span></span> <span data-ttu-id="936bf-115">Dana kopia zmiennej wystąpienia jest dostępna tylko dla wystąpienia klasy lub struktury, w której została utworzona.</span><span class="sxs-lookup"><span data-stu-id="936bf-115">A given copy of an instance variable is available only to the instance of the class or structure in which it was created.</span></span> <span data-ttu-id="936bf-116">Jest on niezależny od kopii zmiennej wystąpienia w innym wystąpieniu klasy lub struktury.</span><span class="sxs-lookup"><span data-stu-id="936bf-116">It is independent of a copy of the instance variable in any other instance of the class or structure.</span></span>  
  
## <a name="declaring-data-type"></a><span data-ttu-id="936bf-117">Deklarowanie typu danych</span><span class="sxs-lookup"><span data-stu-id="936bf-117">Declaring Data Type</span></span>  

 <span data-ttu-id="936bf-118">Klauzula [as](../../../language-reference/statements/as-clause.md) w instrukcji deklaracji umożliwia zdefiniowanie typu danych lub typu obiektu deklarowanej zmiennej.</span><span class="sxs-lookup"><span data-stu-id="936bf-118">The [As](../../../language-reference/statements/as-clause.md) clause in the declaration statement allows you to define the data type or object type of the variable you are declaring.</span></span> <span data-ttu-id="936bf-119">Można określić dowolny z następujących typów dla zmiennej:</span><span class="sxs-lookup"><span data-stu-id="936bf-119">You can specify any of the following types for a variable:</span></span>  
  
- <span data-ttu-id="936bf-120">Podstawowy typ danych, taki jak `Boolean` , `Long` , lub `Decimal`</span><span class="sxs-lookup"><span data-stu-id="936bf-120">An elementary data type, such as `Boolean`, `Long`, or `Decimal`</span></span>  
  
- <span data-ttu-id="936bf-121">Złożony typ danych, taki jak tablica lub struktura</span><span class="sxs-lookup"><span data-stu-id="936bf-121">A composite data type, such as an array or structure</span></span>  
  
- <span data-ttu-id="936bf-122">Typ obiektu lub Klasa, zdefiniowane w aplikacji lub w innej aplikacji</span><span class="sxs-lookup"><span data-stu-id="936bf-122">An object type, or class, defined either in your application or in another application</span></span>  
  
- <span data-ttu-id="936bf-123">Klasa .NET Framework, taka jak <xref:System.Windows.Forms.Label> lub <xref:System.Windows.Forms.TextBox></span><span class="sxs-lookup"><span data-stu-id="936bf-123">A .NET Framework class, such as <xref:System.Windows.Forms.Label> or <xref:System.Windows.Forms.TextBox></span></span>  
  
- <span data-ttu-id="936bf-124">Typ interfejsu, taki jak <xref:System.IComparable> lub <xref:System.IDisposable></span><span class="sxs-lookup"><span data-stu-id="936bf-124">An interface type, such as <xref:System.IComparable> or <xref:System.IDisposable></span></span>  
  
 <span data-ttu-id="936bf-125">Można zadeklarować kilka zmiennych w jednej instrukcji bez konieczności powtarzania typu danych.</span><span class="sxs-lookup"><span data-stu-id="936bf-125">You can declare several variables in one statement without having to repeat the data type.</span></span> <span data-ttu-id="936bf-126">W poniższych instrukcjach zmienne `i` , `j` , i `k` są zadeklarowane jako typ `Integer` , i `l` `m` `Long` `x` i `y` jako `Single` :</span><span class="sxs-lookup"><span data-stu-id="936bf-126">In the following statements, the variables `i`, `j`, and `k` are declared as type `Integer`, `l` and `m` as `Long`, and `x` and `y` as `Single`:</span></span>  
  
```vb  
Dim i, j, k As Integer  
' All three variables in the preceding statement are declared as Integer.  
Dim l, m As Long, x, y As Single  
' In the preceding statement, l and m are Long, x and y are Single.  
```  
  
 <span data-ttu-id="936bf-127">Aby uzyskać więcej informacji na temat typów danych, zobacz [typy danych](../data-types/index.md).</span><span class="sxs-lookup"><span data-stu-id="936bf-127">For more information on data types, see [Data Types](../data-types/index.md).</span></span> <span data-ttu-id="936bf-128">Aby uzyskać więcej informacji na temat obiektów, zobacz [obiekty i klasy](../objects-and-classes/index.md) i [Programowanie za pomocą składników](/previous-versions/visualstudio/visual-studio-2013/0ffkdtkf(v=vs.120)).</span><span class="sxs-lookup"><span data-stu-id="936bf-128">For more information on objects, see [Objects and Classes](../objects-and-classes/index.md) and [Programming with Components](/previous-versions/visualstudio/visual-studio-2013/0ffkdtkf(v=vs.120)).</span></span>  
  
## <a name="local-type-inference"></a><span data-ttu-id="936bf-129">Wnioskowanie o typie lokalnym</span><span class="sxs-lookup"><span data-stu-id="936bf-129">Local Type Inference</span></span>  

 <span data-ttu-id="936bf-130">*Wnioskowanie o typie* służy do określania typów danych zmiennych lokalnych zadeklarowanych bez `As` klauzuli.</span><span class="sxs-lookup"><span data-stu-id="936bf-130">*Type inference* is used to determine the data types of local variables declared without an `As` clause.</span></span> <span data-ttu-id="936bf-131">Kompilator wnioskuje typ zmiennej z typu wyrażenia inicjowania.</span><span class="sxs-lookup"><span data-stu-id="936bf-131">The compiler infers the type of the variable from the type of the initialization expression.</span></span> <span data-ttu-id="936bf-132">Dzięki temu można zadeklarować zmienne bez jawnego stwierdzenia typu.</span><span class="sxs-lookup"><span data-stu-id="936bf-132">This enables you to declare variables without explicitly stating a type.</span></span> <span data-ttu-id="936bf-133">W poniższym przykładzie zarówno, jak `num1` i `num2` są jednoznacznie wpisane jako liczby całkowite.</span><span class="sxs-lookup"><span data-stu-id="936bf-133">In the following example, both `num1` and `num2` are strongly typed as integers.</span></span>  
  
 [!code-vb[VbVbalrTypeInference#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrTypeInference/VB/Class1.vb#1)]  
  
 <span data-ttu-id="936bf-134">Jeśli chcesz użyć wnioskowania o typie lokalnym, `Option Infer` należy ustawić wartość `On` .</span><span class="sxs-lookup"><span data-stu-id="936bf-134">If you want to use local type inference, `Option Infer` must be set to `On`.</span></span> <span data-ttu-id="936bf-135">Aby uzyskać więcej informacji, zobacz [lokalne wnioskowanie o typie](local-type-inference.md) i [zestawienie opcji](../../../language-reference/statements/option-infer-statement.md).</span><span class="sxs-lookup"><span data-stu-id="936bf-135">For more information, see [Local Type Inference](local-type-inference.md) and [Option Infer Statement](../../../language-reference/statements/option-infer-statement.md).</span></span>  
  
## <a name="characteristics-of-declared-variables"></a><span data-ttu-id="936bf-136">Charakterystyki zadeklarowanych zmiennych</span><span class="sxs-lookup"><span data-stu-id="936bf-136">Characteristics of Declared Variables</span></span>  

 <span data-ttu-id="936bf-137">Okres *istnienia* zmiennej to okres czasu, w którym jest dostępny do użycia.</span><span class="sxs-lookup"><span data-stu-id="936bf-137">The *lifetime* of a variable is the period of time during which it is available for use.</span></span> <span data-ttu-id="936bf-138">Ogólnie rzecz biorąc, zmienna istnieje, tak długo, jak element, który deklaruje go (na przykład procedura lub Klasa), nadal istnieje.</span><span class="sxs-lookup"><span data-stu-id="936bf-138">In general, a variable exists as long as the element that declares it (such as a procedure or class) continues to exist.</span></span> <span data-ttu-id="936bf-139">Jeśli zmienna nie musi kontynuować istniejących poza okresem istnienia elementu zawierającego, nie trzeba wykonywać żadnych specjalnych w deklaracji.</span><span class="sxs-lookup"><span data-stu-id="936bf-139">If the variable does not need to continue existing beyond the lifetime of its containing element, you do not need to do anything special in the declaration.</span></span> <span data-ttu-id="936bf-140">Jeśli zmienna musi nadal istnieć dłużej niż jej element zawierający, można `Static` `Shared` w jej instrukcji uwzględnić słowo kluczowe or `Dim` .</span><span class="sxs-lookup"><span data-stu-id="936bf-140">If the variable needs to continue to exist longer than its containing element, you can include the `Static` or `Shared` keyword in its `Dim` statement.</span></span> <span data-ttu-id="936bf-141">Aby uzyskać więcej informacji, zobacz [okres istnienia w Visual Basic](../declared-elements/lifetime.md).</span><span class="sxs-lookup"><span data-stu-id="936bf-141">For more information, see [Lifetime in Visual Basic](../declared-elements/lifetime.md).</span></span>  
  
 <span data-ttu-id="936bf-142">*Zakres* zmiennej to zestaw wszystkich kodów, które mogą odwoływać się do niego bez zakwalifikowania jego nazwy.</span><span class="sxs-lookup"><span data-stu-id="936bf-142">The *scope* of a variable is the set of all code that can refer to it without qualifying its name.</span></span> <span data-ttu-id="936bf-143">Zakres zmiennej jest określany na podstawie tego, gdzie jest zadeklarowany.</span><span class="sxs-lookup"><span data-stu-id="936bf-143">A variable's scope is determined by where it is declared.</span></span> <span data-ttu-id="936bf-144">Kod znajdujący się w danym regionie może używać zmiennych zdefiniowanych w tym regionie bez konieczności kwalifikowania ich nazw.</span><span class="sxs-lookup"><span data-stu-id="936bf-144">Code located in a given region can use the variables defined in that region without having to qualify their names.</span></span> <span data-ttu-id="936bf-145">Aby uzyskać więcej informacji, zobacz [zakres w Visual Basic](../declared-elements/scope.md).</span><span class="sxs-lookup"><span data-stu-id="936bf-145">For more information, see [Scope in Visual Basic](../declared-elements/scope.md).</span></span>  
  
 <span data-ttu-id="936bf-146">*Poziom dostępu* do zmiennej to zakres kodu, który ma uprawnienia dostępu do niego.</span><span class="sxs-lookup"><span data-stu-id="936bf-146">A variable's *access level* is the extent of code that has permission to access it.</span></span> <span data-ttu-id="936bf-147">Jest to określane przez modyfikator dostępu (na przykład [Public](../../../language-reference/modifiers/public.md) lub [Private](../../../language-reference/modifiers/private.md)), który jest używany w `Dim` instrukcji.</span><span class="sxs-lookup"><span data-stu-id="936bf-147">This is determined by the access modifier (such as [Public](../../../language-reference/modifiers/public.md) or [Private](../../../language-reference/modifiers/private.md)) that you use in the `Dim` statement.</span></span> <span data-ttu-id="936bf-148">Aby uzyskać więcej informacji, zobacz [poziomy dostępu w Visual Basic](../declared-elements/access-levels.md).</span><span class="sxs-lookup"><span data-stu-id="936bf-148">For more information, see [Access levels in Visual Basic](../declared-elements/access-levels.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="936bf-149">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="936bf-149">See also</span></span>

- [<span data-ttu-id="936bf-150">Porady: tworzenie nowej zmiennej</span><span class="sxs-lookup"><span data-stu-id="936bf-150">How to: Create a New Variable</span></span>](how-to-create-a-new-variable.md)
- [<span data-ttu-id="936bf-151">Porady: przenoszenie danych do zmiennej i z niej</span><span class="sxs-lookup"><span data-stu-id="936bf-151">How to: Move Data Into and Out of a Variable</span></span>](how-to-move-data-into-and-out-of-a-variable.md)
- [<span data-ttu-id="936bf-152">Typy danych</span><span class="sxs-lookup"><span data-stu-id="936bf-152">Data Types</span></span>](../../../language-reference/data-types/index.md)
- [<span data-ttu-id="936bf-153">Chronione</span><span class="sxs-lookup"><span data-stu-id="936bf-153">Protected</span></span>](../../../language-reference/modifiers/protected.md)
- [<span data-ttu-id="936bf-154">Friend</span><span class="sxs-lookup"><span data-stu-id="936bf-154">Friend</span></span>](../../../language-reference/modifiers/friend.md)
- [<span data-ttu-id="936bf-155">Statyczny</span><span class="sxs-lookup"><span data-stu-id="936bf-155">Static</span></span>](../../../language-reference/modifiers/static.md)
- [<span data-ttu-id="936bf-156">Charakterystyka zadeklarowanych elementów</span><span class="sxs-lookup"><span data-stu-id="936bf-156">Declared Element Characteristics</span></span>](../declared-elements/declared-element-characteristics.md)
- [<span data-ttu-id="936bf-157">Wnioskowanie o typie lokalnym</span><span class="sxs-lookup"><span data-stu-id="936bf-157">Local Type Inference</span></span>](local-type-inference.md)
- [<span data-ttu-id="936bf-158">Option Infer — Instrukcja</span><span class="sxs-lookup"><span data-stu-id="936bf-158">Option Infer Statement</span></span>](../../../language-reference/statements/option-infer-statement.md)
