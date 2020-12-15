---
title: 'Porada: definiowanie stałych w języku C#'
description: Dowiedz się, jak definiować stałe w języku C#, które są polami, których wartości są ustawiane w czasie kompilacji. Użyj stałych, aby podać znaczące nazwy dla specjalnych wartości.
ms.date: 07/20/2015
helpviewer_keywords:
- C# language, constants
- constants [C#]
ms.topic: how-to
ms.custom: contperf-fy21q2
ms.assetid: 43f511be-346c-4b8a-995e-aded94542ece
ms.openlocfilehash: 972deaa4616c15c00e83e26891c4473eae7bfcf8
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2020
ms.locfileid: "97513058"
---
# <a name="how-to-define-constants-in-c"></a>Jak definiować stałe w języku C\#

Stałe są polami, których wartości są ustawiane w czasie kompilacji i nigdy nie mogą być zmieniane. Użyj stałych, aby podać znaczące nazwy zamiast literałów liczbowych ("liczby magiczne") dla specjalnych wartości.  
  
> [!NOTE]
> W języku C# dyrektywa preprocesora [#define](../../language-reference/preprocessor-directives/preprocessor-define.md) nie może służyć do definiowania stałych w sposób, który jest zazwyczaj używany w C i C++.  
  
 Aby zdefiniować stałe wartości typów całkowitych ( `int` , `byte` , i tak dalej), użyj typu wyliczeniowego. Aby uzyskać więcej informacji, zobacz [Wyliczenie](../../language-reference/builtin-types/enum.md).  
  
 Aby zdefiniować niecałkowite stałe, jedno podejście polega na pogrupowania ich w pojedynczej klasie statycznej o nazwie `Constants` . To wymaga, aby wszystkie odwołania do stałych były poprzedzone nazwą klasy, jak pokazano w poniższym przykładzie.  
  
## <a name="example"></a>Przykład  

 [!code-csharp[csProgGuideObjects#89](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#89)]  
  
 Użycie kwalifikatora nazwy klasy pomaga upewnić się, że i inne osoby, które używają stałej, wiedzą, że jest stała i nie mogą być modyfikowane.  
  
## <a name="see-also"></a>Zobacz też

- [Klasy i struktury](./index.md)
