---
title: Typy wyliczeniowe — odwołanie w C#
description: Dowiedz się więcej na temat typów wyliczeniowych języka C#, które reprezentują wybór lub kombinację opcji
ms.date: 12/13/2019
f1_keywords:
- enum
- enum_CSharpKeyword
helpviewer_keywords:
- enum keyword [C#]
- enum type [C#]
- enumeration type [C#]
- bit flags [C#]
ms.assetid: bbeb9a0f-e9b3-41ab-b0a6-c41b1a08974c
ms.openlocfilehash: a21bdf63247dc5fec95922de017e1d3502e08565
ms.sourcegitcommit: 9d525bb8109216ca1dc9e39c149d4902f4b43da5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2020
ms.locfileid: "96599437"
---
# <a name="enumeration-types-c-reference"></a>Typy wyliczeniowe (odwołanie w C#)

*Typ wyliczenia* (lub *Typ wyliczeniowy*) jest [typem wartości](value-types.md) zdefiniowanym przez zestaw nazwanych stałych podstawowego typu [liczbowego](integral-numeric-types.md) . Aby zdefiniować typ wyliczeniowy, użyj `enum` słowa kluczowego i określ nazwy *elementów członkowskich wyliczenia*:

```csharp
enum Season
{
    Spring,
    Summer,
    Autumn,
    Winter
}
```

Domyślnie skojarzone wartości stałe elementów członkowskich wyliczenia są typu `int` ; zaczynają się od zera i zwiększają się o jeden po kolejności tekstu definicji. Można jawnie określić dowolny inny typ [liczbowy całkowity](integral-numeric-types.md) jako typ podstawowy typu wyliczenia. Można również jawnie określić skojarzone wartości stałe, jak pokazano na poniższym przykładzie:

```csharp
enum ErrorCode : ushort
{
    None = 0,
    Unknown = 1,
    ConnectionLost = 100,
    OutlierReading = 200
}
```

Nie można zdefiniować metody wewnątrz definicji typu wyliczenia. Aby dodać funkcjonalność do typu wyliczenia, Utwórz [metodę rozszerzenia](../../programming-guide/classes-and-structs/extension-methods.md).

Wartość domyślna typu wyliczeniowy `E` jest wartością wygenerowaną przez wyrażenie `(E)0` , nawet jeśli zero nie ma odpowiedniego elementu członkowskiego wyliczenia.

Typ wyliczenia służy do reprezentowania wyboru z zestawu wzajemnie wykluczających się wartości lub kombinacji wyboru. Aby przedstawić kombinację opcji, zdefiniuj typ wyliczenia jako flagi bitowe.

## <a name="enumeration-types-as-bit-flags"></a>Typy wyliczeniowe jako flagi bitowe

Jeśli chcesz, aby typ wyliczeniowy reprezentował kombinację opcji, Zdefiniuj elementy członkowskie wyliczenia dla tych opcji, tak że pojedynczy wybór jest polem bitowym. Oznacza to, że skojarzone wartości tych elementów członkowskich wyliczenia powinny być potęgami dwóch. Następnie można użyć [bitowe operatory logiczne `|` lub `&` ](../operators/bitwise-and-shift-operators.md#enumeration-logical-operators) do łączenia opcji lub przecinających się kombinacji opcji. Aby wskazać, że typ wyliczeniowy deklaruje pola bitowe, Zastosuj do niego atrybut [flags](xref:System.FlagsAttribute) . Jak pokazano na poniższym przykładzie, można także uwzględnić niektóre typowe kombinacje w definicji typu wyliczenia.

[!code-csharp[enum flags](snippets/shared/EnumType.cs#Flags)]

Aby uzyskać więcej informacji i przykładów, zobacz <xref:System.FlagsAttribute?displayProperty=nameWithType> stronę referencyjną interfejsu API i [niewyłączne elementy członkowskie oraz atrybuty flag](/dotnet/api/system.enum#non-exclusive-members-and-the-flags-attribute) na <xref:System.Enum?displayProperty=nameWithType> stronie odwołania interfejsu API.

## <a name="the-systemenum-type-and-enum-constraint"></a>Typ System. Enum i ograniczenie wyliczenia

<xref:System.Enum?displayProperty=nameWithType>Typ jest abstrakcyjną klasą bazową wszystkich typów wyliczeniowych. Zawiera kilka metod uzyskiwania informacji na temat typu wyliczenia i jego wartości. Aby uzyskać więcej informacji i przykładów, zobacz <xref:System.Enum?displayProperty=nameWithType> stronę referencyjną interfejsu API.

Począwszy od języka C# 7,3, można użyć `System.Enum` w ramach ograniczenia klasy bazowej (zwanego [ograniczeniem wyliczenia](../../programming-guide/generics/constraints-on-type-parameters.md#enum-constraints)), aby określić, że parametr typu jest typem wyliczenia. Każdy typ wyliczeniowy spełnia również `struct` ograniczenie, które jest używane do określenia, że parametr typu jest typem wartości niedopuszczających wartości null.

## <a name="conversions"></a>Konwersje

Dla dowolnego typu wyliczenia istnieją jawne konwersje między typem wyliczenia i jego podstawowym typem całkowitym. W przypadku [rzutowania](../operators/type-testing-and-cast.md#cast-expression) wartości wyliczenia na jej typ podstawowy wynik jest skojarzoną wartością całkowitą elementu członkowskiego wyliczenia.

[!code-csharp[enum conversions](snippets/shared/EnumType.cs#Conversions)]

Użyj <xref:System.Enum.IsDefined%2A?displayProperty=nameWithType> metody, aby określić, czy typ wyliczeniowy zawiera element członkowski wyliczenia z określoną wartością skojarzoną.

Dla dowolnego typu wyliczenia istnieją konwersje pakowania [i](../../programming-guide/types/boxing-and-unboxing.md) rozpakowywania do i z <xref:System.Enum?displayProperty=nameWithType> typu, odpowiednio.

## <a name="c-language-specification"></a>specyfikacja języka C#

Aby uzyskać więcej informacji, zobacz następujące sekcje [specyfikacji języka C#](~/_csharplang/spec/introduction.md):

- [Wyliczenia](~/_csharplang/spec/enums.md)
- [Wartości wyliczeniowe i operacje](~/_csharplang/spec/enums.md#enum-values-and-operations)
- [Wyliczanie operatorów logicznych](~/_csharplang/spec/expressions.md#enumeration-logical-operators)
- [Operatory porównania wyliczenia](~/_csharplang/spec/expressions.md#enumeration-comparison-operators)
- [Jawne konwersje wyliczenia](~/_csharplang/spec/conversions.md#explicit-enumeration-conversions)
- [Niejawne konwersje wyliczenia](~/_csharplang/spec/conversions.md#implicit-enumeration-conversions)

## <a name="see-also"></a>Zobacz także

- [Dokumentacja języka C#](../index.md)
- [Wyliczanie ciągów formatujących](../../../standard/base-types/enumeration-format-strings.md)
- [Wskazówki dotyczące projektowania — projekt enum](../../../standard/design-guidelines/enum.md)
- [Wytyczne dotyczące projektowania — wyliczanie konwencji nazewnictwa](../../../standard/design-guidelines/names-of-classes-structs-and-interfaces.md#naming-enumerations)
- [switch, instrukcja](../keywords/switch.md)
