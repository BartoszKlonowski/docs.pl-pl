---
title: Niejawnie wpisane tablice — Przewodnik programowania w języku C#
description: Typ tablicy o typie określonym niejawnie w języku C# jest wywnioskowany na podstawie elementów w inicjatorze tablicy. Używanie tablic o typie określonym niejawnie w wyrażeniach zapytań.
ms.date: 07/20/2015
helpviewer_keywords:
- arrays [C#], implicitly-typed
- implicitly-typed arrays [C#]
- C# language, implicitly typed arrays
ms.assetid: e05be95c-6732-403d-ae42-b35f057cbbea
ms.openlocfilehash: 1f14f68207dfb79c92eaa01ac2a8ffaa08facc03
ms.sourcegitcommit: cf5a800a33de64d0aad6d115ffcc935f32375164
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/20/2020
ms.locfileid: "86474712"
---
# <a name="implicitly-typed-arrays-c-programming-guide"></a>Niejawnie wpisane tablice (Przewodnik programowania w języku C#)

Można utworzyć tablicę z określonym niejawnie, w której typ wystąpienia tablicy jest wywnioskowany na podstawie elementów określonych w inicjatorze tablicy. Reguły dla dowolnej zmiennej o typie określonym niejawnie mają zastosowanie również do tablic o typie określonym niejawnie. Aby uzyskać więcej informacji, zobacz [niejawnie wpisane zmienne lokalne](../classes-and-structs/implicitly-typed-local-variables.md).

Tablice o typie określonym niejawnie są zwykle używane w wyrażeniach zapytań wraz z typami anonimowymi i inicjatorami obiektów i kolekcji.

W poniższych przykładach pokazano, jak utworzyć tablicę o typie określonym niejawnie:

[!code-csharp[csProgGuideLINQ#37](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideLINQ/CS/csRef30LangFeatures_2.cs#37)]

W poprzednim przykładzie Zwróć uwagę, że z tablicami z niejawnie określonym typem, w lewej części instrukcji inicjowania nie są używane żadne nawiasy kwadratowe. Zwróć uwagę na to, że tablice nieregularne są inicjowane przy użyciu `new []` podobnie jak w przypadku tablic jednowymiarowych.

## <a name="implicitly-typed-arrays-in-object-initializers"></a>Tablice o typie określonym niejawnie w inicjatorach obiektów

Podczas tworzenia typu anonimowego, który zawiera tablicę, Tablica musi być niejawnie wpisana w inicjatorze obiektu typu. W poniższym przykładzie `contacts` jest tablicą typów anonimowych niejawnie, z których każdy zawiera tablicę o nazwie `PhoneNumbers` . Należy zauważyć, że `var` słowo kluczowe nie jest używane wewnątrz inicjatorów obiektów.

[!code-csharp[csProgGuideLINQ#38](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideLINQ/CS/csRef30LangFeatures_2.cs#38)]

## <a name="see-also"></a>Zobacz także

- [Przewodnik programowania w języku C#](../index.md)
- [Jawnie wpisana zmienna lokalna](../classes-and-structs/implicitly-typed-local-variables.md)
- [Tablice](./index.md)
- [Typy anonimowe](../classes-and-structs/anonymous-types.md)
- [Inicjatory obiektów i kolekcji](../classes-and-structs/object-and-collection-initializers.md)
- [var](../../language-reference/keywords/var.md)
- [LINQ w C#](../../linq/index.md)
