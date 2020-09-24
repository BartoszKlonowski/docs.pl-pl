---
title: Wypełnianie zestawu danych z elementu DataAdapter
description: Dowiedz się, jak wypełnić zestaw danych z elementu DataAdapter w ADO.NET, który zapewnia spójny relacyjny model programowania niezależnie od źródła danych.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 3fa0ac7d-e266-4954-bfac-3fbe2f913153
ms.openlocfilehash: ac84af884238b166266d4206802878c1e21169fd
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91177413"
---
# <a name="populating-a-dataset-from-a-dataadapter"></a><span data-ttu-id="2025e-103">Wypełnianie zestawu danych z elementu DataAdapter</span><span class="sxs-lookup"><span data-stu-id="2025e-103">Populating a DataSet from a DataAdapter</span></span>

<span data-ttu-id="2025e-104">ADO.NET <xref:System.Data.DataSet> to reprezentacja danych znajdujących się w pamięci, która zapewnia spójny relacyjny model programowania niezależnie od źródła danych.</span><span class="sxs-lookup"><span data-stu-id="2025e-104">The ADO.NET <xref:System.Data.DataSet> is a memory-resident representation of data that provides a consistent relational programming model independent of the data source.</span></span> <span data-ttu-id="2025e-105">`DataSet`Reprezentuje kompletny zestaw danych, który zawiera tabele, ograniczenia i relacje między tabelami.</span><span class="sxs-lookup"><span data-stu-id="2025e-105">The `DataSet` represents a complete set of data that includes tables, constraints, and relationships among the tables.</span></span> <span data-ttu-id="2025e-106">Ponieważ `DataSet` program jest niezależny od źródła danych, `DataSet` może obejmować dane lokalne do aplikacji oraz dane z wielu źródeł danych.</span><span class="sxs-lookup"><span data-stu-id="2025e-106">Because the `DataSet` is independent of the data source, a `DataSet` can include data local to the application, and data from multiple data sources.</span></span> <span data-ttu-id="2025e-107">Interakcje z istniejącymi źródłami danych są kontrolowane przez program `DataAdapter` .</span><span class="sxs-lookup"><span data-stu-id="2025e-107">Interaction with existing data sources is controlled through the `DataAdapter`.</span></span>  
  
 <span data-ttu-id="2025e-108">`SelectCommand`Właściwość `DataAdapter` jest `Command` obiektem, który pobiera dane ze źródła danych.</span><span class="sxs-lookup"><span data-stu-id="2025e-108">The `SelectCommand` property of the `DataAdapter` is a `Command` object that retrieves data from the data source.</span></span> <span data-ttu-id="2025e-109">`InsertCommand`Właściwości, `UpdateCommand` i `DeleteCommand` `DataAdapter` są obiektami, `Command` które zarządzają aktualizacjami danych w źródle danych, w zależności od zmian wprowadzonych w danych w `DataSet` .</span><span class="sxs-lookup"><span data-stu-id="2025e-109">The `InsertCommand`, `UpdateCommand`, and `DeleteCommand` properties of the `DataAdapter` are `Command` objects that manage updates to the data in the data source according to modifications made to the data in the `DataSet`.</span></span> <span data-ttu-id="2025e-110">Te właściwości są szczegółowo omówione w temacie [Aktualizowanie źródeł danych za pomocą adapterów](updating-data-sources-with-dataadapters.md).</span><span class="sxs-lookup"><span data-stu-id="2025e-110">These properties are covered in more detail in [Updating Data Sources with DataAdapters](updating-data-sources-with-dataadapters.md).</span></span>  
  
 <span data-ttu-id="2025e-111">`Fill`Metoda `DataAdapter` jest używana do wypełniania `DataSet` wynikami `SelectCommand` `DataAdapter` .</span><span class="sxs-lookup"><span data-stu-id="2025e-111">The `Fill` method of the `DataAdapter` is used to populate a `DataSet` with the results of the `SelectCommand` of the `DataAdapter`.</span></span> <span data-ttu-id="2025e-112">`Fill` przyjmuje jako argumenty `DataSet` , które mają być wypełnione, a `DataTable` obiekt lub nazwę `DataTable` do wypełnienia wierszami zwracanymi z `SelectCommand` .</span><span class="sxs-lookup"><span data-stu-id="2025e-112">`Fill` takes as its arguments a `DataSet` to be populated, and a `DataTable` object, or the name of the `DataTable` to be filled with the rows returned from the `SelectCommand`.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="2025e-113">`DataAdapter`Pobieranie całej tabeli trwa przy użyciu programu, zwłaszcza jeśli w tabeli znajduje się wiele wierszy.</span><span class="sxs-lookup"><span data-stu-id="2025e-113">Using the `DataAdapter` to retrieve all of a table takes time, especially if there are many rows in the table.</span></span> <span data-ttu-id="2025e-114">Dzieje się tak dlatego, że dostęp do bazy danych, lokalizowanie i przetwarzanie danych, a następnie Transferowanie danych do klienta odbywa się czasochłonnie.</span><span class="sxs-lookup"><span data-stu-id="2025e-114">This is because accessing the database, locating and processing the data, and then transferring the data to the client is time-consuming.</span></span> <span data-ttu-id="2025e-115">Przeciągnięcie całej tabeli do klienta spowoduje również zablokowanie wszystkich wierszy na serwerze.</span><span class="sxs-lookup"><span data-stu-id="2025e-115">Pulling all of the table to the client also locks all of the rows on the server.</span></span> <span data-ttu-id="2025e-116">Aby zwiększyć wydajność, można użyć klauzuli, `WHERE` aby znacznie zmniejszyć liczbę wierszy zwracanych do klienta.</span><span class="sxs-lookup"><span data-stu-id="2025e-116">To improve performance, you can use the `WHERE` clause to greatly reduce the number of rows returned to the client.</span></span> <span data-ttu-id="2025e-117">Możesz również zmniejszyć ilość danych zwracanych do klienta, tylko jawnie wymieniając wymagane kolumny w `SELECT` instrukcji.</span><span class="sxs-lookup"><span data-stu-id="2025e-117">You can also reduce the amount of data returned to the client by only explicitly listing required columns in the `SELECT` statement.</span></span> <span data-ttu-id="2025e-118">Innym dobrym rozwiązaniem jest pobranie wierszy w partiach (takich jak kilka setek wierszy w danym momencie) i pobranie kolejnej partii, gdy klient zostanie zakończony przy użyciu bieżącej partii.</span><span class="sxs-lookup"><span data-stu-id="2025e-118">Another good workaround is to retrieve the rows in batches (such as several hundred rows at a time) and only retrieve the next batch when the client is finished with the current batch.</span></span>  
  
 <span data-ttu-id="2025e-119">`Fill`Metoda używa `DataReader` obiektu niejawnie do zwracania nazw kolumn i typów, które są używane do tworzenia tabel w `DataSet` , i danych do wypełniania wierszy tabel w `DataSet` .</span><span class="sxs-lookup"><span data-stu-id="2025e-119">The `Fill` method uses the `DataReader` object implicitly to return the column names and types that are used to create the tables in the `DataSet`, and the data to populate the rows of the tables in the `DataSet`.</span></span> <span data-ttu-id="2025e-120">Tabele i kolumny są tworzone tylko wtedy, gdy jeszcze nie istnieją; w przeciwnym razie `Fill` stosuje istniejący `DataSet` schemat.</span><span class="sxs-lookup"><span data-stu-id="2025e-120">Tables and columns are only created if they do not already exist; otherwise `Fill` uses the existing `DataSet` schema.</span></span> <span data-ttu-id="2025e-121">Typy kolumn są tworzone jako typy .NET Framework zgodnie z tabelami w [mapowaniu typu danych w ADO.NET](data-type-mappings-in-ado-net.md).</span><span class="sxs-lookup"><span data-stu-id="2025e-121">Column types are created as .NET Framework types according to the tables in [Data Type Mappings in ADO.NET](data-type-mappings-in-ado-net.md).</span></span> <span data-ttu-id="2025e-122">Klucze podstawowe nie są tworzone, chyba że istnieją w źródle danych i `DataAdapter` **.**`MissingSchemaAction`</span><span class="sxs-lookup"><span data-stu-id="2025e-122">Primary keys are not created unless they exist in the data source and `DataAdapter`**.**`MissingSchemaAction`</span></span> <span data-ttu-id="2025e-123">jest ustawiona na `MissingSchemaAction` **.** `AddWithKey` .</span><span class="sxs-lookup"><span data-stu-id="2025e-123">is set to `MissingSchemaAction`**.**`AddWithKey`.</span></span> <span data-ttu-id="2025e-124">Jeśli `Fill` okaże się, że klucz podstawowy istnieje dla tabeli, spowoduje to zastąpienie danych w danych z `DataSet` danymi ze źródła danych dla wierszy, w których wartości kolumny klucza podstawowego są zgodne z wierszami zwróconymi ze źródła danych.</span><span class="sxs-lookup"><span data-stu-id="2025e-124">If `Fill` finds that a primary key exists for a table, it will overwrite data in the `DataSet` with data from the data source for rows where the primary key column values match those of the row returned from the data source.</span></span> <span data-ttu-id="2025e-125">Jeśli klucz podstawowy nie zostanie znaleziony, dane są dołączane do tabel w `DataSet` .</span><span class="sxs-lookup"><span data-stu-id="2025e-125">If no primary key is found, the data is appended to the tables in the `DataSet`.</span></span> <span data-ttu-id="2025e-126">`Fill` używa wszelkich mapowań, które mogą istnieć podczas wypełniania `DataSet` (zobacz [mapowania DataAdapter DataTable i DataColumn](dataadapter-datatable-and-datacolumn-mappings.md)).</span><span class="sxs-lookup"><span data-stu-id="2025e-126">`Fill` uses any mappings that may exist when you populate the `DataSet` (see [DataAdapter DataTable and DataColumn Mappings](dataadapter-datatable-and-datacolumn-mappings.md)).</span></span>  
  
