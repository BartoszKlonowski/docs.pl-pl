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
# <a name="blob-io"></a>We/wy obiektu blob

> [!NOTE]
> Klasa SqliteBlob została dodana w wersji 3,0.

Można zmniejszyć użycie pamięci podczas odczytywania i pisania dużych obiektów przez przesyłanie strumieniowe danych do i z bazy danych. Może to być szczególnie przydatne podczas analizowania lub przekształcania danych.

Zacznij od wstawienia wiersza jako normalny. Użyj `zeroblob()` funkcji SQL w celu przydzielenia miejsca w bazie danych w celu przechowywania dużego obiektu. `last_insert_rowid()`Funkcja zapewnia wygodny sposób uzyskiwania jego ROWID.

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/StreamingSample/Program.cs?name=snippet_Insert)]

Po wstawieniu wiersza Otwórz strumień, aby napisać duży obiekt za pomocą <xref:Microsoft.Data.Sqlite.SqliteBlob> .

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/StreamingSample/Program.cs?name=snippet_Write)]

Aby przesłać strumieniowo duży obiekt z bazy danych, musisz wybrać identyfikator RowId lub jeden z jego aliasów, jak pokazano tutaj, oprócz kolumny dużego obiektu. Jeśli nie wybierzesz ROWID, cały obiekt zostanie załadowany do pamięci. Obiekt zwrócony przez to `GetStream()` `SqliteBlob` po poprawnym wykonaniu.

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/StreamingSample/Program.cs?name=snippet_Read)]
