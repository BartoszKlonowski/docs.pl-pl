---
title: Właściwości
description: 'Informacje o właściwościach języka F #, które są elementami członkowskimi reprezentującymi wartości skojarzone z obiektem.'
ms.date: 05/16/2016
ms.openlocfilehash: a2a4fbfc88831dcb5cad7a2da701969b2e98b2e3
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96740201"
---
# <a name="properties"></a><span data-ttu-id="1a57c-103">Właściwości</span><span class="sxs-lookup"><span data-stu-id="1a57c-103">Properties</span></span>

<span data-ttu-id="1a57c-104">*Właściwości* są elementami, które reprezentują wartości skojarzone z obiektem.</span><span class="sxs-lookup"><span data-stu-id="1a57c-104">*Properties* are members that represent values associated with an object.</span></span>

## <a name="syntax"></a><span data-ttu-id="1a57c-105">Składnia</span><span class="sxs-lookup"><span data-stu-id="1a57c-105">Syntax</span></span>

```fsharp
// Property that has both get and set defined.
[ attributes ]
[ static ] member [accessibility-modifier] [self-identifier.]PropertyName
with [accessibility-modifier] get() =
    get-function-body
and [accessibility-modifier] set parameter =
    set-function-body

// Alternative syntax for a property that has get and set.
[ attributes-for-get ]
[ static ] member [accessibility-modifier-for-get] [self-identifier.]PropertyName =
    get-function-body
[ attributes-for-set ]
[ static ] member [accessibility-modifier-for-set] [self-identifier.]PropertyName
with set parameter =
    set-function-body

// Property that has get only.
[ attributes ]
[ static ] member [accessibility-modifier] [self-identifier.]PropertyName =
    get-function-body

// Alternative syntax for property that has get only.
[ attributes ]
[ static ] member [accessibility-modifier] [self-identifier.]PropertyName
with get() =
    get-function-body

// Property that has set only.
[ attributes ]
[ static ] member [accessibility-modifier] [self-identifier.]PropertyName
with set parameter =
    set-function-body

// Automatically implemented properties.
[ attributes ]
[ static ] member val [accessibility-modifier] PropertyName = initialization-expression [ with get, set ]
```

## <a name="remarks"></a><span data-ttu-id="1a57c-106">Uwagi</span><span class="sxs-lookup"><span data-stu-id="1a57c-106">Remarks</span></span>

<span data-ttu-id="1a57c-107">Właściwości reprezentują relację "ma" w programowaniu zorientowanym obiektowo, reprezentującą dane, które są skojarzone z wystąpieniami obiektów lub, dla właściwości statycznych z typem.</span><span class="sxs-lookup"><span data-stu-id="1a57c-107">Properties represent the "has a" relationship in object-oriented programming, representing data that is associated with object instances or, for static properties, with the type.</span></span>

<span data-ttu-id="1a57c-108">Możesz zadeklarować właściwości na dwa sposoby, w zależności od tego, czy chcesz jawnie określić wartość podstawową (nazywaną również magazynem zapasowym) dla właściwości, lub jeśli chcesz zezwolić kompilatorowi na automatyczne generowanie magazynu zapasowego.</span><span class="sxs-lookup"><span data-stu-id="1a57c-108">You can declare properties in two ways, depending on whether you want to explicitly specify the underlying value (also called the backing store) for the property, or if you want to allow the compiler to automatically generate the backing store for you.</span></span> <span data-ttu-id="1a57c-109">Ogólnie rzecz biorąc, należy użyć bardziej jawnej metody, jeśli właściwość ma nieprostą implementację i gdy właściwość to tylko prosta otoka dla wartości lub zmiennej.</span><span class="sxs-lookup"><span data-stu-id="1a57c-109">Generally, you should use the more explicit way if the property has a non-trivial implementation and the automatic way when the property is just a simple wrapper for a value or variable.</span></span> <span data-ttu-id="1a57c-110">Aby jawnie zadeklarować właściwość, użyj `member` słowa kluczowego.</span><span class="sxs-lookup"><span data-stu-id="1a57c-110">To declare a property explicitly, use the `member` keyword.</span></span> <span data-ttu-id="1a57c-111">W tej składni deklaratywnej następuje składnia, która określa `get` metody i `set` , nazywane także metodami *dostępu*.</span><span class="sxs-lookup"><span data-stu-id="1a57c-111">This declarative syntax is followed by the syntax that specifies the `get` and `set` methods, also named *accessors*.</span></span> <span data-ttu-id="1a57c-112">Różne formy jawnej składni pokazanej w sekcji składnia są używane do odczytu/zapisu, właściwości tylko do odczytu i zapisu.</span><span class="sxs-lookup"><span data-stu-id="1a57c-112">The various forms of the explicit syntax shown in the syntax section are used for read/write, read-only, and write-only properties.</span></span> <span data-ttu-id="1a57c-113">W przypadku właściwości tylko do odczytu należy zdefiniować tylko `get` metodę; dla właściwości tylko do zapisu należy zdefiniować tylko `set` metodę.</span><span class="sxs-lookup"><span data-stu-id="1a57c-113">For read-only properties, you define only a `get` method; for write-only properties, define only a `set` method.</span></span> <span data-ttu-id="1a57c-114">Należy pamiętać, że gdy właściwość ma zarówno metody `get` `set` dostępu, jak i Akcesory, Alternatywna składnia pozwala określić atrybuty i Modyfikatory dostępności, które są różne dla każdego akcesora, jak pokazano w poniższym kodzie.</span><span class="sxs-lookup"><span data-stu-id="1a57c-114">Note that when a property has both `get` and `set` accessors, the alternative syntax enables you to specify attributes and accessibility modifiers that are different for each accessor, as is shown in the following code.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3201.fs)]