> [!NOTE]
> <span data-ttu-id="2025e-127">Jeśli `SelectCommand` zwraca wyniki sprzężenia zewnętrznego, `DataAdapter` obiekt nie ustawia `PrimaryKey` wartości wynikowej `DataTable` .</span><span class="sxs-lookup"><span data-stu-id="2025e-127">If the `SelectCommand` returns the results of an OUTER JOIN, the `DataAdapter` does not set a `PrimaryKey` value for the resulting `DataTable`.</span></span> <span data-ttu-id="2025e-128">Należy zdefiniować siebie, `PrimaryKey` Aby upewnić się, że zduplikowane wiersze są poprawnie rozpoznawane.</span><span class="sxs-lookup"><span data-stu-id="2025e-128">You must define the `PrimaryKey` yourself to make sure that duplicate rows are resolved correctly.</span></span> <span data-ttu-id="2025e-129">Aby uzyskać więcej informacji, zobacz [Definiowanie kluczy podstawowych](./dataset-datatable-dataview/defining-primary-keys.md).</span><span class="sxs-lookup"><span data-stu-id="2025e-129">For more information, see [Defining Primary Keys](./dataset-datatable-dataview/defining-primary-keys.md).</span></span>  
  
 <span data-ttu-id="2025e-130">Poniższy przykład kodu tworzy wystąpienie <xref:System.Data.SqlClient.SqlDataAdapter> , które używa <xref:System.Data.SqlClient.SqlConnection> do `Northwind` bazy danych Microsoft SQL Server i wypełnia <xref:System.Data.DataTable> `DataSet` listę klientów w a.</span><span class="sxs-lookup"><span data-stu-id="2025e-130">The following code example creates an instance of a <xref:System.Data.SqlClient.SqlDataAdapter> that uses a <xref:System.Data.SqlClient.SqlConnection> to the Microsoft SQL Server `Northwind` database and populates a <xref:System.Data.DataTable> in a `DataSet` with the list of customers.</span></span> <span data-ttu-id="2025e-131">Instrukcja SQL i <xref:System.Data.SqlClient.SqlConnection> argumenty przekazane do <xref:System.Data.SqlClient.SqlDataAdapter> konstruktora są używane do tworzenia <xref:System.Data.SqlClient.SqlDataAdapter.SelectCommand%2A> właściwości <xref:System.Data.SqlClient.SqlDataAdapter> .</span><span class="sxs-lookup"><span data-stu-id="2025e-131">The SQL statement and <xref:System.Data.SqlClient.SqlConnection> arguments passed to the <xref:System.Data.SqlClient.SqlDataAdapter> constructor are used to create the <xref:System.Data.SqlClient.SqlDataAdapter.SelectCommand%2A> property of the <xref:System.Data.SqlClient.SqlDataAdapter>.</span></span>  
  
