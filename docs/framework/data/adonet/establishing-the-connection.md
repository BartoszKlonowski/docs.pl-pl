---
title: Nawiązywanie połączenia
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 3af512f3-87d9-4005-9e2f-abb1060ff43f
ms.openlocfilehash: bf38475711a193bc69176993154f87d455aefe7d
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91156475"
---
# <a name="establishing-the-connection"></a><span data-ttu-id="ac330-102">Nawiązywanie połączenia</span><span class="sxs-lookup"><span data-stu-id="ac330-102">Establishing the Connection</span></span>

<span data-ttu-id="ac330-103">Aby nawiązać połączenie z Microsoft SQL Server, użyj <xref:System.Data.SqlClient.SqlConnection> obiektu Dostawca danych .NET Framework SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ac330-103">To connect to Microsoft SQL Server, use the <xref:System.Data.SqlClient.SqlConnection> object of the .NET Framework Data Provider for SQL Server.</span></span> <span data-ttu-id="ac330-104">Aby nawiązać połączenie ze źródłem danych OLE DB, użyj <xref:System.Data.OleDb.OleDbConnection> obiektu .NET Framework dostawca danych dla OLE DB.</span><span class="sxs-lookup"><span data-stu-id="ac330-104">To connect to an OLE DB data source, use the <xref:System.Data.OleDb.OleDbConnection> object of the .NET Framework Data Provider for OLE DB.</span></span> <span data-ttu-id="ac330-105">Aby nawiązać połączenie ze źródłem danych ODBC, użyj <xref:System.Data.Odbc.OdbcConnection> obiektu Dostawca danych .NET Framework dla ODBC.</span><span class="sxs-lookup"><span data-stu-id="ac330-105">To connect to an ODBC data source, use the <xref:System.Data.Odbc.OdbcConnection> object of the .NET Framework Data Provider for ODBC.</span></span> <span data-ttu-id="ac330-106">Aby nawiązać połączenie ze źródłem danych Oracle, użyj <xref:System.Data.OracleClient.OracleConnection> obiektu Dostawca danych .NET Framework dla programu Oracle.</span><span class="sxs-lookup"><span data-stu-id="ac330-106">To connect to an Oracle data source, use the <xref:System.Data.OracleClient.OracleConnection> object of the .NET Framework Data Provider for Oracle.</span></span> <span data-ttu-id="ac330-107">Aby bezpiecznie przechowywać i pobierać parametry połączenia, zobacz [Ochrona informacji o połączeniu](protecting-connection-information.md).</span><span class="sxs-lookup"><span data-stu-id="ac330-107">For securely storing and retrieving connection strings, see [Protecting Connection Information](protecting-connection-information.md).</span></span>  
  
