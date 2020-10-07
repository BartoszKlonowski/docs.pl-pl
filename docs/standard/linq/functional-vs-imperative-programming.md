---
title: Programowanie funkcjonalne a bezwzględne programowanie — LINQ to XML
description: Poznaj programowanie funkcjonalne i różnice między tradycyjnymi, niezależnymi (proceduralnymi) programowaniem.
ms.date: 07/20/2015
ms.assetid: 5e35c5a0-c949-422a-873b-fca6b2254f57
ms.openlocfilehash: e99cffa9500c07c507962f41b17ab3f3b05c7781
ms.sourcegitcommit: 636af37170ae75a11c4f7d1ecd770820e7dfe7bd
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/07/2020
ms.locfileid: "91805290"
---
# <a name="functional-programming-vs-imperative-programming-linq-to-xml"></a>Programowanie funkcjonalne a programowanie bezwzględne (LINQ to XML)

W tym artykule porównano i różnią się programowanie funkcjonalne z bardziej tradycyjnym, niewzględnym (proceduralnym) programowaniem.

## <a name="functional-programming-vs-imperative-programming"></a>Programowanie funkcjonalne a programowanie imperatywne

Model *programowania funkcjonalnego* został jawnie utworzony w celu obsługi czystego podejścia funkcjonalnego do rozwiązywania problemów. Programowanie funkcjonalne jest formą *programowania deklaratywnego*. W przeciwieństwie do najpopularniejszych języków, w tym języków programowania zorientowanego obiektowo (OOP), takich jak C#, Visual Basic, C++ i Java, zostały zaprojektowane głównie *do obsługi* bezwzględnego (proceduralnego) programowania.

W przypadku niezależnego podejścia deweloper zapisuje kod, który określa czynności, które musi wykonać komputer, aby osiągnąć cel. Jest to czasami określane jako programowanie *algorytmów* . Z kolei podejście funkcjonalne obejmuje tworzenie problemów jako zestaw funkcji do wykonania. Należy dokładnie zdefiniować dane wejściowe dla każdej funkcji i co zwraca każda funkcja. W poniższej tabeli opisano niektóre ogólne różnice między tymi dwoma podejściami.

|Charakterystyka|Bezwzględne podejście|Podejście funkcjonalne|
|--------------------|-------------------------|-------------------------|
|Fokus programisty|Jak wykonywać zadania (algorytmy) i jak śledzić zmiany w stanie.|Jakie informacje są potrzebne i jakie przekształcenia są wymagane.|
|Zmiany stanu|Ważne.|Nie istnieje.|
|Kolejność wykonywania|Ważne.|Niska ważność.|
|Podstawowe sterowanie przepływem|Pętle, warunkowe i wywołania funkcji (Metoda).|Wywołania funkcji, w tym rekursja.|
|Podstawowa jednostka manipulowania|Wystąpienia struktur lub klas.|Działa jako obiekty pierwszej klasy i kolekcje danych.|

Chociaż większość języków została zaprojektowana do obsługi określonego modelu programowania, wiele języków ogólnych jest wystarczająco elastycznych, aby obsługiwało wiele odmian. Na przykład większość języków zawierających wskaźniki funkcji może służyć do credibly programowania funkcjonalnego. Ponadto Języki C# i Visual Basic zawierają jawne rozszerzenia językowe do obsługi programowania funkcjonalnego, w tym wyrażenia lambda i wnioskowania o typie. Technologia LINQ jest formą deklaracyjnego programowania funkcjonalnego.

## <a name="functional-programming-using-xslt"></a>Programowanie funkcjonalne przy użyciu XSLT

Wielu deweloperów XSLT potrafi poznać czyste podejście funkcjonalne. Najbardziej efektywnym sposobem na Tworzenie arkusza stylów XSLT jest traktowanie każdego szablonu jako odizolowanego, możliwego do redagowania transformacji. Kolejność wykonywania jest całkowicie niewyróżniona. XSLT nie zezwala na efekty uboczne (z wyjątkiem tego, że mechanizmy ucieczki do wykonywania kodu proceduralnego mogą wprowadzać efekty uboczne, które powodują, że nie są one czyste). Chociaż język XSLT jest skutecznym narzędziem, niektóre jego właściwości nie są optymalne. Na przykład, konstrukcje programistyczne w języku XML czynią kod stosunkowo pełny i dlatego trudno jest zachować. Ponadto duże zależności dotyczące rekursji dla sterowania przepływem mogą spowodować, że kod trudno odczytać. Aby uzyskać więcej informacji na temat XSLT, zobacz [XSLT Transformations](../data/xml/xslt-transformations.md).