## <a name="example"></a><span data-ttu-id="2025e-132">Przykład</span><span class="sxs-lookup"><span data-stu-id="2025e-132">Example</span></span>  
  
```vb  
' Assumes that connection is a valid SqlConnection object.  
Dim queryString As String = _  
  "SELECT CustomerID, CompanyName FROM dbo.Customers"  
Dim adapter As SqlDataAdapter = New SqlDataAdapter( _  
  queryString, connection)  
  
Dim customers As DataSet = New DataSet  
adapter.Fill(customers, "Customers")  
```  
  
```csharp  
// Assumes that connection is a valid SqlConnection object.  
string queryString =
  "SELECT CustomerID, CompanyName FROM dbo.Customers";  
SqlDataAdapter adapter = new SqlDataAdapter(queryString, connection);  
  
DataSet customers = new DataSet();  
adapter.Fill(customers, "Customers");  
```  
  
> [!NOTE]
> <span data-ttu-id="2025e-133">Kod przedstawiony w tym przykładzie nie jest jawnie otwarty i zamknięty `Connection` .</span><span class="sxs-lookup"><span data-stu-id="2025e-133">The code shown in this example does not explicitly open and close the `Connection`.</span></span> <span data-ttu-id="2025e-134">`Fill`Metoda niejawnie otwiera `Connection` , czy `DataAdapter` jest używana, jeśli stwierdzi, że połączenie nie jest jeszcze otwarte.</span><span class="sxs-lookup"><span data-stu-id="2025e-134">The `Fill` method implicitly opens the `Connection` that the `DataAdapter` is using if it finds that the connection is not already open.</span></span> <span data-ttu-id="2025e-135">Jeśli `Fill` połączenie zostało otwarte, zamyka również połączenie po `Fill` zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="2025e-135">If `Fill` opened the connection, it also closes the connection when `Fill` is finished.</span></span> <span data-ttu-id="2025e-136">Może to uprościć kod, gdy zajmujesz się jedną operacją, taką jak `Fill` lub `Update` .</span><span class="sxs-lookup"><span data-stu-id="2025e-136">This can simplify your code when you deal with a single operation such as a `Fill` or an `Update`.</span></span> <span data-ttu-id="2025e-137">Jednak w przypadku wykonywania wielu operacji, które wymagają otwartego połączenia, można zwiększyć wydajność aplikacji, jawnie wywołując `Open` metodę `Connection` , wykonując operacje względem źródła danych, a następnie wywołując `Close` metodę `Connection` .</span><span class="sxs-lookup"><span data-stu-id="2025e-137">However, if you are performing multiple operations that require an open connection, you can improve the performance of your application by explicitly calling the `Open` method of the `Connection`, performing the operations against the data source, and then calling the `Close` method of the `Connection`.</span></span> <span data-ttu-id="2025e-138">Aby zwolnić zasoby używane przez inne aplikacje klienckie, należy podjąć próbę zablokowania połączenia ze źródłem danych.</span><span class="sxs-lookup"><span data-stu-id="2025e-138">You should try to keep connections to the data source open as briefly as possible to free resources for use by other client applications.</span></span>  
  
