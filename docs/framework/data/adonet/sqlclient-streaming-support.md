---
title: Obsługa przesyłania strumieniowego SqlClient
ms.date: 03/30/2017
ms.assetid: c449365b-470b-4edb-9d61-8353149f5531
ms.openlocfilehash: a396e3e172c63b0b71b085d4694184c42cc42f3e
ms.sourcegitcommit: 97405ed212f69b0a32faa66a5d5fae7e76628b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/01/2020
ms.locfileid: "91609248"
---
# <a name="sqlclient-streaming-support"></a><span data-ttu-id="9772b-102">Obsługa przesyłania strumieniowego SqlClient</span><span class="sxs-lookup"><span data-stu-id="9772b-102">SqlClient Streaming Support</span></span>

<span data-ttu-id="9772b-103">Obsługa przesyłania strumieniowego między SQL Server i aplikacją (Nowość w .NET Framework 4,5) obsługuje dane bez struktury na serwerze (dokumenty, obrazy i pliki multimedialne).</span><span class="sxs-lookup"><span data-stu-id="9772b-103">Streaming support between SQL Server and an application (new in .NET Framework 4.5) supports unstructured data on the server (documents, images, and media files).</span></span> <span data-ttu-id="9772b-104">Baza danych SQL Server może przechowywać duże obiekty binarne (BLOB), ale pobieranie obiektów BLOB może korzystać z dużej ilości pamięci.</span><span class="sxs-lookup"><span data-stu-id="9772b-104">A SQL Server database can store binary large objects (BLOBs), but retrieving BLOBS can use a lot of memory.</span></span>

<span data-ttu-id="9772b-105">Obsługa przesyłania strumieniowego do i z SQL Server upraszcza pisanie aplikacji, które przesyła strumieniowo dane, bez konieczności całkowitego ładowania danych do pamięci, co spowodowało mniejsze wyjątki przepełnienia pamięci.</span><span class="sxs-lookup"><span data-stu-id="9772b-105">Streaming support to and from SQL Server simplifies writing applications that stream data, without having to fully load the data into memory, resulting in fewer memory overflow exceptions.</span></span>

<span data-ttu-id="9772b-106">Obsługa przesyłania strumieniowego włącza również aplikacje warstwy środkowej do lepszego skalowania, szczególnie w scenariuszach, w których obiekty biznesowe łączą się z usługą SQL Azure w celu wysyłania i pobierania dużych obiektów blob oraz manipulowania nimi.</span><span class="sxs-lookup"><span data-stu-id="9772b-106">Streaming support will also enable middle-tier applications to scale better, especially in scenarios where business objects connect to SQL Azure in order to send, retrieve, and manipulate large BLOBs.</span></span>

> [!WARNING]
> <span data-ttu-id="9772b-107">Wywołania asynchroniczne nie są obsługiwane, jeśli aplikacja używa również `Context Connection` słowa kluczowego parametrów połączenia.</span><span class="sxs-lookup"><span data-stu-id="9772b-107">Asynchronous calls are not supported if an application also uses the `Context Connection` connection string keyword.</span></span>
>
> <span data-ttu-id="9772b-108">Członkowie dodani do obsługi przesyłania strumieniowego są używani do pobierania danych z zapytań i przekazywania parametrów do zapytań i procedur składowanych.</span><span class="sxs-lookup"><span data-stu-id="9772b-108">The members added to support streaming are used to retrieve data from queries and to pass parameters to queries and stored procedures.</span></span> <span data-ttu-id="9772b-109">Funkcja przesyłania strumieniowego obejmuje podstawowe scenariusze przetwarzania OLTP i danych oraz ma zastosowanie do środowisk migracji danych lokalnych i przechowywanych lokalnie.</span><span class="sxs-lookup"><span data-stu-id="9772b-109">The streaming feature addresses basic OLTP and data migration scenarios and is applicable to on-premises and off-premises data migrations environments.</span></span>

## <a name="streaming-support-from-sql-server"></a><span data-ttu-id="9772b-110">Obsługa przesyłania strumieniowego z SQL Server</span><span class="sxs-lookup"><span data-stu-id="9772b-110">Streaming Support from SQL Server</span></span>

