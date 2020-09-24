---
title: Włączanie wielu aktywnych zestawów wyników
description: Informacje na temat włączania/wyłączania usługi MARS w parametrach połączenia, które współdziałają z SQL Server, dzięki czemu można uruchamiać wiele partii na jednym połączeniu w ADO.NET.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 576079e4-debe-4ab5-9204-fcbe2ca7a5e2
ms.openlocfilehash: 0c5b4043b389c7dde39a477f90e82bbf654331f7
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91156254"
---
# <a name="enabling-multiple-active-result-sets"></a><span data-ttu-id="dfea1-103">Włączanie wielu aktywnych zestawów wyników</span><span class="sxs-lookup"><span data-stu-id="dfea1-103">Enabling Multiple Active Result Sets</span></span>

<span data-ttu-id="dfea1-104">Wiele aktywnych zestawów wyników (MARS) to funkcja, która współpracuje z SQL Server, aby umożliwić wykonywanie wielu partii na jednym połączeniu.</span><span class="sxs-lookup"><span data-stu-id="dfea1-104">Multiple Active Result Sets (MARS) is a feature that works with SQL Server to allow the execution of multiple batches on a single connection.</span></span> <span data-ttu-id="dfea1-105">Gdy Usługa MARS jest włączona do użytku z SQL Server, każdy użyty obiekt polecenia dodaje sesję do połączenia.</span><span class="sxs-lookup"><span data-stu-id="dfea1-105">When MARS is enabled for use with SQL Server, each command object used adds a session to the connection.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="dfea1-106">Pojedyncza sesja MARS otwiera jedno połączenie logiczne dla MARS do użycia, a następnie jedno połączenie logiczne dla każdego aktywnego polecenia.</span><span class="sxs-lookup"><span data-stu-id="dfea1-106">A single MARS session opens one logical connection for MARS to use and then one logical connection for each active command.</span></span>  
  
## <a name="enabling-and-disabling-mars-in-the-connection-string"></a><span data-ttu-id="dfea1-107">Włączanie i wyłączanie MARS w parametrach połączenia</span><span class="sxs-lookup"><span data-stu-id="dfea1-107">Enabling and Disabling MARS in the Connection String</span></span>  
  
> [!NOTE]
> <span data-ttu-id="dfea1-108">Poniższe parametry połączenia korzystają z przykładowej bazy danych **AdventureWorks** dołączonej do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dfea1-108">The following connection strings use the sample **AdventureWorks** database included with SQL Server.</span></span> <span data-ttu-id="dfea1-109">W określonych parametrach połączenia przyjęto założenie, że baza danych jest zainstalowana na serwerze o nazwie MSSQL1.</span><span class="sxs-lookup"><span data-stu-id="dfea1-109">The connection strings provided assume that the database is installed on a server named MSSQL1.</span></span> <span data-ttu-id="dfea1-110">Zmodyfikuj parametry połączenia jako niezbędne dla danego środowiska.</span><span class="sxs-lookup"><span data-stu-id="dfea1-110">Modify the connection string as necessary for your environment.</span></span>  
  
 <span data-ttu-id="dfea1-111">Funkcja MARS jest domyślnie wyłączona.</span><span class="sxs-lookup"><span data-stu-id="dfea1-111">The MARS feature is disabled by default.</span></span> <span data-ttu-id="dfea1-112">Można ją włączyć, dodając parę słów kluczowych "MultipleActiveResultSets = true" do parametrów połączenia.</span><span class="sxs-lookup"><span data-stu-id="dfea1-112">It can be enabled by adding the "MultipleActiveResultSets=True" keyword pair to your connection string.</span></span> <span data-ttu-id="dfea1-113">Wartość "true" jest jedyną prawidłową wartością dla włączania MARS.</span><span class="sxs-lookup"><span data-stu-id="dfea1-113">"True" is the only valid value for enabling MARS.</span></span> <span data-ttu-id="dfea1-114">Poniższy przykład pokazuje, jak nawiązać połączenie z wystąpieniem SQL Server i jak określić, że Usługa MARS powinna być włączona.</span><span class="sxs-lookup"><span data-stu-id="dfea1-114">The following example demonstrates how to connect to an instance of SQL Server and how to specify that MARS should be enabled.</span></span>  
  
