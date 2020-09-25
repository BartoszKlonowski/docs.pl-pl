---
title: Elementy DataTable
description: Dowiedz się więcej o elemencie DataTable ADO.NET, który reprezentuje jedną tabelę danych relacyjnych w pamięci, która jest lokalna dla. Aplikacja oparta na sieci, w której znajduje się.
ms.date: 03/30/2017
ms.assetid: 52ff0e32-3e5a-41de-9a3b-7b04ea52b83e
ms.openlocfilehash: d501096b4abe94653acdc5249c120abff94534d1
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91202308"
---
# <a name="datatables"></a><span data-ttu-id="14441-103">Elementy DataTable</span><span class="sxs-lookup"><span data-stu-id="14441-103">DataTables</span></span>

<span data-ttu-id="14441-104"><xref:System.Data.DataSet>Składa się z kolekcji tabel, relacji i ograniczeń.</span><span class="sxs-lookup"><span data-stu-id="14441-104">A <xref:System.Data.DataSet> is made up of a collection of tables, relationships, and constraints.</span></span> <span data-ttu-id="14441-105">W ADO.NET <xref:System.Data.DataTable> obiekty są używane do reprezentowania tabel w **zestawie danych**.</span><span class="sxs-lookup"><span data-stu-id="14441-105">In ADO.NET, <xref:System.Data.DataTable> objects are used to represent the tables in a **DataSet**.</span></span> <span data-ttu-id="14441-106">Element **DataTable** reprezentuje jedną tabelę danych relacyjnych w pamięci; dane są lokalne dla. Aplikacja oparta na sieci, w której znajduje się, ale może zostać wypełniona ze źródła danych, takiego jak Microsoft SQL Server przy użyciu elementu **DataAdapter** Aby uzyskać więcej informacji, zobacz [wypełnianie zestawu danych z elementu DataAdapter](../populating-a-dataset-from-a-dataadapter.md).</span><span class="sxs-lookup"><span data-stu-id="14441-106">A **DataTable** represents one table of in-memory relational data; the data is local to the .NET-based application in which it resides, but can be populated from a data source such as Microsoft SQL Server using a **DataAdapter** For more information, see [Populating a DataSet from a DataAdapter](../populating-a-dataset-from-a-dataadapter.md).</span></span>  
  
 <span data-ttu-id="14441-107">Klasa **DataTable** jest składową przestrzeni nazw **System. Data** w bibliotece klas .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="14441-107">The **DataTable** class is a member of the **System.Data** namespace within the .NET Framework class library.</span></span> <span data-ttu-id="14441-108">Można utworzyć i używać **DataTable** niezależnie lub jako elementu członkowskiego **zestawu danych**, a obiekty **DataTable** mogą być również używane w połączeniu z innymi obiektami .NET Framework, w tym <xref:System.Data.DataView> .</span><span class="sxs-lookup"><span data-stu-id="14441-108">You can create and use a **DataTable** independently or as a member of a **DataSet**, and **DataTable** objects can also be used in conjunction with other .NET Framework objects, including the <xref:System.Data.DataView>.</span></span> <span data-ttu-id="14441-109">Dostęp do kolekcji tabel w **zestawie danych** można uzyskać za pomocą właściwości **Tables** obiektu **DataSet** .</span><span class="sxs-lookup"><span data-stu-id="14441-109">You access the collection of tables in a **DataSet** through the **Tables** property of the **DataSet** object.</span></span>  
  
 <span data-ttu-id="14441-110">Schemat lub struktura tabeli jest reprezentowana przez kolumny i ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="14441-110">The schema, or structure of a table is represented by columns and constraints.</span></span> <span data-ttu-id="14441-111">Schemat **tabeli DataTable** można zdefiniować przy użyciu <xref:System.Data.DataColumn> obiektów Objects <xref:System.Data.ForeignKeyConstraint> oraz obiektów <xref:System.Data.UniqueConstraint> .</span><span class="sxs-lookup"><span data-stu-id="14441-111">You define the schema of a **DataTable** using <xref:System.Data.DataColumn> objects as well as <xref:System.Data.ForeignKeyConstraint> and <xref:System.Data.UniqueConstraint> objects.</span></span> <span data-ttu-id="14441-112">Kolumny w tabeli mogą być mapowane na kolumny w źródle danych, zawierają wartości obliczeniowe z wyrażeń, automatycznie zwiększają ich wartości lub zawierają wartości klucza podstawowego.</span><span class="sxs-lookup"><span data-stu-id="14441-112">The columns in a table can map to columns in a data source, contain calculated values from expressions, automatically increment their values, or contain primary key values.</span></span>  
  
 <span data-ttu-id="14441-113">Poza schematem element **DataTable** musi także zawierać wiersze, które zawierają i porządkują dane.</span><span class="sxs-lookup"><span data-stu-id="14441-113">In addition to a schema, a **DataTable** must also have rows to contain and order data.</span></span> <span data-ttu-id="14441-114"><xref:System.Data.DataRow>Klasa reprezentuje rzeczywiste dane zawarte w tabeli.</span><span class="sxs-lookup"><span data-stu-id="14441-114">The <xref:System.Data.DataRow> class represents the actual data contained in a table.</span></span> <span data-ttu-id="14441-115">Aby pobrać, oszacować i manipulować danymi w tabeli, należy użyć obiektu **DataRow** oraz jego właściwości i metod.</span><span class="sxs-lookup"><span data-stu-id="14441-115">You use the **DataRow** and its properties and methods to retrieve, evaluate, and manipulate the data in a table.</span></span> <span data-ttu-id="14441-116">Gdy uzyskujesz dostęp do danych i zmieniasz je w wierszu, obiekt **DataRow** zachowuje zarówno bieżący, jak i oryginalny stan.</span><span class="sxs-lookup"><span data-stu-id="14441-116">As you access and change the data within a row, the **DataRow** object maintains both its current and original state.</span></span>  
  
 <span data-ttu-id="14441-117">Można utworzyć relacje nadrzędny-podrzędny między tabelami przy użyciu co najmniej jednej powiązanej kolumny w tabelach.</span><span class="sxs-lookup"><span data-stu-id="14441-117">You can create parent-child relationships between tables using one or more related columns in the tables.</span></span> <span data-ttu-id="14441-118">Utwórz relację między obiektami **DataTable** przy użyciu <xref:System.Data.DataRelation> .</span><span class="sxs-lookup"><span data-stu-id="14441-118">You create a relationship between **DataTable** objects using a <xref:System.Data.DataRelation>.</span></span> <span data-ttu-id="14441-119">**Obiektów** można następnie użyć do zwrócenia powiązanych podrzędnych lub nadrzędnych wierszy określonego wiersza.</span><span class="sxs-lookup"><span data-stu-id="14441-119">**DataRelation** objects can then be used to return the related child or parent rows of a particular row.</span></span> <span data-ttu-id="14441-120">Aby uzyskać więcej informacji, zobacz [Dodawanie relacji](adding-datarelations.md)danych.</span><span class="sxs-lookup"><span data-stu-id="14441-120">For more information, see [Adding DataRelations](adding-datarelations.md).</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="14441-121">W tej sekcji</span><span class="sxs-lookup"><span data-stu-id="14441-121">In This Section</span></span>  

 [<span data-ttu-id="14441-122">Tworzenie elementu DataTable</span><span class="sxs-lookup"><span data-stu-id="14441-122">Creating a DataTable</span></span>](creating-a-datatable.md)  
 <span data-ttu-id="14441-123">Wyjaśnia, jak utworzyć element **DataTable** i dodać go do **zestawu danych**.</span><span class="sxs-lookup"><span data-stu-id="14441-123">Explains how to create a **DataTable** and add it to a **DataSet**.</span></span>  
  
 [<span data-ttu-id="14441-124">Definicja schematu elementu DataTable</span><span class="sxs-lookup"><span data-stu-id="14441-124">DataTable Schema Definition</span></span>](datatable-schema-definition.md)  
 <span data-ttu-id="14441-125">Zawiera informacje na temat tworzenia i używania obiektów i ograniczeń **kolumn** danych.</span><span class="sxs-lookup"><span data-stu-id="14441-125">Provides information about creating and using **DataColumn** objects and constraints.</span></span>  
  
 [<span data-ttu-id="14441-126">Operowanie na danych w elemencie DataTable</span><span class="sxs-lookup"><span data-stu-id="14441-126">Manipulating Data in a DataTable</span></span>](manipulating-data-in-a-datatable.md)  
 <span data-ttu-id="14441-127">Wyjaśnia, jak dodawać, modyfikować i usuwać dane w tabeli.</span><span class="sxs-lookup"><span data-stu-id="14441-127">Explains how to add, modify, and delete data in a table.</span></span> <span data-ttu-id="14441-128">Wyjaśnia, jak używać zdarzeń **DataTable** do sprawdzania zmian danych w tabeli.</span><span class="sxs-lookup"><span data-stu-id="14441-128">Explains how to use **DataTable** events to examine changes to data in the table.</span></span>  
  
 [<span data-ttu-id="14441-129">Obsługa zdarzeń elementu DataTable</span><span class="sxs-lookup"><span data-stu-id="14441-129">Handling DataTable Events</span></span>](handling-datatable-events.md)  
 <span data-ttu-id="14441-130">Zawiera informacje o zdarzeniach dostępnych do użycia z elementem **DataTable**, w tym zdarzenia, gdy wartości kolumn są modyfikowane, a wiersze są dodawane lub usuwane.</span><span class="sxs-lookup"><span data-stu-id="14441-130">Provides information about the events available for use with a **DataTable**, including events when column values are modified and rows are added or deleted.</span></span>  
  
