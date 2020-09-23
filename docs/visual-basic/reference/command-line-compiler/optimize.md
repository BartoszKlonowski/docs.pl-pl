---
title: -optimize
ms.date: 07/20/2015
helpviewer_keywords:
- optimize compiler option [Visual Basic]
- /optimize compiler option [Visual Basic]
- optimization [Visual Basic], enabling
- -optimize compiler option [Visual Basic]
ms.assetid: fcba4a97-3622-4b87-a891-0f77deab4998
ms.openlocfilehash: d4b50d56373676bf78a7591102095209401c907d
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/23/2020
ms.locfileid: "91097595"
---
# <a name="-optimize"></a><span data-ttu-id="8bbac-102">-optimize</span><span class="sxs-lookup"><span data-stu-id="8bbac-102">-optimize</span></span>

<span data-ttu-id="8bbac-103">Włącza lub wyłącza optymalizacje kompilatora.</span><span class="sxs-lookup"><span data-stu-id="8bbac-103">Enables or disables compiler optimizations.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="8bbac-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="8bbac-104">Syntax</span></span>  
  
```console  
-optimize[ + | - ]  
```  
  
## <a name="arguments"></a><span data-ttu-id="8bbac-105">Argumenty</span><span class="sxs-lookup"><span data-stu-id="8bbac-105">Arguments</span></span>  
  
|<span data-ttu-id="8bbac-106">Termin</span><span class="sxs-lookup"><span data-stu-id="8bbac-106">Term</span></span>|<span data-ttu-id="8bbac-107">Definicja</span><span class="sxs-lookup"><span data-stu-id="8bbac-107">Definition</span></span>|  
|---|---|  
|<span data-ttu-id="8bbac-108">`+` &#124; `-`</span><span class="sxs-lookup"><span data-stu-id="8bbac-108">`+` &#124; `-`</span></span>|<span data-ttu-id="8bbac-109">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="8bbac-109">Optional.</span></span> <span data-ttu-id="8bbac-110">`-optimize-`Opcja wyłącza optymalizacje kompilatora.</span><span class="sxs-lookup"><span data-stu-id="8bbac-110">The `-optimize-` option disables compiler optimizations.</span></span> <span data-ttu-id="8bbac-111">`-optimize+`Opcja włącza optymalizacje.</span><span class="sxs-lookup"><span data-stu-id="8bbac-111">The `-optimize+` option enables optimizations.</span></span> <span data-ttu-id="8bbac-112">Optymalizacje są domyślnie wyłączone.</span><span class="sxs-lookup"><span data-stu-id="8bbac-112">By default, optimizations are disabled.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="8bbac-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="8bbac-113">Remarks</span></span>  

 <span data-ttu-id="8bbac-114">Optymalizacje kompilatora sprawiają, że plik wyjściowy jest mniejszy, szybszy i bardziej wydajny.</span><span class="sxs-lookup"><span data-stu-id="8bbac-114">Compiler optimizations make your output file smaller, faster, and more efficient.</span></span> <span data-ttu-id="8bbac-115">Jednakże, ponieważ optymalizacje powodują przemieszczenie kodu w pliku wyjściowym, `-optimize+` może utrudniać debugowanie.</span><span class="sxs-lookup"><span data-stu-id="8bbac-115">However, because optimizations result in code rearrangement in the output file, `-optimize+` can make debugging difficult.</span></span>  
  
 <span data-ttu-id="8bbac-116">Wszystkie moduły wygenerowane `-target:module` dla zestawu muszą używać tych samych `-optimize` ustawień co zestaw.</span><span class="sxs-lookup"><span data-stu-id="8bbac-116">All modules generated with `-target:module` for an assembly must use the same `-optimize` settings as the assembly.</span></span> <span data-ttu-id="8bbac-117">Aby uzyskać więcej informacji, zobacz [-Target (Visual Basic)](target.md).</span><span class="sxs-lookup"><span data-stu-id="8bbac-117">For more information, see [-target (Visual Basic)](target.md).</span></span>  
  
 <span data-ttu-id="8bbac-118">Można połączyć `-optimize` `-debug` Opcje i.</span><span class="sxs-lookup"><span data-stu-id="8bbac-118">You can combine the `-optimize` and `-debug` options.</span></span>  
  
|<span data-ttu-id="8bbac-119">Aby ustawić-optymalizować w zintegrowanym środowisku programistycznym programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8bbac-119">To set -optimize in the Visual Studio integrated development environment</span></span>|  
|---|  
|<span data-ttu-id="8bbac-120">1. zaznaczono projekt w **Eksplorator rozwiązań**.</span><span class="sxs-lookup"><span data-stu-id="8bbac-120">1.  Have a project selected in **Solution Explorer**.</span></span> <span data-ttu-id="8bbac-121">W menu **projekt** kliknij polecenie **Właściwości**.</span><span class="sxs-lookup"><span data-stu-id="8bbac-121">On the **Project** menu, click **Properties**.</span></span><br />     <br /><span data-ttu-id="8bbac-122">2. Kliknij kartę **kompilacja** .</span><span class="sxs-lookup"><span data-stu-id="8bbac-122">2.  Click the **Compile** tab.</span></span><br /><span data-ttu-id="8bbac-123">3. kliknij przycisk **Zaawansowane** .</span><span class="sxs-lookup"><span data-stu-id="8bbac-123">3.  Click the **Advanced** button.</span></span><br /><span data-ttu-id="8bbac-124">4. Zmodyfikuj pole wyboru **Włącz optymalizacje** .</span><span class="sxs-lookup"><span data-stu-id="8bbac-124">4.  Modify the **Enable optimizations** check box.</span></span>|  
  
## <a name="example"></a><span data-ttu-id="8bbac-125">Przykład</span><span class="sxs-lookup"><span data-stu-id="8bbac-125">Example</span></span>  

 <span data-ttu-id="8bbac-126">Poniższy kod kompiluje `T2.vb` i włącza optymalizacje kompilatora.</span><span class="sxs-lookup"><span data-stu-id="8bbac-126">The following code compiles `T2.vb` and enables compiler optimizations.</span></span>  
  
```console
vbc t2.vb -optimize  
```  
  
## <a name="see-also"></a><span data-ttu-id="8bbac-127">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="8bbac-127">See also</span></span>

- [<span data-ttu-id="8bbac-128">Kompilator wiersza polecenia Visual Basic</span><span class="sxs-lookup"><span data-stu-id="8bbac-128">Visual Basic Command-Line Compiler</span></span>](index.md)
- [<span data-ttu-id="8bbac-129">-Debug (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="8bbac-129">-debug (Visual Basic)</span></span>](debug.md)
- [<span data-ttu-id="8bbac-130">Przykłady kompilacji — wiersze poleceń</span><span class="sxs-lookup"><span data-stu-id="8bbac-130">Sample Compilation Command Lines</span></span>](sample-compilation-command-lines.md)
- [<span data-ttu-id="8bbac-131">-Target (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="8bbac-131">-target (Visual Basic)</span></span>](target.md)
