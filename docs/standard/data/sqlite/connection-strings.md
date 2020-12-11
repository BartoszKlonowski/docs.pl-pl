---
title: Parametry połączeń
ms.date: 12/08/2020
description: Obsługiwane słowa kluczowe i wartości parametrów połączenia.
ms.openlocfilehash: 35283664c4ac3985d4f517fde77644ab2a891120
ms.sourcegitcommit: 9b877e160c326577e8aa5ead22a937110d80fa44
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2020
ms.locfileid: "97110744"
---
# <a name="connection-strings"></a><span data-ttu-id="84347-103">Parametry połączeń</span><span class="sxs-lookup"><span data-stu-id="84347-103">Connection strings</span></span>

<span data-ttu-id="84347-104">Parametry połączenia służą do określania sposobu łączenia się z bazą danych.</span><span class="sxs-lookup"><span data-stu-id="84347-104">A connection string is used to specify how to connect to the database.</span></span> <span data-ttu-id="84347-105">Parametry połączenia w firmie Microsoft. Data. sqlite są zgodne ze standardową [składnią ADO.NET](../../../framework/data/adonet/connection-strings.md) jako listę słów kluczowych i wartości rozdzielonych średnikami.</span><span class="sxs-lookup"><span data-stu-id="84347-105">Connection strings in Microsoft.Data.Sqlite follow the standard [ADO.NET syntax](../../../framework/data/adonet/connection-strings.md) as a semicolon-separated list of keywords and values.</span></span>

## <a name="keywords"></a><span data-ttu-id="84347-106">Słowa kluczowe</span><span class="sxs-lookup"><span data-stu-id="84347-106">Keywords</span></span>

<span data-ttu-id="84347-107">Następujące słowa kluczowe parametrów połączenia mogą być używane z firmą Microsoft. Data. sqlite:</span><span class="sxs-lookup"><span data-stu-id="84347-107">The following connection string keywords can be used with Microsoft.Data.Sqlite:</span></span>

### <a name="data-source"></a><span data-ttu-id="84347-108">Źródło danych</span><span class="sxs-lookup"><span data-stu-id="84347-108">Data source</span></span>

<span data-ttu-id="84347-109">Ścieżka do pliku bazy danych.</span><span class="sxs-lookup"><span data-stu-id="84347-109">The path to the database file.</span></span> <span data-ttu-id="84347-110">*Źródła danych* (bez spacji) i *filename* są aliasami tego słowa kluczowego.</span><span class="sxs-lookup"><span data-stu-id="84347-110">*DataSource* (without a space) and *Filename* are aliases of this keyword.</span></span>

<span data-ttu-id="84347-111">SQLite traktuje ścieżki względem bieżącego katalogu roboczego.</span><span class="sxs-lookup"><span data-stu-id="84347-111">SQLite treats paths relative to the current working directory.</span></span> <span data-ttu-id="84347-112">Można również określić ścieżki bezwzględne.</span><span class="sxs-lookup"><span data-stu-id="84347-112">Absolute paths can also be specified.</span></span>

<span data-ttu-id="84347-113">Jeśli ta wartość jest **pusta**, program SQLite tworzy tymczasową bazę danych na dysku, która jest usuwana po zamknięciu połączenia.</span><span class="sxs-lookup"><span data-stu-id="84347-113">If **empty**, SQLite creates a temporary on-disk database that's deleted when the connection is closed.</span></span>

<span data-ttu-id="84347-114">Jeśli `:memory:` używana jest baza danych w pamięci.</span><span class="sxs-lookup"><span data-stu-id="84347-114">If `:memory:`, an in-memory database is used.</span></span> <span data-ttu-id="84347-115">Aby uzyskać więcej informacji, zobacz [bazy danych w pamięci](in-memory-databases.md).</span><span class="sxs-lookup"><span data-stu-id="84347-115">For more information, see [In-Memory databases](in-memory-databases.md).</span></span>

