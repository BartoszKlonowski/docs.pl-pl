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
# <a name="how-to-query-for-the-largest-file-or-files-in-a-directory-tree-linq-c"></a>Jak wykonać zapytanie o największy plik lub pliki w drzewie katalogów (LINQ) (C#)

Ten przykład pokazuje pięć zapytań związanych z rozmiarem pliku w bajtach:  
  
- Jak pobrać rozmiar w bajtach największego pliku.  
  
- Jak pobrać rozmiar w bajtach najmniejszego pliku.  
  
- Jak pobrać <xref:System.IO.FileInfo> największy lub najmniejszy plik z co najmniej jednego folderu w określonym folderze głównym.  
  
- Jak pobrać sekwencję, taką jak 10 największych plików.  
  
- Jak zamówić pliki w grupach na podstawie ich rozmiaru pliku w bajtach, ignorowanie plików mniejszych niż określony rozmiar.  
  
## <a name="example"></a>Przykład  

 Poniższy przykład zawiera pięć oddzielnych zapytań, które pokazują, jak wykonywać zapytania i grupować pliki, w zależności od rozmiaru pliku w bajtach. Można łatwo zmodyfikować te przykłady, aby oprzeć zapytania na innej właściwości <xref:System.IO.FileInfo> obiektu.  
  
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
  
 Aby zwrócić jeden lub więcej kompletnych <xref:System.IO.FileInfo> obiektów, zapytanie najpierw musi zbadać każdy z nich w źródle danych, a następnie posortować je według wartości właściwości length. Następnie może zwrócić jedną lub sekwencję o największą długość. Użyj <xref:System.Linq.Enumerable.First%2A> do zwrócenia pierwszego elementu na liście. Użyj, <xref:System.Linq.Enumerable.Take%2A> Aby zwrócić pierwsze n liczbę elementów. Określ malejący porządek sortowania, aby umieścić najmniejsze elementy na początku listy.  
  
 Zapytanie wywołuje oddzielną metodę w celu uzyskania rozmiaru pliku w bajtach, aby można było wykorzystać możliwy wyjątek, który zostanie wywołany w przypadku, gdy plik został usunięty z innego wątku w czasie, ponieważ <xref:System.IO.FileInfo> obiekt został utworzony w wywołaniu `GetFiles` . Nawet za pośrednictwem <xref:System.IO.FileInfo> obiektu został już utworzony, wyjątek może wystąpić, ponieważ <xref:System.IO.FileInfo> obiekt podejmie próbę odświeżenia jego <xref:System.IO.FileInfo.Length%2A> właściwości przy użyciu najbardziej aktualnego rozmiaru w bajtach przy pierwszym dostępie do tej właściwości. Przez umieszczenie tej operacji w bloku try-catch poza zapytaniem przestrzegamy zasad unikania operacji w zapytaniach, które mogą spowodować skutki uboczne. Ogólnie rzecz biorąc należy zachować szczególną ostrożność podczas zużywania wyjątków, aby upewnić się, że aplikacja nie jest pozostawiona w nieznanym stanie.  
  
## <a name="compiling-the-code"></a>Kompilowanie kodu  

Utwórz projekt aplikacji konsolowej w języku C# z `using` dyrektywami dotyczącymi przestrzeni nazw System. LINQ i system.IO.

## <a name="see-also"></a>Zobacz też

- [LINQ to Objects (C#)](./linq-to-objects.md)
- [LINQ i katalogi plików (C#)](./linq-and-file-directories.md)
