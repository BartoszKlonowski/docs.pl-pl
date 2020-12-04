---
title: Reguły nazewnictwa (analiza kodu)
description: Poznaj reguły nazewnictwa analizy kodu.
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.namingrules
helpviewer_keywords:
- managed code analysis rules, naming rules
- naming rules
- rules, naming
author: gewarren
ms.author: gewarren
ms.openlocfilehash: 88e7ec6bc1051fa98c46696b2193a5d5912eb111
ms.sourcegitcommit: 2e4adc490c1d2a705a0592b295d606b10b9f51f1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/25/2020
ms.locfileid: "96586957"
---
# <a name="naming-rules"></a>Reguły nazewnictwa

Reguły nazewnictwa obsługują przestrzeganie konwencji nazewnictwa w wytycznych dotyczących projektowania platformy .NET.

## <a name="in-this-section"></a>W tej sekcji

|Reguła|Opis|
|----------|-----------------|
|[CA1700: Nie nadawaj wartościom wyliczeniowym nazwy „Reserved”](ca1700.md)|Ta reguła zakłada, że element członkowski wyliczenia o nazwie, która zawiera „reserved”, nie jest obecnie używany, ale jest symbolem zastępczym do zmiany nazwy lub usunięcia w przyszłej wersji. Zmiana nazwy lub usuwanie członka jest zmianą przerywającą.|
|[CA1707: Identyfikatory nie powinny zawierać znaków podkreślenia](ca1707.md)|Przez konwencję identyfikatory nazw nie zawierają znaku podkreślenia (_). Ta reguła sprawdza przestrzenie nazw, typy, elementy członkowskie i parametry.|
|[CA1708: Identyfikatory powinny różnić się nie tylko wielkością liter](ca1708.md)|Identyfikatory przestrzeni nazw, typów, elementów członkowskich i parametry nie mogą się różnić jedynie wielkością liter, ponieważ języki dla środowiska uruchomieniowego języka wspólnego nie muszą rozróżniać wielkości liter.|
|[CA1710: Identyfikatory powinny mieć poprawny sufiks](ca1710.md)|Według Konwencji nazwy typów, które poszerzają pewne typy podstawowe lub implementują określone interfejsy lub typy pochodzące z tych typów, mają sufiks skojarzony z typem podstawowym lub interfejsem.|
|[CA1711: Identyfikatory nie powinny mieć nieprawidłowych sufiksów](ca1711.md)|Według konwencji nazwy typów, które rozszerzają pewne typy podstawowe lub implementują dane interfejsy lub typy pochodzące z tych typów, powinny kończyć się określonym zarezerwowanym sufiksem. Inne nazwy typów nie powinny używać tych zarezerwowanych sufiksów.|
|[CA1712: Nie dodawaj prefiksu z nazwą typu do wartości wyliczeniowych](ca1712.md)|Nazwy elementów członkowskich wyliczenia nie są poprzedzone nazwą typu, ponieważ oczekuje się, że informacje o typie są udostępniane przez narzędzia deweloperskie.|
|[CA1713: Zdarzenia nie powinny mieć prefiksu „before” ani „after”](ca1713.md)|Nazwa zdarzenia rozpoczyna się od „Before” lub „After”. Nazwa powiązanych zdarzeń, które są wywoływane w określonej kolejności, używa czasu teraźniejszego lub przeszłego, aby wskazać względne położenie akcji w sekwencji.|
|[CA1714: Wyliczenia z atrybutem Flags powinny mieć nazwy w liczbie mnogiej](ca1714.md)|Publiczne Wyliczenie ma atrybut System. FlagsAttribute, a jego nazwa nie kończy się znakiem "s". Typy oznaczone za pomocą FlagsAttribute mają nazwy, które są w liczbie mnogiej, ponieważ atrybut wskazuje, że można określić więcej niż jedną wartość.|
|[CA1715: Identyfikatory powinny mieć poprawny prefiks](ca1715.md)|Nazwa widocznego na zewnątrz interfejsu nie zaczyna się od wielkiej litery "I".  Nazwa parametru typu ogólnego na widocznym zewnętrznie typie lub metodzie nie zaczyna się od wielkiej litery "T".|
|[CA1716: Identyfikatory nie powinny być zgodne ze słowami kluczowymi](ca1716.md)|Przestrzeń nazw lub nazwa typu odpowiada zastrzeżonym słowom kluczowym w języku programowania. Identyfikatory przestrzeni nazw i typów nie powinny być zgodne ze słowami kluczowymi, które są definiowane przez języki dla środowiska uruchomieniowego języka wspólnego.|
|[CA1717: Tylko wyliczenia z atrybutem Flags powinny mieć nazwy w liczbie mnogiej](ca1717.md)|Zgodnie z konwencjami nazewnictwa, nazwa w liczbie mnogiej dla wyliczenia wskazuje, że w tym samym czasie można określić więcej niż jedną wartość wyliczenia.|
|[CA1720: Identyfikatory nie powinny zawierać nazw typów](ca1720.md)|Nazwa parametru w widocznym na zewnątrz elemencie członkowskim zawiera nazwę typu danych lub nazwa widocznego na zewnątrz elementu członkowskiego zawiera specyficzną dla języka nazwę typu danych.|
|[CA1721: Nazwy właściwości nie powinny być takie same jak nazwy metod Get](ca1721.md)|Nazwa publicznego lub chronionego elementu członkowskiego zaczyna się od „Get” i odpowiada nazwie właściwości publicznej lub chronionej. Metody „Get” i właściwości powinny mieć nazwy, które wyraźnie odróżniają ich funkcje.|
|[CA1724: Nazwy typów nie powinny być takie same jak nazwy przestrzeni nazw](ca1724.md)|Nazwy typów nie powinny być zgodne z nazwami przestrzeni nazw platformy .NET. Naruszenie tej reguły może zmniejszyć użyteczność biblioteki.|
|[CA1725: Nazwy parametrów powinny być zgodne z deklaracją podstawową](ca1725.md)|Spójne nazywanie parametrów w zastąpieniu hierarchii zwiększa użyteczność zastąpienia metody. Jeśli nazwa parametru w metodzie pochodnej różni się od nazwy podstawowej deklaracji, może nie być jasne, czy metoda jest zastąpieniem metody podstawowej, czy też nowym przeciążeniem metody.|
