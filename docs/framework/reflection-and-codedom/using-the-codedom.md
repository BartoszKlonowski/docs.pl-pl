---
title: Używanie modelu CodeDOM
description: Użyj Code Document Object Model (CodeDOM), który dostarcza typy reprezentujące wiele wspólnych typów elementów kodu źródłowego, aby utworzyć Graf obiektu.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- code compilers
- Code Document Object Model
- Code Document Object Model, graphs
- types, CodeDOM
- namespaces [.NET Framework], CodeDOM
- templated code generation
- dynamically representing source code
- source code models
- CodeDOM
- graphing with CodeDOM
- dynamic compilation
- code generators
- CodeDOM, graphs
ms.assetid: 0444ddf3-c3f6-44ed-a999-f710d9c3e0cf
ms.openlocfilehash: 7a730a828488fd3ca04419588b3f32703dfda1c9
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90541737"
---
# <a name="using-the-codedom"></a><span data-ttu-id="b2c6a-103">Używanie modelu CodeDOM</span><span class="sxs-lookup"><span data-stu-id="b2c6a-103">Using the CodeDOM</span></span>
<span data-ttu-id="b2c6a-104">CodeDOM zawiera typy reprezentujące wiele typowych typów elementów kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="b2c6a-104">The CodeDOM provides types that represent many common types of source code elements.</span></span> <span data-ttu-id="b2c6a-105">Można zaprojektować program, który kompiluje model kodu źródłowego za pomocą elementów CodeDOM do złożenia grafu obiektów.</span><span class="sxs-lookup"><span data-stu-id="b2c6a-105">You can design a program that builds a source code model using CodeDOM elements to assemble an object graph.</span></span> <span data-ttu-id="b2c6a-106">Ten Graf obiektu może być renderowany jako kod źródłowy przy użyciu generatora kodu CodeDOM dla obsługiwanego języka programowania.</span><span class="sxs-lookup"><span data-stu-id="b2c6a-106">This object graph can be rendered as source code using a CodeDOM code generator for a supported programming language.</span></span> <span data-ttu-id="b2c6a-107">CodeDOM można także użyć do kompilowania kodu źródłowego do zestawu binarnego.</span><span class="sxs-lookup"><span data-stu-id="b2c6a-107">The CodeDOM can also be used to compile source code into a binary assembly.</span></span>  
  
 <span data-ttu-id="b2c6a-108">Niektóre typowe zastosowania dla CodeDOM:</span><span class="sxs-lookup"><span data-stu-id="b2c6a-108">Some common uses for the CodeDOM include:</span></span>  
  
- <span data-ttu-id="b2c6a-109">Generowanie kodu z szablonami: generowanie kodu dla ASP.NET, proxy klienta usług sieci Web XML, kreatorów kodu, projektantów lub innych mechanizmów emitujących kod.</span><span class="sxs-lookup"><span data-stu-id="b2c6a-109">Templated code generation: generating code for ASP.NET, XML Web services client proxies, code wizards, designers, or other code-emitting mechanisms.</span></span>  
  
- <span data-ttu-id="b2c6a-110">Kompilacja dynamiczna: obsługa kompilacji kodu w jednym lub wielu językach.</span><span class="sxs-lookup"><span data-stu-id="b2c6a-110">Dynamic compilation: supporting code compilation in single or multiple languages.</span></span>  
  
## <a name="building-a-codedom-graph"></a><span data-ttu-id="b2c6a-111">Kompilowanie wykresu CodeDOM</span><span class="sxs-lookup"><span data-stu-id="b2c6a-111">Building a CodeDOM Graph</span></span>  
 <span data-ttu-id="b2c6a-112"><xref:System.CodeDom>Przestrzeń nazw zawiera klasy służące do reprezentowania logicznej struktury kodu źródłowego, niezależnie od składni języka.</span><span class="sxs-lookup"><span data-stu-id="b2c6a-112">The <xref:System.CodeDom> namespace provides classes for representing the logical structure of source code, independent of language syntax.</span></span>  
  
