---
title: Jak pisać konwertery niestandardowe na potrzeby serializacji JSON — .NET
description: Dowiedz się, jak utworzyć niestandardowe konwertery dla klas serializacji JSON, które są dostępne w System.Text.Json przestrzeni nazw.
ms.date: 11/30/2020
no-loc:
- System.Text.Json
- Newtonsoft.Json
zone_pivot_groups: dotnet-version
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
- converters
ms.openlocfilehash: 17671b86dc6d1d7b45a01cb0bf7c5c42f624d99f
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96438118"
---
# <a name="how-to-write-custom-converters-for-json-serialization-marshalling-in-net"></a>Jak pisać konwertery niestandardowe na potrzeby serializacji JSON (kierowanie) w programie .NET

W tym artykule pokazano, jak utworzyć niestandardowe konwertery dla klas serializacji JSON, które są dostępne w <xref:System.Text.Json> przestrzeni nazw. Wprowadzenie do programu można `System.Text.Json` znaleźć [w temacie jak serializować i DESERIALIZOWAĆ kod JSON w programie .NET](system-text-json-how-to.md).

*Konwerter* jest klasą, która konwertuje obiekt lub wartość do i z formatu JSON. `System.Text.Json`Przestrzeń nazw ma wbudowane konwertery dla większości typów pierwotnych, które są mapowane na elementy pierwotne języka JavaScript. Możesz pisać niestandardowe konwertery:

* Aby zastąpić domyślne zachowanie konwertera wbudowanego. Na przykład, możesz chcieć `DateTime` przedstawić wartości w formacie mm/dd/rrrr zamiast domyślnego formatu ISO 8601-1:2019.
* Do obsługi niestandardowego typu wartości. Na przykład `PhoneNumber` Struktura.

Możesz również napisać niestandardowe konwertery, aby dostosować lub zwiększyć `System.Text.Json` funkcjonalność, która nie jest uwzględniona w bieżącej wersji. Poniższe scenariusze zostały omówione w dalszej części tego artykułu:

::: zone pivot="dotnet-5-0"