```vb  
Dim connectionString As String = "Data Source=MSSQL1;" & _  
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" & _  
    "MultipleActiveResultSets=True"  
```  
  
```csharp  
string connectionString = "Data Source=MSSQL1;" +
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" +  
    "MultipleActiveResultSets=True";  
```  
  
 <span data-ttu-id="dfea1-115">Można wyłączyć usługę MARS, dodając parę słów kluczowych "MultipleActiveResultSets = false" do parametrów połączenia.</span><span class="sxs-lookup"><span data-stu-id="dfea1-115">You can disable MARS by adding the "MultipleActiveResultSets=False" keyword pair to your connection string.</span></span> <span data-ttu-id="dfea1-116">Wartość "false" jest jedyną prawidłową wartością do wyłączania usługi MARS.</span><span class="sxs-lookup"><span data-stu-id="dfea1-116">"False" is the only valid value for disabling MARS.</span></span> <span data-ttu-id="dfea1-117">Poniższe parametry połączenia pokazują, jak wyłączyć usługę MARS.</span><span class="sxs-lookup"><span data-stu-id="dfea1-117">The following connection string demonstrates how to disable MARS.</span></span>  
  
```vb  
Dim connectionString As String = "Data Source=MSSQL1;" & _  
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" & _  
    "MultipleActiveResultSets=False"  
```  
  
```csharp  
string connectionString = "Data Source=MSSQL1;" +
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" +  
    "MultipleActiveResultSets=False";  
```  
  
## <a name="special-considerations-when-using-mars"></a><span data-ttu-id="dfea1-118">Specjalne uwagi dotyczące korzystania z usługi MARS</span><span class="sxs-lookup"><span data-stu-id="dfea1-118">Special Considerations When Using MARS</span></span>  

 <span data-ttu-id="dfea1-119">Ogólnie rzecz biorąc, istniejące aplikacje nie powinny wymagać modyfikacji w celu korzystania z połączenia z obsługą usługi MARS.</span><span class="sxs-lookup"><span data-stu-id="dfea1-119">In general, existing applications should not need modification to use a MARS-enabled connection.</span></span> <span data-ttu-id="dfea1-120">Jeśli jednak chcesz korzystać z funkcji MARS w aplikacjach, należy zapoznać się z następującymi kwestiami szczególnymi.</span><span class="sxs-lookup"><span data-stu-id="dfea1-120">However, if you wish to use MARS features in your applications, you should understand the following special considerations.</span></span>  
  
### <a name="statement-interleaving"></a><span data-ttu-id="dfea1-121">Przeplot instrukcji</span><span class="sxs-lookup"><span data-stu-id="dfea1-121">Statement Interleaving</span></span>  

 <span data-ttu-id="dfea1-122">Operacje MARS są wykonywane synchronicznie na serwerze.</span><span class="sxs-lookup"><span data-stu-id="dfea1-122">MARS operations execute synchronously on the server.</span></span> <span data-ttu-id="dfea1-123">Wychodzące instrukcji SELECT i BULK INSERT są dozwolone.</span><span class="sxs-lookup"><span data-stu-id="dfea1-123">Statement interleaving of SELECT and BULK INSERT statements is allowed.</span></span> <span data-ttu-id="dfea1-124">Jednak instrukcje języka manipulowania danymi (DML) i języka definicji danych (DDL) wykonują niepodzielną.</span><span class="sxs-lookup"><span data-stu-id="dfea1-124">However, data manipulation language (DML) and data definition language (DDL) statements execute atomically.</span></span> <span data-ttu-id="dfea1-125">Wszystkie instrukcje, które próbują wykonać podczas wykonywania niepodzielnej partii, są blokowane.</span><span class="sxs-lookup"><span data-stu-id="dfea1-125">Any statements attempting to execute while an atomic batch is executing are blocked.</span></span> <span data-ttu-id="dfea1-126">Wykonywanie równoległe na serwerze nie jest funkcją MARS.</span><span class="sxs-lookup"><span data-stu-id="dfea1-126">Parallel execution at the server is not a MARS feature.</span></span>  
  
 <span data-ttu-id="dfea1-127">Jeśli dwie partie są przesyłane w ramach połączenia MARS, jeden z nich zawierający instrukcję SELECT, drugi zawierający instrukcję DML, może rozpocząć wykonywanie w ramach wykonywania instrukcji SELECT.</span><span class="sxs-lookup"><span data-stu-id="dfea1-127">If two batches are submitted under a MARS connection, one of them containing a SELECT statement, the other containing a DML statement, the DML can begin execution within execution of the SELECT statement.</span></span> <span data-ttu-id="dfea1-128">Jednakże instrukcja DML musi być uruchamiana do zakończenia przed wykonaniem instrukcji SELECT.</span><span class="sxs-lookup"><span data-stu-id="dfea1-128">However, the DML statement must run to completion before the SELECT statement can make progress.</span></span> <span data-ttu-id="dfea1-129">Jeśli obie te instrukcje są uruchomione w ramach tej samej transakcji, wszelkie zmiany wprowadzone przez instrukcję DML po rozpoczęciu wykonywania instrukcji SELECT nie są widoczne dla operacji odczytu.</span><span class="sxs-lookup"><span data-stu-id="dfea1-129">If both statements are running under the same transaction, any changes made by a DML statement after the SELECT statement has started execution are not visible to the read operation.</span></span>  
  
 <span data-ttu-id="dfea1-130">Instrukcja WAITFOR wewnątrz instrukcji SELECT nie zwraca transakcji w oczekiwany sposób, czyli do momentu utworzenia pierwszego wiersza.</span><span class="sxs-lookup"><span data-stu-id="dfea1-130">A WAITFOR statement inside a SELECT statement does not yield the transaction while it is waiting, that is, until the first row is produced.</span></span> <span data-ttu-id="dfea1-131">Oznacza to, że żadne inne partie nie mogą być wykonywane w ramach tego samego połączenia podczas oczekiwania instrukcji WAITFOR.</span><span class="sxs-lookup"><span data-stu-id="dfea1-131">This implies that no other batches can execute within the same connection while a WAITFOR statement is waiting.</span></span>  
  
