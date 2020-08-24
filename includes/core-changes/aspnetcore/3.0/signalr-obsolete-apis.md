---
ms.openlocfilehash: 2a65caedea2af65796267aa145e275ebff814bf8
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/14/2020
ms.locfileid: "72394062"
---
### <a name="signalr-usesignalr-and-useconnections-methods-marked-obsolete"></a><span data-ttu-id="5ccbc-101">Sygnalizujący: metody UseSignalR i UseConnections oznaczone jako przestarzałe</span><span class="sxs-lookup"><span data-stu-id="5ccbc-101">SignalR: UseSignalR and UseConnections methods marked obsolete</span></span>

<span data-ttu-id="5ccbc-102">Metody `UseConnections` i `UseSignalR` i klasy `ConnectionsRouteBuilder` i `HubRouteBuilder` są oznaczone jako przestarzałe w ASP.NET Core 3,0.</span><span class="sxs-lookup"><span data-stu-id="5ccbc-102">The methods `UseConnections` and `UseSignalR` and the classes `ConnectionsRouteBuilder` and `HubRouteBuilder` are marked as obsolete in ASP.NET Core 3.0.</span></span>

#### <a name="version-introduced"></a><span data-ttu-id="5ccbc-103">Wprowadzona wersja</span><span class="sxs-lookup"><span data-stu-id="5ccbc-103">Version introduced</span></span>

<span data-ttu-id="5ccbc-104">3,0</span><span class="sxs-lookup"><span data-stu-id="5ccbc-104">3.0</span></span>

#### <a name="old-behavior"></a><span data-ttu-id="5ccbc-105">Stare zachowanie</span><span class="sxs-lookup"><span data-stu-id="5ccbc-105">Old behavior</span></span>

<span data-ttu-id="5ccbc-106">Routing centrum sygnałów został skonfigurowany przy użyciu `UseSignalR` lub `UseConnections` .</span><span class="sxs-lookup"><span data-stu-id="5ccbc-106">SignalR hub routing was configured using `UseSignalR` or `UseConnections`.</span></span>

#### <a name="new-behavior"></a><span data-ttu-id="5ccbc-107">Nowe zachowanie</span><span class="sxs-lookup"><span data-stu-id="5ccbc-107">New behavior</span></span>

<span data-ttu-id="5ccbc-108">Stary sposób konfigurowania routingu został przestarzały i zastąpiony przez Routing punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="5ccbc-108">The old way of configuring routing has been obsoleted and replaced with endpoint routing.</span></span>

#### <a name="reason-for-change"></a><span data-ttu-id="5ccbc-109">Przyczyna zmiany</span><span class="sxs-lookup"><span data-stu-id="5ccbc-109">Reason for change</span></span>

<span data-ttu-id="5ccbc-110">Oprogramowanie pośredniczące jest przenoszone do nowego systemu routingu punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="5ccbc-110">Middleware is being moved to the new endpoint routing system.</span></span> <span data-ttu-id="5ccbc-111">Stary sposób dodawania oprogramowania pośredniczącego jest przestarzały.</span><span class="sxs-lookup"><span data-stu-id="5ccbc-111">The old way of adding middleware is being obsoleted.</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="5ccbc-112">Zalecana akcja</span><span class="sxs-lookup"><span data-stu-id="5ccbc-112">Recommended action</span></span>

<span data-ttu-id="5ccbc-113">Zamień `UseSignalR` na `UseEndpoints` :</span><span class="sxs-lookup"><span data-stu-id="5ccbc-113">Replace `UseSignalR` with `UseEndpoints`:</span></span>

<span data-ttu-id="5ccbc-114">**Stary kod:**</span><span class="sxs-lookup"><span data-stu-id="5ccbc-114">**Old code:**</span></span>

```csharp
app.UseSignalR(routes =>
{
    routes.MapHub<SomeHub>("/path");
});
```

<span data-ttu-id="5ccbc-115">**Nowy kod:**</span><span class="sxs-lookup"><span data-stu-id="5ccbc-115">**New code:**</span></span>

```csharp
app.UseEndpoints(endpoints =>
{
    endpoints.MapHub<SomeHub>("/path");
});
```

#### <a name="category"></a><span data-ttu-id="5ccbc-116">Kategoria</span><span class="sxs-lookup"><span data-stu-id="5ccbc-116">Category</span></span>

<span data-ttu-id="5ccbc-117">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="5ccbc-117">ASP.NET Core</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="5ccbc-118">Dotyczy interfejsów API</span><span class="sxs-lookup"><span data-stu-id="5ccbc-118">Affected APIs</span></span>

- <xref:Microsoft.AspNetCore.Builder.ConnectionsAppBuilderExtensions.UseConnections(Microsoft.AspNetCore.Builder.IApplicationBuilder,System.Action{Microsoft.AspNetCore.Http.Connections.ConnectionsRouteBuilder})?displayProperty=fullName>
- <xref:Microsoft.AspNetCore.Builder.SignalRAppBuilderExtensions.UseSignalR(Microsoft.AspNetCore.Builder.IApplicationBuilder,System.Action{Microsoft.AspNetCore.SignalR.HubRouteBuilder})?displayProperty=fullName>
- <xref:Microsoft.AspNetCore.Http.Connections.ConnectionsRouteBuilder?displayProperty=fullName>
- <xref:Microsoft.AspNetCore.SignalR.HubRouteBuilder?displayProperty=fullName>

<!-- 

#### Affected APIs

- `M:Microsoft.AspNetCore.Builder.ConnectionsAppBuilderExtensions.UseConnections(Microsoft.AspNetCore.Builder.IApplicationBuilder,System.Action{Microsoft.AspNetCore.Http.Connections.ConnectionsRouteBuilder})`
- `M:Microsoft.AspNetCore.Builder.SignalRAppBuilderExtensions.UseSignalR(Microsoft.AspNetCore.Builder.IApplicationBuilder,System.Action{Microsoft.AspNetCore.SignalR.HubRouteBuilder})`
- `T:Microsoft.AspNetCore.Http.Connections.ConnectionsRouteBuilder`
- `T:Microsoft.AspNetCore.SignalR.HubRouteBuilder`

-->