<span data-ttu-id="9772b-111">Obsługa przesyłania strumieniowego z SQL Server wprowadza nowe funkcje w <xref:System.Data.Common.DbDataReader> i w <xref:System.Data.SqlClient.SqlDataReader> klasach, które umożliwiają uzyskiwanie <xref:System.IO.Stream> , <xref:System.Xml.XmlReader> , i <xref:System.IO.TextReader> reagowanie na nie.</span><span class="sxs-lookup"><span data-stu-id="9772b-111">Streaming support from SQL Server introduces new functionality in the <xref:System.Data.Common.DbDataReader> and in the <xref:System.Data.SqlClient.SqlDataReader> classes in order to get <xref:System.IO.Stream>, <xref:System.Xml.XmlReader>, and <xref:System.IO.TextReader> objects and react to them.</span></span> <span data-ttu-id="9772b-112">Te klasy są używane do pobierania danych z zapytań.</span><span class="sxs-lookup"><span data-stu-id="9772b-112">These classes are used to retrieve data from queries.</span></span> <span data-ttu-id="9772b-113">W związku z tym obsługa przesyłania strumieniowego SQL Server rozwiązuje scenariusze OLTP i ma zastosowanie do środowisk lokalnych i terenowych.</span><span class="sxs-lookup"><span data-stu-id="9772b-113">As a result, Streaming support from SQL Server addresses OLTP scenarios and applies to on-premises and off-premises environments.</span></span>

<span data-ttu-id="9772b-114">Dodano następujące składowe w celu <xref:System.Data.SqlClient.SqlDataReader> włączenia obsługi przesyłania strumieniowego z SQL Server:</span><span class="sxs-lookup"><span data-stu-id="9772b-114">The following members were added to <xref:System.Data.SqlClient.SqlDataReader> to enable streaming support from SQL Server:</span></span>

1. <xref:System.Data.SqlClient.SqlDataReader.IsDBNullAsync%2A>

2. <xref:System.Data.SqlClient.SqlDataReader.GetFieldValue%2A?displayProperty=nameWithType>

3. <xref:System.Data.SqlClient.SqlDataReader.GetFieldValueAsync%2A>

4. <xref:System.Data.SqlClient.SqlDataReader.GetStream%2A>

5. <xref:System.Data.SqlClient.SqlDataReader.GetTextReader%2A>

6. <xref:System.Data.SqlClient.SqlDataReader.GetXmlReader%2A>

<span data-ttu-id="9772b-115">Dodano następujące składowe w celu <xref:System.Data.Common.DbDataReader> włączenia obsługi przesyłania strumieniowego z SQL Server:</span><span class="sxs-lookup"><span data-stu-id="9772b-115">The following members were added to <xref:System.Data.Common.DbDataReader> to enable streaming support from SQL Server:</span></span>

1. <xref:System.Data.Common.DbDataReader.GetFieldValue%2A>

2. <xref:System.Data.Common.DbDataReader.GetStream%2A>

3. <xref:System.Data.Common.DbDataReader.GetTextReader%2A>

## <a name="streaming-support-to-sql-server"></a><span data-ttu-id="9772b-116">Obsługa przesyłania strumieniowego do SQL Server</span><span class="sxs-lookup"><span data-stu-id="9772b-116">Streaming Support to SQL Server</span></span>

<span data-ttu-id="9772b-117">Obsługa przesyłania strumieniowego do SQL Server wprowadza nowe funkcje w <xref:System.Data.SqlClient.SqlParameter> klasie, dzięki czemu można akceptować i reagować na <xref:System.Xml.XmlReader> <xref:System.IO.Stream> obiekty, i <xref:System.IO.TextReader> .</span><span class="sxs-lookup"><span data-stu-id="9772b-117">Streaming support to SQL Server introduces new functionality in the <xref:System.Data.SqlClient.SqlParameter> class so it can accept and react to <xref:System.Xml.XmlReader>, <xref:System.IO.Stream>, and <xref:System.IO.TextReader> objects.</span></span> <span data-ttu-id="9772b-118"><xref:System.Data.SqlClient.SqlParameter> służy do przekazywania parametrów do zapytań i procedur składowanych.</span><span class="sxs-lookup"><span data-stu-id="9772b-118"><xref:System.Data.SqlClient.SqlParameter> is used to pass parameters to queries and stored procedures.</span></span>

<span data-ttu-id="9772b-119">Usuwanie <xref:System.Data.SqlClient.SqlCommand> obiektu lub wywoływanie <xref:System.Data.SqlClient.SqlCommand.Cancel%2A> musi anulować wszystkie operacje przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="9772b-119">Disposing a <xref:System.Data.SqlClient.SqlCommand> object or calling <xref:System.Data.SqlClient.SqlCommand.Cancel%2A> must cancel any streaming operation.</span></span> <span data-ttu-id="9772b-120">Jeśli aplikacja zostanie wysłana <xref:System.Threading.CancellationToken> , anulowanie nie jest gwarantowane.</span><span class="sxs-lookup"><span data-stu-id="9772b-120">If an application sends <xref:System.Threading.CancellationToken>, cancellation is not guaranteed.</span></span>

