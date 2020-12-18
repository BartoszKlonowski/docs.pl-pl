---
title: 'NETSDK1005 i NETSDK1047: brak elementu docelowego w pliku zasobów'
description: Jak rozwiązać problem braku elementu docelowego w pliku zasobu.
author: sfoslund
ms.topic: error-reference
ms.date: 12/17/2020
f1_keywords:
- NETSDK1005
- NETSDK1047
ms.openlocfilehash: e3e7389adf6a9a715d44661a5f7cbae5efe299e4
ms.sourcegitcommit: 4b79862c5b41fbd86cf38f926f6a49516059f6f2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/18/2020
ms.locfileid: "97678168"
---
# <a name="netsdk1005-and-netsdk1047-asset-file-is-missing-target"></a>NETSDK1005 i NETSDK1047: brak elementu docelowego w pliku zasobów

**Ten artykuł ma zastosowanie do:** ✔️ .NET Core 2.1.100 SDK i nowszych wersjach

Gdy zestaw SDK programu .NET wystawia błąd NETSDK1005 lub NETSDK1047, w pliku zasobów projektu brakuje informacji o jednej z platform docelowych. Pakiet NuGet zapisuje plik o nazwie *project.assets.js* w folderze *obj* , a zestaw SDK programu .NET używa go do uzyskiwania informacji na temat pakietów do przekazania do kompilatora. W programie .NET 5 pakiet NuGet dodał nowe pole o nazwie `TargetFrameworkAlias` , więc starsze wersje programu MSBuild lub NuGet generują plik zasobów bez nowego pola. Aby uzyskać więcej informacji, zobacz [Error NETSDK1005](https://developercommunity.visualstudio.com/content/problem/1248649/error-netsdk1005-assets-file-projectassetsjson-doe.html).

Poniżej przedstawiono niektóre akcje, które można wykonać, aby rozwiązać ten problem:

* Upewnij się, że korzystasz z programu MSBuild w wersji 16,8 lub nowszej oraz NuGet w wersji 5,8 lub nowszej, a następnie Przywróć projekt po aktualizacji narzędzi. Gdy korzystasz z pakietu NuGet w wersji 5,8 lub nowszej, należy używać programu Visual Studio 2019 w wersji 16,8 lub nowszej, programu MSBuild w wersji 16,8 lub nowszej oraz zestawu .NET 5,0 SDK lub nowszego.

* Jeśli wystąpi błąd podczas kompilowania projektu w programie Visual Studio 2019 po raz pierwszy po zainstalowaniu wersji 16,8 lub po zmianie platformy docelowej projektu, Skompiluj projekt po raz drugi.

* Usuń folder *obj* przed skompilowaniem projektu.

* Upewnij się, że brakująca wartość docelowa jest uwzględniona we `TargetFrameworks` właściwości projektu.
