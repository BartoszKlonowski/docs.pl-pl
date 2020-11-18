---
title: 'Instrukcje: otwieranie pliku dziennika i dołączanie do niego'
description: Otwórz i Dołącz do pliku dziennika przy użyciu klas StreamWriter — i StreamReader w programie .NET, które zapisują znaki i odczytują znaki ze strumieni.
ms.date: 01/21/2019
dev_langs:
- csharp
- vb
helpviewer_keywords:
- log files, opening
- streams, opening and appending to log file
- log files, appending to
- I/O [.NET], log files
ms.assetid: 74423362-1721-49cb-aa0a-e04005f72a06
ms.openlocfilehash: f92dd34b15ca79f229b365c7c2db4ace411d9353
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "94830756"
---
# <a name="how-to-open-and-append-to-a-log-file"></a>Instrukcje: otwieranie pliku dziennika i dołączanie do niego

<xref:System.IO.StreamWriter> i <xref:System.IO.StreamReader> pisać znaki do i odczytywanie znaków ze strumieni. Poniższy przykład kodu otwiera plik *log.txt* dla danych wejściowych lub tworzy go, jeśli nie istnieje, i dołącza informacje dziennika na końcu pliku. Przykład zapisuje zawartość pliku do standardowego wyjścia na potrzeby wyświetlania.

Alternatywą dla tego przykładu jest zapisanie informacji jako jednego ciągu lub tablicy ciągów i użycie <xref:System.IO.File.WriteAllText%2A?displayProperty=nameWithType> <xref:System.IO.File.WriteAllLines%2A?displayProperty=nameWithType> metody lub do osiągnięcia tych samych funkcji.  
  
> [!NOTE]
> Visual Basic użytkownicy mogą zdecydować się na użycie metod i właściwości dostarczonych przez <xref:Microsoft.VisualBasic.Logging.Log> klasę lub <xref:Microsoft.VisualBasic.FileIO.FileSystem> klasę do tworzenia lub zapisywania w plikach dziennika.  
  
## <a name="example"></a>Przykład  
 [!code-csharp[Conceptual.BasicIO.TextFiles#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.basicio.textfiles/cs/source2.cs#2)]
 [!code-vb[Conceptual.BasicIO.TextFiles#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.basicio.textfiles/vb/source2.vb#2)]  
  
## <a name="see-also"></a>Zobacz także

- <xref:System.IO.StreamWriter>  
- <xref:System.IO.StreamReader>  
- <xref:System.IO.File.AppendText%2A?displayProperty=nameWithType>  
- <xref:System.IO.File.OpenText%2A?displayProperty=nameWithType>  
- <xref:System.IO.StreamReader.ReadLine%2A?displayProperty=nameWithType>  
- [Instrukcje: Wyliczanie katalogów i plików](how-to-enumerate-directories-and-files.md)  
- [Instrukcje: Odczyt i zapis w nowo utworzonym pliku danych](how-to-read-and-write-to-a-newly-created-data-file.md)  
- [Instrukcje: odczytywanie tekstu z pliku](how-to-read-text-from-a-file.md)  
- [Instrukcje: wpisywanie tekstu do pliku](how-to-write-text-to-a-file.md)  
- [Instrukcje: odczytywanie znaków z ciągu](how-to-read-characters-from-a-string.md)  
- [Instrukcje: Wpisywanie znaków do ciągu](how-to-write-characters-to-a-string.md)  
- [We/wy plików i strumieni](index.md)
