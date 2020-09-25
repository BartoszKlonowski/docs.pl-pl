---
title: Obsługa wartości Null
description: Dowiedz się, w jaki sposób Dostawca danych .NET Framework dla SQL Server obsługuje wartość null, i przeczytaj informacje o wartościach null i SqlBoolean, z których ma być przypisana wartość null.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: f18b288f-b265-4bbe-957f-c6833c0645ef
ms.openlocfilehash: 2ed2a88b91f06bb02c72d3e310ae09d58637205f
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91197472"
---
# <a name="handling-null-values"></a><span data-ttu-id="95146-103">Obsługa wartości Null</span><span class="sxs-lookup"><span data-stu-id="95146-103">Handling Null Values</span></span>

<span data-ttu-id="95146-104">Wartość null w relacyjnej bazie danych jest używana, gdy wartość w kolumnie jest nieznana lub brakująca.</span><span class="sxs-lookup"><span data-stu-id="95146-104">A null value in a relational database is used when the value in a column is unknown or missing.</span></span> <span data-ttu-id="95146-105">Wartość null nie jest ciągiem pustym (dla typów danych znakowych lub DateTime) ani wartością zerową (dla liczbowych typów danych).</span><span class="sxs-lookup"><span data-stu-id="95146-105">A null is neither an empty string (for character or datetime data types) nor a zero value (for numeric data types).</span></span> <span data-ttu-id="95146-106">Specyfikacja ANSI SQL-92 stwierdza, że wartość null musi być taka sama dla wszystkich typów danych, tak aby wszystkie wartości null były obsługiwane spójnie.</span><span class="sxs-lookup"><span data-stu-id="95146-106">The ANSI SQL-92 specification states that a null must be the same for all data types, so that all nulls are handled consistently.</span></span> <span data-ttu-id="95146-107"><xref:System.Data.SqlTypes>Przestrzeń nazw zapewnia semantykę o wartości null przez implementację <xref:System.Data.SqlTypes.INullable> interfejsu.</span><span class="sxs-lookup"><span data-stu-id="95146-107">The <xref:System.Data.SqlTypes> namespace provides null semantics by implementing the <xref:System.Data.SqlTypes.INullable> interface.</span></span> <span data-ttu-id="95146-108">Każdy z typów danych w programie <xref:System.Data.SqlTypes> ma własną `IsNull` Właściwość i `Null` wartość, która może być przypisana do wystąpienia tego typu danych.</span><span class="sxs-lookup"><span data-stu-id="95146-108">Each of the data types in <xref:System.Data.SqlTypes> has its own `IsNull` property and a `Null` value that can be assigned to an instance of that data type.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="95146-109">W .NET Framework w wersji 2,0 wprowadzono obsługę typów wartości dopuszczających wartość null, dzięki czemu programiści mogą rozwijać typ wartości reprezentujący wszystkie wartości typu podstawowego.</span><span class="sxs-lookup"><span data-stu-id="95146-109">The .NET Framework version 2.0 introduced support for nullable value types, which allow programmers to extend a value type to represent all values of the underlying type.</span></span> <span data-ttu-id="95146-110">Te typy wartości null CLR reprezentują wystąpienie <xref:System.Nullable> struktury.</span><span class="sxs-lookup"><span data-stu-id="95146-110">These CLR nullable value types represent an instance of the <xref:System.Nullable> structure.</span></span> <span data-ttu-id="95146-111">Ta funkcja jest szczególnie przydatna, gdy typy wartości są opakowane i rozpakowane, zapewniając zwiększoną zgodność z typami obiektów.</span><span class="sxs-lookup"><span data-stu-id="95146-111">This capability is especially useful when value types are boxed and unboxed, providing enhanced compatibility with object types.</span></span> <span data-ttu-id="95146-112">Typy wartości null CLR nie są przeznaczone do przechowywania wartości null bazy danych, ponieważ wartość null w formacie ANSI nie zachowuje się tak samo jak `null` w przypadku odwołania (lub `Nothing` w Visual Basic).</span><span class="sxs-lookup"><span data-stu-id="95146-112">CLR nullable value types are not intended for storage of database nulls because an ANSI SQL null does not behave the same way as a `null` reference (or `Nothing` in Visual Basic).</span></span> <span data-ttu-id="95146-113">W przypadku pracy z bazami danych ANSI SQL o wartości null Użyj <xref:System.Data.SqlTypes> wartości null zamiast <xref:System.Nullable> .</span><span class="sxs-lookup"><span data-stu-id="95146-113">For working with database ANSI SQL null values, use <xref:System.Data.SqlTypes> nulls rather than <xref:System.Nullable>.</span></span> <span data-ttu-id="95146-114">Aby uzyskać więcej informacji na temat pracy z typami CLR wartości null w Visual Basic zobacz [dopuszczanie typów wartości null](../../../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md), a dla języka C# zobacz [dopuszczanie typów wartości](../../../../csharp/language-reference/builtin-types/nullable-value-types.md).</span><span class="sxs-lookup"><span data-stu-id="95146-114">For more information on working with CLR value nullable types in Visual Basic see [Nullable Value Types](../../../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md), and for C# see [Nullable value types](../../../../csharp/language-reference/builtin-types/nullable-value-types.md).</span></span>  
  