<span data-ttu-id="9772b-121">Następujące <xref:System.Data.SqlClient.SqlParameter.SqlDbType%2A> typy zostaną zaakceptowane <xref:System.Data.SqlClient.SqlParameter.Value%2A> z <xref:System.IO.Stream> :</span><span class="sxs-lookup"><span data-stu-id="9772b-121">The following <xref:System.Data.SqlClient.SqlParameter.SqlDbType%2A> types will accept a <xref:System.Data.SqlClient.SqlParameter.Value%2A> of <xref:System.IO.Stream>:</span></span>

- <span data-ttu-id="9772b-122">**Binarne**</span><span class="sxs-lookup"><span data-stu-id="9772b-122">**Binary**</span></span>

- <span data-ttu-id="9772b-123">**Liczby**</span><span class="sxs-lookup"><span data-stu-id="9772b-123">**VarBinary**</span></span>

<span data-ttu-id="9772b-124">Następujące <xref:System.Data.SqlClient.SqlParameter.SqlDbType%2A> typy zostaną zaakceptowane <xref:System.Data.SqlClient.SqlParameter.Value%2A> z <xref:System.IO.TextReader> :</span><span class="sxs-lookup"><span data-stu-id="9772b-124">The following <xref:System.Data.SqlClient.SqlParameter.SqlDbType%2A> types will accept a <xref:System.Data.SqlClient.SqlParameter.Value%2A> of <xref:System.IO.TextReader>:</span></span>

- <span data-ttu-id="9772b-125">**Delikatn**</span><span class="sxs-lookup"><span data-stu-id="9772b-125">**Char**</span></span>

- <span data-ttu-id="9772b-126">**NChar**</span><span class="sxs-lookup"><span data-stu-id="9772b-126">**NChar**</span></span>

- <span data-ttu-id="9772b-127">**NVarChar**</span><span class="sxs-lookup"><span data-stu-id="9772b-127">**NVarChar**</span></span>

- <span data-ttu-id="9772b-128">**Dokument**</span><span class="sxs-lookup"><span data-stu-id="9772b-128">**Xml**</span></span>

<span data-ttu-id="9772b-129">Typ **XML** <xref:System.Data.SqlClient.SqlParameter.SqlDbType%2A> zostanie zaakceptowany <xref:System.Data.SqlClient.SqlParameter.Value%2A> przez <xref:System.Xml.XmlReader> .</span><span class="sxs-lookup"><span data-stu-id="9772b-129">The **Xml**<xref:System.Data.SqlClient.SqlParameter.SqlDbType%2A> type will accept a <xref:System.Data.SqlClient.SqlParameter.Value%2A> of <xref:System.Xml.XmlReader>.</span></span>

<span data-ttu-id="9772b-130"><xref:System.Data.SqlClient.SqlParameter.SqlValue%2A> można akceptować wartości typu <xref:System.Xml.XmlReader> , <xref:System.IO.TextReader> , i <xref:System.IO.Stream> .</span><span class="sxs-lookup"><span data-stu-id="9772b-130"><xref:System.Data.SqlClient.SqlParameter.SqlValue%2A> can accept values of type <xref:System.Xml.XmlReader>, <xref:System.IO.TextReader>, and <xref:System.IO.Stream>.</span></span>

<span data-ttu-id="9772b-131"><xref:System.Xml.XmlReader>Obiekt, <xref:System.IO.TextReader> , i <xref:System.IO.Stream> zostanie przekazany do wartości zdefiniowanej przez <xref:System.Data.SqlClient.SqlParameter.Size%2A> .</span><span class="sxs-lookup"><span data-stu-id="9772b-131">The <xref:System.Xml.XmlReader>, <xref:System.IO.TextReader>, and <xref:System.IO.Stream> object will be transferred up to the value defined by the <xref:System.Data.SqlClient.SqlParameter.Size%2A>.</span></span>

## <a name="sample----streaming-from-sql-server"></a><span data-ttu-id="9772b-132">Przykład — przesyłanie strumieniowe z SQL Server</span><span class="sxs-lookup"><span data-stu-id="9772b-132">Sample -- Streaming from SQL Server</span></span>

