---
title: Jak napisać dane obiektu do pliku XML (C#)
description: Ten przykład w języku C# zapisuje obiekt z klasy do pliku XML przy użyciu klasy XmlSerializer. Dowiedz się, jak skompilować kod.
ms.date: 07/20/2015
ms.assetid: 7681eb98-703d-4005-a369-26a7bca0f894
ms.openlocfilehash: 776ade1752adf15d6acce07d38120de8481a233d
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91178713"
---
# <a name="how-to-write-object-data-to-an-xml-file-c"></a>Jak napisać dane obiektu do pliku XML (C#)

Ten przykład zapisuje obiekt z klasy do pliku XML przy użyciu <xref:System.Xml.Serialization.XmlSerializer> klasy.  
  
## <a name="example"></a>Przykład  
  
```csharp  
public class XMLWrite  
{  
  
   static void Main(string[] args)  
    {  
        WriteXML();  
    }  
  
    public class Book  
    {  
        public String title;
    }  
  
    public static void WriteXML()  
    {  
        Book overview = new Book();  
        overview.title = "Serialization Overview";  
        System.Xml.Serialization.XmlSerializer writer =
            new System.Xml.Serialization.XmlSerializer(typeof(Book));  
  
        var path = Environment.GetFolderPath(Environment.SpecialFolder.MyDocuments) + "//SerializationOverview.xml";  
        System.IO.FileStream file = System.IO.File.Create(path);  
  
        writer.Serialize(file, overview);  
        file.Close();  
    }  
}  
```  
  
## <a name="compiling-the-code"></a>Kompilowanie kodu  

 Serializacja klasy musi mieć Konstruktor publiczny bez parametrów.  
  
## <a name="robust-programming"></a>Niezawodne programowanie  

 Następujące warunki mogą spowodować wyjątek:  
  
- Serializowana Klasa nie ma publicznego konstruktora bez parametrów.  
  
- Plik istnieje i jest tylko do odczytu ( <xref:System.IO.IOException> ).  
  
- Ścieżka jest za długa ( <xref:System.IO.PathTooLongException> ).  
  
- Dysk jest pełny ( <xref:System.IO.IOException> ).  
  
## <a name="net-security"></a>Zabezpieczenia platformy .NET  

 Ten przykład tworzy nowy plik, jeśli plik jeszcze nie istnieje. Jeśli aplikacja musi utworzyć plik, aplikacja musi `Create` mieć dostęp do tego folderu. Jeśli plik już istnieje, aplikacja wymaga tylko `Write` dostępu, ale ma mniejsze uprawnienia. Jeśli to możliwe, bezpieczniejsze jest tworzenie pliku podczas wdrażania i udzielanie `Read` dostępu do pojedynczego pliku, a nie `Create` dostęp do folderu.  
  
## <a name="see-also"></a>Zobacz też

- <xref:System.IO.StreamWriter>
- [Jak odczytywać dane obiektów z pliku XML (C#)](./how-to-read-object-data-from-an-xml-file.md)
- [Serializacja (C#)](./index.md)