### <a name="mars-session-cache"></a><span data-ttu-id="dfea1-132">Pamięć podręczna sesji MARS</span><span class="sxs-lookup"><span data-stu-id="dfea1-132">MARS Session Cache</span></span>  

 <span data-ttu-id="dfea1-133">Po otwarciu połączenia z włączonym usługą MARS zostanie utworzona sesja logiczna, która dodaje dodatkowe obciążenie.</span><span class="sxs-lookup"><span data-stu-id="dfea1-133">When a connection is opened with MARS enabled, a logical session is created, which adds additional overhead.</span></span> <span data-ttu-id="dfea1-134">Aby zminimalizować obciążenie i zwiększyć wydajność, **Klient SqlClient** buforuje sesję Mars w ramach połączenia.</span><span class="sxs-lookup"><span data-stu-id="dfea1-134">To minimize overhead and enhance performance, **SqlClient** caches the MARS session within a connection.</span></span> <span data-ttu-id="dfea1-135">Pamięć podręczna zawiera maksymalnie 10 sesji MARS.</span><span class="sxs-lookup"><span data-stu-id="dfea1-135">The cache contains at most 10 MARS sessions.</span></span> <span data-ttu-id="dfea1-136">Ta wartość nie jest dostosowywana do użytkownika.</span><span class="sxs-lookup"><span data-stu-id="dfea1-136">This value is not user adjustable.</span></span> <span data-ttu-id="dfea1-137">Jeśli limit sesji zostanie osiągnięty, zostanie utworzona nowa sesja — błąd nie zostanie wygenerowany.</span><span class="sxs-lookup"><span data-stu-id="dfea1-137">If the session limit is reached, a new session is created—an error is not generated.</span></span> <span data-ttu-id="dfea1-138">Pamięć podręczna i sesje zawarte w niej są przyłączone do połączenia; nie są one udostępniane między połączeniami.</span><span class="sxs-lookup"><span data-stu-id="dfea1-138">The cache and sessions contained in it are per-connection; they are not shared across connections.</span></span> <span data-ttu-id="dfea1-139">Po wydaniu sesji jest ona zwracana do puli, chyba że górny limit puli został osiągnięty.</span><span class="sxs-lookup"><span data-stu-id="dfea1-139">When a session is released, it is returned to the pool unless the pool's upper limit has been reached.</span></span> <span data-ttu-id="dfea1-140">Jeśli pula pamięci podręcznej jest pełna, sesja zostanie zamknięta.</span><span class="sxs-lookup"><span data-stu-id="dfea1-140">If the cache pool is full, the session is closed.</span></span> <span data-ttu-id="dfea1-141">Sesje MARS nie wygasną.</span><span class="sxs-lookup"><span data-stu-id="dfea1-141">MARS sessions do not expire.</span></span> <span data-ttu-id="dfea1-142">Są czyszczone tylko wtedy, gdy obiekt połączenia zostanie usunięty.</span><span class="sxs-lookup"><span data-stu-id="dfea1-142">They are only cleaned up when the connection object is disposed.</span></span> <span data-ttu-id="dfea1-143">Pamięć podręczna sesji MARS nie jest wstępnie załadowana.</span><span class="sxs-lookup"><span data-stu-id="dfea1-143">The MARS session cache is not preloaded.</span></span> <span data-ttu-id="dfea1-144">Jest ona ładowana, ponieważ aplikacja wymaga więcej sesji.</span><span class="sxs-lookup"><span data-stu-id="dfea1-144">It is loaded as the application requires more sessions.</span></span>  
  