## <a name="closing-connections"></a><span data-ttu-id="ac330-108">Zamykanie połączeń</span><span class="sxs-lookup"><span data-stu-id="ac330-108">Closing Connections</span></span>  

 <span data-ttu-id="ac330-109">Zalecane jest, aby zawsze zamykać połączenie po zakończeniu korzystania z niego, aby można było zwrócić połączenie do puli.</span><span class="sxs-lookup"><span data-stu-id="ac330-109">We recommend that you always close the connection when you are finished using it, so that the connection can be returned to the pool.</span></span> <span data-ttu-id="ac330-110">`Using`Blok w Visual Basic lub C# automatycznie usuwa połączenie, gdy kod opuszcza blok, nawet w przypadku nieobsłużonego wyjątku.</span><span class="sxs-lookup"><span data-stu-id="ac330-110">The `Using` block in Visual Basic or C# automatically disposes of the connection when the code exits the block, even in the case of an unhandled exception.</span></span> <span data-ttu-id="ac330-111">Aby uzyskać więcej informacji, zobacz [używanie instrukcji using](../../../csharp/language-reference/keywords/using-statement.md) i [instrukcji using](../../../visual-basic/language-reference/statements/using-statement.md) .</span><span class="sxs-lookup"><span data-stu-id="ac330-111">See [using Statement](../../../csharp/language-reference/keywords/using-statement.md) and [Using Statement](../../../visual-basic/language-reference/statements/using-statement.md) for more information.</span></span>  
  
 <span data-ttu-id="ac330-112">Można również użyć `Close` `Dispose` metod lub obiektu połączenia dla dostawcy, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="ac330-112">You can also use the `Close` or `Dispose` methods of the connection object for the provider that you are using.</span></span> <span data-ttu-id="ac330-113">Połączenia, które nie zostały jawnie zamknięte, mogą nie zostać dodane lub zwrócone do puli.</span><span class="sxs-lookup"><span data-stu-id="ac330-113">Connections that are not explicitly closed might not be added or returned to the pool.</span></span> <span data-ttu-id="ac330-114">Na przykład połączenie, które zostało utracone poza zakresem, ale nie zostało jawnie zamknięte, zostanie zwrócone do puli połączeń tylko wtedy, gdy Osiągnięto maksymalny rozmiar puli, a połączenie jest nadal ważne.</span><span class="sxs-lookup"><span data-stu-id="ac330-114">For example, a connection that has gone out of scope but that has not been explicitly closed will only be returned to the connection pool if the maximum pool size has been reached and the connection is still valid.</span></span> <span data-ttu-id="ac330-115">Aby uzyskać więcej informacji, zobacz [OLE DB, ODBC i pule połączeń Oracle](ole-db-odbc-and-oracle-connection-pooling.md).</span><span class="sxs-lookup"><span data-stu-id="ac330-115">For more information, see [OLE DB, ODBC, and Oracle Connection Pooling](ole-db-odbc-and-oracle-connection-pooling.md).</span></span>  
  
> [!NOTE]
> <span data-ttu-id="ac330-116">Nie należy wywoływać ani nawiązać `Close` `Dispose` **połączenia**, elementu **DataReader**ani innego obiektu zarządzanego w `Finalize` metodzie klasy.</span><span class="sxs-lookup"><span data-stu-id="ac330-116">Do not call `Close` or `Dispose` on a **Connection**, a **DataReader**, or any other managed object in the `Finalize` method of your class.</span></span> <span data-ttu-id="ac330-117">W finalizatorze zwalniane są tylko niezarządzane zasoby, które są własnością klasy bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="ac330-117">In a finalizer, only release unmanaged resources that your class owns directly.</span></span> <span data-ttu-id="ac330-118">Jeśli Klasa nie jest własnością żadnych niezarządzanych zasobów, nie Uwzględniaj `Finalize` metody w definicji klasy.</span><span class="sxs-lookup"><span data-stu-id="ac330-118">If your class does not own any unmanaged resources, do not include a `Finalize` method in your class definition.</span></span> <span data-ttu-id="ac330-119">Aby uzyskać więcej informacji, zobacz [odzyskiwanie pamięci](../../../standard/garbage-collection/index.md).</span><span class="sxs-lookup"><span data-stu-id="ac330-119">For more information, see [Garbage Collection](../../../standard/garbage-collection/index.md).</span></span>  
  
> [!NOTE]
> <span data-ttu-id="ac330-120">Zdarzenia logowania i wylogowywania nie będą zgłaszane na serwerze, gdy połączenie zostanie pobrane z lub zwrócone do puli połączeń, ponieważ połączenie nie jest faktycznie zamknięte, gdy zostanie zwrócone do puli połączeń.</span><span class="sxs-lookup"><span data-stu-id="ac330-120">Login and logout events will not be raised on the server when a connection is fetched from or returned to the connection pool, because the connection is not actually closed when it is returned to the connection pool.</span></span> <span data-ttu-id="ac330-121">Aby uzyskać więcej informacji, zobacz [SQL Servering pooling (ADO.NET)](sql-server-connection-pooling.md).</span><span class="sxs-lookup"><span data-stu-id="ac330-121">For more information, see [SQL Server Connection Pooling (ADO.NET)](sql-server-connection-pooling.md).</span></span>  
  