## <a name="multiple-result-sets"></a><span data-ttu-id="2025e-139">Wiele zestawów wyników</span><span class="sxs-lookup"><span data-stu-id="2025e-139">Multiple Result Sets</span></span>  

 <span data-ttu-id="2025e-140">Jeśli `DataAdapter` napotkają wiele zestawów wyników, tworzy wiele tabel w `DataSet` .</span><span class="sxs-lookup"><span data-stu-id="2025e-140">If the `DataAdapter` encounters multiple result sets, it creates multiple tables in the `DataSet`.</span></span> <span data-ttu-id="2025e-141">Tabele uzyskują przyrostową domyślną nazwę tabeli*N*, zaczynając od "Table" dla TABLE0.</span><span class="sxs-lookup"><span data-stu-id="2025e-141">The tables are given an incremental default name of Table*N*, starting with "Table" for Table0.</span></span> <span data-ttu-id="2025e-142">Jeśli nazwa tabeli jest przenoszona jako argument do `Fill` metody, tabele uzyskują przyrostową domyślną nazwę tabeliname*N*, rozpoczynając od "TableName" dla TableName0.</span><span class="sxs-lookup"><span data-stu-id="2025e-142">If a table name is passed as an argument to the `Fill` method, the tables are given an incremental default name of TableName*N*, starting with "TableName" for TableName0.</span></span>  
  
## <a name="populating-a-dataset-from-multiple-dataadapters"></a><span data-ttu-id="2025e-143">Wypełnianie zestawu danych z wielu kart DataAdapters</span><span class="sxs-lookup"><span data-stu-id="2025e-143">Populating a DataSet from Multiple DataAdapters</span></span>  

 <span data-ttu-id="2025e-144">Dowolna liczba `DataAdapter` obiektów może być używana z `DataSet` .</span><span class="sxs-lookup"><span data-stu-id="2025e-144">Any number of `DataAdapter` objects can be used with a `DataSet`.</span></span> <span data-ttu-id="2025e-145">Każdy `DataAdapter` z nich może służyć do wypełnienia jednego lub większej liczby `DataTable` obiektów i rozwiązania aktualizacji z powrotem do odpowiedniego źródła danych.</span><span class="sxs-lookup"><span data-stu-id="2025e-145">Each `DataAdapter` can be used to fill one or more `DataTable` objects and resolve updates back to the relevant data source.</span></span> <span data-ttu-id="2025e-146">`DataRelation` i `Constraint` obiekty można dodać do `DataSet` lokalnego, co umożliwia powiązanie danych z niepodobnymi źródłami danych.</span><span class="sxs-lookup"><span data-stu-id="2025e-146">`DataRelation` and `Constraint` objects can be added to the `DataSet` locally, which enables you to relate data from dissimilar data sources.</span></span> <span data-ttu-id="2025e-147">Na przykład `DataSet` może zawierać dane z Microsoft SQL Server bazy danych, bazy danych IBM DB2 uwidocznionej za pośrednictwem OLE DB i źródła danych, które przesyła strumieniowo XML.</span><span class="sxs-lookup"><span data-stu-id="2025e-147">For example, a `DataSet` can contain data from a Microsoft SQL Server database, an IBM DB2 database exposed through OLE DB, and a data source that streams XML.</span></span> <span data-ttu-id="2025e-148">Co najmniej jeden `DataAdapter` obiekt może obsługiwać komunikację z każdym źródłem danych.</span><span class="sxs-lookup"><span data-stu-id="2025e-148">One or more `DataAdapter` objects can handle communication to each data source.</span></span>  
  
### <a name="example"></a><span data-ttu-id="2025e-149">Przykład</span><span class="sxs-lookup"><span data-stu-id="2025e-149">Example</span></span>  

 <span data-ttu-id="2025e-150">Poniższy przykład kodu wypełnia listę klientów z `Northwind` bazy danych w Microsoft SQL Server i listę zamówień z `Northwind` bazy danych przechowywanej w programie Microsoft Access 2000.</span><span class="sxs-lookup"><span data-stu-id="2025e-150">The following code example populates a list of customers from the `Northwind` database on Microsoft SQL Server, and a list of orders from the `Northwind` database stored in Microsoft Access 2000.</span></span> <span data-ttu-id="2025e-151">Wypełnione tabele są powiązane z `DataRelation` , a lista klientów jest następnie wyświetlana wraz z zamówieniami dla tego klienta.</span><span class="sxs-lookup"><span data-stu-id="2025e-151">The filled tables are related with a `DataRelation`, and the list of customers is then displayed with the orders for that customer.</span></span> <span data-ttu-id="2025e-152">Aby uzyskać więcej informacji na temat `DataRelation` obiektów, zobacz [Dodawanie relacji](./dataset-datatable-dataview/adding-datarelations.md) danych i [nawigowanie po relacjach](./dataset-datatable-dataview/navigating-datarelations.md)danych.</span><span class="sxs-lookup"><span data-stu-id="2025e-152">For more information about `DataRelation` objects, see [Adding DataRelations](./dataset-datatable-dataview/adding-datarelations.md) and [Navigating DataRelations](./dataset-datatable-dataview/navigating-datarelations.md).</span></span>  
  
