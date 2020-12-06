---
title: 'Samouczek: Tworzenie dostawcy typów'
description: 'Dowiedz się, jak utworzyć własnych dostawców typów języka F # w języku F # 3,0, badając kilku dostawców typów prostych, aby zilustrować podstawowe pojęcia.'
ms.date: 11/04/2019
ms.openlocfilehash: 65cb9616f66b5850135dbfcdd9b9a9dad30421de
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96739701"
---
# <a name="tutorial-create-a-type-provider"></a><span data-ttu-id="e8969-103">Samouczek: Tworzenie dostawcy typów</span><span class="sxs-lookup"><span data-stu-id="e8969-103">Tutorial: Create a Type Provider</span></span>

<span data-ttu-id="e8969-104">Mechanizm dostawcy typów w języku F # jest znaczną częścią pomocy technicznej dotyczącej rozbudowanego programowania informacji.</span><span class="sxs-lookup"><span data-stu-id="e8969-104">The type provider mechanism in F# is a significant part of its support for information rich programming.</span></span> <span data-ttu-id="e8969-105">W tym samouczku wyjaśniono, jak utworzyć własnych dostawców typów, przechodząc przez rozwój kilku dostawców typów prostych, aby zilustrować podstawowe pojęcia.</span><span class="sxs-lookup"><span data-stu-id="e8969-105">This tutorial explains how to create your own type providers by walking you through the development of several simple type providers to illustrate the basic concepts.</span></span> <span data-ttu-id="e8969-106">Aby uzyskać więcej informacji na temat mechanizmu dostawcy typów w języku F #, zobacz [dostawcy typów](index.md).</span><span class="sxs-lookup"><span data-stu-id="e8969-106">For more information about the type provider mechanism in F#, see [Type Providers](index.md).</span></span>

<span data-ttu-id="e8969-107">Ekosystem F # zawiera szereg dostawców typów dla często używanych usług Internet i Enterprise Data Services.</span><span class="sxs-lookup"><span data-stu-id="e8969-107">The F# ecosystem contains a range of type providers for commonly used Internet and enterprise data services.</span></span> <span data-ttu-id="e8969-108">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="e8969-108">For example:</span></span>

