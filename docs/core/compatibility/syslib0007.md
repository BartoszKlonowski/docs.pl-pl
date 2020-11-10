---
title: Ostrzeżenie SYSLIB0007
description: Dowiedz się więcej o Obsoletions, które generują ostrzeżenie SYSLIB0007 w czasie kompilacji.
ms.topic: reference
ms.date: 10/20/2020
ms.openlocfilehash: 4c0feac1d673e3462a4f2db470825b15cf1b1706
ms.sourcegitcommit: 30a686fd4377fe6472aa04e215c0de711bc1c322
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/10/2020
ms.locfileid: "94439945"
---
# <a name="syslib0007-default-implementations-of-cryptography-algorithms-not-supported"></a>SYSLIB0007: domyślne implementacje algorytmów kryptograficznych nie są obsługiwane

System konfiguracji kryptograficznej w .NET Framework nie pozwala na prawidłową elastyczność kryptograficzną i nie jest obecny w oprogramowaniu .NET Core i .NET 5 +. . Wymagania dotyczące zgodności z poprzednimi wersjami w sieci również uniemożliwiają platformie aktualizowanie niektórych kryptograficznych interfejsów API, aby zachować z wyprzedzeniem kryptografii. W związku z tym następujące interfejsy API są oznaczone jako przestarzałe, począwszy od platformy .NET 5,0. Użycie tych interfejsów API generuje ostrzeżenie `SYSLIB0007` w czasie kompilacji.

- <xref:System.Security.Cryptography.AsymmetricAlgorithm.Create?displayProperty=fullName>
- <xref:System.Security.Cryptography.HashAlgorithm.Create?displayProperty=fullName>
- <xref:System.Security.Cryptography.HMAC.Create?displayProperty=fullName>
- <xref:System.Security.Cryptography.KeyedHashAlgorithm.Create?displayProperty=fullName>
- <xref:System.Security.Cryptography.SymmetricAlgorithm.Create?displayProperty=fullName>

## <a name="workarounds"></a>Obejścia

- Zalecanym sposobem działania jest zastępowanie wywołań teraz przestarzałych interfejsów API z wywołaniami metod fabrycznych dla określonych algorytmów, na przykład <xref:System.Security.Cryptography.Aes.Create?displayProperty=nameWithType> . Zapewnia to pełną kontrolę nad tym, które algorytmy są tworzone.

- Jeśli chcesz zachować zgodność z istniejącymi ładunkiem wygenerowanymi przez .NET Framework aplikacje, które używają teraz przestarzałych interfejsów API, użyj zamienników sugerowanych w poniższej tabeli. Tabela zawiera mapowanie od .NET Framework domyślnych algorytmów do ich odpowiedników w architekturze .NET 5 i.

  | .NET Framework | Zastępowanie zgodne z platformą .NET Core/.NET 5.0 | Uwagi |
  | - | - | - |
  | <xref:System.Security.Cryptography.AsymmetricAlgorithm.Create?displayProperty=nameWithType> | <xref:System.Security.Cryptography.RSA.Create?displayProperty=nameWithType> | |
  | <xref:System.Security.Cryptography.HashAlgorithm.Create?displayProperty=nameWithType> | <xref:System.Security.Cryptography.SHA1.Create?displayProperty=nameWithType> | Algorytm SHA-1 jest uznawany za przerwany. Rozważ użycie silniejszego algorytmu, jeśli jest to możliwe. Aby uzyskać dalsze wskazówki, zapoznaj się z doradcą zabezpieczeń. |
  | <xref:System.Security.Cryptography.HMAC.Create?displayProperty=nameWithType> | <xref:System.Security.Cryptography.HMACSHA1.%23ctor> | Algorytm HMACSHA1 nie jest odradzany w przypadku większości nowoczesnych aplikacji. Rozważ użycie silniejszego algorytmu, jeśli jest to możliwe. Aby uzyskać dalsze wskazówki, zapoznaj się z doradcą zabezpieczeń. |
  | <xref:System.Security.Cryptography.KeyedHashAlgorithm.Create?displayProperty=nameWithType> | <xref:System.Security.Cryptography.HMACSHA1.%23ctor> | Algorytm HMACSHA1 nie jest odradzany w przypadku większości nowoczesnych aplikacji. Rozważ użycie silniejszego algorytmu, jeśli jest to możliwe. Aby uzyskać dalsze wskazówki, zapoznaj się z doradcą zabezpieczeń. |
  | <xref:System.Security.Cryptography.SymmetricAlgorithm.Create?displayProperty=nameWithType> | <xref:System.Security.Cryptography.Aes.Create?displayProperty=nameWithType> |

[!INCLUDE [suppress-syslib-warning](../../../includes/suppress-syslib-warning.md)]

## <a name="see-also"></a>Zobacz też

- [Krytyczne zmiany kryptografii](cryptography.md#instantiating-default-implementations-of-cryptographic-abstractions-is-not-supported)