<span data-ttu-id="1a57c-115">Dla właściwości odczytu/zapisu, które mają zarówno `get` `set` metodę, jak i, kolejność `get` i `set` można wycofać.</span><span class="sxs-lookup"><span data-stu-id="1a57c-115">For read/write properties, which have both a `get` and `set` method, the order of `get` and `set` can be reversed.</span></span> <span data-ttu-id="1a57c-116">Alternatywnie można podać składnię wyświetlaną tylko dla `get` i składnię wyświetlaną `set` tylko zamiast używać połączonej składni.</span><span class="sxs-lookup"><span data-stu-id="1a57c-116">Alternatively, you can provide the syntax shown for `get` only and the syntax shown for `set` only instead of using the combined syntax.</span></span> <span data-ttu-id="1a57c-117">Dzięki temu można łatwiej dodać komentarz do osoby `get` lub `set` metody, jeśli jest to coś, co może być konieczne.</span><span class="sxs-lookup"><span data-stu-id="1a57c-117">Doing this makes it easier to comment out the individual `get` or `set` method, if that is something you might need to do.</span></span> <span data-ttu-id="1a57c-118">Alternatywą dla używania połączonej składni przedstawiono w poniższym kodzie.</span><span class="sxs-lookup"><span data-stu-id="1a57c-118">This alternative to using the combined syntax is shown in the following code.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3203.fs)]

<span data-ttu-id="1a57c-119">Prywatne wartości przechowujące dane dla właściwości są nazywane *magazynami zapasowymi*.</span><span class="sxs-lookup"><span data-stu-id="1a57c-119">Private values that hold the data for properties are called *backing stores*.</span></span> <span data-ttu-id="1a57c-120">Aby kompilator automatycznie utworzył magazyn zapasowy, należy użyć słów kluczowych `member val` , pominąć samoidentyfikator, a następnie podać wyrażenie w celu zainicjowania właściwości.</span><span class="sxs-lookup"><span data-stu-id="1a57c-120">To have the compiler create the backing store automatically, use the keywords `member val`, omit the self-identifier, then provide an expression to initialize the property.</span></span> <span data-ttu-id="1a57c-121">Jeśli właściwość ma być modyfikowalna, Dołącz `with get, set` .</span><span class="sxs-lookup"><span data-stu-id="1a57c-121">If the property is to be mutable, include `with get, set`.</span></span> <span data-ttu-id="1a57c-122">Na przykład następujący typ klasy obejmuje dwie automatycznie zaimplementowane właściwości.</span><span class="sxs-lookup"><span data-stu-id="1a57c-122">For example, the following class type includes two automatically implemented properties.</span></span> <span data-ttu-id="1a57c-123">`Property1` jest tylko do odczytu i jest inicjowana do argumentu dostarczonego przez konstruktora podstawowego i `Property2` jest właściwością settable zainicjowaną do pustego ciągu:</span><span class="sxs-lookup"><span data-stu-id="1a57c-123">`Property1` is read-only and is initialized to the argument provided to the primary constructor, and `Property2` is a settable property initialized to an empty string:</span></span>

```fsharp
type MyClass(property1 : int) =
member val Property1 = property1
member val Property2 = "" with get, set
```

