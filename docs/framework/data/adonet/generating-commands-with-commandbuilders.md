---
title: Generowanie poleceń za pomocą CommandBuilders
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 6e3fb8b5-373b-4f9e-ab03-a22693df8e91
ms.openlocfilehash: d88f5772e038766d49baf8c758c547e6d5667904
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91200722"
---
# <a name="generating-commands-with-commandbuilders"></a>Generowanie poleceń za pomocą CommandBuilders

Gdy `SelectCommand` Właściwość jest określana dynamicznie w czasie wykonywania, na przykład za pomocą narzędzia zapytania pobierającego polecenie tekstowe od użytkownika, nie można określić odpowiedniego `InsertCommand` , `UpdateCommand` lub `DeleteCommand` w czasie projektowania. Jeśli <xref:System.Data.DataTable> mapy lub są generowane na podstawie pojedynczej tabeli bazy danych, można skorzystać z <xref:System.Data.Common.DbCommandBuilder> obiektu, aby automatycznie generować `DeleteCommand` , `InsertCommand` i `UpdateCommand` <xref:System.Data.Common.DbDataAdapter> .  
  
 Minimalnym wymaganiem jest ustawienie `SelectCommand` właściwości w kolejności, w jakiej funkcja automatycznego generowania poleceń będzie działała. Schemat tabeli pobrany przez `SelectCommand` Właściwość określa składnię automatycznie generowanych instrukcji INSERT, Update i DELETE.  
  
 <xref:System.Data.Common.DbCommandBuilder> `SelectCommand` Aby można było zwrócić metadane niezbędne do skonstruowania poleceń INSERT, Update i DELETE SQL, należy wykonać polecenie. W związku z tym konieczna jest dodatkowa podróż do źródła danych, co może utrudnić działanie. Aby osiągnąć optymalną wydajność, należy jawnie określić polecenia zamiast używać <xref:System.Data.Common.DbCommandBuilder> .  
  
 `SelectCommand`Należy również zwrócić co najmniej jeden klucz podstawowy lub unikatową kolumnę. Jeśli nie są obecne, `InvalidOperation` generowany jest wyjątek, a polecenia nie są generowane.  
  
 Gdy jest skojarzona z `DataAdapter` , <xref:System.Data.Common.DbCommandBuilder> automatycznie generuje `InsertCommand` właściwości, `UpdateCommand` i, `DeleteCommand` `DataAdapter` Jeśli są odwołaniami o wartości null. Jeśli `Command` istnieje już dla właściwości, używana jest istniejąca `Command` .  
  
 Widoki bazy danych tworzone przez Sprzęganie dwóch lub więcej tabel nie są traktowane jako jedna tabela bazy danych. W tym wystąpieniu nie można użyć <xref:System.Data.Common.DbCommandBuilder> do automatycznego generowania poleceń. należy jawnie określić polecenia. Aby uzyskać informacje na temat jawnego ustawiania poleceń w celu rozwiązywania aktualizacji z `DataSet` powrotem do źródła danych, zobacz [Aktualizowanie źródeł danych za pomocą kart DataAdapters](updating-data-sources-with-dataadapters.md).  
  
 Możesz chcieć zamapować parametry wyjściowe z powrotem do zaktualizowanego wiersza `DataSet` . Jedno z typowych zadań Pobiera wartość automatycznie wygenerowanego pola tożsamości lub sygnatury czasowej ze źródła danych. <xref:System.Data.Common.DbCommandBuilder>Program nie będzie domyślnie mapować parametrów wyjściowych do kolumn w zaktualizowanym wierszu. W tym wystąpieniu należy jawnie określić polecenie. Aby zapoznać się z przykładem mapowania automatycznie generowanego pola tożsamości z powrotem do kolumny wstawionego wiersza, zobacz [pobieranie tożsamości lub wartości AutoNumber](retrieving-identity-or-autonumber-values.md).  
  
## <a name="rules-for-automatically-generated-commands"></a>Reguły dla automatycznie generowanych poleceń  

 W poniższej tabeli przedstawiono reguły generowania generowanych automatycznie poleceń.  
  
