---
title: Ostrzeżenie SYSLIB0011
description: Dowiedz się więcej o Obsoletions, które generują ostrzeżenie SYSLIB0011 w czasie kompilacji.
ms.topic: reference
ms.date: 10/20/2020
ms.openlocfilehash: 36292cc5314e2b7677d705780880b7e25ae0dfb6
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/16/2020
ms.locfileid: "97596579"
---
# <a name="syslib0011-binaryformatter-serialization-is-obsolete"></a>SYSLIB0011: serializacja BinaryFormatter jest przestarzała

Ze względu na [luki w zabezpieczeniach](../../../standard/serialization/binaryformatter-security-guide.md#binaryformatter-security-vulnerabilities) <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> następujące interfejsy API są oznaczane jako przestarzałe, począwszy od platformy .NET 5,0. Użycie ich w kodzie generuje ostrzeżenie `SYSLIB0011` w czasie kompilacji.

- <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Serialize%2A?displayProperty=nameWithType>
- <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Deserialize%2A?displayProperty=nameWithType>
- <xref:System.Runtime.Serialization.Formatter.Serialize(System.IO.Stream,System.Object)?displayProperty=nameWithType>
- <xref:System.Runtime.Serialization.Formatter.Deserialize(System.IO.Stream)?displayProperty=nameWithType>
- <xref:System.Runtime.Serialization.IFormatter.Serialize(System.IO.Stream,System.Object)?displayProperty=nameWithType>
- <xref:System.Runtime.Serialization.IFormatter.Deserialize(System.IO.Stream)?displayProperty=nameWithType>

## <a name="workarounds"></a>Obejścia

Rozważ użycie <xref:System.Text.Json.JsonSerializer> lub <xref:System.Xml.Serialization.XmlSerializer> zamiast <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> .

Aby uzyskać więcej informacji na temat zalecanych akcji, zobacz [Rozwiązywanie problemów z BinaryFormatter obsoletion i wyłączanie](https://aka.ms/binaryformatter).

[!INCLUDE [suppress-syslib-warning](../../../../includes/suppress-syslib-warning.md)]

## <a name="see-also"></a>Zobacz także

- [Rozwiązywanie błędów BinaryFormatter i wyłączania](https://aka.ms/binaryformatter)
- [Metody serializacji BinaryFormatter są przestarzałe i zabronione w aplikacjach ASP.NET](../core-libraries/5.0/binaryformatter-serialization-obsolete.md)