<span data-ttu-id="1a57c-124">Automatycznie implementowane właściwości są częścią inicjalizacji typu, dlatego muszą być zawarte przed innymi definicjami elementów członkowskich, podobnie jak `let` powiązania i `do` powiązania w definicji typu.</span><span class="sxs-lookup"><span data-stu-id="1a57c-124">Automatically implemented properties are part of the initialization of a type, so they must be included before any other member definitions, just like `let` bindings and `do` bindings in a type definition.</span></span> <span data-ttu-id="1a57c-125">Należy zauważyć, że wyrażenie inicjujące automatycznie implementowaną właściwość jest oceniane tylko po inicjacji, a nie za każdym razem, gdy właściwość jest używana.</span><span class="sxs-lookup"><span data-stu-id="1a57c-125">Note that the expression that initializes an automatically implemented property is only evaluated upon initialization, and not every time the property is accessed.</span></span> <span data-ttu-id="1a57c-126">To zachowanie jest w przeciwieństwie do zachowania jawnie zaimplementowanej właściwości.</span><span class="sxs-lookup"><span data-stu-id="1a57c-126">This behavior is in contrast to the behavior of an explicitly implemented property.</span></span> <span data-ttu-id="1a57c-127">To efektywnie oznacza, że kod, który ma inicjować te właściwości, jest dodawany do konstruktora klasy.</span><span class="sxs-lookup"><span data-stu-id="1a57c-127">What this effectively means is that the code to initialize these properties is added to the constructor of a class.</span></span> <span data-ttu-id="1a57c-128">Rozważmy następujący kod, który pokazuje tę różnicę:</span><span class="sxs-lookup"><span data-stu-id="1a57c-128">Consider the following code that shows this difference:</span></span>

```fsharp
type MyClass() =
    let random  = new System.Random()
    member val AutoProperty = random.Next() with get, set
    member this.ExplicitProperty = random.Next()

let class1 = new MyClass()

printfn $"class1.AutoProperty = %d{class1.AutoProperty}"
printfn $"class1.ExplicitProperty = %d{class1.ExplicitProperty}"
```

<span data-ttu-id="1a57c-129">**Dane wyjściowe**</span><span class="sxs-lookup"><span data-stu-id="1a57c-129">**Output**</span></span>

```console
class1.AutoProperty = 1853799794
class1.AutoProperty = 1853799794
class1.ExplicitProperty = 978922705
class1.ExplicitProperty = 1131210765
```

<span data-ttu-id="1a57c-130">Dane wyjściowe powyższego kodu pokazują, że wartość właściwości autoproperty jest niezmieniona, gdy jest wywoływana wielokrotnie, podczas gdy ExplicitProperty ulega zmianie przy każdym wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="1a57c-130">The output of the preceding code shows that the value of AutoProperty is unchanged when called repeatedly, whereas the ExplicitProperty changes each time it is called.</span></span> <span data-ttu-id="1a57c-131">Pokazuje to, że wyrażenie dla automatycznie zaimplementowanej właściwości nie jest oceniane każdorazowo, podobnie jak metoda pobierająca dla właściwości explicit.</span><span class="sxs-lookup"><span data-stu-id="1a57c-131">This demonstrates that the expression for an automatically implemented property is not evaluated each time, as is the getter method for the explicit property.</span></span>

>[!WARNING]
><span data-ttu-id="1a57c-132">Istnieją pewne biblioteki, takie jak Entity Framework ( `System.Data.Entity` ), które wykonują niestandardowe operacje w konstruktorach klas podstawowych, które nie działają poprawnie z inicjowaniem automatycznie zaimplementowanych właściwości.</span><span class="sxs-lookup"><span data-stu-id="1a57c-132">There are some libraries, such as the Entity Framework (`System.Data.Entity`) that perform custom operations in base class constructors that don't work well with the initialization of automatically implemented properties.</span></span> <span data-ttu-id="1a57c-133">W takich przypadkach spróbuj użyć jawnych właściwości.</span><span class="sxs-lookup"><span data-stu-id="1a57c-133">In those cases, try using explicit properties.</span></span>

<span data-ttu-id="1a57c-134">Właściwości mogą być elementami członkowskimi klas, struktur, Unii rozłącznych, rekordów, interfejsów i rozszerzeń typów i mogą być również zdefiniowane w wyrażeniach obiektu.</span><span class="sxs-lookup"><span data-stu-id="1a57c-134">Properties can be members of classes, structures, discriminated unions, records, interfaces, and type extensions and can also be defined in object expressions.</span></span>

