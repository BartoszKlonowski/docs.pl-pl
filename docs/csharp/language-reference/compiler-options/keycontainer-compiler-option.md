---
description: -containerer (opcje kompilatora C#)
title: -containerer (opcje kompilatora C#)
ms.date: 05/16/2018
f1_keywords:
- /keycontainer
helpviewer_keywords:
- /keycontainer compiler option [C#]
- keycontainer compiler option [C#]
- -keycontainer compiler option [C#]
ms.assetid: b3982b6d-2382-4f7e-bebd-ce98eaa30763
ms.openlocfilehash: 93ee5cd755a4fd6918d2a5825b63151a201a8f6a
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2020
ms.locfileid: "91152471"
---
# <a name="-keycontainer-c-compiler-options"></a><span data-ttu-id="b4e2a-103">-containerer (opcje kompilatora C#)</span><span class="sxs-lookup"><span data-stu-id="b4e2a-103">-keycontainer (C# Compiler Options)</span></span>

<span data-ttu-id="b4e2a-104">Określa nazwę kontenera klucza kryptograficznego.</span><span class="sxs-lookup"><span data-stu-id="b4e2a-104">Specifies the name of the cryptographic key container.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="b4e2a-105">Składnia</span><span class="sxs-lookup"><span data-stu-id="b4e2a-105">Syntax</span></span>  
  
```console  
-keycontainer:string  
```  
  
## <a name="arguments"></a><span data-ttu-id="b4e2a-106">Argumenty</span><span class="sxs-lookup"><span data-stu-id="b4e2a-106">Arguments</span></span>  

 `string`  
 <span data-ttu-id="b4e2a-107">Nazwa kontenera klucza o silnej nazwie.</span><span class="sxs-lookup"><span data-stu-id="b4e2a-107">The name of the strong name key container.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="b4e2a-108">Uwagi</span><span class="sxs-lookup"><span data-stu-id="b4e2a-108">Remarks</span></span>  

 <span data-ttu-id="b4e2a-109">Gdy jest używana opcja **-containerer** , kompilator tworzy składnik udostępniony.</span><span class="sxs-lookup"><span data-stu-id="b4e2a-109">When the **-keycontainer** option is used, the compiler creates a sharable component.</span></span> <span data-ttu-id="b4e2a-110">Kompilator wstawia klucz publiczny z określonego kontenera do manifestu zestawu i podpisuje końcowy zestaw z kluczem prywatnym.</span><span class="sxs-lookup"><span data-stu-id="b4e2a-110">The compiler inserts a public key from the specified container into the assembly manifest and signs the final assembly with the private key.</span></span> <span data-ttu-id="b4e2a-111">Aby wygenerować plik klucza, wpisz `sn -k file` w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="b4e2a-111">To generate a key file, type `sn -k file` at the command line.</span></span> <span data-ttu-id="b4e2a-112">`sn -i` instaluje parę kluczy w kontenerze.</span><span class="sxs-lookup"><span data-stu-id="b4e2a-112">`sn -i` installs the key pair into a container.</span></span> <span data-ttu-id="b4e2a-113">Ta opcja nie jest obsługiwana, gdy kompilator działa w CoreCLR.</span><span class="sxs-lookup"><span data-stu-id="b4e2a-113">This option is not supported when the compiler runs on CoreCLR.</span></span> <span data-ttu-id="b4e2a-114">Aby podpisać zestaw podczas kompilowania na CoreCLR, użyj opcji [-KeyFile](keyfile-compiler-option.md) .</span><span class="sxs-lookup"><span data-stu-id="b4e2a-114">To sign an assembly when building on CoreCLR, use the [-keyfile](keyfile-compiler-option.md) option.</span></span>
  
 <span data-ttu-id="b4e2a-115">W przypadku kompilowania z [modułem-target:](./target-module-compiler-option.md)nazwa pliku klucza jest przechowywana w module i wbudowana w zestaw podczas kompilowania tego modułu do zestawu za pomocą [-addmodule](./addmodule-compiler-option.md).</span><span class="sxs-lookup"><span data-stu-id="b4e2a-115">If you compile with [-target:module](./target-module-compiler-option.md), the name of the key file is held in the module and incorporated into the assembly when you compile this module into an assembly with [-addmodule](./addmodule-compiler-option.md).</span></span>  
  
 <span data-ttu-id="b4e2a-116">Można również określić tę opcję jako atrybut niestandardowy ( <xref:System.Reflection.AssemblyKeyNameAttribute?displayProperty=nameWithType> ) w kodzie źródłowym dla dowolnego modułu języka pośredniego (MSIL) firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b4e2a-116">You can also specify this option as a custom attribute (<xref:System.Reflection.AssemblyKeyNameAttribute?displayProperty=nameWithType>) in the source code for any Microsoft intermediate language (MSIL) module.</span></span>  
  
 <span data-ttu-id="b4e2a-117">Możesz również przekazać informacje o szyfrowaniu do kompilatora za pomocą [-KeyFile](./keyfile-compiler-option.md).</span><span class="sxs-lookup"><span data-stu-id="b4e2a-117">You can also pass your encryption information to the compiler with [-keyfile](./keyfile-compiler-option.md).</span></span> <span data-ttu-id="b4e2a-118">Użyj [-delaysign](./delaysign-compiler-option.md) , jeśli chcesz, aby klucz publiczny został dodany do manifestu zestawu, ale chcesz opóźnić podpisywanie zestawu do momentu przetestowania.</span><span class="sxs-lookup"><span data-stu-id="b4e2a-118">Use [-delaysign](./delaysign-compiler-option.md) if you want the public key added to the assembly manifest but want to delay signing the assembly until it has been tested.</span></span>  
  
 <span data-ttu-id="b4e2a-119">Aby uzyskać więcej informacji, zobacz [Tworzenie i używanie zestawów Strong-Named](../../../standard/assembly/create-use-strong-named.md) i [opóźnianie podpisywania zestawu](../../../standard/assembly/delay-sign.md).</span><span class="sxs-lookup"><span data-stu-id="b4e2a-119">For more information, see [Creating and Using Strong-Named Assemblies](../../../standard/assembly/create-use-strong-named.md) and [Delay Signing an Assembly](../../../standard/assembly/delay-sign.md).</span></span>  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a><span data-ttu-id="b4e2a-120">Aby ustawić tę opcję kompilatora w środowisku programowania Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b4e2a-120">To set this compiler option in the Visual Studio development environment</span></span>  
  
1. <span data-ttu-id="b4e2a-121">Ta opcja kompilatora nie jest dostępna w środowisku deweloperskim programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b4e2a-121">This compiler option is not available in the Visual Studio development environment.</span></span>  
  
 <span data-ttu-id="b4e2a-122">Można programowo uzyskać dostęp do tej opcji kompilatora przy użyciu <xref:VSLangProj.ProjectProperties.AssemblyKeyContainerName%2A> .</span><span class="sxs-lookup"><span data-stu-id="b4e2a-122">You can programmatically access this compiler option with <xref:VSLangProj.ProjectProperties.AssemblyKeyContainerName%2A>.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="b4e2a-123">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="b4e2a-123">See also</span></span>

- [<span data-ttu-id="b4e2a-124">Kompilator języka C# — opcja keyfile</span><span class="sxs-lookup"><span data-stu-id="b4e2a-124">C# Compiler -keyfile option</span></span>](keyfile-compiler-option.md)
- [<span data-ttu-id="b4e2a-125">Opcje kompilatora C#</span><span class="sxs-lookup"><span data-stu-id="b4e2a-125">C# Compiler Options</span></span>](index.md)
- [<span data-ttu-id="b4e2a-126">Zarządzanie właściwościami projektów i rozwiązań</span><span class="sxs-lookup"><span data-stu-id="b4e2a-126">Managing Project and Solution Properties</span></span>](/visualstudio/ide/managing-project-and-solution-properties)
