---
title: -define
ms.date: 03/10/2018
helpviewer_keywords:
- -d compiler option [Visual Basic]
- /d compiler option [Visual Basic]
- -define compiler option [Visual Basic]
- d compiler option [Visual Basic]
- /define compiler option [Visual Basic]
- define compiler option [Visual Basic]
ms.assetid: f735c57d-1cf9-4f2f-a26f-0de630fd4077
ms.openlocfilehash: cb56e727479fd249cb0d7e5e7c3c50d5b68b3a72
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/23/2020
ms.locfileid: "91072018"
---
# <a name="-define-visual-basic"></a><span data-ttu-id="aba9f-102">-Definiuj (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="aba9f-102">-define (Visual Basic)</span></span>

<span data-ttu-id="aba9f-103">Definiuje warunkowe stałe kompilatora.</span><span class="sxs-lookup"><span data-stu-id="aba9f-103">Defines conditional compiler constants.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="aba9f-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="aba9f-104">Syntax</span></span>  
  
```console  
-define:["]symbol[=value][,symbol[=value]]["]  
```

<span data-ttu-id="aba9f-105">lub</span><span class="sxs-lookup"><span data-stu-id="aba9f-105">or</span></span>

```console  
-d:["]symbol[=value][,symbol[=value]]["]  
```  
  
## <a name="arguments"></a><span data-ttu-id="aba9f-106">Argumenty</span><span class="sxs-lookup"><span data-stu-id="aba9f-106">Arguments</span></span>  
  
|<span data-ttu-id="aba9f-107">Termin</span><span class="sxs-lookup"><span data-stu-id="aba9f-107">Term</span></span>|<span data-ttu-id="aba9f-108">Definicja</span><span class="sxs-lookup"><span data-stu-id="aba9f-108">Definition</span></span>|  
|---|---|  
|`symbol`|<span data-ttu-id="aba9f-109">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="aba9f-109">Required.</span></span> <span data-ttu-id="aba9f-110">Symbol do zdefiniowania.</span><span class="sxs-lookup"><span data-stu-id="aba9f-110">The symbol to define.</span></span>|  
|`value`|<span data-ttu-id="aba9f-111">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="aba9f-111">Optional.</span></span> <span data-ttu-id="aba9f-112">Wartość do przypisania `symbol` .</span><span class="sxs-lookup"><span data-stu-id="aba9f-112">The value to assign `symbol`.</span></span> <span data-ttu-id="aba9f-113">Jeśli `value` jest ciągiem, musi być ujęty w nawiasy odwrotne/sekwencje znaku cudzysłowu ( \\ ") zamiast znaków cudzysłowu.</span><span class="sxs-lookup"><span data-stu-id="aba9f-113">If `value` is a string, it must be surrounded by backslash/quotation-mark sequences (\\") instead of quotation marks.</span></span> <span data-ttu-id="aba9f-114">Jeśli żadna wartość nie zostanie określona, jest ona prawdziwa.</span><span class="sxs-lookup"><span data-stu-id="aba9f-114">If no value is specified, then it is taken to be True.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="aba9f-115">Uwagi</span><span class="sxs-lookup"><span data-stu-id="aba9f-115">Remarks</span></span>  

 <span data-ttu-id="aba9f-116">`-define`Opcja ma podobny efekt jak użycie `#Const` dyrektywy preprocesora w pliku źródłowym, z tą różnicą, że stałe zdefiniowane z `-define` są publiczne i stosowane do wszystkich plików w projekcie.</span><span class="sxs-lookup"><span data-stu-id="aba9f-116">The `-define` option has an effect similar to using a `#Const` preprocessor directive in your source file, except that constants defined with `-define` are public and apply to all files in the project.</span></span>  
  
 <span data-ttu-id="aba9f-117">Możesz użyć symboli utworzonych przez tę opcję z `#If` ... `Then` ...`#Else` dyrektywa w celu warunkowego kompilowania plików źródłowych.</span><span class="sxs-lookup"><span data-stu-id="aba9f-117">You can use symbols created by this option with the `#If`...`Then`...`#Else` directive to compile source files conditionally.</span></span>  
  
 <span data-ttu-id="aba9f-118">`-d` jest krótką formą `-define` .</span><span class="sxs-lookup"><span data-stu-id="aba9f-118">`-d` is the short form of `-define`.</span></span>  
  
 <span data-ttu-id="aba9f-119">Można zdefiniować wiele symboli za pomocą `-define` przecinka do oddzielania definicji symboli.</span><span class="sxs-lookup"><span data-stu-id="aba9f-119">You can define multiple symbols with `-define` by using a comma to separate symbol definitions.</span></span>  
  
