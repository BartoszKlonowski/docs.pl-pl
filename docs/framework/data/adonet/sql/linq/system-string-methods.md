---
title: System.String, metody
ms.date: 03/30/2017
ms.assetid: ce307f14-87e6-4816-8694-8a4147f6b784
ms.openlocfilehash: 44d32ed1000ca49d9fc29ffcde4506b44fc975b6
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91155669"
---
# <a name="systemstring-methods"></a><span data-ttu-id="f3bf8-102">System.String, metody</span><span class="sxs-lookup"><span data-stu-id="f3bf8-102">System.String Methods</span></span>

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <span data-ttu-id="f3bf8-103">Program nie obsługuje następujących <xref:System.String> metod.</span><span class="sxs-lookup"><span data-stu-id="f3bf8-103">does not support the following <xref:System.String> methods.</span></span>  
  
## <a name="unsupported-systemstring-methods-in-general"></a><span data-ttu-id="f3bf8-104">Ogólnie nieobsługiwane metody System. String</span><span class="sxs-lookup"><span data-stu-id="f3bf8-104">Unsupported System.String Methods in General</span></span>  

 <span data-ttu-id="f3bf8-105">Ogólnie nieobsługiwane <xref:System.String> metody:</span><span class="sxs-lookup"><span data-stu-id="f3bf8-105">Unsupported <xref:System.String> methods in general:</span></span>  
  
- <span data-ttu-id="f3bf8-106">Przeciążenia z uwzględnieniem kultury (metody, które przyjmują `CultureInfo`  /  `StringComparison`  /  `IFormatProvider` ).</span><span class="sxs-lookup"><span data-stu-id="f3bf8-106">Culture-aware overloads (methods that take a `CultureInfo` / `StringComparison` / `IFormatProvider`).</span></span>  
  
- <span data-ttu-id="f3bf8-107">Metody, które pobierają lub tworzą `char` tablicę.</span><span class="sxs-lookup"><span data-stu-id="f3bf8-107">Methods that take or produce a `char` array.</span></span>  
  
## <a name="unsupported-systemstring-static-methods"></a><span data-ttu-id="f3bf8-108">Nieobsługiwana metoda statyczna system. String</span><span class="sxs-lookup"><span data-stu-id="f3bf8-108">Unsupported System.String Static Methods</span></span>  
  
|<span data-ttu-id="f3bf8-109">Nieobsługiwana metoda statyczna system. String</span><span class="sxs-lookup"><span data-stu-id="f3bf8-109">Unsupported System.String Static Methods</span></span>|  
|----------------------------------------------|  
|<xref:System.String.Copy%28System.String%29?displayProperty=nameWithType>|  
|<xref:System.String.Compare%28System.String%2CSystem.String%2CSystem.Boolean%29?displayProperty=nameWithType>|  
|<xref:System.String.Compare%28System.String%2CSystem.String%2CSystem.Boolean%2CSystem.Globalization.CultureInfo%29?displayProperty=nameWithType>|  
|<xref:System.String.Compare%28System.String%2CSystem.Int32%2CSystem.String%2CSystem.Int32%2CSystem.Int32%29?displayProperty=nameWithType>|  
|<xref:System.String.Compare%28System.String%2CSystem.Int32%2CSystem.String%2CSystem.Int32%2CSystem.Int32%2CSystem.Boolean%29?displayProperty=nameWithType>|  
|<xref:System.String.Compare%28System.String%2CSystem.Int32%2CSystem.String%2CSystem.Int32%2CSystem.Int32%2CSystem.Boolean%2CSystem.Globalization.CultureInfo%29?displayProperty=nameWithType>|  
|<xref:System.String.CompareOrdinal%28System.String%2CSystem.String%29?displayProperty=nameWithType>|  
|<xref:System.String.CompareOrdinal%28System.String%2CSystem.Int32%2CSystem.String%2CSystem.Int32%2CSystem.Int32%29?displayProperty=nameWithType>|  
|<xref:System.String.Format%2A?displayProperty=nameWithType>|  
|<xref:System.String.Join%2A?displayProperty=nameWithType>|  
  
## <a name="unsupported-systemstring-non-static-methods"></a><span data-ttu-id="f3bf8-110">Nieobsługiwana Metoda niestatyczna system. String</span><span class="sxs-lookup"><span data-stu-id="f3bf8-110">Unsupported System.String Non-static Methods</span></span>  
  
