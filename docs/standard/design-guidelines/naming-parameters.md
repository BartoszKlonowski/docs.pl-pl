---
title: Nazewnictwo parametrów
description: Poznaj wskazówki dotyczące nazewnictwa parametrów. Na przykład użyj opisowych nazw parametrów & wielkości liter notacji CamelCase, & Rozważ nadanie nazw na podstawie znaczenia zamiast typu.
ms.date: 10/22/2008
helpviewer_keywords:
- parameters, names
- names [.NET Framework], parameters
ms.assetid: ca3c956e-725a-441b-b4e3-eab5d472f41c
ms.openlocfilehash: b62cfbd58f671745054c557041e5d60af345c8d3
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "94820842"
---
# <a name="naming-parameters"></a>Nazewnictwo parametrów
Poza oczywistym powodem czytelności należy postępować zgodnie z wytycznymi dotyczącymi nazw parametrów, ponieważ parametry są wyświetlane w dokumentacji i w projektancie, gdy narzędzia projektowania wizualnego zapewniają funkcje IntelliSense i przeglądanie klas.

 ✔️ używać camelCasing w nazwach parametrów.

 ✔️ należy używać opisowych nazw parametrów.

 ✔️ ROZWAŻYĆ użycie nazw na podstawie znaczenia parametru, a nie typu parametru.

### <a name="naming-operator-overload-parameters"></a>Parametry przeciążenia operatora nazewnictwa
 ✔️ Użyj `left` i `right` dla nazw parametrów przeciążenia operatora binarnego, jeśli nie ma znaczenia dla parametrów.

 ✔️ używać `value` dla jednoargumentowych nazw parametrów przeciążenia, jeśli nie ma znaczenia dla parametrów.

 ✔️ NALEŻY rozważyć znaczące nazwy dla parametrów przeciążenia operatora, jeśli spowoduje to dodanie znaczącej wartości.

 ❌ NIE używaj skrótów ani indeksów liczbowych dla nazw parametrów przeciążenia operatora.

 *Fragmenty © 2005, 2009 Microsoft Corporation. Wszelkie prawa zastrzeżone.*

 *Ponownie Wydrukowano przez uprawnienie Pearson Education, Inc. z [wytycznych dotyczących projektowania platformy: konwencje, idiomy i wzorce dla bibliotek .NET do wielokrotnego użytku, 2. wydanie](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) przez Krzysztof Cwalina i Brad Abrams, opublikowane 22, 2008 przez Addison-Wesley Professional w ramach serii Microsoft Windows Development.*

## <a name="see-also"></a>Zobacz także

- [Wskazówki dotyczące projektowania struktury](index.md)
- [Wskazówki dotyczące nazewnictwa](naming-guidelines.md)