|<span data-ttu-id="aba9f-120">Aby ustawić — Zdefiniuj w zintegrowanym środowisku programistycznym programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="aba9f-120">To set -define in the Visual Studio integrated development environment</span></span>|  
|---|  
|<span data-ttu-id="aba9f-121">1. zaznaczono projekt w **Eksplorator rozwiązań**.</span><span class="sxs-lookup"><span data-stu-id="aba9f-121">1.  Have a project selected in **Solution Explorer**.</span></span> <span data-ttu-id="aba9f-122">W menu **projekt** kliknij polecenie **Właściwości**.</span><span class="sxs-lookup"><span data-stu-id="aba9f-122">On the **Project** menu, click **Properties**.</span></span> <br /><span data-ttu-id="aba9f-123">2. Kliknij kartę **kompilacja** .</span><span class="sxs-lookup"><span data-stu-id="aba9f-123">2.  Click the **Compile** tab.</span></span><br /><span data-ttu-id="aba9f-124">3. kliknij pozycję **Zaawansowane**.</span><span class="sxs-lookup"><span data-stu-id="aba9f-124">3.  Click **Advanced**.</span></span><br /><span data-ttu-id="aba9f-125">4. Zmodyfikuj wartość w polu **stałe niestandardowe** .</span><span class="sxs-lookup"><span data-stu-id="aba9f-125">4.  Modify the value in the **Custom Constants** box.</span></span>|  
  
## <a name="example"></a><span data-ttu-id="aba9f-126">Przykład</span><span class="sxs-lookup"><span data-stu-id="aba9f-126">Example</span></span>  

 <span data-ttu-id="aba9f-127">Poniższy kod definiuje, a następnie używa dwóch warunkowych stałych kompilatora.</span><span class="sxs-lookup"><span data-stu-id="aba9f-127">The following code defines and then uses two conditional compiler constants.</span></span>  
  
 [!code-vb[VbVbalrCompiler#45](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCompiler/VB/Class1.vb#45)]  
  
## <a name="see-also"></a><span data-ttu-id="aba9f-128">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="aba9f-128">See also</span></span>

- [<span data-ttu-id="aba9f-129">Kompilator wiersza polecenia Visual Basic</span><span class="sxs-lookup"><span data-stu-id="aba9f-129">Visual Basic Command-Line Compiler</span></span>](index.md)
- [<span data-ttu-id="aba9f-130">#If... Then... #Else — dyrektywy</span><span class="sxs-lookup"><span data-stu-id="aba9f-130">#If...Then...#Else Directives</span></span>](../../language-reference/directives/if-then-else-directives.md)
- [<span data-ttu-id="aba9f-131">#Const — dyrektywa</span><span class="sxs-lookup"><span data-stu-id="aba9f-131">#Const Directive</span></span>](../../language-reference/directives/const-directive.md)
- [<span data-ttu-id="aba9f-132">Przykłady kompilacji — wiersze poleceń</span><span class="sxs-lookup"><span data-stu-id="aba9f-132">Sample Compilation Command Lines</span></span>](sample-compilation-command-lines.md)