|Polecenie|Reguła|  
|-------------|----------|  
|`InsertCommand`|Wstawia wiersz w źródle danych dla wszystkich wierszy w tabeli z <xref:System.Data.DataRow.RowState%2A> <xref:System.Data.DataRowState.Added> . Wstawia wartości dla wszystkich kolumn, które są aktualizowalne (ale nie kolumn, takich jak tożsamości, wyrażenia lub sygnatury czasowe).|  
|`UpdateCommand`|Aktualizuje wiersze w źródle danych dla wszystkich wierszy w tabeli z `RowState` <xref:System.Data.DataRowState.Modified> . Aktualizuje wartości wszystkich kolumn z wyjątkiem kolumn, które nie są aktualizowalne, takich jak tożsamości lub wyrażenia. Aktualizuje wszystkie wiersze, w których wartości kolumn w źródle danych pasują do wartości kolumn klucza podstawowego w wierszu i gdzie pozostałe kolumny w źródle danych pasują do oryginalnych wartości wiersza. Aby uzyskać więcej informacji, zobacz "optymistyczny model współbieżności dla aktualizacji i usunięć" w dalszej części tego tematu.|  
|`DeleteCommand`|Usuwa wiersze ze źródła danych dla wszystkich wierszy w tabeli z `RowState` <xref:System.Data.DataRowState.Deleted> . Usuwa wszystkie wiersze, w których wartości kolumn pasują do wartości kolumn klucza podstawowego wiersza i gdzie pozostałe kolumny w źródle danych pasują do oryginalnych wartości wiersza. Aby uzyskać więcej informacji, zobacz "optymistyczny model współbieżności dla aktualizacji i usunięć" w dalszej części tego tematu.|  
  
## <a name="optimistic-concurrency-model-for-updates-and-deletes"></a>Optymistyczny model współbieżności dla aktualizacji i usunięć  

 Logika do generowania poleceń automatycznie dla instrukcji UPDATE i DELETE jest oparta na *optymistycznej współbieżności*— to oznacza, że rekordy nie są zablokowane do edycji i mogą być modyfikowane przez innych użytkowników lub procesy w dowolnym momencie. Ponieważ rekord mógł zostać zmodyfikowany po zwróceniu z instrukcji SELECT, ale przed wystawieniem instrukcji UPDATE lub DELETE, automatycznie wygenerowana instrukcja UPDATE lub DELETE zawiera klauzulę WHERE, określając, że wiersz jest aktualizowany tylko wtedy, gdy zawiera wszystkie oryginalne wartości i nie został usunięty ze źródła danych. Dzieje się tak, aby uniknąć zastępowania nowych danych. Gdy automatycznie wygenerowana aktualizacja próbuje zaktualizować wiersz, który został usunięty lub który nie zawiera oryginalnych wartości znalezionych w <xref:System.Data.DataSet> , polecenie nie ma wpływu na żadne rekordy i <xref:System.Data.DBConcurrencyException> zostanie zgłoszone.  
  
 Jeśli chcesz, aby aktualizacje lub usuwanie zostały wykonane niezależnie od oryginalnych wartości, musisz jawnie ustawić `UpdateCommand` dla `DataAdapter` i nie opierać się na automatycznym generowaniu polecenia.  
  
## <a name="limitations-of-automatic-command-generation-logic"></a>Ograniczenia automatycznej logiki generowania poleceń  

 Do automatycznego generowania poleceń mają zastosowanie następujące ograniczenia.  
  
### <a name="unrelated-tables-only"></a>Tylko niepowiązane tabele  

 Logika automatycznego generowania poleceń generuje instrukcje INSERT, UPDATE lub DELETE dla tabel autonomicznych bez uwzględniania jakichkolwiek relacji z innymi tabelami w źródle danych. W związku z tym może wystąpić błąd podczas wywoływania, `Update` Aby przesłać zmiany dla kolumny, która uczestniczy w ograniczeniu klucza obcego w bazie danych. Aby uniknąć tego wyjątku, nie należy używać <xref:System.Data.Common.DbCommandBuilder> do aktualizowania kolumn związanych z ograniczeniem klucza obcego; w zamian jawnie określić instrukcje używane do wykonania operacji.  
  
### <a name="table-and-column-names"></a>Nazwy tabel i kolumn  

 Automatyczna logika generowania poleceń może zakończyć się niepowodzeniem, jeśli nazwy kolumn lub tabel zawierają dowolne znaki specjalne, takie jak spacje, kropki, znaki cudzysłowu lub inne znaki niealfanumeryczne, nawet jeśli są rozdzielone nawiasami. W zależności od dostawcy ustawienie parametrów QuotePrefix i QuoteSuffix może pozwolić logiki generowania na przetwarzanie spacji, ale nie może wyjść ze znaków specjalnych. W pełni kwalifikowane nazwy tabel w postaci *wykazu. Schema. Table* .  
  