### <a name="the-structure-of-a-codedom-graph"></a><span data-ttu-id="b2c6a-113">Struktura wykresu CodeDOM</span><span class="sxs-lookup"><span data-stu-id="b2c6a-113">The Structure of a CodeDOM Graph</span></span>  
 <span data-ttu-id="b2c6a-114">Struktura wykresu CodeDOM jest taka sama jak drzewo kontenerów.</span><span class="sxs-lookup"><span data-stu-id="b2c6a-114">The structure of a CodeDOM graph is like a tree of containers.</span></span> <span data-ttu-id="b2c6a-115">Najwyższego lub głównego kontenera każdy nadawać wykres CodeDOM ma wartość <xref:System.CodeDom.CodeCompileUnit> .</span><span class="sxs-lookup"><span data-stu-id="b2c6a-115">The top-most, or root, container of each compilable CodeDOM graph is a <xref:System.CodeDom.CodeCompileUnit>.</span></span> <span data-ttu-id="b2c6a-116">Każdy element modelu kodu źródłowego musi być połączony z wykresem przez właściwość <xref:System.CodeDom.CodeObject> w grafie.</span><span class="sxs-lookup"><span data-stu-id="b2c6a-116">Every element of your source code model must be linked into the graph through a property of a <xref:System.CodeDom.CodeObject> in the graph.</span></span>  
  
### <a name="building-a-source-code-model-for-a-sample-hello-world-program"></a><span data-ttu-id="b2c6a-117">Kompilowanie modelu kodu źródłowego dla przykładowego programu Hello world</span><span class="sxs-lookup"><span data-stu-id="b2c6a-117">Building a Source Code Model for a Sample Hello World Program</span></span>  
 <span data-ttu-id="b2c6a-118">Poniższy przewodnik przedstawia przykład sposobu tworzenia wykresu obiektu CodeDOM, który reprezentuje kod dla prostej aplikacji Hello world.</span><span class="sxs-lookup"><span data-stu-id="b2c6a-118">The following walkthrough provides an example of how to build a CodeDOM object graph that represents the code for a simple Hello World application.</span></span> <span data-ttu-id="b2c6a-119">Aby uzyskać pełny kod źródłowy tego przykładu kodu, zapoznaj się z <xref:System.CodeDom.Compiler.CodeDomProvider?displayProperty=nameWithType> tematem.</span><span class="sxs-lookup"><span data-stu-id="b2c6a-119">For the complete source code for this code example, see the <xref:System.CodeDom.Compiler.CodeDomProvider?displayProperty=nameWithType> topic.</span></span>  
  
