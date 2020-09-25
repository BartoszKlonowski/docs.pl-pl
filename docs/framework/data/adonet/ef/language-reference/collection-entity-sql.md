---
title: Kolekcja (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 03228bfa-be3a-4ccc-82f8-eee429f85cf1
ms.openlocfilehash: c960ee69f8188f6dd3184b6fb31f3432f8d58fee
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91197953"
---
# <a name="collection-entity-sql"></a><span data-ttu-id="98e75-102">Kolekcja (Entity SQL)</span><span class="sxs-lookup"><span data-stu-id="98e75-102">COLLECTION (Entity SQL)</span></span>

<span data-ttu-id="98e75-103">Słowo kluczowe COLLECTION jest używane tylko w definicji wbudowanej funkcji.</span><span class="sxs-lookup"><span data-stu-id="98e75-103">The COLLECTION keyword is only used in the definition of an inline function.</span></span> <span data-ttu-id="98e75-104">Funkcje kolekcji to funkcje, które działają na kolekcji wartości i tworzą skalarne dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="98e75-104">Collection functions are functions that operate on a collection of values and produce a scalar output.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="98e75-105">Składnia</span><span class="sxs-lookup"><span data-stu-id="98e75-105">Syntax</span></span>  
  
```csharp  
COLLECTION(type_definition)
```  
  
## <a name="arguments"></a><span data-ttu-id="98e75-106">Argumenty</span><span class="sxs-lookup"><span data-stu-id="98e75-106">Arguments</span></span>  

 `type_definition`  
 <span data-ttu-id="98e75-107">Wyrażenie zwracające kolekcję obsługiwanych typów, wierszy lub odwołań.</span><span class="sxs-lookup"><span data-stu-id="98e75-107">An expression that returns a collection of supported types, rows, or references.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="98e75-108">Uwagi</span><span class="sxs-lookup"><span data-stu-id="98e75-108">Remarks</span></span>  

 <span data-ttu-id="98e75-109">Aby uzyskać więcej informacji na temat słowa kluczowego kolekcja, zobacz [definicje typów](type-definitions-entity-sql.md).</span><span class="sxs-lookup"><span data-stu-id="98e75-109">For more information about the COLLECTION keyword, see [Type Definitions](type-definitions-entity-sql.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="98e75-110">Przykład</span><span class="sxs-lookup"><span data-stu-id="98e75-110">Example</span></span>  

 <span data-ttu-id="98e75-111">Poniższy przykład pokazuje, jak używać słowa kluczowego COLLECTION do deklarowania kolekcji miejsc dziesiętnych jako argumentu dla wbudowanej funkcji zapytania.</span><span class="sxs-lookup"><span data-stu-id="98e75-111">The following sample shows how to use the COLLECTION keyword to declare a collection of decimals as an argument for an inline query function.</span></span>  
  
 [!code-csharp[DP EntityServices Concepts 2#Collection_GroupPartition](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#collection_grouppartition)]  
  
## <a name="see-also"></a><span data-ttu-id="98e75-112">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="98e75-112">See also</span></span>

- [<span data-ttu-id="98e75-113">Odwołanie do jednostki SQL</span><span class="sxs-lookup"><span data-stu-id="98e75-113">Entity SQL Reference</span></span>](entity-sql-reference.md)
