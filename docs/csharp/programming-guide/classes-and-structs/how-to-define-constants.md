---
title: 'Porada: definiowanie stałych w języku C#'
description: Dowiedz się, jak definiować stałe w języku C#, które są polami, których wartości są ustawiane w czasie kompilacji. Użyj stałych, aby podać znaczące nazwy dla specjalnych wartości.
ms.date: 07/20/2015
helpviewer_keywords:
- C# language, constants
- constants [C#]
ms.topic: how-to
ms.custom: contperf-fy21q2
ms.assetid: 43f511be-346c-4b8a-995e-aded94542ece
ms.openlocfilehash: 972deaa4616c15c00e83e26891c4473eae7bfcf8
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2020
ms.locfileid: "97513058"
---
# <a name="how-to-define-constants-in-c"></a><span data-ttu-id="fb8b1-104">Jak definiować stałe w języku C\#</span><span class="sxs-lookup"><span data-stu-id="fb8b1-104">How to define constants in C\#</span></span>

<span data-ttu-id="fb8b1-105">Stałe są polami, których wartości są ustawiane w czasie kompilacji i nigdy nie mogą być zmieniane.</span><span class="sxs-lookup"><span data-stu-id="fb8b1-105">Constants are fields whose values are set at compile time and can never be changed.</span></span> <span data-ttu-id="fb8b1-106">Użyj stałych, aby podać znaczące nazwy zamiast literałów liczbowych ("liczby magiczne") dla specjalnych wartości.</span><span class="sxs-lookup"><span data-stu-id="fb8b1-106">Use constants to provide meaningful names instead of numeric literals ("magic numbers") for special values.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="fb8b1-107">W języku C# dyrektywa preprocesora [#define](../../language-reference/preprocessor-directives/preprocessor-define.md) nie może służyć do definiowania stałych w sposób, który jest zazwyczaj używany w C i C++.</span><span class="sxs-lookup"><span data-stu-id="fb8b1-107">In C# the [#define](../../language-reference/preprocessor-directives/preprocessor-define.md) preprocessor directive cannot be used to define constants in the way that is typically used in C and C++.</span></span>  
  
 <span data-ttu-id="fb8b1-108">Aby zdefiniować stałe wartości typów całkowitych ( `int` , `byte` , i tak dalej), użyj typu wyliczeniowego.</span><span class="sxs-lookup"><span data-stu-id="fb8b1-108">To define constant values of integral types (`int`, `byte`, and so on) use an enumerated type.</span></span> <span data-ttu-id="fb8b1-109">Aby uzyskać więcej informacji, zobacz [Wyliczenie](../../language-reference/builtin-types/enum.md).</span><span class="sxs-lookup"><span data-stu-id="fb8b1-109">For more information, see [enum](../../language-reference/builtin-types/enum.md).</span></span>  
  
 <span data-ttu-id="fb8b1-110">Aby zdefiniować niecałkowite stałe, jedno podejście polega na pogrupowania ich w pojedynczej klasie statycznej o nazwie `Constants` .</span><span class="sxs-lookup"><span data-stu-id="fb8b1-110">To define non-integral constants, one approach is to group them in a single static class named `Constants`.</span></span> <span data-ttu-id="fb8b1-111">To wymaga, aby wszystkie odwołania do stałych były poprzedzone nazwą klasy, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="fb8b1-111">This will require that all references to the constants be prefaced with the class name, as shown in the following example.</span></span>  
  
## <a name="example"></a><span data-ttu-id="fb8b1-112">Przykład</span><span class="sxs-lookup"><span data-stu-id="fb8b1-112">Example</span></span>  

 [!code-csharp[csProgGuideObjects#89](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#89)]  
  
 <span data-ttu-id="fb8b1-113">Użycie kwalifikatora nazwy klasy pomaga upewnić się, że i inne osoby, które używają stałej, wiedzą, że jest stała i nie mogą być modyfikowane.</span><span class="sxs-lookup"><span data-stu-id="fb8b1-113">The use of the class name qualifier helps ensure that you and others who use the constant understand that it is constant and cannot be modified.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="fb8b1-114">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="fb8b1-114">See also</span></span>

- [<span data-ttu-id="fb8b1-115">Klasy i struktury</span><span class="sxs-lookup"><span data-stu-id="fb8b1-115">Classes and Structs</span></span>](./index.md)
