---
title: 'Instrukcje: kompresowanie i wyodrębnianie plików'
description: Kompresuj & Wyodrębnianie plików przy użyciu metody System. IO. Compression. Zobacz przykłady użycia ZipFile, ZipArchive, ZipArchiveEntry, DeflateStream, & GZipStream.
ms.date: 01/14/2019
dev_langs:
- csharp
- vb
helpviewer_keywords:
- I/O [.NET], compression
- compression
- compress files
ms.assetid: e9876165-3c60-4c84-a272-513e47acf579
ms.openlocfilehash: a1077c7277e0aa54e3c8883cfc27d93926485b8e
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "94830860"
---
# <a name="how-to-compress-and-extract-files"></a>Instrukcje: kompresowanie i wyodrębnianie plików

<xref:System.IO.Compression>Przestrzeń nazw zawiera następujące typy do kompresowania i dekompresowania plików i strumieni. Możesz również użyć tych typów do odczytu i modyfikacji zawartości skompresowanego pliku.

- <xref:System.IO.Compression.ZipFile>
- <xref:System.IO.Compression.ZipArchive>
- <xref:System.IO.Compression.ZipArchiveEntry>
- <xref:System.IO.Compression.DeflateStream>
- <xref:System.IO.Compression.GZipStream>

W poniższych przykładach przedstawiono niektóre operacje, które można wykonywać przy użyciu skompresowanych plików. Te przykłady wymagają dodania następujących pakietów NuGet do projektu:

- [System. IO. Compression](https://www.nuget.org/packages/System.IO.Compression)
- [ PlikSystem.IO.Compression.Zip](https://www.nuget.org/packages/System.IO.Compression.ZipFile)

Jeśli używasz .NET Framework, Dodaj odwołania do tych dwóch bibliotek do projektu:

- `System.IO.Compression`
- `System.IO.Compression.FileSystem`

## <a name="example-1-create-and-extract-a-zip-file"></a>Przykład 1: Tworzenie i Wyodrębnianie pliku zip

Poniższy przykład pokazuje, jak utworzyć i wyodrębnić skompresowany plik *zip* przy użyciu <xref:System.IO.Compression.ZipFile> klasy. Przykład kompresuje zawartość folderu do nowego pliku *zip* , a następnie wyodrębnia plik zip do nowego folderu.

Aby uruchomić przykład, należy utworzyć folder *startowy* w folderze programu i wypełnić go plikami do pliku zip.

[!code-csharp[System.IO.Compression.ZipFile#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.compression.zipfile/cs/program1.cs#1)]
[!code-vb[System.IO.Compression.ZipFile#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.compression.zipfile/vb/program1.vb#1)]

## <a name="example-2-extract-specific-file-extensions"></a>Przykład 2: Wyodrębnienie określonych rozszerzeń plików

Następny przykład wykonuje iterację zawartości istniejącego pliku *. zip* i wyodrębnia pliki z rozszerzeniem *. txt* . Używa <xref:System.IO.Compression.ZipArchive> klasy w celu uzyskania dostępu do pliku zip oraz <xref:System.IO.Compression.ZipArchiveEntry> klasy do inspekcji poszczególnych wpisów. Metoda rozszerzenia <xref:System.IO.Compression.ZipFileExtensions.ExtractToFile%2A> dla <xref:System.IO.Compression.ZipArchiveEntry> obiektu jest dostępna w <xref:System.IO.Compression.ZipFileExtensions?displayProperty=nameWithType> klasie.

Aby uruchomić przykład, Umieść plik *zip* o nazwie *result.zip* w folderze programu. Po wyświetleniu monitu podaj nazwę folderu do wyodrębnienia.

> [!IMPORTANT]
> Podczas rozpakowywania plików należy wyszukać złośliwe ścieżki plików, które mogą wyjść z katalogu, w którym się znajdujesz. Jest to tzw. atak przechodzenia do lokalizacji. W poniższym przykładzie pokazano, jak wyszukiwać złośliwe ścieżki plików i zapewniać bezpieczną metodę rozpakowania.

[!code-csharp[System.IO.Compression.ZipArchive#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.compression.ziparchive/cs/program1.cs#1)]
[!code-vb[System.IO.Compression.ZipArchive#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.compression.ziparchive/vb/program1.vb#1)]

## <a name="example-3-add-a-file-to-an-existing-zip"></a>Przykład 3: Dodaj plik do istniejącego pliku zip

Poniższy przykład używa <xref:System.IO.Compression.ZipArchive> klasy, aby uzyskać dostęp do istniejącego pliku *. zip* i dodaje do niego plik. Nowy plik zostanie skompresowany po dodaniu go do istniejącego pliku zip.

[!code-csharp[System.IO.Compression.ZipArchiveMode#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.compression.ziparchivemode/cs/program1.cs#1)]
[!code-vb[System.IO.Compression.ZipArchiveMode#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.compression.ziparchivemode/vb/program1.vb#1)]

## <a name="example-4-compress-and-decompress-gz-files"></a>Przykład 4: kompresowanie i dekompresowanie plików. gz

Można również użyć <xref:System.IO.Compression.GZipStream> <xref:System.IO.Compression.DeflateStream> klas i do kompresowania i dekompresowania danych. Korzystają one z tego samego algorytmu kompresji. Można dekompresowanie <xref:System.IO.Compression.GZipStream> obiektów, które są zapisywane w pliku *. gz* za pomocą wielu popularnych narzędzi. Poniższy przykład przedstawia sposób kompresowania i dekompresowania katalogu plików przy użyciu <xref:System.IO.Compression.GZipStream> klasy:

[!code-csharp[IO.Compression.GZip1#1](../../../samples/snippets/csharp/VS_Snippets_CLR/IO.Compression.GZip1/CS/gziptest.cs#1)]
[!code-vb[IO.Compression.GZip1#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/IO.Compression.GZip1/VB/gziptest.vb#1)]

## <a name="see-also"></a>Zobacz także

- <xref:System.IO.Compression.ZipArchive>  
- <xref:System.IO.Compression.ZipFile>  
- <xref:System.IO.Compression.ZipArchiveEntry>  
- <xref:System.IO.Compression.DeflateStream>  
- <xref:System.IO.Compression.GZipStream>  
- [We/wy plików i strumieni](index.md)
