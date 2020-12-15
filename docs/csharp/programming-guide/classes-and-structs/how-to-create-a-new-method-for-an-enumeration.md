---
title: Jak utworzyć nową metodę dla Przewodnik programowania w języku C#
description: Dowiedz się, jak przy użyciu metod rozszerzania dodać funkcję do wyliczenia w języku C#. Ten przykład pokazuje metodę rozszerzenia o nazwie Pass dla wyliczenia o nazwie klasy.
ms.date: 07/20/2015
helpviewer_keywords:
- enumerations [C#]
- extension methods [C#], for enums
- enum extensibility [C#]
ms.topic: how-to
ms.custom: contperf-fy21q2
ms.assetid: 100106f9-1e54-462c-8ebe-3892fe23b6eb
ms.openlocfilehash: 88afff854b8136bde837db8effb0e0eb512e1099
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2020
ms.locfileid: "97513097"
---
# <a name="how-to-create-a-new-method-for-an-enumeration-c-programming-guide"></a>Jak utworzyć nową metodę dla wyliczenia (Przewodnik programowania w języku C#)

Można użyć metod rozszerzających, aby dodać funkcje specyficzne dla określonego typu wyliczeniowego.  
  
## <a name="example"></a>Przykład  

 W poniższym przykładzie `Grades` Wyliczenie reprezentuje możliwe klasy liter, które student może odebrać w klasie. Metoda rozszerzenia o nazwie `Passing` jest dodawana do `Grades` typu, tak aby każde wystąpienie tego typu było teraz "znane", niezależnie od tego, czy reprezentuje ona przewagę, czy nie.  
  
 [!code-csharp[csProgGuideExtensionMethods#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideExtensionMethods/cs/extensionmethods.cs#2)]  
  
 Należy zauważyć, że `Extensions` Klasa zawiera również zmienną statyczną, która jest aktualizowana dynamicznie i że wartość zwracana metody rozszerzenia odzwierciedla bieżącą wartość tej zmiennej. Pokazuje to, że w tle metody rozszerzające są wywoływane bezpośrednio w klasie statycznej, w której są zdefiniowane.  
  
## <a name="see-also"></a>Zobacz też

- [Przewodnik programowania w języku C#](../index.md)
- [Metody rozszerzania](./extension-methods.md)
