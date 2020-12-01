---
title: Właściwości
description: Dowiedz się więcej o właściwościach języka C#, które obejmują funkcje sprawdzania poprawności, obliczone wartości, oceny z opóźnieniem i zmiany właściwości.
ms.technology: csharp-fundamentals
ms.date: 04/25/2018
ms.openlocfilehash: 5306650a10a3de0ff208f7c72c0ba520a527e746
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96437945"
---
# <a name="properties"></a>Właściwości

Właściwości są obywatelami pierwszej klasy w języku C#. Język definiuje składnię, która umożliwia deweloperom pisanie kodu, który dokładnie wyraża zamiar projektowania.

Właściwości zachowują się jak pola, gdy są dostępne.
Jednak, w przeciwieństwie do pól, właściwości są implementowane przy użyciu metod dostępu definiujących instrukcje wykonywane podczas uzyskiwania dostępu do właściwości lub do przypisywania.

## <a name="property-syntax"></a>Składnia właściwości

Składnia właściwości jest naturalnym rozszerzeniem pól. Pole definiuje lokalizację magazynu:

[!code-csharp[Person class with public fields](../../samples/snippets/csharp/properties/Person.cs#1)]

Definicja właściwości zawiera deklaracje dla `get` `set` metody dostępu i, która pobiera i przypisuje wartość tej właściwości:

[!code-csharp[Person class with public properties](../../samples/snippets/csharp/properties/Person.cs#2)]

Pokazana powyżej składnia jest składnią *Właściwości autoproperty* . Kompilator generuje lokalizację magazynu dla pola, które tworzy kopię zapasową właściwości. Kompilator implementuje także treść `get` `set` metod dostępu i.

Czasami trzeba zainicjować właściwość jako wartość inną niż domyślna dla tego typu.  C# umożliwia ustawienie wartości po zamykającym nawiasie klamrowym właściwości. Możesz preferować wartość początkową `FirstName` właściwości jako pusty ciąg, a nie `null` . Należy określić, jak pokazano poniżej:

[!code-csharp[Person class with properties and initializer](../../samples/snippets/csharp/properties/Person.cs#3)]

Konkretna Inicjalizacja jest najbardziej przydatna w przypadku właściwości tylko do odczytu, ponieważ zobaczysz w dalszej części tego artykułu.

Możesz również zdefiniować magazyn samodzielnie, jak pokazano poniżej:

[!code-csharp[Person class with properties and backing field](../../samples/snippets/csharp/properties/Person.cs#4)]

Gdy implementacja właściwości jest pojedynczym wyrażeniem, można użyć *składowych wyrażeń* dla metody pobierającej lub setter:

[!code-csharp[Person class with properties and expression bodied getters and setters](../../samples/snippets/csharp/properties/Person.cs#5)]

Ta uproszczona składnia zostanie użyta, jeśli ma to zastosowanie w tym artykule.

Pokazana powyżej Definicja właściwości jest właściwością do odczytu i zapisu. Zwróć uwagę na słowo kluczowe `value` w metodzie dostępu set. `set`Metoda dostępu zawsze ma jeden parametr o nazwie `value` . `get`Metoda dostępu musi zwracać wartość, która jest możliwa do przekonwertowania na typ właściwości ( `string` w tym przykładzie).

Jest to podstawy składni. Istnieje wiele różnych wariantów, które obsługują różne idiomy projektowe. Eksplorujmy i poznaję opcje składni dla każdej z nich.

## <a name="scenarios"></a>Scenariusze

Powyższe przykłady pokazują jeden z najprostszych przypadków definicji właściwości: właściwość do odczytu i zapisu bez sprawdzania poprawności. Pisząc odpowiedni kod w `get` `set` metodzie dostępu i, można utworzyć wiele różnych scenariuszy.

### <a name="validation"></a>Walidacja

Można napisać kod w `set` metodzie dostępu, aby upewnić się, że wartości reprezentowane przez właściwość są zawsze prawidłowe. Załóżmy na przykład, że jedna reguła dla `Person` klasy jest, że nazwa nie może być pusta ani zawierać białych znaków. Należy napisać następujący sposób:

[!code-csharp[Validating property setters](../../samples/snippets/csharp/properties/Person.cs#6)]

Poprzedni przykład można uprościć za pomocą `throw` wyrażenia w ramach walidacji metody ustawiającej właściwość:

[!code-csharp[Validating property setters](../../samples/snippets/csharp/properties/Person.cs#7)]

Powyższy przykład wymusza zasadę, że imię nie może być puste ani zawierać białych znaków. Jeśli projektant zapisuje

```csharp
hero.FirstName = "";
```

To przypisanie zgłasza `ArgumentException` . Ponieważ akcesor zestawu właściwości musi mieć typ zwracany void, raportowane są błędy w metodzie dostępu zestawu przez wyrzucanie wyjątku.

Tę samą składnię można zwiększyć do wszystkiego potrzebnego w danym scenariuszu. Można sprawdzić relacje między różnymi właściwościami lub sprawdzić poprawność warunków zewnętrznych. Wszystkie prawidłowe instrukcje języka C# są prawidłowe w metodzie dostępu do właściwości.

### <a name="read-only"></a>Tylko odczyt

Do tego momentu wszystkie przejrzane definicje właściwości są właściwościami odczytu i zapisu z publicznymi dostępem. To nie jest jedyna prawidłowa dostępność dla właściwości.
Można tworzyć właściwości tylko do odczytu lub dawać różne ułatwienia dostępu dla zestawu i uzyskać dostęp. Załóżmy, że `Person` Klasa powinna włączać tylko zmianę wartości `FirstName` właściwości z innych metod w tej klasie. Możliwe jest przyznanie dostępu do zestawu akcesora `private` zamiast `public` :

[!code-csharp[Using a private setter for a publicly readonly property](../../samples/snippets/csharp/properties/Person.cs#8)]

Teraz można `FirstName` uzyskać dostęp do właściwości z dowolnego kodu, ale można go przypisać tylko z innego kodu w `Person` klasie.

Dowolny modyfikator dostępu można dodać do zestawu lub uzyskać dostęp. Każdy modyfikator dostępu umieszczony na pojedynczym akcesorze musi być bardziej ograniczony niż modyfikator dostępu w definicji właściwości. Powyższe jest dozwolone `FirstName` , ponieważ właściwość jest `public` , ale metoda dostępu set ma wartość `private` . Nie można zadeklarować `private` właściwości z `public` akcesorem. Deklaracje właściwości można również deklarować `protected` , `internal` , `protected internal` , lub, nawet `private` .

Istnieje również możliwość umieszczenia modyfikatora bardziej restrykcyjnego w `get` metodzie dostępu. Na przykład możesz mieć `public` Właściwość, ale ograniczyć `get` metodę dostępu do `private` . Ten scenariusz jest rzadko realizowany w sposób praktyczny.

Można również ograniczyć modyfikacje właściwości, aby można było ustawić je tylko w konstruktorze lub inicjatorze właściwości. Można zmodyfikować `Person` klasę w następujący sposób:

[!code-csharp[A readonly auto implemented property](../../samples/snippets/csharp/properties/Person.cs#9)]

Ta funkcja jest najczęściej używana do inicjowania kolekcji, które są udostępniane jako właściwości tylko do odczytu:

```csharp
public class Measurements
{
    public ICollection<DataPoint> points { get; } = new List<DataPoint>();
}
```

### <a name="computed-properties"></a>Właściwości obliczane

Właściwość nie musi po prostu zwracać wartości pola elementu członkowskiego. Można utworzyć właściwości, które zwracają obliczoną wartość. Rozwińmy `Person` obiekt, aby zwrócić pełną nazwę obliczoną przez połączenie imion i nazwisk:

[!code-csharp[A computed property](../../samples/snippets/csharp/properties/Person.cs#10)]

Powyższy przykład używa funkcji [interpolacji ciągów](./language-reference/tokens/interpolated.md) , aby utworzyć sformatowany ciąg dla pełnej nazwy.

Można również użyć *elementu członkowskiego z wyrażeniem*, który zapewnia bardziej zwięzły sposób tworzenia właściwości obliczanej `FullName` :

[!code-csharp[A computed property using an expression bodied member](../../samples/snippets/csharp/properties/Person.cs#11)]

*Składowe* w postaci wyrażeń, używają składni *wyrażenia lambda* do definiowania metod, które zawierają pojedyncze wyrażenie. To wyrażenie zwraca pełną nazwę obiektu osoby.

### <a name="cached-evaluated-properties"></a>Właściwości obliczone w pamięci podręcznej

Można zmieszać koncepcję obliczonej właściwości z magazynem i utworzyć *buforowaną Właściwość*.  Na przykład możesz zaktualizować `FullName` Właściwość tak, aby formatowanie ciągu było nastąpiło tylko podczas pierwszego dostępu:

[!code-csharp[Caching the value of a computed property](../../samples/snippets/csharp/properties/Person.cs#12)]

Powyższy kod zawiera usterkę. Jeśli kod aktualizuje wartość `FirstName` `LastName` właściwości lub, poprzednio oceniane `fullName` pole jest nieprawidłowe. Modyfikujesz metody `set` dostępu `FirstName` właściwości i, `LastName` Aby `fullName` pole zostało obliczone ponownie:

[!code-csharp[Invalidating the cache correctly](../../samples/snippets/csharp/properties/Person.cs#13)]

Ta wersja końcowa oblicza `FullName` Właściwość tylko w razie konieczności.
Jeśli wcześniejsza wersja obliczeniowa jest prawidłowa, jest używana. Jeśli inna zmiana stanu unieważnia wcześniej obliczoną wersję, zostanie ona obliczona ponownie. Deweloperzy korzystający z tej klasy nie muszą znać szczegółów implementacji. Żadna z tych zmian wewnętrznych nie ma wpływu na korzystanie z obiektu osoba. Jest to kluczowa przyczyna użycia właściwości, aby uwidocznić elementy członkowskie danych obiektu.

### <a name="attaching-attributes-to-auto-implemented-properties"></a>Dołączanie atrybutów do właściwości, które zostały zaimplementowane.

Począwszy od języka C# 7,3, atrybuty pola mogą być dołączane do pola zapasowego wygenerowanego przez kompilator we właściwościach, które są implementowane automatycznie. Na przykład rozważmy poprawkę `Person` klasy, która dodaje unikatową `Id` Właściwość Integer.
Należy napisać `Id` Właściwość przy użyciu właściwości, która jest zaimplementowana, ale projekt nie wywołuje się w celu utrwalenia `Id` właściwości. <xref:System.NonSerializedAttribute>Może być tylko dołączone do pól, a nie właściwości. Można dołączyć <xref:System.NonSerializedAttribute> do pola zapasowego `Id` właściwości przy użyciu `field:` specyfikatora dla atrybutu, jak pokazano w następującym przykładzie:

[!code-csharp[Attaching attributes to a backing field](../../samples/snippets/csharp/properties/Person.cs#14)]

Ta technika działa dla dowolnego atrybutu dołączanego do pola zapasowego we właściwości, która jest automatycznie implementowana.

### <a name="implementing-inotifypropertychanged"></a>Implementowanie INotifyPropertyChanged

Ostatnim scenariuszem, w którym należy napisać kod w metodzie dostępu do właściwości, jest obsługa <xref:System.ComponentModel.INotifyPropertyChanged> interfejsu używanego do powiadamiania klientów powiązań danych o zmianie wartości. Gdy wartość właściwości zostanie zmieniona, obiekt zgłasza <xref:System.ComponentModel.INotifyPropertyChanged.PropertyChanged?displayProperty=nameWithType> zdarzenie, aby wskazać zmianę. Biblioteki powiązań danych z kolei aktualizują elementy wyświetlane na podstawie tej zmiany. Poniższy kod przedstawia sposób implementacji `INotifyPropertyChanged` dla `FirstName` właściwości tej klasy osoby.

[!code-csharp[invalidating the cache correctly](../../samples/snippets/csharp/properties/Person.cs#15)]

`?.`Operator jest nazywany *operatorem warunkowym o wartości null*. Sprawdza odwołanie o wartości null przed dokonaniem oceny prawego boku operatora. Wynikiem tego jest to, że jeśli nie ma subskrybentów `PropertyChanged` zdarzenia, kod służący do podniesienia poziomu zdarzenia nie zostanie wykonany. W takim przypadku może zgłosić się `NullReferenceException` bez tego zaewidencjonowania. Aby uzyskać więcej informacji, zobacz [`events`](events-overview.md). Ten przykład używa także operatora new `nameof` do konwersji z symbolu nazwy właściwości na jego reprezentację tekstową.
Korzystanie z programu `nameof` może zmniejszyć liczbę błędów w przypadku błędnego wpisania nazwy właściwości.

<xref:System.ComponentModel.INotifyPropertyChanged>Z tego względu implementacja jest przykładem przypadku, w którym można napisać kod w metodzie dostępu do obsługi potrzebnych scenariuszy.

## <a name="summing-up"></a>Sumowanie

Właściwości są formą pól inteligentnych w klasie lub obiekcie. Z zewnątrz obiektu, są wyświetlane jak pola w obiekcie. Jednak właściwości można zaimplementować przy użyciu pełnej palety funkcji języka C#.
Możesz zapewnić weryfikację, różne dostępność, ocenę z opóźnieniem lub dowolne wymagania, których wymagają Twoje scenariusze.
