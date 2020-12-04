---
title: Narzędzie instalacji .NET dla autorów rozszerzeń VS Code
description: Omówienie narzędzia instalacji .NET dla autorów rozszerzeń, Visual Studio Code rozszerzenia do zainstalowania środowiska uruchomieniowego platformy .NET.
author: sfoslund
ms.date: 11/18/2020
ms.openlocfilehash: 37be1b9dcdb9fba99554800fea23f28443efb5fa
ms.sourcegitcommit: 9d525bb8109216ca1dc9e39c149d4902f4b43da5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2020
ms.locfileid: "96599915"
---
# <a name="net-install-tool-for-extension-authors"></a><span data-ttu-id="5f12f-103">Narzędzie instalacji .NET dla autorów rozszerzeń</span><span class="sxs-lookup"><span data-stu-id="5f12f-103">.NET install tool for extension authors</span></span>

<span data-ttu-id="5f12f-104">[Narzędzie instalacji .NET dla autorów rozszerzeń](https://github.com/dotnet/vscode-dotnet-runtime) jest rozszerzeniem Visual Studio Code, które umożliwia przejęcie środowiska uruchomieniowego .NET w odniesieniu do vs Code autorów rozszerzeń.</span><span class="sxs-lookup"><span data-stu-id="5f12f-104">The [.NET install tool for extension authors](https://github.com/dotnet/vscode-dotnet-runtime) is a Visual Studio Code extension that allows acquisition of the .NET runtime specifically for VS Code extension authors.</span></span> <span data-ttu-id="5f12f-105">To narzędzie jest przeznaczone do wykorzystania w rozszerzeniach, które są zapisywane w programie .NET i wymagają programu .NET do rozruchowego fragmentów rozszerzenia (na przykład serwera języka).</span><span class="sxs-lookup"><span data-stu-id="5f12f-105">This tool is intended to be leveraged in extensions that are written in .NET and require .NET to boot pieces of the extension (for example, a language server).</span></span> <span data-ttu-id="5f12f-106">Rozszerzenie nie jest przeznaczone do użycia bezpośrednio przez użytkowników w celu zainstalowania programu .NET na potrzeby programowania.</span><span class="sxs-lookup"><span data-stu-id="5f12f-106">The extension is not intended to be used directly by users to install .NET for development.</span></span>

## <a name="getting-started-extension-authors"></a><span data-ttu-id="5f12f-107">Wprowadzenie: autorów rozszerzeń</span><span class="sxs-lookup"><span data-stu-id="5f12f-107">Getting started: extension authors</span></span>

<span data-ttu-id="5f12f-108">Aby upewnić się, że narzędzie instalacji .NET dla autorów rozszerzeń ma odpowiednie dopasowanie do Twojego scenariusza, Zacznij od przejrzenia [celów tego rozszerzenia](https://github.com/dotnet/vscode-dotnet-runtime#goals-acquiring-net-core-for-extensions) na naszej stronie w serwisie GitHub.</span><span class="sxs-lookup"><span data-stu-id="5f12f-108">To ensure that the .NET install tool for extension authors is the right fit for your scenario, start by reviewing the [goals of this extension](https://github.com/dotnet/vscode-dotnet-runtime#goals-acquiring-net-core-for-extensions) on our GitHub page.</span></span>

> [!NOTE]
> <span data-ttu-id="5f12f-109">Tego narzędzia można użyć do zainstalowania tylko środowiska uruchomieniowego platformy .NET. obecnie nie ma możliwości zainstalowania zestawu .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="5f12f-109">This tool can be used to install the .NET runtime only, it currently does not have the capability to install the .NET SDK.</span></span>

<span data-ttu-id="5f12f-110">Po sprawdzeniu, czy narzędzie instalacji .NET dla autorów rozszerzeń odpowiada Twoim potrzebom, możesz wykonać zależność od niego w [manifeście rozszerzenia](https://code.visualstudio.com/api/references/extension-manifest) i zacząć korzystać z udostępnianych poleceń za pomocą [interfejsu API vs Code](https://code.visualstudio.com/api/extension-guides/command#programmatically-executing-a-command).</span><span class="sxs-lookup"><span data-stu-id="5f12f-110">Once you have verified that the .NET install tool for extension authors fits your needs, you can take a dependency on it in your [extension manifest](https://code.visualstudio.com/api/references/extension-manifest) and begin using the commands we expose with the [VS Code API](https://code.visualstudio.com/api/extension-guides/command#programmatically-executing-a-command).</span></span> <span data-ttu-id="5f12f-111">Listę poleceń udostępnianych przez to rozszerzenie można znaleźć w naszym serwisie [GitHub](https://github.com/dotnet/vscode-dotnet-runtime/blob/master/Documentation/commands.md).</span><span class="sxs-lookup"><span data-stu-id="5f12f-111">You can find the list of commands this extension exposes on our [GitHub](https://github.com/dotnet/vscode-dotnet-runtime/blob/master/Documentation/commands.md).</span></span>

<span data-ttu-id="5f12f-112">Zapoznaj się z tym [przykładowym rozszerzeniem](https://github.com/dotnet/vscode-dotnet-runtime/tree/master/sample) , aby zobaczyć kroki opisane w akcji.</span><span class="sxs-lookup"><span data-stu-id="5f12f-112">Check out this [sample extension](https://github.com/dotnet/vscode-dotnet-runtime/tree/master/sample) to see these steps in action.</span></span>

<span data-ttu-id="5f12f-113">Aby uzyskać więcej przykładów, zapoznaj się z tymi rozszerzeniami typu "open source", które aktualnie korzystają z tego narzędzia:</span><span class="sxs-lookup"><span data-stu-id="5f12f-113">For more examples, check out these open source extensions that currently leverage this tool:</span></span>

- [<span data-ttu-id="5f12f-114">Narzędzia Azure Resource Manager (ARM) dla Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="5f12f-114">Azure Resource Manager (ARM) Tools for Visual Studio Code</span></span>](https://github.com/microsoft/vscode-azurearmtools)

- [<span data-ttu-id="5f12f-115">Notesy programu .NET Interactive</span><span class="sxs-lookup"><span data-stu-id="5f12f-115">.NET Interactive Notebooks</span></span>](https://github.com/dotnet/interactive/tree/main/src/dotnet-interactive-vscode)

## <a name="getting-started-end-users"></a><span data-ttu-id="5f12f-116">Wprowadzenie: użytkownicy końcowi</span><span class="sxs-lookup"><span data-stu-id="5f12f-116">Getting started: end users</span></span>

<span data-ttu-id="5f12f-117">Ogólnie rzecz biorąc, użytkownik końcowy nie musi korzystać z narzędzia do instalowania platformy .NET dla autorów rozszerzeń.</span><span class="sxs-lookup"><span data-stu-id="5f12f-117">In general, the end user should not need to interact with the .NET install tool for extension authors at all.</span></span> <span data-ttu-id="5f12f-118">Jeśli masz problemy z rozszerzeniem, zapoznaj się z naszą [stroną rozwiązywania problemów](https://github.com/dotnet/vscode-dotnet-runtime/blob/master/Documentation/troubleshooting.md) , aby rozwiązać problem z naszym serwisem [GitHub](https://github.com/dotnet/vscode-dotnet-runtime/issues).</span><span class="sxs-lookup"><span data-stu-id="5f12f-118">If you are having problems with the extension, check out our [troubleshooting page](https://github.com/dotnet/vscode-dotnet-runtime/blob/master/Documentation/troubleshooting.md) or file an issue on our [GitHub](https://github.com/dotnet/vscode-dotnet-runtime/issues).</span></span>
