---
title: Dostawcy danych .NET Framework
description: Dowiedz się, w jaki sposób dostawca danych .NET Framework jest używany do łączenia się z bazą danych, uruchamiania poleceń i pobierania wyników w ADO.NET.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 03a9fc62-2d24-491a-9fe6-d6bdb6dcb131
ms.openlocfilehash: b61fede9144e554ee68f0b41adac36209adb7288
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91177806"
---
# <a name="net-framework-data-providers"></a>Dostawcy danych .NET Framework

Dostawca danych .NET Framework jest używany do łączenia się z bazą danych, wykonywania poleceń i pobierania wyników. Te wyniki są przetwarzane bezpośrednio, umieszczane w, <xref:System.Data.DataSet> aby były udostępniane użytkownikowi w miarę potrzeby, w połączeniu z danymi z wielu źródeł lub zdalnie między warstwami. Dostawcy danych .NET Framework są lekkie, tworząc minimalną warstwę między źródłem danych i kodem, zwiększając wydajność bez ograniczania funkcjonalności.  
  
 Poniższa tabela zawiera listę dostawców danych uwzględnionych w .NET Framework.  
  
|Dostawca danych .NET Framework|Opis|  
|-------------------------------------------------------------------------------|-----------------|  
|Dostawca danych programu .NET Framework dla programu SQL Server|Zapewnia dostęp do danych Microsoft SQL Server. Używa <xref:System.Data.SqlClient> przestrzeni nazw.|  
|.NET Framework Dostawca danych OLE DB|Dla źródeł danych udostępnianych przy użyciu OLE DB. Używa <xref:System.Data.OleDb> przestrzeni nazw.|  
|.NET Framework Dostawca danych dla ODBC|Dla źródeł danych narażonych na korzystanie z ODBC. Używa <xref:System.Data.Odbc> przestrzeni nazw.|  
|.NET Framework Dostawca danych dla programu Oracle|Dla źródeł danych Oracle. .NET Framework Dostawca danych dla programu Oracle obsługuje oprogramowanie klienckie Oracle w wersji 8.1.7 lub nowszej, a następnie używa <xref:System.Data.OracleClient> przestrzeni nazw.|  
|Dostawca EntityClient|Zapewnia dostęp do danych dla aplikacji Entity Data Model (EDM). Używa <xref:System.Data.EntityClient> przestrzeni nazw.|  
|.NET Framework Dostawca danych SQL Server Compact 4,0.|Zapewnia dostęp do danych dla Microsoft SQL Server Compact 4,0. Używa przestrzeni nazw [System. Data. SqlServerCe](/previous-versions/sql/compact/sql-server-compact-4.0/ec4st0e3(v=vs.100)) .|  
  
## <a name="core-objects-of-net-framework-data-providers"></a>Podstawowe obiekty dostawców danych .NET Framework  

 W poniższej tabeli przedstawiono cztery podstawowe obiekty, które tworzą .NET Framework dostawcę danych.  
  
|Obiekt|Opis|  
|------------|-----------------|  
|`Connection`|Ustanawia połączenie z określonym źródłem danych. Klasa bazowa dla wszystkich `Connection` obiektów jest <xref:System.Data.Common.DbConnection> klasą.|  
|`Command`|Wykonuje polecenie względem źródła danych. Uwidacznia `Parameters` i może być wykonywane w zakresie `Transaction` od a do `Connection` . Klasa bazowa dla wszystkich `Command` obiektów jest <xref:System.Data.Common.DbCommand> klasą.|  
|`DataReader`|Odczytuje strumień danych tylko do odczytu z źródła danych. Klasa bazowa dla wszystkich `DataReader` obiektów jest <xref:System.Data.Common.DbDataReader> klasą.|  
|`DataAdapter`|Wypełnia `DataSet` i rozwiązuje aktualizacje ze źródłem danych. Klasa bazowa dla wszystkich `DataAdapter` obiektów jest <xref:System.Data.Common.DbDataAdapter> klasą.|  
  
 Oprócz klas podstawowych wymienionych w tabeli wcześniej w tym dokumencie, dostawca danych .NET Framework również zawiera klasy wymienione w poniższej tabeli.  
  
