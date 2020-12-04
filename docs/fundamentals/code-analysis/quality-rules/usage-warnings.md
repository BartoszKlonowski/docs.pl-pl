---
title: Reguły użycia (analiza kodu)
description: Dowiedz się więcej na temat reguł użycia analizy kodu.
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.usagerules
helpviewer_keywords:
- rules, usage
- managed code analysis rules, usage rules
- usage rules
author: gewarren
ms.author: gewarren
ms.openlocfilehash: c8b14d2f92502d5a82e41a322e599745bdcf8b85
ms.sourcegitcommit: a6bd4cad438fe479cbd112eae10f2cd449f06e40
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/08/2020
ms.locfileid: "96589648"
---
# <a name="usage-rules"></a>Reguły użycia

Reguły użycia obsługują poprawne użycie platformy .NET.

## <a name="in-this-section"></a>W tej sekcji

|Reguła|Opis|
|----------|-----------------|
|[CA1801: Dokonaj przeglądu nieużywanych parametrów](ca1801.md)|Podpis metody zawiera parametr, który nie jest używany w jej treści.|
|[CA1816: Poprawnie wywołaj metodę GC.SuppressFinalize](ca1816.md)|Metoda, która jest implementacją metody Dispose, nie wywołuje `GC.SuppressFinalize` metody lub metoda, która nie jest implementacją `Dispose` wywołań `GC.SuppressFinalize` ; lub metoda wywołuje `GC.SuppressFinalize` i przekazuje coś innego niż `this` ( `Me` w Visual Basic).|
|[CA2200: Ponowie zgłoś wyjątek, aby zachować szczegóły stosu](ca2200.md)|Wyjątek jest zgłaszany ponownie i jest on jawnie określony w instrukcji „throw”. Jeśli wyjątek jest zgłaszany ponownie przez określenie wyjątku w instrukcji „throw”, lista wywołań metod między pierwotną metodą, która zgłosiła wyjątek, a bieżącą zostanie utracona.|
|[CA2201: Nie zgłaszaj wyjątków o zastrzeżonych typach](ca2201.md)|Powoduje to, że oryginalny błąd trudno wykryć i debugować.|
|[CA2207: Pola statyczne typu wartości inicjuj bezpośrednio](ca2207.md)|Typ wartości deklaruje jawny, statyczny konstruktor. Aby naprawić naruszenie tej zasady, zainicjuj wszystkie dane statyczne, gdy jest on zadeklarowany, i usuń konstruktor statyczny.|
|[CA2208: Poprawnie twórz wystąpienia wyjątków argumentów](ca2208.md)|Wywołanie odnosi się do domyślnego (bezparametrowego) konstruktora typu wyjątku, który jest elementem ArgumentException lub od niego pochodzi, albo niepoprawny argument ciągu jest przekazywany do sparametryzowania konstruktora typu wyjątku lub pochodzi od elementu ArgumentException.|
|[CA2211: Pola niebędące stałymi nie powinny być widoczne](ca2211.md)|Pola statyczne, które nie są stałymi lub tylko do odczytu, nie są bezpieczne wątkowo. Dostęp do takiego pola musi być starannie kontrolowany i wymaga zaawansowanych technik programowania do synchronizowania dostępu do obiektu klasy.|
|[CA2213: Pola możliwe do likwidacji należy likwidować](ca2213.md)|Typ, który implementuje <xref:System.IDisposable?displayProperty=fullName> deklarowane pola, które są typu, które również implementują `IDisposable` . `Dispose`Metoda pola nie jest wywoływana przez `Dispose` metodę typu deklarującego.|
|[CA2214: Nie wywołuj w konstruktorach metod, które można przesłaniać](ca2214.md)|Gdy Konstruktor wywołuje metodę wirtualną, istnieje możliwość, że Konstruktor wystąpienia, który wywołuje metodę, nie został wykonany.|
|[CA2215: Metody Dispose powinny wywoływać metodę Dispose klasy bazowej](ca2215.md)|Jeśli typ dziedziczy z typu jednorazowego, musi wywołać `Dispose` metodę typu podstawowego z własnej `Dispose` metody.|
|[CA2216: Typy możliwe do likwidacji powinny deklarować finalizator](ca2216.md)|Typ, który implementuje <xref:System.IDisposable?displayProperty=fullName> i ma pola, które sugerują użycie niezarządzanych zasobów, nie implementuje finalizatora, zgodnie z opisem przez `Object.Finalize` .|
|[CA2217: Nie oznaczaj typów wyliczeniowych atrybutem Flags](ca2217.md)|Widoczne na zewnątrz Wyliczenie jest oznaczone `FlagsAttribute` i ma co najmniej jedną wartość, która nie ma uprawnień dwóch lub kombinacji innych zdefiniowanych wartości w wyliczeniu.|
|[CA2218: Przesłaniaj metodę GetHashCode w razie przesłaniania metody Equals](ca2218.md)|Typ publiczny przesłania, <xref:System.Object.Equals%2A?displayProperty=fullName> ale nie przesłania <xref:System.Object.GetHashCode%2A?displayProperty=fullName> .|
|[CA2219: Nie zgłaszaj wyjątków w klauzulach wyjątków](ca2219.md)|Kiedy wyjątek jest zgłaszany w klauzuli „finally” lub „fault”, nowy wyjątek ukrywa aktywny wyjątek. Gdy wyjątek jest zgłaszany w klauzuli „filter”, środowisko uruchomieniowe dyskretnie przechwytuje wyjątek. Powoduje to, że oryginalny błąd trudno wykryć i debugować.|
|[CA2224: Przesłaniaj metodę equals w przypadku przeciążania operatora równości](ca2224.md)|Typ publiczny implementuje operator równości, ale nie przesłania <xref:System.Object.Equals%2A?displayProperty=fullName> .|
|[CA2225: Przeciążenia operatorów mają nazwane elementy alternatywne](ca2225.md)|Wykryto przeciążony operator i nie znaleziono metody alternatywnej o oczekiwanej nazwie. Nazwany alternatywny element członkowski zapewnia dostęp do tych samych funkcji co operator i jest udostępniany deweloperom programu w językach, które nie obsługują przeciążonych operatorów.|
|[CA2226: Operatory powinny mieć symetryczne przeciążenia](ca2226.md)|Typ implementuje operator równości lub nierówności i nie implementuje operatora przeciwległego.|
|[CA2227: Właściwości kolekcji powinny być tylko do odczytu](ca2227.md)|Właściwość zapisywalnej kolekcji pozwala użytkownikowi zastąpić kolekcję inną kolekcją. Właściwość tylko do odczytu uniemożliwia zastępowanie kolekcji, ale nadal umożliwia ustawienie poszczególnych członków.|
|[CA2229: Zaimplementuj konstruktory serializacji](ca2229.md)|Aby naprawić naruszenie tej zasady, należy zaimplementować konstruktora serializacji. Dla zamkniętej klasy należy ustawić konstruktor prywatny; w przeciwnym razie powinien być chroniony.|
|[CA2231: Przeciążaj operator równości w przypadku przesłaniania metody ValueType.Equals](ca2231.md)|Typ wartości przesłania `Object.Equals` , ale nie implementuje operatora równości.|
|[CA2234: Przekazuj obiekty System.Uri zamiast ciągów](ca2234.md)|Wykonano wywołanie do metody, która ma parametr typu ciąg, którego nazwa zawiera „uri”, „URI”, „urn”, „URN”, „url” lub „URL”.  Typ deklarujący metody zawiera odpowiadające Przeciążenie metody z <xref:System.Uri?displayProperty=fullName> parametrem.|
|[CA2235: Oznacz wszystkie pola nieprzeznaczone do serializacji](ca2235.md)|Pola wystąpienia typu, który nie może być serializowany, jest zadeklarowany w typie, który jest możliwy do serializacji.|
|[CA2237: Oznacz typy ISerializable atrybutem SerializableAttribute](ca2237.md)|Aby można było rozpoznać przez środowisko uruchomieniowe języka wspólnego jako możliwy do serializacji, typy muszą być oznaczone atrybutem SerializableAttribute, nawet jeśli typ używa niestandardowej procedury serializacji za pośrednictwem implementacji `ISerializable` interfejsu.|
|[CA2241: Podaj poprawne argumenty metod formatowania](ca2241.md)|Argument formatu przesłany do <xref:System.String.Format%2A?displayProperty=nameWithType> nie zawiera elementu formatu, który odnosi się do każdego argumentu obiektu lub odwrotnie.|
|[CA2242: Poprawnie testuj nie-liczby (NaN)](ca2242.md)|To wyrażenie służy do testowania wartości w odniesieniu do `Single.Nan` lub `Double.Nan` . Użyj `Single.IsNan(Single)` lub, `Double.IsNan(Double)` Aby przetestować wartość.|
|[CA2243: Analiza literałów ciągów atrybutów powinna przebiegać poprawnie](ca2243.md)|Parametr literału ciągu atrybutu nie jest analizowany poprawnie dla adresu URL, identyfikatora GUID lub wersji.|
|[CA2244: Nie duplikuj inicjowania indeksowanych elementów](ca2244.md)|Inicjator obiektu ma więcej niż jeden indeks elementu indeksowanego z tym samym indeksem stałym. Wszystkie oprócz ostatniego inicjatora są nadmiarowe.|
|[CA2245: Nie przypisuj właściwości do jej samej](ca2245.md)|Właściwość została przypadkowo przypisana do samej siebie.|
|[CA2246: Nie przypisuj symbolu i jego składowej w tej samej instrukcji](ca2246.md)|Przypisanie symbolu i jego elementu członkowskiego, czyli pola lub właściwości, w tej samej instrukcji nie jest zalecane. Nie jest jasne, jeśli dostęp do elementu członkowskiego był przeznaczony do użycia starej wartości symbolu przed przypisaniem lub nową wartością z przypisania w tej instrukcji.|
|[CA2247: Argument przekazany do konstruktora TaskCompletionSource musi być wyliczeniem TaskCreationOptions, a nie wyliczeniem TaskContinuationOptions](ca2246.md)|TaskCompletionSource ma konstruktory, które przyjmują opcji TaskCreationOptions, które kontrolują podstawowe zadanie, i konstruktorów, które przyjmują stan obiektu, który jest przechowywany w zadaniu.  Przypadkowe przekazanie TaskContinuationOptions zamiast opcji TaskCreationOptions spowoduje wywołanie opcji jako stanu.|
|[CA2248: Podaj poprawny argument "enum" dla elementu "enum. HasFlag"](ca2248.md)|Typ wyliczeniowy przesłany jako argument `HasFlag` wywołania metody różni się od typu wyliczeniowego wywołującego.|
|[CA2249: Rozważ użycie metody String.Contains zamiast String.IndexOf](ca2249.md)|Wywołania, do `string.IndexOf` których wynik służy do sprawdzania obecności lub braku podciągu, mogą zostać zastąpione przez `string.Contains` .|
