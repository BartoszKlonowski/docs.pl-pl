---
title: Typy danych programu SQL Server i ADO.NET
titleSuffix: ''
ms.date: 03/30/2017
ms.assetid: 81b43550-23e8-43bb-b460-7eb8ac825c33
ms.openlocfilehash: db4618ac624ea8401cab682a8c21d8f23c253d05
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91155461"
---
# <a name="sql-server-data-types-and-adonet"></a>Typy danych programu SQL Server i ADO.NET

SQL Server i .NET Framework są oparte na różnych systemach typu, co może spowodować utratę danych. Aby zachować integralność danych, Dostawca danych .NET Framework dla SQL Server ( <xref:System.Data.SqlClient> ) zapewnia metody dostępu typu Type do pracy z danymi SQL Server. Możesz użyć wyliczeń w <xref:System.Data.SqlDbType> klasach, aby określić <xref:System.Data.SqlClient.SqlParameter> typy danych.  
  
 Aby uzyskać więcej informacji i tabelę opisującą mapowanie typu danych między SQL Server i .NET Framework typy danych, zobacz [SQL Server mapowania typów danych](../sql-server-data-type-mappings.md).  
  
 SQL Server 2008 wprowadza nowe typy danych, które są przeznaczone do zaspokajania potrzeb firmy, do pracy z danymi o dacie i godzinie, ze strukturą, częściową strukturą i bez struktury. Są one udokumentowane w SQL Server 2008 książki online.  
  
 SQL Server typy danych, które są dostępne do użycia w aplikacji, zależą od używanej wersji programu SQL Server. Aby uzyskać więcej informacji, zobacz odpowiednią wersję dokumentacji SQL Server Books Online w poniższej tabeli.  
  
 **Dokumentacja SQL Server**  
  
1. [Typy danych (Transact-SQL)](/sql/t-sql/data-types/data-types-transact-sql)  
  
## <a name="in-this-section"></a>W tej sekcji  

 [Właściwość SqlTypes i zestaw danych](sqltypes-and-the-dataset.md)  
 Opisuje obsługę typów `SqlTypes` w programie `DataSet` .  
  
 [Obsługa wartości Null](handling-null-values.md)  
 Pokazuje, jak korzystać z wartości null i logiki z trzema wartościami.  
  
 [Porównywanie identyfikatora GUID i wartości uniqueidentifier](comparing-guid-and-uniqueidentifier-values.md)  
 Demonstruje sposób pracy z identyfikatorami GUID i unikatowymi wartościami w SQL Server i .NET Framework.  
  
 [Dane daty i godziny](date-and-time-data.md)  
 Opisuje sposób korzystania z nowych typów danych daty i godziny wprowadzonych w SQL Server 2008.  
  
 [Duże UDT](large-udts.md)  
 Demonstruje sposób pobierania danych z UDTs dużej wartości wprowadzonych w SQL Server 2008.  
  
 [Dane XML w programie SQL Server](xml-data-in-sql-server.md)  
 Opisuje sposób pracy z danymi XML pobranymi z SQL Server.  
  
## <a name="reference"></a>Tematy pomocy  

 <xref:System.Data.DataSet>  
 Opisuje `DataSet` klasę i wszystkich jej członków.  
  
 <xref:System.Data.SqlTypes>  
 Zawiera opis `SqlTypes` przestrzeni nazw i wszystkich jej elementów członkowskich.  
  
 <xref:System.Data.SqlDbType>  
 Opisuje `SqlDbType` Wyliczenie i wszystkie jego elementy członkowskie.  
  
 <xref:System.Data.DbType>  
 Opisuje `DbType` Wyliczenie i wszystkie jego elementy członkowskie.  
  
## <a name="see-also"></a>Zobacz też

- [Mapowanie typu danych serwera SQL](../sql-server-data-type-mappings.md)
- [Konfigurowanie parametrów i typów danych parametrów](../configuring-parameters-and-parameter-data-types.md)
- [Parametry o wartościach tabelowych](table-valued-parameters.md)
- [Dane binarne i dużej wartości w programie SQL Server](sql-server-binary-and-large-value-data.md)
- [Omówienie ADO.NET](../ado-net-overview.md)
