---
title: Oracle i ADO.NET
description: Informacje na temat funkcji i zachowań .NET Framework Dostawca danych dla programu Oracle, które zapewniają dostęp do bazy danych Oracle przy użyciu interfejsu wywołania Oracle.
titleSuffix: ''
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 8ee8e389-53cf-45cf-80bd-1df63ef34f2e
ms.openlocfilehash: 736b8dc5179a15ec219c1dae06b9ee6b5d6c3ef3
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91166628"
---
# <a name="oracle-and-adonet"></a>Oracle i ADO.NET

> [!NOTE]
> Typy w <xref:System.Data.OracleClient> są przestarzałe. Typy pozostają obsługiwane w bieżącej wersji of.NET Framework, ale zostaną usunięte w przyszłej wersji. Firma Microsoft zaleca użycie dostawcy Oracle innej firmy.  
  
 W tej sekcji opisano funkcje i zachowania, które są specyficzne dla Dostawca danych .NET Framework dla programu Oracle.  
  
 .NET Framework Dostawca danych dla programu Oracle zapewnia dostęp do bazy danych Oracle przy użyciu interfejsu wywołania Oracle (OCI) dostarczonego przez oprogramowanie klienckie Oracle. Funkcja dostawcy danych została zaprojektowana tak, aby była podobna do .NET Framework dostawców danych dla SQL Server, OLE DB i ODBC.  
  
 Aby użyć Dostawca danych .NET Framework dla programu Oracle, aplikacja musi odwoływać się do <xref:System.Data.OracleClient> przestrzeni nazw w następujący sposób:  
  
```vb  
Imports System.Data.OracleClient  
```  
  
```csharp  
using System.Data.OracleClient;  
```  
  
 Podczas kompilowania kodu należy również dodać odwołanie do biblioteki DLL. Na przykład, Jeśli kompilujesz program w języku C#, wiersz polecenia powinien zawierać:  
  
```console
csc /r:System.Data.OracleClient.dll  
```  
  
## <a name="in-this-section"></a>W tej sekcji  

 [Wymagania systemowe](system-requirements-for-the-dotnet-data-provider-for-oracle.md)  
 W tym artykule opisano wymagania dotyczące korzystania z Dostawca danych .NET Framework dla programu Oracle oraz opisano różne problemy, które należy wziąć pod uwagę podczas korzystania z niego.  
  
 [Oracle BFILE](oracle-bfiles.md)  
 Opisuje <xref:System.Data.OracleClient.OracleBFile> klasę, która jest używana do pracy z typem danych Oracle bInformacje.  
  
 [Oracle LOB](oracle-lobs.md)  
 Opisuje <xref:System.Data.OracleClient.OracleLob> klasę, która jest używana do pracy z typami danych LOB firmy Oracle.  
  
 [Oracle REF CURSOR](oracle-ref-cursors.md)  
 Opisuje obsługę typu danych kursora usługi Oracle REF.  
  
 [OracleTypes](oracletypes.md)  
 Opisuje struktury, których można użyć do pracy z typami danych Oracle, w tym <xref:System.Data.OracleClient.OracleNumber> i <xref:System.Data.OracleClient.OracleString> .  
  
 [Sekwencje Oracle](oracle-sequences.md)  
 Opisuje obsługę pobierania wartości sekwencji programu Oracle klucza generowanej przez serwer.  
  
 [Mapowanie typu danych Oracle](oracle-data-type-mappings.md)  
 Wyświetla listę typów danych Oracle i ich mapowania na <xref:System.Data.OracleClient.OracleDataReader> .  
  
 [Transakcje rozproszone Oracle](oracle-distributed-transactions.md)  
 Opisuje, jak <xref:System.Data.OracleClient.OracleConnection> obiekt automatycznie jest zarejestrowany w istniejącej transakcji rozproszonej, jeśli określa, że transakcja jest aktywna.  
  
## <a name="related-sections"></a>Sekcje pokrewne  

 [Zabezpieczanie aplikacji ADO.NET](securing-ado-net-applications.md)  
 Zawiera opis bezpiecznych praktyk kodowania w przypadku korzystania z ADO.NET.  
  
 [Elementy DataSet, DataTable i DataView](./dataset-datatable-dataview/index.md)  
 Opisuje sposób tworzenia i używania `DataSets` , wpisywania `DataSets` , `DataTables` i `DataViews` .  
  
 [Pobieranie i modyfikowanie danych ADO.NET](retrieving-and-modifying-data.md)  
 Opisuje sposób pracy z danymi w ADO.NET.  
  
 [SQL Server i ADO.NET](./sql/index.md)  
 Opisuje sposób pracy z funkcjami i funkcjami, które są specyficzne dla SQL Server.  
  
 [DbProviderFactories](dbproviderfactories.md)  
 Opisuje klasy ogólne, które umożliwiają pisanie kodu niezależnego od dostawcy w ADO.NET.  
  
## <a name="see-also"></a>Zobacz też

- [ADO.NET](index.md)
- [Omówienie ADO.NET](ado-net-overview.md)
