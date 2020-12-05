---
title: Liczniki wydajności
description: Użyj liczników wydajności ADO.NET do monitorowania stanu aplikacji i zasobów połączeń przy użyciu Monitora wydajności systemu Windows lub programowo.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 0b121b71-78f8-4ae2-9aa1-0b2e15778e57
ms.openlocfilehash: dca259ef6d8a2229349d88a9fcae3298cb8a829c
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2020
ms.locfileid: "96739467"
---
# <a name="performance-counters-in-adonet"></a>Liczniki wydajności w ADO.NET

W ADO.NET 2,0 wprowadzono rozszerzoną obsługę liczników wydajności, które obejmują obsługę obu <xref:System.Data.SqlClient> i <xref:System.Data.OracleClient> . <xref:System.Data.SqlClient>Liczniki wydajności dostępne w poprzednich wersjach ADO.NET zostały wycofane i zastąpione nowymi licznikami wydajności opisanymi w tym temacie. Liczników wydajności ADO.NET można użyć do monitorowania stanu aplikacji i zasobów połączenia, z których korzysta. Liczniki wydajności można monitorować przy użyciu Monitora wydajności systemu Windows lub mogą być dostępne programowo przy użyciu <xref:System.Diagnostics.PerformanceCounter> klasy w <xref:System.Diagnostics> przestrzeni nazw.

## <a name="available-performance-counters"></a>Dostępne liczniki wydajności

 Obecnie dostępne są 14 różnych liczników wydajności dla <xref:System.Data.SqlClient> i <xref:System.Data.OracleClient> , zgodnie z opisem w poniższej tabeli. Należy zauważyć, że nazwy poszczególnych liczników nie są zlokalizowane w regionalnych wersjach środowiska Microsoft .NET Framework.

