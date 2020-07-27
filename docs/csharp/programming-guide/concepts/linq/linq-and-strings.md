---
title: LINQ i ciągi (C#)
description: LINQ może wykonywać zapytania i przekształcać ciągi i kolekcje ciągów. Zapytania LINQ można łączyć z funkcjami ciągów języka C# i wyrażeniami regularnymi.
ms.date: 07/20/2015
ms.assetid: dbe2d657-b3f3-487e-b645-21fb2d71cd7b
ms.openlocfilehash: c515a0c56ad6473f93c6339540e4ed0245bb5bd2
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/24/2020
ms.locfileid: "87165620"
---
# <a name="linq-and-strings-c"></a><span data-ttu-id="30d40-104">LINQ i ciągi (C#)</span><span class="sxs-lookup"><span data-stu-id="30d40-104">LINQ and strings (C#)</span></span>

<span data-ttu-id="30d40-105">LINQ może służyć do wykonywania zapytań i przekształcania ciągów i kolekcji ciągów.</span><span class="sxs-lookup"><span data-stu-id="30d40-105">LINQ can be used to query and transform strings and collections of strings.</span></span> <span data-ttu-id="30d40-106">Może być szczególnie przydatne w przypadku danych z częściową strukturą w plikach tekstowych.</span><span class="sxs-lookup"><span data-stu-id="30d40-106">It can be especially useful with semi-structured data in text files.</span></span> <span data-ttu-id="30d40-107">Zapytania LINQ można łączyć z tradycyjnymi funkcjami ciągów i wyrażeniami regularnymi.</span><span class="sxs-lookup"><span data-stu-id="30d40-107">LINQ queries can be combined with traditional string functions and regular expressions.</span></span> <span data-ttu-id="30d40-108">Na przykład można użyć <xref:System.String.Split%2A?displayProperty=nameWithType> metody lub, <xref:System.Text.RegularExpressions.Regex.Split%2A?displayProperty=nameWithType> Aby utworzyć tablicę ciągów, które można następnie wykonać zapytania lub zmodyfikować przy użyciu LINQ.</span><span class="sxs-lookup"><span data-stu-id="30d40-108">For example, you can use the <xref:System.String.Split%2A?displayProperty=nameWithType> or <xref:System.Text.RegularExpressions.Regex.Split%2A?displayProperty=nameWithType> method to create an array of strings that you can then query or modify by using LINQ.</span></span> <span data-ttu-id="30d40-109">Możesz użyć <xref:System.Text.RegularExpressions.Regex.IsMatch%2A?displayProperty=nameWithType> metody w `where` klauzuli zapytania LINQ.</span><span class="sxs-lookup"><span data-stu-id="30d40-109">You can use the <xref:System.Text.RegularExpressions.Regex.IsMatch%2A?displayProperty=nameWithType> method in the `where` clause of a LINQ query.</span></span> <span data-ttu-id="30d40-110">I można użyć LINQ do zapytania lub zmodyfikować <xref:System.Text.RegularExpressions.MatchCollection> wyniki zwrócone przez wyrażenie regularne.</span><span class="sxs-lookup"><span data-stu-id="30d40-110">And you can use LINQ to query or modify the <xref:System.Text.RegularExpressions.MatchCollection> results returned by a regular expression.</span></span>

<span data-ttu-id="30d40-111">Można również użyć technik opisanych w tej sekcji, aby przekształcić dane z częściową strukturą do formatu XML.</span><span class="sxs-lookup"><span data-stu-id="30d40-111">You can also use the techniques described in this section to transform semi-structured text data to XML.</span></span> <span data-ttu-id="30d40-112">Aby uzyskać więcej informacji, zobacz [jak generować XML z plików CSV](how-to-generate-xml-from-csv-files.md).</span><span class="sxs-lookup"><span data-stu-id="30d40-112">For more information, see [How to generate XML from CSV files](how-to-generate-xml-from-csv-files.md).</span></span>

<span data-ttu-id="30d40-113">Przykłady w tej sekcji należą do dwóch kategorii:</span><span class="sxs-lookup"><span data-stu-id="30d40-113">The examples in this section fall into two categories:</span></span>

## <a name="querying-a-block-of-text"></a><span data-ttu-id="30d40-114">Wykonywanie zapytania dotyczącego bloku tekstu</span><span class="sxs-lookup"><span data-stu-id="30d40-114">Querying a block of text</span></span>

<span data-ttu-id="30d40-115">Można wykonywać zapytania, analizować i modyfikować bloki tekstu, dzieląc je na tablicę Queryable mniejszych ciągów przy użyciu <xref:System.String.Split%2A?displayProperty=nameWithType> metody lub <xref:System.Text.RegularExpressions.Regex.Split%2A?displayProperty=nameWithType> metody.</span><span class="sxs-lookup"><span data-stu-id="30d40-115">You can query, analyze, and modify text blocks by splitting them into a queryable array of smaller strings by using the <xref:System.String.Split%2A?displayProperty=nameWithType> method or the <xref:System.Text.RegularExpressions.Regex.Split%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="30d40-116">Możesz podzielić tekst źródłowy na słowa, zdania, akapity, strony lub inne kryteria, a następnie wykonać dodatkowe podziały, jeśli są one wymagane w zapytaniu.</span><span class="sxs-lookup"><span data-stu-id="30d40-116">You can split the source text into words, sentences, paragraphs, pages, or any other criteria, and then perform additional splits if they are required in your query.</span></span>

- [<span data-ttu-id="30d40-117">Jak zliczyć wystąpienia wyrazu w ciągu (LINQ) (C#)</span><span class="sxs-lookup"><span data-stu-id="30d40-117">How to count occurrences of a word in a string (LINQ) (C#)</span></span>](how-to-count-occurrences-of-a-word-in-a-string-linq.md)  
  <span data-ttu-id="30d40-118">Pokazuje, jak używać LINQ do prostego wykonywania zapytań względem tekstu.</span><span class="sxs-lookup"><span data-stu-id="30d40-118">Shows how to use LINQ for simple querying over text.</span></span>

- [<span data-ttu-id="30d40-119">Jak wykonać zapytanie o zdania zawierające określony zestaw wyrazów (LINQ) (C#)</span><span class="sxs-lookup"><span data-stu-id="30d40-119">How to query for sentences that contain a specified set of words (LINQ) (C#)</span></span>](how-to-query-for-sentences-that-contain-a-specified-set-of-words-linq.md)

  <span data-ttu-id="30d40-120">Pokazuje sposób dzielenia plików tekstowych na dowolne granice oraz wykonywania zapytań dotyczących poszczególnych części.</span><span class="sxs-lookup"><span data-stu-id="30d40-120">Shows how to split text files on arbitrary boundaries and how to perform queries against each part.</span></span>

- [<span data-ttu-id="30d40-121">Jak wykonać zapytanie o znaki w ciągu (LINQ) (C#)</span><span class="sxs-lookup"><span data-stu-id="30d40-121">How to query for characters in a string (LINQ) (C#)</span></span>](how-to-query-for-characters-in-a-string-linq.md)

  <span data-ttu-id="30d40-122">Pokazuje, że ciąg jest typem queryable.</span><span class="sxs-lookup"><span data-stu-id="30d40-122">Demonstrates that a string is a queryable type.</span></span>

- [<span data-ttu-id="30d40-123">Jak połączyć zapytania LINQ z wyrażeniami regularnymi (C#)</span><span class="sxs-lookup"><span data-stu-id="30d40-123">How to combine LINQ queries with regular expressions (C#)</span></span>](how-to-combine-linq-queries-with-regular-expressions.md)

  <span data-ttu-id="30d40-124">Pokazuje, jak używać wyrażeń regularnych w zapytaniach LINQ dla złożonego dopasowania do wzorca na filtrowanych wynikach zapytań.</span><span class="sxs-lookup"><span data-stu-id="30d40-124">Shows how to use regular expressions in LINQ queries for complex pattern matching on filtered query results.</span></span>

## <a name="querying-semi-structured-data-in-text-format"></a><span data-ttu-id="30d40-125">Wykonywanie zapytania dotyczącego danych z częściową strukturą w formacie tekstowym</span><span class="sxs-lookup"><span data-stu-id="30d40-125">Querying semi-structured data in text format</span></span>

<span data-ttu-id="30d40-126">Wiele różnych typów plików tekstowych składa się z szeregu wierszy, często z podobnym formatowaniem, takim jak pliki rozdzielane znakami tabulacji lub rozdzielonymi długościami.</span><span class="sxs-lookup"><span data-stu-id="30d40-126">Many different types of text files consist of a series of lines, often with similar formatting, such as tab- or comma-delimited files or fixed-length lines.</span></span> <span data-ttu-id="30d40-127">Po przeczytaniu takiego pliku tekstowego do pamięci można użyć LINQ do wykonywania zapytań i/lub modyfikowania wierszy.</span><span class="sxs-lookup"><span data-stu-id="30d40-127">After you read such a text file into memory, you can use LINQ to query and/or modify the lines.</span></span> <span data-ttu-id="30d40-128">Zapytania LINQ upraszczają także zadanie łączenia danych z wielu źródeł.</span><span class="sxs-lookup"><span data-stu-id="30d40-128">LINQ queries also simplify the task of combining data from multiple sources.</span></span>

- [<span data-ttu-id="30d40-129">Jak znaleźć różnice między dwoma listami (LINQ) (C#)</span><span class="sxs-lookup"><span data-stu-id="30d40-129">How to find the set difference between two lists (LINQ) (C#)</span></span>](how-to-find-the-set-difference-between-two-lists-linq.md)

  <span data-ttu-id="30d40-130">Pokazuje, jak znaleźć wszystkie ciągi, które znajdują się na jednej liście, ale nie w drugim.</span><span class="sxs-lookup"><span data-stu-id="30d40-130">Shows how to find all the strings that are present in one list but not the other.</span></span>

- [<span data-ttu-id="30d40-131">Sortowanie lub filtrowanie danych tekstowych według dowolnego wyrazu lub pola (LINQ) (C#)</span><span class="sxs-lookup"><span data-stu-id="30d40-131">How to sort or filter text data by any word or field (LINQ) (C#)</span></span>](how-to-sort-or-filter-text-data-by-any-word-or-field-linq.md)

  <span data-ttu-id="30d40-132">Pokazuje, jak sortować wiersze tekstu na podstawie dowolnego wyrazu lub pola.</span><span class="sxs-lookup"><span data-stu-id="30d40-132">Shows how to sort text lines based on any word or field.</span></span>

- [<span data-ttu-id="30d40-133">Jak zmienić kolejność pól w rozdzielonym pliku (LINQ) (C#)</span><span class="sxs-lookup"><span data-stu-id="30d40-133">How to reorder the fields of a delimited file (LINQ) (C#)</span></span>](how-to-reorder-the-fields-of-a-delimited-file-linq.md)

  <span data-ttu-id="30d40-134">Pokazuje, jak zmienić kolejność pól w wierszu w pliku CSV.</span><span class="sxs-lookup"><span data-stu-id="30d40-134">Shows how to reorder fields in a line in a .csv file.</span></span>

- [<span data-ttu-id="30d40-135">Łączenie i porównywanie kolekcji ciągów (LINQ) (C#)</span><span class="sxs-lookup"><span data-stu-id="30d40-135">How to combine and compare string collections (LINQ) (C#)</span></span>](how-to-combine-and-compare-string-collections-linq.md)

  <span data-ttu-id="30d40-136">Pokazuje, jak łączyć listy ciągów na różne sposoby.</span><span class="sxs-lookup"><span data-stu-id="30d40-136">Shows how to combine string lists in various ways.</span></span>

- [<span data-ttu-id="30d40-137">Jak wypełnić kolekcje obiektów z wielu źródeł (LINQ) (C#)</span><span class="sxs-lookup"><span data-stu-id="30d40-137">How to populate object collections from multiple sources (LINQ) (C#)</span></span>](how-to-populate-object-collections-from-multiple-sources-linq.md)

  <span data-ttu-id="30d40-138">Pokazuje, jak tworzyć kolekcje obiektów przy użyciu wielu plików tekstowych jako źródła danych.</span><span class="sxs-lookup"><span data-stu-id="30d40-138">Shows how to create object collections by using multiple text files as data sources.</span></span>

- [<span data-ttu-id="30d40-139">Jak dołączyć zawartość z niepodobnych plików (LINQ) (C#)</span><span class="sxs-lookup"><span data-stu-id="30d40-139">How to join content from dissimilar files (LINQ) (C#)</span></span>](how-to-join-content-from-dissimilar-files-linq.md)
  
  <span data-ttu-id="30d40-140">Pokazuje, w jaki sposób połączyć ciągi w dwóch listach w jeden ciąg za pomocą pasującego klucza.</span><span class="sxs-lookup"><span data-stu-id="30d40-140">Shows how to combine strings in two lists into a single string by using a matching key.</span></span>

- [<span data-ttu-id="30d40-141">Jak podzielić plik na wiele plików przy użyciu grup (LINQ) (C#)</span><span class="sxs-lookup"><span data-stu-id="30d40-141">How to split a file into many files by using groups (LINQ) (C#)</span></span>](how-to-split-a-file-into-many-files-by-using-groups-linq.md)
  
  <span data-ttu-id="30d40-142">Pokazuje, jak tworzyć nowe pliki przy użyciu pojedynczego pliku jako źródła danych.</span><span class="sxs-lookup"><span data-stu-id="30d40-142">Shows how to create new files by using a single file as a data source.</span></span>

- [<span data-ttu-id="30d40-143">Jak obliczyć wartości kolumn w pliku tekstowym CSV (LINQ) (C#)</span><span class="sxs-lookup"><span data-stu-id="30d40-143">How to compute column values in a CSV text file (LINQ) (C#)</span></span>](how-to-compute-column-values-in-a-csv-text-file-linq.md)
  
  <span data-ttu-id="30d40-144">Pokazuje, jak wykonywać obliczenia matematyczne na danych tekstowych w plikach CSV.</span><span class="sxs-lookup"><span data-stu-id="30d40-144">Shows how to perform mathematical computations on text data in .csv files.</span></span>

## <a name="see-also"></a><span data-ttu-id="30d40-145">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="30d40-145">See also</span></span>

- [<span data-ttu-id="30d40-146">Language-Integrated Query (LINQ) (C#)</span><span class="sxs-lookup"><span data-stu-id="30d40-146">Language-Integrated Query (LINQ) (C#)</span></span>](index.md)
- [<span data-ttu-id="30d40-147">Generowanie kodu XML z plików CSV</span><span class="sxs-lookup"><span data-stu-id="30d40-147">How to generate XML from CSV files</span></span>](how-to-generate-xml-from-csv-files.md)
