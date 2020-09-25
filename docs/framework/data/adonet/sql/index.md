---
title: SQL Server i ADO.NET
description: Dowiedz się więcej na temat funkcji i zachowań Dostawca danych .NET Framework dla SQL Server, które hermetyzują protokoły specyficzne dla bazy danych.
titleSuffix: ''
ms.date: 03/30/2017
ms.assetid: c18b1fb1-2af1-4de7-80a4-95e56fd976cb
ms.openlocfilehash: a517bccd9b60d00f6c6c636c9164d63fb5966de3
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91197394"
---
# <a name="sql-server-and-adonet"></a>SQL Server i ADO.NET

W tej sekcji opisano funkcje i zachowania, które są specyficzne dla Dostawca danych .NET Framework dla SQL Server ( <xref:System.Data.SqlClient> ).  
  
 <xref:System.Data.SqlClient> zapewnia dostęp do wersji SQL Server, które hermetyzują protokoły specyficzne dla bazy danych. Funkcja dostawcy danych została zaprojektowana tak, aby była podobna do .NET Framework dostawców danych dla OLE DB, ODBC i Oracle. <xref:System.Data.SqlClient> zawiera Analizator strumienia danych tabelarycznych (TDS) do bezpośredniego komunikowania się z SQL Server.  
  
> [!NOTE]
> Aby można było użyć Dostawca danych .NET Framework na potrzeby SQL Server, aplikacja musi odwoływać się do <xref:System.Data.SqlClient> przestrzeni nazw.  
  
## <a name="in-this-section"></a>W tej sekcji  

 [Zabezpieczenia serwera SQL](sql-server-security.md)  
 Zawiera omówienie funkcji zabezpieczeń SQL Server i scenariuszy aplikacji do tworzenia bezpiecznych aplikacji ADO.NET, które są przeznaczone SQL Server.  
  
 [Typy danych programu SQL Server i ADO.NET](sql-server-data-types.md)  
 Opisuje sposób pracy z SQL Server typami danych i sposobami ich współpracy z .NET Framework typami danych.  
  
 [Dane binarne i dużej wartości w programie SQL Server](sql-server-binary-and-large-value-data.md)  
 Opisuje sposób pracy z danymi dużej wartości w SQL Server.  
  
 [Operacje danych serwera SQL w ADO.NET](sql-server-data-operations.md)  
 Opisuje sposób pracy z danymi w SQL Server. Zawiera sekcje dotyczące operacji kopiowania zbiorczego, operacji MARS, asynchronicznych i parametrów z wartościami przechowywanymi w tabeli.  
  
 [Funkcje Serwera SQL i ADO.NET](sql-server-features-and-adonet.md)  
 Opisuje funkcje SQL Server, które są przydatne w przypadku deweloperów aplikacji ADO.NET.  
  
 [LINQ to SQL](./linq/index.md)  
 Zawiera opis podstawowych bloków konstrukcyjnych, procesów i technik wymaganych do tworzenia aplikacji LINQ to SQL.  
  
 Aby uzyskać pełną dokumentację aparatu bazy danych SQL Server, zobacz SQL Server Books Online dla używanej wersji programu SQL Server.  
  
 [Książka SQL Server online](/sql/sql-server/sql-server-technical-documentation)  
  
## <a name="see-also"></a>Zobacz też

- [Zabezpieczanie aplikacji ADO.NET](../securing-ado-net-applications.md)
- [Mapowanie typu danych w ADO.NET](../data-type-mappings-in-ado-net.md)
- [Elementy DataSet, DataTable i DataView](../dataset-datatable-dataview/index.md)
- [Pobieranie i modyfikowanie danych ADO.NET](../retrieving-and-modifying-data.md)
- [Omówienie ADO.NET](../ado-net-overview.md)