```vb  
' Assumes that customerConnection is a valid SqlConnection object.  
' Assumes that orderConnection is a valid OleDbConnection object.  
Dim custAdapter As SqlDataAdapter = New SqlDataAdapter( _  
  "SELECT * FROM dbo.Customers", customerConnection)  
  
Dim ordAdapter As OleDbDataAdapter = New OleDbDataAdapter( _  
  "SELECT * FROM Orders", orderConnection)  
  
Dim customerOrders As DataSet = New DataSet()  
custAdapter.Fill(customerOrders, "Customers")  
ordAdapter.Fill(customerOrders, "Orders")  
  
Dim relation As DataRelation = _  
  customerOrders.Relations.Add("CustOrders", _  
  customerOrders.Tables("Customers").Columns("CustomerID"), _
  customerOrders.Tables("Orders").Columns("CustomerID"))  
  
Dim pRow, cRow As DataRow  
For Each pRow In customerOrders.Tables("Customers").Rows  
  Console.WriteLine(pRow("CustomerID").ToString())  
  
  For Each cRow In pRow.GetChildRows(relation)  
    Console.WriteLine(vbTab & cRow("OrderID").ToString())  
  Next  
Next  
```  
  
```csharp  
// Assumes that customerConnection is a valid SqlConnection object.  
// Assumes that orderConnection is a valid OleDbConnection object.  
SqlDataAdapter custAdapter = new SqlDataAdapter(  
  "SELECT * FROM dbo.Customers", customerConnection);  
OleDbDataAdapter ordAdapter = new OleDbDataAdapter(  
  "SELECT * FROM Orders", orderConnection);  
  
DataSet customerOrders = new DataSet();  
  
custAdapter.Fill(customerOrders, "Customers");  
ordAdapter.Fill(customerOrders, "Orders");  
  
DataRelation relation = customerOrders.Relations.Add("CustOrders",  
  customerOrders.Tables["Customers"].Columns["CustomerID"],  
  customerOrders.Tables["Orders"].Columns["CustomerID"]);  
  
foreach (DataRow pRow in customerOrders.Tables["Customers"].Rows)  
{  
  Console.WriteLine(pRow["CustomerID"]);  
   foreach (DataRow cRow in pRow.GetChildRows(relation))  
    Console.WriteLine("\t" + cRow["OrderID"]);  
}  
```  
  
## <a name="sql-server-decimal-type"></a><span data-ttu-id="2025e-153">SQL Server Typ dziesiętny</span><span class="sxs-lookup"><span data-stu-id="2025e-153">SQL Server Decimal Type</span></span>  

 <span data-ttu-id="2025e-154">Domyślnie `DataSet` dane są przechowywane przy użyciu .NET Framework typów danych.</span><span class="sxs-lookup"><span data-stu-id="2025e-154">By default, the `DataSet` stores data by using .NET Framework data types.</span></span> <span data-ttu-id="2025e-155">W przypadku większości aplikacji zapewniają one wygodną reprezentację informacji o źródle danych.</span><span class="sxs-lookup"><span data-stu-id="2025e-155">For most applications, these provide a convenient representation of data source information.</span></span> <span data-ttu-id="2025e-156">Jednakże ta reprezentacja może spowodować problem, gdy typ danych w źródle danych jest SQL Server dziesiętny lub numeryczny typ danych.</span><span class="sxs-lookup"><span data-stu-id="2025e-156">However, this representation may cause a problem when the data type in the data source is a SQL Server decimal or numeric data type.</span></span> <span data-ttu-id="2025e-157">`decimal`Typ danych .NET Framework dopuszcza maksymalnie 28 cyfr znaczących, podczas gdy `decimal` typ danych SQL Server umożliwia 38 cyfr znaczących.</span><span class="sxs-lookup"><span data-stu-id="2025e-157">The .NET Framework `decimal` data type allows a maximum of 28 significant digits, whereas the SQL Server `decimal` data type allows 38 significant digits.</span></span> <span data-ttu-id="2025e-158">Jeśli `SqlDataAdapter` podczas operacji decyduje, `Fill` że dokładność `decimal` pola SQL Server jest większa niż 28 znaków, bieżący wiersz nie zostanie dodany do `DataTable` .</span><span class="sxs-lookup"><span data-stu-id="2025e-158">If the `SqlDataAdapter` determines during a `Fill` operation that the precision of a SQL Server `decimal` field is larger than 28 characters, the current row is not added to the `DataTable`.</span></span> <span data-ttu-id="2025e-159">Zamiast tego `FillError` wystąpi zdarzenie, które pozwala określić, czy nastąpi utrata dokładności i odpowiednio reagować.</span><span class="sxs-lookup"><span data-stu-id="2025e-159">Instead the `FillError` event occurs, which enables you to determine whether a loss of precision will occur, and respond appropriately.</span></span> <span data-ttu-id="2025e-160">Aby uzyskać więcej informacji o `FillError` zdarzeniu, zobacz [Obsługa zdarzeń DataAdapter](handling-dataadapter-events.md).</span><span class="sxs-lookup"><span data-stu-id="2025e-160">For more information about the `FillError` event, see [Handling DataAdapter Events](handling-dataadapter-events.md).</span></span> <span data-ttu-id="2025e-161">Aby uzyskać SQL Server `decimal` wartość, można również użyć <xref:System.Data.SqlClient.SqlDataReader> obiektu i wywołać <xref:System.Data.SqlClient.SqlDataReader.GetSqlDecimal%2A> metodę.</span><span class="sxs-lookup"><span data-stu-id="2025e-161">To get the SQL Server `decimal` value, you can also use a <xref:System.Data.SqlClient.SqlDataReader> object and call the <xref:System.Data.SqlClient.SqlDataReader.GetSqlDecimal%2A> method.</span></span>  
  
 <span data-ttu-id="2025e-162">W programie ADO.NET 2,0 wprowadzono rozszerzoną obsługę programu <xref:System.Data.SqlTypes> w programie `DataSet` .</span><span class="sxs-lookup"><span data-stu-id="2025e-162">ADO.NET 2.0 introduced enhanced support for <xref:System.Data.SqlTypes> in the `DataSet`.</span></span> <span data-ttu-id="2025e-163">Aby uzyskać więcej informacji, zobacz [SqlTypes i zestaw danych](./sql/sqltypes-and-the-dataset.md).</span><span class="sxs-lookup"><span data-stu-id="2025e-163">For more information, see [SqlTypes and the DataSet](./sql/sqltypes-and-the-dataset.md).</span></span>  
  