### <a name="thread-safety"></a><span data-ttu-id="dfea1-145">Bezpieczeństwo wątkowe</span><span class="sxs-lookup"><span data-stu-id="dfea1-145">Thread Safety</span></span>  

 <span data-ttu-id="dfea1-146">Operacje MARS nie są bezpieczne wątkowo.</span><span class="sxs-lookup"><span data-stu-id="dfea1-146">MARS operations are not thread-safe.</span></span>  
  
### <a name="connection-pooling"></a><span data-ttu-id="dfea1-147">Pula połączeń</span><span class="sxs-lookup"><span data-stu-id="dfea1-147">Connection Pooling</span></span>  

 <span data-ttu-id="dfea1-148">Połączenia z obsługą usługi MARS są umieszczane w puli, podobnie jak inne połączenia.</span><span class="sxs-lookup"><span data-stu-id="dfea1-148">MARS-enabled connections are pooled like any other connection.</span></span> <span data-ttu-id="dfea1-149">Jeśli aplikacja otworzy dwa połączenia, jeden z włączonym usługą MARS i jeden z wyłączonym MARS, dwa połączenia są w różnych pulach.</span><span class="sxs-lookup"><span data-stu-id="dfea1-149">If an application opens two connections, one with MARS enabled and one with MARS disabled, the two connections are in separate pools.</span></span> <span data-ttu-id="dfea1-150">Aby uzyskać więcej informacji, zobacz [SQL Servering pooling (ADO.NET)](../sql-server-connection-pooling.md).</span><span class="sxs-lookup"><span data-stu-id="dfea1-150">For more information, see [SQL Server Connection Pooling (ADO.NET)](../sql-server-connection-pooling.md).</span></span>  
  
### <a name="sql-server-batch-execution-environment"></a><span data-ttu-id="dfea1-151">SQL Server środowiska wykonawczego partii</span><span class="sxs-lookup"><span data-stu-id="dfea1-151">SQL Server Batch Execution Environment</span></span>  

 <span data-ttu-id="dfea1-152">Po otwarciu połączenia jest zdefiniowane środowisko domyślne.</span><span class="sxs-lookup"><span data-stu-id="dfea1-152">When a connection is opened, a default environment is defined.</span></span> <span data-ttu-id="dfea1-153">To środowisko jest następnie kopiowane do logicznej sesji MARS.</span><span class="sxs-lookup"><span data-stu-id="dfea1-153">This environment is then copied into a logical MARS session.</span></span>  
  
 <span data-ttu-id="dfea1-154">Środowisko wykonywania wsadowego obejmuje następujące składniki:</span><span class="sxs-lookup"><span data-stu-id="dfea1-154">The batch execution environment includes the following components:</span></span>  
  
- <span data-ttu-id="dfea1-155">Ustawianie opcji (na przykład ANSI_NULLS, DATE_FORMAT, LANGUAGE, wartość PARAMETRU TEXTSIZE)</span><span class="sxs-lookup"><span data-stu-id="dfea1-155">Set options (for example, ANSI_NULLS, DATE_FORMAT, LANGUAGE, TEXTSIZE)</span></span>  
  
- <span data-ttu-id="dfea1-156">Kontekst zabezpieczeń (rola użytkownika/aplikacji)</span><span class="sxs-lookup"><span data-stu-id="dfea1-156">Security context (user/application role)</span></span>  
  