## <a name="connecting-to-sql-server"></a><span data-ttu-id="ac330-122">Nawiązywanie połączenia z SQL Server</span><span class="sxs-lookup"><span data-stu-id="ac330-122">Connecting to SQL Server</span></span>  

 <span data-ttu-id="ac330-123">Dostawca danych .NET Framework dla SQL Server obsługuje format parametrów połączenia, który jest podobny do formatu parametrów połączenia OLE DB (ADO).</span><span class="sxs-lookup"><span data-stu-id="ac330-123">The .NET Framework Data Provider for SQL Server supports a connection string format that is similar to the OLE DB (ADO) connection string format.</span></span> <span data-ttu-id="ac330-124">W przypadku prawidłowych nazw i wartości formatu ciągu zobacz <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A> Właściwość <xref:System.Data.SqlClient.SqlConnection> obiektu.</span><span class="sxs-lookup"><span data-stu-id="ac330-124">For valid string format names and values, see the <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A> property of the <xref:System.Data.SqlClient.SqlConnection> object.</span></span> <span data-ttu-id="ac330-125">Można również użyć <xref:System.Data.SqlClient.SqlConnectionStringBuilder> klasy do tworzenia składniowo prawidłowych parametrów połączenia w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="ac330-125">You can also use the <xref:System.Data.SqlClient.SqlConnectionStringBuilder> class to create syntactically valid connection strings at run time.</span></span> <span data-ttu-id="ac330-126">Aby uzyskać więcej informacji, zobacz [konstruktory parametrów połączenia](connection-string-builders.md).</span><span class="sxs-lookup"><span data-stu-id="ac330-126">For more information, see [Connection String Builders](connection-string-builders.md).</span></span>  
  
 <span data-ttu-id="ac330-127">Poniższy przykład kodu pokazuje, jak utworzyć i otworzyć połączenie z bazą danych SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ac330-127">The following code example demonstrates how to create and open a connection to a SQL Server database.</span></span>  
  
```vb  
' Assumes connectionString is a valid connection string.  
Using connection As New SqlConnection(connectionString)  
    connection.Open()  
    ' Do work here.  
End Using  
```  
  
```csharp  
// Assumes connectionString is a valid connection string.  
using (SqlConnection connection = new SqlConnection(connectionString))  
{  
    connection.Open();  
    // Do work here.  
}  
```  
  
### <a name="integrated-security-and-aspnet"></a><span data-ttu-id="ac330-128">Zintegrowane zabezpieczenia i ASP.NET</span><span class="sxs-lookup"><span data-stu-id="ac330-128">Integrated Security and ASP.NET</span></span>  

 <span data-ttu-id="ac330-129">SQL Server zintegrowane zabezpieczenia (znane także jako zaufane połączenia) pomagają zapewnić ochronę podczas nawiązywania połączenia z SQL Server, ponieważ nie uwidacznia identyfikatora użytkownika i hasła w parametrach połączenia i jest zalecaną metodą uwierzytelniania połączenia.</span><span class="sxs-lookup"><span data-stu-id="ac330-129">SQL Server integrated security (also known as trusted connections) helps to provide protection when connecting to SQL Server as it does not expose a user ID and password in the connection string and is the recommended method for authenticating a connection.</span></span> <span data-ttu-id="ac330-130">Zabezpieczenia zintegrowane korzystają z bieżącej tożsamości lub tokenu procesu wykonywania.</span><span class="sxs-lookup"><span data-stu-id="ac330-130">Integrated security uses the current security identity, or token, of the executing process.</span></span> <span data-ttu-id="ac330-131">W przypadku aplikacji klasycznych zwykle jest to tożsamość aktualnie zalogowanego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ac330-131">For desktop applications, this is typically the identity of the currently logged-on user.</span></span>  
  
 <span data-ttu-id="ac330-132">Tożsamość zabezpieczeń dla aplikacji ASP.NET można ustawić na jedną z kilku różnych opcji.</span><span class="sxs-lookup"><span data-stu-id="ac330-132">The security identity for ASP.NET applications can be set to one of several different options.</span></span> <span data-ttu-id="ac330-133">Aby lepiej zrozumieć tożsamość zabezpieczeń używaną przez aplikację ASP.NET podczas nawiązywania połączenia z SQL Server, zobacz [personifikacja ASP.NET](/previous-versions/aspnet/xh507fc5(v=vs.100)), [uwierzytelnianie ASP.NET](/previous-versions/aspnet/eeyk640h(v=vs.100))i [instrukcje: dostęp SQL Server przy użyciu zintegrowanych zabezpieczeń systemu Windows](/previous-versions/aspnet/bsz5788z(v=vs.100)).</span><span class="sxs-lookup"><span data-stu-id="ac330-133">To better understand the security identity that an ASP.NET application uses when connecting to SQL Server, see [ASP.NET Impersonation](/previous-versions/aspnet/xh507fc5(v=vs.100)), [ASP.NET Authentication](/previous-versions/aspnet/eeyk640h(v=vs.100)), and [How to: Access SQL Server Using Windows Integrated Security](/previous-versions/aspnet/bsz5788z(v=vs.100)).</span></span>  
  