## <a name="ole-db-chapters"></a><span data-ttu-id="2025e-164">Rozdziały OLE DB</span><span class="sxs-lookup"><span data-stu-id="2025e-164">OLE DB Chapters</span></span>  

 <span data-ttu-id="2025e-165">Hierarchiczne zestawy wierszy lub rozdziały (typ OLE DB `DBTYPE_HCHAPTER` , typ ADO `adChapter` ) mogą być używane do wypełniania zawartości `DataSet` .</span><span class="sxs-lookup"><span data-stu-id="2025e-165">Hierarchical rowsets, or chapters (OLE DB type `DBTYPE_HCHAPTER`, ADO type `adChapter`) can be used to fill the contents of a `DataSet`.</span></span> <span data-ttu-id="2025e-166">Gdy <xref:System.Data.OleDb.OleDbDataAdapter> napotkają kolumnę z rozdziałem podczas `Fill` operacji, `DataTable` jest tworzona dla kolumny z rozdziałem, a ta tabela jest wypełniana kolumnami i wierszami z rozdziału.</span><span class="sxs-lookup"><span data-stu-id="2025e-166">When the <xref:System.Data.OleDb.OleDbDataAdapter> encounters a chaptered column during a `Fill` operation, a `DataTable` is created for the chaptered column, and that table is filled with the columns and rows from the chapter.</span></span> <span data-ttu-id="2025e-167">Tabela utworzona dla kolumny z rozdziałem jest nazywana przy użyciu nazwy tabeli nadrzędnej i nazwy kolumny rozdziału w postaci "*ParentTableNameChapteredColumnName*".</span><span class="sxs-lookup"><span data-stu-id="2025e-167">The table created for the chaptered column is named by using both the parent table name and the chaptered column name in the form "*ParentTableNameChapteredColumnName*".</span></span> <span data-ttu-id="2025e-168">Jeśli tabela już istnieje w, `DataSet` która jest zgodna z nazwą kolumny z rozdziałem, bieżąca tabela jest wypełniana danymi rozdziału.</span><span class="sxs-lookup"><span data-stu-id="2025e-168">If a table already exists in the `DataSet` that matches the name of the chaptered column, the current table is filled with the chapter data.</span></span> <span data-ttu-id="2025e-169">Jeśli w istniejącej tabeli nie ma kolumn pasujących do kolumny znalezionej w rozdziale, zostanie dodana nowa kolumna.</span><span class="sxs-lookup"><span data-stu-id="2025e-169">If there is no column in an existing table that matches a column found in the chapter, a new column is added.</span></span>  
  
 <span data-ttu-id="2025e-170">Przed `DataSet` zapełnieniem tabel w obiekcie, które znajdują się w kolumnie z rozdziałem, relacja jest tworzona między tabelami nadrzędnymi i podrzędnymi hierarchicznego zestawu wierszy poprzez dodanie kolumny liczb całkowitych do tabeli nadrzędnej i podrzędnej, ustawienie kolumny nadrzędnej na automatycznie przyrostowe i utworzenie `DataRelation` przy użyciu dodanych kolumn z obu tabel.</span><span class="sxs-lookup"><span data-stu-id="2025e-170">Before the tables in the `DataSet` are filled with the data in the chaptered columns, a relation is created between the parent and child tables of the hierarchical rowset by adding an integer column to both the parent and child table, setting the parent column to auto-increment, and creating a `DataRelation` using the added columns from both tables.</span></span> <span data-ttu-id="2025e-171">Dodana relacja nosi nazwę przy użyciu tabeli nadrzędnej i nazw kolumn rozdziałów w postaci "*ParentTableNameChapterColumnName*".</span><span class="sxs-lookup"><span data-stu-id="2025e-171">The added relation is named by using the parent table and chapter column names in the form "*ParentTableNameChapterColumnName*".</span></span>  
  
 <span data-ttu-id="2025e-172">Zwróć uwagę, że kolumna powiązane istnieje tylko w `DataSet` .</span><span class="sxs-lookup"><span data-stu-id="2025e-172">Note that the related column only exists in the `DataSet`.</span></span> <span data-ttu-id="2025e-173">Kolejne wypełnienia ze źródła danych mogą spowodować dodanie nowych wierszy do tabel zamiast zmian scalanych do istniejących wierszy.</span><span class="sxs-lookup"><span data-stu-id="2025e-173">Subsequent fills from the data source can cause new rows to be added to the tables instead of changes being merged into existing rows.</span></span>  
  
 <span data-ttu-id="2025e-174">Należy również pamiętać, że jeśli używasz `DataAdapter.Fill` przeciążenia, które pobiera `DataTable` , tylko ta tabela zostanie wypełniona.</span><span class="sxs-lookup"><span data-stu-id="2025e-174">Note also that, if you use the `DataAdapter.Fill` overload that takes a `DataTable`, only that table will be filled.</span></span> <span data-ttu-id="2025e-175">Do tabeli zostanie dodana kolumna o podwójnej liczbie całkowitej, ale żadna tabela podrzędna nie zostanie utworzona lub nie zostanie wypełniona, a relacja nie zostanie utworzona.</span><span class="sxs-lookup"><span data-stu-id="2025e-175">An auto-incrementing integer column will still be added to the table, but no child table will be created or filled, and no relation will be created.</span></span>  
  
 <span data-ttu-id="2025e-176">Poniższy przykład używa dostawcy MSDataShape w celu wygenerowania kolumny rozdział zamówień dla każdego klienta na liście klientów.</span><span class="sxs-lookup"><span data-stu-id="2025e-176">The following example uses the MSDataShape Provider to generate a chapter column of orders for each customer in a list of customers.</span></span> <span data-ttu-id="2025e-177">A `DataSet` następnie jest wypełniony danymi.</span><span class="sxs-lookup"><span data-stu-id="2025e-177">A `DataSet` is then filled with the data.</span></span>  
  