|Obiekt|Opis|  
|------------|-----------------|  
|`Transaction`|Rejestrowane są polecenia w transakcjach w źródle danych. Klasa bazowa dla wszystkich `Transaction` obiektów jest <xref:System.Data.Common.DbTransaction> klasą. ADO.NET zapewnia również obsługę transakcji przy użyciu klas w <xref:System.Transactions> przestrzeni nazw.|  
|`CommandBuilder`|Obiekt pomocnika, który automatycznie generuje właściwości polecenia `DataAdapter` lub dziedziczy informacje o parametrach z procedury składowanej i wypełnia `Parameters` kolekcję `Command` obiektu. Klasa bazowa dla wszystkich `CommandBuilder` obiektów jest <xref:System.Data.Common.DbCommandBuilder> klasą.|  
|`ConnectionStringBuilder`|Obiekt pomocnika, który zapewnia prosty sposób tworzenia zawartości parametrów połączenia używanych przez obiekty i zarządzania nią `Connection` . Klasa bazowa dla wszystkich `ConnectionStringBuilder` obiektów jest <xref:System.Data.Common.DbConnectionStringBuilder> klasą.|  
|`Parameter`|Definiuje parametry danych wejściowych, wyjściowych i wartości zwracanych dla poleceń i procedur składowanych. Klasa bazowa dla wszystkich `Parameter` obiektów jest <xref:System.Data.Common.DbParameter> klasą.|  
|`Exception`|Zwracany w przypadku napotkania błędu w źródle danych. W przypadku błędu na kliencie .NET Framework dostawcy danych zgłaszają wyjątek .NET Framework. Klasa bazowa dla wszystkich `Exception` obiektów jest <xref:System.Data.Common.DbException> klasą.|  
|`Error`|Ujawnia informacje z ostrzeżenia lub błędu zwróconego przez źródło danych.|  
|`ClientPermission`|Dostępne dla atrybutów zabezpieczeń dostępu kodu dostawcy danych .NET Framework. Klasa bazowa dla wszystkich `ClientPermission` obiektów jest <xref:System.Data.Common.DBDataPermission> klasą.|  
  
## <a name="net-framework-data-provider-for-sql-server-sqlclient"></a>.NET Framework Dostawca danych SQL Server (SqlClient)  

 Dostawca danych .NET Framework dla SQL Server (SqlClient) używa własnego protokołu do komunikowania się z SQL Server. Jest to lekkie i dobrze działa, ponieważ jest zoptymalizowany pod kątem dostępu do SQL Server bezpośrednio bez dodawania warstwy OLE DB lub Open Database Connectivity (ODBC). Poniższa ilustracja kontrastuje Dostawca danych .NET Framework dla SQL Server z .NET Framework Dostawca danych dla OLE DB. Dostawca danych .NET Framework dla OLE DB komunikuje się ze OLE DB źródłem danych za pomocą składnika usługi OLE DB, który zapewnia obsługę puli połączeń i usług transakcyjnych oraz dostawcę OLE DB dla źródła danych.  
  
> [!NOTE]
> .NET Framework Dostawca danych dla ODBC ma podobną architekturę do .NET Framework Dostawca danych dla OLE DB; na przykład wywołuje do składnika usługi ODBC.  
  
 ![Dostawcy danych](./media/netdataproviders-bpuedev11.gif "NETDataProviders_bpuedev11")  
Porównanie Dostawca danych .NET Framework dla SQL Server i .NET Framework Dostawca danych dla OLE DB  
  
 Dostawca danych .NET Framework klas SQL Server znajdują się w <xref:System.Data.SqlClient> przestrzeni nazw.  
  
 Dostawca danych .NET Framework dla SQL Server obsługuje zarówno transakcje lokalne, jak i rozproszone. W przypadku transakcji rozproszonych SQL Server Dostawca danych .NET Framework, domyślnie jest automatycznie rejestrowana w transakcji i uzyskuje szczegóły transakcji z usług składowych systemu Windows lub <xref:System.Transactions> . Aby uzyskać więcej informacji, zobacz [transakcje i współbieżność](transactions-and-concurrency.md).  
  
 Poniższy przykład kodu pokazuje, jak uwzględnić `System.Data.SqlClient` przestrzeń nazw w aplikacjach.  
  
```vb  
Imports System.Data.SqlClient  
```  
  
```csharp  
using System.Data.SqlClient;  
```  
  
