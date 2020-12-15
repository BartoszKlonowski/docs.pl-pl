---
title: Jak przekonwertować ciągi szesnastkowe i typy liczbowe — Przewodnik programowania w języku C#
description: Dowiedz się, jak przekonwertować ciągi szesnastkowe i typy liczbowe. Zobacz przykłady kodu i Wyświetl dodatkowe dostępne zasoby.
ms.date: 07/20/2015
helpviewer_keywords:
- hexadecimal strings [C#], converting to numeric type
- conversions [C#], hexidecimal strings
- strings [C#], converting hexadecimal strings
- hexadecimal strings [C#]
ms.topic: how-to
ms.custom: contperf-fy21q2
ms.assetid: 7115c49f-7d1d-40c3-8bd9-aae0cc1d46b6
ms.openlocfilehash: 18021156af879f324993beca04531c8a822725db
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2020
ms.locfileid: "97513240"
---
# <a name="how-to-convert-between-hexadecimal-strings-and-numeric-types-c-programming-guide"></a><span data-ttu-id="a5d8d-104">Jak przekonwertować ciągi szesnastkowe i typy liczbowe (Przewodnik programowania w języku C#)</span><span class="sxs-lookup"><span data-stu-id="a5d8d-104">How to convert between hexadecimal strings and numeric types (C# Programming Guide)</span></span>

<span data-ttu-id="a5d8d-105">W poniższych przykładach pokazano, jak wykonywać następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="a5d8d-105">These examples show you how to perform the following tasks:</span></span>  
  
- <span data-ttu-id="a5d8d-106">Uzyskaj wartość szesnastkową każdego znaku w [ciągu](../../language-reference/builtin-types/reference-types.md).</span><span class="sxs-lookup"><span data-stu-id="a5d8d-106">Obtain the hexadecimal value of each character in a [string](../../language-reference/builtin-types/reference-types.md).</span></span>  
  
- <span data-ttu-id="a5d8d-107">Uzyskaj [znak](../../language-reference/builtin-types/char.md) , który odpowiada każdej wartości w ciągu szesnastkowym.</span><span class="sxs-lookup"><span data-stu-id="a5d8d-107">Obtain the [char](../../language-reference/builtin-types/char.md) that corresponds to each value in a hexadecimal string.</span></span>  
  
- <span data-ttu-id="a5d8d-108">Konwertuj wartość szesnastkową `string` na [liczbę całkowitą](../../language-reference/builtin-types/integral-numeric-types.md).</span><span class="sxs-lookup"><span data-stu-id="a5d8d-108">Convert a hexadecimal `string` to an [int](../../language-reference/builtin-types/integral-numeric-types.md).</span></span>  
  
- <span data-ttu-id="a5d8d-109">Konwertuj wartość szesnastkową `string` na wartość [zmiennoprzecinkową](../../language-reference/builtin-types/floating-point-numeric-types.md).</span><span class="sxs-lookup"><span data-stu-id="a5d8d-109">Convert a hexadecimal `string` to a [float](../../language-reference/builtin-types/floating-point-numeric-types.md).</span></span>  
  
- <span data-ttu-id="a5d8d-110">Konwertuj tablicę [bajtów](../../language-reference/builtin-types/integral-numeric-types.md) na wartość szesnastkową `string` .</span><span class="sxs-lookup"><span data-stu-id="a5d8d-110">Convert a [byte](../../language-reference/builtin-types/integral-numeric-types.md) array to a hexadecimal `string`.</span></span>  
  
## <a name="example"></a><span data-ttu-id="a5d8d-111">Przykład</span><span class="sxs-lookup"><span data-stu-id="a5d8d-111">Example</span></span>  

 <span data-ttu-id="a5d8d-112">Ten przykład wyprowadza wartość szesnastkową każdego znaku w `string` .</span><span class="sxs-lookup"><span data-stu-id="a5d8d-112">This example outputs the hexadecimal value of each character in a `string`.</span></span> <span data-ttu-id="a5d8d-113">Najpierw analizuje on `string` tablicę znaków.</span><span class="sxs-lookup"><span data-stu-id="a5d8d-113">First it parses the `string` to an array of characters.</span></span> <span data-ttu-id="a5d8d-114">Następnie wywołuje <xref:System.Convert.ToInt32%28System.Char%29> każdy znak, aby uzyskać jego wartość liczbową.</span><span class="sxs-lookup"><span data-stu-id="a5d8d-114">Then it calls <xref:System.Convert.ToInt32%28System.Char%29> on each character to obtain its numeric value.</span></span> <span data-ttu-id="a5d8d-115">Na koniec formatuje liczbę jako reprezentację szesnastkową w `string` .</span><span class="sxs-lookup"><span data-stu-id="a5d8d-115">Finally, it formats the number as its hexadecimal representation in a `string`.</span></span>  
  
 [!code-csharp[csProgGuideTypes#30](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#30)]  
  
## <a name="example"></a><span data-ttu-id="a5d8d-116">Przykład</span><span class="sxs-lookup"><span data-stu-id="a5d8d-116">Example</span></span>  

 <span data-ttu-id="a5d8d-117">Ten przykład analizuje `string` wartości szesnastkowe i wyprowadza znak odpowiadający każdej wartości szesnastkowej.</span><span class="sxs-lookup"><span data-stu-id="a5d8d-117">This example parses a `string` of hexadecimal values and outputs the character corresponding to each hexadecimal value.</span></span> <span data-ttu-id="a5d8d-118">Najpierw wywołuje metodę [Split (Char \[ \] )](xref:System.String.Split(System.Char[])) , aby uzyskać każdą wartość szesnastkową jako pojedynczą `string` w tablicy.</span><span class="sxs-lookup"><span data-stu-id="a5d8d-118">First it calls the [Split(Char\[\])](xref:System.String.Split(System.Char[])) method to obtain each hexadecimal value as an individual `string` in an array.</span></span> <span data-ttu-id="a5d8d-119">Następnie wywołuje <xref:System.Convert.ToInt32%28System.String%2CSystem.Int32%29> , aby przekonwertować wartość szesnastkową na wartość dziesiętną reprezentowaną jako [int](../../language-reference/builtin-types/integral-numeric-types.md). Przedstawiono dwa różne sposoby uzyskania znaku odpowiadającego kodowi tego znaku.</span><span class="sxs-lookup"><span data-stu-id="a5d8d-119">Then it calls <xref:System.Convert.ToInt32%28System.String%2CSystem.Int32%29> to convert the hexadecimal value to a decimal value represented as an [int](../../language-reference/builtin-types/integral-numeric-types.md). It shows two different ways to obtain the character corresponding to that character code.</span></span> <span data-ttu-id="a5d8d-120">Pierwsza technika używa <xref:System.Char.ConvertFromUtf32%28System.Int32%29> , która zwraca znak odpowiadający argumentowi Integer jako `string` .</span><span class="sxs-lookup"><span data-stu-id="a5d8d-120">The first technique uses <xref:System.Char.ConvertFromUtf32%28System.Int32%29>, which returns the character corresponding to the integer argument as a `string`.</span></span> <span data-ttu-id="a5d8d-121">Druga technika jawnie rzutuje na `int` [znak](../../language-reference/builtin-types/char.md).</span><span class="sxs-lookup"><span data-stu-id="a5d8d-121">The second technique explicitly casts the `int` to a [char](../../language-reference/builtin-types/char.md).</span></span>  
  
 [!code-csharp[csProgGuideTypes#31](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#31)]  
  
## <a name="example"></a><span data-ttu-id="a5d8d-122">Przykład</span><span class="sxs-lookup"><span data-stu-id="a5d8d-122">Example</span></span>  

 <span data-ttu-id="a5d8d-123">Ten przykład pokazuje inny sposób konwersji szesnastkowej `string` na liczbę całkowitą, wywołując <xref:System.Int32.Parse%28System.String%2CSystem.Globalization.NumberStyles%29> metodę.</span><span class="sxs-lookup"><span data-stu-id="a5d8d-123">This example shows another way to convert a hexadecimal `string` to an integer, by calling the <xref:System.Int32.Parse%28System.String%2CSystem.Globalization.NumberStyles%29> method.</span></span>  
  
 [!code-csharp[csProgGuideTypes#32](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#32)]  
  
## <a name="example"></a><span data-ttu-id="a5d8d-124">Przykład</span><span class="sxs-lookup"><span data-stu-id="a5d8d-124">Example</span></span>  

 <span data-ttu-id="a5d8d-125">Poniższy przykład pokazuje, jak konwertować szesnastkowe `string` na [zmiennoprzecinkowe](../../language-reference/builtin-types/floating-point-numeric-types.md) przy użyciu <xref:System.BitConverter?displayProperty=nameWithType> klasy i <xref:System.UInt32.Parse%2A?displayProperty=nameWithType> metody.</span><span class="sxs-lookup"><span data-stu-id="a5d8d-125">The following example shows how to convert a hexadecimal `string` to a [float](../../language-reference/builtin-types/floating-point-numeric-types.md) by using the <xref:System.BitConverter?displayProperty=nameWithType> class and the <xref:System.UInt32.Parse%2A?displayProperty=nameWithType> method.</span></span>  
  
 [!code-csharp[csProgGuideTypes#39](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#39)]  
  
## <a name="example"></a><span data-ttu-id="a5d8d-126">Przykład</span><span class="sxs-lookup"><span data-stu-id="a5d8d-126">Example</span></span>  

 <span data-ttu-id="a5d8d-127">Poniższy przykład pokazuje, jak skonwertować tablicę [bajtów](../../language-reference/builtin-types/integral-numeric-types.md) na ciąg szesnastkowy przy użyciu <xref:System.BitConverter?displayProperty=nameWithType> klasy.</span><span class="sxs-lookup"><span data-stu-id="a5d8d-127">The following example shows how to convert a [byte](../../language-reference/builtin-types/integral-numeric-types.md) array to a hexadecimal string by using the <xref:System.BitConverter?displayProperty=nameWithType> class.</span></span>  
  
 [!code-csharp[csProgGuideTypes#38](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#38)]  
  
## <a name="see-also"></a><span data-ttu-id="a5d8d-128">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="a5d8d-128">See also</span></span>

- [<span data-ttu-id="a5d8d-129">Standardowe ciągi formatów liczbowych</span><span class="sxs-lookup"><span data-stu-id="a5d8d-129">Standard Numeric Format Strings</span></span>](../../../standard/base-types/standard-numeric-format-strings.md)
- [<span data-ttu-id="a5d8d-130">Typy</span><span class="sxs-lookup"><span data-stu-id="a5d8d-130">Types</span></span>](./index.md)
- [<span data-ttu-id="a5d8d-131">Określanie, czy ciąg reprezentuje wartość numeryczną</span><span class="sxs-lookup"><span data-stu-id="a5d8d-131">How to determine whether a string represents a numeric value</span></span>](../strings/how-to-determine-whether-a-string-represents-a-numeric-value.md)
