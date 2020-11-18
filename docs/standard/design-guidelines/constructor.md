---
title: Projekt konstruktora
ms.date: 10/22/2008
helpviewer_keywords:
- member design guidelines, constructors
- constructors, design guidelines
- instance constructors
- type constructors
- virtual members
- constructors, types
- parameterless constructors
- static constructors
ms.assetid: b4496afe-5fa7-4bb0-85ca-70b0ef21e6fc
ms.openlocfilehash: 27fb73aa01adf31117d1b82724873db3a03fd269
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "94821401"
---
# <a name="constructor-design"></a><span data-ttu-id="709f1-102">Projekt konstruktora</span><span class="sxs-lookup"><span data-stu-id="709f1-102">Constructor Design</span></span>

<span data-ttu-id="709f1-103">Istnieją dwa rodzaje konstruktorów: konstruktory typów i konstruktory wystąpień.</span><span class="sxs-lookup"><span data-stu-id="709f1-103">There are two kinds of constructors: type constructors and instance constructors.</span></span>

<span data-ttu-id="709f1-104">Konstruktory typów są statyczne i są uruchamiane przez środowisko CLR przed użyciem typu.</span><span class="sxs-lookup"><span data-stu-id="709f1-104">Type constructors are static and are run by the CLR before the type is used.</span></span> <span data-ttu-id="709f1-105">Konstruktory wystąpień są uruchamiane podczas tworzenia wystąpienia typu.</span><span class="sxs-lookup"><span data-stu-id="709f1-105">Instance constructors run when an instance of a type is created.</span></span>

<span data-ttu-id="709f1-106">Konstruktory typów nie mogą przyjmować żadnych parametrów.</span><span class="sxs-lookup"><span data-stu-id="709f1-106">Type constructors cannot take any parameters.</span></span> <span data-ttu-id="709f1-107">Konstruktory wystąpień mogą.</span><span class="sxs-lookup"><span data-stu-id="709f1-107">Instance constructors can.</span></span> <span data-ttu-id="709f1-108">Konstruktory wystąpień, które nie przyjmują żadnych parametrów, są często nazywane konstruktorami bez parametrów.</span><span class="sxs-lookup"><span data-stu-id="709f1-108">Instance constructors that don’t take any parameters are often called parameterless constructors.</span></span>

<span data-ttu-id="709f1-109">Konstruktory to najbardziej naturalny sposób tworzenia wystąpień typu.</span><span class="sxs-lookup"><span data-stu-id="709f1-109">Constructors are the most natural way to create instances of a type.</span></span> <span data-ttu-id="709f1-110">Większość deweloperów przeszuka i spróbuje użyć konstruktora przed uwzględnieniem alternatywnych sposobów tworzenia wystąpień (takich jak metody fabryki).</span><span class="sxs-lookup"><span data-stu-id="709f1-110">Most developers will search and try to use a constructor before they consider alternative ways of creating instances (such as factory methods).</span></span>

<span data-ttu-id="709f1-111">✔️ ROZWAŻYĆ udostępnienie prostych, idealnie domyślnych konstruktorów.</span><span class="sxs-lookup"><span data-stu-id="709f1-111">✔️ CONSIDER providing simple, ideally default, constructors.</span></span>

<span data-ttu-id="709f1-112">Prosty Konstruktor ma bardzo małą liczbę parametrów, a wszystkie parametry są pierwotne lub wyliczeniowe.</span><span class="sxs-lookup"><span data-stu-id="709f1-112">A simple constructor has a very small number of parameters, and all parameters are primitives or enums.</span></span> <span data-ttu-id="709f1-113">Takie proste konstruktory zwiększają użyteczność struktury.</span><span class="sxs-lookup"><span data-stu-id="709f1-113">Such simple constructors increase usability of the framework.</span></span>

<span data-ttu-id="709f1-114">✔️ ROZWAŻYĆ użycie statycznej metody fabryki zamiast konstruktora, Jeśli semantyka żądanej operacji nie jest mapowana bezpośrednio do konstrukcji nowego wystąpienia lub jeśli zgodnie z wytycznymi projektowania konstruktora uważać nienaturalny.</span><span class="sxs-lookup"><span data-stu-id="709f1-114">✔️ CONSIDER using a static factory method instead of a constructor if the semantics of the desired operation do not map directly to the construction of a new instance, or if following the constructor design guidelines feels unnatural.</span></span>

<span data-ttu-id="709f1-115">✔️ używać parametrów konstruktora jako skrótów do ustawiania właściwości głównych.</span><span class="sxs-lookup"><span data-stu-id="709f1-115">✔️ DO use constructor parameters as shortcuts for setting main properties.</span></span>

<span data-ttu-id="709f1-116">Nie powinno się różnicować semantyki między użyciem pustego konstruktora, a po nim niektóre zestawy właściwości i użycie konstruktora z wieloma argumentami.</span><span class="sxs-lookup"><span data-stu-id="709f1-116">There should be no difference in semantics between using the empty constructor followed by some property sets and using a constructor with multiple arguments.</span></span>