- <span data-ttu-id="e8969-109">[FSharp. Data](https://fsharp.github.io/FSharp.Data/) zawiera dostawców typów dla formatów dokumentów JSON, XML, CSV i HTML.</span><span class="sxs-lookup"><span data-stu-id="e8969-109">[FSharp.Data](https://fsharp.github.io/FSharp.Data/) includes type providers for JSON, XML, CSV and HTML document formats.</span></span>

- <span data-ttu-id="e8969-110">Element [sqldostarczając](https://fsprojects.github.io/SQLProvider/) ma silnie określony dostęp do baz danych SQL za pomocą mapowania obiektów i zapytań języka F # LINQ względem tych źródeł danych.</span><span class="sxs-lookup"><span data-stu-id="e8969-110">[SQLProvider](https://fsprojects.github.io/SQLProvider/) provides strongly typed access to SQL databases through a object mapping and F# LINQ queries against these data sources.</span></span>

- <span data-ttu-id="e8969-111">[FSharp. Data. SqlClient](https://fsprojects.github.io/FSharp.Data.SqlClient/) ma zestaw dostawców typów dla zaznaczonego osadzania języka T-SQL w języku F #.</span><span class="sxs-lookup"><span data-stu-id="e8969-111">[FSharp.Data.SqlClient](https://fsprojects.github.io/FSharp.Data.SqlClient/) has a set of type providers for compile-time checked embedding of T-SQL in F#.</span></span>

- <span data-ttu-id="e8969-112">[FSharp. Data. TypeProviders](https://fsprojects.github.io/FSharp.Data.TypeProviders/) to starszy zestaw dostawców typów do użytku tylko z .NET Framework programowaniem do uzyskiwania dostępu do usług SQL, Entity Framework, OData i WSDL.</span><span class="sxs-lookup"><span data-stu-id="e8969-112">[FSharp.Data.TypeProviders](https://fsprojects.github.io/FSharp.Data.TypeProviders/) is an older set of type providers for use only with .NET Framework programming for accessing SQL, Entity Framework, OData and WSDL data services.</span></span>

<span data-ttu-id="e8969-113">W razie potrzeby można utworzyć niestandardowych dostawców typów lub odwoływać się do dostawców typów utworzonych przez innych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="e8969-113">Where necessary, you can create custom type providers, or you can reference type providers that others have created.</span></span> <span data-ttu-id="e8969-114">Na przykład organizacja może mieć usługę danych, która zapewnia dużą i rosnącą liczbę nazwanych zestawów danych, z których każdy ma własny stabilny schemat danych.</span><span class="sxs-lookup"><span data-stu-id="e8969-114">For example, your organization could have a data service that provides a large and growing number of named data sets, each with its own stable data schema.</span></span> <span data-ttu-id="e8969-115">Można utworzyć dostawcę typów, który odczytuje schematy i prezentuje bieżące zestawy danych programisty w jednoznacznie określonym sposób.</span><span class="sxs-lookup"><span data-stu-id="e8969-115">You can create a type provider that reads the schemas and presents the current data sets to the programmer in a strongly typed way.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="e8969-116">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="e8969-116">Before You Start</span></span>

<span data-ttu-id="e8969-117">Mechanizm dostawcy typów jest przeznaczony głównie do wstrzykiwania stabilnych przestrzeni danych i informacji o usługach do środowiska programowania F #.</span><span class="sxs-lookup"><span data-stu-id="e8969-117">The type provider mechanism is primarily designed for injecting stable data and service information spaces into the F# programming experience.</span></span>

<span data-ttu-id="e8969-118">Ten mechanizm nie jest przeznaczony do wprowadzania miejsc informacji, których schemat zmienia się podczas wykonywania programu w sposób istotny dla logiki programu.</span><span class="sxs-lookup"><span data-stu-id="e8969-118">This mechanism isn’t designed for injecting information spaces whose schema changes during program execution in ways that are relevant to program logic.</span></span> <span data-ttu-id="e8969-119">Mechanizm nie jest również przeznaczony do programowania meta-językowego, nawet jeśli ta domena zawiera nieprawidłowe zastosowania.</span><span class="sxs-lookup"><span data-stu-id="e8969-119">Also, the mechanism isn't designed for intra-language meta-programming, even though that domain contains some valid uses.</span></span> <span data-ttu-id="e8969-120">Tego mechanizmu należy używać tylko tam, gdzie jest to konieczne, a rozwój dostawcy typów daje bardzo wysoką wartość.</span><span class="sxs-lookup"><span data-stu-id="e8969-120">You should use this mechanism only where necessary and where the development of a type provider yields very high value.</span></span>

<span data-ttu-id="e8969-121">Należy unikać pisania dostawcy typów, w którym schemat nie jest dostępny.</span><span class="sxs-lookup"><span data-stu-id="e8969-121">You should avoid writing a type provider where a schema isn't available.</span></span> <span data-ttu-id="e8969-122">Podobnie należy unikać pisania dostawcy typów, w którym wystarcza zwykła (lub nawet istniejąca) Biblioteka platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="e8969-122">Likewise, you should avoid writing a type provider where an ordinary (or even an existing) .NET library would suffice.</span></span>

<span data-ttu-id="e8969-123">Przed rozpoczęciem należy zadać następujące pytania:</span><span class="sxs-lookup"><span data-stu-id="e8969-123">Before you start, you might ask the following questions:</span></span>

- <span data-ttu-id="e8969-124">Czy masz schemat dla źródła informacji?</span><span class="sxs-lookup"><span data-stu-id="e8969-124">Do you have a schema for your information source?</span></span> <span data-ttu-id="e8969-125">Jeśli tak, to jakie jest mapowanie do systemu typu F # i .NET?</span><span class="sxs-lookup"><span data-stu-id="e8969-125">If so, what’s the mapping into the F# and .NET type system?</span></span>

- <span data-ttu-id="e8969-126">Czy można użyć istniejącego (dynamicznie wpisanego) interfejsu API jako punktu wyjścia dla implementacji?</span><span class="sxs-lookup"><span data-stu-id="e8969-126">Can you use an existing (dynamically typed) API as a starting point for your implementation?</span></span>

- <span data-ttu-id="e8969-127">Czy ty i Twoja organizacja będzie miała wystarczające użycie dostawcy typów, aby napisać jego wartościowa?</span><span class="sxs-lookup"><span data-stu-id="e8969-127">Will you and your organization have enough uses of the type provider to make writing it worthwhile?</span></span> <span data-ttu-id="e8969-128">Czy normalna Biblioteka platformy .NET spełnia Twoje potrzeby?</span><span class="sxs-lookup"><span data-stu-id="e8969-128">Would a normal .NET library meet your needs?</span></span>

- <span data-ttu-id="e8969-129">Jak dużo będzie zmieniać schemat?</span><span class="sxs-lookup"><span data-stu-id="e8969-129">How much will your schema change?</span></span>

- <span data-ttu-id="e8969-130">Czy ulegnie zmianie podczas kodowania?</span><span class="sxs-lookup"><span data-stu-id="e8969-130">Will it change during coding?</span></span>

- <span data-ttu-id="e8969-131">Czy zmieni się między sesjami kodowania?</span><span class="sxs-lookup"><span data-stu-id="e8969-131">Will it change between coding sessions?</span></span>

- <span data-ttu-id="e8969-132">Zmieni się podczas wykonywania programu?</span><span class="sxs-lookup"><span data-stu-id="e8969-132">Will it change during program execution?</span></span>

<span data-ttu-id="e8969-133">Dostawcy typów najlepiej nadają się do sytuacji, w których schemat jest stabilny w czasie wykonywania i w okresie istnienia skompilowanego kodu.</span><span class="sxs-lookup"><span data-stu-id="e8969-133">Type providers are best suited to situations where the schema is stable at runtime and during the lifetime of compiled code.</span></span>

## <a name="a-simple-type-provider"></a><span data-ttu-id="e8969-134">Dostawca typu prostego</span><span class="sxs-lookup"><span data-stu-id="e8969-134">A Simple Type Provider</span></span>

<span data-ttu-id="e8969-135">Ten przykład to Sample. HelloWorldTypeProvider, podobny do przykładów w `examples` katalogu [zestawu SDK dostawcy typów języka F #](https://github.com/fsprojects/FSharp.TypeProviders.SDK/).</span><span class="sxs-lookup"><span data-stu-id="e8969-135">This sample is Samples.HelloWorldTypeProvider, similar to the samples in the `examples` directory of the [F# Type Provider SDK](https://github.com/fsprojects/FSharp.TypeProviders.SDK/).</span></span> <span data-ttu-id="e8969-136">Dostawca udostępnia "przestrzeń typu" zawierającą 100 typów wymazanych, jak pokazano w poniższym kodzie za pomocą składni podpisów języka F # i pomijając szczegóły dla wszystkich z wyjątkiem `Type1` .</span><span class="sxs-lookup"><span data-stu-id="e8969-136">The provider makes available a "type space" that contains 100 erased types, as the following code shows by using F# signature syntax and omitting the details for all except `Type1`.</span></span> <span data-ttu-id="e8969-137">Aby uzyskać więcej informacji na temat wymazanych typów, zobacz [szczegóły dotyczące wymazanych typów](#details-about-erased-provided-types) w dalszej części tego tematu.</span><span class="sxs-lookup"><span data-stu-id="e8969-137">For more information about erased types, see [Details About Erased Provided Types](#details-about-erased-provided-types) later in this topic.</span></span>

```fsharp
namespace Samples.HelloWorldTypeProvider

type Type1 =
    /// This is a static property.
    static member StaticProperty : string

    /// This constructor takes no arguments.
    new : unit -> Type1

    /// This constructor takes one argument.
    new : data:string -> Type1

    /// This is an instance property.
    member InstanceProperty : int

    /// This is an instance method.
    member InstanceMethod : x:int -> char

    nested type NestedType =
        /// This is StaticProperty1 on NestedType.
        static member StaticProperty1 : string
        …
        /// This is StaticProperty100 on NestedType.
        static member StaticProperty100 : string

type Type2 =
…
…

type Type100 =
…
```

<span data-ttu-id="e8969-138">Należy zauważyć, że zestaw typów i elementów członkowskich jest znany statycznie.</span><span class="sxs-lookup"><span data-stu-id="e8969-138">Note that the set of types and members provided is statically known.</span></span> <span data-ttu-id="e8969-139">Ten przykład nie wykorzystuje możliwości dostawców do udostępniania typów, które są zależne od schematu.</span><span class="sxs-lookup"><span data-stu-id="e8969-139">This example doesn't leverage the ability of providers to provide types that depend on a schema.</span></span> <span data-ttu-id="e8969-140">Implementacja dostawcy typów została omówiona w poniższym kodzie, a szczegóły znajdują się w dalszej części tego tematu.</span><span class="sxs-lookup"><span data-stu-id="e8969-140">The implementation of the type provider is outlined in the following code, and the details are covered in later sections of this topic.</span></span>

> [!WARNING]
> <span data-ttu-id="e8969-141">Mogą występować różnice między tym kodem i przykładami online.</span><span class="sxs-lookup"><span data-stu-id="e8969-141">There may be differences between this code and the online samples.</span></span>

```fsharp
namespace Samples.FSharp.HelloWorldTypeProvider

open System
open System.Reflection
open ProviderImplementation.ProvidedTypes
open FSharp.Core.CompilerServices
open FSharp.Quotations

// This type defines the type provider. When compiled to a DLL, it can be added
// as a reference to an F# command-line compilation, script, or project.
[<TypeProvider>]
type SampleTypeProvider(config: TypeProviderConfig) as this =

  // Inheriting from this type provides implementations of ITypeProvider
  // in terms of the provided types below.
  inherit TypeProviderForNamespaces(config)

  let namespaceName = "Samples.HelloWorldTypeProvider"
  let thisAssembly = Assembly.GetExecutingAssembly()

  // Make one provided type, called TypeN.
  let makeOneProvidedType (n:int) =
  …
  // Now generate 100 types
  let types = [ for i in 1 .. 100 -> makeOneProvidedType i ]

  // And add them to the namespace
  do this.AddNamespace(namespaceName, types)

[<assembly:TypeProviderAssembly>]
do()
```

<span data-ttu-id="e8969-142">Aby użyć tego dostawcy, Otwórz osobne wystąpienie programu Visual Studio, Utwórz skrypt języka F #, a następnie Dodaj odwołanie do dostawcy ze skryptu przy użyciu #r, jak pokazano w poniższym kodzie:</span><span class="sxs-lookup"><span data-stu-id="e8969-142">To use this provider, open a separate instance of Visual Studio, create an F# script, and then add a reference to the provider from your script by using #r as the following code shows:</span></span>

```fsharp
#r @".\bin\Debug\Samples.HelloWorldTypeProvider.dll"

let obj1 = Samples.HelloWorldTypeProvider.Type1("some data")

let obj2 = Samples.HelloWorldTypeProvider.Type1("some other data")

obj1.InstanceProperty
obj2.InstanceProperty

[ for index in 0 .. obj1.InstanceProperty-1 -> obj1.InstanceMethod(index) ]
[ for index in 0 .. obj2.InstanceProperty-1 -> obj2.InstanceMethod(index) ]

let data1 = Samples.HelloWorldTypeProvider.Type1.NestedType.StaticProperty35
```

<span data-ttu-id="e8969-143">Następnie poszukaj typów w `Samples.HelloWorldTypeProvider` przestrzeni nazw wygenerowanej przez dostawcę typów.</span><span class="sxs-lookup"><span data-stu-id="e8969-143">Then look for the types under the `Samples.HelloWorldTypeProvider` namespace that the type provider generated.</span></span>

<span data-ttu-id="e8969-144">Przed ponownym skompilowaniem dostawcy upewnij się, że wszystkie wystąpienia programu Visual Studio i F# Interactive korzystają z biblioteki DLL dostawcy.</span><span class="sxs-lookup"><span data-stu-id="e8969-144">Before you recompile the provider, make sure that you have closed all instances of Visual Studio and F# Interactive that are using the provider DLL.</span></span> <span data-ttu-id="e8969-145">W przeciwnym razie wystąpi błąd kompilacji, ponieważ wyjściowa biblioteka DLL zostanie zablokowana.</span><span class="sxs-lookup"><span data-stu-id="e8969-145">Otherwise, a build error will occur because the output DLL will be locked.</span></span>

<span data-ttu-id="e8969-146">Aby debugować tego dostawcę przy użyciu instrukcji Print, należy utworzyć skrypt, który ujawnia problem z dostawcą, a następnie użyć następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="e8969-146">To debug this provider by using print statements, make a script that exposes a problem with the provider, and then use the following code:</span></span>

```console
fsc.exe -r:bin\Debug\HelloWorldTypeProvider.dll script.fsx
```

<span data-ttu-id="e8969-147">Aby debugować tego dostawcę przy użyciu programu Visual Studio, Otwórz wiersz polecenia dla deweloperów dla programu Visual Studio z poświadczeniami administracyjnymi i uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="e8969-147">To debug this provider by using Visual Studio, open the Developer Command Prompt for Visual Studio with administrative credentials, and run the following command:</span></span>

```console
devenv.exe /debugexe fsc.exe -r:bin\Debug\HelloWorldTypeProvider.dll script.fsx
```

<span data-ttu-id="e8969-148">Alternatywnie Otwórz program Visual Studio, otwórz menu Debuguj, wybierz `Debug/Attach to process…` i Dołącz do innego procesu, w `devenv` którym edytujesz skrypt.</span><span class="sxs-lookup"><span data-stu-id="e8969-148">As an alternative, open Visual Studio, open the Debug menu, choose `Debug/Attach to process…`, and attach to another `devenv` process where you’re editing your script.</span></span> <span data-ttu-id="e8969-149">Korzystając z tej metody, można łatwiej przekierować konkretną logikę w dostawcy typów przez interakcyjne wpisywanie wyrażeń do drugiego wystąpienia (z pełną technologią IntelliSense i innymi funkcjami).</span><span class="sxs-lookup"><span data-stu-id="e8969-149">By using this method, you can more easily target particular logic in the type provider by interactively typing expressions into the second instance (with full IntelliSense and other features).</span></span>

<span data-ttu-id="e8969-150">Można wyłączyć debugowanie Tylko mój kod, aby lepiej identyfikować błędy w wygenerowanym kodzie.</span><span class="sxs-lookup"><span data-stu-id="e8969-150">You can disable Just My Code debugging to better identify errors in generated code.</span></span> <span data-ttu-id="e8969-151">Aby uzyskać informacje na temat włączania lub wyłączania tej funkcji, zobacz [nawigowanie po kodzie za pomocą debugera](/visualstudio/debugger/navigating-through-code-with-the-debugger).</span><span class="sxs-lookup"><span data-stu-id="e8969-151">For information about how to enable or disable this feature, see [Navigating through Code with the Debugger](/visualstudio/debugger/navigating-through-code-with-the-debugger).</span></span> <span data-ttu-id="e8969-152">Ponadto można również ustawić wyjątek pierwszej szansy do przechwycenia, otwierając `Debug` menu, a następnie wybierając `Exceptions` lub naciskając klawisze CTRL + ALT + E, aby otworzyć okno `Exceptions` dialogowe.</span><span class="sxs-lookup"><span data-stu-id="e8969-152">Also, you can also set first-chance exception catching by opening the `Debug` menu and then choosing `Exceptions` or by choosing the Ctrl+Alt+E keys to open the `Exceptions` dialog box.</span></span> <span data-ttu-id="e8969-153">W tym oknie dialogowym, w obszarze `Common Language Runtime Exceptions` , zaznacz `Thrown` pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="e8969-153">In that dialog box, under `Common Language Runtime Exceptions`, select the `Thrown` check box.</span></span>

### <a name="implementation-of-the-type-provider"></a><span data-ttu-id="e8969-154">Implementacja dostawcy typów</span><span class="sxs-lookup"><span data-stu-id="e8969-154">Implementation of the Type Provider</span></span>

<span data-ttu-id="e8969-155">Ta sekcja przeprowadzi Cię przez główne sekcje implementacji dostawcy typów.</span><span class="sxs-lookup"><span data-stu-id="e8969-155">This section walks you through the principal sections of the type provider implementation.</span></span> <span data-ttu-id="e8969-156">Najpierw należy zdefiniować typ niestandardowego dostawcy typów:</span><span class="sxs-lookup"><span data-stu-id="e8969-156">First, you define the type for the custom type provider itself:</span></span>

```fsharp
[<TypeProvider>]
type SampleTypeProvider(config: TypeProviderConfig) as this =
```

<span data-ttu-id="e8969-157">Ten typ musi być publiczny i musi być oznaczony atrybutem [TypeProvider](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-compilerservices-typeproviderattribute.html) , aby kompilator rozpoznał dostawcę typów, gdy oddzielny projekt F # odwołuje się do zestawu, który zawiera typ.</span><span class="sxs-lookup"><span data-stu-id="e8969-157">This type must be public, and you must mark it with the [TypeProvider](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-compilerservices-typeproviderattribute.html) attribute so that the compiler will recognize the type provider when a separate F# project references the assembly that contains the type.</span></span> <span data-ttu-id="e8969-158">Parametr *config* jest opcjonalny, a jeśli obecny, zawiera informacje o konfiguracji kontekstowej dla wystąpienia dostawcy typu, które tworzy kompilator F #.</span><span class="sxs-lookup"><span data-stu-id="e8969-158">The *config* parameter is optional, and, if present, contains contextual configuration information for the type provider instance that the F# compiler creates.</span></span>

<span data-ttu-id="e8969-159">Następnie należy zaimplementować interfejs [ITypeProvider](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-compilerservices-itypeprovider.html) .</span><span class="sxs-lookup"><span data-stu-id="e8969-159">Next, you implement the [ITypeProvider](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-compilerservices-itypeprovider.html) interface.</span></span> <span data-ttu-id="e8969-160">W takim przypadku należy użyć `TypeProviderForNamespaces` typu z `ProvidedTypes` interfejsu API jako typu podstawowego.</span><span class="sxs-lookup"><span data-stu-id="e8969-160">In this case, you use the `TypeProviderForNamespaces` type from the `ProvidedTypes` API as a base type.</span></span> <span data-ttu-id="e8969-161">Ten typ pomocnika może zapewnić skończoną kolekcję eagerly udostępnionych przestrzenie nazw, z których każdy zawiera bezpośrednio określoną liczbę stałych eagerly typów.</span><span class="sxs-lookup"><span data-stu-id="e8969-161">This helper type can provide a finite collection of eagerly provided namespaces, each of which directly contains a finite number of fixed, eagerly provided types.</span></span> <span data-ttu-id="e8969-162">W tym kontekście dostawca *eagerly* generuje typy, nawet jeśli nie są potrzebne lub używane.</span><span class="sxs-lookup"><span data-stu-id="e8969-162">In this context, the provider *eagerly* generates types even if they aren't needed or used.</span></span>

```fsharp
inherit TypeProviderForNamespaces(config)
```

<span data-ttu-id="e8969-163">Następnie zdefiniuj lokalne wartości prywatne, które określają przestrzeń nazw dla podanych typów i Znajdź sam zestaw dostawcy typów.</span><span class="sxs-lookup"><span data-stu-id="e8969-163">Next, define local private values that specify the namespace for the provided types, and find the type provider assembly itself.</span></span> <span data-ttu-id="e8969-164">Ten zestaw jest używany później jako logiczny typ nadrzędny dla podanych wymazanych typów.</span><span class="sxs-lookup"><span data-stu-id="e8969-164">This assembly is used later as the logical parent type of the erased types that are provided.</span></span>

```fsharp
let namespaceName = "Samples.HelloWorldTypeProvider"
let thisAssembly = Assembly.GetExecutingAssembly()
```

<span data-ttu-id="e8969-165">Następnie Utwórz funkcję, aby zapewnić każdy z typów Type1... Type100.</span><span class="sxs-lookup"><span data-stu-id="e8969-165">Next, create a function to provide each of the types Type1…Type100.</span></span> <span data-ttu-id="e8969-166">Ta funkcja została omówiona bardziej szczegółowo w dalszej części tego tematu.</span><span class="sxs-lookup"><span data-stu-id="e8969-166">This function is explained in more detail later in this topic.</span></span>

```fsharp
let makeOneProvidedType (n:int) = …
```

<span data-ttu-id="e8969-167">Następnie Wygeneruj dostarczone typy 100:</span><span class="sxs-lookup"><span data-stu-id="e8969-167">Next, generate the 100 provided types:</span></span>

```fsharp
let types = [ for i in 1 .. 100 -> makeOneProvidedType i ]
```

<span data-ttu-id="e8969-168">Następnie dodaj typy jako podaną przestrzeń nazw:</span><span class="sxs-lookup"><span data-stu-id="e8969-168">Next, add the types as a provided namespace:</span></span>

```fsharp
do this.AddNamespace(namespaceName, types)
```

<span data-ttu-id="e8969-169">Na koniec Dodaj atrybut zestawu, który wskazuje, że tworzysz bibliotekę DLL dostawcy typów:</span><span class="sxs-lookup"><span data-stu-id="e8969-169">Finally, add an assembly attribute that indicates that you are creating a type provider DLL:</span></span>

```fsharp
[<assembly:TypeProviderAssembly>]
do()
```

### <a name="providing-one-type-and-its-members"></a><span data-ttu-id="e8969-170">Udostępnianie jednego typu i jego składowych</span><span class="sxs-lookup"><span data-stu-id="e8969-170">Providing One Type And Its Members</span></span>

<span data-ttu-id="e8969-171">`makeOneProvidedType`Funkcja wykonuje rzeczywistą służbę dostarczającą jeden z typów.</span><span class="sxs-lookup"><span data-stu-id="e8969-171">The `makeOneProvidedType` function does the real work of providing one of the types.</span></span>

```fsharp
let makeOneProvidedType (n:int) =
…
```

<span data-ttu-id="e8969-172">W tym kroku opisano implementację tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="e8969-172">This step explains the implementation of this function.</span></span> <span data-ttu-id="e8969-173">Najpierw utwórz dostarczony typ (na przykład Type1, gdy n = 1 lub Type57, gdy n = 57).</span><span class="sxs-lookup"><span data-stu-id="e8969-173">First, create the provided type (for example, Type1, when n = 1, or Type57, when n = 57).</span></span>

```fsharp
// This is the provided type. It is an erased provided type and, in compiled code,
// will appear as type 'obj'.
let t = ProvidedTypeDefinition(thisAssembly, namespaceName,
                               "Type" + string n,
                               baseType = Some typeof<obj>)
```

<span data-ttu-id="e8969-174">Należy zwrócić uwagę na następujące kwestie:</span><span class="sxs-lookup"><span data-stu-id="e8969-174">You should note the following points:</span></span>

- <span data-ttu-id="e8969-175">Ten dostarczony typ jest wymazany.</span><span class="sxs-lookup"><span data-stu-id="e8969-175">This provided type is erased.</span></span>  <span data-ttu-id="e8969-176">Ponieważ wskazujesz, że typ podstawowy to `obj` , wystąpienia będą wyświetlane jako wartości typu [obj](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-obj.html) w skompilowanym kodzie.</span><span class="sxs-lookup"><span data-stu-id="e8969-176">Because you indicate that the base type is `obj`, instances will appear as values of type [obj](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-obj.html) in compiled code.</span></span>

- <span data-ttu-id="e8969-177">W przypadku określenia typu niezagnieżdżonego należy określić zestaw i przestrzeń nazw.</span><span class="sxs-lookup"><span data-stu-id="e8969-177">When you specify a non-nested type, you must specify the assembly and namespace.</span></span> <span data-ttu-id="e8969-178">W przypadku wymazanych typów zestaw powinien być samym zestawem dostawcy typów.</span><span class="sxs-lookup"><span data-stu-id="e8969-178">For erased types, the assembly should be the type provider assembly itself.</span></span>

<span data-ttu-id="e8969-179">Następnie Dodaj dokumentację XML do typu.</span><span class="sxs-lookup"><span data-stu-id="e8969-179">Next, add XML documentation to the type.</span></span> <span data-ttu-id="e8969-180">Ta dokumentacja jest opóźniona, to jest obliczana na żądanie, jeśli wymaga tego kompilator hosta.</span><span class="sxs-lookup"><span data-stu-id="e8969-180">This documentation is delayed, that is, computed on-demand if the host compiler needs it.</span></span>

```fsharp
t.AddXmlDocDelayed (fun () -> $"""This provided type {"Type" + string n}""")
```

<span data-ttu-id="e8969-181">Następnie Dodaj podaną Właściwość statyczną do typu:</span><span class="sxs-lookup"><span data-stu-id="e8969-181">Next you add a provided static property to the type:</span></span>

```fsharp
let staticProp = ProvidedProperty(propertyName = "StaticProperty",
                                  propertyType = typeof<string>,
                                  isStatic = true,
                                  getterCode = (fun args -> <@@ "Hello!" @@>))
```

<span data-ttu-id="e8969-182">Pobieranie tej właściwości będzie zawsze oceniane jako ciąg "Hello!".</span><span class="sxs-lookup"><span data-stu-id="e8969-182">Getting this property will always evaluate to the string "Hello!".</span></span> <span data-ttu-id="e8969-183">`GetterCode`Dla właściwości zostanie użyta oferta F #, która reprezentuje kod generowany przez kompilator hosta w celu pobrania właściwości.</span><span class="sxs-lookup"><span data-stu-id="e8969-183">The `GetterCode` for the property uses an F# quotation, which represents the code that the host compiler generates for getting the property.</span></span> <span data-ttu-id="e8969-184">Aby uzyskać więcej informacji na temat ofert, zobacz [cytaty kodu (F #)](../../language-reference/code-quotations.md).</span><span class="sxs-lookup"><span data-stu-id="e8969-184">For more information about quotations, see [Code Quotations (F#)](../../language-reference/code-quotations.md).</span></span>

<span data-ttu-id="e8969-185">Dodaj dokumentację XML do właściwości.</span><span class="sxs-lookup"><span data-stu-id="e8969-185">Add XML documentation to the property.</span></span>

```fsharp
staticProp.AddXmlDocDelayed(fun () -> "This is a static property")
```

<span data-ttu-id="e8969-186">Teraz Dołącz dostarczoną właściwość do podanego typu.</span><span class="sxs-lookup"><span data-stu-id="e8969-186">Now attach the provided property to the provided type.</span></span> <span data-ttu-id="e8969-187">Należy dołączyć podany element członkowski do jednego i tylko jednego typu.</span><span class="sxs-lookup"><span data-stu-id="e8969-187">You must attach a provided member to one and only one type.</span></span> <span data-ttu-id="e8969-188">W przeciwnym razie element członkowski nigdy nie będzie dostępny.</span><span class="sxs-lookup"><span data-stu-id="e8969-188">Otherwise, the member will never be accessible.</span></span>

```fsharp
t.AddMember staticProp
```

<span data-ttu-id="e8969-189">Teraz Utwórz dostarczony Konstruktor, który nie przyjmuje żadnych parametrów.</span><span class="sxs-lookup"><span data-stu-id="e8969-189">Now create a provided constructor that takes no parameters.</span></span>

```fsharp
let ctor = ProvidedConstructor(parameters = [ ],
                               invokeCode = (fun args -> <@@ "The object data" :> obj @@>))
```

<span data-ttu-id="e8969-190">`InvokeCode`Dla konstruktora zwraca cytat F #, który reprezentuje kod generowany przez kompilator hosta, gdy Konstruktor jest wywoływany.</span><span class="sxs-lookup"><span data-stu-id="e8969-190">The `InvokeCode` for the constructor returns an F# quotation, which represents the code that the host compiler generates when the constructor is called.</span></span> <span data-ttu-id="e8969-191">Na przykład można użyć następującego konstruktora:</span><span class="sxs-lookup"><span data-stu-id="e8969-191">For example, you can use the following constructor:</span></span>

```fsharp
new Type10()
```

<span data-ttu-id="e8969-192">Wystąpienie dostarczonego typu zostanie utworzone z danymi źródłowymi "dane obiektu".</span><span class="sxs-lookup"><span data-stu-id="e8969-192">An instance of the provided type will be created with underlying data "The object data".</span></span> <span data-ttu-id="e8969-193">Kod ujęty w cudzysłów zawiera konwersję do [obj](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-obj.html) , ponieważ ten typ jest wymazywanie tego dostarczonego typu (jak określono w przypadku zadeklarowanego typu).</span><span class="sxs-lookup"><span data-stu-id="e8969-193">The quoted code includes a conversion to [obj](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-obj.html) because that type is the erasure of this provided type (as you specified when you declared the provided type).</span></span>

<span data-ttu-id="e8969-194">Dodaj dokumentację XML do konstruktora i Dodaj dostarczony Konstruktor do podanego typu:</span><span class="sxs-lookup"><span data-stu-id="e8969-194">Add XML documentation to the constructor, and add the provided constructor to the provided type:</span></span>

```fsharp
ctor.AddXmlDocDelayed(fun () -> "This is a constructor")

t.AddMember ctor
```

<span data-ttu-id="e8969-195">Utwórz drugiego konstruktora, który przyjmuje jeden parametr:</span><span class="sxs-lookup"><span data-stu-id="e8969-195">Create a second provided constructor that takes one parameter:</span></span>

```fsharp
let ctor2 =
ProvidedConstructor(parameters = [ ProvidedParameter("data",typeof<string>) ],
                    invokeCode = (fun args -> <@@ (%%(args.[0]) : string) :> obj @@>))
```

<span data-ttu-id="e8969-196">`InvokeCode`Dla konstruktora ponownie zwraca cytat F #, który reprezentuje kod wygenerowany przez kompilator hosta dla wywołania metody.</span><span class="sxs-lookup"><span data-stu-id="e8969-196">The `InvokeCode` for the constructor again returns an F# quotation, which represents the code that the host compiler generated for a call to the method.</span></span> <span data-ttu-id="e8969-197">Na przykład można użyć następującego konstruktora:</span><span class="sxs-lookup"><span data-stu-id="e8969-197">For example, you can use the following constructor:</span></span>

```fsharp
new Type10("ten")
```

<span data-ttu-id="e8969-198">Wystąpienie dostarczonego typu jest tworzone z danymi źródłowymi "dziesięć".</span><span class="sxs-lookup"><span data-stu-id="e8969-198">An instance of the provided type is created with underlying data "ten".</span></span> <span data-ttu-id="e8969-199">Być może zauważono, że `InvokeCode` Funkcja zwraca cytat.</span><span class="sxs-lookup"><span data-stu-id="e8969-199">You may have already noticed that the `InvokeCode` function returns a quotation.</span></span> <span data-ttu-id="e8969-200">Wejście do tej funkcji jest listą wyrażeń, jeden na każdy parametr konstruktora.</span><span class="sxs-lookup"><span data-stu-id="e8969-200">The input to this function is a list of expressions, one per constructor parameter.</span></span> <span data-ttu-id="e8969-201">W takim przypadku wyrażenie reprezentujące wartość jednego parametru jest dostępne w `args.[0]` .</span><span class="sxs-lookup"><span data-stu-id="e8969-201">In this case, an expression that represents the single parameter value is available in `args.[0]`.</span></span> <span data-ttu-id="e8969-202">Kod wywołania konstruktora przekształca wartość zwracaną na typ wymazany `obj` .</span><span class="sxs-lookup"><span data-stu-id="e8969-202">The code for a call to the constructor coerces the return value to the erased type `obj`.</span></span> <span data-ttu-id="e8969-203">Po dodaniu drugiego podanego konstruktora do typu utworzysz podaną Właściwość wystąpienia:</span><span class="sxs-lookup"><span data-stu-id="e8969-203">After you add the second provided constructor to the type, you create a provided instance property:</span></span>

```fsharp
let instanceProp =
    ProvidedProperty(propertyName = "InstanceProperty",
                     propertyType = typeof<int>,
                     getterCode= (fun args ->
                        <@@ ((%%(args.[0]) : obj) :?> string).Length @@>))
instanceProp.AddXmlDocDelayed(fun () -> "This is an instance property")
t.AddMember instanceProp
```

<span data-ttu-id="e8969-204">Pobranie tej właściwości zwróci długość ciągu, który jest obiektem reprezentacji.</span><span class="sxs-lookup"><span data-stu-id="e8969-204">Getting this property will return the length of the string, which is the representation object.</span></span> <span data-ttu-id="e8969-205">`GetterCode`Właściwość zwraca cytat F #, który określa kod, który kompilator generuje do uzyskania właściwości.</span><span class="sxs-lookup"><span data-stu-id="e8969-205">The `GetterCode` property returns an F# quotation that specifies the code that the host compiler generates to get the property.</span></span> <span data-ttu-id="e8969-206">Podobnie `InvokeCode` , `GetterCode` Funkcja zwraca cytat.</span><span class="sxs-lookup"><span data-stu-id="e8969-206">Like `InvokeCode`, the `GetterCode` function returns a quotation.</span></span> <span data-ttu-id="e8969-207">Kompilator hosta wywołuje tę funkcję z listą argumentów.</span><span class="sxs-lookup"><span data-stu-id="e8969-207">The host compiler calls this function with a list of arguments.</span></span> <span data-ttu-id="e8969-208">W takim przypadku argumenty zawierają tylko pojedyncze wyrażenie, które reprezentuje wystąpienie, na którym jest wywoływana metoda pobierająca, do której można uzyskać dostęp za pomocą `args.[0]` .</span><span class="sxs-lookup"><span data-stu-id="e8969-208">In this case, the arguments include just the single expression that represents the instance upon which the getter is being called, which you can access by using `args.[0]`.</span></span> <span data-ttu-id="e8969-209">Implementacja `GetterCode` następnie jest przekształcana w cudzysłów wynikowy w typie wymazania `obj` , a Rzutowanie jest używane do zaspokojenia mechanizmu kompilatora do sprawdzania typów, które obiekt jest ciągiem.</span><span class="sxs-lookup"><span data-stu-id="e8969-209">The implementation of `GetterCode` then splices into the result quotation at the erased type `obj`, and a cast is used to satisfy the compiler's mechanism for checking types that the object is a string.</span></span> <span data-ttu-id="e8969-210">Następna część z `makeOneProvidedType` udostępnia metodę wystąpienia z jednym parametrem.</span><span class="sxs-lookup"><span data-stu-id="e8969-210">The next part of `makeOneProvidedType` provides an instance method with one parameter.</span></span>

```fsharp
let instanceMeth =
    ProvidedMethod(methodName = "InstanceMethod",
                   parameters = [ProvidedParameter("x",typeof<int>)],
                   returnType = typeof<char>,
                   invokeCode = (fun args ->
                       <@@ ((%%(args.[0]) : obj) :?> string).Chars(%%(args.[1]) : int) @@>))

instanceMeth.AddXmlDocDelayed(fun () -> "This is an instance method")
// Add the instance method to the type.
t.AddMember instanceMeth
```

<span data-ttu-id="e8969-211">Na koniec Utwórz zagnieżdżony typ, który zawiera 100 właściwości zagnieżdżonych.</span><span class="sxs-lookup"><span data-stu-id="e8969-211">Finally, create a nested type that contains 100 nested properties.</span></span> <span data-ttu-id="e8969-212">Tworzenie tego typu zagnieżdżonego i jego właściwości jest opóźnione, czyli obliczanym na żądanie.</span><span class="sxs-lookup"><span data-stu-id="e8969-212">The creation of this nested type and its properties is delayed, that is, computed on-demand.</span></span>

```fsharp
t.AddMembersDelayed(fun () ->
  let nestedType = ProvidedTypeDefinition("NestedType", Some typeof<obj>)

  nestedType.AddMembersDelayed (fun () ->
    let staticPropsInNestedType =
      [
          for i in 1 .. 100 ->
              let valueOfTheProperty = "I am string "  + string i

              let p =
                ProvidedProperty(propertyName = "StaticProperty" + string i,
                  propertyType = typeof<string>,
                  isStatic = true,
                  getterCode= (fun args -> <@@ valueOfTheProperty @@>))

              p.AddXmlDocDelayed(fun () ->
                  $"This is StaticProperty{i} on NestedType")

              p
      ]

    staticPropsInNestedType)

  [nestedType])
```

### <a name="details-about-erased-provided-types"></a><span data-ttu-id="e8969-213">Szczegóły dotyczące wymazanych typów</span><span class="sxs-lookup"><span data-stu-id="e8969-213">Details about Erased Provided Types</span></span>

<span data-ttu-id="e8969-214">Przykład w tej sekcji zawiera tylko *wymazane dostarczone typy*, które są szczególnie przydatne w następujących sytuacjach:</span><span class="sxs-lookup"><span data-stu-id="e8969-214">The example in this section provides only *erased provided types*, which are particularly useful in the following situations:</span></span>

- <span data-ttu-id="e8969-215">Podczas pisania dostawcy dla przestrzeni informacyjnej zawierającej tylko dane i metody.</span><span class="sxs-lookup"><span data-stu-id="e8969-215">When you are writing a provider for an information space that contains only data and methods.</span></span>

- <span data-ttu-id="e8969-216">Podczas pisania dostawcy, w którym dokładna semantyka typu środowiska uruchomieniowego nie jest krytyczna dla praktycznego użycia przestrzeni informacyjnej.</span><span class="sxs-lookup"><span data-stu-id="e8969-216">When you are writing a provider where accurate runtime-type semantics aren't critical for practical use of the information space.</span></span>

- <span data-ttu-id="e8969-217">Podczas pisania dostawcy dla obszaru informacyjnego, który jest tak duży i połączony, nie jest technicznie wykonalny, aby generować rzeczywiste typy .NET dla obszaru informacji.</span><span class="sxs-lookup"><span data-stu-id="e8969-217">When you are writing a provider for an information space that is so large and interconnected that it isn’t technically feasible to generate real .NET types for the information space.</span></span>

<span data-ttu-id="e8969-218">W tym przykładzie każdy dostarczony typ jest wymazany do typu `obj` , a wszystkie zastosowania typu będą wyświetlane jako typ `obj` w skompilowanym kodzie.</span><span class="sxs-lookup"><span data-stu-id="e8969-218">In this example, each provided type is erased to type `obj`, and all uses of the type will appear as type `obj` in compiled code.</span></span> <span data-ttu-id="e8969-219">W rzeczywistości obiekty bazowe w tych przykładach są ciągami, ale typ będzie wyświetlany jako `System.Object` w skompilowanym kodzie platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="e8969-219">In fact, the underlying objects in these examples are strings, but the type will appear as `System.Object` in .NET compiled code.</span></span> <span data-ttu-id="e8969-220">Podobnie jak w przypadku wszystkich użycia typu wymazywania, można użyć jawnego pakowania, rozpakowywania i rzutowania na wymazywane typy poddanych.</span><span class="sxs-lookup"><span data-stu-id="e8969-220">As with all uses of type erasure, you can use explicit boxing, unboxing, and casting to subvert erased types.</span></span> <span data-ttu-id="e8969-221">W takim przypadku wyjątek rzutowania, który jest nieprawidłowy, może wynikać, gdy obiekt jest używany.</span><span class="sxs-lookup"><span data-stu-id="e8969-221">In this case, a cast exception that isn’t valid may result when the object is used.</span></span> <span data-ttu-id="e8969-222">Środowisko uruchomieniowe dostawcy może zdefiniować własny prywatny typ reprezentacji, aby pomóc w ochronie przed fałszywymi reprezentacjami.</span><span class="sxs-lookup"><span data-stu-id="e8969-222">A provider runtime can define its own private representation type to help protect against false representations.</span></span> <span data-ttu-id="e8969-223">Nie można definiować wymazanych typów w języku F #.</span><span class="sxs-lookup"><span data-stu-id="e8969-223">You can’t define erased types in F# itself.</span></span> <span data-ttu-id="e8969-224">Tylko udostępniane typy mogą zostać wymazane.</span><span class="sxs-lookup"><span data-stu-id="e8969-224">Only provided types may be erased.</span></span> <span data-ttu-id="e8969-225">Należy zrozumieć konsekwencje, zarówno praktycznie, jak i semantykę, przy użyciu wymazanych typów dla dostawcy typu lub dostawcy, który udostępnia wymazane typy.</span><span class="sxs-lookup"><span data-stu-id="e8969-225">You must understand the ramifications, both practical and semantic, of using either erased types for your type provider or a provider that provides erased types.</span></span> <span data-ttu-id="e8969-226">Typ wymazany nie ma rzeczywistego typu .NET.</span><span class="sxs-lookup"><span data-stu-id="e8969-226">An erased type has no real .NET type.</span></span> <span data-ttu-id="e8969-227">W związku z tym nie można przeprowadzić dokładnego odbicia w typie i można przeliczyć wymazywane typy, jeśli używasz rzutowania środowiska uruchomieniowego i innych technik, które opierają się na dokładnej semantyce typu środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="e8969-227">Therefore, you cannot do accurate reflection over the type, and you might subvert erased types if you use runtime casts and other techniques that rely on exact runtime type semantics.</span></span> <span data-ttu-id="e8969-228">Podwersja wymazanych typów często skutkuje wyjątkami rzutowania typu w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="e8969-228">Subversion of erased types frequently results in type cast exceptions at runtime.</span></span>

### <a name="choosing-representations-for-erased-provided-types"></a><span data-ttu-id="e8969-229">Wybieranie reprezentacji dla wymazanych podanych typów</span><span class="sxs-lookup"><span data-stu-id="e8969-229">Choosing Representations for Erased Provided Types</span></span>

<span data-ttu-id="e8969-230">W przypadku niektórych użycia wymazanych typów nie jest wymagana żadna reprezentacja.</span><span class="sxs-lookup"><span data-stu-id="e8969-230">For some uses of erased provided types, no representation is required.</span></span> <span data-ttu-id="e8969-231">Na przykład typ, który został wymazany, może zawierać tylko statyczne właściwości i składowe bez konstruktorów, a żadne metody lub właściwości nie zwróci wystąpienia typu.</span><span class="sxs-lookup"><span data-stu-id="e8969-231">For example, the erased provided type might contain only static properties and members and no constructors, and no methods or properties would return an instance of the type.</span></span> <span data-ttu-id="e8969-232">Jeśli można uzyskać dostęp do wystąpień podanego typu, należy wziąć pod uwagę następujące pytania:</span><span class="sxs-lookup"><span data-stu-id="e8969-232">If you can reach instances of an erased provided type, you must consider the following questions:</span></span>

<span data-ttu-id="e8969-233">**Co to jest wymazanie podanego typu?**</span><span class="sxs-lookup"><span data-stu-id="e8969-233">**What is the erasure of a provided type?**</span></span>

- <span data-ttu-id="e8969-234">Wymazanie podanego typu określa sposób wyświetlania w skompilowanym kodzie .NET.</span><span class="sxs-lookup"><span data-stu-id="e8969-234">The erasure of a provided type is how the type appears in compiled .NET code.</span></span>

- <span data-ttu-id="e8969-235">Wymazywanie dostarczonego typu wymazanej klasy jest zawsze pierwszym niewymazanym typem podstawowym w łańcuchu dziedziczenia typu.</span><span class="sxs-lookup"><span data-stu-id="e8969-235">The erasure of a provided erased class type is always the first non-erased base type in the inheritance chain of the type.</span></span>

- <span data-ttu-id="e8969-236">Wymazywanie dostarczonego typu interfejsu jest zawsze `System.Object` .</span><span class="sxs-lookup"><span data-stu-id="e8969-236">The erasure of a provided erased interface type is always `System.Object`.</span></span>

<span data-ttu-id="e8969-237">**Jakie są reprezentacje dostarczonego typu?**</span><span class="sxs-lookup"><span data-stu-id="e8969-237">**What are the representations of a provided type?**</span></span>

- <span data-ttu-id="e8969-238">Zestaw możliwych obiektów dla podanego typu wymazanego są nazywane jego reprezentacjami.</span><span class="sxs-lookup"><span data-stu-id="e8969-238">The set of possible objects for an erased provided type are called its representations.</span></span> <span data-ttu-id="e8969-239">W przykładzie w tym dokumencie reprezentacje wszystkich wymazanych typów `Type1..Type100` są zawsze obiektami ciągu.</span><span class="sxs-lookup"><span data-stu-id="e8969-239">In the example in this document, the representations of all the erased provided types `Type1..Type100` are always string objects.</span></span>

<span data-ttu-id="e8969-240">Wszystkie reprezentacje dostarczonego typu muszą być zgodne z wymazywaniem podanego typu.</span><span class="sxs-lookup"><span data-stu-id="e8969-240">All representations of a provided type must be compatible with the erasure of the provided type.</span></span> <span data-ttu-id="e8969-241">(W przeciwnym razie kompilator języka F # zwróci błąd dotyczący użycia dostawcy typów lub niemożliwy do sprawdzenia kod platformy .NET, który jest nieprawidłowy).</span><span class="sxs-lookup"><span data-stu-id="e8969-241">(Otherwise, either the F# compiler will give an error for a use of the type provider, or unverifiable .NET code that isn't valid will be generated.</span></span> <span data-ttu-id="e8969-242">Dostawca typów jest nieprawidłowy, jeśli zwraca kod, który zawiera nieprawidłową reprezentację.</span><span class="sxs-lookup"><span data-stu-id="e8969-242">A type provider isn’t valid if it returns code that gives a  representation that isn't valid.)</span></span>

<span data-ttu-id="e8969-243">Można wybrać reprezentację dla dostarczonych obiektów przy użyciu jednej z następujących metod, które są bardzo popularne:</span><span class="sxs-lookup"><span data-stu-id="e8969-243">You can choose a representation for provided objects by using either of the following approaches, both of which are very common:</span></span>

- <span data-ttu-id="e8969-244">Jeśli po prostu udostępnisz silnie wpisaną otokę na istniejącym typie .NET, często ma sens, aby typ mógł zostać wymazany do tego typu, używaj wystąpień tego typu jako reprezentacji lub obu.</span><span class="sxs-lookup"><span data-stu-id="e8969-244">If you're simply providing a strongly typed wrapper over an existing .NET type, it often makes sense for your type to erase to that type, use instances of that type as representations, or both.</span></span> <span data-ttu-id="e8969-245">To podejście jest odpowiednie, gdy większość istniejących metod na tym typie nadal ma sens, gdy używana jest silnie wpisana wersja.</span><span class="sxs-lookup"><span data-stu-id="e8969-245">This approach is appropriate when most of the existing methods on that type still make sense when using the strongly typed version.</span></span>

- <span data-ttu-id="e8969-246">Jeśli chcesz utworzyć interfejs API, który różni się znacznie od istniejącego interfejsu API platformy .NET, warto utworzyć typy środowiska uruchomieniowego, które będą typu wymazywania i reprezentacji dla dostarczonych typów.</span><span class="sxs-lookup"><span data-stu-id="e8969-246">If you want to create an API that differs significantly from any existing .NET API, it makes sense to create runtime types that will be the type erasure and representations for the provided types.</span></span>

<span data-ttu-id="e8969-247">W przykładzie w tym dokumencie są stosowane ciągi jako reprezentacje dostarczonych obiektów.</span><span class="sxs-lookup"><span data-stu-id="e8969-247">The example in this document uses strings as representations of provided objects.</span></span> <span data-ttu-id="e8969-248">Często może być konieczne użycie innych obiektów do przedstawienia.</span><span class="sxs-lookup"><span data-stu-id="e8969-248">Frequently, it may be appropriate to use other objects for representations.</span></span> <span data-ttu-id="e8969-249">Na przykład można użyć słownika jako zbioru właściwości:</span><span class="sxs-lookup"><span data-stu-id="e8969-249">For example, you may use a dictionary as a property bag:</span></span>

```fsharp
ProvidedConstructor(parameters = [],
    invokeCode= (fun args -> <@@ (new Dictionary<string,obj>()) :> obj @@>))
```

<span data-ttu-id="e8969-250">Alternatywnie można zdefiniować typ w dostawcy typu, który będzie używany w czasie wykonywania w celu utworzenia reprezentacji, wraz z co najmniej jedną operacją wykonawczą:</span><span class="sxs-lookup"><span data-stu-id="e8969-250">As an alternative, you may define a type in your type provider that will be used at runtime to form the representation, along with one or more runtime operations:</span></span>

```fsharp
type DataObject() =
    let data = Dictionary<string,obj>()
    member x.RuntimeOperation() = data.Count
```

<span data-ttu-id="e8969-251">Podane elementy członkowskie mogą następnie konstruować wystąpienia tego typu obiektu:</span><span class="sxs-lookup"><span data-stu-id="e8969-251">Provided members can then construct instances of this object type:</span></span>

```fsharp
ProvidedConstructor(parameters = [],
    invokeCode= (fun args -> <@@ (new DataObject()) :> obj @@>))
```

<span data-ttu-id="e8969-252">W takim przypadku możesz (opcjonalnie) używać tego typu jako typu wymazywanego przez określenie tego typu jako `baseType` podczas konstruowania `ProvidedTypeDefinition` :</span><span class="sxs-lookup"><span data-stu-id="e8969-252">In this case, you may (optionally) use this type as the type erasure by specifying this type as the `baseType` when constructing the `ProvidedTypeDefinition`:</span></span>

```fsharp
ProvidedTypeDefinition(…, baseType = Some typeof<DataObject> )
…
ProvidedConstructor(…, InvokeCode = (fun args -> <@@ new DataObject() @@>), …)
```

### <a name="key-lessons"></a><span data-ttu-id="e8969-253">Najważniejsze lekcje</span><span class="sxs-lookup"><span data-stu-id="e8969-253">Key Lessons</span></span>

<span data-ttu-id="e8969-254">W poprzedniej sekcji wyjaśniono, jak utworzyć prostego, wymazywając dostawcę typów, który zapewnia zakres typów, właściwości i metod.</span><span class="sxs-lookup"><span data-stu-id="e8969-254">The previous section explained how to create a simple erasing type provider that provides a range of types, properties, and methods.</span></span> <span data-ttu-id="e8969-255">W tej sekcji wyjaśniono również koncepcję typu wymazywania, w tym niektóre zalety i wady zapewniania wymazanych typów od dostawcy typów oraz omówione reprezentacje typów wymazanych.</span><span class="sxs-lookup"><span data-stu-id="e8969-255">This section also explained the concept of type erasure, including some of the advantages and disadvantages of providing erased types from a type provider, and discussed representations of erased types.</span></span>

## <a name="a-type-provider-that-uses-static-parameters"></a><span data-ttu-id="e8969-256">Dostawca typów, który używa parametrów statycznych</span><span class="sxs-lookup"><span data-stu-id="e8969-256">A Type Provider That Uses Static Parameters</span></span>

<span data-ttu-id="e8969-257">Możliwość Sparametryzuj dostawców typów przez dane statyczne umożliwia wiele interesujących scenariuszy, nawet w przypadkach, gdy dostawca nie musi uzyskiwać dostępu do danych lokalnych lub zdalnych.</span><span class="sxs-lookup"><span data-stu-id="e8969-257">The ability to parameterize type providers by static data enables many interesting scenarios, even in cases when the provider doesn't need to access any local or remote data.</span></span> <span data-ttu-id="e8969-258">W tej sekcji przedstawiono podstawowe techniki tworzenia tego dostawcy.</span><span class="sxs-lookup"><span data-stu-id="e8969-258">In this section, you’ll learn some basic techniques for putting together such a provider.</span></span>

### <a name="type-checked-regex-provider"></a><span data-ttu-id="e8969-259">Dostawca zaznaczonego wyrażenia regularnego typu</span><span class="sxs-lookup"><span data-stu-id="e8969-259">Type Checked Regex Provider</span></span>

<span data-ttu-id="e8969-260">Załóżmy, że chcesz zaimplementować dostawcę typów dla wyrażeń regularnych, które zawijają <xref:System.Text.RegularExpressions.Regex> biblioteki .NET w interfejsie, który zapewnia następujące gwarancje czasu kompilacji:</span><span class="sxs-lookup"><span data-stu-id="e8969-260">Imagine that you want to implement a type provider for regular expressions that wraps the .NET <xref:System.Text.RegularExpressions.Regex> libraries in an interface that provides the following compile-time guarantees:</span></span>

- <span data-ttu-id="e8969-261">Sprawdzanie, czy wyrażenie regularne jest prawidłowe.</span><span class="sxs-lookup"><span data-stu-id="e8969-261">Verifying whether a regular expression is valid.</span></span>

- <span data-ttu-id="e8969-262">Udostępnianie nazwanych właściwości na dopasowaniach, które są oparte na dowolnych nazwach grup w wyrażeniu regularnym.</span><span class="sxs-lookup"><span data-stu-id="e8969-262">Providing named properties on matches that are based on any group names in the regular expression.</span></span>

<span data-ttu-id="e8969-263">W tej sekcji pokazano, jak za pomocą dostawców typów utworzyć `RegexTyped` Typ, który wzorzec wyrażenia regularnego parameterizes, aby zapewnić te korzyści.</span><span class="sxs-lookup"><span data-stu-id="e8969-263">This section shows you how to use type providers to create a `RegexTyped` type that the regular expression pattern parameterizes to provide these benefits.</span></span> <span data-ttu-id="e8969-264">Kompilator zgłosi błąd, jeśli dostarczony wzorzec jest nieprawidłowy, a dostawca typów może wyodrębnić grupy ze wzorca, aby można było uzyskać do nich dostęp przy użyciu nazwanych właściwości w dopasowań.</span><span class="sxs-lookup"><span data-stu-id="e8969-264">The compiler will report an error if the supplied pattern isn't valid, and the type provider can extract the groups from the pattern so that you can access them by using named properties on matches.</span></span> <span data-ttu-id="e8969-265">Podczas projektowania dostawcy typów należy rozważyć sposób, w jaki jego uwidoczniony interfejs API powinien wyglądać użytkownikom końcowym i jak ten projekt będzie tłumaczyć na kod platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="e8969-265">When you design a type provider, you should consider how its exposed API should look to end users and how this design will translate to .NET code.</span></span> <span data-ttu-id="e8969-266">Poniższy przykład pokazuje, jak używać takiego interfejsu API do pobierania składników kodu obszaru:</span><span class="sxs-lookup"><span data-stu-id="e8969-266">The following example shows how to use such an API to get the components of the area code:</span></span>

```fsharp
type T = RegexTyped< @"(?<AreaCode>^\d{3})-(?<PhoneNumber>\d{3}-\d{4}$)">
let reg = T()
let result = T.IsMatch("425-555-2345")
let r = reg.Match("425-555-2345").Group_AreaCode.Value //r equals "425"
```

<span data-ttu-id="e8969-267">Poniższy przykład pokazuje, jak dostawca typów tłumaczy te wywołania:</span><span class="sxs-lookup"><span data-stu-id="e8969-267">The following example shows how the type provider translates these calls:</span></span>

```fsharp
let reg = new Regex(@"(?<AreaCode>^\d{3})-(?<PhoneNumber>\d{3}-\d{4}$)")
let result = reg.IsMatch("425-123-2345")
let r = reg.Match("425-123-2345").Groups.["AreaCode"].Value //r equals "425"
```

<span data-ttu-id="e8969-268">Pamiętaj o następujących kwestiach:</span><span class="sxs-lookup"><span data-stu-id="e8969-268">Note the following points:</span></span>

- <span data-ttu-id="e8969-269">Standardowy typ wyrażenia regularnego reprezentuje `RegexTyped` Typ sparametryzowany.</span><span class="sxs-lookup"><span data-stu-id="e8969-269">The standard Regex type represents the parameterized `RegexTyped` type.</span></span>

- <span data-ttu-id="e8969-270">`RegexTyped`Konstruktor skutkuje wywołaniem konstruktora wyrażenia regularnego, przekazując w argument typu statycznego wzorca.</span><span class="sxs-lookup"><span data-stu-id="e8969-270">The `RegexTyped` constructor results in a call to the Regex constructor, passing in the static type argument for the pattern.</span></span>

- <span data-ttu-id="e8969-271">Wyniki `Match` metody są reprezentowane przez standardowy <xref:System.Text.RegularExpressions.Match> Typ.</span><span class="sxs-lookup"><span data-stu-id="e8969-271">The results of the `Match` method are represented by the standard <xref:System.Text.RegularExpressions.Match> type.</span></span>

- <span data-ttu-id="e8969-272">Każda nazwana grupa skutkuje podaną właściwością i uzyskuje dostęp do właściwości w wyniku użycia indeksatora w `Groups` kolekcji dopasowania.</span><span class="sxs-lookup"><span data-stu-id="e8969-272">Each named group results in a provided property, and accessing the property results in a use of an indexer on a match’s `Groups` collection.</span></span>

<span data-ttu-id="e8969-273">Poniższy kod stanowi rdzeń logiki w celu zaimplementowania takiego dostawcy, a ten przykład pomija dodanie wszystkich członków do podanego typu.</span><span class="sxs-lookup"><span data-stu-id="e8969-273">The following code is the core of the logic to implement such a provider, and this example omits the addition of all members to the provided type.</span></span> <span data-ttu-id="e8969-274">Informacje o każdym dodawanym członku znajdują się w odpowiedniej sekcji w dalszej części tego tematu.</span><span class="sxs-lookup"><span data-stu-id="e8969-274">For information about each added member, see the appropriate section later in this topic.</span></span> <span data-ttu-id="e8969-275">Aby uzyskać pełny kod, Pobierz próbkę z [przykładowego pakietu F # 3,0](https://archive.codeplex.com/?p=fsharp3sample) w witrynie sieci Web CodePlex.</span><span class="sxs-lookup"><span data-stu-id="e8969-275">For the full code, download the sample from the [F# 3.0 Sample Pack](https://archive.codeplex.com/?p=fsharp3sample) on the CodePlex website.</span></span>

```fsharp
namespace Samples.FSharp.RegexTypeProvider

open System.Reflection
open Microsoft.FSharp.Core.CompilerServices
open Samples.FSharp.ProvidedTypes
open System.Text.RegularExpressions

[<TypeProvider>]
type public CheckedRegexProvider() as this =
    inherit TypeProviderForNamespaces()

    // Get the assembly and namespace used to house the provided types
    let thisAssembly = Assembly.GetExecutingAssembly()
    let rootNamespace = "Samples.FSharp.RegexTypeProvider"
    let baseTy = typeof<obj>
    let staticParams = [ProvidedStaticParameter("pattern", typeof<string>)]

    let regexTy = ProvidedTypeDefinition(thisAssembly, rootNamespace, "RegexTyped", Some baseTy)

    do regexTy.DefineStaticParameters(
        parameters=staticParams,
        instantiationFunction=(fun typeName parameterValues ->

          match parameterValues with
          | [| :? string as pattern|] ->

            // Create an instance of the regular expression.
            //
            // This will fail with System.ArgumentException if the regular expression is not valid.
            // The exception will escape the type provider and be reported in client code.
            let r = System.Text.RegularExpressions.Regex(pattern)

            // Declare the typed regex provided type.
            // The type erasure of this type is 'obj', even though the representation will always be a Regex
            // This, combined with hiding the object methods, makes the IntelliSense experience simpler.
            let ty =
              ProvidedTypeDefinition(
                thisAssembly,
                rootNamespace,
                typeName,
                baseType = Some baseTy)

            ...

            ty
          | _ -> failwith "unexpected parameter values"))

    do this.AddNamespace(rootNamespace, [regexTy])

[<TypeProviderAssembly>]
do ()
```

<span data-ttu-id="e8969-276">Pamiętaj o następujących kwestiach:</span><span class="sxs-lookup"><span data-stu-id="e8969-276">Note the following points:</span></span>

- <span data-ttu-id="e8969-277">Dostawca typów przyjmuje dwa parametry statyczne: `pattern` , który jest obowiązkowy, i `options` , które są opcjonalne (z powodu podanej wartości domyślnej).</span><span class="sxs-lookup"><span data-stu-id="e8969-277">The type provider takes two static parameters: the `pattern`, which is mandatory, and the `options`, which are optional (because a default value is provided).</span></span>

- <span data-ttu-id="e8969-278">Po podaniu argumentów statycznych utworzysz wystąpienie wyrażenia regularnego.</span><span class="sxs-lookup"><span data-stu-id="e8969-278">After the static arguments are supplied, you create an instance of the regular expression.</span></span> <span data-ttu-id="e8969-279">To wystąpienie zgłosi wyjątek, jeśli wyrażenie regularne jest źle sformułowane i ten błąd będzie raportowany użytkownikom.</span><span class="sxs-lookup"><span data-stu-id="e8969-279">This instance will throw an exception if the Regex is malformed, and this error will be reported to users.</span></span>

- <span data-ttu-id="e8969-280">W ramach `DefineStaticParameters` wywołania zwrotnego definiujesz typ, który będzie zwracany po dostarczeniu argumentów.</span><span class="sxs-lookup"><span data-stu-id="e8969-280">Within the `DefineStaticParameters` callback, you define the type that will be returned after the arguments are supplied.</span></span>

- <span data-ttu-id="e8969-281">Ten kod `HideObjectMethods` jest ustawiony na wartość true, aby środowisko IntelliSense pozostało usprawnione.</span><span class="sxs-lookup"><span data-stu-id="e8969-281">This code sets `HideObjectMethods` to true so that the IntelliSense experience will remain streamlined.</span></span> <span data-ttu-id="e8969-282">Ten atrybut powoduje `Equals` , że `GetHashCode` elementy członkowskie,, `Finalize` i `GetType` są pomijane z list IntelliSense dla podanego obiektu.</span><span class="sxs-lookup"><span data-stu-id="e8969-282">This attribute causes the `Equals`, `GetHashCode`, `Finalize`, and `GetType` members to be suppressed from IntelliSense lists for a provided object.</span></span>

- <span data-ttu-id="e8969-283">Używasz `obj` jako podstawowego typu metody, ale użyjesz `Regex` obiektu jako reprezentacji tego typu w czasie wykonywania, jak pokazano w następnym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="e8969-283">You use `obj` as the base type of the method, but you’ll use a `Regex` object as the runtime representation of this type, as the next example shows.</span></span>

- <span data-ttu-id="e8969-284">Wywołanie `Regex` konstruktora zgłasza, <xref:System.ArgumentException> gdy wyrażenie regularne jest nieprawidłowe.</span><span class="sxs-lookup"><span data-stu-id="e8969-284">The call to the `Regex` constructor throws a <xref:System.ArgumentException> when a regular expression isn’t valid.</span></span> <span data-ttu-id="e8969-285">Kompilator przechwytuje ten wyjątek i zgłasza komunikat o błędzie do użytkownika w czasie kompilacji lub w edytorze programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e8969-285">The compiler catches this exception and reports an error message to the user at compile time or in the Visual Studio editor.</span></span> <span data-ttu-id="e8969-286">Ten wyjątek umożliwia zweryfikowanie wyrażeń regularnych bez uruchamiania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e8969-286">This exception enables regular expressions to be validated without running an application.</span></span>

<span data-ttu-id="e8969-287">Zdefiniowany powyżej typ nie jest jeszcze użyteczny, ponieważ nie zawiera żadnych istotnych metod lub właściwości.</span><span class="sxs-lookup"><span data-stu-id="e8969-287">The type defined above isn't useful yet because it doesn’t contain any meaningful methods or properties.</span></span> <span data-ttu-id="e8969-288">Najpierw Dodaj metodę statyczną `IsMatch` :</span><span class="sxs-lookup"><span data-stu-id="e8969-288">First, add a static `IsMatch` method:</span></span>

```fsharp
let isMatch =
    ProvidedMethod(
        methodName = "IsMatch",
        parameters = [ProvidedParameter("input", typeof<string>)],
        returnType = typeof<bool>,
        isStatic = true,
        invokeCode = fun args -> <@@ Regex.IsMatch(%%args.[0], pattern) @@>)

isMatch.AddXmlDoc "Indicates whether the regular expression finds a match in the specified input string."
ty.AddMember isMatch
```

<span data-ttu-id="e8969-289">Poprzedni kod definiuje metodę `IsMatch` , która pobiera ciąg jako dane wejściowe i zwraca `bool` .</span><span class="sxs-lookup"><span data-stu-id="e8969-289">The previous code defines a method `IsMatch`, which takes a string as input and returns a `bool`.</span></span> <span data-ttu-id="e8969-290">Jedyną lewę częścią jest użycie `args` argumentu w `InvokeCode` definicji.</span><span class="sxs-lookup"><span data-stu-id="e8969-290">The only tricky part is the use of the `args` argument within the `InvokeCode` definition.</span></span> <span data-ttu-id="e8969-291">W tym przykładzie `args` jest to lista cytatów, która reprezentuje argumenty tej metody.</span><span class="sxs-lookup"><span data-stu-id="e8969-291">In this example, `args` is a list of quotations that represents the arguments to this method.</span></span> <span data-ttu-id="e8969-292">Jeśli metoda jest metodą wystąpienia, pierwszy argument reprezentuje `this` argument.</span><span class="sxs-lookup"><span data-stu-id="e8969-292">If the method is an instance method, the first argument represents the `this` argument.</span></span> <span data-ttu-id="e8969-293">Jednak dla metody statycznej argumenty są tylko jawnymi argumentami metody.</span><span class="sxs-lookup"><span data-stu-id="e8969-293">However, for a static method, the arguments are all just the explicit arguments to the method.</span></span> <span data-ttu-id="e8969-294">Należy zauważyć, że typ cytowanej wartości powinien być zgodny z określonym zwracanym typem (w tym przypadku `bool` ).</span><span class="sxs-lookup"><span data-stu-id="e8969-294">Note that the type of the quoted value should match the specified return type (in this case, `bool`).</span></span> <span data-ttu-id="e8969-295">Należy również zauważyć, że ten kod używa `AddXmlDoc` metody, aby upewnić się, że podana Metoda ma również przydatną dokumentację, którą można dostarczyć za pośrednictwem technologii IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="e8969-295">Also note that this code uses the `AddXmlDoc` method to make sure that the provided method also has useful documentation, which you can supply through IntelliSense.</span></span>

<span data-ttu-id="e8969-296">Następnie Dodaj metodę dopasowania wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="e8969-296">Next, add an instance Match method.</span></span> <span data-ttu-id="e8969-297">Jednakże ta metoda powinna zwracać wartość dostarczonego `Match` typu, aby można było uzyskać dostęp do grup w sposób silnie określony.</span><span class="sxs-lookup"><span data-stu-id="e8969-297">However, this method should return a value of a provided `Match` type so that the groups can be accessed in a strongly typed fashion.</span></span> <span data-ttu-id="e8969-298">W rezultacie należy najpierw zadeklarować `Match` Typ.</span><span class="sxs-lookup"><span data-stu-id="e8969-298">Thus, you first declare the `Match` type.</span></span> <span data-ttu-id="e8969-299">Ponieważ ten typ jest zależny od wzorca, który został dostarczony jako argument statyczny, ten typ musi być zagnieżdżony w definicji typu sparametryzowanego:</span><span class="sxs-lookup"><span data-stu-id="e8969-299">Because this type depends on the pattern that was supplied as a static argument, this type must be nested within the parameterized type definition:</span></span>

```fsharp
let matchTy =
    ProvidedTypeDefinition(
        "MatchType",
        baseType = Some baseTy,
        hideObjectMethods = true)

ty.AddMember matchTy
```

<span data-ttu-id="e8969-300">Następnie należy dodać jedną właściwość do typu dopasowania dla każdej grupy.</span><span class="sxs-lookup"><span data-stu-id="e8969-300">You then add one property to the Match type for each group.</span></span> <span data-ttu-id="e8969-301">W czasie wykonywania dopasowanie jest reprezentowane jako <xref:System.Text.RegularExpressions.Match> wartość, dlatego w cudzysłowie definiującym właściwość musi być używana <xref:System.Text.RegularExpressions.Match.Groups> indeksowana właściwość w celu uzyskania odpowiedniej grupy.</span><span class="sxs-lookup"><span data-stu-id="e8969-301">At runtime, a match is represented as a <xref:System.Text.RegularExpressions.Match> value, so the quotation that defines the property must use the <xref:System.Text.RegularExpressions.Match.Groups> indexed property to get the relevant group.</span></span>

```fsharp
for group in r.GetGroupNames() do
    // Ignore the group named 0, which represents all input.
    if group <> "0" then
    let prop =
      ProvidedProperty(
        propertyName = group,
        propertyType = typeof<Group>,
        getterCode = fun args -> <@@ ((%%args.[0]:obj) :?> Match).Groups.[group] @@>)
        prop.AddXmlDoc($"""Gets the ""{group}"" group from this match""")
    matchTy.AddMember prop
```

<span data-ttu-id="e8969-302">Należy pamiętać, że dodawana jest dokumentacja XML do podanej właściwości.</span><span class="sxs-lookup"><span data-stu-id="e8969-302">Again, note that you’re adding XML documentation to the provided property.</span></span> <span data-ttu-id="e8969-303">Należy również zauważyć, że właściwość może zostać odczytana `GetterCode` , jeśli podano funkcję i właściwość może być zapisywana w przypadku `SetterCode` podanej funkcji, więc Właściwość będąca wynikiem jest tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="e8969-303">Also note that a property can be read if a `GetterCode` function is provided, and the property can be written if a `SetterCode` function is provided, so the resulting property is read only.</span></span>

<span data-ttu-id="e8969-304">Teraz można utworzyć metodę wystąpienia, która zwraca wartość tego `Match` typu:</span><span class="sxs-lookup"><span data-stu-id="e8969-304">Now you can create an instance method that returns a value of this `Match` type:</span></span>

```fsharp
let matchMethod =
    ProvidedMethod(
        methodName = "Match",
        parameters = [ProvidedParameter("input", typeof<string>)],
        returnType = matchTy,
        invokeCode = fun args -> <@@ ((%%args.[0]:obj) :?> Regex).Match(%%args.[1]) :> obj @@>)

matchMeth.AddXmlDoc "Searches the specified input string for the first occurrence of this regular expression"

ty.AddMember matchMeth
```

<span data-ttu-id="e8969-305">Ponieważ tworzysz metodę wystąpienia, `args.[0]` reprezentuje `RegexTyped` wystąpienie, na którym wywoływana jest metoda, i `args.[1]` jest argumentem wejściowym.</span><span class="sxs-lookup"><span data-stu-id="e8969-305">Because you are creating an instance method, `args.[0]` represents the `RegexTyped` instance on which the method is being called, and `args.[1]` is the input argument.</span></span>

<span data-ttu-id="e8969-306">Na koniec Podaj konstruktora, aby można było utworzyć wystąpienia podanego typu.</span><span class="sxs-lookup"><span data-stu-id="e8969-306">Finally, provide a constructor so that instances of the provided type can be created.</span></span>

```fsharp
let ctor =
    ProvidedConstructor(
        parameters = [],
        invokeCode = fun args -> <@@ Regex(pattern, options) :> obj @@>)

ctor.AddXmlDoc("Initializes a regular expression instance.")

ty.AddMember ctor
```

<span data-ttu-id="e8969-307">Konstruktor jedynie wymazuje do tworzenia standardowego wystąpienia wyrażenia regularnego programu .NET, które jest ponownie opakowane do obiektu, ponieważ `obj` jest wymazywany z podanego typu.</span><span class="sxs-lookup"><span data-stu-id="e8969-307">The constructor merely erases to the creation of a standard .NET Regex instance, which is again boxed to an object because `obj` is the erasure of the provided type.</span></span> <span data-ttu-id="e8969-308">Po tej zmianie użycie przykładowego interfejsu API, który określono wcześniej w temacie, działa zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="e8969-308">With that change, the sample API usage that specified earlier in the topic works as expected.</span></span> <span data-ttu-id="e8969-309">Następujący kod jest kompletny i końcowy:</span><span class="sxs-lookup"><span data-stu-id="e8969-309">The following code is complete and final:</span></span>

```fsharp
namespace Samples.FSharp.RegexTypeProvider

open System.Reflection
open Microsoft.FSharp.Core.CompilerServices
open Samples.FSharp.ProvidedTypes
open System.Text.RegularExpressions

[<TypeProvider>]
type public CheckedRegexProvider() as this =
    inherit TypeProviderForNamespaces()

    // Get the assembly and namespace used to house the provided types.
    let thisAssembly = Assembly.GetExecutingAssembly()
    let rootNamespace = "Samples.FSharp.RegexTypeProvider"
    let baseTy = typeof<obj>
    let staticParams = [ProvidedStaticParameter("pattern", typeof<string>)]

    let regexTy = ProvidedTypeDefinition(thisAssembly, rootNamespace, "RegexTyped", Some baseTy)

    do regexTy.DefineStaticParameters(
        parameters=staticParams,
        instantiationFunction=(fun typeName parameterValues ->

            match parameterValues with
            | [| :? string as pattern|] ->

                // Create an instance of the regular expression.

                let r = System.Text.RegularExpressions.Regex(pattern)

                // Declare the typed regex provided type.

                let ty =
                    ProvidedTypeDefinition(
                        thisAssembly,
                        rootNamespace,
                        typeName,
                        baseType = Some baseTy)

                ty.AddXmlDoc "A strongly typed interface to the regular expression '%s'"

                // Provide strongly typed version of Regex.IsMatch static method.
                let isMatch =
                    ProvidedMethod(
                        methodName = "IsMatch",
                        parameters = [ProvidedParameter("input", typeof<string>)],
                        returnType = typeof<bool>,
                        isStatic = true,
                        invokeCode = fun args -> <@@ Regex.IsMatch(%%args.[0], pattern) @@>)

                isMatch.AddXmlDoc "Indicates whether the regular expression finds a match in the specified input string"

                ty.AddMember isMatch

                // Provided type for matches
                // Again, erase to obj even though the representation will always be a Match
                let matchTy =
                    ProvidedTypeDefinition(
                        "MatchType",
                        baseType = Some baseTy,
                        hideObjectMethods = true)

                // Nest the match type within parameterized Regex type.
                ty.AddMember matchTy

                // Add group properties to match type
                for group in r.GetGroupNames() do
                    // Ignore the group named 0, which represents all input.
                    if group <> "0" then
                        let prop =
                          ProvidedProperty(
                            propertyName = group,
                            propertyType = typeof<Group>,
                            getterCode = fun args -> <@@ ((%%args.[0]:obj) :?> Match).Groups.[group] @@>)
                        prop.AddXmlDoc(sprintf @"Gets the ""%s"" group from this match" group)
                        matchTy.AddMember(prop)

                // Provide strongly typed version of Regex.Match instance method.
                let matchMeth =
                  ProvidedMethod(
                    methodName = "Match",
                    parameters = [ProvidedParameter("input", typeof<string>)],
                    returnType = matchTy,
                    invokeCode = fun args -> <@@ ((%%args.[0]:obj) :?> Regex).Match(%%args.[1]) :> obj @@>)
                matchMeth.AddXmlDoc "Searches the specified input string for the first occurrence of this regular expression"

                ty.AddMember matchMeth

                // Declare a constructor.
                let ctor =
                  ProvidedConstructor(
                    parameters = [],
                    invokeCode = fun args -> <@@ Regex(pattern) :> obj @@>)

                // Add documentation to the constructor.
                ctor.AddXmlDoc "Initializes a regular expression instance"

                ty.AddMember ctor

                ty
            | _ -> failwith "unexpected parameter values"))

    do this.AddNamespace(rootNamespace, [regexTy])

[<TypeProviderAssembly>]
do ()
```

### <a name="key-lessons"></a><span data-ttu-id="e8969-310">Najważniejsze lekcje</span><span class="sxs-lookup"><span data-stu-id="e8969-310">Key Lessons</span></span>

<span data-ttu-id="e8969-311">W tej sekcji wyjaśniono, jak utworzyć dostawcę typów, który działa na jego parametry statyczne.</span><span class="sxs-lookup"><span data-stu-id="e8969-311">This section explained how to create a type provider that operates on its static parameters.</span></span> <span data-ttu-id="e8969-312">Dostawca sprawdza parametr statyczny i zapewnia operacje na podstawie jego wartości.</span><span class="sxs-lookup"><span data-stu-id="e8969-312">The provider checks the static parameter and provides operations based on its value.</span></span>

## <a name="a-type-provider-that-is-backed-by-local-data"></a><span data-ttu-id="e8969-313">Dostawca typów, który jest obsługiwany przez dane lokalne</span><span class="sxs-lookup"><span data-stu-id="e8969-313">A Type Provider That Is Backed By Local Data</span></span>

<span data-ttu-id="e8969-314">Często można potrzebować dostawców typów do prezentowania interfejsów API na podstawie nie tylko parametrów statycznych, ale również informacji z systemów lokalnych lub zdalnych.</span><span class="sxs-lookup"><span data-stu-id="e8969-314">Frequently you might want type providers to present APIs based on not only static parameters but also information from local or remote systems.</span></span> <span data-ttu-id="e8969-315">W tej sekcji omówiono dostawców typów, które są oparte na danych lokalnych, takich jak lokalne pliki danych.</span><span class="sxs-lookup"><span data-stu-id="e8969-315">This section discusses type providers that are based on local data, such as local data files.</span></span>

### <a name="simple-csv-file-provider"></a><span data-ttu-id="e8969-316">Prosty dostawca plików CSV</span><span class="sxs-lookup"><span data-stu-id="e8969-316">Simple CSV File Provider</span></span>

<span data-ttu-id="e8969-317">Jako prosty przykład rozważmy dostawcę typów do uzyskiwania dostępu do danych naukowych w formacie wartości rozdzielanych przecinkami (CSV).</span><span class="sxs-lookup"><span data-stu-id="e8969-317">As a simple example, consider a type provider for accessing scientific data in Comma Separated Value (CSV) format.</span></span> <span data-ttu-id="e8969-318">W tej sekcji założono, że pliki CSV zawierają wiersz nagłówka, po którym następuje zmiennoprzecinkowe dane, jak przedstawiono w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="e8969-318">This section assumes that the CSV files contain a header row followed by floating point data, as the following table illustrates:</span></span>

|<span data-ttu-id="e8969-319">Odległość (miernik)</span><span class="sxs-lookup"><span data-stu-id="e8969-319">Distance (meter)</span></span>|<span data-ttu-id="e8969-320">Czas (s)</span><span class="sxs-lookup"><span data-stu-id="e8969-320">Time (second)</span></span>|
|----------------|-------------|
|<span data-ttu-id="e8969-321">50,0</span><span class="sxs-lookup"><span data-stu-id="e8969-321">50.0</span></span>|<span data-ttu-id="e8969-322">3.7</span><span class="sxs-lookup"><span data-stu-id="e8969-322">3.7</span></span>|
|<span data-ttu-id="e8969-323">100,0</span><span class="sxs-lookup"><span data-stu-id="e8969-323">100.0</span></span>|<span data-ttu-id="e8969-324">5.2</span><span class="sxs-lookup"><span data-stu-id="e8969-324">5.2</span></span>|
|<span data-ttu-id="e8969-325">150,0</span><span class="sxs-lookup"><span data-stu-id="e8969-325">150.0</span></span>|<span data-ttu-id="e8969-326">6.4</span><span class="sxs-lookup"><span data-stu-id="e8969-326">6.4</span></span>|

<span data-ttu-id="e8969-327">W tej sekcji przedstawiono sposób dostarczania typu, którego można użyć do uzyskania wierszy z `Distance` właściwością typu `float<meter>` i `Time` właściwością typu `float<second>` .</span><span class="sxs-lookup"><span data-stu-id="e8969-327">This section shows how to provide a type that you can use to get rows with a `Distance` property of type `float<meter>` and a `Time` property of type `float<second>`.</span></span> <span data-ttu-id="e8969-328">Dla uproszczenia wykonywane są następujące założenia:</span><span class="sxs-lookup"><span data-stu-id="e8969-328">For simplicity, the following assumptions are made:</span></span>

- <span data-ttu-id="e8969-329">Nazwa nagłówka jest mniejsza od jednostki lub ma postać "Name (Unit)" i nie może zawierać przecinków.</span><span class="sxs-lookup"><span data-stu-id="e8969-329">Header names are either unit-less or have the form "Name (unit)" and don't contain commas.</span></span>

- <span data-ttu-id="e8969-330">Jednostki to wszystkie jednostki międzynarodowe (SI) systemu, które są zdefiniowane w module [FSharp. Data. UnitSystems. si. UnitNames module (F #)](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-data-unitsystems-si-unitnames.html) .</span><span class="sxs-lookup"><span data-stu-id="e8969-330">Units are all System International (SI) units as the [FSharp.Data.UnitSystems.SI.UnitNames Module (F#)](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-data-unitsystems-si-unitnames.html) module defines.</span></span>

- <span data-ttu-id="e8969-331">Jednostki są proste (na przykład miernik), a nie złożone (na przykład licznik licznika/sekundę).</span><span class="sxs-lookup"><span data-stu-id="e8969-331">Units are all simple (for example, meter) rather than compound (for example, meter/second).</span></span>

- <span data-ttu-id="e8969-332">Wszystkie kolumny zawierają dane zmiennoprzecinkowe.</span><span class="sxs-lookup"><span data-stu-id="e8969-332">All columns contain floating point data.</span></span>

<span data-ttu-id="e8969-333">Bardziej kompletny dostawca spowodowałaby ograniczenie tych ograniczeń.</span><span class="sxs-lookup"><span data-stu-id="e8969-333">A more complete provider would loosen these restrictions.</span></span>

<span data-ttu-id="e8969-334">Najpierw należy rozważyć, jak powinien wyglądać interfejs API.</span><span class="sxs-lookup"><span data-stu-id="e8969-334">Again the first step is to consider how the API should look.</span></span> <span data-ttu-id="e8969-335">Mając `info.csv` plik z zawartością poprzedniej tabeli (w formacie rozdzielanym przecinkami), użytkownicy dostawcy powinni mieć możliwość pisania kodu podobnego do następującego przykładu:</span><span class="sxs-lookup"><span data-stu-id="e8969-335">Given an `info.csv` file with the contents from the previous table (in comma-separated format), users of the provider should be able to write code that resembles the following example:</span></span>

```fsharp
let info = new MiniCsv<"info.csv">()
for row in info.Data do
let time = row.Time
printfn $"{float time}"
```

<span data-ttu-id="e8969-336">W takim przypadku kompilator powinien przekonwertować te wywołania na podobne do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="e8969-336">In this case, the compiler should convert these calls into something like the following example:</span></span>

```fsharp
let info = new CsvFile("info.csv")
for row in info.Data do
let (time:float) = row.[1]
printfn $"%f{float time}"
```

<span data-ttu-id="e8969-337">Optymalne tłumaczenie wymaga dostawcy typów w celu zdefiniowania rzeczywistego `CsvFile` typu w zestawie dostawcy typów.</span><span class="sxs-lookup"><span data-stu-id="e8969-337">The optimal translation will require the type provider to define a real `CsvFile` type in the type provider's assembly.</span></span> <span data-ttu-id="e8969-338">Dostawcy typów często polegają na kilku typach pomocników i metodach zawijania ważnych logiki.</span><span class="sxs-lookup"><span data-stu-id="e8969-338">Type providers often rely on a few helper types and methods to wrap important logic.</span></span> <span data-ttu-id="e8969-339">Ponieważ miary są wymazywane w czasie wykonywania, można użyć `float[]` jako typu wymazania dla wiersza.</span><span class="sxs-lookup"><span data-stu-id="e8969-339">Because measures are erased at runtime, you can use a `float[]` as the erased type for a row.</span></span> <span data-ttu-id="e8969-340">Kompilator będzie traktować różne kolumny jako mające różne typy miar.</span><span class="sxs-lookup"><span data-stu-id="e8969-340">The compiler will treat different columns as having different measure types.</span></span> <span data-ttu-id="e8969-341">Na przykład pierwsza kolumna w naszym przykładzie ma typ `float<meter>` , a drugi ma wartość `float<second>` .</span><span class="sxs-lookup"><span data-stu-id="e8969-341">For example, the first column in our example has type `float<meter>`, and the second has `float<second>`.</span></span> <span data-ttu-id="e8969-342">Wymazywane reprezentacje mogą jednak być bardzo proste.</span><span class="sxs-lookup"><span data-stu-id="e8969-342">However, the erased representation can remain quite simple.</span></span>

<span data-ttu-id="e8969-343">Poniższy kod przedstawia rdzeń implementacji.</span><span class="sxs-lookup"><span data-stu-id="e8969-343">The following code shows the core of the implementation.</span></span>

```fsharp
// Simple type wrapping CSV data
type CsvFile(filename) =
    // Cache the sequence of all data lines (all lines but the first)
    let data =
        seq {
            for line in File.ReadAllLines(filename) |> Seq.skip 1 ->
                line.Split(',') |> Array.map float
        }
        |> Seq.cache
    member _.Data = data

[<TypeProvider>]
type public MiniCsvProvider(cfg:TypeProviderConfig) as this =
    inherit TypeProviderForNamespaces(cfg)

    // Get the assembly and namespace used to house the provided types.
    let asm = System.Reflection.Assembly.GetExecutingAssembly()
    let ns = "Samples.FSharp.MiniCsvProvider"

    // Create the main provided type.
    let csvTy = ProvidedTypeDefinition(asm, ns, "MiniCsv", Some(typeof<obj>))

    // Parameterize the type by the file to use as a template.
    let filename = ProvidedStaticParameter("filename", typeof<string>)
    do csvTy.DefineStaticParameters([filename], fun tyName [| :? string as filename |] ->

        // Resolve the filename relative to the resolution folder.
        let resolvedFilename = Path.Combine(cfg.ResolutionFolder, filename)

        // Get the first line from the file.
        let headerLine = File.ReadLines(resolvedFilename) |> Seq.head

        // Define a provided type for each row, erasing to a float[].
        let rowTy = ProvidedTypeDefinition("Row", Some(typeof<float[]>))

        // Extract header names from the file, splitting on commas.
        // use Regex matching to get the position in the row at which the field occurs
        let headers = Regex.Matches(headerLine, "[^,]+")

        // Add one property per CSV field.
        for i in 0 .. headers.Count - 1 do
            let headerText = headers.[i].Value

            // Try to decompose this header into a name and unit.
            let fieldName, fieldTy =
                let m = Regex.Match(headerText, @"(?<field>.+) \((?<unit>.+)\)")
                if m.Success then

                    let unitName = m.Groups.["unit"].Value
                    let units = ProvidedMeasureBuilder.Default.SI unitName
                    m.Groups.["field"].Value, ProvidedMeasureBuilder.Default.AnnotateType(typeof<float>,[units])

                else
                    // no units, just treat it as a normal float
                    headerText, typeof<float>

            let prop =
                ProvidedProperty(fieldName, fieldTy,
                    getterCode = fun [row] -> <@@ (%%row:float[]).[i] @@>)

            // Add metadata that defines the property's location in the referenced file.
            prop.AddDefinitionLocation(1, headers.[i].Index + 1, filename)
            rowTy.AddMember(prop)

        // Define the provided type, erasing to CsvFile.
        let ty = ProvidedTypeDefinition(asm, ns, tyName, Some(typeof<CsvFile>))

        // Add a parameterless constructor that loads the file that was used to define the schema.
        let ctor0 =
            ProvidedConstructor([],
                invokeCode = fun [] -> <@@ CsvFile(resolvedFilename) @@>)
        ty.AddMember ctor0

        // Add a constructor that takes the file name to load.
        let ctor1 = ProvidedConstructor([ProvidedParameter("filename", typeof<string>)],
            invokeCode = fun [filename] -> <@@ CsvFile(%%filename) @@>)
        ty.AddMember ctor1

        // Add a more strongly typed Data property, which uses the existing property at runtime.
        let prop =
            ProvidedProperty("Data", typedefof<seq<_>>.MakeGenericType(rowTy),
                getterCode = fun [csvFile] -> <@@ (%%csvFile:CsvFile).Data @@>)
        ty.AddMember prop

        // Add the row type as a nested type.
        ty.AddMember rowTy
        ty)

    // Add the type to the namespace.
    do this.AddNamespace(ns, [csvTy])
```

<span data-ttu-id="e8969-344">Należy zwrócić uwagę na następujące kwestie dotyczące implementacji:</span><span class="sxs-lookup"><span data-stu-id="e8969-344">Note the following points about the implementation:</span></span>

- <span data-ttu-id="e8969-345">Przeciążone konstruktory umożliwiają odczytywanie oryginalnego pliku lub jednego, który ma identyczny schemat.</span><span class="sxs-lookup"><span data-stu-id="e8969-345">Overloaded constructors allow either the original file or one that has an identical schema to be read.</span></span> <span data-ttu-id="e8969-346">Ten wzorzec jest typowy podczas pisania dostawcy typów dla lokalnych lub zdalnych źródeł danych, a ten wzorzec umożliwia użycie lokalnego pliku jako szablonu dla danych zdalnych.</span><span class="sxs-lookup"><span data-stu-id="e8969-346">This pattern is common when you write a type provider for local or remote data sources, and this pattern allows a local file to be used as the template for remote data.</span></span>

- <span data-ttu-id="e8969-347">Do rozpoznawania względnych nazw plików można użyć wartości [TypeProviderConfig](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-compilerservices-typeproviderconfig.html) , która została przeniesiona do konstruktora dostawcy typów.</span><span class="sxs-lookup"><span data-stu-id="e8969-347">You can use the [TypeProviderConfig](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-compilerservices-typeproviderconfig.html) value that’s passed in to the type provider constructor to resolve relative file names.</span></span>

- <span data-ttu-id="e8969-348">Możesz użyć metody, `AddDefinitionLocation` Aby zdefiniować lokalizację podanych właściwości.</span><span class="sxs-lookup"><span data-stu-id="e8969-348">You can use the `AddDefinitionLocation` method to define the location of the provided properties.</span></span> <span data-ttu-id="e8969-349">W związku z tym, jeśli używasz `Go To Definition` na podanej właściwości, plik CSV zostanie otwarty w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e8969-349">Therefore, if you use `Go To Definition` on a provided property, the CSV file will open in Visual Studio.</span></span>

- <span data-ttu-id="e8969-350">Możesz użyć typu, `ProvidedMeasureBuilder` Aby wyszukać jednostki si i wygenerować odpowiednie `float<_>` typy.</span><span class="sxs-lookup"><span data-stu-id="e8969-350">You can use the `ProvidedMeasureBuilder` type to look up the SI units and to generate the relevant `float<_>` types.</span></span>

### <a name="key-lessons"></a><span data-ttu-id="e8969-351">Najważniejsze lekcje</span><span class="sxs-lookup"><span data-stu-id="e8969-351">Key Lessons</span></span>

<span data-ttu-id="e8969-352">W tej sekcji wyjaśniono, jak utworzyć dostawcę typów dla lokalnego źródła danych z prostym schematem zawartym w samym źródle danych.</span><span class="sxs-lookup"><span data-stu-id="e8969-352">This section explained how to create a type provider for a local data source with a simple schema that's contained in the data source itself.</span></span>

## <a name="going-further"></a><span data-ttu-id="e8969-353">Dalsze przechodzenie</span><span class="sxs-lookup"><span data-stu-id="e8969-353">Going Further</span></span>

<span data-ttu-id="e8969-354">Poniższe sekcje zawierają sugestie dotyczące dalszych badań.</span><span class="sxs-lookup"><span data-stu-id="e8969-354">The following sections include suggestions for further study.</span></span>

### <a name="a-look-at-the-compiled-code-for-erased-types"></a><span data-ttu-id="e8969-355">Przyjrzyj się skompilowanemu kodowi dla wymazanych typów</span><span class="sxs-lookup"><span data-stu-id="e8969-355">A Look at the Compiled Code for Erased Types</span></span>

<span data-ttu-id="e8969-356">Aby określić, jak użycie dostawcy typów odnosi się do kodu, który jest emitowany, należy poszukać następującej funkcji przy użyciu `HelloWorldTypeProvider` użytej wcześniej w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="e8969-356">To give you some idea of how the use of the type provider corresponds to the code that's emitted, look at the following function by using the `HelloWorldTypeProvider` that's used earlier in this topic.</span></span>

```fsharp
let function1 () =
    let obj1 = Samples.HelloWorldTypeProvider.Type1("some data")
    obj1.InstanceProperty
```

<span data-ttu-id="e8969-357">Poniżej znajduje się obraz kodu pochodzącego z dekompilowanego przy użyciu ildasm.exe:</span><span class="sxs-lookup"><span data-stu-id="e8969-357">Here’s an image of the resulting code decompiled by using ildasm.exe:</span></span>

```il
.class public abstract auto ansi sealed Module1
extends [mscorlib]System.Object
{
.custom instance void [FSharp.Core]Microsoft.FSharp.Core.CompilationMappingAtt
ribute::.ctor(valuetype [FSharp.Core]Microsoft.FSharp.Core.SourceConstructFlags)
= ( 01 00 07 00 00 00 00 00 )
.method public static int32  function1() cil managed
{
// Code size       24 (0x18)
.maxstack  3
.locals init ([0] object obj1)
IL_0000:  nop
IL_0001:  ldstr      "some data"
IL_0006:  unbox.any  [mscorlib]System.Object
IL_000b:  stloc.0
IL_000c:  ldloc.0
IL_000d:  call       !!0 [FSharp.Core_2]Microsoft.FSharp.Core.LanguagePrimit
ives/IntrinsicFunctions::UnboxGeneric<string>(object)
IL_0012:  callvirt   instance int32 [mscorlib_3]System.String::get_Length()
IL_0017:  ret
} // end of method Module1::function1

} // end of class Module1
```

<span data-ttu-id="e8969-358">Jak pokazano w przykładzie, wszystkie wzmianki o typie `Type1` i właściwości zostały `InstanceProperty` wymazane, pozostawiając tylko operacje na typach środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="e8969-358">As the example shows, all mentions of the type `Type1` and the `InstanceProperty` property have been erased, leaving only operations on the runtime types involved.</span></span>

### <a name="design-and-naming-conventions-for-type-providers"></a><span data-ttu-id="e8969-359">Projektowanie i nazewnictwo Konwencji dla dostawców typów</span><span class="sxs-lookup"><span data-stu-id="e8969-359">Design and Naming Conventions for Type Providers</span></span>

<span data-ttu-id="e8969-360">Podczas tworzenia dostawców typów należy przestrzegać następujących konwencji.</span><span class="sxs-lookup"><span data-stu-id="e8969-360">Observe the following conventions when authoring type providers.</span></span>

<span data-ttu-id="e8969-361">**Dostawcy dla protokołów łączności** Ogólnie rzecz biorąc nazwy większości bibliotek DLL dostawcy dla protokołów łączności danych i usług, takich jak połączenia OData lub SQL, powinny kończyć się na `TypeProvider` lub `TypeProviders` .</span><span class="sxs-lookup"><span data-stu-id="e8969-361">**Providers for Connectivity Protocols** In general, names of most provider DLLs for data and service connectivity protocols, such as OData or SQL connections, should end in `TypeProvider` or `TypeProviders`.</span></span> <span data-ttu-id="e8969-362">Na przykład użyj nazwy biblioteki DLL, która jest podobna do następującego ciągu:</span><span class="sxs-lookup"><span data-stu-id="e8969-362">For example, use a DLL name that resembles the following string:</span></span>

`Fabrikam.Management.BasicTypeProviders.dll`

<span data-ttu-id="e8969-363">Upewnij się, że podane typy są członkami odpowiadającej przestrzeni nazw, i wskaż wdrożony protokół łączności:</span><span class="sxs-lookup"><span data-stu-id="e8969-363">Ensure that your provided types are members of the corresponding namespace, and indicate the connectivity protocol that you implemented:</span></span>

```fsharp
  Fabrikam.Management.BasicTypeProviders.WmiConnection<…>
  Fabrikam.Management.BasicTypeProviders.DataProtocolConnection<…>
```

<span data-ttu-id="e8969-364">**Dostawcy narzędzi do ogólnego kodowania**.</span><span class="sxs-lookup"><span data-stu-id="e8969-364">**Utility Providers for General Coding**.</span></span>  <span data-ttu-id="e8969-365">Dla dostawcy typów narzędzi, takich jak dla wyrażeń regularnych, dostawca typów może być częścią biblioteki podstawowej, jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="e8969-365">For a utility type provider such as that for regular expressions, the type provider may be part of a base library, as the following example shows:</span></span>

```fsharp
#r "Fabrikam.Core.Text.Utilities.dll"
```

<span data-ttu-id="e8969-366">W takim przypadku dostarczony typ pojawi się w odpowiednim punkcie zgodnie z normalnymi konwencjami projektowania platformy .NET:</span><span class="sxs-lookup"><span data-stu-id="e8969-366">In this case, the provided type would appear at an appropriate point according to normal .NET design conventions:</span></span>

```fsharp
  open Fabrikam.Core.Text.RegexTyped

  let regex = new RegexTyped<"a+b+a+b+">()
```

<span data-ttu-id="e8969-367">**Pojedyncze źródła danych**.</span><span class="sxs-lookup"><span data-stu-id="e8969-367">**Singleton Data Sources**.</span></span> <span data-ttu-id="e8969-368">Niektórzy dostawcy typów nawiązują połączenie z pojedynczym dedykowanym źródłem danych i zapewniają tylko dane.</span><span class="sxs-lookup"><span data-stu-id="e8969-368">Some type providers connect to a single dedicated data source and provide only data.</span></span> <span data-ttu-id="e8969-369">W takim przypadku należy porzucić `TypeProvider` sufiks i używać zwykłych Konwencji do nadawania nazw .NET:</span><span class="sxs-lookup"><span data-stu-id="e8969-369">In this case, you should drop the `TypeProvider` suffix and use normal conventions for .NET naming:</span></span>

```fsharp
#r "Fabrikam.Data.Freebase.dll"

let data = Fabrikam.Data.Freebase.Astronomy.Asteroids
```

<span data-ttu-id="e8969-370">Aby uzyskać więcej informacji, zobacz `GetConnection` konwencje projektowe opisane w dalszej części tego tematu.</span><span class="sxs-lookup"><span data-stu-id="e8969-370">For more information, see the `GetConnection` design convention that's described later in this topic.</span></span>

### <a name="design-patterns-for-type-providers"></a><span data-ttu-id="e8969-371">Wzorce projektowe dla dostawców typów</span><span class="sxs-lookup"><span data-stu-id="e8969-371">Design Patterns for Type Providers</span></span>

<span data-ttu-id="e8969-372">W poniższych sekcjach opisano wzorce projektowe, których można użyć podczas tworzenia dostawców typów.</span><span class="sxs-lookup"><span data-stu-id="e8969-372">The following sections describe design patterns you can use when authoring type providers.</span></span>

#### <a name="the-getconnection-design-pattern"></a><span data-ttu-id="e8969-373">Wzorzec projektu GetConnect</span><span class="sxs-lookup"><span data-stu-id="e8969-373">The GetConnection Design Pattern</span></span>

<span data-ttu-id="e8969-374">Większość dostawców typów należy napisać, aby używać `GetConnection` wzorca, który jest używany przez dostawców typów w FSharp.Data.TypeProviders.dll, jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="e8969-374">Most type providers should be written to use the `GetConnection` pattern that's used by the type providers in FSharp.Data.TypeProviders.dll, as the following example shows:</span></span>

```fsharp
#r "Fabrikam.Data.WebDataStore.dll"

type Service = Fabrikam.Data.WebDataStore<…static connection parameters…>

let connection = Service.GetConnection(…dynamic connection parameters…)

let data = connection.Astronomy.Asteroids
```

#### <a name="type-providers-backed-by-remote-data-and-services"></a><span data-ttu-id="e8969-375">Dostawcy typów z danymi zdalnymi i usługami</span><span class="sxs-lookup"><span data-stu-id="e8969-375">Type Providers Backed By Remote Data and Services</span></span>

<span data-ttu-id="e8969-376">Przed utworzeniem dostawcy typów, który jest obsługiwany przez zdalne dane i usługi, należy wziąć pod uwagę różne problemy związane z programowaniem.</span><span class="sxs-lookup"><span data-stu-id="e8969-376">Before you create a type provider that's backed by remote data and services, you must consider a range of issues that are inherent in connected programming.</span></span> <span data-ttu-id="e8969-377">Te problemy obejmują następujące zagadnienia:</span><span class="sxs-lookup"><span data-stu-id="e8969-377">These issues include the following considerations:</span></span>

- <span data-ttu-id="e8969-378">mapowanie schematu</span><span class="sxs-lookup"><span data-stu-id="e8969-378">schema mapping</span></span>

- <span data-ttu-id="e8969-379">dynamiczność i unieważnienie w obecności zmiany schematu</span><span class="sxs-lookup"><span data-stu-id="e8969-379">liveness and invalidation in the presence of schema change</span></span>

- <span data-ttu-id="e8969-380">buforowanie schematu</span><span class="sxs-lookup"><span data-stu-id="e8969-380">schema caching</span></span>

- <span data-ttu-id="e8969-381">asynchroniczne implementacje operacji dostępu do danych</span><span class="sxs-lookup"><span data-stu-id="e8969-381">asynchronous implementations of data access operations</span></span>

- <span data-ttu-id="e8969-382">Obsługa zapytań, w tym zapytań LINQ</span><span class="sxs-lookup"><span data-stu-id="e8969-382">supporting queries, including LINQ queries</span></span>

- <span data-ttu-id="e8969-383">poświadczenia i uwierzytelnianie</span><span class="sxs-lookup"><span data-stu-id="e8969-383">credentials and authentication</span></span>

<span data-ttu-id="e8969-384">Ten temat nie omawia problemów w dalszej części tego tematu.</span><span class="sxs-lookup"><span data-stu-id="e8969-384">This topic doesn't explore these issues further.</span></span>

### <a name="additional-authoring-techniques"></a><span data-ttu-id="e8969-385">Dodatkowe techniki tworzenia</span><span class="sxs-lookup"><span data-stu-id="e8969-385">Additional Authoring Techniques</span></span>

<span data-ttu-id="e8969-386">Podczas pisania własnych dostawców typów warto skorzystać z następujących dodatkowych technik.</span><span class="sxs-lookup"><span data-stu-id="e8969-386">When you write your own type providers, you might want to use the following additional techniques.</span></span>

### <a name="creating-types-and-members-on-demand"></a><span data-ttu-id="e8969-387">Tworzenie typów i członków na żądanie</span><span class="sxs-lookup"><span data-stu-id="e8969-387">Creating Types and Members On-Demand</span></span>

<span data-ttu-id="e8969-388">Dostarczony interfejs APItype ma opóźnione wersje elementu AddMember.</span><span class="sxs-lookup"><span data-stu-id="e8969-388">The ProvidedType API has delayed versions of AddMember.</span></span>

```fsharp
  type ProvidedType =
      member AddMemberDelayed  : (unit -> MemberInfo)      -> unit
      member AddMembersDelayed : (unit -> MemberInfo list) -> unit
```

<span data-ttu-id="e8969-389">Te wersje są używane do tworzenia przestrzeni na żądanie typów.</span><span class="sxs-lookup"><span data-stu-id="e8969-389">These versions are used to create on-demand spaces of types.</span></span>

### <a name="providing-array-types-and-generic-type-instantiations"></a><span data-ttu-id="e8969-390">Dostarczanie typów tablicowych i wystąpień typów ogólnych</span><span class="sxs-lookup"><span data-stu-id="e8969-390">Providing Array types and Generic Type Instantiations</span></span>

<span data-ttu-id="e8969-391">Udostępniane elementy członkowskie (których sygnatury zawierają typy tablic, typy ByRef i wystąpienia typów ogólnych), używając zwykłych `MakeArrayType` , `MakePointerType` i `MakeGenericType` z dowolnego wystąpienia <xref:System.Type> , w tym `ProvidedTypeDefinitions` .</span><span class="sxs-lookup"><span data-stu-id="e8969-391">You make provided members (whose signatures include array types, byref types, and instantiations of generic types) by using the normal `MakeArrayType`, `MakePointerType`, and `MakeGenericType` on any instance of <xref:System.Type>, including `ProvidedTypeDefinitions`.</span></span>

> [!NOTE]
> <span data-ttu-id="e8969-392">W niektórych przypadkach może być konieczne użycie pomocnika w programie `ProvidedTypeBuilder.MakeGenericType` .</span><span class="sxs-lookup"><span data-stu-id="e8969-392">In some cases you may have to use the helper in `ProvidedTypeBuilder.MakeGenericType`.</span></span>  <span data-ttu-id="e8969-393">Aby uzyskać więcej informacji, zobacz [dokumentację zestawu SDK dostawcy typów](https://github.com/fsprojects/FSharp.TypeProviders.SDK/blob/master/README.md#explicit-construction-of-code-makegenerictype-makegenericmethod-and-uncheckedquotations) .</span><span class="sxs-lookup"><span data-stu-id="e8969-393">See the [Type Provider SDK documentation](https://github.com/fsprojects/FSharp.TypeProviders.SDK/blob/master/README.md#explicit-construction-of-code-makegenerictype-makegenericmethod-and-uncheckedquotations) for more details.</span></span>

### <a name="providing-unit-of-measure-annotations"></a><span data-ttu-id="e8969-394">Dostarczanie adnotacji jednostki miary</span><span class="sxs-lookup"><span data-stu-id="e8969-394">Providing Unit of Measure Annotations</span></span>

<span data-ttu-id="e8969-395">Interfejs API ProvidedTypes zapewnia pomocników do zapewniania adnotacji miar.</span><span class="sxs-lookup"><span data-stu-id="e8969-395">The ProvidedTypes API provides helpers for providing measure annotations.</span></span> <span data-ttu-id="e8969-396">Na przykład, aby podać typ `float<kg>` , należy użyć następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="e8969-396">For example, to provide the type `float<kg>`, use the following code:</span></span>

```fsharp
  let measures = ProvidedMeasureBuilder.Default
  let kg = measures.SI "kilogram"
  let m = measures.SI "meter"
  let float_kg = measures.AnnotateType(typeof<float>,[kg])
```

  <span data-ttu-id="e8969-397">Aby podać typ `Nullable<decimal<kg/m^2>>` , użyj następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="e8969-397">To provide the type `Nullable<decimal<kg/m^2>>`, use the following code:</span></span>

```fsharp
  let kgpm2 = measures.Ratio(kg, measures.Square m)
  let dkgpm2 = measures.AnnotateType(typeof<decimal>,[kgpm2])
  let nullableDecimal_kgpm2 = typedefof<System.Nullable<_>>.MakeGenericType [|dkgpm2 |]
```

### <a name="accessing-project-local-or-script-local-resources"></a><span data-ttu-id="e8969-398">Uzyskiwanie dostępu do zasobów Project-Local lub Script-Local</span><span class="sxs-lookup"><span data-stu-id="e8969-398">Accessing Project-Local or Script-Local Resources</span></span>

<span data-ttu-id="e8969-399">Podczas konstruowania każde wystąpienie dostawcy typów może mieć określoną `TypeProviderConfig` wartość.</span><span class="sxs-lookup"><span data-stu-id="e8969-399">Each instance of a type provider can be given a `TypeProviderConfig` value during construction.</span></span> <span data-ttu-id="e8969-400">Ta wartość zawiera "folder rozpoznawania" dla dostawcy (czyli folder projektu dla kompilacji lub katalog zawierający skrypt), listę zestawów, do których się odwołuje, i inne informacje.</span><span class="sxs-lookup"><span data-stu-id="e8969-400">This value contains the "resolution folder" for the provider (that is, the project folder for the compilation or the directory that contains a script), the list of referenced assemblies, and other information.</span></span>

### <a name="invalidation"></a><span data-ttu-id="e8969-401">Unieważniania</span><span class="sxs-lookup"><span data-stu-id="e8969-401">Invalidation</span></span>

<span data-ttu-id="e8969-402">Dostawcy mogą zgłaszać sygnały unieważnienia, aby powiadomić usługę języka F # o zmianach założeń schematu.</span><span class="sxs-lookup"><span data-stu-id="e8969-402">Providers can raise invalidation signals to notify the F# language service that the schema assumptions may have changed.</span></span> <span data-ttu-id="e8969-403">Po wystąpieniu unieważnienia typecheck jest wykonywane w przypadku, gdy dostawca jest hostowany w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e8969-403">When invalidation occurs, a typecheck is redone if the provider is being hosted in Visual Studio.</span></span> <span data-ttu-id="e8969-404">Ten sygnał zostanie zignorowany, gdy dostawca jest hostowany w F# Interactive lub przez kompilator F # (fsc.exe).</span><span class="sxs-lookup"><span data-stu-id="e8969-404">This signal will be ignored when the provider is hosted in F# Interactive or by the F# Compiler (fsc.exe).</span></span>

### <a name="caching-schema-information"></a><span data-ttu-id="e8969-405">Buforowanie informacji o schemacie</span><span class="sxs-lookup"><span data-stu-id="e8969-405">Caching Schema Information</span></span>

<span data-ttu-id="e8969-406">Dostawcy muszą często buforować dostęp do informacji o schemacie.</span><span class="sxs-lookup"><span data-stu-id="e8969-406">Providers must often cache access to schema information.</span></span> <span data-ttu-id="e8969-407">Dane w pamięci podręcznej powinny być przechowywane przy użyciu nazwy pliku, która jest podawana jako parametr statyczny lub jako dane użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e8969-407">The cached data should be stored by using a file name that's given as a static parameter or as user data.</span></span> <span data-ttu-id="e8969-408">Przykładem buforowania schematu jest `LocalSchemaFile` parametr w dostawcach typów w `FSharp.Data.TypeProviders` zestawie.</span><span class="sxs-lookup"><span data-stu-id="e8969-408">An example of schema caching is the `LocalSchemaFile` parameter in the type providers in the `FSharp.Data.TypeProviders` assembly.</span></span> <span data-ttu-id="e8969-409">W implementacji tych dostawców ten parametr statyczny kieruje dostawcę typów do użycia informacji o schemacie w określonym pliku lokalnym zamiast uzyskiwania dostępu do źródła danych za pośrednictwem sieci.</span><span class="sxs-lookup"><span data-stu-id="e8969-409">In the implementation of these providers, this static parameter directs the type provider to use the schema information in the specified local file instead of accessing the data source over the network.</span></span> <span data-ttu-id="e8969-410">Aby użyć informacji o schemacie buforowanym, należy również ustawić parametr statyczny `ForceUpdate` na `false` .</span><span class="sxs-lookup"><span data-stu-id="e8969-410">To use cached schema information, you must also set the static parameter `ForceUpdate` to `false`.</span></span> <span data-ttu-id="e8969-411">Możesz użyć podobnej techniki, aby włączyć dostęp do danych w trybie online i offline.</span><span class="sxs-lookup"><span data-stu-id="e8969-411">You could use a similar technique to enable online and offline data access.</span></span>

### <a name="backing-assembly"></a><span data-ttu-id="e8969-412">Zestaw kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="e8969-412">Backing Assembly</span></span>

<span data-ttu-id="e8969-413">Podczas kompilowania `.dll` pliku lub plik `.exe` kopii zapasowej dll dla generowanych typów jest statycznie połączony z powstałym zestawem.</span><span class="sxs-lookup"><span data-stu-id="e8969-413">When you compile a `.dll` or `.exe` file, the backing .dll file for generated types is statically linked into the resulting assembly.</span></span> <span data-ttu-id="e8969-414">Ten link jest tworzony przez skopiowanie definicji typu języka pośredniego (IL) i wszystkich zasobów zarządzanych z zestawu zapasowego do końcowego zestawu.</span><span class="sxs-lookup"><span data-stu-id="e8969-414">This link is created by copying the Intermediate Language (IL) type definitions and any managed resources from the backing assembly into the final assembly.</span></span> <span data-ttu-id="e8969-415">W przypadku korzystania z F# Interactive plik kopii zapasowej dll nie jest kopiowany i jest ładowany bezpośrednio do procesu F# Interactive.</span><span class="sxs-lookup"><span data-stu-id="e8969-415">When you use F# Interactive, the backing .dll file isn't copied and is instead loaded directly into the F# Interactive process.</span></span>

### <a name="exceptions-and-diagnostics-from-type-providers"></a><span data-ttu-id="e8969-416">Wyjątki i Diagnostyka od dostawców typów</span><span class="sxs-lookup"><span data-stu-id="e8969-416">Exceptions and Diagnostics from Type Providers</span></span>

<span data-ttu-id="e8969-417">Wszystkie zastosowania wszystkich elementów członkowskich z dostarczonych typów mogą generować wyjątki.</span><span class="sxs-lookup"><span data-stu-id="e8969-417">All uses of all members from provided types may throw exceptions.</span></span> <span data-ttu-id="e8969-418">We wszystkich przypadkach, jeśli dostawca typu zgłasza wyjątek, kompilator hosta podzieli błąd na dostawcę określonego typu.</span><span class="sxs-lookup"><span data-stu-id="e8969-418">In all cases, if a type provider throws an exception, the host compiler attributes the error to a specific type provider.</span></span>

- <span data-ttu-id="e8969-419">Wyjątki dostawcy typów nigdy nie powinny powodować wewnętrznych błędów kompilatora.</span><span class="sxs-lookup"><span data-stu-id="e8969-419">Type provider exceptions should never result in internal compiler errors.</span></span>

- <span data-ttu-id="e8969-420">Dostawcy typów nie mogą raportować ostrzeżeń.</span><span class="sxs-lookup"><span data-stu-id="e8969-420">Type providers can't report warnings.</span></span>

- <span data-ttu-id="e8969-421">Gdy dostawca typów jest hostowany w kompilatorze F #, środowisku deweloperskim F # lub F# Interactive, wszystkie wyjątki od tego dostawcy są przechwytywane.</span><span class="sxs-lookup"><span data-stu-id="e8969-421">When a type provider is hosted in the F# compiler, an F# development environment, or F# Interactive, all exceptions from that provider are caught.</span></span> <span data-ttu-id="e8969-422">Właściwość Message jest zawsze tekstem błędu i nie pojawia się ślad stosu.</span><span class="sxs-lookup"><span data-stu-id="e8969-422">The Message property is always the error text, and no stack trace appears.</span></span> <span data-ttu-id="e8969-423">Jeśli zamierzasz zgłosić wyjątek, możesz zgłosić następujące przykłady: `System.NotSupportedException` , `System.IO.IOException` , `System.Exception` .</span><span class="sxs-lookup"><span data-stu-id="e8969-423">If you’re going to throw an exception, you can throw the following examples: `System.NotSupportedException`, `System.IO.IOException`, `System.Exception`.</span></span>

#### <a name="providing-generated-types"></a><span data-ttu-id="e8969-424">Zapewnianie wygenerowanych typów</span><span class="sxs-lookup"><span data-stu-id="e8969-424">Providing Generated Types</span></span>

<span data-ttu-id="e8969-425">Do tej pory ten dokument wyjaśnia, jak zapewnić typy wymazane.</span><span class="sxs-lookup"><span data-stu-id="e8969-425">So far, this document has explained how to provide erased types.</span></span> <span data-ttu-id="e8969-426">Można również użyć mechanizmu dostawcy typów w języku F #, aby udostępnić wygenerowane typy, które są dodawane jako prawdziwe definicje typów .NET do programu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e8969-426">You can also use the type provider mechanism in F# to provide generated types, which are added as real .NET type definitions into the users' program.</span></span> <span data-ttu-id="e8969-427">Należy odwołać się do wygenerowanych typów przy użyciu definicji typu.</span><span class="sxs-lookup"><span data-stu-id="e8969-427">You must refer to generated provided types by using a type definition.</span></span>

```fsharp
open Microsoft.FSharp.TypeProviders

type Service = ODataService<"http://services.odata.org/Northwind/Northwind.svc/">
```

<span data-ttu-id="e8969-428">Kod pomocnika ProvidedTypes-0,2, który jest częścią wersji programu F # 3,0, ma ograniczoną obsługę tylko w celu zapewnienia wygenerowanych typów.</span><span class="sxs-lookup"><span data-stu-id="e8969-428">The ProvidedTypes-0.2 helper code that is part of the F# 3.0 release has only limited support for providing generated types.</span></span> <span data-ttu-id="e8969-429">Następujące instrukcje muszą mieć wartość true w przypadku wygenerowanej definicji typu:</span><span class="sxs-lookup"><span data-stu-id="e8969-429">The following statements must be true for a generated type definition:</span></span>

- <span data-ttu-id="e8969-430">`isErased` musi być ustawiony na `false` .</span><span class="sxs-lookup"><span data-stu-id="e8969-430">`isErased` must be set to `false`.</span></span>

- <span data-ttu-id="e8969-431">Wygenerowany typ należy dodać do nowo skonstruowanego elementu `ProvidedAssembly()` , który reprezentuje kontener dla wygenerowanych fragmentów kodu.</span><span class="sxs-lookup"><span data-stu-id="e8969-431">The generated type must be added to a newly constructed `ProvidedAssembly()`, which represents a container for generated code fragments.</span></span>

- <span data-ttu-id="e8969-432">Dostawca musi mieć zestaw, który ma rzeczywiste kopie zapasowe pliku .NET. dll z pasującym plikiem. dll na dysku.</span><span class="sxs-lookup"><span data-stu-id="e8969-432">The provider must have an assembly that has an actual backing .NET .dll file with a matching .dll file on disk.</span></span>

## <a name="rules-and-limitations"></a><span data-ttu-id="e8969-433">Zasady i ograniczenia</span><span class="sxs-lookup"><span data-stu-id="e8969-433">Rules and Limitations</span></span>

<span data-ttu-id="e8969-434">Podczas pisania dostawców typów należy pamiętać o następujących regułach i ograniczeniach.</span><span class="sxs-lookup"><span data-stu-id="e8969-434">When you write type providers, keep the following rules and limitations in mind.</span></span>

### <a name="provided-types-must-be-reachable"></a><span data-ttu-id="e8969-435">Dostarczone typy muszą być dostępne</span><span class="sxs-lookup"><span data-stu-id="e8969-435">Provided types must be reachable</span></span>

<span data-ttu-id="e8969-436">Wszystkie udostępniane typy powinny być dostępne z typów niezagnieżdżonych.</span><span class="sxs-lookup"><span data-stu-id="e8969-436">All provided types should be reachable from the non-nested types.</span></span> <span data-ttu-id="e8969-437">Typy niezagnieżdżone są podawane w wywołaniu `TypeProviderForNamespaces` konstruktora lub wywołaniu `AddNamespace` .</span><span class="sxs-lookup"><span data-stu-id="e8969-437">The non-nested types are given in the call to the `TypeProviderForNamespaces` constructor or a call to `AddNamespace`.</span></span> <span data-ttu-id="e8969-438">Na przykład, jeśli dostawca udostępnia typ `StaticClass.P : T` , należy się upewnić, że T nie jest typem zagnieżdżonym lub jest zagnieżdżony w jednym z nich.</span><span class="sxs-lookup"><span data-stu-id="e8969-438">For example, if the provider provides a type `StaticClass.P : T`, you must ensure that T is either a non-nested type or nested under one.</span></span>

<span data-ttu-id="e8969-439">Na przykład niektórzy dostawcy mają klasę statyczną, taką jak `DataTypes` , która zawiera te `T1, T2, T3, ...` typy.</span><span class="sxs-lookup"><span data-stu-id="e8969-439">For example, some providers have a static class such as `DataTypes` that contain these `T1, T2, T3, ...` types.</span></span> <span data-ttu-id="e8969-440">W przeciwnym razie błąd wskazuje, że znaleziono odwołanie do typu T w zestawie A, ale nie można odnaleźć typu w tym zestawie.</span><span class="sxs-lookup"><span data-stu-id="e8969-440">Otherwise, the error says that a reference to type T in assembly A was found, but the type couldn't be found in that assembly.</span></span> <span data-ttu-id="e8969-441">Jeśli ten błąd pojawia się, sprawdź, czy wszystkie podtypy są osiągalne z typów dostawcy.</span><span class="sxs-lookup"><span data-stu-id="e8969-441">If this error appears, verify that all your subtypes can be reached from the provider types.</span></span> <span data-ttu-id="e8969-442">Uwaga: te `T1, T2, T3...` typy są określane jako typy *na bieżąco* .</span><span class="sxs-lookup"><span data-stu-id="e8969-442">Note: These `T1, T2, T3...` types are referred to as the *on-the-fly* types.</span></span> <span data-ttu-id="e8969-443">Pamiętaj, aby umieścić je w dostępnej przestrzeni nazw lub typie nadrzędnym.</span><span class="sxs-lookup"><span data-stu-id="e8969-443">Remember to put them in an accessible namespace or a parent type.</span></span>

### <a name="limitations-of-the-type-provider-mechanism"></a><span data-ttu-id="e8969-444">Ograniczenia mechanizmu dostawcy typów</span><span class="sxs-lookup"><span data-stu-id="e8969-444">Limitations of the Type Provider Mechanism</span></span>

<span data-ttu-id="e8969-445">Mechanizm dostawcy typów w F # ma następujące ograniczenia:</span><span class="sxs-lookup"><span data-stu-id="e8969-445">The type provider mechanism in F# has the following limitations:</span></span>

- <span data-ttu-id="e8969-446">Podstawowa infrastruktura dla dostawców typów w języku F # nie obsługuje podanych typów ogólnych ani dostarczonych metod ogólnych.</span><span class="sxs-lookup"><span data-stu-id="e8969-446">The underlying infrastructure for type providers in F# doesn't support provided generic types or provided generic methods.</span></span>

- <span data-ttu-id="e8969-447">Mechanizm nie obsługuje zagnieżdżonych typów z parametrami statycznymi.</span><span class="sxs-lookup"><span data-stu-id="e8969-447">The mechanism doesn't support nested types with static parameters.</span></span>

## <a name="development-tips"></a><span data-ttu-id="e8969-448">Porady dotyczące projektowania</span><span class="sxs-lookup"><span data-stu-id="e8969-448">Development Tips</span></span>

<span data-ttu-id="e8969-449">Podczas procesu tworzenia warto poznać następujące wskazówki:</span><span class="sxs-lookup"><span data-stu-id="e8969-449">You might find the following tips helpful during the development process:</span></span>

### <a name="run-two-instances-of-visual-studio"></a><span data-ttu-id="e8969-450">Uruchom dwa wystąpienia programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e8969-450">Run two instances of Visual Studio</span></span>

<span data-ttu-id="e8969-451">Można opracowywać dostawcę typów w jednym wystąpieniu i testować dostawcę w inny sposób, ponieważ test IDE będzie miał blokadę w pliku dll, który uniemożliwia ponowne skompilowanie dostawcy typów.</span><span class="sxs-lookup"><span data-stu-id="e8969-451">You can develop the type provider in one instance and test the provider in the other because the test IDE will take a lock on the .dll file that prevents the type provider from being rebuilt.</span></span> <span data-ttu-id="e8969-452">W tym celu należy zamknąć drugie wystąpienie programu Visual Studio, gdy dostawca jest skompilowany w pierwszym wystąpieniu, a następnie należy ponownie otworzyć drugie wystąpienie po skompilowaniu dostawcy.</span><span class="sxs-lookup"><span data-stu-id="e8969-452">Thus, you must close the second instance of Visual Studio while the provider is built in the first instance, and then you must reopen the second instance after the provider is built.</span></span>

### <a name="debug-type-providers-by-using-invocations-of-fscexe"></a><span data-ttu-id="e8969-453">Debuguj dostawców typów przy użyciu wywołań fsc.exe</span><span class="sxs-lookup"><span data-stu-id="e8969-453">Debug type providers by using invocations of fsc.exe</span></span>

<span data-ttu-id="e8969-454">Dostawców typów można wywoływać przy użyciu następujących narzędzi:</span><span class="sxs-lookup"><span data-stu-id="e8969-454">You can invoke type providers by using the following tools:</span></span>

- <span data-ttu-id="e8969-455">fsc.exe (kompilator wiersza polecenia F #)</span><span class="sxs-lookup"><span data-stu-id="e8969-455">fsc.exe (The F# command line compiler)</span></span>

- <span data-ttu-id="e8969-456">fsi.exe (kompilator F# Interactive)</span><span class="sxs-lookup"><span data-stu-id="e8969-456">fsi.exe (The F# Interactive compiler)</span></span>

- <span data-ttu-id="e8969-457">devenv.exe (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="e8969-457">devenv.exe (Visual Studio)</span></span>

<span data-ttu-id="e8969-458">Można często debugować dostawców typów, używając fsc.exe w pliku skryptu testowego (na przykład Script. FSX).</span><span class="sxs-lookup"><span data-stu-id="e8969-458">You can often debug type providers most easily by using fsc.exe on a test script file (for example, script.fsx).</span></span> <span data-ttu-id="e8969-459">Debuger można uruchomić z poziomu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="e8969-459">You can launch a debugger from a command prompt.</span></span>

```console
devenv /debugexe fsc.exe script.fsx
```

  <span data-ttu-id="e8969-460">Możesz użyć rejestrowania do-stdout.</span><span class="sxs-lookup"><span data-stu-id="e8969-460">You can use print-to-stdout logging.</span></span>

## <a name="see-also"></a><span data-ttu-id="e8969-461">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="e8969-461">See also</span></span>

- [<span data-ttu-id="e8969-462">Dostawcy typów</span><span class="sxs-lookup"><span data-stu-id="e8969-462">Type Providers</span></span>](index.md)
- [<span data-ttu-id="e8969-463">Zestaw SDK dostawcy typów</span><span class="sxs-lookup"><span data-stu-id="e8969-463">The Type Provider SDK</span></span>](https://github.com/fsprojects/FSharp.TypeProviders.SDK)
