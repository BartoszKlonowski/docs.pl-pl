---
title: 'Istotna zmiana: Environment. OSVersion zwraca poprawną wersję systemu operacyjnego'
description: Dowiedz się więcej na temat istotnej zmiany w programie .NET 5,0 w bibliotekach podstawowych platformy .NET, gdzie Environment. OSVersion zwraca rzeczywistą wersję systemu operacyjnego, a na przykład system operacyjny wybrany do zapewnienia zgodności aplikacji.
ms.date: 11/01/2020
ms.openlocfilehash: c810d9a7a028a0c60c30d69e78a9b9c695d933ef
ms.sourcegitcommit: 81f1bba2c97a67b5ca76bcc57b37333ffca60c7b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/10/2020
ms.locfileid: "97009524"
---
# <a name="environmentosversion-returns-the-correct-operating-system-version"></a>Środowisko. OSVersion zwraca poprawną wersję systemu operacyjnego

<xref:System.Environment.OSVersion?displayProperty=nameWithType> zwraca rzeczywistą wersję systemu operacyjnego (OS) zamiast programu, na przykład systemu operacyjnego wybranego na potrzeby zgodności aplikacji.

## <a name="change-description"></a>Zmień opis

W poprzednich wersjach programu .NET <xref:System.Environment.OSVersion?displayProperty=nameWithType> Funkcja zwraca wersję systemu operacyjnego, która może być niepoprawna, gdy aplikacja działa w trybie zgodności systemu Windows. Aby uzyskać więcej informacji, zobacz [uwagi dotyczące funkcji GetVersionExA](/windows/win32/api/sysinfoapi/nf-sysinfoapi-getversionexa#remarks). W systemie macOS <xref:System.Environment.OSVersion?displayProperty=nameWithType> zwraca podstawową wersję jądra programu Darwin.

Począwszy od platformy .NET 5,0, <xref:System.Environment.OSVersion?displayProperty=nameWithType> zwraca rzeczywistą wersję systemu operacyjnego dla systemu Windows i macOS.

W poniższej tabeli przedstawiono różnice w zachowaniu.

|  | Poprzednie wersje .NET | .NET 5 + |
|--|------------------------|---------|
| Windows | 6.2.9200.0 | 10.0.19042.0 |
| macOS | 19.6.0.0 | 10.15.7 |

## <a name="reason-for-change"></a>Przyczyna zmiany

Użytkownicy tej właściwości oczekują zwrócenia rzeczywistej wersji systemu operacyjnego. Większość aplikacji platformy .NET nie określa ich obsługiwanej wersji w manifeście aplikacji i w ten sposób uzyskuje domyślną obsługiwaną wersję z hosta dotnet. W związku z tym podkładka dotycząca zgodności ma rzadko znaczenie dla aplikacji, która jest uruchomiona. Gdy system Windows zwalnia nową wersję, a starszy Host dotnet jest nadal używany, te aplikacje mogą uzyskać niepoprawną wersję systemu operacyjnego. Zwrócenie rzeczywistej wersji jest bardziej wbudowane z oczekiwaniami deweloperów tego interfejsu API.

Wprowadzenie <xref:System.OperatingSystem.IsWindowsVersionAtLeast%2A?displayProperty=nameWithType> <xref:System.OperatingSystem.IsMacOSVersionAtLeast%2A?displayProperty=nameWithType> programów,, i <xref:System.Runtime.Versioning.SupportedOSPlatformAttribute?displayProperty=nameWithType> w programie .NET 5,0, <xref:System.Environment.OSVersion?displayProperty=nameWithType> zostało zmienione tak, aby były spójne dla systemu Windows i macOS.

## <a name="version-introduced"></a>Wprowadzona wersja

5,0

## <a name="recommended-action"></a>Zalecana akcja

Przejrzyj i przetestuj każdy kod, który używa, <xref:System.Environment.OSVersion?displayProperty=nameWithType> Aby upewnić się, że działa zgodnie z potrzebami.

## <a name="affected-apis"></a>Dotyczy interfejsów API

- <xref:System.Environment.OSVersion?displayProperty=fullName>

<!--

### Category

Core .NET libraries

### Affected APIs

- `P:System.Environment.OSVersion`

-->
