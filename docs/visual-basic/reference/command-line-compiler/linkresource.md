---
title: -linkresource
ms.date: 03/10/2018
helpviewer_keywords:
- /linkresource compiler option [Visual Basic]
- -linkresource compiler option [Visual Basic]
- linkresource compiler option [Visual Basic]
- /linkres compiler option [Visual Basic]
- linkres compiler option [Visual Basic]
- -linkres compiler option [Visual Basic]
ms.assetid: cf4dcad8-17b7-404c-9184-29358aa05b15
ms.openlocfilehash: 8c4f753f94aedaf0a4f997a3f9b99fb3f417abf8
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/23/2020
ms.locfileid: "91065687"
---
# <a name="-linkresource-visual-basic"></a><span data-ttu-id="b95b3-102">-linkresource — (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="b95b3-102">-linkresource (Visual Basic)</span></span>

<span data-ttu-id="b95b3-103">Tworzy łącze do zarządzanego zasobu.</span><span class="sxs-lookup"><span data-stu-id="b95b3-103">Creates a link to a managed resource.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="b95b3-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="b95b3-104">Syntax</span></span>  
  
```console  
-linkresource:filename[,identifier[,public|private]]  
```

<span data-ttu-id="b95b3-105">lub</span><span class="sxs-lookup"><span data-stu-id="b95b3-105">or</span></span>  

```console
-linkres:filename[,identifier[,public|private]]  
```  
  
## <a name="arguments"></a><span data-ttu-id="b95b3-106">Argumenty</span><span class="sxs-lookup"><span data-stu-id="b95b3-106">Arguments</span></span>  

 `filename`  
 <span data-ttu-id="b95b3-107">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="b95b3-107">Required.</span></span> <span data-ttu-id="b95b3-108">Plik zasobu, który ma zostać połączony z zestawem.</span><span class="sxs-lookup"><span data-stu-id="b95b3-108">The resource file to link to the assembly.</span></span> <span data-ttu-id="b95b3-109">Jeśli nazwa pliku zawiera spację, należy ująć ją w cudzysłów ("").</span><span class="sxs-lookup"><span data-stu-id="b95b3-109">If the file name contains a space, enclose the name in quotation marks (" ").</span></span>  
  
 `identifier`  
 <span data-ttu-id="b95b3-110">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="b95b3-110">Optional.</span></span> <span data-ttu-id="b95b3-111">Nazwa logiczna zasobu.</span><span class="sxs-lookup"><span data-stu-id="b95b3-111">The logical name for the resource.</span></span> <span data-ttu-id="b95b3-112">Nazwa, która jest używana do ładowania zasobu.</span><span class="sxs-lookup"><span data-stu-id="b95b3-112">The name that is used to load the resource.</span></span> <span data-ttu-id="b95b3-113">Wartość domyślna to nazwa pliku.</span><span class="sxs-lookup"><span data-stu-id="b95b3-113">The default is the name of the file.</span></span> <span data-ttu-id="b95b3-114">Opcjonalnie można określić, czy plik jest publiczny, czy prywatny w manifeście zestawu, na przykład: `-linkres:filename.res,myname.res,public` .</span><span class="sxs-lookup"><span data-stu-id="b95b3-114">Optionally, you can specify whether the file is public or private in the assembly manifest, for example: `-linkres:filename.res,myname.res,public`.</span></span> <span data-ttu-id="b95b3-115">Domyślnie jest on `filename` publiczny w zestawie.</span><span class="sxs-lookup"><span data-stu-id="b95b3-115">By default, `filename` is public in the assembly.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="b95b3-116">Uwagi</span><span class="sxs-lookup"><span data-stu-id="b95b3-116">Remarks</span></span>  

 <span data-ttu-id="b95b3-117">`-linkresource`Opcja nie osadza pliku zasobów w pliku wyjściowym; Użyj `-resource` opcji, aby to zrobić.</span><span class="sxs-lookup"><span data-stu-id="b95b3-117">The `-linkresource` option does not embed the resource file in the output file; use the `-resource` option to do this.</span></span>  
  
 <span data-ttu-id="b95b3-118">`-linkresource`Opcja wymaga jednej z `-target` opcji innych niż `-target:module` .</span><span class="sxs-lookup"><span data-stu-id="b95b3-118">The `-linkresource` option requires one of the `-target` options other than `-target:module`.</span></span>  
  
 <span data-ttu-id="b95b3-119">Jeśli `filename` jest .NET Framework utworzony plik zasobów, na przykład przez [Resgen.exe (Generator plików zasobów)](../../../framework/tools/resgen-exe-resource-file-generator.md) lub w środowisku deweloperskim, dostęp do niego można uzyskać za pomocą elementów członkowskich w <xref:System.Resources> przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="b95b3-119">If `filename` is a .NET Framework resource file created, for example, by the [Resgen.exe (Resource File Generator)](../../../framework/tools/resgen-exe-resource-file-generator.md) or in the development environment, it can be accessed with members in the <xref:System.Resources> namespace.</span></span> <span data-ttu-id="b95b3-120">(Aby uzyskać więcej informacji, zobacz <xref:System.Resources.ResourceManager> .) Aby uzyskać dostęp do wszystkich innych zasobów w czasie wykonywania, należy użyć metod, które zaczynają się od `GetManifestResource` <xref:System.Reflection.Assembly> klasy.</span><span class="sxs-lookup"><span data-stu-id="b95b3-120">(For more information, see <xref:System.Resources.ResourceManager>.) To access all other resources at run time, use the methods that begin with `GetManifestResource` in the <xref:System.Reflection.Assembly> class.</span></span>  
  
 <span data-ttu-id="b95b3-121">Nazwa pliku może być dowolnym formatem pliku.</span><span class="sxs-lookup"><span data-stu-id="b95b3-121">The file name can be any file format.</span></span> <span data-ttu-id="b95b3-122">Można na przykład utworzyć natywną bibliotekę DLL zestawu, tak aby można ją było zainstalować w globalnej pamięci podręcznej zestawów i uzyskać do niej dostęp z kodu zarządzanego w zestawie.</span><span class="sxs-lookup"><span data-stu-id="b95b3-122">For example, you may want to make a native DLL part of the assembly, so that it can be installed into the global assembly cache and accessed from managed code in the assembly.</span></span>  
  
 <span data-ttu-id="b95b3-123">Krótka forma `-linkresource` to `-linkres` .</span><span class="sxs-lookup"><span data-stu-id="b95b3-123">The short form of `-linkresource` is `-linkres`.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="b95b3-124">Ta `-linkresource` opcja jest niedostępna w środowisku deweloperskim programu Visual Studio. jest ona dostępna tylko podczas kompilowania z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="b95b3-124">The `-linkresource` option is not available from the Visual Studio development environment; it is available only when you compile from the command line.</span></span>  
  
