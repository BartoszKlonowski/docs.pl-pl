---
title: Liczniki wydajności w ADO.NET
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 0b121b71-78f8-4ae2-9aa1-0b2e15778e57
ms.openlocfilehash: 360e4a956aec74b6b71185d6acf2f4071d22e2ae
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/22/2019
ms.locfileid: "69951207"
---
# <a name="performance-counters-in-adonet"></a><span data-ttu-id="68210-102">Liczniki wydajności w ADO.NET</span><span class="sxs-lookup"><span data-stu-id="68210-102">Performance Counters in ADO.NET</span></span>
<span data-ttu-id="68210-103">W ADO.NET 2,0 wprowadzono rozszerzoną obsługę liczników wydajności, które obejmują obsługę <xref:System.Data.SqlClient> obu <xref:System.Data.OracleClient>i.</span><span class="sxs-lookup"><span data-stu-id="68210-103">ADO.NET 2.0 introduced expanded support for performance counters that includes support for both <xref:System.Data.SqlClient> and <xref:System.Data.OracleClient>.</span></span> <span data-ttu-id="68210-104">Liczniki <xref:System.Data.SqlClient> wydajności dostępne w poprzednich wersjach ADO.NET zostały wycofane i zastąpione nowymi licznikami wydajności opisanymi w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="68210-104">The <xref:System.Data.SqlClient> performance counters available in previous versions of ADO.NET have been deprecated and replaced with the new performance counters discussed in this topic.</span></span> <span data-ttu-id="68210-105">Liczników wydajności ADO.NET można użyć do monitorowania stanu aplikacji i zasobów połączenia, z których korzysta.</span><span class="sxs-lookup"><span data-stu-id="68210-105">You can use ADO.NET performance counters to monitor the status of your application and the connection resources that it uses.</span></span> <span data-ttu-id="68210-106">Liczniki wydajności można monitorować przy użyciu Monitora wydajności systemu Windows lub mogą być dostępne programowo przy użyciu <xref:System.Diagnostics.PerformanceCounter> klasy <xref:System.Diagnostics> w przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="68210-106">Performance counters can be monitored by using Windows Performance Monitor or can be accessed programmatically using the <xref:System.Diagnostics.PerformanceCounter> class in the <xref:System.Diagnostics> namespace.</span></span>  
  
## <a name="available-performance-counters"></a><span data-ttu-id="68210-107">Dostępne liczniki wydajności</span><span class="sxs-lookup"><span data-stu-id="68210-107">Available Performance Counters</span></span>  
 <span data-ttu-id="68210-108">Obecnie dostępne są 14 różnych liczników wydajności dla <xref:System.Data.SqlClient> i <xref:System.Data.OracleClient> , zgodnie z opisem w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="68210-108">Currently there are 14 different performance counters available for <xref:System.Data.SqlClient> and <xref:System.Data.OracleClient> as described in the following table.</span></span> <span data-ttu-id="68210-109">Należy zauważyć, że nazwy poszczególnych liczników nie są zlokalizowane w regionalnych wersjach środowiska Microsoft .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="68210-109">Note that the names for the individual counters are not localized across regional versions of the Microsoft .NET Framework.</span></span>  
  
