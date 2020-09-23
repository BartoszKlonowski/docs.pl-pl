---
title: -keycontainer
ms.date: 03/10/2018
helpviewer_keywords:
- -keycontainer compiler option [Visual Basic]
- keycontainer compiler option [Visual Basic]
- /keycontainer compiler option [Visual Basic]
ms.assetid: 6a9bc861-1752-4db1-9f64-b5252f0482cc
ms.openlocfilehash: 243583e55dcf278f951b813cca8384246d2d6db9
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/23/2020
ms.locfileid: "91085233"
---
# <a name="-keycontainer"></a><span data-ttu-id="9cef9-102">-keycontainer</span><span class="sxs-lookup"><span data-stu-id="9cef9-102">-keycontainer</span></span>

<span data-ttu-id="9cef9-103">Określa nazwę kontenera kluczy, aby nadać zestawowi silną nazwę.</span><span class="sxs-lookup"><span data-stu-id="9cef9-103">Specifies a key container name for a key pair to give an assembly a strong name.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="9cef9-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="9cef9-104">Syntax</span></span>  
  
```console  
-keycontainer:container  
```  
  
## <a name="arguments"></a><span data-ttu-id="9cef9-105">Argumenty</span><span class="sxs-lookup"><span data-stu-id="9cef9-105">Arguments</span></span>  
  
|<span data-ttu-id="9cef9-106">Termin</span><span class="sxs-lookup"><span data-stu-id="9cef9-106">Term</span></span>|<span data-ttu-id="9cef9-107">Definicja</span><span class="sxs-lookup"><span data-stu-id="9cef9-107">Definition</span></span>|  
|---|---|  
|`container`|<span data-ttu-id="9cef9-108">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="9cef9-108">Required.</span></span> <span data-ttu-id="9cef9-109">Plik kontenera, który zawiera klucz.</span><span class="sxs-lookup"><span data-stu-id="9cef9-109">Container file that contains the key.</span></span> <span data-ttu-id="9cef9-110">Nazwa pliku powinna być ujęta w cudzysłów (""), jeśli nazwa zawiera spację.</span><span class="sxs-lookup"><span data-stu-id="9cef9-110">Enclose the file name in quotation marks ("") if the name contains a space.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="9cef9-111">Uwagi</span><span class="sxs-lookup"><span data-stu-id="9cef9-111">Remarks</span></span>  

 <span data-ttu-id="9cef9-112">Kompilator tworzy składnik udostępniony, wstawiając klucz publiczny do manifestu zestawu i podpisując końcowy zestaw z kluczem prywatnym.</span><span class="sxs-lookup"><span data-stu-id="9cef9-112">The compiler creates the sharable component by inserting a public key into the assembly manifest and by signing the final assembly with the private key.</span></span> <span data-ttu-id="9cef9-113">Aby wygenerować plik klucza, wpisz `sn -k file` w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="9cef9-113">To generate a key file, type `sn -k file` at the command line.</span></span> <span data-ttu-id="9cef9-114">`-i`Opcja powoduje zainstalowanie pary kluczy w kontenerze.</span><span class="sxs-lookup"><span data-stu-id="9cef9-114">The `-i` option installs the key pair into a container.</span></span> <span data-ttu-id="9cef9-115">Aby uzyskać więcej informacji, zobacz [Sn.exe (Narzędzie silnej nazwy)](../../../framework/tools/sn-exe-strong-name-tool.md)).</span><span class="sxs-lookup"><span data-stu-id="9cef9-115">For more information, see [Sn.exe (Strong Name Tool)](../../../framework/tools/sn-exe-strong-name-tool.md)).</span></span>  
  
 <span data-ttu-id="9cef9-116">W przypadku kompilowania za pomocą `-target:module` programu nazwa pliku klucza jest przechowywana w module i włączana do zestawu, który jest tworzony podczas kompilowania zestawu za pomocą [-addmodule](addmodule.md).</span><span class="sxs-lookup"><span data-stu-id="9cef9-116">If you compile with `-target:module`, the name of the key file is held in the module and incorporated into the assembly that is created when you compile an assembly with [-addmodule](addmodule.md).</span></span>  
  
 <span data-ttu-id="9cef9-117">Można również określić tę opcję jako atrybut niestandardowy ( <xref:System.Reflection.AssemblyKeyNameAttribute> ) w kodzie źródłowym dla dowolnego modułu języka pośredniego (MSIL) firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9cef9-117">You can also specify this option as a custom attribute (<xref:System.Reflection.AssemblyKeyNameAttribute>) in the source code for any Microsoft intermediate language (MSIL) module.</span></span>  
  
 <span data-ttu-id="9cef9-118">Możesz również przekazać informacje o szyfrowaniu do kompilatora za pomocą [-KeyFile](keyfile.md).</span><span class="sxs-lookup"><span data-stu-id="9cef9-118">You can also pass your encryption information to the compiler with [-keyfile](keyfile.md).</span></span> <span data-ttu-id="9cef9-119">Użyj [-delaysign](delaysign.md) , jeśli chcesz użyć częściowo podpisanego zestawu.</span><span class="sxs-lookup"><span data-stu-id="9cef9-119">Use [-delaysign](delaysign.md) if you want a partially signed assembly.</span></span>  
  
 <span data-ttu-id="9cef9-120">Zobacz [Tworzenie i używanie zestawów o silnych nazwach,](../../../standard/assembly/create-use-strong-named.md) Aby uzyskać więcej informacji na temat podpisywania zestawu.</span><span class="sxs-lookup"><span data-stu-id="9cef9-120">See [Creating and Using Strong-Named Assemblies](../../../standard/assembly/create-use-strong-named.md) for more information on signing an assembly.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="9cef9-121">`-keycontainer`Opcja jest niedostępna w środowisku deweloperskim programu Visual Studio. jest ona dostępna tylko podczas kompilowania z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="9cef9-121">The `-keycontainer` option is not available from within the Visual Studio development environment; it is available only when compiling from the command line.</span></span>  
  
## <a name="example"></a><span data-ttu-id="9cef9-122">Przykład</span><span class="sxs-lookup"><span data-stu-id="9cef9-122">Example</span></span>  

 <span data-ttu-id="9cef9-123">Poniższy kod kompiluje plik źródłowy `Input.vb` i Określa kontener kluczy.</span><span class="sxs-lookup"><span data-stu-id="9cef9-123">The following code compiles source file `Input.vb` and specifies a key container.</span></span>  
  
```console  
vbc -keycontainer:key1 input.vb  
```  
  
## <a name="see-also"></a><span data-ttu-id="9cef9-124">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="9cef9-124">See also</span></span>

- [<span data-ttu-id="9cef9-125">Zestawy w środowisku .NET</span><span class="sxs-lookup"><span data-stu-id="9cef9-125">Assemblies in .NET</span></span>](../../../standard/assembly/index.md)
- [<span data-ttu-id="9cef9-126">Kompilator wiersza polecenia Visual Basic</span><span class="sxs-lookup"><span data-stu-id="9cef9-126">Visual Basic Command-Line Compiler</span></span>](index.md)
- [<span data-ttu-id="9cef9-127">-keyfile</span><span class="sxs-lookup"><span data-stu-id="9cef9-127">-keyfile</span></span>](keyfile.md)
- [<span data-ttu-id="9cef9-128">Przykłady kompilacji — wiersze poleceń</span><span class="sxs-lookup"><span data-stu-id="9cef9-128">Sample Compilation Command Lines</span></span>](sample-compilation-command-lines.md)
