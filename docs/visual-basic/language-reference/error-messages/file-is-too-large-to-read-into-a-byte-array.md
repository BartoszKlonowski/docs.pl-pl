---
title: Plik jest za duży, aby odczytać z tablicy bajtów
ms.date: 07/20/2015
ms.assetid: 686630a6-a439-46c7-8d7b-34613ae4c5d8
ms.openlocfilehash: 89459aaf766a70f69008f847dda7ac6e2a1e41d1
ms.sourcegitcommit: d2db216e46323f73b32ae312c9e4135258e5d68e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "90874188"
---
# <a name="file-is-too-large-to-read-into-a-byte-array"></a><span data-ttu-id="d4354-102">Plik jest za duży, aby odczytać z tablicy bajtów</span><span class="sxs-lookup"><span data-stu-id="d4354-102">File is too large to read into a byte array</span></span>

<span data-ttu-id="d4354-103">Rozmiar pliku, który próbujesz odczytać do tablicy bajtów, przekracza 4 GB.</span><span class="sxs-lookup"><span data-stu-id="d4354-103">The size of the file you are attempting to read into a byte array exceeds 4 GB.</span></span> <span data-ttu-id="d4354-104">`My.Computer.FileSystem.ReadAllBytes`Metoda nie może odczytać pliku, który przekracza ten rozmiar.</span><span class="sxs-lookup"><span data-stu-id="d4354-104">The `My.Computer.FileSystem.ReadAllBytes` method cannot read a file that exceeds this size.</span></span>  
  
## <a name="to-correct-this-error"></a><span data-ttu-id="d4354-105">Aby poprawić ten błąd</span><span class="sxs-lookup"><span data-stu-id="d4354-105">To correct this error</span></span>  
  
- <span data-ttu-id="d4354-106">Użyj <xref:System.IO.StreamReader> pliku, aby odczytać plik.</span><span class="sxs-lookup"><span data-stu-id="d4354-106">Use a <xref:System.IO.StreamReader> to read the file.</span></span> <span data-ttu-id="d4354-107">Aby uzyskać więcej informacji, zobacz podstawowe informacje na temat operacji [we/wy pliku .NET Framework i systemu plików (Visual Basic)](../../developing-apps/programming/drives-directories-files/basics-of-net-framework-file-io-and-the-file-system.md).</span><span class="sxs-lookup"><span data-stu-id="d4354-107">For more information, see [Basics of .NET Framework File I/O and the File System (Visual Basic)](../../developing-apps/programming/drives-directories-files/basics-of-net-framework-file-io-and-the-file-system.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="d4354-108">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="d4354-108">See also</span></span>

- <xref:Microsoft.VisualBasic.FileIO.FileSystem.ReadAllBytes%2A>
- <xref:System.IO.StreamReader>
- [<span data-ttu-id="d4354-109">Dostęp do plików za pomocą Visual Basic</span><span class="sxs-lookup"><span data-stu-id="d4354-109">File Access with Visual Basic</span></span>](../../developing-apps/programming/drives-directories-files/file-access.md)
- [<span data-ttu-id="d4354-110">Instrukcje: Odczyt tekstu z plików za pomocą StreamReader</span><span class="sxs-lookup"><span data-stu-id="d4354-110">How to: Read Text from Files with a StreamReader</span></span>](../../developing-apps/programming/drives-directories-files/how-to-read-text-from-files-with-a-streamreader.md)
