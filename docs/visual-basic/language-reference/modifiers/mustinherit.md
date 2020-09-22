---
title: MustInherit
ms.date: 07/20/2015
f1_keywords:
- MustInherit
- vb.MustInherit
helpviewer_keywords:
- classes [Visual Basic], abstract
- MustInherit classes [Visual Basic], MustInherit keyword
- abstract classes [Visual Basic], MustInherit class
- MustInherit keyword [Visual Basic]
ms.assetid: b8f05185-90e3-4dd7-adc2-90d852fab5b4
ms.openlocfilehash: 6502da947ae331a26e66d8ce2dbcda46e4172a6e
ms.sourcegitcommit: d2db216e46323f73b32ae312c9e4135258e5d68e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "90867963"
---
# <a name="mustinherit-visual-basic"></a><span data-ttu-id="fd8c6-102">MustInherit (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="fd8c6-102">MustInherit (Visual Basic)</span></span>

<span data-ttu-id="fd8c6-103">Określa, że Klasa może być używana tylko jako klasa bazowa i że nie można bezpośrednio z niej tworzyć obiektów.</span><span class="sxs-lookup"><span data-stu-id="fd8c6-103">Specifies that a class can be used only as a base class and that you cannot create an object directly from it.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="fd8c6-104">Uwagi</span><span class="sxs-lookup"><span data-stu-id="fd8c6-104">Remarks</span></span>  

 <span data-ttu-id="fd8c6-105">Celem *klasy podstawowej* (znanej również jako *Klasa abstrakcyjna*) jest zdefiniowanie funkcji, która jest wspólna dla wszystkich klas pochodnych.</span><span class="sxs-lookup"><span data-stu-id="fd8c6-105">The purpose of a *base class* (also known as an *abstract class*) is to define functionality that is common to all the classes derived from it.</span></span> <span data-ttu-id="fd8c6-106">Spowoduje to zapisanie klas pochodnych przed koniecznością ponownego definiowania elementów wspólnych.</span><span class="sxs-lookup"><span data-stu-id="fd8c6-106">This saves the derived classes from having to redefine the common elements.</span></span> <span data-ttu-id="fd8c6-107">W niektórych przypadkach ta wspólna funkcja nie jest wystarczająca do tworzenia użytecznego obiektu, a każda klasa pochodna definiuje brakującą funkcję.</span><span class="sxs-lookup"><span data-stu-id="fd8c6-107">In some cases, this common functionality is not complete enough to make a usable object, and each derived class defines the missing functionality.</span></span> <span data-ttu-id="fd8c6-108">W takim przypadku kod zużywający ma tworzyć obiekty tylko z klas pochodnych.</span><span class="sxs-lookup"><span data-stu-id="fd8c6-108">In such a case, you want the consuming code to create objects only from the derived classes.</span></span> <span data-ttu-id="fd8c6-109">`MustInherit`Aby wymusić to, użyj klasy bazowej.</span><span class="sxs-lookup"><span data-stu-id="fd8c6-109">You use `MustInherit` on the base class to enforce this.</span></span>  
  
 <span data-ttu-id="fd8c6-110">Innym zastosowaniem `MustInherit` klasy jest ograniczenie zmiennej do zestawu powiązanych klas.</span><span class="sxs-lookup"><span data-stu-id="fd8c6-110">Another use of a `MustInherit` class is to restrict a variable to a set of related classes.</span></span> <span data-ttu-id="fd8c6-111">Można zdefiniować klasę bazową i utworzyć wszystkie powiązane z nią klasy.</span><span class="sxs-lookup"><span data-stu-id="fd8c6-111">You can define a base class and derive all these related classes from it.</span></span> <span data-ttu-id="fd8c6-112">Klasa bazowa nie musi udostępniać żadnych funkcji wspólnych dla wszystkich klas pochodnych, ale może być jako filtr do przypisywania wartości do zmiennych.</span><span class="sxs-lookup"><span data-stu-id="fd8c6-112">The base class does not need to provide any functionality common to all the derived classes, but it can serve as a filter for assigning values to variables.</span></span> <span data-ttu-id="fd8c6-113">Jeśli kod zużywający deklaruje zmienną jako klasę bazową, Visual Basic umożliwia przypisanie tylko obiektu z jednej z klas pochodnych do tej zmiennej.</span><span class="sxs-lookup"><span data-stu-id="fd8c6-113">If your consuming code declares a variable as the base class, Visual Basic allows you to assign only an object from one of the derived classes to that variable.</span></span>  
  
 <span data-ttu-id="fd8c6-114">.NET Framework definiuje kilka `MustInherit` klas, <xref:System.Array> <xref:System.Enum> , i <xref:System.ValueType> .</span><span class="sxs-lookup"><span data-stu-id="fd8c6-114">The .NET Framework defines several `MustInherit` classes, among them <xref:System.Array>, <xref:System.Enum>, and <xref:System.ValueType>.</span></span> <span data-ttu-id="fd8c6-115"><xref:System.ValueType> jest przykładem klasy bazowej, która ogranicza zmienną.</span><span class="sxs-lookup"><span data-stu-id="fd8c6-115"><xref:System.ValueType> is an example of a base class that restricts a variable.</span></span> <span data-ttu-id="fd8c6-116">Wszystkie typy wartości pochodzą od <xref:System.ValueType> .</span><span class="sxs-lookup"><span data-stu-id="fd8c6-116">All value types derive from <xref:System.ValueType>.</span></span> <span data-ttu-id="fd8c6-117">Jeśli zadeklarujesz zmienną jako <xref:System.ValueType> , można przypisać tylko typy wartości do tej zmiennej.</span><span class="sxs-lookup"><span data-stu-id="fd8c6-117">If you declare a variable as <xref:System.ValueType>, you can assign only value types to that variable.</span></span>  
  