<span data-ttu-id="84347-116">Ścieżki, które zaczynają się od `|DataDirectory|` ciągu podstawiania są traktowane tak samo jak ścieżki względne.</span><span class="sxs-lookup"><span data-stu-id="84347-116">Paths that start with the `|DataDirectory|` substitution string are treated the same as relative paths.</span></span> <span data-ttu-id="84347-117">W przypadku ustawienia ścieżki są tworzone względem wartości właściwości domena aplikacji usługi DataDirectory.</span><span class="sxs-lookup"><span data-stu-id="84347-117">If set, paths are made relative to the DataDirectory application domain property value.</span></span>

<span data-ttu-id="84347-118">To słowo kluczowe obsługuje również [nazwy plików URI](https://www.sqlite.org/uri.html).</span><span class="sxs-lookup"><span data-stu-id="84347-118">This keyword also supports [URI Filenames](https://www.sqlite.org/uri.html).</span></span>

### <a name="mode"></a><span data-ttu-id="84347-119">Tryb</span><span class="sxs-lookup"><span data-stu-id="84347-119">Mode</span></span>

<span data-ttu-id="84347-120">Tryb połączenia.</span><span class="sxs-lookup"><span data-stu-id="84347-120">The connection mode.</span></span>

| <span data-ttu-id="84347-121">Wartość</span><span class="sxs-lookup"><span data-stu-id="84347-121">Value</span></span>           | <span data-ttu-id="84347-122">Opis</span><span class="sxs-lookup"><span data-stu-id="84347-122">Description</span></span>                                                                                        |
| --------------- | -------------------------------------------------------------------------------------------------- |
| <span data-ttu-id="84347-123">ReadWriteCreate</span><span class="sxs-lookup"><span data-stu-id="84347-123">ReadWriteCreate</span></span> | <span data-ttu-id="84347-124">Otwiera bazę danych do odczytu i zapisu, a następnie tworzy ją, jeśli nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="84347-124">Opens the database for reading and writing, and creates it if it doesn't exist.</span></span> <span data-ttu-id="84347-125">Jest to opcja domyślna.</span><span class="sxs-lookup"><span data-stu-id="84347-125">This is the default.</span></span> |
| <span data-ttu-id="84347-126">Odczyt/zapis</span><span class="sxs-lookup"><span data-stu-id="84347-126">ReadWrite</span></span>       | <span data-ttu-id="84347-127">Otwiera bazę danych do odczytu i zapisu.</span><span class="sxs-lookup"><span data-stu-id="84347-127">Opens the database for reading and writing.</span></span>                                                        |
| <span data-ttu-id="84347-128">ReadOnly</span><span class="sxs-lookup"><span data-stu-id="84347-128">ReadOnly</span></span>        | <span data-ttu-id="84347-129">Otwiera bazę danych w trybie tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="84347-129">Opens the database in read-only mode.</span></span>                                                              |
| <span data-ttu-id="84347-130">Memory (Pamięć)</span><span class="sxs-lookup"><span data-stu-id="84347-130">Memory</span></span>          | <span data-ttu-id="84347-131">Otwiera bazę danych w pamięci.</span><span class="sxs-lookup"><span data-stu-id="84347-131">Opens an in-memory database.</span></span>                                                                       |

### <a name="cache"></a><span data-ttu-id="84347-132">Pamięć podręczna</span><span class="sxs-lookup"><span data-stu-id="84347-132">Cache</span></span>

<span data-ttu-id="84347-133">Tryb buforowania używany przez połączenie.</span><span class="sxs-lookup"><span data-stu-id="84347-133">The caching mode used by the connection.</span></span>

| <span data-ttu-id="84347-134">Wartość</span><span class="sxs-lookup"><span data-stu-id="84347-134">Value</span></span>   | <span data-ttu-id="84347-135">Opis</span><span class="sxs-lookup"><span data-stu-id="84347-135">Description</span></span>                                                                                    |
| ------- | ---------------------------------------------------------------------------------------------- |
| <span data-ttu-id="84347-136">Domyślny</span><span class="sxs-lookup"><span data-stu-id="84347-136">Default</span></span> | <span data-ttu-id="84347-137">Używa domyślnego trybu podstawowej biblioteki programu SQLite.</span><span class="sxs-lookup"><span data-stu-id="84347-137">Uses the default mode of the underlying SQLite library.</span></span> <span data-ttu-id="84347-138">Jest to opcja domyślna.</span><span class="sxs-lookup"><span data-stu-id="84347-138">This is the default.</span></span>                   |
| <span data-ttu-id="84347-139">Prywatny</span><span class="sxs-lookup"><span data-stu-id="84347-139">Private</span></span> | <span data-ttu-id="84347-140">Każde połączenie używa prywatnej pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="84347-140">Each connection uses a private cache.</span></span>                                                          |
| <span data-ttu-id="84347-141">Udostępniona</span><span class="sxs-lookup"><span data-stu-id="84347-141">Shared</span></span>  | <span data-ttu-id="84347-142">Połączenia korzystają z pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="84347-142">Connections share a cache.</span></span> <span data-ttu-id="84347-143">Ten tryb pozwala zmienić zachowanie blokowania transakcji i tabel.</span><span class="sxs-lookup"><span data-stu-id="84347-143">This mode can change the behavior of transaction and table locking.</span></span> |

### <a name="password"></a><span data-ttu-id="84347-144">Hasło</span><span class="sxs-lookup"><span data-stu-id="84347-144">Password</span></span>

<span data-ttu-id="84347-145">Klucz szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="84347-145">The encryption key.</span></span> <span data-ttu-id="84347-146">Gdy ta `PRAGMA key` wartość jest określona, jest wysyłana natychmiast po otwarciu połączenia.</span><span class="sxs-lookup"><span data-stu-id="84347-146">When specified, `PRAGMA key` is sent immediately after opening the connection.</span></span>

> [!WARNING]
> <span data-ttu-id="84347-147">Hasło nie ma znaczenia, jeśli szyfrowanie nie jest obsługiwane przez natywną bibliotekę oprogramowania SQLite.</span><span class="sxs-lookup"><span data-stu-id="84347-147">Password has no effect when encryption isn't supported by the native SQLite library.</span></span>

> [!NOTE]
> <span data-ttu-id="84347-148">Słowo kluczowe Password zostało dodane w wersji 3,0.</span><span class="sxs-lookup"><span data-stu-id="84347-148">The Password keyword was added in version 3.0.</span></span>

### <a name="foreign-keys"></a><span data-ttu-id="84347-149">Klucze obce</span><span class="sxs-lookup"><span data-stu-id="84347-149">Foreign Keys</span></span>

<span data-ttu-id="84347-150">Wartość wskazująca, czy należy włączyć ograniczenia klucza obcego.</span><span class="sxs-lookup"><span data-stu-id="84347-150">A value indicating whether to enable foreign key constraints.</span></span>

> [!NOTE]
> <span data-ttu-id="84347-151">Słowo kluczowe kluczy obcych zostało dodane w wersji 3,0.</span><span class="sxs-lookup"><span data-stu-id="84347-151">The Foreign Keys keyword was added in version 3.0.</span></span>

| <span data-ttu-id="84347-152">Wartość</span><span class="sxs-lookup"><span data-stu-id="84347-152">Value</span></span>   | <span data-ttu-id="84347-153">Opis</span><span class="sxs-lookup"><span data-stu-id="84347-153">Description</span></span>
| ------- | --- |
| <span data-ttu-id="84347-154">Prawda</span><span class="sxs-lookup"><span data-stu-id="84347-154">True</span></span>    | <span data-ttu-id="84347-155">Wysyła `PRAGMA foreign_keys = 1` natychmiast po otwarciu połączenia.</span><span class="sxs-lookup"><span data-stu-id="84347-155">Sends `PRAGMA foreign_keys = 1` immediately after opening the connection.</span></span>
| <span data-ttu-id="84347-156">Fałsz</span><span class="sxs-lookup"><span data-stu-id="84347-156">False</span></span>   | <span data-ttu-id="84347-157">Wysyła `PRAGMA foreign_keys = 0` natychmiast po otwarciu połączenia.</span><span class="sxs-lookup"><span data-stu-id="84347-157">Sends `PRAGMA foreign_keys = 0` immediately after opening the connection.</span></span>
| <span data-ttu-id="84347-158">ciągiem</span><span class="sxs-lookup"><span data-stu-id="84347-158">(empty)</span></span> | <span data-ttu-id="84347-159">Nie wysyła `PRAGMA foreign_keys` .</span><span class="sxs-lookup"><span data-stu-id="84347-159">Doesn't send `PRAGMA foreign_keys`.</span></span> <span data-ttu-id="84347-160">Jest to opcja domyślna.</span><span class="sxs-lookup"><span data-stu-id="84347-160">This is the default.</span></span> |

<span data-ttu-id="84347-161">Nie ma potrzeby włączania kluczy obcych, jeśli tak, jak w e_sqlite3, SQLITE_DEFAULT_FOREIGN_KEYS został użyty do skompilowania natywnej biblioteki programu SQLite.</span><span class="sxs-lookup"><span data-stu-id="84347-161">There's no need enable foreign keys if, like in e_sqlite3, SQLITE_DEFAULT_FOREIGN_KEYS was used to compile the native SQLite library.</span></span>

### <a name="recursive-triggers"></a><span data-ttu-id="84347-162">Wyzwalacze cykliczne</span><span class="sxs-lookup"><span data-stu-id="84347-162">Recursive triggers</span></span>

<span data-ttu-id="84347-163">Wartość wskazująca, czy włączyć Wyzwalacze cykliczne.</span><span class="sxs-lookup"><span data-stu-id="84347-163">A value that indicates whether to enable recursive triggers.</span></span>

> [!NOTE]
> <span data-ttu-id="84347-164">Słowo kluczowe wyzwalaczy cyklicznych zostało dodane w wersji 3,0.</span><span class="sxs-lookup"><span data-stu-id="84347-164">The Recursive Triggers keyword was added in version 3.0.</span></span>

| <span data-ttu-id="84347-165">Wartość</span><span class="sxs-lookup"><span data-stu-id="84347-165">Value</span></span> | <span data-ttu-id="84347-166">Opis</span><span class="sxs-lookup"><span data-stu-id="84347-166">Description</span></span>                                                                 |
| ----- | --------------------------------------------------------------------------- |
| <span data-ttu-id="84347-167">Prawda</span><span class="sxs-lookup"><span data-stu-id="84347-167">True</span></span>  | <span data-ttu-id="84347-168">Wysyła `PRAGMA recursive_triggers` natychmiast po otwarciu połączenia.</span><span class="sxs-lookup"><span data-stu-id="84347-168">Sends `PRAGMA recursive_triggers` immediately after opening the connection.</span></span> |
| <span data-ttu-id="84347-169">Fałsz</span><span class="sxs-lookup"><span data-stu-id="84347-169">False</span></span> | <span data-ttu-id="84347-170">Nie wysyła `PRAGMA recursive_triggers` .</span><span class="sxs-lookup"><span data-stu-id="84347-170">Doesn't send `PRAGMA recursive_triggers`.</span></span> <span data-ttu-id="84347-171">Jest to opcja domyślna.</span><span class="sxs-lookup"><span data-stu-id="84347-171">This is the default.</span></span>              |

## <a name="connection-string-builder"></a><span data-ttu-id="84347-172">Konstruktor parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="84347-172">Connection string builder</span></span>

<span data-ttu-id="84347-173">Można użyć <xref:Microsoft.Data.Sqlite.SqliteConnectionStringBuilder> jako jednoznacznie określonego sposobu tworzenia parametrów połączenia.</span><span class="sxs-lookup"><span data-stu-id="84347-173">You can use <xref:Microsoft.Data.Sqlite.SqliteConnectionStringBuilder> as a strongly typed way of creating connection strings.</span></span> <span data-ttu-id="84347-174">Można go również użyć, aby zapobiec atakom polegającym na iniekcji parametrów połączenia.</span><span class="sxs-lookup"><span data-stu-id="84347-174">It can also be used to prevent connection string injection attacks.</span></span>

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/EncryptionSample/Program.cs?name=snippet_ConnectionStringBuilder)]

