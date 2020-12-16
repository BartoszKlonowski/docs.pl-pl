---
ms.openlocfilehash: 53840ddd59ae3463bae2930fd0151ab2cd2d65cb
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/16/2020
ms.locfileid: "97593331"
---
### <a name="design-time-builds-only-return-top-level-package-references"></a>Kompilacje w czasie projektowania zwracają tylko odwołania do pakietów najwyższego poziomu

W zestaw .NET Core SDK 3.1.400 są zwracane tylko odwołania do pakietów najwyższego poziomu `RunResolvePackageDependencies` .

#### <a name="version-introduced"></a>Wprowadzona wersja

Zestaw .NET Core SDK 3.1.400

#### <a name="change-description"></a>Zmień opis

W poprzednich wersjach zestaw .NET Core SDK `RunResolvePackageDependencies` obiekt docelowy utworzył następujące elementy programu MSBuild, które zawierały informacje z pliku zasobów NuGet:

- `PackageDefinitions`
- `PackageDependencies`
- `TargetDefinitions`
- `FileDefinitions`
- `FileDependencies`

Te dane są używane przez program Visual Studio do wypełniania węzła zależności w Eksplorator rozwiązań. Jednak może to być duża ilość danych, a dane nie są konieczne, chyba że węzeł zależności jest rozwinięty.

Począwszy od zestaw .NET Core SDK w wersji 3.1.400 większość z tych elementów nie jest generowana domyślnie. Zwracane są tylko elementy typu `Package` . Jeśli program Visual Studio potrzebuje elementów do wypełnienia węzła zależności, odczytuje informacje bezpośrednio z pliku Assets.

#### <a name="reason-for-change"></a>Przyczyna zmiany

Ta zmiana została wprowadzona w celu zwiększenia wydajności ładowania rozwiązań w programie Visual Studio. Poprzednio wszystkie odwołania do pakietów zostaną załadowane, co wiąże się z ładowaniem wielu odwołań, które nigdy nie będą wyświetlane dla większości użytkowników.

#### <a name="recommended-action"></a>Zalecana akcja

Jeśli masz logikę programu MSBuild, która zależy od tych elementów, należy ustawić `EmitLegacyAssetsFileItems` Właściwość na `true` w pliku projektu. To ustawienie włącza poprzednie zachowanie w przypadku tworzenia wszystkich elementów.

#### <a name="category"></a>Kategoria

MSBuild

#### <a name="affected-apis"></a>Dotyczy interfejsów API

Nie dotyczy