## <a name="net-framework-data-provider-for-ole-db"></a>.NET Framework Dostawca danych OLE DB  

 .NET Framework Dostawca danych for OLE DB (OleDb) korzysta z natywnego OLE DB za pośrednictwem modelu COM Interop, aby umożliwić dostęp do danych. Dostawca danych .NET Framework dla OLE DB obsługuje zarówno transakcje lokalne, jak i rozproszone. W przypadku transakcji rozproszonych OLE DB Dostawca danych .NET Framework, domyślnie jest automatycznie rejestrowana w transakcji i uzyskuje szczegóły transakcji z usług składników systemu Windows. Aby uzyskać więcej informacji, zobacz [transakcje i współbieżność](transactions-and-concurrency.md).  
  
 W poniższej tabeli przedstawiono dostawców, którzy zostali przetestowani za pomocą ADO.NET.  
  
|Sterownik|Dostawca|  
|------------|--------------|  
|SQLOLEDB|Dostawca OLE DB firmy Microsoft dla SQL Server|  
|MSDAORA I|Dostawca OLE DB firmy Microsoft dla oprogramowania Oracle|  
|Microsoft. Jet. OLEDB. 4.0|Dostawca OLE DB dla programu Microsoft Jet|  
  
> [!NOTE]
> Nie zaleca się używania bazy danych programu Access (Jet) jako źródła danych dla aplikacji wielowątkowych, takich jak aplikacje ASP.NET. Jeśli konieczne jest użycie aparatu Jet jako źródła danych dla aplikacji ASP.NET, należy pamiętać, że aplikacje ASP.NET nawiązujące połączenie z bazą danych programu Access mogą napotkać problemy z połączeniem.  
  
 Dostawca danych .NET Framework dla OLE DB nie obsługuje interfejsów OLE DB w wersji 2,5. Dostawcy OLE DB, którzy wymagają obsługi interfejsów OLE DB 2,5, nie będą działać poprawnie z Dostawca danych .NET Framework dla OLE DB. Obejmuje to dostawcę OLE DB firmy Microsoft dla programu Exchange i dostawcę OLE DB firmy Microsoft do publikacji w Internecie.  
  
 Dostawca danych .NET Framework dla OLE DB nie działa z dostawcą OLE DB dla ODBC (MSDASQL). Aby uzyskać dostęp do źródła danych ODBC przy użyciu ADO.NET, użyj Dostawca danych .NET Framework dla ODBC.  
  
 Dostawca danych .NET Framework klas OLE DB znajdują się w <xref:System.Data.OleDb> przestrzeni nazw. Poniższy przykład kodu pokazuje, jak uwzględnić `System.Data.OleDb` przestrzeń nazw w aplikacjach.  
  
```vb  
Imports System.Data.OleDb  
```  
  
```csharp  
using System.Data.OleDb;  
```  
  
## <a name="net-framework-data-provider-for-odbc"></a>.NET Framework Dostawca danych dla ODBC  

 .NET Framework Dostawca danych dla ODBC (ODBC) używa natywnego Menedżera sterowników ODBC (DM), aby umożliwić dostęp do danych. Dostawca danych ODBC obsługuje zarówno transakcje lokalne, jak i rozproszone. W przypadku transakcji rozproszonych dostawca danych ODBC jest domyślnie automatycznie zarejestrowany w transakcji i uzyskuje szczegóły transakcji z usług składowych systemu Windows. Aby uzyskać więcej informacji, zobacz [transakcje i współbieżność](transactions-and-concurrency.md).  
  
 W poniższej tabeli przedstawiono sterowniki ODBC testowane z ADO.NET.  
  
|Sterownik|  
|------------|  
|SQL Server|  
|ODBC firmy Microsoft dla programu Oracle|  
|Sterownik programu Microsoft Access (*. mdb)|  
  
 .NET Framework Dostawca danych dla klas ODBC znajdują się w <xref:System.Data.Odbc> przestrzeni nazw.  
  
 Poniższy przykład kodu pokazuje, jak uwzględnić `System.Data.Odbc` przestrzeń nazw w aplikacjach.  
  
```vb  
Imports System.Data.Odbc  
```  
  
```csharp  
using System.Data.Odbc;  
```  
  
