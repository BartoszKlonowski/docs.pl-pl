---
title: 'Ograniczenie: weryfikacja schematu XML'
description: Walidacja schematu XSD wykrywa naruszenie ograniczenia UNIQUE w przypadku użycia klucza złożonego, a jeden klucz jest pusty w .NET Framework 4,6.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: b73dd4f4-f2dc-47a2-9425-3896e92321fb
ms.openlocfilehash: 0672361ca5c0bc7cb6ec166f59278b93555e0947
ms.sourcegitcommit: cf5a800a33de64d0aad6d115ffcc935f32375164
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/20/2020
ms.locfileid: "86475310"
---
# <a name="mitigation-xml-schema-validation"></a>Ograniczenie: weryfikacja schematu XML
W .NET Framework 4,6 Walidacja schematu XSD wykrywa naruszenie ograniczenia UNIQUE w przypadku użycia klucza złożonego, a jeden klucz jest pusty.  
  
## <a name="impact"></a>Wpływ  
 Wpływ tej zmiany powinien być minimalny: na podstawie specyfikacji schematu, oczekiwany jest błąd walidacji schematu, jeśli `xsd:unique` jest on naruszany przy użyciu klucza złożonego z pustym kluczem.  
  
## <a name="mitigation"></a>Ograniczanie ryzyka  
 Czy wykryto błąd sprawdzania poprawności schematu, jeśli klucz złożony ma jeden pusty klucz, który jest konfigurowalną funkcją:  
  
- Począwszy od aplikacji przeznaczonych dla .NET Framework 4,6, wykrywanie błędu walidacji schematu jest domyślnie włączone; można jednak zrezygnować z niego, aby błąd sprawdzania poprawności schematu nie zostanie wykryty.  
  
- W aplikacjach uruchamianych w .NET Framework 4,6, ale przeznaczonych dla .NET Framework 4.5.2 i starszych wersji, błąd walidacji schematu nie jest domyślnie wykrywany; możliwe jest jednak, aby to umożliwić, aby wykrycie błędu walidacji schematu.  
  
 Takie zachowanie można skonfigurować przy użyciu <xref:System.AppContext> klasy do definiowania wartości `System.Xml.IgnoreEmptyKeySequences` przełącznika. Ponieważ domyślna wartość przełącznika to `false` (puste sekwencje klawiszy nie są ignorowane), aplikacje przeznaczone dla .NET Framework 4,6 mogą zrezygnować z zachowania przy użyciu następującego kodu, aby ustawić wartość przełącznika na `true` :  
  
 [!code-csharp[AppCompat.IgnoreEmptyKeySequences#1](../../../samples/snippets/csharp/VS_Snippets_CLR/appcompat.ignoreemptykeysequences/cs/program.cs#1)]
 [!code-vb[AppCompat.IgnoreEmptyKeySequences#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/appcompat.ignoreemptykeysequences/vb/module1.vb#1)]  
  
 W przypadku aplikacji, które są przeznaczone dla .NET Framework 4.5.2 i starszych wersji, ponieważ domyślna wartość przełącznika to `true` (puste sekwencje klawiszy są ignorowane), istnieje możliwość zapewnienia, że klucz złożony z pustym kluczem generuje błąd walidacji schematu, używając następującego kodu, aby ustawić wartość przełącznika na `false` .  
  
 [!code-csharp[AppCompat.IgnoreEmptyKeySequences#2](../../../samples/snippets/csharp/VS_Snippets_CLR/appcompat.ignoreemptykeysequences/cs/program.cs#2)]
 [!code-vb[AppCompat.IgnoreEmptyKeySequences#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/appcompat.ignoreemptykeysequences/vb/module1.vb#2)]  
  
## <a name="see-also"></a>Zobacz także

- [Zgodność aplikacji](application-compatibility.md)
