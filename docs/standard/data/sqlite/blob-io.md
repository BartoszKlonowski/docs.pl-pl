---
title: We/wy obiektu blob
ms.date: 12/08/2020
description: Dowiedz się, jak używać funkcji we/wy obiektu BLOB firmy SQLite.
ms.openlocfilehash: 8b305669f3155d2366215e9a05beb5ed51533d81
ms.sourcegitcommit: 9b877e160c326577e8aa5ead22a937110d80fa44
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2020
ms.locfileid: "97110048"
---
# <a name="blob-io"></a><span data-ttu-id="d4a68-103">We/wy obiektu blob</span><span class="sxs-lookup"><span data-stu-id="d4a68-103">Blob I/O</span></span>

> [!NOTE]
> <span data-ttu-id="d4a68-104">Klasa SqliteBlob została dodana w wersji 3,0.</span><span class="sxs-lookup"><span data-stu-id="d4a68-104">The SqliteBlob class was added in version 3.0.</span></span>

<span data-ttu-id="d4a68-105">Można zmniejszyć użycie pamięci podczas odczytywania i pisania dużych obiektów przez przesyłanie strumieniowe danych do i z bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d4a68-105">You can reduce memory usage while reading and writing large objects by streaming the data into and out of the database.</span></span> <span data-ttu-id="d4a68-106">Może to być szczególnie przydatne podczas analizowania lub przekształcania danych.</span><span class="sxs-lookup"><span data-stu-id="d4a68-106">This can be especially useful when parsing or transforming the data.</span></span>

<span data-ttu-id="d4a68-107">Zacznij od wstawienia wiersza jako normalny.</span><span class="sxs-lookup"><span data-stu-id="d4a68-107">Start by inserting a row as normal.</span></span> <span data-ttu-id="d4a68-108">Użyj `zeroblob()` funkcji SQL w celu przydzielenia miejsca w bazie danych w celu przechowywania dużego obiektu.</span><span class="sxs-lookup"><span data-stu-id="d4a68-108">Use the `zeroblob()` SQL function to allocate space in the database to hold the large object.</span></span> <span data-ttu-id="d4a68-109">`last_insert_rowid()`Funkcja zapewnia wygodny sposób uzyskiwania jego ROWID.</span><span class="sxs-lookup"><span data-stu-id="d4a68-109">The `last_insert_rowid()` function provides a convenient way to get its rowid.</span></span>

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/StreamingSample/Program.cs?name=snippet_Insert)]

<span data-ttu-id="d4a68-110">Po wstawieniu wiersza Otwórz strumień, aby napisać duży obiekt za pomocą <xref:Microsoft.Data.Sqlite.SqliteBlob> .</span><span class="sxs-lookup"><span data-stu-id="d4a68-110">After inserting the row, open a stream to write the large object using <xref:Microsoft.Data.Sqlite.SqliteBlob>.</span></span>

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/StreamingSample/Program.cs?name=snippet_Write)]

<span data-ttu-id="d4a68-111">Aby przesłać strumieniowo duży obiekt z bazy danych, musisz wybrać identyfikator RowId lub jeden z jego aliasów, jak pokazano tutaj, oprócz kolumny dużego obiektu.</span><span class="sxs-lookup"><span data-stu-id="d4a68-111">To stream the large object out of the database, you must select the rowid or one of its aliases as show here in addition to the large object's column.</span></span> <span data-ttu-id="d4a68-112">Jeśli nie wybierzesz ROWID, cały obiekt zostanie załadowany do pamięci.</span><span class="sxs-lookup"><span data-stu-id="d4a68-112">If you don't select the rowid, the entire object will be loaded into memory.</span></span> <span data-ttu-id="d4a68-113">Obiekt zwrócony przez to `GetStream()` `SqliteBlob` po poprawnym wykonaniu.</span><span class="sxs-lookup"><span data-stu-id="d4a68-113">The object returned by `GetStream()` will be a `SqliteBlob` when done correctly.</span></span>

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/StreamingSample/Program.cs?name=snippet_Read)]
