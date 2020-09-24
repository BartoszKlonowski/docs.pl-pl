---
title: Dane daty i godziny
description: Dowiedz się więcej o typach danych do obsługi informacji o dacie i godzinie w .NET Framework Dostawca danych dla SQL Server.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 6f5ff56a-a57e-49d7-8ae9-bbed697e42e3
ms.openlocfilehash: 6fe047fc672a2b42f886e81dcace91042a552932
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91156319"
---
# <a name="date-and-time-data"></a><span data-ttu-id="8e925-103">Dane daty i godziny</span><span class="sxs-lookup"><span data-stu-id="8e925-103">Date and Time Data</span></span>

<span data-ttu-id="8e925-104">SQL Server 2008 wprowadza nowe typy danych do obsługi informacji o dacie i godzinie.</span><span class="sxs-lookup"><span data-stu-id="8e925-104">SQL Server 2008 introduces new data types for handling date and time information.</span></span> <span data-ttu-id="8e925-105">Nowe typy danych obejmują oddzielne typy dat i godzin oraz rozszerzone typy danych o większej dokładności, precyzji i świadomości strefy czasowej.</span><span class="sxs-lookup"><span data-stu-id="8e925-105">The new data types include separate types for date and time, and expanded data types with greater range, precision, and time-zone awareness.</span></span> <span data-ttu-id="8e925-106">Począwszy od .NET Framework w wersji 3,5 Service Pack (SP) 1, .NET Framework Dostawca danych dla SQL Server ( <xref:System.Data.SqlClient> ) zapewnia pełną obsługę wszystkich nowych funkcji aparatu bazy danych SQL Server 2008.</span><span class="sxs-lookup"><span data-stu-id="8e925-106">Starting with the .NET Framework version 3.5 Service Pack (SP) 1, the .NET Framework Data Provider for SQL Server (<xref:System.Data.SqlClient>) provides full support for all the new features of the SQL Server 2008 Database Engine.</span></span> <span data-ttu-id="8e925-107">Aby korzystać z nowych funkcji w programie SqlClient, należy zainstalować .NET Framework 3,5 SP1 (lub nowsze).</span><span class="sxs-lookup"><span data-stu-id="8e925-107">You must install the .NET Framework 3.5 SP1 (or later) to use these new features with SqlClient.</span></span>  
  
 <span data-ttu-id="8e925-108">Wersje SQL Server starszej niż SQL Server 2008 mają tylko dwa typy danych do pracy z wartościami daty i godziny: `datetime` i `smalldatetime` .</span><span class="sxs-lookup"><span data-stu-id="8e925-108">Versions of SQL Server earlier than SQL Server 2008 only had two data types for working with date and time values: `datetime` and `smalldatetime`.</span></span> <span data-ttu-id="8e925-109">Oba te typy danych zawierają zarówno wartość daty, jak i wartość czasu, co utrudnia działanie tylko wartości daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="8e925-109">Both of these data types contain both the date value and a time value, which makes it difficult to work with only date or only time values.</span></span> <span data-ttu-id="8e925-110">Ponadto te typy danych obsługują tylko daty, które wystąpiły po wprowadzeniu kalendarza gregoriańskiego w Anglii w 1753.</span><span class="sxs-lookup"><span data-stu-id="8e925-110">Also, these data types only support dates that occur after the introduction of the Gregorian calendar in England in 1753.</span></span> <span data-ttu-id="8e925-111">Inne ograniczenie polega na tym, że te starsze typy danych nie są świadome strefy czasowej, co utrudnia pracy z danymi, które pochodzą z wielu stref czasowych.</span><span class="sxs-lookup"><span data-stu-id="8e925-111">Another limitation is that these older data types are not time-zone aware, which makes it difficult to work with data that originates from multiple time zones.</span></span>  
  
 <span data-ttu-id="8e925-112">Kompletna dokumentacja typów danych SQL Server jest dostępna w SQL Server Books Online.</span><span class="sxs-lookup"><span data-stu-id="8e925-112">Complete documentation for SQL Server data types is available in SQL Server Books Online.</span></span> <span data-ttu-id="8e925-113">W poniższej tabeli przedstawiono tematy dotyczące poszczególnych wersji dla danych daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="8e925-113">The following table lists the version-specific entry-level topics for date and time data.</span></span>  
  
 <span data-ttu-id="8e925-114">**Dokumentacja SQL Server**</span><span class="sxs-lookup"><span data-stu-id="8e925-114">**SQL Server documentation**</span></span>  
  
1. <span data-ttu-id="8e925-115">[Korzystanie z danych daty i godziny](/previous-versions/sql/sql-server-2008/ms180878(v=sql.100))</span><span class="sxs-lookup"><span data-stu-id="8e925-115">[Using Date and Time Data](/previous-versions/sql/sql-server-2008/ms180878(v=sql.100))</span></span>  
  
## <a name="datetime-data-types-introduced-in-sql-server-2008"></a><span data-ttu-id="8e925-116">Typy danych daty/godziny wprowadzone w SQL Server 2008</span><span class="sxs-lookup"><span data-stu-id="8e925-116">Date/Time Data Types Introduced in SQL Server 2008</span></span>  

 <span data-ttu-id="8e925-117">W poniższej tabeli opisano nowe typy danych daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="8e925-117">The following table describes the new date and time data types.</span></span>  
  