## <a name="nulls-and-three-valued-logic"></a><span data-ttu-id="95146-115">Wartości null i logika trzech wartości</span><span class="sxs-lookup"><span data-stu-id="95146-115">Nulls and Three-Valued Logic</span></span>  

 <span data-ttu-id="95146-116">Zezwalanie na wartości null w definicjach kolumn wprowadza do aplikacji logiczną trzy wartości.</span><span class="sxs-lookup"><span data-stu-id="95146-116">Allowing null values in column definitions introduces three-valued logic into your application.</span></span> <span data-ttu-id="95146-117">Porównanie może wynikać z jednego z trzech warunków:</span><span class="sxs-lookup"><span data-stu-id="95146-117">A comparison can evaluate to one of three conditions:</span></span>  
  
- <span data-ttu-id="95146-118">Prawda</span><span class="sxs-lookup"><span data-stu-id="95146-118">True</span></span>  
  
- <span data-ttu-id="95146-119">Fałsz</span><span class="sxs-lookup"><span data-stu-id="95146-119">False</span></span>  
  
- <span data-ttu-id="95146-120">Nieznane</span><span class="sxs-lookup"><span data-stu-id="95146-120">Unknown</span></span>  
  
 <span data-ttu-id="95146-121">Ponieważ wartość null jest uznawana za nieznaną, dwie wartości null w porównaniu do siebie nie są traktowane jako równe.</span><span class="sxs-lookup"><span data-stu-id="95146-121">Because null is considered to be unknown, two null values compared to each other are not considered to be equal.</span></span> <span data-ttu-id="95146-122">W wyrażeniach wykorzystujących operatory arytmetyczne, jeśli którykolwiek z operandów ma wartość null, wynik jest również równy null.</span><span class="sxs-lookup"><span data-stu-id="95146-122">In expressions using arithmetic operators, if any of the operands is null, the result is null as well.</span></span>  
  