<span data-ttu-id="709f1-117">✔️ Użyj tej samej nazwy dla parametrów konstruktora i właściwości, jeśli konstruktory są używane do zwykłego ustawiania właściwości.</span><span class="sxs-lookup"><span data-stu-id="709f1-117">✔️ DO use the same name for constructor parameters and a property if the constructor parameters are used to simply set the property.</span></span>

<span data-ttu-id="709f1-118">Jedyną różnicą między takimi parametrami i właściwościami powinna być wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="709f1-118">The only difference between such parameters and the properties should be casing.</span></span>

<span data-ttu-id="709f1-119">✔️ WYKONAĆ minimalną ilość pracy w konstruktorze.</span><span class="sxs-lookup"><span data-stu-id="709f1-119">✔️ DO minimal work in the constructor.</span></span>

<span data-ttu-id="709f1-120">Konstruktory nie powinny wykonywać wielu zadań niż przechwycić parametry konstruktora.</span><span class="sxs-lookup"><span data-stu-id="709f1-120">Constructors should not do much work other than capture the constructor parameters.</span></span> <span data-ttu-id="709f1-121">Koszt dowolnego innego przetwarzania powinien zostać opóźniony do czasu wymagane.</span><span class="sxs-lookup"><span data-stu-id="709f1-121">The cost of any other processing should be delayed until required.</span></span>

<span data-ttu-id="709f1-122">✔️ należy zgłosić wyjątki z konstruktorów wystąpień, jeśli są odpowiednie.</span><span class="sxs-lookup"><span data-stu-id="709f1-122">✔️ DO throw exceptions from instance constructors, if appropriate.</span></span>

<span data-ttu-id="709f1-123">✔️ jawnie zadeklarować publiczny Konstruktor bez parametrów w klasach, jeśli taki Konstruktor jest wymagany.</span><span class="sxs-lookup"><span data-stu-id="709f1-123">✔️ DO explicitly declare the public parameterless constructor in classes, if such a constructor is required.</span></span>