Jednak język XSLT udowadniał wartość użycia czystego podejścia funkcjonalnego do przekształcenia XML z jednego kształtu do drugiego. Czyste programowanie funkcjonalne przy użyciu LINQ to XML jest podobne do języka XSLT na wiele sposobów. Jednak konstrukcje programistyczne wprowadzone przez LINQ to XML, C# i Visual Basic umożliwiają pisanie czystych transformacji funkcjonalnych, które są bardziej czytelne i konserwowane niż XSLT.

## <a name="advantages-of-pure-functions"></a>Zalety czystych funkcji

Podstawową przyczyną wdrożenia przekształceń funkcjonalnych jako czystych funkcji jest możliwość tworzenia czystych funkcji: to jest, samodzielne i bezstanowe. Te cechy obejmują szereg korzyści, w tym następujące:

- Zwiększ czytelność i łatwość utrzymania. Jest to spowodowane tym, że każda funkcja została zaprojektowana w celu wykonania określonego zadania z uwzględnieniem argumentów. Funkcja nie polega na żadnym stanie zewnętrznym.
- Łatwiejsza zmiana na rozwój. Ponieważ kod jest łatwiejszy do refaktoryzacji, zmiany w projekcie są często łatwiejsze do wdrożenia. Załóżmy na przykład, że napiszesz skomplikowaną transformację, a następnie dowiesz się, że jakiś kod jest powtórzony kilka razy w transformacji. Jeśli refaktoryzacja jest przeprowadzana za pomocą czystej metody, można wywołać czystą metodę w stanie bez obaw o skutki uboczne.
- Łatwiejsze testowanie i debugowanie. Ze względu na to, że czyste funkcje mogą być łatwiejsze do przetestowania w izolacji, można napisać kod testu, który wywołuje czystą funkcję z typowymi wartościami, prawidłowymi przypadkami krawędzi i nieprawidłowymi przypadkami krawędzi.

## <a name="transitioning-for-oop-developers"></a>Przechodzenie dla deweloperów OOP

W tradycyjnych programowaniu zorientowanym obiektom (OOP) większość deweloperów jest przyzwyczajona do programowania w stylu bezwzględnym/proceduralnym. Aby przełączać się do programowania w czystym stylu funkcjonalnym, muszą one wprowadzać przejście w myśli i ich podejście do rozwoju.

Aby rozwiązać problemy, OOP programiści mogą projektować hierarchie klas, skupić się na poprawnym hermetyzacji i myśleć o kategoriach umów. Zachowanie i stan typów obiektów to najważniejsze, a funkcje językowe, takie jak klasy, interfejsy, dziedziczenie i polimorfizm, są dostarczane w celu rozwiązania tych problemów.

W przeciwieństwie do programowania funkcjonalnego podejścia do problemów obliczeniowych jako ćwiczenia w ocenie czystych, funkcjonalnych transformacji kolekcji danych. Programowanie funkcjonalne pozwala uniknąć stanu i modyfikowalnych danych, a zamiast tego kładzie nacisk na aplikacje funkcji.

Na szczęście język C# i Visual Basic nie wymagają pełnego przestępności do programowania funkcjonalnego, ponieważ obsługują zarówno metody programowania zasadniczego, jak i funkcjonalnego. Deweloper może wybrać, które podejście jest najbardziej odpowiednie dla konkretnego scenariusza. W rzeczywistości programy często łączą oba podejścia.

## <a name="see-also"></a>Zobacz też

- [Wprowadzenie do czystych przekształceń funkcjonalnych](introduction-pure-functional-transformations.md)
- [Przekształcenia XSLT](../data/xml/xslt-transformations.md)
- [Refaktoryzacja do czystych funkcji](refactor-pure-functions.md)