## <a name="nulls-and-sqlboolean"></a><span data-ttu-id="95146-123">Wartości null i SqlBoolean</span><span class="sxs-lookup"><span data-stu-id="95146-123">Nulls and SqlBoolean</span></span>  

 <span data-ttu-id="95146-124">Porównanie między dowolnymi zwróci <xref:System.Data.SqlTypes> wynik <xref:System.Data.SqlTypes.SqlBoolean> .</span><span class="sxs-lookup"><span data-stu-id="95146-124">Comparison between any <xref:System.Data.SqlTypes> will return a <xref:System.Data.SqlTypes.SqlBoolean>.</span></span> <span data-ttu-id="95146-125">`IsNull`Funkcja dla każdej `SqlType` zwraca <xref:System.Data.SqlTypes.SqlBoolean> i może służyć do sprawdzania wartości null.</span><span class="sxs-lookup"><span data-stu-id="95146-125">The `IsNull` function for each `SqlType` returns a <xref:System.Data.SqlTypes.SqlBoolean> and can be used to check for null values.</span></span> <span data-ttu-id="95146-126">Następujące tabele prawdy pokazują, jak i, lub, i nie operatory, w obecności wartości null.</span><span class="sxs-lookup"><span data-stu-id="95146-126">The following truth tables show how the AND, OR, and NOT operators function in the presence of a null value.</span></span> <span data-ttu-id="95146-127">(T = true, F = false i U = Unknown lub null).</span><span class="sxs-lookup"><span data-stu-id="95146-127">(T=true, F=false, and U=unknown, or null.)</span></span>  
  
 <span data-ttu-id="95146-128">![Tabela prawdy](./media/truthtable-bpuedev11.gif "TruthTable_bpuedev11")</span><span class="sxs-lookup"><span data-stu-id="95146-128">![Truth Table](./media/truthtable-bpuedev11.gif "TruthTable_bpuedev11")</span></span>  
  
### <a name="understanding-the-ansi_nulls-option"></a><span data-ttu-id="95146-129">Zrozumienie opcji ANSI_NULLS</span><span class="sxs-lookup"><span data-stu-id="95146-129">Understanding the ANSI_NULLS Option</span></span>  

 <span data-ttu-id="95146-130"><xref:System.Data.SqlTypes> zapewnia taką samą semantykę, jak w przypadku ustawienia opcji ANSI_NULLS w SQL Server.</span><span class="sxs-lookup"><span data-stu-id="95146-130"><xref:System.Data.SqlTypes> provides the same semantics as when the ANSI_NULLS option is set on in SQL Server.</span></span> <span data-ttu-id="95146-131">Wszystkie operatory arytmetyczne (+,-, \* ,/,%), operatory bitowe (~, &, \| ) i większość funkcji zwracają wartość null, jeśli którykolwiek z operandów lub argumentów ma wartość null, z wyjątkiem właściwości `IsNull` .</span><span class="sxs-lookup"><span data-stu-id="95146-131">All arithmetic operators (+, -, \*, /, %), bitwise operators (~, &, \|), and most functions return null if any of the operands or arguments is null, except for the property `IsNull`.</span></span>  
  
 <span data-ttu-id="95146-132">Standard ANSI SQL-92 nie obsługuje elementu *ColumnName* = null w klauzuli WHERE.</span><span class="sxs-lookup"><span data-stu-id="95146-132">The ANSI SQL-92 standard does not support *columnName* = NULL in a WHERE clause.</span></span> <span data-ttu-id="95146-133">W SQL Server opcja ANSI_NULLS steruje domyślną wartością null w bazie danych i ocenie porównań z wartościami null.</span><span class="sxs-lookup"><span data-stu-id="95146-133">In SQL Server, the ANSI_NULLS option controls both default nullability in the database and evaluation of comparisons against null values.</span></span> <span data-ttu-id="95146-134">Jeśli ANSI_NULLS jest włączona (wartość domyślna), operator IS NULL musi być używany w wyrażeniach podczas testowania wartości null.</span><span class="sxs-lookup"><span data-stu-id="95146-134">If ANSI_NULLS is turned on (the default), the IS NULL operator must be used in expressions when testing for null values.</span></span> <span data-ttu-id="95146-135">Na przykład następujące porównanie zawsze jest nieznane, gdy ANSI_NULLS jest włączone:</span><span class="sxs-lookup"><span data-stu-id="95146-135">For example, the following comparison always yields unknown when ANSI_NULLS is on:</span></span>  
  
```sql
colname > NULL  
```  
  
 <span data-ttu-id="95146-136">Porównanie do zmiennej zawierającej wartość null daje również nieznane:</span><span class="sxs-lookup"><span data-stu-id="95146-136">Comparison to a variable containing a null value also yields unknown:</span></span>  
  
