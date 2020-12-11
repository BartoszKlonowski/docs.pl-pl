---
title: Jak obsłużyć wyjątek przy użyciu przewodnika programowania try-catch-C#
description: Dowiedz się, jak obsłużyć wyjątek przy użyciu bloku try-catch. Zobacz przykładowy kod i Wyświetl dodatkowe dostępne zasoby.
ms.date: 12/09/2020
helpviewer_keywords:
- exception handling [C#], try/catch blocks
- exceptions [C#], try/catch blocks
- try/catch blocks [C#]
ms.assetid: ca8e3773-980e-4767-8633-7408540e9818
ms.openlocfilehash: b6368660dbe037123f5bb6ce52502d4a94fcfc3a
ms.sourcegitcommit: 9b877e160c326577e8aa5ead22a937110d80fa44
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2020
ms.locfileid: "97110523"
---
# <a name="how-to-handle-an-exception-using-trycatch-c-programming-guide"></a>Jak obsłużyć wyjątek przy użyciu try/catch (Przewodnik programowania w języku C#)

Celem bloku [try-catch](../../language-reference/keywords/try-catch.md) jest przechwycenie i obsłużenie wyjątku wygenerowanego przez kod roboczy. Niektóre wyjątki mogą być obsługiwane w `catch` bloku i problem został rozwiązany bez zgłaszania wyjątku, jednak częściej, którą można wykonać, jest upewnienie się, że jest zgłaszany odpowiedni wyjątek.

## <a name="example"></a>Przykład

W tym przykładzie <xref:System.IndexOutOfRangeException> nie jest to najbardziej odpowiedni wyjątek: jest to <xref:System.ArgumentOutOfRangeException> bardziej zrozumiałe dla metody, ponieważ błąd jest spowodowany przez argument, który `index` przeszedł przez wywołującego.

:::code language="csharp" source="snippets/exceptions/ExampleTryCatch.cs" id="ExampleTryCatch":::

## <a name="comments"></a>Komentarze

Kod, który powoduje, że wyjątek jest ujęty w `try` bloku. `catch`Instrukcja jest dodawana natychmiast po do dojścia `IndexOutOfRangeException` , jeśli wystąpi. `catch`Blok obsługuje `IndexOutOfRangeException` i zgłasza `ArgumentOutOfRangeException` zamiast niego bardziej odpowiedni wyjątek. Aby zapewnić wywołującemu możliwie jak najwięcej informacji, rozważ określenie oryginalnego wyjątku jako <xref:System.Exception.InnerException%2A> nowego wyjątku. Ponieważ <xref:System.Exception.InnerException%2A> Właściwość jest [tylko do odczytu](../../properties.md#read-only), należy przypisać ją w konstruktorze nowego wyjątku.