<span data-ttu-id="709f1-124">Jeśli nie deklarujesz jawnie żadnych konstruktorów w typie, wiele języków (takich jak C#) automatycznie doda publiczny Konstruktor bez parametrów.</span><span class="sxs-lookup"><span data-stu-id="709f1-124">If you don’t explicitly declare any constructors on a type, many languages (such as C#) will automatically add a public parameterless constructor.</span></span> <span data-ttu-id="709f1-125">(Klasy abstrakcyjne uzyskują chroniony Konstruktor).</span><span class="sxs-lookup"><span data-stu-id="709f1-125">(Abstract classes get a protected constructor.)</span></span>

<span data-ttu-id="709f1-126">Dodanie konstruktora sparametryzowanego do klasy uniemożliwi kompilatorowi dodanie konstruktora bez parametrów.</span><span class="sxs-lookup"><span data-stu-id="709f1-126">Adding a parameterized constructor to a class prevents the compiler from adding the parameterless constructor.</span></span> <span data-ttu-id="709f1-127">Często powoduje to przypadkowe krytyczne zmiany.</span><span class="sxs-lookup"><span data-stu-id="709f1-127">This often causes accidental breaking changes.</span></span>

<span data-ttu-id="709f1-128">❌ UNIKAj jawnego definiowania konstruktorów bez parametrów w strukturach.</span><span class="sxs-lookup"><span data-stu-id="709f1-128">❌ AVOID explicitly defining parameterless constructors on structs.</span></span>

<span data-ttu-id="709f1-129">Dzięki temu tworzenie macierzy jest szybsze, ponieważ jeśli Konstruktor bez parametrów nie jest zdefiniowany, nie musi być uruchamiany w każdym gnieździe tablicy.</span><span class="sxs-lookup"><span data-stu-id="709f1-129">This makes array creation faster, because if the parameterless constructor is not defined, it does not have to be run on every slot in the array.</span></span> <span data-ttu-id="709f1-130">Należy zauważyć, że wiele kompilatorów, w tym C#, nie zezwala strukturom na używanie konstruktorów bez parametrów z tego powodu.</span><span class="sxs-lookup"><span data-stu-id="709f1-130">Note that many compilers, including C#, don’t allow structs to have parameterless constructors for this reason.</span></span>

<span data-ttu-id="709f1-131">❌ Należy unikać wywoływania wirtualnych elementów członkowskich w obiekcie wewnątrz jego konstruktora.</span><span class="sxs-lookup"><span data-stu-id="709f1-131">❌ AVOID calling virtual members on an object inside its constructor.</span></span>

<span data-ttu-id="709f1-132">Wywołanie wirtualnej składowej spowoduje wywołanie najbardziej pochodnego przesłonięcia, nawet jeśli Konstruktor najbardziej pochodnego nie został jeszcze w pełni uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="709f1-132">Calling a virtual member will cause the most derived override to be called, even if the constructor of the most derived type has not been fully run yet.</span></span>

## <a name="type-constructor-guidelines"></a><span data-ttu-id="709f1-133">Wytyczne dotyczące konstruktora typów</span><span class="sxs-lookup"><span data-stu-id="709f1-133">Type Constructor Guidelines</span></span>

<span data-ttu-id="709f1-134">✔️ uczynić statycznymi konstruktorami prywatnymi.</span><span class="sxs-lookup"><span data-stu-id="709f1-134">✔️ DO make static constructors private.</span></span>

<span data-ttu-id="709f1-135">Konstruktor statyczny nazywany również konstruktorem klasy jest używany do inicjowania typu.</span><span class="sxs-lookup"><span data-stu-id="709f1-135">A static constructor, also called a class constructor, is used to initialize a type.</span></span> <span data-ttu-id="709f1-136">CLR wywołuje konstruktora statycznego przed utworzeniem pierwszego wystąpienia typu lub wszystkie statyczne elementy członkowskie tego typu są wywoływane.</span><span class="sxs-lookup"><span data-stu-id="709f1-136">The CLR calls the static constructor before the first instance of the type is created or any static members on that type are called.</span></span> <span data-ttu-id="709f1-137">Użytkownik nie ma kontroli nad tym, kiedy Konstruktor statyczny jest wywoływany.</span><span class="sxs-lookup"><span data-stu-id="709f1-137">The user has no control over when the static constructor is called.</span></span> <span data-ttu-id="709f1-138">Jeśli Konstruktor statyczny nie jest prywatny, może być wywoływany przez kod inny niż CLR.</span><span class="sxs-lookup"><span data-stu-id="709f1-138">If a static constructor is not private, it can be called by code other than the CLR.</span></span> <span data-ttu-id="709f1-139">W zależności od operacji wykonywanych w konstruktorze może to spowodować nieoczekiwane zachowanie.</span><span class="sxs-lookup"><span data-stu-id="709f1-139">Depending on the operations performed in the constructor, this can cause unexpected behavior.</span></span> <span data-ttu-id="709f1-140">Kompilator języka C# wymusza, aby konstruktory statyczne były prywatne.</span><span class="sxs-lookup"><span data-stu-id="709f1-140">The C# compiler forces static constructors to be private.</span></span>

<span data-ttu-id="709f1-141">❌ NIE zgłaszaj wyjątków od konstruktorów statycznych.</span><span class="sxs-lookup"><span data-stu-id="709f1-141">❌ DO NOT throw exceptions from static constructors.</span></span>

<span data-ttu-id="709f1-142">Jeśli wyjątek jest zgłaszany z konstruktora typów, typ nie jest użyteczny w bieżącej domenie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="709f1-142">If an exception is thrown from a type constructor, the type is not usable in the current application domain.</span></span>

<span data-ttu-id="709f1-143">✔️ ROZWAŻYĆ zainicjowanie pól statycznych zamiast jawnie przy użyciu konstruktorów statycznych, ponieważ środowisko uruchomieniowe może zoptymalizować wydajność typów, które nie mają jawnie zdefiniowanego konstruktora statycznego.</span><span class="sxs-lookup"><span data-stu-id="709f1-143">✔️ CONSIDER initializing static fields inline rather than explicitly using static constructors, because the runtime is able to optimize the performance of types that don’t have an explicitly defined static constructor.</span></span>

<span data-ttu-id="709f1-144">*Fragmenty © 2005, 2009 Microsoft Corporation. Wszelkie prawa zastrzeżone.*</span><span class="sxs-lookup"><span data-stu-id="709f1-144">*Portions © 2005, 2009 Microsoft Corporation. All rights reserved.*</span></span>

<span data-ttu-id="709f1-145">*Ponownie Wydrukowano przez uprawnienie Pearson Education, Inc. z [wytycznych dotyczących projektowania platformy: konwencje, idiomy i wzorce dla bibliotek .NET do wielokrotnego użytku, 2. wydanie](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) przez Krzysztof Cwalina i Brad Abrams, opublikowane 22, 2008 przez Addison-Wesley Professional w ramach serii Microsoft Windows Development.*</span><span class="sxs-lookup"><span data-stu-id="709f1-145">*Reprinted by permission of Pearson Education, Inc. from [Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) by Krzysztof Cwalina and Brad Abrams, published Oct 22, 2008 by Addison-Wesley Professional as part of the Microsoft Windows Development Series.*</span></span>

## <a name="see-also"></a><span data-ttu-id="709f1-146">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="709f1-146">See also</span></span>

- [<span data-ttu-id="709f1-147">Wskazówki dotyczące projektowania elementów członkowskich</span><span class="sxs-lookup"><span data-stu-id="709f1-147">Member Design Guidelines</span></span>](member.md)
- [<span data-ttu-id="709f1-148">Wskazówki dotyczące projektowania struktury</span><span class="sxs-lookup"><span data-stu-id="709f1-148">Framework Design Guidelines</span></span>](index.md)
