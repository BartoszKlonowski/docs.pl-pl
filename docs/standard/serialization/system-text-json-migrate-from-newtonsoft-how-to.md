---
title: Migrowanie z Newtonsoft.Json programu do System.Text.Json platformy .NET
author: tdykstra
ms.author: tdykstra
no-loc:
- System.Text.Json
- Newtonsoft.Json
ms.date: 01/10/2020
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
ms.openlocfilehash: fbd3c8062892f106ec17d0fef86d5ad7f1207d20
ms.sourcegitcommit: 6f58a5f75ceeb936f8ee5b786e9adb81a9a3bee9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/28/2020
ms.locfileid: "87303481"
---
# <a name="how-to-migrate-from-no-locnewtonsoftjson-to-no-locsystemtextjson"></a>Jak przeprowadzić migrację z Newtonsoft.Json do programuSystem.Text.Json

W tym artykule przedstawiono sposób migracji programu [Newtonsoft.Json](https://www.newtonsoft.com/json) do programu <xref:System.Text.Json> .

`System.Text.Json`Przestrzeń nazw zawiera funkcje serializacji do i deserializacji z JavaScript Object Notation (JSON). `System.Text.Json`Biblioteka jest zawarta w współdzielonej platformie [.net Core 3,0](https://aka.ms/netcore3download) . W przypadku innych platform docelowych zainstaluj [System.Text.Json](https://www.nuget.org/packages/System.Text.Json) pakiet NuGet. Pakiet obsługuje:

* .NET Standard 2,0 i nowsze wersje
* .NET Framework 4.7.2 i nowsze wersje
* .NET Core 2,0, 2,1 i 2,2

`System.Text.Json`koncentruje się głównie na wydajności, zabezpieczeniach i zgodności ze standardami. Ma pewne kluczowe różnice w zachowaniu domyślnym i nie ma wpływu na dostępność funkcji w programie `Newtonsoft.Json` . W przypadku niektórych scenariuszy program `System.Text.Json` nie ma wbudowanych funkcji, ale istnieją zalecane obejścia tego problemu. W przypadku innych scenariuszy obejścia są niepraktyczne. Jeśli aplikacja zależy od brakującej funkcji, rozważ [zgłoszenie problemu](https://github.com/dotnet/runtime/issues/new) , aby dowiedzieć się, czy można dodać wsparcie dla danego scenariusza.

<!-- For information about which features might be added in future releases, see the [Roadmap](https://github.com/dotnet/runtime/tree/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/roadmap/README.md). [Restore this when the roadmap is updated.]-->

W większości tego artykułu zawarto informacje dotyczące korzystania z <xref:System.Text.Json.JsonSerializer> interfejsu API, ale również wskazówki dotyczące sposobu korzystania z programu <xref:System.Text.Json.JsonDocument> (który reprezentuje Document Object Model lub dom), <xref:System.Text.Json.Utf8JsonReader> i <xref:System.Text.Json.Utf8JsonWriter> .

## <a name="table-of-differences-between-no-locnewtonsoftjson-and-no-locsystemtextjson"></a>Tabela różnic między Newtonsoft.Json iSystem.Text.Json

W poniższej tabeli wymieniono `Newtonsoft.Json` funkcje i `System.Text.Json` odpowiedniki. Równoważne są następujące kategorie:

* Obsługiwane przez wbudowaną funkcję. Uzyskanie podobnego zachowania z programu `System.Text.Json` może wymagać użycia atrybutu lub opcji globalnej.
* Nieobsługiwane, możliwe jest obejście tego problemu. Obejścia to [niestandardowe konwertery](system-text-json-converters-how-to.md), które mogą nie zapewniać pełnej parzystości z `Newtonsoft.Json` funkcjonalnością. W przypadku niektórych z nich przykładowy kod jest dostarczany jako przykłady. Jeśli korzystasz z tych `Newtonsoft.Json` funkcji, migracja będzie wymagała modyfikacji modeli obiektów .NET lub innych zmian w kodzie.
* Nieobsługiwane, obejście nie jest praktyczne ani możliwe. Jeśli korzystasz z tych `Newtonsoft.Json` funkcji, migracja nie będzie możliwa bez znaczących zmian.

| Funkcja systemu Newtonsoft.Json                               | System.Text.Jsonsamą |
|-------------------------------------------------------|-----------------------------|
| Deserializacja bez uwzględniania wielkości liter domyślnie           | ✔️ [Ustawienia globalne PropertyNameCaseInsensitive](#case-insensitive-deserialization) |
| Notacji CamelCase — nazwy właściwości przypadku                             | ✔️ [Ustawienia globalne PropertyNamingPolicy](system-text-json-how-to.md#use-camel-case-for-all-json-property-names) |
| Znak ucieczki minimalnej                            | ✔️ [znaku ucieczki ścisłej, konfigurowalne](#minimal-character-escaping) |
| `NullValueHandling.Ignore`ustawienie globalne             | ✔️ [IgnoreNullValues — opcja globalna](system-text-json-how-to.md#exclude-all-null-value-properties) |
| Zezwalaj na Komentarze                                        | ✔️ [Ustawienia globalne ReadCommentHandling](#comments) |
| Zezwalaj na końcowe przecinki                                 | ✔️ [Ustawienia globalne AllowTrailingCommas](#trailing-commas) |
| Rejestracja niestandardowego konwertera                         | ✔️ [kolejność pierwszeństwa](#converter-registration-precedence) |
| Domyślnie nie ma głębokości maksymalnej                           | ✔️ [Domyślna maksymalna głębokość 64, konfigurowalne](#maximum-depth) |
| Obsługa szerokiego zakresu typów                    | ⚠️[Niektóre typy wymagają konwerterów niestandardowych](#types-without-built-in-support) |
| Deserializacja ciągów jako liczby                        | ⚠️[Nieobsługiwane, obejście, przykład](#quoted-numbers) |
| Deserializacja `Dictionary` z kluczem niebędącym ciągiem          | ⚠️[Nieobsługiwane, obejście, przykład](#dictionary-with-non-string-key) |
| Serializacja polimorficzna                             | ⚠️[Nieobsługiwane, obejście, przykład](#polymorphic-serialization) |
| Deserializacja polimorficzna                           | ⚠️[Nieobsługiwane, obejście, przykład](#polymorphic-deserialization) |
| Zdeserializować typu wywnioskowanego do `object` właściwości      | ⚠️[Nieobsługiwane, obejście, przykład](#deserialization-of-object-properties) |
| Deserializacja `null` literału JSON do typów wartości niedopuszczających wartości null | ⚠️[Nieobsługiwane, obejście, przykład](#deserialize-null-to-non-nullable-type) |
| Deserializacja do niemodyfikowalnych klas i struktur          | ⚠️[Nieobsługiwane, obejście, przykład](#deserialize-to-immutable-classes-and-structs) |
| Atrybut `[JsonConstructor]`                         | ⚠️[Nieobsługiwane, obejście, przykład](#specify-constructor-to-use) |
| `Required`ustawienie dla `[JsonProperty]` atrybutu        | ⚠️[Nieobsługiwane, obejście, przykład](#required-properties) |
| `NullValueHandling`ustawienie dla `[JsonProperty]` atrybutu | ⚠️[Nieobsługiwane, obejście, przykład](#conditionally-ignore-a-property)  |
| `DefaultValueHandling`ustawienie dla `[JsonProperty]` atrybutu | ⚠️[Nieobsługiwane, obejście, przykład](#conditionally-ignore-a-property)  |
| `DefaultValueHandling`ustawienie globalne                 | ⚠️[Nieobsługiwane, obejście, przykład](#conditionally-ignore-a-property) |
| `DefaultContractResolver`Aby wykluczyć właściwości       | ⚠️[Nieobsługiwane, obejście, przykład](#conditionally-ignore-a-property) |
| `DateTimeZoneHandling`, `DateFormatString` Ustawienia   | ⚠️[Nieobsługiwane, obejście, przykład](#specify-date-format) |
| Wywołania zwrotne                                             | ⚠️[Nieobsługiwane, obejście, przykład](#callbacks) |
| Obsługa pól publicznych i niepublicznych              | ⚠️[Nieobsługiwane, obejście](#public-and-non-public-fields) |
| Obsługa wewnętrznych i prywatnych metod ustawiających właściwości i metod pobierających | ⚠️[Nieobsługiwane, obejście](#internal-and-private-property-setters-and-getters) |
| Metoda `JsonConvert.PopulateObject`                   | ⚠️[Nieobsługiwane, obejście](#populate-existing-objects) |
| `ObjectCreationHandling`ustawienie globalne               | ⚠️[Nieobsługiwane, obejście](#reuse-rather-than-replace-properties) |
| Dodaj do kolekcji bez metod ustawiających                    | ⚠️[Nieobsługiwane, obejście](#add-to-collections-without-setters) |
| `PreserveReferencesHandling`ustawienie globalne           | ❌ [Nieobsługiwane](#preserve-object-references-and-handle-loops) |
| `ReferenceLoopHandling`ustawienie globalne                | ❌ [Nieobsługiwane](#preserve-object-references-and-handle-loops) |
| Obsługa `System.Runtime.Serialization` atrybutów | ❌ [Nieobsługiwane](#systemruntimeserialization-attributes) |
| `MissingMemberHandling`ustawienie globalne                | ❌ [Nieobsługiwane](#missingmemberhandling) |
| Zezwalaj na nazwy właściwości bez cudzysłowów                   | ❌ [Nieobsługiwane](#json-strings-property-names-and-string-values) |
| Zezwalaj na pojedyncze cudzysłowy wokół wartości ciągu              | ❌ [Nieobsługiwane](#json-strings-property-names-and-string-values) |
| Zezwalaj na wartości niebędące ciągami JSON dla właściwości ciągu    | ❌ [Nieobsługiwane](#non-string-values-for-string-properties) |

Nie jest to pełna lista `Newtonsoft.Json` funkcji. Lista zawiera wiele scenariuszy, które zostały zażądane w przypadku problemów z usługą [GitHub](https://github.com/dotnet/runtime/issues?q=is%3Aopen+is%3Aissue+label%3Aarea-System.Text.Json) lub wpisów [StackOverflow](https://stackoverflow.com/questions/tagged/system.text.json) . Jeśli zaimplementowano obejście dla jednego z wymienionych poniżej scenariuszy, które nie ma obecnie przykładowego kodu, a jeśli chcesz udostępnić swoje rozwiązanie, wybierz **Tę stronę** w sekcji **opinia** w dolnej części tej strony. Spowoduje to utworzenie problemu w repozytorium GitHub tej dokumentacji i wyświetlenie go w sekcji **opinii** na tej stronie.

## <a name="differences-in-default-jsonserializer-behavior-compared-to-no-locnewtonsoftjson"></a>Różnice dotyczące domyślnego zachowania JsonSerializer w porównaniu zNewtonsoft.Json

<xref:System.Text.Json>jest domyślnie rygorystyczne i pozwala uniknąć wszelkich odgadnąć lub interpretacji w imieniu obiektu wywołującego, podkreślając deterministyczne zachowanie. Biblioteka jest celowo zaprojektowana w taki sposób, aby uzyskać wydajność i bezpieczeństwo. `Newtonsoft.Json`jest elastycznie domyślnie. Ta podstawowa różnica w projekcie jest zbyt wiele z poniższych konkretnych różnic w domyślnym zachowaniu.

### <a name="case-insensitive-deserialization"></a>Deserializacja bez uwzględniania wielkości liter

Podczas deserializacji, program `Newtonsoft.Json` Domyślnie dopasowuje nazwy właściwości bez uwzględniania wielkości liter. Wartość <xref:System.Text.Json> Domyślna uwzględnia wielkość liter, co zapewnia lepszą wydajność, ponieważ wykonuje dokładne dopasowanie. Aby uzyskać informacje o sposobie dopasowywania wielkości liter, zobacz dopasowanie do [wielkości](system-text-json-how-to.md#case-insensitive-property-matching)liter.

Jeśli używasz pośrednio przy `System.Text.Json` użyciu ASP.NET Core, nie musisz nic robić, aby uzyskać zachowanie takie jak `Newtonsoft.Json` . ASP.NET Core określa ustawienia [nazw właściwości notacji CamelCase](system-text-json-how-to.md#use-camel-case-for-all-json-property-names) i bez uwzględniania wielkości liter podczas korzystania z programu `System.Text.Json` .

### <a name="minimal-character-escaping"></a>Znak ucieczki minimalnej

Podczas serializacji, `Newtonsoft.Json` jest relatywnie ograniczając, aby zezwalać na znaki, bez ucieczki. Oznacza to, że nie zastępuje ich, `\uxxxx` gdzie `xxxx` jest punktem kodu znaku. W takim przypadku robi to przez emitowanie `\` przed znakiem (na przykład `"` zostanie `\"` ). <xref:System.Text.Json>Domyślnie uzupełnia więcej znaków, aby zapewnić ochronę przed ochroną przed wieloma lokacjami (XSS) lub ataki z ujawnianiem informacji, a tym samym przy użyciu sekwencji składającej się z sześciu znaków. `System.Text.Json`Domyślnie wyprowadza wszystkie znaki inne niż ASCII, więc nie trzeba wykonywać żadnych czynności, jeśli używasz `StringEscapeHandling.EscapeNonAscii` programu w programie `Newtonsoft.Json` . `System.Text.Json`Ponadto domyślnie wyprowadza znaki z uwzględnieniem kodu HTML. Aby uzyskać informacje na temat sposobu przesłania domyślnego `System.Text.Json` zachowania, zobacz [Dostosowywanie kodowania znaków](system-text-json-how-to.md#customize-character-encoding).

### <a name="comments"></a>Komentarze

Podczas deserializacji program `Newtonsoft.Json` Domyślnie ignoruje komentarze w formacie JSON. <xref:System.Text.Json>Wartością domyślną jest zgłaszanie wyjątków dla komentarzy, ponieważ Specyfikacja [RFC 8259](https://tools.ietf.org/html/rfc8259) nie zawiera ich. Aby uzyskać informacje o sposobach zezwalania na komentarze, zobacz [Zezwalanie na komentarze i końcowe przecinki](system-text-json-how-to.md#allow-comments-and-trailing-commas).

### <a name="trailing-commas"></a>Końcowe przecinki

Podczas deserializacji, `Newtonsoft.Json` Domyślnie ignoruje końcowe przecinki. Ignoruje także kilka końcowych przecinków (na przykład `[{"Color":"Red"},{"Color":"Green"},,]` ). <xref:System.Text.Json>Wartością domyślną jest zgłaszanie wyjątków dla końcowych przecinków, ponieważ Specyfikacja [RFC 8259](https://tools.ietf.org/html/rfc8259) nie zezwala. Aby uzyskać informacje na temat sposobu `System.Text.Json` ich akceptowania, zobacz [Zezwalanie na komentarze i końcowe przecinki](system-text-json-how-to.md#allow-comments-and-trailing-commas). Nie ma możliwości zezwalania na wielokrotne końcowe przecinki.

### <a name="converter-registration-precedence"></a>Pierwszeństwo rejestracji konwertera

`Newtonsoft.Json`Priorytet rejestracji dla konwerterów niestandardowych jest następujący:

* Atrybut właściwości
* Atrybut typu
* Kolekcja [konwerterów](https://www.newtonsoft.com/json/help/html/P_Newtonsoft_Json_JsonSerializerSettings_Converters.htm)

Ta kolejność oznacza, że konwerter niestandardowy w `Converters` kolekcji jest zastępowany przez konwerter zarejestrowany przez zastosowanie atrybutu na poziomie typu. Obie te rejestracje są zastępowane przez atrybut na poziomie właściwości.

<xref:System.Text.Json>Pierwszeństwo rejestracji dla konwerterów niestandardowych jest inne:

* Atrybut właściwości
* <xref:System.Text.Json.JsonSerializerOptions.Converters>zbiera
* Atrybut typu

Różnica polega na tym, że konwerter niestandardowy w `Converters` kolekcji przesłania atrybut na poziomie typu. Zamierzone jest zamierzenie, aby zmiany w czasie wykonywania zastępowały opcje czasu projektowania. Nie ma możliwości zmiany pierwszeństwa.

Aby uzyskać więcej informacji na temat rejestrowania niestandardowego konwertera, zobacz [Rejestrowanie niestandardowego konwertera](system-text-json-converters-how-to.md#register-a-custom-converter).

### <a name="maximum-depth"></a>Maksymalna głębokość

`Newtonsoft.Json`Domyślnie nie ma maksymalnego limitu głębokości. Jest <xref:System.Text.Json> to domyślny limit 64 i jest konfigurowalny przez ustawienie <xref:System.Text.Json.JsonSerializerOptions.MaxDepth?displayProperty=nameWithType> .

### <a name="json-strings-property-names-and-string-values"></a>Ciągi JSON (nazwy właściwości i wartości ciągów)

Podczas deserializacji, `Newtonsoft.Json` akceptuje nazwy właściwości ujęte w podwójne cudzysłowy, apostrofy lub bez cudzysłowu. Akceptuje wartości ciągów ujęte w cudzysłów lub pojedyncze cudzysłowy. Na przykład `Newtonsoft.Json` akceptuje następujący kod JSON:

```json
{
  "name1": "value",
  'name2': "value",
  name3: 'value'
}
```

`System.Text.Json`akceptuje tylko nazwy właściwości i wartości ciągu w podwójnych cudzysłowach, ponieważ ten format jest wymagany przez specyfikację [RFC 8259](https://tools.ietf.org/html/rfc8259) i jest jedynym formatem uważanym za prawidłowy kod JSON.

Wartość zawarta w pojedynczym cudzysłowie powoduje, że element [jsonexception](xref:System.Text.Json.JsonException) z następującym komunikatem:

```
''' is an invalid start of a value.
```

### <a name="non-string-values-for-string-properties"></a>Wartości niebędące ciągami dla właściwości ciągu

`Newtonsoft.Json`akceptuje wartości niebędące ciągami, takie jak liczba lub literały `true` oraz `false` , do deserializacji do właściwości typu String. Oto przykład kodu JSON, który `Newtonsoft.Json` został pomyślnie Zserializowany do następującej klasy:

```json
{
  "String1": 1,
  "String2": true,
  "String3": false
}
```

```csharp
public class ExampleClass
{
    public string String1 { get; set; }
    public string String2 { get; set; }
    public string String3 { get; set; }
}
```

`System.Text.Json`nie wykonuje deserializacji wartości niebędących ciągami na właściwości ciągu. Odebrana wartość niebędąca ciągiem dla pola ciągu powoduje wyrażenie [jsonexception](xref:System.Text.Json.JsonException) z następującym komunikatem:

```
The JSON value could not be converted to System.String.
```

## <a name="scenarios-using-jsonserializer-that-require-workarounds"></a>Scenariusze korzystające z JsonSerializer, które wymagają obejścia

Następujące scenariusze nie są obsługiwane przez funkcje wbudowane, ale możliwe jest obejście tego problemu. Obejścia to [niestandardowe konwertery](system-text-json-converters-how-to.md), które mogą nie zapewniać pełnej parzystości z `Newtonsoft.Json` funkcjonalnością. W przypadku niektórych z nich przykładowy kod jest dostarczany jako przykłady. Jeśli korzystasz z tych `Newtonsoft.Json` funkcji, migracja będzie wymagała modyfikacji modeli obiektów .NET lub innych zmian w kodzie.

### <a name="types-without-built-in-support"></a>Typy bez wbudowanej obsługi

<xref:System.Text.Json>nie udostępnia wbudowanego wsparcia dla następujących typów:

* <xref:System.Data.DataTable>i powiązane typy
* Typy języka F #, takie jak [związki](../../fsharp/language-reference/discriminated-unions.md)rozłączne, [typy rekordów](../../fsharp/language-reference/records.md)i [anonimowe typy rekordów](../../fsharp/language-reference/anonymous-records.md).
* <xref:System.Dynamic.ExpandoObject>
* <xref:System.TimeZoneInfo>
* <xref:System.Numerics.BigInteger>
* <xref:System.TimeSpan>
* <xref:System.DBNull>
* <xref:System.Type>
* <xref:System.ValueTuple>i skojarzone typy ogólne

Konwertery niestandardowe można zaimplementować dla typów, które nie mają wbudowanej obsługi.

### <a name="quoted-numbers"></a>Liczby ujęte w cudzysłów

`Newtonsoft.Json`może serializować lub deserializować liczby reprezentowane przez ciągi JSON (ujęte w cudzysłowy). Na przykład może akceptować: `{"DegreesCelsius":"23"}` zamiast `{"DegreesCelsius":23}` . Aby włączyć to zachowanie w programie <xref:System.Text.Json> , zaimplementuj niestandardowy konwerter, jak w poniższym przykładzie. Konwerter obsługuje właściwości zdefiniowane jako `long` :

* Serializować je jako ciągi JSON.
* Akceptuje liczby i cyfry JSON w cudzysłowie podczas deserializacji.

[!code-csharp[](snippets/system-text-json-how-to/csharp/LongToStringConverter.cs)]

Zarejestrowanie tego konwertera niestandardowego przy [użyciu atrybutu](system-text-json-converters-how-to.md#registration-sample---jsonconverter-on-a-property) dla poszczególnych `long` właściwości lub przez [dodanie konwertera](system-text-json-converters-how-to.md#registration-sample---converters-collection) do <xref:System.Text.Json.JsonSerializerOptions.Converters> kolekcji.

### <a name="dictionary-with-non-string-key"></a>Słownik z kluczem niebędącym ciągiem

`Newtonsoft.Json`obsługuje kolekcje typu `Dictionary<TKey, TValue>` . Wbudowana obsługa kolekcji słowników w programie <xref:System.Text.Json> jest ograniczona do `Dictionary<string, TValue>` . Oznacza to, że klucz musi być ciągiem.

Aby zapewnić obsługę słownika z liczbą całkowitą lub innym typem jako klucz, Utwórz konwerter jak przykład w temacie [How to Write Custom Converters](system-text-json-converters-how-to.md#support-dictionary-with-non-string-key).

### <a name="polymorphic-serialization"></a>Serializacja polimorficzna

`Newtonsoft.Json`automatycznie wykonuje serializacji polimorficznej. Aby uzyskać informacje o ograniczonych możliwościach serializacji polimorficznych w programie <xref:System.Text.Json> , zobacz [Serializowanie właściwości klas pochodnych](system-text-json-how-to.md#serialize-properties-of-derived-classes).

Opisane obejście ma na celu zdefiniowanie właściwości, które mogą zawierać klasy pochodne jako typ `object` . Jeśli to nie jest możliwe, inna opcja polega na utworzeniu konwertera z użyciem `Write` metody dla całej hierarchii typów dziedziczenia, takiej jak przykład w temacie [How to Write Custom Converters](system-text-json-converters-how-to.md#support-polymorphic-deserialization).

### <a name="polymorphic-deserialization"></a>Deserializacja polimorficzna

`Newtonsoft.Json`ma `TypeNameHandling` ustawienie, które dodaje metadane nazwy typu do JSON podczas serializacji. Używa metadanych podczas deserializacji w celu wykonania deserializacji polimorficznej. <xref:System.Text.Json>może wykonywać ograniczony zakres [serializacji polimorficznej](system-text-json-how-to.md#serialize-properties-of-derived-classes) , ale nie deserializacji polimorficznej.

Aby obsłużyć deserializacja polimorficzna, Utwórz konwerter, taki jak przykład, w [jaki sposób pisać konwertery niestandardowe](system-text-json-converters-how-to.md#support-polymorphic-deserialization).

### <a name="deserialization-of-object-properties"></a>Deserializacja właściwości obiektu

Podczas `Newtonsoft.Json` deserializacji do <xref:System.Object> ,:

* Wnioskuje typ wartości pierwotnych w ładunku JSON (poza `null` ) i zwraca przechowywane `string` , `long` ,, `double` `boolean` lub `DateTime` jako obiekt opakowany. *Wartości pierwotne* to pojedyncze wartości JSON, takie jak liczba JSON, ciąg,, `true` `false` lub `null` .
* Zwraca `JObject` lub `JArray` dla wartości złożonych w ładunku JSON. *Wartości złożone* to kolekcje par klucz-wartość JSON w nawiasach klamrowych ( `{}` ) lub listy wartości w nawiasach kwadratowych ( `[]` ). Właściwości i wartości w nawiasach klamrowych mogą mieć dodatkowe właściwości lub wartości.
* Zwraca odwołanie o wartości null, gdy ładunek ma `null` literał JSON.

<xref:System.Text.Json>przechowuje w języku opakowany `JsonElement` dla wartości pierwotnych i złożonych przy każdej deserializacji do <xref:System.Object> , na przykład:

* `object`Właściwość.
* `object`Wartość słownika.
* `object`Wartość tablicy.
* Element główny `object` .

Jednakże `System.Text.Json` traktuje `null` to samo, co `Newtonsoft.Json` i zwraca odwołanie null, gdy ładunek zawiera `null` literał JSON.

Aby zaimplementować wnioskowanie o typie dla `object` właściwości, Utwórz konwerter, taki jak przykład, w [jaki sposób pisać konwertery niestandardowe](system-text-json-converters-how-to.md#deserialize-inferred-types-to-object-properties).

### <a name="deserialize-null-to-non-nullable-type"></a>Deserializacja wartości null na typ niedopuszczający wartości null

`Newtonsoft.Json`nie zgłasza wyjątku w następującym scenariuszu:

* `NullValueHandling`jest ustawiona na `Ignore` , i
* Podczas deserializacji kod JSON zawiera wartość null dla typu wartości, który nie dopuszcza wartości null.

W tym samym scenariuszu program <xref:System.Text.Json> generuje wyjątek. (Odpowiednie ustawienie obsługi ma wartość null <xref:System.Text.Json.JsonSerializerOptions.IgnoreNullValues?displayProperty=nameWithType> ).

Jeśli jesteś własnym typem docelowym, najlepszym obejściem jest to, że właściwość w pytaniu nie dopuszcza wartości null (na przykład zmiana `int` na `int?` ).

Innym obejściem jest tworzenie konwertera dla typu, takiego jak Poniższy przykład, który obsługuje wartości null dla `DateTimeOffset` typów:

[!code-csharp[](snippets/system-text-json-how-to/csharp/DateTimeOffsetNullHandlingConverter.cs)]

Zarejestrowanie tego konwertera niestandardowego przy [użyciu atrybutu właściwości](system-text-json-converters-how-to.md#registration-sample---jsonconverter-on-a-property) lub przez [dodanie konwertera](system-text-json-converters-how-to.md#registration-sample---converters-collection) do <xref:System.Text.Json.JsonSerializerOptions.Converters> kolekcji.

**Uwaga:** Poprzedni konwerter **obsługuje wartości null inaczej** niż `Newtonsoft.Json` dla POCOs, które określają wartości domyślne. Załóżmy na przykład, że następujący kod reprezentuje obiekt docelowy:

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWFWithDefault)]

Załóżmy, że następujący kod JSON jest deserializowany przy użyciu poprzedniego konwertera:

```json
{
  "Date": null,
  "TemperatureCelsius": 25,
  "Summary": null
}
```

Po deserializacji `Date` Właściwość ma 1/1/0001 ( `default(DateTimeOffset)` ), czyli wartość ustawioną w konstruktorze jest zastępowana. Mając te same POCO i kod JSON, `Newtonsoft.Json` deserializacja spowodowałaby pozostawienie 1/1/2001 we `Date` właściwości.

### <a name="deserialize-to-immutable-classes-and-structs"></a>Deserializacja do niemodyfikowalnych klas i struktur

`Newtonsoft.Json`może deserializować do niemodyfikowalnych klas i struktur, ponieważ może używać konstruktorów z parametrami. <xref:System.Text.Json>obsługuje tylko publiczne konstruktory bez parametrów. Jako obejście można wywołać konstruktora z parametrami w niestandardowym konwerterze.

Oto niezmienna struktura z wieloma parametrami konstruktora:

[!code-csharp[](snippets/system-text-json-how-to/csharp/ImmutablePoint.cs#ImmutablePoint)]

A oto konwerter, który serializować i deserializacji tej struktury:

[!code-csharp[](snippets/system-text-json-how-to/csharp/ImmutablePointConverter.cs)]

Zarejestruj ten konwerter niestandardowy, [dodając konwerter](system-text-json-converters-how-to.md#registration-sample---converters-collection) do <xref:System.Text.Json.JsonSerializerOptions.Converters> kolekcji.

Aby zapoznać się z przykładem podobnego konwertera, który obsługuje otwarte właściwości ogólne, zobacz [wbudowany konwerter par klucz-wartość](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/src/System/Text/Json/Serialization/Converters/JsonValueConverterKeyValuePair.cs).

### <a name="specify-constructor-to-use"></a>Określ Konstruktor do użycia

Ten `Newtonsoft.Json` `[JsonConstructor]` atrybut umożliwia określenie konstruktora, który ma być wywoływany podczas deserializacji do poco. <xref:System.Text.Json>obsługuje tylko konstruktory bez parametrów. Jako obejście można wywołać każdy Konstruktor, którego potrzebujesz w niestandardowym konwerterze. Zobacz przykład dla [deserializacji do niemodyfikowalnych klas i struktur](#deserialize-to-immutable-classes-and-structs).

### <a name="required-properties"></a>Wymagane właściwości

W programie `Newtonsoft.Json` należy określić, że właściwość jest wymagana przez ustawienie `Required` dla `[JsonProperty]` atrybutu. `Newtonsoft.Json`zgłasza wyjątek, jeśli żadna wartość nie zostanie odebrana w formacie JSON dla właściwości oznaczonej jako wymagane.

<xref:System.Text.Json>nie zgłasza wyjątku, jeśli nie otrzymano żadnej wartości dla jednej z właściwości typu docelowego. Na przykład jeśli masz `WeatherForecast` klasę:

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWF)]

Następujący kod JSON jest deserializowany bez błędu:

```json
{
    "TemperatureCelsius": 25,
    "Summary": "Hot"
}
```

Aby przeprowadzić deserializacja nie powiodła się `Date` , jeśli w kodzie JSON nie ma żadnej właściwości, zaimplementuj konwerter niestandardowy. Następujący przykładowy kod konwertera zgłasza wyjątek, jeśli `Date` Właściwość nie jest ustawiona po zakończeniu deserializacji:

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecastRequiredPropertyConverter.cs)]

Zarejestruj ten konwerter niestandardowy, [dodając konwerter](system-text-json-converters-how-to.md#registration-sample---converters-collection) do <xref:System.Text.Json.JsonSerializerOptions.Converters?displayProperty=nameWithType> kolekcji.

Ten wzorzec cyklicznie wywołujący konwerter wymaga zarejestrowania konwertera przy użyciu, a <xref:System.Text.Json.JsonSerializerOptions> nie przy użyciu atrybutu. W przypadku zarejestrowania konwertera przy użyciu atrybutu, konwerter niestandardowy cyklicznie wywołuje się do samego siebie. Wynik jest pętlą nieskończoną kończącą się na wyjątek przepełnienia stosu.

Podczas rejestrowania konwertera przy użyciu obiektu Options, unikaj pętli nieskończonej przez pominięcie jej w obiekcie Options podczas rekursywnego wywoływania <xref:System.Text.Json.JsonSerializer.Serialize%2A> lub <xref:System.Text.Json.JsonSerializer.Deserialize%2A> . Obiekt Options zawiera <xref:System.Text.Json.JsonSerializerOptions.Converters%2A> kolekcję. Jeśli przekażesz go do `Serialize` lub `Deserialize` , konwerter niestandardowy wywołuje się do siebie, tworząc nieskończoną pętlę, która powoduje wyjątek przepełnienia stosu. Jeśli opcje domyślne nie są możliwe, Utwórz nowe wystąpienie opcji z ustawieniami, które są potrzebne. Takie podejście będzie powolne, ponieważ każde nowe wystąpienie pamięci podręcznej jest niezależne.

Istnieje alternatywny wzorzec, który może używać `JsonConverterAttribute` rejestracji w klasie do przekonwertowania. W tym podejściu kod konwertera wywołuje `Serialize` lub `Deserialize` na klasę, która dziedziczy z klasy, która ma zostać przekształcona. Klasa pochodna nie ma `JsonConverterAttribute` do niej zastosowania. W poniższym przykładzie tej alternatywy:

* `WeatherForecastWithRequiredPropertyConverterAttribute`jest klasą, która ma zostać odszeregowana i ma `JsonConverterAttribute` do niej zastosowanie.
* `WeatherForecastWithoutRequiredPropertyConverterAttribute`jest klasą pochodną, która nie ma atrybutu konwertera.
* Kod w konwerterze wywołuje `Serialize` i `Deserialize` włączony, `WeatherForecastWithoutRequiredPropertyConverterAttribute` Aby uniknąć nieskończonej pętli. To podejście jest kosztem wydajności na potrzeby serializacji z powodu dodatkowego tworzenia wystąpienia obiektu i kopiowania wartości właściwości.

Oto `WeatherForecast*` typy:

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWFWithReqPptyConverterAttr)]

A oto konwerter:

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecastRequiredPropertyConverterForAttributeRegistration.cs)]

Wymagany konwerter właściwości wymaga dodatkowej logiki, jeśli trzeba obsługiwać atrybuty takie jak [[JsonIgnore]](xref:System.Text.Json.Serialization.JsonIgnoreAttribute) lub różne opcje, takie jak kodery niestandardowe. Ponadto przykładowy kod nie obsługuje właściwości, dla których ustawiono wartość domyślną w konstruktorze. To podejście nie różni się między następującymi scenariuszami:

* Brak właściwości w kodzie JSON.
* Właściwość typu niedopuszczający wartości null jest obecna w notacji JSON, ale wartość jest wartością domyślną dla tego typu, np. zero dla `int` .
* Właściwość typu wartości null jest obecna w notacji JSON, ale wartość jest równa null.

### <a name="conditionally-ignore-a-property"></a>Warunkowo Ignoruj Właściwość

`Newtonsoft.Json`ma kilka sposobów, aby warunkowo ignorować właściwość podczas serializacji lub deserializacji:

* `DefaultContractResolver`umożliwia wybranie właściwości, które mają zostać dołączone lub wykluczone na podstawie dowolnego kryterium.
* `NullValueHandling`Ustawienia i `DefaultValueHandling` `JsonSerializerSettings` umożliwiają określenie, że wszystkie właściwości null-wartość lub wartość domyślna wartości powinny być ignorowane.
* `NullValueHandling`Ustawienia i `DefaultValueHandling` w `[JsonProperty]` atrybucie umożliwiają określanie poszczególnych właściwości, które mają być ignorowane, gdy wartość jest równa null lub wartości domyślnej.

<xref:System.Text.Json>oferuje następujące sposoby pomijania właściwości podczas serializacji:

* Atrybut [[JsonIgnore]](system-text-json-how-to.md#exclude-individual-properties) właściwości powoduje pominięcie właściwości z poziomu JSON podczas serializacji.
* Opcja globalna [IgnoreNullValues](system-text-json-how-to.md#exclude-all-null-value-properties) umożliwia wykluczenie wszystkich właściwości o wartości null.
* Opcja globalna [IgnoreReadOnlyProperties](system-text-json-how-to.md#exclude-all-read-only-properties) umożliwia wykluczenie wszystkich właściwości tylko do odczytu.

Te opcje **nie** pozwalają:

* Zignoruj wszystkie właściwości, które mają wartość domyślną dla tego typu.
* Ignoruj wybrane właściwości, które mają wartość domyślną dla tego typu.
* Ignoruj wybrane właściwości, jeśli ich wartość jest równa null.
* Ignoruj wybrane właściwości na podstawie arbitralnych kryteriów ocenionych w czasie wykonywania.

W przypadku tej funkcji można napisać konwerter niestandardowy. Oto przykład POCO i niestandardowy konwerter dla niego, który ilustruje następujące podejście:

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecast.cs?name=SnippetWF)]

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecastRuntimeIgnoreConverter.cs)]

Konwerter powoduje `Summary` pominięcie właściwości z serializacji, jeśli jej wartość jest równa null, pusty ciąg lub "N/A".

Zarejestrowanie tego konwertera niestandardowego przy [użyciu atrybutu klasy](system-text-json-converters-how-to.md#registration-sample---jsonconverter-on-a-type) lub przez [dodanie konwertera](system-text-json-converters-how-to.md#registration-sample---converters-collection) do <xref:System.Text.Json.JsonSerializerOptions.Converters> kolekcji.

Takie podejście wymaga dodatkowej logiki, jeśli:

* POCO zawiera złożone właściwości.
* Musisz obsługiwać atrybuty takie jak `[JsonIgnore]` lub opcje, takie jak kodery niestandardowe.

### <a name="specify-date-format"></a>Określ format daty

`Newtonsoft.Json`Program udostępnia kilka metod kontrolowania, w jaki sposób właściwości `DateTime` i `DateTimeOffset` typy są serializowane i deserializowane:

* `DateTimeZoneHandling`Ustawienie to może służyć do serializacji wszystkich `DateTime` wartości jako daty UTC.
* `DateFormatString`Ustawienia i `DateTime` konwertery mogą służyć do dostosowywania formatu ciągów daty.

W programie <xref:System.Text.Json> jedynym formatem, który ma wbudowaną obsługę, jest ISO 8601-1:2019, ponieważ jest on powszechnie przyjęty, niejednoznaczny i umożliwia precyzyjne przekazanie rundy. Aby użyć innego formatu, Utwórz konwerter niestandardowy. Aby uzyskać więcej informacji, zobacz [Obsługa DateTime i DateTimeOffset System.Text.Json w ](../datetime/system-text-json-support.md).

### <a name="callbacks"></a>Wywołania zwrotne

`Newtonsoft.Json`umożliwia wykonywanie kodu niestandardowego w kilku punktach w procesie serializacji lub deserializacji:

* OnDeserializing (przy rozpoczynaniu deserializacji obiektu)
* Onserializacja (po zakończeniu deserializacji obiektu)
* Onserializacja (gdy zaczynasz serializować obiekt)
* Onserialed (po zakończeniu serializacji obiektu)

W programie <xref:System.Text.Json> można symulować wywołania zwrotne, pisząc konwertery niestandardowe. W poniższym przykładzie przedstawiono niestandardowy konwerter dla POCO. Konwerter zawiera kod, który wyświetla komunikat w każdym punkcie, który odnosi się do `Newtonsoft.Json` wywołania zwrotnego.

[!code-csharp[](snippets/system-text-json-how-to/csharp/WeatherForecastCallbacksConverter.cs)]

Zarejestruj ten konwerter niestandardowy, [dodając konwerter](system-text-json-converters-how-to.md#registration-sample---converters-collection) do <xref:System.Text.Json.JsonSerializerOptions.Converters> kolekcji.

Jeśli używasz niestandardowego konwertera, który następuje po powyższym przykładzie:

* `OnDeserializing`Kod nie ma dostępu do nowego wystąpienia poco. Aby manipulować nowym wystąpieniem POCO na początku deserializacji, Umieść ten kod w konstruktorze POCO.
* Unikaj pętli nieskończonej przez zarejestrowanie konwertera w obiekcie Options i nieprzekazywanie w obiekcie Options podczas cyklicznego wywoływania `Serialize` lub `Deserialize` .

Aby uzyskać więcej informacji na temat konwerterów niestandardowych, które rekursywnie wywołuje `Serialize` lub `Deserialize` , zapoznaj się z sekcją [wymagane właściwości](#required-properties) wcześniej w tym artykule.

### <a name="public-and-non-public-fields"></a>Pola publiczne i niepubliczne

`Newtonsoft.Json`może serializować i deserializować pola oraz właściwości. <xref:System.Text.Json>działa tylko z właściwościami publicznymi. Te funkcje mogą zapewniać konwertery niestandardowe.

### <a name="internal-and-private-property-setters-and-getters"></a>Metody i metody pobierające właściwości wewnętrznych i prywatnych

`Newtonsoft.Json`można używać funkcji i metod ustawiających właściwości prywatne i wewnętrzne przy użyciu `JsonProperty` atrybutu. <xref:System.Text.Json>obsługuje tylko publiczne metody ustawiające. Te funkcje mogą zapewniać konwertery niestandardowe.

### <a name="populate-existing-objects"></a>Wypełnij istniejące obiekty

`JsonConvert.PopulateObject`Metoda w `Newtonsoft.Json` deserializacji dokumentu JSON do istniejącego wystąpienia klasy, zamiast tworzyć nowe wystąpienie. <xref:System.Text.Json>zawsze tworzy nowe wystąpienie typu docelowego przy użyciu domyślnego publicznego konstruktora bez parametrów. Konwertery niestandardowe mogą zdeserializować do istniejącego wystąpienia.

### <a name="reuse-rather-than-replace-properties"></a>Użyj ponownie zamiast właściwości Zamień

`Newtonsoft.Json` `ObjectCreationHandling` Ustawienie pozwala określić, że obiekty w właściwości powinny być ponownie używane, a nie zastąpione podczas deserializacji. <xref:System.Text.Json>zawsze zastępuje obiekty we właściwościach.  Te funkcje mogą zapewniać konwertery niestandardowe.

### <a name="add-to-collections-without-setters"></a>Dodaj do kolekcji bez metod ustawiających

Podczas deserializacji program `Newtonsoft.Json` dodaje obiekty do kolekcji, nawet jeśli właściwość nie ma metody ustawiającej. <xref:System.Text.Json>ignoruje właściwości, które nie mają metod ustawiających. Te funkcje mogą zapewniać konwertery niestandardowe.

## <a name="scenarios-that-jsonserializer-currently-doesnt-support"></a>Scenariusze, które nie są obecnie obsługiwane przez JsonSerializer

W poniższych scenariuszach obejścia nie są praktyczne ani możliwe. Jeśli korzystasz z tych `Newtonsoft.Json` funkcji, migracja nie będzie możliwa bez znaczących zmian.

### <a name="preserve-object-references-and-handle-loops"></a>Zachowaj odwołania do obiektów i pętle obsługi

Domyślnie `Newtonsoft.Json` serializacji według wartości. Na przykład jeśli obiekt zawiera dwie właściwości, które zawierają odwołanie do tego samego `Person` obiektu, wartości `Person` właściwości tego obiektu są duplikowane w kodzie JSON.

`Newtonsoft.Json`ma `PreserveReferencesHandling` ustawienie `JsonSerializerSettings` , które umożliwia serializacji według odwołania:

* Metadane identyfikatora są dodawane do formatu JSON utworzonego dla pierwszego `Person` obiektu.
* KOD JSON, który jest tworzony dla drugiego `Person` obiektu, zawiera odwołanie do tego identyfikatora zamiast wartości właściwości.

`Newtonsoft.Json`Ponadto ma `ReferenceLoopHandling` ustawienie, które pozwala ignorować odwołania cykliczne zamiast zgłaszać wyjątek.

<xref:System.Text.Json>obsługuje tylko Serializacja przez wartość i zgłasza wyjątek dla odwołań cyklicznych.

### <a name="systemruntimeserialization-attributes"></a>Atrybuty System. Runtime. Serialization

<xref:System.Text.Json>nie obsługuje atrybutów z `System.Runtime.Serialization` przestrzeni nazw, takich jak `DataMemberAttribute` i `IgnoreDataMemberAttribute` .

### <a name="octal-numbers"></a>Liczby ósemkowe

`Newtonsoft.Json`traktuje liczby z zerem wiodącym jako liczba ósemkowa. <xref:System.Text.Json>nie zezwala na zera wiodące, ponieważ Specyfikacja [RFC 8259](https://tools.ietf.org/html/rfc8259) nie zezwala.

### <a name="missingmemberhandling"></a>MissingMemberHandling

`Newtonsoft.Json`można skonfigurować do zgłaszania wyjątków podczas deserializacji, jeśli dane JSON zawierają właściwości, których brakuje w typie docelowym. <xref:System.Text.Json>ignoruje dodatkowe właściwości w formacie JSON, z wyjątkiem sytuacji, gdy jest używany [atrybut [JsonExtensionData]](system-text-json-how-to.md#handle-overflow-json). Nie istnieje obejście dla brakującej funkcji członkowskiej.

### <a name="tracewriter"></a>TraceWriter

`Newtonsoft.Json`umożliwia debugowanie przy użyciu programu `TraceWriter` do wyświetlania dzienników generowanych przez serializacji lub deserializacji. <xref:System.Text.Json>nie wykonuje rejestrowania.

## <a name="jsondocument-and-jsonelement-compared-to-jtoken-like-jobject-jarray"></a>JsonDocument i Jsonelement w porównaniu do JToken (np. JObject, JArray)

<xref:System.Text.Json.JsonDocument?displayProperty=fullName>umożliwia analizowanie i kompilowanie Document Object Model tylko do **odczytu** z istniejących ładunków JSON. DOM zapewnia losowy dostęp do danych w ładunku JSON. Do elementów JSON, które tworzą ładunek, można uzyskać dostęp za pośrednictwem <xref:System.Text.Json.JsonElement> typu. `JsonElement`Typ udostępnia interfejsy API do konwersji tekstu JSON na popularne typy .NET. `JsonDocument`uwidacznia <xref:System.Text.Json.JsonDocument.RootElement> Właściwość.

### <a name="jsondocument-is-idisposable"></a>JsonDocument jest interfejs IDisposable

`JsonDocument`tworzy widok danych w pamięci w buforze puli. W związku z tym, w przeciwieństwie do `JObject` lub `JArray` z `Newtonsoft.Json` , `JsonDocument` Typ implementuje `IDisposable` i musi być używany wewnątrz bloku using.

Zwróć tylko `JsonDocument` z interfejsu API, jeśli chcesz przenieść własność okresu istnienia i usunąć odpowiedzialność do obiektu wywołującego. W większości przypadków nie jest to konieczne. Jeśli obiekt wywołujący musi współdziałać z całym dokumentem JSON, zwróć <xref:System.Text.Json.JsonElement.Clone%2A> część <xref:System.Text.Json.JsonDocument.RootElement%2A> , która jest <xref:System.Text.Json.JsonElement> . Jeśli obiekt wywołujący musi pracować z określonym elementem w dokumencie JSON, należy zwrócić wartość tego elementu <xref:System.Text.Json.JsonElement.Clone%2A> <xref:System.Text.Json.JsonElement> . W przypadku powrotu `RootElement` lub podelementu bezpośrednio bez wykonywania operacji `Clone` obiekt wywołujący nie będzie mógł uzyskać dostępu do zwracanej `JsonElement` po usunięciu elementu podrzędnego `JsonDocument` .

Oto przykład, który wymaga `Clone` :

```csharp
public JsonElement LookAndLoad(JsonElement source)
{
    string json = File.ReadAllText(source.GetProperty("fileName").GetString());

    using (JsonDocument doc = JsonDocument.Parse(json))
    {
        return doc.RootElement.Clone();
    }
}
```

Poprzedzający kod oczekuje `JsonElement` , że zawiera `fileName` Właściwość. Plik JSON zostanie otwarty i zostanie utworzony `JsonDocument` . Metoda zakłada, że obiekt wywołujący chce współpracować z całym dokumentem, dlatego zwraca wartość `Clone` `RootElement` .

Jeśli otrzymasz `JsonElement` i zwrócisz podrzędny element, nie trzeba zwracać `Clone` elementu podrzędnego. Obiekt wywołujący jest odpowiedzialny za utrzymanie aktywności, `JsonDocument` do której należy ten element `JsonElement` . Na przykład:

```csharp
public JsonElement ReturnFileName(JsonElement source)
{
   return source.GetProperty("fileName");
}
```

### <a name="jsondocument-is-read-only"></a>JsonDocument jest tylko do odczytu

<xref:System.Text.Json>Dom nie może dodawać, usuwać ani modyfikować elementów JSON. Ta metoda została zaprojektowana w taki sposób, aby zwiększyć wydajność i zmniejszyć alokacje do analizy wspólnych rozmiarów ładunków JSON (czyli < 1 MB). Jeśli w scenariuszu obecnie jest używany modyfikowalny DOM, jedno z następujących obejść może być wykonalne:

* Aby skompilować `JsonDocument` od podstaw (to oznacza, bez przekazywania istniejącego ładunku JSON do `Parse` metody), Napisz tekst JSON przy użyciu `Utf8JsonWriter` i Przeanalizuj dane wyjściowe z tego, aby utworzyć nowy `JsonDocument` .
* Aby zmodyfikować istniejący `JsonDocument` , użyj go do zapisu tekstu JSON, wprowadzania zmian podczas pisania i analizowania danych wyjściowych, aby utworzyć nowe `JsonDocument` .
* Aby scalić istniejące dokumenty JSON, równoważne z `JObject.Merge` `JContainer.Merge` interfejsami API lub z programu `Newtonsoft.Json` , zobacz [ten problem](https://github.com/dotnet/corefx/issues/42466#issuecomment-570475853)w usłudze GitHub.

### <a name="jsonelement-is-a-union-struct"></a>Jsonelement jest strukturą Union

`JsonDocument`uwidacznia `RootElement` jako właściwość typu <xref:System.Text.Json.JsonElement> , który jest Unią, typ struktury, który obejmuje dowolny element JSON. `Newtonsoft.Json`używa dedykowanych typów hierarchicznych, takich jak `JObject` ,, `JArray` `JToken` i tak dalej. `JsonElement`to elementy, które można wyszukiwać i wyliczyć, i można użyć `JsonElement` do zmaterializowania elementów JSON do typów .NET.

### <a name="how-to-search-a-jsondocument-and-jsonelement-for-sub-elements"></a>Jak wyszukiwać element JsonDocument i Jsonelement dla elementów podrzędnych

Wyszukuje tokeny JSON przy użyciu `JObject` lub `JArray` z usługi `Newtonsoft.Json` jest stosunkowo szybka, ponieważ są wyszukiwaniem w słowniku. Dzięki porównaniu wyszukiwanie `JsonElement` wymaga przeszukania sekwencyjnego właściwości i dlatego jest stosunkowo wolne (na przykład przy użyciu `TryGetProperty` ). <xref:System.Text.Json>służy do minimalizowania czasu początkowej analizy zamiast czasu wyszukiwania. W związku z tym należy stosować następujące podejścia do optymalizowania wydajności podczas wyszukiwania za pomocą `JsonDocument` obiektu:

* Użyj wbudowanych modułów wyliczających ( <xref:System.Text.Json.JsonElement.EnumerateArray%2A> i <xref:System.Text.Json.JsonElement.EnumerateObject%2A> ) zamiast wykonywania własnych operacji indeksowania lub pętli.
* Nie wykonuj wyszukiwania sekwencyjnego w całości `JsonDocument` za pośrednictwem każdej właściwości przy użyciu `RootElement` . Zamiast tego należy szukać obiektów zagnieżdżonych JSON w oparciu o znaną strukturę danych JSON. Na przykład jeśli szukasz `Grade` właściwości w `Student` obiektach, pętla przez `Student` obiekty i Pobierz wartość `Grade` dla każdego z nich, zamiast przeszukiwać wszystkie `JsonElement` obiekty szukające `Grade` właściwości. Wykonanie tych czynności spowoduje niepotrzebne przekazanie tych samych danych.

Aby uzyskać przykład kodu, zobacz [Korzystanie z JsonDocument w celu uzyskania dostępu do danych](system-text-json-how-to.md#use-jsondocument-for-access-to-data).

## <a name="utf8jsonreader-compared-to-jsontextreader"></a>Utf8JsonReader w porównaniu do JsonTextReader

<xref:System.Text.Json.Utf8JsonReader?displayProperty=fullName>jest wysoką wydajnością, niskim alokacją, czytnikiem tylko do przodu dla tekstu JSON zakodowanego w formacie UTF-8, Odczytaj z [ReadOnlySpan \<byte> ](xref:System.ReadOnlySpan%601) lub [ReadOnlySequence \<byte> ](xref:System.Buffers.ReadOnlySequence%601). `Utf8JsonReader`Jest typem niskiego poziomu, który może służyć do tworzenia niestandardowych analizatorów i deserializacji.

W poniższych sekcjach opisano zalecane wzorce programowania do użycia `Utf8JsonReader` .

### <a name="utf8jsonreader-is-a-ref-struct"></a>Utf8JsonReader jest strukturą ref

Ponieważ `Utf8JsonReader` Typ jest *strukturą ref*, ma [pewne ograniczenia](../../csharp/language-reference/builtin-types/struct.md#ref-struct). Na przykład nie można go zapisać jako pola w klasie lub strukturze innej niż struktura ref. Aby osiągnąć wysoką wydajność, ten typ musi być, `ref struct` ponieważ musi buforować dane wejściowe [ \<byte> ReadOnlySpan](xref:System.ReadOnlySpan%601), który sam jest strukturą ref. Ponadto ten typ jest modyfikowalny, ponieważ zawiera stan. W związku z tym **Przekaż go przez odwołanie** , a nie przez wartość. Przekazanie go przez wartość spowoduje skopiowanie struktury i zmiana stanu nie będzie widoczna dla obiektu wywołującego. Różni się to od `Newtonsoft.Json` od momentu, gdy `Newtonsoft.Json` `JsonTextReader` jest klasą. Aby uzyskać więcej informacji o sposobach korzystania z struktur ref, zobacz [Zapisywanie bezpiecznego i wydajnego kodu w języku C#](../../csharp/write-safe-efficient-code.md).

### <a name="read-utf-8-text"></a>Odczytaj tekst UTF-8

Aby osiągnąć najlepszą możliwą wydajność przy użyciu `Utf8JsonReader` , Odczytaj ładunki JSON już zakodowane jako tekst UTF-8, a nie jako ciągi UTF-16. Aby zapoznać się z przykładem kodu, zobacz [filtrowanie danych za pomocą Utf8JsonReader](system-text-json-how-to.md#filter-data-using-utf8jsonreader).

### <a name="read-with-a-stream-or-pipereader"></a>Odczytaj przy użyciu strumienia lub PipeReader

`Utf8JsonReader`Obsługuje odczytywanie z zakodowanego w UTF- [8 \<byte> ReadOnlySpan](xref:System.ReadOnlySpan%601) lub [ \<byte> ReadOnlySequence](xref:System.Buffers.ReadOnlySequence%601) (który jest wynikiem odczytu z <xref:System.IO.Pipelines.PipeReader> ).

W przypadku odczytu synchronicznego można odczytać ładunek JSON do końca strumienia w tablicy bajtów i przekazać go do czytnika. Do odczytywania z ciągu (który jest zakodowany jako UTF-16), wywołaj <xref:System.Text.Encoding.UTF8> .<xref:System.Text.Encoding.GetBytes%2A> Aby najpierw transkodowanie ciąg do tablicy bajtów zakodowanych w formacie UTF-8. Następnie Przekaż go do `Utf8JsonReader` .

Ponieważ `Utf8JsonReader` traktuje dane wejściowe jako tekst JSON, znacznik kolejności bajtów UTF-8 jest uznawany za nieprawidłowy kod JSON. Obiekt wywołujący musi odfiltrować to wyjście przed przekazaniem danych do czytnika.

Aby zapoznać się z przykładami kodu, zobacz [use Utf8JsonReader](system-text-json-how-to.md#use-utf8jsonreader).

### <a name="read-with-multi-segment-readonlysequence"></a>Odczytaj z ReadOnlySequence wiele segmentów

Jeśli dane wejściowe JSON to [ReadOnlySpan \<byte> ](xref:System.ReadOnlySpan%601), do każdego elementu JSON można uzyskać dostęp z `ValueSpan` właściwości w czytniku podczas przechodzenia przez pętlę odczytu. Jeśli jednak dane wejściowe to [ReadOnlySequence \<byte> ](xref:System.Buffers.ReadOnlySequence%601) (który jest wynikiem odczytu z <xref:System.IO.Pipelines.PipeReader> ), niektóre elementy JSON mogą obsłużyć wiele segmentów `ReadOnlySequence<byte>` obiektu. Te elementy nie są dostępne z <xref:System.Text.Json.Utf8JsonReader.ValueSpan%2A> w ciągłym bloku pamięci. Zamiast tego, jeśli masz wiele segmentów `ReadOnlySequence<byte>` jako dane wejściowe, sondowanie <xref:System.Text.Json.Utf8JsonReader.HasValueSequence%2A> właściwości w czytniku, aby ustalić, jak uzyskać dostęp do bieżącego elementu JSON. Oto zalecany wzorzec:

```csharp
while (reader.Read())
{
    switch (reader.TokenType)
    {
        // ...
        ReadOnlySpan<byte> jsonElement = reader.HasValueSequence ?
            reader.ValueSequence.ToArray() :
            reader.ValueSpan;
        // ...
    }
}
```

### <a name="use-valuetextequals-for-property-name-lookups"></a>Użyj ValueTextEquals do wyszukiwania nazw właściwości

Nie używaj <xref:System.Text.Json.Utf8JsonReader.ValueSpan%2A> do porównywania typu Byte-bajtowe, wywołując <xref:System.MemoryExtensions.SequenceEqual%2A> dla wyszukiwania nazw właściwości. <xref:System.Text.Json.Utf8JsonReader.ValueTextEquals%2A>Zamiast tego wywołać metodę, ponieważ ta metoda nie oznacza żadnych znaków, które są wyprowadzane w formacie JSON. Oto przykład, który pokazuje, jak wyszukiwać właściwość o nazwie "name":

[!code-csharp[](snippets/system-text-json-how-to/csharp/ValueTextEqualsExample.cs?name=SnippetDefineUtf8Var)]

[!code-csharp[](snippets/system-text-json-how-to/csharp/ValueTextEqualsExample.cs?name=SnippetUseUtf8Var&highlight=11)]

### <a name="read-null-values-into-nullable-value-types"></a>Odczytywanie wartości null w typach wartości null

`Newtonsoft.Json`udostępnia interfejsy API, które zwracają <xref:System.Nullable%601> , takie jak `ReadAsBoolean` , które obsługują `Null` `TokenType` przez użytkownika przez zwrócenie `bool?` . Wbudowane `System.Text.Json` interfejsy API zwracają tylko typy wartości niedopuszczające wartości null. Na przykład <xref:System.Text.Json.Utf8JsonReader.GetBoolean%2A?displayProperty=nameWithType> zwraca `bool` . Zgłasza wyjątek, jeśli znajduje się `Null` w formacie JSON. W poniższych przykładach pokazano dwa sposoby obsługi wartości null, jeden przez zwrócenie typu wartości null i jednego przez zwrócenie wartości domyślnej:

```csharp
public bool? ReadAsNullableBoolean()
{
    _reader.Read();
    if (_reader.TokenType == JsonTokenType.Null)
    {
        return null;
    }
    if (_reader.TokenType != JsonTokenType.True && _reader.TokenType != JsonTokenType.False)
    {
        throw new JsonException();
    }
    return _reader.GetBoolean();
}
```

```csharp
public bool ReadAsBoolean(bool defaultValue)
{
    _reader.Read();
    if (_reader.TokenType == JsonTokenType.Null)
    {
        return defaultValue;
    }
    if (_reader.TokenType != JsonTokenType.True && _reader.TokenType != JsonTokenType.False)
    {
        throw new JsonException();
    }
    return _reader.GetBoolean();
}
```

### <a name="multi-targeting"></a>Wiele elementów docelowych

Jeśli chcesz nadal używać `Newtonsoft.Json` dla określonych platform docelowych, możesz wybrać wiele implementacji i mieć dwie implementacje. Nie jest to jednak proste i wymaga `#ifdefs` duplikowania niektórych i źródłowych. Jednym ze sposobów udostępniania możliwie największej ilości kodu jest utworzenie `ref struct` otoki wokół `Utf8JsonReader` i `Newtonsoft.Json` `JsonTextReader` . Ta otoka umożliwia ujednolicenie obszaru powierzchni publicznej podczas izolowania różnic behawioralnych. Dzięki temu można izolować zmiany w odniesieniu do konstrukcji typu wraz z przekazywaniem nowego typu dookoła przez odwołanie. Jest to wzorzec, [który jest następujący](https://www.nuget.org/packages/Microsoft.Extensions.DependencyModel/3.1.0/) :

* [UnifiedJsonReader.JsonTextReader.cs](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/installer/managed/Microsoft.Extensions.DependencyModel/UnifiedJsonReader.JsonTextReader.cs)
* [UnifiedJsonReader.Utf8JsonReader.cs](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/installer/managed/Microsoft.Extensions.DependencyModel/UnifiedJsonReader.Utf8JsonReader.cs)

## <a name="utf8jsonwriter-compared-to-jsontextwriter"></a>Utf8JsonWriter w porównaniu do JsonTextWriter

<xref:System.Text.Json.Utf8JsonWriter?displayProperty=fullName>jest wysoce wydajnym sposobem pisania zakodowanego tekstu JSON w formacie UTF-8 ze wspólnych typów platformy .NET, takich jak `String` , `Int32` , i `DateTime` . Składnik zapisywania jest typu niskiego poziomu, który może służyć do tworzenia serializatorów niestandardowych.

W poniższych sekcjach opisano zalecane wzorce programowania do użycia `Utf8JsonWriter` .

### <a name="write-with-utf-8-text"></a>Napisz z tekstem UTF-8

Aby osiągnąć najlepszą możliwą wydajność przy użyciu `Utf8JsonWriter` , Zapisz ładunki JSON już zakodowane jako tekst UTF-8, a nie jako ciągi UTF-16. Użyj polecenia, <xref:System.Text.Json.JsonEncodedText> aby buforować i wstępnie kodować znane nazwy właściwości ciągów oraz wartości jako elementy statyczne i przekazać je do składnika zapisywania zamiast używać literałów ciągów w formacie UTF-16. Jest to szybsze niż buforowanie i korzysta z tablic bajtowych UTF-8.

Takie podejście działa również, jeśli trzeba wykonać niestandardowe ucieczki. `System.Text.Json`nie zezwala na wyłączenie ucieczki podczas pisania ciągu. Można jednak przekazać własne niestandardowe <xref:System.Text.Encodings.Web.JavaScriptEncoder> jako opcję do składnika zapisywania lub utworzyć własne, `JsonEncodedText` które używają funkcji `JavascriptEncoder` do wykonywania ucieczki, a następnie napisać `JsonEncodedText` zamiast ciągu. Aby uzyskać więcej informacji, zobacz [Dostosowywanie kodowania znaków](system-text-json-how-to.md#customize-character-encoding).

### <a name="write-raw-values"></a>Zapisz nieprzetworzone wartości

`Newtonsoft.Json` `WriteRawValue` Metoda zapisuje nieprzetworzony kod JSON, w którym oczekiwana jest wartość. <xref:System.Text.Json>nie ma bezpośredniego odpowiednika, ale jest to obejście, które zapewnia zapis tylko prawidłowy kod JSON:

```csharp
using JsonDocument doc = JsonDocument.Parse(string);
doc.WriteTo(writer);
```

### <a name="customize-character-escaping"></a>Dostosowywanie ucieczki znaków

Ustawienie [StringEscapeHandling](https://www.newtonsoft.com/json/help/html/T_Newtonsoft_Json_StringEscapeHandling.htm) `JsonTextWriter` oferuje opcje ucieczki wszystkich znaków spoza zestawu ASCII **lub** znaków HTML. Domyślnie program `Utf8JsonWriter` wyprowadza wszystkie znaki inne niż ASCII **i** html. To anulowanie jest wykonywane w celu zapewnienia bezpieczeństwa ze względu na ochronę. Aby określić inne zasady ucieczki, Utwórz <xref:System.Text.Encodings.Web.JavaScriptEncoder> zestaw i <xref:System.Text.Json.JsonWriterOptions.Encoder?displayProperty=nameWithType> . Aby uzyskać więcej informacji, zobacz [Dostosowywanie kodowania znaków](system-text-json-how-to.md#customize-character-encoding).

### <a name="customize-json-format"></a>Dostosuj format JSON

`JsonTextWriter`Program zawiera następujące ustawienia, dla których `Utf8JsonWriter` nie ma odpowiednika:

* [Wcięcia](https://www.newtonsoft.com/json/help/html/P_Newtonsoft_Json_JsonTextWriter_Indentation.htm) — określa liczbę znaków do wcięcia. `Utf8JsonWriter`zawsze wykonuje wcięcie z 2 znakami.
* [IndentChar](https://www.newtonsoft.com/json/help/html/P_Newtonsoft_Json_JsonTextWriter_IndentChar.htm) — określa znak do użycia w przypadku wcięcia.  `Utf8JsonWriter`zawsze używa odstępu.
* [QuoteChar](https://www.newtonsoft.com/json/help/html/P_Newtonsoft_Json_JsonTextWriter_QuoteChar.htm) — określa znak, który ma być używany do otaczania wartości ciągu.  `Utf8JsonWriter`zawsze używa podwójnych cudzysłowów.
* [Quote](https://www.newtonsoft.com/json/help/html/P_Newtonsoft_Json_JsonTextWriter_QuoteName.htm) -określa, czy należy ująć nazwy właściwości z cudzysłowami.  `Utf8JsonWriter`zawsze otacza je cudzysłowami.

Nie istnieją obejścia, które pozwolą dostosować kod JSON utworzony przez program `Utf8JsonWriter` w taki sposób.

### <a name="write-null-values"></a>Zapisz wartości null

Aby zapisać wartości null przy użyciu `Utf8JsonWriter` , wywołaj:

* <xref:System.Text.Json.Utf8JsonWriter.WriteNull%2A>Aby zapisać parę klucz-wartość z wartością null jako wartość.
* <xref:System.Text.Json.Utf8JsonWriter.WriteNullValue%2A>Aby zapisać wartość null jako element tablicy JSON.

Dla właściwości String, jeśli ciąg ma wartość null <xref:System.Text.Json.Utf8JsonWriter.WriteString%2A> i <xref:System.Text.Json.Utf8JsonWriter.WriteStringValue%2A> jest odpowiednikiem `WriteNull` i `WriteNullValue` .

### <a name="write-timespan-uri-or-char-values"></a>Zapis wartości TimeSpan, URI lub char

`JsonTextWriter`dostarcza `WriteValue` metody dla wartości [TimeSpan](https://www.newtonsoft.com/json/help/html/M_Newtonsoft_Json_JsonTextWriter_WriteValue_18.htm), [URI](https://www.newtonsoft.com/json/help/html/M_Newtonsoft_Json_JsonTextWriter_WriteValue_22.htm)i [char](https://www.newtonsoft.com/json/help/html/M_Newtonsoft_Json_JsonTextWriter_WriteValue_3.htm) . `Utf8JsonWriter`nie ma równoważnych metod. Zamiast tego sformatuj te wartości jako ciągi (poprzez wywoływanie `ToString()` , na przykład) i wywołanie <xref:System.Text.Json.Utf8JsonWriter.WriteStringValue%2A> .

### <a name="multi-targeting"></a>Wiele elementów docelowych

Jeśli chcesz nadal używać `Newtonsoft.Json` dla określonych platform docelowych, możesz wybrać wiele implementacji i mieć dwie implementacje. Nie jest to jednak proste i wymaga `#ifdefs` duplikowania niektórych i źródłowych. Jednym ze sposobów udostępniania możliwie największej ilości kodu jest utworzenie otoki wokół `Utf8JsonWriter` i `Newtonsoft` `JsonTextWriter` . Ta otoka umożliwia ujednolicenie obszaru powierzchni publicznej podczas izolowania różnic behawioralnych. Dzięki temu można izolować zmiany głównie do konstrukcji typu. Biblioteka [Microsoft. Extensions. DependencyModel](https://www.nuget.org/packages/Microsoft.Extensions.DependencyModel/3.1.0/) :

* [UnifiedJsonWriter.JsonTextWriter.cs](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/installer/managed/Microsoft.Extensions.DependencyModel/UnifiedJsonWriter.JsonTextWriter.cs)
* [UnifiedJsonWriter.Utf8JsonWriter.cs](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/installer/managed/Microsoft.Extensions.DependencyModel/UnifiedJsonWriter.Utf8JsonWriter.cs)

## <a name="additional-resources"></a>Zasoby dodatkowe

<!-- * [System.Text.Json roadmap](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/roadmap/README.md)[Restore this when the roadmap is updated.]-->
* [System.Text.JsonPodsumowanie](system-text-json-overview.md)
* [Jak używaćSystem.Text.Json](system-text-json-how-to.md)
* [Jak pisać konwertery niestandardowe](system-text-json-converters-how-to.md)
* [Obsługa DateTime i DateTimeOffset wSystem.Text.Json](../datetime/system-text-json-support.md)
* [System.Text.JsonDokumentacja interfejsu API](xref:System.Text.Json)
* [System.Text.Json. Dokumentacja interfejsu API serializacji](xref:System.Text.Json.Serialization)
