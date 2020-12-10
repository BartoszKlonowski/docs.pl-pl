---
title: Implementacja metody DisposeAsync
description: Dowiedz się, jak zaimplementować metody DisposeAsync i DisposeAsyncCore, aby przeprowadzić Oczyszczanie zasobów asynchronicznych.
author: IEvangelist
ms.author: dapine
ms.date: 12/09/2020
dev_langs:
- csharp
helpviewer_keywords:
- DisposeAsync method
- garbage collection, DisposeAsync method
ms.openlocfilehash: f04ac6695864b96cdcb7efeb6eb8e1d9551e1d14
ms.sourcegitcommit: 81f1bba2c97a67b5ca76bcc57b37333ffca60c7b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/10/2020
ms.locfileid: "97009693"
---
# <a name="implement-a-disposeasync-method"></a>Implementacja metody DisposeAsync

<xref:System.IAsyncDisposable?displayProperty=nameWithType>Interfejs został wprowadzony jako część języka C# 8,0. Metodę należy zaimplementować <xref:System.IAsyncDisposable.DisposeAsync?displayProperty=nameWithType> , gdy trzeba przeprowadzić Oczyszczanie zasobów, tak jak podczas [implementowania metody Dispose](implementing-dispose.md). Jedną z najważniejszych różnic jest jednak to, że ta implementacja umożliwia asynchroniczne czyszczenie operacji. <xref:System.IAsyncDisposable.DisposeAsync>Zwraca wartość <xref:System.Threading.Tasks.ValueTask> reprezentującą asynchroniczną operację Dispose.

Typowym scenariuszem jest implementowanie <xref:System.IAsyncDisposable> interfejsu, który klasy również implementują <xref:System.IDisposable> interfejs. Dobry wzorzec implementacji <xref:System.IAsyncDisposable> interfejsu jest przygotowany do synchronicznej lub asynchronicznej operacji Dispose. Wszystkie wskazówki dotyczące wdrażania wzorca Dispose dotyczą również implementacji asynchronicznej. W tym artykule założono, że wiesz już, jak [zaimplementować metodę Dispose](implementing-dispose.md).

## <a name="disposeasync-and-disposeasynccore"></a>DisposeAsync () i DisposeAsyncCore ()

<xref:System.IAsyncDisposable>Interfejs deklaruje pojedynczą metodę bez parametrów, <xref:System.IAsyncDisposable.DisposeAsync> . Każda Klasa Niezapieczętowana powinna mieć dodatkową `DisposeAsyncCore()` metodę, która również zwraca wartość <xref:System.Threading.Tasks.ValueTask> .

- `public` <xref:System.IAsyncDisposable.DisposeAsync?displayProperty=nameWithType> Implementacja, która nie ma parametrów.
- `protected virtual ValueTask DisposeAsyncCore()`Metoda, której sygnatura:

  ```csharp
  protected virtual ValueTask DisposeAsyncCore()
  {
  }
  ```

### <a name="the-disposeasync-method"></a>DisposeAsync () — Metoda

`public` `DisposeAsync()` Metoda bez parametrów jest wywoływana niejawnie w `await using` instrukcji i jej celem jest zwolnienie niezarządzanych zasobów, wykonanie ogólnego czyszczenia i wskazanie, że finalizator, jeśli taki istnieje, nie musi być uruchomiony. Zwalnianie pamięci skojarzonej z zarządzanym obiektem jest zawsze domeną [modułu wyrzucania elementów bezużytecznych](index.md). Z tego powodu ma standardową implementację:

```csharp
public async ValueTask DisposeAsync()
{
    // Perform async cleanup.
    await DisposeAsyncCore();

    // Dispose of unmanaged resources.
    Dispose(false);
    // Suppress finalization.
    GC.SuppressFinalize(this);
}
```

> [!NOTE]
> Podstawowa różnica w asynchronicznym wzorcu usuwania w porównaniu do wzorca Dispose polega na tym, że wywołanie z <xref:System.IAsyncDisposable.DisposeAsync> `Dispose(bool)` metody przeciążenia jest podawane `false` jako argument. Podczas implementowania <xref:System.IDisposable.Dispose?displayProperty=nameWithType> metody, jednak `true` jest przenoszona zamiast. Dzięki temu można zapewnić równoważność funkcjonalną z synchronicznym wzorcem usuwania, a dodatkowo zapewnić, że ścieżki kodu finalizatora nadal są wywoływane. Innymi słowy, `DisposeAsyncCore()` Metoda usunie zarządzane zasoby asynchronicznie, więc nie ma potrzeby ich synchronicznego usuwania. W związku `Dispose(false)` z tym zamiast `Dispose(true)` .

### <a name="the-disposeasynccore-method"></a>DisposeAsyncCore () — Metoda

