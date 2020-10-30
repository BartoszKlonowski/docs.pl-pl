---
title: Wykonywanie niezależnych od kultury porównań ciągów
ms.date: 08/22/2018
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- String.CompareTo method
- String.Compare method
- string comparison [.NET], culture-insensitive
- strings [.NET], comparing
- culture-insensitive string operations, comparisons
- culture parameter
ms.assetid: abae50ef-32f7-4a50-a540-fd256fd1aed0
ms.openlocfilehash: 1d8dc3f1bf686550eb94d7fb3003d4c21741739e
ms.sourcegitcommit: b1442669f1982d3a1cb18ea35b5acfb0fc7d93e4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2020
ms.locfileid: "93064148"
---
# <a name="performing-culture-insensitive-string-comparisons"></a>Wykonywanie niezależnych od kultury porównań ciągów
Domyślnie <xref:System.String.Compare%2A?displayProperty=nameWithType> Metoda wykonuje porównania uwzględniające kulturę i wielkość liter. Ta metoda zawiera również kilka przeciążeń, które udostępniają `culture` parametr, który pozwala określić kulturę, która ma być używana, oraz `comparisonType` parametr, który umożliwia określenie reguł porównania do użycia. Wywoływanie tych metod zamiast przeciążenia domyślnego usuwa wszelkie niejednoznaczności dotyczące reguł używanych w wywołaniu określonej metody i jednoznacznie wskazuje, czy w danym porównaniu jest uwzględniana kultura, czy nie.  
  
> [!NOTE]
> Oba przeciążenia <xref:System.String.CompareTo%2A?displayProperty=nameWithType> metody wykonują porównania zależne od kultury i wielkości liter; nie można użyć tej metody do wykonywania porównań bez uwzględniania kultury. W przypadku przejrzystości kodu zalecamy użycie <xref:System.String.Compare%2A?displayProperty=nameWithType> metody zamiast.  
  
 W przypadku operacji zależnych od kultury należy <xref:System.StringComparison.CurrentCulture?displayProperty=nameWithType> określić <xref:System.StringComparison.CurrentCultureIgnoreCase?displayProperty=nameWithType> wartość wyliczenia lub jako `comparisonType` parametr. Jeśli chcesz wykonać porównanie z uwzględnieniem kultury przy użyciu wyoznaczonej kultury innej niż bieżąca kultura, określ <xref:System.Globalization.CultureInfo> obiekt, który reprezentuje tę kulturę jako `culture` parametr.  
  
 Porównania ciągów niewrażliwych na kulturę obsługiwane przez <xref:System.String.Compare%2A?displayProperty=nameWithType> metodę są językiem (na podstawie Konwencji sortowania niezmiennej kultury) lub w języku innym niż język (na podstawie wartości porządkowej znaków w ciągu). Porównania nielingwistyczne stanowią większość pośród porównań ciągów, w których nie jest uwzględniana kultura. Dla tych porównań należy określić <xref:System.StringComparison.Ordinal?displayProperty=nameWithType> <xref:System.StringComparison.OrdinalIgnoreCase?displayProperty=nameWithType> wartość wyliczenia lub jako `comparisonType` parametr. Na przykład jeśli decyzja dotycząca zabezpieczeń (taka jak porównywanie nazwy użytkownika lub hasła) jest podejmowana na podstawie porównania ciągów, w operacji nie powinna być uwzględniana kultura, a operacja powinna być nielingwistyczna, dzięki czemu konwencje dotyczące określonej kultury lub języka nie będą miały wpływu na wynik.  
  
 Lingwistycznych porównań ciągów, w których nie jest uwzględniana kultura, należy używać w sytuacji, gdy trzeba w spójny sposób obsługiwać lingwistycznie podobne ciągi z różnych kultur. Na przykład jeśli w aplikacji w polu listy są wyświetlane wyrazy, w których jest używanych wiele zestawów znaków, warto wyświetlać te wyrazy w takiej samej kolejności, niezależnie od bieżącej kultury. W przypadku porównywania kulturowego niewrażliwego na środowisko .NET definiuje niezmienną kulturę opartą na konwencjach językowych w języku angielskim. Aby przeprowadzić porównanie lingwistyczne bez uwzględniania kultur, określ <xref:System.StringComparison.InvariantCulture?displayProperty=nameWithType> lub <xref:System.StringComparison.InvariantCultureIgnoreCase?displayProperty=nameWithType> jako `comparisonType` parametr.  
  
 W poniższym przykładzie są wykonywane dwa nielingwistyczne porównania ciągów, w których nie jest uwzględniana kultura. W pierwszym z nich jest uwzględniana wielkość liter, a w drugim nie.  
  
 [!code-csharp[Conceptual.Strings.CultureInsensitiveComparison#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.cultureinsensitivecomparison/cs/cultureinsensitive1.cs#1)]
 [!code-vb[Conceptual.Strings.CultureInsensitiveComparison#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.cultureinsensitivecomparison/vb/cultureinsensitive1.vb#1)]  

Można pobrać [tabele wagi sortowania](https://www.microsoft.com/download/details.aspx?id=10921), zestaw plików tekstowych, które zawierają informacje o wagach znaków używanych w operacjach sortowania i porównywania dla systemów operacyjnych Windows, a także [domyślną tabelę elementów sortowania Unicode](https://www.unicode.org/Public/UCA/latest/allkeys.txt), tabelę wagi sortowania dla systemu Linux i macOS.

## <a name="see-also"></a>Zobacz też

- <xref:System.String.Compare%2A?displayProperty=nameWithType>
- <xref:System.String.CompareTo%2A?displayProperty=nameWithType>
- [Wykonywanie niezależnych od kultury operacji na ciągach](performing-culture-insensitive-string-operations.md)
- [Najlepsze rozwiązania dotyczące używania ciągów](../base-types/best-practices-strings.md)