<span data-ttu-id="9772b-133">Użyj następującego języka Transact-SQL, aby utworzyć przykładową bazę danych:</span><span class="sxs-lookup"><span data-stu-id="9772b-133">Use the following Transact-SQL to create the sample database:</span></span>

```sql
CREATE DATABASE [Demo]
GO
USE [Demo]
GO
CREATE TABLE [Streams] (
[id] INT PRIMARY KEY IDENTITY(1, 1),
[textdata] NVARCHAR(MAX),
[bindata] VARBINARY(MAX),
[xmldata] XML)
GO
INSERT INTO [Streams] (textdata, bindata, xmldata) VALUES (N'This is a test', 0x48656C6C6F, N'<test>value</test>')
INSERT INTO [Streams] (textdata, bindata, xmldata) VALUES (N'Hello, World!', 0x54657374696E67, N'<test>value2</test>')
INSERT INTO [Streams] (textdata, bindata, xmldata) VALUES (N'Another row', 0x666F6F626172, N'<fff>bbb</fff><fff>bbc</fff>')
GO
```

<span data-ttu-id="9772b-134">W przykładzie pokazano, jak wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9772b-134">The sample shows how to do the following:</span></span>

- <span data-ttu-id="9772b-135">Należy unikać blokowania wątku interfejsu użytkownika, zapewniając asynchroniczny sposób pobierania dużych plików.</span><span class="sxs-lookup"><span data-stu-id="9772b-135">Avoid blocking a user-interface thread by providing an asynchronous way to retrieve large files.</span></span>

- <span data-ttu-id="9772b-136">Prześlij duży plik tekstowy z SQL Server w .NET Framework 4,5.</span><span class="sxs-lookup"><span data-stu-id="9772b-136">Transfer a large text file from SQL Server in .NET Framework 4.5.</span></span>

- <span data-ttu-id="9772b-137">Transfer dużego pliku XML z SQL Server w .NET Framework 4,5.</span><span class="sxs-lookup"><span data-stu-id="9772b-137">Transfer a large XML file from SQL Server in .NET Framework 4.5.</span></span>

- <span data-ttu-id="9772b-138">Pobierz dane z SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9772b-138">Retrieve data from SQL Server.</span></span>

- <span data-ttu-id="9772b-139">Transfer dużych plików (BLOB) z jednej bazy danych SQL Server do innej bez uruchamiania pamięci.</span><span class="sxs-lookup"><span data-stu-id="9772b-139">Transfer large files (BLOBs) from one SQL Server database to another without running out of memory.</span></span>

