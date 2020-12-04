---
title: Reguły dotyczące zbędnego kodu
description: Dowiedz się więcej o niepotrzebnych regułach kodu analizy kodu
ms.date: 09/30/2020
ms.topic: reference
author: gewarren
ms.author: gewarren
dev_langs:
- CSharp
- VB
ms.openlocfilehash: 16c4ba0e4bee2388736bf9813a3e8290d8d4da32
ms.sourcegitcommit: 48466b8fb7332ececff5dc388f19f6b3ff503dd4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/05/2020
ms.locfileid: "96589868"
---
# <a name="unnecessary-code-rules"></a>Reguły dotyczące zbędnego kodu

Niepotrzebne reguły kodu identyfikują różne części bazy kodu, które są zbędne i mogą być refaktoryzacjne lub usuwane. Obecność niepotrzebnego kodu wskazuje jeden z następujących problemów:

- Czytelność: kod, który jest niekoniecznie obniżać czytelność. Na przykład flagi [IDE0001](ide0001.md) niepotrzebne kwalifikacje nazw typów.
- Łatwość konserwacji: kod, który nie jest już używany po refaktoryzacji i jest niepotrzebny. Na przykład flagi [IDE0051](ide0051.md) nieużywające prywatnych pól, właściwości, zdarzeń i metod.
- Wydajność: niepotrzebne obliczenie, które nie ma efektów ubocznych i prowadzi do niepotrzebnych obciążeń związanych z wydajnością. Na przykład flagi [IDE0059](ide0059.md) nieużywane przypisania wartości, gdzie wyrażenie służące do obliczania wartości nie ma żadnych efektów ubocznych.
- Funkcja: problem funkcjonalny w kodzie prowadzący do wymaganego kodu, który jest renderowany jako nadmiarowy. Na przykład flagi [IDE0060](ide0060.md) nieużywane parametry, w których Metoda przypadkowo ignoruje parametr wejściowy.

Reguły w tej sekcji dotyczą następujących niepotrzebnych reguł kodu:

- [Uprość nazwę (IDE0001)](ide0001.md)
- [Uprość dostęp do składowych (IDE0002)](ide0002.md)
- [Usuń niepotrzebne rzutowanie (IDE0004)](ide0004.md)
- [Usuń niepotrzebne Importy (IDE0005)](ide0005.md)
- [Usuń nieosiągalny kod (IDE0035)](ide0035.md)
- [Usuń nieużywany prywatny element członkowski (IDE0051)](ide0051.md)
- [Usuń odczytanie prywatnego elementu członkowskiego (IDE0052)](ide0052.md)
- [Usuń nieużywaną wartość wyrażenia (IDE0058)](ide0058.md)
- [Usuń niepotrzebne przypisanie wartości (IDE0059)](ide0059.md)
- [Usuń nieużywany parametr (IDE0060)](ide0060.md)
- [Usuń niepotrzebne pomijanie (IDE0079)](ide0079.md)
- [Usuń niezbędny operator pomijania (IDE0080)](ide0080.md) — tylko język C#.
- [Usuń element "ByVal" (IDE0081)](ide0081.md) — tylko Visual Basic.
- [Usuń niezbędny operator równości (IDE0100)](ide0100.md)
- [Usuń niepotrzebne odrzucanie (IDE0110)](ide0110.md) — tylko w języku C#.

Niektóre z tych reguł mają opcje konfigurowania zachowania reguły:

- [csharp_style_unused_value_expression_statement_preference (IDE0058)](ide0058.md#csharp_style_unused_value_expression_statement_preference)
- [visual_basic_style_unused_value_expression_statement_preference (IDE0058)](ide0058.md#visual_basic_style_unused_value_expression_statement_preference)
- [csharp_style_unused_value_assignment_preference (IDE0059)](ide0059.md#csharp_style_unused_value_assignment_preference)
- [visual_basic_style_unused_value_assignment_preference (IDE0059)](ide0059.md#visual_basic_style_unused_value_assignment_preference)
- [dotnet_code_quality_unused_parameters (IDE0060)](ide0060.md#dotnet_code_quality_unused_parameters)
- [dotnet_remove_unnecessary_suppression_exclusions (IDE0079)](ide0079.md#dotnet_remove_unnecessary_suppression_exclusions)

## <a name="see-also"></a>Zobacz także

- [Reguły języka stylu kodu](language-rules.md)
- [Dokumentacja reguł stylu kodu](index.md)
