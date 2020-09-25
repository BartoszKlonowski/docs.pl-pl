---
title: NAKŁADAją się (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 41743e89-79cb-4d7b-8a27-355b45024b61
ms.openlocfilehash: 6902a44af343c37ccb26412738d9f96b28551814
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91204427"
---
# <a name="overlaps-entity-sql"></a><span data-ttu-id="ac702-102">NAKŁADAją się (Entity SQL)</span><span class="sxs-lookup"><span data-stu-id="ac702-102">OVERLAPS (Entity SQL)</span></span>

<span data-ttu-id="ac702-103">Określa, czy dwie kolekcje mają wspólne elementy.</span><span class="sxs-lookup"><span data-stu-id="ac702-103">Determines whether two collections have common elements.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="ac702-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="ac702-104">Syntax</span></span>  
  
```sql  
expression OVERLAPS expression  
```  
  
## <a name="arguments"></a><span data-ttu-id="ac702-105">Argumenty</span><span class="sxs-lookup"><span data-stu-id="ac702-105">Arguments</span></span>  

 `expression`  
 <span data-ttu-id="ac702-106">Każde prawidłowe wyrażenie zapytania, które zwraca kolekcję do porównania z kolekcją zwróconą z innego wyrażenia zapytania.</span><span class="sxs-lookup"><span data-stu-id="ac702-106">Any valid query expression that returns a collection to compare with the collection returned from another query expression.</span></span> <span data-ttu-id="ac702-107">Wszystkie wyrażenia muszą być tego samego typu lub według wspólnego typu podstawowego lub pochodnego `expression` .</span><span class="sxs-lookup"><span data-stu-id="ac702-107">All expressions must be of the same type or of a common base or derived type as `expression`.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="ac702-108">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="ac702-108">Return Value</span></span>  

 <span data-ttu-id="ac702-109">`true` Jeśli dwie kolekcje mają wspólne elementy; w przeciwnym razie `false` .</span><span class="sxs-lookup"><span data-stu-id="ac702-109">`true` if the two collections have common elements; otherwise, `false`.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="ac702-110">Uwagi</span><span class="sxs-lookup"><span data-stu-id="ac702-110">Remarks</span></span>  

 <span data-ttu-id="ac702-111">NAKŁADAjące się funkcje zapewniają funkcję równoważną z następującymi:</span><span class="sxs-lookup"><span data-stu-id="ac702-111">OVERLAPS provides functionally equivalent to the following:</span></span>  
  
 `EXISTS ( expression INTERSECT expression )`  
  
 <span data-ttu-id="ac702-112">NAKŁADAnie się jest jednym z [!INCLUDE[esql](../../../../../../includes/esql-md.md)] operatorów zestawu.</span><span class="sxs-lookup"><span data-stu-id="ac702-112">OVERLAPS is one of the [!INCLUDE[esql](../../../../../../includes/esql-md.md)] set operators.</span></span> <span data-ttu-id="ac702-113">Wszystkie [!INCLUDE[esql](../../../../../../includes/esql-md.md)] Operatory zestawów są oceniane od lewej do prawej.</span><span class="sxs-lookup"><span data-stu-id="ac702-113">All [!INCLUDE[esql](../../../../../../includes/esql-md.md)] set operators are evaluated from left to right.</span></span> <span data-ttu-id="ac702-114">Aby uzyskać informacje o pierwszeństwie dla [!INCLUDE[esql](../../../../../../includes/esql-md.md)] operatorów zestawu, zobacz [except](except-entity-sql.md).</span><span class="sxs-lookup"><span data-stu-id="ac702-114">For precedence information for the [!INCLUDE[esql](../../../../../../includes/esql-md.md)] set operators, see [EXCEPT](except-entity-sql.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="ac702-115">Przykład</span><span class="sxs-lookup"><span data-stu-id="ac702-115">Example</span></span>  

 <span data-ttu-id="ac702-116">Poniższe zapytanie Entity SQL używa operatora NAKŁADAnia się, aby określić, czy dwie kolekcje mają wspólną wartość.</span><span class="sxs-lookup"><span data-stu-id="ac702-116">The following Entity SQL query uses the OVERLAPS operator to determines whether two collections have a common value.</span></span> <span data-ttu-id="ac702-117">Zapytanie jest oparte na modelu sprzedaży AdventureWorks.</span><span class="sxs-lookup"><span data-stu-id="ac702-117">The query is based on the AdventureWorks Sales Model.</span></span> <span data-ttu-id="ac702-118">Aby skompilować i uruchomić, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="ac702-118">To compile and run this, follow these steps:</span></span>  
  
1. <span data-ttu-id="ac702-119">Postępuj zgodnie z procedurą w temacie [How to: Execute a Query zwracającej wyniki StructuralType](../how-to-execute-a-query-that-returns-structuraltype-results.md).</span><span class="sxs-lookup"><span data-stu-id="ac702-119">Follow the procedure in [How to: Execute a Query that Returns StructuralType Results](../how-to-execute-a-query-that-returns-structuraltype-results.md).</span></span>  
  
2. <span data-ttu-id="ac702-120">Przekaż następujące zapytanie jako argument do `ExecuteStructuralTypeQuery` metody:</span><span class="sxs-lookup"><span data-stu-id="ac702-120">Pass the following query as an argument to the `ExecuteStructuralTypeQuery` method:</span></span>  
  
 [!code-sql[DP EntityServices Concepts#OVERLAPS](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#overlaps)]  
  
## <a name="see-also"></a><span data-ttu-id="ac702-121">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="ac702-121">See also</span></span>

- [<span data-ttu-id="ac702-122">Odwołanie do jednostki SQL</span><span class="sxs-lookup"><span data-stu-id="ac702-122">Entity SQL Reference</span></span>](entity-sql-reference.md)