```csharp
using System;
using System.Data;
using System.Data.SqlClient;
using System.IO;
using System.Threading.Tasks;
using System.Xml;

namespace StreamingFromServer {
   class Program {
      // Replace the connection string if needed, for instance to connect to SQL Express: @"Server=(local)\SQLEXPRESS;Database=Demo;Integrated Security=true"
      private const string connectionString = @"Server=(localdb)\V11.0;Database=Demo";

      static void Main(string[] args) {
         CopyBinaryValueToFile().Wait();
         PrintTextValues().Wait();
         PrintXmlValues().Wait();
         PrintXmlValuesViaNVarChar().Wait();

         Console.WriteLine("Done");
      }

      // Application retrieving a large BLOB from SQL Server in .NET 4.5 using the new asynchronous capability
      private static async Task CopyBinaryValueToFile() {
         string filePath = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.MyDocuments), "binarydata.bin");

         using (SqlConnection connection = new SqlConnection(connectionString)) {
            await connection.OpenAsync();
            using (SqlCommand command = new SqlCommand("SELECT [bindata] FROM [Streams] WHERE [id]=@id", connection)) {
               command.Parameters.AddWithValue("id", 1);

               // The reader needs to be executed with the SequentialAccess behavior to enable network streaming
               // Otherwise ReadAsync will buffer the entire BLOB into memory which can cause scalability issues or even OutOfMemoryExceptions
               using (SqlDataReader reader = await command.ExecuteReaderAsync(CommandBehavior.SequentialAccess)) {
                  if (await reader.ReadAsync()) {
                     if (!(await reader.IsDBNullAsync(0))) {
                        using (FileStream file = new FileStream(filePath, FileMode.Create, FileAccess.Write)) {
                           using (Stream data = reader.GetStream(0)) {

                              // Asynchronously copy the stream from the server to the file we just created
                              await data.CopyToAsync(file);
                           }
                        }
                     }
                  }
               }
            }
         }
      }

      // Application transferring a large Text File from SQL Server in .NET 4.5
      private static async Task PrintTextValues() {
         using (SqlConnection connection = new SqlConnection(connectionString)) {
            await connection.OpenAsync();
            using (SqlCommand command = new SqlCommand("SELECT [id], [textdata] FROM [Streams]", connection)) {

               // The reader needs to be executed with the SequentialAccess behavior to enable network streaming
               // Otherwise ReadAsync will buffer the entire text document into memory which can cause scalability issues or even OutOfMemoryExceptions
               using (SqlDataReader reader = await command.ExecuteReaderAsync(CommandBehavior.SequentialAccess)) {
                  while (await reader.ReadAsync()) {
                     Console.Write("{0}: ", reader.GetInt32(0));

                     if (await reader.IsDBNullAsync(1)) {
                        Console.Write("(NULL)");
                     }
                     else {
                        char[] buffer = new char[4096];
                        int charsRead = 0;
                        using (TextReader data = reader.GetTextReader(1)) {
                           do {
                              // Grab each chunk of text and write it to the console
                              // If you are writing to a TextWriter you should use WriteAsync or WriteLineAsync
                              charsRead = await data.ReadAsync(buffer, 0, buffer.Length);
                              Console.Write(buffer, 0, charsRead);
                           } while (charsRead > 0);
                        }
                     }

                     Console.WriteLine();
                  }
               }
            }
         }
      }

      // Application transferring a large Xml Document from SQL Server in .NET 4.5
      private static async Task PrintXmlValues() {
         using (SqlConnection connection = new SqlConnection(connectionString)) {
            await connection.OpenAsync();
            using (SqlCommand command = new SqlCommand("SELECT [id], [xmldata] FROM [Streams]", connection)) {

               // The reader needs to be executed with the SequentialAccess behavior to enable network streaming
               // Otherwise ReadAsync will buffer the entire Xml Document into memory which can cause scalability issues or even OutOfMemoryExceptions
               using (SqlDataReader reader = await command.ExecuteReaderAsync(CommandBehavior.SequentialAccess)) {
                  while (await reader.ReadAsync()) {
                     Console.WriteLine("{0}: ", reader.GetInt32(0));

                     if (await reader.IsDBNullAsync(1)) {
                        Console.WriteLine("\t(NULL)");
                     }
                     else {
                        using (XmlReader xmlReader = reader.GetXmlReader(1)) {
                           int depth = 1;
                           // NOTE: The XmlReader returned by GetXmlReader does NOT support async operations
                           // See the example below (PrintXmlValuesViaNVarChar) for how to get an XmlReader with asynchronous capabilities
                           while (xmlReader.Read()) {
                              switch (xmlReader.NodeType) {
                                 case XmlNodeType.Element:
                                    Console.WriteLine("{0}<{1}>", new string('\t', depth), xmlReader.Name);
                                    depth++;
                                    break;
                                 case XmlNodeType.Text:
                                    Console.WriteLine("{0}{1}", new string('\t', depth), xmlReader.Value);
                                    break;
                                 case XmlNodeType.EndElement:
                                    depth--;
                                    Console.WriteLine("{0}</{1}>", new string('\t', depth), xmlReader.Name);
                                    break;
                              }
                           }
                        }
                     }
                  }
               }
            }
         }
      }

      // Application transferring a large Xml Document from SQL Server in .NET 4.5
      // This goes via NVarChar and TextReader to enable asynchronous reading
      private static async Task PrintXmlValuesViaNVarChar() {
         XmlReaderSettings xmlSettings = new XmlReaderSettings() {
            // Async must be explicitly enabled in the XmlReaderSettings otherwise the XmlReader will throw exceptions when async methods are called
            Async = true,
            // Since we will immediately wrap the TextReader we are creating in an XmlReader, we will permit the XmlReader to take care of closing\disposing it
            CloseInput = true,
            // If the Xml you are reading is not a valid document (as per <https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/6bts1x50(v=vs.100)>) you will need to set the conformance level to Fragment
            ConformanceLevel = ConformanceLevel.Fragment
         };

         using (SqlConnection connection = new SqlConnection(connectionString)) {
            await connection.OpenAsync();

            // Cast the XML into NVarChar to enable GetTextReader - trying to use GetTextReader on an XML type will throw an exception
            using (SqlCommand command = new SqlCommand("SELECT [id], CAST([xmldata] AS NVARCHAR(MAX)) FROM [Streams]", connection)) {

               // The reader needs to be executed with the SequentialAccess behavior to enable network streaming
               // Otherwise ReadAsync will buffer the entire Xml Document into memory which can cause scalability issues or even OutOfMemoryExceptions
               using (SqlDataReader reader = await command.ExecuteReaderAsync(CommandBehavior.SequentialAccess)) {
                  while (await reader.ReadAsync()) {
                     Console.WriteLine("{0}:", reader.GetInt32(0));

                     if (await reader.IsDBNullAsync(1)) {
                        Console.WriteLine("\t(NULL)");
                     }
                     else {
                        // Grab the row as a TextReader, then create an XmlReader on top of it
                        // We are not keeping a reference to the TextReader since the XmlReader is created with the "CloseInput" setting (so it will close the TextReader when needed)
                        using (XmlReader xmlReader = XmlReader.Create(reader.GetTextReader(1), xmlSettings)) {
                           int depth = 1;
                           // The XmlReader above now supports asynchronous operations, so we can use ReadAsync here
                           while (await xmlReader.ReadAsync()) {
                              switch (xmlReader.NodeType) {
                                 case XmlNodeType.Element:
                                    Console.WriteLine("{0}<{1}>", new string('\t', depth), xmlReader.Name);
                                    depth++;
                                    break;
                                 case XmlNodeType.Text:
                                    // Depending on what your data looks like, you should either use Value or GetValueAsync
                                    // Value has less overhead (since it doesn't create a Task), but it may also block if additional data is required
                                    Console.WriteLine("{0}{1}", new string('\t', depth), await xmlReader.GetValueAsync());
                                    break;
                                 case XmlNodeType.EndElement:
                                    depth--;
                                    Console.WriteLine("{0}</{1}>", new string('\t', depth), xmlReader.Name);
                                    break;
                              }
                           }
                        }
                     }
                  }
               }
            }
         }
      }
   }
}
```