```vb  
Using connection As OleDbConnection = New OleDbConnection( _  
  "Provider=MSDataShape;Data Provider=SQLOLEDB;" & _  
  "Data Source=(local);Integrated " & _  
  "Security=SSPI;Initial Catalog=northwind")  
  
Dim adapter As OleDbDataAdapter = New OleDbDataAdapter( _  
  "SHAPE {SELECT CustomerID, CompanyName FROM Customers} " & _  
  "APPEND ({SELECT CustomerID, OrderID FROM Orders} AS Orders " & _  
  "RELATE CustomerID TO CustomerID)", connection)  
  
Dim customers As DataSet = New DataSet()  
  
adapter.Fill(customers, "Customers")  
End Using  
```  
  
```csharp  
using (OleDbConnection connection = new OleDbConnection("Provider=MSDataShape;Data Provider=SQLOLEDB;" +  
  "Data Source=(local);Integrated Security=SSPI;Initial Catalog=northwind"))  
{  
OleDbDataAdapter adapter = new OleDbDataAdapter("SHAPE {SELECT CustomerID, CompanyName FROM Customers} " +  
  "APPEND ({SELECT CustomerID, OrderID FROM Orders} AS Orders " +  
  "RELATE CustomerID TO CustomerID)", connection);  
  
DataSet customers = new DataSet();  
adapter.Fill(customers, "Customers");  
}  
```  
  
 <span data-ttu-id="2025e-178">Po `Fill` zakończeniu operacji `DataSet` zawiera dwie tabele: `Customers` i `CustomersOrders` , gdzie `CustomersOrders` reprezentuje kolumnę z rozdziałem.</span><span class="sxs-lookup"><span data-stu-id="2025e-178">When the `Fill` operation is complete, the `DataSet` contains two tables: `Customers` and `CustomersOrders`, where `CustomersOrders` represents the chaptered column.</span></span> <span data-ttu-id="2025e-179">Dodatkowa kolumna o nazwie `Orders` zostanie dodana do `Customers` tabeli, a dodatkowa kolumna o nazwie `CustomersOrders` zostanie dodana do `CustomersOrders` tabeli.</span><span class="sxs-lookup"><span data-stu-id="2025e-179">An additional column named `Orders` is added to the `Customers` table, and an additional column named `CustomersOrders` is added to the `CustomersOrders` table.</span></span> <span data-ttu-id="2025e-180">`Orders`Kolumna w `Customers` tabeli ma ustawioną funkcję autoprzyrost.</span><span class="sxs-lookup"><span data-stu-id="2025e-180">The `Orders` column in the `Customers` table is set to auto-increment.</span></span> <span data-ttu-id="2025e-181">A `DataRelation` , `CustomersOrders` , jest tworzony przy użyciu kolumn, które zostały dodane do tabel `Customers` jako tabela nadrzędna.</span><span class="sxs-lookup"><span data-stu-id="2025e-181">A `DataRelation`, `CustomersOrders`, is created by using the columns that were added to the tables with `Customers` as the parent table.</span></span> <span data-ttu-id="2025e-182">W poniższych tabelach przedstawiono niektóre przykładowe wyniki.</span><span class="sxs-lookup"><span data-stu-id="2025e-182">The following tables show some sample results.</span></span>  
  
### <a name="tablename-customers"></a><span data-ttu-id="2025e-183">TableName: Customers</span><span class="sxs-lookup"><span data-stu-id="2025e-183">TableName: Customers</span></span>  
  