|<span data-ttu-id="68210-110">Licznik wydajności</span><span class="sxs-lookup"><span data-stu-id="68210-110">Performance counter</span></span>|<span data-ttu-id="68210-111">Opis</span><span class="sxs-lookup"><span data-stu-id="68210-111">Description</span></span>|  
|-------------------------|-----------------|  
|`HardConnectsPerSecond`|<span data-ttu-id="68210-112">Liczba połączeń na sekundę wysyłanych do serwera bazy danych.</span><span class="sxs-lookup"><span data-stu-id="68210-112">The number of connections per second that are being made to a database server.</span></span>|  
|`HardDisconnectsPerSecond`|<span data-ttu-id="68210-113">Liczba połączeń na sekundę, które są wprowadzane do serwera bazy danych.</span><span class="sxs-lookup"><span data-stu-id="68210-113">The number of disconnects per second that are being made to a database server.</span></span>|  
|`NumberOfActiveConnectionPoolGroups`|<span data-ttu-id="68210-114">Liczba aktywnych grup puli połączeń, które są aktywne.</span><span class="sxs-lookup"><span data-stu-id="68210-114">The number of unique connection pool groups that are active.</span></span> <span data-ttu-id="68210-115">Ten licznik jest kontrolowany przez liczbę unikatowych parametrów połączenia znalezionych w domenie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="68210-115">This counter is controlled by the number of unique connection strings that are found in the AppDomain.</span></span>|  
|`NumberOfActiveConnectionPools`|<span data-ttu-id="68210-116">Łączna liczba pul połączeń.</span><span class="sxs-lookup"><span data-stu-id="68210-116">The total number of connection pools.</span></span>|  
|`NumberOfActiveConnections`|<span data-ttu-id="68210-117">Liczba aktywnych połączeń, które są obecnie używane.</span><span class="sxs-lookup"><span data-stu-id="68210-117">The number of active connections that are currently in use.</span></span> <span data-ttu-id="68210-118">**Uwaga:**  Ten licznik wydajności nie jest domyślnie włączony.</span><span class="sxs-lookup"><span data-stu-id="68210-118">**Note:**  This performance counter is not enabled by default.</span></span> <span data-ttu-id="68210-119">Aby włączyć ten licznik wydajności, zobacz sekcję [Aktywowanie liczników wyłączonych jako domyślne](#ActivatingOffByDefault).</span><span class="sxs-lookup"><span data-stu-id="68210-119">To enable this performance counter, see [Activating Off-By-Default Counters](#ActivatingOffByDefault).</span></span>|  
|`NumberOfFreeConnections`|<span data-ttu-id="68210-120">Liczba połączeń dostępnych do użycia w pulach połączeń.</span><span class="sxs-lookup"><span data-stu-id="68210-120">The number of connections available for use in the connection pools.</span></span> <span data-ttu-id="68210-121">**Uwaga:**  Ten licznik wydajności nie jest domyślnie włączony.</span><span class="sxs-lookup"><span data-stu-id="68210-121">**Note:**  This performance counter is not enabled by default.</span></span> <span data-ttu-id="68210-122">Aby włączyć ten licznik wydajności, zobacz sekcję [Aktywowanie liczników wyłączonych jako domyślne](#ActivatingOffByDefault).</span><span class="sxs-lookup"><span data-stu-id="68210-122">To enable this performance counter, see [Activating Off-By-Default Counters](#ActivatingOffByDefault).</span></span>|  
|`NumberOfInactiveConnectionPoolGroups`|<span data-ttu-id="68210-123">Liczba unikatowych grup puli połączeń, które są oznaczone do oczyszczenia.</span><span class="sxs-lookup"><span data-stu-id="68210-123">The number of unique connection pool groups that are marked for pruning.</span></span> <span data-ttu-id="68210-124">Ten licznik jest kontrolowany przez liczbę unikatowych parametrów połączenia znalezionych w domenie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="68210-124">This counter is controlled by the number of unique connection strings that are found in the AppDomain.</span></span>|  
|`NumberOfInactiveConnectionPools`|<span data-ttu-id="68210-125">Liczba nieaktywnych pul połączeń, dla których nie wprowadzono żadnych ostatnich działań i które oczekują na ich likwidację.</span><span class="sxs-lookup"><span data-stu-id="68210-125">The number of inactive connection pools that have not had any recent activity and are waiting to be disposed.</span></span>|  
|`NumberOfNonPooledConnections`|<span data-ttu-id="68210-126">Liczba aktywnych połączeń, które nie są w puli.</span><span class="sxs-lookup"><span data-stu-id="68210-126">The number of active connections that are not pooled.</span></span>|  
|`NumberOfPooledConnections`|<span data-ttu-id="68210-127">Liczba aktywnych połączeń, które są zarządzane przez infrastrukturę puli połączeń.</span><span class="sxs-lookup"><span data-stu-id="68210-127">The number of active connections that are being managed by the connection pooling infrastructure.</span></span>|  
|`NumberOfReclaimedConnections`|<span data-ttu-id="68210-128">Liczba połączeń, które zostały ododzyskiwane za pomocą wyrzucania elementów `Close` bezużytecznych, gdzie lub `Dispose` nie zostały wywołane przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="68210-128">The number of connections that have been reclaimed through garbage collection where `Close` or `Dispose` was not called by the application.</span></span> <span data-ttu-id="68210-129">Niejawnie zamykające lub likwidowane połączenia pogarszają wydajność.</span><span class="sxs-lookup"><span data-stu-id="68210-129">Not explicitly closing or disposing connections hurts performance.</span></span>|  
|`NumberOfStasisConnections`|<span data-ttu-id="68210-130">Liczba połączeń aktualnie oczekujących na ukończenie akcji, które są w związku z tym niedostępne do użytku przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="68210-130">The number of connections currently awaiting completion of an action and which are therefore unavailable for use by your application.</span></span>|  
|`SoftConnectsPerSecond`|<span data-ttu-id="68210-131">Liczba aktywnych połączeń pobieranych z puli połączeń.</span><span class="sxs-lookup"><span data-stu-id="68210-131">The number of active connections being pulled from the connection pool.</span></span> <span data-ttu-id="68210-132">**Uwaga:**  Ten licznik wydajności nie jest domyślnie włączony.</span><span class="sxs-lookup"><span data-stu-id="68210-132">**Note:**  This performance counter is not enabled by default.</span></span> <span data-ttu-id="68210-133">Aby włączyć ten licznik wydajności, zobacz sekcję [Aktywowanie liczników wyłączonych jako domyślne](#ActivatingOffByDefault).</span><span class="sxs-lookup"><span data-stu-id="68210-133">To enable this performance counter, see [Activating Off-By-Default Counters](#ActivatingOffByDefault).</span></span>|  
|`SoftDisconnectsPerSecond`|<span data-ttu-id="68210-134">Liczba aktywnych połączeń, które są zwracane do puli połączeń.</span><span class="sxs-lookup"><span data-stu-id="68210-134">The number of active connections that are being returned to the connection pool.</span></span> <span data-ttu-id="68210-135">**Uwaga:**  Ten licznik wydajności nie jest domyślnie włączony.</span><span class="sxs-lookup"><span data-stu-id="68210-135">**Note:**  This performance counter is not enabled by default.</span></span> <span data-ttu-id="68210-136">Aby włączyć ten licznik wydajności, zobacz sekcję [Aktywowanie liczników wyłączonych jako domyślne](#ActivatingOffByDefault).</span><span class="sxs-lookup"><span data-stu-id="68210-136">To enable this performance counter, see [Activating Off-By-Default Counters](#ActivatingOffByDefault).</span></span>|  
  
### <a name="connection-pool-groups-and-connection-pools"></a><span data-ttu-id="68210-137">Grupy puli połączeń i pule połączeń</span><span class="sxs-lookup"><span data-stu-id="68210-137">Connection Pool Groups and Connection Pools</span></span>  
 <span data-ttu-id="68210-138">W przypadku korzystania z uwierzytelniania systemu Windows (zabezpieczenia zintegrowane) należy monitorować oba `NumberOfActiveConnectionPoolGroups` liczniki `NumberOfActiveConnectionPools` wydajności i.</span><span class="sxs-lookup"><span data-stu-id="68210-138">When using Windows Authentication (integrated security), you must monitor both the `NumberOfActiveConnectionPoolGroups` and `NumberOfActiveConnectionPools` performance counters.</span></span> <span data-ttu-id="68210-139">Przyczyną jest to, że grupy puli połączeń mapują na unikatowe parametry połączenia.</span><span class="sxs-lookup"><span data-stu-id="68210-139">The reason is that connection pool groups map to unique connection strings.</span></span> <span data-ttu-id="68210-140">W przypadku użycia zintegrowanego zabezpieczenia pule połączeń mapują się na parametry połączenia i dodatkowo tworzą oddzielne pule dla poszczególnych tożsamości systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="68210-140">When integrated security is used, connection pools map to connection strings and additionally create separate pools for individual Windows identities.</span></span> <span data-ttu-id="68210-141">Na przykład, jeśli Fred i Julie, każdy w ramach tego samego elementu AppDomain, użyj parametrów `"Data Source=MySqlServer;Integrated Security=true"`połączenia, grupy puli połączeń dla parametrów połączenia i są tworzone dwa dodatkowe pule, jeden dla Fred i jeden dla Julie.</span><span class="sxs-lookup"><span data-stu-id="68210-141">For example, if Fred and Julie, each within the same AppDomain, both use the connection string `"Data Source=MySqlServer;Integrated Security=true"`, a connection pool group is created for the connection string, and two additional pools are created, one for Fred and one for Julie.</span></span> <span data-ttu-id="68210-142">Jeśli Jan i Martha używają parametrów połączenia o identycznym logowaniu SQL Server, `"Data Source=MySqlServer;User Id=lowPrivUser;Password=Strong?Password"`to dla tożsamości **lowPrivUser** zostanie utworzona tylko jedna pula.</span><span class="sxs-lookup"><span data-stu-id="68210-142">If John and Martha use a connection string with an identical SQL Server login, `"Data Source=MySqlServer;User Id=lowPrivUser;Password=Strong?Password"`, then only a single pool is created for the **lowPrivUser** identity.</span></span>  
  
<a name="ActivatingOffByDefault"></a>   
### <a name="activating-off-by-default-counters"></a><span data-ttu-id="68210-143">Aktywowanie liczników wyłączonych przez domyślne</span><span class="sxs-lookup"><span data-stu-id="68210-143">Activating Off-By-Default Counters</span></span>  
 <span data-ttu-id="68210-144">Liczniki `NumberOfFreeConnections` `NumberOfActiveConnections`wydajności ,,i`SoftConnectsPerSecond` są domyślnie wyłączone. `SoftDisconnectsPerSecond`</span><span class="sxs-lookup"><span data-stu-id="68210-144">The performance counters `NumberOfFreeConnections`, `NumberOfActiveConnections`, `SoftDisconnectsPerSecond`, and `SoftConnectsPerSecond` are off by default.</span></span> <span data-ttu-id="68210-145">Dodaj następujące informacje do pliku konfiguracji aplikacji, aby je włączyć:</span><span class="sxs-lookup"><span data-stu-id="68210-145">Add the following information to the application's configuration file to enable them:</span></span>  
  
```xml  
<system.diagnostics>  
  <switches>  
    <add name="ConnectionPoolPerformanceCounterDetail"  
         value="4"/>  
  </switches>  
</system.diagnostics>  
```  
  
## <a name="retrieving-performance-counter-values"></a><span data-ttu-id="68210-146">Pobieranie wartości licznika wydajności</span><span class="sxs-lookup"><span data-stu-id="68210-146">Retrieving Performance Counter Values</span></span>  
 <span data-ttu-id="68210-147">W poniższej aplikacji konsolowej pokazano, jak pobrać wartości liczników wydajności w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="68210-147">The following console application shows how to retrieve performance counter values in your application.</span></span> <span data-ttu-id="68210-148">Połączenia muszą być otwarte i aktywne, aby można było zwracać informacje dla wszystkich liczników wydajności ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="68210-148">Connections must be open and active for information to be returned for all of the ADO.NET performance counters.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="68210-149">Ten przykład używa przykładowej bazy danych **AdventureWorks** dołączonej do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="68210-149">This example uses the sample **AdventureWorks** database included with SQL Server.</span></span> <span data-ttu-id="68210-150">Parametry połączenia podane w przykładowym kodzie założono, że baza danych jest zainstalowana i dostępna na komputerze lokalnym z nazwą wystąpienia SqlExpress oraz że utworzono SQL Server logowania zgodne z tymi określonymi w parametrach połączenia.</span><span class="sxs-lookup"><span data-stu-id="68210-150">The connection strings provided in the sample code assume that the database is installed and available on the local computer with an instance name of SqlExpress, and that you have created SQL Server logins that match those supplied in the connection strings.</span></span> <span data-ttu-id="68210-151">Może być konieczne włączenie SQL Server logowania, jeśli serwer jest skonfigurowany przy użyciu domyślnych ustawień zabezpieczeń, które zezwalają na uwierzytelnianie systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="68210-151">You may need to enable SQL Server logins if your server is configured using the default security settings which allow only Windows Authentication.</span></span> <span data-ttu-id="68210-152">Zmodyfikuj parametry połączenia stosownie do potrzeb środowiska.</span><span class="sxs-lookup"><span data-stu-id="68210-152">Modify the connection strings as necessary to suit your environment.</span></span>  
  
### <a name="example"></a><span data-ttu-id="68210-153">Przykład</span><span class="sxs-lookup"><span data-stu-id="68210-153">Example</span></span>  
  
```vb  
Option Explicit On  
Option Strict On  
  
Imports System.Data.SqlClient  
Imports System.Diagnostics  
Imports System.Runtime.InteropServices  
  
Class Program  
  
    Private PerfCounters(9) As PerformanceCounter  
    Private connection As SqlConnection = New SqlConnection  
  
    Public Shared Sub Main()  
        Dim prog As Program = New Program  
        ' Open a connection and create the performance counters.   
        prog.connection.ConnectionString = _  
           GetIntegratedSecurityConnectionString()  
        prog.SetUpPerformanceCounters()  
        Console.WriteLine("Available Performance Counters:")  
  
        ' Create the connections and display the results.  
        prog.CreateConnections()  
        Console.WriteLine("Press Enter to finish.")  
        Console.ReadLine()  
    End Sub  
  
    Private Sub CreateConnections()  
        ' List the Performance counters.  
        WritePerformanceCounters()  
  
        ' Create 4 connections and display counter information.  
        Dim connection1 As SqlConnection = New SqlConnection( _  
           GetIntegratedSecurityConnectionString)  
        connection1.Open()  
        Console.WriteLine("Opened the 1st Connection:")  
        WritePerformanceCounters()  
  
        Dim connection2 As SqlConnection = New SqlConnection( _  
           GetSqlConnectionStringDifferent)  
        connection2.Open()  
        Console.WriteLine("Opened the 2nd Connection:")  
        WritePerformanceCounters()  
  
        Console.WriteLine("Opened the 3rd Connection:")  
        Dim connection3 As SqlConnection = New SqlConnection( _  
           GetSqlConnectionString)  
        connection3.Open()  
        WritePerformanceCounters()  
  
        Dim connection4 As SqlConnection = New SqlConnection( _  
           GetSqlConnectionString)  
        connection4.Open()  
        Console.WriteLine("Opened the 4th Connection:")  
        WritePerformanceCounters()  
  
        connection1.Close()  
        Console.WriteLine("Closed the 1st Connection:")  
        WritePerformanceCounters()  
  
        connection2.Close()  
        Console.WriteLine("Closed the 2nd Connection:")  
        WritePerformanceCounters()  
  
        connection3.Close()  
        Console.WriteLine("Closed the 3rd Connection:")  
        WritePerformanceCounters()  
  
        connection4.Close()  
        Console.WriteLine("Closed the 4th Connection:")  
        WritePerformanceCounters()  
    End Sub  
  
    Private Enum ADO_Net_Performance_Counters  
        NumberOfActiveConnectionPools  
        NumberOfReclaimedConnections  
        HardConnectsPerSecond  
        HardDisconnectsPerSecond  
        NumberOfActiveConnectionPoolGroups  
        NumberOfInactiveConnectionPoolGroups  
        NumberOfInactiveConnectionPools  
        NumberOfNonPooledConnections  
        NumberOfPooledConnections  
        NumberOfStasisConnections  
        ' The following performance counters are more expensive to track.  
        ' Enable ConnectionPoolPerformanceCounterDetail in your config file.  
        '     SoftConnectsPerSecond  
        '     SoftDisconnectsPerSecond  
        '     NumberOfActiveConnections  
        '     NumberOfFreeConnections  
    End Enum  
  
    Private Sub SetUpPerformanceCounters()  
        connection.Close()  
        Me.PerfCounters(9) = New PerformanceCounter()  
  
        Dim instanceName As String = GetInstanceName()  
        Dim apc As Type = GetType(ADO_Net_Performance_Counters)  
        Dim i As Integer = 0  
        Dim s As String = ""  
        For Each s In [Enum].GetNames(apc)  
            Me.PerfCounters(i) = New PerformanceCounter()  
            Me.PerfCounters(i).CategoryName = ".NET Data Provider for SqlServer"  
            Me.PerfCounters(i).CounterName = s  
            Me.PerfCounters(i).InstanceName = instanceName  
            i = (i + 1)  
        Next  
    End Sub  
  
    Private Declare Function GetCurrentProcessId Lib "kernel32.dll" () As Integer  
  
    Private Function GetInstanceName() As String  
        'This works for Winforms apps.   
        Dim instanceName As String = _  
           System.Reflection.Assembly.GetEntryAssembly.GetName.Name  
  
        ' Must replace special characters like (, ), #, /, \\   
        Dim instanceName2 As String = _  
           AppDomain.CurrentDomain.FriendlyName.ToString.Replace("(", "[") _  
           .Replace(")", "]").Replace("#", "_").Replace("/", "_").Replace("\\", "_")  
  
        'For ASP.NET applications your instanceName will be your CurrentDomain's   
        'FriendlyName. Replace the line above that sets the instanceName with this:   
        'instanceName = AppDomain.CurrentDomain.FriendlyName.ToString.Replace("(", "[") _  
        '    .Replace(")", "]").Replace("#", "_").Replace("/", "_").Replace("\\", "_")  
  
        Dim pid As String = GetCurrentProcessId.ToString  
        instanceName = (instanceName + ("[" & (pid & "]")))  
        Console.WriteLine("Instance Name: {0}", instanceName)  
        Console.WriteLine("---------------------------")  
        Return instanceName  
    End Function  
  
    Private Sub WritePerformanceCounters()  
        Console.WriteLine("---------------------------")  
        For Each p As PerformanceCounter In Me.PerfCounters  
            Console.WriteLine("{0} = {1}", p.CounterName, p.NextValue)  
        Next  
        Console.WriteLine("---------------------------")  
    End Sub  
  
    Private Shared Function GetIntegratedSecurityConnectionString() As String  
        ' To avoid storing the connection string in your code,   
        ' you can retrieve it from a configuration file.   
        Return ("Data Source=.\SqlExpress;Integrated Security=True;" &   
          "Initial Catalog=AdventureWorks")  
    End Function  
  
    Private Shared Function GetSqlConnectionString() As String  
        ' To avoid storing the connection string in your code,   
        ' you can retrieve it from a configuration file.   
        Return ("Data Source=.\SqlExpress;User Id=LowPriv;Password=Data!05;" &   
          "Initial Catalog=AdventureWorks")  
    End Function  
  
    Private Shared Function GetSqlConnectionStringDifferent() As String  
        ' To avoid storing the connection string in your code,   
        ' you can retrieve it from a configuration file.   
        Return ("Initial Catalog=AdventureWorks;Data Source=.\SqlExpress;" & _  
          "User Id=LowPriv;Password=Data!05;")  
    End Function  
End Class  
```  

```csharp  
using System;  
using System.Data.SqlClient;  
using System.Diagnostics;  
using System.Runtime.InteropServices;  
  
class Program  
{  
    PerformanceCounter[] PerfCounters = new PerformanceCounter[10];  
    SqlConnection connection = new SqlConnection();  
  
    static void Main()  
    {  
        Program prog = new Program();  
        // Open a connection and create the performance counters.  
        prog.connection.ConnectionString =  
           GetIntegratedSecurityConnectionString();  
        prog.SetUpPerformanceCounters();  
        Console.WriteLine("Available Performance Counters:");  
  
        // Create the connections and display the results.  
        prog.CreateConnections();  
        Console.WriteLine("Press Enter to finish.");  
        Console.ReadLine();  
    }  
  
    private void CreateConnections()  
    {  
        // List the Performance counters.  
        WritePerformanceCounters();  
  
        // Create 4 connections and display counter information.  
        SqlConnection connection1 = new SqlConnection(  
              GetIntegratedSecurityConnectionString());  
        connection1.Open();  
        Console.WriteLine("Opened the 1st Connection:");  
        WritePerformanceCounters();  
  
        SqlConnection connection2 = new SqlConnection(  
              GetSqlConnectionStringDifferent());  
        connection2.Open();  
        Console.WriteLine("Opened the 2nd Connection:");  
        WritePerformanceCounters();  
  
        SqlConnection connection3 = new SqlConnection(  
              GetSqlConnectionString());  
        connection3.Open();  
        Console.WriteLine("Opened the 3rd Connection:");  
        WritePerformanceCounters();  
  
        SqlConnection connection4 = new SqlConnection(  
              GetSqlConnectionString());  
        connection4.Open();  
        Console.WriteLine("Opened the 4th Connection:");  
        WritePerformanceCounters();  
  
        connection1.Close();  
        Console.WriteLine("Closed the 1st Connection:");  
        WritePerformanceCounters();  
  
        connection2.Close();  
        Console.WriteLine("Closed the 2nd Connection:");  
        WritePerformanceCounters();  
  
        connection3.Close();  
        Console.WriteLine("Closed the 3rd Connection:");  
        WritePerformanceCounters();  
  
        connection4.Close();  
        Console.WriteLine("Closed the 4th Connection:");  
        WritePerformanceCounters();  
    }  
  
    private enum ADO_Net_Performance_Counters  
    {  
        NumberOfActiveConnectionPools,  
        NumberOfReclaimedConnections,  
        HardConnectsPerSecond,  
        HardDisconnectsPerSecond,  
        NumberOfActiveConnectionPoolGroups,  
        NumberOfInactiveConnectionPoolGroups,  
        NumberOfInactiveConnectionPools,  
        NumberOfNonPooledConnections,  
        NumberOfPooledConnections,  
        NumberOfStasisConnections  
        // The following performance counters are more expensive to track.  
        // Enable ConnectionPoolPerformanceCounterDetail in your config file.  
        //     SoftConnectsPerSecond  
        //     SoftDisconnectsPerSecond  
        //     NumberOfActiveConnections  
        //     NumberOfFreeConnections  
    }  
  
    private void SetUpPerformanceCounters()  
    {  
        connection.Close();  
        this.PerfCounters = new PerformanceCounter[10];  
        string instanceName = GetInstanceName();  
        Type apc = typeof(ADO_Net_Performance_Counters);  
        int i = 0;  
        foreach (string s in Enum.GetNames(apc))  
        {  
            this.PerfCounters[i] = new PerformanceCounter();  
            this.PerfCounters[i].CategoryName = ".NET Data Provider for SqlServer";  
            this.PerfCounters[i].CounterName = s;  
            this.PerfCounters[i].InstanceName = instanceName;  
            i++;  
        }  
    }  
  
    [DllImport("kernel32.dll", SetLastError = true)]  
    static extern int GetCurrentProcessId();  
  
    private string GetInstanceName()  
    {  
        //This works for Winforms apps.  
        string instanceName =  
            System.Reflection.Assembly.GetEntryAssembly().GetName().Name;  
  
        // Must replace special characters like (, ), #, /, \\  
        string instanceName2 =  
            AppDomain.CurrentDomain.FriendlyName.ToString().Replace('(', '[')  
            .Replace(')', ']').Replace('#', '_').Replace('/', '_').Replace('\\', '_');  
  
        // For ASP.NET applications your instanceName will be your CurrentDomain's   
        // FriendlyName. Replace the line above that sets the instanceName with this:  
        // instanceName = AppDomain.CurrentDomain.FriendlyName.ToString().Replace('(','[')  
        // .Replace(')',']').Replace('#','_').Replace('/','_').Replace('\\','_');  
  
        string pid = GetCurrentProcessId().ToString();  
        instanceName = instanceName + "[" + pid + "]";  
        Console.WriteLine("Instance Name: {0}", instanceName);  
        Console.WriteLine("---------------------------");  
        return instanceName;  
    }  
  
    private void WritePerformanceCounters()  
    {  
        Console.WriteLine("---------------------------");  
        foreach (PerformanceCounter p in this.PerfCounters)  
        {  
            Console.WriteLine("{0} = {1}", p.CounterName, p.NextValue());  
        }  
        Console.WriteLine("---------------------------");  
    }  
  
    private static string GetIntegratedSecurityConnectionString()  
    {  
        // To avoid storing the connection string in your code,  
        // you can retrieve it from a configuration file.  
        return @"Data Source=.\SqlExpress;Integrated Security=True;" +  
          "Initial Catalog=AdventureWorks";  
    }  
    private static string GetSqlConnectionString()  
    {  
        // To avoid storing the connection string in your code,  
        // you can retrieve it from a configuration file.  
        return @"Data Source=.\SqlExpress;User Id=LowPriv;Password=Data!05;" +  
          "Initial Catalog=AdventureWorks";  
    }  
  
    private static string GetSqlConnectionStringDifferent()  
    {  
        // To avoid storing the connection string in your code,  
        // you can retrieve it from a configuration file.  
        return @"Initial Catalog=AdventureWorks;Data Source=.\SqlExpress;" +  
          "User Id=LowPriv;Password=Data!05;";  
    }  
}  
```  

## <a name="see-also"></a><span data-ttu-id="68210-154">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="68210-154">See also</span></span>

- [<span data-ttu-id="68210-155">Nawiązywanie połączenia ze źródłem danych</span><span class="sxs-lookup"><span data-stu-id="68210-155">Connecting to a Data Source</span></span>](../../../../docs/framework/data/adonet/connecting-to-a-data-source.md)
- [<span data-ttu-id="68210-156">Buforowanie połączenia Oracle, OLE DB i ODBC</span><span class="sxs-lookup"><span data-stu-id="68210-156">OLE DB, ODBC, and Oracle Connection Pooling</span></span>](../../../../docs/framework/data/adonet/ole-db-odbc-and-oracle-connection-pooling.md)
- <span data-ttu-id="68210-157">[Liczniki wydajności dla ASP.NET](https://docs.microsoft.com/previous-versions/aspnet/fxk122b4(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="68210-157">[Performance Counters for ASP.NET](https://docs.microsoft.com/previous-versions/aspnet/fxk122b4(v=vs.100))</span></span>
- [<span data-ttu-id="68210-158">Profilowanie środowiska uruchomieniowego</span><span class="sxs-lookup"><span data-stu-id="68210-158">Runtime Profiling</span></span>](../../../../docs/framework/debug-trace-profile/runtime-profiling.md)
- <span data-ttu-id="68210-159">[Wprowadzenie do monitorowania progów wydajności](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/bd20x32d(v=vs.90))</span><span class="sxs-lookup"><span data-stu-id="68210-159">[Introduction to Monitoring Performance Thresholds](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/bd20x32d(v=vs.90))</span></span>
- [<span data-ttu-id="68210-160">Omówienie ADO.NET</span><span class="sxs-lookup"><span data-stu-id="68210-160">ADO.NET Overview</span></span>](ado-net-overview.md)
