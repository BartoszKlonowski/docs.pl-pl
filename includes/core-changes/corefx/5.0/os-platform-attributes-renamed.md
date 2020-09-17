---
ms.openlocfilehash: 8c739d8f355ffa6a6e09cbe4c531b188acede5bd
ms.sourcegitcommit: fe8877e564deb68d77fa4b79f55584ac8d7e8997
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/17/2020
ms.locfileid: "90720309"
---
### <a name="osplatform-attributes-renamed-or-removed"></a>Atrybuty OSPlatform zostały zmienione lub usunięte

Następujące atrybuty wprowadzone w programie .NET 5,0 Preview 8 zostały usunięte lub zmieniono ich nazwy: `MinimumOSPlatformAttribute` , `RemovedInOSPlatformAttribute` , i `ObsoletedInOSPlatformAttribute` .

#### <a name="change-description"></a>Zmień opis

W programie .NET 5,0 w wersji zapoznawczej 8 wprowadzono następujące atrybuty w <xref:System.Runtime.Versioning> przestrzeni nazw:

- `MinimumOSPlatformAttribute`
- `RemovedInOSPlatformAttribute`
- `ObsoletedInOSPlatformAttribute`

W programie .NET 5,0 w wersji zapoznawczej 8, gdy projekt jest przeznaczony dla programu .NET 5 specyficzny dla systemu operacyjnego, przy użyciu [monikera platformy docelowej](../../../../docs/standard/frameworks.md) , takiej jak `net5.0-windows` , kompilacja dodaje atrybut na poziomie zestawu `System.Runtime.Versioning.MinimumOSPlatformAttribute` .

W programie .NET 5,0 RC1 program `ObsoletedInOSPlatformAttribute` został usunięty i `MinimumOSPlatformAttribute` `RemovedInOSPlatformAttribute` zmieniono jego nazwę w następujący sposób:

| Wersja zapoznawcza 8 | RC1 i nowsze nazwy |
| - | - |
| `MinimumOSPlatformAttribute` | <xref:System.Runtime.Versioning.SupportedOSPlatformAttribute> |
| `RemovedInOSPlatformAttribute` | <xref:System.Runtime.Versioning.UnsupportedOSPlatformAttribute> |

W programie .NET 5,0 w wersji RC1 lub nowszej, gdy projekt jest przeznaczony dla programu .NET 5 specyficzny dla systemu operacyjnego, przy użyciu [monikera platformy docelowej](../../../../docs/standard/frameworks.md) , takiej jak `net5.0-windows` , kompilacja dodaje atrybut na poziomie zestawu <xref:System.Runtime.Versioning.SupportedOSPlatformAttribute> .

#### <a name="reason-for-change"></a>Przyczyna zmiany

Program .NET 5,0 w wersji zapoznawczej 8 wprowadza atrybuty w <xref:System.Runtime.Versioning> celu określenia obsługiwanych platform dla interfejsów API. Atrybuty są używane przez [analizatora zgodności platformy](../../../../docs/core/compatibility/code-analysis.md#ca1416-platform-compatibility) do tworzenia ostrzeżeń kompilacji, gdy interfejsy API specyficzne dla platformy są używane na platformach, które nie obsługują tych interfejsów API.

W przypadku platformy .NET 5,0 RC1 dodano do analizatora zgodności platformy dodatkową funkcję umożliwiającą wykluczenie platformy. Funkcja umożliwia oznaczenie interfejsów API jako całkowicie nieobsługiwanych na platformach systemu operacyjnego. Ta funkcja monituje o wprowadzenie zmian w atrybutach, w tym przy użyciu bardziej odpowiednich nazw. `ObsoletedInOSPlatformAttribute`Zostało usunięte, ponieważ nie było już potrzebne.

#### <a name="version-introduced"></a>Wprowadzona wersja

5,0 RC1

#### <a name="recommended-action"></a>Zalecana akcja

Po przekierowaniu projektu z programu .NET 5,0 w wersji zapoznawczej 8 do programu .NET 5,0 RC1 mogą wystąpić błędy kompilacji lub czasu wykonania z powodu tych zmian. Na przykład zmiana nazwy `MinimumOSPlatformAttribute` może spowodować błędy, ponieważ atrybut jest stosowany do zestawów specyficznych dla platformy w czasie kompilacji, a stare artefakty kompilacji nadal odwołują się do starej nazwy interfejsu API.

Przykładowe błędy czasu kompilacji:

- **błąd CS0246: nie można znaleźć nazwy typu lub przestrzeni nazw "MinimumOSPlatformAttribute" (czy nie brakuje dyrektywy using lub odwołania do zestawu?)**
- **błąd CS0246: nie można znaleźć nazwy typu lub przestrzeni nazw "RemovedInOSPlatformAttribute" (czy nie brakuje dyrektywy using lub odwołania do zestawu?)**
- **błąd CS0246: nie można znaleźć nazwy typu lub przestrzeni nazw "ObsoletedInOSPlatformAttribute" (czy nie brakuje dyrektywy using lub odwołania do zestawu?)**

Przykładowy błąd czasu wykonywania:

**Nieobsługiwany wyjątek. System. TypeLoadException: nie można załadować typu "System. Runtime. Versioning. MinimumOSPlatformAttribute" z zestawu "System. Runtime, Version = 5.0.0.0, Culture = neutral, PublicKeyToken = b03f5f7f11d50a3a".**

Aby rozwiązać te błędy:

- Zaktualizuj wszystkie odwołania `MinimumOSPlatformAttribute` do <xref:System.Runtime.Versioning.SupportedOSPlatformAttribute> .
- Zaktualizuj wszystkie odwołania `RemovedInOSPlatformAttribute` do <xref:System.Runtime.Versioning.UnsupportedOSPlatformAttribute> .
- Usuń wszystkie odwołania do `ObsoletedInOSPlatformAttribute` .
- Skompiluj ponownie projekt (lub wykonaj czyszczenie + kompilację), aby usunąć stare artefakty kompilacji.

#### <a name="category"></a>Kategoria

Podstawowe biblioteki platformy .NET

#### <a name="affected-apis"></a>Dotyczy interfejsów API

- `System.Runtime.Versioning.MinimumOSPlatformAttribute`
- `System.Runtime.Versioning.ObsoletedInOSPlatformAttribute`
- `System.Runtime.Versioning.RemovedInOSPlatformAttribute`

<!--

#### Affected APIs

- `T:System.Runtime.Versioning.MinimumOSPlatformAttribute`
- `T:System.Runtime.Versioning.ObsoletedInOSPlatformAttribute`
- `T:System.Runtime.Versioning.RemovedInOSPlatformAttribute`

-->
