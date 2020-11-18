---
title: Bezpieczeństwo wątków w wyrażeniach regularnych
ms.date: 03/30/2017
helpviewer_keywords:
- .NET regular expressions, threads
- regular expressions, threads
- searching with regular expressions, threads
- parsing text with regular expressions, threads
- pattern-matching with regular expressions, threads
ms.assetid: 7c4a167b-5236-4cde-a2ca-58646230730f
ms.openlocfilehash: 8f4930e0bc1fca51164d1108b169d35c8e73987d
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "94818742"
---
# <a name="thread-safety-in-regular-expressions"></a>Bezpieczeństwo wątków w wyrażeniach regularnych
<xref:System.Text.RegularExpressions.Regex>Sama klasa jest bezpieczna wątkowo i niezmienna (tylko do odczytu). Oznacza to, że obiekty **wyrażenia regularnego** można tworzyć w dowolnym wątku i współdzielonym przez wątki. Metody pasujące mogą być wywoływane z dowolnego wątku i nigdy nie zmieniają żadnego stanu globalnego.  
  
 Jednak obiekty wynikowe (**Match** i **MatchCollection**) zwracane przez **wyrażenie regularne** powinny być używane w pojedynczym wątku. Chociaż wiele z tych obiektów jest logicznie niezmienne, ich implementacje mogą opóźniać Obliczanie niektórych wyników w celu zwiększenia wydajności i w związku z tym wywołujący muszą serializować dostęp do nich.  
  
 Jeśli istnieje potrzeba udostępniania obiektów wynikowych **wyrażeń regularnych** w wielu wątkach, te obiekty mogą być konwertowane na wystąpienia z bezpiecznymi wątkami przez wywołanie ich zsynchronizowanych metod. Z wyjątkiem modułów wyliczających wszystkie klasy wyrażeń regularnych są bezpieczne wątkowo lub mogą być konwertowane na obiekty z bezpiecznymi wątkami przez zsynchronizowaną metodę.  
  
 Numeratory są jedynym wyjątkiem. Aplikacja musi serializować wywołania do modułów wyliczających kolekcje. Zasada polega na tym, że jeśli kolekcja może zostać wyliczona jednocześnie w więcej niż jednym wątku, należy synchronizować metody modułu wyliczającego w obiekcie głównym kolekcji przechodzącej przez moduł wyliczający.  
  
## <a name="see-also"></a>Zobacz także

- [Wyrażenia regularne .NET](regular-expressions.md)
