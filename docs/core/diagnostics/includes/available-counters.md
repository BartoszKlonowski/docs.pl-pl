---
ms.openlocfilehash: 2046762be2ae5d6d4c9f7fb061849b63e7ab06a2
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/16/2020
ms.locfileid: "97612686"
---
## <a name="available-counters"></a>Dostępne liczniki

W przypadku różnych pakietów platformy .NET Podstawowe metryki dotyczące odzyskiwania pamięci (GC), just-in-Time (JIT), zestawów, wyjątków, wątków, sieci i żądań sieci Web są publikowane przy użyciu EventCounters.

### <a name="systemruntime-counters"></a>Liczniki "System. Runtime"

Następujące liczniki są publikowane w ramach środowiska uruchomieniowego .NET i są obsługiwane w [`RuntimeEventSource.cs`](https://github.com/dotnet/coreclr/blob/master/src/System.Private.CoreLib/src/System/Diagnostics/Eventing/RuntimeEventSource.cs) .

| Licznik | Opis |
|--|--|
| :::no-loc text="% Time in GC since last GC"::: (`time-in-gc`) | Procent czasu w GC od momentu ostatniego GC |
| :::no-loc text="Allocation Rate"::: (`alloc-rate`) | Liczba bajtów przydzielono na interwał aktualizacji |
| :::no-loc text="CPU Usage"::: (`cpu-usage`) | Procent użycia procesora CPU przez proces |
| :::no-loc text="Exception Count"::: (`exception-count`) | Liczba wyjątków, które wystąpiły |
| :::no-loc text="GC Heap Size"::: (`gc-heap-size`) | Liczba bajtów, które mają być przydzieloną na podstawie <xref:System.GC.GetTotalMemory(System.Boolean)?displayProperty=nameWithType> |
| :::no-loc text="Gen 0 GC Count"::: (`gen-0-gc-count`) | Liczba wykonań GC dla generacji 0 |
| :::no-loc text="Gen 0 Size"::: (`gen-0-size`) | Liczba bajtów dla generacji 0 GC |
| :::no-loc text="Gen 1 GC Count"::: (`gen-1-gc-count`) | Liczba wykonań GC dla generacji 1 |
| :::no-loc text="Gen 1 Size"::: (`gen-1-size`) | Liczba bajtów dla generacji 1 GC |
| :::no-loc text="Gen 2 GC Count"::: (`gen-2-gc-count`) | Liczba przypadków wygenerowania GC dla generacji 2 |
| :::no-loc text="Gen 2 Size"::: (`gen-2-size`) | Liczba bajtów dla generacji 2 GC |
| :::no-loc text="LOH Size"::: (`loh-size`) | Liczba bajtów dla generacji 2 GC |
| :::no-loc text="POH Size"::: (`poh-size`) | Liczba bajtów dla przypiętych sterty obiektów (dostępnych w programie .NET 5 i nowszych wersjach) |
| :::no-loc text="GC Fragmentation"::: (`gc-fragmentation`) | Fragmentacja sterty GC (dostępna w programie .NET 5 i nowszych wersjach) |
| :::no-loc text="Monitor Lock Contention Count"::: (`monitor-lock-contention-count`) | Liczba przypadków rywalizacji podczas próby przeprowadzenia blokady monitora na podstawie <xref:System.Threading.Monitor.LockContentionCount?displayProperty=nameWithType> |
| :::no-loc text="Number of Active Timers"::: (`active-timer-count`) | Liczba <xref:System.Threading.Timer> wystąpień, które są obecnie aktywne, na podstawie <xref:System.Threading.Timer.ActiveCount?displayProperty=nameWithType> |
| :::no-loc text="Number of Assemblies Loaded"::: (`assembly-count`) | Liczba <xref:System.Reflection.Assembly> wystąpień załadowanych do procesu w punkcie w czasie |
| :::no-loc text="ThreadPool Completed Work Item Count"::: (`threadpool-completed-items-count`) | Liczba elementów roboczych, które zostały przetworzone do tej pory w <xref:System.Threading.ThreadPool> |
| :::no-loc text="ThreadPool Queue Length"::: (`threadpool-queue-length`) | Liczba elementów roboczych, które są obecnie umieszczane w kolejce do przetworzenia w <xref:System.Threading.ThreadPool> |
| :::no-loc text="ThreadPool Thread Count"::: (`threadpool-thread-count`) | Liczba wątków puli wątków, które znajdują się obecnie w <xref:System.Threading.ThreadPool> , w oparciu o <xref:System.Threading.ThreadPool.ThreadCount?displayProperty=nameWithType> |
| :::no-loc text="Working Set"::: (`working-set`) | Ilość pamięci fizycznej zamapowanej na kontekst procesu w punkcie w bazie czasu na <xref:System.Environment.WorkingSet?displayProperty=nameWithType> |
| :::no-loc text="IL Bytes Jitted"::: (`il-bytes-jitted`) | Łączny rozmiar witryn ILs, które są kompilowane w trybie JIT, w bajtach (dostępne w programie .NET 5 i nowszych wersjach) |
| :::no-loc text="Method Jitted Count"::: (`method-jitted-count`) | Liczba metod, które są kompilowane w trybie JIT (dostępne w programie .NET 5 i nowszych wersjach) |

### <a name="microsoftaspnetcorehosting-counters"></a>Liczniki "Microsoft. AspNetCore. hosting"

Następujące liczniki są publikowane w ramach [ASP.NET Core](/aspnet/core) i są obsługiwane w [`HostingEventSource.cs`](https://github.com/dotnet/aspnetcore/blob/master/src/Hosting/Hosting/src/Internal/HostingEventSource.cs) .

| Licznik | Opis |
|--|--|
| :::no-loc text="Current Requests"::: (`current-requests`) | Całkowita liczba żądań, które zostały uruchomione, ale nie zostały jeszcze zatrzymane |
| :::no-loc text="Failed Requests"::: (`failed-requests`) | Całkowita liczba nieudanych żądań, które wystąpiły w okresie istnienia aplikacji |
| :::no-loc text="Request Rate"::: (`requests-per-second`) | Liczba żądań, które wystąpiły dla interwału aktualizacji |
| :::no-loc text="Total Requests"::: (`total-requests`) | Całkowita liczba żądań, które wystąpiły w okresie istnienia aplikacji |

### <a name="microsoftaspnetcorehttpconnections-counters"></a>Liczniki "Microsoft. AspNetCore. http. Connections"

Następujące liczniki są publikowane jako część [sygnalizującego ASP.NET Core](/aspnet/core/signalr/introduction) i są obsługiwane w [`HttpConnectionsEventSource.cs`](https://github.com/dotnet/aspnetcore/blob/master/src/SignalR/common/Http.Connections/src/Internal/HttpConnectionsEventSource.cs) .

| Licznik | Opis |
|--|--|
| :::no-loc text="Average Connection Duration"::: (`connections-duration`) | Średni czas trwania połączenia w milisekundach |
| :::no-loc text="Current Connections"::: (`current-connections`) | Liczba aktywnych połączeń, które zostały uruchomione, ale nie zostały jeszcze zatrzymane |
| :::no-loc text="Total Connections Started"::: (`connections-started`) | Całkowita liczba uruchomionych połączeń |
| :::no-loc text="Total Connections Stopped"::: (`connections-stopped`) | Całkowita liczba zatrzymanych połączeń |
| :::no-loc text="Total Connections Timed Out"::: (`connections-timed-out`) | Całkowita liczba połączeń, które przekroczyły limit czasu |

### <a name="microsoft-aspnetcore-server-kestrel-counters"></a>Liczniki "Microsoft-AspNetCore-Server-Kestrel"

Następujące liczniki są publikowane jako część [serwera sieci Web programu ASP.NET Core Kestrel](/aspnet/core/fundamentals/servers/kestrel) i są obsługiwane w programie [`KestrelEventSource.cs`](https://github.com/dotnet/aspnetcore/blob/master/src/Servers/Kestrel/Core/src/Internal/Infrastructure/KestrelEventSource.cs) .

| Licznik | Opis |
|--|--|
| :::no-loc text="Connection Queue Length"::: (`connection-queue-length`) | Bieżąca długość kolejki połączeń |
| :::no-loc text="Connection Rate"::: (`connections-per-second`) | Liczba połączeń według interwału aktualizacji serwera sieci Web |
| :::no-loc text="Current Connections"::: (`current-connections`) | Bieżąca liczba aktywnych połączeń z serwerem sieci Web |
| :::no-loc text="Current TLS Handshakes"::: (`current-tls-handshakes`) | Bieżąca liczba uzgodnień TLS |
| :::no-loc text="Current Upgraded Requests (WebSockets)"::: (`current-upgraded-requests`) | Bieżąca liczba uaktualnionych żądań (WebSockets) |
| :::no-loc text="Failed TLS Handshakes"::: (`failed-tls-handshakes`) | Łączna liczba niezakończonych uzgodnień TLS |
| :::no-loc text="Request Queue Length"::: (`request-queue-length`) | Bieżąca długość kolejki żądań |
| :::no-loc text="TLS Handshake Rate"::: (`tls-handshakes-per-second`) | Liczba uzgodnień TLS według interwału aktualizacji |
| :::no-loc text="Total Connections"::: (`total-connections`) | Całkowita liczba połączeń z serwerem sieci Web |
| :::no-loc text="Total TLS Handshakes"::: (`total-tls-handshakes`) | Łączna liczba uzgodnień TLS z serwerem sieci Web |
