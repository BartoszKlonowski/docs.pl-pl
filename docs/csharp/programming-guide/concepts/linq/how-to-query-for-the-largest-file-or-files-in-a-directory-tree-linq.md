---
title: Jak wykonać zapytanie o największy plik lub pliki w drzewie katalogów (LINQ) (C#)
description: Ten przykład w języku C# pokazuje pięć zapytań LINQ związanych z rozmiarem pliku w bajtach. Można je zmodyfikować, aby wykonywać zapytania dotyczące innej właściwości obiektu FileInfo.
ms.date: 07/20/2015
ms.assetid: 20c8a917-0552-4514-b489-0b8b6a4c3b4c
ms.openlocfilehash: 049db9bf104af1593ba9807c307008e8e760da32
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91176256"
---
# <a name="how-to-query-for-the-largest-file-or-files-in-a-directory-tree-linq-c"></a><span data-ttu-id="e5c42-104">Jak wykonać zapytanie o największy plik lub pliki w drzewie katalogów (LINQ) (C#)</span><span class="sxs-lookup"><span data-stu-id="e5c42-104">How to query for the largest file or files in a directory tree (LINQ) (C#)</span></span>

<span data-ttu-id="e5c42-105">Ten przykład pokazuje pięć zapytań związanych z rozmiarem pliku w bajtach:</span><span class="sxs-lookup"><span data-stu-id="e5c42-105">This example shows five queries related to file size in bytes:</span></span>  
  
- <span data-ttu-id="e5c42-106">Jak pobrać rozmiar w bajtach największego pliku.</span><span class="sxs-lookup"><span data-stu-id="e5c42-106">How to retrieve the size in bytes of the largest file.</span></span>  
  
- <span data-ttu-id="e5c42-107">Jak pobrać rozmiar w bajtach najmniejszego pliku.</span><span class="sxs-lookup"><span data-stu-id="e5c42-107">How to retrieve the size in bytes of the smallest file.</span></span>  
  
- <span data-ttu-id="e5c42-108">Jak pobrać <xref:System.IO.FileInfo> największy lub najmniejszy plik z co najmniej jednego folderu w określonym folderze głównym.</span><span class="sxs-lookup"><span data-stu-id="e5c42-108">How to retrieve the <xref:System.IO.FileInfo> object largest or smallest file from one or more folders under a specified root folder.</span></span>  
  
- <span data-ttu-id="e5c42-109">Jak pobrać sekwencję, taką jak 10 największych plików.</span><span class="sxs-lookup"><span data-stu-id="e5c42-109">How to retrieve a sequence such as the 10 largest files.</span></span>  
  
- <span data-ttu-id="e5c42-110">Jak zamówić pliki w grupach na podstawie ich rozmiaru pliku w bajtach, ignorowanie plików mniejszych niż określony rozmiar.</span><span class="sxs-lookup"><span data-stu-id="e5c42-110">How to order files into groups based on their file size in bytes, ignoring files that are less than a specified size.</span></span>  
  
## <a name="example"></a><span data-ttu-id="e5c42-111">Przykład</span><span class="sxs-lookup"><span data-stu-id="e5c42-111">Example</span></span>  

 <span data-ttu-id="e5c42-112">Poniższy przykład zawiera pięć oddzielnych zapytań, które pokazują, jak wykonywać zapytania i grupować pliki, w zależności od rozmiaru pliku w bajtach.</span><span class="sxs-lookup"><span data-stu-id="e5c42-112">The following example contains five separate queries that show how to query and group files, depending on their file size in bytes.</span></span> <span data-ttu-id="e5c42-113">Można łatwo zmodyfikować te przykłady, aby oprzeć zapytania na innej właściwości <xref:System.IO.FileInfo> obiektu.</span><span class="sxs-lookup"><span data-stu-id="e5c42-113">You can easily modify these examples to base the query on some other property of the <xref:System.IO.FileInfo> object.</span></span>  
  
```csharp  
class QueryBySize  
{  
    static void Main(string[] args)  
    {  
        QueryFilesBySize();  
        Console.WriteLine("Press any key to exit");  
        Console.ReadKey();  
    }  
  
    private static void QueryFilesBySize()  
    {  
        string startFolder = @"c:\program files\Microsoft Visual Studio 9.0\";  
  
        // Take a snapshot of the file system.  
        System.IO.DirectoryInfo dir = new System.IO.DirectoryInfo(startFolder);  
  
        // This method assumes that the application has discovery permissions  
        // for all folders under the specified path.  
        IEnumerable<System.IO.FileInfo> fileList = dir.GetFiles("*.*", System.IO.SearchOption.AllDirectories);  
  
        //Return the size of the largest file  
        long maxSize =  
            (from file in fileList  
             let len = GetFileLength(file)  
             select len)  
             .Max();  
  
        Console.WriteLine("The length of the largest file under {0} is {1}",  
            startFolder, maxSize);  
  
        // Return the FileInfo object for the largest file  
        // by sorting and selecting from beginning of list  
        System.IO.FileInfo longestFile =  
            (from file in fileList  
             let len = GetFileLength(file)  
             where len > 0  
             orderby len descending  
             select file)  
            .First();  
  
        Console.WriteLine("The largest file under {0} is {1} with a length of {2} bytes",  
                            startFolder, longestFile.FullName, longestFile.Length);  
  
        //Return the FileInfo of the smallest file  
        System.IO.FileInfo smallestFile =  
            (from file in fileList  
             let len = GetFileLength(file)  
             where len > 0  
             orderby len ascending  
             select file).First();  
  
        Console.WriteLine("The smallest file under {0} is {1} with a length of {2} bytes",  
                            startFolder, smallestFile.FullName, smallestFile.Length);  
  
        //Return the FileInfos for the 10 largest files  
        // queryTenLargest is an IEnumerable<System.IO.FileInfo>  
        var queryTenLargest =  
            (from file in fileList  
             let len = GetFileLength(file)  
             orderby len descending  
             select file).Take(10);  
  
        Console.WriteLine("The 10 largest files under {0} are:", startFolder);  
  
        foreach (var v in queryTenLargest)  
        {  
            Console.WriteLine("{0}: {1} bytes", v.FullName, v.Length);  
        }  
  
        // Group the files according to their size, leaving out  
        // files that are less than 200000 bytes.
        var querySizeGroups =  
            from file in fileList  
            let len = GetFileLength(file)  
            where len > 0  
            group file by (len / 100000) into fileGroup  
            where fileGroup.Key >= 2  
            orderby fileGroup.Key descending  
            select fileGroup;  
  
        foreach (var filegroup in querySizeGroups)  
        {  
            Console.WriteLine(filegroup.Key.ToString() + "00000");  
            foreach (var item in filegroup)  
            {  
                Console.WriteLine("\t{0}: {1}", item.Name, item.Length);  
            }  
        }  
    }  
  
    // This method is used to swallow the possible exception  
    // that can be raised when accessing the FileInfo.Length property.  
    // In this particular case, it is safe to swallow the exception.  
    static long GetFileLength(System.IO.FileInfo fi)  
    {  
        long retval;  
        try  
        {  
            retval = fi.Length;  
        }  
        catch (System.IO.FileNotFoundException)  
        {  
            // If a file is no longer present,  
            // just add zero bytes to the total.  
            retval = 0;  
        }  
        return retval;  
    }  
  
}  
```  
  
 <span data-ttu-id="e5c42-114">Aby zwrócić jeden lub więcej kompletnych <xref:System.IO.FileInfo> obiektów, zapytanie najpierw musi zbadać każdy z nich w źródle danych, a następnie posortować je według wartości właściwości length.</span><span class="sxs-lookup"><span data-stu-id="e5c42-114">To return one or more complete <xref:System.IO.FileInfo> objects, the query first must examine each one in the data source, and then sort them by the value of their Length property.</span></span> <span data-ttu-id="e5c42-115">Następnie może zwrócić jedną lub sekwencję o największą długość.</span><span class="sxs-lookup"><span data-stu-id="e5c42-115">Then it can return the single one or the sequence with the greatest lengths.</span></span> <span data-ttu-id="e5c42-116">Użyj <xref:System.Linq.Enumerable.First%2A> do zwrócenia pierwszego elementu na liście.</span><span class="sxs-lookup"><span data-stu-id="e5c42-116">Use <xref:System.Linq.Enumerable.First%2A> to return the first element in a list.</span></span> <span data-ttu-id="e5c42-117">Użyj, <xref:System.Linq.Enumerable.Take%2A> Aby zwrócić pierwsze n liczbę elementów.</span><span class="sxs-lookup"><span data-stu-id="e5c42-117">Use <xref:System.Linq.Enumerable.Take%2A> to return the first n number of elements.</span></span> <span data-ttu-id="e5c42-118">Określ malejący porządek sortowania, aby umieścić najmniejsze elementy na początku listy.</span><span class="sxs-lookup"><span data-stu-id="e5c42-118">Specify a descending sort order to put the smallest elements at the start of the list.</span></span>  
  
 <span data-ttu-id="e5c42-119">Zapytanie wywołuje oddzielną metodę w celu uzyskania rozmiaru pliku w bajtach, aby można było wykorzystać możliwy wyjątek, który zostanie wywołany w przypadku, gdy plik został usunięty z innego wątku w czasie, ponieważ <xref:System.IO.FileInfo> obiekt został utworzony w wywołaniu `GetFiles` .</span><span class="sxs-lookup"><span data-stu-id="e5c42-119">The query calls out to a separate method to obtain the file size in bytes in order to consume the possible exception that will be raised in the case where a file was deleted on another thread in the time period since the <xref:System.IO.FileInfo> object was created in the call to `GetFiles`.</span></span> <span data-ttu-id="e5c42-120">Nawet za pośrednictwem <xref:System.IO.FileInfo> obiektu został już utworzony, wyjątek może wystąpić, ponieważ <xref:System.IO.FileInfo> obiekt podejmie próbę odświeżenia jego <xref:System.IO.FileInfo.Length%2A> właściwości przy użyciu najbardziej aktualnego rozmiaru w bajtach przy pierwszym dostępie do tej właściwości.</span><span class="sxs-lookup"><span data-stu-id="e5c42-120">Even through the <xref:System.IO.FileInfo> object has already been created, the exception can occur because a <xref:System.IO.FileInfo> object will try to refresh its <xref:System.IO.FileInfo.Length%2A> property by using the most current size in bytes the first time the property is accessed.</span></span> <span data-ttu-id="e5c42-121">Przez umieszczenie tej operacji w bloku try-catch poza zapytaniem przestrzegamy zasad unikania operacji w zapytaniach, które mogą spowodować skutki uboczne.</span><span class="sxs-lookup"><span data-stu-id="e5c42-121">By putting this operation in a try-catch block outside the query, we follow the rule of avoiding operations in queries that can cause side-effects.</span></span> <span data-ttu-id="e5c42-122">Ogólnie rzecz biorąc należy zachować szczególną ostrożność podczas zużywania wyjątków, aby upewnić się, że aplikacja nie jest pozostawiona w nieznanym stanie.</span><span class="sxs-lookup"><span data-stu-id="e5c42-122">In general, great care must be taken when consuming exceptions, to make sure that an application is not left in an unknown state.</span></span>  
  
## <a name="compiling-the-code"></a><span data-ttu-id="e5c42-123">Kompilowanie kodu</span><span class="sxs-lookup"><span data-stu-id="e5c42-123">Compiling the Code</span></span>  

<span data-ttu-id="e5c42-124">Utwórz projekt aplikacji konsolowej w języku C# z `using` dyrektywami dotyczącymi przestrzeni nazw System. LINQ i system.IO.</span><span class="sxs-lookup"><span data-stu-id="e5c42-124">Create a C# console application project, with `using` directives for the System.Linq and System.IO namespaces.</span></span>

## <a name="see-also"></a><span data-ttu-id="e5c42-125">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="e5c42-125">See also</span></span>

- [<span data-ttu-id="e5c42-126">LINQ to Objects (C#)</span><span class="sxs-lookup"><span data-stu-id="e5c42-126">LINQ to Objects (C#)</span></span>](./linq-to-objects.md)
- [<span data-ttu-id="e5c42-127">LINQ i katalogi plików (C#)</span><span class="sxs-lookup"><span data-stu-id="e5c42-127">LINQ and File Directories (C#)</span></span>](./linq-and-file-directories.md)
