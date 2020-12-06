---
title: 'Samouczek: Tworzenie dostawcy typów'
description: 'Dowiedz się, jak utworzyć własnych dostawców typów języka F # w języku F # 3,0, badając kilku dostawców typów prostych, aby zilustrować podstawowe pojęcia.'
ms.date: 11/04/2019
ms.openlocfilehash: 65cb9616f66b5850135dbfcdd9b9a9dad30421de
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96739701"
---
# <a name="tutorial-create-a-type-provider"></a>Samouczek: Tworzenie dostawcy typów

Mechanizm dostawcy typów w języku F # jest znaczną częścią pomocy technicznej dotyczącej rozbudowanego programowania informacji. W tym samouczku wyjaśniono, jak utworzyć własnych dostawców typów, przechodząc przez rozwój kilku dostawców typów prostych, aby zilustrować podstawowe pojęcia. Aby uzyskać więcej informacji na temat mechanizmu dostawcy typów w języku F #, zobacz [dostawcy typów](index.md).

Ekosystem F # zawiera szereg dostawców typów dla często używanych usług Internet i Enterprise Data Services. Na przykład:

- [FSharp. Data](https://fsharp.github.io/FSharp.Data/) zawiera dostawców typów dla formatów dokumentów JSON, XML, CSV i HTML.

- Element [sqldostarczając](https://fsprojects.github.io/SQLProvider/) ma silnie określony dostęp do baz danych SQL za pomocą mapowania obiektów i zapytań języka F # LINQ względem tych źródeł danych.

- [FSharp. Data. SqlClient](https://fsprojects.github.io/FSharp.Data.SqlClient/) ma zestaw dostawców typów dla zaznaczonego osadzania języka T-SQL w języku F #.

- [FSharp. Data. TypeProviders](https://fsprojects.github.io/FSharp.Data.TypeProviders/) to starszy zestaw dostawców typów do użytku tylko z .NET Framework programowaniem do uzyskiwania dostępu do usług SQL, Entity Framework, OData i WSDL.

W razie potrzeby można utworzyć niestandardowych dostawców typów lub odwoływać się do dostawców typów utworzonych przez innych użytkowników. Na przykład organizacja może mieć usługę danych, która zapewnia dużą i rosnącą liczbę nazwanych zestawów danych, z których każdy ma własny stabilny schemat danych. Można utworzyć dostawcę typów, który odczytuje schematy i prezentuje bieżące zestawy danych programisty w jednoznacznie określonym sposób.

## <a name="before-you-start"></a>Przed rozpoczęciem

Mechanizm dostawcy typów jest przeznaczony głównie do wstrzykiwania stabilnych przestrzeni danych i informacji o usługach do środowiska programowania F #.

Ten mechanizm nie jest przeznaczony do wprowadzania miejsc informacji, których schemat zmienia się podczas wykonywania programu w sposób istotny dla logiki programu. Mechanizm nie jest również przeznaczony do programowania meta-językowego, nawet jeśli ta domena zawiera nieprawidłowe zastosowania. Tego mechanizmu należy używać tylko tam, gdzie jest to konieczne, a rozwój dostawcy typów daje bardzo wysoką wartość.

Należy unikać pisania dostawcy typów, w którym schemat nie jest dostępny. Podobnie należy unikać pisania dostawcy typów, w którym wystarcza zwykła (lub nawet istniejąca) Biblioteka platformy .NET.

Przed rozpoczęciem należy zadać następujące pytania:

- Czy masz schemat dla źródła informacji? Jeśli tak, to jakie jest mapowanie do systemu typu F # i .NET?

- Czy można użyć istniejącego (dynamicznie wpisanego) interfejsu API jako punktu wyjścia dla implementacji?

- Czy ty i Twoja organizacja będzie miała wystarczające użycie dostawcy typów, aby napisać jego wartościowa? Czy normalna Biblioteka platformy .NET spełnia Twoje potrzeby?

- Jak dużo będzie zmieniać schemat?

- Czy ulegnie zmianie podczas kodowania?

- Czy zmieni się między sesjami kodowania?

- Zmieni się podczas wykonywania programu?

Dostawcy typów najlepiej nadają się do sytuacji, w których schemat jest stabilny w czasie wykonywania i w okresie istnienia skompilowanego kodu.

## <a name="a-simple-type-provider"></a>Dostawca typu prostego

Ten przykład to Sample. HelloWorldTypeProvider, podobny do przykładów w `examples` katalogu [zestawu SDK dostawcy typów języka F #](https://github.com/fsprojects/FSharp.TypeProviders.SDK/). Dostawca udostępnia "przestrzeń typu" zawierającą 100 typów wymazanych, jak pokazano w poniższym kodzie za pomocą składni podpisów języka F # i pomijając szczegóły dla wszystkich z wyjątkiem `Type1` . Aby uzyskać więcej informacji na temat wymazanych typów, zobacz [szczegóły dotyczące wymazanych typów](#details-about-erased-provided-types) w dalszej części tego tematu.

```fsharp
namespace Samples.HelloWorldTypeProvider

type Type1 =
    /// This is a static property.
    static member StaticProperty : string

    /// This constructor takes no arguments.
    new : unit -> Type1

    /// This constructor takes one argument.
    new : data:string -> Type1

    /// This is an instance property.
    member InstanceProperty : int

    /// This is an instance method.
    member InstanceMethod : x:int -> char

    nested type NestedType =
        /// This is StaticProperty1 on NestedType.
        static member StaticProperty1 : string
        …
        /// This is StaticProperty100 on NestedType.
        static member StaticProperty100 : string

type Type2 =
…
…

type Type100 =
…
```

Należy zauważyć, że zestaw typów i elementów członkowskich jest znany statycznie. Ten przykład nie wykorzystuje możliwości dostawców do udostępniania typów, które są zależne od schematu. Implementacja dostawcy typów została omówiona w poniższym kodzie, a szczegóły znajdują się w dalszej części tego tematu.

> [!WARNING]
> Mogą występować różnice między tym kodem i przykładami online.

```fsharp
namespace Samples.FSharp.HelloWorldTypeProvider

open System
open System.Reflection
open ProviderImplementation.ProvidedTypes
open FSharp.Core.CompilerServices
open FSharp.Quotations

// This type defines the type provider. When compiled to a DLL, it can be added
// as a reference to an F# command-line compilation, script, or project.
[<TypeProvider>]
type SampleTypeProvider(config: TypeProviderConfig) as this =

  // Inheriting from this type provides implementations of ITypeProvider
  // in terms of the provided types below.
  inherit TypeProviderForNamespaces(config)

  let namespaceName = "Samples.HelloWorldTypeProvider"
  let thisAssembly = Assembly.GetExecutingAssembly()

  // Make one provided type, called TypeN.
  let makeOneProvidedType (n:int) =
  …
  // Now generate 100 types
  let types = [ for i in 1 .. 100 -> makeOneProvidedType i ]

  // And add them to the namespace
  do this.AddNamespace(namespaceName, types)

[<assembly:TypeProviderAssembly>]
do()
```

Aby użyć tego dostawcy, Otwórz osobne wystąpienie programu Visual Studio, Utwórz skrypt języka F #, a następnie Dodaj odwołanie do dostawcy ze skryptu przy użyciu #r, jak pokazano w poniższym kodzie:

```fsharp
#r @".\bin\Debug\Samples.HelloWorldTypeProvider.dll"

let obj1 = Samples.HelloWorldTypeProvider.Type1("some data")

let obj2 = Samples.HelloWorldTypeProvider.Type1("some other data")

obj1.InstanceProperty
obj2.InstanceProperty

[ for index in 0 .. obj1.InstanceProperty-1 -> obj1.InstanceMethod(index) ]
[ for index in 0 .. obj2.InstanceProperty-1 -> obj2.InstanceMethod(index) ]

let data1 = Samples.HelloWorldTypeProvider.Type1.NestedType.StaticProperty35
```

Następnie poszukaj typów w `Samples.HelloWorldTypeProvider` przestrzeni nazw wygenerowanej przez dostawcę typów.

Przed ponownym skompilowaniem dostawcy upewnij się, że wszystkie wystąpienia programu Visual Studio i F# Interactive korzystają z biblioteki DLL dostawcy. W przeciwnym razie wystąpi błąd kompilacji, ponieważ wyjściowa biblioteka DLL zostanie zablokowana.

Aby debugować tego dostawcę przy użyciu instrukcji Print, należy utworzyć skrypt, który ujawnia problem z dostawcą, a następnie użyć następującego kodu:

```console
fsc.exe -r:bin\Debug\HelloWorldTypeProvider.dll script.fsx
```

Aby debugować tego dostawcę przy użyciu programu Visual Studio, Otwórz wiersz polecenia dla deweloperów dla programu Visual Studio z poświadczeniami administracyjnymi i uruchom następujące polecenie:

```console
devenv.exe /debugexe fsc.exe -r:bin\Debug\HelloWorldTypeProvider.dll script.fsx
```

Alternatywnie Otwórz program Visual Studio, otwórz menu Debuguj, wybierz `Debug/Attach to process…` i Dołącz do innego procesu, w `devenv` którym edytujesz skrypt. Korzystając z tej metody, można łatwiej przekierować konkretną logikę w dostawcy typów przez interakcyjne wpisywanie wyrażeń do drugiego wystąpienia (z pełną technologią IntelliSense i innymi funkcjami).

Można wyłączyć debugowanie Tylko mój kod, aby lepiej identyfikować błędy w wygenerowanym kodzie. Aby uzyskać informacje na temat włączania lub wyłączania tej funkcji, zobacz [nawigowanie po kodzie za pomocą debugera](/visualstudio/debugger/navigating-through-code-with-the-debugger). Ponadto można również ustawić wyjątek pierwszej szansy do przechwycenia, otwierając `Debug` menu, a następnie wybierając `Exceptions` lub naciskając klawisze CTRL + ALT + E, aby otworzyć okno `Exceptions` dialogowe. W tym oknie dialogowym, w obszarze `Common Language Runtime Exceptions` , zaznacz `Thrown` pole wyboru.

### <a name="implementation-of-the-type-provider"></a>Implementacja dostawcy typów

Ta sekcja przeprowadzi Cię przez główne sekcje implementacji dostawcy typów. Najpierw należy zdefiniować typ niestandardowego dostawcy typów:

```fsharp
[<TypeProvider>]
type SampleTypeProvider(config: TypeProviderConfig) as this =
```

Ten typ musi być publiczny i musi być oznaczony atrybutem [TypeProvider](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-compilerservices-typeproviderattribute.html) , aby kompilator rozpoznał dostawcę typów, gdy oddzielny projekt F # odwołuje się do zestawu, który zawiera typ. Parametr *config* jest opcjonalny, a jeśli obecny, zawiera informacje o konfiguracji kontekstowej dla wystąpienia dostawcy typu, które tworzy kompilator F #.

Następnie należy zaimplementować interfejs [ITypeProvider](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-compilerservices-itypeprovider.html) . W takim przypadku należy użyć `TypeProviderForNamespaces` typu z `ProvidedTypes` interfejsu API jako typu podstawowego. Ten typ pomocnika może zapewnić skończoną kolekcję eagerly udostępnionych przestrzenie nazw, z których każdy zawiera bezpośrednio określoną liczbę stałych eagerly typów. W tym kontekście dostawca *eagerly* generuje typy, nawet jeśli nie są potrzebne lub używane.

```fsharp
inherit TypeProviderForNamespaces(config)
```

Następnie zdefiniuj lokalne wartości prywatne, które określają przestrzeń nazw dla podanych typów i Znajdź sam zestaw dostawcy typów. Ten zestaw jest używany później jako logiczny typ nadrzędny dla podanych wymazanych typów.

```fsharp
let namespaceName = "Samples.HelloWorldTypeProvider"
let thisAssembly = Assembly.GetExecutingAssembly()
```

Następnie Utwórz funkcję, aby zapewnić każdy z typów Type1... Type100. Ta funkcja została omówiona bardziej szczegółowo w dalszej części tego tematu.

```fsharp
let makeOneProvidedType (n:int) = …
```

Następnie Wygeneruj dostarczone typy 100:

```fsharp
let types = [ for i in 1 .. 100 -> makeOneProvidedType i ]
```

Następnie dodaj typy jako podaną przestrzeń nazw:

```fsharp
do this.AddNamespace(namespaceName, types)
```

Na koniec Dodaj atrybut zestawu, który wskazuje, że tworzysz bibliotekę DLL dostawcy typów:

```fsharp
[<assembly:TypeProviderAssembly>]
do()
```

### <a name="providing-one-type-and-its-members"></a>Udostępnianie jednego typu i jego składowych

`makeOneProvidedType`Funkcja wykonuje rzeczywistą służbę dostarczającą jeden z typów.

```fsharp
let makeOneProvidedType (n:int) =
…
```

W tym kroku opisano implementację tej funkcji. Najpierw utwórz dostarczony typ (na przykład Type1, gdy n = 1 lub Type57, gdy n = 57).

```fsharp
// This is the provided type. It is an erased provided type and, in compiled code,
// will appear as type 'obj'.
let t = ProvidedTypeDefinition(thisAssembly, namespaceName,
                               "Type" + string n,
                               baseType = Some typeof<obj>)
```

Należy zwrócić uwagę na następujące kwestie:

- Ten dostarczony typ jest wymazany.  Ponieważ wskazujesz, że typ podstawowy to `obj` , wystąpienia będą wyświetlane jako wartości typu [obj](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-obj.html) w skompilowanym kodzie.

- W przypadku określenia typu niezagnieżdżonego należy określić zestaw i przestrzeń nazw. W przypadku wymazanych typów zestaw powinien być samym zestawem dostawcy typów.

Następnie Dodaj dokumentację XML do typu. Ta dokumentacja jest opóźniona, to jest obliczana na żądanie, jeśli wymaga tego kompilator hosta.

```fsharp
t.AddXmlDocDelayed (fun () -> $"""This provided type {"Type" + string n}""")
```

Następnie Dodaj podaną Właściwość statyczną do typu:

```fsharp
let staticProp = ProvidedProperty(propertyName = "StaticProperty",
                                  propertyType = typeof<string>,
                                  isStatic = true,
                                  getterCode = (fun args -> <@@ "Hello!" @@>))
```

Pobieranie tej właściwości będzie zawsze oceniane jako ciąg "Hello!". `GetterCode`Dla właściwości zostanie użyta oferta F #, która reprezentuje kod generowany przez kompilator hosta w celu pobrania właściwości. Aby uzyskać więcej informacji na temat ofert, zobacz [cytaty kodu (F #)](../../language-reference/code-quotations.md).

Dodaj dokumentację XML do właściwości.

```fsharp
staticProp.AddXmlDocDelayed(fun () -> "This is a static property")
```

Teraz Dołącz dostarczoną właściwość do podanego typu. Należy dołączyć podany element członkowski do jednego i tylko jednego typu. W przeciwnym razie element członkowski nigdy nie będzie dostępny.

```fsharp
t.AddMember staticProp
```

Teraz Utwórz dostarczony Konstruktor, który nie przyjmuje żadnych parametrów.

```fsharp
let ctor = ProvidedConstructor(parameters = [ ],
                               invokeCode = (fun args -> <@@ "The object data" :> obj @@>))
```

`InvokeCode`Dla konstruktora zwraca cytat F #, który reprezentuje kod generowany przez kompilator hosta, gdy Konstruktor jest wywoływany. Na przykład można użyć następującego konstruktora:

```fsharp
new Type10()
```

Wystąpienie dostarczonego typu zostanie utworzone z danymi źródłowymi "dane obiektu". Kod ujęty w cudzysłów zawiera konwersję do [obj](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-obj.html) , ponieważ ten typ jest wymazywanie tego dostarczonego typu (jak określono w przypadku zadeklarowanego typu).

Dodaj dokumentację XML do konstruktora i Dodaj dostarczony Konstruktor do podanego typu:

```fsharp
ctor.AddXmlDocDelayed(fun () -> "This is a constructor")

t.AddMember ctor
```

Utwórz drugiego konstruktora, który przyjmuje jeden parametr:

```fsharp
let ctor2 =
ProvidedConstructor(parameters = [ ProvidedParameter("data",typeof<string>) ],
                    invokeCode = (fun args -> <@@ (%%(args.[0]) : string) :> obj @@>))
```

`InvokeCode`Dla konstruktora ponownie zwraca cytat F #, który reprezentuje kod wygenerowany przez kompilator hosta dla wywołania metody. Na przykład można użyć następującego konstruktora:

```fsharp
new Type10("ten")
```

Wystąpienie dostarczonego typu jest tworzone z danymi źródłowymi "dziesięć". Być może zauważono, że `InvokeCode` Funkcja zwraca cytat. Wejście do tej funkcji jest listą wyrażeń, jeden na każdy parametr konstruktora. W takim przypadku wyrażenie reprezentujące wartość jednego parametru jest dostępne w `args.[0]` . Kod wywołania konstruktora przekształca wartość zwracaną na typ wymazany `obj` . Po dodaniu drugiego podanego konstruktora do typu utworzysz podaną Właściwość wystąpienia:

```fsharp
let instanceProp =
    ProvidedProperty(propertyName = "InstanceProperty",
                     propertyType = typeof<int>,
                     getterCode= (fun args ->
                        <@@ ((%%(args.[0]) : obj) :?> string).Length @@>))
instanceProp.AddXmlDocDelayed(fun () -> "This is an instance property")
t.AddMember instanceProp
```

Pobranie tej właściwości zwróci długość ciągu, który jest obiektem reprezentacji. `GetterCode`Właściwość zwraca cytat F #, który określa kod, który kompilator generuje do uzyskania właściwości. Podobnie `InvokeCode` , `GetterCode` Funkcja zwraca cytat. Kompilator hosta wywołuje tę funkcję z listą argumentów. W takim przypadku argumenty zawierają tylko pojedyncze wyrażenie, które reprezentuje wystąpienie, na którym jest wywoływana metoda pobierająca, do której można uzyskać dostęp za pomocą `args.[0]` . Implementacja `GetterCode` następnie jest przekształcana w cudzysłów wynikowy w typie wymazania `obj` , a Rzutowanie jest używane do zaspokojenia mechanizmu kompilatora do sprawdzania typów, które obiekt jest ciągiem. Następna część z `makeOneProvidedType` udostępnia metodę wystąpienia z jednym parametrem.

```fsharp
let instanceMeth =
    ProvidedMethod(methodName = "InstanceMethod",
                   parameters = [ProvidedParameter("x",typeof<int>)],
                   returnType = typeof<char>,
                   invokeCode = (fun args ->
                       <@@ ((%%(args.[0]) : obj) :?> string).Chars(%%(args.[1]) : int) @@>))

instanceMeth.AddXmlDocDelayed(fun () -> "This is an instance method")
// Add the instance method to the type.
t.AddMember instanceMeth
```

Na koniec Utwórz zagnieżdżony typ, który zawiera 100 właściwości zagnieżdżonych. Tworzenie tego typu zagnieżdżonego i jego właściwości jest opóźnione, czyli obliczanym na żądanie.

```fsharp
t.AddMembersDelayed(fun () ->
  let nestedType = ProvidedTypeDefinition("NestedType", Some typeof<obj>)

  nestedType.AddMembersDelayed (fun () ->
    let staticPropsInNestedType =
      [
          for i in 1 .. 100 ->
              let valueOfTheProperty = "I am string "  + string i

              let p =
                ProvidedProperty(propertyName = "StaticProperty" + string i,
                  propertyType = typeof<string>,
                  isStatic = true,
                  getterCode= (fun args -> <@@ valueOfTheProperty @@>))

              p.AddXmlDocDelayed(fun () ->
                  $"This is StaticProperty{i} on NestedType")

              p
      ]

    staticPropsInNestedType)

  [nestedType])
```

### <a name="details-about-erased-provided-types"></a>Szczegóły dotyczące wymazanych typów

Przykład w tej sekcji zawiera tylko *wymazane dostarczone typy*, które są szczególnie przydatne w następujących sytuacjach:

- Podczas pisania dostawcy dla przestrzeni informacyjnej zawierającej tylko dane i metody.

- Podczas pisania dostawcy, w którym dokładna semantyka typu środowiska uruchomieniowego nie jest krytyczna dla praktycznego użycia przestrzeni informacyjnej.

- Podczas pisania dostawcy dla obszaru informacyjnego, który jest tak duży i połączony, nie jest technicznie wykonalny, aby generować rzeczywiste typy .NET dla obszaru informacji.

W tym przykładzie każdy dostarczony typ jest wymazany do typu `obj` , a wszystkie zastosowania typu będą wyświetlane jako typ `obj` w skompilowanym kodzie. W rzeczywistości obiekty bazowe w tych przykładach są ciągami, ale typ będzie wyświetlany jako `System.Object` w skompilowanym kodzie platformy .NET. Podobnie jak w przypadku wszystkich użycia typu wymazywania, można użyć jawnego pakowania, rozpakowywania i rzutowania na wymazywane typy poddanych. W takim przypadku wyjątek rzutowania, który jest nieprawidłowy, może wynikać, gdy obiekt jest używany. Środowisko uruchomieniowe dostawcy może zdefiniować własny prywatny typ reprezentacji, aby pomóc w ochronie przed fałszywymi reprezentacjami. Nie można definiować wymazanych typów w języku F #. Tylko udostępniane typy mogą zostać wymazane. Należy zrozumieć konsekwencje, zarówno praktycznie, jak i semantykę, przy użyciu wymazanych typów dla dostawcy typu lub dostawcy, który udostępnia wymazane typy. Typ wymazany nie ma rzeczywistego typu .NET. W związku z tym nie można przeprowadzić dokładnego odbicia w typie i można przeliczyć wymazywane typy, jeśli używasz rzutowania środowiska uruchomieniowego i innych technik, które opierają się na dokładnej semantyce typu środowiska uruchomieniowego. Podwersja wymazanych typów często skutkuje wyjątkami rzutowania typu w czasie wykonywania.

### <a name="choosing-representations-for-erased-provided-types"></a>Wybieranie reprezentacji dla wymazanych podanych typów

W przypadku niektórych użycia wymazanych typów nie jest wymagana żadna reprezentacja. Na przykład typ, który został wymazany, może zawierać tylko statyczne właściwości i składowe bez konstruktorów, a żadne metody lub właściwości nie zwróci wystąpienia typu. Jeśli można uzyskać dostęp do wystąpień podanego typu, należy wziąć pod uwagę następujące pytania:

**Co to jest wymazanie podanego typu?**

- Wymazanie podanego typu określa sposób wyświetlania w skompilowanym kodzie .NET.

- Wymazywanie dostarczonego typu wymazanej klasy jest zawsze pierwszym niewymazanym typem podstawowym w łańcuchu dziedziczenia typu.

- Wymazywanie dostarczonego typu interfejsu jest zawsze `System.Object` .

**Jakie są reprezentacje dostarczonego typu?**

- Zestaw możliwych obiektów dla podanego typu wymazanego są nazywane jego reprezentacjami. W przykładzie w tym dokumencie reprezentacje wszystkich wymazanych typów `Type1..Type100` są zawsze obiektami ciągu.

Wszystkie reprezentacje dostarczonego typu muszą być zgodne z wymazywaniem podanego typu. (W przeciwnym razie kompilator języka F # zwróci błąd dotyczący użycia dostawcy typów lub niemożliwy do sprawdzenia kod platformy .NET, który jest nieprawidłowy). Dostawca typów jest nieprawidłowy, jeśli zwraca kod, który zawiera nieprawidłową reprezentację.

Można wybrać reprezentację dla dostarczonych obiektów przy użyciu jednej z następujących metod, które są bardzo popularne:

- Jeśli po prostu udostępnisz silnie wpisaną otokę na istniejącym typie .NET, często ma sens, aby typ mógł zostać wymazany do tego typu, używaj wystąpień tego typu jako reprezentacji lub obu. To podejście jest odpowiednie, gdy większość istniejących metod na tym typie nadal ma sens, gdy używana jest silnie wpisana wersja.

- Jeśli chcesz utworzyć interfejs API, który różni się znacznie od istniejącego interfejsu API platformy .NET, warto utworzyć typy środowiska uruchomieniowego, które będą typu wymazywania i reprezentacji dla dostarczonych typów.

W przykładzie w tym dokumencie są stosowane ciągi jako reprezentacje dostarczonych obiektów. Często może być konieczne użycie innych obiektów do przedstawienia. Na przykład można użyć słownika jako zbioru właściwości:

```fsharp
ProvidedConstructor(parameters = [],
    invokeCode= (fun args -> <@@ (new Dictionary<string,obj>()) :> obj @@>))
```

Alternatywnie można zdefiniować typ w dostawcy typu, który będzie używany w czasie wykonywania w celu utworzenia reprezentacji, wraz z co najmniej jedną operacją wykonawczą:

```fsharp
type DataObject() =
    let data = Dictionary<string,obj>()
    member x.RuntimeOperation() = data.Count
```

Podane elementy członkowskie mogą następnie konstruować wystąpienia tego typu obiektu:

```fsharp
ProvidedConstructor(parameters = [],
    invokeCode= (fun args -> <@@ (new DataObject()) :> obj @@>))
```

W takim przypadku możesz (opcjonalnie) używać tego typu jako typu wymazywanego przez określenie tego typu jako `baseType` podczas konstruowania `ProvidedTypeDefinition` :

```fsharp
ProvidedTypeDefinition(…, baseType = Some typeof<DataObject> )
…
ProvidedConstructor(…, InvokeCode = (fun args -> <@@ new DataObject() @@>), …)
```

### <a name="key-lessons"></a>Najważniejsze lekcje

W poprzedniej sekcji wyjaśniono, jak utworzyć prostego, wymazywając dostawcę typów, który zapewnia zakres typów, właściwości i metod. W tej sekcji wyjaśniono również koncepcję typu wymazywania, w tym niektóre zalety i wady zapewniania wymazanych typów od dostawcy typów oraz omówione reprezentacje typów wymazanych.

## <a name="a-type-provider-that-uses-static-parameters"></a>Dostawca typów, który używa parametrów statycznych

Możliwość Sparametryzuj dostawców typów przez dane statyczne umożliwia wiele interesujących scenariuszy, nawet w przypadkach, gdy dostawca nie musi uzyskiwać dostępu do danych lokalnych lub zdalnych. W tej sekcji przedstawiono podstawowe techniki tworzenia tego dostawcy.

### <a name="type-checked-regex-provider"></a>Dostawca zaznaczonego wyrażenia regularnego typu

Załóżmy, że chcesz zaimplementować dostawcę typów dla wyrażeń regularnych, które zawijają <xref:System.Text.RegularExpressions.Regex> biblioteki .NET w interfejsie, który zapewnia następujące gwarancje czasu kompilacji:

- Sprawdzanie, czy wyrażenie regularne jest prawidłowe.

- Udostępnianie nazwanych właściwości na dopasowaniach, które są oparte na dowolnych nazwach grup w wyrażeniu regularnym.

W tej sekcji pokazano, jak za pomocą dostawców typów utworzyć `RegexTyped` Typ, który wzorzec wyrażenia regularnego parameterizes, aby zapewnić te korzyści. Kompilator zgłosi błąd, jeśli dostarczony wzorzec jest nieprawidłowy, a dostawca typów może wyodrębnić grupy ze wzorca, aby można było uzyskać do nich dostęp przy użyciu nazwanych właściwości w dopasowań. Podczas projektowania dostawcy typów należy rozważyć sposób, w jaki jego uwidoczniony interfejs API powinien wyglądać użytkownikom końcowym i jak ten projekt będzie tłumaczyć na kod platformy .NET. Poniższy przykład pokazuje, jak używać takiego interfejsu API do pobierania składników kodu obszaru:

```fsharp
type T = RegexTyped< @"(?<AreaCode>^\d{3})-(?<PhoneNumber>\d{3}-\d{4}$)">
let reg = T()
let result = T.IsMatch("425-555-2345")
let r = reg.Match("425-555-2345").Group_AreaCode.Value //r equals "425"
```

Poniższy przykład pokazuje, jak dostawca typów tłumaczy te wywołania:

```fsharp
let reg = new Regex(@"(?<AreaCode>^\d{3})-(?<PhoneNumber>\d{3}-\d{4}$)")
let result = reg.IsMatch("425-123-2345")
let r = reg.Match("425-123-2345").Groups.["AreaCode"].Value //r equals "425"
```

Pamiętaj o następujących kwestiach:

- Standardowy typ wyrażenia regularnego reprezentuje `RegexTyped` Typ sparametryzowany.

- `RegexTyped`Konstruktor skutkuje wywołaniem konstruktora wyrażenia regularnego, przekazując w argument typu statycznego wzorca.

- Wyniki `Match` metody są reprezentowane przez standardowy <xref:System.Text.RegularExpressions.Match> Typ.

- Każda nazwana grupa skutkuje podaną właściwością i uzyskuje dostęp do właściwości w wyniku użycia indeksatora w `Groups` kolekcji dopasowania.

Poniższy kod stanowi rdzeń logiki w celu zaimplementowania takiego dostawcy, a ten przykład pomija dodanie wszystkich członków do podanego typu. Informacje o każdym dodawanym członku znajdują się w odpowiedniej sekcji w dalszej części tego tematu. Aby uzyskać pełny kod, Pobierz próbkę z [przykładowego pakietu F # 3,0](https://archive.codeplex.com/?p=fsharp3sample) w witrynie sieci Web CodePlex.

```fsharp
namespace Samples.FSharp.RegexTypeProvider

open System.Reflection
open Microsoft.FSharp.Core.CompilerServices
open Samples.FSharp.ProvidedTypes
open System.Text.RegularExpressions

[<TypeProvider>]
type public CheckedRegexProvider() as this =
    inherit TypeProviderForNamespaces()

    // Get the assembly and namespace used to house the provided types
    let thisAssembly = Assembly.GetExecutingAssembly()
    let rootNamespace = "Samples.FSharp.RegexTypeProvider"
    let baseTy = typeof<obj>
    let staticParams = [ProvidedStaticParameter("pattern", typeof<string>)]

    let regexTy = ProvidedTypeDefinition(thisAssembly, rootNamespace, "RegexTyped", Some baseTy)

    do regexTy.DefineStaticParameters(
        parameters=staticParams,
        instantiationFunction=(fun typeName parameterValues ->

          match parameterValues with
          | [| :? string as pattern|] ->

            // Create an instance of the regular expression.
            //
            // This will fail with System.ArgumentException if the regular expression is not valid.
            // The exception will escape the type provider and be reported in client code.
            let r = System.Text.RegularExpressions.Regex(pattern)

            // Declare the typed regex provided type.
            // The type erasure of this type is 'obj', even though the representation will always be a Regex
            // This, combined with hiding the object methods, makes the IntelliSense experience simpler.
            let ty =
              ProvidedTypeDefinition(
                thisAssembly,
                rootNamespace,
                typeName,
                baseType = Some baseTy)

            ...

            ty
          | _ -> failwith "unexpected parameter values"))

    do this.AddNamespace(rootNamespace, [regexTy])

[<TypeProviderAssembly>]
do ()
```

Pamiętaj o następujących kwestiach:

- Dostawca typów przyjmuje dwa parametry statyczne: `pattern` , który jest obowiązkowy, i `options` , które są opcjonalne (z powodu podanej wartości domyślnej).

- Po podaniu argumentów statycznych utworzysz wystąpienie wyrażenia regularnego. To wystąpienie zgłosi wyjątek, jeśli wyrażenie regularne jest źle sformułowane i ten błąd będzie raportowany użytkownikom.

- W ramach `DefineStaticParameters` wywołania zwrotnego definiujesz typ, który będzie zwracany po dostarczeniu argumentów.

- Ten kod `HideObjectMethods` jest ustawiony na wartość true, aby środowisko IntelliSense pozostało usprawnione. Ten atrybut powoduje `Equals` , że `GetHashCode` elementy członkowskie,, `Finalize` i `GetType` są pomijane z list IntelliSense dla podanego obiektu.

- Używasz `obj` jako podstawowego typu metody, ale użyjesz `Regex` obiektu jako reprezentacji tego typu w czasie wykonywania, jak pokazano w następnym przykładzie.

- Wywołanie `Regex` konstruktora zgłasza, <xref:System.ArgumentException> gdy wyrażenie regularne jest nieprawidłowe. Kompilator przechwytuje ten wyjątek i zgłasza komunikat o błędzie do użytkownika w czasie kompilacji lub w edytorze programu Visual Studio. Ten wyjątek umożliwia zweryfikowanie wyrażeń regularnych bez uruchamiania aplikacji.

Zdefiniowany powyżej typ nie jest jeszcze użyteczny, ponieważ nie zawiera żadnych istotnych metod lub właściwości. Najpierw Dodaj metodę statyczną `IsMatch` :

```fsharp
let isMatch =
    ProvidedMethod(
        methodName = "IsMatch",
        parameters = [ProvidedParameter("input", typeof<string>)],
        returnType = typeof<bool>,
        isStatic = true,
        invokeCode = fun args -> <@@ Regex.IsMatch(%%args.[0], pattern) @@>)

isMatch.AddXmlDoc "Indicates whether the regular expression finds a match in the specified input string."
ty.AddMember isMatch
```

Poprzedni kod definiuje metodę `IsMatch` , która pobiera ciąg jako dane wejściowe i zwraca `bool` . Jedyną lewę częścią jest użycie `args` argumentu w `InvokeCode` definicji. W tym przykładzie `args` jest to lista cytatów, która reprezentuje argumenty tej metody. Jeśli metoda jest metodą wystąpienia, pierwszy argument reprezentuje `this` argument. Jednak dla metody statycznej argumenty są tylko jawnymi argumentami metody. Należy zauważyć, że typ cytowanej wartości powinien być zgodny z określonym zwracanym typem (w tym przypadku `bool` ). Należy również zauważyć, że ten kod używa `AddXmlDoc` metody, aby upewnić się, że podana Metoda ma również przydatną dokumentację, którą można dostarczyć za pośrednictwem technologii IntelliSense.

Następnie Dodaj metodę dopasowania wystąpienia. Jednakże ta metoda powinna zwracać wartość dostarczonego `Match` typu, aby można było uzyskać dostęp do grup w sposób silnie określony. W rezultacie należy najpierw zadeklarować `Match` Typ. Ponieważ ten typ jest zależny od wzorca, który został dostarczony jako argument statyczny, ten typ musi być zagnieżdżony w definicji typu sparametryzowanego:

```fsharp
let matchTy =
    ProvidedTypeDefinition(
        "MatchType",
        baseType = Some baseTy,
        hideObjectMethods = true)

ty.AddMember matchTy
```

Następnie należy dodać jedną właściwość do typu dopasowania dla każdej grupy. W czasie wykonywania dopasowanie jest reprezentowane jako <xref:System.Text.RegularExpressions.Match> wartość, dlatego w cudzysłowie definiującym właściwość musi być używana <xref:System.Text.RegularExpressions.Match.Groups> indeksowana właściwość w celu uzyskania odpowiedniej grupy.

```fsharp
for group in r.GetGroupNames() do
    // Ignore the group named 0, which represents all input.
    if group <> "0" then
    let prop =
      ProvidedProperty(
        propertyName = group,
        propertyType = typeof<Group>,
        getterCode = fun args -> <@@ ((%%args.[0]:obj) :?> Match).Groups.[group] @@>)
        prop.AddXmlDoc($"""Gets the ""{group}"" group from this match""")
    matchTy.AddMember prop
```

Należy pamiętać, że dodawana jest dokumentacja XML do podanej właściwości. Należy również zauważyć, że właściwość może zostać odczytana `GetterCode` , jeśli podano funkcję i właściwość może być zapisywana w przypadku `SetterCode` podanej funkcji, więc Właściwość będąca wynikiem jest tylko do odczytu.

Teraz można utworzyć metodę wystąpienia, która zwraca wartość tego `Match` typu:

```fsharp
let matchMethod =
    ProvidedMethod(
        methodName = "Match",
        parameters = [ProvidedParameter("input", typeof<string>)],
        returnType = matchTy,
        invokeCode = fun args -> <@@ ((%%args.[0]:obj) :?> Regex).Match(%%args.[1]) :> obj @@>)

matchMeth.AddXmlDoc "Searches the specified input string for the first occurrence of this regular expression"

ty.AddMember matchMeth
```

Ponieważ tworzysz metodę wystąpienia, `args.[0]` reprezentuje `RegexTyped` wystąpienie, na którym wywoływana jest metoda, i `args.[1]` jest argumentem wejściowym.

Na koniec Podaj konstruktora, aby można było utworzyć wystąpienia podanego typu.

```fsharp
let ctor =
    ProvidedConstructor(
        parameters = [],
        invokeCode = fun args -> <@@ Regex(pattern, options) :> obj @@>)

ctor.AddXmlDoc("Initializes a regular expression instance.")

ty.AddMember ctor
```

Konstruktor jedynie wymazuje do tworzenia standardowego wystąpienia wyrażenia regularnego programu .NET, które jest ponownie opakowane do obiektu, ponieważ `obj` jest wymazywany z podanego typu. Po tej zmianie użycie przykładowego interfejsu API, który określono wcześniej w temacie, działa zgodnie z oczekiwaniami. Następujący kod jest kompletny i końcowy:

```fsharp
namespace Samples.FSharp.RegexTypeProvider

open System.Reflection
open Microsoft.FSharp.Core.CompilerServices
open Samples.FSharp.ProvidedTypes
open System.Text.RegularExpressions

[<TypeProvider>]
type public CheckedRegexProvider() as this =
    inherit TypeProviderForNamespaces()

    // Get the assembly and namespace used to house the provided types.
    let thisAssembly = Assembly.GetExecutingAssembly()
    let rootNamespace = "Samples.FSharp.RegexTypeProvider"
    let baseTy = typeof<obj>
    let staticParams = [ProvidedStaticParameter("pattern", typeof<string>)]

    let regexTy = ProvidedTypeDefinition(thisAssembly, rootNamespace, "RegexTyped", Some baseTy)

    do regexTy.DefineStaticParameters(
        parameters=staticParams,
        instantiationFunction=(fun typeName parameterValues ->

            match parameterValues with
            | [| :? string as pattern|] ->

                // Create an instance of the regular expression.

                let r = System.Text.RegularExpressions.Regex(pattern)

                // Declare the typed regex provided type.

                let ty =
                    ProvidedTypeDefinition(
                        thisAssembly,
                        rootNamespace,
                        typeName,
                        baseType = Some baseTy)

                ty.AddXmlDoc "A strongly typed interface to the regular expression '%s'"

                // Provide strongly typed version of Regex.IsMatch static method.
                let isMatch =
                    ProvidedMethod(
                        methodName = "IsMatch",
                        parameters = [ProvidedParameter("input", typeof<string>)],
                        returnType = typeof<bool>,
                        isStatic = true,
                        invokeCode = fun args -> <@@ Regex.IsMatch(%%args.[0], pattern) @@>)

                isMatch.AddXmlDoc "Indicates whether the regular expression finds a match in the specified input string"

                ty.AddMember isMatch

                // Provided type for matches
                // Again, erase to obj even though the representation will always be a Match
                let matchTy =
                    ProvidedTypeDefinition(
                        "MatchType",
                        baseType = Some baseTy,
                        hideObjectMethods = true)

                // Nest the match type within parameterized Regex type.
                ty.AddMember matchTy

                // Add group properties to match type
                for group in r.GetGroupNames() do
                    // Ignore the group named 0, which represents all input.
                    if group <> "0" then
                        let prop =
                          ProvidedProperty(
                            propertyName = group,
                            propertyType = typeof<Group>,
                            getterCode = fun args -> <@@ ((%%args.[0]:obj) :?> Match).Groups.[group] @@>)
                        prop.AddXmlDoc(sprintf @"Gets the ""%s"" group from this match" group)
                        matchTy.AddMember(prop)

                // Provide strongly typed version of Regex.Match instance method.
                let matchMeth =
                  ProvidedMethod(
                    methodName = "Match",
                    parameters = [ProvidedParameter("input", typeof<string>)],
                    returnType = matchTy,
                    invokeCode = fun args -> <@@ ((%%args.[0]:obj) :?> Regex).Match(%%args.[1]) :> obj @@>)
                matchMeth.AddXmlDoc "Searches the specified input string for the first occurrence of this regular expression"

                ty.AddMember matchMeth

                // Declare a constructor.
                let ctor =
                  ProvidedConstructor(
                    parameters = [],
                    invokeCode = fun args -> <@@ Regex(pattern) :> obj @@>)

                // Add documentation to the constructor.
                ctor.AddXmlDoc "Initializes a regular expression instance"

                ty.AddMember ctor

                ty
            | _ -> failwith "unexpected parameter values"))

    do this.AddNamespace(rootNamespace, [regexTy])

[<TypeProviderAssembly>]
do ()
```

### <a name="key-lessons"></a>Najważniejsze lekcje

W tej sekcji wyjaśniono, jak utworzyć dostawcę typów, który działa na jego parametry statyczne. Dostawca sprawdza parametr statyczny i zapewnia operacje na podstawie jego wartości.

## <a name="a-type-provider-that-is-backed-by-local-data"></a>Dostawca typów, który jest obsługiwany przez dane lokalne

Często można potrzebować dostawców typów do prezentowania interfejsów API na podstawie nie tylko parametrów statycznych, ale również informacji z systemów lokalnych lub zdalnych. W tej sekcji omówiono dostawców typów, które są oparte na danych lokalnych, takich jak lokalne pliki danych.

### <a name="simple-csv-file-provider"></a>Prosty dostawca plików CSV

Jako prosty przykład rozważmy dostawcę typów do uzyskiwania dostępu do danych naukowych w formacie wartości rozdzielanych przecinkami (CSV). W tej sekcji założono, że pliki CSV zawierają wiersz nagłówka, po którym następuje zmiennoprzecinkowe dane, jak przedstawiono w poniższej tabeli:

|Odległość (miernik)|Czas (s)|
|----------------|-------------|
|50,0|3.7|
|100,0|5.2|
|150,0|6.4|

W tej sekcji przedstawiono sposób dostarczania typu, którego można użyć do uzyskania wierszy z `Distance` właściwością typu `float<meter>` i `Time` właściwością typu `float<second>` . Dla uproszczenia wykonywane są następujące założenia:

- Nazwa nagłówka jest mniejsza od jednostki lub ma postać "Name (Unit)" i nie może zawierać przecinków.

- Jednostki to wszystkie jednostki międzynarodowe (SI) systemu, które są zdefiniowane w module [FSharp. Data. UnitSystems. si. UnitNames module (F #)](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-data-unitsystems-si-unitnames.html) .

- Jednostki są proste (na przykład miernik), a nie złożone (na przykład licznik licznika/sekundę).

- Wszystkie kolumny zawierają dane zmiennoprzecinkowe.

Bardziej kompletny dostawca spowodowałaby ograniczenie tych ograniczeń.

Najpierw należy rozważyć, jak powinien wyglądać interfejs API. Mając `info.csv` plik z zawartością poprzedniej tabeli (w formacie rozdzielanym przecinkami), użytkownicy dostawcy powinni mieć możliwość pisania kodu podobnego do następującego przykładu:

```fsharp
let info = new MiniCsv<"info.csv">()
for row in info.Data do
let time = row.Time
printfn $"{float time}"
```

W takim przypadku kompilator powinien przekonwertować te wywołania na podobne do poniższego przykładu:

```fsharp
let info = new CsvFile("info.csv")
for row in info.Data do
let (time:float) = row.[1]
printfn $"%f{float time}"
```

Optymalne tłumaczenie wymaga dostawcy typów w celu zdefiniowania rzeczywistego `CsvFile` typu w zestawie dostawcy typów. Dostawcy typów często polegają na kilku typach pomocników i metodach zawijania ważnych logiki. Ponieważ miary są wymazywane w czasie wykonywania, można użyć `float[]` jako typu wymazania dla wiersza. Kompilator będzie traktować różne kolumny jako mające różne typy miar. Na przykład pierwsza kolumna w naszym przykładzie ma typ `float<meter>` , a drugi ma wartość `float<second>` . Wymazywane reprezentacje mogą jednak być bardzo proste.

Poniższy kod przedstawia rdzeń implementacji.

```fsharp
// Simple type wrapping CSV data
type CsvFile(filename) =
    // Cache the sequence of all data lines (all lines but the first)
    let data =
        seq {
            for line in File.ReadAllLines(filename) |> Seq.skip 1 ->
                line.Split(',') |> Array.map float
        }
        |> Seq.cache
    member _.Data = data

[<TypeProvider>]
type public MiniCsvProvider(cfg:TypeProviderConfig) as this =
    inherit TypeProviderForNamespaces(cfg)

    // Get the assembly and namespace used to house the provided types.
    let asm = System.Reflection.Assembly.GetExecutingAssembly()
    let ns = "Samples.FSharp.MiniCsvProvider"

    // Create the main provided type.
    let csvTy = ProvidedTypeDefinition(asm, ns, "MiniCsv", Some(typeof<obj>))

    // Parameterize the type by the file to use as a template.
    let filename = ProvidedStaticParameter("filename", typeof<string>)
    do csvTy.DefineStaticParameters([filename], fun tyName [| :? string as filename |] ->

        // Resolve the filename relative to the resolution folder.
        let resolvedFilename = Path.Combine(cfg.ResolutionFolder, filename)

        // Get the first line from the file.
        let headerLine = File.ReadLines(resolvedFilename) |> Seq.head

        // Define a provided type for each row, erasing to a float[].
        let rowTy = ProvidedTypeDefinition("Row", Some(typeof<float[]>))

        // Extract header names from the file, splitting on commas.
        // use Regex matching to get the position in the row at which the field occurs
        let headers = Regex.Matches(headerLine, "[^,]+")

        // Add one property per CSV field.
        for i in 0 .. headers.Count - 1 do
            let headerText = headers.[i].Value

            // Try to decompose this header into a name and unit.
            let fieldName, fieldTy =
                let m = Regex.Match(headerText, @"(?<field>.+) \((?<unit>.+)\)")
                if m.Success then

                    let unitName = m.Groups.["unit"].Value
                    let units = ProvidedMeasureBuilder.Default.SI unitName
                    m.Groups.["field"].Value, ProvidedMeasureBuilder.Default.AnnotateType(typeof<float>,[units])

                else
                    // no units, just treat it as a normal float
                    headerText, typeof<float>

            let prop =
                ProvidedProperty(fieldName, fieldTy,
                    getterCode = fun [row] -> <@@ (%%row:float[]).[i] @@>)

            // Add metadata that defines the property's location in the referenced file.
            prop.AddDefinitionLocation(1, headers.[i].Index + 1, filename)
            rowTy.AddMember(prop)

        // Define the provided type, erasing to CsvFile.
        let ty = ProvidedTypeDefinition(asm, ns, tyName, Some(typeof<CsvFile>))

        // Add a parameterless constructor that loads the file that was used to define the schema.
        let ctor0 =
            ProvidedConstructor([],
                invokeCode = fun [] -> <@@ CsvFile(resolvedFilename) @@>)
        ty.AddMember ctor0

        // Add a constructor that takes the file name to load.
        let ctor1 = ProvidedConstructor([ProvidedParameter("filename", typeof<string>)],
            invokeCode = fun [filename] -> <@@ CsvFile(%%filename) @@>)
        ty.AddMember ctor1

        // Add a more strongly typed Data property, which uses the existing property at runtime.
        let prop =
            ProvidedProperty("Data", typedefof<seq<_>>.MakeGenericType(rowTy),
                getterCode = fun [csvFile] -> <@@ (%%csvFile:CsvFile).Data @@>)
        ty.AddMember prop

        // Add the row type as a nested type.
        ty.AddMember rowTy
        ty)

    // Add the type to the namespace.
    do this.AddNamespace(ns, [csvTy])
```

Należy zwrócić uwagę na następujące kwestie dotyczące implementacji:

- Przeciążone konstruktory umożliwiają odczytywanie oryginalnego pliku lub jednego, który ma identyczny schemat. Ten wzorzec jest typowy podczas pisania dostawcy typów dla lokalnych lub zdalnych źródeł danych, a ten wzorzec umożliwia użycie lokalnego pliku jako szablonu dla danych zdalnych.

- Do rozpoznawania względnych nazw plików można użyć wartości [TypeProviderConfig](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-compilerservices-typeproviderconfig.html) , która została przeniesiona do konstruktora dostawcy typów.

- Możesz użyć metody, `AddDefinitionLocation` Aby zdefiniować lokalizację podanych właściwości. W związku z tym, jeśli używasz `Go To Definition` na podanej właściwości, plik CSV zostanie otwarty w programie Visual Studio.

- Możesz użyć typu, `ProvidedMeasureBuilder` Aby wyszukać jednostki si i wygenerować odpowiednie `float<_>` typy.

### <a name="key-lessons"></a>Najważniejsze lekcje

W tej sekcji wyjaśniono, jak utworzyć dostawcę typów dla lokalnego źródła danych z prostym schematem zawartym w samym źródle danych.

## <a name="going-further"></a>Dalsze przechodzenie

Poniższe sekcje zawierają sugestie dotyczące dalszych badań.

### <a name="a-look-at-the-compiled-code-for-erased-types"></a>Przyjrzyj się skompilowanemu kodowi dla wymazanych typów

Aby określić, jak użycie dostawcy typów odnosi się do kodu, który jest emitowany, należy poszukać następującej funkcji przy użyciu `HelloWorldTypeProvider` użytej wcześniej w tym temacie.

```fsharp
let function1 () =
    let obj1 = Samples.HelloWorldTypeProvider.Type1("some data")
    obj1.InstanceProperty
```

Poniżej znajduje się obraz kodu pochodzącego z dekompilowanego przy użyciu ildasm.exe:

```il
.class public abstract auto ansi sealed Module1
extends [mscorlib]System.Object
{
.custom instance void [FSharp.Core]Microsoft.FSharp.Core.CompilationMappingAtt
ribute::.ctor(valuetype [FSharp.Core]Microsoft.FSharp.Core.SourceConstructFlags)
= ( 01 00 07 00 00 00 00 00 )
.method public static int32  function1() cil managed
{
// Code size       24 (0x18)
.maxstack  3
.locals init ([0] object obj1)
IL_0000:  nop
IL_0001:  ldstr      "some data"
IL_0006:  unbox.any  [mscorlib]System.Object
IL_000b:  stloc.0
IL_000c:  ldloc.0
IL_000d:  call       !!0 [FSharp.Core_2]Microsoft.FSharp.Core.LanguagePrimit
ives/IntrinsicFunctions::UnboxGeneric<string>(object)
IL_0012:  callvirt   instance int32 [mscorlib_3]System.String::get_Length()
IL_0017:  ret
} // end of method Module1::function1

} // end of class Module1
```

Jak pokazano w przykładzie, wszystkie wzmianki o typie `Type1` i właściwości zostały `InstanceProperty` wymazane, pozostawiając tylko operacje na typach środowiska uruchomieniowego.

### <a name="design-and-naming-conventions-for-type-providers"></a>Projektowanie i nazewnictwo Konwencji dla dostawców typów

Podczas tworzenia dostawców typów należy przestrzegać następujących konwencji.

**Dostawcy dla protokołów łączności** Ogólnie rzecz biorąc nazwy większości bibliotek DLL dostawcy dla protokołów łączności danych i usług, takich jak połączenia OData lub SQL, powinny kończyć się na `TypeProvider` lub `TypeProviders` . Na przykład użyj nazwy biblioteki DLL, która jest podobna do następującego ciągu:

`Fabrikam.Management.BasicTypeProviders.dll`

Upewnij się, że podane typy są członkami odpowiadającej przestrzeni nazw, i wskaż wdrożony protokół łączności:

```fsharp
  Fabrikam.Management.BasicTypeProviders.WmiConnection<…>
  Fabrikam.Management.BasicTypeProviders.DataProtocolConnection<…>
```

**Dostawcy narzędzi do ogólnego kodowania**.  Dla dostawcy typów narzędzi, takich jak dla wyrażeń regularnych, dostawca typów może być częścią biblioteki podstawowej, jak pokazano w poniższym przykładzie:

```fsharp
#r "Fabrikam.Core.Text.Utilities.dll"
```

W takim przypadku dostarczony typ pojawi się w odpowiednim punkcie zgodnie z normalnymi konwencjami projektowania platformy .NET:

```fsharp
  open Fabrikam.Core.Text.RegexTyped

  let regex = new RegexTyped<"a+b+a+b+">()
```

**Pojedyncze źródła danych**. Niektórzy dostawcy typów nawiązują połączenie z pojedynczym dedykowanym źródłem danych i zapewniają tylko dane. W takim przypadku należy porzucić `TypeProvider` sufiks i używać zwykłych Konwencji do nadawania nazw .NET:

```fsharp
#r "Fabrikam.Data.Freebase.dll"

let data = Fabrikam.Data.Freebase.Astronomy.Asteroids
```

Aby uzyskać więcej informacji, zobacz `GetConnection` konwencje projektowe opisane w dalszej części tego tematu.

### <a name="design-patterns-for-type-providers"></a>Wzorce projektowe dla dostawców typów

W poniższych sekcjach opisano wzorce projektowe, których można użyć podczas tworzenia dostawców typów.

#### <a name="the-getconnection-design-pattern"></a>Wzorzec projektu GetConnect

Większość dostawców typów należy napisać, aby używać `GetConnection` wzorca, który jest używany przez dostawców typów w FSharp.Data.TypeProviders.dll, jak pokazano w poniższym przykładzie:

```fsharp
#r "Fabrikam.Data.WebDataStore.dll"

type Service = Fabrikam.Data.WebDataStore<…static connection parameters…>

let connection = Service.GetConnection(…dynamic connection parameters…)

let data = connection.Astronomy.Asteroids
```

#### <a name="type-providers-backed-by-remote-data-and-services"></a>Dostawcy typów z danymi zdalnymi i usługami

Przed utworzeniem dostawcy typów, który jest obsługiwany przez zdalne dane i usługi, należy wziąć pod uwagę różne problemy związane z programowaniem. Te problemy obejmują następujące zagadnienia:

- mapowanie schematu

- dynamiczność i unieważnienie w obecności zmiany schematu

- buforowanie schematu

- asynchroniczne implementacje operacji dostępu do danych

- Obsługa zapytań, w tym zapytań LINQ

- poświadczenia i uwierzytelnianie

Ten temat nie omawia problemów w dalszej części tego tematu.

### <a name="additional-authoring-techniques"></a>Dodatkowe techniki tworzenia

Podczas pisania własnych dostawców typów warto skorzystać z następujących dodatkowych technik.

### <a name="creating-types-and-members-on-demand"></a>Tworzenie typów i członków na żądanie

Dostarczony interfejs APItype ma opóźnione wersje elementu AddMember.

```fsharp
  type ProvidedType =
      member AddMemberDelayed  : (unit -> MemberInfo)      -> unit
      member AddMembersDelayed : (unit -> MemberInfo list) -> unit
```

Te wersje są używane do tworzenia przestrzeni na żądanie typów.

### <a name="providing-array-types-and-generic-type-instantiations"></a>Dostarczanie typów tablicowych i wystąpień typów ogólnych

Udostępniane elementy członkowskie (których sygnatury zawierają typy tablic, typy ByRef i wystąpienia typów ogólnych), używając zwykłych `MakeArrayType` , `MakePointerType` i `MakeGenericType` z dowolnego wystąpienia <xref:System.Type> , w tym `ProvidedTypeDefinitions` .

> [!NOTE]
> W niektórych przypadkach może być konieczne użycie pomocnika w programie `ProvidedTypeBuilder.MakeGenericType` .  Aby uzyskać więcej informacji, zobacz [dokumentację zestawu SDK dostawcy typów](https://github.com/fsprojects/FSharp.TypeProviders.SDK/blob/master/README.md#explicit-construction-of-code-makegenerictype-makegenericmethod-and-uncheckedquotations) .

### <a name="providing-unit-of-measure-annotations"></a>Dostarczanie adnotacji jednostki miary

Interfejs API ProvidedTypes zapewnia pomocników do zapewniania adnotacji miar. Na przykład, aby podać typ `float<kg>` , należy użyć następującego kodu:

```fsharp
  let measures = ProvidedMeasureBuilder.Default
  let kg = measures.SI "kilogram"
  let m = measures.SI "meter"
  let float_kg = measures.AnnotateType(typeof<float>,[kg])
```

  Aby podać typ `Nullable<decimal<kg/m^2>>` , użyj następującego kodu:

```fsharp
  let kgpm2 = measures.Ratio(kg, measures.Square m)
  let dkgpm2 = measures.AnnotateType(typeof<decimal>,[kgpm2])
  let nullableDecimal_kgpm2 = typedefof<System.Nullable<_>>.MakeGenericType [|dkgpm2 |]
```

### <a name="accessing-project-local-or-script-local-resources"></a>Uzyskiwanie dostępu do zasobów Project-Local lub Script-Local

Podczas konstruowania każde wystąpienie dostawcy typów może mieć określoną `TypeProviderConfig` wartość. Ta wartość zawiera "folder rozpoznawania" dla dostawcy (czyli folder projektu dla kompilacji lub katalog zawierający skrypt), listę zestawów, do których się odwołuje, i inne informacje.

### <a name="invalidation"></a>Unieważniania

Dostawcy mogą zgłaszać sygnały unieważnienia, aby powiadomić usługę języka F # o zmianach założeń schematu. Po wystąpieniu unieważnienia typecheck jest wykonywane w przypadku, gdy dostawca jest hostowany w programie Visual Studio. Ten sygnał zostanie zignorowany, gdy dostawca jest hostowany w F# Interactive lub przez kompilator F # (fsc.exe).

### <a name="caching-schema-information"></a>Buforowanie informacji o schemacie

Dostawcy muszą często buforować dostęp do informacji o schemacie. Dane w pamięci podręcznej powinny być przechowywane przy użyciu nazwy pliku, która jest podawana jako parametr statyczny lub jako dane użytkownika. Przykładem buforowania schematu jest `LocalSchemaFile` parametr w dostawcach typów w `FSharp.Data.TypeProviders` zestawie. W implementacji tych dostawców ten parametr statyczny kieruje dostawcę typów do użycia informacji o schemacie w określonym pliku lokalnym zamiast uzyskiwania dostępu do źródła danych za pośrednictwem sieci. Aby użyć informacji o schemacie buforowanym, należy również ustawić parametr statyczny `ForceUpdate` na `false` . Możesz użyć podobnej techniki, aby włączyć dostęp do danych w trybie online i offline.

### <a name="backing-assembly"></a>Zestaw kopii zapasowych

Podczas kompilowania `.dll` pliku lub plik `.exe` kopii zapasowej dll dla generowanych typów jest statycznie połączony z powstałym zestawem. Ten link jest tworzony przez skopiowanie definicji typu języka pośredniego (IL) i wszystkich zasobów zarządzanych z zestawu zapasowego do końcowego zestawu. W przypadku korzystania z F# Interactive plik kopii zapasowej dll nie jest kopiowany i jest ładowany bezpośrednio do procesu F# Interactive.

### <a name="exceptions-and-diagnostics-from-type-providers"></a>Wyjątki i Diagnostyka od dostawców typów

Wszystkie zastosowania wszystkich elementów członkowskich z dostarczonych typów mogą generować wyjątki. We wszystkich przypadkach, jeśli dostawca typu zgłasza wyjątek, kompilator hosta podzieli błąd na dostawcę określonego typu.

- Wyjątki dostawcy typów nigdy nie powinny powodować wewnętrznych błędów kompilatora.

- Dostawcy typów nie mogą raportować ostrzeżeń.

- Gdy dostawca typów jest hostowany w kompilatorze F #, środowisku deweloperskim F # lub F# Interactive, wszystkie wyjątki od tego dostawcy są przechwytywane. Właściwość Message jest zawsze tekstem błędu i nie pojawia się ślad stosu. Jeśli zamierzasz zgłosić wyjątek, możesz zgłosić następujące przykłady: `System.NotSupportedException` , `System.IO.IOException` , `System.Exception` .

#### <a name="providing-generated-types"></a>Zapewnianie wygenerowanych typów

Do tej pory ten dokument wyjaśnia, jak zapewnić typy wymazane. Można również użyć mechanizmu dostawcy typów w języku F #, aby udostępnić wygenerowane typy, które są dodawane jako prawdziwe definicje typów .NET do programu użytkownika. Należy odwołać się do wygenerowanych typów przy użyciu definicji typu.

```fsharp
open Microsoft.FSharp.TypeProviders

type Service = ODataService<"http://services.odata.org/Northwind/Northwind.svc/">
```

Kod pomocnika ProvidedTypes-0,2, który jest częścią wersji programu F # 3,0, ma ograniczoną obsługę tylko w celu zapewnienia wygenerowanych typów. Następujące instrukcje muszą mieć wartość true w przypadku wygenerowanej definicji typu:

- `isErased` musi być ustawiony na `false` .

- Wygenerowany typ należy dodać do nowo skonstruowanego elementu `ProvidedAssembly()` , który reprezentuje kontener dla wygenerowanych fragmentów kodu.

- Dostawca musi mieć zestaw, który ma rzeczywiste kopie zapasowe pliku .NET. dll z pasującym plikiem. dll na dysku.

## <a name="rules-and-limitations"></a>Zasady i ograniczenia

Podczas pisania dostawców typów należy pamiętać o następujących regułach i ograniczeniach.

### <a name="provided-types-must-be-reachable"></a>Dostarczone typy muszą być dostępne

Wszystkie udostępniane typy powinny być dostępne z typów niezagnieżdżonych. Typy niezagnieżdżone są podawane w wywołaniu `TypeProviderForNamespaces` konstruktora lub wywołaniu `AddNamespace` . Na przykład, jeśli dostawca udostępnia typ `StaticClass.P : T` , należy się upewnić, że T nie jest typem zagnieżdżonym lub jest zagnieżdżony w jednym z nich.

Na przykład niektórzy dostawcy mają klasę statyczną, taką jak `DataTypes` , która zawiera te `T1, T2, T3, ...` typy. W przeciwnym razie błąd wskazuje, że znaleziono odwołanie do typu T w zestawie A, ale nie można odnaleźć typu w tym zestawie. Jeśli ten błąd pojawia się, sprawdź, czy wszystkie podtypy są osiągalne z typów dostawcy. Uwaga: te `T1, T2, T3...` typy są określane jako typy *na bieżąco* . Pamiętaj, aby umieścić je w dostępnej przestrzeni nazw lub typie nadrzędnym.

### <a name="limitations-of-the-type-provider-mechanism"></a>Ograniczenia mechanizmu dostawcy typów

Mechanizm dostawcy typów w F # ma następujące ograniczenia:

- Podstawowa infrastruktura dla dostawców typów w języku F # nie obsługuje podanych typów ogólnych ani dostarczonych metod ogólnych.

- Mechanizm nie obsługuje zagnieżdżonych typów z parametrami statycznymi.

## <a name="development-tips"></a>Porady dotyczące projektowania

Podczas procesu tworzenia warto poznać następujące wskazówki:

### <a name="run-two-instances-of-visual-studio"></a>Uruchom dwa wystąpienia programu Visual Studio

Można opracowywać dostawcę typów w jednym wystąpieniu i testować dostawcę w inny sposób, ponieważ test IDE będzie miał blokadę w pliku dll, który uniemożliwia ponowne skompilowanie dostawcy typów. W tym celu należy zamknąć drugie wystąpienie programu Visual Studio, gdy dostawca jest skompilowany w pierwszym wystąpieniu, a następnie należy ponownie otworzyć drugie wystąpienie po skompilowaniu dostawcy.

### <a name="debug-type-providers-by-using-invocations-of-fscexe"></a>Debuguj dostawców typów przy użyciu wywołań fsc.exe

Dostawców typów można wywoływać przy użyciu następujących narzędzi:

- fsc.exe (kompilator wiersza polecenia F #)

- fsi.exe (kompilator F# Interactive)

- devenv.exe (Visual Studio)

Można często debugować dostawców typów, używając fsc.exe w pliku skryptu testowego (na przykład Script. FSX). Debuger można uruchomić z poziomu wiersza polecenia.

```console
devenv /debugexe fsc.exe script.fsx
```

  Możesz użyć rejestrowania do-stdout.

## <a name="see-also"></a>Zobacz także

- [Dostawcy typów](index.md)
- [Zestaw SDK dostawcy typów](https://github.com/fsprojects/FSharp.TypeProviders.SDK)