`DisposeAsyncCore()`Metoda jest przeznaczona do przeprowadzania asynchronicznego oczyszczania zarządzanych zasobów lub łączenia kaskadowego z `DisposeAsync()` . Hermetyzuje typowe asynchroniczne operacje czyszczenia, gdy Podklasa dziedziczy klasę bazową, która jest implementacją <xref:System.IAsyncDisposable> . `DisposeAsyncCore()`Metoda polega na `virtual` tym, że klasy pochodne mogą definiować dodatkowe czyszczenie w ich zastąpień.

> [!TIP]
> Jeśli implementacja programu <xref:System.IAsyncDisposable> ma wartość `sealed` , `DisposeAsyncCore()` Metoda nie jest wymagana, a oczyszczanie asynchroniczne można wykonać bezpośrednio w <xref:System.IAsyncDisposable.DisposeAsync?displayProperty=nameWithType> metodzie.

## <a name="implement-the-async-dispose-pattern"></a>Implementowanie wzorca usuwania asynchronicznego

Wszystkie niezapieczętowane klasy należy traktować jako potencjalną klasę bazową, ponieważ mogą one być dziedziczone. W przypadku zaimplementowania wzorca usuwania asynchronicznego dla dowolnej potencjalnej klasy podstawowej należy podać `protected virtual ValueTask DisposeAsyncCore()` metodę. Oto Przykładowa implementacja asynchronicznego wzorca Dispose, który używa <xref:System.Text.Json.Utf8JsonWriter?displayProperty=nameWithType> .

:::code language="csharp" source="../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.asyncdisposable/disposeasync.cs":::

Poprzedni przykład używa <xref:System.Text.Json.Utf8JsonWriter> . Aby uzyskać więcej informacji o `System.Text.Json` programie, zobacz [Jak przeprowadzić migrację z Newtonsoft.Js, aby System.Text.Js](../serialization/system-text-json-migrate-from-newtonsoft-how-to.md).

## <a name="implement-both-dispose-and-async-dispose-patterns"></a>Implementuj wzorce usuwania operacji Dispose i Async

Może być konieczne zaimplementowanie obu <xref:System.IDisposable> <xref:System.IAsyncDisposable> interfejsów i, szczególnie gdy zakres klasy zawiera wystąpienia tych implementacji. Dzięki temu można prawidłowo kaskadowo wyczyścić wywołania. Oto przykładowa Klasa implementująca oba interfejsy i demonstrująca odpowiednie wskazówki dotyczące czyszczenia.

:::code language="csharp" source="../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.asyncdisposable/dispose-and-disposeasync.cs":::

<xref:System.IDisposable.Dispose?displayProperty=nameWithType> <xref:System.IAsyncDisposable.DisposeAsync?displayProperty=nameWithType> Implementacje i są prostym kodem niezwykłym.

W `Dispose(bool)` metodzie przeciążenia <xref:System.IDisposable> wystąpienie jest warunkowo usuwane, jeśli nie jest `null` . <xref:System.IAsyncDisposable>Wystąpienie jest rzutowane jako <xref:System.IDisposable> , a jeśli nie `null` , również jest usuwane. Oba wystąpienia są następnie przypisywane do `null` .

Przy użyciu `DisposeAsyncCore()` metody jest stosowane takie samo podejście logiczne. Jeśli <xref:System.IAsyncDisposable> wystąpienie nie jest `null` , jego wywołanie `DisposeAsync().ConfigureAwait(false)` jest oczekiwane. Jeśli <xref:System.IDisposable> wystąpienie jest również implementacją programu <xref:System.IAsyncDisposable> , jest również usuwane asynchronicznie. Oba wystąpienia są następnie przypisywane do `null` .

## <a name="using-async-disposable"></a>Korzystanie z asynchronicznej operacji jednorazowej

Aby prawidłowo korzystać z obiektu, który implementuje <xref:System.IAsyncDisposable> interfejs, należy użyć słów kluczowych [await](../../csharp/language-reference/operators/await.md) i [using](../../csharp/language-reference/keywords/using-statement.md) ze sobą. Rozważmy następujący przykład, w którym `ExampleAsyncDisposable` tworzona jest instancja klasy, a następnie zawinięte w `await using` instrukcji.

:::code language="csharp" source="../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.asyncdisposable/proper-await-using.cs":::

