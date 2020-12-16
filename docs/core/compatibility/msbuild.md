---
title: Zmiany w programie MSBuild
description: Wyświetla listę istotnych zmian w programie MSBuild dla platformy .NET Core 3,0-3,1.
ms.date: 12/14/2020
ms.openlocfilehash: 1ed5878845406fa7727c644f1e196d63a860646a
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/16/2020
ms.locfileid: "97593451"
---
# <a name="msbuild-breaking-changes-in-net-core-30---31"></a>Zmiany w programie MSBuild w programie .NET Core 3,0 — 3,1

Następujące istotne zmiany zostały udokumentowane na tej stronie:

| Zmiana podziału | Wprowadzona wersja |
| - | - |
| [Kompilacje w czasie projektowania zwracają tylko odwołania do pakietów najwyższego poziomu](#design-time-builds-only-return-top-level-package-references) | 3,1 |
| [Zmiana nazwy pliku manifestu zasobu](#resource-manifest-file-name-change) | 3.0 |

## <a name="net-core-31"></a>.NET Core 3.1

[!INCLUDE [design-time-builds-return-top-level-package-refs](../../../includes/core-changes/msbuild/3.1/design-time-builds-return-top-level-package-refs.md)]

***

## <a name="net-core-30"></a>.NET Core 3.0

[!INCLUDE[Resource file names](~/includes/core-changes/msbuild/3.0/resource-manifest-name.md)]

***