<span data-ttu-id="1a57c-135">Atrybuty mogą być stosowane do właściwości.</span><span class="sxs-lookup"><span data-stu-id="1a57c-135">Attributes can be applied to properties.</span></span> <span data-ttu-id="1a57c-136">Aby zastosować atrybut do właściwości, należy zapisać atrybut w osobnym wierszu przed właściwością.</span><span class="sxs-lookup"><span data-stu-id="1a57c-136">To apply an attribute to a property, write the attribute on a separate line before the property.</span></span> <span data-ttu-id="1a57c-137">Aby uzyskać więcej informacji, zobacz [atrybuty](../attributes.md).</span><span class="sxs-lookup"><span data-stu-id="1a57c-137">For more information, see [Attributes](../attributes.md).</span></span>

<span data-ttu-id="1a57c-138">Domyślnie właściwości są publiczne.</span><span class="sxs-lookup"><span data-stu-id="1a57c-138">By default, properties are public.</span></span> <span data-ttu-id="1a57c-139">Modyfikatory dostępności można również stosować do właściwości.</span><span class="sxs-lookup"><span data-stu-id="1a57c-139">Accessibility modifiers can also be applied to properties.</span></span> <span data-ttu-id="1a57c-140">Aby zastosować modyfikator dostępności, należy dodać go bezpośrednio przed nazwą właściwości, jeśli ma zastosowanie do obu `get` `set` metod i; dodać go przed `get` `set` słowami kluczowymi i, jeśli dla każdego akcesora jest wymagana inna dostępność.</span><span class="sxs-lookup"><span data-stu-id="1a57c-140">To apply an accessibility modifier, add it immediately before the name of the property if it is meant to apply to both the `get` and `set` methods; add it before the `get` and `set` keywords if different accessibility is required for each accessor.</span></span> <span data-ttu-id="1a57c-141">*Modyfikator dostępności* może mieć jedną z następujących wartości: `public` , `private` , `internal` .</span><span class="sxs-lookup"><span data-stu-id="1a57c-141">The *accessibility-modifier* can be one of the following: `public`, `private`, `internal`.</span></span> <span data-ttu-id="1a57c-142">Aby uzyskać więcej informacji, zobacz [Kontrola dostępu](../access-control.md).</span><span class="sxs-lookup"><span data-stu-id="1a57c-142">For more information, see [Access Control](../access-control.md).</span></span>

<span data-ttu-id="1a57c-143">Implementacje właściwości są wykonywane za każdym razem, gdy uzyskuje się dostęp do właściwości.</span><span class="sxs-lookup"><span data-stu-id="1a57c-143">Property implementations are executed each time a property is accessed.</span></span>

## <a name="static-and-instance-properties"></a><span data-ttu-id="1a57c-144">Właściwości statyczne i wystąpienia</span><span class="sxs-lookup"><span data-stu-id="1a57c-144">Static and Instance Properties</span></span>

<span data-ttu-id="1a57c-145">Właściwości mogą być właściwościami statycznymi lub wystąpieniami.</span><span class="sxs-lookup"><span data-stu-id="1a57c-145">Properties can be static or instance properties.</span></span> <span data-ttu-id="1a57c-146">Właściwości statyczne mogą być wywoływane bez wystąpienia i są używane w przypadku wartości skojarzonych z typem, a nie z poszczególnymi obiektami.</span><span class="sxs-lookup"><span data-stu-id="1a57c-146">Static properties can be invoked without an instance and are used for values associated with the type, not with individual objects.</span></span> <span data-ttu-id="1a57c-147">W przypadku właściwości statycznych Pomiń autoidentyfikator.</span><span class="sxs-lookup"><span data-stu-id="1a57c-147">For static properties, omit the self-identifier.</span></span> <span data-ttu-id="1a57c-148">Do właściwości wystąpienia są wymagane samoobsługowe identyfikatory.</span><span class="sxs-lookup"><span data-stu-id="1a57c-148">The self-identifier is required for instance properties.</span></span>

<span data-ttu-id="1a57c-149">Następująca Definicja właściwości statycznej jest oparta na scenariuszu, w którym istnieje pole statyczne `myStaticValue` , które jest magazynem zapasowym dla właściwości.</span><span class="sxs-lookup"><span data-stu-id="1a57c-149">The following static property definition is based on a scenario in which you have a static field `myStaticValue` that is the backing store for the property.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3204.fs)]

<span data-ttu-id="1a57c-150">Właściwości mogą również być podobne do tablic, w tym przypadku są nazywane *indeksowanymi właściwościami*.</span><span class="sxs-lookup"><span data-stu-id="1a57c-150">Properties can also be array-like, in which case they are called *indexed properties*.</span></span> <span data-ttu-id="1a57c-151">Aby uzyskać więcej informacji, zobacz [indeksowane właściwości](indexed-properties.md).</span><span class="sxs-lookup"><span data-stu-id="1a57c-151">For more information, see [Indexed Properties](indexed-properties.md).</span></span>

