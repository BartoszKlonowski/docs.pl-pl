---
title: Generowanie i kompilowanie kodu źródłowego z wykresu CodeDOM
description: Generowanie i kompilowanie kodu źródłowego z wykresu CodeDOM w programie .NET. Użyj dostawcy kodu CodeDOM do wygenerowania kodu źródłowego i kompilowania zestawów.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- code compilers
- CodeDOM, generating source code
- Code Document Object Model, graphs
- templated code generation
- source code, generating
- dynamically representing source code
- generating CodeDOM graphs
- Code Document Object Model, generating source code
- translating language to language
- compiling assemblies
- generating source code in multiple languages
- graphing with CodeDOM
- dynamic compilation
- assemblies [.NET Framework], CodeDOM
- source code generation
- outputting source code by CodeDOM
- code generators
- compiling source code, multiple languages
- CodeDOM, graphs
ms.assetid: 6c864c8e-6dd3-4a65-ace0-36879d9a9c42
ms.openlocfilehash: aec7d6b44e63558ae70bc0eb41f94e55c8a6c325
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96266340"
---
# <a name="generating-and-compiling-source-code-from-a-codedom-graph"></a><span data-ttu-id="05984-104">Generowanie i kompilowanie kodu źródłowego z wykresu CodeDOM</span><span class="sxs-lookup"><span data-stu-id="05984-104">Generating and Compiling Source Code from a CodeDOM Graph</span></span>

<span data-ttu-id="05984-105"><xref:System.CodeDom.Compiler>Przestrzeń nazw udostępnia interfejsy do generowania kodu źródłowego z grafów obiektów CodeDOM i do zarządzania kompilacją z obsługiwanymi kompilatorami.</span><span class="sxs-lookup"><span data-stu-id="05984-105">The <xref:System.CodeDom.Compiler> namespace provides interfaces for generating source code from CodeDOM object graphs and for managing compilation with supported compilers.</span></span> <span data-ttu-id="05984-106">Dostawca kodu może utworzyć kod źródłowy w określonym języku programowania zgodnie z wykresem CodeDOM.</span><span class="sxs-lookup"><span data-stu-id="05984-106">A code provider can produce source code in a particular programming language according to a CodeDOM graph.</span></span> <span data-ttu-id="05984-107">Klasa, która pochodzi od, <xref:System.CodeDom.Compiler.CodeDomProvider> zazwyczaj dostarcza metody do generowania i kompilowania kodu dla języka obsługiwanego przez dostawcę.</span><span class="sxs-lookup"><span data-stu-id="05984-107">A class that derives from <xref:System.CodeDom.Compiler.CodeDomProvider> can typically provide methods for generating and compiling code for the language the provider supports.</span></span>  
  