|Licznik wydajności|Opis|
|-------------------------|-----------------|
|`HardConnectsPerSecond`|Liczba połączeń na sekundę wysyłanych do serwera bazy danych.|
|`HardDisconnectsPerSecond`|Liczba połączeń na sekundę, które są wprowadzane do serwera bazy danych.|
|`NumberOfActiveConnectionPoolGroups`|Liczba aktywnych grup puli połączeń, które są aktywne. Ten licznik jest kontrolowany przez liczbę unikatowych parametrów połączenia znalezionych w domenie aplikacji.|
|`NumberOfActiveConnectionPools`|Łączna liczba pul połączeń.|
|`NumberOfActiveConnections`|Liczba aktywnych połączeń, które są obecnie używane. **Uwaga:**  Ten licznik wydajności nie jest domyślnie włączony. Aby włączyć ten licznik wydajności, zobacz sekcję [Aktywowanie liczników wyłączonych jako domyślne](#ActivatingOffByDefault).|
|`NumberOfFreeConnections`|Liczba połączeń dostępnych do użycia w pulach połączeń. **Uwaga:**  Ten licznik wydajności nie jest domyślnie włączony. Aby włączyć ten licznik wydajności, zobacz sekcję [Aktywowanie liczników wyłączonych jako domyślne](#ActivatingOffByDefault).|
|`NumberOfInactiveConnectionPoolGroups`|Liczba unikatowych grup puli połączeń, które są oznaczone do oczyszczenia. Ten licznik jest kontrolowany przez liczbę unikatowych parametrów połączenia znalezionych w domenie aplikacji.|
|`NumberOfInactiveConnectionPools`|Liczba nieaktywnych pul połączeń, dla których nie wprowadzono żadnych ostatnich działań i które oczekują na ich likwidację.|
|`NumberOfNonPooledConnections`|Liczba aktywnych połączeń, które nie są w puli.|
|`NumberOfPooledConnections`|Liczba aktywnych połączeń, które są zarządzane przez infrastrukturę puli połączeń.|
|`NumberOfReclaimedConnections`|Liczba połączeń, które zostały ododzyskiwane za pomocą wyrzucania elementów bezużytecznych, gdzie `Close` lub `Dispose` nie zostały wywołane przez aplikację. Niejawnie zamykające lub likwidowane połączenia pogarszają wydajność.|
|`NumberOfStasisConnections`|Liczba połączeń aktualnie oczekujących na ukończenie akcji, które są w związku z tym niedostępne do użytku przez aplikację.|
|`SoftConnectsPerSecond`|Liczba aktywnych połączeń pobieranych z puli połączeń. **Uwaga:**  Ten licznik wydajności nie jest domyślnie włączony. Aby włączyć ten licznik wydajności, zobacz sekcję [Aktywowanie liczników wyłączonych jako domyślne](#ActivatingOffByDefault).|
|`SoftDisconnectsPerSecond`|Liczba aktywnych połączeń, które są zwracane do puli połączeń. **Uwaga:**  Ten licznik wydajności nie jest domyślnie włączony. Aby włączyć ten licznik wydajności, zobacz sekcję [Aktywowanie liczników wyłączonych jako domyślne](#ActivatingOffByDefault).|

### <a name="connection-pool-groups-and-connection-pools"></a>Grupy puli połączeń i pule połączeń

 W przypadku korzystania z uwierzytelniania systemu Windows (zabezpieczenia zintegrowane) należy monitorować oba `NumberOfActiveConnectionPoolGroups` `NumberOfActiveConnectionPools` liczniki wydajności i. Przyczyną jest to, że grupy puli połączeń mapują na unikatowe parametry połączenia. W przypadku użycia zintegrowanego zabezpieczenia pule połączeń mapują się na parametry połączenia i dodatkowo tworzą oddzielne pule dla poszczególnych tożsamości systemu Windows. Na przykład, jeśli Fred i Julie, każdy w ramach tego samego elementu AppDomain, użyj parametrów połączenia `"Data Source=MySqlServer;Integrated Security=true"` , grupy puli połączeń dla parametrów połączenia i są tworzone dwa dodatkowe pule, jeden dla Fred i jeden dla Julie. Jeśli Jan i Martha używają parametrów połączenia o identycznym logowaniu SQL Server, to `"Data Source=MySqlServer;User Id=lowPrivUser;Password=[PLACEHOLDER]"` dla tożsamości **lowPrivUser** zostanie utworzona tylko jedna pula.

<a name="ActivatingOffByDefault"></a>

### <a name="activating-off-by-default-counters"></a>Aktywowanie liczników wyłączonych przez domyślne

 Liczniki wydajności `NumberOfFreeConnections` ,, `NumberOfActiveConnections` `SoftDisconnectsPerSecond` i `SoftConnectsPerSecond` są domyślnie wyłączone. Dodaj następujące informacje do pliku konfiguracji aplikacji, aby je włączyć:

```xml
<system.diagnostics>
  <switches>
    <add name="ConnectionPoolPerformanceCounterDetail"
         value="4"/>
  </switches>
</system.diagnostics>
```

## <a name="retrieving-performance-counter-values"></a>Pobieranie wartości licznika wydajności

 W poniższej aplikacji konsolowej pokazano, jak pobrać wartości liczników wydajności w aplikacji. Połączenia muszą być otwarte i aktywne, aby można było zwracać informacje dla wszystkich liczników wydajności ADO.NET.

> [!NOTE]
> Ten przykład używa przykładowej bazy danych **AdventureWorks** dołączonej do SQL Server. Parametry połączenia podane w przykładowym kodzie założono, że baza danych jest zainstalowana i dostępna na komputerze lokalnym z nazwą wystąpienia SqlExpress oraz że utworzono SQL Server logowania zgodne z tymi określonymi w parametrach połączenia. Może być konieczne włączenie SQL Server logowania, jeśli serwer jest skonfigurowany przy użyciu domyślnych ustawień zabezpieczeń, które zezwalają na uwierzytelnianie systemu Windows. Zmodyfikuj parametry połączenia stosownie do potrzeb środowiska.

### <a name="example"></a>Przykład

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
        Return ("Data Source=.\SqlExpress;User Id=LowPriv;Password=[PLACEHOLDER];" &
          "Initial Catalog=AdventureWorks")
    End Function

    Private Shared Function GetSqlConnectionStringDifferent() As String
        ' To avoid storing the connection string in your code,
        ' you can retrieve it from a configuration file.
        Return ("Initial Catalog=AdventureWorks;Data Source=.\SqlExpress;" & _
          "User Id=LowPriv;Password=[PLACEHOLDER];")
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
        return @"Data Source=.\SqlExpress;User Id=LowPriv;Password=[PLACEHOLDER];" +
          "Initial Catalog=AdventureWorks";
    }

    private static string GetSqlConnectionStringDifferent()
    {
        // To avoid storing the connection string in your code,
        // you can retrieve it from a configuration file.
        return @"Initial Catalog=AdventureWorks;Data Source=.\SqlExpress;" +
          "User Id=LowPriv;Password=[PLACEHOLDER];";
    }
}
```

## <a name="see-also"></a>Zobacz także

- [Nawiązywanie połączenia ze źródłem danych](connecting-to-a-data-source.md)
- [Buforowanie połączenia Oracle, OLE DB i ODBC](ole-db-odbc-and-oracle-connection-pooling.md)
- [Liczniki wydajności dla ASP.NET](/previous-versions/aspnet/fxk122b4(v=vs.100))
- [Profilowanie środowiska uruchomieniowego](../../debug-trace-profile/runtime-profiling.md)
- [Wprowadzenie do monitorowania progów wydajności](/previous-versions/visualstudio/visual-studio-2008/bd20x32d(v=vs.90))
- [Omówienie ADO.NET](ado-net-overview.md)
