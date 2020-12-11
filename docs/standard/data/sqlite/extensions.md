---
title: Rozszerzenia
ms.date: 12/08/2020
description: Dowiedz się, jak ładować rozszerzenia oprogramowania SQLite.
ms.openlocfilehash: 68d31093662f373d6ebf4460d6a5d44029c27c5c
ms.sourcegitcommit: 9b877e160c326577e8aa5ead22a937110d80fa44
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2020
ms.locfileid: "97110848"
---
# <a name="extensions"></a><span data-ttu-id="166fd-103">Rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="166fd-103">Extensions</span></span>

<span data-ttu-id="166fd-104">Program SQLite obsługuje ładowanie rozszerzeń w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="166fd-104">SQLite supports loading extensions at run time.</span></span> <span data-ttu-id="166fd-105">Rozszerzenia obejmują elementy, takie jak dodatkowe funkcje SQL, sortowania, tabele wirtualne i nie tylko.</span><span class="sxs-lookup"><span data-stu-id="166fd-105">Extensions include things like additional SQL functions, collations, virtual tables, and more.</span></span>

<span data-ttu-id="166fd-106">Platforma .NET Core zawiera dodatkową logikę do lokalizowania bibliotek natywnych w dodatkowych miejscach, takich jak pakiety NuGet, do których istnieją odwołania.</span><span class="sxs-lookup"><span data-stu-id="166fd-106">.NET Core includes additional logic for locating native libraries in additional places like referenced NuGet packages.</span></span> <span data-ttu-id="166fd-107">Niestety, program SQLite nie może wykorzystać tej logiki; Interfejs API platformy jest wywoływany bezpośrednio w celu załadowania bibliotek.</span><span class="sxs-lookup"><span data-stu-id="166fd-107">Unfortunately, SQLite can't leverage this logic; it calls the platform API directly to load libraries.</span></span> <span data-ttu-id="166fd-108">W związku z tym może być konieczne zmodyfikowanie ścieżki, LD_LIBRARY_PATH lub DYLD_LIBRARY_PATH zmiennych środowiskowych przed załadowaniem rozszerzeń programu SQLite.</span><span class="sxs-lookup"><span data-stu-id="166fd-108">Because of this, you may need to modify the PATH, LD_LIBRARY_PATH, or DYLD_LIBRARY_PATH environment variables before loading SQLite extensions.</span></span> <span data-ttu-id="166fd-109">Istnieje [przykład](https://github.com/dotnet/docs/blob/master/samples/snippets/standard/data/sqlite/ExtensionsSample/Program.cs) w witrynie GitHub, który pokazuje wyszukiwanie plików binarnych dla bieżącego środowiska uruchomieniowego w pakiecie NuGet, do którego istnieje odwołanie.</span><span class="sxs-lookup"><span data-stu-id="166fd-109">There's [a sample](https://github.com/dotnet/docs/blob/master/samples/snippets/standard/data/sqlite/ExtensionsSample/Program.cs) on GitHub that demonstrates finding binaries for the current runtime inside a referenced NuGet package.</span></span>

<span data-ttu-id="166fd-110">Aby załadować rozszerzenie, wywołaj <xref:Microsoft.Data.Sqlite.SqliteConnection.LoadExtension%2A> metodę.</span><span class="sxs-lookup"><span data-stu-id="166fd-110">To load an extension, call the <xref:Microsoft.Data.Sqlite.SqliteConnection.LoadExtension%2A> method.</span></span> <span data-ttu-id="166fd-111">Firma Microsoft. Data. sqlite zapewni załadowanie rozszerzenia, nawet jeśli połączenie zostanie zamknięte i ponownie otwarte.</span><span class="sxs-lookup"><span data-stu-id="166fd-111">Microsoft.Data.Sqlite will ensure that the extension remains loaded even if the connection is closed and reopened.</span></span>

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/ExtensionsSample/Program.cs?name=snippet_LoadExtension)]

> [!NOTE]
> <span data-ttu-id="166fd-112">Metoda LoadExtension została dodana w wersji 3,0.</span><span class="sxs-lookup"><span data-stu-id="166fd-112">The LoadExtension method was added in version 3.0.</span></span>

## <a name="see-also"></a><span data-ttu-id="166fd-113">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="166fd-113">See also</span></span>

* [<span data-ttu-id="166fd-114">Rozszerzenia do załadowania w czasie wykonywania</span><span class="sxs-lookup"><span data-stu-id="166fd-114">Run-Time Loadable Extensions</span></span>](https://www.sqlite.org/loadext.html)