## <a name="examples"></a><span data-ttu-id="84347-175">Przykłady</span><span class="sxs-lookup"><span data-stu-id="84347-175">Examples</span></span>

### <a name="basic"></a><span data-ttu-id="84347-176">Podstawowa</span><span class="sxs-lookup"><span data-stu-id="84347-176">Basic</span></span>

<span data-ttu-id="84347-177">Podstawowe parametry połączenia z udostępnioną pamięcią podręczną w celu zwiększenia współbieżności.</span><span class="sxs-lookup"><span data-stu-id="84347-177">A basic connection string with a shared cache for improved concurrency.</span></span>

```connectionstring
Data Source=Application.db;Cache=Shared
```

### <a name="encrypted"></a><span data-ttu-id="84347-178">Zaszyfrowane</span><span class="sxs-lookup"><span data-stu-id="84347-178">Encrypted</span></span>

<span data-ttu-id="84347-179">Zaszyfrowana baza danych.</span><span class="sxs-lookup"><span data-stu-id="84347-179">An encrypted database.</span></span>

```connectionstring
Data Source=Encrypted.db;Password=MyEncryptionKey
```

### <a name="read-only"></a><span data-ttu-id="84347-180">Tylko odczyt</span><span class="sxs-lookup"><span data-stu-id="84347-180">Read-only</span></span>

