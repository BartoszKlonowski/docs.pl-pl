---
title: Integracja aparatu plików wykonywalnych języka wspólnego z programem SQL Server
ms.date: 03/30/2017
ms.assetid: c7a324c4-160d-44c2-b593-641af06eca61
ms.openlocfilehash: d9fe0f03c88584607c6bc38fcbcff3f9424fd40c
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91183029"
---
# <a name="sql-server-common-language-runtime-integration"></a>Integracja aparatu plików wykonywalnych języka wspólnego z programem SQL Server

W SQL Server 2005 wprowadzono integrację składnika środowiska uruchomieniowego języka wspólnego (CLR) .NET Framework dla systemu Microsoft Windows. Oznacza to, że można napisać procedury składowane, wyzwalacze, typy zdefiniowane przez użytkownika, funkcje zdefiniowane przez użytkownika, agregacje zdefiniowane przez użytkownika i funkcję przesyłania strumieniowego z wartościami przechowywanymi w tabeli przy użyciu dowolnego .NET Framework języka, w tym programów Microsoft Visual Basic .NET i Microsoft Visual C#. <xref:Microsoft.SqlServer.Server>Przestrzeń nazw zawiera zestaw nowych interfejsów programowania aplikacji (API), dzięki czemu kod zarządzany może współdziałać ze środowiskiem Microsoft SQL Server.  
  
 W tej sekcji opisano funkcje i zachowania, które są specyficzne SQL Server dla integracji środowiska uruchomieniowego języka wspólnego (CLR) i SQL Server w procesie ADO.NET.  
  
 Ta sekcja ma na celu dostarczenie tylko wystarczającej ilości informacji, aby rozpocząć programowanie przy użyciu integracji środowiska CLR SQL Server i nie jest to wszechstronne. Aby uzyskać bardziej szczegółowe informacje, zapoznaj się z wersją usługi SQL Server Books Online dla używanej wersji SQL Server.  
  
 **Dokumentacja SQL Server**  
  
1. [Pojęcia dotyczące programowania integracji środowiska uruchomieniowego języka wspólnego (CLR)](/sql/relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts)  
  
## <a name="in-this-section"></a>W tej sekcji  

 [Wprowadzenie do integracji środowiska CLR programu SQL Server](introduction-to-sql-server-clr-integration.md)  
 Zawiera wprowadzenie do SQL Server integracji środowiska CLR. Zawiera łącza do dodatkowych tematów.  
  
 [Zdefiniowane przez użytkownika funkcje CLR](clr-user-defined-functions.md)  
 Opisuje sposób implementacji i używania różnych typów funkcji CLR: funkcji agregujących zwracającej tabelę, skalarnej i zdefiniowanej przez użytkownika.  
  
 [Zdefiniowane przez użytkownika typy CLR](clr-user-defined-types.md)  
 Opisuje sposób implementacji i używania typów CLR zdefiniowanych przez użytkownika. Zawiera łącza do dodatkowych tematów.  
  
 [Procedury składowane CLR](clr-stored-procedures.md)  
 Opisuje sposób implementacji i używania procedur składowanych CLR. Zawiera łącza do dodatkowych tematów.  
  
 [Wyzwalacze CLR](clr-triggers.md)  
 Opisuje sposób implementacji i używania wyzwalaczy CLR. Zawiera łącza do dodatkowych tematów.  
  
 [Połączenie kontekstu](the-context-connection.md)  
 Opisuje połączenie kontekstu.  
  
 [Zachowanie w procesie specyficzne dla serwera SQL ADO.NET](sql-server-in-process-specific-behavior-of-adonet.md)  
 W tym artykule opisano SQL Server specyficzne dla procesu rozszerzenia ADO.NET i połączenia kontekstu. Zawiera łącza do dodatkowych tematów.  
  
## <a name="see-also"></a>Zobacz też

- [SQL Server i ADO.NET](index.md)
- [Omówienie ADO.NET](../ado-net-overview.md)
