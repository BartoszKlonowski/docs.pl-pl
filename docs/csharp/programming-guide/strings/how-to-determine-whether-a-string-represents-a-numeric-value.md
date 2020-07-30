---
title: Jak określić, czy ciąg reprezentuje wartość liczbową — Przewodnik programowania w języku C#
description: Dowiedz się, jak ustalić, czy ciąg jest prawidłową reprezentacją określonego typu liczbowego. Zobacz przykłady kodu i wyświetlaj dodatkowe zasoby.
ms.date: 07/20/2015
helpviewer_keywords:
- numeric strings [C#]
- validating numeric input [C#]
- strings [C#], numeric
ms.assetid: a4e84e10-ea0a-489f-a868-503dded9d85f
ms.openlocfilehash: c248c6c54de493ab06a833fc525252fa812d60da
ms.sourcegitcommit: 552b4b60c094559db9d8178fa74f5bafaece0caf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/29/2020
ms.locfileid: "87381752"
---
# <a name="how-to-determine-whether-a-string-represents-a-numeric-value-c-programming-guide"></a><span data-ttu-id="270e6-104">Jak określić, czy ciąg reprezentuje wartość liczbową (Przewodnik programowania w języku C#)</span><span class="sxs-lookup"><span data-stu-id="270e6-104">How to determine whether a string represents a numeric value (C# Programming Guide)</span></span>
<span data-ttu-id="270e6-105">Aby określić, czy ciąg jest prawidłową reprezentacją określonego typu liczbowego, należy użyć statycznej `TryParse` metody, która jest implementowana przez wszystkie pierwotne typy liczbowe, a także typy takie jak <xref:System.DateTime> i <xref:System.Net.IPAddress> .</span><span class="sxs-lookup"><span data-stu-id="270e6-105">To determine whether a string is a valid representation of a specified numeric type, use the static `TryParse` method that is implemented by all primitive numeric types and also by types such as <xref:System.DateTime> and <xref:System.Net.IPAddress>.</span></span> <span data-ttu-id="270e6-106">Poniższy przykład pokazuje, jak ustalić, czy "108" jest prawidłową [int](../../language-reference/builtin-types/integral-numeric-types.md).</span><span class="sxs-lookup"><span data-stu-id="270e6-106">The following example shows how to determine whether "108" is a valid [int](../../language-reference/builtin-types/integral-numeric-types.md).</span></span>  
  
```csharp  
int i = 0;
string s = "108";  
bool result = int.TryParse(s, out i); //i now = 108  
```  
  
 <span data-ttu-id="270e6-107">Jeśli ciąg zawiera znaki nienumeryczne lub wartość liczbowa jest za duża lub za mała dla określonego typu, `TryParse` zwraca wartość false i ustawia parametr out na wartość zero.</span><span class="sxs-lookup"><span data-stu-id="270e6-107">If the string contains nonnumeric characters or the numeric value is too large or too small for the particular type you have specified, `TryParse` returns false and sets the out parameter to zero.</span></span> <span data-ttu-id="270e6-108">W przeciwnym razie zwraca wartość true i ustawia parametr out na wartość liczbową ciągu.</span><span class="sxs-lookup"><span data-stu-id="270e6-108">Otherwise, it returns true and sets the out parameter to the numeric value of the string.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="270e6-109">Ciąg może zawierać tylko znaki numeryczne i nadal nie jest prawidłowy dla typu, którego `TryParse` Metoda jest używana.</span><span class="sxs-lookup"><span data-stu-id="270e6-109">A string may contain only numeric characters and still not be valid for the type whose `TryParse` method that you use.</span></span> <span data-ttu-id="270e6-110">Na przykład "256" nie jest prawidłową wartością dla `byte` , ale jest prawidłowy dla `int` .</span><span class="sxs-lookup"><span data-stu-id="270e6-110">For example, "256" is not a valid value for `byte` but it is valid for `int`.</span></span> <span data-ttu-id="270e6-111">"98,6" nie jest prawidłową wartością dla `int` , ale jest prawidłowy `decimal` .</span><span class="sxs-lookup"><span data-stu-id="270e6-111">"98.6" is not a valid value for `int` but it is a valid `decimal`.</span></span>  
  
## <a name="example"></a><span data-ttu-id="270e6-112">Przykład</span><span class="sxs-lookup"><span data-stu-id="270e6-112">Example</span></span>  
 <span data-ttu-id="270e6-113">W poniższych przykładach pokazano, jak używać `TryParse` z reprezentacjami ciągów `long` `byte` wartości,, i `decimal` .</span><span class="sxs-lookup"><span data-stu-id="270e6-113">The following examples show how to use `TryParse` with string representations of `long`, `byte`, and `decimal` values.</span></span>  
  
 [!code-csharp[csProgGuideStrings#14](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStrings/CS/Strings.cs#14)]  
  
## <a name="robust-programming"></a><span data-ttu-id="270e6-114">Niezawodne programowanie</span><span class="sxs-lookup"><span data-stu-id="270e6-114">Robust Programming</span></span>  
 <span data-ttu-id="270e6-115">Pierwotne typy liczbowe implementują również `Parse` metodę statyczną, która zgłasza wyjątek, jeśli ciąg nie jest prawidłową liczbą.</span><span class="sxs-lookup"><span data-stu-id="270e6-115">Primitive numeric types also implement the `Parse` static method, which throws an exception if the string is not a valid number.</span></span> <span data-ttu-id="270e6-116">`TryParse`jest zwykle bardziej wydajne, ponieważ zwraca wartość false, jeśli liczba jest nieprawidłowa.</span><span class="sxs-lookup"><span data-stu-id="270e6-116">`TryParse` is generally more efficient because it just returns false if the number is not valid.</span></span>  
  
## <a name="net-security"></a><span data-ttu-id="270e6-117">Zabezpieczenia platformy .NET</span><span class="sxs-lookup"><span data-stu-id="270e6-117">.NET Security</span></span>  
 <span data-ttu-id="270e6-118">Zawsze używaj `TryParse` metod lub `Parse` do sprawdzania poprawności danych wejściowych użytkownika z kontrolek, takich jak pola tekstowe i pola kombi.</span><span class="sxs-lookup"><span data-stu-id="270e6-118">Always use the `TryParse` or `Parse` methods to validate user input from controls such as text boxes and combo boxes.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="270e6-119">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="270e6-119">See also</span></span>

- [<span data-ttu-id="270e6-120">Konwertowanie tablicy typu Byte na liczbę całkowitą</span><span class="sxs-lookup"><span data-stu-id="270e6-120">How to convert a byte array to an int</span></span>](../types/how-to-convert-a-byte-array-to-an-int.md)
- [<span data-ttu-id="270e6-121">Konwertowanie ciągu na liczbę</span><span class="sxs-lookup"><span data-stu-id="270e6-121">How to convert a string to a number</span></span>](../types/how-to-convert-a-string-to-a-number.md)
- [<span data-ttu-id="270e6-122">Konwertowanie ciągów szesnastkowych na typy liczbowe</span><span class="sxs-lookup"><span data-stu-id="270e6-122">How to convert between hexadecimal strings and numeric types</span></span>](../types/how-to-convert-between-hexadecimal-strings-and-numeric-types.md)
- [<span data-ttu-id="270e6-123">Analizowanie ciągów liczbowych</span><span class="sxs-lookup"><span data-stu-id="270e6-123">Parsing Numeric Strings</span></span>](../../../standard/base-types/parsing-numeric.md)
- [<span data-ttu-id="270e6-124">Formatowanie typów</span><span class="sxs-lookup"><span data-stu-id="270e6-124">Formatting Types</span></span>](../../../standard/base-types/formatting-types.md)
