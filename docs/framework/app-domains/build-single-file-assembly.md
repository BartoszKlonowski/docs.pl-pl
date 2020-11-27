---
title: 'Instrukcje: kompilowanie zestawu .NET Framework jednego pliku'
description: Zapoznaj się z tematem kompilowania zestawu jednoplikowego w programie .NET. Zestaw pojedynczego pliku może być biblioteką (. dll), która jest przeznaczona dla platformy .NET, lub może być plikiem wykonywalnym (. exe).
ms.date: 08/20/2019
helpviewer_keywords:
- assembly manifest, single-file assemblies
- library assemblies
- command-line compilers
- assemblies [.NET Framework], single-file
- output file name for assemblies
- code modules
- single-file assemblies
dev_langs:
- csharp
- vb
ms.assetid: a6063221-43a5-4d3e-814c-288a4ec69aec
ms.openlocfilehash: bdffa9417a7d52e9c825ca6455997b9bfa7408e4
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "96271528"
---
# <a name="how-to-build-a-net-framework-single-file-assembly"></a><span data-ttu-id="2c37a-104">Instrukcje: kompilowanie zestawu .NET Framework jednego pliku</span><span class="sxs-lookup"><span data-stu-id="2c37a-104">How to: Build a .NET Framework single-file assembly</span></span>

<span data-ttu-id="2c37a-105">Zestaw jednoplikowy, który jest najprostszym typem zestawu, zawiera informacje o typie i implementację, a także [manifest zestawu](../../standard/assembly/manifest.md).</span><span class="sxs-lookup"><span data-stu-id="2c37a-105">A single-file assembly, which is the simplest type of assembly, contains type information and implementation, as well as the [assembly manifest](../../standard/assembly/manifest.md).</span></span> <span data-ttu-id="2c37a-106">Można użyć kompilatorów wiersza polecenia lub programu Visual Studio, aby utworzyć zestaw jednoplikowy, który jest przeznaczony dla .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="2c37a-106">You can use command-line compilers or Visual Studio to create a single-file assembly that targets the .NET Framework.</span></span> <span data-ttu-id="2c37a-107">Domyślnie kompilator tworzy plik zestawu z rozszerzeniem *. exe* .</span><span class="sxs-lookup"><span data-stu-id="2c37a-107">By default, the compiler creates an assembly file with an *.exe* extension.</span></span>

> [!NOTE]
> <span data-ttu-id="2c37a-108">Program Visual Studio dla języka C# i Visual Basic może być używany tylko do tworzenia zestawów jednoplikowych.</span><span class="sxs-lookup"><span data-stu-id="2c37a-108">Visual Studio for C# and Visual Basic can be used only to create single-file assemblies.</span></span> <span data-ttu-id="2c37a-109">Jeśli chcesz utworzyć zestawy wieloplikowe, musisz użyć kompilatorów wiersza polecenia lub Visual C++.</span><span class="sxs-lookup"><span data-stu-id="2c37a-109">If you want to create multifile assemblies, you must use command-line compilers or Visual C++.</span></span>

<span data-ttu-id="2c37a-110">W poniższych procedurach pokazano, jak utworzyć zestawy Jednoplikowe za pomocą kompilatorów wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="2c37a-110">The following procedures show how to create single-file assemblies using command-line compilers.</span></span>

## <a name="create-an-assembly-with-an-exe-extension"></a><span data-ttu-id="2c37a-111">Utwórz zestaw z rozszerzeniem. exe</span><span class="sxs-lookup"><span data-stu-id="2c37a-111">Create an assembly with an .exe extension</span></span>

<span data-ttu-id="2c37a-112">W wierszu polecenia wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="2c37a-112">At the command prompt, type the following command:</span></span>

<span data-ttu-id="2c37a-113">\<*compiler command*> \<*module name*></span><span class="sxs-lookup"><span data-stu-id="2c37a-113">\<*compiler command*> \<*module name*></span></span>

<span data-ttu-id="2c37a-114">W tym poleceniu *kompilator* jest poleceniem kompilatora dla języka używanego w module kodu, a *Nazwa modułu* to nazwa modułu kodu do skompilowania do zestawu.</span><span class="sxs-lookup"><span data-stu-id="2c37a-114">In this command, *compiler command* is the compiler command for the language used in your code module, and *module name* is the name of the code module to compile into the assembly.</span></span>

<span data-ttu-id="2c37a-115">Poniższy przykład tworzy zestaw o nazwie *myCode.exe* z modułu kodu o nazwie `myCode` .</span><span class="sxs-lookup"><span data-stu-id="2c37a-115">The following example creates an assembly named *myCode.exe* from a code module called `myCode`.</span></span>

```csharp
csc myCode.cs
```

```vb
vbc myCode.vb
```

## <a name="create-an-assembly-with-an-exe-extension-and-specify-the-output-file-name"></a><span data-ttu-id="2c37a-116">Tworzenie zestawu z rozszerzeniem. exe i Określanie nazwy pliku wyjściowego</span><span class="sxs-lookup"><span data-stu-id="2c37a-116">Create an assembly with an .exe extension and specify the output file name</span></span>