> [!NOTE]
> Dostawca danych .NET Framework dla ODBC wymaga programu MDAC 2,6 lub nowszej wersji, a zaleca się używanie programu MDAC 2,8 z dodatkiem SP1. Program MDAC 2,8 z dodatkiem SP1 można pobrać z [Centrum pobierania Microsoft](https://www.microsoft.com/download/details.aspx?id=5793).
  
## <a name="net-framework-data-provider-for-oracle"></a>.NET Framework Dostawca danych dla programu Oracle  

 .NET Framework Dostawca danych dla programu Oracle (OracleClient) umożliwia dostęp do danych w źródłach danych Oracle przy użyciu oprogramowania łączności klienta Oracle. Dostawca danych obsługuje oprogramowanie klienckie Oracle w wersji 8.1.7 lub nowszej. Dostawca danych obsługuje zarówno transakcje lokalne, jak i rozproszone. Aby uzyskać więcej informacji, zobacz [transakcje i współbieżność](transactions-and-concurrency.md).  
  
 Aby można było nawiązać połączenie ze źródłem danych Oracle, Dostawca danych .NET Framework dla systemu Oracle wymaga oprogramowania klienckiego Oracle (w wersji 8.1.7 lub nowszej).  
  
 .NET Framework Dostawca danych dla klas Oracle znajdują się w <xref:System.Data.OracleClient> przestrzeni nazw i znajdują się w `System.Data.OracleClient.dll` zestawie. Należy odwoływać się zarówno do, `System.Data.dll` jak i `System.Data.OracleClient.dll` podczas kompilowania aplikacji, która używa dostawcy danych.  
  
 Poniższy przykład kodu pokazuje, jak uwzględnić `System.Data.OracleClient` przestrzeń nazw w aplikacjach.  
  
```vb  
Imports System.Data  
Imports System.Data.OracleClient  
```  
  
```csharp  
using System.Data;  
using System.Data.OracleClient;  
```  
  
## <a name="choosing-a-net-framework-data-provider"></a>Wybieranie Dostawca danych .NET Framework  

 W zależności od projektu i źródła danych aplikacji wybór .NET Framework dostawcy danych może poprawić wydajność, możliwości i integralność aplikacji. W poniższej tabeli omówiono zalety i ograniczenia poszczególnych dostawców danych .NET Framework.  
  
|Dostawca|Uwagi|  
|--------------|-----------|  
|Dostawca danych programu .NET Framework dla programu SQL Server|Zalecane w przypadku aplikacji warstwy środkowej, które używają Microsoft SQL Server.<br /><br /> Zalecane w przypadku aplikacji jednowarstwowych, które korzystają z aparatu Microsoft Database Engine (MSDE) lub SQL Server.<br /><br /> Zalecane użycie dostawcy OLE DB dla SQL Server (SQLOLEDB) z Dostawca danych .NET Framework dla OLE DB.|  
|.NET Framework Dostawca danych OLE DB|W przypadku SQL Server zaleca się .NET Framework Dostawca danych dla SQL Server zamiast tego dostawcy.<br /><br /> Zalecane w przypadku aplikacji jednowarstwowych, które korzystają z baz danych programu Microsoft Access. Nie zaleca się używania bazy danych programu Access dla aplikacji warstwy środkowej.|  
|.NET Framework Dostawca danych dla ODBC|Zalecane w przypadku aplikacji środkowych i jednowarstwowych, które korzystają ze źródeł danych ODBC.|  
|.NET Framework Dostawca danych dla programu Oracle|Zalecane w przypadku aplikacji środkowych i jednowarstwowych, które korzystają ze źródeł danych Oracle.|  
  
## <a name="entityclient-provider"></a>Dostawca EntityClient  

 Dostawca EntityClient służy do uzyskiwania dostępu do danych na podstawie Entity Data Model (EDM). W przeciwieństwie do innych dostawców danych .NET Framework, nie współdziała bezpośrednio ze źródłem danych. Zamiast tego używa Entity SQL do komunikowania się z dostawcą danych bazowych. Aby uzyskać więcej informacji, zobacz [EntityClient Provider for the Entity Framework](./ef/entityclient-provider-for-the-entity-framework.md).  
  
## <a name="see-also"></a>Zobacz też

- [Omówienie ADO.NET](ado-net-overview.md)
- [Pobieranie i modyfikowanie danych ADO.NET](retrieving-and-modifying-data.md)