```sql
colname > @MyVariable  
```  
  
 <span data-ttu-id="95146-137">Użyj predykatu IS NULL lub IS NOT NULL, aby przetestować wartość null.</span><span class="sxs-lookup"><span data-stu-id="95146-137">Use the IS NULL or IS NOT NULL predicate to test for a null value.</span></span> <span data-ttu-id="95146-138">Może to zwiększyć złożoność do klauzuli WHERE.</span><span class="sxs-lookup"><span data-stu-id="95146-138">This can add complexity to the WHERE clause.</span></span> <span data-ttu-id="95146-139">Na przykład kolumna TerritoryID w tabeli klient AdventureWorks pozwala na wartości null.</span><span class="sxs-lookup"><span data-stu-id="95146-139">For example, the TerritoryID column in the AdventureWorks Customer table allows null values.</span></span> <span data-ttu-id="95146-140">Jeśli instrukcja SELECT ma przetestować pod kątem wartości null oprócz innych, musi zawierać predykat IS NULL:</span><span class="sxs-lookup"><span data-stu-id="95146-140">If a SELECT statement is to test for null values in addition to others, it must include an IS NULL predicate:</span></span>  
  
```sql
SELECT CustomerID, AccountNumber, TerritoryID  
FROM AdventureWorks.Sales.Customer  
WHERE TerritoryID IN (1, 2, 3)  
   OR TerritoryID IS NULL  
```  
  
 <span data-ttu-id="95146-141">Jeśli ustawiono ANSI_NULLS wyłączone w SQL Server, można utworzyć wyrażenia, które używają operatora równości do porównywania z wartością null.</span><span class="sxs-lookup"><span data-stu-id="95146-141">If you set ANSI_NULLS off in SQL Server, you can create expressions that use the equality operator to compare to null.</span></span> <span data-ttu-id="95146-142">Nie można jednak uniemożliwiać różnych połączeń z ustawieniem opcji null dla tego połączenia.</span><span class="sxs-lookup"><span data-stu-id="95146-142">However, you can't prevent different connections from setting null options for that connection.</span></span> <span data-ttu-id="95146-143">Używanie funkcji IS NULL do testowania wartości null zawsze działa, niezależnie od ustawień ANSI_NULLS dla połączenia.</span><span class="sxs-lookup"><span data-stu-id="95146-143">Using IS NULL to test for null values always works, regardless of the ANSI_NULLS settings for a connection.</span></span>  
  
 <span data-ttu-id="95146-144">Ustawienie ANSI_NULLS off nie jest obsługiwane w elemencie `DataSet` , który jest zawsze zgodny ze standardem ANSI SQL-92 w celu obsługi wartości null w <xref:System.Data.SqlTypes> .</span><span class="sxs-lookup"><span data-stu-id="95146-144">Setting ANSI_NULLS off is not supported in a `DataSet`, which always follows the ANSI SQL-92 standard for handling null values in <xref:System.Data.SqlTypes>.</span></span>  
  
