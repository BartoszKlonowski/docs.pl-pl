---
title: Jak są używane wersje środowiska uruchomieniowego .NET i zestawu SDK
description: W tym artykule wyjaśniono, jak są używane wersje zestawu .NET SDK i środowiska uruchomieniowego (podobnie jak w przypadku wersji semantycznej).
ms.date: 12/07/2020
ms.openlocfilehash: 2fbc2775f31b4eab1c9883282c58accd9bb2b9f5
ms.sourcegitcommit: 635a0ff775d2447a81ef7233a599b8f88b162e5d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/17/2020
ms.locfileid: "97633627"
---
# <a name="overview-of-how-net-is-versioned"></a>Omówienie wersji platformy .NET

[Środowisko uruchomieniowe platformy .NET i zestaw SDK platformy .NET](../introduction.md#sdk-and-runtimes) dodają nowe funkcje przy użyciu różnych częstotliwości. Ogólnie rzecz biorąc, zestaw SDK jest aktualizowany częściej niż środowisko uruchomieniowe. W tym artykule opisano środowisko uruchomieniowe i numery wersji zestawu SDK.

## <a name="versioning-details"></a>Szczegóły dotyczące wersji

Środowisko uruchomieniowe platformy .NET ma rozwiązane główne/drobne/poprawka do wersji, która następuje po [wersji semantycznej](#semantic-versioning).

Zestaw SDK platformy .NET nie jest zgodny z wersją semantyczną. Zestaw SDK platformy .NET jest szybszy, a jego numery wersji muszą komunikować się z wyrównanym środowiskiem uruchomieniowym i wersjami pomocniczymi i poprawkami zestawu SDK.

Pierwsze dwa pozycje numeru wersji zestawu .NET SDK są blokowane w wersji środowiska uruchomieniowego .NET wydanej w programie. Każda wersja zestawu SDK może tworzyć aplikacje dla tego środowiska uruchomieniowego lub dowolnej niższej wersji.

Trzecia pozycja numeru wersji zestawu SDK komunikuje się zarówno z literą, jak i numerem poprawki. Wersja pomocnicza jest mnożona przez 100. Ostatnie dwie cyfry reprezentują numer poprawki. Wersja pomocnicza 1, Poprawka wersja 2 byłaby reprezentowana jako 102. Na przykład Oto możliwa sekwencja numerów wersji środowiska uruchomieniowego i zestawu SDK:

| Zmiana                | Środowisko uruchomieniowe platformy .NET      | zestaw SDK platformy .NET ( \* )     |
|-----------------------|-------------------|-------------------|
| Wersja początkowa       | 2.2.0             | 2.2.100           |
| Poprawka zestawu SDK             | 2.2.0             | 2.2.101           |
| Środowisko uruchomieniowe i poprawka zestawu SDK | 2.2.1             | 2.2.102           |
| Zmiana funkcji zestawu SDK    | 2.2.1             | 2.2.200           |

O

- Jeśli zestaw SDK ma 10 aktualizacji funkcji przed aktualizacją funkcji środowiska uruchomieniowego, numery wersji są przydzielone do serii 1000 z liczbami takimi jak 2.2.1000 jako wersja funkcji po 2.2.900. Ta sytuacja nie powinna wystąpić.
- 99 wersje poprawek bez wydania funkcji nie zostaną wykonane. Jeśli wersja zbliża się do tej liczby, wymusza wydanie funkcji.

Więcej szczegółów można znaleźć w wstępnej propozycji w repozytorium [dotnet/Designing](https://github.com/dotnet/designs/pull/29) .

## <a name="semantic-versioning"></a>Semantyczna obsługa wersji

*Środowisko uruchomieniowe* platformy .NET jest ściśle zgodne z [wersją semantyki (SemVer)](https://semver.org/), `MAJOR.MINOR.PATCH` przy użyciu różnych części numeru wersji do opisania stopnia i typu zmiany.

```
MAJOR.MINOR.PATCH[-PRERELEASE-BUILDNUMBER]
```

Opcjonalne `PRERELEASE` i `BUILDNUMBER` części nie są nigdy częścią obsługiwanych wersji i istnieją tylko w przypadku nocnych kompilacji, lokalne kompilacje ze źródłowych elementów docelowych i nieobsługiwane wersje wersji zapoznawczej.

### <a name="understand-runtime-version-number-changes"></a>Informacje o zmianach numeru wersji środowiska uruchomieniowego

`MAJOR` jest zwiększana, gdy:

- Wprowadzono znaczące zmiany w produkcie lub nowy kierunek produktu.
- Wprowadzono istotne zmiany. Istnieje wysoki poziom akceptowania istotnych zmian.
- Stara wersja nie jest już obsługiwana.
- `MAJOR`Przyjęto nowszą wersję istniejącej zależności.

`MINOR` jest zwiększana, gdy:

- Dodano publiczny obszar powierzchni interfejsu API.
- Zostanie dodane nowe zachowanie.
- `MINOR`Przyjęto nowszą wersję istniejącej zależności.
- Zostanie wprowadzona nowa zależność.

`PATCH` jest zwiększana, gdy:

- Wprowadzono poprawki błędów.
- Dodano obsługę nowszej platformy.
- `PATCH`Przyjęto nowszą wersję istniejącej zależności.
- Jakakolwiek inna zmiana nie pasuje do jednego z poprzednich przypadków.

W przypadku zmiany wielu zmian najwyższy element, na który wpływają poszczególne zmiany, jest zwiększany, a następujące są resetowane do zera. Na przykład gdy `MAJOR` jest zwiększana, `MINOR` i `PATCH` są resetowane do zera. Gdy `MINOR` jest zwiększana, `PATCH` jest resetowana do zera, podczas gdy pozostaje `MAJOR` nienaruszony.

## <a name="version-numbers-in-file-names"></a>Numery wersji w nazwach plików

Pliki pobrane dla platformy .NET przenoszą wersję, na przykład `dotnet-sdk-2.1.300-win10-x64.exe` .

### <a name="preview-versions"></a>Wersje zapoznawcze

Wersja zapoznawcza ma `-preview[number]-([build]|"final")` dołączony numer wersji. Na przykład `2.0.0-preview1-final`.

### <a name="servicing-versions"></a>Wersje obsługi

Po wyjściu z wersji, gałęzie wydań zwykle zatrzymują codzienne kompilacje i zamiast tego uruchamiają kompilacje obsługi. Wersje obsługujące zostały `-servicing-[number]` dołączone do wersji. Na przykład `2.0.1-servicing-006924`.

## <a name="relationship-to-net-standard-versions"></a>Relacja z wersjami .NET Standard

.NET Standard składa się z zestawu odwołań platformy .NET. Istnieje wiele implementacji specyficznych dla każdej platformy. Zestaw odwołań zawiera definicję interfejsów API platformy .NET, które są częścią danej .NET Standard wersji. Każda implementacja spełnia umowę .NET Standard na określonej platformie.

Zestaw odwołań .NET Standard używa `MAJOR.MINOR` schematu przechowywania wersji. `PATCH` poziom nie jest użyteczny w przypadku .NET Standard, ponieważ uwidacznia tylko specyfikację interfejsu API (bez implementacji) i według definicji jakakolwiek zmiana w interfejsie API będzie reprezentować zmianę zestawu funkcji i w związku z tym nową `MINOR` wersją.

Implementacje na każdej platformie mogą być aktualizowane, zazwyczaj jako część wersji platformy, i nie są widoczne dla programistów używających .NET Standard na tej platformie.

Aby uzyskać więcej informacji, zobacz [.NET Standard](../../standard/net-standard.md).

## <a name="see-also"></a>Zobacz także

- [Platformy docelowe](../../standard/frameworks.md)
- [Pakowanie dystrybucji .NET](../distribution-packaging.md)
- [Arkusz faktów pomocy technicznej dla platformy .NET](https://dotnet.microsoft.com/platform/support/policy)
- [Obrazy Docker dla platformy .NET](https://hub.docker.com/_/microsoft-dotnet/)