* [Deserializacja wywnioskowanych typów do właściwości obiektu](#deserialize-inferred-types-to-object-properties).
* [Obsługa deserializacji polimorficznej](#support-polymorphic-deserialization).
* [Obsługa rundy dla stosu \<T> ](#support-round-trip-for-stackt).
::: zone-end

::: zone pivot="dotnet-core-3-1"

* [Deserializacja wywnioskowanych typów do właściwości obiektu](#deserialize-inferred-types-to-object-properties).
* [Obsługa słownika z kluczem niebędącym ciągiem](#support-dictionary-with-non-string-key).
* [Obsługa deserializacji polimorficznej](#support-polymorphic-deserialization).
* [Obsługa rundy dla stosu \<T> ](#support-round-trip-for-stackt).
::: zone-end

## <a name="custom-converter-patterns"></a>Wzorce niestandardowego konwertera

Istnieją dwa wzorce do tworzenia niestandardowego konwertera: wzorzec podstawowy i wzorzec fabryki. Wzorzec fabryki jest przeznaczony dla konwerterów, które obsługują typ `Enum` lub otwierają typy ogólne. Wzorzec podstawowy dotyczy typów ogólnych nieogólnych i zamkniętych.  Na przykład konwertery dla następujących typów wymagają wzorca fabryki:

* <xref:System.Collections.Generic.Dictionary%602>
* <xref:System.Enum>
* <xref:System.Collections.Generic.List%601>

Niektóre przykłady typów, które mogą być obsługiwane przez wzorzec Basic, obejmują:

* `Dictionary<int, string>`
* `WeekdaysEnum`
* `List<DateTimeOffset>`
* <xref:System.DateTime>
* <xref:System.Int32>

Wzorzec podstawowy tworzy klasę, która może obsługiwać jeden typ. Wzorzec fabryki tworzy klasę, która określa, w czasie wykonywania, który określony typ jest wymagany i dynamicznie tworzy odpowiedni konwerter.

## <a name="sample-basic-converter"></a>Przykładowy konwerter podstawowy

Poniższy przykład to konwerter, który zastąpi domyślną serializację dla istniejącego typu danych. Konwerter używa formatu mm/dd/rrrr dla `DateTimeOffset` właściwości.

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/DateTimeOffsetConverter.cs":::

## <a name="sample-factory-pattern-converter"></a>Przykładowy konwerter wzorców fabryki

Poniższy kod przedstawia niestandardowy konwerter, który współpracuje z `Dictionary<Enum,TValue>` . Kod jest zgodny z wzorcem fabryki, ponieważ pierwszy parametr typu ogólnego to `Enum` , a drugi jest otwarty. `CanConvert`Metoda zwraca `true` tylko dla `Dictionary` z dwoma parametrami ogólnymi, z których pierwszy jest `Enum` typem. Wewnętrzny konwerter pobiera istniejący konwerter do obsługi dowolnego typu w czasie wykonywania dla `TValue` .

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/DictionaryTKeyEnumTValueConverter.cs":::

Poprzedni kod jest taki sam jak w [słowniku pomocy technicznej z kluczem innym niż ciąg](#support-dictionary-with-non-string-key) w dalszej części tego artykułu.

## <a name="steps-to-follow-the-basic-pattern"></a>Kroki prowadzące do wzorca podstawowego

Poniższe kroki wyjaśniają, jak utworzyć konwerter, wykonując następujące czynności:

* Utwórz klasę, która pochodzi od elementu WHERE, który <xref:System.Text.Json.Serialization.JsonConverter%601> `T` ma być serializowany i deserializowany.
* Zastąp `Read` metodę w celu deserializacji przychodzącego pliku JSON i przekonwertuj go na typ `T` . Użyj <xref:System.Text.Json.Utf8JsonReader> , która jest przenoszona do metody odczytu JSON.
* Zastąp `Write` metodę, aby serializować obiekt przychodzący typu `T` . Użyj <xref:System.Text.Json.Utf8JsonWriter> , która jest przenoszona do metody, aby zapisać kod JSON.
* Zastąp `CanConvert` metodę tylko w razie potrzeby. Domyślna implementacja zwraca, `true` gdy typ do konwersji jest typem `T` . W związku z tym konwertery obsługujące tylko typ `T` nie muszą przesłaniać tej metody. Aby zapoznać się z przykładem konwertera, który musi przesłonić tę metodę, zobacz sekcję [deserializacji polimorficzną](#support-polymorphic-deserialization) w dalszej części tego artykułu.

Możesz odwołać się do [wbudowanego kodu źródłowego konwerterów](https://github.com/dotnet/runtime/tree/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/src/System/Text/Json/Serialization/Converters/) jako implementacji odwołań do pisania konwerterów niestandardowych.

## <a name="steps-to-follow-the-factory-pattern"></a>Kroki prowadzące do wzorca fabryki

Poniższe kroki wyjaśniają, jak utworzyć konwerter, postępując zgodnie z wzorcem fabryki:

* Utwórz klasę, która pochodzi od <xref:System.Text.Json.Serialization.JsonConverterFactory> .
* Zastąp `CanConvert` metodę, aby zwracał wartość true, gdy typ do przekonwertowania jest taki, który może obsłużyć konwerter. Na przykład, jeśli konwerter jest przeznaczony dla `List<T>` , może obsłużyć tylko `List<int>` , `List<string>` i `List<DateTime>` .
* Zastąp `CreateConverter` metodę, aby zwrócić wystąpienie klasy konwertera, która będzie obsługiwała typ do konwersji, który jest dostarczany w czasie wykonywania.
* Utwórz klasę konwertera, którą `CreateConverter` tworzy wystąpienie metody.

Wzorzec fabryki jest wymagany do otwierania typów ogólnych, ponieważ kod do konwersji obiektu na i z ciągu nie jest taki sam dla wszystkich typów. Konwerter dla otwartego typu ogólnego ( `List<T>` na przykład) musi utworzyć konwerter dla zamkniętego typu ogólnego ( `List<DateTime>` na przykład) w tle. Kod musi być zapisany, aby obsługiwał każdy zamknięty typ ogólny, który może obsłużyć konwerter.

`Enum`Typ jest podobny do otwartego typu ogólnego: konwerter dla programu `Enum` musi utworzyć konwerter dla określonego `Enum` ( `WeekdaysEnum` na przykład) w tle.

## <a name="error-handling"></a>Obsługa błędów

Jeśli musisz zgłosić wyjątek w kodzie obsługi błędu, rozważ przegenerowanie <xref:System.Text.Json.JsonException> bez komunikatu. Ten typ wyjątku powoduje automatyczne utworzenie komunikatu zawierającego ścieżkę do części JSON, która spowodowała błąd. Na przykład instrukcja `throw new JsonException();` generuje komunikat o błędzie, jak w poniższym przykładzie:

```output
Unhandled exception. System.Text.Json.JsonException:
The JSON value could not be converted to System.Object.
Path: $.Date | LineNumber: 1 | BytePositionInLine: 37.
```

Jeśli zostanie wyświetlony komunikat (na przykład `throw new JsonException("Error occurred")` , wyjątek nadal zapewnia ścieżkę we <xref:System.Text.Json.JsonException.Path> właściwości.

## <a name="register-a-custom-converter"></a>Rejestrowanie niestandardowego konwertera

*Zarejestruj* konwerter niestandardowy, aby `Serialize` `Deserialize` zastosować metody i. Wybierz jedną z następujących metod:

* Dodaj wystąpienie klasy Converter do <xref:System.Text.Json.JsonSerializerOptions.Converters?displayProperty=nameWithType> kolekcji.
* Zastosuj atrybut [[JsonConverter]](xref:System.Text.Json.Serialization.JsonConverterAttribute) do właściwości, które wymagają konwertera niestandardowego.
* Zastosuj atrybut [[JsonConverter]](xref:System.Text.Json.Serialization.JsonConverterAttribute) do klasy lub struktury, która reprezentuje niestandardowy typ wartości.

## <a name="registration-sample---converters-collection"></a>Przykład rejestracji — kolekcja konwerterów

Oto przykład, który sprawia, że <xref:System.ComponentModel.DateTimeOffsetConverter> domyślne właściwości typu <xref:System.DateTimeOffset> :

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RegisterConverterWithConvertersCollection.cs" id="Serialize":::

Załóżmy, że Serializacja wystąpienia następującego typu:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WF":::

Oto przykład danych wyjściowych JSON, które pokazują, że użyto niestandardowego konwertera:

```json
{
  "Date": "08/01/2019",
  "TemperatureCelsius": 25,
  "Summary": "Hot"
}
```

Poniższy kod używa tego samego podejścia do deserializacji przy użyciu niestandardowego `DateTimeOffset` konwertera:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RegisterConverterWithConvertersCollection.cs" id="Deserialize":::

## <a name="registration-sample---jsonconverter-on-a-property"></a>Przykład rejestracji — [JsonConverter] na właściwości

Poniższy kod wybiera niestandardowy konwerter dla `Date` Właściwości:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithConverterAttribute":::

Kod do serializacji `WeatherForecastWithConverterAttribute` nie wymaga użycia `JsonSerializeOptions.Converters` :

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RegisterConverterWithAttributeOnProperty.cs" id="Serialize":::

Kod do deserializacji również nie wymaga użycia `Converters` :

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RegisterConverterWithAttributeOnProperty.cs" id="Deserialize":::

## <a name="registration-sample---jsonconverter-on-a-type"></a>Przykład rejestracji — [JsonConverter] w typie

Tutaj kod, który tworzy strukturę i stosuje `[JsonConverter]` do niego atrybut:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/Temperature.cs":::

Oto niestandardowy konwerter dla poprzedniej struktury:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/TemperatureConverter.cs":::

`[JsonConvert]`Atrybut w strukturze rejestruje niestandardowy konwerter jako domyślny dla właściwości typu `Temperature` . Konwerter jest automatycznie używany we `TemperatureCelsius` Właściwości następującego typu podczas serializacji lub deserializacji:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithTemperatureStruct":::

## <a name="converter-registration-precedence"></a>Pierwszeństwo rejestracji konwertera

Podczas serializacji lub deserializacji konwerter jest wybierany dla każdego elementu JSON w następującej kolejności, na podstawie najwyższego priorytetu:

* `[JsonConverter]` zastosowano do właściwości.
* Konwerter dodany do `Converters` kolekcji.
* `[JsonConverter]` stosowane do niestandardowego typu wartości lub POCO.

Jeśli wiele konwerterów niestandardowych dla typu są zarejestrowane w `Converters` kolekcji, używany jest pierwszy konwerter zwracający wartość true dla `CanConvert` .

Wbudowany konwerter jest wybierany tylko wtedy, gdy nie zarejestrowano żadnego odpowiedniego konwertera niestandardowego.

## <a name="converter-samples-for-common-scenarios"></a>Przykłady konwerterów dla typowych scenariuszy

Poniższe sekcje zawierają przykłady konwerterów, które dotyczą niektórych typowych scenariuszy, które nie obsługują funkcji wbudowanych.

::: zone pivot="dotnet-5-0"

* [Deserializacja wywnioskowanych typów do właściwości obiektu](#deserialize-inferred-types-to-object-properties).
* [Obsługa deserializacji polimorficznej](#support-polymorphic-deserialization).
* [Obsługa rundy dla stosu \<T> ](#support-round-trip-for-stackt).
::: zone-end

::: zone pivot="dotnet-core-3-1"

* [Deserializacja wywnioskowanych typów do właściwości obiektu](#deserialize-inferred-types-to-object-properties).
* [Obsługa słownika z kluczem niebędącym ciągiem](#support-dictionary-with-non-string-key).
* [Obsługa deserializacji polimorficznej](#support-polymorphic-deserialization).
* [Obsługa rundy dla stosu \<T> ](#support-round-trip-for-stackt).
::: zone-end

### <a name="deserialize-inferred-types-to-object-properties"></a>Deserializacja wywnioskowanych typów do właściwości obiektu

Podczas deserializacji do właściwości typu `object` , `JsonElement` tworzony jest obiekt. Przyczyną jest to, że Deserializator nie wie, jakie typy CLR należy utworzyć, i nie próbuje go odgadnąć. Na przykład, jeśli właściwość JSON ma wartość "true", Deserializator nie uzna, że wartość jest a `Boolean` , a jeśli element ma "01/01/2019", Deserializator nie uzna, że jest to `DateTime` .

Wnioskowanie o typie może być niedokładne. Jeśli Deserializator analizuje numer JSON, który nie ma punktu dziesiętnego jako `long` , co może spowodować problemy poza zakresem, jeśli wartość została pierwotnie zserializowana jako `ulong` lub `BigInteger` . Analizowanie liczby, która ma przecinek dziesiętny w postaci, `double` może spowodować utratę precyzji, jeśli liczba została pierwotnie zserializowana jako `decimal` .

W przypadku scenariuszy, które wymagają wnioskowania o typie, poniższy kod przedstawia niestandardowy konwerter `object` właściwości. Kod konwertuje:

* `true` i `false` do `Boolean`
* Liczby bez wartości dziesiętnej na `long`
* Liczby z liczbą dziesiętną do `double`
* Daty do `DateTime`
* Ciągi do `string`
* Wszystko inne do `JsonElement`

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/ObjectToInferredTypesConverter.cs":::

Następujący kod rejestruje konwerter:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/DeserializeInferredTypesToObject.cs" id="Register":::

Oto przykładowy typ z `object` właściwościami:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithObjectProperties":::

Poniższy przykład JSON do deserializacji zawiera wartości, które zostaną rozszeregowane jako `DateTime` , `long` i `string` :

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot",
}
```

Bez niestandardowego konwertera deserializacja umieszcza `JsonElement` w każdej właściwości.

[Folder testów jednostkowych](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/) w `System.Text.Json.Serialization` przestrzeni nazw zawiera więcej przykładów niestandardowych konwerterów, które obsługują deserializacja `object` właściwości.

::: zone pivot="dotnet-core-3-1"

### <a name="support-dictionary-with-non-string-key"></a>Obsługa słownika z kluczem niebędącym ciągiem

Wbudowana obsługa kolekcji słowników jest dla programu `Dictionary<string, TValue>` . Oznacza to, że klucz musi być ciągiem. Aby zapewnić obsługę słownika z liczbą całkowitą lub innym typem jako klucz, wymagany jest konwerter niestandardowy.

Poniższy kod przedstawia niestandardowy konwerter, który współpracuje z `Dictionary<Enum,TValue>` :

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/DictionaryTKeyEnumTValueConverter.cs":::

Następujący kod rejestruje konwerter:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripDictionaryTkeyEnumTValue.cs" id="Register":::

Konwerter może serializować i deserializować `TemperatureRanges` Właściwości następującej klasy, która używa następujących elementów `Enum` :

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithEnumDictionary":::

Dane wyjściowe JSON z serializacji wyglądają podobnie jak w poniższym przykładzie:

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot",
  "TemperatureRanges": {
    "Cold": 20,
    "Hot": 40
  }
}
```

[Folder testów jednostkowych](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/) w `System.Text.Json.Serialization` przestrzeni nazw zawiera więcej przykładów niestandardowych konwerterów, które obsługują słowniki niebędące ciągami.
::: zone-end

### <a name="support-polymorphic-deserialization"></a>Obsługa deserializacji polimorficzna

Wbudowane funkcje zapewniają ograniczony zakres [serializacji polimorficznej](system-text-json-polymorphism.md) , ale nie obsługują deserializacji. Deserializacja wymaga konwertera niestandardowego.

Załóżmy na przykład, że masz `Person` abstrakcyjną klasę bazową z `Employee` i `Customer` klasami pochodnymi. Deserializacja polimorficzna oznacza, że w czasie projektowania można określić `Person` jako element docelowy deserializacji, `Customer` a `Employee` obiekty w formacie JSON są poprawnie deserializowane w czasie wykonywania. Podczas deserializacji należy znaleźć wskazówki, które identyfikują wymagany typ w kodzie JSON. Rodzaje dostępnych wskazówek różnią się w zależności od scenariusza. Na przykład może być dostępna właściwość rozróżniacza lub może zależeć od obecności lub braku określonej właściwości. Bieżąca wersja programu `System.Text.Json` nie udostępnia atrybutów, aby określić sposób obsługi scenariuszy deserializacji polimorficznych, dlatego wymagane są niestandardowe konwertery.

Poniższy kod przedstawia klasę bazową, dwie klasy pochodne i niestandardowy konwerter dla nich. Konwerter używa właściwości rozróżniacza do wykonywania deserializacji polimorficznej. Rozróżniacz typu nie znajduje się w definicjach klas, ale jest tworzony podczas serializacji i jest odczytywany podczas deserializacji.

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/Person.cs" id="Person":::

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/PersonConverterWithTypeDiscriminator.cs":::

Następujący kod rejestruje konwerter:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripPolymorphic.cs" id="Register":::

Konwerter może deserializować kod JSON, który został utworzony przy użyciu tego samego konwertera do serializacji, na przykład:

```json
[
  {
    "TypeDiscriminator": 1,
    "CreditLimit": 10000,
    "Name": "John"
  },
  {
    "TypeDiscriminator": 2,
    "OfficeNumber": "555-1234",
    "Name": "Nancy"
  }
]
```

Kod konwertera w poprzednim przykładzie odczytuje i zapisuje każdą właściwość ręcznie. Alternatywą jest wywołanie `Deserialize` lub `Serialize` wykonanie niektórych zadań. Aby zapoznać się z przykładem, zobacz [ten StackOverflow post](https://stackoverflow.com/a/59744873/12509023).

### <a name="support-round-trip-for-stackt"></a>Obsługa rundy dla stosu\<T>

W przypadku deserializacji ciągu JSON do <xref:System.Collections.Generic.Stack%601> obiektu, a następnie serializacji tego obiektu, zawartość stosu jest w odwrotnej kolejności. To zachowanie dotyczy następujących typów i interfejsów oraz typów zdefiniowanych przez użytkownika, które pochodzą z nich:

* <xref:System.Collections.Stack>
* <xref:System.Collections.Generic.Stack%601>
* <xref:System.Collections.Concurrent.ConcurrentStack%601>
* <xref:System.Collections.Immutable.ImmutableStack%601>
* <xref:System.Collections.Immutable.IImmutableStack%601>

Aby zapewnić obsługę serializacji i deserializacji, która zachowuje oryginalną kolejność w stosie, wymagany jest konwerter niestandardowy.

Poniższy kod przedstawia niestandardowy konwerter, który umożliwia wykonywanie rundy i z `Stack<T>` obiektów:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/JsonConverterFactoryForStackOfT.cs":::

Następujący kod rejestruje konwerter:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripStackOfT.cs" id="Register":::

## <a name="handle-null-values"></a>Obsługa wartości null

Domyślnie serializator obsługuje wartości null w następujący sposób:

* Dla typów i typów referencyjnych <xref:System.Nullable%601> :

  * Nie przekazuje `null` do konwerterów niestandardowych podczas serializacji.
  * Nie przekazuje `JsonTokenType.Null` do konwerterów niestandardowych podczas deserializacji.
  * Zwraca `null` wystąpienie podczas deserializacji.
  * Zapisuje `null` bezpośrednio przy użyciu składnika zapisywania przy serializacji.

* Dla typów wartości niedopuszczających wartości null:

  * Przechodzi `JsonTokenType.Null` do konwerterów niestandardowych podczas deserializacji. (Jeśli konwerter niestandardowy nie jest dostępny, `JsonException` wyjątek jest zgłaszany przez wewnętrzny konwerter typu).

To zachowanie obsługi wartości null polega głównie na optymalizowaniu wydajności przez pominięcie dodatkowego wywołania do konwertera. Ponadto pozwala to uniknąć wymuszania konwerterów dla typów dopuszczających wartość null do sprawdzenia na `null` początku każdego `Read` i `Write` przesłonięcia metody.

::: zone pivot="dotnet-5-0"
Aby włączyć obsługę niestandardowego konwertera `null` dla typu odwołania lub wartości, Przesłoń <xref:System.Text.Json.Serialization.JsonConverter%601.HandleNull%2A?displayProperty=nameWithType> to Return `true` , jak pokazano w następującym przykładzie:

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/CustomConverterHandleNull.cs" highlight="19":::
::: zone-end

## <a name="other-custom-converter-samples"></a>Inne przykłady konwerterów niestandardowych

[Migracja z Newtonsoft.Json do System.Text.Json ](system-text-json-migrate-from-newtonsoft-how-to.md) artykułu zawiera dodatkowe przykłady konwerterów niestandardowych.

[Folder testów jednostkowych](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/) w `System.Text.Json.Serialization` kodzie źródłowym zawiera inne przykłady niestandardowego konwertera, takie jak:

* [Konwerter Int32, który konwertuje wartość null na wartość 0 podczas deserializacji](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/CustomConverterTests.NullValueType.cs)
* [Konwerter Int32, który zezwala na wartości typu String i Number przy deserializacji](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/CustomConverterTests.Int32.cs)
* [Konwerter wyliczenia](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/CustomConverterTests.Enum.cs)
* [\<T>Konwerter listy akceptujący dane zewnętrzne](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/CustomConverterTests.List.cs)
* [Długi konwerter [], który działa z rozdzielaną przecinkami listą liczb](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/CustomConverterTests.Array.cs)

Jeśli musisz utworzyć konwerter, który modyfikuje zachowanie istniejącego wbudowanego konwertera, możesz uzyskać [kod źródłowy istniejącego konwertera](https://github.com/dotnet/runtime/tree/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/src/System/Text/Json/Serialization/Converters) , który będzie używany jako punkt wyjścia do dostosowania.

## <a name="additional-resources"></a>Zasoby dodatkowe

* [Kod źródłowy wbudowanych konwerterów](https://github.com/dotnet/runtime/tree/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/src/System/Text/Json/Serialization/Converters)
* [Obsługa DateTime i DateTimeOffset w System.Text.Json](../datetime/system-text-json-support.md)
* [Jak dostosować kodowanie znaków](system-text-json-character-encoding.md)
* [Jak napisać Serializatory niestandardowe i deserializatory](write-custom-serializer-deserializer.md)
* [System.Text.Json Dokumentacja interfejsu API](xref:System.Text.Json)
* [System.Text.JsonOdwołanie do interfejsu API serializacji](xref:System.Text.Json.Serialization)
