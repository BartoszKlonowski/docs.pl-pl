---
title: Jak używać niejawnie wpisanych zmiennych lokalnych i tablic w wyrażeniu zapytania — Przewodnik programowania w języku C#
description: Użyj niejawnie wpisanych zmiennych lokalnych w języku C#, aby kompilator mógł określić typ zmiennej lokalnej. Musisz użyć ich do przechowywania typów anonimowych.
ms.date: 07/20/2015
helpviewer_keywords:
- implicitly-typed local variables [C#], how to use
ms.topic: how-to
ms.custom: contperf-fy21q2
ms.assetid: 6b7354d2-af79-427a-b6a8-f74eb8fd0b91
ms.openlocfilehash: bd68c913c6f0d410d97973fb28789218f88903b5
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2020
ms.locfileid: "97512388"
---
# <a name="how-to-use-implicitly-typed-local-variables-and-arrays-in-a-query-expression-c-programming-guide"></a>Jak używać niejawnie wpisanych zmiennych lokalnych i tablic w wyrażeniu zapytania (Przewodnik programowania w języku C#)

Możesz użyć niejawnie wpisanych zmiennych lokalnych, ilekroć kompilator ma określić typ zmiennej lokalnej. Należy użyć niejawnie wpisanych zmiennych lokalnych do przechowywania typów anonimowych, które są często używane w wyrażeniach zapytań. Poniższe przykłady ilustrują opcjonalne i wymagane zastosowania niejawnie wpisanych zmiennych lokalnych w zapytaniach.  
  
 Niejawnie wpisane zmienne lokalne są deklarowane przy użyciu słowa kluczowego [var](../../language-reference/keywords/var.md) . Aby uzyskać więcej informacji, zobacz [niejawnie wpisane zmienne lokalne](./implicitly-typed-local-variables.md) i [niejawnie wpisane tablice](../arrays/implicitly-typed-arrays.md).  
  
## <a name="example"></a>Przykład  

 W poniższym przykładzie przedstawiono typowy scenariusz, w którym `var` słowo kluczowe jest wymagane: wyrażenie zapytania, które tworzy sekwencję typów anonimowych. W tym scenariuszu zarówno zmienna zapytania, jak i Zmienna iteracji w `foreach` instrukcji muszą zostać wpisane niejawnie przy użyciu, `var` ponieważ nie masz dostępu do nazwy typu dla typu anonimowego. Aby uzyskać więcej informacji na temat typów anonimowych, zobacz [Typy anonimowe](./anonymous-types.md).  
  
 [!code-csharp[csProgGuideLINQ#32](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideLINQ/CS/csRef30LangFeatures_2.cs#32)]  
  
## <a name="example"></a>Przykład  

 W poniższym przykładzie użyto `var` słowa kluczowego w podobnej sytuacji, ale w którym użycie `var` jest opcjonalne. Ponieważ `student.LastName` jest ciągiem, wykonywanie zapytania zwraca sekwencję ciągów. W związku z tym typ `queryID` może być zadeklarowany jako `System.Collections.Generic.IEnumerable<string>` zamiast `var` . Słowo kluczowe `var` jest używane w celu wygody. W przykładzie zmienna iteracji w `foreach` instrukcji jest jawnie wpisana jako ciąg, ale zamiast tego może być zadeklarowana przy użyciu `var` . Ponieważ typ zmiennej iteracji nie jest typem anonimowym, użycie `var` jest opcją, a nie wymaganie. Pamiętaj, `var` że sam nie jest typem, ale instrukcją kompilatora do wnioskowania i przypisania typu.  
  
 [!code-csharp[csProgGuideLINQ#33](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideLINQ/CS/csRef30LangFeatures_2.cs#33)]  
  
## <a name="see-also"></a>Zobacz też

- [Przewodnik programowania w języku C#](../index.md)
- [Metody rozszerzania](./extension-methods.md)
- [LINQ (zapytanie zintegrowane z językiem)](../../linq/index.md)
- [funkcję](../../language-reference/keywords/var.md)
- [LINQ w C#](../../linq/index.md)