## <a name="type-annotation-for-properties"></a><span data-ttu-id="1a57c-152">Adnotacja typu dla właściwości</span><span class="sxs-lookup"><span data-stu-id="1a57c-152">Type Annotation for Properties</span></span>

<span data-ttu-id="1a57c-153">W wielu przypadkach kompilator ma wystarczającą ilość informacji do wywnioskowania typu właściwości z typu magazynu zapasowego, ale można ustawić typ jawnie poprzez dodanie adnotacji typu.</span><span class="sxs-lookup"><span data-stu-id="1a57c-153">In many cases, the compiler has enough information to infer the type of a property from the type of the backing store, but you can set the type explicitly by adding a type annotation.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3205.fs)]

## <a name="using-property-set-accessors"></a><span data-ttu-id="1a57c-154">Korzystanie z metod dostępu do ustawiania właściwości</span><span class="sxs-lookup"><span data-stu-id="1a57c-154">Using Property set Accessors</span></span>

<span data-ttu-id="1a57c-155">Można ustawić właściwości, które zapewniają `set` metody dostępu przy użyciu `<-` operatora.</span><span class="sxs-lookup"><span data-stu-id="1a57c-155">You can set properties that provide `set` accessors by using the `<-` operator.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3206.fs)]

<span data-ttu-id="1a57c-156">Wynik wynosi **20**.</span><span class="sxs-lookup"><span data-stu-id="1a57c-156">The output is **20**.</span></span>

## <a name="abstract-properties"></a><span data-ttu-id="1a57c-157">Właściwości abstrakcyjne</span><span class="sxs-lookup"><span data-stu-id="1a57c-157">Abstract Properties</span></span>

<span data-ttu-id="1a57c-158">Właściwości mogą być abstrakcyjne.</span><span class="sxs-lookup"><span data-stu-id="1a57c-158">Properties can be abstract.</span></span> <span data-ttu-id="1a57c-159">Podobnie jak w przypadku metod, `abstract` oznacza to, że istnieje wirtualna wysyłka skojarzona z właściwością.</span><span class="sxs-lookup"><span data-stu-id="1a57c-159">As with methods, `abstract` just means that there is a virtual dispatch associated with the property.</span></span> <span data-ttu-id="1a57c-160">Właściwości abstrakcyjne mogą być prawdziwie abstrakcyjne, czyli bez definicji w tej samej klasie.</span><span class="sxs-lookup"><span data-stu-id="1a57c-160">Abstract properties can be truly abstract, that is, without a definition in the same class.</span></span> <span data-ttu-id="1a57c-161">Klasa, która zawiera taką właściwość, jest w związku z tym klasą abstrakcyjną.</span><span class="sxs-lookup"><span data-stu-id="1a57c-161">The class that contains such a property is therefore an abstract class.</span></span> <span data-ttu-id="1a57c-162">Alternatywnie abstrakcyjny może oznaczać, że właściwość jest wirtualna, a w takim przypadku definicja musi być obecna w tej samej klasie.</span><span class="sxs-lookup"><span data-stu-id="1a57c-162">Alternatively, abstract can just mean that a property is virtual, and in that case, a definition must be present in the same class.</span></span> <span data-ttu-id="1a57c-163">Należy zauważyć, że właściwości abstrakcyjne nie mogą być prywatne i jeśli jedna metoda dostępu jest abstrakcyjna, druga musi również być abstrakcyjna.</span><span class="sxs-lookup"><span data-stu-id="1a57c-163">Note that abstract properties must not be private, and if one accessor is abstract, the other must also be abstract.</span></span> <span data-ttu-id="1a57c-164">Aby uzyskać więcej informacji na temat klas abstrakcyjnych, zobacz [klasy abstrakcyjne](../abstract-classes.md).</span><span class="sxs-lookup"><span data-stu-id="1a57c-164">For more information about abstract classes, see [Abstract Classes](../abstract-classes.md).</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3207.fs)]

## <a name="see-also"></a><span data-ttu-id="1a57c-165">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="1a57c-165">See also</span></span>

- [<span data-ttu-id="1a57c-166">Elementy członkowskie</span><span class="sxs-lookup"><span data-stu-id="1a57c-166">Members</span></span>](index.md)
- [<span data-ttu-id="1a57c-167">Metody</span><span class="sxs-lookup"><span data-stu-id="1a57c-167">Methods</span></span>](methods.md)
