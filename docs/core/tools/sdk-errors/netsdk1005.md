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
# <a name="netsdk1005-and-netsdk1047-asset-file-is-missing-target"></a><span data-ttu-id="8e065-103">NETSDK1005 i NETSDK1047: brak elementu docelowego w pliku zasobów</span><span class="sxs-lookup"><span data-stu-id="8e065-103">NETSDK1005 and NETSDK1047: Asset file is missing target</span></span>

<span data-ttu-id="8e065-104">**Ten artykuł ma zastosowanie do:** ✔️ .NET Core 2.1.100 SDK i nowszych wersjach</span><span class="sxs-lookup"><span data-stu-id="8e065-104">**This article applies to:** ✔️ .NET Core 2.1.100 SDK and later versions</span></span>

<span data-ttu-id="8e065-105">Gdy zestaw SDK programu .NET wystawia błąd NETSDK1005 lub NETSDK1047, w pliku zasobów projektu brakuje informacji o jednej z platform docelowych.</span><span class="sxs-lookup"><span data-stu-id="8e065-105">When the .NET SDK issues error NETSDK1005 or NETSDK1047, the project's assets file is missing information on one of your target frameworks.</span></span> <span data-ttu-id="8e065-106">Pakiet NuGet zapisuje plik o nazwie *project.assets.js* w folderze *obj* , a zestaw SDK programu .NET używa go do uzyskiwania informacji na temat pakietów do przekazania do kompilatora.</span><span class="sxs-lookup"><span data-stu-id="8e065-106">NuGet writes a file named *project.assets.json* in the *obj* folder, and the .NET SDK uses it to get information about packages to pass into the compiler.</span></span> <span data-ttu-id="8e065-107">W programie .NET 5 pakiet NuGet dodał nowe pole o nazwie `TargetFrameworkAlias` , więc starsze wersje programu MSBuild lub NuGet generują plik zasobów bez nowego pola.</span><span class="sxs-lookup"><span data-stu-id="8e065-107">In .NET 5, NuGet added a new field named `TargetFrameworkAlias`, so earlier versions of MSBuild or NuGet generate an assets file without the new field.</span></span> <span data-ttu-id="8e065-108">Aby uzyskać więcej informacji, zobacz [Error NETSDK1005](https://developercommunity.visualstudio.com/content/problem/1248649/error-netsdk1005-assets-file-projectassetsjson-doe.html).</span><span class="sxs-lookup"><span data-stu-id="8e065-108">For more information, see [error NETSDK1005](https://developercommunity.visualstudio.com/content/problem/1248649/error-netsdk1005-assets-file-projectassetsjson-doe.html).</span></span>

<span data-ttu-id="8e065-109">Poniżej przedstawiono niektóre akcje, które można wykonać, aby rozwiązać ten problem:</span><span class="sxs-lookup"><span data-stu-id="8e065-109">Here are some actions you can take that may resolve the error:</span></span>

* <span data-ttu-id="8e065-110">Upewnij się, że korzystasz z programu MSBuild w wersji 16,8 lub nowszej oraz NuGet w wersji 5,8 lub nowszej, a następnie Przywróć projekt po aktualizacji narzędzi.</span><span class="sxs-lookup"><span data-stu-id="8e065-110">Make sure that you're using MSBuild version 16.8 or later and NuGet version 5.8 or later, and restore the project after updating your tools.</span></span> <span data-ttu-id="8e065-111">Gdy korzystasz z pakietu NuGet w wersji 5,8 lub nowszej, należy używać programu Visual Studio 2019 w wersji 16,8 lub nowszej, programu MSBuild w wersji 16,8 lub nowszej oraz zestawu .NET 5,0 SDK lub nowszego.</span><span class="sxs-lookup"><span data-stu-id="8e065-111">When you're using NuGet version 5.8 or later, you should be using Visual Studio 2019 version 16.8 or later, MSBuild version 16.8 or later, and .NET 5.0 SDK or later.</span></span>

* <span data-ttu-id="8e065-112">Jeśli wystąpi błąd podczas kompilowania projektu w programie Visual Studio 2019 po raz pierwszy po zainstalowaniu wersji 16,8 lub po zmianie platformy docelowej projektu, Skompiluj projekt po raz drugi.</span><span class="sxs-lookup"><span data-stu-id="8e065-112">If you get the error while building a project in Visual Studio 2019 for the first time after installing version 16.8 or after changing the project's target framework, build the project a second time.</span></span>

* <span data-ttu-id="8e065-113">Usuń folder *obj* przed skompilowaniem projektu.</span><span class="sxs-lookup"><span data-stu-id="8e065-113">Delete the *obj* folder before building the project.</span></span>

* <span data-ttu-id="8e065-114">Upewnij się, że brakująca wartość docelowa jest uwzględniona we `TargetFrameworks` właściwości projektu.</span><span class="sxs-lookup"><span data-stu-id="8e065-114">Make sure that the missing target value is included in the `TargetFrameworks` property of your project.</span></span>