## <a name="connecting-to-an-ole-db-data-source"></a><span data-ttu-id="ac330-134">Nawiązywanie połączenia ze źródłem danych OLE DB</span><span class="sxs-lookup"><span data-stu-id="ac330-134">Connecting to an OLE DB Data Source</span></span>  

 <span data-ttu-id="ac330-135">Dostawca danych .NET Framework dla OLE DB zapewnia łączność ze źródłami danych ujawnionymi przy użyciu OLE DB (za pośrednictwem SQLOLEDB, dostawcy OLE DB dla SQL Server) przy użyciu obiektu **OleDbConnection** .</span><span class="sxs-lookup"><span data-stu-id="ac330-135">The .NET Framework Data Provider for OLE DB provides connectivity to data sources exposed using OLE DB (through SQLOLEDB, the OLE DB Provider for SQL Server), using the **OleDbConnection** object.</span></span>  
  
 <span data-ttu-id="ac330-136">W przypadku .NET Framework Dostawca danych dla OLE DB format parametrów połączenia jest identyczny z formatem parametrów połączenia używanym w ADO, z następującymi wyjątkami:</span><span class="sxs-lookup"><span data-stu-id="ac330-136">For the .NET Framework Data Provider for OLE DB, the connection string format is identical to the connection string format used in ADO, with the following exceptions:</span></span>  
  
- <span data-ttu-id="ac330-137">Słowo kluczowe **Provider** jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="ac330-137">The **Provider** keyword is required.</span></span>  
  
- <span data-ttu-id="ac330-138">**Adresy URL**, **dostawcy zdalnego**i słowa kluczowe **serwera zdalnego** nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="ac330-138">The **URL**, **Remote Provider**, and **Remote Server** keywords are not supported.</span></span>  
  
 <span data-ttu-id="ac330-139">Aby uzyskać więcej informacji na temat OLE DB parametrów połączenia, zobacz <xref:System.Data.OleDb.OleDbConnection.ConnectionString%2A> temat.</span><span class="sxs-lookup"><span data-stu-id="ac330-139">For more information about OLE DB connection strings, see the <xref:System.Data.OleDb.OleDbConnection.ConnectionString%2A> topic.</span></span> <span data-ttu-id="ac330-140">Można również użyć <xref:System.Data.OleDb.OleDbConnectionStringBuilder> do tworzenia parametrów połączenia w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="ac330-140">You can also use the <xref:System.Data.OleDb.OleDbConnectionStringBuilder> to create connection strings at run time.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="ac330-141">Obiekt **OleDbConnection** nie obsługuje ustawiania ani pobierania właściwości dynamicznych specyficznych dla dostawcy OLE DB.</span><span class="sxs-lookup"><span data-stu-id="ac330-141">The **OleDbConnection** object does not support setting or retrieving dynamic properties specific to an OLE DB provider.</span></span> <span data-ttu-id="ac330-142">Obsługiwane są tylko właściwości, które można przekazywać w parametrach połączenia dla dostawcy OLE DB.</span><span class="sxs-lookup"><span data-stu-id="ac330-142">Only properties that can be passed in the connection string for the OLE DB provider are supported.</span></span>  
  
 <span data-ttu-id="ac330-143">Poniższy przykład kodu demonstruje sposób tworzenia i otwierania połączenia ze źródłem danych OLE DB.</span><span class="sxs-lookup"><span data-stu-id="ac330-143">The following code example demonstrates how to create and open a connection to an OLE DB data source.</span></span>  
  