#### <a name="creating-a-compile-unit"></a><span data-ttu-id="b2c6a-120">Tworzenie jednostki kompilacji</span><span class="sxs-lookup"><span data-stu-id="b2c6a-120">Creating a compile unit</span></span>  
 <span data-ttu-id="b2c6a-121">CodeDOM definiuje obiekt o nazwie <xref:System.CodeDom.CodeCompileUnit> , który może odwoływać się do wykresu obiektu CodeDOM, który modeluje kod źródłowy do skompilowania.</span><span class="sxs-lookup"><span data-stu-id="b2c6a-121">The CodeDOM defines an object called a <xref:System.CodeDom.CodeCompileUnit>, which can reference a CodeDOM object graph that models the source code to compile.</span></span> <span data-ttu-id="b2c6a-122">**CodeCompileUnit** ma właściwości do przechowywania odwołań do atrybutów, przestrzeni nazw i zestawów.</span><span class="sxs-lookup"><span data-stu-id="b2c6a-122">A **CodeCompileUnit** has properties for storing references to attributes, namespaces, and assemblies.</span></span>  
  
 <span data-ttu-id="b2c6a-123">Dostawcy CodeDom, które pochodzą z <xref:System.CodeDom.Compiler.CodeDomProvider> klasy, zawierają metody, które przetwarzają Graf obiektów, do których odwołuje się **CodeCompileUnit**.</span><span class="sxs-lookup"><span data-stu-id="b2c6a-123">The CodeDom providers that derive from the <xref:System.CodeDom.Compiler.CodeDomProvider> class contain methods that process the object graph referenced by a **CodeCompileUnit**.</span></span>  
  
 <span data-ttu-id="b2c6a-124">Aby utworzyć Graf obiektu dla prostej aplikacji, należy złożyć model kodu źródłowego i odwołać się do niego z **CodeCompileUnit**.</span><span class="sxs-lookup"><span data-stu-id="b2c6a-124">To create an object graph for a simple application, you must assemble the source code model and reference it from a **CodeCompileUnit**.</span></span>  
  
 <span data-ttu-id="b2c6a-125">Można utworzyć nową jednostkę kompilacji z składnią zademonstrowaną w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="b2c6a-125">You can create a new compile unit with the syntax demonstrated in this example:</span></span>  
  
 [!code-cpp[CodeDomExample#12](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source2.cpp#12)]
 [!code-csharp[CodeDomExample#12](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source2.cs#12)]
 [!code-vb[CodeDomExample#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source2.vb#12)]  
  
 <span data-ttu-id="b2c6a-126">Element <xref:System.CodeDom.CodeSnippetCompileUnit> może zawierać sekcję kodu źródłowego, która znajduje się już w języku docelowym, ale nie może być renderowana w innym języku.</span><span class="sxs-lookup"><span data-stu-id="b2c6a-126">A <xref:System.CodeDom.CodeSnippetCompileUnit> can contain a section of source code that is already in the target language, but cannot be rendered to another language.</span></span>  
  
#### <a name="defining-a-namespace"></a><span data-ttu-id="b2c6a-127">Definiowanie przestrzeni nazw</span><span class="sxs-lookup"><span data-stu-id="b2c6a-127">Defining a namespace</span></span>  
 <span data-ttu-id="b2c6a-128">Aby zdefiniować przestrzeń nazw, Utwórz <xref:System.CodeDom.CodeNamespace> i przypisz jej nazwę przy użyciu odpowiedniego konstruktora lub ustawiając jego właściwość **name** .</span><span class="sxs-lookup"><span data-stu-id="b2c6a-128">To define a namespace, create a <xref:System.CodeDom.CodeNamespace> and assign a name for it using the appropriate constructor or by setting its **Name** property.</span></span>  
  
 [!code-cpp[CodeDomExample#13](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source2.cpp#13)]
 [!code-csharp[CodeDomExample#13](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source2.cs#13)]
 [!code-vb[CodeDomExample#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source2.vb#13)]  
  
#### <a name="importing-a-namespace"></a><span data-ttu-id="b2c6a-129">Importowanie przestrzeni nazw</span><span class="sxs-lookup"><span data-stu-id="b2c6a-129">Importing a namespace</span></span>  
 <span data-ttu-id="b2c6a-130">Aby dodać dyrektywę import przestrzeni nazw do przestrzeni nazw, Dodaj element <xref:System.CodeDom.CodeNamespaceImport> wskazujący przestrzeń nazw do zaimportowania do kolekcji **CodeNamespace. Imports** .</span><span class="sxs-lookup"><span data-stu-id="b2c6a-130">To add a namespace import directive to the namespace, add a <xref:System.CodeDom.CodeNamespaceImport> that indicates the namespace to import to the **CodeNamespace.Imports** collection.</span></span>  
  
 <span data-ttu-id="b2c6a-131">Poniższy kod dodaje import dla przestrzeni nazw **system** do kolekcji **Imports** **CodeNamespace** o nazwie `samples` :</span><span class="sxs-lookup"><span data-stu-id="b2c6a-131">The following code adds an import for the **System** namespace to the **Imports** collection of a **CodeNamespace** named `samples`:</span></span>  
  
 [!code-cpp[CodeDomExample#14](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source2.cpp#14)]
 [!code-csharp[CodeDomExample#14](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source2.cs#14)]
 [!code-vb[CodeDomExample#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source2.vb#14)]  
  
#### <a name="linking-code-elements-into-the-object-graph"></a><span data-ttu-id="b2c6a-132">Łączenie elementów kodu do grafu obiektów</span><span class="sxs-lookup"><span data-stu-id="b2c6a-132">Linking code elements into the object graph</span></span>  
 <span data-ttu-id="b2c6a-133">Wszystkie elementy kodu, które tworzą wykres CodeDOM, muszą być połączone z <xref:System.CodeDom.CodeCompileUnit> elementem głównym drzewa przez serię odwołań między elementami, które bezpośrednio odwołują się do właściwości obiektu głównego grafu.</span><span class="sxs-lookup"><span data-stu-id="b2c6a-133">All code elements that form a CodeDOM graph must be linked to the <xref:System.CodeDom.CodeCompileUnit> that is the root element of the tree by a series of references between elements directly referenced from the properties of the root object of the graph.</span></span> <span data-ttu-id="b2c6a-134">Ustaw obiekt na właściwość obiektu kontenera, aby ustanowić odwołanie z obiektu kontenera.</span><span class="sxs-lookup"><span data-stu-id="b2c6a-134">Set an object to a property of a container object to establish a reference from the container object.</span></span>  
  
 <span data-ttu-id="b2c6a-135">Poniższa instrukcja dodaje `samples` **CodeNamespace** do właściwości kolekcji **przestrzeni nazw** głównego **CodeCompileUnit**.</span><span class="sxs-lookup"><span data-stu-id="b2c6a-135">The following statement adds the `samples` **CodeNamespace** to the **Namespaces** collection property of the root **CodeCompileUnit**.</span></span>  
  
 [!code-cpp[CodeDomExample#15](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source2.cpp#15)]
 [!code-csharp[CodeDomExample#15](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source2.cs#15)]
 [!code-vb[CodeDomExample#15](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source2.vb#15)]  
  
#### <a name="defining-a-type"></a><span data-ttu-id="b2c6a-136">Definiowanie typu</span><span class="sxs-lookup"><span data-stu-id="b2c6a-136">Defining a type</span></span>  
 <span data-ttu-id="b2c6a-137">Aby zadeklarować klasę, strukturę, interfejs lub Wyliczenie przy użyciu CodeDOM, Utwórz nowy <xref:System.CodeDom.CodeTypeDeclaration> i przypisz mu nazwę.</span><span class="sxs-lookup"><span data-stu-id="b2c6a-137">To declare a class, structure, interface, or enumeration using the CodeDOM, create a new <xref:System.CodeDom.CodeTypeDeclaration>, and assign it a name.</span></span> <span data-ttu-id="b2c6a-138">Poniższy przykład ilustruje to przy użyciu przeciążenia konstruktora, aby ustawić właściwość **name** :</span><span class="sxs-lookup"><span data-stu-id="b2c6a-138">The following example demonstrates this using a constructor overload to set the **Name** property:</span></span>  
  
 [!code-cpp[CodeDomExample#16](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source2.cpp#16)]
 [!code-csharp[CodeDomExample#16](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source2.cs#16)]
 [!code-vb[CodeDomExample#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source2.vb#16)]  
  
 <span data-ttu-id="b2c6a-139">Aby dodać typ do przestrzeni nazw, Dodaj element <xref:System.CodeDom.CodeTypeDeclaration> reprezentujący typ, który ma zostać dodany do przestrzeni nazw do kolekcji **typów** **CodeNamespace**.</span><span class="sxs-lookup"><span data-stu-id="b2c6a-139">To add a type to a namespace, add a <xref:System.CodeDom.CodeTypeDeclaration> that represents the type to add to the namespace to the **Types** collection of a **CodeNamespace**.</span></span>  
  
 <span data-ttu-id="b2c6a-140">W poniższym przykładzie pokazano, jak dodać klasę o nazwie `class1` do **CodeNamespace** o nazwie `samples` :</span><span class="sxs-lookup"><span data-stu-id="b2c6a-140">The following example demonstrates how to add a class named `class1` to a **CodeNamespace** named `samples`:</span></span>  
  
 [!code-cpp[CodeDomExample#17](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source2.cpp#17)]
 [!code-csharp[CodeDomExample#17](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source2.cs#17)]
 [!code-vb[CodeDomExample#17](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source2.vb#17)]  
  
#### <a name="adding-class-members-to-a-class"></a><span data-ttu-id="b2c6a-141">Dodawanie elementów członkowskich klasy do klasy</span><span class="sxs-lookup"><span data-stu-id="b2c6a-141">Adding class members to a class</span></span>  
 <span data-ttu-id="b2c6a-142"><xref:System.CodeDom>Przestrzeń nazw zawiera różne elementy, które mogą być używane do reprezentowania elementów członkowskich klasy.</span><span class="sxs-lookup"><span data-stu-id="b2c6a-142">The <xref:System.CodeDom> namespace provides a variety of elements that can be used to represent class members.</span></span> <span data-ttu-id="b2c6a-143">Każdy element członkowski klasy można dodać do kolekcji **Members** <xref:System.CodeDom.CodeTypeDeclaration> .</span><span class="sxs-lookup"><span data-stu-id="b2c6a-143">Each class member can be added to the **Members** collection of a <xref:System.CodeDom.CodeTypeDeclaration>.</span></span>  
  
#### <a name="defining-a-code-entry-point-method-for-an-executable"></a><span data-ttu-id="b2c6a-144">Definiowanie metody punktu wejścia kodu dla pliku wykonywalnego</span><span class="sxs-lookup"><span data-stu-id="b2c6a-144">Defining a code entry point method for an executable</span></span>  
 <span data-ttu-id="b2c6a-145">Jeśli tworzysz kod dla programu wykonywalnego, konieczne jest wskazanie punktu wejścia programu przez utworzenie elementu <xref:System.CodeDom.CodeEntryPointMethod> do reprezentowania metody, w której ma zostać rozpoczęte wykonywanie programu.</span><span class="sxs-lookup"><span data-stu-id="b2c6a-145">If you are building code for an executable program, it is necessary to indicate the entry point of a program by creating a <xref:System.CodeDom.CodeEntryPointMethod> to represent the method at which program execution should begin.</span></span>  
  
 <span data-ttu-id="b2c6a-146">Poniższy przykład ilustruje sposób definiowania metody punktu wejścia, która zawiera obiekt <xref:System.CodeDom.CodeMethodInvokeExpression> wywołujący **System. Console. WriteLine** do drukowania "Hello World!":</span><span class="sxs-lookup"><span data-stu-id="b2c6a-146">The following example demonstrates how to define an entry point method that contains a <xref:System.CodeDom.CodeMethodInvokeExpression> that calls **System.Console.WriteLine** to print "Hello World!":</span></span>  
  
 [!code-cpp[CodeDomExample#18](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source2.cpp#18)]
 [!code-csharp[CodeDomExample#18](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source2.cs#18)]
 [!code-vb[CodeDomExample#18](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source2.vb#18)]  
  
 <span data-ttu-id="b2c6a-147">Poniższa instrukcja dodaje metodę punktu wejścia o nazwie `Start` do kolekcji **Members** `class1` :</span><span class="sxs-lookup"><span data-stu-id="b2c6a-147">The following statement adds the entry point method named `Start` to the **Members** collection of `class1`:</span></span>  
  
 [!code-cpp[CodeDomExample#19](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source2.cpp#19)]
 [!code-csharp[CodeDomExample#19](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source2.cs#19)]
 [!code-vb[CodeDomExample#19](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source2.vb#19)]  
  
 <span data-ttu-id="b2c6a-148">Teraz <xref:System.CodeDom.CodeCompileUnit> nazwa `compileUnit` zawiera wykres CodeDOM dla prostego programu Hello World.</span><span class="sxs-lookup"><span data-stu-id="b2c6a-148">Now the <xref:System.CodeDom.CodeCompileUnit> named `compileUnit` contains the CodeDOM graph for a simple Hello World program.</span></span> <span data-ttu-id="b2c6a-149">Aby uzyskać informacje na temat generowania i kompilowania kodu z wykresu CodeDOM, zobacz [generowanie kodu źródłowego i kompilowanie programu z wykresu CodeDOM](generating-and-compiling-source-code-from-a-codedom-graph.md).</span><span class="sxs-lookup"><span data-stu-id="b2c6a-149">For information on generating and compiling code from a CodeDOM graph, see [Generating Source Code and Compiling a Program from a CodeDOM Graph](generating-and-compiling-source-code-from-a-codedom-graph.md).</span></span>  
  
### <a name="more-information-on-building-a-codedom-graph"></a><span data-ttu-id="b2c6a-150">Więcej informacji na temat tworzenia wykresu CodeDOM</span><span class="sxs-lookup"><span data-stu-id="b2c6a-150">More information on building a CodeDOM graph</span></span>  
 <span data-ttu-id="b2c6a-151">CodeDOM obsługuje wiele typowych typów elementów kodu znalezionych w językach programowania, które obsługują środowisko uruchomieniowe języka wspólnego.</span><span class="sxs-lookup"><span data-stu-id="b2c6a-151">The CodeDOM supports the many common types of code elements found in programming languages that support the common language runtime.</span></span> <span data-ttu-id="b2c6a-152">CodeDOM nie został zaprojektowany tak, aby zapewnić elementy reprezentujące wszystkie możliwe funkcje języka programowania.</span><span class="sxs-lookup"><span data-stu-id="b2c6a-152">The CodeDOM was not designed to provide elements to represent all possible programming language features.</span></span> <span data-ttu-id="b2c6a-153">Kod, którego nie można łatwo przedstawić z elementami CodeDOM, można hermetyzować w <xref:System.CodeDom.CodeSnippetExpression> , a, <xref:System.CodeDom.CodeSnippetStatement> <xref:System.CodeDom.CodeSnippetTypeMember> lub <xref:System.CodeDom.CodeSnippetCompileUnit> .</span><span class="sxs-lookup"><span data-stu-id="b2c6a-153">Code that cannot be represented easily with CodeDOM elements can be encapsulated in a <xref:System.CodeDom.CodeSnippetExpression>, a <xref:System.CodeDom.CodeSnippetStatement>, a <xref:System.CodeDom.CodeSnippetTypeMember>, or a <xref:System.CodeDom.CodeSnippetCompileUnit>.</span></span> <span data-ttu-id="b2c6a-154">Fragmenty kodu nie mogą jednak być tłumaczone na inne języki automatycznie przez CodeDOM.</span><span class="sxs-lookup"><span data-stu-id="b2c6a-154">However, snippets cannot be translated to other languages automatically by the CodeDOM.</span></span>  
  
 <span data-ttu-id="b2c6a-155">Aby uzyskać dokumentację dla każdego z typów CodeDOM, zobacz dokumentację referencyjną dla <xref:System.CodeDom> przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="b2c6a-155">For documentation for the each of the CodeDOM types, see the reference documentation for the <xref:System.CodeDom> namespace.</span></span>  
  
 <span data-ttu-id="b2c6a-156">Aby uzyskać szybki wykres w celu zlokalizowania elementu CodeDOM, który reprezentuje określony typ elementu kodu, zobacz [Krótki przewodnik CodeDOM](/previous-versions/dotnet/netframework-4.0/f1dfsbhc(v=vs.100)).</span><span class="sxs-lookup"><span data-stu-id="b2c6a-156">For a quick chart to locate the CodeDOM element that represents a specific type of code element, see the [CodeDOM Quick Reference](/previous-versions/dotnet/netframework-4.0/f1dfsbhc(v=vs.100)).</span></span>