> [!IMPORTANT]
> Użyj <xref:System.Threading.Tasks.TaskAsyncEnumerableExtensions.ConfigureAwait(System.IAsyncDisposable,System.Boolean)> metody rozszerzenia <xref:System.IAsyncDisposable> interfejsu, aby skonfigurować sposób przyprowadzenia zadania do jego oryginalnego kontekstu lub harmonogramu. Aby uzyskać więcej informacji na temat `ConfigureAwait` , zobacz temat [ConfigureAwait — często zadawane pytania](https://devblogs.microsoft.com/dotnet/configureawait-faq/).

W sytuacjach, gdy użycie `ConfigureAwait` nie jest wymagane, `await using` instrukcja może być uproszczona w następujący sposób:

:::code language="csharp" source="../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.asyncdisposable/await-using-non-configureawait.cs":::

Ponadto można napisać, aby użyć niejawnego zakresu [deklaracji using](../../csharp/whats-new/csharp-8.md#using-declarations).

:::code language="csharp" source="../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.asyncdisposable/await-using-declaration.cs":::

## <a name="stacked-usings"></a>Stos użycia

W sytuacjach, gdy tworzysz i używasz wielu obiektów, które implementują <xref:System.IAsyncDisposable> , istnieje możliwość, że `await using` instrukcje stosujące <xref:System.Threading.Tasks.ValueTask.ConfigureAwait%2A> mogą uniemożliwiać wywołania <xref:System.IAsyncDisposable.DisposeAsync> w warunkach errant. Aby upewnić <xref:System.IAsyncDisposable.DisposeAsync> się, że jest zawsze wywoływana, należy unikać tworzenia stosów. Poniższe trzy przykłady kodu pokazują akceptowalne wzorce do użycia.

### <a name="acceptable-pattern-one"></a>Akceptowalny wzorzec 1

:::code language="csharp" id="one" source="../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.asyncdisposable/stacked-await-usings.cs":::

W poprzednim przykładzie każda operacja czyszczenia asynchronicznego została jawnie objęta zakresem w `await using` bloku. Zakres zewnętrzny jest definiowany przez sposób, w jaki `objOne` ustawia swoje nawiasy klamrowe, `objTwo` w związku z czym `objTwo` najpierw jest usuwany, a następnie `objOne` . `IAsyncDisposable`W obu wystąpieniach istnieją <xref:System.IAsyncDisposable.DisposeAsync> metody oczekujące na wykonanie asynchronicznej operacji czyszczenia. Wywołania są zagnieżdżone, a nie ułożone na stosie.

### <a name="acceptable-pattern-two"></a>Akceptowalny wzorzec dwa

:::code language="csharp" id="two" source="../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.asyncdisposable/stacked-await-usings.cs":::

W poprzednim przykładzie każda operacja czyszczenia asynchronicznego została jawnie objęta zakresem w `await using` bloku. Na końcu każdego bloku odpowiednie `IAsyncDisposable` wystąpienie ma <xref:System.IAsyncDisposable.DisposeAsync> oczekiwaną metodę, w związku z czym wykonuje operację czyszczenia asynchronicznego. Wywołania są sekwencyjne, nie stosują się. W tym scenariuszu najpierw zostanie usunięty `objOne` `objTwo` .

### <a name="acceptable-pattern-three"></a>Akceptowalny wzorzec trzy

:::code language="csharp" id="three" source="../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.asyncdisposable/stacked-await-usings.cs":::

W poprzednim przykładzie każda operacja czyszczenia asynchronicznego jest niejawnie objęta zakresem treści metody zawierającej. Na końcu otaczającego bloku `IAsyncDisposable` wystąpienia wykonują asynchroniczne operacje czyszczenia. Ten przebiega w kolejności odwrotnej, z której zostały zadeklarowane, co oznacza, że `objTwo` jest usuwane przed `objOne` .

### <a name="unacceptable-pattern"></a>Nieakceptowalny wzorzec

Jeśli wystąpi wyjątek z `AnotherAsyncDisposable` konstruktora, program nie zostanie `objOne` prawidłowo usunięty:

:::code language="csharp" id="dontdothis" source="../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.asyncdisposable/stacked-await-usings.cs":::

> [!TIP]
> Należy unikać tego wzorca, ponieważ może to prowadzić do nieoczekiwanego zachowania.

## <a name="see-also"></a>Zobacz także

Aby zapoznać się z dwoma przykładami implementacji `IDisposable` i `IAsyncDisposable` , zobacz <xref:System.Text.Json.Utf8JsonWriter> kod źródłowy [w witrynie GitHub](https://github.com/dotnet/runtime/blob/035b729d829368c2790d825bd02db14f0c0fd2ea/src/libraries/System.Text.Json/src/System/Text/Json/Writer/Utf8JsonWriter.cs#L297-L345).

- <xref:System.IAsyncDisposable>
- <xref:System.IAsyncDisposable.DisposeAsync?displayProperty=nameWithType>
- <xref:System.Threading.Tasks.TaskAsyncEnumerableExtensions.ConfigureAwait(System.IAsyncDisposable,System.Boolean)>
