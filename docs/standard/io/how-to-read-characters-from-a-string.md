---
title: 'Instrukcje: odczytywanie znaków z ciągu'
description: Dowiedz się, jak odczytywać znaki z ciągu w programie .NET. Zobacz przykłady odczytu znaków synchronicznie i asynchronicznie.
ms.date: 01/21/2019
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- reading characters from strings
- data streams, reading characters from string
- I/O [.NET], reading characters from strings
- reading data, strings
- streams, reading characters from string
ms.assetid: 27ea5e52-6db8-42d8-980a-50bcfc7fd270
ms.openlocfilehash: ef545ddd1bebf993db32b1ec450b38defd567f65
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "94830691"
---
# <a name="how-to-read-characters-from-a-string"></a><span data-ttu-id="228b2-104">Instrukcje: odczytywanie znaków z ciągu</span><span class="sxs-lookup"><span data-stu-id="228b2-104">How to: Read characters from a string</span></span>

<span data-ttu-id="228b2-105">Poniższy przykład kodu pokazuje, jak odczytywać znaki synchronicznie lub asynchronicznie z ciągu.</span><span class="sxs-lookup"><span data-stu-id="228b2-105">The following code examples show how to read characters synchronously or asynchronously from a string.</span></span>  
  
## <a name="example-read-characters-synchronously"></a><span data-ttu-id="228b2-106">Przykład: Odczytaj znaki synchronicznie</span><span class="sxs-lookup"><span data-stu-id="228b2-106">Example: Read characters synchronously</span></span>
 <span data-ttu-id="228b2-107">Ten przykład odczytuje 13 znaków synchronicznie z ciągu, zapisuje je w tablicy i wyświetla je.</span><span class="sxs-lookup"><span data-stu-id="228b2-107">This example reads 13 characters synchronously from a string, stores them in an array, and displays them.</span></span> <span data-ttu-id="228b2-108">Przykład odczytuje pozostałe znaki w ciągu, zapisuje je w tablicy, zaczynając od szóstego elementu i wyświetla zawartość tablicy.</span><span class="sxs-lookup"><span data-stu-id="228b2-108">The example then reads the rest of the characters in the string, stores them in the array starting at the sixth element, and displays the contents of the array.</span></span>  
  
 [!code-csharp[Conceptual.StringReader#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.stringreader/cs/source.cs#1)]
 [!code-vb[Conceptual.StringReader#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.stringreader/vb/source.vb#1)]  
  
## <a name="example-read-characters-asynchronously"></a><span data-ttu-id="228b2-109">Przykład: odczytywanie znaków asynchronicznie</span><span class="sxs-lookup"><span data-stu-id="228b2-109">Example: Read characters asynchronously</span></span>  
 <span data-ttu-id="228b2-110">Następny przykład to kod związany z aplikacją WPF.</span><span class="sxs-lookup"><span data-stu-id="228b2-110">The next example is the code behind a WPF app.</span></span> <span data-ttu-id="228b2-111">W przypadku ładowania okna przykład Asynchronicznie odczytuje wszystkie znaki z <xref:System.Windows.Controls.TextBox> kontrolki i zapisuje je w tablicy.</span><span class="sxs-lookup"><span data-stu-id="228b2-111">On window load, the example asynchronously reads all characters from a <xref:System.Windows.Controls.TextBox> control and stores them in an array.</span></span> <span data-ttu-id="228b2-112">Następnie asynchronicznie zapisuje każdą literę lub biały znak w osobnym wierszu <xref:System.Windows.Controls.TextBlock> kontrolki.</span><span class="sxs-lookup"><span data-stu-id="228b2-112">It then asynchronously writes each letter or white-space character to a separate line of a <xref:System.Windows.Controls.TextBlock> control.</span></span>  
  
 [!code-csharp[Conceptual.StringReader#2](../../../samples/snippets/csharp/VS_Snippets_Wpf/StringReaderWriter/MainWindow.xaml.cs)]
 [!code-vb[Conceptual.StringReader#2](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/StringReaderWriter/MainWindow.xaml.vb)]  
  
## <a name="see-also"></a><span data-ttu-id="228b2-113">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="228b2-113">See also</span></span>

- <xref:System.IO.StringReader>  
- <xref:System.IO.StringReader.Read%2A?displayProperty=nameWithType>  
- [<span data-ttu-id="228b2-114">Asynchroniczne operacje we/wy pliku</span><span class="sxs-lookup"><span data-stu-id="228b2-114">Asynchronous file I/O</span></span>](asynchronous-file-i-o.md)  
- <span data-ttu-id="228b2-115">[Instrukcje: Tworzenie listy katalogów](/previous-versions/dotnet/netframework-4.0/5cf8zcfh(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="228b2-115">[How to: Create a directory listing](/previous-versions/dotnet/netframework-4.0/5cf8zcfh(v=vs.100))</span></span>  
- [<span data-ttu-id="228b2-116">Instrukcje: Odczyt i zapis w nowo utworzonym pliku danych</span><span class="sxs-lookup"><span data-stu-id="228b2-116">How to: Read and write to a newly created data file</span></span>](how-to-read-and-write-to-a-newly-created-data-file.md)  
- [<span data-ttu-id="228b2-117">Instrukcje: otwieranie pliku dziennika i dołączanie do niego</span><span class="sxs-lookup"><span data-stu-id="228b2-117">How to: Open and append to a log file</span></span>](how-to-open-and-append-to-a-log-file.md)  
- [<span data-ttu-id="228b2-118">Instrukcje: odczytywanie tekstu z pliku</span><span class="sxs-lookup"><span data-stu-id="228b2-118">How to: Read text from a file</span></span>](how-to-read-text-from-a-file.md)  
- [<span data-ttu-id="228b2-119">Instrukcje: wpisywanie tekstu do pliku</span><span class="sxs-lookup"><span data-stu-id="228b2-119">How to: Write text to a file</span></span>](how-to-write-text-to-a-file.md)  
- [<span data-ttu-id="228b2-120">Instrukcje: Wpisywanie znaków do ciągu</span><span class="sxs-lookup"><span data-stu-id="228b2-120">How to: Write characters to a string</span></span>](how-to-write-characters-to-a-string.md)  
- [<span data-ttu-id="228b2-121">We/wy plików i strumieni</span><span class="sxs-lookup"><span data-stu-id="228b2-121">File and stream I/O</span></span>](index.md)
