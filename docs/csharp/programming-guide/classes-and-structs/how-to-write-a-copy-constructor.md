---
title: Jak napisać Konstruktor kopiujący — Przewodnik programowania w języku C#
description: Dowiedz się, jak napisać Konstruktor kopiujący w języku C#, który przyjmuje wystąpienie klasy i zwraca nowe wystąpienie z wartościami wejściowymi.
ms.date: 07/20/2015
helpviewer_keywords:
- C# Language, copy constructor
- copy constructor [C#]
ms.topic: how-to
ms.custom: contperf-fy21q2
ms.assetid: fba899b5-fc41-428e-a745-3ebdbf37990a
ms.openlocfilehash: dfc702bfe183b3712b20c64f9e82d2d3c3edd6d5
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2020
ms.locfileid: "97512375"
---
# <a name="how-to-write-a-copy-constructor-c-programming-guide"></a>Jak napisać Konstruktor kopiujący (Przewodnik programowania w języku C#)

Język C# nie udostępnia konstruktora kopiującego dla obiektów, ale można napisać jeden siebie.  
  
## <a name="example"></a>Przykład  

 W poniższym przykładzie `Person` [Klasa](../../language-reference/keywords/class.md) definiuje Konstruktor kopiujący, który przyjmuje, jako argument, wystąpienie `Person` . Wartości właściwości argumentu są przypisywane do właściwości nowego wystąpienia `Person` . Kod zawiera alternatywny Konstruktor kopiujący, który wysyła `Name` `Age` właściwości i wystąpienia, które chcesz skopiować do konstruktora wystąpienia klasy.  
  
 [!code-csharp[csProgGuideObjects#16](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#16)]  
  
## <a name="see-also"></a>Zobacz też

- <xref:System.ICloneable>
- [Przewodnik programowania w języku C#](../index.md)
- [Klasy i struktury](./index.md)
- [Konstruktory](./constructors.md)
- [Finalizatory](./destructors.md)
