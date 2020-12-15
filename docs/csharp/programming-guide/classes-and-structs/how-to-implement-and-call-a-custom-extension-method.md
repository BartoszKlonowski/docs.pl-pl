---
title: Jak zaimplementować i wywołać metodę rozszerzenia niestandardowego — Przewodnik programowania w języku C#
description: Dowiedz się, jak zaimplementować metody rozszerzenia dla dowolnego typu .NET. Kod klienta może korzystać z metod przez dodanie odwołania do biblioteki DLL i dodanie dyrektywy using.
ms.date: 07/20/2015
helpviewer_keywords:
- extension methods [C#], implementing and calling
ms.topic: how-to
ms.custom: contperf-fy21q2
ms.assetid: 7dab2a56-cf8e-4a47-a444-fe610a02772a
ms.openlocfilehash: 4ae48a05d451a3276b3a0f2ee4d6c633ce7db306
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2020
ms.locfileid: "97513016"
---
# <a name="how-to-implement-and-call-a-custom-extension-method-c-programming-guide"></a><span data-ttu-id="b9459-104">Implementowanie i wywoływanie niestandardowej metody rozszerzenia (Przewodnik programowania w języku C#)</span><span class="sxs-lookup"><span data-stu-id="b9459-104">How to implement and call a custom extension method (C# Programming Guide)</span></span>

<span data-ttu-id="b9459-105">W tym temacie przedstawiono sposób implementacji własnych metod rozszerzenia dla dowolnego typu .NET.</span><span class="sxs-lookup"><span data-stu-id="b9459-105">This topic shows how to implement your own extension methods for any .NET type.</span></span> <span data-ttu-id="b9459-106">Kod klienta może korzystać z metod rozszerzenia przez dodanie odwołania do biblioteki DLL, która zawiera te metody, i dodanie dyrektywy [using](../../language-reference/keywords/using-directive.md) , która określa przestrzeń nazw, w której są zdefiniowane metody rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="b9459-106">Client code can use your extension methods by adding a reference to the DLL that contains them, and adding a [using](../../language-reference/keywords/using-directive.md) directive that specifies the namespace in which the extension methods are defined.</span></span>  
  
## <a name="to-define-and-call-the-extension-method"></a><span data-ttu-id="b9459-107">Aby zdefiniować i wywołać metodę rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="b9459-107">To define and call the extension method</span></span>  
  
1. <span data-ttu-id="b9459-108">Zdefiniuj [klasę](./static-classes-and-static-class-members.md) statyczną, aby zawierała metodę rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="b9459-108">Define a static [class](./static-classes-and-static-class-members.md) to contain the extension method.</span></span>  
  
     <span data-ttu-id="b9459-109">Klasa musi być widoczna dla kodu klienta.</span><span class="sxs-lookup"><span data-stu-id="b9459-109">The class must be visible to client code.</span></span> <span data-ttu-id="b9459-110">Aby uzyskać więcej informacji na temat reguł ułatwień dostępu, zobacz [Modyfikatory dostępu](./access-modifiers.md).</span><span class="sxs-lookup"><span data-stu-id="b9459-110">For more information about accessibility rules, see [Access Modifiers](./access-modifiers.md).</span></span>  
  
2. <span data-ttu-id="b9459-111">Zaimplementuj metodę rozszerzenia jako metodę statyczną z co najmniej taką samą widocznością jak zawierająca klasy.</span><span class="sxs-lookup"><span data-stu-id="b9459-111">Implement the extension method as a static method with at least the same visibility as the containing class.</span></span>  
  
3. <span data-ttu-id="b9459-112">Pierwszy parametr metody Określa typ, na którym działa Metoda; musi być poprzedzony [tym](../../language-reference/keywords/this.md) modyfikatorem.</span><span class="sxs-lookup"><span data-stu-id="b9459-112">The first parameter of the method specifies the type that the method operates on; it must be preceded with the [this](../../language-reference/keywords/this.md) modifier.</span></span>  
  
4. <span data-ttu-id="b9459-113">W kodzie wywołującym Dodaj dyrektywę, `using` Aby określić [przestrzeń nazw](../../language-reference/keywords/namespace.md) , która zawiera klasę metody rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="b9459-113">In the calling code, add a `using` directive to specify the [namespace](../../language-reference/keywords/namespace.md) that contains the extension method class.</span></span>  
  
5. <span data-ttu-id="b9459-114">Wywołaj metody tak, jakby były metodami wystąpień w typie.</span><span class="sxs-lookup"><span data-stu-id="b9459-114">Call the methods as if they were instance methods on the type.</span></span>  
  
     <span data-ttu-id="b9459-115">Należy zauważyć, że pierwszy parametr nie jest określony przez wywołanie kodu, ponieważ reprezentuje typ, na którym jest stosowany operator, a kompilator już zna typ obiektu.</span><span class="sxs-lookup"><span data-stu-id="b9459-115">Note that the first parameter is not specified by calling code because it represents the type on which the operator is being applied, and the compiler already knows the type of your object.</span></span> <span data-ttu-id="b9459-116">Musisz podać argumenty dla parametrów 2 przez `n` .</span><span class="sxs-lookup"><span data-stu-id="b9459-116">You only have to provide arguments for parameters 2 through `n`.</span></span>  
  
## <a name="example"></a><span data-ttu-id="b9459-117">Przykład</span><span class="sxs-lookup"><span data-stu-id="b9459-117">Example</span></span>  

 <span data-ttu-id="b9459-118">Poniższy przykład implementuje metodę rozszerzającą o nazwie `WordCount` w `CustomExtensions.StringExtension` klasie.</span><span class="sxs-lookup"><span data-stu-id="b9459-118">The following example implements an extension method named `WordCount` in the `CustomExtensions.StringExtension` class.</span></span> <span data-ttu-id="b9459-119">Metoda działa na <xref:System.String> klasie, która jest określona jako pierwszy parametr metody.</span><span class="sxs-lookup"><span data-stu-id="b9459-119">The method operates on the <xref:System.String> class, which is specified as the first method parameter.</span></span> <span data-ttu-id="b9459-120">`CustomExtensions`Przestrzeń nazw jest importowana do przestrzeni nazw aplikacji, a metoda jest wywoływana wewnątrz `Main` metody.</span><span class="sxs-lookup"><span data-stu-id="b9459-120">The `CustomExtensions` namespace is imported into the application namespace, and the method is called inside the `Main` method.</span></span>  
  
 [!code-csharp[csProgGuideExtensionMethods#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideExtensionMethods/cs/extensionmethods.cs#1)]  
  
## <a name="net-security"></a><span data-ttu-id="b9459-121">Zabezpieczenia platformy .NET</span><span class="sxs-lookup"><span data-stu-id="b9459-121">.NET Security</span></span>  

 <span data-ttu-id="b9459-122">Metody rozszerzające nie stwarzają określonych luk w zabezpieczeniach.</span><span class="sxs-lookup"><span data-stu-id="b9459-122">Extension methods present no specific security vulnerabilities.</span></span> <span data-ttu-id="b9459-123">Nigdy nie mogą być używane do personifikacji istniejących metod dla typu, ponieważ wszystkie kolizje nazw są rozwiązywane na korzyść wystąpienia lub statycznej metody zdefiniowanej przez sam typ.</span><span class="sxs-lookup"><span data-stu-id="b9459-123">They can never be used to impersonate existing methods on a type, because all name collisions are resolved in favor of the instance or static method defined by the type itself.</span></span> <span data-ttu-id="b9459-124">Metody rozszerzające nie mogą uzyskać dostępu do żadnych prywatnych danych w klasie rozszerzonej.</span><span class="sxs-lookup"><span data-stu-id="b9459-124">Extension methods cannot access any private data in the extended class.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="b9459-125">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="b9459-125">See also</span></span>

- [<span data-ttu-id="b9459-126">Przewodnik programowania w języku C#</span><span class="sxs-lookup"><span data-stu-id="b9459-126">C# Programming Guide</span></span>](../index.md)
- [<span data-ttu-id="b9459-127">Metody rozszerzania</span><span class="sxs-lookup"><span data-stu-id="b9459-127">Extension Methods</span></span>](./extension-methods.md)
- [<span data-ttu-id="b9459-128">LINQ (zapytanie zintegrowane z językiem)</span><span class="sxs-lookup"><span data-stu-id="b9459-128">LINQ (Language-Integrated Query)</span></span>](../../linq/linq-in-csharp.md)
- [<span data-ttu-id="b9459-129">Klasy statyczne i statyczni członkowie klas</span><span class="sxs-lookup"><span data-stu-id="b9459-129">Static Classes and Static Class Members</span></span>](./static-classes-and-static-class-members.md)
- [<span data-ttu-id="b9459-130">protected</span><span class="sxs-lookup"><span data-stu-id="b9459-130">protected</span></span>](../../language-reference/keywords/protected.md)
- [<span data-ttu-id="b9459-131">internal</span><span class="sxs-lookup"><span data-stu-id="b9459-131">internal</span></span>](../../language-reference/keywords/internal.md)
- [<span data-ttu-id="b9459-132">public</span><span class="sxs-lookup"><span data-stu-id="b9459-132">public</span></span>](../../language-reference/keywords/public.md)
- [<span data-ttu-id="b9459-133">this</span><span class="sxs-lookup"><span data-stu-id="b9459-133">this</span></span>](../../language-reference/keywords/this.md)
- [<span data-ttu-id="b9459-134">obszaru</span><span class="sxs-lookup"><span data-stu-id="b9459-134">namespace</span></span>](../../language-reference/keywords/namespace.md)