## <a name="assigning-null-values"></a><span data-ttu-id="95146-145">Przypisywanie wartości null</span><span class="sxs-lookup"><span data-stu-id="95146-145">Assigning Null Values</span></span>  

 <span data-ttu-id="95146-146">Wartości null są specjalne, a ich semantyka przechowywania i przypisywania różni się w różnych systemach typów i systemach magazynowania.</span><span class="sxs-lookup"><span data-stu-id="95146-146">Null values are special, and their storage and assignment semantics differ across different type systems and storage systems.</span></span> <span data-ttu-id="95146-147">`Dataset`Program jest przeznaczony do użycia z różnymi systemami typu i magazynowania.</span><span class="sxs-lookup"><span data-stu-id="95146-147">A `Dataset` is designed to be used with different type and storage systems.</span></span>  
  
 <span data-ttu-id="95146-148">W tej sekcji opisano semantykę wartości null do przypisywania wartości null do a <xref:System.Data.DataColumn> w <xref:System.Data.DataRow> różnych systemach typów.</span><span class="sxs-lookup"><span data-stu-id="95146-148">This section describes the null semantics for assigning null values to a <xref:System.Data.DataColumn> in a <xref:System.Data.DataRow> across the different type systems.</span></span>  
  
 `DBNull.Value`  
 <span data-ttu-id="95146-149">To przypisanie jest prawidłowe dla `DataColumn` dowolnego typu.</span><span class="sxs-lookup"><span data-stu-id="95146-149">This assignment is valid for a `DataColumn` of any type.</span></span> <span data-ttu-id="95146-150">Jeśli typ implementuje `INullable` , `DBNull.Value` jest przekształcany na odpowiednią silnie wpisaną wartość null.</span><span class="sxs-lookup"><span data-stu-id="95146-150">If the type implements `INullable`, `DBNull.Value` is coerced into the appropriate strongly typed Null value.</span></span>  
  
 `SqlType.Null`  
 <span data-ttu-id="95146-151"><xref:System.Data.SqlTypes>Implementuje wszystkie typy danych `INullable` .</span><span class="sxs-lookup"><span data-stu-id="95146-151">All <xref:System.Data.SqlTypes> data types implement `INullable`.</span></span> <span data-ttu-id="95146-152">Jeśli silnie wpisana wartość null może zostać przekonwertowana na typ danych kolumny przy użyciu niejawnych operatorów rzutowania, przypisanie powinno nastąpić przez.</span><span class="sxs-lookup"><span data-stu-id="95146-152">If the strongly typed null value can be converted into the column's data type using implicit cast operators, the assignment should go through.</span></span> <span data-ttu-id="95146-153">W przeciwnym razie zostanie zgłoszony nieprawidłowy wyjątek rzutowania.</span><span class="sxs-lookup"><span data-stu-id="95146-153">Otherwise an invalid cast exception is thrown.</span></span>  
  
 `null`  
 <span data-ttu-id="95146-154">Jeśli wartość "null" jest wartością prawną dla danego `DataColumn` typu danych, jest ona przekształcana w odpowiednią `DbNull.Value` lub `Null` skojarzona z `INullable` typem ( `SqlType.Null` )</span><span class="sxs-lookup"><span data-stu-id="95146-154">If 'null' is a legal value for the given `DataColumn` data type, it is coerced into the appropriate `DbNull.Value` or `Null` associated with the `INullable` type (`SqlType.Null`)</span></span>  
  
 `derivedUdt.Null`  
 <span data-ttu-id="95146-155">W przypadku kolumn UDT wartości null są zawsze przechowywane na podstawie typu skojarzonego z `DataColumn` .</span><span class="sxs-lookup"><span data-stu-id="95146-155">For UDT columns, nulls are always stored based on the type associated with the `DataColumn`.</span></span> <span data-ttu-id="95146-156">Rozważ przypadek, który jest skojarzony z elementem `DataColumn` , który nie implementuje, `INullable` gdy jego podklasa jest.</span><span class="sxs-lookup"><span data-stu-id="95146-156">Consider the case of a UDT associated with a `DataColumn` that does not implement `INullable` while its sub-class does.</span></span> <span data-ttu-id="95146-157">W takim przypadku, jeśli zostanie przypisana silnie wpisana wartość null skojarzona z klasą pochodną, jest ona przechowywana jako bez typu `DbNull.Value` , ponieważ magazyn o wartości null jest zawsze spójny z typem danych DataColumn.</span><span class="sxs-lookup"><span data-stu-id="95146-157">In this case, if a strongly typed null value associated with the derived class is assigned, it is stored as an untyped `DbNull.Value`, because null storage is always consistent with the DataColumn's data type.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="95146-158">`Nullable<T>`Struktura lub <xref:System.Nullable> nie jest obecnie obsługiwana w `DataSet` .</span><span class="sxs-lookup"><span data-stu-id="95146-158">The `Nullable<T>` or <xref:System.Nullable> structure is not currently supported in the `DataSet`.</span></span>  
  