## <a name="rules"></a><span data-ttu-id="fd8c6-118">Reguły</span><span class="sxs-lookup"><span data-stu-id="fd8c6-118">Rules</span></span>  
  
- <span data-ttu-id="fd8c6-119">**Kontekst deklaracji.**</span><span class="sxs-lookup"><span data-stu-id="fd8c6-119">**Declaration Context.**</span></span> <span data-ttu-id="fd8c6-120">Można użyć `MustInherit` tylko w `Class` instrukcji.</span><span class="sxs-lookup"><span data-stu-id="fd8c6-120">You can use `MustInherit` only in a `Class` statement.</span></span>  
  
- <span data-ttu-id="fd8c6-121">**Połączone modyfikatory.**</span><span class="sxs-lookup"><span data-stu-id="fd8c6-121">**Combined Modifiers.**</span></span> <span data-ttu-id="fd8c6-122">Nie można określić `MustInherit` razem z `NotInheritable` w tej samej deklaracji.</span><span class="sxs-lookup"><span data-stu-id="fd8c6-122">You cannot specify `MustInherit` together with `NotInheritable` in the same declaration.</span></span>  
  
## <a name="example"></a><span data-ttu-id="fd8c6-123">Przykład</span><span class="sxs-lookup"><span data-stu-id="fd8c6-123">Example</span></span>  

 <span data-ttu-id="fd8c6-124">Poniższy przykład ilustruje zarówno wymuszone dziedziczenie, jak i wymuszone przesłanianie.</span><span class="sxs-lookup"><span data-stu-id="fd8c6-124">The following example illustrates both forced inheritance and forced overriding.</span></span> <span data-ttu-id="fd8c6-125">Klasa bazowa `shape` definiuje zmienną `acrossLine` .</span><span class="sxs-lookup"><span data-stu-id="fd8c6-125">The base class `shape` defines a variable `acrossLine`.</span></span> <span data-ttu-id="fd8c6-126">Klasy `circle` i `square` pochodzą od `shape` .</span><span class="sxs-lookup"><span data-stu-id="fd8c6-126">The classes `circle` and `square` derive from `shape`.</span></span> <span data-ttu-id="fd8c6-127">Dziedziczą one definicję `acrossLine` , ale muszą definiować funkcję, `area` ponieważ obliczenia różnią się w zależności od typu kształtu.</span><span class="sxs-lookup"><span data-stu-id="fd8c6-127">They inherit the definition of `acrossLine`, but they must define the function `area` because that calculation is different for each kind of shape.</span></span>  
  
 [!code-vb[VbVbalrKeywords#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrKeywords/VB/Class1.vb#2)]  
  
 <span data-ttu-id="fd8c6-128">Można zadeklarować `shape1` `shape2` Typ `shape` .</span><span class="sxs-lookup"><span data-stu-id="fd8c6-128">You can declare `shape1` and `shape2` to be of type `shape`.</span></span> <span data-ttu-id="fd8c6-129">Nie można jednak utworzyć obiektu, ponieważ nie ma `shape` on funkcjonalności funkcji `area` i jest oznaczony `MustInherit` .</span><span class="sxs-lookup"><span data-stu-id="fd8c6-129">However, you cannot create an object from `shape` because it lacks the functionality of the function `area` and is marked `MustInherit`.</span></span>  
  
 <span data-ttu-id="fd8c6-130">Ponieważ są one deklarowane jako `shape` , zmienne `shape1` i `shape2` są ograniczone do obiektów z klas pochodnych `circle` i `square` .</span><span class="sxs-lookup"><span data-stu-id="fd8c6-130">Because they are declared as `shape`, the variables `shape1` and `shape2` are restricted to objects from the derived classes `circle` and `square`.</span></span> <span data-ttu-id="fd8c6-131">Visual Basic nie pozwala na przypisanie żadnych innych obiektów do tych zmiennych, co zapewnia wysoki poziom bezpieczeństwa typów.</span><span class="sxs-lookup"><span data-stu-id="fd8c6-131">Visual Basic does not allow you to assign any other object to these variables, which gives you a high level of type safety.</span></span>  
  
## <a name="usage"></a><span data-ttu-id="fd8c6-132">Użycie</span><span class="sxs-lookup"><span data-stu-id="fd8c6-132">Usage</span></span>  

 <span data-ttu-id="fd8c6-133">`MustInherit`Modyfikator może być używany w tym kontekście:</span><span class="sxs-lookup"><span data-stu-id="fd8c6-133">The `MustInherit` modifier can be used in this context:</span></span>  
  
 [<span data-ttu-id="fd8c6-134">Class, instrukcja</span><span class="sxs-lookup"><span data-stu-id="fd8c6-134">Class Statement</span></span>](../statements/class-statement.md)  
  
## <a name="see-also"></a><span data-ttu-id="fd8c6-135">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="fd8c6-135">See also</span></span>

- [<span data-ttu-id="fd8c6-136">Inherits — Instrukcja</span><span class="sxs-lookup"><span data-stu-id="fd8c6-136">Inherits Statement</span></span>](../statements/inherits-statement.md)
- [<span data-ttu-id="fd8c6-137">NotInheritable</span><span class="sxs-lookup"><span data-stu-id="fd8c6-137">NotInheritable</span></span>](notinheritable.md)
- [<span data-ttu-id="fd8c6-138">Słowa kluczowe</span><span class="sxs-lookup"><span data-stu-id="fd8c6-138">Keywords</span></span>](../keywords/index.md)
- [<span data-ttu-id="fd8c6-139">Podstawowe informacje o dziedziczeniu</span><span class="sxs-lookup"><span data-stu-id="fd8c6-139">Inheritance Basics</span></span>](../../programming-guide/language-features/objects-and-classes/inheritance-basics.md)
