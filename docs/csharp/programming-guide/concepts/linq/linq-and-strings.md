---
title: LINQ i ciągi (C#)
description: LINQ może wykonywać zapytania i przekształcać ciągi i kolekcje ciągów. Zapytania LINQ można łączyć z funkcjami ciągów języka C# i wyrażeniami regularnymi.
ms.date: 07/20/2015
ms.assetid: dbe2d657-b3f3-487e-b645-21fb2d71cd7b
ms.openlocfilehash: 0500d821335659fa29dd4809513f38dac0a8b193
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90556723"
---
# <a name="linq-and-strings-c"></a>LINQ i ciągi (C#)

LINQ może służyć do wykonywania zapytań i przekształcania ciągów i kolekcji ciągów. Może być szczególnie przydatne w przypadku danych z częściową strukturą w plikach tekstowych. Zapytania LINQ można łączyć z tradycyjnymi funkcjami ciągów i wyrażeniami regularnymi. Na przykład można użyć <xref:System.String.Split%2A?displayProperty=nameWithType> metody lub, <xref:System.Text.RegularExpressions.Regex.Split%2A?displayProperty=nameWithType> Aby utworzyć tablicę ciągów, które można następnie wykonać zapytania lub zmodyfikować przy użyciu LINQ. Możesz użyć <xref:System.Text.RegularExpressions.Regex.IsMatch%2A?displayProperty=nameWithType> metody w `where` klauzuli zapytania LINQ. I można użyć LINQ do zapytania lub zmodyfikować <xref:System.Text.RegularExpressions.MatchCollection> wyniki zwrócone przez wyrażenie regularne.

Można również użyć technik opisanych w tej sekcji, aby przekształcić dane z częściową strukturą do formatu XML. Aby uzyskać więcej informacji, zobacz [jak generować XML z plików CSV](../../../../standard/linq/generate-xml-csv-files.md).

Przykłady w tej sekcji należą do dwóch kategorii:

## <a name="querying-a-block-of-text"></a>Wykonywanie zapytania dotyczącego bloku tekstu

Można wykonywać zapytania, analizować i modyfikować bloki tekstu, dzieląc je na tablicę Queryable mniejszych ciągów przy użyciu <xref:System.String.Split%2A?displayProperty=nameWithType> metody lub <xref:System.Text.RegularExpressions.Regex.Split%2A?displayProperty=nameWithType> metody. Możesz podzielić tekst źródłowy na słowa, zdania, akapity, strony lub inne kryteria, a następnie wykonać dodatkowe podziały, jeśli są one wymagane w zapytaniu.

- [Jak zliczyć wystąpienia wyrazu w ciągu (LINQ) (C#)](how-to-count-occurrences-of-a-word-in-a-string-linq.md)  
  Pokazuje, jak używać LINQ do prostego wykonywania zapytań względem tekstu.

- [Jak wykonać zapytanie o zdania zawierające określony zestaw wyrazów (LINQ) (C#)](how-to-query-for-sentences-that-contain-a-specified-set-of-words-linq.md)

  Pokazuje sposób dzielenia plików tekstowych na dowolne granice oraz wykonywania zapytań dotyczących poszczególnych części.

- [Jak wykonać zapytanie o znaki w ciągu (LINQ) (C#)](how-to-query-for-characters-in-a-string-linq.md)

  Pokazuje, że ciąg jest typem queryable.

- [Jak połączyć zapytania LINQ z wyrażeniami regularnymi (C#)](how-to-combine-linq-queries-with-regular-expressions.md)

  Pokazuje, jak używać wyrażeń regularnych w zapytaniach LINQ dla złożonego dopasowania do wzorca na filtrowanych wynikach zapytań.

## <a name="querying-semi-structured-data-in-text-format"></a>Wykonywanie zapytania dotyczącego danych z częściową strukturą w formacie tekstowym

Wiele różnych typów plików tekstowych składa się z szeregu wierszy, często z podobnym formatowaniem, takim jak pliki rozdzielane znakami tabulacji lub rozdzielonymi długościami. Po przeczytaniu takiego pliku tekstowego do pamięci można użyć LINQ do wykonywania zapytań i/lub modyfikowania wierszy. Zapytania LINQ upraszczają także zadanie łączenia danych z wielu źródeł.

- [Jak znaleźć różnice między dwoma listami (LINQ) (C#)](how-to-find-the-set-difference-between-two-lists-linq.md)

  Pokazuje, jak znaleźć wszystkie ciągi, które znajdują się na jednej liście, ale nie w drugim.

- [Sortowanie lub filtrowanie danych tekstowych według dowolnego wyrazu lub pola (LINQ) (C#)](how-to-sort-or-filter-text-data-by-any-word-or-field-linq.md)

  Pokazuje, jak sortować wiersze tekstu na podstawie dowolnego wyrazu lub pola.

- [Jak zmienić kolejność pól w rozdzielonym pliku (LINQ) (C#)](how-to-reorder-the-fields-of-a-delimited-file-linq.md)

  Pokazuje, jak zmienić kolejność pól w wierszu w pliku CSV.

- [Łączenie i porównywanie kolekcji ciągów (LINQ) (C#)](how-to-combine-and-compare-string-collections-linq.md)

  Pokazuje, jak łączyć listy ciągów na różne sposoby.

- [Jak wypełnić kolekcje obiektów z wielu źródeł (LINQ) (C#)](how-to-populate-object-collections-from-multiple-sources-linq.md)

  Pokazuje, jak tworzyć kolekcje obiektów przy użyciu wielu plików tekstowych jako źródła danych.

- [Jak dołączyć zawartość z niepodobnych plików (LINQ) (C#)](how-to-join-content-from-dissimilar-files-linq.md)
  
  Pokazuje, w jaki sposób połączyć ciągi w dwóch listach w jeden ciąg za pomocą pasującego klucza.

- [Jak podzielić plik na wiele plików przy użyciu grup (LINQ) (C#)](how-to-split-a-file-into-many-files-by-using-groups-linq.md)
  
  Pokazuje, jak tworzyć nowe pliki przy użyciu pojedynczego pliku jako źródła danych.

- [Jak obliczyć wartości kolumn w pliku tekstowym CSV (LINQ) (C#)](how-to-compute-column-values-in-a-csv-text-file-linq.md)
  
  Pokazuje, jak wykonywać obliczenia matematyczne na danych tekstowych w plikach CSV.

## <a name="see-also"></a>Zobacz także

- [Language-Integrated Query (LINQ) (C#)](index.md)
- [Generowanie kodu XML z plików CSV](../../../../standard/linq/generate-xml-csv-files.md)
