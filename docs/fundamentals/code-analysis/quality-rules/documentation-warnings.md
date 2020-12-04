---
title: Reguły dokumentacji (analiza kodu)
description: Poznaj reguły dokumentacji dotyczącej reguł analizy kodu
ms.date: 09/16/2019
ms.topic: reference
f1_keywords:
- vs.codeanalysis.documentationrules
helpviewer_keywords:
- documentation rules
- managed code analysis rules, documentation rules
- warnings, documentation
author: mavasani
ms.author: mavasani
ms.openlocfilehash: 29d1734eec29bd00d456b4b00c48c2e8ef223441
ms.sourcegitcommit: 2e4adc490c1d2a705a0592b295d606b10b9f51f1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/25/2020
ms.locfileid: "96587220"
---
# <a name="documentation-rules"></a>Reguły dokumentacji

Reguły dokumentacji obsługują pisanie dobrze udokumentowanych bibliotek poprzez poprawne użycie [komentarzy dokumentacji XML](../../../csharp/codedoc.md) dla widocznych na zewnątrz interfejsów API.

## <a name="in-this-section"></a>W tej sekcji

| Reguła | Opis |
| - | - |
| [CA1200: Unikaj używania tagów cref z prefiksem](ca1200.md) | Atrybut [cref](../../../csharp/programming-guide/xmldoc/cref-attribute.md) w tagu dokumentacji XML oznacza "odwołanie do kodu". Określa, że wewnętrznym tekstem znacznika jest element kodu, taki jak typ, metoda lub właściwość. Należy unikać używania `cref` tagów z prefiksami, ponieważ uniemożliwia kompilatorowi Weryfikowanie odwołań. Uniemożliwia również znajdowanie i aktualizowanie tych odwołań do tych symboli podczas refaktoryzacji przez program Visual Studio Integrated Development Environment (IDE). |
