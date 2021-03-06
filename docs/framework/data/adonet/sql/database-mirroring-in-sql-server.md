---
title: Dublowanie bazy danych w programie SQL Server
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 89befaff-bb46-4290-8382-e67cdb0e3de9
ms.openlocfilehash: 7e2c1c8ea1cbc1bb22452b9ef9d1f250c96118ea
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91173539"
---
# <a name="database-mirroring-in-sql-server"></a>Dublowanie bazy danych w programie SQL Server

Funkcja dublowania baz danych w programie SQL Server umożliwia przechowywanie kopii bazy danych SQL Server na serwerze rezerwy lub jej dublowanie. Funkcja dublowania gwarantuje, że w każdym momencie istnieją dwie oddzielne kopie danych, zapewniając wysoką dostępność i pełną nadmiarowość danych. Program .NET Dostawca danych dla SQL Server zapewnia niejawną obsługę funkcji dublowania baz danych, dzięki czemu Deweloper nie musi podejmować żadnych działań ani pisać kodu po skonfigurowaniu go dla bazy danych SQL Server. Ponadto <xref:System.Data.SqlClient.SqlConnection> obiekt obsługuje tryb połączenia jawnego, który umożliwia podawanie nazwy serwera partnerskiego trybu failover w programie <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A> .  
  
 Następująca uproszczona sekwencja zdarzeń występuje dla <xref:System.Data.SqlClient.SqlConnection> obiektu, który jest przeznaczony dla bazy danych skonfigurowanej do dublowania:  
  
1. Aplikacja kliencka pomyślnie nawiąże połączenie z główną bazą danych, a serwer wysyła do niej nazwę serwera partnerskiego, która jest następnie buforowana na kliencie.  
  
2. Jeśli serwer zawierający podstawową bazę danych ulegnie awarii lub połączenie zostanie przerwane, stan połączenia i transakcji zostanie utracony. Aplikacja kliencka próbuje ponownie nawiązać połączenie z główną bazą danych i kończy się niepowodzeniem.  
  
3. Aplikacja kliencka w sposób przezroczysty próbuje nawiązać połączenie z duplikatową bazą danych na serwerze partnerskim. Jeśli to się powiedzie, nastąpi przekierowanie do duplikatu bazy danych, która następnie będzie nową podstawową bazą danych.  
  
## <a name="specifying-the-failover-partner-in-the-connection-string"></a>Określanie partnera trybu failover w parametrach połączenia  

 W przypadku podania nazwy serwera partnerskiego trybu failover w parametrach połączenia klient będzie w sposób niewidoczny dla próby nawiązania połączenia z partnerem trybu failover, jeśli główna baza danych jest niedostępna, gdy aplikacja kliencka łączy się po raz pierwszy.  
  
```csharp
";Failover Partner=PartnerServerName"  
```  
  
 Jeśli pominięto nazwę serwera partnerskiego trybu failover, a główna baza danych jest niedostępna, gdy aplikacja kliencka po raz pierwszy łączy <xref:System.Data.SqlClient.SqlException> się, zostanie zgłoszony.  
  
 Po <xref:System.Data.SqlClient.SqlConnection> pomyślnym otwarciu nazwy partnera trybu failover są zwracane przez serwer i zastępują wszystkie wartości podane w parametrach połączenia.  
  
> [!NOTE]
> Należy jawnie określić początkowy katalog lub nazwę bazy danych w parametrach połączenia dla scenariuszy dublowania baz danych. Jeśli klient odbiera informacje o trybie failover dla połączenia, które nie ma jawnie określonego katalogu początkowego lub bazy danych, informacje o pracy awaryjnej nie są buforowane, a aplikacja nie podejmuje próby przełączenia w tryb failover w przypadku awarii serwera głównego. Jeśli parametry połączenia mają wartość dla partnera trybu failover, ale nie zostanie wyniesiona żadna wartość dla początkowego katalogu lub bazy danych `InvalidArgumentException` .  
  
## <a name="retrieving-the-current-server-name"></a>Pobieranie bieżącej nazwy serwera  

 W przypadku przełączenia w tryb failover można pobrać nazwę serwera, z którym bieżące połączenie jest rzeczywiście połączone przy użyciu <xref:System.Data.SqlClient.SqlConnection.DataSource%2A> właściwości <xref:System.Data.SqlClient.SqlConnection> obiektu. Poniższy fragment kodu pobiera nazwę aktywnego serwera, przy założeniu, że zmienna połączenia odwołuje się do otwartej <xref:System.Data.SqlClient.SqlConnection> .  
  
 Po wystąpieniu zdarzenia trybu failover i połączeniu z serwerem dublowanym Właściwość **DataSource** jest aktualizowana w celu odzwierciedlenia nazwy duplikatu.  
  
```vb  
Dim activeServer As String = connection.DataSource  
```  
  
```csharp  
string activeServer = connection.DataSource;  
```  
  
## <a name="sqlclient-mirroring-behavior"></a>Zachowanie funkcji dublowania SqlClient  

 Klient zawsze próbuje nawiązać połączenie z bieżącym serwerem głównym. Jeśli to się nie powiedzie, podejmie próbę partnera trybu failover. Jeśli zdublowana baza danych została już przełączona do roli podmiotu zabezpieczeń na serwerze partnerskim, nawiązanie połączenia zakończy się pomyślnie, a nowe mapowanie dublowanego podmiotu zabezpieczeń jest wysyłane do klienta i buforowane przez okres istnienia wywołania <xref:System.AppDomain> . Nie jest on przechowywany w magazynie trwałym i nie jest dostępny dla kolejnych połączeń w innej **domenie aplikacji** lub procesie. Jest to jednak dostępne dla kolejnych połączeń w ramach tej samej **domeny aplikacji**. Należy zauważyć, że inna **domena aplikacji** lub proces uruchomiony na tym samym lub innym komputerze zawsze ma swoją pulę połączeń i te połączenia nie są resetowane. W takim przypadku, jeśli podstawowa baza danych przestanie działać, każdy proces lub element **AppDomain** zakończy się niepowodzeniem, a pula zostanie automatycznie wyczyszczona.  
  
> [!NOTE]
> Obsługa dublowania na serwerze jest konfigurowana dla poszczególnych baz danych. Jeśli operacje manipulowania danymi są wykonywane w odniesieniu do innych baz danych, które nie znajdują się w zestawie główny/dublowany, przy użyciu nazw wieloczęściowych lub poprzez zmianę bieżącej bazy danych, zmiany tych innych baz danych nie są propagowane w przypadku awarii. Nie Wygenerowano żadnego błędu, gdy dane są modyfikowane w bazie danych, która nie jest dublowana. Deweloper musi oszacować możliwy wpływ takich operacji.  
  
## <a name="database-mirroring-resources"></a>Zasoby dublowania baz danych  

 Aby uzyskać dokumentację koncepcyjną i informacje dotyczące konfigurowania, wdrażania i administrowania dublowaniem, zobacz następujące zasoby w dokumentacji SQL Server.  
  
|Zasób|Opis|  
|--------------|-----------------|  
|[Dublowanie baz danych](/sql/database-engine/database-mirroring/database-mirroring-sql-server)|Opisuje sposób konfigurowania i konfigurowania dublowania w programie SQL Server.|  
  
## <a name="see-also"></a>Zobacz też

- [Omówienie ADO.NET](../ado-net-overview.md)