```vb  
' Assumes connectionString is a valid connection string.  
Using connection As New OleDbConnection(connectionString)  
    connection.Open()  
    ' Do work here.  
End Using  
```  
  
```csharp  
// Assumes connectionString is a valid connection string.  
using (OleDbConnection connection =
  new OleDbConnection(connectionString))  
{  
    connection.Open();  
    // Do work here.  
}  
```  
  
## <a name="do-not-use-universal-data-link-files"></a><span data-ttu-id="ac330-144">Nie używaj plików Universal Data Link</span><span class="sxs-lookup"><span data-stu-id="ac330-144">Do Not Use Universal Data Link Files</span></span>  

 <span data-ttu-id="ac330-145">Możliwe jest podanie informacji o połączeniu dla **OleDbConnection** w pliku Universal Data Link (UDL); należy jednak unikać tego.</span><span class="sxs-lookup"><span data-stu-id="ac330-145">It is possible to supply connection information for an **OleDbConnection** in a Universal Data Link (UDL) file; however you should avoid doing so.</span></span> <span data-ttu-id="ac330-146">Pliki UDL nie są szyfrowane i ujawniają informacje o parametrach połączenia w postaci zwykłego tekstu.</span><span class="sxs-lookup"><span data-stu-id="ac330-146">UDL files are not encrypted, and expose connection string information in clear text.</span></span> <span data-ttu-id="ac330-147">Ponieważ plik UDL jest zewnętrznym zasobem opartym na plikach dla aplikacji, nie może być zabezpieczony przy użyciu .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="ac330-147">Because a UDL file is an external file-based resource to your application, it cannot be secured using the .NET Framework.</span></span>  
  
## <a name="connecting-to-an-odbc-data-source"></a><span data-ttu-id="ac330-148">Nawiązywanie połączenia ze źródłem danych ODBC</span><span class="sxs-lookup"><span data-stu-id="ac330-148">Connecting to an ODBC Data Source</span></span>  

 <span data-ttu-id="ac330-149">Dostawca danych .NET Framework dla ODBC zapewnia łączność ze źródłami danych, które są udostępniane za pomocą ODBC przy użyciu obiektu **OdbcConnection** .</span><span class="sxs-lookup"><span data-stu-id="ac330-149">The .NET Framework Data Provider for ODBC provides connectivity to data sources exposed using ODBC using the **OdbcConnection** object.</span></span>  
  
 <span data-ttu-id="ac330-150">W przypadku .NET Framework Dostawca danych dla ODBC, format parametrów połączenia jest zaprojektowana tak, aby pasował do formatu parametrów połączenia ODBC tak blisko, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="ac330-150">For the .NET Framework Data Provider for ODBC, the connection string format is designed to match the ODBC connection string format as closely as possible.</span></span> <span data-ttu-id="ac330-151">Możesz również podać nazwę źródła danych ODBC (DSN).</span><span class="sxs-lookup"><span data-stu-id="ac330-151">You may also supply an ODBC data source name (DSN).</span></span> <span data-ttu-id="ac330-152">Aby uzyskać więcej szczegółów na temat **OdbcConnection** , zobacz <xref:System.Data.Odbc.OdbcConnection> .</span><span class="sxs-lookup"><span data-stu-id="ac330-152">For more detail on the **OdbcConnection** , see the <xref:System.Data.Odbc.OdbcConnection>.</span></span>  
  
 <span data-ttu-id="ac330-153">Poniższy przykład kodu demonstruje sposób tworzenia i otwierania połączenia ze źródłem danych ODBC.</span><span class="sxs-lookup"><span data-stu-id="ac330-153">The following code example demonstrates how to create and open a connection to an ODBC data source.</span></span>  
  
