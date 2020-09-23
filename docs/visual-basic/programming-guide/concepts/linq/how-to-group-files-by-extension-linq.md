---
title: 'Instrukcje: grupowanie plików według rozszerzenia (LINQ)'
ms.date: 07/20/2015
ms.assetid: 904dc6d7-7162-4655-a7f4-5785d669bc5a
ms.openlocfilehash: 3b1b02283dc65148b8a44952ce39659cc92b483a
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/23/2020
ms.locfileid: "91077309"
---
# <a name="how-to-group-files-by-extension-linq-visual-basic"></a>Instrukcje: grupowanie plików według rozszerzenia (LINQ) (Visual Basic)

Ten przykład pokazuje, jak LINQ może służyć do wykonywania zaawansowanych operacji grupowania i sortowania na listach plików lub folderów. Przedstawiono w nim również sposób wyświetlania stron wyjściowych w oknie konsoli przy użyciu <xref:System.Linq.Enumerable.Skip%2A> <xref:System.Linq.Enumerable.Take%2A> metod i.  
  
## <a name="example"></a>Przykład  

 Poniższe zapytanie pokazuje, jak grupować zawartość określonego drzewa katalogów według rozszerzenia nazwy pliku.  
  
```vb  
Module GroupByExtension  
    Public Sub Main()  
  
        ' Root folder to query, along with all subfolders.  
        Dim startFolder As String = "C:\program files\Microsoft Visual Studio 9.0\VB\"  
  
        ' Used in WriteLine() to skip over startfolder in output lines.  
        Dim rootLength As Integer = startFolder.Length  
  
        'Take a snapshot of the folder contents  
        Dim dir As New System.IO.DirectoryInfo(startFolder)  
        Dim fileList = dir.GetFiles("*.*", System.IO.SearchOption.AllDirectories)  
  
        ' Create the query.  
        Dim queryGroupByExt = From file In fileList _  
                          Group By file.Extension.ToLower() Into fileGroup = Group _  
                          Order By ToLower _  
                          Select fileGroup  
  
        ' Execute the query. By storing the result we can  
        ' page the display with good performance.  
        Dim groupByExtList = queryGroupByExt.ToList()  
  
        ' Display one group at a time. If the number of
        ' entries is greater than the number of lines  
        ' in the console window, then page the output.  
        Dim trimLength = startFolder.Length  
        PageOutput(groupByExtList, trimLength)  
  
    End Sub  
  
    ' Pages console display for large query results. No more than one group per page.  
    ' This sub specifically works with group queries of FileInfo objects  
    ' but can be modified for any type.  
    Sub PageOutput(ByVal groupQuery, ByVal charsToSkip)  
  
        ' "3" = 1 line for extension key + 1 for "Press any key" + 1 for input cursor.  
        Dim numLines As Integer = Console.WindowHeight - 3  
        ' Flag to indicate whether there are more results to display  
        Dim goAgain As Boolean = True  
  
        For Each fg As IEnumerable(Of System.IO.FileInfo) In groupQuery  
            ' Start a new extension at the top of a page.  
            Dim currentLine As Integer = 0  
  
            Do While (currentLine < fg.Count())  
                Console.Clear()  
                Console.WriteLine(fg(0).Extension)  
  
                ' Get the next page of results  
                ' No more than one filename per page  
                Dim resultPage = From file In fg _  
                                Skip currentLine Take numLines  
  
                ' Execute the query. Trim the display output.  
                For Each line In resultPage  
                    Console.WriteLine(vbTab & line.FullName.Substring(charsToSkip))  
                Next  
  
                ' Advance the current position  
                currentLine = numLines + currentLine  
  
                ' Give the user a chance to break out of the loop  
                Console.WriteLine("Press any key for next page or the 'End' key to exit.")  
                Dim key As ConsoleKey = Console.ReadKey().Key  
                If key = ConsoleKey.End Then  
                    goAgain = False  
                    Exit For  
                End If  
            Loop  
        Next  
    End Sub  
End Module  
```  
  
 Dane wyjściowe tego programu mogą być długie, w zależności od szczegółów lokalnego systemu plików i `startFolder` konfiguracji. Aby umożliwić wyświetlanie wszystkich wyników, ten przykład pokazuje, jak przechodzić przez wyniki. Te same techniki można stosować do aplikacji systemu Windows i sieci Web. Zauważ, że ponieważ strona kodowa zawiera elementy w grupie, `For Each` wymagana jest pętla zagnieżdżona. Istnieje również dodatkowa logika służąca do obliczania bieżącej pozycji na liście i umożliwia użytkownikowi zatrzymanie stronicowania i wyjście z programu. W tym konkretnym przypadku kwerenda stronicowania jest uruchamiana względem wyników z pamięci podręcznej z oryginalnego zapytania. W innych kontekstach, takich jak LINQ to SQL, takie buforowanie nie jest wymagane.  
  
## <a name="compile-the-code"></a>Kompiluj kod  

Utwórz projekt aplikacji konsolowej Visual Basic przy użyciu `Imports` instrukcji dla przestrzeni nazw System. LINQ.
  
## <a name="see-also"></a>Zobacz także

- [LINQ to Objects (Visual Basic)](linq-to-objects.md)
- [LINQ i katalogi plików (Visual Basic)](linq-and-file-directories.md)