<span data-ttu-id="84347-181">Baza danych tylko do odczytu, która nie może być modyfikowana przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="84347-181">A read-only database that cannot be modified by the app.</span></span>

```connectionstring
Data Source=Reference.db;Mode=ReadOnly
```

### <a name="in-memory"></a><span data-ttu-id="84347-182">W pamięci</span><span class="sxs-lookup"><span data-stu-id="84347-182">In-memory</span></span>

<span data-ttu-id="84347-183">Prywatna baza danych w pamięci.</span><span class="sxs-lookup"><span data-stu-id="84347-183">A private, in-memory database.</span></span>

```connectionstring
Data Source=:memory:
```

### <a name="sharable-in-memory"></a><span data-ttu-id="84347-184">Współużytkowana pamięć</span><span class="sxs-lookup"><span data-stu-id="84347-184">Sharable in-memory</span></span>

<span data-ttu-id="84347-185">Współużytkowana baza danych w pamięci identyfikowana przy użyciu nazwy, którą można *udostępniać*.</span><span class="sxs-lookup"><span data-stu-id="84347-185">A sharable, in-memory database identified by the name *Sharable*.</span></span>

```connectionstring
Data Source=Sharable;Mode=Memory;Cache=Shared
```

## <a name="see-also"></a><span data-ttu-id="84347-186">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="84347-186">See also</span></span>

* [<span data-ttu-id="84347-187">Parametry połączenia w ADO.NET</span><span class="sxs-lookup"><span data-stu-id="84347-187">Connection Strings in ADO.NET</span></span>](../../../framework/data/adonet/connection-strings.md)
* [<span data-ttu-id="84347-188">Bazy danych w pamięci</span><span class="sxs-lookup"><span data-stu-id="84347-188">In-Memory databases</span></span>](in-memory-databases.md)
* [<span data-ttu-id="84347-189">Transakcje</span><span class="sxs-lookup"><span data-stu-id="84347-189">Transactions</span></span>](transactions.md)