## <a name="related-sections"></a><span data-ttu-id="14441-131">Sekcje pokrewne</span><span class="sxs-lookup"><span data-stu-id="14441-131">Related Sections</span></span>  

 [<span data-ttu-id="14441-132">ADO.NET</span><span class="sxs-lookup"><span data-stu-id="14441-132">ADO.NET</span></span>](../index.md)  
 <span data-ttu-id="14441-133">Opisuje architekturę i składniki ADO.NET oraz sposób ich używania do uzyskiwania dostępu do istniejących źródeł danych i zarządzania danymi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="14441-133">Describes the ADO.NET architecture and components, and how to use them to access existing data sources and manage application data.</span></span>  
  
 [<span data-ttu-id="14441-134">Elementy DataSet, DataTable i DataView</span><span class="sxs-lookup"><span data-stu-id="14441-134">DataSets, DataTables, and DataViews</span></span>](index.md)  
 <span data-ttu-id="14441-135">Zawiera informacje dotyczące **zestawu danych** ADO.NET, w tym sposób tworzenia relacji między tabelami.</span><span class="sxs-lookup"><span data-stu-id="14441-135">Provides information about the ADO.NET **DataSet** including how to create relationships between tables.</span></span>  
  
 <xref:System.Data.Constraint>  
 <span data-ttu-id="14441-136">Zawiera informacje referencyjne dotyczące obiektu **ograniczenia** .</span><span class="sxs-lookup"><span data-stu-id="14441-136">Provides reference information about the **Constraint** object.</span></span>  
  
 <xref:System.Data.DataColumn>  
 <span data-ttu-id="14441-137">Zawiera informacje referencyjne na temat obiektu **DataColumn** .</span><span class="sxs-lookup"><span data-stu-id="14441-137">Provides reference information about the **DataColumn** object.</span></span>  
  
 <xref:System.Data.DataSet>  
 <span data-ttu-id="14441-138">Zawiera informacje referencyjne o obiekcie **DataSet** .</span><span class="sxs-lookup"><span data-stu-id="14441-138">Provides reference information about the **DataSet** object.</span></span>  
  
 <xref:System.Data.DataTable>  
 <span data-ttu-id="14441-139">Zawiera informacje referencyjne dotyczące obiektu **DataTable** .</span><span class="sxs-lookup"><span data-stu-id="14441-139">Provides reference information about the **DataTable** object.</span></span>  
  
 [<span data-ttu-id="14441-140">Przegląd biblioteki klas</span><span class="sxs-lookup"><span data-stu-id="14441-140">Class Library Overview</span></span>](../../../../standard/class-library-overview.md)  
 <span data-ttu-id="14441-141">Zawiera przegląd biblioteki klas .NET Framework, w tym przestrzeń nazw **systemu** , a także jej przestrzeń nazw drugiego poziomu, **System. Data**.</span><span class="sxs-lookup"><span data-stu-id="14441-141">Provides an overview of the .NET Framework class library, including the **System** namespace as well as its second-level namespace, **System.Data**.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="14441-142">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="14441-142">See also</span></span>

- [<span data-ttu-id="14441-143">Omówienie ADO.NET</span><span class="sxs-lookup"><span data-stu-id="14441-143">ADO.NET Overview</span></span>](../ado-net-overview.md)
