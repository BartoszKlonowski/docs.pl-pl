---
title: Argumenty nazwane i opcjonalne — Przewodnik programowania w języku C#
description: Nazwane argumenty w języku C# określają argumenty według nazwy, a nie do położenia. Opcjonalne argumenty można pominąć.
ms.date: 09/25/2020
ms.custom: contperf-fy21q1
f1_keywords:
- namedParameter_CSharpKeyword
- cs_namedParameter
helpviewer_keywords:
- parameters [C#], named
- named arguments [C#]
- arguments [C#], named
- optional arguments [C#]
- arguments [C#], optional
- parameters [C#], optional
- named and optional arguments [C#]
ms.assetid: 839c960c-c2dc-4d05-af4d-ca5428e54008
ms.openlocfilehash: bb79d956124a610bac0de6825c1f42655789e98d
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2020
ms.locfileid: "97513110"
---
# <a name="named-and-optional-arguments-c-programming-guide"></a>Argumenty nazwane i opcjonalne (Przewodnik programowania w języku C#)

W języku C# 4 wprowadzono argumenty nazwane i opcjonalne. *Nazwane argumenty* umożliwiają określenie argumentu dla parametru przez dopasowanie argumentu do jego nazwy, a nie do pozycji na liście parametrów. *Argumenty opcjonalne* umożliwiają pominięcie argumentów dla niektórych parametrów. Obie techniki mogą być używane z metodami, indeksatorami, konstruktorami i delegatami.

W przypadku używania argumentów nazwanych i opcjonalnych argumenty są oceniane w kolejności, w jakiej są wyświetlane na liście argumentów, a nie na liście parametrów.

Parametry nazwane i opcjonalne umożliwiają podawanie argumentów dla wybranych parametrów. Ta funkcja znacznie upraszcza wywołania interfejsów COM, takich jak interfejsy API automatyzacji Microsoft Office.

## <a name="named-arguments"></a>Nazwane argumenty

Nazwane argumenty są bezpłatne od dopasowania do kolejności parametrów na listach parametrów wywoływanych metod. Parametr dla każdego argumentu można określić za pomocą nazwy parametru. Na przykład funkcja, która drukuje szczegóły zamówienia (takie jak nazwa sprzedawcy, numer zamówienia & Nazwa produktu), może być wywoływana przez wysłanie argumentów według pozycji w kolejności zdefiniowanej przez funkcję.

```csharp
PrintOrderDetails("Gift Shop", 31, "Red Mug");
```

Jeśli nie pamiętasz kolejności parametrów, ale znasz ich nazwy, możesz wysłać argumenty w dowolnej kolejności.

```csharp
PrintOrderDetails(orderNum: 31, productName: "Red Mug", sellerName: "Gift Shop");
PrintOrderDetails(productName: "Red Mug", sellerName: "Gift Shop", orderNum: 31);
```

Argumenty nazwane również zwiększają czytelność kodu przez zidentyfikowanie, co reprezentuje każdy argument. W poniższym przykładzie metoda `sellerName` nie może mieć wartości null ani być białym znakiem. Zarówno, jak `sellerName` i `productName` są typami ciągów, zamiast wysyłać argumenty według położenia, warto użyć nazwanych argumentów, aby odróżnić dwa i zmniejszyć liczbę pomyłek dla każdego odczytu kodu.
  
Argumenty nazwane, gdy są używane z argumentami pozycyjnymi, są prawidłowe tak długo, jak

- nie są one następują żadnych argumentów pozycyjnych lub

    ```csharp
    PrintOrderDetails("Gift Shop", 31, productName: "Red Mug");
    ```

- _począwszy od języka C# 7,2_, są one używane w poprawnej pozycji. W poniższym przykładzie parametr `orderNum` znajduje się w poprawnej pozycji, ale nie jest jawnie nazwany.

    ```csharp
    PrintOrderDetails(sellerName: "Gift Shop", 31, productName: "Red Mug");
    ```

Argumenty pozycyjne, które są zgodne z argumentami nazwanymi poza kolejnością, są nieprawidłowe.

```csharp
// This generates CS1738: Named argument specifications must appear after all fixed arguments have been specified.
PrintOrderDetails(productName: "Red Mug", 31, "Gift Shop");
```

## <a name="example"></a>Przykład

Poniższy kod implementuje przykłady z tej sekcji wraz z dodatkowymi.  

[!code-csharp[csProgGuideNamedAndOptional#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguidenamedandoptional/cs/program.cs#1)]

## <a name="optional-arguments"></a>Argumenty opcjonalne

Definicja metody, konstruktora, indeksatora lub delegata może określać, że jej parametry są wymagane lub opcjonalne. Każde wywołanie musi udostępniać argumenty dla wszystkich wymaganych parametrów, ale może pominąć argumenty dla parametrów opcjonalnych.

Każdy opcjonalny parametr ma wartość domyślną w ramach swojej definicji. Jeśli żaden argument nie jest wysyłany dla tego parametru, zostanie użyta wartość domyślna. Wartość domyślna musi być jednym z następujących typów wyrażeń:
  
- wyrażenie stałe;  
- wyrażenie formularza `new ValType()` , gdzie `ValType` jest typem wartości, na przykład [wyliczeniem](../../language-reference/builtin-types/enum.md) lub [strukturą](../../language-reference/builtin-types/struct.md);
- wyrażenie [domyślne (ValType)](../../language-reference/operators/default.md), gdzie `ValType` jest typem wartości.

Parametry opcjonalne są definiowane na końcu listy parametrów po dowolnych wymaganych parametrach. Jeśli obiekt wywołujący zawiera argument dla dowolnego z parametrów opcjonalnych, musi podać argumenty dla wszystkich poprzedzających parametry opcjonalne. Luki rozdzielane przecinkami na liście argumentów nie są obsługiwane. Na przykład, w poniższym kodzie metoda wystąpienia `ExampleMethod` jest zdefiniowana z jednym wymaganym i dwoma opcjonalnymi parametrami.

[!code-csharp[csProgGuideNamedAndOptional#15](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguidenamedandoptional/cs/optional.cs#15)]

Następujące wywołanie `ExampleMethod` powoduje wystąpienie błędu kompilatora, ponieważ argument jest dostarczany dla trzeciego parametru, ale nie w drugim.

```csharp
//anExample.ExampleMethod(3, ,4);
```

Jeśli jednak znasz nazwę trzeciego parametru, możesz użyć argumentu nazwanego do wykonania zadania.

```csharp
anExample.ExampleMethod(3, optionalint: 4);
```

Funkcja IntelliSense używa nawiasów, aby wskazać parametry opcjonalne, jak pokazano na poniższej ilustracji:

![Zrzut ekranu przedstawiający funkcję IntelliSense Quick info dla metody ExampleMethod.](./media/named-and-optional-arguments/optional-examplemethod-parameters.png)

> [!NOTE]
> Można również zadeklarować parametry opcjonalne przy użyciu klasy .NET <xref:System.Runtime.InteropServices.OptionalAttribute> . `OptionalAttribute` parametry nie wymagają wartości domyślnej.

## <a name="example"></a>Przykład

W poniższym przykładzie Konstruktor dla `ExampleClass` ma jeden parametr, który jest opcjonalny. Metoda wystąpienia `ExampleMethod` ma jeden wymagany parametr, `required` i dwa parametry opcjonalne `optionalstr` oraz `optionalint` . Kod w `Main` pokazuje różne sposoby wywoływania konstruktora i metody.

[!code-csharp[csProgGuideNamedAndOptional#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguidenamedandoptional/cs/optional.cs#2)]

Poprzedni kod pokazuje kilka przykładów, w których parametry opcjonalne nie są poprawnie stosowane. Pierwszy ilustruje, że argument musi być podany dla pierwszego parametru, który jest wymagany.
  
## <a name="com-interfaces"></a>Interfejsy COM

Argumenty nazwane i opcjonalne wraz z obsługą obiektów dynamicznych znacznie zwiększają współdziałanie z interfejsami API modelu COM, takimi jak interfejsy API usługi Office Automation.

Na przykład <xref:Microsoft.Office.Interop.Excel.Range.AutoFormat%2A> Metoda w interfejsie programu Excel Microsoft Office <xref:Microsoft.Office.Interop.Excel.Range> ma siedem parametrów, z których wszystkie są opcjonalne. Te parametry przedstawiono na poniższej ilustracji:

![Zrzut ekranu przedstawiający funkcję IntelliSense Quick info dla metody Autoformatowania.](./media/named-and-optional-arguments/autoformat-method-parameters.png)

W języku C# 3,0 i wcześniejszych wersjach argument jest wymagany dla każdego parametru, jak pokazano w poniższym przykładzie.

[!code-csharp[csProgGuideNamedAndOptional#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguidenamedandoptional/cs/namedandoptcom.cs#3)]

Można jednak znacznie uprościć wywołanie do `AutoFormat` za pomocą argumentów nazwanych i opcjonalnych wprowadzonych w języku C# 4,0. Argumenty nazwane i opcjonalne umożliwiają pominięcie argumentu dla opcjonalnego parametru, jeśli nie chcesz zmieniać wartości domyślnej parametru. W poniższym wywołaniu wartość jest określona tylko dla jednego z siedmiu parametrów.

[!code-csharp[csProgGuideNamedAndOptional#13](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguidenamedandoptional/cs/namedandoptcom.cs#13)]

Aby uzyskać więcej informacji i przykładów, zobacz [jak używać argumentów nazwanych i opcjonalnych w programowaniu pakietu Office](./how-to-use-named-and-optional-arguments-in-office-programming.md) oraz [jak uzyskiwać dostęp do obiektów międzyoperacyjności pakietu Office za pomocą funkcji języka C#](../interop/how-to-access-office-onterop-objects.md).
  
## <a name="overload-resolution"></a>Rozpoznanie przeciążenia

Użycie argumentów nazwanych i opcjonalnych wpływa na rozpoznawanie przeciążenia w następujący sposób:

- Metoda, indeksator lub Konstruktor jest kandydatem do wykonania, jeśli każdy z jego parametrów jest opcjonalny lub odpowiada według nazwy lub według pozycji, do pojedynczego argumentu w instrukcji wywołującej i ten argument można przekonwertować na typ parametru.  
- W przypadku znalezienia więcej niż jednego kandydata reguły rozpoznawania przeciążenia dla preferowanych konwersji są stosowane do argumentów, które są jawnie określone. Pominięte argumenty dla parametrów opcjonalnych są ignorowane.
- Jeśli dwie kandydaci są uznawane za równie dobre, preferencja przechodzi do kandydata, który nie ma parametrów opcjonalnych, dla których argumenty zostały pominięte w wywołaniu. Rozpoznanie przeciążenia zazwyczaj preferuje kandydatów, które mają mniej parametrów.
  
## <a name="c-language-specification"></a>Specyfikacja języka C#

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]
