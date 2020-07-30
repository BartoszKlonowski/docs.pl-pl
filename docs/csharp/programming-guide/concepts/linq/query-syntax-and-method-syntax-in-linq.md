---
title: Składnia zapytania i metody w technologii LINQ (C#)
description: Dowiedz się więcej o składni zapytań i składni metod w LINQ. Obejmuje to standardowe metody rozszerzenia operatora zapytania i wyrażenia lambda.
ms.date: 07/20/2015
helpviewer_keywords:
- LINQ [C#], query syntax vs. method syntax
- queries [LINQ in C#], syntax comparisons
ms.assetid: eedd6dd9-fec2-428c-9581-5b8783810ded
ms.openlocfilehash: 1765a15347aeedb9cc5fa6784abdfad6fafe4016
ms.sourcegitcommit: 6f58a5f75ceeb936f8ee5b786e9adb81a9a3bee9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/28/2020
ms.locfileid: "87300764"
---
# <a name="query-syntax-and-method-syntax-in-linq-c"></a>Składnia zapytania i metody w technologii LINQ (C#)
Większość zapytań w dokumentacji języka wprowadzającego Integrated Query (LINQ) jest zapisywana przy użyciu składni zapytania deklaracyjnego LINQ. Jednak Składnia zapytania musi być przetłumaczona na wywołania metody dla środowiska uruchomieniowego języka wspólnego (CLR) platformy .NET podczas kompilowania kodu. Te wywołania metody wywołują standardowe operatory zapytań, które mają nazwy takie jak `Where` , `Select` , `GroupBy` , `Join` , `Max` i `Average` . Można wywołać je bezpośrednio przy użyciu składni metody zamiast składni zapytania.  
  
 Składnia zapytań i składnia metody są semantycznie takie same, ale wiele osób może łatwiej odczytywać składnię zapytań. Niektóre zapytania muszą być wyrażone jako wywołania metod. Na przykład należy użyć wywołania metody, aby wyrazić zapytanie, które pobiera liczbę elementów zgodnych z określonym warunkiem. Należy również użyć wywołania metody dla zapytania pobierającego element, który ma wartość maksymalną w sekwencji źródłowej. Dokumentacja referencyjna dla standardowych operatorów zapytań w <xref:System.Linq> przestrzeni nazw zwykle używa składni metody. W związku z tym nawet gdy zaczynasz pisać zapytania LINQ, warto zapoznać się z sposobami używania składni metody w zapytaniach i w samych wyrażeniach zapytań.  
  
## <a name="standard-query-operator-extension-methods"></a>Metody rozszerzające standardowy operator zapytań  
 W poniższym przykładzie pokazano proste *wyrażenie zapytania* i semantycznie równoważne zapytanie zapisywane jako *zapytanie oparte na metodzie*.  
  
 [!code-csharp[csLINQGettingStarted#22](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#22)]  
  
 Dane wyjściowe z dwóch przykładów są identyczne. Można zobaczyć, że typ zmiennej zapytania jest taka sama w obu formach: <xref:System.Collections.Generic.IEnumerable%601> .  
  
 Aby zrozumieć zapytanie oparte na metodzie, Przeanalizujmy ją dokładniej. Po prawej stronie wyrażenia Zauważ, że `where` klauzula jest teraz wyrażona jako metoda wystąpienia na `numbers` obiekcie, co oznacza, że odwołanie ma typ `IEnumerable<int>` . Jeśli znasz <xref:System.Collections.Generic.IEnumerable%601> interfejs ogólny, wiesz, że nie ma `Where` metody. Jeśli jednak zostanie wywołana lista uzupełniania IntelliSense w środowisku IDE programu Visual Studio, zobaczysz nie tylko `Where` metodę, ale wiele innych metod, takich jak `Select` ,, `SelectMany` `Join` i `Orderby` . To są wszystkie standardowe operatory zapytań.  
  
 ![Zrzut ekranu przedstawiający wszystkie standardowe operatory zapytań w IntelliSense.](./media/query-syntax-and-method-syntax-in-linq/standard-query-operators.png)  
  
 Mimo że został on <xref:System.Collections.Generic.IEnumerable%601> ponownie zdefiniowany w celu uwzględnienia tych dodatkowych metod, w rzeczywistości nie jest to przypadek. Standardowe operatory zapytań są implementowane jako nowy rodzaj metody wywoływanie *metod rozszerzających*. Metody rozszerzeń "rozszerzają" istniejący typ; mogą być wywoływane tak, jakby były metodami wystąpień w typie. Standardowe operatory zapytań zwiększają się <xref:System.Collections.Generic.IEnumerable%601> i dlatego można pisać `numbers.Where(...)` .  
  
 Aby rozpocząć korzystanie z LINQ, wszystko, co naprawdę trzeba wiedzieć na temat metod rozszerzających, polega na tym, jak przenieść je do zakresu w aplikacji za pomocą odpowiednich `using` dyrektyw. Z punktu widzenia aplikacji Metoda rozszerzająca i zwykła metoda wystąpienia są takie same.  
  
 Aby uzyskać więcej informacji na temat metod rozszerzających, zobacz [metody rozszerzenia](../../classes-and-structs/extension-methods.md). Aby uzyskać więcej informacji na temat standardowych operatorów zapytań, zobacz [standardowe operatory zapytań — Omówienie (C#)](./standard-query-operators-overview.md). Niektórzy dostawcy LINQ, takie jak [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] i [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] , implementują własne standardowe operatory zapytań i dodatkowe metody rozszerzające dla innych typów <xref:System.Collections.Generic.IEnumerable%601> .  
  
## <a name="lambda-expressions"></a>Wyrażenia lambda  
 W poprzednim przykładzie należy zauważyć, że wyrażenie warunkowe ( `num % 2 == 0` ) jest przekazywany jako argument w wierszu do `Where` metody: `Where(num => num % 2 == 0).` to wyrażenie wbudowane jest nazywane wyrażeniem lambda. Jest to wygodny sposób pisania kodu, który w przeciwnym razie musi być napisany w bardziej skomplikowany sposób jako metoda anonimowa lub Delegat ogólny lub drzewo wyrażenia. W języku C# `=>` jest operatorem lambda, który jest odczytywany jako "przechodzi do". Po `num` lewej stronie operatora jest zmienną wejściową, która odnosi się do `num` w wyrażeniu zapytania. Kompilator może wywnioskować typ, `num` ponieważ wie, że `numbers` jest typem ogólnym <xref:System.Collections.Generic.IEnumerable%601> . Treść wyrażenia lambda jest taka sama jak wyrażenie w składni zapytania lub w dowolnym innym wyrażeniu lub instrukcji języka C#. może obejmować wywołania metod i inne złożone logiki. "Zwracana wartość" jest tylko wynikiem wyrażenia.  
  
 Aby rozpocząć korzystanie z LINQ, nie musisz używać wyrażeń lambda w szerokim stopniu. Jednak niektóre zapytania można wyrazić tylko w składni metody, a niektóre z nich wymagają wyrażenia lambda. Po poznaniu się z wyrażeniami lambda można sprawdzić, czy są one zaawansowanym i elastycznym narzędziem w przyborniku LINQ. Aby uzyskać więcej informacji, zobacz [wyrażenia lambda](../../statements-expressions-operators/lambda-expressions.md).  
  
## <a name="composability-of-queries"></a>Możliwości tworzenia zapytań  
 W poprzednim przykładzie kodu należy zauważyć, że `OrderBy` Metoda jest wywoływana przy użyciu operatora kropki w wywołaniu `Where` . `Where`tworzy filtrowaną sekwencję, a następnie `Orderby` działa w tej sekwencji, sortując ją. Ponieważ zapytania zwracają `IEnumerable` , należy je złożyć w składni metody przez łańcuch wywołań metod. Jest to działanie kompilatora w tle podczas pisania zapytań przy użyciu składni zapytania. A ponieważ zmienna zapytania nie przechowuje wyników zapytania, można je zmodyfikować lub użyć jako podstawy dla nowego zapytania w dowolnym momencie, nawet po jego wykonaniu.  