### <a name="multiple-column-row-assignment"></a><span data-ttu-id="95146-159">Przypisanie wielu kolumn (wierszy)</span><span class="sxs-lookup"><span data-stu-id="95146-159">Multiple Column (Row) Assignment</span></span>  

 <span data-ttu-id="95146-160">`DataTable.Add`, `DataTable.LoadDataRow` lub inne interfejsy API, które akceptują <xref:System.Data.DataRow.ItemArray%2A> , które są zamapowane na wiersz, mapują wartość "null" do wartości domyślnej DataColumn.</span><span class="sxs-lookup"><span data-stu-id="95146-160">`DataTable.Add`, `DataTable.LoadDataRow`, or other APIs that accept an <xref:System.Data.DataRow.ItemArray%2A> that gets mapped to a row, map 'null' to the DataColumn's default value.</span></span> <span data-ttu-id="95146-161">Jeśli obiekt w tablicy zawiera `DbNull.Value` lub jego silnie wpisaną, te same reguły, jak opisano powyżej, są stosowane.</span><span class="sxs-lookup"><span data-stu-id="95146-161">If an object in the array contains `DbNull.Value` or its strongly typed counterpart, the same rules as described above are applied.</span></span>  
  
 <span data-ttu-id="95146-162">Ponadto dla wystąpienia `DataRow.["columnName"]` przypisań o wartości null są stosowane następujące reguły:</span><span class="sxs-lookup"><span data-stu-id="95146-162">In addition, the following rules apply for an instance of `DataRow.["columnName"]` null assignments:</span></span>  
  
1. <span data-ttu-id="95146-163">Domyślna wartość *Domyślna* to `DbNull.Value` dla wszystkich, z wyjątkiem kolumn o jednoznacznie określonym typie, w których jest to odpowiednia silnie wpisana wartość null.</span><span class="sxs-lookup"><span data-stu-id="95146-163">The default *default* value is `DbNull.Value` for all except the strongly typed null columns where it is the appropriate strongly typed null value.</span></span>  
  
2. <span data-ttu-id="95146-164">Wartości null nigdy nie są zapisywane podczas serializacji do plików XML (podobnie jak w przypadku elementu "xsi: nil").</span><span class="sxs-lookup"><span data-stu-id="95146-164">Null values are never written out during serialization to XML files (as in "xsi:nil").</span></span>  
  
3. <span data-ttu-id="95146-165">Wszystkie wartości inne niż null, w tym wartości domyślne, są zawsze zapisywane podczas serializacji do formatu XML.</span><span class="sxs-lookup"><span data-stu-id="95146-165">All non-null values, including defaults, are always written out while serializing to XML.</span></span> <span data-ttu-id="95146-166">Jest to w przeciwieństwie do semantyki XSD/XML, gdzie wartość null (xsi: nil) jest jawna i wartość domyślna jest niejawna (jeśli nie jest obecny w kodzie XML, Analizator sprawdzania poprawności może pobrać go ze skojarzonego schematu XSD).</span><span class="sxs-lookup"><span data-stu-id="95146-166">This is unlike XSD/XML semantics where a null value (xsi:nil) is explicit and the default value is implicit (if not present in XML, a validating parser can get it from an associated XSD schema).</span></span> <span data-ttu-id="95146-167">Przeciwieństwo jest prawdziwe dla `DataTable` : wartość null jest niejawna, a wartość domyślna to explicit.</span><span class="sxs-lookup"><span data-stu-id="95146-167">The opposite is true for a `DataTable`: a null value is implicit and the default value is explicit.</span></span>  
  
4. <span data-ttu-id="95146-168">Wszystkie brakujące wartości kolumn dla wierszy odczytanych z danych wejściowych XML mają przypisane wartość NULL.</span><span class="sxs-lookup"><span data-stu-id="95146-168">All missing column values for rows read from XML input are assigned NULL.</span></span> <span data-ttu-id="95146-169">Do wierszy utworzonych przy użyciu <xref:System.Data.DataTable.NewRow%2A> lub podobnych metod są przypisywane wartości domyślnej kolumny DataColumn.</span><span class="sxs-lookup"><span data-stu-id="95146-169">Rows created using <xref:System.Data.DataTable.NewRow%2A> or similar methods are assigned the DataColumn's default value.</span></span>  
  
