---
title: Przekazywanie parametrów — Przewodnik programowania w języku C#
description: Można przekazać argument do parametru w języku C# według wartości lub odwołania. Zmiany argumentu przesłane przez odwołanie są utrwalane. Użyj ref lub out do przekazywania przez odwołanie.
ms.date: 07/20/2015
helpviewer_keywords:
- parameters [C#], passing
- passing parameters [C#]
- arguments [C#]
- methods [C#], passing parameters
- C# language, method parameters
ms.assetid: a5c3003f-7441-4710-b8b1-c79de77e0b77
ms.openlocfilehash: 875a42aacf3d7aa4124684aefafdcb07ff4c87d6
ms.sourcegitcommit: 3d84eac0818099c9949035feb96bbe0346358504
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/21/2020
ms.locfileid: "86864738"
---
# <a name="passing-parameters-c-programming-guide"></a>Przekazywanie parametrów (Przewodnik programowania w języku C#)
W języku C# argumenty mogą być przekazane do parametrów przez wartość lub przez odwołanie. Przekazywanie przez odwołanie umożliwia składowe, metody, właściwości, indeksatory, operatory i konstruktory, aby zmienić wartość parametrów i spowodować, że ta zmiana będzie trwała w środowisku wywołującym. Aby przekazać parametr przez odwołanie z intencją zmiany wartości, użyj `ref` `out` słowa kluczowego or. Aby przejść przez odwołanie z intencją uniknięcia kopiowania, ale nie zmiany wartości, użyj `in` modyfikatora. Dla uproszczenia tylko `ref` słowo kluczowe jest używane w przykładach w tym temacie. Aby uzyskać więcej informacji o różnicach między elementami `in` , `ref` , i `out` , zobacz [w](../../language-reference/keywords/in-parameter-modifier.md), [ref](../../language-reference/keywords/ref.md)i [out](../../language-reference/keywords/out-parameter-modifier.md).  
  
 Poniższy przykład ilustruje różnicę między parametrami Value i Reference.  
  
 [!code-csharp[csProgGuideParameters#10](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideParameters/CS/Parameters.cs#10)]  
  
 Aby uzyskać więcej informacji, zobacz następujące tematy:  
  
- [Przekazywanie parametrów typu wartość](./passing-value-type-parameters.md)  
  
- [Przekazywanie parametrów typu odwołanie](./passing-reference-type-parameters.md)  
  
## <a name="c-language-specification"></a>Specyfikacja języka C#  

Aby uzyskać więcej informacji, zobacz [listy argumentów](~/_csharplang/spec/expressions.md#argument-lists) w [specyfikacji języka C#](/dotnet/csharp/language-reference/language-specification/introduction). Specyfikacja języka jest ostatecznym źródłem informacji o składni i użyciu języka C#.
  
## <a name="see-also"></a>Zobacz także

- [Przewodnik programowania w języku C#](../index.md)
- [Metody](./methods.md)