## <a name="sample----streaming-to-sql-server"></a><span data-ttu-id="9772b-140">Przykład — przesyłanie strumieniowe do SQL Server</span><span class="sxs-lookup"><span data-stu-id="9772b-140">Sample -- Streaming to SQL Server</span></span>

<span data-ttu-id="9772b-141">Użyj następującego języka Transact-SQL, aby utworzyć przykładową bazę danych:</span><span class="sxs-lookup"><span data-stu-id="9772b-141">Use the following Transact-SQL to create the sample database:</span></span>

```sql
CREATE DATABASE [Demo2]
GO
USE [Demo2]
GO
CREATE TABLE [BinaryStreams] (
[id] INT PRIMARY KEY IDENTITY(1, 1),
[bindata] VARBINARY(MAX))
GO
CREATE TABLE [TextStreams] (
[id] INT PRIMARY KEY IDENTITY(1, 1),
[textdata] NVARCHAR(MAX))
GO
CREATE TABLE [BinaryStreamsCopy] (
[id] INT PRIMARY KEY IDENTITY(1, 1),
[bindata] VARBINARY(MAX))
GO
```

<span data-ttu-id="9772b-142">W przykładzie pokazano, jak wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9772b-142">The sample shows how to do the following:</span></span>

- <span data-ttu-id="9772b-143">Transferowanie dużego obiektu BLOB do SQL Server w .NET Framework 4,5.</span><span class="sxs-lookup"><span data-stu-id="9772b-143">Transferring a large BLOB to SQL Server in .NET Framework 4.5.</span></span>

- <span data-ttu-id="9772b-144">Transferowanie dużych plików tekstowych do SQL Server w .NET Framework 4,5.</span><span class="sxs-lookup"><span data-stu-id="9772b-144">Transferring a large text file to SQL Server in .NET Framework 4.5.</span></span>

- <span data-ttu-id="9772b-145">Użycie nowej funkcji asynchronicznej do transferu dużego obiektu BLOB.</span><span class="sxs-lookup"><span data-stu-id="9772b-145">Using the new asynchronous feature to transfer a large BLOB.</span></span>

- <span data-ttu-id="9772b-146">Za pomocą nowej funkcji asynchronicznej i słowa kluczowego await do transferu dużego obiektu BLOB.</span><span class="sxs-lookup"><span data-stu-id="9772b-146">Using the new asynchronous feature and the await keyword to transfer a large BLOB.</span></span>

