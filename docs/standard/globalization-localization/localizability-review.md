---
title: Sprawdzenie możliwości lokalizacji
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- world-ready applications, localizability
- application development [.NET], localization
- localizability [.NET]
- international applications [.NET], localizability
- globalization [.NET], localizability
- culture, localizability
- localization [.NET], localizability
- global applications, localizability
- localizing resources
ms.assetid: 3aee2fbb-de47-4e37-8fe4-ddebb9719247
ms.openlocfilehash: 30cde57a5c837d9dc324e9cd263d2a1011641af4
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "94829846"
---
# <a name="localizability-review"></a>Sprawdzenie możliwości lokalizacji

Przegląd możliwości lokalizowania jest pośrednim krokiem w rozwoju aplikacji gotowej do użycia na całym świecie. Sprawdza, czy aplikacja globalna jest gotowa do lokalizacji i identyfikuje każdy kod lub wszelkie aspekty interfejsu użytkownika, które wymagają specjalnej obsługi. Ten krok pomaga również upewnić się, że proces lokalizacji nie spowoduje wprowadzenia żadnych usterek funkcjonalnych do aplikacji. Po rozpatrzeniu wszystkich problemów zgłoszonych przez przegląd zlokalizowania aplikacja jest gotowa do lokalizacji. Jeśli przegląd możliwości zlokalizowania jest dokładny, nie należy modyfikować kodu źródłowego w procesie lokalizacji.

Przegląd możliwości zlokalizowania składa się z trzech następujących testów:

- [Czy zaimplementowano zalecenia dotyczące globalizacji?](#global)

- [Czy funkcje uwzględniające kulturę są prawidłowo obsługiwane?](#culture)

- [Czy aplikacja została przetestowana z danymi międzynarodowymi?](#test)

<a name="global"></a>
## <a name="implement-globalization-recommendations"></a>Implementowanie zaleceń globalizacji

Jeśli aplikacja została zaprojektowana i opracowana z myślą o lokalizacji, a po wykonaniu zaleceń omówionych w artykule [globalizacja](globalization.md) , przegląd możliwości zlokalizowania będzie miał duże gwarancje jakości. W przeciwnym razie na tym etapie należy przejrzeć i zaimplementować zalecenia dotyczące [globalizacji](globalization.md) oraz usunąć błędy w kodzie źródłowym, które uniemożliwiają lokalizację.

<a name="culture"></a>
## <a name="handle-culture-sensitive-features"></a>Obsługa funkcji zależnych od kultury

Platforma .NET nie zapewnia programistycznej pomocy technicznej w wielu obszarach, które różnią się w zależności od kultury. W większości przypadków należy napisać niestandardowy kod do obsługi obszarów funkcji, takich jak następujące:

- Adresy

- Numery telefonów

- Rozmiary papieru

- Jednostki miary używane dla długości, wagi, obszaru, objętości i temperatury

   Chociaż platforma .NET nie oferuje wbudowanej obsługi konwersji między jednostkami miary, można użyć <xref:System.Globalization.RegionInfo.IsMetric%2A?displayProperty=nameWithType> właściwości, aby określić, czy określony kraj lub region używa systemu metrycznego, jak pokazano w poniższym przykładzie.

   [!code-csharp[Conceptual.Localizability#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.localizability/cs/ismetric1.cs#1)]
   [!code-vb[Conceptual.Localizability#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.localizability/vb/ismetric1.vb#1)]

<a name="test"></a>
## <a name="test-your-application"></a>Testowanie aplikacji

Przed zlokalizowaniem aplikacji należy ją przetestować przy użyciu danych międzynarodowych w międzynarodowych wersjach systemu operacyjnego. Chociaż większość interfejsu użytkownika nie zostanie zlokalizowana w tym momencie, będzie można wykryć następujące problemy:

- Serializowane dane, które nie są poprawnie deserializacji w różnych wersjach systemu operacyjnego.

- Dane liczbowe, które nie odzwierciedlają Konwencji bieżącej kultury. Na przykład liczby mogą być wyświetlane z nieprawidłowymi separatorami grup, separatorami dziesiętnymi lub symbolami waluty.

- Dane daty i godziny, które nie odzwierciedlają Konwencji bieżącej kultury. Na przykład liczby reprezentujące miesiąc i dzień mogą występować w niewłaściwej kolejności, separatory dat mogą być niepoprawne lub informacje o strefie czasowej mogą być nieprawidłowe.

- Zasoby, których nie można znaleźć, ponieważ nie zidentyfikowano domyślnej kultury dla aplikacji.

- Ciągi, które są wyświetlane w nietypowej kolejności dla określonej kultury.

- Porównania ciągów lub porównania dla równości, które zwracają nieoczekiwane wyniki.

Jeśli zastosowano zalecenia dotyczące globalizacji podczas tworzenia aplikacji, obsługiwane są funkcje zależne od kultury i zidentyfikowane i rozwiązane z problemami z lokalizacją, które powstały podczas testowania, można przejść do następnego kroku, [lokalizacji](localization.md).

## <a name="see-also"></a>Zobacz także

- [Globalizacja i lokalizacja](index.md)
- [Lokalizacja](localization.md)
- [Globalizacja](globalization.md)
- [Zasoby w aplikacjach klasycznych](../../framework/resources/index.md)
