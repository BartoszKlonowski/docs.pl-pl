---
title: Co nowego w języku C# 7,3
description: Omówienie nowych funkcji w języku C# 7,3
ms.date: 05/16/2018
ms.openlocfilehash: cd8f554516fb5078d9d2ed1eec787f36e8f4c7a7
ms.sourcegitcommit: cb27c01a8b0b4630148374638aff4e2221f90b22
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/09/2020
ms.locfileid: "86174760"
---
# <a name="whats-new-in-c-73"></a>Co nowego w języku C# 7,3

Istnieją dwa główne motywy w wersji C# 7,3. Jeden motyw udostępnia funkcje, które umożliwiają bezpieczny kod, tak jak kod niebezpieczny. Drugi motyw zawiera ulepszenia przyrostowe istniejących funkcji. Ponadto w tej wersji dodano nowe opcje kompilatora.

Poniższe nowe funkcje obsługują motyw lepszej wydajności dla bezpiecznego kodu:

- Można uzyskać dostęp do stałych pól bez przypinania.
- Zmienne lokalne można przypisywać ponownie `ref` .
- Inicjatorów można używać w `stackalloc` tablicach.
- Można używać `fixed` instrukcji z dowolnym typem, który obsługuje wzorzec.
- Można użyć dodatkowych ograniczeń ogólnych.

W istniejących funkcjach wprowadzono następujące ulepszenia:

- Można testować `==` i `!=` z typami krotek.
- Zmiennych wyrażeń można używać w większej liczbie lokalizacji.
- Możesz dołączyć atrybuty do pola zapasowego właściwości, które są implementowane automatycznie.
- Ulepszono metodę rozdzielczości, gdy argumenty różnią się od `in` .
- Rozwiązanie przeciążenia ma teraz mniej niejednoznaczne przypadki.

Nowe opcje kompilatora są następujące:

- `-publicsign`Aby włączyć podpisywanie zestawów przez oprogramowanie typu Open Source (OSS).
- `-pathmap`w celu zapewnienia mapowania dla katalogów źródłowych.

Pozostała część tego artykułu zawiera szczegółowe informacje i linki, aby dowiedzieć się więcej na temat poszczególnych ulepszeń. Te funkcje można eksplorować w środowisku za pomocą `dotnet try` Narzędzia globalnego:

