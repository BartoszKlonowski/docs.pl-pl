---
title: Uruchom polecenie Narzędzia dotnet
description: Polecenie Uruchom narzędzie dotnet wywołuje narzędzie lokalne.
ms.date: 02/14/2020
ms.openlocfilehash: 116ecb61748a0ca70ed385b279b11b939748f4a8
ms.sourcegitcommit: b201d177e01480a139622f3bf8facd367657a472
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/15/2020
ms.locfileid: "94634158"
---
# <a name="dotnet-tool-run"></a><span data-ttu-id="91202-103">dotnet tool run</span><span class="sxs-lookup"><span data-stu-id="91202-103">dotnet tool run</span></span>

<span data-ttu-id="91202-104">**Ten artykuł ma zastosowanie do:** ✔️ .net Core 3,0 SDK i nowszych wersjach</span><span class="sxs-lookup"><span data-stu-id="91202-104">**This article applies to:** ✔️ .NET Core 3.0 SDK and later versions</span></span>

## <a name="name"></a><span data-ttu-id="91202-105">Nazwa</span><span class="sxs-lookup"><span data-stu-id="91202-105">Name</span></span>

<span data-ttu-id="91202-106">`dotnet tool run` -Wywołuje narzędzie lokalne.</span><span class="sxs-lookup"><span data-stu-id="91202-106">`dotnet tool run` - Invokes a local tool.</span></span>

## <a name="synopsis"></a><span data-ttu-id="91202-107">Streszczenie</span><span class="sxs-lookup"><span data-stu-id="91202-107">Synopsis</span></span>

```dotnetcli
dotnet tool run <COMMAND NAME>

dotnet tool run -h|--help
```

## <a name="description"></a><span data-ttu-id="91202-108">Opis</span><span class="sxs-lookup"><span data-stu-id="91202-108">Description</span></span>

<span data-ttu-id="91202-109">`dotnet tool run`Polecenie przeszukuje pliki manifestu narzędzia, które znajdują się w zakresie dla bieżącego katalogu.</span><span class="sxs-lookup"><span data-stu-id="91202-109">The `dotnet tool run` command searches tool manifest files that are in scope for the current directory.</span></span> <span data-ttu-id="91202-110">Po znalezieniu odwołania do określonego narzędzia zostanie uruchomione narzędzie.</span><span class="sxs-lookup"><span data-stu-id="91202-110">When it finds a reference to the specified tool, it runs the tool.</span></span> <span data-ttu-id="91202-111">Aby uzyskać więcej informacji, zobacz [wywoływanie narzędzia lokalnego](global-tools.md#invoke-a-local-tool).</span><span class="sxs-lookup"><span data-stu-id="91202-111">For more information, see [Invoke a local tool](global-tools.md#invoke-a-local-tool).</span></span>

## <a name="arguments"></a><span data-ttu-id="91202-112">Argumenty</span><span class="sxs-lookup"><span data-stu-id="91202-112">Arguments</span></span>

- **`COMMAND_NAME`**

  <span data-ttu-id="91202-113">Nazwa polecenia narzędzia do uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="91202-113">The command name of the tool to run.</span></span>

## <a name="options"></a><span data-ttu-id="91202-114">Opcje</span><span class="sxs-lookup"><span data-stu-id="91202-114">Options</span></span>

- **`-h|--help`**

  <span data-ttu-id="91202-115">Drukuje krótką pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="91202-115">Prints out a short help for the command.</span></span>

## <a name="example"></a><span data-ttu-id="91202-116">Przykład</span><span class="sxs-lookup"><span data-stu-id="91202-116">Example</span></span>

- **`dotnet tool run dotnetsay`**

  <span data-ttu-id="91202-117">Uruchamia `dotnetsay` Narzędzie lokalne.</span><span class="sxs-lookup"><span data-stu-id="91202-117">Runs the `dotnetsay` local tool.</span></span>

## <a name="see-also"></a><span data-ttu-id="91202-118">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="91202-118">See also</span></span>

- [<span data-ttu-id="91202-119">Narzędzia .NET</span><span class="sxs-lookup"><span data-stu-id="91202-119">.NET tools</span></span>](global-tools.md)
- [<span data-ttu-id="91202-120">Samouczek: Instalowanie i używanie lokalnego narzędzia .NET przy użyciu interfejsu wiersza polecenia platformy .NET</span><span class="sxs-lookup"><span data-stu-id="91202-120">Tutorial: Install and use a .NET local tool using the .NET CLI</span></span>](local-tools-how-to-use.md)