5. <span data-ttu-id="95146-170"><xref:System.Data.DataRow.IsNull%2A>Metoda zwraca `true` dla obu `DbNull.Value` i `INullable.Null` .</span><span class="sxs-lookup"><span data-stu-id="95146-170">The <xref:System.Data.DataRow.IsNull%2A> method returns `true` for both `DbNull.Value` and `INullable.Null`.</span></span>  
  
## <a name="assigning-null-values"></a><span data-ttu-id="95146-171">Przypisywanie wartości null</span><span class="sxs-lookup"><span data-stu-id="95146-171">Assigning Null Values</span></span>  

 <span data-ttu-id="95146-172">Wartość domyślna dla dowolnego <xref:System.Data.SqlTypes> wystąpienia ma wartość null.</span><span class="sxs-lookup"><span data-stu-id="95146-172">The default value for any <xref:System.Data.SqlTypes> instance is null.</span></span>  
  
 <span data-ttu-id="95146-173">Wartości null w <xref:System.Data.SqlTypes> są specyficzne dla typu i nie mogą być reprezentowane przez pojedynczą wartość, na przykład `DbNull` .</span><span class="sxs-lookup"><span data-stu-id="95146-173">Nulls in <xref:System.Data.SqlTypes> are type-specific and cannot be represented by a single value, such as `DbNull`.</span></span> <span data-ttu-id="95146-174">Użyj `IsNull` właściwości, aby sprawdzić wartości null.</span><span class="sxs-lookup"><span data-stu-id="95146-174">Use the `IsNull` property to check for nulls.</span></span>  
  
 <span data-ttu-id="95146-175">Wartości null można przypisywać do typu <xref:System.Data.DataColumn> , tak jak pokazano w poniższym przykładzie kodu.</span><span class="sxs-lookup"><span data-stu-id="95146-175">Null values can be assigned to a <xref:System.Data.DataColumn> as shown in the following code example.</span></span> <span data-ttu-id="95146-176">Można bezpośrednio przypisywać wartości null do `SqlTypes` zmiennych bez wyzwalania wyjątku.</span><span class="sxs-lookup"><span data-stu-id="95146-176">You can directly assign null values to `SqlTypes` variables without triggering an exception.</span></span>  
  
