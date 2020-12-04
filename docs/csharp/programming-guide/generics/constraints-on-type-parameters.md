---
title: Ograniczenia dotyczące parametrów typu — Przewodnik programowania w języku C#
description: Poznaj ograniczenia dotyczące parametrów typu. Ograniczenia informują kompilator, jakie możliwości musi mieć argument typu.
ms.date: 04/12/2018
helpviewer_keywords:
- generics [C#], type constraints
- type constraints [C#]
- type parameters [C#], constraints
- unbound type parameter [C#]
ms.openlocfilehash: 8230dfed11bb4ba21e922827cc1a525ce45ba3e5
ms.sourcegitcommit: 9d525bb8109216ca1dc9e39c149d4902f4b43da5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2020
ms.locfileid: "96599118"
---
# <a name="constraints-on-type-parameters-c-programming-guide"></a>Ograniczenia dotyczące parametrów typu (Przewodnik programowania w języku C#)

Ograniczenia informują kompilator o możliwościach, które argument typu musi zawierać. Bez żadnych ograniczeń argument typu może być dowolnym typem. Kompilator może przyjąć tylko elementy członkowskie <xref:System.Object?displayProperty=nameWithType> , które jest ostateczną klasą bazową dla dowolnego typu .NET. Aby uzyskać więcej informacji, zobacz [Dlaczego należy używać ograniczeń](#why-use-constraints). Jeśli kod klienta używa typu, który nie spełnia warunków ograniczenia, kompilator wygeneruje błąd. Ograniczenia są określone za pomocą `where` kontekstowego słowa kluczowego. W poniższej tabeli wymieniono różne typy ograniczeń:

|Typu|Opis|
|----------------|-----------------|
|`where T : struct`|Argument typu musi być [typem wartości](../../language-reference/builtin-types/value-types.md)niedopuszczający wartości null. Aby uzyskać informacje o typach wartości null, zobacz [dopuszczanie typów wartości null](../../language-reference/builtin-types/nullable-value-types.md). Ponieważ wszystkie typy wartości mają dostępny Konstruktor bez parametrów, `struct` ograniczenie implikuje `new()` ograniczenie i nie można go połączyć z `new()` ograniczeniem. Nie można połączyć `struct` ograniczenia z `unmanaged` ograniczeniem.|
|`where T : class`|Argument typu musi być typem referencyjnym. To ograniczenie dotyczy również dowolnego typu klasy, interfejsu, delegata lub tablicy. W kontekście dopuszczającym wartość null w języku C# 8,0 lub nowszym, `T` musi to być typ referencyjny, który nie dopuszcza wartości null. |
|`where T : class?`|Argument typu musi być typem referencyjnym, DOPUSZCZANYM jako Nullable lub nie dopuszczający wartości null. To ograniczenie dotyczy również dowolnego typu klasy, interfejsu, delegata lub tablicy.|
|`where T : notnull`|Argument typu musi być typem niedopuszczający wartości null. Argument może być typem referencyjnym niedopuszczający wartości null w języku C# 8,0 lub nowszym albo typem wartości innym niż null. |
|`where T : unmanaged`|Argument typu musi być [typem niezarządzanym](../../language-reference/builtin-types/unmanaged-types.md)niedopuszczający wartości null. `unmanaged`Ograniczenie implikuje `struct` ograniczenie i nie można go połączyć z `struct` `new()` ograniczeniami lub.|
|`where T : new()`|Argument typu musi mieć publiczny Konstruktor bez parametrów. W przypadku użycia razem z innymi ograniczeniami, `new()` ograniczenie musi być określone jako ostatnie. `new()`Nie można połączyć ograniczenia z `struct` `unmanaged` ograniczeniami i.|
|`where T :` *\<base class name>*|Argument typu musi być lub pochodzić od określonej klasy bazowej. W kontekście dopuszczającym wartość null w języku C# 8,0 i nowszych `T` musi to być typ referencyjny niedopuszczający wartości null pochodzący od określonej klasy bazowej. |
|`where T :` *\<base class name>?*|Argument typu musi być lub pochodzić od określonej klasy bazowej. W kontekście dopuszczającym wartość null w języku C# 8,0 i nowszych `T` może to być typ dopuszczający wartości null lub niedopuszczający wartości null pochodzący z określonej klasy bazowej. |
|`where T :` *\<interface name>*|Argument typu musi być lub zaimplementować określony interfejs. Można określić wiele ograniczeń interfejsu. Interfejs ograniczający może być również ogólny. W kontekście dopuszczającym wartość null w języku C# 8,0 i nowszych `T` musi być typem niedopuszczającym wartości null, który implementuje określony interfejs.|
|`where T :` *\<interface name>?*|Argument typu musi być lub zaimplementować określony interfejs. Można określić wiele ograniczeń interfejsu. Interfejs ograniczający może być również ogólny. W kontekście dopuszczającym wartość null w języku C# 8,0 `T` może to być typ referencyjny dopuszczający wartość null, typ referencyjny niedopuszczający wartości null lub typ wartości. `T` nie może być typem wartości null.|
|`where T : U`|Argument typu dostarczony dla elementu `T` musi być lub dziedziczyć z argumentu dostarczonego dla `U` . W kontekście dopuszczającym wartość null, jeśli `U` jest typem referencyjnym niedopuszczający wartości null, `T` musi być typem referencyjnym, który nie dopuszcza wartości null. Jeśli `U` jest typem referencyjnym dopuszczającym wartość null, `T` może mieć wartość null lub nie dopuszczający wartości null. |

## <a name="why-use-constraints"></a>Dlaczego warto używać ograniczeń

Ograniczenia określają możliwości i oczekiwania parametru typu. Deklarowanie tych ograniczeń oznacza, że można użyć operacji i wywołań metody typu ograniczenia. Jeśli Klasa ogólna lub metoda korzysta z dowolnej operacji na elementach ogólnych poza prostym przypisaniem lub wywoływanie wszelkich metod nieobsługiwanych przez <xref:System.Object?displayProperty=nameWithType> , należy zastosować ograniczenia do parametru typu. Na przykład ograniczenie klasy bazowej instruuje kompilator, że tylko obiekty tego typu lub pochodne z tego typu będą używane jako argumenty typu. Gdy kompilator ma tę gwarancję, może zezwolić na wywoływanie metod tego typu w klasie generycznej. Poniższy przykład kodu demonstruje funkcjonalność, którą można dodać do `GenericList<T>` klasy (w temacie [wprowadzenie do typów ogólnych](../../../standard/generics/index.md)) przez zastosowanie ograniczenia klasy bazowej.

[!code-csharp[using the class and struct constraints](snippets/GenericWhereConstraints.cs#9)]

Ograniczenie pozwala klasie generycznej używać `Employee.Name` właściwości. Ograniczenie określa, że wszystkie elementy typu `T` mają gwarantowany `Employee` obiekt lub obiekt, który dziedziczy z `Employee` .

Do tego samego parametru typu można zastosować wiele ograniczeń, a same ograniczenia mogą być typami ogólnymi w następujący sposób:

[!code-csharp[using the class and struct constraints](snippets/GenericWhereConstraints.cs#10)]

Podczas stosowania `where T : class` ograniczenia, należy unikać `==` operatorów i `!=` w parametrze typu, ponieważ te operatory przetestuje tylko tożsamość referencyjną, a nie dla równości wartości. To zachowanie występuje nawet wtedy, gdy te operatory są przeciążone w typie, który jest używany jako argument. Poniższy kod ilustruje ten punkt; wynik ma wartość false, mimo że <xref:System.String> Klasa przeciążuje `==` operator.

[!code-csharp[using the class and struct constraints](snippets/GenericWhereConstraints.cs#11)]

Kompilator wie, że `T` jest typem referencyjnym w czasie kompilacji i musi używać domyślnych operatorów, które są prawidłowe dla wszystkich typów referencyjnych. Jeśli konieczne jest przetestowanie pod kątem równości wartości, zalecanym sposobem jest również `where T : IEquatable<T>` zastosowanie `where T : IComparable<T>` ograniczenia or i zaimplementowanie interfejsu w dowolnej klasie, która będzie używana do konstruowania klasy generycznej.

## <a name="constraining-multiple-parameters"></a>Ograniczanie wielu parametrów

Można zastosować ograniczenia do wielu parametrów i wiele ograniczeń do jednego parametru, jak pokazano w następującym przykładzie:

[!code-csharp[using the class and struct constraints](snippets/GenericWhereConstraints.cs#12)]

## <a name="unbounded-type-parameters"></a>Niepowiązane parametry typu

 Parametry typu, które nie mają żadnych ograniczeń, takich jak T w klasie publicznej `SampleClass<T>{}` , są nazywane niezwiązanymi parametrami typu. Parametry typu niepowiązanego mają następujące reguły:

- `!=`Operatory i `==` nie mogą być używane, ponieważ nie ma gwarancji, że konkretny argument typu będzie obsługiwał te operatory.
- Mogą być konwertowane do i z `System.Object` lub jawnie konwertowane na dowolny typ interfejsu.
- Można je porównać z [wartością null](../../language-reference/keywords/null.md). Jeśli parametr niezwiązany jest porównywany z `null` , porównywanie zwróci wartość false, jeśli argument typu jest typem wartości.

## <a name="type-parameters-as-constraints"></a>Parametry typu jako ograniczenia

Użycie parametru typu ogólnego jako ograniczenia jest przydatne, gdy funkcja członkowska z własnym parametrem typu musi ograniczyć ten parametr do parametru typu zawierającego typ, jak pokazano w następującym przykładzie:

[!code-csharp[using the class and struct constraints](snippets/GenericWhereConstraints.cs#13)]

W poprzednim przykładzie, `T` jest ograniczeniem typu w kontekście `Add` metody i niezwiązanym parametrem typu w kontekście `List` klasy.

Parametry typu mogą być również używane jako ograniczenia w definicjach klasy generycznej. Parametr type musi być zadeklarowany w nawiasach kątowych wraz z innymi parametrami typu:

[!code-csharp[using the class and struct constraints](snippets/GenericWhereConstraints.cs#14)]

Użyteczność parametrów typu jako ograniczenia z klasami generycznymi jest ograniczona, ponieważ kompilator może nie zajmować niczego informacji o parametrze typu, z wyjątkiem tego, że pochodzi od `System.Object` . Użyj parametrów typu jako ograniczeń dotyczących klas ogólnych w scenariuszach, w których chcesz wymusić relację dziedziczenia między dwoma parametrami typu.

## <a name="notnull-constraint"></a>Ograniczenie NotNull

Począwszy od języka C# 8,0 w kontekście dopuszczającym wartość null, można użyć `notnull` ograniczenia, aby określić, że argument typu musi być typem wartości niedopuszczających wartości null lub typem referencyjnym, który nie dopuszcza wartości null. `notnull`Ograniczenie może być używane tylko w `nullable enable` kontekście. Kompilator generuje ostrzeżenie w przypadku dodania `notnull` ograniczenia w kontekście Oblivious dopuszczający wartość null.

W przeciwieństwie do innych ograniczeń, gdy argument typu narusza `notnull` ograniczenie, kompilator generuje ostrzeżenie, gdy ten kod jest kompilowany w `nullable enable` kontekście. Jeśli kod jest kompilowany w kontekście Oblivious dopuszczający wartość null, kompilator nie generuje żadnych ostrzeżeń ani błędów.

Począwszy od języka C# 8,0 w kontekście dopuszczającym wartość null, `class` ograniczenie określa, że argument typu musi być typem referencyjnym, który nie dopuszcza wartości null. W kontekście dopuszczającym wartość null, gdy parametr typu jest typem referencyjnym dopuszczającym wartość null, kompilator generuje ostrzeżenie.

## <a name="unmanaged-constraint"></a>Niezarządzany warunek ograniczający

Począwszy od języka C# 7,3, można użyć `unmanaged` ograniczenia, aby określić, że parametr typu musi być [typem niezarządzanym](../../language-reference/builtin-types/unmanaged-types.md)niedopuszczający wartości null. `unmanaged`Ograniczenie umożliwia zapisanie procedur wielokrotnego użytku w celu pracy z typami, które mogą być manipulowane jako bloki pamięci, jak pokazano w następującym przykładzie:

[!code-csharp[using the unmanaged constraint](snippets/GenericWhereConstraints.cs#15)]

Poprzednia metoda musi być skompilowana w `unsafe` kontekście, ponieważ używa `sizeof` operatora na typie, który nie jest znany jako typ wbudowany. Bez `unmanaged` ograniczenia `sizeof` operator jest niedostępny.

`unmanaged`Ograniczenie implikuje `struct` ograniczenie i nie może zostać połączone z nim. Ponieważ `struct` ograniczenie implikuje `new()` ograniczenie, `unmanaged` ograniczenie nie może być również połączone z `new()` ograniczeniem.

## <a name="delegate-constraints"></a>Delegowanie ograniczeń

Począwszy od języka C# 7,3, można użyć <xref:System.Delegate?displayProperty=nameWithType> lub <xref:System.MulticastDelegate?displayProperty=nameWithType> jako ograniczenie klasy bazowej. Środowisko CLR zawsze zezwala na to ograniczenie, ale język C# niedozwolony. `System.Delegate`Ograniczenie pozwala napisać kod, który współpracuje z delegatami w sposób bezpieczny dla typu. Poniższy kod definiuje metodę rozszerzenia, która łączy dwa Delegaty pod warunkiem, że są tego samego typu:

[!code-csharp[using the delegate constraint](snippets/GenericWhereConstraints.cs#16)]

Możesz użyć powyższej metody do łączenia delegatów, które są tego samego typu:

[!code-csharp[using the unmanaged constraint](snippets/GenericWhereConstraints.cs#17)]

Usunięcie komentarza do ostatniego wiersza nie spowoduje skompilowania. Oba typy delegatów `first` `test` , ale są różnymi typami delegatów.

## <a name="enum-constraints"></a>Ograniczenia wyliczeniowe

Począwszy od języka C# 7,3, można również określić <xref:System.Enum?displayProperty=nameWithType> Typ jako ograniczenie klasy bazowej. Środowisko CLR zawsze zezwala na to ograniczenie, ale język C# niedozwolony. Typy ogólne przy użyciu `System.Enum` zapewniają programowanie bezpiecznego typu w celu buforowania wyników z używania metod statycznych w `System.Enum` . Poniższy przykład odnajduje wszystkie prawidłowe wartości dla typu wyliczeniowego, a następnie tworzy słownik, który mapuje te wartości na jego reprezentację w postaci ciągu.

[!code-csharp[using the enum constraint](snippets/GenericWhereConstraints.cs#18)]

`Enum.GetValues` i `Enum.GetName` Użyj odbicia, które ma wpływ na wydajność. Można wywołać, `EnumNamedValues` Aby utworzyć kolekcję, która jest buforowana i ponownie używana zamiast powtarzania wywołań, które wymagają odbicia.

Można go użyć, jak pokazano w poniższym przykładzie, aby utworzyć Wyliczenie i skompilować słownik jego wartości i nazw:

[!code-csharp[enum definition](snippets/GenericWhereConstraints.cs#19)]

[!code-csharp[using the enum constrained method](snippets/GenericWhereConstraints.cs#20)]

## <a name="see-also"></a>Zobacz także

- <xref:System.Collections.Generic>
- [Przewodnik programowania w języku C#](../index.md)
- [Wprowadzenie do typów ogólnych](./index.md)
- [Klasy ogólne](./generic-classes.md)
- [nowe ograniczenie](../../language-reference/keywords/new-constraint.md)
