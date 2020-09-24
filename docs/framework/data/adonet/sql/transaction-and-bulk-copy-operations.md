---
title: Transakcja i operacje kopiowania zbiorczego
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: f6f0cbc9-f7bf-4d6e-875f-ad1ba0b4aa62
ms.openlocfilehash: 27fafc0ef45b80eddd993229f52d119b40b4956f
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91155445"
---
# <a name="transaction-and-bulk-copy-operations"></a>Transakcja i operacje kopiowania zbiorczego

Operacje kopiowania zbiorczego można wykonać jako operacje izolowane lub w ramach transakcji wielu kroków. Ta ostatnia opcja umożliwia wykonywanie więcej niż jednej operacji kopiowania zbiorczego w ramach tej samej transakcji, a także wykonywanie innych operacji bazy danych (takich jak wstawianie, aktualizowanie i usuwanie) przy jednoczesnym zapewnieniu lub wycofaniu całej transakcji.  
  
 Domyślnie operacja kopiowania zbiorczego jest wykonywana jako operacja izolowana. Operacja kopiowania zbiorczego odbywa się w sposób nietransakcyjny, bez możliwości wycofywania jej z powrotem. Jeśli chcesz wycofać całość lub część kopiowania zbiorczego w przypadku wystąpienia błędu, możesz użyć <xref:System.Data.SqlClient.SqlBulkCopy> zarządzanej transakcji, wykonać operację kopiowania zbiorczego w ramach istniejącej transakcji lub zarejestrować się w **System. Transactions** <xref:System.Transactions.Transaction> .  
  
## <a name="performing-a-non-transacted-bulk-copy-operation"></a>Wykonywanie operacji kopiowania zbiorczego nietransakcyjnego  

 W poniższej aplikacji konsolowej pokazano, co się dzieje, gdy operacja kopiowania zbiorczego nietransakcyjnego napotka błąd partway za pomocą operacji.  
  
 W przykładzie tabela źródłowa i tabela docelowa zawierają `Identity` kolumnę o nazwie **ProductID**. Kod najpierw przygotowuje tabelę docelową, usuwając wszystkie wiersze, a następnie wstawiając pojedynczy wiersz, którego **ProductID** wiadomo, że istnieje w tabeli źródłowej. Domyślnie nowa wartość `Identity` kolumny jest generowana w tabeli docelowej dla każdego dodanego wiersza. W tym przykładzie opcja jest ustawiana podczas otwierania połączenia, które wymusza użycie przez proces ładowania zbiorczego `Identity` wartości z tabeli źródłowej.  
  
 Operacja kopiowania zbiorczego jest wykonywana z <xref:System.Data.SqlClient.SqlBulkCopy.BatchSize%2A> właściwością ustawioną na wartość 10. Gdy operacja napotka nieprawidłowy wiersz, zgłaszany jest wyjątek. W pierwszym przykładzie operacja kopiowania zbiorczego nie jest transakcyjna. Wszystkie partie skopiowane do punktu błędu są zatwierdzone; Partia zawierająca zduplikowany klucz jest wycofywana, a operacja kopiowania zbiorczego jest zatrzymywana przed przetworzeniem jakichkolwiek innych partii.  
  
