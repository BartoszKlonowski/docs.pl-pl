---
title: Reguły globalizacji (analiza kodu)
description: Poznaj reguły globalizacji reguł analizy kodu
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.globalizationrules
helpviewer_keywords:
- rules, globalization
- globalization rules
- globalization [Visual Studio], rules
- managed code analysis rules, globalization rules
author: gewarren
ms.author: gewarren
ms.openlocfilehash: 83ecc52c5e20e074c6c1aed68204a574494f42d5
ms.sourcegitcommit: 2e4adc490c1d2a705a0592b295d606b10b9f51f1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/25/2020
ms.locfileid: "96589260"
---
# <a name="globalization-rules"></a>Reguły globalizacji

Reguły globalizacji obsługują biblioteki i aplikacje gotowe do zastosowania na całym świecie.

## <a name="in-this-section"></a>W tej sekcji

|Reguła|Opis|
|----------|-----------------|
|[CA1303: Nie przekazuj literałów jako zlokalizowanych parametrów](ca1303.md)|Metoda widoczna na zewnątrz przekazuje literał ciągu jako parametr do konstruktora lub metody .NET, a ten ciąg powinien być Lokalizowalny.|
|[CA1304: Określ argument CultureInfo](ca1304.md)|Metoda lub konstruktor wywołuje członka mającego przeciążenie, które akceptuje parametr System.Globalization.CultureInfo i metodę lub konstruktor niewywołujący przeciążenia, które wymaga parametru CultureInfo. Kiedy obiekt CultureInfo lub System.IFormatProvider nie jest podany, domyślna wartość, która jest dostarczana przez członka przeciążonego, może nie wywoływać oczekiwanego efektu we wszystkich ustawieniach regionalnych.|
|[CA1305: Określ argument IFormatProvider](ca1305.md)|Metoda lub konstruktor wywołują jednego lub kilku członków, którzy mają przeciążenia akceptujące parametr System.IFormatProvider, i metody lub konstruktora, który nie wywołuje przeciążenia przyjmującego parametr IFormatProvider. Kiedy obiekt System.Globalization.CultureInfo lub IFormatProvider nie jest podany, domyślna wartość przekazywana przez członka przeciążonego może nie wywoływać oczekiwanego efektu we wszystkich ustawieniach regionalnych.|
|[CA1307: Określ parametr StringComparison w celu zapewnienia jednoznaczności](ca1307.md)|Operacja porównania ciągu używa przeciążenia metody, które nie ustawia parametru StringComparison.|
|[CA1308: Normalizuj ciągi do postaci zapisanej wielkimi literami](ca1308.md)|Ciągi powinny być znormalizowane do użycia wielkich liter. Małe grupy znaków nie mogą wykonywać rund, gdy są one konwertowane na małe litery.|
|[CA1309: Użyj porządkowego ustawienia właściwości StringComparison](ca1309.md)|Operacja porównania ciągu, która jest nielingwistyczna, nie ustawia parametru StringComparison na Ordinal lub OrdinalIgnoreCase. Poprzez jawne ustawienie parametru na StringComparison.Ordinal lub StringComparison.OrdinalIgnoreCase kod często zaczyna działać szybciej, staje się bardziej poprawny i niezawodny.|
|[CA1310: Określ parametr StringComparison w celu zapewnienia poprawności](ca1310.md)|Operacja porównywania ciągów używa przeciążenia metody, które nie ustawia parametru StringComparison i domyślnie używa porównania ciągów specyficznych dla kultury.|
|[CA2101: Określ kierowanie dla argumentów ciągu P/Invoke](ca2101.md)|Element członkowski wywołania platformy zezwala na częściowo zaufane obiekty wywołujące, ma parametr String i nie jest jawnie zorganizowany przez ciąg. Może to spowodować potencjalne luki w zabezpieczeniach.|
