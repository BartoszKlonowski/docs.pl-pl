---
title: Jak przekonwertować ciąg na Przewodnik programowania w języku C#
ms.date: 02/11/2019
helpviewer_keywords:
- conversions [C#]
- conversions [C#], string to int
- converting strings to int [C#]
- strings [C#], converting to int
ms.assetid: 467b9979-86ee-4afd-b734-30299cda91e3
ms.openlocfilehash: f1d4a0f36292acafad409bf666f861b7637cd644
ms.sourcegitcommit: 7b1497c1927cb449cefd313bc5126ae37df30746
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/16/2020
ms.locfileid: "83442205"
---
# <a name="how-to-convert-a-string-to-a-number-c-programming-guide"></a>Konwertowanie ciągu na liczbę (Przewodnik programowania w języku C#)

Można przekonwertować [ciąg](../../language-reference/builtin-types/reference-types.md) na liczbę poprzez wywołanie `Parse` metody lub w `TryParse` różnych typach liczbowych ( `int` ,, `long` `double` itp.) lub przy użyciu metod w <xref:System.Convert?displayProperty=nameWithType> klasie.  
  
 Jeśli masz ciąg, jest nieco bardziej wydajny i nieskomplikowany do wywołania `TryParse` metody (na przykład [`int.TryParse("11", out number)`](xref:System.Int32.TryParse%2A) ) lub `Parse` metody (na przykład [`var number = int.Parse("11")`](xref:System.Int32.Parse%2A) ).  Użycie <xref:System.Convert> metody jest bardziej przydatne w przypadku ogólnych obiektów, które implementują <xref:System.IConvertible> .  
  
 Można użyć `Parse` lub `TryParse` metod dla typu liczbowego, który powinien zawierać ciąg, na przykład <xref:System.Int32?displayProperty=nameWithType> Typ.  <xref:System.Convert.ToInt32%2A?displayProperty=nameWithType>Metoda używa <xref:System.Int32.Parse%2A> wewnętrznie.  `Parse`Metoda zwraca przekonwertowaną liczbę; `TryParse` Metoda zwraca <xref:System.Boolean> wartość wskazującą, czy konwersja powiodła się, i zwraca przekonwertowaną liczbę w [ `out` parametrze](../../language-reference/keywords/out.md). Jeśli ciąg jest w nieprawidłowym formacie, `Parse` zgłasza wyjątek, a `TryParse` zwraca `false` . Podczas wywoływania `Parse` metody należy zawsze używać obsługi wyjątków, aby przechwytywać <xref:System.FormatException> w przypadku niepowodzenia operacji analizy.  
  
## <a name="calling-the-parse-and-tryparse-methods"></a>Wywoływanie metod Parse i TryParse

`Parse`Metody i `TryParse` ignorują odstęp na początku i na końcu ciągu, ale wszystkie inne znaki muszą być znakami, które tworzą odpowiedni typ liczbowy (,,,, `int` `long` `ulong` `float` `decimal` itd.).  Dowolny biały znak w ciągu, który tworzy liczbę, powoduje błąd.  Na przykład można użyć, `decimal.TryParse` Aby przeanalizować wartość "10", "10,3" lub "10", ale nie można użyć tej metody do przeanalizowania 10 z "10X", "1 0" (zanotować przestrzeń osadzoną), "10 .3" (zanotuj przestrzeń osadzoną), "10e1" ( `float.TryParse` działa tutaj) i tak dalej. Ponadto ciąg, którego wartość jest `null` lub <xref:System.String.Empty?displayProperty=nameWithType> nie można przeanalizować pomyślnie. Przed próbą przeanalizowania można sprawdzić, czy ciąg ma wartość null lub być pusty, wywołując <xref:System.String.IsNullOrEmpty%2A?displayProperty=nameWithType> metodę.

W poniższym przykładzie pokazano zarówno udane, jak i nieudane wywołania do `Parse` i `TryParse` .  
  
[!code-csharp[Parse and TryParse](~/samples/snippets/csharp/programming-guide/string-to-number/parse-tryparse/program.cs)]  

Poniższy przykład ilustruje jedno podejście do analizy ciągu, który powinien zawierać wiodące znaki numeryczne (w tym znaki szesnastkowe) i końcowe znaki niebędące numeryczne. Przypisuje prawidłowe znaki od początku ciągu do nowego ciągu przed wywołaniem <xref:System.Int32.TryParse%2A> metody. Ponieważ ciągi, które mają być analizowane, zawierają niewielką liczbę znaków, przykład wywołuje metodę, <xref:System.String.Concat%2A?displayProperty=nameWithType> Aby przypisać prawidłowe znaki do nowego ciągu. W przypadku większego ciągu <xref:System.Text.StringBuilder> można użyć klasy.
  
[!code-csharp[Removing invalid characters](~/samples/snippets/csharp/programming-guide/string-to-number/parse-tryparse2/program.cs)]  

## <a name="calling-the-convert-methods"></a>Wywoływanie metod konwersji

Poniższa tabela zawiera listę metod z <xref:System.Convert> klasy, których można użyć do przekonwertowania ciągu na liczbę.  
  
|Typ liczbowy|Metoda|  
|------------------|------------|  
|`decimal`|<xref:System.Convert.ToDecimal%28System.String%29>|  
|`float`|<xref:System.Convert.ToSingle%28System.String%29>|  
|`double`|<xref:System.Convert.ToDouble%28System.String%29>|  
|`short`|<xref:System.Convert.ToInt16%28System.String%29>|  
|`int`|<xref:System.Convert.ToInt32%28System.String%29>|  
|`long`|<xref:System.Convert.ToInt64%28System.String%29>|  
|`ushort`|<xref:System.Convert.ToUInt16%28System.String%29>|  
|`uint`|<xref:System.Convert.ToUInt32%28System.String%29>|  
|`ulong`|<xref:System.Convert.ToUInt64%28System.String%29>|  
  
 Poniższy przykład wywołuje metodę, <xref:System.Convert.ToInt32%28System.String%29?displayProperty=nameWithType> Aby przekonwertować ciąg wejściowy na [int](../../language-reference/builtin-types/integral-numeric-types.md). Przykład przechwytuje dwa najczęstsze wyjątki, które mogą być zgłaszane przez tę metodę, <xref:System.FormatException> i <xref:System.OverflowException> . Jeśli wynikowy numer można zwiększyć bez przekroczenia <xref:System.Int32.MaxValue?displayProperty=nameWithType> , przykład dodaje 1 do wyniku i wyświetla dane wyjściowe.  
  
[!code-csharp[Parsing with Convert methods](~/samples/snippets/csharp/programming-guide/string-to-number/convert/program.cs)]  
  
## <a name="see-also"></a>Zobacz także

- [Typy](./index.md)
- [Określanie, czy ciąg reprezentuje wartość numeryczną](../strings/how-to-determine-whether-a-string-represents-a-numeric-value.md)
- [Przykład: Narzędzie formatowania programu .NET Core WinForms (C#)](https://docs.microsoft.com/samples/dotnet/samples/windowsforms-formatting-utility-cs)
