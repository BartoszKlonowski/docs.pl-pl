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
# <a name="net-install-tool-for-extension-authors"></a>Narzędzie instalacji .NET dla autorów rozszerzeń

[Narzędzie instalacji .NET dla autorów rozszerzeń](https://github.com/dotnet/vscode-dotnet-runtime) jest rozszerzeniem Visual Studio Code, które umożliwia przejęcie środowiska uruchomieniowego .NET w odniesieniu do vs Code autorów rozszerzeń. To narzędzie jest przeznaczone do wykorzystania w rozszerzeniach, które są zapisywane w programie .NET i wymagają programu .NET do rozruchowego fragmentów rozszerzenia (na przykład serwera języka). Rozszerzenie nie jest przeznaczone do użycia bezpośrednio przez użytkowników w celu zainstalowania programu .NET na potrzeby programowania.

## <a name="getting-started-extension-authors"></a>Wprowadzenie: autorów rozszerzeń

Aby upewnić się, że narzędzie instalacji .NET dla autorów rozszerzeń ma odpowiednie dopasowanie do Twojego scenariusza, Zacznij od przejrzenia [celów tego rozszerzenia](https://github.com/dotnet/vscode-dotnet-runtime#goals-acquiring-net-core-for-extensions) na naszej stronie w serwisie GitHub.

> [!NOTE]
> Tego narzędzia można użyć do zainstalowania tylko środowiska uruchomieniowego platformy .NET. obecnie nie ma możliwości zainstalowania zestawu .NET SDK.

Po sprawdzeniu, czy narzędzie instalacji .NET dla autorów rozszerzeń odpowiada Twoim potrzebom, możesz wykonać zależność od niego w [manifeście rozszerzenia](https://code.visualstudio.com/api/references/extension-manifest) i zacząć korzystać z udostępnianych poleceń za pomocą [interfejsu API vs Code](https://code.visualstudio.com/api/extension-guides/command#programmatically-executing-a-command). Listę poleceń udostępnianych przez to rozszerzenie można znaleźć w naszym serwisie [GitHub](https://github.com/dotnet/vscode-dotnet-runtime/blob/master/Documentation/commands.md).

Zapoznaj się z tym [przykładowym rozszerzeniem](https://github.com/dotnet/vscode-dotnet-runtime/tree/master/sample) , aby zobaczyć kroki opisane w akcji.

Aby uzyskać więcej przykładów, zapoznaj się z tymi rozszerzeniami typu "open source", które aktualnie korzystają z tego narzędzia:

- [Narzędzia Azure Resource Manager (ARM) dla Visual Studio Code](https://github.com/microsoft/vscode-azurearmtools)

- [Notesy programu .NET Interactive](https://github.com/dotnet/interactive/tree/main/src/dotnet-interactive-vscode)

## <a name="getting-started-end-users"></a>Wprowadzenie: użytkownicy końcowi

Ogólnie rzecz biorąc, użytkownik końcowy nie musi korzystać z narzędzia do instalowania platformy .NET dla autorów rozszerzeń. Jeśli masz problemy z rozszerzeniem, zapoznaj się z naszą [stroną rozwiązywania problemów](https://github.com/dotnet/vscode-dotnet-runtime/blob/master/Documentation/troubleshooting.md) , aby rozwiązać problem z naszym serwisem [GitHub](https://github.com/dotnet/vscode-dotnet-runtime/issues).