<span data-ttu-id="2c37a-117">W wierszu polecenia wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="2c37a-117">At the command prompt, type the following command:</span></span>

<span data-ttu-id="2c37a-118">\<*compiler command*>**/out:** \<*file name*>\<*module name*></span><span class="sxs-lookup"><span data-stu-id="2c37a-118">\<*compiler command*> **/out:**\<*file name*> \<*module name*></span></span>

<span data-ttu-id="2c37a-119">W tym poleceniu *kompilator* jest poleceniem kompilatora dla języka używanego w module kodu, *Nazwa pliku* jest nazwą pliku wyjściowego, a *Nazwa modułu* to nazwa modułu kodu do skompilowania do zestawu.</span><span class="sxs-lookup"><span data-stu-id="2c37a-119">In this command, *compiler command* is the compiler command for the language used in your code module, *file name* is the output file name, and *module name* is the name of the code module to compile into the assembly.</span></span>

<span data-ttu-id="2c37a-120">Poniższy przykład tworzy zestaw o nazwie *myAssembly.exe* z modułu kodu o nazwie `myCode` .</span><span class="sxs-lookup"><span data-stu-id="2c37a-120">The following example creates an assembly named *myAssembly.exe* from a code module called `myCode`.</span></span>

```csharp
csc -out:myAssembly.exe myCode.cs
```

```vb
vbc -out:myAssembly.exe myCode.vb
```

## <a name="create-library-assemblies"></a><span data-ttu-id="2c37a-121">Utwórz zestawy bibliotek</span><span class="sxs-lookup"><span data-stu-id="2c37a-121">Create library assemblies</span></span>

 <span data-ttu-id="2c37a-122">Zestaw biblioteki jest podobny do biblioteki klas.</span><span class="sxs-lookup"><span data-stu-id="2c37a-122">A library assembly is similar to a class library.</span></span> <span data-ttu-id="2c37a-123">Zawiera typy, do których odwołują się inne zestawy, ale nie ma punktu wejścia, aby rozpocząć wykonywanie.</span><span class="sxs-lookup"><span data-stu-id="2c37a-123">It contains types that will be referenced by other assemblies, but it has no entry point to begin execution.</span></span>

<span data-ttu-id="2c37a-124">Aby utworzyć zestaw biblioteki, w wierszu polecenia wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="2c37a-124">To create a library assembly, at the command prompt, type the following command:</span></span>

<span data-ttu-id="2c37a-125">\<*compiler command*>**-t:Library**\<*module name*></span><span class="sxs-lookup"><span data-stu-id="2c37a-125">\<*compiler command*> **-t:library** \<*module name*></span></span>

<span data-ttu-id="2c37a-126">W tym poleceniu *kompilator* jest poleceniem kompilatora dla języka używanego w module kodu, a *Nazwa modułu* to nazwa modułu kodu do skompilowania do zestawu.</span><span class="sxs-lookup"><span data-stu-id="2c37a-126">In this command, *compiler command* is the compiler command for the language used in your code module, and *module name* is the name of the code module to compile into the assembly.</span></span> <span data-ttu-id="2c37a-127">Można również użyć innych opcji kompilatora, takich jak opcja **-out:** .</span><span class="sxs-lookup"><span data-stu-id="2c37a-127">You can also use other compiler options, such as the **-out:** option.</span></span>

<span data-ttu-id="2c37a-128">Poniższy przykład tworzy zestaw biblioteki o nazwie *myCodeAssembly.dll* z modułu kodu o nazwie `myCode` .</span><span class="sxs-lookup"><span data-stu-id="2c37a-128">The following example creates a library assembly named *myCodeAssembly.dll* from a code module called `myCode`.</span></span>

```csharp
csc -out:myCodeLibrary.dll -t:library myCode.cs
```

```vb
vbc -out:myCodeLibrary.dll -t:library myCode.vb
```

## <a name="see-also"></a><span data-ttu-id="2c37a-129">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="2c37a-129">See also</span></span>

- [<span data-ttu-id="2c37a-130">Tworzenie zestawów</span><span class="sxs-lookup"><span data-stu-id="2c37a-130">Create assemblies</span></span>](../../standard/assembly/create.md)
- [<span data-ttu-id="2c37a-131">Zestawy wieloplikowe</span><span class="sxs-lookup"><span data-stu-id="2c37a-131">Multifile assemblies</span></span>](multifile-assemblies.md)
- [<span data-ttu-id="2c37a-132">Instrukcje: tworzenie zestawów wieloplikowych</span><span class="sxs-lookup"><span data-stu-id="2c37a-132">How to: Build a multifile assembly</span></span>](build-multifile-assembly.md)
- [<span data-ttu-id="2c37a-133">Programowanie przy użyciu zestawów</span><span class="sxs-lookup"><span data-stu-id="2c37a-133">Program with assemblies</span></span>](../../standard/assembly/index.md)