- <span data-ttu-id="9772b-147">Anulowanie transferu dużego obiektu BLOB.</span><span class="sxs-lookup"><span data-stu-id="9772b-147">Cancelling the transfer of a large BLOB.</span></span>

- <span data-ttu-id="9772b-148">Przesyłanie strumieniowe między SQL Server przy użyciu nowej funkcji asynchronicznej.</span><span class="sxs-lookup"><span data-stu-id="9772b-148">Streaming from one SQL Server to another using the new asynchronous feature.</span></span>

```csharp
using System;
using System.Data;
using System.Data.SqlClient;
using System.IO;
using System.Threading;
using System.Threading.Tasks;

namespace StreamingToServer {
   class Program {
      // Replace the connection string if needed, for instance to connect to SQL Express: @"Server=(local)\SQLEXPRESS;Database=Demo2;Integrated Security=true"
      private const string connectionString = @"Server=(localdb)\V11.0;Database=Demo2";

      static void Main(string[] args) {
         CreateDemoFiles();

         StreamBLOBToServer().Wait();
         StreamTextToServer().Wait();

         // Create a CancellationTokenSource that will be cancelled after 100ms
         // Typically this token source will be cancelled by a user request (e.g. a Cancel button)
         CancellationTokenSource tokenSource = new CancellationTokenSource();
         tokenSource.CancelAfter(100);
         try {
            CancelBLOBStream(tokenSource.Token).Wait();
         }
         catch (AggregateException ex) {
            // Cancelling an async operation will throw an exception
            // Since we are using the Task's Wait method, this exception will be wrapped in an AggregateException
            // If you were using the 'await' keyword, the compiler would take care of unwrapping the AggregateException
            // Depending on when the cancellation occurs, you can either get an error from SQL Server or from .Net
            if ((ex.InnerException is SqlException) || (ex.InnerException is TaskCanceledException)) {
               // This is an expected exception
               Console.WriteLine("Got expected exception: {0}", ex.InnerException.Message);
            }
            else {
               // Did not expect this exception - re-throw it
               throw;
            }
         }

         Console.WriteLine("Done");
      }

      // This is used to generate the files which are used by the other sample methods
      private static void CreateDemoFiles() {
         Random rand = new Random();
         byte[] data = new byte[1024];
         rand.NextBytes(data);

         using (FileStream file = File.Open("binarydata.bin", FileMode.Create)) {
            file.Write(data, 0, data.Length);
         }

         using (StreamWriter writer = new StreamWriter(File.Open("textdata.txt", FileMode.Create))) {
            writer.Write(Convert.ToBase64String(data));
         }
      }

      // Application transferring a large BLOB to SQL Server in .NET 4.5
      private static async Task StreamBLOBToServer() {
         using (SqlConnection conn = new SqlConnection(connectionString)) {
            await conn.OpenAsync();
            using (SqlCommand cmd = new SqlCommand("INSERT INTO [BinaryStreams] (bindata) VALUES (@bindata)", conn)) {
               using (FileStream file = File.Open("binarydata.bin", FileMode.Open)) {

                  // Add a parameter which uses the FileStream we just opened
                  // Size is set to -1 to indicate "MAX"
                  cmd.Parameters.Add("@bindata", SqlDbType.Binary, -1).Value = file;

                  // Send the data to the server asynchronously
                  await cmd.ExecuteNonQueryAsync();
               }
            }
         }
      }

      // Application transferring a large Text File to SQL Server in .NET 4.5
      private static async Task StreamTextToServer() {
         using (SqlConnection conn = new SqlConnection(connectionString)) {
            await conn.OpenAsync();
            using (SqlCommand cmd = new SqlCommand("INSERT INTO [TextStreams] (textdata) VALUES (@textdata)", conn)) {
               using (StreamReader file = File.OpenText("textdata.txt")) {

                  // Add a parameter which uses the StreamReader we just opened
                  // Size is set to -1 to indicate "MAX"
                  cmd.Parameters.Add("@textdata", SqlDbType.NVarChar, -1).Value = file;

                  // Send the data to the server asynchronously
                  await cmd.ExecuteNonQueryAsync();
               }
            }
         }
      }

      // Cancelling the transfer of a large BLOB
      private static async Task CancelBLOBStream(CancellationToken cancellationToken) {
         using (SqlConnection conn = new SqlConnection(connectionString)) {
            // We can cancel not only sending the data to the server, but also opening the connection
            await conn.OpenAsync(cancellationToken);

            // Artificially delay the command by 100ms
            using (SqlCommand cmd = new SqlCommand("WAITFOR DELAY '00:00:00:100';INSERT INTO [BinaryStreams] (bindata) VALUES (@bindata)", conn)) {
               using (FileStream file = File.Open("binarydata.bin", FileMode.Open)) {

                  // Add a parameter which uses the FileStream we just opened
                  // Size is set to -1 to indicate "MAX"
                  cmd.Parameters.Add("@bindata", SqlDbType.Binary, -1).Value = file;

                  // Send the data to the server asynchronously
                  // Pass the cancellation token such that the command will be cancelled if needed
                  await cmd.ExecuteNonQueryAsync(cancellationToken);
               }
            }
         }
      }
   }
}
```

