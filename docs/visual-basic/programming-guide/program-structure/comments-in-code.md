---
title: Komentarze w kodzie
ms.date: 07/20/2015
helpviewer_keywords:
- Uncomment button
- REM statement [Visual Basic]
- comments [Visual Basic], in code
- comments [Visual Basic], Visual Basic code
- Comment button
- buttons [Visual Basic], Uncomment
- buttons [Visual Basic], Comment
- code comments [Visual Basic], Visual Basic
- Visual Basic code, comments
- comments
- code comments
ms.assetid: 90136fba-22eb-49f9-ba81-63db629b4a47
ms.openlocfilehash: b0077bdae3bad1d67c3d26e503d05f318982eb80
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/23/2020
ms.locfileid: "91099024"
---
# <a name="comments-in-code-visual-basic"></a><span data-ttu-id="1e953-102">Komentarze w kodzie (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="1e953-102">Comments in Code (Visual Basic)</span></span>

<span data-ttu-id="1e953-103">Podczas odczytywania przykładów kodu często występuje symbol komentarza ( `'` ).</span><span class="sxs-lookup"><span data-stu-id="1e953-103">As you read the code examples, you often encounter the comment symbol (`'`).</span></span> <span data-ttu-id="1e953-104">Ten symbol nakazuje kompilatorowi Visual Basic ignorowanie tekstu po nim lub *komentarz*.</span><span class="sxs-lookup"><span data-stu-id="1e953-104">This symbol tells the Visual Basic compiler to ignore the text following it, or the *comment*.</span></span> <span data-ttu-id="1e953-105">Komentarze to krótkie notatki wyjaśniające, dodane do kodu, aby ułatwić życie innym osobom, które go czytają.</span><span class="sxs-lookup"><span data-stu-id="1e953-105">Comments are brief explanatory notes added to code for the benefit of those reading it.</span></span>  
  
 <span data-ttu-id="1e953-106">Dobrą praktyką programowania jest rozpoczynanie wszystkich procedur od krótkiego komentarza, który opisuje charakterystykę funkcjonalną procedury (co dana procedura robi).</span><span class="sxs-lookup"><span data-stu-id="1e953-106">It is good programming practice to begin all procedures with a brief comment describing the functional characteristics of the procedure (what it does).</span></span> <span data-ttu-id="1e953-107">Korzysta z tego i sam programista, i wszyscy inni, którzy czytają kod.</span><span class="sxs-lookup"><span data-stu-id="1e953-107">This is for your own benefit and the benefit of anyone else who examines the code.</span></span> <span data-ttu-id="1e953-108">Szczegóły dotyczące implementacji (jak procedura coś robi) należy oddzielić od komentarzy opisujących charakterystyki funkcjonalne.</span><span class="sxs-lookup"><span data-stu-id="1e953-108">You should separate the implementation details (how the procedure does it) from comments that describe the functional characteristics.</span></span> <span data-ttu-id="1e953-109">Gdy w opisie dołączasz szczegóły dotyczące implementacji, pamiętaj, aby je zaktualizować, gdy aktualizujesz funkcję.</span><span class="sxs-lookup"><span data-stu-id="1e953-109">When you include implementation details in the description, remember to update them when you update the function.</span></span>  
  
 <span data-ttu-id="1e953-110">Komentarze mogą następować po instrukcji w tym samym wierszu lub zajmować cały wiersz.</span><span class="sxs-lookup"><span data-stu-id="1e953-110">Comments can follow a statement on the same line, or occupy an entire line.</span></span> <span data-ttu-id="1e953-111">Poniższy kod ilustruje obie wersje.</span><span class="sxs-lookup"><span data-stu-id="1e953-111">Both are illustrated in the following code.</span></span>  
  
 [!code-vb[VbVbcnConventions#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnConventions/VB/Class1.vb#16)]  
  
 <span data-ttu-id="1e953-112">Jeśli komentarz wymaga więcej niż jednego wiersza, należy użyć symbolu komentarza w każdym wierszu, jak pokazuje poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="1e953-112">If your comment requires more than one line, use the comment symbol on each line, as the following example illustrates.</span></span>  
  
 [!code-vb[VbVbcnConventions#17](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnConventions/VB/Class1.vb#17)]  
  
## <a name="commenting-guidelines"></a><span data-ttu-id="1e953-113">Wytyczne komentowania</span><span class="sxs-lookup"><span data-stu-id="1e953-113">Commenting Guidelines</span></span>  

 <span data-ttu-id="1e953-114">Poniższa tabela zawiera ogólne wytyczne na temat tego, jakie rodzaje komentarzy mogą poprzedzać sekcję kodu.</span><span class="sxs-lookup"><span data-stu-id="1e953-114">The following table provides general guidelines for what types of comments can precede a section of code.</span></span> <span data-ttu-id="1e953-115">Są to sugestie: Visual Basic nie wymusza reguł dodawania komentarzy.</span><span class="sxs-lookup"><span data-stu-id="1e953-115">These are suggestions; Visual Basic does not enforce rules for adding comments.</span></span> <span data-ttu-id="1e953-116">Pisz to, co się najlepiej sprawdza, zarówno dla ciebie, jak i dla każdego, kto czyta twój kod.</span><span class="sxs-lookup"><span data-stu-id="1e953-116">Write what works best, both for you and for anyone else who reads your code.</span></span>  
  
|||  
|---|---|  
|<span data-ttu-id="1e953-117">Typ komentarza</span><span class="sxs-lookup"><span data-stu-id="1e953-117">Comment type</span></span>|<span data-ttu-id="1e953-118">Opis komentarza</span><span class="sxs-lookup"><span data-stu-id="1e953-118">Comment description</span></span>|  
|<span data-ttu-id="1e953-119">Przeznaczenie</span><span class="sxs-lookup"><span data-stu-id="1e953-119">Purpose</span></span>|<span data-ttu-id="1e953-120">Opisuje, co procedura robi (a nie jak to robi)</span><span class="sxs-lookup"><span data-stu-id="1e953-120">Describes what the procedure does (not how it does it)</span></span>|  
|<span data-ttu-id="1e953-121">Założenia</span><span class="sxs-lookup"><span data-stu-id="1e953-121">Assumptions</span></span>|<span data-ttu-id="1e953-122">Wymienia każdą zewnętrzną zmienną, element sterujący, otwarty plik lub inny element, do którego procedura uzyskuje dostęp</span><span class="sxs-lookup"><span data-stu-id="1e953-122">Lists each external variable, control, open file, or other element accessed by the procedure</span></span>|  
|<span data-ttu-id="1e953-123">Efekty</span><span class="sxs-lookup"><span data-stu-id="1e953-123">Effects</span></span>|<span data-ttu-id="1e953-124">Wymienia każdą zewnętrzną zmienną, element sterowania lub plik i efekt, jaki wywołuje (tylko jeśli nie jest on oczywisty)</span><span class="sxs-lookup"><span data-stu-id="1e953-124">Lists each affected external variable, control, or file, and the effect it has (only if it is not obvious)</span></span>|  
|<span data-ttu-id="1e953-125">Dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="1e953-125">Inputs</span></span>|<span data-ttu-id="1e953-126">Określa cel argumentu</span><span class="sxs-lookup"><span data-stu-id="1e953-126">Specifies the purpose of the argument</span></span>|  
|<span data-ttu-id="1e953-127">Zwraca</span><span class="sxs-lookup"><span data-stu-id="1e953-127">Returns</span></span>|<span data-ttu-id="1e953-128">Wyjaśnia wartości zwrócone przez procedurę</span><span class="sxs-lookup"><span data-stu-id="1e953-128">Explains the values returned by the procedure</span></span>|  
  
 <span data-ttu-id="1e953-129">Należy pamiętać o następujących kwestiach:</span><span class="sxs-lookup"><span data-stu-id="1e953-129">Remember the following points:</span></span>  
  
- <span data-ttu-id="1e953-130">Każda ważna deklaracja zmiennej powinna być poprzedzona komentarzem opisującym użycie deklarowanej zmiennej.</span><span class="sxs-lookup"><span data-stu-id="1e953-130">Every important variable declaration should be preceded by a comment describing the use of the variable being declared.</span></span>  
  
- <span data-ttu-id="1e953-131">Zmienne, elementy sterujące i procedury powinno się nazywać na tyle jasno, żeby komentowanie było konieczne tylko w przypadku szczegółów złożonych implementacji.</span><span class="sxs-lookup"><span data-stu-id="1e953-131">Variables, controls, and procedures should be named clearly enough that commenting is needed only for complex implementation details.</span></span>  
  
- <span data-ttu-id="1e953-132">Komentarze nie mogą występować w tym samym wierszu, jeśli jest on kontynuowany w następnym.</span><span class="sxs-lookup"><span data-stu-id="1e953-132">Comments cannot follow a line-continuation sequence on the same line.</span></span>  
  
 <span data-ttu-id="1e953-133">Możesz dodawać lub usuwać symbole komentarzy dla bloku kodu, zaznaczając jeden lub więcej wierszy kodu i wybierając **komentarz** ( ![ przycisk Visual Basic komentarza w programie Visual Studio ](./media/comments-in-code/visual-basic-comment-button.gif) ) i usuwając **komentarz** ( ![ przycisk Visual Basic Usuń komentarz w programie Visual Studio. ](./media/comments-in-code/visual-basic-uncomment-button.gif) ) na pasku narzędzi **Edycja** .</span><span class="sxs-lookup"><span data-stu-id="1e953-133">You can add or remove comment symbols for a block of code by selecting one or more lines of code and choosing the **Comment** (![The Visual Basic Comment button in Visual Studio.](./media/comments-in-code/visual-basic-comment-button.gif)) and **Uncomment** (![The Visual Basic Uncomment button in Visual Studio.](./media/comments-in-code/visual-basic-uncomment-button.gif)) buttons on the **Edit** toolbar.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="1e953-134">Możesz również dodać komentarze do kodu, poprzedzając tekst `REM` słowem kluczowym.</span><span class="sxs-lookup"><span data-stu-id="1e953-134">You can also add comments to your code by preceding the text with the `REM` keyword.</span></span> <span data-ttu-id="1e953-135">Jednak `'` symbole i **Komentarze komentarzy** / **Uncomment** są łatwiejsze do użycia i wymagają mniej miejsca i pamięci.</span><span class="sxs-lookup"><span data-stu-id="1e953-135">However, the `'` symbol and the **Comment**/**Uncomment** buttons are easier to use and require less space and memory.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="1e953-136">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="1e953-136">See also</span></span>

- [<span data-ttu-id="1e953-137">Podstawowe intuicji — dokumentowanie kodu z komentarzami XML</span><span class="sxs-lookup"><span data-stu-id="1e953-137">Basic Instincts - Documenting Your Code With XML Comments</span></span>](/archive/msdn-magazine/2009/may/documenting-your-code-with-xml-comments)
- [<span data-ttu-id="1e953-138">Instrukcje: tworzenie dokumentacji XML</span><span class="sxs-lookup"><span data-stu-id="1e953-138">How to: Create XML Documentation</span></span>](how-to-create-xml-documentation.md)
- [<span data-ttu-id="1e953-139">Tagi komentarza XML</span><span class="sxs-lookup"><span data-stu-id="1e953-139">XML Comment Tags</span></span>](../../language-reference/xmldoc/index.md)
- [<span data-ttu-id="1e953-140">Struktura programu i konwencje związane z kodem</span><span class="sxs-lookup"><span data-stu-id="1e953-140">Program Structure and Code Conventions</span></span>](program-structure-and-code-conventions.md)
- [<span data-ttu-id="1e953-141">REM, instrukcja</span><span class="sxs-lookup"><span data-stu-id="1e953-141">REM Statement</span></span>](../../language-reference/statements/rem-statement.md)