## <a name="using-a-codedom-code-provider-to-generate-source-code"></a><span data-ttu-id="05984-108">Generowanie kodu źródłowego przy użyciu dostawcy kodu CodeDOM</span><span class="sxs-lookup"><span data-stu-id="05984-108">Using a CodeDOM code provider to generate source code</span></span>  

 <span data-ttu-id="05984-109">Aby wygenerować kod źródłowy w określonym języku, potrzebny jest wykres CodeDOM, który reprezentuje strukturę kodu źródłowego do wygenerowania.</span><span class="sxs-lookup"><span data-stu-id="05984-109">To generate source code in a particular language, you need a CodeDOM graph that represents the structure of the source code to generate.</span></span>  
  
 <span data-ttu-id="05984-110">Poniższy przykład pokazuje, jak utworzyć wystąpienie obiektu <xref:Microsoft.CSharp.CSharpCodeProvider> :</span><span class="sxs-lookup"><span data-stu-id="05984-110">The following example demonstrate how to create an instance of a <xref:Microsoft.CSharp.CSharpCodeProvider>:</span></span>  
  
 [!code-cpp[CodeDomExample#21](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source3.cpp#21)]
 [!code-csharp[CodeDomExample#21](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source3.cs#21)]
 [!code-vb[CodeDomExample#21](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source3.vb#21)]  
  
 <span data-ttu-id="05984-111">Wykres generowania kodu jest zwykle zawarty w <xref:System.CodeDom.CodeCompileUnit> .</span><span class="sxs-lookup"><span data-stu-id="05984-111">The graph for code generation is typically contained in a <xref:System.CodeDom.CodeCompileUnit>.</span></span> <span data-ttu-id="05984-112">Aby wygenerować kod dla **CodeCompileUnit** zawierającego wykres CodeDOM, wywołaj <xref:System.CodeDom.Compiler.CodeDomProvider.GenerateCodeFromCompileUnit%2A> metodę dostawcy kodu.</span><span class="sxs-lookup"><span data-stu-id="05984-112">To generate code for a **CodeCompileUnit** that contains a CodeDOM graph, call the <xref:System.CodeDom.Compiler.CodeDomProvider.GenerateCodeFromCompileUnit%2A> method of the code provider.</span></span> <span data-ttu-id="05984-113">Ta metoda ma parametr <xref:System.IO.TextWriter> , który używa do generowania kodu źródłowego, więc czasami konieczne jest utworzenie elementu **TextWriter** , do którego można pisać.</span><span class="sxs-lookup"><span data-stu-id="05984-113">This method has a parameter for a <xref:System.IO.TextWriter> that it uses to generate the source code, so it is sometimes necessary to first create a **TextWriter** that can be written to.</span></span> <span data-ttu-id="05984-114">Poniższy przykład demonstruje generowanie kodu z **CodeCompileUnit** i zapisywanie wygenerowanego kodu źródłowego do pliku o nazwie HelloWorld.cs.</span><span class="sxs-lookup"><span data-stu-id="05984-114">The following example demonstrates generating code from a **CodeCompileUnit** and writing the generated source code to a file named HelloWorld.cs.</span></span>  
  
 [!code-cpp[CodeDomExample#22](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source3.cpp#22)]
 [!code-csharp[CodeDomExample#22](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source3.cs#22)]
 [!code-vb[CodeDomExample#22](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source3.vb#22)]  
  
## <a name="using-a-codedom-code-provider-to-compile-assemblies"></a><span data-ttu-id="05984-115">Używanie dostawcy kodu CodeDOM do kompilowania zestawów</span><span class="sxs-lookup"><span data-stu-id="05984-115">Using a CodeDOM code provider to compile assemblies</span></span>  

 <span data-ttu-id="05984-116">**Wywoływanie kompilacji**</span><span class="sxs-lookup"><span data-stu-id="05984-116">**Invoking compilation**</span></span>  
  
 <span data-ttu-id="05984-117">Aby skompilować zestaw przy użyciu dostawcy CodeDom, musisz mieć kod źródłowy do skompilowania w języku, dla którego masz kompilator, lub wykres CodeDOM, który może zostać wygenerowany przez kod źródłowy do skompilowania.</span><span class="sxs-lookup"><span data-stu-id="05984-117">To compile an assembly using a CodeDom provider, you must have either source code to compile in a language for which you have a compiler, or a CodeDOM graph that source code to compile can be generated from.</span></span>  
  
 <span data-ttu-id="05984-118">Jeśli kompilujesz z wykresu CodeDOM, Przekaż <xref:System.CodeDom.CodeCompileUnit> zawierający wykres do <xref:System.CodeDom.Compiler.CodeDomProvider.CompileAssemblyFromDom%2A> metody dostawcy kodu.</span><span class="sxs-lookup"><span data-stu-id="05984-118">If you are compiling from a CodeDOM graph, pass the <xref:System.CodeDom.CodeCompileUnit> containing the graph to the <xref:System.CodeDom.Compiler.CodeDomProvider.CompileAssemblyFromDom%2A> method of the code provider.</span></span> <span data-ttu-id="05984-119">Jeśli masz plik kodu źródłowego w języku, który jest rozpoznawany przez kompilator, przekaż nazwę pliku zawierającego kod źródłowy do <xref:System.CodeDom.Compiler.CodeDomProvider.CompileAssemblyFromFile%2A> metody dostawcy CodeDOM.</span><span class="sxs-lookup"><span data-stu-id="05984-119">If you have a source code file in a language that the compiler understands, pass the name of the file containing the source code to the <xref:System.CodeDom.Compiler.CodeDomProvider.CompileAssemblyFromFile%2A> method of the CodeDom provider.</span></span> <span data-ttu-id="05984-120">Możesz również przekazać ciąg zawierający kod źródłowy w języku, który kompilator rozumie do <xref:System.CodeDom.Compiler.CodeDomProvider.CompileAssemblyFromSource%2A> metody dostawcy CodeDOM.</span><span class="sxs-lookup"><span data-stu-id="05984-120">You can also pass a string containing source code in a language that the compiler understands to the <xref:System.CodeDom.Compiler.CodeDomProvider.CompileAssemblyFromSource%2A> method of the CodeDom provider.</span></span>  
  
 <span data-ttu-id="05984-121">**Konfigurowanie parametrów kompilacji**</span><span class="sxs-lookup"><span data-stu-id="05984-121">**Configuring compilation parameters**</span></span>  
  
 <span data-ttu-id="05984-122">Wszystkie standardowe kompilacje — metody wywołania dostawcy CodeDom mają parametr typu <xref:System.CodeDom.Compiler.CompilerParameters> , który wskazuje opcje do użycia dla kompilacji.</span><span class="sxs-lookup"><span data-stu-id="05984-122">All of the standard compilation-invoking methods of a CodeDom provider have a parameter of type <xref:System.CodeDom.Compiler.CompilerParameters> that indicates the options to use for compilation.</span></span>  
  
 <span data-ttu-id="05984-123">Możesz określić nazwę pliku dla zestawu wyjściowego we <xref:System.CodeDom.Compiler.CompilerParameters.OutputAssembly%2A> właściwości **CompilerParameters**.</span><span class="sxs-lookup"><span data-stu-id="05984-123">You can specify a file name for the output assembly in the <xref:System.CodeDom.Compiler.CompilerParameters.OutputAssembly%2A> property of the **CompilerParameters**.</span></span> <span data-ttu-id="05984-124">W przeciwnym razie zostanie użyta domyślna nazwa pliku wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="05984-124">Otherwise, a default output file name will be used.</span></span>  
  
 <span data-ttu-id="05984-125">Domyślnie nowy **CompilerParameters** jest inicjowany z <xref:System.CodeDom.Compiler.CompilerParameters.GenerateExecutable%2A> właściwością ustawioną na **wartość false**.</span><span class="sxs-lookup"><span data-stu-id="05984-125">By default, a new **CompilerParameters** is initialized with its <xref:System.CodeDom.Compiler.CompilerParameters.GenerateExecutable%2A> property set to **false**.</span></span> <span data-ttu-id="05984-126">W przypadku kompilowania programu wykonywalnego należy ustawić **wartość true** dla właściwości **GenerateExecutable** .</span><span class="sxs-lookup"><span data-stu-id="05984-126">If you are compiling an executable program, you must set the **GenerateExecutable** property to **true**.</span></span> <span data-ttu-id="05984-127">Gdy **GenerateExecutable** ma wartość **false**, kompilator wygeneruje bibliotekę klas.</span><span class="sxs-lookup"><span data-stu-id="05984-127">When the **GenerateExecutable** is set to **false**, the compiler will generate a class library.</span></span>  
  
 <span data-ttu-id="05984-128">Jeśli kompilujesz plik wykonywalny z wykresu CodeDOM, <xref:System.CodeDom.CodeEntryPointMethod> musi on być zdefiniowany w grafie.</span><span class="sxs-lookup"><span data-stu-id="05984-128">If you are compiling an executable from a CodeDOM graph, a <xref:System.CodeDom.CodeEntryPointMethod> must be defined in the graph.</span></span> <span data-ttu-id="05984-129">Jeśli istnieje wiele punktów wejścia kodu, może być konieczne ustawienie <xref:System.CodeDom.Compiler.CompilerParameters.MainClass%2A> właściwości **CompilerParameters** na nazwę klasy, która definiuje punkt wejścia do użycia.</span><span class="sxs-lookup"><span data-stu-id="05984-129">If there are multiple code entry points, it may be necessary to set the <xref:System.CodeDom.Compiler.CompilerParameters.MainClass%2A> property of the **CompilerParameters** to the name of the class that defines the entry point to use.</span></span>  
  
 <span data-ttu-id="05984-130">Aby dołączyć informacje debugowania w wygenerowanym pliku wykonywalnym, należy ustawić <xref:System.CodeDom.Compiler.CompilerParameters.IncludeDebugInformation%2A> Właściwość na **true**.</span><span class="sxs-lookup"><span data-stu-id="05984-130">To include debug information in a generated executable, set the <xref:System.CodeDom.Compiler.CompilerParameters.IncludeDebugInformation%2A> property to **true**.</span></span>  
  
 <span data-ttu-id="05984-131">Jeśli projekt odwołuje się do wszystkich zestawów, należy określić nazwy zestawów jako elementy w <xref:System.Collections.Specialized.StringCollection> jako <xref:System.CodeDom.Compiler.CompilerParameters.ReferencedAssemblies%2A> Właściwość **CompilerParameters** używanego podczas wywoływania kompilacji.</span><span class="sxs-lookup"><span data-stu-id="05984-131">If your project references any assemblies, you must specify the assembly names as items in a <xref:System.Collections.Specialized.StringCollection> as the <xref:System.CodeDom.Compiler.CompilerParameters.ReferencedAssemblies%2A> property of the **CompilerParameters** you use when invoking compilation.</span></span>  
  
 <span data-ttu-id="05984-132">Można skompilować zestaw, który jest zapisywana w pamięci, a nie na dysku, ustawiając <xref:System.CodeDom.Compiler.CompilerParameters.GenerateInMemory%2A> Właściwość na **true**.</span><span class="sxs-lookup"><span data-stu-id="05984-132">You can compile an assembly that is written to memory rather than disk by setting the <xref:System.CodeDom.Compiler.CompilerParameters.GenerateInMemory%2A> property to **true**.</span></span> <span data-ttu-id="05984-133">Gdy zestaw jest generowany w pamięci, kod może uzyskać odwołanie do wygenerowanego zestawu z <xref:System.CodeDom.Compiler.CompilerResults.CompiledAssembly%2A> właściwości <xref:System.CodeDom.Compiler.CompilerResults> .</span><span class="sxs-lookup"><span data-stu-id="05984-133">When an assembly is generated in memory, your code can obtain a reference to the generated assembly from the <xref:System.CodeDom.Compiler.CompilerResults.CompiledAssembly%2A> property of a <xref:System.CodeDom.Compiler.CompilerResults>.</span></span> <span data-ttu-id="05984-134">Jeśli zestaw jest zapisywana na dysku, można uzyskać ścieżkę do wygenerowanego zestawu z <xref:System.CodeDom.Compiler.CompilerResults.PathToAssembly%2A> właściwości **CompilerResults**.</span><span class="sxs-lookup"><span data-stu-id="05984-134">If an assembly is written to disk, you can obtain the path to the generated assembly from the <xref:System.CodeDom.Compiler.CompilerResults.PathToAssembly%2A> property of a **CompilerResults**.</span></span>  
  
 <span data-ttu-id="05984-135">Aby określić niestandardowy ciąg argumentów wiersza polecenia, który ma być używany podczas wywoływania procesu kompilacji, należy ustawić ciąg we <xref:System.CodeDom.Compiler.CompilerParameters.CompilerOptions%2A> właściwości.</span><span class="sxs-lookup"><span data-stu-id="05984-135">To specify a custom command-line arguments string to use when invoking the compilation process, set the string in the <xref:System.CodeDom.Compiler.CompilerParameters.CompilerOptions%2A> property.</span></span>  
  
 <span data-ttu-id="05984-136">Jeśli token zabezpieczający Win32 jest wymagany do wywołania procesu kompilatora, należy określić token we <xref:System.CodeDom.Compiler.CompilerParameters.UserToken%2A> właściwości.</span><span class="sxs-lookup"><span data-stu-id="05984-136">If a Win32 security token is required to invoke the compiler process, specify the token in the <xref:System.CodeDom.Compiler.CompilerParameters.UserToken%2A> property.</span></span>  
  
 <span data-ttu-id="05984-137">Aby połączyć plik zasobów Win32 do skompilowanego zestawu, należy określić nazwę pliku zasobów Win32 we <xref:System.CodeDom.Compiler.CompilerParameters.Win32Resource%2A> właściwości.</span><span class="sxs-lookup"><span data-stu-id="05984-137">To link a Win32 resource file into the compiled assembly, specify the name of the Win32 resource file in the <xref:System.CodeDom.Compiler.CompilerParameters.Win32Resource%2A> property.</span></span>  
  
 <span data-ttu-id="05984-138">Aby określić poziom ostrzeżeń, dla którego ma zostać zatrzymana kompilacja, należy ustawić <xref:System.CodeDom.Compiler.CompilerParameters.WarningLevel%2A> Właściwość na liczbę całkowitą reprezentującą poziom ostrzeżenia, przy którym ma zostać zatrzymana kompilacja.</span><span class="sxs-lookup"><span data-stu-id="05984-138">To specify a warning level at which to halt compilation, set the <xref:System.CodeDom.Compiler.CompilerParameters.WarningLevel%2A> property to an integer that represents the warning level at which to halt compilation.</span></span> <span data-ttu-id="05984-139">Możesz również skonfigurować kompilator, aby zatrzymać kompilację w przypadku wystąpienia ostrzeżeń przez ustawienie <xref:System.CodeDom.Compiler.CompilerParameters.TreatWarningsAsErrors%2A> właściwości na **wartość true**.</span><span class="sxs-lookup"><span data-stu-id="05984-139">You can also configure the compiler to halt compilation if warnings are encountered by setting the <xref:System.CodeDom.Compiler.CompilerParameters.TreatWarningsAsErrors%2A> property to **true**.</span></span>  
  
 <span data-ttu-id="05984-140">Poniższy przykład kodu demonstruje Kompilowanie pliku źródłowego przy użyciu dostawcy CodeDom pochodnego od <xref:System.CodeDom.Compiler.CodeDomProvider> klasy.</span><span class="sxs-lookup"><span data-stu-id="05984-140">The following code example demonstrates compiling a source file using a CodeDom provider derived from the <xref:System.CodeDom.Compiler.CodeDomProvider> class.</span></span>  
  
 [!code-cpp[CodeDomExample#23](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source3.cpp#23)]
 [!code-csharp[CodeDomExample#23](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source3.cs#23)]
 [!code-vb[CodeDomExample#23](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source3.vb#23)]  
  
## <a name="languages-with-initial-support"></a><span data-ttu-id="05984-141">Języki z zapoczątkową pomocą techniczną</span><span class="sxs-lookup"><span data-stu-id="05984-141">Languages with Initial Support</span></span>  

 <span data-ttu-id="05984-142">.NET Framework zapewnia kompilatory kodu i generatory kodu dla następujących języków: C#, Visual Basic, C++ i JScript.</span><span class="sxs-lookup"><span data-stu-id="05984-142">The .NET Framework provides code compilers and code generators for the following languages: C#, Visual Basic, C++, and JScript.</span></span> <span data-ttu-id="05984-143">Obsługę CodeDOM można rozszerzyć do innych języków przez implementację generatorów kodu specyficznych dla języka i kompilatorów kodu.</span><span class="sxs-lookup"><span data-stu-id="05984-143">CodeDOM support can be extended to other languages by implementing language-specific code generators and code compilers.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="05984-144">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="05984-144">See also</span></span>

- <xref:System.CodeDom>
- <xref:System.CodeDom.Compiler>
- [<span data-ttu-id="05984-145">Dynamiczne generowanie i kompilacja kodu źródłowego</span><span class="sxs-lookup"><span data-stu-id="05984-145">Dynamic Source Code Generation and Compilation</span></span>](dynamic-source-code-generation-and-compilation.md)
- <span data-ttu-id="05984-146">[Zwięzłe odwołanie CodeDOM](/previous-versions/dotnet/netframework-4.0/f1dfsbhc(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="05984-146">[CodeDOM Quick Reference](/previous-versions/dotnet/netframework-4.0/f1dfsbhc(v=vs.100))</span></span>