## <a name="sample----streaming-from-one-sql-server-to-another-sql-server"></a><span data-ttu-id="9772b-149">Próbkowanie — przesyłanie strumieniowe z jednego SQL Server do innego SQL Server</span><span class="sxs-lookup"><span data-stu-id="9772b-149">Sample -- Streaming From One SQL Server to Another SQL Server</span></span>

<span data-ttu-id="9772b-150">Ten przykład pokazuje, jak asynchronicznie przesyłać strumieniowo duże obiekty BLOB z jednego SQL Server do drugiego, z obsługą anulowania.</span><span class="sxs-lookup"><span data-stu-id="9772b-150">This sample demonstrates how to asynchronously stream a large BLOB from one SQL Server to another, with support for cancellation.</span></span>

```csharp
using System;
using System.Data;
using System.Data.SqlClient;
using System.IO;
using System.Threading;
using System.Threading.Tasks;

namespace StreamingFromServerToAnother {
   class Program {
      // Replace the connection string if needed, for instance to connect to SQL Express: @"Server=(local)\SQLEXPRESS;Database=Demo2;Integrated Security=true"
      private const string connectionString = @"Server=(localdb)\V11.0;Database=Demo2";

      static void Main(string[] args) {
         // For this example, we don't want to cancel
         // So we can pass in a "blank" cancellation token
         E2EStream(CancellationToken.None).Wait();

         Console.WriteLine("Done");
      }

      // Streaming from one SQL Server to Another One using the new Async.NET
      private static async Task E2EStream(CancellationToken cancellationToken) {
         using (SqlConnection readConn = new SqlConnection(connectionString)) {
            using (SqlConnection writeConn = new SqlConnection(connectionString)) {

               // Note that we are using the same cancellation token for calls to both connections\commands
               // Also we can start both the connection opening asynchronously, and then wait for both to complete
               Task openReadConn = readConn.OpenAsync(cancellationToken);
               Task openWriteConn = writeConn.OpenAsync(cancellationToken);
               await Task.WhenAll(openReadConn, openWriteConn);

               using (SqlCommand readCmd = new SqlCommand("SELECT [bindata] FROM [BinaryStreams]", readConn)) {
                  using (SqlCommand writeCmd = new SqlCommand("INSERT INTO [BinaryStreamsCopy] (bindata) VALUES (@bindata)", writeConn)) {

                     // Add an empty parameter to the write command which will be used for the streams we are copying
                     // Size is set to -1 to indicate "MAX"
                     SqlParameter streamParameter = writeCmd.Parameters.Add("@bindata", SqlDbType.Binary, -1);

                     // The reader needs to be executed with the SequentialAccess behavior to enable network streaming
                     // Otherwise ReadAsync will buffer the entire BLOB into memory which can cause scalability issues or even OutOfMemoryExceptions
                     using (SqlDataReader reader = await readCmd.ExecuteReaderAsync(CommandBehavior.SequentialAccess, cancellationToken)) {
                        while (await reader.ReadAsync(cancellationToken)) {
                           // Grab a stream to the binary data in the source database
                           using (Stream dataStream = reader.GetStream(0)) {

                              // Set the parameter value to the stream source that was opened
                              streamParameter.Value = dataStream;

                              // Asynchronously send data from one database to another
                              await writeCmd.ExecuteNonQueryAsync(cancellationToken);
                           }
                        }
                     }
                  }
               }
            }
         }
      }
   }
}
```

## <a name="see-also"></a><span data-ttu-id="9772b-151">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="9772b-151">See also</span></span>

- [<span data-ttu-id="9772b-152">Pobieranie i modyfikowanie danych ADO.NET</span><span class="sxs-lookup"><span data-stu-id="9772b-152">Retrieving and Modifying Data in ADO.NET</span></span>](retrieving-and-modifying-data.md)