|<span data-ttu-id="f3bf8-111">Nieobsługiwana Metoda niestatyczna system. String</span><span class="sxs-lookup"><span data-stu-id="f3bf8-111">Unsupported System.String Non-static Methods</span></span>|  
|---------------------------------------------------|  
|<xref:System.String.IndexOfAny%28System.Char%5B%5D%29?displayProperty=nameWithType>|  
|<xref:System.String.Split%2A?displayProperty=nameWithType>|  
|<xref:System.String.ToCharArray?displayProperty=nameWithType>|  
|<xref:System.String.ToUpper%28System.Globalization.CultureInfo%29?displayProperty=nameWithType>|  
|<xref:System.String.TrimEnd%28System.Char%5B%5D%29?displayProperty=nameWithType>|  
|<xref:System.String.TrimStart%28System.Char%5B%5D%29?displayProperty=nameWithType>|  
  
## <a name="differences-from-net"></a><span data-ttu-id="f3bf8-112">Różnice od platformy .NET</span><span class="sxs-lookup"><span data-stu-id="f3bf8-112">Differences from .NET</span></span>  
  
- <span data-ttu-id="f3bf8-113">Zapytania nie uwzględniają sortowania SQL Server, które mogą być stosowane na serwerze i w związku z tym domyślnie udostępniają niezależne od wielkości liter porównania.</span><span class="sxs-lookup"><span data-stu-id="f3bf8-113">Queries do not account for SQL Server collations that might be in effect on the server, and therefore will provide culture-sensitive, case-insensitive comparisons by default.</span></span> <span data-ttu-id="f3bf8-114">To zachowanie różni się od domyślnej, zależnej od wielkości liter semantyki .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="f3bf8-114">This behavior differs from the default, case-sensitive semantics of the .NET Framework.</span></span>  
  
- <span data-ttu-id="f3bf8-115">Gdy `LastIndexOf` zwraca wartość 0, ciąg jest `NULL` lub pozycja znaleziona ma wartość 0.</span><span class="sxs-lookup"><span data-stu-id="f3bf8-115">When `LastIndexOf` returns 0, either the string is `NULL` or the found position is 0.</span></span>  
  
- <span data-ttu-id="f3bf8-116">Nieoczekiwane wyniki mogą zostać zwrócone z łączenia lub innych operacji na ciągach o stałej długości ( `CHAR` , `NCHAR` ), ponieważ te typy automatycznie mają uzupełnienie zastosowane w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="f3bf8-116">Unexpected results might be returned from concatenation or other operations on fixed-length strings (`CHAR`, `NCHAR`), because these types automatically have padding applied in the database.</span></span>  
  
- <span data-ttu-id="f3bf8-117">Ze względu na to, że wiele metod, takich jak `Replace` ,, `ToLower` `ToUpper` i indeksator znaku, nie ma prawidłowych tłumaczeń dla `TEXT` `NTEXT` kolumn i XML, `SqlExceptions` występuje w przypadku przetłumaczenia normalnego.</span><span class="sxs-lookup"><span data-stu-id="f3bf8-117">Because many methods, such as `Replace`, `ToLower`, `ToUpper`, and the character indexer, have no valid translation for `TEXT` or `NTEXT` columns and XML, `SqlExceptions` occur if translated normally.</span></span> <span data-ttu-id="f3bf8-118">Takie zachowanie jest uznawane za akceptowalne dla tych typów.</span><span class="sxs-lookup"><span data-stu-id="f3bf8-118">This behavior is considered acceptable for these types.</span></span> <span data-ttu-id="f3bf8-119">Jednak wszystkie operacje na ciągach muszą być zgodne z semantyką środowiska uruchomieniowego języka wspólnego (CLR) dla `VARCHAR` , `NVARCHAR` , `VARCHAR(max)` i `NVARCHAR(max)` .</span><span class="sxs-lookup"><span data-stu-id="f3bf8-119">However, all string operations must match common language runtime (CLR) semantics for `VARCHAR`, `NVARCHAR`, `VARCHAR(max)`, and `NVARCHAR(max)`.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="f3bf8-120">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="f3bf8-120">See also</span></span>

- [<span data-ttu-id="f3bf8-121">Typy danych i funkcje</span><span class="sxs-lookup"><span data-stu-id="f3bf8-121">Data Types and Functions</span></span>](data-types-and-functions.md)
