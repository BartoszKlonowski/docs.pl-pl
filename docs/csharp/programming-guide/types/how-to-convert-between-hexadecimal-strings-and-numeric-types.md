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
# <a name="how-to-convert-between-hexadecimal-strings-and-numeric-types-c-programming-guide"></a>Jak przekonwertować ciągi szesnastkowe i typy liczbowe (Przewodnik programowania w języku C#)

W poniższych przykładach pokazano, jak wykonywać następujące zadania:  
  
- Uzyskaj wartość szesnastkową każdego znaku w [ciągu](../../language-reference/builtin-types/reference-types.md).  
  
- Uzyskaj [znak](../../language-reference/builtin-types/char.md) , który odpowiada każdej wartości w ciągu szesnastkowym.  
  
- Konwertuj wartość szesnastkową `string` na [liczbę całkowitą](../../language-reference/builtin-types/integral-numeric-types.md).  
  
- Konwertuj wartość szesnastkową `string` na wartość [zmiennoprzecinkową](../../language-reference/builtin-types/floating-point-numeric-types.md).  
  
- Konwertuj tablicę [bajtów](../../language-reference/builtin-types/integral-numeric-types.md) na wartość szesnastkową `string` .  
  
## <a name="example"></a>Przykład  

 Ten przykład wyprowadza wartość szesnastkową każdego znaku w `string` . Najpierw analizuje on `string` tablicę znaków. Następnie wywołuje <xref:System.Convert.ToInt32%28System.Char%29> każdy znak, aby uzyskać jego wartość liczbową. Na koniec formatuje liczbę jako reprezentację szesnastkową w `string` .  
  
 [!code-csharp[csProgGuideTypes#30](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#30)]  
  
## <a name="example"></a>Przykład  

 Ten przykład analizuje `string` wartości szesnastkowe i wyprowadza znak odpowiadający każdej wartości szesnastkowej. Najpierw wywołuje metodę [Split (Char \[ \] )](xref:System.String.Split(System.Char[])) , aby uzyskać każdą wartość szesnastkową jako pojedynczą `string` w tablicy. Następnie wywołuje <xref:System.Convert.ToInt32%28System.String%2CSystem.Int32%29> , aby przekonwertować wartość szesnastkową na wartość dziesiętną reprezentowaną jako [int](../../language-reference/builtin-types/integral-numeric-types.md). Przedstawiono dwa różne sposoby uzyskania znaku odpowiadającego kodowi tego znaku. Pierwsza technika używa <xref:System.Char.ConvertFromUtf32%28System.Int32%29> , która zwraca znak odpowiadający argumentowi Integer jako `string` . Druga technika jawnie rzutuje na `int` [znak](../../language-reference/builtin-types/char.md).  
  
 [!code-csharp[csProgGuideTypes#31](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#31)]  
  
## <a name="example"></a>Przykład  

 Ten przykład pokazuje inny sposób konwersji szesnastkowej `string` na liczbę całkowitą, wywołując <xref:System.Int32.Parse%28System.String%2CSystem.Globalization.NumberStyles%29> metodę.  
  
 [!code-csharp[csProgGuideTypes#32](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#32)]  
  
## <a name="example"></a>Przykład  

 Poniższy przykład pokazuje, jak konwertować szesnastkowe `string` na [zmiennoprzecinkowe](../../language-reference/builtin-types/floating-point-numeric-types.md) przy użyciu <xref:System.BitConverter?displayProperty=nameWithType> klasy i <xref:System.UInt32.Parse%2A?displayProperty=nameWithType> metody.  
  
 [!code-csharp[csProgGuideTypes#39](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#39)]  
  
## <a name="example"></a>Przykład  

 Poniższy przykład pokazuje, jak skonwertować tablicę [bajtów](../../language-reference/builtin-types/integral-numeric-types.md) na ciąg szesnastkowy przy użyciu <xref:System.BitConverter?displayProperty=nameWithType> klasy.  
  
 [!code-csharp[csProgGuideTypes#38](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#38)]  
  
## <a name="see-also"></a>Zobacz też

- [Standardowe ciągi formatów liczbowych](../../../standard/base-types/standard-numeric-format-strings.md)
- [Typy](./index.md)
- [Określanie, czy ciąg reprezentuje wartość numeryczną](../strings/how-to-determine-whether-a-string-represents-a-numeric-value.md)