- <span data-ttu-id="dfea1-157">Kontekst bazy danych (bieżąca baza danych)</span><span class="sxs-lookup"><span data-stu-id="dfea1-157">Database context (current database)</span></span>  
  
- <span data-ttu-id="dfea1-158">Zmienne stanu wykonania (na przykład @ @ERROR , @ @ROWCOUNT , @ @FETCH_STATUS @ @IDENTITY )</span><span class="sxs-lookup"><span data-stu-id="dfea1-158">Execution state variables (for example, @@ERROR, @@ROWCOUNT, @@FETCH_STATUS @@IDENTITY)</span></span>  
  
- <span data-ttu-id="dfea1-159">Tymczasowe tabele najwyższego poziomu</span><span class="sxs-lookup"><span data-stu-id="dfea1-159">Top-level temporary tables</span></span>  
  
 <span data-ttu-id="dfea1-160">W przypadku usługi MARS do połączenia jest skojarzone domyślne środowisko wykonawcze.</span><span class="sxs-lookup"><span data-stu-id="dfea1-160">With MARS, a default execution environment is associated to a connection.</span></span> <span data-ttu-id="dfea1-161">Każda nowa partia, która rozpoczyna wykonywanie w ramach danego połączenia, otrzymuje kopię domyślnego środowiska.</span><span class="sxs-lookup"><span data-stu-id="dfea1-161">Every new batch that starts executing under a given connection receives a copy of the default environment.</span></span> <span data-ttu-id="dfea1-162">Za każdym razem, gdy kod jest wykonywany w ramach danej partii, wszystkie zmiany wprowadzone w środowisku są ograniczone do określonej partii.</span><span class="sxs-lookup"><span data-stu-id="dfea1-162">Whenever code is executed under a given batch, all changes made to the environment are scoped to the specific batch.</span></span> <span data-ttu-id="dfea1-163">Po zakończeniu wykonywania ustawienia wykonywania są kopiowane do środowiska domyślnego.</span><span class="sxs-lookup"><span data-stu-id="dfea1-163">Once execution finishes, the execution settings are copied into the default environment.</span></span> <span data-ttu-id="dfea1-164">W przypadku pojedynczej partii, która wystawia kilka poleceń, które mają być wykonywane sekwencyjnie w ramach tej samej transakcji, semantyka jest taka sama jak w przypadku połączeń obejmujących wcześniejszych klientów lub serwery.</span><span class="sxs-lookup"><span data-stu-id="dfea1-164">In the case of a single batch issuing several commands to be executed sequentially under the same transaction, semantics are the same as those exposed by connections involving earlier clients or servers.</span></span>  
  
