---
title: Transakcje i współbieżność
ms.date: 03/30/2017
ms.assetid: f46570de-9e50-4fe6-8710-a8c31fa8569b
ms.openlocfilehash: 049e402345e1abbb46739e48c89101207a43bb27
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91191674"
---
# <a name="transactions-and-concurrency"></a>Transakcje i współbieżność

Transakcja składa się z jednego polecenia lub grupy poleceń, które są wykonywane jako pakiet. Transakcje umożliwiają łączenie wielu operacji w pojedynczą jednostkę pracy. Jeśli wystąpi awaria w jednym punkcie transakcji, wszystkie aktualizacje można przywrócić do stanu sprzed transakcji.  
  
 Transakcja musi być zgodna z właściwościami KWASu — niepodzielności, spójności, izolacji i trwałości — w celu zagwarantowania spójności danych. Większość systemów relacyjnej bazy danych, takich jak Microsoft SQL Server, obsługa transakcji przez zapewnienie blokowania, rejestrowania i zarządzania transakcjami za każdym razem, gdy aplikacja kliencka wykonuje operację Update, INSERT lub DELETE.  
  
> [!NOTE]
> Transakcje obejmujące wiele zasobów mogą obniżać współbieżność, jeśli blokady są zbyt długie. W związku z tym Zachowaj transakcje tak krótkie, jak to możliwe.  
  
 Jeśli transakcja obejmuje wiele tabel w tej samej bazie danych lub serwerze, to jawne transakcje w procedurach składowanych często działają lepiej. Można tworzyć transakcje w SQL Server procedury składowane przy użyciu instrukcji Transact-SQL `BEGIN TRANSACTION` , `COMMIT TRANSACTION` i `ROLLBACK TRANSACTION` . Aby uzyskać więcej informacji, zobacz SQL Server Books Online.  
  
 Transakcje dotyczące różnych menedżerów zasobów, takich jak transakcja między SQL Server i Oracle, wymagają transakcji rozproszonej.  
  
## <a name="in-this-section"></a>W tej sekcji  

 [Transakcje lokalne](local-transactions.md)  
 Pokazuje, jak wykonywać transakcje względem bazy danych.  
  
 [Transakcje rozproszone](distributed-transactions.md)  
 Opisuje sposób wykonywania transakcji rozproszonych w programie ADO.NET.  
  
 [Integracja System.Transactions z programem SQL Server](system-transactions-integration-with-sql-server.md)  
 Opisuje <xref:System.Transactions> integrację z SQL Server do pracy z transakcjami rozproszonymi.  
  
 [Optymistyczna współbieżność](optimistic-concurrency.md)  
 Opisuje optymistyczne i pesymistyczne współbieżność oraz sposób testowania naruszeń współbieżności.  
  
## <a name="see-also"></a>Zobacz też

- [Podstawowe informacje dotyczące transakcji](../transactions/transaction-fundamentals.md)
- [Nawiązywanie połączenia ze źródłem danych](connecting-to-a-data-source.md)
- [Polecenia i parametry](commands-and-parameters.md)
- [Elementy DataAdapter i DataReader](dataadapters-and-datareaders.md)
- [DbProviderFactories](dbproviderfactories.md)
- [Omówienie ADO.NET](ado-net-overview.md)