|<span data-ttu-id="2025e-184">CustomerID</span><span class="sxs-lookup"><span data-stu-id="2025e-184">CustomerID</span></span>|<span data-ttu-id="2025e-185">CompanyName</span><span class="sxs-lookup"><span data-stu-id="2025e-185">CompanyName</span></span>|<span data-ttu-id="2025e-186">Orders (Zamówienia)</span><span class="sxs-lookup"><span data-stu-id="2025e-186">Orders</span></span>|  
|----------------|-----------------|------------|  
|<span data-ttu-id="2025e-187">ALFKI</span><span class="sxs-lookup"><span data-stu-id="2025e-187">ALFKI</span></span>|<span data-ttu-id="2025e-188">Alfreds Futterkiste</span><span class="sxs-lookup"><span data-stu-id="2025e-188">Alfreds Futterkiste</span></span>|<span data-ttu-id="2025e-189">0</span><span class="sxs-lookup"><span data-stu-id="2025e-189">0</span></span>|  
|<span data-ttu-id="2025e-190">ANATR</span><span class="sxs-lookup"><span data-stu-id="2025e-190">ANATR</span></span>|<span data-ttu-id="2025e-191">P Trujillo Emparedados y Helados</span><span class="sxs-lookup"><span data-stu-id="2025e-191">Ana Trujillo Emparedados y helados</span></span>|<span data-ttu-id="2025e-192">1</span><span class="sxs-lookup"><span data-stu-id="2025e-192">1</span></span>|  
  
### <a name="tablename-customersorders"></a><span data-ttu-id="2025e-193">TableName: CustomersOrders</span><span class="sxs-lookup"><span data-stu-id="2025e-193">TableName: CustomersOrders</span></span>  
  
|<span data-ttu-id="2025e-194">CustomerID</span><span class="sxs-lookup"><span data-stu-id="2025e-194">CustomerID</span></span>|<span data-ttu-id="2025e-195">OrderID</span><span class="sxs-lookup"><span data-stu-id="2025e-195">OrderID</span></span>|<span data-ttu-id="2025e-196">CustomersOrders</span><span class="sxs-lookup"><span data-stu-id="2025e-196">CustomersOrders</span></span>|  
|----------------|-------------|---------------------|  
|<span data-ttu-id="2025e-197">ALFKI</span><span class="sxs-lookup"><span data-stu-id="2025e-197">ALFKI</span></span>|<span data-ttu-id="2025e-198">10643</span><span class="sxs-lookup"><span data-stu-id="2025e-198">10643</span></span>|<span data-ttu-id="2025e-199">0</span><span class="sxs-lookup"><span data-stu-id="2025e-199">0</span></span>|  
|<span data-ttu-id="2025e-200">ALFKI</span><span class="sxs-lookup"><span data-stu-id="2025e-200">ALFKI</span></span>|<span data-ttu-id="2025e-201">10692</span><span class="sxs-lookup"><span data-stu-id="2025e-201">10692</span></span>|<span data-ttu-id="2025e-202">0</span><span class="sxs-lookup"><span data-stu-id="2025e-202">0</span></span>|  
|<span data-ttu-id="2025e-203">ANATR</span><span class="sxs-lookup"><span data-stu-id="2025e-203">ANATR</span></span>|<span data-ttu-id="2025e-204">10308</span><span class="sxs-lookup"><span data-stu-id="2025e-204">10308</span></span>|<span data-ttu-id="2025e-205">1</span><span class="sxs-lookup"><span data-stu-id="2025e-205">1</span></span>|  
|<span data-ttu-id="2025e-206">ANATR</span><span class="sxs-lookup"><span data-stu-id="2025e-206">ANATR</span></span>|<span data-ttu-id="2025e-207">10625</span><span class="sxs-lookup"><span data-stu-id="2025e-207">10625</span></span>|<span data-ttu-id="2025e-208">1</span><span class="sxs-lookup"><span data-stu-id="2025e-208">1</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="2025e-209">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="2025e-209">See also</span></span>

- [<span data-ttu-id="2025e-210">Elementy DataAdapter i DataReader</span><span class="sxs-lookup"><span data-stu-id="2025e-210">DataAdapters and DataReaders</span></span>](dataadapters-and-datareaders.md)
- [<span data-ttu-id="2025e-211">Mapowanie typu danych w ADO.NET</span><span class="sxs-lookup"><span data-stu-id="2025e-211">Data Type Mappings in ADO.NET</span></span>](data-type-mappings-in-ado-net.md)
- [<span data-ttu-id="2025e-212">Modyfikowanie danych za pomocą obiektu DbDataAdapter</span><span class="sxs-lookup"><span data-stu-id="2025e-212">Modifying Data with a DbDataAdapter</span></span>](modifying-data-with-a-dbdataadapter.md)
- [<span data-ttu-id="2025e-213">Wiele aktywnych zestawów wyników (MARS)</span><span class="sxs-lookup"><span data-stu-id="2025e-213">Multiple Active Result Sets (MARS)</span></span>](./sql/multiple-active-result-sets-mars.md)
- [<span data-ttu-id="2025e-214">Omówienie ADO.NET</span><span class="sxs-lookup"><span data-stu-id="2025e-214">ADO.NET Overview</span></span>](ado-net-overview.md)
