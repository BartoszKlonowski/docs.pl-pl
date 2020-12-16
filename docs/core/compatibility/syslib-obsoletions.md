---
title: Przestarzałe funkcje w programie .NET 5 lub nowszym
description: Dowiedz się więcej na temat interfejsów API, które są oznaczone jako przestarzałe w programie .NET 5,0 i nowszych wersjach, które generują ostrzeżenia kompilatora SYSLIB.
ms.date: 10/20/2020
ms.openlocfilehash: 336958c93e3db8f66cfbec89476a666e5e103b70
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/16/2020
ms.locfileid: "97593308"
---
# <a name="obsolete-features-in-net-5"></a>Przestarzałe funkcje w programie .NET 5

Począwszy od platformy .NET 5,0, niektóre interfejsy API, które są nowo oznaczone jako przestarzałe, używają dwóch nowych właściwości w programie <xref:System.ObsoleteAttribute> .

- <xref:System.ObsoleteAttribute.DiagnosticId?displayProperty=nameWithType>Właściwość nakazuje kompilatorowi generowanie ostrzeżeń kompilacji przy użyciu NIESTANDARDOWEGO identyfikatora diagnostyki. Identyfikator niestandardowy pozwala na Pomijanie ostrzeżenia obsoletion, w odniesieniu do siebie i niezależnie od siebie. W przypadku platformy .NET 5 i Obsoletions format niestandardowego identyfikatora diagnostyki to `SYSLIBxxxx` .

- <xref:System.ObsoleteAttribute.UrlFormat?displayProperty=nameWithType>Właściwość nakazuje kompilatorowi dołączenie linku adresu URL, aby dowiedzieć się więcej na temat obsoletion.

Jeśli występują ostrzeżenia lub błędy kompilacji z powodu użycia przestarzałego interfejsu API, postępuj zgodnie ze szczegółowymi wskazówkami dotyczącymi identyfikatora diagnostyki wymienionymi w sekcji [Reference](#reference) . *Nie* można pominąć ostrzeżeń ani błędów dla tych Obsoletions przy użyciu [standardowego identyfikatora diagnostyki (CS0618)](../../csharp/language-reference/compiler-messages/cs0618.md) dla przestarzałych typów lub członków; `SYSLIBxxxx`zamiast tego użyj niestandardowych identyfikatorów diagnostyki. Aby uzyskać więcej informacji, zobacz [pomijanie ostrzeżeń](#suppress-warnings).

## <a name="reference"></a>Dokumentacja

Poniższa tabela zawiera indeks `SYSLIBxxxx` Obsoletions w programie .NET 5 lub nowszym.

| Identyfikator diagnostyki | Opis |
| - | - |
| [SYSLIB0001](syslib-warnings/syslib0001.md) | Kodowanie UTF-7 jest niezabezpieczone i nie powinno być używane. Zamiast tego należy rozważyć użycie UTF-8. |
| [SYSLIB0002](syslib-warnings/syslib0002.md) | <xref:System.Security.Permissions.PrincipalPermissionAttribute> nie jest uznawany przez środowisko uruchomieniowe i nie może być używany. |
| [SYSLIB0003](syslib-warnings/syslib0003.md) | Zabezpieczenia dostępu kodu (CAS) nie są obsługiwane ani honorowane przez środowisko uruchomieniowe. |
| [SYSLIB0004](syslib-warnings/syslib0004.md) | Funkcja ograniczonego regionu wykonywania (CER) nie jest obsługiwana. |
| [SYSLIB0005](syslib-warnings/syslib0005.md) | Globalna pamięć podręczna zestawów (GAC) nie jest obsługiwana. |
| [SYSLIB0006](syslib-warnings/syslib0006.md) | <xref:System.Threading.Thread.Abort?displayProperty=nameWithType> nie jest obsługiwane i zgłasza <xref:System.PlatformNotSupportedException> . |
| [SYSLIB0007](syslib-warnings/syslib0007.md) | Domyślna implementacja tego algorytmu kryptografii nie jest obsługiwana. |
| [SYSLIB0008](syslib-warnings/syslib0008.md) | <xref:System.Runtime.CompilerServices.DebugInfoGenerator.CreatePdbGenerator>Interfejs API nie jest obsługiwany i zgłasza <xref:System.PlatformNotSupportedException> . |
| [SYSLIB0009](syslib-warnings/syslib0009.md) | <xref:System.Net.AuthenticationManager.Authenticate%2A?displayProperty=nameWithType>Metody i <xref:System.Net.AuthenticationManager.PreAuthenticate%2A?displayProperty=nameWithType> nie są obsługiwane i throw <xref:System.PlatformNotSupportedException> . |
| [SYSLIB0010](syslib-warnings/syslib0010.md) | Niektóre interfejsy API komunikacji zdalnej nie są obsługiwane i throw <xref:System.PlatformNotSupportedException> . |
| [SYSLIB0011](syslib-warnings/syslib0011.md) | <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> Serializacja jest przestarzała i nie powinna być używana. |
| [SYSLIB0012](syslib-warnings/syslib0012.md) | <xref:System.Reflection.Assembly.CodeBase?displayProperty=nameWithType> i <xref:System.Reflection.Assembly.EscapedCodeBase?displayProperty=nameWithType> są dołączone tylko do .NET Framework zgodności. Zamiast tego użyj polecenia cmdlet <xref:System.Reflection.Assembly.Location?displayProperty=nameWithType>. |

## <a name="suppress-warnings"></a>Pomijanie ostrzeżeń

Jeśli musisz użyć przestarzałych interfejsów API, a `SYSLIBxxxx` Diagnostyka nie jest powierzchnią jako błąd, możesz pominąć ostrzeżenie w kodzie lub w pliku projektu.

W kodzie:

```csharp
// Disable the warning.
#pragma warning disable SYSLIB0001
// Code that uses obsolete API.
...
// Re-enable the warning.
#pragma warning restore SYSLIB0001
```

Plik projektu:

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
   <TargetFramework>net5.0</TargetFramework>
   <!-- NoWarn below suppresses SYSLIB0001 project-wide -->
   <NoWarn>$(NoWarn);SYSLIB0001</NoWarn>
   <!-- To suppress multiple warnings, you can use multiple NoWarn elements -->
   <NoWarn>$(NoWarn);SYSLIB0002</NoWarn>
   <NoWarn>$(NoWarn);SYSLIB0003</NoWarn>
   <!-- Alternatively, you can suppress multiple warnings by using a semicolon-delimited list -->
   <NoWarn>$(NoWarn);SYSLIB0001;SYSLIB0002;SYSLIB0003</NoWarn>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> Pomijanie ostrzeżeń w ten sposób powoduje wyłączenie wyłącznie określonych ostrzeżeń obsoletion. Nie wyłącza żadnych innych ostrzeżeń, w tym ostrzeżeń obsoletion z różnymi identyfikatorami diagnostycznymi.
