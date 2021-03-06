---
title: 'Zmiana podziału: Kestrel: Libuv transport oznaczony jako przestarzały'
description: 'Dowiedz się więcej o istotnej zmianie w ASP.NET Core 5,0 zatytułowanej Kestrel: Libuv transport oznaczony jako przestarzały'
author: scottaddie
ms.author: scaddie
ms.date: 10/01/2020
ms.openlocfilehash: f66b9b646671e07957e6d30a95333d392eb29617
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/24/2020
ms.locfileid: "95761520"
---
# <a name="kestrel-libuv-transport-marked-as-obsolete"></a>Kestrel: transport Libuv oznaczony jako przestarzały

We wcześniejszych wersjach ASP.NET Core Libuv jako szczegóły implementacji, jak asynchroniczne dane wejściowe i wyjściowe zostały wykonane. W ASP.NET Core 2,0 został opracowany alternatywny <xref:System.Net.Sockets.Socket> transport oparty na bazie. W ASP.NET Core 2,1 Kestrel przełączać się do korzystania z `Socket` transportu opartego na protokole domyślnym. Obsługa Libuv została zachowana ze względu na zgodność.

W tym momencie korzystanie z `Socket` transportu opartego na bazie jest znacznie bardziej powszechne niż transport Libuv. W związku z tym pomoc techniczna Libuv jest oznaczona jako przestarzała w programie .NET 5,0 i zostanie usunięta całkowicie w programie .NET 6,0.

W ramach tej zmiany Libuv obsługę nowych platform systemu operacyjnego (na przykład Windows ARM64) nie zostaną dodane w przedziale czasu .NET 5,0.

Aby uzyskać więcej dyskusji na temat blokowania problemów, które wymagają użycia transportu Libuv, zobacz problem z usługą GitHub w usłudze [dotnet/aspnetcore # 23409](https://github.com/dotnet/aspnetcore/issues/23409).

## <a name="version-introduced"></a>Wprowadzona wersja

5,0 wersja zapoznawcza 8

## <a name="old-behavior"></a>Stare zachowanie

Interfejsy API Libuv nie są oznaczone jako przestarzałe.

## <a name="new-behavior"></a>Nowe zachowanie

Interfejsy API Libuv są oznaczone jako przestarzałe.

## <a name="reason-for-change"></a>Przyczyna zmiany

`Socket`Domyślnym ustawieniem jest transport oparty na protokole. Nie ma żadnych istotnych powodów, aby nadal korzystać z transportu Libuv.

## <a name="recommended-action"></a>Zalecana akcja

Zaprzestanie korzystania z [pakietu Libuv](https://www.nuget.org/packages/Libuv) i metod rozszerzających.

## <a name="affected-apis"></a>Dotyczy interfejsów API

- [WebHostBuilderLibuvExtensions](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderlibuvextensions?view=aspnetcore-3.0)
- [WebHostBuilderLibuvExtensions.UseLibuv](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderlibuvextensions.uselibuv?view=aspnetcore-3.0)
- [Microsoft. AspNetCore. Server. Kestrel. transport. Libuv. LibuvTransportOptions](/dotnet/api/microsoft.aspnetcore.server.kestrel.transport.libuv.libuvtransportoptions?view=aspnetcore-3.0)
- [Microsoft. AspNetCore. Server. Kestrel. transport. Libuv. LibuvTransportOptions. ThreadCount](/dotnet/api/microsoft.aspnetcore.server.kestrel.transport.libuv.libuvtransportoptions.threadcount?view=aspnetcore-3.0)
- [Microsoft. AspNetCore. Server. Kestrel. transport. Libuv. LibuvTransportOptions. NoDelay](/dotnet/api/microsoft.aspnetcore.server.kestrel.transport.libuv.libuvtransportoptions.nodelay?view=aspnetcore-3.0)
- [Microsoft. AspNetCore. Server. Kestrel. transport. Libuv. LibuvTransportOptions. MaxWriteBufferSize](/dotnet/api/microsoft.aspnetcore.server.kestrel.transport.libuv.libuvtransportoptions.maxwritebuffersize?view=aspnetcore-3.0)
- [Microsoft. AspNetCore. Server. Kestrel. transport. Libuv. LibuvTransportOptions. MaxReadBufferSize](/dotnet/api/microsoft.aspnetcore.server.kestrel.transport.libuv.libuvtransportoptions.maxreadbuffersize?view=aspnetcore-3.0)
- `Microsoft.AspNetCore.Server.Kestrel.Transport.Libuv.LibuvTransportOptions.Backlog`

<!--

### Category

ASP.NET Core

### Affected APIs

- `T:Microsoft.AspNetCore.Hosting.WebHostBuilderLibuvExtensions`
- `Overload:Microsoft.AspNetCore.Hosting.WebHostBuilderLibuvExtensions.UseLibuv`
- `T:Microsoft.AspNetCore.Server.Kestrel.Transport.Libuv.LibuvTransportOptions`
- `P:Microsoft.AspNetCore.Server.Kestrel.Transport.Libuv.LibuvTransportOptions.ThreadCount`
- `P:Microsoft.AspNetCore.Server.Kestrel.Transport.Libuv.LibuvTransportOptions.NoDelay`
- `P:Microsoft.AspNetCore.Server.Kestrel.Transport.Libuv.LibuvTransportOptions.MaxWriteBufferSize`
- `P:Microsoft.AspNetCore.Server.Kestrel.Transport.Libuv.LibuvTransportOptions.MaxReadBufferSize`
- `P:Microsoft.AspNetCore.Server.Kestrel.Transport.Libuv.LibuvTransportOptions.Backlog`

-->