1. Zainstaluj narzędzie [dotnet-try](https://github.com/dotnet/try/blob/master/README.md#setup) Global.
1. Sklonuj repozytorium [dotnet/try-Samples](https://github.com/dotnet/try-samples) .
1. Ustaw bieżący katalog na podkatalog *csharp7* dla repozytorium *try-Samples* .
1. Uruchom polecenie `dotnet try`.

## <a name="enabling-more-efficient-safe-code"></a>Włączanie bardziej wydajnego bezpiecznego kodu

Należy mieć możliwość bezpiecznego pisania kodu w języku C#, który wykonuje, a także kod niebezpieczny. Bezpieczny kod unika klas błędów, takich jak przekroczenia buforu, nieużywane wskaźniki i inne błędy dostępu do pamięci. Te nowe funkcje rozszerzają możliwości zweryfikowania bezpiecznego kodu. Staraj się pisać więcej kodu przy użyciu bezpiecznych konstrukcji. Te funkcje ułatwiają to.

### <a name="indexing-fixed-fields-does-not-require-pinning"></a>Pola indeksowania nie `fixed` wymagają przypinania

Rozważmy tę strukturę:

```csharp
unsafe struct S
{
    public fixed int myFixedField[10];
}
```

We wcześniejszych wersjach języka C# wymagało przypinania zmiennej w celu uzyskania dostępu do jednej z liczb całkowitych, które są częścią `myFixedField` . Teraz Poniższy kod kompiluje bez przypinania zmiennej `p` wewnątrz oddzielnej `fixed` instrukcji:

```csharp
class C
{
    static S s = new S();

    unsafe public void M()
    {
        int p = s.myFixedField[5];
    }
}
```

Zmienna `p` uzyskuje dostęp do jednego elementu w `myFixedField` . Nie musisz deklarować odrębnej `int*` zmiennej. Pamiętaj, że nadal potrzebujesz `unsafe` kontekstu. We wcześniejszych wersjach języka C# należy zadeklarować drugi stały wskaźnik:

```csharp
class C
{
    static S s = new S();

    unsafe public void M()
    {
        fixed (int* ptr = s.myFixedField)
        {
            int p = ptr[5];
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz artykuł na temat [ `fixed` instrukcji](../language-reference/keywords/fixed-statement.md).

### <a name="ref-local-variables-may-be-reassigned"></a>`ref`zmienne lokalne mogą zostać ponownie przypisane

Teraz elementy `ref` lokalne mogą zostać ponownie przypisane, aby odwoływać się do różnych wystąpień po zainicjowaniu. Poniższy kod jest teraz kompilowany:

```csharp
ref VeryLargeStruct refLocal = ref veryLargeStruct; // initialization
refLocal = ref anotherVeryLargeStruct; // reassigned, refLocal refers to different storage.
```

Aby uzyskać więcej informacji, zobacz artykuł dotyczący [ `ref` zwrotów i elementów `ref` lokalnych](../programming-guide/classes-and-structs/ref-returns.md)oraz artykuł w artykule [`foreach`](../language-reference/keywords/foreach-in.md) .

### <a name="stackalloc-arrays-support-initializers"></a>`stackalloc`Tablice obsługują inicjatory

Po zainicjowaniu można określić wartości dla elementów w tablicy:

```csharp
var arr = new int[3] {1, 2, 3};
var arr2 = new int[] {1, 2, 3};
```

Teraz tę samą składnię można zastosować do tablic, które są zadeklarowane za pomocą `stackalloc` :

```csharp
int* pArr = stackalloc int[3] {1, 2, 3};
int* pArr2 = stackalloc int[] {1, 2, 3};
Span<int> arr = stackalloc [] {1, 2, 3};
```

Aby uzyskać więcej informacji, zobacz artykuł dotyczący [ `stackalloc` operatorów](../language-reference/operators/stackalloc.md) .

### <a name="more-types-support-the-fixed-statement"></a>Więcej typów obsługuje `fixed` instrukcja

`fixed`Instrukcja obsługuje ograniczony zestaw typów. Począwszy od języka C# 7,3, dowolnego typu, który zawiera `GetPinnableReference()` metodę zwracającą `ref T` lub `ref readonly T` może być `fixed` . Dodanie tej funkcji oznacza, że `fixed` mogą być używane z <xref:System.Span%601?displayProperty=nameWithType> i powiązane typy.

Aby uzyskać więcej informacji, zobacz artykuł [ `fixed` instrukcji](../language-reference/keywords/fixed-statement.md) w dokumentacji języka.

### <a name="enhanced-generic-constraints"></a>Ulepszone ograniczenia ogólne

Teraz można określić typ <xref:System.Enum?displayProperty=nameWithType> lub <xref:System.Delegate?displayProperty=nameWithType> jako ograniczenia klasy bazowej dla parametru typu.

Można również użyć nowego `unmanaged` ograniczenia, aby określić, że parametr typu musi być [typem niezarządzanym](../language-reference/builtin-types/unmanaged-types.md)null.

Aby uzyskać więcej informacji, zobacz artykuły dotyczące [ `where` ograniczeń ogólnych](../language-reference/keywords/where-generic-type-constraint.md) i [ograniczeń dla parametrów typu](../programming-guide/generics/constraints-on-type-parameters.md).

Dodanie tych ograniczeń do istniejących typów jest [niezgodną zmianą](version-update-considerations.md#incompatible-changes). Zamknięte typy ogólne nie mogą już odpowiadać tym nowym ograniczeniom.

## <a name="make-existing-features-better"></a>Ulepszanie istniejących funkcji

Drugi motyw zawiera ulepszenia funkcji w języku. Te funkcje zwiększają produktywność podczas pisania języka C#.

### <a name="tuples-support--and-"></a>Krotki obsługują `==` i`!=`

Typy krotek języka C# teraz obsługują `==` i `!=` . Aby uzyskać więcej informacji, zobacz sekcję [równość krotki](../language-reference/builtin-types/value-tuples.md#tuple-equality) w artykule [typy krotek](../language-reference/builtin-types/value-tuples.md) .

### <a name="attach-attributes-to-the-backing-fields-for-auto-implemented-properties"></a>Dołącz atrybuty do pól zapasowych dla automatycznie implementowanych właściwości

Ta składnia jest teraz obsługiwana:

```csharp
[field: SomeThingAboutFieldAttribute]
public int SomeProperty { get; set; }
```

Ten atrybut `SomeThingAboutFieldAttribute` jest stosowany do pola zapasowego wygenerowanego przez kompilator dla `SomeProperty` . Aby uzyskać więcej informacji, zobacz [atrybuty](../programming-guide/concepts/attributes/index.md) w Przewodnik programowania w języku C#.

### <a name="in-method-overload-resolution-tiebreaker"></a>`in`wczesnego przeciążania metody

Po `in` dodaniu modyfikatora argumentu te dwie metody spowodują niejednoznaczność:

```csharp
static void M(S arg);
static void M(in S arg);
```

Teraz Przeciążenie wartości (najpierw w poprzednim przykładzie) przeciążenia jest lepsze niż wersja odwołania do tylko do odczytu. Aby wywołać wersję z argumentem odwołania tylko do odczytu, należy dołączyć `in` modyfikator podczas wywoływania metody.

> [!NOTE]
> Ta implementacja została zaimplementowana jako Poprawka błędu. To nie jest już niejednoznaczne nawet w przypadku wersji językowej ustawionej na "7,2".

Aby uzyskać więcej informacji, zobacz artykuł dotyczący [ `in` modyfikatora parametru](../language-reference/keywords/in-parameter-modifier.md).

### <a name="extend-expression-variables-in-initializers"></a>Rozszerzone zmienne wyrażeń w inicjatorach

Składnia dodana w języku C# 7,0 do zezwalania na `out` deklaracje zmiennych w celu uwzględnienia inicjatorów pól, inicjatorów właściwości, inicjatorów konstruktora i klauzul zapytania. Umożliwia to wykonywanie kodu, takiego jak Poniższy przykład:

```csharp
public class B
{
   public B(int i, out int j)
   {
      j = i;
   }
}

public class D : B
{
   public D(int i) : base(i, out var j)
   {
      Console.WriteLine($"The value of 'j' is {j}");
   }
}
```

### <a name="improved-overload-candidates"></a>Ulepszone kandydujące metody rozwiązywania przeciążenia

W każdej wersji reguły rozpoznawania przeciążenia zostały zaktualizowane w celu rozwiązania sytuacji, w których niejednoznaczne wywołania metod mają oczywisty wybór. W tej wersji dodano trzy nowe reguły, które ułatwiają wybór oczywisty przez kompilator:

1. Gdy grupa metod zawiera zarówno wystąpienie, jak i statyczne elementy członkowskie, kompilator odrzuca elementy członkowskie wystąpienia, jeśli metoda została wywołana bez odbiorcy wystąpienia lub kontekstu. Kompilator odrzuca statyczne elementy członkowskie, jeśli metoda została wywołana z odbiornikiem wystąpienia. Gdy nie ma odbiornika, kompilator zawiera tylko statyczne elementy członkowskie w kontekście statycznym, w przeciwnym razie elementy członkowskie statyczne i wystąpienia. Gdy odbiorca jest niejednoznacznie wystąpieniem lub typem, kompilator zawiera oba te elementy. Statyczny kontekst, w którym niejawny `this` odbiornik wystąpienia nie może być używany, zawiera treść elementów członkowskich, gdzie nie `this` jest zdefiniowana, takich jak statyczne elementy członkowskie, a także miejsca, w których `this` nie można ich używać, takich jak inicjatory pól i konstruktory.
1. Gdy grupa metod zawiera kilka metod ogólnych, których argumenty typu nie spełniają ograniczeń, te elementy członkowskie są usuwane z zestawu kandydatów.
1. Dla konwersji grup metod, metody kandydujące, których typ zwracany nie jest zgodny z typem zwracanym delegata, są usuwane z zestawu.

Ta zmiana zostanie wykorzystana tylko dlatego, że w przypadku niejednoznacznych przeciążeń metod znajdziesz mniej błędów kompilatora, gdy masz pewność, która metoda jest lepsza.

## <a name="new-compiler-options"></a>Nowe opcje kompilatora

Nowe opcje kompilatora obsługują nowe scenariusze kompilacji i DevOps dla programów w języku C#.

### <a name="public-or-open-source-signing"></a>Podpisywanie publiczne lub Open Source

`-publicsign`Opcja kompilatora instruuje kompilator do podpisania zestawu przy użyciu klucza publicznego. Zestaw jest oznaczony jako podpisany, ale podpis jest pobierany z klucza publicznego. Ta opcja umożliwia tworzenie podpisanych zestawów z projektów typu "open source" przy użyciu klucza publicznego.

Aby uzyskać więcej informacji, zobacz [publicsign opcji kompilatora](../language-reference/compiler-options/publicsign-compiler-option.md) .

### <a name="pathmap"></a>elemencie pathmap

`-pathmap`Opcja kompilatora instruuje kompilator, aby zamieniać ścieżki źródłowe ze środowiska kompilacji z zamapowanymi ścieżkami źródłowymi. `-pathmap`Opcja steruje ścieżką źródłową zapisaną przez kompilator do plików PDB lub dla <xref:System.Runtime.CompilerServices.CallerFilePathAttribute> .

Aby uzyskać więcej informacji, zobacz [elemencie pathmap opcji kompilatora](../language-reference/compiler-options/pathmap-compiler-option.md) .