```vb  
' Assumes connectionString is a valid connection string.  
Using connection As New OdbcConnection(connectionString)  
    connection.Open()  
    ' Do work here.  
End Using  
```  
  
```csharp  
// Assumes connectionString is a valid connection string.  
using (OdbcConnection connection =
  new OdbcConnection(connectionString))  
{  
    connection.Open();  
    // Do work here.  
}  
```  
  
## <a name="connecting-to-an-oracle-data-source"></a><span data-ttu-id="ac330-154">Nawiązywanie połączenia ze źródłem danych Oracle</span><span class="sxs-lookup"><span data-stu-id="ac330-154">Connecting to an Oracle Data Source</span></span>  

 <span data-ttu-id="ac330-155">.NET Framework Dostawca danych dla programu Oracle zapewnia łączność ze źródłami danych Oracle przy użyciu obiektu **OracleConnection** .</span><span class="sxs-lookup"><span data-stu-id="ac330-155">The .NET Framework Data Provider for Oracle provides connectivity to Oracle data sources using the **OracleConnection** object.</span></span>  
  
 <span data-ttu-id="ac330-156">W przypadku .NET Framework Dostawca danych dla programu Oracle format parametrów połączenia jest zaprojektowany tak, aby był zgodny z formatem parametrów połączenia dostawcy OLE DB dla programu Oracle (MSDAORA I).</span><span class="sxs-lookup"><span data-stu-id="ac330-156">For the .NET Framework Data Provider for Oracle, the connection string format is designed to match the OLE DB Provider for Oracle (MSDAORA) connection string format as closely as possible.</span></span> <span data-ttu-id="ac330-157">Aby uzyskać więcej szczegółów na temat **OracleConnection**, zobacz <xref:System.Data.OracleClient.OracleConnection> .</span><span class="sxs-lookup"><span data-stu-id="ac330-157">For more detail on the **OracleConnection**, see the <xref:System.Data.OracleClient.OracleConnection>.</span></span>  
  
 <span data-ttu-id="ac330-158">Poniższy przykład kodu demonstruje sposób tworzenia i otwierania połączenia ze źródłem danych Oracle.</span><span class="sxs-lookup"><span data-stu-id="ac330-158">The following code example demonstrates how to create and open a connection to an Oracle data source.</span></span>  
  
```vb  
' Assumes connectionString is a valid connection string.  
Using connection As New OracleConnection(connectionString)  
    connection.Open()  
    ' Do work here.  
End Using  
```  
  
```csharp  
// Assumes connectionString is a valid connection string.  
using (OracleConnection connection =
  new OracleConnection(connectionString))  
{  
    connection.Open();  
    // Do work here.  
}  
OracleConnection nwindConn = new OracleConnection("Data Source=MyOracleServer;Integrated Security=yes;");  
nwindConn.Open();  
```  
  
## <a name="see-also"></a><span data-ttu-id="ac330-159">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="ac330-159">See also</span></span>

- [<span data-ttu-id="ac330-160">Nawiązywanie połączenia ze źródłem danych</span><span class="sxs-lookup"><span data-stu-id="ac330-160">Connecting to a Data Source</span></span>](connecting-to-a-data-source.md)
- [<span data-ttu-id="ac330-161">Parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="ac330-161">Connection Strings</span></span>](connection-strings.md)
- [<span data-ttu-id="ac330-162">Buforowanie połączenia Oracle, OLE DB i ODBC</span><span class="sxs-lookup"><span data-stu-id="ac330-162">OLE DB, ODBC, and Oracle Connection Pooling</span></span>](ole-db-odbc-and-oracle-connection-pooling.md)
- [<span data-ttu-id="ac330-163">Omówienie ADO.NET</span><span class="sxs-lookup"><span data-stu-id="ac330-163">ADO.NET Overview</span></span>](ado-net-overview.md)