|<span data-ttu-id="8e925-118">Typ danych SQL Server</span><span class="sxs-lookup"><span data-stu-id="8e925-118">SQL Server data type</span></span>|<span data-ttu-id="8e925-119">Opis</span><span class="sxs-lookup"><span data-stu-id="8e925-119">Description</span></span>|  
|--------------------------|-----------------|  
|`date`|<span data-ttu-id="8e925-120">`date`Typ danych ma zakres od 1 stycznia do 31 grudnia 9999 z dokładnością wynoszącą 1 dzień.</span><span class="sxs-lookup"><span data-stu-id="8e925-120">The `date` data type has a range of January 1, 01 through December 31, 9999 with an accuracy of 1 day.</span></span> <span data-ttu-id="8e925-121">Wartość domyślna to 1 stycznia 1900.</span><span class="sxs-lookup"><span data-stu-id="8e925-121">The default value is January 1, 1900.</span></span> <span data-ttu-id="8e925-122">Rozmiar magazynu wynosi 3 bajty.</span><span class="sxs-lookup"><span data-stu-id="8e925-122">The storage size is 3 bytes.</span></span>|  
|`time`|<span data-ttu-id="8e925-123">`time`Typ danych przechowuje tylko wartości czasu w oparciu o zegar 24-godzinny.</span><span class="sxs-lookup"><span data-stu-id="8e925-123">The `time` data type stores time values only, based on a 24-hour clock.</span></span> <span data-ttu-id="8e925-124">`time`Typ danych ma zakres 00:00:00.0000000 do 23:59:59.9999999 z dokładnością do 100 nanosekund.</span><span class="sxs-lookup"><span data-stu-id="8e925-124">The `time` data type has a range of 00:00:00.0000000 through 23:59:59.9999999 with an accuracy of 100 nanoseconds.</span></span> <span data-ttu-id="8e925-125">Wartość domyślna to 00:00:00.0000000 (północ).</span><span class="sxs-lookup"><span data-stu-id="8e925-125">The default value is 00:00:00.0000000 (midnight).</span></span> <span data-ttu-id="8e925-126">`time`Typ danych obsługuje zdefiniowaną przez użytkownika precyzję dziesiętną, a rozmiar magazynu różni się od 3 do 6 bajtów na podstawie określonej precyzji.</span><span class="sxs-lookup"><span data-stu-id="8e925-126">The `time` data type supports user-defined fractional second precision, and the storage size varies from 3 to 6 bytes, based on the precision specified.</span></span>|  
|`datetime2`|<span data-ttu-id="8e925-127">`datetime2`Typ danych łączy zakres i precyzję `date` `time` typów danych i w jeden typ danych.</span><span class="sxs-lookup"><span data-stu-id="8e925-127">The `datetime2` data type combines the range and precision of the `date` and `time` data types into a single data type.</span></span><br /><br /> <span data-ttu-id="8e925-128">Wartości domyślne i formaty literałów ciągów są takie same jak te zdefiniowane w `date` typach i `time` .</span><span class="sxs-lookup"><span data-stu-id="8e925-128">The default values and string literal formats are the same as those defined in the `date` and `time` data types.</span></span>|  
|`datetimeoffset`|<span data-ttu-id="8e925-129">`datetimeoffset`Typ danych zawiera wszystkie funkcje z `datetime2` dodatkowym przesunięciem strefy czasowej.</span><span class="sxs-lookup"><span data-stu-id="8e925-129">The `datetimeoffset` data type has all the features of `datetime2` with an additional time zone offset.</span></span> <span data-ttu-id="8e925-130">Przesunięcie strefy czasowej jest reprezentowane jako [+&#124;-] HH: MM.</span><span class="sxs-lookup"><span data-stu-id="8e925-130">The time zone offset is represented as [+&#124;-] HH:MM.</span></span> <span data-ttu-id="8e925-131">HH to 2 cyfry od 00 do 14, które reprezentują liczbę godzin w przesunięciu strefy czasowej.</span><span class="sxs-lookup"><span data-stu-id="8e925-131">HH is 2 digits ranging from 00 to 14 that represent the number of hours in the time zone offset.</span></span> <span data-ttu-id="8e925-132">MM to 2 cyfry od 00 do 59, które reprezentują liczbę dodatkowych minut w przesunięciu strefy czasowej.</span><span class="sxs-lookup"><span data-stu-id="8e925-132">MM is 2 digits ranging from 00 to 59 that represent the number of additional minutes in the time zone offset.</span></span> <span data-ttu-id="8e925-133">Formaty czasu są obsługiwane w 100 nanosekundach.</span><span class="sxs-lookup"><span data-stu-id="8e925-133">Time formats are supported to 100 nanoseconds.</span></span> <span data-ttu-id="8e925-134">Obowiązkowe + lub-znak wskazuje, czy przesunięcie strefy czasowej jest dodawane lub odejmowane od czasu UTC (uniwersalna Współrzędna czasu Greenwich lub czasu GMT), aby uzyskać czas lokalny.</span><span class="sxs-lookup"><span data-stu-id="8e925-134">The mandatory + or - sign indicates whether the time zone offset is added or subtracted from UTC (Universal Time Coordinate or Greenwich Mean Time) to obtain the local time.</span></span>|  
  
> [!NOTE]
> <span data-ttu-id="8e925-135">Aby uzyskać więcej informacji na temat używania `Type System Version` słowa kluczowego, zobacz <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A> .</span><span class="sxs-lookup"><span data-stu-id="8e925-135">For more information about using the `Type System Version` keyword, see <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A>.</span></span>  
  
## <a name="date-format-and-date-order"></a><span data-ttu-id="8e925-136">Format daty i kolejność dat</span><span class="sxs-lookup"><span data-stu-id="8e925-136">Date Format and Date Order</span></span>  

 <span data-ttu-id="8e925-137">Sposób, w jaki SQL Server analizuje wartości daty i godziny, zależy nie tylko od wersji systemu typu i wersji serwera, ale również w domyślnym języku i ustawieniach formatowania serwera.</span><span class="sxs-lookup"><span data-stu-id="8e925-137">How SQL Server parses date and time values depends not only on the type system version and server version, but also on the server's default language and format settings.</span></span> <span data-ttu-id="8e925-138">Ciąg daty, który działa w przypadku formatów daty jednego języka może być nierozpoznawalny, jeśli zapytanie jest wykonywane przez połączenie, które używa innego ustawienia język i format daty.</span><span class="sxs-lookup"><span data-stu-id="8e925-138">A date string that works for the date formats of one language might be unrecognizable if the query is executed by a connection that uses a different language and date format setting.</span></span>  
  
 <span data-ttu-id="8e925-139">Instrukcja języka Transact-SQL SET niejawnie ustawia DATEFORMAT, który określa kolejność części daty.</span><span class="sxs-lookup"><span data-stu-id="8e925-139">The Transact-SQL SET LANGUAGE statement implicitly sets the DATEFORMAT that determines the order of the date parts.</span></span> <span data-ttu-id="8e925-140">Można użyć instrukcji DATEFORMAT języka Transact-SQL w połączeniu, aby odróżnić wartości daty przez porządkowanie części daty w MDR, DMY, YMD, YDM, MYD lub DYM Order.</span><span class="sxs-lookup"><span data-stu-id="8e925-140">You can use the SET DATEFORMAT Transact-SQL statement on a connection to disambiguate date values by ordering the date parts in MDY, DMY, YMD, YDM, MYD, or DYM order.</span></span>  
  
 <span data-ttu-id="8e925-141">Jeśli nie określisz żadnych DATEFORMAT dla połączenia, SQL Server używa języka domyślnego skojarzonego z połączeniem.</span><span class="sxs-lookup"><span data-stu-id="8e925-141">If you do not specify any DATEFORMAT for the connection, SQL Server uses the default language associated with the connection.</span></span> <span data-ttu-id="8e925-142">Na przykład ciąg daty "01/02/03" będzie interpretowany jako MDR (2 stycznia 2003) na serwerze z ustawieniem języka Stany Zjednoczone angielski i jako DMY (1 lutego 2003) na serwerze z ustawieniem języka brytyjskiego alfabetu angielskiego.</span><span class="sxs-lookup"><span data-stu-id="8e925-142">For example, a date string of '01/02/03' would be interpreted as MDY (January 2, 2003) on a server with a language setting of United States English, and as DMY (February 1, 2003) on a server with a language setting of British English.</span></span> <span data-ttu-id="8e925-143">Rok jest określany za pomocą reguły odcięcia roku SQL Server, która definiuje datę końcową przypisywania wartości wieku.</span><span class="sxs-lookup"><span data-stu-id="8e925-143">The year is determined by using SQL Server's cutoff year rule, which defines the cutoff date for assigning the century value.</span></span> <span data-ttu-id="8e925-144">Aby uzyskać więcej informacji, zobacz [dwubajtowa opcja odcięcia roku](/sql/database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option).</span><span class="sxs-lookup"><span data-stu-id="8e925-144">For more information, see [two digit year cutoff Option](/sql/database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option).</span></span>  
  
> [!NOTE]
> <span data-ttu-id="8e925-145">Format daty YDM nie jest obsługiwany podczas konwersji z formatu ciągu na,, `date` `time` `datetime2` , lub `datetimeoffset` .</span><span class="sxs-lookup"><span data-stu-id="8e925-145">The YDM date format is not supported when converting from a string format to `date`, `time`, `datetime2`, or `datetimeoffset`.</span></span>  
  
 <span data-ttu-id="8e925-146">Aby uzyskać więcej informacji o tym, jak SQL Server interpretuje dane daty i godziny, zobacz [Korzystanie z danych daty i godziny](/previous-versions/sql/sql-server-2008/ms180878(v=sql.100)).</span><span class="sxs-lookup"><span data-stu-id="8e925-146">For more information about how SQL Server interprets date and time data, see [Using Date and Time Data](/previous-versions/sql/sql-server-2008/ms180878(v=sql.100)).</span></span>  
  
## <a name="datetime-data-types-and-parameters"></a><span data-ttu-id="8e925-147">Typy danych daty/godziny i parametry</span><span class="sxs-lookup"><span data-stu-id="8e925-147">Date/Time Data Types and Parameters</span></span>  

 <span data-ttu-id="8e925-148">Następujące wyliczenia zostały dodane do programu <xref:System.Data.SqlDbType> w celu obsługi nowych typów danych daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="8e925-148">The following enumerations have been added to <xref:System.Data.SqlDbType> to support the new date and time data types.</span></span>  
  
- `SqlDbType.Date`  
  
- `SqlDbType.Time`  
  
- `SqlDbType.DateTime2`  
  
- `SqlDbType.DateTimeOffSet`  

<span data-ttu-id="8e925-149">Możesz określić typ danych z przy <xref:System.Data.SqlClient.SqlParameter> użyciu jednego z wcześniejszych <xref:System.Data.SqlDbType> wyliczeń.</span><span class="sxs-lookup"><span data-stu-id="8e925-149">You can specify the data type of a <xref:System.Data.SqlClient.SqlParameter> by using one of the preceding <xref:System.Data.SqlDbType> enumerations.</span></span>

> [!NOTE]
> <span data-ttu-id="8e925-150">Nie można ustawić `DbType` właściwości `SqlParameter` na `SqlDbType.Date` .</span><span class="sxs-lookup"><span data-stu-id="8e925-150">You cannot set the `DbType` property of a `SqlParameter` to `SqlDbType.Date`.</span></span>

 <span data-ttu-id="8e925-151">Można również określić typ <xref:System.Data.SqlClient.SqlParameter> ogólny, ustawiając <xref:System.Data.SqlClient.SqlParameter.DbType%2A> Właściwość `SqlParameter` obiektu na określoną <xref:System.Data.DbType> wartość wyliczenia.</span><span class="sxs-lookup"><span data-stu-id="8e925-151">You can also specify the type of a <xref:System.Data.SqlClient.SqlParameter> generically by setting the <xref:System.Data.SqlClient.SqlParameter.DbType%2A> property of a `SqlParameter` object to a particular <xref:System.Data.DbType> enumeration value.</span></span> <span data-ttu-id="8e925-152">Następujące wartości wyliczenia zostały dodane do programu <xref:System.Data.DbType> w celu obsługi `datetime2` `datetimeoffset` typów danych i:</span><span class="sxs-lookup"><span data-stu-id="8e925-152">The following enumeration values have been added to <xref:System.Data.DbType> to support the `datetime2` and `datetimeoffset` data types:</span></span>  
  
- <span data-ttu-id="8e925-153">DbType. DateTime2</span><span class="sxs-lookup"><span data-stu-id="8e925-153">DbType.DateTime2</span></span>  
  
- <span data-ttu-id="8e925-154">DbType. DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="8e925-154">DbType.DateTimeOffset</span></span>  
  
 <span data-ttu-id="8e925-155">Te nowe wyliczenia uzupełniają `Date` wyliczenia, `Time` i, `DateTime` które istniały we wcześniejszych wersjach .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="8e925-155">These new enumerations supplement the `Date`, `Time`, and `DateTime` enumerations, which existed in earlier versions of the .NET Framework.</span></span>  
  
 <span data-ttu-id="8e925-156">Typ dostawcy danych .NET Framework obiektu parametru jest wywnioskowany na podstawie typu .NET Framework wartości obiektu parametru lub z `DbType` obiektu Parameter.</span><span class="sxs-lookup"><span data-stu-id="8e925-156">The .NET Framework data provider type of a parameter object is inferred from the .NET Framework type of the value of the parameter object, or from the `DbType` of the parameter object.</span></span> <span data-ttu-id="8e925-157">Nie <xref:System.Data.SqlTypes> wprowadzono nowych typów danych w celu obsługi nowych typów danych daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="8e925-157">No new <xref:System.Data.SqlTypes> data types have been introduced to support the new date and time data types.</span></span> <span data-ttu-id="8e925-158">W poniższej tabeli opisano mapowania między typami danych daty i godziny SQL Server 2008 oraz typami danych CLR.</span><span class="sxs-lookup"><span data-stu-id="8e925-158">The following table describes the mappings between the SQL Server 2008 date and time data types and the CLR data types.</span></span>  
  
|<span data-ttu-id="8e925-159">Typ danych SQL Server</span><span class="sxs-lookup"><span data-stu-id="8e925-159">SQL Server data type</span></span>|<span data-ttu-id="8e925-160">Typ programu .NET Framework</span><span class="sxs-lookup"><span data-stu-id="8e925-160">.NET Framework type</span></span>|<span data-ttu-id="8e925-161">System. Data. SqlDbType</span><span class="sxs-lookup"><span data-stu-id="8e925-161">System.Data.SqlDbType</span></span>|<span data-ttu-id="8e925-162">System. Data. DbType</span><span class="sxs-lookup"><span data-stu-id="8e925-162">System.Data.DbType</span></span>|  
|--------------------------|-------------------------|---------------------------|------------------------|  
|<span data-ttu-id="8e925-163">data</span><span class="sxs-lookup"><span data-stu-id="8e925-163">date</span></span>|<span data-ttu-id="8e925-164">System. DateTime</span><span class="sxs-lookup"><span data-stu-id="8e925-164">System.DateTime</span></span>|<span data-ttu-id="8e925-165">Date</span><span class="sxs-lookup"><span data-stu-id="8e925-165">Date</span></span>|<span data-ttu-id="8e925-166">Date</span><span class="sxs-lookup"><span data-stu-id="8e925-166">Date</span></span>|  
|<span data-ttu-id="8e925-167">time</span><span class="sxs-lookup"><span data-stu-id="8e925-167">time</span></span>|<span data-ttu-id="8e925-168">System. TimeSpan</span><span class="sxs-lookup"><span data-stu-id="8e925-168">System.TimeSpan</span></span>|<span data-ttu-id="8e925-169">Godzina</span><span class="sxs-lookup"><span data-stu-id="8e925-169">Time</span></span>|<span data-ttu-id="8e925-170">Godzina</span><span class="sxs-lookup"><span data-stu-id="8e925-170">Time</span></span>|  
|<span data-ttu-id="8e925-171">datetime2</span><span class="sxs-lookup"><span data-stu-id="8e925-171">datetime2</span></span>|<span data-ttu-id="8e925-172">System. DateTime</span><span class="sxs-lookup"><span data-stu-id="8e925-172">System.DateTime</span></span>|<span data-ttu-id="8e925-173">DateTime2</span><span class="sxs-lookup"><span data-stu-id="8e925-173">DateTime2</span></span>|<span data-ttu-id="8e925-174">DateTime2</span><span class="sxs-lookup"><span data-stu-id="8e925-174">DateTime2</span></span>|  
|<span data-ttu-id="8e925-175">datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="8e925-175">datetimeoffset</span></span>|<span data-ttu-id="8e925-176">System. DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="8e925-176">System.DateTimeOffset</span></span>|<span data-ttu-id="8e925-177">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="8e925-177">DateTimeOffset</span></span>|<span data-ttu-id="8e925-178">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="8e925-178">DateTimeOffset</span></span>|  
|<span data-ttu-id="8e925-179">datetime</span><span class="sxs-lookup"><span data-stu-id="8e925-179">datetime</span></span>|<span data-ttu-id="8e925-180">System. DateTime</span><span class="sxs-lookup"><span data-stu-id="8e925-180">System.DateTime</span></span>|<span data-ttu-id="8e925-181">DateTime</span><span class="sxs-lookup"><span data-stu-id="8e925-181">DateTime</span></span>|<span data-ttu-id="8e925-182">DateTime</span><span class="sxs-lookup"><span data-stu-id="8e925-182">DateTime</span></span>|  
|<span data-ttu-id="8e925-183">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="8e925-183">smalldatetime</span></span>|<span data-ttu-id="8e925-184">System. DateTime</span><span class="sxs-lookup"><span data-stu-id="8e925-184">System.DateTime</span></span>|<span data-ttu-id="8e925-185">DateTime</span><span class="sxs-lookup"><span data-stu-id="8e925-185">DateTime</span></span>|<span data-ttu-id="8e925-186">DateTime</span><span class="sxs-lookup"><span data-stu-id="8e925-186">DateTime</span></span>|  
  
### <a name="sqlparameter-properties"></a><span data-ttu-id="8e925-187">Właściwości SqlParameter</span><span class="sxs-lookup"><span data-stu-id="8e925-187">SqlParameter Properties</span></span>  

 <span data-ttu-id="8e925-188">W poniższej tabeli opisano `SqlParameter` właściwości, które są istotne dla typów danych Data i godzina.</span><span class="sxs-lookup"><span data-stu-id="8e925-188">The following table describes `SqlParameter` properties that are relevant to date and time data types.</span></span>  
  
|<span data-ttu-id="8e925-189">Właściwość</span><span class="sxs-lookup"><span data-stu-id="8e925-189">Property</span></span>|<span data-ttu-id="8e925-190">Opis</span><span class="sxs-lookup"><span data-stu-id="8e925-190">Description</span></span>|  
|--------------|-----------------|  
|<xref:System.Data.SqlClient.SqlParameter.IsNullable%2A>|<span data-ttu-id="8e925-191">Pobiera lub ustawia czy wartość dopuszcza wartości null.</span><span class="sxs-lookup"><span data-stu-id="8e925-191">Gets or sets whether a value is nullable.</span></span> <span data-ttu-id="8e925-192">W przypadku wysyłania wartości parametru o wartości null do serwera należy określić <xref:System.DBNull> , a nie `null` ( `Nothing` w Visual Basic).</span><span class="sxs-lookup"><span data-stu-id="8e925-192">When you send a null parameter value to the server, you must specify <xref:System.DBNull>, rather than `null` (`Nothing` in Visual Basic).</span></span> <span data-ttu-id="8e925-193">Aby uzyskać więcej informacji na temat wartości null bazy danych, zobacz [Obsługa wartości null](handling-null-values.md).</span><span class="sxs-lookup"><span data-stu-id="8e925-193">For more information about database nulls, see [Handling Null Values](handling-null-values.md).</span></span>|  
|<xref:System.Data.SqlClient.SqlParameter.Precision%2A>|<span data-ttu-id="8e925-194">Pobiera lub ustawia maksymalną liczbę cyfr używanych do reprezentowania wartości.</span><span class="sxs-lookup"><span data-stu-id="8e925-194">Gets or sets the maximum number of digits used to represent the value.</span></span> <span data-ttu-id="8e925-195">To ustawienie jest ignorowane dla typów danych Data i godzina.</span><span class="sxs-lookup"><span data-stu-id="8e925-195">This setting is ignored for date and time data types.</span></span>|  
|<xref:System.Data.SqlClient.SqlParameter.Scale%2A>|<span data-ttu-id="8e925-196">Pobiera lub ustawia liczbę miejsc dziesiętnych, do których zostanie rozwiązany fragment czasu wartości `Time` , `DateTime2` i `DateTimeOffset` .</span><span class="sxs-lookup"><span data-stu-id="8e925-196">Gets or sets the number of decimal places to which the time portion of the value is resolved for `Time`, `DateTime2`,and `DateTimeOffset`.</span></span> <span data-ttu-id="8e925-197">Wartość domyślna to 0, co oznacza, że rzeczywista Skala jest wywnioskowana z wartości i wysyłana do serwera.</span><span class="sxs-lookup"><span data-stu-id="8e925-197">The default value is 0, which means that the actual scale is inferred from the value and sent to the server.</span></span>|  
|<xref:System.Data.SqlClient.SqlParameter.Size%2A>|<span data-ttu-id="8e925-198">Ignorowany dla typów danych daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="8e925-198">Ignored for date and time data types.</span></span>|  
|<xref:System.Data.SqlClient.SqlParameter.Value%2A>|<span data-ttu-id="8e925-199">Pobiera lub ustawia wartość parametru.</span><span class="sxs-lookup"><span data-stu-id="8e925-199">Gets or sets the parameter value.</span></span>|  
|<xref:System.Data.SqlClient.SqlParameter.SqlValue%2A>|<span data-ttu-id="8e925-200">Pobiera lub ustawia wartość parametru.</span><span class="sxs-lookup"><span data-stu-id="8e925-200">Gets or sets the parameter value.</span></span>|  
  
> [!NOTE]
> <span data-ttu-id="8e925-201">Wartość czasu, która jest mniejsza od zera lub większa lub równa 24 godzin, spowoduje wygenerowanie <xref:System.ArgumentException> .</span><span class="sxs-lookup"><span data-stu-id="8e925-201">Time values that are less than zero or greater than or equal to 24 hours will throw an <xref:System.ArgumentException>.</span></span>  
  
### <a name="creating-parameters"></a><span data-ttu-id="8e925-202">Tworzenie parametrów</span><span class="sxs-lookup"><span data-stu-id="8e925-202">Creating Parameters</span></span>  

 <span data-ttu-id="8e925-203">Można utworzyć <xref:System.Data.SqlClient.SqlParameter> obiekt za pomocą jego konstruktora lub przez dodanie go do <xref:System.Data.SqlClient.SqlCommand> <xref:System.Data.SqlClient.SqlCommand.Parameters%2A> kolekcji, wywołując `Add` metodę <xref:System.Data.SqlClient.SqlParameterCollection> .</span><span class="sxs-lookup"><span data-stu-id="8e925-203">You can create a <xref:System.Data.SqlClient.SqlParameter> object by using its constructor, or by adding it to a <xref:System.Data.SqlClient.SqlCommand><xref:System.Data.SqlClient.SqlCommand.Parameters%2A> collection by calling the `Add` method of the <xref:System.Data.SqlClient.SqlParameterCollection>.</span></span> <span data-ttu-id="8e925-204">`Add`Metoda przyjmuje jako dane wejściowe argumenty konstruktora lub istniejący obiekt Parameter.</span><span class="sxs-lookup"><span data-stu-id="8e925-204">The `Add` method will take as input either constructor arguments or an existing parameter object.</span></span>  
  
 <span data-ttu-id="8e925-205">W następnych sekcjach tego tematu przedstawiono przykłady sposobu określania parametrów daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="8e925-205">The next sections in this topic provide examples of how to specify date and time parameters.</span></span> <span data-ttu-id="8e925-206">Aby uzyskać dodatkowe przykłady pracy z parametrami, zobacz [Konfigurowanie parametrów i typów danych parametrów](../configuring-parameters-and-parameter-data-types.md) i [DataAdapter Parameters](../dataadapter-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="8e925-206">For additional examples of working with parameters, see [Configuring Parameters and Parameter Data Types](../configuring-parameters-and-parameter-data-types.md) and [DataAdapter Parameters](../dataadapter-parameters.md).</span></span>  
  
### <a name="date-example"></a><span data-ttu-id="8e925-207">Przykład daty</span><span class="sxs-lookup"><span data-stu-id="8e925-207">Date Example</span></span>  

 <span data-ttu-id="8e925-208">Poniższy fragment kodu pokazuje, jak określić `date` parametr.</span><span class="sxs-lookup"><span data-stu-id="8e925-208">The following code fragment demonstrates how to specify a `date` parameter.</span></span>  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@Date";  
parameter.SqlDbType = SqlDbType.Date;  
parameter.Value = "2007/12/1";  
```  
  
```vb  
Dim parameter As New SqlParameter()  
parameter.ParameterName = "@Date"  
parameter.SqlDbType = SqlDbType.Date  
parameter.Value = "2007/12/1"  
```  
  
### <a name="time-example"></a><span data-ttu-id="8e925-209">Przykład czasu</span><span class="sxs-lookup"><span data-stu-id="8e925-209">Time Example</span></span>  

 <span data-ttu-id="8e925-210">Poniższy fragment kodu pokazuje, jak określić `time` parametr.</span><span class="sxs-lookup"><span data-stu-id="8e925-210">The following code fragment demonstrates how to specify a `time` parameter.</span></span>  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@time";  
parameter.SqlDbType = SqlDbType.Time;  
parameter.Value = DateTime.Parse("23:59:59").TimeOfDay;  
```  
  
```vb  
Dim parameter As New SqlParameter()  
parameter.ParameterName = "@Time"  
parameter.SqlDbType = SqlDbType.Time  
parameter.Value = DateTime.Parse("23:59:59").TimeOfDay;  
```  
  
### <a name="datetime2-example"></a><span data-ttu-id="8e925-211">Przykład Datetime2</span><span class="sxs-lookup"><span data-stu-id="8e925-211">Datetime2 Example</span></span>  

 <span data-ttu-id="8e925-212">Poniższy fragment kodu pokazuje, jak określić `datetime2` parametr z częściami daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="8e925-212">The following code fragment demonstrates how to specify a `datetime2` parameter with both the date and time parts.</span></span>  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@Datetime2";  
parameter.SqlDbType = SqlDbType.DateTime2;  
parameter.Value = DateTime.Parse("1666-09-02 1:00:00");  
```  
  
```vb  
Dim parameter As New SqlParameter()  
parameter.ParameterName = "@Datetime2"  
parameter.SqlDbType = SqlDbType.DateTime2  
parameter.Value = DateTime.Parse("1666-09-02 1:00:00");  
```  
  
### <a name="datetimeoffset-example"></a><span data-ttu-id="8e925-213">Przykład DateTimeOffSet</span><span class="sxs-lookup"><span data-stu-id="8e925-213">DateTimeOffSet Example</span></span>  

 <span data-ttu-id="8e925-214">Poniższy fragment kodu ilustruje sposób określania `DateTimeOffSet` parametru z datą, godziną i przesunięciem strefy czasowej równej 0.</span><span class="sxs-lookup"><span data-stu-id="8e925-214">The following code fragment demonstrates how to specify a `DateTimeOffSet` parameter with a date, a time, and a time zone offset of 0.</span></span>  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@DateTimeOffSet";  
parameter.SqlDbType = SqlDbType.DateTimeOffSet;  
parameter.Value = DateTimeOffset.Parse("1666-09-02 1:00:00+0");  
```  
  
```vb  
Dim parameter As New SqlParameter()  
parameter.ParameterName = "@DateTimeOffSet"  
parameter.SqlDbType = SqlDbType.DateTimeOffSet  
parameter.Value = DateTimeOffset.Parse("1666-09-02 1:00:00+0");  
```  
  
### <a name="addwithvalue"></a><span data-ttu-id="8e925-215">AddWithValue</span><span class="sxs-lookup"><span data-stu-id="8e925-215">AddWithValue</span></span>  

 <span data-ttu-id="8e925-216">Parametry można także podać przy użyciu `AddWithValue` metody <xref:System.Data.SqlClient.SqlCommand> , jak pokazano w poniższym fragmencie kodu.</span><span class="sxs-lookup"><span data-stu-id="8e925-216">You can also supply parameters by using the `AddWithValue` method of a <xref:System.Data.SqlClient.SqlCommand>, as shown in the following code fragment.</span></span> <span data-ttu-id="8e925-217">Jednak metoda nie `AddWithValue` pozwala na określenie <xref:System.Data.SqlClient.SqlParameter.DbType%2A> <xref:System.Data.SqlClient.SqlParameter.SqlDbType%2A> parametru lub.</span><span class="sxs-lookup"><span data-stu-id="8e925-217">However, the `AddWithValue` method does not allow you to specify the <xref:System.Data.SqlClient.SqlParameter.DbType%2A> or <xref:System.Data.SqlClient.SqlParameter.SqlDbType%2A> for the parameter.</span></span>  
  
```csharp  
command.Parameters.AddWithValue(
    "@date", DateTimeOffset.Parse("16660902"));  
```  
  
```vb  
command.Parameters.AddWithValue( _  
    "@date", DateTimeOffset.Parse("16660902"))  
```  
  
 <span data-ttu-id="8e925-218">`@date`Parametr może być mapowany na `date` `datetime` Typ danych, lub `datetime2` na serwerze.</span><span class="sxs-lookup"><span data-stu-id="8e925-218">The `@date` parameter could map to a `date`, `datetime`, or `datetime2` data type on the server.</span></span> <span data-ttu-id="8e925-219">Podczas pracy z nowymi `datetime` typami danych należy jawnie ustawić <xref:System.Data.SqlDbType> Właściwość parametru na typ danych wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="8e925-219">When working with the new `datetime` data types, you must explicitly set the parameter's <xref:System.Data.SqlDbType> property to the data type of the instance.</span></span> <span data-ttu-id="8e925-220">Użycie <xref:System.Data.SqlDbType.Variant> lub niejawne dostarczenie wartości parametrów może spowodować problemy ze zgodnością z poprzednimi wersjami `datetime` i `smalldatetime` typami danych.</span><span class="sxs-lookup"><span data-stu-id="8e925-220">Using <xref:System.Data.SqlDbType.Variant> or implicitly supplying parameter values can cause problems with backward compatibility with the `datetime` and `smalldatetime` data types.</span></span>  
  
 <span data-ttu-id="8e925-221">W poniższej tabeli przedstawiono, które `SqlDbTypes` są wywnioskowane z typów CLR:</span><span class="sxs-lookup"><span data-stu-id="8e925-221">The following table shows which `SqlDbTypes` are inferred from which CLR types:</span></span>  
  
|<span data-ttu-id="8e925-222">Typ CLR</span><span class="sxs-lookup"><span data-stu-id="8e925-222">CLR type</span></span>|<span data-ttu-id="8e925-223">Wywnioskowane SqlDbType</span><span class="sxs-lookup"><span data-stu-id="8e925-223">Inferred SqlDbType</span></span>|  
|--------------|------------------------|  
|<span data-ttu-id="8e925-224">DateTime</span><span class="sxs-lookup"><span data-stu-id="8e925-224">DateTime</span></span>|<span data-ttu-id="8e925-225">SqlDbType. DateTime</span><span class="sxs-lookup"><span data-stu-id="8e925-225">SqlDbType.DateTime</span></span>|  
|<span data-ttu-id="8e925-226">przedział_czasu</span><span class="sxs-lookup"><span data-stu-id="8e925-226">TimeSpan</span></span>|<span data-ttu-id="8e925-227">SqlDbType. Time</span><span class="sxs-lookup"><span data-stu-id="8e925-227">SqlDbType.Time</span></span>|  
|<span data-ttu-id="8e925-228">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="8e925-228">DateTimeOffset</span></span>|<span data-ttu-id="8e925-229">SqlDbType. DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="8e925-229">SqlDbType.DateTimeOffset</span></span>|  
  
## <a name="retrieving-date-and-time-data"></a><span data-ttu-id="8e925-230">Pobieranie danych daty i godziny</span><span class="sxs-lookup"><span data-stu-id="8e925-230">Retrieving Date and Time Data</span></span>  

 <span data-ttu-id="8e925-231">W poniższej tabeli opisano metody, które są używane do pobierania wartości daty i godziny SQL Server 2008.</span><span class="sxs-lookup"><span data-stu-id="8e925-231">The following table describes methods that are used to retrieve SQL Server 2008 date and time values.</span></span>  
  
|<span data-ttu-id="8e925-232">Metoda SqlClient</span><span class="sxs-lookup"><span data-stu-id="8e925-232">SqlClient method</span></span>|<span data-ttu-id="8e925-233">Opis</span><span class="sxs-lookup"><span data-stu-id="8e925-233">Description</span></span>|  
|----------------------|-----------------|  
|<xref:System.Data.SqlClient.SqlDataReader.GetDateTime%2A>|<span data-ttu-id="8e925-234">Pobiera określoną wartość kolumny jako <xref:System.DateTime> strukturę.</span><span class="sxs-lookup"><span data-stu-id="8e925-234">Retrieves the specified column value as a <xref:System.DateTime> structure.</span></span>|  
|<xref:System.Data.SqlClient.SqlDataReader.GetDateTimeOffset%2A>|<span data-ttu-id="8e925-235">Pobiera określoną wartość kolumny jako <xref:System.DateTimeOffset> strukturę.</span><span class="sxs-lookup"><span data-stu-id="8e925-235">Retrieves the specified column value as a <xref:System.DateTimeOffset> structure.</span></span>|  
|<xref:System.Data.SqlClient.SqlDataReader.GetProviderSpecificFieldType%2A>|<span data-ttu-id="8e925-236">Zwraca typ, który jest podstawowym typem specyficznym dla danego dostawcy dla pola.</span><span class="sxs-lookup"><span data-stu-id="8e925-236">Returns the type that is the underlying provider-specific type for the field.</span></span> <span data-ttu-id="8e925-237">Zwraca takie same typy jak `GetFieldType` dla nowych typów dat i godzin.</span><span class="sxs-lookup"><span data-stu-id="8e925-237">Returns the same types as `GetFieldType` for new date and time types.</span></span>|  
|<xref:System.Data.SqlClient.SqlDataReader.GetProviderSpecificValue%2A>|<span data-ttu-id="8e925-238">Pobiera wartość określonej kolumny.</span><span class="sxs-lookup"><span data-stu-id="8e925-238">Retrieves the value of the specified column.</span></span> <span data-ttu-id="8e925-239">Zwraca takie same typy jak `GetValue` dla nowych typów daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="8e925-239">Returns the same types as `GetValue` for the new date and time types.</span></span>|  
|<xref:System.Data.SqlClient.SqlDataReader.GetProviderSpecificValues%2A>|<span data-ttu-id="8e925-240">Pobiera wartości z określonej tablicy.</span><span class="sxs-lookup"><span data-stu-id="8e925-240">Retrieves the values in the specified array.</span></span>|  
|<xref:System.Data.SqlClient.SqlDataReader.GetSqlString%2A>|<span data-ttu-id="8e925-241">Pobiera wartość kolumny jako <xref:System.Data.SqlTypes.SqlString> .</span><span class="sxs-lookup"><span data-stu-id="8e925-241">Retrieves the column value as a <xref:System.Data.SqlTypes.SqlString>.</span></span> <span data-ttu-id="8e925-242"><xref:System.InvalidCastException>Występuje, jeśli dane nie mogą być wyrażone jako `SqlString` .</span><span class="sxs-lookup"><span data-stu-id="8e925-242">An <xref:System.InvalidCastException> occurs if the data cannot be expressed as a `SqlString`.</span></span>|  
|<xref:System.Data.SqlClient.SqlDataReader.GetSqlValue%2A>|<span data-ttu-id="8e925-243">Domyślnie pobiera dane z kolumny `SqlDbType` .</span><span class="sxs-lookup"><span data-stu-id="8e925-243">Retrieves column data as its default `SqlDbType`.</span></span> <span data-ttu-id="8e925-244">Zwraca takie same typy jak `GetValue` dla nowych typów daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="8e925-244">Returns the same types as `GetValue` for the new date and time types.</span></span>|  
|<xref:System.Data.SqlClient.SqlDataReader.GetSqlValues%2A>|<span data-ttu-id="8e925-245">Pobiera wartości z określonej tablicy.</span><span class="sxs-lookup"><span data-stu-id="8e925-245">Retrieves the values in the specified array.</span></span>|  
|<xref:System.Data.SqlClient.SqlDataReader.GetString%2A>|<span data-ttu-id="8e925-246">Pobiera wartość kolumny jako ciąg, jeśli wersja systemu typu jest ustawiona na SQL Server 2005.</span><span class="sxs-lookup"><span data-stu-id="8e925-246">Retrieves the column value as a string if the Type System Version is set to SQL Server 2005.</span></span> <span data-ttu-id="8e925-247"><xref:System.InvalidCastException>Występuje, jeśli dane nie mogą być wyrażone jako ciąg.</span><span class="sxs-lookup"><span data-stu-id="8e925-247">An <xref:System.InvalidCastException> occurs if the data cannot be expressed as a string.</span></span>|  
|<xref:System.Data.SqlClient.SqlDataReader.GetTimeSpan%2A>|<span data-ttu-id="8e925-248">Pobiera określoną wartość kolumny jako <xref:System.TimeSpan> strukturę.</span><span class="sxs-lookup"><span data-stu-id="8e925-248">Retrieves the specified column value as a <xref:System.TimeSpan> structure.</span></span>|  
|<xref:System.Data.SqlClient.SqlDataReader.GetValue%2A>|<span data-ttu-id="8e925-249">Pobiera określoną wartość kolumny jako jej źródłowy typ CLR.</span><span class="sxs-lookup"><span data-stu-id="8e925-249">Retrieves the specified column value as its underlying CLR type.</span></span>|  
|<xref:System.Data.SqlClient.SqlDataReader.GetValues%2A>|<span data-ttu-id="8e925-250">Pobiera wartości kolumn w tablicy.</span><span class="sxs-lookup"><span data-stu-id="8e925-250">Retrieves column values in an array.</span></span>|  
|<xref:System.Data.SqlClient.SqlDataReader.GetSchemaTable%2A>|<span data-ttu-id="8e925-251">Zwraca <xref:System.Data.DataTable> , który opisuje metadane zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="8e925-251">Returns a <xref:System.Data.DataTable> that describes the metadata of the result set.</span></span>|  
  
> [!NOTE]
> <span data-ttu-id="8e925-252">Nowa Data i godzina `SqlDbTypes` nie są obsługiwane dla kodu, który jest wykonywany w procesie w SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8e925-252">The new date and time `SqlDbTypes` are not supported for code that is executing in-process in SQL Server.</span></span> <span data-ttu-id="8e925-253">Jeśli jeden z tych typów zostanie przekazywać do serwera, zostanie zgłoszony wyjątek.</span><span class="sxs-lookup"><span data-stu-id="8e925-253">An exception will be raised if one of these types is passed to the server.</span></span>  
  
## <a name="specifying-date-and-time-values-as-literals"></a><span data-ttu-id="8e925-254">Określanie wartości daty i godziny jako literałów</span><span class="sxs-lookup"><span data-stu-id="8e925-254">Specifying Date and Time Values as Literals</span></span>  

 <span data-ttu-id="8e925-255">Można określić typy danych daty i godziny przy użyciu różnych formatów ciągów literałów, które SQL Server następnie szacuje się w czasie wykonywania, konwertując je do wewnętrznych struktur daty/czasu.</span><span class="sxs-lookup"><span data-stu-id="8e925-255">You can specify date and time data types by using a variety of different literal string formats, which SQL Server then evaluates at run time, converting them to internal date/time structures.</span></span> <span data-ttu-id="8e925-256">SQL Server rozpoznaje dane daty i godziny ujęte w znaki pojedynczego cudzysłowu (').</span><span class="sxs-lookup"><span data-stu-id="8e925-256">SQL Server recognizes date and time data that is enclosed in single quotation marks (').</span></span> <span data-ttu-id="8e925-257">W poniższych przykładach przedstawiono niektóre formaty:</span><span class="sxs-lookup"><span data-stu-id="8e925-257">The following examples demonstrate some formats:</span></span>  
  
- <span data-ttu-id="8e925-258">Alfabetyczne formaty dat, takie jak `'October 15, 2006'` .</span><span class="sxs-lookup"><span data-stu-id="8e925-258">Alphabetic date formats, such as `'October 15, 2006'`.</span></span>  
  
- <span data-ttu-id="8e925-259">Numeryczne formaty daty, takie jak `'10/15/2006'` .</span><span class="sxs-lookup"><span data-stu-id="8e925-259">Numeric date formats, such as `'10/15/2006'`.</span></span>  
  
- <span data-ttu-id="8e925-260">Nierozdzielne formaty ciągów, takie jak `'20061015'` , które byłyby interpretowane jako 15 października 2006 w przypadku używania standardowego formatu daty ISO.</span><span class="sxs-lookup"><span data-stu-id="8e925-260">Unseparated string formats, such as `'20061015'`, which would be interpreted as October 15, 2006 if you are using the ISO standard date format.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="8e925-261">Pełną dokumentację dotyczącą wszystkich formatów ciągów literałów i innych funkcji typów danych daty i godziny można znaleźć w temacie SQL Server Books Online.</span><span class="sxs-lookup"><span data-stu-id="8e925-261">You can find complete documentation for all of the literal string formats and other features of the date and time data types in SQL Server Books Online.</span></span>  
  
 <span data-ttu-id="8e925-262">Wartość czasu, która jest mniejsza od zera lub większa lub równa 24 godzin, spowoduje wygenerowanie <xref:System.ArgumentException> .</span><span class="sxs-lookup"><span data-stu-id="8e925-262">Time values that are less than zero or greater than or equal to 24 hours will throw an <xref:System.ArgumentException>.</span></span>  
  
## <a name="resources-in-sql-server-books-online"></a><span data-ttu-id="8e925-263">Zasoby w SQL Server książki online</span><span class="sxs-lookup"><span data-stu-id="8e925-263">Resources in SQL Server Books Online</span></span>  

 <span data-ttu-id="8e925-264">Aby uzyskać więcej informacji na temat pracy z wartościami daty i godziny w SQL Server, zobacz następujące zasoby w SQL Server Books Online.</span><span class="sxs-lookup"><span data-stu-id="8e925-264">For more information about working with date and time values in SQL Server, see the following resources in SQL Server Books Online.</span></span>  
  
|<span data-ttu-id="8e925-265">Temat</span><span class="sxs-lookup"><span data-stu-id="8e925-265">Topic</span></span>|<span data-ttu-id="8e925-266">Opis</span><span class="sxs-lookup"><span data-stu-id="8e925-266">Description</span></span>|  
|-----------|-----------------|  
|[<span data-ttu-id="8e925-267">Typy i funkcje danych daty i godziny (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="8e925-267">Date and Time Data Types and Functions (Transact-SQL)</span></span>](/sql/t-sql/functions/date-and-time-data-types-and-functions-transact-sql)|<span data-ttu-id="8e925-268">Zawiera przegląd wszystkich typów danych i funkcji języka Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="8e925-268">Provides an overview of all Transact-SQL date and time data types and functions.</span></span>|  
|<span data-ttu-id="8e925-269">[Korzystanie z danych daty i godziny](/previous-versions/sql/sql-server-2008/ms180878(v=sql.100))</span><span class="sxs-lookup"><span data-stu-id="8e925-269">[Using Date and Time Data](/previous-versions/sql/sql-server-2008/ms180878(v=sql.100))</span></span>|<span data-ttu-id="8e925-270">Zawiera informacje na temat typów i funkcji danych daty i godziny oraz przykłady ich użycia.</span><span class="sxs-lookup"><span data-stu-id="8e925-270">Provides information about the date and time data types and functions, and examples of using them.</span></span>|  
|[<span data-ttu-id="8e925-271">Typy danych (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="8e925-271">Data Types (Transact-SQL)</span></span>](/sql/t-sql/data-types/data-types-transact-sql)|<span data-ttu-id="8e925-272">Opisuje systemowe typy danych w SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8e925-272">Describes system data types in SQL Server.</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="8e925-273">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="8e925-273">See also</span></span>

- [<span data-ttu-id="8e925-274">Mapowanie typu danych serwera SQL</span><span class="sxs-lookup"><span data-stu-id="8e925-274">SQL Server Data Type Mappings</span></span>](../sql-server-data-type-mappings.md)
- [<span data-ttu-id="8e925-275">Konfigurowanie parametrów i typów danych parametrów</span><span class="sxs-lookup"><span data-stu-id="8e925-275">Configuring Parameters and Parameter Data Types</span></span>](../configuring-parameters-and-parameter-data-types.md)
- [<span data-ttu-id="8e925-276">Typy danych programu SQL Server i ADO.NET</span><span class="sxs-lookup"><span data-stu-id="8e925-276">SQL Server Data Types and ADO.NET</span></span>](sql-server-data-types.md)
- [<span data-ttu-id="8e925-277">Omówienie ADO.NET</span><span class="sxs-lookup"><span data-stu-id="8e925-277">ADO.NET Overview</span></span>](../ado-net-overview.md)