> [!NOTE]
> Ten przykład nie zostanie uruchomiony, jeśli nie utworzono tabel roboczych, zgodnie z opisem w [przykładowej konfiguracji kopiowania zbiorczego](bulk-copy-example-setup.md). Ten kod jest dostarczany w celu przedstawienia składni tylko za pomocą **SqlBulkCopy** . Jeśli tabele źródłowe i docelowe znajdują się w tym samym wystąpieniu SQL Server, łatwiej i szybciej można używać instrukcji języka Transact-SQL `INSERT … SELECT` do kopiowania danych.  
  
 [!code-csharp[DataWorks SqlBulkCopy.DefaultTransaction#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlBulkCopy.DefaultTransaction/CS/source.cs#1)]
 [!code-vb[DataWorks SqlBulkCopy.DefaultTransaction#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlBulkCopy.DefaultTransaction/VB/source.vb#1)]  
  
## <a name="performing-a-dedicated-bulk-copy-operation-in-a-transaction"></a>Wykonywanie dedykowanej operacji kopiowania zbiorczego w transakcji  

 Domyślnie operacją kopiowania zbiorczego jest jego własna transakcja. Jeśli chcesz wykonać dedykowaną operację kopiowania zbiorczego, Utwórz nowe wystąpienie <xref:System.Data.SqlClient.SqlBulkCopy> z parametrami połączenia lub Użyj istniejącego <xref:System.Data.SqlClient.SqlConnection> obiektu bez aktywnej transakcji. W każdym scenariuszu operacja kopiowania zbiorczego tworzy, a następnie zatwierdza lub wycofuje transakcję.  
  
 Można jawnie określić <xref:System.Data.SqlClient.SqlBulkCopyOptions.UseInternalTransaction> opcję w <xref:System.Data.SqlClient.SqlBulkCopy> konstruktorze klasy, aby jawnie spowodować wykonanie operacji kopiowania zbiorczego we własnej transakcji, powodując, że każda partia operacji kopiowania zbiorczego jest wykonywana w ramach oddzielnej transakcji.  
  
> [!NOTE]
> Ponieważ różne partie są wykonywane w różnych transakcjach, jeśli wystąpi błąd podczas operacji kopiowania zbiorczego, wszystkie wiersze w bieżącej partii zostaną wycofane, ale wiersze z poprzednich partii pozostaną w bazie danych.  
  
 Następująca aplikacja konsolowa jest podobna do poprzedniego przykładu z jednym wyjątkiem: w tym przykładzie operacja kopiowania zbiorczego zarządza swoimi własnymi transakcjami. Wszystkie partie skopiowane do punktu błędu są zatwierdzone; Partia zawierająca zduplikowany klucz jest wycofywana, a operacja kopiowania zbiorczego jest zatrzymywana przed przetworzeniem jakichkolwiek innych partii.  
  
> [!IMPORTANT]
> Ten przykład nie zostanie uruchomiony, jeśli nie utworzono tabel roboczych, zgodnie z opisem w [przykładowej konfiguracji kopiowania zbiorczego](bulk-copy-example-setup.md). Ten kod jest dostarczany w celu przedstawienia składni tylko za pomocą **SqlBulkCopy** . Jeśli tabele źródłowe i docelowe znajdują się w tym samym wystąpieniu SQL Server, łatwiej i szybciej można używać instrukcji języka Transact-SQL `INSERT … SELECT` do kopiowania danych.  
  
 [!code-csharp[DataWorks SqlBulkCopy.InternalTransaction#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlBulkCopy.InternalTransaction/CS/source.cs#1)]
 [!code-vb[DataWorks SqlBulkCopy.InternalTransaction#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlBulkCopy.InternalTransaction/VB/source.vb#1)]  
  
## <a name="using-existing-transactions"></a>Korzystanie z istniejących transakcji  

 Możesz określić istniejący <xref:System.Data.SqlClient.SqlTransaction> obiekt jako parametr w <xref:System.Data.SqlClient.SqlBulkCopy> konstruktorze. W takiej sytuacji operacja kopiowania zbiorczego jest wykonywana w istniejącej transakcji i nie wprowadzono żadnych zmian w stanie transakcji (to oznacza, że nie jest ona zatwierdzona ani przerwana). Dzięki temu aplikacja może uwzględnić operację kopiowania zbiorczego w transakcji z innymi operacjami bazy danych. Jednakże jeśli nie określisz <xref:System.Data.SqlClient.SqlTransaction> obiektu i nie przekażesz odwołania o wartości null, a połączenie ma aktywną transakcję, zostanie zgłoszony wyjątek.  
  
 Jeśli trzeba wycofać całą operację kopiowania zbiorczego, ponieważ wystąpi błąd lub jeśli kopia Zbiorcza powinna zostać wykonana jako część większego procesu, który może zostać wycofany, można dostarczyć <xref:System.Data.SqlClient.SqlTransaction> obiekt do <xref:System.Data.SqlClient.SqlBulkCopy> konstruktora.  
  
 Następująca aplikacja konsolowa jest podobna do pierwszego (nietransakcyjnego) przykładu z jednym wyjątkiem: w tym przykładzie operacja kopiowania zbiorczego jest uwzględniana w większej, zewnętrznej transakcji. Gdy wystąpi błąd naruszenia klucza podstawowego, cała transakcja jest wycofywana i żadne wiersze nie są dodawane do tabeli docelowej.  
  
> [!IMPORTANT]
> Ten przykład nie zostanie uruchomiony, jeśli nie utworzono tabel roboczych, zgodnie z opisem w [przykładowej konfiguracji kopiowania zbiorczego](bulk-copy-example-setup.md). Ten kod jest dostarczany w celu przedstawienia składni tylko za pomocą **SqlBulkCopy** . Jeśli tabele źródłowe i docelowe znajdują się w tym samym wystąpieniu SQL Server, łatwiej i szybciej można używać instrukcji języka Transact-SQL `INSERT … SELECT` do kopiowania danych.  
  
 [!code-csharp[DataWorks SqlBulkCopy.SqlTransaction#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlBulkCopy.SqlTransaction/CS/source.cs#1)]
 [!code-vb[DataWorks SqlBulkCopy.SqlTransaction#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlBulkCopy.SqlTransaction/VB/source.vb#1)]  
  
## <a name="see-also"></a>Zobacz też

- [Operacje kopiowania masowego w programie SQL Server](bulk-copy-operations-in-sql-server.md)
- [Omówienie ADO.NET](../ado-net-overview.md)
