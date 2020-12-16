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
# <a name="msbuild-breaking-changes-in-net-core-30---31"></a><span data-ttu-id="664d2-103">Zmiany w programie MSBuild w programie .NET Core 3,0 — 3,1</span><span class="sxs-lookup"><span data-stu-id="664d2-103">MSBuild breaking changes in .NET Core 3.0 - 3.1</span></span>

<span data-ttu-id="664d2-104">Następujące istotne zmiany zostały udokumentowane na tej stronie:</span><span class="sxs-lookup"><span data-stu-id="664d2-104">The following breaking changes are documented on this page:</span></span>

| <span data-ttu-id="664d2-105">Zmiana podziału</span><span class="sxs-lookup"><span data-stu-id="664d2-105">Breaking change</span></span> | <span data-ttu-id="664d2-106">Wprowadzona wersja</span><span class="sxs-lookup"><span data-stu-id="664d2-106">Version introduced</span></span> |
| - | - |
| [<span data-ttu-id="664d2-107">Kompilacje w czasie projektowania zwracają tylko odwołania do pakietów najwyższego poziomu</span><span class="sxs-lookup"><span data-stu-id="664d2-107">Design-time builds only return top-level package references</span></span>](#design-time-builds-only-return-top-level-package-references) | <span data-ttu-id="664d2-108">3,1</span><span class="sxs-lookup"><span data-stu-id="664d2-108">3.1</span></span> |
| [<span data-ttu-id="664d2-109">Zmiana nazwy pliku manifestu zasobu</span><span class="sxs-lookup"><span data-stu-id="664d2-109">Resource manifest file name change</span></span>](#resource-manifest-file-name-change) | <span data-ttu-id="664d2-110">3.0</span><span class="sxs-lookup"><span data-stu-id="664d2-110">3.0</span></span> |

## <a name="net-core-31"></a><span data-ttu-id="664d2-111">.NET Core 3.1</span><span class="sxs-lookup"><span data-stu-id="664d2-111">.NET Core 3.1</span></span>

[!INCLUDE [design-time-builds-return-top-level-package-refs](../../../includes/core-changes/msbuild/3.1/design-time-builds-return-top-level-package-refs.md)]

***

## <a name="net-core-30"></a><span data-ttu-id="664d2-112">.NET Core 3.0</span><span class="sxs-lookup"><span data-stu-id="664d2-112">.NET Core 3.0</span></span>

[!INCLUDE[Resource file names](~/includes/core-changes/msbuild/3.0/resource-manifest-name.md)]

***