## <a name="example"></a><span data-ttu-id="b95b3-125">Przykład</span><span class="sxs-lookup"><span data-stu-id="b95b3-125">Example</span></span>  

 <span data-ttu-id="b95b3-126">Poniższy kod kompiluje `in.vb` i łączy się z plikiem zasobów `rf.resource` .</span><span class="sxs-lookup"><span data-stu-id="b95b3-126">The following code compiles `in.vb` and links to resource file `rf.resource`.</span></span>  
  
```console  
vbc -linkresource:rf.resource in.vb  
```  
  
## <a name="see-also"></a><span data-ttu-id="b95b3-127">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="b95b3-127">See also</span></span>

- [<span data-ttu-id="b95b3-128">Kompilator wiersza polecenia Visual Basic</span><span class="sxs-lookup"><span data-stu-id="b95b3-128">Visual Basic Command-Line Compiler</span></span>](index.md)
- [<span data-ttu-id="b95b3-129">-Target (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="b95b3-129">-target (Visual Basic)</span></span>](target.md)
- [<span data-ttu-id="b95b3-130">-Resource (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="b95b3-130">-resource (Visual Basic)</span></span>](resource.md)
- [<span data-ttu-id="b95b3-131">Przykłady kompilacji — wiersze poleceń</span><span class="sxs-lookup"><span data-stu-id="b95b3-131">Sample Compilation Command Lines</span></span>](sample-compilation-command-lines.md)