### <a name="example"></a><span data-ttu-id="95146-177">Przykład</span><span class="sxs-lookup"><span data-stu-id="95146-177">Example</span></span>  

 <span data-ttu-id="95146-178">Poniższy przykład kodu tworzy <xref:System.Data.DataTable> z dwoma kolumnami zdefiniowanymi jako <xref:System.Data.SqlTypes.SqlInt32> i <xref:System.Data.SqlTypes.SqlString> .</span><span class="sxs-lookup"><span data-stu-id="95146-178">The following code example creates a <xref:System.Data.DataTable> with two columns defined as <xref:System.Data.SqlTypes.SqlInt32> and <xref:System.Data.SqlTypes.SqlString>.</span></span> <span data-ttu-id="95146-179">Kod dodaje jeden wiersz znanych wartości, jeden wiersz wartości null, a następnie iteruje przez <xref:System.Data.DataTable> , przypisując wartości do zmiennych i wyświetlając dane wyjściowe w oknie konsoli.</span><span class="sxs-lookup"><span data-stu-id="95146-179">The code adds one row of known values, one row of null values and then iterates through the <xref:System.Data.DataTable>, assigning the values to variables and displaying the output in the console window.</span></span>  
  
 [!code-csharp[DataWorks SqlTypes.IsNull#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlTypes.IsNull/CS/source.cs#1)]
 [!code-vb[DataWorks SqlTypes.IsNull#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlTypes.IsNull/VB/source.vb#1)]  
  
 <span data-ttu-id="95146-180">W tym przykładzie są wyświetlane następujące wyniki:</span><span class="sxs-lookup"><span data-stu-id="95146-180">This example displays the following results:</span></span>  
  
```output
isColumnNull=False, ID=123, Description=Side Mirror  
isColumnNull=True, ID=Null, Description=Null  
```  
  
## <a name="comparing-null-values-with-sqltypes-and-clr-types"></a><span data-ttu-id="95146-181">Porównywanie wartości null z typami SqlTypes i CLR</span><span class="sxs-lookup"><span data-stu-id="95146-181">Comparing Null Values with SqlTypes and CLR Types</span></span>  

 <span data-ttu-id="95146-182">Porównując wartości null, ważne jest, aby zrozumieć różnicę między sposobem, `Equals` w jaki Metoda szacuje wartości null w <xref:System.Data.SqlTypes> porównaniu ze sposobem, w jaki działa z typami CLR.</span><span class="sxs-lookup"><span data-stu-id="95146-182">When comparing null values, it is important to understand the difference between the way the `Equals` method evaluates null values in <xref:System.Data.SqlTypes> as compared with the way it works with CLR types.</span></span> <span data-ttu-id="95146-183">Wszystkie <xref:System.Data.SqlTypes> `Equals` metody używają semantyki bazy danych do oceny wartości null: Jeśli jedna lub obie wartości mają wartość null, porównanie daje wartość null.</span><span class="sxs-lookup"><span data-stu-id="95146-183">All of the <xref:System.Data.SqlTypes>`Equals` methods use database semantics for evaluating null values: if either or both of the values is null, the comparison yields null.</span></span> <span data-ttu-id="95146-184">Z drugiej strony, użycie `Equals` metody CLR na dwóch <xref:System.Data.SqlTypes> zwróci wartość true, jeśli oba mają wartość null.</span><span class="sxs-lookup"><span data-stu-id="95146-184">On the other hand, using the CLR `Equals` method on two <xref:System.Data.SqlTypes> will yield true if both are null.</span></span> <span data-ttu-id="95146-185">Odzwierciedla to różnicę między użyciem metody wystąpienia, takiej jak `String.Equals` Metoda CLR, i przy użyciu metody static/Shared `SqlString.Equals` .</span><span class="sxs-lookup"><span data-stu-id="95146-185">This reflects the difference between using an instance method such as the CLR `String.Equals` method, and using the static/shared method, `SqlString.Equals`.</span></span>  
  
 <span data-ttu-id="95146-186">Poniższy przykład ilustruje różnicę w wynikach między `SqlString.Equals` metodą i `String.Equals` metodą, gdy każda z nich przekazuje parę wartości null, a następnie parę pustych ciągów.</span><span class="sxs-lookup"><span data-stu-id="95146-186">The following example demonstrates the difference in results between the `SqlString.Equals` method and the `String.Equals` method when each is passed a pair of null values and then a pair of empty strings.</span></span>  
  
 [!code-csharp[DataWorks SqlTypes.CompareNulls#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlTypes.CompareNulls/CS/source.cs#1)]
 [!code-vb[DataWorks SqlTypes.CompareNulls#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlTypes.CompareNulls/VB/source.vb#1)]  
  
 <span data-ttu-id="95146-187">Kod generuje następujące dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="95146-187">The code produces the following output:</span></span>  
  
```output
SqlString.Equals shared/static method:  
  Two nulls=Null  
  
String.Equals instance method:  
  Two nulls=True  
  
SqlString.Equals shared/static method:  
  Two empty strings=True  
  
String.Equals instance method:  
  Two empty strings=True
```  
  
## <a name="see-also"></a><span data-ttu-id="95146-188">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="95146-188">See also</span></span>

- [<span data-ttu-id="95146-189">Typy danych programu SQL Server i ADO.NET</span><span class="sxs-lookup"><span data-stu-id="95146-189">SQL Server Data Types and ADO.NET</span></span>](sql-server-data-types.md)
- [<span data-ttu-id="95146-190">Omówienie ADO.NET</span><span class="sxs-lookup"><span data-stu-id="95146-190">ADO.NET Overview</span></span>](../ado-net-overview.md)
