---
title: Konstruktor nazwanego typu (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 549dea04-d93d-4c87-a292-f81b1598dbfd
ms.openlocfilehash: c673b58ee5811e3d3b74b3744d3f5291888e2253
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2020
ms.locfileid: "91197784"
---
# <a name="named-type-constructor-entity-sql"></a><span data-ttu-id="4a0ff-102">Konstruktor nazwanego typu (Entity SQL)</span><span class="sxs-lookup"><span data-stu-id="4a0ff-102">Named Type Constructor (Entity SQL)</span></span>

<span data-ttu-id="4a0ff-103">Służy do tworzenia wystąpień typów nominalnych modelu koncepcyjnego, takich jak jednostki lub typy złożone.</span><span class="sxs-lookup"><span data-stu-id="4a0ff-103">Used to create instances of conceptual model nominal types such as Entity or Complex types.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="4a0ff-104">Składnia</span><span class="sxs-lookup"><span data-stu-id="4a0ff-104">Syntax</span></span>  
  
```sql  
[{identifier. }] identifier( [expression [{, expression }]] )  
```  
  
## <a name="arguments"></a><span data-ttu-id="4a0ff-105">Argumenty</span><span class="sxs-lookup"><span data-stu-id="4a0ff-105">Arguments</span></span>  

 `identifier`  
 <span data-ttu-id="4a0ff-106">Wartość, która jest prostym lub w cudzysłowie identyfikatorem.</span><span class="sxs-lookup"><span data-stu-id="4a0ff-106">Value that is a simple or quoted identifier.</span></span> <span data-ttu-id="4a0ff-107">Aby uzyskać więcej informacji, zobacz [identyfikatory](identifiers-entity-sql.md)</span><span class="sxs-lookup"><span data-stu-id="4a0ff-107">For more information see, [Identifiers](identifiers-entity-sql.md)</span></span>  
  
 `expression`  
 <span data-ttu-id="4a0ff-108">Atrybuty typu, które mają być w tej samej kolejności, w jakiej występują w deklaracji typu.</span><span class="sxs-lookup"><span data-stu-id="4a0ff-108">Attributes of the type that are assumed to be in the same order as they appear in the declaration of the type.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="4a0ff-109">Wartość zwracana</span><span class="sxs-lookup"><span data-stu-id="4a0ff-109">Return Value</span></span>  

 <span data-ttu-id="4a0ff-110">Wystąpienia o nazwanych typach złożonych i typach jednostek.</span><span class="sxs-lookup"><span data-stu-id="4a0ff-110">Instances of named complex types and entity types.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="4a0ff-111">Uwagi</span><span class="sxs-lookup"><span data-stu-id="4a0ff-111">Remarks</span></span>  

 <span data-ttu-id="4a0ff-112">W poniższych przykładach pokazano, jak utworzyć typy nominalne i złożone:</span><span class="sxs-lookup"><span data-stu-id="4a0ff-112">The following examples show how to construct nominal and complex types:</span></span>  
  
 <span data-ttu-id="4a0ff-113">Poniższe wyrażenie tworzy wystąpienie `Person` typu:</span><span class="sxs-lookup"><span data-stu-id="4a0ff-113">The expression below creates an instance of a `Person` type:</span></span>  
  
 `Person("abc", 12)`  
  
 <span data-ttu-id="4a0ff-114">Poniższe wyrażenie tworzy wystąpienie typu złożonego:</span><span class="sxs-lookup"><span data-stu-id="4a0ff-114">The expression below creates an instance of a complex type:</span></span>  
  
 `MyModel.ZipCode(‘98118’, ‘4567’)`  
  
 <span data-ttu-id="4a0ff-115">Poniższe wyrażenie tworzy wystąpienie zagnieżdżonego typu złożonego:</span><span class="sxs-lookup"><span data-stu-id="4a0ff-115">The expression below creates an instance of a nested complex type:</span></span>  
  
 `MyModel.AddressInfo('My street address', 'Seattle', 'WA', MyModel.ZipCode('98118', '4567'))`  
  
 <span data-ttu-id="4a0ff-116">Poniższe wyrażenie tworzy wystąpienie jednostki z zagnieżdżonym typem złożonym:</span><span class="sxs-lookup"><span data-stu-id="4a0ff-116">The expression below creates an instance of an entity with a nested complex type:</span></span>  
  
 `MyModel.Person("Bill", MyModel.AddressInfo('My street address', 'Seattle', 'WA', MyModel.ZipCode('98118', '4567')))`  
  
 <span data-ttu-id="4a0ff-117">Poniższy przykład pokazuje, jak zainicjować właściwość typu złożonego do wartości null:`MyModel.ZipCode(‘98118’, null)`</span><span class="sxs-lookup"><span data-stu-id="4a0ff-117">The following example shows how to initialize a property of a complex type to null:`MyModel.ZipCode(‘98118’, null)`</span></span>  
  
## <a name="example"></a><span data-ttu-id="4a0ff-118">Przykład</span><span class="sxs-lookup"><span data-stu-id="4a0ff-118">Example</span></span>  

 <span data-ttu-id="4a0ff-119">Poniższe zapytanie Entity SQL używa konstruktora nazwanego typu w celu utworzenia wystąpienia typu modelu koncepcyjnego.</span><span class="sxs-lookup"><span data-stu-id="4a0ff-119">The following Entity SQL query uses the named type constructor to create an instance of a conceptual model type.</span></span> <span data-ttu-id="4a0ff-120">Zapytanie jest oparte na modelu sprzedaży AdventureWorks.</span><span class="sxs-lookup"><span data-stu-id="4a0ff-120">The query is based on the AdventureWorks Sales Model.</span></span> <span data-ttu-id="4a0ff-121">Aby skompilować i uruchomić to zapytanie, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="4a0ff-121">To compile and run this query, follow these steps:</span></span>  
  
1. <span data-ttu-id="4a0ff-122">Postępuj zgodnie z procedurą w temacie [How to: Execute a Query zwracającej wyniki StructuralType](../how-to-execute-a-query-that-returns-structuraltype-results.md).</span><span class="sxs-lookup"><span data-stu-id="4a0ff-122">Follow the procedure in [How to: Execute a Query that Returns StructuralType Results](../how-to-execute-a-query-that-returns-structuraltype-results.md).</span></span>  
  
2. <span data-ttu-id="4a0ff-123">Przekaż następujące zapytanie jako argument do `ExecuteStructuralTypeQuery` metody:</span><span class="sxs-lookup"><span data-stu-id="4a0ff-123">Pass the following query as an argument to the `ExecuteStructuralTypeQuery` method:</span></span>  
  
 [!code-sql[DP EntityServices Concepts#NAMED_TYPE_CONSTRUCTOR](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#named_type_constructor)]  
  
## <a name="see-also"></a><span data-ttu-id="4a0ff-124">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="4a0ff-124">See also</span></span>

- [<span data-ttu-id="4a0ff-125">Konstruowanie typów</span><span class="sxs-lookup"><span data-stu-id="4a0ff-125">Constructing Types</span></span>](constructing-types-entity-sql.md)
- [<span data-ttu-id="4a0ff-126">Odwołanie do jednostki SQL</span><span class="sxs-lookup"><span data-stu-id="4a0ff-126">Entity SQL Reference</span></span>](entity-sql-reference.md)
