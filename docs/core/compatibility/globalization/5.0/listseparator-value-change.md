---
title: 'Zmiana podziału: TextInfo. ListSeparator — zmiana wartości'
description: Dowiedz się więcej o różnicach w programie .NET 5,0, gdzie wartość domyślna TextInfo. ListSeparator została zmieniona między wersjami 5,0 i 5.0.1.
ms.date: 12/10/2020
ms.openlocfilehash: 720d46c1908bcd70812f575a90f580470dbc7f32
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/16/2020
ms.locfileid: "97596610"
---
# <a name="textinfolistseparator-values-changed"></a>Zmieniono wartości TextInfo. ListSeparator

Wartości domyślne <xref:System.Globalization.TextInfo.ListSeparator?displayProperty=nameWithType> dla różnych kultur zostały zmienione we wszystkich systemach operacyjnych.

## <a name="change-description"></a>Zmień opis

W programie .NET 5.0.0 jako część [przełącznika z BIBLIOTEK NLS do ICU](icu-globalization-api.md), <xref:System.Globalization.TextInfo.ListSeparator?displayProperty=nameWithType> wartości domyślne dla różnych kultur uległy zmianie w systemie Windows. Wartości separatora dziesiętnego uzyskane ze składników międzynarodowych dla standardu Unicode (ICU) zostały użyte jako <xref:System.Globalization.TextInfo.ListSeparator> wartości. W systemie Linux i macOS nie wprowadzono zmian w <xref:System.Globalization.TextInfo.ListSeparator?displayProperty=nameWithType> wartościach. oznacza to, że nadal używają wartości separatora dziesiętnego.

Dla wszystkich systemów operacyjnych w .NET 5.0.1 i nowszych wersjach wartości dla <xref:System.Globalization.TextInfo.ListSeparator?displayProperty=nameWithType> są równoważne wartościom, które byłyby uzyskane z NLS. W przypadku systemu Windows oznacza to, że wartości są równoważne .NET Framework i .NET Core 1,0-3,1. W przypadku systemów Linux i macOS <xref:System.Globalization.TextInfo.ListSeparator?displayProperty=nameWithType> wartości są teraz zgodne z <xref:System.Globalization.TextInfo.ListSeparator?displayProperty=nameWithType> wartościami dla systemu Windows.

Poniższa tabela zawiera podsumowanie zmian <xref:System.Globalization.TextInfo.ListSeparator?displayProperty=nameWithType> wartości.

| | .NET Framework<br/>.NET Core 1,0 — 3,1 | .NET 5.0 | 5.0.1 .NET |
-|-|-|-
| **Windows** | Uzyskaj z usługi NLS | Separator dziesiętny z ICU.<br/>Można wrócić do lokalizacji sieciowej. | Równoważne z usługą NLS |
| **Linux i macOS** | Separator dziesiętny z ICU | Separator dziesiętny z ICU | Równoważne z usługą NLS |

## <a name="version-introduced"></a>Wprowadzona wersja

5.0.1

## <a name="reason-for-change"></a>Przyczyna zmiany

Deweloperzy zgłosili, że używają <xref:System.Globalization.TextInfo.ListSeparator?displayProperty=nameWithType> właściwości podczas analizowania plików wartości rozdzielanych przecinkami (CSV), a nowe wartości rozstają <xref:System.Globalization.TextInfo.ListSeparator?displayProperty=nameWithType> się nimi.

## <a name="recommended-action"></a>Zalecana akcja

Jeśli kod opiera się na poprzednich wartościach separatora dziesiętnego, można umieszczaj wymagane <xref:System.Globalization.TextInfo.ListSeparator?displayProperty=nameWithType> wartości.

## <a name="affected-apis"></a>Dotyczy interfejsów API

- <xref:System.Globalization.TextInfo.ListSeparator?displayProperty=fullName>

<!--

#### Category

- Globalization

### Affected APIs

- `P:System.Globalization.TextInfo.ListSeparator`

-->