## <a name="using-the-commandbuilder-to-automatically-generate-an-sql-statement"></a>Automatyczne generowanie instrukcji SQL przy użyciu CommandBuilder  

 Aby automatycznie generować instrukcje SQL dla elementu `DataAdapter` , należy najpierw ustawić `SelectCommand` Właściwość `DataAdapter` , a następnie utworzyć `CommandBuilder` obiekt i określić jako argument, `DataAdapter` dla którego `CommandBuilder` będą automatycznie generować instrukcje SQL.  
  
```vb  
' Assumes that connection is a valid SqlConnection object
' inside of a Using block.  
Dim adapter As SqlDataAdapter = New SqlDataAdapter( _  
  "SELECT * FROM dbo.Customers", connection)  
Dim builder As SqlCommandBuilder = New SqlCommandBuilder(adapter)  
builder.QuotePrefix = "["  
builder.QuoteSuffix = "]"  
```  
  
```csharp  
// Assumes that connection is a valid SqlConnection object  
// inside of a using block.  
SqlDataAdapter adapter = new SqlDataAdapter(  
  "SELECT * FROM dbo.Customers", connection);  
SqlCommandBuilder builder = new SqlCommandBuilder(adapter);  
builder.QuotePrefix = "[";  
builder.QuoteSuffix = "]";  
```  
  
## <a name="modifying-the-selectcommand"></a>Modyfikowanie elementu SelectCommand  

 W przypadku zmodyfikowania `CommandText` `SelectCommand` automatycznie generowanych poleceń INSERT, Update lub DELETE może wystąpić wyjątek. Jeśli zmodyfikowane `SelectCommand.CommandText` zawiera informacje o schemacie, które są niespójne z `SelectCommand.CommandText` użyciem podczas automatycznego generowania poleceń INSERT, Update lub DELETE, przyszłe wywołania `DataAdapter.Update` metody mogą próbować uzyskać dostęp do kolumn, które nie znajdują się już w bieżącej tabeli, do której odwołuje się `SelectCommand` i zostanie zgłoszony wyjątek.  
  
 Można odświeżyć informacje o schemacie, które są używane przez program `CommandBuilder` do automatycznego generowania poleceń przez wywołanie `RefreshSchema` metody `CommandBuilder` .  
  
 Jeśli chcesz wiedzieć, jakie polecenie zostało automatycznie wygenerowane, możesz uzyskać odwołanie do automatycznie generowanych poleceń przy użyciu `GetInsertCommand` `GetUpdateCommand` metod,, i `GetDeleteCommand` `CommandBuilder` obiektu i sprawdzając `CommandText` Właściwość skojarzonego polecenia.  
  
 Poniższy przykład kodu zapisuje w konsoli polecenie Update, które zostało automatycznie wygenerowane.  
  
```vb
Console.WriteLine(builder.GetUpdateCommand().CommandText)  
```

```csharp
Console.WriteLine(builder.GetUpdateCommand().CommandText);
```
  
 Poniższy przykład odtworzy `Customers` tabelę w `custDS` zestawie danych. Metoda **RefreshSchema** jest wywoływana w celu odświeżenia automatycznie generowanych poleceń przy użyciu tej nowej informacji o kolumnie.  
  
```vb  
' Assumes an open SqlConnection and SqlDataAdapter inside of a Using block.  
adapter.SelectCommand.CommandText = _  
  "SELECT CustomerID, ContactName FROM dbo.Customers"  
builder.RefreshSchema()  
  
custDS.Tables.Remove(custDS.Tables("Customers"))  
adapter.Fill(custDS, "Customers")  
```  
  
```csharp  
// Assumes an open SqlConnection and SqlDataAdapter inside of a using block.  
adapter.SelectCommand.CommandText =
  "SELECT CustomerID, ContactName FROM dbo.Customers";  
builder.RefreshSchema();  
  
custDS.Tables.Remove(custDS.Tables["Customers"]);  
adapter.Fill(custDS, "Customers");  
```  
  
## <a name="see-also"></a>Zobacz też

- [Polecenia i parametry](commands-and-parameters.md)
- [Wykonywanie polecenia](executing-a-command.md)
- [DbConnection, DbCommand i DbException](dbconnection-dbcommand-and-dbexception.md)
- [Omówienie ADO.NET](ado-net-overview.md)
