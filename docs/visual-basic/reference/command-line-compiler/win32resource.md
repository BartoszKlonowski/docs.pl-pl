---
title: -win32resource
ms.date: 03/13/2018
f1_keywords:
- -win32resource
- win32resource
helpviewer_keywords:
- /win32resource compiler option [Visual Basic]
- -win32resource compiler option [Visual Basic]
- win32resource compiler option [Visual Basic]
ms.assetid: e226946d-19ce-4cc9-91f5-aed24f77aa2b
ms.openlocfilehash: d146f5967058b05795026cd7726ed5eda7ba3153
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/23/2020
ms.locfileid: "91095411"
---
# <a name="-win32resource"></a><span data-ttu-id="14fd2-102">-win32resource</span><span class="sxs-lookup"><span data-stu-id="14fd2-102">-win32resource</span></span>

<span data-ttu-id="14fd2-103">Wstawia plik zasobów Win32 do pliku wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="14fd2-103">Inserts a Win32 resource file in the output file.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="14fd2-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="14fd2-104">Syntax</span></span>  
  
```console  
-win32resource:filename  
```  
  
## <a name="arguments"></a><span data-ttu-id="14fd2-105">Argumenty</span><span class="sxs-lookup"><span data-stu-id="14fd2-105">Arguments</span></span>  

 `filename`  
 <span data-ttu-id="14fd2-106">Nazwa pliku zasobów, który ma zostać dodany do pliku wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="14fd2-106">The name of the resource file to add to your output file.</span></span> <span data-ttu-id="14fd2-107">Nazwa pliku należy ująć w cudzysłów (""), jeśli zawiera spację.</span><span class="sxs-lookup"><span data-stu-id="14fd2-107">Enclose the file name in quotation marks (" ") if it contains a space.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="14fd2-108">Uwagi</span><span class="sxs-lookup"><span data-stu-id="14fd2-108">Remarks</span></span>  

 <span data-ttu-id="14fd2-109">Plik zasobów Win32 można utworzyć za pomocą kompilatora zasobów systemu Microsoft Windows (RC).</span><span class="sxs-lookup"><span data-stu-id="14fd2-109">You can create a Win32 resource file with the Microsoft Windows Resource Compiler (RC).</span></span>  
  
 <span data-ttu-id="14fd2-110">Zasób Win32 może zawierać informacje o wersji lub mapie bitowej (ikony), które ułatwiają identyfikację aplikacji w **Eksploratorze plików**.</span><span class="sxs-lookup"><span data-stu-id="14fd2-110">A Win32 resource can contain version or bitmap (icon) information that helps identify your application in **File Explorer**.</span></span> <span data-ttu-id="14fd2-111">Jeśli nie określisz `-win32resource` , kompilator generuje informacje o wersji na podstawie wersji zestawu.</span><span class="sxs-lookup"><span data-stu-id="14fd2-111">If you do not specify `-win32resource`, the compiler generates version information based on the assembly version.</span></span> <span data-ttu-id="14fd2-112">`-win32resource`Opcje i `-win32icon` wzajemnie się wykluczają.</span><span class="sxs-lookup"><span data-stu-id="14fd2-112">The `-win32resource` and `-win32icon` options are mutually exclusive.</span></span>  
  
 <span data-ttu-id="14fd2-113">Zobacz [-linkresource — (Visual Basic)](linkresource.md) , aby odwołać się do .NET Framework pliku zasobów, lub [-Resource (Visual Basic)](resource.md) , aby dołączyć plik zasobów .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="14fd2-113">See [-linkresource (Visual Basic)](linkresource.md) to reference a .NET Framework resource file, or [-resource (Visual Basic)](resource.md) to attach a .NET Framework resource file.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="14fd2-114">`-win32resource`Opcja jest niedostępna w środowisku deweloperskim programu Visual Studio. jest ona dostępna tylko podczas kompilowania z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="14fd2-114">The `-win32resource` option is not available from within the Visual Studio development environment; it is available only when compiling from the command line.</span></span>  
  
## <a name="example"></a><span data-ttu-id="14fd2-115">Przykład</span><span class="sxs-lookup"><span data-stu-id="14fd2-115">Example</span></span>  

 <span data-ttu-id="14fd2-116">Poniższy kod kompiluje `In.vb` i dołącza plik zasobów Win32 `Rf.res` :</span><span class="sxs-lookup"><span data-stu-id="14fd2-116">The following code compiles `In.vb` and attaches a Win32 resource file, `Rf.res`:</span></span>  
  
```console  
vbc -win32resource:rf.res in.vb  
```  
  
## <a name="see-also"></a><span data-ttu-id="14fd2-117">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="14fd2-117">See also</span></span>

- [<span data-ttu-id="14fd2-118">Kompilator wiersza polecenia Visual Basic</span><span class="sxs-lookup"><span data-stu-id="14fd2-118">Visual Basic Command-Line Compiler</span></span>](index.md)
- [<span data-ttu-id="14fd2-119">Przykłady kompilacji — wiersze poleceń</span><span class="sxs-lookup"><span data-stu-id="14fd2-119">Sample Compilation Command Lines</span></span>](sample-compilation-command-lines.md)