### <a name="parallel-execution"></a><span data-ttu-id="dfea1-165">Wykonywanie równoległe</span><span class="sxs-lookup"><span data-stu-id="dfea1-165">Parallel Execution</span></span>  

 <span data-ttu-id="dfea1-166">Usługa MARS nie została zaprojektowana, aby usunąć wszystkie wymagania dotyczące wielu połączeń w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="dfea1-166">MARS is not designed to remove all requirements for multiple connections in an application.</span></span> <span data-ttu-id="dfea1-167">Jeśli aplikacja wymaga prawdziwie równoległego wykonywania poleceń na serwerze, należy użyć wielu połączeń.</span><span class="sxs-lookup"><span data-stu-id="dfea1-167">If an application needs true parallel execution of commands against a server, multiple connections should be used.</span></span>  
  
 <span data-ttu-id="dfea1-168">Rozważmy na przykład następujący scenariusz.</span><span class="sxs-lookup"><span data-stu-id="dfea1-168">For example, consider the following scenario.</span></span> <span data-ttu-id="dfea1-169">Tworzone są dwa obiekty poleceń: jeden do przetwarzania zestawu wyników i drugi do aktualizowania danych; korzystają one ze wspólnego połączenia za pośrednictwem protokołu MARS.</span><span class="sxs-lookup"><span data-stu-id="dfea1-169">Two command objects are created, one for processing a result set and another for updating data; they share a common connection via MARS.</span></span> <span data-ttu-id="dfea1-170">W tym scenariuszu `Transaction` .`Commit`</span><span class="sxs-lookup"><span data-stu-id="dfea1-170">In this scenario, the `Transaction`.`Commit`</span></span> <span data-ttu-id="dfea1-171">Niepowodzenie w aktualizacji, dopóki wszystkie wyniki nie zostaną odczytane z pierwszego obiektu polecenia, co spowoduje następujący wyjątek:</span><span class="sxs-lookup"><span data-stu-id="dfea1-171">fails on the update until all the results have been read on the first command object, yielding the following exception:</span></span>  
  
 <span data-ttu-id="dfea1-172">Komunikat: kontekst transakcji jest używany przez inną sesję.</span><span class="sxs-lookup"><span data-stu-id="dfea1-172">Message: Transaction context in use by another session.</span></span>  
  
 <span data-ttu-id="dfea1-173">Źródło: Dostawca danych SqlClient platformy .NET</span><span class="sxs-lookup"><span data-stu-id="dfea1-173">Source: .NET SqlClient Data Provider</span></span>  
  
 <span data-ttu-id="dfea1-174">Oczekiwano: (wartość null)</span><span class="sxs-lookup"><span data-stu-id="dfea1-174">Expected: (null)</span></span>  
  
 <span data-ttu-id="dfea1-175">Odebrano: System. Data. SqlClient. SqlException</span><span class="sxs-lookup"><span data-stu-id="dfea1-175">Received: System.Data.SqlClient.SqlException</span></span>  
  
 <span data-ttu-id="dfea1-176">Istnieją trzy opcje obsługi tego scenariusza:</span><span class="sxs-lookup"><span data-stu-id="dfea1-176">There are three options for handling this scenario:</span></span>  
  
1. <span data-ttu-id="dfea1-177">Rozpocznij transakcję po utworzeniu czytnika, aby nie była częścią transakcji.</span><span class="sxs-lookup"><span data-stu-id="dfea1-177">Start the transaction after the reader is created, so that it is not part of the transaction.</span></span> <span data-ttu-id="dfea1-178">Każda aktualizacja zmieni się na własną transakcję.</span><span class="sxs-lookup"><span data-stu-id="dfea1-178">Every update then becomes its own transaction.</span></span>  
  
2. <span data-ttu-id="dfea1-179">Zatwierdź wszystkie prace po zamknięciu czytnika.</span><span class="sxs-lookup"><span data-stu-id="dfea1-179">Commit all work after the reader is closed.</span></span> <span data-ttu-id="dfea1-180">Jest to możliwe w przypadku znacznej partii aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="dfea1-180">This has the potential for a substantial batch of updates.</span></span>  
  
3. <span data-ttu-id="dfea1-181">Nie używaj MARS; Zamiast tego należy użyć oddzielnego połączenia dla każdego obiektu polecenia, tak jak przed MARS.</span><span class="sxs-lookup"><span data-stu-id="dfea1-181">Don't use MARS; instead use a separate connection for each command object as you would have before MARS.</span></span>  
  
### <a name="detecting-mars-support"></a><span data-ttu-id="dfea1-182">Wykrywanie obsługi MARS</span><span class="sxs-lookup"><span data-stu-id="dfea1-182">Detecting MARS Support</span></span>  

 <span data-ttu-id="dfea1-183">Aplikacja może sprawdzić obsługę MARS, odczytując `SqlConnection.ServerVersion` wartość.</span><span class="sxs-lookup"><span data-stu-id="dfea1-183">An application can check for MARS support by reading the `SqlConnection.ServerVersion` value.</span></span> <span data-ttu-id="dfea1-184">Liczba główna powinna wynosić 9 dla SQL Server 2005 i 10 dla SQL Server 2008.</span><span class="sxs-lookup"><span data-stu-id="dfea1-184">The major number should be 9 for SQL Server 2005 and 10 for SQL Server 2008.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="dfea1-185">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="dfea1-185">See also</span></span>

- [<span data-ttu-id="dfea1-186">Wiele aktywnych zestawów wyników (MARS)</span><span class="sxs-lookup"><span data-stu-id="dfea1-186">Multiple Active Result Sets (MARS)</span></span>](multiple-active-result-sets-mars.md)
- [<span data-ttu-id="dfea1-187">Omówienie ADO.NET</span><span class="sxs-lookup"><span data-stu-id="dfea1-187">ADO.NET Overview</span></span>](../ado-net-overview.md)
